---
title: Grundlegendes zum Packen und Verteilen von Workflows in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 545b4930-ac05-4c9d-9980-5818cb800cf1
ms.openlocfilehash: c7627a78d47fc01b2b5366e0919c85434cdcad96
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="understanding-how-to-package-and-deploy-workflow-in-sharepoint"></a><span data-ttu-id="4115c-102">Grundlegendes zum Packen und Bereitstellen von Workflows in SharePoint</span><span class="sxs-lookup"><span data-stu-id="4115c-102">Understanding how to package and deploy workflow in SharePoint</span></span>
<span data-ttu-id="4115c-103">Erhalten Sie Informationen zum Packen und Bereitstellen eines Workflows in SharePoint mit SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="4115c-103">Learn how to package and deploy a workflow in SharePoint Server 2013 with SharePoint Designer 2013.</span></span>
## <a name="overview-of-the-workflow-packaging-capabilities-of-sharepoint-designer-2013"></a><span data-ttu-id="4115c-104">Übersicht über die Workflow-Packfunktionen von SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="4115c-104">Overview of the workflow packaging capabilities of SharePoint Designer 2013</span></span>
<span data-ttu-id="4115c-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="4115c-105"></span></span>

<span data-ttu-id="4115c-106">SharePoint Designer 2013 bietet die Möglichkeit, einen Workflow als Vorlage zu speichern.</span><span class="sxs-lookup"><span data-stu-id="4115c-106">SharePoint Designer 2013 provides the capability to save a workflow as a template.</span></span> <span data-ttu-id="4115c-107">Das Speichern eines Workflows als Vorlage wird auch als Packen des Workflows bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="4115c-107">Saving a workflow as a template is also known as packaging the workflow.</span></span> <span data-ttu-id="4115c-108">Nachdem der Workflow als Vorlage gespeichert wurde, kann er in die SharePoint-Umgebungen importiert und verwendet werden, ohne dass der Workflow neu entwickelt werden muss.</span><span class="sxs-lookup"><span data-stu-id="4115c-108">After the workflow is saved as a template, it can then be imported into other SharePoint environments and used without the need to redevelop the workflow.</span></span> <span data-ttu-id="4115c-109">Nicht alle Arten von Workflows können als Vorlage gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="4115c-109">Not all workflow types can be saved as a template.</span></span> <span data-ttu-id="4115c-110">Die folgende Matrix zeigt die Workflowtypen, die als Vorlage gespeichert werden können.</span><span class="sxs-lookup"><span data-stu-id="4115c-110">The following matrix shows the workflow types that can be saved as a template.</span></span> 
  
    
    

<span data-ttu-id="4115c-111">**Unterstützung nach Plattform für das Speichern eines Workflows als Vorlage**</span><span class="sxs-lookup"><span data-stu-id="4115c-111">**Support, by platform, for saving a workflow as a template**</span></span>


|<span data-ttu-id="4115c-112">**Workflowtyp**</span><span class="sxs-lookup"><span data-stu-id="4115c-112">**Workflow type**</span></span>|<span data-ttu-id="4115c-113">**SharePoint 2010 Workflow-Plattform**</span><span class="sxs-lookup"><span data-stu-id="4115c-113">**SharePoint 2010 Workflow platform**</span></span>|<span data-ttu-id="4115c-114">**SharePoint-Workflowplattform**</span><span class="sxs-lookup"><span data-stu-id="4115c-114">**SharePoint Workflow platform**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="4115c-115">Listenworkflow</span><span class="sxs-lookup"><span data-stu-id="4115c-115">List Workflow</span></span>  <br/> |<span data-ttu-id="4115c-116">Nein</span><span class="sxs-lookup"><span data-stu-id="4115c-116">No</span></span>  <br/> |<span data-ttu-id="4115c-117">Ja</span><span class="sxs-lookup"><span data-stu-id="4115c-117">Yes</span></span>  <br/> |
|<span data-ttu-id="4115c-118">Website-Workflow</span><span class="sxs-lookup"><span data-stu-id="4115c-118">Site Workflow</span></span>  <br/> |<span data-ttu-id="4115c-119">Nein</span><span class="sxs-lookup"><span data-stu-id="4115c-119">No</span></span>  <br/> |<span data-ttu-id="4115c-120">Ja</span><span class="sxs-lookup"><span data-stu-id="4115c-120">Yes</span></span>  <br/> |
|<span data-ttu-id="4115c-121">Wieder verwendbaren Workflows</span><span class="sxs-lookup"><span data-stu-id="4115c-121">Reusable Workflow</span></span>  <br/> |<span data-ttu-id="4115c-122">Ja</span><span class="sxs-lookup"><span data-stu-id="4115c-122">Yes</span></span>  <br/> |<span data-ttu-id="4115c-123">Ja</span><span class="sxs-lookup"><span data-stu-id="4115c-123">Yes</span></span>  <br/> |
   

  
    
    

  
    
    

> <span data-ttu-id="4115c-124">**Hinweis:** SharePoint enthält zwei verschiedene Workflowplattformen: die SharePoint 2010-Workflowplattform und die SharePoint-Workflowplattform.</span><span class="sxs-lookup"><span data-stu-id="4115c-124">**Note:** SharePoint contains two different workflow platforms: the SharePoint 2010 Workflow platform and the SharePoint Workflow platform.</span></span> <span data-ttu-id="4115c-125">Beide Plattformen stehen in SharePoint zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="4115c-125">Both platforms are available in SharePoint.</span></span> <span data-ttu-id="4115c-126">Weitere Informationen zu den beiden Workflows finden Sie unter [Erste Schritte mit SharePoint-Workflow.](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)</span><span class="sxs-lookup"><span data-stu-id="4115c-126">For more information about the two workflow, see  [Getting started with SharePoint workflow.](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)</span></span>
  
    
    


## <a name="packaging-a-workflow-by-using-sharepoint-designer-2013"></a><span data-ttu-id="4115c-127">Packen eines Workflows in SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="4115c-127">Packaging a workflow by using SharePoint Designer 2013</span></span>
<span data-ttu-id="4115c-128"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="4115c-128"></span></span>

<span data-ttu-id="4115c-p103">Der Prozess für das Verpacken eines Workflows umfasst das Speichern des Workflows in eine Vorlagendatei mit SharePoint Designer 2013. Ein Workflow-Paket liegt in Form einer Datei Web Solution Package (WSP) und hat die Dateierweiterung WSP. Wenn Sie ein Paket ein Workflows gehen Sie folgendermaßen vor.</span><span class="sxs-lookup"><span data-stu-id="4115c-p103">The process for packaging a workflow involves saving the workflow to a template file by using SharePoint Designer 2013. A workflow package is in the form of a Web Solution Package (WSP) file and has a .wsp extension. To package a workflow follow these steps.</span></span> 
  
    
    

### <a name="package-a-workflow"></a><span data-ttu-id="4115c-132">Paket eines Workflows</span><span class="sxs-lookup"><span data-stu-id="4115c-132">Package a workflow</span></span>


1. <span data-ttu-id="4115c-133">Öffnen Sie einen vorhandenen Workflow oder entwickeln Sie neuen Workflow in SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="4115c-133">Open an existing workflow, or develop a new workflow, in SharePoint Designer 2013.</span></span>
    
  
2. <span data-ttu-id="4115c-134">Klicken Sie auf der Registerkarte **Workfloweinstellungen** im Menüband auf die Schaltfläche **Speichern als Vorlage** im Abschnitt **Verwalten**, wie in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="4115c-134">On the **Workflow Settings** tab in the ribbon, click the **Save as Template** button in the **Manage** section as shown in the figure.</span></span>
    
   <span data-ttu-id="4115c-135">**Abbildung: Speichern Sie Workflow als Vorlage.**</span><span class="sxs-lookup"><span data-stu-id="4115c-135">**Figure: Save workflow as template**</span></span>

  

  ![Paketworkflow in SPD 2013](../images/SPD15-PackagingWorkflow1.png)
  

  

  
3. <span data-ttu-id="4115c-137">Ein Dialogfeld mit Informationen wird angezeigt, damit Sie wissen, dass die Vorlage in der Bibliothek **Websiteobjekte** gespeichert wurde.</span><span class="sxs-lookup"><span data-stu-id="4115c-137">An informational dialog box appears to let you know the template has been saved to the **Site Assets** library.</span></span>
    
  
4. <span data-ttu-id="4115c-138">Klicken Sie auf der Bibliothek Websiteobjekte, um die Workflowvorlage anzuzeigen, wie in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="4115c-138">Click the Site Assets library to view the workflow template as shown in the figure.</span></span>
    
   <span data-ttu-id="4115c-139">**Abbildung: Eine Workflowvorlage in Websiteobjekten**</span><span class="sxs-lookup"><span data-stu-id="4115c-139">**Figure: A workflow template in Site Assets**</span></span>

  

  ![Workflowvorlage in Websiteobjekten.](../images/SPD15-PackagingWorkflow2.png)
  

  

  

  
    
    

> <span data-ttu-id="4115c-141">**Tipp:** Eine Workflowvorlage speichert automatisch in der Bibliothek **Websiteobjekte** der Websitesammlung, in die sich der Workflow befindet.</span><span class="sxs-lookup"><span data-stu-id="4115c-141">**TIP** A workflow template automatically saves to the **Site Assets** library of the site collection in which the workflow resides.</span></span>
  
    
    


## <a name="deploying-a-workflow-package-to-sharepoint"></a><span data-ttu-id="4115c-142">Bereitstellen eines Workflowpakets in SharePoint</span><span class="sxs-lookup"><span data-stu-id="4115c-142">Deploying a workflow package to SharePoint</span></span>
<span data-ttu-id="4115c-143"><a name="section3"> </a></span><span class="sxs-lookup"><span data-stu-id="4115c-143"></span></span>

<span data-ttu-id="4115c-p104">Sie können einem Workflow-Paket bereitstellen, zu einer SharePoint-Farm oder Website, die unterscheidet sich von der Farm oder Website entwickelt wurde. In der Reihenfolge für einen Workflow muss Bereitstellung erfolgreich zwei Elemente werden erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="4115c-p104">You can deploy a workflow package to a SharePoint farm or site that is different from the farm or site in which it was developed. In order for a workflow deployment to be successful two items must be fulfilled:</span></span>
  
    
    

- <span data-ttu-id="4115c-146">Alle Workflow Abhängigkeiten wie Listen, Bibliotheken, Spalten und Inhaltstypen müssen auf der neuen Website bereits vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="4115c-146">All workflow dependencies such as lists, libraries, columns, and content types must already exist on the new site.</span></span>
    
  
- <span data-ttu-id="4115c-147">Jede einzelne Abhängigkeit benötigen den genauen Namen der Quelle Abhängigkeit.</span><span class="sxs-lookup"><span data-stu-id="4115c-147">Each dependency must have the exact name of the source dependency.</span></span>
    
  
<span data-ttu-id="4115c-148">Wenn ein Workflow bereitgestellt wird und die genauen Abhängigkeiten nicht vorhanden sind, wird ein Fehler ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="4115c-148">If a workflow is deployed and the exact dependencies do not exist then the result will be an error.</span></span>
  
    
    
<span data-ttu-id="4115c-149">Bevor Sie einen Workflow bereitstellen können, müssen Sie zuerst die Workflowvorlage aus der SharePoint-Quellfarm exportieren.</span><span class="sxs-lookup"><span data-stu-id="4115c-149">Before you can deploy a workflow you must first export the workflow template from the source SharePoint Server 2013 farm. To export a workflow template, follow this procedure.</span></span> <span data-ttu-id="4115c-150">Verwenden Sie dieses Verfahren, um eine Workflowvorlage zu exportieren.</span><span class="sxs-lookup"><span data-stu-id="4115c-150">To deploy a workflow package follow this procedure.</span></span>
  
    
    

### <a name="export-a-workflow-template"></a><span data-ttu-id="4115c-151">Exportieren einer Workflowvorlage</span><span class="sxs-lookup"><span data-stu-id="4115c-151">Export a workflow template</span></span>


1. <span data-ttu-id="4115c-152">Öffnen Sie SharePoint Designer 2013, und navigieren Sie zu der Bibliothek Websiteobjekte, in die Vorlage gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="4115c-152">Open SharePoint Designer 2013 and navigate to the Site Assets library where the template is located.</span></span>
    
  
2. <span data-ttu-id="4115c-153">Wählen Sie die Workflowvorlage aus, den, die Sie durch Klicken auf exportieren möchten.</span><span class="sxs-lookup"><span data-stu-id="4115c-153">Select the workflow template you want to export by clicking it.</span></span>
    
  
3. <span data-ttu-id="4115c-154">Klicken Sie auf die Schaltfläche **Datei exportieren**, um die Vorlagendatei an Ihrem lokalen Computer oder einem Netzlaufwerk zu speichern, wie in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="4115c-154">Click the **Export File** button to save the template file to your local computer or a network drive, as shown in the figure.</span></span>
    
   <span data-ttu-id="4115c-155">**Abbildung: Exportieren der Workflowvorlage aus SharePoint Designer 2013**</span><span class="sxs-lookup"><span data-stu-id="4115c-155">**Figure: Export workflow template from SharePoint Designer 2013**</span></span>

  

  ![Workflowdatei aus SPD exportieren.](../images/SPD15-PackagingWorkflow3.png)
  

  

  
<span data-ttu-id="4115c-157">Zum Bereitstellen von einem Workflow-Paket verwenden Sie dieses Verfahren.</span><span class="sxs-lookup"><span data-stu-id="4115c-157">To deploy a workflow package follow this procedure.</span></span>
  
    
    

### <a name="deploy-a-workflow-solution"></a><span data-ttu-id="4115c-158">Bereitstellen einer Workflowlösung</span><span class="sxs-lookup"><span data-stu-id="4115c-158">Deploy a workflow solution</span></span>


1. <span data-ttu-id="4115c-159">Öffnen Sie Internet Explorer und navigieren Sie zu der SharePoint-Websitesammlung, in der Sie den Workflow bereitstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="4115c-159">Open Internet Explorer and navigate to the SharePoint Server 2013 site collection where you want to deploy the workflow.</span></span>
    
  
2. <span data-ttu-id="4115c-160">Klicken Sie auf **Websiteaktionen** und wählen Sie **Websiteeinstellungen**.</span><span class="sxs-lookup"><span data-stu-id="4115c-160">Click **Site Actions** and select **Site Settings**.</span></span>
    
  
3. <span data-ttu-id="4115c-161">Klicken Sie im Abschnitt **Web-Designer-Kataloge** auf **Lösungen**.</span><span class="sxs-lookup"><span data-stu-id="4115c-161">In the **Web Design Galleries** section click **Solutions**.</span></span>
    
    > <span data-ttu-id="4115c-162">**Hinweis:** Sie müssen sich auf der Seite **Websiteeinstellungen** für die Websitesammlung befinden, um den Katalog **Lösungen** zu sehen.</span><span class="sxs-lookup"><span data-stu-id="4115c-162">**Note** You must be on the **Site Settings** page for the site collection in order to see the **Solutions** gallery. If you are on the Site Settings page for a sub-site then the Solutions gallery is not visible.</span></span> <span data-ttu-id="4115c-163">Wenn Sie sich auf der Seite **Websiteeinstellungen** für eine Unterwebsite befinden, ist der Katalog **Lösungen** nicht sichtbar ist.</span><span class="sxs-lookup"><span data-stu-id="4115c-163">Note You must be on the Site Settings page for the site collection in order to see the Solutions gallery. If you are on the **Site Settings** page for a sub-site then the **Solutions** gallery is not visible.</span></span>
4. <span data-ttu-id="4115c-164">Klicken Sie auf die Schaltfläche **Lösung hochladen**, um die Lösung wie in der Abbildung gezeigt hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="4115c-164">Click the **Upload Solution** button to upload the solution as shown in the figure.</span></span>
    
   <span data-ttu-id="4115c-165">**Abbildung: Lösungsschaltfläche hoch**</span><span class="sxs-lookup"><span data-stu-id="4115c-165">**Figure: Upload Solution button**</span></span>

  

  ![Schaltfläche zum Hochladen einer Lösung.](../images/SPD15-PackagingWorkflow4.png)
  

  

  
5. <span data-ttu-id="4115c-167">Aktivieren Sie die Lösung, indem Sie auf die Schaltfläche **Aktivieren**, wie in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="4115c-167">Activate the solution by clicking the **Activate** button as shown in the figure.</span></span>
    
   <span data-ttu-id="4115c-168">**Abbildung: Dialogfeld Lösung und die Schaltfläche aktivieren**</span><span class="sxs-lookup"><span data-stu-id="4115c-168">**Figure: Activate Solution dialog and button**</span></span>

  

  ![Lösung nach Hochladen aktivieren.](../images/SPD15-PackagingWorkflow5.png)
  

  

  
<span data-ttu-id="4115c-p107">Nachdem eine workflowlösung für eine Websitesammlung aktiviert wurde, kann es als ein Feature für alle untergeordneten Websites verfügbar. Verwenden Sie dieses Verfahren, um das Workflowfeature für eine Unterwebsite zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="4115c-p107">After a workflow solution has been activated for a site collection, it is available as a feature for all sub-sites. To activate the workflow feature for a sub-site, follow this procedure.</span></span>
  
    
    

### <a name="activate-the-workflow-feature"></a><span data-ttu-id="4115c-172">Aktivieren des Workflowfeatures</span><span class="sxs-lookup"><span data-stu-id="4115c-172">Activate the workflow feature</span></span>


1. <span data-ttu-id="4115c-173">Öffnen Sie die **Websiteeinstellungen** auf der Website, in dem Sie das Workflowfeature aktivieren möchten.</span><span class="sxs-lookup"><span data-stu-id="4115c-173">Open **Site Settings** on the site where you wish to activate the workflow feature.</span></span>
    
  
2. <span data-ttu-id="4115c-174">Klicken Sie in der Gruppe **Websiteaktionen** auf **Websitefeatures verwalten**.</span><span class="sxs-lookup"><span data-stu-id="4115c-174">In the **Site Actions** group, click **Manage site features**.</span></span>
    
  
3. <span data-ttu-id="4115c-175">Klicken Sie neben dem Workflowfeature auf **Aktivieren**, wie in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="4115c-175">Click **Activate** next to the workflow feature as shown in the figure.</span></span>
    
  

<span data-ttu-id="4115c-176">**Abbildung: Aktivieren Sie Workflowfeatures für Website**</span><span class="sxs-lookup"><span data-stu-id="4115c-176">**Figure: Activate workflow feature for site**</span></span>

  
    
    

  
    
    
![Website-Feature aktivieren.](../images/SPD15-PackagingWorkflow6.png)
  
    
    

  
    
    

  
    
    

## <a name="additional-resources"></a><span data-ttu-id="4115c-178">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="4115c-178">Additional resources</span></span>
<span data-ttu-id="4115c-179"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="4115c-179"></span></span>


-  [<span data-ttu-id="4115c-180">Workflow in SharePoint </span><span class="sxs-lookup"><span data-stu-id="4115c-180">Workflow in SharePoint </span></span>](http://technet.microsoft.com/en-us/sharepoint/jj556245.aspx)
    
  
-  [<span data-ttu-id="4115c-181">Neu in SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="4115c-181">What's new in workflow in SharePoint Server 2013</span></span>](http://msdn.microsoft.com/library/6ab8a28b-fa2f-4530-8b55-a7f663bf15ea.aspx)
    
  
-  [<span data-ttu-id="4115c-182">Erste Schritte mit SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="4115c-182">Getting started with SharePoint Server 2013 workflow</span></span>](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)
    
  
-  [<span data-ttu-id="4115c-183">Workflowentwicklung in SharePoint Designer und Visio</span><span class="sxs-lookup"><span data-stu-id="4115c-183">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [<span data-ttu-id="4115c-184">Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)</span><span class="sxs-lookup"><span data-stu-id="4115c-184">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  
-  [<span data-ttu-id="4115c-185">Blogartikel des SharePoint Designer-Teams: Verpackungs- und Bereitstellungsszenario für Workflows</span><span class="sxs-lookup"><span data-stu-id="4115c-185">Blog article from the SharePoint Designer team: Workflow package and deploy scenario</span></span>](http://blogs.msdn.com/b/sharepointdesigner/archive/2012/08/30/packaging-list-site-and-reusable-workflow-and-how-to-deploy-the-package.aspx)
    
  
