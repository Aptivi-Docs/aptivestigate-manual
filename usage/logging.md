---
description: How do I log events?
icon: list-tree
---

# Logging

This library uses an abstract base logging class that you must inherit from to describe how your application is going to log events. Usually, it's just a simple call to functions like `Debug()`, `Info()`, and so on. That class that you'll need to inherit from in your custom logger class is called `BaseLogger`. However, this can be sometimes difficult, depending on how you want your application to log its events. For this reason, for the sake of simplicity, we've created three pre-built inherited classes in three different libraries:

* `Aptivestigate.Log4Net`
  * Uses the [Log4Net](https://logging.apache.org/log4net/) library to log application events
  * You can create a new instance of the `Log4NetLogger` class (leave all arguments empty to print to the console, or specify a configurator)
* `Aptivestigate.Serilog`
  * Uses the [Serilog](https://serilog.net/) library to log application events (you can use all available [Serilog sinks](https://github.com/serilog/serilog/wiki/provided-sinks))
  * You can create a new instance of the `SerilogLogger` class (leave all arguments empty to print to the console, or specify a configurator)
* `Aptivestigate.NLog`
  * Uses the [NLog](https://nlog-project.org/) library to log application events
  * You can create a new instance of the `NLogLogger` class (leave all arguments empty to print to the console, or specify a configurator)

Here's a simple example of how to log to the console using the Serilog console sink (for all levels):

```csharp
var logger = new SerilogLogger();
var exc = new Exception("We really can't do this.");
LogTools.Debug(logger, "Test message without formatting");
LogTools.Debug(logger, "Test message with formatting: {0}, {1}", "Hello", "John Smith");
LogTools.Info(logger, "This is an informational message!");
LogTools.Info(logger, "Saying: {0}, {1}", "Hello", "John Smith");
LogTools.Warning(logger, "Warning: this may not work properly.");
LogTools.Warning(logger, "Warning: a component, {0}, may not work properly.", "fusion reactor");
LogTools.Error(logger, "Error: Ship is out of fuel!");
LogTools.Error(logger, "Error: Fuel level is empty! {0}/{1}", 0, 320);
LogTools.Error(logger, exc, "Error.");
LogTools.Fatal(logger, "FATAL ERROR!");
LogTools.Fatal(logger, "FATAL ERROR: We can't do this! {0}", "Invalid operation.");
LogTools.Fatal(logger, exc, "FATAL ERROR!");
```

You can use the `LogTools` class that provides you with functions that allow you to easily log an event to different log levels using the base logger as the first parameter. This class contains the following:

* `Debug()`
  * Debug messages
* `Info()`
  * Informational messages
* `Warning()`
  * Warning messages
* `Error()`
  * Error messages
* `Fatal()`
  * Fatal error messages

For exceptions, you must place an exception instance before the message but after the logger instance. This is so that you can format the string with ease.

{% hint style="info" %}
You can also use the class functions to log application events to the logger.
{% endhint %}
