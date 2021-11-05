FROM jupyter/scipy-notebook:python-3.8.8

# Install tableau server client
RUN pip install tableauserverclient==0.16.0

# Install git extension
RUN pip install --upgrade jupyterlab-git && \
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

# Install odbc mssql driver
USER root

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

USER $NB_UID

#USER root