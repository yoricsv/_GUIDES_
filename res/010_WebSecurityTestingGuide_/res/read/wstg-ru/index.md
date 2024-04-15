---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Содержание

## 0. [Предисловие от Ойна Кири](0-Foreword/README.md)

## 1. [Фронтиспис](1-Frontispiece/)

## 2. [Введение](2-Introduction/)

### 2.1 [Проект OWASP по тестированию](2-Introduction/README.md#проект-owasp-по-тестированию)

### 2.2 [Принципы тестирования](2-Introduction/README.md#принципы-тестирования)

### 2.3 [Методы тестирования](2-Introduction/README.md#методы-тестирования)

### 2.4 [Ручные проверки](2-Introduction/README.md#ручные-проверки)

### 2.5 [Моделирование угроз](2-Introduction/README.md#моделирование-угроз)

### 2.6 [Анализ исходного кода](2-Introduction/README.md#анализ-исходного-кода)

### 2.7 [Тестирование на проникновение](2-Introduction/README.md#тестирование-на-проникновение)

### 2.8 [Нужен сбалансированный подход](2-Introduction/README.md#нужен-сбалансированный-подход)

### 2.9 [Определение требований к тестированию безопасности](2-Introduction/README.md#определение-требований-к-тестированию-безопасности)

### 2.10 [Включение тестов безопасности в процессы разработки и тестирования](2-Introduction/README.md#включение-тестов-безопасности-в-процессы-разработки-и-тестирования)

### 2.11 [Анализ данных по тестированию безопасности и отчётность](2-Introduction/README.md#анализ-данных-по-тестированию-безопасности-и-отчётность)

## 3. [Методика тестирования OWASP](3-The_OWASP_Testing_Framework/)

### 3.1 [Методика тестирования безопасности web-приложений](3-The_OWASP_Testing_Framework/0-The_Web_Security_Testing_Framework.md)

### 3.2 [Этап 1. До начала разработки](3-The_OWASP_Testing_Framework/0-The_Web_Security_Testing_Framework.md#этап-1-до-начала-разработки)

### 3.3 [Этап 2. В процессе определения и проектирования](3-The_OWASP_Testing_Framework/0-The_Web_Security_Testing_Framework.md#этап-2-в-процессе-определения-и-проектирования)

### 3.4 [Этап 3. В процессе разработки](3-The_OWASP_Testing_Framework/0-The_Web_Security_Testing_Framework.md#этап-3-в-процессе-разработки)

### 3.5 [Этап 4. В процессе развёртывания](3-The_OWASP_Testing_Framework/0-The_Web_Security_Testing_Framework.md#этап-4-в-процессе-развёртывания)

### 3.6 [Этап 5. В процессах сопровождения и эксплуатации](3-The_OWASP_Testing_Framework/0-The_Web_Security_Testing_Framework.md#этап-5-в-процессах-сопровождения-и-эксплуатации)

### 3.7 [Типичный процесс тестирования в SDLC](3-The_OWASP_Testing_Framework/0-The_Web_Security_Testing_Framework.md#типичный-процесс-тестирования-в-SDLC)

### 3.8 [Методологии тестирования на проникновение](3-The_OWASP_Testing_Framework/1-Penetration_Testing_Methodologies.md)

## 4. [Тестирование безопасности web-приложений](4-Web_Application_Security_Testing/)

### 4.0 [Введение и назначение](4-Web_Application_Security_Testing/00-Introduction_and_Objectives/README.md)

### 4.1 [Сбор информации](4-Web_Application_Security_Testing/01-Information_Gathering/README.md)

#### 4.1.1 [Разведка в поисковых системах](4-Web_Application_Security_Testing/01-Information_Gathering/01-Conduct_Search_Engine_Discovery_Reconnaissance_for_Information_Leakage.md)

#### 4.1.2 [Определение web-сервера](4-Web_Application_Security_Testing/01-Information_Gathering/02-Fingerprint_Web_Server.md)

#### 4.1.3 [Анализ метафайлов web-сервера](4-Web_Application_Security_Testing/01-Information_Gathering/03-Review_Webserver_Metafiles_for_Information_Leakage.md)

#### 4.1.4 [Инвентаризация приложений на web-сервере](4-Web_Application_Security_Testing/01-Information_Gathering/04-Enumerate_Applications_on_Webserver.md)

#### 4.1.5 [Анализ контента web-страницы](4-Web_Application_Security_Testing/01-Information_Gathering/05-Review_Webpage_Content_for_Information_Leakage.md)

#### 4.1.6 [Определение точек входа в приложение](4-Web_Application_Security_Testing/01-Information_Gathering/06-Identify_Application_Entry_Points.md)

#### 4.1.7 [Пути выполнения приложения](4-Web_Application_Security_Testing/01-Information_Gathering/07-Map_Execution_Paths_Through_Application.md)

#### 4.1.8 [Определение фреймворка web-приложения](4-Web_Application_Security_Testing/01-Information_Gathering/08-Fingerprint_Web_Application_Framework.md)

#### 4.1.9 [Определение web-приложения](4-Web_Application_Security_Testing/01-Information_Gathering/09-Fingerprint_Web_Application.md)

#### 4.1.10 [Архитектура приложения](4-Web_Application_Security_Testing/01-Information_Gathering/10-Map_Application_Architecture.md)

### 4.2 [Тестирование управления конфигурациями и развёртыванием](4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/README.md)

#### 4.2.1 [Анализ конфигурации сетевой инфраструктуры](4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/01-Test_Network_Infrastructure_Configuration.md)

#### 4.2.2 [Тестирование конфигурации платформы приложения](4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/02-Test_Application_Platform_Configuration.md)

#### 4.2.3 [Тестирование обработки расширений файлов](4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/03-Test_File_Extensions_Handling_for_Sensitive_Information.md)

#### 4.2.4 [Анализ старых резервных копий и файлов без ссылок](4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/04-Review_Old_Backup_and_Unreferenced_Files_for_Sensitive_Information.md)

#### 4.2.5 [Инвентаризация интерфейсов администрирования](4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/05-Enumerate_Infrastructure_and_Application_Admin_Interfaces.md)

#### 4.2.6 [Тестирование методов HTTP](4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/06-Test_HTTP_Methods.md)

#### 4.2.7 [Тестирование HTTP Strict Transport Security (HSTS)](4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/07-Test_HTTP_Strict_Transport_Security.md)

#### 4.2.8 [Тестирование междоменной политики для RIA](4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/08-Test_RIA_Cross_Domain_Policy.md)

#### 4.2.9 [Тестирование разрешений на доступ к файлам](4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/09-Test_File_Permission.md)

#### 4.2.10 [Тестирование на захват поддомена](4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/10-Test_for_Subdomain_Takeover.md)

#### 4.2.11 [Тестирование облачного хранилища](4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/11-Test_Cloud_Storage.md)

#### 4.2.12 [Тестирование Content Security Policy (CSP)](4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/12-Test_for_Content_Security_Policy.md)

### 4.3 [Тестирование управления идентификацией](4-Web_Application_Security_Testing/03-Identity_Management_Testing/README.md)

#### 4.3.1 [Тестирование определения ролей (RBAC)](4-Web_Application_Security_Testing/03-Identity_Management_Testing/01-Test_Role_Definitions.md)

#### 4.3.2 [Тестирование процесса регистрации пользователя](4-Web_Application_Security_Testing/03-Identity_Management_Testing/02-Test_User_Registration_Process.md)

#### 4.3.3 [Тестирование процесса создания учётных записей](4-Web_Application_Security_Testing/03-Identity_Management_Testing/03-Test_Account_Provisioning_Process.md)

#### 4.3.4 [Перебор и угадывание учётных записей пользователей](4-Web_Application_Security_Testing/03-Identity_Management_Testing/04-Testing_for_Account_Enumeration_and_Guessable_User_Account.md)

#### 4.3.5 [Тестирование политики в отношении имён пользователей](4-Web_Application_Security_Testing/03-Identity_Management_Testing/05-Testing_for_Weak_or_Unenforced_Username_Policy.md)

### 4.4 [Тестирование аутентификации](4-Web_Application_Security_Testing/04-Authentication_Testing/README.md)

#### 4.4.1 [Тестирование учётных данных, передаваемых по зашифрованному каналу](4-Web_Application_Security_Testing/04-Authentication_Testing/01-Testing_for_Credentials_Transported_over_an_Encrypted_Channel.md)

#### 4.4.2 [Тестирование учётных данных по умолчанию](4-Web_Application_Security_Testing/04-Authentication_Testing/02-Testing_for_Default_Credentials.md)

#### 4.4.3 [Тестирование механизма блокировки](4-Web_Application_Security_Testing/04-Authentication_Testing/03-Testing_for_Weak_Lock_Out_Mechanism.md)

#### 4.4.4 [Тестирование обхода схемы аутентификации](4-Web_Application_Security_Testing/04-Authentication_Testing/04-Testing_for_Bypassing_Authentication_Schema.md)

#### 4.4.5 [Тестирование уязвимого запоминания пароля](4-Web_Application_Security_Testing/04-Authentication_Testing/05-Testing_for_Vulnerable_Remember_Password.md)

#### 4.4.6 [Тестирование уязвимостей кэша браузера](4-Web_Application_Security_Testing/04-Authentication_Testing/06-Testing_for_Browser_Cache_Weaknesses.md)

#### 4.4.7 [Тестирование парольной политики](4-Web_Application_Security_Testing/04-Authentication_Testing/07-Testing_for_Weak_Password_Policy.md)

#### 4.4.8 [Тестирование ответа на контрольный вопрос](4-Web_Application_Security_Testing/04-Authentication_Testing/08-Testing_for_Weak_Security_Question_Answer.md)

#### 4.4.9 [Тестирование функций изменения или сброса пароля](4-Web_Application_Security_Testing/04-Authentication_Testing/09-Testing_for_Weak_Password_Change_or_Reset_Functionalities.md)

#### 4.4.10 [Тестирование аутентификации в альтернативных каналах](4-Web_Application_Security_Testing/04-Authentication_Testing/10-Testing_for_Weaker_Authentication_in_Alternative_Channel.md)

#### 4.4.11 [Тестирование мультифакторной аутентификации (MFA)](4-Web_Application_Security_Testing/04-Authentication_Testing/11-Testing_Multi-Factor_Authentication.md)

### 4.5 [Тестирование авторизации](4-Web_Application_Security_Testing/05-Authorization_Testing/README.md)

#### 4.5.1 [Тестирование включения файлов при обходе каталогов](4-Web_Application_Security_Testing/05-Authorization_Testing/01-Testing_Directory_Traversal_File_Include.md)

#### 4.5.2 [Тестирование обхода схемы авторизации](4-Web_Application_Security_Testing/05-Authorization_Testing/02-Testing_for_Bypassing_Authorization_Schema.md)

#### 4.5.3 [Тестирование повышения привилегий](4-Web_Application_Security_Testing/05-Authorization_Testing/03-Testing_for_Privilege_Escalation.md)

#### 4.5.4 [Тестирование небезопасных прямых ссылок на объекты (IDOR)](4-Web_Application_Security_Testing/05-Authorization_Testing/04-Testing_for_Insecure_Direct_Object_References.md)

#### 4.5.5 [Тестирование уязвимостей в OAuth](4-Web_Application_Security_Testing/05-Authorization_Testing/05-Testing_for_OAuth_Weaknesses.md)

##### 4.5.5.1 [Тестирование уязвимостей сервера авторизации OAuth](4-Web_Application_Security_Testing/05-Authorization_Testing/05.1-Testing_for_OAuth_Authorization_Server_Weaknesses.md)

##### 4.5.5.2 [Тестирование уязвимостей клиента OAuth](4-Web_Application_Security_Testing/05-Authorization_Testing/05.2-Testing_for_OAuth_Client_Weaknesses.md)

### 4.6 [Тестирование управления сессиями](4-Web_Application_Security_Testing/06-Session_Management_Testing/README.md)

#### 4.6.1 [Тестирование схемы управления сессиями](4-Web_Application_Security_Testing/06-Session_Management_Testing/01-Testing_for_Session_Management_Schema.md)

#### 4.6.2 [Тестирование атрибутов Cookie](4-Web_Application_Security_Testing/06-Session_Management_Testing/02-Testing_for_Cookies_Attributes.md)

#### 4.6.3 [Тестирование фиксации сессии](4-Web_Application_Security_Testing/06-Session_Management_Testing/03-Testing_for_Session_Fixation.md)

#### 4.6.4 [Тестирование незащищённых параметров сессии](4-Web_Application_Security_Testing/06-Session_Management_Testing/04-Testing_for_Exposed_Session_Variables.md)

#### 4.6.5 [Тестирование подделки межсайтовых запросов (CSRF)](4-Web_Application_Security_Testing/06-Session_Management_Testing/05-Testing_for_Cross_Site_Request_Forgery.md)

#### 4.6.6 [Тестирование выхода из системы](4-Web_Application_Security_Testing/06-Session_Management_Testing/06-Testing_for_Logout_Functionality.md)

#### 4.6.7 [Тестирование тайм-аута сессии](4-Web_Application_Security_Testing/06-Session_Management_Testing/07-Testing_Session_Timeout.md)

#### 4.6.8 [Тестирование «пазла» сессии](4-Web_Application_Security_Testing/06-Session_Management_Testing/08-Testing_for_Session_Puzzling.md)

#### 4.6.9 [Тестирование перехвата сессии](4-Web_Application_Security_Testing/06-Session_Management_Testing/09-Testing_for_Session_Hijacking.md)

#### 4.6.10 [Тестирование JWT](4-Web_Application_Security_Testing/06-Session_Management_Testing/10-Testing_JSON_Web_Tokens.md)

### 4.7 [Тестирование контроля входных данных](4-Web_Application_Security_Testing/07-Input_Validation_Testing/README.md)

#### 4.7.1 [Тестирование отражённых межсайтовых скриптов (Reflected XSS)](4-Web_Application_Security_Testing/07-Input_Validation_Testing/01-Testing_for_Reflected_Cross_Site_Scripting.md)

#### 4.7.2 [Тестирование хранимых межсайтовых скриптов (Stored XSS)](4-Web_Application_Security_Testing/07-Input_Validation_Testing/02-Testing_for_Stored_Cross_Site_Scripting.md)

#### 4.7.3 [Тестирование подделки методов HTTP](4-Web_Application_Security_Testing/07-Input_Validation_Testing/03-Testing_for_HTTP_Verb_Tampering.md)

#### 4.7.4 [Тестирование «загрязнения» HTTP-параметров (HPP)](4-Web_Application_Security_Testing/07-Input_Validation_Testing/04-Testing_for_HTTP_Parameter_Pollution.md)

#### 4.7.5 [Тестирование SQL-инъекций](4-Web_Application_Security_Testing/07-Input_Validation_Testing/05-Testing_for_SQL_Injection.md)

##### 4.7.5.1 [Тестирование Oracle](4-Web_Application_Security_Testing/07-Input_Validation_Testing/05.1-Testing_for_Oracle.md)

##### 4.7.5.2 [Тестирование MySQL](4-Web_Application_Security_Testing/07-Input_Validation_Testing/05.2-Testing_for_MySQL.md)

##### 4.7.5.3 [Тестирование MS SQL Server](4-Web_Application_Security_Testing/07-Input_Validation_Testing/05.3-Testing_for_SQL_Server.md)

##### 4.7.5.4 [Тестирование PostgreSQL](4-Web_Application_Security_Testing/07-Input_Validation_Testing/05.4-Testing_PostgreSQL.md)

##### 4.7.5.5 [Тестирование MS Access](4-Web_Application_Security_Testing/07-Input_Validation_Testing/05.5-Testing_for_MS_Access.md)

##### 4.7.5.6 [Тестирование NoSQL-инъекций](4-Web_Application_Security_Testing/07-Input_Validation_Testing/05.6-Testing_for_NoSQL_Injection.md)

##### 4.7.5.7 [Тестирование ORM-инъекций](4-Web_Application_Security_Testing/07-Input_Validation_Testing/05.7-Testing_for_ORM_Injection.md)

##### 4.7.5.8 [Тестирование на стороне клиента](4-Web_Application_Security_Testing/07-Input_Validation_Testing/05.8-Testing_for_Client-side.md)

#### 4.7.6 [Тестирование LDAP-инъекций](4-Web_Application_Security_Testing/07-Input_Validation_Testing/06-Testing_for_LDAP_Injection.md)

#### 4.7.7 [Тестирование XML-инъекций](4-Web_Application_Security_Testing/07-Input_Validation_Testing/07-Testing_for_XML_Injection.md)

#### 4.7.8 [Тестирование SSI-инъекций](4-Web_Application_Security_Testing/07-Input_Validation_Testing/08-Testing_for_SSI_Injection.md)

#### 4.7.9 [Тестирование XPath-инъекций](4-Web_Application_Security_Testing/07-Input_Validation_Testing/09-Testing_for_XPath_Injection.md)

#### 4.7.10 [Тестирование IMAP/SMTP-инъекций](4-Web_Application_Security_Testing/07-Input_Validation_Testing/10-Testing_for_IMAP_SMTP_Injection.md)

#### 4.7.11 [Тестирование инъекции кода](4-Web_Application_Security_Testing/07-Input_Validation_Testing/11-Testing_for_Code_Injection.md)

##### 4.7.11.1 [Тестирование включения файлов (LFI/RFI)](4-Web_Application_Security_Testing/07-Input_Validation_Testing/11.1-Testing_for_File_Inclusion.md)

#### 4.7.12 [Тестирование инъекции команд ОС](4-Web_Application_Security_Testing/07-Input_Validation_Testing/12-Testing_for_Command_Injection.md)

#### 4.7.13 [Тестирование инъекций в строке форматирования](4-Web_Application_Security_Testing/07-Input_Validation_Testing/13-Testing_for_Format_String_Injection.md)

#### 4.7.14 [Тестирование инкубационных уязвимостей](4-Web_Application_Security_Testing/07-Input_Validation_Testing/14-Testing_for_Incubated_Vulnerability.md)

#### 4.7.15 [Тестирование HTTP Splitting/Smuggling](4-Web_Application_Security_Testing/07-Input_Validation_Testing/15-Testing_for_HTTP_Splitting_Smuggling.md)

#### 4.7.16 [Тестирование входящих HTTP-запросов](4-Web_Application_Security_Testing/07-Input_Validation_Testing/16-Testing_for_HTTP_Incoming_Requests.md)

#### 4.7.17 [Тестирование инъекций в заголовке Host](4-Web_Application_Security_Testing/07-Input_Validation_Testing/17-Testing_for_Host_Header_Injection.md)

#### 4.7.18 [Тестирование инъекции шаблона на стороне сервера (SSTI)](4-Web_Application_Security_Testing/07-Input_Validation_Testing/18-Testing_for_Server-side_Template_Injection.md)

#### 4.7.19 [Тестирование подделки запросов на стороне сервера (SSRF)](4-Web_Application_Security_Testing/07-Input_Validation_Testing/19-Testing_for_Server-Side_Request_Forgery.md)

#### 4.7.20 [Тестирование массового переназначения](4-Web_Application_Security_Testing/07-Input_Validation_Testing/20-Testing_for_Mass_Assignment.md)

### 4.8 [Обработка ошибок](4-Web_Application_Security_Testing/08-Testing_for_Error_Handling/README.md)

#### 4.8.1 [Тестирование некорректной обработки ошибок](4-Web_Application_Security_Testing/08-Testing_for_Error_Handling/01-Testing_For_Improper_Error_Handling.md)

#### 4.8.2 [Тестирование трассировки стека](4-Web_Application_Security_Testing/08-Testing_for_Error_Handling/02-Testing_for_Stack_Traces.md)

### 4.9 [Криптография](4-Web_Application_Security_Testing/09-Testing_for_Weak_Cryptography/README.md)

#### 4.9.1 [Тестирование безопасности транспортного уровня (TLS)](4-Web_Application_Security_Testing/09-Testing_for_Weak_Cryptography/01-Testing_for_Weak_Transport_Layer_Security.md)

#### 4.9.2 [Тестирование оракула дополнений](4-Web_Application_Security_Testing/09-Testing_for_Weak_Cryptography/02-Testing_for_Padding_Oracle.md)

#### 4.9.3 [Тестирование передачи чувствительной информации по незашифрованным каналам](4-Web_Application_Security_Testing/09-Testing_for_Weak_Cryptography/03-Testing_for_Sensitive_Information_Sent_via_Unencrypted_Channels.md)

#### 4.9.4 [Тестирование шифрования](4-Web_Application_Security_Testing/09-Testing_for_Weak_Cryptography/04-Testing_for_Weak_Encryption.md)

### 4.10 [Тестирование бизнес-логики](4-Web_Application_Security_Testing/10-Business_Logic_Testing/README.md)

#### 4.10.0 [Введение в бизнес-логику](4-Web_Application_Security_Testing/10-Business_Logic_Testing/00-Introduction_to_Business_Logic.md)

#### 4.10.1 [Тестирование форматно-логического контроля данных](4-Web_Application_Security_Testing/10-Business_Logic_Testing/01-Test_Business_Logic_Data_Validation.md)

#### 4.10.2 [Тестирование способности подделывать запросы](4-Web_Application_Security_Testing/10-Business_Logic_Testing/02-Test_Ability_to_Forge_Requests.md)

#### 4.10.3 [Тестирование проверки целостности](4-Web_Application_Security_Testing/10-Business_Logic_Testing/03-Test_Integrity_Checks.md)

#### 4.10.4 [Тестирование времени обработки](4-Web_Application_Security_Testing/10-Business_Logic_Testing/04-Test_for_Process_Timing.md)

#### 4.10.5 [Тестирование ограничений на количество раз, которое функция может быть выполнена](4-Web_Application_Security_Testing/10-Business_Logic_Testing/05-Test_Number_of_Times_a_Function_Can_Be_Used_Limits.md)

#### 4.10.6 [Тестирование обхода потока операций](4-Web_Application_Security_Testing/10-Business_Logic_Testing/06-Testing_for_the_Circumvention_of_Work_Flows.md)

#### 4.10.7 [Тестирование защиты от нецелевого использования приложений](4-Web_Application_Security_Testing/10-Business_Logic_Testing/07-Test_Defenses_Against_Application_Misuse.md)

#### 4.10.8 [Тестирование загрузки файлов непредусмотренных типов](4-Web_Application_Security_Testing/10-Business_Logic_Testing/08-Test_Upload_of_Unexpected_File_Types.md)

#### 4.10.9 [Тестирование загрузки вредоносных файлов](4-Web_Application_Security_Testing/10-Business_Logic_Testing/09-Test_Upload_of_Malicious_Files.md)

#### 4.10.10 [Тестирование платёжных функций](4-Web_Application_Security_Testing/10-Business_Logic_Testing/10-Test-Payment-Functionality.md)

### 4.11 [Тестирование на стороне клиента](4-Web_Application_Security_Testing/11-Client-side_Testing/README.md)

#### 4.11.1 [Тестирование XSS на основе DOM](4-Web_Application_Security_Testing/11-Client-side_Testing/01-Testing_for_DOM-based_Cross_Site_Scripting.md)

##### 4.11.1.1 [Тестирование «само-XSS» на основе DOM](4-Web_Application_Security_Testing/11-Client-side_Testing/01.1-Testing_for_Self_DOM_Based_Cross_Site_Scripting.md)

#### 4.11.2 [Тестирование выполнения JavaScript](4-Web_Application_Security_Testing/11-Client-side_Testing/02-Testing_for_JavaScript_Execution.md)

#### 4.11.3 [Тестирование HTML-инъекции](4-Web_Application_Security_Testing/11-Client-side_Testing/03-Testing_for_HTML_Injection.md)

#### 4.11.4 [Тестирование перенаправления URL на стороне клиента](4-Web_Application_Security_Testing/11-Client-side_Testing/04-Testing_for_Client-side_URL_Redirect.md)

#### 4.11.5 [Тестирование CSS-инъекций](4-Web_Application_Security_Testing/11-Client-side_Testing/05-Testing_for_CSS_Injection.md)

#### 4.11.6 [Тестирование манипулирования ресурсами на стороне клиента](4-Web_Application_Security_Testing/11-Client-side_Testing/06-Testing_for_Client-side_Resource_Manipulation.md)

#### 4.11.7 [Тестирование Cross Origin Resource Sharing (CORS)](4-Web_Application_Security_Testing/11-Client-side_Testing/07-Testing_Cross_Origin_Resource_Sharing.md)

#### 4.11.8 [Тестирование межсайтовых Flash](4-Web_Application_Security_Testing/11-Client-side_Testing/08-Testing_for_Cross_Site_Flashing.md)

#### 4.11.9 [Тестирование перехвата клика (Clickjacking)](4-Web_Application_Security_Testing/11-Client-side_Testing/09-Testing_for_Clickjacking.md)

#### 4.11.10 [Тестирование WebSockets](4-Web_Application_Security_Testing/11-Client-side_Testing/10-Testing_WebSockets.md)

#### 4.11.11 [Тестирование обмена web-сообщениями](4-Web_Application_Security_Testing/11-Client-side_Testing/11-Testing_Web_Messaging.md)

#### 4.11.12 [Тестирование хранилищ браузера](4-Web_Application_Security_Testing/11-Client-side_Testing/12-Testing_Browser_Storage.md)

#### 4.11.13 [Тестирование включения межсайтовых скриптов (XSSI)](4-Web_Application_Security_Testing/11-Client-side_Testing/13-Testing_for_Cross_Site_Script_Inclusion.md)

#### 4.11.14 [Тестирование Reverse Tabnabbing](4-Web_Application_Security_Testing/11-Client-side_Testing/14-Testing_for_Reverse_Tabnabbing.md)

### 4.12 [Тестирование API](4-Web_Application_Security_Testing/12-API_Testing/README.md)

#### 4.12.1 [Тестирование GraphQL](4-Web_Application_Security_Testing/12-API_Testing/01-Testing_GraphQL.md)

## 5. [Отчётность](5-Reporting/README.md)

### 5.1 [Структура отчёта](5-Reporting/01-Reporting_Structure.md)

### 5.2 [Схемы наименования уязвимостей](5-Reporting/02-Naming_Schemes.md)

## Приложение A. [Ресурсы по инструментам тестирования](6-Appendix/A-Testing_Tools_Resource.md)

## Приложение B. [Рекомендуется к прочтению](6-Appendix/B-Suggested_Reading.md)

## Приложение C. [Векторы для фаззинга](6-Appendix/C-Fuzz_Vectors.md)

## Приложение D. [Закодированные инъекции](6-Appendix/D-Encoded_Injection.md)

## Приложение E. [История WSTG](6-Appendix/E-History.md)

## Приложение F. [Использование Инструментов разработчика в браузерах](6-Appendix/F-Leveraging_Dev_Tools.md)
