# Notificaciones
Las notificaciones se manejan en el archivo 
```
src/services/notification.js
```
La función exportada es ```Notificar``` que envía notificaciones a los móviles Android que tengan las aplicaciones de la institución CIMA *(Personal,Colegio,Academia,Precadete)*

## 1. Función Notificar
Es una función que retorna una Promesa, sí aún no sabes que es una promesa te dejo un artículo por [aquí](https://medium.com/@jmz12/callbacks-promesas-y-async-await-que-alguien-me-explique-514137cb57e2).

```js
exports.Notificar = async (mensaje,plataforma,titulo,topico,token)=>{
  let campos = {
    priority : 'normal',
    data: {
      data:{
        title:titulo,
        message:mensaje,
        timestamp:new Date().toLocaleString('en-US'),
        plataforma
      }
    }
  }

  if(topico){
    campos.to = '/topics/'+topico;
  }
  else{
    campos.registration_ids = token;    
  }
  
  let respuesta = await axios.post('https://fcm.googleapis.com/fcm/send',campos,{
    headers: { 'Content-Type': 'application/json', 'Authorization':'TOKEN-SECRETO-FIREBASE'}
  })
  return respuesta.data;
}

```


 Los parametros son:

* **Mensaje:** Mensaje que se muestra en la notificación.
* **Plataforma:** Cimapersonal,Cimacolegio,etc.
* **Titulo:** Título de la notificación.
* **Topico:** A quienes va dirigido(Notificación masiva), puede ser ```null``` cuando se envíe **token** y viceversa.
* **Token:** Usuarios específicos a quienes se notifica, puede ser ```null``` cuando se envíe **topico** y viceversa.

El **TOKEN-SECRETO-FIREBASE** es un token que permite a Firebase autenticarnos y enviar las notificaciones.

> El token que se envía como parametro es diferente al token de autenticación de Firebase.

## 2. Usar la función Notificar
Para usar la función **Notificar** debemos importarla, con la siguiente línea de código.

```js
const {Notificar} = require('PATH_DEL_ARCHIVO');
```

Dónde **PATH_DEL_ARCHIVO** es la ruta relativa a donde se encuentra el archivo **notification.js**

Y para ejecutar la función es con el siguiente código:

```js
 Notificar(text, 'CUMPLEAÑOS', 'CUMPLEAÑOS', 'cimapersonal', null)
    .then(()=> console.log('Notificacion[Cumpleaños] enviada'))    
    .catch(err => console.log(err))
```

> La función puede ser llamada en cualquier archivo, en el ejemplo mostrado esta en cron.js para enviar notificaciones de Cumpleaños.