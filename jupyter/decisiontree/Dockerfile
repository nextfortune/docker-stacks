ARG BASE_CONTAINER=timsu27/jupyter-datascience:1.0.4-python3.8
FROM $BASE_CONTAINER

# Fix DL4006
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER $NB_UID
# Install ML packages
RUN pip install --upgrade xgboost && \
    pip install --upgrade lightgbm && \
    pip install tpot==0.11.7
RUN conda install -y -c conda-forge mlxtend=0.18.0

WORKDIR $HOME
