FROM nextbiteam/jupyterlab-datascience:3.1.6-python3.8

# Fix DL4006
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

# Install ML packages
RUN pip install --upgrade xgboost && \
    pip install --upgrade lightgbm && \
    pip install tpot==0.11.7
RUN conda install -y -c conda-forge mlxtend=0.18.0

USER $NB_UID

WORKDIR $HOME

