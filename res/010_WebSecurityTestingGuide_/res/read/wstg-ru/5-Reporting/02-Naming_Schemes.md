---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Схемы наименования уязвимостей

В условиях постоянно растущего числа ИТ-активов, которые необходимо администрировать, специалистам по безопасности требуются новые и более производительные инструменты для проведения автоматизированного и всё более масштабного анализа. Благодаря программному обеспечению внимание можно сосредоточить на более творческих и интеллектуально сложных задачах. К сожалению, это непростая задача с учётом имеющегося разнообразия инструментов оценки уязвимостей, антивирусного программного обеспечения, систем обнаружения вторжений и пр. Это привело к ряду технических сложностей, требующих стандартизированного способа выявления каждой выявленной программной ошибки, уязвимости или некорректной настройки. Отсутствие возможностей по взаимодействию может привести к противоречиям во время оценки защищённости, запутанным отчётам и дополнительным усилиям по сопоставлению, которые помимо прочих проблем приведут к значительной трате ресурсов и времени.

Схема наименования — это систематическая методология, используемая для идентификации каждой из этих уязвимостей, чтобы облегчить чёткую идентификацию и обмен информацией. Эта цель достигается за счёт определения уникального, структурированного и эффективного с точки зрения программного обеспечения имени для каждой уязвимости. Существует несколько схем для облегчения этой работы, наиболее распространёнными из которых являются:

- Software Identification Tag (`SWID`)
- Common Platform Enumeration (`CPE`)
- Package URL (`PURL`)

## Software Identification Tag

Идентификационная метка программного обеспечения (англ.: Software Identification Tag, `SWID`) — это стандарт Международной организации по стандартизации, определённый в [ISO/IEC 19770-2:2015](https://itamstandards.org/iso-iec-19770-1-2/). Метки (теги) `SWID` используются для чёткой идентификации любого программного обеспечения в рамках полного жизненного цикла управления программными активами. Эта информационная схема рекомендуется для использования Национальным институтом стандартов и технологий (англ.: National Institute of Standards and Technology, NIST) в качестве основного идентификатора для любого разработанного или установленного программного обеспечения. Из `SWID` можно генерировать другие схемы, например, `CPE`, используемую Национальной базой данных уязвимостей (англ.: National Vulnerability Database, NVD), тогда как обратный процесс невозможен.

Каждый тег `SWID` представлен в стандартизированном формате XML. Тег `SWID` состоит из трёх групп элементов. Первый блок, состоящий из 7 предопределённых элементов, должен считаться допустимым тегом. За ним следует необязательный блок, содержащий набор из 30 возможных предопределённых элементов, которые создатель тега может использовать для предоставления достоверной и подробной информации. Наконец, группа элементов `Extended` (расширенная) предоставляет создателю тега возможность определить любые заранее не определённые элементы, необходимые для точного определения описываемого программного обеспечения. Высокий уровень детализации, обеспечиваемый `SWID`, даёт возможность не только описать данный программный продукт, но и его конкретный статус в жизненном цикле программного обеспечения.

### Примеры SWID

- _ACME Roadrunner Service Pack 1_ — патч, созданный корпорацией ACME для уже установленного продукта, идентифицированного с помощью `@tagId` как: _com.acme.rms-ce-v4-1-5-0_:

```xml
<SoftwareIdentity
                  xmlns="http://standards.iso.org/iso/19770/-2/2015/schema.xsd"
                  name="ACME Roadrunner Service Pack 1"
                  tagId="com.acme.rms-ce-sp1-v1-0-0"
                  patch="true"
                  version="1.0.0">
  <Entity
          name="The ACME Corporation"
          regid="acme.com"
          role="tagCreator softwareCreator"/>
  <Link
        rel="patches"
        href="swid:com.acme.rms-ce-v4-1-5-0">
    ...
</SoftwareIdentity>
```

- Red Hat Enterprise Linux версии 8 для архитектуры x86-64:

```xml
<SoftwareIdentity
                  xmlns="http://standards.iso.org/iso/19770/-2/2015/schema.xsd"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                  xsi:schemaLocation="http://standards.iso.org/iso/19770/-2/2015/schema.xsd"
                  xml:lang="en-US"
                  name="Red Hat Enterprise Linux"
                  tagId="com.redhat.RHEL-8-x86_64"
                  tagVersion="1"
                  version="8"
                  versionScheme="multipartnumeric"
                  media="(OS:linux)">
```

## Common Platform Enumeration

Общая инвентаризация платформ (англ.: Common Platform Enumeration, `CPE`) представляет собой структурированную схему наименования систем информационных технологий, программного обеспечения и пакетов, поддерживаемых `NVD`. Обычно используется в сочетании с общими идентификационными кодами уязвимостей и рисков (англ.: Common Vulnerabilities and Exposures, CVE), например, `CVE-2017-0147`. Несмотря на то, что `CPE` считается устаревшей, на смену которой пришла `SWID`, она по-прежнему широко применяется в некоторых решениях по безопасности.

Определяется как [словарь](https://nvd.nist.gov/products/cpe), предоставляемый `NVD`. Каждый код `CPE` может быть определён как правильно оформленное имя или как URL. Каждое значение должно соответствовать следующей структуре:

- _cpe-name_ = "cpe:" component-list
- _component-list_ = part ":" vendor ":" product ":" version ":" update ":" edition ":" lang
- _component-list_ = part ":" vendor ":" product ":" version ":" update ":" edition
- _component-list_ = part ":" vendor ":" product ":" version ":" update
- _component-list_ = part ":" vendor ":" product ":" version
- _component-list_ = part ":" vendor ":" product
- _component-list_ = part ":" vendor
- _component-list_ = part
- _component-list_ = empty
- _part_ = "h" / "o" / "a" = string
- _vendor_ = string
- _product_ = string
- _version_ = string
- _update_ = string
- _edition_ = string
- _lang_ LANGTAG / empty
- _string_ = *( unreserved / pct-encoded )
- _empty_ = ""
- _unreserved_ = ALPHA / DIGIT / "-" / "." / "_" / " ̃"
- _pct-encoded_ = "%" HEXDIG HEXDIG
- _ALPHA_ = %x41-5a / %x61-7a ; A-Z or a-z
- _DIGIT_ = %x30-39 ; 0-9
- _HEXDIG_ = DIGIT / "a" / "b" / "c" / "d" / "e" / "f"
- _LANGTAG_ = cf. [RFC5646]

### Примеры CPE

- Microsoft Internet Explorer 8.0.6001 Beta (любая версия): `wfn:[part="a",vendor="microsoft",product="internet_explorer", version="8\.0\.6001",update="beta",edition=ANY]`, который связан со следующим URL: `cpe:/a:microsoft:internet_explorer:8.0.6001:beta`.
- Foo\Bar Big$Money Manager 2010 Специальная версия для iPod Touch 80GB: `wfn:[part="a",vendor="foo\\bar",product="big\$money_manager_2010", sw_edition="special",target_sw="ipod_touch",target_hw="80gb"]`, который связан со следующим URL: `cpe:/a:foo%5cbar:big%24money_manager_2010:::~~special~ipod_touch~80gb~`.

## Package URL

URL пакета (англ.: Package URL, PURL) стандартизирует способ представления метаданных программного пакета, чтобы пакеты можно было найти где угодно, независимо от того, к какому поставщику, проекту или экосистеме они принадлежат.

PURL — это допустимая [RFC3986](https://www.rfc-editor.org/rfc/rfc3986) ASCII-строка, определяющая URL, состоящая из семи элементов. Каждый из них отделён определённым символом, чтобы программы могли легко манипулировать ею.

`scheme:type/namespace/name@version?qualifiers#subpath`

Определения для каждого компонента:

- _scheme_: постоянное значение pkg, соответствующее схеме URL (**обязательный**).
- _type_: тип или протокол пакета, например, maven, npm, nuget, gem, pypi и т.д. (**обязательный**).
- _namespace_: зависящее от типа значение префикса пакета, например, имя владельца, идентификатор группы и т.д. (по желанию).
- _name_: название пакета (**обязательный**).
- _version_: версия пакета (по желанию).
- _qualifiers_: дополнительные уточняющие данные для пакета, такие как ОС, архитектура, дистрибутив и т.д. (по желанию).
- _subpath_: дополнительный путь внутри пакета, относительно его корня (по желанию).

### Примеры PURL

- Программное обеспечение Curl, упакованное в виде пакета `.deb` для Debian Jessie, предназначенного для архитектуры i386: `pkg:deb/debian/curl@7.50.3-1?arch=i386&distro=jessie`
- Docker-образ Apache Cassandra, подписанный SHA256-хэшем 244fd47e07d1004f0aed9c: `pkg:docker/cassandra@sha256:244fd47e07d1004f0aed9c`

## Рекомендации по использованию

| Использование  | Рекомендации  |
|---|---|
| Клиентское или серверное приложение | CPE или SWID |
| Контейнер | PURL или SWID |
| Прошивка (Firmware) | CPE или SWID* |
| Библиотека или фреймворк (пакет) | PURL |
| Библиотека или платформа (без пакета) | SWID |
| Операционная система | CPE или SWID |
| Пакет операционной системы | PURL или SWID |

> Примечание: при наличии выбора между двумя методами, из-за устаревания `CPE` рекомендуется, чтобы в новых проектах использовался `SWID`. Несмотря на то, что `CPE`, как известно, является широко используемой схемой наименования в текущих активных проектах и решениях.

## Ссылки

- [NISTIR 8060 - Guidelines for the Creation of Interoperable Software Identification (SWID) Tags (pdf)](https://nvlpubs.nist.gov/nistpubs/ir/2016/NIST.IR.8060.pdf)
- [NISTIR 8085 - Forming Common Platform Enumeration (CPE) Names from Software Identification (SWID) Tags (pdf)](https://csrc.nist.gov/CSRC/media/Publications/nistir/8085/draft/documents/nistir_8085_draft.pdf)
- [ISO/IEC 19770-2:2015 — Information technology — Software asset management — Part 2: Software identification tag](https://www.iso.org/standard/65666.html)
- [Official Common Platform Enumeration (CPE) Dictionary](https://nvd.nist.gov/products/cpe)
- [Common Platform Enumeration: Dictionary Specification Version 2.3](https://csrc.nist.gov/publications/detail/nistir/7697/final)
- [PURL Specification](https://github.com/package-url/purl-spec)
- [A Proposal to Operationalize Component Identification for Vulnerability Management (pdf)](https://owasp.org/assets/files/posts/A%20Proposal%20to%20Operationalize%20Component%20Identification%20for%20Vulnerability%20Management.pdf)

### Известные реализации

- [packageurl-go](https://github.com/package-url/packageurl-go)
- [packageurl-dotnet](https://github.com/package-url/packageurl-dotnet)
- [packageurl-java](https://github.com/package-url/packageurl-java), [+Sonatype](https://github.com/sonatype/package-url-java)
- [packageurl-python](https://github.com/package-url/packageurl-python)
- [packageurl-rust](https://github.com/package-url/packageurl.rs)
- [packageurl-js](https://github.com/package-url/packageurl-js)
