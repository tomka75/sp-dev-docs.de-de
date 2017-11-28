---
title: Webparts in SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 65e236df834b82d9649d2e43cd3dfef37ebdcdb4
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="web-part-in-the-sharepoint-add-in-model"></a><span data-ttu-id="9fab0-102">Webparts in SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="9fab0-102">Web part in the SharePoint add-in model</span></span>
=======================================

<a name="summary"></a><span data-ttu-id="9fab0-103">Summary</span><span class="sxs-lookup"><span data-stu-id="9fab0-103">Summary</span></span>
-------

<span data-ttu-id="9fab0-104">Ansatz verwenden Sie zum Erstellen von tragbaren Seitenkomponenten unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.</span><span class="sxs-lookup"><span data-stu-id="9fab0-104">The approach you take to create portable page components is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="9fab0-105">In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario-Webparts zum Implementieren der tragbaren Seitenkomponenten erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="9fab0-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, Web Parts were created to implement portable page components.</span></span>

<span data-ttu-id="9fab0-106">In einem Szenario mit SharePoint-Add-Ins Modell werden Add-in-Webparts (App-Webparts) zum Implementieren der tragbaren Seitenkomponenten erstellt.</span><span class="sxs-lookup"><span data-stu-id="9fab0-106">In an SharePoint Add-in model scenario, Add-in Parts (App Parts) are created to implement portable page components.</span></span>  <span data-ttu-id="9fab0-107">Add-in-Komponenten nutzen clientseitigem Code.</span><span class="sxs-lookup"><span data-stu-id="9fab0-107">Add-in parts use client side code.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="9fab0-108">Hohe Stufe Richtlinien</span><span class="sxs-lookup"><span data-stu-id="9fab0-108">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="9fab0-109">In der Regel von einer Ziehpunkt möchten wir die folgenden high Level Richtlinien bezüglich-Add-in-Teile enthalten.</span><span class="sxs-lookup"><span data-stu-id="9fab0-109">As a rule of a thumb, we would like to provide the following high level guidelines regarding Add-in Parts.</span></span>

- <span data-ttu-id="9fab0-110">Sie können nicht in Add-in-Webparts serverseitigen Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="9fab0-110">You cannot run server side code in Add-in Parts.</span></span>
- <span data-ttu-id="9fab0-111">Sie können nicht benutzerdefinierter EditorParts für Webparts-Add-in erstellen.</span><span class="sxs-lookup"><span data-stu-id="9fab0-111">You cannot create custom editor parts for Add-in Parts.</span></span>
- <span data-ttu-id="9fab0-112">Verwenden Sie das Webpart-Add-in-Skript mit JavaScript verknüpfen, die für die Interaktion mit SharePoint und andere Dienste und Erstellen einer Benutzeroberfläche verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="9fab0-112">Use the Add-in Script Part to link to JavaScript that is used to interact with SharePoint and other services and create a user interface.</span></span>
- <span data-ttu-id="9fab0-113">Standardmäßig werden benutzerdefinierte Eigenschaften, die Sie EditorParts hinzufügen immer als letzte Gruppe in einem Editor-Webpart angezeigt.</span><span class="sxs-lookup"><span data-stu-id="9fab0-113">By default, custom properties you add to editor parts are always shown as the final group in an editor part.</span></span>
    + <span data-ttu-id="9fab0-114">JavaScript können Sie um das Aussehen und Verhalten der ein Editor-Webpart für ein Webpart-Add-in zu überschreiben.</span><span class="sxs-lookup"><span data-stu-id="9fab0-114">You can use JavaScript to override the look and feel of an editor part for an Add-in Part.</span></span>
    + <span data-ttu-id="9fab0-115">Finden Sie im folgende Beispiel wird veranschaulicht, wie Sie dies tun, die ein.</span><span class="sxs-lookup"><span data-stu-id="9fab0-115">See the following sample that demonstrates how this is done.</span></span> 
    + [<span data-ttu-id="9fab0-116">Core.AppPartPropertyUIOverride (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="9fab0-116">Core.AppPartPropertyUIOverride (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppPartPropertyUIOverride)

<span data-ttu-id="9fab0-117">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="9fab0-117">**Getting Started**</span></span>

<span data-ttu-id="9fab0-118">Add-in-Webparts können auf einfache Weise mithilfe von außerhalb der Feld-Add-in-Skript Teil erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="9fab0-118">Add-in Parts may be easily created by using the out of the box Add-in Script Part.</span></span>  <span data-ttu-id="9fab0-119">Dadurch können Sie einen Link zu einer JavaScript-Datei an einer beliebigen Stelle gehostet bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="9fab0-119">This allows you to provide a link to a JavaScript file hosted anywhere.</span></span>  <span data-ttu-id="9fab0-120">Die JavaScript-Datei wird clientseitigem Code für die Interaktion mit SharePoint oder andere Dienste und Rendern einer Benutzeroberfläche verwendet.</span><span class="sxs-lookup"><span data-stu-id="9fab0-120">The JavaScript file uses client side code to interact with SharePoint or other services and render a user interface.</span></span>

<span data-ttu-id="9fab0-121">Im folgende Artikel wird beschrieben, das Add-in-Skript Teil Muster und dessen Verwendung.</span><span class="sxs-lookup"><span data-stu-id="9fab0-121">The following article describes the Add-in Script Part pattern and how to use it.</span></span>

- [<span data-ttu-id="9fab0-122">Einführung in die app Skript Teil Muster für Office365 app-Modell (MSDN-Blog-Artikel)</span><span class="sxs-lookup"><span data-stu-id="9fab0-122">Introducing app script part pattern for Office365 app model (MSDN Blog Article)</span></span>](http://blogs.msdn.com/b/vesku/archive/2014/07/08/introducing-app-script-part-pattern-for-office365-app-model.aspx)

<span data-ttu-id="9fab0-123">Das folgende Beispiel veranschaulicht, wie Sie ein Webpart-Add-in-Skript verwenden, um mit Yammer, Bing Maps und Google Maps integrieren.</span><span class="sxs-lookup"><span data-stu-id="9fab0-123">The following sample demonstrates how to use an Add-in Script Part to integrate with Yammer, Bing Maps, and Google Maps.</span></span>

- [<span data-ttu-id="9fab0-124">Core.AppScriptPart (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="9fab0-124">Core.AppScriptPart (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppScriptPart)

<span data-ttu-id="9fab0-125">Das folgende Video führt Sie durch das Codebeispiel.</span><span class="sxs-lookup"><span data-stu-id="9fab0-125">The following video walks you through the code sample.</span></span>

- [<span data-ttu-id="9fab0-126">Core.AppScriptPart (O365 Plug & Play-Video)</span><span class="sxs-lookup"><span data-stu-id="9fab0-126">Core.AppScriptPart (O365 PnP Video)</span></span>](https://channel9.msdn.com/Blogs/Office-365-Dev/App-Script-Parts-in-SharePoint-Office-365-Developer-Patterns-and-Practices)

<a name="related-links"></a><span data-ttu-id="9fab0-127">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="9fab0-127">Related links</span></span>
=============

- [<span data-ttu-id="9fab0-128">Einführung in die app Skript Teil Muster für Office365 app-Modell (MSDN-Blog-Artikel)</span><span class="sxs-lookup"><span data-stu-id="9fab0-128">Introducing app script part pattern for Office365 app model (MSDN Blog Article)</span></span>](http://blogs.msdn.com/b/vesku/archive/2014/07/08/introducing-app-script-part-pattern-for-office365-app-model.aspx)
- [<span data-ttu-id="9fab0-129">Core.AppScriptPart (O365 Plug & Play-Video)</span><span class="sxs-lookup"><span data-stu-id="9fab0-129">Core.AppScriptPart (O365 PnP Video)</span></span>](https://channel9.msdn.com/Blogs/Office-365-Dev/App-Script-Parts-in-SharePoint-Office-365-Developer-Patterns-and-Practices)
- <span data-ttu-id="9fab0-130">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="9fab0-130">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="9fab0-131">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="9fab0-131">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="9fab0-132">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="9fab0-132">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="9fab0-133">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="9fab0-133">Related PnP samples</span></span>
===================

- [<span data-ttu-id="9fab0-134">Core.AppPartPropertyUIOverride (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="9fab0-134">Core.AppPartPropertyUIOverride (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppPartPropertyUIOverride)
- [<span data-ttu-id="9fab0-135">Core.AppScriptPart (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="9fab0-135">Core.AppScriptPart (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppScriptPart)
- <span data-ttu-id="9fab0-136">Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="9fab0-136">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="9fab0-137">Gilt für</span><span class="sxs-lookup"><span data-stu-id="9fab0-137">Applies to</span></span>
==========
- <span data-ttu-id="9fab0-138">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="9fab0-138">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="9fab0-139">Office 365 dedizierte (D)</span><span class="sxs-lookup"><span data-stu-id="9fab0-139">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="9fab0-140">SharePoint 2013 lokal</span><span class="sxs-lookup"><span data-stu-id="9fab0-140">SharePoint 2013 on-premises</span></span>
