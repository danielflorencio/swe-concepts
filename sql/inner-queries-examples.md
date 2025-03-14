# SQL Inner Queries Examples

## 1. Simple Inner Query (Subquery)
A subquery is a query nested inside another query.

**Example:** Find the names of employees with the highest salary.
```sql
SELECT name
FROM employees
WHERE salary = (SELECT MAX(salary) FROM employees);
```

## 2. Inner Query with IN Clause
**Example:** Get the names of students who have enrolled in at least one course.
```sql
SELECT name
FROM students
WHERE id IN (SELECT student_id FROM enrollments);
```

## 3. Inner Query with EXISTS Clause
**Example:** Get a list of customers who have placed at least one order.
```sql
SELECT name
FROM customers
WHERE EXISTS (
    SELECT 1
    FROM orders
    WHERE customers.id = orders.customer_id
);
```

## 4. Inner Query with JOIN
**Example:** Get the average salary of employees in each department.
```sql
SELECT d.name AS department_name, AVG(e.salary) AS average_salary
FROM departments d
JOIN (
    SELECT department_id, salary
    FROM employees
) e ON d.id = e.department_id
GROUP BY d.name;
```

## 5. Inner Query with Aggregation
**Example:** Find departments where the average salary is greater than 50,000.
```sql
SELECT name
FROM departments
WHERE id IN (
    SELECT department_id
    FROM employees
    GROUP BY department_id
    HAVING AVG(salary) > 50000
);
```

## 6. Correlated Subquery
**Example:** Get employees whose salary is above the average salary of their department.
```sql
SELECT name, salary
FROM employees e1
WHERE salary > (
    SELECT AVG(salary)
    FROM employees e2
    WHERE e1.department_id = e2.department_id
);
```

## 7. Nested Subqueries
**Example:** Get the names of employees who earn more than the average salary in their department, and their department's average is above the global average.
```sql
SELECT name
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees e1
    WHERE e1.department_id = employees.department_id
    AND AVG(salary) > (
        SELECT AVG(salary)
        FROM employees
    )
);
```

## 8. Inner Query with UPDATE
**Example:** Increase the salary of employees who earn less than the average salary by 10%.
```sql
UPDATE employees
SET salary = salary * 1.10
WHERE salary < (
    SELECT AVG(salary)
    FROM employees
);
```

## 9. Inner Query with DELETE
**Example:** Delete employees who haven’t made any sales.
```sql
DELETE FROM employees
WHERE id NOT IN (
    SELECT employee_id
    FROM sales
);
```

## 10. Inner Query with UNION
**Example:** Get a list of all cities from both customers and suppliers.
```sql
SELECT city FROM customers
UNION
SELECT city FROM suppliers;
```

### Key Takeaways
- Inner queries are powerful tools to enhance data retrieval and manipulation.
- Use them with aggregate functions, `IN`, `EXISTS`, and even within `UPDATE` and `DELETE` statements.
- Make sure to consider performance when using nested or correlated subqueries.
