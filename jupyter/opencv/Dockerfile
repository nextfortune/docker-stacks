FROM nextbiteam/jupyterlab-general:3.1.8-python3.8

# Install OpenCV
USER root
RUN pip install --quiet --no-cache-dir \
    'opencv-python==4.6.0.66'

USER $NB_UID
