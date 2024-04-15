---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Тестирование шифрования

|ID          |
|------------|
|WSTG-CRYP-04|

## Обзор

Некорректное использование алгоритмов шифрования может привести к разглашению конфиденциальной информации, утечке ключей, нарушению аутентификации, незащищённым сессиям и атакам подмены (англ.: spoofing). Существуют алгоритмы шифрования и хэширования, известные своей нестойкостью, и поэтому теперь не рекомендуются, например, MD5 и RC4.

В дополнение к выбору стойких алгоритмов шифрования или хэширования, для уровня защиты также имеет значение корректное использование параметров. Например, режим ECB (электронной кодовой книги) не рекомендуется при асимметричном шифровании.

## Задачи тестирования

- Дать рекомендации по выявлению использования и реализации нестойкого шифрования или хэширования.

## Как тестировать

### Базовый чек-лист по безопасности

- При использовании AES128 или AES256 вектор инициализации (IV) должен быть случайным и непредсказуемым. См. пункт Continuous random number generator tests в разделе 4.9.2 [FIPS 140-2, Требования безопасности для криптографических модулей](https://csrc.nist.gov/publications/detail/fips/140/2/final). Например, `java.util.Random` в Java считается некриптостойким генератором псевдослучайных чисел (ГПСЧ); и вместо него следует использовать `java.security.SecureRandom`.
- Для асимметричного шифрования используйте криптографию на эллиптических кривых (ECC) с безопасной кривой, например, `Curve25519`.
    - Если использование ECC недоступно, используйте шифрование RSA с длиной ключа как минимум 2048 бит.
- При использовании RSA в подписи рекомендуется дополнение PSS (англ.: RSA Signature Scheme with Appendix-Probabilistic Signature Scheme).
- Не должны использоваться нестойкие алгоритмы хэширования/шифрования, такие как MD5, RC4, DES, Blowfish, SHA1. 
- Недостаточная длина ключа: 1024 бита для RSA или DSA, 160 бит для ECDSA (на эллиптических кривых), 80/112 бит в 2TDEA (два ключа в тройном DES)
- Требования к минимальной длине ключа:

```text
Обмен ключами: обмен ключами Диффи-Хеллмана как минимум 2048 бит
Целостность сообщения: HMAC-SHA2
Хэш сообщения: SHA2 256 бит
Асимметричное шифрование: RSA 2048 бит
Алгоритм с симметричным ключом: AES 128 бит
Хэширование пароля: PBKDF2, Scrypt, Bcrypt
ECDH, ECDSA: 256 бит
```

- Не следует использовать режим CBC в SSH.
- При использовании алгоритма симметричного шифрования не следует использовать режим ECB (электронной кодовой книги).
- При использовании PBKDF2 для хэширования пароля, рекомендуется, чтобы количество итераций было больше 10000. [NIST](https://pages.nist.gov/800-63-3/sp800-63b.html#sec5) также предлагает не менее 10 тыс. итераций хэш-функции. Кроме того, в PBKDF2 запрещено использовать хэш-функцию MD5, например PBKDF2WithHmacMD5.

### Анализ исходного кода

- Ищите следующие ключевые слова, чтобы определить использование нестойких алгоритмов: `MD4, MD5, RC4, RC2, DES, Blowfish, SHA-1, ECB`

- Для реализаций на Java следующий API касается шифрования. Проанализируйте параметры шифрования. Например:

```java
SecretKeyFactory(SecretKeyFactorySpi keyFacSpi, Provider provider, String algorithm)
SecretKeySpec(byte[] key, int offset, int len, String algorithm)
Cipher c = Cipher.getInstance("DES/CBC/PKCS5Padding");
```

- Для шифрования RSA предлагаются следующие режимы дополнения:

```text
RSA/ECB/OAEPWithSHA-1AndMGF1Padding (2048)
RSA/ECB/OAEPWithSHA-256AndMGF1Padding (2048)
```

- Ищите `ECB`, его нельзя использовать в дополнении.
- Проверьте, используются ли разные векторы инициализации (IV).

```java
// для каждого шифрования используются разные значения IV
byte[] newIv = ...;
s = new GCMParameterSpec(s.getTLen(), newIv);
cipher.init(..., s);
...
```

- Найдите `IvParameterSpec`, убедитесь, что каждый раз генерируется новое значение IV и они случайны.

```java
 IvParameterSpec iv = new IvParameterSpec(randBytes);
 SecretKeySpec skey = new SecretKeySpec(key.getBytes(), "AES");
 Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
 cipher.init(Cipher.ENCRYPT_MODE, skey, iv);
```

- В Java найдите MessageDigest, чтобы проверить, не используется ли небезопасный алгоритм хеширования (MD5 или CRC). Например:

`MessageDigest md5 = MessageDigest.getInstance("MD5");`

- Для подписи не следует использовать SHA1 и MD5. Например:

`Signature sig = Signature.getInstance("SHA1withRSA");`

- Найдите `PBKDF2`. Для генерации хэша пароля предлагается использовать `PBKDF2`. Просмотрите параметры для формирования хэша `PBKDF2`.

Итерации должны быть больше **10000**, и значение **salt** должно формироваться **случайным образом**.

```java
private static byte[] pbkdf2(char[] password, byte[] salt, int iterations, int bytes)
    throws NoSuchAlgorithmException, InvalidKeySpecException
  {
       PBEKeySpec spec = new PBEKeySpec(password, salt, iterations, bytes * 8);
       SecretKeyFactory skf = SecretKeyFactory.getInstance(PBKDF2_ALGORITHM);
       return skf.generateSecret(spec).getEncoded();
   }
```

- "Зашитая" в код конфиденциальная информация:

```text
Ключевые слова, связанные с пользователями: name, root, su, sudo, admin, superuser, login, username, uid
Ключевые слова, связанные с ключами: public key, AK, SK, secret key, private key, passwd, password, pwd, share key, shared key, crypto, base64
Другие распространённые чувствительные ключевые слова: sysadmin, root, privilege, pass, key, code, master, admin, uname, session, token, Oauth, privatekey, shared secret
```

## Инструменты

- Сканеры уязвимостей, такие как Nessus, NMAP (NSE-скрипты) или OpenVAS, могут сканировать на предмет использования нестойкого шифрования по таким протоколам, как SNMP, TLS, SSH, SMTP и т.д.
- Инструменты статического анализа кода, например klocwork, Fortify, Coverity, CheckMarx, в следующих случаях:

    - [CWE-261: Weak Encoding for Password](https://cwe.mitre.org/data/definitions/261.html)
    - [CWE-323: Reusing a Nonce, Key Pair in Encryption](https://cwe.mitre.org/data/definitions/323.html)
    - [CWE-326: Inadequate Encryption Strength](https://cwe.mitre.org/data/definitions/326.html)
    - [CWE-327: Use of a Broken or Risky Cryptographic Algorithm](https://cwe.mitre.org/data/definitions/327.html)
    - [CWE-328: Reversible One-Way Hash](https://cwe.mitre.org/data/definitions/328.html)
    - [CWE-329: Not Using a Random IV with CBC Mode](https://cwe.mitre.org/data/definitions/329.html)
    - [CWE-330: Use of Insufficiently Random Values](https://cwe.mitre.org/data/definitions/330.html)
    - [CWE-347: Improper Verification of Cryptographic Signature](https://cwe.mitre.org/data/definitions/347.html)
    - [CWE-354: Improper Validation of Integrity Check Value](https://cwe.mitre.org/data/definitions/354.html)
    - [CWE-547: Use of Hard-coded, Security-relevant Constants](https://cwe.mitre.org/data/definitions/547.html)
    - [CWE-780: Use of RSA Algorithm without OAEP](https://cwe.mitre.org/data/definitions/780.html)

## Ссылки

- [NIST FIPS Standards](https://csrc.nist.gov/publications/fips)
- [Wikipedia: Initialization Vector](https://en.wikipedia.org/wiki/Initialization_vector)
- [Secure Coding - Generating Strong Random Numbers](https://www.securecoding.cert.org/confluence/display/java/MSC02-J.+Generate+strong+random+numbers)
- [Оптимальное асимметричное шифрование с дополнением](https://ru.wikipedia.org/wiki/%D0%9E%D0%BF%D1%82%D0%B8%D0%BC%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D0%B5_%D0%B0%D1%81%D0%B8%D0%BC%D0%BC%D0%B5%D1%82%D1%80%D0%B8%D1%87%D0%BD%D0%BE%D0%B5_%D1%88%D0%B8%D1%84%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5_%D1%81_%D0%B4%D0%BE%D0%BF%D0%BE%D0%BB%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5%D0%BC)
- [Cryptographic Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html)
- [Password Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html)
- [Secure Coding - Do not use insecure or weak cryptographic algorithms](https://www.securecoding.cert.org/confluence/display/java/MSC61-J.+Do+not+use+insecure+or+weak+cryptographic+algorithms)
- [Insecure Randomness](https://owasp.org/www-community/vulnerabilities/Insecure_Randomness)
- [Insufficient Entropy](https://owasp.org/www-community/vulnerabilities/Insufficient_Entropy)
- [Insufficient Session-ID Length](https://owasp.org/www-community/vulnerabilities/Insufficient_Session-ID_Length)
- [Using a broken or risky cryptographic algorithm](https://owasp.org/www-community/vulnerabilities/Using_a_broken_or_risky_cryptographic_algorithm)
- [Javax.crypto.cipher API](https://docs.oracle.com/javase/8/docs/api/javax/crypto/Cipher.html)
- ISO/IEC 18033-1:2021 – Encryption Algorithms
- ISO/IEC 18033-2: Asymmetric ciphers
- ISO/IEC 18033-3: Block ciphers
- ISO/IEC 18033-4: Stream ciphers
- ISO/IEC 18033-5: Identity-based ciphers
- ISO/IEC 18033-6: Homomorphic encryption
- ISO/IEC 18033-7: Tweakable block ciphers
