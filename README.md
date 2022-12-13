### Q1: What is a VIEW? 
 >A view is a virtual table that triggers from join between two tables or more .
 
 **Create :**
 ```bash
 CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
 ```
**Update:**
 ```bash
 CREATE OR REPLACE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
 ```
 **Drop :**
 ```bash
 DROP VIEW view_name;
 ```
 
### Q2: Define a Temp Table ?
>Temporary tables are used to store data temporarily and they can perform CRUD (Create, Read, Update, and Delete), join, and some other operations like the persistent
database tables. Temporary tables are dropped when the session that creates the table has closed

- Local Temporary Table
- Global Temporary Table

**Local Temporary**
>The local temporary tables are visible for the duration of the connection and when the session is closed the local temporary table are dropped automatically.
>Local temporary tables can be created using the “CREATE TABLE” syntax but a single hashtag (#) sign must be added in front of their names

**Create**
```bash

CREATE TABLE #TempPersonTable (
    PersonID int PRIMARY KEY IDENTITY(1,1),
    LastName varchar(255),
    FirstName varchar(255),
    City varchar(255)
)

```
>After creating the table, we can insert data into it as the persisted tables.

```bash
INSERT INTO #TempPersonTable
VALUES
( 'Watson', 'Juan', 'Cleveland'),
( 'Baker', 'Dwayne', 'Fort Wayne'),
( 'Walker', 'Eric', 'Tucson'),
( 'Peterson', 'Bob', 'Indianapolis');
 
SELECT *
FROM #TempPersonTable;
```
>
**Global Temporary Table**
>These tables can be accessed by all other sessions.
>he CREATE TABLE statement and their names must be prefixed with the double hashtag (##) sign.

```bash
CREATE TABLE ##Customers (CustomerId INT IDENTITY(1,1) PRIMARY KEY,
CustomerFullName VARCHAR(50),
EMail VARCHAR(50),
CustomerAddress VARCHAR(50),
Country VARCHAR(50))
```
> After creating the temporary table, we can populate and query it.
```bash
INSERT INTO ##Customers
VALUES('Olivia Rodriguez','hlvdw.wvmqi@rkx.co','66 Elizabeth Street','Canada'),
('Riley Hall','efkfu.ngtpgi@rgg.org','23 Brookside Drive','U.K.') ,
('Allison Lopez','ygpnm.wdvyufu@bevl.com','11 Church Road','South Africa'),
('Gianna King','nklwjv.wimmhzr@ncni.co','193 Park Place','Belgium')
 
SELECT * FROM ##Customers
```
**Delete Temp Table**
```bash
BEGIN TRAN 
DELETE FROM #TestTempTable

BEGIN TRAN 
DELETE FROM ##TestTempTable
```
