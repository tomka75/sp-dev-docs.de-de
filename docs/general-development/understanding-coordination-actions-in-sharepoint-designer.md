---
title: Verstehen von Koordinationsaktionen in SharePoint Designer 2013
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 33fbcf91-0a5d-47ab-85a9-9d2d556a204d
ms.openlocfilehash: 2f70d861564d5c1496d72a479e39329cfdc15a88
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="understanding-coordination-actions-in-sharepoint-designer-2013"></a>Verstehen von Koordinationsaktionen in SharePoint Designer 2013
Koordinationsaktionen in SharePoint Designer 2013 dienen zum Starten eines Workflows, die auf der SharePoint 2010-Workflow-Plattform von innerhalb eines Workflows auf der SharePoint-Workflow-Plattform integriert.

   

## <a name="coordination-actions-in-sharepoint-designer-2013"></a>Koordinierungsaktionen in SharePoint Designer 2013
<a name="section1"> </a>

Es sind zwei Koordinationsaktionen in SharePoint Designer 2013 verfügbar. Beide Aktionen sind nur für die SharePoint-Workflow-Plattform verfügbar. Diese Aktionen sind:
  
    
    

- Listenworkflow starten: zum Starten eines Workflows für eine bestimmte Liste entwickelt wurde.
    
  
- Starten Sie einen Website-Workflow: zum Starten eines Workflows für die Website entwickelt wurden.
    
  
Koordinierung Aktionen werden im Dropdown-Menü **Aktionen** angezeigt, bei der Erstellung eines Workflows basierend auf der SharePoint-Workflow-Plattform, wie in der Abbildung dargestellt.
  
    
    

**Abbildung: Koordinierungsaktionen in SharePoint Designer**

  
    
    

  
    
    
![Koordinierungsaktionen in SharePoint Designer](../images/SPD15-CoordinationActions.png)
  
    
    
Beide Aktionen dienen zum Starten eines Workflows, die auf der SharePoint 2010-Workflow-Plattform mithilfe eines Workflows auf der SharePoint-Workflow-Plattform integriert.
  
    
    

    
> **Wichtig:** Die Koordinationsaktionen unterstützen nur das Aufrufen eines auf der SharePoint 2010-Workflowplattform basierten Workflows von einem auf der SharePoint-Workflowplattform basierten Workflow. Das Aufrufen eines auf der SharePoint-Workflowplattform basierten Workflows von einem auf derselben Plattform basierten Workflow wird nicht unterstützt. 
  
    
    


## <a name="using-coordination-actions"></a>Verwenden von Koordinationsaktionen
<a name="section2"> </a>

Es gibt eine Reihe von Aktionen, die in der SharePoint Workflow-Plattform veraltet sind. Legacy-Workflows zur Erfüllung können Sie Koordinationsaktionen verwenden. Koordinationsaktionen dienen zum Starten einer Listenworkflow oder Website-Workflow, der mithilfe der SharePoint 2010-Workflow-Plattform erstellt wurde.
  
    
    
Eine Aktion Koordinierung umfasst drei bearbeitbare Bereichen wie in der Abbildung dargestellt.
  
    
    

**Abbildung: Starten einer Listenworkflow-koordinierungsaktion**

  
    
    

  
    
    
![Starten einer Listenworkflow-Koordinierungsaktion](../images/SPD15-CoordinationActions2.png)
  
    
    
Die drei bearbeitbaren Bereiche sind: 
  
    
    

- **Workflow für SharePoint 2010** Wählen Sie den zu startenden Workflow 2010 aus.
    
  
- **Parameter** Parameter zum Senden an die 2010-Workflows.
    
  
- **dieses Element** Das Element der 2010-Workflows ausgeführt werden soll, klicken Sie auf.
    
  
Klicken Sie auf einen bearbeitbaren Link, um Informationen eingeben. Klicken Sie auf den Link **SharePoint 2010-Listenworkflow** beispielsweise markieren Sie den zu startenden Workflow 2010. Ein Dialogfeld angezeigt wird, wählen Sie den Workflow verwendet werden, wie in der Abbildung dargestellt.
  
    
    

**Abbildung: Auswählen eines Workflows basierend auf der 2010-Plattform**

  
    
    

  
    
    
![Auswählen eines Workflows basierend auf der 2010-Plattform](../images/SPD15-CoordinationActions3.png)
  
    
    

  
    
    

  
    
    

  
    
    
SharePoint 2010-Workflow-Plattform Workflow-Instanzen, die innerhalb eines SharePoint-Workflows aus koordiniert werden werden auf der Workflowstatusseite im Abschnitt Statusseite aufgelistet, wie in der Abbildung dargestellt.
  
    
    

**Abbildung: Workflow-Statusseite Listet die untergeordneten Workflows**

  
    
    

  
    
    
![Auf der Workflowstatusseite sind die Unterworkflows aufgeführt.](../images/SPD15-CorrelationActions4.png)
  
    
    

  
    
    

  
    
    

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Neuerungen in SharePoint-Workflows](http://msdn.microsoft.com/library/6ab8a28b-fa2f-4530-8b55-a7f663bf15ea.aspx)
    
  
-  [Erste Schritte mit SharePoint-Workflows](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)
    
  
-  [Verstehen von Wörterbuchaktionen in SharePoint Designer 2013](understanding-dictionary-actions-in-sharepoint-designer.md)
    
  

  
    
    

