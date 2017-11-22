---
title: "Visio-Shapes in SharePoint Designer 2013 Eine Kurzübersicht (SharePoint 2010-Workflowplattform)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 51bc37fd-37de-4ad0-a75a-bdf7333bc80c
ms.openlocfilehash: d685265148d2e626982a6010f5f48a00d366863f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="visio-shapes-in-sharepoint-designer-2013-a-quick-reference-guide-sharepoint-2010-workflow-platform"></a>Visio-Shapes in SharePoint Designer 2013: Eine Kurzübersicht (SharePoint 2010-Workflowplattform)
Sie können einen Workflow in Microsoft Visio Professional 2013 erstellen und diesen dann nach Microsoft SharePoint Designer 2013 exportieren. In diesem Handbuch sind die Visio-Shapes aufgeführt, die Sie zum Erstellen des Workflows verwenden.Verwenden Sie diesen Referenzartikel nur, wenn Sie in SharePoint Designer 2013 arbeiten, weiterhin jedoch die SharePoint 2010-Workflowplattform verwenden möchten.Die Shapes für die SharePoint 2010-Workflowplattform umfassen drei Schablonen: **Aktionen - SharePoint 2010-Workflow**, **Bedingungen - SharePoint 2010-Workflow** und **Abschlusszeichen - SharePoint 2010-Workflow**.
## <a name="workflow-actions"></a>Workflowaktionen
<a name="section1"> </a>

Workflowaktionen sind bestimmte Vorgänge, die ein Workflow durchführt. Jeder Workflow muss mindestens eine Aktion enthalten.
  
    
    
Die Aktionen in dieser Liste sind in Kategorien basierend auf ihrem Anwendungsbereich in einem Workflow organisiert. Beispielsweise werden die Aktionen, die Auswirkungen auf das Verhalten eines Listenelements haben, unter **Listenaktionen**, und Aktionen für Dokumentenmappen unter **Aktionen für die Dokumentenmappe** gruppiert. Die Kategorien für Aktionen sind:
  
    
    

-  [Hauptaktionen](visio-shapes-in-sharepoint-designer-a-quick-reference-guide-sharepoint-2010.md#section1a) Hierbei handelt es sich um die am häufigsten verwendeten Aktionen in einem Workflow.
    
  
-  [Aktionen für die Dokumentenmappe](visio-shapes-in-sharepoint-designer-a-quick-reference-guide-sharepoint-2010.md#section1e) Diese Aktionen werden normalerweise in Workflows verwendet, die einer Dokumentbibliothek oder dem Dokumentinhaltstyp zugeordnet sind.
    
  
-  [Listenaktionen](visio-shapes-in-sharepoint-designer-a-quick-reference-guide-sharepoint-2010.md#section1b) Diese Aktionen führen Operationen in Listenelementen aus.
    
  
-  [Relationale Aktionen](visio-shapes-in-sharepoint-designer-a-quick-reference-guide-sharepoint-2010.md#section1d) Die einzige Aktion in dieser Kategorie sucht nach dem Vorgesetzten eines Benutzers und speichert diese Informationen in einer Variablen.
    
  
-  [Aufgabenaktionen](visio-shapes-in-sharepoint-designer-a-quick-reference-guide-sharepoint-2010.md#section1c): Aktionen dieses Typs sind mit Genehmigungs-, Feedback- und Formularoperationen verknüpft.
    
  

> **Wichtig:** Die meisten der Aktionsshapes, die sich in Visio in SharePoint-Workflows einfügen lassen, erfordern zusätzliche Konfigurationsanpassungen, wenn der Workflow in SharePoint Designer importiert wird. Denken Sie daran, in Visio über die Kommentarfunktion der einzelnen Aktionsshapes die Einstellungen oder Konfigurationsoptionen der jeweiligen Aktion zu vermerken. 
  
    
    


### <a name="core-actions"></a>Hauptaktionen
<a name="section1a"> </a>

Dies sind die am häufigsten verwendeten Aktionen, die in in jedem Workflowtyp oder -schritt verwendet werden können.



|**Visio-Aktions-Shapes**|**Entsprechende Aktion in SharePoint Designer**|**Aktionsbeschreibung**|
|:-----|:-----|:-----|
|![Kommentar hinzufügen](../images/spd15-addcomment-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Kommentar hinzufügen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Kommentar hinzufügen](../images/spd15-addcomment-txt.JPG)  <br/>  **Hinweis:** Kommentare bleiben sichtbar, wenn der Workflow nach Visio exportiert wird.           |**Kommentar hinzufügen** <br/> Verwenden Sie diese Aktion, um informative Kommentare zu Referenzzwecken im Workflow-Designer zu hinterlassen. Dies ist besonders hilfreich, wenn es andere Benutzer gibt, die sich an der Erstellung von Workflows beteiligen. Wenn z. B. eine Variable im aktuellen Workflow keinen benutzerfreundlichen Namen aufweist, verwenden Sie diese Aktion zum Hinzufügen von Kommentaren, um anzugeben, welche Funktion die Variable im Workflow hat.<br/> |
|![Zeit zum Datum hinzufügen](../images/spd15-addtimetodate-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Zeit zum Datum hinzufügen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Zeit zum Datum hinzufügen](../images/spd15-addtimetodate-txt.JPG)|**Zeit zum Datum hinzufügen** <br/> Mit dieser Aktion können Sie eine bestimmte Zeit in Minuten, Stunden, Tagen, Monaten oder Jahren zu einem Datum hinzufügen und den Ausgabewert als Variable speichern. Das Datum kann ein aktuelles Datum, ein bestimmtes Datum oder ein Nachschlagewert sein.<br/> |
|![Durchführen der Berechnung](../images/spd15-docalc-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Berechnung ausführen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Durchführen der Berechnung](../images/spd15-docalc-txt.JPG)|**Berechnung ausführen** <br/> Verwenden Sie diese Aktion, um eine Berechnung durchzuführen, z. B. das Addieren, Subtrahieren, Multiplizieren oder Dividieren zweier Werte, und um den Ausgabewert in einer Variablen zu speichern.  <br/> |
|![Protokollieren In Verlaufsliste](../images/spd15-LogHist-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Für die Verlaufsliste protokollieren** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Protokollieren In Verlaufsliste](../images/spd15-LogHist-txt.JPG)|**Für die Verlaufsliste protokollieren** <br/> Verwenden Sie diese Aktion, um eine Nachricht zum Workflow in seiner Verlaufsliste zu protokollieren. Eine Nachricht kann eine Zusammenfassung eines Workflowereignisses oder etwas anderes wichtiges über den Workflow sein. Die Verlaufsliste des Workflows kann bei der Behandlung von Problemen mit dem Workflow hilfreich sein.<br/> |
|![Für Dauer anhalten](../images/spd15-PauseDuration-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Für Dauer anhalten** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Für Dauer anhalten](../images/spd15-PauseDuration-txt.JPG)|**Für Dauer anhalten** <br/> Mit dieser Aktion können Sie den Workflow während eines bestimmten Zeitraums anhalten, angegeben in Tagen, Stunden oder Minuten.  <br/> **Hinweis:** Die Verzögerungszeit wird durch das Intervall des Zeitgeberauftrags festgelegt. Der Standardwert beträgt 5 Minuten.           |
|![Bis Datum anhalten](../images/spd15-PauseDate-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Bis Datum anhalten** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Bis Datum anhalten](../images/spd15-PauseDate-txt.JPG)|**Bis Datum anhalten** <br/> Verwenden Sie diese Aktion, um den Workflow bis zu einem bestimmten Datum anzuhalten. Sie können das aktuelle Datum, ein bestimmtes Datum oder einen Nachschlagewert hinzufügen.<br/> |
|![Festlegen des Zeitbereichs des Felds "Datum/Uhrzeit"](../images/spd15-SetTimePortion-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Den Zeitbereich des Felds 'Datum/Uhrzeit' festlegen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Festlegen des Zeitbereichs des Felds "Datum/Uhrzeit"](../images/spd15-SetTimePortion-txt.JPG)|**Den Zeitbereich des Felds 'Datum/Uhrzeit' festlegen** <br/> Verwenden Sie diese Aktion, um einen Zeitstempel zu erstellen und den Ausgabewert in einer Variablen zu speichern. Sie können die Uhrzeit in Stunden und Minuten festlegen und ein aktuelles Datum, ein bestimmtes Datum oder einen Nachschlagewert festlegen.<br/> |
|![Festlegen des Workflowstatus](../images/spd15-SetWFStatus-visio.JPG)| Diese Visio-Aktion ist identisch mit der Aktion **Workflowstatus festlegen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Festlegen des Workflowstatus](../images/spd15-SetWFStatus-txt.JPG) Sie können einen Statuswert nicht umbenennen oder löschen, nachdem dieser erstellt wurde. Allerdings müssen Sie diesen nicht verwenden. <br/>  Ein benutzerdefinierter Status ist nur für den aktuellen Workflow anwendbar und kann nicht in einem anderen Workflow verwendet werden. <br/>  Ein Workflow kann benutzerdefinierte in der Aktion definierte Statuswerte nicht verwenden, wenn die Aktion in einem Identitätswechselschritt verwendet wird. <br/> |**Festlegen des Workflowstatus** <br/>  Verwenden Sie diese Aktion, um den Status des Workflows festzulegen. Die Standardoptionen sind **Abgebrochen**, **Genehmigt** und **Abgelehnt**.  <br/> Sie können einen neuen Statuswert in der Dropdownliste in der Aktion eingeben. Sobald Sie einen Statuswert eingegeben haben, wird der Eintrag der Dropdownliste automatisch hinzugefügt.<br/> Wenn die Aktion **Workflowstatus festlegen** der letzte Schritt in einem Workflow war, in der auch ein benutzerdefinierter Wert verwendet wurde, wird der benutzerdefinierte Wert in der Spalte **Status** in der Liste angezeigt, wenn der Workflow angehalten oder abgeschlossen ist. <br/> |
|![Festlegen der Workflowvariablen](../images/spd15-SetWFVar-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Workflowvariable festlegen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Festlegen der Workflowvariablen](../images/spd15-SetWFVar-txt.JPG)|**Workflowvariable festlegen** <br/> Verwenden Sie diese Aktion, um eine Workflowvariable auf einen Wert festzulegen. Verwenden Sie diese Aktion, wenn der Workflow einer Variablen Daten zuweisen soll.<br/> |
|![Anhalten des Workflows](../images/spd15-StopWF-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Workflow beenden** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Anhalten des Workflows](../images/spd15-StopWF-txt.JPG)|**Workflow beenden** <br/>  Verwenden Sie diese Aktion, um die aktuelle Instanz des Workflows zu stoppen und eine Nachricht in der Liste **Workflowverlauf** zu protokollieren. Die in der Aktion angegebene Nachricht wird in der Spalte **Beschreibung** im Workflowverlauf angezeigt, wenn der Workflow abgeschlossen wird. <br/> |
   

### <a name="list-actions"></a>Listenaktionen
<a name="section1b"> </a>

Diese Aktionen werden für Listenelemente verwendet.
  
    
    



|**VISIO-AKTIONS-SHAPE**|**ENTSPRECHENDE AKTION IN SHAREPOINT DESIGNER**|**AKTIONSBESCHREIBUNG**|
|:-----|:-----|:-----|
|![Hinzufügen von Berechtigungen für Listenelement](../images/spd15-AddListItemPerms-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Listenelementberechtigungen hinzufügen** in SharePoint Designer 2013 und wird wie folgt visuell dargestellt: <br/> ![Add permissions to item](../images/spd15-AddListItemPerms-txt.JPG)    **Hinweis:** Diese Aktion ist nur innerhalb von Identitätswechselschritten verfügbar.           |**Listenelementberechtigungen hinzufügen** <br/> Diese Aktion gewährt bestimmten Benutzern bestimmte Berechtigungsstufen für ein Element.  <br/> |
|![Einchecken eines Elements](../images/spd15-CheckInItem-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Element einchecken** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Einchecken eines Elements](../images/spd15-CheckInItem-txt.JPG)|**Element einchecken** <br/> Diese Aktion checkt ein ausgechecktes Element ein.  <br/> **Hinweis:** Sie können nur Elemente aus Dokumentbibliotheken einchecken.           |
|![Element auschecken](../images/spd15-CheckOutItem-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Element auschecken** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Auschecken eines Elements](../images/spd15-CheckOutItem-txt.JPG)|**Element auschecken** <br/> Mit dieser Aktion checken Sie ein Element aus. Der Workflow überprüft zunächst, ob das Element eingecheckt ist, bevor das betreffende Dokument ausgecheckt wird.  <br/> **Hinweis:** Sie können nur Elemente aus Bibliotheken innerhalb Ihrer Website auschecken.           |
|![Listenelement kopieren](../images/spd15-CopyListItem-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Listenelement kopieren** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Kopieren eines Listenelements](../images/spd15-CopyListItem-txt.JPG)|**Listenelement kopieren** <br/> Verwenden Sie diese Aktion, um ein Listenelement in eine andere Liste zu kopieren. Wenn ein Dokument in dem Listenelement vorhanden ist, kopiert der Workflow auch das Dokument in die Zielliste.<br/> **Wichtig:** In der Quell- und der Zielliste muss jeweils mindestens eine ähnliche Spalte existieren.           |
|![Listenelement erstellen](../images/spd15-CreateListItem-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Listenelement erstellen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Erstellen eines Listenelements](../images/spd15-CreateListItem-txt.JPG)|**Listenelement erstellen** <br/> Verwenden Sie diese Aktion, um ein neues Listenelement in der angegebenen Liste zu erstellen. Sie können die Felder und Werte in dem neuen Element angeben.<br/> Diese Aktion kann immer dann verwendet werden, wenn Sie ein neues Element mit bestimmten Informationen erstellen möchten.  <br/> **Hinweis:** Die Ausgabevariable ist die ID des in der Liste erstellten Elements.           |
|![Element löschen](../images/spd15-DeleteItem-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Element löschen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Löschen eines Elements](../images/spd15-DeleteItem-txt.JPG)|**Element löschen** <br/> Verwenden Sie diese Aktion, um ein Element zu löschen.  <br/> |
|![Auschecken des Elements verwerfen](../images/spd15-DiscardItem-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Auschecken von Element verwerfen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Auschecken des Elements verwerfen](../images/spd15-DiscardItem-txt.JPG)|**Auschecken von Element verwerfen** <br/> Verwenden Sie diese Aktion, wenn ein Element ausgecheckt ist, Änderungen daran vorgenommen wurden und Sie diese Änderungen verwerfen und das Element wieder einchecken möchten.  <br/> |
|![Erben von Listenelementberechtigungen](../images/spd15-InheritListItemPerms-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Übergeordnete Listenelementberechtigungen erben** in SharePoint Designer 2013 und wird wie folgt visuell dargestellt: <br/> ![Listenelementberechtigungen erben](../images/spd15-InheritListItemPerms-txt.JPG)    **Hinweis:** Diese Aktion ist nur innerhalb von Identitätswechselschritten verfügbar.           |**Listenelementberechtigungen erben** <br/> Wenn das Element über eindeutige Berechtigungen verfügt, können Sie diese Aktion verwenden, damit das Element die übergeordneten Berechtigungen von der Liste erbt.  <br/> |
|![Entfernen von Listenelementberechtigungen](../images/spd15-RmListItemPerms-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Remove List Item Permission** in SharePoint Designer 2013 und wird wie folgt visuell dargestellt:  <br/> ![Listenelementberechtigungen entfernen](../images/spd15-RmListItemPerms-txt.JPG)    **Hinweis:** Diese Aktion ist nur innerhalb von Identitätswechselschritten verfügbar.           |**Listenelementberechtigungen entfernen** <br/> Durch diese Aktion werden Berechtigungen von einem Element für bestimmte Benutzer entzogen.  <br/> |
|![Ersetzen von Listenelementberechtigungen](../images/spd15-ReplaceListItemPerms-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Listenelementberechtigungen ersetzen** in SharePoint Designer 2013 und wird wie folgt visuell dargestellt: <br/> ![Listenelementberechtigungen ersetzen](../images/spd15-ReplaceListItemPerms-txt.JPG)    **Hinweis:** Diese Aktion ist nur innerhalb von Identitätswechselschritten verfügbar.           |**Listenelementberechtigungen ersetzen** <br/> Dadurch werden die aktuellen Berechtigungen eines Elements durch die neuen Berechtigungen ersetzt, die Sie in der Aktion angeben.  <br/> |
|![Festlegen des Inhaltsgenehmigungsstatus](../images/spd15-SetContentApprovalStatus-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Status für die Genehmigung von Inhalten festlegen** in SharePoint Designer 2013 und wird wie folgt visuell dargestellt: <br/> ![Status für die Genehmigung von Inhalten festlegen](../images/spd15-SetContentApprovalStatus-txt.JPG)    **Hinweis:** Diese Aktion kann nur verwendet werden, wenn in der Liste die Inhaltsgenehmigung aktiviert ist.|**Status für die Genehmigung von Inhalten festlegen** <br/> Wenn Sie die Genehmigung von Inhalten in Ihrer Liste aktiviert haben, verwenden Sie diese Aktion, um das Statusfeld für die Inhaltsgehnemigung auf einen Wert wie "Genehmigt", "Abgelehnt" oder "Ausstehend" festzulegen. Sie können in der Aktion einen benutzerdefinierten Status eingeben.<br/> **Hinweis:** Die Aktion **Status für die Genehmigung von Inhalten festlegen** wird auf das Element angewendet, das der Workflow aktuell verarbeitet. In Websiteworkflows ist sie daher nicht verfügbar.          |
|![Feld im aktuellen Element festlegen](../images/spd15-SetFieldCurrItem-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Feld im aktuellen Element festlegen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Festlegen von Feld in aktuellem Element](../images/spd15-SetFieldCurrItem-txt.JPG)|**Feld im aktuellen Element festlegen** <br/> Mit dieser Aktion können Sie einen Wert für ein Feld im aktuellen Element festlegen.  <br/> **Hinweis:** Soll der Workflow bis zur Änderung des Feldwerts angehalten werden, müssen Sie stattdessen die Aktion **Auf Feldänderung im aktuellen Element warten** verwenden.          Die Aktion **Feld im aktuellen Element festlegen** sollte nicht in Websiteworkflows verwendet werden. <br/> |
|![Listenelement aktualisieren](../images/spd15-UpdateListItem-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Listenelement aktualisieren** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Aktualisieren des Listenelements](../images/spd15-UpdateListItem-txt.JPG)|**Listenelement aktualisieren** <br/> Verwenden Sie diese Aktion, um ein Listenelement zu aktualisieren. Sie können die Felder und die neuen Werte in diesen Feldern angeben.<br/> |
|![Warten auf Feldänderung in aktuellem Element](../images/spd15-Wait4FieldChange-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Auf Feldänderung im aktuellen Element warten** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Warten auf Feldänderung](../images/spd15-Wait4FieldChange-txt.JPG)|**Auf Feldänderung im aktuellen Element warten** <br/> Diese Aktion hält den Workflow an, bis das Feld im aktuellen Element auf einen neuen Wert gesetzt wurde.  <br/> **Hinweis:** Soll der Workflow den Feldwert ändern, sollten Sie den Workflow nicht auf eine Feldänderung warten lassen, sondern stattdessen die Aktion **Feld im aktuellen Element festlegen** verwenden.          |
   

### <a name="task-actions"></a>Aufgabenaktionen
<a name="section1c"> </a>

Die Aktionen in dieser Kategorie werden auf Aufgabenelemente angewendet. Sie lassen sich nur auf SharePoint-Websites in SharePoint anwenden.
  
    
    




|**SHAPE FÜR DIE VISIO-AKTION**|**ENTSPRECHENDE AKTION IN SHAREPOINT DESIGNER**|**AKTIONSBESCHREIBUNG**|
|:-----|:-----|:-----|
|![Zuweisen eines Formulars zu einer Gruppe](../images/spd15-AssignForm2Grp-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Formular einer Gruppe zuordnen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Zuweisen eines Formulars zu einer Gruppe](../images/spd15-AssignForm2Grp-txt.JPG)|**Formular einer Gruppe zuordnen** <br/> Mithilfe dieser Aktion können Sie ein benutzerdefiniertes Aufgabenformular mit angepassten Feldern erstellen.  <br/> Sie können diese Aktion verwenden, um eine Aufgabe einem oder mehreren Teilnehmern bzw. einer oder mehreren Gruppen zuzuweisen und diese aufzufordern, ihre Aufgaben auszuführen. Teilnehmer geben ihre Antworten in die Felder des benutzerdefinierten Aufgabenformulars ein, wenn sie mit der Aufgabe fertig sind, und klicken in dem Formular auf **Aufgabe erledigen**.<br/> |
|![Zuweisen eines Aufgabenelements](../images/spd15-AssignToDoItem-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Aufgabe zuordnen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Zuweisen eines Aufgabenelements](../images/spd15-AssignToDoItem-txt.JPG)|**Aufgabe zuordnen** <br/> Mit dieser Aktion können Sie jedem Teilnehmer eine Aufgabe zuordnen und ihn auffordern, seine Aufgaben zu erledigen und nach Abschluss auf die Schaltfläche **Aufgabe erledigen** im Aufgabenformular zu klicken. <br/> |
|![Sammeln von Daten von einem Benutzer](../images/spd15-CollectDataFrUser-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Daten von einem Benutzer sammeln** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Sammeln von Daten von einem Benutzer](../images/spd15-CollectDataFrUser-txt.JPG)|**Daten von einem Benutzer sammeln** <br/> Mit dieser Aktion können Sie einem Teilnehmer eine Aufgabe zuordnen, ihn auffordern, die erforderlichen Informationen in einem benutzerdefinierten Aufgabenformular anzugeben und dann auf die Schaltfläche **Aufgabe erledigen** im Aufgabenformular zu klicken. <br/> Diese Aktion verfügt über eine OUTPUT-Klausel. Das bedeutet: Der Workflow speichert die von der Aktion zurückgegebenen Informationen in einer entsprechenden Variablen. Die Listenelement-ID des abgeschlossenen Aufgabenelements der Aktion wird in der Variablen „collect“ gespeichert.  <br/> |
|![Genehmigungsprozess starten](../images/spd15-StartApprovalProc-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Genehmigungsprozess starten** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Starten des Genehmigungsprozesses für Dokumentensatz](../images/spd15-StartApprovalProc-txt.JPG)|**Genehmigungsprozess starten** <br/> Verwenden Sie diese Aktion, um ein Dokument zur Genehmigung weiterzuleiten. Genehmigende Personen können das Dokument genehmigen oder zurückweisen , die Genehmigungsaufgabe erneut zuweisen oder Änderungen anfordern.<br/> Sie können internen und externen Teilnehmern Aufgaben in der Aktion zuweisen. Ein externer Teilnehmer kann ein Mitarbeiter Ihres Unternehmens sein, der kein Benutzer in der Websitesammlung ist, oder jemand außerhalb Ihres Unternehmens.<br/> |
|![Starten des Feedbackprozesses](../images/spd15-StartFeedback-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Feedbackvorgang starten** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Starten des Feedbackprozesses](../images/spd15-StartFeedback-txt.JPG)|**Feedbackprozess starten** <br/> Mit dieser Aktion können Sie Benutzern Feedback-Aufgabenelemente in einer bestimmten Reihenfolge zuweisen: seriell oder parallel. Der Standardwert ist „parallel“. Benutzer und Aufgabenteilnehmer können Aufgaben auch an andere Benutzer neu zuweisen. Sobald die Benutzer die Aufgabe erledigt haben, können Sie auf die Schaltfläche **Feedback senden** klicken, um mitzuteilen, dass sie fertig sind. <br/> Sie können internen und externen Teilnehmern Aufgaben in der Aktion zuweisen. Ein externer Teilnehmer kann ein Mitarbeiter Ihres Unternehmens sein, der kein Benutzer in der Websitesammlung ist, oder jemand außerhalb Ihres Unternehmens.<br/> |
|![Starten des benutzerdefinierten Aufgabenprozesses](../images/spd15-StartCustomTask-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Benutzerdefinierten Aufgabenprozess starten** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Starten des benutzerdefinierten Aufgabenprozesses](../images/spd15-StartCustomTask-txt.JPG)|**Benutzerdefinierten Aufgabenprozess starten** <br/> Die Aktion **Benutzerdefinierten Aufgabenprozess starten** ist eine Vorlage für einen Genehmigungsprozess, die Sie verwenden können, wenn andere Genehmigungsaktionen nicht Ihren Anforderungen entsprechen. <br/> |
   

### <a name="relational-actions"></a>Relationale Aktionen
<a name="section1d"> </a>

In dieser Kategorie existiert nur eine einzige Aktion. Sie ruft den Vorgesetzten eines Benutzers ab und speichert diese Information in einer Variablen. Diese Aktion lässt sich nur auf SharePoint-Websites in SharePoint anwenden.
  
    
    




|**SHAPE FÜR DIE VISIO-AKTION**|**ENTSPRECHENDE AKTION IN SHAREPOINT DESIGNER**|**AKTIONSBESCHREIBUNG**|
|:-----|:-----|:-----|
|![Nachschlagen des Managers eines Benutzers](../images/spd15-LookupMgr4User-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Vorgesetzten eines Benutzers nachschlagen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Nachschlagen des Managers eines Benutzers](../images/spd15-LookupMgr4User-txt.JPG)|**Vorgesetzten eines Benutzers nachschlagen** <br/> Mit dieser Aktion können Sie den Vorgesetzten eines Benutzers abrufen. Der Ausgabewert wird in einer Variablen gespeichert.  <br/> **Hinweis:** Damit diese Aktion ordnungsgemäß arbeiten kann, muss der Benutzerprofildienst in SharePoint ausgeführt werden.           |
   

### <a name="document-set-actions"></a>Dokumentenmappenaktionen
<a name="section1e"> </a>

Einige Workflowaktionen sind nur verfügbar, wenn der Workflow mit einer Dokumentbibliothek, z. B. freigegebene Dokumente, oder mit dem Dokumentinhaltstyp verknüpft ist.
  
    
    




|**VISIO-AKTIONS-SHAPE**|**ENTSPRECHENDE AKTION IN SHAREPOINT DESIGNER**|**AKTIONSBESCHREIBUNG**|
|:-----|:-----|:-----|
|![Senden der Genehmigung für Dokumentensatz](../images/spd15-SendApproval4DocSet-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Genehmigungsvorgang für Dokumentenmappen starten** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Starten des Genehmigungsprozesses für Dokumentensatz](../images/spd15-SendApproval4DocSet-txt.JPG)|**Genehmigungsvorgang für Dokumentenmappen starten** <br/> Verwenden Sie diese Aktion, um den Genehmigungsprozess für eine Dokumentenmappe zu beginnen.  <br/> |
|![Senden des Dokumentensatzes an Repository](../images/spd15-SendDocSet2Repos-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Dokumentenmappe an Repository senden** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Senden des Dokumentensatzes an Repository](../images/spd15-SendDocSet2Repos-txt.JPG)|**Dokumentenmappe an Repository senden** <br/> Mithilfe dieser Aktion können Sie die Dokumentenmappe in ein Dokumentrepository verschieben oder kopieren. Ein Dokumentrepository kann eine Bibliothek auf Ihrer SharePoint-Website oder eine eigene Website wie das Dokumentcenter sein, das Datensätze anhand der von Ihnen definierten Regeln an ein bestimmtes Ziel weiterleitet.<br/> |
|![Senden des Dokuments an Repository](../images/spd15-SendDoc2Repos-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Dokument an Repository senden** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Senden des Dokuments an Repository](../images/spd15-SendDoc2Repos-txt.JPG)|**Dokument an Repository senden** <br/> Mithilfe dieser Aktion können Sie ein Dokument in ein Dokumentrepository verschieben oder kopieren. Ein Dokumentrepository kann eine Bibliothek auf Ihrer SharePoint-Website oder eine eigene Website wie das Dokumentcenter sein, das Datensätze anhand der von Ihnen definierten Regeln an ein bestimmtes Ziel weiterleitet.<br/> |
|![Festlegen des Inhaltsgenehmigungsstatus für Dokumentensatz](../images/spd15-SetContentApprStatus-visio.JPG)|Diese Visio-Aktion ist identisch mit der Aktion **Inhaltsgenehmigungsstatus für die Dokumentenmappe festlegen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Festlegen des Inhaltsgenehmigungsstatus für Dokumentensatz](../images/spd15-SetContentApprStatus4DocSet-txt.JPG)|**Inhaltsgenehmigungsstatus für die Dokumentenmappe festlegen** <br/> Verwenden Sie diese Aktion, um den Inhaltsgenehmigungsstatus für eine Dokumentenmappe auf **Genehmigt**, **Abgelehnt** oder **Ausstehend** festzulegen.  <br/> |
   

## <a name="workflow-conditions"></a>Workflowbedingungen
<a name="section2"> </a>

Eine Workflowbedingung ist ein Verzweigungspunkt im Workflow. Die Workflowbedingung vergleicht die Eingabe mit einem angegebenen Wert. Stimmen sie überein, folgt der Workflow einer Verzweigung. Wenn dies nicht der Fall ist, folgt er der anderen Verzweigung.
  
    
    

> **Wichtig:** Die meisten der Bedingungsshapes, die sich in Visio in SharePoint-Workflows einfügen lassen, erfordern zusätzliche Konfigurationsanpassungen, wenn der Workflow in SharePoint Designer importiert wird. Denken Sie daran, in Visio über die Kommentarfunktion der einzelnen Bedingungsshapes die Entscheidungskriterien der Bedingung zu vermerken. 
  
    
    


### <a name="general-conditions"></a>Allgemeine Bedingungen

In diesem Abschnitt werden die Bedingungen beschrieben, die in SharePoint Designer 2013 für Listen und wiederverwendbare Listenworkflows verfügbar sind, unabhängig davon, mit welchem Listen- oder Inhaltstyp der Workflow verküpft ist.
  
    
    




|**VISIO-BEDINGUNGS-SHAPE**|**ENTSPRECHENDE BEDINGUNG IN SHAREPOINT DESIGNER**|**BESCHREIBUNG DER BEDINGUNG**|
|:-----|:-----|:-----|
|![Vergleichen der Datenquelle](../images/spd15-CompareDataSrc-visio.JPG)|Diese Visio-Bedingung ist identisch mit der Bedingung **Wenn ein beliebiger Wert gleich dem Wert ist** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![If-Wert entspricht Wert](../images/spd15-CompareDataSrc-txt.JPG)|**Datenquelle vergleichen** <br/> Diese Bedingung vergleicht zwei Werte. Sie können angeben, ob die Werte gleich oder nicht gleich sein sollen.<br/> |
|![Vergleichen des Dokumentfelds](../images/spd15-CompareDocField-visio.JPG)|Diese Visio-Bedingung ist identisch mit der Bedingung **Wenn das aktuelle Elementfeld gleich Wert ist** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Wenn aktuelles Elementfeld dem Wert entspricht](../images/spd15-CompareDocField-txt.JPG)|**Dokumentfeld vergleichen** <br/> Diese Bedingung vergleicht ein Feld mit einem Wert, den Sie angeben. Sie können angeben, ob die Werte gleich oder nicht gleich sein sollen.<br/> |
|![Von einer bestimmten Person erstellt](../images/spd15-CreatedBySpecPerson-visio.JPG)|Diese Visio-Bedingung ist identisch mit der Bedingung **Erstellt von einer bestimmten Person** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Wenn von bestimmter Person erstellt](../images/spd15-CreatedBySpecPerson-txt.JPG)|**Erstellt von einer bestimmten Person** <br/> Diese Bedingung überprüft, ob ein Element von einem bestimmten Benutzer erstellt wurde. Der Benutzer kann als E-Mail-Adresse, z. B. olivier@contoso.com, angegeben oder aus SharePoint-, Exchange- oder Active Directory-Benutzern ausgewählt werden.<br/> **Hinweis:** Bei Benutzernamen und E-Mail-Adressen ist die Groß- und Kleinschreibung zu beachten. Wir empfehlen Ihnen, einen Benutzernamen oder eine E-Mail-Adresse auszuwählen, um die korrekte Groß- und Kleinschreibung zu gewährleisten. Bei der manuellen Eingabe eines Benutzernamens oder einer E-Mail-Adresse müssen Sie die für das Konto verwendete Groß- und Kleinschreibung beachten. So wird die Bedingung „If created by contoso\\molly“ beispielsweise nicht als „true“ ausgewertet, wenn der Name des Benutzerkontos „Contoso\\Molly“ lautet.           |
|![Created in specific data span](../images/spd15-CreatedInSpecDateSpan-visio.JPG)|Diese Visio-Bedingung ist identisch mit der Bedingung **Erstellt in einer bestimmten Zeitspanne** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Wenn in einem bestimmten Zeitabschnitt erstellt](../images/spd15-CreatedInSpecDateSpan-txt.JPG)|**Erstellt in einer bestimmten Zeitspanne** <br/> Diese Bedingung überprüft, ob das Element zwischen den Datumsangaben erstellt wurde. Sie können das aktuelle Datum, ein bestimmtes Datum oder einen Nachschlagewert verwenden.<br/> |
|![Von einer bestimmten Person geändert](../images/spd15-ModifiedBySpecPerson-visio.JPG)|Diese Visio-Bedingung ist identisch mit der Bedingung **Geändert von einer bestimmten Person** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Wenn von einer bestimmten Person geändert](../images/spd15-ModifiedBySpecPerson-txt.JPG)|**Geändert von einer bestimmten Person** <br/> Verwenden Sie diese Bedingung, um zu überprüfen, ob ein Element von einem bestimmten Benutzer geändert wurde. Der Benutzer kann als E-Mail-Adresse, z. B. olivier@contoso.com, angegeben oder aus SharePoint-, Exchange- oder Active Directory-Benutzern ausgewählt werden.<br/> **Hinweis:** Bei Benutzernamen und E-Mail-Adressen ist die Groß- und Kleinschreibung zu beachten. Wir empfehlen Ihnen, einen Benutzernamen oder eine E-Mail-Adresse auszuwählen, um die korrekte Groß- und Kleinschreibung zu gewährleisten. Bei der manuellen Eingabe eines Benutzernamens oder einer E-Mail-Adresse müssen Sie die für das Konto verwendete Groß- und Kleinschreibung beachten. Beispielsweise wird die Bedingung „If modified by contoso\\molly“ nicht als „true“ ausgewertet, wenn der Name des Benutzerkontos „Contoso\\Molly“ lautet.           |
|![Geändert in einer bestimmten Zeitspanne](../images/spd15-ModifiedInSpecDateSpan-visio.JPG)|Diese Visio-Bedingung ist identisch mit der Bedingung **Geändert in einer bestimmten Zeitspanne** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Wenn in einem bestimmten Zeitabschnitt geändert](../images/spd15-ModifiedInSpecDateSpan-txt.JPG)|**Geändert in einer bestimmten Zeitspanne** <br/> Diese Bedingung überprüft, ob ein Element zwischen den Datumsangaben geändert wurde. Sie können das aktuelle Datum, ein bestimmtes Datum oder einen Nachschlagewert verwenden.<br/> |
|![Titelfeld enthält Stichwörter](../images/spd15-TitleFieldKeywords-visio.JPG)|Diese Visio-Bedingung ist identisch mit der Bedingung **Titelfeld enthält Schlüsselwörter** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Wenn Titelfeld Stichwörter enthält](../images/spd15-TitleFieldKeywords-txt.JPG)|**Titelfeld enthält Schlüsselwörter** <br/> Diese Bedingung überprüft, ob das Feld **Title** eines Elements ein bestimmtes Wort enthält. Sie können das Schlüsselwort entweder im Zeichenfolgengenerator angeben (als statischen Wert, als dynamische Zeichenfolge oder als Kombination beider Varianten) oder einen Verweis auf ein Feld oder eine Variable einfügen. <br/> **Hinweis:** Mit der Bedingung **Titelfeld enthält Schlüsselwörter** lässt sich nur nach einem einzigen Schlüsselwort suchen. Sie können jedoch logische Operatoren verwenden, beispielsweise **||** (oder) oder **&amp;&amp;** (und).          |
   

### <a name="document-set-conditions"></a>Bedingungen für Dokumentenmappen

Einige Workflowbedingungen sind nur verfügbar, wenn der Workflow mit einer Dokumentbibliothek, z. B. freigegebene Dokumente, oder mit dem Dokumentinhaltstyp verknüpft ist.
  
    
    


|**VISIO-BEDINGUNGS-SHAPE**|**ENTSPRECHENDE BEDINGUNG IN SHAREPOINT DESIGNER**|**BESCHREIBUNG DER BEDINGUNG**|
|:-----|:-----|:-----|
|![Dateigröße liegt in einem bestimmten Bereich](../images/spd15-FileSzInSpecRange-visio.JPG)|Diese Visio-Bedingung ist identisch mit der Bedingung **Die Dateigröße in einem bestimmten KB-Bereich** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Dateigröße liegt in einem bestimmten Bereich](../images/spd15-FileSzInSpecRange-txt.JPG)|**Die Dateigröße in einem bestimmten KB-Bereich** <br/> Diese Bedingung überprüft, ob die Dateigröße eines Dokuments zwischen den angegebenen Größen liegt (in KB). Die Bedingung schließt die angegebenen Größenwerte nicht in die Auswertung mit ein. Sie können eine Zahl eingeben oder einen Nachschlagewert für die erste oder zweite Größe in der Bedingung verwenden.<br/> |
|![Datei ist ein bestimmter Typ](../images/spd15-FileIsSpecType-visio.JPG)|Diese Visio-Bedingung ist identisch mit der Bedingung **Der Dateityp weist einen bestimmten Typ auf** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Datei ist ein bestimmter Typ](../images/spd15-FileIsSpecType-txt.JPG)|**Der Dateityp weist einen bestimmten Typ auf** <br/> Diese Bedingung überprüft, ob der Dateityp des aktuellen Elements dem angegebenen Typ entspricht, z. B. DOCX. Sie können den Dateityp als Zeichenfolge eingeben oder einen Nachschlagewert verwenden.<br/> |
   

### <a name="list-conditions"></a>Listenbedingungen


  
    
    




|**VISIO-BEDINGUNGS-SHAPE**|**ENTSPRECHENDE BEDINGUNG IN SHAREPOINT DESIGNER**|**BESCHREIBUNG DER BEDINGUNG**|
|:-----|:-----|:-----|
|![Überprüfen genauer Benutzerberechtigungen](../images/spd15-ChkExactUserPerms-visio.JPG)|Diese Visio-Bedingung ist identisch mit der Bedingung **Listenelement-Berechtigungsstufen überprüfen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Überprüfen von Berechtigungsebenen für Listenelement](../images/spd15-ChkExactUserPerms-txt.JPG)|**Exakte Benutzerberechtigungen überprüfen** <br/> Diese Bedingung überprüft, ob der angegebene Benutzer über die minimal erforderliche Berechtigungsstufe verfügt.  <br/> |
|![Überprüfen von Benutzerberechtigungen](../images/spd15-ChkUserPerms-visio.JPG)|Diese Visio-Bedingung ist identisch mit der Bedingung **Listenelementberechtigungen überprüfen** in SharePoint Designer 2013 und wird angezeigt als: <br/> ![Überprüfen von Listenelementberechtigungen](../images/spd15-ChkUserPerms-txt.JPG)|**Benutzerberechtigung überprüfen** <br/> Diese Bedingung überprüft, ob der angegebene Benutzer über die minimal erforderlichen Berechtigungen verfügt.  <br/> |
   

## <a name="workflow-terminators"></a>Workflowabschlusszeichen
<a name="section3"> </a>

In Visio muss jeder Workflow mit einem Start-Abschlusszeichen (![Start](../images/spd15-WFStart-icon.JPG)) beginnen und mit einem Stop-Abschlusszeichen (![Stop](../images/spd15-WFStop-icon.JPG)) enden. In einem Workflow kann jeweils nur ein Typ von Abschlusszeichen verwendet werden. Abschlusszeichen sind erforderlich, wenn Sie einen SharePoint-Workflow in Visio erstellen, damit der Workflow die Validierung besteht und exportiert werden kann. Workflowabschlusszeichen werden in SharePoint Designer nicht verwendet.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Neuerungen in Workflows für SharePoint](what-s-new-in-workflows-for-sharepoint.md)
    
  
-  [Erste Schritte mit Workflows in SharePoint](get-started-with-workflows-in-sharepoint.md)
    
  
-  [Workflowentwicklung in SharePoint Designer und Visio](workflow-development-in-sharepoint-designer-and-visio.md)
    
  

  
    
    
