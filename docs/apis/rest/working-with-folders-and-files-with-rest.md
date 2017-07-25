<span data-ttu-id="aa0f1-p107">**Hinweis**   **PUT** ist die einzige Methode, die Sie zum Aktualisieren einer Datei verwenden können. Die Methode **MERGE** ist nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="aa0f1-p107">**Note**   **PUT** is the only method that you can use to update a file. The **MERGE** method is not allowed.</span></span>

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
## <a name="additional-resources"></a><span data-ttu-id="aa0f1-143">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="aa0f1-143">Additional resources</span></span>
<span data-ttu-id="aa0f1-144"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="aa0f1-144"></span></span>

-  [<span data-ttu-id="aa0f1-145">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="aa0f1-145">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [<span data-ttu-id="aa0f1-146">Dateien und Ordner – REST-API-Referenz</span><span class="sxs-lookup"><span data-stu-id="aa0f1-146">Files and folders REST API reference</span></span>](http://msdn.microsoft.com/library/2c3d2545-1cd7-497e-b535-12199d8edfbb%28Office.15%29.aspx)
-  [<span data-ttu-id="aa0f1-147">Hochladen von Dateien mithilfe der REST-API und jQuery</span><span class="sxs-lookup"><span data-stu-id="aa0f1-147">Upload a file by using the REST API and jQuery</span></span>](upload-a-file-by-using-the-rest-api-and-jquery.md)
-  [<span data-ttu-id="aa0f1-148">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="aa0f1-148">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
-  [<span data-ttu-id="aa0f1-149">SharePoint-Add-in-REST-OData-BasicDataOperations</span><span class="sxs-lookup"><span data-stu-id="aa0f1-149">SharePoint-Add-in-REST-OData-BasicDataOperations</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
-  [<span data-ttu-id="aa0f1-150">SharePoint 2013: Ausführen grundlegender Datenzugriffsvorgänge für Dateien und Ordner mithilfe von REST</span><span class="sxs-lookup"><span data-stu-id="aa0f1-150">SharePoint 2013: Perform basic data access operations on files and folders by using REST</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Perform-ab9c4ae5)
-  [<span data-ttu-id="aa0f1-151">Durchführen von REST-Aufrufen mit C# und JavaScript für SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="aa0f1-151">Making REST calls with C# and JavaScript for SharePoint 2013</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/video.mdl?cid=sdc&amp;from=mscomsdc&amp;VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)
-  [<span data-ttu-id="aa0f1-152">Durchführen von REST-Aufrufen mit C# und JavaScript für SharePoint 2013 Demo</span><span class="sxs-lookup"><span data-stu-id="aa0f1-152">Making REST calls with C# and JavaScript for SharePoint 2013 demo</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/video.mdl?cid=sdc&amp;from=mscomsdc&amp;VideoID=b1e7c9c5-0f62-4a78-bb7b-8e283c86145c)
-  [<span data-ttu-id="aa0f1-153">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint 2013-Clientbibliothekscode</span><span class="sxs-lookup"><span data-stu-id="aa0f1-153">Complete basic operations using SharePoint 2013 client library code</span></span>](complete-basic-operations-using-sharepoint-2013-client-library-code.md)
-  [<span data-ttu-id="aa0f1-154">Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="aa0f1-154">Complete basic operations using JavaScript library code in SharePoint 2013</span></span>](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013.md)
-  [<span data-ttu-id="aa0f1-155">Entwickeln von SharePoint-Add-ins</span><span class="sxs-lookup"><span data-stu-id="aa0f1-155">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
-  [<span data-ttu-id="aa0f1-156">Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="aa0f1-156">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
-  [<span data-ttu-id="aa0f1-157">Arbeiten mit externen Daten in SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="aa0f1-157">Work with external data in SharePoint 2013</span></span>](work-with-external-data-in-sharepoint-2013.md)
-  [<span data-ttu-id="aa0f1-158">Open Data Protocol</span><span class="sxs-lookup"><span data-stu-id="aa0f1-158">Open Data Protocol</span></span>](http://www.odata.org/)
-  [<span data-ttu-id="aa0f1-159">OData: JSON(JavaScript Object Notation)-Format</span><span class="sxs-lookup"><span data-stu-id="aa0f1-159">OData: JavaScript Object Notation (JSON) Format</span></span>](http://www.odata.org/documentation/odata-version-2-0/JSON-format/)
