<span data-ttu-id="dbbef-p107"><a name="bk_folders"> </a> Der SharePoint REST-Dienst bietet keine Unterstützung für das Durchsuchen der Ordnerhierarchie einer Website über die URL-Konstruktion. Verwenden Sie stattdessen das REST-Äquivalent der Methode **Web.GetFolderByServerRelativeUrl**. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="dbbef-p107"><a name="bk_folders"> </a> The SharePoint REST service does not support traversing the folder hierarchy of a site through the URL construction. Instead, use the REST equivalent of the  **Web.GetFolderByServerRelativeUrl** method. For example:</span></span>
<a name="bk_folders"> </a> Der SharePoint REST-Dienst bietet keine Unterstützung für das Durchsuchen der Ordnerhierarchie einer Website über die URL-Konstruktion. Verwenden Sie stattdessen das REST-Äquivalent der Methode **Web.GetFolderByServerRelativeUrl**. Beispiel:
 
 <span data-ttu-id="dbbef-137">*Durch den REST-Dienst nicht unterstützte Navigation:*</span><span class="sxs-lookup"><span data-stu-id="dbbef-137">*Navigation not supported through the REST service:*</span></span> 
  
 `/_vti_bin/client.svc/web/lists/SharedDocuments/folder1/stuff/things/Recycle`
 
<span data-ttu-id="dbbef-138">Durch den REST-Dienst unterstützte Navigation:</span><span class="sxs-lookup"><span data-stu-id="dbbef-138">Navigation that is supported by the REST service:</span></span> 
 
 <span data-ttu-id="dbbef-139">`/_vti_bin/client.svc/web/GetFolderByServerRelativeUrl('SharedDocuments/folder1/stuff/things')/Recycle`.</span><span class="sxs-lookup"><span data-stu-id="dbbef-139"></span></span>
 

## <a name="spcontextwebinformation-object-properties"></a><span data-ttu-id="dbbef-140">SPContextWebInformation-Objekteigenschaften</span><span class="sxs-lookup"><span data-stu-id="dbbef-140">SPContextWebInformation object properties</span></span>
<span data-ttu-id="dbbef-141"><a name="bk_props"> </a></span><span class="sxs-lookup"><span data-stu-id="dbbef-141"></span></span>

|<span data-ttu-id="dbbef-142">**Eigenschaft SPContextWebInformation**</span><span class="sxs-lookup"><span data-stu-id="dbbef-142">**SPContextWebInformation Property**</span></span>|<span data-ttu-id="dbbef-143">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dbbef-143">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dbbef-144">**webFullUrl**</span><span class="sxs-lookup"><span data-stu-id="dbbef-144">**webFullUrl**</span></span>|<span data-ttu-id="dbbef-145">Ruft die serverrelative URL der nächstgelegenen Website ab.</span><span class="sxs-lookup"><span data-stu-id="dbbef-145">Gets the server-relative URL of the nearest site.</span></span>|
|<span data-ttu-id="dbbef-146">**siteFullUrl**</span><span class="sxs-lookup"><span data-stu-id="dbbef-146">**siteFullUrl**</span></span>|<span data-ttu-id="dbbef-147">Ruft die serverrelative URL des Stamms der Websitesammlung ab, in der die Website enthalten ist. Wenn der Stamm einer Websitesammlung am nächsten gelegen ist, dann entspricht der Wert der Eigenschaft **webFullUrl** der Eigenschaft **siteFullUrl**.</span><span class="sxs-lookup"><span data-stu-id="dbbef-147">Gets the server-relative URL of the root of the site collection that the site is contained within.If the nearest web is the root of a site collection, then the value of the  **webFullUrl** property is equal to the **siteFullUrl** property.</span></span>|
|<span data-ttu-id="dbbef-148">**formDigestValue**</span><span class="sxs-lookup"><span data-stu-id="dbbef-148">**formDigestValue**</span></span>|<span data-ttu-id="dbbef-149">Ruft den Formulardigest der Serveranforderung ab.</span><span class="sxs-lookup"><span data-stu-id="dbbef-149">Gets the server's request form digest.</span></span>|
|<span data-ttu-id="dbbef-150">**LibraryVersion**</span><span class="sxs-lookup"><span data-stu-id="dbbef-150">**LibraryVersion**</span></span>|<span data-ttu-id="dbbef-151">Ruft die aktuelle Version der REST-Bibliothek ab.</span><span class="sxs-lookup"><span data-stu-id="dbbef-151">Gets the current version of the REST library.</span></span>|
|<span data-ttu-id="dbbef-152">**SupportedSchemaVersions**</span><span class="sxs-lookup"><span data-stu-id="dbbef-152">**SupportedSchemaVersions**</span></span>|<span data-ttu-id="dbbef-153">Ruft die Versionen des Schemas der REST-/CSOM-Bibliothek ab, die unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="dbbef-153">Gets the versions of the schema of the REST/CSOM library that are supported.</span></span>|

## <a name="webinfo-object"></a><span data-ttu-id="dbbef-154">WebInfo-Objekt</span><span class="sxs-lookup"><span data-stu-id="dbbef-154">WebInfo object</span></span>
<span data-ttu-id="dbbef-155"><a name="bk_webinfo"> </a></span><span class="sxs-lookup"><span data-stu-id="dbbef-155"></span></span>

|<span data-ttu-id="dbbef-156">**WebInfo-Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="dbbef-156">**WebInfo property**</span></span>|<span data-ttu-id="dbbef-157">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dbbef-157">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dbbef-158">**Created**</span><span class="sxs-lookup"><span data-stu-id="dbbef-158">**Created**</span></span>|<span data-ttu-id="dbbef-159">Ruft einen Wert ab, der angibt, wann die Website erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="dbbef-159">Gets a value that specifies when the site was created.</span></span>|
|<span data-ttu-id="dbbef-160">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dbbef-160">**Description**</span></span>|<span data-ttu-id="dbbef-161">Dient zum Abrufen oder Festlegen der Beschreibung der Website.</span><span class="sxs-lookup"><span data-stu-id="dbbef-161">Gets or sets the description for the site.</span></span>|
|<span data-ttu-id="dbbef-162">**Id**</span><span class="sxs-lookup"><span data-stu-id="dbbef-162">**Id**</span></span>|<span data-ttu-id="dbbef-163">Ruft einen Wert ab, der den Websitebezeichner angibt.</span><span class="sxs-lookup"><span data-stu-id="dbbef-163">Gets a value that specifies the site identifier.</span></span>|
|<span data-ttu-id="dbbef-164">**Language**</span><span class="sxs-lookup"><span data-stu-id="dbbef-164">**Language**</span></span>|<span data-ttu-id="dbbef-165">Ruft einen Wert ab, der die Gebietsschema-ID (LCID) für die Sprache angibt, die auf der Website verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="dbbef-165">Gets a value that specifies the locale ID (LCID) for the language that is used on the site.</span></span>|
|<span data-ttu-id="dbbef-166">**LastItemModifiedDate**</span><span class="sxs-lookup"><span data-stu-id="dbbef-166">**lastItemModifiedDate**</span></span>|<span data-ttu-id="dbbef-167">Ruft einen Wert ab, der angibt, wann ein Element in der Website zuletzt geändert wurde.</span><span class="sxs-lookup"><span data-stu-id="dbbef-167">Gets a value that specifies when an item was last modified in the site.</span></span>|
|<span data-ttu-id="dbbef-168">**Title**</span><span class="sxs-lookup"><span data-stu-id="dbbef-168">**Title**</span></span>|<span data-ttu-id="dbbef-169">Dient zum Abrufen oder Festlegen des Titels der Website.</span><span class="sxs-lookup"><span data-stu-id="dbbef-169">Gets or sets the title for the site.</span></span>|
|<span data-ttu-id="dbbef-170">**WebTemplateId**</span><span class="sxs-lookup"><span data-stu-id="dbbef-170">**WebTemplateId**</span></span>|<span data-ttu-id="dbbef-171">Ruft den Bezeichner der Websitevorlage ab.</span><span class="sxs-lookup"><span data-stu-id="dbbef-171">Gets the identifier of the site template.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="dbbef-172">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="dbbef-172">Additional resources</span></span>
<span data-ttu-id="dbbef-173"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="dbbef-173"></span></span>

-  [<span data-ttu-id="dbbef-174">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="dbbef-174">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
-  [<span data-ttu-id="dbbef-175">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="dbbef-175">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [<span data-ttu-id="dbbef-176">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="dbbef-176">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
-  [<span data-ttu-id="dbbef-177">Arbeiten mit Ordnern und Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="dbbef-177">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest.md)
-  [<span data-ttu-id="dbbef-178">Ermitteln von URIs von SharePoint REST-Dienstendpunkten</span><span class="sxs-lookup"><span data-stu-id="dbbef-178">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris.md)
-  [<span data-ttu-id="dbbef-179">Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="dbbef-179">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests.md)
-  [<span data-ttu-id="dbbef-180">REST-API-Referenz und Beispiele</span><span class="sxs-lookup"><span data-stu-id="dbbef-180">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [<span data-ttu-id="dbbef-181">Synchronisieren von SharePoint-Elementen mit dem REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="dbbef-181">Synchronize SharePoint items using the REST service</span></span>](synchronize-sharepoint-items-using-the-rest-service.md)
-  [<span data-ttu-id="dbbef-182">Verwenden von ETag-Werten zum Bestimmen der Version von Dokument- und Listenelementen über den REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="dbbef-182">Use ETag values through the REST service to get document list item versioning</span></span>](http://msdn.microsoft.com/library/use-etag-values-through-the-rest-service-to-get-document-list-item-versioning%28Office.15%29.aspx)
    
 

 

 

