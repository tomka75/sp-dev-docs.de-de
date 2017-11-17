---
title: Verstehen von Koordinationsaktionen in SharePoint Designer 2013
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 33fbcf91-0a5d-47ab-85a9-9d2d556a204d
ms.openlocfilehash: 95a8e8ad85a2f60b81a4b58a2305f3f6dae00187
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="understanding-coordination-actions-in-sharepoint-designer-2013"></a><span data-ttu-id="5d568-102">Verstehen von Koordinationsaktionen in SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="5d568-102">Understanding Coordination actions in SharePoint Designer 2013</span></span>
<span data-ttu-id="5d568-103">Koordinationsaktionen in SharePoint Designer 2013 dienen zum Starten eines Workflows, die auf der SharePoint 2010-Workflow-Plattform von innerhalb eines Workflows auf der SharePoint-Workflow-Plattform integriert.</span><span class="sxs-lookup"><span data-stu-id="5d568-103">Coordination Actions in SharePoint Designer 2013 are designed to start a workflow built on the SharePoint 2010 Workflow platform from within a workflow built on the SharePoint Workflow platform.</span></span>

   

## <a name="coordination-actions-in-sharepoint-designer-2013"></a><span data-ttu-id="5d568-104">Koordinierungsaktionen in SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="5d568-104">Coordination Actions in SharePoint Designer 2013</span></span>
<span data-ttu-id="5d568-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="5d568-105"></span></span>

<span data-ttu-id="5d568-p101">Es sind zwei Koordinationsaktionen in SharePoint Designer 2013 verfügbar. Beide Aktionen sind nur für die SharePoint-Workflow-Plattform verfügbar. Diese Aktionen sind:</span><span class="sxs-lookup"><span data-stu-id="5d568-p101">There are two Coordination Actions available in SharePoint Designer 2013. Both actions are only available for the SharePoint Workflow platform. These actions are:</span></span>
  
    
    

- <span data-ttu-id="5d568-109">Listenworkflow starten: zum Starten eines Workflows für eine bestimmte Liste entwickelt wurde.</span><span class="sxs-lookup"><span data-stu-id="5d568-109">Start a List Workflow: Used to start a workflow developed for a specific list.</span></span>
    
  
- <span data-ttu-id="5d568-110">Starten Sie einen Website-Workflow: zum Starten eines Workflows für die Website entwickelt wurden.</span><span class="sxs-lookup"><span data-stu-id="5d568-110">Start a Site Workflow: Used to start a workflow developed for the site.</span></span>
    
  
<span data-ttu-id="5d568-111">Koordinierung Aktionen werden im Dropdown-Menü **Aktionen** angezeigt, bei der Erstellung eines Workflows basierend auf der SharePoint-Workflow-Plattform, wie in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="5d568-111">Coordination Actions appear in the **Actions** drop-down menu when you build a workflow based on the SharePoint Workflow platform, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="5d568-112">**Abbildung: Koordinierungsaktionen in SharePoint Designer**</span><span class="sxs-lookup"><span data-stu-id="5d568-112">**Figure: Coordination Actions in SharePoint Designer**</span></span>

  
    
    

  
    
    
![Koordinierungsaktionen in SharePoint Designer](../images/SPD15-CoordinationActions.png)
  
    
    
<span data-ttu-id="5d568-114">Beide Aktionen dienen zum Starten eines Workflows, die auf der SharePoint 2010-Workflow-Plattform mithilfe eines Workflows auf der SharePoint-Workflow-Plattform integriert.</span><span class="sxs-lookup"><span data-stu-id="5d568-114">Both actions are designed to start a workflow built on the SharePoint 2010 Workflow platform from a workflow built on the SharePoint Workflow platform.</span></span>
  
    
    

    
> <span data-ttu-id="5d568-115">**Wichtig:** Die Koordinationsaktionen unterstützen nur das Aufrufen eines auf der SharePoint 2010-Workflowplattform basierten Workflows von einem auf der SharePoint-Workflowplattform basierten Workflow.</span><span class="sxs-lookup"><span data-stu-id="5d568-115">**Important** The coordination actions only support starting a workflow based on the SharePoint 2010 Workflow platform from a workflow based on the SharePoint Workflow platform. Starting a workflow built on the SharePoint Workflow platform from within a workflow built on the same platform is not supported.</span></span> <span data-ttu-id="5d568-116">Das Aufrufen eines auf der SharePoint-Workflowplattform basierten Workflows von einem auf derselben Plattform basierten Workflow wird nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="5d568-116">Important The coordination actions only support starting a workflow based on the SharePoint 2010 Workflow platform from a workflow based on the SharePoint Workflow platform. Starting a workflow built on the SharePoint Workflow platform from within a workflow built on the same platform is not supported.</span></span> 
  
    
    


## <a name="using-coordination-actions"></a><span data-ttu-id="5d568-117">Verwenden von Koordinationsaktionen</span><span class="sxs-lookup"><span data-stu-id="5d568-117">Using Coordination Actions</span></span>
<span data-ttu-id="5d568-118"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="5d568-118"></span></span>

<span data-ttu-id="5d568-p103">Es gibt eine Reihe von Aktionen, die in der SharePoint Workflow-Plattform veraltet sind. Legacy-Workflows zur Erfüllung können Sie Koordinationsaktionen verwenden. Koordinationsaktionen dienen zum Starten einer Listenworkflow oder Website-Workflow, der mithilfe der SharePoint 2010-Workflow-Plattform erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="5d568-p103">There are a number of actions that have been deprecated in the SharePoint Workflow platform. To accommodate legacy workflows you can use Coordination Actions. Coordination Actions can be used to start a List workflow or a Site workflow that has been built by using the SharePoint 2010 Workflow platform.</span></span>
  
    
    
<span data-ttu-id="5d568-122">Eine Aktion Koordinierung umfasst drei bearbeitbare Bereichen wie in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="5d568-122">A Coordination Action includes three editable regions, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="5d568-123">**Abbildung: Starten einer Listenworkflow-koordinierungsaktion**</span><span class="sxs-lookup"><span data-stu-id="5d568-123">**Figure: Start a List Workflow coordination action**</span></span>

  
    
    

  
    
    
![Starten einer Listenworkflow-Koordinierungsaktion](../images/SPD15-CoordinationActions2.png)
  
    
    
<span data-ttu-id="5d568-125">Die drei bearbeitbaren Bereiche sind:</span><span class="sxs-lookup"><span data-stu-id="5d568-125">The three editable regions are:</span></span> 
  
    
    

- <span data-ttu-id="5d568-126">**Workflow für SharePoint 2010** Wählen Sie den zu startenden Workflow 2010 aus.</span><span class="sxs-lookup"><span data-stu-id="5d568-126">**SharePoint 2010 list workflow** Select the 2010 workflow to start.</span></span>
    
  
- <span data-ttu-id="5d568-127">**Parameter** Parameter zum Senden an die 2010-Workflows.</span><span class="sxs-lookup"><span data-stu-id="5d568-127">**parameters** Parameters to send to the 2010 workflow.</span></span>
    
  
- <span data-ttu-id="5d568-128">**dieses Element** Das Element der 2010-Workflows ausgeführt werden soll, klicken Sie auf.</span><span class="sxs-lookup"><span data-stu-id="5d568-128">**this item** The item which the 2010 workflow should be run on.</span></span>
    
  
<span data-ttu-id="5d568-p104">Klicken Sie auf einen bearbeitbaren Link, um Informationen eingeben. Klicken Sie auf den Link **SharePoint 2010-Listenworkflow** beispielsweise markieren Sie den zu startenden Workflow 2010. Ein Dialogfeld angezeigt wird, wählen Sie den Workflow verwendet werden, wie in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="5d568-p104">Click an editable link to enter information. For example, to select the 2010 workflow to start, click the link **SharePoint 2010 list workflow**. A dialog box appears that can be used to select the workflow, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="5d568-132">**Abbildung: Auswählen eines Workflows basierend auf der 2010-Plattform**</span><span class="sxs-lookup"><span data-stu-id="5d568-132">**Figure: Selecting a workflow based on the 2010 platform**</span></span>

  
    
    

  
    
    
![Auswählen eines Workflows basierend auf der 2010-Plattform](../images/SPD15-CoordinationActions3.png)
  
    
    

  
    
    

  
    
    

  
    
    
<span data-ttu-id="5d568-134">SharePoint 2010-Workflow-Plattform Workflow-Instanzen, die innerhalb eines SharePoint-Workflows aus koordiniert werden werden auf der Workflowstatusseite im Abschnitt Statusseite aufgelistet, wie in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="5d568-134">The SharePoint 2010 Workflow platform workflow instances that are coordinated from within a SharePoint workflow are listed on the workflow status page in the Subworkflows section, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="5d568-135">**Abbildung: Workflow-Statusseite Listet die untergeordneten Workflows**</span><span class="sxs-lookup"><span data-stu-id="5d568-135">**Figure: The workflow status page lists the subworkflows**</span></span>

  
    
    

  
    
    
![Auf der Workflowstatusseite sind die Unterworkflows aufgeführt.](../images/SPD15-CorrelationActions4.png)
  
    
    

  
    
    

  
    
    

## <a name="additional-resources"></a><span data-ttu-id="5d568-137">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="5d568-137">Additional resources</span></span>
<span data-ttu-id="5d568-138"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="5d568-138"></span></span>


-  [<span data-ttu-id="5d568-139">Neu in SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="5d568-139">What's new in workflow in SharePoint Server 2013</span></span>](http://msdn.microsoft.com/library/6ab8a28b-fa2f-4530-8b55-a7f663bf15ea.aspx)
    
  
-  [<span data-ttu-id="5d568-140">Erste Schritte mit SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="5d568-140">Getting started with SharePoint Server 2013 workflow</span></span>](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)
    
  
-  [<span data-ttu-id="5d568-141">Verstehen von Wörterbuchaktionen in SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="5d568-141">Understanding Dictionary actions in SharePoint Designer 2013</span></span>](understanding-dictionary-actions-in-sharepoint-designer.md)
    
  

  
    
    

