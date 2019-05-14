# Using Azure Databricks Spark SQL via ODBC from Docker
A Dockerfile to access Spark ODBC from .NET Core and others using UnixODBC and the Simba ODBC Driver


## Getting Started


### Get the Simba package
The Simba driver isn't open source, so you must download it and licence it yourself. 

Download the [Spark Simba ODBC Driver](https://www.simba.com/drivers/spark-jdbc-odbc/) (.deb file, 64 bit) and copy it in to the ODBCBase directory. Rename it to `simbaspark.deb`. Copy your license in to `SimbaApacheSparkODBCDriver.lic`. 

### Edit the odbc.ini file

Get a [token from Databricks](https://docs.databricks.com/user-guide/bi/jdbc-odbc-bi.html#username-password) and replace it in the `PWD` field. 

[Construct your JSBC URL](https://docs.databricks.com/user-guide/bi/jdbc-odbc-bi.html#http-path) and pop it in to the `HTTPPath` field. 

More information on connecting to Databricks using ODBC can be found [here](https://docs.databricks.com/user-guide/bi/jdbc-odbc-bi.html). 

### Build the container

Now you should be able to build the container. 

Whilst still in the `ODBCBase` directory.

```
docker build -t odbcbase .
```

Once that builds you're ready to test. 

### Test the container base image

Run the image up by typing `docker run -it --rm odbcbase bash`. This will leave you at a bash prompt. 

Type `isql -v Spark` to run the Spark DSN from the odbc.ini file. 

This should leave uou sitting at an SQL prompt much like the following:

```
SQL>
```

From here you can execute Spark SQL commands!

### Debugging

If you have problems, you might need to debug the connection. 

Edit `odbc.ini` and uncomment the two `trace` lines near the top. Save it and re-run the `isql` command. Once it has failed, take a look in `/tmp/sql.log` to see if there are any clues to your problem. 

### odbcinst

You can use the UnixODBC `odbcinst` tool to check which config files are being used. Run `odbcinst -j` for a list of current odbc configs. 