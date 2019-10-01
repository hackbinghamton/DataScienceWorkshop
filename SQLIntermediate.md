# Intermediate SQL
## Overview
* SELECT Statements using JOIN
  * INNER JOIN (aka Simple Join)
  * LEFT OUTER JOIN (aka LEFT JOIN)
  * RIGHT OUTER JOIN (aka RIGHT JOIN)
  * FULL OUTER JOIN (aka FULL JOIN)
* Functions
  * String
  * Numeric
  * Mathematical
  * Date
  * Conversion

## SELECT Statements using JOIN
Now that you are familiar with using select statements to retrieve specific data from a table,
we are going to continue with more advanced select statements. You might ask yourself, what if
I have data stored in multiple tables that I want to use at the same time? For example, say
for instance that you have a table called suppliers and a table called orders. The suppliers
table contains columns ```supplier_id``` and ```supplier_name```. On the other hand, the orders
table contains 3 columns: ```order_id```, ```supplier_id```, and ```order_date```. How would you
go about retrieving a combination of data from the suppliers table and the orders table?

```JOIN``` is used to retrieve data from not one, but multiple tables. There are four different
types of JOINs and each will be shown below with an example.

## INNER JOIN
```INNER JOIN``` is the most common type of join. Inner joins are used to combine all rows from
multiple tables where a specific join condition is met.

<b>What is a join condition?</b>
A join condition is the specification of which column should be used to link the two tables
together. In our example above, we notice that both the suppliers table and the orders table
contain a column called ```supplier_id```. We can use this column as the join condition to
combine the information from both tables into one table.

The result of using an inner join on the ```supplier_id``` would display all rows where a
```supplier_id``` from the suppliers table matches the ```supplier_id``` from the orders table.
The image below illustrates the intersection of the data that would be returned from this join.

<p align="center">
  <img src="images/inner_join.gif"/>
</p>

Now, lets try it out!

To begin, click [here](http://sqlfiddle.com/#!18/79aeb) to open up the sql text editor with our created data table. <b>Make sure that you are under MS SQL Server 2017 on the top, then press the "Build Schema" button. </b> If the code on the left hand side box does not appear, copy and paste the code below. The code creates two tables: "suppliers" and "orders" from our example above.

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
|    10000    |       IBM       | 2003/05/12 |
|    10001    | Hewlett Packard | 2003/05/13 |


## LEFT OUTER JOIN

<p align="center">
  <img src="images/left_outer_join.gif"/>
</p>

## RIGHT OUTER JOIN

<p align="center">
  <img src="images/right_outer_join.gif"/>
</p>

## FULL OUTER JOIN

<p align="center">
  <img src="images/full_outer_join.gif"/>
</p>

[Next: SQL Advanced](SQLAdvanced.md)
