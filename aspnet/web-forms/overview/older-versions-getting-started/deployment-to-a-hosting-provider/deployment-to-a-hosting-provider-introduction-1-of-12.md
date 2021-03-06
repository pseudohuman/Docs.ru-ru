---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
title: "Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio: введение - 1, 12 | Документы Microsoft"
author: tdykstra
description: "Ряд учебниках показано развертывание ASP.NET (публикации) проекта веб-приложения, который содержит базу данных SQL Server Compact с помощью Visual Stu..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: a2d7f33b-8c4a-4b48-9fb1-9139cf9b9878
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
msc.type: authoredcontent
ms.openlocfilehash: 9c0edb301de85d15b9a3527382b72211f6f3d3ec
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2018
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-introduction---1-of-12"></a>Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio: введение - 1, 12
====================
По [Tom Dykstra](https://github.com/tdykstra)

[Загрузите начальный проект](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> Ряд учебниках показано развертывание ASP.NET (публикации) проекта веб-приложения, который содержит базу данных SQL Server Compact с помощью Visual Studio 2012 RC или Visual Studio Express 2012 RC для Web. Также можно использовать Visual Studio 2010, при установке обновления публикации Web.
> 
> Учебник, в котором показаны возможности развертывания, появившиеся после выпуска версии-КАНДИДАТА Visual Studio 2012, показано, как развернуть выпусках SQL Server, отличных от SQL Server Compact и показано, как для развертывания на веб-приложениях службы приложений Azure, в разделе [развертывания веб-приложения ASP.NET с помощью Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).
> 
> В этих учебниках по развертыванию сначала IIS для локального компьютера разработчика для тестирования, а затем стороннего поставщика услуг размещения. Приложение, которое вы развернете использует базу данных приложения и базы данных членства ASP.NET. Начните с помощью SQL Server Compact и развертывание в SQL Server Compact и следующих руководствах развертывание изменений базы данных и миграции на SQL Server.
> 
> Учебники предполагается, что вы знаете, как работать с ASP.NET в Visual Studio. Если этого не сделать, является удобным инструментом для начала [основные учебник по ASP.NET Web Forms](../tailspin-spyworks/tailspin-spyworks-part-1.md) или [основам ASP.NET MVC](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md).
> 
> Если у вас есть вопросы, которые не связаны непосредственно для работы с учебником, их можно разместить [форум, посвященный развертыванию ASP.NET](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment).


## <a name="overview"></a>Обзор

В этих учебниках по развертыванию сначала IIS для локального компьютера разработчика для тестирования, а затем стороннего поставщика услуг размещения. Приложение, которое вы развернете использует базу данных приложения и базы данных членства ASP.NET. Начните с помощью SQL Server Compact и развертывание в SQL Server Compact и следующих руководствах развертывание изменений базы данных и миграции на SQL Server.

Количество учебников — 11 во всех, а также об устранении неполадок страницы — может сделать процесс развертывания кажется довольно сложным. На самом деле развертывание сайта основные процедуры составляют относительно небольшой частью учебника по службам набора. Тем не менее, в реальных ситуациях часто требуются сведения о некоторых дополнительных аспектов небольшие, но важные развертывания — например, установка разрешений для папки на целевом сервере. Мы включили многие из этих дополнительных методов в учебниках по возможности, не оставляйте учебники, сведения, которые могут препятствовать успешное развертывание в реальном приложении.

Учебники предназначены для запуска в последовательности, и каждая часть на предыдущую часть. Тем не менее можно пропустить части, которые не относятся к данной ситуации. (Пропуск частей может потребоваться настроить процедуры, описанные на следующих занятиях рассматривается.)

## <a name="intended-audience"></a>Целевая аудитория

Учебники предназначены для разработчиков в среде ASP.NET, работающие в небольшой организации или в других средах где:

- Процесс непрерывной интеграции (автоматические построения и развертывания) не используется.
- В рабочей среде является стороннего поставщика услуг размещения.
- Обычно один пользователь может иметь несколько ролей (тот же пользователь разрабатывает, тестирует и развертывает).

В корпоративных средах обычно для реализации непрерывной интеграции процессов и в рабочей среде, как правило, размещенного на серверах компании. Разные люди также обычно выполняют разные роли. Сведения о развертывании предприятия см. в разделе [развертывание веб-приложений в корпоративных сценариях](../../deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).

Организаций всех размеров можно также развертывать веб-приложения в Azure, и большинство процедур, представленных в этих учебниках применяются также для веб-приложениях службы приложений Azure. Введение Azure см. в разделе [https://azure.microsoft.com](https://azure.microsoft.com).

## <a name="the-hosting-provider-shown-in-the-tutorials"></a>Поставщик услуг размещения, представленных в учебниках

Учебники помогут выполнить процесс установки учетная запись с услуг размещения и развертывание приложения этого поставщика услуг размещения. Был выбран определенных услуг размещения, таким образом, чтобы учебники удалось иллюстрируют процесс завершения развертывания на работающий веб-сайт. Каждого поставщика услуг размещения предоставляет различные функции и возможности развертывания на их серверах меняется немного; Тем не менее процесс, описанный в этом учебнике типично для всего процесса.

Поставщик услуг размещения, используемый в этом учебнике Cytanium.com, является одним из нескольких доступных и использовать его в этом учебнике не является одобрением или рекомендацией.

## <a name="deploying-web-site-projects"></a>Развертывание проектов веб-сайтов

Университет Contoso является проект веб-приложения Visual Studio. Большинство методов развертывания и средства, которые демонстрируются в данном учебнике не применяются к [проектов веб-сайтов](https://msdn.microsoft.com/library/dd547590.aspx). Сведения о развертывании проектов веб-сайтов см. в разделе [Карта содержимого развертывания ASP.NET](https://msdn.microsoft.com/library/bb386521.aspx#deployment_for_web_site_projects).

## <a name="deploying-aspnet-mvc-projects"></a>Развертывание проектов ASP.NET MVC

В этом учебнике развертывании проекта веб-форм ASP.NET, но все, что вы узнаете, как сделать также применима к ASP.NET MVC. Проект Visual Studio MVC — просто другую форму проекта веб-приложения. Отличается только что при развертывании на поставщике услуг размещения, который не поддерживает ASP.NET MVC или его требуемой версии, необходимо убедиться, что установлены соответствующие ([MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0) или [MVC 4](http://nuget.org/packages/aspnetmvc)) Пакета NuGet в проекте.

## <a name="programming-language"></a>Язык программирования

В примере приложения используется C#, но учебники не требуется знание C# и методы развертывания, представленные в учебниках не зависят от языка.

## <a name="troubleshooting-during-this-tutorial"></a>Устранение неполадок с помощью этого учебника

При возникновении ошибки во время развертывания или развернутого сайта работает неправильно, сообщения об ошибках не всегда предоставляют решение. Для некоторых распространенных проблем, [Устранение неполадок справочной странице](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md) доступен. Если вы получаете сообщение об ошибке или что-то не работает, как пройти учебники, обязательно обратитесь к странице устранения неполадок.

## <a name="comments-welcome"></a>Вас приветствует комментарии

Приглашаем вас комментарии на учебники и при обновлении учебника все усилия будут внесены учитывает учетной записи исправлений или подсказок для улучшения, которые предоставляются в комментариях учебника.

## <a name="prerequisites"></a>Предварительные требования

Прежде чем начать, убедитесь, что у вас есть Windows 7 или более поздней версии, и на компьютере установлена одна из следующих продуктов:

- [Visual Studio 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
- [Visual Web Developer Express 2010 с пакетом обновления 1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VWD2010SP1Pack)
- [Visual Studio 2012 RC или Visual Studio Express 2012 RC для Web](https://go.microsoft.com/fwlink/?LinkId=240162)

При наличии Visual Studio 2010 с пакетом обновления 1 или Visual Web Developer Express 2010 с пакетом обновления 1, следует также установите следующие продукты:

- [Azure SDK для .NET (VS 2010 с пакетом обновления 1)](https://go.microsoft.com/fwlink/?LinkID=208120) (включает обновление публикации Web)
- [Microsoft Visual Studio 2010 SP1 Tools для SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCEVSTools)

Другое программное обеспечение, необходимые для завершения этого учебника, но не нужно иметь, загружен. Учебник поможет вам выполнить шаги по установке его, когда он необходим.

## <a name="downloading-the-sample-application"></a>Загрузка образца приложения

Приложение, которое вы развернете называется Contoso университета и уже создан для вас. Он представляет собой упрощенную версию веб-сайта университета, слабо исходя из приложения Contoso университета, описанного в [Entity Framework учебники на сайте ASP.NET](https://asp.net/entity-framework/tutorials).

Если у вас есть необходимые компоненты, загрузите [веб-приложение Contoso университета](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b). *.Zip* файл содержит несколько версий проекта и PDF-файл, содержащий все 12 учебники. Для работы через последовательность шагов учебника, начните с ContosoUniversity Begin. Чтобы увидеть, как выглядит проекта в конце учебники, откройте ContosoUniversity-End. Чтобы узнать, как выглядит проект перед выполнением миграции до полного SQL Server в учебнике 10, откройте ContosoUniversity AfterTutorial09.

Чтобы подготовить для работы через шагах учебника, сохраните ContosoUniversity Begin любую папку, можно использовать для работы с проектами Visual Studio. По умолчанию используется следующая папка:

`C:\Users\<username>\Documents\Visual Studio 2012\Projects`

(Для снимков экрана в этом учебнике, папка проекта находится в корневом каталоге на `C`: диск.)

Запустите Visual Studio, откройте проект и нажмите клавиши CTRL + F5, чтобы запустить его.

[![Home_page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image2.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image1.png)

Страницы веб-сайта, доступны в строке меню и позволяют выполнять следующие функции:

- Отображение статистики студента (страница о программе).
- Отображение, изменение, удаление и добавление учащихся.
- Отображение и изменение курсов.
- Отображение и изменение инструкторов.
- Отображение и изменение отделов.

Ниже приведены снимки экрана несколько репрезентативной страниц.

[![Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image4.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image3.png)

[![Add_Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image6.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image5.png)

## <a name="reviewing-application-features-that-affect-deployment"></a>Обзор функций приложения, влияющие на развертывание

Следующие функции приложения влияет на способ развертывания и что необходимо сделать, чтобы развернуть его. Каждый из них является более подробно описываются в следующих учебниках в ряду.

- Университет Contoso использует базу данных SQL Server Compact для хранения данных приложения, такие как имена учащихся и инструкторов. База данных содержит сочетание тестовых данных и рабочих данных, а при развертывании в рабочей среде необходимо исключить тестовых данных. Далее в серии учебника будет перенос из SQL Server Compact в SQL Server.
- Приложение использует систему членства ASP.NET, где хранятся данные учетной записи пользователя в базе данных SQL Server Compact. Приложение определяет, кто имеет доступ к некие закрытые сведения пользователя-администратора. Необходимо выполнить развертывание базы данных членства без тестовые учетные записи, но с одну учетную запись администратора.
- Так как база данных приложения и базы данных членства использовать SQL Server Compact в качестве компонент database engine, необходимо развернуть компонент database engine для поставщика услуг размещения, а также самих базах данных.
- Приложение использует членства в универсальных поставщиков ASP.NET, чтобы система членства может хранить свои данные в базе данных SQL Server Compact. Сборки, содержащей поставщиков членства в универсальных должны быть развернуты вместе с приложением.
- Платформа Entity Framework 5.0 приложением для доступа к данным в базе данных приложения. Сборка, содержащая Entity Framework 5.0 должны быть развернуты вместе с приложением.
- Приложение использует ошибки сторонних разработчиков, журналы и отчетность служебной программы. Эта программа предоставляется в сборке, которая должны быть развернуты вместе с приложением.
- Программа ведения журнала ошибок записывает сведения об ошибке в XML-файлы в папку. У вас убедитесь в том, что учетной записи, под которым выполняется ASP.NET развернутого узла имеет разрешение на запись в эту папку, и имеется исключения этой папки из развертывания. (В противном случае данные журнала об ошибках из тестовой среды можно развернуть в рабочей среде или файлов журнала ошибок в рабочей среде могут быть удалены.)
- Приложение включает некоторые параметры, которые должны быть изменены в в развернутой *Web.config* файла в зависимости от целевой среде (тестовой или рабочей) и другие параметры, которые должны быть изменены в зависимости от сборки Конфигурация (Отладка или выпуск).
- Решение Visual Studio включает в себя проект библиотеки классов. Должны развертываться только сборки, который создает этот проект, не сам проект.

В этом учебнике первого ряда загружен пример проекта Visual Studio и проверить компоненты веб-сайтов, которые влияют на способ развертывания приложения. В следующих учебниках Подготовка развертывания с помощью настройки некоторые из этих действий автоматически обрабатываться. Другие позволяет устранить вручную.

>[!div class="step-by-step"]
[Вперед](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
