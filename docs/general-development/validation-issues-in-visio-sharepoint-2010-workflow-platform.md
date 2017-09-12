---
title: "Probleme bei der Überprüfung in Visio (SharePoint 2010-Workflowplattform)"
ms.prod: SHAREPOINT
ms.assetid: 416c8269-3c4e-40f4-bc20-a625f07a4dac
ms.openlocfilehash: 261892cafbf61c23ad98373be39891f5fb1132c4
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2017
---
# <a name="validation-issues-in-visio-sharepoint-2010-workflow-platform"></a>Probleme bei der Überprüfung in Visio (SharePoint 2010-Workflowplattform)
Verwenden Sie diese Übersicht, bei der Validierung von Problemen beim Exportieren eines SharePoint-Workflows aus Visio Professional 2013 SharePoint Designer 2013 unterstützen. Dieser Artikel beschreibt Überprüfungsprobleme, die auftreten können, wenn Sie die SharePoint 2010-Workflow-Plattform in SharePoint Designer 2013 verwenden.
  
    
    


## <a name="introduction"></a>Einführung
<a name="section1"> </a>

Beim Exportieren eines SharePoint-Workflows von Microsoft Visio Professional 2013 in Microsoft SharePoint Designer 2013 muss das Diagramm zuerst überprüft werden. Das Workflowdiagramm nicht gültig ist, wird ein Fenster **Probleme** angezeigt, die enthält eine Liste der Punkte, die repariert werden muss, bevor der Workflow exportiert werden kann.
  
    
    
Dieser Artikel enthält eine Beschreibung, Beispiel und vorgeschlagenen Aktion für jeden Workflow-Überprüfungsprobleme, die Sie in Visio Professional 2013 erhalten können. Wenn Sie über ein Problem bei der Validierung benachrichtigt werden, finden Sie in der Liste unten die Bezeichnung des Problems, mithilfe des Beispiels zum Identifizieren, wo das Problem liegt, und befolgen Sie die vorgeschlagene Aktion zur Behebung.
  
    
    

## <a name="a-custom-action-cannot-be-added-to-a-workflow-diagram"></a>Eine benutzerdefinierte Aktion kann nicht hinzugefügt werden, einem Workflowdiagramm
<a name="section2"> </a>

Meldung:
  
    
    
Eine benutzerdefinierte Aktion kann keines Workflowdiagramms hinzugefügt werden. Die benutzerdefinierte Aktion kann nur beim Importieren des Workflows aus SharePoint Designer generiert werden.
  
    
    
Beispiel:
  
    
    

  
    
    
![Eine benutzerdefinierte Aktion kann nicht hinzugefügt werden.](../../images/spd15-wf-error1.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Wenn Sie eine Aktion zu einem Workflow hinzufügen möchten, und ein master-Shape ist nicht in der Schablone dafür vorhanden, nicht erstellen Sie eigener Shape oder importieren Sie eine aus einer anderen Schablone. Verwenden Sie stattdessen einer vorhandenen Form, und klicken Sie dann verwenden Sie das Feature **Kommentar hinzufügen** der Form, um das beabsichtigte Verhalten anzugeben.
  
    
    

## <a name="a-custom-condition-cannot-be-added-to-a-workflow-diagram"></a>Eine benutzerdefinierte Bedingung kann nicht hinzugefügt werden, einem Workflowdiagramm
<a name="section3"> </a>

Meldung:
  
    
    
Eine benutzerdefinierte Bedingung kann einem Workflowdiagramm hinzugefügt werden. Benutzerdefinierte Bedingung kann nur beim Importieren des Workflows aus SharePoint Designer generiert werden.
  
    
    
Beispiel:
  
    
    

  
    
    
![Eine benutzerdefinierte Bedingung kann nicht hinzugefügt werden](../../images/spd15-wf-error2.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Wenn Sie eine Bedingung zu einem Workflow hinzufügen möchten, und ein master-Shape ist nicht in der Schablone dafür vorhanden, nicht erstellen Sie eigener Shape oder importieren Sie eine aus einer anderen Schablone. Verwenden Sie stattdessen einer vorhandenen Form, und klicken Sie dann verwenden Sie das Feature **Kommentar hinzufügen** der Form, um das beabsichtigte Verhalten anzugeben.
  
    
    

## <a name="a-compound-condition-cannot-be-manually-added-to-a-workflow-diagram"></a>Eine verbundbedingung kann nicht manuell eines Workflowdiagramms hinzugefügt werden
<a name="section4"> </a>

Meldung:
  
    
    
Eine verbundbedingung kann nicht manuell eines Workflowdiagramms hinzugefügt werden. Die verbundbedingung kann nur beim Importieren des Workflows aus SharePoint Designer generiert werden.
  
    
    
Beispiel:
  
    
    

  
    
    
![Eine Verbundbedingung kann nicht manuell hinzugefügt werden](../../images/spd15-wf-error3.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Wenn Sie eine Bedingung zu einem Workflow hinzufügen möchten, und ein master-Shape ist nicht in der Schablone dafür vorhanden, nicht erstellen Sie eigener Shape oder importieren Sie eine aus einer anderen Schablone. Verwenden Sie stattdessen einer vorhandenen Form, und klicken Sie dann verwenden Sie das **Hinzufügen eines Kommentars** Feature der Form, um das beabsichtigte Verhalten anzugeben.
  
    
    

## <a name="duplicate-connections-exist-between-workflow-shapes"></a>Zwischen Workflow-Shapes bestehen doppelte Verbindungen
<a name="section5"> </a>

Meldung:
  
    
    
Zwischen Workflow-Shapes bestehen doppelte Verbindungen.
  
    
    
Beispiel:
  
    
    

  
    
    
![Zwischen Shapes bestehen doppelte Verbindungen](../../images/spd15-wf-error4.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Entfernen Sie den redundanten Connector, indem markieren und löschen.
  
    
    

## <a name="loop-back-to-parent-shape-is-not-allowed"></a>Ein Zurückschleifen zum übergeordneten Shape ist nicht zulässig
<a name="section6"> </a>

Meldung:
  
    
    
Ein Zurückschleifen zum übergeordneten Shape ist nicht zulässig
  
    
    
Beispiel:
  
    
    

  
    
    
![Ein Zurückschleifen zum übergeordneten Shape ist nicht zulässig](../../images/spd15-wf-error5.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Weder Visio Professional 2013 noch SharePoint Designer 2013 unterstützt Workflows mit Schleifen. Überprüfen Sie den Workflow für Schleifen und löschen Sie die Schleifen Verbindungen. Wenn Sie einen SharePoint-Workflow erstellen, der eine Reihe von Schritten Schleife enthält möchten, müssen Sie den Workflow in Visual Studio erstellen.
  
    
    

## <a name="parallel-activities-that-are-also-sequential-are-not-allowed"></a>Parallele Aktivitäten, die auch sequenziell sind, sind nicht zulässig.
<a name="section7"> </a>

Meldung:
  
    
    
Parallele Aktivitäten, die auch sequenziell sind, sind nicht zulässig.
  
    
    
Beispiel:
  
    
    

  
    
    
![Parallele Aktivitäten, die auch sequenziell sind](../../images/spd15-wf-error6.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Aktivitäten können entweder parallel oder sequenzielle, jedoch nicht beide gleichzeitig sein. Entfernen Sie für parallele Aktivitäten die sequenzielle Connectors. Entfernen Sie die parallele Connectors für sequenzielle Aktivitäten. In einigen Fällen können gleichzeitig parallele und sequenzielle Aktivitäten zum Identifizieren schwierig sein. In den folgenden Beispielen andere allgemeinen Instanzen von parallelen und sequenziellen Anordnung anzeigen und alternative Modalitäten anbieten.
  
    
    
Beispiel:
  
    
    

  
    
    
![Zeigen auf eine Aktivität von mehreren Pfaden vermeiden](../../images/spd15-wf-error7.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Um Connectors, zeigen Sie auf der gleichen Aktivität von mehreren Pfaden zu vermeiden, versuchen Sie die Aktivität:
  
    
    

  
    
    
![Parallele Aktivitäten, die auch sequenziell sind](../../images/spd15-wf-error8.JPG)
  
    
    
Beispiel:
  
    
    

  
    
    
![Parallele Aktivitäten, die auch sequenziell sind](../../images/spd15-wf-error9.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Wenn Umgang mit paralleler Blöcke in aufeinander folgenden Schritten (in der Regel finden Sie unter erstellt mithilfe von SharePoint Designer-Workflows) versuchen Sie die Form "Kommentar hinzufügen" zwischen zwei parallele Blöcke, damit die Schritte ordnungsgemäß getrennt sind.
  
    
    

  
    
    
![Parallele Aktivitäten, die auch sequenziell sind](../../images/spd15-wf.JPG)
  
    
    

  
    
    

  
    
    

## <a name="the-condition-shape-does-not-have-connections-labeled-with-yes-or-no"></a>Die Form ' Bedingung ' hat keine Verbindung mit der Bezeichnung mit Ja oder Nein
<a name="section8"> </a>

Meldung:
  
    
    
Die Form ' Bedingung ' hat keine Verbindung mit der Bezeichnung mit Ja oder Nein.
  
    
    
Beispiel:
  
    
    

  
    
    
![Bedingungs-Shape hat keine ja-/nein-Verbindungen](../../images/spd15-wf-error11.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Mit der rechten Maustaste in des Connectors zur "Ja" oder "No" Bezeichnung zuweisen.
  
    
    

## <a name="the-condition-shape-must-have-at-least-one-outgoing-connection-with-label-yes-or-no"></a>Die Form ' Bedingung ' muss mindestens eine ausgehende Verbindung mit der Bezeichnung Ja oder Nein haben.
<a name="section9"> </a>

Meldung:
  
    
    
Die Form ' Bedingung ' benötigen Sie mindestens eine ausgehende Verbindung mit der Bezeichnung Ja oder Nein.
  
    
    
Beispiel:
  
    
    

  
    
    
![Bedingungs-Shape muss eine ausgehende Verbindung aufweisen](../../images/spd15-wf-error12.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Stellen Sie sicher, dass die Form ' Bedingung ' mindestens einen ausgehenden Connector zu einem anderen Workflow-Shape zugeordnet ist.
  
    
    

## <a name="the-connector-is-not-a-sharepoint-workflow-connector"></a>Der Connector ist keine Verbindung zu SharePoint-Workflow
<a name="section10"> </a>

Meldung:
  
    
    
Der Connector ist keine Verbindung zu SharePoint-Workflow. Stellen Sie sicher, dass der richtige Verbinder mithilfe der Verbinder oder AutoConnect verwendet wird.
  
    
    
Beispiel:
  
    
    

  
    
    
![Vergewissern Sie sich, dass der korrekte Verbinder verwendet wird](../../images/spd15-wf-error13.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Vermeiden Sie die Connectors aus anderen Diagrammen wiederverwenden, da sie nicht notwendigerweise ausgelegt sind mit SharePoint-Workflows verwendet werden. Löschen Sie den ausgewählten Verbinder, und verwenden Sie die Verbinder oder AutoConnect durch einen neuen Connector zu ersetzen.
  
    
    

## <a name="the-connector-must-be-connected-to-two-workflow-shapes"></a>Der Verbinder muss mit zwei workflowformen verbunden sein
<a name="section11"> </a>

Meldung:
  
    
    
Der Verbinder muss mit zwei workflowformen verbunden sein.
  
    
    
Beispiel:
  
    
    

  
    
    
![Verbinder muss mit zwei Workflow-Shapes verbunden sein](../../images/spd15-wf-error14.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Entfernen von Sackgasse Connectors oder Anfügen an ein zweites Shape.
  
    
    

## <a name="the-diagram-must-only-have-one-workflow-and-one-start-shape"></a>Das Diagramm darf nur einen Workflow und ein Anfangs-Shape haben.
<a name="section12"> </a>

Meldung:
  
    
    
Das Diagramm darf nur einen Workflow und ein Anfangs-Shape haben.
  
    
    
Beispiel:
  
    
    

  
    
    
![Diagramm darf nur einen Workflow und einen Anfang haben](../../images/spd15-wf-error15.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Alle Pfade müssen vom gleichen **Starten** Shape stammen. Entfernen Sie zusätzliche **Starten** shapes, und ordnen Sie die Connectors, um der Pfad an einem Ort zu starten.
  
    
    

## <a name="the-shape-is-not-a-sharepoint-workflow-shape-only-sharepoint-workflow-shapes-can-be-connected-in-a-workflow"></a>Das Shape ist kein SharePoint-Workflow-Shape. In einem Workflow können nur SharePoint-Workflow-Shapes verbunden sein
<a name="section13"> </a>

Meldung:
  
    
    
Das Shape ist kein SharePoint-Workflow-Shape. In einem Workflow können nur SharePoint-Workflow-Shapes verbunden werden.
  
    
    
Beispiel:
  
    
    

  
    
    
![Das Shape ist kein SharePoint-Workflow-Shape](../../images/spd15-wf-error16.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
In der Microsoft SharePoint-Workflow-Vorlage können nur Workflow-Shapes aus den Schablonen der SharePoint-Workflow verwendet werden. Andere Flussdiagrammshapes werden nicht erkannt, und sie verhindern, dass des Workflows SharePoint Designer 2013 exportiert wird.
  
    
    

## <a name="the-start-shape-must-not-have-incoming-connections"></a>Das Anfangs-Shape darf keine eingehenden Verbindungen haben
<a name="section14"> </a>

Meldung:
  
    
    
Das Anfangs-Shape darf keine eingehenden Verbindungen haben
  
    
    
Beispiel:
  
    
    

  
    
    
![Das Anfangs-Shape darf keine eingehenden Verbindungen haben](../../images/spd15-wf-error17.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Entfernen Sie den eingehenden Connector mit dem Shape **zu starten**.
  
    
    

## <a name="the-terminate-shape-must-not-have-outgoing-connections"></a>Das Abschluss-Shape darf keine ausgehende Verbindungen haben.
<a name="section15"> </a>

Meldung:
  
    
    
Das Abschluss-Shape darf keine ausgehende Verbindungen haben.
  
    
    
Beispiel:
  
    
    

  
    
    
![Abschluss-Shape darf keine ausgehenden Verbindungen haben](../../images/spd15-wf-error18.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Entfernen Sie den ausgehenden Connector vom **Abschluss**-Shape.
  
    
    

## <a name="the-workflow-must-have-a-start-shape"></a>Der Workflow muss ein Anfangs-Shape haben
<a name="section16"> </a>

Meldung:
  
    
    
Der Workflow muss ein Anfangs-Shape haben
  
    
    
Beispiel:
  
    
    

  
    
    
![Der Workflow muss ein Anfangs-Shape haben](../../images/spd15-wf-error19.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Fügen Sie ein Shape **Starten** an den Anfang des Workflows, und schließen Sie es an die erste Aktivität.
  
    
    

## <a name="the-workflow-shape-is-not-connected-to-a-terminate-shape"></a>Das Workflow-Shape ist nicht mit Abschluss-Shape verbunden.
<a name="section17"> </a>

Meldung:
  
    
    
Das Workflow-Shape ist nicht mit Abschluss-Shape verbunden.
  
    
    
Beispiel:
  
    
    

  
    
    
![Workflow-Shape ist mit keinem Abschluss verbunden](../../images/spd15-wf-error20.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Wenn der Workflow nicht **Abschluss**-Shape verfügt, fügen Sie einen hinzu, und schließen Sie sie bis zum Ende des Workflows. Wenn ein Workflow-Shape eine Verbindung zu einem anderen Workflow-Shape nicht angezeigt wird (siehe Beispiel), können Sie entfernen oder zu einem anderen Workflow-Shape verbinden.
  
    
    

## <a name="the-workflow-shape-is-not-connected-to-the-workflow"></a>Das Workflow-Shape ist nicht mit dem Workflow verbunden.
<a name="section18"> </a>

Meldung:
  
    
    
Das Workflow-Shape ist nicht mit dem Workflow verbunden.
  
    
    
Beispiel:
  
    
    

  
    
    
![Workflow-Shape ist nicht mit dem Workflow verbunden](../../images/spd15-wf-error21.JPG)
  
    
    
Vorgeschlagene Aktion:
  
    
    
Wenn das Workflow-Shape erforderlich ist, fügen Sie Connectors So fügen Sie es auf den Workflow Pfad hinzu. Anderenfalls Löschen des Shapes.
  
    
    

## <a name="workflow-nesting-levels-must-not-exceed-a-maximum-of-10"></a>Workflow geschachtelte Ebenen darf maximal 10 nicht überschreiten.
<a name="section19"> </a>

Meldung:
  
    
    
Workflow geschachtelte Ebenen darf maximal 10 nicht überschreiten.
  
    
    
Vorgeschlagene Aktion:
  
    
    
Visio Professional 2013 können maximal 10 Ebenen geschachtelter Workflowaktivitäten erkennen. Neu anordnen Sie, um Komplexität eliminiert Aktivitäten oder den Pfad der Workflow in mehr als eine Verzweigung Aufteilen des Workflows.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Neuerungen in Workflows für SharePoint](what-s-new-in-workflows-for-sharepoint)
    
  
-  [Erste Schritte mit Workflows in SharePoint](get-started-with-workflows-in-sharepoint)
    
  
-  [Workflowentwicklung in SharePoint Designer und Visio](workflow-development-in-sharepoint-designer-and-visio)
    
  

  
    
    

