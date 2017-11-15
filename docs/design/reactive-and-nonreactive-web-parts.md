---
title: Dynamische und nicht dynamische SharePoint-Webparts
ms.date: 9/25/2017
ms.openlocfilehash: 33f46f3582555690ba5e9f7e08e7a0bce8c5b505
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="reactive-and-nonreactive-sharepoint-web-parts"></a><span data-ttu-id="f719e-102">Dynamische und nicht dynamische SharePoint-Webparts</span><span class="sxs-lookup"><span data-stu-id="f719e-102">Reactive and nonreactive SharePoint web parts</span></span>

<span data-ttu-id="f719e-103">Dynamische Webparts sind nur clientseitig; nicht dynamische Webparts enthalten Elemente, für die ein Server benötigt ist.</span><span class="sxs-lookup"><span data-stu-id="f719e-103">Reactive web parts are client-side only; nonreactive web parts have elements that require a server to operate.</span></span> <span data-ttu-id="f719e-104">Es wird empfohlen, dynamische SharePoint-Webparts erstellen, da diese am besten für das UX-Modell und die WYSIWYG-Prinzipien für die Erstellung geeignet sind.</span><span class="sxs-lookup"><span data-stu-id="f719e-104">We recommend that you build your SharePoint web parts to be reactive, because that best fits the UX model and WYSIWYG principles for authoring.</span></span> <span data-ttu-id="f719e-105">Es ist jedoch in manchen Fällen ggf. nicht möglich oder zu kostspielig, dynamische Webparts zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="f719e-105">However, it might not be possible or cost-effective in all cases to build reactive web parts.</span></span>


## <a name="reactive-web-parts"></a><span data-ttu-id="f719e-106">Dynamische Webparts</span><span class="sxs-lookup"><span data-stu-id="f719e-106">Reactive vs non-reactive web parts</span></span>

<span data-ttu-id="f719e-107">Bei dynamischen Webparts handelt es sich vollständig um clientseitige Webparts.</span><span class="sxs-lookup"><span data-stu-id="f719e-107">Reactive web parts are fully client-side web parts.</span></span> <span data-ttu-id="f719e-108">Dies bedeutet, dass für jede Komponente, die im Eigenschaftenbereich konfiguriert wird, die vorgenommene Änderung innerhalb des Webparts auf der Seite angepasst wird.</span><span class="sxs-lookup"><span data-stu-id="f719e-108">This means that each component configured in the property pane will reflect the change made within the web part on the page.</span></span> <span data-ttu-id="f719e-109">Wenn Sie beispielsweise im Aufgabenlisten-Webpart die Option „Abgeschlossene Aufgaben“ deaktivieren, wird diese Ansicht im Webpart ausgeblendet.</span><span class="sxs-lookup"><span data-stu-id="f719e-109">For example, for the To-Do List web part, unchecking “Completed Tasks” will hide this view in the web part.</span></span>

![Dynamische Webparts](../images/design-reactive-01.png)


## <a name="nonreactive-web-parts"></a><span data-ttu-id="f719e-111">Nicht dynamische Webparts</span><span class="sxs-lookup"><span data-stu-id="f719e-111">Nonreactive web parts</span></span>
<span data-ttu-id="f719e-112">Nicht dynamische Webparts sind nicht vollständig clientseitig, und in der Regel muss mindestens eine Eigenschaft einen Aufruf ausführen, um Daten auf einem Server festzulegen/abzurufen oder zu speichern.</span><span class="sxs-lookup"><span data-stu-id="f719e-112">Non-reactive web parts are not fully client side and generally one or more properties need to make a call to set/pull or store data on a server. In this case, you should enable the Apply and Cancel buttons at the bottom of the properties pane.</span></span> <span data-ttu-id="f719e-113">Sie sollten für nicht dynamische Webparts die Schaltfläche **Übernehmen** unten im Eigenschaftenbereich aktivieren.</span><span class="sxs-lookup"><span data-stu-id="f719e-113">For nonreactive web parts, you should enable the **Apply** button at the bottom of the property pane.</span></span>

<span data-ttu-id="f719e-114">Sie können auch die Schaltfläche **Übernehmen** anpassen, damit diese eine bestimmte Aktion aufweist.</span><span class="sxs-lookup"><span data-stu-id="f719e-114">You can also customize the **Apply** button to be a more specific action.</span></span> <!-- Is this a reference to an image? (design-wp-pp-non-reactive.png) -->

![Ein nicht dynamisches Webpart mit den Schaltflächen „Übernehmen“ und „Abbrechen“](../images/design-reactive-02.png)


<span data-ttu-id="f719e-116">Die folgenden Beispiele zeigen nicht dynamische Webparts im Kontext der [drei Strukturen der Eigenschaftenbereiche](design-a-web-part.md).</span><span class="sxs-lookup"><span data-stu-id="f719e-116">The following examples show nonreactive web parts in the context of the [three property pane structures](design-a-web-part.md).</span></span>

<span data-ttu-id="f719e-117">**Beispiel für einen einzelnen Bereich**</span><span class="sxs-lookup"><span data-stu-id="f719e-117">**Single pane example**</span></span>

![Ein nicht dynamisches Webpart mit einem einzelnen Bereich](../images/design-reactive-03.png)

<span data-ttu-id="f719e-119">**Beispiel für Accordion-Gruppen**</span><span class="sxs-lookup"><span data-stu-id="f719e-119">**Accordion groups example**</span></span>

![Ein nicht dynamisches Webpart mit einem Eigenschaftenbereich „Gruppen“](../images/design-reactive-04.png)

<span data-ttu-id="f719e-121">**Beispiel für Bereich „Gruppen“**</span><span class="sxs-lookup"><span data-stu-id="f719e-121">**Steps pane example**</span></span>

![Ein nicht dynamisches Webpart mit einem Eigenschaftenbereich „Schritte“](../images/design-reactive-05.png)