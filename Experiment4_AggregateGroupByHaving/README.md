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
<img width="789" height="419" alt="image" src="https://github.com/user-attachments/assets/847d1fcd-bd96-497c-8b95-d9dc8060fa54" />


```sql
SELECT SUM(inventory) AS total_available_amount
FROM fruits
WHERE price > 0.5;

```

**Output:**

<img width="576" height="237" alt="image" src="https://github.com/user-attachments/assets/9517a4a5-2d0e-4e12-a8ff-844458848fc5" />


**Question 2**
---
<img width="596" height="381" alt="image" src="https://github.com/user-attachments/assets/97ffb2f6-d5a7-42f2-a856-b0d5b83726da" />


```sql
SELECT AVG(LENGTH(email)) AS avg_email_length
FROM customer;

```

**Output:**

<img width="420" height="247" alt="image" src="https://github.com/user-attachments/assets/5e0fa412-1192-4d7d-be2c-6a0f37a164b3" />


**Question 3**
---
<img width="738" height="402" alt="image" src="https://github.com/user-attachments/assets/f9261805-3f1b-45b5-8646-fcc4583bc754" />


```sql
SELECT COUNT(*) AS COUNT
FROM customer
WHERE city = 'Noida';

```

**Output:**

<img width="346" height="239" alt="image" src="https://github.com/user-attachments/assets/caa3c97a-c0de-40be-938e-f4d40d9c86fc" />


**Question 4**
---
<img width="787" height="379" alt="image" src="https://github.com/user-attachments/assets/75bb7f9d-6340-4cb3-b8b5-2acac488d0fe" />


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
<img width="810" height="353" alt="image" src="https://github.com/user-attachments/assets/f7903295-e97f-4846-b874-718491ebc753" />


```sql
SELECT gender AS Gender, COUNT(*) AS TotalPatients
FROM Patients
GROUP BY gender;

```

**Output:**

<img width="509" height="276" alt="image" src="https://github.com/user-attachments/assets/20dc3c5e-23e9-4602-ba8e-c318a2b3ffa2" />


**Question 6**
---
<img width="775" height="392" alt="image" src="https://github.com/user-attachments/assets/9a350ffc-5679-4b5e-b2e7-432d54dc26cb" />


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

<img width="544" height="359" alt="image" src="https://github.com/user-attachments/assets/8c065d71-0011-47f8-817f-2354fbb839e0" />


**Question 7**
---
<img width="1264" height="386" alt="image" src="https://github.com/user-attachments/assets/5d1f9dad-57af-4b80-8ecd-f32299eacef8" />


```sql
SELECT age, MAX(income) AS "MAX(income)"
FROM employee
GROUP BY age
HAVING MAX(income) > 2000000;

```

**Output:**

<img width="512" height="285" alt="image" src="https://github.com/user-attachments/assets/a9de7258-cb46-4440-ae43-802164ff7bd3" />


**Question 8**
---
<img width="1255" height="430" alt="image" src="https://github.com/user-attachments/assets/0cc2a425-7682-4175-9d14-f750aac8e18d" />


```sql
SELECT occupation, MIN(workhour) AS "MIN(workhour)"
FROM employee1
GROUP BY occupation
HAVING MIN(workhour) > 8;

```

**Output:**
<img width="620" height="386" alt="image" src="https://github.com/user-attachments/assets/653b3473-3b9a-4cbf-bd1b-e9ad61d7f7b0" />


**Question 9**
---
<img width="1279" height="371" alt="image" src="https://github.com/user-attachments/assets/c8c27c52-ba70-401f-bc36-4f27f5292db8" />


```sql
SELECT jdate, AVG(workhour) AS "AVG(workhour)"
FROM employee1
GROUP BY jdate
HAVING AVG(workhour) < 10;

```

**Output:**

<img width="551" height="257" alt="image" src="https://github.com/user-attachments/assets/496549de-4764-4ec5-b25e-b94d741ecbe1" />


**Question 10**
---
<img width="1251" height="370" alt="image" src="https://github.com/user-attachments/assets/c465f96f-7f98-47f3-ace4-3dac9b79e388" />


```sql
SELECT (age/5)*5 AS age_group, MIN(age) 
FROM customer1
GROUP BY (age/5)*5
HAVING MIN(age) < 25;

```

**Output:**

<img width="582" height="233" alt="image" src="https://github.com/user-attachments/assets/754bb967-be59-4acb-a81c-79d5fa7c4e84" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
