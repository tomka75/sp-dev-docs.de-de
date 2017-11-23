---
title: Entwickeln von SharePoint-Workflows mit Visual Studio
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 28f5d3b1-6fe8-4b1f-8c4e-b11105fe6f46
ms.openlocfilehash: de2db87007f801da6555d5f749028f4a30eda172
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="develop-sharepoint-workflows-using-visual-studio"></a><span data-ttu-id="121bc-102">Entwickeln von SharePoint-Workflows mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="121bc-102">Develop SharePoint workflows using Visual Studio</span></span>
<span data-ttu-id="121bc-p101">SharePoint unterstützt zwei primäre Workflowentwicklungsumgebungen zur Erstellung von Workflows: SharePoint Designer und Visual Studio. Dieser Artikel bietet einen Überblick über beide und erläutert die jeweiligen Vor- und Nachteile.</span><span class="sxs-lookup"><span data-stu-id="121bc-p101">SharePoint supports two primary workflow development environments for authoring workflows: SharePoint Designer and Visual Studio. This article summarizes both and discusses the advantages and disadvantages of each.</span></span>
## <a name="authoring-basics-for-sharepoint-workflows"></a><span data-ttu-id="121bc-105">Grundlegendes zur Erstellung von SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="121bc-105">Authoring basics for SharePoint workflows</span></span>
<span data-ttu-id="121bc-106"><a name="bkm_AuthoringBasics"> </a></span><span class="sxs-lookup"><span data-stu-id="121bc-106"></span></span>


> <span data-ttu-id="121bc-107">**Hinweis:** Hinweise zur Einrichtung und Konfiguration von Microsoft SharePoint und dem Workflow-Manager-Client 1.0-Server finden Sie unter [Einrichten und Konfigurieren von SharePoint-Workflow-Manager](set-up-and-configure-sharepoint-workflow-manager.md).</span><span class="sxs-lookup"><span data-stu-id="121bc-107">**Note** For guidance on setting up and configuring Microsoft SharePoint Server 2013 and the Workflow Manager Client 1.0 server, see  [Set up and configure SharePoint Workflow Manager](set-up-and-configure-sharepoint-workflow-manager.md).</span></span> 
  
    
    

<span data-ttu-id="121bc-p102">Wie bei früheren Versionen stellt Microsoft SharePoint zwei primäre Workflowentwicklungsumgebungen zur Erstellung von Workflows bereit: Microsoft SharePoint Designer und Microsoft Visual Studio. Der Unterschied zu früheren Version besteht allerdings darin, dass bei Verwendung von Visual Studio keine codebasierte Erstellungsstrategie mehr bereitgestellt wird. Stattdessen bieten sowohl SharePoint Designer als auch Visual Studio unabhängig von dem von Ihnen ausgewählten Entwicklungstool eine vollständig deklarative, codefreie Erstellungsumgebung.</span><span class="sxs-lookup"><span data-stu-id="121bc-p102">As with previous versions, Microsoft SharePoint provides two primary workflow development environments for authoring workflows: Microsoft SharePoint Designer and Microsoft Visual Studio. However, what differs from previous versions is that using Visual Studio no longer provides a code-based authoring strategy. Instead, both SharePoint Designer and Visual Studio provide a fully declarative, no-code authoring environment regardless of the development tool you select.</span></span>
  
    
    

> <span data-ttu-id="121bc-111">**Hinweis:** Als Ergänzung zur Erstellung von Workflows in SharePoint Designer können Sie auch Microsoft Visio 2013 verwenden, um Ihre Workflowlogik mithilfe von Visio 2013-Shapes zu strukturieren, und Ihre Logik dann in SharePoint Designer 2013 importieren.</span><span class="sxs-lookup"><span data-stu-id="121bc-111">**Note** As a complement to authoring workflows in SharePoint Designer, you can also use Microsoft Visio 2013 to structure your workflow logic by using Visio 2013 shapes, and then import your logic into SharePoint Designer 2013. For information about using Visio 2013 to author your workflow logic, see  Workflow development in SharePoint Designer and Visio.</span></span> <span data-ttu-id="121bc-112">Informationen zur Verwendung von Visio 2013 zum Erstellen Ihrer Workflowlogik finden Sie unter [Workflowentwicklung in SharePoint Designer und Visio](workflow-development-in-sharepoint-designer-and-visio.md).</span><span class="sxs-lookup"><span data-stu-id="121bc-112">For information about using Visio 2013 to author your workflow logic, see  [Workflow development in SharePoint Designer and Visio](workflow-development-in-sharepoint-designer-and-visio.md).</span></span> 
  
    
    


### <a name="declarative-workflows"></a><span data-ttu-id="121bc-113">Deklarative Workflows</span><span class="sxs-lookup"><span data-stu-id="121bc-113">Declarative workflows</span></span>

<span data-ttu-id="121bc-p104">Zunächst sollten Sie wissen, was unter "deklarativen" Workflows zu verstehen ist. Dieser Begriff bedeutet, dass der Workflow nicht in Form von Code erstellt und dann zu verwalteten Assemblys kompiliert wird, sondern in XAML (wortwörtlich) beschrieben und dann zur Laufzeit interpretativ ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="121bc-p104">Let's first be clear what is meant by "declarative" workflows. This term means that instead of being authored in code and then compiled into managed assemblies, the workflow is described (literally) in XAML and then executed interpretively at run time.</span></span>
  
    
    
<span data-ttu-id="121bc-p105">Das XAML wird von den Workflowbausteinen abgeleitet, die Sie in Workflow-Designer (falls Sie Visual Studio verwenden) oder der Workflowdesignoberfläche von SharePoint Designer (oder Visio, mehr dazu später) bearbeiten. Die Bausteine selbst sind die visuellen Workflowdesignobjekte in der Entwurfstoolbox: Stufen, Bedingungen, Aktionen, Ereignisse usw. Der Satz von Tools in den entsprechenden Toolboxes (Visual Studio oder SharePoint Designer) unterscheidet sich geringfügig, das Konzept des deklarativen Workflows bleibt jedoch das gleiche.</span><span class="sxs-lookup"><span data-stu-id="121bc-p105">The XAML is derived (or inferred) from the workflow building blocks that you manipulate in the Workflow Designer (if using Visual Studio) or SharePoint Designer workflow design surface (or Visio, but more about that later). The building blocks themselves are the visual workflow design objects in the designer toolbox—stages, conditions, actions, events, and so on. The set of tools in the respective toolboxes (Visual Studio or SharePoint Designer) differs somewhat, but the concept of the declarative workflow remains the same.</span></span>
  
    
    

## <a name="decision-tree-sharepoint-designer-vs-visual-studio"></a><span data-ttu-id="121bc-119">Entscheidungsbaum: SharePoint Designer im Vergleich zu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="121bc-119">Decision tree: SharePoint Designer vs. Visual Studio</span></span>
<span data-ttu-id="121bc-120"><a name="bkm_DecisionTree"> </a></span><span class="sxs-lookup"><span data-stu-id="121bc-120"></span></span>

<span data-ttu-id="121bc-p106">Zu den größten Vorteilen des Workflowframeworks in SharePoint zählt die Benutzerfreundlichkeit, die es Information Workern erlaubt, mithilfe der codefreien Umgebung von SharePoint Designer umfangreiche und leistungsfähige Workflows zu erstellen. Darüber hinaus bietet eine deklarative Erstellungsumgebung wie Visual Studio ein hohes Maß an Flexibilität und Anpassung.</span><span class="sxs-lookup"><span data-stu-id="121bc-p106">Among the greatest advantages of the workflow framework in SharePoint is the ease with which information workers can use the no-code environment of SharePoint Designer to create rich and powerful workflows. Additionally, a high degree of flexibility and customization is available in a declarative authoring environment such as Visual Studio.</span></span>
  
    
    
<span data-ttu-id="121bc-p107">Beide dieser Workflowerstellungsumgebungen, SharePoint Designer und Visual Studio, sind mit spezifischen Vor- und Nachteilen verbunden. In diesem Abschnitt erfahren Sie, wie Sie herausfinden, welche Erstellungsumgebung für Ihre Anforderungen im Hinblick auf die Workflowentwicklung am besten geeignet ist.</span><span class="sxs-lookup"><span data-stu-id="121bc-p107">Both of these workflow authoring environments—SharePoint Designer and Visual Studio—offer specific advantages and disadvantages. In this section, we explore how to determine which authoring environment best suits your workflow development needs.</span></span>
  
    
    

### <a name="using-sharepoint-designer"></a><span data-ttu-id="121bc-125">Verwenden von SharePoint Designer</span><span class="sxs-lookup"><span data-stu-id="121bc-125">Using SharePoint Designer</span></span>


- <span data-ttu-id="121bc-126">**Zielgruppe:** Information Worker, Geschäftsanalysten, SharePoint-Entwickler</span><span class="sxs-lookup"><span data-stu-id="121bc-126">**Target users:** Information workers, business analysts, SharePoint developers.</span></span>
    
  
- <span data-ttu-id="121bc-127">**Schwierigkeitsstufe:** Gute Kenntnisse im Umgang mit SharePoint Designer, einschließlich der zentralen Workflowkomponenten wie Stufen, Gates, Aktionen, Bedingungen und Schleifen</span><span class="sxs-lookup"><span data-stu-id="121bc-127">**Difficulty level:** Familiarity with SharePoint Designer, including the core workflow components, such as stages, gates, actions, conditions, and loops.</span></span>
    
  
<span data-ttu-id="121bc-p108">Mit SharePoint Designer können Benutzer mithilfe eines codefreien, textbasierten Entwurfstools einen Workflow erstellen, der mit einer Liste, Bibliothek oder Website verknüpft ist. Sie können auch die neue visuelle Entwurfsumgebung verwenden, in der grafische Elemente so auf einer Entwurfsoberfläche angeordnet sind, dass sie den logischen Ablauf eines Geschäftsprozesses darstellen. SharePoint Designer bietet unvergleichliche Funktionen, um technisch wenig versierten Benutzern die schnelle Entwicklung von Workflows zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="121bc-p108">With SharePoint Designer, users can create a workflow that is attached to a list, library, or site using a no-code, text-based designer. Or, they can use the new visual design environment in which graphical elements are arranged on a design surface to represent the logical flow of a business process. SharePoint Designer excels at enabling rapid workflow development by non-technical workers.</span></span>
  
    
    

### <a name="using-visual-studio"></a><span data-ttu-id="121bc-131">Verwenden von Visual Studio</span><span class="sxs-lookup"><span data-stu-id="121bc-131">Using Visual Studio</span></span>


- <span data-ttu-id="121bc-132">**Zielgruppe:** Softwareentwickler mit mittleren oder erweiterten Kenntnissen.</span><span class="sxs-lookup"><span data-stu-id="121bc-132">**Target users:** Intermediate or advanced software developers.</span></span>
    
  
- <span data-ttu-id="121bc-133">**Schwierigkeitsstufe:** Gute Kenntnisse im Umgang mit Visual Studio, einschließlich Konzepten der Softwareentwicklung wie Ereignisempfänger, Verpackung und Bereitstellung und Sicherheit</span><span class="sxs-lookup"><span data-stu-id="121bc-133">**Difficulty level:** Familiarity with Visual Studio, including software development concepts such as event receivers, packaging and deployment, and security.</span></span>
    
  
<span data-ttu-id="121bc-p109">Die Workflowerstellung in Visual Studio bietet die Flexibilität, Workflows zur Unterstützung quasi jedes Geschäftsprozesses zu erstellen, unabhängig von dessen Komplexität, und erlaubt das Debuggen und Wiederverwenden von Workflowdefinitionen. Der vielleicht wichtigste Punkt ist, dass Visual Studio Entwicklern erlaubt, SharePoint-Workflows als Teil einer umfassenderen SharePoint-Lösung oder SharePoint-Add-In einzubinden.</span><span class="sxs-lookup"><span data-stu-id="121bc-p109">Authoring workflows in Visual Studio provides flexibility to create workflows to support virtually any business process, regardless of its complexity, and allows debugging and reuse of workflow definitions. Perhaps most important, Visual Studio lets developers include SharePoint workflows as part of a broader SharePoint solution or SharePoint Add-in.</span></span>
  
    
    
<span data-ttu-id="121bc-p110">Visual Studio erlaubt Entwicklern die Erstellung benutzerdefinierter Aktionen, die von SharePoint Designer verwendet werden, und stellt die Mittel zur Ausführung benutzerdefinierter Logik bereit. Mit Visual Studio können Entwickler auch Workflowvorlagen erstellen, die auf mehreren Websites bereitgestellt werden können.</span><span class="sxs-lookup"><span data-stu-id="121bc-p110">Visual Studio enables developers to create custom actions for consumption by SharePoint Designer, and provides the means to execute custom logic. With Visual Studio, developers can also create workflow templates, which can be deployed to multiple sites.</span></span>
  
    
    

## <a name="comparing-sharepoint-designer-with-visual-studio"></a><span data-ttu-id="121bc-138">Vergleich zwischen SharePoint Designer und Visual Studio</span><span class="sxs-lookup"><span data-stu-id="121bc-138">Comparing SharePoint Designer with Visual Studio</span></span>
<span data-ttu-id="121bc-139"><a name="bkm_Comparing"> </a></span><span class="sxs-lookup"><span data-stu-id="121bc-139"></span></span>

<span data-ttu-id="121bc-140">In der folgenden Tabelle werden die Features und Anforderungen für die Verwendung von SharePoint Designer und Visual Studio zur Erstellung von SharePoint-Workflows gegenübergestellt.</span><span class="sxs-lookup"><span data-stu-id="121bc-140">The following table provides a side-by-side comparison of the features and requirements for using SharePoint Designer and Visual Studio to create SharePoint workflows.</span></span>
  
    
    

<span data-ttu-id="121bc-141">**Tabelle 1. Vergleich von Tools zur Workflowerstellung**</span><span class="sxs-lookup"><span data-stu-id="121bc-141">**Table 1. Workflow authoring tool comparison**</span></span>


|<span data-ttu-id="121bc-142">**Feature/Anforderung**</span><span class="sxs-lookup"><span data-stu-id="121bc-142">**Feature / Requirement**</span></span>|<span data-ttu-id="121bc-143">**SharePoint Designer**</span><span class="sxs-lookup"><span data-stu-id="121bc-143">**SharePoint Designer**</span></span>|<span data-ttu-id="121bc-144">**Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="121bc-144">**Visual Studio**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="121bc-145">Erlaubt schnelle Workflowentwicklung</span><span class="sxs-lookup"><span data-stu-id="121bc-145">Allows rapid workflow development</span></span>  <br/> |<span data-ttu-id="121bc-146">Ja</span><span class="sxs-lookup"><span data-stu-id="121bc-146">Yes</span></span>  <br/> |<span data-ttu-id="121bc-147">Ja</span><span class="sxs-lookup"><span data-stu-id="121bc-147">Yes</span></span>  <br/> |
|<span data-ttu-id="121bc-148">Erlaubt Wiederverwendung von Workflows</span><span class="sxs-lookup"><span data-stu-id="121bc-148">Enables reuse of workflows</span></span>  <br/> |<span data-ttu-id="121bc-p111">Ein Workflow kann nur von der Liste oder Bibliothek verwendet werden, in der er entwickelt wurde. SharePoint Designer bietet allerdings wiederverwendbare Workflows, die auf der gleichen Website mehrmals verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="121bc-p111">A workflow can be used only by the list or library on which it was developed. However, SharePoint Designer provides reusable workflows that can be used multiple times within the same site.</span></span>  <br/> |<span data-ttu-id="121bc-151">Ein Workflow kann als Vorlage geschrieben werden, sodass er nach der Bereitstellung wiederverwendet und einer Liste oder Bibliothek zugeordnet werden kann.</span><span class="sxs-lookup"><span data-stu-id="121bc-151">A workflow can be written as a template so that after it is deployed, it can be reused and associated with any list or library.</span></span>  <br/> |
|<span data-ttu-id="121bc-152">Erlaubt Ihnen, einen Workflow als Teil einer SharePoint-Lösung oder SharePoint-Add-In einzubinden</span><span class="sxs-lookup"><span data-stu-id="121bc-152">Allows you to include a workflow as part of a SharePoint solution or SharePoint Add-in</span></span>  <br/> |<span data-ttu-id="121bc-153">Nein</span><span class="sxs-lookup"><span data-stu-id="121bc-153">No</span></span>  <br/> |<span data-ttu-id="121bc-154">Ja</span><span class="sxs-lookup"><span data-stu-id="121bc-154">Yes</span></span>  <br/> |
|<span data-ttu-id="121bc-155">Erlaubt Ihnen, benutzerdefinierte Aktionen zu erstellen</span><span class="sxs-lookup"><span data-stu-id="121bc-155">Allows you to create custom actions</span></span>  <br/> |<span data-ttu-id="121bc-p112">Nein. Allerdings kann SharePoint Designer benutzerdefinierte Aktionen verwenden und implementieren, die mithilfe von Visual Studio erstellt und bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="121bc-p112">No. However, SharePoint Designer can consume and implement custom actions that are created and deployed by using Visual Studio.</span></span>  <br/> |<span data-ttu-id="121bc-p113">Ja. Beachten Sie allerdings, dass in Visual Studio die zugrunde liegenden Aktivitäten, nicht die entsprechenden Aktionen, verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="121bc-p113">Yes. However, be aware that in Visual Studio, the underlying activities, not their corresponding actions, are used.</span></span>  <br/> |
|<span data-ttu-id="121bc-160">Erlaubt Ihnen, benutzerdefinierten Code zu schreiben</span><span class="sxs-lookup"><span data-stu-id="121bc-160">Allows you to write custom code</span></span>  <br/> |<span data-ttu-id="121bc-161">Nein</span><span class="sxs-lookup"><span data-stu-id="121bc-161">No</span></span>  <br/> |<span data-ttu-id="121bc-162">Nein</span><span class="sxs-lookup"><span data-stu-id="121bc-162">No</span></span>  <br/> <span data-ttu-id="121bc-163">**Hinweis:** Dies ist anders als bei früheren Versionen.</span><span class="sxs-lookup"><span data-stu-id="121bc-163">**Note:** This is changed from previous versions.</span></span> <span data-ttu-id="121bc-164">In SharePoint sind Workflows nur deklarativ, und Visual Studio benötigt für die Workflowentwicklung die visuelle Designüberfläche.</span><span class="sxs-lookup"><span data-stu-id="121bc-164">This is changed from previous versions. In SharePoint, workflows are declarative only and Visual Studio relies on the visual design surface for workflow development.</span></span>           |
|<span data-ttu-id="121bc-165">Visio Professional kann zum Erstellen der Workflowlogik verwendet werden</span><span class="sxs-lookup"><span data-stu-id="121bc-165">Can use Visio Professional to create workflow logic</span></span>  <br/> |<span data-ttu-id="121bc-166">Ja</span><span class="sxs-lookup"><span data-stu-id="121bc-166">Yes</span></span>  <br/> |<span data-ttu-id="121bc-167">Nein</span><span class="sxs-lookup"><span data-stu-id="121bc-167">No</span></span>  <br/> |
|<span data-ttu-id="121bc-168">Bereitstellung)</span><span class="sxs-lookup"><span data-stu-id="121bc-168">Deployment</span></span>  <br/> |<span data-ttu-id="121bc-169">Werden automatisch in der Liste, Bibliothek oder Website bereitgestellt, in der sie erstellt wurden</span><span class="sxs-lookup"><span data-stu-id="121bc-169">Deployed automatically to list, library, or site on which they were created.</span></span>  <br/> |<span data-ttu-id="121bc-170">Erstellen einer SharePoint-Lösungspaketdatei (.wsp) und Bereitstellen des Lösungspakets auf der Website (SPWeb)</span><span class="sxs-lookup"><span data-stu-id="121bc-170">Create a SharePoint solution package (.wsp) file and deploy the solution package to the site (SPWeb).</span></span>  <br/> |
|<span data-ttu-id="121bc-171">Veröffentlichen per Mausklick für Workflows verfügbar</span><span class="sxs-lookup"><span data-stu-id="121bc-171">One-click publishing available for workflows</span></span>  <br/> |<span data-ttu-id="121bc-172">Ja</span><span class="sxs-lookup"><span data-stu-id="121bc-172">Yes</span></span>  <br/> |<span data-ttu-id="121bc-173">Ja</span><span class="sxs-lookup"><span data-stu-id="121bc-173">Yes</span></span>  <br/> |
|<span data-ttu-id="121bc-174">Workflows können verpackt und auf einem Remoteserver bereitgestellt werden</span><span class="sxs-lookup"><span data-stu-id="121bc-174">Workflows can be packaged and deployed to a remote server</span></span>  <br/> |<span data-ttu-id="121bc-175">Ja</span><span class="sxs-lookup"><span data-stu-id="121bc-175">Yes</span></span>  <br/> |<span data-ttu-id="121bc-176">Ja</span><span class="sxs-lookup"><span data-stu-id="121bc-176">Yes</span></span>  <br/> |
|<span data-ttu-id="121bc-177">Debugging</span><span class="sxs-lookup"><span data-stu-id="121bc-177">Debugging</span></span>  <br/> |<span data-ttu-id="121bc-178">Kein Debuggen möglich.</span><span class="sxs-lookup"><span data-stu-id="121bc-178">Cannot be debugged.</span></span>  <br/> |<span data-ttu-id="121bc-179">Workflow kann mithilfe von Visual Studio debuggt werden.</span><span class="sxs-lookup"><span data-stu-id="121bc-179">Workflow can be debugged by using Visual Studio.</span></span>  <br/> |
|<span data-ttu-id="121bc-180">Kann nur Aktionen verwenden, die vom Websiteadministrator genehmigt wurden</span><span class="sxs-lookup"><span data-stu-id="121bc-180">Can use only actions that are approved by site administrator</span></span>  <br/> |<span data-ttu-id="121bc-181">Ja</span><span class="sxs-lookup"><span data-stu-id="121bc-181">Yes</span></span>  <br/> |<span data-ttu-id="121bc-182">Ja</span><span class="sxs-lookup"><span data-stu-id="121bc-182">Yes</span></span>  <br/> <span data-ttu-id="121bc-183">**Hinweis:** Dies ist anders als bei früheren Versionen.</span><span class="sxs-lookup"><span data-stu-id="121bc-183">**Note:** This is changed from previous versions.</span></span> <span data-ttu-id="121bc-184">Zuvor waren Workflows und Aktionen, die mit Visual Studio erstellt wurden, codebasiert und wurden im Farmbereich bereitgestellt, sodass keine Administratorgenehmigung erforderlich war.</span><span class="sxs-lookup"><span data-stu-id="121bc-184">This is changed from previous versions. Previously, workflows and actions that were authored by using Visual Studio were code-based and deployed at the farm scope, so administrator approval was not required.</span></span>           |
   

## <a name="developing-workflows-using-visual-studio"></a><span data-ttu-id="121bc-185">Entwickeln von Workflows mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="121bc-185">Developing workflows using Visual Studio</span></span>
<span data-ttu-id="121bc-186"><a name="bkm_Developing"> </a></span><span class="sxs-lookup"><span data-stu-id="121bc-186"></span></span>

<span data-ttu-id="121bc-p116">Anders als in früheren Versionen sind Workflows in SharePoint vollständig deklarativ. Visual Studio, das nun auf Windows Workflow Foundation 4 basiert, bietet eine visuelle Workflow-Designeroberfläche, mit der Sie benutzerdefinierte Workflows, Workflowvorlagen, Formulare und benutzerdefinierte Workflowaktivitäten vollständig in der Designerumgebung erstellen können. Ihr Workflow wird dann verpackt und als ein SharePoint-Feature bereitgestellt. Informationen zum Verpacken von Features finden Sie unter  [Workflowentwicklung in Visual Studio](http://msdn.microsoft.com/de-de/library/ms461324.aspx).</span><span class="sxs-lookup"><span data-stu-id="121bc-p116">Unlike earlier versions, workflows in SharePoint are entirely declarative. Built now on Windows Workflow Foundation 4, Visual Studio provides a visual workflow designer surface that lets you create custom workflows, workflow templates, forms, and custom workflow activities entirely in the designer environment. Your workflow is then packaged and deployed as a SharePoint Feature. For information about Feature packaging, see  [Using Features in SharePoint Foundation](http://msdn.microsoft.com/de-de/library/ms461324.aspx).</span></span>
  
    
    
<span data-ttu-id="121bc-p117">Die vielleicht wichtigste Änderung für Visual Studio-Entwickler ist, dass benutzerdefinierte Workflows nicht mehr als .NET Framework-Assemblys zusammengestellt und bereitgestellt werden. Darüber hinaus verwendet SharePoint keine Microsoft InfoPath-Formulare mehr; stattdessen werden zur Formularerstellung Microsoft ASP.NET-Formulare benötigt.</span><span class="sxs-lookup"><span data-stu-id="121bc-p117">Perhaps the most significant change for Visual Studio developers is that custom workflows are no longer compiled and deployed as .NET Framework assemblies. Furthermore, SharePoint no longer uses Microsoft InfoPath forms; instead, forms generation relies on Microsoft ASP.NET forms.</span></span> 
  
    
    
<span data-ttu-id="121bc-p118">Außerdem wurden die Visual Studio-Workflowprojektvorlagen geändert. Während früher Vorlagen für Zustandsautomat- und sequenzielle Workflows bereitgestellt wurden, ist diese Unterscheidung nun nicht mehr relevant. Stattdessen stehen im Visual Studio-Build auf Ihrem virtuelle Computer Visual Studio-Projektvorlagen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="121bc-p118">Finally, the Visual Studio workflow project templates have changed. Whereas formerly templates for state machine and sequential workflows were provided, these distinctions are no longer meaningful. Rather, Visual Studio project templates are available in the Visual Studio build provided on your virtual machine (VM).</span></span>
  
    
    

## <a name="enabling-on-premises-workflow-debugging"></a><span data-ttu-id="121bc-196">Aktivieren von lokalem Workflow-Debuggen</span><span class="sxs-lookup"><span data-stu-id="121bc-196">Enabling on-premises workflow debugging</span></span>
<span data-ttu-id="121bc-197"><a name="bkm_Enabling"> </a></span><span class="sxs-lookup"><span data-stu-id="121bc-197"></span></span>

<span data-ttu-id="121bc-198">Um lokale Workflows in Visual Studio zu debuggen, müssen Sie den Workflow-Manager-Tools vorübergehend Zugriff auf Ihr System über die Firewall erlauben.</span><span class="sxs-lookup"><span data-stu-id="121bc-198">To debug on-premises workflows in Visual Studio, you need to temporarily allow the Workflow Manager Tools to access your system through the firewall.</span></span>
  
    
    

1. <span data-ttu-id="121bc-199">Wählen Sie in der **Systemsteuerung** **System und Sicherheit**, **Windows-Firewall** aus.</span><span class="sxs-lookup"><span data-stu-id="121bc-199">In **Control Panel**, choose **System and Security**, **Windows Firewall**.</span></span>
    
  
2. <span data-ttu-id="121bc-200">Wählen Sie in der Liste **Startseite der Systemsteuerung** den Link **Erweiterte Einstellungen** aus.</span><span class="sxs-lookup"><span data-stu-id="121bc-200">In the **Control Panel Home** list, choose the **Advanced Settings** link.</span></span>
    
  
3. <span data-ttu-id="121bc-201">Wählen Sie im linken Fenster von "Windows-Firewall" **Eingehende Regeln** aus.</span><span class="sxs-lookup"><span data-stu-id="121bc-201">In the left pane of Windows Firewall, choose **Inbound Rules**.</span></span>
    
  
4. <span data-ttu-id="121bc-202">Wählen Sie in der Liste **Eingehende Regeln** **Workflow Manager Tools 1.0 for Visual Studio 2012 - Test Service Host** aus.</span><span class="sxs-lookup"><span data-stu-id="121bc-202">In the **Inbound Rules** list, choose **Workflow Manager Tools 1.0 for Visual Studio 2012 - Test Service Host**.</span></span>
    
  
5. <span data-ttu-id="121bc-203">Wählen Sie in der Liste **Aktionen** **Regel aktivieren** aus.</span><span class="sxs-lookup"><span data-stu-id="121bc-203">In the **Actions** list, choose **Enable Rule**.</span></span>
    
  
6. <span data-ttu-id="121bc-204">Wählen Sie auf der Eigenschaftenseite Ihres SharePoint-Projekts die Registerkarte **SharePoint** aus, und aktivieren Sie dann das Kontrollkästchen **Workflow-Debugging aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="121bc-204">On the properties page of your SharePoint project, choose the **SharePoint** tab, and then select the **Enable Workflow debugging** check box.</span></span>
    
  

## <a name="debugging-sharepoint-online-workflows-using-visual-studio"></a><span data-ttu-id="121bc-205">Debuggen von SharePoint Online-Workflows mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="121bc-205">Debugging SharePoint Online workflows using Visual Studio</span></span>
<span data-ttu-id="121bc-206"><a name="bkm_Debug"> </a></span><span class="sxs-lookup"><span data-stu-id="121bc-206"></span></span>

<span data-ttu-id="121bc-207">Führen Sie die folgenden Schritte durch, um SharePoint Online-Workflows in Visual Studio zu debuggen:</span><span class="sxs-lookup"><span data-stu-id="121bc-207">To debug SharePoint Online workflows in Visual Studio, perform the following steps:</span></span>
  
    
    

1. <span data-ttu-id="121bc-208">Wenn sich Ihr Computer hinter einer Firewall befindet, müssen Sie je nach Netzwerktopologie Ihres Unternehmens möglicherweise einen Proxyclient (wie den  [Forefront Threat Management Gateway (TMG)-Client](http://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=10504)) installieren.</span><span class="sxs-lookup"><span data-stu-id="121bc-208">If you're behind a firewall, you may need to install a proxy client (such as the  [Forefront Threat Management Gateway (TMG) Client](http://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=10504)), depending on your company's network topology.</span></span>
    
  
2. <span data-ttu-id="121bc-209">Registrieren Sie sich für ein Microsoft Azure-Konto, wenn Sie dies nicht bereits getan haben, und melden Sie sich dann bei diesem Konto an.</span><span class="sxs-lookup"><span data-stu-id="121bc-209">Register for a Microsoft Azure account if you haven't already, and then sign into that account.</span></span>
    
    <span data-ttu-id="121bc-210">Informationen dazu, wie Sie sich für ein Microsoft Azure-Konto registrieren, finden Sie unter  [Microsoft Azure](http://www.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="121bc-210">For information about how to register for a Microsoft Azure account, see  [Microsoft Azure](http://www.windowsazure.com).</span></span>
    
  
3. <span data-ttu-id="121bc-p119">Erstellen Sie einen Microsoft Azure-Servicebus-Namespace, den Sie zum Debuggen von Remoteworkflows verwenden können. Sie können dies im  [Microsoft Azure-Verwaltungsportal](http://manage.windowsazure.com) tun.</span><span class="sxs-lookup"><span data-stu-id="121bc-p119">Create a Microsoft Azure Service Bus namespace, which you can use to debug remote workflows. You can do this on the  [Microsoft Azure management portal](http://manage.windowsazure.com).</span></span>
    
    <span data-ttu-id="121bc-213">Weitere Informationen zum Microsoft Azure Service Bus finden Sie unter  [Verwalten von Service Bus-Dienstnamespaces](http://msdn.microsoft.com/de-de/library/windowsazure/hh690928.aspx).</span><span class="sxs-lookup"><span data-stu-id="121bc-213">For more information about the Microsoft Azure Service Bus, see  [Managing Service Bus Service Namespaces](http://msdn.microsoft.com/de-de/library/windowsazure/hh690928.aspx).</span></span>
    
    > <span data-ttu-id="121bc-214">**Hinweis:** Das SharePoint Online-Workflowdebugging verwendet die Relay-Dienst-Komponente von Microsoft Azure Service Bus, sodass Ihnen die Nutzung von Service Bus berechnet wird.</span><span class="sxs-lookup"><span data-stu-id="121bc-214">**Note:** SharePoint Online workflow debugging uses the Relay Service component of the Microsoft Azure Service Bus, so you'll be charged for using the Service Bus.</span></span> <span data-ttu-id="121bc-215">Siehe [Preise-FAQ zu Service Bus](http://msdn.microsoft.com/library/hh667438.aspx).</span><span class="sxs-lookup"><span data-stu-id="121bc-215">See  [Service Bus Pricing FAQ](http://msdn.microsoft.com/library/hh667438.aspx).</span></span> <span data-ttu-id="121bc-216">Sie erhalten in jedem Monat, in dem Sie Visual Studio Professional mit MSDN, Visual Studio Premium mit MSDN oder Visual Studio Ultimate mit MSDN abonnieren, kostenlosen Zugriff auf Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="121bc-216">You get free access to Microsoft Azure each month that you subscribe to Visual Studio Professional with MSDN, Visual Studio Premium with MSDN, or Visual Studio Ultimate with MSDN.</span></span> <span data-ttu-id="121bc-217">Mit diesem Zugriff können Sie das Service Bus-Relay je nach MSDN-Abonnement 1.500, 3.000 oder 3.000 Stunden verwenden.</span><span class="sxs-lookup"><span data-stu-id="121bc-217">With this access, you can use the Service Bus relay for 1,500, 3,000, or 3,000 hours, depending on your MSDN subscription.</span></span> <span data-ttu-id="121bc-218">Siehe [Begrenzte monatliche Nutzung von Microsoft Azure Services ohne Zusatzkosten](http://www.windowsazure.com/en-us/pricing/member-offers/msdn-benefits/).</span><span class="sxs-lookup"><span data-stu-id="121bc-218">See  [Get some amount of Microsoft Azure Services each month at no additional charge](http://www.windowsazure.com/en-us/pricing/member-offers/msdn-benefits/).</span></span> 
4. <span data-ttu-id="121bc-219">Wählen Sie in Microsoft Azure Ihren Service-Namespace, klicken Sie auf den **Zugriffsschlüssel**-Link und kopieren Sie dann den Text im Feld **Verbindungszeichenfolge**.</span><span class="sxs-lookup"><span data-stu-id="121bc-219">In Microsoft Azure, choose your service namespace, choose the **Access Key** link, and then copy the text in the **Connection String** box.</span></span>
    
  
5. <span data-ttu-id="121bc-220">Wählen Sie auf der Eigenschaftenseite Ihres SharePoint-Add-In-Projekts die Registerkarte **SharePoint** aus, und aktivieren Sie dann das Kontrollkästchen **Workflow-Debugging aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="121bc-220">On the properties page of your SharePoint Add-in project, choose the **SharePoint** tab, and then select the **Enable Workflow debugging** check box.</span></span>
    
    <span data-ttu-id="121bc-p121">Sie müssen dieses Feature aktivieren, um Workflows in SharePoint Online zu debuggen. Diese Eigenschaft wird auf alle Ihre SharePoint-Projekte in Visual Studio angewendet. Visual Studio deaktiviert Workflow-Debugging automatisch, wenn Sie Ihre App zur Verteilung im Office Store verpacken.</span><span class="sxs-lookup"><span data-stu-id="121bc-p121">You must enable this feature to debug workflows in SharePoint Online. This property applies to all of your SharePoint projects in Visual Studio. Visual Studio automatically turns off workflow debugging if you package your app for distribution on the Office store.</span></span>
    
  
6. <span data-ttu-id="121bc-p122">Aktivieren Sie das Kontrollkästchen **Debugging über Microsoft Azure Service Bus aktivieren**. Fügen Sie dann im Textfeld **Verbindungszeichenfolge für Microsoft Azure Service Bus** die kopierte Verbindungszeichenfolge ein.</span><span class="sxs-lookup"><span data-stu-id="121bc-p122">Select the **Enable debugging via Microsoft Azure Service Bus** check box. Then, in the **Microsoft Azure Service Bus connection string** box, paste the connection string that you copied.</span></span>
    
  
<span data-ttu-id="121bc-226">Nachdem Sie Workflow-Debugging aktualisiert und eine gültige Verbindungszeichenfolge für Microsoft Azure Service Bus eingegeben haben, können Sie SharePoint Online-Workflows debuggen.</span><span class="sxs-lookup"><span data-stu-id="121bc-226">After you enable workflow debugging and provide a valid connection string for the Microsoft Azure Service Bus, you can debug SharePoint Online workflows.</span></span>
  
    
    

> <span data-ttu-id="121bc-227">**Hinweis:** Wenn Sie Workflow-Debugging nicht deaktiviert haben und nicht jedes Mal eine Benachrichtigung erhalten möchten, wenn Ihr Projekt einen Workflow enthält, deaktivieren Sie das Kontrollkästchen **Mich benachrichtigen, wenn Microsoft Azure Service Bus-Debugging nicht konfiguriert ist**.</span><span class="sxs-lookup"><span data-stu-id="121bc-227">**Note** If you haven't disabled workflow debugging and don't want to receive a notification whenever your project contains a workflow, clear the **Notify me if Microsoft Azure Service Bus debugging is not configured** check box.</span></span>
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="121bc-228">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="121bc-228">Additional resources</span></span>
<span data-ttu-id="121bc-229"><a name="workflowbk_addres"> </a></span><span class="sxs-lookup"><span data-stu-id="121bc-229"></span></span>

<span data-ttu-id="121bc-p123">Die Entwicklung von SharePoint-Workflows bleibt für den Visual Studio-Entwickler größteils unverändert. Die wichtigsten Abschnitte der Dokumentation für SharePoint 2010 sind weiterhin relevant:</span><span class="sxs-lookup"><span data-stu-id="121bc-p123">A great deal of developing SharePoint workflows remains unchanged for the Visual Studio developer. The key sections of the documentation for SharePoint 2010 remain relevant:</span></span>
  
    
    

- <span data-ttu-id="121bc-232">Informationen zur Verwendung von Visual StudioWorkflow-Designer finden Sie unter  [Visual Studio Designer für Windows Workflow Foundation (Übersicht)](http://msdn.microsoft.com/de-de/library/ms441543.aspx).</span><span class="sxs-lookup"><span data-stu-id="121bc-232">For information about using the Visual StudioWorkflow Designer, see  [Visual Studio Designer for Windows Workflow Foundation Overview](http://msdn.microsoft.com/de-de/library/ms441543.aspx).</span></span>
    
  
- <span data-ttu-id="121bc-233">Informationen zur Erstellung von Formularen mit Microsoft ASP.NET finden Sie unter  [Workflowformulare (Übersicht)](http://msdn.microsoft.com/de-de/library/ms457061.aspx).</span><span class="sxs-lookup"><span data-stu-id="121bc-233">For information about creating forms by using Microsoft ASP.NET, see  [Workflow Forms Overview](http://msdn.microsoft.com/de-de/library/ms457061.aspx).</span></span>
    
  
- <span data-ttu-id="121bc-234">Informationen zum Verpacken von Features finden Sie unter  [Workflowentwicklung in Visual Studio](http://msdn.microsoft.com/de-de/library/ms461324.aspx).</span><span class="sxs-lookup"><span data-stu-id="121bc-234">For information about Feature packaging, see  [Using Features in SharePoint Foundation](http://msdn.microsoft.com/de-de/library/ms461324.aspx).</span></span>
    
  
