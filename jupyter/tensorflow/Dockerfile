FROM nextbiteam/jupyterlab-general:3.1.8-python3.8

# Install Tensorflow
USER root
RUN pip install --quiet --no-cache-dir \
    'tensorflow==2.7.0' && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

USER $NB_UID
# Install Nextfortune ML packages
RUN pip install datatransformer && \
    pip install modelbricks
