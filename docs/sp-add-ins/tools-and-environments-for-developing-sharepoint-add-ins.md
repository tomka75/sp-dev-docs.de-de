
# <a name="tools-and-environments-for-developing-sharepoint-add-ins"></a><span data-ttu-id="e3519-101">Tools und Umgebungen für die Entwicklung von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="e3519-101">Tools and environments for developing SharePoint Add-ins</span></span>
<span data-ttu-id="e3519-102">Erfahren Sie mehr über die Optionen zum Erstellen einer Entwicklungsumgebung für SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="e3519-102">Learn your options for creating a development environment for  spappplural.</span></span>
 

 <span data-ttu-id="e3519-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="e3519-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="e3519-106">Es gibt zwei grundlegende Muster für Entwicklungsumgebungen für SharePoint-Add-Ins:</span><span class="sxs-lookup"><span data-stu-id="e3519-106">There are two basic patterns for development environments for spappplural:</span></span>
 

-  <span data-ttu-id="e3519-p102">**Die SharePoint-Website für Test und Debugging ist in einer SharePoint Online-Website in einem Office 365-Abonnement enthalten.** Normalerweise wird Visual Studio auf einem lokalen Computer installiert, aber auch eine cloudbasierte Visual Studio-Installation ist eine Option.</span><span class="sxs-lookup"><span data-stu-id="e3519-p102">**The test and debugging SharePoint website is in a SharePoint Online website in an Office 365 subscription.** Typically, Visual Studio is installed to a local computer, but a cloud-based Visual Studio is also an option.</span></span>
    
 
-  <span data-ttu-id="e3519-p103">**Das Testen und Debuggen von SharePoint-Websites findet in einer lokalen SharePoint-Farm mit einem Server statt. ** Visual Studio ist auf demselben Computer installiert.</span><span class="sxs-lookup"><span data-stu-id="e3519-p103">**The test and debugging SharePoint website is on an on-premise, one-server SharePoint farm.** Visual Studio is installed on the same computer.</span></span>
    
 
<span data-ttu-id="e3519-111">Berücksichtigen Sie dabei Folgendes:</span><span class="sxs-lookup"><span data-stu-id="e3519-111">Consider the following:</span></span>
 

- <span data-ttu-id="e3519-p104">Nahezu jedes von Ihnen erstellte Add-In kann entweder an SharePoint Online oder lokale SharePoint-Farmen bereitgestellt werden, unabhängig davon, welche Art von Umgebung Sie verwenden. Allgemein gilt, dass Apps, die nicht an SharePoint Online bereitgestellt werden können, auch nicht damit entwickelt werden können. Beispiele: Add-Ins, die  [Vollzugriffberechtigungen](add-in-permissions-in-sharepoint-2013) benötigen, und Add-Ins, die das [besonders vertrauenswürdige Autorisierungssystem](creating-sharepoint-add-ins-that-use-high-trust-authorization) verwenden.</span><span class="sxs-lookup"><span data-stu-id="e3519-p104">Almost any add-in you create can be deployed to either SharePoint Online or to on-premise SharePoint farms, regardless of which type of environment you use. As a general rule, add-ins that cannot be deployed to SharePoint Online also cannot be developed with it. Examples: add-ins that require  [Full Control permissions](add-in-permissions-in-sharepoint-2013) and add-ins that use the [high-trust authorization system](creating-sharepoint-add-ins-that-use-high-trust-authorization).</span></span>
    
 
- <span data-ttu-id="e3519-115">Sie können sowohl von SharePoint gehostete als auch von einem Anbieter gehostete SharePoint-Add-Ins entwickeln, unabhängig davon, welche Art von Umgebung Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="e3519-115">You can develop both SharePoint-hosted and provider-hosted SharePoint Add-ins, regardless of which type of environment you use.</span></span>
    
 
- <span data-ttu-id="e3519-116">Sie können sowohl lokale als auch SharePoint Online-Testwebsites haben.</span><span class="sxs-lookup"><span data-stu-id="e3519-116">You can have both on-premise and SharePoint Online test sites.</span></span>
    
 
- <span data-ttu-id="e3519-117">Die beiden Optionen sind im Großen und Ganzen beide gleichermaßen problemlos einzurichten.</span><span class="sxs-lookup"><span data-stu-id="e3519-117">All things considered, the two options are equally easy to set up.</span></span>
    
 
 <span data-ttu-id="e3519-118">**Informationen zum Erstellen der SharePoint Online-Umgebung** mithilfe eines SharePoint Online-Abonnements finden Sie unter [Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement](create-a-developer-site-on-an-existing-office-365-subscription)</span><span class="sxs-lookup"><span data-stu-id="e3519-118">**To create the SharePoint Online environment** using an SharePoint Online subscription that you can use for development, see [Create a developer site on an existing Office 365 subscription. To create the on-premise environment, see Set up an on-premises development environment for SharePoint Add-ins](create-a-developer-site-on-an-existing-office-365-subscription).</span></span>
 
 <span data-ttu-id="e3519-119">**Informationen zum Erstellen der lokalen Umgebung** finden Sie unter [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="e3519-119">**To create the on-premise environment**, see [Set up an on-premises development environment for SharePoint Add-ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins).</span></span>
 

 <span data-ttu-id="e3519-p105">**Hinweis** Dieses Thema befasst sich nur mit Umgebungen für die Entwicklung von SharePoint-Add-Ins. Wenn Sie die Entwicklung von Farmlösungen planen, finden Sie weitere Informationen unter [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](http://msdn.microsoft.com/library/08e4e4e1-d960-43fa-85df-f3c279ed6927%28Office.15%29.aspx). Wenn Sie beide Arten von Entwicklung planen, beginnen Sie mit dem letzteren Artikel, und sehen Sie sich dann [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins) für weitere Schritte an, die für die Entwicklung von SharePoint-Add-Ins erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="e3519-p105">**Note** This topic is only concerned with environments for developing SharePoint Add-ins. If you plan to develop farm solutions, see  [Set up a general development environment for SharePoint](http://msdn.microsoft.com/library/08e4e4e1-d960-43fa-85df-f3c279ed6927%28Office.15%29.aspx). If you plan to do both kinds of development, start with the latter article, and then see  [Set up an on-premises development environment for SharePoint Add-ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins) for additional steps you need to develop SharePoint Add-ins.</span></span>
 


## <a name="other-tooling-information"></a><span data-ttu-id="e3519-123">Informationen zu anderen Tools</span><span class="sxs-lookup"><span data-stu-id="e3519-123">Other tooling information</span></span>

 
-  [<span data-ttu-id="e3519-124">Erstellen von SharePoint-Add-Ins in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e3519-124">Create SharePoint Add-ins in Visual Studio</span></span>](create-sharepoint-add-ins-in-visual-studio)
    
 

## <a name="additional-resources"></a><span data-ttu-id="e3519-125">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="e3519-125">Additional resources</span></span>
<span data-ttu-id="e3519-126"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e3519-126"></span></span>


-  [<span data-ttu-id="e3519-127">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="e3519-127">SharePoint Add-ins</span></span>](sharepoint-add-ins)
    
 

