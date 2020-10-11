# Advanced SQL
## Overview

### What You'll Learn
In this section, you'll learn:

1. How to create and manage database tables
  * Create
  * Drop
  * Insert Into
  * Update
2. What stored procedures are

### Prerequisites

1. [Beginner](SQLBeginner.md) and [Intermediate](SQLIntermediate.md) SQL

### Introduction

Welcome to the advanced section of SQL! In the previous sections, we covered queries and in-depth information
on select statements. Now, we will focus on how to manage the tables that were created for the examples from
the prior sections. This section will cover creating tables, dropping tables, inserting into tables, and
updating values stored within tables. Follow along using [SQL Fiddle](http://sqlfiddle.com).

## Database Table Creation and Management

### Create Table
In the examples prior, we used two tables: suppliers and orders to demonstrate how the various joins work.
In order to create the tables that we created queries for, we need to use the ```CREATE TABLE``` function.
The code for creating the tables from the examples is below:

```
CREATE TABLE suppliers
    ([supplier_id] int, [supplier_name] varchar(100))
;

...

CREATE TABLE orders
    ([order_id] int, [supplier_id] int, [order_date] date)
;

...
```

The format of the ```CREATE TABLE``` function is as follows, "suppliers" or "orders" is the name of the table,
the values in the parenthesis are a comma separated list specifying the name of the column in brackets accompanied
with a type that the data in the column will be. For example, we see [supplier_id] int, this will be a column of
integer values representing supplier_ids. In SQL, strings are represented as ```varchar(x)``` where x is the number
of characters in the string. Now that we have a table, we need to learn how to delete the table, insert data into
the table, and update data in the table.

## Drop Table
The DROP TABLE statement is used to delete an existing table in a database. <b>Be careful when dropping a table.
Deleting a table will result in loss of complete information stored in the table!</b>

```
CREATE TABLE suppliers

...

DROP TABLE suppliers
```

By calling drop table on suppliers, the table suppliers we created will be deleted and all information in the table
will be deleted. It is important to ensure that this function is not performed on an essential table and that all
tables are backed up in the event that an accident or intrusive event occurs.

## Insert Into
Now that we have our suppliers and orders table, we want to be able to populate the tables with information that
we currently have. In order to do this, we need to use the ```INSERT INTO``` function. The ```INSERT INTO``` statement
is used to insert new records into a table.

```
CREATE TABLE suppliers
    ([supplier_id] int, [supplier_name] varchar(100))
;

INSERT INTO suppliers
    ([supplier_id], [supplier_name])
VALUES
    ('10000','IBM'),
    ('10001','Hewlett Packard'),
    ('10002','Microsoft'),
    ('10003','NVIDIA')
;

CREATE TABLE orders
    ([order_id] int, [supplier_id] int, [order_date] date)
;

INSERT INTO orders
    ([order_id], [supplier_id], [order_date])
VALUES
    ('500125','10000','2003/05/12'),
    ('500126','10001','2003/05/13'),
    ('500127','10004','2003/05/14')
;
```

The format of the ```INSERT INTO``` function is as follows, "suppliers" or "orders" is the name of the table and
the values in the parenthesis are a comma separated list specifying the name of the columns in brackets. After this,
we must specific ```VALUES``` which contains a list of single-quoted values surrounded by parenthesis which contain
the values to be inserted into the columns specified in the brackets above. For example, in the suppliers table,
`('10000','IBM')` indicates that "<b>10000</b>" will be inserted into the ```supplier_id``` column and "<b>IBM</b>" will be
inserted into the ```supplier_name``` column. By running the above code in the schema portion of SQL Fiddle, we will now
have created a table which can be accessed using the queries from the previous sections.

## Update
Now that we have populated two tables with data, how would you go about updating the values in the table? The ```UPDATE``` statement
is used to modify the existing records in a table.

```
UPDATE suppliers
SET supplier_name = 'HackBU'
WHERE supplier_id = 10000;

SELECT * FROM suppliers;
```

**Be careful when updating records in a table! Notice the `WHERE` clause in the `UPDATE` statement. The `WHERE` clause specifies which record(s) that should be updated. If you omit the `WHERE` clause, all records in the table will be updated!**

The format of the ```UPDATE``` function is as follows, "suppliers" is the name of the table, "supplier_name = 'HackBU'" is the change
to be made when the ```WHERE``` condition is ```true```, and "supplier_id = 10000" is the condition that must be true in order to
update the value(s) in the table. Multiple columns can be set in the second line of the update function and multiple conditions can
exist in the third line which specifies the condition for where to update values.

## Stored Procedures
Check out <b>Stored Procedures</b> online! Stored procedures are widely used to process calls to databases in industry
using APIs. For example, you can write a C# application which has an API that enables you to make calls to a database to
retrieve data or to update data in various database tables.

Resources:
* [Microsoft Documentation](https://docs.microsoft.com/en-us/sql/relational-databases/stored-procedures/create-a-stored-procedure?view=sql-server-2017)
* [w3schools](https://www.w3schools.com/sql/sql_stored_procedures.asp)
* [Tutorial Gateway](https://www.tutorialgateway.org/stored-procedures-in-sql/)

## Exercise
Now that you have completed all of the SQL sections, try creating your own database tables on [SQL Fiddle](http://sqlfiddle.com) and applying the
concepts from each of the difficulty levels to your own data!

## Next Steps

Now that you've become familiar with SQL syntax and queries, check out the [Python/MySQL section](https://colab.research.google.com/github/HackBinghamton/DataScienceWorkshop/blob/master/DataEngineering/PythonMySQL.ipynb) of this workshop to learn how to use SQL queries in Python.
