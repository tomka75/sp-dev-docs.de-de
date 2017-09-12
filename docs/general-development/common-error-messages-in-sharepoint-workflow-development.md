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
# <a name="common-error-messages-in-sharepoint-workflow-development"></a>Allgemeine Fehlermeldungen bei der SharePoint-Workflowentwicklung
Eine Auflistung der häufigsten Fehlermeldungen, die bei der Entwicklung von SharePoint-Workflows auftreten können sowie Anleitungen zur Lösung des zugrunde liegenden Problems.
## <a name="common-sharepoint-workflow-errors"></a>Häufige Fehler bei SharePoint-Workflows

Obwohl diese Liste nicht jeden erdenklichen Fehler enthält, der möglicherweise beim Entwickeln von SharePoint-Workflows auftreten kann, sind dennoch die am wahrscheinlichsten auftretenden Fehler enthalten.
  
    
    

-  [Timeout beim Warten auf den Abschluss der Sandkasten-Codeausführungsanforderung im Arbeitsprozess.](#bkmk_error01)
    
  
-  [Timeout beim Warten auf den Abschluss der Anforderung in der Sandkasten-Anwendungsdomäne.](#bkmk_error02)
    
  
-  [Der Arbeitsprozess, der diese Anforderung verarbeitet, wurde beendet, weil er die Ressource {0} überschritten hat.](#bkmk_error03)
    
  
-  [Dieser Workflow konnte nicht ausgeführt werden, da eine Sandkastenlösung einen Fehler erkannt hat.](#bkmk_error04)
    
  
-  [Dieser Workflow konnte nicht ausgeführt werden, da ein Fehler im Sandkasten aufgetreten ist: Es konnte kein Prozess aus dem Prozesspool abgerufen werden.](#bkmk_error05)
    
  
-  [Dieser Workflow konnte nicht ausgeführt werden, da ein Fehler im Sandkasten aufgetreten ist: Der Sandkasten-Codearbeitsprozess wurde unerwartet beendet.](#bkmk_error06)
    
  
-  [Die E-Mail konnte nicht gesendet werden. Stellen Sie sicher, dass die Einstellungen für ausgehende E-Mails für den Server ordnungsgemäß konfiguriert sind.](#bkmk_error07)
    
  
-  [Das Element konnte vom Workflow nicht aktualisiert werden, möglicherweise weil mindestens eine Spalte des Elements einen anderen Informationstyp erfordert.](#bkmk_error08)
    
  
-  [Fehler des Workflowvorgangs, weil die Workflowsuche kein übereinstimmendes Element finden konnte.](#bkmk_error09)
    
  
-  [Das Listenelement konnte vom Workflow nicht erstellt werden, weil der Dateiname fehlt oder ungültig ist.](#bkmk_error10)
    
  
-  [Koersionsfehler: Die Eingabenachschlagedaten können nicht in den angeforderten Typ umgewandelt werden.](#bkmk_error11)
    
  
-  [Fehler des Workflowvorgangs, weil das Dokument für diese Aktion ausgecheckt sein muss.](#bkmk_error12)
    
  
-  [Fehler beim Kompilieren des Workflows. Die Workflowdateien wurden gespeichert, können aber nicht ausgeführt werden. Unerwarteter Fehler auf dem Server beim Zuweisen des Workflows.](#bkmk_error13)
    
  

### <a name="timeout-while-waiting-for-sandboxed-code-execution-request-to-complete-within-the-worker-process"></a>Timeout beim Warten auf den Abschluss der Sandkasten-Codeausführungsanforderung im Arbeitsprozess.
<a name="bkmk_error01"> </a>

Dasselbe Problem und dieselbe Lösung wie beim nachfolgenden Element, "Timeout beim Warten auf den Abschluss der Anforderung in der Sandkasten-Anwendungsdomäne."
  
    
    

### <a name="timeout-while-waiting-for-request-to-complete-within-the-sandboxed-appdomain"></a>Timeout beim Warten auf den Abschluss der Anforderung in der Sandkasten-Anwendungsdomäne.
<a name="bkmk_error02"> </a>

Beide Fehler ergeben sich aus demselben Problem. Der Standardtimeout zum Ausführen der Workflowaktion wurde überschritten. Der Standardtimeout beträgt 30 Sekunden.
  
    
    
Sie können den Timeoutwert für lokale Installationen, aber nicht für SharePoint Online-Installationen ändern. Damit Sie diesen Fehler nicht in SharePoint Online-Installationen erhalten, müssen Sie den Code ändern, um Aktionen in Arbeitsprozessen oder der Anwendungsdomäne auf weniger als 30 Sekunden zu begrenzen.
  
    
    
Führen Sie den folgenden Windows PowerShell-Befehl aus, um das Timeout in Ihrer lokalen Installation zu ändern. Beachten Sie, dass der Timeout im Beispielcode auf 60 Sekunden zurückgesetzt wird, aber Sie können einen anderen Wert verwenden.
  
    
    



```

Add-pssnapin microsoft.sharepoint.powershell
   $userCodeSvc = [Microsoft.SharePoint.Administration.SPUserCodeService]::Local
   #change to 60 second timeout
   $userCodeSvc.WorkerProcessExecutionTimeout = 60 
   $userCodeSvc.Update()
```


### <a name="the-worker-process-handling-this-request-was-ended-because-it-exceeded-the-resource-0"></a>Der Arbeitsprozess, der diese Anforderung verarbeitet, wurde beendet, weil er die Ressource {0} überschritten hat.
<a name="bkmk_error03"> </a>

In der Fehlerzeichenfolge ist der Wert von  `{0}` ein Platzhalter für eine bestimmte Ressource, deren Schwellenwert überschritten wurde. Um das Problem zu verringern, sollten Sie Ihren Code ändern, damit der Ressourcenschwellenwert nicht überschritten wird. Diese Ressourcenwerte sind unter [Einschränkungen beim Ressourceneinsatz in Sandkastenlösungen](http://msdn.microsoft.com/en-us/library/gg615462%28v=office.14%29.aspx) dokumentiert.
  
    
    

### <a name="this-workflow-could-not-run-because-a-sandboxed-solution-encountered-an-error"></a>Dieser Workflow konnte nicht ausgeführt werden, da eine Sandkastenlösung einen Fehler erkannt hat.
<a name="bkmk_error04"> </a>

Der Workflowcode hat eine unbehandelte Ausnahme ausgelöst. Das Beheben dieses Fehlers erfordert das Debuggen und Bereinigen des Sandkastencodes.
  
    
    

### <a name="this-workflow-could-not-run-because-the-sandbox-failed-could-not-get-a-process-from-the-process-pool"></a>Dieser Workflow konnte nicht ausgeführt werden, da ein Fehler im Sandkasten aufgetreten ist: Es konnte kein Prozess aus dem Prozesspool abgerufen werden.
<a name="bkmk_error05"> </a>

Es ist ein Fehler in Ihrer Sandkastenkonfiguration aufgetreten. Informationen zum Konfigurieren einer Sandkastenlösung finden Sie unter  [Sandkastenlösungen in SharePoint](http://msdn.microsoft.com/en-us/library/ee536577%28v=office.14%29.aspx).
  
    
    

### <a name="this-workflow-could-not-run-because-the-sandbox-failed-the-sandboxed-code-worker-process-exited-unexpectedly"></a>Dieser Workflow konnte nicht ausgeführt werden, da ein Fehler im Sandkasten aufgetreten ist: Der Sandkasten-Codearbeitsprozess wurde unerwartet beendet.
<a name="bkmk_error06"> </a>

Es ist ein Fehler in Ihrer Sandkastenkonfiguration aufgetreten. Informationen zum Konfigurieren einer Sandkastenlösung finden Sie unter  [Sandkastenlösungen in SharePoint](http://msdn.microsoft.com/en-us/library/ee536577%28v=office.14%29.aspx).
  
    
    

### <a name="the-e-mail-message-cannot-be-sent-make-sure-the-outgoing-e-mail-settings-for-the-server-are-configured-correctly"></a>Die E-Mail konnte nicht gesendet werden. Stellen Sie sicher, dass die Einstellungen für ausgehende E-Mails für den Server ordnungsgemäß konfiguriert sind.
<a name="bkmk_error07"> </a>

Bei der Behandlung von E-Mail-Problemen sind zwei Fakten zu berücksichtigen. Stellen Sie sowohl für lokale als auch für SharePoint Online-Installationen sicher, dass alle Adressen in den Zeilen **An:** und **Cc:** gültige E-Mail-Adressen sind. Stellen Sie bei lokalen Installationen sicher, dass die E-Mail-Einstellungen auf dem Server ordnungsgemäß konfiguriert sind.
  
    
    
Überprüfen Sie Folgendes, um sicherzustellen, dass Sie die ein- und ausgehenden E-Mails ordnungsgemäß konfiguriert haben.
  
    
    

-  [Bereitstellungshandbuch für Microsoft SharePoint](http://download.microsoft.com/download/1/F/6/1F6D3BE4-1174-4320-A1D1-C0E2681CCCF3/Deployment-guide-for-SharePoint.pdf)
    
  
-  [Konfigurieren von ein- und ausgehenden E-Mails in SharePoint Server](http://blogs.msdn.com/b/pareshg/archive/2010/04/23/how-to-configure-incoming-and-outgoing-emails-in-sharepoint-server-2010.aspx)
    
  

### <a name="the-workflow-could-not-update-the-item-possibly-because-one-or-more-columns-for-the-item-require-a-different-type-of-information"></a>Das Element konnte vom Workflow nicht aktualisiert werden, möglicherweise weil mindestens eine Spalte des Elements einen anderen Informationstyp erfordert.
<a name="bkmk_error08"> </a>

Dieser Fehler ergibt sich häufig in einer von zwei Situationen:
  
    
    

- Eines der Listenfelder wurde entfernt oder geändert, aber der Workflow wurde nicht aktualisiert, um die Änderung zu berücksichtigen. Daher versucht er einen Wert für das alte Feld festzulegen. Prüfen Sie alle Aktionen **Listenelement aktualisieren** in Ihrem Workflow, und stellen Sie sicher, dass diese geeignete Werte für Felder festlegen. Prüfen Sie zudem, dass diese Felder in der Liste vorhanden sind.
    
  
- Es ist ein Datentypfehler aufgetreten, bei dem der Workflow versucht, einen Wert in einem Feld des Listenelements mit einem falschen Datentyp festzulegen. Bestätigen Sie, dass der Vorgang **Feld zurückgeben als** der Suche den richtigen Datentyp aufweist.
    
  

### <a name="the-workflow-operation-failed-because-the-workflow-lookup-found-no-matching-item"></a>Fehler des Workflowvorgangs, weil die Workflowsuche kein übereinstimmendes Element finden konnte.
<a name="bkmk_error09"> </a>

Dies weist auf einen Fehler in der Workflowlogik hin. Stellen Sie sicher, dass Sie die richtige Liste und das richtige Feld in der Suche auswählen.
  
    
    

### <a name="the-workflow-could-not-create-the-list-item-because-the-file-name-is-either-missing-or-invalid"></a>Das Listenelement konnte vom Workflow nicht erstellt werden, weil der Dateiname fehlt oder ungültig ist.
<a name="bkmk_error10"> </a>

Dies weist auf einen Fehler in der Workflowlogik hin. Stellen Sie sicher, dass der im Feld **Pfad und Name** eingegebene Dateiname gültig ist. Häufige Ursachen für ungültige Dateinamen umfassen fehlende oder falsche Dateierweiterungen oder eine Datei-/Pfadzeichenfolge, die zu lang ist und die zulässige Zeichenanzahl überschreitet.
  
    
    

### <a name="coercion-failed-unable-to-transform-the-input-lookup-data-into-the-requested-type"></a>Koersionsfehler: Die Eingabenachschlagedaten können nicht in den angeforderten Typ umgewandelt werden.
<a name="bkmk_error11"> </a>

Der Vorgang konnte die Werte nicht zwischen inkompatiblen Datentypen verteilen (z. B. die Konvertierung einer zufälligen Zeichenfolge in einen Datum/Uhrzeit-Wert). Prüfen Sie die Einstellungen für **Feld zurückgeben als** in Ihrer Suche, um sicherzustellen, dass es sich um einen gültigen Datentyp für die erwarteten Daten handelt.
  
    
    

### <a name="the-workflow-operation-failed-because-the-action-requires-the-document-to-be-checked-out"></a>Fehler des Workflowvorgangs, weil das Dokument für diese Aktion ausgecheckt sein muss.
<a name="bkmk_error12"> </a>

Sie müssen das Element mithilfe der Aktion **Element auschecken** auschecken, bevor Sie die Aktion **Element aktualisieren** verwenden.
  
    
    

### <a name="errors-were-found-when-compiling-the-workflow-the-workflow-files-were-saved-but-cannot-be-run-unexpected-error-on-server-associating-the-workflow"></a>Fehler beim Kompilieren des Workflows. Die Workflowdateien wurden gespeichert, können aber nicht ausgeführt werden. Unerwarteter Fehler auf dem Server beim Zuweisen des Workflows.
<a name="bkmk_error13"> </a>

Weitere Informationen finden Sie unter  [Microsoft Support Knowledge Base-Artikel-ID 2557533](http://support.microsoft.com/kb/2557533) ( `http://support.microsoft.com/kb/2557533`).
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Bewährte Methoden für die SharePoint-Workflowentwicklung](sharepoint-workflow-development-best-practices)
    
  
-  [Entwickeln von SharePoint-Workflows mit Visual Studio](develop-sharepoint-workflows-using-visual-studio)
    
  

  
    
    

