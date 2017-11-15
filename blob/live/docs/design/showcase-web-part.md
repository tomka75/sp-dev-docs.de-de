---
title: "Showcase für SharePoint-Webpartentwurf: Erstellen eines Eigenschaftenbereichs für Aufgabenlisten"
ms.date: 09/25/2017
ms.openlocfilehash: e2005e1f3b02fb0d6bc89fbf0fe8e701cf52985a
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-web-part-design-showcase-create-a-to-do-list-property-pane"></a><span data-ttu-id="da7b1-102">Showcase für SharePoint-Webpartentwurf: Erstellen eines Eigenschaftenbereichs für Aufgabenlisten</span><span class="sxs-lookup"><span data-stu-id="da7b1-102">SharePoint web part design showcase: Create a To-Do list property pane</span></span>

<span data-ttu-id="da7b1-103">In diesem Artikel wird beschrieben, wie Sie ein Aufgabenlisten-Webpart erstellen.</span><span class="sxs-lookup"><span data-stu-id="da7b1-103">This article describes how to create a To-Do list web part.</span></span> <span data-ttu-id="da7b1-104">Dieses Beispiel verwendet den [Eigenschaftenbereichstyp](design-a-web-part.md) mit einem Bereich, ist [reaktiv](reactive-and-nonreactive-web-parts.md) und basiert auf dem dynamischen Raster von [Office UI Fabric](https://dev.office.com/fabric#/).</span><span class="sxs-lookup"><span data-stu-id="da7b1-104">This example uses the single pane [property pane type](design-a-web-part.md) and is [reactive](reactive-and-nonreactive-web-parts.md) and based on the [Office UI Fabric](https://dev.office.com/fabric#/) responsive grid.</span></span>


1. <span data-ttu-id="da7b1-105">Fügen Sie eine Beschreibung hinzu, damit Benutzer mehr über das Webpart und seine Eigenschaften erfahren.</span><span class="sxs-lookup"><span data-stu-id="da7b1-105">Add a description to help users understand more about the web part and its properties.</span></span>

    <span data-ttu-id="da7b1-106">In diesem Beispiel lautet die Beschreibung „Select a source for your to-dos and customize the display for the list of tasks“.</span><span class="sxs-lookup"><span data-stu-id="da7b1-106">In this example, the description is "Select a source for your to-dos and customize the display for the list of tasks."</span></span>
    
    ![Hinzufügen einer Beschreibung](../images/design-showcase-01.png)

2. <span data-ttu-id="da7b1-108">Fügen Sie eine Fabric-[Dropdown-Komponente](http://dev.office.com/fabric#/components/dropdown) hinzu, die mit einer Liste verbunden ist.</span><span class="sxs-lookup"><span data-stu-id="da7b1-108">Add a Fabric [drop-down component](http://dev.office.com/fabric#/components/dropdown) connected to a list.</span></span>

    ![Hinzufügen einer Fabric-Dropdown-Komponente](../images/design-showcase-02.png)

3. <span data-ttu-id="da7b1-110">Fügen Sie eine Fabric-[Checkbox-Komponente](http://dev.office.com/fabric#/components/checkbox) (Kontrollkästchen) zur Anzeige abgeschlossener Aufgaben hinzu.</span><span class="sxs-lookup"><span data-stu-id="da7b1-110">Add a Fabric [checkbox component](http://dev.office.com/fabric#/components/checkbox) to display completed tasks.</span></span>

    ![Hinzufügen einer Fabric-Checkbox-Komponente](../images/design-showcase-03.png)

4. <span data-ttu-id="da7b1-112">Fügen Sie zwei weitere Kontrollkästchen zum Steuern von Anzeigeoptionen hinzu.</span><span class="sxs-lookup"><span data-stu-id="da7b1-112">Add two more checkboxes to control display options.</span></span>

    ![Hinzufügen von zwei weiteren Fabric-Checkbox-Komponenten](../images/design-showcase-04.png)

5. <span data-ttu-id="da7b1-114">Fügen Sie eine Fabric-[Slider-Komponente](http://dev.office.com/fabric#/components/slider) (Schieberegler) für die maximale Anzahl von anzuzeigenden Elementen hinzu.</span><span class="sxs-lookup"><span data-stu-id="da7b1-114">Add a Fabric [slider](http://dev.office.com/fabric#/components/slider) for the maximum number of items to display.</span></span>

    ![Hinzufügen einer Fabric-Slider-Komponente](../images/design-showcase-05.png)

6. <span data-ttu-id="da7b1-116">Als Nächstes wählt der Autor der Seite eine Liste aus oder fügt manuell Aufgaben hinzu, um das Aufgabenlisten-Webpart vorab auszufüllen.</span><span class="sxs-lookup"><span data-stu-id="da7b1-116">Next, the author of the page selects a list or manually adds tasks to prepopulate the To-Do list web part.</span></span>

    <span data-ttu-id="da7b1-117">![Auswählen einer Liste im Bereich](../images/design-showcase-06.png) ![Auswählen einer Liste im Bereich (erweitert)](../images/design-showcase-07.png) ![Manuelles Hinzufügen von Aufgaben zur Liste](../images/design-showcase-08.png)</span><span class="sxs-lookup"><span data-stu-id="da7b1-117">![Select a list in pane](../images/design-showcase-06.png) ![Select a list in pane expanded](../images/design-showcase-07.png) ![Manual addition of tasks to list](../images/design-showcase-08.png)</span></span>

7. <span data-ttu-id="da7b1-118">Das Webpart zeigt einen Indikator für Elemente, die auf die Seite geladen werden.</span><span class="sxs-lookup"><span data-stu-id="da7b1-118">The web part shows an indicator of items loading onto the page.</span></span>

    ![Indikator für Elemente](../images/design-showcase-09.png)

8. <span data-ttu-id="da7b1-120">Elemente aus der Liste werden geladen.</span><span class="sxs-lookup"><span data-stu-id="da7b1-120">Items from the list load.</span></span>

    ![Listenelemente werden geladen](../images/design-showcase-10.png)

    <span data-ttu-id="da7b1-122">Wenn die neuen Aufgaben geladen werden, werden sie mithilfe von Animationskomponenten aus Office UI Fabric eingeblendet.</span><span class="sxs-lookup"><span data-stu-id="da7b1-122">When the new tasks are loaded the fade into view using animation styles from Office UI Fabric Web part with fabric animations</span></span>

    ![Neue Aufgaben geladen](../images/design-showcase-11.png)

9. <span data-ttu-id="da7b1-124">Der Eigenschaftenbereich steuert die Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="da7b1-124">The property pane controls the UI.</span></span> <span data-ttu-id="da7b1-125">Aufgaben mit aktivierten Pivots werden über die Kontrollkästchen „Anzeigen“ im Eigenschaftenbereich angezeigt.</span><span class="sxs-lookup"><span data-stu-id="da7b1-125">Tasks with pivots enabled are displayed via the Display checkboxes in the property pane.</span></span> 

    ![Eigenschaftenbereich, der Webpartelemente steuert](../images/design-showcase-12.png)

## <a name="responsive-views"></a><span data-ttu-id="da7b1-127">Dynamische Ansichten</span><span class="sxs-lookup"><span data-stu-id="da7b1-127">Responsive views</span></span>

<span data-ttu-id="da7b1-128">Das folgende Beispiel zeigt die 2/3-Spaltenansicht des Webparts.</span><span class="sxs-lookup"><span data-stu-id="da7b1-128">The following example shows the 2/3 column view of the web part.</span></span>

![2/3-Spaltenansicht](../images/design-showcase-13.png)

<span data-ttu-id="da7b1-130">Das folgende Beispiel zeigt die 1/3 Spaltenansicht des Webparts.</span><span class="sxs-lookup"><span data-stu-id="da7b1-130">The following example shows the 1/3 column view of the web part.</span></span>


![1/3-Spaltenansicht](../images/design-showcase-14.png)

<span data-ttu-id="da7b1-132">Das folgende Beispiel zeigt die mobile (schreibgeschützte) Ansicht des Webparts.</span><span class="sxs-lookup"><span data-stu-id="da7b1-132">The following example shows the mobile (read-only) view of the web part.</span></span>

![Mobile Ansicht des Aufgabenlisten-Webparts](../images/design-showcase-15.png)