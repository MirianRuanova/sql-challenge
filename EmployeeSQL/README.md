# sql-challenge
## Relationships
### One-to-One
- #### Each employee has it own salary.
### One-to-many (a data from one table can be repeated to the data from another table)
- #### A sigle department can be shared among multiple employees.Each employee has their own department.
- #### A sigle title can be shared among multiple employees. Each employee has only one title. 
- #### A single title can be shared among multiple employees. 
### Many-to-many relationchips
#### 
## Data Engineeering.
1. #### First, I specicifed the data types, primary keys, foreing keys and other constrains. 
2. #### For the primary keys, it is necessary to verify that the column is unique.
    1.  **departments.csv**: dept_no is the primary key.

    2. **dept_emp.csv**: there is no unique column. dept_no is the foreing key that links with the departments.csv table. emp_no is the foreing key which link with the employees.csv table. 

    3. **dept_manager.csv**: emp_no is the primary key.

    4. **employees.csv**: emp_no is the primary key. emp_title_id is the foreing key that links the employee table with the title table.

    5. **salaries.csv**: emp_no is the foreing key which links with the employees.csv table.

    6. ***title.csv**: title_id is the primary key.
## Data Analysis. 
1. Create a `.sql` file of the query which lists the the employee number, last name, first name, sex, and salary of each employee. Left join on the `emp_no` column for the **employees** and **salaries** tables. [Salary of each employee]()
    ```sql
    SELECT emp_no, first_name, last_name, hire_date, salary
    FROM employees
    LEFT JOIN salaries ON
    salaries.emp_no = employees.emp_no;
    ```
2. Create a `.sql` file of the query which lists the first name, last name, and hire date for the employees who were hired in 1986. Use the wildcar  `%`
    ```sql
    SELECT first_name, last_name, hire_date
    FROM employees
    WHERE hire_date LIKE '1986-%-%';
    ```
3. Create `.sql` file of the query which lists the manager of each department along with their department number, department name, employee number, last name, and first name. Join the **dept_manager** table, **department** table on `dept_no` and then, join the **employees** table on the `emp_no` column
    ```sql
    SELECT 
        departments.dept_no, 
        departments.dept_name, 
        dept_manager.emp_no,
        employees.last_name,
        employees.first_name
    FROM dept_manager
    LEFT JOIN departments ON
     dept_manager.dept_no = departments.dept_no
    LEFT JOIN employees ON
     dept_manager.emp_no = employees.emp_no;
    ```
4. Create `.sql` file of the query which lists the department number for each employee along with that employees employee number, last name, first name, and department name.
    ```sql
    SELECT 
    departments.dept_no,
    departments.dept_name, 
    employees.emp_no, 
    employees.last_name,
    employees.first_name
    FROM employees
    INNER JOIN dept_emp ON employees.emp_no = dept_emp.emp_no
    INNER JOIN departments ON dept_emp.dept_no = departments.dept_no;

    ```
5. Create `.sql` file of the query which lists the first name, last name, and sex of each employee whose first name is Hercules and whose last name begins with the letter B.
    ```sql
    SELECT first_name, last_name, sex
    FROM employees
    WHERE first_name = 'Hercules' AND last_name LIKE 'B%';

    ```
6. Create `.sql` file of the query which lists each employee in the Sales department, including their employee number, last name, and first name.
    ```sql
    SELECT
    employees.emp_no,
    employees.last_name,
    employees.first_name
    FROM
        employees
    INNER JOIN
        dept_emp ON employees.emp_no = dept_emp.emp_no
    INNER JOIN
        departments ON dept_emp.dept_no = departments.dept_no
    WHERE
        departments.dept_name = 'Sales';

    ```
7. Create `.sql` file of the query which lists each employee in the Sales and Development departments, including their employee number, last name, first name, and department name.
    ```sql
    SELECT
    employees.emp_no,
    employees.last_name,
    employees.first_name,
    departments.dept_name
    FROM
        employees
    INNER JOIN
        dept_emp ON employees.emp_no = dept_emp.emp_no
    INNER JOIN
        departments ON dept_emp.dept_no = departments.dept_no
    WHERE
        departments.dept_name IN ('Sales', 'Development');

    ```
8. Create `.sql` file of the query which lists the frequency counts, in descending order, of all the employee last names (that is, how many employees share each last name).
    ```sql
    SELECT last_name, COUNT(*) AS frequency
    FROM employees
    GROUP BY last_name
    ORDER BY frequency DESC;

    ```

