# PL-SQ

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
