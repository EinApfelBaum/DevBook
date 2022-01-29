---
created: 17.08.2021
tags: dotnet nuget
parent: dotnet
---

# Push a nuget package within a docker container

```dockerfile
# https://hub.docker.com/_/microsoft-dotnet-core
FROM mcr.microsoft.com/dotnet/core/sdk:3.1 as build-image

ARG Version
WORKDIR /home/app

# copy csproj and restore as distinct layers
COPY ./*/*.csproj ./SampleProject/
COPY ./*.sln .

RUN dotnet restore

# copy everything else and build app
COPY . .

RUN dotnet build \
        -p:Version=$Version \
        --configuration Release \
        --no-restore

RUN dotnet pack \
        -p:Version=$Version \
        -p:IncludeSymbols=true \
        -p:SymbolPackageFormat=snupkg \
        --configuration Release \
        --no-build \
        --output /artifacts

ENTRYPOINT ["dotnet", "nuget", "push", "/artifacts/*.nupkg", "--skip-duplicate"]

```

Build the container:

```bash
docker build -t push-packages --build-arg Version=0.0.1
```

To push the nuget packages to repository, run the container
=> The source and api-key argument will be appended to the entry point

```bash
docker run push-packages --source ${NUGET_REPO} --api-key ${NUGET_API_KEY}
```

---

## Resources

* [https://andrewlock.net/pushing-nuget-packages-built-in-docker-by-running-the-container/]([https://link](https://andrewlock.net/pushing-nuget-packages-built-in-docker-by-running-the-container/))
