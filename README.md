------------------------------------------ Session 2 -------------------------------------------

drop database Northwind

-- how to create table

create table TestTable(
	ID int,
	UserName varchar(255),
	Address varchar(255),saasasa
	phoneNumber int,
	email varchar(100)
)

drop table TestTable
-- no change to any value
-- no casesensitive
-- DQL : select
-- * meaning all columns 
alter table TestTable
alter column Address varchar(15);

-- for adding new column after table creation
alter table Testtable
Add Email varchar(100)

--How to insert data from existing table
select * into newTable from TestTable
select Id, Username into newTable2 from TestTable

-- how to truncate table
select *  from TestTable;
truncate table TestTable

select * from newTable2
-- how to insert data in table
insert into TestTable values(1,'dumyUsername','address',12);
insert into TestTable (UserName,address) values ('user2','address');

create table TestTable(
	ID int,
	UserName varchar(255),
	Address varchar(255),
	phoneNumber int,
	email varchar(100)
)
insert into testTable values (2,'username','address',20200,'@gmail.com')
select * from TestTable
drop table TestTable

truncate table testTable 

delete from testTable

where id = 2

    ------------------------------------------- Session 3 -------------------------------------------


-- 1 to 500
-- string : ''
-- constraints : for validation purpose
create table TableName(
	id int  not null,
	name varchar(8000) not null,
	Constraint Unique_value unique (name,id)
)

--primary key : unique + not null | only one column in table

drop table TableName;

--how to add unique constraint to table
alter table TableName
Add Constraint Unique_value unique (name);

alter table TableName 
drop Constraint Unique_value

delete from TableName
where id = 1  and name = 'testname2'

insert into TableName values (3,'testname2')
select * from TableName

--create database
create database DatabaseName;

--to delete database
drop database DatabaseName;

--to modify database name
alter Database Northwind Modify name = SQLpractiseDatabase;
alter Database updated modify name = newDataname;

EXEC sp_renamedb 'Northwind' , 'UpdatedDataBase'  
EXEC sp_renamedb 'SQLpractiseDatabase' , 'updated'

--to select a database
use master

--create table
--insert
--alter table : add column, column datatype change
--how to update cell value


select * from Customers

--alter & update


-- for adding new column
alter table Customers
add Newcloumn varchar(500)

-- for changing column datatype
alter table Customers
alter column Newcloumn int

--truncate
--delete

drop table Customers

select * from Customers
--alter : column level
--update: row level

update Customers
Set CompanyName = 'newCompany Name'
where CustomerID = 'ALFKI'

--Constraints : limit 

     ------------------------------------------- Session  4 -------------------------------------------


--not null
--unique drop

create table DemoTable(
	Id int not null unique
)

select * from DemoTable
insert into DemoTable values (5),(6);

exec sp_help DemoTable


alter table DemoTable
alter column Id int null

alter table Demotable
drop constraint UQ__DemoTabl__3214EC06307FDA30


--rename database
exec sp_renamedb 'SQL_Lectures' , 'Updated_SQL_lectures'


use Northwind

-- to change table name using query
exec sp_rename 'DemoTable', 'NewTableName'



--The database could not be exclusively locked to perform the operation.

-- primary : not null & unique

create Table primaryKeyTable(
	ID int,
	name varchar(255),
	Age int,
	Constraint primary_key primary key (id)
)

alter table primarykeyTable
Add constraint primary_key primary key(id)

alter table primarykeyTable
drop constraint primary_key


create table foreignkeyTable(
	foreignkeyID int,
	Address varchar(255),
	Email varchar(200),
	--Constraint fk_key foreign key (foreignkeyID) references primarykeytable(Id)
)

alter table foreignkeyTable
add  Constraint fk_key foreign key (foreignkeyID) references primarykeytable(Id)

alter table foreignkeyTable
drop constraint fk_key


drop table foreignkeyTable

select * from primaryKeyTable
select * from foreignkeyTable

insert into foreignkeyTable (foreignkeyID) values (4);


-- during table creation
-- Alter table

alter table primaryKeyTable
Add constraint primary_key primary key(id,name)

alter table primarykeyTable
drop constraint primary_key

select * from primaryKeyTable
insert into primaryKeyTable values (4,'name1',10)

delete from primaryKeyTable
where id = 4


use Northwind

--primary key & foreign key : relationship between two tables

select * from updatedCategories
select * from Suppliers
select * from products
where CategoryID = 4

alter table updatedCategories
drop constraint PK_Categories

truncate table ForeignkeyTable


       ------------------------------------------- Session  5 -------------------------------------------



create table Foreignkey_table(
	Connected_Id int,

--1st way
constraint fk_connectid_id foreign key (Connected_ID) references Primarykey_table(ID)
)

select * from Foreignkey_table

insert into Foreignkey_table values (6),(1);

--2nd way
--alter table Foreignkey_table
--add constraint fk_connectid_id foreign key (Connected_ID) references Primarykey_table(ID)






-- foregin key : A relation between two table where froeign key table can only take value than are defind in primary table column.


create table Primarykey_table(
-- 1st way	
	ID int primary key,
-- 2nd way	
--	constraint pk_id primary key(ID)
)

select * from Primarykey_table

insert into Primarykey_table values (1),(2),(3),(4),(5);

--3rd way
--alter table primarykey_table
--add constraint pk_id primary key(ID)



-- copy
select Country into UserProvidedCountry from Customers
where Country like 'U%' or Country like 'G%' or Country like 'A%' ;

drop table UserProvidedCountry

select * from UserProvidedCountry


--3country , 100,200 
--user
--germary, france, berlin
select Country from Customers
where Country = 'Germany' or Country = 'France' or Country = 'Brazil' or Country = 'India'


-- sql tuples
select Country from Customers
--sub query
where Country in (select * from userProvidedCountry);


-- % : it can be any thing.
select country from Customers
where Country like 'B%'

use northwind

-- helps us to find only the unique records
select Distinct Country from Customers


       ------------------------------------------- Session  8 -------------------------------------------
				   
				   
create Table Default_testing(
	id int,
	age int,
	--first way
	address varchar(500) Default 'No address input',
	--2nd way
	constraint DF_address Default 'Value Updated' for address
)

exec sp_help Default_testing

alter table Default_testing
drop constraint DF__Default_t__addre__3D5E1FD2

--3rd way
alter table Default_testing
add constraint DF_address Default 'Value Updated' for address

select * from Default_testing

insert into Default_testing (id, age) values (1,10)

******************** Identity

select * from Identity_testing

insert into Identity_testing  values (20,'userName3')

alter table Identity_testing
add ID_updated int

update Identity_testing

alter table Identity_testing
drop column id
set ID_updated = id

exec sp_rename 'Identity_testing.ID_updated', 'id'

insert into Identity_testing  values (20,'userName3')

select * from Identity_testing

delete From Identity_testing
where id is null

         ------------------------------------------- Day 9 -------------------------------------------
select count(*)as count from Products

select * from Products 
where UnitPrice  Between 1 and 10

--and | or 

--

select *  from Products
--where UnitPrice in (select Min(UnitPrice) from Products)

Update Products
set UnitPrice = 2.50
where ProductID = 1

--Between
--Min
--Max
--Count
--Avg
--Sum

select Min(UnitPrice) from Products

           ------------------------------------------- Day 10 -------------------------------------------
--store procedure : ready made query

create Procedure getFilteredRecords @anyvalue int, @randomnumber int
as
select * from Products
where UnitPrice Between @anyvalue and @randomnumber
go

exec getFilteredRecords 5, 10

drop procedure getFilteredRecords



--Views
--insert into view

create view Top10HighPrice as
select top 10 * from Products
order by UnitPrice desc;

drop view Top10HighPrice		

alter table products
Add ReorderLevel int

alter table products
drop constraint DF_Products_ReorderLevel, CK_ReorderLevel


exec sp_help Products


select * from Top10HighPrice

insert into Products values ('Thüringer Rostbratwurst' ,12,6,'50 bags x 30 sausgs.',	10000,	0,	0,	0,	1)


exec sp_rename 'Top10HighPrice.Discontinued','updatedColumnName'

--group by 

select top 1 SupplierID,Count(*) as SupplierProducts from Products
group by SupplierID
order by SupplierProducts desc

select * from Suppliers


select count(*) from Products
where SupplierID = 5

                   ------------------------------------------- Day 12 -------------------------------------------
select * from Orders --830

select * from Employees
select * from Shippers

create view ordersTop10Record as
select top 10 * from Orders


select ord.OrderID,ord.OrderDate,ord.ShipCity,Shippers.*,
CONCAT(Employees.LastName,' ',Employees.FirstName) as empFullName, Employees.Title
from ordersTop10Record as Ord
inner join Shippers
on Ord.ShipVia = Shippers.ShipperID
inner join Employees
on Ord.EmployeeID = Employees.EmployeeID
