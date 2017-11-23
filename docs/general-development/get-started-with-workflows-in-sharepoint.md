---
title: Erste Schritte mit Workflows in SharePoint
ms.date: 09/25/2017
keywords: vs.sharepointtools.workflow4.workflowlist,VS.SharePointTools.Workflow4.WorkflowName
f1_keywords: vs.sharepointtools.workflow4.workflowlist,VS.SharePointTools.Workflow4.WorkflowName
ms.prod: sharepoint
ms.assetid: a2643cd7-474d-4e4c-85bb-00f0b6685a1d
ms.openlocfilehash: ae4354d1659ab4b70ea11a35f88c7fb8553e4048
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="get-started-with-workflows-in-sharepoint"></a><span data-ttu-id="e1760-103">Erste Schritte mit Workflows in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e1760-103">Get started with workflows in SharePoint</span></span>
<span data-ttu-id="e1760-104">Informationen zum neu entwickelten Workflow-Manager-Client 1.0, der die Infrastruktur für Workflows in SharePoint bereitstellt, und zur Integration von SharePoint-Workflows mit dem neuen Modell für SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="e1760-104">Learn about the newly engineered Workflow Manager Client 1.0, which provides the infrastructure for workflows in SharePoint, and how SharePoint workflows are integrated with the new model for SharePoint Add-ins.</span></span>
> <span data-ttu-id="e1760-105">**Wichtig:** Anweisungen zum Einrichten und Konfigurieren von SharePoint und Microsoft Azure finden Sie unter  [Einrichten und Konfigurieren von SharePoint-Workflow-Manager](set-up-and-configure-sharepoint-workflow-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e1760-105">**Important** For instructions on setting up and configuring SharePoint Server 2013 and Microsoft Azure, see  [Set up and configure SharePoint Workflow Manager](set-up-and-configure-sharepoint-workflow-manager.md).</span></span> 
  
    
    


## <a name="overview-of-workflows-in-sharepoint"></a><span data-ttu-id="e1760-106">Übersicht über Workflows in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e1760-106">Overview of workflows in SharePoint</span></span>
<span data-ttu-id="e1760-107"><a name="overview"> </a></span><span class="sxs-lookup"><span data-stu-id="e1760-107"></span></span>

<span data-ttu-id="e1760-p101">Workflows in SharePoint ermöglichen Ihnen das Entwickeln und Automatisieren von Geschäftsprozessen. Bei diesen Geschäftsprozessen kann es sich um einen einfachen Genehmigungsprozess für Dokumente mit einer einzelnen genehmigenden Person (siehe Abbildung 1), um einen komplexen Prozess mit einem Produktkatalog für Kunden unter Verwendung von Webdienstaufrufen und mit Datenbankunterstützung oder praktisch um jede Art von anspruchsvollem, strukturiertem Geschäftsprozess mit einer Vielzahl von Bedingungen, Schleifen, Benutzereingaben, Aufgaben und benutzerdefinierten Aktionen handeln.</span><span class="sxs-lookup"><span data-stu-id="e1760-p101">Workflows in SharePoint allow you to model and automate business processes. These business processes can be as simple as a document approval process with a single approver (shown in Figure 1), as complex as customer-facing product catalog using web service calls and database support, or as formidable as virtually any structured business process, full of conditions, loops, user inputs, tasks, and custom actions.</span></span>
  
    
    

<span data-ttu-id="e1760-110">**Abbildung 1. Einfacher SharePoint-Workflow**</span><span class="sxs-lookup"><span data-stu-id="e1760-110">**Figure 1. Simple SharePoint workflow**</span></span>

  
    
    

  
    
    
![Einfacher Workflow](../images/wfSimple.gif)
  
    
    

  
    
    
<span data-ttu-id="e1760-p102">SharePoint zeichnet sich durch die Einführung von Workflow-Manager-Client 1.0 als neues leistungsstarkes Fundament für Visual Studio-Workflows aus. Basierend auf Windows Workflow Foundation 4 bietet Workflow-Manager-Client 1.0 Vorteile gegenüber Vorversionen, die die Weiterentwicklung von SharePoint in Bezug auf das Modell für SharePoint-Add-Ins und das Cloud Computing zum Ausdruck bringen. Einzelheiten zu diesen Änderungen finden Sie unter  [Neuerungen in Workflows für SharePoint](what-s-new-in-workflows-for-sharepoint.md) und [Grundlegendes zu SharePoint-Workflows](sharepoint-workflow-fundamentals.md).</span><span class="sxs-lookup"><span data-stu-id="e1760-p102">SharePoint marks the introduction of Workflow Manager Client 1.0 as the powerful new foundation for Visual Studio workflows. Build on Windows Workflow Foundation 4, Workflow Manager Client 1.0 provides advantages over previous versions that reflect the commitment of SharePoint to the model for SharePoint Add-ins and cloud-based computing. For details of these changes, see  [What's new in workflows for SharePoint](what-s-new-in-workflows-for-sharepoint.md) and [SharePoint workflow fundamentals](sharepoint-workflow-fundamentals.md).</span></span>
  
    
    
<span data-ttu-id="e1760-p103">Für Workflowersteller vielleicht am wichtigsten ist, dass die Einrichtung von Workflows umfassend verbessert und vereinfacht wurde. Workflows sind mittlerweile nicht nur gänzlich deklarativ (d. h. designerbasiert und ohne Codierung), sondern auch die primären Umgebungen zum Erstellen von Workflows, sowohl Visual Studio 2012 als auch SharePoint Designer 2013, wurden vereinfacht und optimiert.</span><span class="sxs-lookup"><span data-stu-id="e1760-p103">Perhaps most importantly for workflow authors, the way that your create workflows has been vastly improved and simplified. Not only are workflows now entirely declarative (that is, designer-based, no-code workflows), but the primary workflow authoring environments, both Visual Studio 2012 and SharePoint Designer 2013, have been simplified and streamlined.</span></span>
  
    
    
<span data-ttu-id="e1760-p104">Nachfolgend werden die wichtigsten Weiterentwicklungen an Workflows in SharePoint vorgestellt. Eine detailliertere Übersicht der Neuerungen in Workflows für SharePoint finden Sie unter  [Neuerungen in Workflows für SharePoint](what-s-new-in-workflows-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e1760-p104">The key enhancements to workflows in SharePoint include the following. For a more detail overview of what's new in workflows for SharePoint, see  [What's new in workflows for SharePoint](what-s-new-in-workflows-for-sharepoint.md).</span></span>
  
    
    

- <span data-ttu-id="e1760-p105">Verbesserte Verbindungsmöglichkeiten zum Ermöglichen einer cloudbasierten Ausführung von Workflows. In der Tat sind in SharePoint lokale und Office 365-basierte Workflows zu 100 % gleichranging.</span><span class="sxs-lookup"><span data-stu-id="e1760-p105">Enhanced connectivity to enable cloud-based execution of workflows. In fact, there is 100 percent parity in SharePoint between on-premises and Office 365 -based workflows.</span></span>
    
  
- <span data-ttu-id="e1760-121">Es gibt eine vollständige Interoperabilität in SharePoint mit SharePoint 2010-Workflows, die durch die  [SharePoint-Workflowinteroperabilität ](sharepoint-workflow-fundamentals.md#bkm_InteropBridge) ermöglicht wird.</span><span class="sxs-lookup"><span data-stu-id="e1760-121">There is full interoperability in SharePoint with SharePoint 2010 workflows, which is enabled by using the  [SharePoint workflow interop ](sharepoint-workflow-fundamentals.md#bkm_InteropBridge).</span></span>
    
  
- <span data-ttu-id="e1760-122">Verbesserte Möglichkeiten zur Einrichtung von Workflows mithilfe von Visual Studio-Ereignissen und Aktionen, Webdiensten und klassischen Programmierungsstrukturen, alles in einer deklarativen codierungslosen Umgebung.</span><span class="sxs-lookup"><span data-stu-id="e1760-122">Enhanced authoring expressiveness by using Visual Studio events and action, web services, and classic programming structures, all in a declarative, no-code environment.</span></span>
    
  
- <span data-ttu-id="e1760-123">Skalierbarkeit und Zuverlässigkeit im Einklang mit Anforderungen an Office 365 und das Cloud-App-Modell.</span><span class="sxs-lookup"><span data-stu-id="e1760-123">Scalability and robustness that is consistent with requirements for Office 365 and the Cloud App Model.</span></span>
    
  
- <span data-ttu-id="e1760-p106">Bessere Verbindungsmöglichkeiten zum Fördern integrierter Systeme mit hoher Funktionalität. Sie können Ihre Workflows auf beliebigen externen Systemen aufrufen und steuern. Darüber hinaus können Ihre Workflows Webdienstaufrufe an beliebige Streams und Datenquellen richten, wozu gängige Protokolle wie HTTP, SOAP, Odata (Open Data) und REST (Representational State Transfer) zum Einsatz kommen.</span><span class="sxs-lookup"><span data-stu-id="e1760-p106">Enhanced connectivity to promote highly functional integrated systems. You can call and control your workflows from any external system. Additionally, your workflow can make web service calls to any stream or data source using common protocols like HTTP, SOAP, the Open Data protocol (OData), and Representational State Transfer (REST).</span></span>
    
  
- <span data-ttu-id="e1760-127">Optimierte Erstellungsfunktionen für Nichtentwickler in SharePoint Designer 2013 und die Möglichkeit, Workflowlogik in Visio zu entwickeln.</span><span class="sxs-lookup"><span data-stu-id="e1760-127">Enhanced authoring capabilities for the non-developer in SharePoint Designer 2013, and the ability to compose workflow logic in Visio.</span></span>
    
  
- <span data-ttu-id="e1760-128">Optimierte, dennoch vereinfachte Workflowentwicklung in Visual Studio, einschließlich Unterstützung für benutzerdefinierte Workflowaktionen, schnelle Entwicklung in einer deklarativen Umgebung, Bereitstellung in einem Schritt und Unterstützung für die Entwicklung von SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="e1760-128">Enhanced, and yet simplified, workflow development in Visual Studio, including support for custom workflow actions, rapid development in a declarative environment, single-step deployment, and support for developing SharePoint Add-ins.</span></span>
    
  
- <span data-ttu-id="e1760-129">Vollständige Unterstützung für workflowgestützte SharePoint-Add-Ins, bei den Workflows als mittlere Ebene für die Verwaltung von Geschäftsprozessen dienen.</span><span class="sxs-lookup"><span data-stu-id="e1760-129">Full support for workflow-powered SharePoint Add-ins, where workflows function as the middle tier for business process management.</span></span>
    
  

## <a name="workflow-manager-client-10-and-the-model-for-sharepoint-add-ins"></a><span data-ttu-id="e1760-130">Workflow-Manager-Client 1.0 und das Modell für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="e1760-130">Workflow Manager Client 1.0 and the model for SharePoint Add-ins</span></span>
<span data-ttu-id="e1760-131"><a name="bm_appModel"> </a></span><span class="sxs-lookup"><span data-stu-id="e1760-131"></span></span>

<span data-ttu-id="e1760-132">Visual Studio 2012 ist für die Entwicklung workflowgesteuerter SharePoint-Add-Ins und die Ausnutzung der enormen Leistungsfähigkeit und Flexibilität des Modell für SharePoint-Add-Ins optimiert. Sie können mithilfe des Objektmodells für SharePoint-Workflows die Workflowlogik hinter einer SharePoint-App so aktivieren, dass Endbenutzern die App-Oberfläche selbst gezeigt wird, während darunter die App von Ihrer Workflowlogik gesteuert wird.</span><span class="sxs-lookup"><span data-stu-id="e1760-132">Visual Studio 2012 is optimized for developing workflow-driven SharePoint Add-ins and for exploiting the enormous power and flexibility of the model for SharePoint Add-ins. You can use the SharePoint workflow object model to enable workflow logic underneath a SharePoint app in such a way that end users experience the app surface itself while underneath the app is driven by your workflow logic.</span></span>
  
    
    
<span data-ttu-id="e1760-133">Darüber hinaus eignet sich Visual Studio 2012 ideal für die Entwicklung von Office-Add-Ins, die Workflows innerhalb einer Microsoft Office-Anwendung ausführen können.</span><span class="sxs-lookup"><span data-stu-id="e1760-133">Additionally, Visual Studio 2012 is ideal for developing Office Add-ins, which can run workflows from inside a Microsoft Office application.</span></span>
  
    
    

## <a name="authoring-sharepoint-workflows"></a><span data-ttu-id="e1760-134">Erstellen von SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="e1760-134">Authoring SharePoint workflows</span></span>
<span data-ttu-id="e1760-135"><a name="bm_authoringwf"> </a></span><span class="sxs-lookup"><span data-stu-id="e1760-135"></span></span>

<span data-ttu-id="e1760-p107">Es gibt zwei primäre Erstellungsumgebungen für Workflow-Manager-Client 1.0: SharePoint Designer 2013 und Visual Studio. Darüber hinaus können kaufmännisch orientierte Mitarbeiter Visio zum Erstellen von Workflowlogik nutzen, die Sie anschließend in SharePoint Designer importieren und in ein SharePoint-Workflowprojekt integrieren können.</span><span class="sxs-lookup"><span data-stu-id="e1760-p107">There are two primary authoring environments for Workflow Manager Client 1.0: SharePoint Designer 2013 and Visual Studio. Additionally, non-technical information workers can use Visio to construct workflow logic that you can then import into SharePoint Designer and assemble into a SharePoint workflow project.</span></span>
  
    
    
<span data-ttu-id="e1760-p108">Die primären Erstellungsumgebungen sind jedoch Visual Studio 2012 und SharePoint Designer 2013. Damit Sie bestimmen können, welche für Ihre Zwecke am besten geeignet ist, konsultieren Sie die Entscheidungsmatrix in  [Vergleich zwischen SharePoint Designer und Visual Studio](develop-sharepoint-workflows-using-visual-studio.md#bkm_Comparing).</span><span class="sxs-lookup"><span data-stu-id="e1760-p108">However, the primary authoring environments are Visual Studio 2012 and SharePoint Designer 2013. To help you decide which of these best suits your needs, see the decision matrix in  [Comparing SharePoint Designer with Visual Studio](develop-sharepoint-workflows-using-visual-studio.md#bkm_Comparing).</span></span>
  
    
    

## <a name="sharepoint-designer-2013-as-workflow-authoring-tool"></a><span data-ttu-id="e1760-140">SharePoint Designer 2013 als Tool zur Erstellung von Workflows</span><span class="sxs-lookup"><span data-stu-id="e1760-140">SharePoint Designer 2013 as workflow authoring tool</span></span>
<span data-ttu-id="e1760-141"><a name="bm_spd"> </a></span><span class="sxs-lookup"><span data-stu-id="e1760-141"></span></span>

<span data-ttu-id="e1760-p109">In vielerlei Hinsicht ist SharePoint Designer 2013 für SharePoint-Workflows das beste Erstellungstool. Wenngleich einige erweiterte Aufgaben (z. B. das Erstellen benutzerdefinierter Aktionen) das Eingreifen eines Entwicklers mit Visual Studio erfordern, bietet SharePoint Designer 2013 einer breiten Palette von Workflowerstellern den flexibelsten Zugriff für die Workflowentwicklung.</span><span class="sxs-lookup"><span data-stu-id="e1760-p109">In many respects, SharePoint Designer 2013 is the authoring tool of choice for SharePoint workflows. Although some advanced tasks (like creating custom actions, for example) require the intervention of a developer using Visual Studio, SharePoint Designer 2013 provides the most flexible access to workflow development to the widest range of workflow authors.</span></span>
  
    
    

## <a name="create-a-workflow-using-visual-studio-2012"></a><span data-ttu-id="e1760-144">Erstellen eines Workflows mit Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="e1760-144">Create a workflow using Visual Studio 2012</span></span>
<span data-ttu-id="e1760-145"><a name="create"> </a></span><span class="sxs-lookup"><span data-stu-id="e1760-145"></span></span>

<span data-ttu-id="e1760-p110">In Visual Studio 2012 sind SharePoint-Workflowprojekttypen integriert. Befolgen Sie zum Erstellen eines SharePoint-Workflowprojekts in Visual Studio die folgenden Schritte.</span><span class="sxs-lookup"><span data-stu-id="e1760-p110">Visual Studio 2012 has SharePoint workflow project types built in. To create a SharePoint workflow project in Visual Studio, follow these steps.</span></span>
  
    
    

### <a name="to-create-a-workflow-using-visual-studio"></a><span data-ttu-id="e1760-148">So erstellen Sie einen Workflow mithilfe von Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e1760-148">To create a workflow using Visual Studio</span></span>


1. <span data-ttu-id="e1760-p111">Öffnen Sie Visual Studio 2012, und erstellen Sie ein neues Projekt. Wählen Sie im Dialogfeld **Neues Projekt** nacheinander **Vorlagen**, **Visual C#**, **Office SharePoint**, **SharePoint-Lösungen** und **SharePoint-Projekt** (siehe Abbildung 2).</span><span class="sxs-lookup"><span data-stu-id="e1760-p111">Open Visual Studio 2012 and create a new project. In the **New Project** dialog box, choose **Templates**, **Visual C#**, **Office SharePoint**, **SharePoint Solutions**, and **SharePoint Project**, as shown in Figure 2.</span></span>
    
   <span data-ttu-id="e1760-151">**Abbildung 2. Dialogfeld "Neues Projekt"**</span><span class="sxs-lookup"><span data-stu-id="e1760-151">**Figure 2. New Project dialog box**</span></span>

  

  ![Dialogfeld "Neues Projekt"](../images/wfNewProject_b2.png)
  

  

  
2. <span data-ttu-id="e1760-153">Wählen Sie nach dem Erstellen des Projekts im Menü **Projekt** den Befehl **Neues Element hinzufügen** und anschließend unter dem Element **Office SharePoint** den Eintrag **Workflow** (siehe Abbildung 3).</span><span class="sxs-lookup"><span data-stu-id="e1760-153">With the project created, choose **Add New Item** on the **Project** menu, and then choose **Workflow** under the **Office SharePoint** item, as shown in Figure 3.</span></span>
    
   <span data-ttu-id="e1760-154">**Abbildung 3. Dialogfeld "Neues Element hinzufügen"**</span><span class="sxs-lookup"><span data-stu-id="e1760-154">**Figure 3. Add New Item dialog box**</span></span>

  

  ![Dialogfeld "Neues Element hinzufügen"](../images/wfAddNewItemDialog_b2.png)
  

  

  
3. <span data-ttu-id="e1760-p112">Nach der Erstellung des Workflowprojekts wird Ihnen eine Designeroberfläche angezeigt, auf der Sie Ihren Workflow erstellen können. Zur Umgebung für die Workflowentwicklung gehört eine benutzerdefinierte Toolbox mit einer großen Palette von Elementen zur Erstellung von Workflows.</span><span class="sxs-lookup"><span data-stu-id="e1760-p112">After the workflow project is created, you are presented with a designer surface on which to create your workflow. The workflow development environment includes a custom toolbox with a large palette of workflow authoring elements.</span></span>
    
   <span data-ttu-id="e1760-158">**Abbildung 4. Visual Studio-Toolbox für die Erstellung von Workflows**</span><span class="sxs-lookup"><span data-stu-id="e1760-158">**Figure 4. Visual Studio workflow authoring toolbox**</span></span>

  

  ![Workflow-Toolbox](../images/wfToolbox_b2.png)
  

  

  

## <a name="additional-resources"></a><span data-ttu-id="e1760-160">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="e1760-160">Additional resources</span></span>
<span data-ttu-id="e1760-161"><a name="information"> </a></span><span class="sxs-lookup"><span data-stu-id="e1760-161"></span></span>

<span data-ttu-id="e1760-162">Weitere Informationen zu **SharePoint-Add-Ins** erhalten Sie unter den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="e1760-162">For more information about **SharePoint Add-ins**, see the following:</span></span>
  
    
    

-  [<span data-ttu-id="e1760-163">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="e1760-163">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="e1760-164">Drei Ansätze, um Entwurfsentscheidungen für SharePoint-Add-Ins zu treffen</span><span class="sxs-lookup"><span data-stu-id="e1760-164">Three ways to think about design options for SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/0942fdce-3227-496a-8873-399fc1dbb72c%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="e1760-165">Wichtige Aspekte der Architektur und Entwicklungslandschaft von Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="e1760-165">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](http://msdn.microsoft.com/library/ae96572b-8f06-4fd3-854f-fc312f7f2d88%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="e1760-166">Arbeiten mit externen Daten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e1760-166">Work with external data in SharePoint</span></span>](http://msdn.microsoft.com/library/1534a5f4-1d83-45b4-9714-3a1995677d85%28Office.15%29.aspx)
    
  
<span data-ttu-id="e1760-167">Weitere Informationen zum Entwickeln von Workflows mit **Visual Studio 2012** und **SharePoint Designer 2013** erhalten Sie unter den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="e1760-167">For more information about developing workflows using **Visual Studio 2012** and **SharePoint Designer 2013**, see the following:</span></span>
  
    
    

-  [<span data-ttu-id="e1760-168">Entwickeln von SharePoint-Workflows mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e1760-168">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio.md)
    
  
-  [<span data-ttu-id="e1760-169">Workflowentwicklung in SharePoint Designer und Visio</span><span class="sxs-lookup"><span data-stu-id="e1760-169">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
<span data-ttu-id="e1760-170">Weitere Informationen zu Windows Workflow Foundation 4 erhalten Sie unter den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="e1760-170">For more information about Windows Workflow Foundation 4, see the following:</span></span> 
  
    
    

-  <span data-ttu-id="e1760-171">
  [Einführung für Entwickler für Windows Workflow Foundation (WF) in .NET 4](http://msdn.microsoft.com/de-de/library/ee342461.aspx)</span><span class="sxs-lookup"><span data-stu-id="e1760-171">[A Developer's Introduction to Windows Workflow Foundation (WF) in .NET 4](http://msdn.microsoft.com/de-de/library/ee342461.aspx)</span></span>
    
  
-  <span data-ttu-id="e1760-172">
  [Neues in Windows Workflow Foundation](http://msdn.microsoft.com/de-de/library/dd489410%28v=vs.110%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="e1760-172">[What's New in Windows Workflow Foundation](http://msdn.microsoft.com/de-de/library/dd489410%28v=vs.110%29.aspx)</span></span>
    
  
-  [<span data-ttu-id="e1760-173">Handbuch für Anfänger mit Windows Workflow Foundation</span><span class="sxs-lookup"><span data-stu-id="e1760-173">Beginner's Guide to Windows Workflow Foundation</span></span>](http://msdn.microsoft.com/en-us/netframework/first-steps-with-wf.aspx)
    
  
-  <span data-ttu-id="e1760-174">
  [Grundlegendes zu Windows Workflow Foundation](http://msdn.microsoft.com/de-de/library/dd851337.aspx)</span><span class="sxs-lookup"><span data-stu-id="e1760-174">[The Workflow Way: Understanding Windows Workflow Foundation](http://msdn.microsoft.com/de-de/library/dd851337.aspx)</span></span>
    
  
-  <span data-ttu-id="e1760-175">
  [Einführung in das Regelmodul für Windows Workflow Foundation](http://msdn.microsoft.com/de-de/library/dd554919.aspx)</span><span class="sxs-lookup"><span data-stu-id="e1760-175">[Introduction to the Windows Workflow Foundation Rules Engine](http://msdn.microsoft.com/de-de/library/dd554919.aspx)</span></span>
    
  
-  <span data-ttu-id="e1760-176">
  [Integration von Windows Workflow Foundation mit Windows Communication Foundation](http://msdn.microsoft.com/de-de/library/cc626077.aspx)</span><span class="sxs-lookup"><span data-stu-id="e1760-176">[Windows Workflow Foundation integration with Windows Communication Foundation](http://msdn.microsoft.com/de-de/library/cc626077.aspx)</span></span>
    
  

