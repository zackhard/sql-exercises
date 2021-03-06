Leet Code Database Challenges
#Table of Contents

[Main Page](https://github.com/asantos3026/lisa-aileen-sql/blob/master/README.md)<br><br>
[Combine Two Tables](#combine-two-tables)<br>
[Second Highest Salary](#second-highest-salary)<br>
[Nth Highest Salary](#nth-highest-salary)<br>
[Rank Scores](#rank-scores)<br>
[Consecutive Numbers](#consecutive-numbers)<br>
[Employees Earning More Than Their Managers](#employees-earning-more-than-their-managers)<br>
[Duplicate Emails](#duplicate-emails)<br>
[Customers Who Never Order](#customers-who-never-order)<br>
[Department Highest Salary](#department-highest-salary)<br>
[Department Top Three Salaries](#department-top-three-salaries)<br>
[Delete Duplicate Emails](#delete-duplicate-emails)<br>
[Rising Temperature](#rising-temperature)<br>
[Trips Users](#trips-users)<br>

## Combine Two Tables
[Back to Table of Contents](#table-of-contents)

[Combine 2 Tables](http://i.imgur.com/Y9AsIfj.png)


```
SELECT FirstName, LastName, City, State FROM Person
LEFT JOIN Address ON Address.personid=Person.personid;
```

## Second Highest Salary
[Back to Table of Contents](#table-of-contents)

[Second Highest Salary](http://i.imgur.com/x2DGGfN.png)

```
SELECT MAX(Salary) AS SecondHighestSalary FROM Employee 
    WHERE Salary < ALL(SELECT MAX(Salary) FROM Employee);
```

## Nth Highest Salary
[Back to Table of Contents](#table-of-contents)

[Nth Highest Salary](http://i.imgur.com/7Zdr9xO.png)

```
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  SET N = N-1;
  RETURN (
      SELECT DISTINCT Salary FROM Employee
      ORDER BY Salary DESC
      LIMIT 1 OFFSET N
  );
END
```

## Rank Scores
[Back to Table of Contents](#table-of-contents)

[Rank Scores](http://i.imgur.com/prWt6ZZ.png)

```
SELECT name, continent, population FROM world
```

## Consecutive Numbers
[Back to Table of Contents](#table-of-contents)

[Consecutive Numbers](http://i.imgur.com/aOt4kPH.png)


```
SELECT name FROM world
WHERE population>200000000
```

## Employees Earning More Than Their Managers
[Back to Table of Contents](#table-of-contents)

[Employees Earning More Than Their Managers](http://i.imgur.com/aOt4kPH.png)


```
SELECT name, GDP/population FROM world WHERE population > 200000000
```

## Duplicate Emails
[Back to Table of Contents](#table-of-contents)

[Duplicate Emails](http://i.imgur.com/KjWmY9n.png)

```
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950
```

## Customers Who Never Order
[Back to Table of Contents](#table-of-contents)


[Customers Who Never Order](http://i.imgur.com/GcLdsCk.png)

```
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')
```


## Department Highest Salary
[Back to Table of Contents](#table-of-contents)

[Department Highest Salary Part 1](http://i.imgur.com/GJvJRwx.png)

[Department Highest Salary Part 2](http://i.imgur.com/8HMfgke.png)

```
SELECT SUM(population)
FROM world
```

## Department Top Three Salaries
[Back to Table of Contents](#table-of-contents)

[Department Top Three Salaries Part 1](http://i.imgur.com/MZK0e3M.png)
[Department Top Three Salaries Part 2](http://i.imgur.com/iDsfOnY.png)

```
SELECT matchid, player FROM goal 
  WHERE teamid = 'GER';
```

## Delete Duplicate Emails
[Back to Table of Contents](#table-of-contents)

[Delete Duplicate Emails](http://i.imgur.com/aolwsNw.png)

```
SELECT COUNT(id) FROM stops
```

## Rising Temperatures
[Back to Table of Contents](#table-of-contents)

[Rising Temperatures](http://i.imgur.com/uVkmiLj.png)

```
SELECT id, title
 FROM movie
 WHERE yr=1962
```

## Trips Users
[Back to Table of Contents](#table-of-contents)

[Trips and Users Part 1](http://i.imgur.com/y7yt9Cp.png)
[Trips and Users Part 2](http://i.imgur.com/Z8Qxdgg.png)

```
SELECT yr,COUNT(title) FROM
  movie JOIN casting ON movie.id=movieid
         JOIN actor   ON actorid=actor.id
WHERE name='John Travolta'
GROUP BY yr
HAVING COUNT(title)=(SELECT MAX(c) FROM
(SELECT yr,COUNT(title) AS c FROM
   movie JOIN casting ON movie.id=movieid
         JOIN actor   ON actorid=actor.id
 WHERE name='John Travolta'
 GROUP BY yr) AS t
)
```
