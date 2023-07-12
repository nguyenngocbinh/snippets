---
title: Synonym
---


### Creating a synonym for a table in another database

1. First, create a new database named test and set the current database to test:

    ```sql
    CREATE DATABASE test;
    GO

    USE test;
    GO
    ```


2. Next, create a new schema named purchasing inside the test database:

    ```sql
    CREATE SCHEMA purchasing;
    GO
    ```


3. Then, create a new table in the purchasing schema of the test database:

    ```sql
    CREATE TABLE test.purchasing.suppliers
    (
        supplier_id   INT
        PRIMARY KEY IDENTITY, 
        supplier_name NVARCHAR(100) NOT NULL
    );
    ```

4. After that, from the BikeStores database, create a synonym for the purchasing.suppliers table in the test database:

    ```sql
    USE BikeStores;
    GO

    CREATE SYNONYM suppliers 
    FOR test.purchasing.suppliers;

    ```

5. Finally, from the BikeStores database, refer to the test.purchasing.suppliers table using the suppliers synonym:

    ```sql
    SELECT * FROM suppliers;
    ```

6. Removing a synonym

    ```sql
    DROP SYNONYM IF EXISTS orders;
    ```

### Reference

- [sqlservertutorial](https://www.sqlservertutorial.net/sql-server-basics/sql-server-synonym/)