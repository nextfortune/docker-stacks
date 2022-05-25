From jupyter/base-notebook:ubuntu-18.04 as build

USER root
# Install Spark
# Spark dependencies
# Default values can be overridden at build time
# (ARGS are in lower case to distinguish them from ENV)
ARG spark_version="3.1.1"
ARG hadoop_version="3.2"
ARG spark_checksum="E90B31E58F6D95A42900BA4D288261D71F6C19FA39C1CB71862B792D1B5564941A320227F6AB0E09D946F16B8C1969ED2DEA2A369EC8F9D2D7099189234DE1BE"
ARG openjdk_version="8"

ENV APACHE_SPARK_VERSION="${spark_version}" \
    HADOOP_VERSION="${hadoop_version}"

RUN sudo -E apt-get -y update && \
    sudo -E apt-get install --no-install-recommends -y \
    "openjdk-${openjdk_version}-jre-headless" \
    ca-certificates-java
RUN sudo -E apt-get clean && rm -rf /var/lib/apt/lists/*

# Spark installation
WORKDIR /tmp
RUN sudo -E wget -q "https://archive.apache.org/dist/spark/spark-${APACHE_SPARK_VERSION}/spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz" && \
    echo "${spark_checksum} *spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz" | sha512sum -c - && \
    tar xzf "spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz" -C /usr/local --owner root --group root --no-same-owner && \
    rm "spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz"

WORKDIR /usr/local

# Configure Spark
ENV SPARK_HOME=/usr/local/spark
ENV SPARK_OPTS="--driver-java-options=-Xms1024M --driver-java-options=-Xmx8192M --driver-java-options=-Dlog4j.logLevel=info" \
    PATH=$PATH:$SPARK_HOME/bin

RUN ln -s "spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}" spark
# Add a link in the before_notebook hook in order to source automatically PYTHONPATH
RUN mkdir -p /usr/local/bin/before-notebook.d && \
    ln -s "${SPARK_HOME}/sbin/spark-config.sh" /usr/local/bin/before-notebook.d/spark-config.sh

# Fix Spark installation for Java 11 and Apache Arrow library
# see: https://github.com/apache/spark/pull/27356, https://spark.apache.org/docs/latest/#downloading
RUN cp -p "$SPARK_HOME/conf/spark-defaults.conf.template" "$SPARK_HOME/conf/spark-defaults.conf" && \
    echo 'spark.driver.extraJavaOptions -Dio.netty.tryReflectionSetAccessible=true' >> $SPARK_HOME/conf/spark-defaults.conf && \
    echo 'spark.executor.extraJavaOptions -Dio.netty.tryReflectionSetAccessible=true' >> $SPARK_HOME/conf/spark-defaults.conf

# Install findspark
RUN pip install findspark

# Installing basic components
RUN sudo -E apt-get update && \
    sudo -E apt-get upgrade -y
RUN sudo -E apt-get install -y --no-install-recommends python3-dev default-libmysqlclient-dev build-essential libffi-dev gcc g++ && \
    sudo -E apt-get install -y --no-install-recommends libsasl2-dev libldap2-dev 
# Installing extra components
RUN sudo -E apt-get install -y --no-install-recommends libsasl2-dev libkrb5-dev && \
    sudo -E apt-get install -y gcc python3-dev python3-pip libxml2-dev libxslt1-dev && \
    sudo -E apt-get install -y zlib1g-dev g++ libmysqlclient-dev && \
    sudo -E apt-get install -y unixodbc-dev && \
    sudo -E apt-get install -y libsasl2-modules
WORKDIR $HOME

USER $NB_UID
# Fix pip import error
# Install pyhive and pyspark
# Install Tensorflow
# Install Nextfortune ML packages
# Install attrs
# Install BentoML
RUN pip install pip==22.0.4 && \
    pip install thrift && \
    pip install pyhive && \
    pip install pyspark && \
    pip install sasl -U && \
    pip install thrift_sasl -U && \
    pip install tensorflow-gpu==2.7.0 && \
    pip install vaex==4.9.1 && \
    pip install datatransformer && \
    pip install modelbricks && \
    pip install attrs -U && \
    pip install bentoml --pre 

From nextbiteam/nvidialab-base:1.0.2-ubuntu18.04-python3.7.6 as main
COPY --from=build /. /.
User root
RUN jupyter lab build
USER $NB_UID
WORKDIR $HOME
