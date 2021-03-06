---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: "Выполнение то, что если развертывание | Документы Microsoft"
author: jrjlee
description: "В этом разделе описываются способы решения «что если» (или имитируемые) развертываний с помощью инструмента веб-развертывания (Web Deploy) Internet Information Services (IIS) и V..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: cea805c86f0764c7443ccc5c9f89248860a6a842
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2018
---
<a name="performing-a-what-if-deployment"></a>Для выполнения развертывания «Что, если»
====================
по [Джейсон Lee](https://github.com/jrjlee)

[Скачать PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> В этом разделе описывается выполнение «что, если» (или имитируемые) развертываний с помощью инструмента веб-развертывания (Web Deploy) Internet Information Services (IIS) и VSDBCMD. Это позволяет определить последствия логику развертывания в среде с конкретной цели, до фактического развертывания приложения.


Этот раздел входит в состав серию учебников, исходя из требования к развертыванию enterprise вымышленная компания Fabrikam, Inc. Этот учебник ряд использует образец решения & #x 2014; [решения диспетчера контактов](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)& #x 2014; для представления веб-приложения с реалистичных уровень сложности, включая приложения ASP.NET MVC 3, Windows Службы Communication Foundation (WCF) и проект базы данных.

Метод развертывания, в основе этих учебников основан на разбиение проекта файл подход, описанный в [основные сведения о файле проекта](../web-deployment-in-the-enterprise/understanding-the-project-file.md), в которой управляет процессом построения и развертывания двух файлов проекта & #x 2014; o NE, содержащий инструкции сборки, которые применяются для каждой целевой среде и, содержащий параметры построения и развертывания конкретной среды. Во время построения файла проекта среды объединяется в файл проекта зависит от среды, образуют полный набор инструкций построения.

## <a name="performing-a-what-if-deployment-for-web-packages"></a>Выполнение развертывания «Что, если» для веб-пакеты

Веб-развертывания включает функциональность, которая позволяет выполнять развертывание в «что, если» (или пробной версии) режиме. При развертывании артефактов в режиме «что, если» веб-развертывания создает файл журнала, как если бы вы выполнили развертывание, но он не фактически вносит изменения на сервере назначения. Просмотр файла журнала может помочь понять, как повлияет развертывания на конечном сервере, в частности:

- Что будет добавятся.
- Что будет обновляться.
- Что будут удалены.

Из-за развертывания «что, если» не фактически вносит изменения на сервере назначения, что он не всегда можно сделать прогноз, является ли развертывание успешно завершится.

Как описано в [веб-развертывание пакетов](../web-deployment-in-the-enterprise/deploying-web-packages.md), можно развернуть с помощью веб-развертывания в двух способов & #x 2014; с помощью MSDeploy.exe программу командной строки напрямую или путем запуска веб-пакеты *. deploy.cmd* файл, создаваемый в процессе построения.

Если вы используете MSDeploy.exe напрямую, можно выполнить развертывание «что, если» путем добавления **– whatif** флаг в команду. Например чтобы оценить, что может произойти, если пакет был развернут на ContactManager.Mvc.zip в промежуточной среде, MSDeploy команда должна выглядеть следующим образом:


[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]


Если вы удовлетворены результатами развертывания «что, если», можно удалить **– whatif** флаг выполнения динамической развертывания.

> [!NOTE]
> Дополнительные сведения о параметрах командной строки для MSDeploy.exe см. в разделе [веб-развертывание параметров операции](https://technet.microsoft.com/library/dd569089(WS.10).aspx).


Если вы используете *. deploy.cmd* файл, можно запустить развертывания «что, если», включая **/t** флаг флаг (пробный режим), а не **/y** флаг («Да» или режим обновления) в в команду. Например, чтобы оценить, что может произойти, если пакет был развернут на ContactManager.Mvc.zip, запустив *. deploy.cmd* файл, команда должна выглядеть следующим образом:


[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]


Если вы удовлетворены результатами развертывания «в режиме пробной версии», можно заменить **/t** флаг с **/y** флаг выполнения динамической развертывания:


[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]


> [!NOTE]
> Дополнительные сведения о параметрах командной строки для *. deploy.cmd* файлов, в разделе [как: установка, развертывание пакета с помощью deploy.cmd файл](https://msdn.microsoft.com/library/ff356104.aspx). При запуске *. deploy.cmd* файл без указания всевозможные флаги, отображает список доступных флагов командной строки.


## <a name="performing-a-what-if-deployment-for-databases"></a>Выполнение развертывания «Что, если» для баз данных

В этом разделе предполагается, что вы используете программу VSDBCMD выполнить развертывание добавочных, на основе схемы базы данных. Этот подход является более подробно в [развертывание проектов базы данных](../web-deployment-in-the-enterprise/deploying-database-projects.md). Рекомендуется ознакомиться с этим разделом перед применением описанные здесь принципы.

При использовании VSDBCMD в **развернуть** режиме, можно использовать **/dd** (или **/DeployToDatabase**) флаг управления VSDBCMD фактически выполняет развертывание базы данных или просто приводит к возникновению ошибки скрипт развертывания. Если вы развертываете DBSCHEMA-файл, это поведение:

- При указании **/dd+** или **/dd**, VSDBCMD создаст скрипт развертывания и развертывания базы данных.
- При указании **/dd-** или ключ пропущен, VSDBCMD создаст только скрипт развертывания.

> [!NOTE]
> Если вы развертываете DEPLOYMANIFEST-файл, а не файл DBSCHEMA поведение **/dd** коммутатора гораздо более сложен. По существу, VSDBCMD будет игнорировать значение **/dd** перейти при DEPLOYMANIFEST-файл включает **DeployToDatabase** элемент со значением **True**. [Развертывание проектов базы данных](../web-deployment-in-the-enterprise/deploying-database-projects.md) описывает это поведение в полном объеме.


Например, чтобы создать скрипт развертывания для **ContactManager** базы данных без фактического развертывания базы данных в команду VSDBCMD должен выглядеть примерно следующим образом:


[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]


VSDBCMD это средство развертывания разностную копию базы данных, и таким образом динамически создается скрипт развертывания для хранения всех команд SQL, необходимые для обновления текущей базы данных, если таковая существует, для указанной схемы. Просмотр скрипта развертывания является удобным способом для определения того, какое влияние развертывания будет иметь в текущей базе данных и данных, содержащихся в нем. Например может потребоваться указать:

- Будут ли удалены все существующие таблицы и, приведет к потере данных.
- Порядок операций несет риск потери данных, например, если вы разбиения или слияния таблиц.

Если вы довольны скрипт развертывания, можно повторить VSDBCMD с **/dd+** флаг для внесения изменений. Кроме того можно изменить скрипт развертывания для удовлетворения требований и выполнить его вручную на сервере базы данных.

## <a name="integrating-what-if-functionality-into-custom-project-files"></a>Интеграция «Что, если» функциональные возможности в файлы проектов

Для более сложных сценариев развертывания, необходимо использовать пользовательский файл проекта Microsoft Build Engine (MSBuild) для инкапсуляции логики построения и развертывания, как описано в [основные сведения о файле проекта](../web-deployment-in-the-enterprise/understanding-the-project-file.md). Например, в [диспетчера контактов](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) образец решения, *Publish.proj* файла:

- Построение решения.
- Использует веб-развертывания для упаковки и развертывания приложения ContactManager.Mvc.
- Использует веб-развертывания для упаковки и развертывания приложения ContactManager.Service.
- Развертывает **ContactManager** базы данных.

При интеграции развертывание нескольких базы данных или веб-пакетов в один шаг процесс таким образом, можно также выполнять всего развертывания в режиме «что, если».

*Publish.proj* файл демонстрирует, как это сделать. Во-первых необходимо создать свойство для хранения значения «что, если»:


[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]


В этом случае вы создали свойство с именем **WhatIf** со значением по умолчанию **false**. Переопределить значение этого свойства значение **true** в параметре командной строки, как вы увидите.

Следующий этап — параметризацию любой веб-развертывания, VSDBCMD команд, чтобы отразить флаги **WhatIf** значение свойства. Например, следующий целевой объект (из *Publish.proj* файла и упрощенное) выполняется *. deploy.cmd* файл для развертывания веб-пакета. По умолчанию команда включает **/Y** switch («Да» или режим обновления). Если **WhatIf** равно **true**, оно заменяется **/t** switch (пробной версии или режим «что, если»).


[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]


Аналогичным образом следующий целевой объект использует служебную программу VSDBCMD для развертывания базы данных. По умолчанию **/dd** ключ не включен. Это означает, что VSDBCMD будет создать скрипт развертывания, но не будет выполнять развертывание базы данных & #x 2014; другими словами, «что, если» сценарий. Если **WhatIf** не задано значение **true**, **/dd** добавлен переключатель и VSDBCMD будет выполнять развертывание базы данных.


[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]


Можно использовать тот же подход можно параметризовать все соответствующие команды в файле проекта. Если вы хотите выполнить развертывание «что, если», затем можно просто предоставить **WhatIf** значение свойства из командной строки:


[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]


Таким образом можно запустить для всех компонентов проекта за один шаг развертывания «что, если».

## <a name="conclusion"></a>Заключение

В этом разделе описано, как запустить «что, если» развертываний, с помощью веб-развертывания, VSDBCMD и MSBuild. Развертывание «что, если» позволяет оценить влияние предложенных развертывания, прежде чем фактически вы внесли изменения в целевой среде.

## <a name="further-reading"></a>Дополнительные сведения

Дополнительные сведения о синтаксисе командной строки на веб-развертывания см. в разделе [веб-развертывание параметров операции](https://technet.microsoft.com/library/dd569089(WS.10).aspx). Рекомендации по параметрам командной строки при использовании *. deploy.cmd* файла см. в разделе [как: установка, развертывание пакета с помощью deploy.cmd файл](https://msdn.microsoft.com/library/ff356104.aspx). Рекомендации по VSDBCMD синтаксис командной строки см. в разделе [Справочник по командной строке для VSDBCMD. EXE (развертывание и импорт схемы)](https://msdn.microsoft.com/library/dd193283.aspx).

>[!div class="step-by-step"]
[Назад](advanced-enterprise-web-deployment.md)
[Вперед](customizing-database-deployments-for-multiple-environments.md)
