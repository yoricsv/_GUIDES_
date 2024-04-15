---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Определение точек входа в приложение

|ID          |
|------------|
|WSTG-INFO-06|

## Обзор

Инвентаризация приложений и определение их поверхности атаки является ключевым предварительным этапом перед проведением более тщательного тестирования, поскольку это позволяет тестировщику определить вероятные слабые места. Цель этого раздела — помочь определить и наметить области, которые имеет смысл исследовать после инвентаризации и определения взаимосвязей приложения.

## Задача тестирования

- Определить возможные точки входа и инъекции в приложение с помощью анализа запросов и ответов.

## Как тестировать

Прежде чем приступить к тестированию необходимо получить хорошее представление о приложении, о том как с ним взаимодействуют пользователь и браузер. При анализе работы приложения, необходимо обращать внимание на все HTTP-запросы, а также на каждый параметр и поле формы, которые передаются приложению. Особое внимание уделяется вопросам, почему для передачи параметров приложению в одном случае используются запросы GET, а в другом — POST. Также необходимо обращать внимание на то, почему используются другие RESTful-методы.

Для просмотра параметров, отправленных в теле запроса, например, POST, тестировщик может использовать такой инструмент, как перехватывающий прокси. (См. [Инструменты](#инструменты)). В запросе POST тестировщик должен также обратить особое внимание на все скрытые поля формы, которые передаются приложению, поскольку они могут содержать чувствительную информацию, которая не предназначена для того, чтобы её кто-либо видел или изменял.

По опыту автора, на этом этапе было бы полезно использовать перехватывающий прокси и электронную таблицу. Прокси-сервер будет отслеживать каждый запрос тестировщика и ответ от приложения по мере его изучения. Кроме того, на этом этапе обычно перехватывается каждый запрос и ответ, чтобы точно видеть каждый заголовок, параметр и т.д., которые передаются приложению и что возвращается. Иногда это может быть довольно утомительно, особенно на больших интерактивных сайтах (например, приложение банка). Однако опыт со временем покажет, на что следует обратить внимание, и как этот этап может быть сокращён.

По мере тестирования приложения необходимо обращать внимание на интересные параметры в URL-адресе, пользовательских заголовках или тексте запросов/ответов и сохранять их в электронную таблицу. Электронная таблица должна включать запрашиваемую страницу (может быть также полезно добавить номер запроса от прокси-сервера для дальнейшего использования), интересующие нас параметры, тип запроса (GET, POST и т. д.), аутентифицирован ли доступ, используется ли TLS, является ли он частью многоэтапного процесса, используются ли WebSockets и другие уместные примечания. После того, как на схему будут нанесены все области приложения, можно пройтись с тестами по каждой из намеченных областей, и сделать заметки о том, что сработало, а что нет. В остальной части этого руководства будет рассказываться, как тестировать каждую из областей, но сначала необходимо пройти данный раздел.

Ниже приведены некоторые моменты, представляющие интерес для всех запросов и ответов. В разделе запросы сосредоточьтесь на методах GET и POST, поскольку они появляются в большинстве запросов. Обратите внимание, что можно использовать и другие методы, такие как PUT и DELETE. Часто эти более редкие запросы, если они разрешены, могут выявить уязвимости. В этом руководстве есть специальный раздел, посвященный тестированию этих HTTP-методов.

### Запросы

- Определите, где используется GET, а где POST.
- Определите все параметры, используемые в запросе POST (они указаны в теле запроса).
- В запросе POST обратите особое внимание на скрытые параметры. При отправке POST все поля формы (включая скрытые параметры) будут отправлены приложению в теле HTTP-сообщения. Если не используется перехватывающий прокси или Инструменты разработчика, они не видны. Кроме того, в зависимости от значения скрытого(ых) параметра(ов) может меняться следующая отображаемая страница, её данные и уровень доступа.
- Определите все параметры в запросе GET (например, URL-адрес), в частности строку запроса (обычно идёт после знака ?).
- Определите параметры строки запроса. Обычно они представлены в формате `ключ=значение`, например `foo=bar`. Также обратите внимание, что в одной строке запроса может быть несколько параметров, разделённых символами `&`, `\~`, `:`, и любые другие специальные и обычные символы в разных кодировках.
- Если в одной строке или в запросе POST приведено несколько параметров, отметьте, что некоторые из них или все сразу будут нужны для выполнения атак. Тестировщик должен идентифицировать все параметры (даже если они закодированы или зашифрованы) и определить, какие из них обрабатываются приложением. В последующих разделах руководства будет описано, как проверить эти параметры. На этом этапе просто убедитесь, что каждый из них идентифицирован.
- Также обратите внимание на дополнительные или пользовательские типы заголовков, которые обычно не отображаются (например, `debug: false`).

### Ответы

- Определите, где устанавливаются, изменяются или добавляются новые файлы cookie (заголовок `Set-Cookie`).
- Определите, где есть перенаправления (HTTP-коды состояния 3xx), 400-е коды состояния, в частности 403 Forbidden, и 500-е Internal server error при обычных ответах (т.е. на неизменённые запросы).
- Также обратите внимание, где используются интересные заголовки. Например, `Server: BIG-IP` указывает на то, что на сайте используется балансировка нагрузки. В этом случае, если один из серверов настроен неправильно, то, в зависимости от используемого типа балансировки, может потребоваться несколько запросов для доступа к уязвимому серверу.

### OWASP Attack Surface Detector

Инструмент Attack Surface Detector (ASD) исследует исходный код и обнаруживает конечные точки web-приложения, параметры, которые принимают на вход эти конечные точки, и типы данных для этих параметров. Сюда входят ни с чем не связанные конечные точки, которые web-паук не сможет найти, или необязательные параметры, нигде не используемые в коде на стороне клиента. Он также имеет возможность определить изменения поверхности атаки между двумя версиями приложения.

Attack Surface Detector доступен в виде плагина как для ZAP, так и для Burp Suite, а также как инструмент командной строки. Инструмент командной строки экспортирует поверхность атаки в формате JSON, который затем может использоваться другими плагинами ZAP и Burp Suite. Это полезно в тех случаях, когда исходный код не предоставляется. Например, специалист по тестированию на проникновение может получить json с поверхностью атаки от клиента, который не хочет предоставлять сам исходный код.

#### Как применяется

Инструмент командной строки в виде jar-файла доступен для загрузки с [https://github.com/secdec/attack-surface-detector-cli/releases](https://github.com/secdec/attack-surface-detector-cli/releases).

Чтобы определить конечные точки по исходному коду исследуемого web-приложения можно выполнить следующую команду ASD.

`java -jar attack-surface-detector-cli-1.3.5.jar <source-code-path> [flags]`

Ниже пример результата выполнения команды к [OWASP RailsGoat](https://github.com/OWASP/railsgoat).

```text
$ java -jar attack-surface-detector-cli-1.3.5.jar railsgoat/
Beginning endpoint detection for '<...>/railsgoat' with 1 framework types
Using framework=RAILS
[0] GET: /login (0 variants): PARAMETERS={url=name=url, paramType=QUERY_STRING, dataType=STRING}; FILE=/app/controllers/sessions_contro
ller.rb (lines '6'-'9')
[1] GET: /logout (0 variants): PARAMETERS={}; FILE=/app/controllers/sessions_controller.rb (lines '33'-'37')
[2] POST: /forgot_password (0 variants): PARAMETERS={email=name=email, paramType=QUERY_STRING, dataType=STRING}; FILE=/app/controllers/
password_resets_controller.rb (lines '29'-'38')
[3] GET: /password_resets (0 variants): PARAMETERS={token=name=token, paramType=QUERY_STRING, dataType=STRING}; FILE=/app/controllers/p
assword_resets_controller.rb (lines '19'-'27')
[4] POST: /password_resets (0 variants): PARAMETERS={password=name=password, paramType=QUERY_STRING, dataType=STRING, user=name=user, paramType=QUERY_STRING, dataType=STRING, confirm_password=name=confirm_password, paramType=QUERY_STRING, dataType=STRING}; FILE=/app/controllers/password_resets_controller.rb (lines '5'-'17')
[5] GET: /sessions/new (0 variants): PARAMETERS={url=name=url, paramType=QUERY_STRING, dataType=STRING}; FILE=/app/controllers/sessions_controller.rb (lines '6'-'9')
[6] POST: /sessions (0 variants): PARAMETERS={password=name=password, paramType=QUERY_STRING, dataType=STRING, user_id=name=user_id, paramType=SESSION, dataType=STRING, remember_me=name=remember_me, paramType=QUERY_STRING, dataType=STRING, url=name=url, paramType=QUERY_STRING, dataType=STRING, email=name=email, paramType=QUERY_STRING, dataType=STRING}; FILE=/app/controllers/sessions_controller.rb (lines '11'-'31')
[7] DELETE: /sessions/{id} (0 variants): PARAMETERS={}; FILE=/app/controllers/sessions_controller.rb (lines '33'-'37')
[8] GET: /users (0 variants): PARAMETERS={}; FILE=/app/controllers/api/v1/users_controller.rb (lines '9'-'11')
[9] GET: /users/{id} (0 variants): PARAMETERS={}; FILE=/app/controllers/api/v1/users_controller.rb (lines '13'-'15')
... snipped ...
[38] GET: /api/v1/mobile/{id} (0 variants): PARAMETERS={id=name=id, paramType=QUERY_STRING, dataType=STRING, class=name=class, paramType=QUERY_STRING, dataType=STRING}; FILE=/app/controllers/api/v1/mobile_controller.rb (lines '8'-'13')
[39] GET: / (0 variants): PARAMETERS={url=name=url, paramType=QUERY_STRING, dataType=STRING}; FILE=/app/controllers/sessions_controller.rb (lines '6'-'9')
Generated 40 distinct endpoints with 0 variants for a total of 40 endpoints
Successfully validated serialization for these endpoints
0 endpoints were missing code start line
0 endpoints were missing code end line
0 endpoints had the same code start and end line
Generated 36 distinct parameters
Generated 36 total parameters
- 36/36 have their data type
- 0/36 have a list of accepted values
- 36/36 have their parameter type
--- QUERY_STRING: 35
--- SESSION: 1
Finished endpoint detection for '<...>/railsgoat'
----------
-- DONE --
0 projects had duplicate endpoints
Generated 40 distinct endpoints
Generated 40 total endpoints
Generated 36 distinct parameters
Generated 36 total parameters
1/1 projects had endpoints generated
To enable logging include the -debug argument
```

Указав флаг `-json`, можно сгенерировать выходной файл JSON, который можно загрузить в соответствующие плагины для ZAP и для Burp Suite. Более подробная информация по ссылкам ниже.

- [ASD Plugin для OWASP ZAP](https://github.com/secdec/attack-surface-detector-zap/wiki)
- [ASD Plugin для PortSwigger Burp](https://github.com/secdec/attack-surface-detector-burp/wiki)

### Тестирование точек входа в приложение

Ниже приведены два примера для проверки точек входа в приложение.

#### Пример 1

В этом примере показан запрос GET, который позволяет приобрести товар в приложении для онлайн-покупок.

```http
GET /shoppingApp/buyme.asp?CUSTOMERID=100&ITEM=z101a&PRICE=62.50&IP=x.x.x.x HTTP/1.1
Host: x.x.x.x
Cookie: SESSIONID=Z29vZCBqb2IgcGFkYXdhIG15IHVzZXJuYW1lIGlzIGZvbyBhbmQgcGFzc3dvcmQgaXMgYmFy
```

> Все параметры запроса, например, CUSTOMERID, ITEM, PRICE, IP, и Cookie могут быть закодированными или использоваться для контроля состояния сессии.

#### Пример 2

В этом примере показан запрос POST, который позволит вам войти в приложение.

```http
POST /example/authenticate.asp?service=login HTTP/1.1
Host: x.x.x.x
Cookie: SESSIONID=dGhpcyBpcyBhIGJhZCBhcHAgdGhhdCBzZXRzIHByZWRpY3RhYmxlIGNvb2tpZXMgYW5kIG1pbmUgaXMgMTIzNA==;CustomCookie=00my00trusted00ip00is00x.x.x.x00

user=admin&pass=pass123&debug=true&fromtrustIP=true
```

Можно заметить, что параметры отправляются в нескольких местах:

1. В строке запроса: `service`
2. В заголовке Cookie: `SESSIONID`, `CustomCookie`
3. В теле запроса: `user`, `pass`, `debug`, `fromtrustIP`

Наличие нескольких мест для инъекции даёт нарушителю возможность создания цепочек, которые могут повысить шансы найти дефект в коде обработки.

## Инструменты

- [OWASP Zed Attack Proxy (ZAP)](https://www.zaproxy.org/)
- [Burp Suite](https://www.portswigger.net/burp/)
- [Fiddler](https://www.telerik.com/fiddler)

## Ссылки

- [RFC 2616 – Hypertext Transfer Protocol – HTTP 1.1](https://tools.ietf.org/html/rfc2616)
- [OWASP Attack Surface Detector](https://owasp.org/www-project-attack-surface-detector/)
