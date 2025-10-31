# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose AGE is LESS than $30

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000



```sql
select * from CUSTOMERS where AGE<30;
```

**Output:**

<img width="1282" height="661" alt="image" src="https://github.com/user-attachments/assets/c8e5a72b-ed49-43b9-a4be-8f93c11cb594" />


**Question 2**
---
Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

customer table

name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int
```sql
select *
from customer
where customer_id =(
    select salesman_id -2001
    from salesman
    where name='Mc Lyon'
);
```

**Output:**

<img width="1281" height="379" alt="image" src="https://github.com/user-attachments/assets/f06a59fc-4e74-4de4-8f9f-cdeba46d15ed" />


**Question 3**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is EQUAL TO $1500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

```sql
select * from CUSTOMERS where salary=1500;
```

**Output:**

<img width="1277" height="405" alt="image" src="https://github.com/user-attachments/assets/1aaaf683-2450-4c10-9969-19781eec57a0" />


**Question 4**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000
```sql
select * from CUSTOMERS
where salary<2500;
```

**Output:**

<img width="1285" height="531" alt="image" src="https://github.com/user-attachments/assets/cba647b0-ac8d-4725-84d8-126affa3c349" />

**Question 5**
---
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

SALESMAN TABLE

name               type
-----------        ----------
salesman_id  numeric(5)
name             varchar(30)
city                 varchar(15)
commission   decimal(5,2)

ORDERS TABLE

name            type
----------      ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int

```sql
select ord_no, purch_amt, ord_date, customer_id, salesman_id
from ORDERS
where salesman_id in(
    select salesman_id
    from salesman
    where city='New York'
);
```

**Output:**

<img width="1281" height="553" alt="image" src="https://github.com/user-attachments/assets/8be3a71f-97a2-46ee-825c-aa2bfe4a3762" />


**Question 6**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

```sql
select student_name,grade
from GRADES g
where grade=(
    select MIN(grade)
    from GRADES
    where subject=g.subject
);
```

**Output:**

<img width="1279" height="495" alt="image" src="https://github.com/user-attachments/assets/5d4a94f5-47d2-4485-94ea-204d2e39fe05" />


**Question 7**
---
From the following tables write a SQL query to find all orders generated by London-based salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int

```sql
select ord_no, purch_amt, ord_date, customer_id, salesman_id
from ORDERS
where salesman_id in(
    select salesman_id
    from salesman
    where city='London'
);
```

**Output:**

<img width="1279" height="474" alt="image" src="https://github.com/user-attachments/assets/7e394c0b-ad76-44d5-8fcc-d8720e73465e" />


**Question 8**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi and age below 30

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000



```sql
select * from CUSTOMERS
where ADDRESS is 'Delhi' and AGE<30
order by ID;
```

**Output:**

<img width="1283" height="433" alt="image" src="https://github.com/user-attachments/assets/b4a062bc-f92e-4a1d-82af-9741c960edc6" />


**Question 9**
---
From the following tables, write a SQL query to find all orders generated by the salespeople who may work for customers whose id is 3007. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Table Name: orders

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int

```sql
select * from orders
where salesman_id in(
    select salesman_id
    from orders
    where customer_id=3007
);
```

**Output:**

<img width="1276" height="499" alt="image" src="https://github.com/user-attachments/assets/9759c98d-db38-4e36-a0b2-b5bcd0c8f451" />


**Question 10**
---
From the following tables, write a SQL query to find those salespeople who earned the maximum commission. Return ord_no, purch_amt, ord_date, and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int

```sql
select  ord_no, purch_amt, ord_date, salesman_id
from orders
where salesman_id in(
    select salesman_id 
    from salesman
    where commission=(select MAX(commission) from salesman)
);
```

**Output:**

<img width="1274" height="538" alt="image" src="https://github.com/user-attachments/assets/65162625-d588-4089-8a78-5600d1c13e13" />
**Output:**
<img width="1913" height="1081" alt="image" src="https://github.com/user-attachments/assets/7268826a-009a-4d0a-8fdb-7466c8a48a04" />




## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
