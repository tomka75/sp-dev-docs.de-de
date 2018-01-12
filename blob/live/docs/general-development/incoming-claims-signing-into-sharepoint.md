---
title: "Eingehende Ansprüche Anmelden bei SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 08c687aa-e485-4269-aea8-4333da3588a5
ms.openlocfilehash: 713327d7f1fddb2f7ad5d9abbc8d9dbfc99eea61
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="incoming-claims-signing-into-sharepoint"></a><span data-ttu-id="ad1d1-102">Eingehende Ansprüche: Anmelden bei SharePoint</span><span class="sxs-lookup"><span data-stu-id="ad1d1-102">Incoming claims: Signing into SharePoint</span></span>

## <a name="signing-in-to-sharepoint"></a><span data-ttu-id="ad1d1-103">Anmelden bei SharePoint</span><span class="sxs-lookup"><span data-stu-id="ad1d1-103">Signing in to SharePoint</span></span>

<span data-ttu-id="ad1d1-p101">Wenn sich ein Benutzer bei SharePoint Server anmeldet, wird sein Token geprüft und anschließend für die Anmeldung bei SharePoint verwendet. Bei dem Token handelt es sich um ein von einem Forderungsanbieter bereitgestelltes Sicherheitstoken.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-p101">When a user signs in to SharePoint Server, the user's token is validated and then used to sign in to SharePoint. The user's token is a security token issued by a claims provider.</span></span>
  
> [!NOTE]
> <span data-ttu-id="ad1d1-106">Informationen zur forderungsbasierten Authentifizierung für eine einzelne SharePoint-Farm sowie zur farmübergreifenden SharePoint-Forderungsauthentifizierung finden Sie im TechNet unter [Planen der Forderungsauthentifizierung]((http://technet.microsoft.com/de-DE/library/cc262350.aspx)).</span><span class="sxs-lookup"><span data-stu-id="ad1d1-106">[Note:]((http://technet.microsoft.com/de-DE/library/cc262350.aspx)) For information about claims authentication for a single SharePoint farm and inter-farm SharePoint claims authentication, see  Plan for claims authentication on TechNet.</span></span>
  
    
    


### <a name="windows-claims-mode-sign-in"></a><span data-ttu-id="ad1d1-107">Anmelden im Windows-Anspruchsmodus</span><span class="sxs-lookup"><span data-stu-id="ad1d1-107">Windows claims mode sign-in</span></span>

<span data-ttu-id="ad1d1-p102">Bei der Anmeldung im Windows-Forderungsmodus erfolgt die Anmeldung mit einer Negotiate-Abfrage der integrierten Windows-Authentifizierung (NTLM/Kerberos). Nach der Erstellung des  [WindowsIdentity]((https://msdn.microsoft.com/library/System.Security.Principal.WindowsIdentity.aspx)) -Objekts (das einen Windows-Benutzer repräsentiert) wird allerdings von SharePoint Server das [WindowsIdentity]((https://msdn.microsoft.com/library/System.Security.Principal.WindowsIdentity.aspx)) -Objekt in ein [ClaimsIdentity]((https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx)) -Objekt konvertiert (das eine forderungsbasierte Darstellung eines Benutzers repräsentiert).</span><span class="sxs-lookup"><span data-stu-id="ad1d1-p102">In Windows claims mode sign-in, the sign-in happens with Integrated Windows authentication challenge by using Negotiate (NTLM/Kerberos). But, after the  [WindowsIdentity]((https://msdn.microsoft.com/library/System.Security.Principal.WindowsIdentity.aspx)) object (which represents a Windows user) is created, SharePoint Server converts the [WindowsIdentity]((https://msdn.microsoft.com/library/System.Security.Principal.WindowsIdentity.aspx)) object into a [ClaimsIdentity]((https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx)) object (which represents a claims-based representation of a user).</span></span>
  
    
    
<span data-ttu-id="ad1d1-p103">SharePoint Server führt dann eine Forderungsaugmentation durch und verarbeitet das resultierende Token, das von SharePoint Server ausgestellt wird. Das bedeutet, dass einige Features (z. B. die Mehrinstanzenunterstützung für Dienstanwendungen und benutzerdefinierte Forderungsanbieter) in SharePoint Server funktionieren, obwohl die Clients davon ausgehen, dass sich SharePoint Server im systemeigenen Windows-Anmeldungsmodus befindet. Die Anmeldung im Windows-Forderungsmodus ist die Werksvorgabe für SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-p103">SharePoint Server then does claims augmentation and handles the resulting token that is issued by SharePoint Server. This means that some features (for example, multitenant support for service applications and custom claims providers) in SharePoint Server work, even though the clients believe that SharePoint Server is in native Windows login mode. The Windows claims-mode sign-in experience is the built-in default for SharePoint Server.</span></span> 
  
    
    
<span data-ttu-id="ad1d1-p104">Alle Forderungsanmeldungstypen nutzen die passive Anmeldung. Die passive Anmeldung erfolgt über eine Windows-Abfrage, allerdings über eine eigene Anmeldeseite, die über eine 302-Umleitung aufgerufen wird. Dieser Modus ist nützlich, wenn mehrere Anmeldemethoden aktiviert sind und der Benutzer unter mehreren unterstützten Forderungsanbietern wählen muss. Win32-Clients müssen die formularbasierte Authentifizierung in Office-Clients unterstützen. Einige Office-Clients folgen einem anderen Protokoll.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-p104">All claims sign-in types rely on passive sign-in. The passive sign-in happens by using Windows challenge, but from a separate login page that arrives through a 302 redirect. This mode is useful when more than one sign-in method is turned on and the user must choose between the supported claims providers. Win32 clients must support the forms-based authentication that is implemented in Office clients. Some Office clients follow a different protocol.</span></span>
  
    
    

### <a name="saml-passive-sign-in-mode"></a><span data-ttu-id="ad1d1-118">Passiver SAML-Anmeldungsmodus</span><span class="sxs-lookup"><span data-stu-id="ad1d1-118">SAML passive sign-in mode</span></span>

<span data-ttu-id="ad1d1-p105">Bei der passiven SAML-Anmeldung (Security Assertion Markup Language) wird der Client (z. B. eine Webseite) bei der Benutzeranmeldung an den festgelegten Forderungsanbieter (z. B. den Windows Live ID-Forderungsanbieter) umgeleitet. Nach der Authentifizierung des Benutzers durch den Forderungsanbieter wird das vom Forderungsanbieter vorgelegte SAML-Token von SharePoint Server übernommen und verarbeitet, anschließend werden die Forderungen augmentiert.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-p105">In Security Assertion Markup Language (SAML) passive sign-in, when a user signs in, the client (which might be a webpage) is redirected to the designated claims provider (for example, the Windows Live ID claims provider). After the claims provider authenticates the user, SharePoint Server takes the SAML token presented by the claims provider, processes the SAML token, and then augments the claims.</span></span>
  
    
    
<span data-ttu-id="ad1d1-p106">Bei SAML-basierten Forderungsanbietern wie dem Forderungsanbieter der Active Directory-Verbunddienste und dem Windows Live ID-Forderungsanbieter wird nur die Anmeldung im passiven SAML-Anmeldungsmodus unterstützt. Die passive SAML-Anmeldung ist das Onlineidentitätsmodell von SharePoint.  </span><span class="sxs-lookup"><span data-stu-id="ad1d1-p106">For SAML-based claims providers, like the Active Directory Federation Services (ADFS) claims provider and the Windows Live ID claims provider, signing in by using the SAML passive sign-in mode is the only supported way. The SAML passive sign-in is the SharePoint online identity model.</span></span>
  
> [!NOTE]
> <span data-ttu-id="ad1d1-123">Der Begriff passive SAML-Anmeldung beschreibt einen bestimmten Typ Anmeldeprozess.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-123">Note: SAML passive sign-in describes the process of signing in.</span></span> <span data-ttu-id="ad1d1-124">Bei passiver SAML-Anmeldung ist die Anmeldung für eine Webanwendung so konfiguriert, dass Token von einem vertrauenswürdigen Anmeldeanbieter angenommen werden.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-124">When a sign-in for a web application is configured to accept tokens from a trusted login provider, this type of sign-in is called SAML passive sign-in.</span></span> <span data-ttu-id="ad1d1-125">Ein vertrauenswürdiger Anmeldeanbieter ist ein externer Sicherheitstokendienst (STS, Security Token Service) außerhalb von SharePoint, dem SharePoint vertraut.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-125">A trusted login provider is an external (that is, external to SharePoint) security token service (STS) that SharePoint trusts.</span></span> 
  
    
    

<span data-ttu-id="ad1d1-126">Win32-Clients müssen die in Office-Clients implementierte formularbasierte Authentifizierung unterstützen.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-126">Win32 clients must support the forms-based authentication that is implemented in Office clients.</span></span>
  
    
    

### <a name="aspnet-membership-and-role-passive-sign-in"></a><span data-ttu-id="ad1d1-127">Passive Anmeldung von Mitgliedern und Rollen in ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ad1d1-127">ASP.NET membership and role passive sign-in</span></span>

<span data-ttu-id="ad1d1-p108">Bei der passiven Anmeldung von Mitgliedern und Rollen in ASP.NET erfolgt die Anmeldung durch das Umleiten des Clients an eine Webseite, auf der die ASP.NET-Anmeldesteuerelemente gehostet sind. Nachdem das Identitätsobjekt, das eine Benutzeridentität darstellt, erstellt wurde, konvertiert SharePoint Server dies in ein  [ClaimsIdentity]((https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx)) -Objekt (das eine anspruchsbasierte Darstellung eines Benutzers ist).</span><span class="sxs-lookup"><span data-stu-id="ad1d1-p108">In ASP.NET membership and role passive sign-in, the sign-in happens by redirecting the client to a webpage where the ASP.NET log-in controls are hosted. After the identity object that represents a user identity is created, SharePoint Server converts it to a  [ClaimsIdentity]((https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx)) object (which represents a claims-based representation of a user).</span></span>
  
    
    
<span data-ttu-id="ad1d1-p109">Anschließend führt SharePoint Server eine Anspruchserweiterung durch. Win32-Clients müssen die in Office-Clients implementierte formularbasierte Authentifizierung unterstützen.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-p109">SharePoint Server then does claims augmentation. Win32 clients must support the forms-based authentication that is implemented in Office clients.</span></span>
  
    
    

### <a name="windows-classic-mode-sign-in"></a><span data-ttu-id="ad1d1-132">Anmeldung im klassischen Windows-Modus</span><span class="sxs-lookup"><span data-stu-id="ad1d1-132">Windows classic mode sign-in</span></span>

<span data-ttu-id="ad1d1-p110">Die Anmeldung im klassischen Windows-Modus wird in dieser Version nicht mehr unterstützt. Bei der Anmeldung im klassischen Windows-Modus erfolgt die Anmeldung mit einer Negotiate-Abfrage der integrierten Windows-Authentifizierung (NTLM/Kerberos). Es gibt keine Forderungsaugmentation, deshalb funktionieren einige Features (z. B. die Mehrinstanzenunterstützung für Dienstanwendungen und benutzerdefinierte Forderungsanbieter), wenn sich ein Benutzer in diesem Modus anmeldet. </span><span class="sxs-lookup"><span data-stu-id="ad1d1-p110">The Windows classic mode sign-in is deprecated in this release. In Windows classic mode sign-in, the sign-in happens with the Integrated Windows authentication challenge by using Negotiate (NTLM/Kerberos). No claims augmentation is done, so some features (for example, multitenant support for service applications and custom claims providers) do not work when a user signs in by using this mode.</span></span>
  
    
    
<span data-ttu-id="ad1d1-136">Einige Dienstanwendungen erfordern möglicherweise auch den Anspruchsmodus für einige Features.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-136">Some service applications may also require claims mode for some features.</span></span> 
  
    
    

### <a name="anonymous-access"></a><span data-ttu-id="ad1d1-137">Anonymer Zugriff</span><span class="sxs-lookup"><span data-stu-id="ad1d1-137">Anonymous access</span></span>

<span data-ttu-id="ad1d1-p111">Sie können den anonymen Zugriff für eine Webanwendung aktivieren. Die Administratoren der Websites innerhalb der Webanwendung können den anonymen Zugriff gestatten. Wenn anonyme Benutzer auf geschützte Ressourcen zugreifen möchten, können sie auf eine Anmeldeschaltfläche klicken, um ihre Anmeldeinformationen zu übertragen.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-p111">You can enable anonymous access for a web application. Administrators of sites within the web application can choose to allow anonymous access. If anonymous users want to gain access to secured resources, they can click a logon button to submit their credentials.</span></span> 
  
    
    
<span data-ttu-id="ad1d1-p112">SharePoint Server führt dann eine Forderungsaugmentation durch. Win32-Clients müssen die formularbasierte Authentifizierung in Office-Clients unterstützen.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-p112">SharePoint Server then does claims augmentation. Win32 clients must support the forms-based authentication that is implemented in Office clients.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="ad1d1-143">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="ad1d1-143">See also</span></span>
<span data-ttu-id="ad1d1-144"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ad1d1-144"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="ad1d1-145">Anspruchsbasierte Identität in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ad1d1-145">Claims-based identity in SharePoint</span></span>](claims-based-identity-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ad1d1-146">Anspruchsanbieter in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ad1d1-146">Claims provider in SharePoint</span></span>](claims-provider-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ad1d1-147">Vorgehensweise: Erstellen ein anspruchsanbieters in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ad1d1-147">How to: Create a claims provider in SharePoint</span></span>](how-to-create-a-claims-provider-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ad1d1-148">Vorgehensweise: POST eines anspruchsanbieters in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ad1d1-148">How to: Deploy a claims provider in SharePoint</span></span>](how-to-deploy-a-claims-provider-in-sharepoint.md)
    
  

