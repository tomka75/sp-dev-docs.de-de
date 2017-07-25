<span data-ttu-id="01373-p108"><a name="UploadFile"> </a> Im folgenden Codebeispiel werden die SharePoint REST-API und jQuery AJAX-Anforderungen verwendet, um eine Datei in die Bibliothek **Documents** hochzuladen und die Eigenschaften des Listenelements zu ändern, das die Datei darstellt. Der Kontext für dieses Beispiel ist eine Lösung, die auf dem Server ausgeführt wird. Der Code wäre für ein in SharePoint gehostetes Add-in, das Dateien in das Add-in-Web hochlädt, ähnlich.</span><span class="sxs-lookup"><span data-stu-id="01373-p108"><a name="UploadFile"> </a> The following code example uses the SharePoint REST API and jQuery AJAX requests to upload a file to the  **Documents** library and to change properties of the list item that represents the file. The context for this example is a solution that's running on the server. The code would be similar in a SharePoint-hosted add-in that uploads files to the add-in web.</span></span>
<a name="UploadFile"> </a> Im folgenden Codebeispiel werden die SharePoint REST-API und jQuery AJAX-Anforderungen verwendet, um eine Datei in die Bibliothek **Documents** hochzuladen und die Eigenschaften des Listenelements zu ändern, das die Datei darstellt. Der Kontext für dieses Beispiel ist eine Lösung, die auf dem Server ausgeführt wird. Der Code wäre für ein in SharePoint gehostetes Add-in, das Dateien in das Add-in-Web hochlädt, ähnlich.
 
<span data-ttu-id="01373-134">Sie müssen [diese Anforderungen](upload-a-file-by-using-the-rest-api-and-jquery.md#RunTheExamples) erfüllen, um das Beispiel ausführen zu können.</span><span class="sxs-lookup"><span data-stu-id="01373-134">You need to meet  [these requirements](upload-a-file-by-using-the-rest-api-and-jquery.md#RunTheExamples) before you can run this example.</span></span>
 
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

## <a name="additional-resources"></a><span data-ttu-id="01373-135">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="01373-135">Additional resources</span></span>
<span data-ttu-id="01373-136"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="01373-136"></span></span>

-  [<span data-ttu-id="01373-137">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="01373-137">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
-  [<span data-ttu-id="01373-138">Arbeiten mit Ordnern und Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="01373-138">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest.md)
-  [<span data-ttu-id="01373-139">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="01373-139">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
-  [<span data-ttu-id="01373-140">REST-API-Referenz und Beispiele</span><span class="sxs-lookup"><span data-stu-id="01373-140">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [<span data-ttu-id="01373-141">Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek</span><span class="sxs-lookup"><span data-stu-id="01373-141">Access SharePoint data from add-ins using the cross-domain library</span></span>](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library.md)