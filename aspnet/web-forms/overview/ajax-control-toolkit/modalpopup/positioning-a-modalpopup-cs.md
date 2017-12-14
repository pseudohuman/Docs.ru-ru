---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
title: "Позиционирование ModalPopup (C#) | Документы Microsoft"
author: wenz
description: "Элемент управления ModalPopup в наборе элементов управления AJAX предлагает простой способ создания модальное окно, с помощью клиентских средств. Однако элемент управления не предлагает..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 1caac9d0-e21e-49d6-a8ff-e563a736d6ca
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 8dcc4e20ac98cbbad1ea3e86b7f895d32c853d4a
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="positioning-a-modalpopup-c"></a><span data-ttu-id="cda78-104">Позиционирование ModalPopup (C#)</span><span class="sxs-lookup"><span data-stu-id="cda78-104">Positioning a ModalPopup (C#)</span></span>
====================
<span data-ttu-id="cda78-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="cda78-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="cda78-106">[Загрузить код](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="cda78-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)</span></span>

> <span data-ttu-id="cda78-107">Элемент управления ModalPopup в наборе элементов управления AJAX предлагает простой способ создания модальное окно, с помощью клиентских средств.</span><span class="sxs-lookup"><span data-stu-id="cda78-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="cda78-108">Однако элемент управления не предоставляет встроенные функциональные возможности для размещения всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="cda78-108">However the control does not offer a built-in functionality to position the popup.</span></span>


## <a name="overview"></a><span data-ttu-id="cda78-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="cda78-109">Overview</span></span>

<span data-ttu-id="cda78-110">Элемент управления ModalPopup в наборе элементов управления AJAX предлагает простой способ создания модальное окно, с помощью клиентских средств.</span><span class="sxs-lookup"><span data-stu-id="cda78-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="cda78-111">Однако элемент управления не предоставляет встроенные функциональные возможности для размещения всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="cda78-111">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="cda78-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="cda78-112">Steps</span></span>

<span data-ttu-id="cda78-113">Чтобы активировать функциональные возможности ASP.NET AJAX и набора средств управления `ScriptManager`.</span><span class="sxs-lookup"><span data-stu-id="cda78-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager`.</span></span> <span data-ttu-id="cda78-114">элемент управления необходимо поместить в любом месте на странице (но в `<form>` элемент):</span><span class="sxs-lookup"><span data-stu-id="cda78-114">control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample1.aspx)]

<span data-ttu-id="cda78-115">Добавьте панель, который служит в качестве модальное окно.</span><span class="sxs-lookup"><span data-stu-id="cda78-115">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="cda78-116">Кнопки используется, чтобы закрыть всплывающее окно:</span><span class="sxs-lookup"><span data-stu-id="cda78-116">A button is used to close the popup:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample2.aspx)]

<span data-ttu-id="cda78-117">Каждый раз, когда отображается всплывающее окно, его должны размещаться в определенное место на странице.</span><span class="sxs-lookup"><span data-stu-id="cda78-117">Whenever the popup is shown, it shall be positioned at a certain place in the page.</span></span> <span data-ttu-id="cda78-118">Эта задача создается клиентские функции JavaScript.</span><span class="sxs-lookup"><span data-stu-id="cda78-118">For this task, a client-side JavaScript function is created.</span></span> <span data-ttu-id="cda78-119">Сначала пытается получить доступ к панели.</span><span class="sxs-lookup"><span data-stu-id="cda78-119">It first tries to access the panel.</span></span> <span data-ttu-id="cda78-120">В случае успеха положение панели устанавливается с помощью CSS и JavaScript (изменение будет положение во всплывающем окне).</span><span class="sxs-lookup"><span data-stu-id="cda78-120">If it succeeds, the panel's position is set using CSS and JavaScript (change the position of the popup at will).</span></span> <span data-ttu-id="cda78-121">Однако `ModalPopupExtender` управления также пытается положение всплывающего окна.</span><span class="sxs-lookup"><span data-stu-id="cda78-121">However the `ModalPopupExtender` control also tries to position the popup.</span></span> <span data-ttu-id="cda78-122">Таким образом код JavaScript многократно всплывающее окно, каждые десять раз меньше секунды.</span><span class="sxs-lookup"><span data-stu-id="cda78-122">Therefore, the JavaScript code repeatedly positions the popup, every tenth of a second.</span></span>

[!code-html[Main](positioning-a-modalpopup-cs/samples/sample3.html)]

<span data-ttu-id="cda78-123">Как видите, возвращаемое значение `setTimeout()` метода JavaScript сохраняется в глобальной переменной.</span><span class="sxs-lookup"><span data-stu-id="cda78-123">As you can see, the return value of the `setTimeout()` JavaScript method is saved in a global variable.</span></span> <span data-ttu-id="cda78-124">Это позволяет остановить повторное размещение всплывающего окна по требованию, с помощью `clearTimeout()` метод:</span><span class="sxs-lookup"><span data-stu-id="cda78-124">This allows to stop the repeated positioning of the popup on demand, using the `clearTimeout()` method:</span></span>

[!code-javascript[Main](positioning-a-modalpopup-cs/samples/sample4.js)]

<span data-ttu-id="cda78-125">Теперь осталось сделать — сделать вызывать эти функции каждый раз, когда соответствующие браузер.</span><span class="sxs-lookup"><span data-stu-id="cda78-125">Now all that is left to do is to make the browser call these functions whenever appropriate.</span></span> <span data-ttu-id="cda78-126">`movePanel()` Функцию JavaScript должен вызываться при нажатии кнопки, которое запускает панели:</span><span class="sxs-lookup"><span data-stu-id="cda78-126">The `movePanel()` JavaScript function must be called when the button is clicked that triggers the panel:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample5.aspx)]

<span data-ttu-id="cda78-127">И `stopMoving()` функции вступает в действие, когда всплывающее окно закрывается, это может быть предприняты в `ModalPopupExtender` управления:</span><span class="sxs-lookup"><span data-stu-id="cda78-127">And the `stopMoving()` function comes into play when the popup is closed this can be triggered in the `ModalPopupExtender` control:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample6.aspx)]


<span data-ttu-id="cda78-128">[![Модальное окно отображается в указанной позиции](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cda78-128">[![The modal popup appears at the designated position](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)</span></span>

<span data-ttu-id="cda78-129">Модальное окно отображается в указанной позиции ([Просмотр полноразмерное изображение](positioning-a-modalpopup-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="cda78-129">The modal popup appears at the designated position ([Click to view full-size image](positioning-a-modalpopup-cs/_static/image3.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="cda78-130">[Назад](handling-postbacks-from-a-modalpopup-cs.md)
[Вперед](launching-a-modal-popup-window-from-server-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="cda78-130">[Previous](handling-postbacks-from-a-modalpopup-cs.md)
[Next](launching-a-modal-popup-window-from-server-code-vb.md)</span></span>