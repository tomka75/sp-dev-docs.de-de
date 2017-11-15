---
title: Erstellen von Seiten auf einer SharePoint-Website
ms.date: 9/25/2017
ms.openlocfilehash: 349de6ef579d2313ddaa27a178cab9c31654e223
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="authoring-pages-in-a-sharepoint-site"></a><span data-ttu-id="5e08a-102">Erstellen von Seiten auf einer SharePoint-Website</span><span class="sxs-lookup"><span data-stu-id="5e08a-102">Authoring pages in a SharePoint site</span></span>

<span data-ttu-id="5e08a-103">Das Erstellen von Seiten in SharePoint ist ein einfacher Vorgang, aber es erfordert einige Kenntnisse der SharePoint-Umgebung sowie ein grundlegendes Verständnis davon, was und für wen Sie die Seite entwerfen.</span><span class="sxs-lookup"><span data-stu-id="5e08a-103">Authoring pages in SharePoint is a simple process, but it does require some familiarity with the SharePoint environment, as well as an understanding of what and who you are designing the page for.</span></span> <span data-ttu-id="5e08a-104">Ein paar Grundprinzipien – wie „Einfach beginnen“ und „Auf dem aufsetzen, was funktioniert“ – sind zu Beginn der Erstellung hilfreich.</span><span class="sxs-lookup"><span data-stu-id="5e08a-104">A few basic principles – like remembering to "Start simple" and "Build on what's working" - are valuable things to consider as you start authoring.</span></span> <span data-ttu-id="5e08a-105">Es ist auch sinnvoll, ständig Ihre Zielgruppe und die Ziele im Hinterkopf zu behalten, bei denen Sie sie unterstützen möchten.</span><span class="sxs-lookup"><span data-stu-id="5e08a-105">It's also a good idea to consistently remind yourself of your audience, and the goals that you are trying to help them achieve.</span></span>

<!-- Do we have content about the design principles that we can link to here? -->

<span data-ttu-id="5e08a-106">Die Erstellungsumgebung für SharePoint- Seiten weist zwei Modi auf:</span><span class="sxs-lookup"><span data-stu-id="5e08a-106">The new SharePoint page authoring experience has two modes:</span></span> 

- <span data-ttu-id="5e08a-107">Bearbeitungsmodus: In diesem Modus können Seitenautoren Webparts hinzufügen und konfigurieren, um einer Seite Inhalte hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="5e08a-107">Edit mode which allows page author(s) to add and configure web parts to add content to a page.</span></span>
- <span data-ttu-id="5e08a-108">Modus „Veröffentlicht“: In diesem Modus kann Ihr Team oder Ihre Zielgruppe den Inhalt anzeigen und mit Webparts interagieren.</span><span class="sxs-lookup"><span data-stu-id="5e08a-108">Published mode which allows your team or audience to view content and interact with web parts.</span></span> 

## <a name="edit-mode"></a><span data-ttu-id="5e08a-109">Bearbeitungsmodus</span><span class="sxs-lookup"><span data-stu-id="5e08a-109">Edit mode</span></span>

<span data-ttu-id="5e08a-110">Beim Erstellen einer neuen Seite haben Benutzer Zugriff auf die Erstellungsbenutzeroberfläche, um Inhalte hinzuzufügen und den Seiteninhalt anzupassen.</span><span class="sxs-lookup"><span data-stu-id="5e08a-110">When creating a new page, users have access to the authoring UI to add content to and customize the page content.</span></span> 


![Steuerelement „Bearbeiten“](../images/design-authoring-edit-01.png)

![Steuerelement „Bearbeiten“ mit Cursor mit Hervorhebung](../images/design-authoring-edit-02.png)


### <a name="add-hint-and-toolbox"></a><span data-ttu-id="5e08a-113">Hinweis zum Hinzufügen und Toolbox</span><span class="sxs-lookup"><span data-stu-id="5e08a-113">Add hint and Toolbox</span></span>

<span data-ttu-id="5e08a-114">Der Hinweis zum Hinzufügen besteht aus einer horizontalen Linie mit einem Pluszeichen, die angezeigt wird, wenn ein Webpart ausgewählt wird, und wenn darauf gezeigt wird, um anzugeben, wo Seitenautoren neue Webparts zu ihrer Seite hinzufügen können.</span><span class="sxs-lookup"><span data-stu-id="5e08a-114">The add hint is a horizontal line with a plus icon that is visible when a web part is selected and on hover to indicate where page authors can add new web parts to their page. The toolbox opens when a user clicks/taps the plus icon. The toolbox contains all the web parts that can be added to a page.</span></span> <span data-ttu-id="5e08a-115">Die Toolbox wird geöffnet, wenn ein Benutzer das Pluszeichen wählt.</span><span class="sxs-lookup"><span data-stu-id="5e08a-115">The Toolbox opens when a user chooses the plus icon.</span></span> <span data-ttu-id="5e08a-116">Die Toolbox enthält alle Webparts, die einer Seite hinzugefügt werden können.</span><span class="sxs-lookup"><span data-stu-id="5e08a-116">The Toolbox contains all the web parts that can be added to a page.</span></span>

![Hinweis und Toolbox mit Tools](../images/design-authoring-add-hint.png)


### <a name="toolbar"></a><span data-ttu-id="5e08a-118">Symbolleiste</span><span class="sxs-lookup"><span data-stu-id="5e08a-118">Toolbar</span></span>

<span data-ttu-id="5e08a-119">Eine vertikale Symbolleiste und das umgebende Feld sind Teil des Frameworks für jedes Webpart und werden von der Seite bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="5e08a-119">A vertical toolbar and bounding box is part of the framework for every web part and provided by the page. Each web part has an edit and delete action in the toolbar.</span></span> <span data-ttu-id="5e08a-120">Jedes Webpart weist in der Symbolleiste eine Bearbeitungs- und Löschaktion auf.</span><span class="sxs-lookup"><span data-stu-id="5e08a-120">Each web part has an edit and delete action in the toolbar.</span></span> 

![Erweiterte Symbolleiste](../images/design-authoring-toolbar.png)


### <a name="active-and-hover-states"></a><span data-ttu-id="5e08a-122">Aktiver Zustand (Mauszeiger)</span><span class="sxs-lookup"><span data-stu-id="5e08a-122">Active and hover states</span></span>

<span data-ttu-id="5e08a-123">Im aktiven Zustand (Mauszeiger) sind die Hinweisleisten primär Blau oder die primäre Designfarbe für die Website.</span><span class="sxs-lookup"><span data-stu-id="5e08a-123">On hover/active, the hint bars are primary blue or the primary theme color for the site.</span></span>

![Aktiver Zustand (Mauszeiger)](../images/design-authoring-active-hover-01.png)

<span data-ttu-id="5e08a-125">Das umgebende Feld für ein Webpart ist standardmäßig Grau, wird aber primär Blau oder die primäre Designfarbe für die Website beim Zeigen mit der Maus oder wenn das Webpart ausgewählt wird.</span><span class="sxs-lookup"><span data-stu-id="5e08a-125">The bounding box for a web part is gray by default, but picks up the primary blue or primary theme color for the site on hover or when the web part is selected.</span></span>

![Umgebendes Feld an und aus](../images/design-authoring-active-hover-02.png)


### <a name="contextual-edits"></a><span data-ttu-id="5e08a-127">Kontextbezogene Bearbeitungen</span><span class="sxs-lookup"><span data-stu-id="5e08a-127">Contextual edits</span></span>

<span data-ttu-id="5e08a-128">Entwerfen Sie eine WYSIWYG-Umgebung für Webparts, sodass Benutzer Informationen eingeben oder Inhalte hinzufügen können, die beim Veröffentlichen angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="5e08a-128">Design a WYSIWYG experience for web parts so that users can fill in information or add content that will be displayed when published.</span></span> <span data-ttu-id="5e08a-129">Diese Inhalte sollten auf der Seite eingegeben werden, sodass der Benutzer versteht, wie sie im Viewer wiedergegeben werden.</span><span class="sxs-lookup"><span data-stu-id="5e08a-129">This content should be entered on the page so the user understands how the it will render in the viewer.</span></span> <span data-ttu-id="5e08a-130">Titel und Beschreibungen sollten beispielsweise dort eingegeben werden, wo der Text angezeigt wird, oder neue Aufgaben sollten im Kontext der Seite hinzugefügt und geändert werden.</span><span class="sxs-lookup"><span data-stu-id="5e08a-130">For example, titles and descriptions should be filled out where the text displays; new tasks should be added and modified in the context of the page.</span></span>

![Kontextbezogene Elementbearbeitungen](../images/design-authoring-contextual-edits.png)


### <a name="item-level-edits"></a><span data-ttu-id="5e08a-132">Bearbeitungen auf Elementebene</span><span class="sxs-lookup"><span data-stu-id="5e08a-132">Item-level edits</span></span>

<span data-ttu-id="5e08a-133">Die Benutzeroberfläche kann sich innerhalb des Webpart ändern. Text wird zum Beispiel in ein Textfeld umgewandelt, oder Sie können die Benutzeroberfläche zur Neuanordnung von Elementen oder zum Überprüfen von Aufgaben in einem Webpart anzeigen.</span><span class="sxs-lookup"><span data-stu-id="5e08a-133">UI can change within the web part; for example, turning text into a text field to fill out links or when displaying UI to reorder items or to check of tasks in a web part</span></span> <span data-ttu-id="5e08a-134">Sie können interaktive Funktionalität für Webparts im Bearbeitungsmodus, im schreibgeschützten Modus oder in beiden Modi aktivieren, je nach Designabsicht.</span><span class="sxs-lookup"><span data-stu-id="5e08a-134">You can enable interactive functionality for web parts in edit mode, in read mode, or in both, depending on your design intent.</span></span>

![Bearbeitung auf Elementebene mit ausgewähltem Zustand](../images/design-authoring-item-level.png)


### <a name="property-panes"></a><span data-ttu-id="5e08a-136">Eigenschaftenbereiche</span><span class="sxs-lookup"><span data-stu-id="5e08a-136">Property panes</span></span>

<span data-ttu-id="5e08a-137">Eigenschaftenbereiche werden über das Symbol  **Bearbeiten** auf der Symbolleiste aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="5e08a-137">Property panes are invoked via the **Edit** icon on the toolbar.</span></span> <span data-ttu-id="5e08a-138">Eigenschaftenbereiche sollten in erster Linie Konfigurationseinstellungen enthalten, die Features aktivieren oder deaktivieren, die entweder auf der Seite angezeigt werden oder die einen Aufruf eines Diensts vornehmen, um Inhalte anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="5e08a-138">Property panes are invoked via the edit action icon on the toolbar. Panes should primarily contain configuration settings that enable/disable features that either show on page or that make a call to a service to display content.</span></span> 

![Bereich „Erweitert“](../images/design-authoring-panes.png)


## <a name="published-mode"></a><span data-ttu-id="5e08a-140">Modus „Veröffentlicht“</span><span class="sxs-lookup"><span data-stu-id="5e08a-140">Published mode</span></span>

<span data-ttu-id="5e08a-141">Nachdem die Seite veröffentlicht wurde, wird die gesamte Bearbeitungsoberfläche für den Viewer oder Leser der Seite deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="5e08a-141">After the page is published, all edit UI is disabled and for the viewer or reader of the page.</span></span> <span data-ttu-id="5e08a-142">Um mit der Bearbeitung der Seite fortzufahren, wählt der Benutzer oben rechts in der Befehlsleiste die Schaltfläche **Bearbeiten** aus.</span><span class="sxs-lookup"><span data-stu-id="5e08a-142">To continue editing the page, the user selects the **Edit** button on the top right corner of the command bar.</span></span>

![Schaltfläche „Veröffentlichen“ hervorgehoben](../images/design-authoring-published.png)


## <a name="mobile-view"></a><span data-ttu-id="5e08a-144">Mobile Ansicht</span><span class="sxs-lookup"><span data-stu-id="5e08a-144">Mobile view</span></span>

<span data-ttu-id="5e08a-145">Alle SharePoint-Seiten sind [reaktionsschnell](grid-and-responsive-design.md), damit der Inhalt der Seite auf mobilen Geräten angezeigt werden kann.</span><span class="sxs-lookup"><span data-stu-id="5e08a-145">All SharePoint pages are [responsive](grid-and-responsive-design.md) to allow the content of the page to be viewed on mobile devices.</span></span> <span data-ttu-id="5e08a-146">Beim Entwerfen eines Webpart ist es wichtig, zu verstehen, wie die neuen SharePoint-Websiteseiten auf unterschiedlichen Geräten dargestellt werden.</span><span class="sxs-lookup"><span data-stu-id="5e08a-146">While designing a web part, it is important to understand how the new SharePoint site pages render across different devices.</span></span>



![Mobile Ansicht der Website](../images/design-authoring-mobile.png)