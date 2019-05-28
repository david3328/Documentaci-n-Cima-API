# Base de Datos

Para realizar la conexión a la base de datos, utilizamos la librería [pg-promise](https://www.npmjs.com/package/pg-promise), puedes revisar su documentación [aquí.](http://vitaly-t.github.io/pg-promise/)

Simplemente requerimos la librería con la siguiente línea de código 
```js
const pgp = require("pg-promise")();
```
Creamos la cadena de conexión:

```js
const cn = "postgres://user-name:user-password@host:port/database-name";
```

Una alternativa a la cadena de conexión es, crear un objeto de conexión:

```js
const cn = {
    host: 'localhost',
    port: 5432,
    database: 'my-database-name',
    user: 'user-name',
    password: 'user-password'
};
```

Realizamos la conexión y la exportamos para usarlo en los controladores y/o servicios que necesiten alguna consulta la base de datos.

```js
const db = pgp(cn);

module.exports = db;
```

## Utilización de la base de datos

1. Importamos la  conexión con el siguiente código:

```js
const db = require('PATH_RELATIVO')
```
**PATH_RELATIVO:** Es la ruta relativa a donde se encuentra el archivo db.js

2. En un controlador tendríamos algo como esto:
```js
exports.MiControlador = (require,response)=>{
    let parametro1 = req.body.parametro1;
    
    // Podríamos tener una consulta 
    let query = `SELECT * FROM tabla WHERE parametro = ${parametro1}`;

    db.any(query)
    .then(respuesta=>console.log(respuesta))
    .catch(error=>console.log(error))
}
```

En el ejemplo anterior estamos ejecutando una consulta que devuelve varios resultados. Veamos más casos.

* Cuando la consulta devuelve varios registros usamos ```db.any(consulta)```
* Cuando la consulta devuelve un solo registro usamos ```db.one(consulta)```
* Cuando la consulta no devuelve nada usamos ```db.none(consulta)``` *(se puede aplicar a insert update o delete)*

Para estos casos la ejecución devuelve una promesa que se puede resolver o traer un error, por ejemplo: 
```js
db.one(consulta) // aplica para none y any
.then(respuesta=>{
    //acá me trae el registro de ser el caso
    console.log(respuesta)//muestroa la respuesta

    //si estoy creando un servicio,devuelvo la respuesta así:

    response.json(respuesta);
})
.catch(error=>{
    //acá me trae el error 
    console.log(error)//muestro el error

    //si estoy creando un servicio, devuelvo una respuesta así
    response.status(500).json(error)
})
```

* Para ejecutar una funcion ya creada en nuestra base de datos usamos:

    * ```db.func('nombre_funcion')``` cuando no hay parametros que enviar a la función.
    * ```db.func('nombre_funcion',parametro)``` cuando la función recibe un solo parametro.
    * ```db.func('nombre_funcion',[parmetro1,parametro2,parametro3])``` cuando la función reciba más de un parametro. *(para este caso 3 parametros)*

Para culquiera de estos casos la función es una promesa que se resuelve de la siguiente manera:

```js
db.func('mi_funcion') // aplica para los tres casos
.then(respuesta=>{
    //ahora la respuesta es un arreglo con un solo objeto de esta forma 

    /*
        repuesta:[
            mi_funcion: //acá esta el resultado de la función
        ]
    */

    
    //para obtener la respuesta de la función lo guardamos en una variable

    respuesta = respuesta[0].mi_funcion;

    //mi_funcion es el nombre de la funcion


    //si estoy creando un servicio,devuelvo la respuesta así:

    response.json(respuesta);
})
.catch(error=>{
    //acá me trae el error 
    console.log(error)//muestro el error

    //si estoy creando un servicio, devuelvo una respuesta así
    response.status(500).json(error)
})
```