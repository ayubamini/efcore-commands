# efcore-commands
Reference document regarding Entity Framework Core commands.


## Get-Help

| Cmdlet      |        Description
| ------------- | ------------- |
| Add-Migration | Adds a new migration.
| Drop-Database | Drops the database.
| Get-DbContext | Gets information about a DbContext type.
| Remove-Migration | Removes the last migration.
| Scaffold-DbContext | Scaffolds a DbContext and entity types for a database.
| Script-Migration | Generates a SQL script from migrations.
| Update-Database | Updates the database to a specified migration.



## Create `READ MODEL` classes from Existing DataBase
Scaffold-DbContext "Server=localhost;Database=AdventureWorksLT2012;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models

## Advanced 
#Package Manager Console commands 
PM> Scaffold-DbContext "Server=localhost;Database=dashboard_db;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models Model -Context "ApplicationDbContext" -Namespace AdventureWork.Models -ContextNamespace  AdventureWork.Data.DbContext -DataAnnotations

# NET CLI
<csharp>
> dotnet add package Microsoft.EntityFrameworkCore.SqlServer
> dotnet add package Microsoft.EntityFrameworkCore.Design
> dotnet tool install --global dotnet-ef
> dotnet ef dbcontext scaffold "Server=.\;Database=AdventureWorksLT2012;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -o Model -c "ApplicationDbContext" --data-annotations --context-dir 
<code>

## resource
https://www.learnentityframeworkcore.com/walkthroughs/existing-database
https://learn.microsoft.com/en-us/ef/core/managing-schemas/scaffolding/?tabs=vs

# T4 Custom template
<csharp>
> dotnet new install Microsoft.EntityFrameworkCore.Templates
> dotnet new ef-templates
 // for update use --force at the end
<code>

# How to Revert to the last migration
======================================
Revert migration from database: 
PM> Update-Database <prior-migration-name>
Remove migration file from project (or it will be reapplied again on next step)
Update model snapshot: PM> Remove-Migration
UPD: The second step seems to be not required in latest versions of Visual Studio (2017).
