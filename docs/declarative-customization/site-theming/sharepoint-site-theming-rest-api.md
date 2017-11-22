# <a name="sharepoint-site-theming-rest-api"></a>SharePoint-Websitedesign: REST-API

Mithilfe der SharePoint-REST-Schnittstelle können Sie grundlegende CRUD-Operationen auf Websitedesigns anwenden, d. h: Erstellen, Lesen, Aktualisieren und Löschen (Create, Read, Update, Delete).

Der REST-Dienst in SharePoint Online (sowie in lokalen Bereitstellungen von SharePoint 2016 und höher) erlaubt die Zusammenfassung mehrerer Anforderungen in einem einzigen Aufruf an den Service mittels der ODATA-Abfrageoption „$batch“. Einzelheiten und Links zu Codebeispielen finden Sie unter [Durchführen von Batchanforderungen mit den REST-APIs](https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md).

## <a name="prerequisites"></a>Voraussetzungen
Lesen Sie vor der Umsetzung der Beispiele in diesem Artikel zunächst die folgenden Artikel:
- [Grundlegendes zum SharePoint-REST-Dienst](https://dev.office.com/sharepoint/docs/apis/rest/get-to-know-the-sharepoint-rest-service.md) 
- [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints.md)

## <a name="rest-commands-for-site-themes"></a>REST-Befehle für Websitedesigns

Für Websitedesigns stehen die folgenden REST-Befehle zur Verfügung:

* __AddTenantTheme__ &mdash; Erstellt ein neues Design, ähnlich wie das SharePoint-Cmdlet „Add-SPOTheme“.
* __RemoveTenantTheme__ &mdash; Entfernt ein Design aus dem Store des Mandanten, ähnlich wie das PowerShell-Cmdlet „Remove-SPOTheme“.
* __GetTenantThemingOptions__ &mdash; Ruft die Designeinstellungen ab.

Basis für die URL von REST-Befehlen zur Designverwaltung ist die Zeichenfolge „_api/thememanager“. Die Endpunkte für die oben aufgeführten Befehle beispielsweise sehen wie folgt aus:

* http://<site url>/_api/thememanager/AddTenantTheme
* http://<site url>/_api/thememanager/RemoveTenantTheme
* http://<site url>/_api/thememanager/GetTenantThemingOptions

## <a name="addtenanttheme"></a>AddTenantTheme

Der folgende JavaScript-Beispielcode demonstriert, wie Sie einem Mandanten ein neues Design hinzufügen können:

```javascript
function RestRequest(url,params) {
  var req = new XMLHttpRequest();
  req.onreadystatechange = function ()
        {
            if (req.readyState != 4) // Loaded
                return;
            console.log(req.responseText);
        };
  req.open("POST",url,true); 
  req.setRequestHeader("Content-Type", "application/json;charset=utf-8");
  req.setRequestHeader("ACCEPT", "application/json; odata.metadata=minimal");
  req.setRequestHeader("x-requestdigest", _spPageContextInfo.formDigestValue);
  req.setRequestHeader("ODATA-VERSION","4.0");
  req.send(params ? JSON.stringify(params) : void 0);
}
RestRequest("/_api/thememanager/GetTenantThemingOptions");

var pal = {
    "palette" : {
        "themePrimary": "#1BF242",
        "themeLighterAlt": "#0d0b00",
        "themeLighter": "#0b35bc",
        "themeLight": "#322d00",
        "themeTertiary": "#6a5f00",
       "themeSecondary": "#1B22F2",
        "themeDarkAlt": "#ffe817",
        "themeDark": "#ffed4b",
        "themeDarker": "#fff171",
        "neutralLighterAlt": "#252525",
        "neutralLighter": "#282828",
        "neutralLight": "#313131",
        "neutralQuaternaryAlt": "#3f3f3f",
        "neutralQuaternary": "#484848",
        "neutralTertiaryAlt": "#4f4f4f",
        "neutralTertiary": "#c8c8c8",
        "neutralSecondaryAlt": "#d0d0d0",
        "neutralSecondary": "#dadada",
        "neutralPrimary": "#ffffff",
        "neutralDark": "#eaeaea",
        "black": "#f8f8f8",
        "white": "#1f1f1f",
        "primaryBackground": "#1f1f1f",
        "primaryText": "#ffffff",
        "error": "#ff5f5f"
    }
}
RestRequest("/_api/thememanager/AddTenantTheme", {name:"Sounders Rave Green", themeJson: JSON.stringify(pal)});
```
## <a name="removetenanttheme"></a>RemoveTenantTheme
Der folgende JavaScript-Beispielcode demonstriert, wie Sie Designs entfernen können:

```javascript
function RestRequest(url,params) {
  var req = new XMLHttpRequest();
  req.onreadystatechange = function ()
        {
            if (req.readyState != 4) // Loaded
                return;
            console.log(req.responseText);
        };
  req.open("POST",url,true);
  req.setRequestHeader("Content-Type", "application/json;charset=utf-8");
  req.setRequestHeader("ACCEPT", "application/json; odata.metadata=minimal");
  req.setRequestHeader("x-requestdigest", _spPageContextInfo.formDigestValue);
  req.setRequestHeader("ODATA-VERSION","4.0");
  req.send(params ? JSON.stringify(params) : void 0);
}
 
RestRequest("/_api/thememanager/DeleteTenantTheme", { name:"themeName.DarkYellow" });
 
RestRequest("/_api/thememanager/UpdateTenantTheme", { name:"themeName",
     themeJson:""});
```

## <a name="gettenantthemingoptions"></a>GetTenantThemingOptions
Der folgende JavaScript-Beispielcode demonstriert, wie Sie die Einstellungen eines Designs auslesen können.

```javascript
function RestRequest(url,params) {
  var req = new XMLHttpRequest();
  req.onreadystatechange = function ()
        {
            if (req.readyState != 4) // Loaded
                return;
            console.log(req.responseText);
        };
  req.open("POST",url,true);
  req.setRequestHeader("Content-Type", "application/json;charset=utf-8");
  req.setRequestHeader("ACCEPT", "application/json; odata.metadata=minimal");
  req.setRequestHeader("x-requestdigest", _spPageContextInfo.formDigestValue);
  req.setRequestHeader("ODATA-VERSION","4.0");
  req.send(params ? JSON.stringify(params) : void 0);
}
 
RestRequest("/_api/thememanager/GetTenantThemingOptions");
```

## <a name="see-also"></a>Weitere Artikel

* [Überblick über das SharePoint-Websitedesign](sharepoint-site-theming-overview.md)
* [SharePoint-Websitedesign: JSON-Schema](sharepoint-site-theming-json-schema.md)
* [SharePoint-Websitedesign: PowerShell-Cmdlets](sharepoint-site-theming-powershell.md)
* [SharePoint-Websitedesign: CSOM](sharepoint-site-theming-csom.md)
* [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints.md)
* [Making REST calls with C# and JavaScript for SharePoint 2013](http://www.microsoft.com/resources/msdn/en-us/office/media/video/video.mdl?cid=sdc&from=mscomsdc&VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)

