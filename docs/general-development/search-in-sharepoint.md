---
title: Suche in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 59220f81-0e5e-4945-8056-cf0a116446cb
ms.openlocfilehash: daf7d446efd7f20a8123b86e8325cc5f0253cd8d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="search-in-sharepoint"></a><span data-ttu-id="beede-102">Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="beede-102">Search in SharePoint</span></span>
<span data-ttu-id="beede-p101">Informationen zur Erweiterbarkeit von Bausteinen in Suche in SharePoint und zu deren Verwendung für Ihre Anwendungsfälle. Mithilfe von Suche in SharePoint können Benutzer relevante Informationen schneller und einfacher denn je finden. Zudem wird es für Suchadministratoren einfach gestaltet, die Suchabfrage anzupassen. Außerdem werden verschiedene API-Sätze für komplexere Anpassungen und Lösungen bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="beede-p101">Understand the extensibility building blocks in Search in SharePoint and how you can use these building blocks to suit your use cases. Search in SharePoint enables users to find relevant information more quickly and easily than ever before and makes it easy for Search administrators to customize the search experience. It also provides several API sets for more advanced customizations and solutions.</span></span>
  
    
    

<span data-ttu-id="beede-106">In den folgenden Artikeln erhalten Sie eine geeignete Einführung zu allgemeinen SharePoint-Entwicklungskonzepten. Möglicherweise ist es für Sie hilfreich, diese vor dem Fortfahren zu lesen:</span><span class="sxs-lookup"><span data-stu-id="beede-106">See the following articles for a good introduction to general SharePoint development concepts; you may find it helpful to review these before proceeding:</span></span>
-  [<span data-ttu-id="beede-107">Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint</span><span class="sxs-lookup"><span data-stu-id="beede-107">Set up a general development environment for SharePoint</span></span>](set-up-a-general-development-environment-for-sharepoint.md)
    
  
-  [<span data-ttu-id="beede-108">Auswählen des richtigen API-Satzes in SharePoint</span><span class="sxs-lookup"><span data-stu-id="beede-108">Choose the right API set in SharePoint</span></span>](choose-the-right-api-set-in-sharepoint.md)
    
  
-  [<span data-ttu-id="beede-109">SharePoint-Add-Ins im Vergleich zu SharePoint-Lösungen</span><span class="sxs-lookup"><span data-stu-id="beede-109">SharePoint Add-ins compared with SharePoint solutions</span></span>](sharepoint-add-ins-compared-with-sharepoint-solutions.md)
    
  
-  [<span data-ttu-id="beede-110">Entscheidung zwischen SharePoint-Add-Ins und SharePoint-Lösungen</span><span class="sxs-lookup"><span data-stu-id="beede-110">Deciding between SharePoint Add-ins and SharePoint solutions</span></span>](deciding-between-sharepoint-add-ins-and-sharepoint-solutions.md)
    
  

## <a name="search-architecture-overview"></a><span data-ttu-id="beede-111">Übersicht über die Architektur der Suche</span><span class="sxs-lookup"><span data-stu-id="beede-111">Search architecture overview</span></span>

<span data-ttu-id="beede-p102">Suche in SharePoint umfasst eine Vielzahl von Verbesserungen und neuen Features. Mit dieser Version wird Suche in SharePoint zu einer einzelnen Unternehmenssuchplattform umgestaltet. Die Sucharchitektur besteht aus den folgenden Bereichen:</span><span class="sxs-lookup"><span data-stu-id="beede-p102">Search in SharePoint includes a wide variety of improvements and new features. With this version, Search in SharePoint is re-architected to a single enterprise search platform. The search architecture consists of the following areas:</span></span>
  
    
    

-  [<span data-ttu-id="beede-115">Durchforsten und Inhaltsverarbeitung</span><span class="sxs-lookup"><span data-stu-id="beede-115">Crawl and content processing</span></span>](#bk_crawl)
    
  
-  [<span data-ttu-id="beede-116">Index</span><span class="sxs-lookup"><span data-stu-id="beede-116">Index</span></span>](#bk_index)
    
  
-  [<span data-ttu-id="beede-117">Abfrageverarbeitung</span><span class="sxs-lookup"><span data-stu-id="beede-117">Query processing</span></span>](#bk_query)
    
  
-  [<span data-ttu-id="beede-118">Suchverwaltung</span><span class="sxs-lookup"><span data-stu-id="beede-118">Search administration</span></span>](#bk_searchadmin)
    
  
-  [<span data-ttu-id="beede-119">Analyse</span><span class="sxs-lookup"><span data-stu-id="beede-119">Analytics</span></span>](#bk_analytics)
    
  
<span data-ttu-id="beede-p103">Diese Bereiche bestehen aus Komponenten und Datenbanken, die gemeinsam Suchvorgänge ausführen. Abbildung 1 bietet einen Überblick über die verschiedenen Bereiche der Sucharchitektur und die darin enthaltenen Komponenten und Datenbanken, die gemeinsam die Suchvorgänge ausführen.</span><span class="sxs-lookup"><span data-stu-id="beede-p103">These areas consist of components and databases that work cohesively to perform the search operation. Figure 1 provides an overall view of the different areas of search architecture, and the components and databases within that work cohesively to perform the search operation.</span></span> 
  
    
    

<span data-ttu-id="beede-122">**Abbildung 1. Interaktion der Suchkomponenten**</span><span class="sxs-lookup"><span data-stu-id="beede-122">**Figure 1. Search component interaction**</span></span>

  
    
    

  
    
    
![Suchkomponenteninteraktion](../images/SearchComponentInteraction.jpg)
  
    
    
<span data-ttu-id="beede-124">Eine ausführlichere Ansicht finden Sie unter  [Technische Diagramme - Suche](http://technet.microsoft.com/de-de/library/cc263199.aspx#search) und [Übersicht über die Suche in SharePoint](http://technet.microsoft.com/de-de/library/jj219738.aspx).</span><span class="sxs-lookup"><span data-stu-id="beede-124">For a more detailed view, see  [Technical Diagrams -- Search](http://technet.microsoft.com/de-de/library/cc263199.aspx#search) and [Overview of search in SharePoint Server 2013](http://technet.microsoft.com/de-de/library/jj219738.aspx).</span></span>
  
    
    

### <a name="crawl-and-content-processing"></a><span data-ttu-id="beede-125">Durchforsten und Inhaltsverarbeitung</span><span class="sxs-lookup"><span data-stu-id="beede-125">Crawl and content processing</span></span>
<span data-ttu-id="beede-126"><a name="bk_crawl"> </a></span><span class="sxs-lookup"><span data-stu-id="beede-126"></span></span>

<span data-ttu-id="beede-127">Die Architektur für Durchforsten und Inhaltsverarbeitung umfasst Folgendes:</span><span class="sxs-lookup"><span data-stu-id="beede-127">The crawl and content processing architecture consists of the following:</span></span>
  
    
    
 <span data-ttu-id="beede-128">**Durchforstungskomponente**</span><span class="sxs-lookup"><span data-stu-id="beede-128">**Crawl component**</span></span>
  
    
    
 <span data-ttu-id="beede-129">Durchforstet Inhaltsquellen, um durchforstete Eigenschaften und Metadaten von durchforsteten Elementen zu sammeln, und sendet diese Informationen an die Inhaltsverarbeitungskomponente.</span><span class="sxs-lookup"><span data-stu-id="beede-129">Crawls content sources to collect crawled properties and metadata from crawled items and sends this information to the content processing component.</span></span>
  
    
    
 <span data-ttu-id="beede-130">**Durchforstungsdatenbank**</span><span class="sxs-lookup"><span data-stu-id="beede-130">**Crawl database**</span></span>
  
    
    
<span data-ttu-id="beede-131">Enthält Informationen zu durchforsteten Elementen, z. B. zum Zeitstempel der letzten Durchforstung, zur letzten Durchforstungs-ID und zum Typ der Aktualisierung während der letzten Durchforstung.</span><span class="sxs-lookup"><span data-stu-id="beede-131">Contains information about crawled items, such as last crawl time, the last crawl ID, and the type of update during the last crawl.</span></span>
  
    
    
 <span data-ttu-id="beede-132">**Inhaltsverarbeitungskomponente**</span><span class="sxs-lookup"><span data-stu-id="beede-132">**Content processing component**</span></span>
  
    
    
<span data-ttu-id="beede-133">Durchforstet Inhaltsquellen, um durchforstete Eigenschaften und Metadaten von durchforsteten Elementen zu erfassen. Diese Informationen werden dann an die Indexkomponente gesendet.</span><span class="sxs-lookup"><span data-stu-id="beede-133">Crawls content sources to collect crawled properties and metadata from crawled items and sends this information to the index component.</span></span>
  
    
    

### <a name="index"></a><span data-ttu-id="beede-134">Index </span><span class="sxs-lookup"><span data-stu-id="beede-134">Index</span></span>
<span data-ttu-id="beede-135"><a name="bk_index"> </a></span><span class="sxs-lookup"><span data-stu-id="beede-135"></span></span>

<span data-ttu-id="beede-p104">Die Indexkomponente empfängt die von der Inhaltsverarbeitungskomponente verarbeiteten Elemente und schreibt diese in den Suchindex. Diese Komponente behandelt auch eingehende Abfragen, ruft Informationen aus dem Suchindex ab und sendet das Resultset an die Abfrageverarbeitungskomponente zurück.</span><span class="sxs-lookup"><span data-stu-id="beede-p104">The index component receives the processed items from the content processing component and writes them to the search index. This component also handles incoming queries, retrieves information from the search index, and sends back the result set to the query processing component.</span></span>
  
    
    

### <a name="query-processing"></a><span data-ttu-id="beede-138">Abfrageverarbeitung</span><span class="sxs-lookup"><span data-stu-id="beede-138">Query processing</span></span>
<span data-ttu-id="beede-139"><a name="bk_query"> </a></span><span class="sxs-lookup"><span data-stu-id="beede-139"></span></span>

<span data-ttu-id="beede-p105">Die Abfrageverarbeitungkomponente analysiert und verarbeitet Suchabfragen und Ergebnisse. Die verarbeitete Abfrage wird dann an die Indexkomponente gesendet, die eine Reihe von Suchergebnissen für die Abfrage zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="beede-p105">The query processing component analyzes and processes search queries and results. The processed query is then submitted to the index component, which returns a set of search results for the query.</span></span>
  
    
    

### <a name="search-administration"></a><span data-ttu-id="beede-142">Suchverwaltung</span><span class="sxs-lookup"><span data-stu-id="beede-142">Search administration</span></span>
<span data-ttu-id="beede-143"><a name="bk_searchadmin"> </a></span><span class="sxs-lookup"><span data-stu-id="beede-143"></span></span>

<span data-ttu-id="beede-144">Die Suchverwaltung besteht aus der Suchverwaltungskomponente und ihrer entsprechenden Datenbank.</span><span class="sxs-lookup"><span data-stu-id="beede-144">Search administration is composed of the search administration component and its corresponding database.</span></span>
  
    
    
 <span data-ttu-id="beede-145">**Suchverwaltungskomponente**</span><span class="sxs-lookup"><span data-stu-id="beede-145">**Search administration component**</span></span>
  
    
    
<span data-ttu-id="beede-146">Führt die Systemprozesse für die Suche aus, fügt neue Instanzen von Suchkomponenten hinzu und initialisiert diese.</span><span class="sxs-lookup"><span data-stu-id="beede-146">Runs the system processes for search, and adds and initializes new instances of search components.</span></span>
  
    
    
 <span data-ttu-id="beede-147">**Suchverwaltungsdatenbank**</span><span class="sxs-lookup"><span data-stu-id="beede-147">**Search administration database**</span></span>
  
    
    
<span data-ttu-id="beede-148">Speichert Suchkonfigurationsdaten.</span><span class="sxs-lookup"><span data-stu-id="beede-148">Stores search configuration data.</span></span>
  
    
    

### <a name="analytics"></a><span data-ttu-id="beede-149">Analyse</span><span class="sxs-lookup"><span data-stu-id="beede-149">Analytics</span></span>
<span data-ttu-id="beede-150"><a name="bk_analytics"> </a></span><span class="sxs-lookup"><span data-stu-id="beede-150"></span></span>

<span data-ttu-id="beede-151">Die Analysearchitektur besteht aus der Analyseverarbeitungskomponente, Analyseberichtsdatenbank und Linkdatenbank.</span><span class="sxs-lookup"><span data-stu-id="beede-151">The analytics architecture consists of the analytics processing component, analytics reporting database, and link database.</span></span>
  
    
    
 <span data-ttu-id="beede-152">**Analyseverarbeitungskomponente**</span><span class="sxs-lookup"><span data-stu-id="beede-152">**Analytics processing component**</span></span>
  
    
    
<span data-ttu-id="beede-153">Führt die Suchanalyse und Nutzungsanalyse durch.</span><span class="sxs-lookup"><span data-stu-id="beede-153">Performs search analytics and usage analytics.</span></span>
  
    
    
 <span data-ttu-id="beede-154">**Linkdatenbank**</span><span class="sxs-lookup"><span data-stu-id="beede-154">**Link database**</span></span>
  
    
    
<span data-ttu-id="beede-155">Speichert Informationen, die von der Inhaltsverarbeitungskomponente und Klickinformationen der Suche extrahiert werden.</span><span class="sxs-lookup"><span data-stu-id="beede-155">Stores information extracted by the content processing component and search click information.</span></span>
  
    
    
 <span data-ttu-id="beede-156">**Analyseberichtsdatenbank**</span><span class="sxs-lookup"><span data-stu-id="beede-156">**Analytics reporting database**</span></span>
  
    
    
<span data-ttu-id="beede-157">Speichert die Ergebnisse der Verwendungsanalyse.</span><span class="sxs-lookup"><span data-stu-id="beede-157">Stores the results of usage analytics.</span></span>
  
    
    
 <span data-ttu-id="beede-158">**Ereignisspeicher**</span><span class="sxs-lookup"><span data-stu-id="beede-158">**Event store**</span></span>
  
    
    
<span data-ttu-id="beede-159">Speichert die Nutzungsereignisse, die auf dem Front-End erfasst werden.</span><span class="sxs-lookup"><span data-stu-id="beede-159">Stores usage events that are captured on the front-end.</span></span>
  
    
    

## <a name="search-extensibility-points"></a><span data-ttu-id="beede-160">Erweiterbarkeitspunkte der Suche</span><span class="sxs-lookup"><span data-stu-id="beede-160">Search extensibility points</span></span>

<span data-ttu-id="beede-p106">Die Suche in SharePoint-Architektur bietet verschiedene Erweiterbarkeitspunkte, um Anpassungsszenarien zu unterstützen. In diesem Abschnitt werden diese Punkte beschrieben und gezeigt, wo Sie weitere Informationen zur Entwicklung für diese Szenarien finden können.</span><span class="sxs-lookup"><span data-stu-id="beede-p106">The Search in SharePoint architecture provides several extensibility points to support customization scenarios. In this section, we'll describe these points and show you where you can find more information about developing for these scenarios.</span></span>
  
    
    

### <a name="connector-framework"></a><span data-ttu-id="beede-163">Konnektorframework</span><span class="sxs-lookup"><span data-stu-id="beede-163">Connector framework</span></span>

<span data-ttu-id="beede-p107">Die Durchforstungskomponente durchforstet Inhalte, indem Konnektoren oder Protokollhandler aufgerufen werden, die mit Inhaltsquellen interagieren, um Daten abzurufen. Suche in SharePoint umfasst ein Konnektorframework, mit dem Sie Konnektoren anpassen und erstellen können, um neue Inhaltsquellen zu durchforsten. Weitere Informationen zur Architektur des Konnektorframeworks und zu deren Erweiterung finden Sie unter  [Connector Framework für die Suche in SharePoint](search-connector-framework-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="beede-p107">The crawl component crawls content by invoking connectors or protocol handlers that interact with content sources to retrieve data. Search in SharePoint includes a connector framework that you can use to customize and build connectors to crawl new content sources. For detailed information about the connector framework architecture and how to extend it, see  [Search connector framework in SharePoint](search-connector-framework-in-sharepoint.md).</span></span>
  
    
    

### <a name="custom-content-processing"></a><span data-ttu-id="beede-167">Benutzerdefinierte Inhaltsverarbeitung</span><span class="sxs-lookup"><span data-stu-id="beede-167">Custom content processing</span></span>

<span data-ttu-id="beede-p108">Innerhalb der Inhaltsverarbeitungskomponente können Sie das Webdienstpopup für die Inhaltsanreicherung verwenden, um die verwalteten Eigenschaften von durchforsteten Elementen zu ändern, bevor diese zum Suchindex hinzugefügt werden. Dieses Webdienstpopup wird für jeden von Ihnen erstellten externen Webdienst für die Inhaltsanreicherung ausgerufen. Weitere Informationen finden Sie unter  [Benutzerdefinierte Inhaltsverarbeitung mit dem Webdienstpopup zur Inhaltsanreicherung](custom-content-processing-with-the-content-enrichment-web-service-callout.md). Informationen zur schrittweisen Implementierung eines Webdiensts für die Inhaltsanreicherung finden Sie unter  [Vorgehensweise: verwenden die Anreicherung Web Service als Legende für SharePoint Server](how-to-use-the-content-enrichment-web-service-callout-for-sharepoint-server.md). Der Blogbeitrag  [Anpassen der SharePoint-Suchabfrage mit einem Webdienst für die Inhaltsanreicherung](http://blogs.msdn.com/b/sharepointdev/archive/2012/11/13/customize-the-sharepoint-search-experience-with-a-content-enrichment-web-service.aspx) ist ebenfalls eine geeignete Ressource.</span><span class="sxs-lookup"><span data-stu-id="beede-p108">Within the content processing component, you can use the Content Enrichment web service callout to modify the managed properties of crawled items before they are added to the search index. This web service callout calls out to any external content enrichment web service that you create. For more information, see  [Custom content processing with the Content Enrichment web service callout](custom-content-processing-with-the-content-enrichment-web-service-callout.md). For a step-by-step implementation of a content enrichment web service, see  [How to: Use the Content Enrichment web service callout for SharePoint Server](how-to-use-the-content-enrichment-web-service-callout-for-sharepoint-server.md). The blog post  [Customize the SharePoint search experience with a Content Enrichment web service](http://blogs.msdn.com/b/sharepointdev/archive/2012/11/13/customize-the-sharepoint-search-experience-with-a-content-enrichment-web-service.aspx) is also a good resource</span></span>
  
    
    

### <a name="query-apis"></a><span data-ttu-id="beede-173">Abfrage-APIs</span><span class="sxs-lookup"><span data-stu-id="beede-173">Query APIs</span></span>

<span data-ttu-id="beede-174">Suche in SharePoint stellt verschiedene Abfrage-APIs zur Verfügung und bietet Ihnen damit unzählige Wege für den Zugriff auf Suchergebnisse. Suchergebnisse können somit in einer Vielzahl von benutzerdefinierten Lösungstypen zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="beede-174">Search in SharePoint provides several query APIs, giving you lots of ways to access search results, so that you can return search results in a variety of custom solution types.</span></span>
  
    
    
<span data-ttu-id="beede-175">Tabelle 1 zeigt die APIs, die Sie zum Programmieren von Suche in SharePoint verwenden können, und wo Sie diese finden.</span><span class="sxs-lookup"><span data-stu-id="beede-175">Table 1 shows the APIs that you can use to program Search in SharePoint and where to find them.</span></span>
  
    
    

<span data-ttu-id="beede-176">**Tabelle 1: Such-APIs**</span><span class="sxs-lookup"><span data-stu-id="beede-176">**Table 1. Search APIs**</span></span>


|<span data-ttu-id="beede-177">**API-Name**</span><span class="sxs-lookup"><span data-stu-id="beede-177">**API name**</span></span>|<span data-ttu-id="beede-178">**Klassenbibliothek oder Schema und Pfad**</span><span class="sxs-lookup"><span data-stu-id="beede-178">**Class library or schema and path**</span></span>|
|:-----|:-----|
|<span data-ttu-id="beede-179">.NET-Clientobjektmodelle (CSOM)</span><span class="sxs-lookup"><span data-stu-id="beede-179">.NET client object model (CSOM)</span></span>  <br/> |<span data-ttu-id="beede-180">Microsoft.SharePoint.Client.Search.dll</span><span class="sxs-lookup"><span data-stu-id="beede-180">Microsoft.SharePoint.Client.Search.dll          %ProgramFiles%Common FilesMicrosoft Sharedweb server extensions15ISAPI</span></span> <br/><span data-ttu-id="beede-181">im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="beede-181">Microsoft.SharePoint.Client.Search.dll          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span></span>  <br/> |
|<span data-ttu-id="beede-182">Silverlight-CSOM</span><span class="sxs-lookup"><span data-stu-id="beede-182">Silverlight CSOM</span></span>  <br/> |<span data-ttu-id="beede-183">Microsoft.SharePoint.Client.Search.Silverlight.dll</span><span class="sxs-lookup"><span data-stu-id="beede-183">Microsoft.SharePoint.Client.Search.Silverlight.dll          %ProgramFiles%Common FilesMicrosoft Sharedweb server extensions15TEMPLATELAYOUTSClientBin</span></span> <br/><span data-ttu-id="beede-184">im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin</span><span class="sxs-lookup"><span data-stu-id="beede-184">Microsoft.SharePoint.Client.Search.Silverlight.dll          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin</span></span>  <br/> |
|<span data-ttu-id="beede-185">JavaScript-CSOM</span><span class="sxs-lookup"><span data-stu-id="beede-185">JavaScript CSOM</span></span>  <br/> |<span data-ttu-id="beede-186">SP.search.js</span><span class="sxs-lookup"><span data-stu-id="beede-186">SP.search.js</span></span> <br/><span data-ttu-id="beede-187">im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS</span><span class="sxs-lookup"><span data-stu-id="beede-187">SP.search.js          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS</span></span>  <br/> |
|<span data-ttu-id="beede-188">REST-Endpunkte (Representational State Transfer)</span><span class="sxs-lookup"><span data-stu-id="beede-188">Representational State Transfer (REST) service endpoints</span></span>  <br/> |<span data-ttu-id="beede-189">http://server/_api/search/query</span><span class="sxs-lookup"><span data-stu-id="beede-189">http://server/_api/search/query</span></span> <br/><span data-ttu-id="beede-190">http://server/_api/search/suggest</span><span class="sxs-lookup"><span data-stu-id="beede-190">http://server/_api/search/queryhttp://server/_api/search/suggest</span></span>  <br/> |
|<span data-ttu-id="beede-191">Serverobjektmodell</span><span class="sxs-lookup"><span data-stu-id="beede-191">Server object model</span></span>  <br/> |<span data-ttu-id="beede-192">Microsoft.Office.Server.Search.dll</span><span class="sxs-lookup"><span data-stu-id="beede-192">Microsoft.Office.Server.Search.dll</span></span> <br/><span data-ttu-id="beede-193">im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="beede-193">Microsoft.Office.Server.Search.dll          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span></span>  <br/> |
   
<span data-ttu-id="beede-194">Weitere Informationen finden Sie unter  [Verwenden der SharePoint-Suchabfrage-APIs](using-the-sharepoint-search-query-apis.md).</span><span class="sxs-lookup"><span data-stu-id="beede-194">For more information, see  [Using the SharePoint search Query APIs](using-the-sharepoint-search-query-apis.md).</span></span>
  
    
    

### <a name="analytics"></a><span data-ttu-id="beede-195">Analyse</span><span class="sxs-lookup"><span data-stu-id="beede-195">Analytics</span></span>

<span data-ttu-id="beede-196">Die Analyseverarbeitungskomponente analysiert sowohl Inhalte an sich als auch die Interaktion der Benutzer mit Inhalten, um jene Inhalte zu identifizieren und verfügbar zu machen, die für Benutzer am nützlichsten und relevantesten sind.</span><span class="sxs-lookup"><span data-stu-id="beede-196">To help identify and surface the content that users consider to be the most useful and relevant, the analytics processing component analyzes both the content itself, and also the way that users interact with it.</span></span> <span data-ttu-id="beede-197">Diese Analysen werden von Zeitgeberaufträgen durchgeführt, die für die Durchführung der Analyse-Lebenszyklusaufgaben, wie z.B. das Starten, Beenden, Anhalten und Fortsetzen eines Analyseauftrags, verantwortlich sind.</span><span class="sxs-lookup"><span data-stu-id="beede-197">These analyses are done by timer jobs that are responsible for performing analysis lifecycle tasks such as starting, stopping, pausing, and resuming an analysis job when requested.</span></span> <span data-ttu-id="beede-198">Sie können diese Zeitgeberaufträge über den Namespace [Microsoft.Office.Server.Search.Analytics](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Analytics.aspx) bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="beede-198">You can manipulate these timer jobs through the  [Microsoft.Office.Server.Search.Analytics](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Analytics.aspx) namespace.</span></span> <span data-ttu-id="beede-199">Ausführliche Informationen zu Analysen in SharePoint finden Sie unter [Übersicht über die Analyseverarbeitung in SharePoint](http://technet.microsoft.com/de-de/library/jj219554.aspx).</span><span class="sxs-lookup"><span data-stu-id="beede-199">For in-depth information about analytics in SharePoint, see [Overview of analytics processing in SharePoint](http://technet.microsoft.com/de-de/library/jj219554.aspx).</span></span>
  
    
    

### <a name="custom-ranking-models"></a><span data-ttu-id="beede-200">Benutzerdefinierte Rangfolgemodelle</span><span class="sxs-lookup"><span data-stu-id="beede-200">Custom ranking models</span></span>

<span data-ttu-id="beede-201">Suchergebnisse können auf verschiedene Arten, wie z. B. nach Rang, sortiert werden.</span><span class="sxs-lookup"><span data-stu-id="beede-201">Search results can be ordered in various ways, one of which is by rank score.</span></span> <span data-ttu-id="beede-202">Bewertungsergebnisse werden von der Suchmaschine mithilfe von Bewertungsmodellen berechnet.</span><span class="sxs-lookup"><span data-stu-id="beede-202">Rank scores are calculated by the search engine using ranking models.</span></span> <span data-ttu-id="beede-203">SharePoint enthält standardmäßig 14 Bewertungsmodelle.</span><span class="sxs-lookup"><span data-stu-id="beede-203">SharePoint provides fourteen ranking models by default.</span></span> <span data-ttu-id="beede-204">Wenn Sie nicht mit der Sortierung Ihrer Suchergebnisse zufrieden sind, können Sie ein benutzerdefiniertes Bewertungsmodell verwenden.</span><span class="sxs-lookup"><span data-stu-id="beede-204">However, if you are not satisfied with the way your search results are ordered, you can use a custom ranking model.</span></span> <span data-ttu-id="beede-205">Weitere Informationen zum Erstellen und zur Optimierung eines benutzerdefinierten Bewertungsmodells finden Sie unter [Anpassen von Bewertungsmodellen zur Verbesserung der Relevanz in SharePoint](customizing-ranking-models-to-improve-relevance-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="beede-205">To learn more about the process of creating a custom ranking model and tuning it, see  [Customizing ranking models to improve relevance in SharePoint](customizing-ranking-models-to-improve-relevance-in-sharepoint.md).</span></span>
  
    
    

### <a name="custom-security-trimming"></a><span data-ttu-id="beede-206">Benutzerdefinierte Sicherheitskürzung</span><span class="sxs-lookup"><span data-stu-id="beede-206">Custom security trimming</span></span>

<span data-ttu-id="beede-207">Die Suche in SharePoint führt zum Zeitpunkt der Abfrage mit den Sicherheitsinformationen der Durchforstungskomponente eine Sicherheitskürzung der Suchergebnisse durch, die auf der Identität des Benutzers, der die Anfrage sendet, basiert.</span><span class="sxs-lookup"><span data-stu-id="beede-207">Search in SharePoint Server 2013 performs security trimming of search results that are based on the identity of the user submitting the query, at query time, by using security information obtained from the crawl component. However, in some cases, you may need to implement custom security trimming. SharePoint Server 2013 provides two interfaces to accomplish this task:  ISecurityTrimmerPre and ISecurityTrimmerPost .</span></span> <span data-ttu-id="beede-208">In einigen Fällen müssen Sie die benutzerdefinierte Sicherheitskürzung möglicherweise implementieren.</span><span class="sxs-lookup"><span data-stu-id="beede-208">However, in some cases, you may need to implement custom security trimming.</span></span> <span data-ttu-id="beede-209">Dazu bietet SharePoint zwei Schnittstellen an: [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) und [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) .</span><span class="sxs-lookup"><span data-stu-id="beede-209">SharePoint provides two interfaces to accomplish this task:  [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) and [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) .</span></span>
  
    
    
<span data-ttu-id="beede-210">Die Prä-Trimmer-Schnittstelle ( **ISecurityTrimmerPre**) führt eine Auswertung vor der Abfrage aus, wobei die Suchabfrage umgeschrieben wird, um Sicherheitsinformationen hinzuzufügen, bevor die Abfrage mit dem Suchindex abgeglichen wird.</span><span class="sxs-lookup"><span data-stu-id="beede-210">The **ISecurityTrimmerPre** interface carries out pre-trimming, or pre-query evaluation, where the search query is rewritten to add security information before the search query is matched to the search index. The ISecurityTrimmerPost interface carries out post-trimming, or post-query evaluation, where the search results are pruned before they are returned to the user.</span></span> <span data-ttu-id="beede-211">Im Gegensatz dazu führt die Post-Trimmer-Schnittstelle ( **ISecurityTrimmerPost**) eine Auswertung nach der Abfrage durch, wobei die Suchergebnisse gekürzt werden, bevor sie an den Benutzer zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="beede-211">In contrast, the post-trimmer interface ( **ISecurityTrimmerPost**) carries out post-query evaluation, where the search results are pruned before they are returned to the user.</span></span> <span data-ttu-id="beede-212">Weitere Informationen zu den beiden Schnittstellen finden Sie unter [Benutzerdefinierte Sicherheitskürzung für die Suche in SharePoint](custom-security-trimming-for-search-in-sharepoint-server.md).</span><span class="sxs-lookup"><span data-stu-id="beede-212">For more information about the two interfaces, see  [Custom security trimming for Search in SharePoint](custom-security-trimming-for-search-in-sharepoint-server.md).</span></span> <span data-ttu-id="beede-213">Schrittweise Informationen zum Implementieren eines Security Trimmers finden Sie unter [Vorgehensweise: Verwenden eines benutzerdefinierten Security Trimmer für Suchergebnisse für SharePoint Server](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md).</span><span class="sxs-lookup"><span data-stu-id="beede-213">For step-by-step information on how to implement a security trimmer interface, see  [How to: Use a custom security trimmer for SharePoint Server search results](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md).</span></span>
  
    
    

### <a name="content-search-web-part"></a><span data-ttu-id="beede-214">Webpart für Inhaltssuche</span><span class="sxs-lookup"><span data-stu-id="beede-214">Content Search Web Part</span></span>

<span data-ttu-id="beede-p113">Das Inhaltssuche-Webpart ist ein Webpart, das dynamische Inhalte anzeigen kann, die zuvor durchforstet und zum Suchindex hinzugefügt wurden. Jede Instanz des Webparts wird einer Suchabfrage zugeordnet und zeigt die Ergebnisse für diese bestimmte Suchabfrage an. Wenn Benutzer zu einer Seite navigieren, die ein Inhaltssuche-Webpart enthält, wird automatisch eine Suchabfrage gestartet und die entsprechenden Suchergebnisse werden vom Suchindex zurückgegeben. Sie können das Inhaltssuche-Webpart jederzeit verwenden, wenn Sie Inhalte anzeigen möchten, die über automatisch generierte Suchabfragen aufgefüllt werden. In einigen Fällen können Sie das Inhaltssuche-Webpart erweitern, das über den  [Microsoft.Office.Server.Search.WebControls](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.aspx) -Namespace als [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.aspx) bereitgestellt wird. Informationen zum Erweitern von [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.aspx) , damit das Webpart benutzerdefinierte Eigenschaften erkennt, finden Sie unter [Benutzersegmentierung in SharePoint](user-segmentation-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="beede-p113">The Content Search Web Part is a Web Part that can display dynamic content that was previously crawled and added to the search index. Each instance of the Web Part is associated with a search query and shows the results for that particular search query. When users browse to a page that contains a Content Search Web Part, a search query is automatically issued, and the corresponding search results are returned from the search index. You can use the Content Search Web Part whenever you want to display content that is populated by automatically generated search queries. In some cases, you may want to extend the Content Search Web Part, which is exposed through the  [Microsoft.Office.Server.Search.WebControls](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.aspx) namespace as [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.aspx) . To learn about how to extend the [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.aspx) so that the Web Part understands custom properties, see [User segmentation in SharePoint](user-segmentation-in-sharepoint.md).</span></span>
  
    
    

### <a name="search-driven-mobile-apps-using-the-navigation-and-event-logging-rest-interfaces"></a><span data-ttu-id="beede-221">Suchgesteuerte mobile Apps, die die REST-Schnittstellen für die Navigation und Ereignisprotokollierung verwenden</span><span class="sxs-lookup"><span data-stu-id="beede-221">Search-driven mobile apps using the Navigation and Event Logging REST interfaces</span></span>

<span data-ttu-id="beede-222">SharePoint bietet zwei neue REST-Schnittstellen: Navigation und Ereignisprotokollierung.</span><span class="sxs-lookup"><span data-stu-id="beede-222">SharePoint provides two new REST interfaces: Navigation and Event Logging.</span></span> <span data-ttu-id="beede-223">Sie können diese Schnittstellen verwenden, um suchgesteuerte mobile Apps für Mobilgeräte, wie z. B. Smartphones und Tablets, zu erstellen, die auf anderen Betriebssystemen als Windows ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="beede-223">You can use them to create search-driven mobile apps for mobile devices, such as phones and tablets, that run on operating systems other than Windows.</span></span> <span data-ttu-id="beede-224">Mit diesem Feature können Sie den Produktkatalog auf andere Art als über einen mobilen Kanal auf Ihrem Mobilgerät anzeigen.</span><span class="sxs-lookup"><span data-stu-id="beede-224">This feature lets you display the product catalog on a mobile device in an alternate way, instead of using a mobile channel.</span></span> <span data-ttu-id="beede-225">Unter [Vorgehensweise: Erstellen suchgesteuerter mobiler Apps mit den REST-Schnittstellen für Navigation und Ereignisprotokollierung](how-to-build-search-driven-mobile-apps-with-the-navigation-and-event-logging-res.md) finden Sie ein detailliertes Beispiel für die Erstellung einer solchen App.</span><span class="sxs-lookup"><span data-stu-id="beede-225">See  [How to: Build search-driven mobile apps with the Navigation and Event Logging REST interfaces](how-to-build-search-driven-mobile-apps-with-the-navigation-and-event-logging-res.md) for a detailed example of how to create such an app.</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="beede-226">Inhalt dieses Abschnitts</span><span class="sxs-lookup"><span data-stu-id="beede-226">In this section</span></span>


-  [<span data-ttu-id="beede-227">What's new in SharePoint-Suche für Entwickler</span><span class="sxs-lookup"><span data-stu-id="beede-227">What's new in SharePoint search for developers</span></span>](what-s-new-in-sharepoint-search-for-developers.md)
    
  
-  [<span data-ttu-id="beede-228">Durchsuchen neuer Inhalte mit SharePoint-Suche</span><span class="sxs-lookup"><span data-stu-id="beede-228">Searching new content with SharePoint Search</span></span>](searching-new-content-with-sharepoint-search.md)
    
  
-  [<span data-ttu-id="beede-229">Konfigurieren der Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="beede-229">Configure search in SharePoint</span></span>](configure-search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="beede-230">Erstellen von Suchabfragen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="beede-230">Building search queries in SharePoint</span></span>](building-search-queries-in-sharepoint.md)
    
  
-  [<span data-ttu-id="beede-231">Übersicht über die REST-API der SharePoint-Suche</span><span class="sxs-lookup"><span data-stu-id="beede-231">SharePoint Search REST API overview</span></span>](sharepoint-search-rest-api-overview.md)
    
  
-  [<span data-ttu-id="beede-232">Anpassen von Suchergebnissen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="beede-232">Customizing search results in SharePoint</span></span>](customizing-search-results-in-sharepoint.md)
    
  
-  [<span data-ttu-id="beede-233">Sortieren von Suchergebnissen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="beede-233">Sorting search results in SharePoint</span></span>](sorting-search-results-in-sharepoint.md)
    
  
-  [<span data-ttu-id="beede-234">Anpassen von Bewertungsmodellen zur Verbesserung der Relevanz in SharePoint</span><span class="sxs-lookup"><span data-stu-id="beede-234">Customizing ranking models to improve relevance in SharePoint</span></span>](customizing-ranking-models-to-improve-relevance-in-sharepoint.md)
    
  
-  [<span data-ttu-id="beede-235">Benutzerdefinierte Sicherheitskürzung für die Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="beede-235">Custom security trimming for Search in SharePoint Server 2013</span></span>](custom-security-trimming-for-search-in-sharepoint-server.md)
    
  
-  [<span data-ttu-id="beede-236">Exportieren und Importieren von Konfigurationseinstellungen für Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="beede-236">Exporting and importing search configuration settings in SharePoint</span></span>](exporting-and-importing-search-configuration-settings-in-sharepoint.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="beede-237">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="beede-237">Additional resources</span></span>


-  <span data-ttu-id="beede-238">
  [Änderungen zwischen SharePoint 2010 und SharePoint](http://technet.microsoft.com/de-de/library/ff607742.aspx)</span><span class="sxs-lookup"><span data-stu-id="beede-238">[Changes from SharePoint 2010 to SharePoint](http://technet.microsoft.com/de-de/library/ff607742.aspx)</span></span>
    
  
-  <span data-ttu-id="beede-239">
  [Technische Diagramme - Suchen](http://technet.microsoft.com/de-de/library/cc263199.aspx#search)</span><span class="sxs-lookup"><span data-stu-id="beede-239">[Technical Diagrams -- Search](http://technet.microsoft.com/de-de/library/cc263199.aspx#search)</span></span>
    
  
-  [<span data-ttu-id="beede-240">Hinzufügen von SharePoint-Funktionen</span><span class="sxs-lookup"><span data-stu-id="beede-240">Add SharePoint capabilities</span></span>](add-sharepoint-capabilities.md)
    
  
