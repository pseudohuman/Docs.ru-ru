---
uid: web-pages/readme/overview
title: "Файл WebMatrix Readme | Документы Microsoft"
author: rick-anderson
description: "WebMatrix и ASP.NET Web Pages (Razor) версии 1.0 Readme"
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/06/2011
ms.topic: article
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: b8402aa3db1b2566878c4d56212facbbb2925eec
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2018
---
<a name="webmatrix-readme"></a>Файл сведений для WebMatrix
====================
13 января 2011 г.

## <a name="contents"></a>Описание

> [!NOTE]
> Этот файл readme применяется к версии 1.0 WebMatrix.


- [Обзор набора средств Visual Studio для Unity](#Overview)
- [Установка](#Installation_Notes)
- [Сведения о публикации приложений](#InstructionsForPublishingApplications)
- [Изменения и проблемы](#ChangesAndIssues)

    - [Установка WebMatrix 1.0](#Known_Issues_Installation)
    - [Веб-страницы ASP.NET](#Known_Issues_ASPNET)
    - [WebMatrix](#Known_Issues_WebMatrix)
    - [IIS Express](#Known_Issues_IISExpress)
    - [SQL Server Compact](#Known_Issues_SQLServerCompact)
    - [Установка приложений](#Known_Issues_Installing_Applications)
    - [Публикация приложений](#Known_Issues_Publishing_Applications)
- [Дополнительные сведения](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>Обзор

> Microsoft WebMatrix 1.0 представляет собой стек бесплатной разработки, который устанавливается в минутах. Она интегрирует веб-сервера базы данных и платформами программирования для создания единой, интегрированной среды. Вы можете использовать WebMatrix для упрощения разработки кода, тестирования и публикация собственных ASP.NET или PHP, веб-сайт, или вы можете использовать WebMatrix для создания нового веб-сайтов с помощью таких популярных приложений с открытым исходным кодом как DotNetNuke, Umbraco, WordPress и Joomla. WebMatrix использует же мощный веб-сервер, СУБД и платформы среды выполнения веб-сайта в Интернете, что упрощает и ускоряет переход из среды разработки в рабочей среде smooth и удобный.


<a id="Installation_Notes"></a>

## <a name="installation"></a>Установка

> Чтобы установить WebMatrix 1.0, необходимо сначала установить [платформы установщика Microsoft Web 3.0](https://go.microsoft.com/fwlink/?LinkID=194638). После установки установщика веб-платформы, его можно использовать для установки WebMatrix.
> 
> Если во время установки возникают проблемы, см. [Устранение неполадок с Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).


<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a>Сведения о публикации приложений

> В разделе [пошаговые инструкции для публикации приложений](https://go.microsoft.com/fwlink/?LinkID=196149)


<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a>Изменения и проблемы

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a>Проблемы с установкой 1.0 WebMatrix

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a>Проблема: WebMatrix 1.0 доступна только на платформах, поддерживающих Microsoft .NET Framework 4

> .NET Framework версии 4 является обязательным для WebMatrix. В некоторых случаях установщик WebMatrix 1.0 позволит попытается установить на платформу, которая не является частью набора поддерживаемых конфигураций. В частности Windows Vista без обновления SP1 позволит вам начать установку WebMatrix, но компонент .NET Framework 4 не удастся и блокировать установку.
> 
> **Workaround**  
> Установите на поддерживаемых платформах, включая:
> 
> - Windows 7
> - Windows Server 2008
> - Windows Server 2008 R2
> - Windows Vista с пакетом обновления 1 (SP1) или выше
> - Windows XP с пакетом обновления 3 (SP3)
> - Windows Server 2003 с пакетом обновления 2 (SP2)


#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>Проблема: Не удается установить WebMatrix 1.0, если Microsoft Visual Studio 2008 устанавливается без Microsoft Visual Studio 2008 с пакетом обновления 1

> **Workaround**  
> Установка [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) из центра загрузки Майкрософт.


#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a>Проблема: Некоторые сборки для SQL Server Compact 4.0 не установлены в глобальном кэше СБОРОК

> Управляемые сборки для SQL Server Compact 4.0 не помещается в глобальный кэш сборок (GAC), при установке SQL Server Compact 4.0 на 64-разрядном компьютере и что компьютер имеет только профиле .NET Framework 3.5 с пакетом обновления 1 клиента установлен. Управляемые сборки, которые не установлены в глобальном кэше СБОРОК являются:
> 
> - *System.Data.SqlServerCe.dll* (поставщика ADO.NET)
> - *System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework)
> 
> **Workaround**  
> Удаление SQL Server Compact 4.0. Загрузить и установить полную версию .NET Framework 3.5 с пакетом обновления 1 из следующего расположения:  
>   
> [Microsoft .NET Framework 3.5 пакетом обновления 1 (полный пакет)](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> Затем переустановите SQL Server Compact 4.0.


#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a>Проблема: Не удается удалить SQL Server Compact с помощью командной строки

> Удаление SQL Server Compact через параметры командной строки не работает в данном выпуске.
> 
> **Workaround**  
> Используйте *программы и компоненты* в панели управления Windows, чтобы удалить Microsoft SQL Server Compact 4.0.


<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a>Веб-страницы ASP.NET

Этот раздел документа описывает новые возможности, изменения и известные проблемы с версии 1.0 веб-страниц ASP.NET с синтаксисом Razor.

- [Новые возможности](#NewFeatures)
- [Изменения](#Changes)
- [Проблемы](#Issues)

#### <a id="NewFeatures"></a>Новые возможности

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a>Новинка: Добавлен параметр конфигурации для отключения диспетчера пакетов

> Новый `asp:AdminManagerEnabled` ключ доступен для `<appSettings>` элемент в *web.config* файл, который позволяет полностью отключить диспетчер пакетов. Значение по умолчанию для этого элемента имеет значение true, это значит, что, если он не включен в *web.config* включен файл диспетчера пакетов. Чтобы отключить диспетчер пакетов, добавьте следующий элемент для *web.config* файл в корневом каталоге веб-сайта:
> 
> [!code-xml[Main](overview/samples/sample1.xml)]


#### <a id="Changes"></a>Изменения

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a>Изменение: переименована в «asp: AdminFolderVirtualPath» ключ «webPages:AdminFolderVirtualPath»

> `webPages:AdminFolderVirtualPath` Ключ, который может быть добавлен к *web.config* был переименован файл, чтобы указать расположение диспетчер пакетов для использования `asp:` вместо пространства имен `webPages` пространства имен. Если используется этот элемент, его необходимо переименовать в файле конфигурации.


#### <a id="Issues"></a>Известные проблемы

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a>Проблема: Паролей авторизованных пользователей, которые больше не распознан

> Для большей безопасности был изменен алгоритм для создания и хранения паролей членства (имя входа). В результате пароли, сохраненные для членов (пользователей), созданных в бета-версии ASP.NET Razor не распознаются. 
> 
> **Инструкции по решению** Если сайт еще не были размещены в рабочей среде, удалить записи из базы данных членства. Если база данных находится в режиме реального времени, программным образом создать повторно существующие пароли в базе данных членства.


#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>Проблема: Непредвиденное поведение при использовании пользовательские таблицы для членства

> Чтобы инициализировать поставщик членства для веб-сайта ASP.NET Razor, вызовите `WebSecurity.InitializeDatabaseConnection` метод. (В WebMatrix шаблоне начального сайта включает вызов этого метода в  *\_AppStart.cshtml* файл.) Если `autoCreateTables` параметр этого метода имеет значение в значение true (по умолчанию, ему присваивается значение true, если в шаблоне начального сайта), и если имя таблицы нераспознанный передается в метод (второй параметр), метод не выдает ошибку. Вместо этого он автоматически создадут таблицу.
> 
> Это может вызвать проблемы, если планируется использовать пользовательские таблицы членства, но передает имя неправильной таблицы в `WebSecurity.InitializeDatabaseConnection` метод. Поскольку метод по умолчанию вызывает ошибку, если таблицы не существует, и вместо этого он создает новую таблицу, приложение может появиться работает. Тем не менее код приложения, который основан на пользовательские таблицы (и поля в нем) со временем может завершиться непредвиденные ошибки.
> 
> **Workaround**  
> Убедитесь, что имя, переданное в `InitializeDatabaseConnection` метод соответствует таблице в базе данных членства профиль пользователя, или убедитесь, что `autoCreateTables` параметр имеет значение false.


#### <a name="issue-error-message-the-admin-module-requires-access-to-appdata"></a>Проблема: Сообщение об ошибке «модуля администрирования требуется доступ к ~/App\_данных»

> В некоторых случаях для создания пользователей или работы со система членства ASP.NET может привести к странице для отображения ошибки *модуль администрирования требуется доступ к ~/App\_данные*. Это происходит, если учетная запись, под управлением IIS или IIS Express не имеет разрешения на создание и запись в *приложения\_данные* папки в корневом каталоге веб-сайта. 
> 
> **Инструкции по решению** вручную создать *приложения\_данные* папку веб-сайта. Убедитесь, что учетная запись Windows, то приложение запущено под (как правило, NETWORK SERVICE) имеет разрешения на чтение и запись для корневой папки приложения и для вложенных папок, таких как приложения\_данных. Более подробные сведения можно найти в статье базы знаний [проблемы с SQL Server Express пользователя при создании экземпляров и проектами веб-приложений ASP.net](https://support.microsoft.com/kb/2002980).


#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>Ошибка, проблема: «не удалось сформировать пользовательский экземпляр SQL Server»

> Если выполняется IIS 7.5 в Windows 7 или Windows Server 2008 R2 WebMatrix веб-приложение использует SQL Server Express, может появиться сообщение о том, что SQL Server не удалось получить путь локального приложения пользователя во время выполнения.
> 
> **Инструкции по решению** убедитесь, что учетная запись Windows, то приложение запущено под (как правило, NETWORK SERVICE) имеет разрешения на чтение и запись для корневой папки приложения и вложенные папки например *приложения\_данных*. Более подробные сведения можно найти в статье базы знаний [проблемы с SQL Server Express пользователя при создании экземпляров и проектами веб-приложений ASP.net](https://support.microsoft.com/kb/2002980).


#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a>Проблема: Файлы, содержащие ресурсы диспетчера пакетов или пароли диспетчера пакетов servable в службах IIS 6.0 и более ранних версий

> Если выполняется развертывание приложения было создано с помощью выпуска версии-кандидата 2 ASP.NET Web Pages (Razor), и если приложение содержит *password.txt* или *packagesources.txt* файл */App\_ Данные/admin*, IIS 6.0 будет предоставлять этот файл при поступлении запроса подвергает паролей для вашего экземпляра диспетчера пакетов. 
> 
> **Инструкции по решению** переименование *password.txt* или *packagesources.txt* файл *password.config* или *packagesources.config*. По умолчанию службы IIS 6.0 не обслуживает файлы, имеющие *.config* расширения. (В IIS 7, нет файлов в *приложения\_данные* обслуживаются папки, поэтому необходимо переименовать файлы.)


#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a>Проблема: Удаление пакеты, установленные с помощью бета-версии 3 не полностью удаляет компоненты пакета

> Если вы установили пакет с помощью диспетчера пакетов в бета-версии 3 и попытайтесь удалить его с помощью текущего выпуска, пакет не полностью удален. С помощью диспетчера пакетов **удаления** кнопка удаляет некоторые компоненты, но оставляет код библиотеки пакета и не обновляет *package.config* файла.
> 
> **Инструкции по решению**   
> Выполните следующие действия.  
> 1. Удалить *приложения\_Data\packages* папки. При этом удаляются все пакеты.   
> 2. Удалить *packages.config* файл в корневом каталоге веб-сайта.


#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a>Проблема: В Visual Studio вызова диспетчер пакетов веб-переводит приложение автономный режим

> Если вы работаете в Visual Studio (не WebMatrix) и использовать  *\_администратора* функциональные возможности, чтобы запустить диспетчер пакетов Visual Studio переводит приложение в автономный режим и отправляет *приложения\_ OFFLINE.htm* в корневой папке веб-сайта, что прерывает возможность использовать диспетчер пакетов.
> 
> [!NOTE]
> Несмотря на то, что такое поведение обычно появляются при с помощью интерфейса диспетчера веб-пакета, то же поведение возникает, если добавить, удалить или изменить любые файлы в *приложения\_данные* папки.
> 
> **Инструкции по решению**   
> Для работы с пакетами в среде Visual Studio, воспользуйтесь расширение NuGet вместо веб-пакета. Сведения см. в разделе [документации по NuGet](https://docs.microsoft.com/nuget/). При работе с другими файлами в *приложения\_данные* папки, рекомендуется использовать файлы в другом месте, чтобы избежать этой проблемы. Если это невозможно, удалите *приложения\_offline.htm* файл вручную, или подождать, пока узел восстанавливает подключение автоматически (по умолчанию через 30 секунд).


#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>Проблема: Visual Studio IntelliSense и шаблоны проектов доступны только в ASP.NET MVC 3

> Установка веб-страниц ASP.NET не также устанавливает средства для Visual Studio как IntelliSense и шаблоны проектов для приложений веб-страниц ASP.NET.
> 
> **Инструкции по решению** для использования IntelliSense и шаблоны проектов для приложений веб-страниц ASP.NET в Visual Studio, установить ASP.NET MVC 3, версия-Кандидат либо с помощью установщика веб-платформы или [автономного установщика](https://go.microsoft.com/fwlink/?LinkID=191797).


#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>Проблема: Чтение веб-каналов или другие внешние источники данных через прокси-сервер

> Если на сервере сайта находится за прокси-сервер, может потребоваться настроить сведения о прокси-сервера в *web.config* файл, чтобы иметь возможность считывать данные, поступающие от вне локального узла. Например, если вы используете `ReCaptcha` вспомогательный, вспомогательное приложение взаимодействует со службой reCAPTCHA, но может быть заблокирован прокси-сервером. Аналогично веб-каналов, используемые веб-страницах ASP.NET, такие как веб-канал, используемый диспетчер пакетов, может потребоваться настройка прокси-сервера.
> 
> Если возникли проблемы в работе с внешней службы или при работе с пакетом, в веб-канала, помещаются следующие элементы в корневого каталога приложения *web.config* файла:
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> Дополнительные сведения о настройке прокси-сервера см. в разделе [ &lt;прокси&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) на сайте MSDN.


#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>Проблема: Удаление .NET Framework версии 4 отключает веб-страниц ASP.NET с синтаксисом Razor

> Если удалить .NET Framework версии 4, а затем переустановите его, веб-страниц ASP.NET с синтаксисом Razor отключена. Страницы с *.cshtml* расширения работают правильно. Веб-страницы ASP.NET регистрирует сборку в корневой папке машины *web.config* файла и удаление .NET Framework удаляет этот файл. Повторная установка .NET Framework устанавливает новую версию файла конфигурации, но не добавляет ссылку для сборки веб-страниц ASP.NET.
> 
> **Инструкции по решению** после повторной установки .NET Framework, переустановите ASP.NET Web Pages с синтаксисом Razor. При этом добавляется следующий элемент для *web.config* файл в корне машины, которое обычно находится в следующем расположении:  
>   
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]


#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a>Проблема: Без расширений URL-адреса не найдены файлы.cshtml/.vbhtml в IIS 7 или IIS 7.5

> В IIS 7 или IIS 7.5, запросы с URL-адреса следующего вида не удается найти страниц, имеющих *.cshtml* или *.vbhtml* расширения:  
>   
> `http://www.example.com/ExampleSite/ExampleFile`  
>   
> Проблема возникает из-за перезаписи URL-адресов не включена по умолчанию для IIS 7 или IIS 7.5. Возможная сценарий существует, вы не видите проблемы при тестировании локально с помощью IIS Express, но возникают при развертывании веб-сайта для размещения веб-сайта.
> 
> **Workaround**
> 
> - Если у вас есть контроль над компьютером сервера, на компьютере сервера установите обновление, описанное в [обновление доступно, что позволяет определенным обработчикам служб IIS 7.0 или IIS 7.5 обрабатывать запросы, URL-адреса не заканчиваться точкой](https://support.microsoft.com/kb/980368).
> - Если у вас по управлению компьютером сервера (например, развертывается для размещения веб-сайта), добавьте следующий на веб-сайт *web.config* файла: 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]


#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>Проблема: Развертывание приложения на компьютере, не поддерживает SQL Server Compact установлена

> Приложения, включающие баз данных SQL Server Compact могут выполняться на компьютере, где SQL Server Compact не установлена. Microsoft WebMatrix 1.0 автоматически копирует эти двоичные файлы для вас и выполняет соответствующее *web.config* файла преобразования.
> 
> **Инструкции по решению** Если вам нужно скопировать эти файлы и сделать *web.config* изменения файлов вручную, выполните следующие действия:
> 
> 1. Скопируйте сборки ядра базы данных для *Bin* папку (и вложенные папки), приложения на целевом компьютере:  
> 
>     - Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*   
>         **to** *\Bin*
>     - Копировать *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*** для *** \Bin\x86*
>     - Копировать *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\****для *** \Bin\amd64*
> 2. В корневой папке веб-сайта, создайте или откройте *web.config* файла. (В версии 1.0 WebMatrix этот тип файлов доступна при нажатии кнопки **все** в **выберите тип файла** диалоговое окно.)
> 3. Добавьте следующий элемент в качестве дочернего элемента `<configuration>` элемента (не внутри `<system.web>` элемент):
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]


#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>Проблема: «Базы данных» и «WebGrid» вспомогательные методы не работают со средним уровнем доверия в Visual Basic

> Если вы используете Visual Basic (создание *.vbhtml* файлы), `Database` и `WebGrid` вспомогательные методы не будет работать, если приложения настроен для использования со средним уровнем доверия.
> 
> **Workaround**  
> При использовании Visual Studio 2010, можно разрешить эту проблему путем установки выпуска пакета обновления 1. Пока не станет доступен окончательной версии выпуска пакета обновления 1, можно загрузить бета-версии с пакетом обновления 1 из [Microsoft Visual Studio 2010 с пакетом обновления 1 бета-версию обновления](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) страницы в центре загрузки Майкрософт.   
>   
> Если это нецелесообразно, или если вы не используете Visual Studio 2010, можно временно задать приложение для использования полного доверия.


#### <a name="issue-applicationpart-resources-are-externally-accessible"></a>Проблема: «ApplicationPart» ресурсы, доступны извне

> Если сборка содержит объекты, является производным от `ApplicationPart` класса ресурсы сборки предоставляемых `ResourceRouteHandler` класса. Например рассмотрим следующий URL-адрес:  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> Этот запрос загружает все строки ресурса в *System.Web.WebPages.Administration.dll* сборки. Загружаются все внедренные ресурсы (даже те, которые не предназначены для обслуживаемых как статическое содержимое). Если внедренные ресурсы содержат конфиденциальную информацию, это может представлять угрозу безопасности. 
> 
> **Инструкции по решению**   
> Если вы создаете **ApplicationPart** объектов, убедитесь, что внедренные ресурсы, связанные с **ApplicationPart** сборки объекта не содержат конфиденциальной информации.


<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a>WebMatrix

> [!NOTE]
> Сведения о проблемах при установке для WebMatrix содержатся [проблем установки WebMatrix](#Known_Issues_Installation) ранее в этом документе.


Документ в этом разделе описаны известные проблемы для среды разработки WebMatrix.

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a>Проблема: Изменения в имени пользователя или пароля в строку подключения базы данных в файле web.config не отражаются в рабочей области баз данных

> **Workaround**  
> 
> 1. В *web.config* файл, измените имя базы данных в строке подключения (например, добавьте «1» на него).
> 2. Сохранить *web.config* файла.
> 3. Нажмите кнопку **баз данных** и обновления.
> 4. Изменить имя базы данных в строке подключения в *web.config* файл обратно исходное имя базы данных.
> 5. Сохранить *web.config* файла.
> 6. Нажмите кнопку **баз данных** и обновления.


#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a>Проблема: Не удается удалить папки, созданные WebMatrix

> Если запущен с повышенными правами, WebMatrix (то есть запущен с помощью WebMatrix **Запуск от имени администратора** в Windows), нельзя удалять папки, созданные с WebMatrix с помощью проводника Windows.
> 
> **Workaround**  
> Запустите проводник, используя повышенные разрешения. Выполните следующие действия.  
> 
> 1. В Windows, нажмите кнопку **запустить**.
> 2. Введите «Проводник» и щелкните правой кнопкой мыши запись для **Проводник**.
> 3. Нажмите кнопку **Запуск от имени администратора**. Папки можно удалить.


#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a>Проблема: Не удалось выполнить определенные задачи, требующие повышения прав WebMatrix 1.0

> WebMatrix 1.0 не может выполнять определенные задачи, требующие повышения прав, таких как установка дополнительных компонентов в следующих ситуациях:
> 
> - В Windows Vista или Windows 7 вы вошли под учетной записью, у которого нет прав администратора, и управления учетных записей (UAC) отключено.
> - Вы используете Microsoft Windows XP или Microsoft Windows Server 2003.
> 
> **Workaround**  
> Большинство задач в WebMatrix 1.0 необходимы разрешения администратора. Для тех, которые можно выполнять операции от имени администратора или выполните следующие действия:
> 
> - В Windows Vista или Windows 7 включите контроль учетных Записей.
> - В Windows XP добавьте пользователя в группу безопасности "Администраторы".


#### <a name="issue-site-from-web-gallery-is-disabled"></a>Проблема: Отключен «Из галерею веб-узла»

> **Сайта из веб-коллекции** параметр отключен, если не установлен установщик веб-платформы 3.0.
> 
> **Workaround**  
> Установка [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).


#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a>Проблема: Google Chrome не доступен в качестве параметра запуска

> Google Chrome не отображается в списке браузеров в **запуска** на **Главная** вкладки.
> 
> **Workaround**  
> В некоторых версиях Google Chrome не регистрируют себя правильно с функцией программ по умолчанию в Windows. Чтобы избежать этого, Google Chrome, выберите пункт *Настройка и управление Google Chrome* меню, нажмите кнопку *параметры*и нажмите кнопку *марка Google Chrome обозреватель по умолчанию*.


#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a>Проблема: Диалоговое окно «Foreign Key» не допускает ввод первичного ключа

> **Foreign Key** диалоговое окно не позволяет ввести имя первичного ключа из таблицы первичного ключа.
> 
> **Workaround**  
> Это сделано намеренно. Необходимо ввести имя первичного ключа из таблицы первичного ключа.


#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a>Проблема: Технология IntelliSense не доступна в WebMatrix, Razor синтаксис, C# или Visual Basic

> Технология IntelliSense поддерживается в WebMatrix для HTML и CSS. Тем не менее не доступны для других языков. 
> 
> **Инструкции по решению**   
> Отсутствует.


#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a>Проблема: IntelliSense для HTML и CSS предлагает элементы, которые не подходят зависимости от контекста

> IntelliSense для разметки в WebMatrix поддерживает HTML с помощью [схема XHTML 1.0 Transitional](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) и CSS с помощью [схемы CSS 2.1](http://www.w3.org/TR/CSS2/). Так как IntelliSense основана на эти конкретные схемы, определенные теги, атрибутов или свойств может предложенные, еще не подходит для определения текущего страницы или стиль. Для HTML он может также привести к неожиданным предложения в содержимом, которое может быть интерпретировано как неправильного формата XHTML (например, если теги не закрыты). Эта проблема может быть более наглядными, если позиция ввода находится внутри тега неполный; в этом случае IntelliSense может предложить новые открывающие теги или другие неверные оптимизации. 
> 
> **Инструкции по решению**   
> Для HTML убедитесь, что вы работаете с правильным форматом, завершенной страниц XHTML. Для CSS решение отсутствует.


#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a>Проблема: IntelliSense не вызывается во время ввода

> В некоторых случаях IntelliSense не может быть вызван, как HTML и CSS, вводимых в редакторе. В частности это может произойти, когда курсор находится непосредственно рядом с другим элементом, или в конце файла. 
> 
> **Инструкции по решению**   
> Убедитесь, что имеется вокруг курсора и курсор не в конце файла. IntelliSense также можно вызвать вручную, нажав клавиши Ctrl + Пробел.


#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a>Проблема: Пользовательский Интерфейс не доступен для отключения IntelliSense

> WebMatrix 1.0 позволяет без пользовательского интерфейса или жеста отключать IntelliSense. 
> 
> **Инструкции по решению**   
> Запустите WebMatrix, выполните следующую команду, которая включает параметр, который отключает IntelliSense:  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`


<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a>IIS Express

IIS Express имеет свой собственный файл readme, который доступен по следующему АДРЕСУ:

[https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a>SQL Server Compact

SQL Server Compact имеет свой собственный файл readme, который доступен по следующему АДРЕСУ:

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

Сведения о проблемы, связанные с установкой SQL Server Compact в составе WebMatrix разделе [проблем установки WebMatrix](#Known_Issues_Installation) ранее в этом документе.

### <a id="Known_Issues_Installing_Applications"></a>Установка приложений

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>Проблема: При установке приложения может занять много времени при пользовательской папке "Мои документы" перенаправляется в общую сетевую папку

> **Workaround**  
> Отсутствует. Приложение может занять некоторое время, чтобы установить, но устанавливается правильно.


### <a id="Known_Issues_Publishing_Applications"></a>Публикация приложений

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a>Проблема: «требуемые разрешения не могут быть получены» ошибка при публикации базы данных SQL Compact

> WebMatrix не полностью поддерживает развертывание вспомогательные двоичные файлы для SQL Server Compact на сервере под управлением .NET Framework версии 3.5 с конфигурацией среднего уровня доверия.
> 
> **Workaround**  
> Предпочтительный обходным путем является установка .NET Framework 4 на сервере. Кроме того выполните следующее:
> 
> 1. Добавьте следующие элементы для `SecurityClasses` статьи *Web\_MediumTrust.config* файла:
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. Создать новый набор разрешений *Web\_MediumTrust.config* файл следующие необходимые разрешения:
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. Применить набор разрешений для SQL Server Compact, помещая следующие элементы *Web\_MediumTrust.config* файла:
> 
>     [!code-html[Main](overview/samples/sample8.html)]


#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a>Проблема: Веб-приложения в галерее и PhpBB отображает ошибку «Служба недоступна» после публикации

> В некоторых случаях публикации приложения приведет к ошибке «служба недоступна».
> 
> **Workaround**  
> В WebMatrix, добавьте обратную косую черту (\) в конец имени сервера в **параметры публикации** окна, а затем опубликовать приложение еще раз.


#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a>Проблема: Moodle макет веб-сайта и ссылки перестают работать после публикации

> После публикации приложения Moodle, приложение будет работать неправильно.
> 
> **Workaround**  
> В WebMatrix, добавьте косую черту (/) в конец **имя сайта** в **параметры публикации** окна, а затем опубликовать приложение еще раз.


#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a>Проблема: Публикация nopCommerce приведет к ошибке базы данных

> Публикации nopCommerce завершается ошибкой и сообщает об ошибке базы данных как «вставьте nop\_таблицы журнала не удалось.»
> 
> **Workaround**  
> 
> 1. В WebMatrix, щелкните **запуска** для запуска nopCommerce локально.
> 2. Войдите на странице администрирования.
> 3. Нажмите кнопку **системы** меню.
> 4. Нажмите кнопку **журнала** параметр.
> 5. Нажмите кнопку **очистить журнал** кнопки.
> 6. Опубликуйте nopCommerce еще раз.


#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a>Проблема: Silverstripe CMS отображается «HTTP 500 PHP FCGI ошибка» при загрузке опубликованного узла

> **Workaround**  
> После нажатия кнопки **загрузки публикации узла**, пропустить `silverstripe-cache/manifest_main` в **Просмотр публикации**. Этот файл используется для кэширования и относится только к каждому компьютеру.


#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a>Проблема: Subtext отображает «Ошибка сервера в приложении '/'» при загрузке опубликованного узла

> **Workaround**  
> Откройте сайт *web.config* и замените идентификатор пользователя и пароль в строке подключения базы данных с учетными данными администратора SQL Server («sa» учетные данные).
> 
> Кроме того, выполните следующие действия, чтобы предоставить учетной записи пользователя, вы вошли в систему `db_owner` разрешения:
> 
> 1. Установка SQL Server Management Studio с помощью установщика веб-платформы.
> 2. Подключение к локальному экземпляру SQL Server Express (по умолчанию `.\SQLEXPRESS`).
> 3. Нажмите кнопку **баз данных** &gt; *[localSubtextDatabase]* &gt; **безопасности** &gt; **пользователей** &gt; *[localSubtextUser*] (по умолчанию — `subtextuser`], щелкните правой кнопкой мыши и нажмите кнопку **свойства**.
> 4. Выберите **db\_владельца** раздела членство в роли.


#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a>Проблема: Сайта может не работать после публикации, если поле «URL-адрес назначения» нет префикса http:// или https://

> В **параметры публикации** диалоговое окно, если URL-адрес назначения не начинается с `http://` или `https://`, сайт может не работать после развертывания.
> 
> **Workaround**  
> Убедитесь, что перед публикацией сайта, URL-адрес назначения в **параметры публикации** диалоговое окно начинается с `http://` или `https://`.


#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a>Проблема: Публикация базы данных MySQL завершается с ошибкой «не удалось опубликовать базу данных. Это может произойти, если удаленная база данных не может запустить сценарий.»

> Эта ошибка может возникнуть по ряду причин. Одна из причин этой ошибки можно увидеть, — если сценарий базы данных содержит символ одиночные кавычки (') и не является база данных MySQL назначения по умолчанию используется кодировка UTF-8.
> 
> **Workaround**  
> Задайте кодировку по умолчанию для удаленной базы данных MySQL в UTF-8.


#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a>Проблема: Некоторые ссылки не отображаются в DotNetNuke после публикации или загрузка узла

> При публикации или загрузить узла DotNetNuke, может потребоваться очистить кэш, чтобы получить новые ссылки на отобразились на сайте.
> 
> **Workaround**
> 
> 1. Войдите в систему как «Узел».
> 2. Перейдите к меню узел и выберите **параметры узла**.
> 3. Прокрутите список вниз и в разделе **Дополнительные параметры**, разверните **параметры производительности**.
> 4. Нажмите кнопку **очистить кэш** ссылку для страницы.
> 5. Перейдите к нижней части страницы и перезапустить приложение.


#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a>Проблема: Некоторые ссылки в AtomSite не работают после загрузки опубликованного узла

> **Workaround**  
> В *service.config* файла, *users.config* файла и всех *.xml* файлы, замените строку URL-адреса (например, `http://myhost.com/atomsite`) с локальной (например, `http://localhost:1239`).


#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a>Проблема: MySQL-приложений, как в WordPress не смогут публиковать и сообщения об ошибке в базе данных

> По умолчанию WebMatrix устанавливается MySQL с кодировкой UTF-8. Если установка MySQL самостоятельно, а не кодировку UTF-8 (например, это Latin1), процесс публикации для баз данных может завершиться сбоем.
> 
> **Workaround**
> 
> 1. Измените кодировку, MySQL, кодировка UTF-8. (Дополнительные сведения см. в разделе [набор символов сервера и параметры сортировки](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) MySQL веб-сайта.)
> 2. Переустановите приложение.
> 3. Повторно опубликуйте приложение.


#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a>Проблема: «Загрузки публикации узла» завершается ошибкой для приложений, имеющих установки на основе браузера

> Некоторые приложения (например, Kentico CMS) требуется запускать их в браузере для выполнения программы установки после установки, например для создания базы данных. При публикации приложения следующим образом без завершения установки на основе браузера, попытка загрузить на одном сайте с удаленного сервера завершится ошибкой.
> 
> **Workaround**  
> Завершите установку с использованием обозревателя перед публикацией узла.


#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a>Проблема: «Загрузки публикации узла» приведет к ошибке базы данных для DotNetNuke и Kooboo CMS

> Если при попытке загрузить приложения с сервера, и иметь учетные данные администратора в строку подключения базы данных в **параметры публикации** диалогового окна, может появиться следующая ошибка в журнале публикации:
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> **Workaround**  
> Если это возможно, повторно опубликовать сайт (или опубликовать его) с помощью учетных данных без прав администратора для базы данных.


<a id="More_Info"></a>

## <a name="for-more-information"></a>Дополнительные сведения

Дополнительные сведения о WebMatrix 1.0 см. ниже веб-сайтов:

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

© Корпорация Майкрософт, 2011. Все права защищены. [Условия использования](https://msdn.microsoft.cos/cc300389.aspx).
