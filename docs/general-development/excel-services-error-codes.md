---
title: Excel Services-Fehlercodes
ms.date: 09/25/2017
keywords: alerts
f1_keywords: alerts
ms.prod: sharepoint
ms.assetid: ff128d67-f3ac-4a8f-ae8e-1e19e343014e
ms.openlocfilehash: a6f16985d452bc10ffd20e7246a80a3efce34fb8
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="excel-services-error-codes"></a>Excel Services-Fehlercodes

Excel Services generiert Fehler und Fehlermeldungen in die SOAP-Ausnahme basierend auf Fehler, die in Excel Services auftreten. Die folgende Tabelle zeigt die Fehler, die beim Aufrufen der Methoden Excel Web Services einer SOAP-Ausnahme zugegriffen werden. 
  
    
    

You use the  [SubCode](http://msdn.microsoft.com/library/frlrfSystemWebServicesProtocolsSoapExceptionClassSubCodeTopic.aspx) property of the **SoapException** class to capture the error codes. For more information about using the **SubCode** property to capture error codes, see [How to: Use the SubCode Property to Capture Error Codes](how-to-use-the-subcode-property-to-capture-error-codes.md) For more information about Excel Services alerts, see  [Excel Services Alerts](excel-services-alerts.md). 
  
    
    


## <a name="error-codes"></a>Fehlercodes

Die folgende Tabelle enthält die Fehlercodes für Warnungen von Excel-Webdiensten und die zugehörigen Nachrichten, Erläuterungen und Lösungen. 
  
    
    


|**Fehlercode**|**Meldung**|**Erläuterung**|**Lösung**|
|:-----|:-----|:-----|:-----|
|ApiInvalidArgument  <br/> |Ungültiger Wert für Argument: {0}  <br/> |Dem API-Aufruf wurde ein ungültiger Wert für ein Argument übergeben.  <br/> 0 = Name des Arguments. Dieser Wert ist ungültig.  <br/> |Verwenden Sie einen gültigen Wert für das Argument.  <br/> |
|ApiInvalidCoordinate  <br/> |Die {0}-Koordinate von {1} ist ungültig.  <br/> |0 = Name der Koordinate (Zeile, Spalte, Höhe, Breite).  <br/> 1 = Name des Arguments, das die koordinatenstruktur enthält.  <br/> Der Inhalt der **RangeCoordinates** -Klasse oder die Row\\column\\height\\width-Parameter für einen Get- oder Set-Aufruf sind ungültig. <br/> |Verwenden Sie die gültigen Werte für die Koordinaten für das Argument.  <br/> |
|DimensionAndArrayMismatch  <br/> |Die Größe des bereitgestellten Arrays stimmt nicht mit der Größe und der Form des Zielbereichs überein.  <br/> |Der Aufrufer hat versucht, einen Bereich in einer Arbeitsmappe eingefügt werden, aber der Parameter, der die Arraywerte enthält, nicht mit dem Zielbereich überein.  <br/> |Stellen Sie sicher, dass die Größe des bereitgestellten Arrays die Dimensionen des Zielbereichs (z. B. 2 Spalten breit und 3 Zeilen hoch) entspricht.  <br/> |
|DiscontiguousRangeNotSupported  <br/> |Die Anforderung für den Bereich bezieht sich nicht auf einen zusammenhängenden Bereich. Nur zusammenhängende Bereiche werden von Excel Services unterstützt.  <br/> |Der Anrufer ein nicht zusammenhängenden Bereichs angegeben, beim Versuch, festlegen oder Abrufen eines Zellbereichs. Excel Services unterstützt keine nicht zusammenhängenden Bereiche. Es unterstützt nur zusammenhängenden Bereiche.  <br/> |Geben Sie einen zusammenhängenden Bereich wie "A1: B7" oder "A1" oder "MyTable [#Data]" anstelle eines nicht zusammenhängenden Bereichs wie "A1: B7, B12" oder "A1, A3".  <br/> |
|ExternalDataRefreshFailed  <br/> |Externe Daten für die folgenden Verbindungen konnten nicht abgerufen:  <br/> {0}  <br/> Die Datenquellen sind möglicherweise nicht verfügbar, reagieren nicht oder haben den Zugriff verweigert.  <br/> |Beim Versuch, eine Datenquelle innerhalb einer Arbeitsmappe zu aktualisieren, sind wiederholt Fehler aufgetreten.  <br/> 0 ist eine \\n getrennte Liste von Verbindungsnamen.  <br/> |Stellen Sie sicher, dass die Datenquelle verfügbar ist und dass Sie die Berechtigung für den Zugriff verfügen.  <br/> |
|FileOpenAccessDenied  <br/> |Sie verfügen nicht über die Berechtigungen, um diese Datei in Excel Services zu öffnen.  <br/> |Ein Aufruf der **OpenWorkbook** -Methode ist fehlgeschlagen, da der Benutzer auf die Datei keinen Zugriff. <br/> |Wenden Sie sich an Ihren Administrator.  <br/> |
|FileCorrupt  <br/> |Die ausgewählte Datei kann nicht geöffnet werden, weil sie beschädigt ist, durch IRM geschützt ist oder in einem Dateiformat vorliegt, das von Excel Services nicht unterstützt wird. Möglicherweise kann diese Datei in Excel geöffnet werden.  <br/> |Ein Aufruf der **OpenWorkbook** -Methode ist fehlgeschlagen, da die Datei beschädigt ist. <br/> |Versuchen Sie erneut, die Datei zu öffnen, oder verwenden Sie Excel zum Öffnen der Datei.  <br/> |
|FileOpenNotFound  <br/> |Die ausgewählten Datei konnte nicht gefunden werden. Überprüfen Sie die Schreibweise des Dateinamens, und stellen Sie sicher, dass der Speicherort korrekt ist.  <br/> |Ein Aufruf der **OpenWorkbook** -Methode ist fehlgeschlagen, da die Datei nicht vorhanden ist. <br/> |Stellen Sie sicher, dass die Datei wurde nicht wurde umbenannt, verschoben oder gelöscht werden, dass die Datei an einem vertrauenswürdigen Speicherort befindet und, dass Sie Zugriff auf die Datei verfügen. Wenn das Problem weiterhin besteht, wenden Sie sich an den Systemadministrator.  <br/> |
|FileOpenSecuritySettings  <br/> |Die ausgewählten Datei kann nicht zu diesem Zeitpunkt aufgrund von Sicherheitseinstellungen für Excel Services nicht geöffnet werden.  <br/> |Ein Aufruf der **OpenWorkbook** -Methode Fehler aufgrund des Administrators Sicherheitseinstellungen aus verschiedenen Gründen öffnen. Beispielsweise die Datei ist zu groß, d. h., die Größe den vom Administrator festgelegten Grenzwert überschritten.<br/> |Wenden Sie sich an Ihren Administrator.  <br/> |
|FormulaEditingNotEnabled  <br/> |Die Formelbearbeitung ist in dieser Version von Excel Services nicht aktiviert.  <br/> |Der Aufrufer hat versucht, eine Formel in die Arbeitsmappe zu schreiben.  <br/> |Versuchen Sie keine Formel schreiben, da es in dieser Version von Excel Services nicht unterstützt wird.  <br/> |
|GenericFileOpenError  <br/> |Fehler beim Öffnen der ausgewählten Datei.  <br/> |Die Datei kann von Excel Services aus einem unbekannten Grund nicht geöffnet werden.  <br/> |Warten Sie einige Minuten, und versuchen Sie die Datei erneut öffnen. Wenn das Problem weiterhin besteht, wenden Sie sich an den Systemadministrator.  <br/> |
|InvalidSheetName  <br/> |Das angeforderte Arbeitsblatt ist in der Arbeitsmappe nicht vorhanden.  <br/> |Der Name des Arbeitsblatts wurde nicht gefunden oder ist ungültig.  <br/> |Verwenden Sie einen gültigen Wert für den Namen des Blatts.  <br/> |
|InvalidOrTimedOutSession  <br/> |Der aktuelle Vorgang kann zu diesem Zeitpunkt nicht abgeschlossen werden, da die Sitzung nicht mehr auf dem Server verfügbar ist. Sie können die Arbeitsmappe erneut laden und eine neue Sitzung erstellen, allerdings gehen dabei alle vorgenommenen Änderungen verloren.  <br/> |Der Anruf  _sessionId_ Wert ist entweder ungültig oder wurde inzwischen ist eine Zeitüberschreitung aufgetreten. <br/> |Laden Sie die Arbeitsmappe in einer neuen Sitzung neu.  <br/> |
|IRMedWorkbook  <br/> |Die angeforderte Arbeitsmappe ist durch IRM geschützt. IRM-geschützte Arbeitsmappen können von Excel Services kann nicht geladen werden.  <br/> |Ein Aufruf der **OpenWorkbook** -Methode ist fehlgeschlagen, da die Arbeitsmappe von Information Rights Management (IRM) geschützt ist. <br/> |Übergeben Sie nur in Arbeitsmappen, die nicht durch IRM geschützt sind.  <br/> |
|MaxSessionsPerUserExceeded  <br/> |Die maximale Anzahl zulässiger Sitzungen pro Benutzer wurde überschritten. Der Vorgang kann nicht abgeschlossen werden.  <br/> |Die maximale Anzahl von Sitzungen, die ein Benutzer zu einem bestimmten Zeitpunkt geöffnet haben, kann wurde überschritten. Diese Beschränkung wird vom Administrator festgelegt.  <br/> |Überschreiten Sie den Grenzwert nicht, oder wenden Sie sich an Ihren Administrator.  <br/> |
|MultipleRequestsOnSession  <br/> |In dieser Sitzung wird bereits ein Vorgang verarbeitet. In einer Sitzung kann jeweils nur ein Vorgang verarbeitet werden.  <br/> |Mehrere Anforderungen wurden für dieselbe Sitzung ausgestellt. Eine Sitzung kann (bis auf wenige Ausnahmen) immer nur eine Anforderung auf einmal verarbeiten.  <br/> |Führen Sie den Vorgang erneut aus.  <br/> |
|NotMemberOfRole  <br/> |Zugriff verweigert. Sie sind nicht berechtigt, diese Aktion auszuführen oder auf diese Ressource zuzugreifen.  <br/> |Der Aufrufer verfügt nicht über Zugriffsberechtigungen für den Server.  <br/> |Wenden Sie sich an Ihren Administrator.  <br/> |
|ObjectTypeNotSupported  <br/> |Mindestens ein bereitgestellter Objekttyp wird von Excel Services nicht unterstützt. Für den Vorgang wurde ein Rollback ausgeführt.  <br/> |Der Aufrufer hat versucht, nicht unterstützten Typ Objektwerte in einen Bereich zu schreiben.  <br/> |Führen Sie den Vorgang erneut mit einer der unterstützten Objekttypen.  <br/> |
|OperationCanceled  <br/> |Der Vorgang wurde abgebrochen.  <br/> |Der Vorgang, der derzeit stattfindet wurde abgebrochen, da der Benutzer die **CancelRequest** -Methode aufruft. <br/> |Rufen Sie die **CancelRequest** -Methode nur, wenn Sie den aktuellen Vorgang abbrechen möchten. <br/> |
|RangeParseError  <br/> |Der angeforderte Bereich konnte von Excel Services nicht analysiert werden.  <br/> |Der Bereich, der in eine Methode mit dem Suffix A1 ( **SetCellA1**, **SetRangeA1**, **GetCellA1**und **GetRangeA1**) übergeben wurde, konnte nicht analysiert werden.  <br/> |Geben Sie einen Zellbereich A1-Schreibweise wie "Sheet1! Range("a6:a15") "oder einen gültigen strukturierten Verweis wie" [Lieferort]. [#Headers] ".  <br/> |
|RangeRequestAreaExceeded  <br/> |Der angeforderte Bereich überschreitet 1.000.000 Zellen.  <br/> |Der angeforderte Bereich überschreitet den Grenzwert von 1.000.000 Zellen.  <br/> |Verwenden Sie mehrere Aufrufe, um Bereiche zurückzugeben, die mehr als 1.000.000 Zellen enthalten.  <br/> |
|RetryError  <br/> |Die Anforderung kann von Excel Services nicht verarbeitet werden.  <br/> |In Excel Services kann gelegentlich Ressourcenknappheit auftreten. In diesem Fall werden möglicherweise Anforderungen verweigert.  <br/> |Warten Sie einige Minuten, und versuchen Sie es, um diesen Vorgang erneut auszuführen.  <br/> |
|SaveFailed  <br/> |Fehler beim Speichern der Datei.  <br/> |Fehler beim Aufruf der **GetWorkbook** -Methode. <br/> |Versuchen Sie erneut die Datei speichern.  <br/> |
|SetRangeFailure  <br/> |Der angeforderte Vorgang versuchte den Inhalt von Zellen zu überschreiben, die nicht bearbeitet werden können.  <br/> |Der Aufrufer hat versucht, Werte in einem Bereich zu schreiben, die Zellen geschützt ist. Beispielsweise enthält die Zelle eine Formel an.  <br/> |Nur leere Zellen oder Zellen, die Werte enthalten können von Excel Services bearbeitet werden.  <br/> |
|SheetRangeMismatch  <br/> |Das für das Argument 'sheet' eingegebene Blatt ist nicht mit dem für das Argument 'range' angegebenen Blatt identisch.  <br/> |Der Name des Blatts für einen  _sheetName_ -Parameter übergebenen entspricht nicht den im _rangeName_ -Parameter angegebenen Speicherort. <br/> |Wenn Sie einem Blatt in den Bereich und die Blatt Argumente angeben, stellen Sie sicher, dass die Blattnamen identisch sind. Beispielsweise  `Calculate(Sheet1, Sheet1!Range("A1"))`.<br/> |
|SpecifiedRangeNotFound  <br/> |Der angeforderte Bereich ist im Blatt nicht vorhanden.  <br/> |Der Bereich, der in eine Methode mit dem Suffix A1 ( **SetCellA1**, **SetRangeA1**, **GetCellA1**und **GetRangeA1**) übergeben wurde, konnte nicht gefunden werden.  <br/> |Stellen Sie sicher, dass der angegebene Bereich in dem Arbeitsblatt vorhanden ist.  <br/> |
|WorkbookNotSupported  <br/> |Die ausgewählten Datei kann nicht geöffnet werden, da sie Features enthält, die von Excel Services nicht unterstützt werden. Eine oder mehrere der folgenden nicht unterstützten Features wurden in der Arbeitsmappe erkannt:  <br/> {0}  <br/> |Die Arbeitsmappe enthält nicht unterstützte Features.  <br/> 0 = eine \\n getrennte Liste der Namen nicht unterstützter Features.  <br/> |Stellen Sie sicher, dass die Arbeitsmappe nicht Features enthalten, die von Excel Services nicht unterstützt werden.  <br/> |
   

## <a name="see-also"></a>Siehe auch


#### <a name="tasks"></a>Aufgaben


  
    
    
 [How to: Use the SubCode Property to Capture Error Codes](how-to-use-the-subcode-property-to-capture-error-codes.md)
#### <a name="concepts"></a>Konzepte


  
    
    
 [Excel Services Alerts](excel-services-alerts.md)
  
    
    
 [Excel Services Known Issues and Tips](excel-services-known-issues-and-tips.md)
  
    
    
 [Excel Services Best Practices](excel-services-best-practices.md)
