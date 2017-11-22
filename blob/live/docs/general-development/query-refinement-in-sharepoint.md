---
title: Abfrageverfeinerung in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ec31782e-1bc5-4dc3-8df7-c29cd5f7f05c
ms.openlocfilehash: 4fcad16df080ba2bd6a8e6bea378e258559305e5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="query-refinement-in-sharepoint"></a><span data-ttu-id="a356f-102">Abfrageeinschränkung in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a356f-102">Query Refinement in SharePoint</span></span>
<span data-ttu-id="a356f-103">In diesem Artikel erfahren Sie, wie Sie die SharePoint-Features zur Abfrageeinschränkung bei der Arbeit mit Suchabfragen und Suchergebnissen programmgesteuert einsetzen können.</span><span class="sxs-lookup"><span data-stu-id="a356f-103">Learn how to use sps15short query refinement features programmatically when you are working with  search queries and results.</span></span>
<span data-ttu-id="a356f-104">Mithilfe von Features zur Abfrageeinschränkung können Sie Endbenutzern passende Einschränkungsoptionen für ihre Abfragen bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="a356f-104">You can use query refinement features to provide end users with refinement options that are relevant for their queries.</span></span> <span data-ttu-id="a356f-105">Die Features erlauben es Endbenutzern, Suchergebnisse anhand von spezifisch für die Ergebnisse berechneten Einschränkungsdaten detaillierter einzugrenzen.</span><span class="sxs-lookup"><span data-stu-id="a356f-105">These features let the end user drill down into search results by using refinement data computed for the results.</span></span> <span data-ttu-id="a356f-106">Die Einschränkungsdaten werden von der Indexkomponente berechnet, basierend auf aggregierten Statistiken zu den verwalteten Eigenschaften aller Ergebnisse einer Suchabfrage.</span><span class="sxs-lookup"><span data-stu-id="a356f-106">The query refinement is based on the aggregation of managed property statistics for all of the results of a search query.</span></span>
  
    
    

<span data-ttu-id="a356f-p102">Die Abfrageeinschränkung wird typischerweise für Metadaten verwendet, die den indizierten Elementen zugeordnet sind, z. B. das Erstellungsdatum, der Autor und Personennamen, die in dem Element vorhanden sind. Mit den entsprechenden Einschränkungsoptionen können Sie eine Abfrage so präzisieren, dass nur Elemente dargestellt werden, die innerhalb einer bestimmten Zeitspanne erstellt wurden oder einen bestimmten Dateityp aufweisen.</span><span class="sxs-lookup"><span data-stu-id="a356f-p102">Typically, query refinement is used for metadata associated with the indexed items, such as creation date, author, or file types that appear in the item. By using the refinement options, you can refine your query to display only items created during a certain time period, or display only items of a specific file type.</span></span>
## <a name="using-refiners-in-the-query-object-model"></a><span data-ttu-id="a356f-109">Verwenden von Einschränkungen im Abfrageobjektmodell</span><span class="sxs-lookup"><span data-stu-id="a356f-109">Using refiners in the Query Object Model</span></span>
<span data-ttu-id="a356f-110"><a name="SP15_Using_refiners"> </a></span><span class="sxs-lookup"><span data-stu-id="a356f-110"></span></span>

<span data-ttu-id="a356f-111">An der Abfrageeinschränkung sind zwei Abfragen beteiligt:</span><span class="sxs-lookup"><span data-stu-id="a356f-111">There are two queries involved in query refinement:</span></span>
  
    
    

1. <span data-ttu-id="a356f-p103">Sie können anfordern, dass eine Reihe von Einschränkungen in den Suchergebnissen zurückgegeben wird, indem Sie  [eine Einschränkungsspezifikation](#SP15_Adding_refiners) zu der Abfrage des Benutzers hinzufügen. Eine Einschränkungsspezifikation ist die Eingabe für die [Refiners](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.Refiners.aspx) -Eigenschaft. Diese Abfrage wird gegen den Suchindex ausgeführt. Die Suchergebnisse bestehen aus relevanten Ergebnissen und Einschränkungsdaten.</span><span class="sxs-lookup"><span data-stu-id="a356f-p103">You can request for a set of refiners to be returned in the search results by  [adding a refiner spec](#SP15_Adding_refiners) to the end user's query. A refiner spec is the input for the [Refiners](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.Refiners.aspx) property. This query is run against the search index. The search results will consist of relevant results and refinement data.</span></span>
    
  
2. <span data-ttu-id="a356f-p104">Sie können die Einschränkungsdaten verwenden, um einen Drilldown in die Suchergebnisse auszuführen, indem Sie  [eine eingeschränkte Abfrage erstellen](#SP15_Creating_refined_query). Fügen Sie die  [RefinementFilters](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.RefinementFilters.aspx) -Eigenschaft zu der Abfrage hinzu, sodass die endgültigen Suchergebnisse sowohl den Anforderungen des ursprünglichen Abfragetexts des Benutzers als auch der ausgewählten Einschränkungsoption aus den Einschränkungsdaten entspricht.</span><span class="sxs-lookup"><span data-stu-id="a356f-p104">You can use the refinement data to drill down into the search results by,  [creating a refined query](#SP15_Creating_refined_query). Add the  [RefinementFilters](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.RefinementFilters.aspx) property to the query so that the final search results will meet the requirements of both the original query text from the end user and the selected refinement option from the refinement data.</span></span>
    
  
<span data-ttu-id="a356f-118">In den folgenden Abschnitten werden diese Schritte ausführlich beschrieben un Codebeispiele bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="a356f-118">The following sections describe these steps in detail, and provide code examples.</span></span>
  
    
    

## <a name="adding-refiners-to-the-end-users-query-by-using-refiner-specs"></a><span data-ttu-id="a356f-119">Hinzufügen von Einschränkungen zu der Abfrage des Benutzers mithilfe von Einschränkungsspezifikationen</span><span class="sxs-lookup"><span data-stu-id="a356f-119">Adding refiners to the end-user's query by using refiner specs</span></span>
<span data-ttu-id="a356f-120"><a name="SP15_Adding_refiners"> </a></span><span class="sxs-lookup"><span data-stu-id="a356f-120"></span></span>

<span data-ttu-id="a356f-p105">Sie können die angeforderten Abfrageeinschränkungen mithilfe der  [Refiners](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.Refiners.aspx) -Eigenschaft der [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.KeywordQuery.aspx) -Klasse angeben. Verwenden Sie die folgende Syntax, um die angeforderten Abfrageeinschränkungen anzugeben:</span><span class="sxs-lookup"><span data-stu-id="a356f-p105">You can specify the requested query refiners by using the  [Refiners](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.Refiners.aspx) property of the [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.KeywordQuery.aspx) class. Use the following syntax to specify the requested query refiners:</span></span>
  
    
    
 `<refiner>[,<refiner>]*`
  
    
    

  
    
    
<span data-ttu-id="a356f-123">Jede  `refiner` weist das folgende Format auf:</span><span class="sxs-lookup"><span data-stu-id="a356f-123">Each  `refiner` has the following format:</span></span>
  
    
    
 `<refiner-name>[(parameter=value[,parameter=value]*)]?`
  
    
    

  
    
    
<span data-ttu-id="a356f-124">Dabei gilt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a356f-124">Where:</span></span>
  
    
    

-  <span data-ttu-id="a356f-p106">`<refiner-name>` ist der Name der verwalteten Eigenschaft, die der Einschränkung zugeordnet ist. Diese verwaltete Eigenschaft muss im Suchschema auf [Refinable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedPropertyInfo.Refinable.aspx) oder [Sortable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedPropertyInfo.Sortable.aspx) festgelegt sein.</span><span class="sxs-lookup"><span data-stu-id="a356f-p106">`<refiner-name>` is the name of the managed property associated with the refiner. This managed property must be set to [Refinable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedPropertyInfo.Refinable.aspx) or [Sortable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedPropertyInfo.Sortable.aspx) in the search schema.</span></span>
    
  
- <span data-ttu-id="a356f-p107">Die optionale Liste von  `parameter=value`-Paaren gibt die nicht standardmäßigen Konfigurationswerte für die benannte Einschränkung an. Wenn ein Parameter für eine Einschränkung nicht innerhalb der Klammern aufgeführt ist, erhalten Sie von der Suchschemakonfiguration die Standardeinstellung. In Tabelle 1 sind mögliche Werte für die  `parameter=value`-Paare aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="a356f-p107">The optional list of  `parameter=value` pairs specifies non-default configuration values for the named refiner. If a parameter for a refiner is not listed inside the parentheses, the search schema configuration gives you the default setting. Table 1 lists possible values for the `parameter=value` pairs.</span></span>
    
  

> <span data-ttu-id="a356f-130">**Hinweis:** Bei der Angabe von Einschränkungen müssen Sie zumindest einen Wert `refiner-name` angeben, also eine verwaltete Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="a356f-130">**Note** When you specify refiners, the minimum requirement is to specify a  `refiner-name`, which is a managed property.</span></span> 

<span data-ttu-id="a356f-131">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="a356f-131">**Example**</span></span>

`Refiners = "FileType"` 
 
 <span data-ttu-id="a356f-132">Sie können auch die erweiterte Syntax verwenden, um die Einschränkungseinstellungen anzupassen.</span><span class="sxs-lookup"><span data-stu-id="a356f-132">Or, you can also use the advanced syntax to adjust the refiner settings.</span></span> 

 <span data-ttu-id="a356f-133">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="a356f-133">**Example**</span></span>

 `Refiners = "FileType,Write(discretize=manual/2013-01-01/2013-08-22/2013-09-15/2013-09-21/2013-09-22),companies"`
  
    
    


<span data-ttu-id="a356f-134">**Tabelle 1: Liste von Parametern für Einschränkungen**</span><span class="sxs-lookup"><span data-stu-id="a356f-134">**Table 1: List of parameters for refiners**</span></span>


|<span data-ttu-id="a356f-135">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="a356f-135">**Parameter**</span></span>|<span data-ttu-id="a356f-136">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="a356f-136">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="a356f-137">_deephits_</span><span class="sxs-lookup"><span data-stu-id="a356f-137">_deephits_</span></span> <br/>|<span data-ttu-id="a356f-p108">Überschreibt die standardmäßige Anzahl von Treffern, die als Grundlage für die Berechnung der Einschränkung verwendet wird. Wenn Einschränkungen erstellt werden, werden alle Ergebnisse für die Abfrage ausgewertet. Bei Verwendung dieses Parameters wird in der Regel die Suchleistung verbessert.</span><span class="sxs-lookup"><span data-stu-id="a356f-p108">Overrides the default number of hits that is used as the basis for refinement computation. When refiners are produced, all results for the query will be evaluated. Normally, using this parameter will improve search performance.  </span></span><br/><span data-ttu-id="a356f-141">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="a356f-141">**Syntax**</span></span> <br/>`deephits=<integer value>` <br/><span data-ttu-id="a356f-142">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="a356f-142">**Example**</span></span> <br/>`price(deephits=1000)` <br/><span data-ttu-id="a356f-143">**Hinweis:** Dieses Limit gilt innerhalb jeder Indexpartition.</span><span class="sxs-lookup"><span data-stu-id="a356f-143">**Note:** This limit applies within each index partition.</span></span> <span data-ttu-id="a356f-144">Da die Aggregation über alle Suchpartitionen hinweg durchgeführt wird, liegt die Anzahl der tatsächlich ausgewerteten Treffer höher als dieser Wert.</span><span class="sxs-lookup"><span data-stu-id="a356f-144">This limit applies within each index partition. The actual number of hits that are evaluated will be larger than this value due to the aggregation across search partitions.</span></span>           |
| <span data-ttu-id="a356f-145">_discretize_</span><span class="sxs-lookup"><span data-stu-id="a356f-145">_discretize_</span></span> <br/>| <span data-ttu-id="a356f-146">Legt benutzerdefinierte Intervalle (Einschränkungsbins) für numerische Einschränkungen fest.</span><span class="sxs-lookup"><span data-stu-id="a356f-146">Specifies custom intervals (refinement bins) for numeric refiners.</span></span> <br/><span data-ttu-id="a356f-147">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="a356f-147">**Syntax**</span></span> <br/>`discretize=manual/<threshold>/<threshold>[/<threshold>]*` <br/><span data-ttu-id="a356f-148">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="a356f-148">**Example**</span></span> <br/>`write(discretize=manual/2013-01-01/2013-08-22/2013-09-15/2013-09-21/2013-09-22)` <br/><span data-ttu-id="a356f-149">Das Attribut `<threshold>` gibt den Schwellenwert für die einzelnen Einschränkungsbins an.</span><span class="sxs-lookup"><span data-stu-id="a356f-149">The `<threshold>` attribute specifies the threshold for each refinement bin.</span></span> <br/><span data-ttu-id="a356f-150">Es gibt ein Intervall für alle Elemente unterhalb des ersten angegebenen Schwellenwerts, ein Intervall zwischen jedem aufeinanderfolgenden Schwellenwert, und ein Intervall für alle Elemente überhalb dem letzten Schwellenwert.</span><span class="sxs-lookup"><span data-stu-id="a356f-150">There is one interval for everything below the first threshold specified, one interval between each consecutive threshold, and one interval for everything above the last threshold.</span></span> <br/><span data-ttu-id="a356f-151">Für eine Einschränkung des Typs **DateTime** geben Sie den Schwellenwert gemäß einem der folgenden ISO 8601-kompatiblen Formate an:</span><span class="sxs-lookup"><span data-stu-id="a356f-151">For a refiner of type **DateTime**, specify the threshold according to one of the following ISO 8601-compatible formats:</span></span>  <br/><ul><li><span data-ttu-id="a356f-152"><i>YYYY-MM-DD</i></span><span class="sxs-lookup"><span data-stu-id="a356f-152"><i>YYYY-MM-DD</i></span></span></li><li><span data-ttu-id="a356f-153"><i>YYYY-MM-DDThh:mm:ss</i></span><span class="sxs-lookup"><span data-stu-id="a356f-153"><i>YYYY-MM-DDThh:mm:ss</i></span></span></li><li><span data-ttu-id="a356f-154"><i>YYYY-MM-DDThh:mm:ss:Z</i></span><span class="sxs-lookup"><span data-stu-id="a356f-154"><i>YYYY-MM-DDThh:mm:ss:Z</i></span></span></li></ul><span data-ttu-id="a356f-155">Die Formatwerte geben Folgendes an:</span><span class="sxs-lookup"><span data-stu-id="a356f-155">The format values specify the following:</span></span> <ul><li><span data-ttu-id="a356f-p110"><i>YYYY</i> - Vierziffrige Jahresangabe. Es werden nur vierziffrige Jahresangaben unterstützt.</span><span class="sxs-lookup"><span data-stu-id="a356f-p110"><i>YYYY</i> - Four-digit year. Only four-digit years are supported. </span></span></li><li><span data-ttu-id="a356f-p111"><i>MM</i> - Zweiziffriger Monat. 01 = Januar.</span><span class="sxs-lookup"><span data-stu-id="a356f-p111"><i>MM</i> - Two-digit month. 01 = January. </span></span></li><li><span data-ttu-id="a356f-160"><i>DD</i> - Zweiziffriger Tag des Monats (01 bis 31).</span><span class="sxs-lookup"><span data-stu-id="a356f-160"><i>DD</i> - Two-digit day of month (01 through 31).</span></span> </li><li><span data-ttu-id="a356f-161"><i>T</i> - Den Buchstaben „T".</span><span class="sxs-lookup"><span data-stu-id="a356f-161"><i>T</i> - The letter "T".</span></span> </li><li><span data-ttu-id="a356f-p112"><i>hh</i> - Zweiziffrige Stundenangabe (00 bis 23). Die Angabe von A.M. oder P.M. ist nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="a356f-p112"><i>hh</i> - Two-digit hour (00 through 23). A.M. or P.M. indication is not allowed. </span></span></li><li><span data-ttu-id="a356f-166"><i>mm</i> - Zweiziffrige Minutenangabe (00 bis 59).</span><span class="sxs-lookup"><span data-stu-id="a356f-166"><i>mm</i> - Two-digit minute (00 through 59).</span></span> </li><li><span data-ttu-id="a356f-167"><i>ss</i> - zweiziffrige Sekundenangabe (00 bis 59)</span><span class="sxs-lookup"><span data-stu-id="a356f-167"><i>ss</i> - Two-digit second (00 through 59).</span></span> </li></ul><span data-ttu-id="a356f-168">**Wichtig:** Alle Datum/Uhrzeit-Werte müssen gemäß der Zeitzone UTC (Coordinated Universal Time, koordinierte Weltzeit) angegeben werden. Sie wird auch GMT (Greenwich Mean Time, mittlere Sonnenzeit am Nullmeridian) genannt.</span><span class="sxs-lookup"><span data-stu-id="a356f-168">All date/time values must be specified according to the Coordinated Universal Time (UTC), also known as Greenwich Mean Time (GMT) zone. The UTC zone identifier (a trailing "Z" character) is optional.</span></span> <span data-ttu-id="a356f-169">Der Bezeichner für die UTC-Zeitzone (ein nachstehendes „Z“) ist optional.</span><span class="sxs-lookup"><span data-stu-id="a356f-169">The UTC zone identifier (a trailing "Z" character) is optional.</span></span>          |
| <span data-ttu-id="a356f-170">_sort_</span><span class="sxs-lookup"><span data-stu-id="a356f-170">_sort_</span></span> <br/>| <span data-ttu-id="a356f-171">Legt die Sortierreihenfolge der Bins in einer Einschränkung des Typs „String“ fest.</span><span class="sxs-lookup"><span data-stu-id="a356f-171">Defines how to sort the bins within a string refiner.</span></span> <br/><span data-ttu-id="a356f-172">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="a356f-172">**Syntax**</span></span> <br/>`sort=<property>/<direction>` <br/><span data-ttu-id="a356f-173">Die Attribute tun Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a356f-173">The attributes perform the following:</span></span> <ul><li><span data-ttu-id="a356f-174"><i>\<property\></i>: Gibt den Sortierungsalgorithmus an.</span><span class="sxs-lookup"><span data-stu-id="a356f-174"><i>\<property\></i> - Specifies the sorting algorithm.</span></span> <span data-ttu-id="a356f-175">Gültig sind die unten aufgeführten Werte (klein geschrieben).</span><span class="sxs-lookup"><span data-stu-id="a356f-175"> - Specifies the sorting algorithm. These lowercase values are valid:</span></span> <ul><li><span data-ttu-id="a356f-176">**frequency** - Sortiert nach Anzahl der Vorkommen innerhalb der Bins.</span><span class="sxs-lookup"><span data-stu-id="a356f-176">**frequency** - Orders by occurrence within the bins.</span></span> </li><li><span data-ttu-id="a356f-177">**name** - Anordnung nach Bezeichnungsname.</span><span class="sxs-lookup"><span data-stu-id="a356f-177">**name** - Orders by label name.</span></span> </li><li><span data-ttu-id="a356f-p115">**number** - Behandelt die Zeichenfolgen als numerisch und verwendet die numerische Sortierung. Dieser Wert kann hilfreich sein, um diskrete Werte anzugeben, beispielsweise, um eine numerische Sortierung für einen Wert auszuführen, der in einer verwalteten Eigenschaft des Typs **String** enthalten ist. </span><span class="sxs-lookup"><span data-stu-id="a356f-p115">**number** - Treats the strings as numeric and uses numeric sorting. This value can be useful to specify discrete values, for example, to perform numeric sorting of a value that is contained in a managed property of type **String**.</span></span></li></ul></li><li><span data-ttu-id="a356f-180"><i>\<direction\></i>: Gibt die Sortierrichtung an.</span><span class="sxs-lookup"><span data-stu-id="a356f-180"><i>\<direction\></i> - Specifies the sorting direction.</span></span> <span data-ttu-id="a356f-181">Gültig sind die unten aufgeführten Werte (klein geschrieben).</span><span class="sxs-lookup"><span data-stu-id="a356f-181"> - Specifies the sorting direction. These lowercase values are valid :</span></span> <ul><li><span data-ttu-id="a356f-182">**descending**</span><span class="sxs-lookup"><span data-stu-id="a356f-182">**descending**</span></span> </li><li><span data-ttu-id="a356f-183">**ascending**</span><span class="sxs-lookup"><span data-stu-id="a356f-183">**ascending**</span></span> </li></ul></li></ul><span data-ttu-id="a356f-184">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="a356f-184">**Example**</span></span> <br/>`sort=name/ascending` <br/><span data-ttu-id="a356f-185">**Standard:** frequency/descending</span><span class="sxs-lookup"><span data-stu-id="a356f-185">**Default**: frequency/descending</span></span>  <br/>|
| <span data-ttu-id="a356f-186">_filter_</span><span class="sxs-lookup"><span data-stu-id="a356f-186">_filter_</span></span> <br/>| <span data-ttu-id="a356f-187">Definiert, wie Bins innerhalb einer Einschränkung des Typs **String** gefiltert werden, bevor sie an den Client zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="a356f-187">Defines how bins within a refiner of type **String** are filtered before they are returned to the client.</span></span> <br/><span data-ttu-id="a356f-188">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="a356f-188">**Syntax**</span></span> <br/> `filter=<bins>/<freq>/<prefix>[<levels>]` <br/><span data-ttu-id="a356f-189">Die Attribute tun Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a356f-189">The attributes perform the following:</span></span> <ul><li><span data-ttu-id="a356f-190"><i>\<bins\></i>: Gibt an, wie viele Bins maximal zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="a356f-190"><bins> - Specifies the maximum number of returned bins.</span></span> <br/><span data-ttu-id="a356f-191">Verwenden Sie dieses Attribut nach der Sortierung der Bins innerhalb der Einschränkung, um nachfolgende Bins abzuschneiden. Bei bins=10 werden gemäß des angegebenen Sortieralgorithmus beispielsweise nur die ersten 10 Bins zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="a356f-191">After sorting the bins within the refiner, use this attribute to truncate any trailing bins. For example, if bins=10, only the first 10 bins are returned, according to the specified sorting algorithm.</span></span> </li><li><span data-ttu-id="a356f-192"><i>\<freq\></i>: Beschränkt die Anzahl der zurückgegebenen Bins.</span><span class="sxs-lookup"><span data-stu-id="a356f-192"><freq> - Limits the number of returned bins.</span></span> <br/><span data-ttu-id="a356f-p117">Verwenden Sie dieses Attribut, um Bins zu entfernen, die nur selten vorkommen. <i>freq</i>=2 bedeutet beispielsweise, dass nur die Bins mit 2 oder mehr Mitgliedern zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="a356f-p117">Use this attribute to remove bins that have low frequency counts. For example, <i>freq</i>=2 indicates that only the bins with 2 or more members are returned.  </span></span></li><li><span data-ttu-id="a356f-195"><i>\<prefix\></i>: Legt fest, dass nur Bins zurückgegeben werden, deren Name mit dem angegebenen Präfix beginnt.</span><span class="sxs-lookup"><span data-stu-id="a356f-195"><prefix> - Specifies that only bins with a name that begins with this prefix are returned.</span></span> <br/><span data-ttu-id="a356f-196">Wenn Sie das Platzhalterzeichen „\*“ setzen, wird der Filter namensunabhängig auf alle Bins angewendet.</span><span class="sxs-lookup"><span data-stu-id="a356f-196">The wildcard character "*" will match all names.</span></span> <br/><span data-ttu-id="a356f-197">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="a356f-197">**Example**</span></span> <br/>`filter=30/2/*` </li><li><span data-ttu-id="a356f-198"><i>\<levels\></i>: Gibt die Taxonomieebenen an.</span><span class="sxs-lookup"><span data-stu-id="a356f-198"><levels> - Specifies the levels of taxonomy.</span></span> <br/><span data-ttu-id="a356f-199">Mithilfe dieses Attributs können Sie die Ausgabe hierarchischer Einschränkungen auf Basis von Taxonomieebenen filtern.</span><span class="sxs-lookup"><span data-stu-id="a356f-199">Use this attribute to filter hierarchical refiner output based on taxonomy levels.</span></span> <span data-ttu-id="a356f-200">Der Attributwert muss eine positive ganze Zahl <i>n</i> sein.</span><span class="sxs-lookup"><span data-stu-id="a356f-200">The attribute should be a positive integer <i>n</i>.</span></span> <span data-ttu-id="a356f-201">Der **Standardwert** ist <i>n</i> = 0.</span><span class="sxs-lookup"><span data-stu-id="a356f-201">The **default** value is <i>n</i>=0.</span></span> <span data-ttu-id="a356f-202">Ist <i>n</i>\>0 gesetzt, werden nur Einschränkungseinträge zurückgegeben, deren Taxonomiepfad weniger als <i>n</i> Trennzeichen („/“) enthält.</span><span class="sxs-lookup"><span data-stu-id="a356f-202">If n>0, only refiner entries containing less than n taxonomy path separator symbols ("/") will be returned. If n=0, no level filtering is performed.</span></span> <span data-ttu-id="a356f-203">Wenn <i>n</i>=0 gesetzt ist, wird keine Ebenenfilterung angewendet.</span><span class="sxs-lookup"><span data-stu-id="a356f-203">If <i>n</i>=0, no level filtering is performed.</span></span> <span data-ttu-id="a356f-204">Das Ebenentrennzeichen ist der Schrägstrich („/“).</span><span class="sxs-lookup"><span data-stu-id="a356f-204">The level separator is the forward slash character ("/").</span></span>  <br/><span data-ttu-id="a356f-p119">Bedenken Sie immer die Leistungseinbußen, die mit einem großen Taxonomienavigator einhergehen. Die Filterung wird als Teil der Ergebnisverarbeitung durchgeführt. </span><span class="sxs-lookup"><span data-stu-id="a356f-p119">Be aware of the performance cost of using a large taxonomy navigator. The filtering is performed as part of the result processing. </span></span></li></ul><span data-ttu-id="a356f-207">**Hinweis:** Dieser Parameter wendet anwendungsspezifische ergebnisseitige Filterung an.</span><span class="sxs-lookup"><span data-stu-id="a356f-207">**Note:**  This parameter applies application-specific result-side filtering.</span></span> <span data-ttu-id="a356f-208">Damit unterscheidet er sich vom Parameter „cutoff“, der aus Leistungsgründen Grenzwerte auf jede Indexpartition anwendet.</span><span class="sxs-lookup"><span data-stu-id="a356f-208">This parameter applies application-specific result-side filtering. This differs from the cutoff parameter, which applies limitations in every index partition for performance reasons.</span></span>          |
| <span data-ttu-id="a356f-209">_cutoff_</span><span class="sxs-lookup"><span data-stu-id="a356f-209">_cutoff_</span></span> <br/>| <span data-ttu-id="a356f-p121">Schränkt die Daten ein, die für tiefe Zeichenfolgeneinschränkungen übertragen und verarbeitet werden müssen. Sie können die Einschränkungen so konfigurieren, dass nur die relevantesten Werte (Bins) zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="a356f-p121">Limits the data that must be transferred and processed for deep string refiners. You can configure the refiners to return only the most relevant values (bins). </span></span><br/><span data-ttu-id="a356f-212">**Hinweis:** Die Filterung auf Basis des Parameters „cutoff“ wird innerhalb jeder Indexpartition durchgeführt.</span><span class="sxs-lookup"><span data-stu-id="a356f-212">**Note:**  This cutoff filtering is performed within each index partition.</span></span> <span data-ttu-id="a356f-213">Damit unterscheidet sich dieser Parameter vom Parameter _filter_, der ausschließlich eine ergebnisseitige Filterung durchführt.</span><span class="sxs-lookup"><span data-stu-id="a356f-213">This cutoff filtering is performed within each index partition. This differs from the _filter_ parameter, which performs result-side filtering only. You can combine the two parameters.</span></span> <span data-ttu-id="a356f-214">Sie können die beiden Parameter miteinander kombinieren.</span><span class="sxs-lookup"><span data-stu-id="a356f-214">You can combine the two parameters.</span></span> <br/><span data-ttu-id="a356f-215">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="a356f-215">**Syntax**</span></span> <br/>`cutoff=<frequency>/<minbins>/<maxbins>` <br/><span data-ttu-id="a356f-216">Die Attribute tun Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a356f-216">The attributes perform the following:</span></span> <ul><li><span data-ttu-id="a356f-217"><i>\<maxbins\></i>: Schränkt die Anzahl der Bins ein.</span><span class="sxs-lookup"><span data-stu-id="a356f-217"><maxbins> - Limits the number of bins.</span></span> <br/><span data-ttu-id="a356f-p123">Dieser Parameter schränkt die Anzahl eindeutiger Werte (Bins) ein, die für eine Einschränkung zurückgegeben werden. Dies ist die bevorzugte Methode, um die Suchleistung zu steigern, wenn Zeichenfolgeneinschränkungen mit einer großen Anzahl von Bins zurückgegeben werden. „0" bedeutet, dass der im Suchschema angegebene Standardwert verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="a356f-p123">This parameter limits the number of unique values (bins) that will be returned for a refiner. It is the preferred way to increase search performance when string refiners with large number of bins are returned. "0" implies that the default value specified in the search schema is used. </span></span></li><li><span data-ttu-id="a356f-221"><i>\<frequency\></i>: Schränkt die Anzahl der Bins basierend auf der Häufigkeit ihres Vorkommens ein.</span><span class="sxs-lookup"><span data-stu-id="a356f-221"><frequency> - Limits the number of bins by frequency.</span></span> <br/><span data-ttu-id="a356f-p124">Wenn die Anzahl der Vorkommnisse eines Einschränkungswerts in einem Resultset kleiner oder gleich dem Häufigkeitswert ist, wird der Einschränkungswert nicht zurückgegeben. „0" bedeutet, dass der Standardwert gemäß des Suchschemas verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="a356f-p124">If the number of occurrences of a refiner value in a result set is less than or equal to the frequency value, the refiner value is not returned. "0" implies that the default value according to the search schema is used. </span></span></li><li><span data-ttu-id="a356f-224"><i>\<minbins\></i>: Legt den Mindestwert für die häufigkeitsbasierte Einschränkung fest.</span><span class="sxs-lookup"><span data-stu-id="a356f-224"><minbins> - Specifies the minimum value for frequency cutoff.</span></span> <br/><span data-ttu-id="a356f-p125">Wenn die Anzahl eindeutiger Einschränkungswerte für die Abfrage niedriger als dieser Wert ist, wird keine Häufigkeitsabtrennung durchgeführt, und alle Einschränkungswerte werden von dieser Suchpartition zurückgegeben. Wenn eine Abtrennung nach Häufigkeit verwendet wird, kann dieser Parameter verwendet werden, um eine minimale Anzahl von eindeutigen Einschränkungswerten anzugeben, die zurückgegeben werden, unabhängig von der Anzahl von Vorkommnissen. Der Standarwert dieses Attributs ist „0"; dadurch wird angegeben, dass die Häufigkeitsabtrennung unabhängig von der Anzahl eindeutiger Navigatorwerte durchgeführt wird. „0" bedeutet, dass der im Indexschema angegebene Standardwert verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="a356f-p125">If the number of unique refiner values for the query is less than this value, no frequency cutoff is performed, and all refiner values are returned from that search partition. When cutoff by frequency is used, this parameter can be used to specify a minimum number of unique refiner values that will be returned regardless of the number of occurrences. The default value of this attribute is "0", indicating that frequency cutoff is performed regardless of the number of unique navigator values. "0" implies that the default value specified in the index schema is used. </span></span></li></ul><span data-ttu-id="a356f-229">**Hinweis:** Verwenden Sie die Parameter _\<frequency\>_ und _\<minbins\>_ mit Bedacht.</span><span class="sxs-lookup"><span data-stu-id="a356f-229">**Note:**  Use _\<frequency\>_ and _\<minbins\>_ with care.</span></span> <span data-ttu-id="a356f-230">Wir empfehlen Ihnen, nur den Parameter _\<maxbins\>_ zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="a356f-230">Use    and    with care. We recommend that you use only   .</span></span>           |
   

### <a name="example-adding-refiners"></a><span data-ttu-id="a356f-231">Beispiel: Hinzufügen von Einschränkungen</span><span class="sxs-lookup"><span data-stu-id="a356f-231">Example: Adding refiners</span></span>
<span data-ttu-id="a356f-232"><a name="SP15_Example_adding_refiners"> </a></span><span class="sxs-lookup"><span data-stu-id="a356f-232"></span></span>

<span data-ttu-id="a356f-p127">Im folgenden CSOM-Beispiel wird gezeigt, wie drei Einschränkungen programmgesteuert angefordert werden: **FileType**, **Write** und **Companies**. **Write** stellt das Datum der letzten Änderung für das Element dar und verwendet die erweiterte Syntax, um Datums-/Uhrzeitbins mit fester Größe zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="a356f-p127">The following CSOM example shows how to programmatically request three refiners: **FileType**, **Write**, and **Companies**. **Write** represents the last modified date for the item, and uses the advanced syntax to return fixed-size date/time bins.</span></span>
  
    
    

```cs

using (var context = new ClientContext("http://<serverName>/<siteCollectionPath>"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home",
        Refiners = "FileType,Write(discretize=manual/2013-01-01/2013-08-22/2013-09-
            15/2013-09-21/2013-09-22),companies"
    };
    
    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    ResultTable relevantResultsTable = results.Value[0];
    ResultTable refinerResultsTable = results.Value[1];          
    Console.WriteLine(refinerResultsTable.RowCount + " refinement options:");
    foreach (var refinementOption in refinerResultsTable.ResultRows)
    {
        Console.WriteLine("RefinerName: '{0}' RefinementName: '{1}'
            RefinementValue: '{2}' RefinementToken: '{3}' RefinementCount: '{4}'", 
            refinementOption["RefinerName"],
            refinementOption["RefinementName"],
            refinementOption["RefinementValue"],
            refinementOption["RefinementToken"],
            refinementOption["RefinementCount"]
        );
    }
}
```


## <a name="understanding-the-refinement-data-in-the-search-result"></a><span data-ttu-id="a356f-235">Verstehen der Einschränkungsdaten im Suchergebnis</span><span class="sxs-lookup"><span data-stu-id="a356f-235">Understanding the refinement data in the search result</span></span>
<span data-ttu-id="a356f-236"><a name="SP15_Understanding_refinement_data"> </a></span><span class="sxs-lookup"><span data-stu-id="a356f-236"></span></span>

<span data-ttu-id="a356f-p128">Wenn Sie die Abfrageeinschränkung für eine verwaltete Eigenschaft in Ihrer Abfrage aktiviert haben, enthält das Abfrageergebnis Einschränkungsdaten, die in Einschränkungsbins unterteilt sind. Diese Daten befinden sich in der **RefinementResults**-Tabelle ( [RefinementResults](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KnownTableTypes.RefinementResults.aspx) ) innerhalb der [ResultTableCollection](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ResultTableCollection.aspx) . Ein Einschränkungsbin stellt einen bestimmten Wert oder Wertebereich für die verwaltete Eigenschaft dar. Die **RefinementResults**-Tabelle enthält eine Zeile pro Einschränkungsbin und enthält die Spalten, wie in Tabelle 2 angegeben.</span><span class="sxs-lookup"><span data-stu-id="a356f-p128">If you have enabled query refinement for a managed property in your query, the query result contains refinement data split into refinement bins. This data is located in the **RefinementResults** table ( [RefinementResults](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KnownTableTypes.RefinementResults.aspx) ) within the [ResultTableCollection](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ResultTableCollection.aspx) . One refinement bin represents a specific value or value range for the managed property.The **RefinementResults** table contains one row per refinement bin, and contains the columns, as specified in Table 2.</span></span>
  
    
    

<span data-ttu-id="a356f-239">**Tabelle 2: Für Einschränkungsbins zurückgegebene Daten**</span><span class="sxs-lookup"><span data-stu-id="a356f-239">**Table 2: Data returned for refinement bins**</span></span>


|<span data-ttu-id="a356f-240">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="a356f-240">**Parameter**</span></span>|<span data-ttu-id="a356f-241">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="a356f-241">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="a356f-242">**RefinerName**</span><span class="sxs-lookup"><span data-stu-id="a356f-242">**RefinerName**</span></span> <br/>|<span data-ttu-id="a356f-243">Der Name der Abfrageeinschränkung.</span><span class="sxs-lookup"><span data-stu-id="a356f-243">The name of the query refiner.</span></span>  <br/>|
|<span data-ttu-id="a356f-244">**RefinementName**</span><span class="sxs-lookup"><span data-stu-id="a356f-244">**RefinementName**</span></span> <br/>|<span data-ttu-id="a356f-p129">Die Zeichenfolge, die das Einschränkungsbin darstellt. Diese Zeichenfolge wird in der Regel verwendet, wenn Einschränkungsoptionen für die Benutzer auf einer Suchergebnisseite präsentiert werden.</span><span class="sxs-lookup"><span data-stu-id="a356f-p129">The string that represents the refinement bin. This string is typically used when presenting the refinement options to the users on a search result page.</span></span>  <br/>|
|<span data-ttu-id="a356f-247">**RefinementValue**</span><span class="sxs-lookup"><span data-stu-id="a356f-247">**RefinementValue**</span></span> <br/>|<span data-ttu-id="a356f-p130">Eine implementierungsspezifische formatierte Zeichenfolge, die die Einschränkung darstellt. Diese Daten werden zum Debuggen zurückgegeben und sind normalerweise für den Client nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="a356f-p130">An implementation-specific formatted string that represents refinement. This data is returned for debugging and is typically not required for the client.</span></span>  <br/>|
|<span data-ttu-id="a356f-250">**RefinementToken**</span><span class="sxs-lookup"><span data-stu-id="a356f-250">**RefinementToken**</span></span> <br/>|<span data-ttu-id="a356f-251">Eine Zeichenfolge, die das für **RefinerName** zu verwendende Einschränkungsbin darstellt, wenn Sie eine eingeschränkte Abfrage ausführen.</span><span class="sxs-lookup"><span data-stu-id="a356f-251">A string that represents the refinement bin to use with **RefinerName** when you perform a refined query.</span></span> <br/>|
|<span data-ttu-id="a356f-252">**RefinementCount**</span><span class="sxs-lookup"><span data-stu-id="a356f-252">**RefinementCount**</span></span> <br/>|<span data-ttu-id="a356f-p131">Die Anzahl der Ergebnisse für dieses Einschränkungsbin. Diese Daten stellen die Anzahl von Elementen (einschließlich Duplikaten) im Suchergebnis mit einem Wert für die angegebene verwaltete Eigenschaft dar, der in dieses Einschränkungsbin fällt.</span><span class="sxs-lookup"><span data-stu-id="a356f-p131">The result count for this refinement bin. This data represents the number of items (including duplicates) in the search result with a value for the given managed property that falls into this refinement bin.</span></span>  <br/>|
   

### <a name="example-refinement-data"></a><span data-ttu-id="a356f-255">Beispiel: Einschränkungsdaten</span><span class="sxs-lookup"><span data-stu-id="a356f-255">Example: Refinement data</span></span>
<span data-ttu-id="a356f-256"><a name="SP15_Example_refinement_data"> </a></span><span class="sxs-lookup"><span data-stu-id="a356f-256"></span></span>

<span data-ttu-id="a356f-p132">Tabelle 3 unten enthält zwei Zeilen mit Einschränkungsdaten. Die erste Zeile enthält Einschränkungsdaten für indizierte Elemente, wobei der Dateityp HTML ist. Die zweite Zeile enthält Einschränkungsdaten für indizierte Elemente, wobei der Zeitpunkt der letzten Bearbeitung zwischen 21.09.2013 und 22.09.2013 liegt.</span><span class="sxs-lookup"><span data-stu-id="a356f-p132">Table 3 below contains two rows of refinement data. The first row holds refinement data for indexed items, where the file type is HTML. The second row holds refinement data for indexed items, where the last modified time is from 2013/09/21 until 2013/09/22.</span></span>
  
    
    

<span data-ttu-id="a356f-260">**Tabelle 3: Format und Inhalt der Einschränkungsdaten**</span><span class="sxs-lookup"><span data-stu-id="a356f-260">**Table 3: Format and contents of refinement data**</span></span>


|<span data-ttu-id="a356f-261">**RefinerName**</span><span class="sxs-lookup"><span data-stu-id="a356f-261">**RefinerName**</span></span>|<span data-ttu-id="a356f-262">**RefinementName**</span><span class="sxs-lookup"><span data-stu-id="a356f-262">**RefinementName**</span></span>|<span data-ttu-id="a356f-263">**RefinementValue**</span><span class="sxs-lookup"><span data-stu-id="a356f-263">**RefinementValue**</span></span>|<span data-ttu-id="a356f-264">**RefinementToken**</span><span class="sxs-lookup"><span data-stu-id="a356f-264">**RefinementToken**</span></span>|<span data-ttu-id="a356f-265">**RefinementCount**</span><span class="sxs-lookup"><span data-stu-id="a356f-265">**RefinementCount**</span></span>|
|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="a356f-266">FileType</span><span class="sxs-lookup"><span data-stu-id="a356f-266">FileType</span></span>  <br/>|<span data-ttu-id="a356f-267">HTML</span><span class="sxs-lookup"><span data-stu-id="a356f-267">Html</span></span>  <br/>|<span data-ttu-id="a356f-268">HTML</span><span class="sxs-lookup"><span data-stu-id="a356f-268">Html</span></span>  <br/>|<span data-ttu-id="a356f-269">"????68746d6c"</span><span class="sxs-lookup"><span data-stu-id="a356f-269">"????68746d6c"</span></span>  <br/>|<span data-ttu-id="a356f-270">50553</span><span class="sxs-lookup"><span data-stu-id="a356f-270">50553</span></span>  <br/>|
|<span data-ttu-id="a356f-271">Schreiben</span><span class="sxs-lookup"><span data-stu-id="a356f-271">Write</span></span>  <br/>|<span data-ttu-id="a356f-272">Von 2013-09-21T00:00:00Z bis 2013-09-22T00:00:00Z</span><span class="sxs-lookup"><span data-stu-id="a356f-272">From 2013-09-21T00:00:00Z up to 2013-09-22T00:00:00Z</span></span>  <br/>|<span data-ttu-id="a356f-273">Von 2013-09-21T00:00:00Z bis 2013-09-22T00:00:00Z</span><span class="sxs-lookup"><span data-stu-id="a356f-273">From 2013-09-21T00:00:00Z up to 2013-09-22T00:00:00Z</span></span>  <br/>|<span data-ttu-id="a356f-274">range(2013-09-21T00:00:00Z, 2013-09-22T00:00:00Z)</span><span class="sxs-lookup"><span data-stu-id="a356f-274">range(2013-09-21T00:00:00Z, 2013-09-22T00:00:00Z)</span></span>  <br/>|<span data-ttu-id="a356f-275">37</span><span class="sxs-lookup"><span data-stu-id="a356f-275">+37</span></span>  <br/>|
   

## <a name="creating-a-refined-query"></a><span data-ttu-id="a356f-276">Erstellen einer Einschränkungsabfrage</span><span class="sxs-lookup"><span data-stu-id="a356f-276">Creating a refined query</span></span>
<span data-ttu-id="a356f-277"><a name="SP15_Creating_refined_query"> </a></span><span class="sxs-lookup"><span data-stu-id="a356f-277"></span></span>

<span data-ttu-id="a356f-p133">Ein Suchergebnis stellt Einschränkungsoptionen in der Form von Zeichenfolgenwerten oder Wertebereichen dar. Jeder Zeichenfolgenwert oder numerische Wertebereich wird als Einschränkungsbin bezeichnet, und jeder Einschränkungsbin weist einen zugewiesenen **RefinementToken**-Wert auf. Eine Einschränkungsoption ist einer verwalteten Eigenschaft zugeordnet, die vom **RefinerName**-Wert bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="a356f-p133">A search result presents refinement options in the form of string values or value ranges. Each string value or numeric value range is called a refinement bin, and each refinement bin has an associated **RefinementToken** value. A refinement option is associated with a managed property, which is provided by the **RefinerName** value.</span></span>
  
    
    
<span data-ttu-id="a356f-p134">Sowohl der Wert **RefinementToken** als auch der Wert **RefinerName** ist verkettet, sodass eine _refinement filter_-Zeichenfolge erstellt wird. Diese Zeichenfolge stellt einen Filter dar, der verwendet werden kann, um Suchergebnisse so einzuschränken, dass nur Elemente enthalten sind, bei denen eine verwaltete Eigenschaft einen Wert innerhalb eines Einschränkungsbin aufweist. Kurz ausgedrückt:</span><span class="sxs-lookup"><span data-stu-id="a356f-p134">Both the **RefinementToken** and **RefinerName** values are concatenated to create a _refinement filter_ string. This string represents a filter that can be used to limit search result items to include only items where a managed property has a value within a refinement bin. In short:</span></span>
  
    
    
 `refinement filter = <RefinerName>:<RefinementToken>`
  
    
    
<span data-ttu-id="a356f-p135">Sie können einen oder mehrere Einschränkungsfilter für eine eingeschränkte Abfrage angeben, indem Sie der  [RefinementFilters](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.RefinementFilters.aspx) -Eigenschaft der [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx) -Klasse Einschränkungsfilter hinzufügen. Mit mehreren Einschränkungsfiltern können Sie einen Drilldown über mehrere Stufen in Suchergebnisse bereitstellen und eine Einschränkung auf Eigenschaften mit mehreren Werten anwenden. Sie können beispielsweise die Abfrage auf Elemente mit zwei Autoren einschränken, von denen jeder von einem Einschränkungsbin dargestellt wird, aber Elemente ausschließen, die nur einen der Autoren enthalten.</span><span class="sxs-lookup"><span data-stu-id="a356f-p135">You can provide one or more refinement filters for a refined query by adding refinement filters to the  [RefinementFilters](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.RefinementFilters.aspx) property of the [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx) class. Multiple refinement filters enable you to provide multilevel drill-down into the search results, and to apply refinement on multivalued properties. For example, you can refine the query to items that have two authors - each represented by a refinement bin - but exclude items that have only one of the authors.</span></span>
  
    
    

### <a name="example-1-creating-a-refined-query-for-html-file-types"></a><span data-ttu-id="a356f-287">Beispiel 1: Erstellen einer eingeschränkten Abfrage für Dateien des Typs HTML</span><span class="sxs-lookup"><span data-stu-id="a356f-287">Example 1: Creating a refined query for HTML file types</span></span>

<span data-ttu-id="a356f-288">Das folgende CSOM-Beispiel demonstriert, wie Sie programmgesteuert eine Einschränkung implementieren können, die die Suchergebnisse ausschließlich auf Dateien des Typs HTML eingrenzt.</span><span class="sxs-lookup"><span data-stu-id="a356f-288">The following CSOM example shows how to programmatically perform a refinement, to limit the search results to those of HTML file type only. As mentioned in Table 3, refinement data related to this refinement option has RefinerName set to Filetype and RefinementToken set to "ǂǂ68746d6c".</span></span> <span data-ttu-id="a356f-289">Wie bereits im Abschnitt [Beispiel: Einschränkungsdaten](#SP15_Example_refinement_data) erwähnt, ist in den zu dieser Einschränkungsoption gehörenden Einschränkungsdaten der Parameter **RefinerName** auf _Filetype_ gesetzt und der Parameter **RefinementToken** auf _"????68746d6c"_.</span><span class="sxs-lookup"><span data-stu-id="a356f-289">The following CSOM example shows how to programmatically perform a refinement, to limit the search results to those of HTML file type only. As mentioned in  [Example: Refinement data](#SP15_Example_refinement_data), refinement data related to this refinement option has **RefinerName** set to _Filetype_ and **RefinementToken** set to _"ǂǂ68746d6c"_.</span></span>
  
    
    

```cs

using (var context = new ClientContext("http://<serverName>/<siteCollectionPath>"))
{
    var query = new KeywordQuery(context)
    {        
        QueryText = "home"
    };
    
    query.RefinementFilters.Add("FileType:\\"????68746d6c\\"");
    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    ResultTable relevantResultsTable = results.Value[0];
    var resultCount = 1;
    foreach (var relevantResult in relevantResultsTable.ResultRows)
    {
        Console.WriteLine("Relevant result number {0} has file type {1}.", 
            resultCount, relevantResult["FileType"]);
            resultCount++;
    }
}
```


### <a name="example-2-creating-a-refined-query-by-using-previously-obtained-refinement-data"></a><span data-ttu-id="a356f-290">Beispiel 2: Erstellen einer eingeschränkten Abfrage auf Basis von zuvor abgerufenen Einschränkungsdaten</span><span class="sxs-lookup"><span data-stu-id="a356f-290">Example 2: Creating a refined query by using previously obtained refinement data</span></span>

<span data-ttu-id="a356f-p137">Im folgenden CSOM-Beispiel wird veranschaulicht, wie eine Abfrage mit einer Einschränkungsspezifikation ausgeführt wird, um Einschränkungsdaten zu erstellen, die anschließend zum Durchführen einer Einschränkung verwendet werden. In diesem Beispiel wird der Prozess simuliert, bei dem ein Benutzer die erste Einschränkungsoption auswählt.</span><span class="sxs-lookup"><span data-stu-id="a356f-p137">The following CSOM example shows how to run a query with a refiner spec to create refinement data which is subsequently used to perform refinement. This example simulates the process of an end user selecting the first refinement option.</span></span>
  
    
    

```cs

using (var context = new ClientContext("http://<serverName>/<siteCollectionPath>"))
{
    // Step 1: Run the query with refiner spec to provide refinement data in search result
    var query = new KeywordQuery(context)
    {
        QueryText = "home",
        Refiners = "FileType,Write(discretize=manual/2013-01-01/2013-08-22/
2013-09-15/2013-09-21/2013-09-22),companies"
    };
    
    Console.WriteLine("Run query '{0}' with refiner spec '{1}'.", query.QueryText,
query.Refiners);
    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);
    context.ExecuteQuery();

    // The query has been run and we can now look at the refinement data, to view the
    // refinement options
    ResultTable relevantResultsTable = results.Value[0];
    ResultTable refinerResultsTable = results.Value[1];
    Console.WriteLine("Got back {0} refinement options in the result:",
        refinerResultsTable.RowCount);
    
    foreach (var refinementOption in refinerResultsTable.ResultRows)
    {
        Console.WriteLine("RefinerName: '{0}' RefinementName: '{1}'
            RefinementValue: '{2}' RefinementToken: '{3}' RefinementCount: '{4}'",
            refinementOption["RefinerName"],
            refinementOption["RefinementName"],
            refinementOption["RefinementValue"],
            refinementOption["RefinementToken"],
            refinementOption["RefinementCount"]
        );
    }

    // Step 2: Run the refined query with refinement filter to drill down into 
    // the search results. This example uses the first refinement option in the refinement
    // data, if available. This simulates an end user selecting this refinement option.
    var refinementOptionArray = refinerResultsTable.ResultRows.ToArray();

    if (refinementOptionArray.Length > 0)
    {                         
        var firstRefinementOption = refinementOptionArray[6];x
        // Construct the refinement filter by concatenation
        var refinementFilter = firstRefinementOption["RefinerName"] + ":" +
            firstRefinementOption["RefinementToken"];
        var refinedQuery = new KeywordQuery(context)
        {
            QueryText = query.QueryText
        };
        refinedQuery.RefinementFilters.Add(refinementFilter);
        refinedQuery.SelectProperties.Add("FileType");
        refinedQuery.SelectProperties.Add("Write");
        refinedQuery.SelectProperties.Add("Companies");
        Console.WriteLine("Run query '{0}' with refinement filter '{1}'",            
            refinedQuery.QueryText, refinementFilter);
        var refinedResults = executor.ExecuteQuery(refinedQuery);
        context.ExecuteQuery();
        ResultTable refinedRelevantResultsTable = refinedResults.Value[0];
        var resultCount = 1;
        foreach (var relevantResult in refinedRelevantResultsTable.ResultRows)
        {
            Console.WriteLine("Relevant result number {0} has FileType='{1}',
                Write='{2}', Companies='{3}'", 
                resultCount, 
                relevantResult["FileType"],
                relevantResult["Write"],
                relevantResult["Companies"]
            );
            resultCount++;
        }
    }
}
```


## <a name="additional-resources"></a><span data-ttu-id="a356f-293">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="a356f-293">Additional resources</span></span>
<span data-ttu-id="a356f-294"><a name="SP15_Query_refinement_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a356f-294"></span></span>


-  [<span data-ttu-id="a356f-295">Konfigurieren der Eigenschaften des Einschränkungs-Webparts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a356f-295">Configure properties of the Refinement Web Part in SharePoint Server 2013</span></span>](http://technet.microsoft.com/de-DE/library/gg549985.aspx)
    
  
-  [<span data-ttu-id="a356f-296">Übersicht über das Suchschema in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a356f-296">Overview of the search schema in SharePoint</span></span>](http://technet.microsoft.com/de-DE/library/jj219669%28office.15%29.aspx)
    
  

## <a name="see-also"></a><span data-ttu-id="a356f-297">Weitere Artikel</span><span class="sxs-lookup"><span data-stu-id="a356f-297">See also</span></span>
<span data-ttu-id="a356f-298"><a name="SP15_Query_refinement_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a356f-298"></span></span>


#### <a name="other-resources"></a><span data-ttu-id="a356f-299">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="a356f-299">Other resources</span></span>


  
    
    
 [<span data-ttu-id="a356f-300">Indexschema (FAST Search Server für SharePoint)</span><span class="sxs-lookup"><span data-stu-id="a356f-300">Index Schema (FAST Search Server 2010 for SharePoint)</span></span>](http://msdn.microsoft.com/library/3e1eed3f-8a6f-4911-9607-f1616e6a44f3%28Office.15%29.aspx)
  
    
    
 [<span data-ttu-id="a356f-301">Refiner-Element im Microsoft.Search.Query-Schema</span><span class="sxs-lookup"><span data-stu-id="a356f-301">Refiner Element in Microsoft.Search.Query Schema</span></span>](http://msdn.microsoft.com/library/0512c17a-18e9-45e3-9061-9dba9cd45ef4%28Office.15%29.aspx)
