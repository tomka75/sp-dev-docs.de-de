---
title: "Showcase Entwerfen von SharePoint-Webparts: Erstellen eines Eigenschaftenbereichs des Typs „Aufgabenliste“"
description: Erstellen Sie ein Aufgabenlisten-Webpart, das einen einzelnen Bereich verwendet und reaktiv ist.
ms.date: 01/23/2018
ms.openlocfilehash: a3df418a3143fb638210dfde4e5b39841b71444b
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="sharepoint-web-part-design-showcase-create-a-to-do-list-property-pane"></a><span data-ttu-id="8ebf1-103">Showcase Entwerfen von SharePoint-Webparts: Erstellen eines Eigenschaftenbereichs des Typs „Aufgabenliste“</span><span class="sxs-lookup"><span data-stu-id="8ebf1-103">SharePoint web part design showcase: Create a To-Do list property pane</span></span>

<span data-ttu-id="8ebf1-104">In diesem Artikel erfahren Sie, wie Sie ein Aufgabenlisten-Webpart erstellen.</span><span class="sxs-lookup"><span data-stu-id="8ebf1-104">This article describes how to create a To-Do list web part.</span></span> <span data-ttu-id="8ebf1-105">Unser Beispiel verwendet den [Eigenschaftenbereichstyp](design-a-web-part.md) mit einem einzigen Bereich, ist [reaktiv](reactive-and-nonreactive-web-parts.md) und basiert auf dem dynamischen Raster von [Office UI Fabric](https://developer.microsoft.com/de-DE/fabric).</span><span class="sxs-lookup"><span data-stu-id="8ebf1-105">This example uses the single pane [property pane type](design-a-web-part.md) and is [reactive](reactive-and-nonreactive-web-parts.md) and based on the [Office UI Fabric](https://developer.microsoft.com/de-DE/fabric) responsive grid.</span></span>


## <a name="create-a-to-do-list-web-part"></a><span data-ttu-id="8ebf1-106">Erstellen eines Aufgabenlisten-Webparts</span><span class="sxs-lookup"><span data-stu-id="8ebf1-106">Create a To-Do list web part</span></span>

1. <span data-ttu-id="8ebf1-107">Fügen Sie eine Beschreibung hinzu, die Benutzer über das Webpart und seine Eigenschaften informiert.</span><span class="sxs-lookup"><span data-stu-id="8ebf1-107">Add a description to help users understand more about the web part and its properties.</span></span>

    <span data-ttu-id="8ebf1-108">In diesem Beispiel haben wir als Wert für die Beschreibung „Select a source for your to-dos and customize the display for the list of tasks.“ angegeben.</span><span class="sxs-lookup"><span data-stu-id="8ebf1-108">In this example, the description is "Select a source for your to-dos and customize the display for the list of tasks."</span></span>
    
    ![Hinzufügen einer Beschreibung](../images/design-showcase-01.png)

    <br/>

2. <span data-ttu-id="8ebf1-110">Fügen Sie eine Fabric-[Dropdownkomponente](https://developer.microsoft.com/de-DE/fabric#/components/dropdown) hinzu, die mit einer Liste verknüpft ist.</span><span class="sxs-lookup"><span data-stu-id="8ebf1-110">Add a Fabric [drop-down component](https://developer.microsoft.com/de-DE/fabric#/components/dropdown) connected to a list.</span></span>

    ![Hinzufügen einer Fabric-Dropdownkomponente](../images/design-showcase-02.png)

    <br/>

3. <span data-ttu-id="8ebf1-112">Fügen Sie eine Fabric-[Kontrollkästchenkomponente](https://developer.microsoft.com/de-DE/fabric#/components/checkbox) hinzu, über die abgeschlossene Aufgaben angezeigt werden können.</span><span class="sxs-lookup"><span data-stu-id="8ebf1-112">Add a Fabric [checkbox component](https://developer.microsoft.com/de-DE/fabric#/components/checkbox) to display completed tasks.</span></span>

    ![Hinzufügen einer Fabric-Kontrollkästchenkomponente](../images/design-showcase-03.png)

    <br/>

4. <span data-ttu-id="8ebf1-114">Fügen Sie zwei weitere Kontrollkästchen hinzu, mit denen der Benutzer die Anzeigeoptionen steuern kann.</span><span class="sxs-lookup"><span data-stu-id="8ebf1-114">Add two more checkboxes to control display options.</span></span>

    ![Hinzufügen von zwei weiteren Fabric-Kontrollkästchenkomponenten](../images/design-showcase-04.png)

    <br/>

5. <span data-ttu-id="8ebf1-116">Fügen Sie eine Fabric-[Schiebereglerkomponente](https://developer.microsoft.com/de-DE/fabric#/components/slider) hinzu, über die der Benutzer festlegen kann, wie viele Elemente maximal angezeigt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="8ebf1-116">Add a Fabric [slider](https://developer.microsoft.com/de-DE/fabric#/components/slider) for the maximum number of items to display.</span></span>

    ![Hinzufügen einer Fabric-Schiebereglerkomponente](../images/design-showcase-05.png)

    <br/>

6. <span data-ttu-id="8ebf1-118">Als Nächstes wählen Sie eine Liste aus, die automatisch im Aufgabenlisten-Webpart angezeigt werden soll. Sie können auch manuell Aufgaben hinzufügen, die automatisch angezeigt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="8ebf1-118">Next, the author of the page selects a list or manually adds tasks to prepopulate the To-Do list web part.</span></span>

    ![Liste im Bereich auswählen](../images/design-showcase-06.png)

    <br/>

    ![Liste im erweiterten Bereich auswählen](../images/design-showcase-07.png)

    <br/>

    ![Manuelles Hinzufügen von Aufgaben zur Liste](../images/design-showcase-08.png)

    <br/>

7. <span data-ttu-id="8ebf1-122">Das Webpart zeigt einen Indikator für Elemente an, die auf der Seite geladen werden.</span><span class="sxs-lookup"><span data-stu-id="8ebf1-122">The web part shows an indicator of items loading onto the page.</span></span>

    ![Indikator für Elemente](../images/design-showcase-09.png)

    <br/>

8. <span data-ttu-id="8ebf1-124">Die Elemente aus der Liste werden geladen.</span><span class="sxs-lookup"><span data-stu-id="8ebf1-124">Items from the list load.</span></span>

    ![Laden der Listenelemente](../images/design-showcase-10.png)

    <br/>

    <span data-ttu-id="8ebf1-126">Sobald die neuen Aufgaben geladen wurden, werden sie mithilfe von Animationskomponenten aus Office UI Fabric eingeblendet.</span><span class="sxs-lookup"><span data-stu-id="8ebf1-126">When the new tasks are loaded, they fade into view using animation components from Office UI Fabric.</span></span>

    ![Geladene neue Aufgaben](../images/design-showcase-11.png)

    <br/>

9. <span data-ttu-id="8ebf1-128">Der Eigenschaftenbereich steuert die Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="8ebf1-128">The property pane controls the UI.</span></span> <span data-ttu-id="8ebf1-129">Es werden alle Aufgaben mit aktivierter Navigationssteuerung angezeigt, basierend auf den unter „Display“ im Eigenschaftenbereich aktivierten Kontrollkästchen.</span><span class="sxs-lookup"><span data-stu-id="8ebf1-129">Tasks with pivots enabled are displayed via the Display checkboxes in the property pane.</span></span> 

    ![Eigenschaftenbereich, der die Webpartelemente steuert](../images/design-showcase-12.png)

    <br/>

## <a name="responsive-views"></a><span data-ttu-id="8ebf1-131">Dynamische Ansichten</span><span class="sxs-lookup"><span data-stu-id="8ebf1-131">Responsive views</span></span>

<span data-ttu-id="8ebf1-132">Im Beispiel unten füllt das Webpart zwei Drittel der Spaltenbreite.</span><span class="sxs-lookup"><span data-stu-id="8ebf1-132">The following example shows the 2/3 column view of the web part.</span></span>

![Webpartdarstellung auf zwei Dritteln der Spaltenbreite](../images/design-showcase-13.png)

<br/>

<span data-ttu-id="8ebf1-134">Im folgenden Beispiel füllt das Webpart ein Drittel der Spaltenbreite.</span><span class="sxs-lookup"><span data-stu-id="8ebf1-134">The following example shows the 1/3 column view of the web part.</span></span>

![Webpartdarstellung auf einem Drittel der Spaltenbreite](../images/design-showcase-14.png)

<br/>

<span data-ttu-id="8ebf1-136">Unten sehen Sie schließlich, wie das Webpart auf Mobilgeräten angezeigt wird (schreibgeschützte Ansicht).</span><span class="sxs-lookup"><span data-stu-id="8ebf1-136">The following example shows the mobile (read-only) view of the web part.</span></span>

![Mobilgeräteansicht des Aufgabenlisten-Webparts](../images/design-showcase-15.png)

<br/>

## <a name="see-also"></a><span data-ttu-id="8ebf1-138">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="8ebf1-138">See also</span></span>

- [<span data-ttu-id="8ebf1-139">Entwerfen von benutzerfreundlichen SharePoint-Umgebungen</span><span class="sxs-lookup"><span data-stu-id="8ebf1-139">Designing great SharePoint experiences</span></span>](design-guidance-overview.md)