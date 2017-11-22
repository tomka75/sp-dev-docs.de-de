---
title: Reaktive und nicht-reaktive SharePoint-Webparts
ms.date: 9/25/2017
ms.openlocfilehash: 33f46f3582555690ba5e9f7e08e7a0bce8c5b505
ms.sourcegitcommit: 1b295a186814ca6ab13dda1a17e34dc69a61d81e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="reactive-and-nonreactive-sharepoint-web-parts"></a>Reaktive und nicht-reaktive SharePoint-Webparts

Reaktive Webparts sind vollständig clientseitige Webparts, während nicht-reaktive Webparts Elemente enthalten, die eine Interaktion mit einem Server erfordern. Wir empfehlen für SharePoint-Webparts ein reaktives Design, da ein solches Design dem UX-Modell und den WYSIWYG-Erstellungsprinzipien am besten gerecht wird. Es ist jedoch nicht immer möglich oder kosteneffizient, reaktive Webparts zu erstellen.


## <a name="reactive-web-parts"></a>Reaktive Webparts

Bei reaktiven Webparts handelt es sich um vollständig clientseitige Webparts. Das bedeutet: Jede im Eigenschaftenbereich konfigurierte Komponente wird angepasst, sobald der Benutzer auf der Seite Änderungen im Webpart vornimmt. Deaktiviert der Benutzer beispielsweise im Aufgabenlisten-Webpart die Option „Completed Tasks“, wird die zugehörige Ansicht im Webpart ausgeblendet.

![Ein reaktives Webpart](../images/design-reactive-01.png)


## <a name="nonreactive-web-parts"></a>Nicht-reaktive Webparts
Nicht-reaktive Webparts sind nicht vollständig clientseitig. In der Regel müssen eine oder mehrere Eigenschaften Aufrufe senden, um Werte auf einem Server festzulegen oder von einem Server abzurufen oder Daten auf einem Server zu speichern. In nicht-reaktiven Webparts sollten Sie unten im Eigenschaftenbereich eine **Apply**-Schaltfläche einfügen.

Sie können diese **Apply**-Schaltfläche auch so anpassen, dass sie eine spezifischere Aktion ausführt. <!-- Is this a reference to an image? (design-wp-pp-non-reactive.png) -->

![Ein nicht-reaktives Webpart mit einer „Apply“- und einer „Cancel“-Schaltfläche](../images/design-reactive-02.png)


In den folgenden Beispielen sehen Sie nicht-reaktive Webparts im Kontext der [drei verfügbaren Strukturen für Eigenschaftenbereiche](design-a-web-part.md).

**Beispiel mit einem einzigen Bereich**

![Ein nicht-reaktives Webpart mit einem einzigen Eigenschaftenbereich](../images/design-reactive-03.png)

**Beispiel mit Akkordeon-Gruppen**

![Ein nicht-reaktives Webpart mit einem Eigenschaftenbereich mit Akkordeon-Gruppen](../images/design-reactive-04.png)

**Beispiel mit einem Bereich mit mehreren Schritten**

![Ein nicht-reaktives Webpart mit einem Eigenschaftenbereich mit mehreren Schritten](../images/design-reactive-05.png)