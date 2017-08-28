
# <a name="update-remote-components-in-sharepoint-add-ins"></a><span data-ttu-id="6fcfe-101">Aktualisieren von Remotekomponenten in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="6fcfe-101">Update remote components in SharePoint Add-ins</span></span>
<span data-ttu-id="6fcfe-102">Aktualisieren Sie die Remotewebanwendungen und -datenbanken in einem SharePoint-Add-In.</span><span class="sxs-lookup"><span data-stu-id="6fcfe-102">Update the remote web applications and databases in a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="6fcfe-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="6fcfe-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="prerequisites-for-updating-the-remote-components-of-a-sharepoint-add-in"></a><span data-ttu-id="6fcfe-106">Voraussetzungen für die Aktualisierung der Remotekomponenten eines SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="6fcfe-106">Prerequisites for updating the remote components of a SharePoint Add-in</span></span>
<span data-ttu-id="6fcfe-107"><a name="Prerequistes"> </a></span><span class="sxs-lookup"><span data-stu-id="6fcfe-107"></span></span>

<span data-ttu-id="6fcfe-108">Kenntnisse des Themas [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins) und der darin aufgeführten erforderlichen Komponenten und Kernkonzepte.</span><span class="sxs-lookup"><span data-stu-id="6fcfe-108">Be familiar with  [Update SharePoint Add-ins](update-sharepoint-add-ins) and the prerequisites and core concepts listed in it.</span></span>
 

 

## <a name="update-remote-components"></a><span data-ttu-id="6fcfe-109">Aktualisieren von Remotekomponenten</span><span class="sxs-lookup"><span data-stu-id="6fcfe-109">Update remote components</span></span>
<span data-ttu-id="6fcfe-110"><a name="UpdateRemote"> </a></span><span class="sxs-lookup"><span data-stu-id="6fcfe-110"></span></span>

<span data-ttu-id="6fcfe-p102">Aufgrund der großen Unterschiede bei Plattformen und Mandantensystemen können zur Aktualisierung der Remotekomponenten größtenteils nur sehr allgemeine Hinweise gegeben werden. Die folgenden zwei Abschnitte bieten eine Orientierung.</span><span class="sxs-lookup"><span data-stu-id="6fcfe-p102">For the most part, only very general advice can be provided for updating the remote components because of the wide differences in platforms and tenancy systems. The following two sections provide some guidance.</span></span>
 

 

### <a name="update-remote-components-in-a-provider-hosted-add-in"></a><span data-ttu-id="6fcfe-113">Aktualisieren von Remotekomponenten in einem von einem Anbieter gehosteten Add-In</span><span class="sxs-lookup"><span data-stu-id="6fcfe-113">Update remote components in a provider-hosted add-in</span></span>
<span data-ttu-id="6fcfe-114"><a name="UpdateProviderHosted"> </a></span><span class="sxs-lookup"><span data-stu-id="6fcfe-114"></span></span>

<span data-ttu-id="6fcfe-p103">Bei einem vom Anbieter gehosteten SharePoint-Add-In aktualisieren Sie die Remotekomponenten mithilfe der für Updates bewährten Vorgehensweisen der Plattform, auf der die Komponenten gehostet werden. Ebenso wie die Remotekomponenten eines vom Anbieter gehosteten Add-Ins separat von der Installation des SharePoint-Add-Ins selbst installiert werden, werden sie auch separat aktualisiert. Hier einige Punkte, die berücksichtigt werden sollten:</span><span class="sxs-lookup"><span data-stu-id="6fcfe-p103">For a provider-hosted SharePoint Add-in, you update the remote components using the best update practices of the platform on which the components are hosted. Just as the remote components of a provider-hosted add-in are installed separately from the installation of the SharePoint Add-in itself, they are also updated separately. Some points to consider:</span></span>
 

 

- <span data-ttu-id="6fcfe-118">Die aktualisierten Remotekomponenten sollten weiterhin mit allen früheren Versionen des SharePoint-Add-Ins verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="6fcfe-118">The updated remote components should continue to work with all earlier versions of the SharePoint Add-in.</span></span>
    
 
- <span data-ttu-id="6fcfe-119">Wenn Sie für Ihre Remotekomponenten ein Mandantenisolationssystem implementiert haben, beachten Sie, dass unterschiedliche Mandanten möglicherweise mehrere Versionen Ihrer App verwenden. Außerdem können auf einem bestimmten Mandanten auf verschiedenen SharePoint-Websites sogar unterschiedliche Versionen installiert sein.</span><span class="sxs-lookup"><span data-stu-id="6fcfe-119">If you implemented a tenancy isolation system for your remote components, keep in mind that different tenants might be using multiple versions of your add-in, and a specific tenant might even have different versions installed on various SharePoint websites.</span></span>
    
 
<span data-ttu-id="6fcfe-p104">Für ein vom Anbieter gehostetes SharePoint-Add-In, das Microsoft Azure SQL-Datenbank oder SQL Server verwendet, gibt es mehrere Methoden zum Aktualisieren der Datenbank. Lesen Sie zum Einstieg  [Upgrade a Data-tier Application](http://msdn.microsoft.com/library/c117df94-f02b-403f-9383-ec5b3ac3763c.aspx).</span><span class="sxs-lookup"><span data-stu-id="6fcfe-p104">For a provider-hosted SharePoint Add-in that uses Microsoft Azure SQL Database or SQL Server, there are multiple methods for updating the database. To get started, see  [Upgrade a Data-tier Application](http://msdn.microsoft.com/library/c117df94-f02b-403f-9383-ec5b3ac3763c.aspx).</span></span>
 

 

## <a name="next-steps"></a><span data-ttu-id="6fcfe-122">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="6fcfe-122">Next steps</span></span>
<span data-ttu-id="6fcfe-123"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="6fcfe-123"></span></span>

<span data-ttu-id="6fcfe-124">Kehren Sie zu  [Wichtige Schritte beim Aktualisieren eines Add-Ins](update-sharepoint-add-ins#MajorAppUpgradeSteps) zurück, oder rufen Sie direkt einen der folgenden Artikel auf, um zu erfahren, wie Sie die nächste Hauptkomponente Ihres SharePoint-Add-Ins aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="6fcfe-124">Return to  [Major steps in updating an add-in](update-sharepoint-add-ins#MajorAppUpgradeSteps), or go directly to one of the following articles to learn how to update the next major component of your SharePoint Add-in.</span></span>
 

 

-  [<span data-ttu-id="6fcfe-125">Aktualisieren von Add-In-Webkomponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6fcfe-125">Update add-in web components in SharePoint</span></span>](update-add-in-web-components-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="6fcfe-126">Aktualisieren von Hostwebkomponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6fcfe-126">Update host web components in SharePoint</span></span>](update-host-web-components-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="6fcfe-127">Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="6fcfe-127">Create a handler for the update event in SharePoint Add-ins</span></span>](create-a-handler-for-the-update-event-in-sharepoint-add-ins)
    
 

## <a name="additional-resources"></a><span data-ttu-id="6fcfe-128">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6fcfe-128">Additional resources</span></span>
<span data-ttu-id="6fcfe-129"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6fcfe-129"></span></span>


-  [<span data-ttu-id="6fcfe-130">Aktualisieren von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="6fcfe-130">Update SharePoint Add-ins</span></span>](update-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="6fcfe-131">Aktualisierungsverfahren für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="6fcfe-131">SharePoint Add-ins update process</span></span>](sharepoint-add-ins-update-process)
    
 
