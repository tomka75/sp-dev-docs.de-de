---
title: SharePoint Framework-Roadmap
ms.date: 12/15/2017
ms.prod: sharepoint
ms.openlocfilehash: 23629009d1322634c7e5855e3e590694f4caed74
ms.sourcegitcommit: 6f2b3b5bd81c2de4f761e10ed5e2f0b9c3c485bf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sharepoint-framework-roadmap"></a><span data-ttu-id="08612-102">SharePoint-Framework-Roadmap</span><span class="sxs-lookup"><span data-stu-id="08612-102">SharePoint Framework roadmap</span></span>

<span data-ttu-id="08612-103">Die Erstveröffentlichung von SharePoint-Framework enthielt nur Unterstützung für clientseitige Webparts.</span><span class="sxs-lookup"><span data-stu-id="08612-103">First release of the SharePoint Framework contained only support for client-side web parts.</span></span> <span data-ttu-id="08612-104">Dies war jedoch nur der Beginn der Bereitstellung zusätzlicher moderner Anpassungsfunktionen für SharePoint.</span><span class="sxs-lookup"><span data-stu-id="08612-104">This was however just a start on the journey for providing additional modern customization capabilities to SharePoint.</span></span> <span data-ttu-id="08612-105">Im folgenden werden die wichtigsten Funktionen aufgeführt, die nach der Markteinführung veröffentlicht wurden.</span><span class="sxs-lookup"><span data-stu-id="08612-105">Here is a list of key capabilities released after initial General Availability.</span></span>

- [<span data-ttu-id="08612-106">Unterstützung für mandantenweite Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="08612-106">Tenant scoped deployment support</span></span>](./tenant-scoped-deployment.md)
- [<span data-ttu-id="08612-107">Lokale Unterstützung für SharePoint 2016 (Feature Pack 2)</span><span class="sxs-lookup"><span data-stu-id="08612-107">On-premises support for SharePoint 2016 (Feature Pack 2)</span></span>](./sharepoint-2016-support.md)
- [<span data-ttu-id="08612-108">SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="08612-108">SharePoint Framework Extensions</span></span>](./extensions/overview-extensions.md)
- [<span data-ttu-id="08612-109">Mandanteneigenschaften</span><span class="sxs-lookup"><span data-stu-id="08612-109">Tenant properties</span></span>](./tenant-properties.md)
- [<span data-ttu-id="08612-110">ALM-APIs für SPFx-Lösungen und -Add-Ins</span><span class="sxs-lookup"><span data-stu-id="08612-110">ALM APIs for SPFx solutions and add-ins</span></span>](../apis/alm-api-for-spfx-add-ins.md)
- <span data-ttu-id="08612-111">[Unterstützung für Office UI Fabric Core](((https://dev.office.com/blogs)/improved-support-for-office-ui-fabric-core))</span><span class="sxs-lookup"><span data-stu-id="08612-111">[Office UI Fabric Core support](((https://dev.office.com/blogs)/improved-support-for-office-ui-fabric-core))</span></span>
- [<span data-ttu-id="08612-112">Verpacken von Objekten und Websitesammlungs-App-Katalog</span><span class="sxs-lookup"><span data-stu-id="08612-112">Asset packaging and site collection app catalog</span></span>](../general-development/site-collection-app-catalog.md)


> [!NOTE]
> <span data-ttu-id="08612-113">Dies ist eine Liste von Bereichen, die von den SharePoint-Entwicklern abgearbeitet und untersucht werden.</span><span class="sxs-lookup"><span data-stu-id="08612-113">This is a list of areas which SharePoint engineering is having in the backlog and are looking into.</span></span> <span data-ttu-id="08612-114">Das bedeutet **NICHT**, dass all diese Bereiche auch wirklich bereitgestellt werden, wir bemühen uns jedoch, Elemente und Themen aus dieser Liste in den künftigen Versionen von SharePoint-Framework schrittweise zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="08612-114">This does **NOT** mean that all of them will be necessarily delivered, but we are looking for getting items and topics from this list gradually released with the future releases of SharePoint Framework.</span></span>

## <a name="general-improvements"></a><span data-ttu-id="08612-115">Allgemeine Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="08612-115">General improvements</span></span>

- <span data-ttu-id="08612-116">Einfacher Zugriff auf die Graph-API zum Zugreifen auf benutzerspezifische Informationen (GraphHttpClient in der Vorschau)</span><span class="sxs-lookup"><span data-stu-id="08612-116">Easy access to Graph API to access user specific information (GraphHttpClient in preview)</span></span>
- <span data-ttu-id="08612-117">Webhooks auf Website-Ebene</span><span class="sxs-lookup"><span data-stu-id="08612-117">Site level WebHooks</span></span>
- <span data-ttu-id="08612-118">Textabschnitt zum Store mit Unterstützung für SharePoint-Framework aktualisiert</span><span class="sxs-lookup"><span data-stu-id="08612-118">Updated 'store' story with SharePoint Framework support</span></span>

## <a name="client-side-web-parts-and-add-ins"></a><span data-ttu-id="08612-119">Clientseitige Webparts und Add-Ins</span><span class="sxs-lookup"><span data-stu-id="08612-119">Client-side web parts++ and add-ins</span></span>

- <span data-ttu-id="08612-120">Unterstützung für komplexere Szenarios und Interaktionen mit Webparts</span><span class="sxs-lookup"><span data-stu-id="08612-120">Supporting more complex scenarios and interactions with web parts</span></span>
    - <span data-ttu-id="08612-121">Kommunikation von Webpart zu Webpart</span><span class="sxs-lookup"><span data-stu-id="08612-121">Part-to-part communication</span></span>
    - <span data-ttu-id="08612-122">JS Framework-Isolierung</span><span class="sxs-lookup"><span data-stu-id="08612-122">JS Framework isolation</span></span>
    - <span data-ttu-id="08612-123">„Citizen Developer“-Modell für einfache Entwicklung</span><span class="sxs-lookup"><span data-stu-id="08612-123">"citizen developer" model for lightweight development</span></span>

- <span data-ttu-id="08612-124">Add-Ins für die moderne Welt: Ansprechendere Wiedergabe mit der neuen UX.</span><span class="sxs-lookup"><span data-stu-id="08612-124">Bring add-ins to the modern world: Let’s make them play nicer with the new UX.</span></span> 
    - <span data-ttu-id="08612-125">Azure AD-Registrierung</span><span class="sxs-lookup"><span data-stu-id="08612-125">Azure AD Registration</span></span>
    - <span data-ttu-id="08612-126">Systemeigene dynamische Unterstützung</span><span class="sxs-lookup"><span data-stu-id="08612-126">Native responsive support</span></span>
    - <span data-ttu-id="08612-127">Erstellen von Add-Ins mit SharePoint-Framework</span><span class="sxs-lookup"><span data-stu-id="08612-127">Build Add-Ins with SharePoint Framework</span></span>


## <a name="application-lifecycle-management"></a><span data-ttu-id="08612-128">Application Lifecycle Management</span><span class="sxs-lookup"><span data-stu-id="08612-128">Application Lifecycle Management</span></span>

- <span data-ttu-id="08612-129">Optimierte Genehmigungsoberfläche: Sie müssen nicht mehr wissen, wer Ihr Mandantenadministrator ist</span><span class="sxs-lookup"><span data-stu-id="08612-129">Streamlined approval experience: no need to know who your tenant admin is anymore</span></span>
    - <span data-ttu-id="08612-130">Besitzer initiiert den Genehmigungsprozess</span><span class="sxs-lookup"><span data-stu-id="08612-130">Owner initiate the approval process</span></span>
    - <span data-ttu-id="08612-131">Mandantenadministrator wird automatisch benachrichtigt</span><span class="sxs-lookup"><span data-stu-id="08612-131">Tenant admin gets automatically notified</span></span> 
    - <span data-ttu-id="08612-132">Einstellungen zum Steuern der Standardoberfläche um den Genehmigungsprozess herum</span><span class="sxs-lookup"><span data-stu-id="08612-132">Settings to control the default experience around approval process</span></span>


## <a name="developer-experience"></a><span data-ttu-id="08612-133">Entwickleroberfläche</span><span class="sxs-lookup"><span data-stu-id="08612-133">Developer Experience</span></span>
- <span data-ttu-id="08612-134">SharePoint-Framework-Workbench 2.0: Entwicklungsgeschichte für SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="08612-134">SharePoint Framework Workbench 2.0: Development story for SharePoint Framework Extensions</span></span>
- <span data-ttu-id="08612-135">Toolkettenkomponenten</span><span class="sxs-lookup"><span data-stu-id="08612-135">Tool Chain Components</span></span>
- <span data-ttu-id="08612-136">Zusätzliche Yeoman-Vorlagen</span><span class="sxs-lookup"><span data-stu-id="08612-136">Additional Yeoman Templates</span></span>

## <a name="already-shipped-capabilities"></a><span data-ttu-id="08612-137">Bereits ausgeliefert Funktionen</span><span class="sxs-lookup"><span data-stu-id="08612-137">Already shipped capabilities</span></span>

<span data-ttu-id="08612-138">In den folgenden Kapiteln werden ältere Elemente auf der Roadmap-Seite erläutert, die bereits ausgeliefert wurden.</span><span class="sxs-lookup"><span data-stu-id="08612-138">Following chapters are listing older items in the roadmap page, which have been already shipped.</span></span>

### <a name="asset-packaging"></a><span data-ttu-id="08612-139">Verpacken von Objekten</span><span class="sxs-lookup"><span data-stu-id="08612-139">Asset packaging</span></span>

- <span data-ttu-id="08612-140">Automatisches CDN-Hosting für Code – Das JavaScript-Bundle wird im App-Paket verpackt, das dann automatisch in einer Bibliothek bereitgestellt wird, die auf dem Mandanten-Office 365-CDN gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="08612-140">Package JavaScript bundle into app package, which is automatically then deployed to a library that gets hosted on your tenant Office 365 CDN</span></span>

### <a name="alm-rest-apis"></a><span data-ttu-id="08612-141">ALM-REST-APIs</span><span class="sxs-lookup"><span data-stu-id="08612-141">ALM REST APIs</span></span>

- <span data-ttu-id="08612-142">ALM-REST-APIs - Bereitstellen, Aktivieren, Löschen und Aktualisieren von Apps und Add-Ins</span><span class="sxs-lookup"><span data-stu-id="08612-142">ALM REST APIs - Deploy, activate, delete and upgrade apps and add-ins</span></span>
- <span data-ttu-id="08612-143">ALM-REST-APIs zielen darauf ab, *alles* aus dem App-Katalog zu unterstützen, einschließlich Add-Ins</span><span class="sxs-lookup"><span data-stu-id="08612-143">ALM REST APIs targeted to support *everything* in the App Catalog, including add-ins</span></span>
- <span data-ttu-id="08612-144">CSOM und PowerShell-Cmdlets als Initiative der Open-Source-Community</span><span class="sxs-lookup"><span data-stu-id="08612-144">CSOM and PowerShell cmdlets released as an open source community initiative</span></span>

### <a name="javascript-embedding-support-jslink-user-custom-actions"></a><span data-ttu-id="08612-145">Eingebettete JavaScript-Unterstützung (JSLink, benutzerdefinierte Benutzeraktionen)</span><span class="sxs-lookup"><span data-stu-id="08612-145">JavaScript embedding support (JSLink, User Custom Actions)</span></span> 

- <span data-ttu-id="08612-146">Dieselbe Toolkette und dasselbe Bereitstellungsmodell wie bei clientseitigen Webparts</span><span class="sxs-lookup"><span data-stu-id="08612-146">The same tool chain and deployment model as client-side web parts</span></span>
- <span data-ttu-id="08612-147">Leiten Sie von einer stark typisierten Basisklasse, wann immer möglich, ab, anstatt das Seiten-DOM direkt zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="08612-147">Derive from a strongly typed base class wherever possible rather than manipulating the page DOM directly.</span></span>
- <span data-ttu-id="08612-148">Moderne Erweiterungsverwendung mit modernen Benutzerumgebung ähnlich wie Benutzerdefinierte Aktionen und JS-Link in der klassischen Umgebung</span><span class="sxs-lookup"><span data-stu-id="08612-148">Enable modern extension usage with modern experiences similar as Custom Actions and JS Link in classic experience</span></span>
- <span data-ttu-id="08612-149">Arbeiten mit NoScript über Mandanten-App-Katalog</span><span class="sxs-lookup"><span data-stu-id="08612-149">Work with NoScript via tenant app catalog</span></span>

### <a name="on-premises-support---sharepoint-2016-feature-pack-2"></a><span data-ttu-id="08612-150">Lokale Unterstützung – SharePoint 2016 Feature Pack 2</span><span class="sxs-lookup"><span data-stu-id="08612-150">On-premises support - Sharepoint 2016 Feature Pack 2</span></span>

- <span data-ttu-id="08612-151">Bereitstellung als Teil des Feature Pack 2 für SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="08612-151">Shipping as part of Feature Pack 2 for SharePoint 2016</span></span>
- <span data-ttu-id="08612-152">Ähnliche Funktionen wie in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="08612-152">Similar feature capabilities as in SharePoint Online</span></span>
- <span data-ttu-id="08612-153">Ziel ist die Bereitstellung einer gemeinsamen Entwicklungsplattform, lokal und in der Cloud</span><span class="sxs-lookup"><span data-stu-id="08612-153">Target is to provide common development platform across on-premises and the cloud</span></span>
- <span data-ttu-id="08612-154">Nutzung der modernen Toolkette und von Open Soure für lokale Umgebungen</span><span class="sxs-lookup"><span data-stu-id="08612-154">Leveraging modern toolchain and open source on on-premises environments</span></span>
- <span data-ttu-id="08612-155">Abzielen auf SharePoint 2016-Version während des Kalenderjahrs 2017</span><span class="sxs-lookup"><span data-stu-id="08612-155">Targeting SharePoint 2016 version during calendar year 2017</span></span>


## <a name="see-also"></a><span data-ttu-id="08612-156">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="08612-156">See also</span></span>
<span data-ttu-id="08612-157">Verwenden Sie die folgenden Ressourcen, um über die neuen Versionen und Funktionen auf dem Laufenden zu bleiben, die für SharePoint Framework veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="08612-157">Please use following resources to stay up to date on the new releases and capabilities being released for SharePoint Framework.</span></span>

* <span data-ttu-id="08612-158">[dev.office.com-Blog](https://dev.office.com/blogs)</span><span class="sxs-lookup"><span data-stu-id="08612-158">[dev.office.com blog](https://dev.office.com/blogs)</span></span>
* <span data-ttu-id="08612-159">[OfficeDev-Twitterkonto](https://twitter.com/officedev)</span><span class="sxs-lookup"><span data-stu-id="08612-159">[OfficeDev Twitter account](https://twitter.com/officedev)</span></span>
