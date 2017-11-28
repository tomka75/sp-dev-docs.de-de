---
title: "Workflows, Aktionen (Aktivitäten), Ereignisse und Formularen in die SharePoint-add-in-Objektmodell"
ms.date: 11/03/2017
ms.openlocfilehash: d20da3810fc6c6f0cc32eda185ec7cfd45d1f607
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="workflows-actions-activities-events-and-forms-in-the-sharepoint-add-in-model"></a><span data-ttu-id="809ee-102">Workflows, Aktionen (Aktivitäten), Ereignisse und Formularen in die SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="809ee-102">Workflows, actions (activities), events, and forms in the SharePoint add-in model</span></span>
=================================================================================

<a name="summary"></a><span data-ttu-id="809ee-103">Summary</span><span class="sxs-lookup"><span data-stu-id="809ee-103">Summary</span></span>
-------

<span data-ttu-id="809ee-104">Ansatz verwenden Sie zum Implementieren von Workflows und die damit verbundenen Komponenten unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.</span><span class="sxs-lookup"><span data-stu-id="809ee-104">The approach you take to implement workflows and their associated components is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="809ee-105">In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario, Workflows und die damit verbundenen Komponenten mit serverseitigen Code erstellt und über den SharePoint-Lösungen bereitgestellt wurden.</span><span class="sxs-lookup"><span data-stu-id="809ee-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, workflows and their associated components were built with server side code and deployed via SharePoint Solutions.</span></span>  <span data-ttu-id="809ee-106">Die Workflows und die damit verbundenen Komponenten, die für den SharePoint-Server ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="809ee-106">The workflows and their associated components ran on the SharePoint server.</span></span>

<span data-ttu-id="809ee-107">In einem Modell Szenario SharePoint-Add-in Workflows und die damit verbundenen Komponenten mit Code entwickelt wurden, die auf Remoteservern ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="809ee-107">In an SharePoint Add-in model scenario, workflows and their associated components are developed with code that runs on remote servers.</span></span>  <span data-ttu-id="809ee-108">Workflows und die damit verbundenen Komponenten mit dem Workflow-Dienst registriert sind, aber alle Code auf Remoteservern ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="809ee-108">Workflows and their associated components are registered with the Workflow Service, but all code executes on remote servers.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="809ee-109">Hohe Stufe Richtlinien</span><span class="sxs-lookup"><span data-stu-id="809ee-109">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="809ee-110">In der Regel von einer Ziehpunkt möchten wir die folgenden Richtlinien auf hohen Ebenen bieten zum Erstellen von Workflows und die damit verbundenen Komponenten in das neue SharePoint-Add-in-Modell.</span><span class="sxs-lookup"><span data-stu-id="809ee-110">As a rule of a thumb, we would like to provide the following high level guidelines for creating workflows and their associated components in the new SharePoint Add-in model.</span></span>

- <span data-ttu-id="809ee-111">CodeBehind-Workflows sind nicht verfügbar in Office 365-Mandanten oder mit dem SharePoint-Add-in-Objektmodell im Allgemeinen.</span><span class="sxs-lookup"><span data-stu-id="809ee-111">Code behind workflows are not available in Office 365 tenancies, or with the SharePoint Add-in model in general.</span></span>
- <span data-ttu-id="809ee-112">Alle CodeBehind zugeordneten Workflows und die damit verbundenen Komponenten müssen in einem externen Webdienst auf einem Remoteserver ausgeführt platziert werden.</span><span class="sxs-lookup"><span data-stu-id="809ee-112">All code behind associated with workflows and their associated components must be placed in an external web service running on a remote server.</span></span>

<a name="options-to-create-custom-workflows-and-their-associated-components"></a><span data-ttu-id="809ee-113">Optionen zum Erstellen von benutzerdefinierten Workflows und die damit verbundenen Komponenten</span><span class="sxs-lookup"><span data-stu-id="809ee-113">Options to create custom workflows and their associated components</span></span>
------------------------------------------------------------------
<span data-ttu-id="809ee-114">Es gibt einige Optionen zum Erstellen von benutzerdefinierten Workflows und die damit verbundenen Komponenten.</span><span class="sxs-lookup"><span data-stu-id="809ee-114">You have a few options to create custom workflows and their associated components.</span></span>

- <span data-ttu-id="809ee-115">Erstellen von benutzerdefinierten workflows</span><span class="sxs-lookup"><span data-stu-id="809ee-115">Create custom workflows</span></span>
- <span data-ttu-id="809ee-116">Erstellen Sie benutzerdefinierte Workflowaktivitäten</span><span class="sxs-lookup"><span data-stu-id="809ee-116">Create custom workflow activities</span></span>
- <span data-ttu-id="809ee-117">Erstellen von benutzerdefinierten Workflow-Ereignissen</span><span class="sxs-lookup"><span data-stu-id="809ee-117">Create custom workflow events</span></span>
- <span data-ttu-id="809ee-118">Erstellen benutzerdefinierter Workflowformulare</span><span class="sxs-lookup"><span data-stu-id="809ee-118">Create custom workflow forms</span></span>

<a name="create-custom-workflows"></a><span data-ttu-id="809ee-119">Erstellen von benutzerdefinierten workflows</span><span class="sxs-lookup"><span data-stu-id="809ee-119">Create custom workflows</span></span>
-----------------------
<span data-ttu-id="809ee-120">Bei dieser Option werden benutzerdefinierte Workflows erstellt, bereitgestellt und mit der Hostwebsite in SharePoint verknüpft.</span><span class="sxs-lookup"><span data-stu-id="809ee-120">In this option custom workflows are created, deployed, and associated with the Host-web in SharePoint.</span></span>

- <span data-ttu-id="809ee-121">Benutzerdefinierte Workflows können mit Visual Studio oder SharePoint Designer erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="809ee-121">Custom workflows may be created with Visual Studio or SharePoint Designer.</span></span>
    + <span data-ttu-id="809ee-122">Finden Sie unter [Develop SharePoint 2013-Workflows mit Visual Studio (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/office/jj163199.aspx) , die beide zusammenfasst Optionen und werden die vor- und Nachteile der einzelnen.</span><span class="sxs-lookup"><span data-stu-id="809ee-122">See the [Develop SharePoint 2013 workflows using Visual Studio (MSDN Article)](https://msdn.microsoft.com/en-us/library/office/jj163199.aspx) that summarizes both options and discusses the advantages and disadvantages of each.</span></span>
- <span data-ttu-id="809ee-123">Benutzerdefinierte Workflows können bereitgestellt und die Hostwebsite in SharePoint auf verschiedene Weise zugeordnet werden.</span><span class="sxs-lookup"><span data-stu-id="809ee-123">Custom workflows may be deployed and associated with the Host-web in SharePoint in several ways.</span></span>
    - <span data-ttu-id="809ee-124">In Visual Studio erstellte Workflows werden automatisch innerhalb von Features für die Bereitstellung gepackt.</span><span class="sxs-lookup"><span data-stu-id="809ee-124">Workflows created in Visual Studio are automatically packaged inside features for deployment.</span></span>
    - <span data-ttu-id="809ee-125">Workflows in SharePoint Designer exportiert und importiert, um diese Funktionen auf einem Entwicklungsserver für die auf einem Produktionsserver bereitstellen muss erstellt.</span><span class="sxs-lookup"><span data-stu-id="809ee-125">Workflows created in SharePoint designer must be exported and imported to deploy them from a development server to a production server.</span></span>
    - <span data-ttu-id="809ee-126">Workflows können auch bereitgestellt und die Hostwebsite in SharePoint über die remote provisioning Muster zugeordnet werden.</span><span class="sxs-lookup"><span data-stu-id="809ee-126">Workflows may also be deployed and associated with the Host-web in SharePoint via the remote provisioning pattern.</span></span>  <span data-ttu-id="809ee-127">Finden Sie unter der [Website-Bereitstellung (SharePoint-Add-in-Anleitung)](site-provisioning-sharepoint-add-in.md) ausführliche Informationen zum remote-Bereitstellung Muster.</span><span class="sxs-lookup"><span data-stu-id="809ee-127">See the [Site provisioning (SharePoint Add-in Recipe)](site-provisioning-sharepoint-add-in.md) for more details about the remote provisioning pattern.</span></span>

<span data-ttu-id="809ee-128">Im folgenden Codebeispiel wird veranschaulicht, wie CSOM zum Bereitstellen eines Workflows und die Listen die Unterstützung für den Workflow verwenden.</span><span class="sxs-lookup"><span data-stu-id="809ee-128">The following code sample demonstrates how to use CSOM to provision a workflow and the lists which support the workflow.</span></span>

    public void ProvisionIncidentWorkflowAndRelatedLists(string incidentWorkflowFile, string suiteLevelWebAppUrl, string dispatcherName)
    {
        //Return the list the workflow will be associated with
        var incidentsList = CSOMUtil.GetListByTitle(clientContext, "Incidents");

        //Create a new WorkflowProvisionService class instance which uses the 
        //Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager to
        //provision and configure workflows
        var service = new WorkflowProvisionService(clientContext);

        //Read the workflow .XAML file
        var incidentWF = System.IO.File.ReadAllText(incidentWorkflowFile);

        //Create the WorkflowDefinition and use the 
        //Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager
        //to save and publish it.  
        //This method is shown below for reference.
        var incidentWFDefinitionId = service.SaveDefinitionAndPublish("Incident",
            WorkflowUtil.TranslateWorkflow(incidentWF));

        //Create the workflow tasks list
        var taskListId = service.CreateTaskList("Incident Workflow Tasks");

        //Create the workflow history list
        var historyListId = service.CreateHistoryList("Incident Workflow History");

        //Use the Microsoft.SharePoint.Client.WorkflowServices.WorkflowSubscriptionService to 
        //subscibe the workflow to the list the workflow is associated with, register the
        //events it is associated with, and register the tasks and history list. 
        //This method is shown below for reference.
        service.Subscribe("Incident Workflow", incidentWFDefinitionId, incidentsList.Id,
            WorkflowSubscritpionEventType.ItemAdded, taskListId, historyListId);
    }
    
    public Guid SaveDefinitionAndPublish(string name, string translatedWorkflows)
    {
        var definition = new WorkflowDefinition(ClientContext)
        {
            DisplayName = name,
            Xaml = translatedWorkflows
        };

        var deploymentService = workflowServicesManager.GetWorkflowDeploymentService();
        var result = deploymentService.SaveDefinition(definition);
        ClientContext.ExecuteQuery();

        deploymentService.PublishDefinition(result.Value);
        ClientContext.ExecuteQuery();

        return result.Value;
    }

    public Guid Subscribe(string name, Guid definitionId, Guid targetListId, WorkflowSubscritpionEventType eventTypes, Guid taskListId, Guid historyListId)
    {
        var eventTypesList = new List<string>();
        foreach (WorkflowSubscritpionEventType type in Enum.GetValues(typeof(WorkflowSubscritpionEventType)))
        {
            if ((type & eventTypes) > 0)
                eventTypesList.Add(type.ToString());
        }

        var subscription = new WorkflowSubscription(ClientContext)
        {
            Name = name,
            Enabled = true,
            DefinitionId = definitionId,
            EventSourceId = targetListId,
            EventTypes = eventTypesList.ToArray()
        };

        subscription.SetProperty("TaskListId", taskListId.ToString());
        subscription.SetProperty("HistoryListId", historyListId.ToString());

        var subscriptionService = workflowServicesManager.GetWorkflowSubscriptionService();
        var result = subscriptionService.PublishSubscriptionForList(subscription, targetListId);

        ClientContext.ExecuteQuery();
        return result.Value;
    }

<span data-ttu-id="809ee-129">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="809ee-129">**When is it a good fit?**</span></span>

<span data-ttu-id="809ee-130">Wenn Sie zum Erstellen von benutzerdefinierten Workflows mit Code-behind sie diese Option müssen eignet sich gut.</span><span class="sxs-lookup"><span data-stu-id="809ee-130">When you need to create custom workflows with code behind them this option is a good fit.</span></span>

<span data-ttu-id="809ee-131">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="809ee-131">**Getting Started**</span></span>

<span data-ttu-id="809ee-132">In den folgenden Artikeln wird gezeigt, wie benutzerdefinierte Workflows erstellen.</span><span class="sxs-lookup"><span data-stu-id="809ee-132">The following articles demonstrate how to create custom workflows.</span></span>

- [<span data-ttu-id="809ee-133">Erstellen Sie eine SharePoint-Workflow-app mit den Visual Studio 2012 (MSDN-Artikel)</span><span class="sxs-lookup"><span data-stu-id="809ee-133">Create a SharePoint workflow app using Visual Studio 2012 (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/dn456545.aspx)
- [<span data-ttu-id="809ee-134">Vorgehensweise: Erstellen von SharePoint 2013-Workflows mit Visual Studio (MSDN-Artikel)</span><span class="sxs-lookup"><span data-stu-id="809ee-134">How to: Create SharePoint 2013 Workflows using Visual Studio (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/dn584771.aspx)

<a name="create-custom-workflow-activities"></a><span data-ttu-id="809ee-135">Erstellen Sie benutzerdefinierte Workflowaktivitäten</span><span class="sxs-lookup"><span data-stu-id="809ee-135">Create custom workflow activities</span></span>
---------------------------------
<span data-ttu-id="809ee-136">Bei dieser Option werden benutzerdefinierte Workflowaktivitäten erstellt und in SharePoint bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="809ee-136">In this option custom workflow activities are created and deployed to SharePoint.</span></span>

- <span data-ttu-id="809ee-137">Benutzerdefinierte Workflowaktivitäten möglicherweise mit Visual Studio erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="809ee-137">Custom workflow activities may be created with Visual Studio.</span></span>
- <span data-ttu-id="809ee-138">Benutzerdefinierte Workflowaktivitäten können nicht mit SharePoint Designer erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="809ee-138">Custom workflow activities may not be created with SharePoint Designer.</span></span>
- <span data-ttu-id="809ee-139">Benutzerdefinierte Workflowaktivitäten können in SharePoint Designer verwendet werden, nachdem sie eine SharePoint-Umgebung bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="809ee-139">Custom workflow activities may be used in SharePoint Designer after they are deployed to a SharePoint environment.</span></span>

<span data-ttu-id="809ee-140">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="809ee-140">**When is it a good fit?**</span></span>

<span data-ttu-id="809ee-141">Wenn Sie Workflows in Geschäftsprozessen implementieren, deren von der Out-of-Box-Bibliothek Workflowaktionen in SharePoint Designer nicht erfüllt werden, müssen</span><span class="sxs-lookup"><span data-stu-id="809ee-141">When you need to implement workflows in business processes whose requirements are not met by the out-of-the-box library of workflow actions in SharePoint Designer</span></span>

<span data-ttu-id="809ee-142">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="809ee-142">**Getting Started**</span></span>

<span data-ttu-id="809ee-143">Im folgende Artikel veranschaulicht das Erstellen einer benutzerdefinierten Workflowaktivität mit Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="809ee-143">The following article demonstrates how to create a custom workflow activity with Visual Studio.</span></span>

- [<span data-ttu-id="809ee-144">Vorgehensweise: Erstellen und Bereitstellen von benutzerdefinierten Workflowaktionen (MSDN-Artikel)</span><span class="sxs-lookup"><span data-stu-id="809ee-144">How to: Build and deploy workflow custom actions (MSDN Article)</span></span>](https://msdn.microsoft.com/en-us/library/office/jj163911.aspx)

<span data-ttu-id="809ee-145">Die [Workflow.Activities (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) enthält mehrere benutzerdefinierte Workflowaktivitäten mit Visual Studio erstellt.</span><span class="sxs-lookup"><span data-stu-id="809ee-145">The [Workflow.Activities (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) includes several custom workflow activities created with Visual Studio.</span></span>  <span data-ttu-id="809ee-146">Darüber hinaus wird das Verwenden der benutzerdefinierten Workflow-Aktivitäten in einem Workflow veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="809ee-146">It also demonstrates how to use the custom workflow activities in a workflow.</span></span>

<a name="create-custom-workflow-events"></a><span data-ttu-id="809ee-147">Erstellen von benutzerdefinierten Workflow-Ereignissen</span><span class="sxs-lookup"><span data-stu-id="809ee-147">Create custom workflow events</span></span>
-----------------------------
<span data-ttu-id="809ee-148">Bei dieser Option werden benutzerdefinierte Workflowereignisse erstellt und in SharePoint bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="809ee-148">In this option custom workflow events are created and deployed to SharePoint.</span></span>

- <span data-ttu-id="809ee-149">Benutzerdefinierte Workflow-Ereignisse können mit Visual Studio erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="809ee-149">Custom workflow events may be created with Visual Studio.</span></span>
- <span data-ttu-id="809ee-150">Benutzerdefinierte Workflow-Ereignisse können nicht mit SharePoint Designer erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="809ee-150">Custom workflow events may not be created with SharePoint Designer.</span></span>
- <span data-ttu-id="809ee-151">Benutzerdefinierte Workflow-Ereignisse können in SharePoint Designer verwendet werden, nachdem sie eine SharePoint-Umgebung bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="809ee-151">Custom workflow events may be used in SharePoint Designer after they are deployed to a SharePoint environment.</span></span>

<span data-ttu-id="809ee-152">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="809ee-152">**When is it a good fit?**</span></span>

<span data-ttu-id="809ee-153">Wenn Sie Workflows in Geschäftsprozessen implementieren, deren Anforderungen an die Workflows zu warten, bis ein benutzerdefiniertes Ereignis vor dem Fortfahren erforderlich sein, müssen.</span><span class="sxs-lookup"><span data-stu-id="809ee-153">When you need to implement workflows in business processes whose requirements require the workflows to wait for a custom event before proceeding.</span></span>

<span data-ttu-id="809ee-154">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="809ee-154">**Getting Started**</span></span>

<span data-ttu-id="809ee-155">Die [Workflow.CustomEvents (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomEvents) wird gezeigt, wie ein Workflow erstellt, der ein benutzerdefiniertes sogar an ausgelöst werden, bevor Sie fortfahren wartet.</span><span class="sxs-lookup"><span data-stu-id="809ee-155">The [Workflow.CustomEvents (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomEvents) demonstrates how to create a workflow that waits for a custom even to fire before proceeding.</span></span>  <span data-ttu-id="809ee-156">Es wird veranschaulicht, wie die JavaScript Client Side-Objektmodell (JSOM) für den Workflow-Manager verwenden, um ein benutzerdefiniertes Ereignis ausgelöst wird.</span><span class="sxs-lookup"><span data-stu-id="809ee-156">It also demonstrates how to use the JavaScript Client Side Object Model (JSOM) for the Workflow Services Manager to raise a custom event.</span></span>

<a name="create-custom-workflow-forms"></a><span data-ttu-id="809ee-157">Erstellen benutzerdefinierter Workflowformulare</span><span class="sxs-lookup"><span data-stu-id="809ee-157">Create custom workflow forms</span></span>
------------------------------------------------
<span data-ttu-id="809ee-158">Bei dieser Option benutzerdefinierter Workflowformulare erstellt und in SharePoint bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="809ee-158">In this option custom workflow forms are created and deployed to SharePoint.</span></span>

- <span data-ttu-id="809ee-159">Benutzerdefinierter Workflowformulare möglicherweise mit Visual Studio erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="809ee-159">Custom workflow forms may be created with Visual Studio.</span></span>
- <span data-ttu-id="809ee-160">Benutzerdefinierter Workflowformulare können nicht mit SharePoint Designer erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="809ee-160">Custom workflow forms may not be created with SharePoint Designer.</span></span>
- <span data-ttu-id="809ee-161">Benutzerdefinierter Workflowformulare können in SharePoint Designer verwendet werden, nachdem sie eine SharePoint-Umgebung bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="809ee-161">Custom workflow forms may be used in SharePoint Designer after they are deployed to a SharePoint environment.</span></span>

<span data-ttu-id="809ee-162">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="809ee-162">**When is it a good fit?**</span></span>

<span data-ttu-id="809ee-163">Wenn Sie Workflows in Geschäftsprozessen implementieren müssen erfordern, deren Anforderungen für benutzerdefinierte Formulare.</span><span class="sxs-lookup"><span data-stu-id="809ee-163">When you need to implement workflows in business processes whose requirements require custom forms.</span></span>

<span data-ttu-id="809ee-164">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="809ee-164">**Getting Started**</span></span>

<span data-ttu-id="809ee-165">Im folgende Artikel veranschaulicht das Erstellen von benutzerdefinierten Workflows Zuordnungs-und Initiierungsformularen und deren Verwendung in einem Workflow.</span><span class="sxs-lookup"><span data-stu-id="809ee-165">The following article demonstrates how to create custom workflow association and initiation forms and use them in a workflow.</span></span>

- [<span data-ttu-id="809ee-166">Vorgehensweise: Erstellen von benutzerdefinierten SharePoint Server 2013 Workflow-Formularen mit Visual Studio 2012 (MSDN-Artikel)</span><span class="sxs-lookup"><span data-stu-id="809ee-166">How to: Create Custom SharePoint Server 2013 Workflow Forms with Visual Studio 2012 (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/dn518136.aspx)

<span data-ttu-id="809ee-167">Die [Workflow.CustomTasks (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomTasks) veranschaulicht das Erstellen von benutzerdefinierten Formularen für Aufgaben- und Initiierung und deren Verwendung in einem Workflow.</span><span class="sxs-lookup"><span data-stu-id="809ee-167">The [Workflow.CustomTasks (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomTasks) demonstrates how to create custom task and initiation forms and use them in a workflow.</span></span>

<a name="options-to-update-sharepoint-data-from-a-custom-workflow"></a><span data-ttu-id="809ee-168">Optionen zum Aktualisieren von SharePoint-Daten mithilfe eines benutzerdefinierten Workflows</span><span class="sxs-lookup"><span data-stu-id="809ee-168">Options to update SharePoint data from a custom workflow</span></span>
--------------------------------------------------------
<span data-ttu-id="809ee-169">Sie haben verschiedene Optionen zum Aktualisieren von SharePoint-Daten mithilfe eines benutzerdefinierten Workflows.</span><span class="sxs-lookup"><span data-stu-id="809ee-169">You have a couple of options to update SharePoint data from a custom workflow.</span></span>

- <span data-ttu-id="809ee-170">Verwenden Sie die Kontext-Token und Web-URL-Add-in SharePoint authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="809ee-170">Use the context token and Add-in web URL to authenticate to SharePoint.</span></span>
- <span data-ttu-id="809ee-171">Verwenden Sie die Add-Ins Web-URL und den SharePoint Webproxy SharePoint authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="809ee-171">Use the Add-in web URL and the SharePoint web proxy to authenticate to SharePoint.</span></span>

<a name="use-the-context-token-and-add-in-web-url-to-authenticate-to-sharepoint"></a><span data-ttu-id="809ee-172">Verwenden Sie die Kontext-Token und Add-Ins Web-URL zur Authentifizierung in SharePoint</span><span class="sxs-lookup"><span data-stu-id="809ee-172">Use the context token and Add-in web URL to authenticate to SharePoint</span></span>
----------------------------------------------------------------------

<span data-ttu-id="809ee-173">Bei dieser Option übergeben Sie den Kontext-Token und die Add-in-Web-URL der Workflow mit dem Dienst der Workflow ruft über HTTP-Header.</span><span class="sxs-lookup"><span data-stu-id="809ee-173">In this option you pass the context token and the Add-in web URL from the workflow to the service the workflow calls via http headers.</span></span>  <span data-ttu-id="809ee-174">Der Dienst verwendet die Kontext-Token und Add-Ins Web-URL zur Authentifizierung in SharePoint und ein Zugriffstoken vor dem Aktualisieren von SharePoint-Daten zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="809ee-174">The service uses the context token and Add-in web URL to authenticate to SharePoint and return an access token before updating SharePoint data.</span></span> 

- <span data-ttu-id="809ee-175">Bei diesem Ansatz müssen, und übergeben Sie das Content Token an den Webdienst aus dem Workflow.</span><span class="sxs-lookup"><span data-stu-id="809ee-175">This approach requires passing the content token from the workflow to the web service.</span></span>

<span data-ttu-id="809ee-176">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="809ee-176">**When is it a good fit?**</span></span>

<span data-ttu-id="809ee-177">Wenn Sie die Kommunikation mit SharePoint auf Ebene der Client möchten.</span><span class="sxs-lookup"><span data-stu-id="809ee-177">When you want the communication to SharePoint to occur at the client level.</span></span>

<span data-ttu-id="809ee-178">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="809ee-178">**Getting Started**</span></span>

<span data-ttu-id="809ee-179">Im folgende Beispiel wird gezeigt, wie Sie mit den Kontext-Token und die Add-in-Web-URL zur Authentifizierung in SharePoint und SharePoint-Daten zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="809ee-179">The following sample demonstrates how to use the context token and the Add-in web URL to authenticate to SharePoint and update SharePoint data.</span></span>

- [<span data-ttu-id="809ee-180">Workflow.CallCustomService (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="809ee-180">Workflow.CallCustomService (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)

<span data-ttu-id="809ee-181">Finden Sie im Abschnitt [aufrufen Web API-Diensts](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService#call-web-api-service) in der Infodatei [Workflow.CallCustomService (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) ausführliche Informationen zu den Kontext-Token und die Add-in-Web-URL aus dem Workflow an den Dienst übergeben.</span><span class="sxs-lookup"><span data-stu-id="809ee-181">See the [Call Web Api service](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService#call-web-api-service) section in the [Workflow.CallCustomService (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) README for more details about passing the context token and the Add-in web URL from the workflow to the service.</span></span>

<span data-ttu-id="809ee-182">Die anderen Abschnitte in der Infodatei [Workflow.CallCustomService (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) enthalten detaillierte Informationen zu den gesamten Workflow und remote-Dienst und führen Sie auch durch alle Komponenten in Microsoft Azure einrichten.</span><span class="sxs-lookup"><span data-stu-id="809ee-182">The other sections in the [Workflow.CallCustomService (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) README provide detailed information about the entire workflow and remote service and also walk you through setting up all of the components in Microsoft Azure.</span></span>

<a name="use-the-add-in-web-url-and-the-sharepoint-web-proxy-to-authenticate-to-sharepoint"></a><span data-ttu-id="809ee-183">Verwenden Sie die Add-Ins Web-URL und den SharePoint Webproxy zur Authentifizierung in SharePoint</span><span class="sxs-lookup"><span data-stu-id="809ee-183">Use the Add-in web URL and the SharePoint web proxy to authenticate to SharePoint</span></span>
---------------------------------------------------------------------------------

<span data-ttu-id="809ee-184">In diese Option, wenn der Workflow gestartet wird, die Sie übergeben Sie der Add-Ins Web-URL aus dem Workflow mit dem Dienst den Workflow aufruft.</span><span class="sxs-lookup"><span data-stu-id="809ee-184">In this option when the workflow starts you pass the Add-in web URL from the workflow to the service the workflow calls.</span></span>  <span data-ttu-id="809ee-185">Der Dienst übergibt die Add-in-Web-URL an den SharePoint Web Proxy.</span><span class="sxs-lookup"><span data-stu-id="809ee-185">The service passes the Add-in web URL to the SharePoint Web Proxy.</span></span>  <span data-ttu-id="809ee-186">SharePoint-Web-Proxy verwendet die Add-Ins Web-URL zur Authentifizierung in SharePoint und ein Zugriffstoken zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="809ee-186">The SharePoint Web Proxy uses the Add-in web URL to authenticate to SharePoint and return an access token.</span></span>  <span data-ttu-id="809ee-187">Klicken Sie dann fügt den SharePoint Web Proxy das Zugriffstoken an die HTTP-Header vor dem aufrufen, SharePoint-Daten zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="809ee-187">Then, the SharePoint Web Proxy appends the access token to the http headers before making the call to update SharePoint data.</span></span>

- <span data-ttu-id="809ee-188">Dieser Ansatz ist kein erforderlich und übergeben Sie das Content Token an den Webdienst aus dem Workflow.</span><span class="sxs-lookup"><span data-stu-id="809ee-188">This approach does not require passing the content token from the workflow to the web service.</span></span>

<span data-ttu-id="809ee-189">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="809ee-189">**When is it a good fit?**</span></span>

<span data-ttu-id="809ee-190">Wenn Sie die Kommunikation mit SharePoint erfolgt auf Serverebene möchten.</span><span class="sxs-lookup"><span data-stu-id="809ee-190">When you want the communication to SharePoint to occur at the server level.</span></span>

<span data-ttu-id="809ee-191">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="809ee-191">**Getting Started**</span></span>

<span data-ttu-id="809ee-192">Das folgende Beispiel veranschaulicht, wie Sie die Add-Ins Web-URL und den SharePoint Webproxy zur Authentifizierung in SharePoint und SharePoint-Daten zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="809ee-192">The following sample demonstrates how to use the Add-in web URL and the SharePoint web proxy to authenticate to SharePoint and update SharePoint data.</span></span>

- [<span data-ttu-id="809ee-193">Workflow.CallServiceUpdateSPViaProxy (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="809ee-193">Workflow.CallServiceUpdateSPViaProxy (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)

<span data-ttu-id="809ee-194">Finden Sie im Abschnitt [rufen Sie Web-Api-Dienst über den Webproxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy#call-web-api-service-via-web-proxy) [Workflow.CallServiceUpdateSPViaProxy (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) Infodatei Nähere Informationen zu den SharePoint Web Proxy-Aufruf.</span><span class="sxs-lookup"><span data-stu-id="809ee-194">See the [Call Web Api service via web proxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy#call-web-api-service-via-web-proxy) section in the [Workflow.CallServiceUpdateSPViaProxy (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) README for more details about the SharePoint Web Proxy invocation.</span></span>

<span data-ttu-id="809ee-195">Die anderen Abschnitte in der Infodatei [Workflow.CallServiceUpdateSPViaProxy (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) enthalten detaillierte Informationen zu den gesamten Workflow und remote-Dienst und führen Sie auch durch alle Komponenten in Microsoft Azure einrichten.</span><span class="sxs-lookup"><span data-stu-id="809ee-195">The other sections in the [Workflow.CallServiceUpdateSPViaProxy (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) README provide detailed information about the entire workflow and remote service and also walk you through setting up all of the components in Microsoft Azure.</span></span>

<span data-ttu-id="809ee-196">Finden Sie unter die [Abfrage einem Remotedienst mithilfe des Webproxys in SharePoint 2013 (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/office/fp179895.aspx) Weitere Informationen zu den SharePoint Web Proxy.</span><span class="sxs-lookup"><span data-stu-id="809ee-196">See the [Query a remote service using the web proxy in SharePoint 2013 (MSDN Article)](https://msdn.microsoft.com/en-us/library/office/fp179895.aspx) for more information about the SharePoint Web Proxy.</span></span>

<a name="related-links"></a><span data-ttu-id="809ee-197">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="809ee-197">Related links</span></span>
=============
- [<span data-ttu-id="809ee-198">SharePoint 2013 Workflow-Objektmodell (MSDN-Artikel)</span><span class="sxs-lookup"><span data-stu-id="809ee-198">SharePoint 2013 workflow object model (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/jj163969.aspx)
- [<span data-ttu-id="809ee-199">Häufige Fehlermeldungen in SharePoint Workflow Development (MSDN-Artikel)</span><span class="sxs-lookup"><span data-stu-id="809ee-199">Common error messages in SharePoint workflow development (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/dn449112.aspx)
- [<span data-ttu-id="809ee-200">Verwenden von Workflow-Interop für SharePoint 2013 (MSDN-Artikel)</span><span class="sxs-lookup"><span data-stu-id="809ee-200">Use workflow interop for SharePoint 2013 (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/jj670125.aspx)
- [<span data-ttu-id="809ee-201">Entwickeln von SharePoint 2013-Workflows mit Visual Studio (MSDN-Artikel)</span><span class="sxs-lookup"><span data-stu-id="809ee-201">Develop SharePoint 2013 workflows using Visual Studio (MSDN Article)</span></span>](https://msdn.microsoft.com/en-us/library/office/jj163199.aspx)
- [<span data-ttu-id="809ee-202">Site-Bereitstellung (SharePoint-Add-in Anleitung)</span><span class="sxs-lookup"><span data-stu-id="809ee-202">Site provisioning (SharePoint Add-in Recipe)</span></span>](site-provisioning-sharepoint-add-in.md)
- [<span data-ttu-id="809ee-203">Erstellen Sie eine SharePoint-Workflow-app mit den Visual Studio 2012 (MSDN-Artikel)</span><span class="sxs-lookup"><span data-stu-id="809ee-203">Create a SharePoint workflow app using Visual Studio 2012 (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/dn456545.aspx)
- [<span data-ttu-id="809ee-204">Vorgehensweise: Erstellen von SharePoint 2013-Workflows mit Visual Studio (MSDN-Artikel)</span><span class="sxs-lookup"><span data-stu-id="809ee-204">How to: Create SharePoint 2013 Workflows using Visual Studio (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/dn584771.aspx)
- [<span data-ttu-id="809ee-205">Vorgehensweise: Erstellen und Bereitstellen von benutzerdefinierten Workflowaktionen (MSDN-Artikel)</span><span class="sxs-lookup"><span data-stu-id="809ee-205">How to: Build and deploy workflow custom actions (MSDN Article)</span></span>](https://msdn.microsoft.com/en-us/library/office/jj163911.aspx)
- [<span data-ttu-id="809ee-206">Vorgehensweise: Erstellen von benutzerdefinierten SharePoint Server 2013 Workflow-Formularen mit Visual Studio 2012 (MSDN-Artikel)</span><span class="sxs-lookup"><span data-stu-id="809ee-206">How to: Create Custom SharePoint Server 2013 Workflow Forms with Visual Studio 2012 (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/dn518136.aspx)
- [<span data-ttu-id="809ee-207">Abfragen eines Remotediensts unter Verwendung des Webproxys in SharePoint 2013 (MSDN-Artikel)</span><span class="sxs-lookup"><span data-stu-id="809ee-207">Query a remote service using the web proxy in SharePoint 2013 (MSDN Article)</span></span>](https://msdn.microsoft.com/en-us/library/office/fp179895.aspx)
- [<span data-ttu-id="809ee-208">Module (Anleitung SharePoint-Add-Ins)</span><span class="sxs-lookup"><span data-stu-id="809ee-208">Modules (SharePoint Add-in Recipe)</span></span>](modules-sharepoint-add-in.md)
- [<span data-ttu-id="809ee-209">Site-Bereitstellung (SharePoint-Add-in Anleitung)</span><span class="sxs-lookup"><span data-stu-id="809ee-209">Site provisioning (SharePoint Add-in Recipe)</span></span>](site-provisioning-sharepoint-add-in.md)
- <span data-ttu-id="809ee-210">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="809ee-210">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="809ee-211">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="809ee-211">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="809ee-212">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="809ee-212">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="809ee-213">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="809ee-213">Related PnP samples</span></span>
===================
- [<span data-ttu-id="809ee-214">Workflow.Activities (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="809ee-214">Workflow.Activities (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities)
- [<span data-ttu-id="809ee-215">Workflow.CustomEvents (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="809ee-215">Workflow.CustomEvents (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomEvents)
- [<span data-ttu-id="809ee-216">Workflow.CustomTasks (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="809ee-216">Workflow.CustomTasks (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomTasks)
- [<span data-ttu-id="809ee-217">Workflow.CallCustomService (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="809ee-217">Workflow.CallCustomService (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)
- [<span data-ttu-id="809ee-218">Workflow.CallServiceUpdateSPViaProxy (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="809ee-218">Workflow.CallServiceUpdateSPViaProxy (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)
- <span data-ttu-id="809ee-219">Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="809ee-219">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="809ee-220">Gilt für</span><span class="sxs-lookup"><span data-stu-id="809ee-220">Applies to</span></span>
==========
- <span data-ttu-id="809ee-221">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="809ee-221">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="809ee-222">Office 365 dedizierte (D)</span><span class="sxs-lookup"><span data-stu-id="809ee-222">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="809ee-223">SharePoint 2013 lokal</span><span class="sxs-lookup"><span data-stu-id="809ee-223">SharePoint 2013 on-premises</span></span>
