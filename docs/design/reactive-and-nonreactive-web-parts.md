---
title: Reaktive und nicht-reaktive SharePoint-Webparts
ms.date: 9/25/2017
ms.openlocfilehash: 33f46f3582555690ba5e9f7e08e7a0bce8c5b505
ms.sourcegitcommit: 1b295a186814ca6ab13dda1a17e34dc69a61d81e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="reactive-and-nonreactive-sharepoint-web-parts"></a><span data-ttu-id="fe212-102">Reaktive und nicht-reaktive SharePoint-Webparts</span><span class="sxs-lookup"><span data-stu-id="fe212-102">Reactive and nonreactive SharePoint web parts</span></span>

<span data-ttu-id="fe212-103">Reaktive Webparts sind vollständig clientseitige Webparts, während nicht-reaktive Webparts Elemente enthalten, die eine Interaktion mit einem Server erfordern.</span><span class="sxs-lookup"><span data-stu-id="fe212-103">Reactive web parts are client-side only; nonreactive web parts have elements that require a server to operate.</span></span> <span data-ttu-id="fe212-104">Wir empfehlen für SharePoint-Webparts ein reaktives Design, da ein solches Design dem UX-Modell und den WYSIWYG-Erstellungsprinzipien am besten gerecht wird.</span><span class="sxs-lookup"><span data-stu-id="fe212-104">We recommend that you build your SharePoint web parts to be reactive, because that best fits the UX model and WYSIWYG principles for authoring.</span></span> <span data-ttu-id="fe212-105">Es ist jedoch nicht immer möglich oder kosteneffizient, reaktive Webparts zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="fe212-105">However, it might not be possible or cost-effective in all cases to build reactive web parts.</span></span>


## <a name="reactive-web-parts"></a><span data-ttu-id="fe212-106">Reaktive Webparts</span><span class="sxs-lookup"><span data-stu-id="fe212-106">Reactive vs non-reactive web parts</span></span>

<span data-ttu-id="fe212-107">Bei reaktiven Webparts handelt es sich um vollständig clientseitige Webparts.</span><span class="sxs-lookup"><span data-stu-id="fe212-107">Reactive web parts are fully client-side web parts.</span></span> <span data-ttu-id="fe212-108">Das bedeutet: Jede im Eigenschaftenbereich konfigurierte Komponente wird angepasst, sobald der Benutzer auf der Seite Änderungen im Webpart vornimmt.</span><span class="sxs-lookup"><span data-stu-id="fe212-108">This means that each component configured in the property pane will reflect the change made within the web part on the page.</span></span> <span data-ttu-id="fe212-109">Deaktiviert der Benutzer beispielsweise im Aufgabenlisten-Webpart die Option „Completed Tasks“, wird die zugehörige Ansicht im Webpart ausgeblendet.</span><span class="sxs-lookup"><span data-stu-id="fe212-109">For example, for the To-Do List web part, unchecking “Completed Tasks” will hide this view in the web part.</span></span>

![Ein reaktives Webpart](../images/design-reactive-01.png)


## <a name="nonreactive-web-parts"></a><span data-ttu-id="fe212-111">Nicht-reaktive Webparts</span><span class="sxs-lookup"><span data-stu-id="fe212-111">Nonreactive web parts</span></span>
<span data-ttu-id="fe212-112">Nicht-reaktive Webparts sind nicht vollständig clientseitig. In der Regel müssen eine oder mehrere Eigenschaften Aufrufe senden, um Werte auf einem Server festzulegen oder von einem Server abzurufen oder Daten auf einem Server zu speichern.</span><span class="sxs-lookup"><span data-stu-id="fe212-112">Non-reactive web parts are not fully client side and generally one or more properties need to make a call to set/pull or store data on a server. In this case, you should enable the Apply and Cancel buttons at the bottom of the properties pane.</span></span> <span data-ttu-id="fe212-113">In nicht-reaktiven Webparts sollten Sie unten im Eigenschaftenbereich eine **Apply**-Schaltfläche einfügen.</span><span class="sxs-lookup"><span data-stu-id="fe212-113">For nonreactive web parts, you should enable the **Apply** button at the bottom of the property pane.</span></span>

<span data-ttu-id="fe212-114">Sie können diese **Apply**-Schaltfläche auch so anpassen, dass sie eine spezifischere Aktion ausführt.</span><span class="sxs-lookup"><span data-stu-id="fe212-114">You can also customize the **Apply** button to be a more specific action.</span></span> <!-- Is this a reference to an image? (design-wp-pp-non-reactive.png) -->

![Ein nicht-reaktives Webpart mit einer „Apply“- und einer „Cancel“-Schaltfläche](../images/design-reactive-02.png)


<span data-ttu-id="fe212-116">In den folgenden Beispielen sehen Sie nicht-reaktive Webparts im Kontext der [drei verfügbaren Strukturen für Eigenschaftenbereiche](design-a-web-part.md).</span><span class="sxs-lookup"><span data-stu-id="fe212-116">The following examples show nonreactive web parts in the context of the [three property pane structures](design-a-web-part.md).</span></span>

<span data-ttu-id="fe212-117">**Beispiel mit einem einzigen Bereich**</span><span class="sxs-lookup"><span data-stu-id="fe212-117">**Single pane example**</span></span>

![Ein nicht-reaktives Webpart mit einem einzigen Eigenschaftenbereich](../images/design-reactive-03.png)

<span data-ttu-id="fe212-119">**Beispiel mit Akkordeon-Gruppen**</span><span class="sxs-lookup"><span data-stu-id="fe212-119">**Accordion groups example**</span></span>

![Ein nicht-reaktives Webpart mit einem Eigenschaftenbereich mit Akkordeon-Gruppen](../images/design-reactive-04.png)

<span data-ttu-id="fe212-121">**Beispiel mit einem Bereich mit mehreren Schritten**</span><span class="sxs-lookup"><span data-stu-id="fe212-121">**Steps pane example**</span></span>

![Ein nicht-reaktives Webpart mit einem Eigenschaftenbereich mit mehreren Schritten](../images/design-reactive-05.png)