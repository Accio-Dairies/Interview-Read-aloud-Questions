# SQL & MongoDB Interview Preparation Guide
*Essential Database Queries for Freshers*

DOC to Study SQL and Mongo Compariosn View => https://docs.google.com/document/d/1en3VVoDltHWikun32WlS8SssFMgzvZd_/edit?usp=sharing&ouid=100742433070092573757&rtpof=true&sd=true

**Note for Students:** This guide is written exactly how you should answer in interviews. Practice reading these answers out loud to make them natural when speaking. Focus is on theoretical understanding and practical query writing.

---

## Table of Contents

### SQL Basics
1. [What is SQL?](#q1-what-is-sql)
2. [Database Structure](#q2-database-structure-tables-rows-columns)
3. [Data Types](#q3-sql-data-types)
4. [Primary Key vs Foreign Key](#q4-primary-key-vs-foreign-key)

### SQL CRUD Operations
5. [SELECT - Reading Data](#q5-select---reading-data)
6. [WHERE Clause - Filtering](#q6-where-clause---filtering)
7. [INSERT - Adding Data](#q7-insert---adding-data)
8. [UPDATE - Modifying Data](#q8-update---modifying-data)
9. [DELETE - Removing Data](#q9-delete---removing-data)

### SQL Advanced Queries
10. [ORDER BY - Sorting](#q10-order-by---sorting)
11. [LIMIT and OFFSET](#q11-limit-and-offset)
12. [Aggregate Functions](#q12-aggregate-functions-count-sum-avg-min-max)
13. [GROUP BY and HAVING](#q13-group-by-and-having)
14. [DISTINCT](#q14-distinct)
15. [LIKE and Wildcards](#q15-like-and-wildcards)
16. [IN and BETWEEN](#q16-in-and-between)
17. [NULL Handling](#q17-null-handling)

### SQL Joins
18. [What are Joins?](#q18-what-are-joins)
19. [INNER JOIN](#q19-inner-join)
20. [LEFT JOIN](#q20-left-join-left-outer-join)
21. [RIGHT JOIN](#q21-right-join-right-outer-join)
22. [FULL OUTER JOIN](#q22-full-outer-join)
23. [Self Join](#q23-self-join)

### MongoDB Basics
24. [What is MongoDB?](#q24-what-is-mongodb)
25. [SQL vs MongoDB](#q25-sql-vs-mongodb-terminology)
26. [Document Structure](#q26-document-structure)

### MongoDB CRUD Operations
27. [Find - Reading Data](#q27-find---reading-data)
28. [Filtering in MongoDB](#q28-filtering-in-mongodb)
29. [Insert - Adding Data](#q29-insert---adding-data)
30. [Update - Modifying Data](#q30-update---modifying-data)
31. [Delete - Removing Data](#q31-delete---removing-data)

### MongoDB Advanced Queries
32. [Sort and Limit](#q32-sort-and-limit)
33. [Projection](#q33-projection)
34. [Operators](#q34-operators-comparison-and-logical)
35. [Array Queries](#q35-array-queries)
36. [Aggregation Pipeline](#q36-aggregation-pipeline)
37. [Lookup (Joins)](#q37-lookup---joins-in-mongodb)

### Comparison & Tips
38. [SQL vs MongoDB - Side by Side](#q38-sql-vs-mongodb---side-by-side-comparison)
39. [When to Use Which](#q39-when-to-use-sql-vs-mongodb)
40. [Common Interview Questions](#q40-common-interview-questions)

---

## SQL Basics

### Q1: What is SQL?

**How to Answer:**

"SQL stands for Structured Query Language. It's a standard language for managing and manipulating relational databases.

**Key points:**

**What SQL does:**
- Create, read, update, delete data (CRUD)
- Create and modify database structure (tables, indexes)
- Control access and permissions
- Query and analyze data

**SQL is declarative:**
You tell SQL *what* you want, not *how* to get it.

```sql
-- You say "give me all users"
SELECT * FROM users;

-- SQL figures out how to retrieve it efficiently
```

**Different SQL databases:**
- MySQL
- PostgreSQL
- SQLite
- Microsoft SQL Server
- Oracle

They all use SQL but have slight variations.

**SQL commands categories:**

1. **DDL (Data Definition Language)** - Structure
   - CREATE, ALTER, DROP

2. **DML (Data Manipulation Language)** - Data
   - SELECT, INSERT, UPDATE, DELETE

3. **DCL (Data Control Language)** - Permissions
   - GRANT, REVOKE

4. **TCL (Transaction Control Language)** - Transactions
   - COMMIT, ROLLBACK

**Why SQL is important:**
- Industry standard for 40+ years
- Used by most companies
- Works with structured data
- Powerful for complex queries
- ACID compliant (reliable)

**Interview tip:** SQL is a language for managing relational databases. It's declarative (you say what you want, not how), standardized, and used across many database systems."

---

### Q2: What is database structure - Tables, Rows, Columns?

**How to Answer:**

"A relational database organizes data into tables, which are made up of rows and columns. Think of it like a spreadsheet.

**Table (Relation):**
A collection of related data. Each table stores information about a specific entity.

```
Table: users
+----+----------+-------+------------------+
| id | name     | age   | email            |
+----+----------+-------+------------------+
| 1  | John     | 25    | john@email.com   |
| 2  | Jane     | 30    | jane@email.com   |
| 3  | Bob      | 28    | bob@email.com    |
+----+----------+-------+------------------+
```

**Column (Attribute/Field):**
Represents a specific property or characteristic. Each column has:
- Name (e.g., 'age')
- Data type (e.g., INTEGER, VARCHAR)
- Constraints (e.g., NOT NULL, UNIQUE)

In the users table:
- id (INTEGER)
- name (VARCHAR)
- age (INTEGER)
- email (VARCHAR)

**Row (Record/Tuple):**
A single entry in the table. Each row represents one instance of the entity.

One row from users:
```
id: 1
name: John
age: 25
email: john@email.com
```

**Schema:**
The structure/blueprint of the database - defines all tables, columns, types, and relationships.

**Database hierarchy:**

```
Database
  └── Tables
       └── Rows
            └── Columns (values)
```

**Example with multiple tables:**

```
Database: company

Table: employees
+----+----------+-------------+
| id | name     | dept_id     |
+----+----------+-------------+
| 1  | John     | 101         |
| 2  | Jane     | 102         |
+----+----------+-------------+

Table: departments
+--------+--------------+
| dept_id| dept_name    |
+--------+--------------+
| 101    | Engineering  |
| 102    | Marketing    |
+--------+--------------+
```

**Interview tip:** Explain that tables store data in rows and columns - like Excel spreadsheets. Rows are individual records, columns are properties. Each column has a specific data type."

---

### Q3: What are SQL data types?

**How to Answer:**

"SQL data types specify what kind of data a column can hold. Different databases have slight variations, but these are the common ones.

**Numeric Types:**

**Integer types:**
```sql
-- Whole numbers
INT or INTEGER        -- -2,147,483,648 to 2,147,483,647
SMALLINT             -- -32,768 to 32,767
BIGINT               -- Very large integers
TINYINT              -- 0 to 255

-- Example
CREATE TABLE products (
    id INT,
    stock_count SMALLINT,
    views BIGINT
);
```

**Decimal types:**
```sql
-- Numbers with decimals
DECIMAL(p, s)        -- p=precision, s=scale
NUMERIC(p, s)        -- Same as DECIMAL
FLOAT                -- Approximate decimal
DOUBLE               -- Larger floating point

-- Example
CREATE TABLE products (
    price DECIMAL(10, 2),  -- Max 10 digits, 2 after decimal: 12345678.90
    weight FLOAT
);
```

**String/Text Types:**

```sql
CHAR(n)              -- Fixed length, padded with spaces
VARCHAR(n)           -- Variable length, up to n characters
TEXT                 -- Large text, no max length

-- Example
CREATE TABLE users (
    code CHAR(5),           -- Always 5 characters: 'AB123'
    name VARCHAR(100),      -- Up to 100 characters
    bio TEXT               -- Long text
);
```

**CHAR vs VARCHAR:**
```sql
-- CHAR(5) - Always uses 5 bytes
'AB'    → stored as 'AB   ' (padded)

-- VARCHAR(5) - Uses only needed bytes + 1 or 2 for length
'AB'    → stored as 'AB' (2 bytes + length info)
```

**Date and Time Types:**

```sql
DATE                 -- Date only: '2024-01-15'
TIME                 -- Time only: '14:30:00'
DATETIME            -- Date and time: '2024-01-15 14:30:00'
TIMESTAMP           -- Date, time, timezone
YEAR                -- Year only: 2024

-- Example
CREATE TABLE events (
    event_date DATE,
    event_time TIME,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**Boolean:**

```sql
BOOLEAN or BOOL      -- TRUE/FALSE (or 1/0)

-- Example
CREATE TABLE users (
    is_active BOOLEAN DEFAULT TRUE,
    is_verified BOOLEAN DEFAULT FALSE
);
```

**Binary Types:**

```sql
BLOB                 -- Binary Large Object (images, files)
BINARY(n)            -- Fixed-length binary
VARBINARY(n)         -- Variable-length binary

-- Example
CREATE TABLE files (
    file_data BLOB,
    thumbnail VARBINARY(1000)
);
```

**JSON Type (Modern SQL):**

```sql
JSON                 -- Stores JSON data

-- Example
CREATE TABLE settings (
    user_id INT,
    preferences JSON
);
```

**Choosing data types:**

**For IDs:**
```sql
-- Small table (< 32k records)
id SMALLINT

-- Normal table
id INT

-- Very large table
id BIGINT
```

**For money:**
```sql
-- Use DECIMAL, not FLOAT (precision matters!)
price DECIMAL(10, 2)  -- Good
-- price FLOAT        -- Bad (rounding errors)
```

**For text:**
```sql
-- Known max length
name VARCHAR(100)

-- Unknown/very long
description TEXT
```

**For dates:**
```sql
-- Date only
birth_date DATE

-- With time
created_at DATETIME

-- With timezone
updated_at TIMESTAMP
```

**Common interview question:**

**"Why use VARCHAR instead of TEXT?"**
- VARCHAR is faster for small to medium text
- VARCHAR can be indexed fully
- TEXT is for very long content
- VARCHAR has max length constraint (validation)

**"Why DECIMAL for money, not FLOAT?"**
- DECIMAL is exact (no rounding errors)
- FLOAT is approximate
- Money calculations need precision

**Interview tip:** Know the main types: INT for whole numbers, DECIMAL for money/precise decimals, VARCHAR for text, DATE/TIMESTAMP for dates, BOOLEAN for true/false. Mention that CHAR is fixed-length, VARCHAR is variable-length."

---

### Q4: What is Primary Key vs Foreign Key?

**How to Answer:**

"Primary Key and Foreign Key are constraints that define relationships between tables in a database.

**Primary Key (PK):**

A column (or set of columns) that uniquely identifies each row in a table.

**Rules for Primary Key:**
- Must be unique for each row
- Cannot be NULL
- Only one primary key per table
- Usually an ID column

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,          -- Primary Key
    name VARCHAR(100),
    email VARCHAR(100)
);

-- Or after column definition
CREATE TABLE users (
    id INT,
    name VARCHAR(100),
    email VARCHAR(100),
    PRIMARY KEY (id)
);
```

**Example data:**

```
users table:
+----+----------+------------------+
| id | name     | email            |  ← id is PRIMARY KEY
+----+----------+------------------+
| 1  | John     | john@email.com   |
| 2  | Jane     | jane@email.com   |
| 3  | Bob      | bob@email.com    |
+----+----------+------------------+
Each id is unique and NOT NULL
```

**Why Primary Key?**
- Uniquely identifies each record
- Creates automatic index (fast lookups)
- Prevents duplicate rows
- Used as reference by other tables

**Foreign Key (FK):**

A column that creates a link between two tables. It references the primary key in another table.

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    user_id INT,                      -- Foreign Key
    product_name VARCHAR(100),
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

**Visual relationship:**

```
users table (Parent):
+----+----------+
| id | name     |  ← PRIMARY KEY
+----+----------+
| 1  | John     |
| 2  | Jane     |
+----+----------+
       ↑
       | references
       |
orders table (Child):
+----------+---------+---------------+
| order_id | user_id | product_name  |  ← user_id is FOREIGN KEY
+----------+---------+---------------+
| 101      | 1       | Laptop        |  (references users.id = 1)
| 102      | 1       | Mouse         |  (references users.id = 1)
| 103      | 2       | Keyboard      |  (references users.id = 2)
+----------+---------+---------------+
```

**Foreign Key Rules:**
- Must reference a primary key in another table
- Can be NULL (optional relationship)
- Can have duplicates (many orders per user)
- Enforces referential integrity

**Referential Integrity:**

Foreign keys maintain data consistency:

```sql
-- This will FAIL if user_id 999 doesn't exist in users table
INSERT INTO orders (order_id, user_id, product_name)
VALUES (104, 999, 'Monitor');
-- Error: Foreign key constraint fails

-- This will also FAIL - can't delete user with orders
DELETE FROM users WHERE id = 1;
-- Error: Cannot delete because orders reference this user
```

**Cascade options:**

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
        ON DELETE CASCADE      -- Delete orders if user is deleted
        ON UPDATE CASCADE      -- Update orders if user id changes
);

-- Or SET NULL
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
        ON DELETE SET NULL     -- Set user_id to NULL if user deleted
);
```

**Composite Primary Key:**

Multiple columns together form the primary key:

```sql
CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    enrollment_date DATE,
    PRIMARY KEY (student_id, course_id)  -- Combination must be unique
);
```

**Comparison:**

| Feature | Primary Key | Foreign Key |
|---------|------------|-------------|
| Purpose | Identify row uniquely | Link to another table |
| Uniqueness | Must be unique | Can have duplicates |
| NULL allowed | No | Yes |
| Count per table | One | Many |
| References | - | Another table's PK |

**Real-world example:**

```sql
-- Students table
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);

-- Courses table
CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(100),
    credits INT
);

-- Enrollments table (junction table)
CREATE TABLE enrollments (
    enrollment_id INT PRIMARY KEY,
    student_id INT,
    course_id INT,
    grade VARCHAR(2),
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);
```

This creates relationships:
- One student can enroll in many courses
- One course can have many students
- Enrollments links them together

**Interview tip:** Primary Key uniquely identifies each row (like a unique ID), must be unique and not NULL. Foreign Key creates a relationship between tables by referencing a Primary Key in another table. This maintains referential integrity - you can't have an order for a non-existent user."

---

## SQL CRUD Operations

### Q5: SELECT - Reading Data

**How to Answer:**

"SELECT is the most common SQL command - it retrieves data from tables.

**Basic syntax:**

```sql
SELECT column1, column2, ...
FROM table_name;
```

**Select all columns:**

```sql
-- * means all columns
SELECT * FROM users;
```

Result:
```
+----+----------+-----+------------------+
| id | name     | age | email            |
+----+----------+-----+------------------+
| 1  | John     | 25  | john@email.com   |
| 2  | Jane     | 30  | jane@email.com   |
| 3  | Bob      | 28  | bob@email.com    |
+----+----------+-----+------------------+
```

**Select specific columns:**

```sql
SELECT name, email FROM users;
```

Result:
```
+----------+------------------+
| name     | email            |
+----------+------------------+
| John     | john@email.com   |
| Jane     | jane@email.com   |
| Bob      | bob@email.com    |
+----------+------------------+
```

**Column aliases:**

```sql
SELECT 
    name AS full_name,
    age AS years_old,
    email AS email_address
FROM users;
```

Result:
```
+-----------+-----------+------------------+
| full_name | years_old | email_address    |
+-----------+-----------+------------------+
| John      | 25        | john@email.com   |
+-----------+-----------+------------------+
```

**Expressions in SELECT:**

```sql
-- Calculations
SELECT 
    name,
    age,
    age + 5 AS age_in_5_years,
    age * 12 AS age_in_months
FROM users;

-- String concatenation
SELECT 
    CONCAT(name, ' (', age, ')') AS name_with_age
FROM users;
-- Result: 'John (25)'
```

**Select from multiple tables (simple):**

```sql
SELECT users.name, orders.product_name
FROM users, orders
WHERE users.id = orders.user_id;
```

**Best practices:**

```sql
-- Bad - SELECT * in production
SELECT * FROM users;  -- Returns all columns, slow if many

-- Good - Select only needed columns
SELECT id, name, email FROM users;

-- Bad - No alias for complex queries
SELECT u.name, o.product_name FROM users u, orders o;

-- Good - Clear aliases
SELECT 
    u.name AS customer_name,
    o.product_name AS product
FROM users u
JOIN orders o ON u.id = o.user_id;
```

**Interview tip:** SELECT retrieves data from tables. You can select all columns with *, specific columns, or use expressions and aliases. Always select only the columns you need for better performance."

---

### Q6: WHERE Clause - Filtering

**How to Answer:**

"The WHERE clause filters rows based on conditions. It comes after FROM and before ORDER BY.

**Basic syntax:**

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

**Comparison operators:**

```sql
-- Equal to
SELECT * FROM users WHERE age = 25;

-- Not equal to
SELECT * FROM users WHERE age != 25;
-- Or: age <> 25

-- Greater than
SELECT * FROM users WHERE age > 25;

-- Greater than or equal
SELECT * FROM users WHERE age >= 25;

-- Less than
SELECT * FROM users WHERE age < 30;

-- Less than or equal
SELECT * FROM users WHERE age <= 30;
```

**Logical operators:**

**AND - Both conditions must be true:**

```sql
SELECT * FROM users
WHERE age > 25 AND age < 40;
```

**OR - At least one condition must be true:**

```sql
SELECT * FROM users
WHERE age < 20 OR age > 60;
```

**NOT - Negates a condition:**

```sql
SELECT * FROM users
WHERE NOT age = 25;
```

**Combining operators:**

```sql
SELECT * FROM users
WHERE (age > 25 AND age < 40)
   OR (age > 60 AND city = 'NYC');
```

**String comparisons:**

```sql
-- Exact match (case-sensitive in some DBs)
SELECT * FROM users WHERE name = 'John';

-- Case-insensitive (in some DBs)
SELECT * FROM users WHERE LOWER(name) = 'john';
```

**Practical examples:**

**Find users by age range:**

```sql
SELECT name, age
FROM users
WHERE age BETWEEN 25 AND 35;
-- Same as: age >= 25 AND age <= 35
```

**Find users in specific cities:**

```sql
SELECT name, city
FROM users
WHERE city IN ('NYC', 'LA', 'Chicago');
-- Same as: city = 'NYC' OR city = 'LA' OR city = 'Chicago'
```

**Find users with NULL email:**

```sql
SELECT name FROM users
WHERE email IS NULL;

-- Not null
SELECT name FROM users
WHERE email IS NOT NULL;
```

**Pattern matching:**

```sql
-- Names starting with 'J'
SELECT name FROM users
WHERE name LIKE 'J%';

-- Names ending with 'son'
SELECT name FROM users
WHERE name LIKE '%son';

-- Names containing 'oh'
SELECT name FROM users
WHERE name LIKE '%oh%';
```

**Complex example:**

```sql
SELECT 
    name,
    age,
    city,
    salary
FROM employees
WHERE 
    (age BETWEEN 25 AND 35)
    AND (city IN ('NYC', 'LA'))
    AND (salary > 50000)
    AND (department = 'Engineering'
         OR department = 'Product');
```

**Order of evaluation:**

```sql
-- Without parentheses - confusing!
SELECT * FROM users
WHERE age > 25 OR city = 'NYC' AND active = true;

-- With parentheses - clear!
SELECT * FROM users
WHERE age > 25 OR (city = 'NYC' AND active = true);
```

**Performance tip:**

```sql
-- Bad - function on column prevents index use
SELECT * FROM users
WHERE YEAR(created_at) = 2024;

-- Good - allows index use
SELECT * FROM users
WHERE created_at >= '2024-01-01'
  AND created_at < '2025-01-01';
```

**Interview tip:** WHERE filters rows based on conditions. Use comparison operators (=, <, >) and logical operators (AND, OR, NOT). Use BETWEEN for ranges, IN for multiple values, IS NULL for nulls, and LIKE for patterns."

---

### Q7: INSERT - Adding Data

**How to Answer:**

"INSERT adds new rows to a table.

**Basic syntax:**

```sql
INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3);
```

**Insert single row:**

```sql
INSERT INTO users (id, name, age, email)
VALUES (1, 'John', 25, 'john@email.com');
```

**Insert without specifying columns (must match order):**

```sql
-- Provide values for ALL columns in order
INSERT INTO users
VALUES (2, 'Jane', 30, 'jane@email.com');
```

**Insert multiple rows:**

```sql
INSERT INTO users (id, name, age, email)
VALUES 
    (3, 'Bob', 28, 'bob@email.com'),
    (4, 'Alice', 32, 'alice@email.com'),
    (5, 'Charlie', 27, 'charlie@email.com');
```

**Insert with specific columns (others get defaults/NULL):**

```sql
INSERT INTO users (name, email)
VALUES ('David', 'david@email.com');
-- id will be auto-generated, age will be NULL or default
```

**Insert from another table:**

```sql
INSERT INTO users_archive (id, name, email)
SELECT id, name, email
FROM users
WHERE age > 60;
```

**Auto-increment ID:**

```sql
-- Table with auto-increment
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);

-- Insert without ID
INSERT INTO users (name, email)
VALUES ('John', 'john@email.com');
-- id automatically becomes 1

INSERT INTO users (name, email)
VALUES ('Jane', 'jane@email.com');
-- id automatically becomes 2
```

**Insert with DEFAULT values:**

```sql
CREATE TABLE posts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(200),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(20) DEFAULT 'draft'
);

-- Use default values
INSERT INTO posts (title)
VALUES ('My First Post');
-- created_at gets current timestamp
-- status gets 'draft'

-- Or explicitly use DEFAULT keyword
INSERT INTO posts (title, status)
VALUES ('Second Post', DEFAULT);
```

**Handle duplicates:**

```sql
-- Ignore if duplicate key exists (MySQL)
INSERT IGNORE INTO users (id, name, email)
VALUES (1, 'John', 'john@email.com');

-- Update if duplicate exists (upsert)
INSERT INTO users (id, name, email)
VALUES (1, 'John Updated', 'john@email.com')
ON DUPLICATE KEY UPDATE
    name = 'John Updated',
    email = 'john@email.com';
```

**Common errors:**

```sql
-- Error: Missing required column
INSERT INTO users (name)
VALUES ('John');
-- Error if email is required (NOT NULL)

-- Error: Wrong number of values
INSERT INTO users (name, email)
VALUES ('John');
-- Error: 2 columns but 1 value

-- Error: Data type mismatch
INSERT INTO users (id, name, age)
VALUES (1, 'John', 'twenty-five');
-- Error: 'twenty-five' is not an INT

-- Error: Duplicate primary key
INSERT INTO users (id, name)
VALUES (1, 'John');  -- Works

INSERT INTO users (id, name)
VALUES (1, 'Jane');  -- Error: Duplicate key
```

**Best practices:**

```sql
-- Good - Explicit columns
INSERT INTO users (name, email, age)
VALUES ('John', 'john@email.com', 25);

-- Bad - No column names
INSERT INTO users
VALUES ('John', 'john@email.com', 25);
-- Breaks if table structure changes

-- Good - Multiple inserts in one statement
INSERT INTO users (name, email) VALUES
    ('John', 'john@email.com'),
    ('Jane', 'jane@email.com'),
    ('Bob', 'bob@email.com');

-- Bad - Multiple statements (slower)
INSERT INTO users (name, email) VALUES ('John', 'john@email.com');
INSERT INTO users (name, email) VALUES ('Jane', 'jane@email.com');
INSERT INTO users (name, email) VALUES ('Bob', 'bob@email.com');
```

**Interview tip:** INSERT adds new rows. Specify columns and values. You can insert one or multiple rows at once. Auto-increment handles IDs automatically. Always explicitly list columns for clarity and maintainability."

---

### Q8: UPDATE - Modifying Data

**How to Answer:**

"UPDATE modifies existing rows in a table.

**Basic syntax:**

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

**⚠️ CRITICAL:** Always use WHERE clause unless you want to update ALL rows!

**Update single column:**

```sql
UPDATE users
SET age = 26
WHERE id = 1;
```

Before:
```
+----+------+-----+
| id | name | age |
+----+------+-----+
| 1  | John | 25  |
+----+------+-----+
```

After:
```
+----+------+-----+
| id | name | age |
+----+------+-----+
| 1  | John | 26  |
+----+------+-----+
```

**Update multiple columns:**

```sql
UPDATE users
SET 
    name = 'John Doe',
    age = 26,
    city = 'NYC'
WHERE id = 1;
```

**Update with calculations:**

```sql
-- Increase all salaries by 10%
UPDATE employees
SET salary = salary * 1.10
WHERE department = 'Engineering';

-- Increment a counter
UPDATE posts
SET views = views + 1
WHERE id = 5;
```

**Update with expressions:**

```sql
-- Set full name from first and last
UPDATE users
SET full_name = CONCAT(first_name, ' ', last_name);

-- Update based on another column
UPDATE products
SET status = 'Low Stock'
WHERE quantity < 10;
```

**Update multiple rows:**

```sql
-- Updates all users in NYC
UPDATE users
SET status = 'Active'
WHERE city = 'NYC';
```

**Update with multiple conditions:**

```sql
UPDATE employees
SET bonus = 5000
WHERE 
    years_of_service > 5
    AND department = 'Sales'
    AND performance_rating >= 4;
```

**Update using another table (JOIN):**

```sql
-- Update users based on orders table
UPDATE users u
JOIN orders o ON u.id = o.user_id
SET u.total_spent = (
    SELECT SUM(amount)
    FROM orders
    WHERE user_id = u.id
);
```

**Update with subquery:**

```sql
-- Set user's total orders
UPDATE users
SET order_count = (
    SELECT COUNT(*)
    FROM orders
    WHERE orders.user_id = users.id
)
WHERE id = 1;
```

**Conditional UPDATE:**

```sql
-- Update based on condition
UPDATE products
SET 
    price = CASE
        WHEN category = 'Electronics' THEN price * 1.10
        WHEN category = 'Clothing' THEN price * 1.05
        ELSE price
    END;
```

**Common mistakes:**

**Forgetting WHERE (DANGEROUS!):**

```sql
-- WRONG - Updates ALL rows!
UPDATE users
SET age = 30;
-- Now EVERYONE is 30 years old!

-- RIGHT - Update specific row
UPDATE users
SET age = 30
WHERE id = 1;
```

**Wrong condition:**

```sql
-- Accidentally updates wrong rows
UPDATE users
SET deleted = true
WHERE name = 'John';  -- Deletes ALL Johns, not just one!

-- Better - use unique identifier
UPDATE users
SET deleted = true
WHERE id = 5;
```

**Safe practices:**

**1. Always test with SELECT first:**

```sql
-- First, check what will be updated
SELECT * FROM users WHERE id = 1;

-- Then update
UPDATE users SET age = 30 WHERE id = 1;

-- Verify
SELECT * FROM users WHERE id = 1;
```

**2. Use transactions:**

```sql
START TRANSACTION;

UPDATE users SET age = 30 WHERE id = 1;

-- Check if correct
SELECT * FROM users WHERE id = 1;

-- If correct
COMMIT;

-- If wrong
ROLLBACK;
```

**3. Limit updates (MySQL):**

```sql
-- Update only first 10 rows
UPDATE users
SET status = 'Inactive'
WHERE last_login < '2023-01-01'
LIMIT 10;
```

**Return updated rows (PostgreSQL):**

```sql
UPDATE users
SET age = 30
WHERE id = 1
RETURNING *;
-- Returns the updated row
```

**Interview tip:** UPDATE modifies existing rows. ALWAYS use WHERE clause unless you intentionally want to update all rows. Common practice is to test with SELECT first. Use transactions for safety in production."

---

### Q9: DELETE - Removing Data

**How to Answer:**

"DELETE removes rows from a table.

**Basic syntax:**

```sql
DELETE FROM table_name
WHERE condition;
```

**⚠️ CRITICAL:** Always use WHERE clause unless you want to delete ALL rows!

**Delete specific row:**

```sql
DELETE FROM users
WHERE id = 5;
```

**Delete multiple rows:**

```sql
-- Delete all inactive users
DELETE FROM users
WHERE status = 'Inactive';

-- Delete users older than 60
DELETE FROM users
WHERE age > 60;
```

**Delete with multiple conditions:**

```sql
DELETE FROM orders
WHERE 
    status = 'Cancelled'
    AND created_at < '2023-01-01';
```

**Delete with subquery:**

```sql
-- Delete users who have no orders
DELETE FROM users
WHERE id NOT IN (
    SELECT DISTINCT user_id
    FROM orders
);
```

**Delete using JOIN:**

```sql
-- Delete orders for inactive users
DELETE orders
FROM orders
JOIN users ON orders.user_id = users.id
WHERE users.status = 'Inactive';
```

**Delete all rows (DANGEROUS!):**

```sql
-- Deletes ALL rows!
DELETE FROM users;

-- Faster way to delete all (TRUNCATE)
TRUNCATE TABLE users;
-- Resets auto-increment, faster, but can't rollback
```

**TRUNCATE vs DELETE:**

```sql
-- DELETE - Slower, can be rolled back, keeps structure
DELETE FROM users;

-- TRUNCATE - Faster, resets auto-increment, can't rollback easily
TRUNCATE TABLE users;
```

| Feature | DELETE | TRUNCATE |
|---------|--------|----------|
| Speed | Slower | Faster |
| WHERE clause | Yes | No |
| Rollback | Yes | Limited |
| Triggers | Fires | Doesn't fire |
| Auto-increment | Keeps | Resets |
| Logging | Row by row | Minimal |

**Limit deletions (MySQL):**

```sql
-- Delete only 100 rows
DELETE FROM logs
WHERE created_at < '2023-01-01'
LIMIT 100;
```

**Return deleted rows (PostgreSQL):**

```sql
DELETE FROM users
WHERE id = 5
RETURNING *;
-- Returns the deleted row
```

**Cascade delete:**

When foreign key has ON DELETE CASCADE:

```sql
-- If orders has FK to users with CASCADE
DELETE FROM users WHERE id = 1;
-- Also deletes all orders for user 1 automatically
```

**Common mistakes:**

**Forgetting WHERE (CATASTROPHIC!):**

```sql
-- WRONG - Deletes EVERYTHING!
DELETE FROM users;
-- All users are gone!

-- RIGHT - Delete specific rows
DELETE FROM users
WHERE id = 5;
```

**Wrong condition:**

```sql
-- Accidentally deletes wrong data
DELETE FROM users
WHERE name = 'John';  -- Deletes ALL Johns!

-- Better - use unique identifier
DELETE FROM users
WHERE id = 5;
```

**Foreign key constraint errors:**

```sql
-- This fails if orders reference user 1
DELETE FROM users WHERE id = 1;
-- Error: Cannot delete - foreign key constraint

-- Solutions:
-- 1. Delete orders first
DELETE FROM orders WHERE user_id = 1;
DELETE FROM users WHERE id = 1;

-- 2. Use CASCADE (if defined in FK)
-- 3. Set orders.user_id to NULL (if allowed)
```

**Safe practices:**

**1. Always SELECT first:**

```sql
-- First, check what will be deleted
SELECT * FROM users WHERE id = 5;

-- Then delete
DELETE FROM users WHERE id = 5;

-- Verify
SELECT * FROM users WHERE id = 5;
-- Should return no rows
```

**2. Use transactions:**

```sql
START TRANSACTION;

DELETE FROM users WHERE id = 5;

-- Check count
SELECT COUNT(*) FROM users;

-- If correct
COMMIT;

-- If wrong
ROLLBACK;
```

**3. Soft delete instead of hard delete:**

```sql
-- Instead of DELETE, use UPDATE
UPDATE users
SET deleted = true, deleted_at = NOW()
WHERE id = 5;

-- Query only non-deleted
SELECT * FROM users WHERE deleted = false;
```

**Soft delete benefits:**
- Can recover data
- Maintains referential integrity
- Audit trail
- No cascade issues

**Interview tip:** DELETE removes rows from table. ALWAYS use WHERE clause unless deleting all rows intentionally. Use SELECT first to verify what will be deleted. Consider soft deletes (marking as deleted) instead of hard deletes in production. TRUNCATE is faster for deleting all rows but can't be rolled back easily."

---

## SQL Advanced Queries

### Q10: ORDER BY - Sorting

**How to Answer:**

"ORDER BY sorts the result set by one or more columns.

**Basic syntax:**

```sql
SELECT column1, column2
FROM table_name
ORDER BY column1 [ASC|DESC];
```

**Ascending order (default):**

```sql
SELECT name, age
FROM users
ORDER BY age;
-- Or explicitly: ORDER BY age ASC

-- Result: youngest to oldest
+----------+-----+
| name     | age |
+----------+-----+
| John     | 25  |
| Bob      | 28  |
| Jane     | 30  |
+----------+-----+
```

**Descending order:**

```sql
SELECT name, age
FROM users
ORDER BY age DESC;

-- Result: oldest to youngest
+----------+-----+
| name     | age |
+----------+-----+
| Jane     | 30  |
| Bob      | 28  |
| John     | 25  |
+----------+-----+
```

**Multiple columns:**

```sql
SELECT name, city, age
FROM users
ORDER BY city ASC, age DESC;

-- First sort by city (A-Z)
-- Then within each city, sort by age (high to low)

+----------+---------+-----+
| name     | city    | age |
+----------+---------+-----+
| Jane     | Chicago | 30  |
| Charlie  | Chicago | 25  |
| Alice    | NYC     | 32  |
| Bob      | NYC     | 28  |
+----------+---------+-----+
```

**Order by column position (not recommended):**

```sql
SELECT name, age, city
FROM users
ORDER BY 2 DESC;  -- Orders by 2nd column (age)
```

**Order by expression:**

```sql
-- Order by calculated value
SELECT name, price, price * quantity AS total
FROM products
ORDER BY price * quantity DESC;

-- Order by string length
SELECT name
FROM users
ORDER BY LENGTH(name);

-- Order by date parts
SELECT name, birth_date
FROM users
ORDER BY YEAR(birth_date) DESC, MONTH(birth_date);
```

**NULL handling:**

```sql
-- By default, NULLs usually come first (depends on DB)
SELECT name, age
FROM users
ORDER BY age;

-- NULLs last (MySQL)
SELECT name, age
FROM users
ORDER BY age IS NULL, age;

-- NULLs first explicitly (PostgreSQL)
SELECT name, age
FROM users
ORDER BY age NULLS FIRST;

-- NULLs last explicitly (PostgreSQL)
SELECT name, age
FROM users
ORDER BY age NULLS LAST;
```

**CASE in ORDER BY:**

```sql
-- Custom sort order
SELECT name, status
FROM users
ORDER BY 
    CASE status
        WHEN 'urgent' THEN 1
        WHEN 'high' THEN 2
        WHEN 'medium' THEN 3
        WHEN 'low' THEN 4
    END;
```

**Practical examples:**

**Top 5 highest salaries:**

```sql
SELECT name, salary
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

**Alphabetical list:**

```sql
SELECT name
FROM users
ORDER BY name ASC;
```

**Latest records first:**

```sql
SELECT title, created_at
FROM posts
ORDER BY created_at DESC;
```

**Complex sorting:**

```sql
SELECT 
    name,
    city,
    age,
    salary
FROM employees
WHERE department = 'Engineering'
ORDER BY 
    city ASC,           -- First by city
    salary DESC,        -- Then by salary (high to low)
    age ASC;            -- Then by age (young to old)
```

**Performance tip:**

```sql
-- Slow - sorts entire table then limits
SELECT name FROM users
ORDER BY created_at DESC
LIMIT 10;

-- Fast - if index on created_at exists
CREATE INDEX idx_created_at ON users(created_at);
```

**Interview tip:** ORDER BY sorts results. Default is ascending (ASC), use DESC for descending. You can sort by multiple columns - it sorts by first column, then breaks ties with second column, etc. For performance, create indexes on frequently sorted columns."

---

### Q11: LIMIT and OFFSET

**How to Answer:**

"LIMIT restricts the number of rows returned. OFFSET skips a specified number of rows. Together they enable pagination.

**LIMIT syntax:**

```sql
SELECT column1, column2
FROM table_name
LIMIT number;
```

**Basic LIMIT:**

```sql
-- Get first 5 users
SELECT name, email
FROM users
LIMIT 5;
```

**LIMIT with ORDER BY:**

```sql
-- Top 10 highest salaries
SELECT name, salary
FROM employees
ORDER BY salary DESC
LIMIT 10;

-- 5 youngest users
SELECT name, age
FROM users
ORDER BY age ASC
LIMIT 5;
```

**OFFSET - Skip rows:**

```sql
-- Skip first 10 rows, get next 5
SELECT name, email
FROM users
LIMIT 5 OFFSET 10;
```

**Pagination pattern:**

```sql
-- Page 1 (rows 1-10)
SELECT * FROM products
ORDER BY id
LIMIT 10 OFFSET 0;

-- Page 2 (rows 11-20)
SELECT * FROM products
ORDER BY id
LIMIT 10 OFFSET 10;

-- Page 3 (rows 21-30)
SELECT * FROM products
ORDER BY id
LIMIT 10 OFFSET 20;

-- Formula: OFFSET = (page_number - 1) * page_size
```

**Alternative syntax (MySQL):**

```sql
-- LIMIT offset, count
SELECT * FROM users
LIMIT 10, 5;  -- Skip 10, get 5

-- Same as:
SELECT * FROM users
LIMIT 5 OFFSET 10;
```

**Practical examples:**

**Top 3 scores:**

```sql
SELECT student_name, score
FROM exam_results
ORDER BY score DESC
LIMIT 3;
```

**Random sample:**

```sql
-- Get 10 random users (MySQL)
SELECT name FROM users
ORDER BY RAND()
LIMIT 10;

-- PostgreSQL
SELECT name FROM users
ORDER BY RANDOM()
LIMIT 10;
```

**Latest 20 posts:**

```sql
SELECT title, created_at
FROM posts
ORDER BY created_at DESC
LIMIT 20;
```

**Pagination with page number:**

```javascript
// JavaScript example
const page = 2;
const pageSize = 10;
const offset = (page - 1) * pageSize;

const query = `
  SELECT * FROM products
  ORDER BY id
  LIMIT ${pageSize} OFFSET ${offset}
`;
```

**Get total count with pagination:**

```sql
-- Get page data
SELECT * FROM products
LIMIT 10 OFFSET 20;

-- Get total count for pagination info
SELECT COUNT(*) as total FROM products;
```

**LIMIT without ORDER BY (unreliable):**

```sql
-- Bad - unpredictable results
SELECT * FROM users LIMIT 10;
-- Might return different rows each time!

-- Good - deterministic
SELECT * FROM users
ORDER BY id
LIMIT 10;
```

**Performance considerations:**

```sql
-- Slow - has to scan (page * size) rows
SELECT * FROM users
LIMIT 10 OFFSET 1000000;  -- Skip 1 million rows!

-- Faster - use WHERE with cursor
SELECT * FROM users
WHERE id > 1000000
ORDER BY id
LIMIT 10;
```

**Different databases:**

```sql
-- MySQL, PostgreSQL, SQLite
SELECT * FROM users LIMIT 10 OFFSET 5;

-- SQL Server
SELECT TOP 10 * FROM users;

-- Oracle
SELECT * FROM users WHERE ROWNUM <= 10;

-- Standard SQL (newer versions)
SELECT * FROM users
FETCH FIRST 10 ROWS ONLY;
```

**Complete pagination example:**

```sql
-- Input: page = 3, pageSize = 10

-- Calculate offset
-- offset = (3 - 1) * 10 = 20

-- Query
SELECT 
    id,
    name,
    email,
    created_at
FROM users
WHERE status = 'active'
ORDER BY created_at DESC
LIMIT 10 OFFSET 20;

-- Returns rows 21-30
```

**Interview tip:** LIMIT restricts number of rows returned. OFFSET skips rows before starting to return. Together they enable pagination. Formula for pagination: OFFSET = (page_number - 1) * page_size. Always use ORDER BY with LIMIT for predictable results."

---

### Q12: Aggregate Functions - COUNT, SUM, AVG, MIN, MAX

**How to Answer:**

"Aggregate functions perform calculations on multiple rows and return a single value.

**COUNT() - Count rows:**

```sql
-- Count all rows
SELECT COUNT(*) FROM users;
-- Result: 150

-- Count non-NULL values in column
SELECT COUNT(email) FROM users;
-- Only counts rows where email is NOT NULL

-- Count distinct values
SELECT COUNT(DISTINCT city) FROM users;
-- Number of unique cities
```

**SUM() - Add values:**

```sql
-- Total of all salaries
SELECT SUM(salary) FROM employees;
-- Result: 5500000

-- Total sales for specific product
SELECT SUM(quantity * price) AS total_revenue
FROM orders
WHERE product_id = 5;
```

**AVG() - Average value:**

```sql
-- Average age
SELECT AVG(age) FROM users;
-- Result: 28.5

-- Average salary by department
SELECT 
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

**MIN() - Minimum value:**

```sql
-- Youngest user
SELECT MIN(age) FROM users;
-- Result: 18

-- Earliest date
SELECT MIN(created_at) FROM posts;

-- Cheapest product
SELECT MIN(price) FROM products;
```

**MAX() - Maximum value:**

```sql
-- Oldest user
SELECT MAX(age) FROM users;
-- Result: 65

-- Highest salary
SELECT MAX(salary) FROM employees;

-- Most recent order
SELECT MAX(order_date) FROM orders;
```

**Combining aggregates:**

```sql
SELECT 
    COUNT(*) AS total_employees,
    SUM(salary) AS total_payroll,
    AVG(salary) AS avg_salary,
    MIN(salary) AS min_salary,
    MAX(salary) AS max_salary
FROM employees;
```

Result:
```
+-----------------+---------------+-------------+------------+------------+
| total_employees | total_payroll | avg_salary  | min_salary | max_salary |
+-----------------+---------------+-------------+------------+------------+
| 100             | 5500000       | 55000       | 30000      | 120000     |
+-----------------+---------------+-------------+------------+------------+
```

**Aggregates with WHERE:**

```sql
-- Average salary in Engineering
SELECT AVG(salary) AS avg_eng_salary
FROM employees
WHERE department = 'Engineering';

-- Count of active users
SELECT COUNT(*) AS active_users
FROM users
WHERE status = 'active';

-- Total sales in 2024
SELECT SUM(amount) AS total_2024_sales
FROM orders
WHERE YEAR(order_date) = 2024;
```

**Aggregates with expressions:**

```sql
-- Total revenue
SELECT SUM(quantity * price) AS total_revenue
FROM order_items;

-- Average order value
SELECT AVG(quantity * price) AS avg_order_value
FROM order_items;

-- Count of users registered this year
SELECT COUNT(*) AS new_users_2024
FROM users
WHERE created_at >= '2024-01-01';
```

**COUNT(*) vs COUNT(column):**

```sql
-- Table: users
+----+------+-------+
| id | name | email |
+----+------+-------+
| 1  | John | j@... |
| 2  | Jane | NULL  |
| 3  | Bob  | b@... |
+----+------+-------+

SELECT COUNT(*) FROM users;
-- Result: 3 (counts all rows)

SELECT COUNT(email) FROM users;
-- Result: 2 (counts only non-NULL emails)

SELECT COUNT(DISTINCT name) FROM users;
-- Result: 3 (counts unique names)
```

**Aggregates ignore NULL:**

```sql
-- Salaries: 50000, 60000, NULL, 70000

SELECT AVG(salary) FROM employees;
-- Result: 60000 (average of 50000, 60000, 70000)
-- NULL is ignored

SELECT COUNT(salary) FROM employees;
-- Result: 3 (NULL not counted)

SELECT COUNT(*) FROM employees;
-- Result: 4 (all rows counted)
```

**Common patterns:**

**Total and percentage:**

```sql
SELECT 
    COUNT(*) AS total_orders,
    COUNT(CASE WHEN status = 'completed' THEN 1 END) AS completed_orders,
    ROUND(
        COUNT(CASE WHEN status = 'completed' THEN 1 END) * 100.0 / COUNT(*),
        2
    ) AS completion_rate
FROM orders;
```

**Min and max with details:**

```sql
-- Get highest salary WITH the person's name
SELECT name, salary
FROM employees
WHERE salary = (SELECT MAX(salary) FROM employees);

-- Or using ORDER BY + LIMIT
SELECT name, salary
FROM employees
ORDER BY salary DESC
LIMIT 1;
```

**Count by condition:**

```sql
SELECT 
    COUNT(CASE WHEN age < 18 THEN 1 END) AS minors,
    COUNT(CASE WHEN age BETWEEN 18 AND 65 THEN 1 END) AS adults,
    COUNT(CASE WHEN age > 65 THEN 1 END) AS seniors
FROM users;
```

**Interview tip:** Aggregate functions compute values across multiple rows. COUNT counts rows, SUM adds numbers, AVG calculates average, MIN/MAX find smallest/largest. They ignore NULL values (except COUNT(*)). Use them with GROUP BY to calculate per group."

---


### Q13: GROUP BY and HAVING

**How to Answer:**

"GROUP BY groups rows with the same values and allows you to perform aggregate functions on each group. HAVING filters groups (like WHERE filters rows).

**Basic GROUP BY:**

```sql
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1;
```

**Example - Count users by city:**

```sql
SELECT city, COUNT(*) AS user_count
FROM users
GROUP BY city;
```

Result:
```
+----------+------------+
| city     | user_count |
+----------+------------+
| NYC      | 45         |
| LA       | 32         |
| Chicago  | 28         |
+----------+------------+
```

**Multiple aggregates:**

```sql
SELECT 
    department,
    COUNT(*) AS employee_count,
    AVG(salary) AS avg_salary,
    MIN(salary) AS min_salary,
    MAX(salary) AS max_salary
FROM employees
GROUP BY department;
```

Result:
```
+--------------+----------------+------------+------------+------------+
| department   | employee_count | avg_salary | min_salary | max_salary |
+--------------+----------------+------------+------------+------------+
| Engineering  | 50             | 75000      | 50000      | 120000     |
| Marketing    | 20             | 55000      | 40000      | 80000      |
| Sales        | 30             | 60000      | 35000      | 95000      |
+--------------+----------------+------------+------------+------------+
```

**GROUP BY multiple columns:**

```sql
SELECT 
    department,
    city,
    COUNT(*) AS employee_count,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department, city
ORDER BY department, city;
```

**HAVING - Filter groups:**

HAVING is like WHERE, but for groups (after GROUP BY).

```sql
-- Departments with more than 10 employees
SELECT 
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 10;
```

**WHERE vs HAVING:**

```sql
SELECT 
    department,
    COUNT(*) AS employee_count
FROM employees
WHERE salary > 50000           -- Filter ROWS first
GROUP BY department
HAVING COUNT(*) > 5;           -- Then filter GROUPS
```

**Execution order:**
1. WHERE filters rows
2. GROUP BY groups remaining rows
3. Aggregate functions calculate
4. HAVING filters groups
5. ORDER BY sorts results

**Example - Find high-revenue products:**

```sql
SELECT 
    product_id,
    product_name,
    SUM(quantity * price) AS total_revenue
FROM order_items
GROUP BY product_id, product_name
HAVING SUM(quantity * price) > 10000
ORDER BY total_revenue DESC;
```

**Common patterns:**

**Count by category:**

```sql
SELECT 
    category,
    COUNT(*) AS product_count
FROM products
GROUP BY category;
```

**Sales by year:**

```sql
SELECT 
    YEAR(order_date) AS year,
    SUM(amount) AS total_sales
FROM orders
GROUP BY YEAR(order_date)
ORDER BY year;
```

**Average by range:**

```sql
SELECT 
    CASE
        WHEN age < 18 THEN 'Minor'
        WHEN age BETWEEN 18 AND 65 THEN 'Adult'
        ELSE 'Senior'
    END AS age_group,
    COUNT(*) AS count,
    AVG(age) AS avg_age
FROM users
GROUP BY age_group;
```

**Interview tip:** GROUP BY groups rows with same values. Use it with aggregate functions to calculate per group. HAVING filters groups after aggregation (WHERE filters rows before). Remember: WHERE comes before GROUP BY, HAVING comes after."

---

### Q18: What are Joins?

**How to Answer:**

"Joins combine rows from two or more tables based on a related column. They're used to fetch data that's spread across multiple tables.

**Why joins are needed:**

Instead of storing all data in one table (redundant):

```
❌ BAD - Redundant data
orders table:
+----------+-----------+------------+----------------+
| order_id | user_name | user_email | product_name   |
+----------+-----------+------------+----------------+
| 1        | John      | j@mail.com | Laptop         |
| 2        | John      | j@mail.com | Mouse          |
| 3        | Jane      | jane@mail  | Keyboard       |
+----------+-----------+------------+----------------+
```

We split into related tables and use joins:

```
✅ GOOD - Normalized data

users table:                orders table:
+----+------+------------+  +----------+---------+-------------+
| id | name | email      |  | order_id | user_id | product_id  |
+----+------+------------+  +----------+---------+-------------+
| 1  | John | j@mail.com |  | 1        | 1       | 101         |
| 2  | Jane | jane@mail  |  | 2        | 1       | 102         |
+----+------+------------+  | 3        | 2       | 103         |
                            +----------+---------+-------------+
```

**Types of joins:**

1. **INNER JOIN** - Only matching rows
2. **LEFT JOIN** - All from left table + matches from right
3. **RIGHT JOIN** - All from right table + matches from left
4. **FULL OUTER JOIN** - All rows from both tables
5. **CROSS JOIN** - Cartesian product (every combination)
6. **SELF JOIN** - Table joined with itself

**Interview tip:** Joins combine data from multiple tables based on related columns (usually foreign key relationships). They avoid data redundancy and allow querying across related entities."

---

### Q19: INNER JOIN

**How to Answer:**

"INNER JOIN returns only the rows where there's a match in both tables. It's the most common type of join.

**Syntax:**

```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

**Basic example:**

```sql
-- Get orders with user names
SELECT 
    orders.order_id,
    users.name,
    orders.product_name,
    orders.amount
FROM orders
INNER JOIN users ON orders.user_id = users.id;
```

**Visual representation:**

```
users:                    orders:
+----+-------+            +----------+---------+-------------+
| id | name  |            | order_id | user_id | product     |
+----+-------+            +----------+---------+-------------+
| 1  | John  | ←─────────| 101      | 1       | Laptop      |
| 2  | Jane  | ←─────────| 102      | 2       | Mouse       |
| 3  | Bob   |    X      | 103      | 1       | Keyboard    |
+----+-------+            +----------+---------+-------------+
                                               
INNER JOIN result (only matches):
+----------+-------+----------+
| order_id | name  | product  |
+----------+-------+----------+
| 101      | John  | Laptop   |
| 102      | Jane  | Mouse    |
| 103      | John  | Keyboard |
+----------+-------+----------+
Bob is excluded (no orders)
```

**Multiple JOINs:**

```sql
SELECT 
    orders.order_id,
    users.name AS customer_name,
    products.product_name,
    products.price,
    orders.quantity,
    (products.price * orders.quantity) AS total
FROM orders
INNER JOIN users ON orders.user_id = users.id
INNER JOIN products ON orders.product_id = products.id;
```

**JOIN with WHERE:**

```sql
-- Orders from NYC users, amount > $100
SELECT 
    orders.order_id,
    users.name,
    orders.amount
FROM orders
INNER JOIN users ON orders.user_id = users.id
WHERE users.city = 'NYC'
  AND orders.amount > 100;
```

**Table aliases (shorthand):**

```sql
-- Using aliases for readability
SELECT 
    o.order_id,
    u.name,
    o.product_name
FROM orders o
INNER JOIN users u ON o.user_id = u.id;
-- Shorter and clearer
```

**Joining on multiple columns:**

```sql
SELECT *
FROM table1 t1
INNER JOIN table2 t2
  ON t1.column1 = t2.column1
  AND t1.column2 = t2.column2;
```

**Interview tip:** INNER JOIN returns only rows with matches in both tables. Use ON to specify the join condition (usually foreign key = primary key). Most common join type."

---

### Q20: LEFT JOIN (LEFT OUTER JOIN)

**How to Answer:**

"LEFT JOIN returns ALL rows from the left table and matching rows from the right table. If no match, right side is NULL.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```

**Visual representation:**

```
users (LEFT):             orders (RIGHT):
+----+-------+            +----------+---------+
| id | name  |            | order_id | user_id |
+----+-------+            +----------+---------+
| 1  | John  | ←─────────| 101      | 1       |
| 2  | Jane  | ←─────────| 102      | 2       |
| 3  | Bob   |    (no match)
+----+-------+            +----------+---------+
                                               
LEFT JOIN result (all from left):
+----+-------+----------+
| id | name  | order_id |
+----+-------+----------+
| 1  | John  | 101      |
| 2  | Jane  | 102      |
| 3  | Bob   | NULL     | ← Bob included with NULL
+----+-------+----------+
```

**Example - All users with their orders (if any):**

```sql
SELECT 
    u.name,
    o.order_id,
    o.product_name
FROM users u
LEFT JOIN orders o ON u.id = o.user_id;
```

Result:
```
+-------+----------+--------------+
| name  | order_id | product_name |
+-------+----------+--------------+
| John  | 101      | Laptop       |
| John  | 102      | Mouse        |
| Jane  | 103      | Keyboard     |
| Bob   | NULL     | NULL         | ← User with no orders
+-------+----------+--------------+
```

**Find users with NO orders:**

```sql
SELECT u.name
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
WHERE o.order_id IS NULL;
```

Result:
```
+-------+
| name  |
+-------+
| Bob   | ← Only users with no orders
+-------+
```

**Count orders per user (including zero):**

```sql
SELECT 
    u.name,
    COUNT(o.order_id) AS order_count
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
GROUP BY u.id, u.name;
```

Result:
```
+-------+-------------+
| name  | order_count |
+-------+-------------+
| John  | 2           |
| Jane  | 1           |
| Bob   | 0           | ← Shows 0 instead of excluding
+-------+-------------+
```

**When to use LEFT JOIN:**

- Want all records from left table regardless of match
- Finding records WITHOUT matches (orphans)
- Optional relationships
- Reporting that needs to show zero counts

**Interview tip:** LEFT JOIN returns all rows from left table and matching rows from right. If no match, right columns are NULL. Use it to find records without relationships (WHERE right.id IS NULL)."

---

### Q21: RIGHT JOIN (RIGHT OUTER JOIN)

**How to Answer:**

"RIGHT JOIN returns ALL rows from the right table and matching rows from the left table. It's the opposite of LEFT JOIN.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```

**Visual representation:**

```
orders (LEFT):            users (RIGHT):
+----------+---------+    +----+-------+
| order_id | user_id |    | id | name  |
+----------+---------+    +----+-------+
| 101      | 1       |────→| 1  | John  |
| 102      | 2       |────→| 2  | Jane  |
                      (no match)| 3  | Bob   |
+----------+---------+    +----+-------+
                                               
RIGHT JOIN result (all from right):
+----------+-------+
| order_id | name  |
+----------+-------+
| 101      | John  |
| 102      | Jane  |
| NULL     | Bob   | ← Bob included with NULL
+----------+-------+
```

**Example:**

```sql
SELECT 
    o.order_id,
    u.name
FROM orders o
RIGHT JOIN users u ON o.user_id = u.id;

-- Same as:
SELECT 
    o.order_id,
    u.name
FROM users u
LEFT JOIN orders o ON u.id = o.user_id;
```

**Note:** RIGHT JOIN is less common. Usually people rewrite as LEFT JOIN by swapping table order.

**Interview tip:** RIGHT JOIN returns all rows from right table. It's less commonly used - most people use LEFT JOIN instead by swapping the table order."

---

### Q22: FULL OUTER JOIN

**How to Answer:**

"FULL OUTER JOIN returns ALL rows from both tables. Where there's a match, combines them. Where no match, fills with NULL.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Visual representation:**

```
users:                    orders:
+----+-------+            +----------+---------+
| id | name  |            | order_id | user_id |
+----+-------+            +----------+---------+
| 1  | John  | ←─────────| 101      | 1       |
| 2  | Jane  |    X      | 102      | 99      | ← No user 99
| 3  | Bob   |    (no order)
+----+-------+            +----------+---------+
                                               
FULL OUTER JOIN result (all from both):
+----+-------+----------+---------+
| id | name  | order_id | user_id |
+----+-------+----------+---------+
| 1  | John  | 101      | 1       | ← Match
| 2  | Jane  | NULL     | NULL    | ← User, no order
| 3  | Bob   | NULL     | NULL    | ← User, no order
| NULL | NULL| 102      | 99      | ← Order, no user
+----+-------+----------+---------+
```

**Example:**

```sql
SELECT 
    u.name,
    o.order_id
FROM users u
FULL OUTER JOIN orders o ON u.id = o.user_id;
```

**Note:** Not supported in MySQL. Use UNION of LEFT and RIGHT JOIN:

```sql
-- MySQL alternative
SELECT u.name, o.order_id
FROM users u
LEFT JOIN orders o ON u.id = o.user_id

UNION

SELECT u.name, o.order_id
FROM users u
RIGHT JOIN orders o ON u.id = o.user_id;
```

**When to use:** Rare. Used when you need all data from both tables regardless of matches.

**Interview tip:** FULL OUTER JOIN returns all rows from both tables, with NULLs where there's no match. Not commonly used. Not supported in MySQL."

---

### Q23: Self Join

**How to Answer:**

"A self join is when a table is joined with itself. Used for hierarchical data or comparing rows within the same table.

**Example - Employee hierarchy:**

```sql
employees table:
+----+----------+------------+
| id | name     | manager_id |
+----+----------+------------+
| 1  | CEO      | NULL       |
| 2  | Manager1 | 1          |
| 3  | Manager2 | 1          |
| 4  | Employee1| 2          |
| 5  | Employee2| 2          |
+----+----------+------------+
```

**Find each employee with their manager:**

```sql
SELECT 
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.id;
```

Result:
```
+-----------+----------+
| employee  | manager  |
+-----------+----------+
| CEO       | NULL     |
| Manager1  | CEO      |
| Manager2  | CEO      |
| Employee1 | Manager1 |
| Employee2 | Manager1 |
+-----------+----------+
```

**Use case - Find pairs:**

```sql
-- Find users from same city
SELECT 
    u1.name AS user1,
    u2.name AS user2,
    u1.city
FROM users u1
JOIN users u2 ON u1.city = u2.city
WHERE u1.id < u2.id;  -- Avoid duplicates
```

**Interview tip:** Self join joins a table with itself. Common for hierarchical data (employees/managers) or finding relationships within the same table. Use aliases to distinguish between the two references to the same table."

---

## MongoDB Basics

### Q24: What is MongoDB?

**How to Answer:**

"MongoDB is a NoSQL database that stores data in JSON-like documents instead of tables. It's flexible, scalable, and great for unstructured or semi-structured data.

**Key characteristics:**

**Document-oriented:**
Data stored in documents (like JSON objects), not rows.

```javascript
// MongoDB document
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "name": "John",
  "age": 25,
  "email": "john@email.com",
  "hobbies": ["reading", "gaming"],
  "address": {
    "city": "NYC",
    "zip": "10001"
  }
}
```

**Schema-flexible:**
Documents in same collection can have different fields.

```javascript
// User 1 - has phone
{ "name": "John", "email": "john@email.com", "phone": "123-456" }

// User 2 - no phone, has age
{ "name": "Jane", "email": "jane@email.com", "age": 30 }
```

**Key features:**

1. **No fixed schema** - Add fields anytime
2. **Nested data** - Can embed documents
3. **Arrays** - Native array support
4. **Scalability** - Easy horizontal scaling
5. **Indexing** - Like SQL for performance
6. **Aggregation** - Powerful data processing pipeline

**When to use MongoDB:**

✅ Good for:
- Flexible/changing schema
- Hierarchical data
- Rapid development
- Large scale (millions of documents)
- Real-time applications

❌ Not ideal for:
- Complex transactions across multiple documents
- Complex joins
- Financial systems needing ACID guarantees

**Interview tip:** MongoDB is a NoSQL document database. Stores data as JSON-like documents, schema-flexible, supports nesting and arrays. Good for flexible schemas and scalability."

---

### Q25: SQL vs MongoDB Terminology

**How to Answer:**

"SQL and MongoDB use different terminology for similar concepts.

**Mapping:**

| SQL | MongoDB | Description |
|-----|---------|-------------|
| Database | Database | Container for tables/collections |
| Table | Collection | Group of records/documents |
| Row | Document | Single record |
| Column | Field | Single attribute |
| Primary Key | _id | Unique identifier |
| Index | Index | Fast lookup |
| JOIN | $lookup | Combine data |
| Table | Collection | Group of related data |

**Visual comparison:**

**SQL:**
```
Database: company
  └── Table: users
       └── Rows:
            ├── id | name  | email
            ├── 1  | John  | j@...
            └── 2  | Jane  | jane@...
```

**MongoDB:**
```
Database: company
  └── Collection: users
       └── Documents:
            ├── { "_id": 1, "name": "John", "email": "j@..." }
            └── { "_id": 2, "name": "Jane", "email": "jane@..." }
```

**Example comparison:**

**SQL Table:**
```
users table:
+----+------+-------+------------------+
| id | name | age   | email            |
+----+------+-------+------------------+
| 1  | John | 25    | john@email.com   |
+----+------+-------+------------------+
```

**MongoDB Collection:**
```javascript
// users collection
{
  "_id": ObjectId("..."),
  "name": "John",
  "age": 25,
  "email": "john@email.com"
}
```

**Interview tip:** Database and Database are the same. Table→Collection, Row→Document, Column→Field. MongoDB's _id is like SQL's Primary Key."

---

### Q27: Find - Reading Data

**How to Answer:**

"In MongoDB, find() retrieves documents from a collection. It's like SELECT in SQL.

**Basic syntax:**

```javascript
db.collection.find(query, projection)
```

**Find all documents:**

```javascript
// SQL: SELECT * FROM users;
db.users.find()
```

**Find with filter:**

```javascript
// SQL: SELECT * FROM users WHERE age = 25;
db.users.find({ age: 25 })

// SQL: SELECT * FROM users WHERE city = 'NYC';
db.users.find({ city: "NYC" })
```

**Find one document:**

```javascript
// Returns first match
db.users.findOne({ name: "John" })
```

**Comparison operators:**

```javascript
// Greater than: age > 25
db.users.find({ age: { $gt: 25 } })

// Less than: age < 30
db.users.find({ age: { $lt: 30 } })

// Greater than or equal: age >= 25
db.users.find({ age: { $gte: 25 } })

// Less than or equal: age <= 30
db.users.find({ age: { $lte: 30 } })

// Not equal: age != 25
db.users.find({ age: { $ne: 25 } })
```

**Multiple conditions (AND):**

```javascript
// SQL: WHERE age > 25 AND city = 'NYC'
db.users.find({
  age: { $gt: 25 },
  city: "NYC"
})
```

**OR conditions:**

```javascript
// SQL: WHERE age < 20 OR age > 60
db.users.find({
  $or: [
    { age: { $lt: 20 } },
    { age: { $gt: 60 } }
  ]
})
```

**IN operator:**

```javascript
// SQL: WHERE city IN ('NYC', 'LA', 'Chicago')
db.users.find({
  city: { $in: ["NYC", "LA", "Chicago"] }
})
```

**Projection (select specific fields):**

```javascript
// SQL: SELECT name, email FROM users;
db.users.find(
  {},  // no filter
  { name: 1, email: 1, _id: 0 }  // 1=include, 0=exclude
)
```

**Sort, limit, skip:**

```javascript
// SQL: SELECT * FROM users ORDER BY age DESC LIMIT 10;
db.users.find()
  .sort({ age: -1 })  // -1 = descending
  .limit(10)

// Pagination
db.users.find()
  .sort({ _id: 1 })
  .skip(20)
  .limit(10)
```

**Count:**

```javascript
// SQL: SELECT COUNT(*) FROM users WHERE age > 25;
db.users.countDocuments({ age: { $gt: 25 } })
```

**Interview tip:** find() retrieves documents. Use filter object for WHERE conditions. Operators like $gt, $lt for comparisons. Use projection to select specific fields."

---

### Q29: Insert - Adding Data

**How to Answer:**

"In MongoDB, insert adds documents to a collection.

**Insert one document:**

```javascript
// SQL: INSERT INTO users (name, age, email) VALUES ('John', 25, 'john@...');
db.users.insertOne({
  name: "John",
  age: 25,
  email: "john@email.com"
})
```

**Insert multiple documents:**

```javascript
// SQL: INSERT multiple rows
db.users.insertMany([
  { name: "John", age: 25, email: "john@email.com" },
  { name: "Jane", age: 30, email: "jane@email.com" },
  { name: "Bob", age: 28, email: "bob@email.com" }
])
```

**Auto-generated _id:**

```javascript
// MongoDB auto-generates _id if not provided
db.users.insertOne({ name: "John" })
// Creates: { "_id": ObjectId("..."), "name": "John" }
```

**Interview tip:** insertOne() for single document, insertMany() for multiple. _id is auto-generated if not provided (like auto-increment in SQL)."

---

### Q30: Update - Modifying Data

**How to Answer:**

"In MongoDB, update modifies existing documents.

**Update one document:**

```javascript
// SQL: UPDATE users SET age = 26 WHERE name = 'John';
db.users.updateOne(
  { name: "John" },      // filter
  { $set: { age: 26 } }  // update
)
```

**Update multiple documents:**

```javascript
// SQL: UPDATE users SET status = 'active' WHERE city = 'NYC';
db.users.updateMany(
  { city: "NYC" },
  { $set: { status: "active" } }
)
```

**Update operators:**

```javascript
// Increment
db.users.updateOne(
  { name: "John" },
  { $inc: { age: 1 } }  // age = age + 1
)

// Add to array
db.users.updateOne(
  { name: "John" },
  { $push: { hobbies: "gaming" } }
)

// Remove field
db.users.updateOne(
  { name: "John" },
  { $unset: { age: "" } }  // Remove age field
)
```

**Upsert (insert if not exists):**

```javascript
db.users.updateOne(
  { name: "Charlie" },
  { $set: { age: 35 } },
  { upsert: true }  // Insert if doesn't exist
)
```

**Interview tip:** updateOne() for single document, updateMany() for multiple. Use $set to update fields, $inc to increment, $push for arrays. Upsert inserts if document doesn't exist."

---

### Q31: Delete - Removing Data

**How to Answer:**

"In MongoDB, delete removes documents from a collection.

**Delete one document:**

```javascript
// SQL: DELETE FROM users WHERE name = 'John';
db.users.deleteOne({ name: "John" })
```

**Delete multiple documents:**

```javascript
// SQL: DELETE FROM users WHERE age > 60;
db.users.deleteMany({ age: { $gt: 60 } })
```

**Delete all documents:**

```javascript
// SQL: DELETE FROM users;
db.users.deleteMany({})  // Empty filter = all documents
```

**Interview tip:** deleteOne() removes first match, deleteMany() removes all matching documents. Use empty filter {} to delete all."

---

### Q37: Lookup - Joins in MongoDB

**How to Answer:**

"$lookup performs joins in MongoDB, combining documents from different collections.

**SQL JOIN:**

```sql
SELECT u.name, o.product
FROM users u
JOIN orders o ON u._id = o.user_id;
```

**MongoDB $lookup (equivalent):**

```javascript
db.users.aggregate([
  {
    $lookup: {
      from: "orders",           // join with orders collection
      localField: "_id",        // field from users
      foreignField: "user_id",  // field from orders
      as: "user_orders"         // output array name
    }
  }
])
```

**Result:**

```javascript
{
  "_id": 1,
  "name": "John",
  "user_orders": [  // Array of matching orders
    { "_id": 101, "user_id": 1, "product": "Laptop" },
    { "_id": 102, "user_id": 1, "product": "Mouse" }
  ]
}
```

**Interview tip:** $lookup is MongoDB's join. Use it in aggregation pipeline. Results are embedded as an array in the parent document."

---

### Q38: SQL vs MongoDB - Side by Side Comparison

**How to Answer:**

"Here's a quick reference comparing common operations:

**SELECT / Find:**

```sql
-- SQL
SELECT * FROM users WHERE age > 25;

-- MongoDB
db.users.find({ age: { $gt: 25 } })
```

**INSERT:**

```sql
-- SQL
INSERT INTO users (name, age) VALUES ('John', 25);

-- MongoDB
db.users.insertOne({ name: "John", age: 25 })
```

**UPDATE:**

```sql
-- SQL
UPDATE users SET age = 26 WHERE name = 'John';

-- MongoDB
db.users.updateOne(
  { name: "John" },
  { $set: { age: 26 } }
)
```

**DELETE:**

```sql
-- SQL
DELETE FROM users WHERE age > 60;

-- MongoDB
db.users.deleteMany({ age: { $gt: 60 } })
```

**COUNT:**

```sql
-- SQL
SELECT COUNT(*) FROM users WHERE city = 'NYC';

-- MongoDB
db.users.countDocuments({ city: "NYC" })
```

**ORDER BY:**

```sql
-- SQL
SELECT * FROM users ORDER BY age DESC LIMIT 10;

-- MongoDB
db.users.find().sort({ age: -1 }).limit(10)
```

**GROUP BY:**

```sql
-- SQL
SELECT city, COUNT(*) FROM users GROUP BY city;

-- MongoDB
db.users.aggregate([
  { $group: { _id: "$city", count: { $sum: 1 } } }
])
```

**JOIN:**

```sql
-- SQL
SELECT u.name, o.product
FROM users u JOIN orders o ON u.id = o.user_id;

-- MongoDB
db.users.aggregate([
  {
    $lookup: {
      from: "orders",
      localField: "_id",
      foreignField: "user_id",
      as: "orders"
    }
  }
])
```

**Interview tip:** Know the MongoDB equivalents of common SQL operations. Main differences: MongoDB uses methods (find, insertOne), SQL uses keywords (SELECT, INSERT). MongoDB has flexible schema, SQL has fixed schema."

---

### Q39: When to Use SQL vs MongoDB?

**How to Answer:**

"Choose based on your data structure and requirements.

**Use SQL when:**

✅ Fixed schema (structure doesn't change much)
✅ Complex relationships and joins
✅ ACID transactions are critical (banking, finance)
✅ Data integrity is paramount
✅ Complex queries with multiple JOINs
✅ Mature tools and ecosystem

**Examples:** Banking systems, ERP, CRM, E-commerce orders

**Use MongoDB when:**

✅ Flexible/changing schema
✅ Hierarchical/nested data
✅ Rapid development (prototyping)
✅ Horizontal scalability needed
✅ Document-like data (JSON)
✅ High write loads

**Examples:** Content management, catalogs, real-time analytics, IoT, social networks

**Quick decision table:**

| Requirement | SQL | MongoDB |
|-------------|-----|---------|
| Fixed schema | ✅ | ❌ |
| Flexible schema | ❌ | ✅ |
| Complex joins | ✅ | ⚠️ |
| ACID transactions | ✅ | ⚠️ |
| Horizontal scaling | ⚠️ | ✅ |
| Nested data | ⚠️ | ✅ |
| Rapid prototyping | ❌ | ✅ |

**Can use both:**

Many companies use both - SQL for transactional data, MongoDB for flexible/document data.

**Interview tip:** SQL for structured data with complex relationships. MongoDB for flexible schemas and scalability. Neither is universally better - depends on use case."

---

### Q40: Common Interview Questions

**How to Answer:**

"Here are frequently asked database questions for freshers:

**1. What's the difference between SQL and NoSQL?**

SQL: Relational, fixed schema, tables, ACID, vertical scaling
NoSQL: Non-relational, flexible schema, documents/key-value, horizontal scaling

**2. Explain INNER JOIN vs LEFT JOIN**

INNER: Only matching rows from both tables
LEFT: All from left + matching from right (NULLs for non-matches)

**3. What is a primary key?**

Unique identifier for each row. Cannot be NULL. Only one per table.

**4. What's the difference between WHERE and HAVING?**

WHERE: Filters rows before grouping
HAVING: Filters groups after GROUP BY

**5. How do you prevent SQL injection?**

Use parameterized queries/prepared statements. Never concatenate user input into SQL strings.

**6. What is normalization?**

Organizing database to reduce redundancy. Splitting data into related tables.

**7. What's the difference between DELETE and TRUNCATE?**

DELETE: Removes rows, can use WHERE, can rollback, slower
TRUNCATE: Removes all rows, no WHERE, faster, resets auto-increment

**8. Explain MongoDB's _id field**

Auto-generated unique identifier. Like primary key in SQL. ObjectId type (timestamp + random).

**9. How to find duplicate records?**

```sql
SELECT column, COUNT(*) as count
FROM table
GROUP BY column
HAVING COUNT(*) > 1;
```

**10. Second highest salary?**

```sql
SELECT MAX(salary) FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);
```

**11. Difference between CHAR and VARCHAR?**

CHAR: Fixed length, padded with spaces
VARCHAR: Variable length, only uses needed space

**12. What is indexing?**

Data structure for fast lookups. Like book index. Speeds up SELECT, slows down INSERT/UPDATE.

**13. MongoDB aggregation pipeline?**

Series of stages that process documents: $match, $group, $sort, $project, $lookup

**14. Self join example?**

Employee-Manager relationship in same table:

```sql
SELECT e.name as Employee, m.name as Manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.id;
```

**15. Count documents by field in MongoDB?**

```javascript
db.users.aggregate([
  { $group: { _id: "$city", count: { $sum: 1 } } }
])
```

**Practice these patterns - they're very common in fresher interviews!"**

---

## Summary for Interview Preparation

**SQL Must-Know:**
1. SELECT, INSERT, UPDATE, DELETE
2. WHERE, ORDER BY, LIMIT
3. COUNT, SUM, AVG, MIN, MAX
4. GROUP BY, HAVING
5. INNER JOIN, LEFT JOIN
6. Primary Key, Foreign Key

**MongoDB Must-Know:**
1. find(), insertOne/Many()
2. updateOne/Many(), deleteOne/Many()
3. Comparison operators ($gt, $lt, etc.)
4. sort(), limit(), skip()
5. Aggregation basics ($group, $match)
6. $lookup for joins

**Key Differences:**
- SQL: Tables/Rows/Columns, fixed schema
- MongoDB: Collections/Documents/Fields, flexible schema
- SQL: Strong for complex joins and transactions
- MongoDB: Strong for flexible schemas and scalability

**Interview Tips:**
- Always write queries clearly with proper formatting
- Explain your reasoning (why this join type, why this approach)
- Mention performance considerations (indexes, avoid SELECT *)
- Know when to use SQL vs MongoDB
- Practice writing queries by hand (whiteboard coding)

Good luck with your interviews! 
