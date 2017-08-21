
# <a name="use-odata-query-operations-in-sharepoint-rest-requests"></a><span data-ttu-id="9d0be-101">Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="9d0be-101">Use OData query operations in SharePoint REST requests</span></span>
<span data-ttu-id="9d0be-102">Hier erfahren Sie, wie Sie eine Reihe von OData-Abfragezeichenfolgeoperatoren verwenden, um die vom SharePoint REST-Dienst angeforderten Daten auszuwählen, zu filtern und zu ordnen.</span><span class="sxs-lookup"><span data-stu-id="9d0be-102">Learn how to use a wide range of OData query string operators to select, filter, and order the data you request from the SharePoint REST service.</span></span> 
 

 <span data-ttu-id="9d0be-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="9d0be-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

 <span data-ttu-id="9d0be-106">**Bevor Sie beginnen**</span><span class="sxs-lookup"><span data-stu-id="9d0be-106">**Before you start**</span></span>
 

-  [<span data-ttu-id="9d0be-107">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="9d0be-107">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-2013-rest-service)
    
 
-  [<span data-ttu-id="9d0be-108">Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur</span><span class="sxs-lookup"><span data-stu-id="9d0be-108">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service)
    
 
-  [<span data-ttu-id="9d0be-109">Ermitteln von URIs von SharePoint REST-Dienstendpunkten</span><span class="sxs-lookup"><span data-stu-id="9d0be-109">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris)
    
 
<span data-ttu-id="9d0be-110">Der SharePoint REST-Dienst unterstütz eine Reihe von OData-Abfragezeichenfolgeoperatoren, mit denen SIe die angeforderten Daten auswählen, filtern und ordnen können.</span><span class="sxs-lookup"><span data-stu-id="9d0be-110">The SharePoint REST service supports a wide range of OData query string operators that enable you to select, filter, and order the data you request.</span></span>
 

 <span data-ttu-id="9d0be-p102">**Tipp**  Der SharePoint Online-REST-Dienst (und der Dienst von SharePoint 2016 (lokal) und höher) unterstützt die Kombination mehrerer Anforderungen in einem einzelnen Dienstaufruf mithilfe der OData-Abfrageoption `$batch`. Einzelheiten und Links zu Codebeispielen finden Sie unter [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis) (Erstellen von Batchanforderungen mit den REST-APIs).</span><span class="sxs-lookup"><span data-stu-id="9d0be-p102">**Tip**  The SharePoint Online (and on-premise SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData  `$batch` query option. For details and links to code samples, see [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis).</span></span>
 


## <a name="select-fields-to-return"></a><span data-ttu-id="9d0be-113">Auswählen der Felder, die zurückgegeben werden sollen</span><span class="sxs-lookup"><span data-stu-id="9d0be-113">Select fields to return</span></span>

<span data-ttu-id="9d0be-p103">Verwenden Sie die Abfrageoption [$select](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#SelectSystemQueryOption), um anzugeben, welche Felder für eine bestimmte Liste, ein Listenelement oder ein anderes, durch eine Entitätenmenge dargestelltes SharePoint-Objekt zurückgegeben werden sollen. Sie können `$select=*` verwenden, um alle verfügbaren Felder zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="9d0be-p103">Use the  [$select](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#SelectSystemQueryOption) query option to specify which fields to return for a given list, list item, or other SharePoint object represented by an entity set. You can use `$select=*` to return all available fields.</span></span>
 

 

 <span data-ttu-id="9d0be-p104">**Hinweis**  Im Allgemeinen gibt der REST-Dienst standardmäßig alle verfügbaren Felder zurück, wenn Sie die Abfrageoption `$select` nicht angeben. Es kann jedoch manchmal vorkommen, dass einige SharePoint-Objekte Eigenschaften enthalten, deren Abruf äußerst ressourcenintensiv ist. Um die Leistung des REST-Dienstes zu optimieren, sind diese Eigenschaften in der Standardabfrage nicht enthalten und müssen explizit angefordert werden. Beispielsweise wird die Eigenschaft **SPWeb.EffectiveBasePermissions** nicht standardmäßig zurückgegeben und muss explizit mittels der Abfrageoption `$select` angefordert werden.</span><span class="sxs-lookup"><span data-stu-id="9d0be-p104">**Note**  In general, if you do not specify the  `$select` query option, the REST service returns all available fields by default. However, in a few cases, some SharePoint objects include properties that are very resource intensive to retrieve; to optimize REST service performance, these properties are not included in the default query, and must be explicitly requested.For example, the  **SPWeb.EffectiveBasePermissions** property is not returned by default, and must be explicitly requested using the `$select` query option.</span></span>
 

<span data-ttu-id="9d0be-p105">Darüber hinaus können Sie angeben, dass die Anforderung projizierte Felder aus anderen Listen und die Werte von Suchvorgängen zurückgeben soll. Geben Sie hierzu in den beiden Abfrageoptionen `$select` und `$expand` den Feldnamen an. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="9d0be-p105">In addition, you can specify that the request returns projected fields from other lists and the values of lookups. To do this, specify the field name in both the  `$select` and `$expand` query options. For example:</span></span>
 

 
 `http://server/site/_api/web/lists('guid')/items?$select=Title,Products/Name&amp;$expand=Products/Name`
 

 
<span data-ttu-id="9d0be-121">Massenerweiterung und die Auswahl damit zusammenhängender Elemente wird nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="9d0be-121">Bulk expansion and selection of related items is not supported.</span></span>
 

 

## <a name="select-items-to-return"></a><span data-ttu-id="9d0be-122">Auswählen der Elemente, die zurückgegeben werden sollen</span><span class="sxs-lookup"><span data-stu-id="9d0be-122">Select items to return</span></span>

<span data-ttu-id="9d0be-p106">Verwenden Sie die Abfrageoption [$filter](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#FilterSystemQueryOption), um auszuwählen, welche Elemente zurückgegeben werden sollen. Unter [OData query operators supported in the SharePoint REST service](#bk_supported) (Im SharePoint REST-Dienst unterstützte OData-Abfrageoperatoren) sind die Optionen und Funktionen zum Vergleich der Filterabfragen aufgeführt, die Sie im SharePoint REST-Dienst verwenden können.</span><span class="sxs-lookup"><span data-stu-id="9d0be-p106">Use the  [$filter](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#FilterSystemQueryOption) query option to select which items to return. [OData query operators supported in the SharePoint REST service](#bk_supported) lists the filter query comparison options and functions you can use with the SharePoint REST service.</span></span>
 

 

## <a name="query-for-single-value-lookup-fields"></a><span data-ttu-id="9d0be-125">Abfrage für Einzelwert-Suchfelder</span><span class="sxs-lookup"><span data-stu-id="9d0be-125">Query for single value lookup fields</span></span>

<span data-ttu-id="9d0be-p107">Einzelwert-Suchfelder werden beim SharePoint REST-Dienst als zwei separate Felder dargestellt: ein Feld für den tatsächlichen Feldwert und ein weiteres für den Feldnamen. Sie können Abfragen des Suchfeldwerts durchführen wie bei jedem anderen Feld dieses Datentyps. Wenn beispielsweise der Wert des Suchfelds eine Zeichenfolge ist, können Sie die Vergleichsoptionen für Zeichenfolgen in Ihrer Abfrage verwenden.</span><span class="sxs-lookup"><span data-stu-id="9d0be-p107">Single value lookup fields are represented by two separate fields in the SharePoint REST service: one field representing the actual field value, and another representing the field name. You can perform queries against the lookup field value as you would any other field of that data type. For example, if the lookup field value is a string, you can use string comparison options in your query.</span></span>
 

 

## <a name="query-for-users"></a><span data-ttu-id="9d0be-129">Abfrage von Benutzern</span><span class="sxs-lookup"><span data-stu-id="9d0be-129">Query for users</span></span>

<span data-ttu-id="9d0be-p108">Beim SharePoint REST-Dienst werden die Benutzer durch ihren Anzeigennamen repräsentiert und nicht ihrem Alias oder ihrer Domäne\Alias-Kombination. Daher müssen Sie sich bei Benutzerabfragen nach den Anzeigenamen richten.</span><span class="sxs-lookup"><span data-stu-id="9d0be-p108">In the SharePoint REST service, users are represented by the user's friendly (display) name, and not their alias or domain\alias combination. Therefore, you must construct user queries against users' friendly names.</span></span>
 

 

 <span data-ttu-id="9d0be-132">**Hinweis**  Auf Mitgliedschaft basierende Benutzeranfragen werden nicht unterstützt. Der Operator **Current** zum Ausführen von Abfragen mithilfe der ID des aktuellen Benutzers wird nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="9d0be-132">**Note**  Membership-based user queries are not supported.Usage of the  **Current** operator to do queries using the ID of the current user is not supported.</span></span>
 


## <a name="query-for-multi-value-lookup-fields-and-users"></a><span data-ttu-id="9d0be-133">Abfrage für Suchfelder und Benutzer mit mehreren Werten</span><span class="sxs-lookup"><span data-stu-id="9d0be-133">Query for multi-value lookup fields and users</span></span>

<span data-ttu-id="9d0be-134">Da Suchfelder mit mehreren Werten als eine Zeichenfolge mehrerer Werte zurückgegeben werden, ist es nicht möglich, sie abzufragen (z. B. wird das Äquivalent eines **Includes**-Elements oder **NotIncludes**-Elements nicht unterstützt).</span><span class="sxs-lookup"><span data-stu-id="9d0be-134">Because multi-value lookup fields are returned as a string of multiple values, there is no way to query for them (for example, the equivalent of an  **Includes** element or **NotIncludes** element is not supported).</span></span>
 

 

## <a name="sort-returned-items"></a><span data-ttu-id="9d0be-135">Sortieren der zurückgegebenen Elemente</span><span class="sxs-lookup"><span data-stu-id="9d0be-135">Sort returned items</span></span>

<span data-ttu-id="9d0be-p109">Verwenden Sie die Abfrageoption [$orderby](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#OrderBySystemQueryOption), um anzugeben, wie die Elemente bei der Rückgabe geordnet sein sollen. Geben Sie zum Sortieren nach mehreren Feldern eine durch Komma getrennte Liste der Felder an. Sie können auch angeben, ob die Elemente in aufsteigender oder absteigender Reihenfolge sortiert werden sollen. Fügen Sie Ihrer Abfrage dazu das Schlüsselwort **asc** oder **desc** an.</span><span class="sxs-lookup"><span data-stu-id="9d0be-p109">Use the  [$orderby](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#OrderBySystemQueryOption) query option to specify how to sort the items in your query return set. To sort by multiple fields, specify a comma-separated list of fields. You can also specify whether to sort the items in ascending or descending order by appending the **asc** or **desc** keyword to your query.</span></span>
 

 

## <a name="page-through-returned-items"></a><span data-ttu-id="9d0be-139">Unterteilen der zurückgegebenen Elemente</span><span class="sxs-lookup"><span data-stu-id="9d0be-139">Page through returned items</span></span>

<span data-ttu-id="9d0be-140">Verwenden Sie die Abfrageoptionen  [$top](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#TopSystemQueryOption) und [$skiptoken](http://msdn.microsoft.com/library/dd942121.aspx), um eine Teilmenge von Elementen auszuwählen, die nicht von der Abfrage zurückgegeben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="9d0be-140">Use the  [$top](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#TopSystemQueryOption) and [$skiptoken](http://msdn.microsoft.com/library/dd942121.aspx) query options to select a subset of the items that would otherwise be returned by your query.</span></span>
 

 

 <span data-ttu-id="9d0be-141">**Hinweis** Die Abfrageoption „$skip“ funktioniert nicht bei Abfragen für SharePoint-Listenelemente.</span><span class="sxs-lookup"><span data-stu-id="9d0be-141">**Note**  The $skip query option does not work with queries for SharePoint list items.</span></span>
 

<span data-ttu-id="9d0be-p110">Die Option  `$top` ermöglicht Ihnen, die ersten *n*  Elemente des Rückgabesatzes für die Rückgabe auszuwählen. Die folgende URI fordert beispielsweise an, dass nur die ersten zehn Elemente des potenziellen Rückgabesatzes tatsächlich zurückgegeben werden:</span><span class="sxs-lookup"><span data-stu-id="9d0be-p110">The  `$top` option enables you to select the first *n*  items of the return set for return. For example, the following URI requests that only the first ten items in the prospective return set actually be returned:</span></span>
 

 
 `http://server/site/_api/web/lists('<guid>')/items$top=10`
 

 
<span data-ttu-id="9d0be-144">Mit der Option „$skiptoken“ können Sie Elemente bis zum angegebenen Element überspringen und den Rest zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="9d0be-144">The $skiptoken option enables you to skip over items until the specified item is reached and return the rest.</span></span>
 

 
 `$skiptoken=Paged=TRUE&amp;p_ID=5`
 

 

 <span data-ttu-id="9d0be-p111">**Hinweis**  Berücksichtigen Sie bei diesen Abfrageoptionen, dass die Seitenverwaltung in OData Ordnungszahlen verwendet. Nehmen wir beispielsweise an, dass Sie eine Schaltfläche „nächste Seite“ für die Anzeige von SharePoint-Listenelementen implementieren. Mithilfe des REST-Diensts aktivieren Sie die Schaltfläche für die Rückgabe der Elemente 1 bis 20, dann 21 bis 40 usw., wenn darauf geklickt wird. Nehmen Sie jedoch an, dass ein anderer Benutzer die Elemente 4 und 18 zwischen den Klicks auf die Schaltfläche löscht. In diesem Fall wird die Positionierung der verbleibenden Elemente zurückgesetzt und beim Anzeigen der Elemente 21 bis 40 werden zwei Elemente übersprungen.</span><span class="sxs-lookup"><span data-stu-id="9d0be-p111">**Note**  When using these query options, take into account that paging in OData is ordinal. For example, suppose you are implementing a next page button to display SharePoint list items. You use the REST service to enable the button to return items 1 through 20 when clicked, then items 21 through 40, and so on. However, suppose another user deletes items 4 and 18 between clicks of the next button. In such a case, the ordinal positioning of the remaining items is reset, and displaying items 21 through 40 actually skips over two items.</span></span>
 


## <a name="odata-query-operators-supported-in-the-sharepoint-rest-service"></a><span data-ttu-id="9d0be-150">Vom SharePoint REST-Dienst unterstützte OData-Abfrageoperatoren</span><span class="sxs-lookup"><span data-stu-id="9d0be-150">OData query operators supported in the SharePoint REST service</span></span>
<span data-ttu-id="9d0be-151"><a name="bk_supported"> </a></span><span class="sxs-lookup"><span data-stu-id="9d0be-151"></span></span>



|<span data-ttu-id="9d0be-152">**Unterstützt**</span><span class="sxs-lookup"><span data-stu-id="9d0be-152">**Supported**</span></span>|<span data-ttu-id="9d0be-153">**Nicht unterstützt**</span><span class="sxs-lookup"><span data-stu-id="9d0be-153">**Not supported**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9d0be-154">**Numerische Vergleiche** Lt Le Gt Ge Eq Ne</span><span class="sxs-lookup"><span data-stu-id="9d0be-154">**Numeric comparisons** Lt Le Gt Ge Eq Ne</span></span>| <span data-ttu-id="9d0be-155">Arithmetische Operatoren (Add, Sub, Mul, Div, Mod) Grundlegende mathematische Funktionen (round, floor, ceiling)</span><span class="sxs-lookup"><span data-stu-id="9d0be-155">Arithmetic operators  (Add, Sub, Mul, Div, Mod) Basic math functions (round, floor, ceiling)</span></span> |
|<span data-ttu-id="9d0be-156">**String-Vergleiche** startsWith substringof Eq Ne</span><span class="sxs-lookup"><span data-stu-id="9d0be-156">**String comparisons** startsWith substringof Eq Ne</span></span>| <span data-ttu-id="9d0be-157">endsWith replace substring tolower toupper trim concat</span><span class="sxs-lookup"><span data-stu-id="9d0be-157">endsWith replace substring tolower toupper trim concat</span></span>|
|<span data-ttu-id="9d0be-158">**Datums- und Uhrzeitfunktionen** day() month() year() hour() minute() second()</span><span class="sxs-lookup"><span data-stu-id="9d0be-158">**Date and time functions** day() month() year() hour() minute() second()</span></span>| <span data-ttu-id="9d0be-159">Operator „DateTimeRangesOverlap“: Abfrage, ob Datum-Zeit in ein wiederkehrendes Datum-Zeit-Muster fällt</span><span class="sxs-lookup"><span data-stu-id="9d0be-159">DateTimeRangesOverlap operator Querying as to whether a date time falls inside a recurrent date time pattern</span></span>|
<span data-ttu-id="9d0be-160">Die untenstehende Abbildung zeigt unterstützte OData-Abfrageoptionen.</span><span class="sxs-lookup"><span data-stu-id="9d0be-160">The figure below shows the supported OData query options.</span></span>
 

 

<span data-ttu-id="9d0be-161">**Unterstützte OData-Abfrageoptionen**</span><span class="sxs-lookup"><span data-stu-id="9d0be-161">**Supported OData query options**</span></span>

 

 
![Abfrageoptionssyntax des SharePoint REST-Diensts](../../images/SPF15Con_REST_queryOptionSyntax.png)
 

 

 

## <a name="additional-resources"></a><span data-ttu-id="9d0be-163">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="9d0be-163">Additional resources</span></span>
<span data-ttu-id="9d0be-164"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9d0be-164"></span></span>


-  [<span data-ttu-id="9d0be-165">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="9d0be-165">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-2013-rest-service)
    
 
-  [<span data-ttu-id="9d0be-166">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="9d0be-166">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-2013-rest-endpoints)
    
 
-  [<span data-ttu-id="9d0be-167">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="9d0be-167">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest)
    
 
-  [<span data-ttu-id="9d0be-168">Arbeiten mit Ordnern und Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="9d0be-168">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest)
    
 
-  [<span data-ttu-id="9d0be-169">Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur</span><span class="sxs-lookup"><span data-stu-id="9d0be-169">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service)
    
 
-  [<span data-ttu-id="9d0be-170">Ermitteln von URIs von SharePoint REST-Dienstendpunkten</span><span class="sxs-lookup"><span data-stu-id="9d0be-170">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris)
    
 
-  [<span data-ttu-id="9d0be-171">REST-API-Referenz und Beispiele</span><span class="sxs-lookup"><span data-stu-id="9d0be-171">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)
    
 

 

 
