---
title: "Workflowaktions- und -aktivitätenreferenz für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 88e09f75-480f-4a68-87a6-b496350345cc
ms.openlocfilehash: 4f808bbc0e8d6f08d2779a1e3d6b2343f9a5dd01
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="workflow-actions-and-activities-reference-for-sharepoint"></a><span data-ttu-id="606cc-102">Workflowaktions- und -aktivitätenreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="606cc-102">Workflow actions and activities reference for SharePoint</span></span>
<span data-ttu-id="606cc-103">Erfahren Sie mehr über die Workflowaktionen, die für das Erstellen von Workflows in SharePoint Designer 2013 verfügbar sind, und über die Workflowaktivitätsklassen, die für Workflowentwickler zur Verfügung stehen, die Visual Studio 2012 verwenden.</span><span class="sxs-lookup"><span data-stu-id="606cc-103">Learn about the workflow actions that are available for workflow authoring in SharePoint Designer 2013, and the workflow activity classes that are available to workflow developers using Visual Studio 2012.</span></span>
## <a name="workflow-activities-and-actions"></a><span data-ttu-id="606cc-104">Workflowaktivitäten und -aktionen</span><span class="sxs-lookup"><span data-stu-id="606cc-104">Workflow activities and actions</span></span>
<span data-ttu-id="606cc-105"><a name="bkm_Activities"> </a></span><span class="sxs-lookup"><span data-stu-id="606cc-105"><a name="bkm_Activities"> </a></span></span>

<span data-ttu-id="606cc-p101">Workflowaktivitäten sind die Objekte auf Codeebene, die Methodenaufrufe der verschiedenen APIs verarbeiten, welche für das Workflowverhalten verantwortlich sind. Sie verwenden Workflowaktivitäten im Code, indem Sie oder eine andere Entwicklungsumgebung verwenden.</span><span class="sxs-lookup"><span data-stu-id="606cc-p101">Workflow activities represent the code-level objects that handle method calls to the various APIs that drive workflow behaviors. You interact with workflow activities in code, using or another development environment.</span></span>
  
    
    
<span data-ttu-id="606cc-108">Eine Liste der verfügbaren Aktivitäten finden Sie unter  [Aktivität Workflowklassen in SharePoint](workflow-activity-classes-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="606cc-108">For a list of available activities, see  [Workflow activity classes in SharePoint](workflow-activity-classes-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="606cc-p102">Im Gegensatz dazu sind Workflowaktionen Wrapperobjekte, die diese zugrunde liegenden Aktivitäten kapseln und sie in einer benutzerfreundlichen Form in SharePoint Designer darstellen. Sie verwenden die Workflowaktionen in SharePoint Designer.</span><span class="sxs-lookup"><span data-stu-id="606cc-p102">On the other hand, workflow actions are wrapper objects that encapsulate these underlying activities and present them in a user-friendly form in SharePoint Designer. You interact with workflow actions in SharePoint Designer.</span></span>
  
    
    
<span data-ttu-id="606cc-111">Eine Liste der verfügbaren Workflowaktionen finden Sie unter  [Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)](workflow-actions-quick-reference-sharepoint-workflow-platform.md) und [Verwendung der Interop-Workflow-Brücke verfügbar Workflowaktionen](workflow-actions-available-using-the-workflow-interop-bridge.md).</span><span class="sxs-lookup"><span data-stu-id="606cc-111">For a list of available workflow actions, see  [Workflow actions quick reference (SharePoint Workflow platform)](workflow-actions-quick-reference-sharepoint-workflow-platform.md) and [Workflow actions available using the workflow interop bridge](workflow-actions-available-using-the-workflow-interop-bridge.md).</span></span>
  
    
    

## <a name="windows-workflow-foundation-40-activities"></a><span data-ttu-id="606cc-112">Windows Workflow Foundation 4.0-Aktivitäten</span><span class="sxs-lookup"><span data-stu-id="606cc-112">Windows Workflow Foundation 4.0 activities</span></span>
<span data-ttu-id="606cc-113"><a name="bkm_WF4"> </a></span><span class="sxs-lookup"><span data-stu-id="606cc-113"><a name="bkm_WF4"> </a></span></span>

<span data-ttu-id="606cc-p103">Obwohle Ihnen auf der SharePoint-Plattform und -Infrastruktur speziell für die Erstellung benutzerefinierter SharePoint-Workflows ausgelegte Aktivitätsklassen zur Verfügung stehen, können Sie auch die von Windows Workflow Foundation (WF) 4.0 bereitgestellten Aktivitätsklassen verwenden. Diese WF 4.0-Aktivitätsklassen stehen im Microsoft .NET Framework 4 im  [System.Activities.Statements](http://msdn.microsoft.com/de-DE/library/system.activities.statements.aspx)-Namespace zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="606cc-p103">Although the SharePoint platform and infrastructure provide you with specially crafted activity classes for creating custom SharePoint workflows, you can also use any of the activities that are provided by Windows Workflow Foundation (WF) 4.0. These WF 4.0 activity classes are available in the Microsoft .NET Framework 4 in the  [System.Activities.Statements](http://msdn.microsoft.com/de-DE/library/system.activities.statements.aspx) namespace.</span></span>
  
    
    
<span data-ttu-id="606cc-p104">Die WF 4.0-Aktivitätsklassen stellen einige nützliche Features bereit, die Sie in der SharePoint-Aktivitätsklassenbibliothek möglicherweise nicht finden. So beinhaltet WF 4.0 zum Beispiel die **If**-Klasse, mit der Sie bedingte Aktivitäten erstellen können. Darüber hinaus können Sie mit der  [System.ServiceModel.Activities.Send](http://msdn.microsoft.com/de-DE/library/system.servicemodel.activities.send.aspx)-Aktivität eine Verbindung zu Webdienten herstellen.</span><span class="sxs-lookup"><span data-stu-id="606cc-p104">The WF 4.0 activity classes provide some useful features that you may not find in the SharePoint activity class library. For example, WF 4.0 includes the **If** class, which allows you to create conditional activities. Additionally, you can use the [System.ServiceModel.Activities.Send](http://msdn.microsoft.com/de-DE/library/system.servicemodel.activities.send.aspx) activity to connect to web services.</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="606cc-119">Inhalt dieses Abschnitts</span><span class="sxs-lookup"><span data-stu-id="606cc-119">In this section</span></span>
<span data-ttu-id="606cc-120"><a name="bkm_inthissection"> </a></span><span class="sxs-lookup"><span data-stu-id="606cc-120"><a name="bkm_inthissection"> </a></span></span>


-  [<span data-ttu-id="606cc-121">Aktivität Workflowklassen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="606cc-121">Workflow activity classes in SharePoint</span></span>](workflow-activity-classes-in-sharepoint.md)
    
  
-  [<span data-ttu-id="606cc-122">Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)</span><span class="sxs-lookup"><span data-stu-id="606cc-122">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  
-  [<span data-ttu-id="606cc-123">Verwendung der Interop-Workflow-Brücke verfügbar Workflowaktionen</span><span class="sxs-lookup"><span data-stu-id="606cc-123">Workflow actions available using the workflow interop bridge</span></span>](workflow-actions-available-using-the-workflow-interop-bridge.md)
    
  

## <a name="see-also"></a><span data-ttu-id="606cc-124">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="606cc-124">See also</span></span>
<span data-ttu-id="606cc-125"><a name="bkm_addlres"> </a></span><span class="sxs-lookup"><span data-stu-id="606cc-125"><a name="bkm_addlres"> </a></span></span>


-  [<span data-ttu-id="606cc-126">Entwickeln von SharePoint-Workflows mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="606cc-126">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio.md)
    
  
-  [<span data-ttu-id="606cc-127">Grundlegendes zu SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="606cc-127">SharePoint workflow fundamentals</span></span>](sharepoint-workflow-fundamentals.md)
    
  
-  [<span data-ttu-id="606cc-128">Workflows in SharePoint</span><span class="sxs-lookup"><span data-stu-id="606cc-128">Workflows in SharePoint</span></span>](workflows-in-sharepoint.md)
    
  

