---
title: "Ausführen vorbereitender Schritte zum Einrichten und Konfigurieren einer Entwicklungsumgebung für SharePoint-Workflows"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: b6a3321f-4131-4a8e-9cb7-7a1b4ab9e26b
ms.openlocfilehash: 2c75e0c98642891abe614c6650dc09aa80c5df6f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="prepare-to-set-up-and-configure-a-sharepoint-workflow-development-environment"></a><span data-ttu-id="9ea5f-102">Ausführen vorbereitender Schritte zum Einrichten und Konfigurieren einer Entwicklungsumgebung für SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="9ea5f-102">Prepare to set up and configure a SharePoint workflow development environment</span></span>
<span data-ttu-id="9ea5f-103">Erfahren Sie mehr darüber, wie Sie eine Workflowentwicklungsumgebung für das Entwickeln von SharePoint-Workflows als eigenständige  [Apps für SharePoint](http://msdn.microsoft.com/library/fp179930.aspx) mit Visual Studio 2012 entwickeln.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-103">Learn how to set up a workflow development environment to develop SharePoint workflows as free-standing  [apps for SharePoint](http://msdn.microsoft.com/library/fp179930.aspx) by using Visual Studio 2012.</span></span>
## <a name="overview-of-workflow-development-in-sharepoint"></a><span data-ttu-id="9ea5f-104">Übersicht über die Entwicklung von Workflows in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9ea5f-104">Overview of workflow development in SharePoint</span></span>

<span data-ttu-id="9ea5f-105">Zwar sind Workflows seit den frühen Versionen ein Teil von SharePoint, aber Workflows für SharePoint sind eine wesentlich erweiterte und verbesserte Plattform.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-105">Although workflows have been a part of SharePoint since early versions, workflows for SharePoint are a much enhanced and improved platform.</span></span> 
  
    
    

- <span data-ttu-id="9ea5f-106">Zunächst werden SharePoint-Workflows jetzt in  [Windows Workflow Foundation 4.5](http://msdn.microsoft.com/library/dd489441%28v=vs.110%29) erstellt, das Teil von .NET Framework 4.5 ist.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-106">First, SharePoint workflows are now built on  [Windows Workflow Foundation 4.5](http://msdn.microsoft.com/library/dd489441%28v=vs.110%29), which is part of the .NET Framework 4.5.</span></span>
    
  
- <span data-ttu-id="9ea5f-p101">Zweitens wurde das Workflow-Ausführungsmodul,  [Workflow-Manager](http://msdn.microsoft.com/library/windowsazure/jj193528%28v=azure.10%29.aspx), von SharePoint entkoppelt und wird unabhängig ausgeführt. Das sorgt für Flexibilität und Skalierbarkeit. (Beachten Sie, dass aus Gründen der Abwärtskompatibilität das 2010-Vorgängerworkflowmodul Teil von SharePoint bleibt.)</span><span class="sxs-lookup"><span data-stu-id="9ea5f-p101">Second, the workflow execution engine,  [Workflow Manager](http://msdn.microsoft.com/library/windowsazure/jj193528%28v=azure.10%29.aspx), has been decoupled from SharePoint and runs independently. This provides both flexibility and scalability. (Note that for backward compatibility, the legacy 2010 workflow engine remains a part of SharePoint.)</span></span>
    
  
- <span data-ttu-id="9ea5f-110">Statt Workflows durch Schreiben von C#-Code zu entwickeln, erstellen Sie jetzt Workflows in Visual Studio mit einem Workflow-Designer, der deklarative Ausdrücke verwendet.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-110">Instead of developing workflows by writing C# code, you now build workflows in Visual Studio using a workflow designer that uses declarative expressions.</span></span>
    
  
- <span data-ttu-id="9ea5f-111">SharePoint-Workflows können in das neue App-Modell integriert werden, was bedeutet, dass Sie jetzt Workflows in SharePoint-Add-Ins implementieren können.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-111">SharePoint workflows integrate with the new app model, which means you can now implement workflows in SharePoint Add-ins.</span></span>
    
  
- <span data-ttu-id="9ea5f-p102">Sie können einen SharePoint-Workflow außerdem mit SharePoint Designer 2013 entwickeln. Weitere Informationen finden Sie unter  [Workflowentwicklung in SharePoint Designer und Visio](workflow-development-in-sharepoint-designer-and-visio.md).</span><span class="sxs-lookup"><span data-stu-id="9ea5f-p102">You can also develop SharePoint workflows using SharePoint Designer 2013. For more information, see  [Workflow development in SharePoint Designer and Visio](workflow-development-in-sharepoint-designer-and-visio.md).</span></span>
    
  

### <a name="get-started"></a><span data-ttu-id="9ea5f-114">Erste Schritte</span><span class="sxs-lookup"><span data-stu-id="9ea5f-114">Get started</span></span>

<span data-ttu-id="9ea5f-115">Machen Sie sich zunächst mit dem neuen App-Modell und den SharePoint-Add-Ins zugrunde liegenden Konzepten vertraut, indem Sie sich Folgendes ansehen:</span><span class="sxs-lookup"><span data-stu-id="9ea5f-115">First off, get acquainted with the new app model and the concepts underlying SharePoint Add-ins by dipping into the following:</span></span> 
  
    
    

|||
|:-----|:-----|
| [<span data-ttu-id="9ea5f-116">SharePoint für Entwickler</span><span class="sxs-lookup"><span data-stu-id="9ea5f-116">SharePoint for developers</span></span>](http://msdn.microsoft.com/de-DE/sharepoint) <br/> |<span data-ttu-id="9ea5f-117">Portal der SharePoint-Entwicklerwebsite, in dem der Schwerpunkt auf Apps für SharePoint liegt.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-117">Portal to the SharePoint developer site, where the emphasis is on apps for SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="9ea5f-118">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="9ea5f-118">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |<span data-ttu-id="9ea5f-119">Erfahren Sie, was Apps für SharePoint sind, warum Sie sie erstellen sollten und welche Konzepte für ihre Erstellung in SharePoint grundlegend sind.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-119">Learn what apps for SharePoint are, why you should build them, and the concepts that are fundamental to building them in SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="9ea5f-120">Neuer Name für Apps für SharePoint</span><span class="sxs-lookup"><span data-stu-id="9ea5f-120">New name for apps for SharePoint</span></span>](http://msdn.microsoft.com/library/05b07b04-6c8b-4b7e-bd86-e32c589dfead%28Office.15%29.aspx) <br/> |<span data-ttu-id="9ea5f-121">Portal einer Entwicklerwebsite mit dem Schwerpunkt auf der Erstellung von Apps für Office und Apps für SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-121">Portal to a developer site devoted to building apps for Office and apps for SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="9ea5f-122">Übersicht über die SharePoint-Entwicklung</span><span class="sxs-lookup"><span data-stu-id="9ea5f-122">SharePoint development overview</span></span>](sharepoint-development-overview.md) <br/> |<span data-ttu-id="9ea5f-p103">SharePoint ist eine Entwicklungsplattform für Apps für SharePoint und Farmlösungen. Machen Sie sich mit den Funktionen und Features von SharePoint vertraut, um mit Ihrer Entwicklung zu beginnen.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-p103">SharePoint is a development platform for apps for SharePoint and farm solutions. Get acquainted with the capabilities and features of SharePoint to start your development.</span></span>  <br/> |
| [<span data-ttu-id="9ea5f-125">Grundlegendes zu SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="9ea5f-125">SharePoint workflow fundamentals</span></span>](sharepoint-workflow-fundamentals.md) <br/> |<span data-ttu-id="9ea5f-126">Bietet eine allgemeine Übersicht über die Workflowinfrastruktur in SharePoint, einschließlich einer Sicht der Plattformarchitektur und der Workflow-Interopbrücke</span><span class="sxs-lookup"><span data-stu-id="9ea5f-126">Provides a high-level overview of the workflow infrastructure in SharePoint, including a view of the platform architecture and the workflow interop bridge.</span></span>  <br/> |
   
<span data-ttu-id="9ea5f-p104">Stellen Sie im nächsten Schritt sicher, dass eine aktuelle Workflowentwicklungsumgebung installiert ist. Sie müssen nicht auf dem SharePoint-Serverrechner entwickeln, benötigen aber natürlich eine SharePoint Server-Installation, mit der Sie entwickeln können.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-p104">Your next step is to ensure that you have an up-to-date workflow development environment installed. You don't need to develop on the SharePoint server machine, but of course you do need a SharePoint Server installation to develop against.</span></span>
  
    
    
<span data-ttu-id="9ea5f-p105">Im Folgenden sind die erforderlichen Komponenten aufgeführt. Es ist wichtig, dass Sie diese Elemente in der hier beschriebenen Reihenfolge installieren:</span><span class="sxs-lookup"><span data-stu-id="9ea5f-p105">Here are the components you need. It is important that you install these items in the order presented here:</span></span>
  
    
    

1. <span data-ttu-id="9ea5f-131">**Installieren Sie die SharePoint-Umgebung.**</span><span class="sxs-lookup"><span data-stu-id="9ea5f-131">**Install the SharePoint environment**</span></span>
    
  -  [<span data-ttu-id="9ea5f-132">SharePoint-Update (KB2767999)</span><span class="sxs-lookup"><span data-stu-id="9ea5f-132">SharePoint Server 2013 update (KB2767999)</span></span>](http://support.microsoft.com/kb/2767999)
    
  
  - <span data-ttu-id="9ea5f-133">Optional können Sie eine [Office 365-Entwicklungsumgebung](http://msdn.microsoft.com/library/office/apps/fp179924%28v=office.15%29) abonnieren.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-133">Optionally, you can subscribe to an  [Office 365 development environment](http://msdn.microsoft.com/library/office/apps/fp179924%28v=office.15%29)</span></span>
    
  
2. <span data-ttu-id="9ea5f-134">**Installieren der Workflow-Manager-Umgebung**</span><span class="sxs-lookup"><span data-stu-id="9ea5f-134">**Install the Workflow Manager environment**</span></span>
    
  -  [<span data-ttu-id="9ea5f-135">Workflow Manager 1.0 kumulativ (KB2799754)</span><span class="sxs-lookup"><span data-stu-id="9ea5f-135">Workflow Manager 1.0 Cumulative (KB2799754)</span></span>](http://support.microsoft.com/kb/2799754/en-us)
    
  
3. <span data-ttu-id="9ea5f-136">**Installieren der Visual Studio 2012-Entwicklungsumgebung**</span><span class="sxs-lookup"><span data-stu-id="9ea5f-136">**Install the Visual Studio 2012 development environment**</span></span>
    
  -  [<span data-ttu-id="9ea5f-137">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="9ea5f-137">Visual Studio 2012</span></span>](http://www.microsoft.com/visualstudio/eng/downloads#vs)
    
  
  -  [<span data-ttu-id="9ea5f-138">Visual Studio 2012 Update 2 (KB2797912)</span><span class="sxs-lookup"><span data-stu-id="9ea5f-138">Visual Studio 2012 Update 2 (KB2797912)</span></span>](http://support.microsoft.com/kb/2797912)
    
  
  -  [<span data-ttu-id="9ea5f-139">.NET Framework 4.5-Update (KB2750149)</span><span class="sxs-lookup"><span data-stu-id="9ea5f-139">.NET Framework 4.5 update (KB2750149)</span></span>](http://support.microsoft.com/kb/2750149/en-us)
    
  
  -  [<span data-ttu-id="9ea5f-140">Office Developer Tools für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="9ea5f-140">Office Developer Tools for Visual Studio 2012</span></span>](http://aka.ms/OfficeDevToolsForVS2012)
    
  

### <a name="if-you-have-the-preview-version"></a><span data-ttu-id="9ea5f-141">Wenn Sie die „Vorschau"-Version haben</span><span class="sxs-lookup"><span data-stu-id="9ea5f-141">If you have the "Preview" version</span></span>

<span data-ttu-id="9ea5f-p106">Wenn Sie Vorabversionen (d. h. eine „Vorschau") von SharePoint Server, Workflow-Manager 1.0 oder Office Developer Tools für Visual Studio 2013 (Versionen vor März 2013) haben, müssen Sie Ihre Installation aktualisieren. Nachfolgend finden Sie eine Liste der geeigneten Updates:</span><span class="sxs-lookup"><span data-stu-id="9ea5f-p106">If you have pre-release (that is, "Preview") versions of SharePoint Server, Workflow Manager 1.0, or Office Developer Tools for Visual Studio 2013 (versions prior to March 2013), you must update your installation. Following is a list of appropriate updates:</span></span>
  
    
    

-  [<span data-ttu-id="9ea5f-144">SharePoint-Update (KB2767999)</span><span class="sxs-lookup"><span data-stu-id="9ea5f-144">SharePoint Server 2013 update (KB2767999)</span></span>](http://support.microsoft.com/kb/2767999)
    
  
-  [<span data-ttu-id="9ea5f-145">Kumulatives Update für Microsoft Azure Service Bus 1.0 (KB2799752)</span><span class="sxs-lookup"><span data-stu-id="9ea5f-145">Microsoft Azure Service Bus 1.0 Cumulative Update (KB2799752)</span></span>](http://support.microsoft.com/kb/2799752/en-us)
    
  
-  [<span data-ttu-id="9ea5f-146">Workflow Manager 1.0 kumulativ (KB2799754)</span><span class="sxs-lookup"><span data-stu-id="9ea5f-146">Workflow Manager 1.0 Cumulative (KB2799754)</span></span>](http://support.microsoft.com/kb/2799754/en-us)
    
  

### <a name="you-must-also-update-workflow-projects-created-with-the-preview-version"></a><span data-ttu-id="9ea5f-147">Sie müssen auch die Workflowprojekte aktualisieren, die mit der „Vorschau"-Version erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-147">You must also update workflow projects created with the "Preview" version</span></span>

<span data-ttu-id="9ea5f-p107">Mit der endgültigen Produktversion der Visual Studio-Workflowkomponenten und ihren zugehörigen Updates werden wichtige Änderungen eingeführt, die die Leistung, Skalierbarkeit und Zuverlässigkeit verbessern. Diese Upgrades erfordern leider, dass Sie Ihre Workflowprojekte aktualisieren, dass Sie über die Vorschautools erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-p107">The release version of the Visual Studio workflow components and their related updates introduce important changes that enhance performance, scalability, and reliability. Unfortunately, these upgrades require you to update workflow projects that you created using the Preview tools.</span></span>
  
    
    
<span data-ttu-id="9ea5f-p108">Um diesen Prozess zu erleichtern, bieten wir ein Konvertierungstool an, das Sie über CodePlex abrufen können. Das Tool ist der  [SharePoint Workflow-Konverter für Visual Studio 2012](http://wfconverter.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="9ea5f-p108">To make this process easier, we provide a conversion tool that you can get through CodePlex. The tool is called the  [SharePoint Workflow Converter for Visual Studio 2012](http://wfconverter.codeplex.com/).</span></span>
  
    
    
<span data-ttu-id="9ea5f-152">Hier ist eine Zusammenfassung der Änderungen, die eine Aktualisierung Ihrer Workflowprojekte erforderlich machen:</span><span class="sxs-lookup"><span data-stu-id="9ea5f-152">Here is a summary of changes that require you to update your workflow projects:</span></span>
  
    
    

- <span data-ttu-id="9ea5f-153">Aktivitätsverweise auf **Item Guid** werden ersetzt durch **Item Id**. Diese Änderung hat bedeutende Konsequenzen:</span><span class="sxs-lookup"><span data-stu-id="9ea5f-153">Activity references to **Item Guid** are replaced by **Item Id**. This change has important consequences:</span></span>
    
  - <span data-ttu-id="9ea5f-154">Die Aktivitäten  [LookupSPListItemGuid](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.LookupSPListItemGuid.aspx) und [GetCurrentItemGuid](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.GetCurrentItemGuid.aspx) werden aus den Tools entfernt und durch die Aktivitäten **LookupSPListItemId** und **GetCurrentItemId** ersetzt.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-154">The  [LookupSPListItemGuid](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.LookupSPListItemGuid.aspx) and [GetCurrentItemGuid](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.GetCurrentItemGuid.aspx) activities are removed from the tooling; their replacement activities are **LookupSPListItemId** and **GetCurrentItemId**.</span></span>
    
  
  - <span data-ttu-id="9ea5f-p109">Für andere Aktivitäten, die **Item Guid** verwenden, wurde **Item Id** hinzugefügt und **Item Guid** ausgeblendet. Ihre vorhandenen Projekte, die **Item Guid** verwenden, funktionieren weiterhin (außer bei sehr großen Listen mit mehr als 5000 Elementen, was einer der Gründe für die Änderung ist).</span><span class="sxs-lookup"><span data-stu-id="9ea5f-p109">For other activities that use **Item Guid**, you will find **Item Id** added and **Item Guid** hidden. Your existing projects that use **Item Guid** will continue to work (except on very large lists with more than 5000 items, which is one of the reasons for the change).</span></span>
    
  
- <span data-ttu-id="9ea5f-157">Es gibt ein neues Verpackungsformat für Workflows in Apps.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-157">There is a new packaging format for workflows in apps.</span></span>
    
  
- <span data-ttu-id="9ea5f-158">Der Workflowaktivitäten-Assemblyverweis in XAML wurde geändert und verweist jetzt auf eine neue Entwurfszeit-Proxyassembly statt auf die tatsächliche SP-Aktivitätenassembly.</span><span class="sxs-lookup"><span data-stu-id="9ea5f-158">The workflow activities assembly reference in XAML has been changed to point to a new design-time proxy assembly instead of the actual SP activities assembly.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="9ea5f-159">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="9ea5f-159">Additional resources</span></span>
<span data-ttu-id="9ea5f-160"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9ea5f-160"></span></span>


-  [<span data-ttu-id="9ea5f-161">Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="9ea5f-161">Set up an on-premises development environment for SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="9ea5f-162">Neuerungen in Workflows für SharePoint</span><span class="sxs-lookup"><span data-stu-id="9ea5f-162">What's new in workflows for SharePoint</span></span>](what-s-new-in-workflows-for-sharepoint.md)
    
  
-  [<span data-ttu-id="9ea5f-163">Workflowentwicklung in SharePoint Designer und Visio</span><span class="sxs-lookup"><span data-stu-id="9ea5f-163">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [<span data-ttu-id="9ea5f-164">Workflows in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9ea5f-164">Workflows in SharePoint</span></span>](workflows-in-sharepoint.md)
    
  

