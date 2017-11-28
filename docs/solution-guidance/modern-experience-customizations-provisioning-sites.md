---
title: Bereitstellen von "modernen" Teamwebsites programmgesteuert
description: "Bereitstellen einer Teamwebsite über die Benutzeroberfläche oder mit Plug & Play-CSOM Core oder Plug & Play-PowerShell."
ms.date: 11/08/2017
ms.openlocfilehash: 65b9637167045b4fa92728ab3266c336fdfe6ad2
ms.sourcegitcommit: 4ea7e9cb1efb53f89da236282002956739d77418
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="provisioning-modern-team-sites-programmatically"></a>Bereitstellen von "modernen" Teamwebsites programmgesteuert

"Modernen" Teamwebsites in SharePoint Online in 2016 eingeführt wurden, und verwenden sie die Option auf der Ebene der Mandant gesteuert werden kann. In diesem Artikel werden die verschiedenen Optionen und Aspekte für die Bereitstellung von "modernen" Teamwebsites in SharePoint Online.

> [!IMPORTANT]
> Wir sind nicht die "klassische" Erfahrung veralteter; "klassische" und "modernen" werden gleichzeitig verwendet werden.

## <a name="provisioning-a-modern-team-site-from-the-user-interface"></a>Bereitstellung einer "modernen" Teamwebsite aus der Benutzeroberfläche

Es gibt zahlreiche Routen für eine "modernen" Teamwebsite bereitgestellt erhalten möchten. Sie können die Bereitstellung direkt über die SharePoint Online-Website starten, oder Sie können alternativ bereitstellen eine Office 365-Gruppe aus anderen Speicherorten (z. B. von Outlook), die auch dann löst die Bereitstellung einer "modernen" Team Site. 

- Wenn Ihr Administrator "modernen" Teamwebsites in Ihrem Mandanten aktiviert, können Sie der Homepage der SharePoint "modernen" Teamwebsites erstellen.

- Sie können auch eine Office 365-Gruppe von Office 365 Outlook erstellen, und wenn Sie auf die Registerkarte Standort der Gruppe zugreifen, sorgt auf einer Teamwebsite "modernen". 

### <a name="control-default-provisioning-flow"></a>Steuerelement-Standard Flow-Bereitstellung

Sie können die SharePoint-Website Erstellungsprozess SharePoint Online Admin Einstellungen steuern. Sie können auswählen, wenn die Erfahrung "moderne" für die Endbenutzer verfügbar ist oder wenn Sie fortfahren möchten, verwenden die "klassische" Erfahrung. Weitere Informationen hierzu finden Sie unter [Manage Site Creation in SharePoint Online](https://support.office.com/en-US/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9).

*Abbildung 1. Optionen zum Erstellen einer Website von SharePoint Online*

![Optionen zum Erstellen einer Website aus der SharePoint Online-Admin-Benutzeroberfläche](media/modern-experiences/site-creation-options-admin-ui.png)


## <a name="provisioning-a-modern-team-site-programmatically"></a>Bereitstellung einer Teamwebsite "modernen" programmgesteuert

"Modernen" Teamwebsites werden programmgesteuert durch Erstellen einer [Gruppe von Office 365](https://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/group) mit Microsoft Graph erstellt. Wenn Sie eine Office 365-Gruppe erstellen, wird automatisch eine Teamwebsite "modernen" für die Gruppe bereitgestellt. Die "modernen" Teamwebsite URI basiert auf dem **MailNickname** -Parameter der Gruppe der Office 365 und verfügt über die folgenden standardmäßigen Struktur. 

```
https://[tenant].sharepoint.com/sites/[mailNickname]]
``` 

> [!NOTE]
> Eine ausführliche Beschreibung der Erstellung von Gruppen mithilfe von Microsoft Graph ist von der [offizielle Dokumentation](https://graph.microsoft.io/en-us/docs/api-reference/v1.0/api/group_post_groups)zur Verfügung.

### <a name="provision-a-modern-team-site-using-the-pnp-csom-core-component"></a>Bereitstellen einer "modernen" Teamwebsite mithilfe der Plug & Play-CSOM-Core-Komponente

Die Plug & Play-CSOM-Core-Komponente als [NuGet-Paket](https://www.nuget.org/packages/SharePointPnPCoreOnline)wurde Methoden für den Umgang mit "modernen" Gruppe vereinfacht. 

```C#
/// <summary>
/// Let's use the UnifiedGroupsUtility class from PnP CSOM Core to simplify managed code operations for Office 365 groups
/// </summary>
/// <param name="accessToken">Azure AD Access token with Group.ReadWrite.All permission</param>
public static void ManipulateModernTeamSite(string accessToken)
{
    // Create new modern team site at the url https://[tenant].sharepoint.com/sites/mymodernteamsite
    Stream groupLogoStream = new FileStream("C:\\groupassets\\logo-original.png", 
                                            FileMode.Open, FileAccess.Read);
    var group = UnifiedGroupsUtility.CreateUnifiedGroup("displayName", "description", 
                            "mymodernteamsite", accessToken, groupLogo: groupLogoStream);
            
    // We received a group entity containing information about the group
    string url = group.SiteUrl;
    string groupId = group.GroupId;

    // Get group based on groupID
    var group2 = UnifiedGroupsUtility.GetUnifiedGroup(groupId, accessToken);
    // Get SharePoint site URL from group id
    var siteUrl = UnifiedGroupsUtility.GetUnifiedGroupSiteUrl(groupId, accessToken);

    // Get all groups in the tenant
    List<UnifiedGroupEntity> groups = UnifiedGroupsUtility.ListUnifiedGroups(accessToken);

    // Update description and group logo programatically
    groupLogoStream = new FileStream("C:\\groupassets\\logo-new.png", FileMode.Open, FileAccess.Read);
    UnifiedGroupsUtility.UpdateUnifiedGroup(groupId, accessToken, description: "Updated description", 
                                            groupLogo: groupLogoStream);

    // Delete group programatically
    UnifiedGroupsUtility.DeleteUnifiedGroup(groupId, accessToken);
}
```

### <a name="provision-a-modern-team-site-using-pnp-powershell"></a>Bereitstellen einer "modernen" Teamwebsite von Plug & Play-PowerShell

Sie können auch "modernen" Websites erstellen, mithilfe von [Plug & Play-PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases), dem Sie die Authentifizierung auf einfache Weise mit Microsoft Graph mithilfe von Azure Active Directory können. Das folgende Skript erstellt eine "modernen" Teamwebsite und gibt dann den aktuellen SharePoint-Website-URL zur weiteren Bearbeitung zurück. Nachdem Sie den Zugriff auf die URL der Website erstellt haben, können Sie CSOM (mit SharePoint Plug & Play-Hauptkomponenten) oder Plug & Play-PowerShell für SharePoint verwenden, um anderer Vorgänge auf der erstellten Website zu automatisieren.

```PowerShell
# Connect to Azure AD and get back an OAuth 2.0 Access Token
# This command will prompt the sign-in UI to authenticate
Connect-PnPMicrosoftGraph -Scopes "Group.ReadWrite.All","User.Read.All"

# Store the Access Token in a local variable
# This is not really needed for next steps, but is available
$accessToken = Get-PnPAccessToken

# Create a new Office 365 Unified Group, together with the corresponding Modern Site in SPO
$group = New-PnPUnifiedGroup -DisplayName "Awesome Group" -Description "Awesome Group" `
         -MailNickname "awesome-group" -Members "admin@contoso.onmicrosoft.com", "dan@contoso.onmicrosoft.com" `
         -IsPrivate -GroupLogoPath .\logo.jpg

# Connect to the modern site using PnP PowerShell SP cmdlets
# Since we are connecting now to SP side, credentials will be asked
Connect-PnPOnline $group.SiteUrl 

# Now we have access on the SharePoint site for any operations
$context = Get-PnPContext
$web = Get-PnPWeb
$context.Load($web, $web.WebTemplate)
Execute-PnPQuery
$web.WebTemplate + "#" + $web.Configuration
```

> [!NOTE]
> Derzeit wird nicht unterstützt "modernen" Teamwebsites mithilfe der [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588)bereit.

## <a name="additional-considerations"></a>Zusätzliche Überlegungen

### <a name="subsites-use-classic-templates"></a>Unterwebsites verwenden "klassische" Websitevorlagen

Wenn Sie eine Unterwebsite unter der Stammwebsite einer Websitesammlung "modernen" bereitstellen, werden Unterwebsites "klassische" Vorlagen verwendet. Derzeit sind keine "modernen" Unterwebsitevorlagen verfügbar. Eine Unterwebsite "klassische" für eine "modernen" Teamwebsite können von einer Seite "modernen" auf der Website erstellen und Aktualisieren der Seite Willkommen auf der neu erstellten Seite transformiert werden.  

### <a name="sites-are-not-listed-in-the-sharepoint-admin-ui--tenant-api"></a>Websites werden nicht aufgeführt, in der SharePoint-Admin-Benutzeroberfläche / Mandanten-API

"Modernen" Teamwebsites werden nicht in der SharePoint-Admin-Benutzeroberfläche angezeigt. Sie können die Liste der "modernen" Teamwebsites von der Benutzeroberfläche von Office 365 Gruppen Admin unter der Office 365-Verwaltungsportals zugreifen. Die SharePoint Online-Admin-Benutzeroberfläche sind nur "klassische" SharePoint-Websites aufgeführt. Dieselbe Einschränkung gilt nicht für den Mandanten API; Diese API können zusammen mit "klassische" Teamwebsites "modernen" Teamwebsites aufgelistet werden. Um eine Liste der nur "modernen" Teamwebsites zu erhalten, können Sie die Gruppen-Endpunkt aus der Microsoft Graph-API verwenden.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [Anpassen der „modernen“ Benutzeroberflächen in SharePoint Online](modern-experience-customizations.md)
- [Was ist eine SharePoint-Teamwebsite?](https://support.office.com/en-US/article/What-is-a-SharePoint-team-site-75545757-36c3-46a7-beed-0aaa74f0401e?ui=en-US&rs=en-US&ad=US)
- [Erstellen einer Teamwebsite in SharePoint Online](https://support.office.com/en-US/article/Create-a-team-site-in-SharePoint-Online-ef10c1e7-15f3-42a3-98aa-b5972711777d)
- [Verwalten von websiteerstellung in SharePoint Online](https://support.office.com/en-us/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9?ui=en-US&rs=en-US&ad=US)
- [Verwalten Sie Ihrer SharePoint-Team-websiteeinstellungen](https://support.office.com/en-us/article/Manage-your-SharePoint-team-site-settings-8376034d-d0c7-446e-9178-6ab51c58df42?ui=en-US&rs=en-US&ad=US)
