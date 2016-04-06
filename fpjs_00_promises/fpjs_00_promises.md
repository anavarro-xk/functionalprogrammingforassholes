# Promises
****
### What is a promise?
A promise is a value or values returned when a operation is completed, seeing it at the human view, we can understand the concept of promise from the javascript perspective, each promise is an pact between two o more parts where one of them should delivery something back. If a promise has not completed this keep her state as **unfilled**, however when the promise is done this change to the **fullfilled** state. If a promise is not _fullfilled_ as we expect, it is said to have failed.

Now... what is a promise according the official definition:
>_Promise is an object or a function with a then method whose behavior confirms to this specification and represents the eventual result of an asynchronous operation._

Crystal clear, no?

The source of this definition is the slide 21 you can find [here](http://www.slideshare.net/wookieb/callbacks-promises-generators-asynchronous-javascript)

##Concpets that help you to underestand promises

* **Future, promise, and delay:**
Are tools normally used in concurrent programing languages, often used interchangeably. There is some core difference in implementing these terms. _Future_ can be used to define a task and set it on other thread without need the result inmediately, _promise_ allows express that  expect a result without have defined a task, _promise_ can act like container and use _future_, another difference is that _future_ is referenced as "read-only" and _promise_ as "writeable", and delay allows define a task without execute itself or require the result inmediatelly.

* **Promise pipelining:**
It consist in concatenate  various functions with  _then_ and make that a promise take as input the result of the previus promise.
Example:
```javascript
var quote = new Promise(function(resolve, reject) {
  resolve('No, ');
});

quote.then(function(value) {
  console.log(value); // No,
  return value + 'i am your father';
}).then(function(value) {
  console.log(value); //No, i am your father
});

```

* **Promise states:**
The promises are based in three states. Each state has a sense and can be used to manage the results according the need, the three states of a promise are the followings:
    * **Pending:** the initial state of a promise.
    * **Fullfilled:** represent a successfull operation.
    * **Rejected:** represent a failed operation.

Once a promise is _fullfilled_ o _reject_, is "inmutable" (this can´t change its state).

* **Browser support:**
Many modern browsers support promises but not all, an usefull reference of browser that support it is given according the device:
    * Compatibilidad con equipos de escritorios:

    |**Feature**  | **Chrome** | **Firefox** | **IE**                               | **Opera** | **Safari** |
    |-------------|------------|-------------|--------------------------------------|-----------|------------|
    |Basic support|36          |31           |Not supported till IE11. Added in Edge|27         |8           |
    * Compatibilidad con dispositivos móbiles:

    | **Feature** |**Android** |**Firefox Mobile (Gecko)** | **IE Mobile** | **Opera Mobile** | **Safari Mobile** | **Chrome for Android** |
    |-------------|------------|---------------------------|---------------|------------------|-------------------|------------------------|
    |Basic support| 4.4.4      |31                         |Edge           |Not supported     |Not supported      |42                      |
