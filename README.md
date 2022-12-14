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
Scaffold-DbContext "Server=localhost;Database=dashboard_db;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models
