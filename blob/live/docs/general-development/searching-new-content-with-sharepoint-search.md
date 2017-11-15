---
title: Durchsuchen von neuen Inhalten mit der SharePoint-Suche
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2a3a7d23-775a-4d95-9066-ebbd18c92ad4
ms.openlocfilehash: b8798b513c8db47c66c6754f72edb805fc724ce0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="searching-new-content-with-sharepoint-search"></a><span data-ttu-id="5f0fb-102">Durchsuchen von neuen Inhalten mit der SharePoint-Suche</span><span class="sxs-lookup"><span data-stu-id="5f0fb-102">Searching new content with SharePoint Search</span></span>
<span data-ttu-id="5f0fb-103">Erfahren Sie, wie Sie Inhalte für Benutzer für die Suche in SharePoint verfügbar machen.</span><span class="sxs-lookup"><span data-stu-id="5f0fb-103">Learn how to make content available for users to search with SharePoint Server 2013.</span></span>
## <a name="making-content-available-for-search-in-sharepoint"></a><span data-ttu-id="5f0fb-104">Verfügbarmachen von Inhalt für die Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f0fb-104">Making content available for search in SharePoint</span></span>

<span data-ttu-id="5f0fb-105">Suche in SharePoint stellt zwei Ansätze für die Verarbeitung von Abfragen zum Zurückgeben von Suchergebnissen bereit: die Sammelsuche und das Durchforsten von Inhalten.</span><span class="sxs-lookup"><span data-stu-id="5f0fb-105">Search in SharePoint provides two approaches for processing queries to return search results—federated search and content crawling.</span></span>
  
    
    
 <span data-ttu-id="5f0fb-p101">**Sammelsuche** Bei diesem Ansatz werden Suchergebnisse für Inhalte zurückgegeben, die nicht von Ihrem Suchserver durchforstet werden. Die Abfrage wird an ein externes Inhaltsrepository weitergeleitet, in dem sie von der Suchmaschine dieses Repositorys verarbeitet wird. Die Suchmaschine des Repositorys gibt dann die Ergebnisse an den Suchserver zurück. Der Suchserver formatiert und rendert die Ergebnisse aus dem externen Repository für die Anzeige auf der Suchergebnisseite. Dieser Ansatz bietet folgende Vorteile:</span><span class="sxs-lookup"><span data-stu-id="5f0fb-p101">**Federated search** In this approach, search results are returned for content that is not crawled by your search server. The query is forwarded to an external content repository where it is processed by that repository's search engine. The repository's search engine then returns the results to the search server. The search server formats and renders the results from the external repository to display on the search results page. This approach offers the following advantages:</span></span>
  
    
    

- <span data-ttu-id="5f0fb-111">Sie benötigen keine zusätzlichen kapazitätsanforderungen für den Inhaltsindex, wie der Inhalt von Suche in SharePoint nicht durchforstet wird.</span><span class="sxs-lookup"><span data-stu-id="5f0fb-111">You require no additional capacity requirements for the content index, as content is not crawled by Search in SharePoint.</span></span>
    
  
- <span data-ttu-id="5f0fb-p102">Sie können die vorhandene Suchmaschine eines Repositorys nutzen. Sie können z. B. einen Verbund mit einer Internetsuchmaschine herstellen, um das Internet zu durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="5f0fb-p102">You can take advantage of a repository's existing search engine. For example, you can federate to an Internet search engine to search the web.</span></span>
    
  
- <span data-ttu-id="5f0fb-114">Sie können die Suchmaschine des Inhaltsrepositorys für die spezielle Inhaltsgruppe des Repositorys optimieren, was möglicherweise eine bessere Suchleistung für die Inhaltsgruppe bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="5f0fb-114">You can optimize the content repository's search engine for the repository's specific set of content, which might provide better search performance on the content set.</span></span>
    
  
- <span data-ttu-id="5f0fb-115">Sie können auf Repositorys zugreifen, die gegen Durchforstungen abgesichert sind, auf die aber mit Suchabfragen zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="5f0fb-115">You can access repositories that are secured against crawls, but which can be accessed by search queries.</span></span>
    
  
 <span data-ttu-id="5f0fb-p103">**Durchforsten von Inhalten** Bei diesem Ansatz werden Ergebnisse vom Inhaltsindex der Suchdienstanwendung basierend auf der Abfrage des Benutzers zurückgegeben. Der Inhaltsindex enthält Inhalte, die von der Suchdienstanwendung durchforstet werden, und umfasst Textinhalte und Metadaten für jedes Inhaltselement. Dieser Ansatz ermöglicht Folgendes:</span><span class="sxs-lookup"><span data-stu-id="5f0fb-p103">**Content crawling** In this approach, results are returned from the Search service application's content index based on the user's query. The content index contains content that is crawled by the Search service application, and includes text content and metadata for each content item. This approach enables you to:</span></span>
  
    
    

- <span data-ttu-id="5f0fb-119">Sie können Suchergebnisse nach Relevanz sortieren.</span><span class="sxs-lookup"><span data-stu-id="5f0fb-119">Sort results by relevance.</span></span>
    
  
- <span data-ttu-id="5f0fb-120">Sie können steuern, wie häufig der Inhaltsindex aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="5f0fb-120">Control how frequently the content index is updated.</span></span>
    
  
- <span data-ttu-id="5f0fb-121">Sie können angeben, welche Metadaten durchforstet werden.</span><span class="sxs-lookup"><span data-stu-id="5f0fb-121">Specify what metadata is crawled.</span></span>
    
  
- <span data-ttu-id="5f0fb-122">Sie können einen einzelnen Sicherungsvorgang für durchforstete Inhalte durchführen.</span><span class="sxs-lookup"><span data-stu-id="5f0fb-122">Perform a single backup operation for crawled content.</span></span>
    
  

## <a name="in-this-section"></a><span data-ttu-id="5f0fb-123">Inhalt dieses Abschnitts</span><span class="sxs-lookup"><span data-stu-id="5f0fb-123">In this section</span></span>


-  [<span data-ttu-id="5f0fb-124">Connector Framework für die Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f0fb-124">Search connector framework in SharePoint</span></span>](search-connector-framework-in-sharepoint.md)
    
  -  [<span data-ttu-id="5f0fb-125">Optimieren der BDC-Modelldatei für die Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f0fb-125">Enhancing the BDC model file for Search in SharePoint</span></span>](enhancing-the-bdc-model-file-for-search-in-sharepoint.md)
    
  
  -  [<span data-ttu-id="5f0fb-126">Vorgehensweise: durchforsten zugeordneter externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f0fb-126">How to: Crawl associated external content types in SharePoint</span></span>](how-to-crawl-associated-external-content-types-in-sharepoint.md)
    
  
  -  [<span data-ttu-id="5f0fb-127">Vorgehensweise: durchforsten binary large Objects () in SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f0fb-127">How to: Crawl binary large objects (BLOBs) in SharePoint</span></span>](how-to-crawl-binary-large-objects-blobs-in-sharepoint.md)
    
  
  -  [<span data-ttu-id="5f0fb-128">Vorgehensweise: durchforsten zugeordneter externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f0fb-128">How to: Crawl associated external content types in SharePoint</span></span>](how-to-crawl-associated-external-content-types-in-sharepoint.md)
    
  
  -  [<span data-ttu-id="5f0fb-129">Vorgehensweise: Konfigurieren der Sicherheit auf Elementebene in SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f0fb-129">How to: Configure item-level security in SharePoint</span></span>](how-to-configure-item-level-security-in-sharepoint.md)
    
  

