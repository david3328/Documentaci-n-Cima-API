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