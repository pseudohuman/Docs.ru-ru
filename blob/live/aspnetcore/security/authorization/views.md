---
title: "Авторизация на основе представления в ASP.NET Core MVC"
author: rick-anderson
description: "В этом документе показано, как внедрить и использовать службы авторизации внутри представления ASP.NET Core Razor."
ms.author: riande
manager: wpickett
ms.date: 10/30/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/views
ms.openlocfilehash: 8f87ca90b77be1efd75688e8203cb57b1a3360ad
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="view-based-authorization"></a><span data-ttu-id="cc61b-103">Авторизация на основе представления</span><span class="sxs-lookup"><span data-stu-id="cc61b-103">View-based authorization</span></span>

<span data-ttu-id="cc61b-104">Часто разработчику для отображения, скрытия или изменения пользовательского интерфейса на основе идентификатора текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="cc61b-104">A developer often wants to show, hide, or otherwise modify a UI based on the current user identity.</span></span> <span data-ttu-id="cc61b-105">Служба авторизации в представлениях MVC через доступна [внедрения зависимостей](xref:fundamentals/dependency-injection#fundamentals-dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="cc61b-105">You can access the authorization service within MVC views via [dependency injection](xref:fundamentals/dependency-injection#fundamentals-dependency-injection).</span></span> <span data-ttu-id="cc61b-106">Чтобы внедрить службы авторизации в представления Razor, используйте `@inject` директиву:</span><span class="sxs-lookup"><span data-stu-id="cc61b-106">To inject the authorization service into a Razor view, use the `@inject` directive:</span></span>

```cshtml
@using Microsoft.AspNetCore.Authorization
@inject IAuthorizationService AuthorizationService
```

<span data-ttu-id="cc61b-107">Служба авторизации в каждом представлении, установите `@inject` директив в *_ViewImports.cshtml* файл *представления* каталога.</span><span class="sxs-lookup"><span data-stu-id="cc61b-107">If you want the authorization service in every view, place the `@inject` directive into the *_ViewImports.cshtml* file of the *Views* directory.</span></span> <span data-ttu-id="cc61b-108">Дополнительные сведения см. в разделе [внедрение зависимостей в представления](xref:mvc/views/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="cc61b-108">For more information, see [Dependency injection into views](xref:mvc/views/dependency-injection).</span></span>

<span data-ttu-id="cc61b-109">Использовать для вызова службы подставляемого авторизации `AuthorizeAsync` точно таким же образом проводится проверка во время [авторизации на основе ресурсов](xref:security/authorization/resourcebased#security-authorization-resource-based-imperative):</span><span class="sxs-lookup"><span data-stu-id="cc61b-109">Use the injected authorization service to invoke `AuthorizeAsync` in exactly the same way you would check during [resource-based authorization](xref:security/authorization/resourcebased#security-authorization-resource-based-imperative):</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="cc61b-110">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="cc61b-110">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```cshtml
@if ((await AuthorizationService.AuthorizeAsync(User, "PolicyName")).Succeeded)
{
    <p>This paragraph is displayed because you fulfilled PolicyName.</p>
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="cc61b-111">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="cc61b-111">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```cshtml
@if (await AuthorizationService.AuthorizeAsync(User, "PolicyName"))
{
    <p>This paragraph is displayed because you fulfilled PolicyName.</p>
}
```

---

<span data-ttu-id="cc61b-112">В некоторых случаях ресурс будет модели представления.</span><span class="sxs-lookup"><span data-stu-id="cc61b-112">In some cases, the resource will be your view model.</span></span> <span data-ttu-id="cc61b-113">Вызвать `AuthorizeAsync` точно таким же образом проводится проверка во время [авторизации на основе ресурсов](xref:security/authorization/resourcebased#security-authorization-resource-based-imperative):</span><span class="sxs-lookup"><span data-stu-id="cc61b-113">Invoke `AuthorizeAsync` in exactly the same way you would check during [resource-based authorization](xref:security/authorization/resourcebased#security-authorization-resource-based-imperative):</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="cc61b-114">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="cc61b-114">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```cshtml
@if ((await AuthorizationService.AuthorizeAsync(User, Model, Operations.Edit)).Succeeded)
{
    <p><a class="btn btn-default" role="button"
        href="@Url.Action("Edit", "Document", new { id = Model.Id })">Edit</a></p>
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="cc61b-115">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="cc61b-115">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```cshtml
@if (await AuthorizationService.AuthorizeAsync(User, Model, Operations.Edit))
{
    <p><a class="btn btn-default" role="button"
        href="@Url.Action("Edit", "Document", new { id = Model.Id })">Edit</a></p>
}
```

---

<span data-ttu-id="cc61b-116">В приведенном выше коде модели передается в качестве ресурса, которое должен выполнить вычисления политики во внимание.</span><span class="sxs-lookup"><span data-stu-id="cc61b-116">In the preceding code, the model is passed as a resource the policy evaluation should take into consideration.</span></span>

> [!WARNING]
> <span data-ttu-id="cc61b-117">Не полагайтесь на переключение видимости видимость элементов пользовательского интерфейса приложения как проверку единственным авторизации.</span><span class="sxs-lookup"><span data-stu-id="cc61b-117">Don't rely on toggling visibility of your app's UI elements as the sole authorization check.</span></span> <span data-ttu-id="cc61b-118">Скрытие элемента пользовательского интерфейса не могут помешать полностью доступа к связанному контроллеру действия.</span><span class="sxs-lookup"><span data-stu-id="cc61b-118">Hiding a UI element may not completely prevent access to its associated controller action.</span></span> <span data-ttu-id="cc61b-119">Например рассмотрим кнопку в предыдущем фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="cc61b-119">For example, consider the button in the preceding code snippet.</span></span> <span data-ttu-id="cc61b-120">Пользователь может вызвать `Edit` является URL-адрес метода действия, если он или она знает относительного ресурса */Document/Edit/1*.</span><span class="sxs-lookup"><span data-stu-id="cc61b-120">A user can invoke the `Edit` action method if he or she knows the relative resource URL is */Document/Edit/1*.</span></span> <span data-ttu-id="cc61b-121">По этой причине `Edit` метод действия должен выполнить собственную проверку авторизации.</span><span class="sxs-lookup"><span data-stu-id="cc61b-121">For this reason, the `Edit` action method should perform its own authorization check.</span></span>