---
created: 17.08.2021
tags: dotnet nuget cli
---

# nuget push / delete

```bash
dotnet nuget push --source myNugetFeed --api-key "ApiKey" "PackageName.nupkg"

dotnet nuget delete --source myNugetFeed --api-key "ApiKey" "PackageName" "PackageVersion" --non-interactive


dotnet nuget push --source http://<MyNugetFeedIp>:<PORT>/v3/index.json --api-key MyApiKey MyNugetPackage

dotnet nuget delete --source http://<MyNugetFeedIp>:<PORT>/v3/index.json --api-key MyApiKey MyNugetPackage 0.0.1 --non-interactive
```

## local feed in directory or packages copied into folders

```bash
dotnet nuget delete --source localFeed MyLib 1.0.0 --non-interactive
dotnet nuget delete --source ~/git/packages MyLib 1.0.0 --non-interactive
```
