# Back to the Basics

A record is a horizontal entry in a SQL DB
A Column is of course column

Common Sql Commands: 

- SELECT : extracts data from a database
	- DISTINCT : return only distinct values 
	- COUNT(returns the amount of the selected data)
	- WHERE (condition) : is used to filter records
		- BETWEEN : selects values in a given range
		- NOT BETWEEN : selects values not in a given range
		- LIKE : pattern/string matching 
		- Wildcards: 
		- "%" : represents zero, one or multiple characters
		- "_" : represents one, single character 
		- "[]" : represents any single character withing the brackets
		- "^" represents any character not in the brackets
		- "-" represents any single character withing the specified range
		- Operators:
			- "="
			- ">"
			- "<"
			-">="
			-"<="
			-"<>"
			- BETWEEN : gets values between a certain range
			- LIKE : searches for a pattern 
			- IN : To specify multiple possible values for a column

	- AND : can be combined with  WHERE
	- OR : can be combined with WHERE
	- NOT : can be combined with WHERE 
	- ORDER BY : is used to sort the result-set in ascending or descending order.
		- You can use multiple columns to order by but they have a hierarchy
			- first var takes priority
			- then second var if first vars match...etc
		- sorts the records in ascending order by default. to sort descending use...
		- DESC
	-IS NULL 
	- IS NOT NULL
	- SELECT TOP : used to specify the number of records to return
		- useful on large tables with thousands of records. 
	- PERCENT : self explanatory syntax "Select Top 50 PERCENT * FROM Customers"
	- MIN() : returns the smallest value of the selected column
	- MAX() : returns the largest value of the selected column
	- COUNT() : returns the number of rows that matches a specified criterion
	- AVG() : the average value of a numeric column
	- SUM() : the total sum of a num column
	- AS : gives selected "column, table...etc" an alias, "SELECT column_name AS alias_name"
	-UNION : is used to combine the result set of two or more SELECT statements
		- every SELECT statement withing UNION must have the same number of columns	
		- the columns must also have similar data types
		- the columns in every SELECT statement must also be in the same order
		- selects only distinct by default
		- UNION ALL : to allow dups 

	- GROUP BY : groups rows that have the same values into summary rows
		- often used with aggregate functions (COUNT(), MAX(), MIN()...etc)
	- HAVING was added to sql because WHERE cannot be used with aggregate functions
		- "GROUP BY column_name(s) HAVING condition"
	- EXISTS is used to test for the existence of any record in a subquery.
		- returns TRUE if the subquery returns one or more records.
	- ANY and ALL : allow you to perform a comparison between a single column value and a range of other values
		- returns a boolean value as a result
		- returns TRUE if ANY of the subquery values meet the condition
		- ANY : means that the condition will be true if the operation is true for any of the values in the range
		- ALL : returns true if all of the subquery values meet the condition
	SELECT INTO : statement copies data from one table into a new table
	INSERT INTO SELECT : copies data from one table and inserts it into another table
		-requires that the data types in source and target tables match
		- existing records in the target table are unaffected
	- CASE : goes through conditions and returns a value when the first condition is met (like an if-then-else statement)
		- So once a condition is true, it will stop reading and return the result. If no conditions are true, it returns the value in teh ELSE clause.
		- If there is no ELSE part and no conditions are true, it returns NULL.
		"CASE 
			WHEN condition1 THEN result1
			WHEN condition2 THEN result2
			WHEN condition3 THEN result3
			ELSE result
		END"
		
SQL null functions *these all do the same thing but used in different/ MySQL SQLSERVER and ORACLE: 
	- IFNULL() : lets you return an alternative value if an expression is NULL
	- ISNULL() : SQLSERVER
	- COALESCE() : MySQL
	- NVL() : ORACLE


Stored Procedures: 
	- CREATE PROCEDURE : creates a sproc "CREATE PROCEDURE procedure_name AS sql_statement GO"
	- AS : starts the beggining of the sproc logic
	- GO : ends the sproc logic 
	- EXEC : executes a sproc "EXEC procedure_name"
	- @VariableName : declares a var for the sproc  "CREATE PROCEDURE SelectAllCustomers @City nvarchar(30)"
		- set vars during execution "EXEC SelectAllCustomers @City = 'London'"

Comments: 
	- Single Line "--"
	- Multi-Line start "/*" end "*/"

Logical Operators: 
	- ALL : TRUE if all the subquery values meet the condition
	- AND : TRUE if all the conditions separated by AND is TRUE
	- ANY : TRUE if any of the subquery values meet the condition
	- BETWEEN : TRUE if the operand is within the range of comparisons
	- EXISTS : TRUE if the subquery returns one or more records 
	- IN : TRUE if the operand is equal to one of a list of expressions
	- LIKE : TRUE if te operand matches a pattern
	- NOT : Displays a record if the condition(s) is NOT TRUE
	- OR : TRUE if any of the conditions separated by OR is TRUE
	- SOME : TRUE if any of the subquery values meet the condition

- UPDATE : updates data in a database
- DELETE : deletes data from a database
- INSERT INTO : inserts new data into a database
- CREATE DATABASE : creates a new database
- ALTER DATABASE - modifies a database
- CREATE TABLE - creates a table
- ALTER TABLE - alters a table
	- "ALTER TABLE table_name ADD column_name datatype"
- DROP TABLE - deletes a table 
- CREATE INDEX - creates an index (search key)
- DROP INDEX - deletes an index


Constraints: 
	- NOT NULL : Ensures that a column cannot have a NULL value
	- UNIQUE : Ensures that all values in a column are different
	- PRIMARY KEY : A combination of a NOT NULL and UNIQUE niquely identifies each row in a table
	- FOREIGN KEY : Prevents actions that would destroy links between tables
	- CHECK : Ensures that the values in a column satisfies a specific condition
	- DEFAULT : sets a default value for a column if no value is specified
	- CREATE INDEX : Used to create and retrieve data from the database very quickly
		- Users cannot see the indexes, they are just used to speed up searches/queries.
	- PRIMARY KEY : Only one of these per table
	- FOREIGN KEY : is used to prevent actions that would destroy links between tables
		- is a field (or collection of fields) in one table, that refers to the PRIMARY KEY in another table
		- the table with the foreign key is called the child table, and the table with the primary key is called the parent table
		- syntax "CREATE TABLE Orders (
			OrderID int NOT NULL PRIMARY KEY,
			OrderNumber int NOT NULL,
			PersonID int FOREIGN KEY REFERENCES Persons(PersonID)
		)"
		- naming syntax "CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)"
			
Field: 
	- AUTO INCREMENT : allows a unique number to be generated automatically when a new record is inserted into a table.
		- often this is the primary key field that we would like to be created automatically every time a new record is inserted.
		- syntax "CREATE TABLE Persons (
			Personid in NOT NULL AUTO_INCREMENT,
			PRIMARY KEY (Personid)"
		- you can change the start auto increment value with "AUTO_INCREMENT=3"
		- sql server syntax : "CREATE TABLE Persons(
			Personid int IDENTITY(1, 1) PRIMARY KEY"
		- IDENTITY(starting_value, incremented_by_value)

Views : 
	- is a virtual table based on the result-set of an SQL statement
	- "CREATE VIEW view_name AS "
	- a view can be updated with:
		- "CREATE OR REPLACE VIEW view_name AS"

SQL Dates: 
	- DATE : format YYYY-MM-DD
	- DATETIME : format YYYY-MM-DD HH:MI:SS
	-SMALLDATETIME : format YYYY-MM-DD HH:MI:SS
	- TIMESTAMP: format a unique number

JOINS in SQL:
	- (INNER) JOIN: Returns records that have matching values in both tables
	- LEFT (OUTER) JOIN: Returns all records from the left table, and the matched records from the right table
	- RIGHT (OUTER) JOIN: Returns all records from the right table, and the matched records from the left table
	- FULL (OUTER) JOIN: Returns all the records when there is a match in either left or right table


SQL Injection: 
	- Make sure to parameterize your SQL sprocs/Queries/ect 
	- SQL parameters are values that are added to an SQL query at execution time in a controlled manner
	- Note that parameters are represented in the SQL statement by a @ marker
	- SQL engine checks each parameter to ensure that it is correct for its column and are treated literally, and not as part of the SQL to be executed.


SQL Server Data Types: 
	- String
		- char(n)
		- varchar(n)
		- varchar(max)
		- text
		- nchar
		- nvarchar
		- nvarchar(max)
		- ntext
		- binary(n)
		- varbinary
		- varbinary(max)
		- image 
	
	- Numeric
		- bit
		- tinyint
		- smallint
		- int
		- bigint
		- decimal(p, s)
		- numeric(p,s)
		- smallmoney
		- money
		- float
		- real
	- Date and Time Data Types
		- datetime
		- datetime2
		- smalldatetime
		- date
		- time
		- datetimeoffset
		- timestamp
	- Other Data Types
		- sql_variant
		- uniqueidentifier
		- xml
		- cursor
		- table


SQL Keywords: 
	- ADD	
	- ADD CONSTRAINT
	- ALTER
	- ALTER COLUMN
	- ALTER TABLE
	- ALL
	- AND
	- ANY
	- AS
	- ASC
	- BACKUP DATABASE
	- BETWEEN
	- CASE 
	- CHECK
	- COLUMN
	- CONSTRAINT
	- CREATE
	- CREATE DATABASE
	- CREATE INDEX
	- CREATE OR REPLACE VIEW 
	- CREATE TABLE
	- CREATE PROCEDURE
	- CREATE UNIQUE INDEX

SQL Server Advanced Functions: 
	- CAST : Converts a value (of any type) into a specified datatype
	- COALESCE : Returns the first non-null value in a list
	- CONVERT : Converts a value (of any type) into a specified datatype
	- CURRENT USER : Returns the name of the current user in the SQL Server database
	- IIF : Returns a value if a condition is TRUE, or another value if a condition is FALSE
	- ISNULL : Return a specified value if the expression is NULL, otherwise return the expression
	- ISNUMERIC : tests whether an expression is numeric
	- NULLIF : Returns NULL if two expressions are equal
	- SESSION USER: Returns the name of the current user in the SQL Server database
	- SESSION PROPERTY: Returns the session settings for a specified operation
	- SYSTEM USER : Returns the login name for the current user
	- USER NAME : Returns the database user name based on the specified id.


SQL Indexes: 
	- Clustered Index: defined the order in which data is physiclly stored in a table
		- Table data can be sorted in only way, therefore there can be only one clustered index per table.
		- The PRIMARY KEY constraint automatically creates a clustered index on that particular column.
		- syntax "CREATE CLUSTERED INDEX tblStudent_Gender_Score 
		ON student(gender ASC, total_score DESC)"
		- An index that is created on more than one column is called "composite index"

	- Non-Clusterd Index: 
		- Doesn't sort the physical data inside the table. in fact a non-clustered index is stored at one place and table data is stored in another place.
		- It is important to mention here that inside the table the data will be sorted by a clustered index. However inside the non-clustered index data is stored in the 
		specified order. 
		- the index contains column values on which the index is crated and the address of the record that the column value be-longs to.
		- When a query is issued against a column on which the index is created, the database will first go to the index and look for the address of the corresponding row in the table.
		- When a query is issued against a column on which the index is created, the dtabse will first go to the index and look for the address of the corresponding row in the table. It will then go to that row.
		- It will then go to that row address and fetch other column values. It is due to this additional step that non-clustered indexes are slower than clustered indexes. 



Merge in SQL Server: 
	- modifies an existing table based on the result of comparison between the key fields with another table in the context.
	- the MERGE statement combines the INSERT, UPDATE, and the DELETE operations altogether.
	- A most common use case is while trying to maintain Slowly Changing Dimensions (SCD)  in the data warehouse
	- is improvement in performance compared to using all three INSERT UPDATE AND DELETE
	- MERGE allows the data to only be read once in the transaction


Slowly Changing Dimensions (SCD): 
	- in data management and data warehousing is a dimension which contains relatively static data 
		- which can change slowly but unpredictable, rather than according to a regular schedule. 
		- e.x entities as names of geographical locations, customers, or products.