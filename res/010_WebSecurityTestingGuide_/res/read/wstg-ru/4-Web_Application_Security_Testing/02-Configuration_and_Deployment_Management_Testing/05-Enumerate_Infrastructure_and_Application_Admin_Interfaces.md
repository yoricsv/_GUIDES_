---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Инвентаризация интерфейсов администрирования для инфраструктуры и приложений

|ID          |
|------------|
|WSTG-CONF-05|

## Обзор

Интерфейсы администратора могут присутствовать в приложении или на сервере приложений, чтобы дать возможность определённым пользователям выполнять привилегированные действия на сайте. Необходимо провести тесты, чтобы выяснить, может ли эта привилегированная функциональность быть доступна неавторизованному или обычному пользователю, и если да, то каким образом.

Приложению может потребоваться интерфейс администратора, чтобы дать привилегированному пользователю доступ к функциям, которые могут вносить изменения в работу сайта. Такие изменения могут включать:

- работу с учётными записями пользователей
- дизайн и вёрстка сайта
- манипулирование данными
- изменения конфигурации.

Во многих случаях такие интерфейсы не имеют достаточных мер защиты от несанкционированного доступа. Тестирование направлено на обнаружение этих интерфейсов администратора и доступ к функциям, предназначенным для привилегированных пользователей.

## Задача тестирования

- Найти скрытые интерфейсы администратора и определить их функциональные возможности.

## Как тестировать

### Тестирование методом «чёрного ящика»

В следующем разделе описаны векторы, которые можно использовать для проверки наличия административных интерфейсов. Эти методы также можно использовать для проверки связанных проблем, включая повышение привилегий, и они более подробно описаны в других разделах данного руководства (например, [Тестирование обхода схемы авторизации](../05-Authorization_Testing/02-Testing_for_Bypassing_Authorization_Schema.md) и [Тестирование небезопасных прямых ссылок на объекты](../05-Authorization_Testing/04-Testing_for_Insecure_Direct_Object_References.md).

- Инвентаризация каталогов и файлов. Административный интерфейс может присутствовать, но быть невидимым для тестировщика. Попытка угадать путь к административному интерфейсу может оказаться не сложнее запроса */admin* или */administrator* и т.д. или в некоторых сценариях он может быть обнаружен в течение нескольких секунд с помощью [Google dorks](https://www.exploit-db.com/google-hacking-database).
- Существует множество инструментов для перебора содержимого сервера, см. раздел Инструменты ниже для дополнительной информации. Тестировщику, возможно, придётся также указать имя файла страницы администрирования. Принудительный переход на указанную страницу может обеспечить доступ к интерфейсу.
- Комментарии и ссылки в исходном коде. Многие сайты используют общий код, который загружается для всех пользователей сайта. При изучении исходного кода, отправляемого клиенту, можно обнаружить ссылки на функции администратора, и их стоит исследовать.
- Просмотр документации по серверу и приложению. Если сервер приложений или приложение развёрнуты в конфигурации по умолчанию, может оказаться возможным получить доступ к интерфейсу администрирования, используя информацию, описанную в конфигурации или справочной документации. Если найден административный интерфейс и требуются учётные данные, следует обратиться к спискам паролей по умолчанию.
- Общедоступная информация. Многие приложения, такие как WordPress, имеют административные интерфейсы по умолчанию.
- Альтернативный порт сервера. Интерфейсы администрирования могут отображаться на другом порту хоста, отличном от основного приложения. Например, интерфейс администрирования Apache Tomcat часто можно увидеть на порту 8080.
- Подмена параметров. Для включения функций администратора может понадобиться параметр GET или POST или переменная в cookie. На это указывает наличие скрытых полей, например так:

```html
<input type="hidden" name="admin" value="no">
```

или в cookie:

`Cookie: session_cookie; useradmin=0`

После обнаружения административного интерфейса можно использовать комбинацию вышеуказанных методов для попытки обойти аутентификацию. Если это не удаётся, тестировщик может попытаться провести атаку методом перебора. В таком случае он должен знать о возможности блокировки административной учётной записи, если такая функциональность присутствует.

### Тестирование методом «серого ящика»

Следует провести более детальное изучение компонентов сервера и приложения, чтобы укрепить защиту (например, страницы администратора не должны быть доступны для всех за счёт фильтрации по IP-адресам или других мер защиты), и, где применимо, убедиться в том, что компоненты не используют учётные данные или конфигурации по умолчанию.

Следует проанализировать исходный код, чтобы убедиться, что модель авторизации и аутентификации обеспечивает чёткое разделение обязанностей между обычными пользователями и администраторами сайта. Необходимо проанализировать функции пользовательского интерфейса, совместно используемые обычными пользователями и администраторами, чтобы обеспечить чёткое разделение между отображением компонентов и утечкой информации из-за совместного использования общей функциональности.

У каждого web-фрейворка свои страницы администрирования и путь к ним по умолчанию. Например:

WebSphere:

```html
/admin
/admin-authz.xml
/admin.conf
/admin.passwd
/admin/*
/admin/logon.jsp
/admin/secure/logon.jsp
```

PHP:

```html
/phpinfo
/phpmyadmin/
/phpMyAdmin/
/mysqladmin/
/MySQLadmin
/MySQLAdmin
/login.php
/logon.php
/xmlrpc.php
/dbadmin
```

FrontPage:

```html
/admin.dll
/admin.exe
/administrators.pwd
/author.dll
/author.exe
/author.log
/authors.pwd
/cgi-bin
```

WebLogic:

```html
/AdminCaptureRootCA
/AdminClients
/AdminConnections
/AdminEvents
/AdminJDBC
/AdminLicense
/AdminMain
/AdminProps
/AdminRealm
/AdminThreads
```

WordPress:

```html
wp-admin/
wp-admin/about.php
wp-admin/admin-ajax.php
wp-admin/admin-db.php
wp-admin/admin-footer.php
wp-admin/admin-functions.php
wp-admin/admin-header.php
```

## Инструменты

- [OWASP ZAP - Forced Browse](https://www.zaproxy.org/docs/desktop/addons/forced-browse/) в настоящее время поддерживается использование предыдущего проекта OWASP DirBuster.
- [THC-HYDRA](https://github.com/vanhauser-thc/thc-hydra) — инструмент, который позволяет выполнять перебор многих интерфейсов, включая HTTP-аутентификацию в формах.
- Брутфорсер работает намного лучше, если использует хороший словарь, например словарь [netsparker](https://www.netsparker.com/blog/web-security/svn-digger-better-lists-for-forced-browsing/).

## Ссылки

- [CIRT: Список паролей по умолчанию](https://cirt.net/passwords)
- [Для перебора путей к странице входа администратора можно использовать FuzzDB](https://github.com/fuzzdb-project/fuzzdb/blob/master/discovery/predictable-filepaths/login-file-locations/Logins.txt)
- [Распространённые параметры для включения функций администрирования или отладки](https://github.com/fuzzdb-project/fuzzdb/blob/master/attack/business-logic/CommonDebugParamNames.txt)