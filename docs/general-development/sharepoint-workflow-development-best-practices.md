
# <a name="sharepoint-workflow-development-best-practices"></a><span data-ttu-id="bfd0a-101">Bewährte Methoden für die SharePoint-Workflow-Entwicklung</span><span class="sxs-lookup"><span data-stu-id="bfd0a-101">SharePoint workflow development best practices</span></span>
<span data-ttu-id="bfd0a-102">Stellt eine Sammlung von bewährten Methoden für Entwickler bereit, die Visual Studio zum Erstellen von Workflows in SharePoint verwenden.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-102">Provides a collection of best practices for developers using Visual Studio to create workflows in SharePoint.</span></span>
## <a name="workflow-development-best-practices"></a><span data-ttu-id="bfd0a-103">Bewährte Methoden für die Workflowentwicklung</span><span class="sxs-lookup"><span data-stu-id="bfd0a-103">Workflow development best practices</span></span>

<span data-ttu-id="bfd0a-p101">Für die Entwicklung fehlerfreier Workflows für SharePoint ist es empfehlenswert, einige allgemeine Richtlinien oder „bewährte Methoden" zu befolgen, unabhängig davon, ob Sie SharePoint Designer 2013 oder Visual Studio 2012 für die Workflowentwicklung verwenden.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-p101">To develop error-free workflows for SharePoint, it is best to follow some general guidelines, or "best practices." This is the case whether you are using SharePoint Designer 2013 or Visual Studio 2012 for workflow development.</span></span>
  
    
    

-  [<span data-ttu-id="bfd0a-106">Apps für SharePoint, die integrierte Workflows enthalten, müssen ein Tag in der Datei workflowmanifest.xml bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-106">Apps for SharePoint that contain integrated workflows must edit a tag in the workflowmanifest.xml file</span></span>](sharepoint-workflow-development-best-practices#bkm_00)
    
  
-  [<span data-ttu-id="bfd0a-107">Wenn Sie die Aktion „In Verlaufsliste protokollieren" verwenden, sind mehr Informationen besser.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-107">When you use the Log To History List action, more information is better</span></span>](sharepoint-workflow-development-best-practices#bkm_01)
    
  
-  [<span data-ttu-id="bfd0a-108">Schreiben Sie den Wert jeder Zeichenfolge und Variable, die Sie erstellen, in die Verlaufsliste.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-108">Write the value of every string and variable that you construct to the history list</span></span>](sharepoint-workflow-development-best-practices#bkm_02)
    
  
-  [<span data-ttu-id="bfd0a-109">Geben Sie vor und nach jedem Schritt oder jeder wichtigen Arbeitseinheit im Workflow ein Ablaufverfolgungsprotokoll aus.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-109">Output a trace log before and after each step or important unit of work in the workflow</span></span>](sharepoint-workflow-development-best-practices#bkm_03)
    
  
-  [<span data-ttu-id="bfd0a-110">Stellen Sie sicher, dass die Variablen nicht Null sind und erwartete Werte enthalten.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-110">Verify that variables are non-null and contain expected values</span></span>](sharepoint-workflow-development-best-practices#bkm_04)
    
  
-  [<span data-ttu-id="bfd0a-111">Stellen Sie sicher, dass Zeichenfolgen in Textfeldern des Workflows nicht länger als 255 Zeichen sind.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-111">Ensure that strings in workflow text fields do not exceed 255 characters</span></span>](sharepoint-workflow-development-best-practices#bkm_05)
    
  
-  [<span data-ttu-id="bfd0a-112">Verwenden Sie erhöhte Berechtigungen für ein neutrales Konto bei Verwendung eines Identitätswechsels.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-112">Use elevated permissions on a neutral account when using impersonation</span></span>](sharepoint-workflow-development-best-practices#bkm_06)
    
  
-  [<span data-ttu-id="bfd0a-113">Verwenden Sie in wieder verwendbaren Workflows Zuordnungsspalten, um fehlerfreie Listenfelder sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-113">In reusable workflows, use Association columns to ensure error-free list fields</span></span>](sharepoint-workflow-development-best-practices#bkm_07)
    
  
-  [<span data-ttu-id="bfd0a-114">Workflowdesign: Modellieren eines Geschäftsprozesses in einem einzigen Workflow</span><span class="sxs-lookup"><span data-stu-id="bfd0a-114">Workflow design: Model a business process in a single workflow</span></span>](sharepoint-workflow-development-best-practices#bkm_08)
    
  
-  [<span data-ttu-id="bfd0a-115">Workflowdesign: Effektive Verwendung der Genehmigungsaktion</span><span class="sxs-lookup"><span data-stu-id="bfd0a-115">Workflow design: Using the Approval action effectively</span></span>](sharepoint-workflow-development-best-practices#bkm_09)
    
  

### <a name="apps-for-sharepoint-that-contain-integrated-workflows-must-edit-a-tag-in-the-workflowmanifestxml-file"></a><span data-ttu-id="bfd0a-116">Apps für SharePoint, die integrierte Workflows enthalten, müssen ein Tag in der Datei workflowmanifest.xml bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-116">Apps for SharePoint that contain integrated workflows must edit a tag in the workflowmanifest.xml file</span></span>
<span data-ttu-id="bfd0a-117"><a name="bkm_00"> </a></span><span class="sxs-lookup"><span data-stu-id="bfd0a-117"></span></span>

<span data-ttu-id="bfd0a-118">SharePoint-Add-Ins mit integrierten Workflows (die Listen im übergeordneten Web zugeordnet sein können) werden von normalen Workflow-Apps unterschieden, indem das folgende Tag in der Datei  `workflowmanifest.xml` im App-Paket in **true** geändert wird:</span><span class="sxs-lookup"><span data-stu-id="bfd0a-118">SharePoint Add-ins that contain integrated workflows (which can be associated with lists on the parent web) are differentiated from normal workflow apps by changing the following tag to **true** in the `workflowmanifest.xml` file in the app package:</span></span>
  
    
    

```XML

<SPIntegratedWorkflow xmlns="http://schemas.microsoft.com/sharepoint/2014/app/integratedworkflow">
    <IntegratedApp>true</IntegratedApp>
</SPIntegratedWorkflow>

```


### <a name="when-you-use-the-log-to-history-list-action-more-information-is-better"></a><span data-ttu-id="bfd0a-119">Wenn Sie die Aktion „In Verlaufsliste protokollieren" verwenden, sind mehr Informationen besser.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-119">When you use the Log To History List action, more information is better</span></span>
<span data-ttu-id="bfd0a-120"><a name="bkm_01"> </a></span><span class="sxs-lookup"><span data-stu-id="bfd0a-120"></span></span>

<span data-ttu-id="bfd0a-p102">Die Aktion **In Verlaufsliste protokollieren** (oder die Klasse [LogToHistoryListActivity](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.LogToHistoryListActivity.aspx) bei Verwendung von Visual Studio) ermöglicht Ihnen das Aufzeichnen von Informationen dazu, was ein Workflow zu einem bestimmten Punkt im Lebenszyklus des Workflows ausgeführt hat. Damit wird sie zu einem der wichtigsten Tools für die Problembehandlung, das Ihnen zur Verfügung steht. Je mehr Informationen Sie an wichtigen Punkten des Workflows bereitstellen, umso einfacher ist es, unerwartete Ereignisse zu behandeln.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-p102">The **Log To History List** action (or [LogToHistoryListActivity](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.LogToHistoryListActivity.aspx) class if you are using Visual Studio) lets you record information about what a workflow has done at a given point in the workflow's lifecycle. This makes it one of the most important troubleshooting tools you have. The more information you provide at important points in the workflow, the easier it is to troubleshoot unexpected events.</span></span>
  
    
    
<span data-ttu-id="bfd0a-124">Weitere Informationen erhalten Sie unter den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="bfd0a-124">For more information, see the following:</span></span> 
  
    
    

-  [<span data-ttu-id="bfd0a-125">Workflowaktionen in SharePoint Designer 2010: eine Kurzübersicht</span><span class="sxs-lookup"><span data-stu-id="bfd0a-125">Workflow actions in SharePoint Designer 2010: A quick reference guide</span></span>](https://support.office.com/en-us/article/Workflow-actions-in-SharePoint-Designer-2010-A-quick-reference-guide-5a7ad276-0ed7-49b0-b652-e56a77dd96c6?CorrelationId=9cff0340-2d05-4878-b3a0-aecb30b862ed&ui=en-US&rs=en-US&ad=US&ocmsassetID=HA010376961)
    
  
-  <span data-ttu-id="bfd0a-126">[LogToHistoryListActivity](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.LogToHistoryListActivity.aspx) -Klasse</span><span class="sxs-lookup"><span data-stu-id="bfd0a-126">[LogToHistoryListActivity](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.LogToHistoryListActivity.aspx) class</span></span>
    
  
-  [<span data-ttu-id="bfd0a-127">Gewusst wie: Protokollieren in die Verlaufsliste von einer Workflowaktivität</span><span class="sxs-lookup"><span data-stu-id="bfd0a-127">How to: Log to the History List from a Workflow Activity</span></span>](http://msdn.microsoft.com/en-us/library/ff798337.aspx)
    
  
-  [<span data-ttu-id="bfd0a-128">Verwenden der SharePoint-Workflowaktion „In Verlaufsliste protokollieren" für das Debugging</span><span class="sxs-lookup"><span data-stu-id="bfd0a-128">Using the Log to History List SharePoint workflow action for debugging</span></span>](http://www.documentmanagementworkflowinfo.com/sample-sharepoint-workflows/use-log-to-history-list-sharepoint-designer-workflow-action-debug)
    
  

### <a name="write-the-value-of-every-string-and-variable-that-you-construct-to-the-history-list"></a><span data-ttu-id="bfd0a-129">Schreiben Sie den Wert jeder Zeichenfolge und Variable, die Sie erstellen, in die Verlaufsliste.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-129">Write the value of every string and variable that you construct to the history list</span></span>
<span data-ttu-id="bfd0a-130"><a name="bkm_02"> </a></span><span class="sxs-lookup"><span data-stu-id="bfd0a-130"></span></span>

<span data-ttu-id="bfd0a-131">Das Debuggen von Workflows, die mit SharePoint Designer erstellt wurden, ist viel einfacher, wenn Sie Zeichenfolgen und Variablen in mithilfe der Aktion **Log to History List** in die Verlaufsliste schreiben.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-131">Debugging workflows that were created using SharePoint Designer is much easier if you write strings and variables to the history list by using the **Log to History List** action.</span></span>
  
    
    
<span data-ttu-id="bfd0a-132">Weitere Informationen erhalten Sie unter den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="bfd0a-132">For more information, see the following:</span></span> 
  
    
    

-  [<span data-ttu-id="bfd0a-133">Workflowaktionen in SharePoint Designer 2010: eine Kurzübersicht</span><span class="sxs-lookup"><span data-stu-id="bfd0a-133">Workflow actions in SharePoint Designer 2010: A quick reference guide</span></span>](https://support.office.com/en-us/article/Workflow-actions-in-SharePoint-Designer-2010-A-quick-reference-guide-5a7ad276-0ed7-49b0-b652-e56a77dd96c6?CorrelationId=9cff0340-2d05-4878-b3a0-aecb30b862ed&ui=en-US&rs=en-US&ad=US&ocmsassetID=HA010376961)
    
  
-  <span data-ttu-id="bfd0a-134">[LogToHistoryListActivity](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.LogToHistoryListActivity.aspx) -Klasse</span><span class="sxs-lookup"><span data-stu-id="bfd0a-134">[LogToHistoryListActivity](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.LogToHistoryListActivity.aspx) class</span></span>
    
  
-  [<span data-ttu-id="bfd0a-135">Gewusst wie: Protokollieren in die Verlaufsliste von einer Workflowaktivität</span><span class="sxs-lookup"><span data-stu-id="bfd0a-135">How to: Log to the History List from a Workflow Activity</span></span>](http://msdn.microsoft.com/en-us/library/ff798337.aspx)
    
  
-  [<span data-ttu-id="bfd0a-136">Verwenden der SharePoint-Workflowaktion „In Verlaufsliste protokollieren" für das Debugging</span><span class="sxs-lookup"><span data-stu-id="bfd0a-136">Using the Log to History List SharePoint workflow action for debugging</span></span>](http://www.documentmanagementworkflowinfo.com/sample-sharepoint-workflows/use-log-to-history-list-sharepoint-designer-workflow-action-debug)
    
  

### <a name="output-a-trace-log-before-and-after-each-step-or-important-unit-of-work-in-the-workflow"></a><span data-ttu-id="bfd0a-137">Geben Sie vor und nach jedem Schritt oder jeder wichtigen Arbeitseinheit im Workflow ein Ablaufverfolgungsprotokoll aus.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-137">Output a trace log before and after each step or important unit of work in the workflow</span></span>
<span data-ttu-id="bfd0a-138"><a name="bkm_03"> </a></span><span class="sxs-lookup"><span data-stu-id="bfd0a-138"></span></span>

<span data-ttu-id="bfd0a-p103">Zur Unterstützung von Debuggingworkflows ist es wichtig, dass Sie vor und nach jeder wichtigen Arbeitseinheit aussagekräftige Informationen erfassen. Diese Informationen sollten an Ablaufverfolgungsprotokolle übermittelt werden. Hier finden Sie weitere Informationen:</span><span class="sxs-lookup"><span data-stu-id="bfd0a-p103">To assist with debugging workflows, it is important that you capture meaningful information prior to and following each significant unit of work; this information should be committed to trace logs. For more information, see the following:</span></span>
  
    
    

-  [<span data-ttu-id="bfd0a-141">Schreiben an das Ablaufverfolgungsprotokoll</span><span class="sxs-lookup"><span data-stu-id="bfd0a-141">Writing to the Trace Log</span></span>](http://msdn.microsoft.com/en-us/library/aa979595.aspx)
    
  
-  [<span data-ttu-id="bfd0a-142">Verwenden von Ereignis- und Ablaufverfolgungsprotokollen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="bfd0a-142">Using Event and Trace Logs in SharePoint</span></span>](http://msdn.microsoft.com/en-us/library/ff647362.aspx)
    
  

### <a name="verify-that-variables-are-non-null-and-contain-expected-values"></a><span data-ttu-id="bfd0a-143">Stellen Sie sicher, dass die Variablen nicht Null sind und erwartete Werte enthalten.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-143">Verify that variables are non-null and contain expected values</span></span>
<span data-ttu-id="bfd0a-144"><a name="bkm_04"> </a></span><span class="sxs-lookup"><span data-stu-id="bfd0a-144"></span></span>

<span data-ttu-id="bfd0a-p104">Stellen Sie vor der Verwendung von Variablen in Ihren Workflows sicher, dass keine Null-Variablen vorhanden sind. Stellen Sie außerdem sicher, dass Variablen erwartete Werte enthalten und dem richtigen Datentyp entsprechen. Weitere Informationen finden Sie unter  [Variablen und Argumente](http://msdn.microsoft.com/en-us/library/dd489456.aspx).</span><span class="sxs-lookup"><span data-stu-id="bfd0a-p104">Before using variables in your workflows, ensure there are no null variables. Also, ensure that variables contain expected values and are of the correct data type. For more information, see  [Variables and Arguments](http://msdn.microsoft.com/en-us/library/dd489456.aspx).</span></span>
  
    
    

### <a name="ensure-that-strings-in-workflow-text-fields-do-not-exceed-255-characters"></a><span data-ttu-id="bfd0a-148">Stellen Sie sicher, dass Zeichenfolgen in Textfeldern des Workflows nicht länger als 255 Zeichen sind.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-148">Ensure that strings in workflow text fields do not exceed 255 characters</span></span>
<span data-ttu-id="bfd0a-149"><a name="bkm_05"> </a></span><span class="sxs-lookup"><span data-stu-id="bfd0a-149"></span></span>

<span data-ttu-id="bfd0a-p105">Die maximale zulässige Länge für Zeichenfolgen in Textfeldern von Workflows beträgt 255 Zeichen. Wenn Sie das Textfeld so festlegen, dass dieser Grenzwert überschritten wird, wird dessen Inhalt auf 255 Zeichen abgeschnitten.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-p105">The maximum allowable length for strings in workflow text fields is 255 characters. If you set your text field to exceed this limit, its content will be truncated to 255 characters.</span></span>
  
    
    

### <a name="use-elevated-permissions-on-a-neutral-account-when-using-impersonation"></a><span data-ttu-id="bfd0a-152">Verwenden Sie erhöhte Berechtigungen für ein neutrales Konto bei Verwendung eines Identitätswechsels.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-152">Use elevated permissions on a neutral account when using impersonation</span></span>
<span data-ttu-id="bfd0a-153"><a name="bkm_06"> </a></span><span class="sxs-lookup"><span data-stu-id="bfd0a-153"></span></span>

<span data-ttu-id="bfd0a-p106">Wenn Sie Identitätswechselschritte in einem Workflow verwenden, sollten Sie den Workflow mit einem neutralen Konto (d. h. einem Konto, das nicht an einen bestimmten Benutzer gebunden ist) erstellen. Dadurch wird verhindert, dass Ihre Workflows unterbrochen werden, wenn das Konto des Autors aus irgendeinem Grund veraltet ist.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-p106">When using impersonation steps in a workflow, you should author the workflow using a neutral account (that is, an account that is not tied to a specific user). This prevents your workflows from breaking if the author's account becomes obsolete for any reason.</span></span>
  
    
    
<span data-ttu-id="bfd0a-156">Weitere Informationen finden Sie unter  [Erstellen eines Workflows mit erweiterten Berechtigungen mithilfe der SharePoint-Workflow-Plattform](create-a-workflow-with-elevated-permissions-by-using-the-sharepoint-workflo).</span><span class="sxs-lookup"><span data-stu-id="bfd0a-156">For more information, see  [Create a workflow with elevated permissions by using the SharePoint Workflow platform](create-a-workflow-with-elevated-permissions-by-using-the-sharepoint-workflo).</span></span>
  
    
    

### <a name="in-reusable-workflows-use-association-columns-to-ensure-error-free-list-fields"></a><span data-ttu-id="bfd0a-157">Verwenden Sie in wieder verwendbaren Workflows Zuordnungsspalten, um fehlerfreie Listenfelder sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-157">In reusable workflows, use Association columns to ensure error-free list fields</span></span>
<span data-ttu-id="bfd0a-158"><a name="bkm_07"> </a></span><span class="sxs-lookup"><span data-stu-id="bfd0a-158"></span></span>

<span data-ttu-id="bfd0a-p107">Bei der Erstellung eines wieder verwendbaren Workflows, der darauf basiert, dass seine Liste über ein bestimmtes Feld verfügt, können Sie (1) den Workflow auf einen Inhaltstyp mit dem angegebenen Feld beschränken oder (2) das Feld zu einer Zuordnungsspalte machen. Option 2 wird empfohlen, da es möglich ist, dass sich ein Inhaltstyp ändert und dazu führt, dass der Workflow unterbrochen wird.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-p107">If you create a reusable workflow that relies on its list having a specific field, you may either (1) restrict the workflow to a content type that has the specified field, or (2) make the field an association column. Option 2 is recommended because it's possible that a content type will change and cause the workflow to break.</span></span>
  
    
    

### <a name="workflow-design-model-a-business-process-in-a-single-workflow"></a><span data-ttu-id="bfd0a-161">Workflowdesign: Modellieren eines Geschäftsprozesses in einem einzigen Workflow</span><span class="sxs-lookup"><span data-stu-id="bfd0a-161">Workflow design: Model a business process in a single workflow</span></span>
<span data-ttu-id="bfd0a-162"><a name="bkm_08"> </a></span><span class="sxs-lookup"><span data-stu-id="bfd0a-162"></span></span>

<span data-ttu-id="bfd0a-163">Wenn möglich, ist es viel besser, einen Geschäftsprozess in einem einzigen Workflow zu modellieren als die Workflowlogik in mehrere kleinere Workflows zu unterteilen.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-163">Where possible, it is much better to model a business process in a single workflow than to break the workflow logic into several smaller workflows.</span></span>
  
    
    

### <a name="workflow-design-using-the-approval-action-effectively"></a><span data-ttu-id="bfd0a-164">Workflowdesign: Effektive Verwendung der Genehmigungsaktion</span><span class="sxs-lookup"><span data-stu-id="bfd0a-164">Workflow design: Using the Approval action effectively</span></span>
<span data-ttu-id="bfd0a-165"><a name="bkm_09"> </a></span><span class="sxs-lookup"><span data-stu-id="bfd0a-165"></span></span>

<span data-ttu-id="bfd0a-166">Wenn möglich, ist es statt der Erstellung mehrerer **Approval**-Aktionen effektiver, das **Stages**-Feature innerhalb einer **Approval**-Aktion zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="bfd0a-166">Where possible, instead of creating multiple **Approval** actions, it is more effective to use the **Stages** feature within an **Approval** action.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="bfd0a-167">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="bfd0a-167">Additional resources</span></span>
<span data-ttu-id="bfd0a-168"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="bfd0a-168"></span></span>


-  [<span data-ttu-id="bfd0a-169">Workflows in SharePoint</span><span class="sxs-lookup"><span data-stu-id="bfd0a-169">Workflows in SharePoint</span></span>](workflows-in-sharepoint)
    
  
-  [<span data-ttu-id="bfd0a-170">Grundlegendes zu SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="bfd0a-170">SharePoint workflow fundamentals</span></span>](sharepoint-workflow-fundamentals)
    
  
-  [<span data-ttu-id="bfd0a-171">Entwickeln von SharePoint-Workflows mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bfd0a-171">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio)
    
  

