---
title: Arbeiten mit Ordnern und Dateien unter Verwendung von REST
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: ec4f299782b5f1ae58c04ba245ae6c10aeb35c60
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="working-with-folders-and-files-with-rest"></a>Arbeiten mit Ordnern und Dateien unter Verwendung von REST
In diesem Artikel erfahren Sie, wie Sie grundlegende Erstell-, Lese-, Aktualisierungs- und Löschoperationen, auch als CRUD-Operationen (Create, Read, Update, Delete) bezeichnet, für Ordner und Dateien mit der SharePoint REST-Schnittstelle durchführen.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).
 


 **Tipp**  Der SharePoint Online-REST-Dienst (und der Dienst von SharePoint 2016 (lokal) und höher) unterstützt die Kombination mehrerer Anforderungen in einem einzelnen Dienstaufruf mithilfe der OData-Abfrageoption `$batch`. Einzelheiten und Links zu Codebeispielen finden Sie unter [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis.md) (Erstellen von Batchanforderungen mit den REST-APIs). 
 


## <a name="working-with-folders-by-using-rest"></a>Arbeiten mit Ordnern unter Verwendung von REST
<a name="Folders"> </a>

Sie können einen Ordner innerhalb einer Dokumentbibliothek abrufen, wenn Sie die URL des Ordners kennen. Zum Beispiel können Sie den Stammordner Ihrer Bibliothek für freigegebene Dokumente abrufen, indem Sie den Endpunkt im folgenden Beispiel verwenden.
 

 

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Shared Documents')
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

Der folgende XML-Code zeigt ein Beispiel für die Ordnereigenschaften, die beim Anfordern des XML-Inhaltstyps zurückgegeben werden.
 

 



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

Das folgende Beispiel zeigt, wie Sie einen Ordner **erstellen**.
 

 



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

Das folgende Beispiel zeigt, wie Sie einen Ordner **aktualisieren** und dazu die **MERGE**-Methode verwenden.
 

 



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

Das folgende Beispiel zeigt, wie Sie einen Ordner **löschen**.
 

 



```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')
method: POST
Headers: 
     Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"DELETE"

```


## <a name="working-with-files-by-using-rest"></a>Arbeiten mit Dateien unter Verwendung von REST
<a name="Files"> </a>

Das folgende Beispiel zeigt, wie Sie alle Dateien in einem Ordner **abrufen**.
 

 

```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

Das folgende Beispiel zeigt, wie Sie eine bestimmte Datei **abrufen**.
 

 



```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```

Sie können eine Datei auch **abrufen**, wenn Sie ihre URL kennen, wie im folgenden Beispiel gezeigt.
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
```

Das folgende Beispiel zeigt, wie Sie eine Datei **erstellen** und zu einem Ordner hinzufügen.
 

 



```
url: http://site url/_api/web/GetFolderByServerRelativeUrl('/Folder Name')/Files/add(url='a.txt',overwrite=true)
method: POST
body: "Contents of file"
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    content-length:length of post body
```

Das folgende Beispiel zeigt, wie Sie eine Datei **aktualisieren** und dazu die **PUT**-Methode verwenden.
 

 

 **Hinweis**   **PUT** ist die einzige Methode, die Sie zum Aktualisieren einer Datei verwenden können. Die Methode **MERGE** ist nicht zulässig.
 




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

Wenn Sie die Metadaten einer Datei aktualisieren möchten, müssen Sie einen Endpunkt erstellen, der die Datei als ein Listenelement erreicht. Dies ist möglich, da jeder Ordner auch eine Liste ist, und jede Datei auch ein Listenelement. Erstellen Sie einen Endpunkt, der in etwa so aussieht: `https://<site url>/_api/web/lists/getbytitle('Documents')/items(<item id>)`.  Unter [Working with lists and list items with REST](working-with-lists-and-list-items-with-rest.md) (Arbeiten mit Listen und Listenelementen mit REST) wird erläutert, wie Sie die Metadaten eines Listenelements aktualisieren.
 

 
Sie können eine Datei auschecken, um sicherzustellen, dass niemand sie ändert, bevor Sie sie aktualisieren. Nach der Aktualisierung sollten Sie die Datei wieder einchecken, sodass andere wieder damit arbeiten können. Im folgenden Beispiel wird gezeigt, wie Sie **eine Datei auschecken**.
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckOut(),
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```

Im folgenden Beispiel wird gezeigt, wie Sie **eine Datei einchecken**.
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')/CheckIn(comment='Comment',checkintype=0)
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
```

Das folgende Beispiel zeigt, wie Sie eine Datei **löschen**.
 

 



```
url: http://site url/_api/web/GetFileByServerRelativeUrl('/Folder Name/file name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    IF-MATCH: etag or "*"
    X-HTTP-Method:"DELETE"

```


## <a name="working-with-large-files-by-using-rest"></a>Arbeiten mit großen Dateien unter Verwendung von REST
<a name="LargeFiles"> </a>

Wenn Sie eine Binärdatei hochladen möchten, die größer als 1,5 Megabyte (MB) ist, ist die REST-Schnittstelle die einzige Option. Unter [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md) finden Sie ein Codebeispiel, in dem gezeigt wird, wie Sie eine binäre Datei mit unter 1,5 MB mithilfe des SharePoint Javascript-Objektmodells hochladen. Die maximale Größe einer Binärdatei, die Sie mit REST erstellen können, ist 2 Gigabyte (GB.md). Das folgende Beispiel zeigt, wie Sie eine große Binärdatei **erstellen**.
 

 

 **Vorsicht** Dieser Ansatz funktioniert nur mit Internet Explorer 10 und den neuesten Versionen anderer Browser.
 


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

Im folgenden Codebeispiel wird gezeigt, wie Sie eine Datei mit diesem REST-Endpunkt und der domänenübergreifenden Bibliothek erstellen.
 

 



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


## <a name="working-with-files-attached-to-list-items-by-using-rest"></a>Arbeiten mit an Listenelemente angefügten Dateien mithilfe von REST
<a name="FileAttachments"> </a>

Das folgende Beispiel zeigt, wie Sie alle an ein Listenelement angefügten Dateien **abrufen**.
 

 

```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles/
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

Das folgende Beispiel zeigt, wie Sie eine an ein Listenelement angefügte Datei **abrufen**.
 

 



```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles('file name')/$value
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

Das folgende Beispiel zeigt, wie Sie eine an ein Listenelement angefügte Datei **erstellen**.
 

 



```
url: http://site url/_api/web/lists/getbytitle('list title')/items(item id)/AttachmentFiles/ add(FileName='file name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
    body: "Contents of file."
    X-RequestDigest: form digest value
    content-length:length of post body
```

Das folgende Beispiel zeigt, wie Sie eine an ein Listenelement angefügte Datei **erstellen** und dabei die Methode **PUT** verwenden.
 

 

 **Hinweis**   **PUT** ist die einzige Methode, die Sie zum Aktualisieren einer Datei verwenden können. Die Methode **MERGE** ist nicht zulässig.
 




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


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten](complete-basic-operations-using-sharepoint-rest-endpoints.md)
    
 
-  [Dateien und Ordner – REST-API-Referenz](http://msdn.microsoft.com/library/files-and-folders-rest-api-reference%28Office.15%29.aspx)
    
 
-  [Hochladen von Dateien mithilfe der REST-API und jQuery](upload-a-file-by-using-the-rest-api-and-jquery.md)
    
 
-  [Arbeiten mit Listen und Listenelementen unter Verwendung von REST](working-with-lists-and-list-items-with-rest.md)
    
 
-  [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
    
 
-  [SharePoint: Ausführen grundlegender Datenzugriffsvorgänge für Dateien und Ordner mithilfe von REST](http://code.msdn.microsoft.com/SharePoint-Perform-ab9c4ae5)
    
 
-  [Durchführen von REST-Aufrufen mit C# und JavaScript für SharePoint](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)
    
 
-  [Durchführen von REST-Aufrufen mit C# und JavaScript für SharePoint - Demo](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=b1e7c9c5-0f62-4a78-bb7b-8e283c86145c)
    
 
-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode](complete-basic-operations-using-sharepoint-client-library-code.md)
    
 
-  [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md)
    
 
-  [Entwickeln von SharePoint-Add-ins](develop-sharepoint-add-ins.md)
    
 
-  [Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
    
 
-  [Arbeiten mit externen Daten in SharePoint](work-with-external-data-in-sharepoint.md)
    
 
-  [Open Data Protocol](http://www.odata.org/)
    
 
-  [OData: JSON(JavaScript Object Notation)-Format](http://www.odata.org/documentation/odata-version-2-0/JSON-format/)
    
 

 

 

