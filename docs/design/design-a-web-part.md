---
title: Entwerfen eines SharePoint-Webparts
ms.date: 9/25/2017
ms.openlocfilehash: fdee0792f486ebb792d5aaf8d8c7993cdd273324
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="designing-a-sharepoint-web-part"></a><span data-ttu-id="9377b-102">Entwerfen eines SharePoint-Webparts</span><span class="sxs-lookup"><span data-stu-id="9377b-102">Designing a SharePoint web part</span></span>

<span data-ttu-id="9377b-103">Bevor Sie ein SharePoint-Webpart entwerfen, sollten Sie verstehen, wie [Seiten in einer SharePoint-Website erstellt werden](authoring-pages.md).</span><span class="sxs-lookup"><span data-stu-id="9377b-103">Before you design a SharePoint web part, you should understand how to [author pages in a SharePoint site](authoring-pages.md).</span></span> <span data-ttu-id="9377b-104">Wenn Sie noch nicht über diese Kenntnisse verfügen, nehmen Sie sich etwas Zeit,um eine Seite zu erstellen und mehrere Typen von Webparts hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="9377b-104">If you haven't already, take some time to create a page and add multiple types of web parts.</span></span> <span data-ttu-id="9377b-105">Es ist wichtig, dass Sie Office Fabric-Komponenten und -Formatvorlagen nutzen können, damit neue Webparts schneller und einfacher betriebsbereit sind.</span><span class="sxs-lookup"><span data-stu-id="9377b-105">It is important know how to leverage Office Fabric components and styles to make it easier and quicker to get your new web part up and running.</span></span>

<span data-ttu-id="9377b-106">Beim Entwerfen von Webparts ist es wichtig, dass Sie mit folgenden Konzepten vertraut sind:</span><span class="sxs-lookup"><span data-stu-id="9377b-106">When you design web parts, it's important to be familiar with the following concepts:</span></span>

- [<span data-ttu-id="9377b-107">Eigenschaftenbereichstypen und deren Verwendung</span><span class="sxs-lookup"><span data-stu-id="9377b-107">Property pane types and when to use each type</span></span>](#property-pane-types)
- [<span data-ttu-id="9377b-108">Dynamische und nicht dynamische Webparts</span><span class="sxs-lookup"><span data-stu-id="9377b-108">Reactive and nonreactive web parts</span></span>](reactive-and-nonreactive-web-parts.md)
- [<span data-ttu-id="9377b-109">Titel und Beschreibungen</span><span class="sxs-lookup"><span data-stu-id="9377b-109">Titles and descriptions</span></span>](web-part-titles-and-descriptions.md)
- [<span data-ttu-id="9377b-110">Fallbacks und Platzhalter</span><span class="sxs-lookup"><span data-stu-id="9377b-110">Fallbacks and placeholders</span></span>](placeholders-and-fallbacks.md)


## <a name="property-pane-types"></a><span data-ttu-id="9377b-111">Eigenschaftenbereichstypen</span><span class="sxs-lookup"><span data-stu-id="9377b-111">Property pane types</span></span>

<span data-ttu-id="9377b-112">Sie können drei Arten von Eigenschaftenbereichen zum Entwerfen und Entwickeln von Webparts verwenden, die den Anforderungen Ihres Unternehmens oder Ihrer Kunden entsprechen.</span><span class="sxs-lookup"><span data-stu-id="9377b-112">There are three types of property panes to enable you to design and develop web parts that fit your business or customer needs.</span></span>

<span data-ttu-id="9377b-113">Um einen Bereich zum Konfigurieren der Einstellungen für ein Webpart zu öffnen, wählen Sie **Bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="9377b-113">To open a pane to configure settings for a web part, choose **Edit**.</span></span> <span data-ttu-id="9377b-114">Verwenden Sie den Bereich zum Aktivieren und Deaktivieren von Features, Auswählen einer Quelle, Auswählen eines Layouts und zum Festlegen von Optionen.</span><span class="sxs-lookup"><span data-stu-id="9377b-114">Use the pane to enable and disable features, select a source, choose a layout, and set options.</span></span> <span data-ttu-id="9377b-115">Bearbeiten Sie Webpartinhalte innerhalb des Webparts, und nicht im Eigenschaftenbereich.</span><span class="sxs-lookup"><span data-stu-id="9377b-115">Edit web part content within the web part rather than in the property pane.</span></span>

<span data-ttu-id="9377b-116">Der Eigenschaftenbereich ist 320 Pixel groß, und die Seite wird beim Öffnen dynamisch umgebrochen.</span><span class="sxs-lookup"><span data-stu-id="9377b-116">The property pane is 320px and when opened, the page will responsively reflow.</span></span>

### <a name="single-pane"></a><span data-ttu-id="9377b-117">Einzelner Bereich</span><span class="sxs-lookup"><span data-stu-id="9377b-117">Single pane</span></span>
<span data-ttu-id="9377b-118">Verwenden Sie einen einzelnen Bereich für einfache Webparts, bei denen nur eine kleine Anzahl von Eigenschaften konfiguriert werden kann.</span><span class="sxs-lookup"><span data-stu-id="9377b-118">A single pane is used for simple web parts that only have a small number of properties to configure.</span></span>


![Einzelner Bereich](../images/design-web-part-single.png)


### <a name="accordion-pane"></a><span data-ttu-id="9377b-120">Accordion-Bereich</span><span class="sxs-lookup"><span data-stu-id="9377b-120">Accordion pane</span></span>
<span data-ttu-id="9377b-121">Verwenden Sie einen Accordion-Bereich für eine Gruppe bzw. Gruppen von Eigenschaften mit vielen Optionen und dann, wenn die Gruppen zu einer langen Liste mit Optionen zum Scrollen führen würden.</span><span class="sxs-lookup"><span data-stu-id="9377b-121">Use an accordion pane to contain a group or groups of properties with many options, and where the groups result in a long scrolling list of options.</span></span> <span data-ttu-id="9377b-122">Angenommen, Sie haben drei Gruppen mit dem Namen „Eigenschaften“, „Darstellung“ und „Layout“, von denen jede über zehn Komponenten verfügt.</span><span class="sxs-lookup"><span data-stu-id="9377b-122">For example, you might have three groups named Properties, Appearance, and Layout, each with ten components.</span></span>

<span data-ttu-id="9377b-123">Verwenden Sie Accordion-Bereiche, wenn Sie eine Kategorisierung für ein komplexes Webpart anwenden müssen.</span><span class="sxs-lookup"><span data-stu-id="9377b-123">Use accordion panes when you need to apply categorization for a complex web part.</span></span>

![Accordion-Bereich](../images/design-web-part-accordion-group.png)


<span data-ttu-id="9377b-125">**Beispiel für Accordion-Gruppen mit zuletzt verwendetem Bereich**</span><span class="sxs-lookup"><span data-stu-id="9377b-125">**Accordian groups example with last pane open**</span></span>


![Accordion-Bereich mit zuletzt verwendetem Bereich](../images/design-web-part-accordion-last-open.png)


<span data-ttu-id="9377b-127">**Beispiel für Accordion-Gruppen mit zwei Gruppen**</span><span class="sxs-lookup"><span data-stu-id="9377b-127">**Accordion groups example with two groups open**</span></span>

![Accordion-Bereich mit zwei Gruppen](../images/design-web-part-accordion-two-open.png)



### <a name="steps-pane"></a><span data-ttu-id="9377b-129">Bereich „Schritte“</span><span class="sxs-lookup"><span data-stu-id="9377b-129">Steps pane</span></span>

<span data-ttu-id="9377b-130">Verwenden Sie den Bereich „Schritte“ zum Gruppieren von Eigenschaften in mehreren Schritten oder Seiten, wenn das Webpart in einer linearen Reihenfolge konfiguriert werden muss oder wenn die beim ersten Schritt getroffene Auswahl Auswirkungen auf Optionen hat, die im zweiten oder dritten Schritt angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="9377b-130">A steps pane is used for grouping properties in multiple steps or pages when you need the web part to be configured in a linear order or when choices made on the first step affect options that display on the second step.</span></span> 

<span data-ttu-id="9377b-131">**Schritt 1 im Bereich „Schritte“**</span><span class="sxs-lookup"><span data-stu-id="9377b-131">**Step 1 of the steps pane**</span></span>

<span data-ttu-id="9377b-132">In Schritt 1 ist die Schaltfläche „Zurück“ deaktiviert und die Schaltfläche „Weiter“ aktiviert.</span><span class="sxs-lookup"><span data-stu-id="9377b-132">In step 1, the back button is disabled and the next button is enabled.</span></span>

![Bereich „Schritte“ mit aktivierter Schaltfläche „Weiter“](../images/design-web-part-step-pane-01.png)


<span data-ttu-id="9377b-134">**Schritt 2 im Bereich „Schritte“**</span><span class="sxs-lookup"><span data-stu-id="9377b-134">**Step 2 of the steps pane**</span></span> 

<span data-ttu-id="9377b-135">In Schritt 2 sind die Schaltflächen „Zurück“ und „Weiter“ aktiviert.</span><span class="sxs-lookup"><span data-stu-id="9377b-135">In step 2, the back and next buttons are enabled.</span></span>

![Bereich „Schritte“ mit aktivierten Schaltflächen „Zurück“ und „Weiter“](../images/design-web-part-step-pane-02.png)


<span data-ttu-id="9377b-137">**Schritt 3 im Bereich „Schritte“**</span><span class="sxs-lookup"><span data-stu-id="9377b-137">**Step 3 of the steps pane**</span></span> 

<span data-ttu-id="9377b-138">In Schritt 3 ist die Schaltfläche „Weiter“ deaktiviert und die Schaltfläche „Zurück“ aktiviert.</span><span class="sxs-lookup"><span data-stu-id="9377b-138">In step 3, the next button is disabled and the back button is enabled.</span></span>

![Bereich „Schritte“ mit aktivierter Schaltfläche „Zurück“](../images/design-web-part-step-pane-03.png)
