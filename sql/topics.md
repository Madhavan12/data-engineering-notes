# 📘 SQL Foundations Notes

Mastering the basics of SQL — the foundation for data analysis, engineering, and backend development.

---

## 🟩 Topic 1: SELECT Basics

### SELECT Statement
```sql
SELECT column1, column2
FROM table_name;
```

### DISTINCT (Remove duplicates)
```sql
SELECT DISTINCT column_name
FROM table_name;
```

### AS (Aliases for columns/tables)
```sql
SELECT first_name AS name
FROM employees AS e;
```

---

## 🟨 Topic 2: WHERE Clause – Filtering Data

### Basic WHERE clause
```sql
SELECT * FROM table_name
WHERE column_name = 'value';
```

### Comparison Operators:
- `=` Equal
- `!=` or `<>` Not equal
- `<`, `>`, `<=`, `>=`

### Logical Operators:
- `AND`, `OR`, `NOT`

### IN
```sql
SELECT * FROM users
WHERE country IN ('India', 'USA');
```

### BETWEEN
```sql
SELECT * FROM orders
WHERE price BETWEEN 100 AND 500;
```

### LIKE (Pattern matching)
```sql
SELECT * FROM customers
WHERE name LIKE 'A%'  -- Starts with A
```

### NULL Check
```sql
SELECT * FROM employees
WHERE department IS NULL;
```

---

## 🟦 Topic 3: ORDER BY, LIMIT, OFFSET

### ORDER BY (Sort results)
```sql
SELECT * FROM products
ORDER BY price ASC;
```

### LIMIT (Limit number of results)
```sql
SELECT * FROM products
LIMIT 10;
```

### OFFSET (Skip rows)
```sql
SELECT * FROM products
LIMIT 10 OFFSET 20;
```

---

## 🟫 Topic 4: Aggregations & GROUP BY

### Aggregate Functions:
- `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`

### GROUP BY
```sql
SELECT department, COUNT(*) AS total
FROM employees
GROUP BY department;
```

### HAVING (filter after GROUP BY)
```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

---

## 🟪 Topic 5: JOINs

### INNER JOIN
```sql
SELECT a.name, b.salary
FROM employees a
INNER JOIN payroll b ON a.emp_id = b.emp_id;
```

### LEFT JOIN
```sql
SELECT a.name, b.salary
FROM employees a
LEFT JOIN payroll b ON a.emp_id = b.emp_id;
```

### RIGHT JOIN
```sql
SELECT a.name, b.salary
FROM employees a
RIGHT JOIN payroll b ON a.emp_id = b.emp_id;
```

### FULL OUTER JOIN
```sql
SELECT *
FROM employees
FULL OUTER JOIN payroll ON employees.emp_id = payroll.emp_id;
```

---

## 🟧 Topic 6: Subqueries

### Subquery in SELECT
```sql
SELECT name,
  (SELECT AVG(salary) FROM employees) AS avg_salary
FROM employees;
```

### Subquery in WHERE
```sql
SELECT name FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

---

## 🟫 Topic 7: CASE Statements

### Conditional Logic
```sql
SELECT name,
  CASE
    WHEN salary > 80000 THEN 'High'
    WHEN salary > 50000 THEN 'Medium'
    ELSE 'Low'
  END AS salary_band
FROM employees;
```

---

## 🟨 Topic 8: String & Date Functions

### String Functions
- `UPPER()`, `LOWER()`, `TRIM()`, `SUBSTRING()`, `CONCAT()`, `REPLACE()`

### Date Functions
- `NOW()`, `CURRENT_DATE`, `DATE_ADD()`, `DATEDIFF()`, `EXTRACT(YEAR FROM date_column)`

---


# 🧠 Intermediate to Advanced SQL Topics

---

## 🟦 Topic 9: Window Functions (Analytic Functions)

Window functions let you perform calculations across rows related to the current row, without collapsing the result set like GROUP BY does.

### Syntax:
```sql
function_name(column) OVER (
  PARTITION BY column
  ORDER BY column
)
```

### Common Window Functions:

| Function        | Use Case                                 |
|-----------------|-------------------------------------------|
| `ROW_NUMBER()`  | Assigns a unique row number per partition |
| `RANK()`        | Gives same rank for ties, with gaps       |
| `DENSE_RANK()`  | Like RANK(), but no gaps                  |
| `LAG()`         | Returns previous row's value              |
| `LEAD()`        | Returns next row's value                  |
| `NTILE(n)`      | Divides rows into `n` buckets             |

### Example:
```sql
SELECT name, department, salary,
  RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank_in_dept
FROM employees;
```

---

## 🟩 Topic 10: CTEs (Common Table Expressions)

CTEs help write readable, modular queries — like defining subqueries with names.

### Syntax:
```sql
WITH cte_name AS (
  SELECT ...
)
SELECT * FROM cte_name;
```

### Example:
```sql
WITH high_salary AS (
  SELECT * FROM employees WHERE salary > 80000
)
SELECT name FROM high_salary WHERE department = 'Engineering';
```

### Recursive CTE:
```sql
WITH RECURSIVE count_cte(n) AS (
  SELECT 1
  UNION ALL
  SELECT n + 1 FROM count_cte WHERE n < 5
)
SELECT * FROM count_cte;
```

---

## 🟨 Topic 11: Views

Views are virtual tables based on SQL queries.

### Syntax:
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```

### Use:
- Simplify complex joins
- Abstract logic for reuse
- Can sometimes be updatable

---

## 🟥 Topic 12: Set Operations

Combine results from multiple queries.

| Operation     | Description                         |
|---------------|-------------------------------------|
| `UNION`       | Removes duplicates (default)        |
| `UNION ALL`   | Keeps duplicates                    |
| `INTERSECT`   | Rows common to both queries         |
| `EXCEPT` / `MINUS` | Rows in first query but not in second |

### Example:
```sql
SELECT name FROM table1
UNION
SELECT name FROM table2;
```

---

## 🟧 Topic 13: Transactions & ACID

### SQL Transaction:
```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

### ACID Properties:
- **A**tomicity: All or nothing
- **C**onsistency: Valid state maintained
- **I**solation: Transactions don’t interfere
- **D**urability: Committed changes persist

---

## 🟪 Topic 14: Indexes

Indexes make searches faster.

```sql
CREATE INDEX idx_name ON table(column);
```

- Speed up SELECT
- Slow down INSERT/UPDATE
- Use wisely (on frequently filtered or joined columns)

---

## 🟫 Topic 15: Constraints

| Constraint     | Description                         |
|----------------|-------------------------------------|
| `PRIMARY KEY`  | Unique & not null identifier        |
| `FOREIGN KEY`  | Enforces relationship               |
| `UNIQUE`       | No duplicates                       |
| `NOT NULL`     | Must have a value                   |
| `CHECK`        | Enforces a custom rule              |
| `DEFAULT`      | Sets default value for column       |

---

## 🟨 Topic 16: Stored Procedures & Functions

### Stored Procedure:
```sql
CREATE PROCEDURE GetEmployees()
BEGIN
  SELECT * FROM employees;
END;
```

### Function:
```sql
CREATE FUNCTION GetTotalSalary()
RETURNS INT
BEGIN
  RETURN (SELECT SUM(salary) FROM employees);
END;
```

---

## 🟦 Topic 17: Triggers

Triggers run automatically on certain table events.

```sql
CREATE TRIGGER update_time
BEFORE UPDATE ON employees
FOR EACH ROW
SET NEW.updated_at = CURRENT_TIMESTAMP;
```

# 🧩 Advanced SQL Topics (Final Set)

---

## 🟥 Topic 18: Temporary Tables

Temporary tables exist only during the session and are automatically dropped when the session ends.

### Syntax:
```sql
CREATE TEMPORARY TABLE temp_sales AS
SELECT * FROM sales WHERE year = 2024;
```

### Notes:
- Used for storing intermediate results
- Ideal for complex multi-step analysis
- Not visible to other sessions

---

## 🟫 Topic 19: Materialized Views

Unlike regular views, materialized views store data physically and require manual or scheduled refresh.

### Syntax:
```sql
CREATE MATERIALIZED VIEW mv_monthly_sales AS
SELECT region, SUM(sales)
FROM orders
GROUP BY region;
```

### Notes:
- Faster query performance
- Must be refreshed to update data:
```sql
REFRESH MATERIALIZED VIEW mv_monthly_sales;
```

---

## 🟪 Topic 20: Pivot and Unpivot

Used to rotate rows into columns and vice versa.

### PIVOT (SQL Server Example):
```sql
SELECT *
FROM (
  SELECT year, product, revenue
  FROM sales
) src
PIVOT (
  SUM(revenue) FOR year IN ([2022], [2023])
) AS pvt;
```

### UNPIVOT:
```sql
SELECT product, year, revenue
FROM sales_unpivot
UNPIVOT (
  revenue FOR year IN ([2022], [2023])
) AS unpvt;
```

---

## 🟨 Topic 21: JSON Functions in SQL

Modern SQL engines (PostgreSQL, MySQL 5.7+, BigQuery) support querying JSON.

### Access JSON Fields:
```sql
SELECT info->>'email' AS email
FROM users;
```

### Flatten JSON Arrays (PostgreSQL):
```sql
SELECT *
FROM jsonb_array_elements_text('[1,2,3]'::jsonb);
```

---

## 🟦 Topic 22: Full-Text Search

Used for natural language search in databases.

### MySQL Example:
```sql
SELECT * FROM articles
WHERE MATCH(title, content)
AGAINST ('+marketing +strategy' IN BOOLEAN MODE);
```

### PostgreSQL Example:
```sql
SELECT * FROM posts
WHERE to_tsvector(content) @@ to_tsquery('analytics & AI');
```

---

## 🟩 Topic 23: SQL with Geospatial Data (PostGIS)

For working with location-based data like coordinates and distances.

### Example:
```sql
SELECT name
FROM cities
WHERE ST_DWithin(
  location, ST_MakePoint(144.96, -37.81)::geography, 10000
);
```

---

## 🟧 Topic 24: Security – Users, Roles, and Permissions

### GRANT & REVOKE:
```sql
GRANT SELECT, INSERT ON customers TO analyst_user;
REVOKE DELETE ON customers FROM analyst_user;
```

- Control who can SELECT, INSERT, UPDATE, or DELETE on tables/views.

---

## 🟦 Topic 25: SQL Performance Tuning Basics

### Key Concepts:
- Use EXPLAIN to analyze queries
- Avoid SELECT * in large tables
- Index appropriate columns
- Reduce nested subqueries

### Tools:
- PostgreSQL: EXPLAIN ANALYZE
- MySQL: EXPLAIN
- BigQuery: Execution plan UI

---

## 🧠 BONUS: SQL + Python Integration

Use Python libraries like sqlite3, psycopg2, or SQLAlchemy to connect and run SQL queries.

```python
import sqlite3

conn = sqlite3.connect("data.db")
cursor = conn.cursor()

cursor.execute("SELECT * FROM users WHERE age > 30")
results = cursor.fetchall()

conn.close()
```
