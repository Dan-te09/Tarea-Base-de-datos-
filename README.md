# DOCUMENTACION DEL SERVIDOR DE BASE DE DATOS MYSQL CON DOCKER

## SETUP (PREPARACION DEL AMBIENTE)

1.- DOCKER Preinstalado en el equipo.

2.- CMD o terminal para ejecutar comandos.

3.- Docker Desktop (opcional para visualización de contenedores).

## SISTEMA OPERATIVO

El equipo en el que se está trabajando es con un sistema operativo Windows.

***

## COMO HACER EL SERVIDOR DE MYSQL EN DOCKER

Para crear un servidor de base de datos MySQL en Docker, primero abre o ejecuta **Docker Desktop** y después abre el **CMD** o el sistema de símbolos de tu equipo.

### 1. Descargar las imágenes de MySQL y phpMyAdmin

Para descargar las imágenes de MySQL y phpMyAdmin, ejecuta los siguientes comandos:

**Para descargar la imagen de MySQL:**
~~~bash
docker pull mysql:latest
~~~

**Para descargar la imagen de phpMyAdmin:**
~~~bash
docker pull phpmyadmin/phpmyadmin:latest
~~~

Estas imágenes se descargarán en tu máquina local.

### 2. Crear los contenedores de MySQL y phpMyAdmin

Una vez descargadas las imágenes, debes crear los contenedores correspondientes. Ejecuta el siguiente comando para crear el contenedor de MySQL, especificando una contraseña para el usuario root (en este caso, "7777777"):

**Para crear el contenedor de MySQL:**
~~~bash
docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=7777777 -d mysql:latest
~~~

Luego, crea el contenedor de phpMyAdmin y vincúlalo con el contenedor de MySQL mediante el parámetro `--link`:

**Para crear el contenedor de phpMyAdmin:**
~~~bash
docker run --name phpmyadmin-container --link mysql-container:db -p 8080:80 -d phpmyadmin/phpmyadmin:latest
~~~

+ **-e MYSQL_ROOT_PASSWORD=7777777**: Establece la contraseña del usuario `root` de MySQL.
+ **--link mysql-container:db**: Enlaza el contenedor de phpMyAdmin con el contenedor de MySQL.
+ **-p 8080:80**: Mapea el puerto 8080 del host al puerto 80 del contenedor de phpMyAdmin.
+ **-d**: Ejecuta el contenedor en segundo plano.

### 3. Verificación en Docker Desktop

Dentro de **Docker Desktop**, podrás ver los contenedores de MySQL y phpMyAdmin en la pestaña de **Containers / Apps**.

### 4. Acceder a phpMyAdmin

Para acceder a la interfaz web de phpMyAdmin, abre tu navegador y dirígete a:

http://localhost:8080

Desde aquí podrás gestionar las bases de datos MySQL de manera visual.

### 5. Acceder a MySQL desde el contenedor

Si prefieres trabajar directamente desde la terminal dentro del contenedor de MySQL, usa el siguiente comando:

**Para acceder al contenedor de MySQL:**
~~~bash
docker exec -it mysql-container mysql -u root -p
~~~

Te pedirá la contraseña del usuario `root`, que en este caso es **"7777777"**.

### 6. Crear una Base de Datos

Una vez dentro del entorno MySQL, puedes crear una base de datos ejecutando los siguientes comandos SQL:

**Para crear la base de datos `db_Estudiante`:**
~~~sql
CREATE DATABASE db_Estudiante;
USE db_Estudiante;
~~~

Esto creará una base de datos llamada `db_Estudiante` y te cambiará al contexto de esa base de datos.

### 7. Crear Tablas

Ahora puedes crear tablas dentro de la base de datos `db_Estudiante`. Ejemplo:

**Para crear una tabla de estudiantes:**
~~~sql
CREATE TABLE estudiantes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    edad INT
);
~~~

### 8. Verificar Bases de Datos

Para listar las bases de datos creadas, usa el siguiente comando MySQL:

**Para listar las bases de datos:**
~~~sql
SHOW DATABASES;
~~~

Esto mostrará todas las bases de datos disponibles en el servidor MySQL.

---

¡Listo! Ahora tienes un servidor MySQL corriendo dentro de un contenedor Docker, accesible a través de phpMyAdmin en tu navegador y con la capacidad de gestionar bases de datos desde la terminal.
