# oracle odbc connection template for R

Not a package, just some tips to connect R, DBI and dplyr to an Oracle database with odbc::odbc

See [here](https://guillaumepressiat.github.io/blog/2019/11/oraclyr) for full explanation. 
Most importantly: if your Oracle client is 32b, then use R 32b.

Then you can use dplyr on oracle tables:

```r
dplyr::tbl(my_oracle, dbplyr::in_schema('SCHEMA_ONE', 'TB_ONE'))
```

And even use dblinks

```r
dplyr::tbl(my_oracle, dbplyr::in_schema('SCHEMA_B', 'TC_TWO@MYDBTWOLINK'))
```

## Connect to Oracle with odbc via connection string

```r
library(odbc)
library(dplyr)
library(dbplyr)
 
my_oracle <- dbConnect(odbc::odbc(), 
                       .connection_string = "Driver={Oracle dans OraClient10g_home1};DBQ=host:port/db_name;UID=woo;PWD=hoo", 
                       timeout = 10)
```

## Connect to Oracle with odbc specifying parameters directly

```r
library(odbc)
library(dplyr)
library(dbplyr)
library(lubridate)
 
my_oracle <- dbConnect(odbc::odbc(),
                       Driver = "Oracle dans OraClient10g_home1",
                       DBQ = "host:port/db_name",
                       SVC = "DB_SCHEMA", # schema when connection opens
                       UID = "woo",
                       PWD = "hoo")
``` 

Ask for password:

```r
library(odbc)
library(dplyr)
library(dbplyr)
library(lubridate)
 
my_oracle <- dbConnect(odbc::odbc(),
                       Driver = "Oracle dans OraClient10g_home1",
                       DBQ = "host:port/db_name",
                       SVC = "DB_SCHEMA", 
                       UID = rstudioapi::askForPassword('woo (username)'),
                       PWD = rstudioapi::askForPassword('Open, Sesame (password)'))
```

See here for more details

