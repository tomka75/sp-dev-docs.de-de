---
title: Arbeiten mit Listen und Listenelementen unter Verwendung von REST
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: ec63b7dcf294e4a6248ca5c6014b6807f116f655
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="working-with-lists-and-list-items-with-rest"></a><span data-ttu-id="bc6ab-102">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="bc6ab-102">Working with lists and list items with REST</span></span>
<span data-ttu-id="bc6ab-103">In diesem Artikel erfahren Sie, wie Sie grundlegende Erstellungs-, Lese-, Aktualisierungs- und Löschoperationen, auch als CRUD-Operationen (Create, Read, Update, Delete) bezeichnet, für Listen und Listenelemente mit der SharePoint REST-Schnittstelle durchführen.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-103">Learn how to perform basic create, read, update, and delete (CRUD) operations on lists and list items with the SharePoint REST interface.</span></span>
 
 <span data-ttu-id="bc6ab-p101">**Tipp**  Der SharePoint Online-REST-Dienst (und der Dienst von SharePoint 2016 (lokal) und höher) unterstützt die Kombination mehrerer Anforderungen in einem einzelnen Dienstaufruf mithilfe der OData-Abfrageoption `$batch`. Einzelheiten und Links zu Codebeispielen finden Sie unter [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis.md) (Erstellen von Batchanforderungen mit den REST-APIs).</span><span class="sxs-lookup"><span data-stu-id="bc6ab-p101">**Tip**  The SharePoint Online (and on-premise SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData  `$batch` query option. For details and links to code samples, see [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis.md).</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="bc6ab-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="bc6ab-106">Prerequisites</span></span>
<span data-ttu-id="bc6ab-p102">In diesem Artikel setzen wir voraus, dass Sie bereits den Artikel zum Thema [Einführung in den SharePoint-REST-Dienst](get-to-know-the-sharepoint-rest-service.md) sowie den Artikel zum Thema [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](complete-basic-operations-using-sharepoint-rest-endpoints.md) gelesen haben. Es werden keine Codeausschnitte bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-p102">This topic assumes that you are already familiar with the topics  [Get to know the SharePoint REST service](get-to-know-the-sharepoint-rest-service.md) and [Complete basic operations using SharePoint REST endpoints](complete-basic-operations-using-sharepoint-rest-endpoints.md). It does not provide code snippets.</span></span>

## <a name="retrieving-lists-and-list-properties-with-rest"></a><span data-ttu-id="bc6ab-109">Abrufen von Listen und Listeneigenschaften mit REST</span><span class="sxs-lookup"><span data-stu-id="bc6ab-109">Retrieving lists and list properties with REST</span></span>
<span data-ttu-id="bc6ab-110"><a name="RetrieveLists"> </a> Das folgende Beispiel zeigt, wie Sie eine bestimmte Liste **abrufen**, wenn ihre GUID bekannt ist.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-110"><a name="RetrieveLists"> </a> The following example shows how to  **retrieve** a specific list if you know its GUID.</span></span>

```
url: http://site url/_api/web/lists(guid'list GUID'),
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```
> [!NOTE]
> <span data-ttu-id="bc6ab-p103">Verwenden Sie `application/json;odata=verbose` im `accept`-Header, wenn die Antwort im JSON-Format erfolgen soll. Verwenden Sie `application/atom+xml` im `accept`-Header, wenn die Antwort im Atom-Format erfolgen soll.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-p103">`application/json;odata=verbose`  Use  `accept` in the `application/atom+xml` header if you want the response in JSON. Use `accept` in the  header if you want the response in Atom format.</span></span>
 
<span data-ttu-id="bc6ab-113">Das folgende Beispiel zeigt, wie Sie eine bestimmte Liste **abrufen**, wenn ihr Titel bekannt ist.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-113">The following example shows how to  **retrieve** a specific list if you know its title.</span></span>

```
url: http://site url/_api/web/lists/GetByTitle('Test')
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```
<span data-ttu-id="bc6ab-114">Der folgende XML-Code zeigt ein Beispiel für die Listeneigenschaften, die beim Anfordern des XML-Inhaltstyps zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-114">The following XML shows an example of the list properties that are returned when you request the XML content type.</span></span>

```XML
  <content type="application/xml">
    <m:properties>
        <d:AllowContentTypes m:type="Edm.Boolean">true</d:AllowContentTypes> 
        <d:BaseTemplate m:type="Edm.Int32">100</d:BaseTemplate> 
        <d:BaseType m:type="Edm.Int32">0</d:BaseType> 
        <d:ContentTypesEnabled m:type="Edm.Boolean">false</d:ContentTypesEnabled> 
        <d:Created m:type="Edm.DateTime">2012-06-26T23:15:58Z</d:Created> 
        <d:DefaultContentApprovalWorkflowId m:type="Edm.Guid">00000000-0000-0000-0000-000000000000</d:DefaultContentApprovalWorkflowId> 
        <d:Description>A list created by Project Based Retention used to store Project Policy Items.</d:Description> 
        <d:Direction>none</d:Direction> 
        <d:DocumentTemplateUrl m:null="true" /> 
        <d:DraftVersionVisibility m:type="Edm.Int32">0</d:DraftVersionVisibility> 
        <d:EnableAttachments m:type="Edm.Boolean">true</d:EnableAttachments> 
        <d:EnableFolderCreation m:type="Edm.Boolean">false</d:EnableFolderCreation> 
        <d:EnableMinorVersions m:type="Edm.Boolean">false</d:EnableMinorVersions> 
        <d:EnableModeration m:type="Edm.Boolean">false</d:EnableModeration> 
        <d:EnableVersioning m:type="Edm.Boolean">false</d:EnableVersioning> 
        <d:EntityTypeName>ProjectPolicyItemList</d:EntityTypeName> 
        <d:ForceCheckout m:type="Edm.Boolean">false</d:ForceCheckout> 
        <d:HasExternalDataSource m:type="Edm.Boolean">false</d:HasExternalDataSource> 
        <d:Hidden m:type="Edm.Boolean">true</d:Hidden> 
        <d:Id m:type="Edm.Guid">74de3ff3-029c-42f9-bd2a-1e9463def69d</d:Id> 
        <d:ImageUrl>/_layouts/15/images/itgen.gif</d:ImageUrl> 
        <d:IrmEnabled m:type="Edm.Boolean">false</d:IrmEnabled> 
        <d:IrmExpire m:type="Edm.Boolean">false</d:IrmExpire> 
        <d:IrmReject m:type="Edm.Boolean">false</d:IrmReject> 
        <d:IsApplicationList m:type="Edm.Boolean">false</d:IsApplicationList> 
        <d:IsCatalog m:type="Edm.Boolean">false</d:IsCatalog> 
        <d:IsPrivate m:type="Edm.Boolean">false</d:IsPrivate> 
        <d:ItemCount m:type="Edm.Int32">0</d:ItemCount> 
        <d:LastItemDeletedDate m:type="Edm.DateTime">2012-06-26T23:15:58Z</d:LastItemDeletedDate> 
        <d:LastItemModifiedDate m:type="Edm.DateTime">2012-06-26T23:15:59Z</d:LastItemModifiedDate> 
        <d:ListItemEntityTypeFullName>SP.Data.ProjectPolicyItemListItem</d:ListItemEntityTypeFullName> 
        <d:MultipleDataList m:type="Edm.Boolean">false</d:MultipleDataList> 
        <d:NoCrawl m:type="Edm.Boolean">true</d:NoCrawl> 
        <d:ParentWebUrl>/</d:ParentWebUrl> 
        <d:ServerTemplateCanCreateFolders m:type="Edm.Boolean">true</d:ServerTemplateCanCreateFolders> 
        <d:TemplateFeatureId m:type="Edm.Guid">00bfea71-de22-43b2-a848-c05709900100</d:TemplateFeatureId> 
        <d:Title>Project Policy Item List</d:Title> 
    </m:properties>
  </content>
```
> [!NOTE]
> <span data-ttu-id="bc6ab-p104">Die Eigenschaft **ListItemEntityTypeFullName** (**SP.Data.ProjectPolicyItemListItem** im vorhergehenden Beispiel) ist wichtig, wenn Sie Listenelemente erstellen und aktualisieren möchten. Dieser Wert muss als **type**-Eigenschaft in den Metadaten übergeben werden, die Sie im Textkörper der HTTP-Anforderung übergeben, wenn Sie Listenelemente erstellen und aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-p104">**Note**  The  **ListItemEntityTypeFullName** property ( **SP.Data.ProjectPolicyItemListItem** in the previous example) is especially important if you want to create and update list items. This value must be passed as the type property in the metadata that you pass in the body of the HTTP request whenever you create and update list items.</span></span>

## <a name="working-with-lists-by-using-rest"></a><span data-ttu-id="bc6ab-117">Arbeiten mit Listen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="bc6ab-117">Working with lists by using REST</span></span>
<span data-ttu-id="bc6ab-118"><a name="WorkLists"> </a> Das folgende Beispiel zeigt, wie Sie eine Liste **erstellen**.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-118"><a name="WorkLists"> </a> The following example shows how to  **create** a list.</span></span>

```
url: http://site url/_api/web/lists
method: POST
body: { '__metadata': { 'type': 'SP.List' }, 'AllowContentTypes': true, 'BaseTemplate': 100,
 'ContentTypesEnabled': true, 'Description': 'My list description', 'Title': 'Test' }
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

<span data-ttu-id="bc6ab-119">Das folgende Beispiel zeigt, wie Sie eine Liste **aktualisieren** und dazu die **MERGE**-Methode verwenden.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-119">The following example shows how to  **update** a list by using the **MERGE** method.</span></span>

```
url: http://site url/_api/web/lists(guid'list GUID')
method: POST
body: { '__metadata': { 'type': 'SP.List' }, 'Title': 'New title' }
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    IF-MATCH": etag or "*"
    X-HTTP-Method: MERGE,
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```
<span data-ttu-id="bc6ab-120">Das folgende Beispiel zeigt, wie Sie ein **benutzerdefiniertes Feld** für eine Liste **erstellen**.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-120">The following example shows how to  **create** a **custom field** for a list.</span></span>

```
Url: url: http://site url/_api/web/lists(guid'list GUID')/Fields
Method:POST
Body: { '__metadata': { 'type': 'SP.Field' }, 'Title': 'field title', 'FieldTypeKind': FieldType value,'Required': 'true/false', 'EnforceUniqueValues': 'true/false','StaticName': 'field name'}
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

<span data-ttu-id="bc6ab-121">Das folgende Beispiel zeigt, wie Sie eine Liste **löschen**.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-121">The following example shows how to  **delete** a list.</span></span>

```
url: http://site url/_api/web/lists(guid'list GUID')
method: POST
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    IF-MATCH: etag or "*"
    X-HTTP-Method: DELETE

```

## <a name="working-with-list-items-by-using-rest"></a><span data-ttu-id="bc6ab-122">Arbeiten mit Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="bc6ab-122">Working with list items by using REST</span></span>
<span data-ttu-id="bc6ab-123"><a name="ListItems"> </a> Das folgende Beispiel zeigt, wie Sie alle Elemente einer Liste **abrufen**.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-123"><a name="ListItems"> </a> The following example shows how to  **retrieve** all of a list's items.</span></span>
 
> [!NOTE]
> <span data-ttu-id="bc6ab-p105">Die OData-Abfrageoption $skip funktioniert nicht beim Abfragen von Listenelementen. In vielen Situationen können Sie stattdessen die Option [$skiptoken](http://msdn.microsoft.com/library/4dda9434-c2c5-4577-8e01-7bf9e822d90a.aspx) verwenden.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-p105">The OData $skip query option does not work when querying list items. In may situations, you can use the [$skiptoken](http://msdn.microsoft.com/library/4dda9434-c2c5-4577-8e01-7bf9e822d90a.aspx) option instead.</span></span>

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="bc6ab-126">Das folgende Beispiel zeigt, wie sie ein bestimmtes Listenelement **abrufen**.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-126">The following example shows how to  **retrieve** a specific list item.</span></span>

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="bc6ab-127">Der folgende XML-Code zeigt ein Beispiel für die Listenelementeigenschaften, die beim Anfordern des XML-Inhaltstyps zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-127">The following XML shows an example of the list item properties that are returned when you request the XML content type.</span></span>
 
```XML
<content type="application/xml">
<m:properties> 
<d:FileSystemObjectType m:type="Edm.Int32">0</d:FileSystemObjectType>
<d:Id m:type="Edm.Int32">1</d:Id>
<d:ID m:type="Edm.Int32">1</d:ID>
<d:ContentTypeId>0x010049564F321A0F0543BA8C6303316C8C0F</d:ContentTypeId>
<d:Title>an item</d:Title>
<d:Modified m:type="Edm.DateTime">2012-07-24T22:47:26Z</d:Modified>
<d:Created m:type="Edm.DateTime">2012-07-24T22:47:26Z</d:Created>
<d:AuthorId m:type="Edm.Int32">11</d:AuthorId>
<d:EditorId m:type="Edm.Int32">11</d:EditorId>
<d:OData__UIVersionString>1.0</d:OData__UIVersionString>
<d:Attachments m:type="Edm.Boolean">false</d:Attachments>
<d:GUID m:type="Edm.Guid">eb6850c5-9a30-4636-b282-234eda8b1057</d:GUID>
</m:properties>
</content>
```

<span data-ttu-id="bc6ab-128">Das folgende Beispiel zeigt, wie Sie ein Listenelement **erstellen**.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-128">The following example shows how to  **create** a list item.</span></span>

> [!NOTE]
> <span data-ttu-id="bc6ab-129">Um diese Operation durchzuführen, müssen Sie die Eigenschaft **ListItemEntityTypeFullName** der Liste kennen und sie als Wert von **type** im Textkörper der HTTP-Anforderung übergeben.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-129">To do this operation, you must know the **ListItemEntityTypeFullName** property of the list and pass that as the value of **type** in the HTTP request body.</span></span>

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: POST
body: { '__metadata': { 'type': 'SP.Data.TestListItem' }, 'Title': 'Test'}
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

<span data-ttu-id="bc6ab-130">Das folgende Beispiel zeigt, wie Sie ein Listenelement **aktualisieren**.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-130">The following example shows how to  **update** a list item.</span></span>

> [!NOTE]
> <span data-ttu-id="bc6ab-131">Um diese Operation durchzuführen, müssen Sie die Eigenschaft **ListItemEntityTypeFullName** der Liste kennen und sie als Wert von **type** im Textkörper der HTTP-Anforderung übergeben.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-131">To do this operation, you must know the **ListItemEntityTypeFullName** property of the list and pass that as the value of **type** in the HTTP request body.</span></span>

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: POST
body: { '__metadata': { 'type': 'SP.Data.TestListItem' }, 'Title': 'TestUpdated'}
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"MERGE",
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

<span data-ttu-id="bc6ab-132">Das folgende Beispiel zeigt, wie Sie ein Listenelement **löschen**.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-132">The following example shows how to  **delete** a list item.</span></span>

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: POST
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"DELETE"

```

## <a name="using-etag-values-to-determine-document-and-list-item-versioning"></a><span data-ttu-id="bc6ab-133">Verwenden von ETag-Werten zum Bestimmen der Version von Dokument- und Listenelementen</span><span class="sxs-lookup"><span data-stu-id="bc6ab-133">Using ETag values to determine document and list item versioning</span></span>
<span data-ttu-id="bc6ab-134"><a name="Etag"> </a> Der SharePoint REST-Dienst, der sich nach dem  [OData-Standard](http://www.odata.org/developers/protocols/operations) richtet, verwendet  [HTML ETags für die Gleichzeitigkeitssteuerung](http://www.odata.org/developers/protocols/operations#ConcurrencycontrolandETags) von SharePoint-Listen und -Listenelementen.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-134"><a name="Etag"> </a> The SharePoint REST service, which follows the  [OData standard](http://www.odata.org/developers/protocols/operations), uses  [HTML ETags for concurrency control](http://www.odata.org/developers/protocols/operations#ConcurrencycontrolandETags) of SharePoint lists and list items.</span></span> <span data-ttu-id="bc6ab-135">Um die Version eines Elements beim Ausführen einer **PUT**-,  **MERGE**- oder  **DELETE**-Anforderung zu prüfen, geben Sie ein **ETag** im HTTP-Anforderungskopf **If-Match** an.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-135">To check on an item's version when you perform a **PUT**,  **MERGE**, or  **DELETE** request, specify an **ETag** in the **If-Match** HTTP request header.</span></span>
 
<span data-ttu-id="bc6ab-136">Wenn das in Ihrer Anforderung angegebene **ETag** nicht mit dem **ETag** des Dokument- oder Listenelements auf dem Server übereinstimmt, gibt der REST-Dienst gemäß der OData-Spezifikation eine 412-Ausnahme zurück.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-136">If the  **ETag** you specify in your request does not match the **ETag** of the document or list item on the server, the REST service returns a 412 exception, per the OData specification.</span></span>
 
- <span data-ttu-id="bc6ab-137">Wenn Sie ein Überschreiben des Elements unabhängig von der Version erzwingen möchten, legen Sie den **ETag**-Wert auf **"*"** fest.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-137">To force an overwrite of the item regardless of version, set the  **ETag** value to **"*"**.</span></span>
    
- <span data-ttu-id="bc6ab-138">Wenn Sie kein **ETag** angeben, überschreibt SharePoint das Element unabhängig von der Version.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-138">If you do not specify an  **ETag**, SharePoint overwrites the item regardless of version.</span></span>
    
<span data-ttu-id="bc6ab-139">In SharePoint gelten ETags nur für SharePoint-Listen und Listenelemente.</span><span class="sxs-lookup"><span data-stu-id="bc6ab-139">Within SharePoint, ETags apply only to SharePoint lists and list items.</span></span>

## <a name="see-also"></a><span data-ttu-id="bc6ab-140">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="bc6ab-140">See also</span></span>
<span data-ttu-id="bc6ab-141"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="bc6ab-141"><a name="bk_addresources"> </a></span></span>

-  [<span data-ttu-id="bc6ab-142">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="bc6ab-142">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [<span data-ttu-id="bc6ab-143">Arbeiten mit Ordnern und Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="bc6ab-143">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest.md)
-  [<span data-ttu-id="bc6ab-144">SharePoint-Add-in-REST-OData-BasicDataOperations</span><span class="sxs-lookup"><span data-stu-id="bc6ab-144">SharePoint-Add-in-REST-OData-BasicDataOperations</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
-  [<span data-ttu-id="bc6ab-145">SharePoint 2013: Ausführen grundlegender Datenzugriffsvorgänge für Dateien und Ordner mithilfe von REST</span><span class="sxs-lookup"><span data-stu-id="bc6ab-145">SharePoint 2013: Perform basic data access operations on files and folders by using REST</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Perform-ab9c4ae5)
-  [<span data-ttu-id="bc6ab-146">Durchführen von REST-Aufrufen mit C# und JavaScript für SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="bc6ab-146">Making REST calls with C# and JavaScript for SharePoint 2013</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/video.mdl?cid=sdc&amp;from=mscomsdc&amp;VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)
-  [<span data-ttu-id="bc6ab-147">Open Data Protocol</span><span class="sxs-lookup"><span data-stu-id="bc6ab-147">Open Data Protocol</span></span>](http://www.odata.org/)
-  [<span data-ttu-id="bc6ab-148">OData: JSON(JavaScript Object Notation)-Format</span><span class="sxs-lookup"><span data-stu-id="bc6ab-148">OData: JavaScript Object Notation (JSON) Format</span></span>](http://www.odata.org/documentation/odata-version-2-0/json-format/)
