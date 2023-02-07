FROM ubuntu:lunar

RUN apt update -y
RUN apt install -y default-jre openssh-server curl
RUN apt-get clean

RUN service ssh start

RUN adduser hadoop
RUN mkdir /hadoop
RUN chown hadoop:hadoop /hadoop

WORKDIR /hadoop

RUN curl -o /tmp/hadoop-3.3.4.tar.gz https://dlcdn.apache.org/hadoop/common/hadoop-3.3.4/hadoop-3.3.4.tar.gz
RUN tar -xzf /tmp/hadoop-3.3.4.tar.gz
RUN ln -s /hadoop/hadoop-3.3.4 hadoop
RUN rm -f /tmp/hadoop-3.3.4.tar.gz

ENV JAVA_HOME=/usr/lib/jvm/default-java
ENV HADOOP_HOME=/hadoop/hadoop
ENV PATH=${HADOOP_HOME}/bin:${PATH}

RUN $HADOOP_HOME/bin/hdfs namenode -format my-hdfs
