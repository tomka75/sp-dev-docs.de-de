---
title: "Wichtige Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: bdc7c2f6954931f3af8cc8e539b973a1ba238bb6
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape"></a><span data-ttu-id="846e8-102">Wichtige Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="846e8-102">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>
<span data-ttu-id="846e8-p101">Dieser Artikel enthält Informationen zur Architektur von SharePoint-Add-Ins und zum Modell für SharePoint-Add-Ins, einschließlich Add-In-Hostingoptionen, Benutzeroberflächenoptionen, Bereitstellungssystem, Sicherheitssystem und Lebenszyklus. Dieser Artikel ergänzt den Inhalt des Artikels  [SharePoint-Add-Ins](sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="846e8-p101">Learn about aspects of the architecture of SharePoint Add-ins and the model for SharePoint Add-ins, including the add-in hosting options, user interface options, deployment system, security system, and lifecycle. This article supplements the information in the article  [SharePoint Add-ins](sharepoint-add-ins.md).</span></span>
 

 <span data-ttu-id="846e8-p102">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="846e8-p102">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="sharepoint-add-ins-hosting-options"></a><span data-ttu-id="846e8-108">Hostingoptionen für SharePoint Add-Ins</span><span class="sxs-lookup"><span data-stu-id="846e8-108">SharePoint Add-ins hosting options</span></span>
<span data-ttu-id="846e8-109"><a name="SPAppModelArch_SPCenteredVsCloudCentered"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-109"><a name="SPAppModelArch_SPCenteredVsCloudCentered"> </a></span></span>

<span data-ttu-id="846e8-110">Das SharePoint-Add-In-Modell bietet folgende Möglichkeiten zum Hosten der Komponenten eines SharePoint-Add-Ins:</span><span class="sxs-lookup"><span data-stu-id="846e8-110">The SharePoint add-in model provides the following ways to host the components of a SharePoint Add-in:</span></span> 
 

 

-  <span data-ttu-id="846e8-p103">**Vom Anbieter gehostet:** Add-In, die mindestens eine Remotekomponente und möglicherweise auch SharePoint-Komponenten enthalten. Add-In, deren SharePoint-fremde Komponenten von Ihrer Logik auf Ihrem Hardware- oder Cloudkonto bereitgestellt werden, oder auf dem Hardware- oder Cloudkonto des Kunden mithilfe von Installationsprogrammen und Anleitungen, die Sie bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="846e8-p103">**Provider-hosted:** Add-ins that include at least one remote component and may also include SharePoint components. The non-SharePoint components are deployed by your logic on your hardware or cloud account, or deployed on the customer's hardware or cloud account using installation programs and instructions that you provide.</span></span>
    
 
-  <span data-ttu-id="846e8-113">**Von SharePoint-gehostet:** Add-Ins, die nur SharePoint-Komponenten und -Logik enthalten, die auf dem Client ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="846e8-113">**SharePoint-hosted:** Add-ins that include only SharePoint components and logic that runs on the client.</span></span>
    
 
<span data-ttu-id="846e8-114">Ausführlichere Informationen über Hostingoptionen sowie Anleitungen für die Wahl der geeigneten Option finden Sie unter  [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="846e8-114">For more detailed information about hosting options and some guidance for how to choose between them, see  [Choose patterns for developing and hosting your SharePoint Add-in](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in.md).</span></span>
 

 

## <a name="add-in-webs-host-webs-features-and-sharepoint-components-in-add-ins"></a><span data-ttu-id="846e8-115">Add-In-Webs, Hostwebs, Features und SharePoint-Komponenten in Add-Ins</span><span class="sxs-lookup"><span data-stu-id="846e8-115">Add-in webs, host webs, Features, and SharePoint components in add-ins</span></span>
<span data-ttu-id="846e8-116"><a name="SPComponents"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-116"><a name="SPComponents"> </a></span></span>

<span data-ttu-id="846e8-p104">Die Website, auf der ein SharePoint-Add-In installiert wird, wird als Hostwebsite bezeichnet. Die signifikanten Teile des SharePoint-Add-In werden jedoch, gleichgültig, ob es sich um SharePoint-Komponenten oder externe Komponenten handelt, nicht auf der Hostwebsite bereitgestellt. Externe Teile werden auf externen Servern oder Cloudkonten bereitgestellt. SharePoint-Komponenten werden auf einer speziellen Website mit eigener Domäne bereitgestellt. Diese wird als Add-In-Website bezeichnet. Nur eine begrenzte Gruppe von UI-Elementen, die Benutzern Zugriff zu den anderen Komponenten des Add-Ins ermöglichen, werden für die Hostwebsite bereitgestellt. Diese UI-Komponenten in der Hostwebsite werden als Teil eines Hostweb-Features bereitgestellt - ein Feature, das sich lose im Add-In-Paket anstatt in einer WSP-Datei befindet. Die Komponenten, die für die Add-In-Website bereitgestellt werden, sind immer in Features enthalten, die sich in einer WSP-Datei befinden. Beide Arten von Features müssen über **Web**-Bereich verfügen. Ein anderer Bereich ist für Features in SharePoint-Add-Ins nicht möglich.</span><span class="sxs-lookup"><span data-stu-id="846e8-p104">The website to which a SharePoint Add-in is installed is called the host web. However, the significant parts of the SharePoint Add-in, whether they are SharePoint components or external components, are not deployed to the host web. External parts are deployed to external servers or cloud accounts. SharePoint components are deployed to a special website with its own domain. This is called the add-in web. Only a limited set of UI elements that give users access to the add-in's other components are deployed to the host web. These UI components in the host web are deployed as part of a host web Feature — a Feature that is loose in the add-in package instead of inside a .wsp file. The components that are deployed to the add-in web are always in Features that are inside a .wsp file. Both kinds of Features must have  **Web** scope. No other scope is possible for Features in SharePoint Add-ins.</span></span>
 

 
<span data-ttu-id="846e8-p105">Als allgemeine Regel gilt: Jede SharePoint-Komponente, die keinen benutzerdefinierten Code enthält, der auf SharePoint-Servern ausgeführt wird, kann einem SharePoint-Add-In hinzugefügt werden (und für die Add-In-Website bereitgestellt werden). Es gibt jedoch einige Ausnahmen und Feinheiten im Hinblick darauf, wie und wo die Komponenten bereitgestellt werden. Weitere Informationen zu diesen Feinheiten sowie über Hostwebsites, die isolierten Add-In-Websites und Features in Add-Ins finden Sie unter  [Hostwebsites, Add-In-Websites und SharePoint-Komponenten in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="846e8-p105">As a general rule, any SharePoint component that does not include custom code that runs on the SharePoint servers can be included in a SharePoint Add-in (and be deployed to the add-in web). There are, however, some exceptions and some nuances to how and where the components are deployed. For more information about these nuances and about host webs, the isolated add-in webs, and Features in add-ins, see  [Host webs, add-in webs, and SharePoint components in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md).</span></span>
 

 

## <a name="accessing-the-add-in-from-the-ui"></a><span data-ttu-id="846e8-130">Zugreifen auf das Add-In über die Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="846e8-130">Accessing the add-in from the UI</span></span>
<span data-ttu-id="846e8-131"><a name="AccessingApp"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-131"><a name="AccessingApp"> </a></span></span>

<span data-ttu-id="846e8-p106">Wenn ein SharePoint-Add-In auf einer Website installiert ist, wird das Add-In auf der Seite **Websiteinhalt** der Hostwebsite aufgeführt. Benutzer können das Add-In auf dieser Seite starten. Wenn das Add-In auf diese Weise geöffnet wird, wird es im Vollbildmodus ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="846e8-p106">When a SharePoint Add-in is installed on a website, the add-in is listed on the  **Site Contents** page of the host web. Users can start the add-in from that page. When opened in this way, the add-in runs in full-screen mode.</span></span>
 

 
<span data-ttu-id="846e8-p107">Eine andere Möglichkeit zum Anzeigen eines SharePoint-Add-In ist über ein Add-In-Part. Ein Add-In-Part ist ein Webpart-Typ, der durch die Klasse **ClientWebPart** repräsentiert wird. Diese Art von Webpart ist im Wesentlichen ein Wrapper für ein IFrame-Element, das eine Seite des Add-Ins hostet. Im einfachsten Fall ist die einzige wichtige Eigenschaft des Webparts eine URL, die auf die Seite verweist. Webparts können jedoch über benutzerdefinierte Eigenschaften verfügen, die Benutzer in einem Toolpart festlegen können. Solche Eigenschaften können z. B. verwendet werden, um Kontextinformationen, wie die Postleitzahl des Benutzers, festzulegen. Um Ihrem Add-In ein solches Add-In-Part hinzuzufügen, erstellen Sie ein Hostweb-Feature im Add-In und fügen deklaratives Webpart-Markup hinzu. Wie jedes andere Webpart wird es in der SharePoint-Benutzeroberfläche angezeigt, über die Benutzer Webparts hinzufügen. Sie können mehr als ein Add-In-Part mit Ihrem Add-In bereitstellen, wenn Sie noch mehr Variabilität benötigen. Beispielsweise kann ein Wetter-Add-In über ein Add-In-Part verfügen, das das aktuelle Wetter anzeigt, und ein zweites Add-In-Part, das eine Wettervorhersage für eine Woche anzeigt. Die beiden Parts können sich in Größe und Funktionalität unterscheiden.</span><span class="sxs-lookup"><span data-stu-id="846e8-p107">Another way that a SharePoint Add-in can be surfaced is through an add-in part, a type of Web Part that is represented by the  **ClientWebPart** class. This kind of Web Part is essentially a wrapper for an IFrame that would host a page of the add-in. In the simplest case, the only significant property of the Web Part is a URL that points to the page. But Web Parts can have custom properties that users can set in a Tool Part. Such properties could be used, for example, to set context information such as the user's ZIP Code or Postal Code. To include such an add-in part in your add-in, you create a host web Feature in the add-in and add declarative Web Part markup. Like any other Web Part, it appears in the SharePoint UI from which users add Web Parts. You can have more than one add-in part deployed with your add-in if you need even more variability. For example, a weather add-in can have an add-in part that shows current weather and a second add-in part that shows a weekly forecast. The two parts can have different sizes and functionality.</span></span>
 

 

 <span data-ttu-id="846e8-p108">**Hinweis** Sie können Add-In-Parts auch für die Add-In-Website bereitstellen. Dazu muss das Markup für das Webpart Teil eines Features in einer WSP-Datei im Add-In-Paket sein, nicht im Hostweb-Feature.</span><span class="sxs-lookup"><span data-stu-id="846e8-p108">**Note**  You can also deploy add-in parts to the add-in web. To implement this, the markup for the Web Part would be part of a Feature inside a .wsp file in the add-in package, not in the host web Feature.</span></span>
 

<span data-ttu-id="846e8-p109">Es wird empfohlen, dass Sie das Erscheinungsbild Ihrer Add-Ins so weit wie möglich an SharePoint orientieren. Dies ist jedoch nicht zwingend erforderlich und möglicherweise nicht immer die beste Möglichkeit.Weitere Informationen zu den UX-Richtlinien finden Sie unter  [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="846e8-p109">We recommend that you try to give your add-ins a SharePoint appearance to the extent possible, although that is not mandatory and may not always be the best choice. For more information about the user experience guidelines, see  [UX design for SharePoint Add-ins](ux-design-for-sharepoint-add-ins.md).</span></span> 
 

 
<span data-ttu-id="846e8-p110">Beispielsweise gibt es eine spezielle Masterseite mit dem Namen app.master. Diese Seite ist für die Verwendung durch die Seiten von Add-Ins optimiert. Die app.master-Seite ist Teil einer neuen Websitedefinition, die in SharePoint enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="846e8-p110">There is, for example, a special master page called app.master. This page is optimized for use by the pages of add-ins. The app.master page is part of a new site definition that is included in SharePoint.</span></span> 
 

 
<span data-ttu-id="846e8-p111">Ein anderes Tool, das Sie verwenden können, um für Ihre Add-Ins ein einheitliches Aussehen und Verhalten mit SharePoint zu erreichen, ist das Chromsteuerelement, das im Lieferumfang von SharePoint enthalten ist. Dieses Steuerelement ermöglicht es Ihnen, Ihren Add-In-Seiten den SharePoint-Navigationsheaderbereich hinzuzufügen, dies gilt auch für extern gehostete Seiten. Weitere Informationen zum UX-Design in SharePoint-Add-Ins finden Sie unter  [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins.md). Weitere Informationen über das Chromsteuerelement finden Sie unter  [Verwenden des Client-Chromsteuerelements in Add-Ins für SharePoint](use-the-client-chrome-control-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="846e8-p111">Another tool you can use to help your add-ins maintain a consistent look and feel with SharePoint is the chrome control that ships with SharePoint. This control enables you to add the SharePoint navigation header area to your add-in pages, including pages hosted externally. For more information about UX design in SharePoint Add-ins, see  [UX design for SharePoint Add-ins](ux-design-for-sharepoint-add-ins.md). For more information about the chrome control, see  [Use the client chrome control in SharePoint Add-ins](use-the-client-chrome-control-in-sharepoint-add-ins.md).</span></span>
 

 

## <a name="add-in-package-structure"></a><span data-ttu-id="846e8-154">Add-In-Paketstruktur</span><span class="sxs-lookup"><span data-stu-id="846e8-154">Add-in package structure</span></span>
<span data-ttu-id="846e8-155"><a name="SPAppModelArch_Package"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-155"><a name="SPAppModelArch_Package"> </a></span></span>

<span data-ttu-id="846e8-p112">Ein SharePoint-Add-In-Paket ist eine Datei, die die Erweiterung „.app" hat und mit  [OPC (Open Packaging Conventions)](http://msdn.microsoft.com/en-us/magazine/cc163372.aspx) kompatibel ist. (Sie können die Datei öffnen, indem Sie „.zip" als zusätzliche Erweiterung zum Dateinamen hinzufügen und die Datei dann im Windows Explorer öffnen.) Das Paket enthält ein Add-In-Manifest, das bestimmte Eigenschaften des Add-Ins und Anweisungen für die SharePoint-Installationsinfrastruktur spezifiziert. Weitere Informationen über das Add-In-Manifest und -Paket finden Sie unter [Hinweise zur App-Manifeststruktur und zum Paket eines SharePoint-Add-Ins](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="846e8-p112">A SharePoint Add-in package is a file that has an ".app" extension and that complies with the  [Open Packaging Conventions (OPC)](http://msdn.microsoft.com/en-us/magazine/cc163372.aspx). (You can open the file by adding ".zip" as an extra extension on the filename and then opening it in Windows Explorer.) It contains an add-in manifest that specifies certain properties of the add-in and instructions to the SharePoint installation infrastructure. For more information about the add-in manifest and package, see  [Explore the app manifest structure and the package of a SharePoint Add-in](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in.md).</span></span>
 

 

## <a name="permissions-authentication-and-authorization-for-sharepoint-add-ins"></a><span data-ttu-id="846e8-159">Berechtigungen, Authentifizierung und Autorisierung für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="846e8-159">Permissions, authentication, and authorization for SharePoint add-ins</span></span>
<span data-ttu-id="846e8-160"><a name="SPAppModelArch_Running"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-160"><a name="SPAppModelArch_Running"> </a></span></span>

<span data-ttu-id="846e8-161">SharePoint führt ein neues Add-In-Berechtigungs- und Sicherheitssystem ein.</span><span class="sxs-lookup"><span data-stu-id="846e8-161">SharePoint introduces a new add-in permissions and security system.</span></span>
 

 

### <a name="add-in-permissions"></a><span data-ttu-id="846e8-162">Add-In-Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="846e8-162">Add-in permissions</span></span>
<span data-ttu-id="846e8-163"><a name="AppPermissions"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-163"><a name="AppPermissions"> </a></span></span>

<span data-ttu-id="846e8-p113">SharePoint-Add-Ins verfügen wie Benutzer und Gruppen über Berechtigungen. Dadurch kann ein Add-In über eine Gruppe von Berechtigungen verfügen, die sich von den Berechtigungen des Benutzers, der das Add-In ausführt, unterscheiden.</span><span class="sxs-lookup"><span data-stu-id="846e8-p113">SharePoint Add-ins have permissions just as users and groups do. This enables an add-in to have a set of permissions that are different from the permissions of the user who is executing the add-in.</span></span> 
 

 
<span data-ttu-id="846e8-p114">Sie müssen in der Add-In-Manifest-Datei die Berechtigungen anfordern, die ein Add-In für die Ausführung benötigt. Der Benutzer, der das Add-In hinzufügt, muss diese Rechte erteilen, wobei er nur die Berechtigungen erteilen kann, über die er selbst als Benutzer verfügt. Die Erteilung muss für alle angeforderten Berechtigungen oder für keine davon erfolgen, um die Berechtigungsverwaltung für Benutzer und Entwickler zu vereinfachen. (Der Add-In-Prinzipal verfügt grundsätzlich über Vollzugriffsrecht für die Add-In-Website, daher müssen nur Berechtigungen für SharePoint-Ressourcen in der Hostwebsite oder Positionen außerhalb der Add-In-Website angefordert werden.)</span><span class="sxs-lookup"><span data-stu-id="846e8-p114">You must request, in the add-in manifest file, the permissions that an add-in needs to run. The user who adds the add-in must grant these requests, and the user can only grant permissions that he or she has as a user. The grant must be for all the requested permissions or none of them to simplify the management of permissions for users and developers. (The add-in principal always has full control rights to the add-in web, so it only needs to request permissions to SharePoint resources in the host web or other locations outside the add-in web.)</span></span>
 

 
<span data-ttu-id="846e8-170">Weitere Informationen über Add-In-Berechtigungen finden Sie unter [Add-In-Berechtigungen in SharePoint](add-in-permissions-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="846e8-170">For more information about add-in permissions, see  [Add-in permissions in SharePoint](add-in-permissions-in-sharepoint.md).</span></span>
 

 

### <a name="selective-delegation-and-authorization"></a><span data-ttu-id="846e8-171">Selektive Delegierung und Autorisierung</span><span class="sxs-lookup"><span data-stu-id="846e8-171">Selective delegation and authorization</span></span>
<span data-ttu-id="846e8-172"><a name="SelectiveAuthorization"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-172"><a name="SelectiveAuthorization"> </a></span></span>

<span data-ttu-id="846e8-p115">Weder Benutzer, die ein Add-In starten, noch Ressourcenbesitzer, die einem Add-In Zugriffsrechte für eine Ressource erteilen, benötigen für das Add-In Anmeldeinformationen oder ein Kennwort. Stattdessen ermöglicht SharePoint Benutzern und Ressourcenbesitzern, nur die spezifischen Berechtigungen zu erteilen, welche das Add-In anfordert. Möglich wird dies, weil SharePoint das Transaktionsprotokoll  [OAuth 2.0](http://tools.ietf.org/html/draft-ietf-oauth-v2-22) verwendet. Weitere Informationen über OAuth in SharePoint finden Sie unter [OAuth-Ablauf mit Kontexttoken für Add-Ins in SharePoint](context-token-oauth-flow-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="846e8-p115">Neither users who are launching an add-in, nor resource owners who are granting an add-in permission to access a resource, need to provide the add-in their credentials or password. Instead, SharePoint enables users and resource owners to grant only the specific permissions that the add-in requests. What makes this possible is the use by SharePoint of the transaction protocol  [OAuth 2.0](http://tools.ietf.org/html/draft-ietf-oauth-v2-22). For more information about OAuth in SharePoint, see  [Context Token OAuth flow for SharePoint Add-ins](context-token-oauth-flow-for-sharepoint-add-ins.md).</span></span>
 

 

### <a name="cross-domain-access"></a><span data-ttu-id="846e8-177">Domainübergreifender Zugriff</span><span class="sxs-lookup"><span data-stu-id="846e8-177">Cross-domain access</span></span>
<span data-ttu-id="846e8-178"><a name="SelectiveAuthorization"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-178"><a name="SelectiveAuthorization"> </a></span></span>

<span data-ttu-id="846e8-p116">Ein SharePoint-Add-In, das eine Remote-Webanwendung umfasst, welche JavaScript für seine Datenzugriffslogik verwendet, kann eine domänenübergreifende JavaScript-Bibliothek nutzen, um autorisierten Zugriff auf SharePoint-Daten innerhalb der Mandanteneinheit zu erhalten, in der das Add-In installiert ist. Weitere Informationen finden Sie unter  [Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md).</span><span class="sxs-lookup"><span data-stu-id="846e8-p116">A SharePoint Add-in that includes a remote web application that uses JavaScript for its data access logic can use a JavaScript cross domain library to get authorized access to SharePoint data within the tenancy where the add-in is installed. For more information, see  [Access SharePoint data from add-ins using the cross-domain library](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md).</span></span>
 

 

## <a name="add-in-lifecycle"></a><span data-ttu-id="846e8-181">Add-In-Lebenszyklus</span><span class="sxs-lookup"><span data-stu-id="846e8-181">Add-in lifecycle</span></span>
<span data-ttu-id="846e8-182"><a name="SPAppModelArch_Lifecycle"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-182"><a name="SPAppModelArch_Lifecycle"> </a></span></span>

<span data-ttu-id="846e8-p117">Der Lebenszyklus eines SharePoint-Add-In umfasst die Schritte der Veröffentlichung, Installation, Aktualisierung und Deinstallation. Weitere Informationen über diese Themen finden Sie unter  [Veröffentlichen von SharePoint-Add-Ins](publish-sharepoint-add-ins.md),  [Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](deploying-and-installing-sharepoint-add-ins-methods-and-options.md) und [Aktualisierungsverfahren für Add-Ins für SharePoint](sharepoint-add-ins-update-process.md). Beachten Sie außerdem, dass es einen Mechanismus gibt, der Mandantenadministratoren die Stapelinstallation eines SharePoint-Add-In für mehrere Websites ermöglicht. Weitere Informationen finden Sie unter  [Mandantschaften und Bereitstellungsbereiche von Add-Ins für SharePoint](tenancies-and-deployment-scopes-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="846e8-p117">The lifecycle for a SharePoint Add-in includes publishing, installing, upgrading, and uninstalling. For more information about these subjects, see  [Publish SharePoint Add-ins](publish-sharepoint-add-ins.md),  [Deploying and installing SharePoint Add-ins: methods and options](deploying-and-installing-sharepoint-add-ins-methods-and-options.md) and [SharePoint Add-ins update process](sharepoint-add-ins-update-process.md). Note also that there is a mechanism by which tenant administrators can batch install a SharePoint Add-in to multiple websites. For more information, see  [Tenancies and deployment scopes for SharePoint Add-ins](tenancies-and-deployment-scopes-for-sharepoint-add-ins.md).</span></span>
 

 

## <a name="data-storage-in-sharepoint-add-ins"></a><span data-ttu-id="846e8-187">Datenspeicheroptionen in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="846e8-187">Data storage in SharePoint Add-ins</span></span>
<span data-ttu-id="846e8-188"><a name="Data"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-188"><a name="Data"> </a></span></span>

<span data-ttu-id="846e8-p118">SharePoint-Add-Ins können alle möglichen Arten von Daten erstellen oder darauf zugreifen, darunter strukturierte Daten, Dokumente, und Multimedia-Dateien. Diese Daten können in SharePoint oder einem externen Speicherort gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="846e8-p118">SharePoint Add-ins can create and access any kind of data, including structured data, documents, and multimedia files. This data can be stored in SharePoint or in an external location.</span></span> 
 

 

### <a name="structured-data-storage-options"></a><span data-ttu-id="846e8-191">Optionen zum Speichern von strukturierten Daten</span><span class="sxs-lookup"><span data-stu-id="846e8-191">Structured data storage options</span></span>
<span data-ttu-id="846e8-192"><a name="StructuredData"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-192"><a name="StructuredData"> </a></span></span>

<span data-ttu-id="846e8-p119">Ein SharePoint-Add-In kann nahezu jede Art von strukturiertem Datenspeicher verwenden, in und außerhalb von SharePoint und auf Microsoft- und nicht-Microsoft-Plattformen. Im folgenden finden Sie  *some*  -Speicherorte, an denen Sie strukturierte Daten für ein SharePoint-Add-In speichern können:</span><span class="sxs-lookup"><span data-stu-id="846e8-p119">A SharePoint Add-in can use almost any kind of structured data storage, both inside and out of SharePoint and on Microsoft and non-Microsoft platforms. The following are  *some*  locations where you can store structured data for a SharePoint Add-in:</span></span>
 

 

- <span data-ttu-id="846e8-195">SharePoint-Listen in einem Add-In-Web</span><span class="sxs-lookup"><span data-stu-id="846e8-195">SharePoint lists in an add-in web</span></span>
    
 
- <span data-ttu-id="846e8-196">SQL Azure</span><span class="sxs-lookup"><span data-stu-id="846e8-196">SQL Azure</span></span>
    
 
- <span data-ttu-id="846e8-197">Externe mit SharePoint über Microsoft Business Connectivity Services (BCS) verbundene Datenquellen</span><span class="sxs-lookup"><span data-stu-id="846e8-197">External data sources connected to SharePoint with Microsoft Business Connectivity Services (BCS)</span></span>
    
 
- <span data-ttu-id="846e8-198">Ein nicht-Microsoft-Clouddienst</span><span class="sxs-lookup"><span data-stu-id="846e8-198">A non-Microsoft cloud service</span></span>
    
 
- <span data-ttu-id="846e8-199">Eine Datenbank auf Ihrem eigenen Server</span><span class="sxs-lookup"><span data-stu-id="846e8-199">A database on your own server</span></span>
    
 

 <span data-ttu-id="846e8-p120">**Tipp** Zu einem bestimmten Zeitpunkt werden Sie Ihr SharePoint-Add-In aktualisieren. Wenn ein SharePoint-Add-In SharePoint-Komponenten in einem Add-In-Web umfasst, erstellt der Upgradeprozess eine vollständige Kopie des Add-In-Webs. Deshalb ist der Upgradeprozess durch die großen SharePoint-Listen im Add-In-Web sehr zeitaufwendig und prozessorintensiv auf dem Inhaltsdatenbankserver. Sie sollten es also vermeiden, „große Datenmengen“ in SharePoint-Listen im Add-In-Web abzulegen.</span><span class="sxs-lookup"><span data-stu-id="846e8-p120">**Tip**  You will probably upgrade your SharePoint Add-in at some point. When a SharePoint Add-in includes SharePoint components on an add-in web, the upgrade process makes a complete copy of the add-in web. For this reason, very large SharePoint lists on the add-in web make the upgrade process time-consuming and processor intensive on the content database server. You should avoid putting "big data" in SharePoint lists on the add-in web.</span></span>
 


### <a name="unstructured-data-storage-options"></a><span data-ttu-id="846e8-204">Optionen zum Speichern von unstrukturierten Daten</span><span class="sxs-lookup"><span data-stu-id="846e8-204">Unstructured data storage options</span></span>
<span data-ttu-id="846e8-205"><a name="UnStructuredData"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-205"><a name="UnStructuredData"> </a></span></span>

<span data-ttu-id="846e8-p121">Dokumente, Bilder, Videos, Audiodateien und andere Arten von nicht strukturierten Daten, die erzeugt oder von einem SharePoint-Add-In verwendet werden, können in oder außerhalb von SharePoint gespeichert werden. Dokumentbibliotheken sind eine gute Wahl für Dokumente und können über die SharePoint-Suche durchsucht werden. Eine Website-Objektbibliothek ist oftmals eine gute Wahl für Multimediadateien.</span><span class="sxs-lookup"><span data-stu-id="846e8-p121">Documents, images, videos, audio files, and other kinds of unstructured data that is produced or used by a SharePoint Add-in can be stored in or outside SharePoint. Document libraries are a good choice for documents and are searchable via SharePoint search. A site asset library is often a good choice for multimedia files.</span></span> 
 

 
<span data-ttu-id="846e8-p122">Zu den anderen Optionen gehört der BLOB-Speicher in Ihrem Microsoft Azure-Konto oder auf Ihren eigenen Servern. Sie können Dateien auch auf einigen nicht-Microsoft-Plattformen oder in Clouddiensten speichern.</span><span class="sxs-lookup"><span data-stu-id="846e8-p122">Other options include blob storage in your Microsoft Azure account or on your own servers. You can also store files in some non-Microsoft platforms or cloud services.</span></span>
 

 

### <a name="add-in-settings-and-other-metadata-storage-options"></a><span data-ttu-id="846e8-211">Add-In-Einstellungen und andere Speicheroptionen für Metadaten</span><span class="sxs-lookup"><span data-stu-id="846e8-211">Add-in settings and other metadata storage options</span></span>
<span data-ttu-id="846e8-212"><a name="AppMetadata"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-212"><a name="AppMetadata"> </a></span></span>

<span data-ttu-id="846e8-p123">Metadaten für ein SharePoint-Add-In, wie z. B. Benutzereinstellungen, Standortinformatioenn und andere Einstellungen können an verschiedenen Orten gespeichert werden. Eine ausgeblendete SharePoint-Liste ist manchmal eine gute Wahl. Sie können die Eigenschaftensammlung des Add-In-Webs verwenden. Eine andere Option für ein vom Anbieter gehostetes Add-In ist die Verwendung des Microsoft Azure-Tabellenspeichers.</span><span class="sxs-lookup"><span data-stu-id="846e8-p123">Metadata for a SharePoint Add-in, such as user preferences, location information, and other settings can be stored in several places. A hidden SharePoint list is sometimes a good choice. You can also use the property bag of the add-in web. Another option, for a provider-hosted add-in, is to use Microsoft Azure Table storage.</span></span> 
 

 

### <a name="secure-data-access-options"></a><span data-ttu-id="846e8-217">Optionen für den sichere Datenzugriff</span><span class="sxs-lookup"><span data-stu-id="846e8-217">Secure data access options</span></span>
<span data-ttu-id="846e8-218"><a name="DataAccess"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-218"><a name="DataAccess"> </a></span></span>

<span data-ttu-id="846e8-p124">Ihre Optionen für den sicheren Datenzugriff hängen natürlich von der Speicherwahl ab. Der Datenzugriff und die Suche weren detalliert in verschiedenen anderen Artikeln behandelt. Weitere Informationen finden Sie unter  [Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="846e8-p124">Your options for secure data access, of course, depend on your choice of storage. Data access and search are discussed in detail in several other articles. For more information, see  [Secure data access and client object models for SharePoint Add-ins](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md).</span></span>
 

 

## <a name="managing-add-ins"></a><span data-ttu-id="846e8-222">Verwalten von Add-Ins</span><span class="sxs-lookup"><span data-stu-id="846e8-222">Managing add-ins</span></span>
<span data-ttu-id="846e8-223"><a name="SPAppModelArch_Managing"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-223"><a name="SPAppModelArch_Managing"> </a></span></span>

<span data-ttu-id="846e8-p125">Websitesammlungsadministratoren und Mandantenadministratoren können Add-Ins überwachen und die ihnen zugewiesenen Ressourcen ändern. Außerdem können Microsoft-Mitarbeiter des Add-In-Stores Add-Ins mit Flags versehen und sie deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="846e8-p125">Site collection administrators and tenant administrators can monitor add-ins and change the resources allocated to them. In addition, Microsoft personnel for the add-in store can flag add-ins and disable them.</span></span>
 

 
<span data-ttu-id="846e8-226">Weitere Informationen zum Verwalten von Add-Ins finden Sie unter [Installieren und Verwalten von SharePoint-Add-Ins](http://msdn.microsoft.com/en-us/library/733647a3-a5d3-475b-967d-3bb627c2a0c2) auf TechNet.</span><span class="sxs-lookup"><span data-stu-id="846e8-226">For more information about managing add-ins, see  [Install and manage SharePoint Add-ins](http://msdn.microsoft.com/en-us/library/733647a3-a5d3-475b-967d-3bb627c2a0c2) on TechNet.</span></span>
 

 

### <a name="monitoring-add-ins"></a><span data-ttu-id="846e8-227">Überwachen von Add-Ins</span><span class="sxs-lookup"><span data-stu-id="846e8-227">Monitoring add-ins</span></span>
<span data-ttu-id="846e8-228"><a name="SPAppModelArch_Monitoring"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-228"><a name="SPAppModelArch_Monitoring"> </a></span></span>

<span data-ttu-id="846e8-p126">SharePoint bietet Integritätsüberwachung von Add-Ins und macht diese Informationen auf der Benutzeroberfläche für Websitebesitzer, Mandantenadministratoren und Farmadministratoren verfügbar. Die meiste Dokumentation für das Überwachungssystem befindet sich auf TechNet, z. B.  [Überwachen von Add-Ins für SharePoint](http://technet.microsoft.com/library/3adafdd2-f276-4a9d-8a74-e06b8916bbc2). Dieser Abschnitt ist nur eine kurze Einführung, um zu erläutern, wie Add-Ins, die Sie verkaufen, überwacht werden.</span><span class="sxs-lookup"><span data-stu-id="846e8-p126">SharePoint provides health monitoring of add-ins and makes this information available in the UI to website owners, tenant administrators, and farm administrators. Most documentation for the monitoring system is on TechNet; for example  [Monitor SharePoint Add-ins](http://technet.microsoft.com/library/3adafdd2-f276-4a9d-8a74-e06b8916bbc2). This section is just a quick introduction to explain how add-ins that you sell are monitored.</span></span>
 

 
<span data-ttu-id="846e8-p127">Einige Arten von Daten werden pro App gemeldet, andere dagegen pro App-Instanz. Folgendes sind die primären Elemente, die das Überwachungs-Framework meldet:</span><span class="sxs-lookup"><span data-stu-id="846e8-p127">Some kinds of data are reported per-app and other kinds are reported per-app-instance. The primary items that the monitoring framework reports are as follows:</span></span>
 

 

- <span data-ttu-id="846e8-233">Verwendung des Add-Ins, z. B. wie oft es installiert wurde (Erstellen einer neuen Instanz).</span><span class="sxs-lookup"><span data-stu-id="846e8-233">Use of the add-in, such as the number of times it has been installed (creating a new instance).</span></span> 
    
 
- <span data-ttu-id="846e8-234">Serverressourcenverbrauch jeder Add-In-Instanz.</span><span class="sxs-lookup"><span data-stu-id="846e8-234">Server resource consumption of each add-in instance.</span></span>
    
 
- <span data-ttu-id="846e8-235">Installations-, Aktualisierungs- und Laufzeitfehler jeder Add-In-Instanz.</span><span class="sxs-lookup"><span data-stu-id="846e8-235">Installation, upgrade, and run-time errors of each add-in instance.</span></span>
    
 
- <span data-ttu-id="846e8-236">Ein Hinweis auf die Gesamtintegrität jeder Add-In-Instanz durch grüne, gelbe und rote Farbanzeige.</span><span class="sxs-lookup"><span data-stu-id="846e8-236">An overall health indicator for each add-in instance of green, yellow, and red.</span></span>
    
 
<span data-ttu-id="846e8-p128">Wenn das Add-In Azure-Website-Komponenten umfasst, fragt das Überwachungs-Framework außerdem Microsoft Azure stündlich nach Fehlerdaten ab und meldet kritische Fehler und Speicherkontingentdaten auf der SharePoint-Benutzeroberfläche. Microsoft Azure SQL-Datenbank-Fehler werden nicht gemeldet.</span><span class="sxs-lookup"><span data-stu-id="846e8-p128">If the add-in includes Azure Web Site components, the monitoring framework also polls Microsoft Azure hourly for its error data and reports critical errors and storage quota data in the SharePoint UI. Microsoft Azure SQL Database errors are not reported.</span></span>
 

 
<span data-ttu-id="846e8-239">Mit den durch das Überwachungs-Framework bereitgestellten Informationen können Administratoren bestimmen, ob ihr Budget zum Kauf von Add-Ins klug verwendet wird, ob sie weitere Ressourcen für Add-Ins bereitstellen müssen, und ob sie ein nicht einwandfrei funktionierendes Add-In deaktivieren sollten.</span><span class="sxs-lookup"><span data-stu-id="846e8-239">The information that is provided by the monitoring framework enables administrators to determine whether their add-in purchase budget is being wisely spent, whether they have to deploy more resources to add-ins, and whether they have to disable an add-in that is not working correctly.</span></span>
 

 

## <a name="registering-add-in-dependencies"></a><span data-ttu-id="846e8-240">Registrieren von Add-In-Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="846e8-240">Registering add-in dependencies</span></span>
<span data-ttu-id="846e8-241"><a name="RegisterDependency"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-241"><a name="RegisterDependency"> </a></span></span>

<span data-ttu-id="846e8-p129">Wenn Ihr SharePoint-Add-In von einer SharePoint-Funktion abhängt, die nicht verfügbar ist und im Add-In-Web nicht verfügbar gemacht werden kann, funktioniert das Add-In nicht richtig, was zu Beschwerden von Seiten der Kunden führen kann. Sie können sicherstellen, dass das Add-In nicht installiert wird, wenn die erforderlichen Dienste und Features nicht verfügbar sind: Registrieren Sie hierzu die Abhängigkeiten des Add-Ins im Add-In-Manifest. Die Installationsinfrastruktur für SharePoint-Add-Ins sucht nach diesen Voraussetzungen und verhindert die Installation des Add-Ins, wenn eine davon nicht erfüllt wird.</span><span class="sxs-lookup"><span data-stu-id="846e8-p129">If your SharePoint Add-in depends on a SharePoint capability that is not available and cannot be made available on the add-in web, then it will not work properly and your customers will complain. You can ensure that your add-in is not installed where the requisite services and Features are not available by registering the dependencies of the add-in in add-in manifest. The installation infrastructure for SharePoint Add-ins will check for these prerequisites and it will block installation of you add-in if any of them is not available.</span></span>
 

 
<span data-ttu-id="846e8-245">Bei Diensten wie Excel, Access oder Visio prüft die Infrastruktur, ob der Dienst installiert und lizenziert ist.</span><span class="sxs-lookup"><span data-stu-id="846e8-245">For services, such as Excel, Access, or Visio services, the infrastructure will verify that the service is installed and licensed.</span></span>
 

 
<span data-ttu-id="846e8-246">Für Features wie die Aufgabenliste überprüft die Infrastruktur, dass das Feature bereitgestellt und dass es:</span><span class="sxs-lookup"><span data-stu-id="846e8-246">For Features, such as a Task list, the infrastructure will verify that the Feature is deployed and either:</span></span>
 

 
<span data-ttu-id="846e8-247">im **Farm**-, **WebApplication**- oder **Site**-Bereich (Websitesammlung) aktiviert ist,</span><span class="sxs-lookup"><span data-stu-id="846e8-247">-- activated at the  **Farm**,  **WebApplication**, or  **Site** (site collection) scope</span></span>
 

 
<span data-ttu-id="846e8-248">oder</span><span class="sxs-lookup"><span data-stu-id="846e8-248">or</span></span>
 

 
<span data-ttu-id="846e8-249">(mit dem **Web**-Bereich) im Add-In-Web aktivierbar ist, das beim Installieren des Add-Ins erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="846e8-249">-- activatible, with  **Web** scope, on the add-in web that is created when the add-in is installed.</span></span>
 

 

 <span data-ttu-id="846e8-250">**Hinweis** Die Add-In-Installationsinfrastruktur aktiviert diese Features im Add-In-Web automatisch, wenn es erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="846e8-250">**Note**  The add-in installation infrastructure will automatically activate such Features on the add-in web when it is created.</span></span>
 

<span data-ttu-id="846e8-251">Die folgenden Abschnitte enthalten die Details, die Sie benötigen, um die erforderlichen Komponenten registrieren zu können.</span><span class="sxs-lookup"><span data-stu-id="846e8-251">The following sections provide the details you need to register your prerequisites.</span></span>
 

 

### <a name="implicitly-register-dependencies-with-permission-requests"></a><span data-ttu-id="846e8-252">Impliziertes Registrieren von Abhängigkeiten mit Berechtigungsanforderungen</span><span class="sxs-lookup"><span data-stu-id="846e8-252">Implicitly register dependencies with permission requests</span></span>
<span data-ttu-id="846e8-253"><a name="PermAsPreq"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-253"><a name="PermAsPreq"> </a></span></span>

<span data-ttu-id="846e8-p130">Wenn Ihr Add-In Zugriff auf SharePoint-Komponenten außerhalb des Add-In-Webs benötigt, muss es die Berechtigung für diese Ressourcen im Abschnitt **AppPermissionRequests** des Add-In-Manifests anfordern. Diese Berechtigungsanforderungen dienen auch als Voraussetzungsregistrierungen, da SharePoint aus den von Ihrem Add-In angeforderten Berechtigungen ableitet, dass für das Add-In bestimmte SharePoint-Funktionen verfügbar sein müssen. In vielen Fällen kann SharePoint alle vom Add-In benötigten Funktionen ableiten, sodass Sie die verbleibenden Abschnitte dieses Themas nicht benötigen. Redundante Abhängigkeitsregistrierungen haben jedoch keine negativen Auswirkungen.</span><span class="sxs-lookup"><span data-stu-id="846e8-p130">When your add-in needs access to SharePoint components outside of the add-in web, it must request permission for these resources in the  **AppPermissionRequests** section of the add-in manifest. These permission requests also serve as prerequisite registrations because SharePoint will infer from the permissions that your add-in requests that it the add-in needs certain SharePoint capabilities to be available. In many situations, SharePoint can infer all the capabilities that your add-in needs and the remaining sections of this topic are not needed. However, redundant dependency registrations are not harmful.</span></span>
 

 

### <a name="explicitly-register-dependencies-with-appprerequisites"></a><span data-ttu-id="846e8-258">Explizites Registrieren von Abhängigkeiten mit AppPrerequisites</span><span class="sxs-lookup"><span data-stu-id="846e8-258">Explicitly register dependencies with AppPrerequisites</span></span>
<span data-ttu-id="846e8-259"><a name="Explicit"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-259"><a name="Explicit"> </a></span></span>

<span data-ttu-id="846e8-p131">Falls Ihr Add-In über eine Abhängigkeit verfügt, die nicht anhand ihrer Berechtigungsanforderungen impliziert wird, können Sie jede Abhängigkeit mit einem **AppPrerequisite**-Element im Add-In-Manifest registrieren. Dieses Element umfasst drei Attribute: **Type**, **ID** und (optional) **MinimumVersion**.</span><span class="sxs-lookup"><span data-stu-id="846e8-p131">When your add-in has a dependency that is not implied by its permission requests, you register each dependency with an  **AppPrerequisite** element in the add-in manifest. There are three attributes in this element; **Type**,  **ID**, and (optionally)  **MinimumVersion**.</span></span> 
 

 
<span data-ttu-id="846e8-p132">Es gibt drei mögliche Voraussetzungswerte für **Type**, `Feature`, `Capablility` und `AutoProvisioning`. Eine Featurevoraussetzung ist lediglich ein SharePoint-Feature, das im Add-In-Web oder in einem größeren Kontext, dessen Teil das Add-In-Web ist, bereitgestellt und aktiviert werden muss. Bei einer Funktion handelt es sich um eine Gruppe verwandter Features und Dienste, die im Add-In-Web verfügbar sein müssen. ( `AutoProvisioning` wird im nächsten Abschnitt behandelt.)</span><span class="sxs-lookup"><span data-stu-id="846e8-p132">There are three possible prerequisite values for  **Type**;  `Feature`,  `Capablility`, and  `AutoProvisioning`. A Feature prerequisite is simply a SharePoint Feature that must be deployed and activated on the add-in web or a broader scope that includes the add-in web. A capability is a set of related Features and services that must be available on the add-in web. ( `AutoProvisioning` is discussed in the next section.)</span></span>
 

 
<span data-ttu-id="846e8-p133">Mit dem optionalen **MinimumVersion**-Attribut wird die niedrigste Version des für das Add-In erforderlichen Features bzw. der Funktion angegeben. Die Attributwerte haben das Format „n.n.n.n“; z. B.  `15.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="846e8-p133">The optional  **MinimumVersion** specifies the lowest version of the Feature or capability that your add-in requires. The attribute values are of the form n.n.n.n; for example `15.0.0.0`.</span></span>
 

 
<span data-ttu-id="846e8-p134">Mit der **ID** wird angegeben, welches Feature oder welche Funktion erforderlich ist. Wenn **Type** auf `Feature` festgelegt ist, ist die **ID** die in Klammern gesetzte und mit Bindestrichen verbundene GUID des Features, z. B. `{151D22D9-95A8-4904-A0A3-22E4DB85D1E0}`. Wenn **Type** auf `Capability` festgelegt ist, entspricht die **ID** der GUID der Funktion. Die Funktionen sind weiter unten aufgelistet. Informationen für die Suche nach der GUID einer Funktion finden Sie unter [AppPrerequisite-Element (AppPrerequisiteCollection complexType) (SharePoint-Add-In-Manifest)](http://msdn.microsoft.com/library/791be402-981f-519e-fcde-f24cc3cb4139%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="846e8-p134">The  **ID** specifies which Feature or capability is required. If **Type** is `Feature`, the  **ID** is the bracketed, hyphenated GUID of the Feature; for example `{151D22D9-95A8-4904-A0A3-22E4DB85D1E0}`. If  **Type** is `Capability`, the  **ID** is the GUID of the capability. The capabilities are listed below. To get the find the GUID of a capability see [AppPrerequisite element (AppPrerequisiteCollection complexType) (SharePoint Add-in Manifest)](http://msdn.microsoft.com/library/791be402-981f-519e-fcde-f24cc3cb4139%28Office.15%29.aspx).</span></span>
 

 

- <span data-ttu-id="846e8-273">Access Services 2010</span><span class="sxs-lookup"><span data-stu-id="846e8-273">Access Services 2010</span></span>
    
 
- <span data-ttu-id="846e8-274">Access Services</span><span class="sxs-lookup"><span data-stu-id="846e8-274">Access Services</span></span>
    
 
- <span data-ttu-id="846e8-275">Verwalteter Metadatenwebdienst</span><span class="sxs-lookup"><span data-stu-id="846e8-275">Managed Metadata Web Service</span></span>
    
 
- <span data-ttu-id="846e8-276">PowerPoint Services</span><span class="sxs-lookup"><span data-stu-id="846e8-276">PowerPoint Services</span></span>
    
 
- <span data-ttu-id="846e8-277">Secure Store Services</span><span class="sxs-lookup"><span data-stu-id="846e8-277">Secure Store Services</span></span>
    
 
- <span data-ttu-id="846e8-278">Maschineller Übersetzungsdienst</span><span class="sxs-lookup"><span data-stu-id="846e8-278">Machine Translation Service</span></span>
    
 
- <span data-ttu-id="846e8-279">Benutzerprofildienst</span><span class="sxs-lookup"><span data-stu-id="846e8-279">User Profile Service</span></span>
    
 
- <span data-ttu-id="846e8-280">Visio-Grafikdienst</span><span class="sxs-lookup"><span data-stu-id="846e8-280">Visio Graphics Service</span></span>
    
 
- <span data-ttu-id="846e8-281">Arbeitsverwaltungsdienst</span><span class="sxs-lookup"><span data-stu-id="846e8-281">Work Management Service</span></span>
    
 
- <span data-ttu-id="846e8-282">Duet</span><span class="sxs-lookup"><span data-stu-id="846e8-282">Duet</span></span>
    
 
- <span data-ttu-id="846e8-283">Workflow</span><span class="sxs-lookup"><span data-stu-id="846e8-283">Workflow</span></span>
    
 
- <span data-ttu-id="846e8-284">Suche</span><span class="sxs-lookup"><span data-stu-id="846e8-284">Search</span></span>
    
 
- <span data-ttu-id="846e8-285">EDU</span><span class="sxs-lookup"><span data-stu-id="846e8-285">EDU</span></span>
    
 
<span data-ttu-id="846e8-p135">Dies ist ein Beispiel für eine Rohversion des **AppPrerequisites**-Markups, mit dem die Workflow-Funktion registriert wird. Wenn Sie Visual Studio verwenden, bearbeiten Sie das Add-In-Manifest in einem Designertool.</span><span class="sxs-lookup"><span data-stu-id="846e8-p135">The following is an example of raw  **AppPrerequisites** markup that registers the Workflow capability. If you are using Visual Studio, you edit the add-in manifest in a designer tool.</span></span>
 

 



```
<AppPrerequisites>
  <AppPrerequisite Type="Capability" ID="{CDD8F991-B459-4512-8048-03D5A03FF27E}" MinimumVersion="15.0.0.0" />
</ AppPrerequisites>
```


## <a name="in-this-section"></a><span data-ttu-id="846e8-288">Inhalt dieses Abschnitts</span><span class="sxs-lookup"><span data-stu-id="846e8-288">In this section</span></span>
<span data-ttu-id="846e8-289"><a name="RegisterDependency"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-289"><a name="RegisterDependency"> </a></span></span>


-  [<span data-ttu-id="846e8-290">Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="846e8-290">Choose patterns for developing and hosting your SharePoint Add-in</span></span>](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="846e8-291">Hostwebs, Add-In-Webs und SharePoint-Komponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="846e8-291">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)
    
 

## <a name="additional-resources"></a><span data-ttu-id="846e8-292">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="846e8-292">Additional resources</span></span>
<span data-ttu-id="846e8-293"><a name="SPAppModelArch_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="846e8-293"><a name="SPAppModelArch_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="846e8-294">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="846e8-294">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="846e8-295">SharePoint-Add-Ins im Vergleich zu SharePoint-Lösungen</span><span class="sxs-lookup"><span data-stu-id="846e8-295">SharePoint Add-ins compared with SharePoint solutions</span></span>](http://msdn.microsoft.com/library/0e9efadb-aaf2-4c0d-afd5-d6cf25c4e7a8%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="846e8-296">Add-In-Berechtigungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="846e8-296">Add-in permissions in SharePoint</span></span>](add-in-permissions-in-sharepoint.md)
    
 
-  [<span data-ttu-id="846e8-297">OAuth-Ablauf mit Kontexttoken für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="846e8-297">Context Token OAuth flow for SharePoint Add-ins</span></span>](context-token-oauth-flow-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="846e8-298">UX-Design für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="846e8-298">UX design for SharePoint Add-ins</span></span>](ux-design-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="846e8-299">IFrame</span><span class="sxs-lookup"><span data-stu-id="846e8-299">IFrame</span></span>](http://www.w3schools.com/tags/tag_iframe.asp)
    
 
-  [<span data-ttu-id="846e8-300">Hinweise zur App-Manifeststruktur und zum Paket eines SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="846e8-300">Explore the app manifest structure and the package of a SharePoint Add-in</span></span>](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="846e8-301">Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen</span><span class="sxs-lookup"><span data-stu-id="846e8-301">Deploying and installing SharePoint Add-ins: methods and options</span></span>](deploying-and-installing-sharepoint-add-ins-methods-and-options.md)
    
 
-  <span data-ttu-id="846e8-302">[Aktualisierungsverfahren für SharePoint-Add-Ins](sharepoint-add-ins-update-process.md)</span><span class="sxs-lookup"><span data-stu-id="846e8-302">[SharePoint Add-ins update process](sharepoint-add-ins-update-process.md).</span></span>
    
 
-  [<span data-ttu-id="846e8-303">Mandantschaften und Bereitstellungsbereiche von SharePoint- Add-Ins</span><span class="sxs-lookup"><span data-stu-id="846e8-303">Tenancies and deployment scopes for SharePoint Add-ins</span></span>](tenancies-and-deployment-scopes-for-sharepoint-add-ins.md)
    
 

