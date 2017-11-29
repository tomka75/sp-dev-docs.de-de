---
title: "Ändern Sie der Berechtigungen für SharePoint-Website und Abrufen Sie des Status für externe Freigabe"
ms.date: 11/03/2017
ms.openlocfilehash: 0edc0b386eef7330e6085a43c2956940e87cf778
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="modify-sharepoint-site-permissions-and-get-external-sharing-status"></a><span data-ttu-id="30467-102">Ändern Sie der Berechtigungen für SharePoint-Website und Abrufen Sie des Status für externe Freigabe</span><span class="sxs-lookup"><span data-stu-id="30467-102">Modify SharePoint site permissions and get external sharing status</span></span>

<span data-ttu-id="30467-103">Ändern Sie Eigenschaften der Websitesammlungs-Administratoren mithilfe von CSOM.</span><span class="sxs-lookup"><span data-stu-id="30467-103">Modify properties of site collection administrators by using CSOM.</span></span> <span data-ttu-id="30467-104">Rufen Sie die externe Freigabe Status und externe Benutzer von einer Websitesammlung oder Mandanten.</span><span class="sxs-lookup"><span data-stu-id="30467-104">Get the external sharing status and external users of a site collection or tenant.</span></span>

<span data-ttu-id="30467-105">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="30467-105">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="30467-106">Im Beispiel [Core.SitePermissions](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SitePermissions) können Sie um die Websitesammlungs-Administratoren für jede Websitesammlung, einschließlich derjenigen für OneDrive for Business in Office 365-Mandanten zu ändern.</span><span class="sxs-lookup"><span data-stu-id="30467-106">You can use the [Core.SitePermissions](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SitePermissions) sample to modify the site collection administrators on any site collection, including those for OneDrive for Business on Office 365 tenants.</span></span> <span data-ttu-id="30467-107">Dieses Beispiel zeigt, auch so erhalten Sie externe Freigabe Status für Installationen von Office 365 mit mehreren Mandanten.</span><span class="sxs-lookup"><span data-stu-id="30467-107">This sample also shows you how to obtain external sharing status for Office 365 Multi-Tenant installations.</span></span>

<span data-ttu-id="30467-108">Verwenden eine Konsolenanwendung, Sie erstellen ein **ClientContext** -Objekt, wenn Sie Berechtigungen für Liste und/oder Administratoren ändern möchten, und externe Freigabe Status erhalten möchten.</span><span class="sxs-lookup"><span data-stu-id="30467-108">Using a console application, you create a  **ClientContext** object to get permissions to list and/or modify administrators, and get external sharing status.</span></span> <span data-ttu-id="30467-109">Sie erstellen auch registrierten Add-Ins mithilfe von OAuth-Token.</span><span class="sxs-lookup"><span data-stu-id="30467-109">You also create a registered add-in by using OAuth tokens.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="30467-110">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="30467-110">Before you begin</span></span>

<span data-ttu-id="30467-111">Laden Sie Sie zuerst [Core.SitePermissions](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SitePermissions) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="30467-111">To get started, download the [Core.SitePermissions](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SitePermissions) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="work-with-site-collection-administrators"></a><span data-ttu-id="30467-112">Arbeiten Sie mit Websitesammlungs-Administratoren</span><span class="sxs-lookup"><span data-stu-id="30467-112">Work with site collection administrators</span></span>

<span data-ttu-id="30467-113">Um die Administratoren einer Websitesammlung zu aktualisieren, müssen Sie ein Administrator für die Websitesammlung sein.</span><span class="sxs-lookup"><span data-stu-id="30467-113">To update the administrators of a site collection, you must be an administrator for the site collection.</span></span> <span data-ttu-id="30467-114">Der erste Schritt besteht ein **ClientContext** -Objekt von einem Benutzer mit den richtigen Berechtigungen erstellt.</span><span class="sxs-lookup"><span data-stu-id="30467-114">The first step is to create a  **ClientContext** object by a user with the right permissions.</span></span>

<span data-ttu-id="30467-115">**Hinweis:**  Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="30467-115">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
ClientContext cc = new AuthenticationManager().GetSharePointOnlineAuthenticatedContextTenant(String.Format("https://{0}.sharepoint.com/sites/{1}", tenantName, siteName), String.Format("{0}@{1}.onmicrosoft.com", userName, tenantName), password); 
```

<span data-ttu-id="30467-116">Das **ClientContext** -Objekt können Sie Abrufen einer Liste der aktuellen Website Websitesammlungs-Administratoren oder aktualisieren die Websitesammlungs-Administratoren, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="30467-116">Using the  **ClientContext** object, you can get a list of the current site collection administrators or update the site collection administrators, as shown in the following example.</span></span>

```C#
List<UserEntity> admins = cc.Web.GetAdministrators();

List<UserEntity> adminsToAdd = new List<UserEntity>();
adminsToAdd.Add(new UserEntity() { LoginName = "i:0#.f|membership|user@domain" });

cc.Web.AddAdministrators(adminsToAdd);

UserEntity adminToRemove = new UserEntity() { LoginName = "i:0#.f|membership|user@domain" };
cc.Web.RemoveAdministrator(adminToRemove);
```

<span data-ttu-id="30467-117">Sie können die Website festlegen Websitesammlungs-Administratoren von Websitesammlungen, wo sind Sie nicht bereits ein Websitesammlungsadministrator, indem Sie ein **ClientContext** -Objekt mit einem registrierten add-in erstellen.</span><span class="sxs-lookup"><span data-stu-id="30467-117">You can set the site collection administrators for site collections where you're not already a site collection administrator by creating a  **ClientContext** object using a registered add-in.</span></span> <span data-ttu-id="30467-118">Hier das **ClientContext** -Objekt ein OAuth-Token mit Berechtigungen auf Mandantenebene basiert.</span><span class="sxs-lookup"><span data-stu-id="30467-118">Here, the **ClientContext** object is based on an OAuth token with tenant-level permissions.</span></span>

```C#
// Use (Get-MsolCompanyInformation).ObjectID to obtain Target/Tenant realm: <guid>
//
// Manually register an add-in via the appregnew.aspx page and generate an add-in ID and 
// add-in secret. The add-in title and add-in domain can be a simple string like "MyAddin".
//
// Update the add-in ID in your worker role settings.
//
// Add the add-in secret in your worker role settings. 
//
// Manually set the permission XML for you add-in via the appinv.aspx page:
// 1. Look up your add-in via its add-in ID.
// 2. Paste the permission XML and choose create.
//
// Sample permission XML:
// <AppPermissionRequests AllowAppOnlyPolicy="true">
//   <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
// </AppPermissionRequests>
//
// Because you're granting tenant-wide full control to an add-in, the add-in secret is as important
// as the password from your SharePoint administration account.
```
<span data-ttu-id="30467-119">Nachdem Sie das getan haben, können Sie den folgenden Code zum Abrufen eines **ClientContext** -Objekts für das add-in verwenden.</span><span class="sxs-lookup"><span data-stu-id="30467-119">After you've done that, you can use the following code to obtain a  **ClientContext** object for this add-in.</span></span>

```C#
ClientContext cc = new AuthenticationManager().GetAppOnlyAuthenticatedContext("https://tenantname-my.sharepoint.com/personal/user2", "<your tenant realm>", "<appID>", "<appsecret>");
```

## <a name="work-with-external-sharing-office-365-mt-only"></a><span data-ttu-id="30467-120">Arbeiten Sie mit externen Webdiensten Freigabe (nur Office 365 MT)</span><span class="sxs-lookup"><span data-stu-id="30467-120">Work with external sharing (Office 365 MT only)</span></span>

<span data-ttu-id="30467-121">Dieses Szenario veranschaulicht, wie zum Abrufen des externen sharing Status einer Websitesammlung, und rufen Sie eine Liste mit externen Benutzern für eine bestimmte Websitesammlung oder für den gesamten Mandanten.</span><span class="sxs-lookup"><span data-stu-id="30467-121">This scenario shows how to get the external sharing status of a site collection, and get a list of external users for a specific site collection or for the whole tenant.</span></span> <span data-ttu-id="30467-122">Da dies die Mandanten-CSOM-Bibliotheken erforderlich ist, müssen Sie eine **ClientContext** gegen die Mandanten-Admin-Websitesammlung erstellen.</span><span class="sxs-lookup"><span data-stu-id="30467-122">Because this requires the tenant CSOM libraries, you need to create a  **ClientContext** against the tenant admin site collection.</span></span> <span data-ttu-id="30467-123">Das Benutzerkonto muss ein Administratorkonto eines Mandanten sein.</span><span class="sxs-lookup"><span data-stu-id="30467-123">The user account has to be a tenant administrator account.</span></span>

```C#
ClientContext ccTenant = new AuthenticationManager().GetSharePointOnlineAuthenticatedContextTenant(String.Format("https://{0}-admin.sharepoint.com/", tenantName), String.Format("{0}@{1}.onmicrosoft.com", userName, tenantName), password);
```

<span data-ttu-id="30467-124">Nach der **ClientContext** bereit ist, können Sie den folgenden Code verwenden, um der externen sharing Status und eine Liste mit externen Benutzern zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="30467-124">After the  **ClientContext** is ready, you can use the following code to get the external sharing status and a list of external users.</span></span>

```C#
ccTenant.Web.GetSharingCapabilitiesTenant(new Uri(String.Format("https://{0}.sharepoint.com/sites/{1}", tenantName, siteName)))

List<ExternalUserEntity> externalUsers = ccTenant.Web.GetExternalUsersForSiteTenant(new Uri(String.Format("https://{0}.sharepoint.com/sites/{1}", tenantName, siteName)));

List<ExternalUserEntity> externalUsers = ccTenant.Web.GetExternalUsersTenant();

```

## <a name="additional-resources"></a><span data-ttu-id="30467-125">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="30467-125">Additional resources</span></span>
<span data-ttu-id="30467-126"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="30467-126"></span></span>

- [<span data-ttu-id="30467-127">SharePoint-Website Bereitstellen von Lösungen</span><span class="sxs-lookup"><span data-stu-id="30467-127">SharePoint site provisioning solutions</span></span>](sharepoint-site-provisioning-solutions.md)
    
- [<span data-ttu-id="30467-128">Provisioning.Pages-Beispiel</span><span class="sxs-lookup"><span data-stu-id="30467-128">Provisioning.Pages sample</span></span>](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Provisioning.Pages)
