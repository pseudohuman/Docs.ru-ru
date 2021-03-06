---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: "Практическое лабораторное занятие: Visual Studio 2013 веб-инструменты | Документы Microsoft"
author: rick-anderson
description: "Visual Studio — это среда разработки отлично для. NET под управлением Windows и веб-проектов. Он включает в себя мощный текстовый редактор, можно легко использовать для..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/16/2014
ms.topic: article
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: ef8ab82f9043ef9da3a3e6a146a97f083149534d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="hands-on-lab-visual-studio-2013-web-tools"></a>Практическое лабораторное занятие: Visual Studio 2013 веб-инструменты
====================
по [Web лагеря команды](https://twitter.com/webcamps)

[Загрузите комплект учебных материалов лагеря Web](http://aka.ms/webcamps-training-kit)

> Visual Studio — это среда разработки отлично для. NET под управлением Windows и веб-проектов. Он включает в себя мощный текстовый редактор, легко могут использоваться для изменения отдельных файлов без проекта.
> 
> Visual Studio поддерживает дерево синтаксического анализа полнофункциональный в процессе изменения каждого файла. Это позволяет Visual Studio для обеспечения несравненную автозавершение и действия на основе документа при проведении намного быстрее и более удобную процесс разработки. Эти функции особенно выражены в документах HTML и CSS.
> 
> Все эти возможности для расширений, что упрощает расширить редакторы с мощные новые возможности в соответствии с потребностями. Web Essentials — это коллекция (обычно) веб технологиям расширений Visual Studio. Он содержит большое количество новых вариантов завершения IntelliSense (особенно для CSS), новые возможности связи с браузером, автоматический файлы JSHint для JavaScript, новые предупреждения для HTML, CSS и множество других возможностей, которые необходимы для современных веб-разработки.
> 
> Все образцы кода и фрагменты кода включаются в Web лагеря комплект учебных материалов, доступных в [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit).


<a id="Overview"></a>
## <a name="overview"></a>Обзор

<a id="Objectives"></a>
### <a name="objectives"></a>Цели

В этой практической вы узнаете, как:

- Используйте новые возможности редактора HTML, включенных в Web Essentials например форматированного фрагменты кода HTML5 и Zen кодирования
- Используйте новые возможности редактора CSS, включенных в Web Essentials как палитра цветов и подсказка матрицы браузера
- Используйте новые возможности редактора JavaScript, включенных в Essentials Web, таких как извлечение в файле и технологии IntelliSense для всех элементов HTML
- Обмен данными между браузером и Visual Studio, используя связь с браузером

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Предварительные требования

Для завершения этой практической требуется следующее:

- [Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) или выше
- [Web Essentials 2013](http://vswebessentials.com/)
- [Google Chrome](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a>Установка

Чтобы выполнить упражнения в этой практической, необходимо настроить среду.

1. Откройте окно проводника Windows и перейдите в лаборатории **источника** папки.
2. Щелкните правой кнопкой мыши **Setup.cmd** и выберите **Запуск от имени администратора** для запуска процесса установки, будет настроить среду и установить фрагменты кода Visual Studio для этой лабораторной работы.
3. Если отображается диалоговое окно контроля учетных записей, подтвердите действие для продолжения.

> [!NOTE]
> Убедитесь, что все зависимости для этой лабораторной работы вы вернули перед запуском программы установки.


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>Фрагменты кода

В документе лаборатории будет предложено вставлять блоки кода. Visual Studio к фрагментам кода, к которому можно получить из в Visual Studio 2013, чтобы избежать необходимости вручную добавить большая часть кода предоставляется для удобства.

> [!NOTE]
> Каждого упражнения сопровождается начальный решений, расположенный в **начать** папку расчетов, позволяющий выполнить каждого упражнения независимо от других. Имейте в виду, что фрагменты кода, которые добавляются во время упражнения, отсутствуют на их запуск решения и могут не работать до завершения этого упражнения. В исходном коде для упражнения, вы также найдете **окончания** папку, содержащую решение Visual Studio с кодом, полученный в результате выполнения действий в соответствующий упражнении. Эти решения можно использовать как рекомендации, если вам нужна дополнительная помощь, отвечая на этой практической.


* * *

<a id="Exercises"></a>
## <a name="exercises"></a>Упражнения

Данная практическая работа включает следующие упражнения:

1. [Работа с связь с браузером и веб-Essentials](#Exercise1)
2. [Чтобы преимущества фрагменты кода IntelliSense](#Exercise2)

> [!NOTE]
> При первом запуске Visual Studio, необходимо выбрать одну из коллекций предварительно определенных параметров. Каждая предопределенная коллекция соответствует конкретному стилю разработки и определяет макетов окон, поведение редактора, фрагменты кода IntelliSense и параметры диалогового окна. В этой лаборатории описаны действия, необходимые для выполнения данной задачи в Visual Studio при использовании **обычные параметры разработки** коллекции. При выборе другого набора параметров для среды разработки может быть отличия в этапах, которые следует принимать во внимание.


<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a>Упражнение 1: Работа с связь с браузером и веб-Essentials

**Веб-Essentials** представляет собой расширение Visual Studio, которое добавляет ряд полезных возможностей для современных веб-разработки, главным образом уделено облегчению разработки веб-интерфейс намного быстрее и более удобную. Можно установить Web Essentials из галереи расширений в Visual Studio.

**Связь с браузером** — это новая функция, включенных в Visual Studio 2013, который обеспечивает канал между Visual Studio IDE и любой откройте браузер для обмена данными между веб-приложения и Visual Studio. Web Essentials расширяет связь с браузером с помощью средств для управления объектной модели DOM и стили CSS веб-страниц непосредственно из браузера.

В этом упражнении будут рассматриваться некоторые возможности, поддерживаемые **Web Essentials** и **связь с браузером** для повышения уровня страницы простой тест.

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a>Задача 1. запуск проекта в нескольких браузерах

В этой задаче вы настроите веб-приложения для запуска в нескольких браузерах одновременно, что полезно для тестирования в различных браузерах.

1. Откройте **Microsoft Visual Studio**.
2. В **файл** последовательно выберите пункты **откройте | Решение или проект...**  и перейдите к папке **сервера Ex1 WorkingwithBrowserLinkandWebEssentials\Begin** в **источника** папку лаборатории (C:\WebCampsTK\HOL\VSWebTooling\Source). Выберите **Begin.sln** и нажмите кнопку **откройте**.
3. На панели инструментов Visual Studio разверните меню браузера и выберите **просмотр с помощью...** .

    ![Просмотр с помощью пункта меню](visual-studio-2013-web-tools/_static/image1.png "Обзор с меню браузера")

    *Просмотр с помощью пункта меню*
4. В **просмотр с помощью** диалоговое окно, выберите **Google Chrome** и **Internet Explorer** , удерживая нажатой **CTRL** раздел и нажмите кнопку  **По умолчанию**.

    ![Обзор с диалоговым окном](visual-studio-2013-web-tools/_static/image2.png "Обзор с диалоговым окном")

    *При выборе нескольких браузера по умолчанию*
5. Google Chrome и Internet Explorer должен появиться в качестве браузера по умолчанию. Нажмите кнопку **отменить** чтобы закрыть диалоговое окно.

    ![Google Chrome и Internet Explorer в качестве браузера по умолчанию](visual-studio-2013-web-tools/_static/image3.png "браузера Google Chrome и Internet Explorer по умолчанию")

    *Google Chrome и Internet Explorer в качестве браузера по умолчанию*

    > [!NOTE]
    > После настройки браузера по умолчанию, **нескольких браузеров** выбран в меню обозревателя.
    > 
    > ![Нескольких браузеров](visual-studio-2013-web-tools/_static/image4.png "нескольких браузеров")
6. Нажмите клавишу **CTRL** + **F5** для запуска приложения без отладки.
7. При открытии оба окна браузера, установите один из них над другим для просмотра обновлений на обоих браузерах одновременно. Веб-страницы с голубой прямоугольник должен отображаться в браузерах.

    ![Размещение браузера, один над другим](visual-studio-2013-web-tools/_static/image5.png "размещение браузера, один над другим")

    *Размещение браузера, один над другим*
8. Не закрывайте браузеры. В следующей задаче будет использовать их.

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a>Задача 2 - с помощью Zen кода, для создания HTML-элементов

**Кодирование Zen** является редактором кода подключаемого модуля для высокоскоростной HTML, XML, XSL (или любой другой формат структурированный код) и редактирования. Этот подключаемый модуль лежит сокращение мощный механизм, который позволяет расширить - аналогично селекторов CSS - выражения в HTML-код. Кодирование Zen является быстрый способ записи стиля HTML, CSS с помощью синтаксиса селектора.

В этом упражнении будет использовать функцию Zen кодирования, предоставляемые Web Essentials для создания кнопки HTML, которые представляют параметры вопроса.

1. Переключитесь в Visual Studio.
2. Откройте **Index.cshtml** файл, расположенный в **представления** | **Главная** папки.
3. Замените  **&lt;!--TODO: Добавьте здесь--параметры&gt;**  комментарий с ниже код и нажмите клавишу **ВКЛАДКА**.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. Код, развернута в формате HTML.

    ![Развернуть HTML](visual-studio-2013-web-tools/_static/image6.png "развернут HTML")

    *Расширенная HTML*

    > [!NOTE]
    > Дополнительные сведения о синтаксисе Zen кодирования см. в следующих [статьи](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/).
5. Нажмите кнопку **обновить связанные браузеры** кнопку для обновления обоих браузерах.

    ![Обновить связанные браузеры](visual-studio-2013-web-tools/_static/image7.png "обновить связанные браузеры")

    *Обновить связанные браузеры*

    ![Internet Explorer — страница обновлена с четырьмя кнопками](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer — страница обновлена с четырьмя кнопками")

    *Internet Explorer — страница обновлена с четырьмя кнопками*

    ![Google Chrome - страница обновлена с четырьмя кнопками](visual-studio-2013-web-tools/_static/image9.png "Google Chrome - страница обновлена с четырьмя кнопками")

    *Google Chrome - страница обновлена с четырьмя кнопками*
6. Переключитесь в Visual Studio.
7. Вы добавили кнопки на страницу, но по-прежнему необходимо добавить вопрос шаблона. Чтобы сделать это, будут использовать новую функцию в вызове Essentials Web **генератор Lorem Ipsum**. Найдите **div** элемент с **класса** атрибута **передней**.
8. Добавьте следующий код в качестве первого дочернего элемента **div**и нажмите клавишу **ВКЛАДКА**.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. Код, развернута в формате HTML.

    ![Автоматически созданные lorem Ipsum](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum автоматически")

    *Автоматически созданные lorem Ipsum*

    > [!NOTE]
    > В рамках Zen программирования можно приступить к созданию кода Lorem Ipsum непосредственно в редакторе HTML. Просто введите **lorem** и нажмите кнопку **ВКЛАДКА** и 30 word Lorem Ipsum будет вставлен текст. Например *lorem10* вставляет 10 Lorem Ipsum слова.
10. Добавим эмблему в верхней части вопрос с помощью другой новой функцией в вызове Essentials Web **пикселей Lorem генератор**. Добавьте следующий код в качестве первого дочернего элемента **div** элемент с **контейнера** как **класса** и нажмите клавишу **ВКЛАДКА**.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. Код должен развернуть в формате HTML.

    ![Автоматически созданные lorem пикселей](visual-studio-2013-web-tools/_static/image11.png "автоматически Lorem пикселей")

    *Автоматически созданные lorem пикселей*

    > [!NOTE]
    > Как часть Zen кодирования также можно создать непосредственно в редакторе HTML-кода Lorem пикселей. Просто введите **pix-200 x 200-животных** и нажмите кнопку **ВКЛАДКЕ** и **img** тег с изображением 200 x 200 animal будут вставлены. Дополнительные сведения см. в [пикселей Lorem](http://www.lorempixel.com).
12. Нажмите кнопку **обновить связанные браузеры** кнопку для обновления обоих браузерах.

    ![Internet Explorer — автоматически изображение и текст](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer — автоматически изображения и текста")

    *Internet Explorer — автоматически изображения и текста*

    ![Google Chrome - текста и изображений автоматически](visual-studio-2013-web-tools/_static/image13.png "Google Chrome - автоматически изображения и текста")

    *Google Chrome - автоматически изображения и текста*

    > [!NOTE]
    > Изображение выбирается случайным образом при добавлении фрагмента кода, изображения, отображаемого в качестве браузера может отличаться.
13. Не закрывайте браузеры. В следующей задаче будет использовать их.

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a>Задача 3. обновление свойства стиля

В этой задаче будет использовать связь с браузером **проверить режим** возможность определить точное расположение, где формируется конкретный элемент DOM, а затем обновите свойство цвета палитры цветов, предоставляемые веб-элемента Essentials.

1. В обозревателе Internet Explorer, нажмите клавишу **CTRL** + **ALT** + **я** для перехода в режим проверки.
2. Наведите указатель на синий Светлая и нажмите кнопку.

    ![При перемещении указателя над синего Светлая](visual-studio-2013-web-tools/_static/image14.png "при перемещении указателя над светлой синяя рамка")

    *При перемещении указателя над светлой синяя рамка*
3. Переключитесь в Visual Studio. Обратите внимание на то, как HTML-элемента, выбранного в браузере, также выбирается в редактор Visual Studio HTML.

    ![HTML-элемента, выделенного в редакторе Visual Studio HTML](visual-studio-2013-web-tools/_static/image15.png "HTML-элемента, выделенного в редакторе Visual Studio HTML")

    *HTML-элемента, выделенного в редакторе Visual Studio HTML*
4. Теперь вы обновляете **передней** класса CSS, чтобы изменить стиль выбранного элемента. Чтобы сделать это, нажмите клавишу **CTRL** + **,** Открытие **перейти к** поле поиска. Тип **site.css** и нажмите клавишу **ввод** для открытия файла.

    ![Открытие файла Site.css](visual-studio-2013-web-tools/_static/image16.png "Site.css при открытии файла")

    *При открытии файла Site.css*
5. Нажмите клавишу **CTRL** + **F** и тип **.front .flip контейнере** найти селектора CSS.
6. Щелкните светло синий квадрат в свойстве класса, чтобы открыть средство выбора цвета границы.

    ![Открытие палитры цветов](visual-studio-2013-web-tools/_static/image17.png "Открытие палитры цветов")

    *Открытие палитры цветов*
7. Разверните палитру цветов, нажав кнопку шеврона и выберите новый цвет.

    ![Развернув палитра](visual-studio-2013-web-tools/_static/image18.png "расширение палитра цветов")

    *Развернув палитра цветов*
8. Нажмите клавишу **CTRL** + **ALT** + **ввод** для обновления связанных браузеры.
9. Перейдите в Internet Explorer и обратите внимание на то, как изменилась цвет границы.

    ![Internet Explorer — обновить цвет границы](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer — обновить цвет границы")

    *Internet Explorer — обновить цвет границы*
10. Переключитесь в Google Chrome и обратите внимание на то, как изменилась цвет границы.

    ![Google Chrome - цвет границы обновлены](visual-studio-2013-web-tools/_static/image20.png "Google Chrome - обновить цвет границы")

    *Google Chrome - обновить цвет границы*
11. Переключитесь в Visual Studio.
12. Перейдите в конец **Site.css** файл и нажмите кнопку **CTRL** + **F** искомый **.btn** селектора.
13. Обратите внимание, что **- webkit-border-radius** свойство подчеркивается зеленым цветом.

    ![Свойство - webkit-border-radius селектора btn](visual-studio-2013-web-tools/_static/image21.png "- webkit-border-radius свойство btn селектора")

    *Свойство - webkit-border-radius btn селектора*
14. Поместите курсор в **- webkit-border-radius** свойство. В первую букву в первом слове свойства должен появиться синей линией. Это **смарт-тег**.
15. Нажмите клавишу **CTRL** + **.** Чтобы открыть меню предложения и нажмите кнопку **добавить стандартное свойство (границы radius) отсутствует**.

    ![Добавить отсутствует предложение стандартное свойство](visual-studio-2013-web-tools/_static/image22.png "добавить отсутствует предложение стандартное свойство")

    *Добавление недостающих стандартное свойство предложений*
16. **Границы radius** свойство автоматически добавляется в правило CSS.

    ![Отсутствует стандартное свойство добавлено](visual-studio-2013-web-tools/_static/image23.png "отсутствует стандартное свойство добавлено")

    *Отсутствует стандартное свойство добавлено*
17. Наведите указатель на **границы radius** свойство для отображения **подсказка матрицы браузера**. **Подсказка матрицы браузера** представлены сведения о доступности свойства каждого браузера.

    ![Подсказка матрицы браузера](visual-studio-2013-web-tools/_static/image24.png "подсказка матрицы браузера")

    *Подсказка матрицы браузера*
18. Обратите внимание, что значение **границы radius** свойство по-прежнему подчеркнутым. Наведите указатель на значение, чтобы показать предупреждающее сообщение.

    ![Предупреждение значение свойства границы radius](visual-studio-2013-web-tools/_static/image25.png "предупреждение значение свойства Border-radius")

    *Предупреждение значение свойства границы radius*
19. Удалить устройство из **границы radius** значение свойства, как говорится в подсказке.
20. Как **границы radius** является стандартное свойство для определения способа скругленными углами, находятся в углах, можно удалить **- webkit-border-radius** свойства и значения из правила CSS.
21. Поместите курсор в **словам** свойство и обратите внимание, что ниже также отображается смарт-тег.
22. Откройте меню и нажмите кнопку **добавить отсутствующие особенности поставщика**.

    ![Добавить предложение особенности отсутствует поставщик](visual-studio-2013-web-tools/_static/image26.png "добавьте отсутствует предложение особенности поставщика")

    *Добавить отсутствующие предложений особенности поставщика*
23. **-Ms-словам** свойство автоматически добавляется в правило CSS.

    ![Свойство поставщика добавлен](visual-studio-2013-web-tools/_static/image27.png "свойство поставщика добавлен")

    *Свойство поставщика добавлен*

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a>Задача 4 - обновление кода HTML из браузера

В этой задаче будет использовать связь с браузером **режим конструктора** возможность редактирования объекта DOM из браузера и передают эти изменения к файлу исходного кода HTML в Visual Studio.

1. В браузере Google Chrome, нажмите клавишу **CTRL** + **ALT** + **D** для перехода в режим конструктора.
2. Наведите указатель на **Lorem Ipsum dolor sit amet** метки и нажмите кнопку.

    ![Изменение вопроса](visual-studio-2013-web-tools/_static/image28.png "редактирование на вопрос:")

    *Изменение вопроса*
3. Курсор должен появиться. Замените исходный текст с *как она выглядит при рукописном дольше вопрос?*и нажмите клавишу **ESC** для выхода из режима конструктора.

    ![Изменить вопрос](visual-studio-2013-web-tools/_static/image29.png "изменить вопрос")

    *Изменить вопрос*
4. Ключ, вернитесь в Visual Studio и откройте **Index.cshtml**, если еще не открыт. Обратите внимание, что внутренний текст  **&lt;p&gt;**  элемент был обновлен.

    ![Вопрос Updated в HTML-страницу](visual-studio-2013-web-tools/_static/image30.png "вопрос Updated в HTML-страницы")

    *Обновленные вопрос в HTML-страницы*

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a>Задача 5 - рецензирования SEO связанные предупреждения

**Поиск оптимизации поисковой системы** (SEO) представляет собой процесс внесения высокий ранг веб-сайт в список результатов поисковой системы. Чем выше ранжирует сайта и непрерывную содержится в списке, дополнительные посетители сайта будут получены из этого поисковой системы. Web Essentials включает аналитические средства, рассмотрение HTML, отчеты о проблемах найден и приведены рекомендации по их устранению.

1. Последовательно выберите пункты **представление** меню и выберите пункт **список ошибок** Открытие **список ошибок** окна.

    ![Ошибка в представлении списка меню](visual-studio-2013-web-tools/_static/image31.png "список ошибок, в меню "Вид"")

    *Ошибка в представлении списка меню*
2. Обратите внимание, что предупреждение об оптимизации поисковой системы, связанные с уведомлением,  **&lt;meta&gt;**  тегов для описания страницы отсутствует. Дважды щелкните запись предупреждение SEO по ее устранению.

    ![Окно списка ошибок](visual-studio-2013-web-tools/_static/image32.png "окно списка ошибок")

    *Окно списка ошибок*
3. В **Web Essentials** диалоговое окно, нажмите кнопку **Да** для вставки описание &lt;meta&gt; тег.

    ![Веб-диалоговое окно Essentials](visual-studio-2013-web-tools/_static/image33.png "Essentials веб-диалоговое окно")

    *Essentials веб-диалоговое окно*
4. Редактор для  **\_Layout.cshtml** открывает и  **&lt;meta&gt;**  тег добавляется автоматически **head** раздела HTML-файл.

    ![Метатег, автоматически добавляются на странице _Layout](visual-studio-2013-web-tools/_static/image34.png "метатег автоматически добавляется в _Layout страницы")

    *Метатег, автоматически добавляется в \_макета страницы*
5. Измените значение **содержимого** атрибут *GeekQuiz* и сохраните файл.

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a>Упражнение 2: Чтобы преимущества фрагменты кода IntelliSense

Редактор HTML с Essentials веб был расширен с дополнительные функциональные возможности. В этом упражнении вы увидите некоторые новые возможности, которые могут быть полезны при разработке веб-приложений.

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a>Задача 1. Использование IntelliSense в HTML-документы

Первый новый компонент, вы увидите в этой задаче называется **динамического IntelliSense**. Динамические IntelliSense считывает другие теги и атрибуты для определения возможных идентификаторов, который будет использоваться.

В этой задаче вы создадите новый элемент формы HTML, который содержит метку и поле ввода. Затем вы добавите **для** атрибут метки, чтобы привязать его к входным данным, и вы увидите предложений IntelliSense, основанных на идентификаторов потоков входа, в области видимости.

1. Откройте **Visual Studio Express 2013 для Web** и **Begin.sln** решение находится в **источника/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/начало** папки. Кроме того можно продолжить с решением, полученный в предыдущем упражнении.
2. В **обозревателе решений**откройте **Index.cshtml** файл, расположенный в **представления** | **Главная** папки.
3. Добавьте следующую форму внутри  **&lt;раздел&gt;**  элемента.

    (Фрагмент - кода *VisualStudio2013WebTooling* - *Ex2* - *формы*)

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. Метка с некоторыми описание поля должно предшествовать тега input. Добавьте следующую метку перед тега input.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. **Для** атрибут  **&lt;метка&gt;**  указывает, какой элемент формы a метки связан. Значение атрибута должно быть равно идентификатор связанного элемента. Добавить **для** атрибут  **&lt;метка&gt;**  элемента. Как показано на следующем рисунке &quot;имя&quot; значение будет отображена в окне IntelliSense на основе идентификатора элементов в той же области (включающий  **&lt;формы&gt;**).

    ![Отображение идентификатора в IntelliSense](visual-studio-2013-web-tools/_static/image35.png "отображается идентификатор в IntelliSense")

    *Отображение идентификатора в IntelliSense*
6. Удаление недавно добавленных  **&lt;формы&gt;**  элемента и его содержимого.

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a>Задача 2 — с помощью фрагментов кода HTML

HTML5 появился более 25 новых семантических тегов. Visual Studio уже имеет поддержку IntelliSense для этих тегов, но Visual Studio 2013 делает его более быстрым и удобным для написания разметки путем добавления новых фрагментов кода. Хотя эти теги не являются сложными, они поставляются с несколько небольших тонкостей, таких как добавление соответствующий кодек резервные варианты для *аудио* тег. В этой задаче вы увидите фрагменты кода HTML для аудио тега.

1. В **Index.cshtml** введите  **&lt;aud** внутри  **&lt;раздел&gt;**  элемента, как показано на следующем рисунке.

    ![Вставка аудио элементов](visual-studio-2013-web-tools/_static/image36.png "Вставка аудио элементов")

    *Вставка аудио элементов*
2. Нажмите клавишу **ВКЛАДКЕ** дважды и обратите внимание на то, каким образом добавлен следующий код на странице, и курсор помещается в **src** атрибут первого источника.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > Нажав **ВКЛАДКЕ** ключа дважды вставки фрагмента кода. Аудио демонстрирует стандартного использования *аудио* тег с двух файлов исходного кода для лучшей поддержкой.
3. Удалите вторую строку и обновление источника первой строки с помощью следующую ссылку, чтобы показать WebCampsTV Katana: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3). Ниже приведен конечный код.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > Исходный файл *KatanaProject.mp3* используется в качестве примера. При желании можно воспользоваться другим источником.
4. Нажмите клавишу **CTRL** + **S** для сохранения файла.
5. Нажмите клавишу **CTRL** + **F5** для запуска приложения.
6. Обратите внимание, что проигрыватель был добавлен в приложение.

    ![Проигрыватель в Internet Explorer](visual-studio-2013-web-tools/_static/image37.png "аудио проигрывателя в Internet Explorer")

    *Проигрыватель в Internet Explorer*

    ![Проигрыватель в Google Chrome](visual-studio-2013-web-tools/_static/image38.png "аудио проигрывателя в Google Chrome")

    *Проигрыватель в Google Chrome*
7. Не закрывайте браузеры. В следующей задаче будет использовать их.

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a>Задача 3. Использование IntelliSense в документах JavaScript

Web 2013 Essentials HTML-страницы и таблицы стилей создают список имена классов и идентификаторы. В этой задаче вы узнаете, как эти списки улучшить поддержку IntelliSense для JavaScript в Web Essentials 2013.

1. В **Index.cshtml** файл, добавьте следующий код для определения **сценарий** тег для кода JavaScript.

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. Добавьте следующий код внутри **сценарий** тег для определения готовности обратного вызова функции.

    (Фрагмент - кода *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. Поместите курсор в **сценарий** тег и нажмите клавишу **CTRL** + **.** Чтобы открыть меню подсказки.
4. Нажмите кнопку **извлечь файл**.

    ![Извлечение JavaScript в файл предложение](visual-studio-2013-web-tools/_static/image39.png "извлечь JavaScript в файл предложений")

    *Извлечение JavaScript в файл предложений*
5. В **Сохранить как** выберите **сценариев** папки, имя файла **init.js** и нажмите кнопку **Сохранить**.

    ![Сохранить как окно](visual-studio-2013-web-tools/_static/image40.png "окно Сохранить как")

    *Окно Сохранить как*

    > [!NOTE]
    > **Init.js** создается файл и файл перемещается содержимое сценария.
    > 
    > ![Init.js файла, созданного на множестве](visual-studio-2013-web-tools/_static/image41.png "Init.js файла, созданного содержимого пакета")
    > 
    > *Init.js файла, созданного содержимого пакета*
6. Откройте **Index.cshtml** файл и проверьте, что тег сценария был заменен со ссылкой на **init.js** файла.

    ![Справочник по html init.js](visual-studio-2013-web-tools/_static/image42.png "Init.js ссылки html")

    *Справочник по html init.js*
7. Последовательно выберите пункты **обозревателе решений** и обратите внимание, что **init.js** файл был автоматически включен в решение.

    ![Файл init.js, включенных в решение](visual-studio-2013-web-tools/_static/image43.png "Init.js файлов, включенных в решение")

    *Файл init.js, включенных в решение*
8. Вернитесь в **init.js** файл, чтобы обновить **готовности** функции обратного вызова.
9. В определении функции обратного вызова, передаваемого *готовности*, добавьте следующий код, чтобы получить все элементы с помощью определенного класса атрибутов.

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. Нажмите клавишу **CTRL** + **пространства** между кавычки внутри **getElementsByClassName** вызов функции.

    ![Отображение IntelliSense для функции getElementsByClassName](visual-studio-2013-web-tools/_static/image44.png "отображение IntelliSense для функции getElementsByClassName")

    *Отображение IntelliSense для функции getElementsByClassName*

    > [!NOTE]
    > Обратите внимание, что IntelliSense отображает классы, определенные в таблицах стилей проекта.
11. Замените строку, созданного с помощью следующего кода.

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. Поместите курсор после **Австралия** в кавычках в **getElementsByTagName** функцию и нажмите клавишу **CTRL** + **пространства**.

    ![Отображение IntelliSense для метода getElementByTagName](visual-studio-2013-web-tools/_static/image45.png "отображение IntelliSense для метода getElementByTagName")

    *Отображение IntelliSense для метод getElementsByTagName*
13. Выберите  **&quot;аудио&quot;**  из списка и нажмите клавишу **ввод**. Результат показан на примере ниже.

    ![Извлечение элементов, аудио](visual-studio-2013-web-tools/_static/image46.png "извлечение элементов, аудио")

    *Извлечение элементов, аудио*
14. В **обозревателе решений**, щелкните правой кнопкой мыши **init.js** файла в **сценариев** папку и выберите **файлов JavaScript уменьшения** из **Web Essentials** меню.

    ![Уменьшения файлов JavaScript](visual-studio-2013-web-tools/_static/image47.png "файлы JavaScript уменьшения")

    *Уменьшения файлов JavaScript*
15. Когда появится запрос на включение автоматического минификации при изменении исходного файла, нажмите кнопку **Да**.

    ![Включение автоматического минификации предупреждение](visual-studio-2013-web-tools/_static/image48.png "Включение автоматического минификации предупреждение")

    *Включение автоматического минификации предупреждение*

    > [!NOTE]
    > **Init.min.js** создается и добавляется в качестве одной из зависимостей **init.js** файла.
    > 
    > ![Создан файл init.min.js](visual-studio-2013-web-tools/_static/image49.png "Init.min.js файл, созданный")
    > 
    > *Создан файл init.min.js*
16. Откройте **init.min.js** файла и обратите внимание, что файл будет уменьшено.

    ![Содержимое файла init.min.js](visual-studio-2013-web-tools/_static/image50.png "Init.min.js содержимого файла")

    *Содержимое файла init.min.js*
17. В **init.js** файл, добавьте следующий код ниже **getElementsByTagName** вызов для воспроизведения звука элементы функции.

    (Фрагмент - кода *VisualStudio2013WebTooling* - *Ex2* - *PlayAudioElements*)

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. Нажмите кнопку **CTRL** + **S** для сохранения файла. Поскольку уменьшенный файл уже открыт, появится диалоговое окно, о том, что файл был изменен вне редактора исходного. Нажмите кнопку **Да**.

    ![Microsoft Visual Studio предупреждение](visual-studio-2013-web-tools/_static/image51.png "предупреждение Microsoft Visual Studio")

    *Предупреждение Microsoft Visual Studio*
19. Вернитесь в **init.min.js** файл, чтобы убедиться, что файл был обновлен с учетом нового кода.

    ![Обновить файл init.min.js](visual-studio-2013-web-tools/_static/image52.png "Init.min.js файл обновлен")

    *Файл init.min.js обновлен*
20. Нажмите кнопку **обновления ссылку в браузере** кнопки.
21. После обновления обоих браузерах аудио проигрыватели, показанного в предыдущей задаче воспроизведение начнется автоматически.

    ![Проигрыватель, включенных в представлении](visual-studio-2013-web-tools/_static/image53.png "аудио проигрывателя, включенных в представлении")

    *Проигрыватель, включенных в представлении*

* * *

<a id="Summary"></a>
## <a name="summary"></a>Сводка

Выполнив этой практической вы узнали, как:

- Используйте новые возможности редактора HTML, включенных в Web Essentials например форматированного фрагменты кода HTML5 и Zen кодирования
- Используйте новые возможности редактора CSS, включенных в Web Essentials как палитра цветов и подсказка матрицы браузера
- Используйте новые возможности редактора JavaScript, включенных в Essentials Web, таких как извлечение в файле и технологии IntelliSense для всех элементов HTML
- Обмен данными между браузером и Visual Studio, используя связь с браузером
