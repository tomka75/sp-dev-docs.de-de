---
title: Allgemeine Fehlermeldungen bei der SharePoint-Workflowentwicklung
ms.prod: SHAREPOINT
ms.assetid: e9bf6878-c722-4b1f-b5b5-b302ae0ea4da
ms.openlocfilehash: bc5feb68bc2959cdc842a88c9e78faa26730f5f7
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2017
---
# <a name="common-error-messages-in-sharepoint-workflow-development"></a><span data-ttu-id="e8035-102">Allgemeine Fehlermeldungen bei der SharePoint-Workflowentwicklung</span><span class="sxs-lookup"><span data-stu-id="e8035-102">Common error messages in SharePoint workflow development</span></span>
<span data-ttu-id="e8035-103">Eine Auflistung der häufigsten Fehlermeldungen, die bei der Entwicklung von SharePoint-Workflows auftreten können sowie Anleitungen zur Lösung des zugrunde liegenden Problems.</span><span class="sxs-lookup"><span data-stu-id="e8035-103">A listing of common error messages that you might encounter while developing SharePoint workflows and guidance for solving the underlying problem.</span></span>
## <a name="common-sharepoint-workflow-errors"></a><span data-ttu-id="e8035-104">Häufige Fehler bei SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="e8035-104">Common SharePoint workflow errors</span></span>

<span data-ttu-id="e8035-105">Obwohl diese Liste nicht jeden erdenklichen Fehler enthält, der möglicherweise beim Entwickeln von SharePoint-Workflows auftreten kann, sind dennoch die am wahrscheinlichsten auftretenden Fehler enthalten.</span><span class="sxs-lookup"><span data-stu-id="e8035-105">Although this list doesn't cover every possible error you may encounter when developing SharePoint workflows, it does cover those that you are most likely to face.</span></span>
  
    
    

-  [<span data-ttu-id="e8035-106">Timeout beim Warten auf den Abschluss der Sandkasten-Codeausführungsanforderung im Arbeitsprozess.</span><span class="sxs-lookup"><span data-stu-id="e8035-106">Timeout while waiting for sandboxed code execution request to complete within the worker process</span></span>](#bkmk_error01)
    
  
-  [<span data-ttu-id="e8035-107">Timeout beim Warten auf den Abschluss der Anforderung in der Sandkasten-Anwendungsdomäne.</span><span class="sxs-lookup"><span data-stu-id="e8035-107">Timeout while waiting for request to complete within the sandboxed appdomain</span></span>](#bkmk_error02)
    
  
-  [<span data-ttu-id="e8035-108">Der Arbeitsprozess, der diese Anforderung verarbeitet, wurde beendet, weil er die Ressource {0} überschritten hat.</span><span class="sxs-lookup"><span data-stu-id="e8035-108">The worker process handling this request was ended because it exceeded the resource {0}</span></span>](#bkmk_error03)
    
  
-  [<span data-ttu-id="e8035-109">Dieser Workflow konnte nicht ausgeführt werden, da eine Sandkastenlösung einen Fehler erkannt hat.</span><span class="sxs-lookup"><span data-stu-id="e8035-109">This workflow could not run because a sandboxed solution encountered an error</span></span>](#bkmk_error04)
    
  
-  [<span data-ttu-id="e8035-110">Dieser Workflow konnte nicht ausgeführt werden, da ein Fehler im Sandkasten aufgetreten ist: Es konnte kein Prozess aus dem Prozesspool abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="e8035-110">This workflow could not run because the sandbox failed: Could not get a process from the process pool</span></span>](#bkmk_error05)
    
  
-  [<span data-ttu-id="e8035-111">Dieser Workflow konnte nicht ausgeführt werden, da ein Fehler im Sandkasten aufgetreten ist: Der Sandkasten-Codearbeitsprozess wurde unerwartet beendet.</span><span class="sxs-lookup"><span data-stu-id="e8035-111">This workflow could not run because the sandbox failed: The sandboxed code worker process exited unexpectedly</span></span>](#bkmk_error06)
    
  
-  [<span data-ttu-id="e8035-112">Die E-Mail konnte nicht gesendet werden. Stellen Sie sicher, dass die Einstellungen für ausgehende E-Mails für den Server ordnungsgemäß konfiguriert sind.</span><span class="sxs-lookup"><span data-stu-id="e8035-112">The e-mail message cannot be sent. Make sure the outgoing e-mail settings for the server are configured correctly</span></span>](#bkmk_error07)
    
  
-  [<span data-ttu-id="e8035-113">Das Element konnte vom Workflow nicht aktualisiert werden, möglicherweise weil mindestens eine Spalte des Elements einen anderen Informationstyp erfordert.</span><span class="sxs-lookup"><span data-stu-id="e8035-113">The workflow could not update the item, possibly because one or more columns for the item require a different type of information</span></span>](#bkmk_error08)
    
  
-  [<span data-ttu-id="e8035-114">Fehler des Workflowvorgangs, weil die Workflowsuche kein übereinstimmendes Element finden konnte.</span><span class="sxs-lookup"><span data-stu-id="e8035-114">The workflow operation failed because the workflow lookup found no matching item</span></span>](#bkmk_error09)
    
  
-  [<span data-ttu-id="e8035-115">Das Listenelement konnte vom Workflow nicht erstellt werden, weil der Dateiname fehlt oder ungültig ist.</span><span class="sxs-lookup"><span data-stu-id="e8035-115">The workflow could not create the list item because the file name is either missing or invalid</span></span>](#bkmk_error10)
    
  
-  [<span data-ttu-id="e8035-116">Koersionsfehler: Die Eingabenachschlagedaten können nicht in den angeforderten Typ umgewandelt werden.</span><span class="sxs-lookup"><span data-stu-id="e8035-116">Coercion Failed: Unable to transform the input lookup data into the requested type</span></span>](#bkmk_error11)
    
  
-  [<span data-ttu-id="e8035-117">Fehler des Workflowvorgangs, weil das Dokument für diese Aktion ausgecheckt sein muss.</span><span class="sxs-lookup"><span data-stu-id="e8035-117">The workflow operation failed because the action requires the document to be checked out</span></span>](#bkmk_error12)
    
  
-  [<span data-ttu-id="e8035-118">Fehler beim Kompilieren des Workflows. Die Workflowdateien wurden gespeichert, können aber nicht ausgeführt werden. Unerwarteter Fehler auf dem Server beim Zuweisen des Workflows.</span><span class="sxs-lookup"><span data-stu-id="e8035-118">Errors were found when compiling the workflow. The workflow files were saved but cannot be run. Unexpected error on server associating the workflow</span></span>](#bkmk_error13)
    
  

### <a name="timeout-while-waiting-for-sandboxed-code-execution-request-to-complete-within-the-worker-process"></a><span data-ttu-id="e8035-119">Timeout beim Warten auf den Abschluss der Sandkasten-Codeausführungsanforderung im Arbeitsprozess.</span><span class="sxs-lookup"><span data-stu-id="e8035-119">Timeout while waiting for sandboxed code execution request to complete within the worker process</span></span>
<span data-ttu-id="e8035-120"><a name="bkmk_error01"> </a></span><span class="sxs-lookup"><span data-stu-id="e8035-120"></span></span>

<span data-ttu-id="e8035-121">Dasselbe Problem und dieselbe Lösung wie beim nachfolgenden Element, "Timeout beim Warten auf den Abschluss der Anforderung in der Sandkasten-Anwendungsdomäne."</span><span class="sxs-lookup"><span data-stu-id="e8035-121">Same issue and same solution as the item below, "Timeout while waiting for request to complete within the sandboxed appdomain".</span></span>
  
    
    

### <a name="timeout-while-waiting-for-request-to-complete-within-the-sandboxed-appdomain"></a><span data-ttu-id="e8035-122">Timeout beim Warten auf den Abschluss der Anforderung in der Sandkasten-Anwendungsdomäne.</span><span class="sxs-lookup"><span data-stu-id="e8035-122">Timeout while waiting for request to complete within the sandboxed appdomain</span></span>
<span data-ttu-id="e8035-123"><a name="bkmk_error02"> </a></span><span class="sxs-lookup"><span data-stu-id="e8035-123"></span></span>

<span data-ttu-id="e8035-p101">Beide Fehler ergeben sich aus demselben Problem. Der Standardtimeout zum Ausführen der Workflowaktion wurde überschritten. Der Standardtimeout beträgt 30 Sekunden.</span><span class="sxs-lookup"><span data-stu-id="e8035-p101">Both of these errors result from the same issue—exceeding the default timeout period for the workflow action to execute. The default timeout period is 30 seconds.</span></span>
  
    
    
<span data-ttu-id="e8035-p102">Sie können den Timeoutwert für lokale Installationen, aber nicht für SharePoint Online-Installationen ändern. Damit Sie diesen Fehler nicht in SharePoint Online-Installationen erhalten, müssen Sie den Code ändern, um Aktionen in Arbeitsprozessen oder der Anwendungsdomäne auf weniger als 30 Sekunden zu begrenzen.</span><span class="sxs-lookup"><span data-stu-id="e8035-p102">You can change the timeout value in on-premises installations, but you can't change it in SharePoint Online installations. To avoid getting this error in SharePoint Online installations, you must modify your code to limit actions in the worker process or appdomain to fewer than 30 seconds.</span></span>
  
    
    
<span data-ttu-id="e8035-p103">Führen Sie den folgenden Windows PowerShell-Befehl aus, um das Timeout in Ihrer lokalen Installation zu ändern. Beachten Sie, dass der Timeout im Beispielcode auf 60 Sekunden zurückgesetzt wird, aber Sie können einen anderen Wert verwenden.</span><span class="sxs-lookup"><span data-stu-id="e8035-p103">To modify the timeout period in your on-premises installation, execute the following Windows PowerShell command. Note that the example code resets the timeout to 60 seconds, but you can use another value.</span></span>
  
    
    



```

Add-pssnapin microsoft.sharepoint.powershell
   $userCodeSvc = [Microsoft.SharePoint.Administration.SPUserCodeService]::Local
   #change to 60 second timeout
   $userCodeSvc.WorkerProcessExecutionTimeout = 60 
   $userCodeSvc.Update()
```


### <a name="the-worker-process-handling-this-request-was-ended-because-it-exceeded-the-resource-0"></a><span data-ttu-id="e8035-130">Der Arbeitsprozess, der diese Anforderung verarbeitet, wurde beendet, weil er die Ressource {0} überschritten hat.</span><span class="sxs-lookup"><span data-stu-id="e8035-130">The worker process handling this request was ended because it exceeded the resource {0}</span></span>
<span data-ttu-id="e8035-131"><a name="bkmk_error03"> </a></span><span class="sxs-lookup"><span data-stu-id="e8035-131"></span></span>

<span data-ttu-id="e8035-p104">In der Fehlerzeichenfolge ist der Wert von  `{0}` ein Platzhalter für eine bestimmte Ressource, deren Schwellenwert überschritten wurde. Um das Problem zu verringern, sollten Sie Ihren Code ändern, damit der Ressourcenschwellenwert nicht überschritten wird. Diese Ressourcenwerte sind unter [Einschränkungen beim Ressourceneinsatz in Sandkastenlösungen](http://msdn.microsoft.com/en-us/library/gg615462%28v=office.14%29.aspx) dokumentiert.</span><span class="sxs-lookup"><span data-stu-id="e8035-p104">In the error string, the value of  `{0}` is a placeholder for the specific resource whose threshold has been exceeded. To alleviate this problem, you should modify your code so that it does not exceed the resource threshold. These resource values are documented in [Resource Usage Limits on Sandboxed Solutions in SharePoint 2010](http://msdn.microsoft.com/en-us/library/gg615462%28v=office.14%29.aspx).</span></span>
  
    
    

### <a name="this-workflow-could-not-run-because-a-sandboxed-solution-encountered-an-error"></a><span data-ttu-id="e8035-135">Dieser Workflow konnte nicht ausgeführt werden, da eine Sandkastenlösung einen Fehler erkannt hat.</span><span class="sxs-lookup"><span data-stu-id="e8035-135">This workflow could not run because a sandboxed solution encountered an error</span></span>
<span data-ttu-id="e8035-136"><a name="bkmk_error04"> </a></span><span class="sxs-lookup"><span data-stu-id="e8035-136"></span></span>

<span data-ttu-id="e8035-p105">Der Workflowcode hat eine unbehandelte Ausnahme ausgelöst. Das Beheben dieses Fehlers erfordert das Debuggen und Bereinigen des Sandkastencodes.</span><span class="sxs-lookup"><span data-stu-id="e8035-p105">The workflow code threw an unhandled exception. Resolving this error requires debugging and revising your sandboxed code.</span></span>
  
    
    

### <a name="this-workflow-could-not-run-because-the-sandbox-failed-could-not-get-a-process-from-the-process-pool"></a><span data-ttu-id="e8035-139">Dieser Workflow konnte nicht ausgeführt werden, da ein Fehler im Sandkasten aufgetreten ist: Es konnte kein Prozess aus dem Prozesspool abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="e8035-139">This workflow could not run because the sandbox failed: Could not get a process from the process pool</span></span>
<span data-ttu-id="e8035-140"><a name="bkmk_error05"> </a></span><span class="sxs-lookup"><span data-stu-id="e8035-140"></span></span>

<span data-ttu-id="e8035-p106">Es ist ein Fehler in Ihrer Sandkastenkonfiguration aufgetreten. Informationen zum Konfigurieren einer Sandkastenlösung finden Sie unter  [Sandkastenlösungen in SharePoint](http://msdn.microsoft.com/en-us/library/ee536577%28v=office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="e8035-p106">There is an error in your sandbox configuration. For information about configuring a sandboxed solution, see  [Sandboxed Solutions in SharePoint](http://msdn.microsoft.com/en-us/library/ee536577%28v=office.14%29.aspx).</span></span>
  
    
    

### <a name="this-workflow-could-not-run-because-the-sandbox-failed-the-sandboxed-code-worker-process-exited-unexpectedly"></a><span data-ttu-id="e8035-143">Dieser Workflow konnte nicht ausgeführt werden, da ein Fehler im Sandkasten aufgetreten ist: Der Sandkasten-Codearbeitsprozess wurde unerwartet beendet.</span><span class="sxs-lookup"><span data-stu-id="e8035-143">This workflow could not run because the sandbox failed: The sandboxed code worker process exited unexpectedly</span></span>
<span data-ttu-id="e8035-144"><a name="bkmk_error06"> </a></span><span class="sxs-lookup"><span data-stu-id="e8035-144"></span></span>

<span data-ttu-id="e8035-p107">Es ist ein Fehler in Ihrer Sandkastenkonfiguration aufgetreten. Informationen zum Konfigurieren einer Sandkastenlösung finden Sie unter  [Sandkastenlösungen in SharePoint](http://msdn.microsoft.com/en-us/library/ee536577%28v=office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="e8035-p107">There is an error in your sandbox configuration. For information about configuring a sandboxed solution, see  [Sandboxed Solutions in SharePoint](http://msdn.microsoft.com/en-us/library/ee536577%28v=office.14%29.aspx).</span></span>
  
    
    

### <a name="the-e-mail-message-cannot-be-sent-make-sure-the-outgoing-e-mail-settings-for-the-server-are-configured-correctly"></a><span data-ttu-id="e8035-p108">Die E-Mail konnte nicht gesendet werden. Stellen Sie sicher, dass die Einstellungen für ausgehende E-Mails für den Server ordnungsgemäß konfiguriert sind.</span><span class="sxs-lookup"><span data-stu-id="e8035-p108">The e-mail message cannot be sent. Make sure the outgoing e-mail settings for the server are configured correctly</span></span>
<span data-ttu-id="e8035-149"><a name="bkmk_error07"> </a></span><span class="sxs-lookup"><span data-stu-id="e8035-149"></span></span>

<span data-ttu-id="e8035-p109">Bei der Behandlung von E-Mail-Problemen sind zwei Fakten zu berücksichtigen. Stellen Sie sowohl für lokale als auch für SharePoint Online-Installationen sicher, dass alle Adressen in den Zeilen **An:** und **Cc:** gültige E-Mail-Adressen sind. Stellen Sie bei lokalen Installationen sicher, dass die E-Mail-Einstellungen auf dem Server ordnungsgemäß konfiguriert sind.</span><span class="sxs-lookup"><span data-stu-id="e8035-p109">There are two issues of note to consider when troubleshooting email issues. In both on-premises and SharePoint Online installations, ensure that all addresses on the **To:** and **Cc:** lines are valid email addresses. In on-premises installations, ensure that email settings on the server are configured correctly.</span></span>
  
    
    
<span data-ttu-id="e8035-153">Überprüfen Sie Folgendes, um sicherzustellen, dass Sie die ein- und ausgehenden E-Mails ordnungsgemäß konfiguriert haben.</span><span class="sxs-lookup"><span data-stu-id="e8035-153">Review the following to ensure that you have correctly configured incoming and outgoing emails.</span></span>
  
    
    

-  [<span data-ttu-id="e8035-154">Bereitstellungshandbuch für Microsoft SharePoint</span><span class="sxs-lookup"><span data-stu-id="e8035-154">Deployment guide for Microsoft SharePoint</span></span>](http://download.microsoft.com/download/1/F/6/1F6D3BE4-1174-4320-A1D1-C0E2681CCCF3/Deployment-guide-for-SharePoint.pdf)
    
  
-  [<span data-ttu-id="e8035-155">Konfigurieren von ein- und ausgehenden E-Mails in SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="e8035-155">How to configure Incoming and Outgoing emails in SharePoint Server</span></span>](http://blogs.msdn.com/b/pareshg/archive/2010/04/23/how-to-configure-incoming-and-outgoing-emails-in-sharepoint-server-2010.aspx)
    
  

### <a name="the-workflow-could-not-update-the-item-possibly-because-one-or-more-columns-for-the-item-require-a-different-type-of-information"></a><span data-ttu-id="e8035-156">Das Element konnte vom Workflow nicht aktualisiert werden, möglicherweise weil mindestens eine Spalte des Elements einen anderen Informationstyp erfordert.</span><span class="sxs-lookup"><span data-stu-id="e8035-156">The workflow could not update the item, possibly because one or more columns for the item require a different type of information</span></span>
<span data-ttu-id="e8035-157"><a name="bkmk_error08"> </a></span><span class="sxs-lookup"><span data-stu-id="e8035-157"></span></span>

<span data-ttu-id="e8035-158">Dieser Fehler ergibt sich häufig in einer von zwei Situationen:</span><span class="sxs-lookup"><span data-stu-id="e8035-158">This error commonly results from one of two situations:</span></span>
  
    
    

- <span data-ttu-id="e8035-p110">Eines der Listenfelder wurde entfernt oder geändert, aber der Workflow wurde nicht aktualisiert, um die Änderung zu berücksichtigen. Daher versucht er einen Wert für das alte Feld festzulegen. Prüfen Sie alle Aktionen **Listenelement aktualisieren** in Ihrem Workflow, und stellen Sie sicher, dass diese geeignete Werte für Felder festlegen. Prüfen Sie zudem, dass diese Felder in der Liste vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="e8035-p110">One of the list fields was removed or changed, but the workflow was not updated to account for the change and is therefore trying to set a value for the old field. You should check all **Update List Item** actions in your workflow and make sure they are setting appropriate values for fields and that those fields exist on the list.</span></span>
    
  
- <span data-ttu-id="e8035-p111">Es ist ein Datentypfehler aufgetreten, bei dem der Workflow versucht, einen Wert in einem Feld des Listenelements mit einem falschen Datentyp festzulegen. Bestätigen Sie, dass der Vorgang **Feld zurückgeben als** der Suche den richtigen Datentyp aufweist.</span><span class="sxs-lookup"><span data-stu-id="e8035-p111">There is a data type error wherein the workflow is trying to set a value in a field in the list item using the wrong data type. You should confirm that the **Return Field As** operation in their lookup is of the correct data type.</span></span>
    
  

### <a name="the-workflow-operation-failed-because-the-workflow-lookup-found-no-matching-item"></a><span data-ttu-id="e8035-163">Fehler des Workflowvorgangs, weil die Workflowsuche kein übereinstimmendes Element finden konnte.</span><span class="sxs-lookup"><span data-stu-id="e8035-163">The workflow operation failed because the workflow lookup found no matching item</span></span>
<span data-ttu-id="e8035-164"><a name="bkmk_error09"> </a></span><span class="sxs-lookup"><span data-stu-id="e8035-164"></span></span>

<span data-ttu-id="e8035-p112">Dies weist auf einen Fehler in der Workflowlogik hin. Stellen Sie sicher, dass Sie die richtige Liste und das richtige Feld in der Suche auswählen.</span><span class="sxs-lookup"><span data-stu-id="e8035-p112">This indicates there is an error in the workflow logic. Check to ensure that you are selecting the correct list and field in your lookup.</span></span>
  
    
    

### <a name="the-workflow-could-not-create-the-list-item-because-the-file-name-is-either-missing-or-invalid"></a><span data-ttu-id="e8035-167">Das Listenelement konnte vom Workflow nicht erstellt werden, weil der Dateiname fehlt oder ungültig ist.</span><span class="sxs-lookup"><span data-stu-id="e8035-167">The workflow could not create the list item because the file name is either missing or invalid</span></span>
<span data-ttu-id="e8035-168"><a name="bkmk_error10"> </a></span><span class="sxs-lookup"><span data-stu-id="e8035-168"></span></span>

<span data-ttu-id="e8035-p113">Dies weist auf einen Fehler in der Workflowlogik hin. Stellen Sie sicher, dass der im Feld **Pfad und Name** eingegebene Dateiname gültig ist. Häufige Ursachen für ungültige Dateinamen umfassen fehlende oder falsche Dateierweiterungen oder eine Datei-/Pfadzeichenfolge, die zu lang ist und die zulässige Zeichenanzahl überschreitet.</span><span class="sxs-lookup"><span data-stu-id="e8035-p113">This indicates there is an error in the workflow logic. Ensure that the file name entered in the **Path and Name** field is a valid file name. Common reasons for a file name to be invalid include a missing or incorrect file extension or a file/path string that is too long and exceeds the allowable number of characters.</span></span>
  
    
    

### <a name="coercion-failed-unable-to-transform-the-input-lookup-data-into-the-requested-type"></a><span data-ttu-id="e8035-172">Koersionsfehler: Die Eingabenachschlagedaten können nicht in den angeforderten Typ umgewandelt werden.</span><span class="sxs-lookup"><span data-stu-id="e8035-172">Coercion Failed: Unable to transform the input lookup data into the requested type</span></span>
<span data-ttu-id="e8035-173"><a name="bkmk_error11"> </a></span><span class="sxs-lookup"><span data-stu-id="e8035-173"></span></span>

<span data-ttu-id="e8035-p114">Der Vorgang konnte die Werte nicht zwischen inkompatiblen Datentypen verteilen (z. B. die Konvertierung einer zufälligen Zeichenfolge in einen Datum/Uhrzeit-Wert). Prüfen Sie die Einstellungen für **Feld zurückgeben als** in Ihrer Suche, um sicherzustellen, dass es sich um einen gültigen Datentyp für die erwarteten Daten handelt.</span><span class="sxs-lookup"><span data-stu-id="e8035-p114">The operation failed to cast values between incompatible data types (for example, converting a random string to a Date/Time value). You should check the **Return Field As** settings in your lookup to ensure that it is a valid data type for the expected data.</span></span>
  
    
    

### <a name="the-workflow-operation-failed-because-the-action-requires-the-document-to-be-checked-out"></a><span data-ttu-id="e8035-176">Fehler des Workflowvorgangs, weil das Dokument für diese Aktion ausgecheckt sein muss.</span><span class="sxs-lookup"><span data-stu-id="e8035-176">The workflow operation failed because the action requires the document to be checked out</span></span>
<span data-ttu-id="e8035-177"><a name="bkmk_error12"> </a></span><span class="sxs-lookup"><span data-stu-id="e8035-177"></span></span>

<span data-ttu-id="e8035-178">Sie müssen das Element mithilfe der Aktion **Element auschecken** auschecken, bevor Sie die Aktion **Element aktualisieren** verwenden.</span><span class="sxs-lookup"><span data-stu-id="e8035-178">You must check out the item using the **Check Out Item** action before using the **Update Item** action.</span></span>
  
    
    

### <a name="errors-were-found-when-compiling-the-workflow-the-workflow-files-were-saved-but-cannot-be-run-unexpected-error-on-server-associating-the-workflow"></a><span data-ttu-id="e8035-p115">Fehler beim Kompilieren des Workflows. Die Workflowdateien wurden gespeichert, können aber nicht ausgeführt werden. Unerwarteter Fehler auf dem Server beim Zuweisen des Workflows.</span><span class="sxs-lookup"><span data-stu-id="e8035-p115">Errors were found when compiling the workflow. The workflow files were saved but cannot be run. Unexpected error on server associating the workflow</span></span>
<span data-ttu-id="e8035-182"><a name="bkmk_error13"> </a></span><span class="sxs-lookup"><span data-stu-id="e8035-182"></span></span>

<span data-ttu-id="e8035-183">Weitere Informationen finden Sie unter  [Microsoft Support Knowledge Base-Artikel-ID 2557533](http://support.microsoft.com/kb/2557533) ( `http://support.microsoft.com/kb/2557533`).</span><span class="sxs-lookup"><span data-stu-id="e8035-183">See  [Microsoft Support Knowledge Base article ID 2557533](http://support.microsoft.com/kb/2557533) ( `http://support.microsoft.com/kb/2557533`) for more information.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="e8035-184">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="e8035-184">Additional resources</span></span>
<span data-ttu-id="e8035-185"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e8035-185"></span></span>


-  [<span data-ttu-id="e8035-186">Bewährte Methoden für die SharePoint-Workflowentwicklung</span><span class="sxs-lookup"><span data-stu-id="e8035-186">SharePoint workflow development best practices</span></span>](sharepoint-workflow-development-best-practices)
    
  
-  [<span data-ttu-id="e8035-187">Entwickeln von SharePoint-Workflows mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e8035-187">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio)
    
  

  
    
    

