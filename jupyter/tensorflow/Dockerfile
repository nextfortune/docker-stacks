ARG BASE_CONTAINER=timsu27/jupyter-general:1.0.4-python3.8
FROM $BASE_CONTAINER

# Install Tensorflow
USER root
RUN pip install --quiet --no-cache-dir \
    'tensorflow==2.6.0' && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

USER $NB_UID
# Install Nextfortune ML packages
RUN pip install datatransformer && \
    pip install modelbricks
