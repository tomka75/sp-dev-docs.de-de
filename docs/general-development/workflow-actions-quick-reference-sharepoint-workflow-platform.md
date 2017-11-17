---
title: "Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: eb3434e5-bc75-4474-8873-4980062fd29c
ms.openlocfilehash: d480b0d6f2a34e046ecbc3ddf976fcc21da8c2a4
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="workflow-actions-quick-reference-sharepoint-workflow-platform"></a>Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)
In dieser Übersicht werden die Workflowaktionen, die im aktuellen Build von SharePoint Designer 2013 unterstützt werden, sowie nicht verfügbare Workflowaktionen aufgeführt.
## <a name="workflow-actions-in-sharepoint-designer-2013"></a>Workflowaktionen in SharePoint Designer 2013
<a name="bkm_WorkflowActions"> </a>

Es folgt eine Referenz für Workflowaktionen, die für die SharePoint-Workflowplattform verfügbar sind. Zusätzlich zur SharePoint-Workflowplattform unterstützt SharePoint Designer 2013 auch die SharePoint 2010-Workflowplattform. Workflowaktionen für die 2010-Plattform finden Sie unter  [Kurzübersicht zu Workflowaktionen (SharePoint 2010-Workflowplattform)](workflow-actions-quick-reference-sharepoint-2010-workflow-platform.md)
  
    
    

### <a name="core-actions"></a>Hauptaktionen
<a name="bkm_CoreActions"> </a>

Als Hauptaktionen werden die am häufigsten durchgeführten Aktionen bezeichnet, und sie sind für einfachen Zugriff gruppiert. 
  
    
    

**Tabelle 1. Übersicht über Hauptaktionen**


|**Aktion**|**Beschreibung**|
|:-----|:-----|
|Kommentar hinzufügen  <br/> |Ermöglicht Ihnen, im Workflow-Designer zu Referenzzwecken informative Kommentare zu hinterlassen. Dies ist besonders hilfreich, wenn andere Benutzer an diesem Workflow mitarbeiten.  <br/> |
|Zeit zum Datum hinzufügen  <br/> |Fügt einem Datum (Jahr wird nicht unterstützt) eine bestimmte Uhrzeit in Minuten, Stunden, Tagen oder Monaten hinzu und speichert den Ausgabewert als Variable. Das Datum kann ein aktuelles Datum, ein bestimmtes Datum oder ein Nachschlagewert sein. Der Wert "Aktuelles Datum" gibt Mitternacht (UTC) zurück.  <br/> |
|Wörterbuch erstellen  <br/> |Erstellt eine Wörterbuchvariable von Schlüssel-/Wertpaaren.  <br/> **Hinweis:** Das Wörterbuch verwendet zum Speichern von Daten die JSON-Schreibweise.           Weitere Informationen zur Wörterbuchvariable finden Sie unter [Verstehen von Wörterbuchaktionen in SharePoint Designer 2013](understanding-dictionary-actions-in-sharepoint-designer.md). <br/> |
|HTTP-Webdienst aufrufen  <br/> |Dient als Methodenaufruf an einen HTTP-Webdienst und gibt Daten im JSON-Format zurück. Einfache Authentifizierung wird über den Anforderungsheader unterstützt.  <br/> Weitere Informationen zur Wörterbuchvariable finden Sie unter  [Grundlegendes zu Wörterbuchaktionen in SharePoint Designer 2013](understanding-dictionary-actions-in-sharepoint-designer.md) <br/> |
|Elemente in einem Wörterbuch zählen  <br/> |Gibt die Anzahl der Elemente in einem angegebenen Wörterbuch zurück  <br/> |
|Berechnung ausführen  <br/> |Führt eine arithmetische Berechnung durch und speichert den Ausgabewert in einer Variablen.  <br/> **Hinweis:** In SharePoint unterstützt diese Aktion nur den nummerischen Typ **Double**. Ganze Zahlen werden nicht unterstützt. Die Verwendung des Operators "+" (Verkettung) für Zeichenfolgen wird nicht unterstützt.          |
|Ein Element aus einem Wörterbuch abrufen  <br/> |Gibt ein bestimmtes Element aus der Wörterbuchvariable zurück  <br/> |
|In Verlaufsliste protokollieren  <br/> |Schreibt eine Nachricht aus einer Liste vordefinierter Nachrichtenelemente in die Workflowverlaufsliste  <br/> |
|Für Dauer anhalten  <br/> |Hält die Ausführung eines Workflows für ein in Tagen, Stunden und Minuten angegebenes Zeitintervall an  <br/> |
|Bis Datum anhalten  <br/> |Hält die Ausführung eines Workflows bis zu einem angegebenen Datum-/Uhrzeitwert an  <br/> |
|E-Mail senden  <br/> |Sendet bei Auftreten eines bestimmten Workflowereignisses automatisch eine E-Mail-Nachricht, die eine vordefinierte Nachricht an einen Benutzer oder eine Gruppe enthält.  <br/> **Wichtig:** Wenn die Website nicht der Liste vertrauenswürdiger Websites hinzugefügt wurde, werden E-Mails an den Junk-E-Mail-Ordner von Outlook weitergeleitet.           |
|Den Zeitbereich des Felds „Datum/Uhrzeit“ festlegen  <br/> |Erstellt einen Zeitstempel und speichert den Ausgabewert in einer Variablen. Sie können die Uhrzeit in Stunden und Minuten festlegen und ein aktuelles Datum, ein bestimmtes Datum oder einen Nachschlagewert festlegen.  <br/> |
|Workflowstatus festlegen  <br/> |Legt den Status des Workflows fest  <br/> |
|Workflowvariable festlegen  <br/> |Legt eine Workflowvariable auf einen Wert fest. Sie können diese Aktion auch verwenden, wenn der Workflow einer Variablen Daten zuweisen soll.  <br/> |
|Go to Stage (Wechseln zu Phase)  <br/> |Gibt die nächste Phase an, an welche die Ablaufsteuerung übergeben werden sollte  <br/> |
   

### <a name="coordination-actions"></a>Koordinationsaktionen
<a name="bkm_CoreActions"> </a>

Koordinationsaktionen werden verwendet, um einen auf der SharePoint 2010-Workflowplattform basierten Workflow aufzurufen. Weitere Informationen zu Koordinationsaktionen finden Sie unter  [Grundlegendes zur Koordination Aktionen in SharePoint Designer 2013](understanding-coordination-actions-in-sharepoint-designer.md)
  
    
    

**Tabelle 2. Übersicht über Koordinationsaktionen**


|**Aktion**|**Beschreibung**|
|:-----|:-----|
|Listenworkflow starten  <br/> |Starten Sie einen auf der SharePoint 2010-Workflowplattform basierenden Listenworkflow.  <br/> **Hinweis:** „Listenworkflow starten“ weist die folgenden Probleme auf:> Das Feld für den Zuordnungstyp kann nicht als Parameter verwendet werden, wenn der 2010-Workflow eine TaskProcess-Aktion beinhaltet.> Wenn mehrere Aufrufe für den gleichen 2010-Workflow ausgeführt werden, werden mehrere Datenquellen in der 2013-Workflow-Suchfunktion ausgegeben. Diese Datenquellen sind alle gleich.> Variablennamen in 2013 dürfen keine Sonderzeichen, wie z. B. „?“ und „#“, enthalten. Wenn ein 2010-Workflow Sonderzeichen enthält, werden Sie im 2013-Workflow in Hexadezimalcode umgewandelt.          |
|Website-Workflow starten  <br/> |Starten Sie einen auf der SharePoint 2010-Workflowplattform basierenden Seitenworkflow.  <br/> **Hinweis:** „Listenworkflow starten“ weist die folgenden Probleme auf:> Das Feld für den Zuordnungstyp kann nicht als Parameter verwendet werden, wenn der 2010-Workflow eine TaskProcess-Aktion beinhaltet.> Wenn mehrere Aufrufe für den gleichen 2010-Workflow ausgeführt werden, werden mehrere Datenquellen in der 2013-Workflow-Suchfunktion ausgegeben. Diese Datenquellen sind alle gleich.> Variablennamen in 2013 dürfen keine Sonderzeichen, wie z. B. „?“ und „#“, enthalten. Wenn ein 2010-Workflow Sonderzeichen enthält, werden Sie im 2013-Workflow in Hexadezimalcode umgewandelt.          |
   

### <a name="list-actions"></a>Listenaktionen
<a name="bkm_ListActions"> </a>

Listenaktionen gruppieren Aktionen, die zum Bearbeiten von Listen und Listenelementen verwendet werden
  
    
    

**Tabelle 3. Übersicht über Listenaktionen**


|**Aktion**|**Beschreibung**|
|:-----|:-----|
|Element einchecken  <br/> |Checkt ein ausgechecktes Element ein. Sie können nur Elemente aus einer Dokumentbibliothek einchecken.  <br/> **Vorsicht:** Der Workflow stürzt ab, wenn Sie versuchen, ein nicht ausgechecktes Element einzuchecken.           |
|Element auschecken  <br/> |Checkt ein Element aus. Der Workflow prüft, ob das Element eingecheckt ist, bevor er ein Dokument auscheckt. Sie können nur Elemente aus einer Bibliothek in Ihrer Website auschecken.  <br/> **Vorsicht:** Der Workflow stürzt ab, wenn Sie versuchen, ein nicht eingechecktes Element auszuchecken.           |
|Dokument kopieren  <br/> |Kopiert ein Dokument aus der aktuellen Liste in eine andere Dokumentbibliotheksliste.  <br/> |
|Listenelement erstellen  <br/> |Erstellt in der von Ihnen angegebenen Liste ein neues Listenelement. Sie können die Felder und Werte im neuen Element angeben. Sie können diese Aktion verwenden, wenn Sie ein neues Element mit bestimmten Informationen erstellen möchten.  <br/> |
|Element löschen  <br/> |Löscht ein Element.  <br/> **Hinweis:** Diese Aktion wird auf dem Computer beendet, auf dem das Workflow-Manager-Workflowmodul ausgeführt wird, und gibt eine **System.InvalidOperationException**-Ausnahme aus. Für dieses Problem ist keine Umgehung verfügbar.          |
|Auschecken des Elements verwerfen  <br/> |Verwirft die Änderungen und checkt das Element wieder ein, wenn ein Element ausgecheckt wurde und Änderungen daran vorgenommen wurden.  <br/> **Vorsicht:** Der Workflow stürzt ab, wenn Sie versuchen, ein nicht ausgechecktes Element einzuchecken.           |
|Feld im aktuellen Element festlegen  <br/> |Legt ein bestimmtes Feld im aktuellen Element auf einen bestimmten Wert fest.  <br/> **Hinweis:** Wenn Sie möchten, dass der Workflow angehalten wird, bis der Wert des Felds geändert wurde, verwenden Sie anstatt dieser Aktion die Aktion **Auf Ereignis in Listenelement warten**.          |
|Dokument übersetzen  <br/> |Übersetzt ein Dokument in eine bestimmte Sprache.  <br/> **Hinweis:** Eine vorkonfigurierte maschinelle Übersetzungsdienstanwendung ist erforderlich.           |
|Listenelement aktualisieren  <br/> |Aktualisiert ein Listenelement. Sie können die Felder und die neuen Werte in diesen Feldern angeben.  <br/> |
|Auf Ereignis in Listenelement warten  <br/> |[Verbesserte Version der Office 2010-Aktion.] Hält die aktuelle Instanz des Workflows an und wartet auf ein angegebenes Listenelementereignis. Diese Aktion überwacht zwei Ereignisse: **ItemUpdated** und **ItemAdded**.  <br/> |
|Auf Feldänderung im aktuellen Element warten  <br/> |Wartet, bis ein Feld im aktuellen Element einem bestimmten Wert entspricht  <br/> |
   

### <a name="project-actions"></a>Projektaktionen
<a name="bkm_ProjectActions"> </a>

Projektaktionen unterstützen die Integration von Microsoft Project. Sie werden zur Erstellung von Workflows auf der Basis von Project verwendet. Alle Projektaktionen in SharePoint Designer 2013 sind neu.
  
    
    

**Tabelle 4. Referenz zu Projektaktionen**


|**Aktion**|**Beschreibung**|
|:-----|:-----|
|Projekt aus dem aktuellen Element erstellen  <br/> |Erstellt auf Basis des aktuellen Elements auf der PWA-Website der SharePoint-Farm ein neues Projekt  <br/> |
|Projektfeld festlegen  <br/> |Legt für ein bestimmtes Feld auf Project Server einen Wert fest.  <br/> **Hinweis:** Für diesen Vorgang muss das Projekt erst eingecheckt werden. Wenn das Projekt nicht eingecheckt ist, wird der Workflow beendet, und Benutzer können das Projekt in Project Web App nicht öffnen.           |
|Status der Projektstufe festlegen  <br/> |Legt den Status der Projektstufe fest.  <br/> **Hinweis:** Wenn das aktuelle Projekt ausgecheckt ist, tritt eine Ausnahme auf.           |
|Statusfeld in Ideenliste festlegen  <br/> |Aktualisiert den Status für das ursprüngliche Listenelement, das mit dem aktuellen Projekt verknüpft ist  <br/> |
|Auf Projektereignis warten  <br/> |Wartet auf ein bestimmtes Projektereignis  <br/> |
   

### <a name="task-actions"></a>Aufgabenaktionen
<a name="bkm_TaskActions"> </a>

Mit Aufgabenaktionen kann ein auf der SharePoint 2010-Workflowplattform basierter Workflow in einem auf der SharePoint-Workflow-Plattform basierten Workflow aufgerufen werden.
  
    
    

**Tabelle 5. Übersicht über Aufgabenaktionen**


|**Aktion**|**Beschreibung**|
|:-----|:-----|
|Aufgabe zuweisen  <br/> |Weist einem Benutzer eine Workflowaufgabe zu und erstellt ein Fälligkeitsdatum für den Abschluss der Aufgabe  <br/> |
|Aufgabenprozess starten  <br/> |Erstellt Aufgaben für mehrere Benutzer und erlaubt, die Aufgaben einen benutzerdefinierten Prozess durchlaufen zu lassen  <br/> |
   

### <a name="utility-actions"></a>Hilfsaktionen
<a name="bkm_UtilityActions"> </a>

Hilfsaktionen sind Aktionen, die Zeichenfolgen bearbeiten oder das Intervall zwischen Daten suchen. 
  
    
    

**Tabelle 6. Übersicht über Hilfsaktionen**


|**Aktion**|**Beschreibung**|
|:-----|:-----|
|Teilzeichenfolge vom Ende der Zeichenfolge extrahieren  <br/> |Kopiert eine bestimmte Anzahl von Zeichen, beginnend am Ende einer Zeichenfolge, und speichert die Ausgabe in einer Variablen  <br/> |
|Teilzeichenfolge anhand des Index der Zeichenfolge extrahieren  <br/> |Kopiert eine Teilzeichenfolge, beginnend bei einem angegebenen Index in der Zeichenfolge, und speichert den Wert in einer Variablen.  <br/> **Hinweis:** Beachten Sie, dass Werte in SharePoint Designer 2010 mit 1 beginnend indiziert wurden, auch wenn der Indexwert in Microsoft SharePoint Designer 2013 nullbasiert ist.           |
|Teilzeichenfolge vom Anfang der Zeichenfolge extrahieren  <br/> |Kopiert eine bestimmte Anzahl von Zeichen, beginnend am Anfang einer Zeichenfolge, und speichert die Ausgabe in einer Variablen  <br/> |
|Teilzeichenfolge der Zeichenfolge anhand des Index mit bestimmter Länge extrahieren  <br/> |Kopiert eine aus einer bestimmten Anzahl von Zeichen bestehende Teilzeichenfolge heraus, beginnend bei einem angegebenen Index in der Zeichenfolge, und speichert den Wert in einer Variablen.  <br/> **Hinweis:** Beachten Sie, dass Werte in SharePoint Designer 2010 mit 1 beginnend indiziert wurden, auch wenn der Indexwert in Microsoft SharePoint Designer 2013 nullbasiert ist.           |
|Intervall zwischen Daten suchen  <br/> |Berechnet das Zeitintervall zwischen zwei Daten in Minuten, Stunden oder Tagen und speichert die Ausgabe in einer Variablen  <br/> |
|Zeichenfolge kürzen  <br/> |Entfernt Leerzeichen am Beginn und Ende einer Zeichenfolge  <br/> |
|Teilzeichenfolge in Zeichenfolge suchen  <br/> |Sucht eine bestimmte Teilzeichenfolge in einer Zeichenfolge und gibt den Index der Startposition der Teilzeichenfolge zurück  <br/> |
|Teilzeichenfolge in Zeichenfolge ersetzen  <br/> |Ersetzt eine bestimmte Teilzeichenfolge durch eine andere Teilzeichenfolge  <br/> |
|Zeichenfolge kürzen  <br/> |Entfernt Leerzeichen am Beginn und Ende einer Zeichenfolge  <br/> |
   

## <a name="workflow-actions-that-are-deprecated-in-sharepoint"></a>Workflowaktionen, die in SharePoint nicht mehr verwendet werden
<a name="bkm_NotAvailable"> </a>

Eine Liste der Aktionen aus SharePoint 2010, die in SharePoint nicht mehr verwendet werden und nicht verfügbar sind, finden Sie unter  [Verwendung der Interop-Workflow-Brücke verfügbar Workflowaktionen](workflow-actions-available-using-the-workflow-interop-bridge.md).
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bkm_addlresource"> </a>


-  [Workflowaktions- und -aktivitätenreferenz für SharePoint](workflow-actions-and-activities-reference-for-sharepoint.md)
    
  
-  [Grundlegendes zu SharePoint-Workflows](sharepoint-workflow-fundamentals.md)
    
  
-  [Erste Schritte mit Workflows in SharePoint](get-started-with-workflows-in-sharepoint.md)
    
  
-  [Workflowentwicklung in SharePoint Designer und Visio](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
