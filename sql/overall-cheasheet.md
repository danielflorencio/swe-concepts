# SQL Cheatsheet for Mid-Level Backend Developers

## 1. Basics of SQL
- **SQL Syntax:** Understand basic syntax and structure of SQL queries.
- **Data Types:**
  - Numeric: `INT`, `FLOAT`, `DECIMAL`, etc.
  - String: `CHAR`, `VARCHAR`, `TEXT`, etc.
  - Date/Time: `DATE`, `TIME`, `TIMESTAMP`, etc.
  - Boolean: `BOOLEAN`
- **SQL Statements:**
  - `SELECT`, `INSERT`, `UPDATE`, `DELETE`
  - `CREATE`, `DROP`, `ALTER`, `TRUNCATE`

## 2. Data Definition Language (DDL)
Defines the structure of the database.
- **Creating Tables:**
  ```sql
  CREATE TABLE users (
      id INT PRIMARY KEY,
      name VARCHAR(50),
      age INT,
      created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
  );
  ```
- **Altering Tables:**
  ```sql
  ALTER TABLE users ADD COLUMN email VARCHAR(100);
  ALTER TABLE users DROP COLUMN age;
  ALTER TABLE users RENAME TO customers;
  ```
- **Dropping Tables:**
  ```sql
  DROP TABLE IF EXISTS users;
  ```
- **Constraints:**
  - `PRIMARY KEY`, `FOREIGN KEY`
  - `UNIQUE`, `NOT NULL`, `CHECK`
  - `DEFAULT`, `AUTO_INCREMENT`

## 3. Data Manipulation Language (DML)
Used for data modification.
- **Inserting Data:**
  ```sql
  INSERT INTO users (name, age) VALUES ('Alice', 25);
  ```
- **Updating Data:**
  ```sql
  UPDATE users SET age = 26 WHERE name = 'Alice';
  ```
- **Deleting Data:**
  ```sql
  DELETE FROM users WHERE age < 18;
  ```
- **Bulk Insert:**
  ```sql
  INSERT INTO users (name, age) VALUES ('Bob', 30), ('Charlie', 22);
  ```

## 4. Data Querying (DQL)
Used for retrieving data from databases.
- **Basic Select Statement:**
  ```sql
  SELECT name, age FROM users;
  ```
- **Distinct Values:**
  ```sql
  SELECT DISTINCT age FROM users;
  ```
- **Ordering Results:**
  ```sql
  SELECT name, age FROM users ORDER BY age DESC;
  ```
- **Limiting Results:**
  ```sql
  SELECT name FROM users LIMIT 5;
  ```
- **Offset for Pagination:**
  ```sql
  SELECT name FROM users LIMIT 5 OFFSET 10;
  ```

## 5. Filtering Data
- **WHERE Clause:**
  ```sql
  SELECT name FROM users WHERE age > 20;
  ```
- **Comparison Operators:** `=`, `!=`, `<`, `>`, `<=`, `>=`
- **Logical Operators:** `AND`, `OR`, `NOT`
- **BETWEEN Operator:**
  ```sql
  SELECT name FROM users WHERE age BETWEEN 18 AND 30;
  ```
- **LIKE Operator (Pattern Matching):**
  ```sql
  SELECT name FROM users WHERE name LIKE 'A%';
  ```
- **IN Operator:**
  ```sql
  SELECT name FROM users WHERE age IN (20, 25, 30);
  ```

## 6. Aggregation and Grouping
- **Aggregate Functions:** `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`
  ```sql
  SELECT COUNT(*) FROM users;
  ```
- **GROUP BY Clause:**
  ```sql
  SELECT age, COUNT(*) FROM users GROUP BY age;
  ```
- **HAVING Clause:**
  ```sql
  SELECT age, COUNT(*) FROM users GROUP BY age HAVING COUNT(*) > 2;
  ```

## 7. Joins
- **Inner Join:**
  ```sql
  SELECT u.name, o.order_date
  FROM users u
  INNER JOIN orders o ON u.id = o.user_id;
  ```
- **Left Join:**
  ```sql
  SELECT u.name, o.order_date
  FROM users u
  LEFT JOIN orders o ON u.id = o.user_id;
  ```
- **Right Join:**
  ```sql
  SELECT u.name, o.order_date
  FROM users u
  RIGHT JOIN orders o ON u.id = o.user_id;
  ```
- **Full Outer Join:**
  ```sql
  SELECT u.name, o.order_date
  FROM users u
  FULL OUTER JOIN orders o ON u.id = o.user_id;
  ```

## 8. Subqueries (Inner Queries)
- **Scalar Subqueries:** Return a single value.
- **Correlated Subqueries:** Reference columns from the outer query.
- **Nested Subqueries:** Multiple levels of inner queries.
- **EXISTS, IN, ANY, ALL:**
  ```sql
  SELECT name FROM users WHERE age > ALL (SELECT age FROM users WHERE city = 'New York');
  ```

## 9. Set Operations
- **UNION and UNION ALL:**
  ```sql
  SELECT name FROM users
  UNION
  SELECT name FROM customers;
  ```
- **INTERSECT:**
  ```sql
  SELECT name FROM users
  INTERSECT
  SELECT name FROM customers;
  ```

## 10. Indexing and Performance Optimization
- **Creating Indexes:**
  ```sql
  CREATE INDEX idx_name ON users(name);
  ```
- **Performance Tips:**
  - Use indexes on frequently queried columns.
  - Avoid unnecessary SELECT *.
  - Use EXPLAIN to analyze query performance.

## 11. Transactions and Concurrency
- **Transaction Management:**
  ```sql
  BEGIN;
  UPDATE accounts SET balance = balance - 100 WHERE id = 1;
  COMMIT;
  ```

## 12. Advanced Concepts
- **Views:**
  ```sql
  CREATE VIEW user_orders AS
  SELECT u.name, o.order_date
  FROM users u
  JOIN orders o ON u.id = o.user_id;
  ```
- **Window Functions:**
  ```sql
  SELECT name, age, RANK() OVER (ORDER BY age DESC) AS rank FROM users;
  ```
- **Common Table Expressions (CTE):**
  ```sql
  WITH user_count AS (
      SELECT COUNT(*) AS total FROM users
  )
  SELECT * FROM user_count;
  ```

## 13. Database Design Concepts
- **Normalization:** 1NF, 2NF, 3NF, BCNF
- **Denormalization:** Performance vs redundancy
- **Entity-Relationship (ER) Diagrams**
- **Database Sharding and Replication**

Master these concepts to solidify your SQL skills as a mid-level backend developer!
