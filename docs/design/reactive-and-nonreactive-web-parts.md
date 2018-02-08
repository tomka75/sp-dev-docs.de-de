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
# <a name="reactive-and-nonreactive-sharepoint-web-parts"></a><span data-ttu-id="c595a-103">Reaktive und nicht-reaktive SharePoint-Webparts</span><span class="sxs-lookup"><span data-stu-id="c595a-103">Reactive and nonreactive SharePoint web parts</span></span>

<span data-ttu-id="c595a-104">Reaktive Webparts sind vollständig clientseitige Webparts, während nicht-reaktive Webparts Elemente enthalten, die eine Interaktion mit einem Server erfordern.</span><span class="sxs-lookup"><span data-stu-id="c595a-104">Reactive web parts are client-side only; nonreactive web parts have elements that require a server to operate.</span></span> <span data-ttu-id="c595a-105">Wir empfehlen für SharePoint-Webparts ein reaktives Design, da ein solches Design dem UX-Modell und den WYSIWYG-Erstellungsprinzipien am besten gerecht wird.</span><span class="sxs-lookup"><span data-stu-id="c595a-105">We recommend that you build your SharePoint web parts to be reactive, because that best fits the UX model and WYSIWYG principles for authoring.</span></span> <span data-ttu-id="c595a-106">Es ist jedoch nicht immer möglich oder kosteneffizient, reaktive Webparts zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="c595a-106">However, it might not be possible or cost-effective in all cases to build reactive web parts.</span></span>


## <a name="reactive-web-parts"></a><span data-ttu-id="c595a-107">Reaktive Webparts</span><span class="sxs-lookup"><span data-stu-id="c595a-107">Reactive web parts</span></span>

<span data-ttu-id="c595a-108">Bei reaktiven Webparts handelt es sich um vollständig clientseitige Webparts.</span><span class="sxs-lookup"><span data-stu-id="c595a-108">Reactive web parts are fully client-side web parts.</span></span> <span data-ttu-id="c595a-109">Das bedeutet: Jede im Eigenschaftenbereich konfigurierte Komponente wird angepasst, sobald der Benutzer auf der Seite Änderungen im Webpart vornimmt.</span><span class="sxs-lookup"><span data-stu-id="c595a-109">This means that each component configured in the property pane will reflect the change made within the web part on the page.</span></span> <span data-ttu-id="c595a-110">Deaktiviert der Benutzer beispielsweise im Aufgabenlisten-Webpart die Option „Completed Tasks“, wird die zugehörige Ansicht im Webpart ausgeblendet.</span><span class="sxs-lookup"><span data-stu-id="c595a-110">For example, for the To-Do List web part, unchecking “Completed Tasks” will hide this view in the web part.</span></span>

<img alt="A reactive web part" src="../images/design-reactive-01.png" width="850">

## <a name="nonreactive-web-parts"></a><span data-ttu-id="c595a-111">Nicht-reaktive Webparts</span><span class="sxs-lookup"><span data-stu-id="c595a-111">Nonreactive web parts</span></span>
<span data-ttu-id="c595a-112">Nicht-reaktive Webparts sind nicht vollständig clientseitig. In der Regel müssen eine oder mehrere Eigenschaften Aufrufe senden, um Werte auf einem Server festzulegen oder von einem Server abzurufen oder Daten auf einem Server zu speichern.</span><span class="sxs-lookup"><span data-stu-id="c595a-112">Nonreactive web parts are not fully client-side; generally, one or more properties need to make a call to set/pull or store data on a server.</span></span> <span data-ttu-id="c595a-113">In nicht-reaktiven Webparts sollten Sie unten im Eigenschaftenbereich eine **Apply**-Schaltfläche einfügen.</span><span class="sxs-lookup"><span data-stu-id="c595a-113">For nonreactive web parts, you should enable the **Apply** button at the bottom of the property pane.</span></span>

<span data-ttu-id="c595a-114">Sie können diese **Apply**-Schaltfläche auch so anpassen, dass sie eine spezifischere Aktion ausführt.</span><span class="sxs-lookup"><span data-stu-id="c595a-114">You can also customize the **Apply** button to be a more specific action.</span></span> <!-- Is this a reference to an image? (design-wp-pp-non-reactive.png) -->

<img alt="A nonreactive web part with Apply and Cancel buttons" src="../images/design-reactive-02.png" width="850">

<br/>

<span data-ttu-id="c595a-115">In den folgenden Beispielen sehen Sie nicht-reaktive Webparts im Kontext der [drei verfügbaren Strukturen für Eigenschaftenbereiche](design-a-web-part.md).</span><span class="sxs-lookup"><span data-stu-id="c595a-115">The following examples show nonreactive web parts in the context of the [three property pane structures](design-a-web-part.md).</span></span>

<span data-ttu-id="c595a-116">**Beispiel mit einem einzigen Bereich**</span><span class="sxs-lookup"><span data-stu-id="c595a-116">**Single pane example**</span></span>

<img alt="A nonreactive web part with a single pane property structure" src="../images/design-reactive-03.png" width="850">

<br/>

<span data-ttu-id="c595a-117">**Beispiel mit Akkordeon-Gruppen**</span><span class="sxs-lookup"><span data-stu-id="c595a-117">**Accordion groups example**</span></span>

<img alt="A nonreactive web part with an according groups pane property structure" src="../images/design-reactive-04.png" width="850">

<br/>

<span data-ttu-id="c595a-118">**Beispiel mit einem Bereich mit mehreren Schritten**</span><span class="sxs-lookup"><span data-stu-id="c595a-118">**Steps pane example**</span></span>

<img alt="A nonreactive web part with a steps pane property structure" src="../images/design-reactive-05.png" width="850">

## <a name="see-also"></a><span data-ttu-id="c595a-119">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="c595a-119">See also</span></span>

- [<span data-ttu-id="c595a-120">Entwerfen von benutzerfreundlichen SharePoint-Umgebungen</span><span class="sxs-lookup"><span data-stu-id="c595a-120">Designing great SharePoint experiences</span></span>](design-guidance-overview.md)