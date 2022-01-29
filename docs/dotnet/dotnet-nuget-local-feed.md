---
created: 17.08.2021
tags: dotnet nuget
parent: dotnet
---

# dotnet and local nuget feed

## Empty folder

No need to push nuget package to local feed, use an empty folder.
Add `--source localNugetFeedFolder` option to the commands.
Source is the local nuget feed folder.

```bash
dotnet add package MyLib -v 1.0.1 --source ~/git/packages/
dotnet restore --source ~/git/packages
```

## Local nuget feed as source to nuget config

The nuget config can be found here : ~/.nuget/NuGet/NuGet.Config

```bash
# Add feed as source to nuget config
dotnet nuget add source ~/git/packages --name localNugetFeed
dotnet nuget add source http://mynugetfeed.de/v3/index.json --name serverNugetFeed
```

```bash
# push nuget package to local nuget feed
dotnet nuget push --source localNugetFeed MyLib.1.0.0.nupkg 
```

```bash
# add package to app
dotnet add package MyLib -v 1.0.0
```

## Push package and configure in `csproj`

```bash
# push nuget package to local nuget feed
dotnet nuget push --source ~/git/packages MyLib.1.0.0.nupkg 
```

```xml
# add the restore source to the csproj
<PropertyGroup>
    <RestoreSources>$(RestoreSources);../../git/packages/;https://api.nuget.org/v3/index.json</RestoreSources>
</PropertyGroup>
```

```bash
# add package to app
dotnet add package MyLib -v 1.0.0
```

---

## Resources

* [https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-nuget-add-source](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-nuget-add-source)
