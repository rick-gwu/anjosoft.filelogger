# FileLogger

v.1.0.0

Logging provider for .net that allows you to log messages to text files
<br>
<br>

### Installation

Cifra is hosted at [nuget.org](https://www.nuget.org/packages/anjosoft.filelogger/). To Install, run:
``dotnet add package anjosoft.filelogger``

---

### Usage

import the ``anjosoft.filelogger`` namespace

Configure your log levels:

```
{
  "Logging": {
    "File": {
      "LogLevel": {
        "Default": "Information",
        "Microsoft": "Error"
      }
    }
  },
  "AllowedHosts": "*"
}
```

By default, the logger will place logs in the applications’s root directory, inside a folder called “application_logs”. The default file format is UtcDateTime.log, for example, “2024-01-01.log”. To override the default log directory and/or file name format, you can specify a value for FolderPath and/or FilePath in your settings file. For example:

```
{
  "Logging": {
    "File": {
      "Options": {
        "FolderPath": "\Users\Shared\AppLogs",
        "FilePath": "app_{date}.log"
      },
      "LogLevel": {
        "Default": "Information",
        "Microsoft": "Error"
      }
    }
  }
}
```

#### Example

```
...
using anjosoft.filelogger;

namespace myapp_api.Controllers
{
    [Route("items")]
    public class ItemsController(IItemService itemService, ILogger<FileLogger> fileLogger) : ControllerBase
    {
        private readonly IItemService itemService = itemService;
        private readonly ILogger<FileLogger> fileLogger = fileLogger;

        [HttpPost]
        public async Task<IActionResult> Post([FromBody] ItemDTO item)
        {
            fileLogger.LogInformation("Posting a new item");
            ...
        }
        ...
```
