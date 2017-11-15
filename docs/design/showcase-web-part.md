---
title: "Showcase für SharePoint-Webpartentwurf: Erstellen eines Eigenschaftenbereichs für Aufgabenlisten"
ms.date: 09/25/2017
ms.openlocfilehash: e2005e1f3b02fb0d6bc89fbf0fe8e701cf52985a
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-web-part-design-showcase-create-a-to-do-list-property-pane"></a>Showcase für SharePoint-Webpartentwurf: Erstellen eines Eigenschaftenbereichs für Aufgabenlisten

In diesem Artikel wird beschrieben, wie Sie ein Aufgabenlisten-Webpart erstellen. Dieses Beispiel verwendet den [Eigenschaftenbereichstyp](design-a-web-part.md) mit einem Bereich, ist [reaktiv](reactive-and-nonreactive-web-parts.md) und basiert auf dem dynamischen Raster von [Office UI Fabric](https://dev.office.com/fabric#/).


1. Fügen Sie eine Beschreibung hinzu, damit Benutzer mehr über das Webpart und seine Eigenschaften erfahren.

    In diesem Beispiel lautet die Beschreibung „Select a source for your to-dos and customize the display for the list of tasks“.
    
    ![Hinzufügen einer Beschreibung](../images/design-showcase-01.png)

2. Fügen Sie eine Fabric-[Dropdown-Komponente](http://dev.office.com/fabric#/components/dropdown) hinzu, die mit einer Liste verbunden ist.

    ![Hinzufügen einer Fabric-Dropdown-Komponente](../images/design-showcase-02.png)

3. Fügen Sie eine Fabric-[Checkbox-Komponente](http://dev.office.com/fabric#/components/checkbox) (Kontrollkästchen) zur Anzeige abgeschlossener Aufgaben hinzu.

    ![Hinzufügen einer Fabric-Checkbox-Komponente](../images/design-showcase-03.png)

4. Fügen Sie zwei weitere Kontrollkästchen zum Steuern von Anzeigeoptionen hinzu.

    ![Hinzufügen von zwei weiteren Fabric-Checkbox-Komponenten](../images/design-showcase-04.png)

5. Fügen Sie eine Fabric-[Slider-Komponente](http://dev.office.com/fabric#/components/slider) (Schieberegler) für die maximale Anzahl von anzuzeigenden Elementen hinzu.

    ![Hinzufügen einer Fabric-Slider-Komponente](../images/design-showcase-05.png)

6. Als Nächstes wählt der Autor der Seite eine Liste aus oder fügt manuell Aufgaben hinzu, um das Aufgabenlisten-Webpart vorab auszufüllen.

    ![Auswählen einer Liste im Bereich](../images/design-showcase-06.png) ![Auswählen einer Liste im Bereich (erweitert)](../images/design-showcase-07.png) ![Manuelles Hinzufügen von Aufgaben zur Liste](../images/design-showcase-08.png)

7. Das Webpart zeigt einen Indikator für Elemente, die auf die Seite geladen werden.

    ![Indikator für Elemente](../images/design-showcase-09.png)

8. Elemente aus der Liste werden geladen.

    ![Listenelemente werden geladen](../images/design-showcase-10.png)

    Wenn die neuen Aufgaben geladen werden, werden sie mithilfe von Animationskomponenten aus Office UI Fabric eingeblendet.

    ![Neue Aufgaben geladen](../images/design-showcase-11.png)

9. Der Eigenschaftenbereich steuert die Benutzeroberfläche. Aufgaben mit aktivierten Pivots werden über die Kontrollkästchen „Anzeigen“ im Eigenschaftenbereich angezeigt. 

    ![Eigenschaftenbereich, der Webpartelemente steuert](../images/design-showcase-12.png)

## <a name="responsive-views"></a>Dynamische Ansichten

Das folgende Beispiel zeigt die 2/3-Spaltenansicht des Webparts.

![2/3-Spaltenansicht](../images/design-showcase-13.png)

Das folgende Beispiel zeigt die 1/3 Spaltenansicht des Webparts.


![1/3-Spaltenansicht](../images/design-showcase-14.png)

Das folgende Beispiel zeigt die mobile (schreibgeschützte) Ansicht des Webparts.

![Mobile Ansicht des Aufgabenlisten-Webparts](../images/design-showcase-15.png)