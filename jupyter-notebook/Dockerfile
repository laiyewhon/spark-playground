FROM jupyter/base-notebook:python-3.10

USER root

RUN apt-get update && apt-get install -y\
    curl\
    unzip\
    zip

RUN apt-get clean

USER jovyan

RUN pip install pandas numpy

RUN curl -s "https://get.sdkman.io" | bash
RUN source $HOME/.sdkman/bin/sdkman-init.sh && sdk install java 8.0.362-tem
ENV SDKMAN_DIR=$HOME/.sdkman
ENV JAVA_HOME="$SDKMAN_DIR/candidates/java/current"
ENV PATH="$JAVA_HOME/bin:$PATH"

RUN curl -o /tmp/spark-3.2.3-bin-hadoop3.2.tgz https://archive.apache.org/dist/spark/spark-3.2.3/spark-3.2.3-bin-hadoop3.2.tgz
RUN tar -xvzf /tmp/spark-3.2.3-bin-hadoop3.2.tgz
RUN rm /tmp/spark-3.2.3-bin-hadoop3.2.tgz
RUN ln -s spark-3.2.3-bin-hadoop3.2 spark

ENV SPARK_HOME=$HOME/spark
ENV PATH=$SPARK_HOME/bin:$PATH
ENV PYSPARK_DRIVER_PYTHON=jupyter
ENV PYSPARK_DRIVER_PYTHON_OPTS=notebook

CMD $SPARK_HOME/bin/pyspark --master spark://spark-master:7077
