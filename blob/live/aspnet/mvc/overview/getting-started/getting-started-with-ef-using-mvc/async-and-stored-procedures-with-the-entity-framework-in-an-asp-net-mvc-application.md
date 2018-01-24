---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: "Async и хранимых процедур с платформой Entity Framework в приложении ASP.NET MVC | Документы Microsoft"
author: tdykstra
description: "Contoso университета примера веб-приложения показано, как создавать приложения ASP.NET MVC 5 с помощью Entity Framework 6 Code First и Visual Studio..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/07/2014
ms.topic: article
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5b4904037838441942ea266ce71d735642d0a717
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="async-and-stored-procedures-with-the-entity-framework-in-an-aspnet-mvc-application"></a><span data-ttu-id="bbc8f-103">Async и хранимых процедур с платформой Entity Framework в приложении ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="bbc8f-103">Async and Stored Procedures with the Entity Framework in an ASP.NET MVC Application</span></span>
====================
<span data-ttu-id="bbc8f-104">По [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="bbc8f-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="bbc8f-105">[Загрузка завершенного проекта](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) или [скачать PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span><span class="sxs-lookup"><span data-stu-id="bbc8f-105">[Download Completed Project](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) or [Download PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span></span>

> <span data-ttu-id="bbc8f-106">Contoso университета примера веб-приложения показано, как создавать приложения ASP.NET MVC 5 с помощью Entity Framework 6 Code First и Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 Code First and Visual Studio 2013.</span></span> <span data-ttu-id="bbc8f-107">Сведения о учебника серии см [в первом учебнике ряда](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="bbc8f-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>


<span data-ttu-id="bbc8f-108">В предыдущих учебниках вы узнали, как для чтения и обновления данных с использованием синхронной модели программирования.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-108">In earlier tutorials you learned how to read and update data using the synchronous programming model.</span></span> <span data-ttu-id="bbc8f-109">В этом учебнике вы научитесь реализации асинхронной модели программирования.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-109">In this tutorial you see how to implement the asynchronous programming model.</span></span> <span data-ttu-id="bbc8f-110">Асинхронного кода могут помочь приложения работают лучше, поскольку это повышает эффективность использования ресурсов сервера.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-110">Asynchronous code can help an application perform better because it makes better use of server resources.</span></span>

<span data-ttu-id="bbc8f-111">В этом учебнике вы также увидите способ использования хранимых процедур для операций вставки, обновления и delete для сущности.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-111">In this tutorial you'll also see how to use stored procedures for insert, update, and delete operations on an entity.</span></span>

<span data-ttu-id="bbc8f-112">Наконец будет повторно развернуть приложение в Azure, а также все изменения базы данных, которые реализованы с момента при первом развертывании.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-112">Finally, you'll redeploy the application to Azure, along with all of the database changes that you've implemented since the first time you deployed.</span></span>

<span data-ttu-id="bbc8f-113">Некоторые страницы, которые вы будете работать с рисунках ниже.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-113">The following illustrations show some of the pages that you'll work with.</span></span>

![Страница отделов](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Создание подразделения](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="why-bother-with-asynchronous-code"></a><span data-ttu-id="bbc8f-116">Зачем с асинхронного кода</span><span class="sxs-lookup"><span data-stu-id="bbc8f-116">Why bother with asynchronous code</span></span>

<span data-ttu-id="bbc8f-117">Ограниченное число потоков, доступных на веб-сервере, и в случае высокой загрузки все доступные потоки быть используется.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-117">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="bbc8f-118">В этом случае сервер может обработать новые запросы, пока не освободятся потоков.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-118">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="bbc8f-119">С синхронным кодом большое количество потоков может блокировали они не выполняя фактически действия из-за ожидания завершения ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-119">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="bbc8f-120">Асинхронный код когда процесс ожидает ввода-вывода завершить, свой поток освобождается для сервера, используемые для обработки других запросов.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-120">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="bbc8f-121">В результате асинхронного кода включает ресурсы сервера для более эффективного использования и что сервер включен для обработки большего объема трафика без задержек.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-121">As a result, asynchronous code enables server resources to be use more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="bbc8f-122">В более ранних версиях .NET, создания и тестирования асинхронного кода была сложной задачей, вероятностью ошибок и трудно отлаживать.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-122">In earlier versions of .NET, writing and testing asynchronous code was complex, error prone, and hard to debug.</span></span> <span data-ttu-id="bbc8f-123">В .NET 4.5, записи, тестирования и отладки асинхронный код таким образом намного проще, следует обычно написать асинхронный код, если нет причины недоступны для.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-123">In .NET 4.5, writing, testing, and debugging asynchronous code is so much easier that you should generally write asynchronous code unless you have a reason not to.</span></span> <span data-ttu-id="bbc8f-124">Асинхронного кода привести небольшого количества временных затрат, но в ситуациях сниженным трафиком, снижение производительности будет незначительным, при в ситуациях с высоким трафиком, является существенным потенциальное улучшение производительности.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-124">Asynchronous code does introduce a small amount of overhead, but for low traffic situations the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="bbc8f-125">Дополнительные сведения об асинхронном программировании см. в разделе [Поддержка асинхронного использования .NET 4.5 во избежание блокирующих вызовов](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async).</span><span class="sxs-lookup"><span data-stu-id="bbc8f-125">For more information about asynchronous programming, see [Use .NET 4.5's async support to avoid blocking calls](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async).</span></span>

## <a name="create-the-department-controller"></a><span data-ttu-id="bbc8f-126">Создание контроллера отдела</span><span class="sxs-lookup"><span data-stu-id="bbc8f-126">Create the Department controller</span></span>

<span data-ttu-id="bbc8f-127">Создание подразделения контроллера, так же, как это было сделано ранее контроллеров, но в этот раз выберите **Использование асинхронного контроллера** действия флажок.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-127">Create a Department controller the same way you did the earlier controllers, except this time select the **Use async controller** actions check box.</span></span>

![Представление формирования отдел контроллера](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="bbc8f-129">Следующие основные особенности Показать, что был добавлен на синхронный код для `Index` метод создания асинхронного:</span><span class="sxs-lookup"><span data-stu-id="bbc8f-129">The following highlights show what was added to the synchronous code for the `Index` method to make it asynchronous:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

<span data-ttu-id="bbc8f-130">Четыре изменения были применены к включить запрос к базе данных Entity Framework для асинхронного выполнения:</span><span class="sxs-lookup"><span data-stu-id="bbc8f-130">Four changes were applied to enable the Entity Framework database query to execute asynchronously:</span></span>

- <span data-ttu-id="bbc8f-131">Метод помечен атрибутом `async` ключевое слово, которое указывает компилятору создавать обратные вызовы для части тела метода и автоматически создавать `Task<ActionResult>` возвращаемый объект.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-131">The method is marked with the `async` keyword, which tells the compiler to generate callbacks for parts of the method body and to automatically create the `Task<ActionResult>` object that is returned.</span></span>
- <span data-ttu-id="bbc8f-132">Возвращаемый тип был изменен с `ActionResult` для `Task<ActionResult>`.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-132">The return type was changed from `ActionResult` to `Task<ActionResult>`.</span></span> <span data-ttu-id="bbc8f-133">`Task<T>` Тип представляет выполняющуюся работу с результат типа `T`.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-133">The `Task<T>` type represents ongoing work with a result of type `T`.</span></span>
- <span data-ttu-id="bbc8f-134">`await` Была применена ключевое слово для вызова веб-службы.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-134">The `await` keyword was applied to the web service call.</span></span> <span data-ttu-id="bbc8f-135">Если компилятор обнаруживает ключевое слово, за кулисами он разбивает метод на две части.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-135">When the compiler sees this keyword, behind the scenes it splits the method into two parts.</span></span> <span data-ttu-id="bbc8f-136">Первая часть завершается с операцией, которая запускается в асинхронном режиме.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-136">The first part ends with the operation that is started asynchronously.</span></span> <span data-ttu-id="bbc8f-137">Вторая часть переводится в метод обратного вызова, вызываемый после завершения операции.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-137">The second part is put into a callback method that is called when the operation completes.</span></span>
- <span data-ttu-id="bbc8f-138">Асинхронная версия объекта `ToList` метод расширения был вызван.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-138">The asynchronous version of the `ToList` extension method was called.</span></span>

<span data-ttu-id="bbc8f-139">Почему является `departments.ToList` инструкции изменен, но не `departments = db.Departments` инструкции?</span><span class="sxs-lookup"><span data-stu-id="bbc8f-139">Why is the `departments.ToList` statement modified but not the `departments = db.Departments` statement?</span></span> <span data-ttu-id="bbc8f-140">Причина заключается в асинхронное выполнение только инструкции, вызывающие запросов или команд отправки в базу данных.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-140">The reason is that only statements that cause queries or commands to be sent to the database are executed asynchronously.</span></span> <span data-ttu-id="bbc8f-141">`departments = db.Departments` Устанавливает инструкции запроса, но запрос не выполняется до `ToList` вызывается метод.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-141">The `departments = db.Departments` statement sets up a query but the query is not executed until the `ToList` method is called.</span></span> <span data-ttu-id="bbc8f-142">Таким образом только `ToList` метод выполняется асинхронно.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-142">Therefore, only the `ToList` method is executed asynchronously.</span></span>

<span data-ttu-id="bbc8f-143">В `Details` метод и `HttpGet` `Edit` и `Delete` методы, `Find` метод является тот, который вызывает запрос для отправки в базу данных, то есть метод, который получает асинхронное выполнение:</span><span class="sxs-lookup"><span data-stu-id="bbc8f-143">In the `Details` method and the `HttpGet` `Edit` and `Delete` methods, the `Find` method is the one that causes a query to be sent to the database, so that's the method that gets executed asynchronously:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

<span data-ttu-id="bbc8f-144">В `Create`, `HttpPost Edit`, и `DeleteConfirmed` это методы, `SaveChanges` вызов метода, который вызывает команду для выполнения, не таких инструкциях, как `db.Departments.Add(department)` только благодаря чему сущностей в памяти, чтобы изменить.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-144">In the `Create`, `HttpPost Edit`, and `DeleteConfirmed` methods, it is the `SaveChanges` method call that causes a command to be executed, not statements such as `db.Departments.Add(department)` which only cause entities in memory to be modified.</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

<span data-ttu-id="bbc8f-145">Откройте *Views\Department\Index.cshtml*и замените код шаблона с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="bbc8f-145">Open *Views\Department\Index.cshtml*, and replace the template code with the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

<span data-ttu-id="bbc8f-146">Этот код изменяет заголовок из индекса по отделам, перемещает имя администратора справа и предоставляет полное имя администратора.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-146">This code changes the title from Index to Departments, moves the Administrator name to the right, and provides the full name of the administrator.</span></span>

<span data-ttu-id="bbc8f-147">Создания, удаления, сведения и изменения представлений, изменить заголовок для `InstructorID` поля «Administrator» так же, как изменить поля названия отдела «Отдел» в представлениях курса.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-147">In the Create, Delete, Details, and Edit views, change the caption for the `InstructorID` field to "Administrator" the same way you changed the department name field to "Department" in the Course views.</span></span>

<span data-ttu-id="bbc8f-148">Создание и изменение представления используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="bbc8f-148">In the Create and Edit views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

<span data-ttu-id="bbc8f-149">В Delete и сведения о представлениях используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="bbc8f-149">In the Delete and Details views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="bbc8f-150">Запустите приложение и нажмите кнопку **отделы** вкладки.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-150">Run the application, and click the **Departments** tab.</span></span>

![Страница отделов](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="bbc8f-152">Все, что работает так же, как и другие контроллеры, но в этом контроллере все запросы SQL выполняются асинхронно.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-152">Everything works the same as in the other controllers, but in this controller all of the SQL queries are executing asynchronously.</span></span>

<span data-ttu-id="bbc8f-153">Некоторые аспекты, которые следует учитывать при использовании асинхронного программирования с платформой Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-153">Some things to be aware of when you are using asynchronous programming with the Entity Framework:</span></span>

- <span data-ttu-id="bbc8f-154">Асинхронного кода не является потокобезопасным.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-154">The async code is not thread safe.</span></span> <span data-ttu-id="bbc8f-155">Другими словами другими словами, не пытайтесь выполнить несколько операций в параллельном режиме, используя один и тот же экземпляр контекста.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-155">In other words, in other words, don't try to do multiple operations in parallel using the same context instance.</span></span>
- <span data-ttu-id="bbc8f-156">Если вы хотите использовать преимущества производительности асинхронного кода, убедитесь, что ни одну библиотеку пакеты, которые вы используете (например, для разбиения на страницы), также используют асинхронный, вызывающие методы Entity Framework, которые запросы, отправляемые в базу данных.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-156">If you want to take advantage of the performance benefits of async code, make sure that any library packages that you're using (such as for paging), also use async if they call any Entity Framework methods that cause queries to be sent to the database.</span></span>

## <a name="use-stored-procedures-for-inserting-updating-and-deleting"></a><span data-ttu-id="bbc8f-157">Использование хранимых процедур для вставки, обновления и удаления</span><span class="sxs-lookup"><span data-stu-id="bbc8f-157">Use stored procedures for inserting, updating, and deleting</span></span>

<span data-ttu-id="bbc8f-158">Некоторые разработчики и Администраторы баз данных предпочитают использовать хранимые процедуры для доступа к базе данных.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-158">Some developers and DBAs prefer to use stored procedures for database access.</span></span> <span data-ttu-id="bbc8f-159">Данные, с помощью хранимой процедуры, можно получить в более ранних версиях платформы Entity Framework [выполнения необработанных запросов SQL](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), но нельзя указать EF с помощью хранимых процедур для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-159">In earlier versions of Entity Framework you can retrieve data using a stored procedure by [executing a raw SQL query](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), but you can't instruct EF to use stored procedures for update operations.</span></span> <span data-ttu-id="bbc8f-160">EF 6 можно легко настроить Code First с помощью хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-160">In EF 6 it's easy to configure Code First to use stored procedures.</span></span>

1. <span data-ttu-id="bbc8f-161">В *DAL\SchoolContext.cs*, добавьте выделенный код для `OnModelCreating` метод.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-161">In *DAL\SchoolContext.cs*, add the highlighted code to the `OnModelCreating` method.</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    <span data-ttu-id="bbc8f-162">Этот код дает Entity Framework, чтобы использовать сохраненные процедуры для вставки, обновления и удаления операций на `Department` сущности.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-162">This code instructs Entity Framework to use stored procedures for insert, update, and delete operations on the `Department` entity.</span></span>
2. <span data-ttu-id="bbc8f-163">В консоли управления пакета введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bbc8f-163">In Package Manage Console, enter the following command:</span></span>

    `add-migration DepartmentSP`

    <span data-ttu-id="bbc8f-164">Откройте *миграций\&lt; отметка времени&gt;\_DepartmentSP.cs* кода в `Up` метод, который создает вставки, обновления и удаления хранимых процедур:</span><span class="sxs-lookup"><span data-stu-id="bbc8f-164">Open *Migrations\&lt;timestamp&gt;\_DepartmentSP.cs* to see the code in the `Up` method that creates Insert, Update, and Delete stored procedures:</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
- <span data-ttu-id="bbc8f-165">В консоли управления пакета введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bbc8f-165">In Package Manage Console, enter the following command:</span></span>

    `update-database`
- <span data-ttu-id="bbc8f-166">Запустите приложение в режиме отладки, нажмите кнопку **отделы** , а затем щелкните **создать новый**.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-166">Run the application in debug mode, click the **Departments** tab, and then click **Create New**.</span></span>
- <span data-ttu-id="bbc8f-167">Введите данные для нового отдела и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-167">Enter data for a new department, and then click **Create**.</span></span>

    ![Создание подразделения](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
- <span data-ttu-id="bbc8f-169">В Visual Studio, просмотрите журналы в **вывода** окна, чтобы увидеть, что хранимая процедура использовался для вставки новой строки отдела.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-169">In Visual Studio, look at the logs in the **Output** window to see that a stored procedure was used to insert the new Department row.</span></span>

    ![Отдел Insert SP](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="bbc8f-171">Код сначала создает имена по умолчанию хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-171">Code First creates default stored procedure names.</span></span> <span data-ttu-id="bbc8f-172">При использовании существующей базы данных, может потребоваться настроить имен хранимых процедур для использования хранимых процедур в базе данных уже определен.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-172">If you are using an existing database, you might need to customize the stored procedure names in order to use stored procedures already defined in the database.</span></span> <span data-ttu-id="bbc8f-173">Сведения о том, как это сделать, см. в разделе [Entity Framework код первого вставки/обновления/удаления хранимых процедур](https://msdn.microsoft.com/en-us/data/dn468673).</span><span class="sxs-lookup"><span data-stu-id="bbc8f-173">For information about how to do that, see [Entity Framework Code First Insert/Update/Delete Stored Procedures](https://msdn.microsoft.com/en-us/data/dn468673).</span></span>

<span data-ttu-id="bbc8f-174">Если вы хотите настроить, что созданный хранимых процедур не, можно редактировать формирования шаблонов код для миграций `Up` метод, который создает хранимую процедуру.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-174">If you want to customize what generated stored procedures do, you can edit the scaffolded code for the migrations `Up` method that creates the stored procedure.</span></span> <span data-ttu-id="bbc8f-175">В этом случае изменения будут отражены каждый раз, когда, выполняется миграция и будут применяться в производственной базе данных, миграция выполняется автоматически в производственной среде после развертывания.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-175">That way your changes are reflected whenever that migration is run and will be applied to your production database when migrations runs automatically in production after deployment.</span></span>

<span data-ttu-id="bbc8f-176">Чтобы изменить существующую хранимую процедуру, которая была создана в предыдущей миграции можно использовать для создания пустого миграции команды Add-Migration и вручную написать код, вызывающий [AlterStoredProcedure](https://msdn.microsoft.com/en-us/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) метод .</span><span class="sxs-lookup"><span data-stu-id="bbc8f-176">If you want to change an existing stored procedure that was created in a previous migration, you can use the Add-Migration command to generate a blank migration, and then manually write code that calls the [AlterStoredProcedure](https://msdn.microsoft.com/en-us/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) method.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="bbc8f-177">Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="bbc8f-177">Deploy to Azure</span></span>

<span data-ttu-id="bbc8f-178">В этом разделе необходимо выполнить дополнительный **развертыванию приложения в Azure** статьи [миграция и развертывание](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) учебника этой серии.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-178">This section requires you to have completed the optional **Deploying the app to Azure** section in the [Migrations and Deployment](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial of this series.</span></span> <span data-ttu-id="bbc8f-179">Если у вас есть ошибки миграции, которые можно разрешить путем удаления базы данных в локальном проекте, пропустите этот раздел.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-179">If you had migrations errors that you resolved by deleting the database in your local project, skip this section.</span></span>

1. <span data-ttu-id="bbc8f-180">В Visual Studio щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **публикации** в контекстном меню.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-180">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
2. <span data-ttu-id="bbc8f-181">Нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-181">Click **Publish**.</span></span>

    <span data-ttu-id="bbc8f-182">Visual Studio развертывает приложение в Azure, и это приложение открывается в браузере по умолчанию, работающих в Azure.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-182">Visual Studio deploys the application to Azure, and the application opens in your default browser, running in Azure.</span></span>
3. <span data-ttu-id="bbc8f-183">Протестируйте приложение, чтобы проверить его работы.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-183">Test the application to verify it's working.</span></span>

    <span data-ttu-id="bbc8f-184">При первом запуске страницы, который обращается к базе данных, платформа Entity Framework запускает все миграций `Up` методы, необходимые для перевода базы данных в актуальном состоянии с текущей моделью данных.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-184">The first time you run a page that accesses the database, the Entity Framework runs all of the migrations `Up` methods required to bring the database up to date with the current data model.</span></span> <span data-ttu-id="bbc8f-185">Теперь можно использовать все веб-страниц, добавленных с момента последнего развертывания, включая страницы отдела, которые вы добавили в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-185">You can now use all of the web pages that you added since the last time you deployed, including the Department pages that you added in this tutorial.</span></span>

## <a name="summary"></a><span data-ttu-id="bbc8f-186">Сводка</span><span class="sxs-lookup"><span data-stu-id="bbc8f-186">Summary</span></span>

<span data-ttu-id="bbc8f-187">В этом учебнике показано, как повысить эффективность работы сервера путем написания кода, которое выполняется асинхронно и как использовать хранимые процедуры для вставки, обновления и удаления операций.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-187">In this tutorial you saw how to improve server efficiency by writing code that executes asynchronously, and how to use stored procedures for insert, update, and delete operations.</span></span> <span data-ttu-id="bbc8f-188">В следующем уроке вы увидите, как предотвратить потерю данных, когда несколько пользователей одновременно изменять одну запись одновременно.</span><span class="sxs-lookup"><span data-stu-id="bbc8f-188">In the next tutorial, you'll see how to prevent data loss when multiple users try to edit the same record at the same time.</span></span>

<span data-ttu-id="bbc8f-189">Ссылки на другие ресурсы Entity Framework можно найти в [доступа к данным ASP.NET - рекомендуется использовать ресурсы](../../../../whitepapers/aspnet-data-access-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="bbc8f-189">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="bbc8f-190">[Назад](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Вперед](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="bbc8f-190">[Previous](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>