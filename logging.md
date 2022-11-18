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
<h4>Step 1: Install log4net</h4>
To install log4net, one of the options is via the Package Manager. If you're using Visual Studio, go to Tools > NuGet Package Manager > Package Manager Console, then type the following command:

``PM> Install-Package Microsoft.Extensions.Logging.Log4Net.AspNetCore``

This will install both the logging extensions of log4net in ASP.NET Core and the log4net library itself.

<h4>Step 2: Add the log4net.config file</h4>
Create log4net.config file in project root folder

 ```html:
<log4net>
	<root>
		<level value="WARN" />
		<appender-ref ref="RollingFile" />
	</root>
	<appender name="RollingFile" type="log4net.Appender.RollingFileAppender">
		<appendToFile value="true" />
		<file type="log4net.Util.PatternString" value="%property{LoggerFilePath}\logs\BulletinApp_%utcdate{yyyy-MM-dd}.log" />
		<layout type="log4net.Layout.PatternLayout">
			<conversionPattern value="%date %-5level %logger.%method [%line] - MESSAGE: %message%newline" />
		</layout>
	</appender>
</log4net>
```

<h4>Step 3: Modify the Program.cs file</h4>
 
``builder.Logging.ClearProviders(); ``

``builder.Logging.AddLog4Net("log4net.config");``
- If you want to set custom log file path instead of bin/debug, declare your custom log file path and use that in log4net.config file
``GlobalContext.Properties["LoggerFilePath"] = Environment.CurrentDirectory.Replace("\\bin\\Debug", "");``

<h4>Step 4: Test if the log files created</h4>
Add the following lines in the IndexModel() of the Index.cshtml.cs page:

```cs
_logger.LogDebug("Hey, this is a DEBUG message.");
_logger.LogInformation("Hey, this is an INFO message.");
_logger.LogWarning("Hey, this is a WARNING message.");
_logger.LogError("Hey, this is an ERROR message.");
```
- Run the code and wait until the web app is ready. Check the log folder, and you should see a new log file created. When you open the file, it shows the following content:
```cs
2022-11-18 09:06:35,007 WARN  web.Pages.IndexModel..ctor [15] - MESSAGE: Hey, this is a WARNING message.
2022-11-18 09:06:35,042 ERROR web.Pages.IndexModel..ctor [16] - MESSAGE: Hey, this is an ERROR message.
2022-11-18 09:06:39,923 WARN  web.Pages.IndexModel..ctor [15] - MESSAGE: Hey, this is a WARNING message.
2022-11-18 09:06:39,923 ERROR web.Pages.IndexModel..ctor [16] - MESSAGE: Hey, this is an ERROR message.
```
