---
title: "Problembehandlung bei SharePoint Server-Workflow-Überprüfungsfehlern in Visio"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c21cc3e2-45bd-4d34-a57d-dd0954436bd8
ms.openlocfilehash: df9cbf15f3249b8dae78463b97be7d1f9cae595b
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="troubleshooting-sharepoint-server-workflow-validation-errors-in-visio"></a><span data-ttu-id="1682a-102">Problembehandlung bei SharePoint Server-Workflow-Überprüfungsfehlern in Visio</span><span class="sxs-lookup"><span data-stu-id="1682a-102">Troubleshooting SharePoint Server workflow validation errors in Visio</span></span>
<span data-ttu-id="1682a-103">Verwenden Sie diese Übersicht, Validierung und fehlerüberprüfung Probleme in der Workflowvorlage Microsoft SharePoint in Microsoft Visio 2013 und Microsoft SharePoint Designer 2013 aufzulösen.</span><span class="sxs-lookup"><span data-stu-id="1682a-103">Use this reference to resolve validation and error-checking issues in the Microsoft SharePoint Workflow template in Microsoft Visio 2013 and Microsoft SharePoint Designer 2013.</span></span>
## <a name="sharepoint-workflow-validation-issues"></a><span data-ttu-id="1682a-104">Probleme bei der Validierung von SharePoint-workflow</span><span class="sxs-lookup"><span data-stu-id="1682a-104">SharePoint workflow validation issues</span></span>
<span data-ttu-id="1682a-105"><a name="VSSPD_Trouble_Issues"> </a></span><span class="sxs-lookup"><span data-stu-id="1682a-105"><a name="VSSPD_Trouble_Issues"> </a></span></span>

<span data-ttu-id="1682a-p101">Die folgende Tabelle enthält eine Liste aller die Überprüfungsprobleme, die in den Bereich Probleme in Microsoft Visio 2013 oder des visuellen Designers in Microsoft SharePoint Designer 2013 angezeigt werden können. Jeder Fehler hat eine vorgeschlagene zur Behebung dieses Problems auszuführende Aktion.</span><span class="sxs-lookup"><span data-stu-id="1682a-p101">The following table lists all of the validation issues that can appear in the Issues pane in Microsoft Visio 2013 or the Visual Designer in Microsoft SharePoint Designer 2013. Each error has a suggested action to take for resolving the problem.</span></span>
  
    
    


|<span data-ttu-id="1682a-108">**Fehlertext**</span><span class="sxs-lookup"><span data-stu-id="1682a-108">**Error text**</span></span>|<span data-ttu-id="1682a-109">**Vorgeschlagene Aktion**</span><span class="sxs-lookup"><span data-stu-id="1682a-109">**Suggested action**</span></span>|
|:-----|:-----|
|<span data-ttu-id="1682a-110">Zwischen Workflow-Shapes bestehen doppelte Verbindungen.</span><span class="sxs-lookup"><span data-stu-id="1682a-110">Duplicate connections exist between workflow shapes.</span></span>  <br/> |<span data-ttu-id="1682a-111">Entfernen Sie den redundanten Connector, indem markieren und löschen.</span><span class="sxs-lookup"><span data-stu-id="1682a-111">Remove the redundant connector by selecting and deleting it.</span></span>  <br/> |
|<span data-ttu-id="1682a-112">Schleife zurück zu übergeordnetem Shape ist nicht innerhalb einer Phase oder Schritt zulässig.</span><span class="sxs-lookup"><span data-stu-id="1682a-112">Loop back to parent shape is not allowed within a stage or step.</span></span>  <br/> |<span data-ttu-id="1682a-p102">Weder Visio Professional 2013 noch SharePoint Designer 2013 unterstützt Workflows mit impliziten Schleifen innerhalb einer Phase. Überprüfen Sie den Workflow für Schleifen und Löschen der Schleifen Verbindungen. Wenn Sie einen SharePoint-Workflow erstellen, der eine Reihe von Schleifen Schritten innerhalb einer Phase enthält möchten, müssen Sie die Schleife Container verwenden. Alle Aktionen innerhalb dieser Container werden wiederholt. Eine weitere Option ist Phasen verwenden, das Wechseln zu einem früheren Zeitpunkt an.</span><span class="sxs-lookup"><span data-stu-id="1682a-p102">Neither Visio Professional 2013 nor SharePoint Designer 2013 supports workflows with implicit loops inside of a stage. Check your workflow for loops and delete the looping connections. If you want to create a SharePoint workflow that includes a set of looping steps inside of a stage, you must use the loop containers. Any actions inside of these containers will loop. Another option is to use stages that go-to a previous stage.</span></span>  <br/> |
|<span data-ttu-id="1682a-118">Parallele Aktivitäten, die auch sequenziell sind, sind nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="1682a-118">Parallel activities that are also sequential are not allowed.</span></span>  <br/> |<span data-ttu-id="1682a-p103">Aktivitäten können entweder parallel oder sequenzielle, jedoch nicht beide gleichzeitig sein. Entfernen Sie für parallele Aktivitäten die sequenzielle Connectors. Entfernen Sie die parallele Connectors für sequenzielle Aktivitäten. In einigen Fällen können gleichzeitig parallele und sequenzielle Aktivitäten zum Identifizieren schwierig sein. Folgende Überprüfungsfehler andere allgemeinen Instanzen von parallelen und sequenziellen Anordnung anzeigen und alternative Modalitäten anbieten.</span><span class="sxs-lookup"><span data-stu-id="1682a-p103">Activities can be either parallel or sequential, but not both simultaneously. For parallel activities, remove the sequential connectors. For sequential activities, remove the parallel connectors. Sometimes, simultaneously parallel and sequential activities can be difficult to identify. The following validation errors show other common instances of parallel and sequential arrangement and offer alternative arrangements.</span></span>  <br/> <span data-ttu-id="1682a-124">Um Connectors, zeigen Sie auf der gleichen Aktivität von mehreren Pfaden zu vermeiden, versuchen Sie die Aktivität.</span><span class="sxs-lookup"><span data-stu-id="1682a-124">To avoid having connectors point to the same activity from multiple paths, try duplicating the activity.</span></span>  <br/> |
|<span data-ttu-id="1682a-125">Die Form ' Bedingung ' hat keine Verbindung mit der Bezeichnung mit Ja oder Nein.</span><span class="sxs-lookup"><span data-stu-id="1682a-125">The condition shape does not have connections labeled with Yes or No.</span></span>  <br/> |<span data-ttu-id="1682a-126">Mit der rechten Maustaste den Connector Zuweisen von der Bezeichnung "Ja" oder "Nein".</span><span class="sxs-lookup"><span data-stu-id="1682a-126">Right-click the connector to assign the label "Yes" or "No."</span></span>  <br/> |
|<span data-ttu-id="1682a-127">Die Form ' Bedingung ' benötigen ausgehende Verbindungen mit der Bezeichnung Ja und Nein.</span><span class="sxs-lookup"><span data-stu-id="1682a-127">The condition shape must have outgoing connections with label Yes and No.</span></span>  <br/> |<span data-ttu-id="1682a-p104">Sicherstellen Sie, dass die Bedingung Shapes ausgehenden Connectors an andere Shapes Workflow angefügt haben. Jede Form ' Bedingung ' muss eine "Ja" und eine ausgehende Verbindung "No" haben.</span><span class="sxs-lookup"><span data-stu-id="1682a-p104">Ensure that condition shapes have outgoing connectors attached to other workflow shapes. Each condition shape must have a "Yes" and a "No" outgoing connection.</span></span>  <br/> |
|<span data-ttu-id="1682a-p105">Der Verbinder ist keinen SharePoint-Workflow-Connector. Verwenden Sie AutoConnect oder das Verbinder-Tool, um die Shapes verbinden.</span><span class="sxs-lookup"><span data-stu-id="1682a-p105">The connector is not a SharePoint workflow connector. Use AutoConnect or the connector tool to connect your shapes.</span></span>  <br/> |<span data-ttu-id="1682a-p106">Vermeiden Sie die Connectors aus anderen Diagrammen wiederverwenden, wie sie unbedingt nicht mit SharePoint-Workflows verwendet werden soll. Löschen Sie den Verbinder, und verwenden Sie die Verbinder oder AutoConnect ersetzen durch eine neue Verbindung.</span><span class="sxs-lookup"><span data-stu-id="1682a-p106">Avoid reusing connectors from other diagrams as they are not necessarily designed to be used with SharePoint workflows. Delete the selected connector and use the connector tool or AutoConnect to replace with a new connector.</span></span>  <br/> |
|<span data-ttu-id="1682a-134">Der Verbinder muss mit zwei workflowformen verbunden sein.</span><span class="sxs-lookup"><span data-stu-id="1682a-134">The connector must be connected to two workflow shapes.</span></span>  <br/> |<span data-ttu-id="1682a-135">Entfernen von Sackgasse Connectors oder Anfügen an ein zweites Shape.</span><span class="sxs-lookup"><span data-stu-id="1682a-135">Remove dead-end connectors or attach them to a second shape.</span></span>  <br/> |
|<span data-ttu-id="1682a-136">Das Diagramm darf nur einen Workflow und ein Anfangs-Shape haben.</span><span class="sxs-lookup"><span data-stu-id="1682a-136">The diagram must only have one workflow and one Start shape.</span></span>  <br/> |<span data-ttu-id="1682a-p107">Alle Pfade müssen aus der gleichen Anfangs-Shape stammen. Entfernen von zusätzlichen Start-Shapes und ordnen Sie die Connectors, um der Pfad an einem Ort zu starten.</span><span class="sxs-lookup"><span data-stu-id="1682a-p107">All paths must originate from the same Start shape. Remove extra Start shapes and arrange the connectors so that the path starts in one place.</span></span>  <br/> |
|<span data-ttu-id="1682a-p108">Das Shape ist kein SharePoint-Workflow-Shape. In einem Workflow können nur SharePoint-Workflow-Shapes verbunden werden.</span><span class="sxs-lookup"><span data-stu-id="1682a-p108">The shape is not a SharePoint workflow shape. Only SharePoint workflow shapes can be connected in a workflow.</span></span>  <br/> |<span data-ttu-id="1682a-p109">In der Microsoft SharePoint-Workflow-Vorlage können nur Workflow-Shapes aus den Schablonen SharePoint-Workflow verwendet werden. Andere Flussdiagrammshapes werden nicht erkannt und verhindern, dass den Workflow in SharePoint Designer exportiert wird.</span><span class="sxs-lookup"><span data-stu-id="1682a-p109">Only workflow shapes from the SharePoint Workflow stencils can be used in the Microsoft SharePoint Workflow template. Other flowchart shapes are not recognized and prevent the workflow from being exported to SharePoint Designer.</span></span>  <br/> |
|<span data-ttu-id="1682a-143">Das Anfangs-Shape darf keine eingehenden Verbindungen haben</span><span class="sxs-lookup"><span data-stu-id="1682a-143">The Start shape must not have incoming connections.</span></span>  <br/> |<span data-ttu-id="1682a-144">Entfernen Sie den eingehenden Connector an das Anfangs-Shape.</span><span class="sxs-lookup"><span data-stu-id="1682a-144">Remove the incoming connector to the Start shape.</span></span>  <br/> |
|<span data-ttu-id="1682a-145">Der Workflow muss ein Anfangs-Shape haben</span><span class="sxs-lookup"><span data-stu-id="1682a-145">The workflow must have a Start shape.</span></span>  <br/> |<span data-ttu-id="1682a-146">Fügen Sie ein Anfangs-Shape an den Anfang des Workflows, und schließen Sie es an die erste Aktivität.</span><span class="sxs-lookup"><span data-stu-id="1682a-146">Add a Start shape to the beginning of the workflow and connect it to the first activity.</span></span>  <br/> |
|<span data-ttu-id="1682a-147">Das Workflow-Shape ist nicht mit dem Workflow verbunden.</span><span class="sxs-lookup"><span data-stu-id="1682a-147">The workflow shape is not connected to the workflow.</span></span>  <br/> |<span data-ttu-id="1682a-p110">Wenn das Workflow-Shape erforderlich ist, fügen Sie Connectors So fügen Sie es auf den Workflow Pfad hinzu. Anderenfalls Löschen des Shapes.</span><span class="sxs-lookup"><span data-stu-id="1682a-p110">If the workflow shape is necessary, add connectors to attach it to the workflow path. Otherwise, delete the shape.</span></span>  <br/> |
|<span data-ttu-id="1682a-150">Workflow geschachtelte Ebenen darf maximal 10 nicht überschreiten.</span><span class="sxs-lookup"><span data-stu-id="1682a-150">Workflow nesting levels must not exceed a maximum of 10.</span></span>  <br/> |<span data-ttu-id="1682a-p111">Visio 2013 können maximal 10 Ebenen der Schachtelung Workflowaktivitäten erkennen. Neu anordnen Sie, um Komplexität eliminiert Aktivitäten oder den Pfad der Workflow in mehr als eine Verzweigung Aufteilen des Workflows.</span><span class="sxs-lookup"><span data-stu-id="1682a-p111">Visio 2013 can recognize a maximum of 10 levels of nesting workflow activities. Rearrange the workflow to reduce complexity by eliminating activities or dividing the workflow path into more than one branch.</span></span>  <br/> |
|<span data-ttu-id="1682a-153">Das Anfangs-Shape kann nur mit einem Workflow Phasen-Shape verbunden werden.</span><span class="sxs-lookup"><span data-stu-id="1682a-153">The start shape can only be connected to a workflow stage shape.</span></span>  <br/> |<span data-ttu-id="1682a-p112">Alle Workflowdiagramme müssen mit nur ein Anfangs-Shape beginnen. Das Anfangs-Shape muss mit einem Phasen-Shape verbunden sein. Falls erforderlich, fügen Sie ein Anfangs-Shape an den Anfang des Workflows. Sie können auch ein Anfangs-Shape an den Anfang des Workflows in der phasenansicht in Visio 2013 hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="1682a-p112">All workflow diagrams must begin with only one Start shape. The Start shape must be connected to a Stage shape. If necessary, add a Start shape to the beginning of the workflow. You can also add a Start shape to the beginning of the workflow in Stage view in Visio 2013.</span></span>  <br/> |
|<span data-ttu-id="1682a-158">Eine Phase kann nicht in einem anderen Shape geschachtelt werden.</span><span class="sxs-lookup"><span data-stu-id="1682a-158">A stage cannot be nested within any other shape.</span></span>  <br/> |<span data-ttu-id="1682a-p113">Phasen sind in SharePoint Workflowdiagramme Shapes der obersten Ebene. Sie können kein Shape in allen anderen Container-Shapes, einschließlich Schritte, Schleifen oder anderen Stufen platzieren.</span><span class="sxs-lookup"><span data-stu-id="1682a-p113">Stages are top-level shapes in SharePoint workflow diagrams. You cannot place a shape within any other container shape, including steps, loops, or other stages.</span></span>  <br/> <span data-ttu-id="1682a-p114">Falls möglich, verschieben Sie die Phase, damit es außerhalb von Container-Shapes ist, und schließen Sie die Phase. Wenn Sie eine logische Gruppierung von Actions- und Conditions innerhalb einer Phase oder Schleife erstellen möchten, verwenden Sie stattdessen eine Schritt-Form.</span><span class="sxs-lookup"><span data-stu-id="1682a-p114">If possible, move the stage so that it is outside of all other container shapes and reconnect the stage. If you want to create a logical grouping of actions and conditions within a stage or loop, use a Step shape instead.</span></span>  <br/> |
|<span data-ttu-id="1682a-163">Eine Phase kann nur an eine andere Stufe, bedingungs-Shape oder ein Abschlusszeichen verbunden werden.</span><span class="sxs-lookup"><span data-stu-id="1682a-163">A stage can only be connected to another stage, condition shape, or a terminator.</span></span>  <br/> |<span data-ttu-id="1682a-p115">Phasen können nur mit anderen Shapes der obersten Ebene, einschließlich der Bedingungen, Abschlusszeichen oder anderen Stufen verbunden werden. Eine Phase kann nicht mit Aktionen, Schritten oder Schleifen auf der obersten Ebene verbunden werden. Neu anordnen des Workflowdiagramms, damit die Phase nur mit anderen Shapes der obersten Ebene verbunden ist.</span><span class="sxs-lookup"><span data-stu-id="1682a-p115">Stages can be connected only to other top-level shapes, including conditions, terminators, or other stages. A stage cannot be connected to actions, steps, or loops at the top level. Rearrange the workflow diagram so that the stage is connected only to other top-level shapes.</span></span>  <br/> |
|<span data-ttu-id="1682a-167">Phase Schritt und Schleife Container können nicht überlappt werden.</span><span class="sxs-lookup"><span data-stu-id="1682a-167">Stage, step, and loop containers cannot be overlapped.</span></span>  <br/> |<span data-ttu-id="1682a-p116">Die Grenzen der Container-Shapes, wie etwa Phasen, Schleifen und Schritte können nicht berühren oder überschneiden sich. Wenn Sie eine Container-Shape in einer anderen einschließen möchten (beispielsweise enthalten eine Schleife innerhalb einer Phase befinden), achten Sie darauf, dass das enthaltene Shape vollständig innerhalb der Grenzen des Containers ist. Wenn Sie nicht möchten, führen Sie eine Container-Shape der anderen, Space die Shapes in Ihrem Diagramm enthalten sein, damit die Grenzen der Container-Shapes nicht mehr schneidet oder berühren.</span><span class="sxs-lookup"><span data-stu-id="1682a-p116">The boundaries of container shapes, such as stages, steps, and loops, cannot touch or overlap. If you want to include one container shape within another (for example, include a loop within a stage), be sure that the contained shape is entirely within the bounds of the container. If you do not want one container shape to be contained by the other, space out the shapes in your diagram so that the bounds of the container shapes no longer cross or touch each other.</span></span>  <br/> |
|<span data-ttu-id="1682a-171">Workflow-Shapes aus anderen Vorlagen-Versionen sind keine gültige Workflow-Shapes.</span><span class="sxs-lookup"><span data-stu-id="1682a-171">Workflow shapes from other templates/versions are not valid workflow shapes.</span></span>  <br/> |<span data-ttu-id="1682a-p117">Sie können die Shapes nur aus der SharePoint Workflowaktionen, SharePoint Workflowbedingungen, und SharePoint Workflow Abschlusszeichen Schablonen und Connectors, die mit AutoConnect oder der Vorlage in einem Workflowdiagramm Microsoft SharePoint zugeordneten Verbinder-Tool erstellt werden. Alle anderen Shapes sind nicht gültig Verbindungen innerhalb der Validierungsregeln Workflow. Sie können andere Shapes auf die Design-Zeichenbereich platzieren, solange sie nicht mit dem Workflow verbunden sind.</span><span class="sxs-lookup"><span data-stu-id="1682a-p117">You can use shapes only from the SharePoint Workflow Actions, SharePoint Workflow Conditions, and SharePoint Workflow Terminators stencils, and connectors that are created with AutoConnect or the Connector tool associated with the template in a Microsoft SharePoint Workflow diagram. All other shapes are not valid connections within the workflow validation rules. You can place other shapes on the design canvas as long as they are not connected to the Workflow.  </span></span><br/> <span data-ttu-id="1682a-p118">Müssen Sie eine Aktion oder Bedingung, die nicht mit einer Form in eine zugeordnete Workflowvorlage Microsoft SharePoint Schablonen dargestellt wird, sollten Sie eine benutzerdefinierte Workflowaktion erstellen. Benutzerdefinierte Workflowaktionen können in Microsoft Visual Studio 2012 erstellt und in SharePoint Workflows in SharePoint Designer 2013 integriert werden. Weitere Informationen zum Erstellen von benutzerdefinierter Aktionen in Visual Studio 2012 finden Artikel,  [Entwickeln von SharePoint-Workflows mit Visual Studio](develop-sharepoint-workflows-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="1682a-p118">If you need to include an action or condition that is not represented with a shape in one of the stencils associated with the Microsoft SharePoint Workflow template, consider creating a custom workflow action. Custom workflow actions can be created in Microsoft Visual Studio 2012 and incorporated into SharePoint workflows in SharePoint Designer 2013. For more information about how to create custom actions in Visual Studio 2012, see the article  [Develop SharePoint workflows using Visual Studio](develop-sharepoint-workflows-using-visual-studio.md).  </span></span><br/> |
|<span data-ttu-id="1682a-178">Ein Shape kann nicht außerhalb der Anfangs-/Pfad der Container des aktuellen Shapes verbunden werden.</span><span class="sxs-lookup"><span data-stu-id="1682a-178">A shape cannot be connected outside of the start/end path of the current shape's container.</span></span>  <br/> |<span data-ttu-id="1682a-p119">Alle Formen innerhalb einer Phase, Schleife oder Schritt müssen vollständig in das Container-Shape enthalten sein. Shapes können nicht zu Shapes verbinden, die nicht in demselben Container enthalten sind. Neu anordnen des Workflowdiagramms, damit an andere Shapes im Container alle Aktionen, Bedingungen, Schleifen und Schritte in das Container-Shape verbinden.</span><span class="sxs-lookup"><span data-stu-id="1682a-p119">All shapes contained within a stage, loop, or step must be entirely contained within that container shape. Shapes cannot connect to any shapes that are not contained in the same container. Rearrange the workflow diagram so that all actions, conditions, loops, and steps within the container shape connect to other shapes in the container.</span></span>  <br/> <span data-ttu-id="1682a-182">Wenn das Shape auf eine Aktivität außerhalb des Containers verbinden muss, verbinden Sie die Form an das Ausgangs-Shape, das dem Container zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="1682a-182">If the shape must connect to an activity outside of the container, connect the shape to the Exit shape associated with the container.</span></span>  <br/> |
|<span data-ttu-id="1682a-183">Ungültiger Übergang-Shape.</span><span class="sxs-lookup"><span data-stu-id="1682a-183">Invalid transition shape.</span></span>  <br/> |<span data-ttu-id="1682a-p120">Wenn ein Shape nicht Bedingung oder nicht-Stufen Ebene der Basis des Workflows hinzugefügt wird. Ebene der Basis eines Workflows ist möglicherweise nur Phasen und Bedingungen vorhanden. Alle anderen Shapes, die dieser Ebene hinzugefügt werden, werden dieser Fehler verursacht. Sie sollten nicht Bedingung und nicht-Stufen-Shapes in einer Bedingung oder Phase Form kapseln.</span><span class="sxs-lookup"><span data-stu-id="1682a-p120">When a non-condition or non-stage shape is added at the base level of the workflow. Only stages and conditions may exist at the base level of a workflow. Any other shapes that are added to this level will cause this error. You should encapsulate non-condition and non-stage shapes in a condition or stage shape.</span></span>  <br/> |
|<span data-ttu-id="1682a-188">Phasen, Schleifen und Schritte können nur eine eingehende und eine ausgehende Verbindung haben.</span><span class="sxs-lookup"><span data-stu-id="1682a-188">Stages, steps, and loops may have only one incoming and one outgoing connection.</span></span>  <br/> |<span data-ttu-id="1682a-p121">Alle Container-Shapes können nur ein eingehender Connector mit dem Shape EINGABETASTE haben, die zugeordnet ist. Container-Shapes können auf ähnliche Weise nur eine ausgehende Verbindung von ihrer Ausgangs-Shape haben. Neu anordnen Sie das Diagramm, sodass jeder Container einen einzelnen ein- und ausgehenden Pfad hat. Sie müssen möglicherweise zusätzliche Phasen oder Zuordnungstabelle Shapes an den Workflow zum Beheben dieses Fehlers hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="1682a-p121">All container shapes can have only one incoming connector to the Enter shape that is associated with them. Similarly, container shapes can have only one outgoing connector from their Exit shape. Rearrange the diagram so that each container has a single incoming and outgoing path. You may need to add additional stages or Junction shapes to the workflow to fix this error.</span></span>  <br/> |
|<span data-ttu-id="1682a-193">Eine Phase Name muss eindeutig sein und darf nicht leer sein.</span><span class="sxs-lookup"><span data-stu-id="1682a-193">A stage name must be unique and cannot be empty.</span></span>  <br/> |<span data-ttu-id="1682a-p122">Jede Stufe im Workflow muss einen eindeutigen Namen besitzen. Wechseln Sie zum phasenansicht, und stellen Sie sicher, dass jeder Phase einen eigene Namen hat.</span><span class="sxs-lookup"><span data-stu-id="1682a-p122">Each stage in the workflow must have a unique name. Switch to Stage view and be sure that each stage has its own name.</span></span>  <br/> |
|<span data-ttu-id="1682a-196">Projektstufe wurde nicht konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="1682a-196">The Project stage has not been configured.</span></span>  <br/> |<span data-ttu-id="1682a-p123">Für Workflows Projekt basiert muss jeder Phase in eine Stufe in Project Server verknüpft werden. Wenn eine Phase in eine Stufe auf dem Server nicht verknüpft wurde, wird dieser Fehler angezeigt. Um dieses Problem zu beheben, öffnen Sie Eigenschaftenraster Stufe aus, und legen Sie eine Phase aus der Dropdownliste Phase.</span><span class="sxs-lookup"><span data-stu-id="1682a-p123">For Project based workflows, every stage must be linked to a stage on the Project Server. If a stage has not been linked to a stage on the server, you will see this error. To correct this issue, open the Stage property grid and set a stage from the stage drop-down.</span></span>  <br/> |
|<span data-ttu-id="1682a-200">Eine parallele Aktivität muss mit einem Shape starten Verzweigung "Parallel" beginnen.</span><span class="sxs-lookup"><span data-stu-id="1682a-200">A parallel activity must begin with a Start Parallel Branch shape.</span></span>  <br/> |<span data-ttu-id="1682a-201">Überprüfen Sie jede parallele Aktivität im Workflow, um sicherzustellen, dass es eine parallele Verzweigung starten Form hat, vor dem Beginn der parallelen Aktivitätsfeeds.</span><span class="sxs-lookup"><span data-stu-id="1682a-201">Check each parallel activity in the workflow to be sure that it has a Start Parallel Branch shape before the parallel activity begins.</span></span>  <br/> |
   

## <a name="additional-resources"></a><span data-ttu-id="1682a-202">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="1682a-202">Additional resources</span></span>
<span data-ttu-id="1682a-203"><a name="VSSPD_Trouble_Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="1682a-203"><a name="VSSPD_Trouble_Additional"> </a></span></span>


-  [<span data-ttu-id="1682a-204">Workflowentwicklung in SharePoint Designer und Visio</span><span class="sxs-lookup"><span data-stu-id="1682a-204">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [<span data-ttu-id="1682a-205">Shapes in der SharePoint Server-Workflowvorlage in Visio</span><span class="sxs-lookup"><span data-stu-id="1682a-205">Shapes in the SharePoint Server workflow template in Visio</span></span>](shapes-in-the-sharepoint-server-workflow-template-in-visio.md)
    
  
-  [<span data-ttu-id="1682a-206">Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)</span><span class="sxs-lookup"><span data-stu-id="1682a-206">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  
-  [<span data-ttu-id="1682a-207">Erstellen, Importieren und Exportieren von SharePoint-Workflows in Visio</span><span class="sxs-lookup"><span data-stu-id="1682a-207">Create, import, and export SharePoint workflows in Visio 2010</span></span>](http://office.microsoft.com/en-us/visio-help/create-import-and-export-sharepoint-workflows-in-visio-HA101888007.aspx)
    
  
-  [<span data-ttu-id="1682a-208">SharePoint Developer Center</span><span class="sxs-lookup"><span data-stu-id="1682a-208">SharePoint Developer Center</span></span>](http://msdn.microsoft.com/en-us/sharepoint/default.aspx)
    
  
-  [<span data-ttu-id="1682a-209">Visio Developer Center</span><span class="sxs-lookup"><span data-stu-id="1682a-209">Visio Developer Center</span></span>](http://msdn.microsoft.com/en-us/office/aa905478)
    
  
