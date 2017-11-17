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
# <a name="whats-changed-in-sharepoint-designer-2013"></a>Änderungen in SharePoint Designer 2013
Hier erhalten Sie Informationen zu Features, die veraltet sind oder aus SharePoint Designer 2013 entfernt wurden. Veraltete Features sind in SharePoint aus Kompatibilitätsgründen mit der vorherigen Produktversion weiterhin vorhanden, werden aber in zukünftigen Versionen entfernt.
## <a name="discontinued-features-in-sharepoint-designer-2013"></a>Eingestellte Features in SharePoint Designer 2013
<a name="WhatsChangedSharePointDesigner2013_DiscontinuedFeatures"> </a>

Die folgenden Features wurden in SharePoint Designer 2013 eingestellt oder entfernt.
  
    
    

### <a name="sharepoint-2010-workflow-platform"></a>SharePoint 2010 Workflow-Plattform
<a name="WhatsChangedSharePointDesigner2013_WorkflowPlatform"> </a>

 **Beschreibung der Änderung.** Einige Features der SharePoint 2010-Workflow-Plattform, die von der Windows Workflow Foundation 3.0 abhängig sind, wurden in SharePoint eingestellt.
  
    
    
  **Änderungsgrund.** SharePoint führt eine neue SharePoint-Workflow-Plattform ein, die auf der Windows Workflow Foundation 4.0 aufsetzt und mit Workflow-Manager 1.0 integriert wird.
  
    
    
 **Migrationspfad.** In SharePoint Designer 2013 können Sie weiterhin einen SharePoint 2010-Workflow erstellen und alle Workflow-Features von SharePoint 2010 verwenden, indem Sie die SharePoint 2010-Workflow-Plattform auswählen.
  
    
    
Sie können auch Features der SharePoint 2010-Workflow-Plattform in die neue SharePoint-Workflow-Plattform integrieren. Erstellen Sie dazu einen SharePoint 2010-Workflow, indem Sie die SharePoint 2010-Workflow-Plattform auswählen. Erstellen Sie einen SharePoint-Workflow, indem Sie die SharePoint-Workflow-Plattform auswählen. Dann verwenden Sie die Aktionen **Listenworkflow starten** und **Website-Workflow starten** im SharePoint-Workflow, um den SharePoint 2010-Workflow aufzurufen.
  
    
    
Die folgenden Features stehen nur für die SharePoint 2010-Workflow-Plattform zur Verfügung:
  
    
    

- Aktionen:
    
  - Workflow beenden
    
  
  - Version der Dokumentenmappe erfassen
    
  
  - Senden der Dokumentenmappe an das Repository
    
  
  - Inhaltsgenehmigungsstatus für die Dokumentenmappe festlegen
    
  
  - Starten des Genehmigungsvorgangs für Dokumentenmappen
    
  
  - Datensatz deklarieren
    
  
  - Festlegen des Status für die Genehmigung von Inhalten
    
  
  - Deklaration des Datensatzes aufheben
    
  
  - Listenelement hinzufügen 
    
  
  - Übergeordnete Listenelementberechtigungen erben
    
  
  - Listenelementberechtigungen entfernen
    
  
  - Listenelementberechtigungen ersetzen
    
  
  - Vorgesetzten eines Benutzers nachschlagen
    
  
  - Zuweisen eines Formulars zu einer Gruppe
    
  
  - Aufgabe zuordnen
    
  
  - Sammeln von Daten von einem Benutzer
    
  
  - Starten des Genehmigungsvorgangs
    
  
  - Starten des benutzerdefinierten Aufgabenvorgangs
    
  
  - Starten des Feedbackvorgangs
    
  
  - Listenelement kopieren (SharePoint Designer 2013 unterstützt nur das Kopieren des Dokuments)
    
  
- Bedingungen:
    
  - Wenn aktuelles Elementfeld dem Wert entspricht
    
  
  - Überprüfen von Berechtigungsstufen für Listenelemente
    
  
  - Überprüfen von Listenelementberechtigungen
    
  
- Schritte:
    
  - Identitätswechselschritt:
    
  
- Datenquellen:
    
  - Benutzerprofilsuche
    
  
- Sonstige Features:
    
  - Integration von Visio
    
  
  - Zuordnungsspalte
    
  
  - Inhaltstypzuordnung für wiederverwendbare Workflows
    
  
  - Feature "Berechtigungen zum Verwalten von Listen/Websites anfordern" für Listen-/Website-Workflow
    
  
  - Global wiederverwendbarer Workflowtyp
    
  
  - Option "Workflowvisualisierung"
    
  

### <a name="sharepoint-page-design-features"></a>SharePoint-Features für den Seitenentwurf
<a name="WhatsChangedSharePointDesigner2013_PageDesignFeatures"> </a>

Das folgende Feature ist in SharePoint nicht verfügbar.
  
    
    

#### <a name="design-view-and-split-view"></a>Entwurfsansicht und geteilte Ansicht
<a name="WhatsChangedSharePointDesigner2013_DesignViewSplitView"> </a>

 **Beschreibung der Änderung. **SharePoint Designer 2010 besitzt drei Ansichten zum Bearbeiten von HTML-Code und ASPX-Seiten: Codeansicht, Entwurfsansicht und geteilte Ansicht. Die Entwurfsansicht und die geteilte Ansicht werden aus SharePoint Designer 2013 entfernt. Das Wegfallen der Entwurfsansicht und der geteilten Ansicht wirkt sich auf die Funktionen von SharePoint Designer 2013 aus, die zum Bearbeiten von Webparts und Gestaltungsvorlagen verwendet werden. Wenn Sie Seiten in SharePoint Designer 2013 bearbeiten, müssen Sie die Codeansicht verwenden.
  
    
    
 **Änderungsgrund.** Im Vergleich zu aktuellen Versionen von Internet Explorer ist die Entwurfsansicht eine ältere Technologie, die viele neue HTML5- und CSS-Tags nicht unterstützt.
  
    
    
 **Migrationspfad.** Wenn Sie Seiten in der Codeansicht bearbeiten, können Sie **F12** drücken, um eine Vorschau der Seite im Browser anzuzeigen. Alternativ können Sie Visual Studio verwenden, um Seiten zu bearbeiten.
  
    
    
Wenn Sie Ihre Webseite visuell gestalten oder mit einer Marke versehen möchten und eine WYSIWYG-Seitenbearbeitung („What you see is what you get“) wünschen, können Sie jeden professionellen HTML-Editor, wie z. B. Microsoft Expression Web, verwenden. Sie können dann Ihre HTML-Dateien mit dem neuen Entwurfs-Manager in SharePoint importieren. Dieses Feature ist in Veröffentlichungswebsites, wie z. B. der Webseitenvorlage Publishing Portal Site Collection, enthalten.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="WhatsChangedSharePointDesigner2013_AdditionalResources"> </a>


-  [Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  
-  
  [Unterschiede zwischen SharePoint 2010 und SharePoint 2013](http://technet.microsoft.com/en-us/library/ff607742%28v=office.15%29.aspx)
    
  
-  
  [Neu in SharePoint-Workflows](http://technet.microsoft.com/en-us/library/jj219638%28v=office.15%29.aspx)
    
  

  
    
    

