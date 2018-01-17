---
title: REST-API von SharePoint-Websitedesigns
description: "Verwenden Sie SharePoint-Websitedesigns über die SharePoint-REST-Schnittstelle, um grundlegende CRUD-Operationen (Create, Read, Update, Delete, also Erstellen, Lesen, Aktualisieren und Löschen) auszuführen."
ms.date: 12/14/2017
ms.openlocfilehash: 3670ffabcebd5146abb155906dce341324404815
ms.sourcegitcommit: 8e63066ad9591e51bbda419b1b9527452111081b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="site-design-and-site-script-rest-api"></a><span data-ttu-id="85afd-103">REST-API von SharePoint-Websitedesigns und Websiteskripts</span><span class="sxs-lookup"><span data-stu-id="85afd-103">Site design and site script REST API</span></span>

> [!NOTE]
> <span data-ttu-id="85afd-104">Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden.</span><span class="sxs-lookup"><span data-stu-id="85afd-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="85afd-105">Sie werden in Produktionsumgebungen derzeit nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="85afd-105">They are not currently supported for use in production environments.</span></span>

<span data-ttu-id="85afd-106">Mithilfe der SharePoint-REST-Schnittstelle können Sie grundlegende CRUD-Operationen ausführen, d. h: Erstellen, Lesen, Aktualisieren und Löschen (Create, Read, Update, Delete).</span><span class="sxs-lookup"><span data-stu-id="85afd-106">You can use the the SharePoint REST interface to perform basic create, read, update, and delete (CRUD) operations on site themes.</span></span>

<span data-ttu-id="85afd-107">Der REST-Dienst in SharePoint Online (sowie in lokalen Bereitstellungen von SharePoint 2016 und höher) erlaubt die Zusammenfassung mehrerer Anforderungen in einem einzigen Aufruf an den Service mittels der ODATA-Abfrageoption „$batch“.</span><span class="sxs-lookup"><span data-stu-id="85afd-107">The SharePoint Online (and SharePoint 2016 and later on-premises) REST service supports combining multiple requests into a single call to the service by using the OData $batch query option.</span></span> <span data-ttu-id="85afd-108">Einzelheiten und Links zu Codebeispielen finden Sie unter [Durchführen von Batchanforderungen mit den REST-APIs](https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="85afd-108">For details and links to code samples, see [Make batch requests with the REST APIs](https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85afd-109">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="85afd-109">Prerequisites</span></span>
<span data-ttu-id="85afd-110">Lesen Sie vor der Umsetzung der Beispiele in diesem Artikel zunächst die folgenden Artikel:</span><span class="sxs-lookup"><span data-stu-id="85afd-110">Before you get started, make sure that you're familiar with the following:</span></span>
- <span data-ttu-id="85afd-111">[Grundlegendes zum SharePoint-REST-Dienst](https://dev.office.com/sharepoint/docs/apis/rest/get-to-know-the-sharepoint-rest-service.md)</span><span class="sxs-lookup"><span data-stu-id="85afd-111">[Get to know the SharePoint REST service](https://dev.office.com/sharepoint/docs/apis/rest/get-to-know-the-sharepoint-rest-service.md)</span></span> 
- <span data-ttu-id="85afd-112">[Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="85afd-112">[Complete basic operations using SharePoint REST endpoints](https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints.md)</span></span>

## <a name="rest-commands"></a><span data-ttu-id="85afd-113">REST-Befehle</span><span class="sxs-lookup"><span data-stu-id="85afd-113">REST commands</span></span>

<span data-ttu-id="85afd-114">Für Websitedesigns und Websiteskripts stehen die folgenden REST-Befehle zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="85afd-114">The following REST commands are available for working with site themes:</span></span>

- <span data-ttu-id="85afd-115">**CreateSiteScript** &mdash; Erstellen eines neuen Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="85afd-115">**CreateSiteScript** &mdash; Create a new site script.</span></span>
- <span data-ttu-id="85afd-116">**GetSiteScripts** &mdash; Abrufen einer Liste von Informationen zu vorhandenen Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="85afd-116">**GetSiteScripts** &mdash; Get a list of information on existing site scripts.</span></span>
- <span data-ttu-id="85afd-117">**GetSiteScriptMetadata** &mdash; Abrufen von Informationen zu einem bestimmten Websiteskript.</span><span class="sxs-lookup"><span data-stu-id="85afd-117">**GetSiteScriptMetadata** &mdash; Get information about a specific site script.</span></span>
- <span data-ttu-id="85afd-118">**UpdateSiteScript** &mdash; Aktualisieren eines Websiteskripts mit neuen Werten.</span><span class="sxs-lookup"><span data-stu-id="85afd-118">**UpdateSiteScript** &mdash; Update a site script with new values.</span></span>
- <span data-ttu-id="85afd-119">**DeleteSiteScript** &mdash; Löschen eines Websitekripts.</span><span class="sxs-lookup"><span data-stu-id="85afd-119">**DeleteSiteScript** &mdash; Delete a site script.</span></span>
- <span data-ttu-id="85afd-120">**CreateSiteDesign** &mdash; Erstellen eines Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="85afd-120">**CreateSiteDesign** &mdash; Create a site design.</span></span>
- <span data-ttu-id="85afd-121">**GetSiteDesigns** &mdash; Abrufen einer Liste von Informationen zu vorhandenen Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="85afd-121">**GetSiteDesigns** &mdash; Get a list of information on existing site designs.</span></span>
- <span data-ttu-id="85afd-122">**GetSiteDesignMetadata** &mdash; Abrufen von Informationen zu einem bestimmten Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="85afd-122">**GetSiteDesignMetadata** &mdash; Get information about a sepcific site design.</span></span>
- <span data-ttu-id="85afd-123">**UpdateSiteDesign** &mdash; Aktualisieren eines Websitedesigns mit neuen Werten.</span><span class="sxs-lookup"><span data-stu-id="85afd-123">**UpdateSiteDesign** &mdash; Update a site design with new values.</span></span>
- <span data-ttu-id="85afd-124">**DeleteSiteDesign** &mdash; Löschen eines Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="85afd-124">**DeleteSiteDesign** &mdash; Delete a site design.</span></span>
- <span data-ttu-id="85afd-125">**GetSiteDesignRights** &mdash; Abrufen einer Liste von Prinzipalen, die Zugriff auf ein Websitedesign haben.</span><span class="sxs-lookup"><span data-stu-id="85afd-125">**GetSiteDesignRights** &mdash; Get a list of principals that have access to a site design.</span></span>
- <span data-ttu-id="85afd-126">**GrantSiteDesignRights** &mdash; Erteilen von Zugriff auf ein Websitedesign für einen oder mehrere Prinzipale.</span><span class="sxs-lookup"><span data-stu-id="85afd-126">**GrantSiteDesignRights** &mdash; Grant access to a site design for one or more principals.</span></span>
- <span data-ttu-id="85afd-127">**RevokeSiteDesignRights** &mdash; Widerrufen des Zugriffs auf ein Websitedesign für einen oder mehrere Prinzipale.</span><span class="sxs-lookup"><span data-stu-id="85afd-127">**RevokeSiteDesignRights** &mdash; Revoke access from a site design for one or more principals.</span></span>

## <a name="create-a-function-to-send-rest-requests"></a><span data-ttu-id="85afd-128">Erstellen einer Funktion zum Senden von REST-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="85afd-128">Create a function to send REST requests</span></span>

<span data-ttu-id="85afd-129">Zum Arbeiten mit der REST-API wird empfohlen, eine Hilfsfunktion für die REST-Aufrufe zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="85afd-129">To work with the REST API we recommend creating a helper function to make the REST calls.</span></span> <span data-ttu-id="85afd-130">Die folgende **RestRequest**-Funktion ruft die im **url**-Parameter angegebene REST-Methode auf und übergibt die weiteren Parameter in **params**.</span><span class="sxs-lookup"><span data-stu-id="85afd-130">The following **RestRequest** function will call the REST method specified in the **url** parameter and pass the additional parameters in **params**.</span></span>

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

## <a name="createsitescript"></a><span data-ttu-id="85afd-131">CreateSiteScript</span><span class="sxs-lookup"><span data-stu-id="85afd-131">CreateSiteScript</span></span>

<span data-ttu-id="85afd-132">Erstellen eines neues Websitedesigns, das für Benutzer beim Erstellen einer neuen Website von der SharePoint-Startseite verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="85afd-132">Creates a new site design available to users when they create a new site from the SharePoint home page.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteScript(Title=@title)?@title='TITLE'", VARIABLE);
```

## <a name="getsitescripts"></a><span data-ttu-id="85afd-133">GetSiteScripts</span><span class="sxs-lookup"><span data-stu-id="85afd-133">GetSiteScripts</span></span>

<span data-ttu-id="85afd-134">Abrufen einer Liste von Informationen zu vorhandenen Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="85afd-134">Gets a list of information on existing site scripts.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScripts");
```

## <a name="getsitescriptmetadata"></a><span data-ttu-id="85afd-135">GetSiteScriptMetadata</span><span class="sxs-lookup"><span data-stu-id="85afd-135">GetSiteScriptMetadata</span></span>

<span data-ttu-id="85afd-136">Abrufen von Informationen zu einem bestimmten Websiteskript.</span><span class="sxs-lookup"><span data-stu-id="85afd-136">Gets information about a specific site script.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScriptMetadata", {id:"<ID>"});
```

## <a name="updatesitescript"></a><span data-ttu-id="85afd-137">UpdateSiteScript</span><span class="sxs-lookup"><span data-stu-id="85afd-137">UpdateSiteScript</span></span>

<span data-ttu-id="85afd-138">Aktualisieren eines Websiteskripts mit neuen Werten.</span><span class="sxs-lookup"><span data-stu-id="85afd-138">Updates a site script with new values.</span></span>

```javascript
VAR = site script content

RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.UpdateSiteScript", {updateInfo:{Id:"<siteScriptID>", Title:"<updated title>", Description:"<updated description>", Version: 2, Content: JSON.stringify(<VAR>)}});
```

## <a name="deletesitescript"></a><span data-ttu-id="85afd-139">DeleteSiteScript</span><span class="sxs-lookup"><span data-stu-id="85afd-139">DeleteSiteScript</span></span>

<span data-ttu-id="85afd-140">Löschen eines Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="85afd-140">Deletes a site script.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteScript", {id:"<ID>"});
```

## <a name="createsitedesign"></a><span data-ttu-id="85afd-141">CreateSiteDesign</span><span class="sxs-lookup"><span data-stu-id="85afd-141">CreateSiteDesign</span></span>

<span data-ttu-id="85afd-142">Erstellen eines Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="85afd-142">Create a design package</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteDesign", {info:{Title:"<title>", Description:"<description>", SiteScriptIds:["NNN"],  WebTemplate:"<64 | 68>", IsDefault: <false | true>}});
```

## <a name="getsitedesigns"></a><span data-ttu-id="85afd-143">GetSiteDesigns</span><span class="sxs-lookup"><span data-stu-id="85afd-143">GetSiteDesigns</span></span>

<span data-ttu-id="85afd-144">Abrufen einer Liste von Informationen zu vorhandenen Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="85afd-144">Get a list of information on existing site designs.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesigns");
```

## <a name="getsitedesignmetadata"></a><span data-ttu-id="85afd-145">GetSiteDesignMetadata</span><span class="sxs-lookup"><span data-stu-id="85afd-145">GetSiteDesignMetadata</span></span>

<span data-ttu-id="85afd-146">Abrufen von Informationen zu einem bestimmten Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="85afd-146">Get information about a specific site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignMetadata", {id:"<ID>"});
```

## <a name="updatesitedesign"></a><span data-ttu-id="85afd-147">UpdateSiteDesign</span><span class="sxs-lookup"><span data-stu-id="85afd-147">UpdateSiteDesign</span></span>

<span data-ttu-id="85afd-148">Aktualisieren eines Websitedesigns mit neuen Werten.</span><span class="sxs-lookup"><span data-stu-id="85afd-148">Update a resource with new values.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.UpdateSiteDesign", {updateInfo:{Id:"<siteDesignID>", Title:"<updated site design title>", Description:"<updated site design description>", SiteScriptIds:["<ID>"], PreviewImageUrl:"<url to image asset for site design preview image>",PreviewImageAltText:"<alt text for preview image>" WebTemplate:"68", Version: 7, IsDefault: false}});
```

## <a name="deletesitedesign"></a><span data-ttu-id="85afd-149">DeleteSiteDesign</span><span class="sxs-lookup"><span data-stu-id="85afd-149">DeleteSiteDesign</span></span>

<span data-ttu-id="85afd-150">Löschen eines Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="85afd-150">Delete a site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteDesign", {id:"<ID>"});
```

## <a name="getsitedesignrights"></a><span data-ttu-id="85afd-151">GetSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="85afd-151">GetSiteDesignRights</span></span>

<span data-ttu-id="85afd-152">Abrufen einer Liste von Prinzipalen, die Zugriff auf ein Websitedesign haben.</span><span class="sxs-lookup"><span data-stu-id="85afd-152">Get a list of principals that have access to a site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignRights", {id:"<ID>"});
```

## <a name="grantsitedesignrights"></a><span data-ttu-id="85afd-153">GrantSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="85afd-153">GrantSiteDesignRights</span></span>

<span data-ttu-id="85afd-154">Erteilen von Zugriff auf ein Websitedesign für einen oder mehrere Prinzipale.</span><span class="sxs-lookup"><span data-stu-id="85afd-154">Grant access to a site design for one or more principals.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GrantSiteDesignRights", {id:"<ID>", principalNames:["alias", “alias@domain.com”], grantedRights:1});
```

## <a name="revokesitedesignrights"></a><span data-ttu-id="85afd-155">RevokeSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="85afd-155">RevokeSiteDesignRights</span></span>

<span data-ttu-id="85afd-156">Widerrufen des Zugriffs auf ein Websitedesign für einen oder mehrere Prinzipale.</span><span class="sxs-lookup"><span data-stu-id="85afd-156">Revoke access from a site design for one or more principals.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.RevokeSiteDesignRights", {id:"5d4756e9-e1f5-42f7-afa7-5fa5aac170aa", principalNames:["debrab@Contoso.sharepoint.com"] });
```
