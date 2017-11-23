---
title: Synchronisieren von SharePoint-Elementen mit dem REST-Dienst
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: ed16442556103b74c820b0d67ea4bbcc0667f7ea
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="synchronize-sharepoint-items-using-the-rest-service"></a><span data-ttu-id="4bfe3-102">Synchronisieren von SharePoint-Elementen mit dem REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="4bfe3-102">Synchronize SharePoint items using the REST service</span></span>
<span data-ttu-id="4bfe3-103">Erfahren Sie, wie Sie mit der Ressource **GetListItemChangesSinceToken**, die Teil des SharePoint REST-Diensts ist, Elemente zwischen SharePoint und Ihren Add-ins oder Diensten synchronisieren.</span><span class="sxs-lookup"><span data-stu-id="4bfe3-103">Learn how to synchronize items between SharePoint and your add-ins or services by using the  **GetListItemChangesSinceToken** resource, part of the SharePoint REST service.</span></span>

## <a name="synchronizing-sharepoint-items-using-the-getlistitemchangessincetoken-resource"></a><span data-ttu-id="4bfe3-104">Synchronisieren von SharePoint-Elementen mithilfe der Ressource GetListItemChangesSinceToken</span><span class="sxs-lookup"><span data-stu-id="4bfe3-104">Synchronizing SharePoint items using the GetListItemChangesSinceToken resource</span></span>
<span data-ttu-id="4bfe3-p101">Zum Synchronisieren von Elementen zwischen SharePoint und Ihren Add-ins oder Diensten können Sie die Ressource **GetListItemChangesSinceToken** verwenden. **GetListItemChangesSinceToken** ist Teil des SharePoint REST-Diensts und entspricht dem Webdienstaufruf **Lists.GetListItemChangesSinceToken**.</span><span class="sxs-lookup"><span data-stu-id="4bfe3-p101">If you want to synchronize items between SharePoint and your add-ins or services, you can use the  **GetListItemChangesSinceToken** resource to do so. The **GetListItemChangesSinceToken**, part of the SharePoint REST service, corresponds to the  **Lists.GetListItemChangesSinceToken** web service call.</span></span>
 
<span data-ttu-id="4bfe3-107">Führen Sie eine **POST**-Anforderung aus, die ein Objekt [SP.ChangeLogItemQuery object properties](#bk_props) im Hauptteil enthält.</span><span class="sxs-lookup"><span data-stu-id="4bfe3-107">Perform a  **POST** request that includes a [SP.ChangeLogItemQuery object properties](#bk_props) object in the request body.</span></span>
 
<span data-ttu-id="4bfe3-p102">Die Anforderung gibt ADO **rowset** XML mit den Zeilen zurück, die alle mit der Abfrage übereinstimmenden Änderungen an Listenelementen enthalten. Weitere Informationen zu diesen Eigenschaften, einschließlich Eigenschaftendatenstrukturen, CAML-Elementbeschreibungen und Rückgabewerten finden Sie unter **Lists.GetListItemChangesSinceToken**.</span><span class="sxs-lookup"><span data-stu-id="4bfe3-p102">The request returns ADO  **rowset** XML which includes rows corresponding to any list item change matching the specified query. For more information on these properties, including property data structures, CAML element descriptions, and return values, see **Lists.GetListItemChangesSinceToken**.</span></span>
 
||
|:-----|
|<span data-ttu-id="4bfe3-110">**Beispielanforderung**</span><span class="sxs-lookup"><span data-stu-id="4bfe3-110">**Example request**</span></span>|
| `POST http://server/site/_api/web/Lists/GetByTitle('Announcements')/GetListItemChangesSinceToken`|
|<span data-ttu-id="4bfe3-111">**Beispiel für POST-Text**</span><span class="sxs-lookup"><span data-stu-id="4bfe3-111">**Example POST Body**</span></span>|
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

## <a name="spchangelogitemquery-object-properties"></a><span data-ttu-id="4bfe3-112">Objekteigenschaften SP.ChangeLogItemQuery</span><span class="sxs-lookup"><span data-stu-id="4bfe3-112">SP.ChangeLogItemQuery object properties</span></span>
<span data-ttu-id="4bfe3-113"><a name="bk_props"> </a></span><span class="sxs-lookup"><span data-stu-id="4bfe3-113"></span></span>
****

|<span data-ttu-id="4bfe3-114">**Property**</span><span class="sxs-lookup"><span data-stu-id="4bfe3-114">**Property**</span></span>|<span data-ttu-id="4bfe3-115">**Description**</span><span class="sxs-lookup"><span data-stu-id="4bfe3-115">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="4bfe3-116">**ListName**</span><span class="sxs-lookup"><span data-stu-id="4bfe3-116">**ListName**</span></span>|<span data-ttu-id="4bfe3-p103">Eine Zeichenfolge, die entweder Titel oder GUID der Liste enthält. Bei Abruf der Tabelle "UserInfo" enthält die Zeichenfolge UserInfo. Die Verwendung der GUID führt zu einer besseren Leistung.</span><span class="sxs-lookup"><span data-stu-id="4bfe3-p103">A string that contains either the title or the GUID for the list. When querying the UserInfo table, the string contains UserInfo. Using the GUID results in better performance.</span></span>|
|<span data-ttu-id="4bfe3-120">**ViewName**</span><span class="sxs-lookup"><span data-stu-id="4bfe3-120">**ViewName**</span></span>|<span data-ttu-id="4bfe3-p104">Eine Zeichenfolge mit der GUID für die Ansicht, die für die durch die Parameter _query_,  _viewFields_ und  _rowLimit_ dargestellten Standard-Ansichtattribute zu verwenden ist. Wird dieses Argument nicht angegeben, so wird die Standardansicht verwendet. Wird das Argument angegeben, so setzt der Wert der Parameter _query_,  _viewFields_ oder  _rowLimit_ die entsprechende Einstellung in der Ansicht außer Kraft. Weist z. B. die durch den Parameter _viewFields_ angegebene Ansicht ein Zeilenlimit von 100 auf, während der Parameter _rowLimit_ den Wert 1000 enthält, dann werden in der Antwort 1000 Zeilen zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="4bfe3-p104">A string that contains the GUID for the view, which determines the view to use for the default view attributes represented by the  _query_,  _viewFields_, and  _rowLimit_ parameters. If this argument is not supplied, the default view is assumed. If it is supplied, the value of the _query_,  _viewFields_, or  _rowLimit_ parameter overrides the equivalent setting within the view. For example, if the view specified by the _viewFields_ parameter has a row limit of 100 rows but the _rowLimit_ parameter contains a value of 1000, then 1,000 rows are returned in the response.</span></span>|
|<span data-ttu-id="4bfe3-125">**Query**</span><span class="sxs-lookup"><span data-stu-id="4bfe3-125">**Query**</span></span>|<span data-ttu-id="4bfe3-126">Ein [Query](http://msdn.microsoft.com/de-de/library/ms471093.aspx)-Element mit der Abfrage, die festlegt, welche Datensätze in welcher Reihenfolge zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="4bfe3-126">A  [Query](http://msdn.microsoft.com/de-de/library/ms471093.aspx) element containing the query that determines which records are returned and in what order.</span></span>|
|<span data-ttu-id="4bfe3-127">**QueryOptions**</span><span class="sxs-lookup"><span data-stu-id="4bfe3-127">**QueryOptions**</span></span>|<span data-ttu-id="4bfe3-128">Ein XML-Fragment in der folgenden Form, das separate Knoten für die verschiedenen Eigenschaften des Objekts **SPQuery** enthält.</span><span class="sxs-lookup"><span data-stu-id="4bfe3-128">An XML fragment in the following form that contains separate nodes for the various properties of the  **SPQuery** object.</span></span>|
|<span data-ttu-id="4bfe3-129">**ChangeToken**</span><span class="sxs-lookup"><span data-stu-id="4bfe3-129">**ChangeToken**</span></span>|<span data-ttu-id="4bfe3-p105">Eine Zeichenfolge, die das Änderungstoken für die Anforderung enthält. Eine Beschreibung des Formats, das in dieser Zeichenfolge verwendet wird, finden Sie unter [Übersicht über das Änderungsprotokoll](http://msdn.microsoft.com/de-de/library/bb417456.aspx). Wenn Null übergeben wird, werden alle Elemente in der Liste zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="4bfe3-p105">A string that contains the change token for the request. For a description of the format that is used in this string, see  [Overview of the Change Log](http://msdn.microsoft.com/de-de/library/bb417456.aspx). If null is passed, all items in the list are returned.</span></span>|
|<span data-ttu-id="4bfe3-133">**Contains**</span><span class="sxs-lookup"><span data-stu-id="4bfe3-133">**Contains**</span></span>|<span data-ttu-id="4bfe3-134">Ein [Contains](http://msdn.microsoft.com/de-de/library/ms196501.aspx)-Element, das das benutzerdefinierte Filtern für die Abfrage definiert.</span><span class="sxs-lookup"><span data-stu-id="4bfe3-134">A  [Contains](http://msdn.microsoft.com/de-de/library/ms196501.aspx) element that defines custom filtering for the query.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="4bfe3-135">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="4bfe3-135">Additional resources</span></span>
<span data-ttu-id="4bfe3-136"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="4bfe3-136"></span></span>

-  [<span data-ttu-id="4bfe3-137">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="4bfe3-137">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
-  [<span data-ttu-id="4bfe3-138">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="4bfe3-138">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [<span data-ttu-id="4bfe3-139">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="4bfe3-139">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
-  [<span data-ttu-id="4bfe3-140">Arbeiten mit Ordnern und Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="4bfe3-140">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest.md)
-  [<span data-ttu-id="4bfe3-141">Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur</span><span class="sxs-lookup"><span data-stu-id="4bfe3-141">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service.md)
-  [<span data-ttu-id="4bfe3-142">Ermitteln von URIs von SharePoint REST-Dienstendpunkten</span><span class="sxs-lookup"><span data-stu-id="4bfe3-142">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris.md)
-  [<span data-ttu-id="4bfe3-143">Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="4bfe3-143">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests.md)
-  [<span data-ttu-id="4bfe3-144">REST-API-Referenz und Beispiele</span><span class="sxs-lookup"><span data-stu-id="4bfe3-144">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [<span data-ttu-id="4bfe3-145">Verwenden von ETag-Werten zum Bestimmen der Version von Dokument- und Listenelementen über den REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="4bfe3-145">Use ETag values through the REST service to get document list item versioning</span></span>](http://msdn.microsoft.com/library/use-etag-values-through-the-rest-service-to-get-document-list-item-versioning%28Office.15%29.aspx)
    
 

 

 

