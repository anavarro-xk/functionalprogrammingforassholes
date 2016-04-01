# Promises
****
### Que es una promesa?
Un promesa es un valor(es) retornado despues de que una operación es finalizada, viendolo desde el punto de vista humano podemos entender el concepto de promesa desde la perspectiva de Javascript, cada promesa es un pacto entre dos o mas partes en donde una de ellas debe entrega algo a cambio. Si una promesa no se ha cumplido permanece en el estado **unfilled** , sin embargo cuando se ha realizo dicha promesa, pasa al estado **fullfilled**. Si la promesa no es cumplida como se esperaba, se dice que ha fallado.

Ahora... que es una promesa segun la definición oficial:
> _Una promesa es un objeto o una función con un metodo "then" cuyo comportamiento se ajusta a esta especificación y representa el resultado eventual de una operación asincrónica_

[La fuente de esta deficinión la encuentras aqui en el slide numero 21](http://www.slideshare.net/wookieb/callbacks-promises-generators-asynchronous-javascript)

## Conceptos que ayudaran a entender las promesas

* **Future, promise, and delay:**
Son herramientas utilizadas normalmente en lenguajes de programación concurrente, a menudo son usadas indistintamente pero hay algunas diferencias en la implementación de estos terminos. Future puede ser usado para definir una tarea y colocarla en otro hilo sin necesitar el resultado inmediatamente, promise permite expresar que espera un resultado sin tener definida una tarea, promise puede actuar como contenedor y hacer uso de future, otra diferencia es que future es referenciado como "read-only" y promise como "writeable", y delay permite definir una tarea sin tener que ejecutarla o requerir el resultado inmediatamente.

* **Promise pipelining:**
Consiste en concatenar varias funciones _then_ y hacer que una promesa tome como entrada el resultado de la promesa previa a esta.
Ejemplo:
```javascript
var p2 = new Promise(function(resolve, reject) {
  resolve(1);
});

p2.then(function(value) {
  console.log(value); // 1
  return value + 1;
}).then(function(value) {
  console.log(value); // 2
});

p2.then(function(value) {
  console.log(value); // 1
});
```
* **Estados de una promesa**
Las promesas estan basadas en tres estados. cada estado tiene un un significado y puede ser usado para manejar un cierto nivel de resultados segun la necesidad, los tres estados de una promesa son los siguientes:
    * **Pending:** Este es el estado incial de una promesa.
    * **Fullfilled:** Este es es el estado de una promesa representando un operación existosa.
    * **Rejected:** Este es el estado de una promesa representando una operación fallida.

Una vez una promesa es _fullfilled_ o _rejected_, es "inmutable"(es decir, nunca puede cambiar a otro estado)

* **Compatibilidad entre navegadores:**
Muchos navegadores modernos soportan promesas pero no todos, una practica referencia de que navegadores lo soportan es dada segun el dispositivo:
    * Compatibilidad con equipos de escritorios:

    |**Feature**  | **Chrome** | **Firefox** | **IE**                               | **Opera** | **Safari** |
    |-------------|------------|-------------|--------------------------------------|-----------|------------|
    |Basic support|36          |31           |Not supported till IE11. Added in Edge|27         |8           |
    * Compatibilidad con dispositivos móbiles:

    | **Feature** |**Android** |**Firefox Mobile (Gecko)** | **IE Mobile** | **Opera Mobile** | **Safari Mobile** | **Chrome for Android** |
    |-------------|------------|---------------------------|---------------|------------------|-------------------|------------------------|
    |Basic support| 4.4.4      |31                         |Edge           |Not supported     |Not supported      |42                      |
