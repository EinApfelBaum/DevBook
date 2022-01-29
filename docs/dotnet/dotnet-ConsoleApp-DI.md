---
created: 09.07.2021
tags: dotnet ConsoleApp withSample
parent: dotnet
---

# C# Console App with DI

Credits:

* [IAmTimCorey - .NET Core Console App with Dependency Injection, Logging, and Settings](https://www.youtube.com/watch?v=GAOCe-2nXqc)
* [Free elephant api](https://elephant-api.herokuapp.com/)

Running project:
[https://github.com/EinApfelBaum/ElephantClient](https://github.com/EinApfelBaum/ElephantClient)

Needed nuget package:

```xml
  <ItemGroup>
    <PackageReference Include="Microsoft.Extensions.Hosting" Version="5.0.0" />
    <PackageReference Include="Microsoft.Extensions.Http" Version="5.0.0" />
    <PackageReference Include="Serilog.Extensions.Hosting" Version="4.1.2" />
    <PackageReference Include="Serilog.Settings.Configuration" Version="3.1.0" />
    <PackageReference Include="Serilog.Sinks.Console" Version="3.1.1" />
  </ItemGroup>
```

```csharp
class Program
{
    static async Task Main(string[] args)
    {
        var configurationBuilder = new ConfigurationBuilder();
            BuildConfig(configurationBuilder);
            var config = configurationBuilder.Build();

        Log.Logger = new LoggerConfiguration()
            .ReadFrom.Configuration(config)
            .Enrich.FromLogContext() // => adds more information from the serilog context
            .WriteTo.Console()
            .CreateLogger();

        var builder = Host.CreateDefaultBuilder()
            .ConfigureServices(services =>
            {
                // register our entry point
                services.AddTransient<IApplication, Application>();

                // add a typed http client
                services.AddHttpClient<IElephantClient, ElephantClient>(config =>
                {
                    // add http client congif here
                    config.BaseAddress = new Uri("https://elephant-api.herokuapp.com");
                });

                // register some other servies

            })
            .UseSerilog()
            .Build();

        // entry point for our console application, here we need to concrete implementation.
        var app = ActivatorUtilities.CreateInstance<Application>(builder.Services);
        await app.Run();
    }

    static void BuildConfig(IConfigurationBuilder builder)
    {
        // connect appsettings to application
        // The order of AddJsonFile does matter. The last will overwrite existing configs.
        // In our case the environment variable will overwrite existing configs.
        builder.SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("appsettings.json", optional: false, reloadOnChange: true)
            .AddJsonFile($"appsettings.{Environment.GetEnvironmentVariable("ASPNETCORE_ENVIRONMENT") ?? "Production"}.json", optional: true)
            .AddEnvironmentVariables();
        
    }
}
```

```csharp
public interface IApplication
{
    Task Run();
}

public class Application : IApplication
{
    private readonly ILogger _log;
    private readonly IElephantClient _elephantClient;

    public Application(ILogger<Application> log, IElephantClient elephantClient)
    {
        _log = log;
        _elephantClient = elephantClient;
    }

    public async Task Run()
    {
        // my applidaction code
        await _elephantClient.GetElephants();
    }
}
```

```csharp
public class ElephantClient : IElephantClient
{
    private readonly ILogger _log;
    private readonly HttpClient _client;

    public ElephantClient (ILogger<ElephantClient> log, HttpClient client)
    {
        _log = log;
        _client = client;
    }

    public Task<IEnumerable<Elephant>> GetElephants()
    {
        return await _client.GetFromJsonAsync<Elephant[]>("elephants");
    }
}

record Elephant(
    int Index, 
    string Name,
    string Image,
    string Wikilink
    );
```

During development it can happen that this kind of exception occur. This basically means that a property within the incoming data could not be converted to the specified type you defined in your class/record. When you carefully read the exception you can identify the expected and given type. In this example I defined a property as string, but the Json converter expected a property of type int.
![JsonException, JSON value could not be converted](/assets/images/2021-07-09-21-45-26.png)
