---
created: 31.01.2022
tags: dotnet efcore cli cheatSheet
parent: Cheat sheets
---

# dotnet efcore cli

```bash
dotnet ef database update
dotnet ef database update MyMigrationName

dotnet ef migrations add MyMigrationName -p /PathToProjectWithMigration/
dotnet ef migrations remove -p /PathToProjectWithMigration/
```
