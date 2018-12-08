# Week One Assignments
Figure out the appropiate sql queries for the following operation on the hr dataset and add your answers. For your first week you will be writing queries to query the hr database. The data and the structre of the database are present in the Data floder of this repo. 

## Basic Select
- Write a query to display the names (first_name, last_name) using alias name “First Name", "Last Name".

SELECT FIRST_NAME AS "First Name", LAST_NAME AS "Last Name" 
	FROM employees


- Write a query to get unique department ID from employee table.

SELECT DEPARTMENT_ID FROM employees GROUP BY DEPARTMENT_ID


- Write a query to get all employee details from the employee table order by first name, descending.

SELECT * FROM employees ORDER BY FIRST_NAME  DESC

- Write a query to get the names (first_name, last_name), salary, PF of all the employees (PF is calculated as 15% of salary).

SELECT FIRST_NAME AS "First Name", LAST_NAME AS "Last Name", SALARY, ROUND(SALARY*.15, 2) AS "PF"
	FROM employees

- Write a query to get the employee ID, names (first_name, last_name), salary in ascending order of salary.

SELECT EMPLOYEE_ID, FIRST_NAME AS "First Name", LAST_NAME AS "Last Name", SALARY
	FROM employees
ORDER BY SALARY ASC


- Write a query to get the total salaries payable to employees.


SELECT SUM(SALARY)
	FROM employees


- Write a query to get the maximum and minimum salary from employees table.


SELECT MAX(SALARY), MIN(SALARY)
	FROM employees


- Write a query to get the average salary and number of employees in the employees table.

SELECT ROUND(SUM(SALARY)/ COUNT(EMPLOYEE_ID),2) AS "Average Salary", COUNT(EMPLOYEE_ID) AS "Total Employees"
	FROM employees



- Write a query to get the number of employees working with the company.

SELECT COUNT(EMPLOYEE_ID) AS "Total Employees"
	FROM employees



- Write a query to get the number of jobs available in the employees table.

SELECT COUNT(DISTINCT JOB_ID)
	FROM employees



- Write a query get all first name from employees table in upper case.

SELECT UPPER (FIRST_NAME)
	FROM employees


- Write a query to get the first 3 characters of first name from employees table.

SELECT LEFT(FIRST_NAME, 3)
	FROM employees


- Write a query to get the names (for example Ellen Abel, Sundar Ande etc.) of all the employees from employees table.

SELECT CONCAT(FIRST_NAME, " ", LAST_NAME)
	FROM employees


- Write a query to get first name from employees table after removing white spaces from both side.

SELECT LTRIM(RTRIM(FIRST_NAME))
	FROM employees


- Write a query to get the length of the employee names (first_name, last_name) from employees table.

SELECT LENGTH(FIRST_NAME), LENGTH(LAST_NAME)
	FROM employees


- Write a query to check if the first_name fields of the employees table contains numbers.

SELECT FIRST_NAME FROM employees 
WHERE FIRST_NAME LIKE '%[0-9]%'


- Write a query to select first 10 records from a table.

SELECT * FROM employees
LIMIT 10


- Write a query to get monthly salary (round 2 decimal places) of each and every employee.
Note : Assume the salary field provides the 'annual salary' information.

SELECT EMPLOYEE_ID, ROUND(SALARY/12,2)
	FROM employees


## Restriction and Sorting

- Write a query to display the name (first_name, last_name) and salary for all employees whose salary is not in the range $10,000 through $15,000.

SELECT FIRST_NAME, LAST_NAME, SALARY 
FROM employees 
WHERE SALARY < 10000 OR SALARY > 15000


- Write a query to display the name (first_name, last_name) and department ID of all employees in departments 30 or 100 in ascending order.


SELECT FIRST_NAME, LAST_NAME, DEPARTMENT_ID 
FROM employees 
WHERE DEPARTMENT_ID IN ('30', '100')


- Write a query to display the name (first_name, last_name) and salary for all employees whose salary is not in the range $10,000 through $15,000 and are in department 30 or 100.

SELECT FIRST_NAME, LAST_NAME, SALARY
FROM employees 
WHERE DEPARTMENT_ID IN ('30', '100') 
AND SALARY NOT BETWEEN 10000 AND 15000



- Write a query to display the name (first_name, last_name) and hire date for all employees who were hired in 1987.

SELECT FIRST_NAME, LAST_NAME, HIRE_DATE 
FROM employees
WHERE YEAR(HIRE_DATE) = 1987



- Write a query to display the first_name of all employees who have both "b" and "c" in their first name.

SELECT FIRST_NAME
FROM employees
WHERE FIRST_NAME LIKE '%b%' AND 
FIRST_NAME LIKE '%c%'


- Write a query to display the last name, job, and salary for all employees whose job is that of a Programmer or a Shipping Clerk, and whose salary is not equal to $4,500, $10,000, or $15,000.

SELECT employees.FIRST_NAME, jobs.JOB_TITLE, employees.SALARY  FROM employees
INNER JOIN jobs ON employees.JOB_ID=jobs.JOB_ID
WHERE JOB_TITLE IN ('Programmer', 'Shipping Clerk') AND 
SALARY NOT IN (4500, 10000, 15000)




- Write a query to display the last name of employees whose names have exactly 6 characters.

SELECT LAST_NAME FROM employees
WHERE LENGTH(FIRST_NAME) = 6

- Write a query to display the last name of employees having 'e' as the third character.


SELECT LAST_NAME FROM employees
WHERE SUBSTRING(LAST_NAME,3,1) = 'e'



- Write a query to display the jobs/designations available in the employees table.


SELECT DISTINCT (employees.JOB_ID), jobs.JOB_TITLE FROM employees
INNER JOIN jobs ON employees.JOB_ID=jobs.JOB_ID



- Write a query to display the name (first_name, last_name), salary and PF (15% of salary) of all employees.


SELECT CONCAT(FIRST_NAME, " ", LAST_NAME) AS "Full Name", SALARY, ROUND(SALARY*.15, 2) AS "PF"
	FROM employees


- Write a query to select all record from employees where last name in 'BLAKE', 'SCOTT', 'KING' and 'FORD'.


SELECT * FROM employees
WHERE LAST_NAME IN ('BLAKE', 'SCOTT', 'KING', 'FORD')


## Aggregate and Group By

- Write a query to list the number of jobs available in the employees table.


SELECT JOB_ID, COUNT(JOB_ID) FROM employees
GROUP BY JOB_ID



- Write a query to get the total salaries payable to employees.


SELECT SUM(SALARY) FROM employees



- Write a query to get the minimum salary from employees table.


SELECT MIN(SALARY) FROM employees



- Write a query to get the maximum salary of an employee working as a Programmer.


SELECT MAX(employees.SALARY) FROM employees
INNER JOIN jobs ON employees.JOB_ID=jobs.JOB_ID
WHERE jobs.JOB_TITLE = 'Programmer'



- Write a query to get the average salary and number of employees working the department 90.


SELECT ROUND(AVG(SALARY),2), ROUND(SUM(SALARY)/ COUNT(EMPLOYEE_ID),2), COUNT(EMPLOYEE_ID) FROM employees
WHERE DEPARTMENT_ID = 90



- Write a query to get the highest, lowest, sum, and average salary of all employees.


SELECT MAX(SALARY), MIN(SALARY), SUM(SALARY), ROUND(AVG(SALARY),2)  FROM employees



- Write a query to get the number of employees with the same job.


SELECT JOB_ID, COUNT(JOB_ID) FROM employees
GROUP BY JOB_ID



- Write a query to get the difference between the highest and lowest salaries.


SELECT MAX(SALARY) - MIN(SALARY) FROM employees




- Write a query to find the manager ID and the salary of the lowest-paid employee for that manager.


SELECT MANAGER_ID, SALARY FROM employees x
WHERE SALARY <= ALL (SELECT SALARY FROM employees y 
                     WHERE y.MANAGER_ID=x.MANAGER_ID 
                     AND MANAGER_ID>0)



- Write a query to get the department ID and the total salary payable in each department.


SELECT DEPARTMENT_ID, SUM(SALARY) FROM employees
GROUP BY DEPARTMENT_ID



- Write a query to get the average salary for each job ID excluding programmer.


SELECT employees.JOB_ID, ROUND(AVG(employees.SALARY),2) FROM employees
INNER JOIN jobs ON employees.JOB_ID=jobs.JOB_ID
WHERE jobs.JOB_TITLE <> 'Programmer'
GROUP BY employees.JOB_ID



- Write a query to get the total salary, maximum, minimum, average salary of employees (job ID wise), for department ID 90 only.


SELECT MAX(SALARY), MIN(SALARY), SUM(SALARY), ROUND(AVG(SALARY),2)  FROM employees
WHERE DEPARTMENT_ID = 90



- Write a query to get the job ID and maximum salary of the employees where maximum salary is greater than or equal to $4000.

SELECT JOB_ID, MAX(SALARY) FROM employees
WHERE SALARY >= 4000
GROUP BY JOB_ID


- Write a query to get the average salary for all departments employing more than 10 employees.

SELECT DEPARTMENT_ID, AVG(SALARY) FROM employees
GROUP BY DEPARTMENT_ID
HAVING COUNT(EMPLOYEE_ID)>10





## Subqueries

- Write a query to find the name (first_name, last_name) and the salary of the employees who have a higher salary than the employee whose last_name='Bull'.

SELECT FIRST_NAME, LAST_NAME, SALARY FROM employees
WHERE SALARY > ALL (SELECT SALARY FROM employees WHERE LAST_NAME = 'Bull')



- Write a query to find the name (first_name, last_name) of all employees who works in the IT department.

SELECT employees.FIRST_NAME, employees.LAST_NAME, departments.DEPARTMENT_NAME FROM employees
INNER JOIN departments ON employees.DEPARTMENT_ID=departments.DEPARTMENT_ID
WHERE  departments.DEPARTMENT_NAME = 'IT'



- Write a query to find the name (first_name, last_name) of the employees who have a manager and worked in a USA based department.
Hint : Write single-row and multiple-row subqueries




- Write a query to find the name (first_name, last_name) of the employees who are managers.






- Write a query to find the name (first_name, last_name), and salary of the employees whose salary is greater than the average salary.






- Write a query to find the name (first_name, last_name), and salary of the employees whose salary is equal to the minimum salary for their job grade.






- Write a query to find the name (first_name, last_name), and salary of the employees who earns more than the average salary and works in any of the IT departments.






- Write a query to find the name (first_name, last_name), and salary of the employees who earns more than the earning of Mr. Bell.





- Write a query to find the name (first_name, last_name), and salary of the employees who earn the same salary as the minimum salary for all departments.





- Write a query to find the name (first_name, last_name), and salary of the employees whose salary is greater than the average salary of all departments.





- Write a query to find the name (first_name, last_name) and salary of the employees who earn a salary that is higher than the salary of all the Shipping Clerk (JOB_ID = 'SH_CLERK'). Sort the results of the salary of the lowest to highest.





- Write a query to find the name (first_name, last_name) of the employees who are not supervisors.





- Write a query to display the employee ID, first name, last name, and department names of all employees.






- Write a query to display the employee ID, first name, last name, salary of all employees whose salary is above average for their departments.






- Write a query to fetch even numbered records from employees table.





- Write a query to find the 5th maximum salary in the employees table.





- Write a query to find the 4th minimum salary in the employees table. 





- Write a query to select last 10 records from a table.





- Write a query to list the department ID and name of all the departments where no employee is working.





- Write a query to get 3 maximum salaries.





- Write a query to get 3 minimum salaries.





- Write a query to get nth max salaries of employees.


## JOINS

- Write a query to find the addresses (location_id, street_address, city, state_province, country_name) of all the departments.
Hint : Use NATURAL JOIN.




- Write a query to find the name (first_name, last name), department ID and name of all the employees. 




- Write a query to find the name (first_name, last_name), job, department ID and name of the employees who works in London.




- Write a query to find the employee id, name (last_name) along with their manager_id and name (last_name).





- Write a query to find the name (first_name, last_name) and hire date of the employees who was hired after 'Jones'.




- Write a query to get the department name and number of employees in the department.




- Write a query to find the employee ID, job title, number of days between ending date and starting date for all jobs in department 90.




- Write a query to display the department ID and name and first name of manager.




- Write a query to display the department name, manager name, and city.




- Write a query to display the job title and average salary of employees.




- Write a query to display job title, employee name, and the difference between salary of the employee and minimum salary for the job.





- Write a query to display the job history that were done by any employee who is currently drawing more than 10000 of salary.




- Write a query to display department name, name (first_name, last_name), hire date, salary of the manager for all managers whose experience is more than 15 years.





