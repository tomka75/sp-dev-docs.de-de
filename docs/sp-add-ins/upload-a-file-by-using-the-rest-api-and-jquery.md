
# <a name="upload-a-file-by-using-the-rest-api-and-jquery"></a><span data-ttu-id="385da-101">Hochladen von Dateien mithilfe der REST-API und jQuery</span><span class="sxs-lookup"><span data-stu-id="385da-101">Upload a file by using the REST API and jQuery</span></span>
<span data-ttu-id="385da-102">Erfahren Sie, wie Sie eine lokale Datei mithilfe der REST-API und jQuery AJAX-Anforderungen in einen SharePoint-Ordner hochladen.</span><span class="sxs-lookup"><span data-stu-id="385da-102">Learn how to upload a local file to a SharePoint folder by using the REST API and jQuery AJAX requests.</span></span>
 

 <span data-ttu-id="385da-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="385da-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="385da-106">In den Codebeispielen in diesem Artikel werden die REST-Schnittstelle und jQuery AJAX-Anforderungen verwendet, um eine lokale Datei zur Bibliothek **Documents** hinzuzufügen und dann die Eigenschaften des Listenelements zu ändern, das die hochgeladene Datei darstellt.</span><span class="sxs-lookup"><span data-stu-id="385da-106">The code examples in this article use the REST interface and jQuery AJAX requests to add a local file to the  **Documents** library and then change properties of the list item that represents the uploaded file.</span></span>
 

<span data-ttu-id="385da-107">Für dieses Verfahren werden die folgenden allgemeinen Schritte verwendet:</span><span class="sxs-lookup"><span data-stu-id="385da-107">This process uses the following high-level steps:</span></span>
 


1. <span data-ttu-id="385da-p102">Konvertieren der lokalen Datei zu einem Array-Puffer mithilfe der API **FileReader**. Dazu musst HTML5 unterstützt werden. Die Funktion **jQuery(document).ready** überprüft im Browser, ob die FileReader-API unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="385da-p102">Convert the local file to an array buffer by using the  **FileReader** API, which requires HTML5 support. The **jQuery(document).ready** function checks for FileReader API support in the browser.</span></span>
    
 
2. <span data-ttu-id="385da-p103">Hinzufügen der Datei zum Ordner **Shared Documents** mithilfe der Methode **Add** in der Dateiauflistung des Ordners. Der Array-Puffer wird im Textkörper der POST-Anforderung übergeben.</span><span class="sxs-lookup"><span data-stu-id="385da-p103">Add the file to the  **Shared Documents** folder by using the **Add** method on the folder's file collection. The array buffer is passed in the body of the POST request.</span></span>
    
    <span data-ttu-id="385da-112">In diesen Beispielen wird der Endpunkt **getfolderbyserverrelativeurl** verwendet, um die Dateiauflistung zu erreichen. Sie können jedoch auch einen Listenendpunkt verwenden (Beispiel: `…/_api/web/lists/getbytitle('<list title>')/rootfolder/files/add`).</span><span class="sxs-lookup"><span data-stu-id="385da-112">These examples use the  **getfolderbyserverrelativeurl** endpoint to reach the file collection, but you can also use a list endpoint (example: `…/_api/web/lists/getbytitle('<list title>')/rootfolder/files/add`).</span></span>
    
 
3. <span data-ttu-id="385da-113">Abrufen des Listenelements, das der hochgeladenen Datei entspricht, mithilfe der Eigenschaft **ListItemAllFields** der hochgeladenen Datei.</span><span class="sxs-lookup"><span data-stu-id="385da-113">Get the list item that corresponds to the uploaded file by using the  **ListItemAllFields** property of the uploaded file.</span></span>
    
 
4. <span data-ttu-id="385da-114">Ändern des Anzeigenamens und Titels des Listenelements mithilfe einer MERGE-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="385da-114">Change the display name and title of the list item by using a MERGE request.</span></span>
    
 

## <a name="running-the-code-examples"></a><span data-ttu-id="385da-115">Ausführen der Codebeispiele</span><span class="sxs-lookup"><span data-stu-id="385da-115">Running the code examples</span></span>
<span data-ttu-id="385da-116"><a name="RunTheExamples"> </a></span><span class="sxs-lookup"><span data-stu-id="385da-116"></span></span>

<span data-ttu-id="385da-p104"> In beiden Codebeispielen dieses Artikels werden die REST-API und jQuery AJAX-Anforderungen verwendet, um eine Datei in den Ordner **Shared Documents** hochzuladen und dann die Eigenschaften von Listenelementen zu ändern. Im ersten Beispiel wird **SP.AppContextSite** für SharePoint-domänenübergreifende Aufrufe verwendet. Genauso erfolgt dies beim Hochladen von Dateien in das Hostweb durch ein von SharePoint gehostetes Add-in. Im zweiten Beispiel werden Aufrufe in der gleichen Domäne ausgeführt, wie dies beim Hochladen von Dateien in das Add-in-Web durch ein von SharePoint gehostetes Add-in oder beim Hochladen von Dateien durch eine auf dem Server ausgeführte Lösung der Fall wäre.</span><span class="sxs-lookup"><span data-stu-id="385da-p104">Both code examples in this article use the REST API and jQuery AJAX requests to upload a file to the  **Shared Documents** folder and then change list item properties. The first example uses **SP.AppContextSite** to make calls across SharePoint domains, like a SharePoint-hosted add-in would do when uploading files to the host web. The second example makes same-domain calls, like a SharePoint-hosted add-in would do when uploading files to the add-in web, or a solution that's running on the server would do when uploading files.</span></span>
 

 

 <span data-ttu-id="385da-p105">**Hinweis**  In JavaScript geschriebene, vom Anbieter gehostete Add-ins müssen die domänenübergreifende Bibliothek „SP.RequestExecutor“ verwenden, um Anforderungen an eine SharePoint-Domäne zu senden. Ein Beispiel finden Sie unter [Upload a file by using the cross-domain library](http://msdn.microsoft.com/library/files-and-folders-rest-api-reference%28Office.15%29.aspx#bk_FileCollectionAdd) (Hochladen einer Datei mithilfe der domänenübergreifenden Bibliothek).</span><span class="sxs-lookup"><span data-stu-id="385da-p105">**Note**  Provider-hosted add-ins written in JavaScript must use the SP.RequestExecutor cross-domain library to send requests to a SharePoint domain. For an example, see  [upload a file by using the cross-domain library](http://msdn.microsoft.com/library/files-and-folders-rest-api-reference%28Office.15%29.aspx#bk_FileCollectionAdd).</span></span>
 

<span data-ttu-id="385da-122">Um die Beispiele aus diesem Artikel auszuführen, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="385da-122">To use the examples in this article, you'll need the following:</span></span>
 

 

- <span data-ttu-id="385da-123">SharePoint Server oder SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="385da-123">SharePoint Server 2013 or SharePoint Online</span></span>
    
 
-  <span data-ttu-id="385da-p106">**Schreibberechtigungen** für die Bibliothek **Documents** für den Benutzer, der den Code ausführt. Wenn Sie ein SharePoint-Add-in entwickeln, können Sie **Schreibberechtigungen** für Add-ins für den Bereich der **Liste** angeben.</span><span class="sxs-lookup"><span data-stu-id="385da-p106">**Write** permissions to the **Documents** library for the user running the code. If you're developing a SharePoint Add-in, you can specify **Write** add-in permissions at the **List** scope</span></span>
    
 
- <span data-ttu-id="385da-126">Browserunterstützung für die **FileReader**-API (HTML5)</span><span class="sxs-lookup"><span data-stu-id="385da-126">Browser support for the  **FileReader** API (HTML5)</span></span>
    
 
- <span data-ttu-id="385da-p107">Einen Verweis auf die jQuery-Bibliothek im Seitenmarkup. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="385da-p107">A reference to the jQuery library in your page markup. For example:</span></span>
    
```HTML
  <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js" type="text/javascript"></script>
```

- <span data-ttu-id="385da-129">Die folgenden Steuerelemente im Seitenmarkup.</span><span class="sxs-lookup"><span data-stu-id="385da-129">The following controls in your page markup.</span></span>
    
```HTML
  <input id="getFile" type="file"/><br />
<input id="displayName" type="text" value="Enter a unique name" /><br />
<input id="addFileButton" type="button" value="Upload" onclick="uploadFile()"/>
```


## <a name="code-example-1-upload-a-file-across-sharepoint-domains-by-using-the-rest-api-and-jquery"></a><span data-ttu-id="385da-130">Codebeispiel 1: SharePoint-domänenübergreifendes Hochladen einer Datei mithilfe der REST-API und jQuery</span><span class="sxs-lookup"><span data-stu-id="385da-130">Code example 1: Upload a file across SharePoint domains by using the REST API and jQuery</span></span>
<span data-ttu-id="385da-131"><a name="RunTheExamples"> </a></span><span class="sxs-lookup"><span data-stu-id="385da-131"></span></span>

<span data-ttu-id="385da-p108"> Im folgenden Codebeispiel werden die SharePoint REST-API und jQuery AJAX-Anforderungen verwendet, um eine Datei in die Bibliothek **Documents** hochzuladen und die Eigenschaften des Listenelements zu ändern, das die Datei darstellt. Der Kontext für dieses Beispiel ist ein in SharePoint gehostetes Add-in, das eine Datei in einen Ordner im Hostweb hochlädt.</span><span class="sxs-lookup"><span data-stu-id="385da-p108">The following code example uses the SharePoint REST API and jQuery AJAX requests to upload a file to the  **Documents** library and to change properties of the list item that represents the file. The context for this example is a SharePoint-hosted add-in that uploads a file to a folder on the host web.</span></span>
 

 
<span data-ttu-id="385da-134">Sie müssen [diese Anforderungen](upload-a-file-by-using-the-rest-api-and-jquery#RunTheExamples) erfüllen, um das Beispiel verwenden zu können.</span><span class="sxs-lookup"><span data-stu-id="385da-134">You need to meet  [these requirements](upload-a-file-by-using-the-rest-api-and-jquery#RunTheExamples) to use this example.</span></span>
 

 



```javascript
'use strict';

var appWebUrl, hostWebUrl;

jQuery(document).ready(function () {

    // Check for FileReader API (HTML5) support.
    if (!window.FileReader) {
        alert('This browser does not support the FileReader API.');
    }

    // Get the add-in web and host web URLs.
    appWebUrl = decodeURIComponent(getQueryStringParameter("SPAppWebUrl"));
    hostWebUrl = decodeURIComponent(getQueryStringParameter("SPHostUrl"));
});

// Upload the file.
// You can upload files up to 2 GB with the REST API.
function uploadFile() {

    // Define the folder path for this example.
    var serverRelativeUrlToFolder = '/shared documents';

    // Get test values from the file input and text input page controls.
    // The display name must be unique every time you run the example.
    var fileInput = jQuery('#getFile');
    var newName = jQuery('#displayName').val();

    // Initiate method calls using jQuery promises.
    // Get the local file as an array buffer.
    var getFile = getFileBuffer();
    getFile.done(function (arrayBuffer) {

        // Add the file to the SharePoint folder.
        var addFile = addFileToFolder(arrayBuffer);
        addFile.done(function (file, status, xhr) {

            // Get the list item that corresponds to the uploaded file.
            var getItem = getListItem(file.d.ListItemAllFields.__deferred.uri);
            getItem.done(function (listItem, status, xhr) {

                // Change the display name and title of the list item.
                var changeItem = updateListItem(listItem.d.__metadata);
                changeItem.done(function (data, status, xhr) {
                    alert('file uploaded and updated');
                });
                changeItem.fail(onError);
            });
            getItem.fail(onError);
        });
        addFile.fail(onError);
    });
    getFile.fail(onError);

    // Get the local file as an array buffer.
    function getFileBuffer() {
        var deferred = jQuery.Deferred();
        var reader = new FileReader();
        reader.onloadend = function (e) {
            deferred.resolve(e.target.result);
        }
        reader.onerror = function (e) {
            deferred.reject(e.target.error);
        }
        reader.readAsArrayBuffer(fileInput[0].files[0]);
        return deferred.promise();
    }

    // Add the file to the file collection in the Shared Documents folder.
    function addFileToFolder(arrayBuffer) {

        // Get the file name from the file input control on the page.
        var parts = fileInput[0].value.split('\\');
        var fileName = parts[parts.length - 1];

        // Construct the endpoint.
        var fileCollectionEndpoint = String.format(
            "{0}/_api/sp.appcontextsite(@target)/web/getfolderbyserverrelativeurl('{1}')/files" +
            "/add(overwrite=true, url='{2}')?@target='{3}'",
            appWebUrl, serverRelativeUrlToFolder, fileName, hostWebUrl);

        // Send the request and return the response.
        // This call returns the SharePoint file.
        return jQuery.ajax({
            url: fileCollectionEndpoint,
            type: "POST",
            data: arrayBuffer,
            processData: false,
            headers: {
                "accept": "application/json;odata=verbose",
                "X-RequestDigest": jQuery("#__REQUESTDIGEST").val(),
                "content-length": arrayBuffer.byteLength
            }
        });
    }

    // Get the list item that corresponds to the file by calling the file's ListItemAllFields property.
    function getListItem(fileListItemUri) {

        // Construct the endpoint.
        // The list item URI uses the host web, but the cross-domain call is sent to the
        // add-in web and specifies the host web as the context site.
        fileListItemUri = fileListItemUri.replace(hostWebUrl, '{0}');
        fileListItemUri = fileListItemUri.replace('_api/Web', '_api/sp.appcontextsite(@target)/web');
        
        var listItemAllFieldsEndpoint = String.format(fileListItemUri + "?@target='{1}'",
            appWebUrl, hostWebUrl);

        // Send the request and return the response.
        return jQuery.ajax({
            url: listItemAllFieldsEndpoint,
            type: "GET",
            headers: { "accept": "application/json;odata=verbose" }
        });
    }

    // Change the display name and title of the list item.
    function updateListItem(itemMetadata) {

        // Construct the endpoint.
        // Specify the host web as the context site.
        var listItemUri = itemMetadata.uri.replace('_api/Web', '_api/sp.appcontextsite(@target)/web');
        var listItemEndpoint = String.format(listItemUri + "?@target='{0}'", hostWebUrl);

        // Define the list item changes. Use the FileLeafRef property to change the display name. 
        // For simplicity, also use the name as the title.
        // The example gets the list item type from the item's metadata, but you can also get it from the
        // ListItemEntityTypeFullName property of the list.
        var body = String.format("{{'__metadata':{{'type':'{0}'}},'FileLeafRef':'{1}','Title':'{2}'}}",
            itemMetadata.type, newName, newName);

        // Send the request and return the promise.
        // This call does not return response content from the server.
        return jQuery.ajax({
            url: listItemEndpoint,
            type: "POST",
            data: body,
            headers: {
                "X-RequestDigest": jQuery("#__REQUESTDIGEST").val(),
                "content-type": "application/json;odata=verbose",
                "content-length": body.length,
                "IF-MATCH": itemMetadata.etag,
                "X-HTTP-Method": "MERGE"
            }
        });
    }
}

// Display error messages. 
function onError(error) {
    alert(error.responseText);
}

// Get parameters from the query string.
// For production purposes you may want to use a library to handle the query string.
function getQueryStringParameter(paramToRetrieve) {
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var singleParam = params[i].split("=");
        if (singleParam[0] == paramToRetrieve) return singleParam[1];
    }
}
```


## <a name="code-example-2-upload-a-file-in-the-same-domain-by-using-the-rest-api-and-jquery"></a><span data-ttu-id="385da-135">Codebeispiel 2: Hochladen von Dateien in der gleichen Domäne mithilfe der REST-API und jQuery</span><span class="sxs-lookup"><span data-stu-id="385da-135">Code example 2: Upload a file in the same domain by using the REST API and jQuery</span></span>
<span data-ttu-id="385da-136"><a name="UploadFile"> </a></span><span class="sxs-lookup"><span data-stu-id="385da-136"></span></span>

<span data-ttu-id="385da-p109"> Im folgenden Codebeispiel werden die SharePoint REST-API und jQuery AJAX-Anforderungen verwendet, um eine Datei in die Bibliothek **Documents** hochzuladen und die Eigenschaften des Listenelements zu ändern, das die Datei darstellt. Der Kontext für dieses Beispiel ist eine Lösung, die auf dem Server ausgeführt wird. Der Code wäre für ein in SharePoint gehostetes Add-in, das Dateien in das Add-in-Web hochlädt, ähnlich.</span><span class="sxs-lookup"><span data-stu-id="385da-p109">The following code example uses the SharePoint REST API and jQuery AJAX requests to upload a file to the  **Documents** library and to change properties of the list item that represents the file. The context for this example is a solution that's running on the server. The code would be similar in a SharePoint-hosted add-in that uploads files to the add-in web.</span></span>
 

 
<span data-ttu-id="385da-140">Sie müssen [diese Anforderungen](upload-a-file-by-using-the-rest-api-and-jquery#RunTheExamples) erfüllen, um das Beispiel ausführen zu können.</span><span class="sxs-lookup"><span data-stu-id="385da-140">You need to meet  [these requirements](upload-a-file-by-using-the-rest-api-and-jquery#RunTheExamples) before you can run this example.</span></span>
 

 



```javascript
'use strict';

jQuery(document).ready(function () {

    // Check for FileReader API (HTML5) support.
    if (!window.FileReader) {
        alert('This browser does not support the FileReader API.');
    }
});

// Upload the file.
// You can upload files up to 2 GB with the REST API.
function uploadFile() {

    // Define the folder path for this example.
    var serverRelativeUrlToFolder = '/shared documents';

    // Get test values from the file input and text input page controls.
    var fileInput = jQuery('#getFile');
    var newName = jQuery('#displayName').val();

    // Get the server URL.
    var serverUrl = _spPageContextInfo.webAbsoluteUrl;

    // Initiate method calls using jQuery promises.
    // Get the local file as an array buffer.
    var getFile = getFileBuffer();
    getFile.done(function (arrayBuffer) {

        // Add the file to the SharePoint folder.
        var addFile = addFileToFolder(arrayBuffer);
        addFile.done(function (file, status, xhr) {

            // Get the list item that corresponds to the uploaded file.
            var getItem = getListItem(file.d.ListItemAllFields.__deferred.uri);
            getItem.done(function (listItem, status, xhr) {

                // Change the display name and title of the list item.
                var changeItem = updateListItem(listItem.d.__metadata);
                changeItem.done(function (data, status, xhr) {
                    alert('file uploaded and updated');
                });
                changeItem.fail(onError);
            });
            getItem.fail(onError);
        });
        addFile.fail(onError);
    });
    getFile.fail(onError);

    // Get the local file as an array buffer.
    function getFileBuffer() {
        var deferred = jQuery.Deferred();
        var reader = new FileReader();
        reader.onloadend = function (e) {
            deferred.resolve(e.target.result);
        }
        reader.onerror = function (e) {
            deferred.reject(e.target.error);
        }
        reader.readAsArrayBuffer(fileInput[0].files[0]);
        return deferred.promise();
    }

    // Add the file to the file collection in the Shared Documents folder.
    function addFileToFolder(arrayBuffer) {

        // Get the file name from the file input control on the page.
        var parts = fileInput[0].value.split('\\');
        var fileName = parts[parts.length - 1];

        // Construct the endpoint.
        var fileCollectionEndpoint = String.format(
                "{0}/_api/web/getfolderbyserverrelativeurl('{1}')/files" +
                "/add(overwrite=true, url='{2}')",
                serverUrl, serverRelativeUrlToFolder, fileName);

        // Send the request and return the response.
        // This call returns the SharePoint file.
        return jQuery.ajax({
            url: fileCollectionEndpoint,
            type: "POST",
            data: arrayBuffer,
            processData: false,
            headers: {
                "accept": "application/json;odata=verbose",
                "X-RequestDigest": jQuery("#__REQUESTDIGEST").val(),
                "content-length": arrayBuffer.byteLength
            }
        });
    }

    // Get the list item that corresponds to the file by calling the file's ListItemAllFields property.
    function getListItem(fileListItemUri) {

        // Send the request and return the response.
        return jQuery.ajax({
            url: fileListItemUri,
            type: "GET",
            headers: { "accept": "application/json;odata=verbose" }
        });
    }

    // Change the display name and title of the list item.
    function updateListItem(itemMetadata) {

        // Define the list item changes. Use the FileLeafRef property to change the display name. 
        // For simplicity, also use the name as the title. 
        // The example gets the list item type from the item's metadata, but you can also get it from the
        // ListItemEntityTypeFullName property of the list.
        var body = String.format("{{'__metadata':{{'type':'{0}'}},'FileLeafRef':'{1}','Title':'{2}'}}",
            itemMetadata.type, newName, newName);

        // Send the request and return the promise.
        // This call does not return response content from the server.
        return jQuery.ajax({
            url: itemMetadata.uri,
            type: "POST",
            data: body,
            headers: {
                "X-RequestDigest": jQuery("#__REQUESTDIGEST").val(),
                "content-type": "application/json;odata=verbose",
                "content-length": body.length,
                "IF-MATCH": itemMetadata.etag,
                "X-HTTP-Method": "MERGE"
            }
        });
    }
}

// Display error messages. 
function onError(error) {
    alert(error.responseText);
}
```


## <a name="additional-resources"></a><span data-ttu-id="385da-141">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="385da-141">Additional resources</span></span>
<span data-ttu-id="385da-142"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="385da-142"></span></span>


-  [<span data-ttu-id="385da-143">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="385da-143">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-2013-rest-service)
    
 
-  [<span data-ttu-id="385da-144">Arbeiten mit Ordnern und Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="385da-144">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest)
    
 
-  [<span data-ttu-id="385da-145">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="385da-145">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest)
    
 
-  [<span data-ttu-id="385da-146">REST-API-Referenz und Beispiele</span><span class="sxs-lookup"><span data-stu-id="385da-146">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="385da-147">Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek</span><span class="sxs-lookup"><span data-stu-id="385da-147">Access SharePoint data from add-ins using the cross-domain library</span></span>](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library)
    
 

