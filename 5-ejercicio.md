## Esquema para el ejercicio
![Imagen](img/esquema-ejercicio5.PNG)

### Crear la red
```
docker network create net-wp -d brige
```
![Imagen2](img/mysqlEjercicio1.PNG)
### Crear el contenedor mysql a partir de la imagen mysql:8, configurar las variables de entorno necesarias
```
docker run -d --name mysqlContenedor --network net-wp -e MYSQL_ROOT_PASSWORD=secretpassword -e MYSQL_DATABASE=wordpress_db -e MYSQL_USER=wp_user -e MYSQL_PASSWORD=wp_password mysql:8
```
![Imagen3](img/mysqlContenedor.PNG)
### Crear el contenedor wordpress a partir de la imagen: wordpress, configurar las variables de entorno necesarias

```
docker run -d --name wordpress --network net-wp -e WORDPRESS_DB_HOST=mysql:3306 -e WORDPRESS_DB_USER=wp_user -e WORDPRESS_DB_PASSWORD=wp_password -e WORDPRESS_DB_NAME=wordpress_db -p 9300:80 wordpress
```


De acuerdo con el trabajo realizado, en la el esquema de ejercicio el puerto a es 9300

Ingresar desde el navegador al wordpress y finalizar la configuración de instalación.
![Imagen4](img/wordpressConfig.PNG)
![Imagen5](img/wordpressInstall.PNG)

Desde el panel de admin: cambiar el tema y crear una nueva publicación.
![Imagen6](img/wordpressMenu.PNG)
![Imagen7](img/wpNuevoTema.PNG)

Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress
![Imagen8](img/wpPrimerPublicacion.PNG)

### Eliminar el contenedor wordpress
```
docker rm wordpress
```
# COMPLETAR

### Crear nuevamente el contenedor wordpress
![Imagen9](img/reinstalar.PNG)

Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress

![Imagen10](img/wpDNuevo.PNG)
### ¿Qué ha sucedido, qué puede observar?
La primera vez que cargo la publicacion no se me reflejo el cambio de tema. Pero al volver a instalar wordpress este si sale cambiado, por lo que los datos persisten a pesar de que borro el contenedor. Esto por que esta almacenado en la base de datos MySQL en un contenedor separado. 






