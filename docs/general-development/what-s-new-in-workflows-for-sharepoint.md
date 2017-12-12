---
title: "Neuerungen in Workflows für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1d51421b-61ac-46b6-a865-52f968ddc5b3
ms.openlocfilehash: bf9347b0c0120d2cb8317a16be3406aaed388009
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="whats-new-in-workflows-for-sharepoint"></a>Neuerungen in Workflows für SharePoint
Hier erhalten Sie Informationen zu den neuen Features für Workflows in SharePoint. Das Workflow-Framework in SharePoint hat sich gegenüber früheren Versionen erheblich geändert. Die folgenden Abschnitte bieten kurze Zusammenfassungen zu den wichtigsten Updates und Verbesserungen an der Workflowinfrastruktur.
  
    
    


## <a name="completely-redesigned-workflow-infrastructure"></a>Vollständig neu gestaltete Workflowinfrastruktur
<a name="SP15Whatsnewinworflow_infrastructure"> </a>

SharePoint-Workflows werden von Windows Workflow Foundation 4 (WF) unterstützt, das in Vergleich zu früheren Versionen erheblich überarbeitet wurde. Windows Workflow Foundation basiert wiederum auf der von  [Windows Communication Foundation (WCF)](http://msdn.microsoft.com/de-DE/netframework/aa663324) bereitgestellten Messaging-Funktion.
  
    
    
Das wahrscheinlich bedeutendste Feature der neuen Workflowinfrastruktur ist die Einführung von Microsoft Azure als neuer Host für die Workflowausführung. Das Workflowausführungsmodul befindet sich jetzt außerhalb von SharePoint in Microsoft Azure. Abbild 1 zeigt eine verallgemeinerte Ansicht der neuen Workflowinfrastruktur. Ausführlichere Informationen zu den in Abbildung 1 präsentierten Konzepten finden Sie unter  [Grundlegendes zu SharePoint-Workflows](sharepoint-workflow-fundamentals.md).
  
    
    

**Abbildung 1. Allgemeine Architektur der Workflowinfrastruktur**

  
    
    

  
    
    
![Allgemeine Workflowarchitektur](../images/wfArchitecture1.png)
  
    
    

  
    
    

  
    
    

## <a name="fully-declarative-no-code-authoring-environment"></a>Vollständig deklarative Erstellungsumgebung ohne Code
<a name="SP15Whatsnewinworflow_environment"> </a>

Eine weitere bedeutende Änderung besteht darin, dass Workflows auf der WF 4-Plattform vollständig deklarativ sind. Das bedeutet, dass Workflows nicht länger zu verwalteten Assemblys kompiliert und in einem Assembly-Cache bereitgestellt werden. Stattdessen definieren XAML-Dateien Ihre Workflows und legen ihre Ausführung fest.
  
    
    

## <a name="enhanced-sharepoint-designer-2013-authoring-support"></a>Erweiterte Unterstützung der SharePoint Designer 2013-Erstellung
<a name="SP15Whatsnewinworflow_SPDauthoring"> </a>

SharePoint Designer 2013 wurde mit dem Ziel aktualisiert, es für die Erstellung von SharePoint-Workflows zur gewünschten Erstellungsumgebung zu machen. SharePoint Designer 2013 bietet Workflowautoren sowohl eine Designeroberfläche als auch eine textbasierte Erstellungsumgebung für Workflows. Zusätzlich können Sie für Workflows benutzerdefinierte Aktionen in Visual Studio 2012 entwickeln und diese dann in SharePoint Designer 2013 importieren, wo dann Workflow-Designer darauf zugreifen kann.
  
    
    
Kurz gesagt, wurden die Anforderungen der Information-Worker ("Hauptbenutzer") und der Entwickler in den Umgebungen zur SharePoint-Workflowerstellung und -entwicklung genutzt.
  
    
    

## <a name="visual-studio-2012-workflow-project-type-support"></a>Unterstützung des Visual Studio 2012-Workflowprojekttyps
<a name="SP15Whatsnewinworflow_VSworkflow"> </a>

Um die Zusammenarbeit von Information-Worker und Softwareentwickler zu vereinfachen, bietet Visual Studio 2012 die SharePoint-Workflowprojekttypen und einen benutzerdefinierten Aktionselementtyp für Workflows. Weitere Informationen zum Entwickeln von Workflows mithilfe von Visual Studio 2012 sowie Informationen zur Unterscheidung von SharePoint Designer 2013 und Visual Studio 2012 bei der Workflowentwicklung finden Sie unter  [Entwickeln von SharePoint-Workflows mit Visual Studio](develop-sharepoint-workflows-using-visual-studio.md).
  
    
    

## <a name="support-for-creating-custom-actions"></a>Unterstützung für das Erstellen benutzerdefinierter Aktionen
<a name="SP15Whatsnewinworflow_customactions"> </a>

In die Vorhersage der Geschäftsanforderungen von Workflowautoren für die Bereitstellung von Workflowvorlagen, Aktionen und Aktivitäten in SharePoint Designer 2013 und in Visual Studio 2012 wurde viel Arbeit gesteckt. Dennoch können wir nicht die spezifischen Anforderungen jeder einzelnen Person vorhersagen. Aus diesem Grund bietet Visual Studio 2012 einen benutzerdefinierten Aktionselementtyp für Workflows, mit dem Entwickler benutzerdefinierte Aktionen erstellen können. Weitere Informationen zu benutzerdefinierte Aktionen für Workflows finden Sie unter  [Vorgehensweise: Erstellen und POST von benutzerdefinierten Workflowaktionen](how-to-build-and-deploy-workflow-custom-actions.md).
  
    
    

## <a name="tools-support-for-sharepoint-workflows"></a>Unterstützung von Tools für SharePoint-Workflows
<a name="SP15Whatsnewinworflow_Tools"> </a>

Visual Studio 2012 bietet Vorlagen und Unterstützung für das Erstellen von Workflows für das SharePoint-Workflow-Framework. SharePoint-Workflows ähneln früheren Versionen von Workflows, allerdings werden Sie von WF 4 unterstützt und in Microsoft Azure ausgeführt. Außerdem sind sie rein deklarativ (XAML) und für die Interaktion mit der Cloud sowie für die Arbeit mit SharePoint-Add-Ins konzipiert. Einer ihrer Hauptvorteile besteht darin, dass Sie es Ihnen ermöglichen, Workflows außerhalb von SharePoint Server remote zu hosten und auszuführen.
  
    
    

## <a name="new-workflow-actions"></a>Neue Workflowaktionen
<a name="SP15Whatsnewinworflow_Newwfactions"> </a>

Nachfolgend sind die neuen Workflowaktionen aufgeführt, die in SharePoint bereitgestellt werden. Ausführliche Informationen zu neuen und überholten Aktionen finden Sie unter  [Workflowaktions- und -aktivitätenreferenz für SharePoint](workflow-actions-and-activities-reference-for-sharepoint.md). Neu für Workflows in SharePoint sind eine Reihe von Workflowaktionen, die Ihnen die Integration mit Project 2013 und die Erstellung projektbasierter Workflows gestatten.
  
    
    

**Tabelle 1. Neue Workflowaktionen in SharePoint**


|**Aktion**|**Beschreibung**|
|:-----|:-----|
|Aufgabe zuweisen  <br/> |Weist eine einzelne Workflowaufgabe zu einem Benutzer oder einer Gruppe zu.  <br/> |
|Aufgabenprozess starten  <br/> |Startet die Ausführung eines Aufgabenprozesses.  <br/> |
|Zu dieser Phase wechseln  <br/> |Gibt die nächste Phase in einem Workflow an, an welche die Ablaufsteuerung übergeben werden sollte.  <br/> |
|HTTP-Webdienst aufrufen  <br/> |Dient als Methodenaufruf für einen REST-Endpunkt (Representational State Transfer).  <br/> |
|Listenworkflow starten  <br/> |Startet einen listenbezogenen Workflow.  <br/> |
|Website-Workflow starten  <br/> |Startet einen websitebezogenen Workflow.  <br/> |
|DynamicValue erstellen  <br/> |Erstellt eine neue Variable vom Typ **DynamicValue**.  <br/> |
|Eigenschaft von DynamicValue abrufen  <br/> |Ruft einen Eigenschaftswert von einer angegebenen Variablen vom Typ **DynamicValue** ab.  <br/> |
|Elemente in DynamicValue zählen  <br/> |Gibt die Anzahl der Zeilen in einer Variablen vom Typ **DynamicValue** zurück.  <br/> |
|Zeichenfolge kürzen  <br/> |Entfernt alle führenden und nachfolgenden Leerzeichen aus der aktuellen Zeichenfolge.  <br/> |
|Teilzeichenfolge in Zeichenfolge suchen  <br/> |Gibt den auf 1 basierenden Index für das erste Vorkommen eines oder mehrerer Zeichen oder das erste Vorkommen einer Zeichenfolge innerhalb einer Zeichenfolge zurück.  <br/> |
|Teilzeichenfolge in Zeichenfolge ersetzen  <br/> |Gibt eine neue Zeichenfolge zurück, in der alle Vorkommen eines angegebenen Zeichens oder einer Zeichenfolge durch ein anderes angegebenes Zeichen oder durch eine Zeichenfolge ersetzt werden.  <br/> |
|Dokument übersetzen  <br/> |Funktioniert als Wrapper für die HTTP-Aktivität, die die synchrone Übersetzungs-API aufruft. Sie müssen eine maschinelle Übersetzungsdienstanwendung für die SharePoint-Website konfigurieren, für die Sie den Workflow ausführen.  <br/> |
|Workflowstatus festlegen  <br/> |Aktualisiert den Workflowstatus gemäß der Meldungszeichenfolge.  <br/> |
|Projekt aus aktuellem Element erstellen [Microsoft Project]  <br/> |Erstellt auf Basis des aktuellen Elements ein Project Server-Projekt.  <br/> |
|Aktuellen Projektphasenstatus auf diesen Wert festlegen [Microsoft Project]  <br/> |Legt die beiden Statusfelder innerhalb der aktuellen Phase des Projekts fest.  <br/> |
|Statusfeld im Ideenlistenelement auf diesen Wert festlegen [Microsoft Project]  <br/> |Aktualisiert das Statusfeld des ursprünglichen SharePoint-Listenelements.  <br/> |
|Auf Projektereignis warten [Microsoft Project]  <br/> |Hält die aktuelle Instanz des Workflows an, um auf ein angegebenes Projektereignis zu warten: Projekt wurde eingecheckt, Projekt wurde bestätigt, Projekt wurde übermittelt.  <br/> |
|Dieses Feld im Projekt auf diesen Wert festlegen [Microsoft Project]  <br/> |Legt den Wert für das unternehmensspezifische Feld für ein angegebenes Projekt fest.  <br/> |
   

## <a name="see-also"></a>Siehe auch
<a name="SP15Whatsnewinworflow_Addresources"> </a>


-  [Erste Schritte mit Workflows in SharePoint](get-started-with-workflows-in-sharepoint.md)
    
  
-  [Neuerungen für Entwickler in SharePoint](what-s-new-for-developers-in-sharepoint.md)
    
  
-  [Workflowaktions- und -aktivitätenreferenz für SharePoint](workflow-actions-and-activities-reference-for-sharepoint.md)
    
  
-  [Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  

