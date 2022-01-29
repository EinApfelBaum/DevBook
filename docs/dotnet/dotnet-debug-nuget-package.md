---
created: 17.08.2021
tags: dotnet debug nuget
parent: dotnet
---

# Debug a nuget package

Add to `csproj`.

```xml
<PropertyGroup>
    <IncludeSymbols>true</IncludeSymbols>
    <SymbolPackageFormat>snupkg</SymbolPackageFormat>
</PropertyGroup>
```

Pack and push nuget `nupkg` to feed, the `snupkg` will automatically pushed to symbol server

In VSCode add to launch.json

```json
{
    "justMyCode": false,
    "symbolOptions": {
        "searchPaths": ["http://192.168.13.40:57399/api/download/symbols"],
        "searchMicrosoftSymbolServer": false,
        "searchNuGetOrgSymbolServer": false
    }
}
```

---

## Resources

* [https://docs.microsoft.com/en-gb/nuget/create-packages/symbol-packages-snupkg](https://docs.microsoft.com/en-gb/nuget/create-packages/symbol-packages-snupkg)
