---
title: Authentifizierung, Autorisierung und Sicherheit in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8734790c-eb75-4d78-9604-7cc23b33b693
ms.openlocfilehash: 86ef3bb99435bf9a7c5c02e46c4f5a09b2a22765
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="authentication-authorization-and-security-in-sharepoint"></a><span data-ttu-id="e2fce-102">Authentifizierung, Autorisierung und Sicherheit in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e2fce-102">Authentication, authorization, and security in SharePoint</span></span>

## <a name="whats-new-in-sharepoint-for-authentication-authorization-and-security"></a><span data-ttu-id="e2fce-103">Neuerungen in SharePoint bei Authentifizierung, Autorisierung und Sicherheit</span><span class="sxs-lookup"><span data-stu-id="e2fce-103">What's new in SharePoint for authentication, authorization, and security</span></span>
<span data-ttu-id="e2fce-104"><a name="SP15_AuthenticationAuthorizationSecurity_WhatsNew"> </a></span><span class="sxs-lookup"><span data-stu-id="e2fce-104"><a name="SP15_AuthenticationAuthorizationSecurity_WhatsNew"> </a></span></span>

<span data-ttu-id="e2fce-105">Nachfolgend sind einige der optimierten Features von SharePoint aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="e2fce-105">The following are some of the enhancements added to SharePoint:</span></span> 
  
    
    

- <span data-ttu-id="e2fce-106">Benutzeranmeldung</span><span class="sxs-lookup"><span data-stu-id="e2fce-106">User sign-in</span></span>
    
  - <span data-ttu-id="e2fce-p101">SharePoint bietet weiter Unterstützung für den anspruchsbasierten und klassischen Authentifizierungsmodus. Die anspruchsbasierte Authentifizierung ist in SharePoint die Standardeinstellung. Der klassische Authentifizierungsmodus gilt als überholt und kann nur noch mithilfe von Windows PowerShell verwaltet werden. Für zahlreiche Features in SharePoint ist der anspruchsbasierte Modus erforderlich.</span><span class="sxs-lookup"><span data-stu-id="e2fce-p101">SharePoint continues to offer support for both claims and classic authentication modes. Claims authentication is the default authentication option in SharePoint. Classic-mode authentication is deprecated and can be managed only by using Windows PowerShell. A lot of features in SharePoint require claims-mode.</span></span> 
    
  
  - <span data-ttu-id="e2fce-p102">Die **MigrateUsers**-Methode in SharePoint 2010 gilt nun als überholt und eignet sich nicht mehr zum ordnungsgemäßen Migrieren von Konten. Verwenden Sie hierzu das neue Windows PowerShell-Cmdlet  `Convert-SPWebApplication`. Weitere Informationen finden Sie unter  [Migrieren von der klassischen Authentifizierung zur anspruchsbasierten Authentifizierung](http://technet.microsoft.com/de-DE/library/gg251985.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2fce-p102">The **MigrateUsers** method from SharePoint 2010 is now deprecated, it's no longer the correct way to migrate accounts. To migrate accounts, use the new Windows PowerShell cmdlet called `Convert-SPWebApplication`. For more information see  [Migrate from classic-mode to claims-based authentication in SharePoint](http://technet.microsoft.com/de-DE/library/gg251985.aspx).</span></span>
    
  
  - <span data-ttu-id="e2fce-p103">Anspruchsanbieter müssen nicht mehr registriert werden. Anspruchstypen müssen jedoch vorab konfiguriert werden. Sie können die Zeichen für den Anspruchstyp wählen, und für Anspruchstypen gibt es keine zwingende Reihenfolge.</span><span class="sxs-lookup"><span data-stu-id="e2fce-p103">Requirement to register claims providers is eliminated. However, you do have to pre-configure claims type. You can choose the characters for the claim type and there is no enforcement on the ordering of claim types.</span></span>
    
  
  - <span data-ttu-id="e2fce-117">SharePoint verfolgt **FedAuth**-Cookies im neuen verteilten Cachedienst mithilfe von Windows Server AppFabric-Cachefeatures nach.</span><span class="sxs-lookup"><span data-stu-id="e2fce-117">SharePoint tracks **FedAuth** cookies in the new distributed cache service using Windows Server AppFabric Caching.</span></span>
    
  
  - <span data-ttu-id="e2fce-118">Es erfolgt eine wesentlich umfangreichere Protokollierung, die Sie bei der Behandlung von Authentifizierungsproblemen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="e2fce-118">Significantly more logging is provided to help troubleshoot authentication issues.</span></span> 
    
  
- <span data-ttu-id="e2fce-119">Authentifizierung von Diensten und Apps</span><span class="sxs-lookup"><span data-stu-id="e2fce-119">Services and app authentication</span></span>
    
  - <span data-ttu-id="e2fce-p104">In SharePoint können Sie nun Apps für SharePoint erstellen. Eine SharePoint-Add-In hat eine eigene Identität und ist einem Sicherheitsprinzipal zugeordnet, der als App-Prinzipal bezeichnet wird. Wie Benutzer und Gruppen verfügt ein App-Prinzipal über bestimmte Berechtigungen und Rechte.</span><span class="sxs-lookup"><span data-stu-id="e2fce-p104">In SharePoint, you now have the ability to create apps for SharePoint. A SharePoint Add-in has its own identity and is associated with a security principal, called an app principal. Like users and groups, an app principal has certain permissions and rights.</span></span> 
    
  
  - <span data-ttu-id="e2fce-p105">In SharePoint stellt der Server-zu-Server-Sicherheitstokendienst Zugriffstoken für die Server-zu-Server-Authentifizierung bereit. Der Server-zu-Server-Sicherheitstokendienst gewährt temporären Zugriffstoken Zugriff auf andere Anwendungsdienste, z. B. Exchange Server 2013, Microsoft Lync 2013 und Apps für SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e2fce-p105">In SharePoint, the server-to-server security token service (STS) provides access tokens for server-to-server authentication. The server-to-server STS enables temporary access tokens to access other application services, such as Exchange Server 2013 and Microsoft Lync 2013, and apps for SharePoint.</span></span>
    
  

## <a name="authentication-and-authorization"></a><span data-ttu-id="e2fce-125">Authentifizierung und Autorisierung</span><span class="sxs-lookup"><span data-stu-id="e2fce-125">Authentication and authorization</span></span>
<span data-ttu-id="e2fce-126"><a name="SP15_AuthenticationAuthorizationSecurity_AuthenticationAndAuthorization"> </a></span><span class="sxs-lookup"><span data-stu-id="e2fce-126"><a name="SP15_AuthenticationAuthorizationSecurity_AuthenticationAndAuthorization"> </a></span></span>

<span data-ttu-id="e2fce-p106">Von SharePoint wird die Sicherheit für den Benutzerzugriff auf Website-, Listen, Listenordner- oder Bibliotheksordner- und Elementebene unterstützt. Die Sicherheitsverwaltung ist auf allen Ebenen rollenbasiert, sodass eine zusammenhängende Sicherheitsverwaltung in der SharePoint-Plattform mit einer konsistenten rollenbasierten Benutzeroberfläche und einem Objektmodell für das Zuweisen von Berechtigungen für Objekte bereitgestellt wird. Daher implementiert die Sicherheit auf Listenebene, Ordnerebene oder Elementebene dasselbe Benutzermodell wie die Sicherheit auf Websiteebene, sodass das Verwalten von Benutzerrechten und das Gruppieren von Rechten auf einer Website vereinfacht wird. SharePoint bietet auch Unterstützung für eindeutige Berechtigungen in den Ordnern und Elementen von Listen und Dokumentbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="e2fce-p106">SharePoint supports security for user access at the website, list, list or library folder, and item levels. Security management is role-based at all levels, providing coherent security management across the SharePoint platform with a consistent role-based user interface and object model for assigning permissions on objects. As a result, list-level, folder-level, or item-level security implements the same user model as website-level security, making it easier to manage user rights and group rights throughout a website. SharePoint also supports unique permissions on the folders and items contained within lists and document libraries.</span></span>
  
    
    

> [!NOTE]
> <span data-ttu-id="e2fce-131">Informationen zur Autorisierung im Zusammenhang mit SharePoint-Add-Ins finden Sie unter [Autorisierung und Authentifizierung für Add-Ins in SharePoint](http://msdn.microsoft.com/library/bde5647a-fff1-4b51-b67b-2139de79ce4a%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2fce-131">[Note:](http://msdn.microsoft.com/library/bde5647a-fff1-4b51-b67b-2139de79ce4a%28Office.15%29.aspx) For information about authorization related to SharePoint Add-ins, see  Authorization and authentication of SharePoint Add-ins.</span></span> 
  
    
    

<span data-ttu-id="e2fce-p107">Autorisierung bezieht sich auf den Prozess, mit dem SharePoint Sicherheit für Websites, Listen, Ordner oder Elemente bereitstellt, indem bestimmt wird, welche Benutzer bestimmte Aktionen auf ein angegebenes Objekt anwenden dürfen. Der Autorisierungsprozess setzt voraus, dass der Benutzer bereits authentifiziert wurde, was sich auf den Prozess bezieht, mit dem SharePoint den aktuellen Benutzer identifiziert. SharePoint implementiert nicht sein eigenes System für die Authentifizierung oder Identitätsverwaltung, sondern vertraut stattdessen auf externe Systeme, entweder die Windows-Authentifizierung oder ein anderes System.</span><span class="sxs-lookup"><span data-stu-id="e2fce-p107">Authorization refers to the process by which SharePoint provides security for websites, lists, folders, or items by determining which users can perform specific actions on a given object. The authorization process assumes that the user has already been authenticated, which refers to the process by which SharePoint identifies the current user. SharePoint does not implement its own system for authentication or identity management, but instead relies on external systems, whether Windows authentication or non-Windows authentication.</span></span>
  
    
    
<span data-ttu-id="e2fce-135">In SharePoint werden die folgenden Typen von Authentifizierung unterstützt:</span><span class="sxs-lookup"><span data-stu-id="e2fce-135">SharePoint supports the following types of authentication:</span></span>
  
    
    

- <span data-ttu-id="e2fce-p108">**Windows:** Alle Integrationsoptionen in Microsoft-Internetinformationsdienste (Internet Information Services, IIS) und in der Windows-Authentifizierung, einschließlich Standard, Digest, Zertifikate, Windows NT LAN Manager (NTLM) und Kerberos werden unterstützt. Die Windows-Authentifizierung lässt zu, dass IIS die Authentifizierung für SharePoint durchführt.</span><span class="sxs-lookup"><span data-stu-id="e2fce-p108">**Windows:** All Internet Information Services (IIS) and Windows authentication integration options, including Basic, Digest, Certificates, Windows NT LAN Manager (NTLM), and Kerberos are supported. Windows authentication allows IIS to perform the authentication for SharePoint.</span></span>
    
    <span data-ttu-id="e2fce-138">Informationen zum Anmelden bei SharePoint mithilfe des Windows-Forderungsmodus finden Sie unter  [Eingehende Ansprüche: Anmelden bei SharePoint](incoming-claims-signing-into-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e2fce-138">For information about signing in to SharePoint by using Windows claims mode, see  [Incoming claims: Signing into SharePoint](incoming-claims-signing-into-sharepoint.md).</span></span>
    
    > <span data-ttu-id="e2fce-139">**Wichtig:** Weitere Informationen zum Aussetzen des Identitätswechsels finden Sie unter [Vermeiden des Aussetzens des Identitätswechsels durch den aufrufenden Benutzer](http://msdn.microsoft.com/de-DE/library/ff407852.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2fce-139">**Important:** For information about suspending impersonation, see [Avoid suspending impersonation of the calling user](http://msdn.microsoft.com/de-DE/library/ff407852.aspx).</span></span> 
- <span data-ttu-id="e2fce-p109">**ASP.NET-Formulare:** Ein nicht von Windows bereitgestelltes Identitätsverwaltungssystem, das das austauschbare, auf ASP.NET-Formularen basierte Authentifizierungssystem verwendet, wird unterstützt. Mit diesem Modus kann SharePoint mit einer Vielzahl von Identitätsverwaltungssystemen zusammenarbeiten, einschließlich extern definierter Gruppen oder Rollen wie Lightweight Directory Access-Protokoll (LDAP) und schlanker Datenbankidentitäts-Verwaltungssysteme. Dank der Formularauthentifizierung kann ASP.NET die Authentifizierung für SharePoint durchführen, wobei häufig eine Umleitung zu einer Anmeldeseite eingeschlossen ist. In SharePoint werden ASP.NET-Formulare nur bei der anspruchsbasierten Authentifizierung unterstützt. Ein Formularanbieter muss innerhalb einer Webanwendung registriert sein, die für Ansprüche konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="e2fce-p109">**ASP.NET Forms:** A non-Windows identity management system that uses the pluggable ASP.NET forms-based authentication system is supported. This mode enables SharePoint to work with a variety of identity management systems, including externally defined groups or roles such as Lightweight Directory Access Protocol (LDAP) and light-weight database identity management systems. Forms authentication allows ASP.NET to perform the authentication for SharePoint, often involving a redirect to a log-on page. In SharePoint, ASP.NET forms are supported only under claims authentication. A forms provider must be registered within a web application that is configured for claims.</span></span>
    
    <span data-ttu-id="e2fce-145">Informationen zum Anmelden bei SharePoint mithilfe der ASP.NET-Mitgliedschaft und zur passiven Anmeldung mit Rollen finden Sie unter  [Eingehende Ansprüche: Anmelden bei SharePoint](incoming-claims-signing-into-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e2fce-145">For information about signing in to SharePoint by using ASP.NET membership and role passive sign-in, see  [Incoming claims: Signing into SharePoint](incoming-claims-signing-into-sharepoint.md).</span></span>
    
  

> [!NOTE]
> <span data-ttu-id="e2fce-146">SharePoint unterstützt nicht die Arbeit mit einem Mitgliedschaftsanbieter, bei dem die Groß-/Kleinschreibung beachtet wird.</span><span class="sxs-lookup"><span data-stu-id="e2fce-146">Note: SharePoint does not support working with a case-sensitive membership provider.</span></span> <span data-ttu-id="e2fce-147">Es verwendet SQL-Speicher ohne Beachtung der Groß-/Kleinschreibung für alle Benutzer in der Datenbank, unabhängig vom Mitgliedschaftsanbieter.</span><span class="sxs-lookup"><span data-stu-id="e2fce-147">It uses case-insensitive SQL storage for all users in the database, regardless of the membership provider.</span></span> 
  
    
    


## <a name="claims-based-identity-and-authentication"></a><span data-ttu-id="e2fce-148">Anspruchsbasierte Identität und Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="e2fce-148">Claims-based identity and authentication</span></span>
<span data-ttu-id="e2fce-149"><a name="SP15_AuthenticationAuthorizationSecurity_ClaimsBasedIdentity"> </a></span><span class="sxs-lookup"><span data-stu-id="e2fce-149"><a name="SP15_AuthenticationAuthorizationSecurity_ClaimsBasedIdentity"> </a></span></span>

<span data-ttu-id="e2fce-150">Die anspruchsbasierte Identität ist ein Identitätsmodell in SharePoint. Dieses Identitätsmodell umfasst Features wie die Authentifizierung von Benutzern sowohl von Systemen, die auf Windows basieren, als auch von solchen, die nicht auf Windows basieren, mehrere Authentifizierungstypen, stärkere Authentifizierung in Echtzeit, eine größere Palette an Prinzipaltypen und die Delegierung von Benutzeridentitäten zwischen Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="e2fce-150">Claims-based identity is an identity model in SharePoint that includes features such as authentication across users of Windows-based systems and systems that are not Windows-based, multiple authentication types, stronger real-time authentication, a wider set of principal types, and delegation of user identity between applications.</span></span>
  
    
    
<span data-ttu-id="e2fce-p111">Wenn sich ein Benutzer an SharePoint anmeldet, wird das Benutzertoken überprüft und anschließend zum Anmelden an SharePoint verwendet. Das Benutzertoken ist ein von einem Anspruchsanbieter ausgegebenes Sicherheitstoken. Die folgenden Anmelde- oder Zugriffsmodi werden angeboten:</span><span class="sxs-lookup"><span data-stu-id="e2fce-p111">When a user signs in to SharePoint, the user's token is validated and then used to sign in to SharePoint. The user's token is a security token issued by a claims provider. The following are supported sign-in or access modes:</span></span>
  
    
    

- <span data-ttu-id="e2fce-154">Anmeldung im Windows-Forderungsmodus (Standard)</span><span class="sxs-lookup"><span data-stu-id="e2fce-154">Windows claims-mode sign-in (default)</span></span>
    
  
- <span data-ttu-id="e2fce-155">Passiver SAML-Anmeldungsmodus</span><span class="sxs-lookup"><span data-stu-id="e2fce-155">SAML passive sign-in mode</span></span>
    
  
- <span data-ttu-id="e2fce-156">Passive Anmeldung von Mitgliedern und Rollen in ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e2fce-156">ASP.NET membership and role passive sign-in</span></span>
    
  
- <span data-ttu-id="e2fce-157">Anmeldung im klassischen Windows-Modus (in dieser Version veraltet)</span><span class="sxs-lookup"><span data-stu-id="e2fce-157">Windows classic-mode sign-in (deprecated in this release)</span></span>
    
  

> [!NOTE]
> <span data-ttu-id="e2fce-158">Weitere Informationen zum Anmelden an SharePoint und zu den verschiedenen Anmeldemodi finden Sie unter [Eingehende Ansprüche: Anmelden bei SharePoint](incoming-claims-signing-into-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e2fce-158">[Note:](incoming-claims-signing-into-sharepoint.md) For more information about signing into SharePoint and the different sign-in modes, see  Incoming claims: Signing into SharePoint.</span></span> 
  
    
    

<span data-ttu-id="e2fce-p112">Wenn Sie Ansprüche unterstützende Anwendungen erstellen, legt der Benutzer der Anwendung eine Identität als eine Gruppe von Ansprüchen vor. Ein Anspruch kann z. B. der Benutzername sein, ein anderer eine E-Mail-Adresse. Der Grundgedanke ist die Konfiguration eines externen Identitätssystems, damit die Anwendung alle benötigten Informationen erhält, um bei jeder Anfrage alles über den Benutzer zu wissen, sowie eine kryptografische Garantie dahingehend zu geben, dass die von der Anwendung empfangenen Identitätsdaten aus einer vertrauenswürdigen Quelle stammen.</span><span class="sxs-lookup"><span data-stu-id="e2fce-p112">When you build claims-aware applications, the user presents an identity to your application as a set of claims. One claim could be the user's name, another might be an email address. The idea here is that an external identity system is configured to give your application all the information that it needs about the user with each request, along with cryptographic assurance that the identity data received by your application comes from a trusted source.</span></span>
  
    
    
<span data-ttu-id="e2fce-162">Bei diesem Modell ist eine einmalige Anmeldung viel leichter durchzusetzen, und Ihre Anwendung ist nicht mehr für Folgendes zuständig:</span><span class="sxs-lookup"><span data-stu-id="e2fce-162">Under this model, single sign-on is much easier to achieve, and your application is no longer responsible for the following:</span></span>
  
    
    

- <span data-ttu-id="e2fce-163">Authentifizierung von Benutzern</span><span class="sxs-lookup"><span data-stu-id="e2fce-163">Authenticating users</span></span>
    
  
- <span data-ttu-id="e2fce-164">Speicherung von Benutzerkonten und Kennwörtern</span><span class="sxs-lookup"><span data-stu-id="e2fce-164">Storing user accounts and passwords</span></span>
    
  
- <span data-ttu-id="e2fce-165">Aufruf von Unternehmensverzeichnissen zum Nachschlagen von Benutzeridentitätsdetails</span><span class="sxs-lookup"><span data-stu-id="e2fce-165">Calling to enterprise directories to look up user identity details</span></span>
    
  
- <span data-ttu-id="e2fce-166">Integration mit Identitätssystemen anderer Plattformen oder Unternehmen</span><span class="sxs-lookup"><span data-stu-id="e2fce-166">Integrating with identity systems from other platforms or companies</span></span>
    
  
<span data-ttu-id="e2fce-p113">Bei diesem Modell trifft die Anwendung Entscheidungen zur Identität basierend auf den vom Benutzer übermittelten Ansprüchen. Hierbei kann es sich von einer einfachen Anwendungspersonalisierung mit dem Vornamen des Benutzers bis zur Autorisierung des Benutzers für den Zugriff auf hochwertigere Features und Ressourcen in der Anwendung um alles Mögliche handeln.</span><span class="sxs-lookup"><span data-stu-id="e2fce-p113">Under this model, your application makes identity-related decisions based on claims supplied by the user. This could be anything from simple application personalization with the user's first name, to authorizing the user to access higher-value features and resources in your application.</span></span>
  
    
    

> [!NOTE]
> <span data-ttu-id="e2fce-169">Weitere Informationen zur anspruchsbasierten Identität und zu Anspruchsanbietern finden Sie unter [Anspruchsbasierte Identität und Konzepte in SharePoint](claims-based-identity-and-concepts-in-sharepoint.md) und [Anspruchsanbieter in SharePoint](claims-provider-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e2fce-169">[Note:](claims-based-identity-and-concepts-in-sharepoint.md) For more information about claims-based identity and claims providers, see  [Claims-based identity and concepts in SharePoint](claims-provider-in-sharepoint.md) and Claims provider in SharePoint.</span></span> 
  
    
    


## <a name="forms-based-authentication"></a><span data-ttu-id="e2fce-170">Formularbasierte Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="e2fce-170">Forms-based authentication</span></span>
<span data-ttu-id="e2fce-171"><a name="SP15_AuthenticationAuthorizationSecurity_FormsBasedAuthentication"> </a></span><span class="sxs-lookup"><span data-stu-id="e2fce-171"><a name="SP15_AuthenticationAuthorizationSecurity_FormsBasedAuthentication"> </a></span></span>

<span data-ttu-id="e2fce-p114">Die formularbasierte Authentifizierung stellt eine benutzerdefinierte Identitätsverwaltung in SharePoint bereit, indem ein Mitgliedschaftsanbieter implementiert wird, der die Schnittstellen zum Identifizieren und Authentifizieren einzelner Benutzer definiert, und ein Rollen-Manager, der die Schnittstellen zum Gruppieren einzelner Benutzer in logische Gruppen und Rollen definiert. In SharePoint muss ein Mitgliedschaftsanbieter die erforderliche  [System.Web.Security.Membership.ValidateUser](http://msdn.microsoft.com/library/33f4af0b-75c0-4504-b90f-05e742e44a88.aspx)-Methode implementieren. Wenn ein Benutzername angegeben wird, gibt das Rollenanbietersystem eine Liste der Rollen zurück, zu denen der Benutzer gehört.</span><span class="sxs-lookup"><span data-stu-id="e2fce-p114">Forms-based authentication provides custom identity management in SharePoint by implementing a membership provider, which defines interfaces for identifying and authenticating individual users, and a role manager, which defines interfaces for grouping individual users into logical groups or roles. In SharePoint, a membership provider must implement the required  [System.Web.Security.Membership.ValidateUser](http://msdn.microsoft.com/library/33f4af0b-75c0-4504-b90f-05e742e44a88.aspx) method. Given a user name, the role provider system returns a list of roles to which the user belongs.</span></span>
  
    
    
<span data-ttu-id="e2fce-p115">Der Mitgliedschaftsanbieter ist für die Überprüfung der Anmeldeinformationen mithilfe der  [System.Web.Security.Membership.ValidateUser](http://msdn.microsoft.com/library/33f4af0b-75c0-4504-b90f-05e742e44a88.aspx)-Methode (nun in SharePoint erforderlich) verantwortlich. Das tatsächliche Benutzertoken wird jedoch von einem Sicherheitstokendienst (Security Token Service, STS) erstellt. Der STS erstellt das Benutzertoken aus dem vom Mitgliedschaftsanbieter überprüften Benutzernamen und aus der Menge der dem Benutzernamen zugeordneten Gruppenmitgliedschaften, die vom Mitgliedschaftsanbieter bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="e2fce-p115">The membership provider is responsible for validating the credential information by using the  [System.Web.Security.Membership.ValidateUser](http://msdn.microsoft.com/library/33f4af0b-75c0-4504-b90f-05e742e44a88.aspx) method (required now in SharePoint). But, the actual user token is created by the security token service (STS). The STS creates the user token from the user name validated by the membership provider and from the set of group memberships associated with the user name that are provided by the membership provider.</span></span>
  
    
    

> [!NOTE]
> <span data-ttu-id="e2fce-178">Weitere Informationen zu STS finden Sie unter [Anspruchsbasierte Identität und Konzepte in SharePoint](claims-based-identity-and-concepts-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e2fce-178">[Note:](claims-based-identity-and-concepts-in-sharepoint.md) For more information about STS, see  Claims-based identity and concepts in SharePoint.</span></span> 
  
    
    

<span data-ttu-id="e2fce-p116">Der Rollen-Manager ist optional. Falls ein benutzerdefiniertes Authentifizierungssystem Gruppen nicht unterstützt, ist auch kein Rollen-Manager erforderlich. SharePoint unterstützt einen Mitgliedschaftsanbieter und einen Rollen-Manager pro URL-Zone ( [SPUrlZone](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPUrlZone.aspx) ). Den ASP.NET-Formularrollen sind keine inhärenten Rechte zugeordnet. Stattdessen weist SharePoint den Formularrollen Rechte über seine Richtlinien und Autorisierung zu. In SharePoint ist die formularbasierte Authentifizierung in das anspruchsbasierte Identitätsmodell integriert. Falls Sie eine zusätzliche Erweiterung benötigen, um die Grenze von einem Rollenanbieter pro URL-Zone zu umgehen, können Sie auf Anspruchsanbieter vertrauen.</span><span class="sxs-lookup"><span data-stu-id="e2fce-p116">The role manager is optional. If a custom authentication system does not support groups, a role manager is not necessary. SharePoint supports one membership provider and one role manager per URL zone ( [SPUrlZone](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPUrlZone.aspx) ). The ASP.NET forms roles have no inherent rights associated with them. Instead, SharePoint assigns rights to the forms roles through its policies and authorization. In SharePoint, the forms-based authentication is integrated with the claims-based identity model. If you need additional augmentation to bypass the limit of having one role provider per URL zone, you can rely on claims providers.</span></span>
  
    
    

> [!NOTE]
> <span data-ttu-id="e2fce-186">Weitere Informationen zur anspruchsbasierten Identität und zu Anspruchsanbietern finden Sie unter [Anspruchsbasierte Identität und Konzepte in SharePoint](claims-based-identity-and-concepts-in-sharepoint.md) und [Anspruchsanbieter in SharePoint](claims-provider-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e2fce-186">[Note:](claims-based-identity-and-concepts-in-sharepoint.md) For more information about claims-based identity and claims providers, see  [Claims-based identity and concepts in SharePoint](claims-provider-in-sharepoint.md) and Claims provider in SharePoint.</span></span> 
  
    
    

<span data-ttu-id="e2fce-p117">Bei der passiven Anmeldung von Mitgliedern und Rollen in ASP.NET erfolgt die Anmeldung durch das Umleiten des Clients an eine Webseite, auf der die ASP.NET-Anmeldesteuerelemente gehostet sind. Nachdem das Identitätsobjekt, das eine Benutzeridentität darstellt, erstellt wurde, konvertiert SharePoint dies in ein  [ClaimsIdentity](https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx) -Objekt (das eine anspruchsbasierte Darstellung eines Benutzers ist).</span><span class="sxs-lookup"><span data-stu-id="e2fce-p117">In ASP.NET membership and role passive sign-in, the sign-in happens by redirecting the client to a web page where the ASP.NET log-in controls are hosted. After the identity object that represents a user identity is created, SharePoint converts it to a  [ClaimsIdentity](https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx) object (which represents a claims-based representation of a user).</span></span>
  
> [!NOTE]
> <span data-ttu-id="e2fce-189">Weitere Informationen zum Anmelden an SharePoint finden Sie unter [Eingehende Ansprüche: Anmelden bei SharePoint](incoming-claims-signing-into-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e2fce-189">[Note:](incoming-claims-signing-into-sharepoint.md) For more information about signing into SharePoint, see  Incoming claims: Signing into SharePoint.</span></span> 
  
    
    

<span data-ttu-id="e2fce-p118">SharePoint verwendet die standardmäßige ASP.NET-Rollenanbieterschnittstelle zum Sammeln von Gruppeninformationen zum aktuellen Benutzer. Zum Zweck der Authentifizierung sind Rollen und Gruppen dasselbe: eine Möglichkeit zum Gruppieren von Benutzern in logische Gruppen für die Autorisierung. Jede ASP.NET-Rolle wird als Domänengruppe von SharePoint behandelt.</span><span class="sxs-lookup"><span data-stu-id="e2fce-p118">SharePoint consumes the standard ASP.NET role provider interface to gather group information about the current user. For authentication purposes, roles and groups are the same thing: a way of grouping users into logical sets for authorization. Each ASP.NET role is treated as a domain group by SharePoint.</span></span> 
  
    
    
<span data-ttu-id="e2fce-193">Informationen zum austauschbaren Authentifizierungsframework von ASP.NET finden Sie in der ASP.NET-Entwicklerdokumentation.</span><span class="sxs-lookup"><span data-stu-id="e2fce-193">For information about the pluggable authentication framework provided by ASP.NET, see ASP.NET developer documentation.</span></span>
  
> [!NOTE]
> <span data-ttu-id="e2fce-194">Weitere Informationen zur formularbasierten Authentifizierung finden Sie unter [Formularbasierte Authentifizierung in SharePoint-Produkten und -Technologien (Teil 1): Einführung](http://msdn.microsoft.com/library/e5efd4d7-b369-49f0-a6f7-431d21daff20%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2fce-194">For more information about forms-based authentication, see [Forms authentication in SharePoint products and technologies (Part 1): Introduction](http://msdn.microsoft.com/library/e5efd4d7-b369-49f0-a6f7-431d21daff20%28Office.15%29.aspx).</span></span> 
  
    
    


## <a name="see-also"></a><span data-ttu-id="e2fce-195">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="e2fce-195">See also</span></span>
<span data-ttu-id="e2fce-196"><a name="SP15_AuthenticationAuthorizationSecurity_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="e2fce-196"><a name="SP15_AuthenticationAuthorizationSecurity_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="e2fce-197">Autorisierung, Benutzer, Gruppen und das Objektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e2fce-197">Authorization, users, groups, and the object model in SharePoint</span></span>](authorization-users-groups-and-the-object-model-in-sharepoint.md)
    
  
-  [<span data-ttu-id="e2fce-198">Rolle, die Vererbung von, Erhöhung von Berechtigungen und Kennwortänderungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e2fce-198">Role, inheritance, elevation of privilege, and password changes in SharePoint</span></span>](role-inheritance-elevation-of-privilege-and-password-changes-in-sharepoint.md)
    
  
-  [<span data-ttu-id="e2fce-199">Anspruchsbasierte Identität in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e2fce-199">Claims-based identity in SharePoint</span></span>](claims-based-identity-in-sharepoint.md)
    
  
-  [<span data-ttu-id="e2fce-200">Anspruchsbasierte Identität und-Konzepte in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e2fce-200">Claims-based identity and concepts in SharePoint</span></span>](claims-based-identity-and-concepts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="e2fce-201">Konfiguration, Verwaltung und Ressourcen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e2fce-201">Configuration, administration, and resources in SharePoint</span></span>](configuration-administration-and-resources-in-sharepoint.md)
    
  

