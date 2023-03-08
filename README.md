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
```csharp
 PM> Scaffold-DbContext "Server=localhost;Database=AdventureWorksLT2012;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models
```
# Advanced DbContext and EntityTypes

## Package Manager Console commands 
```csharp
 PM> Scaffold-DbContext "Server=localhost;Database=dashboard_db;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models Model    -Context "ApplicationDbContext" -Namespace AdventureWork.Models -ContextNamespace  AdventureWork.Data.DbContext -DataAnnotations
```
## NET CLI
```csharp
 > dotnet add package Microsoft.EntityFrameworkCore.SqlServer
 > dotnet add package Microsoft.EntityFrameworkCore.Design
 > dotnet tool install --global dotnet-ef
 > dotnet ef dbcontext scaffold "Server=.\;Database=AdventureWorksLT2012;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -o Model -c "ApplicationDbContext" --data-annotations --context-dir 
```

## NET CLI (without annotation)
```csharp
 > dotnet add package Microsoft.EntityFrameworkCore.SqlServer
 > dotnet add package Microsoft.EntityFrameworkCore.Design
 > dotnet tool install --global dotnet-ef
 > dotnet ef dbcontext scaffold "Server=.\;Database=AdventureWorksLT2012;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -o Model -c "ApplicationDbContext" --context-dir 
```

## resource
[https://www.learnentityframeworkcore.com/walkthroughs/existing-database](https://www.learnentityframeworkcore.com/walkthroughs/existing-database)

[https://learn.microsoft.com/en-us/ef/core/managing-schemas/scaffolding/?tabs=vs](https://learn.microsoft.com/en-us/ef/core/managing-schemas/scaffolding/?tabs=vs)

# T4 Custom template: DbContext and EntityTypes
Use this tools before DbContext scaffold. Making any changes you want on both dbcontext.t4 and entitytypes.t4 and then run scaffolding.
```csharp
 > dotnet new install Microsoft.EntityFrameworkCore.Templates
 > dotnet new ef-templates
 // for update use --force at the end
 > dotnet ef dbcontext scaffold "Server=.\;Database=AdventureWorksLT2012;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -o "Data\Entities" --context-dir "Data\Context" -c "ApplicationDbContext" -f --no-pluralize --no-build --json
```

# How to Revert to the last migration
 1. Revert migration from database: 
    ```csharp PM> Update-Database <prior-migration-name> ```
 
 2. Remove migration file from project (or it will be reapplied again on next step)
 
 3. Update model snapshot
    ```csharp PM> Remove-Migration ```

  - UPD: The second step seems to be not required in latest versions of Visual Studio (2017).


# Powershell 
To change file names inside the Models folder using the below command
```shell
Get-ChildItem -Path "[YOUR PROJECT PATH]" -Filter Tb*.cs | Rename-Item -NewName { $_.name.Substring(2) | % { "" + $_ } }
```
