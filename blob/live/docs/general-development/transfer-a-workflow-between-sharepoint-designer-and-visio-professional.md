---
title: "Übertragen eines Workflows zwischen SharePoint Designer 2013 und Visio Professional 2013 (SharePoint 2010-Workflow-Plattform)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: dbe6f019-b4f2-480f-a8e7-bcb8842ab924
ms.openlocfilehash: 42d3743885eeea645e2f8a5a88b8646c68379d91
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="transfer-a-workflow-between-sharepoint-designer-2013-and-visio-professional-2013-sharepoint-2010-workflow-platform"></a><span data-ttu-id="64c49-102">Übertragen eines Workflows zwischen SharePoint Designer 2013 und Visio Professional 2013 (SharePoint 2010-Workflow-Plattform)</span><span class="sxs-lookup"><span data-stu-id="64c49-102">Transfer a workflow between SharePoint Designer 2013 and Visio Professional 2013 (SharePoint 2010 Workflow platform)</span></span>
<span data-ttu-id="64c49-103">Verwenden Sie SharePoint Designer zum Importieren eines Workflows aus Visio oder Exportieren eines Workflows zu Visio.</span><span class="sxs-lookup"><span data-stu-id="64c49-103">Use SharePoint Designer to import a workflow from Visio or export a workflow to Visio.</span></span>
## <a name="transferring-a-workflow-between-sharepoint-designer-2013-and-visio-professional-2013"></a><span data-ttu-id="64c49-104">Übertragen eines Workflows zwischen SharePoint Designer 2013 und Visio Professional 2013</span><span class="sxs-lookup"><span data-stu-id="64c49-104">Transferring a workflow between SharePoint Designer 2013 and Visio Professional 2013</span></span>
<span data-ttu-id="64c49-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="64c49-105"></span></span>

<span data-ttu-id="64c49-p101">Geschäfts- und Prozessanalysten, die bereits mit der Flussdiagrammerstellung in Visio vertraut sind, können Visio zum Erstellen eines SharePoint-Workflows verwenden. Der Workflow stellt in Visio die Geschäftslogik dar. Wenn die Geschäftslogik vollständig ist, kann der Workflow zu SharePoint Designer exportiert werden. Wenn der Workflow in SharePoint Designer vorhanden ist, kann ein IT-Experte diesen mit der SharePoint-Website verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="64c49-p101">Business analysts and process analysts who are already familiar with flowcharting in Visio can use Visio to design a SharePoint workflow. The workflow in Visio represents the business logic. After the business logic is complete, the workflow can be exported to SharePoint Designer. Once the workflow is in SharePoint Designer, an IT professional can wire it up to the SharePoint site.</span></span>
  
    
    

  
    
    
![Übersetzen von Geschäftslogik in Workflowregeln](../images/spd15-wf-importFromVisio.png)
  
    
    
<span data-ttu-id="64c49-111">Sie können in Microsoft SharePoint Designer 2013 einen in Microsoft Visio Professional 2013 erstellten Workflow importieren oder einen Workflow zu Visio zur Ansicht exportieren.</span><span class="sxs-lookup"><span data-stu-id="64c49-111">In Microsoft SharePoint Designer 2013, you can import a workflow created in Microsoft Visio Professional 2013 or export a workflow to Visio for viewing.</span></span> 
  
    
    
<span data-ttu-id="64c49-112">In diesem Artikel wird die Übertragung eines Workflows mithilfe der SharePoint 2010-Workflowplattform in SharePoint Designer 2013 beschrieben.</span><span class="sxs-lookup"><span data-stu-id="64c49-112">This article describes transferring a workflow by using the SharePoint 2010 Workflow platform in SharePoint Designer 2013.</span></span>
  
    
    
<span data-ttu-id="64c49-113">So wählen Sie die SharePoint 2010-Workflowplattform aus, wenn Sie einen Workflow erstellen</span><span class="sxs-lookup"><span data-stu-id="64c49-113">To select the SharePoint 2010 Workflow platform when you create a workflow:</span></span>
  
    
    

  
    
    

1. <span data-ttu-id="64c49-114">Klicken Sie im Bereich **Navigation** auf **Workflows**.</span><span class="sxs-lookup"><span data-stu-id="64c49-114">In the **Navigation** pane, click **Workflows**.</span></span>
    
  
2. <span data-ttu-id="64c49-115">Klicken Sie auf der Registerkarte **Workflows** im Abschnitt **Neu** auf **Listenworkflow**, **Wieder verwendbarer Workflow** oder **Websiteworkflow**.</span><span class="sxs-lookup"><span data-stu-id="64c49-115">On the **Workflows** tab, in the **New** section, click **List Workflow**, **Reusable Workflow**, or **Site Workflow**.</span></span>
    
  
3. <span data-ttu-id="64c49-116">Klicken Sie im Dialogfeld **Workflow erstellen** im Feld **Plattformtyp** auf **SharePoint 2010-Workflow**.</span><span class="sxs-lookup"><span data-stu-id="64c49-116">In the **Create Workflow** dialog box, in the **Platform Type** box, click **SharePoint 2010 Workflow**.</span></span>
    
  
<span data-ttu-id="64c49-117">Sie können Workflows in SharePoint Designer auf zwei Arten darstellen:</span><span class="sxs-lookup"><span data-stu-id="64c49-117">You can visualize workflows in SharePoint Designer in two ways:</span></span>
  
    
    

- <span data-ttu-id="64c49-118">Wenn Visio Services auf dem Server installiert ist, auf dem SharePoint ausgeführt wird, können Sie eine Workflowvisualisierung auf der Workflowstatusseite erstellen, auf der Status und Zuordnungen angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="64c49-118">If Visio Services is installed on the server that is running SharePoint, you can create a workflow visualization on the workflow status page that displays progress and assignments.</span></span>
    
  
- <span data-ttu-id="64c49-119">Sie können den Workflow zu Visio exportieren, um eine Workflowzeichnung zu erstellen, die für Feedback oder Genehmigung verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="64c49-119">You can export the workflow to Visio to create a workflow drawing that can be used for feedback and approval.</span></span>
    
  

  
    
    
![Workflowdiagramme können in Visio exportiert werden](../images/spd15-wf-exportToVisio.png)
  
    
    

  
    
    

  
    
    

## <a name="import-a-workflow-from-visio"></a><span data-ttu-id="64c49-121">Importieren eines Workflows aus Visio</span><span class="sxs-lookup"><span data-stu-id="64c49-121">Import a workflow from Visio</span></span>
<span data-ttu-id="64c49-122"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="64c49-122"></span></span>

<span data-ttu-id="64c49-123">So importieren Sie ein SharePoint-Workflow</span><span class="sxs-lookup"><span data-stu-id="64c49-123">To import a SharePoint workflow, do the following:</span></span>
  
    
    

1. <span data-ttu-id="64c49-124">Klicken Sie in SharePoint Designer 2013 im Bereich **Navigation** auf **Workflows**.</span><span class="sxs-lookup"><span data-stu-id="64c49-124">In SharePoint Designer 2013, in the **Navigation** pane, click **Workflows**.</span></span>
    
  
2. <span data-ttu-id="64c49-125">Klicken Sie auf der Registerkarte **Workflows** in der Gruppe **Verwalten** auf **Aus Visio importieren**.</span><span class="sxs-lookup"><span data-stu-id="64c49-125">On the **Workflows** tab, in the **Manage** group, click **Import from Visio**.</span></span>
    
  ![Importworkflow](../images/spd15-ImportFromVisio.JPG)
  

  

  
3. <span data-ttu-id="64c49-127">Navigieren Sie im Dialogfeld **Workflow aus Visio-Zeichnung importieren** zu der zu verwendenden VWI-Datei ( Visio Workflow Interchange), wählen Sie diese aus, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="64c49-127">In the **Import Workflow from Visio Drawing** dialog box, browse to and select the Visio Workflow Interchange (.vwi) file you want to use, and then click **Next**.</span></span>
    
  
4. <span data-ttu-id="64c49-p102">Geben Sie einen Namen für den Workflow an, und wählen Sie dann den gewünschten Workflowtyp aus. Folgende Optionen stehen zur Auswahl:</span><span class="sxs-lookup"><span data-stu-id="64c49-p102">Type a name for the workflow, and then select the type of workflow you want it to be once it has been imported. Your choices are:</span></span>
    
  - <span data-ttu-id="64c49-p103">**Listenworkflow** Ein Workflow, der einer bestimmten Liste angefügt ist. Wenn Sie diese Option wählen, müssen Sie die Liste wählen, der der Workflow angefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="64c49-p103">**List workflow** A workflow that is attached to a specific list. If you select this option, you must choose the list to which the workflow will be attached.</span></span>
    
  
  - <span data-ttu-id="64c49-p104">**Wieder verwendbarer Workflow** Ein Workflow, der einem Inhaltstyp angefügt ist und daher portabel. Er kann von unterschiedlichen Listen auf einer SharePoint-Website verwendet werden. Wenn Sie diese Option wählen, müssen Sie den Inhaltstyp wählen, auf dem der Workflow ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="64c49-p104">**Reusable workflow** A workflow that is attached to a content type, and is therefore portable. It can be used by different lists on a SharePoint site. If you select this option, you must choose the content type on which the workflow will run.</span></span>
    
  
5. <span data-ttu-id="64c49-135">Klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="64c49-135">Click **Finish**.</span></span>
    
  
<span data-ttu-id="64c49-p105">Der importierte Workflow wird im Workflow-Editor in SharePoint Designer im Vollbildmodus angezeigt. Der gesamte Text in benutzerdefinierten Visio-Formen wird im SharePoint Designer als Aktivitätsbezeichnung importiert (der graue Text in der Abbildung unten), um die Absicht des Workflows zu erläutern.</span><span class="sxs-lookup"><span data-stu-id="64c49-p105">The imported workflow appears in the SharePoint Designer full-screen workflow editor. All text in the Visio custom shapes is imported into SharePoint Designer as activity labels (the gray text in the image below) to clarify the intent of the workflow:</span></span>
  
    
    

  
    
    
![Importierter Workflow](../images/spd15-wf-PO.JPG)
  
    
    
<span data-ttu-id="64c49-139">Wenn der Workflow in SharePoint Designer importiert wurde, kann er bearbeitet. Es können die notwendigen Bedingungen, Aktionen, Schritte und Einstellungen hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="64c49-139">After the workflow is imported to SharePoint Designer, it is editable and can be revised to add the necessary conditions, actions, steps, and settings.</span></span> 
  
    
    

## <a name="export-a-workflow-to-visio"></a><span data-ttu-id="64c49-140">Exportieren eines Workflows zu Visio</span><span class="sxs-lookup"><span data-stu-id="64c49-140">Export a workflow to Visio</span></span>
<span data-ttu-id="64c49-141"><a name="section3"> </a></span><span class="sxs-lookup"><span data-stu-id="64c49-141"></span></span>

<span data-ttu-id="64c49-p106">Nachdem Sie einen Workflow in SharePoint Designer 2013 erstellt oder bearbeitet haben, können Sie den Workflow als Visio-Zeichnung exportieren, die in Visio Professional 2013 geöffnet werden kann. Die Möglichkeit, einen Workflow zurück zu Visio exportieren zu können, nachdem er in SharePoint Designer bearbeitet wurde, auch Roundtrips genannt, ermöglicht eine stärkere Zusammenarbeit zwischen Geschäftsbenutzern und Workflowdesignern. Wenn Sie den Workflowentwurf auf diese Weise durchlaufen, können Sie Visio zum Definieren der Geschäftsanforderungen verwenden und dann Roundtrips verwenden, um Änderungen zu koordinieren und zu genehmigen.</span><span class="sxs-lookup"><span data-stu-id="64c49-p106">Once you have created or edited a workflow in SharePoint Designer 2013, you can export the workflow as a Visio drawing that can be opened in Visio Professional 2013. The ability to export a workflow back to Visio after it has been edited in SharePoint Designer—also known as "round-tripping"—enables deeper collaboration between business users and workflow designers. When you iterate the workflow design in this way, you can use Visio to define the business requirements and then use round-tripping to coordinate and approve changes.</span></span>
  
    
    

> <span data-ttu-id="64c49-145">**Hinweis:** Visio Professional 2013 bietet keine Unterstützung für Schritte.</span><span class="sxs-lookup"><span data-stu-id="64c49-145">**Note:** Visio Professional 2013 does not support steps.</span></span> <span data-ttu-id="64c49-146">In SharePoint Designer hinzugefügte Schrittinformationen gehen möglicherweise verloren, wenn der Workflow in Visio geöffnet und dann zurück in SharePoint Designer importiert wird.</span><span class="sxs-lookup"><span data-stu-id="64c49-146">vispro15short does not support steps. Step information that has been added in SharePoint Designer may be lost when the workflow is viewed in Visio and then re-imported into SharePoint Designer.</span></span> 
  
    
    

<span data-ttu-id="64c49-147">Gehen Sie wie folgt vor, um einen Workflow zu exportieren:</span><span class="sxs-lookup"><span data-stu-id="64c49-147">To export a workflow, do the following:</span></span>
  
    
    

1. <span data-ttu-id="64c49-148">Klicken Sie in SharePoint Designer 2013 im Bereich **Navigation** auf **Workflows**.</span><span class="sxs-lookup"><span data-stu-id="64c49-148">In SharePoint Designer 2013, click **Workflows** in the **Navigation** pane.</span></span>
    
  
2. <span data-ttu-id="64c49-149">Klicken Sie auf der Registerkarte **Workflow** in der Gruppe **Verwalten** auf **Nach Visio exportieren**.</span><span class="sxs-lookup"><span data-stu-id="64c49-149">On the **Workflow** tab, in the **Manage** group, click **Export to Visio**.</span></span>
    
  
3. <span data-ttu-id="64c49-p108">Geben Sie im Dialogfeld **Workflow in Visio-Zeichnung exportieren** einen Namen für die Datei an, wählen Sie einen Speicherort, und klicken Sie auf **Speichern**. Die exportierte Datei wird als VWI-Datei gespeichert, die in Visio Professional 2013 direkt geöffnet werden kann.</span><span class="sxs-lookup"><span data-stu-id="64c49-p108">In the **Export Workflow to Visio Drawing** dialog box, name the file, select a location, and then click **Save**. The exported file is saved as a .vwi file that can be opened directly in Visio Professional 2013.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="64c49-152">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="64c49-152">Additional resources</span></span>
<span data-ttu-id="64c49-153"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="64c49-153"></span></span>


-  [<span data-ttu-id="64c49-154">Neuerungen in Workflows für SharePoint</span><span class="sxs-lookup"><span data-stu-id="64c49-154">What's new in workflows for SharePoint</span></span>](what-s-new-in-workflows-for-sharepoint.md)
    
  
-  [<span data-ttu-id="64c49-155">Erste Schritte mit Workflows in SharePoint</span><span class="sxs-lookup"><span data-stu-id="64c49-155">Get started with workflows in SharePoint</span></span>](get-started-with-workflows-in-sharepoint.md)
    
  
-  [<span data-ttu-id="64c49-156">Workflowentwicklung in SharePoint Designer und Visio</span><span class="sxs-lookup"><span data-stu-id="64c49-156">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  

  
    
    

