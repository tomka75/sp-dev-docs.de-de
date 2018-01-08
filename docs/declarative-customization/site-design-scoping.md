---
title: "Bereichsdefinition für den Zugriff auf SharePoint-Websitedesigns"
description: "Legen Sie den Bereich für SharePoint-Websitedesigns fest, um zu steuern, wer diese anzeigen und darauf zugreifen kann."
ms.date: 12/14/2017
ms.openlocfilehash: d6181e92cd76af2e16e847219bb7aaa129ddebb7
ms.sourcegitcommit: 8e63066ad9591e51bbda419b1b9527452111081b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="scoping-access-to-site-designs"></a>Bereichsdefinition für den Zugriff auf Websitedesigns

> [!NOTE]
> Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden. Sie werden in Produktionsumgebungen derzeit nicht unterstützt.

Websitedesigns stehen standardmäßig für alle Personen zur Verfügung. Sie können den Bereich von Websitedesigns jedoch so festlegen, dass diese nur für bestimmte Benutzer oder Gruppen verfügbar sind. Die Buchhaltungsabteilung verfügt beispielsweise über spezielle Websitedesigns, es macht aber vielleicht keinen Sinn, diese Websitedesigns für alle Personen freizugeben. In diesem Artikel wird erläutert, wie Sie steuern können, welche Benutzer und Gruppen bestimmte Websitedesigns anzeigen können.

## <a name="granting-rights-to-a-site-design"></a>Erteilen von Berechtigungen für ein Websitedesign

Bei der Erstellung eines Websitedesigns ist dieses zunächst für alle Personen verfügbar. Sie können **View**-Berechtigungen für das Websitedesign erteilen. Nachdem Berechtigungen erteilt wurden, haben nur die angegebenen Benutzer oder Gruppen (Prinzipale) Zugriff. Mit nachfolgenden API-Aufrufen können Sie weiteren Prinzipalen Berechtigungen erteilen.

## <a name="granting-rights-to-security-groups"></a>Erteilen von Berechtigungen für Sicherheitsgruppen

Nachfolgend finden Sie ein Beispiel, wie der Bereich eines vorhandenen Websitedesigns so festgelegt wird, dass nur die E-Mail-aktivierte Sicherheitsgruppe **Buchhaltung** das Websitedesign anzeigen und dieses verwenden kann.

```powershell
Grant-SPOSiteDesignRights `
  -Identity db752673-18fd-44db-865a-aa3e0b28698e `
  -Principals ("accounting@contoso.sharepoint.com") `
  -Rights View
```

Vielleicht möchten Sie ein neues Websitedesign erstellen und gleichzeitig Berechtigungen erteilen, wie im nächsten Beispiel dargestellt.

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

Nachfolgend finden Sie ein Beispiel, wie Anzeigeberechtigungen für ein Websitedesign für einen Nestor (ein Benutzer auf der fiktiven Contoso-Website) erteilt werden.

```powershell
PS C:\> Grant-SPOSiteDesignRights `
         -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
         -Principals "nestorw@contoso.sharepoint.com" `
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
Nestor Wilke i:0#.f|membership|nestorw@contoso.sharepoint.com   View
```

## <a name="revoking-rights-from-a-site-design"></a>Widerrufen von Berechtigungen von einem Websitedesign

Sie können Berechtigungen für alle Prinzipale widerrufen. Wenn Sie Berechtigungen für alle Prinzipale widerrufen, steht das Websitedesign wieder für alle Personen zur Verfügung.

Nachfolgend finden Sie ein Beispiel dafür, wie der Zugriff für die E-Mail-aktivierte Sicherheitsgruppe „Buchhaltung“ und den Nestor widerrufen wird.

```powershell
Revoke-SPOSiteDesignRights `
  -Identity db752673-18fd-44db-865a-aa3e0b28698e `
  -Principals ("accounting@contoso.sharepoint.com","nestorw@spdfcontosodemo2.onmicrosoft.com") `
```
