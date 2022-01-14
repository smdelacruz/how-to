# MySql
### Install Mysql
•	On Mac > System Preferences > Click MySql
![SystemPreferences](/images/Picture1.png)
![MysqlServer](/images/Picture2.png)


•	Open terminal: type:
o	mysql --- expect that command is not found
o	echo 'export PATH=/usr/local/mysql/bin:$PATH' >> ~/.bash_profile 
o	Hit Enter
o	~/.bash_profile 
o	Hit Enter to reload
o	mysql --- expectt Access denied for user 'shareenadelacruz'@'localhost' (using password: NO)
o	mysql –u root -p
o	
•	Create database on terminal
o	 create database db1;
Install PopSQL – program to write sql queries 
	Create an account: smdelacruz28@yahoo.com / passwordhere
Once created, open the app (note: the app.popsql is not working for localhost) 
1.	Connect to database: 
a.	Hostname: localhost
b.	Database: db1 (connect to the database created on terminal)
c.	Username: root
d.	Password: myself18
e.	Hit Connect button
Note:  Datatypes
INT
DECIMAL (10, 4) 10 digits, 4 numbers after the decimal
Varchar(100) 100 characters
BLOB
DATE ‘YYYY-MM-DD’
TIMESTAMP ‘YYYY-MM-DD HH:MM:SS’

### BASIC COMMANDS
2.	Create a table: CREATE TABLE student(
student_id INT PRIMARY KEY,
name VARCHAR(20),
major VARCHAR(20)
);
3.	Describe a table: DESCRIBE student;
4.	Delete a  table : DROP TABLE student;
5.	Modify the table: ALTER TABLE student ADD gpa DECIMAL(3,2)
6.	Delete A COLUMN ON TABLE: ALTER TABLE student DROP COLUMN gpa;
7.	Insert data on table:
INSERT INTO student VALUES (1, ‘Jack’,’Biology’);
INSERT INTO student(student_id, name)VALUES (3, ‘Claire);
INSERT INTO student VALUES (4, ‘Jack’,’Biology’);
INSERT INTO student VALUES (5, ‘Mike,Computer Science’);

8.	Create table with contraints:
CREATE TABLE student(
student_id INT PRIMARY KEY,
name VARCHAR(20) NOT NULL,
major VARCHAR(20) UNIQUE
);

### CONSTRAINTS:
•	PRIMARY KEY – Combination of NOT NULL and UNIQUE
•	UNIQUE – no data should be duplicated for this column
•	NOT NULL – cannot be NULL or empty
•	DEFAULT – if it was not specified on INSERT, then the default will be the value

	Example:
	Create a default:
CREATE TABLE student(
student_id INT PRIMARY KEY,
name VARCHAR(20) NOT NULL,
major VARCHAR(20) DEFAULT ‘undecided’
);
RESULT:
INSERT INTO student(student_id, name) VALUES (3, 'Claire');
STUDENTID NAME MAJOR
3	Claire	undecided

•	AUTO-INCREMENT – usually on PRIMARY KEY
CREATE TABLE student(
student_id INT AUTO_INCREMENT,
name VARCHAR(20) ,
major VARCHAR(20),
PRIMARY KEY(student_id)
);

Result:
INSERT INTO student(name, major) VALUES ('Kate','Sociology');
INSERT INTO student(name) VALUES ('Claire');
STUDENTID NAME MAJOR
1	Kate	Sociology
2	Claire	



### UPDATE AND DELETE
-	Update data of students with major of Biology to Bio
UPDATE student
SET major = ‘Bio’
WHERE major = ‘Biology’;

-	Update data of students when condition is met

1	Kate	Sociology
2	Claire	
3	MIKE	Bio
4	Jack	Computer Science
5	Mike	Computer Science
UPDATE student
SET major = 'Computer Science'
WHERE major = 'Biology' OR major = "Sociology";

1	Kate	Computer Science
2	Claire	
3	MIKE	Computer Science
4	Jack	Computer Science
5	Mike	Computer Science

UPDATE student
SET name=”Tom, major = ‘Bio’
WHERE student_id=1;
1	Tom	Bio
2	Claire	
3	MIKE	Computer Science
4	Jack	Computer Science
5	Mike	Computer Science

-	UPDATE all columns:
UPDATE student
SET major = ‘Bio’;
1	Tom	Bio
2	Claire	Bio
3	MIKE	Bio
4	Jack	Bio
5	Mike	Bio



DELETE ALL COLUMNS IN STUDENT

ALL – 
DELETE FROM student;
MORE SPECIFIC 
	DELETE FROM student
WHERE student_id = 5;



### Basic Query
SELECT * FROM student_table;

SELECT * FROM student_table
ORDER BY : default = DESC

10	Tom	Computer Science
8	MIKE	Biology
6	Kate	Sociology
9	Jack	Biology
7	Claire	 



/*Query ORDER BY major first then if there are 2+ majors, order by student_id*/
select * from student
ORDER BY major, student_id;
7	Claire	
8	MIKE	Biology
9	Jack	Biology
10	Tom	Computer Science
6	Kate	Sociology


Comparison Operator
 < , > , <= , >= , = , <> , AND , OR


/*Query using IN*/
SELECT * 
FROM student
WHERE major IN ('Biology', 'Sociology');
6	Kate	Sociology
8	MIKE	Biology
9	Jack	Biology

/*Query using IN*/
SELECT * 
FROM student
WHERE major IN ('Biology', 'Sociology') AND student_id > 7;
8	MIKE	Biology
9	Jack	Biology


Create a Company Database
Database: https://www.mikedane.com/databases/sql/creating-company-database/
![CompanyDB](/images/COMPANYDB.png)
LIMIT
```
Get top 5; Only MysqlDB supports LIMIT
SELECT * FROM Employee LIMIT 5;

ALL DATABASE supports TOP
SELECT TOP 3 * FROM Employee;
```

DISTINCT

```
SELECT DISTINCT emp_id FROM employee;
```

### FUNCTIONS
-- Find the number of employee

COUNT
```
SELECT COUNT(*) FROM employee; #9
SELECT COUNT(super_id) FROM employee; #9
SELECT COUNT(emp_id) FROM employee
WHERE sex='F' AND  birth_day > '1970-01-01';
```

-- Find the sum of all employee salaries

SUM
```
SELECT SUM(salary) FROM employee;
```

-- Find the average of all employee salaries

AVG
```
SELECT AVG(salary) FROM employee;
SELECT AVG(salary) FROM employee WHERE sex='M';
```


-- Find out how many females and males

GROUP BY
```
SELECT COUNT(sex), sex FROM employee GROUP BY  sex;
SELECT SUM(total_sales), emp_id FROM works_with GROUP BY emp_id;
SELECT SUM(total_sales), client_id FROM works_with GROUP BY client_id;
```


### WILDCARDS
% = ANY # CHARACTERS

_ = ONE CHARACTER

-- Find any clients who are in LLC

LIKE
```
SELECT client_id FROM client where client_name LIKE '%LLC'; #END AT LLC 
SELECT * FROM BRANCH_SUPPLIER where supplier_name LIKE '%LABEL%';


SELECT * FROM employee where birth_day LIKE '____-10%'; #Find employee which has birthdate on October(10), YEAR is 4-digit so 4 underscore because we know the format of the date, 
```


UNION

1. Should have the same number of columns, 1 column on 1 table and 1 column on another
2. They should have the same datatypes
```
SELECT first_name from employee;
# first_name
David
Jan
Michael

SELECT branch_name from branch;
# branch_name
Corporate
Scranton
Stamford

SELECT first_name from employee UNION
SELECT branch_name from branch;
# first_name
David
Jan
Michael
Corporate
Scranton
Stamford

SELECT first_name from employee UNION
SELECT branch_name from branch UNION
SELECT client_name from client;

# first_name
David
Jan
Michael
Corporate
Scranton
Stamford
FedEx
John Daly Law, LLC
Scranton Whitepages
```
JOINS

Combining tables based on RELATED columns
```
-- JOINS
-- INNER JOIN - only when there is a match on both tables
-- Find all branches and the name of the managers
select b.branch_id, B.branch_name, CONCAT_WS(' ', e.first_name, e.last_name) as Managers 
FROM employee as e 
JOIN branch as b 
ON b.mgr_id = e.emp_id;

#branch_id, branch_name, Managers 
1	Corporate	David Wallace
2	Scranton	Michael Scott
3	Stamford	Josh Porter

-- LEFT JOIN - since employee table will join the branch table (employee -> branch), employee is on the left, it will display all data inside employee.

select b.branch_id, B.branch_name, CONCAT_WS(' ', e.first_name, e.last_name) as Managers 
FROM employee as e 
LEFT JOIN branch as b 
ON b.mgr_id = e.emp_id;
#branch_id, branch_name, Managers 
1	Corporate	David Wallace
NULL NULL		Jan Levinson
2	Scranton	Michael Scott
NULL NULL		Angela Martin
NULL NULL		Kelly Kapoor
NULL NULL		Stanley Hudson
3	Stamford	Josh Porter
.... more


-- RIGHT JOIN - since employee table will join the branch table (employee -> branch), branch is on the right, it will display all data inside branch table.
#branch_id, branch_name, Managers 
1	Corporate	David Wallace
2	Scranton	Michael Scott
3	Stamford	Josh Porter
4	Buffalo	    NULL
```

### NESTED QUERY
```
-- Find names of all employees who have sold over 30,000 to single client
-- my solution
Select DISTINct e.first_name, e.last_name
from employee as e 
JOIN works_with as w 
on total_sales > 30000 and w.emp_id = e.emp_id;
-- tutorial solution
SELECT e.first_name, e.last_name
FROM employee as e
WHERE e.emp_id IN (
    SELECT w.emp_id
    FROM works_with as w
    WHERE w.total_sales > 30000
);


--Find all clients who are handled by the branch that Michael Scott manages, Assume you know Michales ID
-- my solution
Select c.client_name 
FROM client as c
WHERE c.branch_id = (
    SELECT b.branch_id
    FROM branch as b
    WHERE b.mgr_id = 102
	LIMIT 1
);

-- Note: Its always good practice to use LIMIT 1 if where statement uses "="
```


### ON DELETE
Deleting data when there are foreign keys associated to them
```
-- ON DELETE SET NULL - if you delete a row, the associated data will be set to NULL.
					- use this if the connection is just a foreign key in the table
Delete an employee 102 on employee table
#employee table
100	David	Wallace	1967-11-17	M	250000		1
101	Jan	Levinson	1961-05-11	F	110000	100	1
102	Michael	Scott	1964-03-15	M	75000	100	2
...
# branch table
1	Corporate	100	2006-02-09
2	Scranton	102	1992-04-06
3	Stamford	106	1998-02-13
4	Buffalo		NULL	NULL

DELETE FROM employee WHERE emp_id = 102;

# branch table after delete employee 102
1	Corporate	100	2006-02-09
2	Scranton	NULL 1992-04-06
3	Stamford	106	1998-02-13
4	Buffalo		NULL	NULL

-- ON DELETE CASCADE - if you delete a row, the associated data on another table will be deleted as well. 
					- use this if the data is also act as primary key like branch_supplier
Sample:
CREATE TABLE branch_supplier (
  branch_id INT,
  supplier_name VARCHAR(40),
  supply_type VARCHAR(40),
  PRIMARY KEY(branch_id, supplier_name),
  FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE CASCADE
);

when branch_id is deleted from branch table, all its data on branch_supplier table will also be deleted. 
# branch_supplier
	2	Hammer Mill	Paper
	2	J.T. Forms & Labels	Custom Forms
	2	Uni-ball	Writing Utensils
	3	Hammer Mill	Paper
	3	Patriot Paper	Paper
	3	Stamford Lables	Custom Forms
	3	Uni-ball	Writing Utensils

DELETE FROM branch_supplier WHERE branch_id = 2;

# branch_supplier
	3	Hammer Mill	Paper
	3	Patriot Paper	Paper
	3	Stamford Lables	Custom Forms
	3	Uni-ball	Writing Utensils

```
