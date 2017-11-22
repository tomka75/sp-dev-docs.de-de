---
title: "Eingehende Ansprüche Anmelden bei SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 08c687aa-e485-4269-aea8-4333da3588a5
ms.openlocfilehash: 982b9d2b6f65c73223ed4c317e631b017d87c980
ms.sourcegitcommit: d68d6cf927d69696a3561f7d8ffe9a3ed9dbd03c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="incoming-claims-signing-into-sharepoint"></a>Eingehende Ansprüche: Anmelden bei SharePoint

## <a name="signing-in-to-sharepoint"></a>Anmelden bei SharePoint

Wenn sich ein Benutzer bei SharePoint Server anmeldet, wird sein Token geprüft und anschließend für die Anmeldung bei SharePoint verwendet. Bei dem Token handelt es sich um ein von einem Forderungsanbieter bereitgestelltes Sicherheitstoken.
  
    
    

> **Hinweis:** Weitere Informationen zu anspruchsbasierter Authentifizierung für eine einzelne SharePoint-Farm sowie zu anspruchsbasierter Authentifizierung zwischen verschiedenen SharePoint-Farmen finden Sie im TechNet-Artikel zum Thema [Planen von anspruchsbasierter Authentifizierung](http://technet.microsoft.com/de-DE/library/cc262350.aspx).
  
    
    


### <a name="windows-claims-mode-sign-in"></a>Anmelden im Windows-Anspruchsmodus

Bei der Anmeldung im Windows-Forderungsmodus erfolgt die Anmeldung mit einer Negotiate-Abfrage der integrierten Windows-Authentifizierung (NTLM/Kerberos). Nach der Erstellung des  [WindowsIdentity](https://msdn.microsoft.com/library/System.Security.Principal.WindowsIdentity.aspx) -Objekts (das einen Windows-Benutzer repräsentiert) wird allerdings von SharePoint Server das [WindowsIdentity](https://msdn.microsoft.com/library/System.Security.Principal.WindowsIdentity.aspx) -Objekt in ein [ClaimsIdentity](https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx) -Objekt konvertiert (das eine forderungsbasierte Darstellung eines Benutzers repräsentiert).
  
    
    
SharePoint Server führt dann eine Forderungsaugmentation durch und verarbeitet das resultierende Token, das von SharePoint Server ausgestellt wird. Das bedeutet, dass einige Features (z. B. die Mehrinstanzenunterstützung für Dienstanwendungen und benutzerdefinierte Forderungsanbieter) in SharePoint Server funktionieren, obwohl die Clients davon ausgehen, dass sich SharePoint Server im systemeigenen Windows-Anmeldungsmodus befindet. Die Anmeldung im Windows-Forderungsmodus ist die Werksvorgabe für SharePoint Server. 
  
    
    
Alle Forderungsanmeldungstypen nutzen die passive Anmeldung. Die passive Anmeldung erfolgt über eine Windows-Abfrage, allerdings über eine eigene Anmeldeseite, die über eine 302-Umleitung aufgerufen wird. Dieser Modus ist nützlich, wenn mehrere Anmeldemethoden aktiviert sind und der Benutzer unter mehreren unterstützten Forderungsanbietern wählen muss. Win32-Clients müssen die formularbasierte Authentifizierung in Office-Clients unterstützen. Einige Office-Clients folgen einem anderen Protokoll.
  
    
    

### <a name="saml-passive-sign-in-mode"></a>Passiver SAML-Anmeldungsmodus

Bei der passiven SAML-Anmeldung (Security Assertion Markup Language) wird der Client (z. B. eine Webseite) bei der Benutzeranmeldung an den festgelegten Forderungsanbieter (z. B. den Windows Live ID-Forderungsanbieter) umgeleitet. Nach der Authentifizierung des Benutzers durch den Forderungsanbieter wird das vom Forderungsanbieter vorgelegte SAML-Token von SharePoint Server übernommen und verarbeitet, anschließend werden die Forderungen augmentiert.
  
    
    
Bei SAML-basierten Forderungsanbietern wie dem Forderungsanbieter der Active Directory-Verbunddienste und dem Windows Live ID-Forderungsanbieter wird nur die Anmeldung im passiven SAML-Anmeldungsmodus unterstützt. Die passive SAML-Anmeldung ist das Onlineidentitätsmodell von SharePoint.  
  
    
    

> **Hinweis:** Der Begriff passive SAML-Anmeldung beschreibt einen bestimmten Typ Anmeldeprozess. Bei passiver SAML-Anmeldung ist die Anmeldung für eine Webanwendung so konfiguriert, dass Token von einem vertrauenswürdigen Anmeldeanbieter angenommen werden. Ein vertrauenswürdiger Anmeldeanbieter ist ein externer Sicherheitstokendienst (STS, Security Token Service) außerhalb von SharePoint, dem SharePoint vertraut. 
  
    
    

Win32-Clients müssen die in Office-Clients implementierte formularbasierte Authentifizierung unterstützen.
  
    
    

### <a name="aspnet-membership-and-role-passive-sign-in"></a>Passive Anmeldung von Mitgliedern und Rollen in ASP.NET

Bei der passiven Anmeldung von Mitgliedern und Rollen in ASP.NET erfolgt die Anmeldung durch das Umleiten des Clients an eine Webseite, auf der die ASP.NET-Anmeldesteuerelemente gehostet sind. Nachdem das Identitätsobjekt, das eine Benutzeridentität darstellt, erstellt wurde, konvertiert SharePoint Server dies in ein  [ClaimsIdentity](https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx) -Objekt (das eine anspruchsbasierte Darstellung eines Benutzers ist).
  
    
    
Anschließend führt SharePoint Server eine Anspruchserweiterung durch. Win32-Clients müssen die in Office-Clients implementierte formularbasierte Authentifizierung unterstützen.
  
    
    

### <a name="windows-classic-mode-sign-in"></a>Anmeldung im klassischen Windows-Modus

Die Anmeldung im klassischen Windows-Modus wird in dieser Version nicht mehr unterstützt. Bei der Anmeldung im klassischen Windows-Modus erfolgt die Anmeldung mit einer Negotiate-Abfrage der integrierten Windows-Authentifizierung (NTLM/Kerberos). Es gibt keine Forderungsaugmentation, deshalb funktionieren einige Features (z. B. die Mehrinstanzenunterstützung für Dienstanwendungen und benutzerdefinierte Forderungsanbieter), wenn sich ein Benutzer in diesem Modus anmeldet. 
  
    
    
Einige Dienstanwendungen erfordern möglicherweise auch den Anspruchsmodus für einige Features. 
  
    
    

### <a name="anonymous-access"></a>Anonymer Zugriff

Sie können den anonymen Zugriff für eine Webanwendung aktivieren. Die Administratoren der Websites innerhalb der Webanwendung können den anonymen Zugriff gestatten. Wenn anonyme Benutzer auf geschützte Ressourcen zugreifen möchten, können sie auf eine Anmeldeschaltfläche klicken, um ihre Anmeldeinformationen zu übertragen. 
  
    
    
SharePoint Server führt dann eine Forderungsaugmentation durch. Win32-Clients müssen die formularbasierte Authentifizierung in Office-Clients unterstützen.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Anspruchsbasierte Identität in SharePoint](claims-based-identity-in-sharepoint.md)
    
  
-  [Anspruchsanbieter in SharePoint](claims-provider-in-sharepoint.md)
    
  
-  [Vorgehensweise: Erstellen ein anspruchsanbieters in SharePoint](how-to-create-a-claims-provider-in-sharepoint.md)
    
  
-  [Vorgehensweise: POST eines anspruchsanbieters in SharePoint](how-to-deploy-a-claims-provider-in-sharepoint.md)
    
  

