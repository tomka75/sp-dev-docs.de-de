---
title: Erste Schritte mit dem Erstellen von SharePoint-Websitedesigns und -Websiteskripts
description: Erste Schritte mit dem Erstellen von SharePoint-Websitedesigns und -Websiteskripts, aus denen Benutzer ihre eigenen Websites erstellen.
ms.date: 12/14/2017
ms.openlocfilehash: eddc4455695e014899b268456ee501e956639b98
ms.sourcegitcommit: db303a21b5f83c8c2f9c2028a271c9aae0ac0515
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/07/2018
---
# <a name="get-started-creating-site-designs-and-site-scripts"></a>Erste Schritte mit dem Erstellen von Websitedesigns und Websiteskripts

> [!NOTE]
> Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden. Sie werden in Produktionsumgebungen derzeit nicht unterstützt.

Erstellen Sie Websitedesigns, um wiederverwendbare Listen, Designs, Layouts, Seiten oder benutzerdefinierte Aktionen bereitzustellen, damit Ihre Benutzer schnell neue SharePoint-Websites mit den benötigten Features erstellen können. In diesem Artikel erstellen Sie ein einfaches Websitedesign, das eine SharePoint-Liste zum Nachverfolgen von Kundenbestellungen hinzufügt. Sie verwenden dann das Websitedesign, um eine neue SharePoint-Website mit der benutzerdefinierten Liste zu erstellen.

In diesem Artikel wird gezeigt, wie Sie PowerShell-Cmdlets in SharePoint zum Erstellen von Websiteskripts und Websitedesigns verwenden. Sie können auch REST-API für dieselben Aktionen verwenden. Die entsprechenden REST-Aufrufe sind zur Referenz in jedem Schritt dargestellt.

## <a name="create-the-site-script-in-json"></a>Erstellen des Websiteskripts in JSON

Ein Websitedesign ist eine Sammlung von Aktionen, die SharePoint beim Erstellen einer neuen Website ausführt. Aktionen beschreiben Änderungen, die auf die neue Website angewendet werden sollen, z. B. das Erstellen einer neuen Liste oder das Anwenden eines Designs. Die Aktionen werden in einem JSON-Skript angegeben. Das JSON-Skript ist eine Liste aller anzuwendenden Aktionen. Wenn ein Skript ausgeführt wird, schließt SharePoint jede Aktion in der aufgeführten Reihenfolge ab.

Jede Aktion wird vom Wert „verb“ im JSON-Skript angegeben. Aktionen können auch Unteraktionen aufweisen, die auch „verb“-Werte sind. Im folgenden JSON-Code gibt das Skript an, dass eine neue Liste mit dem Namen „Kundenverfolgung“ erstellt werden sollen; Unteraktionen legen dann die Beschreibung fest und fügen mehrere Felder zum Definieren der Liste hinzu.

1. Sie müssen die [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunterladen und installieren. Ist auf Ihrem System bereits eine frühere Version der Shell installiert, müssen Sie diese Version deinstallieren und anschließend die neueste Version installieren.
1. Sie müssen eine Verbindung zu Ihrem SharePoint-Mandanten einrichten. Eine Anleitung finden Sie unter [Herstellen einer Verbindung mit SharePoint Online PowerShell](https://technet.microsoft.com/de-DE/library/fp161372.aspx).
1. Weisen Sie den JSON-Code, der das neue Skript beschreibt, einer Variablen zu, wie im folgenden PowerShell-Code dargestellt.

 ```powershell
$site_script = @'
{
    "$schema": "schema.json",
        "actions": [
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
'@
```

Das vorherige Skript erstellt eine neue SharePoint-Liste mit dem Namen „Kundenverfolgung“. Es legt die Beschreibung fest und fügt der Liste auch vier weitere Felder hinzu. Beachten Sie, dass jedes dieser Felder als eine Aktion betrachtet wird. Websiteskripts sind auf 30 kumulierte Aktionen beschränkt (über ein oder mehrere Skripts, die in einem Websitedesign aufgerufen werden können).

## <a name="add-the-site-script"></a>Hinzufügen des Websiteskripts

Jedes Websiteskript muss in SharePoint registriert werden, damit es verfügbar ist. Fügen Sie ein neues Websitedesign mithilfe des Cmdlets **Add-SPOSiteScript** hinzu. Im folgenden Beispiel wird gezeigt, wie das zuvor beschriebene JSON-Skript hinzugefügt wird. 

```powershell
C:\> Add-SPOSiteScript -Title "Create customer tracking list" -Content $site_script -Description "Creates list for tracking customer contact information"
```

Nach dem Ausführen des Cmdlets erhalten Sie ein Ergebnis, in dem die Websiteskript-**ID** des hinzugefügten Skripts aufgeführt wird. Notieren Sie sich diese ID, denn Sie werden sie später benötigen, wenn Sie das Websitedesign erstellen.

Die REST-API, die dem neuen Websiteskript hinzugefügt wird, ist **CreateSiteScript**.

## <a name="create-the-site-design"></a>Erstellen des Websitedesigns

Als Nächstes müssen Sie das Websitedesign erstellen. Das Websitedesign wird in einer Dropdownliste angezeigt, wenn jemand eine neue Website aus einer der Vorlagen erstellt. Es kann ein oder mehrere Websiteskripts ausführen, die bereits hinzugefügt wurden.

- Führen Sie das folgende Cmdlet aus, um ein neues Websitedesign hinzuzufügen. Ersetzen Sie \<ID\> durch die Websiteskript-ID beim Hinzufügen des Websiteskripts.

```powershell
C:\> Add-SPOSiteDesign -Title "Contoso customer tracking" -WebTemplate "64" -SiteScripts "<ID>" -Description "Tracks key customer data in a list"
```

Das vorherige Cmdlet erstellt ein neues Websitedesign mit dem Namen „Contoso-Kundenverfolgung“. Durch den Wert „-WebTemplate“ wird ausgewählt, welche Basisvorlage verwendet werden soll. Der Wert „64“ gibt die Teamwebsite-Vorlage an, der Wert „68“ gibt die Kommunikationswebsitevorlage an.

In der JSON-Antwort wird die **ID** des neuen Websitedesigns angezeigt. Sie können diese in nachfolgenden Cmdlets verwenden, um das Websitedesign zu aktualisieren oder zu ändern.

Die REST-API, die dem neuen Websiteskript hinzugefügt wird, ist **CreateSiteDesign**.

## <a name="use-the-new-site-design"></a>Verwenden des neuen Websitedesigns

Da Sie nun ein Websiteskript und ein Websitedesign hinzugefügt haben, können Sie diese zum Erstellen neuer Websites verwenden.

1. Gehen Sie zur Startseite der SharePoint-Website, die Sie für die Entwicklung verwenden.
1. Wählen Sie **Website erstellen** aus.
1. Wählen Sie **Teamwebsite** aus.
1. Wählen Sie in der Dropdownliste **Design auswählen** Ihr Websitedesign **Kundenbestellungen** aus.
1. Geben Sie unter „Websitename“ einen Namen für die neue Website **Kundenauftragsverfolgung** ein.
1. Wählen Sie **Weiter** aus.
1. Wählen Sie **Fertig stellen** aus.
1. In einem Bereich wird angegeben, dass Ihr Skript angewendet wird. Wenn dieser Vorgang abgeschlossen ist, wählen Sie **Aktualisierte Website anzeigen**.
1. Die benutzerdefinierte Liste wird auf der Seite angezeigt.
