---
title: "Настройте тип данных первичного ключа удостоверения"
author: AdrienTorris
description: "В этой статье описаны шаги по настройке в нужный тип данных используется для ASP.NET Core Identity первичного ключа."
ms.author: scaddie
manager: wpickett
ms.date: 09/28/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authentication/identity-primary-key-configuration
ms.openlocfilehash: da46aa90a434a978a55467da982d746eb2d959ee
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="configure-the-aspnet-core-identity-primary-key-data-type"></a><span data-ttu-id="0e982-103">Настройка типа данных первичного ключа ASP.NET Core Identity</span><span class="sxs-lookup"><span data-stu-id="0e982-103">Configure the ASP.NET Core Identity primary key data type</span></span>

<span data-ttu-id="0e982-104">ASP.NET Core удостоверений можно настроить тип данных, используемый для представления первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="0e982-104">ASP.NET Core Identity allows you to configure the data type used to represent a primary key.</span></span> <span data-ttu-id="0e982-105">Использует удостоверение `string` тип данных по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0e982-105">Identity uses the `string` data type by default.</span></span> <span data-ttu-id="0e982-106">Это поведение можно переопределить.</span><span class="sxs-lookup"><span data-stu-id="0e982-106">You can override this behavior.</span></span>

## <a name="customize-the-primary-key-data-type"></a><span data-ttu-id="0e982-107">Настроить тип данных первичного ключа</span><span class="sxs-lookup"><span data-stu-id="0e982-107">Customize the primary key data type</span></span>

1. <span data-ttu-id="0e982-108">Создать пользовательскую реализацию [IdentityUser](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.identity.entityframeworkcore.identityuser-1) класса.</span><span class="sxs-lookup"><span data-stu-id="0e982-108">Create a custom implementation of the [IdentityUser](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.identity.entityframeworkcore.identityuser-1) class.</span></span> <span data-ttu-id="0e982-109">Представляет тип, используемый для создания пользовательских объектов.</span><span class="sxs-lookup"><span data-stu-id="0e982-109">It represents the type to be used for creating user objects.</span></span> <span data-ttu-id="0e982-110">В следующем примере значение по умолчанию `string` заменяется типом `Guid`.</span><span class="sxs-lookup"><span data-stu-id="0e982-110">In the following example, the default `string` type is replaced with `Guid`.</span></span>

    [!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Models/ApplicationUser.cs?highlight=4&range=7-13)]

1. <span data-ttu-id="0e982-111">Создать пользовательскую реализацию [IdentityRole](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.identity.entityframeworkcore.identityrole-1) класса.</span><span class="sxs-lookup"><span data-stu-id="0e982-111">Create a custom implementation of the [IdentityRole](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.identity.entityframeworkcore.identityrole-1) class.</span></span> <span data-ttu-id="0e982-112">Представляет тип, используемый для создания объектов роли.</span><span class="sxs-lookup"><span data-stu-id="0e982-112">It represents the type to be used for creating role objects.</span></span> <span data-ttu-id="0e982-113">В следующем примере значение по умолчанию `string` заменяется типом `Guid`.</span><span class="sxs-lookup"><span data-stu-id="0e982-113">In the following example, the default `string` type is replaced with `Guid`.</span></span>
    
    [!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Models/ApplicationRole.cs?highlight=3&range=7-12)]
    
1. <span data-ttu-id="0e982-114">Создайте класс контекста пользовательской базе данных.</span><span class="sxs-lookup"><span data-stu-id="0e982-114">Create a custom database context class.</span></span> <span data-ttu-id="0e982-115">Он наследует от класса контекста базы данных Entity Framework, используемый для удостоверения.</span><span class="sxs-lookup"><span data-stu-id="0e982-115">It inherits from the Entity Framework database context class used for Identity.</span></span> <span data-ttu-id="0e982-116">`TUser` И `TRole` аргументы ссылаться на пользовательские классы пользователя и роли, созданные на предыдущем шаге, соответственно.</span><span class="sxs-lookup"><span data-stu-id="0e982-116">The `TUser` and `TRole` arguments reference the custom user and role classes created in the previous step, respectively.</span></span> <span data-ttu-id="0e982-117">`Guid` Для первичного ключа определен тип данных.</span><span class="sxs-lookup"><span data-stu-id="0e982-117">The `Guid` data type is defined for the primary key.</span></span>

    [!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Data/ApplicationDbContext.cs?highlight=3&range=9-26)]
    
1. <span data-ttu-id="0e982-118">Зарегистрируйте класс контекста пользовательской базе данных, при добавлении удостоверения службы в классе при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="0e982-118">Register the custom database context class when adding the Identity service in the app's startup class.</span></span>

    # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="0e982-119">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="0e982-119">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)
    
    <span data-ttu-id="0e982-120">`AddEntityFrameworkStores` Метод не принимает `TKey` аргумент, как это требовалось в ASP.NET Core 1.x.</span><span class="sxs-lookup"><span data-stu-id="0e982-120">The `AddEntityFrameworkStores` method doesn't accept a `TKey` argument as it did in ASP.NET Core 1.x.</span></span> <span data-ttu-id="0e982-121">Тип данных первичный ключ определяется путем анализа `DbContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="0e982-121">The primary key's data type is inferred by analyzing the `DbContext` object.</span></span>
    
    [!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-PrimaryKeysConfig/Startup.cs?highlight=6-8&range=25-37)]
    
    # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="0e982-122">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="0e982-122">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)
    
    <span data-ttu-id="0e982-123">`AddEntityFrameworkStores` Метод принимает `TKey` аргумент, указывающий тип данных первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="0e982-123">The `AddEntityFrameworkStores` method accepts a `TKey` argument indicating the primary key's data type.</span></span>
    
    [!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?highlight=9-11&range=39-55)]
    
    ---

## <a name="test-the-changes"></a><span data-ttu-id="0e982-124">Тестирование изменений</span><span class="sxs-lookup"><span data-stu-id="0e982-124">Test the changes</span></span>

<span data-ttu-id="0e982-125">После завершения изменений конфигурации свойства, представляющего первичный ключ отражает новый тип данных.</span><span class="sxs-lookup"><span data-stu-id="0e982-125">Upon completion of the configuration changes, the property representing the primary key reflects the new data type.</span></span> <span data-ttu-id="0e982-126">В следующем примере показано обращение к свойству в контроллер MVC.</span><span class="sxs-lookup"><span data-stu-id="0e982-126">The following example demonstrates accessing the property in an MVC controller.</span></span>

[!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Controllers/AccountController.cs?name=snippet_GetCurrentUserId&highlight=6)]