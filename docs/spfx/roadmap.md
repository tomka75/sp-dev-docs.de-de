---
title: SharePoint Framework-Roadmap
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: a5097e0f7d465ab00c5c7a76a8ee78e10f737d7d
ms.sourcegitcommit: 11d9185437fc819ab41421c0f4fe06aa300b9d28
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/25/2017
---
# <a name="sharepoint-framework-roadmap"></a><span data-ttu-id="c21e1-102">SharePoint-Framework-Roadmap</span><span class="sxs-lookup"><span data-stu-id="c21e1-102">SharePoint Framework roadmap</span></span>

<span data-ttu-id="c21e1-103">Die Erstveröffentlichung von SharePoint-Framework enthielt nur Unterstützung für clientseitige Webparts.</span><span class="sxs-lookup"><span data-stu-id="c21e1-103">First release of the SharePoint Framework contained only support for client-side web parts.</span></span> <span data-ttu-id="c21e1-104">Dies war jedoch nur der Beginn der Bereitstellung zusätzlicher moderner Anpassungsfunktionen für SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c21e1-104">This was however just a start on the journey for providing additional modern customization capabilities to SharePoint.</span></span> <span data-ttu-id="c21e1-105">Im folgenden werden die wichtigsten Funktionen aufgeführt, die nach der Markteinführung veröffentlicht wurden.</span><span class="sxs-lookup"><span data-stu-id="c21e1-105">Here is a list of key capabilities released after initial General Availability.</span></span>

- [<span data-ttu-id="c21e1-106">Unterstützung für mandantenweite Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="c21e1-106">Tenant scoped deployment support</span></span>](./tenant-scoped-deployment.md)
- [<span data-ttu-id="c21e1-107">Lokale Unterstützung für SharePoint 2016 (Feature Pack 2)</span><span class="sxs-lookup"><span data-stu-id="c21e1-107">On-premises support for SharePoint 2016 (Feature Pack 2)</span></span>](./sharepoint-2016-support.md)
- [<span data-ttu-id="c21e1-108">SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="c21e1-108">Getting started with SharePoint Framework Extensions</span></span>](./extensions/overview-extensions.md)
- [<span data-ttu-id="c21e1-109">Mandanteneigenschaften</span><span class="sxs-lookup"><span data-stu-id="c21e1-109">Tenant properties</span></span>](./tenant-properties.md)


> [!NOTE]
> <span data-ttu-id="c21e1-110">Dies ist eine Liste von Bereichen, die von den SharePoint-Entwicklern abgearbeitet und untersucht werden.</span><span class="sxs-lookup"><span data-stu-id="c21e1-110">This is a list of areas which SharePoint engineering is having in the backlog and are looking into.</span></span> <span data-ttu-id="c21e1-111">Das bedeutet **NICHT**, dass all diese Bereiche auch wirklich bereitgestellt werden, wir bemühen uns jedoch, Elemente und Themen aus dieser Liste in den künftigen Versionen von SharePoint-Framework schrittweise zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="c21e1-111">Notice. This is a list of areas which SharePoint engineering is having in the backlog and are looking into. This does **NOT** mean that all of them will be necessarily delivered, but we are looking for getting items and topics from this list gradually released with the future releases of SharePoint Framework.</span></span>

## <a name="general-improvements"></a><span data-ttu-id="c21e1-112">Allgemeine Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="c21e1-112">General improvements</span></span>

- <span data-ttu-id="c21e1-113">Einfacher Zugriff auf die Graph-API zum Zugreifen auf benutzerspezifische Informationen (GraphHttpClient in der Vorschau)</span><span class="sxs-lookup"><span data-stu-id="c21e1-113">Easy access to Graph API to access user specific information (GraphHttpClient in dev preview)</span></span>
- <span data-ttu-id="c21e1-114">Websitesammlungs-App-Katalog mit Steuerung auf Mandantenebene für eine einfachere Bereitstellung von Lösungen – Ende 2017</span><span class="sxs-lookup"><span data-stu-id="c21e1-114">Site collection app catalog with tenant level control for enabling easier solution deployed</span></span>
- <span data-ttu-id="c21e1-115">Webhooks auf Website-Ebene</span><span class="sxs-lookup"><span data-stu-id="c21e1-115">Site level WebHooks</span></span>
- <span data-ttu-id="c21e1-116">Unterstützung für Office-UI-Fabric Core</span><span class="sxs-lookup"><span data-stu-id="c21e1-116">Office UI Fabric Core</span></span>

## <a name="client-side-web-parts-and-add-ins"></a><span data-ttu-id="c21e1-117">Clientseitige Webparts und Add-Ins</span><span class="sxs-lookup"><span data-stu-id="c21e1-117">Client-side web parts++ and add-ins</span></span>

- <span data-ttu-id="c21e1-118">Unterstützung für komplexere Szenarios und Interaktionen mit Webparts</span><span class="sxs-lookup"><span data-stu-id="c21e1-118">Supporting more complex scenarios and interactions with web parts</span></span>
    - <span data-ttu-id="c21e1-119">Kommunikation von Webpart zu Webpart</span><span class="sxs-lookup"><span data-stu-id="c21e1-119">Part-to-part communication</span></span>
    - <span data-ttu-id="c21e1-120">JS Framework-Isolierung</span><span class="sxs-lookup"><span data-stu-id="c21e1-120">JS Framework isolation</span></span>
    - <span data-ttu-id="c21e1-121">„Citizen Developer“-Modell für einfache Entwicklung</span><span class="sxs-lookup"><span data-stu-id="c21e1-121">"citizen developer" model for lightweight development</span></span>

- <span data-ttu-id="c21e1-122">Add-Ins für die moderne Welt: Ansprechendere Wiedergabe mit der neuen UX.</span><span class="sxs-lookup"><span data-stu-id="c21e1-122">Bring add-ins to the modern world: Let’s make them play nicer with the new UX.</span></span> 
    - <span data-ttu-id="c21e1-123">Azure AD-Registrierung</span><span class="sxs-lookup"><span data-stu-id="c21e1-123">Azure AD Registration</span></span>
    - <span data-ttu-id="c21e1-124">Systemeigene dynamische Unterstützung</span><span class="sxs-lookup"><span data-stu-id="c21e1-124">Native responsive support</span></span>
    - <span data-ttu-id="c21e1-125">Erstellen von Add-Ins mit SharePoint-Framework</span><span class="sxs-lookup"><span data-stu-id="c21e1-125">Build Add-Ins with SharePoint Framework</span></span>


## <a name="application-lifecycle-management"></a><span data-ttu-id="c21e1-126">Application Lifecycle Management</span><span class="sxs-lookup"><span data-stu-id="c21e1-126">Application Lifecycle Management</span></span>

- <span data-ttu-id="c21e1-127">Optimierte Genehmigungsoberfläche: Sie müssen nicht mehr wissen, wer Ihr Mandantenadministrator ist</span><span class="sxs-lookup"><span data-stu-id="c21e1-127">Streamlined approval experience: no need to know who your tenant admin is anymore</span></span>
    - <span data-ttu-id="c21e1-128">Besitzer initiiert den Genehmigungsprozess</span><span class="sxs-lookup"><span data-stu-id="c21e1-128">Owner initiate the approval process</span></span>
    - <span data-ttu-id="c21e1-129">Mandantenadministrator wird automatisch benachrichtigt</span><span class="sxs-lookup"><span data-stu-id="c21e1-129">Tenant admin gets automatically notified</span></span> 
    - <span data-ttu-id="c21e1-130">Einstellungen zum Steuern der Standardoberfläche um den Genehmigungsprozess herum</span><span class="sxs-lookup"><span data-stu-id="c21e1-130">Settings to control the default experience around approval process</span></span>

- <span data-ttu-id="c21e1-131">ALM-REST-APIs - Bereitstellen, Aktivieren, Löschen und Aktualisieren von Apps und Add-Ins</span><span class="sxs-lookup"><span data-stu-id="c21e1-131">ALM REST APIs - Deploy, activate, delete and upgrade apps and add-ins</span></span>
- <span data-ttu-id="c21e1-132">ALM-REST-APIs zielen darauf ab, *alles* aus dem App-Katalog zu unterstützen, einschließlich Add-Ins</span><span class="sxs-lookup"><span data-stu-id="c21e1-132">ALM REST APIs targeted to support *everything* in the App Catalog, including add-ins</span></span>
- <span data-ttu-id="c21e1-133">Automatisches CDN-Hosting für Code</span><span class="sxs-lookup"><span data-stu-id="c21e1-133">Automatic CDN hosting for code</span></span>
    - <span data-ttu-id="c21e1-134">Das JavaScript-Bundle wird im App-Paket verpackt, das dann automatisch in einer Bibliothek bereitgestellt wird, die auf dem Mandanten-Office 365-CDN gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="c21e1-134">Package JavaScript bundle into app package, which is automatically then deployed to a library that gets hosted on your tenant Office 365 CDN</span></span>


## <a name="developer-experience"></a><span data-ttu-id="c21e1-135">Entwickleroberfläche</span><span class="sxs-lookup"><span data-stu-id="c21e1-135">Developer Experience</span></span>
- <span data-ttu-id="c21e1-136">SharePoint-Framework-Workbench 2.0: Entwicklungsgeschichte für SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="c21e1-136">SharePoint Framework Workbench 2.0: Development story for SharePoint Framework Extensions</span></span>
- <span data-ttu-id="c21e1-137">Toolkettenkomponenten</span><span class="sxs-lookup"><span data-stu-id="c21e1-137">Tool Chain Components</span></span>
- <span data-ttu-id="c21e1-138">Zusätzliche Yeoman-Vorlagen</span><span class="sxs-lookup"><span data-stu-id="c21e1-138">Additional Yeoman Templates</span></span>

## <a name="already-shipped-capabilities"></a><span data-ttu-id="c21e1-139">Bereits ausgeliefert Funktionen</span><span class="sxs-lookup"><span data-stu-id="c21e1-139">Already shipped capabilities</span></span>

<span data-ttu-id="c21e1-140">In den folgenden Kapiteln werden ältere Elemente auf der Roadmap-Seite erläutert, die bereits ausgeliefert wurden.</span><span class="sxs-lookup"><span data-stu-id="c21e1-140">Following chapters are listing older items in the roadmap page, which have been already shipped.</span></span>

### <a name="javascript-embedding-support-jslink-user-custom-actions"></a><span data-ttu-id="c21e1-141">Eingebettete JavaScript-Unterstützung (JSLink, benutzerdefinierte Benutzeraktionen)</span><span class="sxs-lookup"><span data-stu-id="c21e1-141">JavaScript embedding support (JSLink, User Custom Actions)</span></span> 

- <span data-ttu-id="c21e1-142">Dieselbe Toolkette und dasselbe Bereitstellungsmodell wie bei clientseitigen Webparts</span><span class="sxs-lookup"><span data-stu-id="c21e1-142">The same tool chain and deployment model as client-side web parts</span></span>
- <span data-ttu-id="c21e1-143">Leiten Sie von einer stark typisierten Basisklasse, wann immer möglich, ab, anstatt das Seiten-DOM direkt zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="c21e1-143">Derive from a strongly typed base class wherever possible rather than manipulating the page DOM directly.</span></span>
- <span data-ttu-id="c21e1-144">Moderne Erweiterungsverwendung mit modernen Benutzerumgebung ähnlich wie Benutzerdefinierte Aktionen und JS-Link in der klassischen Umgebung</span><span class="sxs-lookup"><span data-stu-id="c21e1-144">Enable modern extension usage with modern experiences similar as Custom Actions and JS Link in classic experience</span></span>
- <span data-ttu-id="c21e1-145">Arbeiten mit NoScript über Mandanten-App-Katalog</span><span class="sxs-lookup"><span data-stu-id="c21e1-145">Work with NoScript via tenant app catalog</span></span>

### <a name="on-premises-support---sharepoint-2016-feature-pack-2"></a><span data-ttu-id="c21e1-146">Lokale Unterstützung – SharePoint 2016 Feature Pack 2</span><span class="sxs-lookup"><span data-stu-id="c21e1-146">On-premises support - Sharepoint 2016 Feature Pack 2</span></span>

- <span data-ttu-id="c21e1-147">Bereitstellung als Teil des Feature Pack 2 für SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="c21e1-147">Shipping as part of Feature Pack 2 for SharePoint 2016</span></span>
- <span data-ttu-id="c21e1-148">Ähnliche Funktionen wie in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="c21e1-148">Similar feature capabilities as in SharePoint Online</span></span>
- <span data-ttu-id="c21e1-149">Ziel ist die Bereitstellung einer gemeinsamen Entwicklungsplattform, lokal und in der Cloud</span><span class="sxs-lookup"><span data-stu-id="c21e1-149">Target is to provide common development platform across on-premises and the cloud</span></span>
- <span data-ttu-id="c21e1-150">Nutzung der modernen Toolkette und von Open Soure für lokale Umgebungen</span><span class="sxs-lookup"><span data-stu-id="c21e1-150">Leveraging modern toolchain and open source on on-premises environments</span></span>
- <span data-ttu-id="c21e1-151">Abzielen auf SharePoint 2016-Version während des Kalenderjahrs 2017</span><span class="sxs-lookup"><span data-stu-id="c21e1-151">Targeting SharePoint 2016 version during calendar year 2017</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c21e1-152">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="c21e1-152">Additional resources</span></span>
<span data-ttu-id="c21e1-153">Verwenden Sie die folgenden Ressourcen, um über die neuen Versionen und Funktionen auf dem Laufenden zu bleiben, die für SharePoint Framework veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="c21e1-153">Please use following resources to stay up to date on the new releases and capabilities being released for SharePoint Framework.</span></span>

* [<span data-ttu-id="c21e1-154">dev.office.com-Blog</span><span class="sxs-lookup"><span data-stu-id="c21e1-154">dev.office.com blog</span></span>](https://dev.office.com/blogs)
* [<span data-ttu-id="c21e1-155">OfficeDev-Twitterkonto</span><span class="sxs-lookup"><span data-stu-id="c21e1-155">OfficeDev Twitter account</span></span>](https://twitter.com/officedev)
