---
title: "Anpassen der standardmäßigen Websitedesigns in SharePoint"
description: "Anpassen der standardmäßigen Websitedesigns auf der SharePoint-Teamwebsite oder auf der Kommunikations-Websitevorlage"
ms.date: 12/18/2017
ms.openlocfilehash: 34107e7028400cec62b0f6454f3474b92ca288be
ms.sourcegitcommit: 9f492519d4eeb3f62a1fddc71cdca79263651a56
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="customize-a-default-site-design"></a>Anpassen eines standardmäßigen Websitedesigns

> [!NOTE]
> Websitedesigns und Websiteskripts befinden sich in der Vorschau und können ohne vorherige Ankündigung geändert werden. Sie werden derzeit nur für Produktionsumgebungen im Zielrelease unterstützt.

SharePoint enthält zahlreiche Websitedesigns, die bereits in den SharePoint Online-Websitevorlagen verfügbar sind. Dies sind die standardmäßigen Websitedesigns. Sie können diese mit PowerShell oder den REST-APIs so ändern, dass sie die gesamte Websitebereitstellung steuern. Sie können zum Beispiel sicherstellen, dass das Unternehmensdesign auf jede Website angewendet wird, die erstellt wird. Sie können auch sicherstellen, dass ein Protokollierungsmechanismus immer ausgeführt wird, unabhängig davon, welcher Websitedesign ausgewählt wird.

## <a name="apply-a-site-design-to-the-default-site-designs"></a>Anwenden eines Websitedesigns auf die standardmäßigen Websitedesigns

Um die standardmäßigen Websitedesigns anzupassen, wenden Sie ein neues Design mit dem Powershell-Cmdlet **Add-SPOSiteDesign** oder der REST-API **CreateSiteDesign**. Geben Sie die Option **IsDefault** an, damit das Websitedesign standardmäßig angewendet wird.

Das folgende Beispiel zeigt, wie Sie mithilfe der **IsDefault**-Option das Contoso-Unternehmensdesign auf die standardmäßigen Websitedesigns anwenden. Das Website-Skript, auf das durch die ID verwiesen wird, enthält das JSON-Skript zum Anwenden des richtigen Designs.

```powershell
C:\> Add-SPOSiteDesign `
  -Title "Contoso company theme" `
  -WebTemplate "68" `
  -SiteScripts "89516c6d-9f4d-4a57-ae79-36b0c95a817b" `
  -Description "Applies standard company theme to site" `
  -IsDefault
```
```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteDesign", {info:{Title:"Contoso company theme", Description:"Applies standard company theme to site", SiteScriptIds:["89516c6d-9f4d-4a57-ae79-36b0c95a817b"],  WebTemplate:"68", IsDefault: true}});
```

## <a name="which-default-site-designs-are-updated"></a>Welche standardmäßigen Websitedesigns werden aktualisiert?

Im vorherigen Beispiel verweist der **WebTemplate**-Wert 68 auf die Websitevorlage für SharePoint Online-Kommunikation. Diese Vorlage enthält die folgenden standardmäßigen Websitedesigns:

- Thema
- Showcase
- Leer

Wenn Sie ein neues Websitedesign anwenden, werden alle drei der standardmäßigen Websitedesigns aktualisiert.

Die Vorlage für SharePoint Online-Teamwebsite enthält nur das standardmäßige Websitedesign mit dem Namen **Team**. In diesem Fall wird beim Anwenden eines standardmäßigen Websitedesigns nur das Websitedesign mit dem Namen **Team** aktualisiert.

## <a name="restoring-the-default-site-designs"></a>Wiederherstellen standardmäßiger Websitedesigns

Entfernen Sie das angewendete Websitedesign, um ein Websitedesign auf die Standardeinstellungen zurückzusetzen. Wenn Sie im vorherigen Beispiel das Websitedesign mit der ID db752673-18fd-44db-865a-aa3e0b28698e erstellt haben, würden Sie es entfernen, wie im folgenden Beispiel gezeigt.

```powershell
C:\> Remove-SPOSiteDesign db752673-18fd-44db-865a-aa3e0b28698e
```
```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteDesign", {id:"db752673-18fd-44db-865a-aa3e0b28698e"});
```

> [!NOTE]
> Wenn Sie nicht sicher sind, welche Websitedesigns die Standardeinstellung sind, führen Sie das Cmdlet **Get-SPOSiteDesign** aus. Damit werden alle Websitedesigns aufgeführt und es wird angegeben, welche die standardmäßigen sind.
