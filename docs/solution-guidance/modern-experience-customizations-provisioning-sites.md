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
# <a name="provisioning-modern-team-sites-programmatically"></a><span data-ttu-id="f8c9d-103">Bereitstellen von "modernen" Teamwebsites programmgesteuert</span><span class="sxs-lookup"><span data-stu-id="f8c9d-103">Provisioning "modern" team sites programmatically</span></span>

<span data-ttu-id="f8c9d-104">"Modernen" Teamwebsites in SharePoint Online in 2016 eingeführt wurden, und verwenden sie die Option auf der Ebene der Mandant gesteuert werden kann.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-104">"Modern" team sites were introduced in SharePoint Online in 2016, and the option to use them can be controlled at the tenant level.</span></span> <span data-ttu-id="f8c9d-105">In diesem Artikel werden die verschiedenen Optionen und Aspekte für die Bereitstellung von "modernen" Teamwebsites in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-105">This article discusses the different options and considerations for provisioning "modern" team sites in SharePoint Online.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8c9d-106">Wir sind nicht die "klassische" Erfahrung veralteter; "klassische" und "modernen" werden gleichzeitig verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-106">We're not deprecating the "classic" experience; both "classic" and "modern" will coexist.</span></span>

## <a name="provisioning-a-modern-team-site-from-the-user-interface"></a><span data-ttu-id="f8c9d-107">Bereitstellung einer "modernen" Teamwebsite aus der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="f8c9d-107">Provisioning a "modern" team site from the user interface</span></span>

<span data-ttu-id="f8c9d-108">Es gibt zahlreiche Routen für eine "modernen" Teamwebsite bereitgestellt erhalten möchten.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-108">There are numerous routes for a "modern" team site to get provisioned.</span></span> <span data-ttu-id="f8c9d-109">Sie können die Bereitstellung direkt über die SharePoint Online-Website starten, oder Sie können alternativ bereitstellen eine Office 365-Gruppe aus anderen Speicherorten (z. B. von Outlook), die auch dann löst die Bereitstellung einer "modernen" Team Site.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-109">You can start the provisioning directly from the SharePoint Online site, or alternatively provision an Office 365 group from other locations (for example, from Outlook), which then also triggers the provisioning of a "modern" team site.</span></span> 

- <span data-ttu-id="f8c9d-110">Wenn Ihr Administrator "modernen" Teamwebsites in Ihrem Mandanten aktiviert, können Sie der Homepage der SharePoint "modernen" Teamwebsites erstellen.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-110">If your administrator enabled "modern" team sites in your tenant, you can create "modern" team sites from the SharePoint home page.</span></span>

- <span data-ttu-id="f8c9d-111">Sie können auch eine Office 365-Gruppe von Office 365 Outlook erstellen, und wenn Sie auf die Registerkarte Standort der Gruppe zugreifen, sorgt auf einer Teamwebsite "modernen".</span><span class="sxs-lookup"><span data-stu-id="f8c9d-111">You can also create an Office 365 group from Office 365 Outlook, and when you access the site tab of that group, you land on a "modern" team site.</span></span> 

### <a name="control-default-provisioning-flow"></a><span data-ttu-id="f8c9d-112">Steuerelement-Standard Flow-Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="f8c9d-112">Control default provisioning flow</span></span>

<span data-ttu-id="f8c9d-113">Sie können die SharePoint-Website Erstellungsprozess SharePoint Online Admin Einstellungen steuern.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-113">You can control the SharePoint site creation process from the SharePoint Online Admin settings.</span></span> <span data-ttu-id="f8c9d-114">Sie können auswählen, wenn die Erfahrung "moderne" für die Endbenutzer verfügbar ist oder wenn Sie fortfahren möchten, verwenden die "klassische" Erfahrung.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-114">You can choose if the "modern" experience is available for your end users, or if you'd like to continue using the "classic" experience.</span></span> <span data-ttu-id="f8c9d-115">Weitere Informationen hierzu finden Sie unter [Manage Site Creation in SharePoint Online](https://support.office.com/en-US/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9).</span><span class="sxs-lookup"><span data-stu-id="f8c9d-115">For details, see [Manage site creation in SharePoint Online](https://support.office.com/en-US/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9).</span></span>

<span data-ttu-id="f8c9d-116">*Abbildung 1. Optionen zum Erstellen einer Website von SharePoint Online*</span><span class="sxs-lookup"><span data-stu-id="f8c9d-116">*Figure 1. Site creation options from SharePoint Online*</span></span>

![Optionen zum Erstellen einer Website aus der SharePoint Online-Admin-Benutzeroberfläche](media/modern-experiences/site-creation-options-admin-ui.png)


## <a name="provisioning-a-modern-team-site-programmatically"></a><span data-ttu-id="f8c9d-118">Bereitstellung einer Teamwebsite "modernen" programmgesteuert</span><span class="sxs-lookup"><span data-stu-id="f8c9d-118">Provisioning a "modern" team site programmatically</span></span>

<span data-ttu-id="f8c9d-119">"Modernen" Teamwebsites werden programmgesteuert durch Erstellen einer [Gruppe von Office 365](https://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/group) mit Microsoft Graph erstellt.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-119">"Modern" team sites are created programmatically by creating an [Office 365 group](https://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/group) using Microsoft Graph.</span></span> <span data-ttu-id="f8c9d-120">Wenn Sie eine Office 365-Gruppe erstellen, wird automatisch eine Teamwebsite "modernen" für die Gruppe bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-120">When you create an Office 365 group, a "modern" team site is automatically provisioned for the group.</span></span> <span data-ttu-id="f8c9d-121">Die "modernen" Teamwebsite URI basiert auf dem **MailNickname** -Parameter der Gruppe der Office 365 und verfügt über die folgenden standardmäßigen Struktur.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-121">The "modern" team site URI is based on the **mailNickname** parameter of the Office 365 group and has the following default structure.</span></span> 

```
https://[tenant].sharepoint.com/sites/[mailNickname]]
``` 

> [!NOTE]
> <span data-ttu-id="f8c9d-122">Eine ausführliche Beschreibung der Erstellung von Gruppen mithilfe von Microsoft Graph ist von der [offizielle Dokumentation](https://graph.microsoft.io/en-us/docs/api-reference/v1.0/api/group_post_groups)zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-122">A detailed description of group creation using Microsoft Graph is available from the [official documentation](https://graph.microsoft.io/en-us/docs/api-reference/v1.0/api/group_post_groups).</span></span>

### <a name="provision-a-modern-team-site-using-the-pnp-csom-core-component"></a><span data-ttu-id="f8c9d-123">Bereitstellen einer "modernen" Teamwebsite mithilfe der Plug & Play-CSOM-Core-Komponente</span><span class="sxs-lookup"><span data-stu-id="f8c9d-123">Provision a "modern" team site using the PnP CSOM Core component</span></span>

<span data-ttu-id="f8c9d-124">Die Plug & Play-CSOM-Core-Komponente als [NuGet-Paket](https://www.nuget.org/packages/SharePointPnPCoreOnline)wurde Methoden für den Umgang mit "modernen" Gruppe vereinfacht.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-124">The PnP CSOM Core component, available as a [NuGet package](https://www.nuget.org/packages/SharePointPnPCoreOnline), has simplified methods for the "modern" group handling.</span></span> 

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

### <a name="provision-a-modern-team-site-using-pnp-powershell"></a><span data-ttu-id="f8c9d-125">Bereitstellen einer "modernen" Teamwebsite von Plug & Play-PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8c9d-125">Provision a "modern" team site using PnP PowerShell</span></span>

<span data-ttu-id="f8c9d-126">Sie können auch "modernen" Websites erstellen, mithilfe von [Plug & Play-PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases), dem Sie die Authentifizierung auf einfache Weise mit Microsoft Graph mithilfe von Azure Active Directory können.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-126">You can also create "modern" sites by using [PnP PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases), which lets you easily authenticate with Microsoft Graph by using Azure Active Directory.</span></span> <span data-ttu-id="f8c9d-127">Das folgende Skript erstellt eine "modernen" Teamwebsite und gibt dann den aktuellen SharePoint-Website-URL zur weiteren Bearbeitung zurück.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-127">The following script creates a "modern" team site and then returns the actual SharePoint site URL for further manipulation.</span></span> <span data-ttu-id="f8c9d-128">Nachdem Sie den Zugriff auf die URL der Website erstellt haben, können Sie CSOM (mit SharePoint Plug & Play-Hauptkomponenten) oder Plug & Play-PowerShell für SharePoint verwenden, um anderer Vorgänge auf der erstellten Website zu automatisieren.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-128">After you have access to the URL of the created site, you can use CSOM (with the SharePoint PnP Core component) or SharePoint PnP PowerShell to automate other operations on the created site.</span></span>

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
> <span data-ttu-id="f8c9d-129">Derzeit wird nicht unterstützt "modernen" Teamwebsites mithilfe der [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588)bereit.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-129">There is currently no support to provision "modern" team sites by using the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="f8c9d-130">Zusätzliche Überlegungen</span><span class="sxs-lookup"><span data-stu-id="f8c9d-130">Additional considerations</span></span>

### <a name="subsites-use-classic-templates"></a><span data-ttu-id="f8c9d-131">Unterwebsites verwenden "klassische" Websitevorlagen</span><span class="sxs-lookup"><span data-stu-id="f8c9d-131">Subsites use "classic" templates</span></span>

<span data-ttu-id="f8c9d-132">Wenn Sie eine Unterwebsite unter der Stammwebsite einer Websitesammlung "modernen" bereitstellen, werden Unterwebsites "klassische" Vorlagen verwendet.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-132">If you provision a subsite under the root site of a "modern" site collection, subsites will use "classic" templates.</span></span> <span data-ttu-id="f8c9d-133">Derzeit sind keine "modernen" Unterwebsitevorlagen verfügbar.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-133">Currently, no "modern" subsite templates are available.</span></span> <span data-ttu-id="f8c9d-134">Eine Unterwebsite "klassische" für eine "modernen" Teamwebsite können von einer Seite "modernen" auf der Website erstellen und Aktualisieren der Seite Willkommen auf der neu erstellten Seite transformiert werden.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-134">You can transform a "classic" subsite to a "modern" team site by creating a "modern" page on the site and updating the welcome page to the newly created page.</span></span>  

### <a name="sites-are-not-listed-in-the-sharepoint-admin-ui--tenant-api"></a><span data-ttu-id="f8c9d-135">Websites werden nicht aufgeführt, in der SharePoint-Admin-Benutzeroberfläche / Mandanten-API</span><span class="sxs-lookup"><span data-stu-id="f8c9d-135">Sites are not listed in the SharePoint Admin UI / Tenant API</span></span>

<span data-ttu-id="f8c9d-136">"Modernen" Teamwebsites werden nicht in der SharePoint-Admin-Benutzeroberfläche angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-136">"Modern" team sites are not visible in the SharePoint Admin UI.</span></span> <span data-ttu-id="f8c9d-137">Sie können die Liste der "modernen" Teamwebsites von der Benutzeroberfläche von Office 365 Gruppen Admin unter der Office 365-Verwaltungsportals zugreifen.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-137">You can access the list of "modern" team sites from the Office 365 groups Admin user interface under the Office 365 Admin portal.</span></span> <span data-ttu-id="f8c9d-138">Die SharePoint Online-Admin-Benutzeroberfläche sind nur "klassische" SharePoint-Websites aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-138">The SharePoint Online Admin user interface only lists "classic" SharePoint sites.</span></span> <span data-ttu-id="f8c9d-139">Dieselbe Einschränkung gilt nicht für den Mandanten API; Diese API können zusammen mit "klassische" Teamwebsites "modernen" Teamwebsites aufgelistet werden.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-139">This same limitation does not apply to the tenant API; you can use this API to enumerate "modern" team sites together with "classic" team sites.</span></span> <span data-ttu-id="f8c9d-140">Um eine Liste der nur "modernen" Teamwebsites zu erhalten, können Sie die Gruppen-Endpunkt aus der Microsoft Graph-API verwenden.</span><span class="sxs-lookup"><span data-stu-id="f8c9d-140">To obtain a list of only "modern" team sites, you can use the Groups end point from the Microsoft Graph API.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f8c9d-141">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f8c9d-141">Additional resources</span></span>

- [<span data-ttu-id="f8c9d-142">Anpassen der „modernen“ Benutzeroberflächen in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f8c9d-142">Customizing the "modern" experiences in SharePoint Online</span></span>](modern-experience-customizations.md)
- [<span data-ttu-id="f8c9d-143">Was ist eine SharePoint-Teamwebsite?</span><span class="sxs-lookup"><span data-stu-id="f8c9d-143">What is a SharePoint team site?</span></span>](https://support.office.com/en-US/article/What-is-a-SharePoint-team-site-75545757-36c3-46a7-beed-0aaa74f0401e?ui=en-US&rs=en-US&ad=US)
- [<span data-ttu-id="f8c9d-144">Erstellen einer Teamwebsite in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f8c9d-144">Create a team site in SharePoint Online</span></span>](https://support.office.com/en-US/article/Create-a-team-site-in-SharePoint-Online-ef10c1e7-15f3-42a3-98aa-b5972711777d)
- [<span data-ttu-id="f8c9d-145">Verwalten von websiteerstellung in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f8c9d-145">Manage site creation in SharePoint Online</span></span>](https://support.office.com/en-us/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9?ui=en-US&rs=en-US&ad=US)
- [<span data-ttu-id="f8c9d-146">Verwalten Sie Ihrer SharePoint-Team-websiteeinstellungen</span><span class="sxs-lookup"><span data-stu-id="f8c9d-146">Manage your SharePoint team site settings</span></span>](https://support.office.com/en-us/article/Manage-your-SharePoint-team-site-settings-8376034d-d0c7-446e-9178-6ab51c58df42?ui=en-US&rs=en-US&ad=US)
