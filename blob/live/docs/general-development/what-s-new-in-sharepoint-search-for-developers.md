---
title: "Neuerungen für Entwickler bei der SharePoint-Suche"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: b8d69685-3612-421e-b011-50b4d580d461
ms.openlocfilehash: aa3e8633312ee6fa814a7e9bb0152d131e30b799
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-in-sharepoint-search-for-developers"></a><span data-ttu-id="ff1fb-102">Neuerungen für Entwickler bei der SharePoint-Suche</span><span class="sxs-lookup"><span data-stu-id="ff1fb-102">What's new in SharePoint search for developers</span></span>
<span data-ttu-id="ff1fb-103">Informationen Sie zu den neuen Features für Entwickler bei der Suche in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-103">Learn about the new features available for developers in Search in SharePoint.</span></span>
## <a name="search-client-object-model-for-access-to-query-object-model-functionality-for-online-on-premises-and-mobile-development"></a><span data-ttu-id="ff1fb-104">Search-Clientobjektmodell für den Zugriff auf die Funktionalität des Objektmodells für online Abfragen, lokalen und Mobilgeräte-Entwicklung</span><span class="sxs-lookup"><span data-stu-id="ff1fb-104">Search client object model for access to Query object model functionality for online, on-premises, and mobile development</span></span>
<span data-ttu-id="ff1fb-105"><a name="SPSearchnew_clientOM"> </a></span><span class="sxs-lookup"><span data-stu-id="ff1fb-105"></span></span>

<span data-ttu-id="ff1fb-p101">SharePoint Suche enthält ein Clientobjektmodell (CSOM), die Zugriff auf die Funktionalität des Abfrage-Objektmodells für die meisten online ermöglicht, lokalen und Mobilgeräte-Entwicklung. Dem Search-Clientobjektmodell können zum Erstellen von Clientanwendungen, die auf einem Computer ausgeführt werden, die keinen SharePoint installiert haben, um Suchergebnisse SharePoint zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p101">SharePoint Search includes a client object model (CSOM) that enables access to most of the Query object model functionality for online, on-premises, and mobile development. You can use the Search CSOM to create client applications that run on a machine that does not have SharePoint installed to return SharePoint search results.</span></span>
  
    
    
<span data-ttu-id="ff1fb-p102">Die Suche CSOM besteht aus einem verwalteten Clientobjektmodell Microsoft .NET Framework und JavaScript-Objektmodell, und es basiert auf SharePoint. Erstens greift Clientcode des SharePoint-CSOM auf. Klicken Sie dann auf Clientcode die Suche CSOM zugegriffen.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p102">The Search CSOM includes a Microsoft .NET Framework managed client object model and JavaScript object model, and it is built on SharePoint. First, client code accesses the SharePoint CSOM. Then, client code accesses the Search CSOM.</span></span> 
  
    
    
<span data-ttu-id="ff1fb-p103">Verwenden die Suche .NET Framework verwaltetes CSOM, Sie müssen eine  [ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx) -Instanz (befindet sich im Namespace [Microsoft.SharePoint.Client](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.aspx) in der Microsoft.SharePoint.Client.dll) abrufen. Klicken Sie dann mithilfe des-Objektmodells im [Microsoft.SharePoint.Client.Search.Query](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.aspx) -Namespace in der Microsoft.Office.Server.Search.Client.dll. Weitere Informationen zu SharePoint-CSOM finden Sie unter [Verwaltetes Clientobjektmodell](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx). Weitere Informationen zum **ClientContext** -Objekt, das den Einstiegspunkt für das CSOM ist, finden Sie unter [Clientkontext als zentrales Objekt](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p103">To use the Search .NET Framework managed CSOM, you must get a  [ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx) instance (located in the [Microsoft.SharePoint.Client](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.aspx) namespace in the Microsoft.SharePoint.Client.dll). Then, use the object model in the [Microsoft.SharePoint.Client.Search.Query](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.aspx) namespace in the Microsoft.Office.Server.Search.Client.dll. For more information about the SharePoint CSOM, see [SharePoint 2010 Client Object Model](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx). For more information about the **ClientContext** object, which is the entry point to the CSOM, see [Client Context as Central Object](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="ff1fb-p104">Die Search-CSOM zurückgegeben Search Results Daten vom Server in JavaScript Object Notation (JSON). Für die Suche Ergebnisdaten die JSON enthält eine  [ResultTableCollection](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.ResultTableCollection.aspx) -Auflistung zusammengesetzten von [ResultTable](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.ResultTable.aspx) -Objekten, die unterschiedliche Resultsets darstellen.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p104">The Search CSOM returns the search results data from the server in JavaScript Object Notation (JSON). The JSON for the search results data contains a  [ResultTableCollection](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.ResultTableCollection.aspx) collection composed of [ResultTable](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.ResultTable.aspx) objects that represent different result sets.</span></span>
  
    
    

## <a name="sql-syntax-support-removed"></a><span data-ttu-id="ff1fb-117">Unterstützung für SQL-Syntax entfernt</span><span class="sxs-lookup"><span data-stu-id="ff1fb-117">SQL Syntax Support Removed</span></span>
<span data-ttu-id="ff1fb-118"><a name="SP15Searchnew_support"> </a></span><span class="sxs-lookup"><span data-stu-id="ff1fb-118"></span></span>

<span data-ttu-id="ff1fb-119">Benutzerdefinierte Suchlösungen in SharePoint bieten keine Unterstützung für [SQL-Syntax](http://msdn.microsoft.com/de-DE/library/ee558869).</span><span class="sxs-lookup"><span data-stu-id="ff1fb-119">Custom search solutions in SharePoint do not support  [SQL syntax](http://msdn.microsoft.com/de-DE/library/ee558869).</span></span> <span data-ttu-id="ff1fb-120">Die SharePoint-Suche unterstützt FQL-Syntax und KQL-Syntax für benutzerdefinierte Suchlösungen.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-120">Search in SharePoint supports FQL syntax and KQL syntax for custom search solutions.</span></span> <span data-ttu-id="ff1fb-121">In benutzerdefinierten Suchlösungen können Sie keine SQL-Syntax verwenden. Das gilt unabhängig von der eingesetzten Technologie und damit auch bei Verwendung des Abfrageserver-Objektmodells, des Clientobjektmodells und des REST-Suchdiensts.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-121">You cannot use SQL syntax in custom search solutions using any technologies, including the Query server object model, the client object model, and the Search REST service.</span></span> <span data-ttu-id="ff1fb-122">In früheren SharePoint-Versionen erstellte benutzerdefinierte Suchlösungen, in denen SQL-Syntax mit dem Abfrageserver-Objektmodell und dem Abfragewebdienst verwendet wird, funktionieren nach einem Upgrade auf SharePoint nicht mehr.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-122">Custom search solutions that use SQL syntax with the Query server object model and the Query web service that were created in earlier versions of SharePoint Server will not work when you upgrade them to SharePoint.</span></span> <span data-ttu-id="ff1fb-123">Über diese Anwendungen gesendete Abfragen geben einen Fehler zurück.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-123">Queries submitted via these applications will return an error.</span></span> <span data-ttu-id="ff1fb-124">Weitere Informationen zur Verwendung von FQL- und KQL-Syntax finden Sie unter [Syntaxreferenz für die Keyword Query Language (KQL)](keyword-query-language-kql-syntax-reference.md) sowie unter [Syntaxreferenz für die FAST Query Language (FQL.md)](fast-query-language-fql-syntax-reference.md).</span><span class="sxs-lookup"><span data-stu-id="ff1fb-124">For more information about using FQL syntax and KQL syntax, see  [Keyword Query Language (KQL) syntax reference](keyword-query-language-kql-syntax-reference.md) and [FAST Query Language (FQL.md) syntax reference](fast-query-language-fql-syntax-reference.md).</span></span>
  
    
    

## <a name="search-rest-service-for-remote-execution-of-queries-from-client-applications"></a><span data-ttu-id="ff1fb-125">REST-Suchdienst für die Remoteausführung von Abfragen über Clientanwendungen</span><span class="sxs-lookup"><span data-stu-id="ff1fb-125">Search REST service for remote execution of queries from client applications</span></span>
<span data-ttu-id="ff1fb-126"><a name="SP15Searchnew_support"> </a></span><span class="sxs-lookup"><span data-stu-id="ff1fb-126"></span></span>

<span data-ttu-id="ff1fb-127">In SharePoint ist ein REST-Dienst (Representational State Transfer) integriert, mit dem Sie über Clientanwendungen Remoteabfragen an den SharePoint-Suchdienst senden können. Für diese Abfragen können Sie jede Technologie verwenden, die REST-Webanforderungen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-127">SharePoint Server 2013 includes a Representational State Transfer (REST) service that enables you to remotely execute queries against the SharePoint Search service from client applications by using any technology that supports REST web requests. The Search REST service exposes two endpoints, query and suggest, and will support both GET and POST operations. Results are returned in either XML or JSON format.</span></span> <span data-ttu-id="ff1fb-128">Der REST-Suchdienst macht zwei Endpunkte verfügbar (**query** und **suggest**) und unterstützt sowohl Operationen des Typs **GET** als auch Operationen des Typs **POST**.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-128">The Search REST service exposes two endpoints, **query** and **suggest**, and will support both **GET** and **POST** operations.</span></span> <span data-ttu-id="ff1fb-129">Die Ergebnisse werden entweder im XML-Format oder im JSON-Format zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-129">Results are returned in either XML or JSON format.</span></span>
  
    
    
<span data-ttu-id="ff1fb-p107">Dies ist der Zugriffspunkt für den Dienst:  `http://server/_api/search/`. Sie können die Website auch wie folgt in der URL angeben:  `http://server/site/_api/search/`. Der Suchdienst gibt Ergebnisse aus der gesamten Websitesammlung zurück. Es werden also die gleichen Ergebnisse bei beiden Arten des Zugriffs auf den Dienst zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p107">The following is the access point for the service:  `http://server/_api/search/`. You can also specify the site in the URL, as follows:  `http://server/site/_api/search/`. The search service returns results from the entire site collection, so the same results are returned for both ways to access the service.</span></span>
  
    
    
<span data-ttu-id="ff1fb-p108">Sie können auch die URL, die Zugriff auf den Dienst wie folgt client.svc verweist:  `http://server/_vti_bin/client.svc/search/`. Die Verwendung von  `_api` ist jedoch die bevorzugte Konvention.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p108">You can also use the URL that references client.svc to access the service, as follows:  `http://server/_vti_bin/client.svc/search/`. However, using  `_api` is the preferred convention.</span></span>
  
    
    
<span data-ttu-id="ff1fb-135">Verwenden Sie den folgenden Zugriffspunkt Zugriff auf die webdienstmetadaten:</span><span class="sxs-lookup"><span data-stu-id="ff1fb-135">Use the following access point to access the service metadata:</span></span> 
  
    
    
 `http://server/_api/$metadata`
  
    
    
<span data-ttu-id="ff1fb-136">Allgemeine Informationen über den REST-Dienst in SharePoint finden Sie unter  [Programmieren mit dem SharePoint REST-Dienst](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff1fb-136">For general information about the REST service in SharePoint, see  [Use OData query operations in SharePoint REST requests](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="sharepoint-search-query-web-service-is-deprecated"></a><span data-ttu-id="ff1fb-137">SharePoint-Suchabfrage-Webdienst ist veraltet.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-137">SharePoint Search Query web service is deprecated</span></span>
<span data-ttu-id="ff1fb-138"><a name="SP15Searchnew_support"> </a></span><span class="sxs-lookup"><span data-stu-id="ff1fb-138"></span></span>

<span data-ttu-id="ff1fb-p109">Der Query-Webdienst (befindet sich in dem Pfad  `http://server/site/_vti_bin/search.asmx`) ist in SharePoint veraltet. Wenn Sie neue Anwendungen schreiben, vermeiden Sie die Verwendung dieses veralteten Features, und verwenden Sie stattdessen den neuen Abfrage CSOM oder Abfrage REST-Dienst. Wenn Sie vorhandene Anwendungen ändern, empfehlen wir dringend empfohlen, keine Abhängigkeit dieses Feature zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p109">The Query web service (located in the path  `http://server/site/_vti_bin/search.asmx`) is deprecated in SharePoint. If you write new applications, avoid using this deprecated feature and instead use the new Query CSOM or Query REST service. If you modify existing applications, we strongly encourage you to remove any dependency on this feature.</span></span>
  
    
    

## <a name="sharepoint-search-query-object-model-enhancements"></a><span data-ttu-id="ff1fb-142">SharePoint Search-Objektmodell Abfragevorgängen</span><span class="sxs-lookup"><span data-stu-id="ff1fb-142">SharePoint Search Query object model enhancements</span></span>
<span data-ttu-id="ff1fb-143"><a name="SP15Searchnew_support"> </a></span><span class="sxs-lookup"><span data-stu-id="ff1fb-143"></span></span>

<span data-ttu-id="ff1fb-p110">Eigenschaften von Abfrage enthalten Informationen zu einer Suchabfrage. Eine Eigenschaftensammlung wurde in SharePoint suchen die Abfrage und Ergebnisse Klassen zum Aktivieren der benutzerdefinierte Abfrageeigenschaften hinzugefügt. Sie können vorhandene Abfrageeigenschaften über die Eigenschaft auf eine der Abfrageklassen wie folgt zugreifen:</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p110">Query properties provide information about a search query. In SharePoint Search, a property bag was added to the query and result classes to enable user-defined query properties. You can access existing query properties via the property on one of the query classes, as follows:</span></span> 
  
    
    
 `KeywordQuery.EnableStemming`
  
    
    
<span data-ttu-id="ff1fb-147">Sie können auch den Eigenschaftenbehälter wie folgt:</span><span class="sxs-lookup"><span data-stu-id="ff1fb-147">Or you can use the property bag, as follows:</span></span> 
  
    
    
 `KeywordQuery.Properties["EnableStemming"]`
  
    
    
<span data-ttu-id="ff1fb-148">Sie können benutzerdefinierte Eigenschaften zugreifen, nur mithilfe der Eigenschaftensammlung wie folgt:</span><span class="sxs-lookup"><span data-stu-id="ff1fb-148">You can access user-defined properties only by using the property bag, as follows:</span></span> 
  
    
    
 `KeywordQuery.Properties["UserDefinedProperty"]`
  
    
    
<span data-ttu-id="ff1fb-149">SharePoint Suche schließt Abfrageeigenschaften im Eigenschaftenbehälter, einschließlich der neuen Abfrageeigenschaften wie etwa:</span><span class="sxs-lookup"><span data-stu-id="ff1fb-149">SharePoint Search includes query properties in the property bag, including new query properties such as:</span></span>
  
    
    

- <span data-ttu-id="ff1fb-p111">**BypassResultTypes** Gibt an, ob die Suche Ergebniselementtyp für den Abfrageergebnissen zurückgegeben wird. Geben Sie **true** zum Zurückgeben von kein Ergebnistyp. andernfalls **false**.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p111">**BypassResultTypes** Specifies whether the search result item type is returned for the query results. Specify **true** to return no result type; otherwise, **false**.</span></span>
    
  
- <span data-ttu-id="ff1fb-p112">**EnableInterleaving** Gibt an, ob die Ergebnissätze, die durch Ausführen von abfrageregelaktionen zum Hinzufügen eines ergebnisblocks generiert mit dem Resultset für die ursprüngliche Abfrage verwendet werden. Geben Sie **true**, um die generierte Ergebnismenge mit dem ursprünglichen Resultset mischen. andernfalls **false**.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p112">**EnableInterleaving** Specifies whether the result sets generated by executing query rule actions to add a result block are mixed with the result set for the original query. Specify **true** to mix the generated result set with the original result set; otherwise, **false**.</span></span>
    
  
- <span data-ttu-id="ff1fb-p113">**EnableQueryRules** Gibt an, ob Abfrageregeln für diese Abfrage aktiviert sind. **true** zum Aktivieren von Abfrageregeln für die Abfrage angeben. andernfalls **false**.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p113">**EnableQueryRules** Specifies whether query rules are turned on for this query. Specify **true** to enable query rules for the query; otherwise, **false**.</span></span>
    
  
<span data-ttu-id="ff1fb-p114">Sie können eine beliebige Eigenschaft im Eigenschaftenbehälter, einschließlich der benutzerdefinierten Eigenschaften als abfrageregelbedingungen angeben. Verwenden Sie Abfrageregeln zum Anpassen des Suchvorgangs für die Arten von Abfragen, die für Ihre Benutzer wichtig sind. Wenn eine Abfrage in einer Abfrageregel angegebene Bedingungen entspricht, gibt die Regel Benutzeraktionen zum Verbessern der Relevanz der Suchergebnisse zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p114">You can specify any property in the property bag, including user-defined properties, as query rule conditions. You use query rules to customize the search experience for the kinds of queries that are important to your users. When a query meets conditions specified in a query rule, the rule specifies actions to improve the relevance of the associated search results.</span></span> 
  
    
    

## <a name="keyword-query-language-enhancements"></a><span data-ttu-id="ff1fb-159">Schlüsselwort Sprache Abfragevorgängen</span><span class="sxs-lookup"><span data-stu-id="ff1fb-159">Keyword query language enhancements</span></span>
<span data-ttu-id="ff1fb-160"><a name="SP15Searchnew_support"> </a></span><span class="sxs-lookup"><span data-stu-id="ff1fb-160"></span></span>

<span data-ttu-id="ff1fb-161">SharePoint enthält Verbesserungen an der Schlüsselwort-Abfragesprache, die in diesem Abschnitt beschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-161">SharePoint includes improvements to the Keyword query language, which are described in this section.</span></span> 
  
    
    

### <a name="improved-near-operator"></a><span data-ttu-id="ff1fb-162">Verbesserte NEAR-operator</span><span class="sxs-lookup"><span data-stu-id="ff1fb-162">Improved NEAR operator</span></span>

<span data-ttu-id="ff1fb-p115">In SharePoint Server 2010 Operators **NEAR** impliziert einen token maximalen Abstand von **8** und die Reihenfolge der Eingabe Token beibehalten. In SharePoint behält der Operator **NEAR** nicht mehr die Reihenfolge der Token. Darüber hinaus erhält der Operator **NEAR** jetzt einen optionalen Parameter, der maximalen token Abstand angibt. Der Standardwert ist jedoch weiterhin **8**. Wenn Sie das vorherige Verhalten verwenden müssen, verwenden Sie stattdessen **ONEAR**.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p115">In SharePoint Server 2010, the **NEAR** operator implied a maximum token distance of **8** and preserved the ordering of the input tokens. In SharePoint, the **NEAR** operator no longer preserves the ordering of tokens. In addition, the **NEAR** operator now receives an optional parameter that indicates maximum token distance. However, the default value is still **8**. If you must use the previous behavior, use **ONEAR** instead.</span></span>
  
    
    
<span data-ttu-id="ff1fb-168">Der **NEAR** -Operator kann in Eigenschaft Einschränkung Ausdrücken verwendet werden, wie im folgenden Beispiel dargestellt:</span><span class="sxs-lookup"><span data-stu-id="ff1fb-168">The **NEAR** operator can be used in property restriction expressions, as shown in the following example:</span></span>
  
    
    
 `"acquisition" NEAR "debt"`
  
    
    
<span data-ttu-id="ff1fb-p116">Diese Abfrage stimmt exakt mit Elementen, in dem das Token "Erwerb" und "Forderung" innerhalb desselben Dokuments, mit einer maximalen token Abstand von **8** angezeigt (der Standardwert der _n_ ist, wenn kein Wert angegeben ist). Die Reihenfolge der Token ist nicht von Bedeutung für die Übereinstimmung.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p116">This query matches items where the tokens "acquisition" and "debt" appear within the same document, with a maximum token distance of **8** (which is the default value of _n_ if no value is provided). The order of the tokens is not significant for the match.</span></span>
  
    
    
<span data-ttu-id="ff1fb-171">Wenn Sie einen geringeren token Abstand benötigen, können Sie es wie folgt angeben:</span><span class="sxs-lookup"><span data-stu-id="ff1fb-171">If you require a smaller token distance, you can specify it as follows:</span></span>
  
    
    
 `"acquisition" NEAR(n=3) "debt"`
  
    
    
<span data-ttu-id="ff1fb-p117">Diese Abfrage stimmt exakt Elemente, in denen die beiden Token "Erwerb" und "Forderung" innerhalb desselben Dokuments, mit einer maximalen token Abstand von **3** angezeigt werden. Die Reihenfolge der Token ist nicht von Bedeutung für die Übereinstimmung.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p117">This query matches items where the two tokens "acquisition" and "debt" appear within the same document, with a maximum token distance of **3**. The order of the tokens is not significant for the match.</span></span>
  
    
    

### <a name="new-onear-operator"></a><span data-ttu-id="ff1fb-174">Neue ONEAR-operator</span><span class="sxs-lookup"><span data-stu-id="ff1fb-174">New ONEAR operator</span></span>

<span data-ttu-id="ff1fb-p118">Der Operator **ONEAR** stellt in der Nähe geordnete Funktionalität bereit. Er empfängt optionalen Parameter, der maximalen token Abstand angibt. Der Standardwert ist **8**.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p118">The **ONEAR** operator provides ordered near functionality. It receives an optional parameter that indicates maximum token distance; the default value is **8**.</span></span>
  
    
    
<span data-ttu-id="ff1fb-p119">Der Operator **ONEAR** behält die Reihenfolge der Eingabe Ausdrücke. Verwenden Sie für ungeordnete Nähe **NEAR**.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p119">The **ONEAR** operator preserves the order of the input expressions. For unordered proximity, use **NEAR**.</span></span>
  
    
    
<span data-ttu-id="ff1fb-179">Den Operator **ONEAR** können in Eigenschaft Einschränkung Ausdrücken wie im folgenden Beispiel dargestellt:</span><span class="sxs-lookup"><span data-stu-id="ff1fb-179">You can use the **ONEAR** operator in property restriction expressions, as shown in the following example:</span></span>
  
    
    
 `"acquisition" ONEAR "debt"`
  
    
    
<span data-ttu-id="ff1fb-p120">Diese Abfrage stimmt exakt Elemente, in denen die beiden Token "Erwerb" und "Forderung" angezeigt werden, innerhalb desselben Dokuments, mit einer maximalen token Abstand von **8** (die den Standardwert _n_ ist, wenn kein Wert angegeben ist). Die Reihenfolge der Token muss für ein Element, das zurückgegeben werden übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p120">This query matches items where the two tokens "acquisition" and "debt" appear within the same document, with a maximum token distance of **8** (which is the default value of _n_ if no value is provided). The order of the tokens must match for an item to be returned.</span></span>
  
    
    
<span data-ttu-id="ff1fb-182">Wenn Sie einen geringeren token Abstand benötigen, können Sie es wie folgt angeben:</span><span class="sxs-lookup"><span data-stu-id="ff1fb-182">If you require a smaller token distance, you can specify it as follows:</span></span>
  
    
    
 `"acquisition" ONEAR(n=3) "debt"`
  
    
    
<span data-ttu-id="ff1fb-p121">Diese Abfrage stimmt exakt Elemente, in denen die beiden Token "Erwerb" und "Forderung" innerhalb desselben Dokuments, mit einer maximalen token Abstand von **3** angezeigt werden. Die Reihenfolge der Token muss für ein Element, das zurückgegeben werden übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p121">This query matches items where the two tokens "acquisition" and "debt" appear within the same document, with a maximum token distance of **3**. The order of the tokens must match for an item to be returned.</span></span>
  
    
    

### <a name="new-xrank-operator"></a><span data-ttu-id="ff1fb-185">Neue XRANK-operator</span><span class="sxs-lookup"><span data-stu-id="ff1fb-185">New XRANK operator</span></span>

<span data-ttu-id="ff1fb-p122">In SharePoint Server 2010 war der **XRANK** Operator nur mit FAST Query Language (FQL) verfügbar. SharePoint führt einen neuen und leistungsstarken **XRANK** -Operator.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p122">In SharePoint Server 2010, the **XRANK** operator was available only with FAST Query language (FQL). SharePoint introduces a new and powerful **XRANK** operator.</span></span>
  
    
    
<span data-ttu-id="ff1fb-p123">Der Operator **XRANK** bietet dynamische Steuerung der Rangordnung. Dieser Operator steigert die dynamische Rangfolge der Elemente, die auf Basis des Vorkommens bestimmter Angaben ohne Ändern der Elemente, die mit die Abfrage übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p123">The **XRANK** operator provides dynamic control of ranking. This operator boosts the dynamic rank of items based on the occurrence of certain terms without changing items that match the query.</span></span>
  
    
    

## <a name="rich-results-framework-for-customizing-search-results-ui"></a><span data-ttu-id="ff1fb-190">Rich-Ergebnis-Framework für das Anpassen der Benutzeroberfläche für Suchergebnisse</span><span class="sxs-lookup"><span data-stu-id="ff1fb-190">Rich results framework for customizing search results UI</span></span>
<span data-ttu-id="ff1fb-191"><a name="SP15Searchnew_support"> </a></span><span class="sxs-lookup"><span data-stu-id="ff1fb-191"></span></span>

<span data-ttu-id="ff1fb-p124">SharePoint Suche umfasst ein neue Framework Ergebnisse, das zum Anpassen der Darstellung (Aussehen und Verhalten) über die Search Results-Benutzeroberfläche (UI) erleichtert. Nun können Sie anstelle von Schreiben von benutzerdefiniertem XSLT zum Ändern der Anzeige von Suchergebnissen aus, die Darstellung der wichtige Typen von Ergebnissen mithilfe von Anzeigevorlagen und Ergebnistypen anpassen.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p124">SharePoint Search includes a new results framework that makes it easy to customize the appearance (look and feel) of the search results user interface (UI). Now, instead of writing a custom XSLT to change how search results are displayed, you can customize the appearance of important types of results by using display templates and result types.</span></span>
  
    
    

### <a name="display-templates"></a><span data-ttu-id="ff1fb-194">Anzeigevorlagen</span><span class="sxs-lookup"><span data-stu-id="ff1fb-194">Display templates</span></span>

<span data-ttu-id="ff1fb-p125">Anzeigevorlagen definieren das visuelle Layout und das Verhalten der einen Ergebnistyp mithilfe von HTML und CSS- JavaScript. Anpassen die vorhandenen Anzeigevorlagen oder Erstellen von Anzeigevorlagen mithilfe ein HTML-Editor, und Laden Sie sie in der Galerieansicht Vorlagen.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p125">Display templates define the visual layout and behavior of a result type by using HTML, CSS, and JavaScript. You can customize the existing display templates or create display templates by using an HTML editor and upload them to the display templates gallery.</span></span>
  
    
    

### <a name="result-types"></a><span data-ttu-id="ff1fb-197">Ergebnistypen</span><span class="sxs-lookup"><span data-stu-id="ff1fb-197">Result types</span></span>

<span data-ttu-id="ff1fb-198">Ergebnistypen definieren, wie Sie eine Reihe von Suchergebnisse basierend auf einer der folgenden Auflistung anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="ff1fb-198">Result types define how to display a set of search results based on a collection of the following:</span></span>
  
    
    

- <span data-ttu-id="ff1fb-p126">**Regeln** Bestimmen Sie, wann einen Ergebnistyp basierend auf den angegebenen Bedingungen gelten. Regelbedingungen können mithilfe von Gleichheit, Vergleichsoperatoren und logischen Operatoren verknüpft werden.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p126">**Rules** Determine when to apply a result type, based on the specified conditions. Rule conditions can be joined by using equality, comparison, and logical operators.</span></span>
    
  
- <span data-ttu-id="ff1fb-p127">**Eigenschaften** Bestimmen Sie die Liste der verwalteten Eigenschaften für das Ergebnis. Sie müssen verwaltete Eigenschaften zur Liste hinzufügen, bevor Sie eine Anzeigevorlage die verwaltete Eigenschaft zuordnen.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p127">**Properties** Determine the list of managed properties for the result. You must add managed properties to the list before you map the managed property to a display template.</span></span>
    
  
- <span data-ttu-id="ff1fb-203">**Anzeigevorlagen** Definieren Sie das visuelle Layout des Ergebnistyps.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-203">**Display templates** Define the visual layout of the result type.</span></span>
    
  
<span data-ttu-id="ff1fb-204">Administratoren können erstellen und Verwalten von Ergebnistypen auf Standortebene oder dienstanwendungsebene; keine benutzerdefinierte Codierung ist erforderlich.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-204">Administrators can create and manage result types at the site level or service application level; no custom coding is required.</span></span>
  
    
    

## <a name="connector-framework-enhancements"></a><span data-ttu-id="ff1fb-205">Connector-Framework-Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="ff1fb-205">Connector framework enhancements</span></span>
<span data-ttu-id="ff1fb-206"><a name="SP15Searchnew_support"> </a></span><span class="sxs-lookup"><span data-stu-id="ff1fb-206"></span></span>

<span data-ttu-id="ff1fb-207">SharePoint Suchen können Sie abrufen Anspruchsinformationen für Inhalte, die in benutzerdefinierten externen Datenquellen, die mithilfe des Frameworks Connector gecrawlt werden.</span><span class="sxs-lookup"><span data-stu-id="ff1fb-207">SharePoint Search enables you to retrieve claims information for content stored in custom external data sources that are crawled by using the connector framework.</span></span>
  
    
    
<span data-ttu-id="ff1fb-p128">Das konnektorframework bietet auch verbesserte Ausnahme erfassen und Protokollierung, um Ihnen bei der Problembehandlung für Fehler beim Crawlen von Inhaltsquellen mit benutzerdefinierten Connectors, die auf das konnektorframework aufbauen. Informationen über das konnektorframework finden Sie unter  [Connector Framework für die Suche in SharePoint](search-connector-framework-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="ff1fb-p128">The connector framework also provides improved exception capturing and logging to help you troubleshoot errors encountered when crawling content sources using custom connectors that are built on top of the connector framework. For information about the connector framework, see  [Search connector framework in SharePoint](search-connector-framework-in-sharepoint.md).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="ff1fb-210">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="ff1fb-210">Additional resources</span></span>
<span data-ttu-id="ff1fb-211"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ff1fb-211"></span></span>


-  [<span data-ttu-id="ff1fb-212">Durchsuchen neuer Inhalte mit SharePoint-Suche</span><span class="sxs-lookup"><span data-stu-id="ff1fb-212">Searching new content with SharePoint Search</span></span>](searching-new-content-with-sharepoint-search.md)
    
  
-  [<span data-ttu-id="ff1fb-213">Konfigurieren der Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ff1fb-213">Configure search in SharePoint</span></span>](configure-search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ff1fb-214">Erstellen von Suchabfragen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ff1fb-214">Building search queries in SharePoint</span></span>](building-search-queries-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ff1fb-215">Vorgehensweise: verwenden ein benutzerdefinierten Security Trimmer für SharePoint Server-Suchergebnisse</span><span class="sxs-lookup"><span data-stu-id="ff1fb-215">How to: Use a custom security trimmer for SharePoint Server search results</span></span>](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md)
    
  

