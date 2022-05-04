FROM jupyter/scipy-notebook:python-3.8.8

#Fix typing-extensions version and Install pylint
RUN pip install typing-extensions==3.10.0.2 && \
    pip install pylint

# Install tableau server client
RUN pip install tableauserverclient==0.16.0

# Install git extension
RUN pip install --upgrade jupyterlab-git && \
    pip install --upgrade jupyterlab_nvdashboard && \
    jupyter labextension install nbdime-jupyterlab --no-build && \
    jupyter labextension install @jupyterlab/git --no-build
RUN jupyter lab build && \
    jupyter lab clean && \
    jlpm cache clean && \
    npm cache clean --force && \
    rm -rf $HOME/.node-gyp && \
    rm -rf $HOME/.local && \
    fix-permissions $CONDA_DIR $HOME
RUN jupyter server extension list

USER root

ENV NVARCH x86_64
ENV NVIDIA_REQUIRE_CUDA "cuda>=11.6 brand=tesla,driver>=418,driver<419 brand=tesla,driver>=440,driver<441 brand=tesla,driver>=450,driver<451  brand=tesla,driver>=460,driver<461 brand=tesla,driver>=470,driver<471"

LABEL maintainer "NVIDIA CORPORATION <cudatools@nvidia.com>"

RUN echo ${NVARCH}
RUN apt-get update && \
    apt-get install -y --no-install-recommends gnupg2 curl ca-certificates
RUN sudo -E curl -fsSL https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/7fa2af80.pub | apt-key add -
RUN echo "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/ /"
RUN echo "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/ /" > /etc/apt/sources.list.d/cuda.list
RUN apt-get purge --autoremove -y curl \
    && rm -rf /var/lib/apt/lists/*

ENV CUDA_VERSION 11.6.0

# For libraries in the cuda-compat-* package: https://docs.nvidia.com/cuda/eula/index.html#attachment-a
RUN apt-get update && apt-get install -y --no-install-recommends \
    cuda-cudart-11-6=11.6.55-1 \
    cuda-compat-11-6 \
    && ln -s cuda-11.6 /usr/local/cuda && \
    rm -rf /var/lib/apt/lists/*

# Required for nvidia-docker v1
RUN echo "/usr/local/nvidia/lib" >> /etc/ld.so.conf.d/nvidia.conf \
    && echo "/usr/local/nvidia/lib64" >> /etc/ld.so.conf.d/nvidia.conf

ENV PATH /usr/local/nvidia/bin:/usr/local/cuda/bin:${PATH}
ENV LD_LIBRARY_PATH /usr/local/nvidia/lib:/usr/local/nvidia/lib64

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES compute,utility

#fix no libcudnn
RUN sudo -E apt-get update
RUN sudo -E apt-get install -y software-properties-common
RUN sudo -E apt update

RUN sudo -E wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin && \
    sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600 && \
    sudo -E apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/7fa2af80.pub && \
    sudo -E add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/ /"

RUN sudo -E apt-get update
RUN sudo -E apt-get install libcudnn8 && \
    sudo -E apt-get install libcudnn8-dev

RUN sudo -E apt-get install -y nvidia-cuda-toolkit

RUN cd /usr/lib/x86_64-linux-gnu/ && \
    sudo ln -s libcublas.so.10.2.1.243 libcublas.so.11 && \
    sudo ln -s libcublasLt.so.10.2.1.243 libcublasLt.so.11 && \
    sudo ln -s libcusolver.so.10.2.0.243 libcusolver.so.11 && \
    sudo ln -s libcusparse.so.10.3.0.243 libcusparse.so.11

#Install odbc mssql driver
RUN sudo -E apt-get -y update && \
    sudo -E apt-get -y upgrade && \
    sudo -E apt-get install -y curl && \
    sudo -E apt-get install -y gnupg && \
    sudo -E apt-get install -y vim
RUN sudo -E curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN sudo -E curl https://packages.microsoft.com/config/ubuntu/20.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
RUN sudo -E apt-get -y update && \
    sudo -E ACCEPT_EULA=Y apt-get install -y msodbcsql17

# Install packages
RUN conda install -y -c conda-forge pyodbc && \
    conda install -y -c conda-forge pycrypto && \
    conda install -y -c anaconda pymssql

# Install support package for turbodbc
RUN conda install -y -c conda-forge pyarrow=3.0.0
RUN conda install -y -c conda-forge turbodbc


USER ${NB_UID}
