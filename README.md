# PL/SQL
## Introducción. ¿Qué es PL/SQL?

Entonces, SQL es un lenguaje de programación especializado y diseñado para gestionar y manipular BASES DE DATOS RELACIONALES. Y es un lenguaje DECLARATIVO, es decir, describes lo que quieres hacer, en lugar de escribir paso a paso cómo hacerlo.

>[!TIP]
>No es un lenguaje de programación completo porque no tiene características como la manipulación de memoria o estructuras de control avanzadas fuera del ámbito de las bases de datos.
>- Los for, while, if, foreach.
>- o arrays para manipular la memoria.
>

SQL cuenta con sublenguajes, para que sea más preciso:

- DDL (Data Definition Languaje) Create, Alter, Drop, Truncate.
- DML (Data Manipulation Language) Select, Insert, Update, Delete.
- DCL (Data Control Language) Grant, Revoke.
- TCL (Transaction Control Language) START TRANSACTION... Commit, Rollback, Savepoint.
- PL/SQL (Procedural SQL) aquí es donde hay programación, como bucles condiciones y variables,
  - PL/SQL (En Oracle).
  - T-SQL (SQL Server).

Entonces, sabiendo esto.

Necesitamos un programa QUE SEA CAPAZ DE SOPORTAR PL/SQL, como Oracle SQL Developer (Que he usado en el Grado Superior...) (O el SQL Plus, que eso es formato CLI ) (El que usaba en Capgemini). 

>[!IMPORTANT]
>Entonces en el SQL Developer puedo hacer SELECTS y demás, SÍ, y en el Plus también.
>
>Sin embargo, en MySQL Workbench no puedo hacer PL/SQL, es exclusivo de Oracle, mientras que MySQL usa un lenguaje procedimental diferente llamado "MySQL Procedural Language" dentro de sus procedimientos almacenados.
>
>Entonces, MySQL Workbench utiliza **ALGO PARECIDO al PL/SQL, pero NO es igual de potente**
>
>| Característica | PL/SQL (Oracle) | MySQL (Procedural) |
>| ------------- | ------------- | ------------- |
>| Base de datos | Oracle | MySQL |
>| Lenguaje Procedural  | PL/SQL | Procedural SQL (MySQL) |
>| Soporta paquetes	  | ✅ Sí | ❌ No |
>| Triggers avanzados  | ✅ Sí | ⚠️ Limitados |
>| Cursores explícitos | ✅ Sí | ⚠️ Limitados  |
>| Manejo de excepciones  | ✅ Sí (EXCEPTION)  | ⚠️ Limitado (DECLARE HANDLER) |


# Introducción al ejercicio.
Voy a crear el entorno usando Docker:

Para ello en Windows voy a descargar el docker-desktop, no hay otra, no es como en Ubuntu que tienes la forma gráfica y forma CMD.
Aquí tienes que descargar el docker-desktop para poder usar los comandos.

Haciendo click a este enlace te lo descargará automaticamente. Es la versión AMD64.

https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe?utm_source=docker&utm_medium=webreferral&utm_campaign=dd-smartbutton&utm_location=module

# Docker Daemon Not Running.
**Vamos a comprobar que el demonio docker funcione.**

Este fue un error que NO fue culpa mía y me hizo fallar una entrevista entera:

```
$ docker build .

ERROR: error during connect: this error may indicate that the docker daemon is not running: Head "http://%2F%2F.%2Fpipe%2Fdocker_engine/_ping": open //./pipe/docker_engine: The system cannot find the file specified.
```

En cualquier caso, funciona, porque:

```
$ docker --version
Docker version 27.5.1, build 9f9e405
```

# Instalar la imagen de Oracle.

**NO se encuentra en Dockerhub**. Se encuentra aquí:

https://container-registry.oracle.com/ords/f?p=113:10:10309525717681:::::

y podemos encontrar cosas como el GoldenGate, MySQL, etc...

Concretamente buscamos la imagen que está aquí:

https://container-registry.oracle.com/ords/f?p=113:4:10309525717681:::4:P4_REPOSITORY,AI_REPOSITORY,AI_REPOSITORY_NAME,P4_REPOSITORY_NAME,P4_EULA_ID,P4_BUSINESS_AREA_ID:803,803,Oracle%20Database%20Express%20Edition,Oracle%20Database%20Express%20Edition,1,0&cs=3kSUSZKpypeaX9BO1ZKQTkvorkgcR9U3WrhddSE5Y2qCsoB10k2zZsV3yoMEsq5F7OWxfmVlKpdHnQc-fgHZCRA

![image](https://github.com/user-attachments/assets/3e2f30b7-a029-4d17-a262-bb762c894bd8)

Y aquí está el comando docker para descargar la imagen.

```
docker pull container-registry.oracle.com/database/express:latest
```

En la propia documentación de la página, nos indican que la imagen, tiene una base de datos por defecto, para que la puesta en marcha sea muy rápida, sirve para CI/CD.

Y si queremos iniciar la instancia pues se hace así:

```
docker run -d --name <oracle-db> container-registry.oracle.com/database/express:21.3.0-xe
```

**EN MI CASO**  voy a usar este comando para hacer el contenedor:

```
docker run --name oracle-xe-ilian-pruebas -p 1521:1521 -e ORACLE_PWD=123456 container-registry.oracle.com/database/express:latest
```

Entonces, una vez tengamos el contenedor, tenemos la Base de Datos en sí. 

```
docker ps | grep oracle-xe-ilian-pruebas
```
O este otro también:
```
docker ps --filter "name=oracle-xe-ilian-pruebas"
```
Ahora necesitamos pues trabajar con ella.

Para ello voy a descargar SQL Developer.

# Oracle SQL Developer.

Se trata de un programa que es como "portable", no requiere de una isntalación clásica, con un .exe y darle a siguiente, siguiente...

https://download.oracle.com/otn_software/java/sqldeveloper/sqldeveloper-24.3.1.347.1826-x64.zip

Este es el enlace a la descarga.

![image](https://github.com/user-attachments/assets/1ad08265-9e49-4ca0-b9d8-5dbff6f24676)


