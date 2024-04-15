---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Тестирование инъекции шаблона на стороне сервера (SSTI)

|ID          |
|------------|
|WSTG-INPV-18|

## Обзор

Web-приложения для создания динамических HTML-страниц обычно используют технологии шаблонов на стороне сервера (Jinja2, Twig, FreeMaker и т.д.). Уязвимости инъекции шаблонов на стороне сервера (SSTI) возникают, когда пользовательский ввод встраивается в шаблон небезопасным образом и приводит к удалённому выполнению кода (RCE) на сервере. Любые функции, которые поддерживают расширенную пользовательскую разметку, могут быть уязвимы для SSTI, включая wiki-страницы, обзоры, маркетинговые приложения, CMS-системы и т.д. Некоторые шаблонизаторы для защиты от SSTI используют различные механизмы (например, песочницу, список разрешений и т.д.).

### Пример: Twig

Следующий пример представляет собой выдержку из проекта [Extreme Vulnerable Web Application](https://github.com/s4n7h0/xvwa):

```php
public function getFilter($name)
{
        [snip]
        foreach ($this->filterCallbacks as $callback) {
        if (false !== $filter = call_user_func($callback, $name)) {
            return $filter;
        }
    }
    return false;
}
```

В функции getFilter `call_user_func($callback, $name)` уязвим к SSTI: параметр `name` извлекается из HTTP-запроса GET и выполняется сервером:

![SSTI XVWA Example](images/SSTI_XVWA.jpeg)\
*Рисунок 4.7.18-1: Пример SSTI в XVWA*

### Пример: Flask/Jinja2

В следующем примере используется шаблонизатор Jinja2 из Flask. Функция `page` принимает параметр `name` из HTTP-запроса GET и отображает HTML-страницу с содержимым переменной `name`:

```python
@app.route("/page")
def page():
    name = request.values.get('name')
    output = Jinja2.from_string('Hello ' + name + '!').render()
    return output
```

Этот фрагмент кода уязвим для XSS, но также уязвим для SSTI. Используем в качестве полезной нагрузки в параметре `name`:

```bash
$ curl -g 'http://www.target.com/page?name={{7*7}}'
Hello 49!
```

## Задачи тестирования

- Найти уязвимые точки для инъекции шаблонов.
- Идентифицировать используемый шаблонизатор.
- Создать эксплойт.

## Как тестировать

Уязвимости SSTI существуют в контексте текста или кода. В контексте простого текста пользователям разрешено использовать «текст» произвольной формы в HTML-разметке. В контексте кода пользовательский ввод также может быть помещён в оператор шаблона (например, в имя переменной).

### Выявление уязвимости для инъекции шаблона

Первым шагом в тестировании SSTI в контексте простого текста является построение распространённых шаблонных выражений, используемых различными шаблонизаторами в качестве полезных нагрузок, и отслеживание ответов сервера, чтобы определить, какое шаблонное выражение было выполнено сервером.

Распространённые примеры шаблонных выражений:

```text
a{{bar}}b
a{{7*7}}
{var} ${var} {{var}} <%var%> [% var %]
```

На данном этапе рекомендуется использовать [обширный список тестовых строк/полезных нагрузок шаблонных  выражений](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection).

Тестирование SSTI в контексте кода немного отличается. Во-первых, тестировщик формирует запрос, который приводит либо к пустым ответам, либо к ответам с ошибками. В приведённом ниже примере параметр HTTP GET вставляется в переменную `personal_greeting` в операторе шаблона:

```text
personal_greeting=username
Hello user01
```

Используя следующую полезную нагрузку — ответ сервера — чистое "Hello":

```text
personal_greeting=username<tag>
Hello
```

Следующим шагом является выход из оператора шаблона и вставка HTML-тега после него с использованием следующей полезной нагрузки.

```text
personal_greeting=username}}<tag>
Hello user01 <tag>
```

### Идентификация шаблонизатора

Основываясь на информации, полученной на предыдущем шаге, теперь тестировщик должен определить, какой шаблонизатор используется, подставляя различные шаблонные выражения. На основе ответов сервера тестировщик делает вывод об используемом шаблонизаторе. Этот ручной подход более подробно обсуждается в [статье](https://portswigger.net/blog/server-side-template-injection?#Identify) на PortSwigger. Для автоматизации выявления уязвимости SSTI и механизма шаблонов доступны различные инструменты, включая [Tplmap](https://github.com/epinna/tplmap) или [расширение сканера Burp Suite с поддержкой обратной косой черты](https://github.com/PortSwigger/backslash-powered-scanner).

### Создание эксплойта RCE

Основная цель на этом этапе — определить, как получить дальнейший контроль над сервером с эксплойтом RCE, изучив документацию по шаблону и проведя исследования. Ключевые области интереса:

- **Для авторов шаблонов** — разделы, посвященные основному синтаксису.
- Разделы, посвященные **вопросам безопасности**.
- Списки встроенных методов, функций, фильтров и переменных.
- Списки расширений/плагинов.

Тестировщик также может определить, какие другие объекты, методы и свойства могут быть раскрыты, сосредоточившись на объекте `self`. Если объект `self` недоступен и документация не раскрывает технических деталей, рекомендуется использовать перебор по имени переменной. Как только объект идентифицирован, следующим шагом является анализ объекта, чтобы определить все его методы, свойства и атрибуты, доступные через шаблонизатор. Это может привести к выявлению других видов нарушений безопасности, включая повышение привилегий, раскрытие информации о паролях приложений, API-ключах, конфигурациях, переменных среды и т.д.

## Инструменты

- [Tplmap](https://github.com/epinna/tplmap)
- [Расширение сканера Burp Suite с поддержкой обратной косой черты](https://github.com/PortSwigger/backslash-powered-scanner)
- [Тестовые строки шаблонных выражений / список полезных нагрузок](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection)

## Ссылки

- [James Kettle: Server-Side Template Injection:RCE for the modern webapp (whitepaper)](https://portswigger.net/kb/papers/serversidetemplateinjection.pdf)
- [Server-Side Template Injection](https://portswigger.net/blog/server-side-template-injection)
- [Exploring SSTI in Flask/Jinja2](https://www.lanmaster53.com/2016/03/exploring-ssti-flask-jinja2/)
- [Server Side Template Injection: from detection to Remote shell](https://www.okiok.com/server-side-template-injection-from-detection-to-remote-shell/)
- [Extreme Vulnerable Web Application](https://github.com/s4n7h0/xvwa)
- [Divine Selorm Tsa: Exploiting server side template injection with tplmap](https://owasp.org/www-pdf-archive/Owasp_SSTI_final.pdf)
- [Exploiting SSTI in Thymeleaf](https://www.acunetix.com/blog/web-security-zone/exploiting-ssti-in-thymeleaf/)
