---
title: "Привязка вспомогательный тег | Документы Microsoft"
author: pkellner
description: "Показано, как работать с вспомогательный тег привязки"
ms.author: riande
manager: wpickett
ms.date: 12/20/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: mvc/views/tag-helpers/builtin-th/anchor-tag-helper
ms.openlocfilehash: 74609b515936ec7da8bfc133c27cb69f51311924
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2018
---
# <a name="anchor-tag-helper"></a>Вспомогательный тег привязки

Автор: [Питер Кельнер (Peter Kellner)](http://peterkellner.net) 

Вспомогательный тег привязки улучшает привязки HTML (`<a ... ></a>`) тега путем добавления новых атрибутов. Ссылки, созданной (на `href` тега) создается с использованием новых атрибутов. Этот URL-адрес может включать необязательный протокол, такой как https.

Динамика контроллер ниже используется в примерах в этом документе.

**SpeakerController.cs** 

[!code-csharp[SpeakerController](sample/TagHelpersBuiltInAspNetCore/src/TagHelpersBuiltInAspNetCore/Controllers/SpeakerController.cs)]


## <a name="anchor-tag-helper-attributes"></a>Атрибуты вспомогательного тег привязки

### <a name="asp-controller"></a>ASP контроллер

`asp-controller`позволяет связать контроллера, который будет использоваться для создания URL-адрес. Контроллеры, указанные должен существовать в текущем проекте. В следующем коде перечисляются все динамики: 

```cshtml
<a asp-controller="Speaker" asp-action="Index">All Speakers</a>
```

Будет создаваемой разметкой:

```html
<a href="/Speaker">All Speakers</a>
```

Если `asp-controller` указан и `asp-action` отсутствует, значение по умолчанию `asp-action` будет выполняться в данный момент представления метода контроллера по умолчанию. Что находится в приведенном выше примере, если `asp-action` опущены, и создается на основе этого вспомогательного объекта тег привязки *HomeController* `Index` представление (**/Home**), созданной разметки будет:

```html
<a href="/Home">All Speakers</a>
```

### <a name="asp-action"></a>Действие ASP

`asp-action`Имя метода действия контроллера, которое будет включено в созданный `href`. Например, следующий код задать созданный `href` указывают на страницу сведений динамика:

```html
<a asp-controller="Speaker" asp-action="Detail">Speaker Detail</a>
```

Будет создаваемой разметкой:

```html
<a href="/Speaker/Detail">Speaker Detail</a>
```

Если не `asp-controller` атрибут указан, будет использоваться по умолчанию контроллера, вызов представлении при выполнении текущего представления.  
 
Если атрибут `asp-action` — `Index`, то никакие действия добавляется к URL-адрес, начальные значения по умолчанию `Index` вызываемого метода. Действие указанного (или по умолчанию), должен существовать в контроллер, на которые ссылается `asp-controller`.

### <a name="asp-page"></a>ASP страницы

Используйте `asp-page` атрибут в тег для задания его URL-адрес, чтобы он указывал на определенную страницу. Создает URL-адрес вставляя перед именем страницы с косой черты «/». В примере ниже URL-адрес указывает на страницу «Говорящего» в текущем каталоге.

```cshtml
<a asp-page="/Speakers">All Speakers</a>
```

`asp-page` Атрибута в приведенном выше примере подготавливает к просмотру в формате HTML в представлении, которая похожа на следующий фрагмент кода:

```html
<a href="/items?page=%2FSpeakers">Speakers</a>
```

`asp-page` Атрибута является взаимоисключающим с `asp-route`, `asp-controller`, и `asp-action` атрибуты. Тем не менее `asp-page` может использоваться с `asp-route-id` для управления маршрутизацией, как показано в следующем образце кода:

```cshtml
<a asp-page="/Speaker" asp-route-id="@speaker.Id">View Speaker</a>
```

`asp-route-id` Выводятся следующие данные:

```html
https://localhost:44399/Speakers/Index/2?page=%2FSpeaker
```

> [!NOTE]
> Для использования `asp-page` атрибут на страницах Razor, URL-адреса должен быть относительным путем, например `"./Speaker"`. Относительные пути в `asp-page` атрибута не доступны в представлениях MVC. Вместо этого используйте синтаксис «/» для представления MVC.

### <a name="asp-route-value"></a>ASP - маршрута-{value}

`asp-route-`является префиксом маршрута подстановочному знаку. Любое значение, помещенный после дефис в конце рассматриваются как потенциальные параметра маршрута. Если маршрут по умолчанию не найден, этот префикс маршрута будет добавлена к созданный href как параметр запроса и значение. В противном случае он будет подставлено в шаблоне маршрута.

При условии, что метод контроллера определены следующим образом:

```csharp
public IActionResult AnchorTagHelper(string id)
{
    var speaker = new SpeakerData()
    {
        SpeakerId = 12
    };
    return View(viewName, speaker);
}
```

У шаблона маршрута по умолчанию, определенные в вашей *файла Startup.cs* следующим образом:

```csharp
app.UseMvc(routes =>
{
   routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id?}");
});

```

**Cshtml** файл, содержащий вспомогательные тег привязки, необходимых для использования **динамика** параметр модели, переданное из контроллера в представление является следующим образом:

```cshtml
@model SpeakerData
<!DOCTYPE html>
<html><body>
<a asp-controller='Speaker' asp-action='Detail' asp-route-id=@Model.SpeakerId>SpeakerId: @Model.SpeakerId</a>
<body></html>
```

Затем созданного кода HTML будет следующим, так как **идентификатор** был найден в маршрут по умолчанию.

```html
<a href='/Speaker/Detail/12'>SpeakerId: 12</a>
```

Если префикс маршрута не входит в состав маршрутизации найден шаблон, как бывает со следующими **cshtml** файла:

```cshtml
@model SpeakerData
<!DOCTYPE html>
<html><body>
<a asp-controller='Speaker' asp-action='Detail' asp-route-speakerid=@Model.SpeakerId>SpeakerId: @Model.SpeakerId</a>
<body></html>
```

Затем созданного кода HTML будет следующим, так как **speakerid** не найден в соответствующих маршрута:

```html
<a href='/Speaker/Detail?speakerid=12'>SpeakerId: 12</a>
```

Если параметр `asp-controller` или `asp-action` не указаны, то следует той же обработки по умолчанию, как в `asp-route` атрибута.

### <a name="asp-route"></a>ASP маршрута

`asp-route`предоставляет способ создания URL-адрес, непосредственно именованный маршрут. Использование атрибутов маршрутизации маршрут, можно назвать как показано в `SpeakerController` и используется в его `Evaluations` метод.

`Name = "speakerevals"`Указывает вспомогательный тег привязки для создания маршрута непосредственно к этому методу контроллера, используя URL-адрес `/Speaker/Evaluations`. Если `asp-controller` или `asp-action` указать в дополнение к `asp-route`, созданный маршрут не может отличаться от ожидаемого. `asp-route`не должны использоваться с любой из атрибутов `asp-controller` или `asp-action` во избежание конфликта маршрута.

### <a name="asp-all-route-data"></a>asp-all-route-data

`asp-all-route-data`позволяет создавать словарь пары ключ-значение, где ключ является именем параметра, а значение — значение, связанное с этим ключом.

Как в следующем примере показано создается словарю встроенные и данные передаются в представление razor. В качестве альтернативы данных может быть передана с помощью модели.

```cshtml
@{
    var dict =
        new Dictionary<string, string>
        {
            {"speakerId", "11"},
            {"currentYear", "true"}
        };
}
<a asp-route="speakerevalscurrent"
asp-all-route-data="dict">SpeakerEvals</a>
```

Приведенный выше код создает следующий URL-адрес: http://localhost/Speaker/EvaluationsCurrent?speakerId=11&currentYear=true

При щелчке по ссылке метод контроллера `EvaluationsCurrent` вызывается. Он вызывается, поскольку этот контроллер имеет два строковых параметра, которые соответствуют создаются на основе `asp-all-route-data` словаря.

Если все ключи в словаре совпадают направления параметров, эти значения будут заменены на маршруте соответствующим образом и другие несовпадающие значения будет создан как параметры запроса.

### <a name="asp-fragment"></a>фрагмент ASP

`asp-fragment`Определяет фрагмент URL-адреса для добавления URL-адрес. Вспомогательный тег привязки будет добавлен символ решетки (#). Если вы создаете тег:

```cshtml
<a asp-action="Evaluations" asp-controller="Speaker"  
   asp-fragment="SpeakerEvaluations">About Speaker Evals</a>
```

Созданный URL-адрес будет: http://localhost/Speaker/Evaluations#SpeakerEvaluations

Хэш-теги полезны при построении приложений на стороне клиента. Они могут использоваться для простой пометки и поиска на языке JavaScript, например.

### <a name="asp-area"></a>область ASP

`asp-area`Задает имя области, ASP.NET Core используется для задания соответствующего маршрута. Ниже приведены примеры как области атрибута вызывает повторное сопоставление маршрутов. Установка `asp-area` блогах префиксов каталоге `Areas/Blogs` ко всем маршрутам связанные контроллеры и представления для этот тег привязки.

* Имя проекта
  * wwwroot
  * Области
    * Блоги
      * Контроллеры
        * HomeController.cs
      * Представления
        * Главная страница
          * Index.cshtml
          * AboutBlog.cshtml
  * Контроллеры

Указание области тег, который является допустимым, такие как ```area="Blogs"``` при ссылке на ```AboutBlog.cshtml``` файла будет выглядеть следующим образом с помощью вспомогательного тег привязки.

```cshtml
<a asp-action="AboutBlog" asp-controller="Home" asp-area="Blogs">Blogs About</a>
```

Созданный код HTML будет содержать сегмент областей и будет выглядеть следующим образом:

```html
<a href="/Blogs/Home/AboutBlog">Blogs About</a>
```

> [!TIP]
> Для областей MVC, для работы в веб-приложении шаблон маршрута необходимо включить ссылку в область, если он существует. Этого шаблона, который является второй параметр из `routes.MapRoute` вызова метода, будут отображаться как:`template: '"{area:exists}/{controller=Home}/{action=Index}"'`

### <a name="asp-protocol"></a>ASP протокол

`asp-protocol` Предназначен для указания протокола (например, `https`) в URL-адрес. Пример вспомогательного тег привязки, включающий протокол будет выглядеть следующим образом:

```<a asp-protocol="https" asp-action="About" asp-controller="Home">About</a>```

и создают HTML-код следующим образом:

```<a href="https://localhost/Home/About">About</a>```

Домен, в примере используется имя localhost, но использует вспомогательный тег привязки общедоступные веб-сайта, при формировании URL-адрес.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Области](xref:mvc/controllers/areas)
