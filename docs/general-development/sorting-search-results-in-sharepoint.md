---
title: Sortieren von Suchergebnissen in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 143925763fd8cebc94899d53d36f52474d8b0afd
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sorting-search-results-in-sharepoint"></a><span data-ttu-id="d527c-102">Sortieren von Suchergebnissen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d527c-102">Sorting search results in SharePoint</span></span>

  
    
    
![Konzeptuelles Übersichtsthema](../images/mod_icon_badge_conoverview.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="d527c-104">Ordnen Sie Suchergebnisse programmgesteuert nach Rang, verwaltetem Eigenschaftswert, einem Formelausdruck oder in zufälliger Reihenfolge mithilfe des Abfrage-Objektmodells in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d527c-104">Sort search results programmatically—by rank, by managed property value, by a formula expression, or in random order—by using the Query object model in SharePoint.</span></span> <span data-ttu-id="d527c-105">Sie können die Suchergebnisse für SharePoint auf vier Arten sortieren:</span><span class="sxs-lookup"><span data-stu-id="d527c-105">You can sort the search results for SharePoint in four ways:</span></span>
  
    
    


-  <span data-ttu-id="d527c-106">[Sortieren von Suchergebnissen nach Rang](#SP15_Sort_search_resuilts_by_rank): Ermöglicht die Sortierung des Suchergebnisses basierend auf dem Relevanzrang.</span><span class="sxs-lookup"><span data-stu-id="d527c-106">[Sort search results by rank](#SP15_Sort_search_resuilts_by_rank): Enables you to sort the search result by relevance rank.</span></span>
    
  
-  <span data-ttu-id="d527c-107">[Sortieren von Suchergebnissen nach dem Wert einer verwalteten Eigenschaft](#SP15_Sort_search_results_by_managed_property_value): Ermöglicht die Sortierung des Suchergebnisses basierend auf dem Wert mindestens einer verwalteten Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="d527c-107">[Sort search results by managed property value](#SP15_Sort_search_results_by_managed_property_value): Enables you to sort the search result based on the value of one or more managed properties.</span></span>
    
  
-  <span data-ttu-id="d527c-108">[Sortieren von Suchergebnissen nach einem Formelausdruck](#SP15_Sort_search_results_by_formula): Ermöglicht die Sortierung des Suchergebnisses nach einer in der Abfrageanforderung angegebenen Formel.</span><span class="sxs-lookup"><span data-stu-id="d527c-108">[Sort search results by a formula expression](#SP15_Sort_search_results_by_formula): Enables you to sort the search result by a formula specified in the query request.</span></span>
    
  
-  <span data-ttu-id="d527c-109">[Sortieren von Suchergebnissen in zufälliger Reihenfolge](#SP15_Sort_search_results_in_random_order): Ermöglicht die Sortierung des Abfrageergebnisses in zufälliger Reihenfolge oder das Hinzufügen einer zufälligen Komponente zur Sortierreihenfolge.</span><span class="sxs-lookup"><span data-stu-id="d527c-109">[Sort search results in random order](#SP15_Sort_search_results_in_random_order): Enables you to sort the query result in random order, or add a random component to the sort order.</span></span>
    
  

<span data-ttu-id="d527c-110">Dieser Artikel befasst sich mit der programmgesteuerten Sortierung von Suchergebnissen.</span><span class="sxs-lookup"><span data-stu-id="d527c-110">This article focuses on sorting search results programmatically.</span></span> <span data-ttu-id="d527c-111">Sehen Sie sich die folgenden Artikel an, um zu erfahren, wie Sie Suchergebnisse mithilfe von SharePoint-Abfrageregeln sortieren können:</span><span class="sxs-lookup"><span data-stu-id="d527c-111">This article focuses on sorting search results programmatically. To learn how to sort search results using SharePoint Server 2013 query rules, see the following articles:</span></span>
  
    
    


-  <span data-ttu-id="d527c-112">
  [Ändern bewerteter Suchergebnisse in „Abfrageregeln verwalten“](http://technet.microsoft.com/en-us/library/jj871676.aspx#BKMK_ChangeRankedSearchResults)</span><span class="sxs-lookup"><span data-stu-id="d527c-112">[Change ranked search results in Manage query rules](http://technet.microsoft.com/en-us/library/jj871676.aspx#BKMK_ChangeRankedSearchResults)</span></span>
    
  
-  <span data-ttu-id="d527c-113">
  [„Ändern bewerteter Suchergebnisse" in „Erstellen von Abfrageregeln für das Web Content Management"](http://technet.microsoft.com/en-us/library/jj871014.aspx#BKMK_ChangeRankedSearchResults)</span><span class="sxs-lookup"><span data-stu-id="d527c-113">[Change ranked search results in Create query rules for web content management](http://technet.microsoft.com/en-us/library/jj871014.aspx#BKMK_ChangeRankedSearchResults)</span></span>
    
  

## <a name="how-to-specify-sorting-in-a-query-request"></a><span data-ttu-id="d527c-114">Angeben der Sortierung in einer Abfrageanforderung</span><span class="sxs-lookup"><span data-stu-id="d527c-114">How to specify sorting in a query request</span></span>
<span data-ttu-id="d527c-115"><a name="SP15_Specify_sorting_in_query_request"> </a></span><span class="sxs-lookup"><span data-stu-id="d527c-115"></span></span>

<span data-ttu-id="d527c-116">Wenn Sie das Abfrage-Objektmodell verwenden, können Sie die Sortierkriterien durch Bereitstellung einer Sortierspezifikation in der [SortList](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.SortList.aspx)-Eigenschaft der [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx)-Klasse wählen.</span><span class="sxs-lookup"><span data-stu-id="d527c-116">When you use the Query object model, you can choose the sort criteria by providing a sort specification through the  [SortList](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.SortList.aspx) property of the [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx) class.</span></span> <span data-ttu-id="d527c-117">Die [SortList](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.SortList.aspx)-Eigenschaft ist vom Typ [SortCollection](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SortCollection.aspx), der eine Sammlung von [Sortierobjekten](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.aspx) repräsentiert.</span><span class="sxs-lookup"><span data-stu-id="d527c-117">The [SortList](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.SortList.aspx) property is of type [SortCollection](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SortCollection.aspx) , which represents a collection of [Sort](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.aspx) objects.</span></span>
  
    
    
<span data-ttu-id="d527c-p104">Ein  [Sort](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.aspx) -Objekt definiert eine Art der Sortierung von Suchergebnissen. Es besteht aus einem Wert, nach dem Sie Suchergebnisse sortieren möchten ( [Property](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.Property.aspx) ), und einer Richtung der Sortierung ( [Direction](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.Direction.aspx) ). Die Richtung ist vom Typ [SortDirection()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SortDirection.aspx) und kann aufsteigend oder absteigend sein.</span><span class="sxs-lookup"><span data-stu-id="d527c-p104">A  [Sort](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.aspx) object defines a way to sort search results; it consists of a value you want to order search results on ( [Property](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.Property.aspx) ) and a direction in which you want to order the results ( [Direction](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.Direction.aspx) ). The direction is of type [SortDirection()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SortDirection.aspx) and can be ascending or descending.</span></span>
  
    
    
<span data-ttu-id="d527c-p105">Wenn  [SortList](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.SortList.aspx) mehrere Werte enthält, erfolgt die Sortierung basierend auf der Reihenfolge, in der die Werte angezeigt werden. Dies bedeutet, dass jedes **Sort**-Objekt eine Ebene der Sortierreihenfolge darstellt. Eine nachfolgende Ebene ändert nicht die Reihenfolge der Ergebnisse, die von vorherigen Ebenen unterschieden wurden. Aber sie kann sich auf die interne Reihenfolge der Ergebnisse auswirken, die die gleichen Sortierwerte für die vorherigen Ebenen aufweisen.</span><span class="sxs-lookup"><span data-stu-id="d527c-p105">If you have multiple values in  [SortList](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.SortList.aspx) , the sorting is performed based on the sequence in which the values appear. This means that every **Sort** object represents a sort order level. Any succeeding level does not change the ordering of results that were differentiated by previous ones, but it may affect the internal ordering of results that have the same sort values for the previous levels.</span></span>
  
    
    
<span data-ttu-id="d527c-123">Neben dem Abfrage-Objektmodell bietet SharePoint zudem einen Search-REST-Dienst, den Sie verwenden können, um den Suchindex mit Ihrer Client- oder mobilen Anwendung abzufragen.</span><span class="sxs-lookup"><span data-stu-id="d527c-123">Apart from the Query object model, SharePoint also provides a Search REST service that you can use to query the search index with your client or mobile applications.</span></span> <span data-ttu-id="d527c-124">Der Search-REST-Dienst unterstützt POST- und GET-HTTP-Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="d527c-124">The Search REST service supports both HTTP POST and HTTP GET requests.</span></span> <span data-ttu-id="d527c-125">Weitere Informationen zum Erstellen von URIs für diese Anforderungen finden Sie unter [Erstellen von Abfragen mit dem Search-REST-Dienst](sharepoint-search-rest-api-overview.md#bk_queryrest).</span><span class="sxs-lookup"><span data-stu-id="d527c-125">For more information on how to construct URIs for these requests, see  [Querying with the Search REST service](sharepoint-search-rest-api-overview.md#bk_queryrest).</span></span>
  
    
    

## <a name="sort-search-results-by-rank"></a><span data-ttu-id="d527c-126">Sortieren der Suchergebnisse nach Rang</span><span class="sxs-lookup"><span data-stu-id="d527c-126">Sort search results by rank</span></span>
<span data-ttu-id="d527c-127"><a name="SP15_Sort_search_resuilts_by_rank"> </a></span><span class="sxs-lookup"><span data-stu-id="d527c-127"></span></span>

<span data-ttu-id="d527c-128">Standardmäßig werden die Suchergebnisse nach Relevanzrang sortiert.</span><span class="sxs-lookup"><span data-stu-id="d527c-128">By default, search results are sorted by relevance rank.</span></span> <span data-ttu-id="d527c-129">Dies bedeutet, dass SharePoint die relevantesten Suchergebnisse ganz oben im Suchergebnissatz platziert.</span><span class="sxs-lookup"><span data-stu-id="d527c-129">This means that SharePoint places the most relevant results on top in the search result set.</span></span> <span data-ttu-id="d527c-130">Bei der Sortierung nach Rang werden die Ergebnisse stets in absteigender Reihenfolge sortiert.</span><span class="sxs-lookup"><span data-stu-id="d527c-130">If you sort by rank, the result is always sorted in descending order.</span></span> <span data-ttu-id="d527c-131">Mit [SortDirection()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SortDirection.aspx) können Sie die Reihenfolge jedoch ändern, sodass die Ergebnisse in aufsteigender Reihenfolge sortiert werden.</span><span class="sxs-lookup"><span data-stu-id="d527c-131">But you can change the sort order to ascending by using  [SortDirection()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SortDirection.aspx) .</span></span>
  
    
    
<span data-ttu-id="d527c-132">Außerdem können Sie die Rangberechnung in der Abfragezeichenfolge auf zwei Arten beeinflussen:</span><span class="sxs-lookup"><span data-stu-id="d527c-132">You can also influence the rank calculation in the query string, in one of two ways:</span></span>
  
    
    

- <span data-ttu-id="d527c-p108">Mit dem **XRANK**-Operator in  [Syntaxreferenz für die Keyword Query Language (KQL)](keyword-query-language-kql-syntax-reference.md) und [Syntaxreferenz für FQL (FAST Query Language)](fast-query-language-fql-syntax-reference.md). Mit **XRANK** können Sie für den Fall, dass eine bestimmte Abfragebedingung erfüllt wird, eine bedingte Rangverstärkung anwenden.</span><span class="sxs-lookup"><span data-stu-id="d527c-p108">By using the **XRANK** operator available in [Keyword Query Language (KQL) syntax reference](keyword-query-language-kql-syntax-reference.md) and [FAST Query Language (FQL) syntax reference](fast-query-language-fql-syntax-reference.md). You can use **XRANK** to apply a conditional rank boosting if a specific query condition is met.</span></span>
    
  
- <span data-ttu-id="d527c-p109">Durch Auswählen einer Relevanzgewichtung für eine dynamische Rangfolge. Bei Verwendung von FQL können Sie eine einzelne Relevanzgewichtung für jeden **STRING**-Operator angeben.</span><span class="sxs-lookup"><span data-stu-id="d527c-p109">By choosing a relevance weight for dynamic ranking. When using FQL, you can specify an individual relevance weight for each **STRING** operator.</span></span>
    
  

## <a name="sort-search-results-by-managed-property-value"></a><span data-ttu-id="d527c-137">Sortieren von Suchergebnissen nach dem Wert einer verwalteten Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="d527c-137">Sort search results by managed property value</span></span>
<span data-ttu-id="d527c-138"><a name="SP15_Sort_search_results_by_managed_property_value"> </a></span><span class="sxs-lookup"><span data-stu-id="d527c-138"></span></span>

<span data-ttu-id="d527c-139">Sie können die Sortierung der Suchergebnisse basierend auf dem Wert einer oder mehrerer verwalteter Eigenschaften angeben.</span><span class="sxs-lookup"><span data-stu-id="d527c-139">You can specify search result sorting based on the value of one or more managed properties. This means that SharePoint Server 2013 performs the sorting based on all results that match the query.</span></span> <span data-ttu-id="d527c-140">Dies bedeutet, dass SharePoint die Sortierung basierend auf allen Ergebnissen durchführt, die der Abfrage entsprechen.</span><span class="sxs-lookup"><span data-stu-id="d527c-140">You can specify search result sorting based on the value of one or more managed properties. This means that SharePoint Server 2013 performs the sorting based on all results that match the query.</span></span>
  
    
    
<span data-ttu-id="d527c-p111">Sie können basierend auf Texteigenschaften und numerischen Eigenschaften sortieren. Bei Texteigenschaften basiert die Sortierung auf der Standardsortierung von Textzeichenfolgen. Im Gegensatz dazu basiert die Sortierung für numerische Eigenschaften (z. B. verwaltete Eigenschaften vom Typ  [DateTime](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) ), auf dem numerischen Wert.</span><span class="sxs-lookup"><span data-stu-id="d527c-p111">You can sort based on text and numeric properties. For text properties, the sorting is based on standard text string sorting. In contrast, for numeric properties (including managed properties of type  [DateTime](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) ), the sorting is based on numeric value.</span></span>
  
    
    

### <a name="example"></a><span data-ttu-id="d527c-144">Beispiel</span><span class="sxs-lookup"><span data-stu-id="d527c-144">Example</span></span>

<span data-ttu-id="d527c-145">Das folgende Beispiel zeigt die Sortierung der Suchergebnisse mithilfe der verwalteten Eigenschaft **Size**.</span><span class="sxs-lookup"><span data-stu-id="d527c-145">The following example shows how to sort search results by using the **Size** managed property.</span></span>
  
    
    

```cs

using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home"
    };
    query.SortList.Add("Size", SortDirection.Descending);

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    { 
        Console.WriteLine(result["Title"] + " Size:" + result["Size"]);
    }
}
```

<span data-ttu-id="d527c-146">Alternativ können Sie mit folgendem Aufruf die Such-REST-API zum Sortieren der Suchergebnisse nach der **Size**-Eigenschaft verwenden.</span><span class="sxs-lookup"><span data-stu-id="d527c-146">Alternatively, you could use the Search REST API to sort search results by using the **Size** property with the following call.</span></span>
  
    
    



```HTML

http://localhost/_api/search/query?querytext='home'&amp;sortlist='size:descending'
```


## <a name="sort-search-results-by-a-formula-expression"></a><span data-ttu-id="d527c-147">Sortieren von Suchergebnissen nach einem Formelausdruck</span><span class="sxs-lookup"><span data-stu-id="d527c-147">Sort search results by a formula expression</span></span>
<span data-ttu-id="d527c-148"><a name="SP15_Sort_search_results_by_formula"> </a></span><span class="sxs-lookup"><span data-stu-id="d527c-148"></span></span>

<span data-ttu-id="d527c-149">Sie können die Sortierung der Suchergebnisse basierend auf einer Sortierspezifikation angeben, die den Sortierwert nach einer mathematischen Formel berechnet.</span><span class="sxs-lookup"><span data-stu-id="d527c-149">You can specify search result sorting based on a sort specification that uses a mathematical formula to create the sorting value.</span></span>
  
    
    
<span data-ttu-id="d527c-p112">Das Feature der Sortierung nach einer Formel ist eine Erweiterung der einstufigen und mehrstufigen Sortierfunktionalität für Suchergebnisse. Das Feature ermöglicht die Angabe einer Formel anstelle einer verwalteten Eigenschaft als Sortierkriterium.</span><span class="sxs-lookup"><span data-stu-id="d527c-p112">The sort by formula feature is an extension of the single-level and multilevel sorting functionality for search results. The feature enables you to specify a formula instead of a managed property as sorting criteria.</span></span> 
  
    
    
<span data-ttu-id="d527c-152">Mit dem Feature der Sortierung nach einer Formel können Sie mathematische Operationen auf den Wert von verwalteten Eigenschaften für jedes Element im Abfrageergebnis anwenden.</span><span class="sxs-lookup"><span data-stu-id="d527c-152">By using the sort by formula feature, you can apply mathematical operations on the value of one or more managed properties for each item in the query result.</span></span>
  
    
    
<span data-ttu-id="d527c-153">Im Folgenden finden Sie Beispiele, die mithilfe einer Formel für die Suchergebnissortierung implementiert werden können:</span><span class="sxs-lookup"><span data-stu-id="d527c-153">The following are examples that can be implemented by using a formula to specify search result sorting:</span></span>
  
    
    

- <span data-ttu-id="d527c-154">K-Nächster-Nachbar-Algorithmus zur Klassifikation von Dokumenten</span><span class="sxs-lookup"><span data-stu-id="d527c-154">K-nearest neighbor algorithm to classify documents.</span></span>
    
  
- <span data-ttu-id="d527c-155">Euklidischer Abstand oder Manhattan-Abstand zur Berechnung geographischer Entfernungen</span><span class="sxs-lookup"><span data-stu-id="d527c-155">Euclidean distance or Manhattan distance to calculate geographical distances.</span></span>
    
  
- <span data-ttu-id="d527c-156">Bevorzugter Wert, z. B. zum Sortieren von Dokumenten basierend darauf, wie weit der Wert einer bestimmten verwalteten Eigenschaft von einem bevorzugten Wert entfernt ist.</span><span class="sxs-lookup"><span data-stu-id="d527c-156">Preferred value, for example, to sort documents based on how far a given managed property value is from a preferred value.</span></span>
    
  
<span data-ttu-id="d527c-157">Das Feature der Sortierung nach einer Formel umfasst keine Kontrolle über statistische dynamische Rangfolgenparameter, wie z. B. Häufigkeit von Begriffen und Nähe.</span><span class="sxs-lookup"><span data-stu-id="d527c-157">The sort by formula feature does not include control of statistical dynamic rank parameters, such as term frequency and proximity.</span></span>
  
    
    
<span data-ttu-id="d527c-p113">Die Formel wird von links nach rechts und mit der Standardrangfolge mathematischer Operatoren ausgewertet. D. h., zuerst werden Funktionen und Klammergruppen ausgewertet, dann werden Multiplikationen und Divisionen und schließlich Additionen und Subtraktionen ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="d527c-p113">The formula is evaluated left to right and uses standard mathematical-operator precedence. That is, functions and parenthetical groups are evaluated first, multiplication and division operations are performed next, and addition and subtraction operations are performed last.</span></span>
  
    
    

> <span data-ttu-id="d527c-160">**Wichtig:** Das endgültige Ergebnis einer Formel muss im Wertebereich einer 32-Bit-Ganzzahl mit Vorzeichen liegen.</span><span class="sxs-lookup"><span data-stu-id="d527c-160">**Important** The final result of a formula must be in the value range of a 32-bit signed integer. Otherwise, the sorting may be incorrect.</span></span> <span data-ttu-id="d527c-161">Andernfalls ist die Sortierung möglicherweise falsch.</span><span class="sxs-lookup"><span data-stu-id="d527c-161">Otherwise, the sorting may be incorrect.</span></span> 
  
    
    


### <a name="specifying-the-sort-formula-in-a-query"></a><span data-ttu-id="d527c-162">Angeben der Sortierformel in einer Abfrage</span><span class="sxs-lookup"><span data-stu-id="d527c-162">Specifying the sort formula in a query</span></span>

<span data-ttu-id="d527c-163">Sie können in der Sortierspezifikation der Abfrageanforderung eine Sortierformel anstelle einer verwalteten Eigenschaft angeben.</span><span class="sxs-lookup"><span data-stu-id="d527c-163">You specify a sort formula instead of a managed property in the sort specification of the query request.</span></span>
  
    
    
<span data-ttu-id="d527c-164">Die Sortierspezifikation hat folgendes Format:  `[formula:<sort-formula>]`</span><span class="sxs-lookup"><span data-stu-id="d527c-164">The sort specification has the following format:  `[formula:<sort-formula>]`</span></span>
  
    
    
<span data-ttu-id="d527c-165">Im Format ist _<sort-formula>_ der Sortierformelausdruck.</span><span class="sxs-lookup"><span data-stu-id="d527c-165">In the format,  _<sort-formula>_ is the sort formula expression.</span></span>
  
    
    

> <span data-ttu-id="d527c-166">**Hinweis:** Die eckigen Klammern sind Teil der Syntax der Sortierspezifikation.</span><span class="sxs-lookup"><span data-stu-id="d527c-166">**Note** The square brackets are part of the sort specification syntax.</span></span> 
  
    
    

<span data-ttu-id="d527c-p115">Die Standardsortierreihenfolge ist absteigend. Sie können auch eine Formel verwenden, die nach aufsteigenden Werten sortiert, z. B. wenn die Formel eine geographische Entfernung angibt.</span><span class="sxs-lookup"><span data-stu-id="d527c-p115">The default sort direction is descending. You may also use a formula that sorts by ascending value, for example, if the formula specifies a geographical distance.</span></span>
  
    
    
<span data-ttu-id="d527c-169">Das folgende Codebeispiel zeigt, wie Sie die Sortierung nach Formel mit aufsteigender Sortierreihenfolge mithilfe des Abfrage-Objektmodells angeben.</span><span class="sxs-lookup"><span data-stu-id="d527c-169">The following code example shows how to specify sort by formula with ascending sort order by using the Query object model.</span></span>
  
    
    



```cs
using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home"
    };
    query.SortList.Add("[formula:abs(2000-size)]", SortDirection.Ascending);

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    { 
        Console.WriteLine(result["Title"]);
    }
}
```

<span data-ttu-id="d527c-170">Alternativ können Sie mit folgendem Aufruf die Such-REST-API zum Sortieren der Suchergebnisse nach der **Size**-Eigenschaft verwenden.</span><span class="sxs-lookup"><span data-stu-id="d527c-170">Alternatively, you could use the Search REST API to sort search results by using the **Size** property with the following call.</span></span>
  
    
    



```HTML

http://localhost/_api/search/query?querytext='home'&amp;sortlist='[formula:abs(2000-size)]:ascending'

```


### <a name="using-managed-properties-in-the-sort-formula"></a><span data-ttu-id="d527c-171">Verwenden von verwalteten Eigenschaften in der Sortierformel</span><span class="sxs-lookup"><span data-stu-id="d527c-171">Using managed properties in the sort formula</span></span>

<span data-ttu-id="d527c-p116">Sie können eine Sortierformel auf den Wert verwalteter Eigenschaften vom Typ  [Integer](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) , [Decimal](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) und [Datetime()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Datetime.aspx) anwenden. Sie müssen die Sortierung für die angegebene verwaltete Eigenschaft im Suchschema aktivieren.</span><span class="sxs-lookup"><span data-stu-id="d527c-p116">You can apply a sort formula on the value of managed properties of type  [Integer](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) , [Decimal](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) , and [Datetime()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Datetime.aspx) . You must enable sorting for the specified managed property in the search schema.</span></span>
  
    
    
<span data-ttu-id="d527c-174">Für weitere verwaltete Eigenschaften vom Typ  [Decimal](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) wird der Wert vor der Formelauswertung mit 10^(Dezimalziffern) multipliziert.</span><span class="sxs-lookup"><span data-stu-id="d527c-174">For more managed properties of type  [Decimal](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) , the value is multiplied by 10^(decimal digits) before being used in the formula evaluation.</span></span>
  
    
    
<span data-ttu-id="d527c-p117">Für verwaltete Eigenschaften vom Typ  [Datetime()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Datetime.aspx) wird der Wert vor der Formelauswertung in die Anzahl von jeweils 100 Nanosekunden seit 1. Januar 29000 v. Chr. konvertiert. Das Jahr hat 366 Tage.</span><span class="sxs-lookup"><span data-stu-id="d527c-p117">For managed properties of type  [Datetime()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Datetime.aspx) , the value is converted to the number of 100 nanoseconds since January 1 29000 BC before being used in the formula evaluation. There are 366 days in the year.</span></span>
  
    
    

### <a name="sort-formula-expressions"></a><span data-ttu-id="d527c-177">Sortierformelausdrücke</span><span class="sxs-lookup"><span data-stu-id="d527c-177">Sort formula expressions</span></span>

<span data-ttu-id="d527c-p118">In Tabelle 1 sind die Funktionen aufgelistet, die Sie im Sortierformelausdruck verwenden können. Der Ausdruck darf keine Leerzeichen enthalten.</span><span class="sxs-lookup"><span data-stu-id="d527c-p118">Table 1 lists the functions you can use in the sort formula expression. The expression must not contain spaces.</span></span>
  
    
    

<span data-ttu-id="d527c-180">**Tabelle 1. Funktionen für Sortierformelausdrücke**</span><span class="sxs-lookup"><span data-stu-id="d527c-180">**Table 1. Functions for sort formula expressions**</span></span>


|<span data-ttu-id="d527c-181">**Funktion**</span><span class="sxs-lookup"><span data-stu-id="d527c-181">**Function**</span></span>|<span data-ttu-id="d527c-182">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="d527c-182">**Description**</span></span>|
|:-----|:-----|
|**+** <br/> |<span data-ttu-id="d527c-183">Gibt Addition an.</span><span class="sxs-lookup"><span data-stu-id="d527c-183">Specifies addition.</span></span>  <br/> |
|**-** <br/> |<span data-ttu-id="d527c-184">Gibt Subtraktion an.</span><span class="sxs-lookup"><span data-stu-id="d527c-184">Specifies subtraction.</span></span>  <br/> |
|* <br/> |<span data-ttu-id="d527c-185">Gibt Multiplikation an.</span><span class="sxs-lookup"><span data-stu-id="d527c-185">Specifies multiplication.</span></span>  <br/> |
|**/** <br/> |<span data-ttu-id="d527c-186">Gibt die Division an.</span><span class="sxs-lookup"><span data-stu-id="d527c-186">Specifies division.</span></span>  <br/> <span data-ttu-id="d527c-187">**Hinweis:** Standardmäßig führt eine Division durch Null zu einer Ausnahme, und die Abfrage gibt einen Fehler zurück.</span><span class="sxs-lookup"><span data-stu-id="d527c-187">**Note:** By default, a division by zero results in an exception, and the query returns with an error.</span></span> <span data-ttu-id="d527c-188">Mithilfe des **errtolast**-Operators können Sie den Abfragefehler vermeiden und stattdessen die fehlerhaften Elemente am Ende des Resultsets platzieren.</span><span class="sxs-lookup"><span data-stu-id="d527c-188">By default, a division by zero results in an exception, and the query returns with an error. By using the **errtolast** operator, you can avoid the query error and instead place the failing items at the end of the result set.</span></span>          |
|<span data-ttu-id="d527c-189">**rank**</span><span class="sxs-lookup"><span data-stu-id="d527c-189">**rank**</span></span> <br/> |<span data-ttu-id="d527c-190">Ein spezielles Schlüsselwort, das den dynamischen Rang eines Elements darstellt.</span><span class="sxs-lookup"><span data-stu-id="d527c-190">A special keyword that represents the dynamic rank of an item.</span></span>  <br/> <span data-ttu-id="d527c-191">Beispiel:  `abs(rank-100)` verwendet den Abstand vom Rangwert 100 als Sortierkriterium.</span><span class="sxs-lookup"><span data-stu-id="d527c-191">Example:  `abs(rank-100)` will use the distance from rank value 100 as the sorting criteria.</span></span> <br/> |
|<span data-ttu-id="d527c-192">**[0-9.]+**</span><span class="sxs-lookup"><span data-stu-id="d527c-192">**[0-9.]+**</span></span> <br/> |<span data-ttu-id="d527c-193">Gibt an, dass Zahlen als ganze Zahl oder doppelte Werte angegeben werden können.</span><span class="sxs-lookup"><span data-stu-id="d527c-193">Specifies that numbers can be given as integer or double values.</span></span>  <br/> <span data-ttu-id="d527c-194">Beispiele: 503; 3,14; 5,4352262</span><span class="sxs-lookup"><span data-stu-id="d527c-194">Examples: 503, 3.14, 5.4352262</span></span>  <br/> |
|<span data-ttu-id="d527c-195">**[a-z0-9]+]**</span><span class="sxs-lookup"><span data-stu-id="d527c-195">**[a-z0-9]+]**</span></span> <br/> |<span data-ttu-id="d527c-p120">Gibt an, dass eine beliebige Zeichenfolge, die nicht als Funktionsname erkannt wird, als Name einer verwalteten Eigenschaft behandelt wird. Sie müssen die Sortierung für die angegebene verwaltete Eigenschaft im Suchschema aktivieren.</span><span class="sxs-lookup"><span data-stu-id="d527c-p120">Specifies that any character sequence not recognized as a function name is treated as a managed property name. You must enable sorting for the specified managed property in the search schema.  </span></span><br/> <span data-ttu-id="d527c-p121"> Beispiel: Sie können eine verwaltete Eigenschaft namens **height** mit aktivierter Sortierung definieren. Dies ermöglicht Ihnen, "height" als Ausdruck in der Formel zu verwenden. Die Formel verwendet dann den Wert der verwalteten Eigenschaft **height**.  </span><span class="sxs-lookup"><span data-stu-id="d527c-p121">Example: You can define a managed property named **height** with sorting enabled. This enables you to use "height" as an expression in the formula. The formula will use the value of the **height** managed property. </span></span><br/> |
|<span data-ttu-id="d527c-201">**( and )**</span><span class="sxs-lookup"><span data-stu-id="d527c-201">**( and )**</span></span> <br/> |<span data-ttu-id="d527c-202">Verwendet zur Gruppierung von Berechnungen, um den richtigen Vorrang sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="d527c-202">Used to group calculations ensuring correct precedence.</span></span>  <br/> <span data-ttu-id="d527c-203">Beispiel: 4*(3+2)</span><span class="sxs-lookup"><span data-stu-id="d527c-203">Example: 4*(3+2)</span></span>  <br/> |
|<span data-ttu-id="d527c-204">**sqrt(n)**</span><span class="sxs-lookup"><span data-stu-id="d527c-204">**sqrt(n)**</span></span> <br/> |<span data-ttu-id="d527c-205">Die Quadratwurzel von  _n_</span><span class="sxs-lookup"><span data-stu-id="d527c-205">The square root of  _n_.</span></span>  <br/> |
|<span data-ttu-id="d527c-206">**exp(n)**</span><span class="sxs-lookup"><span data-stu-id="d527c-206">**exp(n)**</span></span> <br/> |<span data-ttu-id="d527c-207">Die Exponentialfunktion, die  *pow(2.71828182846,n)*  entspricht.</span><span class="sxs-lookup"><span data-stu-id="d527c-207">The exponential function that is equivalent to  *pow(2.71828182846,n)*</span></span>  <br/> |
|<span data-ttu-id="d527c-208">**log(n)**</span><span class="sxs-lookup"><span data-stu-id="d527c-208">**log(n)**</span></span> <br/> |<span data-ttu-id="d527c-209">Der natürliche Logarithmus von _n_</span><span class="sxs-lookup"><span data-stu-id="d527c-209">The natural logarithm of  _n_.</span></span>  <br/> |
|<span data-ttu-id="d527c-210">**abs(n)**</span><span class="sxs-lookup"><span data-stu-id="d527c-210">**abs(n)**</span></span> <br/> |<span data-ttu-id="d527c-211">Der absolute Wert von  _n_</span><span class="sxs-lookup"><span data-stu-id="d527c-211">The absolute value of  _n_.</span></span>  <br/> |
|<span data-ttu-id="d527c-212">**ceil(n)**</span><span class="sxs-lookup"><span data-stu-id="d527c-212">**ceil(n)**</span></span> <br/> |<span data-ttu-id="d527c-p122">Die Obergrenze von  _n_. Das heißt, wenn  _n_ keine ganze Zahl ist, wird auf die nächste ganze Zahl aufgerundet. Wenn _n_ eine ganze Zahl ist, wird _n_ verwendet. </span><span class="sxs-lookup"><span data-stu-id="d527c-p122">The ceiling of  _n_. That is, if  _n_ is not a whole number, round up to the next whole number. If _n_ is a whole number, use _n_.  </span></span><br/> |
|<span data-ttu-id="d527c-216">**floor(n)**</span><span class="sxs-lookup"><span data-stu-id="d527c-216">**floor(n)**</span></span> <br/> |<span data-ttu-id="d527c-p123">Die Untergrenze von  _n_. Das heißt, wenn  _n_ keine ganze Zahl ist, wird auf die nächste ganze Zahl abgerundet. Wenn _n_ eine ganze Zahl ist, wird _n_ verwendet. </span><span class="sxs-lookup"><span data-stu-id="d527c-p123">The floor of  _n_. That is, if  _n_ is not a whole number, round down to the next whole number. If _n_ is a whole number, use _n_.  </span></span><br/> |
|<span data-ttu-id="d527c-220">**round(n)**</span><span class="sxs-lookup"><span data-stu-id="d527c-220">**round(n)**</span></span> <br/> |<span data-ttu-id="d527c-p124">Die Rundung von  _n_ auf die nächstgelegene gerade ganze Zahl. Auch als „Bankers rounding" (mathematisches Runden) oder „Round half to even" bezeichnet. </span><span class="sxs-lookup"><span data-stu-id="d527c-p124">The rounding of  _n_ to the nearest even whole number. Also known as "Bankers rounding" or "Round half to even". </span></span><br/> |
|<span data-ttu-id="d527c-223">**sin(n)**</span><span class="sxs-lookup"><span data-stu-id="d527c-223">**sin(n)**</span></span> <br/> |<span data-ttu-id="d527c-224">Der Sinus von  _n_ Bogenmaß.</span><span class="sxs-lookup"><span data-stu-id="d527c-224">The sine of  _n_ radians.</span></span> <br/> |
|<span data-ttu-id="d527c-225">**cos(n)**</span><span class="sxs-lookup"><span data-stu-id="d527c-225">**cos(n)**</span></span> <br/> |<span data-ttu-id="d527c-226">Der Kosinus von  _n_ Bogenmaß.</span><span class="sxs-lookup"><span data-stu-id="d527c-226">The cosine of  _n_ radians.</span></span> <br/> |
|<span data-ttu-id="d527c-227">**tan(n)**</span><span class="sxs-lookup"><span data-stu-id="d527c-227">**tan(n)**</span></span> <br/> |<span data-ttu-id="d527c-228">Die Tangente von  _n_Bogenmaß.</span><span class="sxs-lookup"><span data-stu-id="d527c-228">The tangent of  _n_ radians.</span></span> <br/> |
|<span data-ttu-id="d527c-229">**asin(n)**</span><span class="sxs-lookup"><span data-stu-id="d527c-229">**asin(n)**</span></span> <br/> |<span data-ttu-id="d527c-230">Der Arcussinus von  _n_ in Bogenmaß.</span><span class="sxs-lookup"><span data-stu-id="d527c-230">The arcsine, in radians, of  _n_.</span></span>  <br/> |
|<span data-ttu-id="d527c-231">**acos(n)**</span><span class="sxs-lookup"><span data-stu-id="d527c-231">**acos(n)**</span></span> <br/> |<span data-ttu-id="d527c-232">Der Arcuskosinus von  _n_ in Bogenmaß.</span><span class="sxs-lookup"><span data-stu-id="d527c-232">The arccosine, in radians, of  _n_.</span></span>  <br/> |
|<span data-ttu-id="d527c-233">**atan(n)**</span><span class="sxs-lookup"><span data-stu-id="d527c-233">**atan(n)**</span></span> <br/> |<span data-ttu-id="d527c-234">Der Arcustangens von  _n_ in Bogenmaß.</span><span class="sxs-lookup"><span data-stu-id="d527c-234">The arctangent, in radians, of  _n_.</span></span>  <br/> |
|<span data-ttu-id="d527c-235">**pow(x,y)**</span><span class="sxs-lookup"><span data-stu-id="d527c-235">**pow(x,y)**</span></span> <br/> |<span data-ttu-id="d527c-236">Der Wert von _x_ potenziert mit _y_.</span><span class="sxs-lookup"><span data-stu-id="d527c-236">The value of  _x_ raised to the power of _y_.</span></span>  <br/> <span data-ttu-id="d527c-237">**Hinweis:** Der Wert von _y_ muss eine reelle Zahl sein.</span><span class="sxs-lookup"><span data-stu-id="d527c-237">The value of  _y_ must be a real number.</span></span>          |
|<span data-ttu-id="d527c-238">**atan2(y,x)**</span><span class="sxs-lookup"><span data-stu-id="d527c-238">**atan2(y,x)**</span></span> <br/> |<span data-ttu-id="d527c-239">Ein Arcustangens (mit zwei Argumenten) des Winkels im Bogenmaß zwischen der positiven X-Achse und der angegebenen kartesischen Koordinate (x,y).</span><span class="sxs-lookup"><span data-stu-id="d527c-239">A two-argument arctangent of the angle in radians between the positive x axis and the specified Cartesian coordinate (x,y).</span></span>  <br/> |
|<span data-ttu-id="d527c-240">**bucket(b,n1,n2,…)**</span><span class="sxs-lookup"><span data-stu-id="d527c-240">**bucket(b,n1,n2,…)**</span></span> <br/> |<span data-ttu-id="d527c-241">Ein Operator, der verwendet werden kann, um diskrete Werte für angegebene Werteverteilungsbereiche für einen Ausdruck anzugeben.</span><span class="sxs-lookup"><span data-stu-id="d527c-241">An operator that can be used to provide discrete values for given value distribution ranges for an expression.</span></span>  <br/> <span data-ttu-id="d527c-p125"> Der Ausdruck  _b_ kann eine verwaltete Eigenschaft oder ein anderer Formelausdruck sein. Die Argumente _n1, n2, …_ stellen numerische Schwellenwerte dar. Sie können eine beliebige Anzahl von Bucket-Schwellenwerten angeben. </span><span class="sxs-lookup"><span data-stu-id="d527c-p125">The expression  _b_ can be a managed property or any other formula expression. The arguments _n1, n2, …_ represent numeric thresholds. You can specify an arbitrary number of bucket thresholds. </span></span><br/> <span data-ttu-id="d527c-246">**Hinweis:** Sie müssen die Argumente _n1, n2, n3 ..._</span><span class="sxs-lookup"><span data-stu-id="d527c-246">**Note:** You must arrange the arguments  _n1, n2, n3, …_</span></span> <span data-ttu-id="d527c-247">in der folgenden Reihenfolge anordnen: `n1 < n2 < n3 < ...` mit `n1 >= 0`.</span><span class="sxs-lookup"><span data-stu-id="d527c-247">in the following order: `n1 < n2 < n3 < ...` with `n1 >= 0`.</span></span>           <span data-ttu-id="d527c-248">Ein bestimmter Wert für den Eingabeausdruck _b_ wird auf den am nächsten liegenden numerischen Schwellenwert abgerundet.</span><span class="sxs-lookup"><span data-stu-id="d527c-248">A given value for the input expression _b_ is rounded down to the closest numeric threshold given. If lower than the lowest threshold given, the resulting value is zero.</span></span> <span data-ttu-id="d527c-249">Wenn der Wert niedriger als der niedrigste angegebene Schwellenwert ist, ist das Ergebnis Null.</span><span class="sxs-lookup"><span data-stu-id="d527c-249">If lower than the lowest threshold given, the resulting value is zero.</span></span> <br/> |
|<span data-ttu-id="d527c-250">**errtolast(x)**</span><span class="sxs-lookup"><span data-stu-id="d527c-250">**errtolast(x)**</span></span> <br/> |<span data-ttu-id="d527c-p127">Ein Operator zur Steuerung der Behandlung von Formelausnahmen.  _x_ kann ein beliebiger Formelausdruck sein. Führt die Berechnung des Formelausdrucks für ein Element im Resultset zu einer mathematischen Ausnahme, z. B. eine Division durch null, werden diese Elemente unabhängig von der angegebenen Sortierreihenfolge am Ende der Sortierliste angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d527c-p127">An operator that can be used to control how to handle formula exceptions;  _x_ can be any formula expression. If the calculation of this formula expression leads to a mathematical exception for an item in the result set, such as division by zero, these items appear at the end of the sort list, regardless of specified sort direction. </span></span><br/> |
   

### <a name="performance-characteristics-for-sort-by-formula"></a><span data-ttu-id="d527c-253">Leistungsmerkmale für das Sortieren nach einer Formel</span><span class="sxs-lookup"><span data-stu-id="d527c-253">Performance characteristics for sort by formula</span></span>

<span data-ttu-id="d527c-p128">Das Verwenden einer Sortierformel impliziert, dass die Formelberechnungen auf alle gefundenen Elemente im Resultset angewendet werden. Somit hängen die Auswirkungen der Abfrageleistung von der Anzahl der Elemente ab, die der Abfrage entsprechen.</span><span class="sxs-lookup"><span data-stu-id="d527c-p128">Using a sort formula implies that the formula calculations are applied to all matching items in the result set. This means that the query performance impact depends on the number of items that match the query.</span></span>
  
    
    
<span data-ttu-id="d527c-256">Lange Formeln mit vielen Operatoren erfordern mehr Verarbeitungszeit als kurze Formeln.</span><span class="sxs-lookup"><span data-stu-id="d527c-256">Long formulas with many operators require more processing time than short formulas.</span></span>
  
    
    

### <a name="using-sort-by-formula-for-geographical-distance"></a><span data-ttu-id="d527c-257">Verwenden der Sortierung nach einer Formel für geographische Entfernungen</span><span class="sxs-lookup"><span data-stu-id="d527c-257">Using sort by formula for geographical distance</span></span>

<span data-ttu-id="d527c-p129">Sie können mit einer Sortierformel eine Bewertung entsprechend der Entfernung anwenden. Dazu müssen Sie verwaltete Eigenschaften angeben, die die geografische Breite und Länge der einzelnen Elemente darstellen.</span><span class="sxs-lookup"><span data-stu-id="d527c-p129">You can use sort by formula to apply a ranking based on distance. This requires that you include managed properties that represent the latitude and longitude of each item.</span></span>
  
    
    
<span data-ttu-id="d527c-260">Beispielsweise können Sie eine der folgenden Standardformeln verwenden:</span><span class="sxs-lookup"><span data-stu-id="d527c-260">For example, you can use one of the following standard formulas:</span></span>
  
    
    

- <span data-ttu-id="d527c-261">Manhattan-Abstand</span><span class="sxs-lookup"><span data-stu-id="d527c-261">Manhattan distance</span></span>
    
  
- <span data-ttu-id="d527c-262">Euklidischer Abstand (siehe Beispiel 2)</span><span class="sxs-lookup"><span data-stu-id="d527c-262">Euclidian distance (see example 2)</span></span>
    
  
- <span data-ttu-id="d527c-263">Haversinus-Formel</span><span class="sxs-lookup"><span data-stu-id="d527c-263">Haversine formula</span></span>
    
  

> <span data-ttu-id="d527c-264">**Wichtig:** Verwenden Sie verwaltete Eigenschaften vom Typ **Decimal** oder **Float**, um die Werte für die geografische Breite und die geografische Länge anzugeben.</span><span class="sxs-lookup"><span data-stu-id="d527c-264">**Important** Use managed properties of type **Decimal** or **Float** to represent the latitude and longitude values.</span></span>
  
    
    


### <a name="examples"></a><span data-ttu-id="d527c-265">Beispiele</span><span class="sxs-lookup"><span data-stu-id="d527c-265">Examples</span></span>

<span data-ttu-id="d527c-266">Die folgenden Beispiele zeigen, wie Sie die Sortierformel mit dem Abfrage-Objektmodells sortieren.</span><span class="sxs-lookup"><span data-stu-id="d527c-266">The following examples show how to specify the sort formula using the Query object model.</span></span>
  
    
    
 <span data-ttu-id="d527c-p130">**Beispiel 1.** Platzieren der Elemente, deren verwaltete Eigenschaft **height** am nächsten bei 20 liegt, am Anfang der Liste.</span><span class="sxs-lookup"><span data-stu-id="d527c-p130">**Example 1.** Place the items that have the **height** managed property closest to 20 on top of the result list.</span></span>
  
    
    



```cs

using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home"
    };
    query.SortList.Add("[formula:abs(20-height)]", SortDirection.Ascending);

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    { 
        Console.WriteLine(result["Title"]);
    }
}
```

<span data-ttu-id="d527c-269">Alternativ könnten Sie die Such-REST-API verwenden, um die Elemente, deren verwaltete Eigenschaft **height** am nächsten bei 20 liegt, am Anfang der Ergebnisliste zu platzieren. Dazu verwenden Sie den folgenden Aufruf.</span><span class="sxs-lookup"><span data-stu-id="d527c-269">Alternatively, you could use the Search REST API to place the items that have the **height** managed property closest to 20 on top of the result list, with the following call.</span></span>
  
    
    



```HTML

http://localhost/_api/search/query?querytext='home'&amp;sortlist='[formula:abs(20-height)]:ascending
```

 <span data-ttu-id="d527c-p131">**Beispiel 2.** Sortieren nach dem echten dreidimensionalen euklidischen Abstand von einer gegebenen Position (z. B. der Position eines Benutzers). Dieser basiert auf Positionsinformationen, die in den verwalteten Eigenschaften **latitude**, **longitude** und **height** bereitgestellt werden. Die folgende Formel gibt den dreidimensionalen euklidischen Abstand an, unter der Voraussetzung, dass die Basisposition 50/100/200 (Breite/Länge/Höhe) ist.</span><span class="sxs-lookup"><span data-stu-id="d527c-p131">**Example 2.** Sort by true 3-D Euclidean distance from a given position (for example, user's position) based on position information that is provided in the managed properties **latitude**, **longitude** and **height**. The following formula provides the 3-D Euclidean distance, given that the base position is 50/100/200 (latitude/longitude/height).</span></span>
  
    
    
 `sqrt(pow(50-latitude,2)+pow(100-longitude,2)+pow(200-height,2))`
  
    
    
<span data-ttu-id="d527c-273">Wenn Sie entfernungsbasiert sortieren möchten (und nicht durch Kombination der Entfernung mit anderen Parametern in einer Formel), können Sie die  `sqrt()`-Komponente entfernen, da dadurch die Sortierreihenfolge nicht geändert wird. Dies verbessert die Abfrageleistung.</span><span class="sxs-lookup"><span data-stu-id="d527c-273">If you want to apply a distance-based sorting (not combining the distance with other parameters in a formula), you can remove the  `sqrt()` component, as it does not change the sorting sequence; but it improves the query performance.</span></span>
  
    
    



```cs
using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home"
    };
    query.SortList.Add("[formula:pow(50-latitude,2)+pow(100-longitude,2)+pow(200-height,2)]", SortDirection.Ascending);

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    { 
        Console.WriteLine(result["Title"]);
    }
}
```

 <span data-ttu-id="d527c-p132">**Beispiel 3.** Runden der Werte der Größe in Buckets, wobei Werte auf einen der folgenden Werte abgerundet werden: 0, 5, 15, 50, 100. Sortierung mit den größten Werten zuerst.</span><span class="sxs-lookup"><span data-stu-id="d527c-p132">**Example 3.** Round the values of size into buckets, rounding values down to one of the following: 0, 5, 15, 50, 100; sort with largest values first.</span></span>
  
    
    



```

using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home"
    };
    query.SortList.Add("[formula:bucket(size,5,15,50,100)]", SortDirection.Ascending);

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    { 
        Console.WriteLine(result["Title"]);
    }
}
```


## <a name="sort-search-results-in-random-order"></a><span data-ttu-id="d527c-276">Sortieren von Suchergebnissen in zufälliger Reihenfolge</span><span class="sxs-lookup"><span data-stu-id="d527c-276">Sort search results in random order</span></span>
<span data-ttu-id="d527c-277"><a name="SP15_Sort_search_results_in_random_order"> </a></span><span class="sxs-lookup"><span data-stu-id="d527c-277"></span></span>

<span data-ttu-id="d527c-278">Sie können Abfrageergebnisse zufällig sortieren oder der Ergebnissortierung eine zufällige Komponente hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="d527c-278">You may apply random sorting of the query result, or add a random component to the result sorting.</span></span>
  
    
    
<span data-ttu-id="d527c-279">Die zufällige Sortierspezifikation besitzt das folgende Format: `[random:seed=<seed>:hashfield=<managed property>]`</span><span class="sxs-lookup"><span data-stu-id="d527c-279">The random sort specification has the following format:  `[random:seed=<seed>:hashfield=<managed property>]`</span></span>
  
    
    

> <span data-ttu-id="d527c-280">**Hinweis:** Die eckigen Klammern sind Teil der Syntax der Sortierspezifikation.</span><span class="sxs-lookup"><span data-stu-id="d527c-280">**Note** The square brackets are part of the sort specification syntax.</span></span> 
  
    
    

<span data-ttu-id="d527c-281">Tabelle 2 erläutert die Parameter für die Spezifikation der zufälligen Sortierung.</span><span class="sxs-lookup"><span data-stu-id="d527c-281">Table 2 explains the parameters to the random sort specification.</span></span>
  
    
    

<span data-ttu-id="d527c-282">**Tabelle 2. Parameter für die Spezifikation der zufälligen Sortierung**</span><span class="sxs-lookup"><span data-stu-id="d527c-282">**Table 2. Parameters for the random sort specification**</span></span>


|<span data-ttu-id="d527c-283">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="d527c-283">**Parameter**</span></span>|<span data-ttu-id="d527c-284">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="d527c-284">**Description**</span></span>|<span data-ttu-id="d527c-285">**Erforderlich**</span><span class="sxs-lookup"><span data-stu-id="d527c-285">**Required**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="d527c-286">_Seed_</span><span class="sxs-lookup"><span data-stu-id="d527c-286">_Seed_</span></span> <br/> |<span data-ttu-id="d527c-287">Der Startwert für die Generierung der Zufallswerte.</span><span class="sxs-lookup"><span data-stu-id="d527c-287">The seed for the random value generation.</span></span>  <br/> <span data-ttu-id="d527c-p133">Der Startwert dient als Eingabe für eine Funktion, die eine Zufallszahl generiert. Diese Zufallszahl wird in der entgültigen Sortierung verwendet. Wird nur die  _seed_-Option verwendet, erhalten Sie ein zufällig sortiertes Abfrageresultset. Die Sortierreihenfolge für die gleiche Abfrage (mit demselben Startwert) kann nach einer Indexaktualisierung anders ausfallen.</span><span class="sxs-lookup"><span data-stu-id="d527c-p133">The seed value is input to a function that generates a random number. This random number is used in the final sorting.Using only the  _seed_ option will give you a randomly sorted query result set. The sorting order for the same query (when using the same seed) may change after an index update. </span></span><br/> |<span data-ttu-id="d527c-291">Ja</span><span class="sxs-lookup"><span data-stu-id="d527c-291">Yes</span></span>  <br/> |
| <span data-ttu-id="d527c-292">_Hashfield_</span><span class="sxs-lookup"><span data-stu-id="d527c-292">_Hashfield_</span></span> <br/> |<span data-ttu-id="d527c-p134">Eine verwaltete Eigenschaft, die als Hashwert für die zufällige Generierung verwendet wird. Sie können diesen Parameter verwenden, um sicherzustellen, dass die Sortierreihenfolge für die gleiche Abfrage (mit demselben Startwert) nach einer Indexaktualisierung unverändert bleibt.</span><span class="sxs-lookup"><span data-stu-id="d527c-p134">A managed property that is used as the hash value for the random generation. You can use this parameter to ensure that the sorting order for the same query (when using the same seed) does not change after an index update.  </span></span><br/> <span data-ttu-id="d527c-p135"> Die verwaltete Eigenschaft muss vom Typ  [Integer](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) sein und [Sortable()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.Sortable.aspx) sein. Sie können diese verwaltete Eigenschaft mit zufälligen oder eindeutigen Werten (z. B. einer von einer Elementverarbeitungsphase aufgefüllten Sequenznummer) belegen. </span><span class="sxs-lookup"><span data-stu-id="d527c-p135">The managed property must be of type  [Integer](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) and must be [Sortable()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.Sortable.aspx) . You may fill this managed property with random or unique values (for example a sequence number populated by an item processing stage). </span></span><br/> |<span data-ttu-id="d527c-297">Nein</span><span class="sxs-lookup"><span data-stu-id="d527c-297">No</span></span>  <br/> |
   
<span data-ttu-id="d527c-p136">Wenn Sie für gleiche Abfragen denselben Startwert angeben, werden die Elemente in der gleichen Reihenfolge angezeigt. Dies ermöglicht Ihnen, die zufällige Reihenfolge beizubehalten, wenn Sie Suchergebnisse seitenweise anzeigen. Verwenden Sie den  _hashfield_-Parameter, wenn die zufällige Reihenfolge erhalten bleiben soll, falls zufällig zwischen den Abfragen eine Indexaktualisierung stattfindet.</span><span class="sxs-lookup"><span data-stu-id="d527c-p136">By providing the same seed for equal queries, items will be presented in the same order. This enables you to preserve the same random order when paging through search results. Use the  _hashfield_ parameter if you want to preserve the same random order when an index update accidentally occurs between the queries.</span></span>
  
    
    

### <a name="examples"></a><span data-ttu-id="d527c-301">Beispiele</span><span class="sxs-lookup"><span data-stu-id="d527c-301">Examples</span></span>

<span data-ttu-id="d527c-302">Die folgenden Beispiele zeigen, wie Sie die zufällige Sortierung mit dem Abfrage-Objektmodell angeben.</span><span class="sxs-lookup"><span data-stu-id="d527c-302">The following examples show how to specify random sorting by using the Query object model.</span></span>
  
    
    
 <span data-ttu-id="d527c-p137">**Beispiel 1.** Das gesamte Resultset wird in zufälliger Reihenfolge sortiert.</span><span class="sxs-lookup"><span data-stu-id="d527c-p137">**Example 1.** Sort the entire result set in random order.</span></span>
  
    
    



```

using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home"
    };
    query.SortList.Add("[random:seed=5432]", SortDirection.Ascending);

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    { 
        Console.WriteLine(result["Title"]);
    }
}
```

<span data-ttu-id="d527c-305">Alternativ können Sie mit folgendem Aufruf die Such-REST-API zum zufälligen Sortieren des gesamten Resultsets verwenden.</span><span class="sxs-lookup"><span data-stu-id="d527c-305">Alternatively, you could use the Search REST API to sort the entire result set in random order, with the following call.</span></span>
  
    
    



```HTML

http://localhost/_api/search/query?querytext='home'&amp;sortlist='[random:seed=5432]:ascending
```

 <span data-ttu-id="d527c-p138">**Beispiel 2.** Das gesamte Resultset wird in zufälliger Reihenfolge sortiert. Die gleiche zufällige Reihenfolge für die gleiche Abfrage wird mit demselben Startwert beibehalten, auch wenn ein Index umgeschaltet wird. Eine benutzerdefinierte verwaltete Eigenschaft namens **hashvalue** muss im Suchschema vorhanden sein. Sie muss mit zufälligen oder sequenziellen numerischen Werten für alle indizierten Elemente belegt sein.</span><span class="sxs-lookup"><span data-stu-id="d527c-p138">**Example 2.** Sort the entire result set in random order. Preserve the same random sequence for the same query with the same seed, even if an index switch occurs. A custom managed property named **hashvalue** must be available in the search schema, and populated with random or sequential numeric values for all indexed items.</span></span>
  
    
    



```cs
using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home"
    };
    query.SortList.Add("[random:seed=6543:hashfield=hashvalue]", SortDirection.Ascending);

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    { 
        Console.WriteLine(result["Title"]);
    }
}
```


## <a name="additional-resources"></a><span data-ttu-id="d527c-310">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="d527c-310">Additional resources</span></span>
<span data-ttu-id="d527c-311"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d527c-311"></span></span>


-  [<span data-ttu-id="d527c-312">Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d527c-312">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d527c-313">Syntaxreferenz für die Keyword Query Language (KQL)</span><span class="sxs-lookup"><span data-stu-id="d527c-313">Keyword Query Language (KQL) syntax reference</span></span>](keyword-query-language-kql-syntax-reference.md)
    
  
-  [<span data-ttu-id="d527c-314">Syntaxreferenz für FQL (FAST Query Language)</span><span class="sxs-lookup"><span data-stu-id="d527c-314">FAST Query Language (FQL) syntax reference</span></span>](fast-query-language-fql-syntax-reference.md)
    
  
-  [<span data-ttu-id="d527c-315">Übersicht über die REST-API für die SharePoint-Suche</span><span class="sxs-lookup"><span data-stu-id="d527c-315">SharePoint Search REST API overview</span></span>](sharepoint-search-rest-api-overview.md)
    
  
-  <span data-ttu-id="d527c-316">
  [Übersicht über durchforstete und verwaltete Eigenschaften in SharePoint](http://technet.microsoft.com/en-us/library/jj219630%28office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="d527c-316">[Overview of crawled and managed properties in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/jj219630%28office.15%29.aspx)</span></span>
    
  

  
    
    
