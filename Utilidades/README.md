# Utilidades 

##  1. Ubicación del proyecto API 

```
/var/www/html/intranetcima/Cima-Colegio-API
```
>La API utiliza PM2 que es un manejador de proyectos de NodeJS.

[PM2 Documentación](http://pm2.keymetrics.io/docs/usage/pm2-doc-single-page/)

### 1.1 ¿Cómo conectarse por SSH?
Podemos conectarnos por Putty o por el SSH integrado que tiene Git Bash, realizaremos el ejemplo con este último.

*   Abrimos un terminarl de Git Bash *(no importa de que directorio se abre el Git Bash)*

![](./bash.png)
*   Nos conectamos mediante SSH al servidor 192.168.70.13 con el siguiente comando:
```
ssh root@192.168.70.13
```
![](./ssh.png)

>En este caso estamos usando la IP privada, porque estamos conectados en la misma red que el servidor, caso contrario solicitar la IP pública al responsable de turno.

* Ingresamos la clave que nos solicita, de no tener la clave contactarse con el responsable de turno. 

![](./password.png)

* De ser la clave correcta nos aparece la fecha y hora de la última conexión y ya podemos ejecutar comando en el servidor. 

![](./connect.png)

> De ser la primera vez que se conecta le pedirá una confirmación solo escribir **yes** y darle enter.

## 2. Obtener cambios realizados en el proyecto

Cada vez que desarrollamos sobre el proyecto, los cambios lo subimos al repositorio remoto(GitLab), necesitamos obtener esos cambios en el servidor **192.168.70.13**, para lo cuál necesitamos ingresar al proyecto y obtener los cambios con el comando ```git pull```, el cual pedirá las credenciales de la cuenta de *GitLab* para descargar los cambios. 

> *Nota:* hay veces en que instalamos paquetes de **npm**, en ese caso antes de reiniciar el servidor debemos instalar los paquetes con el comando ```npm install```

Una vez descargados los cambios se necesita reiniciar el proyecto.

## 3. Reiniciar el servidor *(proyecto)* de la API

Para reinicar el proyecto, primero debemos ubicarnos en la raíz del proyecto:

```
/var/www/html/intranetcima/Cima-Colegio-API
```
Luego ejecutar el siguiente comando ```pm2 restart src/index.js```

El comando reinica el proyecto, **pm2 restart** indica que vamos a reiniciar y **src/index.js** es la ruta del archivo principal *(siempre que nos ubiquemos en la raíz del proyecto)* que ejecuta todo el proyecto.

## 4. Revisar el estado de la API 

Si por algún motivo la API no esta funcionando, primero debemos verificar si esta corriendo.

Ejecutamos el comando:

```
pm2 ls
```

El comando mostrará un cuadro con los proyectos de **NodeJS** que se están ejecutando, y mostrará el estado.

En el caso de tener algún error, debemos ver los logs.

## 5. Revisar los logs de la API
Los logs nos ayudan a ver si ha sucedido algún error, además cada vez que se ejecute un *console.log* también se registrará.

Ejecutamos el comando:
```
pm2 logs --lines 500
```

>*500:* Indica la cantidad de logs que se quiere visualizar