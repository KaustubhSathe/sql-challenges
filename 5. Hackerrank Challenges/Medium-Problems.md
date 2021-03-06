# Medium-Problems

1. **The PADS**

   ```sql
   SELECT NAME + '(' + SUBSTRING(OCCUPATION,1,1) + ')' FROM OCCUPATIONS 
   ORDER BY NAME ASC;
   
   SELECT 'There are a total of ' + CAST(COUNT(*) AS varchar) + ' ' + LOWER(Occupation) + 's.'
   FROM OCCUPATIONS 
   GROUP BY Occupation
   ORDER BY COUNT(*), Occupation ASC;
   ```

2. **The Report**

   ```sql
   SELECT CASE
   WHEN GRADE < 8 THEN NULL
   ELSE NAME
   END, 
   GRADE, MARKS
   FROM STUDENTS JOIN GRADES ON MARKS BETWEEN MIN_MARK AND MAX_MARK
   ORDER BY GRADE DESC,NAME;
   ```

3. **Occupations**

   ```sql
   SELECT
       D.Name,
       P.Name,
       S.Name,
       A.Name
   FROM
       (SELECT ROW_NUMBER() OVER (ORDER BY Name) N, Name FROM Occupations WHERE Occupation = 'Doctor')    D              FULL OUTER JOIN
       (SELECT ROW_NUMBER() OVER (ORDER BY Name) N, Name FROM Occupations WHERE Occupation = 'Professor') P ON P.N = D.N FULL OUTER JOIN
       (SELECT ROW_NUMBER() OVER (ORDER BY Name) N, Name FROM Occupations WHERE Occupation = 'Singer')    S ON S.N = D.N OR S.N = P.N FULL OUTER JOIN
       (SELECT ROW_NUMBER() OVER (ORDER BY Name) N, Name FROM Occupations WHERE Occupation = 'Actor')     A ON A.N = S.N OR A.N = D.N OR A.N = P.N
       
   ```
   
4. **Binary Tree Nodes**

   ```sql
   SELECT N,CASE 
   WHEN P IS NULL THEN 'Root'
   WHEN P IS NOT NULL AND N IN (SELECT DISTINCT P FROM BST) THEN 'Inner'
   ELSE 'Leaf'
   END FROM BST
   ORDER BY N;
   ```

5. **New Companies**

   ```sql
   select Company.Company_code, Company.founder, Count(DISTINCT Employee.Lead_Manager_code), Count(DISTINCT Employee.senior_manager_code), count(DISTINCT Employee.manager_code), count(DISTINCT Employee.employee_code) from Company inner join Employee on Employee.Company_Code = Company.Company_Code group by Company.Company_Code, Company.founder order by Company.Company_code;
   ```

6. **Weather Observation Station 18**

   ```sql
   SELECT CONVERT(decimal(10,4),ABS(MAX(LAT_N) - MIN(LAT_N)) + ABS(MAX(LONG_W) - MIN(LONG_W))) 
   FROM STATION;
   ```

7. **Weather Observation Station 19**

   ```sql
   SELECT
       CONVERT(decimal(10,4),SQRT(
           POWER(MAX(LAT_N)  - MIN(LAT_N),  2)
         + POWER(MAX(LONG_W) - MIN(LONG_W), 2)
       ))
   FROM 
       STATION;
   ```

8. **Top Competitors**

   ```sql
   select Hackers.hacker_id,Hackers.name
   from Submissions JOIN Challenges ON Submissions.challenge_id = Challenges.challenge_id
   JOIN Difficulty ON Challenges.difficulty_level = Difficulty.difficulty_level
   JOIN Hackers ON Submissions.hacker_id = Hackers.hacker_id
   where Submissions.score = Difficulty.score
   group by Hackers.hacker_id,Hackers.name
   having count(Submissions.hacker_id) > 1
   order by count(Hackers.hacker_id) desc, Hackers.hacker_id asc;
   ```

9. **Ollivander's Inventory**

   ```sql
   select w.id, p.age, w.coins_needed, w.power from Wands as w join Wands_Property as p on (w.code = p.code) where p.is_evil = 0 and w.coins_needed = (select min(coins_needed) from Wands as w1 join Wands_Property as p1 on (w1.code = p1.code) where w1.power = w.power and p1.age = p.age) order by w.power desc, p.age desc
   ```


10. **Weather Observation Station 20**

    ```sql
    SELECT CAST(AVG(LAT_N) AS NUMERIC(20,4)) 
    FROM (SELECT LAT_N, 
                 ROW_NUMBER() OVER (ORDER BY LAT_N ASC) AS RowAsc, 
                 ROW_NUMBER() OVER (ORDER BY LAT_N DESC) AS RowDesc 
          FROM STATION) x
    WHERE RowAsc IN (RowDesc, RowDesc - 1, RowDesc + 1);
    ```

    
