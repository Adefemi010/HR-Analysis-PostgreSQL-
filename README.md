# HR-Analysis-PostgreSQL-
In this HR task, we are utilizing SQL to perform a series of data management and analysis tasks involving employee information. The goal is to work with a database that stores detailed records of employees, such as their job positions, salaries, departments, and start dates, while executing queries to derive valuable insights.

The task involves multiple steps:

Data Manipulation: Creating and updating employee and department tables to ensure data accuracy, including promotions, salary adjustments, and tracking employees who have left the company.

Data Analysis: Using SQL queries to retrieve meaningful insights, such as identifying top earners in each department, analyzing average salaries, calculating running totals of salaries over time, and determining salary ranks within divisions.

Advanced SQL Techniques: Applying window functions (like RANK() and ROW_NUMBER()), common table expressions (CTEs), and aggregate functions to organize and manipulate data at various levels of detail, reflecting real-world HR management scenarios.

The queries focus on providing the HR department with the ability to manage employee data, monitor salary developments, and produce reports that help in decision-making processes related to promotions, compensation, and workforce organization.

# Task 1
In your company there hasn't been a database table with all the employee information yet.
You need to set up the table called employees in the following way:
emp_id, first_name, last_name, job_position, salary, start_date, birth_date, soore_id, department_id, manager_id.

There should be NOT NULL constraints for the following columns:
first_name,last_name ,job_position,start_date,birth_date

# Query 1

    CREATE TABLE employees (
    emp_id SERIAL PRIMARY KEY,           -- Primary Key, Auto-incremented Integer
    first_name TEXT NOT NULL,            -- First Name, Cannot be NULL
    last_name TEXT NOT NULL,             -- Last Name, Cannot be NULL
    job_position TEXT NOT NULL,          -- Job Position, Cannot be NULL
    salary NUMERIC,                      -- Salary, Numeric Data Type (optional)
     start_date DATE NOT NULL,            -- Start Date, Cannot be NULL
     birth_date DATE NOT NULL,            -- Birth Date, Cannot be NULL
    store_id INTEGER,                    -- Store ID, Integer (optional)
     department_id INTEGER,               -- Department ID, Integer (optional)
     manager_id INTEGER                   -- Manager ID, Integer (optional)
    );

# Task 2
Set up an additional table called departments in the following way: department_id, department, diviion. No column should allow nulls

# Query 2

    CREATE TABLE departments (
        department_id SERIAL PRIMARY KEY,    -- Primary Key, Auto-incremented Integer, Not NULL
        department TEXT NOT NULL,            -- Department Name, Cannot be NULL
        division TEXT NOT NULL               -- Division Name, Cannot be NULL

# Task 3
Alter the employees table in the following way:

- Set the column department_id to not null.

- Add a default value of CURRENT_DATE to the column start_date.

- Add the column end_date with an appropriate data type (one that you think makes sense).

- Add a constraint called birth_check that doesn't allow birth dates that are in the future.

- Rename the column job_position to position_title.

# Query 3
    ALTER TABLE employees
    -- Set the column department_id to NOT NULL
     ALTER COLUMN department_id SET NOT NULL,

    -- Add a default value of CURRENT_DATE to the column start_date
    ALTER COLUMN start_date SET DEFAULT CURRENT_DATE,

    -- Add the column end_date with data type DATE
    ADD COLUMN end_date DATE,

    -- Add a constraint called birth_check to ensure no birth dates in the future
    ADD CONSTRAINT birth_check CHECK (birth_date <= CURRENT_DATE),

    -- Rename the column job_position to position_title
    RENAME COLUMN job_position TO position_title;


# Task 4
Insert the following values into the employees table.
Columns:
1.	(emp_id,first_name,last_name,position_title,salary,start_date,birth_date,store_id,department_id,manager_id,end_date)

Values:
1.	(1,'Morrie','Conaboy','CTO',21268.94,'2005-04-30','1983-07-10',1,1,NULL,NULL),
2.	(2,'Miller','McQuarter','Head of BI',14614.00,'2019-07-23','1978-11-09',1,1,1,NULL),
3.	(3,'Christalle','McKenny','Head of Sales',12587.00,'1999-02-05','1973-01-09',2,3,1,NULL),
4.	(4,'Sumner','Seares','SQL Analyst',9515.00,'2006-05-31','1976-08-03',2,1,6,NULL),
5.	(5,'Romain','Hacard','BI Consultant',7107.00,'2012-09-24','1984-07-14',1,1,6,NULL),
6.	(6,'Ely','Luscombe','Team Lead Analytics',12564.00,'2002-06-12','1974-08-01',1,1,2,NULL),
7.	(7,'Clywd','Filyashin','Senior SQL Analyst',10510.00,'2010-04-05','1989-07-23',2,1,2,NULL),
8.	(8,'Christopher','Blague','SQL Analyst',9428.00,'2007-09-30','1990-12-07',2,2,6,NULL),
9.	(9,'Roddie','Izen','Software Engineer',4937.00,'2019-03-22','2008-08-30',1,4,6,NULL),
10.	(10,'Ammamaria','Izhak','Customer Support',2355.00,'2005-03-17','1974-07-27',2,5,3,2013-04-14),
11.	(11,'Carlyn','Stripp','Customer Support',3060.00,'2013-09-06','1981-09-05',1,5,3,NULL),
12.	(12,'Reuben','McRorie','Software Engineer',7119.00,'1995-12-31','1958-08-15',1,5,6,NULL),
13.	(13,'Gates','Raison','Marketing Specialist',3910.00,'2013-07-18','1986-06-24',1,3,3,NULL),
14.	(14,'Jordanna','Raitt','Marketing Specialist',5844.00,'2011-10-23','1993-03-16',2,3,3,NULL),
15.	(15,'Guendolen','Motton','BI Consultant',8330.00,'2011-01-10','1980-10-22',2,3,6,NULL),
16.	(16,'Doria','Turbat','Senior SQL Analyst',9278.00,'2010-08-15','1983-01-11',1,1,6,NULL),
17.	(17,'Cort','Bewlie','Project Manager',5463.00,'2013-05-26','1986-10-05',1,5,3,NULL),
18.	(18,'Margarita','Eaden','SQL Analyst',5977.00,'2014-09-24','1978-10-08',2,1,6,2020-03-16),
19.	(19,'Hetty','Kingaby','SQL Analyst',7541.00,'2009-08-17','1999-04-25',1,2,6,'NULL'),
20.	(20,'Lief','Robardley','SQL Analyst',8981.00,'2002-10-23','1971-01-25',2,3,6,2016-07-01),
21.	(21,'Zaneta','Carlozzi','Working Student',1525.00,'2006-08-29','1995-04-16',1,3,6,2012-02-19),
22.	(22,'Giana','Matz','Working Student',1036.00,'2016-03-18','1987-09-25',1,3,6,NULL),
23.	(23,'Hamil','Evershed','Web Developper',3088.00,'2022-02-03','2012-03-30',1,4,2,NULL),
24.	(24,'Lowe','Diamant','Web Developper',6418.00,'2018-12-31','2002-09-07',1,4,2,NULL),
25.	(25,'Jack','Franklin','SQL Analyst',6771.00,'2013-05-18','2005-10-04',1,2,2,NULL),
26.	(26,'Jessica','Brown','SQL Analyst',8566.00,'2003-10-23','1965-01-29',1,1,2,NULL)

# Query 3
    

