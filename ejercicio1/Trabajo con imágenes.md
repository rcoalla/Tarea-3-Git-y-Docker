title: Actividad Evaluable 3, Git y Docker
Segundo Cuatrimestre DAW, CIF La Laboral

Author Rubén Álvarez Coalla



[TOC]



> # Ejercicio 1 - trabajo con imágenes



# TRABAJO CON IMÁGENES

------

### Servidor web

- Arranca un contenedor que ejecute una instancia de la imagen php:7.4-apache , que se llame web y
  que sea accesible desde un navegador en el puerto 8000.
- Colocar en el directorio raíz del servicio web ( `/var/www/html` ) de dicho contenedor un fichero llamado
  index.html con un h1 con tus nombres y apellidos
- Colocar en ese mismo directorio raíz un archivo llamado `mes.php` que muestre el nombre del mes
  actual. Ver la salida del script en el navegador
- Borrar el contenedor



##### 1. Pantallazo que desde el navegador muestre el fichero `index.html` 

```bash
docker run -d --name web -p 8000:80 php:7.4-apache
```

![image-20220410190614497](Trabajo%20con%20im%C3%A1genes.assets/image-20220410190614497-16496103757211.png)





```bash
docker exec web bash -c 'echo "<h1>Hola soy Ruben Alvarez Coalla<h1>" > /var/www/html/index.html'
```



![image-20220409222104297](Trabajo%20con%20im%C3%A1genes.assets/image-20220409222104297.png)





![image-20220407214326480](Trabajo%20con%20im%C3%A1genes.assets/image-20220407214326480.png)



##### 2. Pantallazo que desde un navegador muestre la salida del script `mes.php`



![image-20220410213811464](Trabajo%20con%20im%C3%A1genes.assets/image-20220410213811464.png)





![image-20220410210427257](Trabajo%20con%20im%C3%A1genes.assets/image-20220410210427257.png)





![image-20220410210254594](Trabajo%20con%20im%C3%A1genes.assets/image-20220410210254594.png)



##### 3. Pantallazo donde se vea el tamaño del contenedor `web` después de crear los dos ficheros

```bash
docker ps -a -s
```



![image-20220410215040647](Trabajo%20con%20im%C3%A1genes.assets/image-20220410215040647.png)







### Servidor de base de datos

------

- Arrancar un contenedor que se llame `bbdd` y que ejecute una instancia de la imagen **mariadb**.
- Establece las variables de entorno necesarias para que:
  - La contraseña de root sea `root` 
  - Crear una base de datos automáticamente al arrancar que se llame prueba.
  - Crear el usuario invitado con la contraseña invitado .





##### 1. Pantallazo de la consola de la Base de Datos donde se pueda observar que hemos podido conectarnos al servidor de base de datos con el usuario creado y que se ha creado la base de datos prueba ( `show databases` ).



```bash
docker run -d --name bbdd -e MARIADB_DATABASE=prueba -e MARIADB_ROOT_PASSWORD=root -e MARIADB_USER=invitado,MARIDB_PASSWORD=invitado mariadb:latest
```



![image-20220408230351170](Trabajo%20con%20im%C3%A1genes.assets/image-20220408230351170.png)





```bash
docker exec -it bbdd mariadb -uroot -p
```



![image-20220409131518676](Trabajo%20con%20im%C3%A1genes.assets/image-20220409131518676.png)





![image-20220409131544456](Trabajo%20con%20im%C3%A1genes.assets/image-20220409131544456.png)





##### 2. Pantallazo donde se comprueba que no se puede borrar la imagen `mariadb` mientras el contenedor`bbdd` está creado

```bash
docker rmi maridb
```



![image-20220410223815778](Trabajo%20con%20im%C3%A1genes.assets/image-20220410223815778.png)





##### 3. Pantallazo donde se vean las imágenes que tienes en tu registro local.

```bash
docker images
```



![image-20220410224152374](Trabajo%20con%20im%C3%A1genes.assets/image-20220410224152374.png)





##### 4. Pantallazo donde se vea cómo se eliminan los contenedores utilizados

Primero paramos los contenedores y luego los borramos

```bash
docker stop bbdd
```

```bash
docker rm bbdd
```





![image-20220410224937570](Trabajo%20con%20im%C3%A1genes.assets/image-20220410224937570.png)



```bash
docker stop web
```

```
docker rm web
```



![image-20220410224627691](Trabajo%20con%20im%C3%A1genes.assets/image-20220410224627691.png)





