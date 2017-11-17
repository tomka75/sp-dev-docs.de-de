---
title: SharePoint-Workflow-Objektmodell
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: be615a89-3201-4cd8-bbc7-15f3abf9f668
ms.openlocfilehash: 0b02055055f6777b6c641c1a1445194573c54de5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-workflow-object-model"></a>SharePoint-Workflow-Objektmodell
Rufen Sie eine kurze Einführung in das Workflowobjektmodell in SharePoint.
## <a name="sharepoint-workflow-object-model"></a>SharePoint-Workflow-Objektmodell
<a name="bk_SPwfom"> </a>

Das SharePoint-Objektmodell basiert auf der Basis des .NET Framework 4-Objektmodells für Windows Workflow Foundation 4, jedoch mit Innovationen, die in SharePoint-Workflowfunktionen im Allgemeinen und in SharePoint-Add-Ins insbesondere ermöglichen. Das systemeigene .NET Framework 4-Objektmodell für Windows Workflow Foundation 4 befindet sich in der .NET Framework  [System.Workflow Namespaces](http://msdn.microsoft.com/en-us/library/gg145026.aspx).
  
    
    
Eine Möglichkeit, die SharePoint-Workflow-Objektmodell vorstellen ist als eine Reihe von Workflow-Dienste. Es gibt vier Dienste: 
  
    
    

- **Instanz Verwaltungsdienst:** Verwaltet den Workflow-Instanzen und deren Ausführung.
    
  
- **Deployment-Dienst:** Verwaltet die Bereitstellung von workflowdefinitionen für.
    
  
- **Interop-Dienst:** Verwaltet die Interop-Brücke zur Unterstützung von legacy-Workflows.
    
  
- **Messaging-Dienst:** Verwaltet Message queuing und Transport.
    
  

### <a name="sharepoint-workflow-namespaces"></a>Namespaces für die SharePoint-Workflows

Das Objektmodell der SharePoint-Workflow ist andererseits, in zehn Namespaces enthalten: fünf davon sind SharePoint-Namespaces und fünf andere Microsoft Office Namespaces sind.
  
    
    
 **Microsoft.SharePoint** -Namespaces:
  
    
    

-  [Microsoft.SharePoint.Workflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Workflow.aspx)
    
  
-  [Microsoft.SharePoint.Workflow.Application](https://msdn.microsoft.com/library/Microsoft.SharePoint.Workflow.Application.aspx)
    
  
-  [Microsoft.SharePoint.WorkflowActions](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.aspx)
    
  
-  [Microsoft.SharePoint.WorkflowActions.WithKey](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.WithKey.aspx)
    
  
-  [Microsoft.SharePoint.WorkflowServices](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.aspx)
    
  
-  [Microsoft.SharePoint.WorkflowServices.Activities](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.aspx)
    
  
 **Microsoft.Office** -Namespaces:
  
    
    

-  [Microsoft.Office.Workflow](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.aspx)
    
  
-  [Microsoft.Office.Workflow.Actions](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Actions.aspx)
    
  
-  [Microsoft.Office.Workflow.Feature](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Feature.aspx)
    
  
-  [Microsoft.Office.Workflow.Routing](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Routing.aspx)
    
  
-  [Microsoft.Office.Workflow.Utility](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Utility.aspx)
    
  

### <a name="sharepoint-workflow-schemas"></a>SharePoint-Workflow-schemas

Verweis Inhalte für SharePoint-Schemas in den Anspruch  [Workflowschemas](http://msdn.microsoft.com/library/b36ded16-3ffd-4931-811e-c402c1e35b07%28Office.15%29.aspx)Verweisknoten enthalten ist, und folgende enthalten:
  
    
    

-  [WorkflowActions4-Schemareferenz](http://msdn.microsoft.com/library/1c0112de-0139-e64d-d3d6-658541695391%28Office.15%29.aspx)
    
  
-  [WorkflowActions3-Schemareferenz](http://msdn.microsoft.com/library/7a03ead8-30e0-4601-9c6f-edfb04ce57f9%28Office.15%29.aspx)
    
  
-  [Übersicht zum Workflowkonfigurationsschema](http://msdn.microsoft.com/library/63824239-6eb2-4cf1-ba84-44eace4d3781%28Office.15%29.aspx)
    
  
-  [WorkflowInfo-Schemareferenz](http://msdn.microsoft.com/library/f3bdcc70-15a0-44b2-9b01-330f13430354%28Office.15%29.aspx)
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_additionalresources"> </a>


-  
  [Einführung für Entwickler für Windows Workflow Foundation (WF) in .NET 4](http://msdn.microsoft.com/en-us/library/ee342461.aspx)
    
  
-  [Windows Workflow Foundation 4.0: Hello, Workflow!](http://weblogs.asp.net/gunnarpeipman/archive/2009/07/08/windows-workflow-foundation-4-0-hello-workflow.aspx)
    
  
-  [Windows Workflow Foundation (WF) - Screencasts](http://msdn.microsoft.com/en-us/netframework/dd733248)
    
  
-  [Workflowaktions- und -aktivitätenreferenz für SharePoint](workflow-actions-and-activities-reference-for-sharepoint.md)
    
  
-  [Entwickeln von SharePoint-Workflows mit Visual Studio](develop-sharepoint-workflows-using-visual-studio.md)
    
  

  
    
    

