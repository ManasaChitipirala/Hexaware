# SQL Assignment

# Task:1. Database Design:

### 1.1 Create the database named "TechShop"
~~~sql
create database TechShop;
use Techshop;
~~~

### 1.2 Define the schema for the Customers, Products, Orders, OrderDetails and Inventory tables based on the provided schema.
##### Customers table
~~~sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Email VARCHAR(100) UNIQUE,
    Phone VARCHAR(20),
    Address VARCHAR(255)
);
~~~

##### Products table
~~~sql
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    Description TEXT,
    Price DECIMAL(10, 2)
);
~~~

##### Orders table
~~~sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    TotalAmount DECIMAL(10, 2),
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
~~~

##### OrderDetails table
~~~sql
CREATE TABLE OrderDetails (
    OrderDetailID INT PRIMARY KEY,
    OrderID INT,
    ProductID INT,
    Quantity INT,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);
~~~

##### Inventory table
~~~sql
CREATE TABLE Inventory (
    InventoryID INT PRIMARY KEY,
    ProductID INT,
    QuantityInStock INT,
    LastStockUpdate DATE,
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);
~~~


### 1.3. Create an ERD (Entity Relationship Diagram) for the database.
![ERD](<Screenshot (240).png>)

### 1.4.Create appropriate Primary Key and Foreign Key constraints for referential integrity.
~~~sql

create table customers
(
  CustomerID  int Primary Key,
  FirstName varchar(30),
  LastName varchar(30),
  Email varchar(30),
  Phone varchar(30),
  Address varchar(30)
);

create table products
(
   ProductID int Primary Key,
   ProductName varchar(30),
   Description varchar(50),
   Price numeric(9,2)
);

create table orders
(
   OrderID int Primary Key,
   CustomerID int,
   OrderDate varchar(30),
   TotalAmount numeric(9,2),
   foreign key(customerid) references customers(customerid) on delete cascade
);

create table orderdetails
(
  OrderDetailID int Primary Key,
  OrderID int,
  ProductID int,
  Quan tity int,
  foreign key(orderid) references orders(orderid) on delete cascade,
  foreign key(productid) references products(productid) on delete cascade
);

create table inventory
(
  InventoryID int Primary Key,
  ProductID int,
  QuantityInStock int,
  LastStockUpdate varchar(30),
  foreign key(productid) references products(productid)
);
~~~


### 1.5. Insert at least 10 sample records into each of the following tables.

##### a. Customers

~~~sql
use Techshop;

insert into customers(customerid,firstname,lastname,phone,email,address)
values(1,'Manasa','Reddy','9903285090','manasareddyc90@gmail.com','Chittoor'),
(2,'Teddy','Girl','9373592389','Teddy2715@gmail.com','Tirupati'),
(3,'Mandy','C','1239813681','mandy1527@gmail.com','Hyderabad'),
(4,'Akki','Ram','9312345678','akkiram@gmail.com','Madanapalli'),
(5,'Bikki','Ram','9876543210','bikki123@gmail.com','Pgr'),
(6,'Kumar','Reddy','6303567085','eshu1415@gmail.com','Kadapa'),
(7,'Sandy','Eswar','5463276459','sandyeswar@gmail.com','Kurnool'),
(8,'Sanju','Teju','8610104686','Sanjuteju@gmail.com','kakinada'),
(9,'Chintu','Sai','6303544592','chintusai@gmail.com','chennai'),
(10,'Aadya','Chinni','8934583019','aadyachinni@gmail.com','Vizag');

~~~

##### b. Products

~~~sql

insert into products(productid,productname,description,price)
values(1,'Laptop','Asus',75000),
(2,'Smartphone','Iqoo',20000),
(3,'Smart watch','Apple',40000),
(4,'Mouse','Zebronics',800),
(5,'washing machine','samsung',20000),
(6,'Speakers','NU',4000),
(7,'Stove','Butterfly',5000),
(8,'Refrigerator','Whirlpool',80000),
(9,'Keyboard','zebronics',50000),
(10,'Earbuds','Realme',50000);

~~~

##### c. Orders

~~~ sql

insert into orders(orderid,customerid,orderdate)
values(1,2,'2022-01-23'),
(2,1,'2019-08-18'),
(3,1,'2020-09-5'),
(4,3,'2023-11-14'),
(5,10,'2021-10-02'),
(6,5,'2021-06-09'),
(7,8,'2024-05-17'),
(8,7,'2024-04-27'),
(9,3,'2020-1-15'),
(10,8,'2020-04-14');

~~~

##### d. OrderDetails

~~~sql

insert into orderdetails(orderdetailid,orderid,productid,quantity)
values(1,1,2,4),
(2,2,1,14),
(3,2,8,11),
(4,6,10,9),
(5,7,7,6),
(6,9,6,25),
(7,10,9,10),
(8,2,3,9),
(9,3,2,22),
(10,3,1,35);

~~~

##### e. Inventory

~~~sql

insert into inventory(inventoryid,productid,laststockupdate)
values(1,10,'2024-01-23'),
(2,1,'2023-10-12'),
(3,2,'2023-09-11'),
(4,3,'2023-08-10'),
(5,4,'2023-07-09'),
(6,5,'2023-06-08'),
(7,6,'2023-05-07'),
(8,7,'2023-04-06'),
(9,8,'2023-03-05'),
(10,9,'2023-02-04');

~~~

# Task 2: Select, Where, Between, AND, LIKE:

### 2.1. Write an SQL query to retrieve the names and emails of all customers.

~~~sql
select firstname,lastname,email from customers;
~~~

### 2.2. Write an SQL query to list all orders with their order dates and corresponding customer names.

~~~sql
select orderid,orderdate,firstname from orders,customers 
where orders.customerid=customers.customerid;
~~~

### 2.3.Write an SQL query to insert a new customer record into the "Customers" table. Include customer information such as name, email, and address.

~~~sql
insert into customers(customerid,firstname,lastname,email,address)
values (11,'xyz','abc','xyz@gmail.com','Hyderabad');
~~~

### 2.4. Write an SQL query to update the prices of all electronic gadgets in the "Products" table by increasing them by 10%.

~~~sql
update products set price = price+ ((10*price)/100);
select * from products;
~~~

### 2.5. Write an SQL query to delete a specific order and its associated order details from the "Orders" and "OrderDetails" tables. Allow users to input the order ID as a parameter.

~~~sql
delete from orders where orderid=2;
select * from orders;
select * from orderdetails;
~~~

### 2.6. Write an SQL query to insert a new order into the "Orders" table. Include the customer ID, order date, and any other necessary information.

~~~sql
insert into orders(orderid,customerid,orderdate,totalamount)
values(4,3,'2023-11-14',50000);
~~~

### 2.7. Write an SQL query to update the contact information (e.g., email and address) of a specific customer in the "Customers" table. Allow users to input the customer ID and new contact information.

~~~sql
update customers set email='akkiram123@gmail.com',address='AndhraPradesh' where customerid=4;
select * from customers;
~~~

### 2.8. Write an SQL query to recalculate and update the total cost of each order in the "Orders" table based on the prices and quantities in the "OrderDetails" table.

~~~sql
update Orders
set TotalAmount =
(select (od.Quantity * p.Price) as TotalAmount from Products p
join OrderDetails od on p.ProductID = od.ProductID where
od.OrderID = Orders.OrderID);


select * from orders;

select * from orderdetails;
~~~

### 2.9. Write an SQL query to delete all orders and their associated order details for a specific customer from the "Orders" and "OrderDetails" tables. Allow users to input the customer ID as a parameter.

~~~sql
delete from orders where customerid=3;
select * from orders;
select * from orderdetails;
~~~

### 2.10. Write an SQL query to insert a new electronic gadget product into the "Products" table, including product name, category, price, and any other relevant details

~~~sql
insert into products(productid,productname,description,price)
values(11,'Laptop','used for technical purpose',80000);
~~~

### 2.11. Write an SQL query to update the status of a specific order in the "Orders" table (e.g., from "Pending" to "Shipped"). Allow users to input the order ID and the new status.

~~~sql
alter table orders add column status varchar(30);
update orders set status='pending' ;
update orders set status='shipped' where orderid in ( 3,4,5,6);
select * from orders;
~~~

### 2.12. Write an SQL query to calculate and update the number of orders placed by each customer in the "Customers" table based on the data in the "Orders" table.
~~~sql
--By creating a new column in the Customers Table

alter table Customers
add NoofOrders int;

update Customers
set NoofOrders = (select count(OrderId) from Orders where Orders.CustomerID = Customers.CustomerId);

-- Without Creating a new column

select CustomerId, count(OrderId) as NoofOrders from Orders group by CustomerID;
~~~

# Task 3

### 3.1. Write an SQL query to retrieve a list of all orders along with customer information (e.g., -- customer name) for each order.

~~~sql
select orders.orderid,customers.* from orders 
inner join customers 
on orders.customerid = customers.customerid
group by orders.orderid;

select orderid,firstname from customers,orders where orders.customerid=customers.customerid;
~~~

### 3.2. Write an SQL query to find the total revenue generated by each electronic gadget product.

~~~sql
select ProductName, (od.Quantity * p.Price)
as TotalRevenue from Products p inner join OrderDetails od
on p.ProductID = od.ProductID;
~~~

### 3.3. Write an SQL query to list all customers who have made at least one purchase. Include their names and contact information.
~~~sql
select FirstName, LastName, Email, Address from Customers inner join Orders on Customers.CustomerID = Orders.CustomerID;
~~~

### 3.4. Write an SQL query to find the most popular electronic gadget, which is the one with the highest total quantity ordered. Include the product name and the total quantity ordered.

~~~sql
select ProductName, Quantity from Products inner join
( select top 1 Quantity, ProductID from OrderDetails order by Quantity desc ) as i
on Products.ProductID = i.ProductID;
~~~

### 3.5. Write an SQL query to retrieve a list of electronic gadgets along with their corresponding categories.
~~~sql
select productname,description from products;
~~~

### 3.6. Write an SQL query to calculate the average order value for each customer. Include the customer's name and their average order value.

~~~sql
select * from orders;
select * from customers;
select customers.customerid, sum( orders.totalamount/customers.number_orders ) as average_order_value from customers
inner join orders
on customers.customerid = orders.customerid
group by customers.customerid;
~~~

### 3.7. Write an SQL query to find the order with the highest total revenue. Include the order ID, customer information, and the total revenue.

~~~sql
select top 1 FirstName, OrderID, TotalAmount from Customers inner join Orders
on Customers.CustomerID = Orders.CustomerID order by TotalAmount desc;
~~~

### 3.8. Write an SQL query to list electronic gadgets and the number of times each product has been ordered.

~~~sql
select pr.ProductName, Quantity as NoOfTimes from Products pr inner join OrderDetails od on
pr.ProductID = od.ProductID;
~~~

### 3.9. Write an SQL query to find customers who have purchased a specific electronic gadget product. Allow users to input the product name as a parameter

~~~sql
select customers.firstname ,products.productname
from  orders inner join orderdetails 
on orders.orderid= orderdetails.orderid inner join products
on products.productid = orderdetails.productid inner join customers
on customers.customerid = orders.customerid;
~~~

### 3.10. Write an SQL query to calculate the total revenue generated by all orders placed within a specific time period. Allow users to input the start and end dates as parameters

~~~sql
select * from orders;
select sum(orders.totalamount) 
from  orders where orders.orderdate between '2020-01-01' and '2023-12-30';
~~~

# Task-4:
### 4.1. Write an SQL query to find out which customers have not placed any orders.

~~~sql
select FirstName, LastName from Customers where CustomerID not in (select CustomerID from Orders);
~~~

### 4.2. Write an SQL query to find the total number of products available for sale.
~~~sql
select count(ProductName) as NumberOfProducts from Products where ProductID in
(select ProductID from Inventory where QuantityInStock > 0);
~~~

### 4.3. Write an SQL query to calculate the total revenue generated by TechShop.
~~~sql
select * from orders;
select sum(totalamount) as total_rvenue from orders;
~~~

### 4.4. Write an SQL query to calculate the average quantity ordered for products in a specific category. Allow users to input the category name as a parameter.
~~~sql
declare @n int = 1;

select Category, avg(Quantity) as AvgOrder from
(select p.Category, od.Quantity from Products p join OrderDetails od on
p.ProductID = od.ProductID where p.Category = @n) as i
group by Category;
~~~

### 4.5. Write an SQL query to calculate the total revenue generated by a specific customer. Allow users to input the customer ID as a parameter

~~~sql
Declare @c int = 10;

select sum(TotalAmount) as TotalRevenue from Orders where CustomerID = @c;
~~~

### 4.6. Write an SQL query to find the customers who have placed the most orders. List their names and the number of orders they've placed

~~~sql
select * from customers;
select firstname,number_orders from customers where number_orders = (select max(number_orders) from customers);
~~~

### 4.7. Write an SQL query to find the most popular product category, which is the one with the highest total quantity ordered across all orders
~~~sql
select p.productname,p.description,o.quantity 
from products p inner join orderdetails o
on p.productid = o.productid
order by o.quantity desc limit 1;

select productname,description,quantity from products,orderdetails where quantity =  (select max(quantity) from orderdetails);
~~~

### 4.8. Write an SQL query to find the customer who has spent the most money (highest total revenue) on electronic gadgets. List their name and total spending.

~~~sql
select c.firstname , o.totalamount 
from customers c inner join orders o
on c.customerid=o.customerid
order by o.totalamount desc limit 1;
~~~

### 4.9. Write an SQL query to calculate the average order value (total revenue divided by the number of orders) for all customers.

~~~sql
select customers.customerid, sum( orders.totalamount/customers.number_orders ) as average_order_value from customers
inner join orders
on customers.customerid = orders.customerid
group by customers.customerid;
~~~

### 4.10. Write an SQL query to find the total number of orders placed by each customer and list their names along with the order count

~~~sql
select customers.customerid,customers.firstname,count(orders.orderid) as number_orders from customers inner join orders 
on customers.CustomerID = orders.CustomerID 
group by customers.CustomerID 
order by customers.CustomerID;
~~~
