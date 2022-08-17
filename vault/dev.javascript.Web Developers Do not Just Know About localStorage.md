---
id: qwck0emd5tmgj7769vokyv3
title: Web Developers Do not Just Know About localStorage
desc: ""
updated: 1660778838099
created: 1660778410316
published: false
---

> https://medium.com/frontend-canteen/web-developers-dont-just-know-about-localstorage-2f37385bd8ad

## Cookies

An HTTP cookie (web cookie, browser cookie) is a small piece of data that a server sends to a user’s web browser. The browser may store the cookie and send it back to the same server with later requests. Typically, an HTTP cookie is used to tell if two requests come from the same browser — keeping a user logged in, for example. **It remembers stateful information for the stateless HTTP protocol.**

Cookies are mainly used for three purposes:

1. Session management: Logins, shopping carts, game scores, or anything else the server should remember.
2. Personalization: User preferences, themes, and other settings.
3. Tracking: Recording and analyzing user behavior.

```javascript
document.cookie = "name=bytefer";
document.cookie = "favorite_food=tripe";
alert(document.cookie);
// name=bytefer;favorite\_food=tripe
```

## localStorage

A form of persistent storage, meaning that data never expires unless it is manually purged. It stores data in the form of key-value pairs and saves the data to the corresponding database files according to the domain name. Compared to cookies, it can store larger data.

localStorage has these features:

1. The size is limited to 5MB ~10MB.
2. Share data between all tabs and windows of the same origin.
3. The data is only stored on the client side and does not communicate with the server.
4. The data is persistent and will not expire, and it still exists after restarting the browser.
5. Operations on data are synchronous.

## sessionStorage

Similar to the server-side session, sessionStorage is a session-level cache, and the data is cleared when the browser is closed. It should be noted that the scope of sessionStorage is at the **window level**, which means that sessionStorage data saved between different windows cannot be shared.

sessionStorage has these features:

1. The data of sessionStorage only exists in the current browser tab.
2. The data persists after a page refresh but is cleared when the browser tab is closed.
3. Have a unified API interface with localStorage.
4. Operations on data are synchronous.

## Web SQL

The Web SQL Database API is not actually part of the HTML5 specification, but a separate specification that introduces a set of APIs to manipulate client-side databases using SQL. It’s important to note that **HTML5 has abandoned Web SQL** databases.

Three core methods defined in the Web SQL Database specification:

1. openDatabase: Use an existing database or create a new database to create database objects.
2. transaction: Allows us to control the commit or rollback of the transaction depending on the situation.
3. executeSql: Used to execute SQL statements.

Features of Web SQL (compared to cookies, localStorage and sessionStorage):

1. Web SQL can facilitate object storage.
2. Web SQL supports transactions, which can facilitate data query and data processing operations.

```javascript
const db = openDatabase('mydb', '1.0', 'MyDB', 2 \* 1024 \* 1024);db.transaction(function (tx) {
 tx.executeSql('CREATE TABLE IF NOT EXISTS LOGS (id unique,
 log)');
 // Insert Data
 tx.executeSql('INSERT INTO LOGS (id, log) VALUES (1, "foobar")');
 tx.executeSql('INSERT INTO LOGS (id, log) VALUES (2, "logmsg")');
});
```

## IndexedDB

IndexedDB is a low-level API for client-side storage of large amounts of structured data, including files, and binary large objects. The API uses indexes to enable high-performance searches on this data. While Web Storage is useful for storing smaller amounts of data, it’s less useful for storing larger amounts of structured data. IndexedDB provides a solution.

IndexedDB has these features:

1. Large storage space: The storage space can reach hundreds of megabytes or more.
2. Support binary storage: it can store not only strings but also binary data
3. IndexedDB has the same origin restriction, each database can only be accessed under its own domain name, and cannot be accessed across domain names.
4. Support transaction type: The operations performed by IndexedDB will be grouped according to transactions. In a transaction, either all operations succeed or all operations fail.
5. Data operations are asynchronous: Operations performed with IndexedDB are performed asynchronously so as not to block the application.

```javascript
let dbName = "my_db";
let request = indexedDB.open(dbName, 2);
request.onerror = function (event) {
  // handle error
};
request.onupgradeneeded = function (event) {
  let db = event.target.result;
  let objectStore = db.createObjectStore("customers", {
    keyPath: "ssn",
  });
  objectStore.createIndex("name", "name", { unique: false });
  objectStore.createIndex("email", "email", { unique: true });
  objectStore.transaction.oncomplete = function (event) {
    let customerObjectStore = db
      .transaction("customers", "readwrite")
      .objectStore("customers");
    customerData.forEach(function (customer) {
      customerObjectStore.add(customer);
    });
  };
};
```

Here we only introduce some open source libraries. In fact, there are some other mature open source libraries, such as [lowdb](https://github.com/typicode/lowdb) (Local JSON Database), [Lovefield](https://github.com/google/lovefield) (Relational Database), [LokiJS](https://github.com/techfort/LokiJS) (NoSQL Database), etc. If you know other interesting projects, welcome to leave a message.
