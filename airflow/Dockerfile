
FROM apache/airflow:2.6.1-python3.10
ENV PIP_ROOT_USER_ACTION=ignore
#USER airflow
COPY requirements.txt /
# RUN pip install --no-cache-dir "apache-airflow==${AIRFLOW_VERSION}" -r /requirements.txt --root-user-action=ignore


USER root
#RUN sudo su
# install java 17

RUN apt-get update \
            &&  apt-get install -y ca-certificates-java  openjdk-11-jdk ant

#Install ODBC
RUN apt-get update \
        && apt-get install -y curl wget unzip apt-transport-https gnupg2 nano libaio1 libnsl2 iputils-ping\
        && curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
        && curl https://packages.microsoft.com/config/debian/11/prod.list > /etc/apt/sources.list.d/mssql-release.list \
        && apt-get update \
        && ACCEPT_EULA=Y apt-get install -y msodbcsql18 \
        && ACCEPT_EULA=Y apt-get install -y mssql-tools18 \
        && apt-get install -y unixodbc-dev \
        && apt-get install -y libgssapi-krb5-2


