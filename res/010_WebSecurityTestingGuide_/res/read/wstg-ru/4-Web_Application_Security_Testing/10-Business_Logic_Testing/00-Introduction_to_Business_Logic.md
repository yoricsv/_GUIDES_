---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Введение в бизнес-логику

Тестирование на предмет нарушений в бизнес-логике в многофункциональном динамичном web-приложении требует нестандартных подходов. Предположим, что для аутентификации пользователя в приложении он должен выполнить шаги 1, 2, 3, именно в этой последовательности. Что произойдёт, если пользователь перейдет от шага 1 сразу к шагу 3? В этом упрощённом примере приложение должно дать доступ, отказать или просто выдать 500-ю ошибку?

Можно привести множество подобных примеров, усвоив один неизменный урок — надо нестандартно мыслить. Этот вид уязвимостей не может быть обнаружен сканерами и зависит от навыков и креативности пентестера. Кроме того, обычно он является одним из самых сложных для обнаружения и, как правило, зависит от специфики приложения, но в то же время обычно он является одним из самых опасных при эксплуатации.

Классификация нарушений бизнес-логики изучена недостаточно; хотя эксплуатация таких уязвимостей часто происходит в реальных системах, и многие исследователи безопасности приложений изучают их. Наибольшее внимание уделяется web-приложениям. В сообществе ведутся споры о том, являются ли эти вопросы новыми или вариациями уже известных.

Тестирование нарушений бизнес-логики похоже на тесты, проводимые функциональными тестировщиками, которые тестируют логику или строят диаграммы состояний конечного автомата. Эти виды тестов требуют, чтобы специалисты по безопасности думали немного иначе, включали примеры злоупотреблений и неправильного использования, а также методы тестирования, применяющиеся функциональными тестировщиками. Автоматизация примеров злоупотребления бизнес-логикой пока невозможна и остаётся искусством, зависящим от опыта и навыков тестировщика и его знаний комплексного бизнес-процесса.

## Запреты и ограничения

Рассмотрим правила для бизнес-функций, предоставляемых приложением. Существуют ли какие-либо ограничения или запреты на поведение людей? Затем подумайте, контролирует ли приложение соблюдение этих правил. Обычно, придумать тестовые примеры для анализа приложения довольно легко, если вы знакомы с бизнес-процессом. Если вы пришли извне, придётся включать здравый смысл и спрашивать бизнес, должны ли приложения разрешать те или иные операции.

Иногда, в сложных приложениях, у тестировщика изначально не будет полного представления о каждом аспекте приложения. В таких ситуациях лучше всего, чтобы тестировщика с приложением познакомил клиент, чтобы  ещё до начала тестирования понять ограничения и предполагаемую функциональность. Кроме того, помогает прямой контакт с разработчиками (если это возможно) во время тестирования, если возникнут какие-либо вопросы относительно функциональности.

## Проблемы с тестированием логики

Автоматизированным инструментам трудно оценить контекст, поэтому такие тесты проводят вручную. Следующие два примера иллюстрируют, как понимание функциональности приложения, намерений разработчика и нестандартное мышление могут нарушить логику приложения. Первый пример начинается с упрощённой манипуляции с параметрами, второй представляет собой реальный пример многоступенчатого процесса, а третий полностью нарушает логику приложения.

**Пример 1**:

Предположим, сайт электронной коммерции позволяет пользователям выбирать товары для покупки, просматривать сводную страницу, а затем закрывать сделку. Что, если злоумышленник смог бы вернуться на сводную страницу, поддерживая сессию активной, ввести более низкую цену за штуку и завершить транзакцию, а затем рассчитаться?

**Пример 2**:

Блокирование ресурсов и запрет на покупку таких товаров другими пользователями в Интернете может привести к тому, что злоумышленники приобретут товары по более низкой цене. Меры противодействия для решения этой проблемы заключаются во введении тайм-аутов и механизмов, гарантирующих, что может быть назначена только корректная цена.

**Пример 3**:

Что, если бы пользователь мог начать транзакцию, связанную со своей учётной записью программы лояльности, а после того, как баллы за это добавятся к его учётной записи, отменил транзакцию? Будут ли баллы по-прежнему применяться к его учётной записи?

## Инструменты

Хотя и существуют инструменты для тестирования и проверки правильности работы бизнес-процессов в допустимых ситуациях, эти инструменты неспособны обнаруживать логические уязвимости. Например, инструменты не имеют средств для определения того, способен ли пользователь обойти логику бизнес-процесса путём редактирования параметров, прогнозирования наименований ресурсов или эскалации привилегий для доступа к ограниченным ресурсам, и нет механизма, который помог бы тестировщикам-людям догадаться о существовании таких ситуаций.

Ниже приведены некоторые распространённые типы инструментов, которые могут быть полезны для выявления проблем с бизнес-логикой.

При установке дополнений вы всегда должны тщательно анализировать запрашиваемые ими разрешения и ваши привычки при использовании браузера.

### Перехватывающие прокси

Для наблюдения за блоками запросов и ответов HTTP-трафика

- [OWASP Zed Attack Proxy](https://www.zaproxy.org)
- [Burp Proxy](https://portswigger.net/burp)

### Дополнения для web-браузера

Для просмотра и изменения заголовков HTTP/HTTPS, параметров сообщений и наблюдения за DOM браузера

- [Tamper Data для FF Quantum](https://addons.mozilla.org/en-US/firefox/addon/tamper-data-for-ff-quantum)
- [Tamper Chrome (для Google Chrome)](https://chrome.google.com/webstore/detail/tamper-chrome-extension/hifhgpdkfodlpnlmlnmhchnkepplebkb)

## Разные инструменты тестирования

- [Панель инструментов Web Developer](https://chrome.google.com/webstore/detail/bfbameneiokkgbdmiekhjnmfkcnldhhm)
    - Расширение Web Developer добавляет в браузер кнопку панели инструментов с различными инструментами web-разработчика. Это официальный порт расширения Web Developer для Firefox.
- [HTTP Request Maker для Chrome](https://chrome.google.com/webstore/detail/kajfghlhfkcocafkcjlajldicbikpgnp)
- [HTTP Request Maker для Firefox](https://addons.mozilla.org/en-US/firefox/addon/http-request-maker)
    - Request Maker — инструмент для тестирования на проникновение. С его помощью вы можете легко перехватывать запросы, сделанные web-страницами, менять URL, заголовки и данные в POST и, конечно же, делать новые запросы.
- [Cookie Editor для Chrome](https://chrome.google.com/webstore/detail/fngmhnnpilhplaeedifhccceomclgfbg)
- [Cookie Editor для Firefox](https://addons.mozilla.org/en-US/firefox/addon/cookie-editor)
    - Cookie Editor — менеджер cookie. Вы можете добавлять, удалять, редактировать, искать, защищать и блокировать cookie.

## Ссылки

### Технические руководства

- [The Common Misuse Scoring System (CMSS): Metrics for Software Feature Misuse Vulnerabilities - NISTIR 7864](https://csrc.nist.gov/publications/detail/nistir/7864/final)
- [Finite State testing of Graphical User Interfaces, Fevzi Belli](https://pdfs.semanticscholar.org/b57c/6c8022abfd2cb17ec785d3622027b3edfaaf.pdf)
- [Principles and Methods of Testing Finite State Machines - A Survey, David Lee, Mihalis Yannakakis](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.380.3405&rep=rep1&type=pdf)
- [Security Issues in Online Games, Jianxin Jeff Yan and Hyun-Jin Choi](https://www.researchgate.net/publication/220677013_Security_issues_in_online_games)
- [Securing Virtual Worlds Against Real Attack, Dr. Igor Muttik, McAfee](https://www.infopoint-security.de/open_downloads/2008/McAfee_wp_online_gaming_0808.pdf)
- [Seven Business Logic Flaws That Put Your Website At Risk – Jeremiah Grossman Founder and CTO, WhiteHat Security](https://www.slideshare.net/jeremiahgrossman/seven-business-logic-flaws-that-put-your-website-at-risk-harvard-07062008)
- [Toward Automated Detection of Logic Vulnerabilities in Web Applications - Viktoria Felmetsger Ludovico Cavedon Christopher Kruegel Giovanni Vigna](https://www.usenix.org/legacy/event/sec10/tech/full_papers/Felmetsger.pdf)

### От OWASP

- [How to Prevent Business Flaws Vulnerabilities in Web Applications, Marco Morana](https://owasp.org/www-pdf-archive/OWASP_Cincinnati_Jan_2011.pdf)

### Полезные web-сайты

- [Abuse of Functionality](http://projects.webappsec.org/w/page/13246913/Abuse-of-Functionality)
- [Business logic](https://en.wikipedia.org/wiki/Business_logic)
- [Business Logic Flaws and Yahoo Games](http://jeremiahgrossman.blogspot.com/2006/12/business-logic-flaws.html)
- [CWE-840: Business Logic Errors](https://cwe.mitre.org/data/definitions/840.html)
- [Defying Logic: Theory, Design, and Implementation of Complex Systems for Testing Application Logic](https://pdfs.semanticscholar.org/d14a/18f08f6488f903f2f691a1d159e95d8ee04f.pdf)
- [Software Testing Lifecycle](http://softwaretestingfundamentals.com/software-testing-life-cycle/)

### Книга

- [The Decision Model: A Business Logic Framework Linking Business and Technology, By Barbara Von Halle, Larry Goldberg, Published by CRC Press, ISBN1420082817 (2010)](https://isbnsearch.org/isbn/1420082817)
