# schemaspy-mysql-external

Conjunto de Contenedores Docker encargados de realizar una análisis de base de datos con **SchemaSpy** en **MySQL** publicando los resultados mediante **Nginx**

La base de datos se encuentra disponible (instalacion, contenedor o servicio) antes y de formae externa que el resto de contenedores



## Stack Tecnológico

* [Docker](https://www.docker.com/) - Technología de Contenedores/Containers
* [Docker Hub](https://hub.docker.com/) - Repositorio de Docker Publico
* [SchemaSpy](http://schemaspy.org/) - Utilidad de documentación de la base de datos
* [MySQL](https://www.mysql.com/) - Base de Datos relacional (Version 5.7)
* [Nginx](https://www.nginx.com/) - Servidor Web / Proxy Inverso

Dependencias con Proyectos de Arquitectura

N/A

Dependencias con Terceros

N/A





## Prerrequisitos

Define que elementos son necesarios para instalar el software

* Docker instalado (19+)





## Instalación

### Docker Compose

Configuración del fichero "docker-compose.yaml"

```bash
version: '3.7'

services:

   schemaspy-mysql:
      build: ./schemaspy-mysql
      volumes:
         - ./schemaspy-mysql/output:/app/output/
         - ./schemaspy-mysql/config/schemaspy.properties:/app/config/schemaspy.properties
      command: ["-configFile", "/config/schemaspy.properties"]
      network_mode: host

   nginx:
      build: ./nginx
      ports:
         - "8081:80"
      volumes:
         - ./schemaspy-mysql/output:/usr/share/nginx/html:ro
```

**Servicio schemaspy-mysql** : Genera un contenedor donde se ejecutará el análisis de Schemaspy, se generarán una serie de volumenes y se facilitará un parametro de ejecución

Configuración del fichero "Dockerfile"

```bash
FROM openjdk:8-jdk-alpine

ENV MYSQL_VERSION=6.0.6
ENV SCHEMASPY_VERSION=6.1.0

LABEL MYSQL_VERSION=$MYSQL_VERSION
LABEL SCHEMASPY_VERSION=$SCHEMASPY_VERSION

ADD ./open-sans.tar.gz /usr/share/fonts/

WORKDIR /app

RUN adduser java -h / -D && \
    set -x && \
    apk add --no-cache curl unzip graphviz fontconfig && \
    curl -JLO https://repo1.maven.org/maven2/mysql/mysql-connector-java/$MYSQL_VERSION/mysql-connector-java-$MYSQL_VERSION.jar && \
    curl -JLO https://github.com/schemaspy/schemaspy/releases/download/v$SCHEMASPY_VERSION/schemaspy-$SCHEMASPY_VERSION.jar  && \
    mkdir /app/output /app/config

COPY schemaspy.properties /config/schemaspy.properties

RUN chown -R java /app

# ENTRYPOINT ["java", "-jar", "schemaspy-6.1.0.jar", "-configFile", "/config/schemaspy.properties" ,"-debug"]
ENTRYPOINT ["java", "-jar", "schemaspy-6.1.0.jar"]
```

En este fichero se establece la versión base del conenedor con el que se va a trabajar, se añade mediente apk una serie de dependencias necesarias entre ellas la de graphviz (que es necesaria que este instalada en la maquina que ejecute schemaspy), descargará de de los respositorios las librerías definidas, se compiará el fichero de configuración de schemaspy y se ejecutará schemspy


**Servicio nginx** : Genera un contenedor Nginx que será encargado de publicar los resultados y se publicará por el puerto específico establecido

Configuración del fichero "Dockerfile"

```bash
FROM nginx:alpine

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

En este fichero se establece la versión a utilizar y se le indicará cierta información de configuración


Pasos a seguir


1. Localizar el directorio principal del proyecto : <PROJECT_PATH> (container/mysql/schemspy-mysql-external)

2. Ejecutar el siguiente comando

```bash
docker-compose up --build

ó

docker-compose up --build -d
```

![Trazas de Ejecución de Schemapsy](https://github.com/vjmadrid/enmilocalfunciona-schemaspy/blob/master/images/schemaspy-external-execution.png)

3. Comprobar que la imagen ha sido creada

Verificar que parece como imagen Docker el nombre "schemaspy-mysql-external_nginx"
Verificar que parece como imagen Docker el nombre "schemaspy-mysql-external_schemaspy-mysql"

4. Comprobar que la aplicación ha sido desplegada correctamente

Verificar mediante un navegaor accediendo a la URL de publicación

```bash
http://localhost:8081/
```

![Resultados de Schemapsy](https://github.com/vjmadrid/enmilocalfunciona-schemaspy/blob/master/images/schemaspy-external-result.png)




## Pruebas

N/A





## Despliegue

N/A





## Uso

N/A





## Versionado

**Nota :** [SemVer](http://semver.org/) es usado para el versionado.





## Autores

* **Víctor Madrid**
