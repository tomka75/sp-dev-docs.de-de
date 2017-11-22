# <a name="sharepoint-site-theming-rest-api"></a><span data-ttu-id="2d0f7-101">SharePoint-Websitedesign: REST-API</span><span class="sxs-lookup"><span data-stu-id="2d0f7-101">SharePoint site theming: REST API</span></span>

<span data-ttu-id="2d0f7-102">Mithilfe der SharePoint-REST-Schnittstelle können Sie grundlegende CRUD-Operationen auf Websitedesigns anwenden, d. h: Erstellen, Lesen, Aktualisieren und Löschen (Create, Read, Update, Delete).</span><span class="sxs-lookup"><span data-stu-id="2d0f7-102">You can use the the SharePoint REST interface to perform basic create, read, update, and delete (CRUD) operations on site themes.</span></span>

<span data-ttu-id="2d0f7-103">Der REST-Dienst in SharePoint Online (sowie in lokalen Bereitstellungen von SharePoint 2016 und höher) erlaubt die Zusammenfassung mehrerer Anforderungen in einem einzigen Aufruf an den Service mittels der ODATA-Abfrageoption „$batch“.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-103">Tip  The SharePoint Online (and on-premise SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData   query option. For details and links to code samples, see Make batch requests with the REST APIs.</span></span> <span data-ttu-id="2d0f7-104">Einzelheiten und Links zu Codebeispielen finden Sie unter [Durchführen von Batchanforderungen mit den REST-APIs](https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="2d0f7-104">For details and links to code samples, see [Make batch requests with the REST APIs](https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d0f7-105">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="2d0f7-105">Prerequisites</span></span>
<span data-ttu-id="2d0f7-106">Lesen Sie vor der Umsetzung der Beispiele in diesem Artikel zunächst die folgenden Artikel:</span><span class="sxs-lookup"><span data-stu-id="2d0f7-106">Before you get started, make sure that you're familiar with the following:</span></span>
- [<span data-ttu-id="2d0f7-107">Grundlegendes zum SharePoint-REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="2d0f7-107">Get to know the SharePoint REST service</span></span>](https://dev.office.com/sharepoint/docs/apis/rest/get-to-know-the-sharepoint-rest-service.md) 
- [<span data-ttu-id="2d0f7-108">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="2d0f7-108">Complete basic operations using SharePoint REST endpoints</span></span>](https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints.md)

## <a name="rest-commands-for-site-themes"></a><span data-ttu-id="2d0f7-109">REST-Befehle für Websitedesigns</span><span class="sxs-lookup"><span data-stu-id="2d0f7-109">REST commands for site themes</span></span>

<span data-ttu-id="2d0f7-110">Für Websitedesigns stehen die folgenden REST-Befehle zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="2d0f7-110">The following REST commands are available for working with site themes:</span></span>

* <span data-ttu-id="2d0f7-111">__AddTenantTheme__ &mdash; Erstellt ein neues Design, ähnlich wie das SharePoint-Cmdlet „Add-SPOTheme“.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-111">__AddTenantTheme__ &mdash; create a new theme; similar to the Add-SPOTheme SharePoint cmdlet</span></span>
* <span data-ttu-id="2d0f7-112">__RemoveTenantTheme__ &mdash; Entfernt ein Design aus dem Store des Mandanten, ähnlich wie das PowerShell-Cmdlet „Remove-SPOTheme“.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-112">__RemoveTenantTheme__ &mdash; remove a theme from the tenant store; similar to the Remove-SPOTheme PowerShell cmdlet</span></span>
* <span data-ttu-id="2d0f7-113">__GetTenantThemingOptions__ &mdash; Ruft die Designeinstellungen ab.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-113">__GetTenantThemingOptions__ &mdash; read theme settings</span></span>

<span data-ttu-id="2d0f7-114">Basis für die URL von REST-Befehlen zur Designverwaltung ist die Zeichenfolge „_api/thememanager“.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-114">The URL for theme management REST commands is based on _api/thememanager.</span></span> <span data-ttu-id="2d0f7-115">Die Endpunkte für die oben aufgeführten Befehle beispielsweise sehen wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="2d0f7-115">For example, the following are the endpoints for the commands:</span></span>

* <span data-ttu-id="2d0f7-116">http://<site url>/_api/thememanager/AddTenantTheme</span><span class="sxs-lookup"><span data-stu-id="2d0f7-116">http://<site url>/_api/thememanager/AddTenantTheme</span></span>
* <span data-ttu-id="2d0f7-117">http://<site url>/_api/thememanager/RemoveTenantTheme</span><span class="sxs-lookup"><span data-stu-id="2d0f7-117">http://<site url>/_api/thememanager/RemoveTenantTheme</span></span>
* <span data-ttu-id="2d0f7-118">http://<site url>/_api/thememanager/GetTenantThemingOptions</span><span class="sxs-lookup"><span data-stu-id="2d0f7-118">http://<site url>/_api/thememanager/GetTenantThemingOptions</span></span>

## <a name="addtenanttheme"></a><span data-ttu-id="2d0f7-119">AddTenantTheme</span><span class="sxs-lookup"><span data-stu-id="2d0f7-119">AddTenantTheme</span></span>

<span data-ttu-id="2d0f7-120">Der folgende JavaScript-Beispielcode demonstriert, wie Sie einem Mandanten ein neues Design hinzufügen können:</span><span class="sxs-lookup"><span data-stu-id="2d0f7-120">The following JavaScript sample code shows how to add a new theme to a tenant.</span></span>

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
## <a name="removetenanttheme"></a><span data-ttu-id="2d0f7-121">RemoveTenantTheme</span><span class="sxs-lookup"><span data-stu-id="2d0f7-121">RemoveTenantTheme</span></span>
<span data-ttu-id="2d0f7-122">Der folgende JavaScript-Beispielcode demonstriert, wie Sie Designs entfernen können:</span><span class="sxs-lookup"><span data-stu-id="2d0f7-122">The following JavaScript sample code shows how to remove a theme.</span></span>

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

## <a name="gettenantthemingoptions"></a><span data-ttu-id="2d0f7-123">GetTenantThemingOptions</span><span class="sxs-lookup"><span data-stu-id="2d0f7-123">GetTenantThemingOptions</span></span>
<span data-ttu-id="2d0f7-124">Der folgende JavaScript-Beispielcode demonstriert, wie Sie die Einstellungen eines Designs auslesen können.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-124">The following JavaScript sample code shows how to read theme settings.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="2d0f7-125">Weitere Artikel</span><span class="sxs-lookup"><span data-stu-id="2d0f7-125">See also</span></span>

* [<span data-ttu-id="2d0f7-126">Überblick über das SharePoint-Websitedesign</span><span class="sxs-lookup"><span data-stu-id="2d0f7-126">SharePoint site theming overview</span></span>](sharepoint-site-theming-overview.md)
* [<span data-ttu-id="2d0f7-127">SharePoint-Websitedesign: JSON-Schema</span><span class="sxs-lookup"><span data-stu-id="2d0f7-127">SharePoint site theming: JSON schema</span></span>](sharepoint-site-theming-json-schema.md)
* [<span data-ttu-id="2d0f7-128">SharePoint-Websitedesign: PowerShell-Cmdlets</span><span class="sxs-lookup"><span data-stu-id="2d0f7-128">SharePoint site theming: PowerShell cmdlets</span></span>](sharepoint-site-theming-powershell.md)
* [<span data-ttu-id="2d0f7-129">SharePoint-Websitedesign: CSOM</span><span class="sxs-lookup"><span data-stu-id="2d0f7-129">SharePoint site theming: CSOM</span></span>](sharepoint-site-theming-csom.md)
* [<span data-ttu-id="2d0f7-130">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="2d0f7-130">Complete basic operations using SharePoint REST endpoints</span></span>](https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints.md)
* [<span data-ttu-id="2d0f7-131">Making REST calls with C# and JavaScript for SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="2d0f7-131">Making REST calls with C# and JavaScript for SharePoint 2013</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/video.mdl?cid=sdc&from=mscomsdc&VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)

