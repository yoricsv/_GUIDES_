---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Тестирование загрузки файлов непредусмотренных типов

|ID          |
|------------|
|WSTG-BUSL-08|

## Обзор

Бизнес-процессы многих приложений позволяют загружать и обрабатывать данные, получая их через файлы. Но бизнес-процесс должен контролировать их и разрешать только определённые «разрешённые» типы файлов. Решение о том, какие файлы «разрешены», определяется бизнес-логикой и зависит от приложения/системы. Риск заключается в том, что, если разрешено загружать файлы, то злоумышленники могут отправить файл непредусмотренного типа, который может быть выполнен и негативно повлиять на приложение или систему посредством атак, которые могут исказить (англ.: deface) web-сайт, выполнять удалённые команды, просматривать системные файлы или локальные ресурсы, атаковать другие серверы или использовать локальные уязвимости, и это ещё не всё.

Уязвимости, связанные с загрузкой непредусмотренных типов файлов, уникальны тем, что если расширение неправильное, загрузка должна сразу отклоняться. Кроме того, это отличается от загрузки вредоносных файлов тем, что в большинстве случаев неверный формат файла может сам по себе не быть «вредоносным», но может нанести ущерб хранимым данным. Например, если приложение принимает файлы MS Excel, то когда загружается аналогичный файл базы данных, он может быть прочитан, но извлечённые данные могут быть перемещены не туда, куда планировалось.

Приложение может ожидать, что для обработки будут загружены только определённые типы файлов, например, `.csv` или `.txt`. Приложение может не проверять загруженный файл по расширению (с низкой степенью достоверности) или по содержимому (с более высокой степенью достоверности). Это может привести к неожиданным результатам работы системы или базы данных в приложении/системе или дать злоумышленникам дополнительные методы для эксплуатации приложения/системы.

### Пример

Предположим, приложение для обмена изображениями позволяет пользователям загружать на web-сайт графические файлы `.gif` или `.jpg`. Что, если злоумышленник сможет загрузить туда HTML с тегом `<script>` или файл PHP? Система может переместить файл из временного местоположения в конечное, где код PHP теперь можно выполнить для приложения или системы.

## Задачи тестирования

- Проанализировать проектную документацию на наличие типов файлов, которые отклоняются системой.
- Убедиться, что нежелательные типы файлов отклоняются и обрабатываются безопасно.
- Убедиться, что пакетная загрузка файлов безопасна и не допускает обхода установленных мер защиты.

## Как тестировать

### Конкретный метод тестирования

- Изучите требования логики приложения.
- Подготовьте библиотеку файлов, которые «не разрешены» для загрузки, могут содержать такие файлы, как: jsp, exe или HTML, содержащие скрипты.
- В приложении перейдите к механизму отправки или выгрузки файлов.
- Загрузите «неразрешённый» файл и убедитесь, что это действительно запрещено.
- Проверьте, проверяет ли web-сайт тип файла только в клиентском JavaScript.
- Убедитесь, что web-сайт проверяет тип файла только по Content-Type в HTTP-запросе.
- Проверьте, контролирует ли web-сайт только расширение файла.
- Проверьте, можно ли получить доступ к другим загруженным файлам прямо по указанному URL.
- Проверьте, может ли загруженный файл включать код или инъекцию скрипта.
- Проверьте, есть ли какая-либо проверка пути к файлу для загруженных файлов. В частности, хакеры могут сжимать файлы с указанным путём в ZIP, чтобы распакованные файлы можно было загрузить по заданному пути после загрузки и распаковки.

## Связанные сценарии тестирования

- [Тестирование обработки расширений файлов на наличие чувствительной информации](../02-Configuration_and_Deployment_Management_Testing/03-Test_File_Extensions_Handling_for_Sensitive_Information.md)
- [Тестирование загрузки вредоносных файлов](09-Test_Upload_of_Malicious_Files.md)

## Меры защиты

Приложения должны разрабатываться с механизмами, позволяющими принимать и манипулировать только предусмотренными файлами, которые остальная функциональность приложения готова обрабатывать и ожидает. Примеры включают в себя: списки запрещённых или разрешённых расширений файлов, использование Content-Type из заголовка или использование определителя типов файлов, - всё для того, чтобы разрешить доступ в систему только допустимым типам файлов.

## Ссылки

- [OWASP - Unrestricted File Upload](https://owasp.org/www-community/vulnerabilities/Unrestricted_File_Upload)
- [File upload security best practices: Block a malicious file upload](https://www.computerweekly.com/answer/File-upload-security-best-practices-Block-a-malicious-file-upload)
- [Stop people uploading malicious PHP files via forms](https://stackoverflow.com/questions/602539/stop-people-uploading-malicious-php-files-via-forms)
- [CWE-434: Unrestricted Upload of File with Dangerous Type](https://cwe.mitre.org/data/definitions/434.html)