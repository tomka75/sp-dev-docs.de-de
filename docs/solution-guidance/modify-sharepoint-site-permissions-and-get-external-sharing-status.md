---
title: "Ändern Sie der Berechtigungen für SharePoint-Website und Abrufen Sie des Status für externe Freigabe"
ms.date: 11/03/2017
ms.openlocfilehash: 664db2cc6d314b24be417f009cd8b464bfd0a5cc
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="modify-sharepoint-site-permissions-and-get-external-sharing-status"></a>Ändern Sie der Berechtigungen für SharePoint-Website und Abrufen Sie des Status für externe Freigabe

Ändern Sie Eigenschaften der Websitesammlungs-Administratoren mithilfe von CSOM. Rufen Sie die externe Freigabe Status und externe Benutzer von einer Websitesammlung oder Mandanten.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

Im Beispiel [Core.SitePermissions](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SitePermissions) können Sie um die Websitesammlungs-Administratoren für jede Websitesammlung, einschließlich derjenigen für OneDrive for Business in Office 365-Mandanten zu ändern. Dieses Beispiel zeigt, auch so erhalten Sie externe Freigabe Status für Installationen von Office 365 mit mehreren Mandanten.

Verwenden eine Konsolenanwendung, Sie erstellen ein **ClientContext** -Objekt, wenn Sie Berechtigungen für Liste und/oder Administratoren ändern möchten, und externe Freigabe Status erhalten möchten. Sie erstellen auch registrierten Add-Ins mithilfe von OAuth-Token.

## <a name="before-you-begin"></a>Bevor Sie beginnen:

Laden Sie Sie zuerst [Core.SitePermissions](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SitePermissions) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

## <a name="work-with-site-collection-administrators"></a>Arbeiten Sie mit Websitesammlungs-Administratoren

Um die Administratoren einer Websitesammlung zu aktualisieren, müssen Sie ein Administrator für die Websitesammlung sein. Der erste Schritt besteht ein **ClientContext** -Objekt von einem Benutzer mit den richtigen Berechtigungen erstellt.

> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```C#
ClientContext cc = new AuthenticationManager().GetSharePointOnlineAuthenticatedContextTenant(String.Format("https://{0}.sharepoint.com/sites/{1}", tenantName, siteName), String.Format("{0}@{1}.onmicrosoft.com", userName, tenantName), password); 
```

Das **ClientContext** -Objekt können Sie Abrufen einer Liste der aktuellen Website Websitesammlungs-Administratoren oder aktualisieren die Websitesammlungs-Administratoren, wie im folgenden Beispiel dargestellt.

```C#
List<UserEntity> admins = cc.Web.GetAdministrators();

List<UserEntity> adminsToAdd = new List<UserEntity>();
adminsToAdd.Add(new UserEntity() { LoginName = "i:0#.f|membership|user@domain" });

cc.Web.AddAdministrators(adminsToAdd);

UserEntity adminToRemove = new UserEntity() { LoginName = "i:0#.f|membership|user@domain" };
cc.Web.RemoveAdministrator(adminToRemove);
```

Sie können die Website festlegen Websitesammlungs-Administratoren von Websitesammlungen, wo sind Sie nicht bereits ein Websitesammlungsadministrator, indem Sie ein **ClientContext** -Objekt mit einem registrierten add-in erstellen. Hier das **ClientContext** -Objekt ein OAuth-Token mit Berechtigungen auf Mandantenebene basiert.

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
Nachdem Sie das getan haben, können Sie den folgenden Code zum Abrufen eines **ClientContext** -Objekts für das add-in verwenden.

```C#
ClientContext cc = new AuthenticationManager().GetAppOnlyAuthenticatedContext("https://tenantname-my.sharepoint.com/personal/user2", "<your tenant realm>", "<appID>", "<appsecret>");
```

## <a name="work-with-external-sharing-office-365-mt-only"></a>Arbeiten Sie mit externen Webdiensten Freigabe (nur Office 365 MT)

Dieses Szenario veranschaulicht, wie zum Abrufen des externen sharing Status einer Websitesammlung, und rufen Sie eine Liste mit externen Benutzern für eine bestimmte Websitesammlung oder für den gesamten Mandanten. Da dies die Mandanten-CSOM-Bibliotheken erforderlich ist, müssen Sie eine **ClientContext** gegen die Mandanten-Admin-Websitesammlung erstellen. Das Benutzerkonto muss ein Administratorkonto eines Mandanten sein.

```C#
ClientContext ccTenant = new AuthenticationManager().GetSharePointOnlineAuthenticatedContextTenant(String.Format("https://{0}-admin.sharepoint.com/", tenantName), String.Format("{0}@{1}.onmicrosoft.com", userName, tenantName), password);
```

Nach der **ClientContext** bereit ist, können Sie den folgenden Code verwenden, um der externen sharing Status und eine Liste mit externen Benutzern zu erhalten.

```C#
ccTenant.Web.GetSharingCapabilitiesTenant(new Uri(String.Format("https://{0}.sharepoint.com/sites/{1}", tenantName, siteName)))

List<ExternalUserEntity> externalUsers = ccTenant.Web.GetExternalUsersForSiteTenant(new Uri(String.Format("https://{0}.sharepoint.com/sites/{1}", tenantName, siteName)));

List<ExternalUserEntity> externalUsers = ccTenant.Web.GetExternalUsersTenant();

```

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

- [SharePoint-Website Bereitstellen von Lösungen](sharepoint-site-provisioning-solutions.md)
    
- [Provisioning.Pages-Beispiel](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Provisioning.Pages)
