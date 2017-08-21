
# <a name="update-host-web-components-in-sharepoint"></a><span data-ttu-id="526b8-101">Aktualisieren von SharePoint-Hostwebkomponenten</span><span class="sxs-lookup"><span data-stu-id="526b8-101">Update host web components in SharePoint</span></span>
<span data-ttu-id="526b8-102">Aktualisieren von Add-In-Webparts und benutzerdefinierten Aktionen im Hostweb eines SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="526b8-102">Update add-in parts and custom actions in the host web of a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="526b8-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="526b8-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="prerequisites-for-updating-host-web-components"></a><span data-ttu-id="526b8-106">Voraussetzungen für die Aktualisierung von Hostwebkomponenten</span><span class="sxs-lookup"><span data-stu-id="526b8-106">Prerequisites for updating host web components</span></span>
<span data-ttu-id="526b8-107"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="526b8-107"></span></span>

<span data-ttu-id="526b8-108">Kenntnisse des Themas [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins) und der darin aufgeführten erforderlichen Komponenten und Kernkonzepte.</span><span class="sxs-lookup"><span data-stu-id="526b8-108">Be familiar with  [Update SharePoint Add-ins](update-sharepoint-add-ins) and the prerequisites and core concepts listed in it.</span></span>
 

 

## <a name="update-host-web-components"></a><span data-ttu-id="526b8-109">Aktualisieren von Hostwebkomponenten</span><span class="sxs-lookup"><span data-stu-id="526b8-109">Update host web components</span></span>
<span data-ttu-id="526b8-110"><a name="UpdateHostWeb"> </a></span><span class="sxs-lookup"><span data-stu-id="526b8-110"></span></span>

<span data-ttu-id="526b8-p102">Ihr Add-In kann zwei Arten von Komponenten auf einem Hostweb mit beschreibendem Markup im SharePoint-Add-In installieren: benutzerdefinierte Aktionen undAdd-In-Webparts. Das Aktualisieren dieser Komponenten ist im Hostweb einacher als im Add-In-Web. Sie müssen keine Semantik aktualisieren, fügen Sie einfach die benutzerdefinierten Aktionen und Add-In-Webparts hinzu bzw. ändern Sie diese. Wenn das SharePoint-Add-In aktualisiert wird, wendet SharePoint immer alle neuen Elementmanifestdateien an und wendet dann alle geänderten Elementmanifestdateien in ihrer aktuellen Version erneut an. Die erneute Anwendung verursacht keine Probleme; z. B wird eine Menübandschaltfläche für eine benutzerdefinierte Aktion nicht mehrfach zum Menüband hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="526b8-p102">Your add-in can install two kinds of components on a host web with descriptive markup in the SharePoint Add-in: custom actions andadd-in parts. Updating these components is easier in the host web than in the add-in web. You don't need any update semantics. Just add/change the custom actions and add-in parts. When the SharePoint Add-in is updated, SharePoint always applies any new element manifest files and reapplies any changed element manifest files with the most recent version. No harm is done in reapplying; for example, a ribbon button for a custom action will not be added multiple times to the ribbon.</span></span>
 

 
<span data-ttu-id="526b8-p103">Wenn Sie ein Add-In-Webpart aktualisieren, ersetzt SharePoint die alte Version durch die neue Version im Webpartkatalog. Achten Sie darauf, die Eigenschaft **Name** des **ClientWebPart**-Objekts zu ändern, wenn Sie ein Add-In-Webpart aktualisieren. Dies gewährleistet beim Aktualisieren des Add-Ins, dass SharePoint die alte Version des Add-In-Webparts (diese ist nicht mehr Teil des Add-Ins) von allen Seiten entfernt, zu denen sie hinzugefügt wurde. Die Benutzer müssen die neue Version erneut zu den Seiten hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="526b8-p103">When you update an add-in part, SharePoint replaces the old version with the new version in the Web Part gallery. Be sure to change the **Name** property of the **ClientWebPart** object when you update an add-in part. Doing this ensures that, when the add-in is updated, SharePoint will remove the old version of the add-in part (which is no longer part of the app) from all pages to which it was added. Users will need to re-add the new version to pages.</span></span>
 

 
<span data-ttu-id="526b8-p104">Wenn Sie die Eigenschaft **Name** unverändert lassen, bleibt die alte Version auf Seiten erhalten, denen sie hinzugefügt wurde. Dadurch ist es unwahrscheinlich, dass die Benutzer bemerken, dass eine neue Version des Add-In-Webparts verfügbar ist. Außerdem wird beim Hinzufügen des Add-In-Webparts zu einer Seite die neue Version verwendet. Dadurch hätte eine Version eines SharePoint-Add-Ins unterschiedliche Add-In-Webparts auf unterschiedlichen Seiten.</span><span class="sxs-lookup"><span data-stu-id="526b8-p104">If you leave the **Name** property unchanged, the old version remains on pages where it was added, which makes it unlikely that users will be aware that a new version of the add-in part is available. Also, when the add-in part is added to other pages, it is the new version that is added, so the same version of a SharePoint Add-in would have different add-in parts on different pages.</span></span>
 

 
<span data-ttu-id="526b8-p105">Sie können andere Hostwebkomponenten programmgesteuert bereitstellen, indem Sie einen Remoteereignisempfänger verwenden, den Sie im App-Manifest mit einem  [InstalledEventEndpoint](http://msdn.microsoft.com/library/af9f83d8-8325-3ede-d7b0-bb82c0445eb9%28Office.15%29.aspx)-Element registrieren. Sie sollten einen  [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx)-Empfänger verwenden, um Komponenten zu aktualisieren, die ursprünglich mit einem **InstalledEventEndpoint**-Empfänger bereitgestellt wurden. Weitere Informationen zu  [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx)-Empfängern finden Sie unter  [Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="526b8-p105">You can deploy other kinds of host web components programmatically using a remote event receiver that you register in the add-in manifest with an  [InstalledEventEndpoint](http://msdn.microsoft.com/library/af9f83d8-8325-3ede-d7b0-bb82c0445eb9%28Office.15%29.aspx) element. You should use an [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx) receiver to update components that were originally deployed with an **InstalledEventEndpoint** receiver. [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx) receivers are described in [Create a handler for the update event in SharePoint Add-ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins).</span></span>
 

 

## <a name="next-steps"></a><span data-ttu-id="526b8-126">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="526b8-126">Next steps</span></span>
<span data-ttu-id="526b8-127"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="526b8-127"></span></span>

<span data-ttu-id="526b8-128">Wechseln Sie zu  [Wichtige Schritte beim Aktualisieren eines Add-Ins](update-sharepoint-add-ins#MajorAppUpgradeSteps), oder rufen Sie direkt einen der folgenden Artikel auf, um zu erfahren, wie Sie die nächste Hauptkomponente Ihres SharePoint-Add-Ins aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="526b8-128">Go to  [Major steps in updating an add-in](update-sharepoint-add-ins#MajorAppUpgradeSteps), or go directly to one of the following articles to learn how to update the next major component of your SharePoint Add-in.</span></span>
 

 

-  [<span data-ttu-id="526b8-129">Aktualisieren von Add-In-Webkomponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="526b8-129">Update add-in web components in SharePoint</span></span>](update-add-in-web-components-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="526b8-130">Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="526b8-130">Create a handler for the update event in SharePoint Add-ins</span></span>](create-a-handler-for-the-update-event-in-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="526b8-131">Aktualisieren von Remotekomponenten in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="526b8-131">Update remote components in SharePoint Add-ins</span></span>](update-remote-components-in-sharepoint-add-ins)
    
 

## <a name="additional-resources"></a><span data-ttu-id="526b8-132">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="526b8-132">Additional resources</span></span>
<span data-ttu-id="526b8-133"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="526b8-133"></span></span>


-  [<span data-ttu-id="526b8-134">Aktualisieren von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="526b8-134">Update SharePoint Add-ins</span></span>](update-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="526b8-135">Hostwebs, Add-In-Webs und SharePoint-Komponenten in SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="526b8-135">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013)
    
 

