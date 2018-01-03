---
title: "Connector Framework für die Suche in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 38560a3b-69c6-4a56-97ca-3625bbd5755e
ms.openlocfilehash: ed9e023bbba020eb5e5deb35ac0c8e96cc9a88bd
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="search-connector-framework-in-sharepoint"></a><span data-ttu-id="17a27-102">Connector Framework für die Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="17a27-102">Search connector framework in SharePoint</span></span>
<span data-ttu-id="17a27-103">Erfahren Sie mehr über die SharePoint-Indizierungsconnectors, das Connector Framework und das Erstellen von benutzerdefinierten BCS-Indizierungsconnectors zum Durchsuchen externer Systeme.</span><span class="sxs-lookup"><span data-stu-id="17a27-103">Learn about the SharePoint indexing connectors, the connector framework, and how you can create custom BCS indexing connectors to search external systems.</span></span>
## <a name="making-content-available-for-search-in-sharepoint"></a><span data-ttu-id="17a27-104">Inhalt für die Suche in SharePoint verfügbar machen</span><span class="sxs-lookup"><span data-stu-id="17a27-104">Making content available for search in SharePoint</span></span>
<span data-ttu-id="17a27-105"><a name="SP15searchconnect_make"> </a></span><span class="sxs-lookup"><span data-stu-id="17a27-105"><a name="SP15searchconnect_make"> </a></span></span>

<span data-ttu-id="17a27-106">Suche in SharePoint stellt zwei Ansätze für die Verarbeitung von Anfragen zum Zurückgeben von Suchergebnissen bereit: die Sammelsuche und das Durchforsten von Inhalten.</span><span class="sxs-lookup"><span data-stu-id="17a27-106">Search in SharePoint provides two approaches for processing queries to return search results—federated search and content crawling.</span></span>
  
    
    
 <span data-ttu-id="17a27-p101">**Sammelsuche** Bei diesem Ansatz werden Suchergebnisse für Inhalte zurückgegeben, die nicht von Ihrem Suchserver durchforstet werden. Die Abfrage wird an ein externes Inhaltsrepository weitergeleitet, in dem sie von der Suchmaschine dieses Repositorys verarbeitet wird. Die Suchmaschine des Repositorys gibt dann die Ergebnisse an den Suchserver zurück. Der Suchserver formatiert und rendert die Ergebnisse aus dem externen Repository für die Anzeige auf der Suchergebnisseite. Dieser Ansatz bietet folgende Vorteile:</span><span class="sxs-lookup"><span data-stu-id="17a27-p101">**Federated search** In this approach, search results are returned for content that is not crawled by your search server. The query is forwarded to an external content repository where it is processed by that repository's search engine. The repository's search engine then returns the results to the search server. The search server formats and renders the results from the external repository to display on the search results page. This approach offers the following advantages:</span></span>
  
    
    

- <span data-ttu-id="17a27-112">Sie benötigen keine zusätzlichen Kapazitäten für den Inhaltsindex, da der Inhalt nicht von Suche in SharePoint durchforstet wird.</span><span class="sxs-lookup"><span data-stu-id="17a27-112">You require no additional capacity requirements for the content index, because content is not crawled by Search in SharePoint.</span></span>
    
  
- <span data-ttu-id="17a27-p102">Sie können die vorhandene Suchmaschine eines Repositorys nutzen. Sie können z. B. einen Verbund mit einer Internetsuchmaschine herstellen, um das Internet zu durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="17a27-p102">You can take advantage of a repository's existing search engine. For example, you can federate to an Internet search engine to search the web.</span></span>
    
  
- <span data-ttu-id="17a27-115">Sie können die Suchmaschine des Inhaltsrepositorys für die spezielle Inhaltsgruppe des Repositorys optimieren, was möglicherweise eine bessere Suchleistung für die Inhaltsgruppe bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="17a27-115">You can optimize the content repository's search engine for the repository's specific set of content, which might provide better search performance on the content set.</span></span>
    
  
- <span data-ttu-id="17a27-116">Sie können auf Repositories zugreifen, die gegen Durchforstungen gesichert sind, auf die jedoch mit Suchabfragen zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="17a27-116">You can access repositories that are secured against crawls, but that can be accessed by search queries.</span></span>
    
  
 <span data-ttu-id="17a27-p103">**Durchforsten von Inhalten** Bei diesem Ansatz werden Ergebnisse vom Inhaltsindex der Suchdienstanwendung basierend auf der Abfrage des Benutzers zurückgegeben. Der Inhaltsindex enthält Inhalte, die von der Suchdienstanwendung durchforstet werden, und umfasst Textinhalte und Metadaten für jedes Inhaltselement. Dieser Ansatz ermöglicht Folgendes:</span><span class="sxs-lookup"><span data-stu-id="17a27-p103">**Content crawling** In this approach, results are returned from the Search service application's content index based on the user's query. The content index contains content that is crawled by the Search service application, and includes text content and metadata for each content item. This approach enables you to:</span></span>
  
    
    

- <span data-ttu-id="17a27-120">Sie können Suchergebnisse nach Relevanz sortieren.</span><span class="sxs-lookup"><span data-stu-id="17a27-120">Sort results by relevance.</span></span>
    
  
- <span data-ttu-id="17a27-121">Sie können steuern, wie häufig der Inhaltsindex aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="17a27-121">Control how frequently the content index is updated.</span></span>
    
  
- <span data-ttu-id="17a27-122">Sie können angeben, welche Metadaten durchforstet werden.</span><span class="sxs-lookup"><span data-stu-id="17a27-122">Specify what metadata is crawled.</span></span>
    
  
- <span data-ttu-id="17a27-123">Sie können einen einzelnen Sicherungsvorgang für durchforstete Inhalte durchführen.</span><span class="sxs-lookup"><span data-stu-id="17a27-123">Perform a single backup operation for crawled content.</span></span>
    
  

## <a name="crawling-content-with-indexing-connectors-in-sharepoint"></a><span data-ttu-id="17a27-124">Durchforsten von Inhalten mit Indizierungsconnectors in SharePoint</span><span class="sxs-lookup"><span data-stu-id="17a27-124">Crawling content with indexing connectors in SharePoint</span></span>
<span data-ttu-id="17a27-125"><a name="ConnectorFramework_SPIndexingConnectors"> </a></span><span class="sxs-lookup"><span data-stu-id="17a27-125"><a name="ConnectorFramework_SPIndexingConnectors"> </a></span></span>

<span data-ttu-id="17a27-p104">Der Crawler verwendet Indizierungsconnectors, um auf die zu durchforstenden Inhalte zuzugreifen. Der Indizierungsconnector ist eine Komponente, die weiß, wie eine Verbindung mit der Inhaltsquelle hergestellt wird, was durchforstet werden soll und wie der Inhalt durchforstet wird. In früheren Versionen von SharePoint wurden diese als Protokollhandler bezeichnet, Komponenten, die auf benutzerdefinierten Schnittstellen nicht verwalteten C++-Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="17a27-p104">The crawler uses indexing connectors to access the content to crawl. The indexing connector is the component that knows how to connect to the content source, what to crawl, and how to crawl it. In earlier versions of SharePoint, these were known as protocol handlers, components that are based on custom interfaces running unmanaged C++ code.</span></span> 
  
    
    
<span data-ttu-id="17a27-p105">Suche in SharePointenthält ein Connector Framework, das in SharePoint Server 2010 eingeführt wurde und auf Microsoft Business Connectivity Services (BCS) basiert, was einen einfacheren Ansatz für die Entwicklung von Indizierungsconnectors bietet. Mit dem Connector Framework verwendet der Crawler auf BCS basierende Indizierungsconnectors zum Durchforsten von externen Inhalten. SharePoint verwendet sowohl Indizierungsconnectors, die auf Protokollhandlern basieren, als auch BCS-Indizierungsconnectors zum Durchforsten von Inhalten.</span><span class="sxs-lookup"><span data-stu-id="17a27-p105">Search in SharePoint includes a connector framework, introduced in SharePoint Server 2010 and built on Microsoft Business Connectivity Services (BCS), which provides a simpler approach to developing indexing connectors. With the connector framework, the crawler uses indexing connectors based on BCS to crawl external content. SharePoint uses both protocol handler-based indexing connectors and BCS indexing connectors to crawl content.</span></span>
  
    
    
<span data-ttu-id="17a27-132">In Abbildung 1 sehen Sie eine allgemeine Übersicht über die SharePoint-Indizierungsconnectors.</span><span class="sxs-lookup"><span data-stu-id="17a27-132">Figure 1 provides a high-level overview of the SharePoint indexing connector story.</span></span>
  
    
    

  
    
    
![SharePoint-Indizierungs-Connectors](../images/SP15Con_CF_IndexingConnectors.jpg)
  
    
    

  
    
    

  
    
    

## <a name="bcs-overview-for-search-in-sharepoint"></a><span data-ttu-id="17a27-134">BCS-Übersicht für Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="17a27-134">BCS overview for Search in SharePoint</span></span>
<span data-ttu-id="17a27-135"><a name="ConnectorFramework_BCSOverview"> </a></span><span class="sxs-lookup"><span data-stu-id="17a27-135"><a name="ConnectorFramework_BCSOverview"> </a></span></span>

<span data-ttu-id="17a27-p106">BCS ist die Sammlung von Tools und Infrastrukturen, mit denen Sie eine Verbindung zu externen Systemen von SharePoint herstellen können. Abbildung 2 enthält eine allgemeine Ansicht der BCS-Architektur, in der die für die Suche relevanten Bereiche markiert sind.</span><span class="sxs-lookup"><span data-stu-id="17a27-p106">BCS is the umbrella of tools and infrastructure that enables you to connect to external systems from SharePoint. Figure 2 shows a high-level view of the BCS architecture, with the relevant areas for Search highlighted.</span></span>
  
    
    

  
    
    

<span data-ttu-id="17a27-138">**Abbildung 2: BCS-Architektur einschließlich Suche**</span><span class="sxs-lookup"><span data-stu-id="17a27-138">**Figure 2. BCS architecture including Search**</span></span>

  
    
    

  
    
    
![BCS-Architektur](../images/SP15Con_CF_BCS_Overview.jpg)
  
    
    

  
    
    
<span data-ttu-id="17a27-p107">BCS stellt die Verbindung mit den externen Daten basierend auf den externen Inhaltstypdefinition im Metadatenspeicher her. Der Metadatenspeicher enthält die folgenden Informationen für einen externen Inhaltstyp:</span><span class="sxs-lookup"><span data-stu-id="17a27-p107">BCS makes the connection to the external data based on the external content type definition in the metadata store. The metadata store contains the following information for an external content type:</span></span>
  
    
    

- <span data-ttu-id="17a27-142">**Konnektivitätsinformationen** Beschreibt, wie eine Verbindung mit dem externen System hergestellt wird.</span><span class="sxs-lookup"><span data-stu-id="17a27-142">**Connectivity information** Describes how to connect to the external system.</span></span>
    
  
- <span data-ttu-id="17a27-143">**Entitätsinformationen** Beschreibt die Struktur der externen Daten.</span><span class="sxs-lookup"><span data-stu-id="17a27-143">**Entity information** Describes the structure of the external data.</span></span>
    
  
- <span data-ttu-id="17a27-p108">**Vorgänge**Beschreibt Methoden, die für den Zugriff auf die externen Daten verwendet werden. Bei Datenbanken und Webdiensten werden diese Methoden vom externen System unterstützt: SQL-Anweisungen für Datenbankconnectors und Webmethoden für Webdienste. Bei .NET- und benutzerdefinierten BCS-Indizierungsconnectors handelt es sich um Methoden, die in der Connectorassembly implementiert sind, der Komponenten-DLL, die Sie für den Indizierungsconnector erstellen.</span><span class="sxs-lookup"><span data-stu-id="17a27-p108">**Operations** Describes methods used to access the external data. In the case of databases and web services, these are methods supported by the external system: SQL statements for database connectors and web methods for web services. For .NET and custom BCS indexing connectors, these are methods that are implemented in the connector assembly, which is the component DLL you create for the indexing connector.</span></span>
    
  
<span data-ttu-id="17a27-p109">Diese Informationen sind in der BDC-Modelldatei für den externen Inhaltstyp angegeben. Weitere Informationen zu BDC-Modellen und deren Inhalten finden Sie unter  [BDC-Modellinfrastruktur]((http://msdn.microsoft.com/library/2818ebdd-6cda-4d8f-82b2-7fde9fbf2633%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="17a27-p109">This information is specified in the external content type's BDC model file. For more information about BDC models and what they contain, see  [BDC Model Infrastructure]((http://msdn.microsoft.com/library/2818ebdd-6cda-4d8f-82b2-7fde9fbf2633%28Office.15%29.aspx)).</span></span>
  
    
    
<span data-ttu-id="17a27-149">Ausführliche Informationen über die BCS-Architektur und -Funktionalität finden Sie unter  [Business Connectivity Services (Übersicht)]((http://msdn.microsoft.com/library/91dd7b01-ead2-4f87-804b-b59ef2245c87%28Office.15%29.aspx)) und [Mechanismen im Zusammenhang mit der Verwendung von Business Connectivity Services]((http://msdn.microsoft.com/library/ff3e312b-0fbc-48ed-a752-76c50d286533%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="17a27-149">For details about BCS architecture and functionality, see  [Business Connectivity Services Overview]((http://msdn.microsoft.com/library/91dd7b01-ead2-4f87-804b-b59ef2245c87%28Office.15%29.aspx)) and [Mechanics of Using Business Connectivity Services]((http://msdn.microsoft.com/library/ff3e312b-0fbc-48ed-a752-76c50d286533%28Office.15%29.aspx)).</span></span>
  
    
    

### <a name="using-the-connector-framework"></a><span data-ttu-id="17a27-150">Verwenden des Connector Frameworks</span><span class="sxs-lookup"><span data-stu-id="17a27-150">Using the connector framework</span></span>

<span data-ttu-id="17a27-p110">Zum Durchforseten externer Daten müssen Sie einen der Inhaltsquellentypen hinzufügen, die das Verbinden mit externen Daten unterstützen. In Tabelle 1 sind diese Inhaltsquellentypen aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="17a27-p110">To crawl external data, you have to add one of the content source types that support connecting to external data. Table 1 lists these content source types.</span></span>
  
    
    

<span data-ttu-id="17a27-153">**Tabelle 1: Inhaltsquellentypen, die BCS-Indizierungsconnectors unterstützen**</span><span class="sxs-lookup"><span data-stu-id="17a27-153">**Table 1. Content source types that support BCS indexing connectors**</span></span>


|<span data-ttu-id="17a27-154">**Inhaltsquellentyp**</span><span class="sxs-lookup"><span data-stu-id="17a27-154">**Content source type**</span></span>|<span data-ttu-id="17a27-155">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="17a27-155">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="17a27-156">Branchendaten</span><span class="sxs-lookup"><span data-stu-id="17a27-156">Line of Business Data</span></span>  <br/> |<span data-ttu-id="17a27-157">Verwenden Sie diese Inhaltsquelle für Datenbank- und Webdienst-BCS-Indizierungsconnenctors.</span><span class="sxs-lookup"><span data-stu-id="17a27-157">Use this content source for database and web service BCS indexing connectors.</span></span>  <br/> |
|<span data-ttu-id="17a27-158">Benutzerdefiniertes Repository</span><span class="sxs-lookup"><span data-stu-id="17a27-158">Custom Repository</span></span>  <br/> |<span data-ttu-id="17a27-159">Verwenden Sie diese Inhaltsquelle für .NET- und benutzerdefinierte BCS-Indizierungsconnectors.</span><span class="sxs-lookup"><span data-stu-id="17a27-159">Use this content source for .NET and custom BCS indexing connectors.</span></span>  <br/> |
   
<span data-ttu-id="17a27-p111">Mit dem Connector Framework können Sie BCS-Indizierungsconnectors verwenden, um eine Verbindung zu externen Inhalten herzustellen, die Sie durchforsten und in den Inhaltsindex einschließen möchten. Der BCS-Indizierungsconnector wird vom Crawler verwendet, um mit der externen Datenquelle zu kommunizieren. Zum Zeitpunkt der Durchforstung ruft der Crawler den BCS-Indizierungsconnector auf, um die Daten aus dem externen System abzurufen und zurück an den Crawler zu übergeben. Der BCS-Indizierungsconnector analysiert außerdem die Zugriffs-URLs, die von der Suche verstanden wurden, und die Kennungen, die von BCS verstanden wurden, wenn sie während der Durchforstung zwischen BCS und der Suche übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="17a27-p111">The connector framework enables you to create BCS indexing connectors to connect to external content that you want to crawl and include in the content index. The BCS indexing connector is used by the crawler to communicate with the external data source. At crawl time, the crawler calls the BCS indexing connector to fetch the data from the external system and pass it back to the crawler. The BCS indexing connector also parses the access URLs understood by Search and the identifiers understood by BCS as they are passed between BCS and Search during the crawl process.</span></span>
  
    
    
<span data-ttu-id="17a27-164">BCS-Indizierungsconnectors bestehen aus Folgendem:</span><span class="sxs-lookup"><span data-stu-id="17a27-164">BCS indexing connectors are composed of the following:</span></span>
  
    
    


  
    
    
> <span data-ttu-id="17a27-165">**BDC-Modelldatei** Die Datei, die die Struktur der Daten und die Verbindungsinformationen für das externe System bereitstellt</span><span class="sxs-lookup"><span data-stu-id="17a27-165">**The BDC model file** The file that provides the structure of the data, and that provides connection information to the external system.</span></span>
    
  

  
    
    
> <span data-ttu-id="17a27-166">**Connector** Die Komponente, die den Code enthält, der eine Verbindung mit dem externen System herstellt und die Zugriffs-URLs und BCS-Kennungen analysiert.</span><span class="sxs-lookup"><span data-stu-id="17a27-166">**The connector** The component containing the code that connects to the external system and parses the access URLs and BCS identifiers.</span></span>
    
  
<span data-ttu-id="17a27-167">Für BCS-Indizierungsconnectors, die auf den Branchen-Inhaltsquelltypen basieren, enthält die Suche integrierte Connectors, sodass Sie nur eine BDC-Modelldatei erstellen müssen.</span><span class="sxs-lookup"><span data-stu-id="17a27-167">For BCS indexing connectors based on the Line of Business Data content source types, Search includes built-in connectors, so you have to create only a BDC model file.</span></span> 
  
    
    
<span data-ttu-id="17a27-168">Für BCS-Indizierungsconnectors, die auf dem Inhaltsquellentyp für ein benutzerdefiniertes Repository basieren, müssen Sie eine benutzerdefinierte Komponente zusätzlich zu einer BDC-Modelldatei entwickeln, um die Verbindung mit externen Daten herzustellen.</span><span class="sxs-lookup"><span data-stu-id="17a27-168">For BCS indexing connectors based on the Custom Repository content source types, you must develop a custom component in addition to a BDC model file to connect to the external data.</span></span>
  
    
    
<span data-ttu-id="17a27-169">Abbildung 3 zeigt eine allgemeine Ansicht der Such-Connector-Framework-Architektur.</span><span class="sxs-lookup"><span data-stu-id="17a27-169">Figure 3 shows a high-level view of the search connector framework architecture.</span></span>
  
    
    

<span data-ttu-id="17a27-170">**Abbildung 3: Such-Connector-Framework-Architektur**</span><span class="sxs-lookup"><span data-stu-id="17a27-170">**Figure 3. Search connector framework architecture**</span></span>

  
    
    

  
    
    
![Architektur des Search Connector Framework](../images/SP15Con_CF_ConnFrwkArch.jpg)
  
    
    

  
    
    

  
    
    

### <a name="bcs-indexing-connectors"></a><span data-ttu-id="17a27-172">BCS-Indizierungsconnectors</span><span class="sxs-lookup"><span data-stu-id="17a27-172">BCS indexing connectors</span></span>
<span data-ttu-id="17a27-173"><a name="ConnectorFramework_BCSIndexingConnectors"> </a></span><span class="sxs-lookup"><span data-stu-id="17a27-173"><a name="ConnectorFramework_BCSIndexingConnectors"> </a></span></span>

<span data-ttu-id="17a27-174">SharePoint unterstützt die folgenden Typen von BCS-Indizierungsconnectors:</span><span class="sxs-lookup"><span data-stu-id="17a27-174">SharePoint supports the following types of BCS indexing connectors:</span></span>
  
    
    

- <span data-ttu-id="17a27-175">**Datenbankconnector** SharePoint enthält einen vordefinierten BCS-Connector, der das Herstellen einer Verbindung zu Datenbanken unterstützt, sodass Sie einen Datenbank-BCS-Indizierungsconnector erstellen können, ohne Code schreiben zu müssen - Sie erstellen einfach die BDC-Modelldatei für den Connector.</span><span class="sxs-lookup"><span data-stu-id="17a27-175">**Database connector** SharePoint includes a predefined BCS connector that supports connecting to databases, so you can create a database BCS indexing connector without writing any code—just create the BDC model file for the connector.</span></span>
    
  
- <span data-ttu-id="17a27-176">**WCF-Connector (Webdienste)** SharePoint enthält einen vordefinierten BCS-Connector, der das Herstellen einer Verbindung zu Webdiensten unterstützt, sodass Sie einen Webdienst-BCS-Indizierungsconnector erstellen können, ohne Code schreiben zu müssen - Sie erstellen einfach die BDC-Modelldatei für den Connector.</span><span class="sxs-lookup"><span data-stu-id="17a27-176">**WCF (web services) connector** SharePoint includes a predefined BCS connector that supports connecting to web services, so you can create a web service BCS indexing connector without writing any code—just create the BDC model file for the connector.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="17a27-177">Sie müssen zwar keinen Code schreiben, um einen Connector für einen Webdienst zu erstellen; der Webdienst muss jedoch Methoden enthalten, die dieselben Funktionen bereitstellen wie der .NET-BCS-Connector. Nur so lassen sich externe Geschäftsdaten an BCS übergeben.</span><span class="sxs-lookup"><span data-stu-id="17a27-177">Note: Although you don't have to write code to create a connector for web services, the web service must include methods that provide the same functionality that the .NET BCS connector provides, to pass the external business data to BCS.</span></span> <span data-ttu-id="17a27-178">Informationen zur Erstellung von Webdiensten finden Sie unter [Erstellen von .NET-Konnektivitäts-Assemblys und Webdiensten]((http://msdn.microsoft.com/library/9a6c6712-868a-4a9c-9645-3aa448ad5092%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="17a27-178">For information about creating a web service, see  [Creating .NET Connectivity Assemblies and Web Services]((http://msdn.microsoft.com/library/9a6c6712-868a-4a9c-9645-3aa448ad5092%28Office.15%29.aspx)).</span></span> <span data-ttu-id="17a27-179">Codebeispiele finden Sie unter [Codebeispiel: Sample Orders ASP.Net Web Service]((http://msdn.microsoft.com/library/10e46860-788f-4ed0-a4d8-1e17ada58e83%28Office.15%29.aspx)) und [Codebeispiel: Sample Orders WCF Service]((http://msdn.microsoft.com/library/535277c8-9d5c-41eb-ab23-0ae141d726c5%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="17a27-179">For code examples, see  [Sample Orders ASP.NET Web Service Sample]((http://msdn.microsoft.com/library/10e46860-788f-4ed0-a4d8-1e17ada58e83%28Office.15%29.aspx)) and [Sample Orders WCF Service Sample]((http://msdn.microsoft.com/library/535277c8-9d5c-41eb-ab23-0ae141d726c5%28Office.15%29.aspx)).</span></span> 

- <span data-ttu-id="17a27-p113">**.NET-BCS-Connector**SharePoint enthält keinen vordefinierten BCS-Connector für .NET-Connectors, sodass Sie zusätzlich zum Erstellen einer BDC-Modelldatei auch eine .NET-Komponente für den BCS-Indizierungsconnector erstellen müssen. Sie müssen die erforderlichen stereotypen Vorgänge zur Unterstützung der Durchforstung der Daten sowie Methoden für die Analyse der Zugriffs-URLs und BDC-Kennungen implementieren.</span><span class="sxs-lookup"><span data-stu-id="17a27-p113">**.NET BCS connector** SharePoint does not include a predefined BCS connector for .NET connectors, so in addition to creating a BDC model file, you must also create a .NET component for the BCS indexing connector. You must implement the required stereotyped operations to support crawling the data, and implement methods for parsing the access URLs and BDC identifiers.</span></span>
    
  
- <span data-ttu-id="17a27-p114">**Benutzerdefinierter BCS-Connector**SharePoint enthält keinen vordefinierten BCS-Connector für benutzerdefinierte .NET-Connectors, deshalb müssen Sie zusätzlich zum Erstellen einer BDC-Modelldatei wie beim .NET-BCS-Connector auch eine .NET-Komponente für den BCS-Indizierungsconnector erstellen. Sie müssen die erforderlichen stereotypen Vorgänge zur Unterstützung der Durchforstung der Daten sowie Methoden für die Analyse der Zugriffs-URLs und BDC-Kennungen implementieren. Außerdem müssen Sie die **ISystemUtility**-Schnittstelle implementieren.</span><span class="sxs-lookup"><span data-stu-id="17a27-p114">**Custom BCS connector** SharePoint does not include a predefined BCS connector for custom .NET connectors, so in addition to creating a BDC model file, you must also create a .NET component for the BCS indexing connector, just as you must for the .NET BCS connector. You must implement the required stereotyped operations to support crawling the data, and implement methods for parsing the access URLs and BDC identifiers. You must also implement the **ISystemUtility** interface.</span></span>
    
  

## <a name="building-bcs-indexing-connectors"></a><span data-ttu-id="17a27-185">Erstellen von BCS-Indizierungsconnectors</span><span class="sxs-lookup"><span data-stu-id="17a27-185">Building BCS indexing connectors</span></span>
<span data-ttu-id="17a27-186"><a name="ConnectorFramework_BCSOverview"> </a></span><span class="sxs-lookup"><span data-stu-id="17a27-186"><a name="ConnectorFramework_BCSOverview"> </a></span></span>

<span data-ttu-id="17a27-187">Bei der Entwicklung eines BCS-Indizierungsconnectors müssen Sie unabhängig davon, ob Sie nur die BDC-Modelldatei für Datenbank- und Webdienst-Indizierungsconnectors erstellen oder die BDC-Modelldatei erstellen und die BCS-Connectorkomponente für .NET sowie benutzerdefinierte Indizierungsconnectors codieren, Folgendes berücksichtigen:</span><span class="sxs-lookup"><span data-stu-id="17a27-187">When you develop a BCS indexing connector—whether you're just creating the BDC model file for database and web service indexing connectors, or creating the BDC model file and coding the BCS connector component for .NET and custom indexing connectors—you need to think about the following:</span></span>
  
    
    

- <span data-ttu-id="17a27-p115">**Konnektivität** Wie Sie die Verbindung zum externen Datenrepository erstellen, z. B. die Serveradresse, die IP-Adresse oder den Namen der Datenbankinstanz. Umfasst außerdem die Authentifizierungsinformationen, die zum Verbinden mit dem externen Datenrepository verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="17a27-p115">**Connectivity** How to connect to the external data repository, for example, the server address, IP address, or database instance name. Also includes the authentication information used to connect to the external data repository.</span></span>
    
  
- <span data-ttu-id="17a27-p116">**Struktur des Repositorys** Zum Lesen der Daten muss der Connector wissen, wie das Repository organisiert ist. Ist es hierarchisch, numerisch oder muss es Links durchlaufen?</span><span class="sxs-lookup"><span data-stu-id="17a27-p116">**Structure of repository** To read the data, the connector must know how the repository is organized. Is it hierarchical, enumerical, or does it have to traverse links?</span></span>
    
  
- <span data-ttu-id="17a27-p117">**Inkrementelle Durchforstungen** Geben Sie dem Connector zur Reduzierung der Leistungsauslastung im externen Datenrepository die Möglichkeit, zusätzliche zu vollständigen Durchforstungen inkrementelle Durchforstungen durchzuführen. Dafür muss der Connector erkennen, welche Daten seit der letzten Durchforstung geändert wurden und nur diese Daten durchforsten können. Dies kann mit einer zeitstempelbasierten inkrementellen Durchforstung oder einer Durchforstung auf der Basis des Änderungsprotokolls erfolgen. Der von Ihnen implementierte Ansatz hängt von den APIs, die das Repository bereitstellt, und den Aktualitätszielen für den Inhalt ab.</span><span class="sxs-lookup"><span data-stu-id="17a27-p117">**Incremental crawls** To reduce the performance load on the external data repository, give the connector the ability to do incremental crawls in addition to full crawls. For this, the connector must recognize what data has changed since the last crawl and be able to crawl only that data. This can be done by using a timestamp-based incremental crawl or a change log-based crawl. The approach you implement depends on the APIs provided by the repository and the freshness goals for the content.</span></span>
    
  
- <span data-ttu-id="17a27-p118">**Sichern von Daten** In den meisten Szenarien sind nicht alle Daten für alle Benutzer zugänglich. Es ist wichtig, dass dies auch bei der Suche funktioniert, damit einem Benutzer, der über die Suchbenutzeroberfläche sucht, nur die Ergebnisse angezeigt werden, auf die er Zugriff hat. Das bedeutet, dass der Connector wissen muss, wie er die Sicherheit des externen Systems liest, und diese sicherheitsbezogenen Informationen während der Durchforstung zurück zum Index bringen muss. Sie können z. B. das Speichern von Windows NT-Zugriffssteuerungslisten (ACLs) während der Durchforstung implementieren.</span><span class="sxs-lookup"><span data-stu-id="17a27-p118">**Securing data** In most scenarios, not all data is accessible to all users. It's important that this also works with search, so when a user searches by using the search UI, the user can see only the results he or she has access to. This means the connector must know how to read the security of the external system, and bring that security-related information back during the crawl into the index. For example, you could implement crawl-time storage of Windows NT access control lists (ACLs).</span></span>
    
  
<span data-ttu-id="17a27-200">In Tabelle 2 sind die stereotypen Vorgänge beschrieben, die für das Erstellen eines BCS-Indizierungsconnectors für SharePoint gelten.</span><span class="sxs-lookup"><span data-stu-id="17a27-200">Table 2 describes the stereotyped operations that apply when you create a BCS indexing connector for SharePoint.</span></span>
  
    
    

<span data-ttu-id="17a27-201">**Tabelle 2: Von Suche in SharePoint unterstützte stereotype BCS-Vorgänge**</span><span class="sxs-lookup"><span data-stu-id="17a27-201">**Table 2. BCS stereotyped operations supported by Search in SharePoint**</span></span>


|<span data-ttu-id="17a27-202">**Vorgang**</span><span class="sxs-lookup"><span data-stu-id="17a27-202">**Operation**</span></span>|<span data-ttu-id="17a27-203">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="17a27-203">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="17a27-204">Finder</span><span class="sxs-lookup"><span data-stu-id="17a27-204">Finder</span></span>  <br/> |<span data-ttu-id="17a27-p119">Kernvorgang, der beim Erstellen eines BCS-Connectors erforderlich ist. Dieser Vorgang ruft die Liste der Elemente der externen Inhaltsquelle ab. Weitere Informationen finden Sie unter  [Implementieren eines Finders]((http://msdn.microsoft.com/library/a0cb7cfe-8758-4057-aa85-03071536745e%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="17a27-p119">Core operation required when creating a BCS connector. This operation retrieves the list of items of the external content source. See  [Implementing a Finder]((http://msdn.microsoft.com/library/a0cb7cfe-8758-4057-aa85-03071536745e%28Office.15%29.aspx)).  </span></span><br/> |
|<span data-ttu-id="17a27-208">SpecificFinder</span><span class="sxs-lookup"><span data-stu-id="17a27-208">SpecificFinder</span></span>  <br/> |<span data-ttu-id="17a27-p120">Kernvorgang, der beim Erstellen eines BCS-Connectors erforderlich ist. Dieser Vorgang ruft einzelne Elemente aus der externen Inhaltsquelle ab. Weitere Informationen finden Sie unter  [Implementieren von SpecificFinder]((http://msdn.microsoft.com/library/9b6effa5-20ce-4ce7-a8dc-0fd601eb0f23%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="17a27-p120">Core operation required when creating a BCS connector. This operation retrieves individual items from the external content source. See  [Implementing a SpecificFinder]((http://msdn.microsoft.com/library/9b6effa5-20ce-4ce7-a8dc-0fd601eb0f23%28Office.15%29.aspx)).  </span></span><br/> |
|<span data-ttu-id="17a27-212">ChangedIdEnumerator</span><span class="sxs-lookup"><span data-stu-id="17a27-212">ChangedIdEnumerator</span></span>  <br/> |<span data-ttu-id="17a27-p121">Erforderlich, um inkrementelle Durchforstungen auf der Basis des Änderungsprotokolls zu implementieren. Weitere Informationen finden Sie unter  [Implementieren von ChangedIdEnumerator]((http://msdn.microsoft.com/library/19d3c942-f6d7-49e7-853f-4d9b61b10422%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="17a27-p121">Required to implement changelog-based incremental crawls. See  [Implementing a ChangedIdEnumerator]((http://msdn.microsoft.com/library/19d3c942-f6d7-49e7-853f-4d9b61b10422%28Office.15%29.aspx)).  </span></span><br/> |
|<span data-ttu-id="17a27-215">DeletedIdEnumerator</span><span class="sxs-lookup"><span data-stu-id="17a27-215">DeletedIdEnumerator</span></span>  <br/> |<span data-ttu-id="17a27-p122">Erforderlich, um inkrementelle Durchforstungen auf der Basis des Änderungsprotokolls zu implementieren. Weitere Informationen finden Sie unter  [Implementieren von DeletedIdEnumerator]((http://msdn.microsoft.com/library/aa1c521a-0c9b-4dc0-a32f-fb9e54c52bed%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="17a27-p122">Required to implement changelog-based incremental crawls. See  [Implementing a DeletedIdEnumerator]((http://msdn.microsoft.com/library/aa1c521a-0c9b-4dc0-a32f-fb9e54c52bed%28Office.15%29.aspx)).  </span></span><br/> |
|<span data-ttu-id="17a27-218">BinarySecurityDescriptorAccessor</span><span class="sxs-lookup"><span data-stu-id="17a27-218">BinarySecurityDescriptorAccessor</span></span>  <br/> |<span data-ttu-id="17a27-p123">Erforderlich zum Implementieren der Sicherheit auf Elementebene. Gibt die Sicherheitsbeschreibung für ein Element aus der externen Inhaltsquelle zurück. Weitere Informationen finden Sie unter  [Implementieren von BinarySecurityDescriptorAccessor]((http://msdn.microsoft.com/library/6cf70490-dd3c-49cd-bb13-ed33e938435d%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="17a27-p123">Required to implement item-level security. Returns the security descriptor for an item from the external content source. See  [Implementing a BinarySecurityDescriptorAccessor]((http://msdn.microsoft.com/library/6cf70490-dd3c-49cd-bb13-ed33e938435d%28Office.15%29.aspx)).  </span></span><br/> |
|<span data-ttu-id="17a27-222">StreamAccessor</span><span class="sxs-lookup"><span data-stu-id="17a27-222">StreamAccessor</span></span>  <br/> |<span data-ttu-id="17a27-p124">Erforderlich zum Aktivieren der Durchforstung von Anlagen aus der externen Inhaltsquelle. Gibt die Anlage als Datenstrom zurück. Weitere Informationen finden Sie unter  [Implementieren von StreamAccessor]((http://msdn.microsoft.com/library/e3d8053b-90c0-4207-98e3-91e42db13cf1%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="17a27-p124">Required to enable crawling of attachments from the external content source. Returns the attachment as a data stream. See  [Implementing a StreamAccessor]((http://msdn.microsoft.com/library/e3d8053b-90c0-4207-98e3-91e42db13cf1%28Office.15%29.aspx)).  </span></span><br/> |
   

  
    
    

### <a name="tooling-support-for-developing-bcs-indexing-connectors"></a><span data-ttu-id="17a27-226">Toolunterstützung für die Entwicklung von BCS-Indizierungsconnectors</span><span class="sxs-lookup"><span data-stu-id="17a27-226">Tooling support for developing BCS indexing connectors</span></span>

<span data-ttu-id="17a27-227">BCS bietet Toolunterstützung für BCS-Connectors in SharePoint Designer und Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17a27-227">BCS provides tooling support for BCS connectors in SharePoint Designer and Visual Studio.</span></span>
  
    
    

#### <a name="sharepoint-designer-tooling-support-for-bcs-connectors"></a><span data-ttu-id="17a27-228">SharePoint Designer-Toolunterstützung für BCS-Connectors</span><span class="sxs-lookup"><span data-stu-id="17a27-228">SharePoint Designer tooling support for BCS connectors</span></span>

<span data-ttu-id="17a27-p125">SharePoint Designer stellt eine begrenzte Sammlung von Funktionen bereit. Sie können diese verwenden, um BDC-Modelldateien für vorhandene BCS-Connectortypen wie Datenbank-, Webdienst- und .NET-BCS-Connectors zu erstellen. Sie können sie auch verwenden, um BDC-Modelldateien aus einer BCS-Dienstanwendung in eine andere BCS-Dienstanwendung zu exportieren.</span><span class="sxs-lookup"><span data-stu-id="17a27-p125">SharePoint Designer provides a limited set of capabilities; you can use it to create BDC model files for existing BCS connector types, such as database, web service, and .NET BCS connectors. You can also use it to export BDC model files from one BCS service application to another BCS service application.</span></span>
  
    
    

#### <a name="visual-studio-tooling-support-for-bcs-connectors"></a><span data-ttu-id="17a27-231">Visual Studio-Toolunterstützung für BCS-Connectors</span><span class="sxs-lookup"><span data-stu-id="17a27-231">Visual Studio tooling support for BCS connectors</span></span>

<span data-ttu-id="17a27-p126">Sie können mit Visual Studio die Komponente für .NET-BCS- und benutzerdefinierten BCS-Connectors erstellen. Für .NET-BCS-Connectors stellt Visual Studio die Business Data Connectivity-Modellprojektvorlage bereit, die eine Reihe von visuellen Designer- und Codeverwaltungsfunktionen enthält, mit denen Sie die .NET-Komponente und die zugehörige BDC-Modelldatei für den .NET-BCS-Connector einfacher erstellen, debuggen und bereitstellen können. Es gibt keine entsprechende Projektvorlage für benutzerdefinierte BCS-Connectors.</span><span class="sxs-lookup"><span data-stu-id="17a27-p126">You can use Visual Studio to create the component for .NET BCS connectors and custom BCS connectors. For .NET BCS connectors, Visual Studio provides the Business Data Connectivity Model project template, which includes a set of visual designers and code management capabilities to enable you to more easily create, debug, and deploy the .NET component and the associated BDC model file for the .NET BCS connector. There is no corresponding project template for custom BCS connectors.</span></span>
  
    
    

## <a name="connector-framework-enhancements-in-sharepoint"></a><span data-ttu-id="17a27-235">Verbesserungen am Connector Framework in SharePoint</span><span class="sxs-lookup"><span data-stu-id="17a27-235">Connector framework enhancements in SharePoint</span></span>
<span data-ttu-id="17a27-236"><a name="SP15searchconnect_enhancements"> </a></span><span class="sxs-lookup"><span data-stu-id="17a27-236"><a name="SP15searchconnect_enhancements"> </a></span></span>

<span data-ttu-id="17a27-237">In SharePoint unterstützt das Connector Framework BCS-Connectors, die Anspruchsinformationen für Inhalte abrufen, die in benutzerdefinierten externen Datenrepositorys gespeichert sind.</span><span class="sxs-lookup"><span data-stu-id="17a27-237">In SharePoint the connector framework supports BCS connectors retrieving claims information for content that is stored in custom external data repositories.</span></span>
  
    
    
<span data-ttu-id="17a27-238">Das Connector Framework bietet außerdem eine verbesserte Ausnahmeerfassung und -protokollierung, die Ihnen helfen, Fehler beim Durchforsten von Inhaltsquellen mithilfe von BCS-Connectors zu beheben.</span><span class="sxs-lookup"><span data-stu-id="17a27-238">The connector framework also provides improved exception capturing and logging to help you troubleshoot errors encountered when crawling content sources by using BCS connectors.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="17a27-239">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="17a27-239">See also</span></span>
<span data-ttu-id="17a27-240"><a name="SP15searchconnect_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="17a27-240"><a name="SP15searchconnect_addlresources"> </a></span></span>


-  [<span data-ttu-id="17a27-241">Optimieren der BDC-Modelldatei für die Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="17a27-241">Enhancing the BDC model file for Search in SharePoint</span></span>](enhancing-the-bdc-model-file-for-search-in-sharepoint.md)
    
  
-  <span data-ttu-id="17a27-242">[SharePoint 2013: MyFileConnector custom BCS indexing connector sample]((https://code.msdn.microsoft.com/sharepoint-2013-myfileconne-79d2ea26))</span><span class="sxs-lookup"><span data-stu-id="17a27-242">[SharePoint 2013: MyFileConnector custom BCS indexing connector sample]((https://code.msdn.microsoft.com/sharepoint-2013-myfileconne-79d2ea26))</span></span>
    
  
-  [<span data-ttu-id="17a27-243">How to: Crawl associated external content types in SharePoint</span><span class="sxs-lookup"><span data-stu-id="17a27-243">How to: Crawl associated external content types in SharePoint</span></span>](how-to-crawl-associated-external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="17a27-244">Vorgehensweise: durchforsten binary large Objects () in SharePoint</span><span class="sxs-lookup"><span data-stu-id="17a27-244">How to: Crawl binary large objects (BLOBs) in SharePoint</span></span>](how-to-crawl-binary-large-objects-blobs-in-sharepoint.md)
    
  
-  [<span data-ttu-id="17a27-245">Vorgehensweise: durchforsten zugeordneter externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="17a27-245">How to: Crawl associated external content types in SharePoint</span></span>](how-to-crawl-associated-external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="17a27-246">Vorgehensweise: Konfigurieren der Sicherheit auf Elementebene in SharePoint</span><span class="sxs-lookup"><span data-stu-id="17a27-246">How to: Configure item-level security in SharePoint</span></span>](how-to-configure-item-level-security-in-sharepoint.md)
    
  

