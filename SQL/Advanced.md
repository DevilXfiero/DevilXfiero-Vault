
## View

## Creating a View

Views are virtual tables that are created as a result of a SELECT query. They offer a number of advantages such as showing only a subset of data that is meaningful to users or restricting the number of rows and columns shown for security reasons.


A view containing columns from multiple tables can simplify queries by changing a multi-table query to a single-table query against a view. Views are stored in the database along with tables.

A view can be created from a single table, by joining two tables, or from another view.

```sql
-- Query 1
CREATE VIEW DigitalAssetCount AS 
SELECT ActorId, COUNT(AssetType) AS NumberOfAssets 
FROM DigitalAssets
GROUP BY ActorId;

-- Query 2
SELECT * FROM DigitalAssetCount;

-- Query 3
CREATE VIEW ActorsTwitterAccounts AS
SELECT FirstName, SecondName, URL
FROM Actors
INNER JOIN DigitalAssets  
ON Actors.Id = DigitalAssets.ActorID 
WHERE AssetType = 'Twitter';

-- Query 4
CREATE OR REPLACE VIEW ActorsTwitterAccounts AS
SELECT CONCAT(FirstName, ' ', SecondName) AS ActorName, URL
FROM Actors
INNER JOIN DigitalAssets  
ON Actors.Id = DigitalAssets.ActorID 
WHERE AssetType = 'Twitter';

-- Query 5
CREATE VIEW RichActors AS
SELECT FirstName, SecondName, Gender, NetWorthInMillions  
FROM Actors
WHERE NetWorthInMillions > (
SELECT AVG(NetWorthInMillions)
FROM Actors)
ORDER BY NetWorthInMillions DESC;

-- Query 6
CREATE VIEW RichFemaleActors AS
SELECT * FROM RichActors
WHERE Gender = 'Female';

-- Query 7
CREATE VIEW ActorDetails (ActorName, Age, MaritalStatus, NetWorthInMillions) AS
SELECT CONCAT(FirstName,' ',SecondName) AS ActorName, 
       TIMESTAMPDIFF(YEAR, DoB, CURDATE()) AS Age, 
       MaritalStatus, NetWorthInMillions 
FROM Actors;

-- Query 8
SELECT ActorName, Age, NetWorthInMillions
    FROM ActorDetails
    ORDER BY Age DESC;
```

Views are stored as virtual tables and also appear in the list of tables when SHOW TABLES is executed.

## Updatable Views

Views are not only used to query data; they can also be used to update data in the underlying tables. It is possible to insert or update rows in the base table, and in the same vein, delete rows from the table using an updatable view. In order for a view to become updatable, it must abide by certain conditions.

If the SELECT query that creates the view has aggregate functions (MAX, MIN, COUNT, SUM, etc.), DISTINCT keyword, LEFT JOIN or GROUP BY, HAVING, and UNION clauses, the resulting view will not be updatable. Similarly, a subquery that refers to the same table that appears in the FROM clause prohibits updates to the base table.

```sql
-- Query 1
CREATE VIEW ActorView AS
SELECT Id, FirstName, SecondName, NetWorthInMillions 
FROM Actors;

-- Query 2
UPDATE ActorView 
SET 
NetWorthInMillions = 250 
WHERE 
Id =1;

-- Query 3
SELECT Table_name, is_updatable
FROM information_schema.views
WHERE table_schema = 'MovieIndustry';

-- Query 4
DELETE FROM ActorView
WHERE Id = 11;
```


