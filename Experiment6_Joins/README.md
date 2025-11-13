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
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

Sample table: customer
```
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
 ```       
Sample table: orders
```
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
```

```sql
SELECT o.ord_no,
o.purch_amt,
c.cust_name,
c.city
FROM orders o
INNER JOIN customer c
  ON o.customer_id=c.customer_id
WHERE o.purch_amt BETWEEN 500 AND 2000;
```

**Output:**

<img width="1200" height="366" alt="Screenshot 2025-10-27 153603" src="https://github.com/user-attachments/assets/ce83e8cd-ee62-4f6a-806b-871aecaf06dd" />


**Question 2**
---
 From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.

Sample table: customer
```
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
```
Sample table: salesman
```
 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```

```sql
SELECT c.cust_name AS "Customer Name",
c.city,
s.name AS Salesman,
s.commission
FROM customer c
INNER JOIN salesman s
  ON c.salesman_id=s.salesman_id;
  
```

**Output:**

<img width="1201" height="762" alt="Screenshot 2025-10-27 153618" src="https://github.com/user-attachments/assets/62429b5f-fcad-4e2e-a554-5472a9ff44b0" />


**Question 3**
---
From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission.  

Sample table: customer
```
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
```
Sample table: salesman
```
 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```
```sql
SELECT c.cust_name AS "Customer Name",
c.city,
s.name AS Salesman,
s.city,
s.commission
FROM customer c
JOIN salesman s
  ON c.salesman_id=s.salesman_id
WHERE c.city<>s.city AND s.commission>0.12;
```

**Output:**

<img width="1032" height="369" alt="Screenshot 2025-10-27 153641" src="https://github.com/user-attachments/assets/c5736546-7cfb-4ec3-9721-d49c8dd5673f" />


**Question 4**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for salesman with the name 'Mc Lyon'.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)
Salesman Table: (salesman_id, name, city, commission)

```sql
SELECT
c.customer_id,
c.cust_name,
c.city,
c.grade,
s.salesman_id
FROM customer c
LEFT JOIN salesman s
  ON c.salesman_id=s.salesman_id
WHERE s.name="Mc Lyon";
```

**Output:**

<img width="1045" height="217" alt="Screenshot 2025-10-27 153655" src="https://github.com/user-attachments/assets/1fa1fce8-97a7-49a8-803b-519caa8ecc60" />


**Question 5**
---
Write an SQL query to select all columns from the 'customer' table (aliased as 'c') by performing a LEFT JOIN with the 'orders' table on the 'customer_id' column, including only those orders where the order date falls between '2012-08-01' and '2012-08-30'.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)
'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

```sql
SELECT
c.*
FROM customer c
LEFT JOIN orders o
  ON c.customer_id=o.customer_id
WHERE o.ord_date BETWEEN "2012-08-01" AND "2012-08-30";
```

**Output:**

<img width="1059" height="280" alt="Screenshot 2025-10-27 153708" src="https://github.com/user-attachments/assets/d5658094-1215-422a-8914-c70a095ba9be" />


**Question 6**
---
Write the SQL query that achieves the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column. Include conditions to filter for patients discharged between '2024-03-01' and '2024-03-31' but not admitted during the same period.

PATIENTS TABLE:
```
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT
```
SURGERIES TABLE:
```
name             type
---------------  ---------------
surgery_id       INT
patient_id       INT
surgeon_id       INT
surgery_date     DATE
```

```sql
SELECT p.first_name,s.*
FROM patients p
INNER JOIN surgeries s
  ON p.patient_id=s.patient_id
WHERE discharge_date BETWEEN "2024-03-01" AND "2024-03-31";

```

**Output:**

<img width="1065" height="226" alt="Screenshot 2025-10-27 153716" src="https://github.com/user-attachments/assets/74e6c6de-a032-4b48-bea4-071fe3552b97" />


**Question 7**
---
Write the SQL query that accomplishes the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

PATIENTS TABLE:
```
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT
```
SURGERIES TABLE:
```
name             type
---------------  ---------------
surgery_id       INT
patient_id       INT
surgeon_id       INT
surgery_date     DATE
```

```sql
SELECT p.first_name,s.*
FROM patients p
INNER JOIN surgeries s
  ON p.patient_id=s.patient_id
WHERE p.first_name="Alice";
```

**Output:**

<img width="1061" height="217" alt="Screenshot 2025-10-27 153820" src="https://github.com/user-attachments/assets/6be0625f-77e2-4e31-9913-1bbede343908" />


**Question 8**
---
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id. 

Sample table: customer
```
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
```
Sample table: salesman
```
 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```

```sql
SELECT
c.cust_name,
c.city,
c.grade,
s.name AS Salesman,
s.city
FROM customer c
INNER JOIN salesman s
  ON c.salesman_id=s.salesman_id
WHERE c.grade<300
ORDER BY c.customer_id ASC;
```

**Output:**

<img width="1026" height="462" alt="Screenshot 2025-10-27 153838" src="https://github.com/user-attachments/assets/d342384b-f177-46aa-8499-892047dba17b" />


**Question 9**
---
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

Sample table: salesman
```
 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```
Sample table: customer
```
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
```

```sql
SELECT s.name AS Salesman,
c.cust_name,c.city
FROM salesman s
JOIN customer c
  ON s.city=c.city;
```

**Output:**

<img width="685" height="417" alt="Screenshot 2025-10-27 153858" src="https://github.com/user-attachments/assets/10e60c88-700c-40e1-a2f6-d87079486034" />



**Question 10**
---
Write the SQL query that achieves the selection of the first name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date of '2024-01-15'.:

PATIENTS TABLE:
```
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT
```
SURGERIES TABLE:
```
name             type
---------------  ---------------
surgery_id       INT
patient_id       INT
surgeon_id       INT
surgery_date     DATE
```

```sql
SELECT p.first_name
FROM patients p
INNER JOIN surgeries s
  ON p.patient_id=s.patient_id
WHERE s.surgery_date="2024-01-15";
```

**Output:**

<img width="284" height="217" alt="Screenshot 2025-10-27 153908" src="https://github.com/user-attachments/assets/ee4042be-c5a7-4059-88c3-e838da7f26d3" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.


