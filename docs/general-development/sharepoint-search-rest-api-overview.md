---
title: "Übersicht über die REST-API der SharePoint-Suche"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: d0684be67a04f79cea059564390918be084d9eaf
ms.sourcegitcommit: d68d6cf927d69696a3561f7d8ffe9a3ed9dbd03c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="sharepoint-search-rest-api-overview"></a><span data-ttu-id="0ef1e-102">Übersicht über die REST-API der SharePoint-Suche</span><span class="sxs-lookup"><span data-stu-id="0ef1e-102">SharePoint Search REST API overview</span></span>
<span data-ttu-id="0ef1e-103">Fügen Sie Suchfunktionen zu Client- und mobilen Anwendungen hinzu, mit dem Search-REST-Dienst in SharePoint und jeder Technologie, die REST-Webanforderungen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-103">Add search functionality to client and mobile applications using the Search REST service in SharePoint Server 2013 and any technology that supports REST web requests.</span></span>
## <a name="querying-with-the-search-rest-service"></a><span data-ttu-id="0ef1e-104">Erstellen von Abfragen mit dem Search-REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="0ef1e-104">Querying with the Search REST service</span></span>
<span data-ttu-id="0ef1e-105"><a name="bk_queryrest"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-105"></span></span>

<span data-ttu-id="0ef1e-p101">Suche in SharePoint enthält einen Search-REST-Dienst, mit dem Sie Suchfunktionen zu Ihren Client- und mobilen Anwendungen hinzufügen können. Verwenden sie dazu eine beliebige Technologie, die REST-Webanforderungen unterstützt. Mit dem Search-REST-Dienst können Sie Keyword Query Language (KQL)- oder FAST Query Language (FQL)-Abfragen in Ihren SharePoint-Add-Ins, Remoteclient-Anwendungen, mobilen Anwendungen und anderen Anwendungen senden.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p101">Search in SharePoint includes a Search REST service you can use to add search functionality to your client and mobile applications by using any technology that supports REST web requests. You can use the Search REST service to submit Keyword Query Language (KQL) or FAST Query Language (FQL) queries in your SharePoint Add-ins, remote client applications, mobile applications, and other applications.</span></span>
  
    
    
<span data-ttu-id="0ef1e-108">Der Search-REST-Dienst unterstützt **POST**- und **GET**-HTTP-Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-108">The Search REST service supports both HTTP **POST** and HTTP **GET** requests.</span></span>
  
    
    

### <a name="get-requests"></a><span data-ttu-id="0ef1e-109">GET-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="0ef1e-109">GET requests</span></span>

<span data-ttu-id="0ef1e-110">Erstellen Sie den URI für **GET**Abfrageanforderungen hinsichtlich des Search-REST-Diensts wie folgt:</span><span class="sxs-lookup"><span data-stu-id="0ef1e-110">Construct the URI for query **GET** requests to the Search REST service as follows:</span></span>
  
    
    
 `/_api/search/query`
  
    
    
<span data-ttu-id="0ef1e-p102">Für **GET**-Anforderungen geben Sie die Abfrageparameter in der URL an. Sie können die **GET**-Anforderungs-URL auf zwei Arten erstellen:</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p102">For **GET** requests, you specify the query parameters in the URL. You can construct the **GET** request URL in two ways:</span></span>
  
    
    


  
    
    
>  `http://server/_api/search/query?query_parameter=value&amp;query_parameter=value`
    
  

  
    
    
>  `http://server/_api/search/query(query_parameter=value&amp;query_parameter=<value>)`
    
  

### <a name="post-requests"></a><span data-ttu-id="0ef1e-113">POST-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="0ef1e-113">POST requests</span></span>

<span data-ttu-id="0ef1e-114">Sie erstellen den URI für **POST**-Abfrageanforderungen hinsichtlich des Search-REST-Diensts wie folgt:</span><span class="sxs-lookup"><span data-stu-id="0ef1e-114">You construct the URI for query **POST** requests to the Search REST service as follows:</span></span>
  
    
    
 `/_api/search/postquery`
  
    
    
<span data-ttu-id="0ef1e-115">Für **POST**-Anforderungen geben Sie die Abfrageparameter in der Anforderung im JavaScript Object Notation (JSON)-Format weiter.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-115">For **POST** requests, you pass the query parameters in the request in JavaScript Object Notation (JSON) format.</span></span>
  
    
    
<span data-ttu-id="0ef1e-p103">Die **POST**-HTTP-Version des Search-REST-Diensts unterstützt alle Parameter, die von der **GET**-HTTP-Version unterstützt werden. Einige der Parameter weisen jedoch unterschiedliche Datentypen auf, wie in Tabelle 1 beschrieben.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p103">The HTTP **POST** version of the Search REST service supports all parameters supported by the HTTP **GET** version. However, some of the parameters have different data types, as described in Table 1.</span></span>
  
    
    

<span data-ttu-id="0ef1e-118">**Tabelle 1. Abfrageparameter mit unterschiedlichen Datentypen für POST-Anforderungen**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-118">**Table 1. Query parameters with different data types for POST requests**</span></span>


|<span data-ttu-id="0ef1e-119">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-119">**Parameter**</span></span>|<span data-ttu-id="0ef1e-120">**Datentyp**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-120">**Data type**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="0ef1e-121">SelectProperties</span><span class="sxs-lookup"><span data-stu-id="0ef1e-121">SelectProperties</span></span>](#bk_SelectProperties) <br/> |<span data-ttu-id="0ef1e-122">string[]</span><span class="sxs-lookup"><span data-stu-id="0ef1e-122">string[]</span></span>  <br/> |
| [<span data-ttu-id="0ef1e-123">RefinementFilters</span><span class="sxs-lookup"><span data-stu-id="0ef1e-123">RefinementFilters</span></span>](#bk_RefinementFilters) <br/> |<span data-ttu-id="0ef1e-124">string[]</span><span class="sxs-lookup"><span data-stu-id="0ef1e-124">string[]</span></span>  <br/> |
| [<span data-ttu-id="0ef1e-125">SortList</span><span class="sxs-lookup"><span data-stu-id="0ef1e-125">SortList</span></span>](#bk_SortList) <br/> | [<span data-ttu-id="0ef1e-126">Sort</span><span class="sxs-lookup"><span data-stu-id="0ef1e-126">Sort</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.Sort.aspx) <br/> |
| [<span data-ttu-id="0ef1e-127">HithighlightedProperties</span><span class="sxs-lookup"><span data-stu-id="0ef1e-127">HithighlightedProperties</span></span>](#bk_HithighlightedProperties) <br/> |<span data-ttu-id="0ef1e-128">string[]</span><span class="sxs-lookup"><span data-stu-id="0ef1e-128">string[]</span></span>  <br/> |
| [<span data-ttu-id="0ef1e-129">Properties</span><span class="sxs-lookup"><span data-stu-id="0ef1e-129">Properties</span></span>](#bk_Properties) <br/> | [<span data-ttu-id="0ef1e-130">Microsoft.SharePoint.Client.Search.Query.KeywordQueryProperties</span><span class="sxs-lookup"><span data-stu-id="0ef1e-130">Microsoft.SharePoint.Client.Search.Query.KeywordQueryProperties</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.KeywordQueryProperties.aspx) <br/> |
   
<span data-ttu-id="0ef1e-131">Verwenden Sie **POST**-Anforderungen in den folgenden Szenarios:</span><span class="sxs-lookup"><span data-stu-id="0ef1e-131">Use **POST** requests in the following scenarios:</span></span>
  
    
    

- <span data-ttu-id="0ef1e-132">Bei Überschreitung der URL-Längenbeschränkung für eine **GET**-Anforderung</span><span class="sxs-lookup"><span data-stu-id="0ef1e-132">When you'll exceed the URL length restriction with a **GET** request.</span></span>
    
  
- <span data-ttu-id="0ef1e-p104">Wenn Sie die Abfrageparameter nicht in einer einfachen URL angeben können. Wenn Sie beispielsweise Parameterwerte weitergeben müssen, die ein Array eines komplexen Typs oder durch Kommas getrennte Zeichenfolgen enthalten, sind Sie bei der Erstellung der **POST**-Anforderung flexibler.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p104">When you can't specify the query parameters in a simple URL. For example, if you have to pass parameter values that contain a complex type array, or comma-separated strings, you have more flexibility when constructing the **POST** request.</span></span>
    
  
- <span data-ttu-id="0ef1e-135">Bei Verwendung des  [ReorderingRules](#bk_ReorderingRules)-Parameters, da er nur für **POST**-Anforderungen unterstützt wird</span><span class="sxs-lookup"><span data-stu-id="0ef1e-135">When you use the  [ReorderingRules](#bk_ReorderingRules) parameter because it is supported only with **POST** requests.</span></span>
    
  

## <a name="using-query-parameters-with-the-search-rest-service"></a><span data-ttu-id="0ef1e-136">Verwenden von Abfrageparametern für den Search-REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="0ef1e-136">Using query parameters with the Search REST service</span></span>
<span data-ttu-id="0ef1e-137"><a name="bk_UsingQueryParams"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-137"></span></span>

<span data-ttu-id="0ef1e-p105">Wenn Sie den Search-REST-Dienst aufrufen, geben Sie Abfrageparameter für die Anforderung an. Suche in SharePoint verwendet diese Abfrageparameter, um die Suchabfrage zu erstellen. Für eine **GET**-Anforderung geben Sie die Abfrageparameter in der URL an. Für **POST**-Anforderungen geben Sie die Abfrageparameter im Textkörper im JavaScript Object Notation (JSON)-Format weiter.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p105">When you make a call to the Search REST service, you specify query parameters with the request. Search in SharePoint uses these query parameters to construct the search query. With a **GET** request, you specify the query parameters in the URL. For **POST** requests, you pass the query parameters in the body in JavaScript Object Notation (JSON) format.</span></span>
  
    
    
<span data-ttu-id="0ef1e-142">In den folgenden Abschnitten werden die Abfrageparameter beschrieben, mit denen Sie Suchabfragen mit dem Search-REST-Dienst senden können.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-142">The following sections describe the query parameters you can use to submit search queries with the Search REST service.</span></span>
  
    
    

### <a name="querytext-parameter"></a><span data-ttu-id="0ef1e-143">QueryText-Parameter</span><span class="sxs-lookup"><span data-stu-id="0ef1e-143">QueryText parameter</span></span>

<span data-ttu-id="0ef1e-144">Eine Zeichenfolge, die den Text für die Suchabfrage enthält</span><span class="sxs-lookup"><span data-stu-id="0ef1e-144">A string that contains the text for the search query.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-145">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-145">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-146">http:// _server_/_api/search/query?querytext='sharepoint'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-146">http:// _server_/_api/search/query?querytext='sharepoint'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-147">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-147">**Sample POST request**</span></span>

```JSON
{
    'request': {
         'Querytext': 'sharepoint',
         'RowLimit':20, 
         'ClientType':'ContentSearchRegular'
         }
}
```


### <a name="querytemplate"></a><span data-ttu-id="0ef1e-148">QueryTemplate</span><span class="sxs-lookup"><span data-stu-id="0ef1e-148">QueryTemplate</span></span>
<span data-ttu-id="0ef1e-149"><a name="bk_QueryTemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-149"></span></span>

<span data-ttu-id="0ef1e-150">Eine Zeichenfolge, die den Text enthält, der den Abfragetext ersetzt (als Teil einer Abfragetransformation)</span><span class="sxs-lookup"><span data-stu-id="0ef1e-150">A string that contains the text that replaces the query text, as part of a query transform.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-151">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-151">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-152">http://server/_api/search/query?querytext='sharepoint'&amp;querytemplate='{searchterms} author:johndoe'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-152">http://server/_api/search/query?querytext='sharepoint'&amp;querytemplate='{searchterms} author:johndoe'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-153">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-153">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'Querytemplate' : '{searchterms} Author:johndoe'
}
```


### <a name="enableinterleaving"></a><span data-ttu-id="0ef1e-154">EnableInterleaving</span><span class="sxs-lookup"><span data-stu-id="0ef1e-154">EnableInterleaving</span></span>
<span data-ttu-id="0ef1e-155"><a name="bk_EnableInterleaving"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-155"></span></span>

<span data-ttu-id="0ef1e-156">Ein boolescher Wert, der angibt, ob die für den Ergebnisblock zurückgegebenen Ergebnistabellen mit den für die ursprüngliche Abfrage zurückgegebenen Ergebnistabellen kombiniert werden</span><span class="sxs-lookup"><span data-stu-id="0ef1e-156">A Boolean value that specifies whether the result tables that are returned for the result block are mixed with the result tables that are returned for the original query.</span></span> 
  
    
    
 <span data-ttu-id="0ef1e-p106">**true** zum Kombinieren der Ergebnistabellen; andernfalls **false**. Der Standardwert ist **true**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p106">**true** to mix the ResultTables; otherwise, **false**. The default value is **true**.</span></span> 
  
    
    
<span data-ttu-id="0ef1e-159">Ändern Sie diesen Wert nur, wenn Sie Ihre eigene überlappende Implementierung bereitstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-159">Change this value only if you want to provide your own interleaving implementation.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-160">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-160">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-161">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enableinterleaving=true</span><span class="sxs-lookup"><span data-stu-id="0ef1e-161">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enableinterleaving=true</span></span>
  
    
    
 <span data-ttu-id="0ef1e-162">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-162">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'EnableInterleaving' : 'True'
}
```


### <a name="sourceid"></a><span data-ttu-id="0ef1e-163">SourceId</span><span class="sxs-lookup"><span data-stu-id="0ef1e-163">SourceId</span></span>
<span data-ttu-id="0ef1e-164"><a name="bk_SourceId"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-164"></span></span>

<span data-ttu-id="0ef1e-165">Ergebnis-Quell-ID für Ausführung der Suchabfrage</span><span class="sxs-lookup"><span data-stu-id="0ef1e-165">The result source ID to use for executing the search query.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-166">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-166">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-167">http:// _server_/_api/search/query?querytext='sharepoint'&amp;sourceid='8413cd39-2156-4e00-b54d-11efd9abdb89'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-167">http:// _server_/_api/search/query?querytext='sharepoint'&amp;sourceid='8413cd39-2156-4e00-b54d-11efd9abdb89'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-168">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-168">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'SourceId' : '8413cd39-2156-4e00-b54d-11efd9abdb89'
}
```


### <a name="rankingmodelid"></a><span data-ttu-id="0ef1e-169">RankingModelId</span><span class="sxs-lookup"><span data-stu-id="0ef1e-169">RankingModelId</span></span>
<span data-ttu-id="0ef1e-170"><a name="bk_RankingModelId"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-170"></span></span>

<span data-ttu-id="0ef1e-171">ID des Rangfolgemodells für die Abfrage</span><span class="sxs-lookup"><span data-stu-id="0ef1e-171">The ID of the ranking model to use for the query.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-172">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-172">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-173">http:// _server_/_api/search/query?querytext='sharepoint'&amp;rankingmodelid= _CustomRankingModelID_</span><span class="sxs-lookup"><span data-stu-id="0ef1e-173">http:// _server_/_api/search/query?querytext='sharepoint'&amp;rankingmodelid= _CustomRankingModelID_</span></span>
  
    
    
 <span data-ttu-id="0ef1e-174">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-174">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'RankingModelId' : 'CustomRankingModelID '
}
```


### <a name="startrow"></a><span data-ttu-id="0ef1e-175">StartRow</span><span class="sxs-lookup"><span data-stu-id="0ef1e-175">StartRow</span></span>
<span data-ttu-id="0ef1e-176"><a name="bk_StartRow"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-176"></span></span>

<span data-ttu-id="0ef1e-p107">Erste Zeile, die in den Suchergebnissen enthalten ist, die zurückgegeben werden. Verwenden Sie diesen Parameter, wenn Sie die Seitenverwaltung für Suchergebnisse implementieren möchten.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p107">The first row that is included in the search results that are returned. You use this parameter when you want to implement paging for search results.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-179">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-179">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-180">http:// _server_/_api/search/query?querytext='sharepoint'&amp;startrow=10</span><span class="sxs-lookup"><span data-stu-id="0ef1e-180">http:// _server_/_api/search/query?querytext='sharepoint'&amp;startrow=10</span></span>
  
    
    
 <span data-ttu-id="0ef1e-181">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-181">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'StartRow' : '10'
}
```


### <a name="rowlimit"></a><span data-ttu-id="0ef1e-182">RowLimit</span><span class="sxs-lookup"><span data-stu-id="0ef1e-182">RowLimit</span></span>
<span data-ttu-id="0ef1e-183"><a name="bk_RowLimit"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-183"></span></span>

<span data-ttu-id="0ef1e-p108">Maximale Anzahl von Zeilen, die in den Suchergebnissen zurückgegeben werden. Verglichen mit  _RowsPerPage_ ist _RowLimit_ die maximale Anzahl zurückgegebener Zeilen.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p108">The maximum number of rows overall that are returned in the search results. Compared to  _RowsPerPage_,  _RowLimit_ is the maximum number of rows returned overall.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-186">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-186">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-187">http:// _server_/_api/search/query?querytext='sharepoint'&amp;rowlimit=30</span><span class="sxs-lookup"><span data-stu-id="0ef1e-187">http:// _server_/_api/search/query?querytext='sharepoint'&amp;rowlimit=30</span></span>
  
    
    
 <span data-ttu-id="0ef1e-188">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-188">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'RowLimit' : '30'
}
```


### <a name="rowsperpage"></a><span data-ttu-id="0ef1e-189">RowsPerPage</span><span class="sxs-lookup"><span data-stu-id="0ef1e-189">RowsPerPage</span></span>
<span data-ttu-id="0ef1e-190"><a name="bk_RowsPerPage"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-190"></span></span>

<span data-ttu-id="0ef1e-p109">Maximale Anzahl von Zeilen, die pro Seite zurückgegeben werden. Verglichen mit  _RowLimit_ bezieht sich _RowsPerPage_ auf die maximale Anzahl von Zeilen, die pro Seite zurückgegeben werden. "RowsPerPage" wird hauptsächlich verwendet, wenn Sie die Seitenverwaltung für Suchergebnisse implementieren möchten.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p109">The maximum number of rows to return per page. Compared to  _RowLimit_,  _RowsPerPage_ refers to the maximum number of rows to return per page, and is used primarily when you want to implement paging for search results.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-193">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-193">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-194">http:// _server_/_api/search/query?querytext='sharepoint'&amp;rowsperpage=10</span><span class="sxs-lookup"><span data-stu-id="0ef1e-194">http:// _server_/_api/search/query?querytext='sharepoint'&amp;rowsperpage=10</span></span>
  
    
    
 <span data-ttu-id="0ef1e-195">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-195">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'RowsPerPage' : '10'
}
```


### <a name="selectproperties"></a><span data-ttu-id="0ef1e-196">SelectProperties</span><span class="sxs-lookup"><span data-stu-id="0ef1e-196">SelectProperties</span></span>
<span data-ttu-id="0ef1e-197"><a name="bk_SelectProperties"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-197"></span></span>

<span data-ttu-id="0ef1e-p110">Verwaltete Eigenschaften, die in den Suchergebnissen zurückgegeben werden. Um eine verwaltete Eigenschaft zurückzugeben, stellen Sie das abrufbare Flag der Eigenschaft im Suchschema auf **true** ein.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p110">The managed properties to return in the search results. To return a managed property, set the property's retrievable flag to **true** in the search schema.</span></span>
  
    
    
<span data-ttu-id="0ef1e-p111">Für **GET**-Anforderungen können Sie den  _SelectProperties_-Parameter in einer Zeichenfolge mit einer durch Kommas getrennten Liste von Eigenschaften angeben. Für **POST**-Anforderungen geben Sie den  _SelectProperties_-Parameter als Zeichenfolgenarray an.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p111">For **GET** requests, you specify the _SelectProperties_ parameter in a string containing a comma-separated list of properties. For **POST** requests, you specify the _SelectProperties_ parameter as a string array.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-202">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-202">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-203">http:// _server_/_api/search/query?querytext='sharepoint'&amp;selectproperties='Title,Author'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-203">http:// _server_/_api/search/query?querytext='sharepoint'&amp;selectproperties='Title,Author'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-204">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-204">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'SelectProperties' : {
    'results' : [
          'Title,
          Author'
          ]
}
}
```


### <a name="culture"></a><span data-ttu-id="0ef1e-205">Culture</span><span class="sxs-lookup"><span data-stu-id="0ef1e-205">Culture</span></span>
<span data-ttu-id="0ef1e-206"><a name="bk_Culture"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-206"></span></span>

<span data-ttu-id="0ef1e-207">Gebietsschema-ID (LCID) für die Abfrage (siehe  [Von Microsoft zugewiesene Gebietsschema-IDs](http://msdn.microsoft.com/en-us/goglobal/bb964664.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-207">The locale ID (LCID) for the query (see  [Locale IDs Assigned by Microsoft](http://msdn.microsoft.com/en-us/goglobal/bb964664.aspx)).</span></span>
  
    
    
 <span data-ttu-id="0ef1e-208">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-208">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-209">http:// _server_/_api/search/query?querytext='sharepoint'&amp;culture=1044</span><span class="sxs-lookup"><span data-stu-id="0ef1e-209">http:// _server_/_api/search/query?querytext='sharepoint'&amp;culture=1044</span></span>
  
    
    
 <span data-ttu-id="0ef1e-210">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-210">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'Culture' : '1044'
}
```


### <a name="refinementfilters"></a><span data-ttu-id="0ef1e-211">RefinementFilters</span><span class="sxs-lookup"><span data-stu-id="0ef1e-211">RefinementFilters</span></span>
<span data-ttu-id="0ef1e-212"><a name="bk_RefinementFilters"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-212"></span></span>

<span data-ttu-id="0ef1e-p112">Satz an Verfeinerungsfiltern für das Senden einer Verfeinerungsabfrage. Für **GET**-Anforderungen wird der  _RefinementFilters_-Parameter als FQL-Filter angegeben. Für **POST**-Anforderungen wird der  _RefinementFilters_-Parameter als Array von FQL-Filtern angegeben.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p112">The set of refinement filters used when issuing a refinement query. For **GET** requests, the _RefinementFilters_ parameter is specified as an FQL filter. For **POST** requests, the _RefinementFilters_ parameter is specified as an array of FQL filters.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-216">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-216">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-217">http:// _server_/_api/search/query?querytext='sharepoint'&amp;refinementfilters='fileExtension:equals("docx")'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-217">http:// _server_/_api/search/query?querytext='sharepoint'&amp;refinementfilters='fileExtension:equals("docx")'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-218">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-218">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'RefinementFilters' : {
'results' : ['fileExtension:equals("docx")']
}
}
```


### <a name="refiners"></a><span data-ttu-id="0ef1e-219">Einschränkungen</span><span class="sxs-lookup"><span data-stu-id="0ef1e-219">Refiners</span></span>
<span data-ttu-id="0ef1e-220"><a name="bk_Refiners"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-220"></span></span>

<span data-ttu-id="0ef1e-221">Satz an Einschränkungen, die in einem Suchergebnis zurückgegeben werden</span><span class="sxs-lookup"><span data-stu-id="0ef1e-221">The set of refiners to return in a search result.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-222">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-222">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-223">http:// _server_/_api/search/query?querytext='sharepoint'&amp;refiners='author,size'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-223">http:// _server_/_api/search/query?querytext='sharepoint'&amp;refiners='author,size'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-224">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-224">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'Refiners': {
'results' : ['author,size']
}
}
```


### <a name="hiddenconstraints"></a><span data-ttu-id="0ef1e-225">HiddenConstraints</span><span class="sxs-lookup"><span data-stu-id="0ef1e-225">HiddenConstraints</span></span>
<span data-ttu-id="0ef1e-226"><a name="bk_HiddenConstraints"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-226"></span></span>

<span data-ttu-id="0ef1e-227">Zusätzliche Abfrageausdrücke zum Anhängen an die Abfrage</span><span class="sxs-lookup"><span data-stu-id="0ef1e-227">The additional query terms to append to the query.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-228">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-228">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-229">http:// _server_/_api/search/query?querytext='sharepoint'&amp;hiddenconstraints='developer'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-229">http:// _server_/_api/search/query?querytext='sharepoint'&amp;hiddenconstraints='developer'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-230">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-230">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'HiddenConstraints':'developer'
}
```


### <a name="sortlist"></a><span data-ttu-id="0ef1e-231">SortList</span><span class="sxs-lookup"><span data-stu-id="0ef1e-231">SortList</span></span>
<span data-ttu-id="0ef1e-232"><a name="bk_SortList"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-232"></span></span>

<span data-ttu-id="0ef1e-233">Liste der Eigenschaften, nach der die Suchergebnisse sortiert sind</span><span class="sxs-lookup"><span data-stu-id="0ef1e-233">The list of properties by which the search results are ordered.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-234">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-234">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-235">http:// _server_/_api/search/query?querytext='sharepoint'&amp;sortlist='rank:descending,modifiedby:ascending'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-235">http:// _server_/_api/search/query?querytext='sharepoint'&amp;sortlist='rank:descending,modifiedby:ascending'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-236">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-236">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'SortList' : 
{
    'results' : [
        {
                'Property':'Created',
                'Direction': '0'
        },
        {
                'Property':'FileExtension',
                'Direction': '1'
        }
    ]
}
}
```


### <a name="enablestemming"></a><span data-ttu-id="0ef1e-237">EnableStemming</span><span class="sxs-lookup"><span data-stu-id="0ef1e-237">EnableStemming</span></span>
<span data-ttu-id="0ef1e-238"><a name="bk_EnableStemming"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-238"></span></span>

<span data-ttu-id="0ef1e-239">Ein boolescher Wert, der angibt, ob Wortstammerkennung aktiviert ist</span><span class="sxs-lookup"><span data-stu-id="0ef1e-239">A Boolean value that specifies whether stemming is enabled.</span></span> 
  
    
    
 <span data-ttu-id="0ef1e-p113">**true**, wenn Wortstammerkennung aktiviert ist; andernfalls **false**. Der Standardwert ist **true**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p113">**true** if the stemming is enabled; otherwise, **false**. The default value is **true**.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-242">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-242">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-243">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablestemming=false</span><span class="sxs-lookup"><span data-stu-id="0ef1e-243">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablestemming=false</span></span>
  
    
    
 <span data-ttu-id="0ef1e-244">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-244">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'EnableStemming : 'False'
}
```


### <a name="trimduplicates"></a><span data-ttu-id="0ef1e-245">TrimDuplicates</span><span class="sxs-lookup"><span data-stu-id="0ef1e-245">TrimDuplicates</span></span>
<span data-ttu-id="0ef1e-246"><a name="bk_TrimDuplicates"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-246"></span></span>

<span data-ttu-id="0ef1e-247">Ein boolescher Wert, der angibt, ob doppelte Elemente aus den Ergebnissen entfernt werden</span><span class="sxs-lookup"><span data-stu-id="0ef1e-247">A Boolean value that specifies whether duplicate items are removed from the results.</span></span> 
  
    
    
 <span data-ttu-id="0ef1e-p114">**true**, um doppelte Elemente zu entfernen; andernfalls **false**. Der Standardwert ist **true**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p114">**true** to remove the duplicate items; otherwise, **false**. The default value is **true**.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-250">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-250">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-251">http:// _server_/_api/search/query?querytext='sharepoint'&amp;trimduplicates=false</span><span class="sxs-lookup"><span data-stu-id="0ef1e-251">http:// _server_/_api/search/query?querytext='sharepoint'&amp;trimduplicates=false</span></span>
  
    
    
 <span data-ttu-id="0ef1e-252">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-252">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'TrimDuplicates':'False'
}
```


### <a name="timeout"></a><span data-ttu-id="0ef1e-253">Timeout</span><span class="sxs-lookup"><span data-stu-id="0ef1e-253">Timeout</span></span>
<span data-ttu-id="0ef1e-254"><a name="bk_Timeout"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-254"></span></span>

<span data-ttu-id="0ef1e-255">Zeit in Millisekunden bis zum Timeout der Abfrageanforderung. Der Standardwert ist 30000.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-255">The amount of time in milliseconds before the query request times out. The default value is 30000.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-256">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-256">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-257">http:// _server_/_api/search/query?querytext='sharepoint'&amp;timeout=60000</span><span class="sxs-lookup"><span data-stu-id="0ef1e-257">http:// _server_/_api/search/query?querytext='sharepoint'&amp;timeout=60000</span></span>
  
    
    
 <span data-ttu-id="0ef1e-258">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-258">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'Timeout':'60000'
}
```


### <a name="enablenicknames"></a><span data-ttu-id="0ef1e-259">EnableNicknames</span><span class="sxs-lookup"><span data-stu-id="0ef1e-259">EnableNicknames</span></span>
<span data-ttu-id="0ef1e-260"><a name="bk_EnableNicknames"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-260"></span></span>

<span data-ttu-id="0ef1e-261">Ein boolescher Wert, der angibt, ob die genauen Ausdrücke in der Suchabfrage verwendet werden, um Übereinstimmungen zu finden, oder ob auch Spitznamen verwendet werden</span><span class="sxs-lookup"><span data-stu-id="0ef1e-261">A Boolean value that specifies whether the exact terms in the search query are used to find matches, or if nicknames are used also.</span></span> 
  
    
    
 <span data-ttu-id="0ef1e-p115">**true**, wenn Spitznamen verwendet werden; andernfalls **false**. Der Standardwert ist **false**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p115">**true** if nicknames are used; otherwise, **false**. The default value is **false**.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-264">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-264">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-265">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablenicknames=true</span><span class="sxs-lookup"><span data-stu-id="0ef1e-265">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablenicknames=true</span></span>
  
    
    
 <span data-ttu-id="0ef1e-266">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-266">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'EnableNicknames':'True'
}
```


### <a name="enablephonetic"></a><span data-ttu-id="0ef1e-267">EnablePhonetic</span><span class="sxs-lookup"><span data-stu-id="0ef1e-267">EnablePhonetic</span></span>
<span data-ttu-id="0ef1e-268"><a name="bk_EnablePhonetic"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-268"></span></span>

<span data-ttu-id="0ef1e-269">Ein boolescher Wert, der angibt, ob die phonetische Form der Abfrageausdrücke verwendet wird, um Übereinstimmungen zu finden</span><span class="sxs-lookup"><span data-stu-id="0ef1e-269">A Boolean value that specifies whether the phonetic forms of the query terms are used to find matches.</span></span> 
  
    
    
 <span data-ttu-id="0ef1e-p116">**true**, wenn die phonetische Form verwendet wird; andernfalls **false**. Der Standardwert ist **false**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p116">**true** if phonetic forms are used; otherwise, **false**. The default value is **false**.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-272">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-272">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-273">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablephonetic=true</span><span class="sxs-lookup"><span data-stu-id="0ef1e-273">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablephonetic=true</span></span>
  
    
    
 <span data-ttu-id="0ef1e-274">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-274">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'EnablePhonetic':'True'
}
```


### <a name="enablefql"></a><span data-ttu-id="0ef1e-275">EnableFql</span><span class="sxs-lookup"><span data-stu-id="0ef1e-275">EnableFql</span></span>
<span data-ttu-id="0ef1e-276"><a name="bk_EnableFql"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-276"></span></span>

<span data-ttu-id="0ef1e-277">Ein boolescher Wert, der angibt, ob die Abfrage die FAST Query Language (FQL) verwendet</span><span class="sxs-lookup"><span data-stu-id="0ef1e-277">A Boolean value that specifies whether the query uses the FAST Query Language (FQL).</span></span> 
  
    
    
 <span data-ttu-id="0ef1e-p117">**true**, wenn die Abfrage eine FQL-Abfrage ist; andernfalls **false**. Der Standardwert ist **false**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p117">**true** if the query is an FQL query; otherwise, **false**. The default value is **false**.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-280">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-280">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-281">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablefql=true</span><span class="sxs-lookup"><span data-stu-id="0ef1e-281">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablefql=true</span></span>
  
    
    
 <span data-ttu-id="0ef1e-282">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-282">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'EnableFQL':'True'
}
```


### <a name="hithighlightedproperties"></a><span data-ttu-id="0ef1e-283">HithighlightedProperties</span><span class="sxs-lookup"><span data-stu-id="0ef1e-283">HithighlightedProperties</span></span>
<span data-ttu-id="0ef1e-284"><a name="bk_HithighlightedProperties"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-284"></span></span>

<span data-ttu-id="0ef1e-p118">Eigenschaften zur Hervorhebung in der Suchergebnisübersicht, wenn der Eigenschaftenwert den vom Benutzer eingegebenen Suchbegriffen entspricht. Für **GET**-Anforderungen geben Sie eine Zeichenfolge mit einer durch Kommas getrennten Liste von Eigenschaften an. Für **POST**-Anforderungen geben Sie ein Array von Zeichenfolgen an.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p118">The properties to highlight in the search result summary when the property value matches the search terms entered by the user. For **GET** requests, Specify in a string containing a comma-separated list of properties. For **POST** requests, specify as an array of strings.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-288">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-288">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-289">http:// _server_/_api/search/query?querytext='sharepoint'&amp;hithighlightedproperties='Title'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-289">http:// _server_/_api/search/query?querytext='sharepoint'&amp;hithighlightedproperties='Title'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-290">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-290">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'HitHighlightedProperties' :  {
    'results' : [
         'Title'   
    ]
}
}
```


### <a name="bypassresulttypes"></a><span data-ttu-id="0ef1e-291">BypassResultTypes</span><span class="sxs-lookup"><span data-stu-id="0ef1e-291">BypassResultTypes</span></span>
<span data-ttu-id="0ef1e-292"><a name="bk_BypassResultTypes"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-292"></span></span>

<span data-ttu-id="0ef1e-293">Ein boolescher Wert, der angibt, ob eine Ergebnistypverarbeitung für die Abfrage durchgeführt werden soll</span><span class="sxs-lookup"><span data-stu-id="0ef1e-293">A Boolean value that specifies whether to perform result type processing for the query.</span></span> 
  
    
    
 <span data-ttu-id="0ef1e-p119">**true**, um eine Ereignistypverarbeitung durchzuführen; andernfalls **false**. Der Standardwert ist **false**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p119">**true** to perform result type processing; otherwise, **false**. The default value is **false**.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-296">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-296">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-297">http:// _server_/_api/search/query?querytext='sharepoint'&amp;bypassresulttypes=true</span><span class="sxs-lookup"><span data-stu-id="0ef1e-297">http:// _server_/_api/search/query?querytext='sharepoint'&amp;bypassresulttypes=true</span></span>
  
    
    
 <span data-ttu-id="0ef1e-298">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-298">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'BypassResultTypes' : 'true'
}
```


### <a name="processbestbets"></a><span data-ttu-id="0ef1e-299">ProcessBestBets</span><span class="sxs-lookup"><span data-stu-id="0ef1e-299">ProcessBestBets</span></span>
<span data-ttu-id="0ef1e-300"><a name="bk_ProcessBestBets"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-300"></span></span>

<span data-ttu-id="0ef1e-301">Ein boolescher Wert, der angibt, ob die besten Suchergebnisse für die Abfrage zurückgegeben werden sollen</span><span class="sxs-lookup"><span data-stu-id="0ef1e-301">A Boolean value that specifies whether to return best bet results for the query.</span></span> 
  
    
    
 <span data-ttu-id="0ef1e-p120">**true**, um die besten Suchergebnisse zurückzugeben; andernfalls **false**. Dieser Parameter wird nur verwendet, wenn **EnableQueryRules** auf **true** festgelegt ist. Andernfalls wird er ignoriert. Der Standardwert ist **false**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p120">**true** to return best bets; otherwise, **false**. This parameter is used only when **EnableQueryRules** is set to **true**, otherwise it is ignored. The default value is **false**.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-305">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-305">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-306">http:// _server_/_api/search/query?querytext='sharepoint'&amp;processbestbets=true&amp;enablequeryrules=true</span><span class="sxs-lookup"><span data-stu-id="0ef1e-306">http:// _server_/_api/search/query?querytext='sharepoint'&amp;processbestbets=true&amp;enablequeryrules=true</span></span>
  
    
    
 <span data-ttu-id="0ef1e-307">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-307">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'ProcessBestBets' : 'true',
'EnableQueryRules' : 'true'
}
```


### <a name="clienttype"></a><span data-ttu-id="0ef1e-308">ClientType</span><span class="sxs-lookup"><span data-stu-id="0ef1e-308">ClientType</span></span>
<span data-ttu-id="0ef1e-309"><a name="bk_ClientType"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-309"></span></span>

<span data-ttu-id="0ef1e-310">Typ des Clients, der die Abfrage gesendet hat</span><span class="sxs-lookup"><span data-stu-id="0ef1e-310">The type of the client that issued the query.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-311">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-311">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-312">http:// _server_/_api/search/query?querytext='sharepoint'&amp;clienttype='custom'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-312">http:// _server_/_api/search/query?querytext='sharepoint'&amp;clienttype='custom'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-313">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-313">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'ClientType':'custom'
}
```


### <a name="personalizationdata"></a><span data-ttu-id="0ef1e-314">PersonalizationData</span><span class="sxs-lookup"><span data-stu-id="0ef1e-314">PersonalizationData</span></span>
<span data-ttu-id="0ef1e-315"><a name="bk_PersonalizationData"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-315"></span></span>

<span data-ttu-id="0ef1e-316">GUID für den Benutzer, der die Suchabfrage gesendet hat</span><span class="sxs-lookup"><span data-stu-id="0ef1e-316">The GUID for the user who submitted the search query.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-317">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-317">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-318">http:// _\<server\>_/_api/search/query?querytext='sharepoint'&amp;personalizationdata=' _\<GUID\>_'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-318">http:// _\<server\>_/_api/search/query?querytext='sharepoint'&amp;personalizationdata=' _\<GUID\>_'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-319">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-319">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'PersonalizationData' : ' <GUID> '
}
```


### <a name="resultsurl"></a><span data-ttu-id="0ef1e-320">ResultsURL</span><span class="sxs-lookup"><span data-stu-id="0ef1e-320">ResultsURL</span></span>
<span data-ttu-id="0ef1e-321"><a name="bk_ResultsURL"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-321"></span></span>

<span data-ttu-id="0ef1e-322">URL für die Seite mit den Suchergebnissen</span><span class="sxs-lookup"><span data-stu-id="0ef1e-322">The URL for the search results page.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-323">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-323">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-324">http:// _server_/_api/search/query?querytext='sharepoint'&amp;resultsurl='http://server/site/resultspage.aspx'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-324">http:// _server_/_api/search/query?querytext='sharepoint'&amp;resultsurl='http://server/site/resultspage.aspx'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-325">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-325">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint'
'ResultURL' : 'http://server/site/resultspage.aspx'
}
```


### <a name="querytag"></a><span data-ttu-id="0ef1e-326">QueryTag</span><span class="sxs-lookup"><span data-stu-id="0ef1e-326">QueryTag</span></span>
<span data-ttu-id="0ef1e-327"><a name="bk_QueryTag"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-327"></span></span>

<span data-ttu-id="0ef1e-p121">Benutzerdefinierte Tags, die die Abfrage identifizieren. Sie können mehrere Abfrage-Tags angeben, getrennt durch Semikolons.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p121">Custom tags that identify the query. You can specify multiple query tags, separated by semicolons.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-330">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-330">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-331">http:// _server_/_api/search/query?querytext='sharepoint'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-331">http:// _server_/_api/search/query?querytext='sharepoint'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-332">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-332">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint'
}
```


### <a name="properties"></a><span data-ttu-id="0ef1e-333">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="0ef1e-333">Properties</span></span>
<span data-ttu-id="0ef1e-334"><a name="bk_Properties"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-334"></span></span>

<span data-ttu-id="0ef1e-p122">Zusätzliche Eigenschaften für die Abfrage. **GET**-Anforderungen unterstützen nur Zeichenfolgewerte. **POST**-Anforderungen unterstützen Werte jedes Typs.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p122">Additional properties for the query. **GET** requests support only string values. **POST** requests support values of any type.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-338">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-338">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-339">http:// _server_/_api/search/query?querytext='sharepoint'&amp;properties='termid:guid'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-339">http:// _server_/_api/search/query?querytext='sharepoint'&amp;properties='termid:guid'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-340">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-340">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'Properties' : {
     'results' : [
          {
               'Name' : 'sampleBooleanProperty',
               'Value' :
               {
                    'BoolVal' : 'True',
                    'QueryPropertyValueTypeIndex' : 3
               }
          },
          {
               'Name' : 'sampleIntProperty',
               'Value' : 
               {
                    'IntVal' : '1234',
                    'QueryPropertyValueTypeIndex' : 2
               }
          }
     ]
}
}
```


> <span data-ttu-id="0ef1e-341">**Hinweis:** [QueryPropertyValueType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.QueryPropertyValueType.aspx) gibt den Typ der Eigenschaft an. Jeder Typ weist einen bestimmten Indexwert auf.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-341">Note  QueryPropertyValueType specifies the type for the property; each type has a specific index value.</span></span>
  
    
    


### <a name="enablequeryrules"></a><span data-ttu-id="0ef1e-342">EnableQueryRules</span><span class="sxs-lookup"><span data-stu-id="0ef1e-342">EnableQueryRules</span></span>
<span data-ttu-id="0ef1e-343"><a name="bk_EnableQueryRules"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-343"></span></span>

<span data-ttu-id="0ef1e-344">Ein boolescher Wert, der angibt, ob Abfrageregeln für die Abfrage aktiviert werden</span><span class="sxs-lookup"><span data-stu-id="0ef1e-344">A Boolean value that specifies whether to enable query rules for the query.</span></span> 
  
    
    
 <span data-ttu-id="0ef1e-p123">**true**, um Abfrageregeln zu aktivieren; andernfalls **false**. Der Standardwert ist **true**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p123">**true** to enable query rules; otherwise, **false**. The default value is **true**.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-347">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-347">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-348">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablequeryrules=false</span><span class="sxs-lookup"><span data-stu-id="0ef1e-348">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablequeryrules=false</span></span>
  
    
    
 <span data-ttu-id="0ef1e-349">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-349">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'EnableQueryRules' : 'false' 
}
```


### <a name="reorderingrules"></a><span data-ttu-id="0ef1e-350">ReorderingRules</span><span class="sxs-lookup"><span data-stu-id="0ef1e-350">ReorderingRules</span></span>
<span data-ttu-id="0ef1e-351"><a name="bk_ReorderingRules"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-351"></span></span>

<span data-ttu-id="0ef1e-p124">Spezielle Regeln für die Neuanordnung der Suchergebnisse. Diese Regeln können angeben, dass Dokumente, die bestimmte Bedingungen erfüllen, weiter oben oder unten in den Ergebnissen platziert werden. Diese Eigenschaft wird nur angewendet, wenn die Suchergebnisse basierend auf dem Rang sortiert sind. Sie müssen eine **POST**-Anforderung für diese Eigenschaft verwenden; dies funktioniert nicht für eine **GET**-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p124">Special rules for reordering search results. These rules can specify that documents matching certain conditions are ranked higher or lower in the results. This property applies only when search results are sorted based on rank. You must use a **POST** request for this property; it does not work in a **GET** request.</span></span>
  
    
    
<span data-ttu-id="0ef1e-p125">Im folgenden Beispiel bezieht sich  _MatchType_ auf [ReorderingRuleMatchType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ReorderingRuleMatchType.aspx) . Im folgenden Beispiel spezifiziert `'MatchType' : '0'` Folgendes: [ResultContainsKeyword](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ReorderingRuleMatchType.ResultContainsKeyword.aspx) .</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p125">In the following example,  _MatchType_ refers to [ReorderingRuleMatchType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ReorderingRuleMatchType.aspx) . In the following example, `'MatchType' : '0'` specifies [ResultContainsKeyword](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ReorderingRuleMatchType.ResultContainsKeyword.aspx) .</span></span>
  
    
    
 <span data-ttu-id="0ef1e-358">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-358">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'ReorderingRules' :  {
    'results' : [
         {
             'MatchValue' : '<someValue>',
             'Boost' : '10',
             'MatchType' : '0'
         }
    ]
}
}
```


### <a name="processpersonalfavorites"></a><span data-ttu-id="0ef1e-359">ProcessPersonalFavorites</span><span class="sxs-lookup"><span data-stu-id="0ef1e-359">ProcessPersonalFavorites</span></span>
<span data-ttu-id="0ef1e-360"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-360"></span></span>

<span data-ttu-id="0ef1e-361">Ein boolescher Wert, der angibt, ob persönliche Favoriten in den Suchergebnissen zurückgegeben werden</span><span class="sxs-lookup"><span data-stu-id="0ef1e-361">A Boolean value that specifies whether to return personal favorites with the search results.</span></span> 
  
    
    
 <span data-ttu-id="0ef1e-362">**true**, um persönliche Favoriten zurückzugeben; andernfalls **false**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-362">**true** to return personal favorites; otherwise **false**.</span></span> 
  
    
    
 <span data-ttu-id="0ef1e-363">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-363">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-364">http:// _server_/_api/search/query?querytext='sharepoint'&amp;processpersonalfavorites=true</span><span class="sxs-lookup"><span data-stu-id="0ef1e-364">http:// _server_/_api/search/query?querytext='sharepoint'&amp;processpersonalfavorites=true</span></span>
  
    
    
 <span data-ttu-id="0ef1e-365">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-365">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'ProcessPersonalFavorites' : 'false'
}
```


### <a name="querytemplatepropertiesurl"></a><span data-ttu-id="0ef1e-366">QueryTemplatePropertiesUrl</span><span class="sxs-lookup"><span data-stu-id="0ef1e-366">QueryTemplatePropertiesUrl</span></span>
<span data-ttu-id="0ef1e-367"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-367"></span></span>

<span data-ttu-id="0ef1e-p126">Speicherort der Datei queryparametertemplate.xml. Diese Datei wird verwendet, um anonymen Benutzern das Senden von Search-REST-Abfragen zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p126">The location of the queryparametertemplate.xml file. This file is used to enable anonymous users to make Search REST queries.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-370">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-370">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-371">http:// _server_/_api/search/query?querytext='sharepoint'&amp;querytemplatepropertiesurl='spfile://webroot/queryparametertemplate.xml'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-371">http:// _server_/_api/search/query?querytext='sharepoint'&amp;querytemplatepropertiesurl='spfile://webroot/queryparametertemplate.xml'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-372">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-372">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
QueryTemplatePropertiesUrl : 'spfile://webroot/queryparametertemplate.xml'
}
```


### <a name="hithighlightedmultivaluepropertylimit"></a><span data-ttu-id="0ef1e-373">HitHighlightedMultivaluePropertyLimit</span><span class="sxs-lookup"><span data-stu-id="0ef1e-373">HitHighlightedMultivaluePropertyLimit</span></span>
<span data-ttu-id="0ef1e-374"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-374"></span></span>

<span data-ttu-id="0ef1e-375">Anzahl der Eigenschaften für die Anzeige der Treffermarkierung in den Suchergebnissen</span><span class="sxs-lookup"><span data-stu-id="0ef1e-375">The number of properties to show hit highlighting for in the search results.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-376">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-376">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-377">http:// _server_/_api/search/query?querytext='sharepoint'&amp;hithighlightedmultivaluepropertylimit=2</span><span class="sxs-lookup"><span data-stu-id="0ef1e-377">http:// _server_/_api/search/query?querytext='sharepoint'&amp;hithighlightedmultivaluepropertylimit=2</span></span>
  
    
    
 <span data-ttu-id="0ef1e-378">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-378">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'HitHighlihtedMultivaluePropertyLimit' : '2'
}
```


### <a name="enableorderinghithighlightedproperty"></a><span data-ttu-id="0ef1e-379">EnableOrderingHitHighlightedProperty</span><span class="sxs-lookup"><span data-stu-id="0ef1e-379">EnableOrderingHitHighlightedProperty</span></span>
<span data-ttu-id="0ef1e-380"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-380"></span></span>

<span data-ttu-id="0ef1e-381">Ein boolescher Wert, der angibt, ob die Eigenschaften für die Treffermarkierung sortiert werden können</span><span class="sxs-lookup"><span data-stu-id="0ef1e-381">A Boolean value that specifies whether the hit highlighted properties can be ordered.</span></span> 
  
    
    
 <span data-ttu-id="0ef1e-382">**true**, um Sortierungsregeln zu aktivieren; andernfalls **false**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-382">**true** to enable ordering rules; otherwise **false**.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-383">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-383">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-384">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enableorderinghithighlightedproperty=false</span><span class="sxs-lookup"><span data-stu-id="0ef1e-384">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enableorderinghithighlightedproperty=false</span></span>
  
    
    
 <span data-ttu-id="0ef1e-385">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-385">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'EnableOrderingHitHighlightedProperty' : 'false'
}
```


### <a name="collapsespecification"></a><span data-ttu-id="0ef1e-386">CollapseSpecification</span><span class="sxs-lookup"><span data-stu-id="0ef1e-386">CollapseSpecification</span></span>
<span data-ttu-id="0ef1e-387"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-387"></span></span>

<span data-ttu-id="0ef1e-p127">Verwaltete Eigenschaften zum Reduzieren einzelner Suchergebnisse. Ergebnisse werden auf ein Ergebnis oder eine angegebene Anzahl von Ergebnissen reduziert, wenn sie beliebigen individuellen Reduzierungsspezifikationen entsprechen. In einer einzelnen Reduzierungsspezifikation werden die Ergebnisse reduziert, wenn ihre Eigenschaften allen individuellen Eigenschaften in der Reduzierungsspezifikation entsprechen.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p127">The managed properties that are used to determine how to collapse individual search results. Results are collapsed into one or a specified number of results if they match any of the individual collapse specifications. Within a single collapse specification, results are collapsed if their properties match all individual properties in the collapse specification.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-391">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-391">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-392">http:// _server_/_api/search/query?querytext='sharepoint'&amp;collapsespecification='Author:1 ContentType:2'</span><span class="sxs-lookup"><span data-stu-id="0ef1e-392">http:// _server_/_api/search/query?querytext='sharepoint'&amp;collapsespecification='Author:1 ContentType:2'</span></span>
  
    
    
 <span data-ttu-id="0ef1e-393">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-393">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'CollapseSpecification' : 'Author:1 ContentType:2'
}
```


### <a name="enablesorting"></a><span data-ttu-id="0ef1e-394">EnableSorting</span><span class="sxs-lookup"><span data-stu-id="0ef1e-394">EnableSorting</span></span>
<span data-ttu-id="0ef1e-395"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-395"></span></span>

<span data-ttu-id="0ef1e-396">Ein boolescher Wert, der angibt, ob die Suchergebnisse sortiert werden</span><span class="sxs-lookup"><span data-stu-id="0ef1e-396">A Boolean value that specifies whether to sort search results.</span></span> 
  
    
    
<span data-ttu-id="0ef1e-p128">I **true**, um die Suchergebnisse mit  _SortList_ oder nach Rang zu sortieren, wenn _SortList_ leer ist. **false**, um die Ergebnisse nicht zu sortieren.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p128">I **true** to sort search results using _SortList_, or by rank if  _SortList_ is empty. **false** to leave results unsorted.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-399">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-399">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-400">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablesorting=false</span><span class="sxs-lookup"><span data-stu-id="0ef1e-400">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablesorting=false</span></span>
  
    
    
 <span data-ttu-id="0ef1e-401">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-401">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'EnableSorting' : 'false'
}
```


### <a name="generateblockranklog"></a><span data-ttu-id="0ef1e-402">GenerateBlockRankLog</span><span class="sxs-lookup"><span data-stu-id="0ef1e-402">GenerateBlockRankLog</span></span>
<span data-ttu-id="0ef1e-403"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-403"></span></span>

<span data-ttu-id="0ef1e-p129">Ein boolescher Wert, der angibt, ob Blockrang-Protokollinformationen in der Eigenschaft **BlockRankLog** der überlappenden Ergebnistabelle zurückgegeben werden. Ein Blockrang-Protokoll enthält die Textinformationen zur Blockbewertung und die Dokumente, die dedupliziert wurden.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p129">A Boolean value that specifies whether to return block rank log information in the **BlockRankLog** property of the interleaved result table. A block rank log contains the textual information on the block score and the documents that were de-duplicated.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-406">**true**, um Blockrang-Protokollinformationen zurückzugeben; andernfalls **false**.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-406">**true** to return block rank log information; otherwise, **false**.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-407">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-407">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-408">http:// _server_/_api/search/query?querytext='sharepoint'&amp;generateblockranklog=true</span><span class="sxs-lookup"><span data-stu-id="0ef1e-408">http:// _server_/_api/search/query?querytext='sharepoint'&amp;generateblockranklog=true</span></span>
  
    
    
 <span data-ttu-id="0ef1e-409">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-409">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'GenerateBlockRankLog' : 'true'
}
```


### <a name="uilanguage"></a><span data-ttu-id="0ef1e-410">UIlanguage</span><span class="sxs-lookup"><span data-stu-id="0ef1e-410">UIlanguage</span></span>
<span data-ttu-id="0ef1e-411"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-411"></span></span>

<span data-ttu-id="0ef1e-412">Gebietsschema-ID (LCID) der Benutzeroberfläche (siehe  [Von Microsoft zugewiesene Gebietsschema-IDs](http://msdn.microsoft.com/en-us/goglobal/bb964664)).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-412">The locale identifier (LCID) of the user interface (see  [Locale IDs Assigned by Microsoft](http://msdn.microsoft.com/en-us/goglobal/bb964664)).</span></span>
  
    
    
 <span data-ttu-id="0ef1e-413">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-413">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-414">http:// _server_/_api/search/query?querytext='sharepoint'&amp;uilanguage=1044</span><span class="sxs-lookup"><span data-stu-id="0ef1e-414">http:// _server_/_api/search/query?querytext='sharepoint'&amp;uilanguage=1044</span></span>
  
    
    
 <span data-ttu-id="0ef1e-415">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-415">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'UILanguage' : '1044'
}
```


### <a name="desiredsnippetlength"></a><span data-ttu-id="0ef1e-416">DesiredSnippetLength</span><span class="sxs-lookup"><span data-stu-id="0ef1e-416">DesiredSnippetLength</span></span>
<span data-ttu-id="0ef1e-417"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-417"></span></span>

<span data-ttu-id="0ef1e-418">Bevorzugte Anzahl von Zeichen in der Treffermarkierungsübersicht für ein Suchergebnis</span><span class="sxs-lookup"><span data-stu-id="0ef1e-418">The preferred number of characters to display in the hit-highlighted summary generated for a search result.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-419">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-419">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-420">http:// _server_/_api/search/query?querytext='sharepoint'&amp;desiredsnippetlength=80</span><span class="sxs-lookup"><span data-stu-id="0ef1e-420">http:// _server_/_api/search/query?querytext='sharepoint'&amp;desiredsnippetlength=80</span></span>
  
    
    
 <span data-ttu-id="0ef1e-421">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-421">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'DesiredSnippetLength' : '80'
}
```


### <a name="maxsnippetlength"></a><span data-ttu-id="0ef1e-422">MaxSnippetLength</span><span class="sxs-lookup"><span data-stu-id="0ef1e-422">MaxSnippetLength</span></span>
<span data-ttu-id="0ef1e-423"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-423"></span></span>

<span data-ttu-id="0ef1e-424">Maximale Anzahl von Zeichen in der Treffermarkierungsübersicht für ein Suchergebnis</span><span class="sxs-lookup"><span data-stu-id="0ef1e-424">The maximum number of characters to display in the hit-highlighted summary generated for a search result.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-425">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-425">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-426">http:// _server_/_api/search/query?querytext='sharepoint'&amp;maxsnippetlength=100</span><span class="sxs-lookup"><span data-stu-id="0ef1e-426">http:// _server_/_api/search/query?querytext='sharepoint'&amp;maxsnippetlength=100</span></span>
  
    
    
 <span data-ttu-id="0ef1e-427">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-427">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'MaxSnippetLength' : '100' 
}
```


### <a name="summarylength"></a><span data-ttu-id="0ef1e-428">SummaryLength</span><span class="sxs-lookup"><span data-stu-id="0ef1e-428">SummaryLength</span></span>
<span data-ttu-id="0ef1e-429"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-429"></span></span>

<span data-ttu-id="0ef1e-430">Anzahl der Zeichen in der Ergebnisübersicht für ein Suchergebnis</span><span class="sxs-lookup"><span data-stu-id="0ef1e-430">The number of characters to display in the result summary for a search result.</span></span>
  
    
    
 <span data-ttu-id="0ef1e-431">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-431">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="0ef1e-432">http:// _server_/_api/search/query?querytext='sharepoint'&amp;summarylength=150</span><span class="sxs-lookup"><span data-stu-id="0ef1e-432">http:// _server_/_api/search/query?querytext='sharepoint'&amp;summarylength=150</span></span>
  
    
    
 <span data-ttu-id="0ef1e-433">**Beispiel für POST-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-433">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'Summarylength' : '150'
}
```


## <a name="enabling-anonymous-search-rest-queries"></a><span data-ttu-id="0ef1e-434">Ermöglichen anonymer Search-REST-Abfragen</span><span class="sxs-lookup"><span data-stu-id="0ef1e-434">Enabling anonymous Search REST queries</span></span>
<span data-ttu-id="0ef1e-435"><a name="bk_AnonymousREST"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-435"></span></span>

<span data-ttu-id="0ef1e-p130">Sie können die Suche konfigurieren, um Search-REST-Abfragen von anonymen Benutzern zu unterstützen. Websiteadministratoren können entscheiden, welche Abfrageparameter unter Verwendung der Datei queryparametertemplate.xml anonymen Benutzern zur Verfügung gestellt werden. Dieser Abschnitt beschreibt die Konfiguration Ihrer Website, um anonymen Zugriff zu ermöglichen und die Datei queryparametertemplate.xml zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p130">You can configure search to support Search REST queries from anonymous users. Site administrators can decide what query parameters to expose to anonymous users by using the queryparametertemplate.xml file. This section describes how to configure your site to enable anonymous access, and create the queryparametertemplate.xml file.</span></span>
  
    
    

### <a name="to-enable-anonymous-search-rest-queries"></a><span data-ttu-id="0ef1e-439">So ermöglichen Sie anonyme Search-REST-Abfragen</span><span class="sxs-lookup"><span data-stu-id="0ef1e-439">To enable anonymous Search REST queries</span></span>


1. <span data-ttu-id="0ef1e-p131">Ermöglichen Sie den anonymen Zugriff auf die Webanwendung und Veröffentlichungswebsite. Weitere Informationen erhalten Sie unter  [Verwalten von Berechtigungsrichtlinien für eine Webanwendung in SharePoint](http://technet.microsoft.com/en-us/library/ff608071.aspx) und [Planen der Benutzerauthentifizierungsmethoden in SharePoint](http://technet.microsoft.com/en-us/library/cc262350.aspx) in [TechNet](http://technet.microsoft.com/en-US/).</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p131">Enable anonymous access on the web application and publishing site. For more information about how to do this, see  [Manage permission policies for a web application in SharePoint](http://technet.microsoft.com/en-us/library/ff608071.aspx) and [Plan for user authentication methods in SharePoint](http://technet.microsoft.com/en-us/library/cc262350.aspx) on [TechNet](http://technet.microsoft.com/en-US/).</span></span>
    
  
2. <span data-ttu-id="0ef1e-442">Fügen Sie eine neue Dokumentbibliothek namens QueryPropertiesTemplate zur Veröffentlichungswebsite hinzu.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-442">Add a new document library named QueryPropertiesTemplate to the publishing site.</span></span>
    
  
3. <span data-ttu-id="0ef1e-443">Erstellen Sie eine XML-Datei namens queryparametertemplate.xml, und kopieren Sie die folgende XML in die Datei.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-443">Create an XML file named queryparametertemplate.xml, and copy the following XML to the file.</span></span>
    
```XML
  
<QueryPropertiesTemplate xmlns="http://www.microsoft.com/sharepoint/search/KnownTypes/2008/08" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <QueryProperties i:type="KeywordQueryProperties">
        <EnableStemming>true</EnableStemming>
        <FarmId>FarmID</FarmId>
        <IgnoreAllNoiseQuery>true</IgnoreAllNoiseQuery>
        <KeywordInclusion>AllKeywords</KeywordInclusion>
        <SiteId>SiteID</SiteId>
        <SummaryLength>180</SummaryLength>
        <TrimDuplicates>true</TrimDuplicates>
        <WcfTimeout>120000</WcfTimeout>
        <WebId>WebID</WebId>
        <Properties xmlns:a="http://schemas.microsoft.com/2003/10/Serialization/Arrays">
            <a:KeyValueOfstringanyType>
                <a:Key>_IsEntSearchLicensed</a:Key>
                <a:Value i:type="b:boolean" xmlns:b="http://www.w3.org/2001/XMLSchema">true</a:Value>
            </a:KeyValueOfstringanyType>
            <a:KeyValueOfstringanyType>
                <a:Key>EnableSorting</a:Key>
                <a:Value i:type="b:boolean" xmlns:b="http://www.w3.org/2001/XMLSchema">true</a:Value>
            </a:KeyValueOfstringanyType>
            <a:KeyValueOfstringanyType>
                <a:Key>MaxKeywordQueryTextLength</a:Key>
                <a:Value i:type="b:int" xmlns:b="http://www.w3.org/2001/XMLSchema">4096</a:Value>
            </a:KeyValueOfstringanyType>
            <a:KeyValueOfstringanyType>
                <a:Key>TryCache</a:Key>
                <a:Value i:type="b:boolean" xmlns:b="http://www.w3.org/2001/XMLSchema">true</a:Value>
            </a:KeyValueOfstringanyType>
        </Properties>
        <PropertiesContractVersion>15.0.0.0</PropertiesContractVersion>
        <EnableFQL>false</EnableFQL>
        <EnableSpellcheck>Suggest</EnableSpellcheck>
        <EnableUrlSmashing>true</EnableUrlSmashing>
        <IsCachable>false</IsCachable>
        <MaxShallowRefinementHits>100</MaxShallowRefinementHits>
        <MaxSummaryLength>185</MaxSummaryLength>
        <MaxUrlLength>2048</MaxUrlLength>
        <SimilarType>None</SimilarType>
        <SortSimilar>true</SortSimilar>
        <TrimDuplicatesIncludeId>0</TrimDuplicatesIncludeId>
        <TrimDuplicatesKeepCount>1</TrimDuplicatesKeepCount>
    </QueryProperties>
    <WhiteList xmlns:a="http://schemas.microsoft.com/2003/10/Serialization/Arrays">
        <a:string>RowLimit</a:string>
        <a:string>SortList</a:string>
        <a:string>StartRow</a:string>
        <a:string>RefinementFilters</a:string>
        <a:string>Culture</a:string>
        <a:string>RankingModelId</a:string>
        <a:string>TrimDuplicatesIncludeId</a:string>
        <a:string>ReorderingRules</a:string>
        <a:string>EnableQueryRules</a:string>
        <a:string>HiddenConstraints</a:string>
        <a:string>QueryText</a:string>
        <a:string>QueryTemplate</a:string>
    </WhiteList>
</QueryPropertiesTemplate>
```

4. <span data-ttu-id="0ef1e-444">Aktualisieren Sie die Elemente  _SiteId_,  _FarmId_ und _WebId_ mit den Werten für Ihre Farm-, Website- und Veröffentlichungswebsitesammlung.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-444">Update the  _SiteId_,  _FarmId_, and  _WebId_ elements with the values for your farm, website and publishing site collection.</span></span>
    
  
5. <span data-ttu-id="0ef1e-445">Speichern Sie die queryparametertemplate.xml in der QueryPropertiesTemplate-Dokumentbibliothek.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-445">Save queryparametertemplate.xml to the QueryPropertiesTemplate document library.</span></span>
    
  
6. <span data-ttu-id="0ef1e-446">Fügen Sie den  _QueryTemplatePropertiesUrl_-Parameter zu Ihrem Search-REST-Aufruf hinzu, und geben Sie spfile://webroot/queryparametertemplate.xml als Wert an.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-446">Add the  _QueryTemplatePropertiesUrl_ parameter to your Search REST call, specifyingspfile://webroot/queryparametertemplate.xml as the value.</span></span>
    
  

### <a name="queryparametertemplatexml-file"></a><span data-ttu-id="0ef1e-447">Datei "queryparametertemplate.xml"</span><span class="sxs-lookup"><span data-stu-id="0ef1e-447">queryparametertemplate.xml file</span></span>

<span data-ttu-id="0ef1e-448">Die wichtigsten Elemente in der Datei "queryparametertemplate.xml" sind:</span><span class="sxs-lookup"><span data-stu-id="0ef1e-448">The primary elements in the queryparametertemplate.xml file are:</span></span>
  
    
    

- <span data-ttu-id="0ef1e-449">Element **QueryProperties**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-449">**QueryProperties** element</span></span>
  
    
    
<span data-ttu-id="0ef1e-450">Enthält ein serialisiertes  [QueryProperties](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.QueryProperties.aspx) -Objekt.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-450">Contains a serialized  [QueryProperties](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.QueryProperties.aspx) object.</span></span>
    
  
- <span data-ttu-id="0ef1e-451">Element **WhiteList**</span><span class="sxs-lookup"><span data-stu-id="0ef1e-451">**WhiteList** element</span></span>
  
    
    
<span data-ttu-id="0ef1e-452">Enthält die Liste der Abfrageeigenschaften, die der anonyme Benutzer festlegen darf.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-452">Contains the list of query properties that the anonymous user is allowed to set.</span></span>
    
  
<span data-ttu-id="0ef1e-p132">Wenn eine anonyme Search-REST-Abfrage gesendet wird, wird das Abfrageobjekt mit den Informationen im **QueryProperties**-Element erstellt. Dann werden alle Eigenschaften in der Positivliste aus der eingehenden Abfrage in das neu erstellte Abfrageobjekt kopiert.</span><span class="sxs-lookup"><span data-stu-id="0ef1e-p132">When an anonymous Search REST query is submitted, the query object is constructed using what's specified in the **QueryProperties** element. Then, all the properties that are listed in the whitelist are copied from the incoming query to the newly constructed query object.</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="0ef1e-455">Inhalt dieses Abschnitts</span><span class="sxs-lookup"><span data-stu-id="0ef1e-455">In this section</span></span>
<span data-ttu-id="0ef1e-456"><a name="bk_AnonymousREST"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-456"></span></span>

-  [<span data-ttu-id="0ef1e-457">Abrufen von Abfragevorschläge mithilfe des Suche REST-Diensts</span><span class="sxs-lookup"><span data-stu-id="0ef1e-457">Retrieving query suggestions using the Search REST service</span></span>](retrieving-query-suggestions-using-the-search-rest-service.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="0ef1e-458">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="0ef1e-458">Additional resources</span></span>
<span data-ttu-id="0ef1e-459"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="0ef1e-459"></span></span>


-  [<span data-ttu-id="0ef1e-460">Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="0ef1e-460">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0ef1e-461">SharePoint: Verwenden des Search-REST-Diensts über eine App für SharePoint</span><span class="sxs-lookup"><span data-stu-id="0ef1e-461">SharePoint: Using the search REST service from an app for SharePoint</span></span>](http://code.msdn.microsoft.com/sharepoint/SharePoint-Perform-a-1bf3e87d)
    
  
-  [<span data-ttu-id="0ef1e-462">What's new in SharePoint-Suche für Entwickler</span><span class="sxs-lookup"><span data-stu-id="0ef1e-462">What's new in SharePoint search for developers</span></span>](what-s-new-in-sharepoint-search-for-developers.md)
    
  
-  [<span data-ttu-id="0ef1e-463">Programmieren mit dem SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="0ef1e-463">Use OData query operations in SharePoint REST requests</span></span>](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  

  
    
    

