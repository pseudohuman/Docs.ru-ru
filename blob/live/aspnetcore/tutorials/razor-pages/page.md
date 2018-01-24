---
title: "Сформированные страницы Razor Pages в ASP.NET Core"
author: rick-anderson
description: "Описание страниц Razor Pages, созданных путем формирования шаблонов."
ms.author: riande
manager: wpickett
ms.date: 09/27/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages/page
ms.openlocfilehash: ad2a2b48beb31dddcfd78a8aab79ac58ccda28f3
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="scaffolded-razor-pages-in-aspnet-core"></a><span data-ttu-id="2c39c-103">Сформированные страницы Razor Pages в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="2c39c-103">Scaffolded Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="2c39c-104">Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)</span><span class="sxs-lookup"><span data-stu-id="2c39c-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="2c39c-105">В этом руководстве рассматриваются страницы Razor Pages, созданные в ходе формирования шаблонов в предыдущем руководстве по [добавлению модели](xref:tutorials/razor-pages/model#scaffold-the-movie-model).</span><span class="sxs-lookup"><span data-stu-id="2c39c-105">This tutorial examines the Razor Pages created by scaffolding in the previous tutorial topic [Adding a model](xref:tutorials/razor-pages/model#scaffold-the-movie-model).</span></span> 

<span data-ttu-id="2c39c-106">[Просмотрите или скачайте](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie) пример.</span><span class="sxs-lookup"><span data-stu-id="2c39c-106">[View or download](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie) sample.</span></span>

## <a name="the-create-delete-details-and-edit-pages"></a><span data-ttu-id="2c39c-107">Страницы Create, Delete, Details и Edit</span><span class="sxs-lookup"><span data-stu-id="2c39c-107">The Create, Delete, Details, and Edit pages.</span></span>

<span data-ttu-id="2c39c-108">Изучите страничную модель *Pages/Movies/Index.cshtml.cs*: [!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs)]</span><span class="sxs-lookup"><span data-stu-id="2c39c-108">Examine the *Pages/Movies/Index.cshtml.cs* Page Model: [!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs)]</span></span>

<span data-ttu-id="2c39c-109">Страницы Razor Pages являются производными от `PageModel`.</span><span class="sxs-lookup"><span data-stu-id="2c39c-109">Razor Pages are derived from `PageModel`.</span></span> <span data-ttu-id="2c39c-110">Как правило, класс, производный от `PageModel`, называется `<PageName>Model`.</span><span class="sxs-lookup"><span data-stu-id="2c39c-110">By convention, the `PageModel`-derived class is called `<PageName>Model`.</span></span> <span data-ttu-id="2c39c-111">Используя [внедрение зависимостей](xref:fundamentals/dependency-injection), конструктор добавляет на страницу `MovieContext`.</span><span class="sxs-lookup"><span data-stu-id="2c39c-111">The constructor uses [dependency injection](xref:fundamentals/dependency-injection) to add the `MovieContext` to the page.</span></span> <span data-ttu-id="2c39c-112">Этому шаблону соответствуют все сформированные страницы.</span><span class="sxs-lookup"><span data-stu-id="2c39c-112">All the scaffolded pages follow this pattern.</span></span> <span data-ttu-id="2c39c-113">Дополнительные сведения об асинхронном программировании с использованием Entity Framework см. в разделе [Асинхронный код](xref:data/ef-rp/intro#asynchronous-code).</span><span class="sxs-lookup"><span data-stu-id="2c39c-113">See [Asynchronous code](xref:data/ef-rp/intro#asynchronous-code) for more information on asynchronous programing with Entity Framework.</span></span>

<span data-ttu-id="2c39c-114">Когда к странице направляется запрос, метод `OnGetAsync` возвращает на страницу Razor список фильмов.</span><span class="sxs-lookup"><span data-stu-id="2c39c-114">When a request is made for the page, the `OnGetAsync` method returns a list of movies to the Razor Page.</span></span> <span data-ttu-id="2c39c-115">На странице Razor вызывается метод `OnGetAsync` или `OnGet`, инициализирующий состояние для страницы.</span><span class="sxs-lookup"><span data-stu-id="2c39c-115">`OnGetAsync` or `OnGet` is called on a Razor Page to initialize the state for the page.</span></span> <span data-ttu-id="2c39c-116">В этом случае `OnGetAsync` возвращает список фильмов для отображения.</span><span class="sxs-lookup"><span data-stu-id="2c39c-116">In this case, `OnGetAsync` gets a list of movies and displays them.</span></span> 

<span data-ttu-id="2c39c-117">Когда `OnGet` возвращает `void` или `OnGetAsync` возвращает `Task`, возвращаемый метод не используется.</span><span class="sxs-lookup"><span data-stu-id="2c39c-117">When `OnGet` returns `void` or `OnGetAsync` returns`Task`, no return method is used.</span></span> <span data-ttu-id="2c39c-118">Если возвращаемый тип — `IActionResult` или `Task<IActionResult>`, необходимо предоставить оператор return.</span><span class="sxs-lookup"><span data-stu-id="2c39c-118">When the return type is `IActionResult` or `Task<IActionResult>`, a return statement must be provided.</span></span> <span data-ttu-id="2c39c-119">Например, метод `OnPostAsync` *Pages/Movies/Create.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="2c39c-119">For example, the *Pages/Movies/Create.cshtml.cs* `OnPostAsync` method:</span></span>

<!-- TODO - replace with snippet
[!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Create.cshtml.cs?name=snippetALL)]
 -->

```csharp
public async Task<IActionResult> OnPostAsync()
{
    if (!ModelState.IsValid)
    {
        return Page();
    }

    _context.Movie.Add(Movie);
    await _context.SaveChangesAsync();

    return RedirectToPage("./Index");
}
```
<span data-ttu-id="2c39c-120">Изучите страницу Razor *Pages/Movies/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="2c39c-120">Examine the *Pages/Movies/Index.cshtml* Razor Page:</span></span>

[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml)]

<span data-ttu-id="2c39c-121">Razor может выполнять переход с HTML на C# или на разметку Razor.</span><span class="sxs-lookup"><span data-stu-id="2c39c-121">Razor can transition from HTML into C# or into Razor-specific markup.</span></span> <span data-ttu-id="2c39c-122">Если за символом `@` следует [зарезервированное ключевое слово Razor](xref:mvc/views/razor#razor-reserved-keywords), он переходит на разметку Razor, а если нет, то на C#.</span><span class="sxs-lookup"><span data-stu-id="2c39c-122">When an `@` symbol is followed by a [Razor reserved keyword](xref:mvc/views/razor#razor-reserved-keywords), it transitions into Razor-specific markup, otherwise it transitions into C#.</span></span>

<span data-ttu-id="2c39c-123">Директива Razor `@page` преобразует файл в действие MVC &mdash;, а значит, он может обрабатывать запросы.</span><span class="sxs-lookup"><span data-stu-id="2c39c-123">The `@page` Razor directive makes the file into an MVC action &mdash; which means that it can handle requests.</span></span> <span data-ttu-id="2c39c-124">Директива `@page` должна быть первой директивой Razor на странице.</span><span class="sxs-lookup"><span data-stu-id="2c39c-124">`@page` must be the first Razor directive on a page.</span></span> <span data-ttu-id="2c39c-125">`@page` — это пример перехода на разметку Razor.</span><span class="sxs-lookup"><span data-stu-id="2c39c-125">`@page` is an example of transitioning into Razor-specific markup.</span></span> <span data-ttu-id="2c39c-126">Дополнительные сведения см. в статье [Синтаксис Razor](xref:mvc/views/razor#razor-syntax).</span><span class="sxs-lookup"><span data-stu-id="2c39c-126">See [Razor syntax](xref:mvc/views/razor#razor-syntax) for more information.</span></span>

<span data-ttu-id="2c39c-127">Проверьте лямбда-выражение, которое используется в следующем вспомогательном методе HTML.</span><span class="sxs-lookup"><span data-stu-id="2c39c-127">Examine the lambda expression used in the following HTML Helper:</span></span>

```cshtml
@Html.DisplayNameFor(model => model.Movie[0].Title))
```

<span data-ttu-id="2c39c-128">Вспомогательный метод HTML `DisplayNameFor` проверяет свойство `Title`, указанное в лямбда-выражении, и определяет отображаемое имя.</span><span class="sxs-lookup"><span data-stu-id="2c39c-128">The `DisplayNameFor` HTML Helper inspects the `Title` property referenced in the lambda expression to determine the display name.</span></span> <span data-ttu-id="2c39c-129">Лямбда-выражение проверяется, а не вычисляется.</span><span class="sxs-lookup"><span data-stu-id="2c39c-129">The lambda expression is inspected rather than evaluated.</span></span> <span data-ttu-id="2c39c-130">Это означает, что в случае, если `model`, `model.Movie` или `model.Movie[0]` имеют значение `null` или пусты, права доступа не нарушаются.</span><span class="sxs-lookup"><span data-stu-id="2c39c-130">That means there is no access violation when `model`, `model.Movie`, or `model.Movie[0]` are `null` or empty.</span></span> <span data-ttu-id="2c39c-131">При вычислении лямбда-выражения (например, с помощью `@Html.DisplayFor(modelItem => item.Title)`) вычисляются значения для свойств модели.</span><span class="sxs-lookup"><span data-stu-id="2c39c-131">When the lambda expression is evaluated (for example, with `@Html.DisplayFor(modelItem => item.Title)`), the model's property values are evaluated.</span></span>

<a name="md"></a>
### <a name="the-model-directive"></a><span data-ttu-id="2c39c-132">директиву @model </span><span class="sxs-lookup"><span data-stu-id="2c39c-132">The @model directive</span></span>

[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml?range=1-2&highlight=2)]

<span data-ttu-id="2c39c-133">Директива `@model` определяет тип модели, передаваемой на страницу Razor.</span><span class="sxs-lookup"><span data-stu-id="2c39c-133">The `@model` directive specifies the type of the model passed to the Razor Page.</span></span> <span data-ttu-id="2c39c-134">В приведенном выше примере строка `@model` делает класс, производный от `PageModel`, доступным для страниц Razor.</span><span class="sxs-lookup"><span data-stu-id="2c39c-134">In the preceding example, the `@model` line makes the `PageModel`-derived class available to the Razor Page.</span></span> <span data-ttu-id="2c39c-135">Модель используется на странице во [вспомогательных методах HTML](https://docs.microsoft.com/aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs#understanding-html-helpers) `@Html.DisplayNameFor` и `@Html.DisplayName`.</span><span class="sxs-lookup"><span data-stu-id="2c39c-135">The model is used in the `@Html.DisplayNameFor` and `@Html.DisplayName` [HTML Helpers](https://docs.microsoft.com/aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs#understanding-html-helpers) on the page.</span></span>

<span data-ttu-id="2c39c-136"><!-- why don't xref links work?
[HTML Helpers 2](xref:aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs)
-->

<a name="vd"></a>
### ViewData и макет</span><span class="sxs-lookup"><span data-stu-id="2c39c-136"><!-- why don't xref links work?
[HTML Helpers 2](xref:aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs)
-->

<a name="vd"></a>
### ViewData and layout</span></span>

<span data-ttu-id="2c39c-137">Рассмотрим следующий код.</span><span class="sxs-lookup"><span data-stu-id="2c39c-137">Consider the following code:</span></span>

[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml?range=1-6&highlight=4-)]

<span data-ttu-id="2c39c-138">Выделенный выше код представляет собой пример перехода Razor на C#.</span><span class="sxs-lookup"><span data-stu-id="2c39c-138">The preceding highlighted code is an example of Razor transitioning into C#.</span></span> <span data-ttu-id="2c39c-139">Символы `{` и `}` ограничивают блок кода C#.</span><span class="sxs-lookup"><span data-stu-id="2c39c-139">The `{` and `}` characters enclose a block of C# code.</span></span>

<span data-ttu-id="2c39c-140">Базовый класс `PageModel` содержит свойство словаря `ViewData`, позволяющее передать данные в представление.</span><span class="sxs-lookup"><span data-stu-id="2c39c-140">The `PageModel` base class has a `ViewData` dictionary property that can be used to add data that you want to pass to a View.</span></span> <span data-ttu-id="2c39c-141">Объекты можно добавить в словарь `ViewData` с помощью шаблона "ключ/значение".</span><span class="sxs-lookup"><span data-stu-id="2c39c-141">You add objects into the `ViewData` dictionary using a key/value pattern.</span></span> <span data-ttu-id="2c39c-142">В приведенном выше примере в словарь `ViewData` добавляется свойство "Title".</span><span class="sxs-lookup"><span data-stu-id="2c39c-142">In the preceding sample, the "Title" property is added to the `ViewData` dictionary.</span></span> <span data-ttu-id="2c39c-143">Свойство "Title" используется в файле *Pages/_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="2c39c-143">The "Title" property is used in the *Pages/_Layout.cshtml* file.</span></span> <span data-ttu-id="2c39c-144">Ниже показаны первые несколько строк файла *Pages/_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="2c39c-144">The following markup shows the first few lines of the *Pages/_Layout.cshtml* file.</span></span>

[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/NU/_Layout1.cshtml?highlight=6-)]

<span data-ttu-id="2c39c-145">Строка `@*Markup removed for brevity.*@` представляет собой комментарий Razor.</span><span class="sxs-lookup"><span data-stu-id="2c39c-145">The line `@*Markup removed for brevity.*@` is a Razor comment.</span></span> <span data-ttu-id="2c39c-146">В отличие от комментариев HTML (`<!-- -->`) комментарии Razor не отправляются клиенту.</span><span class="sxs-lookup"><span data-stu-id="2c39c-146">Unlike HTML comments (`<!-- -->`), Razor comments are not sent to the client.</span></span>

<span data-ttu-id="2c39c-147">Запустите приложение и проверьте ссылки в проекте (**Главная**, **О программе**, **Контакты**, **Создать**, **Изменить** и **Удалить**).</span><span class="sxs-lookup"><span data-stu-id="2c39c-147">Run the app and test the links in the project (**Home**, **About**, **Contact**, **Create**, **Edit**, and **Delete**).</span></span> <span data-ttu-id="2c39c-148">Каждая страница задает заголовок, который отображается на вкладке браузера. При добавлении страницы в избранное заголовок используется в закладках.</span><span class="sxs-lookup"><span data-stu-id="2c39c-148">Each page sets the title, which you can see in the browser tab. When you bookmark a page, the title is used for the bookmark.</span></span> <span data-ttu-id="2c39c-149">В настоящее время страницы *Pages/Index.cshtml* и *Pages/Movies/Index.cshtml* могут иметь один и тот же заголовок, но при желании их заголовки можно изменить.</span><span class="sxs-lookup"><span data-stu-id="2c39c-149">*Pages/Index.cshtml* and *Pages/Movies/Index.cshtml* currently have the same title, but you can modify them to have different values.</span></span>

<span data-ttu-id="2c39c-150">Свойство `Layout` определяется в файле *Pages/_ViewStart.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="2c39c-150">The `Layout` property is set in the *Pages/_ViewStart.cshtml* file:</span></span>

[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/_ViewStart.cshtml)]

<span data-ttu-id="2c39c-151">Представленный выше код задает файл разметки *Pages/_Layout.cshtml* для всех файлов Razor в папке *Pages*.</span><span class="sxs-lookup"><span data-stu-id="2c39c-151">The preceding markup sets the layout file to *Pages/_Layout.cshtml* for all Razor files under the *Pages* folder.</span></span> <span data-ttu-id="2c39c-152">Дополнительные сведения см. в статье о [макете](xref:mvc/razor-pages/index#layout).</span><span class="sxs-lookup"><span data-stu-id="2c39c-152">See [Layout](xref:mvc/razor-pages/index#layout) for more information.</span></span>

### <a name="update-the-layout"></a><span data-ttu-id="2c39c-153">Обновление макета</span><span class="sxs-lookup"><span data-stu-id="2c39c-153">Update the layout</span></span>

<span data-ttu-id="2c39c-154">Измените элемент `<title>` в файле *Pages/_Layout.cshtml*, чтобы использовать более короткую строку.</span><span class="sxs-lookup"><span data-stu-id="2c39c-154">Change the `<title>` element in the *Pages/_Layout.cshtml* file to use a shorter string.</span></span>

[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/_Layout.cshtml?range=1-6&highlight=6)]

<span data-ttu-id="2c39c-155">Найдите следующий элемент привязки в файле *Pages/_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="2c39c-155">Find the following anchor element in the *Pages/_Layout.cshtml* file.</span></span>

```cshtml
<a asp-page="/Index" class="navbar-brand">RazorPagesMovie</a>
```
<span data-ttu-id="2c39c-156">Замените указанный выше элемент на следующую разметку.</span><span class="sxs-lookup"><span data-stu-id="2c39c-156">Replace the preceding element with the following markup.</span></span>

```cshtml
<a asp-page="/Movies/Index" class="navbar-brand">RpMovie</a>
```

<span data-ttu-id="2c39c-157">Указанный выше элемент привязки является [вспомогательной функцией тега](xref:mvc/views/tag-helpers/intro).</span><span class="sxs-lookup"><span data-stu-id="2c39c-157">The preceding anchor element is a [Tag Helper](xref:mvc/views/tag-helpers/intro).</span></span> <span data-ttu-id="2c39c-158">В данном случае он является [вспомогательной функцией тега привязки](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper).</span><span class="sxs-lookup"><span data-stu-id="2c39c-158">In this case, it's the [Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper).</span></span> <span data-ttu-id="2c39c-159">Атрибут вспомогательной функции тега `asp-page="/Movies/Index"` и его значение создают ссылку на страницу Razor `/Movies/Index`.</span><span class="sxs-lookup"><span data-stu-id="2c39c-159">The `asp-page="/Movies/Index"` Tag Helper attribute and value creates a link to the `/Movies/Index` Razor Page.</span></span>

<span data-ttu-id="2c39c-160">Сохраните изменения и протестируйте приложение, нажав на ссылку **RpMovie**.</span><span class="sxs-lookup"><span data-stu-id="2c39c-160">Save your changes, and test the app by clicking on the **RpMovie** link.</span></span> <span data-ttu-id="2c39c-161">См. файл [_Layout.cshtml](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/_Layout.cshtml) в GitHub.</span><span class="sxs-lookup"><span data-stu-id="2c39c-161">See the [_Layout.cshtml](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/_Layout.cshtml) file in GitHub.</span></span>

### <a name="the-create-code-behind-page"></a><span data-ttu-id="2c39c-162">Страница кода программной части Create</span><span class="sxs-lookup"><span data-stu-id="2c39c-162">The Create code-behind page</span></span>

<span data-ttu-id="2c39c-163">Изучите файл кода программной части *Pages/Movies/Create.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="2c39c-163">Examine the *Pages/Movies/Create.cshtml.cs* code-behind file:</span></span>

[!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Create.cshtml.cs?name=snippetALL)]

<span data-ttu-id="2c39c-164">Метод `OnGet` инициализирует все состояния, необходимые для страницы.</span><span class="sxs-lookup"><span data-stu-id="2c39c-164">The `OnGet` method initializes any state needed for the page.</span></span> <span data-ttu-id="2c39c-165">Страница Create не содержит никаких состояний для инициализации.</span><span class="sxs-lookup"><span data-stu-id="2c39c-165">The Create page doesn't have any state to initialize.</span></span> <span data-ttu-id="2c39c-166">Метод `Page` создает объект `PageResult`, который формирует страницу *Create.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="2c39c-166">The `Page` method creates a `PageResult` object that renders the *Create.cshtml* page.</span></span>

<span data-ttu-id="2c39c-167">Для указания согласия на [привязку модели](xref:mvc/models/model-binding) в свойстве `Movie` используется атрибут `[BindProperty]`.</span><span class="sxs-lookup"><span data-stu-id="2c39c-167">The `Movie` property uses the `[BindProperty]` attribute to opt-in to [model binding](xref:mvc/models/model-binding).</span></span> <span data-ttu-id="2c39c-168">Когда форма Create публикует свои значения, среда выполнения ASP.NET Core связывает переданные значения с моделью `Movie`.</span><span class="sxs-lookup"><span data-stu-id="2c39c-168">When the Create form posts the form values, the ASP.NET Core runtime binds the posted values to the `Movie` model.</span></span>

<span data-ttu-id="2c39c-169">Метод `OnPostAsync` выполняется, когда страница публикует данные формы:</span><span class="sxs-lookup"><span data-stu-id="2c39c-169">The `OnPostAsync` method is run when the page posts form data:</span></span>

[!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Create.cshtml.cs?name=snippetPost)]

<span data-ttu-id="2c39c-170">Если в модели есть ошибки, форма отображается снова вместе со всеми опубликованными данными этой формы.</span><span class="sxs-lookup"><span data-stu-id="2c39c-170">If there are any model errors, the form is redisplayed, along with any form data posted.</span></span> <span data-ttu-id="2c39c-171">Большинство ошибок в модели может быть перехвачено на стороне клиента до публикации формы.</span><span class="sxs-lookup"><span data-stu-id="2c39c-171">Most model errors can be caught on the client-side before the form is posted.</span></span> <span data-ttu-id="2c39c-172">Пример ошибки в модели — это публикация значения для поля даты, которое нельзя конвертировать в дату.</span><span class="sxs-lookup"><span data-stu-id="2c39c-172">An example of a model error is posting a value for the date field that cannot be converted to a date.</span></span> <span data-ttu-id="2c39c-173">О проверке на стороне клиента и проверке модели мы поговорим подробнее далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="2c39c-173">We'll talk more about client-side validation and model validation later in the tutorial.</span></span>

<span data-ttu-id="2c39c-174">Если ошибок в модели нет, данные сохраняются, а браузер переадресуется на страницу индексов.</span><span class="sxs-lookup"><span data-stu-id="2c39c-174">If there are no model errors, the data is saved, and the browser is redirected to the Index page.</span></span>

### <a name="the-create-razor-page"></a><span data-ttu-id="2c39c-175">Страница Razor Create</span><span class="sxs-lookup"><span data-stu-id="2c39c-175">The Create Razor Page</span></span>

<span data-ttu-id="2c39c-176">Изучите файл страницы Razor *Pages/Movies/Create.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="2c39c-176">Examine the *Pages/Movies/Create.cshtml* Razor Page file:</span></span>

[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Create.cshtml)]

<span data-ttu-id="2c39c-177">Visual Studio выделяет тег `<form method="post">` отдельным шрифтом, который используется для вспомогательных функций тегов.</span><span class="sxs-lookup"><span data-stu-id="2c39c-177">Visual Studio displays the `<form method="post">` tag in a distinctive font used for Tag Helpers.</span></span> <span data-ttu-id="2c39c-178">Элемент `<form method="post">` представляет собой [вспомогательную функцию тега Form](xref:mvc/views/working-with-forms#the-form-tag-helper).</span><span class="sxs-lookup"><span data-stu-id="2c39c-178">The `<form method="post">` element is a [Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper).</span></span> <span data-ttu-id="2c39c-179">Вспомогательная функция тега Form автоматически включает [маркер защиты от подделки](xref:security/anti-request-forgery).</span><span class="sxs-lookup"><span data-stu-id="2c39c-179">The Form Tag Helper automatically includes an [antiforgery token](xref:security/anti-request-forgery).</span></span>

![Представление страницы Create.cshtml в VS17](page/_static/th.png)

<span data-ttu-id="2c39c-181">Ядро формирования шаблонов создает разметку Razor для каждого поля в модели (кроме ID) следующего вида:</span><span class="sxs-lookup"><span data-stu-id="2c39c-181">The scaffolding engine creates Razor markup for each field in the model (except the ID) similar to the following:</span></span>

[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Create.cshtml?range=15-20)]

<span data-ttu-id="2c39c-182">[Вспомогательные функции тегов Validation](xref:mvc/views/working-with-forms#the-validation-tag-helpers) (`<div asp-validation-summary` и ` <span asp-validation-for`) отображают ошибки проверки.</span><span class="sxs-lookup"><span data-stu-id="2c39c-182">The [Validation Tag Helpers](xref:mvc/views/working-with-forms#the-validation-tag-helpers) (`<div asp-validation-summary` and ` <span asp-validation-for`) display validation errors.</span></span> <span data-ttu-id="2c39c-183">Более подробно проверка рассматривается далее в этой серии статей.</span><span class="sxs-lookup"><span data-stu-id="2c39c-183">Validation is covered in more detail later in this series.</span></span>

<span data-ttu-id="2c39c-184">[Вспомогательная функция тега Label](xref:mvc/views/working-with-forms#the-label-tag-helper) (`<label asp-for="Movie.Title" class="control-label"></label>`) создает подпись к метке и атрибут `for` для свойства `Title`.</span><span class="sxs-lookup"><span data-stu-id="2c39c-184">The [Label Tag Helper](xref:mvc/views/working-with-forms#the-label-tag-helper) (`<label asp-for="Movie.Title" class="control-label"></label>`) generates the label caption and `for` attribute for the `Title` property.</span></span>

<span data-ttu-id="2c39c-185">[Вспомогательная функция тега Input](xref:mvc/views/working-with-forms) (`<input asp-for="Movie.Title" class="form-control" />`) использует атрибуты [DataAnnotations](https://docs.microsoft.com/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) и создает HTML-атрибуты, необходимые для проверки jQuery на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="2c39c-185">The [Input Tag Helper](xref:mvc/views/working-with-forms) (`<input asp-for="Movie.Title" class="form-control" />`) uses the [DataAnnotations](https://docs.microsoft.com/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) attributes and produces HTML attributes needed for jQuery Validation on the client-side.</span></span>

<span data-ttu-id="2c39c-186">В следующем учебнике рассматривается SQL Server LocalDB и заполнение базы данных.</span><span class="sxs-lookup"><span data-stu-id="2c39c-186">The next tutorial explains SQL Server LocalDB and seeding the database.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="2c39c-187">[Назад: Добавление модели](xref:tutorials/razor-pages/model)
[Далее: SQL Server LocalDB](xref:tutorials/razor-pages/sql)</span><span class="sxs-lookup"><span data-stu-id="2c39c-187">[Previous: Adding a model](xref:tutorials/razor-pages/model)
[Next: SQL Server LocalDB](xref:tutorials/razor-pages/sql)</span></span>