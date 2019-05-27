
# Tareas Programadas
## 1. Librería Cron
Para realizar tareas programadas se utiliza la librería [CronJs](https://www.npmjs.com/package/cron), el cual puedes revisar la [Documentación](https://github.com/kelektiv/node-cron).

## 2. Crear un tarea
Para crear una tarea debemos ir al archivo **cron.js**. Ubícandonos en la raíz del proyecto vamos a la siguiente ruta: 

```
src/services/cron.js
```
Encontraremos tareas ya realizadas y el llamado a la librería **cron.js** en la siguiente línea de código: ```var CronJob = require('cron').CronJob``` por lo que solo debemos crear nuestra tarea de la siguiente manera: 

```js
const nuevaTarea = new CronJob('* * * * * *',function(){
    // Ejecutamos el código
},null,true);
```
El código anterior al no darle tiempo y solo estar con asteriscos se ejecuta cada segundo. 

Cada asterísco de izquierda a derecha representa:
* Segundos: 0-59
* Minutos: 0-59
* Horas: 0-23
* Días del mes: 1-31
* Meses: 0-11 (Ene-Dic)
* Día de la Semana: 0-6 (Dom-Sab)

Por ejemplo:

```js
const evento = new CronJob('0 50 6 * * *',function() {
    console.log('Me ejecuto todos los días a las 06:50:00');
},null,true);
```

> El formato es de 24 horas, si queremos ejecutar algo a las 8:50:30 pm sería '30 50 20 * * *'

Puedes revisar los [Ejemplos](https://github.com/kelektiv/node-cron/tree/master/examples) de la librería y/o revisar las [Expresiones de cron](https://crontab.guru/)

## 3. Ejecutar la tarea
En el paso anterior ya creamos nuestra tarea, pero ¿cómo hacemos para que se ejecute?, en la parte final exportamos una funcion que se autoejecuta:

```js
module.exports = function () {
  birthay.start();
  evento.start();
  proximosEventos.start();
}()
```

Simplemente colocamos nuestra función que hemos creado y llamados al método ```start()```, por ejemplo

```js
module.exports = function () {
  birthay.start();
  evento.start();
  proximosEventos.start();
  nuevaTarea.start() //Tarea creada en el paso anterior
}()
```