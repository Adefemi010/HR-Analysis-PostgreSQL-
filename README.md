# HR-Analysis-PostgreSQL-
In this HR task, we are utilizing SQL to perform a series of data management and analysis tasks involving employee information. The goal is to work with a database that stores detailed records of employees, such as their job positions, salaries, departments, and start dates, while executing queries to derive valuable insights.

The task involves multiple steps:

Data Manipulation: Creating and updating employee and department tables to ensure data accuracy, including promotions, salary adjustments, and tracking employees who have left the company.

Data Analysis: Using SQL queries to retrieve meaningful insights, such as identifying top earners in each department, analyzing average salaries, calculating running totals of salaries over time, and determining salary ranks within divisions.

Advanced SQL Techniques: Applying window functions (like RANK() and ROW_NUMBER()), common table expressions (CTEs), and aggregate functions to organize and manipulate data at various levels of detail, reflecting real-world HR management scenarios.

The queries focus on providing the HR department with the ability to manage employee data, monitor salary developments, and produce reports that help in decision-making processes related to promotions, compensation, and workforce organization.

# Task 1.1
In your company there hasn't been a database table with all the employee information yet.
You need to set up the table called employees in the following way:
emp_id, first_name, last_name, job_position, salary, start_date, birth_date, soore_id, department_id, manager_id
There should be NOT NULL constraints for the following columns:
first_name,last_name ,job_position,start_date,birth_date
# Query 1.1

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

