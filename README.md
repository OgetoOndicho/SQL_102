# SQL_102 (PART_1)
This is an SQL learning Project, aimed at bettering my SQL Skills using JOINS and SUB-QUERIES for Data Analytics. This project is divide into 2 Parts. 
Part 1 includes use of JOINS in SQL. Starts first by designing of some Databases, Creating and Updating Tables, Inserting Data into the Tables within the databases, then writing SQL Queries to perform Joins so as analyze and gain insights about the data.
Part 2 includes also designing of database from scratch, creating tables, updating the tables then writing SQL Subqueries for efficient data analysis.

## 1.1 PROJECT OVERVIEW
A recently launched Book Publishing Company called Studio hires a Data Analyst to create a Database for them so as to house records of the company. The Data Analyst is expected to create an exclusive database for the company, to store accurate data on attributes such as newly launched books, their authors, book types and so on. The data analyst is also mandated to continously make changes to the database over a period of time for easier consistency, retrieval and tracking.

## 1.2 PROJECT DELIVERABLES (PART 1)
- Create a database for the Publishing Company.
- Create four tables for the company's main attributes and update records into the tables within the databases.
- Create accurate joins within the tables so as to produce consistence records for easier analysis

## SAMPLE SQL QUERIES TO ANSWER QUESTIONS
- A. Create database for the Company 'Studio' and the authorise its use:
```sql
CREATE DATABASE Publishing_Studio;
USE Publishing_Studio;
```
- B. Create 4 Tables: (Books, Authors, Editors and Translators):
```sql
CREATE TABLE Books(
id INT,
title VARCHAR(30),
type VARCHAR(30),
author_id VARCHAR(10),
editor_id INT,
translator_id INT);
```
```sql
CREATE TABLE Authors (
id INT,
first_name VARCHAR(20),
last_name VARCHAR(20)
);
```
```sql
CREATE TABLE Editors (
id INT,
first_name VARCHAR(20),
last_name VARCHAR(20)
);
```
```sql
CREATE TABLE Translators (
id INT,
first_name VARCHAR(20),
last_name VARCHAR(20)
);
```

- C. Update data into the respective tables

Books;

```sql
INSERT INTO Books VALUES 
(1, 'time to glow up', 'original', '15', '21', NULL),
(2, 'your trip', 'translated', '14', '22', '32'),
(3, 'lovely love', 'original', '11', '24', NULL),
(4, 'dream your life', 'original', '12', '24', NULL),
(5, 'oranges', 'translated', '13', '25', '31'),
(6, 'your high life', 'translated', '11', '22', '33'),
(7, 'applied AI', 'translated', '10', '23', '34'),
(8, 'my last book', 'original', '12', '28', NULL);
```

Authors;

```sql
INSERT INTO Authors VALUES
('11', 'Elon', 'Musk'),
('12', 'Jeff', 'Bezos'),
('13', 'Dan', 'Gucci'),
('14', 'Donald', 'Trump'),
('15', 'Yoo', 'Mama');
```

Editors;

```sql
INSERT INTO Editors VALUES
('21', 'Dan', 'Masembe'),
('22', 'Maek', 'Mali'),
('23', 'John', 'Gotti'),
('24', 'Mana', 'Ryan'),
('25', 'Jack', 'Danils'),
('26', 'Oman', 'Kas'),
('27', 'Matthew', 'Stains');
```

Translators;

```sql
INSERT INTO Translators VALUES
('31', 'Lira', 'Dave'),
('32', 'Ling', 'Huan'),
('33', 'Christian', 'Combs'),
('34', 'Roman', 'Reigns');
```

- D. Write SQL Queries to retrieve data from the Tables created
Ans: We use the SELECT * FROM Name of table Statement to retrieve data using Name of specifiic table for instance Books:
```sql
SELECT * FROM Name_of_Table;
```

- E. Write an SQL Query to Retrieve name of Books with corresponding Authors from the Database
In these cases we use alliases with small cases of the first letter of Table Name for efficient querying. For example, Books as b, Authors as a, Editors as e and Translators as t

```sql
SELECT b.id, b.title, a.first_name, a.last_name
FROM Books b
INNER JOIN Authors a 
ON b.author_id = a.id
ORDER BY b.id;
```
- F. Write a Query to Retrieve name of Books with corresponding Translators:
```sql
SELECT b.id, b.title, b.type, t.first_name, t.last_name
FROM Books b
INNER JOIN Translators t
ON b.translator_id = t.id
ORDER BY b.id;
```
- G. Retrieve id, type, title from Books table matching records with Translators and Authors Table
The AS is used as an Alias to refer to a given column from the Table
We use the ORDER BY Statement for precise ordering of results
```sql
SELECT b.id, b.title, b.type, a.first_name AS Author, t.first_name AS Translator
FROM Books b
LEFT JOIN Authors a  ON b.author_id = a.id
LEFT JOIN Translators t
ON b.translator_id = t.id
ORDER BY b.id;
```
- H. Write Query to Retrieve all records from Editors Table
```sql
SELECT b.id, b.title, e.last_name AS Author
FROM Books b
RIGHT JOIN Editors e
ON b.editor_id = e.id
ORDER BY b.id;
```
- I. Write a Query to Perform a full join on the Books and Editors Table
```sql
SELECT b.id, b.title, b.type, e.last_name as Editor
FROM Books b
JOIN Editors e
ON b.editor_id = e.id
ORDER BY b.id;
```

## CONCLUSION (PART 1)
There are 4 types of SQL JOIN QUERIES used for data analysis.
- In the above cases "FULL JOIN / JOIN" is used to pull all records from tables irregardless whether they match or not.
- The "LEFT JOIN" Pulls all records from the Left Table matching the right table.
- The "RIGHT JOIN" Pulls all reccords from the Right Table matching the Left table.
- The "INNER JOIN" Pulls ONLY matching records from the TWO Tables.

# SQL 102 (PART_2)
The CEO of the Publishing Studio Company, also happens to be the Director of Global Company X that deal with fresh fruit exports. He hires the same data analyst to design a database for his company, analyze data so as to derive some meaningful insights. In this part, we will be exploring use of Sub-Queries in SQL as means of manipulating data.

## PROJECT DELIVERABLES (PART_2)
- Design a database for the Global Company X.
- Design tables for the company's main attributes and update records into the tables within the databases.
- Draw key insights using SQL Sub-Queries to make meaningful insights and analysis

## SAMPLE SQL QUERIES TO ANSWER QUESTIONS
- 1.1. Design database, two tables (employees and departments)for the Global Company X and the authorise its use:
```sql
CREATE DATABASE Global_Company_X;
USE Global_Company_X;
```
- 1.2. Design tables (employees and departments) and insert data
---Employees Table---
```sql
CREATE TABLE employee(
employee_id INT PRIMARY KEY,
first_name VARCHAR(30),
last_name VARCHAR(30),
email VARCHAR(30),
phone_number INT,
hire_date DATE,
Salary DECIMAL(6,2),
Commission_pct DECIMAL(4,2),
Department_id INT,
Manager_id INT,
job_id VARCHAR(30)
);

INSERT INTO employee VALUES
(10, 'Brion', 'Cajio', 'br100@gmail.com', '074567891', '2020-11-22', '100.44', '30.89', '100', '200','A1010'),
(11, 'Jane', 'Tanu', 'janetanu@outlook.com', '0890675432', '2023-11-11', '300.01', '44.44', '101', '201', 'B4040'),
(12, 'Carla', 'Vanui', 'carla101@gmail.com', '067709345', '1990-11-28', '239.45', '21.23', '102', '202', 'C1010'),
(13, 'Big', 'Gotti', 'gotti@gmail.com', '078788900', '1997-06-22', '300.66', '33.33', '104', '203', 'D1234'),
(14, 'Jane', 'Carlos', 'janecarlo12@gmail.com', '0789341111', '1997-10-10', '400.44', '56.45', '105', '204', 'D7098'),
(17, 'Jeanne', 'Nganga', 'jeanne56@outlook.com', '01005432897', '1999-12-29', '500.99', '37.89', '106', '205', 'B1230');
```
---Departments Table---
```sql
CREATE TABLE departments (
department_id INT PRIMARY KEY,
department_name VARCHAR(30),
manager_id INT,
location_id VARCHAR(30)
);

INSERT INTO departments VALUES
(100, 'Security', '404040', 'F404040'),
(101, 'Guests', '303030', 'D303030'),
(120, 'Staff', '5050505', 'G505050'),
(104, 'Marketing', '606060', 'L606060'),
(108, 'Digitization', '909090', 'M909090'),
(106, 'Sales', '707870', '707870');
```

##SQL Sub-Query Questions
- A. Scalar Sub-Query: Retrieve Employee first name with salary > than the Average salary from the table
  
```sql
SELECT first_name
FROM employee
WHERE salary >(SELECT AVG(Salary) FROM employee);
```

- B.TABLESUB-QUERY = Values as a set of Tables

```sql
SELECT first_name, last_name
FROM employee
WHERE department_id IN (SELECT department_id FROM departments);
```

- C. COLUMN SUB-QUERY = Single Column of Values

```sql
SELECT last_name
FROM employee
WHERE department_id IN (SELECT department_id FROM departments WHERE location_id = 'F404040');
```

- D. CORRELATED SUB-QUERY = Depends on the outer query

```sql
SELECT first_name
FROM employee 
WHERE Salary IN (SELECT AVG(Salary) FROM employee WHERE department_id = '100');
```

## CONCLUSION
In conclusion, SQL Sub-Query is a query nested within another query to perform operations that depend on results of another queries. 
There are different types of sub-queries such as:
- Scalar Subquery
- Table Subquery
- Column Subquery
- Correlated Subquery
All these are useful in performing complex SQL Operations.






