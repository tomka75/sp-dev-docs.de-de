---
title: Reaktive und nicht-reaktive SharePoint-Webparts
description: "Reaktive Webparts sind vollständig clientseitige Webparts, während nicht-reaktive Webparts Elemente enthalten, die eine Interaktion mit einem Server erfordern."
ms.date: 01/23/2018
ms.openlocfilehash: 74d1ccfd1ed882d5efbdd8181ac44ceb1a1674eb
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="reactive-and-nonreactive-sharepoint-web-parts"></a>Reaktive und nicht-reaktive SharePoint-Webparts

Reaktive Webparts sind vollständig clientseitige Webparts, während nicht-reaktive Webparts Elemente enthalten, die eine Interaktion mit einem Server erfordern. Wir empfehlen für SharePoint-Webparts ein reaktives Design, da ein solches Design dem UX-Modell und den WYSIWYG-Erstellungsprinzipien am besten gerecht wird. Es ist jedoch nicht immer möglich oder kosteneffizient, reaktive Webparts zu erstellen.


## <a name="reactive-web-parts"></a>Reaktive Webparts

Bei reaktiven Webparts handelt es sich um vollständig clientseitige Webparts. Das bedeutet: Jede im Eigenschaftenbereich konfigurierte Komponente wird angepasst, sobald der Benutzer auf der Seite Änderungen im Webpart vornimmt. Deaktiviert der Benutzer beispielsweise im Aufgabenlisten-Webpart die Option „Completed Tasks“, wird die zugehörige Ansicht im Webpart ausgeblendet.

<img alt="A reactive web part" src="../images/design-reactive-01.png" width="850">

## <a name="nonreactive-web-parts"></a>Nicht-reaktive Webparts
Nicht-reaktive Webparts sind nicht vollständig clientseitig. In der Regel müssen eine oder mehrere Eigenschaften Aufrufe senden, um Werte auf einem Server festzulegen oder von einem Server abzurufen oder Daten auf einem Server zu speichern. In nicht-reaktiven Webparts sollten Sie unten im Eigenschaftenbereich eine **Apply**-Schaltfläche einfügen.

Sie können diese **Apply**-Schaltfläche auch so anpassen, dass sie eine spezifischere Aktion ausführt. <!-- Is this a reference to an image? (design-wp-pp-non-reactive.png) -->

<img alt="A nonreactive web part with Apply and Cancel buttons" src="../images/design-reactive-02.png" width="850">

<br/>

In den folgenden Beispielen sehen Sie nicht-reaktive Webparts im Kontext der [drei verfügbaren Strukturen für Eigenschaftenbereiche](design-a-web-part.md).

**Beispiel mit einem einzigen Bereich**

<img alt="A nonreactive web part with a single pane property structure" src="../images/design-reactive-03.png" width="850">

<br/>

**Beispiel mit Akkordeon-Gruppen**

<img alt="A nonreactive web part with an according groups pane property structure" src="../images/design-reactive-04.png" width="850">

<br/>

**Beispiel mit einem Bereich mit mehreren Schritten**

<img alt="A nonreactive web part with a steps pane property structure" src="../images/design-reactive-05.png" width="850">

## <a name="see-also"></a>Siehe auch

- [Entwerfen von benutzerfreundlichen SharePoint-Umgebungen](design-guidance-overview.md)