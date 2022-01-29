---
created: 17.08.2021
tags: dotnet efcore
parent: dotnet
---

# EfCore value converter for DateTime

EFCore converts DateTime from database with an undefined kind property with this extension method the property kind will be converted to UTC.

```csharp

public static class ModelBuilderExtensions
{
    public static ModelBuilder UseValueConverterForType<T>(this ModelBuilder modelBuilder, ValueConverter converter)
    {
        return modelBuilder.UseValueConverterForType(typeof(T), converter);
    }

    public static ModelBuilder UseValueConverterForType(this ModelBuilder modelBuilder, Type type, ValueConverter converter)
    {
        foreach (var entityType in modelBuilder.Model.GetEntityTypes())
        {
            // note that entityType.GetProperties() will throw an exception, so we have to use reflection 
            var properties = entityType.ClrType.GetProperties().Where(p => p.PropertyType == type);
            foreach (var property in properties)
            {
                modelBuilder.Entity(entityType.Name).Property(property.Name)
                    .HasConversion(converter);
            }
        }

        return modelBuilder;
    }
}

// In the dbcontext we need to definde the value converter
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    var dateTimeConverter = new ValueConverter<DateTime, DateTime>(v => v, v => DateTime.SpecifyKind(v, DateTimeKind.Utc));
    modelBuilder.UseValueConverterForType<DateTime>(dateTimeConverter);
 }

```

---

## Resources

* [https://github.com/dotnet/efcore/issues/10784](https://github.com/dotnet/efcore/issues/10784)
* [https://github.com/dotnet/efcore/issues/4711]([https://link](https://github.com/dotnet/efcore/issues/4711))