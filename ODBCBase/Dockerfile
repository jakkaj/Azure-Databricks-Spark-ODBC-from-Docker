################################
# This Dockerfile demonstrates setting up Spark SQL ODBC in a container
# Please see the GitHub repo for more
# https://github.com/jakkaj/Azure-Databricks-Spark-ODBC-from-Docker 
################################

FROM ubuntu:14.04


RUN apt-get update 

RUN apt-get install -y odbcinst1debian2 libodbcinstq4-1

RUN apt-get install -y unixodbc-dev unixodbc-bin unixodbc 
RUN apt-get install -y libsasl2-2 libsasl2-modules-gssapi-mit

COPY ./simbaspark.deb /simba/simbaspark.deb

WORKDIR /simba

RUN dpkg -i simbaspark.deb

COPY ./odbc.ini /odbc.ini
COPY ./simba.sparkodbc.ini /opt/simba/spark/lib/64/simba.sparkodbc.ini
COPY ./SimbaApacheSparkODBCDriver.lic /opt/simba/spark/lib/64/SimbaApacheSparkODBCDriver.lic

ENV ODBCINI /odbc.ini
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:/usr/lib/x86_64-linux-gnu
ENV SIMBASPARKINI /opt/simba/spark/lib/64/simba.sparkodbc.ini 

RUN ln -s /opt/simba/spark /opt/simba/sparkodbc

####.NET Bits
RUN apt-get install -y wget

RUN wget -q https://packages.microsoft.com/config/ubuntu/14.04/packages-microsoft-prod.deb
RUN sudo dpkg -i packages-microsoft-prod.deb

RUN apt-get install -y apt-transport-https
RUN apt-get update
RUN apt-get install -y dotnet-sdk-2.2