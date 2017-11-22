---
title: "Showcase Entwerfen von SharePoint-Webparts: Erstellen eines Eigenschaftenbereichs des Typs „Aufgabenliste“"
ms.date: 09/25/2017
ms.openlocfilehash: e2005e1f3b02fb0d6bc89fbf0fe8e701cf52985a
ms.sourcegitcommit: 1b295a186814ca6ab13dda1a17e34dc69a61d81e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-web-part-design-showcase-create-a-to-do-list-property-pane"></a>Showcase Entwerfen von SharePoint-Webparts: Erstellen eines Eigenschaftenbereichs des Typs „Aufgabenliste“

In diesem Artikel erfahren Sie, wie Sie ein Aufgabenlisten-Webpart erstellen. Unser Beispiel verwendet den [Eigenschaftenbereichstyp](design-a-web-part.md) mit einem einzigen Bereich, ist [reaktiv](reactive-and-nonreactive-web-parts.md) und basiert auf dem dynamischen Raster von [Office UI Fabric](https://dev.office.com/fabric#/).


1. Fügen Sie eine Beschreibung hinzu, die Benutzer über das Webpart und seine Eigenschaften informiert.

    In diesem Beispiel haben wir als Wert für die Beschreibung „Select a source for your to-dos and customize the display for the list of tasks.“ angegeben.
    
    ![Hinzufügen einer Beschreibung](../images/design-showcase-01.png)

2. Fügen Sie eine Fabric-[Dropdownkomponente](http://dev.office.com/fabric#/components/dropdown) hinzu, die mit einer Liste verknüpft ist.

    ![Hinzufügen einer Fabric-Dropdownkomponente](../images/design-showcase-02.png)

3. Fügen Sie eine Fabric-[Kontrollkästchenkomponente](http://dev.office.com/fabric#/components/checkbox) hinzu, über die abgeschlossene Aufgaben angezeigt werden können.

    ![Hinzufügen einer Fabric-Kontrollkästchenkomponente](../images/design-showcase-03.png)

4. Fügen Sie zwei weitere Kontrollkästchen hinzu, mit denen der Benutzer die Anzeigeoptionen steuern kann.

    ![Hinzufügen von zwei weiteren Fabric-Kontrollkästchenkomponenten](../images/design-showcase-04.png)

5. Fügen Sie eine Fabric-[Schiebereglerkomponente](http://dev.office.com/fabric#/components/slider) hinzu, über die der Benutzer festlegen kann, wie viele Elemente maximal angezeigt werden sollen.

    ![Hinzufügen einer Fabric-Schiebereglerkomponente](../images/design-showcase-05.png)

6. Als Nächstes wählen Sie eine Liste aus, die automatisch im Aufgabenlisten-Webpart angezeigt werden soll. Sie können auch manuell Aufgaben hinzufügen, die automatisch angezeigt werden sollen.

    ![Auswählen einer Liste im Bereich](../images/design-showcase-06.png) ![Auswählen einer Liste im Bereich (erweitert)](../images/design-showcase-07.png) ![Manuelles Hinzufügen von Aufgaben zur Liste](../images/design-showcase-08.png)

7. Das Webpart zeigt einen Indikator für Elemente an, die auf der Seite geladen werden.

    ![Indikator für Elemente](../images/design-showcase-09.png)

8. Die Elemente aus der Liste werden geladen.

    ![Laden der Listenelemente](../images/design-showcase-10.png)

    Sobald die neuen Aufgaben geladen wurden, werden sie mithilfe von Animationskomponenten aus Office UI Fabric eingeblendet.

    ![Geladene neue Aufgaben](../images/design-showcase-11.png)

9. Der Eigenschaftenbereich steuert die Benutzeroberfläche. Es werden alle Aufgaben mit aktivierter Navigationssteuerung angezeigt, basierend auf den unter „Display“ im Eigenschaftenbereich aktivierten Kontrollkästchen. 

    ![Eigenschaftenbereich, der die Webpartelemente steuert](../images/design-showcase-12.png)

## <a name="responsive-views"></a>Dynamische Ansichten

Im Beispiel unten füllt das Webpart zwei Drittel der Spaltenbreite.

![Webpartdarstellung auf zwei Dritteln der Spaltenbreite](../images/design-showcase-13.png)

Im folgenden Beispiel füllt das Webpart ein Drittel der Spaltenbreite.


![Webpartdarstellung auf einem Drittel der Spaltenbreite](../images/design-showcase-14.png)

Unten sehen Sie schließlich, wie das Webpart auf Mobilgeräten angezeigt wird (schreibgeschützte Ansicht).

![Mobilgeräteansicht des Aufgabenlisten-Webparts](../images/design-showcase-15.png)