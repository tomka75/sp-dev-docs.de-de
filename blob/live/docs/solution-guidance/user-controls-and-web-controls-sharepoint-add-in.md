---
title: Benutzersteuerelemente und -Websteuerelemente in SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: cd1f3b127a7ae2eb1ac06e75f5a23c8f13563a8f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="user-controls-and-web-controls-in-the-sharepoint-add-in-model"></a><span data-ttu-id="8e1c2-102">Benutzersteuerelemente und -Websteuerelemente in SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="8e1c2-102">User controls and Web controls in the SharePoint add-in model</span></span>
=============================================================

<a name="summary"></a><span data-ttu-id="8e1c2-103">Summary</span><span class="sxs-lookup"><span data-stu-id="8e1c2-103">Summary</span></span>
-------

<span data-ttu-id="8e1c2-104">Ansatz verwenden Sie zum Implementieren von benutzerdefinierter Steuerelementen in Ihrem Code unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-104">The approach you take to implement custom controls in your code is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="8e1c2-105">In einer typischen vollständige vertrauen Code (FTC) / Szenario Farmlösung, benutzerdefinierte Steuerelemente als Benutzersteuerelemente erstellt wurden oder Web steuert und über SharePoint-Lösungen bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, custom controls were built as user controls or web controls and deployed via SharePoint Solutions.</span></span>

<span data-ttu-id="8e1c2-106">In einem Szenario mit Modell SharePoint-Add-in ist der JavaScript-Code in SharePoint-Seiten zum Implementieren von benutzerdefinierter Steuerelementen eingebettet.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-106">In a SharePoint Add-in model scenario, the JavaScript is embedded in SharePoint pages to implement custom controls.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="8e1c2-107">Allgemeine Richtlinien</span><span class="sxs-lookup"><span data-stu-id="8e1c2-107">High-level Guidelines</span></span>
---------------------

<span data-ttu-id="8e1c2-108">In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien zum Erstellen von benutzerdefinierten Steuerelementen in das neue SharePoint-Add-in-Modell bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-108">As a rule of a thumb, we would like to provide the following high-level guidelines for creating custom controls in the new SharePoint Add-in model.</span></span>

- <span data-ttu-id="8e1c2-109">Verwenden von JavaScript zum Erstellen von benutzerdefinierter Steuerelementen embedded.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-109">Use embedded JavaScript to create custom controls.</span></span>
- <span data-ttu-id="8e1c2-110">Interaktion mit SharePoint-Daten und-Dienste verwenden Sie SharePoint ECMA Client Side-Objekt Objektmodell (CSOM) und/oder SharePoint/Office 365-REST-APIs.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-110">Use the SharePoint ECMA Client Side Object Model (CSOM), and/or the SharePoint/Office 365 REST APIs to interact with SharePoint data and services.</span></span>

<a name="options-to-embed-javascript-in-sharepoint-pages"></a><span data-ttu-id="8e1c2-111">Optionen für das Einbetten von JavaScript in SharePoint-Seiten</span><span class="sxs-lookup"><span data-stu-id="8e1c2-111">Options to embed JavaScript in SharePoint pages</span></span>
-----------------------------------------------
<span data-ttu-id="8e1c2-112">Es gibt einige Optionen JavaScript in SharePoint-Seiten eingebettet.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-112">You have a few options to embed JavaScript in SharePoint pages.</span></span>

- <span data-ttu-id="8e1c2-113">Verwenden von benutzerdefinierten Aktionen</span><span class="sxs-lookup"><span data-stu-id="8e1c2-113">Use custom user actions</span></span>
- <span data-ttu-id="8e1c2-114">Einbetten von JavaScript direkt in Seitenlayouts</span><span class="sxs-lookup"><span data-stu-id="8e1c2-114">Embed JavaScript directly into page layouts</span></span>
- <span data-ttu-id="8e1c2-115">Einbetten von JavaScript direkt in benutzerdefinierten Gestaltungsvorlagen (nicht empfohlen)</span><span class="sxs-lookup"><span data-stu-id="8e1c2-115">Embed JavaScript directly into custom master pages (not recommended)</span></span>

<a name="use-custom-user-actions"></a><span data-ttu-id="8e1c2-116">Verwenden von benutzerdefinierten Aktionen</span><span class="sxs-lookup"><span data-stu-id="8e1c2-116">Use custom user actions</span></span>
-----------------------
<span data-ttu-id="8e1c2-117">In diesem Muster werden benutzerdefinierte Aktionen Einbetten von JavaScript in eine Seite zur Laufzeit verwendet.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-117">In this pattern, custom user actions are used to embed JavaScript into a page at run time.</span></span>

- <span data-ttu-id="8e1c2-118">Dieser Ansatz ist absolut unterstützt und ist ein gültiger Ansatz.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-118">This approach is absolutely supported and is a valid approach.</span></span>

<span data-ttu-id="8e1c2-119">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="8e1c2-119">**When is it a good fit?**</span></span>

<span data-ttu-id="8e1c2-120">Wenn Sie JavaScript in alle Ihre SharePoint-Seiten eingebettet werden müssen, ist diese Option geeignet.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-120">When you need to embed JavaScript into all of your SharePoint pages, this option is a good fit.</span></span>

<span data-ttu-id="8e1c2-121">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="8e1c2-121">**Getting started**</span></span>

<span data-ttu-id="8e1c2-122">Die folgenden Artikel und zugehörige Video wird gezeigt, wie benutzerdefinierte Aktionen verwenden, um JavaScript in SharePoint-Seiten eingebettet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-122">The following article and accompanying video demonstrates how to use custom user actions to embed JavaScript into SharePoint pages.</span></span>

- [<span data-ttu-id="8e1c2-123">Core.EmbedJavaScript (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="8e1c2-123">Core.EmbedJavaScript (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript)
- [<span data-ttu-id="8e1c2-124">OD4B. NavLinksInjection (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="8e1c2-124">OD4B.NavLinksInjection (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/OD4B.NavLinksInjection)
- [<span data-ttu-id="8e1c2-125">Schneidet websitesammlungsnavigation (O365 Plug & Play-Video)</span><span class="sxs-lookup"><span data-stu-id="8e1c2-125">Cross site collection navigation (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Cross-site-collection-navigation)

<a name="embed-javascript-directly-into-page-layouts"></a><span data-ttu-id="8e1c2-126">Einbetten von JavaScript direkt in Seitenlayouts</span><span class="sxs-lookup"><span data-stu-id="8e1c2-126">Embed JavaScript directly into page layouts</span></span>
-------------------------------------------

<span data-ttu-id="8e1c2-127">In diesem Muster ist JavaScript direkt in Seitenlayouts in Veröffentlichungswebsites eingebettet.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-127">In this pattern, JavaScript is embedded directly in page layouts in publishing sites.</span></span>  

- <span data-ttu-id="8e1c2-128">Dieser Ansatz ist absolut unterstützt und ist ein gültiger Ansatz.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-128">This approach is absolutely supported and is a valid approach.</span></span>
- <span data-ttu-id="8e1c2-129">Dieser Ansatz ist beim Veröffentlichen von Websites.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-129">This approach works with publishing sites.</span></span>

<span data-ttu-id="8e1c2-130">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="8e1c2-130">**When is it a good fit?**</span></span>

<span data-ttu-id="8e1c2-131">Wenn Sie JavaScript in bestimmten SharePoint-Seitenlayouts in Veröffentlichungswebsites in einem Szenario WCM einbetten müssen, ist diese Option geeignet.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-131">When you need to embed JavaScript into specific SharePoint page layouts in publishing sites in a WCM scenario, this option is a good fit.</span></span>

<a name="embed-javascript-directly-into-custom-master-pages"></a><span data-ttu-id="8e1c2-132">Einbetten von JavaScript direkt in benutzerdefinierten Gestaltungsvorlagen</span><span class="sxs-lookup"><span data-stu-id="8e1c2-132">Embed JavaScript directly into custom master pages</span></span>
--------------------------------------------------

<span data-ttu-id="8e1c2-133">In diesem Muster ist JavaScript direkt in benutzerdefinierten Gestaltungsvorlagen eingebettet.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-133">In this pattern, JavaScript is embedded directly in custom master pages.</span></span>  

- <span data-ttu-id="8e1c2-134">Diese Vorgehensweise wird nicht empfohlen.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-134">This approach is not recommended.</span></span>
- <span data-ttu-id="8e1c2-135">Dieser Ansatz ist ein gültiger Ansatz.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-135">This approach is a valid approach.</span></span>
- <span data-ttu-id="8e1c2-136">Einbetten von JavaScript direkt in benutzerdefinierten Gestaltungsvorlagen, aber behalten im Hinterkopf Dadurch werden Sie zusätzliche langfristige Kosten und Probleme mit zukünftige Updates.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-136">You can embed JavaScript directly in custom master pages, but keep in mind this will cause you additional long-term costs and challenges with future updates.</span></span>
    + <span data-ttu-id="8e1c2-137">Wenn Sie benutzerdefinierte Masterseiten verwenden möchten, bereiten Sie Änderungen der benutzerdefinierten Gestaltungsvorlagen anwenden, wenn wichtige Updates funktionsfähig zu Office 365 angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-137">If you chose to use custom master pages, be prepared to apply changes to the custom master pages when major functional updates are applied to Office 365.</span></span>

<span data-ttu-id="8e1c2-138">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="8e1c2-138">**When is it a good fit?**</span></span>

<span data-ttu-id="8e1c2-139">Wenn Sie auf JavaScript einbetten müssen eine Gestaltungsvorlage pro, ist dies eine gute Option, da es ermöglicht es Ihnen zu steuern, welche Seiten master in der JavaScript-Code eingebettet ist.</span><span class="sxs-lookup"><span data-stu-id="8e1c2-139">When you need to embed JavaScript on a per master page basis, this is a good option because it allows you to control which master pages the JavaScript is embedded in.</span></span>

<a name="related-links"></a><span data-ttu-id="8e1c2-140">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="8e1c2-140">Related links</span></span>
=============
- [<span data-ttu-id="8e1c2-141">Schneidet websitesammlungsnavigation (O365 Plug & Play-Video)</span><span class="sxs-lookup"><span data-stu-id="8e1c2-141">Cross site collection navigation (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Cross-site-collection-navigation)
- <span data-ttu-id="8e1c2-142">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="8e1c2-142">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="8e1c2-143">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="8e1c2-143">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="8e1c2-144">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="8e1c2-144">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="8e1c2-145">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="8e1c2-145">Related PnP samples</span></span>
===================
- [<span data-ttu-id="8e1c2-146">Core.EmbedJavaScript (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="8e1c2-146">Core.EmbedJavaScript (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript)
- [<span data-ttu-id="8e1c2-147">OD4B. NavLinksInjection (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="8e1c2-147">OD4B.NavLinksInjection (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/OD4B.NavLinksInjection)
- [<span data-ttu-id="8e1c2-148">Core.EmbedJavaScript.WeekNumbers (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="8e1c2-148">Core.EmbedJavaScript.WeekNumbers (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript.WeekNumbers)
- [<span data-ttu-id="8e1c2-149">Core.EmbedJavaScriptJSOM (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="8e1c2-149">Core.EmbedJavaScriptJSOM (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScriptJSOM)
- [<span data-ttu-id="8e1c2-150">Core.JavaScriptCustomization (O365 Plug & Play-Szenario mit Plug & Play-Hauptkomponente)</span><span class="sxs-lookup"><span data-stu-id="8e1c2-150">Core.JavaScriptCustomization (O365 PnP Scenario using PnP Core component)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization)
- <span data-ttu-id="8e1c2-151">Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="8e1c2-151">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="8e1c2-152">Gilt für</span><span class="sxs-lookup"><span data-stu-id="8e1c2-152">Applies to</span></span>
==========
- <span data-ttu-id="8e1c2-153">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="8e1c2-153">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="8e1c2-154">Office 365 dedizierte (D)</span><span class="sxs-lookup"><span data-stu-id="8e1c2-154">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="8e1c2-155">SharePoint 2013 lokal</span><span class="sxs-lookup"><span data-stu-id="8e1c2-155">SharePoint 2013 on-premises</span></span>
