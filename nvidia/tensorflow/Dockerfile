From nvidialab-base:1.0.0-python3.8

USER root

RUN sudo rm /etc/apt/sources.list.d/cuda.list
RUN sudo -E apt-key del 7fa2af80
RUN sudo -E apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/3bf863cc.pub
RUN sudo -E apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu2004/x86_64/7fa2af80.pub

## Installing basic components
RUN sudo -E apt-get  update && \
    sudo -E apt-get upgrade -y
RUN sudo -E apt-get install -y --no-install-recommends python3-dev default-libmysqlclient-dev build-essential libffi-dev gcc g++ && \
    sudo -E apt-get install -y --no-install-recommends libsasl2-dev libldap2-dev && \
## Installing extra components
RUN sudo -E apt-get install -y --no-install-recommends libsasl2-dev libkrb5-dev && \
    sudo -E apt-get install -y gcc python3-dev python3-pip libxml2-dev libxslt1-dev && \
    sudo -E apt-get install -y  zlib1g-dev g++ libmysqlclient-dev && \
    sudo -E apt-get install -y unixodbc-dev && \
    sudo -E apt-get install -y libsasl2-modules

USER ${NB_UID}
# Install pyhive and pyspark
RUN pip install thrift && \
    pip install pyhive && \
    pip install pyspark && \
    pip install sasl -U && \
    pip install thrift_sasl -U
# Install Tensorflow
RUN pip install tensorflow-gpu==2.7.0
# Install Nextfortune ML packages
RUN pip install datatransformer && \
    pip install modelbricks
# Install attrs
RUN pip install attrs -U
# Install BentoML
RUN pip install bentoml --pre
