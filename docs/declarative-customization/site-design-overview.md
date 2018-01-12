---
title: "Übersicht über das SharePoint-Websitedesign und -Websiteskripts"
description: Verwenden Sie SharePoint-Websiteskripts und -Websitedesigns, um die Bereitstellung neuer SharePoint-Websites mit neuen Konfigurationen zu automatisieren.
ms.date: 12/14/2017
ms.openlocfilehash: 5821c4a48ecccbfc23ff5eaaf1c7941c6026d06e
ms.sourcegitcommit: 31f793b42ec75679f01e1a024d0375a2bc7b5ec7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2017
---
# <a name="sharepoint-site-design-and-site-script-overview"></a>Übersicht über das SharePoint-Websitedesign und -Websiteskripts

> [!NOTE]
> Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden. Sie werden in Produktionsumgebungen derzeit nicht unterstützt.

Verwenden Sie Websiteskripts und Websitedesigns, um die Bereitstellung neuer SharePoint-Websites mit Ihren eigenen benutzerdefinierten Konfigurationen zu automatisieren. Wenn Personen in Ihrem Unternehmen neue SharePoint-Websites erstellen, müssen Sie häufig ein gewisses Maß an Konsistenz sicherstellen. Vielleicht benötigen Sie für jede neue Website ein entsprechendes Branding und passende Designs. Vielleicht haben Sie auch detaillierte Bereitstellungsskripts, z. B. die Verwendung des PnP-Bereitstellungsmoduls, die immer dann angewendet werden müssen, wenn eine neue Website erstellt wird. In diesem Artikel wird beschrieben, wie Sie Websitedesigns und Websiteskripts verwenden können, um benutzerdefinierte Konfigurationen bereitzustellen, die angewendet werden, wenn neue Websites erstellt werden.

## <a name="how-site-designs-work"></a>Funktionsweise von Websitedesigns

Websitedesigns sind wie eine Vorlage. Sie können immer dann verwendet werden, wenn eine neue Website erstellt wird, um einen konsistenten Satz von Aktionen anzuwenden. Die meisten Aktionen betreffen in der Regel die Website selbst, z. B. das Festlegen des Designs oder das Erstellen von Listen. Ein Websitedesign kann jedoch auch andere Aktionen umfassen, z. B. das Aufzeichnen der URL der neuen Website in einem Protokoll oder das Senden eines Tweets.

Websitedesigns werden in SharePoint auf einer der modernen Vorlagenwebsites erstellt und registriert: auf der Teamwebsite oder auf der Kommunikationswebsite. In den folgenden Schritten können Sie sehen, wie dies funktioniert.

1. Gehen Sie in Ihrem Entwicklermandanten auf die SharePoint-Startseite.
1. Wählen Sie **Website erstellen** aus.

    Sie sehen die beiden modernen Vorlagenwebsites: die **Teamwebsite** und **Kommunikationswebsite**.

1. Wählen Sie **Kommunikationswebsite** aus.

    Die Kommunikationswebsite weist das Feld **Design auswählen**, in dem die folgenden Websitedesigs zur Verfügung stehen.

    - Thema
    - Showcase
    - Leer

Dies sind die standardmäßigen Websitedesigns. Jedes Websitedesign weist einen Titel, eine Beschreibung und ein Bild auf.

![Titel, Beschreibung und Bild im standardmäßigen Websitedesign in der Kommunikationswebsite-Vorlage](images/site-designs-listed-on-communication-site-template.png)

Wenn Sie die Vorlage für die Teamwebsite ausgewählt hätten, würde diese nur das standardmäßige Websitedesign mit dem Namen **Teamwebsite** enthalten. Weitere Informationen dazu, wie Sie die standardmäßigen Websitedesigns ändern können, finden Sie unter [Anpassen eines standardmäßigen Websitedesigns](customize-default-site-design.md).

Nachdem ein Websitedesign ausgewählt wurde, erstellt SharePoint die neue Website und führt Websiteskripts für das Websitedesign aus. In den Websiteskripts ist die Arbeit wie z. B. das Erstellen neuer Listen oder das Anwenden eines Designs aufgeführt. Wenn die Aktionen in den Skripts abgeschlossen sind, zeigt SharePoint die ausführlichen Ergebnisse dieser Aktionen in einer Statusanzeige an.

![Statusanzeige, in der die abgeschlossenen Aktionen in einem Websitedesign aufgeführt sind](images/progress-pane.png)

## <a name="anatomy-of-a-site-script"></a>Anatomie eines Websiteskripts

Bei Websiteskripts handelt es sich um JSON-Dateien, die eine sortierte Liste von Aktionen angeben, die beim Erstellen der neuen Website ausgeführt werden. Die Aktionen werden in der aufgeführten Reihenfolge ausgeführt. Das folgende Beispiel ist ein Skript, das über zwei Aktionen auf oberster Ebene verfügt. Zuerst wird ein Design angewendet, das zuvor mit dem Namen **Contoso Explorers** erstellt wurde. Anschließend wird die Liste **Kundennachverfolgung** erstellt.

```json
{
  "$schema": "schema.json",
  "actions": [
    {
      "verb": "applyTheme",
      "themeName": "Contoso Explorers"
    },
    {
      "verb": "createSPList",
      "listName": "Customer Tracking",
      "templateType": 100,
      "subactions": [
        {
          "verb": "SetDescription",
          "description": "List of Customers and Orders"
        },
        {
          "verb": "addSPField",
          "fieldType": "Text",
          "displayName": "Customer Name",
          "isRequired": false,
          "addToDefaultView": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Number",
          "displayName": "Requisition Total",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
          "fieldType": "User",
          "displayName": "Contact",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Note",
          "displayName": "Meeting Notes",
          "isRequired": false
        }
      ]
    }
  ],
  "bindata": { },
  "version": 1
}
```

Jede Aktion in einem Websiteskript wird vom Wert **verb** im JSON-Skript angegeben. Im vorherigen Skript wird die erste Aktion vom Verb **applyTheme** angegeben. Dann erstellt das Verb **createSPList** die Liste. Beachten Sie, dass das Verb **createSPList** seinen eigenen Satz von Verben enthält, die zusätzliche Aktionen nur für die Liste ausführen.

Verfügbare Aktionen umfassen:

- Erstellen einer neuen Liste
- Anwenden eines Designs
- Erstellen einer Seite
- Festlegen eines Websitelogos
- Hinzufügen einer Nagivation
- Auslösen eines Microsoft-Flusses

Websiteskripts können nach der Bereitstellung erneut auf derselben Website ausgeführt werden. Dies kann nur programmgesteuert erfolgen. Websiteskripts sind nicht destruktiv, wenn sie also erneut ausgeführt werden, wird sichergestellt, dass die Website der Konfiguration im Skript entspricht. Wenn die Website beispielsweise bereits eine Liste mit demselben Namen aufweist, den das Websiteskript erstellt, fügt das Websiteskripts nur fehlende Felder zu der vorhandenen Liste hinzu.

## <a name="using-powershell-or-rest-to-work-with-site-designs-and-site-scripts"></a>Verwenden von PowerShell oder REST zum Arbeiten mit Websitedesigns und Websiteskripts

Sie können Websitedesigns und Websiteskripts mithilfe von PowerShell oder der REST-API erstellen. Im folgenden Beispiel wird ein Websiteskript und ein Websitedesign erstellt, das das Websiteskript verwendet. <!-- The PowerShell example loads the script from a file, while the REST example has the script inline. -->

```powershell
C:\> Get-Content 'c:\scripts\site-script.json' `
     -Raw | `
     Add-SPOSiteScript `
    -Title "Contoso theme and list"

Id          : 2756067f-d818-4933-a514-2a2b2c50fb06
Title       : Contoso theme and list
Description :
Content     :
Version     : 0

C:\> Add-SPOSiteDesign `
  -Title "Contoso customer tracking" `
  -WebTemplate "64" `
  -SiteScripts "2756067f-d818-4933-a514-2a2b2c50fb06" `
  -Description "Creates customer list and applies standard theme"
```

<!-- 
```javascript
var site_script = {
  "$schema": "schema.json",
  "actions": [
    {
      "verb": "applyTheme",
      "themeName": "Contoso Explorers"
    },
    {
      "verb": "createSPList",
      "listName": "Customer Tracking",
      "templateType": 100,
      "subactions": [
        {
          "verb": "SetDescription",
          "description": "List of Customers and Orders"
        },
        {
          "verb": "addSPField",
          "fieldType": "Text",
          "displayName": "Customer Name",
          "isRequired": false,
          "addToDefaultView": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Number",
          "displayName": "Requisition Total",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
          "fieldType": "User",
          "displayName": "Contact",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Note",
          "displayName": "Meeting Notes",
          "isRequired": false
        }
      ]
    }
  ],
  "bindata": { },
  "version": 1
};

RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteScript(Title=@title)?@title='Contoso theme and list'", site_script);

RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteDesign",{
  info:{
    Title:"Contoso customer tracking", Description:"Creates customer list and applies standard theme",  SiteScriptIds:["607aed52-6d61-490a-b692-c0f58a6981a1"],  WebTemplate:"64"
   }
  });
```
-->

Im vorherigen Beispiel gibt das Cmdlet **Add-SPOSiteScript** oder die REST-API **CreateSiteScript** eine Websiteskript-ID zurück. Diese wird für den Parameter **SiteScripts** im nachfolgenden Aufruf des Cmdlets **Add-SPO-SiteDesign** oder der REST-API **CreateSiteDesign** verwendet.

Der auf den Wert „64“ festgelegte Parameter **WebTemplate** gibt an, dass das Websitedesign bei der Teamwebsitevorlage registriert werden soll. Der Wert „68“ würde auf die Kommunikationswebsitevorlage hinweisen. Die Parameter **Title** und **Description** werden angezeigt, wenn ein Benutzer Websitedesigns beim Erstellen einer neuen Teamwebsite ansieht.

> [!NOTE]
> Ein Websitedesign kann mehrere Skripts ausführen. Die Skript-IDs werden in einem Array übergeben und werden in der aufgeführten Reihenfolge ausgeführt.

Schrittweise Anweisungen zum Erstellen eines Websitedesigns finden Sie unter [Erste Schritte mit dem Erstellen von Websitedesigns](get-started-create-site-design.md).

## <a name="pnp-provisioning-and-customization-using-microsoft-flow"></a>PnP-Bereitstellung und Anpassung mithilfe von Microsoft Flow

Eine von Websiteskripts bereitgestellte Aktion ist die Möglichkeit, einen Microsoft-Fluss auszulösen. Auf diese Weise können Sie beliebige benutzerdefinierte Aktionen angeben, die Sie über die systemeigen in Websiteskripts bereitgestellten Aktionen benötigen.

Wenn Sie das PnP-Bereitstellungsmodul zum Automatisieren der Websiteerstellung verwenden, können Sie einen Microsoft Flow zur Integration in Websitedesigns verwenden. Mithilfe dieser Technik können Sie alle vorhandenen Bereitstellungsskripts beibehalten und auch neue benutzerdefinierte Bereitstellungsskripts erstellen.

![Prozess des Auslösens eines Microsoft-Flusses](images/process-for-triggering-a-custom-flow.png)

Dieser Prozess funktioniert folgendermaßen:

1. Das Skript instanziiert Ihren Microsoft-Fluss mithilfe einer URL mit zusätzlichen Details.
1. Der Flow sendet eine Nachricht an die Azure-Speicherwarteschlage, die Sie konfiguriert haben.
1. Die Nachricht löst einen Aufruf einer Azure-Funktion aus, die Sie konfiguriert haben.
1. Die Azure-Funktion führt Ihr benutzerdefiniertes Skript aus, z. B. das PnP-Bereitstellungsmoduls, um Ihre benutzerdefinierten Konfigurationen anzuwenden.

Ein schrittweises Lernprogramm zum Konfigurieren Ihres eigenen Microsoft-Flusses mit der PnP-Bereitstellung finden Sie unter [Erstellen eines vollständigen Websitedesigns mithilfe des PnP-Bereitstellungsmoduls](site-design-pnp-provisioning.md)

## <a name="scoping"></a>Bereichsdefinition

Sie können Websitedesigns so konfigurieren, dass sie nur für bestimmte Gruppen oder Personen in Ihrer Organisation angezeigt werden. Dies ist hilfreich, um sicherzustellen, dass Personen nur die für sie beabsichtigten Websitedesigns sehen. Vielleicht möchten Sie, dass die Buchhaltungsabteilung nur Websitedesigns sieht, die für sie gedacht sind. Und die Websitedesigns der Buchhaltung sind möglicherweise für andere Personen nicht sinnvoll.

Ein Websitedesign kann standardmäßig bei Erstellung von jeder Person angezeigt werden. Bereiche werden mit dem Cmdlet **Grant-SPOSiteDesignRights** oder der REST-API **GrantSiteDesignRights** angewendet.  Sie können den Bereich nach Benutzer oder nach einer E-Mail-aktivierten Sicherheitsgruppe angeben. Im folgenden Beispiel wird gezeigt, wie Anzeigeberechtigungen für einen Nestor (ein Benutzer auf der fiktiven Contoso-Website) in einem Websitedesign hinzugefügt werden.

> [!div class="tabbedCodeSnippets"]
```powershell
Grant-SPOSiteDesignRights `
  -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
  -Principals "nestorw@contoso.onmicrosoft.com" `
  -Rights View
```

<!--
```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GrantSiteDesignRights", {id:"44252d09-62c4-4913-9eb0-a2a8b8d7f863", principalNames:["nestorw@contoso.onmicrosoft.com”], grantedRights:1});
```
-->
Weitere Informationen zum Arbeiten mit Bereichen finden Sie unter [Bereichsdefinition für den Zugriff auf Websitedesigns](site-design-scoping.md).

## <a name="see-also"></a>Siehe auch

- [Erste Schritte mit dem Erstellen von Websitedesigns](get-started-create-site-design.md)
- [Anwenden eines Bereichs auf Ihr Websitedesign](site-design-scoping.md)
- [JSON-Schema eines Websitedesigns](site-design-json-schema.md)
- [PowerShell-Cmdlets für SharePoint-Websitedesigns und -Websiteskripts](site-design-powershell.md)
- [REST-API von Websitedesigns und Websiteskripts](site-design-rest-api.md)
- [Beispiele für die Websitedesign]((https://github.com/SharePoint/sp-dev-site-scripts))
