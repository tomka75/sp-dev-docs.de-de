---
title: "Rolle, Vererbung, Erhöhung von Berechtigungen und Kennwortänderungen in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 07ff58f15255bdb924b3ccc14877056c64d65172
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="role-inheritance-elevation-of-privilege-and-password-changes-in-sharepoint"></a><span data-ttu-id="3ea9b-102">Rolle, Vererbung, Erhöhung von Berechtigungen und Kennwortänderungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ea9b-102">Role, inheritance, elevation of privilege, and password changes in SharePoint</span></span>

## <a name="roles-role-definitions-and-role-assignments"></a><span data-ttu-id="3ea9b-103">Rollen, Rollendefinitionen und rollenzuweisungen</span><span class="sxs-lookup"><span data-stu-id="3ea9b-103">Roles, role definitions, and role assignments</span></span>
<span data-ttu-id="3ea9b-104"><a name="SP15_RoleInheritance_Role"> </a></span><span class="sxs-lookup"><span data-stu-id="3ea9b-104"><a name="SP15_RoleInheritance_Role"> </a></span></span>

<span data-ttu-id="3ea9b-105">Eine Rolle besteht aus zwei Teilen: einer Rollendefinition und einer Rollenzuweisung.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-105">A role consists of two parts: a role definition and a role assignment.</span></span> 
  
    
    
<span data-ttu-id="3ea9b-p101">Die Rollendefinition oder Berechtigungsstufe, um die Liste der Rechte der Rolle zugeordnet. Ein Recht ist ein eindeutig gesteuert Aktion innerhalb einer SharePoint-Website. Beispielsweise kann ein Benutzer mit der Rolle **Read** Seiten in der Website und Ansicht Elemente in Listen wechseln. Benutzerberechtigungen werden niemals direkt mithilfe der Verwaltung von Informationsrechten verwaltet. Über Rollen werden alle Benutzer- und Gruppenkonten verwaltet. Eine Rollendefinition ist eine Auflistung der Rechte für ein bestimmtes Objekt gebunden. Rollendefinitionen (z. B. **Full Control**, **Read**, **Contribute**, **Design**oder **Limited Access**) sind bezogen auf der Website und die dieselbe Bedeutung überall innerhalb der Website, deren Bedeutung können unterscheiden sich jedoch zwischen Websites innerhalb der gleichen Websitesammlung befindet. Von der übergeordneten Website können auch Rollendefinitionen geerbt werden, wie Berechtigungen vererbt werden können.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p101">The role definition, or permission level, is the list of rights associated with the role. A right is a uniquely controllable action within a SharePoint website. For example, a user with the **Read** role can browse pages in the website and view items in lists. User permissions are never managed directly by using rights. All user and group permissions are managed through roles. A role definition is a collection of rights bound to a specific object. Role definitions (for example, **Full Control**, **Read**, **Contribute**, **Design**, or **Limited Access**) are scoped to the website and mean the same thing everywhere within the website, but their meanings can differ between sites within the same site collection. Role definitions can also be inherited from the parent website, just as permissions can be inherited.</span></span> 
  
    
    
<span data-ttu-id="3ea9b-p102">Die rollenzuweisung wird die Beziehung zwischen der Rollendefinition, die Benutzer und Gruppen und den Bereich (beispielsweise ein Benutzer möglicherweise ein Leser in Liste 1, während ein anderer Benutzer ein Leser in Liste 2 ist). Die Beziehung ausgedrückt durch die rollenzuweisung ist der Schlüssel vornehmen, rollenbasierte SharePoint Security Management. Alle Berechtigungen sind über Rollen verwaltet. Sie weisen nie Rechte direkt für einen Benutzer. Sie weisen nur sinnvolle Auflistungen der Rechte (Rollendefinitionen), die gut definiert und konsistent sind. Verwalten Sie eindeutige Berechtigungen durch Hinzufügen oder Entfernen von Benutzern und Gruppen zu oder von Rollendefinitionen über rollenzuweisungen.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p102">The role assignment is the relationship among the role definition, the users and groups, and the scope (for example, one user may be a reader on list 1, while another user is a reader on list 2). The relationship expressed through the role assignment is the key to making SharePoint security management role-based. All permissions are managed through roles; you never assign rights directly to a user. You assign only meaningful collections of rights (role definitions) that are well-defined and consistent. You manage unique permissions by adding or removing users and groups to or from role definitions through role assignments.</span></span>
  
    
    
<span data-ttu-id="3ea9b-119">Der Websiteadministrator kann die standardmäßigen Rollendefinitionen anpassen und zusätzliche benutzerdefinierte Rollen mithilfe der Seite Rollen verwalten erstellen, auf der die verfügbaren Rollendefinitionen der Website aufgelistet sind.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-119">The website administrator can customize the default role definitions and create additional custom roles by using the Manage Roles page, which lists the available role definitions in the site.</span></span>
  
    
    

## <a name="role-definition-inheritance"></a><span data-ttu-id="3ea9b-120">Vererbung von Rollendefinitionen</span><span class="sxs-lookup"><span data-stu-id="3ea9b-120">Role definition inheritance</span></span>
<span data-ttu-id="3ea9b-121"><a name="SP15_RoleInheritance_RoleDefInheritance"> </a></span><span class="sxs-lookup"><span data-stu-id="3ea9b-121"><a name="SP15_RoleInheritance_RoleDefInheritance"> </a></span></span>

<span data-ttu-id="3ea9b-122">SharePoint unterstützt erbende Rollendefinitionen auf ähnliche Weise, wie es unterstützt Vererbung von Berechtigungen und Vererbung von Rollendefinitionen Knacken erfordert auch Unterbrechen der Vererbung von Berechtigungen.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-122">SharePoint supports inheriting role definitions similarly to how it supports inheriting permissions, and breaking role definition inheritance requires also breaking permissions inheritance.</span></span>
  
    
    
<span data-ttu-id="3ea9b-p103">Jeder SharePoint-Objekt kann haben einen eigenen Satz von Berechtigungen oder erben die Berechtigungen von seinem übergeordneten Container. SharePoint unterstützt keine teilweise Vererbung, in dem ein Objekt alle Berechtigungen des übergeordneten Objekts erben und auch einige eigene Berechtigungen haben. Die Berechtigungen sind entweder eigene oder vererbte. gesteuerte Vererbung unterstützt SharePoint nicht. Ein Objekt kann beispielsweise nur von seinem übergeordneten Container, nicht von einem anderen Objekt oder Container erben.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p103">Each SharePoint object can have its own set of permissions or inherit its permissions from its parent container. SharePoint does not support partial inheritance, where an object would inherit all the permissions of its parent and also have some of its own permissions. Permissions are either unique or inherited. SharePoint does not support directed inheritance. For example, an object can inherit only from its parent container, not from some other object or container.</span></span>
  
    
    
<span data-ttu-id="3ea9b-p104">Wenn eine Website Rollendefinitionen erbt, sind die Rollen schreibgeschützt - genauso wie die schreibgeschützten Berechtigungen in einer geerbten Website. Der Benutzer kann über einen Link zur übergeordneten Website navigieren, die die spezifischen Rollendefinitionen enthält. Die Standardeinstellung für alle neuen Websites, und zwar auch für Websites mit spezifischen Berechtigungen, sieht vor, dass Rollendefinitionen von der übergeordneten Website geerbt werden. Wenn die Berechtigungen websitespezifisch sind, können Rollendefinitionen auf geerbte Rollendefinitionen zurückgesetzt oder als lokale Rollendefinitionen bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p104">When a website inherits role definitions, the roles are read-only, like the read-only permissions in an inherited website. The user can navigate to the parent site that holds the unique role definitions via a link. The default setting for all new websites, even sites with unique permissions, is to inherit role definitions from the parent website. When the permissions are unique, role definitions can be reverted to inherited role definitions or edited as local role definitions.</span></span>
  
    
    
<span data-ttu-id="3ea9b-132">Vererbung von Rollendefinitionen in einer Website wirkt sich auf die Vererbung von Berechtigungen folgenden Regeln:</span><span class="sxs-lookup"><span data-stu-id="3ea9b-132">Role definition inheritance in a website affects permissions inheritance following these rules:</span></span>
  
    
    

- <span data-ttu-id="3ea9b-133">Das Erben von Berechtigungen ist nur möglich, wenn auch Rollendefinitionen geerbt werden.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-133">Cannot inherit permissions unless it also inherits role definitions.</span></span>
    
  
- <span data-ttu-id="3ea9b-134">Das Erstellen spezifischer Rollendefinitionen ist nur möglich, wenn auch spezifische Berechtigungen erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-134">Cannot create unique role definitions unless it also creates unique permissions.</span></span>
    
  
- <span data-ttu-id="3ea9b-p105">Das Zurücksetzen auf geerbte Rollendefinitionen ist nur möglich, wenn alle spezifischen Berechtigungen innerhalb der Website zurückgesetzt werden. Die vorhandenen Berechtigungen sind abhängig von den Rollendefinitionen.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p105">Cannot revert to inherited role definitions unless it also reverts all unique permissions within the website. The existing permissions are dependent on the role definitions.</span></span>
    
  
- <span data-ttu-id="3ea9b-p106">Das Zurücksetzen auf geerbte Berechtigungen ist nur möglich, wenn auch eine Zurücksetzung auf geerbte Rollendefinitionen erfolgt. Die Berechtigungen für eine Website sind immer an die Rollendefinitionen für diese Website geknüpft.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p106">Cannot revert to inherited permissions unless it also reverts to inherited role definitions. The permissions for a website are always tied to the role definitions for that website.</span></span>
    
  

## <a name="managing-user-tokens"></a><span data-ttu-id="3ea9b-139">Verwalten von Benutzertoken</span><span class="sxs-lookup"><span data-stu-id="3ea9b-139">Managing user tokens</span></span>
<span data-ttu-id="3ea9b-140"><a name="SP15_RoleInheritance_ManagingUserTokens"> </a></span><span class="sxs-lookup"><span data-stu-id="3ea9b-140"><a name="SP15_RoleInheritance_ManagingUserTokens"> </a></span></span>

<span data-ttu-id="3ea9b-p107">SharePoint ruft Benutzertokeninformationen aus der SharePoint-Datenbank ab. Wenn der Benutzer die Website noch nie besucht hat oder das Benutzertoken vor mehr als 24 Stunden generiert wurde, erzeugt SharePoint ein neues Benutzertoken. Hierzu wird versucht, die Liste der Gruppen zu aktualisieren, denen der Benutzer angehört.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p107">SharePoint fetches user token information from the SharePoint database. If the user has never visited the site or if the user's token was generated more than 24 hours previously, SharePoint generates a new user token by trying to refresh the list of groups that the user belongs to.</span></span> 
  
    
    
<span data-ttu-id="3ea9b-p108">Wenn es sich bei dem Benutzerkonto um ein NT-Konto handelt, verwendet SharePoint die **AuthZ**-Schnittstelle, um im Active Directory-Verzeichnisdienst eine Abfrage nach der **TokenGroups**-Eigenschaft durchzuführen. Hierbei können Fehler auftreten, wenn SharePoint im Extranetmodus ausgeführt wird und nicht über die Berechtigung zum Abfragen von Active Directory nach dieser Eigenschaft verfügt.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p108">If the user account is an NT account, SharePoint uses the **AuthZ** interface to query the Active Directory directory service for the **TokenGroups** property. This may fail if SharePoint is running in an extranet mode, and does not have permission to query Active Directory for this property.</span></span>
  
    
    
<span data-ttu-id="3ea9b-p109">Wenn das Benutzerkonto ein Mitgliedschaftsbenutzer ist, fragt SharePoint die ASP.NET **RoleManager** für alle Rollen, denen der Benutzer angehört. Dies kann fehlschlagen, wenn eine ordnungsgemäße .config-Datei für die aktuelle ausführbare Datei nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p109">If the user account is a membership user, SharePoint queries the ASP.NET **RoleManager** for all the roles that the user belongs to. This may fail if there is not a proper .config file for the current executable file.</span></span>
  
    
    
<span data-ttu-id="3ea9b-p110">Wenn SharePoint Gruppenmitgliedschaften des Benutzers aus Active Directory oder **<roleManager>**erhalten kann, enthält das neu generierte Token nur der Benutzer eindeutige Sicherheits-ID (SID). Wird keine Ausnahme ausgelöst, aber ein Eintrag in der Server-ULS-Protokoll geschrieben wird. Das neue Token wird auch in der SharePoint-Datenbank geschrieben, damit es nicht innerhalb von 24 Stunden wiederhergestellt wird.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p110">If SharePoint can't obtain the user's group memberships from Active Directory or **<roleManager>**, the newly generated token contains only the user's unique security ID (SID). No exception is thrown, but an entry is written into the ULS server log. The new token is also written into the SharePoint database so that it will not be regenerated within 24 hours.</span></span>
  
    
    
<span data-ttu-id="3ea9b-p111">Nach SharePoint ein aktuell Token aus der SharePoint-Datenbank oder durch Generieren eines neuen Tokens erhält, SharePoint den Zeitstempel der aktuellen Zeit werden festgelegt und dann an den Aufrufer zurückgegeben wird. Dadurch wird sichergestellt, dass das Token 24 Stunden aktuell ist.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p111">After SharePoint obtains a fresh token, from the SharePoint database or by generating a new token, SharePoint sets the timestamp to be the current time and then returns it to the caller. This guarantees that the token is fresh for 24 hours.</span></span>
  
    
    
<span data-ttu-id="3ea9b-p112">Nachdem das  [SPUserToken](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPUserToken.aspx) -Objekt an den Anrufer zurückgegeben wurde, ist es des Anrufers Verantwortung Token nicht zu verwenden, nachdem es abgelaufen ist. Sie können ein Hilfsprogramm nachverfolgen möchten den Ablauf des token Aufzeichnung der Zeit, wenn Sie das Token abrufen, schreiben und Vergleichen der Diff mit aktuellen Zeit vor [SPWebService.TokenTimeout](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPWebService.TokenTimeout.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p112">After the  [SPUserToken](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPUserToken.aspx) object is returned to the caller, it is the caller's responsibility to not use the token after it is expired. You can write a helper utility to track the token expiration by recording the time when you get the token, and compare the diff with current time against [SPWebService.TokenTimeout](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPWebService.TokenTimeout.aspx) .</span></span>
  
    
    
<span data-ttu-id="3ea9b-p113">Wenn ein abgelaufene Token zum Erstellen einer SharePoint-Website verwendet wird, wird eine Ausnahme ausgelöst. Der Standardwert token-Timeout ist 24 Stunden. Es kann über  [SPWebService.TokenTimeout](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPWebService.TokenTimeout.aspx) zugegriffen werden.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p113">If an expired token is used to create a SharePoint website, an exception is thrown. The default token timeout value is 24 hours. It can be accessed via  [SPWebService.TokenTimeout](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPWebService.TokenTimeout.aspx) .</span></span>
  
    
    

## <a name="elevation-of-privilege"></a><span data-ttu-id="3ea9b-157">Erhöhung von Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="3ea9b-157">Elevation of privilege</span></span>
<span data-ttu-id="3ea9b-158"><a name="SP15_RoleInheritance_ElevationOfPrivilege"> </a></span><span class="sxs-lookup"><span data-stu-id="3ea9b-158"><a name="SP15_RoleInheritance_ElevationOfPrivilege"> </a></span></span>

<span data-ttu-id="3ea9b-p114">Mithilfe von Rechteerweiterungen, einem in Windows SharePoint Services 3.0 neu eingeführten Feature, können Sie programmgesteuert Aktionen im Code mit einer höheren Berechtigungsstufe ausführen. Mit der  [SPSecurity.RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) -Methode kann ein Delegat bereitgestellt werden, von dem eine Teilmenge des Codes im Kontext eines Kontos mit höheren Berechtigungen als denen des aktuellen Benutzers ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p114">Elevation of privilege, a feature that was added in Windows SharePoint Services 3.0, enables you to programmatically perform actions in code by using an increased level of privilege. The  [SPSecurity.RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) method enables you to supply a delegate that runs a subset of code in the context of an account with higher privileges than the current user.</span></span>
  
    
    
<span data-ttu-id="3ea9b-161">Es folgt eine standardmäßige Verwendung von **RunWithElevatedPrivileges**.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-161">The following is a standard use of **RunWithElevatedPrivileges**.</span></span>
  
    
    



```cs

SPSecurity.RunWithElevatedPrivileges(delegate()
{
    // Do things by assuming the permission of the "system account".
});
```

<span data-ttu-id="3ea9b-p115">Häufig müssen Sie zum Ausführen von Aktionen in SharePoint ein neues  [SPSite](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSite.aspx) -Objekt abrufen, durch das die Änderungen bewirkt werden. Ein Beispiel:</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p115">Frequently, to perform actions in SharePoint, you must get a new  [SPSite](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSite.aspx) object to effect the changes. For example:</span></span>
  
    
    



```cs

SPSecurity.RunWithElevatedPrivileges(delegate()
{
    using (SPSite site = new SPSite(web.Site.ID))
    {
       // Do things by assuming the permission of the "system account".
    }
});
```

<span data-ttu-id="3ea9b-p116">Obwohl rechteerweiterungen eine leistungsstarke Technik zum Verwalten der Sicherheit bietet, sollten sie mit Vorsicht verwendet werden. Sie sollten keine direkte Schäden, nicht gesteuerte Mechanismen für Personen mit niedrigen Berechtigungen, die Ihnen erteilten Berechtigungen zu umgehen verfügbar machen.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p116">Although elevation of privilege provides a powerful technique for managing security, it should be used with care. You should not expose direct, uncontrolled mechanisms for people with low privileges to circumvent the permissions granted to them.</span></span>
  
    
    

> <span data-ttu-id="3ea9b-166">**Wichtig:** Wenn die an  [RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) übergebene Methode Schreibvorgänge beinhaltet, sollte vor dem Aufruf von [RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) ein Aufruf von [SPUtility.ValidateFormDigest()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPUtility.ValidateFormDigest.aspx) oder [SPWeb.ValidateFormDigest()](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.ValidateFormDigest.aspx) erfolgen.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-166">**Important:** If the method passed to  [RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) includes any write operations, the call to [RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) should be preceded by a call to either [SPUtility.ValidateFormDigest()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPUtility.ValidateFormDigest.aspx) or [SPWeb.ValidateFormDigest()](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.ValidateFormDigest.aspx) .</span></span>
  
    
    


## <a name="automatic-password-changes"></a><span data-ttu-id="3ea9b-167">Automatische Kennwortänderung</span><span class="sxs-lookup"><span data-stu-id="3ea9b-167">Automatic password changes</span></span>
<span data-ttu-id="3ea9b-168"><a name="SP15_RoleInheritance_AutomaticPasswordChange"> </a></span><span class="sxs-lookup"><span data-stu-id="3ea9b-168"><a name="SP15_RoleInheritance_AutomaticPasswordChange"> </a></span></span>

<span data-ttu-id="3ea9b-p117">Features für die automatische kennwortänderung können Sie aktualisieren und Bereitstellen von Kennwörtern ohne manuelle Kennwort Updateaufgaben für mehrere Konten, Dienste und Webanwendungen. Dadurch wird das Verwalten von Kennwort in SharePoint einfacher. Features für die automatische kennwortänderung können Sie bestimmen, ob ein Kennwort Testzeitraum und das Kennwort zurücksetzen können mithilfe von eine lange, kryptografisch starke zufällige Zeichenfolge ist.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p117">The automatic password change feature enables you to update and deploy passwords without performing manual password update tasks across multiple accounts, services, and web applications. This makes managing password in SharePoint simpler. You can use the automatic password change feature to determine whether a password is about to expire and to reset the password by using a long, cryptographically strong random string.</span></span>
  
    
    

### <a name="managed-account"></a><span data-ttu-id="3ea9b-172">Verwaltete Konten</span><span class="sxs-lookup"><span data-stu-id="3ea9b-172">Managed account</span></span>

<span data-ttu-id="3ea9b-p118">Verwenden Sie verwaltete Konten, um Features für die automatische kennwortänderung implementieren. Verwaltete Konten erhöhen der Sicherheit und Anwendungsisolation sicherzustellen. Mit verwalteten Konten können Sie folgende Aktionen ausführen:</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p118">You use managed accounts to implement the automatic password change feature. Managed accounts improve security and ensure application isolation. With managed accounts, you can:</span></span>
  
    
    

- <span data-ttu-id="3ea9b-176">Konfigurieren von Features für die automatische kennwortänderung zum Bereitstellen von Kennwörtern in allen Diensten in einer Farm.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-176">Configure the automatic password change feature to deploy passwords across all services in a farm.</span></span>
    
  
- <span data-ttu-id="3ea9b-177">Konfigurieren von SharePoint-Webanwendungen und -Diensten, die auf Anwendungsservern in einer SharePoint-Farm ausgeführt werden, sodass sie verschiedene Domänenkonten verwenden.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-177">Configure SharePoint web applications and services, that are running on application servers in a SharePoint farm, to use different domain accounts.</span></span>
    
  
- <span data-ttu-id="3ea9b-178">Zuordnen von verwalteten Konten zu verschiedenen Diensten und Webanwendungen in einer Farm.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-178">Map managed accounts to various services and web applications in a farm.</span></span>
    
  
- <span data-ttu-id="3ea9b-179">Erstellen Sie mehrerer Konten in Active Directory-Domänendienste (AD DS) und anschließendes registrieren Sie jedes dieser Konten in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-179">Create multiple accounts in Active Directory Domain Services (AD DS), and then register each of these accounts in SharePoint.</span></span>
    
  
<span data-ttu-id="3ea9b-p119">Außerdem können verwaltete Konten registrieren und aktivieren Sie SharePoint Kontokennwörter Steuerelement. Benutzer müssen informiert geplanten kennwortänderungen und verwandte Dienst unterbrechen, aber die Konten, die von einer SharePoint-Farm, Webanwendungen, verwendet werden und verschiedene Dienste automatisch zurücksetzen und bereitgestellt, die in der Farm nach Bedarf, basierend auf einzeln konfigurierte Kennwort zurücksetzen Zeitpläne.</span><span class="sxs-lookup"><span data-stu-id="3ea9b-p119">You can also register managed accounts and enable SharePoint to control account passwords. Users have to be notified about planned password changes and related service interruptions, but the accounts used by a SharePoint farm, web applications, and various services can be automatically reset and deployed within the farm as necessary, based on individually configured password reset schedules.</span></span>
  
    
    
<span data-ttu-id="3ea9b-182">Zu den von der  [SPManagedAccount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.aspx) -Klasse ausgeführten Vorgängen zählen Folgende:</span><span class="sxs-lookup"><span data-stu-id="3ea9b-182">Operations that you can use the  [SPManagedAccount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.aspx) class to perform include:</span></span>
  
    
    

- <span data-ttu-id="3ea9b-183">Ändern des Kennworts</span><span class="sxs-lookup"><span data-stu-id="3ea9b-183">Change password</span></span>
    
  
- <span data-ttu-id="3ea9b-184">Festlegen eines Zeitplans für die Kennwortänderung</span><span class="sxs-lookup"><span data-stu-id="3ea9b-184">Set a password change schedule</span></span>
    
  
- <span data-ttu-id="3ea9b-185">Verteilen der Kennwortänderung</span><span class="sxs-lookup"><span data-stu-id="3ea9b-185">Propagate password change</span></span>
    
  
- <span data-ttu-id="3ea9b-186">Bestimmen der letzten Änderung eines Kennworts</span><span class="sxs-lookup"><span data-stu-id="3ea9b-186">Find out when a password was last changed</span></span>
    
  
- <span data-ttu-id="3ea9b-187">Erzwingen einer minimalen Länge für ein Kennwort</span><span class="sxs-lookup"><span data-stu-id="3ea9b-187">Enforce minimum length for password</span></span>
    
  
<span data-ttu-id="3ea9b-188">Weitere Informationen zur API für verwaltete Konten finden Sie über die folgenden Hyperlinks:</span><span class="sxs-lookup"><span data-stu-id="3ea9b-188">For more information about the managed account API, see the following links:</span></span>
  
    
    

-  [<span data-ttu-id="3ea9b-189">SPManagedAccount</span><span class="sxs-lookup"><span data-stu-id="3ea9b-189">SPManagedAccount</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.aspx)
    
  
-  [<span data-ttu-id="3ea9b-190">SPManagedAccount.EventProcessingOptions</span><span class="sxs-lookup"><span data-stu-id="3ea9b-190">SPManagedAccount.EventProcessingOptions</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.EventProcessingOptions.aspx)
    
  
-  [<span data-ttu-id="3ea9b-191">SPManagedAccount.EventType</span><span class="sxs-lookup"><span data-stu-id="3ea9b-191">SPManagedAccount.EventType</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.EventType.aspx)
    
  

## <a name="see-also"></a><span data-ttu-id="3ea9b-192">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="3ea9b-192">See also</span></span>
<span data-ttu-id="3ea9b-193"><a name="SP15_RoleInheritance_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="3ea9b-193"><a name="SP15_RoleInheritance_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="3ea9b-194">Authentifizierung, Autorisierung und Sicherheit in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ea9b-194">Authentication, authorization, and security in SharePoint</span></span>](authentication-authorization-and-security-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3ea9b-195">Autorisierung, Benutzer, Gruppen und das Objektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ea9b-195">Authorization, users, groups, and the object model in SharePoint</span></span>](authorization-users-groups-and-the-object-model-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3ea9b-196">Anspruchsbasierte Identität in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ea9b-196">Claims-based identity in SharePoint</span></span>](claims-based-identity-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3ea9b-197">Anspruchsbasierte Identität und-Konzepte in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ea9b-197">Claims-based identity and concepts in SharePoint</span></span>](claims-based-identity-and-concepts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3ea9b-198">Konfiguration, Verwaltung und Ressourcen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ea9b-198">Configuration, administration, and resources in SharePoint</span></span>](configuration-administration-and-resources-in-sharepoint.md)
    
  

