---
title: SharePoint-Benutzer und Gruppen verwalten
ms.date: 11/03/2017
ms.openlocfilehash: 06c47217b185aec190e818f1a67ce98cc5bbc63f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="manage-sharepoint-users-and-groups"></a>SharePoint-Benutzer und Gruppen verwalten

Verwalten von Benutzern, Gruppen und Berechtigungen in einer SharePoint-Websitesammlung. 

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

In diesem Artikel wird das Hinzufügen oder Entfernen von Gruppen und Benutzern innerhalb einer bestimmten Websitesammlung veranschaulicht. Die Codebeispiele in diesem Artikel Hinzufügen von Benutzern und Gruppen, und klicken Sie dann geben sie Berechtigungsstufen der Zugriff auf SharePoint. Diese Benutzer und Gruppe die Berechtigung Ebene Aktionen sind über Erweiterungsmethoden im [Core.GroupManagement](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.GroupManagement) Plug & Play-Beispiel implementiert.

## <a name="before-you-begin"></a>Bevor Sie beginnen:

Laden Sie Sie zuerst [Core.GroupManagement](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.GroupManagement) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

## <a name="add-and-remove-groups-and-users"></a>Hinzufügen und Entfernen von Gruppen und Benutzern

Im folgende Beispiel wird das Hinzufügen von Gruppen und Hinzufügen von Benutzern zu Gruppen veranschaulicht.

> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```C#
cc.Load(cc.Web, web => web.CurrentUser);
cc.ExecuteQuery();
Microsoft.SharePoint.Client.User currentUser = cc.Web.CurrentUser;

if (!cc.Web.GroupExists("Test"))
{
  Group group = cc.Web.AddGroup("Test", "Test group", true);
  cc.Web.AddUserToGroup("Test", currentUser.LoginName);
}
```

Im nächste Beispiel wird eine Gruppe entfernt.

```C#
if (cc.Web.GroupExists("Test"))
{
  cc.Web.RemoveGroup("Test");
}
```

Im nächste Beispiel werden Benutzer aus Gruppen entfernt.

```C#
cc.Load(cc.Web, web => web.CurrentUser);
cc.ExecuteQuery();
Microsoft.SharePoint.Client.User currentUser = cc.Web.CurrentUser;
if (cc.Web.GroupExists("Test"))
{
  if (cc.Web.IsUserInGroup("Test", currentUser.LoginName))
  {
    cc.Web.RemoveUserFromGroup("Test", currentUser.LoginName);
  }
}
```

## <a name="add-permission-level-to-group-or-user"></a>Hinzufügen der Berechtigungsstufe zu Gruppen- oder Benutzernamen

Das folgende Beispiel fügt eine Berechtigungsstufe zu einer Gruppe.

```C#
if (cc.Web.GroupExists("Test"))
{
  cc.Web.AddPermissionLevelToGroup("Test", RoleType.Contributor);
}
```

Im nächste Beispiel fügt eine Berechtigungsstufe, die einem Benutzer.

```C#
cc.Load(cc.Web, web => web.CurrentUser);
cc.ExecuteQuery();
Microsoft.SharePoint.Client.User currentUser = cc.Web.CurrentUser;
cc.Web.AddPermissionLevelToUser(currentUser.LoginName, RoleType.Reader);
```

## <a name="remove-permission-level-from-group-or-user"></a>Berechtigungsstufe aus Gruppen- oder Benutzernamen entfernen

Das folgende Beispiel entfernt eine Berechtigungsstufe aus einer Gruppe.

```C#
if (cc.Web.GroupExists("Test"))
{
  cc.Web.RemovePermissionLevelFromGroup("Test", RoleType.Reader);
}

```
Im nächste Beispiel entfernt eine Berechtigungsstufe von einem Benutzer.

```C#
cc.Load(cc.Web, web => web.CurrentUser);
cc.ExecuteQuery();
Microsoft.SharePoint.Client.User currentUser = cc.Web.CurrentUser;
cc.Web.RemovePermissionLevelFromUser(currentUser.LoginName, RoleType.Reader);
```

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

- [SharePoint-Website Bereitstellen von Lösungen](sharepoint-site-provisioning-solutions.md)
    
- [Branding und Bereitstellen von Lösungen für SharePoint 2013 und SharePoint Online-Website](Branding-and-site-provisioning-solutions-for-SharePoint.md)
