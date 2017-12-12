---
title: SharePoint-Workflow-Objektmodell
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: be615a89-3201-4cd8-bbc7-15f3abf9f668
ms.openlocfilehash: 02434d1a009b54ad971145d53cb1c47b52a096ad
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-workflow-object-model"></a><span data-ttu-id="edcd7-102">SharePoint-Workflow-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="edcd7-102">SharePoint workflow object model</span></span>
<span data-ttu-id="edcd7-103">Rufen Sie eine kurze Einführung in das Workflowobjektmodell in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="edcd7-103">Get a brief introduction to the workflow object model in SharePoint.</span></span>
## <a name="sharepoint-workflow-object-model"></a><span data-ttu-id="edcd7-104">SharePoint-Workflow-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="edcd7-104">SharePoint workflow object model</span></span>
<span data-ttu-id="edcd7-105"><a name="bk_SPwfom"> </a></span><span class="sxs-lookup"><span data-stu-id="edcd7-105"><a name="bk_SPwfom"> </a></span></span>

<span data-ttu-id="edcd7-p101">Das SharePoint-Objektmodell basiert auf der Basis des .NET Framework 4-Objektmodells für Windows Workflow Foundation 4, jedoch mit Innovationen, die in SharePoint-Workflowfunktionen im Allgemeinen und in SharePoint-Add-Ins insbesondere ermöglichen. Das systemeigene .NET Framework 4-Objektmodell für Windows Workflow Foundation 4 befindet sich in der .NET Framework  [System.Workflow Namespaces](http://msdn.microsoft.com/de-DE/library/gg145026.aspx).</span><span class="sxs-lookup"><span data-stu-id="edcd7-p101">The SharePoint object model is built on top of the .NET Framework 4 object model for Windows Workflow Foundation 4, but with innovations that enable workflow functionality in SharePoint generally, and in SharePoint Add-ins in particular. The native .NET Framework 4 object model for Windows Workflow Foundation 4 is located in the .NET Framework  [System.Workflow namespaces](http://msdn.microsoft.com/de-DE/library/gg145026.aspx).</span></span>
  
    
    
<span data-ttu-id="edcd7-p102">Eine Möglichkeit, die SharePoint-Workflow-Objektmodell vorstellen ist als eine Reihe von Workflow-Dienste. Es gibt vier Dienste:</span><span class="sxs-lookup"><span data-stu-id="edcd7-p102">One way to think of the SharePoint workflow object model is as a set of workflow services. There are four services:</span></span> 
  
    
    

- <span data-ttu-id="edcd7-110">**Instanz Verwaltungsdienst:** Verwaltet den Workflow-Instanzen und deren Ausführung.</span><span class="sxs-lookup"><span data-stu-id="edcd7-110">**Instance management service:** Manages workflow instances and their execution.</span></span>
    
  
- <span data-ttu-id="edcd7-111">**Deployment-Dienst:** Verwaltet die Bereitstellung von workflowdefinitionen für.</span><span class="sxs-lookup"><span data-stu-id="edcd7-111">**Deployment service:** Manages the deployment of workflow definitions.</span></span>
    
  
- <span data-ttu-id="edcd7-112">**Interop-Dienst:** Verwaltet die Interop-Brücke zur Unterstützung von legacy-Workflows.</span><span class="sxs-lookup"><span data-stu-id="edcd7-112">**Interop service:** Manages the interop bridge for supporting legacy workflows.</span></span>
    
  
- <span data-ttu-id="edcd7-113">**Messaging-Dienst:** Verwaltet Message queuing und Transport.</span><span class="sxs-lookup"><span data-stu-id="edcd7-113">**Messaging service:** Manages message queuing and transport.</span></span>
    
  

### <a name="sharepoint-workflow-namespaces"></a><span data-ttu-id="edcd7-114">Namespaces für die SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="edcd7-114">SharePoint workflow namespaces</span></span>

<span data-ttu-id="edcd7-115">Das Objektmodell der SharePoint-Workflow ist andererseits, in zehn Namespaces enthalten: fünf davon sind SharePoint-Namespaces und fünf andere Microsoft Office Namespaces sind.</span><span class="sxs-lookup"><span data-stu-id="edcd7-115">The SharePoint workflow object model, on the other hand, is contained in ten namespaces: five of them are SharePoint namespaces, and five others are Microsoft Office namespaces.</span></span>
  
    
    
 <span data-ttu-id="edcd7-116">**Microsoft.SharePoint** -Namespaces:</span><span class="sxs-lookup"><span data-stu-id="edcd7-116">**Microsoft.SharePoint** namespaces:</span></span>
  
    
    

-  [<span data-ttu-id="edcd7-117">Microsoft.SharePoint.Workflow</span><span class="sxs-lookup"><span data-stu-id="edcd7-117">Microsoft.SharePoint.Workflow</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Workflow.aspx)
    
  
-  [<span data-ttu-id="edcd7-118">Microsoft.SharePoint.Workflow.Application</span><span class="sxs-lookup"><span data-stu-id="edcd7-118">Microsoft.SharePoint.Workflow.Application</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Workflow.Application.aspx)
    
  
-  [<span data-ttu-id="edcd7-119">Microsoft.SharePoint.WorkflowActions</span><span class="sxs-lookup"><span data-stu-id="edcd7-119">Microsoft.SharePoint.WorkflowActions</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.aspx)
    
  
-  [<span data-ttu-id="edcd7-120">Microsoft.SharePoint.WorkflowActions.WithKey</span><span class="sxs-lookup"><span data-stu-id="edcd7-120">Microsoft.SharePoint.WorkflowActions.WithKey</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.WithKey.aspx)
    
  
-  [<span data-ttu-id="edcd7-121">Microsoft.SharePoint.WorkflowServices</span><span class="sxs-lookup"><span data-stu-id="edcd7-121">Microsoft.SharePoint.WorkflowServices</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.aspx)
    
  
-  [<span data-ttu-id="edcd7-122">Microsoft.SharePoint.WorkflowServices.Activities</span><span class="sxs-lookup"><span data-stu-id="edcd7-122">Microsoft.SharePoint.WorkflowServices.Activities</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.aspx)
    
  
 <span data-ttu-id="edcd7-123">**Microsoft.Office** -Namespaces:</span><span class="sxs-lookup"><span data-stu-id="edcd7-123">**Microsoft.Office** namespaces:</span></span>
  
    
    

-  [<span data-ttu-id="edcd7-124">Microsoft.Office.Workflow</span><span class="sxs-lookup"><span data-stu-id="edcd7-124">Microsoft.Office.Workflow</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.aspx)
    
  
-  [<span data-ttu-id="edcd7-125">Microsoft.Office.Workflow.Actions</span><span class="sxs-lookup"><span data-stu-id="edcd7-125">Microsoft.Office.Workflow.Actions</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Actions.aspx)
    
  
-  [<span data-ttu-id="edcd7-126">Microsoft.Office.Workflow.Feature</span><span class="sxs-lookup"><span data-stu-id="edcd7-126">Microsoft.Office.Workflow.Feature</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Feature.aspx)
    
  
-  [<span data-ttu-id="edcd7-127">Microsoft.Office.Workflow.Routing</span><span class="sxs-lookup"><span data-stu-id="edcd7-127">Microsoft.Office.Workflow.Routing</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Routing.aspx)
    
  
-  [<span data-ttu-id="edcd7-128">Microsoft.Office.Workflow.Utility</span><span class="sxs-lookup"><span data-stu-id="edcd7-128">Microsoft.Office.Workflow.Utility</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Utility.aspx)
    
  

### <a name="sharepoint-workflow-schemas"></a><span data-ttu-id="edcd7-129">SharePoint-Workflow-schemas</span><span class="sxs-lookup"><span data-stu-id="edcd7-129">SharePoint workflow schemas</span></span>

<span data-ttu-id="edcd7-130">Verweis Inhalte für SharePoint-Schemas in den Anspruch  [Workflowschemas](http://msdn.microsoft.com/library/b36ded16-3ffd-4931-811e-c402c1e35b07%28Office.15%29.aspx)Verweisknoten enthalten ist, und folgende enthalten:</span><span class="sxs-lookup"><span data-stu-id="edcd7-130">Reference content for SharePoint schemas is contained in the reference node entitled  [Workflow schemas](http://msdn.microsoft.com/library/b36ded16-3ffd-4931-811e-c402c1e35b07%28Office.15%29.aspx), and contain the following:</span></span>
  
    
    

-  [<span data-ttu-id="edcd7-131">WorkflowActions4-Schemareferenz</span><span class="sxs-lookup"><span data-stu-id="edcd7-131">WorkflowActions4 schema reference</span></span>](http://msdn.microsoft.com/library/1c0112de-0139-e64d-d3d6-658541695391%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="edcd7-132">WorkflowActions3-Schemareferenz</span><span class="sxs-lookup"><span data-stu-id="edcd7-132">WorkflowActions3 schema reference</span></span>](http://msdn.microsoft.com/library/7a03ead8-30e0-4601-9c6f-edfb04ce57f9%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="edcd7-133">Übersicht zum Workflowkonfigurationsschema</span><span class="sxs-lookup"><span data-stu-id="edcd7-133">Workflow configuration schema reference</span></span>](http://msdn.microsoft.com/library/63824239-6eb2-4cf1-ba84-44eace4d3781%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="edcd7-134">WorkflowInfo-Schemareferenz</span><span class="sxs-lookup"><span data-stu-id="edcd7-134">WorkflowInfo schema reference</span></span>](http://msdn.microsoft.com/library/f3bdcc70-15a0-44b2-9b01-330f13430354%28Office.15%29.aspx)
    
  

## <a name="see-also"></a><span data-ttu-id="edcd7-135">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="edcd7-135">See also</span></span>
<span data-ttu-id="edcd7-136"><a name="bk_additionalresources"> </a></span><span class="sxs-lookup"><span data-stu-id="edcd7-136"><a name="bk_additionalresources"> </a></span></span>


-  [<span data-ttu-id="edcd7-137">Einführung für Entwickler für Windows Workflow Foundation (WF) in .NET 4</span><span class="sxs-lookup"><span data-stu-id="edcd7-137">A Developer's Introduction to Windows Workflow Foundation (WF) in .NET 4</span></span>](http://msdn.microsoft.com/de-DE/library/ee342461.aspx)
    
  
-  [<span data-ttu-id="edcd7-138">Windows Workflow Foundation 4.0: Hello, Workflow!</span><span class="sxs-lookup"><span data-stu-id="edcd7-138">Windows Workflow Foundation 4.0: Hello, workflow!</span></span>](http://weblogs.asp.net/gunnarpeipman/archive/2009/07/08/windows-workflow-foundation-4-0-hello-workflow.aspx)
    
  
-  [<span data-ttu-id="edcd7-139">Windows Workflow Foundation (WF) - Screencasts</span><span class="sxs-lookup"><span data-stu-id="edcd7-139">Windows Workflow Foundation (WF) Screencasts</span></span>](http://msdn.microsoft.com/de-DE/netframework/dd733248)
    
  
-  [<span data-ttu-id="edcd7-140">Workflowaktions- und -aktivitätenreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="edcd7-140">Workflow actions and activities reference for SharePoint</span></span>](workflow-actions-and-activities-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="edcd7-141">Entwickeln von SharePoint-Workflows mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="edcd7-141">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio.md)
    
  

  
    
    

