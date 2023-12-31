---
title: "plsql-db2"
---

Here's a table comparing DB2 and PL/SQL based on the provided features and their syntax:

These SQL commands are mainly categorized into five categories: 

1. DDL – Data Definition Language
1. DQL – Data Query Language
1. DML – Data Manipulation Language
1. DCL – Data Control Language
1. TCL – Transaction Control Language

![](https://media.geeksforgeeks.org/wp-content/uploads/20210920153429/new.png)

## Basic SQL commands:

1. DDL – Data Definition Language
   
    | Feature                | PL/SQL Syntax                   | DB2 Syntax                      |
    |------------------------|---------------------------------|---------------------------------|
    | Create Table           | `CREATE TABLE new_table AS SELECT * FROM existing_table;` | `similar` |
    | Drop Table             | `DROP TABLE table_name [PURGE];`       | `DROP TABLE IF EXISTS table_name;`       |
    | Rename Columns         | `ALTER TABLE table_name RENAME COLUMN old_column TO new_column;` | `similar` |
    | Modify Columns         | `ALTER TABLE table_name MODIFY COLUMN column_name datatype;` | `similar` |
    | Add Columns            | `ALTER TABLE table_name ADD COLUMN new_column datatype;` | `similar` |

2. DQL – Data Query Language
    
    | Feature                | PL/SQL Syntax                   | DB2 Syntax                      |
    |------------------------|---------------------------------|---------------------------------|
    | Left Join              | `SELECT * FROM table1 LEFT JOIN table2 ON table1.column = table2.column;` | `similar` |
    | Inner Join             | `SELECT * FROM table1 INNER JOIN table2 ON table1.column = table2.column;` | `similar`|
    | Full Join              | `SELECT * FROM table1 FULL JOIN table2 ON table1.column = table2.column;` | `similar`|
    | Anti Join              | `SELECT column1, column2 FROM table1 WHERE NOT EXISTS (SELECT * FROM table2 WHERE table1.column = table2.column)`         | `similar` |
    | Merge                  | `MERGE INTO table_name USING source_table ON (table_name.column = source_table.column) WHEN MATCHED THEN UPDATE SET column1 = value1 WHEN NOT MATCHED THEN INSERT (column1) VALUES (value1);` | `similar` |
    | Insert Into            | `INSERT INTO table_name (column1, column2) VALUES (value1, value2);` | `similar` |
    | Update                 | `UPDATE staff a SET salary = (SELECT AVG(salary) + 2000 FROM staff b WHERE a.dept = b.dept) WHERE id < 60;` | `similar`|
    | Truncate Table         | `TRUNCATE TABLE table_name;`   | `TRUNCATE TABLE table_name IMMEDIATE;`   |
    | Temporary Table        | `DECLARE GLOBAL TEMPORARY TABLE table_name (column1 datatype, column2 datatype);` | `CREATE GLOBAL TEMPORARY TABLE table_name (column1 datatype, column2 datatype);` |
    | Group By               | `SELECT column1, COUNT(*) FROM table_name GROUP BY column1;` | `similar` |
    | Partition By           | `SELECT column1, RANK() OVER (PARTITION BY column2 ORDER BY column3) FROM table_name;` | `similar` |
    | Run Procedure          | `EXECUTE procedure_name;`       | `CALL procedure_name();`       |
    | Loop                   | `FOR row IN (SELECT * FROM table_name) LOOP <statements> END LOOP;` | `FOR row AS cursor_name CURSOR FOR SELECT * FROM table_name DO <statements> END FOR;` |
    | Parallel               | ` INSERT /*+APPEND PARALLEL(8)*/ INTO` |`SELECT * FROM table_name PARALLEL 4;` | 
    |                        | `MERGE /*+ parallel(8) */ INTO `  |  | 
    |                        | `SELECT /*+ PARALLEL(8) */ * FROM ` |  | 

4. DCL – Data Control Language

    | Feature                | PL/SQL Syntax                   | DB2 Syntax                      |
    |------------------------|---------------------------------|---------------------------------|
    | Select                 | `SELECT column1, column2 FROM table_name;` | `similar` |


## Utilities

| Feature                | PL/SQL Syntax                   | DB2 Syntax                      |
|------------------------|---------------------------------|---------------------------------|
| SYS_INFO               |  | `SELECT * FROM SYSIBMADM.ENV_SYS_INFO` |
| NVL                    | `NVL(column, 0)` | `COALESCE(column, 0)` |
|                        | `COALESCE(column, 0)` | `COALESCE(column, 0)` |
| Diff Month             | `SELECT (EXTRACT(YEAR FROM end_date) - EXTRACT(YEAR FROM start_date)) * 12 + EXTRACT(MONTH FROM end_date) - EXTRACT(MONTH FROM start_date) AS month_diff FROM your_table;`         | `SELECT (YEAR(end_date) - YEAR(start_date)) * 12 + MONTH(end_date) - MONTH(start_date) AS month_diff FROM your_table;` |
| Add Months             | `SELECT ADD_MONTHS(date1, number_of_months) FROM dual;`        | `SELECT ADD_YEARS(current_date, 3), ADD_MONTHS(current_date, 3 ), ADD_DAYS(current_date, 3), ADD_HOURS(current timestamp, 3), ADD_MINUTES(current timestamp, 3), ADD_SECONDS(current timestamp, 3) FROM sysibm.sysdummy1;` |
| Diff Date              | `SELECT date2 - date1 FROM dual;`         |  |
| Compare 2 Tables       | `(SELECT * FROM B_TMP MINUS SELECT * FROM B_TMP1) UNION ALL(SELECT * FROM B_TMP1 MINUS SELECT * FROM B_TMP)` |  `SELECT * FROM table1 EXCEPT SELECT * FROM table2;` |

## References

- [db2-sql-cookbook](http://db2-sql-cookbook.org/pdf/Db2_SQL_Cookbook.pdf)
  
