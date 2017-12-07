---
title: "Erstellen von SharePoint-Add-Ins, die eine Autorisierung mit hoher Vertrauenswürdigkeit verwenden"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: d39ab5425d0ba60f47dbf2902e4c3cd1e6d4c689
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="creating-sharepoint-add-ins-that-use-high-trust-authorization"></a><span data-ttu-id="61cea-102">Erstellen von SharePoint-Add-Ins, die eine Autorisierung mit hoher Vertrauensstellung verwenden</span><span class="sxs-lookup"><span data-stu-id="61cea-102">Creating SharePoint Add-ins that use high-trust authorization</span></span>
<span data-ttu-id="61cea-103">Erfahren Sie mehr über besonders vertrauenswürdige SharePoint-Add-Ins, die digitale Zertifikate verwenden, um eine Vertrauensstellung zwischen SharePoint und den Remotekomponenten einzurichten, die auf SharePoint zugreifen.</span><span class="sxs-lookup"><span data-stu-id="61cea-103">Learn about high-trust SharePoint Add-ins, which use digital certificates to establish trust between SharePoint and the remote components that access SharePoint.</span></span>
 

 <span data-ttu-id="61cea-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="61cea-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

 <span data-ttu-id="61cea-107">**Von:**</span><span class="sxs-lookup"><span data-stu-id="61cea-107">**Provided by:**</span></span>
 
<span data-ttu-id="61cea-108">Steve Peschka, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="61cea-108">Steve Peschka, Microsoft Corporation</span></span>

<span data-ttu-id="61cea-109">Siew Moi Khor, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="61cea-109">Siew Moi Khor, Microsoft Corporation</span></span>
 

## <a name="overview-of-high-trust-sharepoint-add-ins"></a><span data-ttu-id="61cea-110">Übersicht über besonders vertrauenswürdige SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="61cea-110">Overview of high-trust SharePoint Add-ins</span></span>
<span data-ttu-id="61cea-111"><a name="Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="61cea-111"></span></span>

<span data-ttu-id="61cea-p102">Ein besonders vertrauenswürdiges Add-In ist eine vom Anbieter gehostete SharePoint-Add-In, die in einer lokalen SharePoint-Farm installiert wird. Sie kann nicht in Microsoft SharePoint Online installiert werden oder über den Office Store vertrieben werden. Für ein besonders vertrauenswürdiges Add-In wird zum Einrichten der Vertrauensstellung anstelle eines Kontexttoken ein Zertifikat verwendet.</span><span class="sxs-lookup"><span data-stu-id="61cea-p102">A high-trust add-in is a provider-hosted SharePoint Add-in that is installed to an on-premises SharePoint farm. It cannot be installed to Microsoft SharePoint Online or marketed through the Office Store. A high-trust add-in uses a certificate instead of a context token to establish trust.</span></span>
 

 

 <span data-ttu-id="61cea-115">**Hinweis** In diesem Thema erfahren Sie mehr über das besonders vertrauenswürdige Autorisierungssystem für SharePoint-Add-Ins. Praktische Informationen zur Erstellung und Bereitstellung besonders vertrauenswürdiger Add-Ins finden Sie in den folgenden Themen: [Erstellen besonders vertrauenswürdiger SharePoint-Add-Ins](create-high-trust-sharepoint-add-ins.md) [Packen und Veröffentlichen besonders vertrauenswürdiger SharePoint-Add-Ins](package-and-publish-high-trust-sharepoint-add-ins.md)</span><span class="sxs-lookup"><span data-stu-id="61cea-115">**Note**   This topic helps you understand the high-trust authorization system for SharePoint Add-ins. For practical information about creating and deploying high-trust add-ins, see the following topics: [Create high-trust SharePoint Add-ins](create-high-trust-sharepoint-add-ins.md) [Package and publish high-trust SharePoint Add-ins](package-and-publish-high-trust-sharepoint-add-ins.md)</span></span>
 

<span data-ttu-id="61cea-p103">In SharePoint liefert der Sicherheitstokendienst Zugriffstoken für Server-zu-Server-Authentifizierung. Der Sicherheitstokendienst aktiviert vorübergehende Zugriffstoken, um auf andere Anwendungsdienste wie Exchange 2013, Lync 2013 und SharePoint-Add-Ins zuzugreifen. Ein Farmadministrator richtet eine Vertrauensstellung zwischen SharePoint und der anderen Anwendung oder dem Add-In ein, indem er Windows PowerShell-Cmdlets und ein Zertifikat verwendet. Jedes Zertifikat, das verwendet wird, muss von SharePoint mithilfe des Cmdlets  `New-SPTrustedRootAuthority` als vertrauenswürdig eingestuft werden. Außerdem muss jedes Zertifikat bei SharePoint mithilfe des Cmdlets `New-SPTrustedSecurityTokenIssuer` als ein Tokenherausgeber registriert werden.</span><span class="sxs-lookup"><span data-stu-id="61cea-p103">In SharePoint, the security token service (STS) provides access tokens for server-to-server authentication. The STS enables temporary access tokens to access other application services such as Exchange 2013, Lync 2013, and SharePoint Add-ins. A farm administrator establishes trust between SharePoint and the other application or add-in by using Windows PowerShell cmdlets and a certificate. Each certificate that is used must be trusted by SharePoint using the  `New-SPTrustedRootAuthority` cmdlet. Also each certificate must be registered with SharePoint as a token issuer using the `New-SPTrustedSecurityTokenIssuer` cmdlet.</span></span>
 

 

 <span data-ttu-id="61cea-p104">**Hinweis** Der Sicherheitstokendienst ist nicht für die Benutzerauthentifizierung vorgesehen. Daher wird der Sicherheitstokendienst weder auf der Benutzeranmeldeseite, noch im Abschnitt **Authentifizierungsanbieter** der Zentraladministration oder in der Personenauswahl in SharePoint angezeigt.</span><span class="sxs-lookup"><span data-stu-id="61cea-p104">**Note**  The STS isn't intended for user authentication. So, you won't see the STS listed on the user sign-in page, in the  **Authentication Provider** section in Central Administration, or in the People Picker in SharePoint.</span></span>
 


## <a name="two-kinds-of-token-issuers"></a><span data-ttu-id="61cea-122">Zwei Arten von Tokenherausgebern</span><span class="sxs-lookup"><span data-stu-id="61cea-122">Two kinds of token issuers</span></span>
<span data-ttu-id="61cea-123"><a name="TwoKindsOfIssuers"> </a></span><span class="sxs-lookup"><span data-stu-id="61cea-123"></span></span>

<span data-ttu-id="61cea-p105">Die Remotewebanwendung einer besonders vertrauenswürdigen SharePoint-Add-In ist an ein digitales Zertifikat gebunden. (Informationen zur entsprechenden Vorgehensweise finden Sie in den beiden oben verlinkten Themen.) Das Zertifikat wird von der Remotewebanwendung verwendet, um die Zugriffstoken zu signieren, die sie in alle Anforderungen an SharePoint einfügt. Die Webanwendung signiert das Token mit dem privaten Schlüssel des Zertifikats, und SharePoint validiert es mit dem öffentlichen Schlüssel des Zertifikats. Das Zertifikat muss als vertrauenswürdiger Tokenherausgeber registriert sein, bevor SharePoint den Token vertraut, die von diesem ausgestellt werden. Es gibt zwei Arten von Tokenherausgebern: Die einen können nur Token für eine bestimmte SharePoint-Add-In ausstellen, die anderen, die als Vertrauensbroker bezeichnet werden, können Token für mehrere SharePoint-Add-Ins ausstellen.</span><span class="sxs-lookup"><span data-stu-id="61cea-p105">The remote web application of a high-trust SharePoint Add-in is bound to a digital certificate. (For information about how this is done, see the two topics linked-to above.) The certificate is used by the remote web application to sign the access tokens that it includes in all its requests to SharePoint. The web application signs the token with the private key of the certificate and SharePoint validates it with the public key of the certificate. The certificate has to be registered as a trusted token issuer before SharePoint will trust the tokens that it issues. There are two kinds of token issuers: some can only issue tokens for a particular SharePoint Add-in; others, called trust brokers, can issue tokens for multiple SharePoint Add-ins.</span></span>
 

 
<span data-ttu-id="61cea-p106">In der Praxis legen SharePoint-Farmadministratoren anhand der Switches und Parameterwerte, die sie mit dem Cmdlet  `New-SPTrustedSecurityTokenIssuer` verwenden, fest, welche Art von Tokenherausgeber erstellt wird. Um einen Tokenherausgeber zu erstellen, der ein Vertrauensbroker ist, fügen Sie der Befehlszeile den Switch `-IsTrustBroker` hinzu, und verwenden Sie für den `-Name`-Parameter einen eindeutigen Wert, der nicht mit der Client-ID des Add-Ins identisch ist. Hier sehen Sie ein bearbeitetes Beispiel.</span><span class="sxs-lookup"><span data-stu-id="61cea-p106">As a practical matter, SharePoint farm administrators determine which type of token issuer is created by the switches and parameter values they use with the  `New-SPTrustedSecurityTokenIssuer` cmdlet. To create a token issuer that is a trust broker, add the `-IsTrustBroker` switch to the command line and use a unique value, other than an add-in's client ID, for the `-Name` parameter. The following is an edited example.</span></span>
 

 



```
New-SPTrustedSecurityTokenIssuer -IsTrustBroker -RegisteredIssuerName "<full_token_issuer_name> " --other parameters omitted--
```

<span data-ttu-id="61cea-p107">Um einen Tokenherausgeber zu erstellen, der kein Broker ist, wird der Switch  `-IsTrustBroker` nicht verwendet. Es besteht ein weiterer Unterschied. Der Wert des `-RegisteredIssuerName`-Parameters weist stets die Form zweier GUIDs auf, die durch das Zeichen "@" getrennt sind;  _GUID_@ _GUID_. Die GUID auf der rechten Seite ist immer die ID des Authentifizierungsbereichs der SharePoint-Farm (oder des Websiteabonnements). Die GUID auf der linken Seite ist immer eine bestimmte ID für einen Tokenherausgeber. Es handelt sich um eine zufällige GUID, wenn ein Tokenherausgeber erstellt wird, der ein  *Vertrauensbroker*  ist. Wenn jedoch ein Tokenherausgeber erstellt wird, der kein Vertrauensbroker ist, muss die spezifische Herausgeber-GUID mit der GUID identisch sein, die als Client-ID der SharePoint-Add-In verwendet wird. Dieser Parameter liefert nicht nur einen Namen für den Herausgeber, sondern er informiert SharePoint auch darüber, welche SharePoint-Add-In die einzige ist, für die das Zertifikat Token ausstellen kann. Hier ein unvollständiges Beispiel:</span><span class="sxs-lookup"><span data-stu-id="61cea-p107">To create a non-broker token issuer, the  `-IsTrustBroker` switch is not used. There is one other difference. The value of the `-RegisteredIssuerName` parameter is always in the form of two GUIDs separated by the "@" character; _GUID_@ _GUID_. The GUID on the right side is always the ID of the authentication realm of the SharePoint farm (or site subscription). The GUID on the left side is always a specific ID for a token issuer. It is a random GUID when a  *trust broker*  token issuer is being created. But when a non-broker token issuer is being created, the specific issuer GUID must be the same GUID that is used as the client ID of the SharePoint Add-in. This parameter provides a name for the issuer. It also tells SharePoint which SharePoint Add-in is the only one for which the certificate can issue tokens. The following is a partial example:</span></span>
 

 



```
$fullIssuerIdentifier = "<client_ID_of_SP_app> " + "@" + "<realm_GUID> "
New-SPTrustedSecurityTokenIssuer -RegisteredIssuerName $fullIssuerIdentifier --other parameters omitted--
```

<span data-ttu-id="61cea-142">Normalerweise wird das Cmdlet  `New-SPTrustedSecurityTokenIssuer` in einem Skript verwendet, das andere Aufgaben durchführt, um SharePoint für besonders vertrauenswürdige Add-Ins zu konfigurieren. Weitere Informationen zu diesen Skripts und vollständige Beispiele für das Cmdlet `New-SPTrustedSecurityTokenIssuer` finden Sie unter [Besonders vertrauenswürdige Konfigurationsskripts für SharePoint](high-trust-configuration-scripts-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="61cea-142">Typically, the  `New-SPTrustedSecurityTokenIssuer` cmdlet is used in a script that performs other tasks to configure SharePoint for high-trust add-ins. For more information about such scripts and complete examples of the `New-SPTrustedSecurityTokenIssuer` cmdlet, see [High-trust configuration scripts for SharePoint](high-trust-configuration-scripts-for-sharepoint.md).</span></span>
 

 

## <a name="deciding-between-using-one-certificate-or-many-for-high-trust-sharepoint-add-ins"></a><span data-ttu-id="61cea-143">Entscheiden zwischen der Verwendung eines oder mehrerer Zertifikate für besonders vertrauenswürdige SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="61cea-143">Deciding between using one certificate or many for high-trust SharePoint Add-ins</span></span>
<span data-ttu-id="61cea-144"><a name="Deciding"> </a></span><span class="sxs-lookup"><span data-stu-id="61cea-144"></span></span>

<span data-ttu-id="61cea-145">SharePoint- und Netzwerkadministratoren können zwischen zwei grundlegenden Strategien wählen, wenn sie Zertifikate zur Verwendung durch besonders vertrauenswürdige SharePoint-Add-Ins abrufen und verwalten:</span><span class="sxs-lookup"><span data-stu-id="61cea-145">SharePoint and network administrator have two basic strategies to choose from when obtaining and managing certificates for use by high-trust SharePoint Add-ins:</span></span>
 

 

- <span data-ttu-id="61cea-146">Verwenden des gleichen Zertifikats für mehrere SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="61cea-146">Use the same certificate for multiple SharePoint Add-ins.</span></span>
    
 
- <span data-ttu-id="61cea-147">Verwenden eines separaten Zertifikats für jede SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="61cea-147">Use a separate certificate for each SharePoint Add-in.</span></span>
    
 
<span data-ttu-id="61cea-148">In diesem Abschnitt werden die Vor- und Nachteile der jeweiligen Strategie erläutert.</span><span class="sxs-lookup"><span data-stu-id="61cea-148">This section discusses the pros and cons for each strategy.</span></span>
 

 
<span data-ttu-id="61cea-p108">Der Vorteil der Verwendung des gleichen Zertifikats für mehrere SharePoint-Add-Ins ist, dass ein Administrator weniger Zertifikate hat, die als vertrauenswürdig eingestuft und verwaltet werden müssen. Der Nachteil dieses Ansatzes ist, dass Sie im Falle, dass der Administrator einer bestimmten SharePoint-Add-In das Vertrauen entziehen möchte, nur die Möglichkeit haben, das Zertifikat als Tokenherausgeber oder als Stammautorisierungsstelle zu entfernen. Wenn Sie das Zertifikat entfernen, wird aber auch allen anderen SharePoint-Add-Ins, die das gleiche Zertifikat verwenden, das Vertrauen entzogen, sodass sie nicht mehr verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="61cea-p108">The benefit of using the same certificate for multiple SharePoint Add-ins is that an administrator has fewer certificates to trust and manage. The disadvantage in this approach is that, when you encounter a situation where you want to break trust with a particular SharePoint Add-in, the only way the administrator can break trust is by removing the certificate as a token issuer or as a root authority. But removing the certificate also breaks trust with all other SharePoint Add-ins that use the same certificate, which causes them all to stop working.</span></span>
 

 
<span data-ttu-id="61cea-p109">Damit die weiterhin vertrauenswürdigen SharePoint-Add-Ins wieder verwendet werden können, müsste der Administrator  *mithilfe eines neuen Zertifikats*  ein `New-SPTrustedSecurityTokenIssuer`-Objekt erstellen und die Kennzeichnung  `-IsTrustBroker` hinzufügen. Dann müsste das neue Zertifikat bei jedem Server registriert werden, der eines der vertrauenswürdigen Add-Ins hostet, und jedes dieser Add-Ins müsste an das neue Zertifikat gebunden werden.</span><span class="sxs-lookup"><span data-stu-id="61cea-p109">To get the still trustworthy SharePoint Add-ins working again, the administrator would need to create a  `New-SPTrustedSecurityTokenIssuer` object *using a new certificate*  and include the `-IsTrustBroker` flag. Then the new certificate would have to be registered with each server that hosts any of the trustworthy add-ins and each of those add-ins would have to be bound to the new certificate.</span></span>
 

 
<span data-ttu-id="61cea-p110">Der Vorteil der Verwendung eines Zertifikats pro Add-In ist, dass es einfacher ist, einem bestimmten Add-In das Vertrauen zu entziehen, da die von den weiterhin vertrauenswürdigen Add-Ins verwendeten Zertifikate nicht betroffen sind, wenn der Administrator dem Zertifikat des einen Add-Ins das Vertrauen entzieht. Der Nachteil dieser Strategie besteht darin, dass ein Administrator mehr Zertifikate beschaffen muss und SharePoint so konfiguriert sein muss, dass jedes der Zertifikate verwendet wird, was mithilfe eines wiederverwendbaren Skripts erfolgen kann (siehe  [Besonders vertrauenswürdige Konfigurationsskripts für SharePoint](high-trust-configuration-scripts-for-sharepoint.md)).</span><span class="sxs-lookup"><span data-stu-id="61cea-p110">The benefit of using one certificate per add-in is that it makes it easier to break trust with a particular add-in, because the certificates that are used by the still trustworthy add-ins are not affected when the administrator breaks trust with the certificate of the one add-in. The disadvantage in this strategy is that an administrator has more certificates to acquire and SharePoint must be configured to use each of them, which can be done with a reusable script as shown in  [High-trust configuration scripts for SharePoint](high-trust-configuration-scripts-for-sharepoint.md).</span></span>
 

 

## <a name="certificates-are-root-authorities-in-sharepoint"></a><span data-ttu-id="61cea-156">Zertifikate sind Stammzertifizierungsstellen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="61cea-156">Certificates are root authorities in SharePoint</span></span>
<span data-ttu-id="61cea-157"><a name="RootAuthorities"> </a></span><span class="sxs-lookup"><span data-stu-id="61cea-157"></span></span>

<span data-ttu-id="61cea-p111">Wie kurz weiter oben in diesem Artikel erwähnt, müssen SharePoint-Farmadministratoren das Zertifikat der Remotewebanwendung in dem besonders vertrauenswürdigen Add-In zu einer vertrauenswürdigen Stammzertifizierungsstelle in SharePoint sowie zu einem vertrauenswürdigen Tokenherausgeber machen. Wenn es hinter dem Zertifikat der Webanwendung eine Hierarchie von Zertifizierungsstellen gibt, müssen alle Zertifikate in der Kette zur Liste der vertrauenswürdigen Stammzertifizierungsstellen in SharePoint hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="61cea-p111">As mentioned briefly at the top of this article, SharePoint farm administrators have to make the certificate, of the remote web application in the high-trust add-in, a trusted root authority in SharePoint as well as a trusted token issuer. In fact, when there is a hierarchy of certificate issuing authorities behind the web application's certificate, all the certificates in the chain must be added to SharePoint's list of trusted root authorities.</span></span>
 

 
<span data-ttu-id="61cea-p112">Jedes Zertifikat in der Kette wird durch den Aufruf des Cmdlets  `New-SPTrustedRootAuthority` zur Liste der vertrauenswürdigen Stammzertifizierungsstellen in SharePoint hinzugefügt. Nehmen wir beispielsweise an, dass das Zertifikat der Webanwendung ein Domänenzertifikat ist, das von einer Zertifizierungsstelle einer Unternehmensdomäne im LAN ausgestellt wurde, und dass dessen Zertifikat wiederum von einer eigenständigen Zertifizierungsstelle der obersten Ebene im LAN ausgestellt wurde. In diesem Szenario müssen sämtliche Zertifikate, d. h. das Zertifikat der Zertifizierungsstelle der obersten Ebene, der mittleren Ebene und der Webanwendung, der Liste der vertrauenswürdigen Stammzertifizierungsstellen in SharePoint hinzugefügt werden. Dazu könnte der folgende Windows PowerShell-Code verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="61cea-p112">Each certificate in the chain is added to SharePoint's list of trusted root authorities with a call of the  `New-SPTrustedRootAuthority` cmdlet. For example, suppose that the web application's certificate is a domain certificate that is issued by an enterprise domain certificate authority on the LAN, and suppose that its certificate, in turn, was issued by a standalone, top-level certificate authority on the LAN. In this scenario, the certificates of the top-level CA, the intermediate CA, and the web application all have to be added to SharePoint's list of trusted root authorities. The following Windows PowerShell code would accomplish this.</span></span>
 

 



```
$rootCA = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2("<path_to_top-level_CA's_cer_file>")
New-SPTrustedRootAuthority -Name "<name_of_certificate>" -Certificate $rootCA

$intermediateCA = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2("path_to_intermediate_CA's_cer_file")
New-SPTrustedRootAuthority -Name "<name_of_certificate>" -Certificate $intermediateCA

$certificate = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2("path_to_web_application's_cer_file") 
New-SPTrustedRootAuthority -Name "<name_of_certificate>" -Certificate $certificate 

```

<span data-ttu-id="61cea-p113">Das Stammzertifikat und das Zertifikat der mittleren Ebene sollten nur einmal in einer SharePoint-Farm hinzugefügt werden. Normalerweise wird das Zertifikat der Webanwendung in einem separaten Skript hinzugefügt, das auch andere Konfigurationen vornimmt, wie dem Aufruf von  `New-SPTrustedSecurityTokenIssuer`. Beispiele finden Sie unter  [Besonders vertrauenswürdige Konfigurationsskripts für SharePoint](high-trust-configuration-scripts-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="61cea-p113">The root and intermediate certificates should be added only once on a SharePoint farm. Typically, the web application's certificate is added in a separate script that does other configuration too, such as the call to  `New-SPTrustedSecurityTokenIssuer`. For examples, see  [High-trust configuration scripts for SharePoint](high-trust-configuration-scripts-for-sharepoint.md).</span></span>
 

 
<span data-ttu-id="61cea-167">Wenn das Zertifikat der Webanwendung selbstsigniert ist, wie das z. B. der Fall ist, wenn das Add-In entwickelt und debuggt wird, gibt es keine Zertifikatskette, sodass nur das Zertifikat der Webanwendung der Liste der Stammauthentifizierungsstellen hinzugefügt werden muss.</span><span class="sxs-lookup"><span data-stu-id="61cea-167">If the web application's certificate is self-signed, as might be the case when the add-in is being developed and debugged, then there is no certificate chain and only the web application's certificate needs to be added to the list of root authorities.</span></span>
 

 
<span data-ttu-id="61cea-p114">Weitere Informationen finden Sie im Blog-Post  [Fehler: Dem Stamm der Zertifikatskette wird bei anspruchsbasierter Authentifizierung nicht vertraut](http://blogs.technet.com/b/speschka/archive/2010/02/13/root-of-certificate-chain-not-trusted-error-with-claims-authentication.aspx). (Überblättern Sie den Abschnitt zum Exportieren des Zertifikats aus Active Directory-Verbunddiensten, wobei davon ausgegangen wird, dass Sie Ihr Zertifikat für Ihre besonders vertrauenswürdigen Add-Ins auf anderem Weg erstellt haben, z. B. mithilfe eines durch eine Zertifizierungsstelle ausgestellten kommerziellen Zertifikats, eines selbstsignierten Zertifikats oder eines von der Domäne ausgestellten Zertifikats.)</span><span class="sxs-lookup"><span data-stu-id="61cea-p114">For more information, see the blog post  [Root of certificate chain not trusted error with claims authentication](http://blogs.technet.com/b/speschka/archive/2010/02/13/root-of-certificate-chain-not-trusted-error-with-claims-authentication.aspx). (Scroll past the section about exporting the certificate from Active Directory Federation Services (AD FS), assuming you created your certificate for your high-trust add-ins via some other means; for example, by using a commercial certificate issued by a Certificate Authority, a self-signed certificate, or a domain-issued certificate.)</span></span>
 

 

## <a name="web-application-needs-to-know-that-it-is-a-token-issuer"></a><span data-ttu-id="61cea-170">Die Webanwendung muss wissen, dass es sich um einen Tokenherausgeber handelt</span><span class="sxs-lookup"><span data-stu-id="61cea-170">Web application needs to know that it is a token issuer</span></span>
<span data-ttu-id="61cea-171"><a name="AppIsTokenIssuer"> </a></span><span class="sxs-lookup"><span data-stu-id="61cea-171"></span></span>

<span data-ttu-id="61cea-p115">Die Remotewebanwendungs-Komponente des SharePoint-Add-Ins ist an ihr Zertifikat in IIS gebunden. Dies ist für die herkömmlichen Zwecke von Zertifikaten ausreichend: sicheres Identifizieren der Webanwendung und Kodieren der HTTP-Anforderungen und -Antworten. In einem besonders vertrauenswürdigen SharePoint-Add-In hat das Zertifikat jedoch die zusätzliche Aufgabe, offizieller „Aussteller“ der Zugriffstoken zu sein, die von der Webanwendung an SharePoint gesendet werden. Dazu muss die Webanwendung die Aussteller-ID des Zertifikats kennen, das verwendet wird, wenn das Zertifikat bei SharePoint als Tokenherausgeber registriert wird. Die Webanwendung findet diese ID im Abschnitt **appSettings** der Datei „web.config“, in dem sich ein Schlüssel mit der Bezeichnung **IssuerId** befindet. Anweisungen dazu, wie der Add-In-Entwickler diesen Wert festlegt und wie das Zertifikat an die Webanwendung in IIS gebunden wird, finden Sie unter [Packen und Veröffentlichen besonders vertrauenswürdiger SharePoint-Add-Ins](package-and-publish-high-trust-sharepoint-add-ins.md). Wenn der Kunde die Strategie verwendet, für jedes besonders vertrauenswürdige SharePoint-Add-In ein separates Zertifikat zu haben, wird der **ClientId**-Wert auch als der **IssuerId**-Wert verwendet. Dies gilt nicht, wenn mehrere Add-Ins das gleiche Zertifikat verwenden, da jedes SharePoint-Add-In seine eigene eindeutige Client-ID aufweisen muss, während die Aussteller-ID der Bezeichner für ein **SPTrustedSecurityTokenIssuer**-Objekt ist.</span><span class="sxs-lookup"><span data-stu-id="61cea-p115">The remote web application component of the SharePoint Add-in is bound to its certificate in IIS. This is sufficient for the traditional purposes of certificates: securely identifying the web application and encoding the HTTP requests and responses. However, in a high-trust SharePoint Add-in, the certificate has the additional task of being the official "issuer" of the access tokens that the web application sends to SharePoint. For this purpose, web application has to know the issuer ID of the certificate that is used when registering the certificate as a token issuer with SharePoint. The web application gets this ID from the  **appSettings** section of the web.config file, where there is a key named **IssuerId**. Instructions for how the add-in developer sets this value, and how the certificate is bound to the web application in IIS, are in  [Package and publish high-trust SharePoint Add-ins](package-and-publish-high-trust-sharepoint-add-ins.md). Note that if the customer is using the strategy of having a separate certificate for each high-trust SharePoint Add-in, then the  **ClientId** value is also used as the **IssuerId** value. This is not the case when multiple add-ins share the same certificate, because each SharePoint Add-in must have its own unique client ID, but the issuer ID is the identifier for a **SPTrustedSecurityTokenIssuer** object.</span></span>
 

 
<span data-ttu-id="61cea-p116">Es folgt ein Beispiel für einen **appSettings**-Abschnitt für ein besonders vertrauenswürdiges SharePoint-Add-In. In diesem Beispiel wird ein Zertifikat von mehreren Add-Ins gemeinsam verwendet. Daher ist die **IssuerId** nicht mit der **ClientId** identisch. Beachten Sie, dass ein besonders vertrauenswürdiges SharePoint-Add-In keinen **ClientSecret**-Schlüssel enthält.</span><span class="sxs-lookup"><span data-stu-id="61cea-p116">Following is an example of an  **appSettings** section for a high-trust SharePoint Add-in. In this example, a certificate is being shared by multiple add-ins, so the **IssuerId** is not the same as the **ClientId**. Note that there is no  **ClientSecret** key in a high-trust SharePoint Add-in.</span></span>
 

 



```XML
<appSettings>
  <add key="ClientId" value="6569a7e8-3670-4669-91ae-ec6819ab461" />
  <add key="ClientSigningCertificatePath" value="C:\MyCerts\HighTrustCert.pfx" />
  <add key="ClientSigningCertificatePassword" value="3VeryComplexPa$$word82" />
  <add key="IssuerId" value="e9134021-0180-4b05-9e7e-0a9e5a524965" />
</appSettings>

```


 <span data-ttu-id="61cea-p117">**Sicherheitshinweis** Im vorherigen Beispiel wird davon ausgegangen, dass das Zertifikat im Dateisystem gespeichert ist. Dies ist akzeptabel für Entwicklung und Debugging. In einem besonders vertrauenswürdigen SharePoint-Add-In für die Produktion wird das Zertifikat in der Regel im Windows-Zertifikatspeicher gespeichert, und die Schlüssel **ClientSigningCertificatePath** und **ClientSigningCertificatePassword** werden in der Regel durch einen **ClientSigningCertificateSerialNumber**-Schlüssel ersetzt.</span><span class="sxs-lookup"><span data-stu-id="61cea-p117">**Security Note**  The preceding example assumes that the certificate is stored on the file system. This is acceptable for development and debugging. In a production high-trust SharePoint Add-in, the certificate is usually stored in the Windows Certificate Store, and the  **ClientSigningCertificatePath** and **ClientSigningCertificatePassword** keys are typically replaced by a **ClientSigningCertificateSerialNumber** key.</span></span>
 


## <a name="it-staff-responsibilities-in-the-high-trust-system"></a><span data-ttu-id="61cea-185">Aufgaben der IT-Mitarbeiter im besonders vertrauenswürdigen System</span><span class="sxs-lookup"><span data-stu-id="61cea-185">IT staff responsibilities in the high-trust system</span></span>
<span data-ttu-id="61cea-186"><a name="ITPro"> </a></span><span class="sxs-lookup"><span data-stu-id="61cea-186"></span></span>

<span data-ttu-id="61cea-p118">Entwickler müssen die Anforderungen für Anwendungssicherheit, wie oben beschrieben, verstehen, während IT-Experten die Infrastruktur implementieren, die zur Unterstützung erforderlich ist. IT-Experten müssen die folgenden betrieblichen Anforderungen einplanen:</span><span class="sxs-lookup"><span data-stu-id="61cea-p118">Developers will have to understand the requirements for application security as described above, but IT Pros will be implementing the infrastructure required to support it. IT Pros must plan for the following operational requirements:</span></span>
 

 

- <span data-ttu-id="61cea-189">Erstellen oder Erwerben mindestens eines Zertifikats, das für vertrauenswürdige SharePoint-Add-Ins verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="61cea-189">Create or purchase one or more certificates that will be used for trusted SharePoint Add-ins.</span></span>
    
 
- <span data-ttu-id="61cea-p119">Sicherstellen, dass die Zertifikate sicher auf den Webanwendungsservern gespeichert werden. Bei Verwendung eines Windows-Betriebssystems bedeutet dies das Speichern der Zertifikate im Windows-Zertifikatspeicher.</span><span class="sxs-lookup"><span data-stu-id="61cea-p119">Ensure that the certificates are securely stored on the web application servers. When Windows OS is being used, this means storing the certificates in the Windows Certificate Store.</span></span>
    
 
- <span data-ttu-id="61cea-192">Verwalten der Verteilung dieser Zertifikate an Entwickler, die SharePoint-Add-Ins erstellen.</span><span class="sxs-lookup"><span data-stu-id="61cea-192">Manage the distribution of those certificates to developers who are building SharePoint Add-ins.</span></span>
    
 
- <span data-ttu-id="61cea-p120">Verfolgen der Stellen, an die jedes Zertifikat verteilt wird, sowohl für die Add-Ins, die es verwenden, als auch für die Entwickler, die eine Kopie erhalten haben. Wenn ein Zertifikat zurückgerufen werden muss, muss der IT-Mitarbeiter in Zusammenarbeit mit jedem Entwickler einen verwalteten Übergang zu einem neuen Zertifikat planen.</span><span class="sxs-lookup"><span data-stu-id="61cea-p120">Keep track where each certificate is distributed, for both the add-ins using it and the developers who have received a copy. If a certificate has to be revoked, the IT staff must work with each developer to arrange for a managed transition to a new certificate.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="61cea-195">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="61cea-195">Additional resources</span></span>
<span data-ttu-id="61cea-196"><a name="AR"> </a></span><span class="sxs-lookup"><span data-stu-id="61cea-196"></span></span>


-  [<span data-ttu-id="61cea-197">Erstellen von besonders vertrauenswürdigen SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="61cea-197">Create high-trust SharePoint Add-ins</span></span>](create-high-trust-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="61cea-198">Packen und Veröffentlichen besonders vertrauenswürdiger SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="61cea-198">Package and publish high-trust SharePoint Add-ins</span></span>](package-and-publish-high-trust-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="61cea-199">Tipps zur Problembehandlung für besonders vertrauenswürdige Add-Ins unter SharePoint</span><span class="sxs-lookup"><span data-stu-id="61cea-199">Troubleshooting tips for high trust add-ins on SharePoint</span></span>](http://blogs.technet.com/b/speschka/archive/2012/11/01/more-troubleshooting-tips-for-high-trust-apps-on-sharepoint-2013.aspx)
    
 
-  [<span data-ttu-id="61cea-200">Autorisierung und Authentifizierung für Add-Ins in SharePoint</span><span class="sxs-lookup"><span data-stu-id="61cea-200">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins.md)
    
 

