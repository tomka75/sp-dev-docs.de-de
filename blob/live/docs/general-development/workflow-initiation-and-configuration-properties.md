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
# <a name="workflow-initiation-and-configuration-properties"></a><span data-ttu-id="dc6b1-102">Workflow-Initiierung und Konfigurationseigenschaften</span><span class="sxs-lookup"><span data-stu-id="dc6b1-102">Workflow initiation and configuration properties</span></span>
<span data-ttu-id="dc6b1-103">Finden Sie unter Übersicht über die Initiierung und Zuordnung Eigenschaften, die für Workflows SharePoint festlegt.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-103">See an overview of the initiation and association properties that SharePoint sets on workflows.</span></span>
## 

<span data-ttu-id="dc6b1-p101">Wenn Sie einen Workflow starten, stellt SharePoint automatisch eine Reihe von Zuordnungs- und Initiierungsformularen Eigenschaften, die den Workflow zu unterstützen. Diese sind unten aufgeführt. Die Gruppe von Eigenschaften, die festgelegt werden hingegen etwas je nach, ob es sich um eine **Website** -Workflows oder **einen Listenworkflow** handelt. Diese Unterschiede werden in den Listen identifiziert.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-p101">When you launch a workflow, SharePoint automatically sets a number of association and initiation properties that support the workflow. These are listed below. The set of properties that are set differs slightly depending whether it is a **site** workflows or a **list** workflow. These differences are identified in the lists.</span></span>
  
    
    
<span data-ttu-id="dc6b1-108">Verwenden Sie die folgenden Richtlinien, um zuzuordnen und Ihre Workflows mithilfe des Workflow-Objektmodells (Initialisieren) zu starten:</span><span class="sxs-lookup"><span data-stu-id="dc6b1-108">Use the following guidelines to associate and launch (initiate) your workflows using the workflow object model:</span></span>
  
    
    

- <span data-ttu-id="dc6b1-109">Verwenden Sie die  [PublishSubscriptionForList](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscriptionForList.aspx) -Methode, um eine Zuordnung für **einen Listenworkflow** zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-109">To create an association for a **list** workflow, use the [PublishSubscriptionForList](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscriptionForList.aspx) method.</span></span>
    
  
- <span data-ttu-id="dc6b1-110">Verwenden Sie die  [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) -Methode, um eine Zuordnung für **einen Websiteworkflow** zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-110">To create an association for a **site** workflow, use the [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) method.</span></span>
    
  
- <span data-ttu-id="dc6b1-111">Verwenden Sie die  [StartWorkflowOnListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflowOnListItem.aspx) -Methode, um **einen Listenworkflow** zu initiieren.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-111">To initiate a **list** workflow, use the [StartWorkflowOnListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflowOnListItem.aspx) method.</span></span>
    
  
- <span data-ttu-id="dc6b1-112">Verwenden Sie zum Starten eines **Webseiten**-Workflows die [StartWorkflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflow.aspx)-Methode.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-112">To initiate a **site** workflow, use the [StartWorkflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflow.aspx) method.</span></span>
    
  

> <span data-ttu-id="dc6b1-113">**Hinweis:** Die beiden Methoden zum **Zuordnen** von Workflows befinden sich in der [WorkflowSubscriptionService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.aspx) -Klasse, während die beiden Methoden zum **Starten** von Workflows in der [WorkflowInstanceService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.aspx)-Klasse vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-113">**Note** The two methods for **associating** workflows are found on the [WorkflowSubscriptionService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.aspx) class, while the two methods for **launching** workflows are found on the [WorkflowInstanceService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.aspx) class.</span></span>
  
    
    


## <a name="association-properties"></a><span data-ttu-id="dc6b1-114">Zuordnungseigenschaften</span><span class="sxs-lookup"><span data-stu-id="dc6b1-114">Association properties</span></span>

<span data-ttu-id="dc6b1-p102">Die Werte der Zuordnungseigenschaften werden festgelegt, wenn Sie  [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) aufrufen. Werte der Zuordnung sind Association-Level-Eigenschaften, was bedeutet, dass alle Workflowinstanzen mit einer bestimmten Zuordnung den gleichen Eigenschaftswert freigeben. Sie können einen Zuordnung Eigenschaftswert innerhalb des Workflows selbst abrufen, mithilfe der **GetConfigurationValue** -Aktivitätsfeeds ab.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-p102">The values of association properties are set when you call  [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) . The association property values are association-level properties, meaning that all workflow instances with a given association share the same property value. You can retrieve an association property value within the workflow itself by using the **GetConfigurationValue** activity.</span></span>
  
    
    
<span data-ttu-id="dc6b1-118">Es folgt eine Liste der Zuordnungseigenschaften, die standardmäßig für **Listen** und **Website** -Workflows festgelegt sind, wenn Sie [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) aufrufen.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-118">Following is a list of association properties that are set by default for both **list** and **site** workflows when you call [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) .</span></span>
  
    
    

-  [<span data-ttu-id="dc6b1-119">AssociationTitle</span><span class="sxs-lookup"><span data-stu-id="dc6b1-119">AssociationTitle</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.AssociationTitle.aspx)
    
  
-  [<span data-ttu-id="dc6b1-120">AssociatorUserId</span><span class="sxs-lookup"><span data-stu-id="dc6b1-120">AssociatorUserId</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.AssociatorUserId.aspx)
    
  
-  [<span data-ttu-id="dc6b1-121">LayoutsFolder</span><span class="sxs-lookup"><span data-stu-id="dc6b1-121">LayoutsFolder</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.LayoutsFolder.aspx)
    
  
-  <span data-ttu-id="dc6b1-122">ParentContentTypeId()</span><span class="sxs-lookup"><span data-stu-id="dc6b1-122">ParentContentTypeId()</span></span>
    
  
- <span data-ttu-id="dc6b1-123">**HistoryListId***</span><span class="sxs-lookup"><span data-stu-id="dc6b1-123">**HistoryListId***</span></span>
    
  
- <span data-ttu-id="dc6b1-124">**TaskListId***</span><span class="sxs-lookup"><span data-stu-id="dc6b1-124">**TaskListId***</span></span>
    
  
- <span data-ttu-id="dc6b1-125">**FormData***</span><span class="sxs-lookup"><span data-stu-id="dc6b1-125">formData()</span></span>
    
  
- <span data-ttu-id="dc6b1-126">**SharePointWorkflowContext.Subscription.EventSourceId***</span><span class="sxs-lookup"><span data-stu-id="dc6b1-126">**SharePointWorkflowContext.Subscription.EventSourceId***</span></span>
    
  
- <span data-ttu-id="dc6b1-127">**SharePointWorkflowContext.Subscription.EventType***</span><span class="sxs-lookup"><span data-stu-id="dc6b1-127">**SharePointWorkflowContext.Subscription.EventType***</span></span>
    
  
- <span data-ttu-id="dc6b1-128">**SharePointWorkflowContext.Subscription.DisplayName***</span><span class="sxs-lookup"><span data-stu-id="dc6b1-128">**SharePointWorkflowContext.Subscription.DisplayName***</span></span>
    
  
- <span data-ttu-id="dc6b1-129">**SharePointWorkflowContext.Subscription.Id***</span><span class="sxs-lookup"><span data-stu-id="dc6b1-129">**SharePointWorkflowContext.Subscription.Id***</span></span>
    
  
- <span data-ttu-id="dc6b1-130">**SharePointWorkflowContext.Subscription.Name***</span><span class="sxs-lookup"><span data-stu-id="dc6b1-130">**SharePointWorkflowContext.Subscription.Name***</span></span>
    
  
- <span data-ttu-id="dc6b1-131">**SharePointWorkflowContext.Subscription.CreatedDate***</span><span class="sxs-lookup"><span data-stu-id="dc6b1-131">**SharePointWorkflowContext.Subscription.CreatedDate***</span></span>
    
  

> <span data-ttu-id="dc6b1-132">**Wichtig:** Eigenschaften, die mit einem Sternchen (\*) markiert sind, sind nicht in den Workflow-APIs definiert, sodass Sie für den Zugriff auf diese Eigenschaften einfach die entsprechenden Zeichenfolgenwerte verwenden können.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-132">**Important** Properties marked with an asterisk (*) are not defined in the Workflow APIs, so to access them simply use their string values.</span></span> 
  
    
    

<span data-ttu-id="dc6b1-133">Für **Listen**-Workflows gibt es vier zusätzliche Zuordnungseigenschaften, die standardmäßig festgelegt werden, wenn Sie [PublishSubscriptionForList (WorkflowSubscription, Guid)](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscriptionForList.aspx) aufrufen.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-133">In the case of **list** workflows, there are four additional association properties that are set by default when you call [PublishSubscriptionForList(WorkflowSubscription, Guid)](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscriptionForList.aspx) .</span></span>
  
    
    

-  [<span data-ttu-id="dc6b1-134">ListId</span><span class="sxs-lookup"><span data-stu-id="dc6b1-134">listId</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.ListId.aspx)
    
  
-  [<span data-ttu-id="dc6b1-135">ListName</span><span class="sxs-lookup"><span data-stu-id="dc6b1-135">ListName</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.ListName.aspx)
    
  
- <span data-ttu-id="dc6b1-136">**StatusColumnCreated***</span><span class="sxs-lookup"><span data-stu-id="dc6b1-136">**StatusColumnCreated***</span></span>
    
  
- <span data-ttu-id="dc6b1-137">**StatusFieldName***</span><span class="sxs-lookup"><span data-stu-id="dc6b1-137">**StatusFieldName***</span></span>
    
  

> <span data-ttu-id="dc6b1-138">**Wichtig:** Eigenschaften, die mit einem Sternchen (\*) markiert sind, sind nicht in den Workflow-APIs definiert, sodass Sie für den Zugriff auf diese Eigenschaften einfach die entsprechenden Zeichenfolgenwerte verwenden können.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-138">**Important** Properties marked with an asterisk (*) are not defined in the Workflow APIs, so to access them simply use their string values.</span></span> 
  
    
    


> <span data-ttu-id="dc6b1-139">**Hinweis:** Sie können benutzerdefinierte Zuordnungseigenschaften mithilfe eines Zuordnungsformulars hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-139">**Note** You can add custom association properties by using an association form.</span></span> 
  
    
    


## <a name="initiation-properties"></a><span data-ttu-id="dc6b1-140">Initiierungseigenschaften</span><span class="sxs-lookup"><span data-stu-id="dc6b1-140">Initiation properties</span></span>

<span data-ttu-id="dc6b1-p103">Initiation Eigenschaften sind externe Variablen, deren Werte festgelegt werden, wenn der Workflow - d. h., initiiert wird Wenn Sie **StartWorkflow**aufrufen. Beachten Sie jedoch, dass der Eigenschaftswerte zur Laufzeit über innerhalb der Workflow-Instanz mithilfe der **ExternalVariableValue** Aktivitätsfeeds aktualisiert werden können. Sie können die Werte von externen Variablen von *außerhalb*  des Workflows mithilfe von [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstance.Properties.aspx) abrufen.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-p103">Initiation properties are external variables whose values are set when the workflow is initiated - that is, when you call **StartWorkflow**. Note, however, that the property values can be updated at runtime from within the workflow instance by using the **ExternalVariableValue** activity. You can retrieve the values of external variables from *outside*  the workflow by using [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstance.Properties.aspx) .</span></span>
  
    
    
<span data-ttu-id="dc6b1-144">Externe Variablenwerte sind für jede Workflowinstanz (im Gegensatz zur Zuordnungseigenschaften, in dem alle Workflowinstanzen die gleichen Eigenschaftswerte gemeinsam) spezifisch.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-144">External variable values are specific to each workflow instance (as opposed to association properties, where all workflow instances share the same property values).</span></span> 
  
    
    
<span data-ttu-id="dc6b1-145">Alle Workflowinstanzen (Liste und Site) verfügen einige externen Variablen, die standardmäßig beim Aufruf von **StartWorkflow**festgelegt werden:</span><span class="sxs-lookup"><span data-stu-id="dc6b1-145">All workflow instances (both list and site) have some external variables that are set by default when you call **StartWorkflow**:</span></span>
  
    
    

-  [<span data-ttu-id="dc6b1-146">InitiatorUserId</span><span class="sxs-lookup"><span data-stu-id="dc6b1-146">InitiatorUserId</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.InitiatorUserId.aspx)
    
  
-  [<span data-ttu-id="dc6b1-147">RetryCode</span><span class="sxs-lookup"><span data-stu-id="dc6b1-147">RetryCode</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.RetryCode.aspx)
    
  
-  [<span data-ttu-id="dc6b1-148">RelatedItems</span><span class="sxs-lookup"><span data-stu-id="dc6b1-148">RelatedItems</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.RelatedItems.aspx)
    
  
<span data-ttu-id="dc6b1-149">Listeninstanzen Workflows verfügen einige zusätzlichen externen Variablen, die standardmäßig beim Aufruf von  [StartWorkflowOnListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflowOnListItem.aspx) festgelegt werden:</span><span class="sxs-lookup"><span data-stu-id="dc6b1-149">List workflows instances have some additional external variables that are set by default when you call  [StartWorkflowOnListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflowOnListItem.aspx) :</span></span>
  
    
    

-  [<span data-ttu-id="dc6b1-150">CurrentItemUrl</span><span class="sxs-lookup"><span data-stu-id="dc6b1-150">CurrentItemUrl</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.CurrentItemUrl.aspx)
    
  
-  [<span data-ttu-id="dc6b1-151">ItemId</span><span class="sxs-lookup"><span data-stu-id="dc6b1-151">item-id</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.ItemId.aspx)
    
  
-  [<span data-ttu-id="dc6b1-152">ItemGuid</span><span class="sxs-lookup"><span data-stu-id="dc6b1-152">ItemGuid</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.ItemGuid.aspx)
    
  
-  [<span data-ttu-id="dc6b1-153">ContextListId</span><span class="sxs-lookup"><span data-stu-id="dc6b1-153">ContextListId</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.ContextListId.aspx)
    
  
-  [<span data-ttu-id="dc6b1-154">UniqueId</span><span class="sxs-lookup"><span data-stu-id="dc6b1-154">UniqueID</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.UniqueId.aspx)
    
  

> <span data-ttu-id="dc6b1-155">**Hinweis:** Sie können benutzerdefinierte Initiierungseigenschaften mit einem Initiierungsformular hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="dc6b1-155">**Note** You can add custom initiation properties by using an initiation form.</span></span> 
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="dc6b1-156">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="dc6b1-156">Additional resources</span></span>
<span data-ttu-id="dc6b1-157"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="dc6b1-157"></span></span>


-  [<span data-ttu-id="dc6b1-158">Entwickeln von SharePoint-Workflows mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dc6b1-158">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio.md)
    
  
-  [<span data-ttu-id="dc6b1-159">Gewusst wie: Erstellen von SharePoint-Workflows mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dc6b1-159">How to: Create SharePoint Workflows using Visual Studio</span></span>](how-to-create-sharepoint-workflows-using-visual-studio.md)
    
  

  
    
    

