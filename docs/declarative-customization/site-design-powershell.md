---
title: "PowerShell-Cmdlets für SharePoint-Websitedesigns und -Websiteskripts"
description: Verwenden Sie PowerShell-Cmdlets zum Erstellen, Abrufen und Entfernen von Websitedesigns und Websiteskripts.
ms.date: 12/14/2017
ms.openlocfilehash: d28a487c20970973cd11a26532068b54c095d939
ms.sourcegitcommit: 8e63066ad9591e51bbda419b1b9527452111081b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="powershell-cmdlets-for-sharepoint-site-designs-and-site-scripts"></a>PowerShell-Cmdlets für SharePoint-Websitedesigns und -Websiteskripts

> [!NOTE]
> Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden. Sie werden in Produktionsumgebungen derzeit nicht unterstützt.

Verwenden Sie PowerShell-Cmdlets zum Erstellen, Abrufen und Entfernen von Websitedesigns und Websiteskripts.

## <a name="getting-started"></a>Erste Schritte

Bevor Sie die PowerShell-Cmdlets ausführen können, müssen Sie Folgendes tun:

1. Sie müssen die [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunterladen und installieren. Ist auf Ihrem System bereits eine frühere Version der Shell installiert, müssen Sie diese Version deinstallieren und anschließend die neueste Version installieren.
1. Sie müssen eine Verbindung zu Ihrem SharePoint-Mandanten einrichten. Eine Anleitung finden Sie unter [Herstellen einer Verbindung mit SharePoint Online PowerShell]((https://technet.microsoft.com/de-DE/library/fp161372.aspx)).

Um die Einrichtung zu überprüfen, verwenden Sie das **Get-SPOSiteScript** zum Lesen der aktuellen Liste von Websiteskripts. Wenn das Cmdlet ausgeführt und ohne Fehler zurückgegeben wird, können Sie fortfahren.

## <a name="site-design-cmdlets"></a>Websitedesign-Cmdlets

Zur Verwaltung von Websitedesigns und Websiteskripts über die PowerShell stehen Ihnen die folgenden Cmdlets zur Verfügung:

- **Add-SPOSiteDesign**
- **Add-SPOSiteScript**
- **Get-SPOSiteDesign**
- **Get-SPOSiteDesignRights**
- **Get-SPOSiteScript**
- **Grant-SPOSiteDesignRights**
- **Remove-SPOSiteDesign**
- **Remove-SPOSiteScript**
- **Revoke-SPOSiteDesignRights**

<!--
- **Set-SPOSiteDesign**
- **Set-SPOSiteScript**
-->

<!-- TBD document pipe bind parameters -->

## <a name="add-spositedesign"></a>Add-SPOSiteDesign

Erstellen eines neues Websitedesigns, das für Benutzer beim Erstellen einer neuen Website von der SharePoint-Startseite verfügbar ist.

```powershell
Add-SPOSiteDesign
  -Title <string>
  -WebTemplate <string>
  -SiteScripts <SPOSiteScriptPipeBind[]>
  [-Description <string>]
  [-PreviewImageUrl <string>]
  [-PreviewImageAltText <string>]
  [-IsDefault]
  [<CommonParameters>]
```

### <a name="parameters"></a>Parameter

|Parameter  | Beschreibung  |
|-----------|--------------|
|-Title                 | Der Anzeigename des Websitedesigns. |
|-WebTemplate           | Identifiziert, zu welcher Basisvorlage das Design hinzugefügt werden soll. Verwenden Sie den Wert **64** für die Teamwebsite-Vorlage und den Wert **68** für die Kommunikationswebsitevorlage. |
|-SiteScripts           | Ein Array von einem oder mehreren Websiteskripts. Jedes wird durch eine ID identifziert. Die Skripts werden in der aufgeführten Reihenfolge ausgeführt. |
|[-Description]         | Die Anzeigebeschreibung des Websitedesigns. |
|[-PreviewImageUrl]     | Die URL eines Vorschaubilds. Wenn keine angegeben ist, verwendet SharePoint ein allgemeines Bild. |
|[-PreviewImageAltText] | Die Alternativtextbeschreibung des Bilds für Barrierefreiheit. |
|[-IsDefault]           | Eine Option, die das Websitedesign auf die Standardwebsitevorlage anwendet. <!-- For more information see [Applying a site design to a default SharePoint template](site-design-apply-default-template.md) --> |

Nachfolgend finden Sie ein Beispiel für das Erstellen eines neues Websitedesigns.

```powershell
C:\> Add-SPOSiteDesign `
  -Title "Contoso customer tracking" `
  -WebTemplate "64" `
  -SiteScripts "<ID>" `
  -Description "Tracks key customer data in a list" `
  -PreviewImageUrl "https://contoso.sharepoint.com/SiteAssets/site-preview.png" `
  -PreviewImageAltText "site preview" `
  -IsDefault $false
```

## <a name="add-spositescript"></a>**Add-SPOSiteScript**

Lädt ein neues Websiteskript in den Katalog hoch, das entweder direkt oder in einem Websitedesign verwendet werden kann. Dieses Cmdlet unterstützt die Inline-Skriptdatei.

```powershell
Add-SPOSiteScript
  -Title <string>
  -Content <string>
  [-Description <string>]
  [<CommonParameters>]
```

### <a name="parameters"></a>Parameter

|Parameter     | Beschreibung  |
|--------------|--------------|
| -Title       | Der Anzeigename des Websitedesigns. |
| -Content     | JSON-Wert, der das Skript beschreibt. Weitere Informationen finden Sie unter [JSON-Referenz](site-design-json-schema.md).|
| -Description | Eine Beschreibung des Skripts. |

Nachfolgend finden Sie ein Beispiel für das Hinzufügen einer neuen Website aus dem folgenden Skript zu einer Datei.

```json
{
  "verb": "setSiteLogo",
  "url": "https://contoso.sharepoint.com/SiteAssets/company-logo.png"
},
```

```powershell
C:\> Get-Content 'c:\scripts\site-script.json' -Raw | Add-SPOSiteScript -Title "Customer logo" -Description "Applies customer logo for customer sites"
```

## <a name="get-spositedesign"></a>Get-SPOSiteDesign

Ruft Details zu Websitedesigns ab, die sich im SharePoint-Mandanten befinden. Sie können eine ID eines bestimmten Websitedesigns angeben, das abgerufen werden soll. Wenn keine Parameter aufgeführt werden, werden Details zu allen Websitedesigns aufgeführt.

```powershell
Get-SPOSiteDesign
  [[-Identity] <SPOSiteDesignPipeBind>]
  [<CommonParameters>]
```

### <a name="parameters"></a>Parameter

|Parameter     | Beschreibung  |
|--------------|--------------|
| [-Identity]  | Die ID des abzurufenden Websitedesigns. |

Nachfolgend finden Sie ein Beispiel und eine Beispielantwort für das Abrufen von Websitedesigndetails.

```powershell
PS C:\> Get-SPOSiteDesign 44252d09-62c4-4913-9eb0-a2a8b8d7f863
```

```
Id                  : 44252d09-62c4-4913-9eb0-a2a8b8d7f863
Title               : Contoso - Team Project
WebTemplate         : 64
SiteScriptIds       : {1306913c-8463-42ca-bd63-efad0fcdbba4}
Description         : Use this design to apply Contoso theme and create
                      custom lists and add to nav
```

## <a name="get-spositedesignrights"></a>Get-SPOSiteDesignRights

Zeigt eine Liste von Prinzipalen und deren Berechtigungen zur Verwendung des Websitedesigns an. Dies kann verwendet werden, um den Bereich zu ermitteln, den Ihr Websitedesign mit Benutzern in dem Mandanten aufweist.

```powershell
Get-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a>Parameter

|Parameter     | Beschreibung  |
|--------------|--------------|
| [-Identity]  | Die ID des Websitedesigns zum Abrufen von Bereichsinformationen. |

Nachfolgend finden Sie ein Beispiel zum Abrufen der Berechtigungen für ein Websitedesign.

```powershell
PS C:\> Get-SPOSiteDesignRights 607aed52-6d61-490a-b692-c0f58a6981a1
```

```
DisplayName  PrincipalName                                      Rights
-----------  -------------                                      ------
Nestor Wilke i:0#.f|membership|nestorw@contoso.sharepoint.com   View
```

## <a name="get-spositescript"></a>Get-SPOSiteScript

Zeigt Informationen zu vorhandenen Websiteskripts an. Wenn kein Parameter bereitgestellt wird, gibt dieses Cmdlet **Id**, **Title**, **Description** und **Version** jedes Websiteskripts an. Wenn eine Websiteskript-ID bereitgestellt wird, gibt dieses Cmdlet auch **Content** an, wobei es sich um den JSON-Code des Websiteskripts handelt.

```powershell
Get-SPOSiteScript
  [[-Identity] <SPOSiteScriptPipeBind>]
  [<CommonParameters>]
```

### <a name="parameters"></a>Parameter

|Parameter     | Beschreibung  |
|--------------|--------------|
| [-Identity]  | Die ID des Websiteskripts, über das Informationen abgerufen werden sollen. |

## <a name="grant-spositedesignrights"></a>Grant-SPOSiteDesignRights

Wird zum Anwenden von Berechtigungen auf einen Satz von Benutzern oder eine Sicherheitsgruppe verwendet, wodurch die Sichtbarkeit des Websitedesigns in der UX effektiv festgelegt wird. Diese beginnen öffentlich. Nachdem Sie jedoch Berechtigungen festgelegt haben, können nur diese Gruppen oder Benutzer auf das Websitedesign zugreifen.

```powershell
Grant-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  -Principals <string[]>
  -Rights {View}
  [<CommonParameters>]
```

### <a name="parameters"></a>Parameter

|Parameter     | Beschreibung  |
|--------------|--------------|
| [-Identity]  | Die ID des Websitedesigns zum Abrufen von Bereichsinformationen. |
| -Principals  | Eine oder mehrere Prinzipale, für die Berechtigungen hinzugefügt werden sollen. |
| -Rights      | Ist immer auf den Wert **View** festgelegt. Alle Benutzer oder Gruppen mit Anzeigeberechtigungen können das Websitedesign anzeigen und verwenden. |

Nachfolgend finden Sie ein Beispiel, wie Anzeigeberechtigungen für ein Websitedesign für einen Nestor (ein Benutzer auf der fiktiven Contoso-Website) erteilt werden.

```powershell
PS C:\> Grant-SPOSiteDesignRights `
         -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
         -Principals "nestorw@contoso.sharepoint.com" `
         -Rights View
```

## <a name="remove-spositedesign"></a>Remove-SPOSiteDesign

Entfernt ein Websitedesign. Dieses wird nicht mehr in der Benutzeroberfläche zum Erstellen einer neuen Website angezeigt.

```powershell
  Remove-SPOSiteDesign
  [-Identity] <SPOSiteDesignPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a>Parameter

|Parameter     | Beschreibung  |
|--------------|--------------|
| [-Identity]  | Die ID des zu entfernenden Websitedesigns. |

## <a name="remove-spositescript"></a>Remove-SPOSiteScript

Entfernt ein Websiteskripts. <!-- TBD how is dependency problem handled so you don't delete a script that a design depends on. this currently creates an error when running the design.) -->

```powershell
Remove-SPOSiteScript
  [-Identity] <SPOSiteScriptPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a>Parameter

|Parameter     | Beschreibung  |
|--------------|--------------|
| [-Identity]  | Die ID des zu entfernenden Websiteskripts. |

## <a name="revoke-spositedesignrights"></a>Revoke-SPOSiteDesignRights

Widerruft Berechtigungen für angegebene Prinzipale aus einem Websitedesign.

```powershell
Revoke-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  -Principals <string[]>
  [<CommonParameters>]
```

### <a name="parameters"></a>Parameter

|Parameter     | Beschreibung  |
|--------------|--------------|
| [-Identity]  | Die ID des Websitedesigns, aus dem Berechtigungen widerrufen werden sollen. |
| -Principals  | Mindestens ein Prinzipal zum Widerrufen von Berechtigungen im angegebenen Websitedesign. |

<!--
## Set-SPOSiteDesign (TBD)

## Set-SPOSiteScript (TBD)
-->

Entwickler können zur Verwaltung von Designs außerdem die [REST-API](site-design-rest-api.md) verwenden.

Informationen zur Definition und Speicherung von Designs finden Sie in der [JSON-Schemareferenz](site-design-json-schema.md).