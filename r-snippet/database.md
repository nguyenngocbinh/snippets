---
title: database
---

## dbplyr
### list connection driver
```r
odbc::odbcListDrivers()
```

### Connect to DB
```r
library(DBI)
con <- DBI::dbConnect(odbc::odbc(), "BILIVE", UID="JUMP_B", PWD="******")
```

### list table
```r
dbListTables(con, schema = "JUMP_B")
dbListTables(con, schema = "SB_BI")
```

### push table into database
```r
dbWriteTable(con, "mtcars", mtcars[1:5, ])
```

## RODBC

### Connect to DB
```r
library(RODBC)
channel <- odbcConnect('BILIVE',
                   uid = 'JUMP_B',
                   pwd = '******')
```

### Get data
```r
cus <- sqlQuery(con, "select /*+ PARALLEL(11) */ * from nnb_cus") 
```
_This function load all rows_
