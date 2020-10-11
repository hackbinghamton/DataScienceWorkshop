# Intermediate SQL
## Overview
### What You'll Learn
In this section you'll learn:
1. SELECT Statements using JOIN
    * INNER JOIN
    * LEFT OUTER JOIN
    * RIGHT OUTER JOIN
    * FULL OUTER JOIN

### Prerequisites
Before starting this section you should have an understanding of:
1. How to retrieve data in SQL - [Beginner SQL portion](SQLBeginner.md)

### Introduction
In this section, you will be introduced to `JOIN` statements. You will learn how they are used and
when each statement is applicable. In this section there are exercises to follow along with that use the included data set. You will use SQLFiddle to follow along.

## SELECT Statements using JOIN
Now that you are familiar with using select statements to retrieve specific data from a table,
we are going to continue with more advanced select statements. You might ask yourself, what if
I have data stored in multiple tables that I want to use at the same time? For example, say
for instance that you have a table called suppliers and a table called orders. The suppliers
table contains columns ```supplier_id``` and ```supplier_name```. On the other hand, the orders
table contains 3 columns: ```order_id```, ```supplier_id```, and ```order_date```. How would you
go about retrieving a combination of data from the suppliers table and the orders table?

`JOIN` is used to retrieve data from not one, but multiple tables. There are four different
types of JOINs and each will be shown below with an example.

## INNER JOIN
`INNER JOIN` is the most common type of join. Inner joins are used to combine all rows from
multiple tables where a specific join condition is met.

<b>What is a join condition?</b>
A join condition is the specification of which column should be used to link the two tables
together. In our example above, we notice that both the suppliers table and the orders table
contain a column called ```supplier_id```. We can use this column as the join condition to
combine the information from both tables into one table.

The result of using an inner join on the ```supplier_id``` would display all rows where a `supplier_id` from the suppliers table matches the ```supplier_id``` from the orders table.

The image below illustrates the intersection of the data that would be returned from this join.

<p align="center">
  <img src="images/inner_join.gif"/>
</p>

Now, lets try it out! To begin, click [here](http://sqlfiddle.com/#!18/79aeb) to open up the sql text editor with our created data table. <b>Make sure that you are under MS SQL Server 2017 on the top, then press the "Build Schema" button. </b> If the code on the left hand side box does not appear, copy and paste the code below. The code creates two tables: "suppliers" and "orders" from our example above.

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

Now, input the following select statement using inner join on the left. Before running it,
think about what the output table will look like. We said before that it will combine the
tables using the join condition and output the selected columns for all rows that have a
match from each table.

```
SELECT suppliers.supplier_id, suppliers.supplier_name, orders.order_date
FROM suppliers
INNER JOIN orders
ON suppliers.supplier_id = orders.supplier_id;
```

The result should be the following:

| supplier_id |  supplier_name  | order_date |
|:-----------:|:---------------:|:----------:|
|    10000    |       IBM       | 2003-05-12 |
|    10001    | Hewlett Packard | 2003-05-13 |


## LEFT OUTER JOIN
The second type of join is ```LEFT OUTER JOIN```. Left outer joins are used to combine all the rows from
the left-hand table with <b>only</b> the rows of the right-hand table that meet the specific join condition.

The result of using a left outer join on the ```supplier_id``` would display all the rows from suppliers and <b>only</b> the
rows from orders where the ```supplier_id``` from the suppliers table matches the ```supplier_id``` from the
orders table. The image below illustrates the intersection of the data that would be returned from this join.

<p align="center">
  <img src="images/left_outer_join.gif"/>
</p>

Your turn! Using the same tables from the previous join example above, run the following left outer join query below.
Again, what table do you think will be the result of this select statement? What happens if there is no match in the
right-hand table for a specific ```supplier_id``` from the left-hand table?

```
SELECT suppliers.supplier_id, suppliers.supplier_name, orders.order_date
FROM suppliers
LEFT OUTER JOIN orders
ON suppliers.supplier_id = orders.supplier_id;
```

The result should be the following:

| supplier_id |  supplier_name  | order_date |
|:-----------:|:---------------:|:----------:|
|    10000    |       IBM       | 2003-05-12 |
|    10001    | Hewlett Packard | 2003-05-13 |
|    10002    |    Microsoft    |   (null)   |
|    10003    |      NVIDIA     |   (null)   |

When there is no match in the right-hand table for a ```supplier_id``` in the left-hand table, the query inserts ```null```
for all data values for columns from the right-hand table that are unmatched.

## RIGHT OUTER JOIN
The third type of join is ```RIGHT OUTER JOIN```. Right outer joins are used to combine all the rows from
the right-hand table with <b>only</b> the rows of the left-hand table that meet the specific join condition.
This is the same interaction as ```LEFT OUTER JOIN``` except, it prioritizes the right-hand table as the table
to create the join on.

The result of using a right outer join on the ```supplier_id``` would display all the selected rows from orders and <b>only</b> the
rows from suppliers where the ```supplier_id``` from the orders table matches the ```supplier_id``` from the
suppliers table. The image below illustrates the intersection of the data that would be returned from this join.

<p align="center">
  <img src="images/right_outer_join.gif"/>
</p>

Your turn again! Using the same tables, run the following right outer join query below. Again, what table do you think will be the
result of this select statement? What happens if there is no match in the left-hand table for a specific ```supplier_id``` from the
right-hand table?

```
SELECT orders.order_id, orders.order_date, suppliers.supplier_name
FROM suppliers
RIGHT OUTER JOIN orders
ON suppliers.supplier_id = orders.supplier_id;
```
The result should be the following:

| order_id | order_date |  supplier_name  |
|:--------:|------------|:---------------:|
|  500125  | 2003-05-12 |       IBM       |
|  500126  | 2003-05-13 | Hewlett Packard |
|  500127  | 2003-05-14 |      (null)     |

## FULL OUTER JOIN
The final type of join is ```FULL OUTER JOIN```. Full outer joins are used to combine <b>all</b> the rows from
the left-hand table with <b>all</b> the rows of the right-hand table. This time, whenever there exists a join
condition that is not met, the unmatched values will be substituted with ```null``` values instead of being omitted.

The result of using a full outer join on the ```supplier_id``` would display all the rows from suppliers and all the
rows from orders where the ```supplier_id``` from the suppliers table matches the ```supplier_id``` from the
orders table. Additionally, all the values that are not matched from either the suppliers table or the order tables will
be substituted with ```null```. The image below illustrates the intersection of the data that would be returned from this join.


<p align="center">
  <img src="images/full_outer_join.gif"/>
</p>

Your turn! Using the same tables, run the following full outer join query below.
What table do you think will be the result of this select statement? What happens if the ```supplier_id``` does not correctly
match for the rows in either table?

```
SELECT suppliers.supplier_id, suppliers.supplier_name, orders.order_date
FROM suppliers
FULL OUTER JOIN orders
ON suppliers.supplier_id = orders.supplier_id;
```

The result should be the following:

| supplier_id |  supplier_name  | order_date |
|:-----------:|:---------------:|:----------:|
|    10000    |       IBM       | 2003-05-12 |
|    10001    | Hewlett Packard | 2003-05-13 |
|    10002    |    Microsoft    |   (null)   |
|    10003    |      NVIDIA     |   (null)   |
|    (null)   |      (null)     | 2003-05-14 |


## Exercise
Given the following data set, perform the following instructions to retrieve data. Here is the [SQLFiddle](http://sqlfiddle.com/#!18/850309) link.

```
CREATE TABLE winners
    ([winner_id] int, [entrant_id] int, [sport] varchar(100), [medal] varchar(100))
;

INSERT INTO winners
    ([winner_id], [entrant_id], [sport], [medal])
VALUES
    ('1', '500', 'Basketball', 'gold'),
    ('2', '201', 'Basketball', 'silver'),
    ('3', '343', 'Swimming', 'gold'),
    ('4', '332', 'Ultimate Frisbee', 'gold'),
    ('5', '101', 'Soccer', 'gold'),
    ('6', '189', 'Soccer', 'silver'),
    ('7', '176', 'Soccer', 'bronze')
;

CREATE TABLE entrants
    ([entrant_id] int, [name] varchar(100), [age] int, [gender] varchar(100))
;

INSERT INTO entrants
    ([entrant_id], [name], [age], [gender])
VALUES  
    ('101', 'Steven S', '20', 'male'),
    ('116', 'Maria M', '21', 'female'),
    ('126', 'Patrick P', '23', 'male'),
    ('176', 'Scott S', '21', 'male'),
    ('177', 'Annie A', '20', 'female'),
    ('189', 'Sherry S', '24', 'female'),
    ('190', 'Cammie C', '21', 'female'),
    ('201', 'Brian B', '22', 'male'),
    ('332', 'Uri F', '20', 'female'),
    ('343', 'Sarah S', '19', 'female'),  
    ('400', 'Benjamin B', '23', 'male')
;
```

* Perform a right join to retrieve common data between both data sets while also
  including all data from the right data set.
* Perform an inner join to retrieve all common data between the two sets.
* Perform an outer join to retrieve all data between both sets.

Now that you know how to retrieve data from tables, check out this fun [murder mystery SQL game](https://mystery.knightlab.com/) and find out who committed the crime! 

## Next Steps
Head onto our [SQL Advanced](SQLAdvanced.md) section of the workshop to learn how to create and manage tables.
