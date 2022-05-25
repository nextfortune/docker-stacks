FROM jupyter/base-notebook:ubuntu-18.04 as build
# Fix typing-extensions version and Install pylint
# Install tableau server client
RUN pip install typing-extensions==4.2.0 && \
    pip install pylint && \
    pip install tableauserverclient==0.16.0 && \
    pip install jupyter-server==1.6.4 && \
    pip install jupyterlab-git==0.22.1

USER root
# Install git extension
RUN jupyter labextension install nbdime-jupyterlab --no-build
RUN jupyter lab build && \
    jupyter lab clean && \
    jlpm cache clean && \
    npm cache clean --force && \
    rm -rf $HOME/.node-gyp && \
    rm -rf $HOME/.local && \
    fix-permissions $CONDA_DIR $HOME

# Install Nvidia driver and cudnn 
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    apt update

RUN wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
RUN mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
RUN apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/3bf863cc.pub && \
    add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/ /"

RUN wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
RUN apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/7fa2af80.pub && \
    apt install ./nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb

RUN wget https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/libnvinfer7_7.1.3-1+cuda11.0_amd64.deb
RUN apt install ./libnvinfer7_7.1.3-1+cuda11.0_amd64.deb -y && \
    apt-get update

# Install development and runtime libraries (~4GB)
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends --allow-downgrades \
    cuda-11-0  \
    libcudnn8=8.0.4.30-1+cuda11.0  \
    libcudnn8-dev=8.0.4.30-1+cuda11.0

# Reboot. Check that GPUs are visible using the command: nvidia-smi

# Install TensorRT. Requires that libcudnn8 is installed above.
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends --allow-downgrades \
    libnvinfer7=7.1.3-1+cuda11.0 \
    libnvinfer-dev=7.1.3-1+cuda11.0 \
    libnvinfer-plugin7=7.1.3-1+cuda11.0

RUN cd /usr/lib/x86_64-linux-gnu/ && \
    ln -s libcublas.so.10.2.1.243 libcublas.so.11 && \
    ln -s libcublasLt.so.10.2.1.243 libcublasLt.so.11 && \
    ln -s libcusparse.so.10.3.0.243 libcusparse.so.11 && \
    ln -s /usr/local/cuda-11.0/targets/x86_64-linux/lib/libcusolver.so.10 libcusolver.so.11 && \
    ln -s /usr/local/cuda-11.0/targets/x86_64-linux/lib/libcudart.so.11.0 libcudart.so.11.0 && \
    rm -rf /var/lib/apt/lists/*

#Install odbc mssql driver
RUN sudo -E apt-get -y update && \
    sudo -E apt-get -y upgrade && \
    sudo -E apt-get install -y curl && \
    sudo -E apt-get install -y gnupg && \
    sudo -E apt-get install -y vim
RUN sudo -E curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    sudo -E curl https://packages.microsoft.com/config/ubuntu/20.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
RUN sudo -E apt-get -y update && \
    sudo -E ACCEPT_EULA=Y apt-get install -y msodbcsql17

# Install pyodbc and turodbc
RUN conda install -y -c conda-forge pyodbc && \
    conda install -y -c conda-forge turbodbc

# USER $NB_UID
USER root
RUN pip install pycrypto && \
    pip install pymssql && \
    pip install numpy==1.20.3 -U && \
    pip install pandas==1.3.3 -U && \
    pip install pyarrow==4.0.1 -U
WORKDIR $HOME
USER $NB_UID

FROM jupyter/scipy-notebook:ubuntu-18.04 as main
COPY --from=build /. /.
User root
RUN jupyter lab build
USER $NB_UID
WORKDIR $HOME
