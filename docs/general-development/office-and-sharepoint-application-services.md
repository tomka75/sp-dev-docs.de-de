---
title: Office 2013- und SharePoint-Anwendungsdienste
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f962922c-2967-492f-9a89-5ad10a1a6dd3
ms.openlocfilehash: d976ee840824abe4a12e7cacc28b1cf46cb11c94
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="office-2013-and-sharepoint-application-services"></a><span data-ttu-id="6d067-102">Office 2013- und SharePoint-Anwendungsdienste</span><span class="sxs-lookup"><span data-stu-id="6d067-102">Office 2013 and SharePoint application services</span></span>
<span data-ttu-id="6d067-103">Erfahren Sie mehr über Access Services, Excel Services, Dienst für maschinelle Übersetzung, PerformancePoint-Dienste, PowerPoint Automation Services, Visio Services und Word Automation Services.</span><span class="sxs-lookup"><span data-stu-id="6d067-103">Learn about Access Services, Excel Services, Machine Translation Service, PerformancePoint Services, PowerPoint Automation Services, Visio Services, and Word Automation Services.</span></span>
## <a name="overview-and-usage-scenarios-for-office-and-sharepoint-services-in-sharepoint"></a><span data-ttu-id="6d067-104">Überblick und Nutzungsszenarien für Office und SharePoint-Dienste in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d067-104">Overview and usage scenarios for Office and SharePoint services in SharePoint</span></span>
<span data-ttu-id="6d067-105"><a name="bkmk_servicesOverview"> </a></span><span class="sxs-lookup"><span data-stu-id="6d067-105"></span></span>

<span data-ttu-id="6d067-p101">Office- und SharePoint-Dienste werden auf einzelnen Anwendungsservern in der Farm ausgeführt und bieten eine Vielzahl von Funktionen. Die Dienste, die in diesem Abschnitt beschrieben werden, stellen Funktionen für die folgenden Szenarien bereit:</span><span class="sxs-lookup"><span data-stu-id="6d067-p101">Office and SharePoint services run on individual application servers in the farm and provide a wide range of functionality. The services that are described in this section provide functionality across the following scenarios:</span></span>
  
    
    

- <span data-ttu-id="6d067-108">**Business Intelligence (BI) und Einblicke** ermöglichen Benutzern, Informationen zu ihrer Arbeit oder ihrem Unternehmen zu finden, zu analysieren und freizugeben.</span><span class="sxs-lookup"><span data-stu-id="6d067-108">**Business intelligence (BI) and Insights** enable people to find, analyze, and share information about their work or business.</span></span>
    
  
- <span data-ttu-id="6d067-109">**Einfache Apps** ermöglichen Benutzern die Erstellung grundlegender Apps, die einen zuverlässigen Sicherungsspeicher enthalten.</span><span class="sxs-lookup"><span data-stu-id="6d067-109">**Simple apps** let users create basic apps that contain a reliable backing store.</span></span>
    
  
- <span data-ttu-id="6d067-110">Die **Dateikonvertierung** konvertiert Word- und PowerPoint-Dateien und -Datenströme in andere Formate.</span><span class="sxs-lookup"><span data-stu-id="6d067-110">**File conversion** converts Word and PowerPoint files and streams to other formats.</span></span>
    
  
- <span data-ttu-id="6d067-111">Die **Übersetzung** übersetzt Websites, Dokumente und Datenströme, um mehrere Sprachen zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="6d067-111">**Translation** translates sites, documents, and streams for multilingual support.</span></span>
    
  
<span data-ttu-id="6d067-112">Die folgende Tabelle zeigt allgemeine Szenarien, die für die in diesem Abschnitt beschriebenen Dienste gelten.</span><span class="sxs-lookup"><span data-stu-id="6d067-112">The following table shows high-level scenarios that apply to the services described in this section.</span></span>
  
    
    

<span data-ttu-id="6d067-113">**Tabelle 1: Szenarien für Office- und SharePoint-Dienste in SharePoint**</span><span class="sxs-lookup"><span data-stu-id="6d067-113">**Table 1. Scenarios for Office and SharePoint services in SharePoint**</span></span>


||<span data-ttu-id="6d067-114">**BI/Einblicke**</span><span class="sxs-lookup"><span data-stu-id="6d067-114">**BI/Insights**</span></span>|<span data-ttu-id="6d067-115">**Einfache Apps**</span><span class="sxs-lookup"><span data-stu-id="6d067-115">**Simple apps**</span></span>|<span data-ttu-id="6d067-116">**Dateikonvertierung**</span><span class="sxs-lookup"><span data-stu-id="6d067-116">**File conversion**</span></span>|<span data-ttu-id="6d067-117">**Übersetzung**</span><span class="sxs-lookup"><span data-stu-id="6d067-117">**Translation**</span></span>|
|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="6d067-118">Access Services</span><span class="sxs-lookup"><span data-stu-id="6d067-118">Access Services</span></span>  <br/> |<span data-ttu-id="6d067-119">X</span><span class="sxs-lookup"><span data-stu-id="6d067-119">X</span></span>  <br/> |<span data-ttu-id="6d067-120">X</span><span class="sxs-lookup"><span data-stu-id="6d067-120">X</span></span>  <br/> |||
|<span data-ttu-id="6d067-121">Excel Services</span><span class="sxs-lookup"><span data-stu-id="6d067-121">Excel Services</span></span>  <br/> |<span data-ttu-id="6d067-122">X</span><span class="sxs-lookup"><span data-stu-id="6d067-122">X</span></span>  <br/> ||||
|<span data-ttu-id="6d067-123">Maschineller Übersetzungsdienst</span><span class="sxs-lookup"><span data-stu-id="6d067-123">Machine Translation Service</span></span>  <br/> ||||<span data-ttu-id="6d067-124">X</span><span class="sxs-lookup"><span data-stu-id="6d067-124">X</span></span>  <br/> |
|<span data-ttu-id="6d067-125">PerformancePoint Services</span><span class="sxs-lookup"><span data-stu-id="6d067-125">PerformancePoint Services</span></span>  <br/> |<span data-ttu-id="6d067-126">X</span><span class="sxs-lookup"><span data-stu-id="6d067-126">X</span></span>  <br/> ||||
|<span data-ttu-id="6d067-127">PowerPoint Automation Services</span><span class="sxs-lookup"><span data-stu-id="6d067-127">PowerPoint Automation Services</span></span>  <br/> |||<span data-ttu-id="6d067-128">X</span><span class="sxs-lookup"><span data-stu-id="6d067-128">X</span></span>  <br/> ||
|<span data-ttu-id="6d067-129">Visio Services</span><span class="sxs-lookup"><span data-stu-id="6d067-129">Visio Services</span></span>  <br/> |<span data-ttu-id="6d067-130">X</span><span class="sxs-lookup"><span data-stu-id="6d067-130">X</span></span>  <br/> ||||
|<span data-ttu-id="6d067-131">Word Automation Services</span><span class="sxs-lookup"><span data-stu-id="6d067-131">Word Automation Services</span></span>  <br/> |||<span data-ttu-id="6d067-132">X</span><span class="sxs-lookup"><span data-stu-id="6d067-132">X</span></span>  <br/> ||
   

> <span data-ttu-id="6d067-133">**Hinweis:** In diesem Abschnitt werden nicht alle Dienste und Szenarien dargestellt.</span><span class="sxs-lookup"><span data-stu-id="6d067-133">**Note** Not all services and scenarios are represented in this section. For links to developer documentation for other services, see  Additional resources.</span></span> <span data-ttu-id="6d067-134">Links zu Entwicklerdokumentationen für andere Dienste finden Sie unter [Weitere Ressourcen](#bkmk_Resources).</span><span class="sxs-lookup"><span data-stu-id="6d067-134">Not all services and scenarios are represented in this section. For links to developer documentation for other services, see  [Additional resources](#bkmk_Resources).</span></span> 
  
    
    


## <a name="in-this-section"></a><span data-ttu-id="6d067-135">Inhalt dieses Abschnitts</span><span class="sxs-lookup"><span data-stu-id="6d067-135">In this section</span></span>
<span data-ttu-id="6d067-136"><a name="bkmk_inThisSection"> </a></span><span class="sxs-lookup"><span data-stu-id="6d067-136"></span></span>

<span data-ttu-id="6d067-137">Verwenden Sie die Links in Tabelle 2, um mehr über die Entwicklung mit den in diesem Abschnitt beschriebenen Office- und SharePoint-Diensten zu erfahren: Access Services, Excel Services, Dienst für maschinelle Übersetzung, PerformancePoint-Dienste, PowerPoint Automation Services, Visio Services und Word Automation Services.</span><span class="sxs-lookup"><span data-stu-id="6d067-137">Use the links in Table 2 to learn more about developing with the Office and SharePoint services described in this section: Access Services, Excel Services, Machine Translation Service, PerformancePoint Services, PowerPoint Automation Services, Visio Services, and Word Automation Services.</span></span> 
  
    
    

<span data-ttu-id="6d067-138">**Tabelle 2: Überblick über Office- und SharePoint-Dienste in diesem Abschnitt**</span><span class="sxs-lookup"><span data-stu-id="6d067-138">**Table 2. Overview of Office and SharePoint services in this section**</span></span>


|<span data-ttu-id="6d067-139">**Dienst**</span><span class="sxs-lookup"><span data-stu-id="6d067-139">**Service**</span></span>|<span data-ttu-id="6d067-140">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="6d067-140">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6d067-141">Access Services</span><span class="sxs-lookup"><span data-stu-id="6d067-141">Access Services</span></span>  <br/> <span data-ttu-id="6d067-142">Siehe  [Entwickeln von Access-Web-Apps](develop-access-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="6d067-142">See  [Develop Access web apps](develop-access-web-apps.md)</span></span> <br/> |<span data-ttu-id="6d067-143">Ermöglicht Benutzern das Erstellen, Bereitstellen und Verwalten von gemeinsamen webbasierten Access-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="6d067-143">Enables users to create, deploy, and manage collaborative web-based Access applications.</span></span>  <br/> |
|<span data-ttu-id="6d067-144">Excel Services</span><span class="sxs-lookup"><span data-stu-id="6d067-144">Excel Services</span></span>  <br/> <span data-ttu-id="6d067-145">Siehe  [Excel Services in SharePoint](excel-services-in-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="6d067-145">See  [Excel Services in SharePoint](excel-services-in-sharepoint.md)</span></span> <br/> |<span data-ttu-id="6d067-146">Ermöglicht Benutzern das Laden, Berechnen und Anzeigen von Excel-Arbeitsmappen auf SharePoint-Websites.</span><span class="sxs-lookup"><span data-stu-id="6d067-146">Enables users to load, calculate, and display Excel workbooks on SharePoint sites.</span></span>  <br/> |
|<span data-ttu-id="6d067-147">Maschineller Übersetzungsdienst</span><span class="sxs-lookup"><span data-stu-id="6d067-147">Machine Translation Service</span></span>  <br/> <span data-ttu-id="6d067-148">Siehe  [Dienste für maschinelle Übersetzung in SharePoint](machine-translation-services-in-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="6d067-148">See  [Machine Translation Services in SharePoint](machine-translation-services-in-sharepoint.md)</span></span> <br/> |<span data-ttu-id="6d067-149">Bietet automatische maschinelle Übersetzungen von Sites, Dokumenten und Websites.</span><span class="sxs-lookup"><span data-stu-id="6d067-149">Provides automatic machine translation of sites, documents, and sites.</span></span>  <br/> |
|<span data-ttu-id="6d067-150">PerformancePoint Services</span><span class="sxs-lookup"><span data-stu-id="6d067-150">PerformancePoint Services</span></span>  <br/> <span data-ttu-id="6d067-151">Siehe [PerformancePoint-Dienste in SharePoint](performancepoint-services-in-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="6d067-151">See  [PerformancePoint Services in SharePoint](performancepoint-services-in-sharepoint.md)</span></span> <br/> |<span data-ttu-id="6d067-152">Erstellt und veröffentlicht Dashboards, die interaktive Datenvisualisierungen (z. B. Scorecards und Berichte) enthalten, mit denen Benutzer ihre Unternehmensleistung überwachen und analysieren können.</span><span class="sxs-lookup"><span data-stu-id="6d067-152">Creates and publishes dashboards that contain interactive data visualizations (such as scorecards and reports) that enable people to monitor and analyze their business performance.</span></span>  <br/> |
|<span data-ttu-id="6d067-153">PowerPoint Automation Services</span><span class="sxs-lookup"><span data-stu-id="6d067-153">PowerPoint Automation Services</span></span>  <br/>  [<span data-ttu-id="6d067-154">PowerPoint Automation Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d067-154">PowerPoint Automation Services in SharePoint</span></span>](powerpoint-automation-services-in-sharepoint.md) <br/> |<span data-ttu-id="6d067-155">Stellt eine unbeaufsichtigte, serverseitige Konvertierung von PowerPoint-Präsentationen in andere Formate bereit.</span><span class="sxs-lookup"><span data-stu-id="6d067-155">Provides unattended, server-side conversion of PowerPoint presentations into other formats.</span></span>  <br/> |
|<span data-ttu-id="6d067-156">Visio Services</span><span class="sxs-lookup"><span data-stu-id="6d067-156">Visio Services</span></span>  <br/> <span data-ttu-id="6d067-157">Siehe  [Visio Services in SharePoint](visio-services-in-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="6d067-157">See  [Visio Services in SharePoint](visio-services-in-sharepoint.md)</span></span> <br/> |<span data-ttu-id="6d067-158">Ermöglicht Benutzern das Anzeigen und Interagieren mit Visio-Zeichnungen, die auf SharePoint-Websites gespeichert sind.</span><span class="sxs-lookup"><span data-stu-id="6d067-158">Enables users to view and interact with Visio drawings stored on SharePoint sites.</span></span>  <br/> |
|<span data-ttu-id="6d067-159">Word Automation Services</span><span class="sxs-lookup"><span data-stu-id="6d067-159">Word Automation Services</span></span>  <br/> <span data-ttu-id="6d067-160">Siehe  [Neuerungen in Word Automation Services für Entwickler](what-s-new-in-word-automation-services-for-developers.md)</span><span class="sxs-lookup"><span data-stu-id="6d067-160">See  [What's new in Word Automation Services for developers](what-s-new-in-word-automation-services-for-developers.md)</span></span> <br/> |<span data-ttu-id="6d067-161">Ermöglicht eine unbeaufsichtigte, serverseitige Konvertierung von Dokumenten, die von Word unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="6d067-161">Provides unattended, server-side conversion of documents that are supported by Word.</span></span>  <br/> |
   
<span data-ttu-id="6d067-p103">In diesem Abschnitt sind nicht alle Dienste und Szenarien dargestellt. Links zu Dokumentation für Entwickler für andere Dienste finden Sie unter  [Zusätzliche Ressourcen](#bkmk_Resources).</span><span class="sxs-lookup"><span data-stu-id="6d067-p103">Not all services and scenarios are represented in this section. For links to developer documentation for other services, see  [Additional resources](#bkmk_Resources).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="6d067-164">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6d067-164">Additional resources</span></span>
<span data-ttu-id="6d067-165"><a name="bkmk_Resources"> </a></span><span class="sxs-lookup"><span data-stu-id="6d067-165"></span></span>


-  [<span data-ttu-id="6d067-166">Hinzufügen von SharePoint-Funktionen</span><span class="sxs-lookup"><span data-stu-id="6d067-166">Add SharePoint capabilities</span></span>](add-sharepoint-capabilities.md)
    
  
-  [<span data-ttu-id="6d067-167">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d067-167">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6d067-168">Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d067-168">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  <span data-ttu-id="6d067-169">
  [Installieren von SQL Server-BI-Features mit SharePoint (PowerPivot und Reporting Services)](http://msdn.microsoft.com/en-us/library/hh231671)</span><span class="sxs-lookup"><span data-stu-id="6d067-169">[Install SQL Server BI Features with SharePoint (PowerPivot and Reporting Services)](http://msdn.microsoft.com/en-us/library/hh231671)</span></span>
    
  

