---
title: "Problembehandlung bei SharePoint Server-Workflow-Überprüfungsfehlern in Visio"
ms.prod: SHAREPOINT
ms.assetid: c21cc3e2-45bd-4d34-a57d-dd0954436bd8
ms.openlocfilehash: 53021bbfbfc67c643a0d72e70e29f61097668acc
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2017
---
# <a name="troubleshooting-sharepoint-server-workflow-validation-errors-in-visio"></a>Problembehandlung bei SharePoint Server-Workflow-Überprüfungsfehlern in Visio
Verwenden Sie diese Übersicht, Validierung und fehlerüberprüfung Probleme in der Workflowvorlage Microsoft SharePoint in Microsoft Visio 2013 und Microsoft SharePoint Designer 2013 aufzulösen.
## <a name="sharepoint-workflow-validation-issues"></a>Probleme bei der Validierung von SharePoint-workflow
<a name="VSSPD_Trouble_Issues"> </a>

Die folgende Tabelle enthält eine Liste aller die Überprüfungsprobleme, die in den Bereich Probleme in Microsoft Visio 2013 oder des visuellen Designers in Microsoft SharePoint Designer 2013 angezeigt werden können. Jeder Fehler hat eine vorgeschlagene zur Behebung dieses Problems auszuführende Aktion.
  
    
    


|**Fehlertext**|**Vorgeschlagene Aktion**|
|:-----|:-----|
|Zwischen Workflow-Shapes bestehen doppelte Verbindungen.  <br/> |Entfernen Sie den redundanten Connector, indem markieren und löschen.  <br/> |
|Schleife zurück zu übergeordnetem Shape ist nicht innerhalb einer Phase oder Schritt zulässig.  <br/> |Weder Visio Professional 2013 noch SharePoint Designer 2013 unterstützt Workflows mit impliziten Schleifen innerhalb einer Phase. Überprüfen Sie den Workflow für Schleifen und Löschen der Schleifen Verbindungen. Wenn Sie einen SharePoint-Workflow erstellen, der eine Reihe von Schleifen Schritten innerhalb einer Phase enthält möchten, müssen Sie die Schleife Container verwenden. Alle Aktionen innerhalb dieser Container werden wiederholt. Eine weitere Option ist Phasen verwenden, das Wechseln zu einem früheren Zeitpunkt an.  <br/> |
|Parallele Aktivitäten, die auch sequenziell sind, sind nicht zulässig.  <br/> |Aktivitäten können entweder parallel oder sequenzielle, jedoch nicht beide gleichzeitig sein. Entfernen Sie für parallele Aktivitäten die sequenzielle Connectors. Entfernen Sie die parallele Connectors für sequenzielle Aktivitäten. In einigen Fällen können gleichzeitig parallele und sequenzielle Aktivitäten zum Identifizieren schwierig sein. Folgende Überprüfungsfehler andere allgemeinen Instanzen von parallelen und sequenziellen Anordnung anzeigen und alternative Modalitäten anbieten.  <br/> Um Connectors, zeigen Sie auf der gleichen Aktivität von mehreren Pfaden zu vermeiden, versuchen Sie die Aktivität.  <br/> |
|Die Form ' Bedingung ' hat keine Verbindung mit der Bezeichnung mit Ja oder Nein.  <br/> |Mit der rechten Maustaste den Connector Zuweisen von der Bezeichnung "Ja" oder "Nein".  <br/> |
|Die Form ' Bedingung ' benötigen ausgehende Verbindungen mit der Bezeichnung Ja und Nein.  <br/> |Sicherstellen Sie, dass die Bedingung Shapes ausgehenden Connectors an andere Shapes Workflow angefügt haben. Jede Form ' Bedingung ' muss eine "Ja" und eine ausgehende Verbindung "No" haben.  <br/> |
|Der Verbinder ist keinen SharePoint-Workflow-Connector. Verwenden Sie AutoConnect oder das Verbinder-Tool, um die Shapes verbinden.  <br/> |Vermeiden Sie die Connectors aus anderen Diagrammen wiederverwenden, wie sie unbedingt nicht mit SharePoint-Workflows verwendet werden soll. Löschen Sie den Verbinder, und verwenden Sie die Verbinder oder AutoConnect ersetzen durch eine neue Verbindung.  <br/> |
|Der Verbinder muss mit zwei workflowformen verbunden sein.  <br/> |Entfernen von Sackgasse Connectors oder Anfügen an ein zweites Shape.  <br/> |
|Das Diagramm darf nur einen Workflow und ein Anfangs-Shape haben.  <br/> |Alle Pfade müssen aus der gleichen Anfangs-Shape stammen. Entfernen von zusätzlichen Start-Shapes und ordnen Sie die Connectors, um der Pfad an einem Ort zu starten.  <br/> |
|Das Shape ist kein SharePoint-Workflow-Shape. In einem Workflow können nur SharePoint-Workflow-Shapes verbunden werden.  <br/> |In der Microsoft SharePoint-Workflow-Vorlage können nur Workflow-Shapes aus den Schablonen SharePoint-Workflow verwendet werden. Andere Flussdiagrammshapes werden nicht erkannt und verhindern, dass den Workflow in SharePoint Designer exportiert wird.  <br/> |
|Das Anfangs-Shape darf keine eingehenden Verbindungen haben  <br/> |Entfernen Sie den eingehenden Connector an das Anfangs-Shape.  <br/> |
|Der Workflow muss ein Anfangs-Shape haben  <br/> |Fügen Sie ein Anfangs-Shape an den Anfang des Workflows, und schließen Sie es an die erste Aktivität.  <br/> |
|Das Workflow-Shape ist nicht mit dem Workflow verbunden.  <br/> |Wenn das Workflow-Shape erforderlich ist, fügen Sie Connectors So fügen Sie es auf den Workflow Pfad hinzu. Anderenfalls Löschen des Shapes.  <br/> |
|Workflow geschachtelte Ebenen darf maximal 10 nicht überschreiten.  <br/> |Visio 2013 können maximal 10 Ebenen der Schachtelung Workflowaktivitäten erkennen. Neu anordnen Sie, um Komplexität eliminiert Aktivitäten oder den Pfad der Workflow in mehr als eine Verzweigung Aufteilen des Workflows.  <br/> |
|Das Anfangs-Shape kann nur mit einem Workflow Phasen-Shape verbunden werden.  <br/> |Alle Workflowdiagramme müssen mit nur ein Anfangs-Shape beginnen. Das Anfangs-Shape muss mit einem Phasen-Shape verbunden sein. Falls erforderlich, fügen Sie ein Anfangs-Shape an den Anfang des Workflows. Sie können auch ein Anfangs-Shape an den Anfang des Workflows in der phasenansicht in Visio 2013 hinzufügen.  <br/> |
|Eine Phase kann nicht in einem anderen Shape geschachtelt werden.  <br/> |Phasen sind in SharePoint Workflowdiagramme Shapes der obersten Ebene. Sie können kein Shape in allen anderen Container-Shapes, einschließlich Schritte, Schleifen oder anderen Stufen platzieren.  <br/> Falls möglich, verschieben Sie die Phase, damit es außerhalb von Container-Shapes ist, und schließen Sie die Phase. Wenn Sie eine logische Gruppierung von Actions- und Conditions innerhalb einer Phase oder Schleife erstellen möchten, verwenden Sie stattdessen eine Schritt-Form.  <br/> |
|Eine Phase kann nur an eine andere Stufe, bedingungs-Shape oder ein Abschlusszeichen verbunden werden.  <br/> |Phasen können nur mit anderen Shapes der obersten Ebene, einschließlich der Bedingungen, Abschlusszeichen oder anderen Stufen verbunden werden. Eine Phase kann nicht mit Aktionen, Schritten oder Schleifen auf der obersten Ebene verbunden werden. Neu anordnen des Workflowdiagramms, damit die Phase nur mit anderen Shapes der obersten Ebene verbunden ist.  <br/> |
|Phase Schritt und Schleife Container können nicht überlappt werden.  <br/> |Die Grenzen der Container-Shapes, wie etwa Phasen, Schleifen und Schritte können nicht berühren oder überschneiden sich. Wenn Sie eine Container-Shape in einer anderen einschließen möchten (beispielsweise enthalten eine Schleife innerhalb einer Phase befinden), achten Sie darauf, dass das enthaltene Shape vollständig innerhalb der Grenzen des Containers ist. Wenn Sie nicht möchten, führen Sie eine Container-Shape der anderen, Space die Shapes in Ihrem Diagramm enthalten sein, damit die Grenzen der Container-Shapes nicht mehr schneidet oder berühren.  <br/> |
|Workflow-Shapes aus anderen Vorlagen-Versionen sind keine gültige Workflow-Shapes.  <br/> |Sie können die Shapes nur aus der SharePoint Workflowaktionen, SharePoint Workflowbedingungen, und SharePoint Workflow Abschlusszeichen Schablonen und Connectors, die mit AutoConnect oder der Vorlage in einem Workflowdiagramm Microsoft SharePoint zugeordneten Verbinder-Tool erstellt werden. Alle anderen Shapes sind nicht gültig Verbindungen innerhalb der Validierungsregeln Workflow. Sie können andere Shapes auf die Design-Zeichenbereich platzieren, solange sie nicht mit dem Workflow verbunden sind.<br/>Müssen Sie eine Aktion oder Bedingung, die nicht mit einer Form in eine zugeordnete Workflowvorlage Microsoft SharePoint Schablonen dargestellt wird, sollten Sie eine benutzerdefinierte Workflowaktion erstellen. Benutzerdefinierte Workflowaktionen können in Microsoft Visual Studio 2012 erstellt und in SharePoint Workflows in SharePoint Designer 2013 integriert werden. Weitere Informationen zum Erstellen von benutzerdefinierter Aktionen in Visual Studio 2012 finden Artikel,  [Entwickeln von SharePoint-Workflows mit Visual Studio](develop-sharepoint-workflows-using-visual-studio).<br/> |
|Ein Shape kann nicht außerhalb der Anfangs-/Pfad der Container des aktuellen Shapes verbunden werden.  <br/> |Alle Formen innerhalb einer Phase, Schleife oder Schritt müssen vollständig in das Container-Shape enthalten sein. Shapes können nicht zu Shapes verbinden, die nicht in demselben Container enthalten sind. Neu anordnen des Workflowdiagramms, damit an andere Shapes im Container alle Aktionen, Bedingungen, Schleifen und Schritte in das Container-Shape verbinden.  <br/> Wenn das Shape auf eine Aktivität außerhalb des Containers verbinden muss, verbinden Sie die Form an das Ausgangs-Shape, das dem Container zugeordnet.  <br/> |
|Ungültiger Übergang-Shape.  <br/> |Wenn ein Shape nicht Bedingung oder nicht-Stufen Ebene der Basis des Workflows hinzugefügt wird. Ebene der Basis eines Workflows ist möglicherweise nur Phasen und Bedingungen vorhanden. Alle anderen Shapes, die dieser Ebene hinzugefügt werden, werden dieser Fehler verursacht. Sie sollten nicht Bedingung und nicht-Stufen-Shapes in einer Bedingung oder Phase Form kapseln.  <br/> |
|Phasen, Schleifen und Schritte können nur eine eingehende und eine ausgehende Verbindung haben.  <br/> |Alle Container-Shapes können nur ein eingehender Connector mit dem Shape EINGABETASTE haben, die zugeordnet ist. Container-Shapes können auf ähnliche Weise nur eine ausgehende Verbindung von ihrer Ausgangs-Shape haben. Neu anordnen Sie das Diagramm, sodass jeder Container einen einzelnen ein- und ausgehenden Pfad hat. Sie müssen möglicherweise zusätzliche Phasen oder Zuordnungstabelle Shapes an den Workflow zum Beheben dieses Fehlers hinzufügen.  <br/> |
|Eine Phase Name muss eindeutig sein und darf nicht leer sein.  <br/> |Jede Stufe im Workflow muss einen eindeutigen Namen besitzen. Wechseln Sie zum phasenansicht, und stellen Sie sicher, dass jeder Phase einen eigene Namen hat.  <br/> |
|Projektstufe wurde nicht konfiguriert.  <br/> |Für Workflows Projekt basiert muss jeder Phase in eine Stufe in Project Server verknüpft werden. Wenn eine Phase in eine Stufe auf dem Server nicht verknüpft wurde, wird dieser Fehler angezeigt. Um dieses Problem zu beheben, öffnen Sie Eigenschaftenraster Stufe aus, und legen Sie eine Phase aus der Dropdownliste Phase.  <br/> |
|Eine parallele Aktivität muss mit einem Shape starten Verzweigung "Parallel" beginnen.  <br/> |Überprüfen Sie jede parallele Aktivität im Workflow, um sicherzustellen, dass es eine parallele Verzweigung starten Form hat, vor dem Beginn der parallelen Aktivitätsfeeds.  <br/> |
   

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="VSSPD_Trouble_Additional"> </a>


-  [Workflowentwicklung in SharePoint Designer und Visio](workflow-development-in-sharepoint-designer-and-visio)
    
  
-  [Shapes in der SharePoint Server-Workflowvorlage in Visio](shapes-in-the-sharepoint-server-workflow-template-in-visio)
    
  
-  [Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)](workflow-actions-quick-reference-sharepoint-workflow-platform)
    
  
-  [Erstellen, Importieren und Exportieren von SharePoint-Workflows in Visio](http://office.microsoft.com/en-us/visio-help/create-import-and-export-sharepoint-workflows-in-visio-HA101888007.aspx)
    
  
-  [SharePoint Developer Center](http://msdn.microsoft.com/en-us/sharepoint/default.aspx)
    
  
-  [Visio Developer Center](http://msdn.microsoft.com/en-us/office/aa905478)
    
  

