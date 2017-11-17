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
# <a name="using-the-sharepoint-search-query-apis"></a>Verwenden der SharePoint-Suchabfrage-APIs
In diesem Artikel erhalten Sie Informationen zu den in SharePoint verfügbaren Abfrage-APIs, die es Ihnen ermöglichen, benutzerdefinierten Lösungen und Anwendungen Suchfunktionen hinzuzufügen. 
## <a name="sharepoint-query-apis"></a>SharePoint-Abfrage-APIs
<a name="bk_QueryAPIs"> </a>

Suche in SharePoint stellt verschiedene Abfrage-APIs zur Verfügung und bietet Ihnen damit unzählige Wege für den Zugriff auf Suchergebnisse. Suchergebnisse können somit in einer Vielzahl von benutzerdefinierten Lösungstypen zurückgegeben werden.
  
    
    
Neben dem Serverobjektmodell, das in früheren Versionen von SharePoint verfügbar war, bietet die Suche in SharePoint darüber hinaus Folgendes:
  
    
    

- Clientobjektmodell (CSOM)
    
  
- JavaScript-Objektmodell (JSOM)
    
  
- REST (Representational State Transfer)-Dienst
    
  
In Tabelle 1 sind die APIs aufgeführt, die Sie zum Programmieren von Suchabfragen verwenden können, sowie der Pfad zu der Quelldatei auf dem Server.
  
    
    

**Tabelle 1: Such-APIS**


|**API-Name**|**Klassenbibliothek oder Schema und Pfad**|
|:-----|:-----|
|.NET CSOM  <br/> |Microsoft.SharePoint.Client.Search.dll <br/>im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI  <br/> |
|Silverlight-CSOM  <br/> |Microsoft.SharePoint.Client.Search.Silverlight.dll <br/>im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin  <br/> |
|JavaScript-CSOM  <br/> |SP.search.js <br/>im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS  <br/> |
|REST-Dienstendpunkte  <br/> |http://Server/_API/Search/Query <br/>http://server/_api/search/suggest  <br/> |
|Serverobjektmodell  <br/> |Microsoft.Office.Server.Search.dll <br/>im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI  <br/> |
   
Verwenden Sie als bewährtes Verfahren bei der SharePoint-Entwicklung möglichst Client-APIs. Client-APIs enthalten die .NET-, Silverlight-, Phone- und JavaScript-Clientobjektmodelle und den REST-Dienst. Weitere Informationen zu den APIs in SharePoint und zu deren Verwendungsweise finden Sie unter  [Auswählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md).
  
    
    

### <a name="query-using-the-net-client-object-model"></a>Abfrage mithilfe des .NET-Clientobjektmodells
<a name="bk_QueryNETcsom"> </a>

Die Suche in SharePoint umfasst ein Clientobjektmodell, das den Zugriff auf Suchergebnisse für die Onlineentwicklung sowie die lokale und die mobile Entwicklung ermöglicht. Das CSOM der Suche in SharePoint ist auf dem SharePoint-CSOM aufgebaut. Daher muss der Clientcode zuerst auf das SharePoint-CSOM und dann auf das CSOM der Suche in SharePoint zugreifen. Weitere Informationen zum SharePoint-CSOM finden Sie unter  [Verwaltetes Clientobjektmodell](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx). Weitere Informationen zur  [ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx) -Klasse, die der Einstiegspunkt zum CSOM ist, finden Sie unter [Clientkontext als zentrales Objekt](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).
  
    
    
Rufen Sie für das .NET-verwaltete CSOM eine **ClientContext**-Instanz ab (diese befindet sich im  [Microsoft.SharePoint.Client](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.aspx) -Namespace in der Microsoft.SharePoint.Client.dll). Verwenden Sie dann das Objektmodell im **Microsoft.SharePoint.Search.Client.Query** -Namespace in der Microsoft.SharePoint.Search.Client.dll.
  
    
    
Nachfolgend finden Sie ein allgemeines Beispiel.
  
    
    



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

Sie können das folgende von SharePoint MVP  [Corey Roth](http://mvp.microsoft.com/en-us/mvp/Corey%20Roth-4029260) veröffentlichte Codebeispiel herunterladen: [SharePoint: Suchabfrage mit dem verwalteten Clientobjektmodell](http://code.msdn.microsoft.com/Query-Search-with-the-649f1bc1).
  
    
    

### <a name="query-using-the-javascript-client-object-model"></a>Abfrage mithilfe des JavaScript-Clientobjektmodells
<a name="bk_QueryJSOM"> </a>

Rufen Sie für das JavaScript-CSOM eine [ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx)-Instanz ab und verwenden Sie dann das Clientobjektmodell in der Datei SP.Search.js.
  
    
    
Nachfolgend finden Sie ein allgemeines Beispiel.
  
    
    



```

var clientContext = new SP.ClientContext("<serverRelativeUrl>");
var contextSite = clientContext.get_site();
var keywordQuery = new Microsoft.SharePoint.Client.Search.Query.KeywordQuery(clientContext); 
keywordQuery.set_queryText("SharePoint"); 
var searchExecutor = new Microsoft.SharePoint.Client.Search.Query.SearchExecutor(clientContext);  
var results = searchExecutor.executeQuery(keywordQuery); 
context.executeQueryAsync(onQuerySuccess, onQueryError);
```

Sie können das folgende von SharePoint MVP  [Corey Roth](http://mvp.microsoft.com/en-us/mvp/Corey%20Roth-4029260) veröffentlichte Codebeispiel herunterladen: [SharePoint: Suchabfrage mit dem JavaScript-Clientobjektmodell](http://code.msdn.microsoft.com/SharePoint-Querying-a629b53b).
  
    
    

### <a name="query-using-the-rest-service"></a>Abfrage mithilfe des REST-Diensts
<a name="bk_QueryREST"> </a>

SharePoint enthält einen REST-Dienst, mit dem Sie Remoteabfragen für den SharePoint-Suchdienst in Clientanwendungen mit jeder Technologie, die REST-Webanforderungen unterstützt, durchführen können. Der REST-Suchdienst macht zwei Endpunkte verfügbar, **query** und **suggest**, und unterstützt die Vorgänge **GET** und **POST**. Die Ergebnisse werden im XML- oder im JavaScript Object Notation (JSON)-Format zurückgegeben.
  
    
    
Dies ist der Zugriffspunkt für den Dienst:  `http://server/_api/search/`. Sie können die Website auch wie folgt in der URL angeben:  `http://server/site/_api/search/`. Der Suchdienst gibt Ergebnisse aus der gesamten Websitesammlung zurück. Es werden also die gleichen Ergebnisse bei beiden Arten des Zugriffs auf den Dienst zurückgegeben.
  
    
    
Weitere Informationen finden Sie unter  [Übersicht über die REST-API der SharePoint-Suche](sharepoint-search-rest-api-overview.md) und [Abrufen von Abfragevorschläge mithilfe des Suche REST-Diensts](retrieving-query-suggestions-using-the-search-rest-service.md).
  
    
    

### <a name="query-using-the-net-server-object-model"></a>Abfrage mithilfe des .NET-Serverobjektmodells
<a name="bk_QuerySOM"> </a>

Anwendungen, die das Serverobjektmodell nutzen, müssen direkt auf einem Server mit SharePoint ausgeführt werden. Das Serverobjektmodell für die Suchabfrage befindet sich im  [Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx) -Namespace, der sich in der Microsoft.Office.Server.Search.dll befindet
  
    
    
Wie in SharePoint Server 2010 verwenden Sie die  **KeywordQuery** -Klasse zum Definieren der Abfrage. Anschließend wird die [Execute()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Query.Execute.aspx) -Methode aufgerufen, um die Abfrage zu übermitteln. In SharePoint ist die **Execute**-Methode veraltet. Sie funktioniert zwar noch, aber Sie sollten stattdessen die  [SearchExecutor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SearchExecutor.aspx) -Klasse verwenden. Rufen Sie zum Übermitteln der Abfrage die [ExecuteQuery()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SearchExecutor.ExecuteQuery.aspx) -Methode auf, und übergeben Sie die Instanz der **KeywordQuery**-Klasse in dem Aufruf.
  
    
    
Nachfolgend finden Sie ein allgemeines Beispiel.
  
    
    



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

Sie können das folgende von SharePoint MVP  [Corey Roth](http://mvp.microsoft.com/en-us/mvp/Corey%20Roth-4029260) veröffentlichte Codebeispiel herunterladen: [SharePoint: Suchabfrage mit der KeywordQuery-Klasse](http://code.msdn.microsoft.com/Query-Search-with-the-372139b5).
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Erstellen von Suchabfragen in SharePoint](building-search-queries-in-sharepoint.md)
    
  
-  [Übersicht über die REST-API der SharePoint-Suche](sharepoint-search-rest-api-overview.md)
    
  
-  [SharePoint: Verwenden des Such-REST-Diensts über eine App für SharePoint](http://code.msdn.microsoft.com/sharepoint/SharePoint-Perform-a-1bf3e87d)
    
  

  
    
    
