---
title: SharePoint Framework-Roadmap
ms.date: 12/15/2017
ms.prod: sharepoint
ms.openlocfilehash: e467c80920855fabcd7e76f174073127139f9795
ms.sourcegitcommit: d24c7dd063a417382e8d0efa83238f08dc349c2c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/22/2018
---
# <a name="sharepoint-framework-roadmap"></a><span data-ttu-id="c5364-102">SharePoint-Framework-Roadmap</span><span class="sxs-lookup"><span data-stu-id="c5364-102">SharePoint Framework roadmap</span></span>

<span data-ttu-id="c5364-103">Die Erstveröffentlichung von SharePoint-Framework enthielt nur Unterstützung für clientseitige Webparts.</span><span class="sxs-lookup"><span data-stu-id="c5364-103">First release of the SharePoint Framework contained only support for client-side web parts.</span></span> <span data-ttu-id="c5364-104">Dies war jedoch nur der Beginn der Bereitstellung zusätzlicher moderner Anpassungsfunktionen für SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c5364-104">This was however just a start on the journey for providing additional modern customization capabilities to SharePoint.</span></span> <span data-ttu-id="c5364-105">Im folgenden werden die wichtigsten Funktionen aufgeführt, die nach der Markteinführung veröffentlicht wurden.</span><span class="sxs-lookup"><span data-stu-id="c5364-105">Here is a list of key capabilities released after initial General Availability.</span></span>

- [<span data-ttu-id="c5364-106">Unterstützung für mandantenweite Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="c5364-106">Tenant scoped deployment support</span></span>](./tenant-scoped-deployment.md)
- [<span data-ttu-id="c5364-107">Lokale Unterstützung für SharePoint 2016 (Feature Pack 2)</span><span class="sxs-lookup"><span data-stu-id="c5364-107">On-premises support for SharePoint 2016 (Feature Pack 2)</span></span>](./sharepoint-2016-support.md)
- [<span data-ttu-id="c5364-108">SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="c5364-108">SharePoint Framework Extensions</span></span>](./extensions/overview-extensions.md)
- [<span data-ttu-id="c5364-109">Mandanteneigenschaften</span><span class="sxs-lookup"><span data-stu-id="c5364-109">Tenant properties</span></span>](./tenant-properties.md)
- [<span data-ttu-id="c5364-110">ALM-APIs für SPFx-Lösungen und -Add-Ins</span><span class="sxs-lookup"><span data-stu-id="c5364-110">ALM APIs for SPFx solutions and add-ins</span></span>](../apis/alm-api-for-spfx-add-ins.md)
- [<span data-ttu-id="c5364-111">Unterstützung für Office UI Fabric Core</span><span class="sxs-lookup"><span data-stu-id="c5364-111">Office UI Fabric Core support</span></span>](https://dev.office.com/blogs/improved-support-for-office-ui-fabric-core)
- [<span data-ttu-id="c5364-112">Verpacken von Objekten und Websitesammlungs-App-Katalog</span><span class="sxs-lookup"><span data-stu-id="c5364-112">Asset packaging and site collection app catalog</span></span>](../general-development/site-collection-app-catalog.md)


> [!NOTE]
> <span data-ttu-id="c5364-113">Dies ist eine Liste von Bereichen, die von den SharePoint-Entwicklern abgearbeitet und untersucht werden.</span><span class="sxs-lookup"><span data-stu-id="c5364-113">This is a list of areas which SharePoint engineering is having in the backlog and are looking into.</span></span> <span data-ttu-id="c5364-114">Das bedeutet **NICHT**, dass all diese Bereiche auch wirklich bereitgestellt werden, wir bemühen uns jedoch, Elemente und Themen aus dieser Liste in den künftigen Versionen von SharePoint-Framework schrittweise zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="c5364-114">This does **NOT** mean that all of them will be necessarily delivered, but we are looking for getting items and topics from this list gradually released with the future releases of SharePoint Framework.</span></span>

## <a name="general-improvements"></a><span data-ttu-id="c5364-115">Allgemeine Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="c5364-115">General improvements</span></span>

- <span data-ttu-id="c5364-116">Einfacher Zugriff auf die Graph-API zum Zugreifen auf benutzerspezifische Informationen (GraphHttpClient in der Vorschau)</span><span class="sxs-lookup"><span data-stu-id="c5364-116">Easy access to Graph API to access user specific information (GraphHttpClient in preview)</span></span>
- <span data-ttu-id="c5364-117">Webhooks auf Website-Ebene</span><span class="sxs-lookup"><span data-stu-id="c5364-117">Site level WebHooks</span></span>
- <span data-ttu-id="c5364-118">Textabschnitt zum Store mit Unterstützung für SharePoint-Framework aktualisiert</span><span class="sxs-lookup"><span data-stu-id="c5364-118">Updated 'store' story with SharePoint Framework support</span></span>
- <span data-ttu-id="c5364-119">Textabschnitt zum Store für SharePoint-Framework-Lösungen mit einfachem Vertriebskanal für ISVs</span><span class="sxs-lookup"><span data-stu-id="c5364-119">'Store' story for SharePoint Framework solutions with easy distribution channel for ISVs</span></span> 

## <a name="client-side-web-parts-and-add-ins"></a><span data-ttu-id="c5364-120">Clientseitige Webparts und Add-Ins</span><span class="sxs-lookup"><span data-stu-id="c5364-120">Client-side web parts++ and add-ins</span></span>

- <span data-ttu-id="c5364-121">Unterstützung für komplexere Szenarios und Interaktionen mit Webparts</span><span class="sxs-lookup"><span data-stu-id="c5364-121">Supporting more complex scenarios and interactions with web parts</span></span>
    - <span data-ttu-id="c5364-122">Kommunikation von Webpart zu Webpart</span><span class="sxs-lookup"><span data-stu-id="c5364-122">Part-to-part communication</span></span>
    - <span data-ttu-id="c5364-123">JS Framework-Isolierung</span><span class="sxs-lookup"><span data-stu-id="c5364-123">JS Framework isolation</span></span>
    - <span data-ttu-id="c5364-124">„Citizen Developer“-Modell für einfache Entwicklung</span><span class="sxs-lookup"><span data-stu-id="c5364-124">"citizen developer" model for lightweight development</span></span>

- <span data-ttu-id="c5364-125">Add-Ins für die moderne Welt: Ansprechendere Wiedergabe mit der neuen UX.</span><span class="sxs-lookup"><span data-stu-id="c5364-125">Bring add-ins to the modern world: Let’s make them play nicer with the new UX.</span></span> 
    - <span data-ttu-id="c5364-126">Azure AD-Registrierung</span><span class="sxs-lookup"><span data-stu-id="c5364-126">Azure AD Registration</span></span>
    - <span data-ttu-id="c5364-127">Systemeigene dynamische Unterstützung</span><span class="sxs-lookup"><span data-stu-id="c5364-127">Native responsive support</span></span>
    - <span data-ttu-id="c5364-128">Erstellen von Add-Ins mit SharePoint-Framework</span><span class="sxs-lookup"><span data-stu-id="c5364-128">Build Add-Ins with SharePoint Framework</span></span>


## <a name="application-lifecycle-management"></a><span data-ttu-id="c5364-129">Application Lifecycle Management</span><span class="sxs-lookup"><span data-stu-id="c5364-129">Application Lifecycle Management</span></span>

- <span data-ttu-id="c5364-130">Optimierte Genehmigungsoberfläche: Sie müssen nicht mehr wissen, wer Ihr Mandantenadministrator ist</span><span class="sxs-lookup"><span data-stu-id="c5364-130">Streamlined approval experience: no need to know who your tenant admin is anymore</span></span>
    - <span data-ttu-id="c5364-131">Besitzer initiiert den Genehmigungsprozess</span><span class="sxs-lookup"><span data-stu-id="c5364-131">Owner initiates the approval process</span></span>
    - <span data-ttu-id="c5364-132">Mandantenadministrator wird automatisch benachrichtigt</span><span class="sxs-lookup"><span data-stu-id="c5364-132">Tenant admin gets automatically notified</span></span> 
    - <span data-ttu-id="c5364-133">Einstellungen zum Steuern der Standardoberfläche um den Genehmigungsprozess herum</span><span class="sxs-lookup"><span data-stu-id="c5364-133">Settings to control the default experience around approval process</span></span>


## <a name="developer-experience"></a><span data-ttu-id="c5364-134">Entwickleroberfläche</span><span class="sxs-lookup"><span data-stu-id="c5364-134">Developer Experience</span></span>
- <span data-ttu-id="c5364-135">SharePoint-Framework-Workbench 2.0: Entwicklungsgeschichte für SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="c5364-135">SharePoint Framework Workbench 2.0: Development story for SharePoint Framework Extensions</span></span>
- <span data-ttu-id="c5364-136">Toolkettenkomponenten</span><span class="sxs-lookup"><span data-stu-id="c5364-136">Tool Chain Components</span></span>
- <span data-ttu-id="c5364-137">Zusätzliche Yeoman-Vorlagen</span><span class="sxs-lookup"><span data-stu-id="c5364-137">Additional Yeoman Templates</span></span>

## <a name="already-shipped-capabilities"></a><span data-ttu-id="c5364-138">Bereits ausgeliefert Funktionen</span><span class="sxs-lookup"><span data-stu-id="c5364-138">Already shipped capabilities</span></span>

<span data-ttu-id="c5364-139">In den folgenden Kapiteln werden ältere Elemente auf der Roadmap-Seite erläutert, die bereits ausgeliefert wurden.</span><span class="sxs-lookup"><span data-stu-id="c5364-139">Following chapters are listing older items in the roadmap page, which have been already shipped.</span></span>

### <a name="asset-packaging"></a><span data-ttu-id="c5364-140">Verpacken von Objekten</span><span class="sxs-lookup"><span data-stu-id="c5364-140">Asset packaging</span></span>

- <span data-ttu-id="c5364-141">Automatisches CDN-Hosting für Code – Das JavaScript-Bundle wird im App-Paket verpackt, das dann automatisch in einer Bibliothek bereitgestellt wird, die auf dem Mandanten-Office 365-CDN gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="c5364-141">Automatic CDN hosting for code - Package JavaScript bundle into app package, which is automatically then deployed to a library that gets hosted on your tenant Office 365 CDN</span></span>

### <a name="alm-rest-apis"></a><span data-ttu-id="c5364-142">ALM-REST-APIs</span><span class="sxs-lookup"><span data-stu-id="c5364-142">ALM REST APIs</span></span>

- <span data-ttu-id="c5364-143">ALM-REST-APIs - Bereitstellen, Aktivieren, Löschen und Aktualisieren von Apps und Add-Ins</span><span class="sxs-lookup"><span data-stu-id="c5364-143">ALM REST APIs - Deploy, activate, delete and upgrade apps and add-ins</span></span>
- <span data-ttu-id="c5364-144">ALM-REST-APIs zielen darauf ab, *alles* aus dem App-Katalog zu unterstützen, einschließlich Add-Ins</span><span class="sxs-lookup"><span data-stu-id="c5364-144">ALM REST APIs targeted to support *everything* in the App Catalog, including add-ins</span></span>
- <span data-ttu-id="c5364-145">CSOM und PowerShell-Cmdlets als Initiative der Open-Source-Community</span><span class="sxs-lookup"><span data-stu-id="c5364-145">CSOM and PowerShell cmdlets released as an open source community initiative</span></span>

### <a name="javascript-embedding-support-jslink-user-custom-actions"></a><span data-ttu-id="c5364-146">Eingebettete JavaScript-Unterstützung (JSLink, benutzerdefinierte Benutzeraktionen)</span><span class="sxs-lookup"><span data-stu-id="c5364-146">JavaScript embedding support (JSLink, User Custom Actions)</span></span> 

- <span data-ttu-id="c5364-147">Dieselbe Toolkette und dasselbe Bereitstellungsmodell wie bei clientseitigen Webparts</span><span class="sxs-lookup"><span data-stu-id="c5364-147">The same tool chain and deployment model as client-side web parts</span></span>
- <span data-ttu-id="c5364-148">Leiten Sie von einer stark typisierten Basisklasse, wann immer möglich, ab, anstatt das Seiten-DOM direkt zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="c5364-148">Derive from a strongly typed base class wherever possible rather than manipulating the page DOM directly.</span></span>
- <span data-ttu-id="c5364-149">Moderne Erweiterungsverwendung mit modernen Benutzerumgebung ähnlich wie Benutzerdefinierte Aktionen und JS-Link in der klassischen Umgebung</span><span class="sxs-lookup"><span data-stu-id="c5364-149">Enable modern extension usage with modern experiences similar as Custom Actions and JS Link in classic experience</span></span>
- <span data-ttu-id="c5364-150">Arbeiten mit NoScript über Mandanten-App-Katalog</span><span class="sxs-lookup"><span data-stu-id="c5364-150">Work with NoScript via tenant app catalog</span></span>

### <a name="on-premises-support---sharepoint-2016-feature-pack-2"></a><span data-ttu-id="c5364-151">Lokale Unterstützung – SharePoint 2016 Feature Pack 2</span><span class="sxs-lookup"><span data-stu-id="c5364-151">On-premises support - Sharepoint 2016 Feature Pack 2</span></span>

- <span data-ttu-id="c5364-152">Bereitstellung als Teil des Feature Pack 2 für SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="c5364-152">Shipping as part of Feature Pack 2 for SharePoint 2016</span></span>
- <span data-ttu-id="c5364-153">Ähnliche Funktionen wie in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="c5364-153">Similar feature capabilities as in SharePoint Online</span></span>
- <span data-ttu-id="c5364-154">Ziel ist die Bereitstellung einer gemeinsamen Entwicklungsplattform, lokal und in der Cloud</span><span class="sxs-lookup"><span data-stu-id="c5364-154">Target is to provide common development platform across on-premises and the cloud</span></span>
- <span data-ttu-id="c5364-155">Nutzung der modernen Toolkette und von Open Soure für lokale Umgebungen</span><span class="sxs-lookup"><span data-stu-id="c5364-155">Leveraging modern toolchain and open source on on-premises environments</span></span>
- <span data-ttu-id="c5364-156">Abzielen auf SharePoint 2016-Version während des Kalenderjahrs 2017</span><span class="sxs-lookup"><span data-stu-id="c5364-156">Targeting SharePoint 2016 version during calendar year 2017</span></span>


## <a name="see-also"></a><span data-ttu-id="c5364-157">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="c5364-157">See also</span></span>
<span data-ttu-id="c5364-158">Verwenden Sie die folgenden Ressourcen, um über die neuen Versionen und Funktionen auf dem Laufenden zu bleiben, die für SharePoint Framework veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="c5364-158">Please use following resources to stay up to date on the new releases and capabilities being released for SharePoint Framework.</span></span>

* [<span data-ttu-id="c5364-159">dev.office.com-Blog</span><span class="sxs-lookup"><span data-stu-id="c5364-159">dev.office.com blog</span></span>](https://dev.office.com/blogs)
* [<span data-ttu-id="c5364-160">OfficeDev-Twitterkonto</span><span class="sxs-lookup"><span data-stu-id="c5364-160">OfficeDev Twitter account</span></span>](https://twitter.com/officedev)
