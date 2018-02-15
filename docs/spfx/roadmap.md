---
title: SharePoint-Framework-Roadmap
description: "Wichtige moderne Anpassungsfunktionen nach der Version mit allgemeiner Verfügbarkeit veröffentlicht"
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: 8b50c0a6ec81f27001d9abafc5e8a9e0a2fa957e
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="sharepoint-framework-roadmap"></a><span data-ttu-id="9a887-103">SharePoint-Framework-Roadmap</span><span class="sxs-lookup"><span data-stu-id="9a887-103">SharePoint Framework roadmap</span></span>

<span data-ttu-id="9a887-104">Die Erstveröffentlichung von SharePoint-Framework enthielt nur Unterstützung für clientseitige Webparts.</span><span class="sxs-lookup"><span data-stu-id="9a887-104">First release of the SharePoint Framework contained only support for client-side web parts.</span></span> <span data-ttu-id="9a887-105">Dies war jedoch nur der Beginn der Bereitstellung zusätzlicher moderner Anpassungsfunktionen für SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9a887-105">This was however just a start on the journey for providing additional modern customization capabilities to SharePoint.</span></span> <span data-ttu-id="9a887-106">Im Folgenden werden die wichtigsten Funktionen aufgeführt, die nach der Version mit allgemeiner Verfügbarkeit veröffentlicht wurden:</span><span class="sxs-lookup"><span data-stu-id="9a887-106">Here is a list of key capabilities released after initial General Availability.</span></span>

- [<span data-ttu-id="9a887-107">Unterstützung für mandantenweite Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="9a887-107">Tenant-scoped deployment support</span></span>](./tenant-scoped-deployment.md)
- [<span data-ttu-id="9a887-108">Lokale Unterstützung für SharePoint 2016 (Feature Pack 2)</span><span class="sxs-lookup"><span data-stu-id="9a887-108">On-premises support for SharePoint 2016 (Feature Pack 2)</span></span>](./sharepoint-2016-support.md)
- [<span data-ttu-id="9a887-109">SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="9a887-109">SharePoint Framework Extensions</span></span>](./extensions/overview-extensions.md)
- [<span data-ttu-id="9a887-110">Mandanteneigenschaften</span><span class="sxs-lookup"><span data-stu-id="9a887-110">Tenant properties</span></span>](./tenant-properties.md)
- [<span data-ttu-id="9a887-111">Application Lifecycle Management (ALM)-APIs für SPFx Lösungen und Add-Ins</span><span class="sxs-lookup"><span data-stu-id="9a887-111">Application Lifecycle Management (ALM) APIs for SPFx solutions and add-ins</span></span>](../apis/alm-api-for-spfx-add-ins.md)
- [<span data-ttu-id="9a887-112">Unterstützung für Office UI Fabric Core</span><span class="sxs-lookup"><span data-stu-id="9a887-112">Office UI Fabric Core support</span></span>](https://dev.office.com/blogs/improved-support-for-office-ui-fabric-core)
- [<span data-ttu-id="9a887-113">Verpacken von Objekten und Websitesammlungs-App-Katalog</span><span class="sxs-lookup"><span data-stu-id="9a887-113">Asset packaging and site collection app catalog</span></span>](../general-development/site-collection-app-catalog.md)


> [!NOTE]
> <span data-ttu-id="9a887-114">Dies ist eine Liste von Bereichen, die von den SharePoint-Entwicklern abgearbeitet und untersucht werden.</span><span class="sxs-lookup"><span data-stu-id="9a887-114">This is a list of areas which SharePoint engineering is having in the backlog and are looking into.</span></span> <span data-ttu-id="9a887-115">Das bedeutet **NICHT**, dass all diese Bereiche tatsächlich bereitgestellt werden, wir bemühen uns jedoch, Elemente und Themen aus dieser Liste in den künftigen Versionen von SharePoint-Framework schrittweise zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="9a887-115">This does **NOT** mean that all of them will be necessarily delivered, but we are looking for getting items and topics from this list gradually released with the future releases of SharePoint Framework.</span></span>

## <a name="general-improvements"></a><span data-ttu-id="9a887-116">Allgemeine Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="9a887-116">General improvements</span></span>

- <span data-ttu-id="9a887-117">Einfacher Zugriff auf die Graph-API zum Zugreifen auf benutzerspezifische Informationen (GraphHttpClient in der Vorschau)</span><span class="sxs-lookup"><span data-stu-id="9a887-117">Easy access to Graph API to access user specific information (GraphHttpClient in preview)</span></span>
- <span data-ttu-id="9a887-118">Webhooks auf Website-Ebene</span><span class="sxs-lookup"><span data-stu-id="9a887-118">Site level WebHooks</span></span>
- <span data-ttu-id="9a887-119">Textabschnitt zum Store mit Unterstützung für SharePoint-Framework aktualisiert</span><span class="sxs-lookup"><span data-stu-id="9a887-119">Updated 'store' story with SharePoint Framework support</span></span>
- <span data-ttu-id="9a887-120">Textabschnitt zum Store für SharePoint-Framework-Lösungen mit einfachem Vertriebskanal für ISVs</span><span class="sxs-lookup"><span data-stu-id="9a887-120">'Store' story for SharePoint Framework solutions with easy distribution channel for ISVs</span></span> 

## <a name="client-side-web-parts-and-add-ins"></a><span data-ttu-id="9a887-121">Clientseitige Webparts und Add-Ins</span><span class="sxs-lookup"><span data-stu-id="9a887-121">Client-side web parts++ and add-ins</span></span>

- <span data-ttu-id="9a887-122">Unterstützung für komplexere Szenarios und Interaktionen mit Webparts</span><span class="sxs-lookup"><span data-stu-id="9a887-122">Supporting more complex scenarios and interactions with web parts</span></span>
    - <span data-ttu-id="9a887-123">Kommunikation von Webpart zu Webpart</span><span class="sxs-lookup"><span data-stu-id="9a887-123">Part-to-part communication</span></span>
    - <span data-ttu-id="9a887-124">JavaScript-Framework-Isolierung</span><span class="sxs-lookup"><span data-stu-id="9a887-124">JavaScript Framework isolation</span></span>
    - <span data-ttu-id="9a887-125">„Citizen Developer“-Modell für einfache Entwicklung</span><span class="sxs-lookup"><span data-stu-id="9a887-125">"citizen developer" model for lightweight development</span></span>

- <span data-ttu-id="9a887-126">Add-Ins für die moderne Welt: Ansprechendere Wiedergabe mit der neuen UX.</span><span class="sxs-lookup"><span data-stu-id="9a887-126">Bring add-ins to the modern world: Let’s make them play nicer with the new UX.</span></span>
    - <span data-ttu-id="9a887-127">Azure AD-Registrierung</span><span class="sxs-lookup"><span data-stu-id="9a887-127">Azure AD Registration</span></span>
    - <span data-ttu-id="9a887-128">Native, reaktionsschnelle Unterstützung</span><span class="sxs-lookup"><span data-stu-id="9a887-128">Native responsive support</span></span>
    - <span data-ttu-id="9a887-129">Erstellen von Add-Ins mit SharePoint-Framework</span><span class="sxs-lookup"><span data-stu-id="9a887-129">Build Add-Ins with SharePoint Framework</span></span>


## <a name="application-lifecycle-management"></a><span data-ttu-id="9a887-130">Application Lifecycle Management</span><span class="sxs-lookup"><span data-stu-id="9a887-130">Application Lifecycle Management</span></span>

- <span data-ttu-id="9a887-131">Optimierte Genehmigungsoberfläche: Sie müssen nicht mehr wissen, wer Ihr Mandantenadministrator ist.</span><span class="sxs-lookup"><span data-stu-id="9a887-131">Streamlined approval experience: no need to know who your tenant admin is anymore</span></span>
    - <span data-ttu-id="9a887-132">Besitzer initiiert den Genehmigungsprozess.</span><span class="sxs-lookup"><span data-stu-id="9a887-132">Owner initiates the approval process</span></span>
    - <span data-ttu-id="9a887-133">Mandantenadministrator wird automatisch benachrichtigt.</span><span class="sxs-lookup"><span data-stu-id="9a887-133">Tenant admin gets automatically notified</span></span>
    - <span data-ttu-id="9a887-134">Einstellungen zum Steuern der Standardoberfläche um den Genehmigungsprozess herum.</span><span class="sxs-lookup"><span data-stu-id="9a887-134">Settings to control the default experience around approval process</span></span>


## <a name="developer-experience"></a><span data-ttu-id="9a887-135">Entwickleroberfläche</span><span class="sxs-lookup"><span data-stu-id="9a887-135">Developer Experience</span></span>

- <span data-ttu-id="9a887-136">SharePoint-Framework-Workbench 2.0: Entwicklungsgeschichte für SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="9a887-136">SharePoint Framework Workbench 2.0: Development story for SharePoint Framework Extensions</span></span>
- <span data-ttu-id="9a887-137">Komponenten der Toolkette</span><span class="sxs-lookup"><span data-stu-id="9a887-137">Toolchain components</span></span>
- <span data-ttu-id="9a887-138">Zusätzliche Yeoman-Vorlagen</span><span class="sxs-lookup"><span data-stu-id="9a887-138">Additional Yeoman Templates</span></span>

## <a name="already-shipped-capabilities"></a><span data-ttu-id="9a887-139">Bereits ausgeliefert Funktionen</span><span class="sxs-lookup"><span data-stu-id="9a887-139">Already shipped capabilities</span></span>

<span data-ttu-id="9a887-140">In den folgenden Abschnitten werden ältere Elemente aufgeführt, die bereits ausgeliefert wurden.</span><span class="sxs-lookup"><span data-stu-id="9a887-140">The following sections list older items that have already shipped.</span></span>

### <a name="asset-packaging"></a><span data-ttu-id="9a887-141">Verpacken von Objekten</span><span class="sxs-lookup"><span data-stu-id="9a887-141">Asset packaging</span></span>

- <span data-ttu-id="9a887-142">Automatisches CDN-Hosting für Code</span><span class="sxs-lookup"><span data-stu-id="9a887-142">Automatic CDN hosting for code</span></span> <span data-ttu-id="9a887-143">Das JavaScript-Bundle wird im App-Paket verpackt, das automatisch in einer Bibliothek bereitgestellt wird, die auf dem Mandanten-Office 365-CDN gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="9a887-143">Package JavaScript bundle into app package, which is automatically then deployed to a library that gets hosted on your tenant Office 365 CDN</span></span>

### <a name="alm-rest-apis"></a><span data-ttu-id="9a887-144">ALM-REST-APIs</span><span class="sxs-lookup"><span data-stu-id="9a887-144">ALM REST APIs</span></span>

- <span data-ttu-id="9a887-145">ALM-REST-APIs.</span><span class="sxs-lookup"><span data-stu-id="9a887-145">ALM REST APIs</span></span> <span data-ttu-id="9a887-146">Bereitstellen, Aktivieren, Löschen und Aktualisieren von Apps und Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="9a887-146">ALM REST APIs - Deploy, activate, delete and upgrade apps and add-ins</span></span>
- <span data-ttu-id="9a887-147">ALM-REST-APIs zielen darauf ab, *alles* aus dem App-Katalog zu unterstützen, einschließlich Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="9a887-147">ALM REST APIs targeted to support *everything* in the App Catalog, including add-ins</span></span>
- <span data-ttu-id="9a887-148">CSOM- und PowerShell-Cmdlets als Initiative der Open-Source-Community veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="9a887-148">CSOM and PowerShell cmdlets released as an open source community initiative</span></span>

### <a name="javascript-embedding-support-jslink-user-custom-actions"></a><span data-ttu-id="9a887-149">Eingebettete JavaScript-Unterstützung (JSLink, benutzerdefinierte Benutzeraktionen)</span><span class="sxs-lookup"><span data-stu-id="9a887-149">JavaScript embedding support (JSLink, User Custom Actions)</span></span> 

- <span data-ttu-id="9a887-150">Dieselbe Toolkette und dasselbe Bereitstellungsmodell wie bei clientseitigen Webparts</span><span class="sxs-lookup"><span data-stu-id="9a887-150">The same tool chain and deployment model as client-side web parts</span></span>
- <span data-ttu-id="9a887-151">Ableitung von einer stark typisierten Basisklasse wann immer möglich, anstelle der direkten Bearbeitung des Seiten-DOM</span><span class="sxs-lookup"><span data-stu-id="9a887-151">Derive from a strongly typed base class wherever possible rather than manipulating the page DOM directly.</span></span>
- <span data-ttu-id="9a887-152">Moderne Erweiterungsverwendung mit modernen Benutzerumgebungen ähnlich wie benutzerdefinierte Aktionen und JS-Link in der klassischen Umgebung</span><span class="sxs-lookup"><span data-stu-id="9a887-152">Enable modern extension usage with modern experiences similar as Custom Actions and JS Link in classic experience</span></span>
- <span data-ttu-id="9a887-153">Arbeiten mit NoScript über Mandanten-App-Katalog</span><span class="sxs-lookup"><span data-stu-id="9a887-153">Work with NoScript via tenant app catalog</span></span>

### <a name="on-premises-support---sharepoint-2016-feature-pack-2"></a><span data-ttu-id="9a887-154">Lokale Unterstützung – SharePoint 2016 Feature Pack 2</span><span class="sxs-lookup"><span data-stu-id="9a887-154">On-premises support - Sharepoint 2016 Feature Pack 2</span></span>

- <span data-ttu-id="9a887-155">Bereitstellung als Teil des Feature Pack 2 für SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="9a887-155">Shipping as part of Feature Pack 2 for SharePoint 2016</span></span>
- <span data-ttu-id="9a887-156">Ähnliche Funktionen wie in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="9a887-156">Similar feature capabilities as in SharePoint Online</span></span>
- <span data-ttu-id="9a887-157">Ziel ist die Bereitstellung einer gemeinsamen Entwicklungsplattform, lokal und in der Cloud</span><span class="sxs-lookup"><span data-stu-id="9a887-157">Target is to provide common development platform across on-premises and the cloud</span></span>
- <span data-ttu-id="9a887-158">Nutzung der modernen Toolkette und von Open Soure für lokale Umgebungen</span><span class="sxs-lookup"><span data-stu-id="9a887-158">Leveraging modern toolchain and open source on on-premises environments</span></span>
- <span data-ttu-id="9a887-159">Abzielen auf SharePoint 2016-Version während des Kalenderjahrs 2017</span><span class="sxs-lookup"><span data-stu-id="9a887-159">Targeting SharePoint 2016 version during calendar year 2017</span></span>


## <a name="see-also"></a><span data-ttu-id="9a887-160">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="9a887-160">See also</span></span>

- [<span data-ttu-id="9a887-161">dev.office.com-Blog</span><span class="sxs-lookup"><span data-stu-id="9a887-161">dev.office.com blog</span></span>](https://dev.office.com/blogs)
- [<span data-ttu-id="9a887-162">OfficeDev-Twitterkonto</span><span class="sxs-lookup"><span data-stu-id="9a887-162">OfficeDev Twitter account</span></span>](https://twitter.com/officedev)
- [<span data-ttu-id="9a887-163">Übersicht über das SharePoint-Framework</span><span class="sxs-lookup"><span data-stu-id="9a887-163">SharePoint Framework Extensions Overview</span></span>](sharepoint-framework-overview.md)
