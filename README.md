# TASK-6
Objective: Use subqueries in SELECT, WHERE, and FROM

Deliverables:SQL queries with nested logic

1.Use scalar and correlated subqueries
2.Use subqueries inside IN, EXISTS, =
Outcome:     Advanced query logic skils

 1. Scalar Subquery
-- Get the name and salary of employees who earn the highest salary
SELECT name, salary
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
);


2. Correlated Subquery
 -- Find employees earning above their department's average
SELECT name, salary, department_id
FROM employees e1
WHERE salary > (
    SELECT AVG(salary)
    FROM employees e2
    WHERE e2.department_id = e1.department_id
);

3. Subquery with IN
-- Get employees working in departments with average salary > 55000
SELECT name, department_id
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM employees
    GROUP BY department_id
    HAVING AVG(salary) > 55000
);

4. Subquery with EXISTS
 -- Show departments that have at least one employee earning more than 60000
SELECT DISTINCT department_id
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department_id = d.department_id
    AND e.salary > 60000
);

5. Subquery with =
 -- Show department name of the employee with emp_id = 3
SELECT department_name
FROM departments
WHERE department_id = (
    SELECT department_id
    FROM employees
    WHERE emp_id = 3
);
