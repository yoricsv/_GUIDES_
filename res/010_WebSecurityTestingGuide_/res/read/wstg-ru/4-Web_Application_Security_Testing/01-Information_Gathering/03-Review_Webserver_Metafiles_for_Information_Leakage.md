---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Анализ метафайлов web-сервера на предмет утечки информации

|ID          |
|------------|
|WSTG-INFO-03|

## Обзор

В этом разделе описывается, как тестировать различные файлы метаданных на утечку информации о путях или функциях web-приложения. Кроме того, может быть создан перечень каталогов, которые следует избегать паукам, роботам или сканерам, в зависимости от [Схемы путей выполнения приложения](07-Map_Execution_Paths_Through_Application.md). Также может быть собрана другая информация для определения поверхности атаки, сведений о технологиях или для использования в социальной инженерии.

## Задачи тестирования

- Выявить скрытые или неочевидные пути и функциональные возможности приложения с помощью анализа файлов метаданных.
- Извлечь и отобразить на схеме эту и другую информацию, которая может привести к лучшему пониманию исследуемых систем.

## Как тестировать

> Любое из действий, выполняемых ниже с помощью `wget` также может быть выполнено с помощью `curl`. Многие инструменты динамического тестирования безопасности приложений (DAST), такие как ZAP или Burp Suite, включают анализ метафайлов в состав их функциональности spider / crawler. Они также могут определяться с помощью различных [Google Dorks](https://en.wikipedia.org/wiki/Google_hacking) или используя операторы поиска, такие как `inurl:`.

### Robots

Web-пауки, поисковые роботы или сканеры извлекают web-страницу, а затем рекурсивно обходят её гиперссылки для извлечения дополнительного контента. Их поведение определяется [Robots Exclusion Protocol](https://www.robotstxt.org) в файле [robots.txt](https://www.robotstxt.org/) из каталога webroot.

В качестве примера можно привести начало файла `robots.txt` от [Google](https://www.google.com/robots.txt), который 5 мая 2020 г. выглядел так:

```text
User-agent: *
Disallow: /search
Allow: /search/about
Allow: /search/static
Allow: /search/howsearchworks
Disallow: /sdch
...
```

Директива [User-Agent](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent) относится к конкретному пауку/роботу/сканеру. Например, `User-Agent: Googlebot` относится к пауку из Google, а `User-Agent: bingbot` относится к сканеру от Microsoft. `User-Agent: *` в приведенном выше примере относится ко всем [паукам/роботам/сканерам](https://support.google.com/webmasters/answer/6062608?visit_id=637173940975499736-3548411022&rd=1).

Директива `Disallow` указывает, какие ресурсы запрещено посещать паукам/роботам/сканерам. В приведенном выше примере запрещены:

```text
...
Disallow: /search
...
Disallow: /sdch
...
```

Web-пауки/роботы/сканеры могут [намеренно игнорировать](https://blog.isc2.org/isc2_blog/2008/07/the-attack-of-t.html) директивы `Disallow` указанные в файле `robots.txt`. Поэтому не стоит рассматривать `robots.txt` как механизм для ограничений на доступ, хранение или публикацию web-контента третьими лицами.

Файл `robots.txt` извлекается из корневого web-каталога web-сервера. Например, чтобы взять файл `robots.txt` с `www.google.com` с помощью `wget` или `curl`:

```bash
$ curl -O -Ss http://www.google.com/robots.txt && head -n5 robots.txt
User-agent: *
Disallow: /search
Allow: /search/about
Allow: /search/static
Allow: /search/howsearchworks
...
```

#### Анализ robots.txt с помощью инструментов Google для web-мастеров

Владельцы web-сайтов могут использовать функцию «Анализ robots.txt» для анализа сайта в составе [Google Webmaster Tools](https://www.google.com/webmasters/tools). Этот инструмент может помочь в тестировании, и процедура выглядит следующим образом:

1. Войдите в Инструменты Google для web-мастеров с помощью учетной записи Google.
2. На панели инструментов введите URL-адрес анализируемого сайта.
3. Выберите один из имеющихся методов и следуйте инструкциям на экране.

### Теги META

Теги `<META>` размещаются в разделе `HEAD` каждого HTML-документа и должны быть одинаковыми на всём web-сайте, на тот случай, если начальной точкой робота/паука/сканера будет ссылка на документ вне каталога webroot, т.е. c [внешней ссылки](https://en.wikipedia.org/wiki/Deep_linking). Директива robots также может быть указана с помощью [META тега](https://www.robotstxt.org/meta.html).

#### META-тег ROBOTS

Если тег со значением `<META NAME="ROBOTS" ... >` отсутствует, то "Robots Exclusion Protocol" использует значение по умолчанию `INDEX,FOLLOW`. Таким образом, две другие альтернативы начинаются с `NO...` т.е. `NOINDEX` и `NOFOLLOW`.

На основе директив Disallow, перечисленных в файле robots.txt в каталоге webroot, выполняется поиск по регулярному выражению `<META NAME="ROBOTS"` на каждой web-странице, и результат сравнивается с файлом `robots.txt` в webroot.

#### Информационные META-теги

Организации часто встраивают информационные МЕТА-теги в web-контент для поддержки различных технологий, таких как программы чтения с экрана, предварительный просмотр в социальных сетях, индексация в поисковых системах и т.д. Такая метаинформация может быть полезна для тестировщиков при определении используемых технологий и дополнительных путей / функций для изучения и тестирования. Например, в исходном коде страницы `www.whitehouse.gov` по состоянию на 5 мая 2020 г. присутствовала следующая метаинформация:

```html
...
<meta property="og:locale" content="en_US" />
<meta property="og:type" content="website" />
<meta property="og:title" content="The White House" />
<meta property="og:description" content="We, the citizens of America, are now joined in a great national effort to rebuild our country and to restore its promise for all. – President Donald Trump." />
<meta property="og:url" content="https://www.whitehouse.gov/" />
<meta property="og:site_name" content="The White House" />
<meta property="fb:app_id" content="1790466490985150" />
<meta property="og:image" content="https://www.whitehouse.gov/wp-content/uploads/2017/12/wh.gov-share-img_03-1024x538.png" />
<meta property="og:image:secure_url" content="https://www.whitehouse.gov/wp-content/uploads/2017/12/wh.gov-share-img_03-1024x538.png" />
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:description" content="We, the citizens of America, are now joined in a great national effort to rebuild our country and to restore its promise for all. – President Donald Trump." />
<meta name="twitter:title" content="The White House" />
<meta name="twitter:site" content="@whitehouse" />
<meta name="twitter:image" content="https://www.whitehouse.gov/wp-content/uploads/2017/12/wh.gov-share-img_03-1024x538.png" />
<meta name="twitter:creator" content="@whitehouse" />
...
<meta name="apple-mobile-web-app-title" content="The White House">
<meta name="application-name" content="The White House">
<meta name="msapplication-TileColor" content="#0c2644">
<meta name="theme-color" content="#f5f5f5">
...
```

### Карта сайта

Карта сайта — это файл, в котором разработчик может предоставить информацию о страницах, видео и других файлах, предлагаемых сайтом или приложением, а также о взаимосвязях между ними. Поисковые системы могут использовать этот файл для более тщательного изучения вашего сайта. Тестировщики могут использовать файл `sitemap.xml`, чтобы изучить сайт или приложение более полно.

Следующий отрывок взят из основной карты сайта Google, полученной 5 мая 2020 года.

```bash
$ wget --no-verbose https://www.google.com/sitemap.xml && head -n8 sitemap.xml
2020-05-05 12:23:30 URL:https://www.google.com/sitemap.xml [2049] -> "sitemap.xml" [1]

<?xml version="1.0" encoding="UTF-8"?>
<sitemapindex xmlns="http://www.google.com/schemas/sitemap/0.84">
  <sitemap>
    <loc>https://www.google.com/gmail/sitemap.xml</loc>
  </sitemap>
  <sitemap>
    <loc>https://www.google.com/forms/sitemaps.xml</loc>
  </sitemap>
...
```

Далее тестировщик может захотеть исследовать карту сайта gmail `https://www.google.com/gmail/sitemap.xml`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9" xmlns:xhtml="http://www.w3.org/1999/xhtml">
  <url>
    <loc>https://www.google.com/intl/am/gmail/about/</loc>
    <xhtml:link href="https://www.google.com/gmail/about/" hreflang="x-default" rel="alternate"/>
    <xhtml:link href="https://www.google.com/intl/el/gmail/about/" hreflang="el" rel="alternate"/>
    <xhtml:link href="https://www.google.com/intl/it/gmail/about/" hreflang="it" rel="alternate"/>
    <xhtml:link href="https://www.google.com/intl/ar/gmail/about/" hreflang="ar" rel="alternate"/>
...
```

### Security TXT

[security.txt](https://securitytxt.org) был ратифицирован IETF как [RFC 9116 - Формат файла для помощи в раскрытии уязвимостей в системе безопасности](https://www.rfc-editor.org/rfc/rfc9116.html), давая возможность web-сайтам указывать политику безопасности и контактные данные. Существует множество причин, по которым это может представлять интерес для сценариев тестирования, включая:

- Определение дополнительных путей или ресурсов для включения в обнаружение/анализ.
- Сбор открытой информации.
- Поиск информации о Bug Bounty и т.п.
- Социальная инженерия.

Файл может находиться либо в корневом каталоге web-сервера, либо в каталоге `.well-known/`. Например:

- `https://example.com/security.txt`
- `https://example.com/.well-known/security.txt`

Вот пример из реальной жизни, полученный из LinkedIn 5 мая 2020 года:

```bash
$ wget --no-verbose https://www.linkedin.com/.well-known/security.txt && cat security.txt
2020-05-07 12:56:51 URL:https://www.linkedin.com/.well-known/security.txt [333/333] -> "security.txt" [1]
# Conforms to IETF `draft-foudil-securitytxt-07`
Contact: mailto:security@linkedin.com
Contact: https://www.linkedin.com/help/linkedin/answer/62924
Encryption: https://www.linkedin.com/help/linkedin/answer/79676
Canonical: https://www.linkedin.com/.well-known/security.txt
Policy: https://www.linkedin.com/help/linkedin/answer/62924
```

### Humans TXT

`humans.txt` — это инициатива для знакомства с людьми, стоящими за web-сайтом. Он имеет форму текстового файла, который содержит информацию о людях, которые внесли свой вклад в создание сайта. Этот файл часто (хотя и не всегда) содержит информацию о карьерных возможностях.

Следующий пример был получен из Google 5 мая 2020 г.:

```bash
$ wget --no-verbose  https://www.google.com/humans.txt && cat humans.txt
2020-05-07 12:57:52 URL:https://www.google.com/humans.txt [286/286] -> "humans.txt" [1]
Google is built by a large team of engineers, designers, researchers, robots, and others in many different sites across the globe. It is updated continuously, and built with more tools and technologies than we can shake a stick at. If you'd like to help us out, see careers.google.com.
```

### Другие .well-known источники информации

Существуют другие RFC и проекты, которые предлагают стандартизированное использование файлов в каталоге `.well-known/`. Списки которых можно найти [здесь](https://en.wikipedia.org/wiki/List_of_/.well-known/_services_offered_by_webservers) или [тут](https://www.iana.org/assignments/well-known-uris/well-known-uris.xhtml).

Тестировщик может просмотреть RFC/проекты и создать список, который можно загрузить в сканер или фаззер, чтобы проверить существование или содержимое таких файлов.

## Инструменты

- Браузер (см. Исходный код страницы или Инструменты разработчика)
- curl
- wget
- Burp Suite
- ZAP
