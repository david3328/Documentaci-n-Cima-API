# Rutas o Endpoints 
Las rutas o endpoints son **uri** donde podemos realizar distintas peticiones HTTP *(GET,POST,PUT,DELETE) entre las más conocidas* 

> Las rutas en esta documentación estarán organizadas por proyecto, por lo cual solo se colocará la **URI**

## 1. Rutas según entorno.
La URL que podemos tener va según el entorno que nos encontremos, entonces tenemos: 

* http://localhost:3000/api
* http://192.168.70.13:3000/api
* http://intranet.cima.com.pe:3000/api

> Las **URL** dependen de donde nos encontremos. Del mismo modo al llamar a la ruta debemos tener en cuenta que acceso debería tener nuestro proyecto.

## 2. Accesos al proyecto

* Si estamos trabajando en nuestro local podemos hacer referencia a http://localhost:3000/api *(solo serviría para etapa de desarrollo)*


* Si queremos que el proyecto solo tenga acceso a la intranet, haremos referencia a http://192.168.70.13:3000/api *(cualquier persona que no se encuentre en la red de CIMA no tendrá acceso)*

> Esta URL es utilizada el proyecto RFID.

* Si queremos tener nuestra aplicación publicada, haremos referencia a http://intranet.cima.com.pe:3000/api 

> La Aplicación en Android utiliza *(siempre)* esta URL.

## 3. Conclusiones

Las **3 URL** indicadas serán utilizadas según el acceso que se le darán a los proyectos que consumen el **API**. 

> En las carpetas que tenemos solo haremos referencia a la uri y se deben concatenar con la **URL** que cree sea la adecuada. 

Ejemplo: 
 * Tenemos un **uri** del colegio que me lista los profesores **/colegio/profesores**, entonces al concatenar con la **URL**, tendríamoss

    * http://localhost:3000/api/colegio/profesores
    * http://192.168.70.13:3000/api/colegio/profesores
    * http://intranet.cima.com.pe:3000/api/colegio/profesores
