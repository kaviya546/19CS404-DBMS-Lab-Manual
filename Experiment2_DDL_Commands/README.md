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
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.
<img width="1130" height="64" alt="image" src="https://github.com/user-attachments/assets/ac3312fa-469d-4508-aa7b-05eb8616ff4e" />


```sql

CREATE TABLE ProjectAssignments (
    AssignmentID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    ProjectID INTEGER,
    AssignmentDate DATE NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
    FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
);

```

**Output:**

<img width="1235" height="146" alt="image" src="https://github.com/user-attachments/assets/998f2d54-536a-438d-8c82-c85414ff9c02" />

**Question 2**
---

Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0

<img width="672" height="136" alt="image" src="https://github.com/user-attachments/assets/1b2ccb8f-6b1b-4447-866e-fe64b776d80c" />



```sql

INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
SELECT RollNo, Name, Gender, Subject, MARKS
FROM Archived_students;

```

**Output:**

<img width="1206" height="139" alt="image" src="https://github.com/user-attachments/assets/c41a4669-5788-4380-b6f4-c5bf4a8c1862" />


**Question 3**
---

Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.

<img width="1218" height="106" alt="image" src="https://github.com/user-attachments/assets/19f7d0d2-14d1-423c-ab1f-9aff3fad9431" />


```sql

CREATE TABLE Attendance (
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    AttendanceDate DATE,
    Status TEXT CHECK (Status IN ('Present', 'Absent', 'Leave')),
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);

```

**Output:**

<img width="1230" height="135" alt="image" src="https://github.com/user-attachments/assets/648f3d51-f28e-4082-a7e5-55e4458a4ea2" />


**Question 4**
---

Write an SQL query to add two new columns, first_name and last_name, to the table employee. Both columns should have a data type of varchar(50).

<img width="742" height="155" alt="image" src="https://github.com/user-attachments/assets/bf887ea1-67bd-48e9-b5a7-21c615781000" />


```sql

ALTER TABLE employee ADD COLUMN first_name varchar(50);
ALTER TABLE employee ADD COLUMN last_name varchar(50);

```

**Output:**

<img width="1228" height="172" alt="image" src="https://github.com/user-attachments/assets/73f18066-25d8-4d69-9696-aaca7becab19" />


**Question 5**
---

Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL


```sql

CREATE TABLE Bonuses (
    BonusID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    BonusAmount REAL CHECK (BonusAmount > 0),
    BonusDate DATE,
    Reason TEXT NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);

```

**Output:**

<img width="1231" height="136" alt="image" src="https://github.com/user-attachments/assets/2a2b57c8-29c2-4a25-b374-c44fe99528b6" />


**Question 6**
---

Write a SQL query to add a column named Date_of_birth as Date in the Student_details table.

<img width="793" height="206" alt="image" src="https://github.com/user-attachments/assets/a6a1a2cb-cd84-4055-bd13-0010351ee5ed" />


```sql

ALTER TABLE Student_details
ADD COLUMN Date_of_birth Date;

```

**Output:**

<img width="1220" height="196" alt="image" src="https://github.com/user-attachments/assets/8b2b4b89-7b08-478a-9f03-e9759815d669" />


**Question 7**
---

Insert the following employees into the Employee table:

EmployeeID  Name        Position    Department  Salary
----------  ----------  ----------  ----------  ----------
2           John Smith  Developer   IT          75000
3           Anna Bell   Designer    Marketing   68000



```sql

INSERT INTO Employee (EmployeeID, Name, Position, Department, Salary)
VALUES 
(2, 'John Smith', 'Developer', 'IT', 75000),
(3, 'Anna Bell', 'Designer', 'Marketing', 68000);


```

**Output:**

<img width="1234" height="200" alt="image" src="https://github.com/user-attachments/assets/6b15890c-1c2b-417c-bcc1-923f37264b2a" />


**Question 8**
---

In the Books table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ISBN             Title                      Author           Publisher   Year
---------------  -------------------------  ---------------  ----------  ----------
978-1234567890   Introduction to AI         John Doe
978-9876543210   Deep Learning              Jane Doe         TechPress   2022
978-1122334455   Cybersecurity Essentials   Alice Smith                  2021

<img width="755" height="144" alt="image" src="https://github.com/user-attachments/assets/31d6f79f-4b1d-4366-b6ab-2cae98e5a103" />


```sql

-- Record with some NULL fields
INSERT INTO Books (ISBN, Title, Author)
VALUES ('978-1234567890', 'Introduction to AI', 'John Doe');

-- Record with all fields filled (no NULL)
INSERT INTO Books (ISBN, Title, Author, Publisher, Year)
VALUES ('978-9876543210', 'Deep Learning', 'Jane Doe', 'TechPress', 2022);

-- Record with some fields filled, others NULL
INSERT INTO Books (ISBN, Title, Author, Year)
VALUES ('978-1122334455', 'Cybersecurity Essentials', 'Alice Smith', 2021);

```

**Output:**

<img width="1240" height="142" alt="image" src="https://github.com/user-attachments/assets/4186c799-2167-4e23-a6b3-a9f2f792ea84" />


**Question 9**
---

Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.


<img width="1016" height="94" alt="image" src="https://github.com/user-attachments/assets/d00ad51b-9cb9-40d2-8e26-9c1d733238e7" />


```sql


CREATE TABLE Employees (
    EmployeeID INTEGER PRIMARY KEY,
    FirstName TEXT NOT NULL,
    LastName TEXT NOT NULL,
    Email TEXT UNIQUE,
    Salary REAL CHECK (Salary > 0),
    DepartmentID INTEGER,
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);


```

**Output:**


<img width="1235" height="252" alt="image" src="https://github.com/user-attachments/assets/38c104db-ae72-4ee0-ba07-6898c4b72ae7" />


**Question 10**
---

Create a table named Customers with the following columns:

CustomerID as INTEGER
Name as TEXT
Email as TEXT
JoinDate as DATETIME


<img width="732" height="156" alt="image" src="https://github.com/user-attachments/assets/ea222152-6b99-482f-ae85-7ee9defc97ff" />


```sql

CREATE TABLE Customers (
    CustomerID INTEGER,
    Name TEXT,
    Email TEXT,
    JoinDate DATETIME
);

```

**Output:**


<img width="1239" height="231" alt="image" src="https://github.com/user-attachments/assets/13b81778-79b0-4bcc-93ae-0e227f8b98ed" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
