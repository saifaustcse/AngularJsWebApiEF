# Enitity Framekwork - Databse Design

## Technologies

-   [.NET 5](https://dotnet.microsoft.com/download)
-   [ASP.NET Core 5](https://docs.microsoft.com/en-us/aspnet/core)
-   [Entity Framework Core 5](https://docs.microsoft.com/en-us/ef/core)

## Practices

-   one-to-one, one-to-many, many-to-many relationship databse design
-   code first entity frmamework approach
-   Data seeding

## Run

<details>
<summary>Visual Studio</summary>

#### Prerequisites

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [.NET 5 SDK](https://dotnet.microsoft.com/download/dotnet/5.0)
-   [SQL Server](https://go.microsoft.com/fwlink/?linkid=866662)

#### Steps

1. Open **EntityFramework.Database.Design.sln** in Visual Studio.
2. Open nuget package console
3. Run commands migration commands  
   `Add-Migration InitialCreate`  
   `Update-Database`
4. Verify that database is created with seed dada
5. Run the project

</details>

<details>
<summary>Visual Studio Code</summary>

#### Prerequisites

-   [.NET 5 SDK](https://dotnet.microsoft.com/download/dotnet/5.0)
-   [SQL Server](https://go.microsoft.com/fwlink/?linkid=866662)
-   [Visual Studio Code](https://code.visualstudio.com)
-   [C# Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)

#### Steps

1. Open directory **entity-framework-database-design** in vs code
2. Open Integrated Terminal under **EntityFramework.Database.Design** directiory
3. Run commands migration commands  
   `dotnet tool install --global dotnet-ef `  
   `dotnet ef migrations add InitialCreate `  
   `dotnet ef database update`
4. Verify that database is created with seed data

</details>

## Check Relationship

![diagram](./resources/diagram.png)

<details>
<summary>One to Many relationship</summary>

#### Department and Employee

-   One Employee is associated only one department
-   One Department has many Employees
-   So we need to add reference in Employees (many) table

#### Verify that Same DepartmentId is used many items in Employee table

![one-to-many](./resources/one-to-many.PNG)

</details>

<details>
<summary>One to One relationship</summary>

#### Employee and EmployeeSalary

-   One Employee is associated only one EmployeeSalary
-   One EmployeeSalary is associated only one Employees
-   So we need to add reference in both (EmployeeSalary and Employee) table but foreign key will be used only in mendotory table i.e EmployeeSalary

#### Execute the following inset query twice

         INSERT INTO [EmployeeSalary] (
         [EmployeeId]
         ,[SalaryAmount]
         ,[IsActive]
         ,[CreatedDate]
         )
         VALUES (1, 3000, 1, GETDATE());

#### Generally in One to many relation, you could enter multiple times EmployeeID, but here in one to one relation an error will be thrown while executing the query except first time

         Cannot insert duplicate key row in object 'dbo.EmployeeSalary' with unique index 'IX_EmployeeSalary_EmployeeId'. The duplicate key value is (1).

#### Verify that not duplicate EmployeeId is allowed EmployeeSalary table

![one-to-one](./resources/one-to-one.PNG)

</details>
