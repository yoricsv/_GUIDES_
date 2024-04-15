---

layout: col-document
title: WSTG - Latest
tags: WSTG

---

{% include breadcrumb.html %}
# Тестирование хранилищ браузера

|ID          |
|------------|
|WSTG-CLNT-12|

## Обзор

Браузеры предоставляют разработчикам следующие механизмы хранения данных на стороне клиента для хранения и извлечения данных:

- Локальное хранилище
- Сессионное хранилище
- IndexedDB
- Web SQL (устарел)
- Cookie

Эти механизмы хранения можно просматривать и редактировать с помощью инструментов разработчика браузера, таких как [DevTools в Google Chrome](https://developer.chrome.com/docs/devtools/), [Storage Inspector в Firefox](https://developer.mozilla.org/ru/docs/Tools/Storage_Inspector) или [Web Inspector в Safari](https://support.apple.com/ru-ru/guide/safari-developer/devdf5596c56/mac).

Примечание: хотя кэш также является формой хранилища, он рассматривается в [другом разделе](../04-Authentication_Testing/06-Testing_for_Browser_Cache_Weaknesses.md), охватывающем его особенности и проблемы.

## Задачи тестирования

- Выяснить, хранит ли web-сайт чувствительные данные в хранилище на стороне клиента.
- Проверить обработку в коде объектов хранилища на наличие возможностей атак инъекции, таких как использование непроверенных входных данных или уязвимых библиотек.

## Как тестировать

### Локальное хранилище

`window.localStorage` — это глобальное свойство, которое реализует [API web-хранилища](https://developer.mozilla.org/ru/docs/Web/API/Web_Storage_API) и обеспечивает **постоянное** хранение пар ключ-значение в браузере.

И ключи, и значения могут быть только строками, поэтому любые нестроковые значения перед сохранением должны быть преобразованы в строки, что обычно делается с помощью [JSON.stringify](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify).

Записи в `localStorage` сохраняются даже при закрытии окна браузера, за исключением окон в режиме частного доступа/инкогнито.

Максимальная ёмкость хранилища `localStorage` зависит от браузера.

#### Вывод всех записей ключ-значение локального хранилища

```javascript
for (let i = 0; i < localStorage.length; i++) {
  const key = localStorage.key(i);
  const value = localStorage.getItem(key);
  console.log(`${key}: ${value}`);
}
```

### Сессионное хранилище

`window.sessionStorage`  — это глобальное свойство, которое реализует [API web-хранилища](https://developer.mozilla.org/ru/docs/Web/API/Web_Storage_API) и обеспечивает **эфемерное** хранение пар ключ-значение в браузере.

И ключи, и значения могут быть только строками, поэтому любые нестроковые значения перед сохранением должны быть преобразованы в строки, что обычно делается с помощью [JSON.stringify](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify).

Записи в `sessionStorage` называются эфемерными, поскольку они удаляются при закрытии вкладки/окна браузера.

Максимальная ёмкость хранилища `sessionStorage` зависит от браузера.

#### Вывод всех записей ключ-значение сессионного хранилища

```javascript
for (let i = 0; i < sessionStorage.length; i++) {
  const key = sessionStorage.key(i);
  const value = sessionStorage.getItem(key);
  console.log(`${key}: ${value}`);
}
```

### IndexedDB

IndexedDB — это транзакционная объектно-ориентированная база данных, предназначенная для структурированных данных. База данных IndexedDB может иметь несколько хранилищ объектов, и в каждом из них может быть несколько объектов.

В отличие от локального и сессионного хранилищ, IndexedDB может хранить больше, чем просто строки. Любые объекты, поддерживаемые [алгоритмом структурированного клонирования](https://developer.mozilla.org/ru/docs/Web/API/Web_Workers_API/Structured_clone_algorithm), могут храниться в IndexedDB.

Примером сложного объекта JavaScript, который может храниться в IndexedDB, но не в локальном/сессионном хранилище, является [CryptoKey](https://developer.mozilla.org/en-US/docs/Web/API/CryptoKey).

Из [рекомендации](https://www.w3.org/TR/WebCryptoAPI/) W3C по Web Crypto API [следует](https://www.w3.org/TR/WebCryptoAPI/#concepts-key-storage), что CryptoKey, который необходимо сохранить в браузере, хранился в IndexedDB. При тестировании web-страницы найдите CryptoKeys в IndexedDB и проверьте, не установлено ли для них значение `extractable: true`, тогда как должно быть `extractable: false` (т.е. убедитесь, что материал базового закрытого ключа во время криптографических операций не раскрывается.)

#### Вывод содержимого IndexedDB

```javascript
const dumpIndexedDB = dbName => {
  const DB_VERSION = 1;
  const req = indexedDB.open(dbName, DB_VERSION);
  req.onsuccess = function() {
    const db = req.result;
    const objectStoreNames = db.objectStoreNames || [];

    console.log(`[*] Database: ${dbName}`);

    Array.from(objectStoreNames).forEach(storeName => {
      const txn = db.transaction(storeName, 'readonly');
      const objectStore = txn.objectStore(storeName);

      console.log(`\t[+] ObjectStore: ${storeName}`);

      // Вывести все записи в objectStore с именем `storeName`
      objectStore.getAll().onsuccess = event => {
        const items = event.target.result || [];
        items.forEach(item => console.log(`\t\t[-] `, item));
      };
    });
  };
};

indexedDB.databases().then(dbs => dbs.forEach(db => dumpIndexedDB(db.name)));
```

### Web SQL

Web-SQL с 18 ноября 2010 г. признан устаревшим, поэтому разработчикам его использовать не рекомендуется.

### Cookie

Cookies — это механизм хранения пар ключ-значение, который в основном используется для управления сессией, но web-разработчики могут использовать его для хранения произвольных строковых данных.

Cookies подробно рассматриваются в сценарии [тестирования атрибутов Cookies](../06-Session_Management_Testing/02-Testing_for_Cookies_Attributes.md).

#### Вывести все Cookie

```javascript
console.log(window.document.cookie);
```

### Глобальный объект Window

Иногда web-разработчики инициализируют и поддерживают глобальное состояние, доступное только во время выполнения страницы, путём назначения настраиваемых атрибутов глобальному объекту `window`. Например:

```javascript
window.MY_STATE = {
  counter: 0,
  flag: false,
};
```

Любые данные, прикрепленные к объекту `window` будут потеряны при обновлении или закрытии страницы.

#### Вывести все записи в объекте Window

```javascript
(() => {
  // создаём iframe и добавляем его к телу, чтобы загрузить чистый объект window
  const iframe = document.createElement('iframe');
  iframe.style.display = 'none';
  document.body.appendChild(iframe);

  // получаем текущий список свойств window
  const currentWindow = Object.getOwnPropertyNames(window);

  // фильтруем список по свойствам, которые существуют в чистом window
  const results = currentWindow.filter(
    prop => !iframe.contentWindow.hasOwnProperty(prop)
  );

  // удаляем iframe
  document.body.removeChild(iframe);

  // записи ключ-значение, которые отличаются, пишем в журнал
  results.forEach(key => console.log(`${key}: ${window[key]}`));
})();
```

_(Это модифицированная версия данного [фрагмента](https://stackoverflow.com/a/17246535/3099132))_

### Цепочка атаки

После выявления любого из перечисленных выше векторов атаки может быть сформирована цепочка из различных типов атак на стороне клиента, например, [XSS на основе DOM](01-Testing_for_DOM-based_Cross_Site_Scripting.md).

## Меры защиты

Приложения должны хранить чувствительные данные на стороне сервера, а не клиента, безопасным образом и в соответствии с рекомендациями.

## Ссылки

- [Локальное хранилище](https://developer.mozilla.org/ru/docs/Web/API/Window/localStorage)
- [Сессионное хранилище](https://developer.mozilla.org/ru/docs/Web/API/Window/sessionStorage)
- [IndexedDB](https://developer.mozilla.org/ru/docs/Web/API/IndexedDB_API)
- [Web Crypto API: хранилище ключей](https://www.w3.org/TR/WebCryptoAPI/#concepts-key-storage)
- [Web SQL](https://www.w3.org/TR/webdatabase/)
- [Cookie](https://developer.mozilla.org/ru/docs/Web/HTTP/Cookies)

Дополнительные ресурсы OWASP по API Web-хранилища HTML5 см. в [Памятке по управлению сессиями](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html#html5-web-storage-api).
