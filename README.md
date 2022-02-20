# Data-Science-Interview-Questions
TOC
- [Data-Science-Interview-Questions](#data-science-interview-questions)
- [SQL](#sql)
- [Python](#python)

# SQL
1. Write a query to retrive the list of Employees working in the same department?
    ```
    SELECT DISTINCT E1.EmpId, E1.EmpFName, E1.Department 
    FROM EmployeeInfo E1
    INNER JOIN
    EmployeeInfo E2
    ON E1.department = E2.department
    AND E1.EmpId != E2.EmpId
    ```
2. Find the higest and lowest salary without using MIN, MAX, LIMIT, TOP, ROW_NUMBER, RANK, DENSE_RANK?
   ```
   -- Higest
    SELECT name,salary 
    From EmpSalary E1 
    WHERE 
    0 = (SELECT COUNT(DISTINCT salary)
    FROM  E2 
    WHERE E2.salary > E1.salary)

    -- Lowest
    SELECT name,salary 
    From EmpSalary E1 
    WHERE 
    0 = (SELECT COUNT(DISTINCT salary)
    FROM  E2 
    WHERE E2.salary < E1.salary)

    -- Nth
    SELECT name,salary 
    From EmpSalary E1 
    WHERE 
    N-1 = (SELECT COUNT(DISTINCT salary)
    FROM  E2 
    WHERE E2.salary > E1.salary)
   ```
    Here N is number. Example for 3rd higest salary, it'd be 3-1

# Python