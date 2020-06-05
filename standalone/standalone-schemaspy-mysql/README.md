# standalone-schemaspy-mysql

Este proyecto representa un ejemplo de ejecución de **Schemaspy** como una librería Java para una base de datos **MySQL** que se encuentre disponible y con datos.

Como resultado de la ejecución se generá un directorio con los resultados en formato HTML





## Stack Tecnológico

* Java 8
* [SchemaSpy](http://schemaspy.org/) - Utilidad de documentación de la base de datos
* [Graphviz](https://graphviz.org/) - Generador de diagramas de base de datos
* [MySQL](https://www.mysql.com/) - Base de Datos relacional (Version 5.7)

Dependencias proyectos de arquitectura

N/A

Dependencias de terceros 

* **mysql-connector-java** [6.0.6] : Conector SQL server (compatible con la versión de la base de datos utilizada)
* **schemaspy** [6.1.0] : Utilidad SchemaSpy (single-jar)





## Prerrequisitos

Define que elementos son necesarios para instalar el software

* Java 8 instalado (1.5+ version requerido)
* Base de datos a utilizar instalada y arrancada con datos
* Driver de conexión a la base de datos utilizada
* Graphviz instalado para la generación visual de los diagramas de relación





## Instalación

N/A





## Testing

N/A





## Deploy

N/A




## Uso



### Standalone con fichero de configuración

Pasos a seguir

* Arrancar un terminal
* Localizar el PATH de esta funcionalidad : **standalone-schemaspy-mysql**
* Definir el fichero **"schemaspy.properties"** con todos los elementos de configuración de la base de datos con la que se va a trabajar

Ejemplo de fichero "schemaspy.properties" utilizado

```bash
# Database Type
schemaspy.t=mysql

# Path Database JDBC driver
schemaspy.dp=mysql-connector-java-6.0.6.jar

# Database Machine
schemaspy.host=127.0.0.1
schemaspy.port=3306

# Database user
schemaspy.u=test
schemaspy.p=test

# Database Name
schemaspy.db=acme

# Database Schema
schemaspy.s=acme

# Path output folder for the generated result
schemaspy.o=output
```

* Ejecutar el siguiente comando

```bash
java -jar schemaspy-6.1.0.jar 
```

Nota : Si no se indica nada, buscará en el directorio actual el fichero de configuración para ejecutarlo 


Se puede establecer que ejecute un fichero concreto (por entorno, apuntando a un contenedor, etc.)

```bash
java -jar schemaspy-6.1.0.jar -configFile config/schemaspy-dev.properties
```


### Standalone con parámetros

Pasos a seguir

* Arrancar un terminal
* Localizar el PATH de esta funcionalidad : **standalone-schemaspy-mysql**
* Ejecutar el siguiente comando con parámetros (No se usa eñ fichero de configuración)

```bash
java -jar schemaspy-6.1.0.jar -t mysql -dp mysql-connector-java-6.0.6.jar -host 127.0.0.1 -port 3306 -u test -p test -db acme -s acme -o output
```

* -t : Tipo de base de datos de los identificados por la utilidad
* -dp : Ubicación del driver de DB utilizado
* -host : IP de la máquina donde se encuentra la base de datos
* -port : Puerto de conexión a la base de datos (en muchos casos la definición del tipo y el driver lo establecen por defecto)
* -u : Ususario
* -p : Password
* -db : Base de datos a la que conectar
* -s : Esquema de base de datos
* -o : Path de salida de los resultados del análisis



### Resultado

![Trazas de Ejecución de Schemapsy](https://github.com/vjmadrid/enmilocalfunciona-schemaspy/blob/master/images/mysql-schemaspy-standalone-execution.png)

* Verificar que se dejan los resultados en el directorio establecido

* Abrir con un navegador el fichero index.html

![Resultados de Schemapsy](https://github.com/vjmadrid/enmilocalfunciona-schemaspy/blob/master/images/mysql-schemaspy-standalone-result.png)





## Versionado

**Nota :** [SemVer](http://semver.org/) es utilizado por el versionado

Para ver las versiones disponibles ver los tags del repositorio





## Autores

* **Víctor Madrid**

