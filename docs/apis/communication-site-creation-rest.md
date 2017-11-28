# <a name="creating-sharepoint-communication-site-using-rest"></a><span data-ttu-id="cafa4-101">Erstellen einer SharePoint-Kommunikationswebsite mithilfe von REST</span><span class="sxs-lookup"><span data-stu-id="cafa4-101">Creating SharePoint Communication Site using REST</span></span>

<span data-ttu-id="cafa4-102">In diesem Artikel erfahren Sie, wie Sie mithilfe der REST-Schnittstelle eine neue moderne SharePoint-Kommunikationswebsite erstellen und deren Status abrufen können.</span><span class="sxs-lookup"><span data-stu-id="cafa4-102">Learn how to create and get the status of a new modern SharePoint Communication site with the REST interface.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cafa4-103">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="cafa4-103">Prerequisites</span></span>

<span data-ttu-id="cafa4-104">In diesem Artikel setzen wir voraus, dass Sie bereits den Artikel „Grundlegendes zum SharePoint-REST-Dienst“ sowie den Artikel „Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten“ gelesen haben.</span><span class="sxs-lookup"><span data-stu-id="cafa4-104">This topic assumes that you are already familiar with the topics Get to know the SharePoint REST service and Complete basic operations using SharePoint REST endpoints.</span></span> <span data-ttu-id="cafa4-105">Es werden keine Codeausschnitte bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="cafa4-105">It does not provide code snippets.</span></span>

<span data-ttu-id="cafa4-106">Zur Erstellung moderner SharePoint-Kommunikationswebsites stehen die folgenden REST-Befehle zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="cafa4-106">The following REST commands are available for creating a modern SharePoint Communication site.</span></span>

- <span data-ttu-id="cafa4-107">**Create**: Erstellt eine neue SharePoint-Kommunikationswebsite.</span><span class="sxs-lookup"><span data-stu-id="cafa4-107">**Create** - Create a new SharePoint Communication site</span></span>
- <span data-ttu-id="cafa4-108">**Status**: Ruft den Status einer SharePoint-Kommunikationswebsite ab.</span><span class="sxs-lookup"><span data-stu-id="cafa4-108">**Status** - Get the status of a SharePoint Communication site</span></span> 

<span data-ttu-id="cafa4-109">Basis für die URL von REST-Befehlen für Kommunikationswebsites ist die Zeichenfolge `_api/sitepages/communicationsite`.</span><span class="sxs-lookup"><span data-stu-id="cafa4-109">The URL for communication site REST commands is based on `_api/sitepages/communicationsite`.</span></span> <span data-ttu-id="cafa4-110">Die Endpunkte für die oben aufgeführten Befehle beispielsweise sehen wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="cafa4-110">For example, these are the endpoints for the commands listed above:</span></span>

- `http:///_api/sitepages/communicationsite/create`
- `http:///_api/sitepages/communicationsite/status`

## <a name="create-communication-site"></a><span data-ttu-id="cafa4-111">Erstellen einer Kommunikationswebsite</span><span class="sxs-lookup"><span data-stu-id="cafa4-111">Create Communication Site</span></span>

```
url: /_api/sitepages/communicationsite/create
method: POST
body:
{
   "request":{
      "__metadata":{
         "type":"SP.Publishing.CommunicationSiteCreationRequest"
      },
      "AllowFileSharingForGuestUsers":false,
      "Classification":"LBI",
      "Description":"Description",
      "SiteDesignId":"6142d2a0-63a5-4ba0-aede-d9fefca2c767",
      "Title":"Comm Site 1",
      "Url":"https://vesku.sharepoint.com/sites/commsite132",
      "lcid":1033
   }
}
```

> [!IMPORTANT]
> <span data-ttu-id="cafa4-112">Der Parameter „lcid“ wird von dieser API derzeit nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="cafa4-112">lcid parameter is not currently supported with this API.</span></span> <span data-ttu-id="cafa4-113">Aktuell lassen sich nur englischsprachige Websites erstellen.</span><span class="sxs-lookup"><span data-stu-id="cafa4-113">You can currently only create English sites.</span></span> 

<span data-ttu-id="cafa4-114">Das Konzept „SiteDesignID“ wurde in dieser API neu eingeführt.</span><span class="sxs-lookup"><span data-stu-id="cafa4-114">New in this API is the concept of SiteDesignID.</span></span> <span data-ttu-id="cafa4-115">Ähnlich wie der Websiteerstellungsfluss innerhalb des Produkts verweist der Parameter „SiteDesignID“ auf die eingeschlossenen Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="cafa4-115">Much like the in-product site creation flow, the SiteDesignID parameter maps to the included site designs.</span></span> <span data-ttu-id="cafa4-116">Dies sind:</span><span class="sxs-lookup"><span data-stu-id="cafa4-116">They are:</span></span>

- <span data-ttu-id="cafa4-117">Topic: null</span><span class="sxs-lookup"><span data-stu-id="cafa4-117">Topic: null</span></span>
- <span data-ttu-id="cafa4-118">Showcase: 6142d2a0-63a5-4ba0-aede-d9fefca2c767</span><span class="sxs-lookup"><span data-stu-id="cafa4-118">Showcase: 6142d2a0-63a5-4ba0-aede-d9fefca2c767</span></span>
- <span data-ttu-id="cafa4-119">Blank: f6cc5403-0d63-442e-96c0-285923709ffc</span><span class="sxs-lookup"><span data-stu-id="cafa4-119">Blank: f6cc5403-0d63-442e-96c0-285923709ffc</span></span>

<span data-ttu-id="cafa4-120">**Antwort**</span><span class="sxs-lookup"><span data-stu-id="cafa4-120">**Response**</span></span>

<span data-ttu-id="cafa4-121">Bei fehlerfreier Ausführung gibt die Methode im Antworttext den Antwortcode „200, OK“ zurück sowie ein einfaches JSON-Objekt mit den folgenden Informationen:</span><span class="sxs-lookup"><span data-stu-id="cafa4-121">If successful, this method returns 200, OK response code and simple JSON object in the response body with following details.</span></span>

```
{
  "d":{
      "Create":{
           "__metadata":{"type":"SP.Publishing.CommunicationSiteCreationResponse"},
          "SiteStatus":2,
          "SiteUrl":"https://contoso.sharepoint.com/sites/comm1"
      }
  }
}
```


## <a name="get-communication-site-status"></a><span data-ttu-id="cafa4-122">Abrufen des Status einer Kommunikationswebsite</span><span class="sxs-lookup"><span data-stu-id="cafa4-122">Get Communication Site Status</span></span>

<span data-ttu-id="cafa4-123">Die REST-API zum Abrufen des Status einer modernen SharePoint-Kommunikationswebsite sieht wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="cafa4-123">REST API for getting the status of a modern SharePoint Communication site</span></span>

```
url: /_api/sitepages/communicationsite/status?url='https%3A%2F%2Fcontoso.sharepoint.com%2Fsites%2Fcomm1'
method: GET
body: none
```

<span data-ttu-id="cafa4-124">**Antwort**</span><span class="sxs-lookup"><span data-stu-id="cafa4-124">**Response**</span></span>

<span data-ttu-id="cafa4-125">Bei fehlerfreier Ausführung gibt die Methode im Antworttext den Antwortcode „200, OK“ zurück sowie ein einfaches JSON-Objekt mit den folgenden Informationen:</span><span class="sxs-lookup"><span data-stu-id="cafa4-125">If successful, this method returns 200, OK response code and simple JSON object in the response body with following details.</span></span>
 
<span data-ttu-id="cafa4-126">Existiert die Website, gibt die Antwort den Status der Website sowie die URL der Website zurück.</span><span class="sxs-lookup"><span data-stu-id="cafa4-126">If the site exists, the response will return the site status and site URL.</span></span>

```
{
  "d":{
      "Status":{
           "__metadata":{"type":"SP.Publishing.CommunicationSiteCreationResponse"},
          "SiteStatus":2,
          "SiteUrl":"https://contoso.sharepoint.com/sites/comm1"
      }
  }
}
```

<span data-ttu-id="cafa4-127">Existiert die Website nicht, gibt die Antwort als Status der Website den Wert „0“ zurück, ohne URL.</span><span class="sxs-lookup"><span data-stu-id="cafa4-127">If the site does not exist, the response will return site status of 0 with no URL.</span></span>

```
{
  "d":{
      "Status":{
           "__metadata":{"type":"SP.Publishing.CommunicationSiteCreationResponse"},
          "SiteStatus":0,
          "SiteUrl":
      }
  }
}
```