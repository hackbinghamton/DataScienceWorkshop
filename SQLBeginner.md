# Beginner SQL
## Overview
* Syntax
* Commenting
* SQL Statements
  * SELECT
  * SELECT DISTINCT
  * WHERE
  * Logical operators
    * AND
    * OR
    * NOT
    * ALL
    * ANY
    * SOME
    * EXISTS
    * BETWEEN
    * IN
    * LIKE
  * ORDER BY
  * GROUP BY
  * HAVING

## Syntax
Relational databases are represented as tables. Each table is identified by a name. In MS SQL, the names of tables are in quotes ```"tableName" ```. Tables are made up of rows (also called records) and columns.

SQL uses many keywords. Keywords are not case sensitive, but are conventionally uppercased. ```SELECT``` and ```select``` both work, but using uppercased letters for keywords is recommended.  

Semicolons are the standard way to separate SQL statements. Depending on the database system, having semicolons at the end may be optional. However, it is the standard and the recommended way to always end statements with semicolons.

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

To practice using SQL, this workshop will be using an online application called [sqlfiddle.com](http://sqlfiddle.com). The left hand box is called the Schema Panel and that is where you create your data table. The right hand box is called the Query Panel and that is where you access the data you created on the left. In this beginner section, the data will be given so you can focus on creating queries and accessing the data. The advanced SQL section of this workshop will go more in depth about database table creation. (add link).

To begin, click [here](http://sqlfiddle.com/#!18/cb380/1) to open up the sql text editor with an already created data table. <b>Make sure that you are under MS SQL Server 2017 on the top, then press the "Build Schema" button. </b> If the code on the left hand side box does not appear, copy and paste the code below. The code creates a new table called "Students" that has four attributes: name, id, major, and year. Then we add new Student data into the table.


```
CREATE TABLE Students
    ([name] varchar(13), [id] varchar(3), [major] varchar(30), [year] varchar(10))
;

INSERT INTO Students
    ([name], [id], [major], [year])
VALUES
    ('Adam', '420', 'Architecture', 'Senior'),
    ('Bob', '101', 'Biology', 'Freshman'),
    ('Caroline', '222', 'Computer Science', 'Sophomore'),
    ('Dylan', '132', 'Dentistry', 'Freshman'),
    ('Eveline', '309', 'Economics', 'Junior'),
    ('Frank', '400', 'Forensic Science', 'Senior'),
    ('George', '339', 'Geology', 'Junior')  
;

```

#### Select


```
SELECT * FROM Students;
```

[in progress]
