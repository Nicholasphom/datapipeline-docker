
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

# #INSTALL Oracle instant client
# RUN wget --no-verbose -O oracle_instant_client.zip "https://download.oracle.com/otn_software/linux/instantclient/1919000/instantclient-basic-linux.x64-19.19.0.0.0dbru.zip" \
# && mkdir -p /opt/oracle \
# && unzip oracle_instant_client.zip -d /opt/oracle \
# && rm oracle_instant_client.zip

# # Install MSSql Jar
# RUN wget --no-verbose -O mssql.zip "https://go.microsoft.com/fwlink/?linkid=2223050" \
# && unzip mssql.zip -d /opt \
# && rm mssql.zip

# #Install Sql Plus 
# RUN wget --no-verbose -O sqlplus.zip "https://download.oracle.com/otn_software/linux/instantclient/1919000/instantclient-sqlplus-linux.x64-19.19.0.0.0dbru.zip" \
# && unzip sqlplus.zip -d /opt/oracle 
# # Link Client run to ssqlplus
# RUN sh -c "echo /opt/oracle/instantclient_19_19 > /etc/ld.so.conf.d/oracle-instantclient.conf"
# RUN ldconfig

# #add path to run sql plus anywhere
# RUN chmod 777 /opt/oracle/instantclient_19_19/sqlplus
# ENV PATH="$PATH:/opt/oracle/instantclient_19_19"
# RUN echo $PATH

# # use orapki anywhere
# ADD ./oracle_scripts/orapki /opt/oracle/oracle_scripts/orapki
# RUN chmod 777 /opt/oracle/oracle_scripts/orapki
# ENV PATH="$PATH:/opt/oracle/oracle_scripts/orapki"
# RUN echo $PATH

# #Oracle_Home

# ENV ORACLE_HOME="/opt/oracle/instantclient_19_19"
# ENV PATH="$PATH:/opt/mssql-tools18/bin"
# ENV LD_LIBRARY_PATH = "/opt/oracle/instantclient_19_19:$LD_LIBRARY_PATH"
# ENV TNS_ADMIN = "/opt/oracle/instantclient_19_19/network/admin"
# ENV ORACLE_SID ="SAWSREPO.CALSAWS"
# #RUN export PATH="$PATH:/opt/mssql-tools18/bin"; echo $PATH
# RUN echo $PATH

# ## ADD JARS AND CERTS
# ADD ./oracle_jars /opt/oracle/instantclient_19_19/lib
# RUN mkdir /opt/oracle/instantclient_19_19/certs
# ADD ./oracle_certs /opt/oracle/instantclient_19_19/certs
# ADD ./oracle_files /opt/oracle/instantclient_19_19/network/admin
# # CREATE WALLET AND ADD CERTS
# RUN mkdir -p /opt/oracle/instantclient_19_19/wallet
# RUN cd /opt/oracle/instantclient_19_19/wallet \
# && /opt/oracle/oracle_scripts/orapki wallet create -wallet nickwallet -auto_login -pwd dashydash123 \
# && /opt/oracle/oracle_scripts/orapki wallet add -wallet nickwallet -trusted_cert -cert /opt/oracle/instantclient_19_19/certs/usawcwopr100_production_calwin_org.crt -pwd dashydash123 \
# && /opt/oracle/oracle_scripts/orapki wallet add -wallet nickwallet -trusted_cert -cert /opt/oracle/instantclient_19_19/certs/usawcwopr100_production_calwin_org.ca-bundle -pwd dashydash123 
# RUN chmod 777 -R /opt/oracle/instantclient_19_19/wallet
# # All folders viewable my airflow user
# RUN chown airflow -R /opt/oracle
