
# <a name="working-with-folders-and-files-with-rest"></a><span data-ttu-id="97c12-101">Arbeiten mit Ordnern und Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="97c12-101">Working with folders and files with REST</span></span>
<span data-ttu-id="97c12-102">In diesem Artikel erfahren Sie, wie Sie grundlegende Erstell-, Lese-, Aktualisierungs- und Löschoperationen, auch als CRUD-Operationen (Create, Read, Update, Delete) bezeichnet, für Ordner und Dateien mit der SharePoint REST-Schnittstelle durchführen.</span><span class="sxs-lookup"><span data-stu-id="97c12-102">Learn how to perform basic create, read, update, and delete (CRUD) operations on folders and files with the SharePoint REST interface.</span></span>
 

 <span data-ttu-id="97c12-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="97c12-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


 <span data-ttu-id="97c12-p102">**Tipp**  Der SharePoint Online-REST-Dienst (und der Dienst von SharePoint 2016 (lokal) und höher) unterstützt die Kombination mehrerer Anforderungen in einem einzelnen Dienstaufruf mithilfe der OData-Abfrageoption `$batch`. Einzelheiten und Links zu Codebeispielen finden Sie unter [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis) (Erstellen von Batchanforderungen mit den REST-APIs).</span><span class="sxs-lookup"><span data-stu-id="97c12-p102">**Tip**  The SharePoint Online (and on-premise SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData  `$batch` query option. For details and links to code samples, see [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis).</span></span> 
 


## <a name="working-with-folders-by-using-rest"></a><span data-ttu-id="97c12-108">Arbeiten mit Ordnern unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="97c12-108">Working with folders by using REST</span></span>
<span data-ttu-id="97c12-109"><a name="Folders"> </a></span><span class="sxs-lookup"><span data-stu-id="97c12-109"></span></span>

<span data-ttu-id="97c12-p103">Sie können einen Ordner innerhalb einer Dokumentbibliothek abrufen, wenn Sie die URL des Ordners kennen. Zum Beispiel können Sie den Stammordner Ihrer Bibliothek für freigegebene Dokumente abrufen, indem Sie den Endpunkt im folgenden Beispiel verwenden.</span><span class="sxs-lookup"><span data-stu-id="97c12-p103">You can retrieve a folder inside a document library when you know its URL. For example, you can retrieve the root folder of your Shared Documents library by using the endpoint in the following example.</span></span>
 

 

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Shared Documents')
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="97c12-112">Der folgende XML-Code zeigt ein Beispiel für die Ordnereigenschaften, die beim Anfordern des XML-Inhaltstyps zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="97c12-112">The following XML shows an example of folder properties that are returned when you request the XML content type.</span></span>
 

 



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

<span data-ttu-id="97c12-113">Das folgende Beispiel zeigt, wie Sie einen Ordner **erstellen**.</span><span class="sxs-lookup"><span data-stu-id="97c12-113">The following example shows how to  **create** a folder.</span></span>
 

 



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

<span data-ttu-id="97c12-114">Das folgende Beispiel zeigt, wie Sie einen Ordner **aktualisieren** und dazu die **MERGE**-Methode verwenden.</span><span class="sxs-lookup"><span data-stu-id="97c12-114">The following example shows how to  **update** a folder by using the **MERGE** method.</span></span>
 

 



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

<span data-ttu-id="97c12-115">Das folgende Beispiel zeigt, wie Sie einen Ordner **löschen**.</span><span class="sxs-lookup"><span data-stu-id="97c12-115">The following example shows how to  **delete** a folder.</span></span>
 

 



```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')
method: POST
Headers: 
     Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"DELETE"

```


## <a name="working-with-files-by-using-rest"></a><span data-ttu-id="97c12-116">Arbeiten mit Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="97c12-116">Working with files by using REST</span></span>
<span data-ttu-id="97c12-117"><a name="Files"> </a></span><span class="sxs-lookup"><span data-stu-id="97c12-117"></span></span>

<span data-ttu-id="97c12-118">Das folgende Beispiel zeigt, wie Sie alle Dateien in einem Ordner **abrufen**.</span><span class="sxs-lookup"><span data-stu-id="97c12-118">The following example shows how to  **retrieve** all of the files in a folder.</span></span>
 

 

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="97c12-119">Das folgende Beispiel zeigt, wie Sie eine bestimmte Datei **abrufen**.</span><span class="sxs-lookup"><span data-stu-id="97c12-119">The following example shows how to  **retrieve** a specific file.</span></span>
 

 



```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```

<span data-ttu-id="97c12-120">Sie können eine Datei auch **abrufen**, wenn Sie ihre URL kennen, wie im folgenden Beispiel gezeigt.</span><span class="sxs-lookup"><span data-stu-id="97c12-120">You can also  **retrieve** a file when you know its URL, as in the following example.</span></span>
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```

<span data-ttu-id="97c12-121">Das folgende Beispiel zeigt, wie Sie eine Datei **erstellen** und zu einem Ordner hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="97c12-121">The following example shows how to  **create** a file and add it to a folder.</span></span>
 

 



```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files/add(url='a.txt',overwrite=true)
method: POST
body: "Contents of file"
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    content-length:length of post body
```

<span data-ttu-id="97c12-122">Das folgende Beispiel zeigt, wie Sie eine Datei **aktualisieren** und dazu die **PUT**-Methode verwenden.</span><span class="sxs-lookup"><span data-stu-id="97c12-122">The following example shows how to  **update** a file by using the **PUT** method.</span></span>
 

 

 <span data-ttu-id="97c12-p104">**Hinweis**   **PUT** ist die einzige Methode, die Sie zum Aktualisieren einer Datei verwenden können. Die Methode **MERGE** ist nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="97c12-p104">**Note**   **PUT** is the only method that you can use to update a file. The **MERGE** method is not allowed.</span></span>
 




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

<span data-ttu-id="97c12-p105">Wenn Sie die Metadaten einer Datei aktualisieren möchten, müssen Sie einen Endpunkt erstellen, der die Datei als ein Listenelement erreicht. Dies ist möglich, da jeder Ordner auch eine Liste ist, und jede Datei auch ein Listenelement. Erstellen Sie einen Endpunkt, der in etwa so aussieht: `https://<site url>/_api/web/lists/getbytitle('Documents')/items(<item id>)`.  Unter [Working with lists and list items with REST](working-with-lists-and-list-items-with-rest) (Arbeiten mit Listen und Listenelementen mit REST) wird erläutert, wie Sie die Metadaten eines Listenelements aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="97c12-p105">If you want to update a file's metadata, you'll have to construct an endpoint that reaches the file as a list item. You can do this because each folder is also a list, and each file is also a list item. Construct an endpoint that looks like this:  `https://<site url>/_api/web/lists/getbytitle('Documents')/items(<item id>)`.  [Working with lists and list items with REST](working-with-lists-and-list-items-with-rest) explains how to update a list item's metadata.</span></span>
 

 
<span data-ttu-id="97c12-p106">Sie können eine Datei auschecken, um sicherzustellen, dass niemand sie ändert, bevor Sie sie aktualisieren. Nach der Aktualisierung sollten Sie die Datei wieder einchecken, sodass andere wieder damit arbeiten können. Im folgenden Beispiel wird gezeigt, wie Sie **eine Datei auschecken**.</span><span class="sxs-lookup"><span data-stu-id="97c12-p106">You may want to check out a file in order to make sure that no one changes it before you update it. After your update, you should also may want to check the file back in so that others can work with it. The following example shows you how to  **check a file out**.</span></span>
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckOut(),
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```

<span data-ttu-id="97c12-132">Im folgenden Beispiel wird gezeigt, wie Sie **eine Datei einchecken**.</span><span class="sxs-lookup"><span data-stu-id="97c12-132">The following example shows you how to  **check a file in**.</span></span>
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckIn(comment='Comment',checkintype=0)
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```

<span data-ttu-id="97c12-133">Das folgende Beispiel zeigt, wie Sie eine Datei **löschen**.</span><span class="sxs-lookup"><span data-stu-id="97c12-133">The following example shows how to  **delete** a file.</span></span>
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    IF-MATCH: etag or "*"
    X-HTTP-Method:"DELETE"

```


## <a name="working-with-large-files-by-using-rest"></a><span data-ttu-id="97c12-134">Arbeiten mit großen Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="97c12-134">Working with large files by using REST</span></span>
<span data-ttu-id="97c12-135"><a name="LargeFiles"> </a></span><span class="sxs-lookup"><span data-stu-id="97c12-135"></span></span>

<span data-ttu-id="97c12-p107"> Wenn Sie eine Binärdatei hochladen möchten, die größer ist als 1,5 Megabyte (MB), ist die REST-Schnittstelle die einzige Option. Unter [Complete basic operations using JavaScript library code in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013) (Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint) finden Sie ein Codebeispiel, in dem gezeigt wird, wie Sie eine binäre Datei mit unter 1,5 MB mithilfe des SharePoint Javascript-Objektmodells hochladen. Die maximale Größe einer Binärdatei, die Sie mit REST erstellen können, ist 2 Gigabyte (GB). Das folgende Beispiel zeigt, wie Sie eine große Binärdatei **erstellen**.</span><span class="sxs-lookup"><span data-stu-id="97c12-p107">When you need to upload a binary file that is larger than 1.5 megabytes (MB), the REST interface is your only option. See  [Complete basic operations using JavaScript library code in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013) for a code example that shows you how to upload a binary file that is smaller than 1.5 MB by using the SharePoint Javascript object model. The maximum size of a binary file that you can create with REST is 2 gigabytes (GB). The following example shows how to **create** a large binary file.</span></span>
 

 

 <span data-ttu-id="97c12-140">**Vorsicht** Dieser Ansatz funktioniert nur mit Internet Explorer 10 und den neuesten Versionen anderer Browser.</span><span class="sxs-lookup"><span data-stu-id="97c12-140">**Caution**  This approach will work only with Internet Explorer 10 and the latest versions of other browsers.</span></span>
 


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

<span data-ttu-id="97c12-141">Im folgenden Codebeispiel wird gezeigt, wie Sie eine Datei mit diesem REST-Endpunkt und der domänenübergreifenden Bibliothek erstellen.</span><span class="sxs-lookup"><span data-stu-id="97c12-141">The following code sample shows how to create a file by using this REST endpoint and the cross-domain library.</span></span>
 

 



```
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


## <a name="working-with-files-attached-to-list-items-by-using-rest"></a><span data-ttu-id="97c12-142">Arbeiten mit an Listenelemente angefügten Dateien mithilfe von REST</span><span class="sxs-lookup"><span data-stu-id="97c12-142">Working with files attached to list items by using REST</span></span>
<span data-ttu-id="97c12-143"><a name="FileAttachments"> </a></span><span class="sxs-lookup"><span data-stu-id="97c12-143"></span></span>

<span data-ttu-id="97c12-144">Das folgende Beispiel zeigt, wie Sie alle an ein Listenelement angefügten Dateien **abrufen**.</span><span class="sxs-lookup"><span data-stu-id="97c12-144">The following example shows how to  **retrieve** all of the files that are attached to a list item.</span></span>
 

 

```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles/
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="97c12-145">Das folgende Beispiel zeigt, wie Sie eine an ein Listenelement angefügte Datei **abrufen**.</span><span class="sxs-lookup"><span data-stu-id="97c12-145">The following example shows how to  **retrieve** a file that is attached to a list item.</span></span>
 

 



```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="97c12-146">Das folgende Beispiel zeigt, wie Sie eine an ein Listenelement angefügte Datei **erstellen**.</span><span class="sxs-lookup"><span data-stu-id="97c12-146">The following example shows how to  **create** a file attachment to a list item.</span></span>
 

 



```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles/ add(FileName='file name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
    body: "Contents of file."
    X-RequestDigest: form digest value
    content-length:length of post body
```

<span data-ttu-id="97c12-147">Das folgende Beispiel zeigt, wie Sie eine an ein Listenelement angefügte Datei **erstellen** und dabei die Methode **PUT** verwenden.</span><span class="sxs-lookup"><span data-stu-id="97c12-147">The following example shows how to  **update** a file attachment to a list item by using the **PUT** method.</span></span>
 

 

 <span data-ttu-id="97c12-p108">**Hinweis**   **PUT** ist die einzige Methode, die Sie zum Aktualisieren einer Datei verwenden können. Die Methode **MERGE** ist nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="97c12-p108">**Note**   **PUT** is the only method that you can use to update a file. The **MERGE** method is not allowed.</span></span>
 




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


## <a name="additional-resources"></a><span data-ttu-id="97c12-150">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="97c12-150">Additional resources</span></span>
<span data-ttu-id="97c12-151"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="97c12-151"></span></span>


-  [<span data-ttu-id="97c12-152">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="97c12-152">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-2013-rest-endpoints)
    
 
-  [<span data-ttu-id="97c12-153">Dateien und Ordner – REST-API-Referenz</span><span class="sxs-lookup"><span data-stu-id="97c12-153">Files and folders REST API reference</span></span>](http://msdn.microsoft.com/library/files-and-folders-rest-api-reference%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="97c12-154">Hochladen von Dateien mithilfe der REST-API und jQuery</span><span class="sxs-lookup"><span data-stu-id="97c12-154">Upload a file by using the REST API and jQuery</span></span>](upload-a-file-by-using-the-rest-api-and-jquery)
    
 
-  [<span data-ttu-id="97c12-155">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="97c12-155">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest)
    
 
-  [<span data-ttu-id="97c12-156">SharePoint-Add-in-REST-OData-BasicDataOperations</span><span class="sxs-lookup"><span data-stu-id="97c12-156">SharePoint-Add-in-REST-OData-BasicDataOperations</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
    
 
-  [<span data-ttu-id="97c12-157">SharePoint: Ausführen grundlegender Datenzugriffsvorgänge für Dateien und Ordner mithilfe von REST</span><span class="sxs-lookup"><span data-stu-id="97c12-157">SharePoint: Perform basic data access operations on files and folders by using REST</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Perform-ab9c4ae5)
    
 
-  [<span data-ttu-id="97c12-158">Durchführen von REST-Aufrufen mit C# und JavaScript für SharePoint</span><span class="sxs-lookup"><span data-stu-id="97c12-158">Making REST calls with C# and JavaScript for SharePoint</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)
    
 
-  [<span data-ttu-id="97c12-159">Durchführen von REST-Aufrufen mit C# und JavaScript für SharePoint - Demo</span><span class="sxs-lookup"><span data-stu-id="97c12-159">Making REST calls with C# and JavaScript for SharePoint demo</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=b1e7c9c5-0f62-4a78-bb7b-8e283c86145c)
    
 
-  [<span data-ttu-id="97c12-160">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode</span><span class="sxs-lookup"><span data-stu-id="97c12-160">Complete basic operations using SharePoint client library code</span></span>](complete-basic-operations-using-sharepoint-2013-client-library-code)
    
 
-  [<span data-ttu-id="97c12-161">Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint</span><span class="sxs-lookup"><span data-stu-id="97c12-161">Complete basic operations using JavaScript library code in SharePoint</span></span>](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="97c12-162">Entwickeln von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="97c12-162">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="97c12-163">Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="97c12-163">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="97c12-164">Arbeiten mit externen Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="97c12-164">Work with external data in SharePoint</span></span>](work-with-external-data-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="97c12-165">Open Data Protocol</span><span class="sxs-lookup"><span data-stu-id="97c12-165">Open Data Protocol</span></span>](http://www.odata.org/)
    
 
-  [<span data-ttu-id="97c12-166">OData: JSON(JavaScript Object Notation)-Format</span><span class="sxs-lookup"><span data-stu-id="97c12-166">OData: JavaScript Object Notation (JSON) Format</span></span>](http://www.odata.org/documentation/odata-version-2-0/JSON-format/)
    
 

 

 

