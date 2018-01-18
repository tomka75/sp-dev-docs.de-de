---
title: REST-API von SharePoint-Websitedesigns
description: "Verwenden Sie SharePoint-Websitedesigns über die SharePoint-REST-Schnittstelle, um grundlegende CRUD-Operationen (Create, Read, Update, Delete, also Erstellen, Lesen, Aktualisieren und Löschen) auszuführen."
ms.date: 12/14/2017
ms.openlocfilehash: 618f8b0bb7eed7a3bf60bdd86363e095fb0a8221
ms.sourcegitcommit: 6f2b3b5bd81c2de4f761e10ed5e2f0b9c3c485bf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="site-design-and-site-script-rest-api"></a><span data-ttu-id="9b7de-103">REST-API von SharePoint-Websitedesigns und Websiteskripts</span><span class="sxs-lookup"><span data-stu-id="9b7de-103">Site design and site script REST API</span></span>

> [!NOTE]
> <span data-ttu-id="9b7de-104">Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden.</span><span class="sxs-lookup"><span data-stu-id="9b7de-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="9b7de-105">Sie werden in Produktionsumgebungen derzeit nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="9b7de-105">They are not currently supported for use in production environments.</span></span>

<span data-ttu-id="9b7de-106">Mithilfe der SharePoint-REST-Schnittstelle können Sie grundlegende CRUD-Operationen ausführen, d. h: Erstellen, Lesen, Aktualisieren und Löschen (Create, Read, Update, Delete).</span><span class="sxs-lookup"><span data-stu-id="9b7de-106">You can use the the SharePoint REST interface to perform basic create, read, update, and delete (CRUD) operations on site themes.</span></span>

<span data-ttu-id="9b7de-107">Der REST-Dienst in SharePoint Online (sowie in lokalen Bereitstellungen von SharePoint 2016 und höher) erlaubt die Zusammenfassung mehrerer Anforderungen in einem einzigen Aufruf an den Service mittels der ODATA-Abfrageoption „$batch“.</span><span class="sxs-lookup"><span data-stu-id="9b7de-107">The SharePoint Online (and SharePoint 2016 and later on-premises) REST service supports combining multiple requests into a single call to the service by using the OData $batch query option.</span></span> <span data-ttu-id="9b7de-108">Einzelheiten und Links zu Codebeispielen finden Sie unter [Durchführen von Batchanforderungen mit den REST-APIs](https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="9b7de-108">For details and links to code samples, see [Make batch requests with the REST APIs](https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b7de-109">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="9b7de-109">Prerequisites</span></span>
<span data-ttu-id="9b7de-110">Lesen Sie vor der Umsetzung der Beispiele in diesem Artikel zunächst die folgenden Artikel:</span><span class="sxs-lookup"><span data-stu-id="9b7de-110">Before you get started, make sure that you're familiar with the following:</span></span>
- [<span data-ttu-id="9b7de-111">Grundlegendes zum SharePoint-REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="9b7de-111">Get to know the SharePoint REST service</span></span>](https://dev.office.com/sharepoint/docs/apis/rest/get-to-know-the-sharepoint-rest-service.md) 
- [<span data-ttu-id="9b7de-112">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="9b7de-112">Complete basic operations using SharePoint REST endpoints</span></span>](https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints.md)

## <a name="rest-commands"></a><span data-ttu-id="9b7de-113">REST-Befehle</span><span class="sxs-lookup"><span data-stu-id="9b7de-113">REST commands</span></span>

<span data-ttu-id="9b7de-114">Für Websitedesigns und Websiteskripts stehen die folgenden REST-Befehle zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="9b7de-114">The following REST commands are available for working with site themes:</span></span>

- <span data-ttu-id="9b7de-115">**CreateSiteScript** &mdash; Erstellen eines neuen Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="9b7de-115">**CreateSiteScript** &mdash; Creates a new site script.</span></span>
- <span data-ttu-id="9b7de-116">**GetSiteScripts** &mdash; Abrufen einer Liste von Informationen zu vorhandenen Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="9b7de-116">**GetSiteScripts** &mdash; Gets a list of information on existing site scripts.</span></span>
- <span data-ttu-id="9b7de-117">**GetSiteScriptMetadata** &mdash; Abrufen von Informationen zu einem bestimmten Websiteskript.</span><span class="sxs-lookup"><span data-stu-id="9b7de-117">**GetSiteScriptMetadata** &mdash; Gets information about a specific site script.</span></span>
- <span data-ttu-id="9b7de-118">**UpdateSiteScript** &mdash; Aktualisieren eines Websiteskripts mit neuen Werten.</span><span class="sxs-lookup"><span data-stu-id="9b7de-118">**UpdateSiteScript** &mdash; Updates a site script with new values.</span></span>
- <span data-ttu-id="9b7de-119">**DeleteSiteScript** &mdash; Löschen eines Websitekripts.</span><span class="sxs-lookup"><span data-stu-id="9b7de-119">**DeleteSiteScript** &mdash; Deletes a site script.</span></span>
- <span data-ttu-id="9b7de-120">**CreateSiteDesign** &mdash; Erstellen eines Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="9b7de-120">**CreateSiteDesign** &mdash; Creates a site design.</span></span>
- <span data-ttu-id="9b7de-121">**GetSiteDesigns** &mdash; Abrufen einer Liste von Informationen zu vorhandenen Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="9b7de-121">**GetSiteDesigns** &mdash; Gets a list of information on existing site designs.</span></span>
- <span data-ttu-id="9b7de-122">**GetSiteDesignMetadata** &mdash; Abrufen von Informationen zu einem bestimmten Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="9b7de-122">**GetSiteDesignMetadata** &mdash; Gets information about a sepcific site design.</span></span>
- <span data-ttu-id="9b7de-123">**UpdateSiteDesign** &mdash; Aktualisieren eines Websitedesigns mit neuen Werten.</span><span class="sxs-lookup"><span data-stu-id="9b7de-123">**UpdateSiteDesign** &mdash; Updates a site design with new values.</span></span>
- <span data-ttu-id="9b7de-124">**DeleteSiteDesign** &mdash; Löschen eines Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="9b7de-124">**DeleteSiteDesign** &mdash; Deletes a site design.</span></span>
- <span data-ttu-id="9b7de-125">**GetSiteDesignRights** &mdash; Abrufen einer Liste von Prinzipalen, die Zugriff auf ein Websitedesign haben.</span><span class="sxs-lookup"><span data-stu-id="9b7de-125">**GetSiteDesignRights** &mdash; Gets a list of principals that have access to a site design.</span></span>
- <span data-ttu-id="9b7de-126">**GrantSiteDesignRights** &mdash; Erteilen von Zugriff auf ein Websitedesign für einen oder mehrere Prinzipale.</span><span class="sxs-lookup"><span data-stu-id="9b7de-126">**GrantSiteDesignRights** &mdash; Grants access to a site design for one or more principals.</span></span>
- <span data-ttu-id="9b7de-127">**RevokeSiteDesignRights** &mdash; Widerrufen des Zugriffs auf ein Websitedesign für einen oder mehrere Prinzipale.</span><span class="sxs-lookup"><span data-stu-id="9b7de-127">**RevokeSiteDesignRights** &mdash; Revokes access from a site design for one or more principals.</span></span>

## <a name="create-a-function-to-send-rest-requests"></a><span data-ttu-id="9b7de-128">Erstellen einer Funktion zum Senden von REST-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="9b7de-128">Create a function to send REST requests</span></span>

<span data-ttu-id="9b7de-129">Zum Arbeiten mit der REST-API wird empfohlen, eine Hilfsfunktion für die REST-Aufrufe zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="9b7de-129">To work with the REST API we recommend creating a helper function to make the REST calls.</span></span> <span data-ttu-id="9b7de-130">Die folgende **RestRequest**-Funktion ruft die im **url**-Parameter angegebene REST-Methode auf und übergibt die weiteren Parameter in **params**.</span><span class="sxs-lookup"><span data-stu-id="9b7de-130">The following **RestRequest** function will call the REST method specified in the **url** parameter and pass the additional parameters in **params**.</span></span>

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

## <a name="createsitescript"></a><span data-ttu-id="9b7de-131">CreateSiteScript</span><span class="sxs-lookup"><span data-stu-id="9b7de-131">CreateSiteScript</span></span>

<span data-ttu-id="9b7de-132">Erstellt ein neues Websiteskript.</span><span class="sxs-lookup"><span data-stu-id="9b7de-132">Creates a new site script.</span></span>

### <a name="parameters"></a><span data-ttu-id="9b7de-133">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-133">Parameters</span></span>

|<span data-ttu-id="9b7de-134">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-134">Parameter</span></span>     | <span data-ttu-id="9b7de-135">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b7de-135">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="9b7de-136">Titel</span><span class="sxs-lookup"><span data-stu-id="9b7de-136">Title</span></span>       | <span data-ttu-id="9b7de-137">Der Anzeigename des Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="9b7de-137">The display name of the web site.</span></span> |
| <span data-ttu-id="9b7de-138">Inhalt</span><span class="sxs-lookup"><span data-stu-id="9b7de-138">Content</span></span>     | <span data-ttu-id="9b7de-139">JSON-Wert, der das Skript beschreibt.</span><span class="sxs-lookup"><span data-stu-id="9b7de-139">JSON value that describes the script.</span></span> <span data-ttu-id="9b7de-140">Weitere Informationen finden Sie unter [JSON-Referenz](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="9b7de-140">For more information, see [JSON reference](site-design-json-schema.md).</span></span>|

<span data-ttu-id="9b7de-141">Im folgenden Beispiel wird ein neues Websiteskript erstellt, das ein benutzerdefiniertes Design anwendet.</span><span class="sxs-lookup"><span data-stu-id="9b7de-141">The following example creates a new site script that applies a custom theme.</span></span>

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

<span data-ttu-id="9b7de-142">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **CreateSiteScript** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="9b7de-142">Here is an example of the JSON returned after calling **CreateSiteScript**.</span></span> <span data-ttu-id="9b7de-143">Er enthält die ID des neuen Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="9b7de-143">It contains the ID of the new site script.</span></span>

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

## <a name="getsitescripts"></a><span data-ttu-id="9b7de-144">GetSiteScripts</span><span class="sxs-lookup"><span data-stu-id="9b7de-144">GetSiteScripts</span></span>

<span data-ttu-id="9b7de-145">Abrufen einer Liste von Informationen zu allen vorhandenen Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="9b7de-145">Gets a list of information on all existing site scripts.</span></span>

### <a name="parameters"></a><span data-ttu-id="9b7de-146">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-146">Parameters</span></span>

<span data-ttu-id="9b7de-147">Keine</span><span class="sxs-lookup"><span data-stu-id="9b7de-147">None.</span></span>

<span data-ttu-id="9b7de-148">Im folgenden Beispiel werden die Websiteskriptinformationen für alle Websiteskripts abgerufen.</span><span class="sxs-lookup"><span data-stu-id="9b7de-148">The following example gets the site script information for all site scripts.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScripts");
```

<span data-ttu-id="9b7de-149">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **GetSiteScripts** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="9b7de-149">Here is an example of the JSON returned after calling **GetSiteScripts**.</span></span>

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

## <a name="getsitescriptmetadata"></a><span data-ttu-id="9b7de-150">GetSiteScriptMetadata</span><span class="sxs-lookup"><span data-stu-id="9b7de-150">GetSiteScriptMetadata</span></span>

<span data-ttu-id="9b7de-151">Abrufen von Informationen zu einem bestimmten Websiteskript.</span><span class="sxs-lookup"><span data-stu-id="9b7de-151">Gets information about a specific site script.</span></span> <span data-ttu-id="9b7de-152">Es wird auch der JSON-Code des Skripts zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="9b7de-152">It also returns the JSON of the script.</span></span>

### <a name="parameters"></a><span data-ttu-id="9b7de-153">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-153">Parameters</span></span>

|<span data-ttu-id="9b7de-154">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-154">Parameter</span></span>     | <span data-ttu-id="9b7de-155">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b7de-155">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="9b7de-156">id</span><span class="sxs-lookup"><span data-stu-id="9b7de-156">id</span></span>    | <span data-ttu-id="9b7de-157">Die ID des Websiteskripts, über das Informationen abgerufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="9b7de-157">The ID of the site script to get information about.</span></span> |

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScriptMetadata",
{id:"07702c07-0485-426f-b710-4704241caad9"});
```

<span data-ttu-id="9b7de-158">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **GetSiteScriptMetadata** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="9b7de-158">Here is an example of the JSON returned after calling **GetSiteScriptMetadata**.</span></span>

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

## <a name="updatesitescript"></a><span data-ttu-id="9b7de-159">UpdateSiteScript</span><span class="sxs-lookup"><span data-stu-id="9b7de-159">UpdateSiteScript</span></span>

<span data-ttu-id="9b7de-160">Aktualisieren eines Websiteskripts mit neuen Werten.</span><span class="sxs-lookup"><span data-stu-id="9b7de-160">Updates a site script with new values.</span></span>

### <a name="parameters"></a><span data-ttu-id="9b7de-161">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-161">Parameters</span></span>

|<span data-ttu-id="9b7de-162">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-162">Parameter</span></span>   | <span data-ttu-id="9b7de-163">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b7de-163">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="9b7de-164">Id</span><span class="sxs-lookup"><span data-stu-id="9b7de-164">Id</span></span>         | <span data-ttu-id="9b7de-165">Die ID des zu aktualisierenden Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="9b7de-165">The ID of the site script to update.</span></span> |
|<span data-ttu-id="9b7de-166">Titel</span><span class="sxs-lookup"><span data-stu-id="9b7de-166">Title</span></span>       | <span data-ttu-id="9b7de-167">(optional) Der neue Anzeigename des Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="9b7de-167">(optional) The new display name of the site script.</span></span> |
|<span data-ttu-id="9b7de-168">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b7de-168">Description</span></span> | <span data-ttu-id="9b7de-169">(Optional) Die neue Beschreibung des Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="9b7de-169">(Optional) The new description of the site script.</span></span> |
| <span data-ttu-id="9b7de-170">Version</span><span class="sxs-lookup"><span data-stu-id="9b7de-170">Version</span></span>    | <span data-ttu-id="9b7de-171">(Optional) Die neue Versionsnummer des Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="9b7de-171">(Optional) The new version number of the site script.</span></span> |
| <span data-ttu-id="9b7de-172">Inhalt</span><span class="sxs-lookup"><span data-stu-id="9b7de-172">Content</span></span>    | <span data-ttu-id="9b7de-173">(Optional) Ein neues JSON-Skript, das die Skriptaktionen definiert.</span><span class="sxs-lookup"><span data-stu-id="9b7de-173">(Optional) A new JSON script defining the script actions.</span></span> <span data-ttu-id="9b7de-174">Weitere Informationen finden Sie unter [JSON-Schema eines Websitedesigns](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="9b7de-174">For more information, see [Site design JSON schema](site-design-json-schema.md)</span></span> |

<span data-ttu-id="9b7de-175">Nachfolgend finden Sie ein Beispiel des Aktualisierens eines vorhandenen Websiteskripts mit einem neuen JSON-Skript und neuen Werten.</span><span class="sxs-lookup"><span data-stu-id="9b7de-175">Here's an example of updating an existing site script with a new JSON script and values.</span></span>

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

<span data-ttu-id="9b7de-176">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **UpdateSiteScript** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="9b7de-176">Here is an example of the JSON returned after calling **UpdateSiteScript**.</span></span>

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

## <a name="deletesitescript"></a><span data-ttu-id="9b7de-177">DeleteSiteScript</span><span class="sxs-lookup"><span data-stu-id="9b7de-177">DeleteSiteScript</span></span>

<span data-ttu-id="9b7de-178">Löschen eines Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="9b7de-178">Deletes a site script.</span></span>

### <a name="parameters"></a><span data-ttu-id="9b7de-179">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-179">Parameters</span></span>

|<span data-ttu-id="9b7de-180">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-180">Parameter</span></span>   | <span data-ttu-id="9b7de-181">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b7de-181">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="9b7de-182">id</span><span class="sxs-lookup"><span data-stu-id="9b7de-182">id</span></span>         | <span data-ttu-id="9b7de-183">Die ID des zu löschenden Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="9b7de-183">The ID of the item to delete.</span></span> |

<span data-ttu-id="9b7de-184">Nachfolgend finden Sie ein Beispiel zum Löschen eines Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="9b7de-184">Here's an example of deleting a site script.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteScript", 
{id:"07702c07-0485-426f-b710-4704241caad9"});
```

## <a name="createsitedesign"></a><span data-ttu-id="9b7de-185">CreateSiteDesign</span><span class="sxs-lookup"><span data-stu-id="9b7de-185">CreateSiteDesign</span></span>

<span data-ttu-id="9b7de-186">Erstellen eines neues Websitedesigns, das für Benutzer beim Erstellen einer neuen Website von der SharePoint-Startseite verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="9b7de-186">Creates a new site design available to users when they create a new site from the SharePoint home page.</span></span>

### <a name="parameters"></a><span data-ttu-id="9b7de-187">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-187">Parameters</span></span>

|<span data-ttu-id="9b7de-188">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-188">Parameter</span></span>  | <span data-ttu-id="9b7de-189">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b7de-189">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="9b7de-190">Titel</span><span class="sxs-lookup"><span data-stu-id="9b7de-190">Title</span></span>                 | <span data-ttu-id="9b7de-191">Der Anzeigename des Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="9b7de-191">The display name of the web site.</span></span> |
|<span data-ttu-id="9b7de-192">WebTemplate</span><span class="sxs-lookup"><span data-stu-id="9b7de-192">WebTemplate</span></span>           | <span data-ttu-id="9b7de-193">Identifiziert, zu welcher Basisvorlage das Design hinzugefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="9b7de-193">Identifies which base template to add the design to.</span></span> <span data-ttu-id="9b7de-194">Verwenden Sie den Wert **64** für die Teamwebsite-Vorlage und den Wert **68** für die Kommunikationswebsitevorlage.</span><span class="sxs-lookup"><span data-stu-id="9b7de-194">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="9b7de-195">SiteScripts</span><span class="sxs-lookup"><span data-stu-id="9b7de-195">SiteScripts</span></span>           | <span data-ttu-id="9b7de-196">Ein Array von einem oder mehreren Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="9b7de-196">An array of one or more site scripts.</span></span> <span data-ttu-id="9b7de-197">Jedes wird durch eine ID identifziert.</span><span class="sxs-lookup"><span data-stu-id="9b7de-197">Each is identified by an ID.</span></span> <span data-ttu-id="9b7de-198">Die Skripts werden in der aufgeführten Reihenfolge ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="9b7de-198">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="9b7de-199">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b7de-199">Description</span></span>         | <span data-ttu-id="9b7de-200">(Optional) Die Anzeigebeschreibung des Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="9b7de-200">(Optional) The display description of site design.</span></span> |
|<span data-ttu-id="9b7de-201">PreviewImageUrl</span><span class="sxs-lookup"><span data-stu-id="9b7de-201">PreviewImageUrl</span></span>     | <span data-ttu-id="9b7de-202">(optional) Die URL eines Vorschaubilds.</span><span class="sxs-lookup"><span data-stu-id="9b7de-202">(Optional) The URL of a preview image.</span></span> <span data-ttu-id="9b7de-203">Wenn keine angegeben ist, verwendet SharePoint ein allgemeines Bild.</span><span class="sxs-lookup"><span data-stu-id="9b7de-203">If none is specified SharePoint will use a generic image.</span></span> |
|<span data-ttu-id="9b7de-204">PreviewImageAltText</span><span class="sxs-lookup"><span data-stu-id="9b7de-204">PreviewImageAltText</span></span> | <span data-ttu-id="9b7de-205">(Optional) Die Alternativtextbeschreibung des Bilds für Barrierefreiheit.</span><span class="sxs-lookup"><span data-stu-id="9b7de-205">(Optional) The alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="9b7de-206">IsDefault</span><span class="sxs-lookup"><span data-stu-id="9b7de-206">isDefault</span></span>           | <span data-ttu-id="9b7de-207">(Optional) **True**, wenn das Websitedesign als Standarddesign der Website angewendet wird; andernfalls **False**.</span><span class="sxs-lookup"><span data-stu-id="9b7de-207">(Optional) **true** if the site design is applied as the default site design; otherwise, **false**.</span></span> <span data-ttu-id="9b7de-208">Weitere Informationen finden Sie unter [Anpassen eines standardmäßigen Websitedesigns](customize-default-site-design.md).</span><span class="sxs-lookup"><span data-stu-id="9b7de-208">For more information see [Customize a default site design](customize-default-site-design.md)</span></span> |

<span data-ttu-id="9b7de-209">Nachfolgend finden Sie ein Beispiel für das Erstellen eines neuen Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="9b7de-209">Here's an example of creating a new site design.</span></span>

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

<span data-ttu-id="9b7de-210">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **CreateSiteDesign** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="9b7de-210">Here is an example of the JSON returned after calling **CreateSiteDesign**.</span></span> <span data-ttu-id="9b7de-211">Er enthält die ID des neuen Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="9b7de-211">It contains the ID of the new site design.</span></span>

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

## <a name="getsitedesigns"></a><span data-ttu-id="9b7de-212">GetSiteDesigns</span><span class="sxs-lookup"><span data-stu-id="9b7de-212">GetSiteDesigns</span></span>

<span data-ttu-id="9b7de-213">Abrufen einer Liste von Informationen zu vorhandenen Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="9b7de-213">Gets a list of information on existing site designs.</span></span>

### <a name="parameters"></a><span data-ttu-id="9b7de-214">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-214">Parameters</span></span>

<span data-ttu-id="9b7de-215">Keine</span><span class="sxs-lookup"><span data-stu-id="9b7de-215">None</span></span>

<span data-ttu-id="9b7de-216">Nachfolgend finden Sie ein Beispiel zum Abrufen aller Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="9b7de-216">Here's an example of getting all the site designs.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesigns");
```

<span data-ttu-id="9b7de-217">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **GetSiteDesigns** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="9b7de-217">Here is an example of the JSON returned after calling **GetSiteDesigns**.</span></span>

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

## <a name="getsitedesignmetadata"></a><span data-ttu-id="9b7de-218">GetSiteDesignMetadata</span><span class="sxs-lookup"><span data-stu-id="9b7de-218">GetSiteDesignMetadata</span></span>

<span data-ttu-id="9b7de-219">Abrufen von Informationen zu einem bestimmten Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="9b7de-219">Gets information about a specific site design.</span></span>

### <a name="parameters"></a><span data-ttu-id="9b7de-220">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-220">Parameters</span></span>

|<span data-ttu-id="9b7de-221">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-221">Parameter</span></span>   | <span data-ttu-id="9b7de-222">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b7de-222">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="9b7de-223">id</span><span class="sxs-lookup"><span data-stu-id="9b7de-223">id</span></span>         | <span data-ttu-id="9b7de-224">Die ID des Websitedesigns, über das Informationen abgerufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="9b7de-224">The ID of the site design to get information about.</span></span> |

<span data-ttu-id="9b7de-225">Nachfolgend finden Sie ein Beispiel zum Abrufen von Informationen zu einem bestimmten Websitedesign nach ID.</span><span class="sxs-lookup"><span data-stu-id="9b7de-225">Here's an example of getting information about a specific site design by ID.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignMetadata", 
{id:"614f9b28-3e85-4ec9-a961-5971ea086cca"});
```

<span data-ttu-id="9b7de-226">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **GetSiteDesignMetadata** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="9b7de-226">Here is an example of the JSON returned after calling **GetSiteDesignMetadata**.</span></span>

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

## <a name="updatesitedesign"></a><span data-ttu-id="9b7de-227">UpdateSiteDesign</span><span class="sxs-lookup"><span data-stu-id="9b7de-227">UpdateSiteDesign</span></span>

<span data-ttu-id="9b7de-228">Aktualisieren eines Websitedesigns mit neuen Werten.</span><span class="sxs-lookup"><span data-stu-id="9b7de-228">Updates a site design with new values.</span></span>

### <a name="parameters"></a><span data-ttu-id="9b7de-229">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-229">Parameters</span></span>

|<span data-ttu-id="9b7de-230">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-230">Parameter</span></span>  | <span data-ttu-id="9b7de-231">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b7de-231">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="9b7de-232">Id</span><span class="sxs-lookup"><span data-stu-id="9b7de-232">Id</span></span>         | <span data-ttu-id="9b7de-233">Die ID des zu aktualisierenden Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="9b7de-233">The ID of the site design to update.</span></span> |
|<span data-ttu-id="9b7de-234">Titel</span><span class="sxs-lookup"><span data-stu-id="9b7de-234">Title</span></span>                 |  <span data-ttu-id="9b7de-235">(Optional) Der neue Anzeigename des aktualisierten Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="9b7de-235">(optional) The new display name of the updated site design.</span></span> |
|<span data-ttu-id="9b7de-236">WebTemplate</span><span class="sxs-lookup"><span data-stu-id="9b7de-236">WebTemplate</span></span>           | <span data-ttu-id="9b7de-237">(Optional) Die neue Vorlage, der das Websitedesign hinzugefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="9b7de-237">(optional) The new template to add the site design to.</span></span> <span data-ttu-id="9b7de-238">Verwenden Sie den Wert **64** für die Teamwebsite-Vorlage und den Wert **68** für die Kommunikationswebsitevorlage.</span><span class="sxs-lookup"><span data-stu-id="9b7de-238">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="9b7de-239">SiteScripts</span><span class="sxs-lookup"><span data-stu-id="9b7de-239">SiteScripts</span></span>           | <span data-ttu-id="9b7de-240">(Optional) Ein neues Array von einem oder mehreren Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="9b7de-240">(optional) A new array of one or more site scripts.</span></span> <span data-ttu-id="9b7de-241">Jedes wird durch eine ID identifziert.</span><span class="sxs-lookup"><span data-stu-id="9b7de-241">Each is identified by an ID.</span></span> <span data-ttu-id="9b7de-242">Die Skripts werden in der aufgeführten Reihenfolge ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="9b7de-242">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="9b7de-243">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b7de-243">Description</span></span>         | <span data-ttu-id="9b7de-244">(Optional) Die neue Anzeigebeschreibung des aktualisierten Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="9b7de-244">(Optional) The new display description of updated site design.</span></span> |
|<span data-ttu-id="9b7de-245">PreviewImageUrl</span><span class="sxs-lookup"><span data-stu-id="9b7de-245">PreviewImageUrl</span></span>     | <span data-ttu-id="9b7de-246">(Optional) Die neue URL eines Vorschaubilds.</span><span class="sxs-lookup"><span data-stu-id="9b7de-246">(Optional) The new URL of a preview image.</span></span> |
|<span data-ttu-id="9b7de-247">PreviewImageAltText</span><span class="sxs-lookup"><span data-stu-id="9b7de-247">PreviewImageAltText</span></span> | <span data-ttu-id="9b7de-248">(Optional) Die neue Alternativtextbeschreibung des Bilds für Barrierefreiheit.</span><span class="sxs-lookup"><span data-stu-id="9b7de-248">(Optional) The new alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="9b7de-249">IsDefault</span><span class="sxs-lookup"><span data-stu-id="9b7de-249">isDefault</span></span>           | <span data-ttu-id="9b7de-250">(Optional) **True**, wenn das Websitedesign als Standarddesign der Website angewendet wird; andernfalls **False**.</span><span class="sxs-lookup"><span data-stu-id="9b7de-250">(Optional) **true** if the site design is applied as the default site design; otherwise, **false**.</span></span> <span data-ttu-id="9b7de-251">Weitere Informationen finden Sie unter [Anpassen eines standardmäßigen Websitedesigns](customize-default-site-design.md).</span><span class="sxs-lookup"><span data-stu-id="9b7de-251">For more information see [Customize a default site design](customize-default-site-design.md)</span></span> |

<span data-ttu-id="9b7de-252">Nachfolgend finden Sie ein Beispiel, in dem jeder Wert in einem vorhandenen Websitedesign aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="9b7de-252">Here's an example that updates every value on an existing site design.</span></span>

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

<span data-ttu-id="9b7de-253">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **UpdateSiteDesign** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="9b7de-253">Here is an example of the JSON returned after calling **UpdateSiteDesign**.</span></span>

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

## <a name="deletesitedesign"></a><span data-ttu-id="9b7de-254">DeleteSiteDesign</span><span class="sxs-lookup"><span data-stu-id="9b7de-254">DeleteSiteDesign</span></span>

<span data-ttu-id="9b7de-255">Löscht ein Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="9b7de-255">Deletes a site design.</span></span>

### <a name="parameters"></a><span data-ttu-id="9b7de-256">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-256">Parameters</span></span>

|<span data-ttu-id="9b7de-257">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-257">Parameter</span></span>   | <span data-ttu-id="9b7de-258">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b7de-258">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="9b7de-259">id</span><span class="sxs-lookup"><span data-stu-id="9b7de-259">id</span></span>         | <span data-ttu-id="9b7de-260">Die ID des zu löschenden Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="9b7de-260">The ID of the item to delete.</span></span> |

<span data-ttu-id="9b7de-261">Nachfolgend finden Sie ein Beispiel zum Löschen eines Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="9b7de-261">Here's an example of deleting a site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteDesign", 
{id:"f9e76746-5076-4bd2-bad3-e611c488fa85"});
```

## <a name="getsitedesignrights"></a><span data-ttu-id="9b7de-262">GetSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="9b7de-262">GetSiteDesignRights</span></span>

<span data-ttu-id="9b7de-263">Abrufen einer Liste von Prinzipalen, die Zugriff auf ein Websitedesign haben.</span><span class="sxs-lookup"><span data-stu-id="9b7de-263">Gets a list of principals that have access to a site design.</span></span>


### <a name="parameters"></a><span data-ttu-id="9b7de-264">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-264">Parameters</span></span>

|<span data-ttu-id="9b7de-265">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-265">Parameter</span></span>   | <span data-ttu-id="9b7de-266">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b7de-266">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="9b7de-267">id</span><span class="sxs-lookup"><span data-stu-id="9b7de-267">id</span></span>         | <span data-ttu-id="9b7de-268">Die ID des Websitedesigns, über das Berechtigungsinformationen abgerufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="9b7de-268">The ID of the site design to get rights information from.</span></span> |

<span data-ttu-id="9b7de-269">Nachfolgend finden Sie ein Beispiel zum Abrufen der Anzeigeberechtigungen für ein bestimmtes Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="9b7de-269">Here's an example of getting view rights for a specific site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignRights", 
{id:"dc076f7b-6c15-4d76-8f85-948a17f5dd18"});
```

<span data-ttu-id="9b7de-270">Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **GetSiteDesignRights** zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="9b7de-270">Here is an example of the JSON returned after calling **GetSiteDesignRights**.</span></span>

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

## <a name="grantsitedesignrights"></a><span data-ttu-id="9b7de-271">GrantSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="9b7de-271">GrantSiteDesignRights</span></span>

<span data-ttu-id="9b7de-272">Erteilen von Zugriff auf ein Websitedesign für einen oder mehrere Prinzipale.</span><span class="sxs-lookup"><span data-stu-id="9b7de-272">Grants access to a site design for one or more principals.</span></span>

### <a name="parameters"></a><span data-ttu-id="9b7de-273">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-273">Parameters</span></span>

|<span data-ttu-id="9b7de-274">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-274">Parameter</span></span>   | <span data-ttu-id="9b7de-275">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b7de-275">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="9b7de-276">id</span><span class="sxs-lookup"><span data-stu-id="9b7de-276">id</span></span>         | <span data-ttu-id="9b7de-277">Die ID des Websitedesigns, für das Berechtigungen gewährt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="9b7de-277">The ID of the site design to grant rights on.</span></span> |
| <span data-ttu-id="9b7de-278">principalNames</span><span class="sxs-lookup"><span data-stu-id="9b7de-278">principalNames</span></span> | <span data-ttu-id="9b7de-279">Ein Array von einem oder mehreren Prinzipalen, denen Anzeigeberechtigungen gewährt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="9b7de-279">An array of one or more principals to grant view rights.</span></span> <span data-ttu-id="9b7de-280">Prinzipale können Benutzer oder E-Mail-aktivierte Sicherheitsgruppen in der Form „Alias“ oder „Alias@\<*Domänenname*\>.com“ sein.</span><span class="sxs-lookup"><span data-stu-id="9b7de-280">Principals can be users or mail-enabled security groups in the form of "alias" or "alias@\<*domain name*\>.com"</span></span> |
| <span data-ttu-id="9b7de-281">grantedRights</span><span class="sxs-lookup"><span data-stu-id="9b7de-281">grantedRights</span></span> | <span data-ttu-id="9b7de-282">Stets auf **1** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="9b7de-282">Always set to **1**.</span></span> <span data-ttu-id="9b7de-283">Dies steht für die Berechtigung **View**.</span><span class="sxs-lookup"><span data-stu-id="9b7de-283">This represents the **View** right.</span></span> |

<span data-ttu-id="9b7de-284">Nachfolgend finden Sie ein Beispiel zum Gewähren von Anzeigeberechtigungen für ein Websitedesign für Nestor und Patti (fiktive Benutzer bei Contoso).</span><span class="sxs-lookup"><span data-stu-id="9b7de-284">Here's an example of granting view rights to a site design for Nestor and Patti (fictional users at Contoso.)</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GrantSiteDesignRights", {
  "id": "dc076f7b-6c15-4d76-8f85-948a17f5dd18",
  "principalNames": [ "NestorW@contoso.onmicrosoft.com", "PattiF@contoso.onmicrosoft.com" ],
  "grantedRights": 1
});
```

## <a name="revokesitedesignrights"></a><span data-ttu-id="9b7de-285">RevokeSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="9b7de-285">RevokeSiteDesignRights</span></span>

<span data-ttu-id="9b7de-286">Widerrufen des Zugriffs auf ein Websitedesign für einen oder mehrere Prinzipale.</span><span class="sxs-lookup"><span data-stu-id="9b7de-286">Revokes access from a site design for one or more principals.</span></span>

### <a name="parameters"></a><span data-ttu-id="9b7de-287">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-287">Parameters</span></span>

|<span data-ttu-id="9b7de-288">Parameter</span><span class="sxs-lookup"><span data-stu-id="9b7de-288">Parameter</span></span>   | <span data-ttu-id="9b7de-289">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b7de-289">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="9b7de-290">id</span><span class="sxs-lookup"><span data-stu-id="9b7de-290">id</span></span>         | <span data-ttu-id="9b7de-291">Die ID des Websitedesigns, von dem Berechtigungen widerrufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="9b7de-291">The ID of the site design to revoke rights from.</span></span> |
| <span data-ttu-id="9b7de-292">principalNames</span><span class="sxs-lookup"><span data-stu-id="9b7de-292">principalNames</span></span> | <span data-ttu-id="9b7de-293">Ein Array von einem oder mehreren Prinzipalen, von denen Anzeigeberechtigungen widerrufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="9b7de-293">An array of one or more principals to revoke view rights from.</span></span> <span data-ttu-id="9b7de-294">Wenn für alle Prinzipale Berechtigungen für das Websitedesign widerrufen werden, ist die Seite für jeden sichtbar.</span><span class="sxs-lookup"><span data-stu-id="9b7de-294">If all principals have rights revoked on the site design, the site design becomes viewable to everyone.</span></span> |

<span data-ttu-id="9b7de-295">Nachfolgend finden Sie ein Beispiel zum Widerrufen von Anzeigeberechtigungen für ein Websitedesign für Patti (fiktiver Benutzer bei Contoso).</span><span class="sxs-lookup"><span data-stu-id="9b7de-295">Here's an example of revoking view rights from a site design for Patti (fictional user at Contoso.)</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.RevokeSiteDesignRights", 
{id:"5d4756e9-e1f5-42f7-afa7-5fa5aac170aa",
 principalNames:["debrab@Contoso.sharepoint.com"] });
```
