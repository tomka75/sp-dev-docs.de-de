# <a name="create-a-cloud-business-add-in"></a><span data-ttu-id="0b421-101">Erstellen eines Cloud-Business-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="0b421-101">Create a cloud business add-in</span></span>
<span data-ttu-id="0b421-102">Mit der Cloud-Geschäfts-Add-In-Vorlage in Visual Studio können Sie Add-Ins für SharePoint oder SharePoint in Office 365 erstellen, die für das Hinzufügen und Verwalten von Daten optimiert sind.</span><span class="sxs-lookup"><span data-stu-id="0b421-102">By using the Cloud Business Add-in template in Visual Studio, you can create SharePoint Add-ins 2013 or SharePoint on Office 365 that are optimized for adding and managing data.</span></span>
 

 <span data-ttu-id="0b421-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="0b421-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


 <span data-ttu-id="0b421-106">**Hinweis** Sie können ein SharePoint-Add-In auch entwickeln, indem Sie die Vorlage für Add-Ins für SharePoint verwenden.</span><span class="sxs-lookup"><span data-stu-id="0b421-106">**Note** You can also build a SharePoint Add-in by using the Add-in for SharePoint template.</span></span>
 


### <a name="to-create-a-cloud-business-add-in"></a><span data-ttu-id="0b421-107">So erstellen Sie ein Cloud-Business-Add-In</span><span class="sxs-lookup"><span data-stu-id="0b421-107">To create a cloud business add-in</span></span>


1. <span data-ttu-id="0b421-108">Wählen Sie auf der Menüleiste die Optionen **Datei**, **Neu**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="0b421-108">On the menu bar, choose  **File**,  **New**,  **Project**.</span></span>
    
    <span data-ttu-id="0b421-109">Das Dialogfeld **Neues Projekt** wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="0b421-109">The  **New Project** dialog box opens.</span></span>
    
 
2. <span data-ttu-id="0b421-110">Erweitern Sie in der Vorlagenliste den Knoten **Visual Basic** oder **Visual C#**, dann den Knoten **Office/SharePoint**, klicken Sie auf den Knoten **Add-Ins** und dann auf **Cloud-Business-Add-In**, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="0b421-110">In the list of templates, expand the **Visual Basic** or **Visual C#** node, expand the **Office/SharePoint** node, choose the **Add-ins** node, and then choose **Cloud Business Add-in**, as shown in Figure 1.</span></span>
    
    <span data-ttu-id="0b421-111">**Abbildung 1. Vorlage für Cloud-Business-Add-Ins**</span><span class="sxs-lookup"><span data-stu-id="0b421-111">**Figure 1. Cloud Business Add-in template**</span></span>

 

  ![Vorlage zum Erstellen einer Cloud-Business-App](../../images/CloudBusinessApptemplate.PNG)
 

 

 
3. <span data-ttu-id="0b421-113">Geben Sie im Textfeld **Name** den Namen Ihres Projekts ein, und klicken Sie dann auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="0b421-113">In the **Name** text box, enter a name for your project, and then choose the **OK** button.</span></span>
    
    <span data-ttu-id="0b421-114">Der Assistent **Neues Cloud-Geschäfts-Add-In** wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="0b421-114">The **New Cloud Business Add-in** wizard opens.</span></span>
    
 
4. <span data-ttu-id="0b421-115">Geben Sie im Assistenten **Neues Cloud-Geschäfts-Add-In** die Website-URL für Ihren SharePoint-Server oder Ihre Office 365-Entwicklerwebsite ein, wie in Abbildung 2 dargestellt, und klicken Sie anschließend auf die Schaltfläche **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="0b421-115">In the **New Cloud Business Add-in** wizard, enter the Site URL for your SharePoint server or your Office 365 Developer site as shown in Figure 2, and then choose the **Finish** button.</span></span>
    
    <span data-ttu-id="0b421-116">**Abbildung 2. SharePoint-URL**</span><span class="sxs-lookup"><span data-stu-id="0b421-116">**Figure 2. SharePoint URL**</span></span>

 

  ![SharePoint-URL](../../images/SiteURL.PNG)
 

    <span data-ttu-id="0b421-118">Die URL sollte das Format „https://_MeineWebsite_.sharepoint.com/sites/Developer/“ haben.</span><span class="sxs-lookup"><span data-stu-id="0b421-118">The URL should take the form https://  _MySite_.sharepoint.com/sites/Developer/.</span></span>
    
    <span data-ttu-id="0b421-119">Dem Projektmappen-Explorer wurde eine neue Projektmappe mit vier Projekten hinzugefügt: ein Projekt auf oberster Ebene, ein **HTMLClient**-Projekt, ein **Server**-Projekt und ein **SharePoint**-Projekt.</span><span class="sxs-lookup"><span data-stu-id="0b421-119">A new solution is added to Solution Explorer with four projects: a top-level project, a **HTMLClient** project, a **Server** project, and a **SharePoint** project.</span></span>
    
 

### <a name="to-change-the-site-for-a-cloud-business-add-in"></a><span data-ttu-id="0b421-120">So ändern Sie die Website für ein Cloud-Business-Add-In</span><span class="sxs-lookup"><span data-stu-id="0b421-120">To change the site for a cloud business add-in</span></span>


1. <span data-ttu-id="0b421-121">Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü des Projektknotens auf oberster Ebene, und klicken Sie dann auf **Eigenschaften**, wie in Abbildung 3 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="0b421-121">In **Solution Explorer**, open the shortcut menu for the top-level project node and choose **Properties**, as shown in Figure 3.</span></span>
    
    <span data-ttu-id="0b421-122">**Abbildung 3. Der Projektknoten auf oberster Ebene**</span><span class="sxs-lookup"><span data-stu-id="0b421-122">**Figure 3. The top-level project node**</span></span>

 

  ![Der Projektknoten auf oberster Ebene](../../images/Top-levelprojectnode.PNG)
 

    <span data-ttu-id="0b421-124">Der Anwendungs-Designer wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="0b421-124">The application designer opens.</span></span>
    
 
2. <span data-ttu-id="0b421-125">Wählen Sie im Anwendungs-Designer die Registerkarte **SharePoint** aus, wie in Abbildung 4 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="0b421-125">In the application designer, choose the **SharePoint** tab as shown in Figure 4.</span></span>
    
    <span data-ttu-id="0b421-126">**Abbildung 4. Die Registerkarte „SharePoint“**</span><span class="sxs-lookup"><span data-stu-id="0b421-126">**Figure 4. The SharePoint tab**</span></span>

 

  ![Die SharePoint-Registerkarte „Eigenschaften“](../../images/SharePointtab.PNG)
 

 

 
3. <span data-ttu-id="0b421-128">Klicken Sie in der Liste **Website-URL** auf eine vorhandene URL, oder geben Sie die Website-URL Ihres SharePoint-Servers oder Ihrer Office 365-Entwicklerwebsite ein.</span><span class="sxs-lookup"><span data-stu-id="0b421-128">In the **Site URL** list, choose an existing URL or enter the Site URL for your SharePoint server or your Office 365 Developer site.</span></span>
    
 
4. <span data-ttu-id="0b421-129">Klicken Sie auf die Schaltfläche **Überprüfen**, um die URL zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="0b421-129">Choose the **Validate** button to verify the URL.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="0b421-130">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="0b421-130">Additional resources</span></span>
<span data-ttu-id="0b421-131"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="0b421-131"></span></span>


-  [<span data-ttu-id="0b421-132">Entwickeln von Cloud-Business-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="0b421-132">Develop cloud business add-ins</span></span>](develop-cloud-business-add-ins)
    
 
-  [<span data-ttu-id="0b421-133">Erstellen von Cloud-Business-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="0b421-133">Create cloud business add-ins</span></span>](create-cloud-business-add-ins)
    
 

