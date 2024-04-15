---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Тестирование HTML-инъекции

|ID          |
|------------|
|WSTG-CLNT-03|

## Обзор

HTML-инъекция — вид уязвимости, который возникает, когда пользователь может контролировать точку входа и вставлять произвольный HTML-код на уязвимую web-страницу. Эта уязвимость может иметь множество последствий, таких как раскрытие сессионных cookie пользователя, которые могут быть использованы для выдачи себя за жертву, или, в более общем плане, она может позволить злоумышленнику изменять содержимое страницы, которую видят жертвы.

Эта уязвимость возникает, когда вводимые пользователем данные некорректно нейтрализуются, а выходные — не кодируются. Инъекция позволяет злоумышленнику отправить вредоносную HTML-страницу жертве. Целевой браузер не может отличить легитимные части страницы от вредоносных (т.е. доверять им) и, следовательно, будет парсить и выполнять всю страницу в контексте жертвы.

Для отображения HTML-контента можно использовать широкий ассортимент методов и атрибутов. Если в этих методах обрабатываются недоверенные входные данные, существует высокий риск уязвимости HTML-инъекций. Например, можно вставить вредоносный HTML-код с помощью метода JavaScript `innerHTML`. Если строки должным образом не нейтрализуются, этот метод может допускать HTML-инъекцию. Для этой цели можно применять функцию JavaScript `document.write()`.

В следующем примере показан фрагмент уязвимого кода, который позволяет использовать недоверенные входные данные для создания динамического HTML-кода в контексте страницы:

```js
var userposition=location.href.indexOf("user=");
var user=location.href.substring(userposition+5);
document.getElementById("Welcome").innerHTML=" Hello, "+user;
```

В данном примере показан уязвимый код, использующий функцию `document.write()`:

```js
var userposition=location.href.indexOf("user=");
var user=location.href.substring(userposition+5);
document.write("<h1>Hello, " + user +"</h1>");
```

В обоих случаях эту уязвимость можно эксплуатировать с помощью таких входных данных, как:

```text
http://vulnerable.site/page.html?user=<img%20src='aaa'%20onerror=alert(1)>
```

При вводе добавляется на страницу тег изображения, который будет выполнять произвольный код JavaScript, вставленный злоумышленником в контекст HTML.

## Задача тестирования

- Найти точки инъекции HTML и оценить возможные последствия от вставленного контента.

## Как тестировать

Рассмотрим следующее [упражнение](http://www.domxss.com/domxss/01_Basics/06_jquery_old_html.html) на DOM XSS.

HTML-код содержит следующий скрипт:

```html
<script src="../js/jquery-1.7.1.js"></script>
<script>
function setMessage(){
    var t=location.hash.slice(1);
    $("div[id="+t+"]").text("The DOM is now loaded and can be manipulated.");
}
$(document).ready(setMessage  );
$(window).bind("hashchange",setMessage)
</script>
<body>
    <script src="../js/embed.js"></script>
    <span><a href="#message" > Show Here</a><div id="message">Showing Message1</div></span>
    <span><a href="#message1" > Show Here</a><div id="message1">Showing Message2</div>
    <span><a href="#message2" > Show Here</a><div id="message2">Showing Message3</div>
</body>
```

Можно вводить HTML-код.
