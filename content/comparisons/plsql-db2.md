---
title: So sánh PL/SQL (Oracle) và DB2 (IBM) - Hướng dẫn cú pháp SQL
---

Bảng so sánh **<span style="color: #28A745;">PL/SQL (Oracle)</span>** và **<span style="color: #17A2B8;">DB2 (IBM)</span>** dựa trên các tính năng và cú pháp được cung cấp:

## 🗃️ **Phân loại lệnh SQL**

Các lệnh SQL chủ yếu được phân thành 5 loại:

1. **<span style="color: #DC3545;">DDL</span>** – Data Definition Language *(Ngôn ngữ định nghĩa dữ liệu)*
2. **<span style="color: #28A745;">DQL</span>** – Data Query Language *(Ngôn ngữ truy vấn dữ liệu)*
3. **<span style="color: #FFC107;">DML</span>** – Data Manipulation Language *(Ngôn ngữ thao tác dữ liệu)*
4. **<span style="color: #17A2B8;">DCL</span>** – Data Control Language *(Ngôn ngữ kiểm soát dữ liệu)*
5. **<span style="color: #6F42C1;">TCL</span>** – Transaction Control Language *(Ngôn ngữ kiểm soát giao dịch)*

![](https://media.geeksforgeeks.org/wp-content/uploads/20210920153429/new.png)

## 🔧 **Lệnh SQL cơ bản:**

### 1. 🏗️ **DDL – Data Definition Language**
   
| **Chức năng** | **<span style="color: #28A745;">PL/SQL (Oracle)</span>** | **<span style="color: #17A2B8;">DB2 (IBM)</span>** |
|---------------|-----------------------------------------------------------|-----------------------------------------------------|
| **<span style="color: #DC3545;">Create Table</span>** *(Tạo bảng)* | `CREATE TABLE new_table AS SELECT * FROM existing_table;` | `similar` *(tương tự)* |
| **<span style="color: #DC3545;">Drop Table</span>** *(Xóa bảng)* | `DROP TABLE table_name [PURGE];` | `DROP TABLE IF EXISTS table_name;` |
| **<span style="color: #DC3545;">Rename Columns</span>** *(Đổi tên cột)* | `ALTER TABLE table_name RENAME COLUMN old_column TO new_column;` | `similar` *(tương tự)* |
| **<span style="color: #DC3545;">Modify Columns</span>** *(Chỉnh sửa cột)* | `ALTER TABLE table_name MODIFY COLUMN column_name datatype;` | `similar` *(tương tự)* |
| **<span style="color: #DC3545;">Add Columns</span>** *(Thêm cột)* | `ALTER TABLE table_name ADD COLUMN new_column datatype;` | `similar` *(tương tự)* |

### 2. 🔍 **DQL – Data Query Language**
    
| **Chức năng** | **<span style="color: #28A745;">PL/SQL (Oracle)</span>** | **<span style="color: #17A2B8;">DB2 (IBM)</span>** |
|---------------|-----------------------------------------------------------|-----------------------------------------------------|
| **<span style="color: #007ACC;">Left Join</span>** *(Nối trái)* | `SELECT * FROM table1 LEFT JOIN table2 ON table1.column = table2.column;` | `similar` *(tương tự)* |
| **<span style="color: #007ACC;">Inner Join</span>** *(Nối trong)* | `SELECT * FROM table1 INNER JOIN table2 ON table1.column = table2.column;` | `similar` *(tương tự)* |
| **<span style="color: #007ACC;">Full Join</span>** *(Nối đầy đủ)* | `SELECT * FROM table1 FULL JOIN table2 ON table1.column = table2.column;` | `similar` *(tương tự)* |
| **<span style="color: #007ACC;">Anti Join</span>** *(Nối ngược)* | `SELECT column1, column2 FROM table1 WHERE NOT EXISTS (SELECT * FROM table2 WHERE table1.column = table2.column)` | `similar` *(tương tự)* |
| **<span style="color: #FF6B35;">Merge</span>** *(Hợp nhất)* | `MERGE INTO table_name USING source_table ON (table_name.column = source_table.column) WHEN MATCHED THEN UPDATE SET column1 = value1 WHEN NOT MATCHED THEN INSERT (column1) VALUES (value1);` | `similar` *(tương tự)* |
| **<span style="color: #FF6B35;">Insert Into</span>** *(Chèn dữ liệu)* | `INSERT INTO table_name (column1, column2) VALUES (value1, value2);` | `similar` *(tương tự)* |
| **<span style="color: #FF6B35;">Update</span>** *(Cập nhật)* | `UPDATE staff a SET salary = (SELECT AVG(salary) + 2000 FROM staff b WHERE a.dept = b.dept) WHERE id < 60;` | `similar` *(tương tự)* |
| **<span style="color: #E83E8C;">Truncate Table</span>** *(Xóa dữ liệu)* | `TRUNCATE TABLE table_name;` | `TRUNCATE TABLE table_name IMMEDIATE;` |
| **<span style="color: #20C997;">Temporary Table</span>** *(Bảng tạm)* | `DECLARE GLOBAL TEMPORARY TABLE table_name (column1 datatype, column2 datatype);` | `CREATE GLOBAL TEMPORARY TABLE table_name (column1 datatype, column2 datatype);` |
| **<span style="color: #6F42C1;">Group By</span>** *(Nhóm theo)* | `SELECT column1, COUNT(*) FROM table_name GROUP BY column1;` | `similar` *(tương tự)* |
| **<span style="color: #6F42C1;">Partition By</span>** *(Phân vùng theo)* | `SELECT column1, RANK() OVER (PARTITION BY column2 ORDER BY column3) FROM table_name;` | `similar` *(tương tự)* |
| **<span style="color: #FD7E14;">Run Procedure</span>** *(Chạy thủ tục)* | `EXECUTE procedure_name;` | `CALL procedure_name();` |
| **<span style="color: #FD7E14;">Loop</span>** *(Vòng lặp)* | `FOR row IN (SELECT * FROM table_name) LOOP <statements> END LOOP;` | `FOR row AS cursor_name CURSOR FOR SELECT * FROM table_name DO <statements> END FOR;` |
| **<span style="color: #6C757D;">Parallel</span>** *(Xử lý song song)* | `INSERT /*+APPEND PARALLEL(8)*/ INTO` | `SELECT * FROM table_name PARALLEL 4;` |
|  | `MERGE /*+ parallel(8) */ INTO` |  |
|  | `SELECT /*+ PARALLEL(8) */ * FROM` |  |

### 3. 🛡️ **DCL – Data Control Language**

| **Chức năng** | **<span style="color: #28A745;">PL/SQL (Oracle)</span>** | **<span style="color: #17A2B8;">DB2 (IBM)</span>** |
|---------------|-----------------------------------------------------------|-----------------------------------------------------|
| **<span style="color: #17A2B8;">Select</span>** *(Truy vấn)* | `SELECT column1, column2 FROM table_name;` | `similar` *(tương tự)* |

## 🔧 **Tiện ích hỗ trợ (Utilities)**

| **Chức năng** | **<span style="color: #28A745;">PL/SQL (Oracle)</span>** | **<span style="color: #17A2B8;">DB2 (IBM)</span>** |
|---------------|-----------------------------------------------------------|-----------------------------------------------------|
| **<span style="color: #007ACC;">SYS_INFO</span>** *(Thông tin hệ thống)* | <span style="color: #6C757D;">*Không có*</span> | `SELECT * FROM SYSIBMADM.ENV_SYS_INFO` |
| **<span style="color: #28A745;">NVL</span>** *(Xử lý NULL)* | `NVL(column, 0)` | `COALESCE(column, 0)` |
|  | `COALESCE(column, 0)` | `COALESCE(column, 0)` |
| **<span style="color: #FFC107;">Diff Month</span>** *(Chênh lệch tháng)* | `SELECT (EXTRACT(YEAR FROM end_date) - EXTRACT(YEAR FROM start_date)) * 12 + EXTRACT(MONTH FROM end_date) - EXTRACT(MONTH FROM start_date) AS month_diff FROM your_table;` | `SELECT (YEAR(end_date) - YEAR(start_date)) * 12 + MONTH(end_date) - MONTH(start_date) AS month_diff FROM your_table;` |
| **<span style="color: #DC3545;">Add Months</span>** *(Thêm tháng)* | `SELECT ADD_MONTHS(date1, number_of_months) FROM dual;` | `SELECT ADD_YEARS(current_date, 3), ADD_MONTHS(current_date, 3 ), ADD_DAYS(current_date, 3), ADD_HOURS(current timestamp, 3), ADD_MINUTES(current timestamp, 3), ADD_SECONDS(current timestamp, 3) FROM sysibm.sysdummy1;` |
| **<span style="color: #E83E8C;">Diff Date</span>** *(Chênh lệch ngày)* | `SELECT date2 - date1 FROM dual;` | <span style="color: #6C757D;">*Không có sẵn*</span> |
| **<span style="color: #6F42C1;">Compare 2 Tables</span>** *(So sánh 2 bảng)* | `(SELECT * FROM B_TMP MINUS SELECT * FROM B_TMP1) UNION ALL(SELECT * FROM B_TMP1 MINUS SELECT * FROM B_TMP)` | `SELECT * FROM table1 EXCEPT SELECT * FROM table2;` |

---

## 📖 **Tài liệu tham khảo**

- **[DB2 SQL Cookbook](http://db2-sql-cookbook.org/pdf/Db2_SQL_Cookbook.pdf)** - *Sách hướng dẫn chi tiết về DB2 SQL*
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
  
