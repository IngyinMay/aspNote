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

<h2> Log4net </h2>
ref - https://blog.hackajob.co/how-to-log-in-asp-net-core-web-apps-using-log4net/

<h3>Installation</h3>
<h4> Step1</h4>
To install log4net, one of the options is via the Package Manager. If you're using Visual Studio, go to Tools > NuGet Package Manager > Package Manager Console, then type the following command:

``PM> Install-Package Microsoft.Extensions.Logging.Log4Net.AspNetCore``

This will install both the logging extensions of log4net in ASP.NET Core and the log4net library itself.
