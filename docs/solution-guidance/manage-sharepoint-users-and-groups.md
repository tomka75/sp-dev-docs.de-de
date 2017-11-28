---
title: SharePoint-Benutzer und Gruppen verwalten
ms.date: 11/03/2017
ms.openlocfilehash: 9f287515faede9c92aa172c947f6b1826efc0fa1
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="manage-sharepoint-users-and-groups"></a><span data-ttu-id="882c0-102">SharePoint-Benutzer und Gruppen verwalten</span><span class="sxs-lookup"><span data-stu-id="882c0-102">Manage SharePoint users and groups</span></span>

<span data-ttu-id="882c0-103">Verwalten von Benutzern, Gruppen und Berechtigungen in einer SharePoint-Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="882c0-103">Manage users, groups, and permissions within a SharePoint site collection.</span></span> 

<span data-ttu-id="882c0-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="882c0-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="882c0-105">In diesem Artikel wird das Hinzufügen oder Entfernen von Gruppen und Benutzern innerhalb einer bestimmten Websitesammlung veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="882c0-105">This article shows you how to add or remove groups and users within a given site collection.</span></span> <span data-ttu-id="882c0-106">Die Codebeispiele in diesem Artikel Hinzufügen von Benutzern und Gruppen, und klicken Sie dann geben sie Berechtigungsstufen der Zugriff auf SharePoint.</span><span class="sxs-lookup"><span data-stu-id="882c0-106">The code examples in this article add users and groups, and then give them permission levels of access to SharePoint.</span></span> <span data-ttu-id="882c0-107">Diese Benutzer und Gruppe die Berechtigung Ebene Aktionen sind über Erweiterungsmethoden im [Core.GroupManagement](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.GroupManagement) Plug & Play-Beispiel implementiert.</span><span class="sxs-lookup"><span data-stu-id="882c0-107">These user and group permission level actions are implemented via extension methods in the [Core.GroupManagement](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.GroupManagement) PnP sample.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="882c0-108">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="882c0-108">Before you begin</span></span>

<span data-ttu-id="882c0-109">Laden Sie Sie zuerst [Core.GroupManagement](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.GroupManagement) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="882c0-109">To get started, download the [Core.GroupManagement](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.GroupManagement) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="add-and-remove-groups-and-users"></a><span data-ttu-id="882c0-110">Hinzufügen und Entfernen von Gruppen und Benutzern</span><span class="sxs-lookup"><span data-stu-id="882c0-110">Add and remove groups and users</span></span>

<span data-ttu-id="882c0-111">Im folgende Beispiel wird das Hinzufügen von Gruppen und Hinzufügen von Benutzern zu Gruppen veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="882c0-111">The following example shows you how to add groups and add users to groups.</span></span>

<span data-ttu-id="882c0-112">**Hinweis:**  Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="882c0-112">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="882c0-113">Im nächste Beispiel wird eine Gruppe entfernt.</span><span class="sxs-lookup"><span data-stu-id="882c0-113">The next example removes a group.</span></span>

```C#
if (cc.Web.GroupExists("Test"))
{
  cc.Web.RemoveGroup("Test");
}
```

<span data-ttu-id="882c0-114">Im nächste Beispiel werden Benutzer aus Gruppen entfernt.</span><span class="sxs-lookup"><span data-stu-id="882c0-114">The next example removes users from groups.</span></span>

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

## <a name="add-permission-level-to-group-or-user"></a><span data-ttu-id="882c0-115">Hinzufügen der Berechtigungsstufe zu Gruppen- oder Benutzernamen</span><span class="sxs-lookup"><span data-stu-id="882c0-115">Add permission level to group or user</span></span>

<span data-ttu-id="882c0-116">Das folgende Beispiel fügt eine Berechtigungsstufe zu einer Gruppe.</span><span class="sxs-lookup"><span data-stu-id="882c0-116">The following example adds a permission level to a group.</span></span>

```C#
if (cc.Web.GroupExists("Test"))
{
  cc.Web.AddPermissionLevelToGroup("Test", RoleType.Contributor);
}
```

<span data-ttu-id="882c0-117">Im nächste Beispiel fügt eine Berechtigungsstufe, die einem Benutzer.</span><span class="sxs-lookup"><span data-stu-id="882c0-117">The next example adds a permission level to a user.</span></span>

```C#
cc.Load(cc.Web, web => web.CurrentUser);
cc.ExecuteQuery();
Microsoft.SharePoint.Client.User currentUser = cc.Web.CurrentUser;
cc.Web.AddPermissionLevelToUser(currentUser.LoginName, RoleType.Reader);
```

## <a name="remove-permission-level-from-group-or-user"></a><span data-ttu-id="882c0-118">Berechtigungsstufe aus Gruppen- oder Benutzernamen entfernen</span><span class="sxs-lookup"><span data-stu-id="882c0-118">Remove permission level from group or user</span></span>

<span data-ttu-id="882c0-119">Das folgende Beispiel entfernt eine Berechtigungsstufe aus einer Gruppe.</span><span class="sxs-lookup"><span data-stu-id="882c0-119">The following example removes a permission level from a group.</span></span>

```C#
if (cc.Web.GroupExists("Test"))
{
  cc.Web.RemovePermissionLevelFromGroup("Test", RoleType.Reader);
}

```
<span data-ttu-id="882c0-120">Im nächste Beispiel entfernt eine Berechtigungsstufe von einem Benutzer.</span><span class="sxs-lookup"><span data-stu-id="882c0-120">The next example removes a permission level from a user.</span></span>

```C#
cc.Load(cc.Web, web => web.CurrentUser);
cc.ExecuteQuery();
Microsoft.SharePoint.Client.User currentUser = cc.Web.CurrentUser;
cc.Web.RemovePermissionLevelFromUser(currentUser.LoginName, RoleType.Reader);
```

## <a name="additional-resources"></a><span data-ttu-id="882c0-121">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="882c0-121">Additional resources</span></span>
<span data-ttu-id="882c0-122"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="882c0-122"></span></span>

- [<span data-ttu-id="882c0-123">SharePoint-Website Bereitstellen von Lösungen</span><span class="sxs-lookup"><span data-stu-id="882c0-123">SharePoint site provisioning solutions</span></span>](sharepoint-site-provisioning-solutions.md)
    
- [<span data-ttu-id="882c0-124">Branding und Bereitstellen von Lösungen für SharePoint 2013 und SharePoint Online-Website</span><span class="sxs-lookup"><span data-stu-id="882c0-124">Branding and site provisioning solutions for SharePoint 2013 and SharePoint Online</span></span>](Branding-and-site-provisioning-solutions-for-SharePoint.md)
