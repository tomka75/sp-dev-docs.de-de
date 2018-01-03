---
title: "Aktivität Workflowklassen in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 70d5ca8d-520d-40a9-b24e-52bb31bd6c22
ms.openlocfilehash: 8f8b57aca40efecf9a63f2213817c29e1e116837
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="workflow-activity-classes-in-sharepoint"></a>Aktivität Workflowklassen in SharePoint
Bietet eine Übersicht über die SharePoint-Workflow Aktivitätsklassen, die in SharePoint verfügbar sind. Die Palette von Aktivitätsklassen wurde für SharePoint überarbeitet. Tabelle 1 werden den aktuellen Katalog 49 gruppiert nach ihren jeweiligen Kategorien verfügbaren Aktivitäten aufgelistet.
  
> [!NOTE] 
> In zukünftigen Versionen werden die in der Tabelle aufgeführten Aktivitäten auf die API-Referenzdokumentation für die jeweils zugehörigen verwalteten Klassen verlinken. 
  
    
    


## <a name="workflow-activity-classes-available-in-sharepoint"></a>Workflow-Aktivitätsklassen in SharePoint
<a name="bk_wfactivityclasses"> </a>


**In Tabelle 1. Workflow-Aktivitätsklassen**

||||
|:-----|:-----|:-----|
|**Aktivität** <br/> |**Kategorie** <br/> |**Beschreibung** <br/> |
|CreatedBy  <br/> |Bedingung  <br/> |Gibt zurück, ob das aktuelle Element von angegebenen Benutzer erstellt wurde.  <br/> |
|CreatedInRange  <br/> |Bedingung  <br/> |Gibt zurück, ob der aktuelle Element in der angegebenen Datumsbereichs erstellt wurde.  <br/> |
|ModifiedBy  <br/> |Bedingung  <br/> |Gibt zurück, ob das aktuelle Element vom angegebenen Benutzer geändert wurde.  <br/> |
|ModifiedInRange  <br/> |Bedingung  <br/> |Gibt zurück, ob das aktuelle Element im angegebenen Zeitraum geändert wurde.  <br/> |
|WordsInTitle  <br/> |Bedingung  <br/> |Gibt zurück, ob die angegebenen Schlüsselwörter in den Titel des aktuellen Elements vorhanden sind.  <br/> |
|WorkflowInterop  <br/> |Koordinierung  <br/> |Startet einen Workflow SharePoint 2010 (Windows Workflow Foundation 3.5).  <br/> |
|WaitForCustomEvent  <br/> |Ereignis  <br/> |Wartet auf ein benutzerdefiniertes Ereignis an den Workflow gesendet werden.  <br/> |
|WaitForFieldChange  <br/> |Ereignis  <br/> |Wartet auf die angegebene Feld, in dem angegebenen Wert für das angegebene Listenelement zu ändern.  <br/> |
|WaitForItemEvent  <br/> |Ereignis  <br/> |Wartet auf die angegebene Ereignis eintritt auf angegebenes Listenelement.  <br/> |
|CheckInItem  <br/> |List  <br/> |Checkt das angegebene Listenelement.  <br/> |
|CheckOutItem  <br/> |List  <br/> |Checkt das angegebene Listenelement.  <br/> |
|CopyItem  <br/> |List  <br/> |Kopiert das angegebene Datei-Element in der angegebenen Dokumentbibliothek. Gilt nicht für nicht-Datei-Listenelemente.  <br/> |
|CreateListItem  <br/> |List  <br/> |Erstellt ein Listenelement.  <br/> |
|DeleteListItem  <br/> |List  <br/> |Löscht ein Listenelement.  <br/> |
|LookupSPList  <br/> |List  <br/> |Gibt Informationen zu der Liste, die die angegebene Liste-ID entspricht.  <br/> |
|LookupSPListItem  <br/> |List  <br/> |Eigenschaften für das angegebene Listenelement zurückgegeben.  <br/> |
|LookupSPListItemBooleanProperty  <br/> |List  <br/> |Gibt den Wert der angegebenen Liste Item-Eigenschaft als **Boolean**zurück.  <br/> |
|LookupSPListItemDateTimeProperty  <br/> |List  <br/> |Gibt den Wert der angegebenen Liste Item-Eigenschaft als **DateTime**zurück.  <br/> |
|LookupSPListItemDoubleProperty  <br/> |List  <br/> |Gibt den Wert der angegebenen Liste Item-Eigenschaft als **Double**zurück.  <br/> |
|LookupSPListItemDynamicValueProperty  <br/> |List  <br/> |Gibt den Wert der angegebenen Liste Item-Eigenschaft als **DynamicValue**zurück.  <br/> |
|LookupSPListItemGuid  <br/> |List  <br/> |Gibt die GUID-Eigenschaft des ersten Listenelements, das mit der Eigenschaftenname und Wert-Eigenschaft angegebenen Filterkriterien übereinstimmt.  <br/> |
|LookupSPListItemInt32Property  <br/> |List  <br/> |Gibt den Wert der angegebenen Liste Item-Eigenschaft als **Int32**zurück.  <br/> |
|LookupSPListItemProperty  <br/> |List  <br/> |Gibt den Wert der angegebenen Liste Item-Eigenschaft als **Object**zurück.  <br/> |
|LookupSPListItemStringProperty  <br/> |List  <br/> |Gibt den Wert der angegebenen Liste Item-Eigenschaft als **String**zurück.  <br/> |
|LookupSPListProperty  <br/> |List  <br/> |Gibt auflisten Eigenschaften als **DynamicValue**.  <br/> |
|UndoCheckOutItem  <br/> |List  <br/> |Widerruft Auschecken des Elements angegebene Liste.  <br/> |
|UpdateListItem  <br/> |List  <br/> |Aktualisiert ein Listenelement.  <br/> |
|CompositeTask  <br/> |Aufgabe  <br/> |Führt einen Aufgabenprozess - mehrere Personen in der Datenreihe oder Parallel, wartet Aufgaben abgeschlossen haben, mehrere Aufgaben zugewiesen und aggregierte Ergebnis berechnet.  <br/> |
|SingleTask  <br/> |Aufgabe  <br/> |Führt einen einfache Aufgabe-Prozess - eine Einzelperson oder eine Gruppe, wartet auf den Abschluss der Aufgabe eine einzelne Aufgabe zugewiesen.  <br/> |
|ExpandGroupToUsers  <br/> |Benutzer  <br/> |Gibt eine Auflistung von LoginNames von Benutzern, die Mitglieder einer angegebenen Prinzipal der SharePoint-Gruppe sind.  <br/> |
|IsValidUser  <br/> |Benutzer  <br/> |Überprüft, ob der angegebene Benutzer Prinzipal-ID einen gültigen SharePoint-Benutzer darstellt.  <br/> |
|LookupSPGroup  <br/> |Benutzer  <br/> |Gibt Informationen zu einer SP-Gruppe, die entspricht der angegebenen Prinzipal-Id zurück.  <br/> |
|LookupSPGroupMembers  <br/> |Benutzer  <br/> |Gibt die Auflistung von Informationen über jedes Mitglied einer Gruppe zurück.  <br/> |
|LookupSPPrincipal  <br/> |Benutzer  <br/> |Gibt Informationen zu einer SP-Principal (Prinzipal stellt einen Benutzer oder eine Gruppe in SharePoint, die Berechtigungen zugewiesen werden kann).  <br/> |
|LookupSPPrincipalId  <br/> |Benutzer  <br/> |Gibt Prinzipal-ID, die einen angegebenen Benutzernamen entspricht.  <br/> |
|LookupSPPrincipalProperty  <br/> |Benutzer  <br/> |Gibt eine angegebene Eigenschaft von einem angegebenen SP Principal-Wert zurück.  <br/> |
|LookupSPUser  <br/> |Benutzer  <br/> |Gibt Informationen zu einem Benutzer, der entspricht der angegebenen Prinzipal-ID.  <br/> |
|LookupSPUserProperty  <br/> |Benutzer  <br/> |Gibt den Wert einer angegebenen Eigenschaft des Benutzers, den entspricht für angegebenen SP Principal zurück.  <br/> |
|E-Mail  <br/> |Utility  <br/> |Sendet eine e-Mail-Nachricht an die Benutzer der SharePoint-Website.  <br/> |
|GetCurrentItemGuid  <br/> |Utility  <br/> |Gibt die GUID-Eigenschaft des SharePoint-Listenelement auf dem die Workflowinstanz ausgeführt wird.  <br/> |
|GetCurrentListId  <br/> |Utility  <br/> |Gibt die ID-Eigenschaft des SharePoint-Liste auf dem die Workflowinstanz ausgeführt wird.  <br/> |
|GetHistoryListId  <br/> |Utility  <br/> |Gibt die ID der Verlaufsliste einer Workflowinstanz zurück, wenn eine Verlaufsliste für die workflowzuordnung angegeben ist.  <br/> |
|GetTaskListId  <br/> |Utility  <br/> |Gibt die ID der Vorgangsliste einer Workflowinstanz zurück, wenn eine Verlaufsliste für die workflowzuordnung angegeben ist.  <br/> |
|LookupWorkflowContextProperty  <br/> |Utility  <br/> |Wert der angegebenen Workflow Context-Eigenschaft zurückgegeben.  <br/> |
|SetField  <br/> |Utility  <br/> |Legt ein Feld im aktuellen Element fest.  <br/> |
|SetWorkflowStatus  <br/> |Utility  <br/> |Legt angegebenen Text als Status für das angegebene Feld aktuelle Listenelement. Ermöglicht den Workflow an, legen Sie den Wert eines zeichenfolgefelds eines Listenelements als "Workflowstatus".  <br/> |
|TranslateDocument  <br/> |Utility  <br/> |Erstellt eine übersetzte Kopie des angegebenen Dokuments in einer angegebenen Dokumentbibliothek mithilfe von SharePoint-Übersetzungsdienste.  <br/> |
|WebUri  <br/> |Utility  <br/> |Gibt die absoluten URI des SP-Webs, die den Workflow enthält.  <br/> |
|WriteToHistory  <br/> |Utility  <br/> |Schreibvorgänge angegebenen Kommentar Verlaufsliste.  <br/> |
   

## <a name="see-also"></a>Siehe auch
<a name="bkm_addlresource"> </a>


-  [Workflowaktions- und -aktivitätenreferenz für SharePoint](workflow-actions-and-activities-reference-for-sharepoint.md)
    
  
-  [Entwickeln von SharePoint-Workflows mit Visual Studio](develop-sharepoint-workflows-using-visual-studio.md)
    
  
-  [Einrichten und Konfigurieren von SharePoint-Workflow-Manager](set-up-and-configure-sharepoint-workflow-manager.md)
    
  

