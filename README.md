                                                    --MSSQL-DATABASE--
                                                    

-------------create database-------------<br>
create database S1;

-------------use database-------------<br>
use S1;

-------------rename database-------------<br>
alter database S1 modify name = S18

-------------delete database-------------<br>
drop database S18


-------------------------------------------------------------------------------------------------------------------------<br>

--TABLE<br>

-------------create TABLE-------------<br>
create table prectice(
id int,
Fname varchar(225),
dob date,
dob1 time,
dob2 datetime,
percentt float,
phonenumber bigint unique,
);


-------------select table-------------<br>
select * from prectice;
select id,dob2 from prectice;

select * into newtest from prectice
select * from newtest


-------------insert table-------------<br>
insert into prectice values (1,'sakshi', '2002-04-18','12:12:12', '2002-04-18 12:12:12' ,100.10 , 123456789);
insert into prectice (id,Fname,phonenumber)values (2,'rafat',123456789);
insert into prectice (id,Fname,phonenumber)values (3,'rohit',123456789);


-------------drop table-------------<br>
drop table prectice;


-------------------------------------------------------------------------------------------------------------------------<br>


-------------Alter table-------------<br>
alter table prectice 
add Lname varchar(225);

alter table prectice
alter column Lname varchar(50); 

alter table prectice 
drop column Lname;

-------------------------------------------------------------------------------------------------------------------------<br>

--rename column name--<br>
sp_rename 'prectice.Lname','LNAME','COLUMN';

--rename table name--<br>
sp_rename 'practice','prectice'


-------------------------------------------------------------------------------------------------------------------------<br>

-------------truncate table-------------<br>
truncate table prectice;


-------------------------------------------------------------------------------------------------------------------------

-------------UPDATE TABLE-------------<br>
update prectice 
set LNAME = 'munde'
where id = 1;


-------------------------------------------------------------------------------------------------------------------------<br>

-------------DELETE TABLE VALUES-------------<br>
delete from  prectice
where id = 3 and id = 4;


-------------------------------------------------------------------------------------------------------------------------<br>

-------------TABLE CONSTRAINTS-------------<br>
--not null--
alter table prectice
alter column id int not null;


--unique--<br>
alter table prectice 
add age int unique;



--DEFAULT--<br>
create table t3(
id int,
fname varchar(225) default 'rohit'
);

insert into t3 (id) values(2)
select * from t3



--primary key--<br>
create table t1(
id int,
fname varchar(225) not null
constraint pk primary key (id)
);

select * from t1;
insert into t1 values (3,'sakshi'),(4,'rafat'),(5,'rohit')



--foreign key--<br>
create table t2(
id int,
fname varchar(225) not null
constraint fk foreign key (id) references t1(fname)
);

insert into t2 values (3,'sakshi munde'),(4,'rohit waghmare'),(5,'rafat naaz')
select * from t2


-------------------------------------------------------------------------------------------------------------------------<br>


--add constraint--<br>
alter table prectice 
add constraint unique_value unique(id);


--drop constraint--<br>
alter table prectice
drop constraint unique_value; 


-------------------------------------------------------------------------------------------------------------------------<br>

--TABLE DESC--<br>
sp_help t2


-------------------------------------------------------------------------------------------------------------------------<br>


--SELECT IN TABLE--<br>
use Northwind
select * from Products


-------------------------------------------------------------------------------------------------------------------------<br>

--DISTINCT--<br>
select distinct Country from Customers


-------------------------------------------------------------------------------------------------------------------------<br>

--COUNT--<br>
select count(*) as countt from Customers

select count(country) from Customers
select count(distinct country) from Customers


-------------------------------------------------------------------------------------------------------------------------<br>

--SUM--<br>
select sum(CategorySales) as summ from [Category Sales for 1997]


-------------------------------------------------------------------------------------------------------------------------<br>

--AVG--<br>
select avg(UnitsInStock) from Products


-------------------------------------------------------------------------------------------------------------------------<br>

--MIN--<br>
select min(UnitsInStock) from Products


-------------------------------------------------------------------------------------------------------------------------<br>


--MAX--<br>
select max(UnitsInStock) from Products


-------------------------------------------------------------------------------------------------------------------------<br>


--BETWEEN--<br>
select * from Products
where UnitPrice between 1 and 10;

select * from Products
where UnitPrice not between 1 and 10;


-------------------------------------------------------------------------------------------------------------------------<br>


--GROUP BY--<br>
select Country,count(Country) as countt from Customers 
group by Country

select Discontinued from Products
group by Discontinued


-------------------------------------------------------------------------------------------------------------------------<br>

--ORDER BY--<br>
select Country,count(Country) as countt from Customers 
group by Country order by count(Country) asc;

select PostalCode from Customers
order by PostalCode desc



-------------------------------------------------------------------------------------------------------------------------<br>

--top--<br>
select top 10 * from Customers

select top 93 percent * from Customers


-------------------------------------------------------------------------------------------------------------------------<br>

--LIKE--<br>
select * from Customers
where (Country like 'a%' or Country like 'e%' or Country like 'i%' or Country like 'o%' or Country like 'u%') 
AND   (Country like '%a' or Country like '%e' or Country like '%i' or Country like '%o' or Country like '%u')
order by Country

select * from Customers
where Country like '_s%'

select * from Customers
where Country like '[a-g]%a'


-------------------------------------------------------------------------------------------------------------------------<br>

--IN--<br>
select * from Customers
where Country in ('argentina','usa','germany')
order by country


-------------------------------------------------------------------------------------------------------------------------<br>

--IDENTITY--<br>
create table t4(
id int identity (1,1),
fname varchar(225)
);

insert into t4 (fname) values ('rohit'),('rafat')
select * from t4


-------------------------------------------------------------------------------------------------------------------------<br>

--SUB QUERY--<br>

select Country into newcountry from Customers
where Country in ('usa','argentina')

select * from Customers
where Country in (select * from newcountry)


-------------------------------------------------------------------------------------------------------------------------<br>

--PROCEDURES--<br>

create procedure getcountryUsaAndArgentina
as
select * from Customers
where Country in ('usa','argentina')
go


exec getcountryUsaAndArgentina


drop procedure getcountryUsaAndArgentina


--DYNAMIC PROCEDURE--<br>

create procedure getcountryUsaAndArgentina2 @value1 varchar(225), @value2 varchar(225)
as
select * from Customers
where Country = @value1 or Country = @value2
go

exec getcountryUsaAndArgentina2 @value1 = 'USA',@value2 = 'argentina' 

drop procedure getcountryUsaAndArgentina2


-------------------------------------------------------------------------------------------------------------------------<br>


--VIEW--<br>
create view prod
as
select * from Products
where UnitPrice between 0 and 10

select * from prod
insert into prod values('Aniseed Syrupp',1,2,'122 - 550 ml bottles',3.00,	13,	70,	25,	0)


-------------------------------------------------------------------------------------------------------------------------<br>


--JIONS--<br>

--inner join--<br>
select * from Orders
select * from Customers

select * from Customers
inner join Orders
on Customers.CustomerID = Orders.CustomerID

create table lt(
id int 
);

create table Rt(
id int 
);

insert into lt values(1),(2),(3),(4)
insert into Rt values(1),(5),(6)

select * from lt 
inner join Rt
on lt.left_id = Rt.right_id

sp_rename 'lt.id','left_id','COLUMN'
sp_rename 'Rt.id','right_id','COLUMN'

alter table lt
add mid int identity(1,1)

update Rt
set fname = concat('name-',right_id)


update Rt 
set fname = 'sakshi'
where fname in (select top 1 fname from RT)



--left--<br>
select * from lt
left join Rt 
on lt.left_id = Rt.right_id



--Right--<br>
select * from Rt
right join lt 
on lt.left_id = Rt.right_id



--full OUTER JOIN--<br>
select * from lt
full outer join Rt 
on lt.left_id = Rt.right_id


--union------DISTINT values <br>
select * from lt
union
select * from Rt

--union all--ALL values<br>
select * from lt
union all
select * from Rt


--3 TABLE JOIN--<br>
create table newtable(
t3_id int,
fname varchar(225)
)

select * from newtable
insert into newtable values(1,'sakshi'),(2,'rohit'),(3,'rafat')

--1--<br>
select * from lt 
inner join Rt
on lt.left_id = Rt.right_id
inner join newtable
on lt.left_id = newtable.t3_id


--2--<br>
select * from lt
left join Rt
on lt.left_id = Rt.right_id
left join newtable
on lt.left_id = newtable.t3_id


--3--<br>
select * from lt
right join Rt
on lt.left_id = Rt.right_id
right join newtable
on lt.left_id = newtable.t3_id



--TRIGGERS--<br>

create trigger tig
on ARCustomers
after insert,delete,update
as
select * from ARCustomers

update ARCustomers
set Country = 'United Arab Emir'
where CustomerID = 13006

--VIEW--<br>
create view v1
as
select top 10 * from ARCustomers

select * from v1

--BETWEEN--<br>
select * from ARCustomers
where CustomerID between  13000 and 15000

--LIKE--<br>
select * from ARCustomers
where City like 'a%'

--group BY--<br>
select City,count(City) from ARCustomers
group by City



