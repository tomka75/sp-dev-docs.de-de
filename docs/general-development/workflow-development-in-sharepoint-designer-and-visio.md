---
title: Workflowentwicklung in SharePoint Designer und Visio
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 496780d5-47d6-4a43-bf14-70aefb8d820c
ms.openlocfilehash: 79d3cf98b6468697d1c1cecbd37ea63017761780
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="workflow-development-in-sharepoint-designer-and-visio"></a><span data-ttu-id="d6fce-102">Workflowentwicklung in SharePoint Designer und Visio</span><span class="sxs-lookup"><span data-stu-id="d6fce-102">Workflow development in SharePoint Designer and Visio</span></span>
<span data-ttu-id="d6fce-103">Hier erfahren Sie, wie Sie mit Visio 2013 und SharePoint Designer 2013 Workflows erstellen und auf einer SharePoint-Website veröffentlichen, ohne dass Sie Code benötigen.</span><span class="sxs-lookup"><span data-stu-id="d6fce-103">Learn to use Visio 2013 and SharePoint Designer 2013 to create and publish workflows to a SharePoint site without needing any code.</span></span>
## <a name="introduction"></a><span data-ttu-id="d6fce-104">Einführung</span><span class="sxs-lookup"><span data-stu-id="d6fce-104">Introduction</span></span>
<span data-ttu-id="d6fce-105"><a name="VSSPD_Intro"> </a></span><span class="sxs-lookup"><span data-stu-id="d6fce-105"><a name="VSSPD_Intro"> </a></span></span>

<span data-ttu-id="d6fce-p101">Visio 2013 und SharePoint Designer 2013 machen es Geschäftsanalysten, Prozessberatern und IT-Experten einfach, zusammenzuarbeiten und -Workflows zu erstellen. Sowohl Visio Professional 2013 als auch der Visual Designer in SharePoint Designer 2013 bieten eine optionale Darstellung von Workflows in einem Format, das für Benutzer mit und ohne Programmierkenntnisse gleichermaßen verständlich ist.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p101">Visio 2013 and SharePoint Designer 2013 make it easy for business analysts, process consultants, and IT professionals to collaborate and build workflows. Both Visio Professional 2013 and the Visual Designer in SharePoint Designer 2013 provide a rich representation of workflows in a format that is understandable to programmers and non-programmers alike.</span></span>
  
> [!NOTE] 
> <span data-ttu-id="d6fce-108">Hinweise zur Einrichtung und Konfiguration von SharePoint und dem Workflow-Manager-Server finden Sie unter [Konfigurieren von Workflows in SharePoint]((http://technet.microsoft.com/de-DE/library/jj658586.aspx)).</span><span class="sxs-lookup"><span data-stu-id="d6fce-108">[Note:]((http://technet.microsoft.com/de-DE/library/jj658586.aspx)) For guidance on setting up and configuring SharePoint and the Workflow Manager server, see  Configure workflow in SharePoint.</span></span> 
  
    
    

<span data-ttu-id="d6fce-p102">Mithilfe von Visio 2013 können Sie einen SharePoint-Workflow visuell erstellen, den Workflow nach SharePoint Designer 2013 exportieren und diesen Workflow dann auf einer SharePoint-Website veröffentlichen. Nachdem ein Workflow in Visio 2013 erstellt wurde, muss er nach SharePoint Designer 2013 exportiert werden. Dann fügt ein SharePoint-Websiteeigentümer oder IT-Experte dem Workflow Parameter hinzu. Er verwendet dazu entweder den Workflow-Text-Editor oder den neuen Visual Workflow Designer. Dabei handelt es sich um ein Visio 2013-ActiveX-Steuerelement, das in SharePoint Designer 2013 gehostet wird. Nachdem der Workflow abgeschlossen wurde, kann er auf der SharePoint-Website veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p102">By using Visio 2013, you can visually create a SharePoint workflow, export the workflow to SharePoint Designer 2013, and then publish that workflow to a SharePoint site. After a workflow has been created in Visio 2013, it must be exported to SharePoint Designer 2013. Then, a SharePoint site owner or IT professional adds parameters to the workflow by using either the workflow text editor or the new Visual Workflow Designer, which is a Visio 2013 ActiveX control that is hosted in SharePoint Designer 2013. After the workflow has been completed, it can be published to the SharePoint site.</span></span>
  
    
    
<span data-ttu-id="d6fce-p103">Dies ist ideal für Geschäftsanalysten und Prozessberater, die bereits mit Flussdiagrammen in Visio vertraut sind, da sie einen Workflow entwerfen können, der Geschäftslogik darstellt. Die Person, die den Workflow entwirft, kann sich voll und ganz auf die BI-spezifischen (Business Intelligence) Anforderungen des Workflows konzentrieren, ohne ein Experte für deklarative Workflows sein zu müssen.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p103">This is ideal for business analysts and process consultants who are already familiar with flowcharts in Visio, because it allows them to design a workflow that represents business logic. The person who designs the workflow can focus solely on the business intelligence (BI) needs of the workflow without needing to be an expert in declarative workflows.</span></span>
  
    
    

## <a name="about-creating-sharepoint-workflows-in-visio-2013-and-sharepoint-designer-2013"></a><span data-ttu-id="d6fce-115">Info zur Erstellung von SharePoint-Workflows in Visio 2013 und SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="d6fce-115">About creating SharePoint Workflows in Visio 2013 and SharePoint Designer 2013</span></span>
<span data-ttu-id="d6fce-116"><a name="VSSPD_About"> </a></span><span class="sxs-lookup"><span data-stu-id="d6fce-116"><a name="VSSPD_About"> </a></span></span>

<span data-ttu-id="d6fce-p104">Visio 2013 enthält eine SharePoint-Workflowvorlage, die zur Erstellung von SharePoint-Workflows verwendet werden kann. Die SharePoint-Workflowvorlage ist mit drei Vorlagen verknüpft: SharePoint-Workflowaktionen, SharePoint--Workflowbedingungen und SharePoint-Workflow-Abschlusszeichen. Die Shapes in diesen Schablonen entsprechen den spezifischen Aktionen und Bedingungen, die in einem SharePoint-Workflow verwendet werden können. Zur Erstellung eines Workflows müssen Sie nur Shapes in den Zeichenbereich in Visio 2013 ziehen, um die Geschäftslogik hinter dem Workflow zu modellieren.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p104">Visio 2013 includes a SharePoint Workflow template that can be used to build SharePoint workflows. The SharePoint Workflow template is associated with three stencils: SharePoint Workflow Actions, SharePoint Workflow Conditions, and SharePoint Workflow Terminators. The shapes in these stencils correspond to specific actions and conditions that can be used within a SharePoint workflow. To build a workflow, you need only to drag shapes onto the drawing canvas in Visio 2013 to model the business logic behind the workflow.</span></span>
  
    
    

### <a name="stages-loops-and-steps"></a><span data-ttu-id="d6fce-121">Phasen, Schleifen und Schritte</span><span class="sxs-lookup"><span data-stu-id="d6fce-121">Stages, loops, and steps</span></span>

<span data-ttu-id="d6fce-p105">Bei Workflows in SharePoint Designer 2013 werden jetzt die Begriffe Phasen, Schleifen undSchritte verwendet. Workflowautoren können eine Reihe einzelner Aktionen und Bedingungen als einzelne Einheit gruppieren, um den Prozess klarer zu definieren. So könnte es z. B. eine Phase oder einen Schritt für die Genehmigung oder die Anforderung von Feedback geben. Diese Phase oder dieser Schritt würde alle Aktionen umfassen, die für diesen Prozess relevant sind. Die Phase oder der Schritt selbst kann ein Knoten eines längeren Workflows sein und würde einem Benutzer erlauben, anstatt einer Reihe einzelner Aktionen den Status dieser Phase als Ganzes anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p105">Workflows in SharePoint Designer 2013 now include the notions of stages, loops, and steps. Workflow authors can group a number of individual actions and conditions as a single unit to more clearly define the process. For example, there could be an Approval or Request Feedback stage or step. Within that stage or step would be all of the actions that are necessary for that process. The stage or step itself might be one node of a longer workflow and would allow a viewer to see the status of that stage as a whole, rather than a set of individual actions.</span></span>
  
    
    
<span data-ttu-id="d6fce-127">Die SharePoint-Workflowvorlage, die in Visio 2013 enthalten ist, verwendet ebenfalls Phasen, Schleifen und Schritte als logische Bausteine zur Erstellung eines Workflows.</span><span class="sxs-lookup"><span data-stu-id="d6fce-127">The SharePoint Workflow template that is included in Visio 2013 also uses stages, loops, and steps as logical building blocks for creating a workflow.</span></span> 
  
    
    

> <span data-ttu-id="d6fce-128">**Wichtig:** Aufgrund der Unterschiede zwischen der Microsoft SharePoint 2010-Workflowvorlage und der SharePoint-Workflowvorlage können Sie keine Shapes aus einer Vorlage in ein Diagramm verwenden, das von der anderen erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="d6fce-128">**Important:** Because of the underlying differences between the Microsoft SharePoint 2010 Workflow template and the SharePoint Workflow template, you cannot use shapes from one template within a diagram created by the other.</span></span> <span data-ttu-id="d6fce-129">Nur Shapes aus den SharePoint-Workflowaktionen, SharePoint-Workflowbedingungen und SharePoint-Workflow-Abschlusszeichen-Schablonen können verwendet werden, um einen SharePoint-Workflow zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d6fce-129">Only shapes from the SharePoint Workflow Actions, SharePoint Workflow Conditions, and SharePoint Workflow Terminators stencils can be used to build a SharePoint workflow.</span></span> 
  
    
    


### <a name="stage-shapes"></a><span data-ttu-id="d6fce-130">Phasen-Shapes</span><span class="sxs-lookup"><span data-stu-id="d6fce-130">Stage shapes</span></span>

<span data-ttu-id="d6fce-p107">Eine Phase kann eine Reihe von Shapes und möglicherweise Verzweigungen enthalten. Allerdings kann es nur einen Pfad in eine Phase (und einen Schritt) und einen Pfad heraus geben. Alle Aktionen im Workflow müssen in einer Phase enthalten sein. Phasen-Shapes werden mithilfe von Container-Shapes visuell dargestellt. Bei einem Phasen-Shape müssen an den Rändern des Containers ein Eingangs- und Ausgangs-Shape hinzugefügt werden, um die Pfade zur und aus der Phase zu definieren. Visio 2013 und der Visual Designer in SharePoint Designer 2013 fügen die Eingangs- und Ausgangs-Shapes für Sie hinzu, wenn Sie den Container zum ersten Mal ablegen.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p107">A stage can contain any number of shapes and may include branching. However, there can be only one path into a stage (and a step) and one path out. All actions in the workflow must be contained by a stage. Stage shapes are visualized by using container shapes. A Stage shape requires that an Enter and an Exit shape be added to the edges of the container to define the paths in and out of the stage. Visio 2013 and the Visual Designer in SharePoint Designer 2013 add the Enter and Exit shapes for you when you first drop the container.</span></span>
  
    
    
<span data-ttu-id="d6fce-136">Für Phasen gelten außerdem die folgenden Regeln:</span><span class="sxs-lookup"><span data-stu-id="d6fce-136">Stages also have the following rules:</span></span>
  
    
    

- <span data-ttu-id="d6fce-p108">Alle Diagramme müssen mindestens eine Phase aufweisen. Eine vollständige Phase mit Eingangs-, Ausgangs- und Start-Shapes ist als Teil einer SharePoint-Standardworkflowvorlage vorhanden.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p108">All diagrams must have at least one stage. A stage, complete with Enter, Exit, and Start shapes are present as part of the default SharePoint Workflow template.</span></span>
    
  
- <span data-ttu-id="d6fce-139">Wenn Sie dem Zeichenbereich eine neue Phase hinzufügen, fügt Visio 2013 Start- und Ende-Konnektoren hinzu, wenn die Phase abgelegt wird.</span><span class="sxs-lookup"><span data-stu-id="d6fce-139">When you add a new stage to the drawing canvas, Visio 2013 will add Start and End connectors when the stage is dropped.</span></span>
    
  
- <span data-ttu-id="d6fce-140">Bei Phasen können Konnektoren nur über die Eingangs- und Ausgangs-Shapes eingehen oder ausgehen.</span><span class="sxs-lookup"><span data-stu-id="d6fce-140">Stages cannot have any connectors coming in or going out other than through the Enter and Exit shapes.</span></span>
    
  
- <span data-ttu-id="d6fce-p109">Phasen-Container können nicht verschachtelt werden. Wenn Sie einen anderen Unterprozess innerhalb einer Phase vernesteln möchten, verwenden Sie einen Schritt.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p109">Stage containers cannot be nested. If you want to nest another sub-process within a stage, use a step.</span></span>
    
  
- <span data-ttu-id="d6fce-143">Eine Phase kann Workflow-stoppen-Shapes enthalten.</span><span class="sxs-lookup"><span data-stu-id="d6fce-143">Stop Workflow shapes may exist within a stage.</span></span>
    
  
- <span data-ttu-id="d6fce-p110">Für das gesamte Diagramm ist außerhalb der Phase ein explizites Start-Shape erforderlich. Ein explizites Terminieren-Shape ist außerhalb der Phase nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p110">An explicit Start shape is required outside of the stage for the entire diagram. An explicit Terminate shape outside of the stage is not required.</span></span>
    
  
- <span data-ttu-id="d6fce-p111">Auf der obersten Ebene kann der Workflow nur Phasen, bedingte Shapes und Start- und Terminieren-Shapes enthalten. Alle anderen Shapes müssen in einer Phase enthalten sein.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p111">At the top level, the workflow can contain only stages, conditional shapes, and Start and Terminate terminators. All other shapes must be contained within a stage.</span></span>
    
  

### <a name="loop-shapes"></a><span data-ttu-id="d6fce-148">Schleifen-Shapes</span><span class="sxs-lookup"><span data-stu-id="d6fce-148">Loop shapes</span></span>

<span data-ttu-id="d6fce-149">Schleifen sind eine Reihe verbundener Shapes, die als Schleife ausgeführt werden, wobei so lange vom letzten Shape in der Reihe zum ersten Shape iteriert wird, bis eine Bedingung erfüllt ist.</span><span class="sxs-lookup"><span data-stu-id="d6fce-149">Loops are a series of connected shapes that will execute as a loop, returning from the last shape in the series to the first, until a condition is satisfied.</span></span> 
  
    
    
<span data-ttu-id="d6fce-p112">Wie Phasen werden Schleifen durch ein Container-Shape dargestellt, das ein Eingangs- und Ausgangs-Shape enthält (wird hinzugefügt, wenn das Shape im Zeichenbereich abgelegt wird). Auch bei einem Schleifen-Shape müssen an den Rändern des Containers ein Eingangs- und Ausgangs-Shape hinzugefügt werden, um die Pfade in die und aus der Schleife zu definieren.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p112">Like stages, loops are represented by a container shape that includes an Enter and Exit shape (added when the shape is dropped on the drawing canvas). A Loop shape also requires that an Enter and Exit shape be added to the edges of the container to define the paths in and out of the loop.</span></span>
  
    
    
<span data-ttu-id="d6fce-152">Visio 2013 und SharePoint Designer 2013 unterstützen zwei Arten von Schleifen: Schleife  *n*  -mal ausführen und Schleife ausführen, bis *Wert1*  *Wert2*  entspricht.</span><span class="sxs-lookup"><span data-stu-id="d6fce-152">Visio 2013 and SharePoint Designer 2013 support two types of loops: loop  *n*  times and loop until *value1*  equals *value2*  .</span></span>
  
    
    
<span data-ttu-id="d6fce-153">Für Schleifen gelten außerdem die folgenden Regeln:</span><span class="sxs-lookup"><span data-stu-id="d6fce-153">Loops must also conform to the following rules:</span></span>
  
    
    

- <span data-ttu-id="d6fce-154">Schleifen müssen sich innerhalb einer Phase befinden, und Phasen können sich nicht in einer Schleife befinden.</span><span class="sxs-lookup"><span data-stu-id="d6fce-154">Loops must be within a stage, and stages cannot be within a loop.</span></span>
    
  
- <span data-ttu-id="d6fce-155">Eine Schleife kann Schritte enthalten.</span><span class="sxs-lookup"><span data-stu-id="d6fce-155">Steps may be within a loop.</span></span>
    
  
- <span data-ttu-id="d6fce-156">Schleifen dürfen nur einen Eingangs- und einen Ausgangspunkt aufweisen.</span><span class="sxs-lookup"><span data-stu-id="d6fce-156">Loops may have only one entry and one exit point.</span></span>
    
  

### <a name="step-shapes"></a><span data-ttu-id="d6fce-157">Schritt-Shapes</span><span class="sxs-lookup"><span data-stu-id="d6fce-157">Step shapes</span></span>

<span data-ttu-id="d6fce-p113">Schritte stellen eine gruppierte Reihe aufeinanderfolgender Aktionen dar. Schritte müssen in einer Phase enthalten sein. Ein Schritt-Shape muss auch ein Eingangs- und Ausgangs-Shape aufweisen, um die Pfade in das und aus dem Shape zu definieren. Beide Shapes werden standardmäßig hinzugefügt, wenn das Shape im Zeichenbereich abgelegt wird.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p113">Steps represent a grouped series of sequential actions. Steps must be contained by a stage. A step shape must also have an Enter and Exit shape to define the paths in and out of the shape. Both shapes are added by default when the shape is dropped onto the canvas.</span></span>
  
    
    

## <a name="creating-a-workflow-in-visio-2013"></a><span data-ttu-id="d6fce-162">Erstellen eines Workflows in Visio 2013</span><span class="sxs-lookup"><span data-stu-id="d6fce-162">Creating a workflow in Visio 2013</span></span>
<span data-ttu-id="d6fce-163"><a name="VSSPD_Creating"> </a></span><span class="sxs-lookup"><span data-stu-id="d6fce-163"><a name="VSSPD_Creating"> </a></span></span>

<span data-ttu-id="d6fce-p114">Alle Master-Shapes in den SharePoint-Workflowschablonen entsprechen den Aktionen, Bedingungen und anderen logischen Konstrukten innerhalb eines SharePoint-Workflows. Zur Erstellung eines Workflows können Sie Shapes, wie in jedem anderen Flussdiagramm in Visio, in den Zeichenbereich ziehen. Wenn Sie mit der Erstellung des Workflows in Visio 2013 fertig sind, speichern Sie den Workflow, bevor SharePoint Designer 2013 ihn öffnen kann.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p114">All of the master shapes in the SharePoint Workflow stencils correspond to actions, conditions, and other logical constructs within a SharePoint workflow. To build a workflow, you can drag shapes onto the drawing canvas, just like any other flowchart in Visio. After you have finished building the workflow in Visio 2013, save the workflow before SharePoint Designer 2013 can open it.</span></span>
  
    
    
<span data-ttu-id="d6fce-167">Gehen Sie folgendermaßen vor, um die SharePoint-Workflowvorlage in Visio 2013 zu öffnen:</span><span class="sxs-lookup"><span data-stu-id="d6fce-167">To open the SharePoint Workflow template in Visio 2013, do the following:</span></span>
  
    
    

### <a name="to-open-the-sharepoint-workflow-template-in-visio-2013"></a><span data-ttu-id="d6fce-168">So öffnen Sie die SharePoint-Workflowvorlage in Visio 2013</span><span class="sxs-lookup"><span data-stu-id="d6fce-168">To open the SharePoint Workflow template in Visio 2013</span></span>


1. <span data-ttu-id="d6fce-169">Öffnen Sie Visio 2013.</span><span class="sxs-lookup"><span data-stu-id="d6fce-169">Open Visio 2013.</span></span>
    
  
2. <span data-ttu-id="d6fce-170">Wählen Sie **Neu** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-170">Choose **New**.</span></span>
    
  
3. <span data-ttu-id="d6fce-171">Wählen Sie unter **Vorlagenkategorien** **Flussdiagramm** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-171">Under **Template Categories**, choose **Flowchart**.</span></span>
    
  
4. <span data-ttu-id="d6fce-172">Wählen Sie unter **Vorlage auswählen** **SharePoint Workflow** und dann **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-172">Under **Choose a Template**, choose **SharePoint Workflow** and then choose **Create**.</span></span>
    
    <span data-ttu-id="d6fce-p115">Die Vorlage wird geöffnet, und der Zeichenbereich wird mit Start- und Phasen-Shapes aufgefüllt. Das Phasen-Shape enthält ein Eingangs- und Ausgangs-Shape, verbunden durch einen einzelnen Konnektor.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p115">The template opens and the drawing canvas is prepopulated with Start, and Stage shapes. The Stage shape contains an Enter and an Exit shape, joined by a single connector.</span></span>
    
  
<span data-ttu-id="d6fce-p116">Ziehen Sie, während die SharePoint-Workflowvorlage geöffnet ist, Aktionen, Bedingungen und andere Shapes in den Zeichenbereich, um einen Workflow zu entwerfen. Weitere Informationen zu einzelnen Shapes und deren Bedeutung finden Sie im Artikel  [Shapes in der SharePoint Server-Workflowvorlage in Visio](shapes-in-the-sharepoint-server-workflow-template-in-visio.md).</span><span class="sxs-lookup"><span data-stu-id="d6fce-p116">With the SharePoint Workflow template open, drag actions, conditions, and other shapes onto the drawing canvas to design a workflow. For more information about individual shapes and what they mean, see the article  [Shapes in the SharePoint Server workflow template in Visio](shapes-in-the-sharepoint-server-workflow-template-in-visio.md).</span></span>
  
    
    

> <span data-ttu-id="d6fce-177">**Tipp:** Berücksichtigen Sie beim Entwerfen eines Workflows zusätzlich Folgendes:</span><span class="sxs-lookup"><span data-stu-id="d6fce-177">**Tip:** When designing a workflow, keep the following additional considerations in mind:</span></span>
>  - <span data-ttu-id="d6fce-178">Um schnell einen Workflow zu erstellen, legen Sie Aktions- und Bedingungs-Shapes auf den internen Konnektor, der in neuen Phasen-Shapes enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="d6fce-178">To quickly build a workflow, drop action and condition shapes onto the internal connector that is contained by new stage shapes.</span></span> <span data-ttu-id="d6fce-179">Visio 2013 teilt den Konnektor automatisch in weitere Konnektoren, sodass der Workflow vom Eingangs- bis zum Ausgangs-Shape verbunden ist.</span><span class="sxs-lookup"><span data-stu-id="d6fce-179">Visio 2013 automatically splits the connector into additional connectors, keeping the workflow connected from the Enter shape to the Exit shape.</span></span>
>  - <span data-ttu-id="d6fce-180">Verwenden Sie nur Shapes aus den SharePoint-Workflowaktionen, SharePoint-Workflowbedingungen und SharePoint-Workflow-Abschlusszeichen-Schablonen.</span><span class="sxs-lookup"><span data-stu-id="d6fce-180">Do not use any shapes from a stencil other than the SharePoint Workflow Actions, SharePoint Workflow Conditions, and SharePoint Workflow Terminators stencils.</span></span> <span data-ttu-id="d6fce-181">Verwenden Sie nur das von der SharePoint-Workflowvorlage bereitgestellte Konnektortool, um Verbindungen zwischen Shapes hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="d6fce-181">Use only the Connector tool provided by the SharePoint Workflow template to add connections between shapes.</span></span> <span data-ttu-id="d6fce-182">Alle anderen Konnektor-Shapes sind in einem SharePoint-Workflow ungültig.</span><span class="sxs-lookup"><span data-stu-id="d6fce-182">All other connector shapes are not valid within a SharePoint workflow.</span></span>
>  - <span data-ttu-id="d6fce-p119">Aktions-Shapes, Schritte und Schleifen müssen immer in einem Phase-Shape enthalten sein. Einige bedingte Shapes können sich außerhalb einer Phase befinden.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p119">Action shapes, steps, and loops must always be contained within a Stage shape. Some conditional shapes can be outside of a stage.</span></span>
>  - <span data-ttu-id="d6fce-p120">Ein Phasen-Shape muss genau ein Eingangs-Shape und ein Ausgangs-Shape aufweisen. Der in der Phase enthaltene Unterprozess des Workflows muss mit dem Eingangs-Shape beginnen und mit dem Ausgangs-Shape enden.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p120">A Stage shape must have exactly one Enter shape and one Exit shape. The workflow sub-process that is contained within the stage must start with the Enter shape and end with the Exit shape.</span></span>
>  - <span data-ttu-id="d6fce-187">Ein Bedingungs-Shape muss zwei ausgehende Konnektoren aufweisen, einen mit der Bezeichnung "Ja" und den anderen mit der Bezeichnung "Nein".</span><span class="sxs-lookup"><span data-stu-id="d6fce-187">A condition shape must have two connectors leaving the shape, one labeled "Yes" and the other labeled "No."</span></span> <span data-ttu-id="d6fce-188">Sie können mit der rechten Maustaste auf einen Konnektor klicken und **Ja** oder **Nein** auswählen.</span><span class="sxs-lookup"><span data-stu-id="d6fce-188">You can right-click a connector to choose **Yes** or **No**.</span></span> 
>  - <span data-ttu-id="d6fce-p122">Ein Workflow muss nur ein Anfangs-Shape haben. Das Anfangs-Shape muss sich außerhalb eine Phase befinden.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p122">A workflow must have only one Start shape. The Start shape must be outside of a stage.</span></span>
>  - <span data-ttu-id="d6fce-191">Sie fügen im Workflow Text zu Shapes hinzu, aber der Shape-Text hat keinen Einfluss auf den Workflow.</span><span class="sxs-lookup"><span data-stu-id="d6fce-191">You add text to shapes in the workflow, but the shape text will not affect the workflow.</span></span>
  
    
    


  
    
    
<span data-ttu-id="d6fce-p123">Die Überprüfung des Workflows in Visio 2013 erfolgt wie bei jedem anderen verbundenen Diagramm: Visio prüft das Diagramm anhand einer Reihe von Regeln und gibt eine Liste mit Fehlern zurück, die im Diagramm gefunden wurden. Informationen dazu, wie Sie Validierungsprobleme beheben, finden Sie im Artikel  [Beheben von SharePoint Server 2013-Workflowvalidierungsfehlern in Visio 2013](troubleshooting-sharepoint-server-workflow-validation-errors-in-visio.md).</span><span class="sxs-lookup"><span data-stu-id="d6fce-p123">Validating the workflow in Visio 2013 is like validating any other connected diagram: Visio checks the diagram against a set of rules and returns a list of errors that it found in the diagram. See the article  [Troubleshooting SharePoint Server workflow validation errors in Visio](troubleshooting-sharepoint-server-workflow-validation-errors-in-visio.md) to learn how to resolve validation issues.</span></span>
  
    
    

### <a name="to-validate-a-sharepoint-workflow-in-visio-2013"></a><span data-ttu-id="d6fce-194">So überprüfen Sie einen SharePoint-Workflow in Visio 2013</span><span class="sxs-lookup"><span data-stu-id="d6fce-194">To validate a SharePoint workflow in Visio 2013</span></span>


1. <span data-ttu-id="d6fce-195">Wählen Sie auf der Registerkarte **Prozess** in der Gruppe **Diagrammüberprüfung** **Diagramm überprüfen** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-195">On the **Process** tab, in the **Diagram Validation** group, choose **Check Diagram**.</span></span>
    
  
2. <span data-ttu-id="d6fce-p124">Wenn im Workflow Fehler gefunden werden, wird unter dem Diagramm der Bereich **Probleme** geöffnet. Wählen Sie in der Liste jedes Element aus, um das Shape im Diagramm auszuwählen, das den Fehler verursacht hat.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p124">If any errors are found in the workflow, the **Issues** pane opens below the diagram. Choose each item in the list to select the shape in the diagram that caused the error.</span></span>
    
  
3. <span data-ttu-id="d6fce-p125">Beheben Sie jeden in der Liste **Probleme** aufgeführten Validierungsfehler. Nachdem alle Fehler behoben wurden, wählen Sie erneut **Diagramm überprüfen** aus. Weitere Informationen dazu, wie Sie Validierungsprobleme in Visio 2013 beheben, finden Sie im Artikel [Beheben von SharePoint Server 2013-Workflowvalidierungsfehlern in Visio 2013](troubleshooting-sharepoint-server-workflow-validation-errors-in-visio.md).</span><span class="sxs-lookup"><span data-stu-id="d6fce-p125">Resolve each validation error listed in the **Issues** list. Once all of the errors have been addressed, choose **Check Diagram** again. For more information about how to resolve validation issues in Visio 2013, see the article [Troubleshooting SharePoint Server workflow validation errors in Visio](troubleshooting-sharepoint-server-workflow-validation-errors-in-visio.md).</span></span>
    
  
4. <span data-ttu-id="d6fce-201">Werden im Workflow keine Fehler gefunden, zeigt Visio die Meldung an, dass die Diagrammüberprüfung abgeschlossen wurde und keine Fehler gefunden wurden.</span><span class="sxs-lookup"><span data-stu-id="d6fce-201">If no errors are found in the workflow, Visio displays a message stating that the diagram validation is complete and that no issues were found.</span></span>
    
  
<span data-ttu-id="d6fce-p126">Nachdem der Workflow in Visio 2013 erfolgreich überprüft wurde, können Sie die Datei speichern und in SharePoint Designer 2013 importieren. Im Gegensatz zur Microsoft SharePoint 2010-Workflowvorlage können Sie eine Kopie des SharePoint-Workflowdiagramms unter dem Visio 2013-Standarddateiformat (.vsdx) speichern, und SharePoint Designer 2013 kann die Datei öffnen.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p126">After the workflow has been successfully validated in Visio 2013, you can save the file and import it into SharePoint Designer 2013. Unlike the Microsoft SharePoint 2010 Workflow template, you can save a copy of the SharePoint Workflow diagram as the default Visio 2013 file format (.vsdx) and SharePoint Designer 2013 can open the file.</span></span> 
  
    
    
<span data-ttu-id="d6fce-204">Verwenden Sie das folgende Verfahren, um einen SharePoint-Workflow in Visio 2013 als Visio 2013-.vsdx-Datei zu speichern, die in SharePoint Designer 2013 geöffnet werden kann:</span><span class="sxs-lookup"><span data-stu-id="d6fce-204">Use the following procedure to save a SharePoint workflow in Visio 2013 as a Visio 2013 .vsdx file that can be opened in SharePoint Designer 2013:</span></span>
  
    
    

### <a name="to-save-a-workflow-in-visio-2013"></a><span data-ttu-id="d6fce-205">So speichern Sie einen Workflow in Visio 2013</span><span class="sxs-lookup"><span data-stu-id="d6fce-205">To save a workflow in Visio 2013</span></span>


1. <span data-ttu-id="d6fce-206">Wählen Sie **Datei** und dann **Speichern unter** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-206">Choose **File**, and then choose **Save As**.</span></span>
    
  
2. <span data-ttu-id="d6fce-207">Wählen Sie unter **Speichern unter** **Speichern** und dann **Navigieren** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-207">Under **Save As**, choose **Save**, and then choose **Browse**.</span></span>
    
  
3. <span data-ttu-id="d6fce-208">Wählen Sie im Dialogfeld **Speichern unter** einen Speicherort aus, um die Datei zu speichern, und geben Sie einen Namen für die Datei ein ("Mein SP-Workflow").</span><span class="sxs-lookup"><span data-stu-id="d6fce-208">In the **Save As** dialog box, select a location to save the file and type a name for the file ("My SP Workflow").</span></span>
    
  
4. <span data-ttu-id="d6fce-209">Wählen Sie **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-209">Choose **Save**.</span></span>
    
  

## <a name="customizing-and-publishing-a-workflow-in-sharepoint-designer-2013"></a><span data-ttu-id="d6fce-210">Anpassen und Veröffentlichen eines Workflows in SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="d6fce-210">Customizing and publishing a workflow in SharePoint Designer 2013</span></span>
<span data-ttu-id="d6fce-211"><a name="VSSPD_Customizing"> </a></span><span class="sxs-lookup"><span data-stu-id="d6fce-211"><a name="VSSPD_Customizing"> </a></span></span>

<span data-ttu-id="d6fce-p127">Nachdem Sie die zugrunde liegende Geschäftslogik für einen SharePoint-Workflow in Visio 2013 erstellt und das Diagramm gespeichert haben, können Sie die Visio-.vsdx-Datei in SharePoint Designer 2013 öffnen und damit beginnen, den Workflow an Ihre SharePoint-Website anzupassen. Das .vsdx-Dateipaket enthält XML-Dokumente, die SharePoint Designer 2013 in Workflows übersetzen kann.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p127">Once you have created the underlying business logic for a SharePoint workflow in Visio 2013 and saved the diagram, you can open the Visio .vsdx file in SharePoint Designer 2013 and begin tailoring the workflow to your SharePoint site. The .vsdx file package contains XML documents that SharePoint Designer 2013 can translate into workflows.</span></span>
  
    
    
<span data-ttu-id="d6fce-214">Verwenden Sie das folgende Verfahren, um eine SharePoint-Website in SharePoint Designer 2013 zu öffnen:</span><span class="sxs-lookup"><span data-stu-id="d6fce-214">Use the following procedure to open a SharePoint site in SharePoint Designer 2013:</span></span>
  
    
    

### <a name="to-open-a-sharepoint-site-in-sharepoint-designer-2013"></a><span data-ttu-id="d6fce-215">So öffnen Sie eine SharePoint-Website in SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="d6fce-215">To open a SharePoint site in SharePoint Designer 2013</span></span>


1. <span data-ttu-id="d6fce-216">Öffnen Sie SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="d6fce-216">Open SharePoint Designer 2013.</span></span>
    
  
2. <span data-ttu-id="d6fce-217">Wählen Sie unter **SharePoint-Website öffnen** **Website öffnen** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-217">Under **Open SharePoint Site**, choose **Open Site**.</span></span>
    
  
3. <span data-ttu-id="d6fce-218">Wählen Sie im Dialogfeld **Website öffnen** die Website aus, die Sie öffnen möchten.</span><span class="sxs-lookup"><span data-stu-id="d6fce-218">In the **Open Site** dialog box, select the site that you want to open.</span></span>
    
  
4. <span data-ttu-id="d6fce-219">Wählen Sie **Öffnen** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-219">Choose **Open**.</span></span>
    
  
<span data-ttu-id="d6fce-220">Nachdem die SharePoint-Website geöffnet wurde, können Sie das Visio 2013-.vsdx-Diagramm in SharePoint Designer 2013 öffnen.</span><span class="sxs-lookup"><span data-stu-id="d6fce-220">Once the SharePoint site is open, you can open the Visio 2013 .vsdx diagram within SharePoint Designer 2013.</span></span>
  
    
    

### <a name="to-open-a-visio-professional-2013-workflow-in-sharepoint-designer-2013"></a><span data-ttu-id="d6fce-221">So öffnen Sie einen Visio Professional 2013-Workflow in SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="d6fce-221">To open a Visio Professional 2013 workflow in SharePoint Designer 2013</span></span>


1. <span data-ttu-id="d6fce-222">Wählen Sie **Datei** und dann **Element hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-222">Choose **File**, and then choose **Add Item**.</span></span>
    
  
2. <span data-ttu-id="d6fce-223">Gehen Sie folgendermaßen vor, um einen Listenworkflow zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="d6fce-223">To create a List Workflow, do the following:</span></span>
    
1. <span data-ttu-id="d6fce-224">Wählen Sie unter **Workflows** **Listenworkflow** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-224">Under **Workflows**, choose **List Workflow**.</span></span>
    
  
2. <span data-ttu-id="d6fce-225">Geben Sie im linken Bereich unter **Listenworkflow** einen Namen für Ihren Workflow ein (Mein erster SP2013-Workflow), und wählen Sie die Liste auf der Website aus, auf der Sie den Workflow veröffentlichen möchten.</span><span class="sxs-lookup"><span data-stu-id="d6fce-225">In the left pane under **List Workflow**, type a name for your workflow (My First SP2013 Workflow) and select the list on the site that you want to publish the workflow to.</span></span>
    
  
3. <span data-ttu-id="d6fce-226">Wählen Sie in der Liste **Workflowplattform für den neuen Workflow auswählen** **SharePoint-Workflow** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-226">In the **Choose the workflow platform for the new workflow** list, select **SharePoint Workflow**.</span></span>
    
  
4. <span data-ttu-id="d6fce-227">Wählen Sie **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="d6fce-227">Choose **Create**.</span></span>
    
  
3. <span data-ttu-id="d6fce-228">Gehen Sie folgendermaßen vor, um einen Websiteworkflow zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="d6fce-228">To create a Site Workflow, do the following:</span></span>
    
1. <span data-ttu-id="d6fce-229">Wählen Sie unter **Workflows** **Websiteworkflow** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-229">Under **Workflows**, choose **Site Workflow**.</span></span>
    
  
2. <span data-ttu-id="d6fce-230">Geben Sie im linken Bereich unter **Websiteworkflow** einen Namen für Ihren Workflow ein (Mein erster SP2013-Workflow).</span><span class="sxs-lookup"><span data-stu-id="d6fce-230">In the left pane, under **Site Workflow**, type a name for your workflow (My First SP2013 Workflow).</span></span>
    
  
3. <span data-ttu-id="d6fce-231">Wählen Sie in der Liste **Workflowplattform für den neuen Workflow auswählen** **SharePoint-Workflow** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-231">In the **Choose the workflow platform for the new workflow** list, select **SharePoint Workflow**.</span></span>
    
  
4. <span data-ttu-id="d6fce-232">Wählen Sie **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="d6fce-232">Choose **Create**.</span></span>
    
  
4. <span data-ttu-id="d6fce-233">Wählen Sie auf der Registerkarte **Workflow** in der Gruppe **Verwalten** **Workfloweinstellungen** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-233">On the **Workflow** tab, in the **Manage** group, choose **Workflow Settings**.</span></span>
    
  
5. <span data-ttu-id="d6fce-234">Wählen Sie auf der Registerkarte **Workfloweinstellungen** in der Gruppe **Verwalten** **Aus Visio importieren** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-234">On the **Workflow Settings** tab, in the **Manage** group, choose **Import from Visio.**</span></span>
    
  
6. <span data-ttu-id="d6fce-235">Navigieren Sie im Dialogfeld **Workflow aus Visio-Zeichnung importieren** zum Speicherort der .vsdx-Datei.</span><span class="sxs-lookup"><span data-stu-id="d6fce-235">In the **Import Workflow from Visio Drawing** dialog box, browse to the location where the .vsdx file is located.</span></span>
    
  
7. <span data-ttu-id="d6fce-236">Wählen Sie die Datei aus, die Sie öffnen möchten (Mein SP-Workflow), und wählen Sie dann **Öffnen** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-236">Select the file that you want to open (My SP Workflow), and then choose **Open**.</span></span>
    
  
<span data-ttu-id="d6fce-p128">Wenn Sie eine .vsdx-Datei in SharePoint Designer 2013 öffnen, wird die Datei im Visual Designer, einem in SharePoint Designer gehosteten Visio-ActiveX-Steuerelement, angezeigt. Das Visio 2013-Diagramm enthält alle in Visio erstellten Shapes und sämtlichen Shape-Text.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p128">When you open a .vsdx file in SharePoint Designer 2013, the file is displayed in the Visual Designer, a Visio ActiveX control that is hosted within SharePoint Designer. The Visio 2013 diagram retains all of the shapes and shape text that was created in Visio.</span></span> 
  
> [!NOTE] 
> <span data-ttu-id="d6fce-239">Zum Wechseln zwischen dem Visual Designer und dem Declarative Designer in SharePoint Designer 2013 wählen Sie auf der Registerkarte **Workflows** der Gruppe **Verwalten** die Option **Ansichten**.</span><span class="sxs-lookup"><span data-stu-id="d6fce-239">Note: To switch between the Visual Designer and the Declarative Designer in SharePoint Designer 2013, on the **Workflow** tab, in the **Manage** group, choose **Views**.</span></span> <span data-ttu-id="d6fce-240">Dieser Vorgang kann einen Moment dauern, da SharePoint Designer 2013 den Workflow überprüft und dann die Workflow-Informationen von einem Format in ein anderes umwandelt.</span><span class="sxs-lookup"><span data-stu-id="d6fce-240">This process may take a few moments, as SharePoint Designer 2013 validates the workflow and then converts the workflow information from one format to another.</span></span> <span data-ttu-id="d6fce-241">Während dieses Vorgangs wird eine weitere Überprüfung auf Shape-Ebene durchgeführt.</span><span class="sxs-lookup"><span data-stu-id="d6fce-241">During this process, another shape level validation will occur.</span></span> <span data-ttu-id="d6fce-242">Wenn Fehler im Diagramm erkannt werden, werden die Fehler in einem Fehlerbereich am unteren Rand (wie in Visio) angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d6fce-242">If any errors are detected with the diagram, the errors will be displayed in an error pane at the bottom of the canvas (just like in Visio).</span></span> 
  
    
    

<span data-ttu-id="d6fce-p130">Die im Visual Designer angezeigten Shapes weisen auch Aktionstags auf (unten links im Shape durch ein Symbol des Typs Workfloweinstellungen dargestellt). Wenn Sie ein Aktionstag auswählen, zeigt ein Dropdownmenü die Attribute für diese Aktion oder Bedingung im Workflow und **Eigenschaften** an. Diese Eigenschaften definieren die Parameterwerte, die für diese Aktion verwendet werden sollen: aus welchen Listen Elemente abgerufen werden sollen, welcher Berechnungsoperator verwendet werden soll, oder an welche E-Mail-Adresse eine Nachricht gesendet werden soll. Wenn Sie eine in der Liste angezeigte Eigenschaft auswählen, wird ein Dialogfeld angezeigt, in dem Sie die Einstellungen für diese Eigenschaft anpassen können.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p130">The shapes that are displayed in the Visual Designer also have Action Tags (shown by a workflow settings type icon on the bottom left hand side of the shape). When you choose an Action Tag, a drop-down menu displays the attributes for that action or condition in the workflow and **Properties** property. These properties will define the parameter values to be used for that action: which lists to pull items from, what calculation operator to use, or which email address to send a message to. When you choose a property that is displayed in the list, a dialog box appears in which you can customize the settings for that property.</span></span>
  
    
    
<span data-ttu-id="d6fce-p131">So sind z. B. mit dem Shape **E-Mail senden** zwei Eigenschaften verknüpft: **E-Mail erstellen** und **Eigenschaften**. Wenn Sie **E-Mail erstellen** auswählen, wird das Dialogfeld **E-Mail-Nachricht definieren** angezeigt, in dem Sie die Nachricht erstellen können, die durch die Aktion gesendet werden soll. Wenn Sie **Eigenschaften** auswählen, wird das Dialogfeld **E-Mail senden - Eigenschaften** angezeigt, das alle Parameter für die Aktion anzeigt.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p131">For example, the **Send an email** shape has two properties associated with it: **Create Email** and **Properties**. When you choose **Create Email**, a **Define Email Message** dialog box appears in which you can create the message to be sent by the action. If you choose **Properties**, a **Send an Email Properties** dialog box appears that displays all of the parameters for the action.</span></span>
  
> [!NOTE] 
> <span data-ttu-id="d6fce-250">Weitere Informationen zu einzelnen Aktionen, Shapes und deren Eigenschaften finden Sie in den Artikeln [Shapes in der SharePoint Server-Workflowvorlage in Visio](shapes-in-the-sharepoint-server-workflow-template-in-visio.md) und [Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform.md)](workflow-actions-quick-reference-sharepoint-workflow-platform.md).</span><span class="sxs-lookup"><span data-stu-id="d6fce-250">[Note:](shapes-in-the-sharepoint-server-workflow-template-in-visio.md) For more information about individual actions, shapes, and their properties, see the articles  [Shapes in the SharePoint Server workflow template in Visio](workflow-actions-quick-reference-sharepoint-workflow-platform.md) and Workflow actions quick reference (SharePoint Workflow platform.md).</span></span> 
  
    
    

<span data-ttu-id="d6fce-p132">Wenn Sie die Eigenschaften im Workflow festgelegt haben und zum Veröffentlichen bereit sind, müssen Sie den Workflow in SharePoint Designer 2013 zuerst auf Fehler prüfen. Wenn Sie im Menüband auf der Registerkarte **Visual Designer** **Veröffentlichen** auswählen, prüft SharePoint Designer 2013 den Workflow automatisch auf Fehler. Wenn Sie möchten, können Sie die Fehlerprüfung auch manuell auslösen.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p132">Once you have set the properties within the workflow and are ready to publish, you must first check the workflow for errors in SharePoint Designer 2013. When you choose **Publish** in the **Visual Designer** tab in the ribbon, SharePoint Designer 2013 automatically checks the workflow for errors. If you want, you can also manually initiate the error checking.</span></span>
  
    
    
<span data-ttu-id="d6fce-254">Verwenden Sie das folgende Verfahren, um den SharePoint-Workflow in SharePoint Designer 2013 zu überprüfen:</span><span class="sxs-lookup"><span data-stu-id="d6fce-254">Use the following procedure to check the SharePoint workflow in SharePoint Designer 2013:</span></span>
  
    
    

### <a name="to-manually-check-a-workflow-for-errors-in-sharepoint-designer-2013"></a><span data-ttu-id="d6fce-255">So prüfen Sie einen Workflow in SharePoint Designer 2013 manuell auf Fehler</span><span class="sxs-lookup"><span data-stu-id="d6fce-255">To manually check a workflow for errors in SharePoint Designer 2013</span></span>


1. <span data-ttu-id="d6fce-256">Wählen Sie auf der Registerkarte **Visual Designer** in der Gruppe **Speichern** **Auf Fehler überprüfen** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-256">On the **Visual Designer** tab, in the **Save** group, choose **Check for Errors**.</span></span>
    
  
2. <span data-ttu-id="d6fce-p133">Werden im Workflow Fehler gefunden, wird unter dem Zeichenbereich von Visual Designer der Bereich **Probleme** geöffnet. Wählen Sie jedes Element in der Liste aus, um die Aktion, die Bedingung, den Konnektor, das Abschlusszeichen oder den Container im Workflow auszuwählen, der den Fehler verursacht hat.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p133">If any errors are found in the workflow, the **Issues** pane opens below the Visual Designer canvas. Choose each item in the list to select the action, condition, connector, terminator, or container in the workflow that caused the error.</span></span>
    
  
3. <span data-ttu-id="d6fce-p134">Beheben Sie jeden in der Liste **Probleme** aufgeführten Validierungsfehler. Nachdem alle Fehler behoben wurden, wählen Sie erneut **Auf Fehler überprüfen** aus.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p134">Resolve each validation error listed in the **Issues** list. Once all of the errors have been addressed, choose **Check for Errors** again.</span></span>
    
  
4. <span data-ttu-id="d6fce-261">Werden im Workflow keine Fehler gefunden, zeigtSharePoint Designer die Meldung an, dass im Workflow keine Fehler gefunden wurden.</span><span class="sxs-lookup"><span data-stu-id="d6fce-261">If no errors are found in the workflow, SharePoint Designer displays a message stating that no issues were found in the workflow.</span></span>
    
  
<span data-ttu-id="d6fce-p135">Wenn der Workflow überprüft wurde und keine Fehler gefunden wurden, können Sie den Workflow in der SharePoint-Liste veröffentlichen. Um den Workflow in SharePoint Designer 2013 zu veröffentlichen, wählen Sie auf der Registerkarte **Visual Designer** in der Gruppe **Speichern** **Veröffentlichen** aus. Wenn während des Veröffentlichungsvorgangs Fehler auftreten, kehrt SharePoint Designer 2013 zum Visual Designer zurück und zeigt die Fehler im Bereich **Fehler** an.</span><span class="sxs-lookup"><span data-stu-id="d6fce-p135">After the workflow has been checked and no issues have been found, you can publish the workflow to the SharePoint list. To publish the workflow from SharePoint Designer 2013, on the **Visual Designer** tab, in the **Save** group, choose **Publish**. If any errors occur during the publishing process, SharePoint Designer 2013 returns to the Visual Designer and displays the errors in the **Issues** pane.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="d6fce-265">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="d6fce-265">See also</span></span>
<span data-ttu-id="d6fce-266"><a name="VSSPD_Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="d6fce-266"><a name="VSSPD_Additional"> </a></span></span>

<span data-ttu-id="d6fce-267">Weitere Informationen finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="d6fce-267">For more information, see the following resources:</span></span>
  
    
    

-  [<span data-ttu-id="d6fce-268">Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)</span><span class="sxs-lookup"><span data-stu-id="d6fce-268">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  
-  [<span data-ttu-id="d6fce-269">Shapes in der SharePoint Server-Workflowvorlage in Visio</span><span class="sxs-lookup"><span data-stu-id="d6fce-269">Shapes in the SharePoint Server workflow template in Visio</span></span>](shapes-in-the-sharepoint-server-workflow-template-in-visio.md)
    
  
-  [<span data-ttu-id="d6fce-270">Beheben von SharePoint Server 2013-Workflowvalidierungsfehlern in Visio 2013</span><span class="sxs-lookup"><span data-stu-id="d6fce-270">Troubleshooting SharePoint Server workflow validation errors in Visio</span></span>](troubleshooting-sharepoint-server-workflow-validation-errors-in-visio.md)
    
  
-  <span data-ttu-id="d6fce-271">[Erstellen, Importieren und Exportieren von SharePoint-Workflows in Visio]((http://office.microsoft.com/de-DE/visio-help/create-import-and-export-sharepoint-workflows-in-visio-HA101888007.aspx))</span><span class="sxs-lookup"><span data-stu-id="d6fce-271">[Create, import, and export SharePoint workflows in Visio 2010]((http://office.microsoft.com/de-DE/visio-help/create-import-and-export-sharepoint-workflows-in-visio-HA101888007.aspx))</span></span>
    
  
-  <span data-ttu-id="d6fce-272">[SharePoint Developer Center]((http://msdn.microsoft.com/de-DE/sharepoint/default.aspx))</span><span class="sxs-lookup"><span data-stu-id="d6fce-272">[SharePoint Developer Center]((http://msdn.microsoft.com/de-DE/sharepoint/default.aspx))</span></span>
    
  
-  <span data-ttu-id="d6fce-273">[Visio Developer Center]((http://msdn.microsoft.com/de-DE/office/aa905478))</span><span class="sxs-lookup"><span data-stu-id="d6fce-273">[Visio Developer Center]((http://msdn.microsoft.com/de-DE/office/aa905478))</span></span>
    
  

