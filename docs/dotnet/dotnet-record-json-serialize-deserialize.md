---
created: 02.08.2021
tags: dotnet record
parent: dotnet
---

# Record: Serialize/deserialize attributes using primary constructor

> The `JsonPropertyName` will override any naming policy specified by JsonNamingPolicy.

```csharp
    public record Person(
        [property: JsonPropertyName("name_test")] string Name,
        [property: JsonPropertyName("age_test")] int Age
        );

    var person = new Person("userA", 42);
    var json = JsonSerializer.Serialize(person);
```

```json
{
    "name_test": "userA",
    "age_test": 42
}
```