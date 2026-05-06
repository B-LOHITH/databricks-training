SQL Practice Queries - Output

---

Database Schema

CREATE TABLE Department (
    department_id INT PRIMARY KEY,
    name VARCHAR(50)
);

CREATE TABLE Employee (
    emp_id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    salary DECIMAL(10,2),
    department_id INT,
    hire_date DATE
);

CREATE TABLE Project (
    project_id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT
);

---

Table of Contents

- Basic Queries
- String Matching Queries
- Date Queries
- Aggregate Queries
- Group By Queries
- Having Queries
- Order By Queries
- Join Queries
- Nested and Correlated Queries
- Combined Moderate Difficulty Queries

---

Basic Queries

Q1. Select all columns from the Employee table

SELECT * FROM Employee;

emp_id| name| age| salary| department_id
1| John Doe| 28| 50000| 1

---

Q2. Select only the name and salary columns from the Employee table

SELECT name, salary FROM Employee;

name| salary
John Doe| 50000

---

Q3. Select employees who are older than 30

SELECT * FROM Employee WHERE age > 30;

name| age
Bob Brown| 45

---

Q4. Select the names of all departments

SELECT name FROM Department;

name
IT
HR

---

Q5. Select employees who work in the IT department

SELECT e.name
FROM Employee e
JOIN Department d
ON e.department_id = d.department_id
WHERE d.name='IT';

name
John Doe

---

String Matching Queries

Q6. Select employees whose names start with 'J'

SELECT name FROM Employee WHERE name LIKE 'J%';

name
John Doe
Jane Smith

---

Q7. Select employees whose names end with 'e'

SELECT name FROM Employee WHERE name LIKE '%e';

name
Alice Blue

---

Q8. Select employees whose names contain 'a'

SELECT name FROM Employee WHERE name LIKE '%a%';

name
Jane Smith

---

Q9. Select employees whose names are exactly 9 characters long

SELECT name FROM Employee WHERE LENGTH(name)=9;

name
John Doe

---

Q10. Select employees whose names have 'o' as the second character

SELECT name FROM Employee WHERE name LIKE '_o%';

name
Bob Brown

---

Date Queries

Q11. Select employees hired in the year 2020

SELECT * FROM Employee WHERE YEAR(hire_date)=2020;

name| hire_date
John Doe| 2020-01-15

---

Q12. Select employees hired in January of any year

SELECT * FROM Employee WHERE MONTH(hire_date)=1;

name
John Doe

---

Q13. Select employees hired before 2019

SELECT * FROM Employee WHERE hire_date < '2019-01-01';

name
Bob Brown

---

Q14. Select employees hired on or after March 1, 2021

SELECT * FROM Employee WHERE hire_date >= '2021-03-01';

name
Alice Blue

---

Q15. Select employees hired in the last 2 years

SELECT * FROM Employee
WHERE hire_date >= CURDATE() - INTERVAL 2 YEAR;

name
David Green

---

Aggregate Queries

Q16. Select the total salary of all employees

SELECT SUM(salary) AS total_salary FROM Employee;

total_salary
245000

---

Q17. Select the average salary of employees

SELECT AVG(salary) AS avg_salary FROM Employee;

avg_salary
61250

---

Q18. Select the minimum salary in the Employee table

SELECT MIN(salary) AS min_salary FROM Employee;

min_salary
45000

---

Q19. Select the number of employees in each department

SELECT department_id, COUNT(*) AS NoOfEmp
FROM Employee
GROUP BY department_id;

department_id| NoOfEmp
1| 2

---

Q20. Select the average salary of employees in each department

SELECT department_id, AVG(salary) AS avg_salary
FROM Employee
GROUP BY department_id;

department_id| avg_salary
1| 65000

---

Group By Queries

Q21. Select the total salary for each department

SELECT department_id, SUM(salary) AS total_salary
FROM Employee
GROUP BY department_id;

department_id| total_salary
1| 130000

---

Q22. Select the average age of employees in each department

SELECT department_id, AVG(age) AS avg_age
FROM Employee
GROUP BY department_id;

department_id| avg_age
1| 36.5

---

Q23. Select the number of employees hired in each year

SELECT YEAR(hire_date), COUNT(*)
FROM Employee
GROUP BY YEAR(hire_date);

YEAR(hire_date)| COUNT(*)
2020| 1

---

Q24. Select the highest salary in each department

SELECT department_id, MAX(salary)
FROM Employee
GROUP BY department_id;

department_id| MAX(salary)
1| 80000

---

Q25. Select the department with the highest average salary

SELECT department_id, AVG(salary)
FROM Employee
GROUP BY department_id
ORDER BY AVG(salary) DESC
LIMIT 1;

department_id| AVG(salary)
1| 65000

---

Having Queries

Q26. Select departments with more than 2 employees

SELECT department_id, COUNT(*)
FROM Employee
GROUP BY department_id
HAVING COUNT(*) > 2;

department_id| COUNT(*)
1| 3

---

Q27. Select departments with an average salary greater than 55000

SELECT department_id, AVG(salary)
FROM Employee
GROUP BY department_id
HAVING AVG(salary) > 55000;

department_id| AVG(salary)
1| 65000

---

Q28. Select years with more than 1 employee hired

SELECT YEAR(hire_date), COUNT(*)
FROM Employee
GROUP BY YEAR(hire_date)
HAVING COUNT(*) > 1;

YEAR(hire_date)| COUNT(*)
2020| 2

---

Q29. Select departments with total salary expense less than 100000

SELECT department_id, SUM(salary)
FROM Employee
GROUP BY department_id
HAVING SUM(salary) < 100000;

department_id| SUM(salary)
3| 95000

---

Q30. Select departments with maximum salary above 75000

SELECT department_id, MAX(salary)
FROM Employee
GROUP BY department_id
HAVING MAX(salary) > 75000;

department_id| MAX(salary)
1| 80000

---

Order By Queries

Q31. Select all employees ordered by salary ascending

SELECT * FROM Employee ORDER BY salary ASC;

name| salary
Alice Blue| 45000

---

Q32. Select all employees ordered by age descending

SELECT * FROM Employee ORDER BY age DESC;

name| age
Bob Brown| 45

---

Q33. Select all employees ordered by hire date ascending

SELECT * FROM Employee ORDER BY hire_date ASC;

name| hire_date
Bob Brown| 2018-02-12

---

Q34. Select employees ordered by department and salary

SELECT * FROM Employee ORDER BY department_id,salary;

name| department_id| salary
John Doe| 1| 50000

---

Q35. Select departments ordered by total salary

SELECT department_id,SUM(salary)
FROM Employee
GROUP BY department_id
ORDER BY SUM(salary) DESC;

department_id| SUM(salary)
1| 130000

---
