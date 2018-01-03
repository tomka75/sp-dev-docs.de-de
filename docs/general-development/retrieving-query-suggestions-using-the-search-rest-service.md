---
title: "Abrufen von Abfragevorschläge mithilfe des Such-REST-Diensts"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a64c5bec-64a8-4752-9c72-433d1c864aed
ms.openlocfilehash: 64f07696df6df14756303a53dd75f41de9ccbdbf
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="retrieving-query-suggestions-using-the-search-rest-service"></a><span data-ttu-id="407c4-102">Abrufen von Abfragevorschläge mithilfe des Search-REST-Diensts</span><span class="sxs-lookup"><span data-stu-id="407c4-102">Retrieving query suggestions using the Search REST service</span></span>
<span data-ttu-id="407c4-103">Erfahren Sie, wie Sie den Search-REST-Dienst aus Ihren Client- und mobilen Anwendungen verwenden können, um Abfragevorschläge aus der Suche in SharePoint abzurufen.</span><span class="sxs-lookup"><span data-stu-id="407c4-103">Learn how you can use the Search REST service from your client and mobile applications to retrieve query suggestions from Search in SharePoint.</span></span>
<span data-ttu-id="407c4-104">Abfragevorschläge, auch Suchvorschläge genannt, sind Ausdrücke, nach denen Benutzer bereits gesucht haben und die beim Eingeben einer Abfrage angezeigt oder "vorgeschlagen" werden.</span><span class="sxs-lookup"><span data-stu-id="407c4-104">Query suggestions, also known as search suggestions, are phrases that users have already searched for and that are displayed or "suggested" to them as they type their queries.</span></span> <span data-ttu-id="407c4-105">Über die Suche in SharePoint können Sie die Vorschläge nach und vor der Abfrage aktivieren.</span><span class="sxs-lookup"><span data-stu-id="407c4-105">You can use Search in SharePoint to turn on pre-query and post-query suggestions.</span></span> <span data-ttu-id="407c4-106">Die Vorschläge werden in einer Liste unter dem Suchfeld angezeigt, während der Benutzer eine Abfrage eingibt.</span><span class="sxs-lookup"><span data-stu-id="407c4-106">These suggestions appear in a list below the Search box as a user types a query.</span></span> <span data-ttu-id="407c4-107">Weitere Informationen zu Abfragevorschlägen und deren Aktivierung finden Sie unter [Verwalten von Abfragevorschlägen in SharePoint]((http://technet.microsoft.com/de-DE/library/jj721441.aspx)).</span><span class="sxs-lookup"><span data-stu-id="407c4-107">For more information about query suggestions and how to enable them, see  [Manage query suggestions in SharePoint]((http://technet.microsoft.com/de-DE/library/jj721441.aspx)).</span></span>
  
    
    


## <a name="suggest-endpoint-in-the-search-rest-service"></a><span data-ttu-id="407c4-108">Vorschlagen eines Endpunkts im Search-REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="407c4-108">Suggest endpoint in the Search REST service</span></span>
<span data-ttu-id="407c4-109"><a name="bk_SuggestEndpoint"> </a></span><span class="sxs-lookup"><span data-stu-id="407c4-109"><a name="bk_SuggestEndpoint"> </a></span></span>

<span data-ttu-id="407c4-110">Der Search-REST-Dienst enthält einen **Suggest** -Endpunkt, den Sie verwenden können, in jeder Technologie, die unterstützt der REST-Webanfragen Abfragevorschläge abgerufen, die das Suchsystem für eine Abfrage von Client oder mobilen Anwendungen generiert.</span><span class="sxs-lookup"><span data-stu-id="407c4-110">The Search REST service includes a **Suggest** endpoint you can use in any technology that supports REST web requests to retrieve query suggestions that the search system generates for a query from client or mobile applications.</span></span>
  
    
    
<span data-ttu-id="407c4-111">Der URI für **GET** Anforderungen an die Search-REST-Dienst **Suggest** Endpunkt ist:</span><span class="sxs-lookup"><span data-stu-id="407c4-111">The URI for **GET** requests to the Search REST service's **Suggest** endpoint is:</span></span>
  
    
    
 `/_api/search/suggest`
  
    
    
<span data-ttu-id="407c4-p102">Die Parameter für die Abfragevorschläge werden in der URL angegeben. Sie können die Anforderungs-URL auf zwei Arten erstellen:</span><span class="sxs-lookup"><span data-stu-id="407c4-p102">The query suggestion parameters are specified in the URL. You can construct the request URL in two ways:</span></span>
  
    
    


  
    
    
>  `http://server/_api/search/suggest?parameter=value&amp;parameter=value`
    
  

  
    
    
>  `http://server/_api/search/suggest(parameter=value&amp;parameter=value)`
    
  
> [!NOTE]
> <span data-ttu-id="407c4-114">Der Search-REST-Dienst unterstützt keine anonyme Anfragen an den Endpunkt **Suggest**.</span><span class="sxs-lookup"><span data-stu-id="407c4-114">**Note:** The Search REST service doesn't support anonymous requests to the Suggest endpoint.</span></span>
  
    
    


## <a name="query-suggestion-parameters"></a><span data-ttu-id="407c4-115">Parameter für die Abfragevorschläge</span><span class="sxs-lookup"><span data-stu-id="407c4-115">Query suggestion parameters</span></span>
<span data-ttu-id="407c4-116"><a name="bk_SuggestParameters"> </a></span><span class="sxs-lookup"><span data-stu-id="407c4-116"><a name="bk_SuggestParameters"> </a></span></span>

<span data-ttu-id="407c4-117">Den folgenden Abschnitten werden die Parameter, die Sie für den Endpunkt **Suggest** verwenden können.</span><span class="sxs-lookup"><span data-stu-id="407c4-117">The following sections describe the parameters you can use for the **Suggest** endpoint.</span></span>
  
    
    

### <a name="querytext"></a><span data-ttu-id="407c4-118">Abfragetext</span><span class="sxs-lookup"><span data-stu-id="407c4-118">Querytext</span></span>

<span data-ttu-id="407c4-119">Eine Zeichenfolge, die den Text für die Suchabfrage enthält</span><span class="sxs-lookup"><span data-stu-id="407c4-119">A string that contains the text for the search query.</span></span>
  
    
    
 <span data-ttu-id="407c4-120">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="407c4-120">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="407c4-121">http:// _server_/_api/search/suggest?querytext = "Sharepoint"</span><span class="sxs-lookup"><span data-stu-id="407c4-121">http:// _server_/_api/search/suggest?querytext='sharepoint'</span></span>
  
    
    

### <a name="inumberofquerysuggestions"></a><span data-ttu-id="407c4-122">iNumberOfQuerySuggestions</span><span class="sxs-lookup"><span data-stu-id="407c4-122">iNumberOfQuerySuggestions</span></span>

<span data-ttu-id="407c4-p103">Die Anzahl der Abfragevorschläge abgerufen. Muss größer als 0 (null) sein. Der Standardwert ist 5.</span><span class="sxs-lookup"><span data-stu-id="407c4-p103">The number of query suggestions to retrieve. Must be greater than zero (0). The default value is 5.</span></span>
  
    
    
 <span data-ttu-id="407c4-126">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="407c4-126">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="407c4-127">http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Inumberofquerysuggestions = 3</span><span class="sxs-lookup"><span data-stu-id="407c4-127">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;inumberofquerysuggestions=3</span></span>
  
    
    

### <a name="inumberofresultsuggestions"></a><span data-ttu-id="407c4-128">iNumberOfResultSuggestions</span><span class="sxs-lookup"><span data-stu-id="407c4-128">iNumberOfResultSuggestions</span></span>

<span data-ttu-id="407c4-p104">Die Anzahl der persönlichen Ergebnisse abgerufen. Muss größer als 0 (null) sein. Der Standardwert ist 5.</span><span class="sxs-lookup"><span data-stu-id="407c4-p104">The number of personal results to retrieve. Must be greater than zero (0). The default value is 5.</span></span>
  
    
    
 <span data-ttu-id="407c4-132">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="407c4-132">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="407c4-133">http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Inumberofresultsuggestions = 4</span><span class="sxs-lookup"><span data-stu-id="407c4-133">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;inumberofresultsuggestions=4</span></span>
  
    
    

### <a name="fprequerysuggestions"></a><span data-ttu-id="407c4-134">fPreQuerySuggestions</span><span class="sxs-lookup"><span data-stu-id="407c4-134">fPreQuerySuggestions</span></span>

<span data-ttu-id="407c4-p105">Ein boolescher Wert, der angibt, ob Vorschläge vor der Abfrage oder nach der Abfrage abgerufen. **true** Vorschläge vor der Abfrage zurückzugebenden; andernfalls **false**. Der Standardwert ist **false**.</span><span class="sxs-lookup"><span data-stu-id="407c4-p105">A Boolean value that specifies whether to retrieve pre-query or post-query suggestions. **true** to return pre-query suggestions; otherwise, **false**. The default value is **false**.</span></span>
  
    
    
 <span data-ttu-id="407c4-138">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="407c4-138">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="407c4-139">http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Fprequerysuggestions = True</span><span class="sxs-lookup"><span data-stu-id="407c4-139">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;fprequerysuggestions=true</span></span>
  
    
    

### <a name="fhithighlighting"></a><span data-ttu-id="407c4-140">fHitHighlighting</span><span class="sxs-lookup"><span data-stu-id="407c4-140">fHitHighlighting</span></span>

<span data-ttu-id="407c4-p106">Ein boolescher Wert, der angibt, ob Treffer hervorheben oder Abfragevorschläge fett formatiert. **true** fett formatiert die Ausdrücke in den zurückgegebenen Abfragevorschläge, die Ausdrücke in der angegebenen Abfrage übereinstimmen; andernfalls **false**. Der Standardwert ist **true**.</span><span class="sxs-lookup"><span data-stu-id="407c4-p106">A Boolean value that specifies whether to hit-highlight or format in bold the query suggestions. **true** to format in bold the terms in the returned query suggestions that match terms in the specified query; otherwise, **false**. The default value is **true**.</span></span>
  
    
    
 <span data-ttu-id="407c4-144">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="407c4-144">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="407c4-145">http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Fhithighlighting = False</span><span class="sxs-lookup"><span data-stu-id="407c4-145">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;fhithighlighting=false</span></span>
  
    
    

### <a name="fcapitalizefirstletters"></a><span data-ttu-id="407c4-146">fCapitalizeFirstLetters</span><span class="sxs-lookup"><span data-stu-id="407c4-146">fCapitalizeFirstLetters</span></span>

<span data-ttu-id="407c4-p107">Ein boolescher Wert, der angibt, ob für die Großschreibung des ersten Buchstabens in jeden Ausdruck in der zurückgegebenen Abfragevorschläge. **true** für die Großschreibung des ersten Buchstabens in jeden Ausdruck; andernfalls **false**. Der Standardwert ist **false**.</span><span class="sxs-lookup"><span data-stu-id="407c4-p107">A Boolean value that specifies whether to capitalize the first letter in each term in the returned query suggestions. **true** to capitalize the first letter in each term; otherwise, **false**. The default value is **false**.</span></span>
  
    
    
 <span data-ttu-id="407c4-150">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="407c4-150">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="407c4-151">http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Fcapitalizefirstletters = False</span><span class="sxs-lookup"><span data-stu-id="407c4-151">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;fcapitalizefirstletters=false</span></span>
  
    
    

### <a name="culture"></a><span data-ttu-id="407c4-152">Culture</span><span class="sxs-lookup"><span data-stu-id="407c4-152">Culture</span></span>

<span data-ttu-id="407c4-153">Gebietsschema-ID (LCID) für die Abfrage (siehe  [Von Microsoft zugewiesene Gebietsschema-IDs]((http://msdn.microsoft.com/de-DE/goglobal/bb964664.aspx))).</span><span class="sxs-lookup"><span data-stu-id="407c4-153">The locale ID (LCID) for the query (see  [Locale IDs Assigned by Microsoft]((http://msdn.microsoft.com/de-DE/goglobal/bb964664.aspx))).</span></span>
  
    
    
 <span data-ttu-id="407c4-154">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="407c4-154">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="407c4-155">http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Culture = 1044</span><span class="sxs-lookup"><span data-stu-id="407c4-155">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;culture=1044</span></span>
  
    
    

### <a name="enablestemming"></a><span data-ttu-id="407c4-156">EnableStemming</span><span class="sxs-lookup"><span data-stu-id="407c4-156">EnableStemming</span></span>

<span data-ttu-id="407c4-p108">Ein boolescher Wert, der angibt, ob die wortstammerkennung aktiviert ist. **true** zum Aktivieren der wortstammerkennung; andernfalls **false**. Der Standardwert ist **true**.</span><span class="sxs-lookup"><span data-stu-id="407c4-p108">A Boolean value that specifies whether stemming is enabled. **true** to enable stemming; otherwise, **false**. The default value is **true**.</span></span>
  
    
    
 <span data-ttu-id="407c4-160">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="407c4-160">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="407c4-161">http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Enablestemming = False</span><span class="sxs-lookup"><span data-stu-id="407c4-161">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;enablestemming=false</span></span>
  
    
    

### <a name="showpeoplenamesuggestions"></a><span data-ttu-id="407c4-162">ShowPeopleNameSuggestions</span><span class="sxs-lookup"><span data-stu-id="407c4-162">ShowPeopleNameSuggestions</span></span>

<span data-ttu-id="407c4-p109">Ein boolescher Wert, der angibt, ob in der zurückgegebenen Abfragevorschläge Personennamen eingeschlossen. **true** Personennamen in der zurückgegebenen Abfragevorschläge enthalten; andernfalls **false**. Der Standardwert ist **true**.</span><span class="sxs-lookup"><span data-stu-id="407c4-p109">A Boolean value that specifies whether to include people names in the returned query suggestions. **true** to include people names in the returned query suggestions; otherwise, **false**. The default value is **true**.</span></span>
  
    
    
 <span data-ttu-id="407c4-166">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="407c4-166">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="407c4-167">http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Showpeoplenamesuggestions = False</span><span class="sxs-lookup"><span data-stu-id="407c4-167">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;showpeoplenamesuggestions=false</span></span>
  
    
    

### <a name="enablequeryrules"></a><span data-ttu-id="407c4-168">EnableQueryRules</span><span class="sxs-lookup"><span data-stu-id="407c4-168">EnableQueryRules</span></span>

<span data-ttu-id="407c4-p110">Ein boolescher Wert, der angibt, ob Abfrageregeln für diese Abfrage zu aktivieren. **true** um Abfrageregeln zu aktivieren; andernfalls **false**. Der Standardwert ist **true**.</span><span class="sxs-lookup"><span data-stu-id="407c4-p110">A Boolean value that specifies whether to turn on query rules for this query. **true** to turn on query rules; otherwise, **false**. The default value is **true**.</span></span>
  
    
    
 <span data-ttu-id="407c4-172">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="407c4-172">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="407c4-173">http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Enablequeryrules = False</span><span class="sxs-lookup"><span data-stu-id="407c4-173">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;enablequeryrules=false</span></span>
  
    
    

### <a name="fprefixmatchallterms"></a><span data-ttu-id="407c4-174">fPrefixMatchAllTerms</span><span class="sxs-lookup"><span data-stu-id="407c4-174">fPrefixMatchAllTerms</span></span>

<span data-ttu-id="407c4-p111">Ein boolescher Wert, der angibt, ob Abfragevorschläge zurückgegeben für Präfix übereinstimmt. **true** zurückzugebenden Abfragevorschläge basierend auf Präfix entspricht, andernfalls **false** beim Abfragevorschläge das vollständige Abfragewort übereinstimmen soll.</span><span class="sxs-lookup"><span data-stu-id="407c4-p111">A Boolean value that specifies whether to return query suggestions for prefix matches. **true** to return query suggestions based on prefix matches, otherwise, **false** when query suggestions should match the full query word.</span></span>
  
    
    
 <span data-ttu-id="407c4-177">**Beispiel für GET-Anforderung**</span><span class="sxs-lookup"><span data-stu-id="407c4-177">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="407c4-178">http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Fprefixmatchallterms = False</span><span class="sxs-lookup"><span data-stu-id="407c4-178">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;fprefixmatchallterms=false</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="407c4-179">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="407c4-179">See also</span></span>
<span data-ttu-id="407c4-180"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="407c4-180"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="407c4-181">Übersicht über die REST-API der SharePoint-Suche</span><span class="sxs-lookup"><span data-stu-id="407c4-181">SharePoint Search REST API overview</span></span>](sharepoint-search-rest-api-overview.md)
    
  
-  [<span data-ttu-id="407c4-182">Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="407c4-182">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  <span data-ttu-id="407c4-183">[SharePoint: Verwenden des Search-REST-Diensts über eine App für SharePoint]((http://code.msdn.microsoft.com/sharepoint/SharePoint-Perform-a-1bf3e87d))</span><span class="sxs-lookup"><span data-stu-id="407c4-183">[SharePoint: Using the search REST service from an app for SharePoint]((http://code.msdn.microsoft.com/sharepoint/SharePoint-Perform-a-1bf3e87d))</span></span>
    
  
-  [<span data-ttu-id="407c4-184">What's new in SharePoint-Suche für Entwickler</span><span class="sxs-lookup"><span data-stu-id="407c4-184">What's new in SharePoint search for developers</span></span>](what-s-new-in-sharepoint-search-for-developers.md)
    
  
-  <span data-ttu-id="407c4-185">[Programmieren mit dem SharePoint REST-Dienst]((http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx))</span><span class="sxs-lookup"><span data-stu-id="407c4-185">[Use OData query operations in SharePoint REST requests]((http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx))</span></span>
    
  

  
    
    

