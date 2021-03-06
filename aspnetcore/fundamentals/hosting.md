---
title: "Размещение в ASP.NET Core"
author: guardrex
description: "Дополнительные сведения о веб-узла в ASP.NET Core, который отвечает за управление запуском и временем существования приложения."
ms.author: riande
manager: wpickett
ms.date: 09/21/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/hosting
ms.openlocfilehash: 7f6712073002b73ca4ddd7586718c81e62cacbc2
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="hosting-in-aspnet-core"></a>Размещение в ASP.NET Core

Автор [Люк Латэм](https://github.com/guardrex) (Luke Latham)

Настройка приложений ASP.NET Core и запустите *узла*. Основное приложение отвечает за управление запуском и временем существования приложения. Как минимум узел настраивает сервер и конвейер обработки запросов.

## <a name="setting-up-a-host"></a>Настройка узла

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

Создание узла с помощью экземпляра [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder). Это обычно выполняется в точке входа приложения, `Main` метод. В шаблоны проектов `Main` находится в папке *Program.cs*. Типичный *Program.cs* вызовы [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) начата Настройка узла:

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main)]

`CreateDefaultBuilder`выполняет следующие задачи:

* Настраивает [Kestrel](servers/kestrel.md) и веб-сервер. Параметры по умолчанию Kestrel см. в разделе [Kestrel параметры раздела Kestrel реализация веб-сервера в ASP.NET Core](xref:fundamentals/servers/kestrel#kestrel-options).
* Задает содержимое корневого пути, возвращенных [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory).
* Необязательная конфигурация загружает из:
  * *appsettings.json*.
  * *appsettings.{Environment}.json*.
  * [Секреты пользователя](xref:security/app-secrets) при запуске приложения `Development` среде.
  * Переменные среды.
  * Аргументы командной строки.
* Настраивает [входа](xref:fundamentals/logging/index) для вывода на консоль и отладки. Ведение журнала включает [фильтрации журнала](xref:fundamentals/logging/index#log-filtering) правила, указанные в разделе конфигурации ведения журнала *appsettings.json* или *appsettings. {} Среда} .json* файл.
* При работе под IIS позволяет [интеграции IIS](xref:host-and-deploy/iis/index). Настраивает сервер прослушивает при использовании порта и пути к базовой папке [модуль ASP.NET Core](xref:fundamentals/servers/aspnet-core-module). Модуль создает обратный прокси-сервер служб IIS и Kestrel. Кроме того, настраивает приложение для [перехватить ошибки запуска](#capture-startup-errors). Параметры по умолчанию служб IIS см. в разделе [IIS параметры раздела узла ASP.NET Core в Windows с помощью IIS](xref:host-and-deploy/iis/index#iis-options).

*Содержимое корневого* определяет, где узел ищет файлы содержимого, такие как файлы представления MVC. При запуске приложения из корневой папки проекта в корневой папки проекта используется в качестве корня содержимого. Это значение по умолчанию, используемых в [Visual Studio](https://www.visualstudio.com/) и [dotnet новые шаблоны](/dotnet/core/tools/dotnet-new).

Дополнительные сведения о настройке приложения см. в разделе [конфигурации в ASP.NET Core](xref:fundamentals/configuration/index).

> [!NOTE]
> В качестве альтернативы с помощью статического `CreateDefaultBuilder` метод, создание узла из [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) поддерживаемых подход с ASP.NET Core 2.x. Дополнительные сведения см. в разделе вкладке 1.x ASP.NET Core.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

Создание узла с помощью экземпляра [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder). Создание ведущего приложения обычно выполняется в точке входа приложения, `Main` метод. В шаблоны проектов `Main` находится в папке *Program.cs*:

[!code-csharp[Main](../common/samples/WebApplication1/Program.cs)]

`WebHostBuilder`требуется [сервера, который реализует IServer](servers/index.md). Встроенные серверы являются [Kestrel](servers/kestrel.md) и [HTTP.sys](servers/httpsys.md) (до выхода ASP.NET Core 2.0 был вызван HTTP.sys [WebListener](xref:fundamentals/servers/weblistener)). В этом примере [метод расширения UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) указывает сервер Kestrel.

*Содержимое корневого* определяет, где узел ищет файлы содержимого, такие как файлы представления MVC. Для получения содержимого корневого каталога по умолчанию `UseContentRoot` по [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1). При запуске приложения из корневой папки проекта в корневой папки проекта используется в качестве корня содержимого. Это значение по умолчанию, используемых в [Visual Studio](https://www.visualstudio.com/) и [dotnet новые шаблоны](/dotnet/core/tools/dotnet-new).

Чтобы использовать в качестве обратного прокси-сервера IIS, вызовите [UseIISIntegration](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions) как часть построения узла. `UseIISIntegration`неправильно настраивает *сервера*, таких как [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) does. `UseIISIntegration`настраивает сервер прослушивает при использовании порта и пути к базовой папке [модуль ASP.NET Core](xref:fundamentals/servers/aspnet-core-module) создание обратного прокси-сервера между Kestrel и службами IIS. Для использования IIS с ASP.NET Core `UseKestrel` и `UseIISIntegration` должен быть указан. `UseIISIntegration`активируется, только при запуске IIS или IIS Express. Дополнительные сведения см. в разделе [введение в ASP.NET Core модуля](xref:fundamentals/servers/aspnet-core-module) и [ссылки на конфигурации ASP.NET Core модуль](xref:host-and-deploy/aspnet-core-module).

Минимальную реализацию, которая настраивает узел (и приложения ASP.NET Core) включает в себя указание сервера и настройки конвейера запросов приложения:

```csharp
var host = new WebHostBuilder()
    .UseKestrel()
    .Configure(app =>
    {
        app.Run(context => context.Response.WriteAsync("Hello World!"));
    })
    .Build();

host.Run();
```

---

При настройке узла, [Настройка](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) и [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) методы могут быть предоставлены. Если `Startup` класса указан, то оно должно определять `Configure` метод. Дополнительные сведения см. в разделе [запуск приложения в ASP.NET Core](startup.md). Несколько вызовов `ConfigureServices` append друг с другом. Несколько вызовов `Configure` или `UseStartup` на `WebHostBuilder` заменить предыдущие параметры.

## <a name="host-configuration-values"></a>Значения конфигурации узла

[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) зависит от следующих подходов для задания значений конфигурации узла:

* Построитель конфигурации узла, включая переменные среды с форматом `ASPNETCORE_{configurationKey}`. Например, `ASPNETCORE_URLS`.
* Явные методы, такие как `CaptureStartupErrors`.
* [UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) и связанный ключ. При установке значения с `UseSetting`, имеет значение как строка независимо от типа.

Узел использует какой бы параметр задает значение последнего. Дополнительные сведения см. в разделе [переопределение конфигурации](#overriding-configuration) в следующем разделе.

### <a name="capture-startup-errors"></a>Запись ошибки при загрузке

Этот параметр управляет отслеживания ошибок при запуске.

**Ключ**: captureStartupErrors  
**Тип**: *bool* (`true` или `1`)  
**По умолчанию**: по умолчанию используется значение `false` Если приложение запускается с Kestrel за IIS, где значение по умолчанию — `true`.  
**Задать с помощью**:`CaptureStartupErrors`  
**Переменная среды**:`ASPNETCORE_CAPTURESTARTUPERRORS`

Когда `false`, ошибки во время запуска результат в узле выхода. Когда `true`, узел перехватывает исключения во время запуска и пытается запустить сервер.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .CaptureStartupErrors(true)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .CaptureStartupErrors(true)
    ...
```

---

### <a name="content-root"></a>Содержимое корневого

Этот параметр определяет, где ASP.NET Core начинает поиск файлов содержимого, такие как представления MVC. 

**Ключ**: contentRoot  
**Тип**: *строка*  
**По умолчанию**: по умолчанию для папки, в которой хранится сборку приложения.  
**Задать с помощью**:`UseContentRoot`  
**Переменная среды**:`ASPNETCORE_CONTENTROOT`

Содержимое корневого также используется как базовый путь для [параметр корневого веб-каталога](#web-root). Если путь не существует, узлу не удается запустить.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseContentRoot("c:\\mywebsite")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseContentRoot("c:\\mywebsite")
    ...
```

---

### <a name="detailed-errors"></a>Подробные сведения об ошибках

Определяет ли подробные ошибки должны быть зафиксированы.

**Ключ**: detailedErrors  
**Тип**: *bool* (`true` или `1`)  
**По умолчанию**: false  
**Задать с помощью**:`UseSetting`  
**Переменная среды**:`ASPNETCORE_DETAILEDERRORS`

При включении (или когда <a href="#environment">среды</a> равно `Development`), приложение записывает подробные сведения об исключениях.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

---

### <a name="environment"></a>Среда

Задает среду приложения.

**Ключ**: среды  
**Тип**: *строка*  
**По умолчанию**: рабочей среде  
**Задать с помощью**:`UseEnvironment`  
**Переменная среды**:`ASPNETCORE_ENVIRONMENT`

Среды может быть присвоено любое значение. Значения, определяемые платформой `Development`, `Staging`, и `Production`. Значения не учитывается регистр. По умолчанию *среды* считывается из `ASPNETCORE_ENVIRONMENT` переменной среды. При использовании [Visual Studio](https://www.visualstudio.com/), переменные среды может быть задан в *launchSettings.json* файла. Дополнительные сведения см. в статье [Работа с несколькими средами](xref:fundamentals/environments).

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseEnvironment("Development")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseEnvironment("Development")
    ...
```

---

### <a name="hosting-startup-assemblies"></a>Размещение загрузки сборок

Задает размещения сборок при запуске приложения.

**Ключ**: hostingStartupAssemblies  
**Тип**: *строка*  
**По умолчанию**: пустая строка  
**Задать с помощью**:`UseSetting`  
**Переменная среды**:`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`

Разделенный точками с запятой строка размещения запуска сборок для загрузки при запуске. Этот компонент впервые появился в ASP.NET Core 2.0.

Несмотря на то, что значения конфигурации по умолчанию устанавливается равным пустой строке, размещения сборок запуска всегда включать сборку приложения. Когда указаны размещения сборок при запуске, они добавляются в сборку приложения для загрузки, когда приложение создает его общие службы во время запуска.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupAssembliesKey, "assembly1;assembly2")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

Эта функция недоступна в ASP.NET Core 1.x.

---

### <a name="prefer-hosting-urls"></a>Предпочтение размещение URL-адреса

Указывает ли узел должен прослушивать URL-адресов настроены `WebHostBuilder` вместо настроенных с `IServer` реализации.

**Ключ**: preferHostingUrls  
**Тип**: *bool* (`true` или `1`)  
**По умолчанию**: true  
**Задать с помощью**:`PreferHostingUrls`  
**Переменная среды**:`ASPNETCORE_PREFERHOSTINGURLS`

Этот компонент впервые появился в ASP.NET Core 2.0.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .PreferHostingUrls(false)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

Эта функция недоступна в ASP.NET Core 1.x.

---

### <a name="prevent-hosting-startup"></a>Запретить размещение запуска

Предотвращает автоматическая загрузка размещение запуска сборок, включая размещение сборок запуска задаются сборку приложения. В разделе [Добавление компонентов приложения из внешней сборки с помощью IHostingStartup](xref:host-and-deploy/ihostingstartup) для получения дополнительной информации.

**Ключ**: preventHostingStartup  
**Тип**: *bool* (`true` или `1`)  
**По умолчанию**: false  
**Задать с помощью**:`UseSetting`  
**Переменная среды**:`ASPNETCORE_PREVENTHOSTINGSTARTUP`

Этот компонент впервые появился в ASP.NET Core 2.0.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.PreventHostingStartupKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

Эта функция недоступна в ASP.NET Core 1.x.

---

### <a name="server-urls"></a>URL-адреса сервера

Указывает IP-адреса или адреса узлов с портами и протоколы, которые сервер должен прослушивать запросы.

**Ключ**: URL-адреса  
**Тип**: *строка*  
**По умолчанию**: http://localhost: 5000  
**Задать с помощью**:`UseUrls`  
**Переменная среды**:`ASPNETCORE_URLS`

Значение, разделенных точкой с запятой (;) префиксов список URL-адрес которого сервер должен отвечать. Например, `http://localhost:123`. Используйте "\*» для указания, что сервер должен прослушивать запросы по любой IP-адрес или имя узла, используя указанный порт и протокол (например, `http://*:5000`). Протокол (`http://` или `https://`) должен быть включен, все URL-адреса. Поддерживаемые форматы различаться для разных серверов.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

Kestrel имеет собственную конфигурацию конечной точки API. Дополнительные сведения см. в статье [Реализация веб-сервера Kestrel в ASP.NET Core](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration).

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

---

### <a name="shutdown-timeout"></a>Время ожидания завершения работы

Указывает время ожидания для завершения работы веб-узла.

**Ключ**: shutdownTimeoutSeconds  
**Тип**: *int*  
**По умолчанию**: 5  
**Задать с помощью**:`UseShutdownTimeout`  
**Переменная среды**:`ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`

Несмотря на то, что ключ принимает *int* с `UseSetting` (например, `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`), `UseShutdownTimeout` принимает метод расширения `TimeSpan`. Этот компонент впервые появился в ASP.NET Core 2.0.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseShutdownTimeout(TimeSpan.FromSeconds(10))
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

Эта функция недоступна в ASP.NET Core 1.x.

---

### <a name="startup-assembly"></a>При запуске сборки

Определяет сборку для поиска `Startup` класса.

**Ключ**: startupAssembly  
**Тип**: *строка*  
**По умолчанию**: сборка приложения  
**Задать с помощью**:`UseStartup`  
**Переменная среды**:`ASPNETCORE_STARTUPASSEMBLY`

Сборки по имени (`string`) или тип (`TStartup`) может ссылаться. При наличии нескольких `UseStartup` методы вызываются, приоритет имеет последняя.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup("StartupAssemblyName")
    ...
```

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup<TStartup>()
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseStartup("StartupAssemblyName")
    ...
```

```csharp
var host = new WebHostBuilder()
    .UseStartup<TStartup>()
    ...
```

---

### <a name="web-root"></a>Персональный компьютер

Задает относительный путь для приложения статических ресурсах.

**Ключ**: webroot  
**Тип**: *строка*  
**По умолчанию**: Если не указан, значение по умолчанию — "(Content Root)/wwwroot», если путь существует. Если путь не существует, то используется поставщик холостой файла.  
**Задать с помощью**:`UseWebRoot`  
**Переменная среды**:`ASPNETCORE_WEBROOT`

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseWebRoot("public")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseWebRoot("public")
    ...
```

---

## <a name="overriding-configuration"></a>Переопределение конфигурации

Используйте [конфигурации](xref:fundamentals/configuration/index) для настройки узла. В следующем примере конфигурации узла при необходимости указывается в *hosting.json* файла. Загрузить любую конфигурацию из *hosting.json* файл может быть переопределена аргументы командной строки. Конфигурации построения (в `config`) используется для настройки узла с `UseConfiguration`.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

*Hosting.JSON*:

```json
{
    urls: "http://*:5005"
}
```

Переопределение конфигурации, обеспечиваемой `UseUrls` с *hosting.json* конфигурации первый аргументом командной строки конфигурации второй:

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        BuildWebHost(args).Run();
    }

    public static IWebHost BuildWebHost(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("hosting.json", optional: true)
            .AddCommandLine(args)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseUrls("http://*:5000")
            .UseConfiguration(config)
            .Configure(app =>
            {
                app.Run(context => 
                    context.Response.WriteAsync("Hello, World!"));
            })
            .Build();
    }
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

*Hosting.JSON*:

```json
{
    urls: "http://*:5005"
}
```

Переопределение конфигурации, обеспечиваемой `UseUrls` с *hosting.json* конфигурации первый аргументом командной строки конфигурации второй:

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("hosting.json", optional: true)
            .AddCommandLine(args)
            .Build();

        var host = new WebHostBuilder()
            .UseUrls("http://*:5000")
            .UseConfiguration(config)
            .UseKestrel()
            .Configure(app =>
            {
                app.Run(context => 
                    context.Response.WriteAsync("Hello, World!"));
            })
            .Build();

        host.Run();
    }
}
```

---

> [!NOTE]
> [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) метода расширения не может в настоящее время синтаксического анализа раздела конфигурации, возвращенных `GetSection` (например, `.UseConfiguration(Configuration.GetSection("section"))`. `GetSection` Метод фильтрует ключи в запрошенный раздел конфигурации, но оставляет имя раздела по ключам (например, `section:urls`, `section:environment`). `UseConfiguration` Метод ожидает ключи для сопоставления `WebHostBuilder` ключи (например, `urls`, `environment`). Имя раздела по ключам присутствия запрещает настраивать узла значения этого раздела. Эта проблема будет устранена в следующем выпуске. Дополнительные сведения и способы решения проблем см. в разделе [передачи раздела конфигурации в WebHostBuilder.UseConfiguration использует полное ключи](https://github.com/aspnet/Hosting/issues/839).

Для указания выполнения на определенный URL-адрес узла, требуемого значения могут передаваться в командной строке при выполнении `dotnet run`. Аргумент командной строки переопределяет `urls` значение из *hosting.json* файла, а сервер прослушивает порт 8080:

```console
dotnet run --urls "http://*:8080"
```

## <a name="starting-the-host"></a>Запуск узла

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

**Выполнить**

`Run` Метод запускает веб-приложения и блокирует вызывающий поток до завершения работы узла:

```csharp
host.Run();
```

**Start**

Запустить узел в без блокирования путем вызова его `Start` метод:

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

Если передается список URL-адресов `Start` метод, он прослушивает URL-адреса:

```csharp
var urls = new List<string>()
{
    "http://*:5000",
    "http://localhost:5001"
};

var host = new WebHostBuilder()
    .UseKestrel()
    .UseStartup<Startup>()
    .Start(urls.ToArray());

using (host)
{
    Console.ReadLine();
}
```

Приложение может инициализации и запуска нового узла с помощью предварительно настроенного значения по умолчанию `CreateDefaultBuilder` с помощью статических удобных метода. Эти методы требуют запуска серверу без вывода на консоль с [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) ожидания break (Ctrl-C или SIGINT или SIGTERM):

**Начала (приложение RequestDelegate)**

Начать с `RequestDelegate`:

```csharp
using (var host = WebHost.Start(app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

Сделать запрос в браузере для `http://localhost:5000` для получения ответа «Hello World!» `WaitForShutdown`блоки, пока не будет выполнена break (Ctrl-C или SIGINT или SIGTERM). Приложение отображается `Console.WriteLine` сообщение и ожидает keypress для выхода.

**Запуск (строковый URL-адрес, RequestDelegate приложения)**

Запуск с URL-адреса и `RequestDelegate`:

```csharp
using (var host = WebHost.Start("http://localhost:8080", app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

Дает тот же результат, как **начала (приложение RequestDelegate)**, за исключением приложение реагирует на `http://localhost:8080`.

**Запуск (действие<IRouteBuilder> routeBuilder)**

Использовать экземпляр `IRouteBuilder` ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) для использования маршрутизации по промежуточного слоя:

```csharp
using (var host = WebHost.Start(router => router
    .MapGet("hello/{name}", (req, res, data) => 
        res.WriteAsync($"Hello, {data.Values["name"]}!"))
    .MapGet("buenosdias/{name}", (req, res, data) => 
        res.WriteAsync($"Buenos dias, {data.Values["name"]}!"))
    .MapGet("throw/{message?}", (req, res, data) => 
        throw new Exception((string)data.Values["message"] ?? "Uh oh!"))
    .MapGet("{greeting}/{name}", (req, res, data) => 
        res.WriteAsync($"{data.Values["greeting"]}, {data.Values["name"]}!"))
    .MapGet("", (req, res, data) => res.WriteAsync("Hello, World!"))))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

В примере можно используйте следующие запросы браузера:

| Запрос                                    | Ответ                                 |
| ------------------------------------------ | ---------------------------------------- |
| `http://localhost:5000/hello/Martin`       | Привет, Мартин!                           |
| `http://localhost:5000/buenosdias/Catrina` | Буэнос dias Catrina!                    |
| `http://localhost:5000/throw/ooops!`       | Вызывает исключение со строкой «ooops!» |
| `http://localhost:5000/throw`              | Вызывает исключение со строкой «Uh ой!» |
| `http://localhost:5000/Sante/Kevin`        | Sante Kevin!                            |
| `http://localhost:5000`                    | Пример "Здравствуй,                             |

`WaitForShutdown`блоки, пока не будет выполнена break (Ctrl-C или SIGINT или SIGTERM). Приложение отображается `Console.WriteLine` сообщение и ожидает keypress для выхода.

**Запуск (URL-адрес, действие строки<IRouteBuilder> routeBuilder)**

Использовать URL-адреса и имени экземпляра `IRouteBuilder`:

```csharp
using (var host = WebHost.Start("http://localhost:8080", router => router
    .MapGet("hello/{name}", (req, res, data) => 
        res.WriteAsync($"Hello, {data.Values["name"]}!"))
    .MapGet("buenosdias/{name}", (req, res, data) => 
        res.WriteAsync($"Buenos dias, {data.Values["name"]}!"))
    .MapGet("throw/{message?}", (req, res, data) => 
        throw new Exception((string)data.Values["message"] ?? "Uh oh!"))
    .MapGet("{greeting}/{name}", (req, res, data) => 
        res.WriteAsync($"{data.Values["greeting"]}, {data.Values["name"]}!"))
    .MapGet("", (req, res, data) => res.WriteAsync("Hello, World!"))))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

Дает тот же результат, как **запуска (действие<IRouteBuilder> routeBuilder)**, за исключением приложение реагирует на `http://localhost:8080`.

**StartWith (действие<IApplicationBuilder> приложения)**

Укажите делегат для настройки `IApplicationBuilder`:

```csharp
using (var host = WebHost.StartWith(app => 
    app.Use(next => 
    {
        return async context => 
        {
            await context.Response.WriteAsync("Hello World!");
        };
    })))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

Сделать запрос в браузере для `http://localhost:5000` для получения ответа «Hello World!» `WaitForShutdown`блоки, пока не будет выполнена break (Ctrl-C или SIGINT или SIGTERM). Приложение отображается `Console.WriteLine` сообщение и ожидает keypress для выхода.

**StartWith (URL-адрес, действие строки<IApplicationBuilder> приложения)**

Укажите URL-адрес и делегат для настройки `IApplicationBuilder`:

```csharp
using (var host = WebHost.StartWith("http://localhost:8080", app => 
    app.Use(next => 
    {
        return async context => 
        {
            await context.Response.WriteAsync("Hello World!");
        };
    })))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

Дает тот же результат, как **StartWith (действие<IApplicationBuilder> приложения)**, за исключением приложение реагирует на `http://localhost:8080`.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

**Выполнить**

`Run` Метод запускает веб-приложения и блокирует вызывающий поток до завершения работы узла:

```csharp
host.Run();
```

**Start**

Запустить узел в без блокирования путем вызова его `Start` метод:

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

Если передается список URL-адресов `Start` метод, он прослушивает URL-адреса:


```csharp
var urls = new List<string>()
{
    "http://*:5000",
    "http://localhost:5001"
};

var host = new WebHostBuilder()
    .UseKestrel()
    .UseStartup<Startup>()
    .Start(urls.ToArray());

using (host)
{
    Console.ReadLine();
}
```

---

## <a name="ihostingenvironment-interface"></a>Интерфейс IHostingEnvironment

[IHostingEnvironment интерфейс](/aspnet/core/api/microsoft.aspnetcore.hosting.ihostingenvironment) предоставляет сведения о среде размещения веб-приложения. Используйте [внедрение конструктора](xref:fundamentals/dependency-injection) для получения `IHostingEnvironment` для использования его свойства и методы расширения:

```csharp
public class CustomFileReader
{
    private readonly IHostingEnvironment _env;

    public CustomFileReader(IHostingEnvironment env)
    {
        _env = env;
    }

    public string ReadFile(string filePath)
    {
        var fileProvider = _env.WebRootFileProvider;
        // Process the file here
    }
}
```

Объект [подход на основе соглашения о](xref:fundamentals/environments#startup-conventions) можно использовать для настройки приложения во время запуска, в зависимости от среды. Кроме того, вставка `IHostingEnvironment` в `Startup` конструктора для использования в `ConfigureServices`:

```csharp
public class Startup
{
    public Startup(IHostingEnvironment env)
    {
        HostingEnvironment = env;
    }

    public IHostingEnvironment HostingEnvironment { get; }

    public void ConfigureServices(IServiceCollection services)
    {
        if (HostingEnvironment.IsDevelopment())
        {
            // Development configuration
        }
        else
        {
            // Staging/Production configuration
        }

        var contentRootPath = HostingEnvironment.ContentRootPath;
    }
}
```

> [!NOTE]
> В дополнение к `IsDevelopment` метод расширения `IHostingEnvironment` предлагает `IsStaging`, `IsProduction`, и `IsEnvironment(string environmentName)` методы. В разделе [работа с несколькими средами](xref:fundamentals/environments) подробные сведения.

`IHostingEnvironment` Службы также могут быть добавлены непосредственно в `Configure` метода настройки конвейера обработки:

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        // In Development, use the developer exception page
        app.UseDeveloperExceptionPage();
    }
    else
    {
        // In Staging/Production, route exceptions to /error
        app.UseExceptionHandler("/error");
    }

    var contentRootPath = env.ContentRootPath;
}
```

`IHostingEnvironment`может быть введено в `Invoke` метод при создании пользовательских [по промежуточного слоя](xref:fundamentals/middleware#writing-middleware):

```csharp
public async Task Invoke(HttpContext context, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        // Configure middleware for Development
    }
    else
    {
        // Configure middleware for Staging/Production
    }

    var contentRootPath = env.ContentRootPath;
}
```

## <a name="iapplicationlifetime-interface"></a>Интерфейс IApplicationLifetime

[IApplicationLifetime](/aspnet/core/api/microsoft.aspnetcore.hosting.iapplicationlifetime) позволяет после запуска и завершения действия. Три свойства для интерфейса являются токенов отмены, используемый для регистрации `Action` методы, которые определяют события запуска и завершения работы. Имеется также `StopApplication` метод.

| Токен отмены    | Запустить &#8230; |
| --------------------- | --------------------- |
| `ApplicationStarted`  | Узел полностью запущен. |
| `ApplicationStopping` | Узел выполняет правильное завершение работы. По-прежнему может обрабатывать запросы. Завершение работы блокируется до завершения этого события. |
| `ApplicationStopped`  | Узел завершает нормальное завершение работы. Все запросы будут обрабатываться. Завершение работы блокируется до завершения этого события. |

| Метод            | Действие                                           |
| ----------------- | ------------------------------------------------ |
| `StopApplication` | Завершение запросов текущего приложения. |

```csharp
public class Startup 
{
    public void Configure(IApplicationBuilder app, IApplicationLifetime appLifetime) 
    {
        appLifetime.ApplicationStarted.Register(OnStarted);
        appLifetime.ApplicationStopping.Register(OnStopping);
        appLifetime.ApplicationStopped.Register(OnStopped);

        Console.CancelKeyPress += (sender, eventArgs) =>
        {
            appLifetime.StopApplication();
            // Don't terminate the process immediately, wait for the Main thread to exit gracefully.
            eventArgs.Cancel = true;
        };
    }

    private void OnStarted()
    {
        // Perform post-startup activities here
    }

    private void OnStopping()
    {
        // Perform on-stopping activities here
    }

    private void OnStopped()
    {
        // Perform post-stopped activities here
    }
}
```

## <a name="troubleshooting-systemargumentexception"></a>Устранение неполадок System.ArgumentException

**Применяется к только базовые ASP.NET 2.0**

Узел может быть построена, внедряя `IStartup` непосредственно в контейнер внедрения зависимостей, а не вызовом `UseStartup` или `Configure`:

```csharp
services.AddSingleton<IStartup, Startup>();
```

Если узел построен таким образом, может возникнуть следующая ошибка:

```
Unhandled Exception: System.ArgumentException: A valid non-empty application name must be provided.
```

Это происходит потому, что [applicationName(ApplicationKey)](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey) (текущая сборка) необходим для проверки на наличие `HostingStartupAttributes`. Если приложение вручную внедряет `IStartup` в контейнер внедрения зависимостей, добавьте следующий вызов `WebHostBuilder` с указанным именем сборки:

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("applicationName", "<Assembly Name>")
    ...
```

Кроме того, добавить фиктивное `Configure` для `WebHostBuilder`, который устанавливает `applicationName`(`ApplicationKey`) автоматически:

```csharp
WebHost.CreateDefaultBuilder(args)
    .Configure(_ => { })
    ...
```

**Примечание**: это необходимо только необходимые с выпуском ASP.NET Core 2.0 и только если приложение не вызывает `UseStartup` или `Configure`.

Дополнительные сведения см. в разделе [объявления: Microsoft.Extensions.PlatformAbstractions был удален (комментарий)](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938) и [StartupInjection пример](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Размещение в Windows с помощью IIS](xref:host-and-deploy/iis/index)
* [Размещение в Linux с использованием Nginx](xref:host-and-deploy/linux-nginx)
* [Размещение в Linux с использованием Apache](xref:host-and-deploy/linux-apache)
* [Узел в службе Windows](xref:host-and-deploy/windows-service)
