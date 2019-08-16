# What is a database (DB)
1. Collection of related information
2. Can be stored in different ways
3. Amount of information
4. Availability
5. How critical
6. Security

# Database management systems (DBMS)
1. Software that helps users create and maintain a DB
2. Manage large amounts of data
3. Handle security
4. Backups
5. Import/export data
6. Concurrency
7. Interacts with software applications
8. Amazon interacts with DB to interact with data (CRUD)
   1. Create
   2. Read
   3. Update
   4. Delete
9. CRUD are main operations with DB

# Two types of DBs
1. Relational DB (SQL)
   1. One or more tables
   2. Each table has columns and rows
   3. *Unique key* identifies each row
   4. Relational database management systems (RDBMS)
      1. Helps users maintain relational database
      2. mySQL, Oracle, postgreSQL, mariaDB, etc.
   5. Structured query language
      1. Standardized language to interact with RDBMS
      2. Used to perform CRUD and other admin tasks
      3. Can define tables and structures
      4. Code is not always portable 
2. Non-relational (noSQL / not just SQL)
   1. Organize data is anything but a traditional table
   2. Key-value pair
   3. Documents (JSON, XML, etc)
   4. Graphs
      1. Relational nodes
   5. Flexible tables
   6. Non-relational database management systems (NRDBMS)
      1. MongoDB, dynamoDB, apache cassandra, firebase, etc.
   7. Implementation specific
      1. Any non-relational database falls under this category
      2. Not NRDBMS implement their own language for performing CRUD and admin ops
   
# Database queries
1. Request made for specific information
2. Complex structure requires complex queries

# Tables and keys
1. Row: collection of informaton for a single entity
2. Column: collection of information type
3. Primary key: uniquely identify a row
   1. Identification number
   2. Email
4. Surrogate key: no mapping to anything to the real world
5. Natural key: has mapping to anything in the real world; social security number
6. Foreign key: links multiple tables together; stores primary key of another table
7. Composite key: two or more columns need to match to identify a unique row

# Structured query language (SQL)
1. Language used to interact with relational database management system RDBMS
2. Not all RDBMS follow the SQL standard
3. Concepts are the same but implementation varies
4. Hybrid language
   1. 4 languages in 1
   2. Data query language (DQL)
      1. Retrieve information
   3. Data definition language (DDL)
      1. Define schemas
   4. Data control language (DCL)
      1. Controls access
      2. User & permissions management
   5. Data manipulation language (DML)
      1. Insert, update, delete data

# Queries
1. Set of instructions sent to the RDBMS to indicate what information you want it to retrieve for you
2. 
  ```sql
    SELECT employee.name, employee.age
    FROM employee
    WHERE employee.salary > 3000;
  ```

```sql
CREATE TABLE student (
  student_id INT PRIMARY KEY,
  name VARCHAR(20),
  major VARCHAR(20)
  -- PRIMARY KEY(student_id) 
);

DESCRIBE student;

DROP TABLE student;

ALTER TABLE student ADD gpa DECIMAL;

ALTER TABLE student DROP COLUMN gpa;

INSERT INTO student VALUES(
  1,
  "Jack",
  "Biology",
);

INSERT INTO student(student_id, name) VALUES(2, "Kate");
```

```sql
CREATE TABLE student (
  student_id INT UNIQUE NOT NULL,
  name VARCHAR(20) NOT NULL,
  major VARCHAR(20) UNIQUE,
  PRIMARY KEY (student_id)
);
```

```sql
CREATE TABLE student (
  student_id INT UNIQUE NOT NULL,
  name VARCHAR(20) NOT NULL,
  major VARCHAR(20) DEFAULT "Undecided",
  PRIMARY KEY(student_id)
);
```

```sql
CREATE TABLE student(
  student_id INT AUTO_INCREMENT,
  name VARCHAR(20) NOT NULL,
  major VARCHAR(20),
  PRIMARY KEY(student_id)
);
```

```sql
SELECT * FROM student;

UPDATE student
SET major = "Bio"
WHERE major = "Biology";

UPDATE student
SET major = "Biochemistry"
WHERE major = "Bio" OR major = "Chemistry";

UPDATE student
SET name = "Cowman", major = "Undecided"
WHERE student_id = 1;

UPDATE student
SET name = "Deleted", major = "Deleted";

DELETE FROM student
WHERE student_id = 5 AND name = "Tom";
```

```sql
SELECT *
FROM student;

SELECT student.name, student.student_id
FROM student
ORDER BY name DESC;

SELECT student.name
FROM student
ORDER BY student_id ASC;

SELECT *
FROM student
ORDER BY name, student_id DESC;

SELECT * 
FROM student
ORDER BY student_id DESC
LIMIT 2;

SELECT *
FROM student
WHERE student_id <= 3 AND name <> 'Jack';

SELECT *
FROM student
WHERE major IN ('Biology', 'Chemistry') AND student_id > 2;
```

```sql
CREATE TABLE branch(
  branch_id INT PRIMARY KEY,
  branch_name VARCHAR(40),
  mgr_id INT,
  mgr_start_date DATE,
  FOREIGN KEY(mgr_id) 
  REFERENCES employee(emp_id) 
  ON DELETE SET NULL;
)

ALTER TABLE employee
ADD FOREIGN KEY(branch_id)
REFERENCES branch(branch_id)
ON DELETE SET NULL;

CREATE TABLE works_with(
  emp_id INT,
  client_id INT,
  total_sales INT,
  PRIMARY KEY(emp_id, client_id)
  FOREIGN KEY(emp_id) REFERENCES employee(emp_id) ON DELETE CASCADE
  FOREIGN KEY(client_id) REFERENCES client(client_id) ON DELETE CASCADE
);

INSERT INTO employee VALUES(100, 'David', 'Wallace', '1967-11-17', 'M', 250000, NULL, NULL);

INSERT INTO branch VALUES(1, 'Corporate', 100, '2006-02-09');

UPDATE employee
SET branch_id = 1
WHERE emp_id = 100;

SELECT first_name AS forename, last_name AS surname
FROM employee;

SELECT DISTINCT sex
FROM employee;

SELECT DISTINCT branch_id
FROM employee;

SELECT COUNT(emp_id)
FROM employee
WHERE sex = 'F' AND birth_date > '1970-01-01';

SELECT AVG(salary)
FROM employee
WHERE sex = 'M';

SELECT SUM(salary)
FROM employee;

SELECT COUNT(sex), sex
FROM employee
GROUP BY sex;

SELECT SUM(total_sales), total_sales
FROM works_with
GROUP BY emp_id;

SELECT * 
FROM clientclient_name
WHERE client_name LIKE '%LLC';

SELECT *
FROM branch_supplier
WHERE supplier_name LIKE '% Label%';

SELECT *
FROM employee
WHERE birth_data LIKE '____-10%';

SELECT *
FROM client
WHERE client_name LIKE '%school%';

SELECT first_name
FROM employee;

SELECT branch_name
FROM branch;

-- Same number of columns
-- Similar data types
SELECT first_name AS name
FROM employee
UNION
SELECT branch_name
FROM branch;
UNION
SELECT client_name
FROM client;

SELECT client_name, client.branch_id
FROM client
UNION
SELECT supplier_name, branch_suppler.branch_id 
FROM branch_supplier;

SELECT salary
FROM employee
UNION
SELECT total_sales
FROM works_with;

SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee
JOIN branch -- aka inner join
ON employee.emp_id = branch.m/gr_id;

SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee
LEFT JOIN branch -- Gets other employees as well that do not match
--RIGHT JOIN branch Gets other branches as well that do not match
-- FULL OUTER JOIN left join and right join combined GRAB THEM ALL
ON employee.emp_id = branch.mgr_id;

SELECT works_with.emp_id
FROM works_with
WHERE works_with.total_sales > 30000;

SELECT employee.first_name, employee.last_name
FROM employee
WHERE employee.emp_id IN (
  SELECT works_with.emp_id
  FROM works_with
  WHERE works_with.total_sales > 30000;
);

SELECT client.client_name
FROM client
WHERE client.branch_id = (
  SELECT branch.branch_id
  FROM branch
  WHERE branch.mgr_id = 102;
);
```