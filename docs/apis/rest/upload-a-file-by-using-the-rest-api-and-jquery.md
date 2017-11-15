---
title: Hochladen von Dateien mithilfe der REST-API und jQuery
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 891b9682406188b0c5dff9f07161c1da8ca25739
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="upload-a-file-by-using-the-rest-api-and-jquery"></a>Hochladen von Dateien mithilfe der REST-API und jQuery
Erfahren Sie, wie Sie eine lokale Datei mithilfe der REST-API und jQuery AJAX-Anforderungen in einen SharePoint-Ordner hochladen.
 
In den Codebeispielen in diesem Artikel werden die REST-Schnittstelle und jQuery AJAX-Anforderungen verwendet, um eine lokale Datei zur Bibliothek **Documents** hinzuzufügen und dann die Eigenschaften des Listenelements zu ändern, das die hochgeladene Datei darstellt.
 
Für dieses Verfahren werden die folgenden allgemeinen Schritte verwendet:

1. Konvertieren der lokalen Datei zu einem Array-Puffer mithilfe der API **FileReader**. Dazu musst HTML5 unterstützt werden. Die Funktion **jQuery(document).ready** überprüft im Browser, ob die FileReader-API unterstützt wird.
    
2. Hinzufügen der Datei zum Ordner **Shared Documents** mithilfe der Methode **Add** in der Dateiauflistung des Ordners. Der Array-Puffer wird im Textkörper der POST-Anforderung übergeben.
    
    In diesen Beispielen wird der Endpunkt **getfolderbyserverrelativeurl** verwendet, um die Dateiauflistung zu erreichen. Sie können jedoch auch einen Listenendpunkt verwenden (Beispiel: `…/_api/web/lists/getbytitle('<list title>')/rootfolder/files/add`).
    
3. Abrufen des Listenelements, das der hochgeladenen Datei entspricht, mithilfe der Eigenschaft **ListItemAllFields** der hochgeladenen Datei.

4. Ändern des Anzeigenamens und Titels des Listenelements mithilfe einer MERGE-Anforderung.

## <a name="running-the-code-examples"></a>Ausführen der Codebeispiele
<a name="RunTheExamples"> </a> In beiden Codebeispielen dieses Artikels werden die REST-API und jQuery AJAX-Anforderungen verwendet, um eine Datei in den Ordner **Shared Documents** hochzuladen und dann die Eigenschaften von Listenelementen zu ändern. Im ersten Beispiel wird **SP.AppContextSite** für SharePoint-domänenübergreifende Aufrufe verwendet. Genauso erfolgt dies beim Hochladen von Dateien in das Hostweb durch ein von SharePoint gehostetes Add-In. Im zweiten Beispiel werden Aufrufe in der gleichen Domäne ausgeführt, wie dies beim Hochladen von Dateien in das Add-in-Web durch ein von SharePoint gehostetes Add-in oder beim Hochladen von Dateien durch eine auf dem Server ausgeführte Lösung der Fall wäre.

 **Hinweis**  In JavaScript geschriebene, vom Anbieter gehostete Add-ins müssen die domänenübergreifende Bibliothek „SP.RequestExecutor“ verwenden, um Anforderungen an eine SharePoint-Domäne zu senden. Ein Beispiel finden Sie unter [Upload a file by using the cross-domain library](http://msdn.microsoft.com/library/2c3d2545-1cd7-497e-b535-12199d8edfbb%28Office.15%29.aspx#bk_FileCollectionAdd) (Hochladen einer Datei mithilfe der domänenübergreifenden Bibliothek).
 
Um die Beispiele aus diesem Artikel auszuführen, benötigen Sie Folgendes:
 
- SharePoint Server 2013, 2016 oder SharePoint Online
-  **Schreibberechtigungen** für die Bibliothek **Documents** für den Benutzer, der den Code ausführt. Wenn Sie ein SharePoint-Add-in entwickeln, können Sie **Schreibberechtigungen** für Add-ins für den Bereich der **Liste** angeben.
- Browserunterstützung für die **FileReader**-API (HTML5)
- Einen Verweis auf die jQuery-Bibliothek im Seitenmarkup. Beispiel:
    
```
  <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js" type="text/javascript"></script>
```

- Die folgenden Steuerelemente im Seitenmarkup.
    
```
  <input id="getFile" type="file"/><br />
  <input id="displayName" type="text" value="Enter a unique name" /><br />
  <input id="addFileButton" type="button" value="Upload" onclick="uploadFile()"/>
```


## <a name="code-example-1-upload-a-file-across-sharepoint-domains-by-using-the-rest-api-and-jquery"></a>Codebeispiel 1: SharePoint-domänenübergreifendes Hochladen einer Datei mithilfe der REST-API und jQuery
<a name="RunTheExamples"> </a> Im folgenden Codebeispiel werden die SharePoint REST-API und jQuery AJAX-Anforderungen verwendet, um eine Datei in die Bibliothek **Documents** hochzuladen und die Eigenschaften des Listenelements zu ändern, das die Datei darstellt. Der Kontext für dieses Beispiel ist ein in SharePoint gehostetes Add-in, das eine Datei in einen Ordner im Hostweb hochlädt.
 
Sie müssen [diese Anforderungen](upload-a-file-by-using-the-rest-api-and-jquery.md#RunTheExamples) erfüllen, um das Beispiel verwenden zu können.
 
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


## <a name="code-example-2-upload-a-file-in-the-same-domain-by-using-the-rest-api-and-jquery"></a>Codebeispiel 2: Hochladen von Dateien in der gleichen Domäne mithilfe der REST-API und jQuery
<a name="UploadFile"> </a> Im folgenden Codebeispiel werden die SharePoint REST-API und jQuery AJAX-Anforderungen verwendet, um eine Datei in die Bibliothek **Documents** hochzuladen und die Eigenschaften des Listenelements zu ändern, das die Datei darstellt. Der Kontext für dieses Beispiel ist eine Lösung, die auf dem Server ausgeführt wird. Der Code wäre für ein in SharePoint gehostetes Add-in, das Dateien in das Add-in-Web hochlädt, ähnlich.
 
Sie müssen [diese Anforderungen](upload-a-file-by-using-the-rest-api-and-jquery.md#RunTheExamples) erfüllen, um das Beispiel ausführen zu können.
 
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

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Grundlegendes zum SharePoint REST-Dienst](get-to-know-the-sharepoint-rest-service.md)
-  [Arbeiten mit Ordnern und Dateien unter Verwendung von REST](working-with-folders-and-files-with-rest.md)
-  [Arbeiten mit Listen und Listenelementen unter Verwendung von REST](working-with-lists-and-list-items-with-rest.md)
-  [REST-API-Referenz und Beispiele](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek](../../sp-add-ins/access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md)