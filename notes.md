# SQL CODING WORKSHOP

primary key = can be a unique column or a combination of columns 

star *  = everything 

hr is the schema and you choose table employees
```sql

SELECT employee_id, last_name, email, manager_id FROM hr.employees 

```

### to compute the unique combinations of columns 
```sql

SELECT DISTINCT col1, col 2, ... col N FROM table employees

```

### compute the number of distinct combinations of order ids

option 1: subqueries
```sql

SELECT COUNT (*)
FROM (
    SELECT DISTINCT order_id
    FROM CO.order_items
    )

```
option 2: counts all the rows where order_id is not null
```sql

SELECT COUNT (order_id) FROM CO.order_items

```
option 3: counts all the rows
```sql

SELECT COUNT (*) FROM CO.order_items

```
option 4: counts  the distinct values of order_id
```sql

SELECT COUNT (DISTINCT order_id) FROM CO.order_items

```
answer: 1950


### compute the number of distinct combinations of order ids and product ids
```sql

SELECT COUNT (*)
FROM (
    SELECT DISTINCT order_id, product_id
    FROM CO.order_items
    )

```
answer: 3914


### order job history by employee_id in ascending order, start_date in descending order and end_date in ascending order
```sql

SELECT employee_id, start_date, end_date
FROM hr.job_history
ORDER BY employee_id, start_date DESC, end_date

```
comment: the DESC argument is applied on each column separetely. ASCENDING is default


### Select all rows in the table hr.employees where either the percentage comission or the manager_id take NULL values
```sql

SELECT * FROM hr.employees WHERE manager_id IS NULL OR commission_pct IS NULL
```

### Find all employees whose last name starts with Sm:
```sql

SELECT * FROM hr.employees WHERE last_name LIKE 'Sm%'

```

### Find all employees whose last name does not start with Sm:
```sql

SELECT * FROM hr.employees WHERE last_name NOT LIKE 'Sm%'

```

### Select the 10 first rows
```sql

SELECT * FROM hr.employees FETCH FIRST 10 ROWS ONLY

```


```sql

SELECT years
FROM(
    SELECT ROUND((CURRENT_DATE - hire_date) / 365, 0 ) Years
    FROM hr.employees
)

```

group_by -> output that reduces the number of rows

parition_by -> preserves the number of rows

### count the number of employees with a comission_pct value different from null for each department 
```sql

SELECT department_id, COUNT(*) as num_employees_with_commission
FROM hr.employees
WHERE commission_pct IS NOT NULL
GROUP BY department_id;

```

### find the avergae salary for each department where there aer more than two employees and order the results by average salary 
```sql
SELECT department_id, AVG(salary) as average_salary
FROM hr.employees
GROUP BY department_id
HAVING COUNT(*) > 2

```


