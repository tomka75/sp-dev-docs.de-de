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
# <a name="sharepoint-web-part-design-showcase-create-a-to-do-list-property-pane"></a>Showcase Entwerfen von SharePoint-Webparts: Erstellen eines Eigenschaftenbereichs des Typs „Aufgabenliste“

In diesem Artikel erfahren Sie, wie Sie ein Aufgabenlisten-Webpart erstellen. Unser Beispiel verwendet den [Eigenschaftenbereichstyp](design-a-web-part.md) mit einem einzigen Bereich, ist [reaktiv](reactive-and-nonreactive-web-parts.md) und basiert auf dem dynamischen Raster von [Office UI Fabric](https://developer.microsoft.com/de-DE/fabric).


## <a name="create-a-to-do-list-web-part"></a>Erstellen eines Aufgabenlisten-Webparts

1. Fügen Sie eine Beschreibung hinzu, die Benutzer über das Webpart und seine Eigenschaften informiert.

    In diesem Beispiel haben wir als Wert für die Beschreibung „Select a source for your to-dos and customize the display for the list of tasks.“ angegeben.
    
    ![Hinzufügen einer Beschreibung](../images/design-showcase-01.png)

    <br/>

2. Fügen Sie eine Fabric-[Dropdownkomponente](https://developer.microsoft.com/de-DE/fabric#/components/dropdown) hinzu, die mit einer Liste verknüpft ist.

    ![Hinzufügen einer Fabric-Dropdownkomponente](../images/design-showcase-02.png)

    <br/>

3. Fügen Sie eine Fabric-[Kontrollkästchenkomponente](https://developer.microsoft.com/de-DE/fabric#/components/checkbox) hinzu, über die abgeschlossene Aufgaben angezeigt werden können.

    ![Hinzufügen einer Fabric-Kontrollkästchenkomponente](../images/design-showcase-03.png)

    <br/>

4. Fügen Sie zwei weitere Kontrollkästchen hinzu, mit denen der Benutzer die Anzeigeoptionen steuern kann.

    ![Hinzufügen von zwei weiteren Fabric-Kontrollkästchenkomponenten](../images/design-showcase-04.png)

    <br/>

5. Fügen Sie eine Fabric-[Schiebereglerkomponente](https://developer.microsoft.com/de-DE/fabric#/components/slider) hinzu, über die der Benutzer festlegen kann, wie viele Elemente maximal angezeigt werden sollen.

    ![Hinzufügen einer Fabric-Schiebereglerkomponente](../images/design-showcase-05.png)

    <br/>

6. Als Nächstes wählen Sie eine Liste aus, die automatisch im Aufgabenlisten-Webpart angezeigt werden soll. Sie können auch manuell Aufgaben hinzufügen, die automatisch angezeigt werden sollen.

    ![Liste im Bereich auswählen](../images/design-showcase-06.png)

    <br/>

    ![Liste im erweiterten Bereich auswählen](../images/design-showcase-07.png)

    <br/>

    ![Manuelles Hinzufügen von Aufgaben zur Liste](../images/design-showcase-08.png)

    <br/>

7. Das Webpart zeigt einen Indikator für Elemente an, die auf der Seite geladen werden.

    ![Indikator für Elemente](../images/design-showcase-09.png)

    <br/>

8. Die Elemente aus der Liste werden geladen.

    ![Laden der Listenelemente](../images/design-showcase-10.png)

    <br/>

    Sobald die neuen Aufgaben geladen wurden, werden sie mithilfe von Animationskomponenten aus Office UI Fabric eingeblendet.

    ![Geladene neue Aufgaben](../images/design-showcase-11.png)

    <br/>

9. Der Eigenschaftenbereich steuert die Benutzeroberfläche. Es werden alle Aufgaben mit aktivierter Navigationssteuerung angezeigt, basierend auf den unter „Display“ im Eigenschaftenbereich aktivierten Kontrollkästchen. 

    ![Eigenschaftenbereich, der die Webpartelemente steuert](../images/design-showcase-12.png)

    <br/>

## <a name="responsive-views"></a>Dynamische Ansichten

Im Beispiel unten füllt das Webpart zwei Drittel der Spaltenbreite.

![Webpartdarstellung auf zwei Dritteln der Spaltenbreite](../images/design-showcase-13.png)

<br/>

Im folgenden Beispiel füllt das Webpart ein Drittel der Spaltenbreite.

![Webpartdarstellung auf einem Drittel der Spaltenbreite](../images/design-showcase-14.png)

<br/>

Unten sehen Sie schließlich, wie das Webpart auf Mobilgeräten angezeigt wird (schreibgeschützte Ansicht).

![Mobilgeräteansicht des Aufgabenlisten-Webparts](../images/design-showcase-15.png)

<br/>

## <a name="see-also"></a>Siehe auch

- [Entwerfen von benutzerfreundlichen SharePoint-Umgebungen](design-guidance-overview.md)