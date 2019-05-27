# Envío de Correo
Para enviar correos electronicos, hacemos uso de la librería [nodemailer](https://nodemailer.com/about/)

El archivo donde se encuentra la función para enviar correo esta en
```
src/services/mail.js
```

Primero requerimos la librería
```js
const nodemailer = require('nodemailer');
```
Luego tenemos la función que nos crea un transportador

```js
const transporter = nodemailer.createTransport({
  service: 'gmail',
  auth: {
    user: 'correo-quien-envia',
    pass: 'constraseña-correo-quien-envia'
  },
  tls: {
    rejectUnauthorized: false
  }
})
```

Y finalmente exportamos el transportador

```js
module.exports = transporter
```

## 1. Uso del transportador

Primero importamos el transportador:

```js
const transporter = require('PATH_DEL_ARCHIVO');
```
Dónde **PATH_DEL_ARCHIVO** es la ruta relativa a donde se encuentra el archivo **notification.js**

Luego reamos el objeto con las opciones:

```js
 const mailOption = {
      from : 'informes@cima.com.pe', //correo que envía, debe ser el mismo que se encuentra en mail.js
      to: 'sistemas@cima.com.pe', // correo destinatario
      subject: `MENSAJE DE SUGERENCIA DE CIMA COLEGIO`, //Asunto del correo
      html: '<h1>Hola</h1>' //contenido HTML
    }
```

Luego para enviar el correo ejecutamos el siguiente código:

```js
transporter.sendMail(mailOption,(err,info)=>{
    if(err) return console.log('ocurrió un error');
    console.log('se envió el correo');
})
```