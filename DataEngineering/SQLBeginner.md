# Beginner SQL
## Overview
### What You'll Learn

In this section you'll learn:
1. What Database and Database Management Systems are
2. What SQL is
3. Uses and Applications of SQL
4. SQL Syntax
5. Basic SQL Statements
  * SELECT
  * SELECT DISTINCT
  * WHERE
  * Logical operators
    * AND
    * OR
    * NOT
    * IN
    * BETWEEN
    * LIKE
  * Aggregate functions
    * COUNT
    * AVG
    * SUM
  * ORDER BY
  * GROUP BY
  * HAVING

### Prerequisites

None!

### Introduction

Databases are crucial to organize and manage large amounts of data. In this section, you will learn what databases are and how to access them using a query language called SQL. To become familiar with the SQL language, this workshop will use [SQLFiddle](http://sqlfiddle.com/) as a playground for you to practice and reinforce what you learn in this section.

## Database and Database Management Systems

A database is a collection of data, a place to store and access information. Database management systems (DBMS) are systems that manage how to interact with a database. DBMS defines how users can access, modify, and manipulate data in a database.

One type of database management system is the relational database management system (RDBMS). Relational means that data has relationships with other data in the database in the form of rows and columns. Relational databases are essentially a group of data tables. Popular RDBMS's are Microsoft SQL Server, MySQL, and Oracle.

## What is SQL?
SQL stands for Structured Query Language (pronounced as "sequel" or "S-Q-L"). It is a programming language used to access relational databases.

SQL syntax between DBMS are very similar, but there are slight differences. This workshop will be using syntax for a popular RDBMS called Microsoft SQL Server (MS SQL Server).

## SQL Uses and Applications

SQL has four main uses as a Data Definition Language (DDL), Data Manipulation Language (DML), Transaction Control Language (TCL), and Data Control Language (DCL):

1. SQL as a Data Definition Language defines databases and labels data with additional properties.

2. SQL as a Data Manipulation Language manages data in the database.

3. SQL as a Transaction Control Language manages transaction made in the database, such as any changes to the database from DML statements.

4. SQL as a Data Control Language controls accesses to databases.

SQL programming language can be used with anything that uses databases. A few example are:

* health care - patient records
* business - trends, sales, inventory
* website displaying analyzed data

## Syntax
Relational databases are represented as tables. Each table is identified by a name. In MS SQL, the names of tables are in quotes ```"tableName" ```. Tables are made up of rows (also called records) and columns.

SQL uses many keywords. Keywords are not case sensitive, but are conventionally uppercased. ```SELECT``` and ```select``` both work, but using uppercased letters for keywords is recommended.  

Semicolons are the standard way to separate SQL statements. Depending on the database system, having semicolons at the end may be optional. However, it is the standard and the recommended way to always end statements with semicolons.

When defining or calling text values, use single quotes around the value (ex.```'string'```). Some databases do allow double quotation marks instead, but in MS SQL Server, use single quotes. Numeric fields do not use any quotation marks.

General syntax:
```
SELECT column1, column2, ..., columnN FROM tableName
WHERE condition;
```
Select these data points from this table where the data satisfies these conditions.

## Commenting
<b>Single line comments:</b>

To write comments on a single line, add two dashes before the comment

```
-- This is a single line comment
```

<b>Multi line comments and inline comments: </b>

To write comments on multiple lines and inline, write comments in between the asterisks ```/* */ ```
```
/*
This is a
multi line comment
*/

SELECT * FROM tableName; /* This is an inline comment */
```

## SQL Statements

To practice using SQL, this workshop will be using an online application called <a href="http://sqlfiddle.com" target="blank"> sqlfiddle.com </a>
The left hand box is called the Schema Panel and that is where you create your data table. The right hand box is called the Query Panel and that is where you access the data you created on the left. In this beginner section, the data will be given so you can focus on creating queries and accessing the data. The [advanced SQL section](SQLAdvanced.md) of this workshop will go more in depth about database table creation.

To begin, click [on this SQLFiddle link](http://sqlfiddle.com/#!18/ccca2) to open up the sql text editor that is already set up to create a data table. <b>Make sure that you are under MS SQL Server 2017 on the top, then press the "Build Schema" button. </b> If the code on the left hand side box does not appear, copy and paste the code below. The code creates a new table called "Students" that has four attributes: name, id, major, and year. Then we add new Student data into the table.


```
CREATE TABLE Students
    ([name] varchar(13), [id] int, [major] varchar(30), [year] varchar(10))
;


INSERT INTO Students
    ([name], [id], [major], [year])
VALUES
    ('Dillion', 420, 'Architecture', 'Senior'),
    ('Adam', 420, 'Architecture', 'Senior'),
    ('Zack', 420, 'Architecture', 'Senior'),
    ('Bob', 101, 'Biology', 'Freshman'),
    ('Bob', 102, 'Biology', 'Freshman'),
    ('Caroline', 222, 'Computer Science', 'Sophomore'),
    ('Dylan', 132, 'Dentistry', 'Freshman'),
    ('Eveline', 309, 'Economics', 'Junior'),
    ('Frank', 400, 'Forensic Science', 'Senior'),
    ('George', 339, 'Geology', 'Junior');
```

#### SELECT
The SELECT statement is the most common statement in SQL, fetching data from a database. SELECT can fetch the entire data table or specific data by defining rules. Write in the following code in the query panel on the right and click on the "Run SQL" button to see the output on the bottom. </br>
The ```*``` means to fetch *everything* from the table called Students.

```
SELECT * FROM Students;
```

To fetch certain attributes of each record, replace the ```*``` with column names separated by commas, like so:
```
SELECT name, id FROM Students;
```

#### SELECT DISTINCT
The DISTINCT statement is used with the SELECT statement. Tacking on DISTINCT after SELECT means to fetch data that is unique (ignore duplicated values).
Update your SELECT statement so that the query outputs only the unique names from the Students table.

#### WHERE
The WHERE statement is used to filter data using conditions. Only data that satisfies the conditions in the WHERE clause will be fetched. Comparison, arithmetic, bitwise, and logical operators can be used to set conditions. For example, the following code will fetch all students who are Seniors:
```
SELECT * FROM Students
WHERE year='Senior';
```

Using the *id* column, use the where clause with only one conditional statement to retrieve all students who are either Freshmen or Sophomores.

Comparison, arithmetic and bitwise operators are the same in SQL like in other programming language. (Ex. ```<=```, ```+```, ```&```). In SQL, ```<>``` is another way to write not equals to ```!=```. Logical operators are keywords and they are fully typed.

#### Logical Operators
* ```AND``` - if all conditions true
* ```OR``` - of one of the conditions is true
* ```NOT``` - if conditions are not true
```
SELECT DISTINCT * FROM Students
WHERE NOT id < 300 OR major='Architecture';
```
* ```IN``` - if condition is in one of these specific values; a shorthand for OR statements
```
SELECT * FROM Students
WHERE id IN (101, 222, 309);
```
* ```BETWEEN``` - if condition is in between a range (inclusive)
```
SELECT * FROM Students
WHERE id BETWEEN 200 AND 300;
```
* ```LIKE``` - if condition follows a pattern (not case sensitive)
    - ```%``` - represents zero or more characters
    - ```_``` - represents a single character

  ```
  -- if name of student ends with an 'e'
  ... WHERE name LIKE '%e';

  -- if name of student has an 'o' in their name
  ... WHERE name LIKE '%o%';

  -- if the second letter of student's major is an 'o'
  ... WHERE major LIKE '_o%';

  ```

### Aggregate Functions
Aggregate functions are functions that combine values of data. The three main aggregate functions are COUNT, AVG, and SUM.
* ```COUNT``` - returns the number of rows that satisfy certain conditions
* ```AVG``` - returns the average of numbers of a column
* ```SUM``` - returns the sum of numbers of a column


### ORDER BY
The ORDER BY keyword sorts the fetched data in ascending order by default. To sort in descending order, tack on ```DESC``` at the end of the clause. The following code will fetch all data and print them out by id in ascending order.

```
SELECT * FROM Students
ORDER BY id;
```

The following code will fetch all data and print them out by id in descending order, then by major in ascending order if any of the rows have the same id values. For example, notice that for id = 420 the rows are in order by ascending name as well (Adam, Dillion, Zack).
```
SELECT * FROM Students
ORDER BY id DESC, name;
```

### GROUP BY
The GROUP BY keyword combines identical data into groups. This statement is usually used with aggregate functions. The following code counts how many students there are in each year (group), then prints them out in ascending order by number of students in each year.

```
SELECT COUNT(id), year FROM Students
GROUP BY year
ORDER BY COUNT(id);
```

GROUP BY always comes before ORDER BY

### HAVING
The HAVING keyword is similar to the WHERE keyword, but it can use aggregate functions. The following code counts how many students are in each year and only prints out the number of students and their year if the number of students is greater than 2.

```
SELECT COUNT(id) FROM Students
GROUP BY year
HAVING COUNT(id) > 2;
```

## Exercise
Here is a library dataset that holds information about books. Here is the [SQLFiddle](http://sqlfiddle.com/#!18/11e678) with the dataset created, or you can copy the code below. Perform a few operations on this to see how you can use the SQL queries you've learned in this section to retrieve data.

```
CREATE TABLE Books

    ([author] varchar(100), [title] varchar(100), [pages] int, [genre] varchar(100));

INSERT INTO Books
    ([author], [title], [pages], [genre])

VALUES
    ('Drew Harper', 'Epic Gamer Moves', 200, 'academic'),
    ('AJ Stensland', 'How To Hack', 350, 'mystery'),
    ('Junhson Jean-Baptiste', 'Cooking with Junhson', 999, 'necessary'),
    ('Colin Fiutak', 'The Art of the KD Tree', 420, 'fiction'),
    ('Theresa Gundel', 'Fearless Leadership', 87, 'must-read'),
    ('Maeve Farrell', 'Buff Kirby', 100, 'nonfiction'),
    ('Alison Garrity', 'Learn Programming', 5, 'short story')

```

Here are some exercises to try on this data:
* Find the sum of all of the pages in the books.
* Select all books where by genres end in a 'y'.
* If a book has less than or equal to 100 pages and the authors name starts with 'A', retrieve the tiles.
* Retrieve only book titles in ascending order.

## Next Steps

Go onto the next portion of SQL to learn more about intermediate SQL like joins -- [SQL Intermediate](SQLIntermediate.md)
