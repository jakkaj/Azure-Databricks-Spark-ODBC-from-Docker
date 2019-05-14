# Azure-Databricks-Spark-ODBC-from-Docker
A Dockerfile to access Spark ODBC from .NET Core and others using UnixODBC and the Simba ODBC Driver


## Getting Started


### Get the Simba package
The Simba driver isn't open source, so you must download it and licence it yourself. 

Download the [Spark Simba ODBC Driver](https://www.simba.com/drivers/spark-jdbc-odbc/) (.deb file, 64 bit) and copy it in to the ODBCBase directory. Rename it to `simbaspark.deb`. Copy your license in to `SimbaApacheSparkODBCDriver.lic`. 

### Edit the odbc.ini file

Get a [token from Databricks](https://docs.databricks.com/user-guide/bi/jdbc-odbc-bi.html#username-password) and replace it in the PWD field. 

[Construct your JSBC URL](https://docs.databricks.com/user-guide/bi/jdbc-odbc-bi.html#http-path) and pop it in to the `HTTPPath` field. 

More information on connecting to Databricks using ODBC can be found [here](https://docs.databricks.com/user-guide/bi/jdbc-odbc-bi.html). 