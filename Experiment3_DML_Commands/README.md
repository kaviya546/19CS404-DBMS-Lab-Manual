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
-- Write a SQL query to identify the top 3 most expensive discounted products. Return product_id, original_price, discount_percentage, and discounted_price.

Sample table: Products

product_id | original_price | discount_percentage

 ------------+----------------+--------------------- 

101 | 50.00 | 0.10 

102 | 150.00 | 0.15 

103 | 200.00 | 0.20 

104 | 300.00 | 0.25

```sql
-- SELECT 
    product_id,
    original_price,
    discount_percentage,
    original_price * (1 - discount_percentage) AS discounted_price
FROM Products
ORDER BY discounted_price DESC
LIMIT 3;

```

**Output:**

<img width="1086" height="199" alt="image" src="https://github.com/user-attachments/assets/92702c56-7972-49aa-adf3-23f980b5e7ad" />


**Question 2**
---
-- Write a SQL query to assess the performance of value2 as 'Poor', 'Average', or 'Excellent' based on whether it is less than 30, between 30 and 70, or greater than 70 in the Calculations table

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0

```sql
-- SELECT 
    id,
    value2,
    CASE
        WHEN value2 < 30 THEN 'Poor'
        WHEN value2 BETWEEN 30 AND 70 THEN 'Average'
        WHEN value2 > 70 THEN 'Excellent'
    END AS performance
FROM Calculations;

```

**Output:**

<img width="648" height="335" alt="image" src="https://github.com/user-attachments/assets/7a163623-0da2-46bb-a9a1-7fe6c0f28b10" />

**Question 3**
---
-- Write a SQL query to Get the employee names where the first letter of each word is the same.

 
Table name: emp

name        type
----------  ----------
empno       INT
ename       VARCHAR(100)
job         VARCHAR(50)
mgr         INT
hiredate    DATE
sal         DECIMAL(10,2)
comm        DECIMAL(10,2)
deptno      INT

```sql
-- SELECT ename
FROM emp
WHERE UPPER(SUBSTR(ename, 1, 1)) = UPPER(SUBSTR(ename, INSTR(ename, ' ') + 1, 1));

```

**Output:**

<img width="404" height="314" alt="image" src="https://github.com/user-attachments/assets/0ad6f04b-9288-4e79-8acf-dd69ee9da7be" />


**Question 4**
---
-- Update the total selling price to quantity sold multiplied by updated selling price per unit where product id is 10 in the sales table.

SALES TABLE
name               type
-----------------  ---------------
sale_id            INT
sale_date          DATE
product_id         INT
quantity           INT
sell_price         DECIMAL(10,2)
total_sell_price   DECIMAL(10,2)

```sql
-- UPDATE sales
SET total_sell_price = quantity * sell_price
WHERE product_id = 10;

```

**Output:**

<img width="1246" height="400" alt="image" src="https://github.com/user-attachments/assets/e218396c-22db-4158-a722-e725063ff273" />


**Question 5**
---
-- <img width="824" height="364" alt="image" src="https://github.com/user-attachments/assets/abb83f94-1974-4314-8151-90d579d82cb3" />


```sql
-- SELECT name, city
FROM salesman
WHERE city IN ('London', 'Rome');

```

**Output:**

<img width="578" height="268" alt="image" src="https://github.com/user-attachments/assets/1089a54f-e169-4e9d-9810-c1e4fc22760e" />


**Question 6**
---
-- Write a SQL statement to Change the category to 'Household' where product name contains 'Detergent' in the products table.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lvl    INT        
quantity       INT      

```sql
-- UPDATE products
SET category = 'Household'
WHERE product_name LIKE '%Detergent%';

```

**Output:**


<img width="1259" height="406" alt="image" src="https://github.com/user-attachments/assets/3f1dca31-05d5-473d-957c-e6d1f00263bd" />


**Question 7**
---

-- <img width="1261" height="238" alt="image" src="https://github.com/user-attachments/assets/cc0031e0-452a-460a-8b48-98d07001d80f" />


```sql
-- DELETE FROM customer
WHERE OPENING_AMT BETWEEN 4000 AND 6000;

```

**Output:**


<img width="1243" height="494" alt="image" src="https://github.com/user-attachments/assets/f59126ac-8228-4559-b341-0e25007a034f" />


**Question 8**
---
-- Write a SQL query to calculate the number of days between the hiredate and a specified date ('2024-12-31') for each employee using the JULIANDAY function from the emp table.

emp table

cid         name        type        
----------  ----------  ---------- 
0           empno       INT         
1           ename       VARCHAR(100)
2           job         VARCHAR(50)
3           mgr         INT        
4           hiredate    DATE        
5           sal         DECIMAL(10,2)  
6           comm        DECIMAL(10,2)  
7           deptno      INT         

```sql
-- SELECT ename,
       hiredate,
       JULIANDAY('2024-12-31') - JULIANDAY(hiredate) AS days_worked
FROM emp;

```

**Output:**


<img width="642" height="203" alt="image" src="https://github.com/user-attachments/assets/9a805109-74d8-4e4e-92e5-b81ad4a9ae43" />


**Question 9**
---

-- <img width="1276" height="249" alt="image" src="https://github.com/user-attachments/assets/a9177ffd-40de-49c8-b2fc-f77e90289c29" />


```sql
-- DELETE FROM customer
WHERE GRADE >= 2;

```

**Output:**


<img width="684" height="435" alt="image" src="https://github.com/user-attachments/assets/e7fdd79f-bf53-4f87-8504-b3544627ecc9" />


**Question 10**
---
-- Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
-- DELETE FROM Doctors
WHERE doctor_id BETWEEN 2 AND 4;

```

**Output:**


<img width="1018" height="662" alt="image" src="https://github.com/user-attachments/assets/ba95c9fa-9c30-49d9-8dde-95c466045ce4" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
