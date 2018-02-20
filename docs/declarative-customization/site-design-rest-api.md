---
title: REST-API von SharePoint-Websitedesigns
description: "Verwenden Sie SharePoint-Websitedesigns über die SharePoint-REST-Schnittstelle, um grundlegende CRUD-Operationen (Create, Read, Update, Delete, also Erstellen, Lesen, Aktualisieren und Löschen) auszuführen."
ms.date: 12/14/2017
ms.openlocfilehash: a230c66d55ab60b900ae60a31c37f0cf75f1a789
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/19/2018
---
# <a name="site-design-and-site-script-rest-api"></a><span data-ttu-id="3aa2e-103">REST-API von SharePoint-Websitedesigns und Websiteskripts</span><span class="sxs-lookup"><span data-stu-id="3aa2e-103">Site design and site script REST API</span></span>

> [!NOTE]
> <span data-ttu-id="3aa2e-104">Websitedesigns und Websiteskripts befinden sich in der Vorschau und können ohne vorherige Ankündigung geändert werden.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-104">Site designs and site scripts are in preview and are subject to change.</span></span> <span data-ttu-id="3aa2e-105">Sie werden derzeit nur für Produktionsumgebungen im Zielrelease unterstützt.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-105">They are currently only supported for use in production environments in Targeted Release.</span></span>

<span data-ttu-id="3aa2e-106">Mithilfe der SharePoint-REST-Schnittstelle können Sie grundlegende CRUD-Operationen ausführen, d. h: Erstellen, Lesen, Aktualisieren und Löschen (Create, Read, Update, Delete).</span><span class="sxs-lookup"><span data-stu-id="3aa2e-106">You can use the the SharePoint REST interface to perform basic create, read, update, and delete (CRUD) operations on site designs and site scripts.</span></span>

<span data-ttu-id="3aa2e-107">Der REST-Dienst in SharePoint Online (sowie in lokalen Bereitstellungen von SharePoint 2016 und höher) erlaubt die Zusammenfassung mehrerer Anforderungen in einem einzigen Aufruf an den Service mittels der ODATA-Abfrageoption „$batch“.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-107">The SharePoint Online (and SharePoint 2016 and later on-premises) REST service supports combining multiple requests into a single call to the service by using the OData $batch query option.</span></span> <span data-ttu-id="3aa2e-108">Einzelheiten und Links zu Codebeispielen finden Sie unter [Durchführen von Batchanforderungen mit den REST-APIs](../sp-add-ins/make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="3aa2e-108">For details and links to code samples, see [Make batch requests with the REST APIs](../sp-add-ins/make-batch-requests-with-the-rest-apis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3aa2e-109">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="3aa2e-109">Prerequisites</span></span>
<span data-ttu-id="3aa2e-110">Lesen Sie vor der Umsetzung der Beispiele in diesem Artikel zunächst die folgenden Artikel:</span><span class="sxs-lookup"><span data-stu-id="3aa2e-110">Before you get started, make sure that you're familiar with the following:</span></span>
- [<span data-ttu-id="3aa2e-111">Grundlegendes zum SharePoint-REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="3aa2e-111">Get to know the SharePoint REST service</span></span>](../sp-add-ins/get-to-know-the-sharepoint-rest-service.md) 
- [<span data-ttu-id="3aa2e-112">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="3aa2e-112">Complete basic operations using SharePoint REST endpoints</span></span>](../sp-add-ins/complete-basic-operations-using-sharepoint-rest-endpoints.md)

## <a name="rest-commands"></a><span data-ttu-id="3aa2e-113">REST-Befehle</span><span class="sxs-lookup"><span data-stu-id="3aa2e-113">REST commands</span></span>

<span data-ttu-id="3aa2e-114">Für Websitedesigns und Websiteskripts stehen die folgenden REST-Befehle zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="3aa2e-114">The following REST commands are available for working with site designs and site scripts:</span></span>

- <span data-ttu-id="3aa2e-115">**CreateSiteScript** &mdash; Erstellen eines neuen Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-115">**CreateSiteScript** &mdash; Creates a new site script.</span></span>
- <span data-ttu-id="3aa2e-116">**GetSiteScripts** &mdash; Abrufen einer Liste von Informationen zu vorhandenen Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-116">**GetSiteScripts** &mdash; Gets a list of information on existing site scripts.</span></span>
- <span data-ttu-id="3aa2e-117">**GetSiteScriptMetadata** &mdash; Abrufen von Informationen zu einem bestimmten Websiteskript.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-117">**GetSiteScriptMetadata** &mdash; Gets information about a specific site script.</span></span>
- <span data-ttu-id="3aa2e-118">**UpdateSiteScript** &mdash; Aktualisieren eines Websiteskripts mit neuen Werten.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-118">**UpdateSiteScript** &mdash; Updates a site script with new values.</span></span>
- <span data-ttu-id="3aa2e-119">**DeleteSiteScript** &mdash; Löschen eines Websitekripts.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-119">**DeleteSiteScript** &mdash; Deletes a site script.</span></span>
- <span data-ttu-id="3aa2e-120">**CreateSiteDesign** &mdash; Erstellen eines Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-120">**CreateSiteDesign** &mdash; Creates a site design.</span></span>
- <span data-ttu-id="3aa2e-121">**GetSiteDesigns** &mdash; Abrufen einer Liste von Informationen zu vorhandenen Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-121">**GetSiteDesigns** &mdash; Gets a list of information on existing site designs.</span></span>
- <span data-ttu-id="3aa2e-122">**GetSiteDesignMetadata** &mdash; Abrufen von Informationen zu einem bestimmten Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-122">**GetSiteDesignMetadata** &mdash; Gets information about a sepcific site design.</span></span>
- <span data-ttu-id="3aa2e-123">**UpdateSiteDesign** &mdash; Aktualisieren eines Websitedesigns mit neuen Werten.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-123">**UpdateSiteDesign** &mdash; Updates a site design with new values.</span></span>
- <span data-ttu-id="3aa2e-124">**DeleteSiteDesign** &mdash; Löschen eines Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-124">**DeleteSiteDesign** &mdash; Deletes a site design.</span></span>
- <span data-ttu-id="3aa2e-125">**GetSiteDesignRights** &mdash; Abrufen einer Liste von Prinzipalen, die Zugriff auf ein Websitedesign haben.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-125">**GetSiteDesignRights** &mdash; Gets a list of principals that have access to a site design.</span></span>
- <span data-ttu-id="3aa2e-126">**GrantSiteDesignRights** &mdash; Erteilen von Zugriff auf ein Websitedesign für einen oder mehrere Prinzipale.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-126">**GrantSiteDesignRights** &mdash; Grants access to a site design for one or more principals.</span></span>
- <span data-ttu-id="3aa2e-127">**RevokeSiteDesignRights** &mdash; Widerrufen des Zugriffs auf ein Websitedesign für einen oder mehrere Prinzipale.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-127">**RevokeSiteDesignRights** &mdash; Revokes access from a site design for one or more principals.</span></span>

## <a name="create-a-function-to-send-rest-requests"></a><span data-ttu-id="3aa2e-128">Erstellen einer Funktion zum Senden von REST-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="3aa2e-128">Create a function to send REST requests</span></span>

<span data-ttu-id="3aa2e-129">Zum Arbeiten mit der REST-API wird empfohlen, eine Hilfsfunktion für die REST-Aufrufe zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-129">To work with the REST API we recommend creating a helper function to make the REST calls.</span></span> <span data-ttu-id="3aa2e-130">Die folgende **RestRequest**-Funktion ruft die im **url**-Parameter angegebene REST-Methode auf und übergibt die weiteren Parameter in **params**.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-130">The following **RestRequest** function will call the REST method specified in the **url** parameter and pass the additional parameters in **params**.</span></span>

```javascript
function RestRequest(url,params) {
  var req = new XMLHttpRequest();
  req.onreadystatechange = function ()
  {
    if (req.readyState != 4) // Loaded
      return;
    console.log(req.responseText);
  };

  // Prepend web URL to url and remove duplicated slashes.
  var webBasedUrl = (_spPageContextInfo.webServerRelativeUrl + "//" + url).replace(/\/{2,}/,"/");
  req.open("POST",webBasedUrl,true);
  req.setRequestHeader("Content-Type", "application/json;charset=utf-8");
  req.setRequestHeader("ACCEPT", "application/json; odata.metadata=minimal");
  req.setRequestHeader("x-requestdigest", _spPageContextInfo.formDigestValue);
  req.setRequestHeader("ODATA-VERSION","4.0");
  req.send(params ? JSON.stringify(params) : void 0);
}
```

## <a name="createsitescript"></a><span data-ttu-id="3aa2e-131">CreateSiteScript</span><span class="sxs-lookup"><span data-stu-id="3aa2e-131">CreateSiteScript</span></span>

<span data-ttu-id="3aa2e-132">Erstellt ein neues Websiteskript.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-132">Creates a new site script.</span></span>

### <a name="parameters"></a><span data-ttu-id="3aa2e-133">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-133">Parameters</span></span>

|<span data-ttu-id="3aa2e-134">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-134">Parameter</span></span>     | <span data-ttu-id="3aa2e-135">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3aa2e-135">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="3aa2e-136">Titel</span><span class="sxs-lookup"><span data-stu-id="3aa2e-136">Title</span></span>       | <span data-ttu-id="3aa2e-137">Der Anzeigename des Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-137">The display name of the site design.</span></span> |
| <span data-ttu-id="3aa2e-138">Inhalt</span><span class="sxs-lookup"><span data-stu-id="3aa2e-138">Content</span></span>     | <span data-ttu-id="3aa2e-139">JSON-Wert, der das Skript beschreibt.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-139">JSON value that describes the script.</span></span> <span data-ttu-id="3aa2e-140">Weitere Informationen finden Sie unter [JSON-Referenz](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="3aa2e-140">For more information, see [JSON reference](site-design-json-schema.md).</span></span>|

<span data-ttu-id="3aa2e-141">Im folgenden Beispiel wird ein neues Websiteskript erstellt, das ein benutzerdefiniertes Design anwendet.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-141">The following example creates a new site script that applies a custom theme.</span></span>

```javascript
var site_script = 
{
  "$schema": "schema.json",
  "actions": [
    {
      "verb": "applyTheme",
      "themeName": "Contoso Theme"
    }
  ],
  "bindata": { },
  "version": 1
};

RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteScript(Title=@title)?@title='Contoso theme script'", site_script);
```

<span data-ttu-id="3aa2e-142">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **CreateSiteScript** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-142">Here is an example of the JSON returned after calling **CreateSiteScript**.</span></span> <span data-ttu-id="3aa2e-143">Er enthält die ID des neuen Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-143">It contains the ID of the new site script.</span></span>

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteScriptMetadata",
  "Content": null,
  "Description": null,
  "Id": "7647d3d6-1046-41fe-a798-4ff66b099d12",
  "Title": "Contoso customer list",
  "Version": 0
}
```

## <a name="getsitescripts"></a><span data-ttu-id="3aa2e-144">GetSiteScripts</span><span class="sxs-lookup"><span data-stu-id="3aa2e-144">GetSiteScripts</span></span>

<span data-ttu-id="3aa2e-145">Abrufen einer Liste von Informationen zu allen vorhandenen Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-145">Gets a list of information on all existing site scripts.</span></span>

### <a name="parameters"></a><span data-ttu-id="3aa2e-146">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-146">Parameters</span></span>

<span data-ttu-id="3aa2e-147">Keine</span><span class="sxs-lookup"><span data-stu-id="3aa2e-147">None.</span></span>

<span data-ttu-id="3aa2e-148">Im folgenden Beispiel werden die Websiteskriptinformationen für alle Websiteskripts abgerufen.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-148">The following example gets the site script information for all site scripts.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScripts");
```

<span data-ttu-id="3aa2e-149">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **GetSiteScripts** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-149">Here is an example of the JSON returned after calling **GetSiteScripts**.</span></span>

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Collection(Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteScriptMetadata)",
  "value": [
    {
      "Content": null,
      "Description": null,
      "Id": "6dfedb96-c090-44e3-875a-1c38032715fc",
      "Title": "Customer orders",
      "Version": 1
    },
    {
      "Content": null,
      "Description": null,
      "Id": "07702c07-0485-426f-b710-4704241caad9",
      "Title": "Contoso theme",
      "Version": 1
    }
  ]
}
```

## <a name="getsitescriptmetadata"></a><span data-ttu-id="3aa2e-150">GetSiteScriptMetadata</span><span class="sxs-lookup"><span data-stu-id="3aa2e-150">GetSiteScriptMetadata</span></span>

<span data-ttu-id="3aa2e-151">Abrufen von Informationen zu einem bestimmten Websiteskript.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-151">Gets information about a specific site script.</span></span> <span data-ttu-id="3aa2e-152">Es wird auch der JSON-Code des Skripts zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-152">It also returns the JSON of the script.</span></span>

### <a name="parameters"></a><span data-ttu-id="3aa2e-153">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-153">Parameters</span></span>

|<span data-ttu-id="3aa2e-154">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-154">Parameter</span></span>     | <span data-ttu-id="3aa2e-155">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3aa2e-155">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="3aa2e-156">id</span><span class="sxs-lookup"><span data-stu-id="3aa2e-156">id</span></span>    | <span data-ttu-id="3aa2e-157">Die ID des Websiteskripts, über das Informationen abgerufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-157">The ID of the site script to get information about.</span></span> |

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScriptMetadata",
{id:"07702c07-0485-426f-b710-4704241caad9"});
```

<span data-ttu-id="3aa2e-158">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **GetSiteScriptMetadata** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-158">Here is an example of the JSON returned after calling **GetSiteScriptMetadata**.</span></span>

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteScriptMetadata",
  "Content": "{\r\n    \"$schema\": \"schema.json\",\r\n        \"actions\": [\r\n            {\r\n               \"verb\": \"applyTheme\",\r\n               \"themeName\": \"Custom Cyan\"\r\n            }\r\n        ],\r\n            \"bindata\": { },\r\n    \"version\": 1\r\n}",
  "Description": null,
  "Id": "07702c07-0485-426f-b710-4704241caad9",
  "Title": "Contoso theme",
  "Version": 1
}
```

## <a name="updatesitescript"></a><span data-ttu-id="3aa2e-159">UpdateSiteScript</span><span class="sxs-lookup"><span data-stu-id="3aa2e-159">UpdateSiteScript</span></span>

<span data-ttu-id="3aa2e-160">Aktualisieren eines Websiteskripts mit neuen Werten.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-160">Updates a site script with new values.</span></span> <span data-ttu-id="3aa2e-161">In dem REST-Aufruf sind alle Parameter mit Ausnahme der Website-Skript-ID optional.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-161">In the REST call all parameters are optional except the site script Id.</span></span>

### <a name="parameters"></a><span data-ttu-id="3aa2e-162">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-162">Parameters</span></span>

|<span data-ttu-id="3aa2e-163">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-163">Parameter</span></span>   | <span data-ttu-id="3aa2e-164">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3aa2e-164">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="3aa2e-165">Id</span><span class="sxs-lookup"><span data-stu-id="3aa2e-165">Id</span></span>         | <span data-ttu-id="3aa2e-166">Die ID des zu aktualisierenden Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-166">The ID of the site script to update.</span></span> |
|<span data-ttu-id="3aa2e-167">Titel</span><span class="sxs-lookup"><span data-stu-id="3aa2e-167">Title</span></span>       | <span data-ttu-id="3aa2e-168">(optional) Der neue Anzeigename des Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-168">(optional) The new display name of the site script.</span></span> |
|<span data-ttu-id="3aa2e-169">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3aa2e-169">Description</span></span> | <span data-ttu-id="3aa2e-170">(Optional) Die neue Beschreibung des Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-170">(Optional) The new description of the site script.</span></span> |
| <span data-ttu-id="3aa2e-171">Version</span><span class="sxs-lookup"><span data-stu-id="3aa2e-171">Version</span></span>    | <span data-ttu-id="3aa2e-172">(Optional) Die neue Versionsnummer des Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-172">(Optional) The new version number of the site script.</span></span> |
| <span data-ttu-id="3aa2e-173">Inhalt</span><span class="sxs-lookup"><span data-stu-id="3aa2e-173">Content</span></span>    | <span data-ttu-id="3aa2e-174">(Optional) Ein neues JSON-Skript, das die Skriptaktionen definiert.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-174">(Optional) A new JSON script defining the script actions.</span></span> <span data-ttu-id="3aa2e-175">Weitere Informationen finden Sie unter [JSON-Schema eines Websitedesigns](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="3aa2e-175">For more information, see [Site design JSON schema](site-design-json-schema.md)</span></span> |

<span data-ttu-id="3aa2e-176">Nachfolgend finden Sie ein Beispiel des Aktualisierens eines vorhandenen Websiteskripts mit einem neuen JSON-Skript und neuen Werten.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-176">Here's an example of updating an existing site script with a new JSON script and values.</span></span>

```javascript
var updated_site_script = 
{
  "$schema": "schema.json",
  "actions": [
    {
      "verb": "applyTheme",
      "themeName": "Contoso Theme"
    }
  ],
  "bindata": { },
  "version": 2
};


RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.UpdateSiteScript", 
{updateInfo:{
  Id:"07702c07-0485-426f-b710-4704241caad9",
  Title:"New Contoso theme", 
  Description:"Updated Contoso site script", 
  Version: 2, 
  Content: JSON.stringify(updated_site_script)}});
```

<span data-ttu-id="3aa2e-177">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **UpdateSiteScript** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-177">Here is an example of the JSON returned after calling **UpdateSiteScript**.</span></span>

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteScriptMetadata",
  "Content": "{\"$schema\":\"schema.json\",\"actions\":[{\"verb\":\"applyTheme\",\"themeName\":\"Contoso Theme\"}],\"bindata\":{},\"version\":2}",
  "Description": "Updated Contoso site script",
  "Id": "07702c07-0485-426f-b710-4704241caad9",
  "Title": "New Contoso theme",
  "Version": 2
}
```

## <a name="deletesitescript"></a><span data-ttu-id="3aa2e-178">DeleteSiteScript</span><span class="sxs-lookup"><span data-stu-id="3aa2e-178">DeleteSiteScript</span></span>

<span data-ttu-id="3aa2e-179">Löschen eines Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-179">Deletes a site script.</span></span>

### <a name="parameters"></a><span data-ttu-id="3aa2e-180">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-180">Parameters</span></span>

|<span data-ttu-id="3aa2e-181">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-181">Parameter</span></span>   | <span data-ttu-id="3aa2e-182">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3aa2e-182">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="3aa2e-183">id</span><span class="sxs-lookup"><span data-stu-id="3aa2e-183">id</span></span>         | <span data-ttu-id="3aa2e-184">Die ID des zu löschenden Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-184">The ID of the site script to delete.</span></span> |

<span data-ttu-id="3aa2e-185">Nachfolgend finden Sie ein Beispiel zum Löschen eines Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-185">Here's an example of deleting a site script.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteScript", 
{id:"07702c07-0485-426f-b710-4704241caad9"});
```

## <a name="createsitedesign"></a><span data-ttu-id="3aa2e-186">CreateSiteDesign</span><span class="sxs-lookup"><span data-stu-id="3aa2e-186">CreateSiteDesign</span></span>

<span data-ttu-id="3aa2e-187">Erstellen eines neues Websitedesigns, das für Benutzer beim Erstellen einer neuen Website von der SharePoint-Startseite verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-187">Creates a new site design available to users when they create a new site from the SharePoint home page.</span></span>

### <a name="parameters"></a><span data-ttu-id="3aa2e-188">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-188">Parameters</span></span>

|<span data-ttu-id="3aa2e-189">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-189">Parameter</span></span>  | <span data-ttu-id="3aa2e-190">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3aa2e-190">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="3aa2e-191">Titel</span><span class="sxs-lookup"><span data-stu-id="3aa2e-191">Title</span></span>                 | <span data-ttu-id="3aa2e-192">Der Anzeigename des Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-192">The display name of the site design.</span></span> |
|<span data-ttu-id="3aa2e-193">WebTemplate</span><span class="sxs-lookup"><span data-stu-id="3aa2e-193">WebTemplate</span></span>           | <span data-ttu-id="3aa2e-194">Identifiziert, zu welcher Basisvorlage das Design hinzugefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-194">Identifies which base template to add the design to.</span></span> <span data-ttu-id="3aa2e-195">Verwenden Sie den Wert **64** für die Teamwebsite-Vorlage und den Wert **68** für die Kommunikationswebsitevorlage.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-195">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="3aa2e-196">SiteScripts</span><span class="sxs-lookup"><span data-stu-id="3aa2e-196">SiteScripts</span></span>           | <span data-ttu-id="3aa2e-197">Ein Array von einem oder mehreren Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-197">An array of one or more site scripts.</span></span> <span data-ttu-id="3aa2e-198">Jedes wird durch eine ID identifziert.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-198">Each is identified by an ID.</span></span> <span data-ttu-id="3aa2e-199">Die Skripts werden in der aufgeführten Reihenfolge ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-199">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="3aa2e-200">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3aa2e-200">Description</span></span>         | <span data-ttu-id="3aa2e-201">(Optional) Die Anzeigebeschreibung des Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-201">(Optional) The display description of site design.</span></span> |
|<span data-ttu-id="3aa2e-202">PreviewImageUrl</span><span class="sxs-lookup"><span data-stu-id="3aa2e-202">PreviewImageUrl</span></span>     | <span data-ttu-id="3aa2e-203">(optional) Die URL eines Vorschaubilds.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-203">(Optional) The URL of a preview image.</span></span> <span data-ttu-id="3aa2e-204">Wenn keine angegeben ist, verwendet SharePoint ein allgemeines Bild.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-204">If none is specified SharePoint will use a generic image.</span></span> |
|<span data-ttu-id="3aa2e-205">PreviewImageAltText</span><span class="sxs-lookup"><span data-stu-id="3aa2e-205">PreviewImageAltText</span></span> | <span data-ttu-id="3aa2e-206">(Optional) Die Alternativtextbeschreibung des Bilds für Barrierefreiheit.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-206">(Optional) The alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="3aa2e-207">IsDefault</span><span class="sxs-lookup"><span data-stu-id="3aa2e-207">IsDefault</span></span>           | <span data-ttu-id="3aa2e-208">(Optional) **True**, wenn das Websitedesign als Standarddesign der Website angewendet wird; andernfalls **False**.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-208">(Optional) **true** if the site design is applied as the default site design; otherwise, **false**.</span></span> <span data-ttu-id="3aa2e-209">Weitere Informationen finden Sie unter [Anpassen eines standardmäßigen Websitedesigns](customize-default-site-design.md).</span><span class="sxs-lookup"><span data-stu-id="3aa2e-209">For more information see [Customize a default site design](customize-default-site-design.md)</span></span> |

<span data-ttu-id="3aa2e-210">Nachfolgend finden Sie ein Beispiel für das Erstellen eines neuen Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-210">Here's an example of creating a new site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteDesign",{
  info:{
    Title:"Contoso customer tracking",
    Description:"Creates customer list and applies standard theme",
    SiteScriptIds:["07702c07-0485-426f-b710-4704241caad9"],
    WebTemplate:"64",
    PreviewImageUrl: "https://contoso.sharepoint.com/SiteAssets/contoso-design.png",
    PreviewImageAltText: "Customer tracking site design theme"
    }
  });
```

<span data-ttu-id="3aa2e-211">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **CreateSiteDesign** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-211">Here is an example of the JSON returned after calling **CreateSiteDesign**.</span></span> <span data-ttu-id="3aa2e-212">Er enthält die ID des neuen Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-212">It contains the ID of the new site design.</span></span>

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignMetadata",
  "Description": "Creates customer list and applies standard theme",
  "PreviewImageAltText": "Customer tracking site design theme",
  "PreviewImageUrl": "https://contoso.sharepoint.com/SiteAssets/contoso-design.png",
  "SiteScriptIds": [ "07702c07-0485-426f-b710-4704241caad9" ],
  "Title": "Contoso customer tracking",
  "WebTemplate": "64",
  "Id": "614f9b28-3e85-4ec9-a961-5971ea086cca",
  "Version": 1
}
```

## <a name="getsitedesigns"></a><span data-ttu-id="3aa2e-213">GetSiteDesigns</span><span class="sxs-lookup"><span data-stu-id="3aa2e-213">GetSiteDesigns</span></span>

<span data-ttu-id="3aa2e-214">Abrufen einer Liste von Informationen zu vorhandenen Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-214">Gets a list of information on existing site designs.</span></span>

### <a name="parameters"></a><span data-ttu-id="3aa2e-215">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-215">Parameters</span></span>

<span data-ttu-id="3aa2e-216">Keine</span><span class="sxs-lookup"><span data-stu-id="3aa2e-216">None</span></span>

<span data-ttu-id="3aa2e-217">Nachfolgend finden Sie ein Beispiel zum Abrufen aller Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-217">Here's an example of getting all the site designs.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesigns");
```

<span data-ttu-id="3aa2e-218">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **GetSiteDesigns** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-218">Here is an example of the JSON returned after calling **GetSiteDesigns**.</span></span>

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Collection(Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignMetadata)",
  "value": [
    {
      "Description": "Tracks customer orders",
      "IsDefault": false,
      "PreviewImageAltText": null,
      "PreviewImageUrl": null,
      "SiteScriptIds": [ "6dfedb96-c090-44e3-875a-1c38032715fc" ],
      "Title": "customer orders",
      "WebTemplate": "64",
      "Id": "bbbd5740-ed97-461b-8b8e-e682f3fa167b",
      "Version": 1
    },
    {
      "Description": "Creates customer list and applies standard theme",
      "IsDefault": true,
      "PreviewImageAltText": "Customer tracking site design theme",
      "PreviewImageUrl": "https://contoso.sharepoint.com/SiteAssets/site_design.png",
      "SiteScriptIds": [ "07702c07-0485-426f-b710-4704241caad9" ],
      "Title": "Contoso customer tracking",
      "WebTemplate": "64",
      "Id": "614f9b28-3e85-4ec9-a961-5971ea086cca",
      "Version": 1
    }
  ]
}
```

## <a name="getsitedesignmetadata"></a><span data-ttu-id="3aa2e-219">GetSiteDesignMetadata</span><span class="sxs-lookup"><span data-stu-id="3aa2e-219">GetSiteDesignMetadata</span></span>

<span data-ttu-id="3aa2e-220">Abrufen von Informationen zu einem bestimmten Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-220">Gets information about a specific site design.</span></span>

### <a name="parameters"></a><span data-ttu-id="3aa2e-221">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-221">Parameters</span></span>

|<span data-ttu-id="3aa2e-222">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-222">Parameter</span></span>   | <span data-ttu-id="3aa2e-223">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3aa2e-223">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="3aa2e-224">id</span><span class="sxs-lookup"><span data-stu-id="3aa2e-224">id</span></span>         | <span data-ttu-id="3aa2e-225">Die ID des Websitedesigns, über das Informationen abgerufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-225">The ID of the site design to get information about.</span></span> |

<span data-ttu-id="3aa2e-226">Nachfolgend finden Sie ein Beispiel zum Abrufen von Informationen zu einem bestimmten Websitedesign nach ID.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-226">Here's an example of getting information about a specific site design by ID.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignMetadata", 
{id:"614f9b28-3e85-4ec9-a961-5971ea086cca"});
```

<span data-ttu-id="3aa2e-227">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **GetSiteDesignMetadata** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-227">Here is an example of the JSON returned after calling **GetSiteDesignMetadata**.</span></span>

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignMetadata",
  "Description": "Creates customer list and applies standard theme",
  "IsDefault": true,
  "PreviewImageAltText": "Customer tracking site design theme",
  "PreviewImageUrl": "https://contoso.sharepoint.com/SiteAssets/site_design.png",
  "SiteScriptIds": [ "07702c07-0485-426f-b710-4704241caad9" ],
  "Title": "Contoso customer tracking",
  "WebTemplate": "64",
  "Id": "614f9b28-3e85-4ec9-a961-5971ea086cca",
  "Version": 1
}
```

## <a name="updatesitedesign"></a><span data-ttu-id="3aa2e-228">UpdateSiteDesign</span><span class="sxs-lookup"><span data-stu-id="3aa2e-228">UpdateSiteDesign</span></span>

<span data-ttu-id="3aa2e-229">Aktualisieren eines Websitedesigns mit neuen Werten.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-229">Updates a site design with new values.</span></span> <span data-ttu-id="3aa2e-230">In dem REST-Aufruf sind mit Ausnahme der Website-Skript-ID optional. Hinweis: Wenn Sie zuvor den IsDefault-Parameter auf „true“ festgelegt haben und sie diese Einstellung beibehalten möchten, müssen Sie diesen Parameter erneut übergeben (andernfalls wird er auf „false“ zurückgesetzt).</span><span class="sxs-lookup"><span data-stu-id="3aa2e-230">In the REST call all parameters are optional except the site script Id. NOTE: if you had previously set the IsDefault parameter to TRUE and wish it to remain true, you must pass in this parameter again (otherwise it will be reset to FALSE).</span></span> 

### <a name="parameters"></a><span data-ttu-id="3aa2e-231">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-231">Parameters</span></span>

|<span data-ttu-id="3aa2e-232">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-232">Parameter</span></span>  | <span data-ttu-id="3aa2e-233">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3aa2e-233">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="3aa2e-234">Id</span><span class="sxs-lookup"><span data-stu-id="3aa2e-234">Id</span></span>         | <span data-ttu-id="3aa2e-235">Die ID des zu aktualisierenden Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-235">The ID of the site design to update.</span></span> |
|<span data-ttu-id="3aa2e-236">Titel</span><span class="sxs-lookup"><span data-stu-id="3aa2e-236">Title</span></span>                 |  <span data-ttu-id="3aa2e-237">(Optional) Der neue Anzeigename des aktualisierten Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-237">(optional) The new display name of the updated site design.</span></span> |
|<span data-ttu-id="3aa2e-238">WebTemplate</span><span class="sxs-lookup"><span data-stu-id="3aa2e-238">WebTemplate</span></span>           | <span data-ttu-id="3aa2e-239">(Optional) Die neue Vorlage, der das Websitedesign hinzugefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-239">(optional) The new template to add the site design to.</span></span> <span data-ttu-id="3aa2e-240">Verwenden Sie den Wert **64** für die Teamwebsite-Vorlage und den Wert **68** für die Kommunikationswebsitevorlage.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-240">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="3aa2e-241">SiteScripts</span><span class="sxs-lookup"><span data-stu-id="3aa2e-241">SiteScripts</span></span>           | <span data-ttu-id="3aa2e-242">(Optional) Ein neues Array von einem oder mehreren Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-242">(optional) A new array of one or more site scripts.</span></span> <span data-ttu-id="3aa2e-243">Jedes wird durch eine ID identifziert.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-243">Each is identified by an ID.</span></span> <span data-ttu-id="3aa2e-244">Die Skripts werden in der aufgeführten Reihenfolge ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-244">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="3aa2e-245">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3aa2e-245">Description</span></span>         | <span data-ttu-id="3aa2e-246">(Optional) Die neue Anzeigebeschreibung des aktualisierten Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-246">(Optional) The new display description of updated site design.</span></span> |
|<span data-ttu-id="3aa2e-247">PreviewImageUrl</span><span class="sxs-lookup"><span data-stu-id="3aa2e-247">PreviewImageUrl</span></span>     | <span data-ttu-id="3aa2e-248">(Optional) Die neue URL eines Vorschaubilds.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-248">(Optional) The new URL of a preview image.</span></span> |
|<span data-ttu-id="3aa2e-249">PreviewImageAltText</span><span class="sxs-lookup"><span data-stu-id="3aa2e-249">PreviewImageAltText</span></span> | <span data-ttu-id="3aa2e-250">(Optional) Die neue Alternativtextbeschreibung des Bilds für Barrierefreiheit.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-250">(Optional) The new alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="3aa2e-251">IsDefault</span><span class="sxs-lookup"><span data-stu-id="3aa2e-251">IsDefault</span></span>           | <span data-ttu-id="3aa2e-252">(Optional) **True**, wenn das Websitedesign als Standarddesign der Website angewendet wird; andernfalls **False**.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-252">(Optional) **true** if the site design is applied as the default site design; otherwise, **false**.</span></span> <span data-ttu-id="3aa2e-253">Weitere Informationen finden Sie unter [Anpassen eines standardmäßigen Websitedesigns](customize-default-site-design.md).</span><span class="sxs-lookup"><span data-stu-id="3aa2e-253">For more information see [Customize a default site design](customize-default-site-design.md)</span></span> |

<span data-ttu-id="3aa2e-254">Nachfolgend finden Sie ein Beispiel, in dem jeder Wert in einem vorhandenen Websitedesign aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-254">Here's an example that updates every value on an existing site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.UpdateSiteDesign",
 {updateInfo:{
   Id:"614f9b28-3e85-4ec9-a961-5971ea086cca", 
   Title:"Contoso customer site", 
   Description:"Creates site with customer theme and list", 
   SiteScriptIds:["6b2b79e4-5da3-4352-8565-42a896fabd57","2b997981-258b-4e1e-81ff-f6fbf7235a1f"], 
   PreviewImageUrl:"https://contoso.sharepoint.com/SiteAssets/customer_site.png",
   PreviewImageAltText:"Customer site with list and theme", 
   WebTemplate:"68", 
   Version: 7, 
   IsDefault: false}});
```

<span data-ttu-id="3aa2e-255">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **UpdateSiteDesign** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-255">Here is an example of the JSON returned after calling **UpdateSiteDesign**.</span></span>

```json{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignMetadata",
  "Description": "Creates site with customer theme and list",
  "IsDefault": false,
  "PreviewImageAltText": "Customer site with list and theme",
  "PreviewImageUrl": "https://contoso.sharepoint.com/SiteAssets/customer_site.png",
  "SiteScriptIds": [ "6b2b79e4-5da3-4352-8565-42a896fabd57", "2b997981-258b-4e1e-81ff-f6fbf7235a1f" ],
  "Title": "Contoso customer site",
  "WebTemplate": "68",
  "Id": "614f9b28-3e85-4ec9-a961-5971ea086cca",
  "Version": 7
}
```

## <a name="deletesitedesign"></a><span data-ttu-id="3aa2e-256">DeleteSiteDesign</span><span class="sxs-lookup"><span data-stu-id="3aa2e-256">DeleteSiteDesign</span></span>

<span data-ttu-id="3aa2e-257">Löscht ein Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-257">Deletes a site design.</span></span>

### <a name="parameters"></a><span data-ttu-id="3aa2e-258">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-258">Parameters</span></span>

|<span data-ttu-id="3aa2e-259">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-259">Parameter</span></span>   | <span data-ttu-id="3aa2e-260">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3aa2e-260">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="3aa2e-261">id</span><span class="sxs-lookup"><span data-stu-id="3aa2e-261">id</span></span>         | <span data-ttu-id="3aa2e-262">Die ID des zu löschenden Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-262">The ID of the site design to delete.</span></span> |

<span data-ttu-id="3aa2e-263">Nachfolgend finden Sie ein Beispiel zum Löschen eines Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-263">Here's an example of deleting a site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteDesign", 
{id:"f9e76746-5076-4bd2-bad3-e611c488fa85"});
```

## <a name="getsitedesignrights"></a><span data-ttu-id="3aa2e-264">GetSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="3aa2e-264">GetSiteDesignRights</span></span>

<span data-ttu-id="3aa2e-265">Abrufen einer Liste von Prinzipalen, die Zugriff auf ein Websitedesign haben.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-265">Gets a list of principals that have access to a site design.</span></span>


### <a name="parameters"></a><span data-ttu-id="3aa2e-266">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-266">Parameters</span></span>

|<span data-ttu-id="3aa2e-267">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-267">Parameter</span></span>   | <span data-ttu-id="3aa2e-268">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3aa2e-268">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="3aa2e-269">id</span><span class="sxs-lookup"><span data-stu-id="3aa2e-269">id</span></span>         | <span data-ttu-id="3aa2e-270">Die ID des Websitedesigns, über das Berechtigungsinformationen abgerufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-270">The ID of the site design to get rights information from.</span></span> |

<span data-ttu-id="3aa2e-271">Nachfolgend finden Sie ein Beispiel zum Abrufen der Anzeigeberechtigungen für ein bestimmtes Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-271">Here's an example of getting view rights for a specific site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignRights", 
{id:"dc076f7b-6c15-4d76-8f85-948a17f5dd18"});
```

<span data-ttu-id="3aa2e-272">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **GetSiteDesignRights** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-272">Here is an example of the JSON returned after calling **GetSiteDesignRights**.</span></span>

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#SiteDesignPrincipals",
  "value": [
    {
      "@odata.type": "#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignPrincipal",
      "@odata.id": "https://contoso.sharepoint.com/_api/Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignPrincipalfca62a9f-e43e-49a0-9139-6ae4df212859",
      "@odata.editLink": "Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignPrincipalfca62a9f-e43e-49a0-9139-6ae4df212859",
      "DisplayName": "Nestor Wilke",
      "PrincipalName": "i:0#.f|membership|nestorw@contoso.onmicrosoft.com",
      "Rights": 1
    },
    {
      "@odata.type": "#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignPrincipal",
      "@odata.id": "https://contoso.sharepoint.com/_api/Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignPrincipalce4cd6f6-553b-4a55-9364-1d39125be0ef",
      "@odata.editLink": "Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignPrincipalce4cd6f6-553b-4a55-9364-1d39125be0ef",
      "DisplayName": "Patti Fernandez",
      "PrincipalName": "i:0#.f|membership|pattif@contoso.onmicrosoft.com",
      "Rights": 1
    }
  ]
}
```

## <a name="grantsitedesignrights"></a><span data-ttu-id="3aa2e-273">GrantSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="3aa2e-273">GrantSiteDesignRights</span></span>

<span data-ttu-id="3aa2e-274">Erteilen von Zugriff auf ein Websitedesign für einen oder mehrere Prinzipale.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-274">Grants access to a site design for one or more principals.</span></span>

### <a name="parameters"></a><span data-ttu-id="3aa2e-275">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-275">Parameters</span></span>

|<span data-ttu-id="3aa2e-276">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-276">Parameter</span></span>   | <span data-ttu-id="3aa2e-277">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3aa2e-277">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="3aa2e-278">id</span><span class="sxs-lookup"><span data-stu-id="3aa2e-278">id</span></span>         | <span data-ttu-id="3aa2e-279">Die ID des Websitedesigns, für das Berechtigungen gewährt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-279">The ID of the site design to grant rights on.</span></span> |
| <span data-ttu-id="3aa2e-280">principalNames</span><span class="sxs-lookup"><span data-stu-id="3aa2e-280">principalNames</span></span> | <span data-ttu-id="3aa2e-281">Ein Array von einem oder mehreren Prinzipalen, denen Anzeigeberechtigungen gewährt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-281">An array of one or more principals to grant view rights.</span></span> <span data-ttu-id="3aa2e-282">Prinzipale können Benutzer oder E-Mail-aktivierte Sicherheitsgruppen in der Form „Alias“ oder „Alias@\<*Domänenname*\>.com“ sein.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-282">Principals can be users or mail-enabled security groups in the form of "alias" or "alias@\<*domain name*\>.com"</span></span> |
| <span data-ttu-id="3aa2e-283">grantedRights</span><span class="sxs-lookup"><span data-stu-id="3aa2e-283">grantedRights</span></span> | <span data-ttu-id="3aa2e-284">Stets auf **1** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-284">Always set to **1**.</span></span> <span data-ttu-id="3aa2e-285">Dies steht für die Berechtigung **View**.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-285">This represents the **View** right.</span></span> |

<span data-ttu-id="3aa2e-286">Nachfolgend finden Sie ein Beispiel zum Gewähren von Anzeigeberechtigungen für ein Websitedesign für Nestor und Patti (fiktive Benutzer bei Contoso).</span><span class="sxs-lookup"><span data-stu-id="3aa2e-286">Here's an example of granting view rights to a site design for Nestor and Patti (fictional users at Contoso.)</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GrantSiteDesignRights", {
  "id": "dc076f7b-6c15-4d76-8f85-948a17f5dd18",
  "principalNames": [ "NestorW@contoso.onmicrosoft.com", "PattiF@contoso.onmicrosoft.com" ],
  "grantedRights": 1
});
```

## <a name="revokesitedesignrights"></a><span data-ttu-id="3aa2e-287">RevokeSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="3aa2e-287">RevokeSiteDesignRights</span></span>

<span data-ttu-id="3aa2e-288">Widerrufen des Zugriffs auf ein Websitedesign für einen oder mehrere Prinzipale.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-288">Revokes access from a site design for one or more principals.</span></span>

### <a name="parameters"></a><span data-ttu-id="3aa2e-289">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-289">Parameters</span></span>

|<span data-ttu-id="3aa2e-290">Parameter</span><span class="sxs-lookup"><span data-stu-id="3aa2e-290">Parameter</span></span>   | <span data-ttu-id="3aa2e-291">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3aa2e-291">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="3aa2e-292">id</span><span class="sxs-lookup"><span data-stu-id="3aa2e-292">id</span></span>         | <span data-ttu-id="3aa2e-293">Die ID des Websitedesigns, von dem Berechtigungen widerrufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-293">The ID of the site design to revoke rights from.</span></span> |
| <span data-ttu-id="3aa2e-294">principalNames</span><span class="sxs-lookup"><span data-stu-id="3aa2e-294">principalNames</span></span> | <span data-ttu-id="3aa2e-295">Ein Array von einem oder mehreren Prinzipalen, von denen Anzeigeberechtigungen widerrufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-295">An array of one or more principals to revoke view rights from.</span></span> <span data-ttu-id="3aa2e-296">Wenn für alle Prinzipale Berechtigungen für das Websitedesign widerrufen werden, ist die Seite für jeden sichtbar.</span><span class="sxs-lookup"><span data-stu-id="3aa2e-296">If all principals have rights revoked on the site design, the site design becomes viewable to everyone.</span></span> |

<span data-ttu-id="3aa2e-297">Nachfolgend finden Sie ein Beispiel zum Widerrufen von Anzeigeberechtigungen für ein Websitedesign für Patti (fiktiver Benutzer bei Contoso).</span><span class="sxs-lookup"><span data-stu-id="3aa2e-297">Here's an example of revoking view rights from a site design for Patti (fictional user at Contoso.)</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.RevokeSiteDesignRights", 
{id:"5d4756e9-e1f5-42f7-afa7-5fa5aac170aa",
 principalNames:["debrab@Contoso.sharepoint.com"] });
```
