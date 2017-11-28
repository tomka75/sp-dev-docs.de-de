---
title: Stellvertretungs-Steuerelemente in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 3981faf45be7a2a5e80dae40859b023d9dda9092
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="delegate-controls-in-the-sharepoint-add-in-model"></a><span data-ttu-id="a3347-102">Stellvertretungs-Steuerelemente in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="a3347-102">Delegate controls in the SharePoint add-in model</span></span>
================================================

<a name="summary"></a><span data-ttu-id="a3347-103">Summary</span><span class="sxs-lookup"><span data-stu-id="a3347-103">Summary</span></span>
-------

<span data-ttu-id="a3347-104">Ansatz verwenden Sie zum Implementieren von stellvertretungs-Steuerelemente in Ihrem Code unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.</span><span class="sxs-lookup"><span data-stu-id="a3347-104">The approach you take to implement delegate controls in your code is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="a3347-105">In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario Steuerelemente, als Benutzersteuerelemente oder Websteuerelemente erstellt wurden, Delegaten Features registriert, und über die SharePoint-Lösungen bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="a3347-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, delegate controls were built as user controls or web controls, registered with features, and deployed via SharePoint Solutions.</span></span>

<span data-ttu-id="a3347-106">In einem Modell Szenario SharePoint-Add-in ist JavaScript in SharePoint-Seiten implementiert die gleiche Funktion wie stellvertretungs-Steuerelemente eingebettet.</span><span class="sxs-lookup"><span data-stu-id="a3347-106">In an SharePoint Add-in model scenario, JavaScript is embedded in SharePoint pages to implement the same functionality as delegate controls.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="a3347-107">Hohe Stufe Richtlinien</span><span class="sxs-lookup"><span data-stu-id="a3347-107">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="a3347-108">In der Regel von einer Ziehpunkt möchten wir die folgenden Richtlinien auf hohen Ebenen bieten für das stellvertretungs-Steuerelemente in das neue SharePoint-Add-in-Modell erstellen.</span><span class="sxs-lookup"><span data-stu-id="a3347-108">As a rule of a thumb, we would like to provide the following high level guidelines for creating delegate controls in the new SharePoint Add-in model.</span></span>

- <span data-ttu-id="a3347-109">Es ist kein direkten Delegaten-Steuerelement-Ersatz im SharePoint-Add-in-Modell.</span><span class="sxs-lookup"><span data-stu-id="a3347-109">There is no direct delegate control replacement in the SharePoint Add-in model.</span></span>
- <span data-ttu-id="a3347-110">Verwenden Sie eingebettetes JavaScript, um die gleiche Funktion wie stellvertretungs-Steuerelemente aus Sicht des Endbenutzers zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="a3347-110">Use embedded JavaScript to implement the same functionality as delegate controls from an end-user's perspective.</span></span>
- <span data-ttu-id="a3347-111">Interaktion mit SharePoint-Daten und-Dienste verwenden Sie SharePoint JavaScript Client Side-Objektmodell (JSOM) und/oder SharePoint/Office365-REST-APIs.</span><span class="sxs-lookup"><span data-stu-id="a3347-111">Use the SharePoint JavaScript Client Side Object Model (JSOM), and/or the SharePoint/Office365 REST APIs to interact with SharePoint data and services.</span></span>

<span data-ttu-id="a3347-112">Finden Sie unter der [Benutzersteuerelemente und Websteuerelemente (SharePoint-Add-in Modell Anleitung)](user-controls-and-web-controls-sharepoint-add-in.md) erfahren, wie JavaScript mit benutzerdefinierten Aktionen für alle SharePoint-Seiten eingebettet und JavaScript direkt in Seitenlayouts und Masterseiten einzubetten.</span><span class="sxs-lookup"><span data-stu-id="a3347-112">See the [User controls and web controls (SharePoint Add-in Model Recipe)](user-controls-and-web-controls-sharepoint-add-in.md) to learn how to embed JavaScript to all SharePoint pages with custom user actions and how to embed JavaScript directly into page layouts and master pages.</span></span>

<a name="related-links"></a><span data-ttu-id="a3347-113">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="a3347-113">Related links</span></span>
=============
- [<span data-ttu-id="a3347-114">Schneidet websitesammlungsnavigation (O365 Plug & Play-Video)</span><span class="sxs-lookup"><span data-stu-id="a3347-114">Cross site collection navigation (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Cross-site-collection-navigation)
- <span data-ttu-id="a3347-115">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="a3347-115">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="a3347-116">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="a3347-116">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="a3347-117">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="a3347-117">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="a3347-118">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="a3347-118">Related PnP samples</span></span>
===================
- [<span data-ttu-id="a3347-119">OD4B. NavLinksInjection (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="a3347-119">OD4B.NavLinksInjection (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/OD4B.NavLinksInjection)
- <span data-ttu-id="a3347-120">Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="a3347-120">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="a3347-121">Gilt für</span><span class="sxs-lookup"><span data-stu-id="a3347-121">Applies to</span></span>
==========
- <span data-ttu-id="a3347-122">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="a3347-122">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="a3347-123">Office 365 dedizierte (D)</span><span class="sxs-lookup"><span data-stu-id="a3347-123">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="a3347-124">SharePoint 2013 lokal</span><span class="sxs-lookup"><span data-stu-id="a3347-124">SharePoint 2013 on-premises</span></span>
