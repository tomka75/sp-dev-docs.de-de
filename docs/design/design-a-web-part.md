---
title: Entwerfen eines SharePoint-Webparts
ms.date: 9/25/2017
ms.openlocfilehash: fdee0792f486ebb792d5aaf8d8c7993cdd273324
ms.sourcegitcommit: 1b295a186814ca6ab13dda1a17e34dc69a61d81e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="designing-a-sharepoint-web-part"></a><span data-ttu-id="4009f-102">Entwerfen eines SharePoint-Webparts</span><span class="sxs-lookup"><span data-stu-id="4009f-102">Designing a SharePoint web part</span></span>

<span data-ttu-id="4009f-103">Bevor Sie mit der Arbeit an einem SharePoint-Webpart beginnen, sollten Sie wissen, wie [Seiten in SharePoint-Websites erstellt werden](authoring-pages.md).</span><span class="sxs-lookup"><span data-stu-id="4009f-103">Before you design a SharePoint web part, you should understand how to [author pages in a SharePoint site](authoring-pages.md).</span></span> <span data-ttu-id="4009f-104">Erstellen Sie, falls noch nicht geschehen, eine Seite, und fügen Sie ihr Webparts verschiedenen Typs hinzu.</span><span class="sxs-lookup"><span data-stu-id="4009f-104">If you haven't already, take some time to create a page and add multiple types of web parts.</span></span> <span data-ttu-id="4009f-105">Außerdem ist es wichtig, dass Sie den Umgang mit Office Fabric-Komponenten und -Formatvorlagen beherrschen, damit Sie Ihr neues Webpart schneller und einfacher implementieren können.</span><span class="sxs-lookup"><span data-stu-id="4009f-105">It is important know how to leverage Office Fabric components and styles to make it easier and quicker to get your new web part up and running.</span></span>

<span data-ttu-id="4009f-106">Wenn Sie Webparts entwerfen möchten, sollten Sie mit den folgenden Konzepten vertraut sein:</span><span class="sxs-lookup"><span data-stu-id="4009f-106">When you design web parts, it's important to be familiar with the following concepts:</span></span>

- [<span data-ttu-id="4009f-107">Eigenschaftenbereichstypen und deren Verwendung</span><span class="sxs-lookup"><span data-stu-id="4009f-107">Property pane types and when to use each type</span></span>](#property-pane-types)
- [<span data-ttu-id="4009f-108">Reaktive und nicht-reaktive Webparts</span><span class="sxs-lookup"><span data-stu-id="4009f-108">Reactive and nonreactive web parts</span></span>](reactive-and-nonreactive-web-parts.md)
- [<span data-ttu-id="4009f-109">Titel und Beschreibungen</span><span class="sxs-lookup"><span data-stu-id="4009f-109">Titles and descriptions</span></span>](web-part-titles-and-descriptions.md)
- [<span data-ttu-id="4009f-110">Fallbacks und Platzhalter</span><span class="sxs-lookup"><span data-stu-id="4009f-110">Fallbacks and placeholders</span></span>](placeholders-and-fallbacks.md)


## <a name="property-pane-types"></a><span data-ttu-id="4009f-111">Eigenschaftenbereichstypen</span><span class="sxs-lookup"><span data-stu-id="4009f-111">Property pane types</span></span>

<span data-ttu-id="4009f-112">Ihnen stehen drei verschiedene Typen von Eigenschaftenbereichen zur Verfügung, mit denen Sie Webparts entwerfen und entwickeln können, die perfekt auf die Anforderungen Ihres Unternehmens oder Ihrer Kunden zugeschnitten sind.</span><span class="sxs-lookup"><span data-stu-id="4009f-112">There are three types of property panes to enable you to design and develop web parts that fit your business or customer needs.</span></span>

<span data-ttu-id="4009f-113">Über einen Klick auf **Bearbeiten** lässt sich ein Bereich für die Konfiguration der Webparteinstellungen öffnen.</span><span class="sxs-lookup"><span data-stu-id="4009f-113">To open a pane to configure settings for a web part, choose **Edit**.</span></span> <span data-ttu-id="4009f-114">In diesem Bereich können Features aktiviert und deaktiviert, eine Quelle und ein Layout ausgewählt und Optionen festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="4009f-114">Use the pane to enable and disable features, select a source, choose a layout, and set options.</span></span> <span data-ttu-id="4009f-115">Webpartinhalte sollten innerhalb des Webparts bearbeitet werden, nicht im Eigenschaftenbereich.</span><span class="sxs-lookup"><span data-stu-id="4009f-115">Edit web part content within the web part rather than in the property pane.</span></span>

<span data-ttu-id="4009f-116">Der Eigenschaftenbereich ist 320 Pixel groß; sobald er geöffnet wird, wird die Seite dynamisch umgebrochen.</span><span class="sxs-lookup"><span data-stu-id="4009f-116">The property pane is 320px and when opened, the page will responsively reflow.</span></span>

### <a name="single-pane"></a><span data-ttu-id="4009f-117">Einzelner Bereich</span><span class="sxs-lookup"><span data-stu-id="4009f-117">Single pane</span></span>
<span data-ttu-id="4009f-118">Verwenden Sie einen einzelnen Bereich für einfache Webparts, bei denen nur wenige Eigenschaften konfiguriert werden können.</span><span class="sxs-lookup"><span data-stu-id="4009f-118">A single pane is used for simple web parts that only have a small number of properties to configure.</span></span>


![Einzelner Bereich](../images/design-web-part-single.png)


### <a name="accordion-pane"></a><span data-ttu-id="4009f-120">Akkordeon-Bereich</span><span class="sxs-lookup"><span data-stu-id="4009f-120">Accordion pane</span></span>
<span data-ttu-id="4009f-121">Verwenden Sie einen Akkordeon-Bereich, wenn Sie eine oder mehrere Gruppen von Eigenschaften mit vielen Optionen implementieren möchten. Diese Variante ist auch empfehlenswert, wenn in den Gruppen lange, scrollbare Optionslisten angezeigt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="4009f-121">Use an accordion pane to contain a group or groups of properties with many options, and where the groups result in a long scrolling list of options.</span></span> <span data-ttu-id="4009f-122">Ein Anwendungsbeispiel wäre ein Bereich mit drei Gruppen namens „Properties“, „Appearance“ und „Layout“, von denen jede über zehn Komponenten verfügt.</span><span class="sxs-lookup"><span data-stu-id="4009f-122">For example, you might have three groups named Properties, Appearance, and Layout, each with ten components.</span></span>

<span data-ttu-id="4009f-123">Sie sollten Akkordeon-Bereiche ebenfalls verwenden, wenn Sie Kategorisierung auf ein komplexes Webpart anwenden müssen.</span><span class="sxs-lookup"><span data-stu-id="4009f-123">Use accordion panes when you need to apply categorization for a complex web part.</span></span>

![Akkordeon-Bereich](../images/design-web-part-accordion-group.png)


<span data-ttu-id="4009f-125">**Beispiel für Akkordeon-Gruppen, mit geöffnetem letzten Bereich**</span><span class="sxs-lookup"><span data-stu-id="4009f-125">**Accordian groups example with last pane open**</span></span>


![Akkordeon-Bereich mit geöffnetem letzten Bereich](../images/design-web-part-accordion-last-open.png)


<span data-ttu-id="4009f-127">**Beispiel für Akkordeon-Gruppen mit zwei geöffneten Gruppen**</span><span class="sxs-lookup"><span data-stu-id="4009f-127">**Accordion groups example with two groups open**</span></span>

![Akkordeon-Bereich mit zwei geöffneten Gruppen](../images/design-web-part-accordion-two-open.png)



### <a name="steps-pane"></a><span data-ttu-id="4009f-129">Schrittbasierter Bereich</span><span class="sxs-lookup"><span data-stu-id="4009f-129">Steps pane</span></span>

<span data-ttu-id="4009f-130">Ein schrittbasierter Bereich empfiehlt sich, wenn Sie Eigenschaften auf mehrere Schritte oder Seiten aufteilen möchten, beispielsweise wenn Ihr Webpart in linearer Reihenfolge konfiguriert werden muss oder wenn die im ersten Schritt getroffene Auswahl Auswirkungen darauf hat, welche Optionen im zweiten oder dritten Schritt angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="4009f-130">A steps pane is used for grouping properties in multiple steps or pages when you need the web part to be configured in a linear order or when choices made on the first step affect options that display on the second step.</span></span> 

<span data-ttu-id="4009f-131">**Schritt 1 im schrittbasierten Bereich**</span><span class="sxs-lookup"><span data-stu-id="4009f-131">**Step 1 of the steps pane**</span></span>

<span data-ttu-id="4009f-132">In Schritt 1 ist die „Back“-Schaltfläche deaktiviert und die „Next“-Schaltfläche aktiviert.</span><span class="sxs-lookup"><span data-stu-id="4009f-132">In step 1, the back button is disabled and the next button is enabled.</span></span>

![Schrittbasierter Bereich mit aktivierter „Next“-Schaltfläche](../images/design-web-part-step-pane-01.png)


<span data-ttu-id="4009f-134">**Schritt 2 im schrittbasierten Bereich**</span><span class="sxs-lookup"><span data-stu-id="4009f-134">**Step 2 of the steps pane**</span></span> 

<span data-ttu-id="4009f-135">In Schritt 2 ist sowohl die „Back“-Schaltfläche als auch die „Next“-Schaltfläche aktiviert.</span><span class="sxs-lookup"><span data-stu-id="4009f-135">In step 2, the back and next buttons are enabled.</span></span>

![Schrittbasierter Bereich mit den aktivierten Schaltflächen „Back“ und „Next“](../images/design-web-part-step-pane-02.png)


<span data-ttu-id="4009f-137">**Schritt 3 im schrittbasierten Bereich**</span><span class="sxs-lookup"><span data-stu-id="4009f-137">**Step 3 of the steps pane**</span></span> 

<span data-ttu-id="4009f-138">In Schritt 3 ist die „Next“-Schaltfläche deaktiviert und die „Back“-Schaltfläche aktiviert.</span><span class="sxs-lookup"><span data-stu-id="4009f-138">In step 3, the next button is disabled and the back button is enabled.</span></span>

![Schrittbasierter Bereich mit aktivierter „Back“-Schaltfläche](../images/design-web-part-step-pane-03.png)
