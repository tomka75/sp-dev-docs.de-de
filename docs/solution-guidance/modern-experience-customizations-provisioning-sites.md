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
# <a name="provisioning-modern-team-sites-programmatically"></a><span data-ttu-id="a5ad3-103">Bereitstellen von "modernen" Teamwebsites programmgesteuert</span><span class="sxs-lookup"><span data-stu-id="a5ad3-103">Provisioning "modern" team sites programmatically</span></span>

<span data-ttu-id="a5ad3-104">"Modernen" Websites in SharePoint Online im Herbst des 2016 eingeführt wurden und die Möglichkeit, verwenden sie auf der Ebene der Mandant gesteuert werden kann.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-104">"Modern" sites were introduced in SharePoint Online during the autumn of 2016 and the option to use them can be controlled at the tenant level.</span></span> <span data-ttu-id="a5ad3-105">In diesem Artikel werden die verschiedenen Optionen und Aspekte für die Bereitstellung von "modernen" Websites in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-105">This article discusses the different options and considerations for provisioning "modern" sites in SharePoint Online.</span></span> <span data-ttu-id="a5ad3-106">Insbesondere behandelt der Artikel sowohl Teamwebsites "modernen" und "modernen" kommunikationswebsites zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-106">In particular, the article covers how to create both "modern" team sites, and "modern" communication sites.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5ad3-107">Wir sind nicht die "klassische" Erfahrung veralteter; "klassische" und "modernen" werden gleichzeitig verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-107">We're not deprecating the "classic" experience; both "classic" and "modern" will coexist.</span></span>

## <a name="comparing-modern-team-sites-and-modern-communication-sites"></a><span data-ttu-id="a5ad3-108">Vergleichen von Teamwebsites "modernen" und "modernen" kommunikationswebsites</span><span class="sxs-lookup"><span data-stu-id="a5ad3-108">Comparing "modern" team sites and "modern" communication sites</span></span>
<span data-ttu-id="a5ad3-109">Bevor Sie eine Suche in der ausführliche Informationen zum Bereitstellen von "modernen" Websites, betrachten wir etwas über die zwei wichtigsten Arten: Teamwebsites und kommunikationswebsites.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-109">Before digging into the details about how to provision "modern" sites, let's discuss a little bit about the two main flavors available: team sites, and communication sites.</span></span>

<span data-ttu-id="a5ad3-110">Eine Teamwebsite "modernen" ist ein Platz, in dem eine Gruppe von Personen zusammenarbeiten kann, Zusammenarbeit, Dokumente und Nachrichten freigeben.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-110">A "modern" team site is a place where a group of people can work together, collaborate, share documents and messages.</span></span> <span data-ttu-id="a5ad3-111">Jeder Teamwebsite "modernen" hat eine Sicherung Office 365 Gruppe, um die allgemeine Zusammenarbeit optimieren.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-111">Every "modern" team site has a backing Office 365 Group, in order to improve the overall collaboration experience.</span></span> <span data-ttu-id="a5ad3-112">Tatsächlich können Teammitglieder Dank der Office 365-Gruppe von Diensten wie Planner, einen freigegebenen Kalender, einen freigegebenen OneDrive für Unternehmen Speicher, benutzerdefinierte Konnektoren für Office 365 usw. nutzen. Die Mitglieder können in der Regel in einer "modernen" Teamwebsite auf den Inhalt (Lese-/Schreibzugriff) beitragen.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-112">In fact, thanks to the Office 365 Group, members of the team can benefit of services like Planner, a shared Calendar, a shared OneDrive for Business storage, custom Office 365 connectors, etc. In a "modern" team site, typically the members can contribute to the content (read/write).</span></span> <span data-ttu-id="a5ad3-113">Darüber hinaus kann der Office 365-Gruppe Sichern einer Teamwebsite "modernen" privaten oder öffentlichen, und in der Standardeinstellung ist öffentlich.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-113">Moreover, the Office 365 Group backing a "modern" team site can be private or public, and by default it is public.</span></span>

<span data-ttu-id="a5ad3-114">Eine Website "modernen" Kommunikation ist ein Ort, in dem Sie News, freigeben können, einen Textabschnitt präsentieren, eine Nachricht senden.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-114">A "modern" communication site is a place where you can share news, showcase a story, broadcast a message.</span></span> <span data-ttu-id="a5ad3-115">Die Vorstellung, dass eine Website für die Kommunikation ist einige Editoren, die den Inhalt und eine große Zielgruppe, der diesen Inhalt erstellen und verwalten.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-115">The idea of a communication site is to have few editors that create and maintain the content, and a wide audience that consumes that content.</span></span> <span data-ttu-id="a5ad3-116">Eine Website für die Kommunikation muss jedoch keine Sicherung Office 365-Gruppe.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-116">However, a communication site does not have a backing Office 365 Group.</span></span> <span data-ttu-id="a5ad3-117">Benutzer können die Zielwebsite für die Kommunikation mit dem bekannten Satz von Berechtigungen für andere SharePoint-Website zugreifen, und jede Website Kommunikation ist standardmäßig privat.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-117">Users can access the target communication site with the well-known set of permissions of any other SharePoint site, and by default every communication site is private.</span></span>

<span data-ttu-id="a5ad3-118">Wenn Sie zum Erstellen einer Website für die Teamzusammenarbeit verfügen, beträgt wahrscheinlich die Teamwebsite "modernen" die richtige Wahl.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-118">Thus, if you have to create a site for team collaboration, most likely the "modern" team site is the right choice.</span></span> <span data-ttu-id="a5ad3-119">Im Gegensatz dazu, wenn Sie etwas für eine Vielzahl von Personen kommunizieren möchten, stellen wahrscheinlich die Website für die Kommunikation die beste Wahl.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-119">On the contrary, if you want to communicate something to a broad set of people, probably the communication site is your best choice.</span></span>

## <a name="provisioning-modern-team-sites"></a><span data-ttu-id="a5ad3-120">Bereitstellen von "modernen" Teamwebsites</span><span class="sxs-lookup"><span data-stu-id="a5ad3-120">Provisioning "modern" team sites</span></span>


<span data-ttu-id="a5ad3-121">Jetzt in diesem Abschnitt erfahren Sie, wie eine "modernen" Teamwebsite bereitgestellt, und was sind die verfügbaren Optionen dafür.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-121">Now in this section you will learn how to provision a "modern" team site, and what are the available options to do that.</span></span>

### <a name="provisioning-a-modern-team-site-from-the-user-interface"></a><span data-ttu-id="a5ad3-122">Bereitstellung einer "modernen" Teamwebsite aus der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="a5ad3-122">Provisioning a "modern" team site from the user interface</span></span>

<span data-ttu-id="a5ad3-123">Es gibt zahlreiche Routen für eine "modernen" Teamwebsite bereitgestellt erhalten möchten.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-123">There are numerous routes for a "modern" team site to get provisioned.</span></span> <span data-ttu-id="a5ad3-124">Sie können die Bereitstellung direkt über die SharePoint Online-Website starten, oder Sie können alternativ bereitstellen eine Office 365-Gruppe aus anderen Speicherorten (z. B. von Outlook), die auch dann löst die Bereitstellung einer "modernen" Team Site.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-124">You can start the provisioning directly from the SharePoint Online site, or alternatively provision an Office 365 group from other locations (for example, from Outlook), which then also triggers the provisioning of a "modern" team site.</span></span> 

- <span data-ttu-id="a5ad3-125">Wenn Ihr Administrator "modernen" Teamwebsites in Ihrem Mandanten aktiviert, können Sie der Homepage der SharePoint "modernen" Teamwebsites erstellen.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-125">If your administrator enabled "modern" team sites in your tenant, you can create "modern" team sites from the SharePoint home page.</span></span>

- <span data-ttu-id="a5ad3-126">Sie können auch eine Office 365-Gruppe von Office 365 Outlook erstellen, und wenn Sie auf die Registerkarte Standort der Gruppe zugreifen, sorgt auf einer Teamwebsite "modernen".</span><span class="sxs-lookup"><span data-stu-id="a5ad3-126">You can also create an Office 365 group from Office 365 Outlook, and when you access the site tab of that group, you land on a "modern" team site.</span></span> 

### <a name="how-to-control-default-provisioning-flow"></a><span data-ttu-id="a5ad3-127">Standardmäßige provisioning Ablauf der Steuerung</span><span class="sxs-lookup"><span data-stu-id="a5ad3-127">How to control default provisioning flow</span></span>

<span data-ttu-id="a5ad3-128">Sie können die SharePoint-Website Erstellungsprozess SharePoint Online Admin Einstellungen steuern.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-128">You can control the SharePoint site creation process from the SharePoint Online admin settings.</span></span> <span data-ttu-id="a5ad3-129">Sie können auswählen, wenn die Erfahrung "moderne" für die Endbenutzer verfügbar ist oder wenn Sie fortfahren, verwenden die "klassische" Erfahrung möchten.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-129">You can choose if the "modern" experience is available for your end users or if you'd like to continue using the "classic" experience.</span></span>

![Optionen zum Erstellen einer Website aus der SharePoint Online Admin-Benutzeroberfläche](media/modern-experiences/site-creation-options-admin-ui.png)

<span data-ttu-id="a5ad3-131">Finden Sie im folgenden Office-Support-Artikel Weitere Informationen:</span><span class="sxs-lookup"><span data-stu-id="a5ad3-131">See the following Office Support article for details:</span></span>
- <span data-ttu-id="a5ad3-132">Verwalten von websiteerstellung in SharePoint Online: https://support.office.com/en-US/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9</span><span class="sxs-lookup"><span data-stu-id="a5ad3-132">Manage site creation in SharePoint Online: https://support.office.com/en-US/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9</span></span>

### <a name="provisioning-a-modern-team-site-programmatically-via-sharepoint-online-rest-api"></a><span data-ttu-id="a5ad3-133">Bereitstellung einer "modernen" Teamwebsite programmgesteuert über SharePoint Online-REST-API</span><span class="sxs-lookup"><span data-stu-id="a5ad3-133">Provisioning a "modern" team site programmatically via SharePoint Online REST API</span></span>

<span data-ttu-id="a5ad3-134">"Modernen" Teamwebsites können programmgesteuert mithilfe von SharePoint Online bereitgestellt und von der Website erstellen Benutzeroberfläche von SharePoint Online zu verwendet eine REST-API erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-134">"Modern" team sites can be created programmatically using a REST API provided by SharePoint Online, and used by the 'Create Site' UI of SharePoint Online, too.</span></span>

#### <a name="provisioning-a-modern-team-site-using-the-pnp-csom-core-component"></a><span data-ttu-id="a5ad3-135">Bereitstellung einer "modernen" Teamwebsite Hauptkomponenten Plug & Play-CSOM verwenden</span><span class="sxs-lookup"><span data-stu-id="a5ad3-135">Provisioning a "modern" team site using the PnP CSOM core component</span></span>

<span data-ttu-id="a5ad3-136">In SharePoint Plug & Play-Hauptkomponenten - seit der Veröffentlichung Oktober 2017 (V.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-136">In the SharePoint PnP Core component - since the October 2017 release (v.</span></span> <span data-ttu-id="a5ad3-137">2.19.1710.1) - Es wird eine neue Erweiterungsmethode für den CSOM _ClientContext_ -Typ.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-137">2.19.1710.1) - there is a new extension method for the CSOM _ClientContext_ type.</span></span> <span data-ttu-id="a5ad3-138">Der Name der Erweiterung-Methode ist _CreateSiteAsync_ und zum Erstellen einer Teamwebsite "modernen" in einige Sekunden ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-138">The extension method name is _CreateSiteAsync_ and allows you to create a "modern" team site in a matter of few seconds.</span></span> <span data-ttu-id="a5ad3-139">Im folgenden Codeausschnitt sehen Sie, wie Sie dieses Verfahren verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-139">In the following code snippet you can see how to use this technique.</span></span>

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
> <span data-ttu-id="a5ad3-140">In der [offizielle Dokumentation](https://msdn.microsoft.com/en-us/pnp_articles/modern-experience-site-classification)finden Sie weitere Details über das Argument _Klassifikation_ .</span><span class="sxs-lookup"><span data-stu-id="a5ad3-140">You can find further details about the _Classification_ argument in the [official documentation](https://msdn.microsoft.com/en-us/pnp_articles/modern-experience-site-classification).</span></span>

<span data-ttu-id="a5ad3-141">Wie Sie sehen können, die Erweiterungsmethode erstellt eine neue "modernen" Teamwebsite und gibt ein neues _ClientContext_ -Objekt direkt mit der neu erstellten Website verbunden ist.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-141">As you can see, the extension method creates a new "modern" team site and returns a new _ClientContext_ object directly connected to the newly created site.</span></span>

#### <a name="provisioning-a-modern-team-site-using-pnp-powershell"></a><span data-ttu-id="a5ad3-142">Bereitstellung einer "modernen" Teamwebsite von Plug & Play-PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5ad3-142">Provisioning a "modern" team site using PnP PowerShell</span></span>

<span data-ttu-id="a5ad3-143">Sie können auch von [Plug & Play-PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases)"modernen" Websites erstellen.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-143">You can also create "modern" sites using [PnP PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases).</span></span> <span data-ttu-id="a5ad3-144">Das folgende Skript erstellen eine Teamwebsite "modernen" und dann zurückgeben den tatsächlichen SharePoint-Website-URL zur weiteren Bearbeitung.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-144">The following script will create a "modern" team site and then return the actual SharePoint site URL for further manipulation.</span></span> <span data-ttu-id="a5ad3-145">Sobald Sie Zugriff auf die URL der Website erstellt haben, können Sie CSOM (mit SharePoint Plug & Play-Hauptkomponenten) oder SharePoint PnP-PowerShell verwenden, um anderer Vorgänge auf der erstellten Website zu automatisieren.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-145">Once you have access to the URL of the created site, you can use CSOM (with the SharePoint PnP Core component) or SharePoint PnP-PowerShell to automate other operations on the created site.</span></span>

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

### <a name="provisioning-an-office-365-group-programmatically"></a><span data-ttu-id="a5ad3-146">Bereitstellen einer Office 365-Gruppe programmgesteuert</span><span class="sxs-lookup"><span data-stu-id="a5ad3-146">Provisioning an Office 365 Group programmatically</span></span>

<span data-ttu-id="a5ad3-147">"Modernen" Teamwebsites können programmgesteuert, indem Sie mit der Microsoft Graph zu einer [Gruppe von Office 365](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/group) erstellen erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-147">"Modern" team sites can be created programmatically by creating an [Office 365 group](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/group) using the Microsoft Graph, too.</span></span> <span data-ttu-id="a5ad3-148">Tatsächlich, wenn Sie eine Office 365-Gruppe "modernen" Erstellen einer Teamwebsite werden automatisch für die Gruppe bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-148">In fact, when you create an Office 365 group a "modern" team site is automatically provisioned for the group.</span></span> <span data-ttu-id="a5ad3-149">Die "modernen" Teamwebsite URI je nach der _MailNickname_ -Parameter der Gruppe der Office 365 und verfügt über die folgenden standardmäßigen Struktur.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-149">The "modern" team site URI will be based upon the _mailNickname_ parameter of the Office 365 group and has the following default structure.</span></span> 

```
https://[tenant].sharepoint.com/sites/[mailNickname]
``` 

> [!NOTE]
> <span data-ttu-id="a5ad3-150">Eine ausführliche Beschreibung der Erstellung von Gruppen mithilfe von Microsoft Graph ist von der [offizielle Dokumentation](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/group_post_groups)zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-150">A detailed description of group creation using Microsoft Graph is available from the [official documentation](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/group_post_groups).</span></span>

#### <a name="provisioning-an-office-365-group-using-the-pnp-csom-core-component"></a><span data-ttu-id="a5ad3-151">Bereitstellung mit Plug & Play-CSOM Hauptkomponenten einer Office 365-Gruppe</span><span class="sxs-lookup"><span data-stu-id="a5ad3-151">Provisioning an Office 365 Group using the PnP CSOM core component</span></span>

<span data-ttu-id="a5ad3-152">Die Plug & Play-CSOM-Core-Komponente als [NuGet-Paket](https://www.nuget.org/packages/SharePointPnPCoreOnline)wurde Methoden für den Umgang mit "modernen" Gruppe vereinfacht.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-152">The PnP CSOM Core component, available as a [NuGet package](https://www.nuget.org/packages/SharePointPnPCoreOnline), has simplified methods for the "modern" group handling.</span></span> 

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

#### <a name="provisioning-an-office-365-group-using-pnp-powershell"></a><span data-ttu-id="a5ad3-153">Bereitstellen einer Office 365-Gruppe von Plug & Play-PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5ad3-153">Provisioning an Office 365 Group using PnP PowerShell</span></span>

<span data-ttu-id="a5ad3-154">Sie können auch eine Office 365-Gruppe von [Plug & Play-PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases), Sie die Authentifizierung auf einfache Weise mit der Microsoft Graph mit Azure Active Directory können erstellen.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-154">You can also create an Office 365 Group using [PnP PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases), which will let you easily authenticate with the Microsoft Graph using Azure Active Directory.</span></span> <span data-ttu-id="a5ad3-155">Das folgende Skript erstellen ein Office 365-Gruppe, zusammen mit einer "modernen" Teamwebsite, und klicken Sie dann zurückgeben den tatsächlichen SharePoint-Website-URL zur weiteren Bearbeitung.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-155">The following script will create an Office 365 Group, together with a "modern" team site, and then return the actual SharePoint site URL for further manipulation.</span></span> <span data-ttu-id="a5ad3-156">Sobald Sie Zugriff auf die URL der Website erstellt haben, können Sie CSOM (mit SharePoint Plug & Play-Hauptkomponenten) oder SharePoint PnP-PowerShell verwenden, um anderer Vorgänge auf der erstellten Website zu automatisieren.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-156">Once you have access to the URL of the created site, you can use CSOM (with the SharePoint PnP Core component) or SharePoint PnP-PowerShell to automate other operations on the created site.</span></span>

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
> <span data-ttu-id="a5ad3-157">Derzeit wird nicht unterstützt "modernen" Teamwebsites mit [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588)bereit.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-157">There is currently no support to provision "modern" team sites using [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span>

## <a name="provisioning-modern-communication-sites"></a><span data-ttu-id="a5ad3-158">Bereitstellen von kommunikationswebsites "modernen</span><span class="sxs-lookup"><span data-stu-id="a5ad3-158">Provisioning "Modern" communication sites</span></span>

<span data-ttu-id="a5ad3-159">In diesem Abschnitt erfahren Sie, wie zum Bereitstellen einer Website "modernen" Kommunikation, und was sind die verfügbaren Optionen dafür.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-159">In this section you will learn how to provision a "modern" communication site, and what are the available options to do that.</span></span>

### <a name="provisioning-a-modern-communication-site-from-user-interface"></a><span data-ttu-id="a5ad3-160">Bereitstellen einer Website "modernen" Kommunikation von Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="a5ad3-160">Provisioning a "modern" communication site from user interface</span></span>

<span data-ttu-id="a5ad3-161">Um eine Kommunikation "modernen" Site mithilfe der Benutzeroberfläche – Wenn Ihr Administrator "modernen" Teamwebsites in Ihrem Mandanten aktiviert - bereitstellen können Sie direkt über der Homepage der SharePoint Online starten.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-161">To provision a "modern" communication site using the user interface - if your administrator enabled "modern" team sites in your tenant - you can start directly from the SharePoint Online home page.</span></span> <span data-ttu-id="a5ad3-162">Klicken Sie auf die Schaltfläche 'Site erstellen' erstellen 'Kommunikation Site', wählen ein Design für Ihre Website aus, verfügen Sie alle über einen Namen und eine Beschreibung sowie die Website in Sekundenschnelle einige erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-162">Click the 'Create Site' button, select to create a 'Communication Site', choose a design for your site,  provide a name and a description, and the site will be created in a matter of few seconds.</span></span>
<span data-ttu-id="a5ad3-163">Zeitpunkt der Erstellung dieses Dokuments sind die verfügbaren Designs für eine Website für die Kommunikation:</span><span class="sxs-lookup"><span data-stu-id="a5ad3-163">At the time of this writing the available designs for a communication site are:</span></span>
* <span data-ttu-id="a5ad3-164">**Thema**: Verwenden Sie diese Vorlage aus, wenn Sie viel Informationen wie Nachrichten, Ereignisse und andere Inhalte freigegeben haben.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-164">**Topic**: use this design if you have a lot of information to share such as news, events, and other content.</span></span>
* <span data-ttu-id="a5ad3-165">**Showcase**: Verwenden Sie diese Vorlage um zu einem Produkt, Team oder Ereignis mithilfe von Fotos oder Bilder zu präsentieren.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-165">**Showcase**: use this design to showcase a product, team, or event using photos or images.</span></span>
* <span data-ttu-id="a5ad3-166">**Leere**: beginnen Sie mit einer leeren Website, und stellen Sie Ihren Entwurf zum Leben schnell und einfach erfolgen.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-166">**Blank**: start with a blank site and make your design come to life quickly and easily.</span></span>

### <a name="provisioning-a-modern-communication-site-programmatically"></a><span data-ttu-id="a5ad3-167">Bereitstellung einer Site "modernen" Kommunikation programmgesteuert</span><span class="sxs-lookup"><span data-stu-id="a5ad3-167">Provisioning a "modern" communication site programmatically</span></span>

<span data-ttu-id="a5ad3-168">Wenn Sie lieber bevorzugen, können Sie eine "modernen" Kommunikation-Website, die programmgesteuert mit entweder CSOM erstellen und Plug & Play-, oder PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-168">If you rather prefer, you can create a "modern" communication site programmatically using either CSOM and PnP, or PowerShell.</span></span>

#### <a name="provisioning-a-modern-communication-site-using-the-pnp-csom-core-component"></a><span data-ttu-id="a5ad3-169">Bereitstellen einer Hauptkomponenten Plug & Play-CSOM mit "modernen" Kommunikation-Website</span><span class="sxs-lookup"><span data-stu-id="a5ad3-169">Provisioning a "modern" communication site using the PnP CSOM core component</span></span>

<span data-ttu-id="a5ad3-170">Die Plug & Play-CSOM-Core-Komponente als [NuGet-Paket](https://www.nuget.org/packages/SharePointPnPCoreOnline), verfügt über vereinfachte Methoden für die Behandlung von "modernen" Websites.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-170">The PnP CSOM Core component, available as a [NuGet package](https://www.nuget.org/packages/SharePointPnPCoreOnline), has simplified methods for the "modern" sites handling.</span></span> 

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

<span data-ttu-id="a5ad3-171">Wie Sie sehen können, die Erweiterungsmethode erstellt eine neue Website "modernen" Kommunikation und gibt ein neues _ClientContext_ -Objekt direkt mit der neu erstellten Website verbunden ist.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-171">As you can see, the extension method creates a new "modern" communication site and returns a new _ClientContext_ object directly connected to the newly created site.</span></span>

#### <a name="provisioning-a-modern-team-site-using-pnp-powershell"></a><span data-ttu-id="a5ad3-172">Bereitstellung einer "modernen" Teamwebsite von Plug & Play-PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5ad3-172">Provisioning a "modern" team site using PnP PowerShell</span></span>

<span data-ttu-id="a5ad3-173">Das folgende Skript erstellen eine Website "modernen" Kommunikation und dann zurückgeben den tatsächlichen SharePoint-Website-URL zur weiteren Bearbeitung, wie wie im vorherigen Beispiel mit "modernen" Teamwebsites war.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-173">The following script will create a "modern" communication site and then return the actual SharePoint site URL for further manipulation, as like as it was in the previous example with "modern" team sites.</span></span>

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

## <a name="additional-considerations"></a><span data-ttu-id="a5ad3-174">Zusätzliche Überlegungen</span><span class="sxs-lookup"><span data-stu-id="a5ad3-174">Additional Considerations</span></span>

### <a name="sub-sites-use-classic-templates"></a><span data-ttu-id="a5ad3-175">Sub-Websites verwenden "klassische" Vorlagen</span><span class="sxs-lookup"><span data-stu-id="a5ad3-175">Sub sites use "classic" templates</span></span>

<span data-ttu-id="a5ad3-176">Wenn Sie eine Unterwebsite unter der Stammwebsite einer Websitesammlung "modernen" bereitstellen, werden "Sub" Websites "klassische" Vorlagen verwenden.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-176">If you provision a sub site under the root site of a "modern" site collection, sub sites will use "classic" templates.</span></span> <span data-ttu-id="a5ad3-177">Derzeit sind keine "modernen" Sub-Websitevorlagen verfügbar.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-177">There are currently no "modern" sub site templates available.</span></span> <span data-ttu-id="a5ad3-178">Eine "klassische" Sub-Website auf eine Teamwebsite "modernen" können von einer Seite "modernen" auf der Website erstellen und Aktualisieren der Seite Willkommen auf der neu erstellten Seite transformiert werden.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-178">You can transform a "classic" sub site to a "modern" team site by creating a "modern" page on the site and updating the welcome page to the newly created page.</span></span>  

<span data-ttu-id="a5ad3-179">Wenn Sie nicht für Benutzer zu eine "klassische" Sub-Website unter einer "modernen" Websitesammlung erstellen möchten, als Administrator navigieren Sie zu der SharePoint-Verwaltungskonsole wählen Sie der Seite Einstellungen und konfigurieren die Option für "Unterwebsite erstellen" das "Unterwebsite" Erstellung Menü ausblenden.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-179">If you don't want to allow users to create a "classic" sub site under a "modern" site collection, as an admin you can go to the SharePoint Admin Center, select the Settings page and configure the option for "Subsite Creation" to hide the "subsite" creation menu.</span></span> <span data-ttu-id="a5ad3-180">Sie können die Option "Unterwebsite erstellen" in der folgenden Abbildung sehen.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-180">You can see the "Subsite Creation" option in the following image.</span></span>

![Optionen zum Erstellen von SharePoint Online Administratorbenutzeroberfläche Unterwebsite](media/modern-experiences/subsite-creation-admin-setting.png)

### <a name="sites-are-not-listed-in-the-classic-sharepoint-admin-ui--tenant-api"></a><span data-ttu-id="a5ad3-182">Websites werden nicht in der klassischen SharePoint Admin-Benutzeroberfläche aufgeführt / Mandanten-API</span><span class="sxs-lookup"><span data-stu-id="a5ad3-182">Sites are not listed in the classic SharePoint Admin UI / Tenant API</span></span>

<span data-ttu-id="a5ad3-183">"Modernen" Teamwebsites werden nicht in der SharePoint-Admin-Benutzeroberfläche angezeigt.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-183">"Modern" team sites are not visible in the SharePoint admin UI.</span></span> <span data-ttu-id="a5ad3-184">Sie können die Liste der "modernen" Teamwebsites aus der Admin-Benutzeroberfläche von Office 365 Gruppen unter Office 365-Verwaltungsportal zugreifen.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-184">You can access the list of "modern" team sites from the Office 365 Groups admin user interface under Office 365 admin portal.</span></span> <span data-ttu-id="a5ad3-185">SharePoint Online Admin-Benutzeroberfläche nur Listen "klassische" SharePoint-Websites.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-185">SharePoint Online admin user interface only list "classic" SharePoint sites.</span></span> <span data-ttu-id="a5ad3-186">Dieselbe Einschränkung gilt nicht für den Mandanten API: Sie können diese API verwenden, um "modernen" Teamwebsites zusammen mit "klassische" Teamwebsites aufgelistet werden.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-186">This same limitation does not apply to the tenant API: you can use this API to enumerate "modern" team sites together with "classic" team sites.</span></span> <span data-ttu-id="a5ad3-187">Zum Abrufen einer Liste von nur "modernen" Teamwebsites können Sie auch den Endpunkt Gruppen von Microsoft Graph-API verwenden.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-187">To obtain a list of only "modern" team sites you can also use the Groups endpoint from Microsoft Graph API.</span></span>

<span data-ttu-id="a5ad3-188">Es gibt auch eine anstehende neue SharePoint Admin-Benutzeroberfläche, die Verwaltung von der neuen "modernen" Websitesammlungen zusammen mit "klassischen" diejenigen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="a5ad3-188">There is also an upcoming new SharePoint Admin UI, which supports managing the new "modern" site collections, together with the "classic" ones.</span></span>

## <a name="see-also"></a><span data-ttu-id="a5ad3-189">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="a5ad3-189">See also</span></span>

- [<span data-ttu-id="a5ad3-190">Anpassen der „modernen“ Benutzeroberflächen in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="a5ad3-190">Customizing the "modern" experiences in SharePoint Online</span></span>](modern-experience-customizations.md)
- [<span data-ttu-id="a5ad3-191">Was ist eine SharePoint-Teamwebsite?</span><span class="sxs-lookup"><span data-stu-id="a5ad3-191">What is a SharePoint team site?</span></span>](https://support.office.com/en-US/article/What-is-a-SharePoint-team-site-75545757-36c3-46a7-beed-0aaa74f0401e?ui=en-US&rs=en-US&ad=US)
- [<span data-ttu-id="a5ad3-192">Erstellen einer Teamwebsite in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="a5ad3-192">Create a team site in SharePoint Online</span></span>](https://support.office.com/en-US/article/Create-a-team-site-in-SharePoint-Online-ef10c1e7-15f3-42a3-98aa-b5972711777d)
- [<span data-ttu-id="a5ad3-193">Verwalten von websiteerstellung in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="a5ad3-193">Manage site creation in SharePoint Online</span></span>](https://support.office.com/en-us/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9?ui=en-US&rs=en-US&ad=US)
- [<span data-ttu-id="a5ad3-194">Verwalten Sie Ihrer SharePoint-Team-websiteeinstellungen</span><span class="sxs-lookup"><span data-stu-id="a5ad3-194">Manage your SharePoint team site settings</span></span>](https://support.office.com/en-us/article/Manage-your-SharePoint-team-site-settings-8376034d-d0c7-446e-9178-6ab51c58df42?ui=en-US&rs=en-US&ad=US)
