---
title: Erstellen von SharePoint-Workflows mit Visual Studio
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 739af178-96b3-4630-bbc0-5def02065eeb
ms.openlocfilehash: a76d7c80cf48846b706a68b1a6b111901e478722
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="create-sharepoint-workflows-using-visual-studio"></a><span data-ttu-id="b0bef-102">Erstellen von SharePoint-Workflows mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b0bef-102">Create SharePoint workflows using Visual Studio</span></span>

<span data-ttu-id="b0bef-103">Erfahren Sie mehr über die Grundlagen des Erstellens eines SharePoint-Workflows auf der neuen SharePoint-Workflowplattform.</span><span class="sxs-lookup"><span data-stu-id="b0bef-103">Learn the basics of creating a SharePoint workflow in the new SharePoint workflow platform. Provided by:Andrew Connell,  AndrewConnell.com</span></span>

<span data-ttu-id="b0bef-104">**Bereitgestellt von:** [Andrew Connell](http://social.msdn.microsoft.com/profile/andrew%20connell%20%5bmvp%5d/), [www.AndrewConnell.com](http://www.andrewconnell.com)</span><span class="sxs-lookup"><span data-stu-id="b0bef-104">**Provided by:** [Andrew Connell](http://social.msdn.microsoft.com/profile/andrew%20connell%20%5bmvp%5d/),  [AndrewConnell.com](http://www.andrewconnell.com)</span></span>

> [!NOTE]
> <span data-ttu-id="b0bef-p101">Dieser Artikel enthält ein durchgängiges Codebeispiel, das Sie beim Folgen des Artikels oder als Grundlage für eigene SharePoint-Workflowprojekte verwenden können. Den herunterladbaren Code finden Sie hier: LINK.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p101">This article is accompanied by an end-to-end code sample that you can use to follow the article, or as a starter for your own SharePoint workflow projects. You can find the downloadable code here: LINK.</span></span> 
    
<span data-ttu-id="b0bef-p102">Microsoft hat in SharePoint einen ganz anderen Ansatz für Workflows umgesetzt als in früheren Versionen. SharePoint-Workflows basieren jetzt auf Windows Workflow Foundation 4, und ihre Ausführung wird von einer neuen Komponente namens Workflow-Manager gesteuert, die extern von SharePoint ausgeführt wird.Workflow-Manager übernimmt die Rolle als Host für die Windows Workflow Foundation-Runtime und alle erforderlichen Dienste in einer hoch verfügbaren und skalierbaren Weise. Er nutzt Service Bus für Leistung und Skalierbarkeit und wird bei Bereitstellung in einer lokalen Bereitstellung exakt auf dieselbe Weise ausgeführt wie bei einer Bereitstellung an einen Cloud-basierten Dienst wie Office 365, da er für die Weitergabe der gesamten Workflowausführung und zugehöriger Aufgaben an die Workflow-Manager-Farm konfiguriert ist.Die drastische Änderung in der Workflowarchitektur machte einige Änderungen an den beiden primären Workflowerstellungstools für das Erstellen von benutzerdefinierten Workflows - Visual Studio und SharePoint Designer - erforderlich. In diesem Artikel wird die Verwendung von Visual Studio 2012 als Workflowerstellungstool zum Erstellen benutzerdefinierter Workflows zur Verwendung in **sp15allshort** -Bereitstellungen dargestellt, sowohl für lokale als auch für Office 365-Bereitstellungen</span><span class="sxs-lookup"><span data-stu-id="b0bef-p102">Microsoft has taken a very different approach to workflows in SharePoint than in previous versions. SharePoint workflows are now based on Windows Workflow Foundation 4, and their execution is driven by a new component called Workflow Manager, which runs externally to SharePoint.Workflow Manager serves the role as host for the Windows Workflow Foundation runtime and all the necessary services in a highly available and scalable way. It leverages Service Bus for performance and scalability, and when deployed it runs exactly the same in an on-premises deployment as when deployed to a cloud-based service, such as Office 365, because it is configured to hand off all workflow execution and related tasks to the Workflow Manager farm.The dramatic change in the workflow architecture required some changes to the two primary workflow authoring tools for creating custom workflows - Visual Studio and SharePoint Designer. This article will explore using Visual Studio 2012 as your workflow authoring tool to create custom workflows for use in **sp15allshort** deployments - either on-premises or Office 365 deployments</span></span>

## <a name="types-of-workflows-in-visual-studio-2012"></a><span data-ttu-id="b0bef-111">Workflowtypen in Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="b0bef-111">Types of workflows in Visual Studio 2012</span></span>
<span data-ttu-id="b0bef-112"><a name="bm1"> </a></span><span class="sxs-lookup"><span data-stu-id="b0bef-112"></span></span>

<span data-ttu-id="b0bef-p103">Während SharePoint Designer 2013 nur Workflows erstellen kann, die aus Phasen bestehen, unterstützt Visual Studio einen anderen leistungsstarken Workflowtyp: den Zustandsautomatenworkflow. Effektiv unterstützen die Visual Studio 2012-Workflowentwicklungsumgebungen (und Visual Studio 2013) damit drei Arten der Workflowentwicklung: sequenziell, Flussdiagramm und Zustandsautomat.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p103">While SharePoint Designer 2013 can only create workflows comprised of stages, Visual Studio supports another powerful type of workflow: the state machine workflow. Effectively, then, the Visual Studio 2012 (and Visual Studio 2013) workflow development environments support three types of workflow authoring: sequential, flowchart, and state machine.</span></span>
  
    
    

### <a name="sequential"></a><span data-ttu-id="b0bef-115">Sequenziell</span><span class="sxs-lookup"><span data-stu-id="b0bef-115">Sequential</span></span>

<span data-ttu-id="b0bef-p104">Ein sequenzieller Workflow folgt einem bestimmten Pfad. Möglicherweise gibt es Entscheidungszweige und Schleifen oder der Workflow hat keinen Endpunkt, aber es ist einfach, dem vorhersagbaren Pfad im Entwurfsprozess zu folgen. Tatsächlich beginnen alle Workflows auf diese Weise, wenn Sie die Projektvorlage **Workflow** in Visual Studio verwenden.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p104">A sequential workflow is one that follows a specific path. There may be decision branches, loops, and the workflow may not have a termination point, but it is easy to follow the predictable path in the design process. In fact, is how all workflows start out when you are using the **Workflow** project template in Visual Studio.</span></span>
  
    
    
<span data-ttu-id="b0bef-p105">Ein sequenzieller Workflow enthält eine einzelne **Sequence**-Aktivität, in der eine beliebige Anzahl von Aktivitäten enthalten ist. Einige dieser Aktivitäten könnten weitere **Sequence**-Aktivitäten sein, die Sie verwenden, um eine Reihe kleinerer Schritte zu gruppieren.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p105">A sequential workflow contains a single **Sequence** activity and then any number of activities within it. Some of these could be other **Sequence** activities that you use to group together a series of smaller steps.</span></span>
  
    
    

### <a name="flowchart"></a><span data-ttu-id="b0bef-121">Flussdiagramm</span><span class="sxs-lookup"><span data-stu-id="b0bef-121">Flowchart</span></span>

<span data-ttu-id="b0bef-p106">Im Flowchartworkflow kann der Ausführungspfad gemäß den von Ihnen angegebenen Bedingungen in verschiedene Bereiche übergehen, wie in Abbildung 1 gezeigt. Die Flussdiagrammaktivität wird normalerweise zusammen mit der zugehörigen FlowDescision- und FlowSwitch-Aktivität in eine Sequence-Aktivität platziert und agiert entweder wie eine herkömmliche **if**-Aussage oder wie eine **switch**-Aussage in gängigen Programmiersprachen.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p106">In flowchart workflow, the execution pathway can transition to different sections of the workflow according to conditions that you specify, as shown in the Figure 1. The flowchart activity, along with the associated FlowDescision and FlowSwitch activity, are typically placed within a Sequence activity and act like either a traditional **if** statement, or like **switch** statement in common programming languages.</span></span>
  
    
    
<span data-ttu-id="b0bef-p107">Das Phasenkonstrukt in einem SharePoint Designer 2013-basierten Workflow basiert auf den Grundsätzen eines Flussdiagramms. Diese Arten von Workflows haben im Gegensatz zu einem sequenziellen Workflow keinen vorgeschriebenen Pfad, in dem sie folgen. Stattdessen bestimmen die Dinge, die während des Workflows geschehen den Pfad, dem der Workflow folgt.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p107">The stage construct within a SharePoint Designer 2013 based workflow is based on the principles of a flowchart. These types of workflows, unlike a sequential workflow, do not have a prescribed path in which they follow. Rather the things that happen during the workflow dictate the path the workflow follows.</span></span>
  
    
    

<span data-ttu-id="b0bef-127">**Abbildung 1: Flussdiagrammworkflow in Visual Studio 2012**</span><span class="sxs-lookup"><span data-stu-id="b0bef-127">**Figure 1. Flowchart workflow in Visual Studio 2012**</span></span>

  
    
    

  
    
    
![Abbildung 1. Flussdiagramm-Workflow](../images/ngWfFig01.png)
  
> [!NOTE]
> <span data-ttu-id="b0bef-130">Sie finden den in Abbildung 1 dargestellten Workflow als Workflowbeispiel hier auf MSDN:  [SharePoint: Genehmigungsworkflow, der ein benutzerdefiniertes Initiierungsformular verwendet](http://code.msdn.microsoft.com/officeapps/SharePoint-Approval-f5ac5eb2).</span><span class="sxs-lookup"><span data-stu-id="b0bef-130">Note: You can find the workflow depicted in Figure 1 as a workflow sample on MSDN here:  [SharePoint: Approval workflow that uses a custom initiation form](http://code.msdn.microsoft.com/officeapps/SharePoint-Approval-f5ac5eb2).</span></span> 
  
    
    


### <a name="state-machine"></a><span data-ttu-id="b0bef-131">Zustandsautomat</span><span class="sxs-lookup"><span data-stu-id="b0bef-131">State machine</span></span>

<span data-ttu-id="b0bef-p109">Zustandsautomatworkflows folgen normalerweise wie Flussdiagrammsorkflows keinem bestimmten Ausführungspfad. Stattdessen bestehen sie aus zwei oder mehr Zuständen, wie in Abbildung 2 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p109">State machine workflows, like flowchart workflows, do not typically follow a specific path of execution. Rather, they consist of two or more states as shown in Figure 2.</span></span> 
  
    
    

<span data-ttu-id="b0bef-134">**Abbildung 2: Zustandsautomatworkflow in Visual Studio 2012**</span><span class="sxs-lookup"><span data-stu-id="b0bef-134">**Figure 2. State machine workflow in Visual Studio 2012**</span></span>

  
    
    

  
    
    
![Abbildung 2. Zustandsautomat-Workflow](../images/ngWfFig02.png)
  
> [!NOTE]
> <span data-ttu-id="b0bef-137">Sie finden den in Abbildung 1 dargestellten Workflow als Workflowbeispiel hier auf MSDN:  [SharePoint: Von Aktionen und Ereignissen abhängiges Weiterleiten von Workflows zu Zuständen](http://code.msdn.microsoft.com/officeapps/SharePoint-Route-25a25d87).</span><span class="sxs-lookup"><span data-stu-id="b0bef-137">Note: You can find the workflow depicted in Figure 1 as a workflow sample on MSDN here:  [SharePoint: Route workflows to states depending on actions and events](http://code.msdn.microsoft.com/officeapps/SharePoint-Route-25a25d87).</span></span> 
  
    
    

<span data-ttu-id="b0bef-p111">Stellen Sie sich jeden Zustand als einen kleineren Workflow vor, der mehrere Workflowaktivitäten enthält. Sie können festlegen, dass bestimmte Aktivitäten gestartet werden, wenn der Workflow in einen bestimmten wechselt oder diesen verlässt. Was Zustandsautomatcomputer wirklich interessant macht, sind die Übergänge, die Sie definieren können. Jeder Zustand kann einen oder mehrere Übergänge haben, die dem Workflowmodul mitteilen, wie der Wechsel von einem Zustand zu einem anderen erfolgt.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p111">Think of each state as a smaller workflow that contains multiple workflow activities. You can set specific activities to start when the workflow enters or exits a given state. What really makes state machines interesting is the transitions that you can define. Each state can have one or more transitions that tell the workflow engine how to move from one state to another state.</span></span> 
  
    
    
<span data-ttu-id="b0bef-p112">Der Workflow ist immer in einem der Zustände in einen Zustandsautomatworkflow. Ein Übergang gibt den Auslöser für den Workflow zum Wechseln von einem Zustand in einen anderen vor. Viele ziehen Zustandsautomatworkflows den anderen Workflowtypen vor, da sie reale Geschäftsprozesse besser spiegeln können. Die Workflowtypen können jedoch schnell kompliziert werden.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p112">The workflow is always going to be in one of the states in a state machine workflow. A transition will dictate the trigger for the workflow to move from one state to another. Many people favor state machine workflows over the other types of workflows because they can be made to more closely mirror real world business processes. However these types of workflows can get complicated quickly.</span></span>
  
    
    

## <a name="visual-studio-2012-workflow-development-interface"></a><span data-ttu-id="b0bef-146">Oberfläche für die Workflowentwicklung in Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="b0bef-146">Visual Studio 2012 workflow development interface</span></span>
<span data-ttu-id="b0bef-147"><a name="bm2"> </a></span><span class="sxs-lookup"><span data-stu-id="b0bef-147"></span></span>

<span data-ttu-id="b0bef-p113">Beim Hinzufügen eines neuen Workflows zu einem SharePoint-Projekt fügt die Vorlage eine einzelne Sequenz-Aktivität hinzu, die als Hauptcontainer dient. Wenn Sie einen Flussdiagramm- oder Zustandsautomatworkflow erstellen möchten, löschen Sie diese Standardaktivität einfach und ziehen Sie eine StateMachine- oder Flowchart-Aktivität auf die Entwurfsoberfläche.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p113">When adding a new workflow to a SharePoint project, the template adds a single Sequence activity which serves as the main container. If you want to create a flowchart or state machine workflow simply delete this default activity and drag either a StateMachine or Flowchart activity onto the design surface.</span></span>
  
    
    
<span data-ttu-id="b0bef-p114">Vor dem Erstellen eines benutzerdefinierten Workflows sollten Entwickler ein gutes Verständnis für die Toolfenster und die Entwurfsoberfläche von Visual Studio 2012 haben. Viele der Elemente sind recht gängig, wie in Abbildung 3 dargestellt:</span><span class="sxs-lookup"><span data-stu-id="b0bef-p114">Before building a custom workflow, developers should have a good understanding on the tool windows and design surface that Visual Studio 2012 provides. Many of the elements are quite common, as shown in Figure 3:</span></span>
  
    
    

<span data-ttu-id="b0bef-152">**Abbildung 3: Oberfläche für die Erstellung von Workflows in Visual Studio 2012**</span><span class="sxs-lookup"><span data-stu-id="b0bef-152">**Figure 3. Visual Studio 2012 workflow authoring interface**</span></span>

  
    
    

  
    
    
![Abbildung 3. Oberfläche zur Workflowerstellung](../images/ngWfFig03.png)
  
    
    
<span data-ttu-id="b0bef-155">Die Oberfläche für die Workflowerstellung - d. h. der Workflow-Designer - verfügt über die folgenden wichtigen Elemente:</span><span class="sxs-lookup"><span data-stu-id="b0bef-155">The workflow development interface - that is, the workflow designer - has the following key elements:</span></span>
  
    
    

  
    
    

1. <span data-ttu-id="b0bef-156">**Projektmappen-Explorer**, in dem Ihr Projekt als Dateistruktur angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="b0bef-156">**Solution Explorer** displays your project as a file tree.</span></span>
    
  
2. <span data-ttu-id="b0bef-p116">**Workflow-Toolbox** mit allen Aktivitäten, aus denen Sie einen Workflow zusammensetzen können. Sie ziehen Sie per Drag and Drop aus der Toolbox auf die Designeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p116">**Workflow toolbox** contains all of the activities that you can use to assemble a workflow. You drag and drop from the toolbox to the designer surface.</span></span>
    
  
3. <span data-ttu-id="b0bef-159">**Workflow-Designeroberfläche**, in der Sie die Workflowelemente zusammenstellen und verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="b0bef-159">**Workflow designer surface** is where you assemble and link the workflow elements.</span></span>
    
  
4. <span data-ttu-id="b0bef-p117">**Eigenschaftenraster**, in dem die Eigenschaften einer ausgewählten Aktivität oder eines Elements im **Projektmappen-Explorer** angezeigt werden. Verwenden Sie diese Option zum Festlegen oder Ändern der Eigenschaftswerte.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p117">**Property grid** displays properties of a selected activity or item in **Solution Explorer**. Use this to set or change property values.</span></span>
    
  
5. <span data-ttu-id="b0bef-162">**Ausgabebereich**, in dem Informationen zu Aktivitätenelementen von Workflows angezeigt werden, z. B. Variablen, Argumente und Import.</span><span class="sxs-lookup"><span data-stu-id="b0bef-162">**Output pane** displays information about workflow activity elements - variables, arguments, and import.</span></span>
    
  
6. <span data-ttu-id="b0bef-163">**Registerkarten der Breadcrumb-Navigation**, die Ihnen ermöglichen, verschiedene Teile eines Workflows in der Entwicklungsphase ein- oder auszuzoomen.</span><span class="sxs-lookup"><span data-stu-id="b0bef-163">**Breadcrumb navigation tabs** allows you to zoom in and out on various portions of a workflow under development.</span></span>
    
  
<span data-ttu-id="b0bef-p118">Der **Ausgabebereich** (Nr. 5 in Abbildung 3) ist wichtig, da er Ihnen ermöglicht, alle Variablen in Ihrem Workflow im aktuellen Bereich anzuzeigen. Die Bereichsdefinition funktioniert genauso wie im objektorientierten Standardprogrammierungsentwurf: Eine Variable mit Bereichsdefinition im Stammverzeichnis ist für alle unteren Bereiche (wie Methoden innerhalb einer Klasse) zugänglich, aber eine Variable innerhalb eines niedrigeren Bereichs (wie eine Methode in einer Klasse) ist nur in diesem Bereich und dessen untergeordneten Bereichen, aber nicht in parallelen oder übergeordneten Bereichen zugänglich.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p118">The **Output pane** (#5 in Figure 3) is important because it allows you to see all of the variables in your workflow at the current scope. Scoping works the same way as it does in standard programming object oriented design: a variable scoped at the root is accessible to all lower scopes (such as methods within a class), but a variable within a lower scope (such as a method in a class) is only accessible within that scope and its children, but not parallel or parent scopes.</span></span>
  
    
    
<span data-ttu-id="b0bef-166">Klicken Sie auf die Registerkarte **Argumente**, um eine Liste der Argumente anzuzeigen, die verwendet werden, um Werte in den Workflow zu übergeben, z. B. von einem Initiierungsformular übergebene Werte.</span><span class="sxs-lookup"><span data-stu-id="b0bef-166">Click on the **Arguments** tab to see a list of the arguments that are used to pass values into the workflow, such as those passed from an initiation form.</span></span>
  
    
    

## <a name="how-to-create-a-custom-workflow"></a><span data-ttu-id="b0bef-167">So erstellen Sie einen benutzerdefinierten Workflow</span><span class="sxs-lookup"><span data-stu-id="b0bef-167">How to create a custom workflow</span></span>
<span data-ttu-id="b0bef-168"><a name="bm3"> </a></span><span class="sxs-lookup"><span data-stu-id="b0bef-168"></span></span>

<span data-ttu-id="b0bef-p119">Stellen Sie zum Erstellen eines benutzerdefinierten Workflows mithilfe von Visual Studio 2012 oder höher sicher, dass Sie Zugriff auf eine SharePoint-Entwicklerwebsite haben. In dieser exemplarischen Vorgehensweise wird empfohlen, dass Sie eine lokale SharePoint-Installation verwenden. Der Grund dafür ist, dass Workflows, die lokal getestet werden, mithilfe der **WriteLine**-Aktivität Debuginformationen an das Konsolenhilfsprogramm zum Testen des Diensthosts schreiben kann. Dieses Hilfsprogramm ist im Lieferumfang der Office Developer Tools für Visual Studio 2013 enthalten, die Teil der Standardinstallation von Visual Studio 2012 und höher in den Editionen Professional, Premium und Ultimate sind.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p119">To create a custom workflow using Visual Studio 2012 or later, ensure that you have access to a SharePoint developer site. For this walkthrough, it is recommended that you use a local SharePoint installation. This is because workflows tested locally can write debugging information to the Test Service Host console utility using the **WriteLine** activity. This utility is included with the Office Developer Tools for Visual Studio 2013, which are part of the default installation of Visual Studio 2012 and later in the Professional, Premium, and Ultimate editions.</span></span>
  
    
    

### <a name="create-a-new-app-project"></a><span data-ttu-id="b0bef-173">Erstellen eines neuen App-Projekts</span><span class="sxs-lookup"><span data-stu-id="b0bef-173">Create a new app project</span></span>


1. <span data-ttu-id="b0bef-174">Erstellen Sie in Visual Studio ein neues SharePoint-Add-Ins-Projekt, und konfigurieren Sie es als von SharePoint gehostete App.</span><span class="sxs-lookup"><span data-stu-id="b0bef-174">In Visual Studio, create a new SharePoint Add-ins project and configure it to be a SharePoint-hosted app.</span></span>
    
  
2. <span data-ttu-id="b0bef-p120">Fügen Sie in diesem Projekt eine neue **Announcement**-Listeninstanz. Wir verwenden diese Liste als Container für Elemente, die wir zum Testen des Workflows verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p120">In this project, add a new **Announcement** list instance. We use this list as a container for items that we are going to use to test the workflow.</span></span>
    
  
3. <span data-ttu-id="b0bef-177">Fügen Sie dem Projekt ein Workflowelement hinzu, indem Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projektsymbol klicken und anschließend auf **Hinzufügen** und **Neues Element** klicken.</span><span class="sxs-lookup"><span data-stu-id="b0bef-177">Add a workflow item to the project by right-clicking the project icon in **Solution Explorer** and selecting **Add**, then **New Item**.</span></span>
    
  
4. <span data-ttu-id="b0bef-p121">Wählen Sie im Dialogfeld **Neues Element hinzufügen** in der Kategorie **Office/SharePoint** das Projektelement **Workflow** aus, und nennen Sie es „Mein erster Workflow". Klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p121">In the **Add New Item** dialog box, select the **Workflow** project item from the **Office/SharePoint** category and name it "My First Workflow". Click **Next**.</span></span>
    
  
5. <span data-ttu-id="b0bef-p122">Wenn Sie vom **SharePoint-Anpassungs-Assistenten** aufgefordert werden, einen Namen einzugeben, behalten Sie den Standardwert bei, und legen Sie ihn dann auf einen **Listenworkflow** fest. Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p122">When prompted by the **SharePoint Customization Wizard** for a name, leave the default, then set it to be a **List Workflow**. Click **Next**.</span></span>
    
  
6. <span data-ttu-id="b0bef-182">Aktivieren Sie auf der nächsten Seite des Assistenten das Kontrollkästchen zum Erstellen einer Zuordnung, und wählen Sie dann die soeben erstellte Liste **Announcements** aus. Wählen Sie **<Create New>** für den erforderlichen Workflowverlauf und die Aufgabenliste aus, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="b0bef-182">On the next page of the wizard, check the box to create an association, then select the **Announcements** list that we just created; select **<Create New>** for the required workflow history and task lists and then click **Next**.</span></span>
    
  
7. <span data-ttu-id="b0bef-p123">Aktivieren Sie auf der letzten Seite des Assistenten das Kontrollkästchen zum manuellen Starten des Workflows, lassen die beiden Optionen für den automatischen Start deaktiviert, und klicken Sie dann auf **Fertig stellen**. Visual Studio fügt automatisch die erforderlichen Elemente zum Projekt hinzu und lädt die Datei „Workflow.xaml" in den Designer, wie in Abbildung 4 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p123">On the final page of the wizard, check the box to start the workflow manually, leaving the two automatic start options unchecked; then click **Finish**. Visual Studio automatically adds the required elements to the project and loads the Workflow.xaml file into the designer, as shown in Figure 4.</span></span>
    
   <span data-ttu-id="b0bef-185">**Abbildung 4: Standard-Designeroberfläche nach Hinzufügen des Workflowelements**</span><span class="sxs-lookup"><span data-stu-id="b0bef-185">**Figure 4. Default designer surface after adding the workflow item**</span></span>

  

  ![Abbildung 4. Standarddesigneroberfläche](../images/ngWfFig04.png)
  

  

  

### <a name="organize-workflow-steps"></a><span data-ttu-id="b0bef-188">Organisieren von Workflowschritten</span><span class="sxs-lookup"><span data-stu-id="b0bef-188">Organize workflow steps</span></span>

<span data-ttu-id="b0bef-p125">Um einen bestimmten Geschäftsprozess zu automatisieren, können Workflows eine beliebige Anzahl von Aktivitäten enthalten, die Sie in einem Schritt oder einer **Sequenz** gruppieren. Wenn Sie jedoch zu viele dieser Aktivitäten in einer einzigen **Sequenz** gruppieren, wird der Workflow unübersichtlich und schwer zu folgen und zu debuggen. Das ist ganz ähnlich wie in einer üblichen Programmiersprache davon abgeraten wird, extrem lange und komplexe Methoden zu erstellen. Stattdessen sollten Sie Aktivitäten gruppieren, die zusammenarbeiten, um eine bestimmte Aufgabe in einer gängigen Sequenz durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p125">To automate a given business process, workflows can contain any number of activities that you group together into a step, or **Sequence**. However, if you group too many of these activities in a single **Sequence**, the workflow becomes cluttered and difficult to follow and debug. This is similar to how in a common programming language it is ill-advised to create extremely long and complex methods. Instead, you should group activities that work together to perform a specific task in a common sequence.</span></span>
  
    
    
<span data-ttu-id="b0bef-p126">Dieses Workflowbeispiel veranschaulicht die Methode der Segmentierung Ihrer Workflows. Fügen Sie in Ihrem neuen Projekt auf der Designeroberfläche der vorhandenen Sequence-Standardaktivität zwei neue Sequence-Aktivitäten hinzu, und nennen Sie sie in „Untergeordnete Sequenz 1" und „Untergeordnete Sequenz 2" um, wie in Abbildung 5 dargestellt. Ändern Sie außerdem den Namen der ursprünglichen Sequence-Aktivität zu „Root" (was jedoch nicht in Abbildung 5 gezeigt ist).</span><span class="sxs-lookup"><span data-stu-id="b0bef-p126">This workflow sample will illustrate this practice of segmenting your workflows. In your new project, on the designer surface, to the existing default Sequence activity, add two new Sequence activities and rename them "Child Sequence 1" and Child Sequence 2", as depicted in Figure 5. Also (though not shown in Figure 5), change the name of the original Sequence activity to "Root".</span></span>
  
    
    

<span data-ttu-id="b0bef-196">**Abbildung 5: Hinzufügen von untergeordneten Sequenzen zur Standard- oder Rootsequenz**</span><span class="sxs-lookup"><span data-stu-id="b0bef-196">**Figure 5. Adding child sequences to the default, or root, sequence**</span></span>

  
    
    

  
    
    
![Abbildung 5. Hinzufügen untergeordneter Sequenzen](../images/ngWfFig05.png)
  
    
    

  
    
    

  
    
    

### <a name="comment-your-workflow-using-annotations"></a><span data-ttu-id="b0bef-199">Kommentieren des Workflows mithilfe von Anmerkungen</span><span class="sxs-lookup"><span data-stu-id="b0bef-199">Comment your workflow using annotations</span></span>

<span data-ttu-id="b0bef-p128">Bei Verwendung einer gängigen Programmiersprache wie C#, VB.NET oder C++ können Sie Ihren Code mithilfe der entsprechenden Kommentarbezeichner kommentieren. Das Kommentieren von Code ist wichtig für das Testen und Verwalten einer Codebasis. Nun, mit Visual Studio können Sie Ihre Workflowentwicklung auch mit einer Funktion namens **annotations** kommentieren.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p128">When using a common programming language like C#, VB.NET, or C++, you can comment your code by using appropriate comment specifiers. Commenting code is important for testing and maintaining a code base. Well, Visual Studio allows you also comment your workflow development by providing a feature called **annotations**.</span></span>
  
    
    
<span data-ttu-id="b0bef-p129">Sie können eine bestimmte Workflowaktivität kommentieren, indem Sie die Aktivität auswählen und dann **Anmerkungen** und **Anmerkung hinzufügen** auswählen. Ein kleines Symbol mit invertierten Chevrons rechts neben der Titelleiste der Aktivität signalisiert, dass eine Anmerkung vorhanden ist. Zeigen oder klicken Sie auf das Symbol, um die Meldung anzuzeigen (siehe Abbildung 6). Sie haben die Möglichkeit, die Anmerkung an die Aktivität anzuheften, damit sie immer sichtbar ist, wie in Abbildung 6 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p129">You can comment a given workflow activity by selecting the activity, the selecting **Annotations**, then **Add Annotation**. A small icon of inverted chevrons on the right side of the activity's title bar signals that it has an annotation. Hover over or click on the icon to see the message (shown in Figure 6). You have the option to pin the annotation to the activity so it is always visible, as shown in Figure 6.</span></span> 
  
    
    

<span data-ttu-id="b0bef-207">**Abbildung 6: Anmerkung zu einer Aktivität**</span><span class="sxs-lookup"><span data-stu-id="b0bef-207">**Figure 6. Annotation on an activity**</span></span>

  
    
    

  
    
    
![Abbildung 6. Anmerkung zu einer Aktivität](../images/ngWfFig06.png)
  
    
    

  
    
    

  
    
    

### <a name="obtain-values-from-list-items"></a><span data-ttu-id="b0bef-210">Abrufen von Werten aus Listenelementen</span><span class="sxs-lookup"><span data-stu-id="b0bef-210">Obtain values from list items</span></span>

<span data-ttu-id="b0bef-p131">Eine häufige Aufgabe, der Sie beim Erstellen von Workflows begegnen, ist das Abrufen von Eigenschaften eines Listenelements. Um diese Aufgabe auszuführen, verwenden Sie die Aktivität **LookupSPListItem**. Diese Aktivität für über die SharePoint-REST-API einen Webdienstaufruf durch, um Informationen für das Listenelement zu suchen. Das folgende Verfahren zeigt, wie das geht:</span><span class="sxs-lookup"><span data-stu-id="b0bef-p131">A common task you will encounter when creating workflows is getting properties of a list item. To accomplish this task, use the **LookupSPListItem** activity. What this activity does is make a web service call using the SharePoint REST API to lookup information on the list item. The following procedure shows how to do this:</span></span>
  
    
    
<span data-ttu-id="b0bef-215">Ziehen Sie zunächst eine **LookupSPListItem**-Aktivität aus der Toolbox, und legen Sie es sie in der Aktivität **Untergeordnete Sequenz 1** ab.</span><span class="sxs-lookup"><span data-stu-id="b0bef-215">First, drag a **LookupSPListItem** activity from the toolbox and drop it in the **Child Sequence 1** activity.</span></span>
  
    
    
<span data-ttu-id="b0bef-p132">Nach dem Hinzufügen der Aktivität zum Designer müssen Sie einige Eigenschaften festlegen: **ListId** und **ItemId**. Diese Eigenschaften können so festgelegt werden, dass sie Informationen in einer beliebigen Liste suchen, aber mit den Verknüpfungen für **Aktuelle Liste** und **Aktuelles Element** weisen Sie Workflow-Manager an, diese Werte automatisch herauszufinden.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p132">After adding the activity to the designer, you have to set a couple of properties: **ListId** and **ItemId**. These properties can be set to lookup information in any list, but using the shortcuts for **current list** and **current item** tell Workflow Manager to figure these values out automatically.</span></span>
  
    
    
<span data-ttu-id="b0bef-p133">Da wir einen Webdienstaufruf vornehmen, ist der Rückgabewert aus dieser Aktivität, der in der **Result**-Eigenschaft dargestellt ist, vom Typ **DynamicValue**. Aus diesem Grund benötigen wir eine Variable dieses Datentyps zum Speichern der Ausgabe des Webdienstaufrufs. Dies ist ziemlich einfach, da ein großer Teil davon durch Klicken auf den Link **Eigenschaften abrufen** in der **LookupSPListItem**-Aktivität automatisch durchführt:</span><span class="sxs-lookup"><span data-stu-id="b0bef-p133">Because we are making a web service call, the return value from this activity, reflected in the **Result** property, is of type **DynamicValue**. Therefore, we need a variable of that data type in which to store the output output of the web service call. This is actually pretty easy to do because clicking the **Get Properties** link in the **LookupSPListItem** activity much of this automatically:</span></span>
  
    
    

- <span data-ttu-id="b0bef-221">Erstellen Sie zunächst eine neue Variable vom Typ **DynamicValue**.</span><span class="sxs-lookup"><span data-stu-id="b0bef-221">First, it creates a new variable of type **DynamicValue**.</span></span>
    
  
- <span data-ttu-id="b0bef-222">Anschließend wird diese neue Variable als Quelle für die Eigenschaft **Result** für die Aktivität **LookupSPListItem** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="b0bef-222">Next, it sets this new variable to be the source for the **Result** property on the **LookupSPListItem** activity.</span></span>
    
  
- <span data-ttu-id="b0bef-223">Dann wird eine **GetDynamicValueProperties**-Aktivität für den Workflow festgelegt, sodass wir den Wert aus der Variablen abrufen können.</span><span class="sxs-lookup"><span data-stu-id="b0bef-223">It then adds a **GetDynamicValueProperties** activity to the workflow so that we can retrieve the value from the variable.</span></span>
    
  
- <span data-ttu-id="b0bef-224">Schließlich wird die Variable an die Eigenschaft **Source** für die Aktivität **GetDynamicValueProperties** gebunden.</span><span class="sxs-lookup"><span data-stu-id="b0bef-224">Finally, it binds the variable to the **Source** property on the **GetDynamicValueProperties** activity.</span></span>
    
  
<span data-ttu-id="b0bef-p134">Natürlich hätten Sie all dies manuell durchführen können, aber die Tools vereinfachen den Prozess. Falls erforderlich, können Sie die Namen der Variablen ändern.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p134">Of course, you could have done all of this manually, but the tools simplify the process. If necessary, you can change the names of the variables.</span></span>
  
    
    
<span data-ttu-id="b0bef-227">Der Punkt ist natürlich, einige Werte aus dem Listenelement abzurufen, die den Workflow ausgelöst haben: In der Spalte „Zugewiesen zu" sind die Werte dieser Eigenschaften an zuvor erstellte Variablen gebunden, oder verwenden Sie den Link „Variablen auffüllen", über den die Variablen automatisch erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="b0bef-227">The point, of course, is to get some values from the list item that triggered the workflow: Now the Assigned To column is where the values of these properties are bound to variables previously created or use the Populate Variables link that will create the variables automatically.</span></span>
  
    
    

1. <span data-ttu-id="b0bef-228">Klicken Sie in der Eigenschaft **Properties** für die Aktivität **GetDynamicValueProperties** auf die Schaltfläche mit den Auslassungspunkten [ **...**], um das Dialogfeld **Eigenschaften** zu öffnen, wie in Abbildung 7 gezeigt.</span><span class="sxs-lookup"><span data-stu-id="b0bef-228">On the **Properties** property on the **GetDynamicValueProperties** activity, click on the ellipses button [ **???**] to open the **Properties** dialog box, shown in Figure 7.</span></span>
    
   <span data-ttu-id="b0bef-229">**Abbildung 7. Extrahieren von Werten mithilfe des Dialogfelds Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="b0bef-229">**Figure 7. Extract values using the Properties dialog box**</span></span>

  

  ![Abbildung 7. Extrahieren von Werten aus Listenelementen](../images/ngWfFig07.png)
  

  

  
2. <span data-ttu-id="b0bef-232">Ändern Sie dann den **Entitätstyp** so, dass er dem Typ des Elements entspricht, in diesem Fall dem Listenelement **Listenelement von Ankündigungen**.</span><span class="sxs-lookup"><span data-stu-id="b0bef-232">Next change the **Entity Type** to match the type of the item; in this case it is the **List Item of Announcements** list item.</span></span>
    
  
3. <span data-ttu-id="b0bef-233">Wählen Sie die zwei Eigenschaften zum Abrufen auf: die Felder **Title** und **Created By**.</span><span class="sxs-lookup"><span data-stu-id="b0bef-233">Select the two properties to retrieve: the **Title** and **Created By** fields.</span></span>
    
  
4. <span data-ttu-id="b0bef-p136">In der Spalte **Zuweisen zu** binden Sie diese Eigenschaften an die erstellten Variablen. Alternativ können Sie den Link **Variablen auffüllen** verwenden, über den die Variablen automatisch zugewiesen werden.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p136">The **Assign To** column is where you bind these properties to the variables that we created. Alternatively, you can use the **Populate Variables** link, which assigns the variables automatically.</span></span>
    
  
<span data-ttu-id="b0bef-p137">Beachten Sie in Abbildung 7, wie das Tool die Variablen erstellt und sogar die Datentypen ordnungsgemäß zugeordnet hat. Beachten Sie außerdem, dass das Feld **Erstellt von** eine ganze Zahl ist. Es ist nicht wirklich sinnvoll, dem Benutzer eine Zahl für den Autor anzeigen, oder? Dieses Problem wird später im Workflow behoben.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p137">Notice in Figure 7 how the tool created the variables and even matched the data types correctly. Also notice how the **Created By** field is an integer. It is not really useful to show the user a number for the author is it? This will be addressed later in the workflow.</span></span>
  
    
    

### <a name="get-user-properties"></a><span data-ttu-id="b0bef-240">Abrufen von Benutzereigenschaften</span><span class="sxs-lookup"><span data-stu-id="b0bef-240">Get user properties</span></span>

<span data-ttu-id="b0bef-p138">Eine weitere gängige Aufgabe in der Entwicklung von benutzerdefinierten Workflows ist die Suche nach Benutzern. Unser Workflow weiß beispielsweise derzeit, wer das Ankündigungselement erstellt hat, kennt aber nur die ID. Diese ID ist die ID des Benutzers, der zur **Benutzerinformationsliste** der Website hinzugefügt wurde, die eine zwischengespeicherte Kopie der Profilinformationen ist. Wirklich erwünscht ist der Name oder Anmeldename.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p138">Another common task in custom workflow development is looking up users. For instance, our workflow currently knows who created the announcement item, but only knows them by their ID. This ID is the ID of the user that has been added to the site's **User Information List**, which is a cached copy of their profile information. What is really desired is their name or login name.</span></span>
  
    
    
<span data-ttu-id="b0bef-245">Führen Sie folgende Schritte aus, um Benutzerinformationen abzurufen:</span><span class="sxs-lookup"><span data-stu-id="b0bef-245">To get user information, do the following:</span></span>
  
    
    

1. <span data-ttu-id="b0bef-246">Benennen Sie die erste Sequenz (**Untergeordnete Sequenz 1**) in „Elementeigenschaften abrufen“ um, und nennen Sie die zweite Sequenz „Autoreigenschaften abrufen“.</span><span class="sxs-lookup"><span data-stu-id="b0bef-246">Rename our first sequence ( **Child Sequence 1**) to "Get Item Properties" and name the second sequence to "Get Author Properties".</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b0bef-247">Stellen Sie sicher, dass für die Variable, die die Benutzer-ID enthält, die Bereichsdefinition auf den gesamten Workflow und nicht nur auf die Sequenz festgelegt wird, an der wir arbeiten.</span><span class="sxs-lookup"><span data-stu-id="b0bef-247">Note: Make certain the variable that contains the user ID is scoped to the whole workflow and not just to the sequence we were working on.</span></span> <span data-ttu-id="b0bef-248">Lassen Sie uns den Bereich für die Variable jetzt ändern, wie in Abbildung 8 gezeigt.</span><span class="sxs-lookup"><span data-stu-id="b0bef-248">Let's change the scope of the variable now, as shown in Figure 8.</span></span> 

   <span data-ttu-id="b0bef-249">**Abbildung 8. Ändern des Bereichs von Variablen**</span><span class="sxs-lookup"><span data-stu-id="b0bef-249">**Figure 8. Changing the scope of variables**</span></span>

  

  ![Abbildung 8. Ändern des Variablenumfangs](../images/ngWfFig08.png)
  

  

  
2. <span data-ttu-id="b0bef-p141">Um jetzt Benutzerinformationen abzurufen, ziehen Sie per Drag-and-Drop eine **LookupSpUser**-Aktivität in den Workflow, und benennen Sie sie in „Ankündigungsautor abrufen" um. Diese Aktivität ruft die SharePoint-REST-API auf und übergibt eine bestimmte ID. Überprüfen Sie, wie der REST-Dienst aussieht, indem Sie mithilfe des Browsers zu  `http://../_api/web/SiteUsers` navigieren. Notieren Sie auch die zurückgegebenen Eigenschaften, da wir diese in einem Moment benötigen.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p141">Now, to get the user information, drag-and-drop a **LookupSpUser** activity in the workflow and rename it to "Get Announcement Author". This activity will call the SharePoint REST API and pass in a specific ID. Verify what the REST service looks like by using the browser and navigating to `http://../_api/web/SiteUsers`. Take notice of the properties returned, too, as we will need these in a moment.</span></span>
    
  
3. <span data-ttu-id="b0bef-p142">Beachten Sie, dass jeder Benutzer über eine bestimmte URL verfügt, die seine ID zum Abrufen der Benutzerinformationen enthält. Beachten Sie außerdem, dass die Aktivität wahrscheinlich den Dienstoperator **GetUserById** aufruft und die ID des zu suchenden Benutzers übergibt. Übergeben Sie diese, indem Sie die Eigenschaft **PrincipalId** der Aktivität **LookupSPUser** als **CreatedBy**-Variable festlegen, die die ganze Zahl des Autors des Ankündigungselements ist.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p142">Notice that each user has a specific URL that includes their ID to get the user information. Also notice that the activity is likely calling the **GetUserById** service operator and passing in the ID of the user to lookup. Pass this in by specifying the **PrincipalId** property of the **LookupSPUser** activity to be the **CreatedBy** variable, which is the integer of the author of the announcement item.</span></span>
    
  
4. <span data-ttu-id="b0bef-259">Wie die Aktivität **LookupSPListItem** gibt die Aktivität **LookupSPUser** einen Wert des Typs **DynamicValue** zurück. Erstellen Sie deshalb eine Variable dieses Typs zum Zuweisen zu unserer Antwort, und binden Sie dann diese Variable an die **Result**-Eigenschaften der Aktivität **LookupSPUser**, wie in Abbildung 9 gezeigt.</span><span class="sxs-lookup"><span data-stu-id="b0bef-259">Just like the **LookupSPListItem** activity, the **LookupSPUser** activity returns a value of type **DynamicValue**, so create a variable of that type to associate with our response and then bind this variable to the **Result** properties of the **LookupSPUser** activity, as shown in Figure 9.</span></span>
    
   <span data-ttu-id="b0bef-260">**Abbildung 9: Aktualisieren der Ausgabe der LookupSPUser-Aktivität**</span><span class="sxs-lookup"><span data-stu-id="b0bef-260">**Figure 9. Updating the output of the LookupSPUser activity**</span></span>

  

  ![Abbildung 9. Aktualisieren der LookupSPUser-Ausgabe](../images/ngWfFig09.png)
  

  

  
5. <span data-ttu-id="b0bef-p144">Wie bereits zuvor verwenden wir eine **GetDynamicValueProperties**-Aktivität zum Abrufen der Ergebnisse aus dem Wert **AuthorProperties**. Beachten Sie jedoch, dass **Entity Type** dieses Mal nicht über eine Option verfügt, die festgelegt werden kann. Das ist kein Problem, da die tatsächliche Webdienstantwort **LookupSPUser** im Browser angezeigt werden kann. Geben Sie zum Anzeigen den Pfad zu der Eigenschaft ein, die Sie suchen, in diesem Fall `d/results/(0)/LoginName`. Geben Sie dann eine andere ein, um den Anzeigenamen des Autors abzurufen, wie in Abbildung 10 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p144">As we did earlier, use a **GetDynamicValueProperties** activity to pull the results out of the **AuthorProperties** value. However, notice this time around that the **Entity Type** does not have an option that we can set. This is not a problem, because the actual web service response the **LookupSPUser** can be seen in the browser. To see it, enter the path to the property you are looking for, which, in this case is `d/results/(0)/LoginName`; then, enter another to get the display name of the author, as shown in Figure 10.</span></span>
    
   <span data-ttu-id="b0bef-267">**Abbildung 10. Abrufen von Werten aus der LookupSPUser-Aktivität**</span><span class="sxs-lookup"><span data-stu-id="b0bef-267">**Figure 10. Retrieving values from the LookupSPUser activity**</span></span>

  

  ![Abbildung 10. Abrufen von Werten aus LookupSPUser](../images/ngWfFig10.png)
  

  

  

### <a name="test-the-workflow"></a><span data-ttu-id="b0bef-270">Testen des Workflows</span><span class="sxs-lookup"><span data-stu-id="b0bef-270">Test the workflow</span></span>

<span data-ttu-id="b0bef-p146">Lassen Sie uns abschließend den Workflow testen. Beginnen Sie, indem Sie zwei **WriteLine**-Aktivitäten hinzufügen. Mit diesen können wir die Inhalte unserer zwei Variablen anzeigen. Wenn der Workflow getestet wird, schreibt das Konsolenhilfsprogramm zum Testen des Diensthosts die beiden Werte aus, wie in Abbildung 11 gezeigt.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p146">Finally, let's test the workflow. Start by adding two **WriteLine** activities. These allow us to show the contents of our two variables. When testing the workflow, the Test Service Host console utility will write out the two values as shown in Figure 11.</span></span>
  
    
    

<span data-ttu-id="b0bef-275">**Abbildung 11: Test mithilfe der Konsole zum Testen des Diensthosts**</span><span class="sxs-lookup"><span data-stu-id="b0bef-275">**Figure 11. Test using Test Service Host Console**</span></span>

  
    
    

  
    
    
![Abbildung 11. Testen des Workflows](../images/ngWfFig11.png)
  
    
    

  
    
    

  
    
    

## <a name="conclusion"></a><span data-ttu-id="b0bef-278">Schlussbemerkung</span><span class="sxs-lookup"><span data-stu-id="b0bef-278">Conclusion</span></span>
<span data-ttu-id="b0bef-279"><a name="bm4"> </a></span><span class="sxs-lookup"><span data-stu-id="b0bef-279"></span></span>

<span data-ttu-id="b0bef-p148">In diesem Artikel wurden zunächst die verschiedenen Workflowtypen erläutert, die mithilfe von Visual Studio 2012 und höher für SharePoint erstellt werden können, wenn eine Verbindung zur einer Workflow-Manager-Farm hergestellt wurde. Als Nächstes wurde gezeigt, wie Sie einen Workflow erstellen, der nicht nur Werte aus dem Listenelement erfasst, das den Workflow auslöst, sondern auch eine gängige Aufgabe wie das Abrufen des Anmeldenamens und Anzeigenamens eines Benutzers mithilfe der **LookupSPUser**-Aktivität durchführt. Darüber hinaus wurden im Artikel einige bewährte Methoden für das Organisieren von Workflows und das Hinzufügen von Kommentaren mithilfe von Anmerkungen dargestellt.</span><span class="sxs-lookup"><span data-stu-id="b0bef-p148">This article first explained the different types of workflows that can be created using Visual Studio 2012 and later for SharePoint when it has been connected to a Workflow Manager farm. Next it demonstrated how to create a workflow that not only collected values from the list item that triggered the workflow, but it also demonstrated how to perform a common task such as obtaining a user's login name and display name using the **LookupSPUser** activity. In addition, the article touched on a few good practices for keeping workflows organized and adding comments using annotations.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="b0bef-283">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="b0bef-283">See also</span></span>
<span data-ttu-id="b0bef-284"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b0bef-284"></span></span>


-  [<span data-ttu-id="b0bef-285">Workflows in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b0bef-285">Workflows in SharePoint</span></span>](workflows-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b0bef-286">Bewährte Methoden für die SharePoint-Workflowentwicklung</span><span class="sxs-lookup"><span data-stu-id="b0bef-286">SharePoint workflow development best practices</span></span>](sharepoint-workflow-development-best-practices.md)
    
  
-  [<span data-ttu-id="b0bef-287">Beispiele für SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="b0bef-287">SharePoint workflow samples</span></span>](sharepoint-workflow-samples.md)
    
  

  
    
    

