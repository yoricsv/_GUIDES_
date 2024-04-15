---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Тестирование ограничений на количество раз, которое функция может быть вызвана

|ID          |
|------------|
|WSTG-BUSL-05|

## Обзор

Многие проблемы, решаемые приложениями, требуют ограничений на количество раз, которое может быть использована функция или какое действие может быть выполнено. Приложения должны быть «достаточно интеллектуальными», чтобы не позволить пользователю превысить свой лимит на использование этих функций, поскольку во многих случаях каждый раз, когда функция используется, пользователь может получить некоторую выгоду, которую необходимо учитывать, чтобы должным образом компенсировать владельцу. Например: сайт электронной коммерции может разрешать пользователям применять скидку только один раз за транзакцию, или некоторые приложения согласно тарифному плану пользователя могут позволять загружать только три полных документа в месяц.

Уязвимости, связанные с тестированием ограничений функций, зависят от конкретного приложения, и необходимо придумать примеры некорректного использования, которые стремятся выполнить приложение/функцию/или действие больше допустимого количества раз.

Злоумышленники могут обойти бизнес-логику и выполнить функцию больше раз, чем это «допустимо», используя приложение для личной выгоды.

### Пример

Предположим, сайт электронной коммерции позволяет пользователям воспользоваться любой из множества скидок на общую сумму покупки, а затем перейти к оплате и получению заказа. Что произойдёт, когда злоумышленник возвратится на страницу скидок после получения и применения одной из «допустимых» скидок? Сможет ли он воспользоваться другой скидкой? Сможет ли он воспользоваться одной и той же скидкой несколько раз?

## Задачи тестирования

- Найти функции, для которых должны быть установлены ограничения на количество раз, которое их можно вызвать.
- Оценить, установлено ли логическое ограничение для функций и корректно ли оно контролируется.

## Как тестировать

- Проанализируйте проектную документацию и проведите ознакомительное тестирование для поиска функций или возможностей в приложении или системе, которые не должны выполняться более одного раза (или заданного количества раз) в течение бизнес-процесса.
- Для каждой из найденных функций и возможностей, которые должны выполняться только один (или заданное количество) раз в ходе бизнес-процесса, придумайте примеры злоупотребления/некорректного использования, которые могут позволить пользователю выполнить их больше допустимого количества раз. Например, может ли пользователь  несколько раз перемещаться вперед и назад по страницам, вызывая функцию, которая должна выполняться только один раз? Или он может наполнять и освобождать корзину для покупок, что позволяет получать дополнительные скидки?

## Связанные сценарии тестирования

- [Перебор и угадывание учётных записей пользователей](../03-Identity_Management_Testing/04-Testing_for_Account_Enumeration_and_Guessable_User_Account.md)
- [Тестирование механизма блокировки](../04-Authentication_Testing/03-Testing_for_Weak_Lock_Out_Mechanism.md)

## Меры защиты

Приложение должно применять жёсткие меры для предотвращения злоупотреблений ограничениями. Этого можно добиться в зависимости от того, что лучше соответствует бизнес-требованиям. Например, установив ограничение на уровне базы данных, что скидочный купон больше не действителен; или установив в серверной части предел для счётчика по каждому пользователю, т.к. все пользователи должны быть идентифицированы по их сессии.

## Ссылки

- [InfoPath Forms Services business logic exceeded the maximum limit of operations Rule](http://mpwiki.viacode.com/default.aspx?g=posts&t=115678)
- [Gold Trading Was Temporarily Halted On The CME This Morning](https://www.businessinsider.com/gold-halted-on-cme-for-stop-logic-event-2013-10)