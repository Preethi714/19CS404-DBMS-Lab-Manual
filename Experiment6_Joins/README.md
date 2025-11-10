# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
Write the SQL query that achieves the selection of admission dates from the "patients" table and surgery dates from the "surgeries" table, with an inner join on the "patient_id" column.

```
SELECT 
    p.admission_date, 
    s.surgery_date
FROM 
    patients p
INNER JOIN 
    surgeries s
ON 
    p.patient_id = s.patient_id;

```

**Output:**

<img width="791" height="532" alt="image" src="https://github.com/user-attachments/assets/a5a0fb9d-0c8b-4a4c-ae07-3d0e3f94d1e6" />


**Question 2**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the specialization from the "doctors" table (aliased as "Doctor_specialization"), with an inner join on the "doctor_id" column and a condition filtering for patients admitted between '2024-01-01' and '2024-01-31'.

```
SELECT 
    p.first_name AS patient_name,
    d.specialization AS Doctor_specialization
FROM 
    patients p
INNER JOIN 
    doctors d
ON 
    p.doctor_id = d.doctor_id
WHERE 
    p.admission_date BETWEEN '2024-01-01' AND '2024-01-31';

```

**Output:**

<img width="774" height="390" alt="image" src="https://github.com/user-attachments/assets/e85f6511-4db0-42b1-a7b0-21cf04d1a2a6" />


**Question 3**
---
Write the SQL query that achieves the selection of all columns from the "nurses" table (aliased as "n") and the "department_name" column from the "departments" table, with an inner join on the "department_id" column.

NURSES TABLE:

ATTRIBUTES - nurse_id, first_name, last_name, department_id

```
SELECT 
    n.*, 
    d.department_name
FROM 
    nurses n
INNER JOIN 
    departments d
ON 
    n.department_id = d.department_id;
```

**Output:**

<img width="1237" height="552" alt="image" src="https://github.com/user-attachments/assets/677d5cf1-548d-45df-971d-47be4e6b1215" />


**Question 4**
---
From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission.  

Sample table: customer

```
SELECT
    c.cust_name AS "Customer Name",
    c.city AS city,                 
    s.name AS Salesman,
    s.city AS city,                 
    s.commission
FROM
    customer c
JOIN
    salesman s ON c.salesman_id = s.salesman_id 
WHERE
    c.city <> s.city                         
    AND s.commission > 0.12; 
```

**Output:**

<img width="1239" height="629" alt="image" src="https://github.com/user-attachments/assets/b40346c1-6cfd-4e9b-8541-42ad52f58e21" />


**Question 5**
---
Write the SQL query that achieves the selection of all columns from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers with the name 'Fabian Johns'.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

```
SELECT 
    s.*
FROM 
    salesman s
LEFT JOIN 
    customer c
ON 
    s.salesman_id = c.salesman_id
WHERE 
    c.cust_name = 'Fabian Johns';

```

**Output:**

<img width="1239" height="398" alt="image" src="https://github.com/user-attachments/assets/62d5e4d3-7a69-43d9-a281-ca67d3186a8e" />


**Question 6**
---
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  

Sample table: customer

```
SELECT
    c.cust_name AS cust_name,
    c.city AS city,                 
    c.grade AS grade,
    s.name AS Salesman,
    s.city AS city                  
FROM
    customer c
INNER JOIN
    salesman s ON c.salesman_id = s.salesman_id
ORDER BY
    c.customer_id ASC;
```

**Output:**

<img width="1238" height="916" alt="image" src="https://github.com/user-attachments/assets/421f2363-1511-42f4-8910-8763bd010928" />


**Question 7**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.  

```
SELECT 
    o.ord_no,
    o.purch_amt,
    c.cust_name,
    c.city
FROM 
    orders o
INNER JOIN 
    customer c
ON 
    o.customer_id = c.customer_id
WHERE 
    o.purch_amt BETWEEN 500 AND 2000
ORDER BY 
    o.ord_no;

```

**Output:**

<img width="1239" height="476" alt="Screenshot 2025-11-10 132059" src="https://github.com/user-attachments/assets/ece09340-6521-4fa5-9244-6b7bd5d1a1b0" />


**Question 8**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with a purchase amount less than 100.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

```
SELECT 
    c.cust_name
FROM 
    customer c
LEFT JOIN 
    orders o
ON 
    c.customer_id = o.customer_id
WHERE 
    o.purch_amt < 100;

```

**Output:**

<img width="425" height="456" alt="image" src="https://github.com/user-attachments/assets/bb95c775-eda0-4c48-aeab-2d34e65572b8" />

**Question 9**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c") and the "commission" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

```
SELECT
    c.cust_name,
    s.commission
FROM
    customer c
LEFT JOIN
    salesman s ON c.salesman_id = s.salesman_id;

```

**Output:**

<img width="735" height="907" alt="image" src="https://github.com/user-attachments/assets/ae4c7fe7-492f-4f36-bae3-453af202fcde" />


**Question 10**
---
Write the SQL query that achieves the selection of all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

```
SELECT
    t.*
FROM
    test_results t
INNER JOIN
    patients p ON t.patient_id = p.patient_id
WHERE
    p.first_name = 'Alice';

```

**Output:**

<img width="1241" height="406" alt="image" src="https://github.com/user-attachments/assets/4a2346b2-d5b4-422e-ac59-b6752384fa26" />




## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
