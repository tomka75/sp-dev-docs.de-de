---
title: Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 21d0326e9729a0cdb16f03211fae76a76859e5ab
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="navigate-the-sharepoint-data-structure-represented-in-the-rest-service"></a><span data-ttu-id="dab96-102">Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur</span><span class="sxs-lookup"><span data-stu-id="dab96-102">Navigate the SharePoint data structure represented in the REST service</span></span>
<span data-ttu-id="dab96-103">Informationen zum Starten von einem REST-Endpunkt für einen gegebenen SharePoint-Element und Navigieren zu und Zugreifen auf dazugehörige Elemente, z. B. übergeordnete Standorte oder die Bibliotheksstruktur, in der sich das jeweilige Element befindet.</span><span class="sxs-lookup"><span data-stu-id="dab96-103">Learn how to start from a REST endpoint for a given SharePoint item, and navigate to and access related items, such as parent sites or the library structure where that item resides.</span></span> 
 
## <a name="navigate-from-a-given-url-to-reach-other-sharepoint-resources"></a><span data-ttu-id="dab96-104">Navigieren von einer bestimmten URL zu anderen SharePoint-Ressourcen</span><span class="sxs-lookup"><span data-stu-id="dab96-104">Navigate from a given URL to reach other SharePoint resources</span></span>
<span data-ttu-id="dab96-p101">Wenn Sie mit dem SharePoint REST-Dienst arbeiten, kennen Sie häufig die URL eines bestimmten SharePoint-Elements, möchten aber auf dazugehörige Elemente zugreifen, z. B. den Ordner oder die Bibliotheksstruktur, in dem/der sich das jeweilige Element befindet. Angenommen, Sie erstellen ein Add-In, bei dem die Benutzer die URL eines Dokuments in eine SharePoint-Bibliothek eingeben. Ihr Add-In muss dann die URL aufgliedern, um die tatsächliche URL der SharePoint-Website zu bestimmen. Anschließend kann das Add-In im Auftrag des Benutzers weitere Anforderungen an die Website stellen, z. B. zum Erstellen, Aktualisieren oder Löschen verwandter Elemente oder Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="dab96-p101">When you're working with the SharePoint REST service, you'll often start out knowing the URL of a specific SharePoint item, but want to access related items, such as the folder or library structure where that item resides. For example, suppose you create an add-in where your user enters the URL of a document in a SharePoint library. Your add-in must then break down that URL to figure out the actual SharePoint site URL. Once it's done that, the add-in can then make more requests from the site on the user's behalf, such as to create, update, or delete related items or resources.</span></span> 
 
<span data-ttu-id="dab96-109">Zu diesem Zweck muss das Add-in folgende Informationen von SharePoint abfragen:</span><span class="sxs-lookup"><span data-stu-id="dab96-109">To do this, your add-in needs to query SharePoint for the following information:</span></span>
 
- <span data-ttu-id="dab96-110">Die serverrelativen URLs der Website und die Websitesammlung, die die Ressource enthält</span><span class="sxs-lookup"><span data-stu-id="dab96-110">The server relative URLs of the site and site collection containing the resource</span></span>   
 
- <span data-ttu-id="dab96-111">Ein Formulardigest, mit dem Sie Abfragen ausführen können, die den Status der Ressource ändern. Beispiel:  **POST**,  **PUT**,  **MERGE** und  **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="dab96-111">A form digest to enable you to perform requests that change the state of the resource, such as  **POST**,  **PUT**,  **MERGE**, and  **DELETE**</span></span>
    
<span data-ttu-id="dab96-112">Das grundlegende Verfahren:</span><span class="sxs-lookup"><span data-stu-id="dab96-112">The basic process:</span></span>

1. <span data-ttu-id="dab96-p102">Verwenden Sie den Operator `/contextinfo` mit der angegebenen URL, um auf die Adressen der Website und der Websitesammlung und den Formulardigest zuzugreifen. Verwenden Sie den Operator `/contextinfo` in folgendem Format:</span><span class="sxs-lookup"><span data-stu-id="dab96-p102">Use the  `/contextinfo` operator with the given URL to access the site and site collection addresses, and the form digest. Use the `/contextinfo` operator in the following format:</span></span>
    
     `http://server/web/doclib/forms/_api/contextinfo`
    
    <span data-ttu-id="dab96-115">Zur Verbesserung der Sicherheit gegenüber websiteübergreifenden Scriptingversuchen akzeptiert der `/contextinfo`-Operator nur **POST**-Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="dab96-115">To increase security against cross-site scripting attempts, the  `/contextinfo` operator accepts only **POST** requests.</span></span>
    
 
2. <span data-ttu-id="dab96-116">Verwenden Sie für den Zugriff auf zusätzliche Ressourcen bei Bedarf die Objekteigenschaften [SPContextWebInformation](#bk_props), die der `/contextinfo`-Operator zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="dab96-116">Use the  [SPContextWebInformation object properties](#bk_props) that the `/contextinfo` operator returns to access additional resources as desired.</span></span>
    
 
 <span data-ttu-id="dab96-117">**Verwenden**</span><span class="sxs-lookup"><span data-stu-id="dab96-117">**Try it**</span></span>
 

1. <span data-ttu-id="dab96-p103">Beginnen Sie mit einer URL zu einem SharePoint-Element. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="dab96-p103">Start with a URL to a given SharePoint item. For example:</span></span>
    
     `http://site/web/doclib/myDocument.docx`
     
2. <span data-ttu-id="dab96-p104">Entfernen Sie den Namen der spezifischen Ressource vom Ende der URL, damit die URL auf eine Dokumentbibliothek, einen Ordner oder eine Liste verweist. In diesem Fall:</span><span class="sxs-lookup"><span data-stu-id="dab96-p104">Remove the name of the specific resource from the end of the URL, so that the URL points to a document library, folder, or list. IN this case:</span></span>
    
     `http://site/web/doclib/`
    
3. <span data-ttu-id="dab96-122">Fügen Sie den Zeiger des REST-Dienstes und den `/contextinfo`-Operator an die URL an:</span><span class="sxs-lookup"><span data-stu-id="dab96-122">Append the REST service pointer and the  `/contextinfo` operator to the URL:</span></span>
    
     `http://site/web/doclib/_api/contextinfo`
    
4. <span data-ttu-id="dab96-123">Lesen Sie den Formulardigest und die Eigenschaften **WebFullUrl** aus der Antwort aus.</span><span class="sxs-lookup"><span data-stu-id="dab96-123">Read the form digest and  **webFullUrl** properties from the response.</span></span>
    
5. <span data-ttu-id="dab96-124">Fügen Sie den Zeiger des REST-Dienstes `_api` an die Web-URL an:</span><span class="sxs-lookup"><span data-stu-id="dab96-124">Append the REST service pointer  `_api` to the web URL</span></span>
    
6. <span data-ttu-id="dab96-125">Verwenden Sie die resultierende URL und den Formulardigest für Anforderungen nach anderen Ressourcen, die Sie benötigen.</span><span class="sxs-lookup"><span data-stu-id="dab96-125">Use the resulting URL and the form digest to make requests for other resources you need.</span></span>
    
<span data-ttu-id="dab96-126">Sie müssen den Formulardigest nicht übergeben, wenn Sie **GET**-Anforderungen oder Anforderungen mit einem überprüften OAuth-Token ausführen möchten.</span><span class="sxs-lookup"><span data-stu-id="dab96-126">You don't have to pass the form digest if you're making  **GET** requests, or making requests using a validated OAuth token.</span></span>
 
## <a name="navigate-parent-and-child-sites"></a><span data-ttu-id="dab96-127">Navigieren durch über- und untergeordnete Websites</span><span class="sxs-lookup"><span data-stu-id="dab96-127">Navigate parent and child sites</span></span>
<span data-ttu-id="dab96-128"><a name="bk_sites"> </a> Wenn Sie mithilfe des SharePoint Serverobjektmodells durch die Websitestruktur navigieren, verwenden Sie für den Zugriff auf Objekte, die übergeordnete und untergeordnete Websites darstellen, die Eigenschaften **SPWeb.ParentWeb** und **SPWeb.Webs**.</span><span class="sxs-lookup"><span data-stu-id="dab96-128">When you navigate your site structure using the SharePoint server object model, you use the  **SPWeb.ParentWeb** and **SPWeb.Webs** properties to access objects that represent parent and child sites.</span></span>

<span data-ttu-id="dab96-p105">Die entsprechenden REST Ressourcen – `web/parentweb` und `web/webs`– geben keine Objekte zurück, die Websites darstellen. Der Grund ist, dass der REST-Dienst OData-Standards entspricht und solche Anforderungen durch das Zurückgeben vollständiger Websitedarstellungen ineffizient würden. Stattdessen geben sie ein [WebInfo-Objekt](#bk_webinfo) mit den skalaren Eigenschaften der Website, aber ohne zugehörige Entitätenmengen wie Sammlungen oder Feldsammlungen zurück.</span><span class="sxs-lookup"><span data-stu-id="dab96-p105">The corresponding REST resources— `web/parentweb` and `web/webs`—don't return objects that represent sites. This is because the REST service conforms to OData standards, and returning complete site representations would make such requests inefficient. Instead, they return a  [WebInfo object ](#bk_webinfo) that contains the site's scalar properties, but without related entity sets such as like collections or field collections.</span></span>
  
<span data-ttu-id="dab96-p106">Um zu einer bestimmten übergeordneten oder untergeordneten Website zu navigieren, erstellen Sie die entsprechende REST-URL zu dieser Website und verwenden Sie dabei **Id** oder **Title**. Hier können Sie auf die mit der Website verknüpften Entitätenmengen zugreifen.</span><span class="sxs-lookup"><span data-stu-id="dab96-p106">To navigate to a specific parent or child site, construct the appropriate REST URL to that site using the  **Id** or **Title** property to. From there, you can access that site's related entity sets.</span></span>
 
## <a name="navigating-folder-structure"></a><span data-ttu-id="dab96-134">Navigieren durch die Datei- und Ordnerstruktur</span><span class="sxs-lookup"><span data-stu-id="dab96-134">Navigating folder structure</span></span>
<span data-ttu-id="dab96-135"><a name="bk_folders"> </a> Der SharePoint REST-Dienst bietet keine Unterstützung für das Durchsuchen der Ordnerhierarchie einer Website über die URL-Konstruktion.</span><span class="sxs-lookup"><span data-stu-id="dab96-135"><a name="bk_folders"> </a> The SharePoint REST service does not support traversing the folder hierarchy of a site through the URL construction. Instead, use the REST equivalent of the  Web.GetFolderByServerRelativeUrl method. For example:</span></span> <span data-ttu-id="dab96-136">Verwenden Sie stattdessen das REST-Äquivalent der Methode **Web.GetFolderByServerRelativeUrl**.</span><span class="sxs-lookup"><span data-stu-id="dab96-136">Instead, use the REST equivalent of the  **Web.GetFolderByServerRelativeUrl** method.</span></span> <span data-ttu-id="dab96-137">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="dab96-137">For example:</span></span>
 
 <span data-ttu-id="dab96-138">*Durch den REST-Dienst nicht unterstützte Navigation:*</span><span class="sxs-lookup"><span data-stu-id="dab96-138">*Navigation not supported through the REST service:*</span></span> 
  
 `/_vti_bin/client.svc/web/lists/SharedDocuments/folder1/stuff/things/Recycle`
 
<span data-ttu-id="dab96-139">Durch den REST-Dienst unterstützte Navigation:</span><span class="sxs-lookup"><span data-stu-id="dab96-139">Navigation that is supported by the REST service:</span></span> 
 
 <span data-ttu-id="dab96-140">`/_vti_bin/client.svc/web/GetFolderByServerRelativeUrl('SharedDocuments/folder1/stuff/things')/Recycle`.</span><span class="sxs-lookup"><span data-stu-id="dab96-140"></span></span>
 

## <a name="spcontextwebinformation-object-properties"></a><span data-ttu-id="dab96-141">SPContextWebInformation-Objekteigenschaften</span><span class="sxs-lookup"><span data-stu-id="dab96-141">SPContextWebInformation object properties</span></span>
<span data-ttu-id="dab96-142"><a name="bk_props"> </a></span><span class="sxs-lookup"><span data-stu-id="dab96-142"></span></span>

|<span data-ttu-id="dab96-143">**Eigenschaft SPContextWebInformation**</span><span class="sxs-lookup"><span data-stu-id="dab96-143">**SPContextWebInformation Property**</span></span>|<span data-ttu-id="dab96-144">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dab96-144">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dab96-145">**webFullUrl**</span><span class="sxs-lookup"><span data-stu-id="dab96-145">**webFullUrl**</span></span>|<span data-ttu-id="dab96-146">Ruft die serverrelative URL der nächstgelegenen Website ab.</span><span class="sxs-lookup"><span data-stu-id="dab96-146">Gets the server-relative URL of the nearest site.</span></span>|
|<span data-ttu-id="dab96-147">**siteFullUrl**</span><span class="sxs-lookup"><span data-stu-id="dab96-147">**siteFullUrl**</span></span>|<span data-ttu-id="dab96-148">Ruft die serverrelative URL des Stamms der Websitesammlung ab, in der die Website enthalten ist. Wenn der Stamm einer Websitesammlung am nächsten gelegen ist, dann entspricht der Wert der Eigenschaft **webFullUrl** der Eigenschaft **siteFullUrl**.</span><span class="sxs-lookup"><span data-stu-id="dab96-148">Gets the server-relative URL of the root of the site collection that the site is contained within.If the nearest web is the root of a site collection, then the value of the  **webFullUrl** property is equal to the **siteFullUrl** property.</span></span>|
|<span data-ttu-id="dab96-149">**formDigestValue**</span><span class="sxs-lookup"><span data-stu-id="dab96-149">**formDigestValue**</span></span>|<span data-ttu-id="dab96-150">Ruft den Formulardigest der Serveranforderung ab.</span><span class="sxs-lookup"><span data-stu-id="dab96-150">Gets the server's request form digest.</span></span>|
|<span data-ttu-id="dab96-151">**LibraryVersion**</span><span class="sxs-lookup"><span data-stu-id="dab96-151">**LibraryVersion**</span></span>|<span data-ttu-id="dab96-152">Ruft die aktuelle Version der REST-Bibliothek ab.</span><span class="sxs-lookup"><span data-stu-id="dab96-152">Gets the current version of the REST library.</span></span>|
|<span data-ttu-id="dab96-153">**SupportedSchemaVersions**</span><span class="sxs-lookup"><span data-stu-id="dab96-153">**SupportedSchemaVersions**</span></span>|<span data-ttu-id="dab96-154">Ruft die Versionen des Schemas der REST-/CSOM-Bibliothek ab, die unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="dab96-154">Gets the versions of the schema of the REST/CSOM library that are supported.</span></span>|

## <a name="webinfo-object"></a><span data-ttu-id="dab96-155">WebInfo-Objekt</span><span class="sxs-lookup"><span data-stu-id="dab96-155">WebInfo object</span></span>
<span data-ttu-id="dab96-156"><a name="bk_webinfo"> </a></span><span class="sxs-lookup"><span data-stu-id="dab96-156"></span></span>

|<span data-ttu-id="dab96-157">**WebInfo-Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="dab96-157">**WebInfo property**</span></span>|<span data-ttu-id="dab96-158">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dab96-158">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dab96-159">**Created**</span><span class="sxs-lookup"><span data-stu-id="dab96-159">**Created**</span></span>|<span data-ttu-id="dab96-160">Ruft einen Wert ab, der angibt, wann die Website erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="dab96-160">Gets a value that specifies when the site was created.</span></span>|
|<span data-ttu-id="dab96-161">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dab96-161">**Description**</span></span>|<span data-ttu-id="dab96-162">Dient zum Abrufen oder Festlegen der Beschreibung der Website.</span><span class="sxs-lookup"><span data-stu-id="dab96-162">Gets or sets the description for the site.</span></span>|
|<span data-ttu-id="dab96-163">**Id**</span><span class="sxs-lookup"><span data-stu-id="dab96-163">**Id**</span></span>|<span data-ttu-id="dab96-164">Ruft einen Wert ab, der den Websitebezeichner angibt.</span><span class="sxs-lookup"><span data-stu-id="dab96-164">Gets a value that specifies the site identifier.</span></span>|
|<span data-ttu-id="dab96-165">**Language**</span><span class="sxs-lookup"><span data-stu-id="dab96-165">**Language**</span></span>|<span data-ttu-id="dab96-166">Ruft einen Wert ab, der die Gebietsschema-ID (LCID) für die Sprache angibt, die auf der Website verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="dab96-166">Gets a value that specifies the locale ID (LCID) for the language that is used on the site.</span></span>|
|<span data-ttu-id="dab96-167">**LastItemModifiedDate**</span><span class="sxs-lookup"><span data-stu-id="dab96-167">**LastItemModifiedDate**</span></span>|<span data-ttu-id="dab96-168">Ruft einen Wert ab, der angibt, wann ein Element in der Website zuletzt geändert wurde.</span><span class="sxs-lookup"><span data-stu-id="dab96-168">Gets a value that specifies when an item was last modified in the site.</span></span>|
|<span data-ttu-id="dab96-169">**Title**</span><span class="sxs-lookup"><span data-stu-id="dab96-169">**Title**</span></span>|<span data-ttu-id="dab96-170">Dient zum Abrufen oder Festlegen des Titels der Website.</span><span class="sxs-lookup"><span data-stu-id="dab96-170">Gets or sets the title for the site.</span></span>|
|<span data-ttu-id="dab96-171">**WebTemplateId**</span><span class="sxs-lookup"><span data-stu-id="dab96-171">**WebTemplateId**</span></span>|<span data-ttu-id="dab96-172">Ruft den Bezeichner der Websitevorlage ab.</span><span class="sxs-lookup"><span data-stu-id="dab96-172">Gets the identifier of the site template.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="dab96-173">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="dab96-173">Additional resources</span></span>
<span data-ttu-id="dab96-174"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="dab96-174"></span></span>

-  [<span data-ttu-id="dab96-175">Grundlegendes zum SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="dab96-175">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
-  [<span data-ttu-id="dab96-176">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="dab96-176">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [<span data-ttu-id="dab96-177">Arbeiten mit Listen und Listenelementen unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="dab96-177">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
-  [<span data-ttu-id="dab96-178">Arbeiten mit Ordnern und Dateien unter Verwendung von REST</span><span class="sxs-lookup"><span data-stu-id="dab96-178">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest.md)
-  [<span data-ttu-id="dab96-179">Ermitteln von URIs von SharePoint REST-Dienstendpunkten</span><span class="sxs-lookup"><span data-stu-id="dab96-179">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris.md)
-  [<span data-ttu-id="dab96-180">Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="dab96-180">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests.md)
-  [<span data-ttu-id="dab96-181">REST-API-Referenz und Beispiele</span><span class="sxs-lookup"><span data-stu-id="dab96-181">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [<span data-ttu-id="dab96-182">Synchronisieren von SharePoint-Elementen mit dem REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="dab96-182">Synchronize SharePoint items using the REST service</span></span>](synchronize-sharepoint-items-using-the-rest-service.md)
-  [<span data-ttu-id="dab96-183">Verwenden von ETag-Werten zum Bestimmen der Version von Dokument- und Listenelementen über den REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="dab96-183">Use ETag values through the REST service to get document list item versioning</span></span>](http://msdn.microsoft.com/library/use-etag-values-through-the-rest-service-to-get-document-list-item-versioning%28Office.15%29.aspx)
    
 

 

 

