---
title: "Änderungen in SharePoint Designer 2013"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f1cd30c9-9a73-428d-9151-f1813b43b020
ms.openlocfilehash: e336ccd9ad1a257ffa3c8bb44ed3b4933c8784ea
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="whats-changed-in-sharepoint-designer-2013"></a><span data-ttu-id="bebe0-102">Änderungen in SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="bebe0-102">What's changed in SharePoint Designer 2013</span></span>
<span data-ttu-id="bebe0-p101">Hier erhalten Sie Informationen zu Features, die veraltet sind oder aus SharePoint Designer 2013 entfernt wurden. Veraltete Features sind in SharePoint aus Kompatibilitätsgründen mit der vorherigen Produktversion weiterhin vorhanden, werden aber in zukünftigen Versionen entfernt.</span><span class="sxs-lookup"><span data-stu-id="bebe0-p101">Learn about features that are deprecated in or removed from SharePoint Designer 2013. Features that are deprecated are included in the SharePoint release for compatibility with previous product versions but will be removed from future versions.</span></span>
## <a name="discontinued-features-in-sharepoint-designer-2013"></a><span data-ttu-id="bebe0-105">Eingestellte Features in SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="bebe0-105">Discontinued features in SharePoint Designer 2013</span></span>
<span data-ttu-id="bebe0-106"><a name="WhatsChangedSharePointDesigner2013_DiscontinuedFeatures"> </a></span><span class="sxs-lookup"><span data-stu-id="bebe0-106"></span></span>

<span data-ttu-id="bebe0-107">Die folgenden Features wurden in SharePoint Designer 2013 eingestellt oder entfernt.</span><span class="sxs-lookup"><span data-stu-id="bebe0-107">The following features are deprecated in SharePoint Designer 2013 or have been removed.</span></span>
  
    
    

### <a name="sharepoint-2010-workflow-platform"></a><span data-ttu-id="bebe0-108">SharePoint 2010 Workflow-Plattform</span><span class="sxs-lookup"><span data-stu-id="bebe0-108">SharePoint 2010 Workflow platform</span></span>
<span data-ttu-id="bebe0-109"><a name="WhatsChangedSharePointDesigner2013_WorkflowPlatform"> </a></span><span class="sxs-lookup"><span data-stu-id="bebe0-109"></span></span>

 <span data-ttu-id="bebe0-p102">**Beschreibung der Änderung.** Einige Features der SharePoint 2010-Workflow-Plattform, die von der Windows Workflow Foundation 3.0 abhängig sind, wurden in SharePoint eingestellt.</span><span class="sxs-lookup"><span data-stu-id="bebe0-p102">**Description of the change.** Some features of the SharePoint 2010 Workflow platform that are dependent on Windows Workflow Foundation 3.0 are deprecated in SharePoint.</span></span>
  
    
    
 <span data-ttu-id="bebe0-112"> **Änderungsgrund.** SharePoint führt eine neue SharePoint-Workflow-Plattform ein, die auf der Windows Workflow Foundation 4.0 aufsetzt und mit Workflow-Manager 1.0 integriert wird.</span><span class="sxs-lookup"><span data-stu-id="bebe0-112">**Reason for the change.** SharePoint introduces a new SharePoint Workflow platform that is built upon Windows Workflow Foundation 4.0 and that is integrated with Workflow Manager 1.0.</span></span>
  
    
    
 <span data-ttu-id="bebe0-p103">**Migrationspfad.** In SharePoint Designer 2013 können Sie weiterhin einen SharePoint 2010-Workflow erstellen und alle Workflow-Features von SharePoint 2010 verwenden, indem Sie die SharePoint 2010-Workflow-Plattform auswählen.</span><span class="sxs-lookup"><span data-stu-id="bebe0-p103">**Migration path.** In SharePoint Designer 2013, you can still create a SharePoint 2010 Workflow and use all of the SharePoint 2010 Workflow features by choosing the SharePoint 2010 Workflow platform.</span></span>
  
    
    
<span data-ttu-id="bebe0-p104">Sie können auch Features der SharePoint 2010-Workflow-Plattform in die neue SharePoint-Workflow-Plattform integrieren. Erstellen Sie dazu einen SharePoint 2010-Workflow, indem Sie die SharePoint 2010-Workflow-Plattform auswählen. Erstellen Sie einen SharePoint-Workflow, indem Sie die SharePoint-Workflow-Plattform auswählen. Dann verwenden Sie die Aktionen **Listenworkflow starten** und **Website-Workflow starten** im SharePoint-Workflow, um den SharePoint 2010-Workflow aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="bebe0-p104">You can also integrate features from the SharePoint 2010 Workflow platform into the new SharePoint Workflow platform. To do this, create a SharePoint 2010 Workflow by choosing the SharePoint 2010 Workflow platform; create a SharePoint Workflow by choosing the SharePoint Workflow platform; and then use the **Start a list workflow** and **Start a site workflow** actions in the SharePoint Workflow to call the SharePoint 2010 Workflow.</span></span>
  
    
    
<span data-ttu-id="bebe0-117">Die folgenden Features stehen nur für die SharePoint 2010-Workflow-Plattform zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="bebe0-117">The following features are available only on the SharePoint 2010 Workflow platform:</span></span>
  
    
    

- <span data-ttu-id="bebe0-118">Aktionen:</span><span class="sxs-lookup"><span data-stu-id="bebe0-118">Actions:</span></span>
    
  - <span data-ttu-id="bebe0-119">Workflow beenden</span><span class="sxs-lookup"><span data-stu-id="bebe0-119">Stop Workflow</span></span>
    
  
  - <span data-ttu-id="bebe0-120">Version der Dokumentenmappe erfassen</span><span class="sxs-lookup"><span data-stu-id="bebe0-120">Capture a Version of the Document Set</span></span>
    
  
  - <span data-ttu-id="bebe0-121">Senden der Dokumentenmappe an das Repository</span><span class="sxs-lookup"><span data-stu-id="bebe0-121">Send Document Set to Repository</span></span>
    
  
  - <span data-ttu-id="bebe0-122">Inhaltsgenehmigungsstatus für die Dokumentenmappe festlegen</span><span class="sxs-lookup"><span data-stu-id="bebe0-122">Set Content Approval Status for the Document Set</span></span>
    
  
  - <span data-ttu-id="bebe0-123">Starten des Genehmigungsvorgangs für Dokumentenmappen</span><span class="sxs-lookup"><span data-stu-id="bebe0-123">Start Document Set Approval Process</span></span>
    
  
  - <span data-ttu-id="bebe0-124">Datensatz deklarieren</span><span class="sxs-lookup"><span data-stu-id="bebe0-124">Declare Record</span></span>
    
  
  - <span data-ttu-id="bebe0-125">Festlegen des Status für die Genehmigung von Inhalten</span><span class="sxs-lookup"><span data-stu-id="bebe0-125">Set Content Approval Status</span></span>
    
  
  - <span data-ttu-id="bebe0-126">Deklaration des Datensatzes aufheben</span><span class="sxs-lookup"><span data-stu-id="bebe0-126">Undeclare Record</span></span>
    
  
  - <span data-ttu-id="bebe0-127">Listenelement hinzufügen</span><span class="sxs-lookup"><span data-stu-id="bebe0-127">Add List Item</span></span> 
    
  
  - <span data-ttu-id="bebe0-128">Übergeordnete Listenelementberechtigungen erben</span><span class="sxs-lookup"><span data-stu-id="bebe0-128">Inherit List Item Parent Permissions</span></span>
    
  
  - <span data-ttu-id="bebe0-129">Listenelementberechtigungen entfernen</span><span class="sxs-lookup"><span data-stu-id="bebe0-129">Remove List Item Permissions</span></span>
    
  
  - <span data-ttu-id="bebe0-130">Listenelementberechtigungen ersetzen</span><span class="sxs-lookup"><span data-stu-id="bebe0-130">Replace List Item Permissions</span></span>
    
  
  - <span data-ttu-id="bebe0-131">Vorgesetzten eines Benutzers nachschlagen</span><span class="sxs-lookup"><span data-stu-id="bebe0-131">Lookup Manager of a User</span></span>
    
  
  - <span data-ttu-id="bebe0-132">Zuweisen eines Formulars zu einer Gruppe</span><span class="sxs-lookup"><span data-stu-id="bebe0-132">Assign a Form to a Group</span></span>
    
  
  - <span data-ttu-id="bebe0-133">Aufgabe zuordnen</span><span class="sxs-lookup"><span data-stu-id="bebe0-133">Assign a To-Do Item</span></span>
    
  
  - <span data-ttu-id="bebe0-134">Sammeln von Daten von einem Benutzer</span><span class="sxs-lookup"><span data-stu-id="bebe0-134">Collect Data from a User</span></span>
    
  
  - <span data-ttu-id="bebe0-135">Starten des Genehmigungsvorgangs</span><span class="sxs-lookup"><span data-stu-id="bebe0-135">Start Approval Process</span></span>
    
  
  - <span data-ttu-id="bebe0-136">Starten des benutzerdefinierten Aufgabenvorgangs</span><span class="sxs-lookup"><span data-stu-id="bebe0-136">Start Custom Task Process</span></span>
    
  
  - <span data-ttu-id="bebe0-137">Starten des Feedbackvorgangs</span><span class="sxs-lookup"><span data-stu-id="bebe0-137">Start Feedback Process</span></span>
    
  
  - <span data-ttu-id="bebe0-138">Listenelement kopieren (SharePoint Designer 2013 unterstützt nur das Kopieren des Dokuments)</span><span class="sxs-lookup"><span data-stu-id="bebe0-138">Copy List Item (SharePoint Designer 2013 supports only the document-copying action.)</span></span>
    
  
- <span data-ttu-id="bebe0-139">Bedingungen:</span><span class="sxs-lookup"><span data-stu-id="bebe0-139">Conditions:</span></span>
    
  - <span data-ttu-id="bebe0-140">Wenn aktuelles Elementfeld dem Wert entspricht</span><span class="sxs-lookup"><span data-stu-id="bebe0-140">If current item field equals value</span></span>
    
  
  - <span data-ttu-id="bebe0-141">Überprüfen von Berechtigungsstufen für Listenelemente</span><span class="sxs-lookup"><span data-stu-id="bebe0-141">Check list item permission levels</span></span>
    
  
  - <span data-ttu-id="bebe0-142">Überprüfen von Listenelementberechtigungen</span><span class="sxs-lookup"><span data-stu-id="bebe0-142">Check list item permissions</span></span>
    
  
- <span data-ttu-id="bebe0-143">Schritte:</span><span class="sxs-lookup"><span data-stu-id="bebe0-143">Steps:</span></span>
    
  - <span data-ttu-id="bebe0-144">Identitätswechselschritt:</span><span class="sxs-lookup"><span data-stu-id="bebe0-144">Impersonation Step:</span></span>
    
  
- <span data-ttu-id="bebe0-145">Datenquellen:</span><span class="sxs-lookup"><span data-stu-id="bebe0-145">Data sources:</span></span>
    
  - <span data-ttu-id="bebe0-146">Benutzerprofilsuche</span><span class="sxs-lookup"><span data-stu-id="bebe0-146">User Profile lookup</span></span>
    
  
- <span data-ttu-id="bebe0-147">Sonstige Features:</span><span class="sxs-lookup"><span data-stu-id="bebe0-147">Other features:</span></span>
    
  - <span data-ttu-id="bebe0-148">Integration von Visio</span><span class="sxs-lookup"><span data-stu-id="bebe0-148">Visio integration</span></span>
    
  
  - <span data-ttu-id="bebe0-149">Zuordnungsspalte</span><span class="sxs-lookup"><span data-stu-id="bebe0-149">Association Column</span></span>
    
  
  - <span data-ttu-id="bebe0-150">Inhaltstypzuordnung für wiederverwendbare Workflows</span><span class="sxs-lookup"><span data-stu-id="bebe0-150">Content Type Association for reusable workflow</span></span>
    
  
  - <span data-ttu-id="bebe0-151">Feature "Berechtigungen zum Verwalten von Listen/Websites anfordern" für Listen-/Website-Workflow</span><span class="sxs-lookup"><span data-stu-id="bebe0-151">'Require Manage List/Web Permission' feature for list/site workflow</span></span>
    
  
  - <span data-ttu-id="bebe0-152">Global wiederverwendbarer Workflowtyp</span><span class="sxs-lookup"><span data-stu-id="bebe0-152">Globally reusable workflow type</span></span>
    
  
  - <span data-ttu-id="bebe0-153">Option "Workflowvisualisierung"</span><span class="sxs-lookup"><span data-stu-id="bebe0-153">Workflow visualization option</span></span>
    
  

### <a name="sharepoint-page-design-features"></a><span data-ttu-id="bebe0-154">SharePoint-Features für den Seitenentwurf</span><span class="sxs-lookup"><span data-stu-id="bebe0-154">SharePoint page-design features</span></span>
<span data-ttu-id="bebe0-155"><a name="WhatsChangedSharePointDesigner2013_PageDesignFeatures"> </a></span><span class="sxs-lookup"><span data-stu-id="bebe0-155"></span></span>

<span data-ttu-id="bebe0-156">Das folgende Feature ist in SharePoint nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="bebe0-156">The following feature is not available in SharePoint.</span></span>
  
    
    

#### <a name="design-view-and-split-view"></a><span data-ttu-id="bebe0-157">Entwurfsansicht und geteilte Ansicht</span><span class="sxs-lookup"><span data-stu-id="bebe0-157">Design view and Split view</span></span>
<span data-ttu-id="bebe0-158"><a name="WhatsChangedSharePointDesigner2013_DesignViewSplitView"> </a></span><span class="sxs-lookup"><span data-stu-id="bebe0-158"></span></span>

 <span data-ttu-id="bebe0-159">**Beschreibung der Änderung. **SharePoint Designer 2010 besitzt drei Ansichten zum Bearbeiten von HTML-Code und ASPX-Seiten: Codeansicht, Entwurfsansicht und geteilte Ansicht.</span><span class="sxs-lookup"><span data-stu-id="bebe0-159">**Description of the change.**SharePoint Designer 2010 has three views for editing HTML and ASPX pages: Code view, Design view, and Split view.</span></span> <span data-ttu-id="bebe0-160">Die Entwurfsansicht und die geteilte Ansicht werden aus SharePoint Designer 2013 entfernt.</span><span class="sxs-lookup"><span data-stu-id="bebe0-160">Design view and Split view are removed from SharePoint Designer 2013.</span></span> <span data-ttu-id="bebe0-161">Das Wegfallen der Entwurfsansicht und der geteilten Ansicht wirkt sich auf die Funktionen von SharePoint Designer 2013 aus, die zum Bearbeiten von Webparts und Gestaltungsvorlagen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="bebe0-161">The removal of Design view and Split view affects the features of SharePoint Designer 2013 that are used for editing Web Parts and master pages.</span></span> <span data-ttu-id="bebe0-162">Wenn Sie Seiten in SharePoint Designer 2013 bearbeiten, müssen Sie die Codeansicht verwenden.</span><span class="sxs-lookup"><span data-stu-id="bebe0-162">If you edit pages in SharePoint Designer 2013, you must use Code view.</span></span>
  
    
    
 <span data-ttu-id="bebe0-p106">**Änderungsgrund.** Im Vergleich zu aktuellen Versionen von Internet Explorer ist die Entwurfsansicht eine ältere Technologie, die viele neue HTML5- und CSS-Tags nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="bebe0-p106">**Reason for the change.** Compared to current versions of Internet Explorer, Design view is an older technology that does not support many new HTML5 and CSS tags.</span></span>
  
    
    
 <span data-ttu-id="bebe0-p107">**Migrationspfad.** Wenn Sie Seiten in der Codeansicht bearbeiten, können Sie **F12** drücken, um eine Vorschau der Seite im Browser anzuzeigen. Alternativ können Sie Visual Studio verwenden, um Seiten zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="bebe0-p107">**Migration path.** If you edit pages in Code view, you can press **F12** to preview the page in the browser. Alternatively, you can use Visual Studio to edit pages.</span></span>
  
    
    
<span data-ttu-id="bebe0-168">Wenn Sie Ihre Webseite visuell gestalten oder mit einer Marke versehen möchten und eine WYSIWYG-Seitenbearbeitung („What you see is what you get“) wünschen, können Sie jeden professionellen HTML-Editor, wie z. B. Microsoft Expression Web, verwenden.</span><span class="sxs-lookup"><span data-stu-id="bebe0-168">If you want to visually design or brand your site, and you want a WYSIWYG ("what you see is what you get") page-editing experience, you can use any professional HTML editor, such as Microsoft Expression Web. Then you can import your HTML files into sps15short by using the new Design Manager, which is a feature included in publishing sites, such as the Publishing Portal Site Collection site template.</span></span> <span data-ttu-id="bebe0-169">Sie können dann Ihre HTML-Dateien mit dem neuen Entwurfs-Manager in SharePoint importieren. Dieses Feature ist in Veröffentlichungswebsites, wie z. B. der Webseitenvorlage Publishing Portal Site Collection, enthalten.</span><span class="sxs-lookup"><span data-stu-id="bebe0-169">If you want to visually design or brand your site, and you want a WYSIWYG ("what you see is what you get") page-editing experience, you can use any professional HTML editor, such as Microsoft Expression Web. Then you can import your HTML files into SharePoint Server 2013 by using the new Design Manager, which is a feature included in publishing sites, such as the Publishing Portal Site Collection site template.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="bebe0-170">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="bebe0-170">Additional resources</span></span>
<span data-ttu-id="bebe0-171"><a name="WhatsChangedSharePointDesigner2013_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="bebe0-171"></span></span>


-  [<span data-ttu-id="bebe0-172">Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)</span><span class="sxs-lookup"><span data-stu-id="bebe0-172">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  
-  <span data-ttu-id="bebe0-173">
  [Unterschiede zwischen SharePoint 2010 und SharePoint 2013](http://technet.microsoft.com/de-de/library/ff607742%28v=office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="bebe0-173">[Changes from SharePoint 2010 to SharePoint](http://technet.microsoft.com/de-de/library/ff607742%28v=office.15%29.aspx)</span></span>
    
  
-  <span data-ttu-id="bebe0-174">
  [Neu in SharePoint-Workflows](http://technet.microsoft.com/de-de/library/jj219638%28v=office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="bebe0-174">[What's new in workflow in SharePoint Server 2013](http://technet.microsoft.com/de-de/library/jj219638%28v=office.15%29.aspx)</span></span>
    
  

  
    
    

