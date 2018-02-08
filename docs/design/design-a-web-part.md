---
title: Entwerfen eines SharePoint-Webparts
description: "Ihnen stehen drei verschiedene Typen von Eigenschaftenbereichen zur Verfügung, mit denen Sie Webparts entwerfen und entwickeln können, die perfekt auf die Anforderungen Ihres Unternehmens oder Ihrer Kunden zugeschnitten sind."
ms.date: 01/23/2018
ms.openlocfilehash: 0e6afe3323407fda99d76bd72c7006527c30c5f5
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="designing-a-sharepoint-web-part"></a><span data-ttu-id="37169-103">Entwerfen eines SharePoint-Webparts</span><span class="sxs-lookup"><span data-stu-id="37169-103">Designing a SharePoint web part</span></span>

<span data-ttu-id="37169-104">Bevor Sie mit der Arbeit an einem SharePoint-Webpart beginnen, sollten Sie wissen, wie [Seiten in SharePoint-Websites erstellt werden](authoring-pages.md).</span><span class="sxs-lookup"><span data-stu-id="37169-104">Before you design a SharePoint web part, you should understand how to [author pages in a SharePoint site](authoring-pages.md).</span></span> <span data-ttu-id="37169-105">Erstellen Sie, falls noch nicht geschehen, eine Seite, und fügen Sie ihr Webparts verschiedenen Typs hinzu.</span><span class="sxs-lookup"><span data-stu-id="37169-105">If you haven't already, take some time to create a page and add multiple types of web parts.</span></span> <span data-ttu-id="37169-106">Außerdem ist es wichtig, dass Sie den Umgang mit Office Fabric-Komponenten und -Formatvorlagen beherrschen, damit Sie Ihr neues Webpart schneller und einfacher implementieren können.</span><span class="sxs-lookup"><span data-stu-id="37169-106">It is important know how to leverage Office Fabric components and styles to make it easier and quicker to get your new web part up and running.</span></span>

<span data-ttu-id="37169-107">Wenn Sie Webparts entwerfen möchten, sollten Sie mit den folgenden Konzepten vertraut sein:</span><span class="sxs-lookup"><span data-stu-id="37169-107">When you design web parts, it's important to be familiar with the following concepts:</span></span>

- [<span data-ttu-id="37169-108">Eigenschaftenbereichstypen und deren Verwendung</span><span class="sxs-lookup"><span data-stu-id="37169-108">Property pane types and when to use each type</span></span>](#property-pane-types)
- [<span data-ttu-id="37169-109">Reaktive und nicht-reaktive Webparts</span><span class="sxs-lookup"><span data-stu-id="37169-109">Reactive and nonreactive web parts</span></span>](reactive-and-nonreactive-web-parts.md)
- [<span data-ttu-id="37169-110">Titel und Beschreibungen</span><span class="sxs-lookup"><span data-stu-id="37169-110">Titles and descriptions</span></span>](web-part-titles-and-descriptions.md)
- [<span data-ttu-id="37169-111">Platzhalter und Fallbacks</span><span class="sxs-lookup"><span data-stu-id="37169-111">Placeholders and fallbacks</span></span>](placeholders-and-fallbacks.md)


## <a name="property-pane-types"></a><span data-ttu-id="37169-112">Eigenschaftenbereichstypen</span><span class="sxs-lookup"><span data-stu-id="37169-112">Property pane types</span></span>

<span data-ttu-id="37169-113">Ihnen stehen drei verschiedene Typen von Eigenschaftenbereichen zur Verfügung, mit denen Sie Webparts entwerfen und entwickeln können, die perfekt auf die Anforderungen Ihres Unternehmens oder Ihrer Kunden zugeschnitten sind.</span><span class="sxs-lookup"><span data-stu-id="37169-113">You can use three types of property panes to design and develop web parts that fit your business or customer needs.</span></span>

<span data-ttu-id="37169-114">Über einen Klick auf **Bearbeiten** lässt sich ein Bereich für die Konfiguration der Webparteinstellungen öffnen.</span><span class="sxs-lookup"><span data-stu-id="37169-114">To open a pane to configure settings for a web part, select **Edit**.</span></span> <span data-ttu-id="37169-115">In diesem Bereich können Features aktiviert und deaktiviert, eine Quelle und ein Layout ausgewählt und Optionen festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="37169-115">Use the pane to enable and disable features, select a source, choose a layout, and set options.</span></span> <span data-ttu-id="37169-116">Webpartinhalte sollten innerhalb des Webparts bearbeitet werden, nicht im Eigenschaftenbereich.</span><span class="sxs-lookup"><span data-stu-id="37169-116">Edit web part content within the web part rather than in the property pane.</span></span>

<span data-ttu-id="37169-117">Der Eigenschaftenbereich ist 320 Pixel groß. Sobald er geöffnet wird, wird die Seite dynamisch umgebrochen.</span><span class="sxs-lookup"><span data-stu-id="37169-117">The property pane is 320px and when opened, the page will responsively reflow.</span></span>

### <a name="single-pane"></a><span data-ttu-id="37169-118">Einzelner Bereich</span><span class="sxs-lookup"><span data-stu-id="37169-118">Single pane</span></span>

<span data-ttu-id="37169-119">Verwenden Sie einen einzelnen Bereich für einfache Webparts, bei denen nur wenige Eigenschaften konfiguriert werden können.</span><span class="sxs-lookup"><span data-stu-id="37169-119">Use a single pane for simple web parts that have only a small number of properties to configure.</span></span>

![Einzelner Bereich](../images/design-web-part-single.png)

<br/>

### <a name="accordion-pane"></a><span data-ttu-id="37169-121">Akkordeon-Bereich</span><span class="sxs-lookup"><span data-stu-id="37169-121">Accordion pane</span></span>

<span data-ttu-id="37169-122">Verwenden Sie einen Akkordeon-Bereich, wenn Sie eine oder mehrere Gruppen von Eigenschaften mit vielen Optionen implementieren möchten. Diese Variante ist auch empfehlenswert, wenn in den Gruppen lange, scrollbare Optionslisten angezeigt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="37169-122">Use an accordion pane to contain a group or groups of properties with many options, and where the groups result in a long scrolling list of options.</span></span> <span data-ttu-id="37169-123">Ein Anwendungsbeispiel wäre ein Bereich mit drei Gruppen namens „Properties“, „Appearance“ und „Layout“, von denen jede über zehn Komponenten verfügt.</span><span class="sxs-lookup"><span data-stu-id="37169-123">For example, you might have three groups named Properties, Appearance, and Layout, each with ten components.</span></span>

<span data-ttu-id="37169-124">Sie sollten Akkordeon-Bereiche ebenfalls verwenden, wenn Sie Kategorisierung auf ein komplexes Webpart anwenden müssen.</span><span class="sxs-lookup"><span data-stu-id="37169-124">Use accordion panes when you need to apply categorization for a complex web part.</span></span>

![Akkordeon-Bereich](../images/design-web-part-accordion-group.png)

<br/>

<span data-ttu-id="37169-126">**Beispiel für Akkordeon-Gruppen, mit geöffnetem letzten Bereich**</span><span class="sxs-lookup"><span data-stu-id="37169-126">**Accordian groups example with last pane open**</span></span>

![Akkordeon-Bereich mit geöffnetem letzten Bereich](../images/design-web-part-accordion-last-open.png)

<br/>

<span data-ttu-id="37169-128">**Beispiel für Akkordeon-Gruppen mit zwei geöffneten Gruppen**</span><span class="sxs-lookup"><span data-stu-id="37169-128">**Accordion groups example with two groups open**</span></span>

![Akkordeon-Bereich mit zwei geöffneten Gruppen](../images/design-web-part-accordion-two-open.png)

<br/>

### <a name="steps-pane"></a><span data-ttu-id="37169-130">Schrittbasierter Bereich</span><span class="sxs-lookup"><span data-stu-id="37169-130">Steps pane</span></span>

<span data-ttu-id="37169-131">Ein schrittbasierter Bereich empfiehlt sich, wenn Sie Eigenschaften auf mehrere Schritte oder Seiten aufteilen möchten, beispielsweise wenn Ihr Webpart in linearer Reihenfolge konfiguriert werden muss oder wenn die im ersten Schritt getroffene Auswahl Auswirkungen darauf hat, welche Optionen im zweiten oder dritten Schritt angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="37169-131">Use a steps pane to group properties in multiple steps or pages when you need the web part to be configured in a linear order, or when choices in the first step affect the options that display in the second or third step.</span></span> 

<span data-ttu-id="37169-132">**Schritt 1 im schrittbasierten Bereich**</span><span class="sxs-lookup"><span data-stu-id="37169-132">**Step 1 of the steps pane**</span></span>

<span data-ttu-id="37169-133">In Schritt 1 ist die „Back“-Schaltfläche deaktiviert und die „Next“-Schaltfläche aktiviert.</span><span class="sxs-lookup"><span data-stu-id="37169-133">In step 1, the back button is disabled and the next button is enabled.</span></span>

![Schrittbasierter Bereich mit aktivierter „Next“-Schaltfläche](../images/design-web-part-steps-pane-01.png)

<br/>

<span data-ttu-id="37169-135">**Schritt 2 im schrittbasierten Bereich**</span><span class="sxs-lookup"><span data-stu-id="37169-135">**Step 2 of the steps pane**</span></span> 

<span data-ttu-id="37169-136">In Schritt 2 ist sowohl die „Back“-Schaltfläche als auch die „Next“-Schaltfläche aktiviert.</span><span class="sxs-lookup"><span data-stu-id="37169-136">In step 2, the back and next buttons are enabled.</span></span>

![Schrittbasierter Bereich mit den aktivierten Schaltflächen „Back“ und „Next“](../images/design-web-part-steps-pane-02.png)

<br/>

<span data-ttu-id="37169-138">**Schritt 3 im schrittbasierten Bereich**</span><span class="sxs-lookup"><span data-stu-id="37169-138">**Step 3 of the steps pane**</span></span> 

<span data-ttu-id="37169-139">In Schritt 3 ist die „Next“-Schaltfläche deaktiviert und die „Back“-Schaltfläche aktiviert.</span><span class="sxs-lookup"><span data-stu-id="37169-139">In step 3, the next button is disabled and the back button is enabled.</span></span>

![Schrittbasierter Bereich mit aktivierter „Back“-Schaltfläche](../images/design-web-part-steps-pane-03.png)


## <a name="see-also"></a><span data-ttu-id="37169-141">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="37169-141">See also</span></span>

- [<span data-ttu-id="37169-142">Entwerfen von benutzerfreundlichen SharePoint-Umgebungen</span><span class="sxs-lookup"><span data-stu-id="37169-142">Designing great SharePoint experiences</span></span>](design-guidance-overview.md)


