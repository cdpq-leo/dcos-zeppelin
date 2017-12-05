FROM mesosphere/mesos:1.4.1

RUN apt-get update && \
    apt-get install -y software-properties-common
RUN add-apt-repository ppa:openjdk-r/ppa
RUN apt-get update && \
    apt-get install --yes \
    openjdk-8-jdk\
    wget \
    tar

# java
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
RUN update-alternatives --set java /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java

# hadoop
ENV HADOOP_CONF_DIR /etc/hadoop
ADD ./conf/hadoop/hdfs-site.xml /etc/hadoop/hdfs-site.xml
ADD ./conf/hadoop/core-site.xml /etc/hadoop/core-site.xml

# spark
RUN wget https://downloads.mesosphere.com/spark/assets/spark-2.2.0-1-bin-2.6.tgz
RUN tar xzvf spark-2.2.0-1-bin-2.6.tgz
ENV SPARK_HOME /spark-2.2.0-1-bin-2.6/
ADD ./conf/spark/spark-defaults.conf /spark-2.2.0-1-bin-2.6/conf/spark-defaults.conf

# zeppelin
RUN wget http://www.apache.org/dist/zeppelin/zeppelin-0.7.3/zeppelin-0.7.3-bin-all.tgz
RUN tar xzvf zeppelin-0.7.3-bin-all.tgz
WORKDIR /zeppelin-0.7.3-bin-all
ADD zeppelin-env.sh conf/zeppelin-env.sh

CMD ["bin/zeppelin.sh", "start"]
