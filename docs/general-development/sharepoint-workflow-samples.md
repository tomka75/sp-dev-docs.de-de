---
title: SharePoint-Workflowbeispiele
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ffaccd6b-426d-4ca0-b62f-bc7b14641a49
ms.openlocfilehash: 42abbc0a0b8e1ae8522092fce06452429cf673b7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-workflow-samples"></a><span data-ttu-id="a474c-102">SharePoint-Workflowbeispiele</span><span class="sxs-lookup"><span data-stu-id="a474c-102">SharePoint workflow samples</span></span>
<span data-ttu-id="a474c-103">Stellt Beispiel-Workflows bereit, die verdeutlichen, wie SharePoint-Workflows im neuen Workflow-Manager-Client 1.0 -Framework erstellt und implementiert werden können.</span><span class="sxs-lookup"><span data-stu-id="a474c-103">Provides sample workflows to help illustrate how to create and implement SharePoint workflows in the new Workflow Manager Client 1.0 framework.</span></span>
## <a name="workflow-samples-for-sharepoint"></a><span data-ttu-id="a474c-104">Workflow-Beispiele für SharePoint</span><span class="sxs-lookup"><span data-stu-id="a474c-104">Workflow samples for SharePoint</span></span>
<span data-ttu-id="a474c-105"><a name="bkm_wfsamples"> </a></span><span class="sxs-lookup"><span data-stu-id="a474c-105"></span></span>

<span data-ttu-id="a474c-p101">Diese Reihe von Beispiel-Workflows wurde entwickelt, um das breite Spektrum an Workflow-Funktionen in SharePoint aufzuzeigen. Sie wurden mit Visual Studio 2012 entwickelt und sie sind in der  [MSDN-Beispielgalerie](http://code.msdn.microsoft.com/) verfügbar. Dort befinden sich auch Links zu den einzelnen Beispielen.</span><span class="sxs-lookup"><span data-stu-id="a474c-p101">This series of sample workflows was developed to demonstrate the large range of workflow capabilities in SharePoint. They were developed using Visual Studio 2012 and are available in the  [MSDN Samples Gallery](http://code.msdn.microsoft.com/). Links to the individual samples are provided.</span></span>
  
    
    

### <a name="sharepoint-workflow-call-an-external-web-service"></a><span data-ttu-id="a474c-109">SharePoint-Workflow: Aufrufen eines externen Webdiensts</span><span class="sxs-lookup"><span data-stu-id="a474c-109">SharePoint workflow: Call an external web service</span></span>

<span data-ttu-id="a474c-p102">Dieses Beispiel verwendet Visual Studio, um das Erstellen eines Workflows aufzuzeigen, der mit der **HttpGet**-Aktivität einen externen Webdienst aufruft. Beim Aufrufen des Webdienstes verwendet der Workflow außerdem den neuen Datentyp **DynamicValue**.</span><span class="sxs-lookup"><span data-stu-id="a474c-p102">This sample uses Visual Studio to demonstrate creating a workflow that calls an external web service using the **HttpGet** activity. In calling the web service, the workflow also uses the new **DynamicValue** data type.</span></span>
  
    
    
<span data-ttu-id="a474c-112">Das Beispiel und eine Infodatei sind hier verfügbar:  [SharePoint-Workflow: Aufrufen eines externen Webdiensts](http://code.msdn.microsoft.com/SharePoint-workflow-48ea87d4)</span><span class="sxs-lookup"><span data-stu-id="a474c-112">The sample, along with a readme file, is available here:  [SharePoint workflow: Call an external web service](http://code.msdn.microsoft.com/SharePoint-workflow-48ea87d4)</span></span>
  
    
    

### <a name="sharepoint-workflow-create-a-custom-action"></a><span data-ttu-id="a474c-113">SharePoint-Workflow: Erstellen einer benutzerdefinierten Aktion</span><span class="sxs-lookup"><span data-stu-id="a474c-113">SharePoint workflow: Create a custom action</span></span>

<span data-ttu-id="a474c-p103">Dieses Beispiel verwendet Visual Studio um das Erstellen eines Workflows aufzuzeigen, der einen externen Webdienst aufruft. Beim Aufrufen des Webdiensts verwendet der Workflow außerdem den neuen Datentyp **DynamicValue**. Der Teil des Workflows, der den Webdienst aufruft und die Details aus der Antwort extrahiert, die sich in einer benutzerdefinierten Aktivität befindet, **GetNWCustomerDetailsWorkflow**.</span><span class="sxs-lookup"><span data-stu-id="a474c-p103">This sample uses Visual Studio to demonstrate creating a workflow that calls an external web service. In calling the web service, the workflow also uses the new **DynamicValue** data type. The part of the workflow that calls the web service and extracts the details from the response is contained within a custom activity, **GetNWCustomerDetailsWorkflow**.</span></span>
  
    
    
<span data-ttu-id="a474c-117">Das Beispiel und eine Infodatei sind hier verfügbar:  [SharePoint-Workflow: Erstellen einer benutzerdefinierten Aktion](http://code.msdn.microsoft.com/SharePoint-workflow-41e5c0f9)</span><span class="sxs-lookup"><span data-stu-id="a474c-117">The sample, along with a readme file, is available here:  [SharePoint workflow: Create a custom action](http://code.msdn.microsoft.com/SharePoint-workflow-41e5c0f9)</span></span>
  
    
    

### <a name="sharepoint-workflow-sales-tax-calculator"></a><span data-ttu-id="a474c-118">SharePoint-Workflow: Mehrwertsteuer-Rechner</span><span class="sxs-lookup"><span data-stu-id="a474c-118">SharePoint workflow: Sales tax calculator</span></span>

<span data-ttu-id="a474c-119">In diesem durchgängigen Beispiel verwendet der Workflow einen Webdienst zum Abrufen der auf dem Standort des Käufers basierenden Mehrwertsteuer und verwendet anschließend den Basispreis zum Berechnen der Mehrwertsteuer und der Summe.</span><span class="sxs-lookup"><span data-stu-id="a474c-119">In this end-to-end sample, the workflow uses a web service to obtain the appropriate tax rate based on a purchaser's location, and then uses the base price to calculate the sales tax and total price.</span></span>
  
    
    
<span data-ttu-id="a474c-120">Das Beispiel und eine Infodatei sind hier verfügbar:  [SharePoint-Workflow: Mehrwertsteuer-Rechner](http://code.msdn.microsoft.com/SharePoint-workflow-f7a1a8ba)</span><span class="sxs-lookup"><span data-stu-id="a474c-120">The sample, along with a readme file, is available here:  [SharePoint workflow: Sales tax calculator](http://code.msdn.microsoft.com/SharePoint-workflow-f7a1a8ba)</span></span>
  
    
    

### <a name="sharepoint-workflow-use-a-task-action-in-sharepoint-designer"></a><span data-ttu-id="a474c-121">SharePoint-Workflow: Verwenden Sie eine Aufgabenaktion in SharePoint Designer</span><span class="sxs-lookup"><span data-stu-id="a474c-121">SharePoint workflow: Use a task action in SharePoint Designer</span></span>

<span data-ttu-id="a474c-122">Eine erweiterte Vorgehensweise des Prozesses zum Implementieren von Aufgabenaktionen in einen Workflow, die mit Microsoft SharePoint Designer 2013 erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="a474c-122">An extended walkthrough of the process of implementing task actions in a workflow created using Microsoft SharePoint Designer 2013.</span></span>
  
    
    
<span data-ttu-id="a474c-123">Das Beispiel und eine Infodatei sind hier verfügbar:  [SharePoint-Workflow: Verwenden einer Aufgabenaktion in SharePoint Designer](http://code.msdn.microsoft.com/SharePoint-workflow-942a5441)</span><span class="sxs-lookup"><span data-stu-id="a474c-123">The sample, along with a readme file, is available here:  [SharePoint workflow: Using a task action in SharePoint Designer](http://code.msdn.microsoft.com/SharePoint-workflow-942a5441)</span></span>
  
    
    

### <a name="sharepoint-workflow-workflow-om-in-a-sharepoint-app"></a><span data-ttu-id="a474c-124">SharePoint-Workflow: Workflow-OM in einer SharePoint-App</span><span class="sxs-lookup"><span data-stu-id="a474c-124">SharePoint workflow: Workflow OM in a SharePoint app</span></span>

<span data-ttu-id="a474c-125">Das Codebeispiel **SharePoint-Workflow: Workflow-OM in einer SharePoint-App** stellt ein Beispiel einer interaktiven in Sharepoint gehosteten App dar, die das SharePoint-Workflow-JSOM zum Bereitstellen der Workflowdefinitionen für ein App-Web und ein "übergeordnetes Web" (d. h. ein SharePoint-Web, das die App hostet) verwendet.</span><span class="sxs-lookup"><span data-stu-id="a474c-125">The **SharePoint workflow: Workflow OM in a SharePoint app** code sample is an example of an interactive SharePoint-hosted app that uses the SharePoint workflow JSOM to deploy workflow definitions to both an app web and to a "parent web" (that is, a SharePoint web that is hosting the app).</span></span>
  
    
    
<span data-ttu-id="a474c-126">Beispielcode dazu finden Sie hier:  [SharePoint-Workflow: Workflow-OM in einer SharePoint-App](http://code.msdn.microsoft.com/SharePoint-workflow-050f5211).</span><span class="sxs-lookup"><span data-stu-id="a474c-126">You can locate the sample code here:  [SharePoint workflow: Workflow OM in a SharePoint app](http://code.msdn.microsoft.com/SharePoint-workflow-050f5211).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="a474c-127">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="a474c-127">Additional resources</span></span>
<span data-ttu-id="a474c-128"><a name="bkm_additional"> </a></span><span class="sxs-lookup"><span data-stu-id="a474c-128"></span></span>


-  [<span data-ttu-id="a474c-129">Erste Schritte mit Workflows in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a474c-129">Get started with workflows in SharePoint</span></span>](get-started-with-workflows-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a474c-130">Einrichten und Konfigurieren von SharePoint-Workflow-Manager</span><span class="sxs-lookup"><span data-stu-id="a474c-130">Set up and configure SharePoint Workflow Manager</span></span>](set-up-and-configure-sharepoint-workflow-manager.md)
    
  
-  [<span data-ttu-id="a474c-131">Neuerungen in Workflows für SharePoint</span><span class="sxs-lookup"><span data-stu-id="a474c-131">What's new in workflows for SharePoint</span></span>](what-s-new-in-workflows-for-sharepoint.md)
    
  
-  [<span data-ttu-id="a474c-132">Workflowaktions- und -aktivitätenreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="a474c-132">Workflow actions and activities reference for SharePoint</span></span>](workflow-actions-and-activities-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="a474c-133">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="a474c-133">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  

