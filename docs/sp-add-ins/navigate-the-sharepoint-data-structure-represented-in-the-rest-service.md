
# <a name="navigate-the-sharepoint-data-structure-represented-in-the-rest-service"></a><span data-ttu-id="fa409-101">Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur</span><span class="sxs-lookup"><span data-stu-id="fa409-101">Navigate the SharePoint data structure represented in the REST service</span></span>
<span data-ttu-id="fa409-102">Informationen zum Starten von einem REST-Endpunkt für einen gegebenen SharePoint-Element und Navigieren zu und Zugreifen auf dazugehörige Elemente, z. B. übergeordnete Standorte oder die Bibliotheksstruktur, in der sich das jeweilige Element befindet.</span><span class="sxs-lookup"><span data-stu-id="fa409-102">Learn how to start from a REST endpoint for a given SharePoint item, and navigate to and access related items, such as parent sites or the library structure where that item resides.</span></span> 
 

 <span data-ttu-id="fa409-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="fa409-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="navigate-from-a-given-url-to-reach-other-sharepoint-resources"></a><span data-ttu-id="fa409-106">Navigieren von einer bestimmten URL zu anderen SharePoint-Ressourcen</span><span class="sxs-lookup"><span data-stu-id="fa409-106">Navigate from a given URL to reach other SharePoint resources</span></span>

<span data-ttu-id="fa409-p102">Wenn Sie mit dem SharePoint REST-Dienst arbeiten, kennen Sie häufig die URL eines bestimmten SharePoint-Elements, möchten aber auf dazugehörige Elemente zugreifen, z. B. den Ordner oder die Bibliotheksstruktur, in dem/der sich das jeweilige Element befindet. Angenommen, Sie erstellen ein Add-In, bei dem die Benutzer die URL eines Dokuments in eine SharePoint-Bibliothek eingeben. Ihr Add-In muss dann die URL aufgliedern, um die tatsächliche URL der SharePoint-Website zu bestimmen. Anschließend kann das Add-In im Auftrag des Benutzers weitere Anforderungen an die Website stellen, z. B. zum Erstellen, Aktualisieren oder Löschen verwandter Elemente oder Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="fa409-p102">When you're working with the SharePoint REST service, you'll often start out knowing the URL of a specific SharePoint item, but want to access related items, such as the folder or library structure where that item resides. For example, suppose you create an add-in where your user enters the URL of a document in a SharePoint library. Your add-in must then break down that URL to figure out the actual SharePoint site URL. Once it's done that, the add-in can then make more requests from the site on the user's behalf, such as to create, update, or delete related items or resources.</span></span> 
 

 
<span data-ttu-id="fa409-111">Zu diesem Zweck muss das Add-in folgende Informationen von SharePoint abfragen:</span><span class="sxs-lookup"><span data-stu-id="fa409-111">To do this, your add-in needs to query SharePoint for the following information:</span></span>
 

 

- <span data-ttu-id="fa409-112">Die serverrelativen URLs der Website und die Websitesammlung, die die Ressource enthält</span><span class="sxs-lookup"><span data-stu-id="fa409-112">The server relative URLs of the site and site collection containing the resource</span></span>
    
 
- <span data-ttu-id="fa409-113">Ein Formulardigest, mit dem Sie Abfragen ausführen können, die den Status der Ressource ändern. Beispiel:  **POST**,  **PUT**,  **MERGE** und  **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="fa409-113">A form digest to enable you to perform requests that change the state of the resource, such as  **POST**,  **PUT**,  **MERGE**, and  **DELETE**</span></span>
    
 
<span data-ttu-id="fa409-114">Das grundlegende Verfahren:</span><span class="sxs-lookup"><span data-stu-id="fa409-114">The basic process:</span></span>
 

 

1. <span data-ttu-id="fa409-p103">Verwenden Sie den Operator `/contextinfo` mit der angegebenen URL, um auf die Adressen der Website und der Websitesammlung und den Formulardigest zuzugreifen. Verwenden Sie den Operator `/contextinfo` in folgendem Format:</span><span class="sxs-lookup"><span data-stu-id="fa409-p103">Use the  `/contextinfo` operator with the given URL to access the site and site collection addresses, and the form digest. Use the `/contextinfo` operator in the following format:</span></span>
    
     `http://server/web/doclib/forms/_api/contextinfo`
    
    <span data-ttu-id="fa409-117">Zur Verbesserung der Sicherheit gegenüber websiteübergreifenden Scriptingversuchen akzeptiert der `/contextinfo`-Operator nur **POST**-Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="fa409-117">To increase security against cross-site scripting attempts, the  `/contextinfo` operator accepts only **POST** requests.</span></span>
    
 
2. <span data-ttu-id="fa409-118">Verwenden Sie für den Zugriff auf zusätzliche Ressourcen bei Bedarf die Objekteigenschaften [SPContextWebInformation](#bk_props), die der `/contextinfo`-Operator zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="fa409-118">Use the  [SPContextWebInformation object properties](#bk_props) that the `/contextinfo` operator returns to access additional resources as desired.</span></span>
    
 
 <span data-ttu-id="fa409-119">**Verwenden**</span><span class="sxs-lookup"><span data-stu-id="fa409-119">**Try it**</span></span>
 

 

1. <span data-ttu-id="fa409-p104">Beginnen Sie mit einer URL zu einem SharePoint-Element. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="fa409-p104">Start with a URL to a given SharePoint item. For example:</span></span>
    
     `http://site/web/doclib/myDocument.docx`
    
 
2. <span data-ttu-id="fa409-p105">Entfernen Sie den Namen der spezifischen Ressource vom Ende der URL, damit die URL auf eine Dokumentbibliothek, einen Ordner oder eine Liste verweist. In diesem Fall:</span><span class="sxs-lookup"><span data-stu-id="fa409-p105">Remove the name of the specific resource from the end of the URL, so that the URL points to a document library, folder, or list. IN this case:</span></span>
    
     `http://site/web/doclib/`
    
 
3. <span data-ttu-id="fa409-124">Fügen Sie den Zeiger des REST-Dienstes und den `/contextinfo`-Operator an die URL an:</span><span class="sxs-lookup"><span data-stu-id="fa409-124">Append the REST service pointer and the  `/contextinfo` operator to the URL:</span></span>
    
     `http://site/web/doclib/_api/contextinfo`
    
 
4. <span data-ttu-id="fa409-125">Lesen Sie den Formulardigest und die Eigenschaften **WebFullUrl** aus der Antwort aus.</span><span class="sxs-lookup"><span data-stu-id="fa409-125">Read the form digest and  **webFullUrl** properties from the response.</span></span>
    
 
5. <span data-ttu-id="fa409-126">Fügen Sie den Zeiger des REST-Dienstes `_api` an die Web-URL an:</span><span class="sxs-lookup"><span data-stu-id="fa409-126">Append the REST service pointer  `_api` to the web URL</span></span>
    
 
6. <span data-ttu-id="fa409-127">Verwenden Sie die resultierende URL und den Formulardigest für Anforderungen nach anderen Ressourcen, die Sie benötigen.</span><span class="sxs-lookup"><span data-stu-id="fa409-127">Use the resulting URL and the form digest to make requests for other resources you need.</span></span>
    
 
<span data-ttu-id="fa409-128">Sie müssen den Formulardigest nicht übergeben, wenn Sie **GET**-Anforderungen oder Anforderungen mit einem überprüften OAuth-Token ausführen möchten.</span><span class="sxs-lookup"><span data-stu-id="fa409-128">You don't have to pass the form digest if you're making  **GET** requests, or making requests using a validated OAuth token.</span></span>
 

 

## <a name="navigate-parent-and-child-sites"></a><span data-ttu-id="fa409-129">Navigieren durch über- und untergeordnete Websites</span><span class="sxs-lookup"><span data-stu-id="fa409-129">Navigate parent and child sites</span></span>
<span data-ttu-id="fa409-130"><a name="bk_sites"> </a></span><span class="sxs-lookup"><span data-stu-id="fa409-130"></span></span>

<span data-ttu-id="fa409-131"> Wenn Sie mithilfe des SharePoint Serverobjektmodells durch die Websitestruktur navigieren, verwenden Sie für den Zugriff auf Objekte, die übergeordnete und untergeordnete Websites darstellen, die Eigenschaften **SPWeb.ParentWeb** und **SPWeb.Webs**.</span><span class="sxs-lookup"><span data-stu-id="fa409-131">When you navigate your site structure using the SharePoint server object model, you use the  **SPWeb.ParentWeb** and **SPWeb.Webs** properties to access objects that represent parent and child sites.</span></span>
 

 
<span data-ttu-id="fa409-p106">Die entsprechenden REST Ressourcen – `web/parentweb` und `web/webs`– geben keine Objekte zurück, die Websites darstellen. Der Grund ist, dass der REST-Dienst OData-Standards entspricht und solche Anforderungen durch das Zurückgeben vollständiger Websitedarstellungen ineffizient würden. Stattdessen geben sie ein [WebInfo-Objekt](#bk_webinfo) mit den skalaren Eigenschaften der Website, aber ohne zugehörige Entitätenmengen wie Sammlungen oder Feldsammlungen zurück.</span><span class="sxs-lookup"><span data-stu-id="fa409-p106">The corresponding REST resources— `web/parentweb` and `web/webs`—don't return objects that represent sites. This is because the REST service conforms to OData standards, and returning complete site representations would make such requests inefficient. Instead, they return a  [WebInfo object ](#bk_webinfo) that contains the site's scalar properties, but without related entity sets such as like collections or field collections.</span></span>
 

 
<span data-ttu-id="fa409-p107">Um zu einer bestimmten übergeordneten oder untergeordneten Website zu navigieren, erstellen Sie die entsprechende REST-URL zu dieser Website und verwenden Sie dabei **Id** oder **Title**. Hier können Sie auf die mit der Website verknüpften Entitätenmengen zugreifen.</span><span class="sxs-lookup"><span data-stu-id="fa409-p107">To navigate to a specific parent or child site, construct the appropriate REST URL to that site using the  **Id** or **Title** property to. From there, you can access that site's related entity sets.</span></span>
 

 

## <a name="navigating-folder-structure"></a><span data-ttu-id="fa409-137">Navigieren durch die Datei- und Ordnerstruktur</span><span class="sxs-lookup"><span data-stu-id="fa409-137">Navigating folder structure</span></span>
<span data-ttu-id="fa409-138"><a name="bk_folders"> </a></span><span class="sxs-lookup"><span data-stu-id="fa409-138"></span></span>

<span data-ttu-id="fa409-p108"> Der SharePoint REST-Dienst bietet keine Unterstützung für das Durchsuchen der Ordnerhierarchie einer Website über die URL-Konstruktion. Verwenden Sie stattdessen das REST-Äquivalent der Methode **Web.GetFolderByServerRelativeUrl**. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="fa409-p108">The SharePoint REST service does not support traversing the folder hierarchy of a site through the URL construction. Instead, use the REST equivalent of the  **Web.GetFolderByServerRelativeUrl** method. For example:</span></span>
 

 
 <span data-ttu-id="fa409-142">*Durch den REST-Dienst nicht unterstützte Navigation:*</span><span class="sxs-lookup"><span data-stu-id="fa409-142">*Navigation not supported through the REST service:*</span></span> 
 

 
 `/_vti_bin/client.svc/web/lists/SharedDocuments/folder1/stuff/things/Recycle`
 

 
<span data-ttu-id="fa409-143">Durch den REST-Dienst unterstützte Navigation:</span><span class="sxs-lookup"><span data-stu-id="fa409-143">Navigation that is supported by the REST service:</span></span> 
 

 
 <span data-ttu-id="fa409-144">`/_vti_bin/client.svc/web/GetFolderByServerRelativeUrl('SharedDocuments/folder1/stuff/things')/Recycle`.</span><span class="sxs-lookup"><span data-stu-id="fa409-144"></span></span>
 

 

## <a name="spcontextwebinformation-object-properties"></a><span data-ttu-id="fa409-145">SPContextWebInformation-Objekteigenschaften</span><span class="sxs-lookup"><span data-stu-id="fa409-145">SPContextWebInformation object properties</span></span>
<span data-ttu-id="fa409-146"><a name="bk_props"> </a></span><span class="sxs-lookup"><span data-stu-id="fa409-146"></span></span>



|<span data-ttu-id="fa409-147">**Eigenschaft SPContextWebInformation**</span><span class="sxs-lookup"><span data-stu-id="fa409-147">**SPContextWebInformation Property**</span></span>|<span data-ttu-id="fa409-148">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="fa409-148">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="fa409-149">**webFullUrl**</span><span class="sxs-lookup"><span data-stu-id="fa409-149">**webFullUrl**</span></span>|<span data-ttu-id="fa409-150">Ruft die serverrelative URL der nächstgelegenen Website ab.</span><span class="sxs-lookup"><span data-stu-id="fa409-150">Gets the server-relative URL of the nearest site.</span></span>|
|<span data-ttu-id="fa409-151">**siteFullUrl**</span><span class="sxs-lookup"><span data-stu-id="fa409-151">**siteFullUrl**</span></span>|<span data-ttu-id="fa409-152">Ruft die serverrelative URL des Stamms der Websitesammlung ab, in der die Website enthalten ist. Wenn der Stamm einer Websitesammlung am nächsten gelegen ist, dann entspricht der Wert der Eigenschaft **webFullUrl** der Eigenschaft **siteFullUrl**.</span><span class="sxs-lookup"><span data-stu-id="fa409-152">Gets the server-relative URL of the root of the site collection that the site is contained within.If the nearest web is the root of a site collection, then the value of the  **webFullUrl** property is equal to the **siteFullUrl** property.</span></span>|
|<span data-ttu-id="fa409-153">**formDigestValue**</span><span class="sxs-lookup"><span data-stu-id="fa409-153">**formDigestValue**</span></span>|<span data-ttu-id="fa409-154">Ruft den Formulardigest der Serveranforderung ab.</span><span class="sxs-lookup"><span data-stu-id="fa409-154">Gets the server's request form digest.</span></span>|
|<span data-ttu-id="fa409-155">**LibraryVersion**</span><span class="sxs-lookup"><span data-stu-id="fa409-155">**LibraryVersion**</span></span>|<span data-ttu-id="fa409-156">Ruft die aktuelle Version der REST-Bibliothek ab.</span><span class="sxs-lookup"><span data-stu-id="fa409-156">Gets the current version of the REST library.</span></span>|
|<span data-ttu-id="fa409-157">**SupportedSchemaVersions**</span><span class="sxs-lookup"><span data-stu-id="fa409-157">**SupportedSchemaVersions**</span></span>|<span data-ttu-id="fa409-158">Ruft die Versionen des Schemas der REST-/CSOM-Bibliothek ab, die unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="fa409-158">Gets the versions of the schema of the REST/CSOM library that are supported.</span></span>|

## <a name="webinfo-object"></a><span data-ttu-id="fa409-159">WebInfo-Objekt</span><span class="sxs-lookup"><span data-stu-id="fa409-159">WebInfo object</span></span>
<span data-ttu-id="fa409-160"><a name="bk_webinfo"> </a></span><span class="sxs-lookup"><span data-stu-id="fa409-160"></span></span>



|<span data-ttu-id="fa409-161">**WebInfo-Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="fa409-161">**WebInfo property**</span></span>|<span data-ttu-id="fa409-162">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="fa409-162">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="fa409-163">**Created**</span><span class="sxs-lookup"><span data-stu-id="fa409-163">**Created**</span></span>|<span data-ttu-id="fa409-164">Ruft einen Wert ab, der angibt, wann die Website erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="fa409-164">Gets a value that specifies when the site was created.</span></span>|
|<span data-ttu-id="fa409-165">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="fa409-165">**Description**</span></span>|<span data-ttu-id="fa409-166">Dient zum Abrufen oder Festlegen der Beschreibung der Website.</span><span class="sxs-lookup"><span data-stu-id="fa409-166">Gets or sets the description for the site.</span></span>|
|<span data-ttu-id="fa409-167">**Id**</span><span class="sxs-lookup"><span data-stu-id="fa409-167">**Id**</span></span>|<span data-ttu-id="fa409-168">Ruft einen Wert ab, der den Websitebezeichner angibt.</span><span class="sxs-lookup"><span data-stu-id="fa409-168">Gets a value that specifies the site identifier.</span></span>|
|<span data-ttu-id="fa409-169">**Language**</span><span class="sxs-lookup"><span data-stu-id="fa409-169">**Language**</span></span>|<span data-ttu-id="fa409-170">Ruft einen Wert ab, der die Gebietsschema-ID (LCID) für die Sprache angibt, die auf der Website verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="fa409-170">Gets a value that specifies the locale ID (LCID) for the language that is used on the site.</span></span>|
|<span data-ttu-id="fa409-171">**LastItemModifiedDate**</span><span class="sxs-lookup"><span data-stu-id="fa409-171">**LastItemModifiedDate**</span></span>|<span data-ttu-id="fa409-172">Ruft einen Wert ab, der angibt, wann ein Element in der Website zuletzt geändert wurde.</span><span class="sxs-lookup"><span data-stu-id="fa409-172">Gets a value that specifies when an item was last modified in the site.</span></span>|
|<span data-ttu-id="fa409-173">**Title**</span><span class="sxs-lookup"><span data-stu-id="fa409-173">**Title**</span></span>|<span data-ttu-id="fa409-174">Dient zum Abrufen oder Festlegen des Titels der Website.</span><span class="sxs-lookup"><span data-stu-id="fa409-174">Gets or sets the title for the site.</span></span>|
|<span data-ttu-id="fa409-175">**WebTemplateId**</span><span class="sxs-lookup"><span data-stu-id="fa409-175">**WebTemplateId**</span></span>|<span data-ttu-id="fa409-176">Ruft den Bezeichner der Websitevorlage ab.</span><span class="sxs-lookup"><span data-stu-id="fa409-176">Gets the identifier of the site template.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="fa409-177">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="fa409-177">Additional resources</span></span>
<span data-ttu-id="fa409-178"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="fa409-178"></span></span>


-  [<span data-ttu-id="fa409-179">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="fa409-179">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-2013-rest-service)
    
 
-  [<span data-ttu-id="fa409-180">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="fa409-180">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-2013-rest-endpoints)
    
 
-  [<span data-ttu-id="fa409-181">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="fa409-181">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest)
    
 
-  [<span data-ttu-id="fa409-182">Arbeiten mit Ordnern und Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="fa409-182">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest)
    
 
-  [<span data-ttu-id="fa409-183">Ermitteln von URIs von SharePoint REST-Dienstendpunkten</span><span class="sxs-lookup"><span data-stu-id="fa409-183">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris)
    
 
-  [<span data-ttu-id="fa409-184">Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="fa409-184">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests)
    
 
-  [<span data-ttu-id="fa409-185">REST-API-Referenz und Beispiele</span><span class="sxs-lookup"><span data-stu-id="fa409-185">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="fa409-186">Synchronisieren von SharePoint-Elementen mit dem REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="fa409-186">Synchronize SharePoint items using the REST service</span></span>](synchronize-sharepoint-items-using-the-rest-service)
    
 
-  [<span data-ttu-id="fa409-187">Verwenden von ETag-Werten zum Bestimmen der Version von Dokument- und Listenelementen über den REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="fa409-187">Use ETag values through the REST service to get document list item versioning</span></span>](http://msdn.microsoft.com/library/5f7e0579-46b7-44ab-b3b4-cdbc622dcd98%28Office.15%29.aspx)
    
 

 

 

