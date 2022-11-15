Call WebApplication.CreateBuilder, which adds the following logging providers:
- Console
- Debug
- EventSource
- EventLog (for window only)

``var builder = WebApplication.CreateBuilder(args);`` in program.cs

Configure logging
- in appsettings.{ENVIRONMENT}.json
```{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  }
}

```
Log levels - Trace = 0, Debug = 1, Information = 2, Warning = 3, Error = 4, Critical = 5, and None = 6

