
##### What is pattern matching.
Pattern matching is a way of searching for data when you lack the full search criteria. It uses Wild cards to allow you to build partial seach queries. 

%Wild card will return all results with first names starting with the letter K

	Select *
	From Students
	Where first_name LIKE 'K%'

Ommiting patterns with the % whild card

	Select *
	From Students
	Where first_name NOT LIKE 'K%'

Matching patterns anywhere as long as the pattern inbetween the two % exists it will return the record

	Select * 
	From Students
	Where first_name LIKE '%W%'

Pattern matching at a particular position returns all records where the letter K is in the third posiction

	Select * 
	From Students 
	Where First_name LIKE '__K%'

Pattern matching for a spesfic length
	Select *
	From Students 
	Where Frist_name LIKE '_ _ _ _  _'
##### Create a temporary table containing the structuer of another table

	Select * INTO Students_copy
	From Students
	Where 1 = 2

##### How to create StoredProcedures

	Create Procedure ProcedureName
	Begine
		Select * 
		From Students
	END

##### What are the differences between OLTP and OLAP 

OLTP: Online Transaction Processing. 
- Designed for a large amount of end users who whis to return small sets of information.
- A important attribute is to maintain concurrency 
- Quires in this case tend to be small and simple.
- Number of transactions is a way of measuring its effectiveness 

OLAP: Online analytical processing 
- Designed for small amount of requests at a time
- Uses complex queries with a large amount of aggregation
- Speed of response time is a way to mesure its effectivness

##### What are user defined functions and how many types are there.

User defined functions act much as other programming cunctions allow the engineer to save predefined functionality to be used in SQL quires. There are two main type

Scaler Functions: User defined scaler functions return a singular scaler value

Table-Valued Functions: User defined Table-Valued functions. Returns a table.
	Inline: Returns a Table of data based on a Select
	Multi-Statment: Like a Inline but can return one or more select results

##### What is the Unique constraint
Ensures that all additions to spesfic coloumn are Unique and distint Ie no duplcates.

##### What is a Index and what types are there.

A data base index provides a quick look up for data in a table, spesficaly data in a coloum or coloumns in a table. It provides a faster return of records for the cost of taking up more storage.

There are four types of Index

Non-Clusterd & Clusterd index: Clusterd index is a index whos order of rows in the index corispond to orders of records in the database. Normaly focused on one or more coloums. 

There can only be one Clusterd Index as it tries to keep the records in order based on spesfic keys

There can be many Non-clusterd indexes per table as it dose not contain the same constraint but is slower.

Both can increase the speed of operations in the db related to the table with a index.

Unique & Non-Unique
Unique indexes work to maintain data inegraty by insureing that there is no duplacates of data within a table.

##### How many types of joins are, name and describe them  

There are six types of joins

1. INNER JOIN: Return select records that have matching values in both tables
2. FULL OUTER JOIN: Return all records from Left and Right when there is a match in either of the two tables
3. Left Join: Returne all the records from the Left Table and matching records from the right table
4. Right Join: Return all the records from the Right Table and matching records from the right table
5. Self Join: Allow for joining a table on its self.
6. Cross Join: Returns the all the posoble configurations of a join. Ie each coloumn will match with every other colomune. 


##### Perform a Inner join.

Returns all the Products and their corresponding Category Name.

	Select ProductId, ProductName, CategoryName
	From Products
	INNER JOIN Categories ON Products.CategoriesID =Categories.CategoryID;

##### Preform a Full OuterJoin

Returns all records from both tables adding Nulled Coloumns where there is not coralation and filling in the correct information where there is.

	Select Customers.CustomerName, Orders.OrderID
	from Customers
	FULL OUTER JOIN Orders ON Custmers.CustomerID = Orders.CustomerID
	Order By Customer.CustomerName;

##### Perform a Left Join

Returns all elements from the Left table even if there is no corresponding record on the right, if not add null.

	Select Customer.CustomerName, OrderID
	from Customers
	LEFT JOIN Orders on Customer.CustomerID = Orders.CustomerID
	Order By Customer.Name

##### Perform a Right Join

Returns all elements from the right table even if there is no corresponding record on the left, if not add null.

	Select Customer.CustomerName, OrderID
	from Customers
	Right JOIN Orders on Customer.CustomerID = Orders.CustomerID
	Order By Customer.Name


##### Perform a self join

Allows for advanced queries of a table

Returns Unique Customers who live in the same city

	Select A.CustomerName As CustomerName1, B.CustomerName As CustomerName2, City
	from Customer A, Customer B
	Where A.CustomerId<> B.CustomerID
	And A.City = B.City
	Order BY A.City


##### Perform a Cross Join

Returns the Cartusian product of two tables and their coloumns.

	Select stu.Name, sub.Subject
	From Students as stu
	Cross Join Subjects as sub

##### What is a Foreign key 

A Foreign key is a Coloumn or collection of coloumns that referance another tables Primary key. This insures referential integrity between the two tables. Example: Coustomer.OrderID, Orders.OrderID

		CREATE Table Students(
		StudentId INT NOT NULL
		StudentName VARCHAR(255)
		LibaryId INT
		PRIMARY KEY (StudentId)
		FOREIGN KEY (LibaryID) REFERANCES Libaries(LibaryId))


		Alter Table Students
		ADD FOREIGN KEY(LibaryID)
		REFERANCES Libaries(LibaryId)

##### What is a Primary Key

A Primary Key is the Unique identifier of a Table. It must be Unique and will act as the primary referance to a record.

		Create Table Students(
		StudentId INT UNIQUE NOT NULL
		StudentName VARCHAR(225)
		PRIMARY KEY(StudentId))


##### What are Constraints

Constraints are rules that can be placed upon coloumns in tables. 

- Unique: All attrabuts in this coloumn must be unique 
- Index: Sets a field as a INDEX for faster retrival
- NOT NULL: Field must not be null
- PRIMARY KEY: 
- FORGIEN KEY
- CHECK: Verafies that all values in a field adhear to a spesfic condishion
- DEFAULT: Automaticly assigns a value to a field if non is given


##### What are UNION, MINUS and INTERSECT commands?

UNION: Combines and returns the set of two or more selects
MINUS: Removes the Duplacates of data returned by Select from that of another Select
INTERSECT: returns the result set of when two selects have matching records. It returns the Matching records.

There are three rules for running the above command
1. The Select statments must have the same about of 

	Select from Students
	Union
	Select from Contacts


##### What is the difference between DROP and TRUNCATE statements?

DROP: When a Table is DROPED all things related to that table are droped including releashionships defined on that table, integraty checks and constraints as well as User access to that table.

TRUNCATE: Retains all the meta data for tables.

##### What is the difference between DELETE and TRUNCATE statements?

TRUNCATE: This action is for removing all rows from a table and freeing up space in the DB
DELETE: While this action deleates data from a table it dose not free the space up containing the table.

##### What are Aggregate and Scalar functions?

An aggreate function: performs a function on a collection of values to return a singular scaler value 
- MIN()
- MAX()
- SUM()
- COUNT()


A scalar Function: Returns a singular scaler value based on a input.
- CONCAT()
- ROUND()

##### What are ACID properties? 

- Atomicity: This property insures that the transaction is commit in a all or nothing way
- Consistency: This ensures that updates made to the DB are valid and adhear to its rules
- Isolation: This property insures integrity of transactions that are visible to all other transactions 
- Durability: This property insures that commit transactions are stored in the database indefinitely 


