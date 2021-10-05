FROM jupyter/scipy-notebook

#ENV NODE_OPTIONS="--max-old-space-size=4096"

#install git extension
RUN pip install --upgrade jupyterlab-git
RUN pip install tableauserverclient

RUN jupyter labextension install nbdime-jupyterlab --no-build
RUN jupyter labextension install @jupyterlab/git --no-build
RUN jupyter lab build && \
    jupyter lab clean && \
    jlpm cache clean && \
    npm cache clean --force && \
    rm -rf $HOME/.node-gyp && \
    rm -rf $HOME/.local && \
    fix-permissions $CONDA_DIR $HOME
RUN jupyter server extension list

#install sql driver
USER root

RUN sudo apt-get update && \
    sudo apt-get -y upgrade && \
    sudo apt-get install -y curl
RUN sudo apt-get install -y gnupg
RUN sudo curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN sudo curl https://packages.microsoft.com/config/ubuntu/20.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
RUN sudo apt-get -y update
RUN sudo ACCEPT_EULA=Y apt-get install -y msodbcsql17

#install packages
RUN conda install -y -c conda-forge pyodbc
RUN conda install -y -c conda-forge pycrypto
RUN conda install -y -c anaconda pymssql
RUN conda install -y -c conda-forge pyarrow=3.0.0
RUN conda install -y -c conda-forge turbodbc

USER ${NB_USER}
