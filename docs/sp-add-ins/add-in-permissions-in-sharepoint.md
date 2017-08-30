# <a name="add-in-permissions-in-sharepoint"></a><span data-ttu-id="cfd15-101">Add-In-Berechtigungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="cfd15-101">Add-in permissions in SharePoint</span></span>
<span data-ttu-id="cfd15-p101">Dieser Artikel enthält Informationen zu Add-In-Berechtigungen in SharePoint, zu Typen von Add-In-Berechtigungen, Berechtigungsanforderungsbereichen und der Verwaltung von Berechtigungen. Zudem werden in diesem Artikel die Unterschiede zwischen Add-In-Berechtigungsrechten, Benutzerrechten und Office Store-App-Rechten besprochen.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p101">Learn about add-in permissions in spnv, including types of add-in permissions, permission request scopes, and managing permissions. This article also discusses the differences in add-in permission rights, user rights, and spstore app rights.</span></span>
 

 <span data-ttu-id="cfd15-p102">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="cfd15-p102">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="cfd15-107">Sie sollten sich zuerst mit dem Thema [Autorisierung und Authentifizierung für Add-Ins in SharePoint 2013](authorization-and-authentication-of-sharepoint-add-ins) vertraut machen, bevor Sie diesen Artikel lesen.</span><span class="sxs-lookup"><span data-stu-id="cfd15-107">You should first be familiar with the topic [Authorization and authentication for add-ins in SharePoint 2013](authorization-and-authentication-of-sharepoint-add-ins) before you read this article.</span></span> 

## <a name="get-an-overview-of-add-in-permissions-in-sharepoint"></a><span data-ttu-id="cfd15-108">Übersicht über Add-In-Berechtigungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="cfd15-108">Get an overview of add-in permissions in SharePoint</span></span>
<span data-ttu-id="cfd15-109"><a name="Perm_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="cfd15-109"></span></span>

<span data-ttu-id="cfd15-p103">Ein SharePoint-Add-In fordert die Berechtigungen, die es benötigt, während der Installation von dem installierenden Benutzer an. Der Entwickler eines Add-Ins muss über die Add-In-Manifestdatei die Berechtigungen anfordern, die das bestimmte Add-In benötigt, um ausgeführt werden zu können. (Geräte- und Web-Apps, die auf SharePoint zugreifen, aber nicht auf SharePoint-Websites installiert werden, müssen während der Laufzeit Berechtigungen von dem Benutzer gewährt werden, der das Add-In ausführt. Weitere Informationen finden Sie unter  [Übersicht über Add-Ins, die dynamisch Zugriffsberechtigungen von SharePoint anfordern](authorization-code-oauth-flow-for-sharepoint-add-ins#Overview).) Benutzer können nur die Berechtigungen gewähren, über die sie selbst verfügen. Der Benutzer muss entweder alle Berechtigungen gewähren, die ein Add-In anfordert, oder keine Berechtigungen gewähren. Eine selektive Gewährung von Berechtigungen ist nicht möglich. (Bei Add-Ins, die dynamisch Berechtigungen anfordern, kann nur ein Benutzer mit Verwaltungsberechtigungen für die SharePoint-Ressourcen, auf die das Add-In zugreifen möchte, das Add-In ausführen, selbst wenn das Add-In geringere Berechtigungen wie beispielsweise eine Leseberechtigung anfragt.)</span><span class="sxs-lookup"><span data-stu-id="cfd15-p103">a SharePoint Add-in requests the permissions that it needs during installation from the user who is installing it. The developer of an add-in must request, through the add-in manifest file, the permissions that the particular add-in needs to be able to run. (Device and web apps that access SharePoint, but are not installed to SharePoint websites must be granted permissions at runtime by the user who is executing the add-in. For more information, see  [Get an overview of add-ins that request access permission from SharePoint on the fly](authorization-code-oauth-flow-for-sharepoint-add-ins#Overview).) Users can grant only the permissions that they have. The user must grant all the permissions that an add-in requests or not grant any permission. Selective grants are not possible. (For add-ins that request permissions on the fly, only a user with Manage permissions to the SharePoint resources that the add-in seeks to access can run the add-in, even if the add-in is asking only for lesser permissions, such as Read.)</span></span>
 

 
<span data-ttu-id="cfd15-p104">Die Berechtigungen, die der App gewährt wurden, werden außerdem in der Inhaltsdatenbank der SharePoint-Farm oder der SharePoint Online-Mandantschaft gespeichert. Sie werden nicht mit einem sicheren Tokendienst wie Microsoft Azure Access Control Service (ACS) gespeichert. Wenn ein Benutzer einer App erstmals Berechtigungen gewährt, ruft SharePoint Informationen zu der von ACS ab. SharePoint speichert dann die grundlegenden Informationen zur App zusammen mit den Berechtigungen der App im App-Verwaltungsdienst und der Inhaltsdatenbank. Weitere Informationen zu ACS finden Sie unter  [Erstellen von SharePoint-Add-Ins, die die Autorisierung mit niedriger Vertrauensebene verwenden](creating-sharepoint-add-ins-that-use-low-trust-authorization).</span><span class="sxs-lookup"><span data-stu-id="cfd15-p104">The permissions that the add-in has been granted are also stored in the content database of the SharePoint farm or SharePoint Online tenancy. They are not stored with a secure token service, such as Microsoft Azure Access Control Service (ACS). When a user first grants an add-in permissions, SharePoint obtains information about the add-in from ACS. SharePoint then stores the basic information about the add-in in the add-in management service and the content database along with the add-in's permissions. For more information about ACS, see  [Creating SharePoint Add-ins that use low-trust authorization](creating-sharepoint-add-ins-that-use-low-trust-authorization).</span></span>
 

 
<span data-ttu-id="cfd15-p105">Wenn ein Objekt, für das der App Berechtigungen gewährt wurden, gelöscht wird, werden auch die zugehörigen Berechtigungen gelöscht. Wenn ein Objekt, für das der App Berechtigungen gewährt wurden, recycelt wird, dann ändert SharePoint die zugehörigen Berechtigungen nicht, damit die Berechtigungen noch intakt sind, wenn das Objekt aus dem Papierkorb wiederhergestellt wird. .</span><span class="sxs-lookup"><span data-stu-id="cfd15-p105">If an object to which an add-in was granted permission is deleted, the corresponding grants are deleted also. When an object to which an add-in was granted permission is recycled, SharePoint does not modify the corresponding grant. This is so that if the object is restored from the Recycle Bin, the grant is still intact.</span></span>
 

 
<span data-ttu-id="cfd15-p106">Wenn eine App entfernt wird, dann werden alle Berechtigungen widerrufen, die dieser App in dem Bereich, aus dem sie entfernt wird, gewährt wurden. Auf diese Weise soll sichergestellt werden, dass die App nicht weiterhin remote auf geschützte SharePoint-Ressourcen zugreifen kann, nachdem ein Benutzer die App aus SharePoint entfernt hat.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p106">When an add-in is removed, all the permissions granted to that add-in at the scope from which it was removed are revoked. This is to ensure that the add-in can't use its credentials to continue accessing protected SharePoint resources remotely after a user removes the add-in from SharePoint.</span></span>
 

 

## <a name="understand-the-types-of-add-in-permissions-and-permission-scopes"></a><span data-ttu-id="cfd15-127">Arten von App-Berechtigungen und Berechtigungsbereichen</span><span class="sxs-lookup"><span data-stu-id="cfd15-127">Understand the types of add-in permissions and permission scopes</span></span>
<span data-ttu-id="cfd15-128"><a name="Perm_types"> </a></span><span class="sxs-lookup"><span data-stu-id="cfd15-128"></span></span>

<span data-ttu-id="cfd15-p107">Ein SharePoint-Add-In gibt mithilfe von Berechtigungsanforderungen die Berechtigungen an, die für sein ordnungsgemäßes Funktionieren erforderlich sind. Die Berechtigungsanforderungen geben sowohl die von einem Add-In benötigten Rechte als auch den Bereich an, in dem die Rechte benötigt werden. Diese Berechtigungen werden als Teil des Add-In-Manifests angefordert.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p107">A SharePoint Add-in uses permission requests to specify the permissions that it needs to function correctly. The permission requests specify both the rights that an add-in needs and the scope at which it needs the rights. These permissions are requested as part of the add-in manifest.</span></span>
 

 

 <span data-ttu-id="cfd15-p108">**Hinweis** Die in diesem Abschnitt beschriebenen Bereiche gelten nur für Listeninhalte und Bibliotheksinhalte. Weitere Informationen zu Bereichen und anderen Features finden Sie unter [Arten von App-Berechtigungen und Berechtigungsbereichen](#Perm_types) in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p108">**Note** The scopes described in this section apply to list content and library content only. For information about scopes for other features, see the  [Understand the types of add-in permissions and permission scopes](#Perm_types) section in this article.</span></span>
 

<span data-ttu-id="cfd15-134">Berechtigungsanforderungsbereiche geben die Position in der SharePoint-Hierarchie an, auf die sich eine Berechtigungsanforderung bezieht.</span><span class="sxs-lookup"><span data-stu-id="cfd15-134">Permission request scopes indicate the location in the SharePoint hierarchy where a permission request applies.</span></span>
 

 

 <span data-ttu-id="cfd15-p109">**Hinweis** Ein SharePoint-Add-In besitzt eine eigene Identität und ist ein Sicherheitsprinzipal, der als Add-In-Prinzipal bezeichnet wird. Wie Benutzer und Gruppen hat auch ein Add-In-Prinzipal bestimmte Berechtigungen oder Rechte. Da der Add-In-Prinzipal Vollzugriff auf das Add-In-Web besitzt, muss er nur Berechtigungen zum Zugriff auf die SharePoint -Ressourcen im Hostweb oder auf andere Speicherorte außerhalb des Add-In-Webs anfordern. Weitere Informationen zum Add-In-Web finden Sie unter [Wichtige Aspekte der Architektur und Entwicklungslandschaft von Add-Ins für SharePoint](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape) und [Hostwebsites, Add-In-Websites und SharePoint-Komponenten in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013).</span><span class="sxs-lookup"><span data-stu-id="cfd15-p109">**Note** A SharePoint Add-in has its own identity and is a security principal, called an add-in principal. Like users and groups, an add-in principal has certain permissions or rights. The add-in principal has full control rights to the add-in web so it only needs to request permissions to SharePoint resources in the host web or other locations outside the add-in web. For more information about add-in web, see  [Important aspects of the SharePoint Add-in architecture and development landscape](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape) and [Host webs, add-in webs, and SharePoint components in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013).</span></span>
 

<span data-ttu-id="cfd15-p110">SharePoint unterstützt vier verschiedene Berechtigungsbereiche innerhalb der Inhaltsdatenbank und Mandanteneinheit, die in Tabelle 1 dargestellt werden. Berechtigungsbereiche werden mit URIs, einschließlich "http:"-Präfix, benannt, sind aber keine URLs und enthalten keine Platzhalter. Die Berechtigungsbereich in dieser Tabelle und in diesem Artikel sind Zeichenfolgenliterale.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p110">SharePoint supports four different permission scopes within the content database and tenancy, as shown in Table 1. Permission scopes are named with URIs, including a "http:" prefix, but they are not URLs and they contain no placeholders. The permission scopes in this table and this article are literal strings.</span></span>
 

 

<span data-ttu-id="cfd15-142">**Tabelle 1: URIs des SharePoint-Add-In-Berechtigungsanforderungsbereichs und Beschreibungen**</span><span class="sxs-lookup"><span data-stu-id="cfd15-142">**Table 1. SharePoint add-in permission request scope URIs and descriptions**</span></span>

|<span data-ttu-id="cfd15-143">**Bereich**</span><span class="sxs-lookup"><span data-stu-id="cfd15-143">**Scope**</span></span>|<span data-ttu-id="cfd15-144">**Bereichs-URI**</span><span class="sxs-lookup"><span data-stu-id="cfd15-144">**Scope URI**</span></span>|<span data-ttu-id="cfd15-145">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="cfd15-145">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="cfd15-146">Mandant</span><span class="sxs-lookup"><span data-stu-id="cfd15-146">tenancy</span></span>| <span data-ttu-id="cfd15-147">http://sharepoint/content/tenant</span><span class="sxs-lookup"><span data-stu-id="cfd15-147">http://sharepoint/content/tenant</span></span>|<span data-ttu-id="cfd15-p111">Der Mandant, in dem das Add-In installiert ist. Enthält alle untergeordneten Elemente dieses Bereichs.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p111">The tenancy where the add-in is installed. Includes all children of this scope.</span></span>|
|<span data-ttu-id="cfd15-150">Websitesammlung</span><span class="sxs-lookup"><span data-stu-id="cfd15-150">Site Collection</span></span>| <span data-ttu-id="cfd15-151">http://sharepoint/content/sitecollection</span><span class="sxs-lookup"><span data-stu-id="cfd15-151">http://sharepoint/content/sitecollection</span></span>|<span data-ttu-id="cfd15-p112">Die Websitesammlung, in der das Add-In installiert ist. Enthält alle untergeordneten Elemente dieses Bereichs.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p112">The site collection where the add-in is installed. Includes all children of this scope.</span></span>|
|<span data-ttu-id="cfd15-154">Website</span><span class="sxs-lookup"><span data-stu-id="cfd15-154">Website</span></span>| <span data-ttu-id="cfd15-155">http://sharepoint/content/sitecollection/web</span><span class="sxs-lookup"><span data-stu-id="cfd15-155">http://sharepoint/content/sitecollection/web</span></span>|<span data-ttu-id="cfd15-p113">Die Website, in der das Add-In installiert ist. Enthält alle untergeordneten Elemente dieses Bereichs.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p113">The website where the add-in is installed. Includes all children of this scope.</span></span>|
|<span data-ttu-id="cfd15-158">Auflisten</span><span class="sxs-lookup"><span data-stu-id="cfd15-158">List</span></span>| <span data-ttu-id="cfd15-159">http://sharepoint/content/sitecollection/web/list</span><span class="sxs-lookup"><span data-stu-id="cfd15-159">http://sharepoint/content/sitecollection/web/list</span></span>|<span data-ttu-id="cfd15-p114">Eine einzelne Liste auf der Website, auf der das Add-In installiert ist. Wenn der Benutzer, der das Add-In installiert, zum Erteilen von Berechtigungen aufgefordert wird, kann der Benutzer im Dialogfeld eine Liste auswählen, für die dem Add-In Berechtigungen erteilt werden. Wenn das Add-In Berechtigungen für mehrere Listen benötigt, muss es die Berechtigung für den Webbereich anfordern. Da Sie als Entwickler außerdem nicht steuern können, welche Liste der Benutzer auswählt, oder dem Benutzer nicht mitteilen können, welche Liste er auswählen soll, müssen Sie den Webbereich verwenden, wenn eine Liste vorhanden ist, für die Ihr Add-In die Berechtigung haben  *muss*  . (Es gibt jedoch eine Möglichkeit, die Auswahl des Benutzers auf bestimmte Untersammlungen von Listen einzuschränken. Weitere Informationen dazu finden Sie unter [Berechtigungsanforderungsbereich mit den zugehörigen Eigenschaften](#AssociatedProperties) weiter unten.) </span><span class="sxs-lookup"><span data-stu-id="cfd15-p114">A single list in the website where the add-in is installed. When the user who installs the add-in is prompted to grant permissions, the dialog enables the user to select one list to which the add-in is granted permissions. If the add-in needs permission to more than one list, it must request permission to web scope. Also, since you, the developer, have no way to control which list the user chooses or to tell the user which one to choose, you must use web scope if there is a list to which your add-in  *must*  have permission. (But there is a way to narrow the user's choice to certain subsets of lists. See [Permission request scope with associated properties](#AssociatedProperties) below.)</span></span>|

<span data-ttu-id="cfd15-p115">Wenn einer App eine Berechtigung für einen der Bereiche gewährt wird, gilt diese Berechtigung für alle untergeordneten Elemente des Bereichs. Wenn einer App beispielsweise Berechtigungen für eine Website gewährt werden, dann erhält die App auch Berechtigungen für alle Listen dieser Website und für alle Listenelemente dieser Listen.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p115">If an add-in is granted permission to one of the scopes, the permission applies to all children of the scope. For example, if an add-in is granted permission to a website, the add-in is also granted permission to each list that is contained in the website, and all list items that are in each list.</span></span>
 

 
<span data-ttu-id="cfd15-p116">Da Berechtigungsanforderungen ohne Informationen zur Topologie der Websitesammlung erfolgen, in der die App installiert ist, wird der Bereich als Typ statt als URL einer bestimmten Instanz ausgedrückt. Diese Bereichstypen werden als URIs angegeben. Auf die SharePoint-Inhaltsdatenbank bezogene Berechtigungen werden unter dem folgenden URI zusammengefasst:  `http://sharepoint/content`.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p116">Because permission requests are made without information about the topology of the site collection where the add-in is installed, the scope is expressed as a type instead of as the URL of a specific instance. These scope types are expressed as URIs. Permissions to resources that are stored in the SharePoint content database are organized under the following URI:  `http://sharepoint/content`.</span></span>
 

 

## <a name="understand-the-differences-between-add-in-permission-rights-and-user-rights"></a><span data-ttu-id="cfd15-171">Verstehen der Unterschiede zwischen App-Berechtigungsrechten und Benutzerrechten</span><span class="sxs-lookup"><span data-stu-id="cfd15-171">Understand the differences between add-in permission rights and user rights</span></span>
<span data-ttu-id="cfd15-172"><a name="Perm_diff"> </a></span><span class="sxs-lookup"><span data-stu-id="cfd15-172"></span></span>

<span data-ttu-id="cfd15-p117">Berechtigungen geben die Aktivitäten an, die eine App im Anforderungsbereich ausführen darf. SharePoint unterstützt vier Berechtigungsstufen in der Inhaltsdatenbank. Für jeden Bereich kann die App über folgende Rechte verfügen:</span><span class="sxs-lookup"><span data-stu-id="cfd15-p117">Permissions indicate the activities that an add-in is permitted to do within the requested scope. SharePoint supports four rights levels in the content database. For each scope, an add-in can have the following rights:</span></span>
 

 

- <span data-ttu-id="cfd15-176">Lesen</span><span class="sxs-lookup"><span data-stu-id="cfd15-176">Read</span></span>
    
 
- <span data-ttu-id="cfd15-177">Schreiben</span><span class="sxs-lookup"><span data-stu-id="cfd15-177">Write</span></span>
    
 
- <span data-ttu-id="cfd15-178">Verwalten</span><span class="sxs-lookup"><span data-stu-id="cfd15-178">Manage</span></span>
    
 
- <span data-ttu-id="cfd15-179">Vollzugriff</span><span class="sxs-lookup"><span data-stu-id="cfd15-179">Full-control</span></span>
    
 

 <span data-ttu-id="cfd15-180">**Hinweis** Weitere Informationen dazu, was die Rechte Read, Write, Manage und FullControl beinhalten finden Sie im Thema zur  [Planung der App-Berechtigungsverwaltung](http://technet.microsoft.com/en-us/library/jj219576%28office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfd15-180">**Note** For more information about what Read, Write, Manage, and FullControl rights include, see  [Plan add-in permissions management](http://technet.microsoft.com/en-us/library/jj219576%28office.15%29.aspx).</span></span>
 


 <span data-ttu-id="cfd15-p118">**Hinweis** Diese Rechte entsprechen den standardmäßigen Benutzerberechtigungsstufen von SharePoint: Leser, Mitwirkender, Designer und Vollzugriff. Weitere Informationen über die Benutzerberechtigungsstufen finden Sie unter [Benutzerberechtigungen und Berechtigungsstufen](http://technet.microsoft.com/en-us/library/cc288074.aspx). Die Berechtigungsnamen der Add-Ins entsprechen nicht den Berechtigungsnamen von SharePoint-Benutzerrollen, um eine Verwechslung auszuschließen. Da sich die Anpassung der Berechtigungen, die mit SharePoint-Benutzerrollen verknüpft sind, nicht auf die Add-In-Berechtigungsanforderungsstufen auswirken, stimmen die Add-In-Rechtenamen nicht mit den entsprechenden SharePoint-Benutzerrollen überein, mit der Ausnahme von „Vollzugriff“, der über die Benutzeroberfläche für die Berechtigungsverwaltung nicht angepasst werden kann.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p118">**Note**  These rights correspond to the default user permission levels of SharePoint: Reader, Contributor, Designer, and Full Control. For more information about user permission levels, see  [User permissions and permission levels](http://technet.microsoft.com/en-us/library/cc288074.aspx).The add-ins rights names do not match SharePoint user roles rights names, to avoid confusion between user roles rights and add-in rights. Because customizing the permissions that are associated with SharePoint user roles does not affect add-in permission request levels, the add-in rights names do not match the corresponding SharePoint user roles, except Full Control, which can't be customized through the permissions management user interface.</span></span>
 

<span data-ttu-id="cfd15-184">Weitere Schritte:</span><span class="sxs-lookup"><span data-stu-id="cfd15-184">In addition:</span></span>
 

 

- <span data-ttu-id="cfd15-185">Nur für den Bereich Search gilt, dass eine App das Query-Recht zum Abfragen haben kann.</span><span class="sxs-lookup"><span data-stu-id="cfd15-185">For Search only, an add-in can have the Query right.</span></span>
    
 
- <span data-ttu-id="cfd15-p119">Bei einigen Microsoft Project Server 2013-Bereichen ist auch das SubmitStatus-Recht oder das Elevate-Recht verfügbar. Bei den meisten Bereichen für Project Server 2013 sind nur die Rechte zum Lesen und Schreiben verfügbar. Weitere Informationen finden Sie im Abschnitt  [Arten von App-Berechtigungen und Berechtigungsbereichen](#Perm_types) in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p119">For some Microsoft Project Server 2013 scopes, there is also the SubmitStatus right or the Elevate right. For most scopes for Project Server 2013, only Read and Write are available. For more information, see the  [Understand the types of add-in permissions and permission scopes](#Perm_types) section in this article.</span></span>
    
 
- <span data-ttu-id="cfd15-189">Für die Taxonomie sind nur Lese- und Schreibberechtigungen verfügbar.</span><span class="sxs-lookup"><span data-stu-id="cfd15-189">For taxonomy, only rights for Read and Write are available.</span></span>
    
 

 <span data-ttu-id="cfd15-p120">**Hinweis** Für Office Store-Apps gelten Beschränkungen hinsichtlich der Typen von Rechten, die ein Add-In anfordern kann. Weitere Informationen finden Sie im Abschnitt  [Arten von App-Berechtigungen und Berechtigungsbereichen](#Perm_types) in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p120">**Note** Office Store apps have some restrictions as to what type of rights an add-in can request. For more information, see the  [Understand the types of add-in permissions and permission scopes](#Perm_types) section in this article.</span></span>
 

<span data-ttu-id="cfd15-p121">Im Gegensatz zu SharePoint-Benutzerrollen sind diese Berechtigungsstufen nicht anpassbar. Damit soll sichergestellt werden, dass die App durch die Gewährung einer Berechtigungsanforderung eine vorhersehbare Gruppe von Funktionen erhält und nicht der Möglichkeit Rechnung tragen muss, unter Umständen weniger als die erwarteten Berechtigungen zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p121">Unlike SharePoint user roles, these rights levels are not customizable. This is to ensure that when an add-in is granted a permission request, the add-in is guaranteed a predictable set of capabilities, and it does not have to account for the possibility of being granted less permission than it expects.</span></span>
 

 
<span data-ttu-id="cfd15-p122">Ein Benutzer kann einer App keine Berechtigungen gewähren, über die er nicht selbst verfügt. Wenn ein Benutzer versucht, eine App zu installieren, die mehr Berechtigungen anfordert, als der Benutzer hat, wird eine Fehlermeldung angezeigt, die den Benutzer darüber informiert, dass er nicht über ausreichende Berechtigungen verfügt, um die Anforderungen der App erfüllen zu können.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p122">A user cannot grant an add-in permissions that the user himself or herself does not have. If a user attempts to install an add-in that requests more permissions than the user has, an error message displays to the user informing them that they don't have sufficient permissions to grant the add-in its request.</span></span>
 

 
<span data-ttu-id="cfd15-p123">Berechtigungen, die SharePoint nicht kennt, werden ignoriert. Das heißt, wenn eine App eine Berechtigung anfordert, die SharePoint nicht erkennt, dann kann die App installiert werden, aber der Benutzer wird nicht aufgefordert, diese Berechtigung zu gewähren, und die App erhält diese Berechtigung nicht.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p123">Permissions that are not known to SharePoint are ignored. This means that, if an add-in requests a permission that SharePoint does not recognize, the add-in can still be installed, but the user is not prompted to grant the permission, and the permission is not granted to the add-in.</span></span>
 

 

## <a name="learn-about-the-available-scopes-and-permissions-and-about-the-restrictions-on-office-store-apps-permissions"></a><span data-ttu-id="cfd15-198">Weitere Informationen zu den verfügbaren Bereichen und Berechtigungen sowie zu Einschränkungen für Office Store-App-Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="cfd15-198">Learn about the available scopes and permissions, and about the restrictions on Office Store apps permissions</span></span>
<span data-ttu-id="cfd15-199"><a name="Perm_rightlist"> </a></span><span class="sxs-lookup"><span data-stu-id="cfd15-199"></span></span>

<span data-ttu-id="cfd15-p124">Verschiedene Bereiche verfügen über verschiedene Rechte, die von einem Add-In angefordert werden können. In diesem Abschnitt werden die Gruppen von Rechten beschrieben, die für die einzelnen Bereiche verfügbar sind. Zudem wird auf die für SharePoint-Add-Ins, die über den Office Store verkauft werden, geltenden Beschränkungen hingewiesen.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p124">Different scopes have different sets of rights that are available for an add-in to request. This section describes the sets of rights that are available for each scope. Also, it highlights the restrictions for SharePoint Add-ins that are sold through the Office Store.</span></span>
 

 

### <a name="office-store-apps-rights"></a><span data-ttu-id="cfd15-203">Rechte von Office Store-Apps</span><span class="sxs-lookup"><span data-stu-id="cfd15-203">Office Store apps' rights</span></span>

<span data-ttu-id="cfd15-p125">Nur die Rechte Lesen, Schreiben und Verwalten sind für Office Store-Apps zulässig. Wenn Sie versuchen, eine App, die FullControl-Rechte benötigt, an den Office Store zu übermitteln, wird die Übermittlung dieser App blockiert. Da sich der Block in der Office Store-Übermittlungspipeline befindet, können Apps, die mehr als Verwaltungsberechtigungen anfordern, dennoch über den Add-In-Katalog bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p125">Only Read, Write, and Manage rights are allowed for Office Store apps. If you try to submit an app to the Office Store that requires FullControl rights, your app is blocked from submission. Because the block is in the Office Store submission pipeline, apps that request more than Manage permissions can still be deployed through the add-in catalog.</span></span>
 

 

### <a name="permission-request-scopes-for-list-content-and-library-content"></a><span data-ttu-id="cfd15-207">Berechtigungsanforderungsbereiche für Listeninhalte und Bibliotheksinhalte</span><span class="sxs-lookup"><span data-stu-id="cfd15-207">Permission request scopes for list content and library content</span></span>
<span data-ttu-id="cfd15-208"><a name="PermissionsForLists"> </a></span><span class="sxs-lookup"><span data-stu-id="cfd15-208"></span></span>

<span data-ttu-id="cfd15-p126">Tabelle 2 enthält den Berechtigungsanforderungsbereich für Listen- und Bibliotheksinhalte. Zudem enthält sie die Rechte, die für die einzelnen Bereichs-URIs angegeben werden können.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p126">Table 2 shows the permission request scope for list and library content. It also lists the rights that can be specified for each scope URI.</span></span>
 

 

 <span data-ttu-id="cfd15-211">**Hinweis** Die in Tabelle 2 angegebenen URIs sind Literalwerte.</span><span class="sxs-lookup"><span data-stu-id="cfd15-211">**Note** The URIs used in Table 2 are literal values.</span></span>
 


<span data-ttu-id="cfd15-212">**Tabelle 2: URIs des SharePoint-Add-In-Berechtigungsbereichs und verfügbare Rechte**</span><span class="sxs-lookup"><span data-stu-id="cfd15-212">**Table 2. SharePoint add-in permission scope URIs and available rights**</span></span>

|<span data-ttu-id="cfd15-213">**Bereichs-URI**</span><span class="sxs-lookup"><span data-stu-id="cfd15-213">**Scope URI**</span></span>|<span data-ttu-id="cfd15-214">**Verfügbare Rechte**</span><span class="sxs-lookup"><span data-stu-id="cfd15-214">**Available Rights**</span></span>|
|:-----|:-----|
|<span data-ttu-id="cfd15-215">http://sharepoint/content/sitecollection</span><span class="sxs-lookup"><span data-stu-id="cfd15-215">http://sharepoint/content/sitecollection</span></span>|<span data-ttu-id="cfd15-216">Read, Write, Manage, FullControl</span><span class="sxs-lookup"><span data-stu-id="cfd15-216">Read, Write, Manage, FullControl</span></span>|
|<span data-ttu-id="cfd15-217">http://sharepoint/content/sitecollection/web</span><span class="sxs-lookup"><span data-stu-id="cfd15-217">http://sharepoint/content/sitecollection/web</span></span>|<span data-ttu-id="cfd15-218">Read, Write, Manage, FullControl</span><span class="sxs-lookup"><span data-stu-id="cfd15-218">Read, Write, Manage, FullControl</span></span>|
|<span data-ttu-id="cfd15-219">http://sharepoint/content/sitecollection/web/list</span><span class="sxs-lookup"><span data-stu-id="cfd15-219">http://sharepoint/content/sitecollection/web/list</span></span>|<span data-ttu-id="cfd15-220">Read, Write, Manage, FullControl</span><span class="sxs-lookup"><span data-stu-id="cfd15-220">Read, Write, Manage, FullControl</span></span>|
|<span data-ttu-id="cfd15-221">http://sharepoint/content/tenant</span><span class="sxs-lookup"><span data-stu-id="cfd15-221">http://sharepoint/content/tenant</span></span>|<span data-ttu-id="cfd15-222">Read, Write, Manage, FullControl</span><span class="sxs-lookup"><span data-stu-id="cfd15-222">Read, Write, Manage, FullControl</span></span>|
<span data-ttu-id="cfd15-p127">Im folgenden Code wird gezeigt, wie Sie Berechtigungsbereiche und Rechte in der Datei AppManifest.xml verwenden. Im ersten Beispiel fordert die App Schreibzugriff auf den Listenbereich an.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p127">The following code shows how you use permission scopes and rights in the AppManifest.xml file. In the first example, an add-in is asking for Write access to the list scope.</span></span>
 

 



```XML
<?xml version="1.0" encoding="utf-8" ?>
<App xmlns="http://schemas.microsoft.com/sharepoint/2012/app/manifest"
     ProductID="{4a07f3bd-803d-45f2-a710-b9e944c3396e}"
     Version="1.0.0.0"
     SharePointMinVersion="15.0.0.0"
     Name="MySampleAddIn"
>
  <Properties>
    <Title>My Sample Add-in</Title>
    <StartPage>~remoteAppUrl/Home.aspx?{StandardTokens}</StartPage>
  </Properties>

  <AppPrincipal>
    <RemoteWebApplication ClientId="1ee82b34-7c1b-471b-b27e-ff272accd564" />
  </AppPrincipal>

  <AppPermissionRequests>
    <AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web/list" Right="Write"/>
  </AppPermissionRequests>
</App>
```

<span data-ttu-id="cfd15-225">Im folgenden Code wird eine App veranschaulicht, die Lesezugriff auf den Webbereich und Schreibzugriff auf den Listenbereich anfordert.</span><span class="sxs-lookup"><span data-stu-id="cfd15-225">The following code shows an add-in that is asking for Read access to the web scope and Write access to the list scope.</span></span>
 

 



```XML
<?xml version="1.0" encoding="utf-8" ?>
<App xmlns="http://schemas.microsoft.com/sharepoint/2012/app/manifest"
     ProductID="{4a07f3bd-803d-45f2-a710-b9e944c3396e}"
     Version="1.0.0.0"
     SharePointMinVersion="15.0.0.0"
     Name="MySampleAddIn"
>
  <Properties>
    <Title>My Sample Add-in</Title>
    <StartPage>~remoteAppUrl/Home.aspx?{StandardTokens}</StartPage>
  </Properties>

  <AppPrincipal>
    <RemoteWebApplication ClientId="6daebfdd-6516-4506-a7a9-168862921986" />
  </AppPrincipal>

  <AppPermissionRequests>
    <AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web" Right="Read"/>
    <AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web/list" Right="Write"/>
  </AppPermissionRequests>
</App>
```


### <a name="permission-request-scopes-for-other-sharepoint-features"></a><span data-ttu-id="cfd15-226">Berechtigungsanforderungsbereiche für andere SharePoint-Funktionen</span><span class="sxs-lookup"><span data-stu-id="cfd15-226">Permission request scopes for other SharePoint features</span></span>
<span data-ttu-id="cfd15-227"><a name="PermissionsForLists"> </a></span><span class="sxs-lookup"><span data-stu-id="cfd15-227"></span></span>

<span data-ttu-id="cfd15-228">Die Berechtigungsanforderungsbereiche für andere SharePoint-Features sind in den folgenden Tabellen aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="cfd15-228">The permission request scope for other SharePoint features are listed in the following tables.</span></span> 
 

 

 <span data-ttu-id="cfd15-229">**Hinweis** Die in der Tabelle angegebenen URIs sind Literalwerte.</span><span class="sxs-lookup"><span data-stu-id="cfd15-229">**Note** The URIs used in the tables are literal values.</span></span>
 

<span data-ttu-id="cfd15-p128">Tabelle 3 enthält den Berechtigungsanforderungsbereich von Business Connectivity Services (BCS). Darin werden auch die Rechte aufgeführt, die für diesen Bereichs-URI angegeben werden können.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p128">Table 3 shows the permission request scope for Business Connectivity Services (BCS) . It also lists the rights that can be specified for that scope URI.</span></span>
 

 

<span data-ttu-id="cfd15-232">**Tabelle 3. URIs und verfügbare Rechte des App-Berechtigungsanforderungsbereichs BCS**</span><span class="sxs-lookup"><span data-stu-id="cfd15-232">**Table 3. BCS add-in permission request scope URIs and available rights**</span></span>

|<span data-ttu-id="cfd15-233">**Bereichs-URI**</span><span class="sxs-lookup"><span data-stu-id="cfd15-233">**Scope URI**</span></span>|<span data-ttu-id="cfd15-234">**Verfügbare Rechte**</span><span class="sxs-lookup"><span data-stu-id="cfd15-234">**Available Rights**</span></span>|
|:-----|:-----|
|<span data-ttu-id="cfd15-235">http://sharepoint/bcs/connection</span><span class="sxs-lookup"><span data-stu-id="cfd15-235">http://sharepoint/bcs/connection</span></span>|<span data-ttu-id="cfd15-236">Lesen</span><span class="sxs-lookup"><span data-stu-id="cfd15-236">Read</span></span>|

 <span data-ttu-id="cfd15-237">**Hinweis** Weitere Informationen zum App-Berechtigungsanforderungsbereich für BCS finden Sie unter  [Business Connectivity Services in SharePoint](http://msdn.microsoft.com/library/64b7d032-4b83-4e9e-bc08-f0a161af5457%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfd15-237">**Note** For more information about the BCS add-in permission request scope, see  [Business Connectivity Services in SharePoint](http://msdn.microsoft.com/library/64b7d032-4b83-4e9e-bc08-f0a161af5457%28Office.15%29.aspx).</span></span>
 


 

 
<span data-ttu-id="cfd15-p129">Tabelle 4 zeigt den Berechtigungsanforderungsbereich für „Search“. Darüber hinaus sind die Rechte aufgeführt, die für diesen Bereichs-URI angegeben werden können.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p129">Table 4 shows the permission request scope for Search. It also lists the rights that can be specified for that scope URI.</span></span>
 

 

<span data-ttu-id="cfd15-240">**Tabelle 4. URIs und verfügbare Rechte des App-Berechtigungsanforderungsbereichs Search**</span><span class="sxs-lookup"><span data-stu-id="cfd15-240">**Table 4. Search add-in permission request scope URIs and available rights**</span></span>

|<span data-ttu-id="cfd15-241">**Bereichs-URI**</span><span class="sxs-lookup"><span data-stu-id="cfd15-241">**Scope URI**</span></span>|<span data-ttu-id="cfd15-242">**Verfügbare Rechte**</span><span class="sxs-lookup"><span data-stu-id="cfd15-242">**Available Rights**</span></span>|
|:-----|:-----|
|<span data-ttu-id="cfd15-243">http://sharepoint/search</span><span class="sxs-lookup"><span data-stu-id="cfd15-243">http://sharepoint/search</span></span>|<span data-ttu-id="cfd15-244">QueryAsUserIgnoreAppPrincipal</span><span class="sxs-lookup"><span data-stu-id="cfd15-244">QueryAsUserIgnoreAppPrincipal</span></span>|

 <span data-ttu-id="cfd15-245">**Hinweis** Weitere Informationen zum App-Berechtigungsanforderungsbereich „Search“ finden Sie unter  [Suche in SharePoint](http://msdn.microsoft.com/library/59220f81-0e5e-4945-8056-cf0a116446cb%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfd15-245">**Note** For more information about the Search add-in permission request scope, see  [Search in SharePoint](http://msdn.microsoft.com/library/59220f81-0e5e-4945-8056-cf0a116446cb%28Office.15%29.aspx).</span></span>
 


 

 
<span data-ttu-id="cfd15-p130">Tabelle 5 enthält den Berechtigungsanforderungsbereich für Project Server 2013. Darin werden auch die Rechte aufgeführt, die für diesen Bereichs-URI angegeben werden können.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p130">Table 5 shows the permission request scope for Project Server 2013. It also lists the rights that can be specified for each scope URI.</span></span>
 

 

 <span data-ttu-id="cfd15-p131">**Hinweis** Anwendungen, die Features und Dienste von Project Server 2013 verwenden, sollten in einer Umgebung getestet werden, die über die erforderlichen Project Server-Features und -Dienste verfügen. Die Berechtigungsanbieterassembly von Project Server 2013, in der die Project Server 2013-Berechtigungsbereiche verzeichnet sind, wird nicht standardmäßig mit SharePoint Server installiert. Weitere Informationen finden Sie in der Project Server 2013-Entwicklerdokumentation.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p131">**Note** An add-in that uses Project Server 2013 features and services should be tested in an environment that has the required Project Server features and services. The Project Server 2013 permission provider assembly that knows about Project Server 2013 permission scopes is not installed by default with SharePoint Server. For more information, see the Project Server 2013 developer documentation.</span></span>
 


<span data-ttu-id="cfd15-251">**Tabelle 5: URIs des Projektserver-Add-In-Berechtigungsanforderungsbereichs und verfügbaren Rechte**</span><span class="sxs-lookup"><span data-stu-id="cfd15-251">**Table 5. Project Server add-in permission request scope URIs and available rights**</span></span>

|<span data-ttu-id="cfd15-252">**Bereich**</span><span class="sxs-lookup"><span data-stu-id="cfd15-252">**Scope**</span></span>|<span data-ttu-id="cfd15-253">**Verfügbare Rechte**</span><span class="sxs-lookup"><span data-stu-id="cfd15-253">**Available Rights**</span></span>|
|:-----|:-----|
|<span data-ttu-id="cfd15-254">http://sharepoint/projectserver</span><span class="sxs-lookup"><span data-stu-id="cfd15-254">http://sharepoint/projectserver</span></span>|<span data-ttu-id="cfd15-255">Verwalten</span><span class="sxs-lookup"><span data-stu-id="cfd15-255">Manage</span></span>|
|<span data-ttu-id="cfd15-256">http://sharepoint/projectserver/projects</span><span class="sxs-lookup"><span data-stu-id="cfd15-256">http://sharepoint/projectserver/projects</span></span>|<span data-ttu-id="cfd15-257">Read, Write</span><span class="sxs-lookup"><span data-stu-id="cfd15-257">Read, Write</span></span>|
|<span data-ttu-id="cfd15-258">http://sharepoint/projectserver/projects/project</span><span class="sxs-lookup"><span data-stu-id="cfd15-258">http://sharepoint/projectserver/projects/project</span></span>|<span data-ttu-id="cfd15-259">Read, Write</span><span class="sxs-lookup"><span data-stu-id="cfd15-259">Read, Write</span></span>|
|<span data-ttu-id="cfd15-260">http://sharepoint/projectserver/enterpriseresources</span><span class="sxs-lookup"><span data-stu-id="cfd15-260">http://sharepoint/projectserver/enterpriseresources</span></span>|<span data-ttu-id="cfd15-261">Read, Write</span><span class="sxs-lookup"><span data-stu-id="cfd15-261">Read, Write</span></span>|
|<span data-ttu-id="cfd15-262">http://sharepoint/projectserver/statusing</span><span class="sxs-lookup"><span data-stu-id="cfd15-262">http://sharepoint/projectserver/statusing</span></span>|<span data-ttu-id="cfd15-263">SubmitStatus</span><span class="sxs-lookup"><span data-stu-id="cfd15-263">SubmitStatus</span></span>|
|<span data-ttu-id="cfd15-264">http://sharepoint/projectserver/reporting</span><span class="sxs-lookup"><span data-stu-id="cfd15-264">http://sharepoint/projectserver/reporting</span></span>|<span data-ttu-id="cfd15-265">Lesen</span><span class="sxs-lookup"><span data-stu-id="cfd15-265">Read</span></span>|
|<span data-ttu-id="cfd15-266">http://sharepoint/projectserver/workflow</span><span class="sxs-lookup"><span data-stu-id="cfd15-266">http://sharepoint/projectserver/workflow</span></span>|<span data-ttu-id="cfd15-267">Elevate</span><span class="sxs-lookup"><span data-stu-id="cfd15-267">Elevate</span></span>|

 

 
<span data-ttu-id="cfd15-p132">Tabelle 6 enthält den Berechtigungsanforderungsbereich für Features für soziale Netzwerke. Darin werden auch die Rechte aufgeführt, die für diesen Bereichs-URI angegeben werden können.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p132">Table 6 shows the permission request scope for social features. It also lists the rights that can be specified for each scope URI.</span></span>
 

 

<span data-ttu-id="cfd15-270">**Tabelle 6. URIs und verfügbare Rechte des App-Berechtigungsanforderungsbereichs für Features für soziale Netzwerke**</span><span class="sxs-lookup"><span data-stu-id="cfd15-270">**Table 6. Social features add-in permission request scope URIs and available rights**</span></span>

|<span data-ttu-id="cfd15-271">**Bereichs-URI**</span><span class="sxs-lookup"><span data-stu-id="cfd15-271">**Scope URI**</span></span>|<span data-ttu-id="cfd15-272">**Verfügbare Rechte**</span><span class="sxs-lookup"><span data-stu-id="cfd15-272">**Available Rights**</span></span>|
|:-----|:-----|
|<span data-ttu-id="cfd15-273">http://sharepoint/social/tenant</span><span class="sxs-lookup"><span data-stu-id="cfd15-273">http://sharepoint/social/tenant</span></span>|<span data-ttu-id="cfd15-274">Read, Write, Manage, FullControl</span><span class="sxs-lookup"><span data-stu-id="cfd15-274">Read, Write, Manage, FullControl</span></span>|
|<span data-ttu-id="cfd15-275">http://sharepoint/social/core</span><span class="sxs-lookup"><span data-stu-id="cfd15-275">http://sharepoint/social/core</span></span>|<span data-ttu-id="cfd15-276">Read, Write, Manage, FullControl</span><span class="sxs-lookup"><span data-stu-id="cfd15-276">Read, Write, Manage, FullControl</span></span>|
|<span data-ttu-id="cfd15-277">http://sharepoint/social/microfeed</span><span class="sxs-lookup"><span data-stu-id="cfd15-277">http://sharepoint/social/microfeed</span></span>|<span data-ttu-id="cfd15-278">Read, Write, Manage, FullControl</span><span class="sxs-lookup"><span data-stu-id="cfd15-278">Read, Write, Manage, FullControl</span></span>|

 <span data-ttu-id="cfd15-279">**Hinweis** Weitere Informationen zum App-Berechtigungsanforderungsbereich für Features für soziale Netzwerke finden Sie unter  [App-Berechtigungsanforderungen für den Zugriff auf soziale Features](http://msdn.microsoft.com/library/8852ce36-8309-45a7-a141-2e10ac17a123%28Office.15%29.aspx#bkmk_AppPerms).</span><span class="sxs-lookup"><span data-stu-id="cfd15-279">**Note** For more information about social features add-in permission request scope, see  [Add-in permission requests for accessing social features](http://msdn.microsoft.com/library/8852ce36-8309-45a7-a141-2e10ac17a123%28Office.15%29.aspx#bkmk_AppPerms).</span></span>
 


 

 
<span data-ttu-id="cfd15-p133">Tabelle 7 zeigt den Berechtigungsanforderungsbereich für „Taxonomy“. Darüber hinaus sind die Rechte aufgeführt, die für diesen Bereichs-URI angegeben werden können.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p133">Table 7 shows the permission request scope for taxonomy. It also lists the rights that can be specified for that scope URI.</span></span>
 

 

<span data-ttu-id="cfd15-282">**Tabelle 7. URIs und verfügbare Rechte des App-Berechtigungsanforderungsbereichs Taxonomy**</span><span class="sxs-lookup"><span data-stu-id="cfd15-282">**Table 7. Taxonomy add-in permission request scope URIs and available rights**</span></span>

|<span data-ttu-id="cfd15-283">**Bereichs-URI**</span><span class="sxs-lookup"><span data-stu-id="cfd15-283">**Scope URI**</span></span>|<span data-ttu-id="cfd15-284">**Verfügbare Rechte**</span><span class="sxs-lookup"><span data-stu-id="cfd15-284">**Available Rights**</span></span>|
|:-----|:-----|
|<span data-ttu-id="cfd15-285">http://sharepoint/taxonomy</span><span class="sxs-lookup"><span data-stu-id="cfd15-285">http://sharepoint/taxonomy</span></span>|<span data-ttu-id="cfd15-286">Read, Write</span><span class="sxs-lookup"><span data-stu-id="cfd15-286">Read, Write</span></span>|

 <span data-ttu-id="cfd15-287">**Hinweis** Weitere Informationen zum App-Berechtigungsanforderungsbereich Taxonomy finden Sie unter  [Hinzufügen von SharePoint-Funktionen](http://msdn.microsoft.com/library/11ecb65e-6dc5-4cf1-80ca-3c16418697b6%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfd15-287">**Note** For more information about the taxonomy add-in permission request scope, see  [Add SharePoint capabilities](http://msdn.microsoft.com/library/11ecb65e-6dc5-4cf1-80ca-3c16418697b6%28Office.15%29.aspx).</span></span>
 


### <a name="permission-request-scope-with-associated-properties"></a><span data-ttu-id="cfd15-288">Berechtigungsanforderungsbereich mit den zugehörigen Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="cfd15-288">Permission request scope with associated properties</span></span>
<span data-ttu-id="cfd15-289"><a name="AssociatedProperties"> </a></span><span class="sxs-lookup"><span data-stu-id="cfd15-289"></span></span>

<span data-ttu-id="cfd15-p134">Der Berechtigungsanforderungsbereich für Listen verfügt über eine zusätzliche Eigenschaft. Dem Listenbereich kann eine Eigenschaft namens **BaseTemplateId** und ein ganzzahliger Wert für eine Listenbasisvorlage übergeben werden, wie im Markupbeispiel unten gezeigt. Wenn keine Listenbasisvorlagen-ID angegeben wird, hat der Benutzer, der das Add-In installiert, die Wahl, ihr die Berechtitung für *eine Liste*  aus allen Listen im Web zu gewähren. Durch die Angabe einer Listenbasisvorlagen-ID wird die Auswahl des Benutzers auf die Gruppe von Listen eingeschränkt, die dem Wert der Eigenschaft **BaseTemplateId** entsprechen.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p134">The list permission request scope has an additional optional property. The list scope can take a property with the name **BaseTemplateId**, and an integer value corresponding with a list base template, as shown in the markup sample below. Without a base template ID, the user who installs the add-in has the choice of granting it permission to *one list*  from among all lists in the web. Specifying a base template ID limits the user's choice to the set of lists that match what is specified by the **BaseTemplateId** property.</span></span>
 

 
<span data-ttu-id="cfd15-p135">Die **BaseTemplateId**-Eigenschaft ist ein untergeordnetes Element, kein Attribut des **AppPermissionRequest**-Elements. Im folgenden Code wird gezeigt, wie die **BaseTemplateId**-Eigenschaft verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p135">The **BaseTemplateId** property is a child element, not an attribute of the **AppPermissionRequest** element. The following code shows how to use the **BaseTemplateId** property.</span></span>
 

 



```XML
<AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web/list" Right="Write">
  <Property Name="BaseTemplateId" Value="101"/>
</AppPermissionRequest>
```


<span data-ttu-id="cfd15-296">**Tabelle 7: Berechtigungsanforderungsbereich mit den zugehörigen Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="cfd15-296">**Table 7. Permission request scope with associated properties**</span></span>

|<span data-ttu-id="cfd15-297">**Bereichs-URI**</span><span class="sxs-lookup"><span data-stu-id="cfd15-297">**Scope URI**</span></span>|<span data-ttu-id="cfd15-298">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="cfd15-298">**Property**</span></span>|<span data-ttu-id="cfd15-299">**Typ**</span><span class="sxs-lookup"><span data-stu-id="cfd15-299">**Type**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="cfd15-300">http://sharepoint/content/sitecollection/web/list</span><span class="sxs-lookup"><span data-stu-id="cfd15-300">http://sharepoint/content/sitecollection/web/list</span></span>|<span data-ttu-id="cfd15-301">**BaseTemplateId**</span><span class="sxs-lookup"><span data-stu-id="cfd15-301">**BaseTemplateId**</span></span>|<span data-ttu-id="cfd15-302">Ganze Zahl **Hinweis** Weitere Informationen zu **BaseTemplateId** und dem zugehörigen ganzzahligen Wert für die Listenbasisvorlage finden Sie unter dem **Type**-Attribut von [List Element (List)](http://msdn.microsoft.com/library/b2b26fee-eb45-48ac-99f1-65f725da293f%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfd15-302">For more information about **BaseTemplateId** and the corresponding integer value for the list base template, see the **Type** attribute of the [List Element (List)](http://msdn.microsoft.com/library/b2b26fee-eb45-48ac-99f1-65f725da293f%28Office.15%29.aspx).</span></span> |

## <a name="manage-and-troubleshoot-add-in-permissions"></a><span data-ttu-id="cfd15-303">Verwaltung und Problembehandlung von Add-In-Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="cfd15-303">Manage and troubleshoot add-in permissions</span></span>
<span data-ttu-id="cfd15-304"><a name="Perm_manage"> </a></span><span class="sxs-lookup"><span data-stu-id="cfd15-304"></span></span>

<span data-ttu-id="cfd15-p136">SharePoint-Add-Ins, die in SharePoint installiert sind, werden bei der Installation Berechtigungen gewährt. Add-Ins, die auf anderen Plattformen installiert sind, aber auf SharePoint zugreifen, werden während der Laufzeit von dem Benutzer, der das Add-In ausführt, Berechtigungen gewährt. Gelegentlich kann die erste Art von Add-In die Berechtigungen verlieren. Add-Ins können mit den folgenden Schritten erneut Berechtigungen gewährt werden:</span><span class="sxs-lookup"><span data-stu-id="cfd15-p136">SharePoint Add-ins that are installed to SharePoint are granted permissions when they are installed. Add-ins that are installed on other platforms but access SharePoint, are granted permissions at runtime, by the user who is running the add-in. Occasionally, the first kind of add-in may lose its permissions. Add-ins can be regranted its permissions with the following steps:</span></span>
 

 

1. <span data-ttu-id="cfd15-p137">Klicken Sie auf der Seite **Websiteinhalt** der Website, auf der die App Berechtigungen verloren zu haben scheint, auf die Schaltfläche **…** auf der Kachel der App. Damit wird ein Popup mit dem Link **BERECHTIGUNGEN** oder einer weiteren **…**-Schaltfläche geöffnet.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p137">On the **Site Contents** page of the website where the add-in seems to have lost permissions, click the **…** button on the add-in's tile. This will open a callout with either a **PERMISSIONS** link or another **…** button.</span></span>
    
 
2. <span data-ttu-id="cfd15-p138">Klicken Sie auf den Link **BERECHTIGUNGEN**, wenn dieser vorhanden ist, und überspringen Sie den nächsten Schritt, oder klicken Sie auf die Schaltfläche **???**.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p138">Click the **PERMISSIONS** link if it is there and skip the next step, or click the **…** button.</span></span>
    
 
3. <span data-ttu-id="cfd15-315">Klicken Sie auf den Link **Berechtigungen**.</span><span class="sxs-lookup"><span data-stu-id="cfd15-315">Click the **Permissions** link.</span></span>
    
 
4. <span data-ttu-id="cfd15-p139">Klicken auf der daraufhin geöffneten Seite auf den Link **hier** im letzten Satz. Damit werden der App ihre Berechtigungen erneut gewährt, und der Browser wird zurück zu Seite **Websiteinhalt** geleitet.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p139">On the page that opens, click **here** link in the last sentence. This will regrant the add-in its permissions and redirect the browser back to the **Site Contents** page.</span></span>
    
 

 
![Einer App erneut Berechtigungen gewähren](../../images/RegrantPermissionsToAnApp.png)
 
<span data-ttu-id="cfd15-p140">Wenn Sie eine App entwickeln oder Fehler in einer App beheben, gibt es möglicherweise Situationen, in denen Sie die Berechtigungen einer bereits installierten App ändern oder erneut gewähren möchten. Gehen Sie dafür wie folgt vor :</span><span class="sxs-lookup"><span data-stu-id="cfd15-p140">When you are developing an add-in or troubleshooting an add-in, there may be occasions when you want to change, or regrant, the permissions of an add-in that has already been installed. You can do so with these steps:</span></span>
 

 

 

1. <span data-ttu-id="cfd15-p141">Navigieren Sie zu `http://<SharePointWebSite>/_layouts/15/AppInv.aspx`, wobei _<SharePointWebSite>_ die URL der Website ist, auf der die App installiert ist. Achten Sie sorgfältig darauf, dass Sie der URL keine Abfrageparameter hinzufügen. Das benötigte Formular wird nur auf dieser Seite angezeigt, wenn Sie die URL exakt wie angezeigt eingeben.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p141">Navigate to  `http://<SharePointWebSite>/_layouts/15/AppInv.aspx`, where  _<SharePointWebSite>SharePointWebSite_ is the URL of the website where the add-in is installed. Be careful not to add any query parameters on the URL. The form you need only appears on this page if the URL is exactly as shown.</span></span>
    
 
2. <span data-ttu-id="cfd15-p142">Geben Sie die ID der App, die auch als Client-ID bezeichnet wird, in das Feld **App-ID** ein, und klicken Sie auf **Suchen**. Die anderen Felder im Formular werden dann mit Informationen zur App ausgefüllt.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p142">Enter the add-in's ID, also called the client ID, in the **Add-in Id** box and click **Lookup**. The other boxes on the form are then populated with information about the add-in.</span></span>
    
 
3. <span data-ttu-id="cfd15-p143">Füllen Sie das Feld **Berechtigungsanforderungs-XML** genau so mit Berechtigungsanforderungen aus, wie Sie sie in einem App-Manifest eingeben würden. Beispiele finden Sie unter [Berechtigungsanforderungsbereiche für Listeninhalte und Bibliotheksinhalte](#PermissionsForLists) weiter oben. Informationen zur vollständigen Syntax finden Sie unter [AppPermissionRequest-Element](http://msdn.microsoft.com/library/4ad90fb0-33b2-aee5-69c2-5b97ca5334f8%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfd15-p143">Fill the **Permission Request XML** box with permission requests exactly as you would enter them in an add-in manifest. For examples, see [Permission request scopes for list content and library content](#PermissionsForLists) above. For complete syntax information see [AppPermissionRequest Element](http://msdn.microsoft.com/library/4ad90fb0-33b2-aee5-69c2-5b97ca5334f8%28Office.15%29.aspx).</span></span>
    
 
4. <span data-ttu-id="cfd15-329">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="cfd15-329">Click **Create**.</span></span> 
    
 
<span data-ttu-id="cfd15-330">Die Berechtigungen für ein Add-In für einen bestimmten Bereich werden widerrufen, wenn es aus dem Bereich entfernt wird.</span><span class="sxs-lookup"><span data-stu-id="cfd15-330">An add-in's permissions for a specific scope are revoked when it is removed from that scope.</span></span>
 

 

## <a name="learn-why-add-ins-cannot-be-hidden-from-users"></a><span data-ttu-id="cfd15-331">Erfahren Sie, warum Apps nicht vor Benutzern ausgeblendet werden können</span><span class="sxs-lookup"><span data-stu-id="cfd15-331">Learn why add-ins cannot be hidden from users</span></span>
<span data-ttu-id="cfd15-332"><a name="CannotBeHidden"> </a></span><span class="sxs-lookup"><span data-stu-id="cfd15-332"></span></span>

<span data-ttu-id="cfd15-p144">Jeder Benutzer mit Rechten zum Durchsuchen für eine SharePoint-Website kann jedes auf der Website installierte SharePoint-Add-In starten. Ob der Benutzer etwas mit dem Add-In anfangen kann, hängt von den anderen Berechtigungen des Benutzers und davon ab, welcher  [Autorisierungsrichtlinientyp](add-in-authorization-policy-types-in-sharepoint-2013) von dem Add-In verwendet wird. Wenn der Benutzer versucht, etwas mit dem Add-In auszuführen, für das der Benutzer keine Berechtigung besitzt, und der Aufruf an SharePoint die Benutzer- und Add-In-Richtlinie verwendet, wird der Aufruf fehlschlagen.</span><span class="sxs-lookup"><span data-stu-id="cfd15-p144">Any user with browse rights to a SharePoint website can launch any SharePoint Add-in installed on the site. Whether the user can do anything with the add-in will depend on the user's other permissions and what  [authorization policy type](add-in-authorization-policy-types-in-sharepoint-2013) is being used by the add-in. If the user tries to do something with the add-in that the user does not have permission to do, and the call to SharePoint is using the user+add-in policy, then the call will fail.</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="cfd15-336">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="cfd15-336">Additional resources</span></span>
<span data-ttu-id="cfd15-337"><a name="Filename_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="cfd15-337"></span></span>


-  [<span data-ttu-id="cfd15-338">Autorisierung und Authentifizierung für Add-Ins in SharePoint</span><span class="sxs-lookup"><span data-stu-id="cfd15-338">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="cfd15-339">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="cfd15-339">SharePoint Add-ins</span></span>](sharepoint-add-ins)
    
 
-  [<span data-ttu-id="cfd15-340">Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="cfd15-340">Set up an on-premises development environment for SharePoint Add-ins</span></span>](set-up-an-on-premises-development-environment-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="cfd15-341">Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="cfd15-341">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="cfd15-342">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="cfd15-342">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 
