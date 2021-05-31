# FROM openjdk:8u212-jre-alpine3.9
FROM fedora-minimal:33


WORKDIR /opt
COPY binaries/spark-3.1.1-bin-hadoop3.2.tgz .
 

VOLUME [ "/data", "/opt/spark/history", "/opt/spark/conf", "/opt/spark/logs"]

# RUN apk update && apk upgrade && apk add bash && apk add util-linux
RUN microdnf -y install java-1.8.0-openjdk tar tree util-linux procps

RUN tar xf spark-3.1.1-bin-hadoop3.2.tgz && cp -r spark-3.1.1-bin-hadoop3.2/* spark

RUN mkdir -p /tmp/spark-events

ENV SPARK_HOME=/opt/spark
ENV SPARK_CONF_DIR=/opt/spark/conf
ENV SPARK_NO_DAEMONIZE=TRUE
ENV JAVA_HOME=/usr/lib/jvm/jre
ENV PATH=$SPARK_HOME/bin:$SPARK_HOME/sbin:$PATH

RUN echo $PATH


EXPOSE 18080

CMD ["/opt/spark/sbin/start-history-server.sh"]