## 
Data Definition Language (DDL)
- create, alter, drop
Data Manupulation Language (DML)
- insert, update, delete
Data Query Language (DQL)
- select
Data Control Language (DCL)
- 

## Numeric Data Types
$ mysql
> CREATE DATABASE cm_devices;
> USE cm_devices;
> CREATE TABLE devices(deviceID INT, deviceName varchar(50), price DECIMAL);
> SHOW COLUMNS FROM devices;
> CREATE TABLE stock(deviceID INT, quantity INT, totalCost DECIMAL);
> SHOW TABLES;

## String Data Types
> CREATE DATABASE customers;
> CREATE TABLE customers (username CHAR(9), fullName VARCHAR(100), email VARCHAR(255));
> CREATE TABLE feedback (feedbackID CHAR(8), feedbackType VARCHAR(100), feedbackComment TEXT(500));

## Working with Default Values

> CREATE TABLE address (customerID INT NOT NULL, street VARCHAR(255), postcode VARCHAR(10), town VARCHAR(30) DEFAULT "Harrow");
> DROP TABLE address;
> CREATE TABLE address (customerID INT NOT NULL, street VARCHAR(255), postcode VARCHAR(10) DEFAULT "HA97DE", town VARCHAR(30) DEFAULT "Harrow");
> CREATE TABLE invoice (customerName VARCHAR(50), orderDate DATE, quatity INT, price DECIMAL);
> CREATE TABLE customers (customerName VARCHAR(50), accountNumber INTEGER, phoneNumber INTEGER, email VARCHAR(255));


> CREATE DATABASE db_name;
> DROP DATABASE db_name;

> CREATE TABLE table_name (column_name1 type, column_name1 type)
> ALTER TABLE table_name ADD (column_name1 type)

> INSERT INTO table_name (column_name1, colum_name2) VALUES (value1, value2), (value1, value2), (value1, value2);

> create table customers(customerID int, customerName varchar(50), customerAddress varchar(255));
> insert into customers(customerID, customerName, customerAddress) VALUES(1, "Jose", "31 Amsterdan Ave.");
> select * from customers;

> SELECT column FROM table;
> INSERT INTO target_table_name (column_name1) SELECT column_from1 FROM source_table_name;


> INSERT INTO table_name (colum1, colum2, colum3) VALUES (value1, value2, value3);
> ALTER TABLE table_name ADD (column4 datatype(size));
> UPDATE table_name SET colum_name="value" WHERE ID = 02;
> DELETE FROM table_name WHERE ID = 03; 
> SELECT colum1, colum2 FROM table_name;
> SELECT * FROM table_name;
> TRYNCATE TABLE table_name;     # just empty the table
> DROP TABLE table_name

## Updating and Deleting
> UPDATE table_name SET column1 = "new_value1", column2 = "new_value2" WHERE ID = 3;
> UPDATE table_name SET column1 = "new_value1", column2 = "new_value2" WHERE column3 = "value3";CRE

> DELETE FROM table_name  WHERE ID = 3;
> DELETE FROM table_name  WHERE column3 = "value3";
> DELETE FROM table_name;
> TRUNCATE TABLE customers;

INSERT INTO customers (customerID, customerName, customerAddress) 
VALUES 
(1, "Jack", "115 Old street Belfast"),
(2, "James", "24 Carlson Rd London"),
(4, "Maria", "5 Fredrik Rd, Bedford"),
(5, "Jade", "10 Copland Ave Portsmouth"),
(6, "Yasmine", "15 Fredrik Rd, Bedford"),
(3, "Jimmy", "110 Copland Ave Portsmouth");

## Arithmetic operators
# Arithmetic operators can be used in the SELECT clause as well as in the WHERE clause in a SQL SELECT statement. When an operator is used in the WHERE clause, it’s intended to perform the operations on specific rows only.
# All arithmetic operators are used on numerical operands for performing:
- Addition 
- Subtraction 
- Multiplication 
- Division 
- Modulus 

> SELECT column_name1 + column_name2 FROM table_name; 


## Comparison Operators

Operator 	What it does
=		Checks for equality
<> or !=	Checks for not inequality
>		Check if something is greater than
>=		Check if something is greater than or equal
<		Check if something is less than
<=		Check if something is less than or equal

> SELECT * FROM employee WHERE salary + allowance = 25000; 
> SELECT * FROM employee WHERE salary < 24000;
> SELECT * FROM employee WHERE salary <> 24000;    -- Not equal

## Logical Operators

Operator	Description

ALL		Used to compare a single value to all the values in another value set.
AND		Allows for the existence of multiple conditions in an SQL statement's WHERE clause.
ANY		Used to compare a value to any applicable value in the list as per the condition.
BETWEEN	Used to search for values that are within a set of values, given the minimum value and the maximum value.
EXISTS	Used to search for the presence of a row in a specified table that meets a certain criterion.
IN		Used to compare a value to a list of literal values that have been specified.
LIKE		Used to compare a value to similar values using wildcard operators.
NOT		Reverses the meaning of the logical operator with which it is used. For example: NOT EXISTS, NOT BETWEEN, NOT IN, etc. This is a negate operator.
OR		Used to combine multiple conditions in an SQL statement's WHERE clause.
IS NULL	Used to compare a value with a NULL value.
UNIQUE	Searches every row of a specified table for uniqueness (no duplicates).

SELECT column1, column2 FROM table_name WHERE [condition1] AND [condition2]; 

## SORTING AND FILTERING
# ORDER BY
# WHERE (BETWEEN, LIKE, IN)
# DISTINC

SELECT column1, column2 FROM table_name ORDER BY column1 ASC, column2 DESC;  -- Default is ASC


SELECT DISTINCT BillingCountry FROM invoices ORDER BY BillingCountry; 


CREATE DATABASE Chinook;
USE Chinook;
CREATE TABLE Customer (CustomerId INT NOT NULL, FirstName VARCHAR(40) NOT NULL, LastName VARCHAR(20) NOT NULL, Company VARCHAR(80), Address VARCHAR(70), City VARCHAR(40), State VARCHAR(40), Country VARCHAR(40), PostalCode VARCHAR(10), Phone VARCHAR(24), Fax VARCHAR(24), Email VARCHAR(60) NOT NULL, SupportRepId INT, CONSTRAINT PK_Customer PRIMARY KEY (CustomerId));

## Aggregate functions (count, avg, max)

SELECT COUNT(DISTINCT country) FROM customers; 

## Creating schemas

> CREATE DATABASE restaurant;
> CREATE TABLE tbl( 
    table_id INT, 
    location VARCHAR(255), 
    PRIMARY KEY (table_id)); 
> CREATE TABLE waiter( 
    waiter_id INT, 
    name VARCHAR(150), 
    contact_no VARCHAR(10), 
    shift VARCHAR(10), 
    PRIMARY KEY (waiter_id)); 
> CREATE TABLE table_order( 
    order_id INT, 
    date_time DATETIME, 
    table_id INT, 
    waiter_id INT, 
    PRIMARY KEY (order_id), 
    FOREIGN KEY (table_id) REFERENCES tbl(table_id), 
    FOREIGN KEY (waiter_id) REFERENCES waiter(waiter_id)); 
> CREATE TABLE customer( 
    customer_id INT, 
    name VARCHAR(100), 
    NIC_no VARCHAR(12), 
    contact_no VARCHAR(10), 
    PRIMARY KEY (customer_id)); 
> CREATE TABLE reservation( 
    reservation_id INT, 
    date_time DATETIME, 
    no_of_pax INT, 
    order_id INT, 
    table_id INT, 
    customer_id INT, 
    PRIMARY KEY (reservation_id), 
    FOREIGN KEY (order_id) REFERENCES table_order(table_id), 
    FOREIGN KEY (table_id) REFERENCES tbl(table_id), 
    FOREIGN KEY (customer_id) REFERENCES customer(customer_id)); 
> CREATE TABLE menu( 
    menu_id INT, 
    description VARCHAR(255), 
    availability INT, 
    PRIMARY KEY (menu_id)); 
> CREATE TABLE menu_item( 
    menu_item_id INT, 
    description VARCHAR(255), 
    price FLOAT, 
    availability INT, 
    menu_id INT, 
    PRIMARY KEY (menu_item_id), 
    FOREIGN KEY (menu_id) REFERENCES menu(menu_id)); 
> CREATE TABLE order_menu_item( 
    order_id INT, 
    menu_item_id INT, 
    quantity INT, 
    PRIMARY KEY (order_id,menu_item_id), 
    FOREIGN KEY (order_id) REFERENCES table_order(order_id), 
    FOREIGN KEY (menu_item_id) REFERENCES menu_item(menu_item_id)); 

## Types of relationships
# One to many
# One to one
# many to many

CREATE DATABASE automobile; 
CREATE TABLE vehicle( vehicleID varchar(10), ownerID varchar(10), plateNumber varchar(10), phoneNumber INT);
CREATE TABLE Owner(ownerID VARCHAR(10), ownerName VARCHAR(50), ownerdrerss  VARCHAR(255), PRIMARY KEY (ownerID));
ALTER TABLE vehicle ADD FOREIGN KEY (ownerID) REFERENCES owner (ownerID);
