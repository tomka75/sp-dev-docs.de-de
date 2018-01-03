---
title: "Konfigurieren von MSMQ für SharePoint-Workflows"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c0e130f6-c210-44ea-83ed-b327f04551d6
ms.openlocfilehash: 80b380299e29ad78eb8e8475c076f360971316b2
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="configure-msmq-for-sharepoint-workflows"></a><span data-ttu-id="159ed-102">Konfigurieren von MSMQ für SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="159ed-102">Configure MSMQ for SharePoint workflows</span></span>

<span data-ttu-id="159ed-103">Informationen Sie zum Konfigurieren von Microsoft Message Queuing (MSMQ) in SharePoint asynchrones Ereignis messaging in SharePoint-Workflows unterstützen.</span><span class="sxs-lookup"><span data-stu-id="159ed-103">Learn how to configure Microsoft Message Queuing (MSMQ) in SharePoint to support asynchronous event messaging in SharePoint workflows.</span></span> 

## <a name="enabling-msmq"></a><span data-ttu-id="159ed-104">Aktivieren von MSMQ</span><span class="sxs-lookup"><span data-stu-id="159ed-104">Enabling MSMQ</span></span>

<span data-ttu-id="159ed-p101">MSMQ ist ein Windows Server-Feature, das Sie auf Ihrem Computer SharePoint Server aktivieren können, um asynchrones Ereignis messaging in SharePoint-Workflows zu ermöglichen. Um asynchrones Ereignis messaging unterstützen möchten, müssen Sie MSMQ auf Ihrem Computer SharePoint Server aktivieren.</span><span class="sxs-lookup"><span data-stu-id="159ed-p101">MSMQ is a Windows Server feature that you can enable on your SharePoint Server computer to allow asynchronous event messaging in SharePoint workflows. To support asynchronous event messaging, you must enable MSMQ on your SharePoint Server computer.</span></span>
  
    
    
<span data-ttu-id="159ed-p102">MSMQ wird als „Feature“ in Windows Server bereitgestellt. Wenn Sie MSMQ aktivieren möchten, gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="159ed-p102">MSMQ is provided as a "Feature" in Windows Server. To enable MSMQ, do the following:</span></span>
  
    
    

> <span data-ttu-id="159ed-109">**Wichtig:** Die Screenshots in diesem Artikel stammen aus Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="159ed-109">**Important:** The screen shots included here are from Windows Server 2008 R2.</span></span> <span data-ttu-id="159ed-110">In Windows Server 2012 kann die Benutzeroberfläche zum Aktivieren dieses Features anders aussehen.</span><span class="sxs-lookup"><span data-stu-id="159ed-110">The UI may change for enabling this feature in Windows Server 2012.</span></span> 
  
    
    


1. <span data-ttu-id="159ed-111">Öffnen Sie auf Ihrem SharePoint Server-Computer die Komponente **Server-Manager**.</span><span class="sxs-lookup"><span data-stu-id="159ed-111">On your SharePoint Server computer, open **Server Manager**.</span></span>
    
  
2. <span data-ttu-id="159ed-112">Wählen Sie im linken Bereich der **Features**-Symbol aus, und wählen Sie dann **Features hinzufügen**, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="159ed-112">Select the **Features** icon in the left pane, then select **Add Features**, as depicted in Figure 1.</span></span>
    
   <span data-ttu-id="159ed-113">**Abbildung 1: Hinzufügen des Message Queuing-Features.**</span><span class="sxs-lookup"><span data-stu-id="159ed-113">**Figure 1. Adding the Message Queuing feature.**</span></span>

  

  ![Abbildung 1: Hinzufügen des Message Queuing-Features.](../images/ng_MsmqFeature.png)
  

  

  
3. <span data-ttu-id="159ed-p105">Wählen Sie im **Assistenten zum Hinzufügen von Features**, die angezeigt wird, **Message Queuing**. Akzeptieren Sie die Standardauswahl, und klicken Sie dann klicken Sie auf **Weiter** und dann auf **Installieren**.</span><span class="sxs-lookup"><span data-stu-id="159ed-p105">In the **Add Features Wizard** that appears, select **Message Queuing**. Accept the default selections and then click **Next**, then click **Install**.</span></span>
    
  
4. <span data-ttu-id="159ed-118">Jetzt müssen Sie den Computer neu starten.</span><span class="sxs-lookup"><span data-stu-id="159ed-118">You must now restart your computer.</span></span>
    
  
5. <span data-ttu-id="159ed-p106">Nach dem Neustart, öffnen Sie den **Server Manager**, und öffnen Sie **Message Queuing-** Symbol im linken Bereich. Beachten Sie, dass sie jetzt eine **Message Queuing-** Ordner und seiner Unterverzeichnisse enthält, wie in Abbildung 2 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="159ed-p106">Once restarted, open **Server Manager** and then open **Message Queuing** icon in the left pane. Notice that it now contains a **Message Queuing** folder and subdirectories, as depicted in Figure 2.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="159ed-121">In Windows Server 2012 befinden sich die Warteschlangen nicht unter **Server-Manager**.</span><span class="sxs-lookup"><span data-stu-id="159ed-121">Note: In Windows Server 2012 you will not find the queues in **Server Manager**.</span></span> <span data-ttu-id="159ed-122">Wechseln Sie stattdessen zu **Computerverwaltung**, und wählen Sie dann **Dienste und Anwendungen** aus.</span><span class="sxs-lookup"><span data-stu-id="159ed-122">Instead, go to **Computer Management**, then select **Services and applications**.</span></span> 

6. <span data-ttu-id="159ed-p108">Wählen Sie das Unterverzeichnis namens **Private Warteschlangen** aus. Dies ist das Verzeichnis, in dem Ihre Workflow-Ereignisnachrichten gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="159ed-p108">Select the subdirectory named **Private Queues**. This is the directory in which your workflow event messages are stored.</span></span>
    
   <span data-ttu-id="159ed-125">**Abbildung 2. Das Feature für die Message Queuing-zu-Server-Manager hinzugefügt.**</span><span class="sxs-lookup"><span data-stu-id="159ed-125">**Figure 2. The Message Queuing feature added to Server Manager.**</span></span>

    ![Abbildung 2: Das Message Queuing-Feature hinzugefügt zu Ser](../images/ng_MsmqQueues.png)
  
    > [!NOTE]
    > <span data-ttu-id="159ed-128">Beim ersten Hinzufügen des Features **Message Queuing** ist der Ordner **Private Warteschlangen** leer.</span><span class="sxs-lookup"><span data-stu-id="159ed-128">Note: When you first add the **Message Queuing** feature, the **Private Queues** folder is empty.</span></span> <span data-ttu-id="159ed-129">Nach der Ausführung eines Workflows, der ein Ereignis ausgelöst (oder eines Workflows, der durch Ausführung eines SharePoint-Inhaltsänderungsereignisses ausgelöst wird), ist der Ordner **Private Warteschlangen** wie in Abbildung 2 dargestellt gefüllt.</span><span class="sxs-lookup"><span data-stu-id="159ed-129">However, after a workflow runs that fires an event (or a workflow triggered by a SharePoint content change event runs), the **Private Queues** folder is populated as shown in Figure 2.</span></span>

7. <span data-ttu-id="159ed-p111">Um die Installation abzuschließen, müssen Sie die **SPWorkflowServiceApplicationProxy.AllowQueue** -Eigenschaft auf **true** mithilfe eines Skripts Windows PowerShell festlegen. Führen Sie in der **SharePoint-Zentraladministration Shell** folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="159ed-p111">To complete the installation, you must set the **SPWorkflowServiceApplicationProxy.AllowQueue** property to **true** using a Windows PowerShell script. In the **SharePoint Administration shell**, run the following:</span></span>
    
```
  
$proxy = Get-SPWorkflowServiceApplicationProxy
$proxy.AllowQueue = $true;
$proxy.Update();

```


## <a name="troubleshooting-msmq"></a><span data-ttu-id="159ed-132">Problembehandlung bei MSMQ</span><span class="sxs-lookup"><span data-stu-id="159ed-132">Troubleshooting MSMQ</span></span>

<span data-ttu-id="159ed-p112">Windows-Entwicklercenter bietet ausführliche Dokumentation von MSMQ. Es folgen einige nützlichen Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="159ed-p112">The Windows Developer Center provides extensive documentation of MSMQ. Following are some useful resources:</span></span>
  
    
    

-  <span data-ttu-id="159ed-135">
  [Zu Message Queuing](http://msdn.microsoft.com/en-us/library/windows/desktop/ms706032%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="159ed-135">[About Message Queuing](http://msdn.microsoft.com/en-us/library/windows/desktop/ms706032%28v=vs.85%29.aspx)</span></span>
    
  
-  <span data-ttu-id="159ed-136">
  [Message Queuing-Referenz (engl.)](http://msdn.microsoft.com/en-us/library/windows/desktop/ms700112%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="159ed-136">[Message Queuing Reference](http://msdn.microsoft.com/en-us/library/windows/desktop/ms700112%28v=vs.85%29.aspx)</span></span>
    
  
-  <span data-ttu-id="159ed-137">
  [Message Queuing-Fehler und Codes für Statusangaben](http://msdn.microsoft.com/en-us/library/windows/desktop/ms700106%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="159ed-137">[Message Queuing Error and Information Codes](http://msdn.microsoft.com/en-us/library/windows/desktop/ms700106%28v=vs.85%29.aspx)</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="159ed-138">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="159ed-138">See also</span></span>
<span data-ttu-id="159ed-139"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="159ed-139"><a name="bk_addresources"> </a></span></span>


-  <span data-ttu-id="159ed-140">
  [Message Queuing (MSMQ)](http://msdn.microsoft.com/en-us/library/windows/desktop/ms711472%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="159ed-140">[Message Queuing (MSMQ)](http://msdn.microsoft.com/en-us/library/windows/desktop/ms711472%28v=vs.85%29.aspx)</span></span>
    
  

  
    
    

