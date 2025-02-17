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
