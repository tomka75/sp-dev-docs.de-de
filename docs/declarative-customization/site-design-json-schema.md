---
title: JSON-Schema eines Websitedesigns
description: "JSON-Schemareferenz zum Erstellen von Websitedesigns für SharePoint."
ms.date: 12/14/2017
ms.openlocfilehash: 0b1d0a0bd79d89e269744ca0646eb30b4ed0e731
ms.sourcegitcommit: 8e63066ad9591e51bbda419b1b9527452111081b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="site-design-json-schema"></a>JSON-Schema eines Websitedesigns

> [!NOTE]
> Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden. Sie werden in Produktionsumgebungen derzeit nicht unterstützt.

Das Websitedesign besteht aus einer Liste von Aktionen. Für komplexere Aktionen, z. B. das Erstellen einer Liste, gibt es auch Unteraktionen. Jede Aktion wird durch den Wert „verb“ angegeben. Verb-Aktionen werden in der Reihenfolge ausgeführt, in der Sie im JSON-Skript angezeigt werden.

Die allgemeine JSON-Struktur wird wie folgt angegeben:

```json
{
    "$schema": "schema.json",
        "actions": [
            ...
            <one or more verb actions>
            ...
        ],
        "bindata": { },
        "version": 1
};
```

## <a name="create-a-new-sharepoint-list"></a>Erstellen einer neuen SharePoint-Liste

Verwenden Sie das Verb **createSPList**, um eine neue SharePoint-Liste zu erstellen.

JSON-Werte:

- **listName** - Der Name der Liste, anhand der Benutzer diese identifzieren können.
- **templateType** - Welche Vorlage auf die Liste angewendet werden soll. In der Regel wird der Wert „100“ verwendet. Vorlagentypwerte sind in [SPListTemplateType-Enumeration]((https://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.splisttemplatetype.aspx)) dokumentiert.
- **subactions** - Ein Array von Aktionen, die in der aufgeführten Reihenfolge ausgeführt werden, um Ihre Liste zu erstellen.

Beispiel:

```json
{
    "verb": "createSPList",
    "listName": "Customer Tracking",
    "templateType": 100,
    "subactions": [
        {
            "verb": "SetDescription",
            "description": "List of Customers and Orders"
         }
    ]
}
```

Das Array mit Unteraktionen bietet zusätzliche Aktionen, um anzugeben, wie die Liste erstellt wird. Unteraktionen werden auch mithilfe eines **verb**-Werts angegeben.

### <a name="settitle"></a>setTitle

Legt einen Titel fest, der die Liste in Ansichten identifiziert.

JSON-Wert:

- **title** - Der Titel der neuen Liste.

Beispiel:

```json
{
   "verb": "setTitle",
   "title": "Customers and Orders"
}
```

### <a name="setdescription"></a>setDescription

Legt die Beschreibung der Liste fest.

JSON-Wert:

- **description** - Die Beschreibung der neuen Liste.

Beispiel:

```json
{
   "verb": "SetDescription",
   "description": "List of Customers and Orders"
}
```

### <a name="addspfield"></a>addSPField

Fügt ein neues Feld hinzu.

JSON-Werte:

- **fieldType** - Der Feldtyp kann auf **Text**, **Note**, **Number**, **Boolean**, **User** oder **DateTime** festgelegt werden.
- **displayName** - Der Anzeigename des Felds.
- **isRequired** - „True“, wenn dieses Feld Informationen enthalten muss, andernfalls „False“.
- **addToDefaultView** - „True“, wenn das Feld der Standardansicht hinzugefügt wird, andernfalls „False“.

Beispiel:

```json
{
   "verb": "addSPField",
   "fieldType": "Text",
   "displayName": "Customer Name",
   "isRequired": false,
   "addToDefaultView": true
}
```

### <a name="deletespfield"></a>deleteSPField

Löscht ein Standardfeld, das vom ausgewählten Vorlagentyp bereitgestellt wurde.

JSON-Wert:

- **displayName** - Der Anzeigename, um das zu löschende Feld zu identifzieren.

Beispiel:

```json
{
   "verb": "deleteSPField",
   "displayName": "Modified"
}
```

### <a name="addcontenttype"></a>addContentType

Fügte einen Inhaltstyp zu der Liste hinzu.

JSON-Wert:

- **name** - Der Name des hinzuzufügenden Inhaltstyps.

Beispiel:

```json
{
   "verb": "addContentType",
   "name": "name"
}
```

### <a name="removecontenttype"></a>removeContentType

Entfernt einen Inhaltstyp, der vom ausgewählten Vorlagentyp bereitgestellt wurde.

JSON-Wert:

- **name** - Der Name des zu entfernenden Inhaltstyps.

Beispiel:

```json
{
   "verb": "removeContentType",
   "name": "name"
}
```

### <a name="setspfieldcustomformatter"></a>setSPFieldCustomFormatter

Legt die Spaltenformatierung für ein Feld fest. Weitere Informationen zur Spaltenformatierung finden Sie unter [Anpassen von SharePoint mithilfe von Spaltenformatierungen](column-formatting.md).

JSON-Werte:

- **fieldDisplayName** - Der Anzeigename des zu verwendenden Felds.
- **formatterJSON** - Ein JSON-Objekt, das als das CustomFormatter-Feld verwendet werden soll.

Beispiel:

```json
{
   "verb": "setSPFieldCustomFormatter",
   "fieldDisplayName": "name",
   "formatterJSON": "json" 
}
```
<!-- TBD provide an example for formatterJSON in previous example -->

## <a name="add-a-navigation-link"></a>Hinzufügen eines Navigationslinks

Verwenden Sie das Verb **addNavLink**, um der Website einen neuen Navigationslink hinzuzufügen.

JSON-Werte:

- **url** - Die URL des hinzuzufügenden Links.
- **displayName** - Der Anzeigename des Links.
- **isWebRelative** - „True“, wenn der Link relativ zum Web ist, andernfalls „False.“

Beispiel:

```json
{
   "verb": "addNavLink",
   "url": "/Customer Event Collateral",
   "displayName": "Event Collateral",
   "isWebRelative": true
}
```

## <a name="apply-a-theme"></a>Anwenden eines Designs

Verwenden Sie das Verb **applyTheme**, um der Website ein Design hinzuzufügen. Weitere Informationen zu Designs finden Sie unter [SharePoint-Websitedesign](site-theming/sharepoint-site-theming-overview.md).

JSON-Wert:

- **themeName** - Der Name des anzuwendenden Designs.

Beispiel:

<!-- TBD: add link to Doug's Blue Yonder theme with note you need to create it first -->

```json
{
   "verb": "applyTheme",
   "themeName": "Blue Yonder"
}
```

<!-- 
## Create a page

Use the **createPage** verb to create a new page on the site.

JSON values:

- **fileName** - The name of the file.
- **setAsHomePage** - True if this page is the home page; otherwise, false.
- **pageData** - An object with additional information about the page. **pageData** requires the following values:
  - **Title** - The title of the page.
  - **BannerImageUrl** - A URL specifying the location of an image to display for the banner. <TBD: need more info>
  - **CanvasContent1** - Content for the page specified as XML. <TBD: need more info>
  - **LayoutWebpartsContent** - JSON for the layout. <TBD: need more info>

Example:

```json
{
   "verb": "createPage",
   "fileName": "event-collateral.aspx",
   "pageData":
        {
            "Title": "Comment customer events",
            "BannerImageUrl": "/Customer Event Collateral/customer.jpg",
            "CanvasContent1": "<xml>",
            "LayoutWebpartsContent": "{json}"
        },
    "setAsHomePage": true
}
```
-->

## <a name="set-a-site-logo"></a>Festlegen eines Websitelogos

Verwenden Sie das Verb **setSiteLogo**, um ein Logo für Ihre Website anzugeben. Diese Aktion funktioniert nur für die Kommunikationswebsitevorlage (68).

JSON-Wert:

- **url** - Die URL des zu verwendenden Logobilds.

Beispiel:

```json
{
    "verb": "setSiteLogo",
    "url": "/Customer Event Collateral/logo.jpg"
}
```

## <a name="join-a-hub-site"></a>Beitreten zu einem Hub-Standort

Verwenden Sie das Verb **joinHubSite**, um die Website einem Hub hinzuzufügen. <!-- TBD provide link to more information on hubs and how to get the id -->

JSON-Wert:

- **hubSiteId** - Die ID des Hub-Standorts für den Beitritt.

Beispiel:

```json
{
    "verb": "joinHubSite",
    "hubSiteId": "e337cc17-b355-45d2-8dd4-e056f1bcf6f6"
}
```

## <a name="trigger-a-flow"></a>Auslösen eines Flusses

Verwenden Sie das Verb **triggerFlow**, um einen benutzerdefinierten Fluss auzulösen.
<!-- update this with example from trigger workflow topic -->

JSON-Werte:

- **url** - Eine Trigger-URL des Flusses.
- **name** - Der Name des Flusses.
- **parameters** - Ein optionaler Satz von Parameter, die an den Fluss übergeben werden.

Beispiel:

```json
 {
    "verb": "triggerFlow",
    "url": "<A trigger URL of the Flow.>",
    "name": "Record and tweet site creation event",
    "parameters": {
        "event": "Microsoft Event",
        "product": "SharePoint"
    }
}
```
