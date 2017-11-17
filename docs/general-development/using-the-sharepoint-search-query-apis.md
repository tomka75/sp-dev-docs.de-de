---
title: Verwenden der SharePoint-Suchabfrage-APIs
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ae9d73ed-1140-430b-9287-01dbbe8ae7d1
ms.openlocfilehash: 1a68b192b9b27040b68f8f4a5b95e3711ba57ba5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="using-the-sharepoint-search-query-apis"></a><span data-ttu-id="7231f-102">Verwenden der SharePoint-Suchabfrage-APIs</span><span class="sxs-lookup"><span data-stu-id="7231f-102">Using the SharePoint search Query APIs</span></span>
<span data-ttu-id="7231f-103">In diesem Artikel erhalten Sie Informationen zu den in SharePoint verfügbaren Abfrage-APIs, die es Ihnen ermöglichen, benutzerdefinierten Lösungen und Anwendungen Suchfunktionen hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="7231f-103">Learn about the query APIs available in SharePoint that enable you to add search functionality to custom solutions and applications.</span></span> 
## <a name="sharepoint-query-apis"></a><span data-ttu-id="7231f-104">SharePoint-Abfrage-APIs</span><span class="sxs-lookup"><span data-stu-id="7231f-104">SharePoint Query APIs</span></span>
<span data-ttu-id="7231f-105"><a name="bk_QueryAPIs"> </a></span><span class="sxs-lookup"><span data-stu-id="7231f-105"></span></span>

<span data-ttu-id="7231f-106">Suche in SharePoint stellt verschiedene Abfrage-APIs zur Verfügung und bietet Ihnen damit unzählige Wege für den Zugriff auf Suchergebnisse. Suchergebnisse können somit in einer Vielzahl von benutzerdefinierten Lösungstypen zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="7231f-106">Search in SharePoint provides several query APIs, giving you lots of ways to access search results, so that you can return search results in a variety of custom solution types.</span></span>
  
    
    
<span data-ttu-id="7231f-107">Neben dem Serverobjektmodell, das in früheren Versionen von SharePoint verfügbar war, bietet die Suche in SharePoint darüber hinaus Folgendes:</span><span class="sxs-lookup"><span data-stu-id="7231f-107">In addition to the server object model that was available in previous versions of SharePoint, Search in SharePoint also provides the following:</span></span>
  
    
    

- <span data-ttu-id="7231f-108">Clientobjektmodell (CSOM)</span><span class="sxs-lookup"><span data-stu-id="7231f-108">Client object model (CSOM)</span></span>
    
  
- <span data-ttu-id="7231f-109">JavaScript-Objektmodell (JSOM)</span><span class="sxs-lookup"><span data-stu-id="7231f-109">JavaScript object model (JSOM)</span></span>
    
  
- <span data-ttu-id="7231f-110">REST (Representational State Transfer)-Dienst</span><span class="sxs-lookup"><span data-stu-id="7231f-110">Representational State Transfer (REST) service</span></span>
    
  
<span data-ttu-id="7231f-111">In Tabelle 1 sind die APIs aufgeführt, die Sie zum Programmieren von Suchabfragen verwenden können, sowie der Pfad zu der Quelldatei auf dem Server.</span><span class="sxs-lookup"><span data-stu-id="7231f-111">Table 1 shows the APIs that you can use to program search queries and the path to the source file on the server.</span></span>
  
    
    

<span data-ttu-id="7231f-112">**Tabelle 1: Such-APIS**</span><span class="sxs-lookup"><span data-stu-id="7231f-112">**Table 1. Search APIs**</span></span>


|<span data-ttu-id="7231f-113">**API-Name**</span><span class="sxs-lookup"><span data-stu-id="7231f-113">**API name**</span></span>|<span data-ttu-id="7231f-114">**Klassenbibliothek oder Schema und Pfad**</span><span class="sxs-lookup"><span data-stu-id="7231f-114">**Class library or schema and path**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7231f-115">.NET CSOM</span><span class="sxs-lookup"><span data-stu-id="7231f-115">.NET CSOM</span></span>  <br/> |<span data-ttu-id="7231f-116">Microsoft.SharePoint.Client.Search.dll</span><span class="sxs-lookup"><span data-stu-id="7231f-116">Microsoft.SharePoint.Client.Search.dll          %ProgramFiles%Common FilesMicrosoft Sharedweb server extensions15ISAPI</span></span> <br/><span data-ttu-id="7231f-117">im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="7231f-117">Microsoft.SharePoint.Client.Search.dll          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span></span>  <br/> |
|<span data-ttu-id="7231f-118">Silverlight-CSOM</span><span class="sxs-lookup"><span data-stu-id="7231f-118">Silverlight CSOM</span></span>  <br/> |<span data-ttu-id="7231f-119">Microsoft.SharePoint.Client.Search.Silverlight.dll</span><span class="sxs-lookup"><span data-stu-id="7231f-119">Microsoft.SharePoint.Client.Search.Silverlight.dll          %ProgramFiles%Common FilesMicrosoft Sharedweb server extensions15TEMPLATELAYOUTSClientBin</span></span> <br/><span data-ttu-id="7231f-120">im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin</span><span class="sxs-lookup"><span data-stu-id="7231f-120">Microsoft.SharePoint.Client.Search.Silverlight.dll          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin</span></span>  <br/> |
|<span data-ttu-id="7231f-121">JavaScript-CSOM</span><span class="sxs-lookup"><span data-stu-id="7231f-121">JavaScript CSOM</span></span>  <br/> |<span data-ttu-id="7231f-122">SP.search.js</span><span class="sxs-lookup"><span data-stu-id="7231f-122">SP.search.js</span></span> <br/><span data-ttu-id="7231f-123">im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS</span><span class="sxs-lookup"><span data-stu-id="7231f-123">SP.search.js          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS</span></span>  <br/> |
|<span data-ttu-id="7231f-124">REST-Dienstendpunkte</span><span class="sxs-lookup"><span data-stu-id="7231f-124">REST service endpoints</span></span>  <br/> |<span data-ttu-id="7231f-125">http://Server/_API/Search/Query</span><span class="sxs-lookup"><span data-stu-id="7231f-125">http://server/_api/search/query</span></span> <br/><span data-ttu-id="7231f-126">http://server/_api/search/suggest</span><span class="sxs-lookup"><span data-stu-id="7231f-126">http://server/_api/search/queryhttp://server/_api/search/suggest</span></span>  <br/> |
|<span data-ttu-id="7231f-127">Serverobjektmodell</span><span class="sxs-lookup"><span data-stu-id="7231f-127">Server object model</span></span>  <br/> |<span data-ttu-id="7231f-128">Microsoft.Office.Server.Search.dll</span><span class="sxs-lookup"><span data-stu-id="7231f-128">Microsoft.Office.Server.Search.dll</span></span> <br/><span data-ttu-id="7231f-129">im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="7231f-129">Microsoft.Office.Server.Search.dll          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span></span>  <br/> |
   
<span data-ttu-id="7231f-p101">Verwenden Sie als bewährtes Verfahren bei der SharePoint-Entwicklung möglichst Client-APIs. Client-APIs enthalten die .NET-, Silverlight-, Phone- und JavaScript-Clientobjektmodelle und den REST-Dienst. Weitere Informationen zu den APIs in SharePoint und zu deren Verwendungsweise finden Sie unter  [Auswählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="7231f-p101">As a best practice in SharePoint development, use client APIs when you can. Client APIs include the .NET, Silverlight, Phone, and JavaScript client object models, and the REST service. For more information about the APIs in SharePoint and when to use them, see  [Choose the right API set in SharePoint](choose-the-right-api-set-in-sharepoint.md).</span></span>
  
    
    

### <a name="query-using-the-net-client-object-model"></a><span data-ttu-id="7231f-133">Abfrage mithilfe des .NET-Clientobjektmodells</span><span class="sxs-lookup"><span data-stu-id="7231f-133">Query using the .NET client object model</span></span>
<span data-ttu-id="7231f-134"><a name="bk_QueryNETcsom"> </a></span><span class="sxs-lookup"><span data-stu-id="7231f-134"></span></span>

<span data-ttu-id="7231f-p102">Die Suche in SharePoint umfasst ein Clientobjektmodell, das den Zugriff auf Suchergebnisse für die Onlineentwicklung sowie die lokale und die mobile Entwicklung ermöglicht. Das CSOM der Suche in SharePoint ist auf dem SharePoint-CSOM aufgebaut. Daher muss der Clientcode zuerst auf das SharePoint-CSOM und dann auf das CSOM der Suche in SharePoint zugreifen. Weitere Informationen zum SharePoint-CSOM finden Sie unter  [Verwaltetes Clientobjektmodell](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx). Weitere Informationen zur  [ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx) -Klasse, die der Einstiegspunkt zum CSOM ist, finden Sie unter [Clientkontext als zentrales Objekt](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="7231f-p102">Search in SharePoint includes a client object model that enables access to search results for online, on-premises, and mobile development. The Search in SharePoint CSOM is built on the SharePoint CSOM. Therefore, your client code first needs to access the SharePoint CSOM and then access the Search in SharePoint CSOM. For more information about the SharePoint CSOM, see  [SharePoint 2010 Client Object Model](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx). For more information about the  [ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx) class, which is the entry point to the CSOM, see [Client Context as Central Object](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="7231f-p103">Rufen Sie für das .NET-verwaltete CSOM eine **ClientContext**-Instanz ab (diese befindet sich im  [Microsoft.SharePoint.Client](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.aspx) -Namespace in der Microsoft.SharePoint.Client.dll). Verwenden Sie dann das Objektmodell im **Microsoft.SharePoint.Search.Client.Query** -Namespace in der Microsoft.SharePoint.Search.Client.dll.</span><span class="sxs-lookup"><span data-stu-id="7231f-p103">For the .NET managed CSOM, get a **ClientContext** instance (located in the [Microsoft.SharePoint.Client](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.aspx) namespace in the Microsoft.SharePoint.Client.dll). Then use the object model in the **Microsoft.SharePoint.Search.Client.Query** namespace in the Microsoft.SharePoint.Search.Client.dll.</span></span>
  
    
    
<span data-ttu-id="7231f-142">Nachfolgend finden Sie ein allgemeines Beispiel.</span><span class="sxs-lookup"><span data-stu-id="7231f-142">Here's a basic example.</span></span>
  
    
    



```cs

using (ClientContext clientContext = new ClientContext("http://<serverName>/sites/<siteCollectionPath>"))
{
    KeywordQuery keywordQuery = new KeywordQuery(clientContext);
    keywordQuery.QueryText = "SharePoint";
    SearchExecutor searchExecutor = new SearchExecutor(clientContext);
    ClientResult<ResultTableCollection> results = searchExecutor.ExecuteQuery(keywordQuery);
    clientContext.ExecuteQuery();
}
```

<span data-ttu-id="7231f-143">Sie können das folgende von SharePoint MVP  [Corey Roth](http://mvp.microsoft.com/en-us/mvp/Corey%20Roth-4029260) veröffentlichte Codebeispiel herunterladen: [SharePoint: Suchabfrage mit dem verwalteten Clientobjektmodell](http://code.msdn.microsoft.com/Query-Search-with-the-649f1bc1).</span><span class="sxs-lookup"><span data-stu-id="7231f-143">To download an example, see the following code sample posted by SharePoint MVP  [Corey Roth](http://mvp.microsoft.com/en-us/mvp/Corey%20Roth-4029260):  [SharePoint: Query Search with the Managed Client Object Model](http://code.msdn.microsoft.com/Query-Search-with-the-649f1bc1).</span></span>
  
    
    

### <a name="query-using-the-javascript-client-object-model"></a><span data-ttu-id="7231f-144">Abfrage mithilfe des JavaScript-Clientobjektmodells</span><span class="sxs-lookup"><span data-stu-id="7231f-144">Query using the JavaScript client object model</span></span>
<span data-ttu-id="7231f-145"><a name="bk_QueryJSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="7231f-145"></span></span>

<span data-ttu-id="7231f-146">Rufen Sie für das JavaScript-CSOM eine [ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx)-Instanz ab und verwenden Sie dann das Clientobjektmodell in der Datei SP.Search.js.</span><span class="sxs-lookup"><span data-stu-id="7231f-146">For the JavaScript CSOM, get a [T:Microsoft.SharePoint.Client.ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx) instance, and then use the object model in the SP.Search.js file.</span></span>
  
    
    
<span data-ttu-id="7231f-147">Nachfolgend finden Sie ein allgemeines Beispiel.</span><span class="sxs-lookup"><span data-stu-id="7231f-147">Here's a basic example.</span></span>
  
    
    



```

var clientContext = new SP.ClientContext("<serverRelativeUrl>");
var contextSite = clientContext.get_site();
var keywordQuery = new Microsoft.SharePoint.Client.Search.Query.KeywordQuery(clientContext); 
keywordQuery.set_queryText("SharePoint"); 
var searchExecutor = new Microsoft.SharePoint.Client.Search.Query.SearchExecutor(clientContext);  
var results = searchExecutor.executeQuery(keywordQuery); 
context.executeQueryAsync(onQuerySuccess, onQueryError);
```

<span data-ttu-id="7231f-148">Sie können das folgende von SharePoint MVP  [Corey Roth](http://mvp.microsoft.com/en-us/mvp/Corey%20Roth-4029260) veröffentlichte Codebeispiel herunterladen: [SharePoint: Suchabfrage mit dem JavaScript-Clientobjektmodell](http://code.msdn.microsoft.com/SharePoint-Querying-a629b53b).</span><span class="sxs-lookup"><span data-stu-id="7231f-148">To download an example, see the following code sample posted by SharePoint MVP  [Corey Roth](http://mvp.microsoft.com/en-us/mvp/Corey%20Roth-4029260):  [SharePoint: Querying Search with the JavaScript Client Object Model](http://code.msdn.microsoft.com/SharePoint-Querying-a629b53b).</span></span>
  
    
    

### <a name="query-using-the-rest-service"></a><span data-ttu-id="7231f-149">Abfrage mithilfe des REST-Diensts</span><span class="sxs-lookup"><span data-stu-id="7231f-149">Query using the REST service</span></span>
<span data-ttu-id="7231f-150"><a name="bk_QueryREST"> </a></span><span class="sxs-lookup"><span data-stu-id="7231f-150"></span></span>

<span data-ttu-id="7231f-p104">SharePoint enthält einen REST-Dienst, mit dem Sie Remoteabfragen für den SharePoint-Suchdienst in Clientanwendungen mit jeder Technologie, die REST-Webanforderungen unterstützt, durchführen können. Der REST-Suchdienst macht zwei Endpunkte verfügbar, **query** und **suggest**, und unterstützt die Vorgänge **GET** und **POST**. Die Ergebnisse werden im XML- oder im JavaScript Object Notation (JSON)-Format zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="7231f-p104">SharePoint includes a REST service that enables you to remotely execute queries against the SharePoint Search service from client applications by using any technology that supports REST web requests. The Search REST service exposes two endpoints, **query** and **suggest**, and will support both **GET** and **POST** operations. Results are returned in either XML or JavaScript Object Notation (JSON) format.</span></span>
  
    
    
<span data-ttu-id="7231f-p105">Dies ist der Zugriffspunkt für den Dienst:  `http://server/_api/search/`. Sie können die Website auch wie folgt in der URL angeben:  `http://server/site/_api/search/`. Der Suchdienst gibt Ergebnisse aus der gesamten Websitesammlung zurück. Es werden also die gleichen Ergebnisse bei beiden Arten des Zugriffs auf den Dienst zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="7231f-p105">The following is the access point for the service:  `http://server/_api/search/`. You can also specify the site in the URL, as follows:  `http://server/site/_api/search/`. The search service returns results from the entire site collection, so the same results are returned for both ways to access the service.</span></span>
  
    
    
<span data-ttu-id="7231f-157">Weitere Informationen finden Sie unter  [Übersicht über die REST-API der SharePoint-Suche](sharepoint-search-rest-api-overview.md) und [Abrufen von Abfragevorschläge mithilfe des Suche REST-Diensts](retrieving-query-suggestions-using-the-search-rest-service.md).</span><span class="sxs-lookup"><span data-stu-id="7231f-157">See  [SharePoint Search REST API overview](sharepoint-search-rest-api-overview.md) and [Retrieving query suggestions using the Search REST service](retrieving-query-suggestions-using-the-search-rest-service.md) for more information.</span></span>
  
    
    

### <a name="query-using-the-net-server-object-model"></a><span data-ttu-id="7231f-158">Abfrage mithilfe des .NET-Serverobjektmodells</span><span class="sxs-lookup"><span data-stu-id="7231f-158">Query using the .NET server object model</span></span>
<span data-ttu-id="7231f-159"><a name="bk_QuerySOM"> </a></span><span class="sxs-lookup"><span data-stu-id="7231f-159"></span></span>

<span data-ttu-id="7231f-p106">Anwendungen, die das Serverobjektmodell nutzen, müssen direkt auf einem Server mit SharePoint ausgeführt werden. Das Serverobjektmodell für die Suchabfrage befindet sich im  [Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx) -Namespace, der sich in der Microsoft.Office.Server.Search.dll befindet</span><span class="sxs-lookup"><span data-stu-id="7231f-p106">Applications that use the server object model must run directly on a server that is running SharePoint. The search Query server object model resides in the  [Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx) namespace, which is located in Microsoft.Office.Server.Search.dll.</span></span>
  
    
    
<span data-ttu-id="7231f-p107">Wie in SharePoint Server 2010 verwenden Sie die  **KeywordQuery** -Klasse zum Definieren der Abfrage. Anschließend wird die [Execute()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Query.Execute.aspx) -Methode aufgerufen, um die Abfrage zu übermitteln. In SharePoint ist die **Execute**-Methode veraltet. Sie funktioniert zwar noch, aber Sie sollten stattdessen die  [SearchExecutor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SearchExecutor.aspx) -Klasse verwenden. Rufen Sie zum Übermitteln der Abfrage die [ExecuteQuery()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SearchExecutor.ExecuteQuery.aspx) -Methode auf, und übergeben Sie die Instanz der **KeywordQuery**-Klasse in dem Aufruf.</span><span class="sxs-lookup"><span data-stu-id="7231f-p107">As in SharePoint Server 2010, you use the  **KeywordQuery** class to define the query, and then called the [Execute()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Query.Execute.aspx) method to submit the query. In SharePoint, the **Execute** method is obsolete, and while it will still work, you should use the [SearchExecutor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SearchExecutor.aspx) class instead. To submit the query, call the [ExecuteQuery()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SearchExecutor.ExecuteQuery.aspx) method, passing the instance of the **KeywordQuery** class in the call.</span></span>
  
    
    
<span data-ttu-id="7231f-165">Nachfolgend finden Sie ein allgemeines Beispiel.</span><span class="sxs-lookup"><span data-stu-id="7231f-165">Here's a basic example.</span></span>
  
    
    



```cs

using (SPSite siteCollection = new SPSite("<serverRelativeUrl>"))
{
    KeywordQuery keywordQuery = new KeywordQuery(siteCollection);
    keywordQuery.QueryText = "SharePoint";
    SearchExecutor searchExecutor = new SearchExecutor(); 
    ResultTableCollection resultTableCollection = searchExecutor.ExecuteQuery(keywordQuery); 
    resultTableCollection = resultTableCollection.Filter("TableType", KnownTableTypes.RelevantResults); 
    ResultTable resultTable = resultTableCollection.FirstOrDefault(); 
    DataTable dataTable = resultTable.Table; 
}
```

<span data-ttu-id="7231f-166">Sie können das folgende von SharePoint MVP  [Corey Roth](http://mvp.microsoft.com/en-us/mvp/Corey%20Roth-4029260) veröffentlichte Codebeispiel herunterladen: [SharePoint: Suchabfrage mit der KeywordQuery-Klasse](http://code.msdn.microsoft.com/Query-Search-with-the-372139b5).</span><span class="sxs-lookup"><span data-stu-id="7231f-166">To download an example, see the following code sample posted by SharePoint MVP  [Corey Roth](http://mvp.microsoft.com/en-us/mvp/Corey%20Roth-4029260):  [SharePoint: Query Search with the KeywordQuery Class](http://code.msdn.microsoft.com/Query-Search-with-the-372139b5).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="7231f-167">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="7231f-167">Additional resources</span></span>
<span data-ttu-id="7231f-168"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="7231f-168"></span></span>


-  [<span data-ttu-id="7231f-169">Erstellen von Suchabfragen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="7231f-169">Building search queries in SharePoint</span></span>](building-search-queries-in-sharepoint.md)
    
  
-  [<span data-ttu-id="7231f-170">Übersicht über die REST-API der SharePoint-Suche</span><span class="sxs-lookup"><span data-stu-id="7231f-170">SharePoint Search REST API overview</span></span>](sharepoint-search-rest-api-overview.md)
    
  
-  [<span data-ttu-id="7231f-171">SharePoint: Verwenden des Such-REST-Diensts über eine App für SharePoint</span><span class="sxs-lookup"><span data-stu-id="7231f-171">SharePoint: Using the search REST service from an app for SharePoint</span></span>](http://code.msdn.microsoft.com/sharepoint/SharePoint-Perform-a-1bf3e87d)
    
  

  
    
    
