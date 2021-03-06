---
title: "Работа с SQL Server LocalDB"
author: rick-anderson
description: "Использование SQL Server LocalDB с простым приложением MVC"
manager: wpickett
ms.author: riande
ms.date: 03/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-mvc-app/working-with-sql
ms.openlocfilehash: a0aa6fdfa51650628021a4ba6d0533e7e0e39200
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/30/2018
---
# <a name="working-with-sql-server-localdb"></a>Работа с SQL Server LocalDB

Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)

Объект `MvcMovieContext` обрабатывает задачу подключения к базе данных и сопоставления объектов `Movie` с записями базы данных. Контекст базы данных регистрируется с помощью контейнера [внедрения зависимостей](xref:fundamentals/dependency-injection) в методе `ConfigureServices` в файле *Startup.cs*:

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?name=ConfigureServices&highlight=6-7)]

Система [конфигурации](xref:fundamentals/configuration/index) ASP.NET Core считывает `ConnectionString`. Для разработки на локальном уровне она получает строку подключения из файла *appsettings.json*:

[!code-json[Main](start-mvc/sample/MvcMovie/appsettings.json?highlight=2&range=8-10)]

При развертывании приложения на тестовом или рабочем сервере вы можете использовать переменную среды или другой способ настройки строки подключения к реальному серверу SQL Server. Дополнительные сведения см. в статье [Конфигурация](xref:fundamentals/configuration/index).

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

LocalDB — это упрощенная версия ядра СУБД SQL Server Express, предназначенная для разработки программ. LocalDB запускается по запросу в пользовательском режиме, поэтому настройки не слишком сложны. По умолчанию база данных LocalDB создает файлы \*.mdf в каталоге *C:/Users/\<пользователь\>*.

* В меню **Вид** откройте **обозреватель объектов SQL Server** (SSOX).

  ![Меню "Вид"](working-with-sql/_static/ssox.png)

* Щелкните правой кнопкой мыши таблицу `Movie` и выберите пункт **Конструктор представлений**.

  ![Контекстное меню, открытое на таблице Movie](working-with-sql/_static/design.png)

  ![Таблица Movie, открытая в конструкторе](working-with-sql/_static/dv.png)

Обратите внимание на значок с изображением ключа рядом с `ID`. По умолчанию EF сделает свойство с именем `ID` первичным ключом.

* Щелкните правой кнопкой мыши таблицу `Movie` и выберите пункт **Просмотр данных**.

  ![Контекстное меню, открытое на таблице Movie](working-with-sql/_static/ssox2.png)

  ![Открытая таблица Movie с отображением данных](working-with-sql/_static/vd22.png)

## <a name="seed-the-database"></a>Заполнение базы данных

Создайте класс `SeedData` в папке *Models*. Замените сгенерированный код следующим кодом:

[!code-csharp[Main](start-mvc/sample/MvcMovie/Models/SeedData.cs?name=snippet_1)]

Если в базе данных есть фильмы, возвращается инициализатор заполнения и фильмы не добавляются.

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```

<a name="si"></a>
### <a name="add-the-seed-initializer"></a>Добавление инициализатора заполнения

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

Добавьте инициализатор заполнения в метод `Main` в файле *Program.cs*:

[!code-csharp[Main](start-mvc/sample/MvcMovie/Program.cs?highlight=6,14-32)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

Добавьте инициализатор заполнения в конец метода `Configure` в файле *Startup.cs*:

[!code-csharp[Main](start-mvc/sample/MvcMovie/Startup.cs?highlight=9&name=snippet_seed)]

---

Тестирование приложения

* Удалите все записи из базы данных. Это можно сделать с помощью ссылок удаления в браузере или из SSOX.
* Необходимо выполнить инициализацию (вызывать методы в классе `Startup`), чтобы запустить метод заполнения. Для этого следует остановить и перезапустить IIS Express. Воспользуйтесь одним из перечисленных ниже подходов.

  * Щелкните правой кнопкой мыши значок IIS Express в области уведомлений и выберите **Выход** или **Остановить сайт**.

    ![Значок IIS Express в области уведомлений](working-with-sql/_static/iisExIcon.png)

    ![Контекстное меню](working-with-sql/_static/stopIIS.png)

   * Если среда VS была запущена в режиме без отладки, нажмите клавишу F5 для запуска в режиме отладки.
   * Если среда VS была запущена в режиме отладки, остановите отладчик и нажмите клавишу F5.
   
В приложении будут отображены данные.

![Приложение MVC Movie, открытое в Microsoft Edge и отображающие данные о фильме](working-with-sql/_static/m55.png)

>[!div class="step-by-step"]
[Назад](adding-model.md)
[Вперед](controller-methods-views.md)  
