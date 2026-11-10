# 🗄️ Oracle SQL Developer — Basics

> [!abstract] 🎯 Goal Connect to Oracle, create users, grant permissions, create tables, define constraints and retrieve data.

---

## 🔌 1. Connect to Oracle

SQL Developer → New Connection.

|Field|Value|
|---|---|
|Connection Name|`MyConnection`|
|Username|`system`|
|Password|Your Oracle password|
|Hostname|`localhost`|
|Port|`1521`|
|Connection Type|`Basic`|
|Role|`Default`|
|Service Name|`XEPDB1`|

Click **Test** → **Connect**.

💡 `XEPDB1` = Oracle XE pluggable database service.

---

## 👤 2. Create a User

Connect as `SYSTEM`:

```sql
CREATE USER student
IDENTIFIED BY student123;
```

### 🔑 Grant Permissions


```sql
-- Connect to database
GRANT CREATE SESSION TO student;

-- Create objects
GRANT CREATE TABLE TO student;
GRANT CREATE VIEW TO student;
GRANT CREATE SEQUENCE TO student;
GRANT CREATE PROCEDURE TO student;
GRANT CREATE TRIGGER TO student;

-- Tablespace quota
ALTER USER student
QUOTA UNLIMITED ON USERS;
```

### 🎭 Other Privileges

```sql
-- Grant a role
GRANT CONNECT TO student;

-- Access any schema (powerful privileges)
GRANT SELECT ANY TABLE TO student;
GRANT INSERT ANY TABLE TO student;
GRANT UPDATE ANY TABLE TO student;
GRANT DELETE ANY TABLE TO student;

-- Remove a privilege
REVOKE CREATE TABLE FROM student;
```

⚠️ Avoid `ANY` privileges unless necessary. Prefer granting access to specific tables.

---

## 🔤 3. Oracle Data Types

|Data Type|Description|Example|
|---|---|---|
|`NUMBER(p,s)`|Numeric values|`NUMBER(10,2)`|
|`INTEGER`|Whole numbers|`INTEGER`|
|`VARCHAR2(n)`|Variable-length text|`VARCHAR2(100)`|
|`CHAR(n)`|Fixed-length text|`CHAR(2)`|
|`DATE`|Date and time|`DATE`|
|`TIMESTAMP`|Date and precise time|`TIMESTAMP`|
|`CLOB`|Large text|`CLOB`|
|`BLOB`|Binary data/files|`BLOB`|
|`RAW(n)`|Binary values|`RAW(16)`|

### Examples


```sql
employee_id NUMBER(8)
salary NUMBER(10,2)
first_name VARCHAR2(50)
country_code CHAR(2)
birth_date DATE
created_at TIMESTAMP
description CLOB
photo BLOB
```

💡 `NUMBER(10,2)` = 10 digits total, 2 after the decimal point.

---

## 🏗️ 4. Constraints & Naming Conventions

A **CONSTRAINT** is a rule that controls the data allowed in a table.

### 📋 Standard Naming Convention

Use lowercase prefixes and descriptive names.

|Constraint|Prefix|Example|
|---|---|---|
|Primary Key|`pk_`|`pk_employees`|
|Foreign Key|`fk_`|`fk_employees_departments`|
|Unique|`uq_`|`uq_employees_email`|
|Check|`ck_`|`ck_employees_salary`|
|Not Null|`nn_`|`nn_employees_name`|

💡 Format: `prefix_table_column` (or a descriptive relationship name).

### 🔑 PRIMARY KEY (PK)

Unique identifier for each row. Cannot be NULL or duplicated.

```sql
CONSTRAINT pk_employees
PRIMARY KEY (employee_id)
```

### 🔗 FOREIGN KEY (FK)

Connects two tables. References a primary key or unique key in another table.

```sql
CONSTRAINT fk_employees_departments
FOREIGN KEY (department_id)
REFERENCES departments(department_id)
```

## 🏛️ 5. Create Tables — Complete Example

### Parent Table

```sql
CREATE TABLE departments (
    department_id NUMBER(5),
    department_name VARCHAR2(50) NOT NULL,

    CONSTRAINT pk_departments
    PRIMARY KEY (department_id),

    CONSTRAINT uq_departments_name
    UNIQUE (department_name)
);
```

### ✏️ Add or Remove Constraints

```sql
-- Add Primary Key
ALTER TABLE employees
ADD CONSTRAINT pk_employees
PRIMARY KEY (employee_id);

-- Add Foreign Key
ALTER TABLE employees
ADD CONSTRAINT fk_employees_departments
FOREIGN KEY (department_id)
REFERENCES departments(department_id);

-- Remove a constraint
ALTER TABLE employees
DROP CONSTRAINT fk_employees_departments;
```

💡 When creating tables, define constraints directly inside `CREATE TABLE` whenever possible.

---

## ✏️ 6. Insert Data

```sql
INSERT INTO departments
VALUES (1, 'IT');

INSERT INTO employees (
    employee_id,
    employee_name,
    email,
    salary,
    department_id
)
VALUES (
    101, 'John',
    'john@email.com',
    2500, 1
);

COMMIT;
```

💡 Insert the parent row before the child row when using a foreign key.

---

## 🔍 7. Select Data


```sql
-- All columns
SELECT * FROM employees;

-- Specific columns
SELECT employee_name, salary
FROM employees;

-- Filter
SELECT *
FROM employees
WHERE department_id = 1;

-- Sort
SELECT *
FROM employees
ORDER BY employee_name ASC;

-- Join tables
SELECT e.employee_name,
       d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;
```

---

## 🧠 8. Quick SQL Reference

|Command|Purpose|
|---|---|
|`CREATE USER`|Create user|
|`GRANT`|Give permissions|
|`REVOKE`|Remove permissions|
|`CREATE TABLE`|Create table|
|`ALTER TABLE`|Modify table|
|`DROP TABLE`|Delete table|
|`INSERT`|Add data|
|`SELECT`|Retrieve data|
|`UPDATE`|Modify data|
|`DELETE`|Delete rows|
|`COMMIT`|Save changes|
|`ROLLBACK`|Undo uncommitted changes|

### ⭐ Remember

- `PK` → uniquely identifies a row.
- `FK` → connects tables.
- `UQ` → prevents duplicate values.
- `CK` → validates a condition.
- `NN` → requires a value.
- `GRANT` → gives permissions.
- `REVOKE` → removes permissions.
- `XEPDB1` → Oracle XE service name.

> [!tip] Naming rule Keep names descriptive, consistent and easy to understand.
> 
> `pk_employees`
> 
> `fk_employees_departments`
> 
> `uq_employees_email`
> 
> `ck_employees_salary`

---
