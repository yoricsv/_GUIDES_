---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Тестирование передачи чувствительной информации по незашифрованным каналам

|ID          |
|------------|
|WSTG-CRYP-03|

## Обзор

Чувствительные данные должны быть защищены при их передаче по сети. Если данные передаются по протоколу HTTPS или зашифрованы другим способом, механизм защиты не должен иметь ограничений или уязвимостей, как поясняется в статье [Тестирование безопасности транспортного уровня](01-Testing_for_Weak_Transport_Layer_Security.md) и в другой документации OWASP:

- [OWASP Top 10 2017 A3-Разглашение конфиденциальной информации](https://wiki.owasp.org/?title=Special:Redirect/file/OWASP%20Top%2010-2017-ru.pdf) > [A02:2021 – Cryptographic Failures](https://owasp.org/Top10/A02_2021-Cryptographic_Failures/).
- [OWASP ASVS - V9. Передача данных](https://github.com/OWASP/ASVS/blob/master/4.0/ru/0x17-V9-Communications.md).
- [Transport Layer Protection Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Protection_Cheat_Sheet.html).

Как правило, если информация должна быть защищена при хранении, то эта информация также должна быть защищена и при передаче. Вот некоторые примеры чувствительной информации:

- Информация, используемая при аутентификации (например, учётные данные, PIN-коды, идентификаторы сессии, токены, cookie…)
- Информация, защищаемая законами, нормативными актами или политикой организации (например, банковские карты, данные клиентов)

Если приложение передаёт чувствительную информацию по незашифрованным каналам, например. через HTTP, — это считается угрозой безопасности. Злоумышленники могут завладеть учётными записями, [прослушивая сетевой трафик](https://owasp.org/www-community/attacks/Manipulator-in-the-middle_attack). Примерами являются: базовая аутентификация по протоколу HTTP, при которой учётные данные передаются в виде открытого текста; аутентификации на основе форм, передающихся по HTTP; или передача в виде открытого текста любой другой информации, которая считается конфиденциальной вследствие правил, законов, политики организации или бизнес-логики приложения.

Примеры информации, позволяющей установить личность (англ.: Personal Identifying Information, PII):

- Индивидуальные номера лицевых счетов (СНИЛС, ИНН)
- Номера банковских счетов и карт
- Паспортные данные
- Медицинские карты
- Полисы обязательного медицинского страхования
- Студенческие или военные билеты
- Номера мобильных телефонов
- Водительские удостоверения и др.

## Задачи тестирования

- Определить категории конфиденциальности информации, передаваемой по различным каналам.
- Оценить степень защищённости используемых каналов.

## Как тестировать

Различные категории информации, которые должны быть защищены, могут передаваться приложением открытым текстом. Чтобы проверить, передаётся ли эта информация по протоколу HTTP вместо HTTPS, перехватите трафик между клиентом и сервером web-приложений, которому требуются учётные данные. Для любого сообщения, содержащего конфиденциальную информацию, убедитесь, что обмен произошёл с использованием HTTPS. Узнать больше о незащищённой передаче учётных данных можно в [OWASP Top 10 A02:2021 – Cryptographic Failures](https://owasp.org/Top10/A02_2021-Cryptographic_Failures/) или [Памятке по безопасности транспортного уровня](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Protection_Cheat_Sheet.html).

### Пример 1: Базовая аутентификация через HTTP

Типичным примером является использование базовой аутентификации по протоколу HTTP. При использовании базовой аутентификации учётные данные пользователя кодируются, а не шифруются, и передаются в виде HTTP-заголовков. В приведённом ниже примере тестировщик использует [curl](https://curl.se/) для выявления этой проблемы. Обратите внимание, как приложение использует базовую аутентификацию и HTTP, а не HTTPS.

```http
$ curl -kis http://example.com/restricted/
HTTP/1.1 401 Authorization Required
Date: Fri, 01 Aug 2013 00:00:00 GMT
WWW-Authenticate: Basic realm="Restricted Area"
Accept-Ranges: bytes Vary:
Accept-Encoding Content-Length: 162
Content-Type: text/html

<html><head><title>401 Authorization Required</title></head>
<body bgcolor=white> <h1>401 Authorization Required</h1>  Invalid login credentials!  </body></html>
```

### Пример 2: Аутентификация на основе форм через HTTP

Другим типичным примером являются формы аутентификации, которые передают учётные данные пользователя по протоколу HTTP. В приведённом ниже примере можно видеть, что HTTP используется в атрибуте `action` формы. Также можно увидеть эту проблему, изучая HTTP-трафик с помощью перехватывающего прокси.

```html
<form action="http://example.com/login">
    <label for="username">User:</label> <input type="text" id="username" name="username" value=""/><br />
    <label for="password">Password:</label> <input type="password" id="password" name="password" value=""/>
    <input type="submit" value="Login"/>
</form>
```

### Пример 3: Cookie с Session ID передаётся по HTTP

Cookie, содержащий идентификатор сессии, должен передаваться по защищённым каналам. Если для cookie не установлен [атрибут Secure](../06-Session_Management_Testing/02-Testing_for_Cookies_Attributes.md), то приложению разрешено передавать его в незашифрованном виде. Обратите внимание, что cookie устанавливается без атрибута Secure, и весь процесс входа идёт по протоколу HTTP, а не HTTPS.

```http
https://secure.example.com/login

POST /login HTTP/1.1
Host: secure.example.com
[...]
Referer: https://secure.example.com/
Content-Type: application/x-www-form-urlencoded
Content-Length: 188

HTTP/1.1 302 Found
Date: Tue, 03 Dec 2013 21:18:55 GMT
Server: Apache
Set-Cookie: JSESSIONID=BD99F321233AF69593EDF52B123B5BDA; expires=Fri, 01-Jan-2014 00:00:00 GMT; path=/; domain=example.com; httponly
Location: private/
Content-Length: 0
Content-Type: text/html
```

```http
http://example.com/private

GET /private HTTP/1.1
Host: example.com
[...]
Referer: https://secure.example.com/login
Cookie: JSESSIONID=BD99F321233AF69593EDF52B123B5BDA;

HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 730
Date: Tue, 25 Dec 2013 00:00:00 GMT
```

### Пример 4: Сброс и изменение пароля или другие манипуляции с учётной записью через HTTP

Если у web-приложения есть функции, позволяющие пользователю изменять учётную запись или вызывать другой сервис с учётными данными, убедитесь, что все эти взаимодействия идут по HTTPS. Взаимодействия, подлежащие тестированию, включают:

- формы, позволяющие пользователям восстановить забытый пароль или другие учётные данные;
- формы, позволяющие пользователям редактировать учётные данные;
- формы, требующие аутентификации пользователя у третьей стороны (например, проведение платежей).

### Пример 5: Поиск чувствительной информации в исходном коде или журналах

Используйте один из следующих методов для поиска информации.

Проверьте, не зашит ли пароль или ключ шифрования в исходный код или файлы конфигурации:

`grep -r –E "Pass | password | pwd |user | guest| admin | encrypt | key | decrypt | sharekey " ./PathToSearch/`

Проверьте, могут ли журналы или исходный код содержать номер телефона, адрес электронной почты, идентификатор или другие персональные данные (ПДн). Измените регулярное выражение в соответствии с форматом ПДн.

`grep -r " {2\}[0-9]\{6\} "  ./PathToSearch/`

## Меры защиты

Используйте HTTPS на всех web-сайтах и перенаправляйте любые HTTP-запросы на HTTPS.

## Инструменты

- [curl](https://curl.se/)
- [grep](http://man7.org/linux/man-pages/man1/egrep.1.html)
- [Wireshark](https://www.wireshark.org/)
- [TCPDUMP](https://www.tcpdump.org/)

## Ссылки

- [OWASP Insecure Transport](https://owasp.org/www-community/vulnerabilities/Insecure_Transport)
- [Памятка OWASP по HTTP Strict Transport Security](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Strict_Transport_Security_Cheat_Sheet.html)
- [Let's Encrypt](https://letsencrypt.org)
