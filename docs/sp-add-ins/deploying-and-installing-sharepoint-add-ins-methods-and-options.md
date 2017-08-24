# <a name="deploying-and-installing-sharepoint-add-ins-methods-and-options"></a><span data-ttu-id="baecb-101">Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen</span><span class="sxs-lookup"><span data-stu-id="baecb-101">Deploying and installing SharePoint Add-ins: methods and options</span></span>
<span data-ttu-id="baecb-102">Informieren Sie sich über die Methoden zum Veröffentlichen, Installieren und Deinstallieren eines SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="baecb-102">Learn about the methods for publishing, installing, and uninstalling a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="baecb-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="baecb-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="publishing-to-the-office-store-or-an-organizations-add-in-catalog"></a><span data-ttu-id="baecb-106">Veröffentlichen im Office Store oder im Add-In-Katalog eines Unternehmens</span><span class="sxs-lookup"><span data-stu-id="baecb-106">Publishing to the Office Store or an organization's add-in catalog</span></span>
<span data-ttu-id="baecb-107"><a name="MarketOrCatalog"> </a></span><span class="sxs-lookup"><span data-stu-id="baecb-107"></span></span>

<span data-ttu-id="baecb-p102">Sie können Ihr SharePoint-Add-In entweder in den öffentlichen Office Store oder in den privaten Add-In-Katalog eines Unternehmens hochladen. Ein privater Add-In-Katalog ist eine dedizierte Websitesammlung in einer SharePoint-Webanwendung (oder einer SharePoint Online-Mandanteneinheit), in der Dokumentbibliotheken für SharePoint-Add-Ins und Office-Add-Ins gehostet werden. Wenn der Katalog in eine eigene Websitesammlung gestellt wird, ist es für den Webanwendungsadministrator oder den Mandantenadministrator einfacher, die Berechtigungen für den Katalog einzuschränken.</span><span class="sxs-lookup"><span data-stu-id="baecb-p102">You can upload your SharePoint Add-in to either the public Office Store or to an organization's private add-in catalog. A private add-in catalog is a dedicated site collection in a SharePoint web application (or a SharePoint Online tenancy) that hosts document libraries for SharePoint Add-ins and Office Add-ins. Putting the catalog into its own site collection makes it easier for the web application administrator or tenant administrator to limit permissions to the catalog.</span></span> 
 

 
<span data-ttu-id="baecb-p103">Wenn das Add-In in den Office Store hochgeladen wird, führt Microsoft Validierungsprüfungen aus. Es wird beispielsweise überprüft, ob das Markup des Add-In-Manifests gültig und vollständig ist, und sichergestellt, dass hinzugefügte SharePoint-Lösungspakte (WSP-Dateien) keine unzulässigen Elemente oder Features mit einem breiteren Bereich als **Web** enthalten. Auch der Paketinhalt wird auf unzulässige Inhalte untersucht. Wenn das Add-In alle Prüfungen besteht, wird das Add-In-Paket in eine Datei verpackt und von Microsoft signiert.</span><span class="sxs-lookup"><span data-stu-id="baecb-p103">If the add-in is uploaded to the Office Store, Microsoft runs some validation checks on it. For example, it checks whether the add-in manifest markup is valid and complete and verifies that any SharePoint solution packages (.wsp files) that are included do not include disallowed elements or Features with a scope broader than **Web**. The content of the package is also inspected for objectionable content. If the add-in passes all tests, the add-in package is wrapped into a file and signed by Microsoft.</span></span> 
 

 

 <span data-ttu-id="baecb-p104">**Hinweis** Wenn Sie Ihr Add-In mit den Microsoft Office Developer Tools für Visual Studio entwickeln und bereitstellen, wird das Add-In direkt auf der SharePoint-Zieltestwebsite installiert. Da es nicht über den Office Store übergeben wird, findet die oben beschriebene Überprüfung nicht statt.</span><span class="sxs-lookup"><span data-stu-id="baecb-p104">**Note** When you are developing your add-in and deploying it with Microsoft Office Developer Tools for Visual Studio, the add-in is directly installed in the target test SharePoint site. Since it is not passing through the Office Store, the validation checking described above does not occur.</span></span>
 

<span data-ttu-id="baecb-p105">Ein SharePoint-Add-In in den Add-In-Katalog eines Unternehmens zu laden ist so einfach, wie eine Datei in eine SharePoint Foundation-Dokumentbibliothek zu laden. Sie füllen ein Popup-Formular aus, in dem Sie die lokale URL des Add-In-Pakets und weitere Informationen angeben, wie z. B. den Namen des Add-Ins. Wenn das Add-In in den Add-In-Katalog eines Unternehmens geladen wird, werden ähnliche Überprüfungen durchgeführt. Dabei werden Add-Ins, die die Prüfungen nicht bestehen, als ungültig gekennzeichnet oder im Katalog deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="baecb-p105">Uploading a SharePoint Add-in to an organization's add-in catalog is as easy as uploading any file to a SharePoint Foundation document library. You fill out a pop-up form in which you supply the local URL of the add-in package and other information, such as the name of the add-in. When the add-in is uploaded to an organization's add-in catalog, similar checks take place and add-ins that do not pass are marked as invalid or disabled in the catalog.</span></span> 
 

 
<span data-ttu-id="baecb-p106">Mandantenadministratoren und SharePoint-Webanwendungsadministratoren können SharePoint-Add-Ins im Office Store kaufen. Zum Öffnen des Office Store wählt der Administrator die Option **Add-In hinzufügen** auf der Seite **Websiteinhalte** und dann **SharePoint Store** auf der Seite **Eigene Add-Ins** aus. Damit wird die Seite **SharePoint Store** geöffnet, über die der Administrator mehr über SharePoint-Add-Ins erfahren kann, die von Anbietern angeboten werden. (Dies ist auch auf office.com möglich.) Add-Ins, die eine erforderliche Komponente benötigen, die auf der Anwendungswebsite oder Mandantschaft des Administrators nicht installiert ist, werden abgeblendet angezeigt und sind im Add-In-Store nicht verfügbar. Wenn ein Add-In beispielsweise Suchdienste erfordert und diese nicht installiert sind, wird das Add-In abgeblendet angezeigt. Administratoren können die Liste der Add-Ins sortieren, filtern und durchsuchen, Informationen über Add-Ins lesen, Add-In-Rezensionen anzeigen und Lizenzen für ein Add-In erwerben.</span><span class="sxs-lookup"><span data-stu-id="baecb-p106">Tenant administrators and SharePoint web application administrators can shop for SharePoint Add-ins on the Office Store. To open the Office Store, the administrator selects **Add an Add-in** on the **Site Contents** page and then selects **SharePoint Store** in the **Your Add-ins** page. This opens a **SharePoint Store** page that the administrators can use to discover and learn about SharePoint Add-ins that vendors are offering. (They can also do this on office.com.) Add-ins that require a prerequisite that is not installed on the administrator's web application or tenancy appear dimmed and are unavailable in the add-in store. For example, if an add-in requires Search Services and this is not installed, the add-in appears dimmed. Administrators can sort, filter, and browse the list of add-ins, read about the add-ins, see add-in reviews, and purchase licenses for an add-in.</span></span>
 

 
<span data-ttu-id="baecb-126">Wenn ein Administrator eine Lizenz erwerben möchte, muss er die Kaufbestimmungen akzeptieren und den für das Add-In erforderlichen Berechtigungen zustimmen, wie z. B. Lesezugriff auf Listen oder Vollzugriff auf die Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="baecb-126">When an administrator decides to purchase a license, she must accept the terms and conditions of purchase and agree to the permissions that the add-in must have in order to execute, such as read access to lists or full control access to the site collection.</span></span> 
 

 
<span data-ttu-id="baecb-p107">Wenn eine oder mehrere Lizenzen für ein Add-In erworben werden, werden die Lizenzen in die Webanwendung oder Mandanteneinheit heruntergeladen. Das Add-In wird beim Lizenzerwerb nicht automatisch heruntergeladen und installiert, obwohl der Administrator die Option hat, die Installation mit dem Lizenzerwerb zu kombinieren.</span><span class="sxs-lookup"><span data-stu-id="baecb-p107">When one or more licenses for an add-in are purchased, the licenses are downloaded to the web application or tenancy. The add-in is not automatically downloaded and installed when the license is purchased, although administrators have the option to combine installation with license purchase.</span></span>
 

 
<span data-ttu-id="baecb-p108">Benutzer installieren Add-Ins von der Seite **Ihre Add-Ins**. Diese Seite enthält eine zusammengeführte Liste mit folgenden Komponenten:</span><span class="sxs-lookup"><span data-stu-id="baecb-p108">Users install add-ins from the **Your Add-ins** page. This page has a merged listing of the following:</span></span>
 

 

- <span data-ttu-id="baecb-131">SharePoint-Add-Ins aus dem Organisations-Add-In-Katalog der Webanwendung (oder des Mandanten).</span><span class="sxs-lookup"><span data-stu-id="baecb-131">SharePoint Add-ins from the web application's (or the tenant's) organization add-in catalog.</span></span>
    
 
- <span data-ttu-id="baecb-132">SharePoint-Add-Ins aus dem Office Store, für die das Unternehmen oder der Mandant bereits eine Website-Lizenz oder eine dem Benutzer zugewiesene Lizenz besitzt.</span><span class="sxs-lookup"><span data-stu-id="baecb-132">SharePoint Add-ins from the Office Store for which the organization or tenant already owns a site license or a license which has been assigned to the user.</span></span>
    
 
<span data-ttu-id="baecb-p109">Alle Add-Ins, die der Benutzer sofort installieren kann, werden aufgeführt, und mit einigen wenigen Ausnahmen werden nur Add-Ins aufgeführt, die der Benutzer sofort installieren kann. Benutzer können die auf der Seite enthaltenen Add-Ins filtern, um dem Organsiations-Add-In-Katalog nur Add-Ins hinzuzufügen. Wenn ein Add-In installiert ist, wird es in der Liste der Add-Ins auf der Seite **Websiteinhalte** der Website angezeigt, auf der es installiert ist.</span><span class="sxs-lookup"><span data-stu-id="baecb-p109">All the add-ins that the user can install immediately are listed, and with few exceptions only add-ins the user can install immediately are listed. Users can filter the add-ins included on the page to include only add-ins in the organization's add-in catalog. When an add-in is installed, it appears in the list of add-ins on the **Site Contents** page of the website to which it is installed.</span></span>
 

 

## <a name="installing-sharepoint-add-ins"></a><span data-ttu-id="baecb-136">Installieren von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="baecb-136">Installing SharePoint Add-ins</span></span>
<span data-ttu-id="baecb-137"><a name="Installing"> </a></span><span class="sxs-lookup"><span data-stu-id="baecb-137"></span></span>

<span data-ttu-id="baecb-p110">Websitebesitzer installieren SharePoint-Add-Ins von der Seite **Ihre Add-Ins**, wie weiter oben in diesem Thema beschrieben. Die Installation erstellt eine Instanz des Add-Ins. Weitere Informationen über das Installieren von Add-Ins finden Sie unter [Hinzufügen von SharePoint-Add-Ins zu einer SharePoint-Website](https://technet.microsoft.com/en-us/library/fp161231.aspx).</span><span class="sxs-lookup"><span data-stu-id="baecb-p110">Website owners install SharePoint Add-ins from the **Your Add-ins** page as described earlier in this topic. Installation creates an instance of the add-in. For more information about installing add-ins, see [Add SharePoint Add-ins to a SharePoint site](https://technet.microsoft.com/en-us/library/fp161231.aspx).</span></span> 
 

 

 <span data-ttu-id="baecb-p111">**Hinweis** Manchmal kann ein vorübergehender Verlust der Netzwerkverbindung die Installation blockieren. Wenn die Installation aus irgendeinem Grund fehlschlägt, führt die Installationsinfrastruktur drei Wiederholungsversuche durch. Wenn sie nicht erfolgreich sind, wird dies auf der Benutzeroberfläche angezeigt. Benutzer können die Installation zu einem späteren Zeitpunkt erneut versuchen.</span><span class="sxs-lookup"><span data-stu-id="baecb-p111">**Note** Sometimes a temporary loss of a network connection can block installation. If installation fails for any reason, the installation infrastructure will retry three times. If it does not succeed, an indication of the failure appears in the UI. Users can retry the installation later.</span></span> 
 


## <a name="uninstalling-sharepoint-add-ins"></a><span data-ttu-id="baecb-145">Deinstallieren von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="baecb-145">Uninstalling SharePoint Add-ins</span></span>
<span data-ttu-id="baecb-146"><a name="Uninstalling"> </a></span><span class="sxs-lookup"><span data-stu-id="baecb-146"></span></span>

<span data-ttu-id="baecb-p112">Websitebesitzer können eine Instanz eines SharePoint-Add-In über die SharePoint-Benutzeroberfläche deinstallieren. Die Deinstallation einer Instanz eines SharePoint-Add-Ins ist sauber. Das bedeutet, dass alle vom Add-In installierten Komponenten deinstalliert werden.</span><span class="sxs-lookup"><span data-stu-id="baecb-p112">Website owners can uninstall an instance of a SharePoint Add-in through the SharePoint UI. Uninstallation of an instance of a SharePoint Add-ins is clean. This means that everything installed by the add-in is uninstalled.</span></span> 
 

 
<span data-ttu-id="baecb-p113">Komponenten jedoch, die von einem Add-In verwendet werden, aber separat von der Installation des Add-Ins installiert sind, werden nicht entfernt. Nehmen Sie beispielsweise an, ein Add-In verfügt über eine Remotewebseite mit Schaltflächen, die Listen im Hostweb erstellen. Durch die Deinstallation des Add-Ins wird die Kachel des Add-Ins von der Seite **Websiteinhalte** entfernt, wodurch wiederum die Remoteseite im Wesentlichen für Endbenutzer nicht zugänglich oder nicht benutzbar wird; die Listen, die mit dem Add-In erstellt wurden, werden jedoch nicht entfernt. SharePoint bewahrt keine Aufzeichnung auf, welche Listen im Hostweb mit dem Add-In und welche von Benutzern in der SharePoint-Benutzeroberfläche erstellt wurden, deshalb können mit dem Add-In erstellte Listen nicht gelöscht werden. Im Allgemeinen ist dieses Verhalten wünschenswert, da die Listen möglicherweise Daten enthalten, die für Benutzer auch nach Entfernen des Add-Ins, das die Listen erstellt hat, nützlich bleiben können.</span><span class="sxs-lookup"><span data-stu-id="baecb-p113">However, components that an add-in uses, but that are installed separately from the installation of the add-in, are not removed. For example, suppose an add-in has a remote web page with buttons that create lists on the host web. Uninstallation of the add-in removes the add-in's tile from the **Site Contents** page which, in turn makes the remote page effectively inaccessible or unusable for end users, but it does not remove the lists that were created with the add-in. SharePoint does not keep a record of which lists on the host web were created with the add-in and which ones were created by users in the SharePoint UI, so it can't delete lists that were created with the add-in. This is generally desirable behavior because the lists may have data that remains useful to users even after the removal of the add-in that created the lists.</span></span>
 

 
<span data-ttu-id="baecb-p114">Wenn das SharePoint-Add-In ein Add-In-Web umfasst, wird das Add-In-Web gelöscht. Dies ermöglicht eine sauberere Deinstallation als die systematische Deaktivierung von Funktionen und das Rückgängigmachen der Bereitstellung der Internen WSP-Datei des Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="baecb-p114">If the SharePoint Add-in includes an add-in web, the add-in web is deleted. This provides a cleaner uninstall than systematically deactivating features and reversing the deployment of the add-in's internal .wsp file.</span></span>
 

 

 <span data-ttu-id="baecb-p115">**Hinweis** Wenn ein Benutzer ein Add-In entfernt, wird es in die erste Phase des Papierkorbs verschoben. Wird es dort gelöscht, wird es in die zweite Phase des Papierkorbs verschoben. Wird es aus der zweiten Phase des Papierkorbs gelöscht, dann wird das Add-In vollständig deinstalliert und kann nicht wiederhergestellt werden.</span><span class="sxs-lookup"><span data-stu-id="baecb-p115">**Note** When a user removes an add-in, it is moved to the first stage Recycle Bin. Deleting it from there moves it to the second stage Recycle Bin. If it is deleted from the second stage Recycle Bin, then it is completely uninstalled and cannot be restored.</span></span> 
 

<span data-ttu-id="baecb-160">Außerdem werden die Berechtigungen des Add-Ins beim Entfernen (Recyceln) des Add-Ins entsprechend den folgenden Regeln widerrufen:</span><span class="sxs-lookup"><span data-stu-id="baecb-160">The add-in's permissions are also revoked when it is removed (recycled), according to these rules:</span></span>
 

 

- <span data-ttu-id="baecb-161">Webgültigkeitsberechtigungen werden immer abgerufen.</span><span class="sxs-lookup"><span data-stu-id="baecb-161">Web-scoped permissions are always revoked.</span></span>
    
 
- <span data-ttu-id="baecb-162">Falls es keine weitere Instanz des Add-Ins in der Websitesammlung gibt, werden die Berechtigungen für die Websitesammlung ebenfalls abgerufen.</span><span class="sxs-lookup"><span data-stu-id="baecb-162">If there is no other instance of the add-in in the site collection, site collection-scoped permissions are also revoked.</span></span>
    
 
- <span data-ttu-id="baecb-163">Wenn keine andere Instanz des Add-Ins im Websiteabonnement (Mandantschaft) vorhanden ist, werden auch Berechtigungen im Mandantenbereich widerrufen.</span><span class="sxs-lookup"><span data-stu-id="baecb-163">If there is no other instance of the add-in in the site subscription (tenancy), tenant-scoped permissions are also revoked.</span></span>
    
 
<span data-ttu-id="baecb-p116">Der Webdienst  [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx), falls er im App-Manifest des Add-Ins registeriert ist, wird zu Beginn des Deinstallationsvorgangs ausgeführt (tritt auf, wenn das Add-In aus dem endgültigen Papierkorb entfernt wird). Sie sollten den Webdienst  [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx) installiert haben, wenn Sie gleichzeitig auch [InstalledEventEndpoint](http://msdn.microsoft.com/library/af9f83d8-8325-3ede-d7b0-bb82c0445eb9%28Office.15%29.aspx) installiert haben. Sie sollten auch den Dienst [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx) entwerfen, um eventuell Schritte im [InstalledEventEndpoint](http://msdn.microsoft.com/library/af9f83d8-8325-3ede-d7b0-bb82c0445eb9%28Office.15%29.aspx)-Dienst rückgängig machen zu können. Weitere Informationen finden Sie unter  [Behandeln von Ereignissen in SharePoint-Add-Ins](handle-events-in-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="baecb-p116">The  [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx) web service, if one is registered in the add-in manifest of the add-in, executes at the beginning of the uninstallation process (which occurs when the add-in is removed from the second stage Recycle Bin). It is a best practice to have an [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx) web service if you have an [InstalledEventEndpoint](http://msdn.microsoft.com/library/af9f83d8-8325-3ede-d7b0-bb82c0445eb9%28Office.15%29.aspx) web service and to design the [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx) service to reverse anything done in your [InstalledEventEndpoint](http://msdn.microsoft.com/library/af9f83d8-8325-3ede-d7b0-bb82c0445eb9%28Office.15%29.aspx) service. For more information, see [Handle events in SharePoint Add-ins](handle-events-in-sharepoint-add-ins).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="baecb-167">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="baecb-167">Additional resources</span></span>
<span data-ttu-id="baecb-168"><a name="SP15deployinstallapps_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="baecb-168"></span></span>


-  [<span data-ttu-id="baecb-169">Veröffentlichen von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="baecb-169">Publish SharePoint Add-ins</span></span>](publish-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="baecb-170">Kritische Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="baecb-170">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 
-  [<span data-ttu-id="baecb-171">Aktualisierungsverfahren für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="baecb-171">SharePoint Add-ins update process</span></span>](sharepoint-add-ins-update-process)
    
 

