---
title: "Neuerungen in Workflows für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1d51421b-61ac-46b6-a865-52f968ddc5b3
ms.openlocfilehash: d17537f93cd1636e8399d0713801c975f3e7f042
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-in-workflows-for-sharepoint"></a><span data-ttu-id="31992-102">Neuerungen in Workflows für SharePoint</span><span class="sxs-lookup"><span data-stu-id="31992-102">What's new in workflows for SharePoint</span></span>
<span data-ttu-id="31992-p101">Hier erhalten Sie Informationen zu den neuen Features für Workflows in SharePoint. Das Workflow-Framework in SharePoint hat sich gegenüber früheren Versionen erheblich geändert. Die folgenden Abschnitte bieten kurze Zusammenfassungen zu den wichtigsten Updates und Verbesserungen an der Workflowinfrastruktur.</span><span class="sxs-lookup"><span data-stu-id="31992-p101">Learn about the capabilities and features that are new to workflows in SharePoint. The workflow framework in SharePoint is significantly changed from previous versions. The following sections provide brief summaries of the most significant updates and enhancements to the workflow infrastructure.</span></span>
  
    
    


## <a name="completely-redesigned-workflow-infrastructure"></a><span data-ttu-id="31992-106">Vollständig neu gestaltete Workflowinfrastruktur</span><span class="sxs-lookup"><span data-stu-id="31992-106">Completely redesigned workflow infrastructure</span></span>
<span data-ttu-id="31992-107"><a name="SP15Whatsnewinworflow_infrastructure"> </a></span><span class="sxs-lookup"><span data-stu-id="31992-107"></span></span>

<span data-ttu-id="31992-p102">SharePoint-Workflows werden von Windows Workflow Foundation 4 (WF) unterstützt, das in Vergleich zu früheren Versionen erheblich überarbeitet wurde. Windows Workflow Foundation basiert wiederum auf der von  [Windows Communication Foundation (WCF)](http://msdn.microsoft.com/en-us/netframework/aa663324) bereitgestellten Messaging-Funktion.</span><span class="sxs-lookup"><span data-stu-id="31992-p102">SharePoint workflows are powered by Windows Workflow Foundation 4 (WF), which was substantially redesigned from previous versions. Windows Workflow Foundation, in turn, is built on the messaging functionality that is provided by  [Windows Communication Foundation (WCF)](http://msdn.microsoft.com/en-us/netframework/aa663324).</span></span>
  
    
    
<span data-ttu-id="31992-p103">Das wahrscheinlich bedeutendste Feature der neuen Workflowinfrastruktur ist die Einführung von Microsoft Azure als neuer Host für die Workflowausführung. Das Workflowausführungsmodul befindet sich jetzt außerhalb von SharePoint in Microsoft Azure. Abbild 1 zeigt eine verallgemeinerte Ansicht der neuen Workflowinfrastruktur. Ausführlichere Informationen zu den in Abbildung 1 präsentierten Konzepten finden Sie unter  [Grundlegendes zu SharePoint-Workflows](sharepoint-workflow-fundamentals.md).</span><span class="sxs-lookup"><span data-stu-id="31992-p103">Perhaps the most prominent feature of the new workflow infrastructure is the introduction of Microsoft Azure as the new workflow execution host. The workflow execution engine now lives outside of SharePoint, in Microsoft Azure. Figure 1 provides a generalized, high-level view of the new workflow infrastructure. For a more thorough discussion of the concepts presented in Figure 1, see  [SharePoint workflow fundamentals](sharepoint-workflow-fundamentals.md).</span></span>
  
    
    

<span data-ttu-id="31992-114">**Abbildung 1. Allgemeine Architektur der Workflowinfrastruktur**</span><span class="sxs-lookup"><span data-stu-id="31992-114">**Figure 1. High-level architecture of the workflow infrastructure**</span></span>

  
    
    

  
    
    
![Allgemeine Workflowarchitektur](../images/wfArchitecture1.png)
  
    
    

  
    
    

  
    
    

## <a name="fully-declarative-no-code-authoring-environment"></a><span data-ttu-id="31992-116">Vollständig deklarative Erstellungsumgebung ohne Code</span><span class="sxs-lookup"><span data-stu-id="31992-116">Fully declarative, no-code authoring environment</span></span>
<span data-ttu-id="31992-117"><a name="SP15Whatsnewinworflow_environment"> </a></span><span class="sxs-lookup"><span data-stu-id="31992-117"></span></span>

<span data-ttu-id="31992-p104">Eine weitere bedeutende Änderung besteht darin, dass Workflows auf der WF 4-Plattform vollständig deklarativ sind. Das bedeutet, dass Workflows nicht länger zu verwalteten Assemblys kompiliert und in einem Assembly-Cache bereitgestellt werden. Stattdessen definieren XAML-Dateien Ihre Workflows und legen ihre Ausführung fest.</span><span class="sxs-lookup"><span data-stu-id="31992-p104">Another of the prominent changes is that workflows on the WF 4 platform are fully declarative. That is, workflows are no longer compiled into managed assemblies and deployed to an assembly cache. Instead, XAML files define your workflows and frame their execution.</span></span>
  
    
    

## <a name="enhanced-sharepoint-designer-2013-authoring-support"></a><span data-ttu-id="31992-121">Erweiterte Unterstützung der SharePoint Designer 2013-Erstellung</span><span class="sxs-lookup"><span data-stu-id="31992-121">Enhanced SharePoint Designer 2013 authoring support</span></span>
<span data-ttu-id="31992-122"><a name="SP15Whatsnewinworflow_SPDauthoring"> </a></span><span class="sxs-lookup"><span data-stu-id="31992-122"></span></span>

<span data-ttu-id="31992-p105">SharePoint Designer 2013 wurde mit dem Ziel aktualisiert, es für die Erstellung von SharePoint-Workflows zur gewünschten Erstellungsumgebung zu machen. SharePoint Designer 2013 bietet Workflowautoren sowohl eine Designeroberfläche als auch eine textbasierte Erstellungsumgebung für Workflows. Zusätzlich können Sie für Workflows benutzerdefinierte Aktionen in Visual Studio 2012 entwickeln und diese dann in SharePoint Designer 2013 importieren, wo dann Workflow-Designer darauf zugreifen kann.</span><span class="sxs-lookup"><span data-stu-id="31992-p105">SharePoint Designer 2013 has been updated with the goal of making it the authoring environment of choice for authoring SharePoint workflows. SharePoint Designer 2013 provides workflow authors with both a designer surface and a text-based workflow authoring environment. Additionally, you can develop workflow custom actions in Visual Studio 2012 and then import them into SharePoint Designer 2013, where they can then be accessed from the Workflow Designer.</span></span>
  
    
    
<span data-ttu-id="31992-126">Kurz gesagt, wurden die Anforderungen der Information-Worker ("Hauptbenutzer") und der Entwickler in den Umgebungen zur SharePoint-Workflowerstellung und -entwicklung genutzt.</span><span class="sxs-lookup"><span data-stu-id="31992-126">In short, the needs of both the information worker (the "power user") and the developer have been harnessed in SharePoint workflow authoring and development environments.</span></span>
  
    
    

## <a name="visual-studio-2012-workflow-project-type-support"></a><span data-ttu-id="31992-127">Unterstützung des Visual Studio 2012-Workflowprojekttyps</span><span class="sxs-lookup"><span data-stu-id="31992-127">Visual Studio 2012 workflow project type support</span></span>
<span data-ttu-id="31992-128"><a name="SP15Whatsnewinworflow_VSworkflow"> </a></span><span class="sxs-lookup"><span data-stu-id="31992-128"></span></span>

<span data-ttu-id="31992-p106">Um die Zusammenarbeit von Information-Worker und Softwareentwickler zu vereinfachen, bietet Visual Studio 2012 die SharePoint-Workflowprojekttypen und einen benutzerdefinierten Aktionselementtyp für Workflows. Weitere Informationen zum Entwickeln von Workflows mithilfe von Visual Studio 2012 sowie Informationen zur Unterscheidung von SharePoint Designer 2013 und Visual Studio 2012 bei der Workflowentwicklung finden Sie unter  [Entwickeln von SharePoint-Workflows mit Visual Studio](develop-sharepoint-workflows-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="31992-p106">To make collaboration easier between information worker and software developer, Visual Studio 2012 provides SharePoint workflow project types and a workflow custom action-item type. For more information about developing workflows by using Visual Studio 2012, and for information about differentiating between SharePoint Designer 2013 and Visual Studio 2012 in workflow development, see  [Develop SharePoint workflows using Visual Studio](develop-sharepoint-workflows-using-visual-studio.md).</span></span>
  
    
    

## <a name="support-for-creating-custom-actions"></a><span data-ttu-id="31992-131">Unterstützung für das Erstellen benutzerdefinierter Aktionen</span><span class="sxs-lookup"><span data-stu-id="31992-131">Support for creating custom actions</span></span>
<span data-ttu-id="31992-132"><a name="SP15Whatsnewinworflow_customactions"> </a></span><span class="sxs-lookup"><span data-stu-id="31992-132"></span></span>

<span data-ttu-id="31992-p107">In die Vorhersage der Geschäftsanforderungen von Workflowautoren für die Bereitstellung von Workflowvorlagen, Aktionen und Aktivitäten in SharePoint Designer 2013 und in Visual Studio 2012 wurde viel Arbeit gesteckt. Dennoch können wir nicht die spezifischen Anforderungen jeder einzelnen Person vorhersagen. Aus diesem Grund bietet Visual Studio 2012 einen benutzerdefinierten Aktionselementtyp für Workflows, mit dem Entwickler benutzerdefinierte Aktionen erstellen können. Weitere Informationen zu benutzerdefinierte Aktionen für Workflows finden Sie unter  [Vorgehensweise: Erstellen und POST von benutzerdefinierten Workflowaktionen](how-to-build-and-deploy-workflow-custom-actions.md).</span><span class="sxs-lookup"><span data-stu-id="31992-p107">A lot of effort has gone into anticipating the business requirements of workflow authors in the providing of workflow templates, actions, and activities in SharePoint Designer 2013 and in Visual Studio 2012. However, we also know that we cannot anticipate each person's specific needs. For this reason, Visual Studio 2012 provides a workflow custom action-item type that lets developers create custom actions. For more information about workflow custom actions, see  [How to: Build and deploy workflow custom actions](how-to-build-and-deploy-workflow-custom-actions.md).</span></span>
  
    
    

## <a name="tools-support-for-sharepoint-workflows"></a><span data-ttu-id="31992-137">Unterstützung von Tools für SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="31992-137">Tools support for SharePoint workflows</span></span>
<span data-ttu-id="31992-138"><a name="SP15Whatsnewinworflow_Tools"> </a></span><span class="sxs-lookup"><span data-stu-id="31992-138"></span></span>

<span data-ttu-id="31992-p108">Visual Studio 2012 bietet Vorlagen und Unterstützung für das Erstellen von Workflows für das SharePoint-Workflow-Framework. SharePoint-Workflows ähneln früheren Versionen von Workflows, allerdings werden Sie von WF 4 unterstützt und in Microsoft Azure ausgeführt. Außerdem sind sie rein deklarativ (XAML) und für die Interaktion mit der Cloud sowie für die Arbeit mit SharePoint-Add-Ins konzipiert. Einer ihrer Hauptvorteile besteht darin, dass Sie es Ihnen ermöglichen, Workflows außerhalb von SharePoint Server remote zu hosten und auszuführen.</span><span class="sxs-lookup"><span data-stu-id="31992-p108">Visual Studio 2012 provides templates and support for creating workflows on the SharePoint workflow framework. SharePoint workflows are similar to previous versions of workflows except that they are powered by WF 4 and run in Microsoft Azure. They are also declarative-only (XAML) and designed to interact with the cloud and work with SharePoint Add-ins. One of their primary benefits is that they enable you to remotely host and run workflows outside SharePoint Server.</span></span>
  
    
    

## <a name="new-workflow-actions"></a><span data-ttu-id="31992-142">Neue Workflowaktionen</span><span class="sxs-lookup"><span data-stu-id="31992-142">New workflow actions</span></span>
<span data-ttu-id="31992-143"><a name="SP15Whatsnewinworflow_Newwfactions"> </a></span><span class="sxs-lookup"><span data-stu-id="31992-143"></span></span>

<span data-ttu-id="31992-p109">Nachfolgend sind die neuen Workflowaktionen aufgeführt, die in SharePoint bereitgestellt werden. Ausführliche Informationen zu neuen und überholten Aktionen finden Sie unter  [Workflowaktions- und -aktivitätenreferenz für SharePoint](workflow-actions-and-activities-reference-for-sharepoint.md). Neu für Workflows in SharePoint sind eine Reihe von Workflowaktionen, die Ihnen die Integration mit Project 2013 und die Erstellung projektbasierter Workflows gestatten.</span><span class="sxs-lookup"><span data-stu-id="31992-p109">Following are new workflow actions that are provided in SharePoint. For a full detailing of both new and deprecated actions, see  [Workflow actions and activities reference for SharePoint](workflow-actions-and-activities-reference-for-sharepoint.md). New to workflows in SharePoint are a set of workflow actions that allow you to integrate with Project 2013 and let you create Project-based workflows.</span></span>
  
    
    

<span data-ttu-id="31992-147">**Tabelle 1. Neue Workflowaktionen in SharePoint**</span><span class="sxs-lookup"><span data-stu-id="31992-147">**Table 1. New workflow actions in SharePoint**</span></span>


|<span data-ttu-id="31992-148">**Aktion**</span><span class="sxs-lookup"><span data-stu-id="31992-148">**Action**</span></span>|<span data-ttu-id="31992-149">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="31992-149">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="31992-150">Aufgabe zuweisen</span><span class="sxs-lookup"><span data-stu-id="31992-150">Assign a Task</span></span>  <br/> |<span data-ttu-id="31992-151">Weist eine einzelne Workflowaufgabe zu einem Benutzer oder einer Gruppe zu.</span><span class="sxs-lookup"><span data-stu-id="31992-151">Assigns a single workflow task to a user or group.</span></span>  <br/> |
|<span data-ttu-id="31992-152">Aufgabenprozess starten</span><span class="sxs-lookup"><span data-stu-id="31992-152">Start a Task Process</span></span>  <br/> |<span data-ttu-id="31992-153">Startet die Ausführung eines Aufgabenprozesses.</span><span class="sxs-lookup"><span data-stu-id="31992-153">Initiates execution of a task process.</span></span>  <br/> |
|<span data-ttu-id="31992-154">Zu dieser Phase wechseln</span><span class="sxs-lookup"><span data-stu-id="31992-154">Go to This Stage</span></span>  <br/> |<span data-ttu-id="31992-155">Gibt die nächste Phase in einem Workflow an, an welche die Ablaufsteuerung übergeben werden sollte.</span><span class="sxs-lookup"><span data-stu-id="31992-155">Specifies the next stage in a workflow to which flow control should be handed.</span></span>  <br/> |
|<span data-ttu-id="31992-156">HTTP-Webdienst aufrufen</span><span class="sxs-lookup"><span data-stu-id="31992-156">Call HTTP Web Service</span></span>  <br/> |<span data-ttu-id="31992-157">Dient als Methodenaufruf für einen REST-Endpunkt (Representational State Transfer).</span><span class="sxs-lookup"><span data-stu-id="31992-157">Functions as a method call to a Representational State Transfer (REST) endpoint.</span></span>  <br/> |
|<span data-ttu-id="31992-158">Listenworkflow starten</span><span class="sxs-lookup"><span data-stu-id="31992-158">Start a List Workflow</span></span>  <br/> |<span data-ttu-id="31992-159">Startet einen listenbezogenen Workflow.</span><span class="sxs-lookup"><span data-stu-id="31992-159">Starts a list-scoped workflow.</span></span>  <br/> |
|<span data-ttu-id="31992-160">Website-Workflow starten</span><span class="sxs-lookup"><span data-stu-id="31992-160">Start a Site Workflow</span></span>  <br/> |<span data-ttu-id="31992-161">Startet einen websitebezogenen Workflow.</span><span class="sxs-lookup"><span data-stu-id="31992-161">Starts a site-scoped workflow.</span></span>  <br/> |
|<span data-ttu-id="31992-162">DynamicValue erstellen</span><span class="sxs-lookup"><span data-stu-id="31992-162">Build DynamicValue</span></span>  <br/> |<span data-ttu-id="31992-163">Erstellt eine neue Variable vom Typ **DynamicValue**.</span><span class="sxs-lookup"><span data-stu-id="31992-163">Creates a new variable of type **DynamicValue**.</span></span>  <br/> |
|<span data-ttu-id="31992-164">Eigenschaft von DynamicValue abrufen</span><span class="sxs-lookup"><span data-stu-id="31992-164">Get Property from DynamicValue</span></span>  <br/> |<span data-ttu-id="31992-165">Ruft einen Eigenschaftswert von einer angegebenen Variablen vom Typ **DynamicValue** ab.</span><span class="sxs-lookup"><span data-stu-id="31992-165">Retrieves a property value from a specified variable of type **DynamicValue**.</span></span>  <br/> |
|<span data-ttu-id="31992-166">Elemente in DynamicValue zählen</span><span class="sxs-lookup"><span data-stu-id="31992-166">Count Items in DynamicValue</span></span>  <br/> |<span data-ttu-id="31992-167">Gibt die Anzahl der Zeilen in einer Variablen vom Typ **DynamicValue** zurück.</span><span class="sxs-lookup"><span data-stu-id="31992-167">Returns the number of rows in a variable of type **DynamicValue**.</span></span>  <br/> |
|<span data-ttu-id="31992-168">Zeichenfolge kürzen</span><span class="sxs-lookup"><span data-stu-id="31992-168">Trim String</span></span>  <br/> |<span data-ttu-id="31992-169">Entfernt alle führenden und nachfolgenden Leerzeichen aus der aktuellen Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="31992-169">Removes all leading and trailing white-space characters from the current string.</span></span>  <br/> |
|<span data-ttu-id="31992-170">Teilzeichenfolge in Zeichenfolge suchen</span><span class="sxs-lookup"><span data-stu-id="31992-170">Find Substring in String</span></span>  <br/> |<span data-ttu-id="31992-171">Gibt den auf 1 basierenden Index für das erste Vorkommen eines oder mehrerer Zeichen oder das erste Vorkommen einer Zeichenfolge innerhalb einer Zeichenfolge zurück.</span><span class="sxs-lookup"><span data-stu-id="31992-171">Returns 1-based index of the first occurrence of one or more characters, or the first occurrence of a string, within a string.</span></span>  <br/> |
|<span data-ttu-id="31992-172">Teilzeichenfolge in Zeichenfolge ersetzen</span><span class="sxs-lookup"><span data-stu-id="31992-172">Replace Substring in String</span></span>  <br/> |<span data-ttu-id="31992-173">Gibt eine neue Zeichenfolge zurück, in der alle Vorkommen eines angegebenen Zeichens oder einer Zeichenfolge durch ein anderes angegebenes Zeichen oder durch eine Zeichenfolge ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="31992-173">Returns a new string in which all occurrences of a specified character or string are replaced with another specified character or string.</span></span>  <br/> |
|<span data-ttu-id="31992-174">Dokument übersetzen</span><span class="sxs-lookup"><span data-stu-id="31992-174">Translate Document</span></span>  <br/> |<span data-ttu-id="31992-p110">Funktioniert als Wrapper für die HTTP-Aktivität, die die synchrone Übersetzungs-API aufruft. Sie müssen eine maschinelle Übersetzungsdienstanwendung für die SharePoint-Website konfigurieren, für die Sie den Workflow ausführen.</span><span class="sxs-lookup"><span data-stu-id="31992-p110">Functions as a wrapper around the HTTP activity that calls the synchronous translation API. You must configure a Machine Translation Service Application for the SharePoint site on which you run the workflow.</span></span>  <br/> |
|<span data-ttu-id="31992-177">Workflowstatus festlegen</span><span class="sxs-lookup"><span data-stu-id="31992-177">Set Workflow Status</span></span>  <br/> |<span data-ttu-id="31992-178">Aktualisiert den Workflowstatus gemäß der Meldungszeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="31992-178">Updates workflow status as specified in message string.</span></span>  <br/> |
|<span data-ttu-id="31992-179">Projekt aus aktuellem Element erstellen [Microsoft Project]</span><span class="sxs-lookup"><span data-stu-id="31992-179">Create a Project from Current Item [Microsoft Project]</span></span>  <br/> |<span data-ttu-id="31992-180">Erstellt auf Basis des aktuellen Elements ein Project Server-Projekt.</span><span class="sxs-lookup"><span data-stu-id="31992-180">Creates a Project Server project based on the current item.</span></span>  <br/> |
|<span data-ttu-id="31992-181">Aktuellen Projektphasenstatus auf diesen Wert festlegen [Microsoft Project]</span><span class="sxs-lookup"><span data-stu-id="31992-181">Set the current project stage status to this value [Microsoft Project]</span></span>  <br/> |<span data-ttu-id="31992-182">Legt die beiden Statusfelder innerhalb der aktuellen Phase des Projekts fest.</span><span class="sxs-lookup"><span data-stu-id="31992-182">Sets the two status fields within the current stage of the project.</span></span>  <br/> |
|<span data-ttu-id="31992-183">Statusfeld im Ideenlistenelement auf diesen Wert festlegen [Microsoft Project]</span><span class="sxs-lookup"><span data-stu-id="31992-183">Set the status field in the idea list item to this value [Microsoft Project]</span></span>  <br/> |<span data-ttu-id="31992-184">Aktualisiert das Statusfeld des ursprünglichen SharePoint-Listenelements.</span><span class="sxs-lookup"><span data-stu-id="31992-184">Updates the status field of the original SharePoint list item.</span></span>  <br/> |
|<span data-ttu-id="31992-185">Auf Projektereignis warten [Microsoft Project]</span><span class="sxs-lookup"><span data-stu-id="31992-185">Wait for Project Event [Microsoft Project]</span></span>  <br/> |<span data-ttu-id="31992-186">Hält die aktuelle Instanz des Workflows an, um auf ein angegebenes Projektereignis zu warten: Projekt wurde eingecheckt, Projekt wurde bestätigt, Projekt wurde übermittelt.</span><span class="sxs-lookup"><span data-stu-id="31992-186">Pauses the current instance of the workflow to await a specified Project event: Project checked in, Project committed, Project submitted.</span></span>  <br/> |
|<span data-ttu-id="31992-187">Dieses Feld im Projekt auf diesen Wert festlegen [Microsoft Project]</span><span class="sxs-lookup"><span data-stu-id="31992-187">Set this field in the project to this value [Microsoft Project]</span></span>  <br/> |<span data-ttu-id="31992-188">Legt den Wert für das unternehmensspezifische Feld für ein angegebenes Projekt fest.</span><span class="sxs-lookup"><span data-stu-id="31992-188">Sets the value for the enterprise custom field for a specified project.</span></span>  <br/> |
   

## <a name="additional-resources"></a><span data-ttu-id="31992-189">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="31992-189">Additional resources</span></span>
<span data-ttu-id="31992-190"><a name="SP15Whatsnewinworflow_Addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="31992-190"></span></span>


-  [<span data-ttu-id="31992-191">Erste Schritte mit Workflows in SharePoint</span><span class="sxs-lookup"><span data-stu-id="31992-191">Get started with workflows in SharePoint</span></span>](get-started-with-workflows-in-sharepoint.md)
    
  
-  [<span data-ttu-id="31992-192">Neuerungen für Entwickler in SharePoint</span><span class="sxs-lookup"><span data-stu-id="31992-192">What's new for developers in SharePoint</span></span>](what-s-new-for-developers-in-sharepoint.md)
    
  
-  [<span data-ttu-id="31992-193">Workflowaktions- und -aktivitätenreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="31992-193">Workflow actions and activities reference for SharePoint</span></span>](workflow-actions-and-activities-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="31992-194">Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)</span><span class="sxs-lookup"><span data-stu-id="31992-194">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  

