---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Ресурсы по инструментам тестирования

## Введение

В этом приложении приведён список распространённых инструментов, используемых для тестирования web-приложений. Он не претендует на то, чтобы быть полным справочником по инструментам, и включение в него инструмента не следует рассматривать как особое одобрение этого инструмента со стороны OWASP.

Список содержит только те инструменты, которые находятся в свободном доступе для скачивания и использования (хотя у них могут быть лицензии, ограничивающие их использование в коммерческих целях).

## Общее тестирование web-приложений

### Web-прокси

- [OWASP ZAP](https://www.zaproxy.org)
    - Zed Attack Proxy (ZAP) — это простой в использовании интегрированный инструмент тестирования на проникновение для поиска уязвимостей в web-приложениях. Он предназначен для использования людьми с широким спектром опыта в области безопасности и поэтому идеально подходит для разработчиков и функциональных тестировщиков, которые ещё не знакомы с тестированием на проникновение.
    - В ZAP есть автоматические сканеры, а также набор инструментов, позволяющих находить уязвимости в системе безопасности вручную.
- [Burp Suite Community Edition](https://portswigger.net/burp/communitydownload)
    - Burp Suite — перехватывающий прокси для тестирования безопасности. Он позволяет перехватывать и изменять весь трафик HTTP(S), проходящий в обоих направлениях, он может работать с пользовательскими SSL-сертификатами и клиентами, не поддерживающими прокси.
- [Telerik Fiddler](https://www.telerik.com/fiddler)
    - Fiddler — перехватывающий web-прокси, который в первую очередь предназначен для разработчиков, а не для тестировщиков на проникновение, но все же предоставляет полезную функциональность. Он также напрямую подключается к Windows HTTP API, что позволяет ему перехватывать трафик от некоторых программ, которые не позволяют устанавливать пользовательские прокси.

### Расширения Firefox

- [Firefox HTTP Header Live](https://addons.mozilla.org/en-US/firefox/addon/http-header-live)
    - Анализ HTTP-заголовков страницы во время её просмотра.
- [Firefox Multi-Account Containers](https://addons.mozilla.org/en-GB/firefox/addon/multi-account-containers/)
    - Создаёт несколько контейнеров, каждый из которых имеет свои собственные изолированные cookie и сессии. Полезно для тестирования контроля доступа между разными пользователями.
- [Firefox Tamper Data](https://addons.mozilla.org/en-US/firefox/addon/tamper-data-for-ff-quantum/)
    - Для просмотра и изменения заголовков HTTP/HTTPS и параметров сообщений.
- [Firefox Web Developer](https://addons.mozilla.org/en-US/firefox/addon/web-developer/)
    - Добавляет в браузер различные инструменты web-разработчика.

### Расширения Chrome

- [Chrome Web Developer](https://chrome.google.com/webstore/detail/bfbameneiokkgbdmiekhjnmfkcnldhhm)
    - Добавляет в браузер кнопку панели инструментов с различными инструментами web-разработчика. Это официальный порт расширения Web Developer для Chrome.
- [HTTP Request Maker](https://chrome.google.com/webstore/detail/kajfghlhfkcocafkcjlajldicbikpgnp?hl=en-US)
    - С помощью этого инструмента вы можете перехватывать запросы, вмешиваться в URL, заголовки и данные POST и, конечно, делать новые запросы.
- [Cookie Editor](https://chrome.google.com/webstore/detail/fngmhnnpilhplaeedifhccceomclgfbg?hl=en-US)
    -  Менеджер файлов cookie. Вы можете добавлять, удалять, редактировать, искать, защищать и блокировать cookie.

### Тестирование конкретных уязвимостей

#### Тестирование SQL-инъекций

- [sqlmap](http://sqlmap.org)

#### Тестирование TLS

- [OWASP O-Saft](https://owasp.org/www-project-o-saft/)
- [sslyze](https://github.com/nabla-c0d3/sslyze)
- [testssl.sh](https://github.com/drwetter/testssl.sh)
- [SSLScan](https://github.com/rbsec/sslscan)
- [SSLLabs](https://www.ssllabs.com/ssltest/)

#### Тестирование атак методом перебора

##### Взлом хэшей

- [John the Ripper](https://github.com/openwall/john)
- [hashcat](https://hashcat.net/hashcat/)

##### Удалённый перебор

- [OWASP ZAP](https://www.zaproxy.org)
- [Patator](https://github.com/lanjelot/patator)
- [THC Hydra](https://github.com/vanhauser-thc/thc-hydra)
- [Burp Suite Community Edition (Intruder)](https://portswigger.net/burp/communitydownload)

#### Фаззеры

- [Ffuf](https://github.com/ffuf/ffuf)
- [Wfuzz](https://github.com/xmendez/wfuzz)
- [Jdam](https://gitlab.com/michenriksen/jdam)

#### Дорки

- [Google Hacking database](https://www.exploit-db.com/google-hacking-database/)

#### Замедление HTTP

- [Slowloris](https://github.com/gkbrk/slowloris)
- [slowhttptest](https://github.com/shekyan/slowhttptest)

### Зеркалирование сайта

- [wget](https://www.gnu.org/software/wget/)
- [wget для windows](http://gnuwin32.sourceforge.net/packages/wget.htm)
- [curl](https://curl.haxx.se)

### Обнаружение контента

- [Gobuster](https://github.com/OJ/gobuster)

### Обнаружение портов и сервисов

- [Nmap](https://nmap.org/)

## Сканеры уязвимостей

- [OWASP ZAP](https://www.zaproxy.org)
- [Nikto](https://cirt.net/Nikto2)
- [Nuclei](https://nuclei.projectdiscovery.io/)

## Фреймворки для эксплуатации уязвимостей

- [Metasploit](https://github.com/rapid7/metasploit-framework)
- [BeEF](https://github.com/beefproject/beef/)

## Дистрибутивы Linux

- [Kali](https://www.kali.org)
- [Parrot](https://www.parrotsec.org)
- [Samurai](https://github.com/SamuraiWTF/samuraiwtf)
- [Santoku](https://sourceforge.net/projects/santoku/)
- [BlackArch](https://blackarch.org/downloads.html)

## Анализаторы исходного кода

- [Spotbugs](https://spotbugs.github.io)
- [Find Security Bugs](https://find-sec-bugs.github.io)
- [phpcs-security-audit](https://github.com/squizlabs/PHP_CodeSniffer)
- [PMD](https://pmd.github.io)
- [Microsoft's .NET Analyzers](https://docs.microsoft.com/en-us/visualstudio/code-quality/install-net-analyzers)
- [SonarQube Community Edition](https://www.sonarqube.org)

## Инструменты автоматизации браузера

Средства автоматизации браузера используются для проверки функциональности web-приложений. Некоторые придерживаются скриптового подхода и используют платформу модульного тестирования для создания наборов тестов и тестовых примеров. Большинство из них, если не все, могут быть адаптированы для проведения конкретных тестов безопасности в дополнение к функциональным тестам.

### Инструменты с открытым исходным кодом

- [HtmlUnit](http://htmlunit.sourceforge.net)
    - Фреймворк на основе Java и JUnit, который использует Apache HttpClient в качестве транспорта.
    - Очень надёжный и настраиваемый, используется в качестве движка для ряда других инструментов тестирования.
- [Selenium](https://www.selenium.dev)
    - Фреймворк для тестирования на основе JavaScript, кроссплатформенный, предоставляет графический интерфейс для создания тестов.
