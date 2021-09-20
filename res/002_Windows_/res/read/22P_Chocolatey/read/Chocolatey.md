## [_GUIDES_][1] > [**Windows**][3] > 2. SPEC. PROG. > 2. SERV. > Pack Managers > *Chocolatey*

## <p align=center>[Git & GitHub][2] | [Windows][3] | [Linux][4] | [Networks][5] <br/> [Programming][6] | [Databases][7] | [Docker & Kubernetes][8] | [Embedded systems][9] </p>

<!--
* [_GUIDES_][1]
* [Git & GitHub][2]
* [Windows][3]
* [Linux][4]
* [Networks][5]
* [Programming][6]
* [Databases][7]
* [Docker & Kubernetes][8]
* [Embedded systems][9]
-->

[1]: ../../../../../../README.md
[2]: ../../../../../001_Git_and_GitHub_/Git_And_GitHub.md
[3]: ../../../../Windows.md
[4]: ../../../../../003_Linux_(Unix)_/Linux_(Unix).md
[5]: ../../../../../004_Networks_/Networks.md
[6]: ../../../../../005_Programming_languages_/Programming.md
[7]: ../../../../../006_Databases_/Databases.md
[8]: ../../../../../007_Docker_and_Kubernetes_/Docker_and_Kubernates.md
[9]: ../../../../../008_Embedded_systems_/Embedded_systems.md

--- 
<br/>
<!-- ---------------------------------- * Navigation * ---------------------------------- -->

# <p align=center><b>Chocolatey</b></p>

Packages managers:
* [Chokolatey][10]
<!--* [Vagrant][] -->

---
<br/>

## Chocolatey magic: apt-get and yum (dnf) for Windows
В наше время становится все меньше и меньше людей, которые хоть раз не устанавливали софт в среде Linux. Это невероятно просто: для установки midnight commander (mc), в среде RH (RedHat Enterprise, CentOS, Fedora, и т.д) нам всего лишь нужна пара «волшебных» команд:
```bash
yum install mc
```
Менеджер пакетов yum позаботится о том, чтобы установилась самая свежая версия mc, а также о зависимостях пакета, если таковые имеются. Но что же делать, если в нашем распоряжении находится Windows, а мы хотим что-то подобное? Правильно, перейти на Linux или читать дальше!

Под моей «опекой» находится гетерогенная сеть из Windows и Linux машин (проще сказать — зоопарк), и вот уже около двух лет для установки софта под Win* я пользуюсь, где это возможно, Chocolatey. Chocolatey ([chocolatey.org][11], [github.com/chocolatey][12] ) — система управления пакетами, во многом схожая с apt-get или yum, но только для Windows.

На хабре уже касались темы Chocolatey в контексте разработчика, сегодня я хочу взглянуть на этот замечательный инструмент с точки зрения системного администратора. Chocolatey работает на основе технологии NuGet (активно используется разработчиками софта под Windows), и основная черта Chocolatey — пакеты чаще всего **не содержат установочных файлов** (setup.msi, setup.exe, и т.д...). Работает это следующим образом: в пакете находится скрипт-установщик на powershell, который скачивает и устанавливает нужную версию установочного файла из нужного места в интернете, а Вам остается только наслаждаться легкостью установки.

## Установка Chocolatey
Прежде чем получить возможность использовать магию Chocolatey нам нужно установить ее ядро. Для этого запускаем в командной строке:

```sh
@powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%systemdrive%\chocolatey\bin
```

Эта команда скачает и запустит основной скрипт установки [chocolatey.org/install.ps1][13], а также настроит требуемые переменные окружения. Теперь, когда у нас есть все необходимое давайте испытаем систему управления пакетами и установим Nodepad++. Достаточно выполнить следующую команду:

```sh
cinst notepadplusplus
```

Какие еще есть пакеты и откуда они берутся?

Как и NuGet, Chocolatey обладает внушительным списком пакетов, который располагается в репозитории, он же [библиотека пакетов][14]. Вот только некоторые из них:

**Топ 10 самых популярных пакетов на chocolatey.org (28.01.2014)**
- Git — 51191 скачиваний
- Notepad++ — 37533 скачиваний
- 7Zip — 37802 скачиваний
- Google Chrome — 25960 скачиваний
- Java Runtime — 25699 скачиваний
- NodeJS — 25542 скачиваний
- Mozilla Firefox — 20747 скачиваний
- Adobe Flash Player — 20660 скачиваний
- VLC Player — 20419 скачиваний
- Ruby 2.0 — 19587 скачиваний

Пакеты добавляются каждый день, ведь любой желающий может добавить свой пакет на chocolatey.org, главное чтобы он отвечал [требованиям][15].

**Требования к публикации пакетов**:
* **Не публикуйте незаконные программы.** Программы, которые незаконны в большинстве стран мира также запрещены к размещению на Chocolatey.org. Это также применимо к программам, которые нарушает авторские права, пиратские программы и «кряки». Помните, что это также касается программ которые используются для пиратства.
* **Не пакуйте программы в chocolatey на которые у Вас нет прав на распространение. **Пожалуйста, уточняйте правила распространения программного обеспечения и не нарушайте их.
* **Не публикуйте вирусы либо любые другие программы наносящие вред.**
* Публикуйте только те программы, которые будут полезны для других. Если Ваш пакет не относится к этой категории — не публикуйте его.
* **Не публикуйте spyware или adware.** Программы, которые поставляются с встроенными adware или spyware или любыми другими нерелевантными программами не разрешены для публикации. Обычно все нерелевантные программы можно исключить из установки используя ключи установщика. Примерами таких программ являются PDFCreator и CCleaner.
* **Не публикуйте программы, которые уже опубликованы.** Используйте поиск по Chocolatey.org. Если Вы хотите улучшить уже существующий пакет — свяжитесь с человеком, который поддерживает пакет или отправьте pull-request в его репозиторий.
* **Не включайте другие программы в Ваш пакет, если для них уже есть свой пакет.** Если Вашему пакету требуется те или иные программы, существующий пакет должен быть включен Вами в качестве зависимости.
* **Разделяйте зависимости на несколько пакетов.** Старайтесь разделить пакет на как можно больше пакетов. Например программа поставляется с опциональными модулями. Создайте дополнительные пакеты для модулей, вместо того, чтобы включать их в общий пакет. Эта идея уже давно применяется в пакетах под Linux по той причине, что это позволяет создавать легковесные пакеты и минимизирует шанс конфликта.

## Как это работает?
Я хотел бы подробнее разобрать содержание пакетов Chocolatey на примере logstash, который я создавал специально для развертывания агента logstash на сервере Windows:

```
\logstash
  \tools
    chocolateyInstall.ps1
  logstash.nuspec
```

Здесь видно, что в пакете всего 2 файла: logstash.nuspec и chocolateyInstall.ps1.

### **logstash.nuspec** - файл, в котором описывается мета-информация пакета
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
  <metadata>
    <id>logstash</id>
    <version>1.2.1.2013101701</version>
    <title>logstash</title>
    <authors>kireevco</authors>
    <owners>http://chocolatey.org/profiles/kireevco</owners>
    <projectUrl>https://github.com/kireevco/chocolatey-packages</projectUrl>
  <copyright>http://logstash.net</copyright>
    <iconUrl>http://logstash.net/images/logstash.png</iconUrl>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Logstash is a tool for managing events and logs. You can use it to collect logs, parse them, and store them for later use (like, for searching). Speaking of searching, logstash comes with a web interface for searching and drilling into all of your logs. This package installs logstash flat jar as an agent service via nssm. All you need to do - is to configure your logstash.conf and start logstash service. Service is installed with these parameters: "java.exe -Xmx512M -jar logstash.jar agent --config logstash.conf --log logstash.log
"</description>
    <summary>Logstash Agent package</summary>
    <tags>logstash, logging</tags>
    <dependencies>
      <dependency id="javaruntime" version="7.0.0" />
      <dependency id="NSSM" version="2.16.0" />
      <dependency id="Chocolatey" version="0.9.8.20" />
    </dependencies>
  </metadata>
</package>
```

В этом файле будет интересно разобрать секцию *dependencies*, в которой мы указываем что нашему пакету необходимо наличие 3х других пакетов определенных версий, а именно [javaruntime][16], [NSSM][17] (позволяет установить наш .jar файл в качестве службы Windows), а также Chocolatey определенной версии. Если какой-либо из необходимых пакетов отсутствует, либо его версия не соответствует требуемой — система зависимостей разрешит ситуацию и приведет все к требуемому виду. Стоит отметить, что для указания версий используется [нотация nuget][18].

### Powershell скрипт chocolateyInstall.ps1
```sh
#Указываем откуда скачивать jar файл
$url='https://download.elasticsearch.org/logstash/logstash/logstash-1.2.1-flatjar.jar' 

#Указываем путь где будет раполагаться управляющий cmd файл
$cmdfile='c:/logstash/logstash.cmd'

#Указываем куда копировать конфигурационный файл
$confile = 'c:/logstash/logstash.conf.sample'
$dir='c:/logstash'

if (!(Test-Path -path $dir)) {New-Item $dir -Type Directory}

Get-ChocolateyWebFile 'logstash' 'c:/logstash/logstash.jar' $url $url
$cmdcontent = @"
set HOME=c:/logstash/sincedb
cd /d c:\logstash
java.exe -Xmx512M -jar logstash.jar agent --config logstash.conf --log logstash.log
"@
Set-Content $cmdfile $cmdcontent -Encoding ASCII

#Создаем тестовый конфиг
$confcontent = @"
input {
  stdin {}
}

output {
   stdout {}
}
"@
Set-Content $confile $confcontent -Encoding ASCII


if ($serviceinfo = Get-Service "Logstash" -ErrorAction SilentlyContinue)
{
  if ($serviceinfo.status -ne 'Running')
  {
    if ($serviceinfo.status -eq 'Stopped')
    {
      echo "Service found and is stopped. Deleting."
      echo "Delete Service"

      sc.exe \\localhost delete "Logstash"
      nssm install "Logstash" C:\logstash\logstash.cmd
    }
  }
  else
  {
    echo "Stop Service"
    sc.exe \\localhost stop "Logstash"
    echo "Delete Service"
    sc.exe \\localhost delete "Logstash"
    echo "Installing Service"
    nssm install "Logstash" C:\logstash\logstash.cmd

  }
}
else
{
  #Устанавливаем службу через nssm
  echo "Installing Logstash Service"
  nssm install "Logstash" C:\logstash\logstash.cmd
}
```

## Применение:
Многие админы, вероятно, побежали тестировать функционал — оно и правильно, ведь ничего сложного в использовании Chocolatey нет — в этом-то и есть сладость Chocolatey. Тем не менее, хотелось бы предложить несколько сценариев использования этого менеджера пакетов для Windows.

### Cmd и Powershell скрипты
Все мы используем простейшие скрипты в нашей работе, и chocolatey как нельзя лучше интегрируется в этот процесс. Простейший скрипт для обычной клиентской машины может выглядеть так:

```sh
cinst flashplayerplugin
cinst flashplayeractivex
cinst notepadplusplus
cinst sublimetext2
cinst 7zip
cinst GoogleChrome
cinst javaruntime
cinst Firefox
cinst flashplayerplugin
cinst adobereader
cinst ccleaner
cinst sysinternals
cinst putty
cinst filezilla
cinst dropbox
cinst skype
cinst paint.net
cinst virtualbox
cinst DotNet4.5
cinst Wget
cinst ConEmu
cinst libreoffice
cinst PDFCreator
cinst teamviewer
cinst wuinstall.run
```

## Puppet
Я использую Puppet для управления конфигурацией своей инфраструктуры, что экономит мне массу времени и нервов. В Puppet есть замечательная концепция ресурсов, а также декларативный стиль, которые в купе помогают мыслить абстрактно, на уровне «Какая программа должна стоять на том или ином сервере», а не на уровне «Какие комманды я должен запустить на Windows, а какие на Linux». Для Puppet существует [провайдер Chocolatey][19], который позволяет нам сделать следующее:

```
package {
    "7zip" : ensure => installed,    
}
```

или

```
package {
    "notepadplusplus" : ensure => 1.0,    
}
```

Обо всем остальном позаботятся Puppet и Chocolatey. Поверьте, это намного удобнее чем производить установку из msi файла, который нужно еще где-то захостить, а также удостовериться что при обновлении версии (которое еще нужно сделать) старые версии тоже сохраняться и ничего при этом не сломается.

## Chocolatey и Desktop
Предлагаю рассмотреть два способа использования Chocolatey для администрировании рабочих станций.

**ChocolateyGUI** — это графический интерфейс для системы управления пакетов Chocolatey. Удобный способ для обзора текущего состояния репозитория, а также состояния локально-установленных пакетов. Мне почему-то очень сильно напомнило раннюю версию synaptic или даже aptitude. Работает достаточно сносно. Установить его, кстати, можно из коммандной строки:

```
cinst ChocolateyGUI
```

![Chocolatey GUI][20]

## Windows Post Install (WPI)
Можно пойти еще дальше, использовать интерфейс [WPI][21] для удобного выбора пакетов, в котором будут исполняться команды Chocolatey. При помощи WPI можно удобно группировать программы по категориям, а также создавать шаблоны и наборы установки.
Решение не всегда сможет стать абсолютной альтернативой использования USB-HDD в качестве источника, но заменив все возможные компоненты на аналогичные из репозитория Chocolatey Вы избавите себя от мучительного копирования образа (папки) с полным набором софта (Photoshop, Office, 3D Max с Архикадом, что там еще?) и оболочкой WPI (а все ради того, чтобы поставить «легкие» программы вроде Google Chrome, Notepad++, Avast и т.п.).

К примеру, для приходящих админов, поддерживающих разрозненный парк машин без централизованного хранилища удобно иметь что-то вроде такого списка шаблонов:
* Бизнес
* Бухгалтер
* Разработчк
* Домашний пользователь
* Медиа-Станция

![Win PIW 1][22]

![Win PIW 2][23]

![Win PIW 3][24]

Таким образом, WPI всего лишь является оболочкой для запуска команд Chocolatey, что позволяет уменьшить суммарный объем дистрибутива. Конечно, при таком подходе на клиентской машине уже должен быть рабочее интернет-подключение, что сегодня не является проблемой, за исключением отдельных случаев.
<br/>
Возвращаясь к программам которые отсутствуют в репозитории Chocolatey.org, следует упомянуть, что Chocolatey поддерживает любые NuGet фиды, а не только предлагаемый по-умолчанию chocolatey.org. Заливаем важные файлы в DropBox и создаем свой пакет где-нибудь на www.myget.org — это очень просто!
<br/>

Если кому интересно, могу рассказать в подробностях (в форме отдельного поста) как создать свой пакет и как загрузить его в репозиторий chocolatey.org, и о том, как я научил Windows устанавливать все обновления без моего участия (с перезагрузками и лицензиями), как я обновляю базу maxmind.dat в автоматическом режиме, как я использую logstash и многом другом, и все это не без помощи chocolatey и puppet!
<br/>

В заключение скажу, что на мой взгляд, идея децентрализованной системы управления пакетам для Windows и ее реализация — очередной способ убедиться что в наши дни opensource и открытие технологии становится не менее качественными и применимыми к реалиям системного администрирования. Закрытый код все реже становится рыночным преимуществом того или иного сообщества / компании, в то время как реализация и поддержка играют огромную роль. Представить что десять лет назад открытый проект, созданный одним человеком сможет создать такой резонанс в широких кругах, да еще и Windows кругах — нереально, а сегодня Chocolatey — это еще один шанс окунуться в opensource сообщество и убедиться в открытой возможности внести свой вклад в общую идею.
<br/>

На любые ошибки и неточности прошу указывать в комментариях, с удовольствием поправлю и дополню материал.

<!--
* [Chokolatey][10]
* [chocolatey.org][11]
* [github.com/chocolatey][12]
* [chocolatey.org/install.ps1][13]
* [библиотека пакетов][14]
* [требованиям][15]
* [javaruntime][16]
* [NSSM][17]
* [нотация nuget][18]
* [провайдер Chocolatey][19]
* [Chocolatey GUI][20]
* [WPI][21]
* [Win PIW 1][22]
* [Win PIW 2][23]
* [Win PIW 3][24]

* [Vagrant][]
-->

[10]: https://habr.com/ru/post/210626/
[11]: http://chocolatey.org/
[12]: https://github.com/chocolatey/chocolatey
[13]: https://chocolatey.org/install.ps1
[14]: http://chocolatey.org/packages
[15]: https://github.com/chocolatey/chocolatey/wiki/CreatePackages
[16]: http://chocolatey.org/packages/javaruntime
[17]: http://chocolatey.org/packages/NSSM
[18]: http://docs.nuget.org/docs/reference/versioning
[19]: http://forge.puppetlabs.com/rismoney/chocolatey
[20]: ../img/2176f009962c386c64d9f7584cc7be8f.png
[21]: http://www.wpiw.net/
[22]: ../img/03830d588fd96d8853fe9d324d1ceccb.jpg
[23]: ../img/bdd242fc109f32fad5a0671be2b20592.jpg
[24]: ../img/955bce902d302cbe036ae74d7dec59d4.jpg

<!--[]: -->

---
<br/>