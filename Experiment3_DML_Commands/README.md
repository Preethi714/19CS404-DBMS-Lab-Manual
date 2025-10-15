# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Write a SQL statement to Increase the selling price by 10% for all products in the 'Bakery' category in the products table.

Products table

product_id,
product_name,
category,
cost_price,
sell_price,
reorder_lvl,
quantity,
supplier_id

```
update Products
set sell_price=sell_price*1.10
where category='Bakery';
```

**Output:**

<img width="1186" height="515" alt="Screenshot 2025-10-15 101645" src="https://github.com/user-attachments/assets/69e50ade-2f59-466b-b76b-00e84a7b29a0" />


**Question 2**
---
Write a SQL statement to Update the grade of all customers in Chennai city as  5. 

Customer table (customer_id,cust_name,city,grade,salesman_id)

```
update Customer
set grade=5
where city ='Chennai';
```

**Output:**

<img width="1185" height="465" alt="Screenshot 2025-10-15 101734" src="https://github.com/user-attachments/assets/88a023e8-399d-43f7-93f6-0627bdf2a8c8" />


**Question 3**
---
Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.
Sample table: Doctors
attributes : doctor_id, first_name, last_name, specialization


```
delete from Doctors
where doctor_id between 2 and 4;
```

**Output:**

<img width="1182" height="847" alt="Screenshot 2025-10-15 101949" src="https://github.com/user-attachments/assets/e7cff624-aa99-4fab-a94f-474e81119cc2" />

**Question 4**
---
Write a SQL query to delete a doctor from Doctors table whose Specialization is 'Pediatrics' and First name is 'Michael'.
Sample table: Doctors
attributes : doctor_id, first_name, last_name, specialization

```
delete from Doctors
where specialization='Pediatrics'
and first_name='Michael';
```

**Output:**

<img width="1181" height="374" alt="Screenshot 2025-10-15 102047" src="https://github.com/user-attachments/assets/cd7e527f-350e-4b98-9eff-9c698a025dc6" />

**Question 5**
---
Write a SQL query to Delete a Specific Surgery which was made on 28th Feb 2024.
Sample table: Surgeries
attributes: surgery_id, patient_id, surgeon_id, surgery_date

```
delete from Surgeries
where surgery_date='2024-02-28';
```

**Output:**

<img width="1187" height="373" alt="Screenshot 2025-10-15 102242" src="https://github.com/user-attachments/assets/6046d168-9c80-42f4-a7de-f5af29fdd044" />


**Question 6**
---
Write a SQL statement to Find those salesmen with all information whose name containing the 1st character is 'N' and the 4th character is 'l' and rests may be any character.
salesman table

|cid      |   name     |    type    |    
|----------|  ----------- | ----------|  
|0        |   salesman_id | numeric(5)  |
|1         |name         |varchar(30)  |
|2         |  city       |  varchar(15)  |
|3        |   commission |  decimal(5,2)|  

```
select*
from salesman
where name like 'N%';
```

**Output:**

<img width="1179" height="317" alt="Screenshot 2025-10-15 102522" src="https://github.com/user-attachments/assets/46339ab0-3db1-4321-b96e-8a07345cbd3c" />


**Question 7**
---
Write a query to list all products that have a discounted price between $100 and $250. Return product_id, original_price, discount_percentage, and discounted_price from products table.

```
select product_id,original_price,discount_percentage,original_price*(1-discount_percentage) as discounted_price
from products
where original_price*(1-discount_percentage) between 100 and 250;
```

**Output:**

<img width="1184" height="280" alt="Screenshot 2025-10-15 102719" src="https://github.com/user-attachments/assets/94276b28-2b49-448e-bc77-8426d4e7bf8f" />


**Question 8**
---
Write a SQL query to retrieve the year, month, and day from the hiredate column in the emp table.

```
select STRFTIME('%Y',hiredate) as Year,
STRFTIME('%m',hiredate) as Month,
strftime('%d',hiredate) as Day
from emp;
```

**Output:**

<img width="764" height="351" alt="Screenshot 2025-10-15 102828" src="https://github.com/user-attachments/assets/23d95818-bb3d-466a-b0e1-8822c34b3dd6" />


**Question 9**
---
Change the supplier name to upper case where contact person contains ' Singh' in suppliers table.

|name           |    type|
|-----------------|  ---------------|
|supplier_id       | INT|
|supplier_name    |  VARCHAR(100)|
|contact_person  |   VARCHAR(100)|
|phone_number   |    VARCHAR(20)|
|email         |     VARCHAR(100)|
|address      |      VARCHAR(250)|

```
update suppliers
set supplier_name=upper(supplier_name)
where contact_person like '%Singh%';
```

**Output:**

<img width="1181" height="342" alt="Screenshot 2025-10-15 103057" src="https://github.com/user-attachments/assets/f2fd1b7d-1875-4202-9d85-8a2a30b6a8d1" />


**Question 10**
---
Write a SQL query to determine the age group of value1 in the Calculations table as 'Child' if it is less than 13, 'Teen' if it is between 13 and 19, and 'Adult' if it is 20 or older.

|cid      |   name    |    type      |  notnull |    dflt_value|  pk|
|---------- | ---------- | ----------|  ----------  |---------- | ----------|
|0          | id          |INTEGER |    0      |             |    1|
|1           |value1      |REAL      |  0        |             |  0|
|2           |value2      |REAL       | 0         |            |  0|
|3           |base       | INTEGER     |0          |           |  0|
|4           |exponent  |  INTEGER    | 0           |          |  0|
|5           |number   |   REAL       | 0            |         |  0|
|6           |decimal |    REAL       | 0             |         | 0|
 

```
select id,value1,
case
    when value1<13 then 'Child'
    when value1 between 13 and 19 then 'Teen'
    else 'Adult'
end as age_group
from calculations;
```

**Output:**

<img width="767" height="341" alt="Screenshot 2025-10-15 103644" src="https://github.com/user-attachments/assets/5405ebc1-1baa-4041-9aaf-4b93a1cb7116" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
