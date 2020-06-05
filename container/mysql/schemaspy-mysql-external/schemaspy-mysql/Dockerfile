FROM openjdk:8-jdk-alpine

ENV MYSQL_VERSION=6.0.6
ENV SCHEMASPY_VERSION=6.1.0
ENV SCHEMASPY_OUTPUT=/output

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