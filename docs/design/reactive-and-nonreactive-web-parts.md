---
title: Dynamische und nicht dynamische SharePoint-Webparts
ms.date: 9/25/2017
ms.openlocfilehash: 33f46f3582555690ba5e9f7e08e7a0bce8c5b505
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="reactive-and-nonreactive-sharepoint-web-parts"></a>Dynamische und nicht dynamische SharePoint-Webparts

Dynamische Webparts sind nur clientseitig; nicht dynamische Webparts enthalten Elemente, für die ein Server benötigt ist. Es wird empfohlen, dynamische SharePoint-Webparts erstellen, da diese am besten für das UX-Modell und die WYSIWYG-Prinzipien für die Erstellung geeignet sind. Es ist jedoch in manchen Fällen ggf. nicht möglich oder zu kostspielig, dynamische Webparts zu erstellen.


## <a name="reactive-web-parts"></a>Dynamische Webparts

Bei dynamischen Webparts handelt es sich vollständig um clientseitige Webparts. Dies bedeutet, dass für jede Komponente, die im Eigenschaftenbereich konfiguriert wird, die vorgenommene Änderung innerhalb des Webparts auf der Seite angepasst wird. Wenn Sie beispielsweise im Aufgabenlisten-Webpart die Option „Abgeschlossene Aufgaben“ deaktivieren, wird diese Ansicht im Webpart ausgeblendet.

![Dynamische Webparts](../images/design-reactive-01.png)


## <a name="nonreactive-web-parts"></a>Nicht dynamische Webparts
Nicht dynamische Webparts sind nicht vollständig clientseitig, und in der Regel muss mindestens eine Eigenschaft einen Aufruf ausführen, um Daten auf einem Server festzulegen/abzurufen oder zu speichern. Sie sollten für nicht dynamische Webparts die Schaltfläche **Übernehmen** unten im Eigenschaftenbereich aktivieren.

Sie können auch die Schaltfläche **Übernehmen** anpassen, damit diese eine bestimmte Aktion aufweist. <!-- Is this a reference to an image? (design-wp-pp-non-reactive.png) -->

![Ein nicht dynamisches Webpart mit den Schaltflächen „Übernehmen“ und „Abbrechen“](../images/design-reactive-02.png)


Die folgenden Beispiele zeigen nicht dynamische Webparts im Kontext der [drei Strukturen der Eigenschaftenbereiche](design-a-web-part.md).

**Beispiel für einen einzelnen Bereich**

![Ein nicht dynamisches Webpart mit einem einzelnen Bereich](../images/design-reactive-03.png)

**Beispiel für Accordion-Gruppen**

![Ein nicht dynamisches Webpart mit einem Eigenschaftenbereich „Gruppen“](../images/design-reactive-04.png)

**Beispiel für Bereich „Gruppen“**

![Ein nicht dynamisches Webpart mit einem Eigenschaftenbereich „Schritte“](../images/design-reactive-05.png)