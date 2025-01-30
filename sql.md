# SQL Notes (Optimized)

## Basics of SQL

- **SQL operates on CRUD operations**: Create, Read, Update, Delete.
- **SQL**: Structured Query Language for managing relational database data.
- **SQL is supported by RDBMS (Relational Database Management Systems)**, such as:
  1. MySQL
  2. Microsoft SQL Server
  3. Oracle
  4. IBM DB2

### Why Focus on MySQL?

- **Open source** and highly popular.
- Used by major companies like Meta and Adobe.

## Major Difference Between SQL and MySQL

| **SQL**                   | **MySQL**                             |
| ------------------------- | ------------------------------------- |
| Query language            | Relational database management system |
| CRUD operations supported | CRUD operations performed using SQL   |

## Basic Commands

1. **Create a Database**:

```sql
CREATE DATABASE db_name;
```

2. **Select a Database to Work On**:

```sql
USE db_name;
```

3. **Create a Table**:

```sql
CREATE TABLE table_name (
  column_name data_type constraints
);
```

4. **Insert Values into a Table**:

```sql
INSERT INTO table_name VALUES (value1, value2, ...);
```

5. **Retrieve Data from a Table**:

```sql
SELECT * FROM table_name;
```

- `*` selects all columns from the table.

## SQL Data Types

### Character Data Types

- **CHAR(n)**: Fixed-length string (0–255 characters).
- **VARCHAR(n)**: Variable-length string (0–255 characters).
  - **Difference**: CHAR allocates full memory for `n`, VARCHAR uses memory based on actual content.

### Text Data Types

- **TINYTEXT**: Up to 255 characters.
- **TEXT**: Up to 65,535 characters.
- **BLOB**: Binary large object (e.g., audio, video, files).

### Numeric Data Types

- **Signed**: Supports negative and positive values (e.g., -128 to 127 for TINYINT).
- **Unsigned**: Supports only positive values (e.g., 0 to 255 for TINYINT).

```sql
CREATE TABLE example (
  col1 TINYINT,
  col2 TINYINT UNSIGNED
);
```

### Advanced Data Types

- **JSON**: Stores data in JSON format.

```sql
CREATE TABLE example (
  col1 JSON
);
```

## Types of SQL Commands

1. **DDL (Data Definition Language)**:

   - Define schema: `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME`.

2. **DRL/DQL (Data Retrieval/Query Language)**:

   - Retrieve data: `SELECT`.

3. **DML (Data Manipulation Language)**:

   - Modify data: `INSERT`, `UPDATE`, `DELETE`.

4. **DCL (Data Control Language)**:

   - Manage permissions: `GRANT`, `REVOKE`.

5. **TCL (Transaction Control Language)**:
   - Manage transactions: `START TRANSACTION`, `COMMIT`, `ROLLBACK`, `SAVEPOINT`.

## Managing a Database

1. **Create a Database**:

```sql
CREATE DATABASE IF NOT EXISTS db_name;
```

2. **Switch Between Databases**:

```sql
USE db_name;
```

3. **Drop a Database**:

```sql
DROP DATABASE IF EXISTS db_name;
```

4. **List All Databases**:

```sql
SHOW DATABASES;
```

5. **List All Tables in the Current Database**:

```sql
SHOW TABLES;
```

## Relationships in SQL

- **Primary Key**: Uniquely identifies records in a table (Parent Table).
- **Foreign Key**: Connects two tables by referencing the primary key of another table (Child Table).

## Query Execution Flow

1. **SELECT** syntax:

```sql
SELECT <column_names> FROM <table_name>;
```

- Execution starts from the `FROM` clause, then applies `SELECT`.

2. **WHERE Clause**:

   - Filters rows based on conditions:

   ```sql
   SELECT * FROM customer WHERE age > 18;
   ```

3. **BETWEEN**:

   - Specifies a range (inclusive):

   ```sql
   SELECT * FROM customer WHERE age BETWEEN 0 AND 100;
   ```

4. **IN**:

   - Reduces multiple OR conditions:

   ```sql
   SELECT * FROM officers WHERE officer_name IN ('Lakshay', 'Maharana Pratap', 'Deepika');
   ```

5. **IS NULL**:
   - Checks for NULL values:
   ```sql
   SELECT * FROM table_name WHERE column_name IS NULL;
   ```

## Pattern Searching with Wildcards

- `%`: Matches zero or more characters.
- `_`: Matches exactly one character.

```sql
SELECT * FROM table_name WHERE first_name LIKE '%i%';
SELECT * FROM table_name WHERE first_name LIKE '_i%';
```

## Sorting

1. **ORDER BY**:

```sql
SELECT * FROM worker ORDER BY salary;
```

2. **Descending Order**:

```sql
SELECT * FROM worker ORDER BY salary DESC;
```

## DISTINCT Values

- Eliminates duplicates:

```sql
SELECT DISTINCT department FROM worker;
```

## Data Grouping and Aggregation

1. Group by department:

```sql
SELECT department, COUNT(*) FROM worker GROUP BY department;
```

2. Aggregations include `MAX`, `MIN`, `AVG`, `SUM`:

```sql
SELECT department, AVG(salary) FROM worker GROUP BY department;
SELECT department, MAX(salary) FROM worker GROUP BY department;
```

3. Filter grouped data using `HAVING`:

```sql
SELECT department, AVG(salary) FROM worker GROUP BY department HAVING AVG(salary) > 50000;
```

## DDL Constraints

1. **Primary Key**:

   - Enforces `NOT NULL` and `UNIQUE`.

2. **Foreign Key**:

   - References the primary key of another table.

3. **Unique**:

```sql
CREATE TABLE data (
  name VARCHAR(255) UNIQUE
);
```

4. **Check**:

```sql
CREATE TABLE account (
  balance INT CONSTRAINT acc_balance_chk CHECK (balance > 1000)
);
```

5. **Default**:

```sql
CREATE TABLE account (
  balance INT NOT NULL DEFAULT 0
);
```

## ALTER Operations

1. **Add a Column**:

```sql
ALTER TABLE customer ADD age INT;
```

2. **Modify a Column**:

```sql
ALTER TABLE customer MODIFY name CHAR(1024);
```

3. **Change a Column Name**:

```sql
ALTER TABLE customer CHANGE COLUMN name customer_name VARCHAR(1024);
```

4. **Drop a Column**:

```sql
ALTER TABLE customer DROP COLUMN middle_name;
```

5. **Rename a Table**:

```sql
ALTER TABLE customer RENAME TO customer_details;
```

## Data Modification Commands

1. **Insert**:

```sql
INSERT INTO table_name (col1, col2) VALUES ('value1', 'value2');
```

2. **Update**:

```sql
UPDATE customer SET address = 'Mumbai' WHERE id = 121;
```

3. **Replace**:
   - Inserts new or replaces existing data:

```sql
REPLACE INTO customer (col1, col2) VALUES ('value1', 'value2');
```

## Joins

1. **Inner Join**:
   - Matches data between tables:

```sql
SELECT * FROM table1 INNER JOIN table2 ON table1.id = table2.id;
```

2. **Left Join**:
   - Includes all rows from the left table:

```sql
SELECT * FROM table1 LEFT JOIN table2 ON table1.id = table2.id;
```

3. **Right Join**:
   - Includes all rows from the right table:

```sql
SELECT * FROM table1 RIGHT JOIN table2 ON table1.id = table2.id;
```

4. **Full Join**:

   - Includes all rows when there's a match in either table (requires simulation in MySQL).

5. **Self Join**:
   - Joins a table with itself.

## Interview Tip

- **Can SELECT be used without FROM?**
  - Yes, using dual tables in MySQL:

```sql
SELECT 55 + 11;
```
