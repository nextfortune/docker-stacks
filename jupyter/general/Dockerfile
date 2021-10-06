FROM timsu27/jupyter-base:3.1.6-python3.8

# Install Airflow
## Airflow install ENV
ENV AIRFLOW_BASICS="async,amazon,celery,cncf.kubernetes,docker,dask,elasticsearch,ftp,grpc,hashicorp,http,ldap,google,microsoft.azure,mysql,postgres,redis,sendgrid,sftp,slack,ssh,statsd,virtualenv" \
    AIRFLOW_VERSION="2.1.0" \
    PYTHON_VERSION="3.8" \
    CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"

USER root

## Installing basic components
RUN sudo -E apt-get install -y --no-install-recommends python3-dev default-libmysqlclient-dev build-essential libffi-dev gcc g++ && \
    sudo -E apt-get install -y --no-install-recommends libsasl2-dev libldap2-dev
RUN pip install --no-cache-dir "apache-airflow[${AIRFLOW_BASICS}]==${AIRFLOW_VERSION}" \
        --constraint  "https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"

## Installing extra components
COPY ./requirements.txt .
RUN sudo -E apt-get  update && \
    sudo -E apt-get upgrade -y && \
    sudo -E apt-get install -y --no-install-recommends libsasl2-dev libkrb5-dev && \
    sudo -E apt-get install -y gcc python3-dev python3-pip libxml2-dev libxslt1-dev && \
    sudo -E apt-get install -y  zlib1g-dev g++ libmysqlclient-dev && \
    sudo -E apt-get install -y unixodbc-dev && \
    pip install  -r ./requirements.txt

# Install bentoml
RUN pip install bentoml==0.13.1

# Install pylint
RUN pip install pylint==2.11.1
USER $NB_UID
