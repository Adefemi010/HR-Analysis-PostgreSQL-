# HR-Analysis-PostgreSQL-
In this HR task, I am utilizing SQL to perform a series of data management and analysis tasks involving employee information. The goal is to work with a database that stores detailed records of employees, such as their job positions, salaries, departments, and start dates, while executing queries to derive valuable insights.

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
    );    

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
    ADD CONSTRAINT birth_check CHECK (birth_date < CURRENT_DATE);

    -- Rename the column job_position to position_title
    ALTER TABLE employees
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

# Query 4
    INSERT INTO employees (emp_id, first_name, last_name, position_title, salary, start_date, birth_date, store_id,             department_id, manager_id, end_date)
    VALUES 
    (1, 'Morrie', 'Conaboy', 'CTO', 21268.94, '2005-04-30', '1983-07-10', 1, 1, NULL, NULL),
    (2, 'Miller', 'McQuarter', 'Head of BI', 14614.00, '2019-07-23', '1978-11-09', 1, 1, 1, NULL),
    (3, 'Christalle', 'McKenny', 'Head of Sales', 12587.00, '1999-02-05', '1973-01-09', 2, 3, 1, NULL),
    (4, 'Sumner', 'Seares', 'SQL Analyst', 9515.00, '2006-05-31', '1976-08-03', 2, 1, 6, NULL),
    (5, 'Romain', 'Hacard', 'BI Consultant', 7107.00, '2012-09-24', '1984-07-14', 1, 1, 6, NULL),
    (6, 'Ely', 'Luscombe', 'Team Lead Analytics', 12564.00, '2002-06-12', '1974-08-01', 1, 1, 2, NULL),
    (7, 'Clywd', 'Filyashin', 'Senior SQL Analyst', 10510.00, '2010-04-05', '1989-07-23', 2, 1, 2, NULL),
    (8, 'Christopher', 'Blague', 'SQL Analyst', 9428.00, '2007-09-30', '1990-12-07', 2, 2, 6, NULL),
    (9, 'Roddie', 'Izen', 'Software Engineer', 4937.00, '2019-03-22', '2008-08-30', 1, 4, 6, NULL),
    (10, 'Ammamaria', 'Izhak', 'Customer Support', 2355.00, '2005-03-17', '1974-07-27', 2, 5, 3, '2013-04-14'),
    (11, 'Carlyn', 'Stripp', 'Customer Support', 3060.00, '2013-09-06', '1981-09-05', 1, 5, 3, NULL),
    (12, 'Reuben', 'McRorie', 'Software Engineer', 7119.00, '1995-12-31', '1958-08-15', 1, 5, 6, NULL),
    (13, 'Gates', 'Raison', 'Marketing Specialist', 3910.00, '2013-07-18', '1986-06-24', 1, 3, 3, NULL),
    (14, 'Jordanna', 'Raitt', 'Marketing Specialist', 5844.00, '2011-10-23', '1993-03-16', 2, 3, 3, NULL),
    (15, 'Guendolen', 'Motton', 'BI Consultant', 8330.00, '2011-01-10', '1980-10-22', 2, 3, 6, NULL),
    (16, 'Doria', 'Turbat', 'Senior SQL Analyst', 9278.00, '2010-08-15', '1983-01-11', 1, 1, 6, NULL),
    (17, 'Cort', 'Bewlie', 'Project Manager', 5463.00, '2013-05-26', '1986-10-05', 1, 5, 3, NULL),
    (18, 'Margarita', 'Eaden', 'SQL Analyst', 5977.00, '2014-09-24', '1978-10-08', 2, 1, 6, '2020-03-16'),
    (19, 'Hetty', 'Kingaby', 'SQL Analyst', 7541.00, '2009-08-17', '1999-04-25', 1, 2, 6, NULL),
    (20, 'Lief', 'Robardley', 'SQL Analyst', 8981.00, '2002-10-23', '1971-01-25', 2, 3, 6, '2016-07-01'),
    (21, 'Zaneta', 'Carlozzi', 'Working Student', 1525.00, '2006-08-29', '1995-04-16', 1, 3, 6, '2012-02-19'),
    (22, 'Giana', 'Matz', 'Working Student', 1036.00, '2016-03-18', '1987-09-25', 1, 3, 6, NULL),
    (23, 'Hamil', 'Evershed', 'Web Developer', 3088.00, '2022-02-03', '2012-03-30', 1, 4, 2, NULL),
    (24, 'Lowe', 'Diamant', 'Web Developer', 6418.00, '2018-12-31', '2002-09-07', 1, 4, 2, NULL),
    (25, 'Jack', 'Franklin', 'SQL Analyst', 6771.00, '2013-05-18', '2005-10-04', 1, 2, 2, NULL),
    (26, 'Jessica', 'Brown', 'SQL Analyst', 8566.00, '2003-10-23', '1965-01-29', 1, 1, 2, NULL);
    
# Task 5
Insert the following values into the departments table. department_id :1,2,3,4,5. department: Analytics, Finance, Sales, Website, Back Office. division: IT, Administration, Sales, IT, Administration.

# Query 5
    INSERT INTO departments (department_id, department, division)
    VALUES 
    (1, 'Analytics', 'IT'),
    (2, 'Finance', 'Administration'),
    (3, 'Sales', 'Sales'),
    (4, 'Website', 'IT'),
    (5, 'Backoffice', 'Administration');

 # Task 6  
Jack Franklin gets promoted to 'Senior SQL Analyst' and the salary raises to 7200.
Update the values accordingly.

# Query 6
    UPDATE employees
    SET position_title = 'Senior SQL Analyst', salary = 7200
    WHERE first_name = 'Jack' AND last_name = 'Franklin';

 # Task 7
The responsible people decided to rename the position_title Customer Support to Customer Specialist.
Update the values accordingly.

# Query 7 
    UPDATE employees
    SET position_title = 'Customer Specialist'
    WHERE position_title = 'Customer Support';

# Task 8
All SQL Analysts including Senior SQL Analysts get a raise of 6%.
Upate the salaries accordingly.

# Query 8 
    UPDATE employees
    SET salary = salary * 1.06
    WHERE position_title IN ('SQL Analyst', 'Senior SQL Analyst');

# Task 9
What is the average salary of a SQL Analyst in the company (excluding Senior SQL Analyst)?

# Query 9
    SELECT AVG(salary) AS average_salary
    FROM employees
    WHERE position_title = 'SQL Analyst';

# Task 10
Write a query that adds a column called manager that contains  first_name and last_name (in one column) in the data output.
Secondly, add a column called is_active with 'false' if the employee has left the company already, otherwise the value is 'true'.

# Query 10

    SELECT 
    emp.*,
    CASE WHEN emp.end_date IS NULL THEN 'true'
    ELSE 'false' 
    END as is_active,
    mng.first_name ||' '|| mng.last_name AS manager_name
    FROM employees emp
    LEFT JOIN employees mng	
    ON emp.manager_id=mng.emp_id;

# Task 11
Create a view called v_employees_info from that previous query.

# Query 11
    CREATE VIEW v_employees_info
    AS
    SELECT 
    emp.*,
    CASE WHEN emp.end_date IS NULL THEN 'true'
    ELSE 'false' 
    END as is_active,
    mng.first_name ||' '|| mng.last_name AS manager_name
    FROM employees emp
    LEFT JOIN employees mng
    ON emp.manager_id=mng.emp_id;

# Task 12
Write a query that returns the average salaries for each positions with appropriate roundings.

# Query 12

    SELECT 
    position_title,
    ROUND(AVG(salary), 2) AS average_salary
    FROM 
    employees
    GROUP BY 
    position_title
    ORDER BY 
    average_salary DESC

# Task 13
What is the average salary for a Software Engineer in the company.

# Query 13
    SELECT 
    ROUND(AVG(salary), 2) AS average_salary
    FROM 
    employees
    WHERE 
    job_position = 'Software Engineer';

# Task 14
What is the average salaries per division.

# Query 14
    SELECT 
    d.division,
    ROUND(AVG(e.salary), 2) AS average_salary
    FROM 
    employees e
    JOIN 
    departments d ON e.department_id = d.department_id
    GROUP BY 
    d.division
    ORDER BY 
    average_salary DESC

# Task 15 
Write a query that returns the following:
emp_id,
first_name,
last_name,
position_title,
salary
and a column that returns the average salary for every job_position.
Order the results by the emp_id.


# Query 15 

    SELECT 
    emp_id,
    first_name,
    last_name,
    position_title AS position_title,
    salary,
    ROUND(AVG(salary) OVER (PARTITION BY position_title), 2) AS average_position_salary
    FROM 
    employees
    ORDER BY 
    emp_id;

# Task 16
How many people earn less than there avg_position_salary?

# Query 16
    SELECT
    COUNT(*)
    FROM (
    SELECT 
    emp_id,
    salary,
    ROUND(AVG(salary) OVER(PARTITION BY position_title),2) as avg_pos_sal
    FROM employees) a
    WHERE salary<avg_pos_sal;

# Task 17
Write a query that returns a running total of the salary development by the start_date.

# Query 17
    SELECT 
    emp_id,
    start_date,
    salary,
    SUM(salary) OVER (ORDER BY start_date) AS running_total_salary
    FROM 
    employees
    ORDER BY 
    start_date;


# Task 18
Create the same running total but now also consider the fact that people were leaving the company.

# Query 18
    SELECT 
    start_date,
    SUM(salary) OVER(ORDER BY start_date)
    FROM (
    SELECT 
    emp_id,
    salary,
    start_date
    FROM employees
    UNION 
    SELECT 
    emp_id,
    -salary,
    end_date
    FROM v_employees_info
    WHERE is_active ='false'
    ORDER BY start_date) a;
    
    
 # Task 19
 Write a query that outputs only the top earner per position_title including first_name and position_title and their salary.

# Query 19
    SELECT
    first_name, 
    position_title,
    salary
    FROM employees e1
    WHERE salary = (SELECT MAX(salary)
    			   FROM employees e2
    			   WHERE e1.position_title=e2.position_title);


# Task 20
Add also the average salary per position_title.

# Query 20
    SELECT
    first_name,
    position_title,
    salary,
    (SELECT ROUND(AVG(salary),2) as avg_in_pos FROM employees e3
    WHERE e1.position_title=e3.position_title)
    FROM employees e1
    WHERE salary = (SELECT MAX(salary)
    			   FROM employees e2
    			   WHERE e1.position_title=e2.position_title);

# Task 21
Remove those employees from the output of the previous query that has the same salary as the average of their position_title.
These are the people that are the only ones with their position_title

# Query 21
    SELECT
    first_name,
    position_title,
    salary,
    (SELECT ROUND(AVG(salary),2) as avg_in_pos FROM employees e3
    WHERE e1.position_title=e3.position_title)
    FROM employees e1
    WHERE salary = (SELECT MAX(salary)
    			   FROM employees e2
    			   WHERE e1.position_title=e2.position_title)
    AND salary<>(SELECT ROUND(AVG(salary),2) as avg_in_pos FROM employees e3
    WHERE e1.position_title=e3.position_title)
    
       
# Task 22
Write a query that returns all meaningful aggregations of
sum of salary,
number of employees,
average salary
grouped by all meaningful combinations of
division,
department,
position_title.
Consider the levels of hierarchies in a meaningful way.

# Query 22
    SELECT 
    division,
    department,
    position_title,
    SUM(salary),
    COUNT(*),
    ROUND(AVG(salary),2)
    FROM employees
    NATURAL JOIN departments
    GROUP BY 
    ROLLUP(
    division,
    department,
    position_title
    )
    ORDER BY 1,2,3


# Task 23
Write a query that returns all employees (emp_id) including their position_title, department, their salary, and the rank of that salary partitioned by department.

The highest salary per division should have rank 1.

# Query 23

    SELECT
    emp_id,
    position_title,
    department,
    salary,
    RANK() OVER(PARTITION BY department ORDER BY salary DESC)
    FROM employees
    NATURAL LEFT JOIN departments


# Task 24
Write a query that returns only the top earner of each department including
their emp_id, position_title, department, and their salary.

    SELECT * FROM
    (
    SELECT
    emp_id,
    position_title,
    department,
    salary,
    RANK() OVER(PARTITION BY department ORDER BY salary DESC)
    FROM employees
    NATURAL LEFT JOIN departments) a
    WHERE rank=1


    
    
        
    
