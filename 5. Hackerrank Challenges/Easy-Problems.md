# Easy-Problems

1. **Revising the Select Query I**

   ​	

   ```sql
   SELECT * FROM CITY
   WHERE CountryCode = 'USA'
   AND POPULATION > 100000;
   ```

2. **Revising the Select Query II**

   ```sql
   SELECT NAME FROM CITY
   WHERE COUNTRYCODE = 'USA'
   AND POPULATION > 120000;
   ```

3. **Select All**

   ```sql
   SELECT * FROM CITY
   ```

4. **Select By ID**

   ```sql
   SELECT * FROM CITY WHERE ID = 1661;
   ```

5. **Japanese Cities' Attributes**

   ```sql
   SELECT * FROM CITY
   WHERE COUNTRYCODE = 'JPN';
   ```

6. **Japanese Cities' Names**

   ```sql
   SELECT NAME FROM CITY
   WHERE COUNTRYCODE = 'JPN';
   ```

7. **Weather Observation Station 1**

   ```sql
   SELECT CITY,STATE FROM STATION;
   ```

8. **Weather Observation Station 3**

   ```sql
   SELECT DISTINCT CITY FROM STATION
   WHERE MOD(ID,2) = 0;
   ```

9. **Weather Observation Station 4**

   ```sql
   SELECT COUNT(CITY) - COUNT(DISTINCT CITY) FROM STATION; 
   ```

10. **Weather Observation Station 5**

    ```sql
    select city, length(city) from station
    order by length(city),city asc
    limit 1;
    select city, length(city) from station
    order by length(city) desc
    limit 1;
    ```

11. **Weather Observation Station 6**

    ```sql
    SELECT DISTINCT CITY FROM STATION
    WHERE SUBSTRING(CITY,1,1) IN ('a','e','i','o','u');
    ```

12. **Weather Observation Station 7**

    ```sql
    SELECT DISTINCT CITY FROM STATION
    WHERE SUBSTRING(CITY,LEN(CITY),1) IN ('a','e','i','o','u');
    ```

13. **Weather Observation Station 8**

    ```sql
    SELECT DISTINCT CITY FROM 
    STATION WHERE SUBSTRING(CITY,LEN(CITY),1) IN ('a','e','i','o','u')
    AND 
    SUBSTRING(CITY,1,1) IN ('a','e','i','o','u');
    ```

14. **Weather Observation Station 9**

    ```sql
    SELECT DISTINCT CITY FROM STATION
    WHERE SUBSTRING(CITY,1,1) NOT IN ('a','e','i','o','u');
    ```

15. **Weather Observation Station 10**

    ```sql
    SELECT DISTINCT CITY FROM STATION
    WHERE SUBSTRING(CITY,LEN(CITY),1) NOT IN ('a','e','i','o','u');
    ```

16. **Weather Observation Station 11**

    ```sql
    SELECT DISTINCT CITY FROM STATION 
    WHERE SUBSTRING(CITY,1,1) NOT IN ('a','e','i','o','u')
    OR SUBSTRING(CITY,LEN(CITY),1) NOT IN ('a','e','i','o','u');
    ```

17. **Weather Observation Station 12**

    ```sql
    SELECT DISTINCT CITY FROM STATION 
    WHERE SUBSTRING(CITY,1,1) NOT IN ('a','e','i','o','u')
    AND SUBSTRING(CITY,LEN(CITY),1) NOT IN ('a','e','i','o','u');
    ```

18. **Higher Than 75 Marks**

    ```sql
    SELECT NAME FROM STUDENTS
    WHERE MARKS > 75
    ORDER BY SUBSTRING(NAME,LEN(NAME)-2,3),ID ASC;
    ```

19. **Employee Names**

    ```sql
    SELECT NAME FROM Employee
    ORDER BY NAME;
    ```

20. **Employee Salaries**

    ```sql
    SELECT NAME FROM EMPLOYEE
    WHERE SALARY > 2000 AND MONTHS < 10
    ORDER BY employee_id ASC;
    ```

21. **Type of Triangle**

    ```sql
    SELECT CASE             
                WHEN A + B > C AND B + C > A AND A + C > B THEN
                    CASE 
                        WHEN A = B AND B = C THEN 'Equilateral'
                        WHEN A = B OR B = C OR A = C THEN 'Isosceles'
                        ELSE 'Scalene'
                    END
                ELSE 'Not A Triangle'
            END
    FROM TRIANGLES;
    ```

22. **Revising Aggregations - The Count Function**

    ```sql
    SELECT COUNT(*) FROM CITY
    WHERE POPULATION > 100000;
    ```

23. **Revising Aggregations - The Sum Function**

    ```sql
    SELECT SUM(POPULATION) FROM CITY
    WHERE DISTRICT = 'California';
    ```

24. **Revising Aggregations - Averages**

    ```sql
    SELECT AVG(POPULATION) FROM CITY
    WHERE DISTRICT = 'California';
    ```

25. **Average Population**

    ```sql
    SELECT ROUND(AVG(POPULATION)) FROM CITY;
    ```

26. **Japan Population**

    ```sql
    SELECT SUM(POPULATION) FROM CITY
    WHERE COUNTRYCODE = 'JPN';
    ```

27. **Population Density Difference**

    ```sql
    SELECT MAX(POPULATION) - MIN(POPULATION)
    FROM CITY;
    ```

28. **The Blunder**

    ```sql
    SELECT CEIL(AVG(Salary)-AVG(REPLACE(Salary,'0',''))) FROM EMPLOYEES;
    ```

29. **Top Earners**

    ```sql
    SELECT TOP 1 salary * months AS earnings, COUNT(*)
    FROM Employee
    GROUP BY salary * months
    ORDER BY salary * months DESC;
    ```

30. **Weather Observation Station 2**

    ```sql
    SELECT FORMAT(ROUND(SUM(LAT_N),2),'#.00'), FORMAT(ROUND(SUM(LONG_W),2),'#.00')
    FROM STATION;
    ```

31. **Weather Observation Station 13**

    ```sql
    SELECT ROUND(SUM(Lat_N), 4)
    FROM STATION
    WHERE Lat_N > 38.7880 AND Lat_N < 137.2345;
    ```

32. **Weather Observation Station 14**

    ```sql
    SELECT ROUND(MAX(LAT_N),4) FROM STATION
    WHERE LAT_N < 137.2345;s
    ```

33. **Weather Observation Station 15**

    ```sql
    SELECT ROUND(LONG_W,4) FROM STATION
    WHERE LAT_N = (SELECT MAX(LAT_N) FROM STATION WHERE LAT_N < 137.2345);
    ```

34. **Weather Observation Station 16**

    ```sql
    SELECT ROUND(MIN(LAT_N),4) FROM STATION 
    WHERE LAT_N > 38.7780;
    ```

35. **Weather Observation Station 17**

    ```sql
    SELECT ROUND(LONG_W,4) FROM STATION 
    WHERE LAT_N = (SELECT MIN(LAT_N) FROM STATION WHERE LAT_N > 38.770);
    ```

36. **Population Census**

    ```sql
    SELECT SUM(CITY.POPULATION)
    FROM CITY INNER JOIN COUNTRY ON CITY.COUNTRYCODE = COUNTRY.CODE
    WHERE COUNTRY.CONTINENT = 'Asia';
    ```

37. **African Cities**

    ```sql
    SELECT CITY.NAME
    FROM CITY INNER JOIN COUNTRY ON CITY.COUNTRYCODE = COUNTRY.CODE
    WHERE COUNTRY.CONTINENT = 'Africa';
    ```

38. **Average Population of Each Continent**

    ```sql
    SELECT COUNTRY.CONTINENT, FLOOR(AVG(CITY.POPULATION))
    FROM CITY INNER JOIN COUNTRY ON CITY.COUNTRYCODE = COUNTRY.CODE
    GROUP BY COUNTRY.CONTINENT;
    ```

39. **Draw The Triangle 1**

    ```sql
    DECLARE @i INT = 20;
    WHILE (@i > 0) 
    BEGIN
       PRINT REPLICATE('* ', @i) ;
       SET @i = @i - 1;
    END
    ```

40. **Draw The Triangle 2**

    ```sql
    DECLARE @i INT = 1;
    WHILE (@i <= 20) 
    BEGIN
       PRINT REPLICATE('* ', @i) ;
       SET @i = @i + 1;
    END
    ```

    