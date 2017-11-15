---
title: Vorgehensweise Erstellen und POST von benutzerdefinierten Workflowaktionen
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 9d2fa681-30c2-4549-9df2-ea9ed757fda9
ms.openlocfilehash: 35ccb0313dc0a30b0308ff9ce1cc4eef988b8fae
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-build-and-deploy-workflow-custom-actions"></a><span data-ttu-id="30d1b-102">Vorgehensweise: Erstellen und POST von benutzerdefinierten Workflowaktionen</span><span class="sxs-lookup"><span data-stu-id="30d1b-102">How to: Build and deploy workflow custom actions</span></span>
<span data-ttu-id="30d1b-p101">In diesem Artikel erfahren Sie, wie Sie Geschäftsprozesse entwickeln, deren Anforderungen von der vorhandenen Bibliothek mit Workflowaktionen in SharePoint Designer nicht erfüllt werden, indem Sie benutzerdefinierte Workflowaktionen in SharePoint erstellen. SharePoint Designer enthält eine Auflistung von Workflowaktionen, die über die Workflow-Designer-Benutzeroberfläche (UI) verfügbar sind. Obwohl Bereich von Workflowaktionen, die in SharePoint Designer enthaltenen) ist umfassende, es ist jedoch begrenzt. In einigen Fällen müssen Sie einen Geschäftsprozess modellieren, deren nicht von der vorhandenen Workflowaktionen-Bibliothek erfüllt sind, die in SharePoint Designer verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="30d1b-p101">Learn how to model business processes whose requirements are not met by the existing library of workflow actions in SharePoint Designer by creating custom workflow actions in SharePoint. SharePoint Designer provides a collection of workflow actions that are available through the Workflow Designer user interface (UI). Although the range of workflow actions that are included in SharePoint Designer) is extensive, it is nevertheless finite. In some cases, you may need to model a business process whose requirements are not met by the existing library of workflow actions that are available in SharePoint Designer.</span></span>
  
    
    

<span data-ttu-id="30d1b-p102">Erkennen, dass Geschäftsprozesse häufig Anforderungen spezielle, können SharePoint Sie benutzerdefinierte Workflowaktionen erstellen. Entwickeln von benutzerdefinierten Aktionen mithilfe von Visual Studio, und klicken Sie dann zu packen, und stellen diese in SharePoint. An dieser Stelle wird die benutzerdefinierte Aktion für Autoren von Workflow in SharePoint Designer, genau wie wäre es zwischen der Bibliothek vorhandener Aktivitäten verfügbar. Diese Funktion können Sie die Funktionalität in Ihrer Umgebung der Workflow authoring keines der spezielle Geschäftsprozesse entsprechend anpassen.</span><span class="sxs-lookup"><span data-stu-id="30d1b-p102">Recognizing that business processes often have specialized requirements, SharePoint lets you create custom workflow actions. You can develop these custom actions by using Visual Studio, and then package and deploy them to SharePoint. At that point, the custom action becomes available to workflow authors in SharePoint Designer, exactly as if it were among the library of existing actions. This capability lets you customize the functionality in your workflow authoring environment to match any of your specialized business processes.</span></span>
> <span data-ttu-id="30d1b-111">**Hinweis:** Es wird ein Beispiel für das Erstellen einer benutzerdefinierten Aktion bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="30d1b-111">**Note:** A sample is provided that illustrates creating a custom action.</span></span> <span data-ttu-id="30d1b-112">Das Beispiel und eine Readme-Datei sind hier verfügbar:  [SharePoint-Workflow: Erstellen einer benutzerdefinierten Aktion](http://code.msdn.microsoft.com/SharePoint-workflow-41e5c0f9) (http://code.msdn.microsoft.com/SharePoint-workflow-41e5c0f9).</span><span class="sxs-lookup"><span data-stu-id="30d1b-112">The sample, along with a readme file, is available here:  SharePoint 2013 workflow: Create a custom action http://code.msdn.microsoft.com/SharePoint-2013-workflow-41e5c0f9 </span></span>
  
    
    


## <a name="core-scenario-for-custom-workflow-actions"></a><span data-ttu-id="30d1b-113">Kernszenario für benutzerdefinierte Workflowaktionen</span><span class="sxs-lookup"><span data-stu-id="30d1b-113">Core scenario for custom workflow actions</span></span>
<span data-ttu-id="30d1b-114"><a name="bk_corescenario"> </a></span><span class="sxs-lookup"><span data-stu-id="30d1b-114"></span></span>

<span data-ttu-id="30d1b-115">Das Core Szenario für benutzerdefinierte Workflowaktionen werden in der folgenden Zeile verbale erfasst:</span><span class="sxs-lookup"><span data-stu-id="30d1b-115">The core scenario for custom workflow actions is captured in the following narrative line:</span></span>
  
    
    

1. <span data-ttu-id="30d1b-p104">Business Analyst oder für andere technischen Information Worker ist SharePoint Designer verwenden, um einen Workflow, um einen internen Geschäftsprozess modellieren erstellen - beispielsweise eine Dokument-Genehmigungsprozess. Jedoch ist in das Unternehmen, der letzte Schritt des Prozesses, nach der endgültigen Genehmigung automatisch das Dokument auf eine externe Drucker senden, die gedruckt und bindet eine angegebene Anzahl von Kopien des Dokuments.</span><span class="sxs-lookup"><span data-stu-id="30d1b-p104">A business analyst or other non-technical information worker is using SharePoint Designer to author a workflow to model an internal business process—for example, a document-approval process. However, in this company, the final step of the process is, upon final approval, to automatically dispatch the document to an external printer who prints and binds a specified number of copies of the document.</span></span> 
    
  
2. <span data-ttu-id="30d1b-p105">Keine Workflowaktion, die in SharePoint Designer 2013 enthalten ist unterstützt ein Dokument an eine externe Drucker weiterleitet. Entscheiden daher Managern des Unternehmens investieren bei der Bereitstellung der benutzerdefinierten Aktion (sie rufen sie als die Aktion "Dateien zu Drucker senden") für das Unternehmen Information Worker.</span><span class="sxs-lookup"><span data-stu-id="30d1b-p105">No workflow action that is included in SharePoint Designer 2013 supports dispatching a document to an external printer. Therefore, the company managers decide to invest in providing this custom action (they call it the "Send Files to Printer" action) for the company's information workers.</span></span>
    
  
3. <span data-ttu-id="30d1b-120">Anbieter stellen Druck-Webdienste zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="30d1b-120">Vendors expose printing web services.</span></span> <span data-ttu-id="30d1b-121">Um davon zu profitieren, erstellt ein Entwickler eine benutzerdefinierte Aktion zum **Senden der Dateien an den Drucker** mit dem Namen **SendFilesToPrinter**.</span><span class="sxs-lookup"><span data-stu-id="30d1b-121">To capitalize, a developer creates a custom **Send Files to Printer** action, named **SendFilesToPrinter**.</span></span> <span data-ttu-id="30d1b-122">Der Entwickler erstellt hier eine deklarative Workflowaktivität.</span><span class="sxs-lookup"><span data-stu-id="30d1b-122">What the developer creates is a declarative workflow activity.</span></span> <span data-ttu-id="30d1b-123">Der Entwickler erstellt dann die Workflowaktion zum Bereitstellen der Drag & Drop-Benutzeroberfläche für die Aktion in SharePoint Designer.</span><span class="sxs-lookup"><span data-stu-id="30d1b-123">The developer also, then, creates the workflow action to provide the drag-and-drop UI for the action in SharePoint Designer.</span></span>
    
  
4. <span data-ttu-id="30d1b-124">Der Entwickler Pakete, die Aktivität **SendFilesToPrinter** und die **Dateien an Drucker senden** -Aktion in einer SharePoint-Lösungspaketdatei (.wsp) und als Websitesammlungs-Feature zur SharePoint-Farm bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="30d1b-124">The developer packages both the **SendFilesToPrinter** activity and the **Send Files to Printer** action in a SharePoint solution package (.wsp) file and deploys it as a site collection feature to the SharePoint farm.</span></span>
    
  
5. <span data-ttu-id="30d1b-125">Nachdem das Feature bereitgestellt und aktiviert ist, wird der Information Worker erhält die neue benutzerdefinierte Aktion, **Dateien an Drucker senden**, in der Benutzeroberfläche zusammen mit allen normalerweise Aktionen SharePoint Designer und es genau wie alle anderen verwenden kann.</span><span class="sxs-lookup"><span data-stu-id="30d1b-125">After the feature is deployed and activated, the information worker sees the new custom action, **Send Files to Printer**, in the SharePoint Designer UI along with all of the normally included actions and can use it just like all the others.</span></span>
    
  

## <a name="overview-of-custom-actions"></a><span data-ttu-id="30d1b-126">Übersicht über benutzerdefinierte Aktionen</span><span class="sxs-lookup"><span data-stu-id="30d1b-126">Overview of custom actions</span></span>
<span data-ttu-id="30d1b-127"><a name="bk_overviewcustact"> </a></span><span class="sxs-lookup"><span data-stu-id="30d1b-127"></span></span>

<span data-ttu-id="30d1b-p107">Eine Aktion ist ein Wrapper, der die Funktionalität der zugrunde liegenden Aktivität in SharePoint Designer abstrahiert. Zur Laufzeit wird die zugrunde liegende Aktivität, nicht die Aktion selbst, in der Windows Server AppFabric ausgeführt. In diesem Sinne sind Aktionen nur Entwurfszeit Abstraktionen der zugrunde liegenden Funktionen im SharePoint Designer Workflow authoring-Umgebung (zusätzlich zum werden Elemente der SharePoint Designer Schnittstelle verwenden.</span><span class="sxs-lookup"><span data-stu-id="30d1b-p107">An action is a wrapper that abstracts the functionality of its underlying activity in SharePoint Designer. At run time, the underlying activity, not the action itself, is executed in the Windows Server AppFabric. In this sense, actions are just design-time abstractions of underlying functions in the SharePoint Designer workflow authoring environment (in addition to being elements of the SharePoint Designer using interface.</span></span>
  
    
    
<span data-ttu-id="30d1b-131">Benutzerdefinierte Aktionen sind wie alle Aktionen "Webbereich" - d. h., sie werden auf der Ebene der SharePoint-Website oder **SharePoint.SPWeb** -Instanz aktiviert.</span><span class="sxs-lookup"><span data-stu-id="30d1b-131">Like all actions, custom actions are "web scoped"—that is, they are activated at the level of the SharePoint website, or **SharePoint.SPWeb** instance.</span></span>
  
    
    
<span data-ttu-id="30d1b-p108">Aktionen sind in XML-Definitionsdateien definiert, die die Erweiterung .actions4 aufweisen. Die zugrunde liegende Aktivität (oder Aktivitäten) sind andererseits, in eine XAML-Datei definiert.</span><span class="sxs-lookup"><span data-stu-id="30d1b-p108">Actions are defined in XML definition files that have the .actions4 file name extension. The underlying activity (or activities), on the other hand, are defined in a XAML file.</span></span>
  
    
    

## <a name="writing-custom-activities-in-visual-studio-2012"></a><span data-ttu-id="30d1b-134">Schreiben von benutzerdefinierten Aktivitäten in Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="30d1b-134">Writing custom activities in Visual Studio 2012</span></span>
<span data-ttu-id="30d1b-135"><a name="bk_writecustact"> </a></span><span class="sxs-lookup"><span data-stu-id="30d1b-135"></span></span>

<span data-ttu-id="30d1b-p109">Visual Studio 2012 bietet nun einen "benutzerdefinierten Workflowaktivität" Elementtyp innerhalb von SharePoint-Projekten. Den Elementtyp können Sie eine benutzerdefinierte Aktivität erstellen, die Sie als benutzerdefinierte Aktion in SharePoint Designer 2013 dann importieren können.</span><span class="sxs-lookup"><span data-stu-id="30d1b-p109">Visual Studio 2012 now provides a "workflow custom activity" item type within SharePoint projects. You can use the item type to create a custom activity that you can then import as a custom action in SharePoint Designer 2013.</span></span>
  
    
    

## <a name="example-create-package-and-deploy-a-custom-activity"></a><span data-ttu-id="30d1b-138">Beispiel:-Paket zu erstellen und Bereitstellen einer benutzerdefinierten Aktivitätsfeeds</span><span class="sxs-lookup"><span data-stu-id="30d1b-138">Example: Create, package, and deploy a custom activity</span></span>
<span data-ttu-id="30d1b-139"><a name="bk_createcustact"> </a></span><span class="sxs-lookup"><span data-stu-id="30d1b-139"></span></span>


### <a name="to-create-a-workflow-custom-activity"></a><span data-ttu-id="30d1b-140">Erstellen eine benutzerdefinierten Workflowaktivität</span><span class="sxs-lookup"><span data-stu-id="30d1b-140">To create a workflow custom activity</span></span>


1. <span data-ttu-id="30d1b-141">Beginnen Sie mit dem Visual Studio 2012 öffnen und erstellen ein neues Visual C#-Projekt vom Typ **SharePoint-Projekts**, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="30d1b-141">Begin by opening Visual Studio 2012 and creating a new Visual C# project of type **SharePoint Project**, as shown in Figure 1.</span></span>
    
   <span data-ttu-id="30d1b-142">**Abbildung 1. Dialogfeld "Neues Projekt"**</span><span class="sxs-lookup"><span data-stu-id="30d1b-142">**Figure 1. New Project dialog box**</span></span>

  

  ![Dialog "Neues Projekt"](../images/wfVS_NewProjectDialog.JPG)
  

  

  
2. <span data-ttu-id="30d1b-p110">Im **Projektmappen-Explorer** mit der rechten Maustaste in des Name-Projektknoten, und wählen Sie **Hinzufügen** und **Neues Element**. Daraufhin wird das Dialogfeld **Neues Element hinzufügen**, wie in Abbildung 2 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="30d1b-p110">In **Solution Explorer**, right-click the project name node, and choose **Add**, **New Item**. This opens the **Add New Item** dialog box, as shown in Figure 2.</span></span>
    
   <span data-ttu-id="30d1b-146">**Abbildung 2. Im Dialogfeld Neues Element hinzufügen**</span><span class="sxs-lookup"><span data-stu-id="30d1b-146">**Figure 2. Add New Item dialog box**</span></span>

  

  ![Dialogfeld "Neues Element"](../images/wfVS_NewItem.JPG)
  

    
    
  
3. <span data-ttu-id="30d1b-p111">Klicken Sie im Dialogfeld **Neues Element hinzufügen** wählen Sie den Elementtyp für **Benutzerdefinierte Workflowaktivität aus**, und weisen Sie ihr einen aussagekräftigen Namen. In der Abbildung ist der Name "WorkflowActionsModule1". Wählen Sie dann **Hinzufügen** aus. Das neue Element wird erstellt, und Sie werden mit der Entwurfsoberfläche Aktivität bearbeitet.</span><span class="sxs-lookup"><span data-stu-id="30d1b-p111">In the **Add New Item** dialog box, choose the **Workflow Custom Activity** item type and give it a meaningful name. In the illustration, the name is "WorkflowActionsModule1". Then choose **Add**. The new item is created, and you are presented with the activity design surface.</span></span>
    
  
4. <span data-ttu-id="30d1b-p112">Die **Toolbox**-Registerkarte nicht bereits angezeigt wird, klicken Sie darauf, um die Knoten Toolbox verfügbar zu machen. Klicken Sie auf der **SharePoint-Workflow**-Knoten, um den Workflow Development-Objekte anzuzeigen. Es wird eine partielle Ansicht der Objekte in der Workflowtoolbox in Abbildung 3.</span><span class="sxs-lookup"><span data-stu-id="30d1b-p112">If the **Toolbox** tab is not already showing, click it to expose the toolbox nodes. Click the **SharePoint Workflow** node to show the workflow development objects. There is a partial view of objects in the workflow toolbox in Figure 3.</span></span>
    
   <span data-ttu-id="30d1b-155">**Abbildung 3. Partielle Ansicht der SharePoint-Workflow-toolbox**</span><span class="sxs-lookup"><span data-stu-id="30d1b-155">**Figure 3. Partial view of SharePoint workflow toolbox**</span></span>

  

  ![Workflow-Toolbox](../images/wfVS_WorkflowToolbox.jpg)
  

    
    
  
5. <span data-ttu-id="30d1b-p113">Fügen Sie neue Aktion (.actions4) und Dateien des Vorgangs (XAML hinzu) Ihrem Workflow-Modul nach Bedarf. Um diese Dateien hinzuzufügen, mit der rechten Maustaste in des Symbols Aktionen Modul im **Projektmappen-Explorer**, wählen Sie **Hinzufügen** und wählen Sie dann nach Bedarf **Aktion hinzufügen** (zum Hinzufügen einer neuen action4-Datei) oder **Neue Aktivität** (um eine neue Aktivität hinzuzufügen).</span><span class="sxs-lookup"><span data-stu-id="30d1b-p113">Add new action (.actions4) and activity (.xaml) files to your workflow module, as needed. To add these files, right-click the actions module icon in **Solution Explorer**, choose **Add**, and then choose either **Add Action** (to add a new action4 file) or **New Activity** (to add a new activity), as appropriate.</span></span>
    
  
<span data-ttu-id="30d1b-p114">Nachdem Sie Ihre Aktionen Modul erstellen und der Aktion und der Aktivität Dateien hinzufügen, sollte Ihr Projekt etwa, abgebildeten in Abbildung 5 aussehen. Sie können eine .actions4-Datei für die einzelnen Aktionen, die Sie hinzugefügt und eine XAML-Datei für jede Aktivität werden angezeigt. Darüber hinaus müssen Sie eine Datei "Elements.xml" und das Modul XAML-Datei.</span><span class="sxs-lookup"><span data-stu-id="30d1b-p114">After you create your actions module and add your action and activity files, your project should look something like that depicted in Figure 5. You will see one .actions4 file for each action that you added, and one .xaml file for each activity. Additionally, you will have an Elements.xml file and the module's .xaml file.</span></span>
  
    
    

<span data-ttu-id="30d1b-162">**Abbildung 5. Workflow Aktionen Modul im Projektmappen-Explorer**</span><span class="sxs-lookup"><span data-stu-id="30d1b-162">**Figure 5. Workflow actions module in Solution Explorer**</span></span>

  
    
    

  
    
    
![Aktivitätsknoten im Projektmappen-Explorer](../images/wfVS_ActivityNode.jpg)
  
    
    
<span data-ttu-id="30d1b-p115">Nachdem Sie Ihre benutzerdefinierten Workflowaktivität erstellt haben, können Sie und klicken Sie dann zu packen und bereitstellen. Nach der Bereitstellung ist, kann die benutzerdefinierte Aktivität als benutzerdefinierte Aktion von SharePoint Designer 2013 genutzt werden.</span><span class="sxs-lookup"><span data-stu-id="30d1b-p115">After you create your custom workflow activity, you can then package and deploy it. After it is deployed, the custom activity can be consumed by SharePoint Designer 2013 as a custom action.</span></span>
  
    
    
<span data-ttu-id="30d1b-p116">Benutzerdefinierte Aktionen sind gepackt und als SharePoint-Features in SharePoint-Lösungspaket (.wsp) Lösungsdateien bereitgestellt. Das Lösungspaket enthält ein Modul benutzerdefinierte Aktionen, also eine Reihe von Dateien, die in SharePoint bereitgestellt werden. In diesem Modul kann eine beliebige Anzahl von Workflow-Aktivitäten-Definitionen enthalten, von denen jedes eine XAML-Datei ist. Das Modul enthält außerdem Aktionen (.actions4) Dateien. Jede Actions-Datei enthält mehrere Aktionen, die verweisen, um die Aktivitäten im Modul oder systemeigene Aktivitäten, die auf einer SharePoint-Standardinstallation verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="30d1b-p116">Custom actions are packaged and deployed as SharePoint Features in SharePoint solution package (.wsp) files. The solution package contains a custom actions module, which is a set of files that are deployed on SharePoint. This module can contain any number of workflow activity definitions, each of which is a .xaml file. The module also contains actions (.actions4) files. Each actions file contains multiple actions that refer to the activities in the module, or to native activities that are available on a default SharePoint installation.</span></span>
  
    
    
<span data-ttu-id="30d1b-p117">Nach eine Lösungspaketdatei (.wsp) hochgeladen und auf der Zielwebsite (d. h., die SharePoint-Websitesammlung) aktiviert ist, sind die Features, die im Paket enthalten sind, installiert und bereit zur Aktivierung. Nachdem die benutzerdefinierten Aktionen aktiviert sind, sind sie für die Verwendung in einem Workflow verfügbar.</span><span class="sxs-lookup"><span data-stu-id="30d1b-p117">After a solution package (.wsp) file is uploaded and activated on the target website (that is, the SharePoint site collection), the features that are contained in the package are installed and available for activation. After the custom actions are activated, they are available for use in a workflow.</span></span> 
  
    
    

## <a name="updating-and-deleting-custom-actions"></a><span data-ttu-id="30d1b-173">Aktualisieren und Löschen von benutzerdefinierten Aktionen</span><span class="sxs-lookup"><span data-stu-id="30d1b-173">Updating and deleting custom actions</span></span>
<span data-ttu-id="30d1b-174"><a name="bk_updatecustact"> </a></span><span class="sxs-lookup"><span data-stu-id="30d1b-174"></span></span>

<span data-ttu-id="30d1b-p118">Nach dem die benutzerdefinierte Aktion bereitgestellt wird, können Sie zu aktualisieren oder leicht zu entfernen. Haben Sie tun ist, öffnen Sie das Aktivitätsprojekt in Visual Studio, stellen Sie die Änderungen, die Sie möchten, und klicken Sie dann Verpacken und erneut bereitstellen, wie im vorherigen Verfahren beschrieben. Wenn die benutzerdefinierte Aktion entfernen möchten, können Sie einfach das Feature für die Ziel-Websitesammlung deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="30d1b-p118">After your custom action is deployed, you can update or remove it very easily. All you have to do is open the activity project in Visual Studio, make the changes that you want, and then package and redeploy as described in the preceding procedure. To remove the custom action, you can just uninstall the feature on the target site collection.</span></span>
  
    
    

### <a name="feature-activation"></a><span data-ttu-id="30d1b-178">Aktivierung des Features</span><span class="sxs-lookup"><span data-stu-id="30d1b-178">Feature activation</span></span>

<span data-ttu-id="30d1b-p119">Aktivieren ein benutzerdefiniertes Feature für eine Websitesammlung (d. h., in einer Instanz **SPWeb** ) nur erfolgreich, wenn die Azure / Workflow-Manager-Client 1.0 (mandantenfähigen Workflowmodul) ordnungsgemäß konfiguriert ist. Zwei Hinweise zur Problembehandlung, die dazu beitragen können eine korrekte Konfiguration umfassen:</span><span class="sxs-lookup"><span data-stu-id="30d1b-p119">Activating a custom action feature on a site collection (that is, on an **SPWeb** instance) succeeds only if the Azure/ Workflow Manager Client 1.0 (the multitenant workflow engine) is correctly configured. Two troubleshooting hints that may help ensure a correct configuration include:</span></span>
  
    
    

- <span data-ttu-id="30d1b-181">Aufrufen der Seite Websitefeatures und sicherstellen, dass das Feature mit der benutzerdefinierten Aktion aus aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="30d1b-181">Going to the Site Features page and ensuring that the feature that contains the custom action is activated.</span></span>
    
  
- <span data-ttu-id="30d1b-182">Abfragen der Workflow-Manager-Client 1.0-Datenbank, um sicherzustellen, dass die Aktivität erfolgreich bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="30d1b-182">Querying the Workflow Manager Client 1.0 database to ensure that the activity is successfully deployed.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="30d1b-183">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="30d1b-183">Additional resources</span></span>
<span data-ttu-id="30d1b-184"><a name="bk_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="30d1b-184"></span></span>


-  [<span data-ttu-id="30d1b-185">Grundlegendes zu SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="30d1b-185">SharePoint workflow fundamentals</span></span>](sharepoint-workflow-fundamentals.md)
    
  
-  [<span data-ttu-id="30d1b-186">Workflowaktions- und -aktivitätenreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="30d1b-186">Workflow actions and activities reference for SharePoint</span></span>](workflow-actions-and-activities-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="30d1b-187">Entwickeln von SharePoint-Workflows mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="30d1b-187">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio.md)
    
  

