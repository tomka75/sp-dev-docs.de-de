
# <a name="synchronize-sharepoint-items-using-the-rest-service"></a><span data-ttu-id="2a1ab-101">Synchronisieren von SharePoint-Elementen mithilfe des REST-Diensts</span><span class="sxs-lookup"><span data-stu-id="2a1ab-101">Synchronize SharePoint items using the REST service</span></span>
<span data-ttu-id="2a1ab-102">Erfahren Sie, wie Sie mit der Ressource **GetListItemChangesSinceToken**, die Teil des SharePoint REST-Diensts ist, Elemente zwischen SharePoint und Ihren Add-Ins oder Diensten synchronisieren.</span><span class="sxs-lookup"><span data-stu-id="2a1ab-102">Learn how to synchronize items between SharePoint and your add-ins or services by using the  **GetListItemChangesSinceToken** resource, part of the SharePoint REST service.</span></span>
 

 <span data-ttu-id="2a1ab-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="2a1ab-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="synchronizing-sharepoint-items-using-the-getlistitemchangessincetoken-resource"></a><span data-ttu-id="2a1ab-106">Synchronisieren von SharePoint-Elementen mithilfe der Ressource GetListItemChangesSinceToken</span><span class="sxs-lookup"><span data-stu-id="2a1ab-106">Synchronizing SharePoint items using the GetListItemChangesSinceToken resource</span></span>

<span data-ttu-id="2a1ab-p102">Zum Synchronisieren von Elementen zwischen SharePoint und Ihren Add-ins oder Diensten können Sie die Ressource **GetListItemChangesSinceToken** verwenden. **GetListItemChangesSinceToken** ist Teil des SharePoint REST-Diensts und entspricht dem Webdienstaufruf **Lists.GetListItemChangesSinceToken**.</span><span class="sxs-lookup"><span data-stu-id="2a1ab-p102">If you want to synchronize items between SharePoint and your add-ins or services, you can use the  **GetListItemChangesSinceToken** resource to do so. The **GetListItemChangesSinceToken**, part of the SharePoint REST service, corresponds to the  **Lists.GetListItemChangesSinceToken** web service call.</span></span>
 

 
<span data-ttu-id="2a1ab-109">Führen Sie eine **POST**-Anforderung aus, die ein Objekt [SP.ChangeLogItemQuery object properties](#bk_props) im Hauptteil enthält.</span><span class="sxs-lookup"><span data-stu-id="2a1ab-109">Perform a  **POST** request that includes a [SP.ChangeLogItemQuery object properties](#bk_props) object in the request body.</span></span>
 

 
<span data-ttu-id="2a1ab-p103">Die Anforderung gibt ADO **rowset** XML mit den Zeilen zurück, die alle mit der Abfrage übereinstimmenden Änderungen an Listenelementen enthalten. Weitere Informationen zu diesen Eigenschaften, einschließlich Eigenschaftendatenstrukturen, CAML-Elementbeschreibungen und Rückgabewerten finden Sie unter **Lists.GetListItemChangesSinceToken**.</span><span class="sxs-lookup"><span data-stu-id="2a1ab-p103">The request returns ADO  **rowset** XML which includes rows corresponding to any list item change matching the specified query. For more information on these properties, including property data structures, CAML element descriptions, and return values, see **Lists.GetListItemChangesSinceToken**.</span></span>
 

 

||
|:-----|
|<span data-ttu-id="2a1ab-112">**Beispielanforderung**</span><span class="sxs-lookup"><span data-stu-id="2a1ab-112">**Example request**</span></span>|
| `POST http://server/site/_api/web/Lists/GetByTitle('Announcements')/GetListItemChangesSinceToken`|
|<span data-ttu-id="2a1ab-113">**Beispiel für POST-Text**</span><span class="sxs-lookup"><span data-stu-id="2a1ab-113">**Example POST Body**</span></span>|
|
```XML
{ 'd' : { 
  'query': { 
    '__metadata': { 'type': 'SP.ChangeLogItemQuery'}, 
    'ViewName': '', 
    'Query': '<Where>
      <Contains>
         <FieldRef Name="Title" />
         <Value Type='Text'>Te</Value>
      </Contains></Where>',
    'QueryOptions': '<QueryOptions>
      <IncludeMandatoryColumns>FALSE</IncludeMandatoryColumns>
      <DateInUtc>False</DateInUtc>
      <IncludePermissions>TRUE</IncludePermissions>
      <IncludeAttachmentUrls>FALSE</IncludeAttachmentUrls>
      <Folder>Shared Documents/Test1</Folder></QueryOptions>', 
    'ChangeToken':'1;3;eee4c6d5-f88a-42c4-8ce1-685122984870;634397182229400000;3710', 
    'Contains':'<Contains>
      <FieldRef Name="Title"/>
      <Value Type="Text">Testing</Value></Contains>' } 
  } 
}

```

|

## <a name="spchangelogitemquery-object-properties"></a><span data-ttu-id="2a1ab-114">Objekteigenschaften SP.ChangeLogItemQuery</span><span class="sxs-lookup"><span data-stu-id="2a1ab-114">SP.ChangeLogItemQuery object properties</span></span>
<span data-ttu-id="2a1ab-115"><a name="bk_props"> </a></span><span class="sxs-lookup"><span data-stu-id="2a1ab-115"></span></span>


****


|<span data-ttu-id="2a1ab-116">**Property**</span><span class="sxs-lookup"><span data-stu-id="2a1ab-116">**Property**</span></span>|<span data-ttu-id="2a1ab-117">**Description**</span><span class="sxs-lookup"><span data-stu-id="2a1ab-117">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="2a1ab-118">**ListName**</span><span class="sxs-lookup"><span data-stu-id="2a1ab-118">**ListName**</span></span>|<span data-ttu-id="2a1ab-p104">Eine Zeichenfolge, die entweder Titel oder GUID der Liste enthält. Bei Abruf der Tabelle "UserInfo" enthält die Zeichenfolge UserInfo. Die Verwendung der GUID führt zu einer besseren Leistung.</span><span class="sxs-lookup"><span data-stu-id="2a1ab-p104">A string that contains either the title or the GUID for the list. When querying the UserInfo table, the string contains UserInfo. Using the GUID results in better performance.</span></span>|
|<span data-ttu-id="2a1ab-122">**ViewName**</span><span class="sxs-lookup"><span data-stu-id="2a1ab-122">**ViewName**</span></span>|<span data-ttu-id="2a1ab-p105">Eine Zeichenfolge mit der GUID für die Ansicht, die für die durch die Parameter _query_,  _viewFields_ und  _rowLimit_ dargestellten Standard-Ansichtattribute zu verwenden ist. Wird dieses Argument nicht angegeben, so wird die Standardansicht verwendet. Wird das Argument angegeben, so setzt der Wert der Parameter _query_,  _viewFields_ oder  _rowLimit_ die entsprechende Einstellung in der Ansicht außer Kraft. Weist z. B. die durch den Parameter _viewFields_ angegebene Ansicht ein Zeilenlimit von 100 auf, während der Parameter _rowLimit_ den Wert 1000 enthält, dann werden in der Antwort 1000 Zeilen zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="2a1ab-p105">A string that contains the GUID for the view, which determines the view to use for the default view attributes represented by the  _query_,  _viewFields_, and  _rowLimit_ parameters. If this argument is not supplied, the default view is assumed. If it is supplied, the value of the _query_,  _viewFields_, or  _rowLimit_ parameter overrides the equivalent setting within the view. For example, if the view specified by the _viewFields_ parameter has a row limit of 100 rows but the _rowLimit_ parameter contains a value of 1000, then 1,000 rows are returned in the response.</span></span>|
|<span data-ttu-id="2a1ab-127">**Query**</span><span class="sxs-lookup"><span data-stu-id="2a1ab-127">**Query**</span></span>|<span data-ttu-id="2a1ab-128">Ein [Query](http://msdn.microsoft.com/en-us/library/ms471093.aspx)-Element mit der Abfrage, die festlegt, welche Datensätze in welcher Reihenfolge zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="2a1ab-128">A  [Query](http://msdn.microsoft.com/en-us/library/ms471093.aspx) element containing the query that determines which records are returned and in what order.</span></span>|
|<span data-ttu-id="2a1ab-129">**QueryOptions**</span><span class="sxs-lookup"><span data-stu-id="2a1ab-129">**QueryOptions**</span></span>|<span data-ttu-id="2a1ab-130">Ein XML-Fragment in der folgenden Form, das separate Knoten für die verschiedenen Eigenschaften des Objekts **SPQuery** enthält.</span><span class="sxs-lookup"><span data-stu-id="2a1ab-130">An XML fragment in the following form that contains separate nodes for the various properties of the  **SPQuery** object.</span></span>|
|<span data-ttu-id="2a1ab-131">**ChangeToken**</span><span class="sxs-lookup"><span data-stu-id="2a1ab-131">**ChangeToken**</span></span>|<span data-ttu-id="2a1ab-p106">Eine Zeichenfolge, die das Änderungstoken für die Anforderung enthält. Eine Beschreibung des Formats, das in dieser Zeichenfolge verwendet wird, finden Sie unter [Übersicht über das Änderungsprotokoll](http://msdn.microsoft.com/en-us/library/bb417456.aspx). Wenn Null übergeben wird, werden alle Elemente in der Liste zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="2a1ab-p106">A string that contains the change token for the request. For a description of the format that is used in this string, see  [Overview of the Change Log](http://msdn.microsoft.com/en-us/library/bb417456.aspx). If null is passed, all items in the list are returned.</span></span>|
|<span data-ttu-id="2a1ab-135">**Contains**</span><span class="sxs-lookup"><span data-stu-id="2a1ab-135">**Contains**</span></span>|<span data-ttu-id="2a1ab-136">Ein [Contains](http://msdn.microsoft.com/en-us/library/ms196501.aspx)-Element, das das benutzerdefinierte Filtern für die Abfrage definiert.</span><span class="sxs-lookup"><span data-stu-id="2a1ab-136">A  [Contains](http://msdn.microsoft.com/en-us/library/ms196501.aspx) element that defines custom filtering for the query.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="2a1ab-137">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="2a1ab-137">Additional resources</span></span>
<span data-ttu-id="2a1ab-138"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2a1ab-138"></span></span>


-  [<span data-ttu-id="2a1ab-139">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="2a1ab-139">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-2013-rest-service)
    
 
-  [<span data-ttu-id="2a1ab-140">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="2a1ab-140">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-2013-rest-endpoints)
    
 
-  [<span data-ttu-id="2a1ab-141">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="2a1ab-141">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest)
    
 
-  [<span data-ttu-id="2a1ab-142">Arbeiten mit Ordnern und Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="2a1ab-142">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest)
    
 
-  [<span data-ttu-id="2a1ab-143">Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur</span><span class="sxs-lookup"><span data-stu-id="2a1ab-143">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service)
    
 
-  [<span data-ttu-id="2a1ab-144">Ermitteln von URIs von SharePoint REST-Dienstendpunkten</span><span class="sxs-lookup"><span data-stu-id="2a1ab-144">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris)
    
 
-  [<span data-ttu-id="2a1ab-145">Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="2a1ab-145">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests)
    
 
-  [<span data-ttu-id="2a1ab-146">REST-API-Referenz und Beispiele</span><span class="sxs-lookup"><span data-stu-id="2a1ab-146">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="2a1ab-147">Verwenden von ETag-Werten zum Bestimmen der Version von Dokument- und Listenelementen über den REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="2a1ab-147">Use ETag values through the REST service to get document list item versioning</span></span>](http://msdn.microsoft.com/library/5f7e0579-46b7-44ab-b3b4-cdbc622dcd98%28Office.15%29.aspx)
    
 

 

 

