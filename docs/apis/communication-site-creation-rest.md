# <a name="creating-sharepoint-communication-site-using-rest"></a>Erstellen einer SharePoint-Kommunikationswebsite mithilfe von REST

In diesem Artikel erfahren Sie, wie Sie mithilfe der REST-Schnittstelle eine neue moderne SharePoint-Kommunikationswebsite erstellen und deren Status abrufen können.

## <a name="prerequisites"></a>Voraussetzungen

In diesem Artikel setzen wir voraus, dass Sie bereits den Artikel „Grundlegendes zum SharePoint-REST-Dienst“ sowie den Artikel „Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten“ gelesen haben. Es werden keine Codeausschnitte bereitgestellt.

Zur Erstellung moderner SharePoint-Kommunikationswebsites stehen die folgenden REST-Befehle zur Verfügung:

- **Create**: Erstellt eine neue SharePoint-Kommunikationswebsite.
- **Status**: Ruft den Status einer SharePoint-Kommunikationswebsite ab. 

Basis für die URL von REST-Befehlen für Kommunikationswebsites ist die Zeichenfolge `_api/sitepages/communicationsite`. Die Endpunkte für die oben aufgeführten Befehle beispielsweise sehen wie folgt aus:

- `http:///_api/sitepages/communicationsite/create`
- `http:///_api/sitepages/communicationsite/status`

## <a name="create-communication-site"></a>Erstellen einer Kommunikationswebsite

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
> Der Parameter „lcid“ wird von dieser API derzeit nicht unterstützt. Aktuell lassen sich nur englischsprachige Websites erstellen. 

Das Konzept „SiteDesignID“ wurde in dieser API neu eingeführt. Ähnlich wie der Websiteerstellungsfluss innerhalb des Produkts verweist der Parameter „SiteDesignID“ auf die eingeschlossenen Websitedesigns. Dies sind:

- Topic: null
- Showcase: 6142d2a0-63a5-4ba0-aede-d9fefca2c767
- Blank: f6cc5403-0d63-442e-96c0-285923709ffc

**Antwort**

Bei fehlerfreier Ausführung gibt die Methode im Antworttext den Antwortcode „200, OK“ zurück sowie ein einfaches JSON-Objekt mit den folgenden Informationen:

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


## <a name="get-communication-site-status"></a>Abrufen des Status einer Kommunikationswebsite

Die REST-API zum Abrufen des Status einer modernen SharePoint-Kommunikationswebsite sieht wie folgt aus:

```
url: /_api/sitepages/communicationsite/status?url='https%3A%2F%2Fcontoso.sharepoint.com%2Fsites%2Fcomm1'
method: GET
body: none
```

**Antwort**

Bei fehlerfreier Ausführung gibt die Methode im Antworttext den Antwortcode „200, OK“ zurück sowie ein einfaches JSON-Objekt mit den folgenden Informationen:
 
Existiert die Website, gibt die Antwort den Status der Website sowie die URL der Website zurück.

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

Existiert die Website nicht, gibt die Antwort als Status der Website den Wert „0“ zurück, ohne URL.

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