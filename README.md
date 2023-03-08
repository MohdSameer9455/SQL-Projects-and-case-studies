# SQL-Projects-and-case-studies
use AdventureWorks2012;
select * from Person.EmailAddress;
select * from Person.PersonPhone;
--#get all the details from the person table including phone no,phone no type,email id so we use join on both table
------------------------------------------------------------------------------------------------------------------------
select pp.PhoneNumber,pp.PhoneNumberTypeID,pe.EmailAddress
from person.PersonPhone pp
join person.EmailAddress pe on pe.BusinessEntityID=pp.BusinessEntityID;
-----------------------------------------------------------------------------------------------------------------------
--#get the details of the sale header order made in may 2011

select * from Sales.SalesOrderHeader;
select * from Sales.SalesOrderHeader
where datepart(year,OrderDate)=2011 and datepart(month,OrderDate)=05;
-----------------------------------------------------------------------------------------------------------------------

--#get the details of the sales detail order made in month may 2011

select * from Sales.SalesOrderDetail;
select * from Sales.SalesOrderHeader;
SELECT so.*
from Sales.SalesOrderDetail so
join Sales.SalesOrderHeader sh on sh.SalesOrderID=so.SalesOrderID
where year(sh.OrderDate)=2011 and month(sh.OrderDate)=05;

----------------------------------------------------------------------------------------------------------------------------

--#get the total sales made in may 2011

SELECT sum(so.LineTotal)
from Sales.SalesOrderDetail so
join Sales.SalesOrderHeader sh on sh.SalesOrderID=so.SalesOrderID
where year(sh.OrderDate)=2011 and month(sh.OrderDate)=05;

----------------------------------------------------------------------------------------------------------------------------------

--#get the total sales made in year 2011 by month order by increasing sales

SELECT sum(so.LineTotal) totalsales,month(sh.OrderDate) month,year(sh.OrderDate) year
from Sales.SalesOrderDetail so
join Sales.SalesOrderHeader sh on sh.SalesOrderID=so.SalesOrderID
WHERE year(sh.OrderDate)=2011
group by month(sh.OrderDate),year(sh.OrderDate)
order by sum(so.LineTotal) desc;

-----------------------------------------------------------------------------------------------------------------------------

--#get the totalsales made to the customer withfirstname= gustavo and lastname=achong

select * from Sales.SalesOrderDetail;
select * from Person.Person;
select * from Person.BusinessEntity;

SELECT rowguid  from person.Person
where FirstName='gustavo' and LastName='achong'

 select COUNT(rowguid),FirstName,LastName from person.person
 where rowguid='D4C132D3-FCB5-4231-9DD5-888A54BEC693'
 group by FirstName,LastName

 select sum(ss.LineTotal) totalsales,pp.FirstName,pp.LastName
 from Sales.SalesOrderDetail ss
 join person.person pp on pp.rowguid=ss.rowguid
 where pp.FirstName='gustavo' and pp.LastName='achong'
 group by pp.FirstName,pp.LastName;

select LineTotal from Sales.SalesOrderDetail
 where rowguid='D4C132D3-FCB5-4231-9DD5-888A54BEC693'

 --its prooved that there is no sales done by gustavo and achong
