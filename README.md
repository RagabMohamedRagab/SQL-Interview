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
### Q3: What is PRIMARY KEY?
>Primary Key is one of constraint Not Accepted Null and Duplicated data in the column.

>It can be one or more key in the table.

>uniquely identifies each record in a table
**Create**
```bash
CREATE TABLE Persons (
    ID int NOT NULL PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);
```
**Drop**
```bash
ALTER TABLE Persons
DROP CONSTRAINT PK_Person;
```
### Q4: What is DEFAULT?
> Default is a contraint , Set Default value to column.

**Create**
```bash
CREATE TABLE Orders (
    ID int NOT NULL PRIMARY KEY ,
    OrderNumber int NOT NULL,
    OrderDate date DEFAULT GETDATE()
);
```

### Q5: What is FOREIGN KEY?  
> The FOREIGN KEY constraint is used to prevent actions that would destroy links between tables(Transver Dependency).

>A FOREIGN KEY is a field (or collection of fields) in one table, that refers to the PRIMARY KEY in another table

**Create**
```bash
CREATE TABLE Orders (
    OrderID int NOT NULL PRIMARY KEY,
    OrderNumber int NOT NULL,
    PersonID int FOREIGN KEY REFERENCES Persons(PersonID)
);
```
**Alter**
```bash
ALTER TABLE Orders
ADD CONSTRAINT FK_PersonOrder
FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
```
**Drop**
```bash
ALTER TABLE Orders
DROP CONSTRAINT FK_PersonOrder;
```

### Q6: What is the difference between TRUNCATE and DELETE? 

> TRUNCATE is Data definition language (DDL) , Used to remove all the records in the table.

```bash

TRUNCATE TABLE [SQLShackDemo].[dbo].[Employee];
```
> Delete is Data manipulation language (DML) , Used to delete specify record in the table based on where clause.

```bash
DELETE FROM table_name WHERE condition;
```

###  Q7: What is Normalisation?

> It is database design used to reduce data redundenty
> Easier To insertion and updating and deleting.
> It is Splited large table into Two tables and make relationships between two table.
- First Normal Form (1NF) 
   <ol>
      <li>Removing Repeat group (Multi - values)</li>
      <li>Removing Repeat Similar Name Columns</li>
      <li>Data of cell must be saming Data types of the column</li>
   <ol>
 **Example**
 
| Id | City |
| :---:|:---: | 
| 1    |Giza  | 
| 1 | Menofia | 


     Second Normal Form (2NF)
  
    
      - 1NF
     -  Removing Partial Dependency (Must be Finding Composite Primary Key To achive Partial Dependency)
     
   
   


     
   
   | Std_Id | C_Id | grade |course_name|
| --------------- | --------------- | --------------- | --------------- |
| 1| 2 |A |C#
|2 | 3 | B |C++
     
    C_Id dependence on course_name , here we must remove this partial dependency.
     
     - First Table
     
     ------------------------
     |   Std_Id  |  grade |
     ------------------------
     |   1       |     A   |
     -----------------------
     |   2       |    B    | 
     -----------------------
    - Second Table
     ------------------------
     |   C_Id | course_name |
     ------------------------
     |    2   |    C#       |
     -----------------------
     |    3   |    C++      | 
     -----------------------
   #### Here Removing Partial Dependency.


### Third Normal Form (3NF)
> 2NF 

> Removing transitive dependency ,SO must split table into two tables.


