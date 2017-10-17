---
title: "Probleme bei der Überprüfung in Visio (SharePoint 2010-Workflowplattform)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 416c8269-3c4e-40f4-bc20-a625f07a4dac
ms.openlocfilehash: 170ff120dceb06e6854aaf63079f9f3027c244a3
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="validation-issues-in-visio-sharepoint-2010-workflow-platform"></a><span data-ttu-id="ef8ca-102">Probleme bei der Überprüfung in Visio (SharePoint 2010-Workflowplattform)</span><span class="sxs-lookup"><span data-stu-id="ef8ca-102">Validation issues in Visio (SharePoint 2010 Workflow platform)</span></span>
<span data-ttu-id="ef8ca-p101">Verwenden Sie diese Übersicht, bei der Validierung von Problemen beim Exportieren eines SharePoint-Workflows aus Visio Professional 2013 SharePoint Designer 2013 unterstützen. Dieser Artikel beschreibt Überprüfungsprobleme, die auftreten können, wenn Sie die SharePoint 2010-Workflow-Plattform in SharePoint Designer 2013 verwenden.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p101">Use this reference to help resolve validation issues when you export a SharePoint workflow from Visio Professional 2013 to SharePoint Designer 2013. This article describes validation issues that might arise when you use the SharePoint 2010 Workflow platform in SharePoint Designer 2013.</span></span>
  
    
    


## <a name="introduction"></a><span data-ttu-id="ef8ca-105">Einführung</span><span class="sxs-lookup"><span data-stu-id="ef8ca-105">Introduction</span></span>
<span data-ttu-id="ef8ca-106"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-106"></span></span>

<span data-ttu-id="ef8ca-p102">Beim Exportieren eines SharePoint-Workflows von Microsoft Visio Professional 2013 in Microsoft SharePoint Designer 2013 muss das Diagramm zuerst überprüft werden. Das Workflowdiagramm nicht gültig ist, wird ein Fenster **Probleme** angezeigt, die enthält eine Liste der Punkte, die repariert werden muss, bevor der Workflow exportiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p102">When you export a SharePoint workflow from Microsoft Visio Professional 2013 to Microsoft SharePoint Designer 2013, the diagram must first be validated. If the workflow diagram is not valid, an **Issues** window appears that includes a list of issues that must be repaired before the workflow can be exported..</span></span>
  
    
    
<span data-ttu-id="ef8ca-p103">Dieser Artikel enthält eine Beschreibung, Beispiel und vorgeschlagenen Aktion für jeden Workflow-Überprüfungsprobleme, die Sie in Visio Professional 2013 erhalten können. Wenn Sie über ein Problem bei der Validierung benachrichtigt werden, finden Sie in der Liste unten die Bezeichnung des Problems, mithilfe des Beispiels zum Identifizieren, wo das Problem liegt, und befolgen Sie die vorgeschlagene Aktion zur Behebung.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p103">This article includes a description, example, and suggested action for each of the workflow validation issues that you can receive in Visio Professional 2013. If you receive notice of an issue during validation, find the issue name in the list below, use the example to help identify where the problem is, and then follow the suggested action to resolve it.</span></span>
  
    
    

## <a name="a-custom-action-cannot-be-added-to-a-workflow-diagram"></a><span data-ttu-id="ef8ca-111">Eine benutzerdefinierte Aktion kann nicht hinzugefügt werden, einem Workflowdiagramm</span><span class="sxs-lookup"><span data-stu-id="ef8ca-111">A custom action cannot be added to a workflow diagram</span></span>
<span data-ttu-id="ef8ca-112"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-112"></span></span>

<span data-ttu-id="ef8ca-113">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-113">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p104">Eine benutzerdefinierte Aktion kann keines Workflowdiagramms hinzugefügt werden. Die benutzerdefinierte Aktion kann nur beim Importieren des Workflows aus SharePoint Designer generiert werden.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p104">A Custom action cannot be added to a workflow diagram. The Custom action can only be generated when importing workflow from SharePoint Designer.</span></span>
  
    
    
<span data-ttu-id="ef8ca-116">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-116">Example:</span></span>
  
    
    

  
    
    
![Eine benutzerdefinierte Aktion kann nicht hinzugefügt werden.](../images/spd15-wf-error1.JPG)
  
    
    
<span data-ttu-id="ef8ca-118">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-118">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p105">Wenn Sie eine Aktion zu einem Workflow hinzufügen möchten, und ein master-Shape ist nicht in der Schablone dafür vorhanden, nicht erstellen Sie eigener Shape oder importieren Sie eine aus einer anderen Schablone. Verwenden Sie stattdessen einer vorhandenen Form, und klicken Sie dann verwenden Sie das Feature **Kommentar hinzufügen** der Form, um das beabsichtigte Verhalten anzugeben.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p105">If you want to add an action to your workflow and a master shape does not exist for it in the stencil, do not create your own shape or import one from a different stencil. Instead, use an existing shape, and then use the **Add Comment** feature of the shape to specify the intended behavior.</span></span>
  
    
    

## <a name="a-custom-condition-cannot-be-added-to-a-workflow-diagram"></a><span data-ttu-id="ef8ca-121">Eine benutzerdefinierte Bedingung kann nicht hinzugefügt werden, einem Workflowdiagramm</span><span class="sxs-lookup"><span data-stu-id="ef8ca-121">A Custom condition cannot be added to a workflow diagram</span></span>
<span data-ttu-id="ef8ca-122"><a name="section3"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-122"></span></span>

<span data-ttu-id="ef8ca-123">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-123">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p106">Eine benutzerdefinierte Bedingung kann einem Workflowdiagramm hinzugefügt werden. Benutzerdefinierte Bedingung kann nur beim Importieren des Workflows aus SharePoint Designer generiert werden.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p106">A Custom condition cannot be added to a workflow diagram. The custom condition can only be generated when importing workflow from SharePoint Designer.</span></span>
  
    
    
<span data-ttu-id="ef8ca-126">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-126">Example:</span></span>
  
    
    

  
    
    
![Eine benutzerdefinierte Bedingung kann nicht hinzugefügt werden](../images/spd15-wf-error2.JPG)
  
    
    
<span data-ttu-id="ef8ca-128">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-128">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p107">Wenn Sie eine Bedingung zu einem Workflow hinzufügen möchten, und ein master-Shape ist nicht in der Schablone dafür vorhanden, nicht erstellen Sie eigener Shape oder importieren Sie eine aus einer anderen Schablone. Verwenden Sie stattdessen einer vorhandenen Form, und klicken Sie dann verwenden Sie das Feature **Kommentar hinzufügen** der Form, um das beabsichtigte Verhalten anzugeben.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p107">If you want to add a condition to your workflow and a master shape does not exist for it in the stencil, do not create your own shape or import one from a different stencil. Instead, use an existing shape, and then use the **Add Comment** feature of the shape to specify the intended behavior.</span></span>
  
    
    

## <a name="a-compound-condition-cannot-be-manually-added-to-a-workflow-diagram"></a><span data-ttu-id="ef8ca-131">Eine verbundbedingung kann nicht manuell eines Workflowdiagramms hinzugefügt werden</span><span class="sxs-lookup"><span data-stu-id="ef8ca-131">A Compound condition cannot be manually added to a workflow diagram</span></span>
<span data-ttu-id="ef8ca-132"><a name="section4"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-132"></span></span>

<span data-ttu-id="ef8ca-133">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-133">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p108">Eine verbundbedingung kann nicht manuell eines Workflowdiagramms hinzugefügt werden. Die verbundbedingung kann nur beim Importieren des Workflows aus SharePoint Designer generiert werden.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p108">A Compound condition cannot be manually added to a workflow diagram. The compound condition can only be generated when importing workflow from SharePoint Designer.</span></span>
  
    
    
<span data-ttu-id="ef8ca-136">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-136">Example:</span></span>
  
    
    

  
    
    
![Eine Verbundbedingung kann nicht manuell hinzugefügt werden](../images/spd15-wf-error3.JPG)
  
    
    
<span data-ttu-id="ef8ca-138">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-138">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p109">Wenn Sie eine Bedingung zu einem Workflow hinzufügen möchten, und ein master-Shape ist nicht in der Schablone dafür vorhanden, nicht erstellen Sie eigener Shape oder importieren Sie eine aus einer anderen Schablone. Verwenden Sie stattdessen einer vorhandenen Form, und klicken Sie dann verwenden Sie das **Hinzufügen eines Kommentars** Feature der Form, um das beabsichtigte Verhalten anzugeben.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p109">If you want to add a condition to your workflow and a master shape does not exist for it in the stencil, do not create your own shape or import one from a different stencil. Instead, use an existing shape, and then use the **Add a Comment** feature of the shape to specify the intended behavior.</span></span>
  
    
    

## <a name="duplicate-connections-exist-between-workflow-shapes"></a><span data-ttu-id="ef8ca-141">Zwischen Workflow-Shapes bestehen doppelte Verbindungen</span><span class="sxs-lookup"><span data-stu-id="ef8ca-141">Duplicate connections exist between workflow shapes</span></span>
<span data-ttu-id="ef8ca-142"><a name="section5"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-142"></span></span>

<span data-ttu-id="ef8ca-143">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-143">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-144">Zwischen Workflow-Shapes bestehen doppelte Verbindungen.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-144">Duplicate connections exist between workflow shapes.</span></span>
  
    
    
<span data-ttu-id="ef8ca-145">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-145">Example:</span></span>
  
    
    

  
    
    
![Zwischen Shapes bestehen doppelte Verbindungen](../images/spd15-wf-error4.JPG)
  
    
    
<span data-ttu-id="ef8ca-147">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-147">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-148">Entfernen Sie den redundanten Connector, indem markieren und löschen.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-148">Remove the redundant connector by selecting and deleting it.</span></span>
  
    
    

## <a name="loop-back-to-parent-shape-is-not-allowed"></a><span data-ttu-id="ef8ca-149">Ein Zurückschleifen zum übergeordneten Shape ist nicht zulässig</span><span class="sxs-lookup"><span data-stu-id="ef8ca-149">Loop back to parent shape is not allowed</span></span>
<span data-ttu-id="ef8ca-150"><a name="section6"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-150"></span></span>

<span data-ttu-id="ef8ca-151">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-151">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-152">Ein Zurückschleifen zum übergeordneten Shape ist nicht zulässig</span><span class="sxs-lookup"><span data-stu-id="ef8ca-152">Loop back to parent shape is not allowed.</span></span>
  
    
    
<span data-ttu-id="ef8ca-153">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-153">Example:</span></span>
  
    
    

  
    
    
![Ein Zurückschleifen zum übergeordneten Shape ist nicht zulässig](../images/spd15-wf-error5.JPG)
  
    
    
<span data-ttu-id="ef8ca-155">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-155">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p110">Weder Visio Professional 2013 noch SharePoint Designer 2013 unterstützt Workflows mit Schleifen. Überprüfen Sie den Workflow für Schleifen und löschen Sie die Schleifen Verbindungen. Wenn Sie einen SharePoint-Workflow erstellen, der eine Reihe von Schritten Schleife enthält möchten, müssen Sie den Workflow in Visual Studio erstellen.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p110">Neither Visio Professional 2013 nor SharePoint Designer 2013 supports workflows with loops. Check your workflow for loops, and delete the looping connections. If you want to create a SharePoint workflow that includes a set of looping steps, you must create the workflow in Visual Studio.</span></span>
  
    
    

## <a name="parallel-activities-that-are-also-sequential-are-not-allowed"></a><span data-ttu-id="ef8ca-159">Parallele Aktivitäten, die auch sequenziell sind, sind nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-159">Parallel activities that are also sequential are not allowed</span></span>
<span data-ttu-id="ef8ca-160"><a name="section7"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-160"></span></span>

<span data-ttu-id="ef8ca-161">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-161">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-162">Parallele Aktivitäten, die auch sequenziell sind, sind nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-162">Parallel activities that are also sequential are not allowed.</span></span>
  
    
    
<span data-ttu-id="ef8ca-163">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-163">Example:</span></span>
  
    
    

  
    
    
![Parallele Aktivitäten, die auch sequenziell sind](../images/spd15-wf-error6.JPG)
  
    
    
<span data-ttu-id="ef8ca-165">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-165">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p111">Aktivitäten können entweder parallel oder sequenzielle, jedoch nicht beide gleichzeitig sein. Entfernen Sie für parallele Aktivitäten die sequenzielle Connectors. Entfernen Sie die parallele Connectors für sequenzielle Aktivitäten. In einigen Fällen können gleichzeitig parallele und sequenzielle Aktivitäten zum Identifizieren schwierig sein. In den folgenden Beispielen andere allgemeinen Instanzen von parallelen und sequenziellen Anordnung anzeigen und alternative Modalitäten anbieten.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p111">Activities can be either parallel or sequential, but not both simultaneously. For parallel activities, remove the sequential connectors. For sequential activities, remove the parallel connectors. Sometimes, simultaneously parallel and sequential activities can be difficult to identify. The following examples show other common instances of parallel and sequential arrangement and offer alternative arrangements.</span></span>
  
    
    
<span data-ttu-id="ef8ca-171">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-171">Example:</span></span>
  
    
    

  
    
    
![Zeigen auf eine Aktivität von mehreren Pfaden vermeiden](../images/spd15-wf-error7.JPG)
  
    
    
<span data-ttu-id="ef8ca-173">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-173">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-174">Um Connectors, zeigen Sie auf der gleichen Aktivität von mehreren Pfaden zu vermeiden, versuchen Sie die Aktivität:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-174">To avoid having connectors point to the same activity from multiple paths, try duplicating the activity:</span></span>
  
    
    

  
    
    
![Parallele Aktivitäten, die auch sequenziell sind](../images/spd15-wf-error8.JPG)
  
    
    
<span data-ttu-id="ef8ca-176">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-176">Example:</span></span>
  
    
    

  
    
    
![Parallele Aktivitäten, die auch sequenziell sind](../images/spd15-wf-error9.JPG)
  
    
    
<span data-ttu-id="ef8ca-178">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-178">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-179">Wenn Umgang mit paralleler Blöcke in aufeinander folgenden Schritten (in der Regel finden Sie unter erstellt mithilfe von SharePoint Designer-Workflows) versuchen Sie die Form "Kommentar hinzufügen" zwischen zwei parallele Blöcke, damit die Schritte ordnungsgemäß getrennt sind.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-179">If dealing with parallel blocks in sequential steps (usually found in workflows constructed by using SharePoint Designer), try using the "Add a Comment" shape between the two parallel blocks so that the steps are separated cleanly.</span></span>
  
    
    

  
    
    
![Parallele Aktivitäten, die auch sequenziell sind](../images/spd15-wf.JPG)
  
    
    

  
    
    

  
    
    

## <a name="the-condition-shape-does-not-have-connections-labeled-with-yes-or-no"></a><span data-ttu-id="ef8ca-181">Die Form ' Bedingung ' hat keine Verbindung mit der Bezeichnung mit Ja oder Nein</span><span class="sxs-lookup"><span data-stu-id="ef8ca-181">The condition shape does not have connections labeled with Yes or No</span></span>
<span data-ttu-id="ef8ca-182"><a name="section8"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-182"></span></span>

<span data-ttu-id="ef8ca-183">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-183">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-184">Die Form ' Bedingung ' hat keine Verbindung mit der Bezeichnung mit Ja oder Nein.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-184">The condition shape does not have connections labeled with Yes or No.</span></span>
  
    
    
<span data-ttu-id="ef8ca-185">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-185">Example:</span></span>
  
    
    

  
    
    
![Bedingungs-Shape hat keine ja-/nein-Verbindungen](../images/spd15-wf-error11.JPG)
  
    
    
<span data-ttu-id="ef8ca-187">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-187">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-188">Mit der rechten Maustaste in des Connectors zur "Ja" oder "No" Bezeichnung zuweisen.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-188">Right-click the connector to assign a "Yes" or "No" label.</span></span>
  
    
    

## <a name="the-condition-shape-must-have-at-least-one-outgoing-connection-with-label-yes-or-no"></a><span data-ttu-id="ef8ca-189">Die Form ' Bedingung ' muss mindestens eine ausgehende Verbindung mit der Bezeichnung Ja oder Nein haben.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-189">The condition shape must have at least one outgoing connection with label Yes or No</span></span>
<span data-ttu-id="ef8ca-190"><a name="section9"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-190"></span></span>

<span data-ttu-id="ef8ca-191">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-191">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-192">Die Form ' Bedingung ' benötigen Sie mindestens eine ausgehende Verbindung mit der Bezeichnung Ja oder Nein.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-192">The condition shape must have at least one outgoing connection with label Yes or No.</span></span>
  
    
    
<span data-ttu-id="ef8ca-193">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-193">Example:</span></span>
  
    
    

  
    
    
![Bedingungs-Shape muss eine ausgehende Verbindung aufweisen](../images/spd15-wf-error12.JPG)
  
    
    
<span data-ttu-id="ef8ca-195">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-195">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-196">Stellen Sie sicher, dass die Form ' Bedingung ' mindestens einen ausgehenden Connector zu einem anderen Workflow-Shape zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-196">Ensure that the condition shape has at least one outgoing connector attached to another workflow shape.</span></span>
  
    
    

## <a name="the-connector-is-not-a-sharepoint-workflow-connector"></a><span data-ttu-id="ef8ca-197">Der Connector ist keine Verbindung zu SharePoint-Workflow</span><span class="sxs-lookup"><span data-stu-id="ef8ca-197">The connector is not a SharePoint Workflow connector</span></span>
<span data-ttu-id="ef8ca-198"><a name="section10"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-198"></span></span>

<span data-ttu-id="ef8ca-199">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-199">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p112">Der Connector ist keine Verbindung zu SharePoint-Workflow. Stellen Sie sicher, dass der richtige Verbinder mithilfe der Verbinder oder AutoConnect verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p112">The connector is not a SharePoint Workflow connector. Ensure the correct connector is used by using the connector tool or AutoConnect.</span></span>
  
    
    
<span data-ttu-id="ef8ca-202">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-202">Example:</span></span>
  
    
    

  
    
    
![Vergewissern Sie sich, dass der korrekte Verbinder verwendet wird](../images/spd15-wf-error13.JPG)
  
    
    
<span data-ttu-id="ef8ca-204">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-204">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p113">Vermeiden Sie die Connectors aus anderen Diagrammen wiederverwenden, da sie nicht notwendigerweise ausgelegt sind mit SharePoint-Workflows verwendet werden. Löschen Sie den ausgewählten Verbinder, und verwenden Sie die Verbinder oder AutoConnect durch einen neuen Connector zu ersetzen.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p113">Avoid reusing connectors from other diagrams, because they are not necessarily designed to be used with SharePoint workflows. Delete the selected connector, and use the connector tool or AutoConnect to replace it with a new connector.</span></span>
  
    
    

## <a name="the-connector-must-be-connected-to-two-workflow-shapes"></a><span data-ttu-id="ef8ca-207">Der Verbinder muss mit zwei workflowformen verbunden sein</span><span class="sxs-lookup"><span data-stu-id="ef8ca-207">The connector must be connected to two workflow shapes</span></span>
<span data-ttu-id="ef8ca-208"><a name="section11"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-208"></span></span>

<span data-ttu-id="ef8ca-209">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-209">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-210">Der Verbinder muss mit zwei workflowformen verbunden sein.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-210">The connector must be connected to two workflow shapes.</span></span>
  
    
    
<span data-ttu-id="ef8ca-211">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-211">Example:</span></span>
  
    
    

  
    
    
![Verbinder muss mit zwei Workflow-Shapes verbunden sein](../images/spd15-wf-error14.JPG)
  
    
    
<span data-ttu-id="ef8ca-213">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-213">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-214">Entfernen von Sackgasse Connectors oder Anfügen an ein zweites Shape.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-214">Remove dead-end connectors or attach them to a second shape.</span></span>
  
    
    

## <a name="the-diagram-must-only-have-one-workflow-and-one-start-shape"></a><span data-ttu-id="ef8ca-215">Das Diagramm darf nur einen Workflow und ein Anfangs-Shape haben.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-215">The diagram must only have one workflow and one Start shape</span></span>
<span data-ttu-id="ef8ca-216"><a name="section12"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-216"></span></span>

<span data-ttu-id="ef8ca-217">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-217">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-218">Das Diagramm darf nur einen Workflow und ein Anfangs-Shape haben.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-218">The diagram must only have one workflow and one Start shape.</span></span>
  
    
    
<span data-ttu-id="ef8ca-219">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-219">Example:</span></span>
  
    
    

  
    
    
![Diagramm darf nur einen Workflow und einen Anfang haben](../images/spd15-wf-error15.JPG)
  
    
    
<span data-ttu-id="ef8ca-221">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-221">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p114">Alle Pfade müssen vom gleichen **Starten** Shape stammen. Entfernen Sie zusätzliche **Starten** shapes, und ordnen Sie die Connectors, um der Pfad an einem Ort zu starten.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p114">All paths must originate from the same **Start** shape. Remove extra **Start** shapes, and arrange the connectors so that the path starts in one place.</span></span>
  
    
    

## <a name="the-shape-is-not-a-sharepoint-workflow-shape-only-sharepoint-workflow-shapes-can-be-connected-in-a-workflow"></a><span data-ttu-id="ef8ca-p115">Das Shape ist kein SharePoint-Workflow-Shape. In einem Workflow können nur SharePoint-Workflow-Shapes verbunden sein</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p115">The shape is not a SharePoint workflow shape. Only SharePoint workflow shapes can be connected in a workflow</span></span>
<span data-ttu-id="ef8ca-226"><a name="section13"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-226"></span></span>

<span data-ttu-id="ef8ca-227">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-227">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p116">Das Shape ist kein SharePoint-Workflow-Shape. In einem Workflow können nur SharePoint-Workflow-Shapes verbunden werden.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p116">The shape is not a SharePoint workflow shape. Only SharePoint workflow shapes can be connected in a workflow.</span></span>
  
    
    
<span data-ttu-id="ef8ca-230">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-230">Example:</span></span>
  
    
    

  
    
    
![Das Shape ist kein SharePoint-Workflow-Shape](../images/spd15-wf-error16.JPG)
  
    
    
<span data-ttu-id="ef8ca-232">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-232">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p117">In der Microsoft SharePoint-Workflow-Vorlage können nur Workflow-Shapes aus den Schablonen der SharePoint-Workflow verwendet werden. Andere Flussdiagrammshapes werden nicht erkannt, und sie verhindern, dass des Workflows SharePoint Designer 2013 exportiert wird.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p117">Only workflow shapes from the SharePoint workflow stencils can be used in the Microsoft SharePoint Workflow template. Other flowchart shapes are not recognized, and they prevent the workflow from being exported to SharePoint Designer 2013.</span></span>
  
    
    

## <a name="the-start-shape-must-not-have-incoming-connections"></a><span data-ttu-id="ef8ca-235">Das Anfangs-Shape darf keine eingehenden Verbindungen haben</span><span class="sxs-lookup"><span data-stu-id="ef8ca-235">The Start shape must not have incoming connections</span></span>
<span data-ttu-id="ef8ca-236"><a name="section14"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-236"></span></span>

<span data-ttu-id="ef8ca-237">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-237">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-238">Das Anfangs-Shape darf keine eingehenden Verbindungen haben</span><span class="sxs-lookup"><span data-stu-id="ef8ca-238">The Start shape must not have incoming connections.</span></span>
  
    
    
<span data-ttu-id="ef8ca-239">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-239">Example:</span></span>
  
    
    

  
    
    
![Das Anfangs-Shape darf keine eingehenden Verbindungen haben](../images/spd15-wf-error17.JPG)
  
    
    
<span data-ttu-id="ef8ca-241">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-241">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-242">Entfernen Sie den eingehenden Connector mit dem Shape **zu starten**.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-242">Remove the incoming connector to the **Start** shape.</span></span>
  
    
    

## <a name="the-terminate-shape-must-not-have-outgoing-connections"></a><span data-ttu-id="ef8ca-243">Das Abschluss-Shape darf keine ausgehende Verbindungen haben.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-243">The Terminate shape must not have outgoing connections</span></span>
<span data-ttu-id="ef8ca-244"><a name="section15"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-244"></span></span>

<span data-ttu-id="ef8ca-245">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-245">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-246">Das Abschluss-Shape darf keine ausgehende Verbindungen haben.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-246">The Terminate shape must not have outgoing connections.</span></span>
  
    
    
<span data-ttu-id="ef8ca-247">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-247">Example:</span></span>
  
    
    

  
    
    
![Abschluss-Shape darf keine ausgehenden Verbindungen haben](../images/spd15-wf-error18.JPG)
  
    
    
<span data-ttu-id="ef8ca-249">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-249">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-250">Entfernen Sie den ausgehenden Connector vom **Abschluss**-Shape.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-250">Remove the outgoing connector from the **Terminate** shape.</span></span>
  
    
    

## <a name="the-workflow-must-have-a-start-shape"></a><span data-ttu-id="ef8ca-251">Der Workflow muss ein Anfangs-Shape haben</span><span class="sxs-lookup"><span data-stu-id="ef8ca-251">The workflow must have a Start shape</span></span>
<span data-ttu-id="ef8ca-252"><a name="section16"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-252"></span></span>

<span data-ttu-id="ef8ca-253">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-253">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-254">Der Workflow muss ein Anfangs-Shape haben</span><span class="sxs-lookup"><span data-stu-id="ef8ca-254">The workflow must have a Start shape.</span></span>
  
    
    
<span data-ttu-id="ef8ca-255">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-255">Example:</span></span>
  
    
    

  
    
    
![Der Workflow muss ein Anfangs-Shape haben](../images/spd15-wf-error19.JPG)
  
    
    
<span data-ttu-id="ef8ca-257">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-257">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-258">Fügen Sie ein Shape **Starten** an den Anfang des Workflows, und schließen Sie es an die erste Aktivität.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-258">Add a **Start** shape to the beginning of the workflow, and connect it to the first activity.</span></span>
  
    
    

## <a name="the-workflow-shape-is-not-connected-to-a-terminate-shape"></a><span data-ttu-id="ef8ca-259">Das Workflow-Shape ist nicht mit Abschluss-Shape verbunden.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-259">The workflow shape is not connected to a Terminate shape</span></span>
<span data-ttu-id="ef8ca-260"><a name="section17"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-260"></span></span>

<span data-ttu-id="ef8ca-261">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-261">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-262">Das Workflow-Shape ist nicht mit Abschluss-Shape verbunden.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-262">The workflow shape is not connected to a Terminate shape.</span></span>
  
    
    
<span data-ttu-id="ef8ca-263">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-263">Example:</span></span>
  
    
    

  
    
    
![Workflow-Shape ist mit keinem Abschluss verbunden](../images/spd15-wf-error20.JPG)
  
    
    
<span data-ttu-id="ef8ca-265">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-265">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p118">Wenn der Workflow nicht **Abschluss**-Shape verfügt, fügen Sie einen hinzu, und schließen Sie sie bis zum Ende des Workflows. Wenn ein Workflow-Shape eine Verbindung zu einem anderen Workflow-Shape nicht angezeigt wird (siehe Beispiel), können Sie entfernen oder zu einem anderen Workflow-Shape verbinden.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p118">If the workflow does not have a **Terminate** shape, add one and connect it to the end of the workflow. If a workflow shape is missing a connection to another workflow shape (see example), you can remove it or connect it to another workflow shape.</span></span>
  
    
    

## <a name="the-workflow-shape-is-not-connected-to-the-workflow"></a><span data-ttu-id="ef8ca-268">Das Workflow-Shape ist nicht mit dem Workflow verbunden.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-268">The workflow shape is not connected to the workflow</span></span>
<span data-ttu-id="ef8ca-269"><a name="section18"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-269"></span></span>

<span data-ttu-id="ef8ca-270">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-270">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-271">Das Workflow-Shape ist nicht mit dem Workflow verbunden.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-271">The workflow shape is not connected to the workflow.</span></span>
  
    
    
<span data-ttu-id="ef8ca-272">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-272">Example:</span></span>
  
    
    

  
    
    
![Workflow-Shape ist nicht mit dem Workflow verbunden](../images/spd15-wf-error21.JPG)
  
    
    
<span data-ttu-id="ef8ca-274">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-274">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p119">Wenn das Workflow-Shape erforderlich ist, fügen Sie Connectors So fügen Sie es auf den Workflow Pfad hinzu. Anderenfalls Löschen des Shapes.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p119">If the workflow shape is necessary, add connectors to attach it to the workflow path. Otherwise, delete the shape.</span></span>
  
    
    

## <a name="workflow-nesting-levels-must-not-exceed-a-maximum-of-10"></a><span data-ttu-id="ef8ca-277">Workflow geschachtelte Ebenen darf maximal 10 nicht überschreiten.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-277">Workflow nesting levels must not exceed a maximum of 10</span></span>
<span data-ttu-id="ef8ca-278"><a name="section19"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-278"></span></span>

<span data-ttu-id="ef8ca-279">Meldung:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-279">Message:</span></span>
  
    
    
<span data-ttu-id="ef8ca-280">Workflow geschachtelte Ebenen darf maximal 10 nicht überschreiten.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-280">Workflow nesting levels must not exceed a maximum of 10.</span></span>
  
    
    
<span data-ttu-id="ef8ca-281">Vorgeschlagene Aktion:</span><span class="sxs-lookup"><span data-stu-id="ef8ca-281">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ef8ca-p120">Visio Professional 2013 können maximal 10 Ebenen geschachtelter Workflowaktivitäten erkennen. Neu anordnen Sie, um Komplexität eliminiert Aktivitäten oder den Pfad der Workflow in mehr als eine Verzweigung Aufteilen des Workflows.</span><span class="sxs-lookup"><span data-stu-id="ef8ca-p120">Visio Professional 2013 can recognize a maximum of 10 levels of nested workflow activities. Rearrange the workflow to reduce complexity by eliminating activities or dividing the workflow path into more than one branch.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="ef8ca-284">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="ef8ca-284">Additional resources</span></span>
<span data-ttu-id="ef8ca-285"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ef8ca-285"></span></span>


-  [<span data-ttu-id="ef8ca-286">Neuerungen in Workflows für SharePoint</span><span class="sxs-lookup"><span data-stu-id="ef8ca-286">What's new in workflows for SharePoint</span></span>](what-s-new-in-workflows-for-sharepoint.md)
    
  
-  [<span data-ttu-id="ef8ca-287">Erste Schritte mit Workflows in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ef8ca-287">Get started with workflows in SharePoint</span></span>](get-started-with-workflows-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ef8ca-288">Workflowentwicklung in SharePoint Designer und Visio</span><span class="sxs-lookup"><span data-stu-id="ef8ca-288">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  

  
    
    
