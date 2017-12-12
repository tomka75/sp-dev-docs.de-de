---
title: Informationsverwaltungsrichtlinie in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 6b98c863dd21c5769ee03f3898970c90ee46e08c
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
<a name="information-management-policy-in-the-sharepoint-add-in-model"></a><span data-ttu-id="af939-102">Informationsverwaltungsrichtlinie in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="af939-102">Information management policy in the SharePoint add-in model</span></span>
============================================================

<a name="summary"></a><span data-ttu-id="af939-103">Summary</span><span class="sxs-lookup"><span data-stu-id="af939-103">Summary</span></span>
-------

<span data-ttu-id="af939-104">Ansatz verwenden Sie zum Anwenden der Informationsverwaltungsrichtlinie unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.</span><span class="sxs-lookup"><span data-stu-id="af939-104">The approach you take to apply information management policy is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="af939-105">In einer typischen vollständige vertrauen Code (FTC) / in der Regel als Teil eines Zeitgebers Job Farmlösung Szenario Informationen Richtlinie zur Verwaltung wurde verwaltete und über die SharePoint Server-Side Object Model angewendet und über die SharePoint-Farmlösungen bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="af939-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, information management policy was managed and applied via the SharePoint Server Side Object Model and deployed via SharePoint Farm Solutions, usually as part of a Timer Job.</span></span> 

<span data-ttu-id="af939-106">In einem Szenario mit Modell SharePoint-Add-in die SharePoint-Client Side-Objekt Objektmodell (CSOM) und remote Zeitgeberaufträge dienen zum Verwalten und Informationsverwaltungsrichtlinie anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="af939-106">In a SharePoint Add-in model scenario, the SharePoint Client Side Object Model (CSOM) and remote timer jobs are used to manage and apply information management policy.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="af939-107">Hohe Stufe Richtlinien</span><span class="sxs-lookup"><span data-stu-id="af939-107">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="af939-108">In der Regel von einer Ziehpunkt möchten wir die folgenden high Level Richtlinien zum Verwalten und Anwenden von Informationsverwaltungsrichtlinien für SharePoint-Websites bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="af939-108">As a rule of a thumb, we would like to provide the following high level guidelines to manage and apply information management policies to SharePoint sites.</span></span>  

- <span data-ttu-id="af939-109">Beachten Sie, wenn Informationsverwaltungsrichtlinien auf der Ebene der Websitesammlung definiert sind, und klicken Sie dann die Besitzer der Websitesammlung, die sie deaktivieren können.</span><span class="sxs-lookup"><span data-stu-id="af939-109">Keep in mind, when information management policies are defined at the site collection level then site collection owners may disable them.</span></span>
    + <span data-ttu-id="af939-110">Wenn von Informationsverwaltungsrichtlinien Besitzer einer Websitesammlung festlegen mit dem remote-Modell und CSOM sie nicht deaktivieren können.</span><span class="sxs-lookup"><span data-stu-id="af939-110">When using the remote model and CSOM to set information management policies a site collection owner cannot disable them.</span></span>  <span data-ttu-id="af939-111">Der remote-Modell Ansatz ist ein weitere benutzerfreundliche Enterprise-Modell, das Informationsverwaltungsrichtlinien wird sichergestellt werden immer in der gesamten einer SharePoint-Umgebung aktiviert.</span><span class="sxs-lookup"><span data-stu-id="af939-111">The remote model approach is a more enterprise friendly model that ensures information management policies are always enabled throughout a SharePoint environment.</span></span>
- <span data-ttu-id="af939-112">Verwenden des SharePoint-CSOM in einem remote Zeitgeberauftrag zum Verwalten und Anwenden von Informationsverwaltungsrichtlinien.</span><span class="sxs-lookup"><span data-stu-id="af939-112">Use the SharePoint CSOM in a remote timer job to manage and apply information management policies.</span></span>

- <span data-ttu-id="af939-113">Stellen Sie sicher, dass Sie nicht die Grenzwerte für die SharePoint-API für Office 365 Throttle verletzt werden beim Arbeiten mit großen Datenmengen und rekursive crawlt beim Überprüfen von Artefakten in Ihrer SharePoint-Websites und Informationsverwaltungsrichtlinien für diese entsprechend anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="af939-113">Ensure you are not violating the Office 365 SharePoint API throttle limits when working with large data sets and recursive crawls as you inspect artifacts in your SharePoint sites and apply information management policies to them accordingly.</span></span>
    + <span data-ttu-id="af939-114">Die [Core.Throttling (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.Throttling) wird gezeigt, wie intelligent Code SharePoint-API für Office 365-Einschränkung zu schreiben.</span><span class="sxs-lookup"><span data-stu-id="af939-114">The [Core.Throttling (O365 Pnp Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.Throttling) demonstrates how to write intelligent code to handle Office 365 SharePoint API throttling.</span></span>

> [!NOTE] 
> <span data-ttu-id="af939-115">Das CSOM hat derzeit keine Methoden verwenden, um die Aufbewahrung für Inhaltstypen (nur auf Websites) festgelegt.</span><span class="sxs-lookup"><span data-stu-id="af939-115">Currently, the CSOM does not have methods to set retention on content types (only on sites).</span></span>

<span data-ttu-id="af939-116">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="af939-116">**Getting Started**</span></span>

<span data-ttu-id="af939-117">Die folgenden O365 Plug & Play-Codebeispiel und Video wird gezeigt, wie zum Verwalten und Anwenden von Informationsverwaltungsrichtlinie für SharePoint-Websites.</span><span class="sxs-lookup"><span data-stu-id="af939-117">The following O365 PnP Code Sample and video demonstrates how to manage and apply information management policy for SharePoint sites.</span></span>  <span data-ttu-id="af939-118">In diesem Beispiel wird der Code durchläuft die Inhaltstypen zu Dokumentbibliotheken in SharePoint-Websitesammlungen angewendet und eine Aufbewahrungsrichtlinie gilt.</span><span class="sxs-lookup"><span data-stu-id="af939-118">In this example, the code iterates through the content types applied to document libraries in SharePoint site collections and applies a retention policy.</span></span>

- [<span data-ttu-id="af939-119">Governance.ContentTypeEnforceRetention (O365 Plug & Play-Codebeispiel)</span><span class="sxs-lookup"><span data-stu-id="af939-119">Governance.ContentTypeEnforceRetention (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Governance.ContentTypeEnforceRetention)

<span data-ttu-id="af939-120">Im folgende Video durchlaufen im Codebeispiel.</span><span class="sxs-lookup"><span data-stu-id="af939-120">The following video walks through the code sample.</span></span>

- [<span data-ttu-id="af939-121">Informationsverwaltungsrichtlinie mit app-Modell (O365 Plug & Play-Video)</span><span class="sxs-lookup"><span data-stu-id="af939-121">Information management policy with app model (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Information-management-policy-wtih-app-model)

<a name="related-links"></a><span data-ttu-id="af939-122">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="af939-122">Related links</span></span>
=============
- [<span data-ttu-id="af939-123">Informationsverwaltungsrichtlinie mit app-Modell (O365 Plug & Play-Video)</span><span class="sxs-lookup"><span data-stu-id="af939-123">Information management policy with app model (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Information-management-policy-wtih-app-model)
- <span data-ttu-id="af939-124">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="af939-124">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="af939-125">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="af939-125">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="af939-126">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="af939-126">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="af939-127">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="af939-127">Related PnP samples</span></span>
===================

- [<span data-ttu-id="af939-128">Governance.ContentTypeEnforceRetention (O365 Plug & Play-Codebeispiel)</span><span class="sxs-lookup"><span data-stu-id="af939-128">Governance.ContentTypeEnforceRetention (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Governance.ContentTypeEnforceRetention)
- <span data-ttu-id="af939-129">Beispiele und Inhalte am https://github.com/SharePoint/PnP</span><span class="sxs-lookup"><span data-stu-id="af939-129">Samples and content at https://github.com/SharePoint/PnP</span></span>

<a name="applies-to"></a><span data-ttu-id="af939-130">Gilt für</span><span class="sxs-lookup"><span data-stu-id="af939-130">Applies to</span></span>
==========
- <span data-ttu-id="af939-131">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="af939-131">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="af939-132">Office 365 dedizierte (D) *teilweise*</span><span class="sxs-lookup"><span data-stu-id="af939-132">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="af939-133">SharePoint 2013 lokal – *teilweise*</span><span class="sxs-lookup"><span data-stu-id="af939-133">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="af939-134">*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*</span><span class="sxs-lookup"><span data-stu-id="af939-134">*Patterns for dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
