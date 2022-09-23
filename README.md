# Interview Questions
Table of Contents
- [Interview Questions](#interview-questions)
- [SQL](#sql)
- [Python](#python)

# SQL
<details>
    <summary>
    Setup DB -     <a href='https://sqliteonline.com/'>Online</a>
    </summary>

    -- Create table
    CREATE TABLE EmployeeInfo(
        EmpId INT,
        EmpFName VARCHAR(50),
        Department VARCHAR(50),
        Salary INT
    )

    -- Insert values
    INSERT INTO EmployeeInfo VALUES(
        1, 'Abram', 'HR', 12000),
        (2, 'Kalin', 'Marketing'), 35000,
        (3, 'Jeetu', 'HR', 18000),
        (4, 'Pinky', 'Sales', 28000)
    
</details>

1. Write a query to retrive the list of Employees working in the same department?
    ``` SQL
    SELECT DISTINCT E1.EmpId, E1.EmpFName, E1.Department 
    FROM EmployeeInfo E1
    INNER JOIN
    EmployeeInfo E2
    ON E1.department = E2.department
    AND E1.EmpId != E2.EmpId
    ```
2. Find the higest and lowest salary without using MIN, MAX, LIMIT, TOP, ROW_NUMBER, RANK, DENSE_RANK?
   ``` SQL
   -- Higest
    SELECT EmpFName, salary 
    From EmployeeInfo E1 
    WHERE 
    0 = (SELECT COUNT(DISTINCT salary)
    FROM EmployeeInfo E2 
    WHERE E2.salary > E1.salary)

    -- Lowest
    SELECT EmpFName, salary 
    From EmployeeInfo E1 
    WHERE 
    0 = (SELECT COUNT(DISTINCT salary)
    FROM EmployeeInfo E2 
    WHERE E2.salary < E1.salary)

    -- Nth
    SELECT EmpFName, salary 
    From EmployeeInfo E1 
    WHERE 
    N-1 = (SELECT COUNT(DISTINCT salary)
    FROM EmployeeInfo E2 
    WHERE E2.salary > E1.salary)
   ```
    Here N is number. Example for 3rd higest salary, it'd be 3-1

3. Find next flight date for user
   <details>
    <summary>
    Setup DB -     <a href='https://sqliteonline.com/'>Online</a>
    </summary>

    -- drop table
    -- DROP TABLE travel;

    -- Create table
    CREATE TABLE travel(
    Name VARCHAR(20),
    Flight_Date date);

    -- Insert values
    INSERT INTO travel VALUES ('Bharat', '2021-09-20');
    INSERT INTO travel VALUES ('Peter', '2021-09-24');
    INSERT INTO travel VALUES ('Bhalu', '2021-09-22');
    INSERT INTO travel VALUES ('Bharat', '2021-09-28');
    INSERT INTO travel VALUES ('Peter', '2021-09-25');

    
</details>

   ```
   -- Without Windows Function
   (SELECT A.NAME, A.FLIGHT_DATE, B.FLIGHT_DATE AS NEW_DATE
    FROM TRAVEL A INNER JOIN TRAVEL B
    ON A.NAME=B.NAME
    AND B.FLIGHT_DATE > A.FLIGHT_DATE
    ORDER BY A.NAME)
    UNION
    SELECT NAME, FLIGHT_DATE, NULL AS NEW_DATE
    FROM TRAVEL
    WHERE NAME IN (
    SELECT NAME FROM TRAVEL
    GROUP BY NAME
    HAVING COUNT(*)=1)

    -- Using Windows Function
    SELECT NAME, FLIGHT_DATE, 
    LEAD(FLIGHT_DATE, 1) OVER(PARTITION BY NAME 
	ORDER BY NAME) AS NEW_DATE
    FROM TRAVEL
   ```

# Python