---
title: "Workflowaktions- und -aktivitätenreferenz für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 88e09f75-480f-4a68-87a6-b496350345cc
ms.openlocfilehash: 2be2fd88314a3e961a586ee4b80c80010cc0976f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="workflow-actions-and-activities-reference-for-sharepoint"></a>Workflowaktions- und -aktivitätenreferenz für SharePoint
Erfahren Sie mehr über die Workflowaktionen, die für das Erstellen von Workflows in SharePoint Designer 2013 verfügbar sind, und über die Workflowaktivitätsklassen, die für Workflowentwickler zur Verfügung stehen, die Visual Studio 2012 verwenden.
## <a name="workflow-activities-and-actions"></a>Workflowaktivitäten und -aktionen
<a name="bkm_Activities"> </a>

Workflowaktivitäten sind die Objekte auf Codeebene, die Methodenaufrufe der verschiedenen APIs verarbeiten, welche für das Workflowverhalten verantwortlich sind. Sie verwenden Workflowaktivitäten im Code, indem Sie oder eine andere Entwicklungsumgebung verwenden.
  
    
    
Eine Liste der verfügbaren Aktivitäten finden Sie unter  [Aktivität Workflowklassen in SharePoint](workflow-activity-classes-in-sharepoint.md).
  
    
    
Im Gegensatz dazu sind Workflowaktionen Wrapperobjekte, die diese zugrunde liegenden Aktivitäten kapseln und sie in einer benutzerfreundlichen Form in SharePoint Designer darstellen. Sie verwenden die Workflowaktionen in SharePoint Designer.
  
    
    
Eine Liste der verfügbaren Workflowaktionen finden Sie unter  [Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)](workflow-actions-quick-reference-sharepoint-workflow-platform.md) und [Verwendung der Interop-Workflow-Brücke verfügbar Workflowaktionen](workflow-actions-available-using-the-workflow-interop-bridge.md).
  
    
    

## <a name="windows-workflow-foundation-40-activities"></a>Windows Workflow Foundation 4.0-Aktivitäten
<a name="bkm_WF4"> </a>

Obwohle Ihnen auf der SharePoint-Plattform und -Infrastruktur speziell für die Erstellung benutzerefinierter SharePoint-Workflows ausgelegte Aktivitätsklassen zur Verfügung stehen, können Sie auch die von Windows Workflow Foundation (WF) 4.0 bereitgestellten Aktivitätsklassen verwenden. Diese WF 4.0-Aktivitätsklassen stehen im Microsoft .NET Framework 4 im  [System.Activities.Statements](http://msdn.microsoft.com/en-us/library/system.activities.statements.aspx)-Namespace zur Verfügung.
  
    
    
Die WF 4.0-Aktivitätsklassen stellen einige nützliche Features bereit, die Sie in der SharePoint-Aktivitätsklassenbibliothek möglicherweise nicht finden. So beinhaltet WF 4.0 zum Beispiel die **If**-Klasse, mit der Sie bedingte Aktivitäten erstellen können. Darüber hinaus können Sie mit der  [System.ServiceModel.Activities.Send](http://msdn.microsoft.com/en-us/library/system.servicemodel.activities.send.aspx)-Aktivität eine Verbindung zu Webdienten herstellen.
  
    
    

## <a name="in-this-section"></a>Inhalt dieses Abschnitts
<a name="bkm_inthissection"> </a>


-  [Aktivität Workflowklassen in SharePoint](workflow-activity-classes-in-sharepoint.md)
    
  
-  [Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  
-  [Verwendung der Interop-Workflow-Brücke verfügbar Workflowaktionen](workflow-actions-available-using-the-workflow-interop-bridge.md)
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bkm_addlres"> </a>


-  [Entwickeln von SharePoint-Workflows mit Visual Studio](develop-sharepoint-workflows-using-visual-studio.md)
    
  
-  [Grundlegendes zu SharePoint-Workflows](sharepoint-workflow-fundamentals.md)
    
  
-  [Workflows in SharePoint](workflows-in-sharepoint.md)
    
  

