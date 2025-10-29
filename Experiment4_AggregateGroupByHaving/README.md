# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
How many patients have insurance coverage valid in each year?

Sample table:Insurance Table

|name            |   type|
|-----------------|  ----------|
|InsuranceID       | INTEGER|
|PatientID          |INTEGER|
|InsuranceCompany   |TEXT|
|PolicyNumber       |TEXT|
|PolicyHolder       |TEXT|
|ValidityPeriod     |TEXT|

```
select
SUBSTR(ValidityPeriod, 1, 4) AS
ValidityYear,
Count(DISTINCT PatientID) AS
TotalPatients
from
   Insurance
group by
ValidityYear
Order BY
ValidityYear;
```

**Output:**

<img width="878" height="397" alt="Screenshot 2025-10-29 113122" src="https://github.com/user-attachments/assets/b09f81d3-ebb8-4ecf-ab5f-37ec5b90b6fd" />


**Question 2**
---
What is the average dosage prescribed for each medication?
Sample tablePrescriptions Table

```
select
    Medication,AVG(CAST(SUBSTR(Dosage,1,INSTR(Dosage || ' ',' ')-1) AS REAL)) AS AvgDosage
from
    Prescriptions
GROUP BY
    Medication
Order By
    Medication;
```

**Output:**

<img width="743" height="756" alt="Screenshot 2025-10-29 113131" src="https://github.com/user-attachments/assets/c2d16932-2903-4748-aef6-72fb044b7c41" />


**Question 3**
---
What is the total number of appointments scheduled for each day?

Table: Appointments
|name                | type|
|-------------------  |----------|
|AppointmentID     |   INTEGER|
|PatientID          |  INTEGER|
|DoctorID           |  INTEGER|
|AppointmentDateTime | DATETIME|
|Purpose              |TEXT|
|Status               |TEXT|

```
select 
    DATE(AppointmentDateTime) AS
    AppointmentDate,
    Count(AppointmentId) AS
    TotalAppointments
from 
Appointments
group by
AppointmentDate
order by
AppointmentDate;
```

**Output:**

<img width="762" height="643" alt="Screenshot 2025-10-29 113139" src="https://github.com/user-attachments/assets/546fb629-db5d-4cf5-9a57-3dcf5773acc6" />


**Question 4**
---
Write a SQL query to find the total amount of fruits with a unit type of 'LB'.
Note: Inventory attribute contains amount of fruits
Table: fruits

|name       | type|
|----------  |----------|
|id          |INTEGER|
|name        |TEXT|
|unit        |TEXT|
|inventory   |INTEGER|
|price       |REAL|

```
select
     SUM(inventory) AS total
from 
fruits
where unit='LB';
```

**Output:**

<img width="484" height="296" alt="Screenshot 2025-10-29 113145" src="https://github.com/user-attachments/assets/05af8cd9-ab43-4d0d-a0bc-0c67954aee71" />


**Question 5**
---
Write a SQL query to return the total number of rows in the 'customer' table where the city is not Noida.
Sample table: customer

```
select
     COUNT(*) AS COUNT
from 
customer
where city<> 'Noida';
```

**Output:**

<img width="578" height="317" alt="Screenshot 2025-10-29 113151" src="https://github.com/user-attachments/assets/cc5c4813-355f-495e-8a23-7bbed005e440" />


**Question 6**
---
Write a SQL query to Calculate the average income of the employees with names starting with 'A': 

Table: employee

|name        |type|
|----------  |----------|
|id          |INTEGER|
|name        |TEXT|
|age         |INTEGER|
|city        |TEXT|
|income      |INTEGER|

```
SELECT AVG(income) AS avg_income
from employee
where name like 'A%';
```

**Output:**

<img width="452" height="297" alt="Screenshot 2025-10-29 113157" src="https://github.com/user-attachments/assets/44c3d5ba-bd94-4b18-9e97-b989a8ccfa08" />


**Question 7**
---
Write a SQL query to  find the average salary of all employees?

Table: employee

|name     |   type|
|----------|  ----------|
|id         | INTEGER|
|name        |TEXT|
|age         |INTEGER|
|city      |  TEXT|
|income     | INTEGER|

```
select AVG(income) as Average_Salary
from employee;
```

**Output:**

<img width="497" height="300" alt="Screenshot 2025-10-29 113202" src="https://github.com/user-attachments/assets/ea9f734d-8c21-4d7a-96f0-7026a072ac11" />


**Question 8**
---
Write a SQL query to identify the cities (addresses) where the average salary is greater than Rs. 5000, as per the "customer1" table.

```
select address,AVG(salary)
from customer1
group by address
having avg(salary) >5000;
```

**Output:**

<img width="621" height="427" alt="Screenshot 2025-10-29 113208" src="https://github.com/user-attachments/assets/9528b4d1-4848-47ab-beba-0572f1baa65a" />


**Question 9**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the average work hours for each occupation, and includes only those occupations where the average work hour falls between 10 and 12.

Sample table: employee1

```
select OCCUPATION,AVG(workhour)
from employee1
group by OCCUPATION
having AVG(workhour) between 10 and 12;
```

**Output:**

<img width="640" height="372" alt="Screenshot 2025-10-29 113214" src="https://github.com/user-attachments/assets/e5f59374-720a-474b-926c-098d2117b415" />


**Question 10**
---
Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

Sample table: products

```
SELECT category_id,
count(product_name)
from products
where category_id<3
group by category_id;
```

**Output:**

<img width="732" height="349" alt="image" src="https://github.com/user-attachments/assets/5607a810-1461-45b4-ac42-fdd171a709be" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
