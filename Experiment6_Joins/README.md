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

PATIENTS TABLE:

name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

SURGERIES TABLE:

name             type
---------------  ---------------
surgery_id       INT
patient_id       INT
surgeon_id       INT
surgery_date     DATE


```sql

SELECT p.admission_date, s.surgery_date
FROM patients p
INNER JOIN surgeries s
ON p.patient_id = s.patient_id;


```

**Output:**

<img width="548" height="360" alt="image" src="https://github.com/user-attachments/assets/f055e60f-eb11-40bc-9bca-4e10c7b5dfdd" />


**Question 2**
---

Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for patients admitted between '2024-01-01' and '2024-01-31'.

<img width="606" height="103" alt="image" src="https://github.com/user-attachments/assets/d472b10a-691a-4f48-9a8e-c189335a2cc5" />

<img width="558" height="94" alt="image" src="https://github.com/user-attachments/assets/05d4a38f-43e6-4da8-a94c-33c16bc34d9c" />


```sql

SELECT p.first_name AS patient_name, t.*
FROM patients p
INNER JOIN test_results t
ON p.patient_id = t.patient_id
WHERE p.admission_date BETWEEN '2024-01-01' AND '2024-01-31';

```

**Output:**

<img width="1236" height="250" alt="image" src="https://github.com/user-attachments/assets/d75f4c46-0aa4-4696-a480-47de65fdb1c1" />


**Question 3**

---

Write the SQL query that achieves the selection of all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

<img width="588" height="96" alt="image" src="https://github.com/user-attachments/assets/e146484d-a969-451e-adb4-13580c729020" />

<img width="595" height="103" alt="image" src="https://github.com/user-attachments/assets/b802929a-3b78-4813-beaa-963cc349f07b" />


```sql

SELECT t.*
FROM test_results t
INNER JOIN patients p
ON t.patient_id = p.patient_id
WHERE p.first_name = 'Alice';



```

**Output:**

<img width="1220" height="249" alt="image" src="https://github.com/user-attachments/assets/d835af02-54fb-46c4-bbcc-282f063fbcc5" />


**Question 4**

---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the specialization from the "doctors" table (aliased as "Doctor_specialization"), with an inner join on the "doctor_id" column and a condition filtering for patients admitted between '2024-01-01' and '2024-01-31'.

PATIENTS TABLE:
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

DOCTORS TABLE:

name             type
---------------  ---------------
doctor_id        INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
specialization   VARCHAR(100)


```sql

SELECT p.first_name AS patient_name, d.specialization AS Doctor_specialization
FROM patients p
INNER JOIN doctors d
ON p.doctor_id = d.doctor_id
WHERE p.admission_date BETWEEN '2024-01-01' AND '2024-01-31';

```

**Output:**



**Question 5**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with an order date later than '2012-08-17'.

<img width="595" height="101" alt="image" src="https://github.com/user-attachments/assets/fa832780-40bb-490d-9ad5-3dab09ce53a7" />

<img width="574" height="96" alt="image" src="https://github.com/user-attachments/assets/54a408fa-a914-4beb-98f6-3e9f0ff5cf9c" />






```sql

SELECT c.*
FROM customer c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.ord_date > '2012-08-17';

```

**Output:**

<img width="1238" height="601" alt="image" src="https://github.com/user-attachments/assets/44b95824-f591-4915-b440-990888bd239d" />


**Question 6**

---
doctor_id" column.

PATIENTS TABLE:
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

DOCTORS TABLE:

name             type
---------------  ---------------
doctor_id        INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
specialization   VARCHAR(100)



```sql


SELECT p.*, d.first_name AS doctor_name
FROM patients p
INNER JOIN doctors d
ON p.doctor_id = d.doctor_id;

```

**Output:**

<img width="1230" height="370" alt="image" src="https://github.com/user-attachments/assets/e5a8c598-7dfd-4be1-ae16-2948da4a0bee" />


**Question 7**

---
Write the SQL query that achieves the selection of the first name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date of '2024-01-15'.:

PATIENTS TABLE:

name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

SURGERIES TABLE:

name             type
---------------  ---------------
surgery_id       INT
patient_id       INT
surgeon_id       INT
surgery_date     DATE


```sql

SELECT p.first_name
FROM patients p
INNER JOIN surgeries s
ON p.patient_id = s.patient_id
WHERE s.surgery_date = '2024-01-15';

```

**Output:**

<img width="313" height="265" alt="image" src="https://github.com/user-attachments/assets/1e415a12-47ec-4850-8807-7f586221b9d8" />


**Question 8**

---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for test results with the test name 'Blood Pressure'.

<img width="610" height="105" alt="image" src="https://github.com/user-attachments/assets/b40494ff-f06f-4d50-84de-8c561de79043" />

<img width="577" height="96" alt="image" src="https://github.com/user-attachments/assets/0cd639a4-8ad1-4a3e-8e0d-5f70993c3140" />


```sql

SELECT p.first_name AS patient_name, t.*
FROM patients p
INNER JOIN test_results t
ON p.patient_id = t.patient_id
WHERE t.test_name = 'Blood Pressure';

```

**Output:**

<img width="1234" height="255" alt="image" src="https://github.com/user-attachments/assets/6cfde811-c2dd-4fa4-b61b-5b08be33c434" />


**Question 9**
---

Write the SQL query that accomplishes the selection of the first name and last name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date between '2024-01-01' and '2024-01-31'.

PATIENTS TABLE:

name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

SURGERIES TABLE:

name             type
---------------  ---------------
surgery_id       INT
patient_id       INT
surgeon_id       INT
surgery_date     DATE


```sql

SELECT p.first_name, p.last_name
FROM patients p
INNER JOIN surgeries s
ON p.patient_id = s.patient_id
WHERE s.surgery_date BETWEEN '2024-01-01' AND '2024-01-31';

```

**Output:**

<img width="544" height="250" alt="image" src="https://github.com/user-attachments/assets/335f1b42-ef71-46e4-9712-de9b8ae23df5" />


**Question 10**
---

Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the test name from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

<img width="566" height="107" alt="image" src="https://github.com/user-attachments/assets/14433297-8f4f-494b-8553-b4816cfdac65" />

<img width="563" height="92" alt="image" src="https://github.com/user-attachments/assets/75c8278e-f37c-4e4e-bb79-3d35dedd60ae" />


```sql

SELECT p.first_name AS patient_name, t.test_name
FROM patients p
INNER JOIN test_results t
ON p.patient_id = t.patient_id;

```

**Output:**

<img width="557" height="366" alt="image" src="https://github.com/user-attachments/assets/9bb44023-2644-440b-9562-367f64ce4a9a" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
