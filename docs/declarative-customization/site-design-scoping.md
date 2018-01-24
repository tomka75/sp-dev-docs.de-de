---
title: "Bereichsdefinition für den Zugriff auf SharePoint-Websitedesigns"
description: "Legen Sie den Bereich für SharePoint-Websitedesigns fest, um zu steuern, wer diese anzeigen und darauf zugreifen kann."
ms.date: 12/14/2017
ms.openlocfilehash: c0896cab28a4c9cba3f74fbad8120061311004a2
ms.sourcegitcommit: d9372f6009de1c1e48e272fd3629a99aed7fef9f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="scoping-access-to-site-designs"></a>Bereichsdefinition für den Zugriff auf Websitedesigns

> [!NOTE]
> Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden. Sie werden in Produktionsumgebungen derzeit nicht unterstützt.

Websitedesigns stehen standardmäßig allen Benutzern zur Verfügung. Sie können den Bereich von Websitedesigns jedoch so festlegen, dass diese nur für bestimmte Benutzer oder Gruppen verfügbar sind. Die Buchhaltungsabteilung verfügt beispielsweise über spezielle Websitedesigns, es macht aber vielleicht keinen Sinn, diese Websitedesigns für alle Personen freizugeben. In diesem Artikel wird erläutert, wie Sie steuern können, welche Benutzer und Gruppen bestimmte Websitedesigns anzeigen können.

## <a name="granting-rights-to-a-site-design"></a>Erteilen von Berechtigungen für ein Websitedesign

Bei der Erstellung eines Websitedesigns ist dieses zunächst für alle Benutzer verfügbar. Sie können Berechtigungen des Typs **Anzeigen** für das Websitedesign erteilen. Sobald Berechtigungen erteilt wurden, haben nur die angegebenen Benutzer oder Gruppen (Prinzipale) Zugriff. Mit nachfolgenden API-Aufrufen können Sie weiteren Prinzipalen Berechtigungen erteilen.

## <a name="granting-rights-to-security-groups"></a>Erteilen von Berechtigungen für Sicherheitsgruppen

Nachfolgend finden Sie ein Beispiel, wie der Bereich eines vorhandenen Websitedesigns so festgelegt werden kann, dass nur die E-Mail-aktivierte Sicherheitsgruppe **accounting** das Websitedesign anzeigen und verwenden kann.

```powershell
Grant-SPOSiteDesignRights `
  -Identity db752673-18fd-44db-865a-aa3e0b28698e `
  -Principals ("accounting@contoso.sharepoint.com") `
  -Rights View
```

Vielleicht möchten Sie Berechtigungen auch direkt bei der Erstellung eines Websitedesigns erteilen. Das funktioniert wie in diesem Beispiel demonstriert:

```powershell
Add-SPOSiteDesign `
  -Title "Scoped site design" `
  -Description "Scoped to only the accounting email security group" `
  -SiteScripts 256494cb-bd31-4f60-9eba-285308d7a863 `
  -WebTemplate 64 `
  -PreviewImageUrl "https://contoso.sharepoint.com/SiteAssets/scope-image.png" `
| Grant-SPOSiteDesignRights `
  -Principals ("accounting@contoso.com") `
  -Rights View
```

## <a name="granting-rights-to-users"></a>Erteilen von Berechtigungen für Benutzer

Im folgenden Beispiel wird gezeigt, wie Sie einem Benutzer (Nestor) auf der fiktiven Contoso-Website Anzeigeberechtigungen für ein Websitedesign erteilen können.

```powershell
PS C:\> Grant-SPOSiteDesignRights `
         -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
         -Principals "nestorw@contoso.onmicrosoft.com" `
         -Rights View
```

## <a name="viewing-rights-assigned-to-a-site-design"></a>Anzeigeberechtigungen, die einem Websitedesign zugewiesen sind

Verwenden Sie zum Anzeigen von Berechtigungen das Cmdlet **Get-SPOSiteDesignRights**. Im folgenden Beispiel wird gezeigt, wie dieses Cmdlet und eine Antwort verwendet wird, wenn nur der Nestor über Anzeigeberechtigungen verfügt.

```powershell
PS C:\> Get-SPOSiteDesignRights 607aed52-6d61-490a-b692-c0f58a6981a1
```

```
DisplayName  PrincipalName                                      Rights
-----------  -------------                                      ------
Nestor Wilke i:0#.f|membership|nestorw@contoso.onmicrosoft.com   View
```

## <a name="revoking-rights-from-a-site-design"></a>Widerrufen von Berechtigungen von einem Websitedesign

Sie können die Berechtigungen jedes Prinzipals jederzeit widerrufen. Wenn Sie die Anzeigeberechtigungen für alle Prinzipale widerrufen, steht das Websitedesign wieder für alle Benutzer zur Verfügung.

Nachfolgend finden Sie ein Beispiel dafür, wie sich die Zugriffsberechtigungen der E-Mail-aktivierten Sicherheitsgruppe „accounting“ und des Benutzers „Nestor“ widerrufen lassen.

```powershell
Revoke-SPOSiteDesignRights `
  -Identity db752673-18fd-44db-865a-aa3e0b28698e `
  -Principals ("accounting@contoso.sharepoint.com","nestorw@spdfcontosodemo2.onmicrosoft.com") `
```
