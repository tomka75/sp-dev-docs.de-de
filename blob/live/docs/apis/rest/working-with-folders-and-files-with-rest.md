---
title: Arbeiten mit Ordnern und Dateien unter Verwendung von REST
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: e73431770902a5cfca0d5192f335091f39419f73
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="working-with-folders-and-files-with-rest"></a><span data-ttu-id="2fb6e-102">Arbeiten mit Ordnern und Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="2fb6e-102">Working with folders and files with REST</span></span>
<span data-ttu-id="2fb6e-103">In diesem Artikel erfahren Sie, wie Sie grundlegende Erstellungs-, Lese-, Aktualisierungs- und Löschoperationen, auch als CRUD-Operationen (Create, Read, Update, Delete) bezeichnet, für Ordner und Dateien mit der SharePoint 2013 REST-Schnittstelle durchführen.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-103">Learn how to perform basic create, read, update, and delete (CRUD) operations on folders and files with the SharePoint 2013 REST interface.</span></span>

 <span data-ttu-id="2fb6e-p101">**Tipp**  Der SharePoint Online-REST-Dienst (und der Dienst von SharePoint 2016 (lokal) und höher) unterstützt die Kombination mehrerer Anforderungen in einem einzelnen Dienstaufruf mithilfe der OData-Abfrageoption `$batch`. Einzelheiten und Links zu Codebeispielen finden Sie unter [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis.md) (Erstellen von Batchanforderungen mit den REST-APIs).</span><span class="sxs-lookup"><span data-stu-id="2fb6e-p101">**Tip**  The SharePoint Online (and on-premise SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData  `$batch` query option. For details and links to code samples, see [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis.md).</span></span> 

## <a name="working-with-folders-by-using-rest"></a><span data-ttu-id="2fb6e-106">Arbeiten mit Ordnern unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="2fb6e-106">Working with folders by using REST</span></span>
<span data-ttu-id="2fb6e-p102"><a name="Folders"> </a> Sie können einen Ordner in einer Dokumentbibliothek abrufen, wenn Sie die entsprechende URL kennen. Beispielsweise können Sie den Stammordner Ihrer Bibliothek freigegebener Dokumente abrufen, indem Sie den Endpunkt wie im folgenden Beispiel verwenden.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-p102"><a name="Folders"> </a> You can retrieve a folder inside a document library when you know its URL. For example, you can retrieve the root folder of your Shared Documents library by using the endpoint in the following example.</span></span>

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Shared Documents')
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="2fb6e-109">Der folgende XML-Code zeigt ein Beispiel für die Ordnereigenschaften, die beim Anfordern des XML-Inhaltstyps zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-109">The following XML shows an example of folder properties that are returned when you request the XML content type.</span></span>

```XML
<content type="application/xml">
<m:properties>
<d:ItemCount m:type="Edm.Int32">0</d:ItemCount>
<d:Name>Shared Documents</d:Name>
<d:ServerRelativeUrl>/Shared Documents</d:ServerRelativeUrl>
<d:WelcomePage/>
</m:properties>
</content>
```
<span data-ttu-id="2fb6e-110">Das folgende Beispiel zeigt, wie Sie einen Ordner **erstellen**.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-110">The following example shows how to  **create** a folder.</span></span>

```
url: http://site url/_api/web/folders
method: POST
body: { '__metadata': { 'type': 'SP.Folder' }, 'ServerRelativeUrl': '/document library relative url/folder name'}
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

<span data-ttu-id="2fb6e-111">Das folgende Beispiel zeigt, wie Sie einen Ordner **aktualisieren** und dazu die **MERGE**-Methode verwenden.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-111">The following example shows how to  **update** a folder by using the **MERGE** method.</span></span>

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')
method: POST
body: { '__metadata': { 'type': 'SP.Folder' }, 'Name': 'New name' }
Headers: 
     Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"MERGE",
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

<span data-ttu-id="2fb6e-112">Das folgende Beispiel zeigt, wie Sie einen Ordner **löschen**.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-112">The following example shows how to  **delete** a folder.</span></span>

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')
method: POST
Headers: 
     Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"DELETE"

```
## <a name="working-with-files-by-using-rest"></a><span data-ttu-id="2fb6e-113">Arbeiten mit Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="2fb6e-113">Working with files by using REST</span></span>
<span data-ttu-id="2fb6e-114"><a name="Files"> </a> Das folgende Beispiel zeigt, wie Sie alle Dateien in einem Ordner **abrufen**.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-114"><a name="Files"> </a> The following example shows how to  **retrieve** all of the files in a folder.</span></span>

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="2fb6e-115">Das folgende Beispiel zeigt, wie sie eine bestimmte Datei **abrufen**.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-115">The following example shows how to  **retrieve** a specific file.</span></span>
 
```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```

<span data-ttu-id="2fb6e-116">Sie können eine Datei auch **abrufen**, wenn Sie ihre URL kennen, wie im folgenden Beispiel gezeigt.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-116">You can also  **retrieve** a file when you know its URL, as in the following example.</span></span>
 
```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```
<span data-ttu-id="2fb6e-117">Das folgende Beispiel zeigt, wie Sie eine Datei **erstellen** und zu einem Ordner hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-117">The following example shows how to  **create** a file and add it to a folder.</span></span>
 
```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files/add(url='a.txt',overwrite=true)
method: POST
body: "Contents of file"
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    content-length:length of post body
```

<span data-ttu-id="2fb6e-118">Das folgende Beispiel zeigt, wie Sie eine Datei **aktualisieren** und dazu die **PUT**-Methode verwenden.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-118">The following example shows how to  **update** a file by using the **PUT** method.</span></span>

 <span data-ttu-id="2fb6e-p103">**Hinweis**   **PUT** ist die einzige Methode, die Sie zum Aktualisieren einer Datei verwenden können. Die Methode **MERGE** ist nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-p103">**Note**   **PUT** is the only method that you can use to update a file. The **MERGE** method is not allowed.</span></span>

```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/$value
method: POST
body: "Contents of file."
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    X-HTTP-Method:"PUT"
    content-length:length of post body
```
<span data-ttu-id="2fb6e-p104">Wenn Sie die Metadaten einer Datei aktualisieren möchten, müssen Sie einen Endpunkt erstellen, der die Datei als ein Listenelement erreicht. Dies ist möglich, da jeder Ordner auch eine Liste ist, und jede Datei auch ein Listenelement. Erstellen Sie einen Endpunkt, der in etwa so aussieht: `https://<site url>/_api/web/lists/getbytitle('Documents')/items(<item id>)`.  Unter [Working with lists and list items with REST](working-with-lists-and-list-items-with-rest.md) (Arbeiten mit Listen und Listenelementen mit REST) wird erläutert, wie Sie die Metadaten eines Listenelements aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-p104">If you want to update a file's metadata, you'll have to construct an endpoint that reaches the file as a list item. You can do this because each folder is also a list, and each file is also a list item. Construct an endpoint that looks like this:  `https://<site url>/_api/web/lists/getbytitle('Documents')/items(<item id>)`.  [Working with lists and list items with REST](working-with-lists-and-list-items-with-rest.md) explains how to update a list item's metadata.</span></span>
 
<span data-ttu-id="2fb6e-p105">Sie können eine Datei auschecken, um sicherzustellen, dass niemand sie ändert, bevor Sie sie aktualisieren. Nach der Aktualisierung sollten Sie die Datei wieder einchecken, sodass andere wieder damit arbeiten können. Im folgenden Beispiel wird gezeigt, wie Sie **eine Datei auschecken**.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-p105">You may want to check out a file in order to make sure that no one changes it before you update it. After your update, you should also may want to check the file back in so that others can work with it. The following example shows you how to  **check a file out**.</span></span>

```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckOut(),
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```
<span data-ttu-id="2fb6e-128">Im folgenden Beispiel wird gezeigt, wie Sie **eine Datei einchecken**.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-128">The following example shows you how to  **check a file in**.</span></span>

```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckIn(comment='Comment',checkintype=0)
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```
<span data-ttu-id="2fb6e-129">Das folgende Beispiel zeigt, wie Sie eine Datei **löschen**.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-129">The following example shows how to  **delete** a file.</span></span>

```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    IF-MATCH: etag or "*"
    X-HTTP-Method:"DELETE"

```

## <a name="working-with-large-files-by-using-rest"></a><span data-ttu-id="2fb6e-130">Arbeiten mit großen Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="2fb6e-130">Working with large files by using REST</span></span>
<span data-ttu-id="2fb6e-p106"><a name="LargeFiles"> </a> Wenn Sie eine Binärdatei hochladen möchten, die größer ist als 1,5 Megabyte (MB), ist die REST-Schnittstelle die einzige Option. Unter [Complete basic operations using JavaScript library code in SharePoint](../../sp-add-ins/complete-basic-operations-using-javascript-library-code-in-sharepoint.md) (Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint) finden Sie ein Codebeispiel, in dem gezeigt wird, wie Sie eine binäre Datei mit unter 1,5 MB mithilfe des SharePoint Javascript-Objektmodells hochladen. Die maximale Größe einer Binärdatei, die Sie mit REST erstellen können, ist 2 Gigabyte (GB). Das folgende Beispiel zeigt, wie Sie eine große Binärdatei **erstellen**.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-p106"><a name="LargeFiles"> </a> When you need to upload a binary file that is larger than 1.5 megabytes (MB), the REST interface is your only option. See  [Complete basic operations using JavaScript library code in SharePoint](../../sp-add-ins/complete-basic-operations-using-javascript-library-code-in-sharepoint.md) for a code example that shows you how to upload a binary file that is smaller than 1.5 MB by using the SharePoint Javascript object model. The maximum size of a binary file that you can create with REST is 2 gigabytes (GB). The following example shows how to **create** a large binary file.</span></span>
 
 <span data-ttu-id="2fb6e-135">**Vorsicht**  Dieser Ansatz funktioniert nur mit Internet Explorer 10 und den neuesten Versionen anderer Browser.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-135">**Caution**  This approach will work only with Internet Explorer 10 and the latest versions of other browsers.</span></span>
 
```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files/Add(url='file name', overwrite=true)
method: POST
body: contents of binary file
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```
<span data-ttu-id="2fb6e-136">Im folgenden Codebeispiel wird gezeigt, wie Sie eine Datei mit diesem REST-Endpunkt und der domänenübergreifenden Bibliothek erstellen.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-136">The following code sample shows how to create a file by using this REST endpoint and the cross-domain library.</span></span>
 
```javascript
function uploadFileBinary() {
XDomainTestHelper.clearLog();
var ro;
if (document.getElementById("TxtViaUrl").value.length > 0) {
ro = new SP.RequestExecutor(document.getElementById("TxtWebUrl").value, document.getElementById("TxtViaUrl").value);
}
else {
ro = new SP.RequestExecutor(document.getElementById("TxtWebUrl").value);
}
var body = "";
for (var i = 0; i < 1000; i++) {
var ch = i % 256;
body = body + String.fromCharCode(ch);
}
var info = {
url: "_api/web/lists/getByTitle('Shared Documents')/RootFolder/Files/Add(url='a.dat', overwrite=true)",
method: "POST",
binaryStringRequestBody: true,
body: body,
success: success,
error: fail,
state: "Update"
};
ro.executeAsync(info);
}

```
## <a name="working-with-files-attached-to-list-items-by-using-rest"></a><span data-ttu-id="2fb6e-137">Arbeiten mit an Listenelemente angefügten Dateien mithilfe von REST</span><span class="sxs-lookup"><span data-stu-id="2fb6e-137">Working with files attached to list items by using REST</span></span>
<span data-ttu-id="2fb6e-138"><a name="FileAttachments"> </a> Das folgende Beispiel zeigt, wie Sie alle an ein Listenelement angefügten Dateien **abrufen**.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-138"><a name="FileAttachments"> </a> The following example shows how to  **retrieve** all of the files that are attached to a list item.</span></span>

```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles/
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```
<span data-ttu-id="2fb6e-139">Das folgende Beispiel zeigt, wie Sie eine an ein Listenelement angefügte Datei **abrufen**.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-139">The following example shows how to  **retrieve** a file that is attached to a list item.</span></span>

```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```
<span data-ttu-id="2fb6e-140">Das folgende Beispiel zeigt, wie Sie eine an ein Listenelement angefügte Datei **erstellen**.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-140">The following example shows how to  **create** a file attachment to a list item.</span></span>

```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles/ add(FileName='file name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
    body: "Contents of file."
    X-RequestDigest: form digest value
    content-length:length of post body
```

<span data-ttu-id="2fb6e-141">Das folgende Beispiel zeigt, wie Sie eine an ein Listenelement angefügte Datei **erstellen** und dabei die Methode **PUT** verwenden.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-141">The following example shows how to  **update** a file attachment to a list item by using the **PUT** method.</span></span>

 <span data-ttu-id="2fb6e-p107">**Hinweis**   **PUT** ist die einzige Methode, die Sie zum Aktualisieren einer Datei verwenden können. Die Methode **MERGE** ist nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-p107">**Note**   **PUT** is the only method that you can use to update a file. The **MERGE** method is not allowed.</span></span>
 
```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles('file name')/$value
method: POST
body: "Contents of file."
headers:
    Authorization: "Bearer " + accessToken
    "X-HTTP-Method":"PUT"
    X-RequestDigest: form digest value
    content-length:length of post body
```
## <a name="additional-resources"></a><span data-ttu-id="2fb6e-144">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="2fb6e-144">Additional resources</span></span>
<span data-ttu-id="2fb6e-145"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2fb6e-145"></span></span>

-  [<span data-ttu-id="2fb6e-146">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="2fb6e-146">Complete basic operations using SharePoint REST endpoints</span></span>](../../sp-add-ins/complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [<span data-ttu-id="2fb6e-147">Dateien und Ordner – REST-API-Referenz</span><span class="sxs-lookup"><span data-stu-id="2fb6e-147">Files and folders REST API reference</span></span>](http://msdn.microsoft.com/library/2c3d2545-1cd7-497e-b535-12199d8edfbb%28Office.15%29.aspx)
-  [<span data-ttu-id="2fb6e-148">Hochladen von Dateien mithilfe der REST-API und jQuery</span><span class="sxs-lookup"><span data-stu-id="2fb6e-148">Upload a file by using the REST API and jQuery</span></span>](upload-a-file-by-using-the-rest-api-and-jquery.md)
-  [<span data-ttu-id="2fb6e-149">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="2fb6e-149">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
-  [<span data-ttu-id="2fb6e-150">SharePoint-Add-in-REST-OData-BasicDataOperations</span><span class="sxs-lookup"><span data-stu-id="2fb6e-150">SharePoint-Add-in-REST-OData-BasicDataOperations</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
-  [<span data-ttu-id="2fb6e-151">SharePoint 2013: Ausführen grundlegender Datenzugriffsvorgänge für Dateien und Ordner mithilfe von REST</span><span class="sxs-lookup"><span data-stu-id="2fb6e-151">SharePoint 2013: Perform basic data access operations on files and folders by using REST</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Perform-ab9c4ae5)
-  [<span data-ttu-id="2fb6e-152">Durchführen von REST-Aufrufen mit C# und JavaScript für SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="2fb6e-152">Making REST calls with C# and JavaScript for SharePoint 2013</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/video.mdl?cid=sdc&amp;from=mscomsdc&amp;VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)
-  [<span data-ttu-id="2fb6e-153">Durchführen von REST-Aufrufen mit C# und JavaScript für SharePoint 2013 Demo</span><span class="sxs-lookup"><span data-stu-id="2fb6e-153">Making REST calls with C# and JavaScript for SharePoint 2013 demo</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/video.mdl?cid=sdc&amp;from=mscomsdc&amp;VideoID=b1e7c9c5-0f62-4a78-bb7b-8e283c86145c)
-  [<span data-ttu-id="2fb6e-154">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint 2013-Clientbibliothekscode</span><span class="sxs-lookup"><span data-stu-id="2fb6e-154">Complete basic operations using SharePoint 2013 client library code</span></span>](../../sp-add-ins/complete-basic-operations-using-sharepoint-client-library-code.md)
-  [<span data-ttu-id="2fb6e-155">Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="2fb6e-155">Complete basic operations using JavaScript library code in SharePoint 2013</span></span>](../../sp-add-ins/complete-basic-operations-using-javascript-library-code-in-sharepoint.md)
-  [<span data-ttu-id="2fb6e-156">Entwickeln von Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="2fb6e-156">Develop SharePoint Add-ins</span></span>](../../sp-add-ins/develop-sharepoint-add-ins.md)
-  [<span data-ttu-id="2fb6e-157">Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="2fb6e-157">Secure data access and client object models for SharePoint Add-ins</span></span>](../../sp-add-ins/secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
-  [<span data-ttu-id="2fb6e-158">Arbeiten mit externen Daten in SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="2fb6e-158">Work with external data in SharePoint 2013</span></span>](../../sp-add-ins/work-with-external-data-in-sharepoint.md)
-  [<span data-ttu-id="2fb6e-159">Open Data Protocol</span><span class="sxs-lookup"><span data-stu-id="2fb6e-159">Open Data Protocol</span></span>](http://www.odata.org/)
-  [<span data-ttu-id="2fb6e-160">OData: JSON(JavaScript Object Notation)-Format</span><span class="sxs-lookup"><span data-stu-id="2fb6e-160">OData: JavaScript Object Notation (JSON) Format</span></span>](http://www.odata.org/documentation/odata-version-2-0/JSON-format/)
