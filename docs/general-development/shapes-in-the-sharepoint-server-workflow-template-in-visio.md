---
title: Formen in der SharePoint Server-Workflowvorlage in Visio
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f35bdf5d-c102-4e2d-8a23-1d2df17155b9
ms.openlocfilehash: 0ef12568c05e15ea3bf65ab48cff095128e3f96f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="shapes-in-the-sharepoint-server-workflow-template-in-visio"></a>Formen in der SharePoint Server-Workflowvorlage in Visio
In diesem Artikel erfahren Sie mehr über die Shapes in der SharePoint-Workflowvorlage in Visio 2013.
## <a name="introduction"></a>Einführung
<a name="VSSPD_Shapes_Intro"> </a>

In diesem Artikel sind die Shapes aufgelistet, die in der SharePoint-Workflowvorlage in Visio 2013 und im Visual Designer in SharePoint Designer 2013 enthalten sind. Wenn die Vorlage geöffnet wird, öffnet auch die Schablonen für SharePoint-Workflowaktionen, SharePoint-Workflowbedingungen und SharePoint-Workflow-Abschlusszeichen. Viele der in den Schablonen aufgeführten Shapes entsprechen bestimmten Aktionen, Bedingungen oder anderen logischen Konstrukten im Declarative Designer zum Erstellen von Workflows in SharePoint Designer 2013.
  
    
    

> **Wichtig:** Nachfolgend finden Sie einen Überblick über die in SharePoint Designer 2013 unterstützten Workflowaktionen. Die meisten dieser Aktionen standen bereits in SharePoint Designer 2010 zur Verfügung. Nur die Aktion „Wait for List Item Event“ wurde in der aktuellen Version überarbeitet und verbessert. Zudem wurden in der neuen Version zwölf neue Aktionen eingeführt und 25 Aktionen entfernt. (Eine Liste aller entfernten Aktionen, Bedingungen und Sperren finden Sie unter [Workflow actions available using the workflow interop bridge](workflow-actions-available-using-the-workflow-interop-bridge.md). 
  
    
    


## <a name="action-shapes"></a>Aktionsshapes
<a name="VSSDP_Actions"> </a>

Die folgende Tabelle enthält eine Liste aller Shapes, die in der SharePoint-Aktionsschablone in der SharePoint-Workflowvorlage in Visio 2013 enthalten sind.
  
    
    

> **Hinweis:** Jedes in der nachfolgenden Tabelle aufgelistete Shape verfügt über die aufgeführten Eigenschaften sowie eine Eigenschaft **Properties**.
  
    
    



|**Shapes in Visio 2013 und SharePoint Designer 2013 Visual Designer**|**Aktion im SharePoint Designer 2013 Declarative Designer**|**Eigenschaften im SharePoint Designer 2013 Visual Designer**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Kommentar hinzufügen  <br/> |**Kommentar hinzufügen** <br/> |**Kommentar** <br/> |Ermöglicht Ihnen, im Workflow-Designer zu Referenzzwecken informative Kommentare zu hinterlassen. Dies ist besonders hilfreich, wenn andere Benutzer an diesem Workflow mitarbeiten.  <br/> |
|Zeit zum Datum hinzufügen  <br/> |**Zeit zum Datum hinzufügen** <br/> |**Monate** <br/> **Tage** <br/> **Stunden** <br/> **Minuten** <br/> **Date** <br/> **Ausgabe** <br/> |Fügt einem Datum eine bestimmte Uhrzeit in Minuten, Stunden, Tagen oder Monaten hinzu und speichert den Ausgabewert als Variable. Das Datum kann ein aktuelles Datum, ein bestimmtes Datum oder ein Nachschlagewert sein. Der Wert "Aktuelles Datum" gibt Mitternacht (UTC) zurück.  <br/> |
|Aufgabe zuweisen  <br/> |**Aufgabe zuweisen** <br/> |**Aufgabeneinstellungen** <br/> **Ergebnis des Vorgangs** <br/> **Aufgabenelement-ID** <br/> |Weist einem Benutzer eine Workflowaufgabe zu und erstellt ein Fälligkeitsdatum für den Abschluss der Aufgabe  <br/> |
|HTTP-Webdienst aufrufen  <br/> |**HTTP-Webdienst aufrufen** <br/> |**HTTP-Anforderung** <br/> **Parameter** <br/> **Antwortinhaltsvariable** <br/> **Antwortkopfzeilenvariable** <br/> **Antwortcodevariable** <br/> |Fungiert als Methodenaufruf an einen HTTP-Webdienst.  <br/> **Hinweis:** Der aktuelle Build unterstützt ausschließlich SharePoint-Aufrufe an **anonyme** HTTP-Dienste und ausschließlich Aufrufe mit Parametern des Typs **string** und Rückgabetypen. Darüber hinaus werden XML-Verbundelemente nicht unterstützt. Ebenso wird lediglich der klassische ASMX unterstützt, nicht jedoch der WCG-Dienst.          |
|Element einchecken  <br/> |**Element einchecken** <br/> |**Element** <br/> **Kommentar** <br/> |Checkt ein ausgechecktes Element ein. Sie können nur Elemente aus einer Dokumentbibliothek einchecken.  <br/> **Vorsicht:** Der Workflow stürzt ab, wenn Sie versuchen, ein nicht ausgechecktes Element einzuchecken.           |
|Element auschecken  <br/> |**Element auschecken** <br/> |**Element** <br/> |Checkt ein Element aus. Der Workflow prüft, ob das Element eingecheckt ist, bevor er ein Dokument auscheckt. Sie können nur Elemente aus einer Bibliothek in Ihrer Website auschecken.  <br/> **Vorsicht:** Der Workflow stürzt ab, wenn Sie versuchen, ein nicht eingechecktes Element auszuchecken.           |
|Dokument kopieren  <br/> |**Dokument kopieren** <br/> |**Dokument** <br/> **Bibliothek** <br/> |Kopiert ein Dokument aus der aktuellen Liste in eine andere Dokumentbibliotheksliste.  <br/> |
|Elemente im Wörterbuch zählen  <br/> |**Elemente im Wörterbuch zählen** <br/> |**Wörterbuch** <br/> **Ausgabevariable** <br/> |Zählt die Anzahl der Elemente in einer Wörterbuchvariablen.  <br/> |
|Projekt aus dem aktuellen Element erstellen  <br/> |**Projekt aus dem aktuellen Element erstellen** <br/> |**Enterprise-Projekttyp** <br/> |Erstellt auf Basis des aktuellen Elements auf der PWA-Website der SharePoint-Farm ein neues Projekt  <br/> |
|Listenelement erstellen  <br/> |**Listenelement erstellen** <br/> |**Element** <br/> **Ausgabevariable** <br/> |Erstellt in der von Ihnen angegebenen Liste ein neues Listenelement. Sie können die Felder und Werte im neuen Element angeben. Sie können diese Aktion verwenden, wenn Sie ein neues Element mit bestimmten Informationen erstellen möchten.  <br/> |
|Element löschen  <br/> |**Element löschen** <br/> |**Element** <br/> |Löscht ein Element.  <br/> **Hinweis:** Diese Aktion wird auf dem Computer beendet, auf dem das Workflowmodul Workflow-Manager ausgeführt wird, und löst eine Ausnahme des Typs **System.InvalidOperationException** aus. Eine Problemumgehung ist derzeit nicht verfügbar.          |
|Auschecken verwerfen  <br/> |**Auschecken des Elements verwerfen** <br/> |**Element** <br/> |Verwirft die Änderungen und checkt das Element wieder ein, wenn ein Element ausgecheckt und verändert wurde.  <br/> **Vorsicht:** Der Workflow stürzt ab, wenn Sie versuchen, ein nicht ausgechecktes Element einzuchecken.           |
|Berechnung ausführen  <br/> |**Berechnung ausführen** <br/> |**LeftOperand** <br/> **Operator** <br/> **RightOperand** <br/> **Bis** <br/> |Führt eine arithmetische Berechnung durch und speichert den Ausgabewert in einer Variablen.  <br/> **Hinweis:** In SharePoint unterstützt diese Aktion nur den numerischen Typ **Double**. Ganze Zahlen werden nicht unterstützt. Die Verwendung des Operators „+“ (Verkettung) für Zeichenfolgen wird nicht unterstützt.          |
|Teilzeichenfolge ab dem Ende der Zeichenfolge extrahieren  <br/> |**Teilzeichenfolge ab dem Ende der Zeichenfolge extrahieren** <br/> |**Anzahl der Zeichen** <br/> **String** <br/> **Ausgabe** <br/> |Kopiert eine bestimmte Anzahl von Zeichen, beginnend am Ende einer Zeichenfolge, und speichert die Ausgabe in einer Variablen  <br/> |
|Teilzeichenfolge anhand des Index der Zeichenfolge extrahieren  <br/> |**Teilzeichenfolge ab Index der Zeichenfolge extrahieren** <br/> |**String** <br/> **Index** <br/> **Ausgabe** <br/> |Kopiert eine Teilzeichenfolge beginnend bei einem angegebenen Index in der Zeichenfolge und speichert den Wert in einer Variablen.  <br/> **Hinweis:** Der Indexwert im vorhandenen Build (Technical Preview) von SharePoint Designer ist nullbasiert. Werte in SharePoint Designer 2010 wurden allerdings mit 1 beginnend indiziert.           |
|Teilzeichenfolge ab Anfang der Zeichenfolge extrahieren  <br/> |**Teilzeichenfolge ab Anfang der Zeichenfolge extrahieren** <br/> |**Anzahl der Zeichen** <br/> **String** <br/> **Ausgabe** <br/> |Kopiert eine bestimmte Anzahl von Zeichen, beginnend am Anfang einer Zeichenfolge, und speichert die Ausgabe in einer Variablen  <br/> |
|Teilzeichenfolge der Zeichenfolge anhand des Index mit bestimmter Länge extrahieren  <br/> |**Teilzeichenfolge der Zeichenfolge anhand des Index mit bestimmter Länge extrahieren** <br/> |**String** <br/> **Index** <br/> **Anzahl der Zeichen** <br/> **Ausgabe** <br/> |Kopiert eine aus einer bestimmten Anzahl von Zeichen bestehende Teilzeichenfolge heraus, beginnend bei einem angegebenen Index in der Zeichenfolge, und speichert den Wert in einer Variablen.  <br/> **Hinweis:** Der Indexwert im vorhandenen Build (Technical Preview) von SharePoint Designer ist nullbasiert. Werte in SharePoint Designer 2010 wurden allerdings mit 1 beginnend indiziert.           |
|Intervall zwischen Datumsangaben suchen  <br/> |**Intervall zwischen Datumsangaben suchen** <br/> |**Einheiten** <br/> **Startdatum** <br/> **Enddatum** <br/> **Ausgabe** <br/> |Berechnet das Zeitintervall zwischen zwei Daten in Minuten, Stunden oder Tagen und speichert die Ausgabe in einer Variablen  <br/> |
|Teilzeichenfolge in Zeichenfolge suchen  <br/> |**Teilzeichenfolge in Zeichenfolge suchen** <br/> |**Teilzeichenfolge** <br/> **String** <br/> **Ausgabe** <br/> |Sucht eine bestimmte Teilzeichenfolge in einer Zeichenfolge und gibt den Index der Startposition der Teilzeichenfolge zurück.  <br/> |
|Element aus Wörterbuch abrufen  <br/> |**Element aus Wörterbuch abrufen** <br/> |**Elementname des Pfads** <br/> **Wörterbuch** <br/> **Ausgabevariable** <br/> |Gibt ein bestimmtes Element aus der Wörterbuchvariable zurück  <br/> |
|In Verlaufsliste protokollieren  <br/> |**In Verlaufsliste protokollieren** <br/> |**Meldung** <br/> |Schreibt eine Nachricht aus einer Liste vordefinierter Nachrichtenelemente in die Workflowverlaufsliste  <br/> |
|Für Dauer anhalten  <br/> |**Für Dauer anhalten** <br/> |**Tage** <br/> **Stunden** <br/> **Minuten** <br/> |Hält die Ausführung eines Workflows für ein in Tagen, Stunden und Minuten angegebenes Zeitintervall an  <br/> |
|Anhalten bis zum Datum  <br/> |**Bis Datum anhalten** <br/> |**Date** <br/> |Hält die Ausführung eines Workflows bis zu einem angegebenen Datum-/Uhrzeitwert an  <br/> |
|Teilzeichenfolge in Zeichenfolge ersetzen  <br/> |**Teilzeichenfolge in Zeichenfolge ersetzen** <br/> |**Suchzeichenfolge** <br/> **Ersetzungszeichenfolge** <br/> **String** <br/> **Ausgabe** <br/> |Ersetzt eine bestimmte Teilzeichenfolge durch eine andere Teilzeichenfolge  <br/> |
|E-Mail senden  <br/> |**E-Mail senden** <br/> |**E-Mail** <br/> |Sendet bei Eintreten eines bestimmten Workflowereignisses automatisch eine E-Mail-Nachricht, die eine vordefinierte Nachricht an einen Benutzer oder eine Gruppe enthält.  <br/> **Wichtig:** Wenn die Website nicht der Liste „Vertrauenswürdige Sites“ hinzugefügt wurde, werden E-Mails an den Junk-E-Mail-Ordner von Outlook weitergeleitet.           |
|Feld in aktuellem Element festlegen  <br/> |**Feld in aktuellem Element festlegen** <br/> |**Field** <br/> **Wert** <br/> |Legt ein Feld im aktuellen Element auf einen Wert fest.  <br/> |
|Den Zeitbereich des Felds 'Datum/Uhrzeit' festlegen  <br/> |**Den Zeitbereich des Felds "Datum/Uhrzeit" festlegen** <br/> |**Stunden** <br/> **Minuten** <br/> **Date** <br/> **Ausgabe** <br/> |Erstellt einen Zeitstempel und speichert den Ausgabewert in einer Variablen. Sie können die Uhrzeit in Stunden und Minuten festlegen und ein aktuelles Datum, ein bestimmtes Datum oder einen Nachschlagewert festlegen.  <br/> |
|Festlegen des Workflowstatus  <br/> |**Workflowstatus festlegen** <br/> |**Status** <br/> |Legt den Status des Workflows fest  <br/> |
|Workflowvariable festlegen  <br/> |**Workflowvariable festlegen** <br/> |**Variable** <br/> **Wert** <br/> |Legt eine Workflowvariable auf einen Wert fest. Sie können diese Aktion auch verwenden, wenn der Workflow einer Variablen Daten zuweisen soll.  <br/> |
|Listenworkflow starten  <br/> |**Listenworkflow starten** <br/> |**Zuordnungsname** <br/> **Eingaben** <br/> **Element** <br/> |Startet einen SharePoint 2010-Listenworkflow.  <br/> **Hinweis:** Mit der Aktion „Listenworkflow starten“ gibt es die folgenden Probleme:<ul><li>Das Feld für Zuweisungstypen kann nicht als Parameter verwendet werden, wenn der 2010-Workflow eine TaskProcess-Aktion enthält.</li><li>Wenn an den gleichen 2010-Workflow mehrere Aufrufe gerichtet werden, führt dies zu mehreren Datenquellen in der 2013-Workflownachschlagefunktion. Diese Datenquellen sind alle gleich.</li><li>Variablennamen dürfen in 2013 keine Sonderzeichen wie '?' und '#' enthalten. Wenn ein 2010-Workflow Sonderzeichen enthält, werden Sie im 2013-Workflow in Hexadezimalcode umgewandelt.</li></ul>|
|Website-Workflow starten  <br/> |**Website-Workflow starten** <br/> |**Zuordnungsname** <br/> **Parameter** <br/> |Startet einen SharePoint 2010-Website-Workflow.  <br/> **Hinweis:** Mit der Aktion „Listenworkflow starten“ gibt es die folgenden Probleme: <ul><li>Das Feld für Zuweisungstypen kann nicht als Parameter verwendet werden, wenn der 2010-Workflow eine TaskProcess-Aktion enthält.</li><li>Wenn an den gleichen 2010-Workflow mehrere Aufrufe gerichtet werden, führt dies zu mehreren Datenquellen in der 2013-Workflownachschlagefunktion. Diese Datenquellen sind alle gleich.</li><li>Variablennamen dürfen in 2013 keine Sonderzeichen wie '?' und '#' enthalten. Wenn ein 2010-Workflow Sonderzeichen enthält, werden Sie im 2013-Workflow in Hexadezimalcode umgewandelt.</li></ul>       |
|Aufgabenprozess starten  <br/> |**Aufgabenprozess starten** <br/> |**Prozesseinstellungen** <br/>  Prozessergebnis <br/> |Erstellt Aufgaben für mehrere Benutzer und erlaubt, die Aufgaben einen benutzerdefinierten Prozess durchlaufen zu lassen  <br/> |
|Dokument übersetzen  <br/> |**Dokument übersetzen** <br/> |**Dokument** <br/> **Language** <br/> **Dokumentbibliothek** <br/> |Übersetzt ein Dokument in eine bestimmte Sprache.  <br/> **Hinweis:** Für diese Aktion ist ein vorkonfigurierter maschineller Übersetzungsdienst erforderlich.           |
|Zeichenfolge kürzen  <br/> |**Zeichenfolge kürzen** <br/> |**String** <br/> **Ausgabe** <br/> |Entfernt Leerzeichen am Beginn und Ende einer Zeichenfolge  <br/> |
|Listenelement aktualisieren  <br/> |**Listenelement aktualisieren** <br/> |**Element** <br/> |Aktualisiert ein Listenelement. Sie können die Felder und die neuen Werte in diesen Feldern angeben.  <br/> |
|Auf Ereignis in Listenelement warten  <br/> |**Auf Ereignis in Listenelement warten** <br/> |Document.SelectionChanged **-Ereignis** <br/> **Verknüpftes Element** <br/> |[Verbesserte Version der Office 2010-Aktion.] Hält die aktuelle Instanz des Workflows an und wartet auf ein angegebenes Listenelementereignis. Diese Aktion überwacht zwei Ereignisse: **ItemUpdated** und **ItemAdded**.  <br/> |
|Warten auf Feldänderung  <br/> |**Auf Feldänderung warten** <br/> |**Field** <br/> **Wert** <br/> |Wartet, bis ein Feld im aktuellen Element einem bestimmten Wert entspricht  <br/> |
|Projektfeld festlegen  <br/> |**Projektfeld festlegen** <br/> |**Field** <br/> **Wert** <br/> |Legt für ein bestimmtes Feld einen Wert in Project Server fest.  <br/> **Hinweis:** Für diese Aktion muss das Projekt eingecheckt sein. Wenn das Projekt nicht eingecheckt ist, wird der Workflow beendet, und das Projekt lässt sich nicht in Project Web App öffnen.           |
|Status der Projektstufe festlegen  <br/> |**Status der Projektstufe festlegen** <br/> |**Stufenstatus** <br/> **Stufeninformationen** <br/> |Legt den Status der Projektstufe fest.  <br/> **Hinweis:** Wenn das aktuelle Projekt ausgecheckt ist, wird eine Ausnahme ausgelöst.           |
|Statusfeld in Ideenliste festlegen  <br/> |**Statusfeld in Ideenliste festlegen** <br/> |**Status** <br/> |Aktualisiert den Status für das ursprüngliche Listenelement, das mit dem aktuellen Projekt verknüpft ist  <br/> |
|Auf Projektereignis warten  <br/> |**Auf Projektereignis warten** <br/> |**Ereignisname** <br/> |Wartet auf ein bestimmtes Projektereignis  <br/> |
   

## <a name="condition-shapes"></a>Bedingungs-Shapes
<a name="VSSPD_Conditions"> </a>

Die folgende Tabelle enthält eine Liste aller Shapes, die in der SharePoint-Bedingungsschablone in der SharePoint-Workflowvorlage enthalten sind.
  
    
    


|**Shape in Visio 2013 und SharePoint Designer 2013 Visual Designer**|**Aktion im SharePoint Designer 2013 Declarative Designer**|**Eigenschaften im SharePoint Designer 2013 Visual Designer**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Wenn ein beliebiger Wert gleich dem Wert ist  <br/> |**Wenn ein beliebiger Wert gleich dem Wert ist** <br/> |**Wert** <br/> **Operand** <br/> **Wert** <br/> |Vergleicht zwei Werte. Sie können angeben, ob die Werte gleich oder nicht gleich sein sollen.  <br/> |
|Person ist ein gültiger SharePoint-Benutzer  <br/> |**Person ist ein gültiger SharePoint-Benutzer** <br/> |**Benutzer** <br/> |Überprüft, ob ein bestimmter Benutzer ein registrierter Benutzer oder ein Mitglied einer Gruppe auf der SharePoint-Website ist.  <br/> |
|Projektstufe überspringen  <br/> |**Projektstufe überspringen** <br/> |–  <br/> |Diese Bedingung prüft, ob das Feature zum Überspringen der Stufe auf dem Server für die aktuelle Workflowinstanz aktiviert wurde.  <br/> |
   

## <a name="terminator-shapes"></a>Abschlusszeichen-Shapes
<a name="VSSPD_Terminators"> </a>

Die folgende Tabelle enthält eine Liste aller Shapes, die in der SharePoint-Abschlusszeichen-Schablone in der SharePoint-Workflowvorlage enthalten sind.
  
    
    


|**Shape in Visio 2013 und SharePoint Designer 2013 Visual Designer**|**Aktion im SharePoint Designer 2013 Declarative Designer**|**Eigenschaften im SharePoint Designer 2013 Visual Designer**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|Start  <br/> |–  <br/> |–  <br/> |Startet den Workflow. Jedes SharePoint-Workflowdiagramm darf nur ein Anfangs-Shape enthalten.  <br/> |
|Stufe 1  <br/> |**Stufe** <br/> |–  <br/> |Enthält eine beliebige Anzahl von Shapes und kann ggf. Verzweigungen enthalten. Alle Aktionen im Workflow müssen in einer Stufe enthalten sein. Stufen-Shapes werden mithilfe von Container-Shapes visualisiert. Ein Stufen-Shape erfordert, dass ein Eingabe-Shape und eine Ausgangs-Shape an den Kanten des Containers hinzugefügt werden, um die Pfade innerhalb und außerhalb der Stufe zu definieren.<br/> Weitere Informationen finden Sie im Abschnitt "Phasen, Schleifen und Schritte" im Artikel  [Workflowentwicklung in SharePoint Designer und Visio](workflow-development-in-sharepoint-designer-and-visio.md).  <br/> |
|Schritt  <br/> |**Schritt** <br/> |–  <br/> |Stellt eine gruppierte Reihe aufeinanderfolgender Aktionen dar. Schritte müssen in einer Stufe enthalten sein. Ein Schritt-Shape muss auch über ein Eingabe- und ein Ausgangs-Shape verfügen. Diese werden hinzugefügt, wenn das Shape im Zeichenbereich abgelegt wird.<br/> Weitere Informationen finden Sie im Abschnitt "Phasen, Schleifen und Schritte" im Artikel  [Workflowentwicklung in SharePoint Designer und Visio](workflow-development-in-sharepoint-designer-and-visio.md).  <br/> |
|Einfache Stufe  <br/> |**Stufe** <br/> |–  <br/> |Fügt neue Stufen auf der oberen Ebene des Workflows in der Phasenansicht in Visio 2013 hinzu.  <br/> |
|Schleife n-mal  <br/> |**Schleife n-mal** <br/> |**Schleifenanzahl** <br/> |Definiert eine Reihe verbundener Shapes, die als Schleife ausgeführt werden, wobei so oft vom letzten Shape in der Reihe wieder zum ersten gewechselt wird, bis die Schleife eine festgelegte Anzahl von Malen ausgeführt wurde. Ebenso wie Stufen werden Schleifen durch ein Container-Shape dargestellt, das ein Eingabe- und ein Ausgangs-Shape enthält.<br/> Weitere Informationen finden Sie im Abschnitt "Phasen, Schleifen und Schritte" im Artikel  [Workflowentwicklung in SharePoint Designer und Visio](workflow-development-in-sharepoint-designer-and-visio.md).  <br/> |
|Schleife mit Bedingung  <br/> |**Schleife mit Bedingung** <br/> |**Schleifenanzahl** <br/> |Die Schleife wird ausgeführt, bis eine bestimmte Bedingungen erfüllt ist.  <br/> |
|Parallele Aktion starten  <br/> |**Paralleler Block** <br/> |–  <br/> ||
|Parallele Aktion beenden  <br/> |**Paralleler Block** <br/> |–  <br/> ||
   

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="VSSPD_Additional"> </a>


-  [Workflowentwicklung in SharePoint Designer und Visio](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  
-  [Leitfaden für Shapes in SharePoint-Workflowvorlagen](http://office.microsoft.com/de-DE/visio-help/sharepoint-workflow-template-shapes-guide-HA101903894.aspx)
    
  
-  [SharePoint Developer Center](http://msdn.microsoft.com/de-DE/sharepoint/default.aspx)
    
  
-  [Visio Developer Center](http://msdn.microsoft.com/de-DE/office/aa905478)
    
  
