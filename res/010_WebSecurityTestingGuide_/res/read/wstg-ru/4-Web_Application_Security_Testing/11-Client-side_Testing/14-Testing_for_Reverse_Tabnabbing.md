---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Тестирование Reverse Tabnabbing

|ID          |
|------------|
|WSTG-CLNT-14|

## Обзор

[Обратный редирект на захваченную вкладку (англ.: Reverse Tabnabbing)](https://owasp.org/www-community/attacks/Reverse_Tabnabbing) — это атака, которая может использоваться для перенаправления пользователей на фишинговые страницы. Обычно это становится возможным из-за того, что атрибут `target` у тега `<a>` установлен в значение `_blank`, что приводит к открытию ссылки в новой вкладке. Если в том же теге `<a>` нет атрибута `rel='noopener noreferrer'`, то открываемая страница может повлиять на исходную и перенаправить её на домен, контролируемый злоумышленником.

Поскольку при открытии новой вкладки пользователь находился в исходном домене, он с меньшей вероятностью заметит, что страница изменилась, особенно, если фишинговая страница похожа на страницу в исходном домене. Таким образом, учётные данные, введённые жертвой в домене, контролируемом злоумышленником, окажутся в его владении.

Ссылки, открываемые с помощью функции JavaScript `window.open`, также уязвимы для этой атаки.

_ПРИМЕЧАНИЕ. Это устаревшая проблема, которая не влияет на [современные браузеры](https://caniuse.com/mdn-html_elements_a_implicit_noopener). Этой атаке подвержены старые версии популярных браузеров (например, версии Google Chrome до 88), а также Internet Explorer._

### Пример

Представьте себе web-приложение, в котором пользователям разрешено вставлять URL в свой профиль. Если приложение уязвимо к Reverse tabnabbing, злоумышленник сможет дать ссылку на страницу со следующим кодом:

```html
<html>
 <body>
  <script>
    window.opener.location = "https://example.org";
  </script>
<b>Ошибка загрузки...</b>
 </body>
</html>
```

При переходе по ссылке откроется новая вкладка, а исходная будет перенаправлена на "example.org". Предположим, что "example.org" выглядит похоже на уязвимое web-приложение, тогда пользователь с меньшей вероятностью заметит подмену и с большей вероятностью введёт чувствительную информацию на странице.

## Как тестировать

- Проверьте HTML-код приложения, чтобы узнать, используются ли в ссылках с `target="_blank"` в атрибуте `rel` ключевые слова `noopener` и `noreferrer`. Если нет, вполне вероятно, что приложение уязвимо для Reverse tabnabbing. Такая ссылка становится пригодной для эксплуатации, если она либо указывает на сторонний сайт, скомпрометированный злоумышленником, либо находится под контролем пользователя.
- Проверьте те области, куда злоумышленник может вставлять ссылки, т.е. контролировать аргумент `href` тега `<a>`. Попробуйте вставить ссылку на страницу с исходным кодом в приведённом выше примере, и посмотрите, есть ли перенаправление с исходного домена. Этот тест можно провести в IE, если не получится в других браузерах.

## Меры защиты

Убедиться, что для всех ссылок HTML-атрибут `rel` применяется с ключевыми словами `noreferrer` и `noopener`.

## Ссылки

- [Tabnabbing - Памятка по HTML5](https://cheatsheetseries.owasp.org/cheatsheets/HTML5_Security_Cheat_Sheet.html#tabnabbing)
- [Уязвимость на примере target="_blank"](https://dev.to/ben/the-targetblank-vulnerability-by-example)
- [О rel=noopener](https://mathiasbynens.github.io/rel-noopener/)
- [Target=”_blank” — самая недооцененная уязвимость](https://medium.com/@jitbit/target-blank-the-most-underestimated-vulnerability-ever-96e328301f4c)
- [Уязвимость Reverse tabnabbing затрагивает IBM Business Automation Workflow и IBM Business Process Manager](https://www.ibm.com/support/pages/security-bulletin-reverse-tabnabbing-vulnerability-affects-ibm-business-automation-workflow-and-ibm-business-process-manager-bpm-cve-2020-4490-0)
- [Опасный target="_blank"](https://habr.com/ru/post/282880/)