---
title: "Rolle, Vererbung, Erhöhung von Berechtigungen und Kennwortänderungen in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6860c6c126d3d617e303ec4bd67f73236eb647d0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="role-inheritance-elevation-of-privilege-and-password-changes-in-sharepoint"></a>Rolle, Vererbung, Erhöhung von Berechtigungen und Kennwortänderungen in SharePoint

## <a name="roles-role-definitions-and-role-assignments"></a>Rollen, Rollendefinitionen und rollenzuweisungen
<a name="SP15_RoleInheritance_Role"> </a>

Eine Rolle besteht aus zwei Teilen: einer Rollendefinition und einer Rollenzuweisung. 
  
    
    
Die Rollendefinition oder Berechtigungsstufe, um die Liste der Rechte der Rolle zugeordnet. Ein Recht ist ein eindeutig gesteuert Aktion innerhalb einer SharePoint-Website. Beispielsweise kann ein Benutzer mit der Rolle **Read** Seiten in der Website und Ansicht Elemente in Listen wechseln. Benutzerberechtigungen werden niemals direkt mithilfe der Verwaltung von Informationsrechten verwaltet. Über Rollen werden alle Benutzer- und Gruppenkonten verwaltet. Eine Rollendefinition ist eine Auflistung der Rechte für ein bestimmtes Objekt gebunden. Rollendefinitionen (z. B. **Full Control**, **Read**, **Contribute**, **Design**oder **Limited Access**) sind bezogen auf der Website und die dieselbe Bedeutung überall innerhalb der Website, deren Bedeutung können unterscheiden sich jedoch zwischen Websites innerhalb der gleichen Websitesammlung befindet. Von der übergeordneten Website können auch Rollendefinitionen geerbt werden, wie Berechtigungen vererbt werden können. 
  
    
    
Die rollenzuweisung wird die Beziehung zwischen der Rollendefinition, die Benutzer und Gruppen und den Bereich (beispielsweise ein Benutzer möglicherweise ein Leser in Liste 1, während ein anderer Benutzer ein Leser in Liste 2 ist). Die Beziehung ausgedrückt durch die rollenzuweisung ist der Schlüssel vornehmen, rollenbasierte SharePoint Security Management. Alle Berechtigungen sind über Rollen verwaltet. Sie weisen nie Rechte direkt für einen Benutzer. Sie weisen nur sinnvolle Auflistungen der Rechte (Rollendefinitionen), die gut definiert und konsistent sind. Verwalten Sie eindeutige Berechtigungen durch Hinzufügen oder Entfernen von Benutzern und Gruppen zu oder von Rollendefinitionen über rollenzuweisungen.
  
    
    
Der Websiteadministrator kann die standardmäßigen Rollendefinitionen anpassen und zusätzliche benutzerdefinierte Rollen mithilfe der Seite Rollen verwalten erstellen, auf der die verfügbaren Rollendefinitionen der Website aufgelistet sind.
  
    
    

## <a name="role-definition-inheritance"></a>Vererbung von Rollendefinitionen
<a name="SP15_RoleInheritance_RoleDefInheritance"> </a>

SharePoint unterstützt erbende Rollendefinitionen auf ähnliche Weise, wie es unterstützt Vererbung von Berechtigungen und Vererbung von Rollendefinitionen Knacken erfordert auch Unterbrechen der Vererbung von Berechtigungen.
  
    
    
Jeder SharePoint-Objekt kann haben einen eigenen Satz von Berechtigungen oder erben die Berechtigungen von seinem übergeordneten Container. SharePoint unterstützt keine teilweise Vererbung, in dem ein Objekt alle Berechtigungen des übergeordneten Objekts erben und auch einige eigene Berechtigungen haben. Die Berechtigungen sind entweder eigene oder vererbte. gesteuerte Vererbung unterstützt SharePoint nicht. Ein Objekt kann beispielsweise nur von seinem übergeordneten Container, nicht von einem anderen Objekt oder Container erben.
  
    
    
Wenn eine Website Rollendefinitionen erbt, sind die Rollen schreibgeschützt - genauso wie die schreibgeschützten Berechtigungen in einer geerbten Website. Der Benutzer kann über einen Link zur übergeordneten Website navigieren, die die spezifischen Rollendefinitionen enthält. Die Standardeinstellung für alle neuen Websites, und zwar auch für Websites mit spezifischen Berechtigungen, sieht vor, dass Rollendefinitionen von der übergeordneten Website geerbt werden. Wenn die Berechtigungen websitespezifisch sind, können Rollendefinitionen auf geerbte Rollendefinitionen zurückgesetzt oder als lokale Rollendefinitionen bearbeitet werden.
  
    
    
Vererbung von Rollendefinitionen in einer Website wirkt sich auf die Vererbung von Berechtigungen folgenden Regeln:
  
    
    

- Das Erben von Berechtigungen ist nur möglich, wenn auch Rollendefinitionen geerbt werden.
    
  
- Das Erstellen spezifischer Rollendefinitionen ist nur möglich, wenn auch spezifische Berechtigungen erstellt werden.
    
  
- Das Zurücksetzen auf geerbte Rollendefinitionen ist nur möglich, wenn alle spezifischen Berechtigungen innerhalb der Website zurückgesetzt werden. Die vorhandenen Berechtigungen sind abhängig von den Rollendefinitionen.
    
  
- Das Zurücksetzen auf geerbte Berechtigungen ist nur möglich, wenn auch eine Zurücksetzung auf geerbte Rollendefinitionen erfolgt. Die Berechtigungen für eine Website sind immer an die Rollendefinitionen für diese Website geknüpft.
    
  

## <a name="managing-user-tokens"></a>Verwalten von Benutzertoken
<a name="SP15_RoleInheritance_ManagingUserTokens"> </a>

SharePoint ruft Benutzertokeninformationen aus der SharePoint-Datenbank ab. Wenn der Benutzer die Website noch nie besucht hat oder das Benutzertoken vor mehr als 24 Stunden generiert wurde, erzeugt SharePoint ein neues Benutzertoken. Hierzu wird versucht, die Liste der Gruppen zu aktualisieren, denen der Benutzer angehört. 
  
    
    
Wenn es sich bei dem Benutzerkonto um ein NT-Konto handelt, verwendet SharePoint die **AuthZ**-Schnittstelle, um im Active Directory-Verzeichnisdienst eine Abfrage nach der **TokenGroups**-Eigenschaft durchzuführen. Hierbei können Fehler auftreten, wenn SharePoint im Extranetmodus ausgeführt wird und nicht über die Berechtigung zum Abfragen von Active Directory nach dieser Eigenschaft verfügt.
  
    
    
Wenn das Benutzerkonto ein Mitgliedschaftsbenutzer ist, fragt SharePoint die ASP.NET **RoleManager** für alle Rollen, denen der Benutzer angehört. Dies kann fehlschlagen, wenn eine ordnungsgemäße .config-Datei für die aktuelle ausführbare Datei nicht vorhanden ist.
  
    
    
Wenn SharePoint Gruppenmitgliedschaften des Benutzers aus Active Directory oder **<roleManager>**erhalten kann, enthält das neu generierte Token nur der Benutzer eindeutige Sicherheits-ID (SID). Wird keine Ausnahme ausgelöst, aber ein Eintrag in der Server-ULS-Protokoll geschrieben wird. Das neue Token wird auch in der SharePoint-Datenbank geschrieben, damit es nicht innerhalb von 24 Stunden wiederhergestellt wird.
  
    
    
Nach SharePoint ein aktuell Token aus der SharePoint-Datenbank oder durch Generieren eines neuen Tokens erhält, SharePoint den Zeitstempel der aktuellen Zeit werden festgelegt und dann an den Aufrufer zurückgegeben wird. Dadurch wird sichergestellt, dass das Token 24 Stunden aktuell ist.
  
    
    
Nachdem das  [SPUserToken](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPUserToken.aspx) -Objekt an den Anrufer zurückgegeben wurde, ist es des Anrufers Verantwortung Token nicht zu verwenden, nachdem es abgelaufen ist. Sie können ein Hilfsprogramm nachverfolgen möchten den Ablauf des token Aufzeichnung der Zeit, wenn Sie das Token abrufen, schreiben und Vergleichen der Diff mit aktuellen Zeit vor [SPWebService.TokenTimeout](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPWebService.TokenTimeout.aspx) .
  
    
    
Wenn ein abgelaufene Token zum Erstellen einer SharePoint-Website verwendet wird, wird eine Ausnahme ausgelöst. Der Standardwert token-Timeout ist 24 Stunden. Es kann über  [SPWebService.TokenTimeout](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPWebService.TokenTimeout.aspx) zugegriffen werden.
  
    
    

## <a name="elevation-of-privilege"></a>Erhöhung von Berechtigungen
<a name="SP15_RoleInheritance_ElevationOfPrivilege"> </a>

Mithilfe von Rechteerweiterungen, einem in Windows SharePoint Services 3.0 neu eingeführten Feature, können Sie programmgesteuert Aktionen im Code mit einer höheren Berechtigungsstufe ausführen. Mit der  [SPSecurity.RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) -Methode kann ein Delegat bereitgestellt werden, von dem eine Teilmenge des Codes im Kontext eines Kontos mit höheren Berechtigungen als denen des aktuellen Benutzers ausgeführt wird.
  
    
    
Es folgt eine standardmäßige Verwendung von **RunWithElevatedPrivileges**.
  
    
    



```cs

SPSecurity.RunWithElevatedPrivileges(delegate()
{
    // Do things by assuming the permission of the "system account".
});
```

Häufig müssen Sie zum Ausführen von Aktionen in SharePoint ein neues  [SPSite](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSite.aspx) -Objekt abrufen, durch das die Änderungen bewirkt werden. Ein Beispiel:
  
    
    



```cs

SPSecurity.RunWithElevatedPrivileges(delegate()
{
    using (SPSite site = new SPSite(web.Site.ID))
    {
       // Do things by assuming the permission of the "system account".
    }
});
```

Obwohl rechteerweiterungen eine leistungsstarke Technik zum Verwalten der Sicherheit bietet, sollten sie mit Vorsicht verwendet werden. Sie sollten keine direkte Schäden, nicht gesteuerte Mechanismen für Personen mit niedrigen Berechtigungen, die Ihnen erteilten Berechtigungen zu umgehen verfügbar machen.
  
    
    

> **Wichtig:** Wenn die an  [RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) übergebene Methode Schreibvorgänge beinhaltet, sollte vor dem Aufruf von [RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) ein Aufruf von [SPUtility.ValidateFormDigest()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPUtility.ValidateFormDigest.aspx) oder [SPWeb.ValidateFormDigest()](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.ValidateFormDigest.aspx) erfolgen.
  
    
    


## <a name="automatic-password-changes"></a>Automatische Kennwortänderung
<a name="SP15_RoleInheritance_AutomaticPasswordChange"> </a>

Features für die automatische kennwortänderung können Sie aktualisieren und Bereitstellen von Kennwörtern ohne manuelle Kennwort Updateaufgaben für mehrere Konten, Dienste und Webanwendungen. Dadurch wird das Verwalten von Kennwort in SharePoint einfacher. Features für die automatische kennwortänderung können Sie bestimmen, ob ein Kennwort Testzeitraum und das Kennwort zurücksetzen können mithilfe von eine lange, kryptografisch starke zufällige Zeichenfolge ist.
  
    
    

### <a name="managed-account"></a>Verwaltete Konten

Verwenden Sie verwaltete Konten, um Features für die automatische kennwortänderung implementieren. Verwaltete Konten erhöhen der Sicherheit und Anwendungsisolation sicherzustellen. Mit verwalteten Konten können Sie folgende Aktionen ausführen:
  
    
    

- Konfigurieren von Features für die automatische kennwortänderung zum Bereitstellen von Kennwörtern in allen Diensten in einer Farm.
    
  
- Konfigurieren von SharePoint-Webanwendungen und -Diensten, die auf Anwendungsservern in einer SharePoint-Farm ausgeführt werden, sodass sie verschiedene Domänenkonten verwenden.
    
  
- Zuordnen von verwalteten Konten zu verschiedenen Diensten und Webanwendungen in einer Farm.
    
  
- Erstellen Sie mehrerer Konten in Active Directory-Domänendienste (AD DS) und anschließendes registrieren Sie jedes dieser Konten in SharePoint.
    
  
Außerdem können verwaltete Konten registrieren und aktivieren Sie SharePoint Kontokennwörter Steuerelement. Benutzer müssen informiert geplanten kennwortänderungen und verwandte Dienst unterbrechen, aber die Konten, die von einer SharePoint-Farm, Webanwendungen, verwendet werden und verschiedene Dienste automatisch zurücksetzen und bereitgestellt, die in der Farm nach Bedarf, basierend auf einzeln konfigurierte Kennwort zurücksetzen Zeitpläne.
  
    
    
Zu den von der  [SPManagedAccount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.aspx) -Klasse ausgeführten Vorgängen zählen Folgende:
  
    
    

- Ändern des Kennworts
    
  
- Festlegen eines Zeitplans für die Kennwortänderung
    
  
- Verteilen der Kennwortänderung
    
  
- Bestimmen der letzten Änderung eines Kennworts
    
  
- Erzwingen einer minimalen Länge für ein Kennwort
    
  
Weitere Informationen zur API für verwaltete Konten finden Sie über die folgenden Hyperlinks:
  
    
    

-  [SPManagedAccount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.aspx)
    
  
-  [SPManagedAccount.EventProcessingOptions](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.EventProcessingOptions.aspx)
    
  
-  [SPManagedAccount.EventType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.EventType.aspx)
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15_RoleInheritance_AdditionalResources"> </a>


-  [Authentifizierung, Autorisierung und Sicherheit in SharePoint](authentication-authorization-and-security-in-sharepoint.md)
    
  
-  [Autorisierung, Benutzer, Gruppen und das Objektmodell in SharePoint](authorization-users-groups-and-the-object-model-in-sharepoint.md)
    
  
-  [Anspruchsbasierte Identität in SharePoint](claims-based-identity-in-sharepoint.md)
    
  
-  [Anspruchsbasierte Identität und-Konzepte in SharePoint](claims-based-identity-and-concepts-in-sharepoint.md)
    
  
-  [Konfiguration, Verwaltung und Ressourcen in SharePoint](configuration-administration-and-resources-in-sharepoint.md)
    
  

