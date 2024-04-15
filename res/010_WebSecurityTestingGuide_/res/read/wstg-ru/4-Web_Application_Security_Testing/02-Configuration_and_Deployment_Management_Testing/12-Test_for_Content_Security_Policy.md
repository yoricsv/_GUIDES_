---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Тестирование Content Security Policy (CSP)

|ID          |
|------------|
|WSTG-CONF-12|

## Обзор

Политика защиты контента (англ.: Content Security Policy, CSP) — декларативная политика, определяющая список разрешённых источников и реализуемая с помощью заголовка ответа `Content-Security-Policy` или эквивалентного элемента `<meta>`. Она позволяет разработчикам ограничивать источники, из которых загружаются такие ресурсы, как JavaScript, CSS, изображения, файлы и т.д. CSP — эффективная технология эшелонированной защиты для снижения риска таких уязвимостей, как межсайтовый скриптинг (XSS) и перехват клика (англ.: Clickjacking).

Content Security Policy поддерживает директивы, которые позволяют детально контролировать процесс применения политик. (См. дополнительную информацию в [ссылках](#ссылки))

## Задача тестирования

- Проанализировать наличие заголовка `Content-Security-Policy` или одноимённого элемента `<meta>`, чтобы определить небезопасные конфигурации.

## Как тестировать

Чтобы протестировать наличие некорректных конфигураций в CSP, найдите их, изучая заголовки HTTP-ответа `Content-Security-Policy` или элемент `meta` в инструменте прокси:

- директива `unsafe-inline` разрешает встроенные скрипты или стили, делающие приложения уязвимыми для XSS-атак.
- директива `unsafe-eval` разрешает использовать `eval()` в приложении.
- директива `unsafe-hashes` разрешает использовать встроенные скрипты/стили при условии, что они соответствуют указанным хэшам.
- Ресурсы, например, скрипты, могут быть разрешены для загрузки из любого источника с помощью подстановочного знака (`*`).
    - Также изучите подстановки на основе неполных совпадений, например: `https://*` или `*.cdn.com`.
    - Подумайте, предоставляют ли перечисленные разрешённые источники точки входа для JSONP, которые могут быть использованы для обхода CSP или политики same-origin.
- Фреймы могут быть разрешены для всех источников с помощью подстановочного знака (`*`) для источника в директиве `frame-ancestors`
- Критически важные бизнес-приложения должны требовать использования строгой политики.

## Меры защиты

Применять строгую политику безопасности контента, которая уменьшает поверхность атаки приложения. Разработчики могут проверить работоспособность политики защиты контента с помощью онлайн-инструментов, например, [Google CSP Evaluator](https://csp-evaluator.withgoogle.com/).

### Строгая политика

Строгой (англ.: strict) называется политика, которая обеспечивает защиту от классических хранимых, отражённых и некоторых XSS-атак на основе DOM. Она является оптимальной для любой команды, пытающейся внедрить CSP.

Google пошёл дальше и создал руководство по внедрению строгой CSP на основе одноразовых случайных значений (nonce). По материалам презентации на [LocoMocoSec](https://speakerdeck.com/lweichselbaum/csp-a-successful-mess-between-hardening-and-mitigation?slide=55) для применения строгой политики можно использовать следующие два варианта:

Умеренно строгая политика:

```HTTP
script-src 'nonce-r4nd0m' 'strict-dynamic';
object-src 'none'; base-uri 'none';
```

Блокирующая строгая политика:

```HTTP
script-src 'nonce-r4nd0m';
object-src 'none'; base-uri 'none';
```

## Инструменты

- [Google CSP Evaluator](https://csp-evaluator.withgoogle.com/)
- [CSP Auditor — расширение для Burp Suite](https://portswigger.net/bappstore/35237408a06043e9945a11016fcbac18)
- [CSP Generator для Chrome](https://chrome.google.com/webstore/detail/content-security-policy-c/ahlnecfloencbkpfnpljbojmjkfgnmdc) / [для Firefox](https://addons.mozilla.org/en-US/firefox/addon/csp-generator/)

## Ссылки

- [Памятка OWASP по Content Security Policy](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html)
- [Mozilla Developer Network: Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)
- [CSP Level 3 W3C](https://www.w3.org/TR/CSP3/)
- [CSP с Google](https://csp.withgoogle.com/docs/index.html)
- [Content-Security-Policy](https://content-security-policy.com/)
- [Google CSP Evaluator](https://csp-evaluator.withgoogle.com/)
- [CSP — гремучая смесь из укрепления защиты и смягчения последствий](https://speakerdeck.com/lweichselbaum/csp-a-successful-mess-between-hardening-and-mitigation)
- [Список источников в директиве unsafe-hashes](https://content-security-policy.com/unsafe-hashes/)
- [Использование CSP для защиты web-приложений](https://webdevblog.ru/ispolzovanie-politiki-bezopasnosti-kontenta-csp-dlya-zashhity-veb-prilozhenij/)
- [Разрешено всё! Изучаем новую крутую технику обхода CSP](https://xakep.ru/2018/10/01/xss-csp-bypass/)
