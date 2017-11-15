---
title: Anspruchsanbieter in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 5918d5b6-5fd6-4f41-9473-a15b1491d056
ms.openlocfilehash: cd935e975f4c469079905c1afe242da790f33e2f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="claims-provider-in-sharepoint"></a><span data-ttu-id="9d960-102">Anspruchsanbieter in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9d960-102">Claims provider in SharePoint</span></span>

## <a name="claims-providers"></a><span data-ttu-id="9d960-103">Anspruchsanbieter</span><span class="sxs-lookup"><span data-stu-id="9d960-103">Claims providers</span></span>

<span data-ttu-id="9d960-p101">Ein Anspruchsanbieter in SharePoint Server Probleme Ansprüche und Pakete Ansprüche in Sicherheitstokens, d. h., in dem Token des Benutzers. Wenn ein Benutzer bei SharePoint Server anmeldet, wird das Zugriffstoken des Benutzers überprüft und zur Anmeldung bei SharePoint verwendet.</span><span class="sxs-lookup"><span data-stu-id="9d960-p101">A claims provider in SharePoint Server issues claims and packages claims into security tokens, that is, into the user's token. When a user signs in to SharePoint Server, the user's token is validated and then used to sign in to SharePoint.</span></span>
  
    
    
<span data-ttu-id="9d960-106">Ein Anspruchsanbieter in SharePoint hat zwei Rollen: Erweiterung und Auswahl.</span><span class="sxs-lookup"><span data-stu-id="9d960-106">A claims provider in SharePoint has two roles: augmentation and picking.</span></span>
  
    
    

> <span data-ttu-id="9d960-107">**Hinweis:** Weitere Informationen zum Erstellen eines Anspruchsanbieters finden Sie unter  [Gewusst wie: Erstellen eines Anspruchsanbieters in SharePoint](how-to-create-a-claims-provider-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="9d960-107">**Note** For information about how to create a claims provider, see  [How to: Create a claims provider in SharePoint](how-to-create-a-claims-provider-in-sharepoint.md).</span></span> 
  
    
    


### <a name="claims-augmentation"></a><span data-ttu-id="9d960-108">Anspruchserweiterung</span><span class="sxs-lookup"><span data-stu-id="9d960-108">Claims augmentation</span></span>

<span data-ttu-id="9d960-p102">In der Erweiterungsfunktion erweitert ein Anspruchsanbieter ein Benutzertoken während der Anmeldung mit Ansprüchen. Durch die Anspruchserweiterung kann eine Anwendung zusätzliche Ansprüche in das Token des Benutzers aufnehmen. Beispielsweise kann bei der Windows-basierten Anmeldung der Active Directory-Verzeichnisdienst alle Sicherheitsgruppen eines Benutzers in das Windows-Token des Benutzers aufnehmen. Bei der anspruchsbasierten Anmeldung kann eine CRM-Anwendung (Customer Relationship Management, Kundenbeziehungsmanagement) Rollen aus einer CRM-Datenbank erweitern. Ressourcen können für diese Ansprüche autorisiert werden, indem diese Ansprüche in das Token des Benutzers eingeschlossen werden. Das heißt, mit diesen Ansprüchen wird bestimmt, ob ein bestimmter Benutzer Zugriff auf bestimmte Ressourcen hat.</span><span class="sxs-lookup"><span data-stu-id="9d960-p102">In the augmentation role, a claims provider augments a user token with claims during sign-in. Claims augmentation enables an application to augment additional claims into the user's token. For example, with Windows-based log-in, the Active Directory directory service can augment all of a user's security groups into the user's Windows token. With claims-based log-in, a customer relationship management (CRM) application can augment roles from a CRM database. By including these claims in the user's token, resources can be authorized against these claims. That is, these claims are used to determine whether a particular user has access to specific resources.</span></span>
  
    
    

### <a name="claims-picking"></a><span data-ttu-id="9d960-115">Anspruchsauswahl</span><span class="sxs-lookup"><span data-stu-id="9d960-115">Claims picking</span></span>

<span data-ttu-id="9d960-p103">In der Auswahlfunktion bietet ein Anspruchsanbieter die Funktionalitäten Auflistung, Auflösung, Suche und benutzerfreundliche Anzeige von Ansprüchen bei der Personenauswahl. Durch die Anspruchsauswahl kann eine Anwendung Ansprüche in der Personenauswahl anzeigen, z. B. beim Konfigurieren der Sicherheit einer SharePoint-Website oder eines SharePoint-Diensts.</span><span class="sxs-lookup"><span data-stu-id="9d960-p103">In the picking role, a claims provider provides listing, resolve, search, and friendly display of claims functionality in the people picker. Claims picking enables an application to surface claims in the people picker, for example when configuring the security of a SharePoint site or SharePoint service.</span></span> 
  
    
    

## <a name="claims-provider-use-scenarios"></a><span data-ttu-id="9d960-118">Szenarien für die Verwendung von Anspruchsanbietern</span><span class="sxs-lookup"><span data-stu-id="9d960-118">Claims provider use scenarios</span></span>

<span data-ttu-id="9d960-p104">Anspruchsanbieter werden verwendet, um verschiedene Szenarien zu lösen. Es folgen einige Beispiele für Szenarien, zum Lösen Anspruchsanbieter verwenden können.</span><span class="sxs-lookup"><span data-stu-id="9d960-p104">Claims providers are used to solve different scenarios. The following are some examples of the scenarios that you can use claims providers to solve.</span></span>
  
    
    

### <a name="list-resolve-and-search"></a><span data-ttu-id="9d960-121">Auflisten, Auflösen und Suchen</span><span class="sxs-lookup"><span data-stu-id="9d960-121">List, resolve, and search</span></span>

<span data-ttu-id="9d960-p105">In SharePoint Server sind integrierte Ansprüche zu Liste aktivieren Anbieter auflösen und suchen für integrierte Authentifizierungsanbieter. Beispiele für integrierte Authentifizierungsanbieter sind Windows Active Directory, formularbasierte Authentifizierung und vertrauenswürdigen Security Assertion Markup Language (SAML) tokenherausgebern - d. h., Sicherheitstokendienst (Security Token Service, STS).</span><span class="sxs-lookup"><span data-stu-id="9d960-p105">In SharePoint Server, there are built-in claims providers to enable list, resolve, and search for built-in authentication providers. Examples of built-in authentication providers are Windows Active Directory, forms-based authentication, and trusted Security Assertion Markup Language (SAML) token issuers—that is, a security token service (STS).</span></span> 
  
    
    
<span data-ttu-id="9d960-p106">Für einen vertrauenswürdigen SAML-tokenherausgeber bietet SharePoint Server oder in den keine. Wenn ein Benutzer einen Wert eingibt, löst SharePoint Server immer sie. Dies bedeutet, dass bei Eingabe von adam@contoso.comdie Personenauswahl den Wert annimmt. Dies ist, da es keine Industriestandard ist, die gibt an, wie ein STS aufgelöst wird, Suche implementiert oder listet Forderung Werte.</span><span class="sxs-lookup"><span data-stu-id="9d960-p106">For a trusted SAML token issuer, SharePoint Server does not offer list or search. When a user enters some value, SharePoint Server always resolves it. This means that if you enter adam@contoso.com, the people picker accepts the value. This is because there is no industry standard that specifies how an STS resolves, implements search, or lists claim values.</span></span>
  
    
    
<span data-ttu-id="9d960-p107">Benutzer können den integrierten Anspruchsanbieter zum Implementieren benutzerdefinierter Features für Suche, Namensauflösung und Auflistung überschreiben. Dies ist sehr nützlich in Szenarien wie der Verwendung eines vertrauenswürdigen Herausgebers von SAML-Token.</span><span class="sxs-lookup"><span data-stu-id="9d960-p107">Users can override the built-in claims provider to implement custom search, name resolution, and list features. This is very useful in scenarios like using a trusted SAML token issuer.</span></span>
  
    
    

### <a name="authenticated-users-or-all-users-claims"></a><span data-ttu-id="9d960-130">Authentifizierte Benutzer oder "Alle Benutzer"-Ansprüche</span><span class="sxs-lookup"><span data-stu-id="9d960-130">Authenticated users or All Users claims</span></span>

<span data-ttu-id="9d960-p108">In SharePoint Server sind einige bestimmte integrierte Anspruchsanbietern, die Implementierung von Unterstützung für Konzepte wie authentifizierten Benutzernzu ermöglichen. Dies ist auch bekannt als ein Anspruch Alle Benutzer . In diesem Szenario können Sie alle Benutzer aus einer bestimmten Authentifizierungsanbieter Zugriffsrechte.</span><span class="sxs-lookup"><span data-stu-id="9d960-p108">In SharePoint Server, there are some specific built-in claims providers that enable implementation support for concepts like authenticated users. This is also known as an All Users claim. This scenario enables you to grant rights to all users from a given authentication provider.</span></span>
  
    
    

> <span data-ttu-id="9d960-134">**Hinweis:** Bei einem Authentifizierungsanbieter kann es sich um Windows Active Directory, formularbasierte Authentifizierung oder einen vertrauenswürdigen Herausgeber von SAML-Token (d. h. einen STS) handeln.</span><span class="sxs-lookup"><span data-stu-id="9d960-134">**Note** An authentication provider can be a Windows Active Directory, forms-based authentication, or a trusted SAML token issuer (that is, an STS).</span></span> 
  
    
    

<span data-ttu-id="9d960-p109">In SharePoint Server ist auch ein Anspruchsanbieters für Systeme, das einige interner Ansprüche, die von einem taxonomiedienst verwendete hinzufügt. Es wird beispielsweise Identität und Application Pool Farmkonto.</span><span class="sxs-lookup"><span data-stu-id="9d960-p109">In SharePoint Server, there is also a systems claims provider that adds some internal claims used by a taxonomy service. For example, it adds farm identity and application pool account.</span></span>
  
    
    

### <a name="adding-claims-to-an-original-token"></a><span data-ttu-id="9d960-137">Hinzufügen von Ansprüchen zu einem ursprünglichen Token</span><span class="sxs-lookup"><span data-stu-id="9d960-137">Adding claims to an original token</span></span>

<span data-ttu-id="9d960-p110">Einige der integrierten Anspruchsanbieter werden auch verwendet, um die Ansprüche aus dem ursprünglichen "Token" hinzuzufügen. Das Wort "Token" wird in Anführungszeichen gesetzt, da einige Authentifizierungsanbieter, z. B. die formularbasierte Authentifizierung (d. h. ASP.NET-Mitgliedschafts- und Rollenanbieter), kein echtes Token bereitstellen. In diesem Fall können Sie dieses Token aus einer konzeptionellen Perspektive betrachten.</span><span class="sxs-lookup"><span data-stu-id="9d960-p110">Some of the built-in claims providers are also used to add the claims from the original "token". The word "token" is marked in quotes because some authentication providers, for example, forms-based authentication (that is, ASP.NET membership and role providers), do not provide a real token. In this case, think of this token from a conceptual perspective.</span></span>
  
    
    
<span data-ttu-id="9d960-p111">Möglicherweise müssen dem ursprünglichen Anspruchstoken des Benutzers zusätzliche Ansprüche hinzugefügt werden. In diesem Szenario kann ein Anspruchsanbieter erforderlich sein. Beispielsweise kann ein Anspruchsanbieter erforderlich sein, um dem ursprünglichen Anspruchstoken des Benutzers SAP-Rollen hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="9d960-p111">It might be necessary to add additional claims to a user's original claims token. For this scenario, a claims provider might be needed. For example, a claims provider might be needed to add SAP roles to a user's original claims token.</span></span>
  
    
    

### <a name="identity-not-from-original-token"></a><span data-ttu-id="9d960-144">Identität nicht vom ursprünglichen Token</span><span class="sxs-lookup"><span data-stu-id="9d960-144">Identity not from original token</span></span>

<span data-ttu-id="9d960-p112">Nehmen Sie ein Szenario an, in dem das System einige spezifische Anforderungen für die Personenauswahl und Anspruchstoken aufweist. In diesem Szenario kennen Sie die Identität des Benutzers basierend auf der Microsoft .NET Passport Unique ID (PUID) und dem ursprünglichen Benutzer. Die Informationen über den Benutzer stammen jedoch nicht aus dem ursprünglichen Benutzertoken, sondern aus Ihrem benutzerdefinierten Active Directory. Sie verwenden auch einige zusätzliche Active Directory-Gruppen, denen der Benutzer angehören kann, die nicht im ursprünglichen Benutzertoken (von Windows Live ID ausgegeben) enthalten sind. In diesem Szenario können Sie einen Anspruchsanbieter für Ihre systemspezifischen Anforderungen erstellen.</span><span class="sxs-lookup"><span data-stu-id="9d960-p112">Assume a scenario where your system has some specific requirements for people picking and token claims. In this scenario, you know the identity of the user based on the Microsoft .NET Passport Unique ID (PUID) and the original user. However, the information about the user does not come from the original user token; it comes from your custom Active Directory. You also have some additional Active Directory groups that the user may belong to, which are not contained in the original user token (issued by Windows Live ID). In this scenario, you can build a claims provider to meet your system-specific needs.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="9d960-150">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="9d960-150">Additional resources</span></span>
<span data-ttu-id="9d960-151"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9d960-151"></span></span>


-  [<span data-ttu-id="9d960-152">Anspruchsbasierte Identität in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9d960-152">Claims-based identity in SharePoint</span></span>](claims-based-identity-in-sharepoint.md)
    
  
-  [<span data-ttu-id="9d960-153">Eingehende Ansprüche: Anmelden bei SharePoint</span><span class="sxs-lookup"><span data-stu-id="9d960-153">Incoming claims: Signing into SharePoint</span></span>](incoming-claims-signing-into-sharepoint.md)
    
  
-  [<span data-ttu-id="9d960-154">Vorgehensweise: Erstellen ein anspruchsanbieters in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9d960-154">How to: Create a claims provider in SharePoint</span></span>](how-to-create-a-claims-provider-in-sharepoint.md)
    
  
-  [<span data-ttu-id="9d960-155">Vorgehensweise: POST eines anspruchsanbieters in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9d960-155">How to: Deploy a claims provider in SharePoint</span></span>](how-to-deploy-a-claims-provider-in-sharepoint.md)
    
  

