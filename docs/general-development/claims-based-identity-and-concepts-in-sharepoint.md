---
title: "Anspruchsbasierte Identität und Konzepte in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d96c7cf4-2e48-4223-a3c0-42368d079b74
ms.openlocfilehash: 45834f7699463a2ee849edc78e9c7d34166d3bbb
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="claims-based-identity-and-concepts-in-sharepoint"></a><span data-ttu-id="55e3b-102">Anspruchsbasierte Identität und Konzepte in SharePoint</span><span class="sxs-lookup"><span data-stu-id="55e3b-102">Claims-based identity and concepts in SharePoint</span></span>

## <a name="claims-based-identity-model"></a><span data-ttu-id="55e3b-103">Anspruchsbasiertes Identitätsmodell</span><span class="sxs-lookup"><span data-stu-id="55e3b-103">Claims-based identity model</span></span>

<span data-ttu-id="55e3b-p101">Wenn Sie die Ansprüche unterstützende Anwendungen erstellen, bietet dem Benutzer eine Identität für Ihre Anwendung als eine Reihe von Ansprüchen aus. Ein Anspruch den Namen des Benutzers kann, eine andere möglicherweise eine e-Mail-Adresse. Die Idee ist, dass der Anwendung, die von der Anwendung empfangenen Identitätsdaten von einer vertrauenswürdigen Quelle stammen alle Informationen, die sie benötigt, über den Benutzer bei jeder Anforderung zusammen mit kryptografischen Assurance zuweisen ein externen Identitäts-Systems konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p101">When you build claims-aware applications, the user presents an identity to your application as a set of claims. One claim could be the user's name, another might be an email address. The idea here is that an external identity system is configured to give your application all the information it needs about the user with each request, along with cryptographic assurance that the identity data received by your application comes from a trusted source.</span></span>
  
    
    
<span data-ttu-id="55e3b-107">Bei diesem Modell ist eine einmalige Anmeldung viel leichter durchzusetzen, und Ihre Anwendung ist nicht mehr für Folgendes zuständig:</span><span class="sxs-lookup"><span data-stu-id="55e3b-107">Under this model, single sign-on is much easier to achieve, and your application is no longer responsible for the following:</span></span>
  
    
    

- <span data-ttu-id="55e3b-108">Authentifizierung von Benutzern</span><span class="sxs-lookup"><span data-stu-id="55e3b-108">Authenticating users</span></span>
    
  
- <span data-ttu-id="55e3b-109">Speicherung von Benutzerkonten und Kennwörtern</span><span class="sxs-lookup"><span data-stu-id="55e3b-109">Storing user accounts and passwords</span></span>
    
  
- <span data-ttu-id="55e3b-110">Aufruf von Unternehmensverzeichnissen zum Nachschlagen von Benutzeridentitätsdetails</span><span class="sxs-lookup"><span data-stu-id="55e3b-110">Calling to enterprise directories to look up user identity details</span></span>
    
  
- <span data-ttu-id="55e3b-111">Integration mit Identitätssystemen anderer Plattformen oder Unternehmen</span><span class="sxs-lookup"><span data-stu-id="55e3b-111">Integrating with identity systems from other platforms or companies</span></span>
    
  
<span data-ttu-id="55e3b-p102">Bei diesem Modell entscheidet die Anwendung identitätsbezogene basierend auf vom Benutzer bereitgestellte Ansprüche. Dies könnte aus einfachen Anwendung Personalisierung mit den Vornamen des Benutzers, für das die Benutzer Zugriff auf einer höheren Wert Features und Ressourcen in der Anwendung zu autorisieren.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p102">Under this model, your application makes identity-related decisions based on claims supplied by the user. This could be anything from simple application personalization with the user's first name, to authorizing the user to access higher value features and resources in your application.</span></span>
  
    
    
<span data-ttu-id="55e3b-114">Die folgenden Abschnitte erläutern die Terminologie und Konzepte, die Ihnen das Verständnis der anspruchsbasierten identitätsarchitektur erleichtern.</span><span class="sxs-lookup"><span data-stu-id="55e3b-114">The following sections introduce terminology and concepts to help you understand the claims-based identity architecture.</span></span>
  
    
    

### <a name="identity-a-set-of-attributes-that-describe-an-entity"></a><span data-ttu-id="55e3b-115">Identität: Eine Reihe von Attributen, die eine Entität beschreiben</span><span class="sxs-lookup"><span data-stu-id="55e3b-115">Identity: A set of attributes that describe an entity</span></span>

<span data-ttu-id="55e3b-116">Unter "Identität" ist in diesem Kontext eine Gruppe von Attributen zu verstehen, die einen Benutzer oder eine andere Entität in einem System beschreibt, das Sie absichern möchten.</span><span class="sxs-lookup"><span data-stu-id="55e3b-116">Identity is a set of attributes that describe a user, or some other entity, in a system that you want to secure.</span></span>
  
    
    

### <a name="claim-a-piece-of-identity-information"></a><span data-ttu-id="55e3b-117">Forderung: Eine Information Identität</span><span class="sxs-lookup"><span data-stu-id="55e3b-117">Claim: A piece of identity information</span></span>

<span data-ttu-id="55e3b-p103">Stellen Sie sich eine Forderung als eine Information Identität (beispielsweise Name, e-Mail-Adresse, Alter oder die Mitgliedschaft in der Rolle ""). Die weitere Ansprüche Ihrer Anwendung empfängt, je mehr Sie wissen über Ihre Benutzer. Diese werden "Ansprüchen" statt "Attribute" bezeichnet, wie häufig zum Beschreiben von Unternehmensverzeichnissen, aufgrund der Übermittlungsmethode verwendet wird. In diesem Modell wird die Anwendung nicht Benutzerattribute in einem Verzeichnis nachgeschlagen werden. Stattdessen der Benutzer bietet Forderungen an den die Anwendung und Ihre Anwendung überprüft werden. Jeder Anspruch erfolgt durch einen Aussteller, und nur ähnlich, wie Sie den Aussteller vertrauen, vertrauen den Anspruch. Beispielsweise verlassen Sie eine Forderung vorgenommene Ihres Unternehmens Domänencontroller mehr als eine Forderung vertrauenswürdigen vom Benutzer vorgenommen.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p103">Think of a claim as a piece of identity information (for example, name, email address, age, or membership in the Sales role). The more claims your application receives, the more you know about your user. These are called "claims" rather than "attributes," as is commonly used in describing enterprise directories, because of the delivery method. In this model, your application does not look up user attributes in a directory. Instead, the user delivers claims to your application, and your application examines them. Each claim is made by an issuer, and you trust the claim only as much as you trust the issuer. For example, you trust a claim made by your company's domain controller more than you trust a claim made by the user.</span></span>
  
    
    

### <a name="security-token-a-serialized-set-of-claims"></a><span data-ttu-id="55e3b-125">Sicherheitstoken: einen serialisierten Satz von Ansprüchen</span><span class="sxs-lookup"><span data-stu-id="55e3b-125">Security token: A serialized set of claims</span></span>

<span data-ttu-id="55e3b-p104">Der Benutzer bietet eine Reihe von Ansprüchen Ihrer Anwendung mit einer Anforderung. In einem Webdienst werden diese Ansprüche in der Kopfzeile der Sicherheit von SOAP-Umschlag übermittelt. In einer browserbasierten Webanwendung die Ansprüche von Browser des Benutzers über HTTP POST eintreffen, und möglicherweise später in einem Cookie zwischengespeichert werden, bei Bedarf eine Sitzung ist. Unabhängig davon, wie diese Ansprüche zu gelangen müssen sie serialisiert werden. Ein Sicherheitstoken ist ein serialisierten Ansprüche, die von der ausstellenden Zertifizierungsstelle signiert wurde. Die Signatur ist wichtig: können Sie sicherstellen, dass der Benutzer nicht nur von Ansprüchen und an Sie werden gesendet. In niedrige Sicherheitsstufe Situationen, in dem Kryptografie nicht erforderlich oder erwünscht ist, können nicht signierte Token, aber dieses Szenario wird in diesem Artikel nicht beschrieben.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p104">The user delivers a set of claims to your application with a request. In a web service, these claims are carried in the security header of the SOAP envelope. In a browser-based web application, the claims arrive through an HTTP POST from the user's browser, and may later be cached in a cookie if a session is desired. Regardless of how these claims arrive, they must be serialized. A security token is a serialized set of claims that is digitally signed by the issuing authority. The signature is important: it gives you assurance that the user did not just make up claims and send them to you. In low-security situations where cryptography is not necessary or desired, you can use unsigned tokens, but that scenario is not described in this article.</span></span>
  
    
    
<span data-ttu-id="55e3b-p105">Eine der Hauptfunktionen in Windows Identity Foundation (WIF) ist die Möglichkeit des Erstellens und Lesens von Sicherheitstoken. WIF und Microsoft .NET Framework sind für sämtliche kryptografischen Aufgaben zuständig und legen Ihrer Anwendung eine Gruppe von Ansprüchen vor, die diese lesen kann.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p105">One of the core features in Windows Identity Foundation (WIF) is the ability to create and read security tokens. WIF and the Microsoft .NET Framework handle all of the cryptographic work, and present your application with a set of claims that it can read.</span></span>
  
    
    

### <a name="security-token-service-sts"></a><span data-ttu-id="55e3b-135">Sicherheitstokendienst</span><span class="sxs-lookup"><span data-stu-id="55e3b-135">Security token service (STS)</span></span>

<span data-ttu-id="55e3b-p106">Ein Sicherheitstokendienst (STS) ist die Grundstruktur, die erstellt, auf Anzeichen für und Sicherheitstoken entsprechend die interoperablen Protokolle im Abschnitt "Standards" dieses Artikels beschriebenen Probleme. Es gibt viele arbeiten bei Implementierung dieser Protokolle, aber WIF all dies für Sie lässt sich für eine Person, die keiner Protokolle ist ein STS Einstieg Experten und mit minimalem Aufwand ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p106">A security token service (STS) is the plumbing that builds, signs, and issues security tokens according to the interoperable protocols discussed in the "Standards" section of this article. There is a lot of work that goes into implementing these protocols, but WIF does all of this work for you, making it possible for someone who is not a protocols expert to get an STS up and running with little effort.</span></span> 
  
    
    
<span data-ttu-id="55e3b-p107">WIF macht das Erstellen eines eigenen STS einfach. Sie müssen lediglich bestimmen, wie die Logik samt Durchsetzungsregeln (d. h. die Sicherheitsrichtlinie) implementiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p107">WIF makes it easier to build your own STS. It is up to you to figure out how to implement the logic, or rules, that enforce it (often referred to as security policy).</span></span>
  
    
    

### <a name="issuing-authority"></a><span data-ttu-id="55e3b-140">Ausstellende Stelle</span><span class="sxs-lookup"><span data-stu-id="55e3b-140">Issuing authority</span></span>

<span data-ttu-id="55e3b-p108">Es gibt viele verschiedene Typen von ausstellenden Behörden, von Domänencontrollern, die Kerberos-Tickets Zertifizierungsstellen ausstellen, die x. 509-Zertifikate aus. Welche Art von Autorität erläutert in diesem Artikel Aspekte Sicherheitstoken, die Ansprüche enthalten. Diese ausstellende Stelle ist a Web Application oder Webdienst, der Sicherheitstoken ausstellt. Es muss die richtige Ansprüche erhält das Ziel relying Party und der Benutzer, der die Anforderung ausstellen, und möglicherweise verantwortlich für die Interaktion mit Benutzerspeichern zum Nachschlagen von Ansprüchen und Authentifizieren von Benutzern.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p108">There are many different types of issuing authorities, from domain controllers that issue Kerberos tickets, to certificate authorities that issue X.509 certificates. The specific type of authority discussed in this article issues security tokens that contain claims. This issuing authority is a web application or web service that issues security tokens. It must be able to issue the proper claims given the target relying party and the user making the request, and might be responsible for interacting with user stores to look up claims and authenticate users.</span></span>
  
    
    
<span data-ttu-id="55e3b-p109">Unabhängig davon, welche ausstellende Stelle Sie wählen, spielt diese eine Kernrolle in Ihrer Identitätslösung. Wenn Sie die Authentifizierung aus Ihrer Anwendung ausklammern, indem Sie auf Ansprüche setzen, übergeben Sie die Zuständigkeit an diese Stelle und fordern sie auf, die Authentifizierung von Benutzern in Ihrem Auftrag zu übernehmen.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p109">Whatever issuing authority you choose, it plays a central role in your identity solution. When you factor authentication out of your application by relying on claims, you are passing responsibility to that authority and asking it to authenticate users on your behalf.</span></span>
  
    
    

### <a name="relying-parties"></a><span data-ttu-id="55e3b-147">Vertrauende Seiten</span><span class="sxs-lookup"><span data-stu-id="55e3b-147">Relying parties</span></span>

<span data-ttu-id="55e3b-p110">Bei der Erstellung einer Anwendung, die Ansprüche abhängt, erstellen Sie eine relying Party-Anwendung. Synonyme für eine vertrauende Seite einschließen "Ansprüche unterstützende Anwendung" und "Claims-based Application". Webanwendungen und Webdienste können beide vertrauenden Seiten sein.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p110">When you build an application that relies on claims, you are building a relying party application. Synonyms for a relying party include "claims-aware application" and "claims-based application". Web applications and web services can both be relying parties.</span></span>
  
    
    
<span data-ttu-id="55e3b-p111">Eine relying Party-Anwendung von einem STS ausgestellte Token verbraucht und extrahiert Ansprüche von Token für die Identität für die Nutzung Aufgaben im Zusammenhang mit. STS unterstützt zwei Arten von relying party Anwendung: ASP.NET Webanwendungen und Windows Communication Foundation (WCF)-Webdienste.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p111">A relying party application consumes tokens issued by an STS and extracts claims from tokens to use them for identity related tasks. The STS supports two types of relying party application: ASP.NET web applications, and Windows Communication Foundation (WCF) web services.</span></span>
  
    
    

### <a name="standards"></a><span data-ttu-id="55e3b-153">Standards</span><span class="sxs-lookup"><span data-stu-id="55e3b-153">Standards</span></span>

<span data-ttu-id="55e3b-p112">All dies interoperable, tätigen WS-* Standards im vorherigen Szenario verwendet werden. Richtlinie wird mithilfe von WS-MetadataExchange abgerufen, und die Richtlinie selbst wird gemäß der Spezifikation WS-Policy strukturiert. Der STS stellt Endpunkte, die die Spezifikation WS-Trust implementieren, die beschreibt, wie zum Anfordern und Empfangen von Sicherheitstoken zur Verfügung. Die meisten Security Token services heute Problem Token mit Security Assertion Markup Language (SAML) formatiert. SAML ist ein anerkannten XML-Vokabular, die zur Darstellung von Ansprüchen Authentifizierungsdienste verwendet werden können. Oder in einer Situation für mehrere Plattformen Dadurch können Sie die Kommunikation mit einem STS auf eine vollständig andere Plattform und einmaliges Anmelden in allen Anwendungen, unabhängig von der Plattform zu erzielen.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p112">To make all of this interoperable, several WS-* standards are used in the previous scenario. Policy is retrieved by using WS-MetadataExchange, and the policy itself is structured according to the WS-Policy specification. The STS exposes endpoints that implement the WS-Trust specification, which describes how to request and receive security tokens. Most security token services today issue tokens formatted with Security Assertion Markup Language (SAML). SAML is an industry-recognized XML vocabulary that can be used to represent claims in an interoperable way. Or, in a multiplatform situation, this enables you to communicate with an STS on an entirely different platform and achieve single sign-on across all of your applications, regardless of platform.</span></span>
  
    
    

### <a name="browser-based-applications"></a><span data-ttu-id="55e3b-160">Browserbasierte Anwendungen</span><span class="sxs-lookup"><span data-stu-id="55e3b-160">Browser-based applications</span></span>

<span data-ttu-id="55e3b-p113">Nicht nur intelligente Clients können mit dem anspruchsbasierten Identitätsmodell arbeiten. Browserbasierte Anwendungen (die als passive Clients bezeichnet werden) können dies auch, was im folgenden Abschnitt beschrieben wird.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p113">Smart clients are not the only ones who can use the claims-based identity model. Browser-based applications (also referred to as passive clients) can also use it. The following scenario describes how this works.</span></span>
  
    
    
<span data-ttu-id="55e3b-p114">Zunächst verweist ein Benutzer einen Browser an eine Ansprüche unterstützende Anwendung (die Anwendung mit vertrauender Seite). Die Webanwendung leitet den Browser an den Sicherheitstokendienst um, damit der Benutzer authentifiziert werden kann. Der Sicherheitstokendienst wird in einer einfachen Webanwendung gehostet, welche die eingehende Anforderung liest, den Benutzer mittels HTTP-Standardmechanismen authentifiziert und anschließend ein SAML-Token erstellen. Danach antwortet die Webanwendung mit einem ECMAScript (JavaScript, JScript)-Codefragment, das bewirkt, dass der Browser einen HTTP POST-Befehl auslöst, der das SAML-Token zurück zur vertrauenden Seite sendet. Der Hauptteil dieses POST-Befehls enthält die Ansprüche, die die vertrauende Seite angefordert hat. An dieser Stelle fügt die vertrauende Seite die Ansprüche häufig einem Cookie hinzu, damit der Benutzer nicht bei jeder Anforderung umgeleitet werden muss.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p114">First, the user points a browser at a claims-aware web application (the relying party application). The web application redirects the browser to the STS so that the user can be authenticated. The STS is hosted in a simple web application that reads the incoming request, authenticates the user by using standard HTTP mechanisms, and then creates a SAML token and replies with a piece of ECMAScript (JavaScript, JScript) code that causes the browser to initiate an HTTP POST that sends the SAML token back to the relying party. The body of this POST contains the claims that the relying party requested. At this point, it is common for the relying party to package the claims into a cookie so that the user does not have to be redirected for each request.</span></span>
  
    
    

### <a name="claims-to-windows-token-service-c2wts"></a><span data-ttu-id="55e3b-169">Forderungen an den Windows-Tokendienst (c2WTS)</span><span class="sxs-lookup"><span data-stu-id="55e3b-169">Claims to Windows Token Service (c2WTS)</span></span>

<span data-ttu-id="55e3b-p115">Der Forderungen an den Windows-Tokendienst (c2WTS) ist eine Komponente von Windows Identity Foundation (WIF). Der c2WTS extrahiert UPN-Ansprüche (User Principal Name, Benutzerprinzipalname) aus Nicht-Windows-Sicherheitstoken (z. B. SAML- und X.509-Token) und generiert Windows-Sicherheitstoken auf Identitätswechselebene. Dadurch kann die Anwendung auf der vertrauenden Seite die Identität des Benutzers übernehmen. Dies ist ggf. für den Zugriff auf Back-End-Ressourcen wie Computer mit Microsoft SQL Server erforderlich, die für den Computer mit der Anwendung der vertrauenden Seite als extern gelten.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p115">The Claims to Windows Token Service (c2WTS) is a feature of Windows Identity Foundation (WIF). The c2WTS extracts user principal name (UPN) claims from non-Windows security tokens, such as SAML and X.509 tokens, and generates impersonation-level Windows security tokens. This allows a relying party application to impersonate the user. This might be needed to access back-end resources, such as Microsoft SQL Servers, that are external to the computer running the relying party application.</span></span>
  
    
    
<span data-ttu-id="55e3b-p116">Die c2WTS ist ein Windowsdienst, der als Teil des WIF installiert ist. Aus Sicherheitsgründen arbeitet die c2WTS nur für eine einzelne Opt in. Manuell gestartet werden müssen, und er wird als lokales Systemkonto ausgeführt. Ein Administrator muss die c2WTS mit einer Liste der zulässigen Anrufer auch manuell konfigurieren. Standardmäßig ist die Liste leer.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p116">The c2WTS is a Windows service that is installed as part of WIF. For security reasons, the c2WTS works only on an opt-in basis. It must be started manually and it runs as the local system account. An administrator must also manually configure the c2WTS with a list of allowed callers. By default, the list is empty.</span></span> 
  
    
    
<span data-ttu-id="55e3b-p117">Wenn die relying Party-Anwendung als lokales Systemkonto ausgeführt wird, muss es nicht die c2WTS verwenden. Jedoch ist die relying Party-Anwendung wird als das Netzwerkdienstkonto ausgeführt, oder einer Anwendung ASP.NET, beispielsweise es müssen möglicherweise die c2WTS Zugriff auf Ressourcen auf einem anderen Computer verwenden.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p117">If your relying party application runs as the local system account, it does not need to use the c2WTS. But, if your relying party application runs as the network service account, or is an ASP.NET application, for example, it might need to use the c2WTS to access resources on another computer.</span></span>
  
    
    
<span data-ttu-id="55e3b-p118">Nehmen Sie an, dass Sie über eine Webfarm verfügen, die von einem Server besteht, die eine Anwendung ASP.NET greift auf einer SQL-Datenbank auf einem Back-End-Server ausgeführt. Diese Anwendung Ansprüche unterstützenden werden sollen. Aber die Anwendung kann nicht mit den Anspruch, den sie aus einem STS erhält die SQL-Datenbank zugreifen. Stattdessen wird die c2WTS umzuwandelnde UPN-Anspruch auf einem Windows-Sicherheitstoken verwendet. Dies ermöglicht es Zugriff auf die SQL-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="55e3b-p118">Suppose that you have a web farm that consists of a server that runs an ASP.NET application, which accesses a SQL database on a back-end server. You want to make this application claims-aware. But, the application can't access the SQL database by using the claim that it receives from an STS. Instead, it uses the c2WTS to convert the UPN claim to a Windows security token. This allows it to access the SQL database.</span></span>
  
> [!NOTE]
> <span data-ttu-id="55e3b-186">Wenn Sie den Zugriff auf Ressourcen auf einem anderen Server für eine Anwendung ermöglichen, muss ein Domänenadministrator den Active Directory-Verzeichnisdienst für eingeschränkte Delegierung konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="55e3b-186">Note: To allow an application to access resources on a different server, a domain administrator must configure the Active Directory directory service to enable constrained delegation.</span></span> <span data-ttu-id="55e3b-187">Informationen zum Aktivieren der eingeschränkten Delegierung finden Sie unter [Gewusst wie: Verwenden des Protokollübergangs und der eingeschränkten Delegierung in ASP.NET 2.0]((http://msdn.microsoft.com/de-DE/library/ms998355.aspx)).</span><span class="sxs-lookup"><span data-stu-id="55e3b-187">For information about how to enable constrained delegation, see  [How to: Use protocol transition and constrained eelegation in ASP.NET 2.0]((http://msdn.microsoft.com/de-DE/library/ms998355.aspx)).</span></span> 
  
    
    


## <a name="see-also"></a><span data-ttu-id="55e3b-188">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="55e3b-188">See also</span></span>
<span data-ttu-id="55e3b-189"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="55e3b-189"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="55e3b-190">Authentifizierung, Autorisierung und Sicherheit in SharePoint</span><span class="sxs-lookup"><span data-stu-id="55e3b-190">Authentication, authorization, and security in SharePoint</span></span>](authentication-authorization-and-security-in-sharepoint.md)
    
  
-  [<span data-ttu-id="55e3b-191">Stellvertretung, Verbund und Authentifizierung Beispielszenario SharePoint</span><span class="sxs-lookup"><span data-stu-id="55e3b-191">Sample delegation, federation, and authentication scenario in SharePoint</span></span>](sample-delegation-federation-and-authentication-scenario-in-sharepoint.md)
    
  
-  [<span data-ttu-id="55e3b-192">Anspruchsbasierte Identität - Begriffsdefinitionen</span><span class="sxs-lookup"><span data-stu-id="55e3b-192">Claims-based identity term definitions</span></span>](claims-based-identity-term-definitions.md)
    
  

