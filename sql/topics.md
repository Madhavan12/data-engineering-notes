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
