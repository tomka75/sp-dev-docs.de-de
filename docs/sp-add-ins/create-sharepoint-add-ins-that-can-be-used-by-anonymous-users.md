# <a name="create-sharepoint-add-ins-that-can-be-used-by-anonymous-users"></a><span data-ttu-id="42ab1-101">Erstellen von SharePoint-Add-Ins, die von anonymen Benutzern verwendet werden können</span><span class="sxs-lookup"><span data-stu-id="42ab1-101">Create SharePoint Add-ins that can be used by anonymous users</span></span>
<span data-ttu-id="42ab1-102">Erfahren Sie, wie Sie SharePoint-Add-Ins erstellen, die von anonymen Benutzern auf öffentlich zugänglichen Microsoft SharePoint-Websites verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="42ab1-102">Learn how to create SharePoint Add-ins that can be used by anonymous users on public-facing Microsoft SharePoint sites.</span></span>
 

 <span data-ttu-id="42ab1-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="42ab1-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


 <span data-ttu-id="42ab1-106">**Wichtig** Wenn in diesem Artikel der Begriff *lokales* SharePoint verwendet wird, wird davon ausgegangen, dass Service Pack 1 für SharePoint installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="42ab1-106">**Important** Wherever  *on-premise*  SharePoint is mentioned in this article, we assume that Service Pack 1 for SharePoint has been installed.</span></span>
 


## <a name="prerequisites-for-creating-anonymously-accessible-sharepoint-add-ins"></a><span data-ttu-id="42ab1-107">Voraussetzungen für die Erstellung anonym zugänglicher SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="42ab1-107">Prerequisites for creating anonymously accessible SharePoint Add-ins</span></span>

<span data-ttu-id="42ab1-p102">Anonymer Zugriff ist für in SharePoint gehostete und vom Anbieter gehostete SharePoint-Add-Ins möglich. Je nach Art der App, die Sie erstellen, sollten Sie einen der folgenden Sätze von Voraussetzungen prüfen:</span><span class="sxs-lookup"><span data-stu-id="42ab1-p102">Anonymous access is possible for SharePoint-hosted and provider-hosted SharePoint Add-ins. Depending on which type you create, review one of the following sets of prerequisites:</span></span>
 
-  [<span data-ttu-id="42ab1-110">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="42ab1-110">Get Started Creating SharePoint Hosted SharePoint add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins#SP15SPhostedapps_bk_prereqs)
    
-  [<span data-ttu-id="42ab1-111">Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="42ab1-111">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins#SP15createselfhostapp_bk_prereq)
    
 
<span data-ttu-id="42ab1-p103">Sie benötigen in Ihrer SharePoint-Testinstallation eine Websitesammlung, die für anonymen Zugriff konfiguriert ist. Wenn Sie eine Website für Office 365-Entwickler haben, ist damit bereits eine öffentliche Websitesammlung verknüpft, die eine spezielle "Public Website"-Websitedefinition verwendet. (Weitere Informationen zur Verwendung von öffentlichen Websites in Microsoft SharePoint Online finden Sie unter  [Hilfe zu öffentlichen Websites für Office 365](http://office.microsoft.com/en-gb/office365-sharepoint-online-enterprise-help/public-website-help-for-office-365-HA102891740.aspx?CTT=1).) Diese Websitedefinition ist für lokale SharePoint-Installationen nicht verfügbar. Wenn Ihre Testinstallation lokal ist, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="42ab1-p103">You will also need a site collection in your test SharePoint installation that is configured for anonymous access. If you have an Office 365 Developer Site, there is already a public site collection associated with it that uses a special Public Website site definition. (For more information about the use of Public Websites in Microsoft SharePoint Online, see  [Public Website help for Office 365](http://office.microsoft.com/en-gb/office365-sharepoint-online-enterprise-help/public-website-help-for-office-365-HA102891740.aspx?CTT=1).) That site definition is not available for on premises SharePoint installations. So if your test installation is on-premises, you will need:</span></span>
 

 

- <span data-ttu-id="42ab1-p104">Eine SharePoint-Webanwendung, die so konfiguriert ist, dass sie anonymen Zugriff zulässt. Diese Konfiguration muss aber erfolgen, nachdem die SharePoint-Add-In installiert wurde, die Sie testen.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p104">A SharePoint web application that is configured to allow anonymous access. But this configuration must occur after the SharePoint Add-in that you are testing has been installed.</span></span>
    
 
- <span data-ttu-id="42ab1-p105">Eine Websitesammlung innerhalb der Webanwendung, die selbst für anonymen Zugriff konfiguriert ist. Diese Konfiguration muss aber erfolgen, nachdem die SharePoint-Add-In installiert wurde, die Sie testen.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p105">A site collection within the web application that is itself configured for anonymous access. But this configuration must occur after the SharePoint Add-in that you are testing has been installed.</span></span>
    
 
- <span data-ttu-id="42ab1-120">Wenn Ihr Add-In von SharePoint gehostet wird und auf eine SharePoint-Liste zugreift: eine Liste in der Websitesammlung, die für anonymen Zugriff konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="42ab1-120">If your add-in is SharePoint-hosted and accesses a SharePoint list, a list in the site collection that is configured for anonymous access.</span></span>
    
 
<span data-ttu-id="42ab1-121">Anleitungen für diese Aufgaben sind im Abschnitt [Konfigurieren einer SharePoint-Webanwendung und einer Websitesammlung und Liste für anonymen Zugriff](#Configuring) zu finden.</span><span class="sxs-lookup"><span data-stu-id="42ab1-121">Instructions for these tasks are in the section  [Configuring an SharePoint web application and site collection and list for anonymous access](#Configuring).</span></span>
 

 

## <a name="limitations-on-the-use-of-sharepoint-add-ins-by-anonymous-users"></a><span data-ttu-id="42ab1-122">Einschränkungen bei der Verwendung von SharePoint-Add-Ins durch anonyme Benutzer</span><span class="sxs-lookup"><span data-stu-id="42ab1-122">Limitations on the use of SharePoint Add-ins by anonymous users</span></span>

<span data-ttu-id="42ab1-123">Berücksichtigen Sie die folgenden Aspekte, wie Sie Ihr SharePoint-Add-In entwickeln:</span><span class="sxs-lookup"><span data-stu-id="42ab1-123">Consider the following facts as you design your SharePoint Add-in:</span></span>
 

 

- <span data-ttu-id="42ab1-p106">Wenn die SharePoint-Add-In in SharePoint gestartet wird, muss sie eine benutzerdefinierte Aktion oder ein Add-In-Webpart enthalten oder über einen benutzerdefinierten Link auf einer Seite gestartet werden. Der Grund dafür ist, dass Benutzer das Add-In nicht über die entsprechende Kachel starten können. Der Mechanismus, durch den Add-Ins über eine Kachel gestartet werden, erfordert den Einsatz einer speziellen  [Anwendungsseite](http://msdn.microsoft.com/library/685c8e01-b163-4b5e-888c-421d9ecbb25e%28Office.15%29.aspx), die für anonyme Benutzer nicht zugänglich ist. Eine weitere Möglichkeit ist, den Start des Add-Ins von außerhalb von SharePoint zu ermöglichen. In diesem Fall muss es die Nur-Add-In-Autorisierungsrichtlinie verwenden.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p106">If the SharePoint Add-in is launched from SharePoint, it has to include a custom action or an add-in part, or it must be launched from a custom link on a page. This is because anonymous users cannot launch the add-in by its tile. The mechanism by which add-ins are launched from the tile requires the use of a special  [application page](http://msdn.microsoft.com/library/685c8e01-b163-4b5e-888c-421d9ecbb25e%28Office.15%29.aspx) that is not accessible to anonymous users. Another option is to make the add-in launchable from outside SharePoint, in which case it has to use theadd-in-only authorization policy.</span></span>
    
 
- <span data-ttu-id="42ab1-p107">Ein anonymer Benutzer kann nur SharePoint-Add-Ins starten, die von anderen installiert wurden. Der Grund dafür ist, dass anonyme Benutzer die Seite **Add-In hinzufügen** nicht öffnen können.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p107">An anonymous user can only launch SharePoint Add-ins that have been installed by others. This is because anonymous users cannot open the **Add an Add-in** page.</span></span>
    
 
- <span data-ttu-id="42ab1-p108">Wenn ein angemeldeter Benutzer zu einer Website in einer lokalen SharePoint-Webanwendung navigiert, die für anonymen Zugriff konfiguriert wurde, wird die Identität des Benutzers in **Systemkonto** geändert. Diese Identität kann SharePoint-Add-Ins nicht installieren. Da anonyme Benutzer Add-Ins auch nicht installieren können, bedeutet dies, dass niemand SharePoint-Add-Ins installieren kann, wenn die Webanwendung für anonymen Zugriff konfiguriert ist. Entsprechend sollten SharePoint-Add-Ins auf Websites in der SharePoint-Webanwendung installiert werden, bevor die Webanwendung für anonymen Zugriff konfiguriert wird. Wenn später weitere Add-Ins installiert werden müssen, muss die Webanwendung vorübergehend so geändert werden, dass anonymer Zugriff deaktiviert wird, sodass die Add-Ins von einem angemeldeten Benutzer installiert werden können.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p108">When a logged in user navigates to a website in an on-premises SharePoint web application that has been configured for anonymous access, the user's identity changes to **System Account**. This identity cannot install SharePoint Add-ins. Since anonymous users also cannot install add-ins, this means that nobody can install a SharePoint Add-ins when the web application is configured for anonymous access. Accordingly, SharePoint Add-ins should be installed to websites in the SharePoint web application before the web application is configured for anonymous access. If other add-ins need to be installed later, the web application must be temporarily changed to disable anonymous access so that the add-ins can be installed by a logged in user.</span></span>
    
 
- <span data-ttu-id="42ab1-p109">Um die REST-APIs für die SharePoint-Suchfunktion in einer lokalen SharePoint-Website zu aktivieren, können Sie Abfrage-XML konfigurieren. Nähere Informationen dazu finden Sie unter  [Aktivieren von anonymen Such-REST-Abfragen](http://msdn.microsoft.com/library/office/jj163876.aspx#bk_AnonymousREST).</span><span class="sxs-lookup"><span data-stu-id="42ab1-p109">To enable the SharePoint Search REST APIs in an on-premises SharePoint website, you to configure some query XML. For details, see  [Enabling anonymous Search REST queries](http://msdn.microsoft.com/library/office/jj163876.aspx#bk_AnonymousREST).</span></span>
    
 
- <span data-ttu-id="42ab1-p110">Daten im Add-In-Web werden von den Suchindexern nicht durchforstet, sodass benutzerdefinierte Daten remote oder im Hostweb bereitgestellt werden müssen. Dies gilt für alle SharePoint-Add-Ins, wird aber hier erwähnt, da auf anonymen Zugriff ausgelegte Add-Ins häufig eine Suchfunktion erfordern.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p110">Data on the add-in web is not crawled by the search indexers, so custom data must be deployed remotely or in the host web. This applies to all SharePoint Add-ins, but we note it here because add-ins intended for anonymous access often require search functionality.</span></span>
    
 

## <a name="creating-provider-hosted-add-ins-that-are-anonymously-accessible"></a><span data-ttu-id="42ab1-139">Erstellen von vom Anbieter gehosteten Add-Ins, die anonym zugänglich sind</span><span class="sxs-lookup"><span data-stu-id="42ab1-139">Creating provider-hosted add-ins that are anonymously accessible</span></span>
<span data-ttu-id="42ab1-140"><a name="Cloud-hosted"> </a></span><span class="sxs-lookup"><span data-stu-id="42ab1-140"></span></span>

<span data-ttu-id="42ab1-p111">Um ein vom Anbieter gehostetes Add-In für anonyme Benutzer zugänglich zu machen, muss es lediglich so konfiguriert werden, dass es die Nur-Add-In-Autorisierungsrichtlinie verwendet. Wenn diese Richtlinie verwendet wird, fügt SharePoint nicht einmal Benutzerkontext ein, sodass es keine Rolle spielt, dass der Benutzer anonym ist. Es ist nur wichtig, dass dem Add-In-Prinzipal vom Mandantenadministrator, der das Add-In installiert, alle Berechtigungen gewährt werden, die er für das Hostweb benötigt, sowie alle Berechtigungen, die er für die übergeordnete Websitesammlung oder den übergeordneten Mandanten benötigt. Sie fordern Berechtigungen für das Hostweb im Add-In-Manifest an, genau so, wie Sie dies bei jedem anderen Add-In tun würden.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p111">Making a provider-hosted add-in accessible to anonymous users is simply a matter of configuring it to use the add-in-only authorization policy. When this policy is used, SharePoint does not even include a user context, so it doesn't matter that the user is anonymous. It is only necessary that the add-in principal is granted any permissions it needs to the host web -- and any it needs to the parent site collection or parent tenancy -- by the tenant administrator that installs the add-in. You request permissions to the host web in the add-in manifest just as you would any add-in.</span></span>
 

 

 <span data-ttu-id="42ab1-p112">**Hinweis** Wenn die SharePoint-Website für anonyme Benutzer zugänglich ist, erlaubt sie anstatt HTTPS-Zugriff normalerweise HTTP-Zugriff. Es können Sicherheitsprobleme auftreten, wenn in diesem Szenario die Nur-Add-In-Richtlinie für Add-Ins verwendet wird. Nähere Informationen dazu sowie eine Methode zur Behebung der Probleme finden Sie unter [Was jeder Entwickler über SharePoint-Add-Ins, CSOM und anonyme Veröffentlichungswebsites wissen muss](http://blogs.msdn.com/b/kaevans/archive/2013/10/24/what-every-developer-needs-to-know-about-sharepoint-apps-csom-and-anonymous-publishing-sites.aspx).</span><span class="sxs-lookup"><span data-stu-id="42ab1-p112">**Note** If the SharePoint site is accessible to anonymous users, it typically allows HTTP access, rather than HTTPS. There are potential security issues when the add-in-only policy is used for add-ins in this scenario. For details and a method of mitigating them, see  [What Every Developer Needs to Know About SharePoint Add-ins, CSOM, and Anonymous Publishing Sites](http://blogs.msdn.com/b/kaevans/archive/2013/10/24/what-every-developer-needs-to-know-about-sharepoint-apps-csom-and-anonymous-publishing-sites.aspx).</span></span>
 

<span data-ttu-id="42ab1-148">Zum Entwerfen eines Add-Ins, das die Nur-Add-In-Richtlinie verwendet, sind zwei Dinge erforderlich:</span><span class="sxs-lookup"><span data-stu-id="42ab1-148">Designing an add-in to use the add-in-only policy requires two things:</span></span>
 

 

- <span data-ttu-id="42ab1-149">Sie müssen `AllowAppOnlyPolicy="true"` zum **AppPermissionRequests**-Element im Add-In-Manifest hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="42ab1-149">You must add  `AllowAppOnlyPolicy="true"` to the **AppPermissionRequests** element in the add-in manifest.</span></span>
    
 
- <span data-ttu-id="42ab1-p113">Ihr Code muss vom OAuth-Autorisierungsserver einen Nur-Add-In-Zugriffstoken anfordern. Wenn Sie mit verwaltetem Code arbeiten, gibt es in den Codedateien, die von Microsoft Office-Entwicklertools für Visual Studio generiert werden, APIs, die speziell zu diesem Zweck erstellt wurden: "SharePointContext.cs" (oder ".vb") und "TokenHelper.cs" (oder ".vb").</span><span class="sxs-lookup"><span data-stu-id="42ab1-p113">Your code must ask for an add-in-only access token from the OAuth authorization server. If you are working with managed code, there are APIs specifically created for this purpose in the code files that are generated by Microsoft Office Developer Tools for Visual Studio: SharePointContext.cs (or .vb) and TokenHelper.cs (or .vb).</span></span>
    
 
<span data-ttu-id="42ab1-152">Details zur Nur-Add-In-Richtlinie (mit Codeausschnitten), zu Add-In-Berechtigungen und zum Add-In-Manifest finden Sie in diesen Themen:</span><span class="sxs-lookup"><span data-stu-id="42ab1-152">For details about the add-in-only policy (with code snippets), add-in permissions, and the add-in manifest see these topics:</span></span>
 

 

-  [<span data-ttu-id="42ab1-153">Add-In-Autorisierungsrichtlinientypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="42ab1-153">Add-in authorization policy types in SharePoint</span></span>](add-in-authorization-policy-types-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="42ab1-154">Add-In-Berechtigungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="42ab1-154">Add-in permissions in SharePoint</span></span>](add-in-permissions-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="42ab1-155">Hinweise zur App-Manifeststruktur und zum Paket eines SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="42ab1-155">Explore the app manifest structure and the package of a SharePoint Add-in</span></span>](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in)
    
 

## <a name="creating-sharepoint-hosted-add-ins-that-are-anonymously-accessible"></a><span data-ttu-id="42ab1-156">Erstellen von in SharePoint gehosteten Add-Ins, die anonym zugänglich sind</span><span class="sxs-lookup"><span data-stu-id="42ab1-156">Creating SharePoint-hosted add-ins that are anonymously accessible</span></span>
<span data-ttu-id="42ab1-157"><a name="SP-hosted"> </a></span><span class="sxs-lookup"><span data-stu-id="42ab1-157"></span></span>

<span data-ttu-id="42ab1-p114">Um ein in SharePoint gehostetes Add-In zu erstellen, das von anonymen Benutzern ausgeführt werden kann, sind keine speziellen Techniken erforderlich. Es wird genauso erstellt wie jedes andere in SharePoint gehostete Add-In. Nähere Informationen finden Sie unter  [Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins) und [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013).</span><span class="sxs-lookup"><span data-stu-id="42ab1-p114">Creating a SharePoint-hosted add-in that can be run by anonymous users does not require any special techniques. You create it the same way you would create any SharePoint-hosted add-in. For details, see  [Get started creating SharePoint-hosted SharePoint Add-ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins) and [Complete basic operations using JavaScript library code in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013).</span></span>
 

 
<span data-ttu-id="42ab1-p115">Was wirklich wichtig ist, um ein in SharePoint gehostetes Add-In für anonyme Benutzer verwendbar zu machen, ist, dass ein Mandantenadministrator die SharePoint Online-Websitesammlung so konfiguriert, dass sie anonymen Zugriff zulässt. Es ist Ihnen als Entwickler unmöglich, diese Konfiguration über das Add-In, einen Remote-Add-In-Ereignisempfänger oder die SharePoint-Add-In-Installationsinfrastruktur vorzunehmen. Sie können in das Add-In eine benutzerdefinierte Liste oder Bibliothek einschließen, aber Collaborative Application Markup Language (CAML) bietet keine Möglichkeit, es vorab für anonymen Zugriff zu konfigurieren. Daher muss dieser nach der Installation des Add-Ins konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p115">What's really crucial for making a SharePoint-hosted add-in usable by anonymous access is that the SharePoint Online site collection is configured by a tenant administrator to allow anonymous access. There is no way that you as a developer of a SharePoint-hosted add-in can make this configuration from the add-in, or a remote add-in event receiver, or with the SharePoint add-in installation infrastructure. You can include a custom list or library in the add-in, but Collaborative Application Markup Language (CAML) does not provide any way to preconfigure it for anonymous access, so it would have to be configured after the add-in is installed.</span></span>
 

 
<span data-ttu-id="42ab1-p116">Wenn Sie Ihr Add-In über den Office Store vertreiben und ein erheblicher Anteil Ihrer möglichen Kunden es besonders hilfreich fänden, wenn es für anonyme Benutzer zugänglich wäre, sollten Sie erwägen, diese Konfigurationsanforderung in Ihrer Add-In-Beschreibung zu erwähnen. Erwägen Sie außerdem, unten auf der Supportseite Ihres Add-Ins eine Version des Verfahrens **So konfigurieren Sie eine SharePoint Online-Websitesammlung für anonymen Zugriff** einzufügen.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p116">If you are marketing your add-in through the Office Store, and a significant portion of your potential customers would find the add-in most useful if it is accessible to anonymous users, then you should consider mentioning this configuration requirement in your add-in description. Consider also including a version of the procedure **To configure a SharePoint Online site collection for anonymous access** below in your add-in's support page.</span></span>
 

 
<span data-ttu-id="42ab1-p117">Wenn Ihr Add-In das JavaScript-Objektmodell (JSOM) von SharePoint verwendet, gibt es nur eine sehr wichtige Konfigurationsanforderung. Nur ein sehr kleiner Teil der JSOM-APIs ist standardmäßig für anonyme Benutzer zugänglich. Alle anderen erfordern, dass ein Benutzer die Berechtigung **Remoteschnittstellen verwenden** besitzt, und anonyme Benutzer besitzen diese Berechtigung nicht. Diese Anforderung muss in der übergeordneten Websitesammlung oder übergeordneten SharePoint-Webanwendung der Website deaktiviert werden, in der das Add-In installiert ist. Eine Beschreibung dazu finden Sie unter [Konfigurieren einer SharePoint-Webanwendung und einer Websitesammlung und Liste für anonymen Zugriff](#Configuring).</span><span class="sxs-lookup"><span data-stu-id="42ab1-p117">If your add-in uses SharePoint's JavaScript object model (JSOM), there is one configuration requirement that is very crucial. Only a very small portion of the JSOM APIs are accessible by default to anonymous users. All others require that a user have the **Use Remote Interfaces** permission and anonymous users do not have this permission. This requirement has to be turned off in the parent site collection or parent SharePoint web application of the website where the add-in is installed, as described in [Configuring an SharePoint web application and site collection and list for anonymous access](#Configuring).</span></span>
 

 

 <span data-ttu-id="42ab1-p118">**Hinweis** Wenn Sie die Anforderung, dass Benutzer die Berechtigung **Remoteschnittstellen verwenden** besitzen, deaktivieren, hat dies Auswirkungen auf den Datenschutz. Nähere Informationen finden Sie unter [Was jeder Entwickler über SharePoint-Add-Ins, CSOM und anonyme Veröffentlichungswebsites wissen muss](http://blogs.msdn.com/b/kaevans/archive/2013/10/24/what-every-developer-needs-to-know-about-sharepoint-apps-csom-and-anonymous-publishing-sites.aspx).</span><span class="sxs-lookup"><span data-stu-id="42ab1-p118">**Note** Turning off the requirement that users have the **Use Remote Interfaces** permission has implications for information privacy. For details, see [What Every Developer Needs to Know About SharePoint Add-ins, CSOM, and Anonymous Publishing Sites](http://blogs.msdn.com/b/kaevans/archive/2013/10/24/what-every-developer-needs-to-know-about-sharepoint-apps-csom-and-anonymous-publishing-sites.aspx).</span></span>
 


## <a name="limitations-of-sharepoint-hosted-add-ins-for-anonymous-users"></a><span data-ttu-id="42ab1-172">Einschränkungen von in SharePoint gehosteten Add-Ins für anonyme Benutzer</span><span class="sxs-lookup"><span data-stu-id="42ab1-172">Limitations of SharePoint-hosted add-ins for anonymous users</span></span>
<span data-ttu-id="42ab1-173"><a name="SP-hosted"> </a></span><span class="sxs-lookup"><span data-stu-id="42ab1-173"></span></span>

<span data-ttu-id="42ab1-174">Wir sind ehrlich mit Ihnen: Es gibt einige wesentliche Einschränkungen für in SharePoint gehostete Add-Ins für anonyme Benutzer, die Sie berücksichtigen müssen:</span><span class="sxs-lookup"><span data-stu-id="42ab1-174">We'll be honest with you: there are some significant limitations on SharePoint-hosted add-ins for anonymous users that you need to be aware of:</span></span>
 

 

- <span data-ttu-id="42ab1-p119">Es ist nicht möglich, eine Liste oder Bibliothek in einer SharePoint Online für anonyme Benutzer zugänglich zu machen. Entsprechen können JSOM-APIs, die Interaktionen mit Listen oder Bibliotheken erfordern, in SharePoint Online nicht von anonymen Benutzern verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p119">It is not possible to make a list or library on a SharePoint Online accessible to anonymous users. Accordingly, JSOM APIs that involve interaction with lists or libraries do not work on SharePoint Online for anonymous users.</span></span>
    
 
- <span data-ttu-id="42ab1-p120">Ein in SharePoint gehostetes Add-In, das auf einer  *lokalen*  SharePoint-Website installiert ist, kann alle JSOM-APIs verwenden. Die Webanwendung, die Websitesammlung sowie Listen oder Bibliotheken müssen allerdings *manuell*  für anonymen Zugriff konfiguriert werden, und die Berechtigungsanforderung **Remoteschnittstellen verwenden** muss deaktiviert werden. Wenn das Add-In im Add-In-Web benutzerdefinierte Listen oder Bibliotheken installiert, ist es Aufgabe der Benutzer, diese nach der Add-In-Installation manuell für anonymen Zugriff zu konfiguriere</span><span class="sxs-lookup"><span data-stu-id="42ab1-p120">A SharePoint-hosted add-in installed to an  *on-premises*  SharePoint website can make use all of the JSOM APIs. However, the web application, site collection, and lists/libraries must be *manually*  configured for anonymous access, and the **Use Remote Interfaces** permission requirement must be disabled. If the add-in installs custom lists/libraries to the add-in web, users are responsible for manually configuring these for anonymous access after add-in installation.</span></span>
    
 
- <span data-ttu-id="42ab1-180">Da Daten im Add-In-Web nicht von den Suchindexern durchforstet werden und es keine Möglichkeit gibt, benutzerdefinierte Listen oder Bibliotheken im Hostweb zu installieren, und da in SharePoint gehostete Add-Ins keine Remotekomponenten oder Ereignisempfänger enthalten können, sind benutzerdefinierte Daten in einem in SharePoint gehosteten Add-In nicht durchsuchba</span><span class="sxs-lookup"><span data-stu-id="42ab1-180">Because data on the add-in web is not crawled by the search indexers, and because there is no way to install custom lists or libraries to the host web, and because SharePoint-hosted add-ins cannot have remote components or event receivers, custom data in a SharePoint-hosted add-in is not searchable.</span></span>
    
 

## <a name="configuring-an-sharepoint-web-application-and-site-collection-and-list-for-anonymous-access"></a><span data-ttu-id="42ab1-181">Konfigurieren einer SharePoint-Webanwendung und einer Websitesammlung und Liste für anonymen Zugriff</span><span class="sxs-lookup"><span data-stu-id="42ab1-181">Configuring an SharePoint web application and site collection and list for anonymous access</span></span>
<span data-ttu-id="42ab1-182"><a name="Configuring"> </a></span><span class="sxs-lookup"><span data-stu-id="42ab1-182"></span></span>

<span data-ttu-id="42ab1-p121">Wenn Ihre SharePoint-Testinstallation lokal ist, müssen Sie die ersten beiden unten stehenden Verfahren ausführen, um zu testen, ob Ihre SharePoint-Add-In von anonymen Benutzern verwendet werden kann. Die Kunden, die Ihre SharePoint-Add-In installieren, müssen diese Verfahren auch für die übergeordnete Websitesammlung und die Webanwendung jeder Website durchführen, auf der Ihre SharePoint-Add-In installiert ist.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p121">If your test SharePoint installation is on-premises, you must carry out the first two procedures below in order to test whether your SharePoint Add-in can be used by anonymous users. The customers who install your SharePoint Add-in must also carry out these procedures for the parent site collection and web application of any website where your SharePoint Add-in is installed.</span></span>
 

 

 <span data-ttu-id="42ab1-p122">**Wichtig** Wenn möglich, sollten Sie das SharePoint-Add-In auf einer Website installieren, *bevor* Sie die ersten beiden Verfahren ausführen. Add-Ins können nicht auf jede Website in einer lokalen SharePoint-Webanwendung installiert werden, wenn die Webanwendung für anonymen Zugriff installiert wurde. Wenn die Webanwendung bereits für anonymen Zugriff installiert wurde, müssen Sie die Einstellung vorübergehend deaktivieren, um das Add-In zu installieren.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p122">**Important** If possible, you should install the SharePoint Add-in to a website  *before*  you carry out the first two procedures. Add-ins cannot be installed to any website in an on-premise SharePoint web application when the web application has been configured for anonymous access. If the web application has already been configured for anonymous access, you have to reverse that setting temporarily in order to install the add-in.</span></span>
 


### <a name="to-configure-the-parent-web-application-for-anonymous-access"></a><span data-ttu-id="42ab1-188">So konfigurieren Sie die übergeordnete Webanwendung für anonymen Zugriff</span><span class="sxs-lookup"><span data-stu-id="42ab1-188">To configure the parent web application for anonymous access</span></span>


1. <span data-ttu-id="42ab1-189">Wählen Sie in der **Zentraladministration** zuerst **Anwendungsverwaltung** und dann **Webanwendungen verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="42ab1-189">In **Central Administration**, choose **Application Management**, and then **Manage Web Applications**.</span></span>
    
 
2. <span data-ttu-id="42ab1-p123">(Optional) Wenn Sie für keine der vorhandenen SharePoint-Webanwendungen anonymen Zugriff erlauben möchten, erstellen Sie eine neue Webanwendung. (Das Webanwendungs-Erstellformular bietet Ihnen zwar die Option, anonymen Zugriff zuzulassen.  *Diese Option sollten Sie allerdings nicht verwenden*  . Anonymer Zugriff sollte erst aktiviert werden, *nachdem*  die SharePoint-Add-In installiert wurde.) Nähere Informationen finden Sie unter [Create a web application in SharePoint](http://msdn.microsoft.com/library/121c8d83-a508-4437-978b-303096aa59df.aspx).</span><span class="sxs-lookup"><span data-stu-id="42ab1-p123">(Optional) If you don't want to allow anonymous access for any of the existing SharePoint web applications, create a new web application. (Although the web application creation form gives you the option of allowing anonymous access,  *do not use this option*  . Anonymous access should not be enabled until *after*  the SharePoint Add-in is installed.) For details, see [Create a web application in SharePoint](http://msdn.microsoft.com/library/121c8d83-a508-4437-978b-303096aa59df.aspx).</span></span>
    
 
3. <span data-ttu-id="42ab1-193">Wählen Sie in der Liste der Webanwendungen eine aus, die für anonyme Benutzer zugänglich sein soll, und wählen Sie im Menüband **Authentifizierungsanbieter** aus.</span><span class="sxs-lookup"><span data-stu-id="42ab1-193">On the list of web applications, select the one that is to be accessible by anonymous users, and select **Authentication Providers** on the ribbon.</span></span>
    
 
4. <span data-ttu-id="42ab1-p124">Wählen Sie im daraufhin angezeigten Popup die Zone aus, für die anonymer Zugriff aktiviert werden soll. Normalerweise ist dies **Internet** oder **Standard**. Das Formular **Authentifizierung bearbeiten** wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p124">On the callout that opens, choose the zone for which anonymous access is to be enabled. Typically, this is **Internet** or **Default**. The **Edit Authentication** form opens.</span></span>
    
 
5. <span data-ttu-id="42ab1-p125">Aktivieren Sie das Kontrollkästchen **Anonymen Zugriff aktivieren**, falls es nicht bereits aktiviert ist. Damit wird eine Standardeinstellung festgelegt, die für bestimmte Websitesammlungen deaktiviert werden kann. Wenn Sie diese allerdings für die Webanwendung nicht aktivieren, können Sie sie für keine Websitesammlung aktivieren.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p125">Check the **Enable anonymous access** box, it if isn't enabled already. This sets a default that can be turned off for specific site collections, but if you do not enable this for the web application, you cannot enable it for any site collections.</span></span>
    
 
6. <span data-ttu-id="42ab1-p126">(Optional) Deaktivieren Sie das Kontrollkästchen **Berechtigung 'Remoteschnittstellen verwenden' verlangen**. Dadurch wird Code und Skript, der bzw. das im Kontext eines anonymen Benutzers ausgeführt wird, erlaubt, in jeder Websitesammlung Aufrufe an das Clientobjektmodell von SharePoint zu richten. Sie können die Anforderung für keine Websitesammlung erneut aktivieren. Wenn Sie das Kontrollkästchen aktiviert lassen, bedeutet dies, dass anonyme Benutzer standardmäßig nicht auf die Clientobjektmodelle zugreifen können, aber Sie können die Anforderung für bestimmte Websitesammlungen deaktivieren (und ihnen den Zugriff erlauben).</span><span class="sxs-lookup"><span data-stu-id="42ab1-p126">(Optional) Uncheck the **Require Use Remote Interfaces permission** box. Doing so allows code and script running in the context of an anonymous user to make calls to SharePoint's client object model on every site collection. You cannot re-enable the requirement for any site collections. Leaving the box checked means that by default anonymous users cannot access the client object models, but you can disable the requirement (and give them access) for specific site collections.</span></span>
    
     <span data-ttu-id="42ab1-p127">**Hinweis** Im Zusammenhang mit der Entwicklung von SharePoint-Add-Ins für anonyme Benutzer ist diese Einstellung nur für in SharePoint gehostete Apps von Bedeutung. Vom Anbieter gehostete SharePoint-Add-Ins, die auf anonyme Benutzer ausgelegt sind, verwenden eine Technik, welche die Berechtigungen des Benutzers irrelevant machen. Weitere Informationen hierzu finden Sie oben im Abschnitt [Erstellen von vom Anbieter gehosteten Add-Ins, die anonym zugänglich sind](#Cloud-hosted).</span><span class="sxs-lookup"><span data-stu-id="42ab1-p127">**Note** In the context of developing SharePoint Add-ins for anonymous users, this setting is only meaningful for SharePoint-hosted add-ins. Provider-hosted SharePoint Add-ins that are designed for anonymous users use a technique that makes the user's permissions irrelevant. For more information about this, see the section  [Creating provider-hosted add-ins that are anonymously accessible](#Cloud-hosted) above.</span></span>
7. <span data-ttu-id="42ab1-206">Wählen Sie zum Schließen des Formulars **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="42ab1-206">Choose **Save** to close the form.</span></span>
    
 
8. <span data-ttu-id="42ab1-207">Wählen Sie im Menüband **Richtlinie für anonymen Zugriff** aus, während die Webanwendung markiert ist.</span><span class="sxs-lookup"><span data-stu-id="42ab1-207">With the web application still highlighted, select **Anonymous Policy** on the ribbon.</span></span>
    
 
9. <span data-ttu-id="42ab1-p128">Wählen Sie im Formular **Einschränkungen für anonymen Zugriff** die Zone aus, und achten Sie darauf, dass das Optionsfeld **Keine** aktiviert ist. Wenn das SharePoint-Add-In, das Sie testen, nur Leserechte für SharePoint-Daten benötigt, aktivieren Sie stattdessen **Schreiben verweigern**.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p128">In the **Anonymous Access Restrictions** form, choose the zone and be sure that the **None** radio button is enabled. If the SharePoint Add-in that you are testing needs only read rights to SharePoint data, enable **Deny Write** instead.</span></span>
    
     <span data-ttu-id="42ab1-210">**Hinweis** Dies ist eine weitere Einstellung, die im Zusammenhang mit der Entwicklung von SharePoint-Add-Ins für anonyme Benutzer nur für in SharePoint gehostete Add-Ins von Bedeutung ist.</span><span class="sxs-lookup"><span data-stu-id="42ab1-210">**Note** This is another setting that, in the context of developing SharePoint Add-ins for anonymous users, is only meaningful for SharePoint-hosted add-ins.</span></span>
10. <span data-ttu-id="42ab1-211">Wenn Sie in Schritt 2 eine neue Webanwendung erstellt haben, müssen Sie darin eine Websitesammlung erstellen.</span><span class="sxs-lookup"><span data-stu-id="42ab1-211">If you created a new web application in step 2, you have to create a site collection in it.</span></span>
    
 

### <a name="to-configure-an-on-premises-site-collection-for-anonymous-access"></a><span data-ttu-id="42ab1-212">So konfigurieren Sie eine lokale Websitesammlung für den anonymen Zugriff</span><span class="sxs-lookup"><span data-stu-id="42ab1-212">To configure an on-premises site collection for anonymous access</span></span>


1. <span data-ttu-id="42ab1-213">Wählen Sie auf der Startseite einer Websitesammlung in der Webanwendung das Zahnradsymbol und dann **Websiteeinstellungen** aus.</span><span class="sxs-lookup"><span data-stu-id="42ab1-213">On the home page of a site collection in the web application, select the gear icon and then **Site Settings**.</span></span>
    
 
2. <span data-ttu-id="42ab1-214">Wählen Sie im Abschnitt **Benutzer und Berechtigungen** der Seite **Websiteeinstellungen** die Option **Websiteberechtigungen** aus.</span><span class="sxs-lookup"><span data-stu-id="42ab1-214">In the **Users and Permissions** section of the **Site Settings** page, select **Site permissions**.</span></span>
    
 
3. <span data-ttu-id="42ab1-215">Wählen Sie im Menüband **Anonymer Zugriff** aus.</span><span class="sxs-lookup"><span data-stu-id="42ab1-215">Choose **Anonymous Access** on the ribbon.</span></span>
    
 
4. <span data-ttu-id="42ab1-p129">Wählen Sie im Formular **Anonymer Zugriff** entweder **Gesamte Website** oder **Listen und Bibliotheken** aus, je nachdem, welche Zugriffsebene das Add-In benötigt, das Sie testen. (Unabhängig davon, welche Option Sie auswählen, können anonyme Benutzer nur dann auf eine Liste oder Bibliothek mit einem in SharePoint gehosteten Add-In zugreifen, wenn die Liste oder Bibliothek einzeln für anonymen Zugriff konfiguriert ist. Das unten stehende Verfahren beschreibt, wie Sie dabei vorgehen.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p129">On the **Anonymous Access** form, choose either **Entire Web site** or **Lists and libraries**, depending on the level of access the add-in that you are testing needs. (Regardless of which option you choose, anonymous users cannot access a list or library with a SharePoint-hosted add-in unless the list of library is individually configured to all anonymous access. A procedure below describes how to do this.</span></span>
    
 
5. <span data-ttu-id="42ab1-p130">Wenn das Add-In, das Sie testen, auf das SharePoint-Clientobjektmodell zugreifen muss, achten Sie darauf, dass das Kontrollkästchen **Berechtigung 'Remoteschnittstellen verwenden' verlangen** *nicht* aktiviert ist. Wenn das Kontrollkästchen ausgegraut ist, wurde die Anforderung auf der Webanwendungsebene deaktiviert, was den gleichen Effekt hat wie das deaktivierte Kontrollkästchen. (Wie im vorherigen Verfahren erwähnt, ist diese Einstellung im Zusammenfassung mit der Entwicklung von SharePoint-Add-Ins für anonyme Benutzer nur für in SharePoint gehostete Add-Ins relevant.)</span><span class="sxs-lookup"><span data-stu-id="42ab1-p130">If the add-in you are testing needs to access the SharePoint client object model, ensure that the **Require Use Remote Interfaces permission** box is *not*  checked. If the checkbox is grayed out, then the requirement was turned off at the web application level which has the same effect as the box being unchecked. (As noted in the previous procedure, this setting, in the context of developing SharePoint Add-ins for anonymous users, is only meaningful for SharePoint-hosted apps.)</span></span>
    
 

 <span data-ttu-id="42ab1-p131">**Wichtig** Das folgende Verfahren kann nur auf einer öffentlichen Website in SharePoint Online ausgeführt werden. (Weitere Informationen zur Verwendung von öffentlichen Websites in Microsoft SharePoint Online finden Sie unter [Hilfe zu öffentlichen Websites für Office 365](http://office.microsoft.com/en-gb/office365-sharepoint-online-enterprise-help/public-website-help-for-office-365-HA102891740.aspx?CTT=1).)</span><span class="sxs-lookup"><span data-stu-id="42ab1-p131">**Important** The following procedure can only be carried out on a public website in SharePoint Online. (For more information about the use of Public Websites in Microsoft SharePoint Online, see  [Public Website help for Office 365](http://office.microsoft.com/en-gb/office365-sharepoint-online-enterprise-help/public-website-help-for-office-365-HA102891740.aspx?CTT=1).)</span></span>
 


### <a name="to-configure-a-sharepoint-online-site-collection-for-anonymous-access"></a><span data-ttu-id="42ab1-224">So konfigurieren Sie eine SharePoint Online-Websitesammlung für anonymen Zugriff</span><span class="sxs-lookup"><span data-stu-id="42ab1-224">To configure a SharePoint Online site collection for anonymous access</span></span>


1. <span data-ttu-id="42ab1-225">Melden Sie sich bei Office 365 als Mandantenadministrator an.</span><span class="sxs-lookup"><span data-stu-id="42ab1-225">Login to Office 365 as a tenant administrator.</span></span>
    
 
2. <span data-ttu-id="42ab1-p132">Wählen Sie auf der Startseite der Websitesammlung nahe der oberen rechten Ecke der Seite **WEBSITE ONLINE STELLEN** aus. Mit dieser Aktion wird die Anforderung **Berechtigung 'Remoteschnittstellen verwenden' verlangen** deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p132">On the home page of the site collection, choose **MAKE WEBSITE ONLINE** near the upper right corner of the page. This action also turns off the **Use Remote Interfaces permission** requirement.</span></span>
    
 
<span data-ttu-id="42ab1-p133">Wenn Sie ein in SharePoint gehostetes Add-In entwickeln und es auf eine SharePoint-Liste zugreift, müssen Sie in Ihrer Testwebsitesammlung auch das folgende Verfahren ausführen. Auch Kunden, die Ihr Add-In verwenden, müssen dieses Verfahren auf jeder Website durchführen, auf der das Add-In installiert ist. Einem Add-In ist es nicht möglich, programmgesteuert oder deskriptiv eine Liste für anonymen Zugriff zu konfigurieren. Add-Ins können benutzerdefinierte Listen installieren, diese Listen aber nicht vorab für anonymen Zugriff konfigurieren. Die Konfiguration muss manuell erfolgen, nachdem das Add-In installiert wurde. Wenn Sie ein vom Anbieter gehostetes SharePoint-Add-In für anonyme Benutzer entwickeln, ist dieses Verfahren nicht erforderlic</span><span class="sxs-lookup"><span data-stu-id="42ab1-p133">If you are developing a SharePoint-hosted add-in and it accesses a SharePoint list, you must also carry out the following procedure in your test site collection. Customers who use your add-in will need to do this as well on any website where the add-in is installed. There is no way that an add-in can programmatically or descriptively configure a list for anonymous access. Add-ins can install custom lists, but there is no way to preconfigure such lists for anonymous access. The configuration must still be done manually after the add-in is installed. If you are developing a provider-hosted SharePoint Add-in for anonymous users, this procedure is not required.</span></span>
 

 

 <span data-ttu-id="42ab1-234">**Hinweis** Dieses Verfahren kann nicht in einer SharePoint Online-Websitesammlung ausgeführt werden. Daher können in SharePoint gehostete Add-Ins, die in SharePoint Online installiert sind und von anonymen Benutzern verwendet werden sollen, keine Listen oder Bibliotheken aufrufen.</span><span class="sxs-lookup"><span data-stu-id="42ab1-234">**Note** This procedure cannot be carried out in a SharePoint Online site collection, so SharePoint-hosted add-ins that are installed to SharePoint Online and intended for use by anonymous users cannot access lists or libraries.</span></span>
 


### <a name="to-configure-an-list-or-library-for-anonymous-access"></a><span data-ttu-id="42ab1-235">So konfigurieren Sie eine Liste oder Bibliothek für anonymen Zugriff</span><span class="sxs-lookup"><span data-stu-id="42ab1-235">To configure an list or library for anonymous access</span></span>


1. <span data-ttu-id="42ab1-p134">Navigieren Sie zu einer Liste oder Bibliothek, auf die das SharePoint-Add-In zugreift, das Sie testen, und öffnen Sie die **Listeneinstellungen** oder **Bibliothekseinstellungen**. Bei einer SharePoint Online-Website müssen Sie als Mandantenadministrator angemeldet sein.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p134">Navigate to a list or library that the SharePoint Add-in that you are testing accesses and open the **List Settings** or **Library Settings**. For a SharePoint Online site, you must be logged in as a tenant administrator.</span></span>
    
 
2. <span data-ttu-id="42ab1-238">Wählen Sie **Berechtigungen für diese Liste/Bibliothek** aus.</span><span class="sxs-lookup"><span data-stu-id="42ab1-238">Choose **Permissions for this list/library**.</span></span>
    
 
3. <span data-ttu-id="42ab1-239">Wählen Sie auf der Seite, die daraufhin geöffnet wird, auf der Registerkarte **Berechtigungen** die Option **Berechtigungsvererbung beenden** aus, und wählen Sie dann **OK** aus, wenn Sie zur Bestätigung aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="42ab1-239">On the page that opens, choose **Stop Inheriting Permissions** on the **Permissions** tab, and then choose **OK** on the confirmation prompt.</span></span>
    
 
4. <span data-ttu-id="42ab1-240">Wählen Sie auf der Registerkarte **Berechtigung** die Option **Anonymer Zugriff** aus.</span><span class="sxs-lookup"><span data-stu-id="42ab1-240">Choose **Anonymous Access** on the **Permission** tab.</span></span>
    
 
5. <span data-ttu-id="42ab1-p135">Wählen Sie im Formular **Anonymer Zugriff**, das daraufhin geöffnet wird, alle Berechtigungen aus, welche die Benutzer des SharePoint-Add-Ins benötigen. Sie können Berechtigungen zum Anzeigen, Bearbeiten, Hinzufügen und Löschen von Elementen erteilen. Sie können keinen Vollzugriff gewähren. Somit können anonyme Benutzer das Schema der Liste oder Listeneinstellungen nicht ändern.</span><span class="sxs-lookup"><span data-stu-id="42ab1-p135">On the **Anonymous Access** form that opens, select all of the permissions that that users of the SharePoint Add-in require. You can grant permission to View, Edit, Add, and Delete items. You cannot grant Full Control, so anonymous users cannot change the schema of the list or change list settings.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="42ab1-244">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="42ab1-244">Additional resources</span></span>
<span data-ttu-id="42ab1-245"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="42ab1-245"></span></span>


-  [<span data-ttu-id="42ab1-246">Entwickeln von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="42ab1-246">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins)
    
 

