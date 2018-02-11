---
title: REST-API von SharePoint-Websitedesigns
description: "Verwenden Sie SharePoint-Websitedesigns über die SharePoint-REST-Schnittstelle, um grundlegende CRUD-Operationen (Create, Read, Update, Delete, also Erstellen, Lesen, Aktualisieren und Löschen) auszuführen."
ms.date: 12/14/2017
ms.openlocfilehash: 03170b69718946d97901de8277433ff58543f43e
ms.sourcegitcommit: e4bf60eabffe63dc07f96824167d249c0678db82
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/30/2018
---
# <a name="site-design-and-site-script-rest-api"></a>REST-API von SharePoint-Websitedesigns und Websiteskripts

> [!NOTE]
> Websitedesigns und Websiteskripts befinden sich in der Vorschau und können ohne vorherige Ankündigung geändert werden. Sie werden derzeit nur für Produktionsumgebungen im Zielrelease unterstützt.

Mithilfe der SharePoint-REST-Schnittstelle können Sie grundlegende CRUD-Operationen ausführen, d. h: Erstellen, Lesen, Aktualisieren und Löschen (Create, Read, Update, Delete).

Der REST-Dienst in SharePoint Online (sowie in lokalen Bereitstellungen von SharePoint 2016 und höher) erlaubt die Zusammenfassung mehrerer Anforderungen in einem einzigen Aufruf an den Service mittels der ODATA-Abfrageoption „$batch“. Einzelheiten und Links zu Codebeispielen finden Sie unter [Durchführen von Batchanforderungen mit den REST-APIs](https://docs.microsoft.com/de-DE/sharepoint/dev/sp-add-ins/make-batch-requests-with-the-rest-apis).

## <a name="prerequisites"></a>Voraussetzungen
Lesen Sie vor der Umsetzung der Beispiele in diesem Artikel zunächst die folgenden Artikel:
- [Grundlegendes zum SharePoint-REST-Dienst](https://docs.microsoft.com/de-DE/sharepoint/dev/sp-add-ins/get-to-know-the-sharepoint-rest-service) 
- [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](https://docs.microsoft.com/de-DE/sharepoint/dev/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints)

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

Erstellt ein neues Websiteskript.

### <a name="parameters"></a>Parameter

|Parameter     | Beschreibung  |
|--------------|--------------|
| Titel       | Der Anzeigename des Websitedesigns. |
| Inhalt     | JSON-Wert, der das Skript beschreibt. Weitere Informationen finden Sie unter [JSON-Referenz](site-design-json-schema.md).|

Im folgenden Beispiel wird ein neues Websiteskript erstellt, das ein benutzerdefiniertes Design anwendet.

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

Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **CreateSiteScript** zurückgegeben wird. Er enthält die ID des neuen Websiteskripts.

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

## <a name="getsitescripts"></a>GetSiteScripts

Abrufen einer Liste von Informationen zu allen vorhandenen Websiteskripts.

### <a name="parameters"></a>Parameter

Keine

Im folgenden Beispiel werden die Websiteskriptinformationen für alle Websiteskripts abgerufen.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScripts");
```

Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **GetSiteScripts** zurückgegeben wird.

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

## <a name="getsitescriptmetadata"></a>GetSiteScriptMetadata

Abrufen von Informationen zu einem bestimmten Websiteskript. Es wird auch der JSON-Code des Skripts zurückgegeben.

### <a name="parameters"></a>Parameter

|Parameter     | Beschreibung  |
|--------------|--------------|
| id    | Die ID des Websiteskripts, über das Informationen abgerufen werden sollen. |

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScriptMetadata",
{id:"07702c07-0485-426f-b710-4704241caad9"});
```

Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **GetSiteScriptMetadata** zurückgegeben wird.

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

## <a name="updatesitescript"></a>UpdateSiteScript

Aktualisieren eines Websiteskripts mit neuen Werten. In dem REST-Aufruf sind alle Parameter mit Ausnahme der Website-Skript-ID optional.

### <a name="parameters"></a>Parameter

|Parameter   | Beschreibung  |
|------------|--------------|
| Id         | Die ID des zu aktualisierenden Websiteskripts. |
|Titel       | (optional) Der neue Anzeigename des Websiteskripts. |
|Beschreibung | (Optional) Die neue Beschreibung des Websiteskripts. |
| Version    | (Optional) Die neue Versionsnummer des Websiteskripts. |
| Inhalt    | (Optional) Ein neues JSON-Skript, das die Skriptaktionen definiert. Weitere Informationen finden Sie unter [JSON-Schema eines Websitedesigns](site-design-json-schema.md). |

Nachfolgend finden Sie ein Beispiel des Aktualisierens eines vorhandenen Websiteskripts mit einem neuen JSON-Skript und neuen Werten.

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

Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **UpdateSiteScript** zurückgegeben wird.

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

## <a name="deletesitescript"></a>DeleteSiteScript

Löschen eines Websiteskripts.

### <a name="parameters"></a>Parameter

|Parameter   | Beschreibung  |
|------------|--------------|
| id         | Die ID des zu löschenden Websiteskripts. |

Nachfolgend finden Sie ein Beispiel zum Löschen eines Websiteskripts.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteScript", 
{id:"07702c07-0485-426f-b710-4704241caad9"});
```

## <a name="createsitedesign"></a>CreateSiteDesign

Erstellen eines neues Websitedesigns, das für Benutzer beim Erstellen einer neuen Website von der SharePoint-Startseite verfügbar ist.

### <a name="parameters"></a>Parameter

|Parameter  | Beschreibung  |
|-----------|--------------|
|Titel                 | Der Anzeigename des Websitedesigns. |
|WebTemplate           | Identifiziert, zu welcher Basisvorlage das Design hinzugefügt werden soll. Verwenden Sie den Wert **64** für die Teamwebsite-Vorlage und den Wert **68** für die Kommunikationswebsitevorlage. |
|SiteScripts           | Ein Array von einem oder mehreren Websiteskripts. Jedes wird durch eine ID identifziert. Die Skripts werden in der aufgeführten Reihenfolge ausgeführt. |
|Beschreibung         | (Optional) Die Anzeigebeschreibung des Websitedesigns. |
|PreviewImageUrl     | (optional) Die URL eines Vorschaubilds. Wenn keine angegeben ist, verwendet SharePoint ein allgemeines Bild. |
|PreviewImageAltText | (Optional) Die Alternativtextbeschreibung des Bilds für Barrierefreiheit. |
|IsDefault           | (Optional) **True**, wenn das Websitedesign als Standarddesign der Website angewendet wird; andernfalls **False**. Weitere Informationen finden Sie unter [Anpassen eines standardmäßigen Websitedesigns](customize-default-site-design.md). |

Nachfolgend finden Sie ein Beispiel für das Erstellen eines neuen Websitedesigns.

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

Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **CreateSiteDesign** zurückgegeben wird. Er enthält die ID des neuen Websitedesigns.

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

## <a name="getsitedesigns"></a>GetSiteDesigns

Abrufen einer Liste von Informationen zu vorhandenen Websitedesigns.

### <a name="parameters"></a>Parameter

Keine

Nachfolgend finden Sie ein Beispiel zum Abrufen aller Websitedesigns.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesigns");
```

Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **GetSiteDesigns** zurückgegeben wird.

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

## <a name="getsitedesignmetadata"></a>GetSiteDesignMetadata

Abrufen von Informationen zu einem bestimmten Websitedesign.

### <a name="parameters"></a>Parameter

|Parameter   | Beschreibung  |
|------------|--------------|
| id         | Die ID des Websitedesigns, über das Informationen abgerufen werden sollen. |

Nachfolgend finden Sie ein Beispiel zum Abrufen von Informationen zu einem bestimmten Websitedesign nach ID.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignMetadata", 
{id:"614f9b28-3e85-4ec9-a961-5971ea086cca"});
```

Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **GetSiteDesignMetadata** zurückgegeben wird.

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

## <a name="updatesitedesign"></a>UpdateSiteDesign

Aktualisieren eines Websitedesigns mit neuen Werten. In dem REST-Aufruf sind mit Ausnahme der Website-Skript-ID optional. Hinweis: Wenn Sie zuvor den IsDefault-Parameter auf „true“ festgelegt haben und sie diese Einstellung beibehalten möchten, müssen Sie diesen Parameter erneut übergeben (andernfalls wird er auf „false“ zurückgesetzt). 

### <a name="parameters"></a>Parameter

|Parameter  | Beschreibung  |
|-----------|--------------|
|Id         | Die ID des zu aktualisierenden Websitedesigns. |
|Titel                 |  (Optional) Der neue Anzeigename des aktualisierten Websitedesigns. |
|WebTemplate           | (Optional) Die neue Vorlage, der das Websitedesign hinzugefügt werden soll. Verwenden Sie den Wert **64** für die Teamwebsite-Vorlage und den Wert **68** für die Kommunikationswebsitevorlage. |
|SiteScripts           | (Optional) Ein neues Array von einem oder mehreren Websiteskripts. Jedes wird durch eine ID identifziert. Die Skripts werden in der aufgeführten Reihenfolge ausgeführt. |
|Beschreibung         | (Optional) Die neue Anzeigebeschreibung des aktualisierten Websitedesigns. |
|PreviewImageUrl     | (Optional) Die neue URL eines Vorschaubilds. |
|PreviewImageAltText | (Optional) Die neue Alternativtextbeschreibung des Bilds für Barrierefreiheit. |
|IsDefault           | (Optional) **True**, wenn das Websitedesign als Standarddesign der Website angewendet wird; andernfalls **False**. Weitere Informationen finden Sie unter [Anpassen eines standardmäßigen Websitedesigns](customize-default-site-design.md). |

Nachfolgend finden Sie ein Beispiel, in dem jeder Wert in einem vorhandenen Websitedesign aktualisiert wird.

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

Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **UpdateSiteDesign** zurückgegeben wird.

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

## <a name="deletesitedesign"></a>DeleteSiteDesign

Löscht ein Websitedesign.

### <a name="parameters"></a>Parameter

|Parameter   | Beschreibung  |
|------------|--------------|
| id         | Die ID des zu löschenden Websitedesigns. |

Nachfolgend finden Sie ein Beispiel zum Löschen eines Websitedesigns.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteDesign", 
{id:"f9e76746-5076-4bd2-bad3-e611c488fa85"});
```

## <a name="getsitedesignrights"></a>GetSiteDesignRights

Abrufen einer Liste von Prinzipalen, die Zugriff auf ein Websitedesign haben.


### <a name="parameters"></a>Parameter

|Parameter   | Beschreibung  |
|------------|--------------|
| id         | Die ID des Websitedesigns, über das Berechtigungsinformationen abgerufen werden sollen. |

Nachfolgend finden Sie ein Beispiel zum Abrufen der Anzeigeberechtigungen für ein bestimmtes Websitedesign.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignRights", 
{id:"dc076f7b-6c15-4d76-8f85-948a17f5dd18"});
```

Nachfolgend sehen Sie ein Beispiel des JSON-Codes, der nach dem Aufrufen von **GetSiteDesignRights** zurückgegeben wird.

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

## <a name="grantsitedesignrights"></a>GrantSiteDesignRights

Erteilen von Zugriff auf ein Websitedesign für einen oder mehrere Prinzipale.

### <a name="parameters"></a>Parameter

|Parameter   | Beschreibung  |
|------------|--------------|
| id         | Die ID des Websitedesigns, für das Berechtigungen gewährt werden sollen. |
| principalNames | Ein Array von einem oder mehreren Prinzipalen, denen Anzeigeberechtigungen gewährt werden sollen. Prinzipale können Benutzer oder E-Mail-aktivierte Sicherheitsgruppen in der Form „Alias“ oder „Alias@\<*Domänenname*\>.com“ sein. |
| grantedRights | Stets auf **1** festgelegt. Dies steht für die Berechtigung **View**. |

Nachfolgend finden Sie ein Beispiel zum Gewähren von Anzeigeberechtigungen für ein Websitedesign für Nestor und Patti (fiktive Benutzer bei Contoso).

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GrantSiteDesignRights", {
  "id": "dc076f7b-6c15-4d76-8f85-948a17f5dd18",
  "principalNames": [ "NestorW@contoso.onmicrosoft.com", "PattiF@contoso.onmicrosoft.com" ],
  "grantedRights": 1
});
```

## <a name="revokesitedesignrights"></a>RevokeSiteDesignRights

Widerrufen des Zugriffs auf ein Websitedesign für einen oder mehrere Prinzipale.

### <a name="parameters"></a>Parameter

|Parameter   | Beschreibung  |
|------------|--------------|
| id         | Die ID des Websitedesigns, von dem Berechtigungen widerrufen werden sollen. |
| principalNames | Ein Array von einem oder mehreren Prinzipalen, von denen Anzeigeberechtigungen widerrufen werden sollen. Wenn für alle Prinzipale Berechtigungen für das Websitedesign widerrufen werden, ist die Seite für jeden sichtbar. |

Nachfolgend finden Sie ein Beispiel zum Widerrufen von Anzeigeberechtigungen für ein Websitedesign für Patti (fiktiver Benutzer bei Contoso).

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.RevokeSiteDesignRights", 
{id:"5d4756e9-e1f5-42f7-afa7-5fa5aac170aa",
 principalNames:["debrab@Contoso.sharepoint.com"] });
```
