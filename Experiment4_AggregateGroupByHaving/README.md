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
<img width="928" height="434" alt="image" src="https://github.com/user-attachments/assets/4558aebd-7861-40ec-8574-9b8a3b6c7a57" />


```sql
SELECT SUM(inventory) AS total_available_amount
FROM fruits
WHERE price > 0.5;

```

**Output:**

   <img width="509" height="238" alt="image" src="https://github.com/user-attachments/assets/02fb5515-66e7-4e4e-a17e-c99ebcd94482" />

**Question 2**
---
<img width="630" height="351" alt="image" src="https://github.com/user-attachments/assets/aad13283-b080-414f-a942-6c7b128b7511" />


```sql
SELECT AVG(LENGTH(email)) AS avg_email_length
FROM customer;

```

**Output:**

<img width="360" height="236" alt="image" src="https://github.com/user-attachments/assets/efa8cd2a-4712-4b4e-a1ba-a709af6fd69d" />


**Question 3**
---
<img width="739" height="395" alt="image" src="https://github.com/user-attachments/assets/59bceab6-011a-4213-9be3-086f740b0e31" />


```sql
SELECT COUNT(*) AS COUNT
FROM customer
WHERE city = 'Noida';

```

**Output:**

<img width="396" height="235" alt="image" src="https://github.com/user-attachments/assets/83106482-9f68-4e00-ac56-97cc1713a935" />


**Question 4**
---
<img width="895" height="366" alt="image" src="https://github.com/user-attachments/assets/16b978b9-d5c5-4e05-acff-d26525979f18" />


```sql
SELECT 
    DATE_FORMAT(Date, '%Y-%m') AS Month,
    COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY DATE_FORMAT(Date, '%Y-%m')
ORDER BY Month;

```



**Question 5**
---
<img width="848" height="365" alt="image" src="https://github.com/user-attachments/assets/a715e193-203f-4d00-8c22-79f2ea5b0dce" />


```sql
SELECT gender AS Gender, COUNT(*) AS TotalPatients
FROM Patients
GROUP BY gender;

```

**Output:**

<img width="573" height="282" alt="image" src="https://github.com/user-attachments/assets/b056c568-c5a3-41ca-afb8-67be97ca7d45" />


**Question 6**
---
<img width="801" height="402" alt="image" src="https://github.com/user-attachments/assets/1eb32f63-90ee-43c6-ad21-8ac0b6884076" />


```sql
SELECT 
    CASE
        WHEN (CAST(strftime('%Y', 'now') AS INTEGER) - CAST(strftime('%Y', DateOfBirth) AS INTEGER))
             - (strftime('%m-%d', 'now') < strftime('%m-%d', DateOfBirth)) < 20 THEN 'Under 20'
        WHEN (CAST(strftime('%Y', 'now') AS INTEGER) - CAST(strftime('%Y', DateOfBirth) AS INTEGER))
             - (strftime('%m-%d', 'now') < strftime('%m-%d', DateOfBirth)) BETWEEN 20 AND 30 THEN '20-30'
        WHEN (CAST(strftime('%Y', 'now') AS INTEGER) - CAST(strftime('%Y', DateOfBirth) AS INTEGER))
             - (strftime('%m-%d', 'now') < strftime('%m-%d', DateOfBirth)) BETWEEN 31 AND 40 THEN '31-40'
        WHEN (CAST(strftime('%Y', 'now') AS INTEGER) - CAST(strftime('%Y', DateOfBirth) AS INTEGER))
             - (strftime('%m-%d', 'now') < strftime('%m-%d', DateOfBirth)) BETWEEN 41 AND 50 THEN '41-50'
        ELSE 'Above 50'
    END AS AgeGroup,
    COUNT(*) AS TotalPatients
FROM Patients
GROUP BY AgeGroup
ORDER BY MIN((CAST(strftime('%Y', 'now') AS INTEGER) - CAST(strftime('%Y', DateOfBirth) AS INTEGER))
             - (strftime('%m-%d', 'now') < strftime('%m-%d', DateOfBirth)));

```

**Output:**

<img width="600" height="353" alt="image" src="https://github.com/user-attachments/assets/ed108a0a-93cf-4c43-9025-b5ac53a47a08" />


**Question 7**
---
<img width="1212" height="378" alt="image" src="https://github.com/user-attachments/assets/242ec3e7-0ad3-49c0-8db8-4440fa925091" />


```sql
SELECT age, MAX(income) AS "MAX(income)"
FROM employee
GROUP BY age
HAVING MAX(income) > 2000000;

```

**Output:**
<img width="486" height="285" alt="image" src="https://github.com/user-attachments/assets/bfa21413-97c2-4e95-ad3f-db2874da7165" />


**Question 8**
---
<img width="1248" height="426" alt="image" src="https://github.com/user-attachments/assets/a4e5f800-4a2f-44f8-80c7-df317554f886" />


```sql
SELECT occupation, MIN(workhour) AS "MIN(workhour)"
FROM employee1
GROUP BY occupation
HAVING MIN(workhour) > 8;

```

**Output:**

<img width="777" height="375" alt="image" src="https://github.com/user-attachments/assets/1d36ab3b-b2ef-407b-9b48-a87922dabac1" />

**Question 9**
---
<img width="1296" height="365" alt="image" src="https://github.com/user-attachments/assets/da314148-4eb2-413d-b484-96bdde8cbc91" />


```sql
SELECT jdate, AVG(workhour) AS "AVG(workhour)"
FROM employee1
GROUP BY jdate
HAVING AVG(workhour) < 10;

```

**Output:**

<img width="655" height="256" alt="image" src="https://github.com/user-attachments/assets/88328303-69b3-405d-8891-1840c8296a16" />

**Question 10**
---
<img width="1296" height="348" alt="image" src="https://github.com/user-attachments/assets/9a795794-81a5-4d11-acde-00fcf4eead2a" />


```sql
SELECT (age/5)*5 AS age_group, MIN(age) 
FROM customer1
GROUP BY (age/5)*5
HAVING MIN(age) < 25;

```

**Output:**

<img width="594" height="239" alt="image" src="https://github.com/user-attachments/assets/25c0d11e-359e-47d3-b311-5add8d0ce22f" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
