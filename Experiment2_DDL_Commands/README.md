# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

|RollNo   |   Name     |       Gender    |  Subject |     MARKS|
|----------|  ------------|    ---------- | ----------|   ----------|
|205       |  Olivia Green |   F       |            |
|207        | Liam Smith    |  M        |   Mathematics|  85|
|208         |Sophia Johnson | F         |  Science|

```
insert into Student_details(RollNo,Name,Gender)
values (205,'Olivia Green','F');
insert into Student_details(RollNo,Name,Gender,Subject,MARKS)
values (207,'Liam Smith','M','Mathematics',85);
insert into Student_details(RollNo,Name,Gender,Subject)
values (208,'Sophia Johnson','F','Science');
```

**Output:**

<img width="1189" height="341" alt="Screenshot 2025-09-29 132730" src="https://github.com/user-attachments/assets/3ce02c4d-0ee4-4b41-af00-1c300828681a" />


**Question 2**
---
Write a SQL query to Add a new column named "discount" with the data type DECIMAL(5,2) to the "customer" table.

Sample table: customer

 |customer_id |   cust_name    |    city    | grade | salesman_id| 
|-------------|----------------|------------|-------|-------------|
|3002 | Nick Rimando   | New York   |   100 |        5001|
|3007 | Brad Davis     | New York   |   200 |        5001|
| 3005 | Graham Zusi    | California |   200 |        5002|

```
alter table customer
add discount DECIMAL(5,2);
```

**Output:**

<img width="1193" height="431" alt="Screenshot 2025-09-29 133045" src="https://github.com/user-attachments/assets/9e418115-fe28-443d-9897-f9bd90fb876f" />


**Question 3**
---
Write an SQL query to add a new column salary of type INTEGER to the Employees table, with a CHECK constraint that ensures the value in this column is greater than 0.

```
alter table Employees
add column salary INTEGER CHECK (salary>0);
```

**Output:**

<img width="1189" height="344" alt="Screenshot 2025-09-29 133151" src="https://github.com/user-attachments/assets/017bc2c7-a840-4c1b-a8f6-ebbcf5c8840b" />


**Question 4**
---
Insert a new product with ProductID 101, Name Laptop, Category Electronics, Price 1500, and Stock 50 into the Products table.

```
insert into Products(ProductID,Name,Category,Price,Stock)
values (101,'Laptop','Electronics',1500,50);
```

**Output:**

<img width="1181" height="221" alt="Screenshot 2025-09-29 133256" src="https://github.com/user-attachments/assets/a35bd458-3dcb-4b4f-b723-62148549fccd" />


**Question 5**
---
Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.

```
create table Department(DepartmentID int primary key,
DepartmentName TEXT NOT NULL UNIQUE,
Location TEXT);
```

**Output:**

<img width="1183" height="268" alt="Screenshot 2025-09-29 133413" src="https://github.com/user-attachments/assets/ea8c7478-c932-4d19-86dd-454986e3b88d" />


**Question 6**
---
Create a new table named item with the following specifications and constraints:
1.item_id as TEXT and as primary key.
2.item_desc as TEXT.
3.rate as INTEGER.
4.icom_id as TEXT with a length of 4.
5.icom_id is a foreign key referencing com_id in the company table.
6.The foreign key should cascade updates and deletes.
7.item_desc and rate should not accept NULL.

```
create table item(
item_id TEXT PRIMARY KEY,
item_desc TEXT NOT NULL,
rate INT NOT NULL,
icom_id TEXT(4),
FOREIGN KEY(icom_id)references company(com_id)
ON UPDATE CASCADE
ON DELETE CASCADE);
```

**Output:**

<img width="1186" height="345" alt="Screenshot 2025-09-29 133702" src="https://github.com/user-attachments/assets/fe54ce49-45a5-4084-b78a-eb122188e1bb" />


**Question 7**
---
Create a new table named contacts with the following specifications:
1.contact_id as INTEGER and primary key.
2.first_name as TEXT and not NULL.
3.last_name as TEXT and not NULL.
4.email as TEXT.
5.phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.

```
create table contacts(
contact_id integer primary key,
first_name TEXT NOT NULL,
last_name TEXT NOT NULL,
email TEXT,
phone  TEXT NOT NULL CHECK(LENGTH(phone)>=10));
```

**Output:**

<img width="1181" height="314" alt="Screenshot 2025-09-29 133839" src="https://github.com/user-attachments/assets/ecee75eb-4f11-48c1-a1a4-78d60cc68158" />


**Question 8**
---
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

```
INSERT INTO Books (ISBN, Title, Author, Publisher, YearPublished)
SELECT ISBN, Title, Author, Publisher, YearPublished FROM Out_of_print_books;
```

**Output:**

<img width="1185" height="272" alt="Screenshot 2025-09-29 133940" src="https://github.com/user-attachments/assets/4dd5dbd6-48a9-46cc-9935-e8942209b704" />


**Question 9**
---
Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT

```
CREATE TABLE Reviews (
ReviewID  INTEGER,
ProductID  INTEGER,
Rating  REAL,
ReviewText  TEXT);
```

**Output:**

<img width="1182" height="385" alt="Screenshot 2025-09-29 134059" src="https://github.com/user-attachments/assets/f23504df-b795-42c1-bee6-f1267b922d23" />


**Question 10**
---
Create a table named Events with the following columns:

EventID as INTEGER
EventName as TEXT
EventDate as DATE

```
create table Events(
EventID INTEGER,
EventName TEXT,
EventDate DATE);
```

**Output:**

<img width="1180" height="360" alt="Screenshot 2025-09-29 134229" src="https://github.com/user-attachments/assets/1d16d585-ed18-4fe6-b6a9-6d1d0a597919" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
