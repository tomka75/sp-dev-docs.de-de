---
title: Erstellen von SharePoint-Add-Ins, die Autorisierung mit einer niedrigen Vertrauensebene verwenden
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 4719c9697edb95c43532b7f438cf3b5d0e714399
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="creating-sharepoint-add-ins-that-use-low-trust-authorization"></a><span data-ttu-id="621e4-102">Erstellen von SharePoint-Add-Ins, die Autorisierung mit einer niedrigen Vertrauensebene verwenden</span><span class="sxs-lookup"><span data-stu-id="621e4-102">Creating SharePoint Add-ins that use low-trust authorization</span></span>
<span data-ttu-id="621e4-103">Erfahren Sie mehr über das Autorisierungssystem mit niedriger Vertrauensebene für SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="621e4-103">Learn about the low-trust authorization system for SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="621e4-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="621e4-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="621e4-p102">Remotekomponenten in einem SharePoint-Add-In (oder einer externen Anwendung) können die Autorisierung für SharePoint-Ressourcen erteilen, indem mit jeder HTTP-Anforderung ein Zugriffstoken an SharePoint weitergegeben wird. Die Remotekomponenten rufen das Zugriffstoken aus einem Microsoft Azure Access Control Service (ACS)-Konto ab, das dem Office 365-Mandanten zugeordnet ist. Azure ACS dient als Autorisierungsserver in einer  [OAuth 2.0](http://oauth.net/)-Transaktion, die einen Ablauf aufruft, dabei dient SharePoint als Ressourcenserver und die Remotekomponenten als der Client. Entsprechende Protokollspezifikationen finden Sie unter [Web-Autorisierungsprotokoll (oauth)](http://datatracker.ietf.org/doc/active/#oauth).</span><span class="sxs-lookup"><span data-stu-id="621e4-p102">Remote components in a SharePoint Add-in (or external application) can gain authorization to SharePoint resources by passing an access token to SharePoint with each HTTP request. The remote components obtain the access token from a Microsoft Azure Access Control Service (ACS) account that is associated with the customer's Office 365 tenancy. Azure ACS acts as the authorization server in an  [OAuth 2.0](http://oauth.net/) transaction, called aflow, with SharePoint as the resource server and the remote components as the client. For related protocol specifications, see  [Web Authorization Protocol (oauth)](http://datatracker.ietf.org/doc/active/#oauth).</span></span> 
 

<span data-ttu-id="621e4-p103">Vom Anbieter gehostete SharePoint-Add-Ins, die das Autorisierungssystem mit niedriger Vertrauensebene verwenden, können im Office Store verkauft und in Microsoft SharePoint Online oder einer lokalen SharePoint-Farm installiert werden, die so konfiguriert ist, dass sie zum Einrichten einer Vertrauensstellung mit Azure ACS den Office 365-Mandanten des Kunden verwendet. Der Kunde muss einen Office 365-Mandanten besitzen, um SharePoint-Add-Ins zu installieren, die das System mit niedriger Vertrauensstellung verwenden. Der Kunde benötigt den Mandanten jedoch zu keinem anderen Zweck. Anweisungen zum Verknüpfen einer lokalen Farm mit einem Office 365-Mandanten finden Sie unter  [Verwenden einer Office 365 SharePoint-Website, um vom Anbieter gehostete Add-Ins auf einer lokalen SharePoint-Website zu autorisieren](use-an-office-365-sharepoint-site-to-authorize-provider-hosted-add-ins-on-an-on.md).</span><span class="sxs-lookup"><span data-stu-id="621e4-p103">Provider-hosted SharePoint Add-ins that use low-trust authorization system can be sold in the Office Store and installed on either Microsoft SharePoint Online or an on-premise SharePoint farm that has been configured to use the customer's Office 365 tenancy to establish trust with Azure ACS. The customer must have an Office 365 tenancy to install SharePoint Add-ins that use the low-trust system. However, it is not necessary for the customer to use the tenancy for any other purpose. For instructions about linking an on-premise farm to a Office 365 tenancy, see  [Use an Office 365 SharePoint site to authorize provider-hosted add-ins on an on-premises SharePoint site](use-an-office-365-sharepoint-site-to-authorize-provider-hosted-add-ins-on-an-on.md).</span></span>
 


## <a name="registration-with-azure-acs"></a><span data-ttu-id="621e4-115">Registrierung mit Azure ACS</span><span class="sxs-lookup"><span data-stu-id="621e4-115">Registration with Azure ACS</span></span>
<span data-ttu-id="621e4-116"><a name="Registration"> </a></span><span class="sxs-lookup"><span data-stu-id="621e4-116"></span></span>

<span data-ttu-id="621e4-p104">Zum Verwenden des Systems mit niedriger Vertrauensstellung muss das SharePoint-Add-In zunächst bei Azure ACS und dem App-Verwaltungsdienst der SharePoint-Farm oder des SharePoint Online-Mandanten registriert werden. (Er wird „App-Verwaltungsdienst“" genannt, da SharePoint-Add-Ins ursprünglich „Apps für SharePoint“ genannt wurden). Bei Add-Ins, die über den Office Store verkauft werden, erfolgt die Registrierung bei ACS im Verkäuferdashboard, und die Registrierung bei dem Dienst wird bei der Installation des Add-Ins durchgeführt. Bei Add-Ins, die im Add-In-Katalog der Organisation verteilt werden, erfolgt die Registrierung bei ACS und dem Dienst auf der _Layouts15\_AppRegNew.aspx-Seite eines SharePoint-Mandanten oder einer Farm, auf der das Add-In installiert werden soll. Externe, Nicht-SharePoint-Anwendungen, die auf SharePoint zugreifen, müssen ebenfalls registriert werden. Diese Kategorie umfasst Office-Add-Ins, Windows Store-Apps, Webanwendungen und Geräte-Apps, wie z. B. Smartphone-Apps.</span><span class="sxs-lookup"><span data-stu-id="621e4-p104">To use the low-trust system, the SharePoint Add-in must first be registered with Azure ACS and with the App Management Service of the SharePoint farm or SharePoint Online tenancy. (It is called "App Management Service" because SharePoint Add-ins were originally called "apps for SharePoint".) For add-ins that are sold through the Office Store, registration to ACS is performed in the Seller Dashboard and registration with the service is performed when the add-in is installed. For add-ins that are distributed in the organization add-in catalog, registration to both ACS and the service is performed on the \_Layouts\15\AppRegNew.aspx page of any SharePoint tenancy or farm where the add-in is to be installed. External, non- SharePoint, applications that access SharePoint, also need to be registered. This category includes Office Add-ins, Windows Store apps, web applications, and device apps such as smartphone apps.</span></span>
 

 

 <span data-ttu-id="621e4-p105">**Hinweis** Für die Registrierung muss die Anwendung über eine Internetdomäne verfügen. Zu diesem Zweck kann jede vorhandene Domäne verwendet werden, Sie können jedoch nicht zu 100 % sicher sein, dass eine Domäne, die Sie nicht besitzen, auch existiert, deshalb muss eine Webanwendung Teil einer systemeigenen Geräteanwendung sein, selbst wenn die Webanwendungskomponente nur zum Aktivieren der Registrierung dient. Weitere Informationen finden Sie in einem so konzipierten Codebeispiel unter [Bereitstellen von Websites in Batches mithilfe des Add-In-Modells](http://code.msdn.microsoft.com/Provision-sites-in-batches-fcf31bc6).</span><span class="sxs-lookup"><span data-stu-id="621e4-p105">**Note**  Registration requires that the application have an Internet domain. Any existing domain can be used for this purpose, but you can't be 100% certain that any domain you don't own will always exist, so a web application would need to be part of a native device application even if the web application component played no other role than to enable registration. For an advanced code sample that is designed in this way, see  [Provision sites in batches with the add-in model](http://code.msdn.microsoft.com/Provision-sites-in-batches-fcf31bc6).</span></span>
 

<span data-ttu-id="621e4-125">Weitere Informationen über die Registrierung finden Sie unter [Registrieren von SharePoint-Add-Ins 2013](register-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="621e4-125">For more information on registration, see  [Register SharePoint Add-ins 2013](register-sharepoint-add-ins.md).</span></span>
 

 

### <a name="add-in-secret-expiration"></a><span data-ttu-id="621e4-126">Ablauf des geheimen Add-In-Schlüssels</span><span class="sxs-lookup"><span data-stu-id="621e4-126">Add-in secret expiration</span></span>

<span data-ttu-id="621e4-p106">Der geheime Add-In-Schlüssel muss alle 12 Monate ersetzt werden. Weitere Informationen finden Sie unter [Ersetzen eines ablaufenden geheimen Clientschlüssels in einem SharePoint-Add-In](replace-an-expiring-client-secret-in-a-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="621e4-p106">The add-in secret must be replaced every 12 months. For details, see  [Replace an expiring client secret in a SharePoint Add-in](replace-an-expiring-client-secret-in-a-sharepoint-add-in.md).</span></span>
 

 

## <a name="authorization-policies"></a><span data-ttu-id="621e4-129">Autorisierungsrichtlinien</span><span class="sxs-lookup"><span data-stu-id="621e4-129">Authorization policies</span></span>
<span data-ttu-id="621e4-130"><a name="Policies"> </a></span><span class="sxs-lookup"><span data-stu-id="621e4-130"></span></span>

<span data-ttu-id="621e4-131">Ein SharePoint-Add-In kann für die Verwendung einer der beiden folgenden Autorisierungsrichtlinien ausgelegt sein:</span><span class="sxs-lookup"><span data-stu-id="621e4-131">A SharePoint Add-in can be designed to use either of two authorization policies:</span></span>
 

 

-  <span data-ttu-id="621e4-p107">**Benutzer- und Add-In-Richtlinie:** Add-Ins, die diese Richtlinie verwenden, können nur Aktionen ausführen, für die sowohl das Add-In als auch der Benutzer Berechtigungen besitzen. Dies ist die standardmäßig verwendete Richtlinie, sofern der Entwickler keine bestimmten Schritte zur Verwendung der anderen Richtlinie unternimmt.</span><span class="sxs-lookup"><span data-stu-id="621e4-p107">**User + add-in Policy:** Add-ins that use this policy can only perform actions that both the add-in and the user have permission to do. This is the default policy that is used unless the developer takes specific steps to use the other.</span></span>
    
 
-  <span data-ttu-id="621e4-p108">**Nur-Add-In-Richtlinie:** Add-Ins, die diese Richtlinie verwenden, können jede Aktion ausführen, für die sie eine Berechtigung besitzen, selbst wenn der Benutzer die Berechtigung für die Aktion nicht besitzt. Der Entwickler muss eine Anforderung senden, damit diese Richtlinie im Add-In-Manifest des Add-Ins verwendet wird. Die Anforderung muss von dem Benutzer genehmigt werden, der das Add-In installiert. Diese Richtlinie ist nur für vom Anbieter gehostete SharePoint-Add-Ins zulässig.</span><span class="sxs-lookup"><span data-stu-id="621e4-p108">**App-only Policy:** Add-ins that use this policy can perform any action that it has permission to do, even if the user does not have permission for the action. The developer must request that this policy be used in the add-in manifest of the add-in. The request must be approved by the user who installs the add-in. This policy is allowed for only provider-hosted SharePoint Add-ins.</span></span>
    
 
<span data-ttu-id="621e4-138">Weitere Informationen über Autorisierungsrichtlinien finden Sie unter  [Add-In-Autorisierungsrichtlinientypen in SharePoint](add-in-authorization-policy-types-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="621e4-138">For more information about authorization policies, see  [Add-in authorization policy types in SharePoint](add-in-authorization-policy-types-in-sharepoint.md).</span></span>
 

 

## <a name="two-oauth-runtime-flows"></a><span data-ttu-id="621e4-139">Zwei OAuth-Laufzeitabläufe</span><span class="sxs-lookup"><span data-stu-id="621e4-139">Two OAuth runtime flows</span></span>
<span data-ttu-id="621e4-140"><a name="Flows"> </a></span><span class="sxs-lookup"><span data-stu-id="621e4-140"></span></span>

<span data-ttu-id="621e4-p109">Bei jedem Ausführen eines in der Cloud gehosteten SharePoint-Add-In oder einer externen Anwendung, die auf SharePoint zugreift, tritt ein Ablauf - eine Reihe von Interaktionen zwischen dem Add-In, SharePoint, ACS und manchmal dem Endbenutzer - auf. Das Endergebnis des Ablaufs besteht darin, dass SharePoint ein bei Erstell-, Aktualisierungs-, Löschanforderungen enthaltenes Zugriffstoken erhält, die die Anwendung an SharePoint senden.</span><span class="sxs-lookup"><span data-stu-id="621e4-p109">Each time a cloud-hosted SharePoint Add-in or external application that is accessing SharePoint is run, a flow -- a series of interactions between the add-in, SharePoint, ACS, and sometimes the end user -- occurs. The end result of the flow is that SharePoint receives an access token included with each create, update, delete (CRUD) request that the application makes to SharePoint.</span></span>
 

 
<span data-ttu-id="621e4-p110">SharePoint verwendet zwei große OAuth-Abläufe. Einer ist für in der Cloud gehostete SharePoint-Add-Ins. Der andere „fließende" ist für Anwendungen auf anderen Plattformen, die auf SharePoint-Daten zugreifen.</span><span class="sxs-lookup"><span data-stu-id="621e4-p110">There are two major OAuth flows used by SharePoint. One is for cloud-hosted SharePoint Add-ins. The other, called "on the fly," is for applications on other platforms that access SharePoint data.</span></span>
 

 

-  <span data-ttu-id="621e4-p111">**Ablauf mit Kontexttoken:** Die Remotekomponente der SharePoint-Add-In verwendet das SharePoint-Clientobjektmodell (CSOM) oder REST-Endpunkte, um Aufrufe an SharePoint auszuführen. SharePoint fordert ein Kontexttoken von ACS an, das es an den Remoteserver senden kann. Der Remoteserver verwendet das Kontexttoken, um ein Zugriffstoken bei ACS anzufordern. Der Remoteserver verwendet das Zugriffstoken anschließend, um mit SharePoint zu kommunizieren. Details zu diesem Ablauf finden Sie unter [OAuth-Ablauf mit Kontexttoken für Add-Ins in SharePoint](context-token-oauth-flow-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="621e4-p111">**Context Token flow:** The remote component of the SharePoint Add-in uses the SharePoint client object model (CSOM) or REST endpoints to make calls to SharePoint. SharePoint requests a context token from ACS that it can send to the remote server. The remote server uses the context token to request an access token from the ACS. The remote server then uses the access token to talk back to SharePoint. For details about this flow, see [Context Token OAuth flow for SharePoint Add-ins](context-token-oauth-flow-for-sharepoint-add-ins.md).</span></span>
    
 
-  <span data-ttu-id="621e4-p112">**Ablauf mit Authentifizierungscode:** Ein SharePoint-Add-In erhält die benötigten Berechtigungen für den Zugriff auf SharePoint-Ressourcen, wenn es installiert wird. Anwendungen, die nicht in SharePoint installiert sind, müssen jedoch „spontan" Berechtigungen anfordern, d. h., jedes Mal, wenn sie ausgeführt werden. In diesem Ablauf ist kein SharePoint-Kontexttoken vorhanden. Wenn das Add-In ausgeführt wird und versucht, auf SharePoint zuzugreifen, fordert SharePoint den Benutzer stattdessen dazu auf, Berechtigungen für die Anwendung zu gewähren, die es anfordert. Wenn der Benutzer die Berechtigungen gewährt, ruft SharePoint einen Autorisierungscode von ACS ab, der an die Anwendung weitergegeben wird. Die Anwendung verwendet den Code, um ein Zugriffstoken von ACS abzurufen, das anschließend für die Kommunikation mit SharePoint verwendet werden kann. Details zu diesem Ablauf finden Sie unter [OAuth-Ablauf mit Authentifizierungscode für SharePoint-Add-Ins](authorization-code-oauth-flow-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="621e4-p112">**Authenticaton Code flow:** a SharePoint Add-in is granted the permissions it needs to SharePoint resources when it is installed. But applications that are not installed on SharePoint must ask for permissions "on the fly," that is, each time they run. There is no SharePoint context token in this flow. Instead, when the add-in runs and attempts to access SharePoint, SharePoint prompts the user to grant the permissions to the application that it is requesting. When the user grants the permissions, SharePoint obtains an authorization code from ACS which it passes to the application. The application uses the code to obtain an access token from ACS which it can then use to talk to SharePoint. For details about this flow, see [Authorization Code OAuth flow for SharePoint Add-ins](authorization-code-oauth-flow-for-sharepoint-add-ins.md).</span></span>
    
 

## <a name="troubleshooting-low-trust-sharepoint-add-ins"></a><span data-ttu-id="621e4-157">Problembehandlung bei SharePoint-Add-Ins mit niedriger Vertrauensebene</span><span class="sxs-lookup"><span data-stu-id="621e4-157">Troubleshooting low-trust SharePoint Add-ins</span></span>
<span data-ttu-id="621e4-158"><a name="Trouble"> </a></span><span class="sxs-lookup"><span data-stu-id="621e4-158"></span></span>

<span data-ttu-id="621e4-159">Dieser Artikel bietet einige allgemeine Informationen zur Problembehandlung sowie Informationen über einige spezielle Probleme mit SharePoint-Add-Ins, die das Autorisierungssystem mit niedriger Vertrauensebene verwenden.</span><span class="sxs-lookup"><span data-stu-id="621e4-159">This article provides some general troubleshooting guidance and information about some specific issues with SharePoint Add-ins that use the low-trust authorization system.</span></span>
 

 

### <a name="use-the-fiddler-tool"></a><span data-ttu-id="621e4-160">Verwenden des Fiddler-Tools</span><span class="sxs-lookup"><span data-stu-id="621e4-160">Use the Fiddler tool</span></span>

<span data-ttu-id="621e4-p113">Sie können das kostenlose  [Fiddler-Tool](http://www.telerik.com/fiddler) verwenden, um die HTTP-Anforderungen zu erfassen, die von der Remotekomponente Ihres Add-Ins an SharePoint gesendet werden. Es gibt eine [kostenlose Erweiterung des Tools](https://github.com/andrewconnell/SPOAuthFiddlerExt), das die Zugriffstoken in den Anforderungen automatisch decodiert.</span><span class="sxs-lookup"><span data-stu-id="621e4-p113">The free  [Fiddler tool](http://www.telerik.com/fiddler) can be used to capture the HTTP Requests sent by the remote component of your add-in to SharePoint. There is a [free extension to the tool](https://github.com/andrewconnell/SPOAuthFiddlerExt) that automatically decodes the access tokens in the requests.</span></span>
 

 

### <a name="turn-off-the-https-requirement-for-oauth-during-development"></a><span data-ttu-id="621e4-163">Deaktivieren der HTTPS-Anforderung für OAuth während der Entwicklung</span><span class="sxs-lookup"><span data-stu-id="621e4-163">Turn off the HTTPS requirement for OAuth during development</span></span>
<span data-ttu-id="621e4-164"><a name="TurnOffHTTPRequirement"> </a></span><span class="sxs-lookup"><span data-stu-id="621e4-164"></span></span>

<span data-ttu-id="621e4-p114">OAuth erfordert, dass SharePoint HTTPS ausführt (nicht nur Ihr Dienst, sondern auch SharePoint). Dies kann bei der Entwicklung des Add-Ins hinderlich sein. Sie erhalten zum Beispiel eine 403-Fehlermeldung (unzulässig), wenn Sie versuchen, beim Debuggen des Add-Ins einen Aufruf an SharePoint zu richten, da der „localhost", auf dem das Add-In ausgeführt wird, keine SSL-Unterstützung bietet.</span><span class="sxs-lookup"><span data-stu-id="621e4-p114">OAuth requires SharePoint to run HTTPS (not only your service, but SharePoint too). This can get in the away when you are developing the add-in. For example, you may get a 403 (forbidden) message when attempting to make a call to SharePoint when debugging the add-in because the SSL support is not present in the "localhost" where your add-in is running.</span></span>
 

 
<span data-ttu-id="621e4-168">Sie können die HTTPS-Anforderung während der Entwicklung mithilfe der folgenden Windows PowerShell-Cmdlets deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="621e4-168">You can turn off the HTTPS requirement during development using the following Windows PowerShell cmdlets.</span></span>
 

 



```
$serviceConfig = Get-SPSecurityTokenServiceConfig
$serviceConfig.AllowOAuthOverHttp = $true
$serviceConfig.Update()

```

<span data-ttu-id="621e4-169">Um die HTTPS-Anforderung später wieder zu aktivieren, verwenden Sie die folgenden Windows PowerShell-Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="621e4-169">To turn the HTTPS requirement back on later, use the following Windows PowerShell cmdlets.</span></span>
 

 



```
$serviceConfig = Get-SPSecurityTokenServiceConfig
$serviceConfig.AllowOAuthOverHttp = $false
$serviceConfig.Update()

```


### <a name="miscellaneous-ssl-and-domain-related-authorization-errors"></a><span data-ttu-id="621e4-170">Verschiedene SSL- und domänenbezogene Autorisierungsfehler</span><span class="sxs-lookup"><span data-stu-id="621e4-170">Miscellaneous SSL and domain-related authorization errors</span></span>
<span data-ttu-id="621e4-171"><a name="DomainRelatedErrors"> </a></span><span class="sxs-lookup"><span data-stu-id="621e4-171"></span></span>

<span data-ttu-id="621e4-p115">Die fehlende Übereinstimmung von Domänennamen in Konfigurationsdateien und Registrierungsformularen kann die Autorisierung verhindern. Die folgenden vier Werte müssen exakt gleich sein:</span><span class="sxs-lookup"><span data-stu-id="621e4-p115">A mismatch of domain names in configuration files and registration forms can prevent authorization. The following four values have to be exactly the same:</span></span>
 

 

- <span data-ttu-id="621e4-174">Die **Add-In-Domäne**, die bei der SharePoint-Add-In-Registrierung auf „AppRegNew.aspx" oder im Verkäuferdashboard angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="621e4-174">The  **Add-in Domain** that is specified when the SharePoint Add-in is registered on either AppRegNew.aspx or Seller Dashboard.</span></span>
    
 
- <span data-ttu-id="621e4-175">Die Domäne, die unter der das Sicherheitszertifikat der Remotewebanwendung registriert ist</span><span class="sxs-lookup"><span data-stu-id="621e4-175">The domain under which the remote web application's security certificate is registered.</span></span>
    
 
- <span data-ttu-id="621e4-176">Der Domänenteil des Werts **StartPage** in der Datei „AppManifest.xml“</span><span class="sxs-lookup"><span data-stu-id="621e4-176">The domain part of the  **StartPage** value in the AppManifest.xml file.</span></span>
    
 
- <span data-ttu-id="621e4-177">Der Domänenteil der URL aller Ereignisempfänger, die in der Datei „AppManifest.xml“ angegeben sind</span><span class="sxs-lookup"><span data-stu-id="621e4-177">The domain part of the URLs of any event receivers specified in the AppManifest.xml.</span></span>
    
 
<span data-ttu-id="621e4-178">Beachten Sie in Verbindung mit diesem Punkt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="621e4-178">In connection with this point, note the following:</span></span>
 

 

- <span data-ttu-id="621e4-p116">Wenn die Remotekomponente Ihres SharePoint-Add-In einen anderen Port als 443 verwendet, müssen Sie den Port ausdrücklich als Teil der Domäne an allen vier Stellen einschließen, beispielsweise  `contoso.com:3333`. (Sie müssen das HTTPS-Protokoll verwenden, für das der Standardport 443 ist.)</span><span class="sxs-lookup"><span data-stu-id="621e4-p116">If the remote component of your SharePoint Add-in is using any port other than 443, you must explicitly include the port as part of the domain in all four places; for example,  `contoso.com:3333`. (You must use the HTTPS protocol for which the default port is 443.)</span></span>
    
 
- <span data-ttu-id="621e4-p117">Wenn Sie einen DNS CNAME-Alias für Ihre Remotewebanwendung erstellen, verwenden Sie an allen vier Stellen den CNAME-Alias für den Domänenwert. Wenn Ihre Anwendung beispielsweise unter contoso.cloudapp.net gehostet wird und Sie den CNAME contososoftware.com dafür erstellen, verwenden Sie contososoftware.com als Domäne.</span><span class="sxs-lookup"><span data-stu-id="621e4-p117">If you create a DNS CNAME alias for your remote web application, use the CNAME alias for the domain value in all four places. For example, if your application is hosted at contoso.cloudapp.net and you create a CNAME of contososoftware.com for it, use contososoftware.com as the domain.</span></span>
    
 
- <span data-ttu-id="621e4-p118">Die Domäne muss im **StartPage**-Wert (und allen Ereignisempfänger-URLs) der Datei „AppManifest.xml" hartcodiert sein, bevor das Add-In gepackt wird. Wenn Sie den Assistenten **Veröffentlichen** in Visual Studio zum Packen des Add-Ins verwenden, werden Sie nach der Domäne gefragt. Office-Entwicklertools für Visual Studio fügt die Domäne für Sie in den **StartPage**-Wert ein (an der Stelle des  `~remoteWebUrl`-Tokens, das während des Debuggens verwendet wird). Wenn Sie den Assistenten **Veröffentlichen** nicht verwenden, oder auch dann, wenn Sie ihn verwenden, Ihre Remotewebanwendung jedoch in Azure bereitgestellt wird, müssen Sie das Token manuell durch die Domäne (und das Protokoll) ersetzen, z. B `https://contososoftware.com` oder `https://MyCloudVM:3333`.</span><span class="sxs-lookup"><span data-stu-id="621e4-p118">The domain needs to be hardcoded in the  **StartPage** value (and any event receiver URLs) of the AppManifest.xml file before the add-in is packaged. If you use the **Publish** wizard in Visual Studio to package the add-in, you will be prompted for the domain and the Office Developer Tools for Visual Studio will insert it into the **StartPage** value for you (in place of the `~remoteWebUrl` token that is used during debugging. But if you are not using the **Publish** wizard, or even if you are but your remote web application is deployed to Azure, you must manually replace the token with the domain (and protocol); for example `https://contososoftware.com` or `https://MyCloudVM:3333`.</span></span>
    
 

### <a name="error-the-underlying-connection-was-closed-could-not-establish-trust-relationship-for-the-ssltls-secure-channel"></a><span data-ttu-id="621e4-186">Fehler „Die zugrunde liegende Verbindung wurde geschlossen: Für den geschützten SSL/TLS-Kanal konnte keine Vertrauensstellung hergestellt werden“.</span><span class="sxs-lookup"><span data-stu-id="621e4-186">Error "The underlying connection was closed: Could not establish trust relationship for the SSL/TLS secure channel."</span></span>
<span data-ttu-id="621e4-187"><a name="ErrorConnectionClosed"> </a></span><span class="sxs-lookup"><span data-stu-id="621e4-187"></span></span>

<span data-ttu-id="621e4-p119">Dieser Fehler ist ein SSL Handshake-, kein OAuth-Problem. Stellen Sie sicher, dass das von Ihnen verwendete Zertifikat für SharePoint vertrauenswürdig ist und das Zertifikat mit dem Endpunktnamen übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="621e4-p119">This error is an SSL handshake issue, not an OAuth issue. Make sure that the certificate you are using is trusted by SharePoint, and that the certificate matches the endpoint name.</span></span>
 

 

### <a name="errors-using-http-dav-method-to-read-files-from-sharepoint"></a><span data-ttu-id="621e4-190">Fehler bei der Verwendung der HTTP-DAV-Methode zum Lesen von Dateien aus SharePoint</span><span class="sxs-lookup"><span data-stu-id="621e4-190">Errors using HTTP DAV method to read files from SharePoint</span></span>
<span data-ttu-id="621e4-191"><a name="ErrorConnectionClosed"> </a></span><span class="sxs-lookup"><span data-stu-id="621e4-191"></span></span>

<span data-ttu-id="621e4-p120">HTTP DAV funktioniert nicht zusammen mit OAuth. Wenn Sie das SharePoint-Clientobjektmodell (CSOM) nutzen, verwenden Sie zum Lesen einer Datei den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="621e4-p120">HTTP DAV does not work with OAuth. If you are using the SharePoint client object model (CSOM), use the following code to read a file.</span></span>
 

 

```C#
File f = clientContext.Web.GetFileByServerRelativeUrl( url);
ClientResult<Stream> r = f.OpenBinaryStream();
clientContext.ExecuteQuery();

```


## <a name="in-this-section"></a><span data-ttu-id="621e4-194">Inhalt dieses Abschnitts</span><span class="sxs-lookup"><span data-stu-id="621e4-194">In this section</span></span>
<span data-ttu-id="621e4-195"><a name="Trouble"> </a></span><span class="sxs-lookup"><span data-stu-id="621e4-195"></span></span>

 [<span data-ttu-id="621e4-196">Verwenden einer Office 365 SharePoint-Website, um vom Anbieter gehostete Add-Ins auf einer lokalen SharePoint-Website zu autorisieren</span><span class="sxs-lookup"><span data-stu-id="621e4-196">Use an Office 365 SharePoint site to authorize provider-hosted add-ins on an on-premises SharePoint site</span></span>](use-an-office-365-sharepoint-site-to-authorize-provider-hosted-add-ins-on-an-on.md)
 

 
 [<span data-ttu-id="621e4-197">OAuth-Ablauf mit Kontexttoken für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="621e4-197">Context Token OAuth flow for SharePoint Add-ins</span></span>](context-token-oauth-flow-for-sharepoint-add-ins.md)
 

 
 [<span data-ttu-id="621e4-198">Autorisierungscode-OAuth-Fluss für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="621e4-198">Authorization Code OAuth flow for SharePoint Add-ins</span></span>](authorization-code-oauth-flow-for-sharepoint-add-ins.md)
 

 
 [<span data-ttu-id="621e4-199">Austauschen eines ablaufenden geheimen Clientschlüssels in einem SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="621e4-199">Replace an expiring client secret in a SharePoint Add-in</span></span>](replace-an-expiring-client-secret-in-a-sharepoint-add-in.md)
 

 

## <a name="additional-resources"></a><span data-ttu-id="621e4-200">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="621e4-200">Additional resources</span></span>
<span data-ttu-id="621e4-201"><a name="FileName_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="621e4-201"></span></span>


-  [<span data-ttu-id="621e4-202">Registrieren von SharePoint-Add-Ins 2013</span><span class="sxs-lookup"><span data-stu-id="621e4-202">Register SharePoint Add-ins 2013</span></span>](register-sharepoint-add-ins.md)
    
 

