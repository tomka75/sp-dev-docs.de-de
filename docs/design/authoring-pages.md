---
title: Erstellen von Seiten auf einer SharePoint-Website
description: "Erstellen Sie Seiten im Bearbeitungsmodus, im Modus „Veröffentlicht“, und ziehen Sie auch die mobile Ansicht in Betracht."
ms.date: 1/23/2018
ms.openlocfilehash: 048105633e6c2b66e06ef3eca899c19bf19d59c0
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="authoring-pages-in-a-sharepoint-site"></a><span data-ttu-id="8b27c-103">Erstellen von Seiten auf einer SharePoint-Website</span><span class="sxs-lookup"><span data-stu-id="8b27c-103">Authoring pages in a SharePoint site</span></span>

<span data-ttu-id="8b27c-104">Das Erstellen von Seiten in SharePoint ist unkompliziert, erfordert jedoch einige Kenntnisse der SharePoint-Umgebung. Außerdem müssen Sie sich in grundlegenden Zügen bewusst sein, was Sie entwerfen und für wen.</span><span class="sxs-lookup"><span data-stu-id="8b27c-104">Authoring pages in SharePoint is a simple process, but it does require some familiarity with the SharePoint environment, as well as an understanding of what and who you are designing the page for.</span></span> <span data-ttu-id="8b27c-105">Ein paar Grundprinzipien – wie „Einfach beginnen“ und „Auf dem aufsetzen, was funktioniert“ – sind zu Beginn eines Projekts hilfreich.</span><span class="sxs-lookup"><span data-stu-id="8b27c-105">A few basic principles – like remembering to "Start simple" and "Build on what's working" - are valuable things to consider as you start authoring.</span></span> <span data-ttu-id="8b27c-106">Es ist auch sinnvoll, immer Ihre Zielgruppe und die Ziele im Hinterkopf zu behalten, bei deren Umsetzung Sie sie unterstützen möchten.</span><span class="sxs-lookup"><span data-stu-id="8b27c-106">It's also a good idea to consistently remind yourself of your audience, and the goals that you are trying to help them achieve.</span></span>

<!-- Do we have content about the design principles that we can link to here? -->

<span data-ttu-id="8b27c-107">Die Erstellungsumgebung für SharePoint Seiten hat zwei Modi:</span><span class="sxs-lookup"><span data-stu-id="8b27c-107">The SharePoint page authoring experience has two modes:</span></span> 

- <span data-ttu-id="8b27c-108">**Bearbeiten**</span><span class="sxs-lookup"><span data-stu-id="8b27c-108">Edit</span></span> <span data-ttu-id="8b27c-109">In diesem Modus können Seitenautoren Webparts hinzufügen und konfigurieren, um einer Seite Inhalte hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="8b27c-109">Edit - Allows page authors to add and configure web parts to add content to a page.</span></span>
- <span data-ttu-id="8b27c-110">**Veröffentlicht**</span><span class="sxs-lookup"><span data-stu-id="8b27c-110">Published</span></span> <span data-ttu-id="8b27c-111">In diesem Modus kann Ihr Team oder Ihre Zielgruppe die Inhalte sehen und mit Webparts interagieren.</span><span class="sxs-lookup"><span data-stu-id="8b27c-111">Published - Allows your team or audience to view content and interact with web parts.</span></span> 

## <a name="edit-mode"></a><span data-ttu-id="8b27c-112">Bearbeitungsmodus</span><span class="sxs-lookup"><span data-stu-id="8b27c-112">Edit mode</span></span>

<span data-ttu-id="8b27c-113">Beim Erstellen einer neuen Seite haben Benutzer Zugriff auf die Erstellungsbenutzeroberfläche, um Inhalte hinzuzufügen und den Seiteninhalt anzupassen.</span><span class="sxs-lookup"><span data-stu-id="8b27c-113">When creating a new page, users have access to the authoring UI to add content to and customize the page content.</span></span> 

<img alt="Edit control" src="../images/design-authoring-edit-01.png" width="850">

<br/>

<img alt="Edit control with cursor showing highlight" src="../images/design-authoring-edit-02.png" width="850">

<br/>

### <a name="add-hint-and-toolbox"></a><span data-ttu-id="8b27c-114">Hinweis zum Hinzufügen und Toolbox</span><span class="sxs-lookup"><span data-stu-id="8b27c-114">Add hint and Toolbox</span></span>

<span data-ttu-id="8b27c-115">Der Hinweis zum Hinzufügen besteht aus einer horizontalen Linie mit einem Pluszeichen, die angezeigt wird, wenn ein Webpart ausgewählt wird oder wenn auf ein Webpart gezeigt wird. Er markiert, wo Autoren neue Webparts zu ihrer Seite hinzufügen können.</span><span class="sxs-lookup"><span data-stu-id="8b27c-115">The add hint is a horizontal line with a plus icon that is visible when a web part is selected and on hover to indicate where page authors can add new web parts to their page.</span></span> <span data-ttu-id="8b27c-116">Die Toolbox wird geöffnet, wenn ein Benutzer auf das Pluszeichen klickt.</span><span class="sxs-lookup"><span data-stu-id="8b27c-116">The Toolbox opens when a user chooses the plus icon.</span></span> <span data-ttu-id="8b27c-117">Die Toolbox enthält alle Webparts, die einer Seite hinzugefügt werden können.</span><span class="sxs-lookup"><span data-stu-id="8b27c-117">The Toolbox contains all the web parts that can be added to a page.</span></span>

<img alt="Hint and toolbox showing tools" src="../images/design-authoring-add-hint.png" width="850">

<br/>

### <a name="toolbar"></a><span data-ttu-id="8b27c-118">Symbolleiste</span><span class="sxs-lookup"><span data-stu-id="8b27c-118">Toolbar</span></span>

<span data-ttu-id="8b27c-119">Eine vertikale Symbolleiste und ein umgebendes Feld sind Teil des Frameworks für jedes Webpart und werden von der Seite bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="8b27c-119">A vertical toolbar and bounding box is part of the framework for every web part and is provided by the page.</span></span> <span data-ttu-id="8b27c-120">Jedes Webpart stellt in der Symbolleiste eine Bearbeitungs- und eine Löschaktion bereit.</span><span class="sxs-lookup"><span data-stu-id="8b27c-120">Each web part has an edit and delete action in the toolbar.</span></span> 

<img alt="Expanded toolbar" src="../images/design-authoring-toolbar.png" width="850">

<br/>

### <a name="active-and-hover-states"></a><span data-ttu-id="8b27c-121">Aktiver Zustand und Hover-Zustand</span><span class="sxs-lookup"><span data-stu-id="8b27c-121">Active and hover states</span></span>

<span data-ttu-id="8b27c-122">Im Hover-Zustand oder im aktiven Zustand haben die Hinweisleisten als Farbe das primäre Blau oder das primäre Farbdesign für die Website.</span><span class="sxs-lookup"><span data-stu-id="8b27c-122">On hover/active, the hint bars are primary blue or the primary theme color for the site.</span></span>

<img alt="Hover and active state" src="../images/design-authoring-active-hover-01.png" width="850">

<br/>

<span data-ttu-id="8b27c-123">Das umgebende Feld für ein Webpart ist standardmäßig Grau, wird aber in Primärblau oder dem primären Farbdesign der Website angezeigt, wenn der Mauszeiger auf ihm platziert wird oder wenn das Webpart ausgewählt wird.</span><span class="sxs-lookup"><span data-stu-id="8b27c-123">The bounding box for a web part is gray by default, but picks up the primary blue or primary theme color for the site on hover or when the web part is selected.</span></span>

<img alt="Bounding box on and off" src="../images/design-authoring-active-hover-02.png" width="850">

<br/>

### <a name="contextual-edits"></a><span data-ttu-id="8b27c-124">Kontextbezogene Bearbeitungen</span><span class="sxs-lookup"><span data-stu-id="8b27c-124">Contextual edits</span></span>

<span data-ttu-id="8b27c-125">Entwerfen Sie eine WYSIWYG-Umgebung für Webparts, sodass Benutzer Informationen eingeben oder Inhalte hinzufügen können, die beim Veröffentlichen angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="8b27c-125">Design a WYSIWYG experience for web parts so that users can fill in information or add content that will be displayed when published.</span></span> <span data-ttu-id="8b27c-126">Diese Inhalte sollten auf der Seite eingegeben werden, sodass der Benutzer nachvollziehen kann, wie sie im Viewer gerendert werden.</span><span class="sxs-lookup"><span data-stu-id="8b27c-126">This content should be entered on the page so the user understands how the it will render in the viewer.</span></span> <span data-ttu-id="8b27c-127">Titel und Beschreibungen sollten beispielsweise dort eingegeben werden, wo der Text angezeigt werden soll; neue Aufgaben sollten im Kontext der Seite hinzugefügt und geändert werden.</span><span class="sxs-lookup"><span data-stu-id="8b27c-127">For example, titles and descriptions should be filled out where the text displays; new tasks should be added and modified in the context of the page.</span></span>

![Formularelement für kontextbezogeneBearbeitungen](../images/design-authoring-contextual-edits.png)

<br/>

### <a name="item-level-edits"></a><span data-ttu-id="8b27c-129">Bearbeitungen auf Elementebene</span><span class="sxs-lookup"><span data-stu-id="8b27c-129">Item-level edits</span></span>

<span data-ttu-id="8b27c-130">Die Benutzeroberfläche kann sich innerhalb des Webpart ändern. Text wird zum Beispiel in ein Textfeld umgewandelt, oder auf der Benutzeroberfläche werden Elemente neu angeordnet oder Aufgaben als erledigt markiert.</span><span class="sxs-lookup"><span data-stu-id="8b27c-130">UI can change within the web part; for example, text can become a text field, or you can display UI to reorder items or to check off tasks in a web part.</span></span> <span data-ttu-id="8b27c-131">Sie können interaktive Funktionen für Webparts im Bearbeitungsmodus, im Lesemodus oder in beiden Modi aktivieren, je nach Designabsicht.</span><span class="sxs-lookup"><span data-stu-id="8b27c-131">You can enable interactive functionality for web parts in edit mode, in read mode, or in both, depending on your design intent.</span></span>

![Bearbeitung auf Elementebene im ausgewählten Zustand](../images/design-authoring-item-level.png)

<br/>

### <a name="property-panes"></a><span data-ttu-id="8b27c-133">Eigenschaftenbereiche</span><span class="sxs-lookup"><span data-stu-id="8b27c-133">Property panes</span></span>

<span data-ttu-id="8b27c-134">Eigenschaftenbereiche werden über das **Bearbeiten**-Symbol auf der Symbolleiste aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="8b27c-134">Property panes are invoked via the **Edit** icon on the toolbar.</span></span> <span data-ttu-id="8b27c-135">Eigenschaftenbereiche sollten in erster Linie Konfigurationseinstellungen zur Aktivierung oder Deaktivierung von Features enthalten, die entweder auf der Seite angezeigt werden oder Inhalte über den Aufruf eines Diensts rendern.</span><span class="sxs-lookup"><span data-stu-id="8b27c-135">Property panes should primarily contain configuration settings that enable or disable features that either show on page, or make a call to a service to display content.</span></span> 

![Erweiterter Bereich](../images/design-authoring-panes.png)

<br/>

## <a name="published-mode"></a><span data-ttu-id="8b27c-137">Modus „Veröffentlicht“</span><span class="sxs-lookup"><span data-stu-id="8b27c-137">Published mode</span></span>

<span data-ttu-id="8b27c-138">Sobald die Seite veröffentlicht wurde, wird die gesamte Bearbeitungsoberfläche für den Betrachter oder Leser der Seite deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="8b27c-138">After the page is published, all edit UI is disabled and for the viewer or reader of the page.</span></span> <span data-ttu-id="8b27c-139">Will der Benutzer die Seite weiter bearbeiten, muss er oben rechts auf der Befehlsleiste auf die Schaltfläche **Bearbeiten** klicken.</span><span class="sxs-lookup"><span data-stu-id="8b27c-139">To continue editing the page, the user selects the **Edit** button on the top right corner of the command bar.</span></span>

![Schaltfläche „Veröffentlichen“ hervorgehoben](../images/design-authoring-published.png)

<br/>

## <a name="mobile-view"></a><span data-ttu-id="8b27c-141">Mobile Ansicht</span><span class="sxs-lookup"><span data-stu-id="8b27c-141">Mobile view</span></span>

<span data-ttu-id="8b27c-142">Alle SharePoint-Seiten sind [dynamisch](grid-and-responsive-design.md), damit die Seiteninhalte auf mobilen Geräten optimal dargestellt werden.</span><span class="sxs-lookup"><span data-stu-id="8b27c-142">All SharePoint pages are [responsive](grid-and-responsive-design.md) to allow the content of the page to be viewed on mobile devices.</span></span> <span data-ttu-id="8b27c-143">Beim Entwerfen eines Webparts müssen Sie immer vor Augen haben, wie die neuen Seiten Ihrer SharePoint-Website auf unterschiedlichen Geräten gerendert werden.</span><span class="sxs-lookup"><span data-stu-id="8b27c-143">While designing a web part, it is important to understand how the new SharePoint site pages render across different devices.</span></span>

![Website auf einem Mobilgerät](../images/design-authoring-mobile.png)

## <a name="see-also"></a><span data-ttu-id="8b27c-145">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="8b27c-145">See also</span></span>

- [<span data-ttu-id="8b27c-146">Entwerfen von benutzerfreundlichen SharePoint-Umgebungen</span><span class="sxs-lookup"><span data-stu-id="8b27c-146">Designing great SharePoint experiences</span></span>](design-guidance-overview.md)