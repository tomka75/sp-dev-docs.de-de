---
title: "Ausführen vorbereitender Schritte zum Einrichten und Konfigurieren einer Entwicklungsumgebung für SharePoint-Workflows"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: b6a3321f-4131-4a8e-9cb7-7a1b4ab9e26b
ms.openlocfilehash: 2c75e0c98642891abe614c6650dc09aa80c5df6f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="prepare-to-set-up-and-configure-a-sharepoint-workflow-development-environment"></a>Ausführen vorbereitender Schritte zum Einrichten und Konfigurieren einer Entwicklungsumgebung für SharePoint-Workflows
Erfahren Sie mehr darüber, wie Sie eine Workflowentwicklungsumgebung für das Entwickeln von SharePoint-Workflows als eigenständige  [Apps für SharePoint](http://msdn.microsoft.com/library/fp179930.aspx) mit Visual Studio 2012 entwickeln.
## <a name="overview-of-workflow-development-in-sharepoint"></a>Übersicht über die Entwicklung von Workflows in SharePoint

Zwar sind Workflows seit den frühen Versionen ein Teil von SharePoint, aber Workflows für SharePoint sind eine wesentlich erweiterte und verbesserte Plattform. 
  
    
    

- Zunächst werden SharePoint-Workflows jetzt in  [Windows Workflow Foundation 4.5](http://msdn.microsoft.com/library/dd489441%28v=vs.110%29) erstellt, das Teil von .NET Framework 4.5 ist.
    
  
- Zweitens wurde das Workflow-Ausführungsmodul,  [Workflow-Manager](http://msdn.microsoft.com/library/windowsazure/jj193528%28v=azure.10%29.aspx), von SharePoint entkoppelt und wird unabhängig ausgeführt. Das sorgt für Flexibilität und Skalierbarkeit. (Beachten Sie, dass aus Gründen der Abwärtskompatibilität das 2010-Vorgängerworkflowmodul Teil von SharePoint bleibt.)
    
  
- Statt Workflows durch Schreiben von C#-Code zu entwickeln, erstellen Sie jetzt Workflows in Visual Studio mit einem Workflow-Designer, der deklarative Ausdrücke verwendet.
    
  
- SharePoint-Workflows können in das neue App-Modell integriert werden, was bedeutet, dass Sie jetzt Workflows in SharePoint-Add-Ins implementieren können.
    
  
- Sie können einen SharePoint-Workflow außerdem mit SharePoint Designer 2013 entwickeln. Weitere Informationen finden Sie unter  [Workflowentwicklung in SharePoint Designer und Visio](workflow-development-in-sharepoint-designer-and-visio.md).
    
  

### <a name="get-started"></a>Erste Schritte

Machen Sie sich zunächst mit dem neuen App-Modell und den SharePoint-Add-Ins zugrunde liegenden Konzepten vertraut, indem Sie sich Folgendes ansehen: 
  
    
    

|||
|:-----|:-----|
| [SharePoint für Entwickler](http://msdn.microsoft.com/de-DE/sharepoint) <br/> |Portal der SharePoint-Entwicklerwebsite, in dem der Schwerpunkt auf Apps für SharePoint liegt.  <br/> |
| [SharePoint-Add-Ins](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |Erfahren Sie, was Apps für SharePoint sind, warum Sie sie erstellen sollten und welche Konzepte für ihre Erstellung in SharePoint grundlegend sind.  <br/> |
| [Neuer Name für Apps für SharePoint](http://msdn.microsoft.com/library/05b07b04-6c8b-4b7e-bd86-e32c589dfead%28Office.15%29.aspx) <br/> |Portal einer Entwicklerwebsite mit dem Schwerpunkt auf der Erstellung von Apps für Office und Apps für SharePoint.  <br/> |
| [Übersicht über die SharePoint-Entwicklung](sharepoint-development-overview.md) <br/> |SharePoint ist eine Entwicklungsplattform für Apps für SharePoint und Farmlösungen. Machen Sie sich mit den Funktionen und Features von SharePoint vertraut, um mit Ihrer Entwicklung zu beginnen.  <br/> |
| [Grundlegendes zu SharePoint-Workflows](sharepoint-workflow-fundamentals.md) <br/> |Bietet eine allgemeine Übersicht über die Workflowinfrastruktur in SharePoint, einschließlich einer Sicht der Plattformarchitektur und der Workflow-Interopbrücke  <br/> |
   
Stellen Sie im nächsten Schritt sicher, dass eine aktuelle Workflowentwicklungsumgebung installiert ist. Sie müssen nicht auf dem SharePoint-Serverrechner entwickeln, benötigen aber natürlich eine SharePoint Server-Installation, mit der Sie entwickeln können.
  
    
    
Im Folgenden sind die erforderlichen Komponenten aufgeführt. Es ist wichtig, dass Sie diese Elemente in der hier beschriebenen Reihenfolge installieren:
  
    
    

1. **Installieren Sie die SharePoint-Umgebung.**
    
  -  [SharePoint-Update (KB2767999)](http://support.microsoft.com/kb/2767999)
    
  
  - Optional können Sie eine [Office 365-Entwicklungsumgebung](http://msdn.microsoft.com/library/office/apps/fp179924%28v=office.15%29) abonnieren.
    
  
2. **Installieren der Workflow-Manager-Umgebung**
    
  -  [Workflow Manager 1.0 kumulativ (KB2799754)](http://support.microsoft.com/kb/2799754/en-us)
    
  
3. **Installieren der Visual Studio 2012-Entwicklungsumgebung**
    
  -  [Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/downloads#vs)
    
  
  -  [Visual Studio 2012 Update 2 (KB2797912)](http://support.microsoft.com/kb/2797912)
    
  
  -  [.NET Framework 4.5-Update (KB2750149)](http://support.microsoft.com/kb/2750149/en-us)
    
  
  -  [Office Developer Tools für Visual Studio 2012](http://aka.ms/OfficeDevToolsForVS2012)
    
  

### <a name="if-you-have-the-preview-version"></a>Wenn Sie die „Vorschau"-Version haben

Wenn Sie Vorabversionen (d. h. eine „Vorschau") von SharePoint Server, Workflow-Manager 1.0 oder Office Developer Tools für Visual Studio 2013 (Versionen vor März 2013) haben, müssen Sie Ihre Installation aktualisieren. Nachfolgend finden Sie eine Liste der geeigneten Updates:
  
    
    

-  [SharePoint-Update (KB2767999)](http://support.microsoft.com/kb/2767999)
    
  
-  [Kumulatives Update für Microsoft Azure Service Bus 1.0 (KB2799752)](http://support.microsoft.com/kb/2799752/en-us)
    
  
-  [Workflow Manager 1.0 kumulativ (KB2799754)](http://support.microsoft.com/kb/2799754/en-us)
    
  

### <a name="you-must-also-update-workflow-projects-created-with-the-preview-version"></a>Sie müssen auch die Workflowprojekte aktualisieren, die mit der „Vorschau"-Version erstellt wurden.

Mit der endgültigen Produktversion der Visual Studio-Workflowkomponenten und ihren zugehörigen Updates werden wichtige Änderungen eingeführt, die die Leistung, Skalierbarkeit und Zuverlässigkeit verbessern. Diese Upgrades erfordern leider, dass Sie Ihre Workflowprojekte aktualisieren, dass Sie über die Vorschautools erstellt haben.
  
    
    
Um diesen Prozess zu erleichtern, bieten wir ein Konvertierungstool an, das Sie über CodePlex abrufen können. Das Tool ist der  [SharePoint Workflow-Konverter für Visual Studio 2012](http://wfconverter.codeplex.com/).
  
    
    
Hier ist eine Zusammenfassung der Änderungen, die eine Aktualisierung Ihrer Workflowprojekte erforderlich machen:
  
    
    

- Aktivitätsverweise auf **Item Guid** werden ersetzt durch **Item Id**. Diese Änderung hat bedeutende Konsequenzen:
    
  - Die Aktivitäten  [LookupSPListItemGuid](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.LookupSPListItemGuid.aspx) und [GetCurrentItemGuid](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.GetCurrentItemGuid.aspx) werden aus den Tools entfernt und durch die Aktivitäten **LookupSPListItemId** und **GetCurrentItemId** ersetzt.
    
  
  - Für andere Aktivitäten, die **Item Guid** verwenden, wurde **Item Id** hinzugefügt und **Item Guid** ausgeblendet. Ihre vorhandenen Projekte, die **Item Guid** verwenden, funktionieren weiterhin (außer bei sehr großen Listen mit mehr als 5000 Elementen, was einer der Gründe für die Änderung ist).
    
  
- Es gibt ein neues Verpackungsformat für Workflows in Apps.
    
  
- Der Workflowaktivitäten-Assemblyverweis in XAML wurde geändert und verweist jetzt auf eine neue Entwurfszeit-Proxyassembly statt auf die tatsächliche SP-Aktivitätenassembly.
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx)
    
  
-  [Neuerungen in Workflows für SharePoint](what-s-new-in-workflows-for-sharepoint.md)
    
  
-  [Workflowentwicklung in SharePoint Designer und Visio](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [Workflows in SharePoint](workflows-in-sharepoint.md)
    
  

