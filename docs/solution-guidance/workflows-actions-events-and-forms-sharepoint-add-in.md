---
title: "Workflows, Aktionen (Aktivitäten), Ereignisse und Formularen in die SharePoint-add-in-Objektmodell"
ms.date: 11/03/2017
ms.openlocfilehash: d20da3810fc6c6f0cc32eda185ec7cfd45d1f607
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="workflows-actions-activities-events-and-forms-in-the-sharepoint-add-in-model"></a>Workflows, Aktionen (Aktivitäten), Ereignisse und Formularen in die SharePoint-add-in-Objektmodell
=================================================================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Implementieren von Workflows und die damit verbundenen Komponenten unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.  In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario, Workflows und die damit verbundenen Komponenten mit serverseitigen Code erstellt und über den SharePoint-Lösungen bereitgestellt wurden.  Die Workflows und die damit verbundenen Komponenten, die für den SharePoint-Server ausgeführt werden.

In einem Modell Szenario SharePoint-Add-in Workflows und die damit verbundenen Komponenten mit Code entwickelt wurden, die auf Remoteservern ausgeführt wird.  Workflows und die damit verbundenen Komponenten mit dem Workflow-Dienst registriert sind, aber alle Code auf Remoteservern ausgeführt wird.

<a name="high-level-guidelines"></a>Hohe Stufe Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden Richtlinien auf hohen Ebenen bieten zum Erstellen von Workflows und die damit verbundenen Komponenten in das neue SharePoint-Add-in-Modell.

- CodeBehind-Workflows sind nicht verfügbar in Office 365-Mandanten oder mit dem SharePoint-Add-in-Objektmodell im Allgemeinen.
- Alle CodeBehind zugeordneten Workflows und die damit verbundenen Komponenten müssen in einem externen Webdienst auf einem Remoteserver ausgeführt platziert werden.

<a name="options-to-create-custom-workflows-and-their-associated-components"></a>Optionen zum Erstellen von benutzerdefinierten Workflows und die damit verbundenen Komponenten
------------------------------------------------------------------
Es gibt einige Optionen zum Erstellen von benutzerdefinierten Workflows und die damit verbundenen Komponenten.

- Erstellen von benutzerdefinierten workflows
- Erstellen Sie benutzerdefinierte Workflowaktivitäten
- Erstellen von benutzerdefinierten Workflow-Ereignissen
- Erstellen benutzerdefinierter Workflowformulare

<a name="create-custom-workflows"></a>Erstellen von benutzerdefinierten workflows
-----------------------
Bei dieser Option werden benutzerdefinierte Workflows erstellt, bereitgestellt und mit der Hostwebsite in SharePoint verknüpft.

- Benutzerdefinierte Workflows können mit Visual Studio oder SharePoint Designer erstellt werden.
    + Finden Sie unter [Develop SharePoint 2013-Workflows mit Visual Studio (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/office/jj163199.aspx) , die beide zusammenfasst Optionen und werden die vor- und Nachteile der einzelnen.
- Benutzerdefinierte Workflows können bereitgestellt und die Hostwebsite in SharePoint auf verschiedene Weise zugeordnet werden.
    - In Visual Studio erstellte Workflows werden automatisch innerhalb von Features für die Bereitstellung gepackt.
    - Workflows in SharePoint Designer exportiert und importiert, um diese Funktionen auf einem Entwicklungsserver für die auf einem Produktionsserver bereitstellen muss erstellt.
    - Workflows können auch bereitgestellt und die Hostwebsite in SharePoint über die remote provisioning Muster zugeordnet werden.  Finden Sie unter der [Website-Bereitstellung (SharePoint-Add-in-Anleitung)](site-provisioning-sharepoint-add-in.md) ausführliche Informationen zum remote-Bereitstellung Muster.

Im folgenden Codebeispiel wird veranschaulicht, wie CSOM zum Bereitstellen eines Workflows und die Listen die Unterstützung für den Workflow verwenden.

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

**Wenn sie geeignet ist?**

Wenn Sie zum Erstellen von benutzerdefinierten Workflows mit Code-behind sie diese Option müssen eignet sich gut.

**Erste Schritte**

In den folgenden Artikeln wird gezeigt, wie benutzerdefinierte Workflows erstellen.

- [Erstellen Sie eine SharePoint-Workflow-app mit den Visual Studio 2012 (MSDN-Artikel)](https://msdn.microsoft.com/EN-US/library/office/dn456545.aspx)
- [Vorgehensweise: Erstellen von SharePoint 2013-Workflows mit Visual Studio (MSDN-Artikel)](https://msdn.microsoft.com/EN-US/library/office/dn584771.aspx)

<a name="create-custom-workflow-activities"></a>Erstellen Sie benutzerdefinierte Workflowaktivitäten
---------------------------------
Bei dieser Option werden benutzerdefinierte Workflowaktivitäten erstellt und in SharePoint bereitgestellt.

- Benutzerdefinierte Workflowaktivitäten möglicherweise mit Visual Studio erstellt werden.
- Benutzerdefinierte Workflowaktivitäten können nicht mit SharePoint Designer erstellt werden.
- Benutzerdefinierte Workflowaktivitäten können in SharePoint Designer verwendet werden, nachdem sie eine SharePoint-Umgebung bereitgestellt werden.

**Wenn sie geeignet ist?**

Wenn Sie Workflows in Geschäftsprozessen implementieren, deren von der Out-of-Box-Bibliothek Workflowaktionen in SharePoint Designer nicht erfüllt werden, müssen

**Erste Schritte**

Im folgende Artikel veranschaulicht das Erstellen einer benutzerdefinierten Workflowaktivität mit Visual Studio.

- [Vorgehensweise: Erstellen und Bereitstellen von benutzerdefinierten Workflowaktionen (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/office/jj163911.aspx)

Die [Workflow.Activities (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) enthält mehrere benutzerdefinierte Workflowaktivitäten mit Visual Studio erstellt.  Darüber hinaus wird das Verwenden der benutzerdefinierten Workflow-Aktivitäten in einem Workflow veranschaulicht.

<a name="create-custom-workflow-events"></a>Erstellen von benutzerdefinierten Workflow-Ereignissen
-----------------------------
Bei dieser Option werden benutzerdefinierte Workflowereignisse erstellt und in SharePoint bereitgestellt.

- Benutzerdefinierte Workflow-Ereignisse können mit Visual Studio erstellt werden.
- Benutzerdefinierte Workflow-Ereignisse können nicht mit SharePoint Designer erstellt werden.
- Benutzerdefinierte Workflow-Ereignisse können in SharePoint Designer verwendet werden, nachdem sie eine SharePoint-Umgebung bereitgestellt werden.

**Wenn sie geeignet ist?**

Wenn Sie Workflows in Geschäftsprozessen implementieren, deren Anforderungen an die Workflows zu warten, bis ein benutzerdefiniertes Ereignis vor dem Fortfahren erforderlich sein, müssen.

**Erste Schritte**

Die [Workflow.CustomEvents (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomEvents) wird gezeigt, wie ein Workflow erstellt, der ein benutzerdefiniertes sogar an ausgelöst werden, bevor Sie fortfahren wartet.  Es wird veranschaulicht, wie die JavaScript Client Side-Objektmodell (JSOM) für den Workflow-Manager verwenden, um ein benutzerdefiniertes Ereignis ausgelöst wird.

<a name="create-custom-workflow-forms"></a>Erstellen benutzerdefinierter Workflowformulare
------------------------------------------------
Bei dieser Option benutzerdefinierter Workflowformulare erstellt und in SharePoint bereitgestellt.

- Benutzerdefinierter Workflowformulare möglicherweise mit Visual Studio erstellt werden.
- Benutzerdefinierter Workflowformulare können nicht mit SharePoint Designer erstellt werden.
- Benutzerdefinierter Workflowformulare können in SharePoint Designer verwendet werden, nachdem sie eine SharePoint-Umgebung bereitgestellt werden.

**Wenn sie geeignet ist?**

Wenn Sie Workflows in Geschäftsprozessen implementieren müssen erfordern, deren Anforderungen für benutzerdefinierte Formulare.

**Erste Schritte**

Im folgende Artikel veranschaulicht das Erstellen von benutzerdefinierten Workflows Zuordnungs-und Initiierungsformularen und deren Verwendung in einem Workflow.

- [Vorgehensweise: Erstellen von benutzerdefinierten SharePoint Server 2013 Workflow-Formularen mit Visual Studio 2012 (MSDN-Artikel)](https://msdn.microsoft.com/EN-US/library/office/dn518136.aspx)

Die [Workflow.CustomTasks (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomTasks) veranschaulicht das Erstellen von benutzerdefinierten Formularen für Aufgaben- und Initiierung und deren Verwendung in einem Workflow.

<a name="options-to-update-sharepoint-data-from-a-custom-workflow"></a>Optionen zum Aktualisieren von SharePoint-Daten mithilfe eines benutzerdefinierten Workflows
--------------------------------------------------------
Sie haben verschiedene Optionen zum Aktualisieren von SharePoint-Daten mithilfe eines benutzerdefinierten Workflows.

- Verwenden Sie die Kontext-Token und Web-URL-Add-in SharePoint authentifizieren.
- Verwenden Sie die Add-Ins Web-URL und den SharePoint Webproxy SharePoint authentifizieren.

<a name="use-the-context-token-and-add-in-web-url-to-authenticate-to-sharepoint"></a>Verwenden Sie die Kontext-Token und Add-Ins Web-URL zur Authentifizierung in SharePoint
----------------------------------------------------------------------

Bei dieser Option übergeben Sie den Kontext-Token und die Add-in-Web-URL der Workflow mit dem Dienst der Workflow ruft über HTTP-Header.  Der Dienst verwendet die Kontext-Token und Add-Ins Web-URL zur Authentifizierung in SharePoint und ein Zugriffstoken vor dem Aktualisieren von SharePoint-Daten zurückgeben. 

- Bei diesem Ansatz müssen, und übergeben Sie das Content Token an den Webdienst aus dem Workflow.

**Wenn sie geeignet ist?**

Wenn Sie die Kommunikation mit SharePoint auf Ebene der Client möchten.

**Erste Schritte**

Im folgende Beispiel wird gezeigt, wie Sie mit den Kontext-Token und die Add-in-Web-URL zur Authentifizierung in SharePoint und SharePoint-Daten zu aktualisieren.

- [Workflow.CallCustomService (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)

Finden Sie im Abschnitt [aufrufen Web API-Diensts](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService#call-web-api-service) in der Infodatei [Workflow.CallCustomService (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) ausführliche Informationen zu den Kontext-Token und die Add-in-Web-URL aus dem Workflow an den Dienst übergeben.

Die anderen Abschnitte in der Infodatei [Workflow.CallCustomService (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) enthalten detaillierte Informationen zu den gesamten Workflow und remote-Dienst und führen Sie auch durch alle Komponenten in Microsoft Azure einrichten.

<a name="use-the-add-in-web-url-and-the-sharepoint-web-proxy-to-authenticate-to-sharepoint"></a>Verwenden Sie die Add-Ins Web-URL und den SharePoint Webproxy zur Authentifizierung in SharePoint
---------------------------------------------------------------------------------

In diese Option, wenn der Workflow gestartet wird, die Sie übergeben Sie der Add-Ins Web-URL aus dem Workflow mit dem Dienst den Workflow aufruft.  Der Dienst übergibt die Add-in-Web-URL an den SharePoint Web Proxy.  SharePoint-Web-Proxy verwendet die Add-Ins Web-URL zur Authentifizierung in SharePoint und ein Zugriffstoken zurückzugeben.  Klicken Sie dann fügt den SharePoint Web Proxy das Zugriffstoken an die HTTP-Header vor dem aufrufen, SharePoint-Daten zu aktualisieren.

- Dieser Ansatz ist kein erforderlich und übergeben Sie das Content Token an den Webdienst aus dem Workflow.

**Wenn sie geeignet ist?**

Wenn Sie die Kommunikation mit SharePoint erfolgt auf Serverebene möchten.

**Erste Schritte**

Das folgende Beispiel veranschaulicht, wie Sie die Add-Ins Web-URL und den SharePoint Webproxy zur Authentifizierung in SharePoint und SharePoint-Daten zu aktualisieren.

- [Workflow.CallServiceUpdateSPViaProxy (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)

Finden Sie im Abschnitt [rufen Sie Web-Api-Dienst über den Webproxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy#call-web-api-service-via-web-proxy) [Workflow.CallServiceUpdateSPViaProxy (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) Infodatei Nähere Informationen zu den SharePoint Web Proxy-Aufruf.

Die anderen Abschnitte in der Infodatei [Workflow.CallServiceUpdateSPViaProxy (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) enthalten detaillierte Informationen zu den gesamten Workflow und remote-Dienst und führen Sie auch durch alle Komponenten in Microsoft Azure einrichten.

Finden Sie unter die [Abfrage einem Remotedienst mithilfe des Webproxys in SharePoint 2013 (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/office/fp179895.aspx) Weitere Informationen zu den SharePoint Web Proxy.

<a name="related-links"></a>Verwandte links
=============
- [SharePoint 2013 Workflow-Objektmodell (MSDN-Artikel)](https://msdn.microsoft.com/EN-US/library/office/jj163969.aspx)
- [Häufige Fehlermeldungen in SharePoint Workflow Development (MSDN-Artikel)](https://msdn.microsoft.com/EN-US/library/office/dn449112.aspx)
- [Verwenden von Workflow-Interop für SharePoint 2013 (MSDN-Artikel)](https://msdn.microsoft.com/EN-US/library/office/jj670125.aspx)
- [Entwickeln von SharePoint 2013-Workflows mit Visual Studio (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/office/jj163199.aspx)
- [Site-Bereitstellung (SharePoint-Add-in Anleitung)](site-provisioning-sharepoint-add-in.md)
- [Erstellen Sie eine SharePoint-Workflow-app mit den Visual Studio 2012 (MSDN-Artikel)](https://msdn.microsoft.com/EN-US/library/office/dn456545.aspx)
- [Vorgehensweise: Erstellen von SharePoint 2013-Workflows mit Visual Studio (MSDN-Artikel)](https://msdn.microsoft.com/EN-US/library/office/dn584771.aspx)
- [Vorgehensweise: Erstellen und Bereitstellen von benutzerdefinierten Workflowaktionen (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/office/jj163911.aspx)
- [Vorgehensweise: Erstellen von benutzerdefinierten SharePoint Server 2013 Workflow-Formularen mit Visual Studio 2012 (MSDN-Artikel)](https://msdn.microsoft.com/EN-US/library/office/dn518136.aspx)
- [Abfragen eines Remotediensts unter Verwendung des Webproxys in SharePoint 2013 (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/office/fp179895.aspx)
- [Module (Anleitung SharePoint-Add-Ins)](modules-sharepoint-add-in.md)
- [Site-Bereitstellung (SharePoint-Add-in Anleitung)](site-provisioning-sharepoint-add-in.md)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================
- [Workflow.Activities (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities)
- [Workflow.CustomEvents (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomEvents)
- [Workflow.CustomTasks (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomTasks)
- [Workflow.CallCustomService (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)
- [Workflow.CallServiceUpdateSPViaProxy (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)
- Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D)
- SharePoint 2013 lokal
