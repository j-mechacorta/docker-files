FROM fedora-minimal:33

COPY binaries/hive/3.0.0/hive /opt/hive
COPY binaries/hadoop/2.7.5/hadoop /opt/hadoop
COPY binaries/postgresql-42.2.20.jar /opt/hive/lib
RUN microdnf -y install which java-1.8.0-openjdk java-1.8.0-openjdk-devel

ENV JAVA_HOME=/usr/lib/jvm/java
ENV HADOOP_HOME=/opt/hadoop
ENV HADOOP_CONF_DIR=/opt/hadoop/conf
ENV HADOOP_COMMON_LIB_NATIVE_DIR=/opt/hadoop/lib
ENV HIVE_HOME=/opt/hive
ENV PATH=${JAVA_HOME}:${HADOOP_HOME}/bin:${HIVE_HOME}/bin:${PATH}

RUN schematool -dbType postgres -initSchema

CMD ["start-metastore"]