# SQLSERVER-SNIPPET


### PARALEL
```sql
OPTION(USE HINT('ENABLE_PARALLEL_PLAN_PREFERENCE'))
```
### INFORMATION_SCHEMA

```sql
SELECT *
FROM INFORMATION_SCHEMA.TABLES;

USE [IFRS9_CUSTOMER];
GO

SELECT *
FROM INFORMATION_SCHEMA.COLUMNS
WHERE upper(COLUMN_NAME) LIKE '%AVG_COLL%';

SELECT *
FROM [IFRS9_CUSTOMER]..[b_tmp_tbl_info]
WHERE upper(ColumnName) LIKE '%CASH_TXN_RT%';
```

### LAG - LEAD

```sql
LAG(return_value ,offset [,default]) 
OVER (
    [PARTITION BY partition_expression, ... ]
    ORDER BY sort_expression [ASC | DESC], ...
)

-- lag 6
lead(CUST_LMT, 6) OVER (
		PARTITION BY [CUSTOMER_ID] ORDER BY [PROCESS_DATE] DESC
		)


-- moving aveage
CASE WHEN row_number() OVER (
              PARTITION BY CUSTOMER_ID ORDER BY [PROCESS_DATE] ASC
              ) >= 3 -- chi lay nhung TH du 3 thang tro len
              THEN avg(NUM_CASH_TXN) OVER (
                PARTITION BY CUSTOMER_ID ORDER BY [PROCESS_DATE] ASC rows BETWEEN 2 preceding
                  AND CURRENT row
                )
		END AS MovingAvg


```

### rename column
```sql
sp_rename 'table_name.old_column_name'
	,'new_column_name'
	,'COLUMN';

sp_rename '[IFRS9_CUSTOMER]..[B_CUSTOMER].[COLL_VAL_CTR (Contribution)]'
	,'COLL_VAL_CTR'
	,'COLUMN';

sp_rename '[IFRS9_CUSTOMER]..[B_CUSTOMER].[CUST_LMT]'
	,'CUST_LMT_UTIL'
	,'COLUMN';
```

### add column

```sql
ALTER TABLE table_name ADD column_name1 datatype
	,column_name2 datatype;

ALTER TABLE [IFRS9_CUSTOMER]..[B_CUSTOMER] ADD OS_PCT_OD_CURR FLOAT;
```

### drop table
```sql
DROP TABLE
IF EXISTS [IFRS9_CUSTOMER]..[b_tmp];
```
### update from another table 
```sql
UPDATE
    Sales_Import
SET
    Sales_Import.AccountNumber = RAN.AccountNumber
FROM
    Sales_Import SI
INNER JOIN
    RetrieveAccountNumber RAN
ON 
    SI.LeadID = RAN.LeadID;
```

### Convert Date

```sql
-- convert float to date
,CONVERT(DATE, CONVERT(VARCHAR(10), CONVERT(INT, [MSR_PRD_ID])))
-- convert int to date 
,CONVERT(DATETIME, MTH_SNC_10DPD_L6)
-- convert string to date
,CONVERT(DATETIME, CONVERT(FLOAT, MTH_SNC_10DPD_L6))
```

### Month between 
```sql
DATEDIFF(MONTH, START_DATE, END_DATE)
-- 
CASE WHEN DATEPART(DAY, @Start_date) > DATEPART(DAY, @End_date)
	THEN DATEDIFF(MONTH, @Start_date, @End_date) - 1
	ELSE DATEDIFF(MONTH, @Start_date, @End_date)
	END
```
