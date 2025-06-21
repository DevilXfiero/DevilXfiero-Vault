
## Types of Joins

### Cross Join

We’ll start with the cross join, which is also known as the cartesian product. In this case, we pick the first row of Table A and match it with every row of Table B.

## Inner Join

In case of an inner join, a condition, or multiple conditions, are tested to determine if a row from Table A should be joined with a row from Table B. This condition is called the **join predicate**.


## Left Outer Join

In the case of left join, the result set consists of rows that match the join predicate and also rows from the table specified on the left of the left join clause that doesn’t match the join predicate

## Right Outer Join

The right join is the reverse of the left join. In this case, all rows from the right table are always included in the result set and only those rows from the left table make it to the result set that satisfies the join condition.


## Full Outer Join

In the case of a full join, rows from both the tables are included in the result set. Rows that evaluate true for the join predicate are only included once.




Self Inner Join 
```sql
SELECT * FROM Actors a INNER JOIN Actors b;

-- Query 2
SELECT * FROM Actors a INNER JOIN Actors b USING(FirstName);

-- Query 3
SELECT * FROM Actors a INNER JOIN Actors b USING(NetWorthInMillions);
```

Inner Join
```sql
SELECT FirstName, SecondName, AssetType, URL
FROM Actors 
INNER JOIN DigitalAssets  
ON Actors.Id = DigitalAssets.ActorID;

-- Query 2
SELECT FirstName, SecondName, AssetType, URL 
FROM Actors 
INNER JOIN DigitalAssets 
USING(Id);

-- Query 3
SELECT FirstName, SecondName, AssetType, URL 
FROM Actors, DigitalAssets 
WHERE ActorId=Id;
```


## Union

The **UNION** clause allows us to combine the results from several queries together. The clause doesn’t join the table but merely clubs the two results together.


```sql
SELECT FirstName FROM Actors 
UNION 
SELECT URL FROM DigitalAssets;

-- Query 2
(SELECT CONCAT(FirstName, ' ', SecondName) AS "Actor Name" 
FROM Actors 
ORDER BY NetworthInMillions DESC 
LIMIT 2)
UNION
(SELECT CONCAT(FirstName, ' ', SecondName) AS "ThisAliasIsIgnored" 
FROM Actors 
ORDER BY NetworthInMillions ASC 
LIMIT 2);

-- Query 3
SELECT FirstName, Id FROM Actors 
UNION 
SELECT FirstName FROM Actors;  
-- When using the **UNION** clause, the two result sets being combined should have the same number and order of columns. The columns from the result sets should be of the same type or types that are compatible.

-- Query 4
-- To make the above query work, we can insert a _fake column_ or null as follows:
SELECT FirstName, Id FROM Actors 
UNION 
SELECT FirstName, null FROM Actors;

-- Query 5
SELECT MaritalStatus FROM Actors 
UNION 
SELECT Gender FROM Actors;

-- Query 6
-- Note that the union clause doesn’t output duplicate values and works similarly to the distinct clause. If we want duplicate values to be included in the query result, we need to use the **UNION ALL** clause as follows
SELECT MaritalStatus FROM Actors 
UNION ALL
SELECT Gender FROM Actors;

-- Query 7
(SELECT CONCAT(FirstName, ' ', SecondName) AS "Actor Name"  
FROM Actors  
ORDER BY NetworthInMillions DESC  LIMIT 2)  
UNION  
(SELECT NetworthInMillions 
FROM Actors 
ORDER BY NetworthInMillions ASC);

-- Query 8
(SELECT CONCAT(FirstName, ' ', SecondName) AS "Actor Name"  
FROM Actors  
ORDER BY NetworthInMillions DESC  LIMIT 2)  
UNION  
(SELECT NetworthInMillions 
FROM Actors 
ORDER BY NetworthInMillions ASC LIMIT 3);
```

## Nested Queries


### Nested Scalar Queries

```sql
SELECT URL 
FROM DigitalAssets 
WHERE AssetType = "Instagram" AND 
ActorId = (SELECT Id 
           FROM Actors 
           WHERE FirstName = "Brad");

SELECT FirstName 
FROM Actors 
INNER JOIN DigitalAssets 
ON ActorId = Id 
WHERE LastUpdatedOn = (SELECT MAX(LastUpdatedOn) 
                       FROM DigitalAssets);

```


When a subquery returns a single value, it is said to return a scalar operand. Nesting allows us to get the result in one shot.


### Nested Column Queries

```sql
SELECT * FROM Actors 
INNER JOIN DigitalAssets ON ActorId=Id 
WHERE AssetType = ANY (SELECT DISTINCT AssetType 
                       FROM DigitalAssets
                       WHERE AssetType != 'Website');

-- Query 2
SELECT * FROM Actors 
INNER JOIN DigitalAssets ON ActorId=Id 
WHERE AssetType != 'Website';

-- Query 3
SELECT FirstName, SecondName
FROM Actors
WHERE Id = ANY (SELECT ActorId
                FROM DigitalAssets
                WHERE AssetType = 'Facebook');

-- Query 4
SELECT FirstName, SecondName
FROM Actors
WHERE Id IN (SELECT ActorId
             FROM DigitalAssets
             WHERE AssetType = 'Facebook');

-- Query 5
SELECT FirstName, SecondName 
FROM Actors 
WHERE NetworthInMillions > ALL (SELECT NetworthInMillions 
                                FROM Actors
                                WHERE FirstName LIKE "j%");
```

The **ANY** clause has an alias **IN** that can be used interchangeably.

### Nested Row Queries
```sql
-- Query 1
SELECT FirstName
FROM Actors
INNER JOIN DigitalAssets
ON Id=ActorId 
AND MONTH(DoB) = MONTH(LastUpdatedOn) 
AND DAY(DoB) = DAY(LastUpdatedOn);

-- Query 2
SELECT FirstName
FROM Actors 
WHERE (Id, MONTH(DoB), DAY(DoB))
IN ( SELECT ActorId, MONTH(LastUpdatedOn), DAY(LastUpdatedOn)
     FROM DigitalAssets);

--Query 3
SELECT ActorId, AssetType, LastUpdatedOn FROM DigitalAssets;

-- Query 4
SELECT FirstName, AssetType, LastUpdatedOn 
FROM Actors  
INNER JOIN (SELECT ActorId, AssetType, LastUpdatedOn 
            FROM DigitalAssets) AS tbl 
ON ActorId = Id;

-- Query 5
SELECT FirstName, AssetType, LastUpdatedOn 
FROM Actors 
INNER JOIN (SELECT ActorId, AssetType, LastUpdatedOn 
            FROM DigitalAssets) AS tbl 
ON ActorId = Id
WHERE FirstName = "Kim";

-- Query 6
SELECT FirstName, AssetType, LastUpdatedOn 
FROM Actors 
INNER JOIN (SELECT ActorId, AssetType, LastUpdatedOn 
            FROM DigitalAssets) AS tbl 
ON ActorId = Id
WHERE FirstName = "Kim"
ORDER BY LastUpdatedOn DESC LIMIT 1;
```

## EXISTS Operator

```sql
-- Query 1
SELECT *
FROM Actors
WHERE EXISTS ( SELECT * 
               FROM DigitalAssets
               WHERE BINARY URL LIKE "%clooney%"); 

-- Query 2
SELECT *
FROM Actors
WHERE NOT EXISTS ( SELECT * 
               FROM DigitalAssets
               WHERE BINARY URL LIKE "%clooney%"); 
```
## Correlated Queries

Correlated queries are a type of nested queries. The distinguishing feature about them is that the inner query references a table or a column from the outer query.

```sql
-- Query 1
SELECT FirstName
FROM Actors 
INNER JOIN DigitalAssets
ON Id = ActorId
WHERE URL LIKE CONCAT("%",FirstName,"%") 
AND AssetType="Twitter";

-- Query 2
SELECT FirstName
FROM Actors
WHERE EXISTS (SELECT URL 
              FROM DigitalAssets
              WHERE URL LIKE CONCAT("%",FirstName,"%") 
              AND AssetType="Twitter");
```

## Multi-Table Operations

### Multi-Table Delete

We know how to delete data from a single table, however, if you are confronted with a situation where you want to delete data from one table and also any related data from other tables, you can employ the multi-table delete queries.

```sql
-- Query 1
DELETE Actors, DigitalAssets   -- Mention tables to delete rows from
FROM Actors   -- The inner join creates a derived table with matching rows from both tables    
INNER JOIN DigitalAssets
ON Actors.Id = DigitalAssets.ActorId
WHERE AssetType = "Twitter";

-- Query 2
DELETE FROM Actors, DigitalAssets
USING Actors        
INNER JOIN DigitalAssets
ON Actors.Id = DigitalAssets.ActorId
WHERE AssetType = "Twitter";

-- Query 3
DELETE Actors 
FROM Actors 
WHERE EXISTS ( SELECT * 
               FROM Actors 
               INNER JOIN DigitalAssets
               ON  Id = ActorId 
               WHERE AssetType="Twitter");

-- The above query fails because MySQL disallows rows to be deleted from a table if the same table also appears in the **SELECT** clause, i.e., we can’t delete from a table that’s read from in a nested subquery.

-- Query 4
DELETE Actors 
FROM Actors 
WHERE EXISTS (SELECT * 
              FROM DigitalAssets 
              WHERE ActorId = Id AND AssetType = "Twitter");
-- To make above work

-- Query 5
DELETE Actors, DigitalAssets   -- specify the tables to delete from
FROM Actors, DigitalAssets   -- reference tables
WHERE ActorId = Id   -- conditions to narrow down rows         
AND FirstName = "Johnny"
AND AssetType != "Pinterest";
```


## Multi-Table Update

```sql
-- Query 1
UPDATE 
Actors INNER JOIN DigitalAssets 
ON Id = ActorId 
SET FirstName = UPPER(FirstName), SecondName = UPPER(SecondName), URL = UPPER(URL) 
WHERE AssetType = "Facebook";

-- Query 2
UPDATE  Actors, DigitalAssets
SET FirstName = UPPER(FirstName), SecondName = UPPER(SecondName), URL = UPPER(URL) 
WHERE AssetType = "Facebook"
AND ActorId = Id;
```

## SELECT AND INSERT

```sql
-- Query 1
CREATE TABLE Names (name VARCHAR(20),
                    PRIMARY KEY(name));

-- Query 2
INSERT INTO Names(name) 
SELECT SecondName FROM Actors;

-- Query 3
INSERT IGNORE INTO Names(name) 
SELECT SecondName 
FROM Actors WHERE Id = 1;

-- Query 4
CREATE TABLE MyTempTable SELECT * FROM Actors;

-- Query 5
CREATE TABLE NamesWithDoBs ( 
Id INT AUTO_INCREMENT,
Name VARCHAR(20) NOT NULL DEFAULT "unknown",  
DoB DATE,  
PRIMARY KEY(Id), KEY(Name), KEY(DoB))  SELECT FirstName, DoB FROM Actors;

-- Query 6
CREATE TABLE CopyOfActors LIKE Actors;

```

## REPLACE

```sql
REPLACE INTO
Actors (Id, FirstName, SecondName,DoB, Gender, MaritalStatus, NetworthInMillions)
VALUES (3, "George", "Clooney", "1961-05-06","Male", "Married", 500.00);

-- To see the result of the query
SELECT * FROM Actors;

-- Query 2
REPLACE INTO 
Actors (Id)
VALUES (3);

-- To see the result of the query
SELECT * FROM Actors;

-- Query 3
REPLACE INTO  Actors 
SET id = (SELECT Id 
          FROM Actors 
          WHERE FirstName="Brad");
```

