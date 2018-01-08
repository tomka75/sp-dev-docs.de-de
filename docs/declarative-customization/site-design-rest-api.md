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
# <a name="site-design-and-site-script-rest-api"></a>REST-API von SharePoint-Websitedesigns und Websiteskripts

> [!NOTE]
> Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden. Sie werden in Produktionsumgebungen derzeit nicht unterstützt.

Mithilfe der SharePoint-REST-Schnittstelle können Sie grundlegende CRUD-Operationen ausführen, d. h: Erstellen, Lesen, Aktualisieren und Löschen (Create, Read, Update, Delete).

Der REST-Dienst in SharePoint Online (sowie in lokalen Bereitstellungen von SharePoint 2016 und höher) erlaubt die Zusammenfassung mehrerer Anforderungen in einem einzigen Aufruf an den Service mittels der ODATA-Abfrageoption „$batch“. Einzelheiten und Links zu Codebeispielen finden Sie unter [Durchführen von Batchanforderungen mit den REST-APIs]((https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md)).

## <a name="prerequisites"></a>Voraussetzungen
Lesen Sie vor der Umsetzung der Beispiele in diesem Artikel zunächst die folgenden Artikel:
- [Grundlegendes zum SharePoint-REST-Dienst]((https://dev.office.com/sharepoint/docs/apis/rest/get-to-know-the-sharepoint-rest-service.md)) 
- [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten]((https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints.md))

## <a name="rest-commands"></a>REST-Befehle

Für Websitedesigns und Websiteskripts stehen die folgenden REST-Befehle zur Verfügung:

- **CreateSiteScript** &mdash; Erstellen eines neuen Websiteskripts.
- **GetSiteScripts** &mdash; Abrufen einer Liste von Informationen zu vorhandenen Websiteskripts.
- **GetSiteScriptMetadata** &mdash; Abrufen von Informationen zu einem bestimmten Websiteskript.
- **UpdateSiteScript** &mdash; Aktualisieren eines Websiteskripts mit neuen Werten.
- **DeleteSiteScript** &mdash; Löschen eines Websitekripts.
- **CreateSiteDesign** &mdash; Erstellen eines Websitedesigns.
- **GetSiteDesigns** &mdash; Abrufen einer Liste von Informationen zu vorhandenen Websitedesigns.
- **GetSiteDesignMetadata** &mdash; Abrufen von Informationen zu einem bestimmten Websitedesign.
- **UpdateSiteDesign** &mdash; Aktualisieren eines Websitedesigns mit neuen Werten.
- **DeleteSiteDesign** &mdash; Löschen eines Websitedesigns.
- **GetSiteDesignRights** &mdash; Abrufen einer Liste von Prinzipalen, die Zugriff auf ein Websitedesign haben.
- **GrantSiteDesignRights** &mdash; Erteilen von Zugriff auf ein Websitedesign für einen oder mehrere Prinzipale.
- **RevokeSiteDesignRights** &mdash; Widerrufen des Zugriffs auf ein Websitedesign für einen oder mehrere Prinzipale.

## <a name="create-a-function-to-send-rest-requests"></a>Erstellen einer Funktion zum Senden von REST-Anforderungen

Zum Arbeiten mit der REST-API wird empfohlen, eine Hilfsfunktion für die REST-Aufrufe zu erstellen. Die folgende **RestRequest**-Funktion ruft die im **url**-Parameter angegebene REST-Methode auf und übergibt die weiteren Parameter in **params**.

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

## <a name="createsitescript"></a>CreateSiteScript

Erstellen eines neues Websitedesigns, das für Benutzer beim Erstellen einer neuen Website von der SharePoint-Startseite verfügbar ist.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteScript(Title=@title)?@title='TITLE'", VARIABLE);
```

## <a name="getsitescripts"></a>GetSiteScripts

Abrufen einer Liste von Informationen zu vorhandenen Websiteskripts.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScripts");
```

## <a name="getsitescriptmetadata"></a>GetSiteScriptMetadata

Abrufen von Informationen zu einem bestimmten Websiteskript.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScriptMetadata", {id:"<ID>"});
```

## <a name="updatesitescript"></a>UpdateSiteScript

Aktualisieren eines Websiteskripts mit neuen Werten.

```javascript
VAR = site script content

RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.UpdateSiteScript", {updateInfo:{Id:"<siteScriptID>", Title:"<updated title>", Description:"<updated description>", Version: 2, Content: JSON.stringify(<VAR>)}});
```

## <a name="deletesitescript"></a>DeleteSiteScript

Löschen eines Websiteskripts.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteScript", {id:"<ID>"});
```

## <a name="createsitedesign"></a>CreateSiteDesign

Erstellen eines Websitedesigns.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteDesign", {info:{Title:"<title>", Description:"<description>", SiteScriptIds:["NNN"],  WebTemplate:"<64 | 68>", IsDefault: <false | true>}});
```

## <a name="getsitedesigns"></a>GetSiteDesigns

Abrufen einer Liste von Informationen zu vorhandenen Websitedesigns.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesigns");
```

## <a name="getsitedesignmetadata"></a>GetSiteDesignMetadata

Abrufen von Informationen zu einem bestimmten Websitedesign.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignMetadata", {id:"<ID>"});
```

## <a name="updatesitedesign"></a>UpdateSiteDesign

Aktualisieren eines Websitedesigns mit neuen Werten.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.UpdateSiteDesign", {updateInfo:{Id:"<siteDesignID>", Title:"<updated site design title>", Description:"<updated site design description>", SiteScriptIds:["<ID>"], PreviewImageUrl:"<url to image asset for site design preview image>",PreviewImageAltText:"<alt text for preview image>" WebTemplate:"68", Version: 7, IsDefault: false}});
```

## <a name="deletesitedesign"></a>DeleteSiteDesign

Löschen eines Websitedesigns.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteDesign", {id:"<ID>"});
```

## <a name="getsitedesignrights"></a>GetSiteDesignRights

Abrufen einer Liste von Prinzipalen, die Zugriff auf ein Websitedesign haben.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignRights", {id:"<ID>"});
```

## <a name="grantsitedesignrights"></a>GrantSiteDesignRights

Erteilen von Zugriff auf ein Websitedesign für einen oder mehrere Prinzipale.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GrantSiteDesignRights", {id:"<ID>", principalNames:["alias", “alias@domain.com”], grantedRights:1});
```

## <a name="revokesitedesignrights"></a>RevokeSiteDesignRights

Widerrufen des Zugriffs auf ein Websitedesign für einen oder mehrere Prinzipale.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.RevokeSiteDesignRights", {id:"5d4756e9-e1f5-42f7-afa7-5fa5aac170aa", principalNames:["debrab@Contoso.sharepoint.com"] });
```
