# <a name="associate-a-document-library-with-an-entity"></a><span data-ttu-id="363fe-101">Zuordnen einer Dokumentbibliothek zu einer Entität</span><span class="sxs-lookup"><span data-stu-id="363fe-101">Associate a document library with an entity</span></span>
<span data-ttu-id="363fe-p101">Mit dem Dokumentbibliothek-Feature in SharePoint können Sie mit einzelnen Elementen in einer Liste oder Entität verknüpfte Dokumente erstellen oder hochladen. Sie können beispielsweise eine Dokumentbibliothek zum Speichern von Vertriebsdokumentationen und Produkthandbüchern für jedes Produkt in einer Liste verwenden. In einem Cloud-Geschäfts-Add-In können Sie einer Dokumentbibliothek eine Entität zuordnen, indem Sie eine Beziehung erstellen.</span><span class="sxs-lookup"><span data-stu-id="363fe-p101">By using the document library feature in SharePoint, you can create or upload documents associated with individual items in a list or entity. For example, you might use a document library to store sales literature and product manuals for each product in a list. In a Cloud Business Add-in, you can associate a document library with an entity by creating a relationship.</span></span>
 

 <span data-ttu-id="363fe-p102">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="363fe-p102">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="associating-a-document-library"></a><span data-ttu-id="363fe-108">Zuordnen einer Dokumentbibliothek</span><span class="sxs-lookup"><span data-stu-id="363fe-108">Associating a Document Library</span></span>

<span data-ttu-id="363fe-109">Der Prozess zum Zuordnen einer Dokumentbibliothek umfasst drei Schritte:</span><span class="sxs-lookup"><span data-stu-id="363fe-109">The process of associating a document library with an entity involves three steps:</span></span>
 

 

1. <span data-ttu-id="363fe-110">Hinzufügen einer SharePoint-Dokumentbibliothek zu Ihrem Projekt als Datenquelle.</span><span class="sxs-lookup"><span data-stu-id="363fe-110">Add a SharePoint document library to your project as a data source.</span></span>
    
     <span data-ttu-id="363fe-p103">**Wichten** Sie müssen zunächst eine Dokumentbibliothek auf Ihrer SharePoint-Website erstellen. Sie muss eine benutzerdefinierte Spalte enthalten, die einem eindeutigen Feld in Ihrer Entität zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="363fe-p103">**Important** You must first create a document library on your SharePoint site. It must contain a custom column that maps to a unique field in your entity.</span></span>
2. <span data-ttu-id="363fe-113">Erstellen einer Beziehung zwischen der Dokumentbibliothek und einer Entität.</span><span class="sxs-lookup"><span data-stu-id="363fe-113">Create a relationship between the document library and an entity.</span></span>
    
 
3. <span data-ttu-id="363fe-p104">Fügen Sie die Dokumentbibliothek zu einem Bildschirm hinzu. Der Prozess unterscheidet sich, je nachdem, ob Sie einen neuen Bildschirm erstellen oder sie zu einem vorhandenen Bildschirm hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="363fe-p104">Add the document library to a screen. The process differs depending on whether you're creating a new screen or adding it to an existing screen.</span></span>
    
 

### <a name="to-add-a-document-library"></a><span data-ttu-id="363fe-116">So fügen Sie eine Dokumentbibliothek hinzu</span><span class="sxs-lookup"><span data-stu-id="363fe-116">To add a document library</span></span>


1. <span data-ttu-id="363fe-117">Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü des Knotens **Datenquellen**, und klicken Sie dann auf **Datenquelle hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="363fe-117">In **Solution Explorer**, open the shortcut menu for the **Data Sources** node and choose **Add Data Source**.</span></span>
    
 
2. <span data-ttu-id="363fe-118">Klicken Sie im **Assistenten zum Zuordnen von Datenquellen** auf das **SharePoint**-Symbol und anschließend auf die Schaltfläche **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="363fe-118">In the **Attach Data Source Wizard**, choose the **SharePoint** icon, and then choose the **Next** button.</span></span>
    
 
3. <span data-ttu-id="363fe-119">Geben Sie auf der Seite **Verbindungsinformationen eingeben** im Textfeld **Adresse der SharePoint-Website angeben** die URL Ihrer SharePoint-Entwicklerwebsite an, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="363fe-119">On the **Enter Connection Information** page, in the **Specify the SharePoint site address** text box, enter the URL for your SharePoint developer site, and then choose the **Next** button.</span></span>
    
 
4. <span data-ttu-id="363fe-120">Klicken Sie auf der Seite **SharePoint-Elemente auswählen** im linken Bereich auf das Listenelement **Dokumentbibliotheken**, und aktivieren Sie im rechten Bereich das Kontrollkästchen für Ihre Dokumentbibliothek, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="363fe-120">On the **Choose your SharePoint Items** page, in the left pane, choose the **Document Libraries** list item, and in the right pane, select the checkbox for your document library as shown in Figure 1.</span></span>
    
    <span data-ttu-id="363fe-121">**Abbildung 1. Auswählen der Dokumentbibliothek**</span><span class="sxs-lookup"><span data-stu-id="363fe-121">**Figure 1. Selecting the document library**</span></span>

 

  ![Auswählen der Dokumentbibliothek](../../images/CBADocLibrary.PNG)
 

    <span data-ttu-id="363fe-123">Abbildung 2 zeigt die Dokumentbibliothek auf der SharePoint-Website.</span><span class="sxs-lookup"><span data-stu-id="363fe-123">Figure 2 shows the document library on the SharePoint site.</span></span>
    

    <span data-ttu-id="363fe-124">**Abbildung 2. Beachten Sie die benutzerdefinierte Spalte „ProductName“**</span><span class="sxs-lookup"><span data-stu-id="363fe-124">**Figure 2. Note the custom ProductName column**</span></span>

 

  ![Dokumentbibliothek mit benutzerdefinierter Spalte „ProductName“](../../images/CBADocLibrary2.PNG)
 

    
     <span data-ttu-id="363fe-126">**Wichtig** Die Dokumentbibliothek muss bereits vorhanden sein und eine benutzerdefinierte Spalte enthalten, die einem eindeutigen Feld in Ihrer Entität zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="363fe-126">**Important** The document library must already exist and must contain a custom column that maps to a unique field in your entity.</span></span>
5. <span data-ttu-id="363fe-127">Geben Sie im Feld **Geben Sie den Namen der Datenquelle an** einen Namen ein, und klicken Sie dann auf die Schaltfläche **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="363fe-127">In the **Specify the name of the data source**, enter a name, and then choose the **Finish** button.</span></span>
    
 

### <a name="to-create-a-relationship"></a><span data-ttu-id="363fe-128">So erstellen Sie eine Beziehung</span><span class="sxs-lookup"><span data-stu-id="363fe-128">To create a relationship</span></span>


1. <span data-ttu-id="363fe-129">Öffnen Sie im **Projektmappen-Explorer** die Dokumentbibliothek-Entität, und klicken Sie dann auf der Leiste **Perspektive** auf die Registerkarte **Server**.</span><span class="sxs-lookup"><span data-stu-id="363fe-129">In **Solution Explorer**, open the document library entity, and then on the **Perspective** bar, choose the **Server** tab.</span></span>
    
 
2. <span data-ttu-id="363fe-130">Klicken Sie auf der Symbolleiste auf **Beziehung**.</span><span class="sxs-lookup"><span data-stu-id="363fe-130">On the toolbar, choose **Relationship**.</span></span>
    
 
3. <span data-ttu-id="363fe-131">Klicken Sie im Dialogfeld **Neue Beziehung hinzufügen** in der Dropdownliste **An** auf die Entität, die Sie zuordnen möchten, wie in Abbildung 3 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="363fe-131">In the **Add New Relationship** dialog box, in the **To** dropdown list, choose the entity that you want to associate, as shown in Figure 3.</span></span>
    
    <span data-ttu-id="363fe-132">**Abbildung 3. Erstellen einer Beziehung.**</span><span class="sxs-lookup"><span data-stu-id="363fe-132">**Figure 3. Creating a relationship.**</span></span>

 

  ![Erstellen einer Beziehung](../../images/CBARelationship.PNG)
 

 

 
4. <span data-ttu-id="363fe-134">Klicken Sie in der Dropdownliste **Fremdschlüssel** auf die benutzerdefinierte Spalte aus Ihrer Dokumentbibliothek.</span><span class="sxs-lookup"><span data-stu-id="363fe-134">In the **Foreign** key dropdown list, choose the custom column from your document library.</span></span>
    
 
5. <span data-ttu-id="363fe-p105">Klicken Sie in der Dropdownliste **Primärschlüssel** auf das Feld aus Ihrer Entität, das der benutzerdefinierten Spalte in der Dokumentbibliothek zugeordnet ist, und klicken Sie dann auf die Schaltfläche **OK**. Für die benutzerdefinierte Spalte „ProductName“ müssen Sie beispielsweise auf das Feld „ProductName“ klicken, wie in Abbildung 4 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="363fe-p105">In the **Primary** key dropdown list, choose the field from your entity that maps to the custom column in the document library, and then choose the **OK** button. For example, for a ProductName custom column, choose the ProductName field, as shown in Figure 4.</span></span>
    
    <span data-ttu-id="363fe-137">**Abbildung 4. Zusammengehöriger Fremdschlüssel und Primärschlüssel**</span><span class="sxs-lookup"><span data-stu-id="363fe-137">**Figure 4. Related foreign and primary keys**</span></span>

 

  ![Festlegen der zugehörigen Eigenschaften](../../images/CBARelationship2.PNG)
 

    
     <span data-ttu-id="363fe-139">**Hinweis** Das Feld muss den gleichen Datentyp aufweisen wie das Feld **Fremdschlüssel**.</span><span class="sxs-lookup"><span data-stu-id="363fe-139">**Note** The field must be of the same data type as the **Foreign** key field.</span></span>

### <a name="to-add-a-document-library-to-a-new-screen-set"></a><span data-ttu-id="363fe-140">So fügen Sie eine Dokumentbibliothek zu einer neuen Bildschirmgruppe hinzu</span><span class="sxs-lookup"><span data-stu-id="363fe-140">To add a document library to a new screen set</span></span>


1. <span data-ttu-id="363fe-141">Öffnen Sie im **Projektmappen-Explorer** die Entität, die der Dokumentbibliothek zugeordnet ist, und klicken Sie dann auf der Leiste **Perspektive** auf die Registerkarte **HTMLClient**.</span><span class="sxs-lookup"><span data-stu-id="363fe-141">In **Solution Explorer**, open the entity that is associated with a document library, and then on the **Perspective** bar, choose the **HTMLClient** tab.</span></span>
    
 
2. <span data-ttu-id="363fe-142">Klicken Sie auf der Symbolleiste auf **Bildschirm**.</span><span class="sxs-lookup"><span data-stu-id="363fe-142">On the toolbar, choose **Screen**.</span></span>
    
 
3. <span data-ttu-id="363fe-143">Geben Sie in dem Dialogfeld **Neuen Bildschirm hinzufügen** im Textfeld **Bildschirmgruppenname** einen Namen für die Bildschirmgruppe ein.</span><span class="sxs-lookup"><span data-stu-id="363fe-143">In the **Add New Screen** dialog box, in the **Screen Set Name** text box, enter a name for the screen set.</span></span>
    
 
4. <span data-ttu-id="363fe-144">Klicken Sie in der Liste **Bildschirmdaten** auf Ihre Entität.</span><span class="sxs-lookup"><span data-stu-id="363fe-144">In the **Screen Data** list, choose your entity.</span></span>
    
 
5. <span data-ttu-id="363fe-145">Aktivieren Sie in der Liste **Zusätzliche einzuschließende Daten** das Kontrollkästchen für Ihre Dokumentbibliothek, und klicken Sie dann auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="363fe-145">In the **Additional Data to Include** list, select the checkbox for your document library, and then choose the **OK** button.</span></span>
    
    <span data-ttu-id="363fe-146">Abbildung 5 zeigt eine Bildschirmgruppe für eine Produktentität.</span><span class="sxs-lookup"><span data-stu-id="363fe-146">Figure 5 shows a screen set for a Product entity.</span></span>
    

    <span data-ttu-id="363fe-147">**Abbildung 5. Produkt-Bildschirmgruppe**</span><span class="sxs-lookup"><span data-stu-id="363fe-147">**Figure 5. Products screen set**</span></span>

 

  ![Das Dialogfeld „Neuen Bildschirm hinzufügen“](../../images/CBAScreenSet.PNG)
 

    <span data-ttu-id="363fe-p106">Der für die Entität erstellte Bildschirm **Ansicht** enthält eine Registerkarte **Dokumente** mit einer Schaltfläche **Dokument hinzufügen**. Die Schaltfläche zeigt ein Popup zum Hinzufügen oder Hochladen von Dokumenten an.</span><span class="sxs-lookup"><span data-stu-id="363fe-p106">The **View** screen that is created for the entity contains a **Documents** tab with an **Add Document** button. The button displays a Popup for adding or uploading documents.</span></span>
    
 

### <a name="to-add-a-document-library-to-an-existing-screen"></a><span data-ttu-id="363fe-151">So fügen Sie eine Dokumentbibliothek zu einem vorhandenen Bildschirm hinzu</span><span class="sxs-lookup"><span data-stu-id="363fe-151">To add a document library to an existing screen</span></span>


1. <span data-ttu-id="363fe-152">Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü des Bildschirms, den Sie einer Dokumentbibliothek zuordnen möchten, und klicken Sie dann auf **Öffnen**.</span><span class="sxs-lookup"><span data-stu-id="363fe-152">In **Solution Explorer**, open the shortcut menu for the screen that you want to associate with a document library and choose **Open**.</span></span>
    
 
2. <span data-ttu-id="363fe-153">Klicken Sie im Bildschirm-Designer auf den Knoten **Registerkarten**, wie in Abbildung 6 dargestellt, und anschließend auf den Knoten **Registerkarte hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="363fe-153">In the screen designer, choose the **Tabs** node as shown in Figure 6, and then choose the **Add Tab** node.</span></span>
    
    <span data-ttu-id="363fe-154">**Abbildung 6. Der Knoten „Registerkarten“**</span><span class="sxs-lookup"><span data-stu-id="363fe-154">**Figure 6. The Tabs node**</span></span>

 

  ![Hinzufügen einer neuen Registerkarte](../../images/CBAAddTab.PNG)
 

 

 
3. <span data-ttu-id="363fe-p107">Klicken Sie im Fenster **Eigenschaften** auf die Eigenschaft **Anzeigename**, und geben Sie dann einen aussagekräftigen Namen für die neu hinzugefügte Registerkarte ein, z. B. „Dokumente“.</span><span class="sxs-lookup"><span data-stu-id="363fe-p107">In the **Properties** window, choose the **Display Name** property and enter a meaningful name for the newly added tab. For example,Documents.</span></span>
    
 
4. <span data-ttu-id="363fe-158">Klicken Sie im linken Bereich des Bildschirm-Designers auf den Link _DocumentLibraryName_ **hinzufügen**, wie in Abbildung 7 dargestellt, dabei ist _DocumentLibraryName_ der Name Ihrer Dokumentbibliothek.</span><span class="sxs-lookup"><span data-stu-id="363fe-158">In the left pane of the screen designer, choose the **Add** _DocumentLibraryName_ link as shown in Figure 7, where _DocumentLibraryName_ is the name of your document library.</span></span>
    
    <span data-ttu-id="363fe-159">**Abbildung 7. Der Link „ProductDocuments hinzufügen“**</span><span class="sxs-lookup"><span data-stu-id="363fe-159">**Figure 7. The Add ProductDocuments link**</span></span>

 

  ![Hinzufügen der Entität „Dokumente“](../../images/CBAAddDoc.PNG)
 

 

 
5. <span data-ttu-id="363fe-161">Klicken Sie im mittleren Bereich auf den Knoten der neuen Registerkarte, erweitern Sie die Liste **Hinzufügen**, und klicken Sie dann auf _DocumentLibraryName_.</span><span class="sxs-lookup"><span data-stu-id="363fe-161">In the center pane, choose the node for the new tab, expand the **Add** list, and then choose _DocumentLibraryName_.</span></span>
    
 
6. <span data-ttu-id="363fe-162">Erweitern Sie den Knoten **Befehlszeile** der neuen Registerkarte, wie in Abbildung 8 dargestellt, und klicken Sie dann auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="363fe-162">Expand the **Command Bar** node for the new tab as shown in Figure 8 and choose **Add**.</span></span>
    
    <span data-ttu-id="363fe-163">**Abbildung 8. Der Knoten „Befehlsleiste“**</span><span class="sxs-lookup"><span data-stu-id="363fe-163">**Figure 8. The Command Bar node**</span></span>

 

  ![Hinzufügen einer Schaltfläche](../../images/CBAAddButton.PNG)
 

 

 
7. <span data-ttu-id="363fe-165">Akzeptieren Sie im Dialogfeld **Schaltfläche hinzufügen** die Standardauswahlmöglichkeiten, und klicken Sie dann auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="363fe-165">In the **Add Button** dialog box, accept the default choices and choose the **OK** button.</span></span>
    
    <span data-ttu-id="363fe-166">In Abbildung 9 ist das Dialogfeld **Schaltfläche hinzufügen** mit der Standardmethode, **createOrUploadDocument**, dargestellt.</span><span class="sxs-lookup"><span data-stu-id="363fe-166">Figure 9 shows the **Add Button** dialog box with the default method, **createOrUploadDocument**.</span></span>
    

    <span data-ttu-id="363fe-167">**Abbildung 9: Das Dialogfeld „Schaltfläche hinzufügen“**</span><span class="sxs-lookup"><span data-stu-id="363fe-167">**Figure 9. The Add Button dialog box**</span></span>

 

  ![Das Dialogfeld „Schaltfläche hinzufügen“](../../images/CBAAddDialog.PNG)
 

 

 
8. <span data-ttu-id="363fe-p108">Klicken Sie im Fenster **Eigenschaften** auf die Eigenschaft **Anzeigename**, und geben Sie einen aussagekräftigen Namen für die Schaltfläche ein, z.. B. „Dokument hinzufügen“.</span><span class="sxs-lookup"><span data-stu-id="363fe-p108">In the **Properties** window, choose the **Display Name** property and enter a meaningful name for the button. For example,Add Document.</span></span>
    
    <span data-ttu-id="363fe-p109">Der Bildschirm enthält nun eine Registerkarte **Dokumente** mit einer Schaltfläche in der Befehlsleiste. Die Schaltfläche zeigt ein Popup zum Hinzufügen oder Hochladen von Dokumenten an.</span><span class="sxs-lookup"><span data-stu-id="363fe-p109">The screen now contains a **Documents** tab with a button on the command bar. The button displays a Popup for adding or uploading documents.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="363fe-173">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="363fe-173">Additional resources</span></span>
<span data-ttu-id="363fe-174"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="363fe-174"></span></span>


-  [<span data-ttu-id="363fe-175">Entwickeln von Cloud-Business-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="363fe-175">Develop cloud business add-ins</span></span>](develop-cloud-business-add-ins)
    
 
-  [<span data-ttu-id="363fe-176">Vorfallverwaltung: Lernprogramm für das Cloud-Business-Add-In</span><span class="sxs-lookup"><span data-stu-id="363fe-176">Incident manager: A cloud business add-in tutorial</span></span>](incident-manager-a-cloud-business-add-in-tutorial)
    
 

