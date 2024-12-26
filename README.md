# Parameters_And_Joins_IN_SQL

# PARAMETER'S

In SQL, parameters are used in various contexts to define, filter, and manipulate data. Below is an explanation of **all key parameters** that you might encounter when working with SQL:

---

### **1. SELECT Parameters**
Used to specify the columns or expressions to retrieve.

- **`*`**: Selects all columns.
  ```sql
  SELECT * FROM employees;
  ```
- **Specific columns**: Select specific columns.
  ```sql
  SELECT name, salary FROM employees;
  ```
- **Alias (`AS`)**: Renames a column or expression in the output.
  ```sql
  SELECT name AS EmployeeName FROM employees;
  ```

---

### **2. WHERE Parameters**
Used to filter records based on specific conditions.

- **Comparison Operators**: `=`, `!=`, `<`, `>`, `<=`, `>=`.
  ```sql
  SELECT * FROM employees WHERE salary > 50000;
  ```
- **Logical Operators**: `AND`, `OR`, `NOT`.
  ```sql
  SELECT * FROM employees WHERE department = 'HR' AND salary > 50000;
  ```
- **Pattern Matching (`LIKE`)**: For partial matches.
  ```sql
  SELECT * FROM employees WHERE name LIKE 'A%'; -- Starts with 'A'
  ```
- **Range (`BETWEEN`)**:
  ```sql
  SELECT * FROM employees WHERE salary BETWEEN 40000 AND 60000;
  ```

---

### **3. JOIN Parameters**
Used to combine rows from two or more tables.

- **`ON`**: Specifies the condition for joining tables.
  ```sql
  SELECT employees.name, departments.department_name
  FROM employees
  INNER JOIN departments
  ON employees.department_id = departments.id;
  ```

---

### **4. GROUP BY Parameters**
Used to group rows sharing a property into summary rows.

- **Column/Expression**:
  ```sql
  SELECT department, COUNT(*) AS EmployeeCount
  FROM employees
  GROUP BY department;
  ```
- **HAVING**: Filters grouped results.
  ```sql
  SELECT department, COUNT(*) AS EmployeeCount
  FROM employees
  GROUP BY department
  HAVING COUNT(*) > 10;
  ```

---

### **5. ORDER BY Parameters**
Used to sort the result set.

- **`ASC`**: Ascending order (default).
  ```sql
  SELECT * FROM employees ORDER BY name ASC;
  ```
- **`DESC`**: Descending order.
  ```sql
  SELECT * FROM employees ORDER BY salary DESC;
  ```

---

### **6. INSERT Parameters**
Used to add new rows to a table.

- **Columns and Values**:
  ```sql
  INSERT INTO employees (name, department, salary)
  VALUES ('John Doe', 'HR', 60000);
  ```
- **Multiple Rows**:
  ```sql
  INSERT INTO employees (name, department, salary)
  VALUES 
    ('Alice', 'Finance', 70000),
    ('Bob', 'IT', 80000);
  ```

---

### **7. UPDATE Parameters**
Used to modify existing rows in a table.

- **SET**: Specifies the column(s) to update.
  ```sql
  UPDATE employees
  SET salary = 70000
  WHERE id = 1;
  ```

---

### **8. DELETE Parameters**
Used to delete rows from a table.

- **Condition**:
  ```sql
  DELETE FROM employees WHERE id = 1;
  ```
- **Delete All Rows**:
  ```sql
  DELETE FROM employees;
  ```

---

### **9. CREATE TABLE Parameters**
Used to create a new table.

- **Column Definitions**:
  ```sql
  CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL(10, 2)
  );
  ```
- **Constraints**: Defines rules for the data.
  - `PRIMARY KEY`, `NOT NULL`, `UNIQUE`, `FOREIGN KEY`, `CHECK`, `DEFAULT`.

---

### **10. FUNCTIONS and AGGREGATES**
Used to perform calculations on data.

- **Aggregate Functions**:
  - `COUNT()`: Counts rows.
    ```sql
    SELECT COUNT(*) FROM employees;
    ```
  - `SUM()`: Sums values.
    ```sql
    SELECT SUM(salary) FROM employees;
    ```
  - `AVG()`: Calculates the average.
    ```sql
    SELECT AVG(salary) FROM employees;
    ```
  - `MAX()`, `MIN()`:
    ```sql
    SELECT MAX(salary), MIN(salary) FROM employees;
    ```

---

### **11. SUBQUERIES Parameters**
A query nested within another query.

- **In `WHERE`**:
  ```sql
  SELECT name FROM employees
  WHERE department_id = (SELECT id FROM departments WHERE department_name = 'HR');
  ```

---

### **12. LIMIT and OFFSET**
Used to restrict the number of rows returned.

- **LIMIT**: Limits the number of rows.
  ```sql
  SELECT * FROM employees LIMIT 10;
  ```
- **OFFSET**: Skips rows before starting to return results.
  ```sql
  SELECT * FROM employees LIMIT 10 OFFSET 5;
  ```

---

### **13. Indexing and Optimization Parameters**
- **CREATE INDEX**:
  ```sql
  CREATE INDEX idx_employee_name ON employees(name);
  ```

---

### **14. Transaction Parameters**
Used for ensuring data integrity.

- **START TRANSACTION**, **COMMIT**, **ROLLBACK**:
  ```sql
  START TRANSACTION;
  UPDATE accounts SET balance = balance - 100 WHERE id = 1;
  UPDATE accounts SET balance = balance + 100 WHERE id = 2;
  COMMIT;
  ```


# SQL JOIN'S

SQL joins are used to combine rows from two or more tables based on a related column. Here's an overview of all the SQL JOIN types with examples and explanations:

---

### 1. **INNER JOIN**
Returns records that have matching values in both tables.

**Syntax**:
```sql
SELECT column_names
FROM table1
INNER JOIN table2
ON table1.common_column = table2.common_column;
```

**Example**:
```sql
SELECT employees.name, departments.department_name
FROM employees
INNER JOIN departments
ON employees.department_id = departments.id;
```

---

### 2. **LEFT JOIN** (or LEFT OUTER JOIN)
Returns all records from the left table and the matched records from the right table. If no match is found, NULL is returned for columns of the right table.

**Syntax**:
```sql
SELECT column_names
FROM table1
LEFT JOIN table2
ON table1.common_column = table2.common_column;
```

**Example**:
```sql
SELECT employees.name, departments.department_name
FROM employees
LEFT JOIN departments
ON employees.department_id = departments.id;
```

---

### 3. **RIGHT JOIN** (or RIGHT OUTER JOIN)
Returns all records from the right table and the matched records from the left table. If no match is found, NULL is returned for columns of the left table.

**Syntax**:
```sql
SELECT column_names
FROM table1
RIGHT JOIN table2
ON table1.common_column = table2.common_column;
```

**Example**:
```sql
SELECT employees.name, departments.department_name
FROM employees
RIGHT JOIN departments
ON employees.department_id = departments.id;
```

---

### 4. **FULL JOIN** (or FULL OUTER JOIN)
Returns all records when there is a match in either table. If no match is found, NULL is returned for the non-matching side.

**Syntax**:
```sql
SELECT column_names
FROM table1
FULL JOIN table2
ON table1.common_column = table2.common_column;
```

**Example**:
```sql
SELECT employees.name, departments.department_name
FROM employees
FULL JOIN departments
ON employees.department_id = departments.id;
```

---

### 5. **CROSS JOIN**
Returns the Cartesian product of both tables (i.e., every row of table1 is paired with every row of table2).

**Syntax**:
```sql
SELECT column_names
FROM table1
CROSS JOIN table2;
```

**Example**:
```sql
SELECT employees.name, departments.department_name
FROM employees
CROSS JOIN departments;
```

---

### 6. **SELF JOIN**
A table is joined with itself. It is useful for hierarchical or comparison queries.

**Syntax**:
```sql
SELECT A.column_name, B.column_name
FROM table_name A, table_name B
WHERE condition;
```

**Example**:
```sql
SELECT E1.name AS Employee, E2.name AS Manager
FROM employees E1
INNER JOIN employees E2
ON E1.manager_id = E2.id;
```

---

### 7. **NATURAL JOIN**
Automatically joins tables based on columns with the same name and compatible data types. No `ON` clause is required.

**Syntax**:
```sql
SELECT column_names
FROM table1
NATURAL JOIN table2;
```

**Example**:
```sql
SELECT employees.name, departments.department_name
FROM employees
NATURAL JOIN departments;
```

---

### Comparison of Joins

| **Type**       | **Matched Rows**                   | **Unmatched Rows (Nulls)**              |
|-----------------|------------------------------------|-----------------------------------------|
| **INNER JOIN**  | Rows with matches in both tables  | No                                     |
| **LEFT JOIN**   | All rows from the left table      | Yes (for unmatched rows in right table) |
| **RIGHT JOIN**  | All rows from the right table     | Yes (for unmatched rows in left table)  |
| **FULL JOIN**   | Rows with matches in either table | Yes (both sides if unmatched)           |
| **CROSS JOIN**  | Cartesian product                | N/A                                    |

