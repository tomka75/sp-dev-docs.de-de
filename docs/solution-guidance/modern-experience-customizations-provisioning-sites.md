---
title: Bereitstellen von "modernen" Teamwebsites programmgesteuert
description: "Bereitstellen einer Teamwebsite über die Benutzeroberfläche oder mit Plug & Play-CSOM Core oder Plug & Play-PowerShell."
ms.date: 12/19/2017
ms.openlocfilehash: f9016d6798eb3cda98eb7a801340b7c438c63ab5
ms.sourcegitcommit: bf4bc1e80c6ef1a0ff479039ef9ae0ee84d5f6b4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2017
---
# <a name="provisioning-modern-team-sites-programmatically"></a>Bereitstellen von "modernen" Teamwebsites programmgesteuert

"Modernen" Websites in SharePoint Online im Herbst des 2016 eingeführt wurden und die Möglichkeit, verwenden sie auf der Ebene der Mandant gesteuert werden kann. In diesem Artikel werden die verschiedenen Optionen und Aspekte für die Bereitstellung von "modernen" Websites in SharePoint Online. Insbesondere behandelt der Artikel sowohl Teamwebsites "modernen" und "modernen" kommunikationswebsites zu erstellen.

> [!IMPORTANT]
> Wir sind nicht die "klassische" Erfahrung veralteter; "klassische" und "modernen" werden gleichzeitig verwendet werden.

## <a name="comparing-modern-team-sites-and-modern-communication-sites"></a>Vergleichen von Teamwebsites "modernen" und "modernen" kommunikationswebsites
Bevor Sie eine Suche in der ausführliche Informationen zum Bereitstellen von "modernen" Websites, betrachten wir etwas über die zwei wichtigsten Arten: Teamwebsites und kommunikationswebsites.

Eine Teamwebsite "modernen" ist ein Platz, in dem eine Gruppe von Personen zusammenarbeiten kann, Zusammenarbeit, Dokumente und Nachrichten freigeben. Jeder Teamwebsite "modernen" hat eine Sicherung Office 365 Gruppe, um die allgemeine Zusammenarbeit optimieren. Tatsächlich können Teammitglieder Dank der Office 365-Gruppe von Diensten wie Planner, einen freigegebenen Kalender, einen freigegebenen OneDrive für Unternehmen Speicher, benutzerdefinierte Konnektoren für Office 365 usw. nutzen. Die Mitglieder können in der Regel in einer "modernen" Teamwebsite auf den Inhalt (Lese-/Schreibzugriff) beitragen. Darüber hinaus kann der Office 365-Gruppe Sichern einer Teamwebsite "modernen" privaten oder öffentlichen, und in der Standardeinstellung ist öffentlich.

Eine Website "modernen" Kommunikation ist ein Ort, in dem Sie News, freigeben können, einen Textabschnitt präsentieren, eine Nachricht senden. Die Vorstellung, dass eine Website für die Kommunikation ist einige Editoren, die den Inhalt und eine große Zielgruppe, der diesen Inhalt erstellen und verwalten. Eine Website für die Kommunikation muss jedoch keine Sicherung Office 365-Gruppe. Benutzer können die Zielwebsite für die Kommunikation mit dem bekannten Satz von Berechtigungen für andere SharePoint-Website zugreifen, und jede Website Kommunikation ist standardmäßig privat.

Wenn Sie zum Erstellen einer Website für die Teamzusammenarbeit verfügen, beträgt wahrscheinlich die Teamwebsite "modernen" die richtige Wahl. Im Gegensatz dazu, wenn Sie etwas für eine Vielzahl von Personen kommunizieren möchten, stellen wahrscheinlich die Website für die Kommunikation die beste Wahl.

## <a name="provisioning-modern-team-sites"></a>Bereitstellen von "modernen" Teamwebsites


Jetzt in diesem Abschnitt erfahren Sie, wie eine "modernen" Teamwebsite bereitgestellt, und was sind die verfügbaren Optionen dafür.

### <a name="provisioning-a-modern-team-site-from-the-user-interface"></a>Bereitstellung einer "modernen" Teamwebsite aus der Benutzeroberfläche

Es gibt zahlreiche Routen für eine "modernen" Teamwebsite bereitgestellt erhalten möchten. Sie können die Bereitstellung direkt über die SharePoint Online-Website starten, oder Sie können alternativ bereitstellen eine Office 365-Gruppe aus anderen Speicherorten (z. B. von Outlook), die auch dann löst die Bereitstellung einer "modernen" Team Site. 

- Wenn Ihr Administrator "modernen" Teamwebsites in Ihrem Mandanten aktiviert, können Sie der Homepage der SharePoint "modernen" Teamwebsites erstellen.

- Sie können auch eine Office 365-Gruppe von Office 365 Outlook erstellen, und wenn Sie auf die Registerkarte Standort der Gruppe zugreifen, sorgt auf einer Teamwebsite "modernen". 

### <a name="how-to-control-default-provisioning-flow"></a>Standardmäßige provisioning Ablauf der Steuerung

Sie können die SharePoint-Website Erstellungsprozess SharePoint Online Admin Einstellungen steuern. Sie können auswählen, wenn die Erfahrung "moderne" für die Endbenutzer verfügbar ist oder wenn Sie fortfahren, verwenden die "klassische" Erfahrung möchten.

![Optionen zum Erstellen einer Website aus der SharePoint Online Admin-Benutzeroberfläche](media/modern-experiences/site-creation-options-admin-ui.png)

Finden Sie im folgenden Office-Support-Artikel Weitere Informationen:
- Verwalten von websiteerstellung in SharePoint Online: https://support.office.com/en-US/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9

### <a name="provisioning-a-modern-team-site-programmatically-via-sharepoint-online-rest-api"></a>Bereitstellung einer "modernen" Teamwebsite programmgesteuert über SharePoint Online-REST-API

"Modernen" Teamwebsites können programmgesteuert mithilfe von SharePoint Online bereitgestellt und von der Website erstellen Benutzeroberfläche von SharePoint Online zu verwendet eine REST-API erstellt werden.

#### <a name="provisioning-a-modern-team-site-using-the-pnp-csom-core-component"></a>Bereitstellung einer "modernen" Teamwebsite Hauptkomponenten Plug & Play-CSOM verwenden

In SharePoint Plug & Play-Hauptkomponenten - seit der Veröffentlichung Oktober 2017 (V. 2.19.1710.1) - Es wird eine neue Erweiterungsmethode für den CSOM _ClientContext_ -Typ. Der Name der Erweiterung-Methode ist _CreateSiteAsync_ und zum Erstellen einer Teamwebsite "modernen" in einige Sekunden ermöglicht. Im folgenden Codeausschnitt sehen Sie, wie Sie dieses Verfahren verwendet wird.

```C#
// Let's use the CreateSiteAsync extension method of PnP CSOM Core
// to create the "modern" team site

var targetTenantUrl = "https://[tenant].sharepoint.com/";

using (var context = new ClientContext(targetTenantUrl))
{
    context.Credentials = OfficeDevPnP.Core.Utilities.CredentialManager.GetSharePointOnlineCredential("[Name-of-Your-Credentials]");

    // Create new "modern" team site at the url
    // https://[tenant].sharepoint.com/sites/mymodernteamsite
    var teamContext = await context.CreateSiteAsync(
        new TeamSiteCollectionCreationInformation
        {
            Alias = "mymodernteamsite", // Mandatory
            DisplayName = "displayName", // Mandatory
            Description = "description", // Optional
            Classification = "classification", // Optional
            IsPublic = true, // Optional, default true
        });
    teamContext.Load(teamContext.Web, w => w.Url);
    teamContext.ExecuteQueryRetry();
    Console.WriteLine(teamContext.Web.Url);
}
```

> [!NOTE]
> In der [offizielle Dokumentation](https://msdn.microsoft.com/en-us/pnp_articles/modern-experience-site-classification)finden Sie weitere Details über das Argument _Klassifikation_ .

Wie Sie sehen können, die Erweiterungsmethode erstellt eine neue "modernen" Teamwebsite und gibt ein neues _ClientContext_ -Objekt direkt mit der neu erstellten Website verbunden ist.

#### <a name="provisioning-a-modern-team-site-using-pnp-powershell"></a>Bereitstellung einer "modernen" Teamwebsite von Plug & Play-PowerShell

Sie können auch von [Plug & Play-PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases)"modernen" Websites erstellen. Das folgende Skript erstellen eine Teamwebsite "modernen" und dann zurückgeben den tatsächlichen SharePoint-Website-URL zur weiteren Bearbeitung. Sobald Sie Zugriff auf die URL der Website erstellt haben, können Sie CSOM (mit SharePoint Plug & Play-Hauptkomponenten) oder SharePoint PnP-PowerShell verwenden, um anderer Vorgänge auf der erstellten Website zu automatisieren.

```ps
# Connect to SharePoint Online
# This command will prompt the sign-in UI to authenticate
Connect-PnPOnline "https://[tenant].sharepoint.com/"

# Create the new "modern" team site
$teamSiteUrl = New-PnPSite -Type TeamSite -Title "displayName" -Alias "mymodernteamsite" -Description "description" -IsPublic -Classification "classification" 

# Connect to the modern site using PnP PowerShell SP cmdlets
# Since we are connecting now to SP side, credentials will be asked
Connect-PnPOnline $teamSiteUrl

# Now we have access on the SharePoint site for any operations
$context = Get-PnPContext
$web = Get-PnPWeb
$context.Load($web, $web.WebTemplate)
Execute-PnPQuery
$web.WebTemplate + "#" + $web.Configuration
```

### <a name="provisioning-an-office-365-group-programmatically"></a>Bereitstellen einer Office 365-Gruppe programmgesteuert

"Modernen" Teamwebsites können programmgesteuert, indem Sie mit der Microsoft Graph zu einer [Gruppe von Office 365](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/group) erstellen erstellt werden. Tatsächlich, wenn Sie eine Office 365-Gruppe "modernen" Erstellen einer Teamwebsite werden automatisch für die Gruppe bereitgestellt. Die "modernen" Teamwebsite URI je nach der _MailNickname_ -Parameter der Gruppe der Office 365 und verfügt über die folgenden standardmäßigen Struktur. 

```
https://[tenant].sharepoint.com/sites/[mailNickname]
``` 

> [!NOTE]
> Eine ausführliche Beschreibung der Erstellung von Gruppen mithilfe von Microsoft Graph ist von der [offizielle Dokumentation](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/group_post_groups)zur Verfügung.

#### <a name="provisioning-an-office-365-group-using-the-pnp-csom-core-component"></a>Bereitstellung mit Plug & Play-CSOM Hauptkomponenten einer Office 365-Gruppe

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

#### <a name="provisioning-an-office-365-group-using-pnp-powershell"></a>Bereitstellen einer Office 365-Gruppe von Plug & Play-PowerShell

Sie können auch eine Office 365-Gruppe von [Plug & Play-PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases), Sie die Authentifizierung auf einfache Weise mit der Microsoft Graph mit Azure Active Directory können erstellen. Das folgende Skript erstellen ein Office 365-Gruppe, zusammen mit einer "modernen" Teamwebsite, und klicken Sie dann zurückgeben den tatsächlichen SharePoint-Website-URL zur weiteren Bearbeitung. Sobald Sie Zugriff auf die URL der Website erstellt haben, können Sie CSOM (mit SharePoint Plug & Play-Hauptkomponenten) oder SharePoint PnP-PowerShell verwenden, um anderer Vorgänge auf der erstellten Website zu automatisieren.

```ps
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
> Derzeit wird nicht unterstützt "modernen" Teamwebsites mit [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588)bereit.

## <a name="provisioning-modern-communication-sites"></a>Bereitstellen von kommunikationswebsites "modernen

In diesem Abschnitt erfahren Sie, wie zum Bereitstellen einer Website "modernen" Kommunikation, und was sind die verfügbaren Optionen dafür.

### <a name="provisioning-a-modern-communication-site-from-user-interface"></a>Bereitstellen einer Website "modernen" Kommunikation von Benutzeroberfläche

Um eine Kommunikation "modernen" Site mithilfe der Benutzeroberfläche – Wenn Ihr Administrator "modernen" Teamwebsites in Ihrem Mandanten aktiviert - bereitstellen können Sie direkt über der Homepage der SharePoint Online starten. Klicken Sie auf die Schaltfläche 'Site erstellen' erstellen 'Kommunikation Site', wählen ein Design für Ihre Website aus, verfügen Sie alle über einen Namen und eine Beschreibung sowie die Website in Sekundenschnelle einige erstellt werden.
Zeitpunkt der Erstellung dieses Dokuments sind die verfügbaren Designs für eine Website für die Kommunikation:
* **Thema**: Verwenden Sie diese Vorlage aus, wenn Sie viel Informationen wie Nachrichten, Ereignisse und andere Inhalte freigegeben haben.
* **Showcase**: Verwenden Sie diese Vorlage um zu einem Produkt, Team oder Ereignis mithilfe von Fotos oder Bilder zu präsentieren.
* **Leere**: beginnen Sie mit einer leeren Website, und stellen Sie Ihren Entwurf zum Leben schnell und einfach erfolgen.

### <a name="provisioning-a-modern-communication-site-programmatically"></a>Bereitstellung einer Site "modernen" Kommunikation programmgesteuert

Wenn Sie lieber bevorzugen, können Sie eine "modernen" Kommunikation-Website, die programmgesteuert mit entweder CSOM erstellen und Plug & Play-, oder PowerShell.

#### <a name="provisioning-a-modern-communication-site-using-the-pnp-csom-core-component"></a>Bereitstellen einer Hauptkomponenten Plug & Play-CSOM mit "modernen" Kommunikation-Website

Die Plug & Play-CSOM-Core-Komponente als [NuGet-Paket](https://www.nuget.org/packages/SharePointPnPCoreOnline), verfügt über vereinfachte Methoden für die Behandlung von "modernen" Websites. 

```C#
// Let's use the CreateSiteAsync extension method of PnP CSOM Core
// to create the "modern" team site

var targetTenantUrl = "https://[tenant].sharepoint.com/";

using (var context = new ClientContext(targetTenantUrl))
{
    context.Credentials = OfficeDevPnP.Core.Utilities.CredentialManager.GetSharePointOnlineCredential("[Name-of-Your-Credentials]");

    // Create new "modern" communication site at the url https://[tenant].sharepoint.com/sites/mymoderncommunicationsite
    var communicationContext = await context.CreateSiteAsync(new CommunicationSiteCollectionCreationInformation {
        Title = "title", // Mandatory
        Description = "description", // Mandatory
        Lcid = 1033, // Mandatory
        AllowFileSharingForGuestUsers = false, // Optional
        Classification = "classification", // Optional
        SiteDesign = CommunicationSiteDesign.Topic, // Mandatory
        Url = "https://[tenant].sharepoint.com/sites/mymoderncommunicationsite", // Mandatory
    });
    communicationContext.Load(communicationContext.Web, w => w.Url);
    communicationContext.ExecuteQueryRetry();
    Console.WriteLine(communicationContext.Web.Url);
}
```

Wie Sie sehen können, die Erweiterungsmethode erstellt eine neue Website "modernen" Kommunikation und gibt ein neues _ClientContext_ -Objekt direkt mit der neu erstellten Website verbunden ist.

#### <a name="provisioning-a-modern-team-site-using-pnp-powershell"></a>Bereitstellung einer "modernen" Teamwebsite von Plug & Play-PowerShell

Das folgende Skript erstellen eine Website "modernen" Kommunikation und dann zurückgeben den tatsächlichen SharePoint-Website-URL zur weiteren Bearbeitung, wie wie im vorherigen Beispiel mit "modernen" Teamwebsites war.

```ps
# Connect to SharePoint Online
# This command will prompt the sign-in UI to authenticate
Connect-PnPOnline "https://[tenant].sharepoint.com/"

# Create the new "modern" communication site
$communicationSiteUrl = New-PnPSite -Type CommunicationSite -Title "displayName" -Url "https://[tenant].sharepoint.com/sites/mymoderncommunicationsite" -Description "description" -Classification "classification" -SiteDesign Topic

# Connect to the modern site using PnP PowerShell SP cmdlets
# Since we are connecting now to SP side, credentials will be asked
Connect-PnPOnline $teamSiteUrl

# Now we have access on the SharePoint site for any operations
$context = Get-PnPContext
$web = Get-PnPWeb
$context.Load($web, $web.Title)
Execute-PnPQuery
$web.Title
```

## <a name="additional-considerations"></a>Zusätzliche Überlegungen

### <a name="sub-sites-use-classic-templates"></a>Sub-Websites verwenden "klassische" Vorlagen

Wenn Sie eine Unterwebsite unter der Stammwebsite einer Websitesammlung "modernen" bereitstellen, werden "Sub" Websites "klassische" Vorlagen verwenden. Derzeit sind keine "modernen" Sub-Websitevorlagen verfügbar. Eine "klassische" Sub-Website auf eine Teamwebsite "modernen" können von einer Seite "modernen" auf der Website erstellen und Aktualisieren der Seite Willkommen auf der neu erstellten Seite transformiert werden.  

Wenn Sie nicht für Benutzer zu eine "klassische" Sub-Website unter einer "modernen" Websitesammlung erstellen möchten, als Administrator navigieren Sie zu der SharePoint-Verwaltungskonsole wählen Sie der Seite Einstellungen und konfigurieren die Option für "Unterwebsite erstellen" das "Unterwebsite" Erstellung Menü ausblenden. Sie können die Option "Unterwebsite erstellen" in der folgenden Abbildung sehen.

![Optionen zum Erstellen von SharePoint Online Administratorbenutzeroberfläche Unterwebsite](media/modern-experiences/subsite-creation-admin-setting.png)

### <a name="sites-are-not-listed-in-the-classic-sharepoint-admin-ui--tenant-api"></a>Websites werden nicht in der klassischen SharePoint Admin-Benutzeroberfläche aufgeführt / Mandanten-API

"Modernen" Teamwebsites werden nicht in der SharePoint-Admin-Benutzeroberfläche angezeigt. Sie können die Liste der "modernen" Teamwebsites aus der Admin-Benutzeroberfläche von Office 365 Gruppen unter Office 365-Verwaltungsportal zugreifen. SharePoint Online Admin-Benutzeroberfläche nur Listen "klassische" SharePoint-Websites. Dieselbe Einschränkung gilt nicht für den Mandanten API: Sie können diese API verwenden, um "modernen" Teamwebsites zusammen mit "klassische" Teamwebsites aufgelistet werden. Zum Abrufen einer Liste von nur "modernen" Teamwebsites können Sie auch den Endpunkt Gruppen von Microsoft Graph-API verwenden.

Es gibt auch eine anstehende neue SharePoint Admin-Benutzeroberfläche, die Verwaltung von der neuen "modernen" Websitesammlungen zusammen mit "klassischen" diejenigen unterstützt.

## <a name="see-also"></a>Siehe auch

- [Anpassen der „modernen“ Benutzeroberflächen in SharePoint Online](modern-experience-customizations.md)
- [Was ist eine SharePoint-Teamwebsite?](https://support.office.com/en-US/article/What-is-a-SharePoint-team-site-75545757-36c3-46a7-beed-0aaa74f0401e?ui=en-US&rs=en-US&ad=US)
- [Erstellen einer Teamwebsite in SharePoint Online](https://support.office.com/en-US/article/Create-a-team-site-in-SharePoint-Online-ef10c1e7-15f3-42a3-98aa-b5972711777d)
- [Verwalten von websiteerstellung in SharePoint Online](https://support.office.com/en-us/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9?ui=en-US&rs=en-US&ad=US)
- [Verwalten Sie Ihrer SharePoint-Team-websiteeinstellungen](https://support.office.com/en-us/article/Manage-your-SharePoint-team-site-settings-8376034d-d0c7-446e-9178-6ab51c58df42?ui=en-US&rs=en-US&ad=US)
