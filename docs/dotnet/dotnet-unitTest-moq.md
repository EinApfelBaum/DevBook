---
created: 26.07.2021
tags: dotnet unitTest moq 
parent: dotnet
---

# Verify a method call wit exact parameters

```csharp
var name = "Peter";
var age = 42;
serviceMock.Verify(service =>
    service.CreateAsync(
        It.Is<Person>(x =>
            x.Name == name &&
            x.Age == age),
        It.IsAny<CancellationToken>()),
    Times.Once);
```

This does not work, because moq uses `Object.Equals` under the hood:

```csharp
serviceMock.Verify(service =>
    service.CreateAsync(
        new Person() { Name = "Peter", Age = 42 },
        It.IsAny<CancellationToken>()),
    Times.Once);
```
