# <a name="add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="53851-101">Hinzufügen eines Workflows zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="53851-101">Add a workflow to a SharePoint-hosted SharePoint Add-in</span></span>
<span data-ttu-id="53851-102">Erfahren Sie, wie Sie einen Workflow in ein SharePoint-Add-In einschließen.</span><span class="sxs-lookup"><span data-stu-id="53851-102">Learn how to include a workflow in a spappsing.</span></span>
 

 <span data-ttu-id="53851-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="53851-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="53851-p102">Dies ist der sechste in einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins) und den vorherigen Artikeln in dieser Reihe vertraut:</span><span class="sxs-lookup"><span data-stu-id="53851-p102">Learn how to surface a remote web form in a SharePoint page in a provider-hosted SharePoint Add-in. This is the sixth in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="53851-108">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="53851-108">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="53851-109">Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="53851-109">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [<span data-ttu-id="53851-110">Hinzufügen von benutzerdefinierten Spalten zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="53851-110">Add custom columns to a SharePoint-hostedSharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in)
    
 
-  [<span data-ttu-id="53851-111">Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="53851-111">Add a custom content type to a SharePoint-hostedSharePoint Add-in</span></span>](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in)
    
 
-  [<span data-ttu-id="53851-112">Hinzufügen eines Webparts zu einer Seite in einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="53851-112">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in)
    
 

 <span data-ttu-id="53851-p103">**Hinweis** Wenn Sie diese Reihe zu von SharePoint gehosteten Add-Ins durchgearbeitet haben, haben Sie eine Visual Studio-Projektmappe, die Sie verwenden können, um mit diesem Thema fortzufahren. Sie können außerdem das Repository unter [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeWorkflow.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="53851-p103">**Note** If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeContentType.sln file.</span></span>
 

<span data-ttu-id="53851-115">In diesem Artikel fügen Sie einen Workflow zum SharePoint-Add-In „Orientierung für Mitarbeiter“ hinzu, der die Personalabteilung (HR) benachrichtigt, dass ein neuer Mitarbeiter bereit ist, die Personalpapiere auszufüllen.</span><span class="sxs-lookup"><span data-stu-id="53851-115">In this article you add a workflow the Employee Orientation spappsing that notifies the Human Resources (HR) department that a new employee is ready to fill out the HR paperwork.</span></span>
 

## <a name="add-a-workflow-to-an-add-in"></a><span data-ttu-id="53851-116">Hinzufügen eines Workflows zu einem Add-In</span><span class="sxs-lookup"><span data-stu-id="53851-116">Add  a workflow to an add-in</span></span>


 

 

1. <span data-ttu-id="53851-p104">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie **Hinzufügen** > **Neuer Ordner** aus. Nennen Sie den Ordner „Workflows“.</span><span class="sxs-lookup"><span data-stu-id="53851-p104">In  **Solution Explorer**, right-click the project and choose  **Add** > **New Folder**. Name the folder Workflows.</span></span>
    
 
2. <span data-ttu-id="53851-p105">Klicken Sie mit der rechten Maustaste auf den neuen Ordner, und wählen Sie **Hinzufügen** > **Neues Element** aus. Das Dialogfeld **Neues Element hinzufügen** wird mit dem Knoten **Office/SharePoint** geöffnet.</span><span class="sxs-lookup"><span data-stu-id="53851-p105">Right-click the new folder and choose **Add** > **New Item**. The **Add New Item** dialog opens to the **Office/SharePoint** node.</span></span>
    
 
3. <span data-ttu-id="53851-p106">Wählen Sie **Workflow** aus, und geben Sie dem Workflow den Namen „HR_Intake“. Wenn Sie aufgefordert werden, den Workflowtyp auszuwählen, wählen Sie **Listenworkflow** und dann **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="53851-p106">Choose Workflow and give it the name HR_Intake. When prompted to choose the type of workflow, choose List Workflow, and choose Next.</span></span>
    
 
4. <span data-ttu-id="53851-123">Aktivieren Sie auf der nächsten Seite des Assistenten die Option **Ja, Zuordnung durchführen...** aus, und legen Sie dann die Dropdownfelder auf die folgenden Werte fest:</span><span class="sxs-lookup"><span data-stu-id="53851-123">On the next page of the wizard, enable the **Yes, associate ... **option and then set the drop down controls to the following values:</span></span>
    
      -  <span data-ttu-id="53851-124">**Die Bibliothek oder Liste, der Ihr Workflow zugeordnet werden soll**</span><span class="sxs-lookup"><span data-stu-id="53851-124">**The library or list to associate your workflow with**</span></span>
    
    <span data-ttu-id="53851-125">Neue Mitarbeiter in Seattle</span><span class="sxs-lookup"><span data-stu-id="53851-125">New Employees in Seattle</span></span>
    
 
  -  <span data-ttu-id="53851-126">**Die Verlaufsliste...**</span><span class="sxs-lookup"><span data-stu-id="53851-126">**The history list ...**</span></span>
    
    <create new>
    
 
  -  <span data-ttu-id="53851-127">**Die Aufgabenliste...**</span><span class="sxs-lookup"><span data-stu-id="53851-127">**The Task list ...**</span></span>
    
    <create new>
    
 

    <span data-ttu-id="53851-128">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="53851-128">Click **Next**.</span></span>
    
 
5. <span data-ttu-id="53851-129">Aktivieren Sie auf der letzten Seite des Assistenten die Option zum automatischen Starten des Workflows *nur*, wenn ein Element *geändert* wird.</span><span class="sxs-lookup"><span data-stu-id="53851-129">On the last page of the wizard, enable *only* the option to start the workflow automatically when an item is *changed*.</span></span>
    
 
6. <span data-ttu-id="53851-130">Wählen Sie **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="53851-130">Choose **Finish**.</span></span>
    
    <span data-ttu-id="53851-131">Von den Office Developer Tools für Visual Studio wird Folgendes ausgeführt:</span><span class="sxs-lookup"><span data-stu-id="53851-131">The Office Developer Tools for Visual Studio will do the following:</span></span>
    
      - <span data-ttu-id="53851-132">Erstellen eines HR_Intake-Workflows im Ordner **Workflows** mit einer untergeordneten Workflow.xaml-Datei, die im Workflow-Designer geöffnet ist</span><span class="sxs-lookup"><span data-stu-id="53851-132">Create an HR_Intake workflow  in the **Workflow** folder, with a child Workflow.xaml file that is open in the workflow designer.</span></span>
    
 
  - <span data-ttu-id="53851-133">Erstellen einer **WorkflowTaskList**-Listeninstanz, in der Aufgaben, die Teil des Workflows sind, erstellt und aktualisiert werden</span><span class="sxs-lookup"><span data-stu-id="53851-133">Create a **WorkflowTaskList** list instance where tasks that are part of the workflow are created and updated.</span></span>
    
 
  - <span data-ttu-id="53851-134">Erstellen einer **WorkflowHistoryList**-Listeninstanz, die ein Protokoll der verschiedenen stattfindenden Schritte bei jeder Ausführung des Workflows ist</span><span class="sxs-lookup"><span data-stu-id="53851-134">Create a **WorkflowHistoryList** list instance, which is a log of the various steps in each execution of the workflow as they occur.</span></span>
    
 
7. <span data-ttu-id="53851-135">Ziehen Sie die zwei neuen Listeninstanzen in den Ordner **Listen**.</span><span class="sxs-lookup"><span data-stu-id="53851-135">Drag the two new list instances into the **Lists** folder.</span></span>
    
 

## <a name="design-the-workflow"></a><span data-ttu-id="53851-136">Entwerfen des Workflows</span><span class="sxs-lookup"><span data-stu-id="53851-136">Design the workflow</span></span>

<span data-ttu-id="53851-p107">Der Workflow sendet eine E-Mail, um einen Mitarbeiter der Personalabteilung zu benachrichtigen, dass der neue Mitarbeiter die Orientierungsphase der **Tour durch das Gebäude** abgeschlossen hat und zum Ausfüllen der Aufnahmepersonalpapiere bereit ist. Jede Änderung in einem vorhandenen Element auf der Liste „Neue Mitarbeiter in Seattle“ löst den Workflow aus, aber der Workflow führt keine Aktionen durch, bis das Feld „Orientierungsphase“ des Listenelements auf HR paperwork festgelegt wird. Dann wird eine E-Mail an einen Mitarbeiter der Personalabteilung gesendet und eine Aufgabe für diesen Mitarbeiter zur **WorkflowTaskList** hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="53851-p107">The workflow sends an email to notify an HR staffer that the new employee has finished the Tour of building stage of orientation and is ready to fill out the HR intake paperwork. Any change in an existing item on the New Employees in Seattle list triggers the workflow, but the workflow does nothing unless the Orientation Stage field of the list item is set to HR paperwork.  If it is, then an email is sent to an HR staffer and a task for that employee will be added to the WorkflowTaskList.</span></span> 
 

 

 <span data-ttu-id="53851-140">**Hinweis** An verschiedenen Punkten während des Entwerfens Ihres Workflows wird ein blaues Rautensymbol mit einem Ausrufezeichen</span><span class="sxs-lookup"><span data-stu-id="53851-140">**Note**  At various times when designing your workflow, a blue diamond symbol with an exclamation mark in it,</span></span> 
 
![Ein kleines blaues Rautensymbol mit einem weißen Ausrufezeichen darin.](../../images/f7b82a70-80fe-4e7e-a0f5-5a78cd12b367.PNG)
 
<span data-ttu-id="53851-p108">für ein oder mehrere Elemente im Workflow-Designer angezeigt. Diese weisen auf temporäre Fehler hin. (Bewegen Sie den Cursor über das Symbol, um eine kurze Meldung anzuzeigen, oder suchen Sie in der **Fehlerliste** von Visual Studio nach Details.) Hierbei handelt es sich um Nebeneffekte der Unvollständigkeit des Workflows. Diese sollten nicht mehr vorhanden sein, wenn Sie das Verfahren abgeschlossen haben.</span><span class="sxs-lookup"><span data-stu-id="53851-p108">At various times when designing your workflow, a blue diamond symbol with an exclamation mark in it, , will appear on one or more items in the workflow designer. These report temporary errors. (Hover the cursor over the symbol to see a brief message, or look in the Visual Studio **Error List** for details.) These are side effects of the incompleteness of the workflow. They should all be gone when you have finished this procedure.</span></span>
 


1. <span data-ttu-id="53851-146">Öffnen Sie den Bereich **Toolbox** in Visual Studio, erweitern Sie den Knoten **SP - Liste**, und ziehen Sie dann **LookupSPListItem** in die **Sequenz** im Designer.</span><span class="sxs-lookup"><span data-stu-id="53851-146">Open the Toolbox pane in vsnv, expand the  SP - List node, and then drag LookupSPListItem into the Sequence in the designer.</span></span>
    
 
2. <span data-ttu-id="53851-p109">Wählen Sie **LookupSPListItem** aus, um die Eigenschaften im Visual Studio-Bereich **Eigenschaften** anzuzeigen. Legen Sie die Eigenschaften auf die folgenden Werte fest:</span><span class="sxs-lookup"><span data-stu-id="53851-p109">Select the **LookupSPListItem** so that its properties appear in the Visual Studio **Properties** pane. Set the following properties to these values:</span></span>
    
      -  <span data-ttu-id="53851-149">**ItemID:** (aktuelles Element)</span><span class="sxs-lookup"><span data-stu-id="53851-149">**ItemId**: (current item)</span></span>
    
 
  -  <span data-ttu-id="53851-150">**ListID:** (aktuelle Liste)</span><span class="sxs-lookup"><span data-stu-id="53851-150">**ListId**: (current list)</span></span>
    
 
  -  <span data-ttu-id="53851-151">**DisplayName:** LookupCurrentNewEmployee</span><span class="sxs-lookup"><span data-stu-id="53851-151">**DisplayName:** LookupCurrentNewEmployee</span></span>
    
 

    <span data-ttu-id="53851-152">Der Bereich **Eigenschaften** sollte jetzt wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="53851-152">The **Properties** pane should now look like the following:</span></span>
    

    <span data-ttu-id="53851-153">**Eigenschaftenbereich von LookupSPListItem**</span><span class="sxs-lookup"><span data-stu-id="53851-153">**Properties pane of LookupSPListItem**</span></span>

 

  ![Eigenschaftenbereich der Workflowaktivität „Listenelement suchen“, wobei die Eigenschaften „ItemID“, „ListID“ und „DisplayName“ festgelegt sind.](../../images/60f3302e-ca9c-45be-b785-0c9f636181da.PNG)
 

    <span data-ttu-id="53851-155">Klicken Sie auf eine beliebige Stelle außerhalb des Bereichs, um die Änderungen zu speichern. Die Oberfläche des Designers sollte jetzt wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="53851-155">Click anywhere outside the pane to save your changes and the designer surface should now look like this.</span></span>
    

    <span data-ttu-id="53851-156">**Sequenz im Workflow-Designer**</span><span class="sxs-lookup"><span data-stu-id="53851-156">**Sequence in the workflow designer**</span></span>

 

  ![Workflow-Designer mit dem Feld „Sequenz“ und einer darin enthaltenen Aktivität mit dem Namen „Aktuellen neuen Mitarbeiter suchen“.](../../images/c8fbf801-e8e4-444a-9d2e-c14e29f537de.PNG)
 

    
    
 
3. <span data-ttu-id="53851-p110">Klicken Sie auf den Link **Eigenschaften abrufen** in der (neu umbenannten) Aktivität LookupCurrentNewEmployee im Designer. Dadurch wird eine **GetDynamicValueProperties**-Aktivität zur Sequenz hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="53851-p110">Click the Get Properties link inside the (newly renamed) LookupCurrentNewEmployee activity in the designer. This adds a GetDynamicValueProperties activity to the sequence.</span></span>
    
 
4. <span data-ttu-id="53851-p111">Klicken Sie auf den Text **Definieren...** in der Aktivität **GetDynamicValueProperties**. Damit wird das Dialogfeld **Eigenschaften** geöffnet.</span><span class="sxs-lookup"><span data-stu-id="53851-p111">Click the **Define…** text in the **GetDynamicValueProperties** activity. This will open the **Properties** dialog.</span></span>
    
 
5. <span data-ttu-id="53851-163">Legen Sie den **Entitätstyp** auf **Listenelement von** _Name_der_Listeninstanz_ fest, wobei _Name_der_Listeninstanz_ „Neue Mitarbeiter in Seattle“ ist.</span><span class="sxs-lookup"><span data-stu-id="53851-163">Set the Entity Type to List Item of  list_instance_name, where list_instance_name is New Employees in Seattle.</span></span>
    
 
6. <span data-ttu-id="53851-164">Klicken Sie in der Spalte **Pfad** auf die oberste Zelle, und wählen Sie dann „Orientierungsphase“ aus der Dropdownliste aus.</span><span class="sxs-lookup"><span data-stu-id="53851-164">In the **Path** column, click the top cell and then choose Orientation Stage from the drop down.</span></span>
    
 
7. <span data-ttu-id="53851-165">Klicken Sie auf die Zelle darunter, und wählen Sie dann **Title (Title)** aus der Dropdownliste aus.</span><span class="sxs-lookup"><span data-stu-id="53851-165">Click the cell below it and then choose **Title (Title)** from the drop down.</span></span>
    
 
8. <span data-ttu-id="53851-p112">Klicken Sie auf **Variablen auffüllen **. Damit werden die Variablen namens „OrientationStage“ und **Title** erstellt, und jeder wird der Wert der entsprechenden Felder im aktuellen Element der Liste „Neue Mitarbeiter in Seattle“ zugewiesen. Das Dialogfeld **Eigenschaften** sollte nun wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="53851-p112">Click **Populate Variables**. This will create a variables named OrientationStage and **Title** and assign each of the value of corresponding fields in the current item of the New Employees in Seattle list. The **Properties** dialog should now look like the following:</span></span>
    
    <span data-ttu-id="53851-169">**Dialogfeld „Eigenschaften“ der Workflowaktivität**</span><span class="sxs-lookup"><span data-stu-id="53851-169">**Properties dialog of workflow activity**</span></span>

 

  ![Das Dialogfeld "Eigenschaften" für die Aktivität "Dynamische Werte abrufen", wobei der Entitätstyp auf Elemente der Liste "Neue Mitarbeiter" festgelegt ist, und Variablen mit dem Namen "Title" und "OrientationStage", die Feldern mit dem gleichen Namen zugewiesen sind.](../../images/36a841e7-ce1b-444c-9bfe-7cdc56399ec1.PNG)
 

 

 
9. <span data-ttu-id="53851-p113">Wählen Sie **OK** aus. Die Designeroberfläche sollte jetzt wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="53851-p113">Choose **OK**. The designer surface should now look like the following:</span></span>
    
    <span data-ttu-id="53851-173">**Workflow-Designer**</span><span class="sxs-lookup"><span data-stu-id="53851-173">**Workflow Designer**</span></span>

 

  ![Der Workflow-Designer mit zwei Aktivitäten: „Listenelement suchen“ und „Dynamische Werte abrufen2.](../../images/cd8eb456-d883-491a-b171-38c1b9f64018.PNG)
 

    
    
 
10. <span data-ttu-id="53851-175">Öffnen Sie den Bereich **Toolbox** in Visual Studio, erweitern Sie den Knoten **Ablaufsteuerung**, und ziehen Sie dann **Wenn** in den unteren Bereich von **Sequenz** unterhalb von **GetDynamicValueProperties**.</span><span class="sxs-lookup"><span data-stu-id="53851-175">Open the Toolbox pane in vsnv, expand the Control Flow node, and then drag If into the bottom of the Sequence below the GetDynamicValueProperties.</span></span>
    
 
11. <span data-ttu-id="53851-176">Geben Sie in das Feld **Bedingung** von **Wenn** den Wert OrientationStage=="HR paperwork" ein.</span><span class="sxs-lookup"><span data-stu-id="53851-176">In the Condition box of the If, enter OrientationStage=="HR paperwork".</span></span>
    
 
12. <span data-ttu-id="53851-177">Öffnen Sie den Bereich **Toolbox** in Visual Studio, erweitern Sie den Knoten **SP - Hilfsprogramme**, und ziehen Sie dann **E-Mail** in das Feld **Dann** der **Wenn**-Aktivität.</span><span class="sxs-lookup"><span data-stu-id="53851-177">Open the Toolbox pane in vsnv, expand the  SP - Utilities node, and then drag Email into the Then box of the If activity.</span></span>
    
 
13. <span data-ttu-id="53851-p114">Wählen Sie die Aktivität **E-Mail** aus. Legen Sie im Bereich **Eigenschaften** die Werte für die Eigenschaften des Textkörpers, des Betreffs und der Option „An“ fest. Wählen Sie in jedem Fall die Popupschaltfläche **...** für die Eigenschaft aus, und verwenden Sie den sich öffnenden **Ausdrucks-Editor**, um den Wert der Eigenschaft wie in der folgenden Tabelle festzulegen. Da es sich dabei um C# Zeichenfolgenausdrücke handelt, verwenden Sie die Anführungszeichen exakt wie gezeigt. Der `Title` ist hier eine Variable, die Sie zuvor zum Feld **Title** des Listenelements zugewiesen haben (das den Namen des Mitarbeiters enthält).</span><span class="sxs-lookup"><span data-stu-id="53851-p114">Select the **Email** activity. In the **Properties** pane,  set the values of the Body, Subject, and To properties. In each case, choose the callout button, **. . .**, for the property and use the **Expression Editor** that opens to  set the property's value as in the following table. These are C# string expressions, so use quotation marks exactly as shown. The Title`Title` here is a variable that you assigned earlier to the **Title** field  of the list item (which holds the name of the employee).</span></span>
    
      -  <span data-ttu-id="53851-183">**Text:** `Title + " is waiting in the lobby to fill out benefits and employment forms."`</span><span class="sxs-lookup"><span data-stu-id="53851-183">body</span></span>
    
 
  -  <span data-ttu-id="53851-184">**Betreff:** `Title + " is ready for HR paperwork"`</span><span class="sxs-lookup"><span data-stu-id="53851-184">subject</span></span>
    
 
  -  <span data-ttu-id="53851-185">**An:** `new System.Collections.ObjectModel.Collection<string>() {"your_O365_email"}`</span><span class="sxs-lookup"><span data-stu-id="53851-185">**to** `new System.Collections.ObjectModel.Collection<string>() {"your_O365_email"}`</span></span>
    
    <span data-ttu-id="53851-p115">Ersetzen Sie den Platzhalter *your_O365_email* durch die Identität, mit der Sie sich bei Ihrem Office 365-Entwicklerkonto anmelden, z. B. *alias*  @ *O365domain* .sharepoint.com. Da es sich hier um eine C#-Zeichenfolge handelt, muss diese in Anführungszeichen eingeschlossen sein.</span><span class="sxs-lookup"><span data-stu-id="53851-p115">Replace the placeholder, your_O365_email, with the identity that you use to login to your Office 365 developer account, such as alias@O365domain.sharepoint.com. This is a C# string so it must be in quotation  marks.</span></span>
    
 
14. <span data-ttu-id="53851-188">Öffnen Sie den Bereich **Toolbox** in Visual Studio, erweitern Sie den Knoten **Runtime**, und ziehen Sie dann **TerminateWorkflow** in das Feld **Sonst** der **Wenn**-Aktivität.</span><span class="sxs-lookup"><span data-stu-id="53851-188">Open the Toolbox pane in vsnv, expand the Runtime node, and then drag TerminateWorkflow into the Else box of the If activity.</span></span>
    
 
15. <span data-ttu-id="53851-p116">Wählen Sie die Aktivität **TerminateWorkflow** aus, und legen Sie im Bereich **Eigenschaften** den **Grund** auf Folgendes fest, einschließlich der Anführungszeichen* : "Not at HR paperwork stage.". Der Designer sollte jetzt wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="53851-p116">Select the TerminateWorkflow activity and in the Properties pane, set the Reason to the following,  including the quotation marks: "Not at HR paperwork stage.". The designer should now look the following:</span></span>
    
    <span data-ttu-id="53851-191">**Workflow-Designer, wenn der Workflow abgeschlossen ist**</span><span class="sxs-lookup"><span data-stu-id="53851-191">**Workflow designer when the workflow is complete**</span></span>

 

  ![Der Workflow-Designer mit Aktivitäten für "Listenelement suchen", "Dynamischen Wert abrufen" und einer "Wenn-Dann-Sonst"-Struktur. E-Mail ist die Aktivität im Teil "Dann" und "Workflow beenden" ist die Aktivität für "Sonst".](../../images/c1230e3b-d149-413c-aa66-d258250a4512.PNG)
 

 

 

## <a name="run-and-test-the-add-in"></a><span data-ttu-id="53851-194">Ausführen und Testen des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="53851-194">Run and test the add-in</span></span>


 

 

1. <span data-ttu-id="53851-p118">Verwenden Sie die F5-TASTE, um das Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Website durch und führt das Add-In sofort aus. Die Konsole **Diensttesthost** des Workflow-Managers wird ebenfalls geöffnet.</span><span class="sxs-lookup"><span data-stu-id="53851-p118">Use the F5 key to deploy and run your add-in. vsnv makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in. The Workflow Manager's Test Service Host console also opens.</span></span>
    
 
2. <span data-ttu-id="53851-198">Wenn die Standardseite des Add-Ins geöffnet wird, öffnen Sie eins der Elemente zum Bearbeiten, und legen Sie den Wert von „Orientierungsphase“ auf HR paperwork fest.</span><span class="sxs-lookup"><span data-stu-id="53851-198">When the add-in's default page opens,  open one of the items for editing, and set the value of Orientation Stage to HR paperwork.</span></span> 
    
    <span data-ttu-id="53851-p119">In der Konsole **Diensttesthost** wird der Hinweis angezeigt, dass der Workflow gestartet wurde. Kurz danach wird der Hinweis angezeigt, dass der Workflow abgeschlossen ist. Im Folgenden sehen Sie ein Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53851-p119">In the **Test Service Host** console, an indication appears that the workflow has started. Shortly after, there is an indication that the workflow has completed. The following is an example:</span></span>
    

    <span data-ttu-id="53851-202">**Konsole „Diensttesthost“**</span><span class="sxs-lookup"><span data-stu-id="53851-202">**Service Test Host console**</span></span>

 

  ![Das Workflowfenster "Test Service Host" mit einer Zeile, die besagt, dass der Workflow gestartet wurde, gefolgt von einer Zeile, die besagt, dass der Workflow beendet wurde. Die GUID der Workflowinstanz befindet sich am Anfang jeder Zeile.](../../images/2422936d-7ef6-4c90-a03f-30053fbb9743.PNG)
 

    
    
    
     <span data-ttu-id="53851-p121">**Hinweis** Wenn die Konsole **Diensttesthost** nicht geöffnet wird, müssen Sie möglicherweise das Workflow-Debugging aktivieren. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Projektnamen, und wählen Sie **Eigenschaften** aus. Öffnen Sie im Bereich **Eigenschaften** die Registerkarte **SharePoint**, und aktivieren Sie das Kontrollkästchen **Workflow-Debugging aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="53851-p121">If the **Test Service Host** console does not open, you may need to enable workflow debugging. Right-click the project name in **Solution Explorer** and choose **Properties**. Open the **SharePoint** tab on the **Properties** pane and check the box for **Enable Workflow debugging**.</span></span>
3. <span data-ttu-id="53851-p122">Navigieren Sie zum E-Mail-Postfach (Outlook) Ihres Office 365-Entwicklerkontos. Dort finden Sie eine E-Mail mit dem Betreff „*Employee* is ready for HR paperwork“, wobei *Employee* der Name des Mitarbeiters ist, deren Element Sie bearbeitet haben. Im Textkörper der E-Mail steht: „*Employee* is waiting in the lobby to fill out benefits and employment forms.“ Im Folgenden sehen Sie ein Beispiel:</span><span class="sxs-lookup"><span data-stu-id="53851-p122">Navigate to the email inbox (Outlook) of your Office 365 developer account. There is an email with the subject "*Employee* is ready for HR paperwork." where *Employee* is the name of the employee whose item you edited. The body of the email says "*Employee* is waiting in the lobby to fill out benefits and employment forms." The following is an example:</span></span>
    
    <span data-ttu-id="53851-213">**Vom Workflow gesendete E-Mail**</span><span class="sxs-lookup"><span data-stu-id="53851-213">**Email sent by workflow**</span></span>

 

  ![Eine E-Mail-Nachricht in Outlook aus dem Workflow mit dem Betreff "Cassie Hicks ist bereit für die Schreibarbeiten der Personalabteilung" und dem Nachrichtentext "Cassie Hicks wartet in der Lobby, um Formulare für Zusatzleistungen und Dienstverhältnisse auszufüllen."](../../images/7b1d8f47-9c34-441e-af6a-3af4a8c65533.PNG)
 

    
    
    
     <span data-ttu-id="53851-p123">**Tipp** Wenn der Workflow gestartet, aber niemals abgeschlossen und die E-Mail nicht gesendet wird, versuchen Sie, die Debugsitzung zu beenden, und drücken Sie einige Male erneut F5, bevor Sie davon ausgehen, dass etwas in Ihrem Code nicht in Ordnung ist. Manchmal liegt das Problem bei SharePoint Online. Wenn weiterhin Probleme auftreten, versuchen Sie, einen Inhaltstyp namens **ListFieldsContentType**, falls dieser noch nicht vorhanden ist, zum Abschnitt **ContentTypes** der schema.xml-Datei hinzuzufügen. Das Folgende ist ein Beispiel für das Markup.`<ContentType ID="0x0100781dd48170b94fdc9706313c82b3d04c" Name="ListFieldsContentType" Hidden="TRUE">`</span><span class="sxs-lookup"><span data-stu-id="53851-p123">**Tip**  If the workflow begins but never completes, and the email is not sent, try ending the debugging session and trying F5 again a few times before you conclude there is something wrong in your code. Sometimes the problem is in SharePoint Online. If you are still having problems, try adding a content type called  **ListFieldsContentType**, if there isn't one already, to the  **ContentTypes** section of the schema.xml file. The following is an example of the markup. `<ContentType ID="0x0100781dd48170b94fdc9706313c82b3d04c" Name="ListFieldsContentType" Hidden="TRUE">`</span></span>
 
 <span data-ttu-id="53851-219">`</ContentType>`Kopieren Sie dann den gesamten Abschnitt **FieldRefs** des Inhaltstyps **NewEmployee** in diesen neuen Inhaltstyp. Speichern Sie das Projekt, ziehen Sie es zurück, und drücken Sie erneut F5.</span><span class="sxs-lookup"><span data-stu-id="53851-219">Then copy the whole of the **FieldRefs** section of the **NewEmployee** content type into this new content type.</span></span>
4. <span data-ttu-id="53851-p124">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.</span><span class="sxs-lookup"><span data-stu-id="53851-p124">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
5. <span data-ttu-id="53851-p125">Da Sie mit diesem Add-In und dieser Visual Studio-Projektmappe in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben. Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="53851-p125">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="53851-224"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="53851-224"></span></span>

<span data-ttu-id="53851-225">Im nächsten Artikel dieser Reihe fügen Sie eine benutzerdefinierte Seite und Formatvorlage zum SharePoint-Add-In hinzu: [Hinzufügen einer benutzerdefinierten Seite und Formatvorlage zu einem von SharePoint gehosteten SharePoint-Add-In](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in).</span><span class="sxs-lookup"><span data-stu-id="53851-225">In the next article in this series, you'll add  a custom page and style to the spappsing: Add a custom page and styles to a SharePoint-hosted Add-in.</span></span>
 

 

