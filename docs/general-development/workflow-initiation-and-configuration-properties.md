---
title: Workflow-Initiierung und Konfigurationseigenschaften
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7386bbf9-3ed6-4732-bcdb-b27baed7397e
ms.openlocfilehash: eb69b75b91289cca91edb448242b4f233c7a08f7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="workflow-initiation-and-configuration-properties"></a>Workflow-Initiierung und Konfigurationseigenschaften
Finden Sie unter Übersicht über die Initiierung und Zuordnung Eigenschaften, die für Workflows SharePoint festlegt.
## 

Wenn Sie einen Workflow starten, stellt SharePoint automatisch eine Reihe von Zuordnungs- und Initiierungsformularen Eigenschaften, die den Workflow zu unterstützen. Diese sind unten aufgeführt. Die Gruppe von Eigenschaften, die festgelegt werden hingegen etwas je nach, ob es sich um eine **Website** -Workflows oder **einen Listenworkflow** handelt. Diese Unterschiede werden in den Listen identifiziert.
  
    
    
Verwenden Sie die folgenden Richtlinien, um zuzuordnen und Ihre Workflows mithilfe des Workflow-Objektmodells (Initialisieren) zu starten:
  
    
    

- Verwenden Sie die  [PublishSubscriptionForList](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscriptionForList.aspx) -Methode, um eine Zuordnung für **einen Listenworkflow** zu erstellen.
    
  
- Verwenden Sie die  [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) -Methode, um eine Zuordnung für **einen Websiteworkflow** zu erstellen.
    
  
- Verwenden Sie die  [StartWorkflowOnListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflowOnListItem.aspx) -Methode, um **einen Listenworkflow** zu initiieren.
    
  
- Verwenden Sie zum Starten eines **Webseiten**-Workflows die [StartWorkflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflow.aspx)-Methode.
    
  

> **Hinweis:** Die beiden Methoden zum **Zuordnen** von Workflows befinden sich in der [WorkflowSubscriptionService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.aspx) -Klasse, während die beiden Methoden zum **Starten** von Workflows in der [WorkflowInstanceService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.aspx)-Klasse vorhanden sind.
  
    
    


## <a name="association-properties"></a>Zuordnungseigenschaften

Die Werte der Zuordnungseigenschaften werden festgelegt, wenn Sie  [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) aufrufen. Werte der Zuordnung sind Association-Level-Eigenschaften, was bedeutet, dass alle Workflowinstanzen mit einer bestimmten Zuordnung den gleichen Eigenschaftswert freigeben. Sie können einen Zuordnung Eigenschaftswert innerhalb des Workflows selbst abrufen, mithilfe der **GetConfigurationValue** -Aktivitätsfeeds ab.
  
    
    
Es folgt eine Liste der Zuordnungseigenschaften, die standardmäßig für **Listen** und **Website** -Workflows festgelegt sind, wenn Sie [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) aufrufen.
  
    
    

-  [AssociationTitle](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.AssociationTitle.aspx)
    
  
-  [AssociatorUserId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.AssociatorUserId.aspx)
    
  
-  [LayoutsFolder](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.LayoutsFolder.aspx)
    
  
-  ParentContentTypeId()
    
  
- **HistoryListId***
    
  
- **TaskListId***
    
  
- **FormData***
    
  
- **SharePointWorkflowContext.Subscription.EventSourceId***
    
  
- **SharePointWorkflowContext.Subscription.EventType***
    
  
- **SharePointWorkflowContext.Subscription.DisplayName***
    
  
- **SharePointWorkflowContext.Subscription.Id***
    
  
- **SharePointWorkflowContext.Subscription.Name***
    
  
- **SharePointWorkflowContext.Subscription.CreatedDate***
    
  

> **Wichtig:** Eigenschaften, die mit einem Sternchen (\*) markiert sind, sind nicht in den Workflow-APIs definiert, sodass Sie für den Zugriff auf diese Eigenschaften einfach die entsprechenden Zeichenfolgenwerte verwenden können. 
  
    
    

Für **Listen**-Workflows gibt es vier zusätzliche Zuordnungseigenschaften, die standardmäßig festgelegt werden, wenn Sie [PublishSubscriptionForList (WorkflowSubscription, Guid)](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscriptionForList.aspx) aufrufen.
  
    
    

-  [ListId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.ListId.aspx)
    
  
-  [ListName](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.ListName.aspx)
    
  
- **StatusColumnCreated***
    
  
- **StatusFieldName***
    
  

> **Wichtig:** Eigenschaften, die mit einem Sternchen (\*) markiert sind, sind nicht in den Workflow-APIs definiert, sodass Sie für den Zugriff auf diese Eigenschaften einfach die entsprechenden Zeichenfolgenwerte verwenden können. 
  
    
    


> **Hinweis:** Sie können benutzerdefinierte Zuordnungseigenschaften mithilfe eines Zuordnungsformulars hinzufügen. 
  
    
    


## <a name="initiation-properties"></a>Initiierungseigenschaften

Initiation Eigenschaften sind externe Variablen, deren Werte festgelegt werden, wenn der Workflow - d. h., initiiert wird Wenn Sie **StartWorkflow**aufrufen. Beachten Sie jedoch, dass der Eigenschaftswerte zur Laufzeit über innerhalb der Workflow-Instanz mithilfe der **ExternalVariableValue** Aktivitätsfeeds aktualisiert werden können. Sie können die Werte von externen Variablen von *außerhalb*  des Workflows mithilfe von [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstance.Properties.aspx) abrufen.
  
    
    
Externe Variablenwerte sind für jede Workflowinstanz (im Gegensatz zur Zuordnungseigenschaften, in dem alle Workflowinstanzen die gleichen Eigenschaftswerte gemeinsam) spezifisch. 
  
    
    
Alle Workflowinstanzen (Liste und Site) verfügen einige externen Variablen, die standardmäßig beim Aufruf von **StartWorkflow**festgelegt werden:
  
    
    

-  [InitiatorUserId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.InitiatorUserId.aspx)
    
  
-  [RetryCode](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.RetryCode.aspx)
    
  
-  [RelatedItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.RelatedItems.aspx)
    
  
Listeninstanzen Workflows verfügen einige zusätzlichen externen Variablen, die standardmäßig beim Aufruf von  [StartWorkflowOnListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflowOnListItem.aspx) festgelegt werden:
  
    
    

-  [CurrentItemUrl](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.CurrentItemUrl.aspx)
    
  
-  [ItemId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.ItemId.aspx)
    
  
-  [ItemGuid](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.ItemGuid.aspx)
    
  
-  [ContextListId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.ContextListId.aspx)
    
  
-  [UniqueId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.UniqueId.aspx)
    
  

> **Hinweis:** Sie können benutzerdefinierte Initiierungseigenschaften mit einem Initiierungsformular hinzufügen. 
  
    
    


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Entwickeln von SharePoint-Workflows mit Visual Studio](develop-sharepoint-workflows-using-visual-studio.md)
    
  
-  [Gewusst wie: Erstellen von SharePoint-Workflows mit Visual Studio](how-to-create-sharepoint-workflows-using-visual-studio.md)
    
  

  
    
    

