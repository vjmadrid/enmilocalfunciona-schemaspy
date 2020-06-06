# enmilocalfunciona-schemaspy

Este repositorio se encarga de servir como estructura de recursos utilidazados para los artículos publicados en la plataforma **enmilocalfunciona.io** relacionados con el uso de **[Schemaspy](http://schemaspy.org/)**

* [Web Principal SchemaSpy](http://schemaspy.org/)
* [Documentación SchemaSpy](https://schemaspy.readthedocs.io/en/latest/)
* [Repositiorio de código Github](https://github.com/schemaspy/schemaspy)
* [Repositorio de contenedores Docker Hub](https://hub.docker.com/r/schemaspy/schemaspy/)

Schemaspy destaca por proporciona un site web con **Documentación visual** sobre : tablas, volumetrías, columnas, constraints, routines, ... -> web-based

Para ello se han planteado 2 enfoques de uso :

**Standalone** : Ejecuta Schemaspy como una librería Java independiente en base a 2 modos de ejecución (mediante ficheros y por parámetros) y generando los resultados HTML en un directorio

IMPORTANTE : En este caso Schemaspy requiere tener ciertas dependencias instaladas previamente ([Graphviz](https://graphviz.org/))

**Container** : Ejecuta Schemaspy dentro de un contenedor como una librería Java independiente en base a la configuración de un fichero, generando los resultados HTML en un directorio y exponiendo dichos resultados mediante el uso de Nginx. En este caso también se enseñarán 2 modos de ejecución pero basados en la incorporación de forma interna o externa de la base de datos.

IMPORTANTE : En este caso Schemaspy tendrá las dependencias instaladas en el container ([Graphviz](https://graphviz.org/))



## Stack Tecnológico

* Java 8
* [Graphviz](https://graphviz.org/) - Generador de diagramas de base de datos
* [SchemaSpy](http://schemaspy.org/) - Utilidad de documentación de la base de datos
* [Docker](https://www.docker.com/) - Technología de Contenedores/Containers
* [Docker Hub](https://hub.docker.com/) - Repositorio de Docker Publico
* [Nginx](https://www.nginx.com/) - Servidor Web / Proxy Inverso

Dependencias con Proyectos de Arquitectura

N/A

Dependecias con Terceros

N/A





## Prerrequisitos

Define que elementos son necesarios para instalar el software

* Java 8 instalado (1.5+ version requerido)
* Docker instalado (19+)
* Graphviz instalado para el caso "Standalone"





Se encuentra organizado en 3 áreas :

* infraestructure-db
* standalone
* containers





## infraestructure-db

Directorio encargado de almacenar las versiones contenerizadas con Docker de las bases de datos utilizadas en el ejemplo del artículo.

Las base de datos utilizadas son :

* MySQL 5.7
* Postgresql 11

Para ello, se hará uso de los ficheros "docker-compose.yaml" y Dockerfile donde se detallarán detalles de la versión utilizada, definición de usuarios utilizados, pre-carga inicial de datos, etc. 

IMPORTANTE : Seguir en detalle el ficherio explicativo de cada caso.





## standalone
 
Directorio encargado de almacenar el modo de uso de Schemaspy que lo ejecuta como una librería Java independiente





## container

Directorio encargado de almacenar el modo de uso de Schemaspy que lo ejecuta como un contenedor

Se seguiran 2 modos de uso :

* Internal : Hará uso de una BD que además será un contendor
* External : Hará uso de una BD externa arrancada, funcionando y con juego de datos


## Autor

* **Víctor Madrid**
