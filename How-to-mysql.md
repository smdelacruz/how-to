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
```
Get top 5; Only MysqlDB supports LIMIT
SELECT * FROM Employee LIMIT 5;

ALL DATABASE supports TOP
SELECT TOP 3 * FROM Employee;
```
