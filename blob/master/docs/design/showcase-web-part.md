---
title: "Showcase Entwerfen von SharePoint-Webparts: Erstellen eines Eigenschaftenbereichs des Typs „Aufgabenliste“"
ms.date: 09/25/2017
ms.openlocfilehash: e2005e1f3b02fb0d6bc89fbf0fe8e701cf52985a
ms.sourcegitcommit: 1b295a186814ca6ab13dda1a17e34dc69a61d81e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-web-part-design-showcase-create-a-to-do-list-property-pane"></a><span data-ttu-id="15e8d-102">Showcase Entwerfen von SharePoint-Webparts: Erstellen eines Eigenschaftenbereichs des Typs „Aufgabenliste“</span><span class="sxs-lookup"><span data-stu-id="15e8d-102">SharePoint web part design showcase: Create a To-Do list property pane</span></span>

<span data-ttu-id="15e8d-103">In diesem Artikel erfahren Sie, wie Sie ein Aufgabenlisten-Webpart erstellen.</span><span class="sxs-lookup"><span data-stu-id="15e8d-103">This article describes how to create a To-Do list web part.</span></span> <span data-ttu-id="15e8d-104">Unser Beispiel verwendet den [Eigenschaftenbereichstyp](design-a-web-part.md) mit einem einzigen Bereich, ist [reaktiv](reactive-and-nonreactive-web-parts.md) und basiert auf dem dynamischen Raster von [Office UI Fabric](https://dev.office.com/fabric#/).</span><span class="sxs-lookup"><span data-stu-id="15e8d-104">This example uses the single pane [property pane type](design-a-web-part.md) and is [reactive](reactive-and-nonreactive-web-parts.md) and based on the [Office UI Fabric](https://dev.office.com/fabric#/) responsive grid.</span></span>


1. <span data-ttu-id="15e8d-105">Fügen Sie eine Beschreibung hinzu, die Benutzer über das Webpart und seine Eigenschaften informiert.</span><span class="sxs-lookup"><span data-stu-id="15e8d-105">Add a description to help users understand more about the web part and its properties.</span></span>

    <span data-ttu-id="15e8d-106">In diesem Beispiel haben wir als Wert für die Beschreibung „Select a source for your to-dos and customize the display for the list of tasks.“ angegeben.</span><span class="sxs-lookup"><span data-stu-id="15e8d-106">In this example, the description is "Select a source for your to-dos and customize the display for the list of tasks."</span></span>
    
    ![Hinzufügen einer Beschreibung](../images/design-showcase-01.png)

2. <span data-ttu-id="15e8d-108">Fügen Sie eine Fabric-[Dropdownkomponente](http://dev.office.com/fabric#/components/dropdown) hinzu, die mit einer Liste verknüpft ist.</span><span class="sxs-lookup"><span data-stu-id="15e8d-108">Add a Fabric [drop-down component](http://dev.office.com/fabric#/components/dropdown) connected to a list.</span></span>

    ![Hinzufügen einer Fabric-Dropdownkomponente](../images/design-showcase-02.png)

3. <span data-ttu-id="15e8d-110">Fügen Sie eine Fabric-[Kontrollkästchenkomponente](http://dev.office.com/fabric#/components/checkbox) hinzu, über die abgeschlossene Aufgaben angezeigt werden können.</span><span class="sxs-lookup"><span data-stu-id="15e8d-110">Add a Fabric [checkbox component](http://dev.office.com/fabric#/components/checkbox) to display completed tasks.</span></span>

    ![Hinzufügen einer Fabric-Kontrollkästchenkomponente](../images/design-showcase-03.png)

4. <span data-ttu-id="15e8d-112">Fügen Sie zwei weitere Kontrollkästchen hinzu, mit denen der Benutzer die Anzeigeoptionen steuern kann.</span><span class="sxs-lookup"><span data-stu-id="15e8d-112">Add two more checkboxes to control display options.</span></span>

    ![Hinzufügen von zwei weiteren Fabric-Kontrollkästchenkomponenten](../images/design-showcase-04.png)

5. <span data-ttu-id="15e8d-114">Fügen Sie eine Fabric-[Schiebereglerkomponente](http://dev.office.com/fabric#/components/slider) hinzu, über die der Benutzer festlegen kann, wie viele Elemente maximal angezeigt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="15e8d-114">Add a Fabric [slider](http://dev.office.com/fabric#/components/slider) for the maximum number of items to display.</span></span>

    ![Hinzufügen einer Fabric-Schiebereglerkomponente](../images/design-showcase-05.png)

6. <span data-ttu-id="15e8d-116">Als Nächstes wählen Sie eine Liste aus, die automatisch im Aufgabenlisten-Webpart angezeigt werden soll. Sie können auch manuell Aufgaben hinzufügen, die automatisch angezeigt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="15e8d-116">Next, the author of the page selects a list or manually adds tasks to prepopulate the To-Do list web part.</span></span>

    <span data-ttu-id="15e8d-117">![Auswählen einer Liste im Bereich](../images/design-showcase-06.png) ![Auswählen einer Liste im Bereich (erweitert)](../images/design-showcase-07.png) ![Manuelles Hinzufügen von Aufgaben zur Liste](../images/design-showcase-08.png)</span><span class="sxs-lookup"><span data-stu-id="15e8d-117">![Select a list in pane](../images/design-showcase-06.png) ![Select a list in pane expanded](../images/design-showcase-07.png) ![Manual addition of tasks to list](../images/design-showcase-08.png)</span></span>

7. <span data-ttu-id="15e8d-118">Das Webpart zeigt einen Indikator für Elemente an, die auf der Seite geladen werden.</span><span class="sxs-lookup"><span data-stu-id="15e8d-118">The web part shows an indicator of items loading onto the page.</span></span>

    ![Indikator für Elemente](../images/design-showcase-09.png)

8. <span data-ttu-id="15e8d-120">Die Elemente aus der Liste werden geladen.</span><span class="sxs-lookup"><span data-stu-id="15e8d-120">Items from the list load.</span></span>

    ![Laden der Listenelemente](../images/design-showcase-10.png)

    <span data-ttu-id="15e8d-122">Sobald die neuen Aufgaben geladen wurden, werden sie mithilfe von Animationskomponenten aus Office UI Fabric eingeblendet.</span><span class="sxs-lookup"><span data-stu-id="15e8d-122">When the new tasks are loaded the fade into view using animation styles from Office UI Fabric Web part with fabric animations</span></span>

    ![Geladene neue Aufgaben](../images/design-showcase-11.png)

9. <span data-ttu-id="15e8d-124">Der Eigenschaftenbereich steuert die Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="15e8d-124">The property pane controls the UI.</span></span> <span data-ttu-id="15e8d-125">Es werden alle Aufgaben mit aktivierter Navigationssteuerung angezeigt, basierend auf den unter „Display“ im Eigenschaftenbereich aktivierten Kontrollkästchen.</span><span class="sxs-lookup"><span data-stu-id="15e8d-125">Tasks with pivots enabled are displayed via the Display checkboxes in the property pane.</span></span> 

    ![Eigenschaftenbereich, der die Webpartelemente steuert](../images/design-showcase-12.png)

## <a name="responsive-views"></a><span data-ttu-id="15e8d-127">Dynamische Ansichten</span><span class="sxs-lookup"><span data-stu-id="15e8d-127">Responsive views</span></span>

<span data-ttu-id="15e8d-128">Im Beispiel unten füllt das Webpart zwei Drittel der Spaltenbreite.</span><span class="sxs-lookup"><span data-stu-id="15e8d-128">The following example shows the 2/3 column view of the web part.</span></span>

![Webpartdarstellung auf zwei Dritteln der Spaltenbreite](../images/design-showcase-13.png)

<span data-ttu-id="15e8d-130">Im folgenden Beispiel füllt das Webpart ein Drittel der Spaltenbreite.</span><span class="sxs-lookup"><span data-stu-id="15e8d-130">The following example shows the 1/3 column view of the web part.</span></span>


![Webpartdarstellung auf einem Drittel der Spaltenbreite](../images/design-showcase-14.png)

<span data-ttu-id="15e8d-132">Unten sehen Sie schließlich, wie das Webpart auf Mobilgeräten angezeigt wird (schreibgeschützte Ansicht).</span><span class="sxs-lookup"><span data-stu-id="15e8d-132">The following example shows the mobile (read-only) view of the web part.</span></span>

![Mobilgeräteansicht des Aufgabenlisten-Webparts](../images/design-showcase-15.png)