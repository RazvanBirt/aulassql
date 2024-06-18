use AdventureWorks2014
go

--2.1
--select name from HumanResources.Department;

--2.2
--select P.BusinessEntityID, P.FirstName + '' + P.LastName as 'Nome Completo' from Person.Person as P;

--2.3
--select * from Purchasing.Vendor;

--2.4
--select BusinessEntityID, FirstName, LastName from Person.Person order by FirstName;

--2.5
--select FirstName, MiddleName, LastName from Person.Person where MiddleName IS NOT NULL;

--2.6
--select BusinessEntityID, LoginID, JobTitle, HireDate from HumanResources.Employee where JobTitle like 'Design Engineer' order by HireDate desc;

--2.7
--select ProductID, Name, ProductNumber, Color, ListPrice from Production.Product where Color is not null and ListPrice > 0;

--2.8
--select ProductNumber, Name, StandardCost,Class from Production.Product where StandardCost > 0 and Class in ('L', 'M');

--2.9
--select BusinessEntityID, JobTitle, MaritalStatus, Gender, HireDate from HumanResources.Employee where HireDate > '2008-12-31' and Gender like 'M' and MaritalStatus like 'M';

--2.10
--select Color, ProductNumber, Name from Production.Product where Name like 'M%' and Color in('Red','Silver');

--2.11
--select count(CreditCardID) as 'Total Cartões de Credito' from Sales.CreditCard;

--2.12
--select BusinessEntityID, LoginID, JobTitle, MaritalStatus, Gender, HireDate from HumanResources.Employee where HireDate like '2008%' or HireDate like '2009%';

--2.13
--select JobTitle, count(JobTitle) as 'Total_Empregados' from HumanResources.Employee group by JobTitle order by count(JobTitle) desc;

--2.14
--select AVG(ListPrice) as 'Média do Preço dos Produtos', MAX(ListPrice) as 'Maximo do Preço dos Produtos', MIN(ListPrice) as 'Minimo do Preço dos Produtos', SUM(ListPrice) as 'Soma do Preço dos Produtos' from Production.Product;

--2.15
--select Class, AVG(ListPrice) as 'Média do Preço dos Produtos', MAX(ListPrice) as 'Maximo do Preço dos Produtos', MIN(ListPrice) as 'Minimo do Preço dos Produtos', SUM(ListPrice) as 'Soma do Preço dos Produtos'
--from Production.Product where Class in ('H','L','M') group by Class;

--2.16
--select ExpYear, count(ExpYear) as 'Total de Cartões' from Sales.CreditCard group by ExpYear;

--2.17
--select CustomerID, SUM(TotalDue) as 'Total Devido' from Sales.SalesOrderHeader
--group by CustomerID having SUM(TotalDue)>=1500 order by SUM(TotalDue);

--2.18
--select ProductID, count(OrderQty) as 'Total Ordens de Trabalho' from Production.WorkOrder
--group by ProductID having count(OrderQty) between 100 and 200;

--2.1
--select HumanResources.Employee.BusinessEntityID, MaritalStatus, Gender, JobTitle, BirthDate, Bonus, SalesLastYear
--from HumanResources.Employee, Sales.SalesPerson;

--2.2
--select Person.Person.BusinessEntityID, FirstName, LastName, Person.EmailAddress.EmailAddress
--from Person.Person inner join Person.EmailAddress
--on Person.Person.BusinessEntityID = Person.EmailAddress.BusinessEntityID;

--2.3
--select Production.ProductCategory.Name, Production.ProductSubcategory.Name, Production.Product.Name, Production.Product.ProductNumber, Production.Product.ListPrice, Production.Product.SellStartDate, Production.Product.SellEndDate
--from Production.ProductCategory inner join Production.ProductSubcategory
--on Production.ProductCategory.ProductCategoryID = Production.ProductSubcategory.ProductCategoryID
--inner join Production.Product
--on Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID
--order by Production.Product.ListPrice desc;

--2.4
--select SOH.CustomerID as 'Cliente', SOH.OrderDate, SOH.PurchaseOrderNumber, SOD.ProductID, SOD.OrderQty, SOH.SubTotal, ST.Name
----from Sales.Customer C, Sales.SalesOrderHeader SOH, Sales.SalesOrderDetail SOD, Sales.SalesTerritory ST
--from Sales.SalesOrderHeader SOH inner join Sales.SalesOrderDetail SOD
--on SOH.SalesOrderID = SOD.SalesOrderID
--inner join Sales.SalesTerritory ST
--on SOH.TerritoryID = ST.TerritoryID
--where ST.Name like 'Canada';

--2.5
--select P.FirstName, sum(SOH.TotalDue) as 'Total Devido (Total Due)'
--from Person.Person P inner join Sales.Customer C
--on P.BusinessEntityID = C.PersonID
--inner join Sales.SalesOrderHeader SOH
--on SOH.CustomerID = C.CustomerID
--group by P.FirstName
--having P.FirstName like 'Manuel';

--2.6
--select Sales.SalesTerritory.Name, count(distinct(Sales.SalesOrderHeader.SalesOrderID)) as 'Numero Vendas'
--from Sales.SalesTerritory inner join Sales.SalesOrderHeader
--on Sales.SalesTerritory.TerritoryID = Sales.SalesOrderHeader.TerritoryID
--group by Sales.SalesTerritory.Name;

--2.7
--select P.FirstName + ' ' + P.LastName as 'Nome_Completo', ST.Name
--from Person.Person P inner join Sales.Customer C
--on P.BusinessEntityID = C.CustomerID
--inner join Sales.SalesTerritory ST
--on C.TerritoryID = ST.TerritoryID
--where ST.Name like 'Canada'
--order by 'Nome_Completo';

--2.8
--select ST.Name, P.FirstName, P.LastName, CC.CardType, CC.CardNumber, CC.ExpYear, SOH.SalesOrderNumber, SOH.TotalDue, SOH.DueDate
--from Sales.SalesTerritory ST inner join Sales.SalesOrderHeader SOH
--on ST.TerritoryID = SOH.TerritoryID inner join Person.Person P
--on P.BusinessEntityID = SOH.CustomerID inner join Sales.CreditCard CC
--on CC.CreditCardID = SOH.CreditCardID
--where CC.CardType like 'SuperiorCard' and ST.Name like 'Germany';

--2.9
--select Purchasing.PurchaseOrderHeader.PurchaseOrderID as 'SalesOrderID', Purchasing.PurchaseOrderHeader.OrderDate from Purchasing.PurchaseOrderHeader
--union
--select Sales.SalesOrderHeader.SalesOrderID, NULL from Sales.SalesOrderHeader;

--2.10
--select Purchasing.PurchaseOrderHeader.PurchaseOrderID, Purchasing.PurchaseOrderHeader.OrderDate, Purchasing.PurchaseOrderHeader.TotalDue
--from Purchasing.PurchaseOrderHeader
--where TotalDue>3000
--intersect
--select Purchasing.PurchaseOrderHeader.PurchaseOrderID, Purchasing.PurchaseOrderHeader.OrderDate, Purchasing.PurchaseOrderHeader.TotalDue
--from Purchasing.PurchaseOrderHeader
--where TotalDue<5000;

--2.11
--insert into HumanResources.Department(GroupName, Name, ModifiedDate) values('Formadores', 'Formadores Lda', '2018-03-07');
--insert into HumanResources.Department(GroupName, Name, ModifiedDate) values('Técnicos BONS', 'Técnicos do Melhor', '2018-03-06');
--insert into HumanResources.Department(GroupName, Name, ModifiedDate) values('Managers', 'Managers Top', '2018-03-07');
--insert into HumanResources.Department(GroupName, Name, ModifiedDate) values('Cleaning', 'Cleaning People', '2018-03-04');
--insert into HumanResources.Department(GroupName, Name, ModifiedDate) values('Chefes', 'Chefes de topo', '2018-03-02');

--2.12
--delete from HumanResources.Department
--where ModifiedDate>='2018-03-02' AND ModifiedDate <='2018-03-06';

--2.13
--update Production.Product
--set Color = 'Blue'
--where ProductID between 1 and 4;

--2.14
--update Production.Product
--set SafetyStockLevel = SafetyStockLevel + 100, Size = 42
--where Class is Null;

--2.15
--update Sales.SalesPerson
--set Bonus = Bonus * 1.2;

--2.16
--update Sales.CreditCard
--set CardType = 'The Best', ExpYear = '2020'
--where CardType = 'Distinguish';

--2.17
--update Person.Person
--set Title = 'Boss', Suffix = 'bs'
--where PersonType = 'VC';

--2.18
--update Purchasing.Vendor
--set CreditRating = 5
--where BusinessEntityID between 1500 and 1600;


-- autorização para diagrama
--ALTER AUTHORIZATION ON DATABASE::SalesBD TO [sa];

--2.1
--create database SalesBD

--2.2
--create table Employees (
--EmployeeID int not null primary key,
--FirstName nvarchar(40) not null,
--MiddleInitial nvarchar(40) default '-',
--LastName nvarchar(40) not null
--)

--create table Products(
--ProductID int not null primary key,
--Name nvarchar(40) not null,
--Price money check(Price > 0)
--)

--create table Customers(
--CustomerID int not null primary key,
--FirstName nvarchar(40) not null,
--MiddleInitial nvarchar(40) default '-',
--LastName nvarchar(40) not null
--)

--create table Sales(
--SalesID int not null primary key,
--SalesPersonID int not null references Employees(EmployeeID),
--CustomerID int not null references Customers(CustomerID),
--ProductID int not null references Products(ProductID),
--Quantity int not null check(Quantity > 0)
--)

--2.3
--2.3.1
--alter table Customers add Genero char(1) check(Genero in ('F', 'M'))
--alter table Employees add Genero char(1) check(Genero in ('F', 'M'))

--2.3.2
--alter table Employees add Salario money check(Salario>0)

--2.3.3
--alter table Sales add DueDate date default getdate()

--2.3.4
--alter table Products alter column Name varchar(100)

--2.3.5
--create type DINHEIRO from numeric(12,2) not null
--alter table Sales add Subtotal DINHEIRO

--2.4
--create schema vendas
--alter schema vendas transfer Customers
--alter schema vendas transfer Employees
--alter schema vendas transfer Products
--alter schema vendas transfer Sales

--2.5
--create login XUtilizador with password = 'Xlog2018+'

--2.6
--create user TESTE for login XUtilizador

--2.7
--deny delete on object::vendas.Sales to TESTE

--2.8 drop database
--USE master;
--ALTER DATABASE SalesBD SET SINGLE_USER WITH ROLLBACK IMMEDIATE;
--DROP DATABASE SalesBD;
