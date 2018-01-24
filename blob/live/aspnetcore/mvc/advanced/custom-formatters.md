---
title: "Пользовательские модули форматирования в ASP.NET Core MVC веб-API"
author: tdykstra
description: "Узнайте, как создавать и использовать пользовательские модули форматирования для веб-API в ASP.NET Core."
ms.author: tdykstra
manager: wpickett
ms.date: 02/08/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/models/custom-formatters
ms.openlocfilehash: 3a6474fdae29b170978226de74d523b20a16cd0c
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="custom-formatters-in-aspnet-core-mvc-web-apis"></a><span data-ttu-id="4d4cb-103">Пользовательские модули форматирования в ASP.NET Core MVC веб-API</span><span class="sxs-lookup"><span data-stu-id="4d4cb-103">Custom formatters in ASP.NET Core MVC web APIs</span></span>

<span data-ttu-id="4d4cb-104">По [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="4d4cb-104">By [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="4d4cb-105">ASP.NET Core MVC имеет встроенную поддержку для обмена данными в веб-API с помощью формата JSON, XML или обычного текста.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-105">ASP.NET Core MVC has built-in support for data exchange in web APIs by using JSON, XML, or plain text formats.</span></span> <span data-ttu-id="4d4cb-106">В этой статье показано, как добавить поддержку дополнительных форматов, создав пользовательские модули форматирования.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-106">This article shows how to add support for additional formats by creating custom formatters.</span></span>

<span data-ttu-id="4d4cb-107">[Просмотреть или загрузить пример из GitHub](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample).</span><span class="sxs-lookup"><span data-stu-id="4d4cb-107">[View or download sample from GitHub](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample).</span></span>

## <a name="when-to-use-custom-formatters"></a><span data-ttu-id="4d4cb-108">Когда следует использовать пользовательские модули форматирования</span><span class="sxs-lookup"><span data-stu-id="4d4cb-108">When to use custom formatters</span></span>

<span data-ttu-id="4d4cb-109">Использовать пользовательский модуль форматирования [содержимого согласования](xref:mvc/models/formatting) процесса для поддержки типа содержимого, которое не поддерживается в встроенные модули форматирования (JSON, XML и обычный текст).</span><span class="sxs-lookup"><span data-stu-id="4d4cb-109">Use a custom formatter when you want the [content negotiation](xref:mvc/models/formatting) process to support a content type that isn't supported by the built-in formatters (JSON, XML, and plain text).</span></span>

<span data-ttu-id="4d4cb-110">Например, если некоторые из клиентов для веб-API может обрабатывать [Protobuf](https://github.com/google/protobuf) формат, может потребоваться использовать Protobuf этими клиентами, поскольку он является более эффективным.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-110">For example, if some of the clients for your web API can handle the [Protobuf](https://github.com/google/protobuf) format, you might want to use Protobuf with those clients because it's more efficient.</span></span>  <span data-ttu-id="4d4cb-111">Либо можно использовать веб-API для отправки имена и адреса в [vCard](https://wikipedia.org/wiki/VCard) формат, широко распространенный формат для обмена контактных данных.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-111">Or you might want your web API to send contact names and addresses in [vCard](https://wikipedia.org/wiki/VCard) format, a commonly used format for exchanging contact data.</span></span> <span data-ttu-id="4d4cb-112">Пример приложения, описываемых в этой статье реализует простой vCard модуль форматирования.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-112">The sample app provided with this article implements a simple vCard formatter.</span></span>

## <a name="overview-of-how-to-use-a-custom-formatter"></a><span data-ttu-id="4d4cb-113">Общие сведения о том, как использовать пользовательский модуль форматирования</span><span class="sxs-lookup"><span data-stu-id="4d4cb-113">Overview of how to use a custom formatter</span></span>

<span data-ttu-id="4d4cb-114">Ниже приведены шаги, чтобы создать и использовать пользовательский модуль форматирования.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-114">Here are the steps to create and use a custom formatter:</span></span>

* <span data-ttu-id="4d4cb-115">Создайте класс модуля форматирования выходных данных, если необходимо сериализовать данные для отправки клиенту.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-115">Create an output formatter class if you want to serialize data to send to the client.</span></span>
* <span data-ttu-id="4d4cb-116">Создание класса модуль форматирования входных данных, если вы хотите выполнить десериализацию данных, полученных от клиента.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-116">Create an input formatter class if you want to deserialize data received from the client.</span></span> 
* <span data-ttu-id="4d4cb-117">Добавить экземпляры к модули форматирования `InputFormatters` и `OutputFormatters` коллекций в [MvcOptions](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.mvcoptions).</span><span class="sxs-lookup"><span data-stu-id="4d4cb-117">Add instances of your formatters to the `InputFormatters` and `OutputFormatters` collections in [MvcOptions](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.mvcoptions).</span></span>

<span data-ttu-id="4d4cb-118">В следующих разделах руководства и примеры кода для каждого из этих действий.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-118">The following sections provide guidance and code examples for each of these steps.</span></span>

## <a name="how-to-create-a-custom-formatter-class"></a><span data-ttu-id="4d4cb-119">Как создать класс пользовательский модуль форматирования</span><span class="sxs-lookup"><span data-stu-id="4d4cb-119">How to create a custom formatter class</span></span>

<span data-ttu-id="4d4cb-120">Чтобы создать модуль форматирования:</span><span class="sxs-lookup"><span data-stu-id="4d4cb-120">To create a formatter:</span></span>

* <span data-ttu-id="4d4cb-121">Создайте класс, производный от соответствующего базового класса.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-121">Derive the class from the appropriate base class.</span></span>
* <span data-ttu-id="4d4cb-122">Укажите допустимый носитель типов и кодировок в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-122">Specify valid media types and encodings in the constructor.</span></span>
* <span data-ttu-id="4d4cb-123">Переопределить `CanReadType` / `CanWriteType` методы</span><span class="sxs-lookup"><span data-stu-id="4d4cb-123">Override `CanReadType`/`CanWriteType` methods</span></span>
* <span data-ttu-id="4d4cb-124">Переопределить `ReadRequestBodyAsync` / `WriteResponseBodyAsync` методы</span><span class="sxs-lookup"><span data-stu-id="4d4cb-124">Override `ReadRequestBodyAsync`/`WriteResponseBodyAsync` methods</span></span>
  
### <a name="derive-from-the-appropriate-base-class"></a><span data-ttu-id="4d4cb-125">Является производным от соответствующего базового класса</span><span class="sxs-lookup"><span data-stu-id="4d4cb-125">Derive from the appropriate base class</span></span>

<span data-ttu-id="4d4cb-126">Для текстовых типов носителей (например, vCard), являются производными от [TextInputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textinputformatter) или [TextOutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textoutputformatter) базового класса.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-126">For text media types (for example, vCard), derive from the [TextInputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textinputformatter) or [TextOutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textoutputformatter) base class.</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=classdef)]

<span data-ttu-id="4d4cb-127">Двоичные типы являются производными от [InputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.inputformatter) или [OutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformatter) базового класса.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-127">For binary types, derive from the [InputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.inputformatter) or [OutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformatter) base class.</span></span>

### <a name="specify-valid-media-types-and-encodings"></a><span data-ttu-id="4d4cb-128">Укажите допустимый носитель типы и кодировки</span><span class="sxs-lookup"><span data-stu-id="4d4cb-128">Specify valid media types and encodings</span></span>

<span data-ttu-id="4d4cb-129">В конструкторе, укажите допустимый носитель типов и кодировок, добавив `SupportedMediaTypes` и `SupportedEncodings` коллекции.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-129">In the constructor, specify valid media types and encodings by adding to the `SupportedMediaTypes` and `SupportedEncodings` collections.</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=ctor&highlight=3,5-6)]

> [!NOTE]  
> <span data-ttu-id="4d4cb-130">Внедрение зависимостей конструктор в класс модуля форматирования не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-130">You can't do constructor dependency injection in a formatter class.</span></span> <span data-ttu-id="4d4cb-131">Например средство ведения журнала не удается получить, добавив параметр ведения журнала в конструктор.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-131">For example, you can't get a logger by adding a logger parameter to the constructor.</span></span> <span data-ttu-id="4d4cb-132">Для доступа к службам, необходимо использовать объект context, переданного в методы.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-132">To access services, you have to use the context object that gets passed in to your methods.</span></span> <span data-ttu-id="4d4cb-133">Пример кода [ниже](#read-write) показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-133">A code example [below](#read-write) shows how to do this.</span></span>

### <a name="override-canreadtypecanwritetype"></a><span data-ttu-id="4d4cb-134">Переопределить CanReadType/CanWriteType</span><span class="sxs-lookup"><span data-stu-id="4d4cb-134">Override CanReadType/CanWriteType</span></span> 

<span data-ttu-id="4d4cb-135">Укажите тип можно десериализовать в или сериализации из путем переопределения `CanReadType` или `CanWriteType` методы.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-135">Specify the type you can deserialize into or serialize from by overriding the `CanReadType` or `CanWriteType` methods.</span></span> <span data-ttu-id="4d4cb-136">Например, можно только будет создание vCard текст из `Contact` и наоборот.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-136">For example, you might only be able to create vCard text from a `Contact` type and vice versa.</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=canwritetype)]

#### <a name="the-canwriteresult-method"></a><span data-ttu-id="4d4cb-137">Метод CanWriteResult</span><span class="sxs-lookup"><span data-stu-id="4d4cb-137">The CanWriteResult method</span></span>

<span data-ttu-id="4d4cb-138">В некоторых сценариях необходимо переопределить `CanWriteResult` вместо `CanWriteType`.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-138">In some scenarios you have to override `CanWriteResult` instead of `CanWriteType`.</span></span> <span data-ttu-id="4d4cb-139">Используйте `CanWriteResult` , если выполняются следующие условия:</span><span class="sxs-lookup"><span data-stu-id="4d4cb-139">Use `CanWriteResult` if the following conditions are true:</span></span>

  * <span data-ttu-id="4d4cb-140">Метод действия возвращает класс модели.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-140">Your action method returns a model class.</span></span>
  * <span data-ttu-id="4d4cb-141">Существуют производные классы, которые могут возвращаться во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-141">There are derived classes which might be returned at runtime.</span></span>
  * <span data-ttu-id="4d4cb-142">Необходимо знать во время выполнения, который производным классом, возвращаемого действием.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-142">You need to know at runtime which derived class was returned by the action.</span></span>  

<span data-ttu-id="4d4cb-143">Предположим, что подпись метода действие возвращает `Person` типа, но он может возвращать `Student` или `Instructor` тип, производный от `Person`.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-143">For example, suppose your action method signature returns a `Person` type, but it may return a `Student` or `Instructor` type that derives from `Person`.</span></span> <span data-ttu-id="4d4cb-144">Если требуется, чтобы модуль форматирования для обработки только `Student` объектов, проверьте тип [объекта](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformattercanwritecontext#Microsoft_AspNetCore_Mvc_Formatters_OutputFormatterCanWriteContext_Object) в контекст объект, предоставляемый для `CanWriteResult` метод.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-144">If you want your formatter to handle only `Student` objects, check the type of [Object](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformattercanwritecontext#Microsoft_AspNetCore_Mvc_Formatters_OutputFormatterCanWriteContext_Object) in the context object provided to the `CanWriteResult` method.</span></span> <span data-ttu-id="4d4cb-145">Обратите внимание, что нет необходимости использовать `CanWriteResult` при возвращении операции `IActionResult`; в этом случае `CanWriteType` метод получает тип среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-145">Note that it's not necessary to use `CanWriteResult` when the action method returns `IActionResult`; in that case, the `CanWriteType` method receives the runtime type.</span></span>

<a id="read-write"></a>
### <a name="override-readrequestbodyasyncwriteresponsebodyasync"></a><span data-ttu-id="4d4cb-146">Override ReadRequestBodyAsync/WriteResponseBodyAsync</span><span class="sxs-lookup"><span data-stu-id="4d4cb-146">Override ReadRequestBodyAsync/WriteResponseBodyAsync</span></span> 

<span data-ttu-id="4d4cb-147">Выполняют реальную работу десериализации или сериализации в `ReadRequestBodyAsync` или `WriteResponseBodyAsync`.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-147">You do the actual work of deserializing or serializing in `ReadRequestBodyAsync` or `WriteResponseBodyAsync`.</span></span>  <span data-ttu-id="4d4cb-148">Выделенные строки в следующем примере показано, как получить службы из контейнера внедрения зависимостей (их не удается получить из параметров конструктора).</span><span class="sxs-lookup"><span data-stu-id="4d4cb-148">The highlighted lines in the following example show how to get services from the dependency injection container (you can't get them from constructor parameters).</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=writeresponse&highlight=3-4)]

## <a name="how-to-configure-mvc-to-use-a-custom-formatter"></a><span data-ttu-id="4d4cb-149">Настройка MVC, чтобы использовать пользовательский модуль форматирования</span><span class="sxs-lookup"><span data-stu-id="4d4cb-149">How to configure MVC to use a custom formatter</span></span>
 
<span data-ttu-id="4d4cb-150">Чтобы использовать пользовательский модуль форматирования, добавьте экземпляр класса модуля форматирования для `InputFormatters` или `OutputFormatters` коллекции.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-150">To use a custom formatter, add an instance of the formatter class to the `InputFormatters` or `OutputFormatters` collection.</span></span>

[!code-csharp[Main](custom-formatters/sample/Startup.cs?name=mvcoptions&highlight=3-4)]

<span data-ttu-id="4d4cb-151">Модули форматирования, вычисляются в порядке, в каком они добавлены.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-151">Formatters are evaluated in the order you insert them.</span></span> <span data-ttu-id="4d4cb-152">Первый из них имеет приоритет.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-152">The first one takes precedence.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4d4cb-153">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="4d4cb-153">Next steps</span></span>

<span data-ttu-id="4d4cb-154">В разделе [образец приложения](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample), который реализует простой vCard входных данных и модули форматирования выходных данных.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-154">See the [sample application](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample), which implements simple vCard input and output formatters.</span></span>  <span data-ttu-id="4d4cb-155">Приложение считывает и записывает визитные карточки, которые выглядят как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="4d4cb-155">The application reads and writes vCards that look like the following example:</span></span>

```
BEGIN:VCARD
VERSION:2.1
N:Davolio;Nancy
FN:Nancy Davolio
UID:20293482-9240-4d68-b475-325df4a83728
END:VCARD
```

<span data-ttu-id="4d4cb-156">Чтобы увидеть vCard выходных данных, запустите приложение и отправка запроса Get с Accept заголовок «текст/vcard» для `http://localhost:63313/api/contacts/` (при запуске из Visual Studio) или `http://localhost:5000/api/contacts/` (при запуске из командной строки).</span><span class="sxs-lookup"><span data-stu-id="4d4cb-156">To see vCard output, run the application and send a Get request with Accept header "text/vcard" to `http://localhost:63313/api/contacts/` (when running from Visual Studio) or `http://localhost:5000/api/contacts/` (when running from the command line).</span></span>

<span data-ttu-id="4d4cb-157">Чтобы добавить ее в памяти коллекцию контактов, отправьте запрос Post в URL, с заголовка Content-Type «text/vcard» и текст vCard в тексте, отформатированных как в приведенном выше примере.</span><span class="sxs-lookup"><span data-stu-id="4d4cb-157">To add a vCard to the in-memory collection of contacts, send a Post request to the same URL, with Content-Type header "text/vcard" and with vCard text in the body, formatted like the example above.</span></span>