---
title: SharePoint-Workflow-Grundlagen
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1e622296-f78b-4e3a-a1e7-8effa24111a8
ms.openlocfilehash: bc595ebee4d80def6994cbb5b38b406c71cd331a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-workflow-fundamentals"></a><span data-ttu-id="31a14-102">SharePoint-Workflow-Grundlagen</span><span class="sxs-lookup"><span data-stu-id="31a14-102">SharePoint workflow fundamentals</span></span>
<span data-ttu-id="31a14-103">Bietet eine allgemeine Übersicht über die Workflowinfrastruktur in SharePoint, einschließlich einer Sicht der Plattformarchitektur und der Workflow-Interopbrücke</span><span class="sxs-lookup"><span data-stu-id="31a14-103">Provides a high-level overview of the workflow infrastructure in SharePoint, including a view of the platform architecture and the workflow interop bridge.</span></span>
## <a name="overview-of-workflows-in-sharepoint"></a><span data-ttu-id="31a14-104">Übersicht über Workflows in SharePoint</span><span class="sxs-lookup"><span data-stu-id="31a14-104">Overview of workflows in SharePoint</span></span>
<span data-ttu-id="31a14-105"><a name="bkm_overview"> </a></span><span class="sxs-lookup"><span data-stu-id="31a14-105"><a name="bkm_overview"> </a></span></span>

<span data-ttu-id="31a14-p101">SharePoint-Workflows werden von Windows Workflow Foundation 4 unterstützt, das in Vergleich zu früheren Versionen erheblich überarbeitet wurde. Windows Workflow Foundation (WF) basiert wiederum auf der von  [Windows Communication Foundation (WCF)](http://msdn.microsoft.com/en-us/library/vstudio/ms735119%28v=vs.90%29.aspx) bereitgestellten Messaging-Funktion.</span><span class="sxs-lookup"><span data-stu-id="31a14-p101">SharePoint workflows are powered by Windows Workflow Foundation 4, which was substantially redesigned from earlier versions. Windows Workflow Foundation (WF), in turn, is built on the messaging functionality that is provided by  [Windows Communication Foundation (WCF)](http://msdn.microsoft.com/en-us/library/vstudio/ms735119%28v=vs.90%29.aspx).</span></span>
  
    
    
<span data-ttu-id="31a14-p102">Konzeptionell gesehen modellieren Workflows strukturierte Geschäftsprozesse. Daher sind Windows Workflow Foundation 4-Workflows eine strukturierte Sammlung von "Workflowaktivitäten", die jeweils eine funktionale Komponente eines Geschäftsprozesses darstellen.</span><span class="sxs-lookup"><span data-stu-id="31a14-p102">Conceptually, workflows model structured business processes. Therefore, Windows Workflow Foundation 4 workflows are a structured collection of workflow "activities," each of which represents a functional component of a business process.</span></span>
  
    
    
<span data-ttu-id="31a14-p103">Die Workflowplattform in SharePoint verwendet das Windows Workflow Foundation 4-Aktivitätsmodell, um einen SharePoint-basierten Geschäftsprozess darzustellen. Zusätzlich führt SharePoint ein allgemeineres Stage-Gate-Modell ein, auf dem Workflows erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="31a14-p103">The workflow platform in SharePoint uses the Windows Workflow Foundation 4 activity model to represent a SharePoint-based business process. Additionally, SharePoint introduces a higher-level stage-gate model on which to create workflows.</span></span>
  
    
    
<span data-ttu-id="31a14-p104">Es ist wichtig, die Beziehung zwischen Workflowaktivitäten undSharePoint-Aktionen zu beachten. Workflowaktivitäten stellen die zugrunde liegenden verwalteten Objekte dar, deren Methoden Workflowverhalten steuern. Workflowaktionen stellen andererseits Wrapper dar, welche die zugrunde liegenden Aktivitäten kapseln und sie in benutzerfreundlicher Form in SharePoint Designer präsentieren. Workflowautoren interagieren mit den Workflowaktionen, wohingegen das Workflow-Ausführungsmodul die entsprechenden Aktivitäten verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="31a14-p104">It is important to note the relationship between workflow activities and SharePointactions. Workflow activities represent the underlying managed objects whose methods drive workflow behaviors. Workflow actions, on the other hand, are wrappers that encapsulate the underlying activities and present them in a user-friendly form in SharePoint Designer. Workflow authors interact with the workflow actions, whereas the workflow execution engine acts on the corresponding activities.</span></span>
  
    
    
<span data-ttu-id="31a14-116">Die Aktivitäten, die Implementierungen von Aktivitätsklassen darstellen, werden mithilfe von XAML deklarativ implementiert.</span><span class="sxs-lookup"><span data-stu-id="31a14-116">The activities, which are implementations of activity classes, are implemented declaratively by using XAML.</span></span>
  
    
    
<span data-ttu-id="31a14-p105">Workflowaktivitäten werden mithilfe locker gekoppelter Webdienste aufgerufen, die zum Kommunizieren mit SharePoint Messaging-APIs verwenden. Diese APIs basieren auf der von  [Windows Communication Foundation (WCF)](http://msdn.microsoft.com/en-us/library/vstudio/ms735119%28v=vs.90%29.aspx) bereitgestellten Messaging-Funktion.</span><span class="sxs-lookup"><span data-stu-id="31a14-p105">Workflow activities are invoked using loosely coupled web services that use messaging APIs to communicate with SharePoint. These APIs are built on the messaging functionality that is provided by  [Windows Communication Foundation (WCF)](http://msdn.microsoft.com/en-us/library/vstudio/ms735119%28v=vs.90%29.aspx).</span></span>
  
    
    
<span data-ttu-id="31a14-p106">Das Messaging-Framework ist sehr flexibel und unterstützt quasi jedes Messaging-Muster, das Sie benötigen. Beachten Sie, dass Windows Workflow Foundation und WCF in einer SharePoint-Farm in Workflow-Manager-Client 1.0 gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="31a14-p106">The messaging framework is very flexible and supports virtually any messaging pattern that you need. Note that on a SharePoint farm, Windows Workflow Foundation and WCF are hosted in Workflow Manager Client 1.0.</span></span>
  
    
    
<span data-ttu-id="31a14-121">Workflow-Manager-Client 1.0, SharePoint und SharePoint Designer 2013 stellen jeweils wesentliche Teile der neuen Infrastruktur bereit:</span><span class="sxs-lookup"><span data-stu-id="31a14-121">Workflow Manager Client 1.0, SharePoint, and SharePoint Designer 2013 each provide significant parts of the new infrastructure:</span></span>
  
    
    

- <span data-ttu-id="31a14-p107">**Workflow-Manager-Client 1.0** stellt das Management von Workflowdefinitionen bereit. Er hostet außerdem die Ausführungsprozesse für Workflowinstanzen.</span><span class="sxs-lookup"><span data-stu-id="31a14-p107">**Workflow Manager Client 1.0** provides the management of workflow definitions. It also hosts the execution processes for workflow instances.</span></span>
    
  
- <span data-ttu-id="31a14-p108">**SharePoint** stellt das Framework für SharePoint-Workflows bereit, die SharePoint-basierte Geschäftsprozesse modellieren, welche SharePoint-Dokumente, -Listen, -Benutzer und -Aufgaben umfassen. Darüber hinaus werden SharePoint-Workflows, -Zuordnungen, -Aktivitäten und andere Workflowmetadaten in SharePoint gespeichert und verwaltet.</span><span class="sxs-lookup"><span data-stu-id="31a14-p108">**SharePoint** provides the framework for SharePoint workflows, which model SharePoint-based business processes that involve SharePoint documents, lists, users, and tasks. Additionally, SharePoint workflows, associations, activities, and other workflow metadata are stored and managed in SharePoint.</span></span>
    
  
- <span data-ttu-id="31a14-p109">**SharePoint Designer 2013** stellt, wie in früheren Versionen, das zentrale Geschäftsbenutzertool zur Erstellung von Workflowdefinitionen und deren Veröffentlichung dar. Es kann auch zum Verpacken einer Workflowdefinition mit oder ohne zugeordnete SharePoint-Komponenten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="31a14-p109">**SharePoint Designer 2013** is the primary business-user tool for creating workflow definitions and publishing them, as it was in previous versions. It can also be used to package a workflow definition with or without associated SharePoint components.</span></span>
    
  

## <a name="platform-architecture"></a><span data-ttu-id="31a14-128">Plattformarchitektur</span><span class="sxs-lookup"><span data-stu-id="31a14-128">Platform architecture</span></span>
<span data-ttu-id="31a14-129"><a name="bkm_Architecture"> </a></span><span class="sxs-lookup"><span data-stu-id="31a14-129"><a name="bkm_Architecture"> </a></span></span>

<span data-ttu-id="31a14-p110">Abbildung 1 zeigt eine allgemeine Ansicht des SharePoint-Workflow-Frameworks. Beachten Sie zunächst, wie die neue Workflowinfrastruktur Workflow-Manager-Client 1.0 als den neuen Workflowausführungshost einführt. Während die Workflowausführung in früheren Versionen in SharePoint selbst gehostet wurde, wurde dies in SharePoint geändert. Workflow-Manager-Client 1.0 befindet sich außerhalb von SharePoint und kommuniziert mithilfe allgemeiner Protokolle über den Microsoft Azure-Servicebus, vermittelt durch OAuth. Ansonsten enthält SharePoint die erwarteten Features: Inhaltselemente, Ereignisse, Apps usw. Beachten Sie allerdings, dass es für Abwärtskompatibilität auch eine Implementierung des SharePoint 2010-Workflow-Hosts (d. h. das Windows Workflow Foundation 3-Modul) gibt. Weitere Informationen dazu finden Sie unter  [Verwenden von Workflow-Interop für SharePoint](use-workflow-interop-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="31a14-p110">Figure 1 depicts a high-level view of the SharePoint workflow framework. Notice, first, how the new workflow infrastructure introduces Workflow Manager Client 1.0 as the new workflow execution host. Whereas in previous versions workflow execution was hosted in SharePoint itself, this has changed in SharePoint. Workflow Manager Client 1.0 is external to SharePoint and communicates using common protocols over the Microsoft Azure service bus, mediated by OAuth. Otherwise, SharePoint includes the feature that you would expect to see: content items, events, apps, and so on. But notice that there is also an implementation of the SharePoint 2010 workflow host (that is, the Windows Workflow Foundation 3 engine) for backward compatibility. You can read more about this in  [Use workflow interop for SharePoint](use-workflow-interop-for-sharepoint.md).</span></span>
  
    
    

<span data-ttu-id="31a14-137">**Abbildung 1. Allgemeine Architektur der Workflowinfrastruktur**</span><span class="sxs-lookup"><span data-stu-id="31a14-137">**Figure 1. High-level architecture of the workflow infrastructure**</span></span>

  
    
    

  
    
    
![Allgemeine Workflowarchitektur](../images/wfArchitecture1.png)
  
    
    
<span data-ttu-id="31a14-p111">Workflow-Manager-Client 1.0 wird in SharePoint in der Form des Workflow-Manager-Client 1.0-Dienstanwendungsproxys dargestellt. Diese Komponente erlaubt SharePoint, mit dem Workflow-Manager-Client 1.0-Server zu kommunizieren und zu interagieren. Server-zu-Server-Authentifizierung wird mithilfe von OAuth bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="31a14-p111">Workflow Manager Client 1.0 is represented in SharePoint in the form of the Workflow Manager Client 1.0 Service Application Proxy. This component allows SharePoint to communicate and interact with the Workflow Manager Client 1.0 server. Server-to-server authentication is provided using OAuth.</span></span>
  
    
    
<span data-ttu-id="31a14-p112">SharePoint-Ereignisse, die ein Workflow überwacht, wie **itemCreated**, **itemUpdated** usw., werden mithilfe des Microsoft Azure-Servicebus an Workflow-Manager-Client 1.0 weitergeleitet. Für den Weg zurück verwendet die Plattform die SharePoint-REST-API (Representational State Transfer), um einen Rückruf an SharePoint durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="31a14-p112">SharePoint events for which a workflow is listening, like **itemCreated**, **itemUpdated**, and so on, are routed to Workflow Manager Client 1.0 using the Microsoft Azure service bus. For the return trip, the platform uses the SharePoint Representational State Transfer (REST) API to call back into SharePoint.</span></span>
  
    
    
<span data-ttu-id="31a14-p113">Außerdem wurde das SharePoint-Workflowobjektmodell, das zusammenfassend als der Workflow-Dienstemanager bezeichnet wird, ergänzt, sodass Sie Ihre Workflows und deren Ausführung verwalten und steuern können. Die Hauptinteraktionszonen für den Dienstemanager sind Bereitstellung, Messaging, Instanzensteuerung und (für Abwärtskompatibilität) Interoperabilität mit SharePoint 2010-Workflows.</span><span class="sxs-lookup"><span data-stu-id="31a14-p113">There are also additions to the SharePoint workflow object model, called collectively the Workflow Services Manager, which allow you to manage and control your workflows and their execution. The primary zones of interaction for the services manager are deployment, messaging, instance control, and (for backward compatibility) interoperability with SharePoint 2010 workflows.</span></span>
  
    
    
<span data-ttu-id="31a14-p114">Schließlich gibt es die Workflowerstellungskomponente. SharePoint Designer kann nun sowohl SharePoint 2010- als auch SharePoint-Workflows erstellen und bereitstellen. Visual Studio 2012 bietet nicht nur eine Designeroberfläche zur Erstellung deklarativer Workflows, sonder kann auch SharePoint-Add-Ins und Lösungen erstellen, die Workflow-Manager-Client 1.0-Funktionen vollständig integrieren.</span><span class="sxs-lookup"><span data-stu-id="31a14-p114">Finally, there is the workflow authoring component. SharePoint Designer can now create and deploy both SharePoint 2010 and SharePoint workflows. Visual Studio 2012 not only provides a designer surface for creating declarative workflows, but it can also create SharePoint Add-ins and solutions that fully integrate Workflow Manager Client 1.0 functionality.</span></span>
  
    
    

## <a name="workflow-subscriptions-and-associations"></a><span data-ttu-id="31a14-149">Workflowabonnements und -zuordnungen</span><span class="sxs-lookup"><span data-stu-id="31a14-149">Workflow subscriptions and associations</span></span>
<span data-ttu-id="31a14-150"><a name="bkm_Subscriptions"> </a></span><span class="sxs-lookup"><span data-stu-id="31a14-150"><a name="bkm_Subscriptions"> </a></span></span>

<span data-ttu-id="31a14-p115">Da die wichtigste Änderung an SharePoint-Workflows die Verschiebung der Workflowverarbeitung zu externen Workflow-Hosts wie Microsoft Azure darstellt, war es wichtig, dass SharePoint-Nachrichten und -Ereignisse eine Verbindung zur Workflowinfrastruktur in Microsoft Azure aufweisen. Zusätzlich war es erforderlich, dass Microsoft Azure die Infrastruktur mit Kundendaten verbindet. Workflowzuordnungen (die auf dem WF-Konzept von Abonnements basieren) stellen die SharePoint-Infrastrukturkomponenten dar, die diese Anforderungen unterstützen.</span><span class="sxs-lookup"><span data-stu-id="31a14-p115">Because the most significant change to SharePoint workflows is the moving of workflow processing onto external workflow hosts like Microsoft Azure, it was essential for SharePoint messages and events to connect to the workflow infrastructure in Microsoft Azure. In addition, it was necessary for Microsoft Azure to connect the infrastructure to customer data. Workflow associations (which are built on the WF concept of subscriptions) are the SharePoint infrastructure pieces that support these requirements.</span></span>
  
    
    

### <a name="microsoft-azure-publicationsubscribe-service"></a><span data-ttu-id="31a14-154">Microsoft Azure-Veröffentlichungs-/Abonnementdienst</span><span class="sxs-lookup"><span data-stu-id="31a14-154">Microsoft Azure publication/subscribe service</span></span>

<span data-ttu-id="31a14-p116">Bevor wir über Workflowverknüpfungen und -abonnements sprechen können, müssen wir uns den Microsoft Azure-Veröffentlichungs-/Abonnementdienst näher ansehen, der manchmal alspub/sub oder einfachPubSub bezeichnet wird. PubSub ist ein asynchrones Messaging-Framework. Nachrichtenabsender (Herausgeber) senden Nachrichten nicht direkt an Nachrichtenempfänger (Abonnenten). Stattdessen werden Nachrichten von Herausgebern als Klassen gerendert, die den Nachrichtenabonnenten nicht kennen. Abonnenten nutzen dann veröffentlichte Nachrichten, indem sie auf Basis der von ihnen erstellten Abonnements für sie relevante Nachrichten, unabhängig vom Herausgeber, identifizieren.</span><span class="sxs-lookup"><span data-stu-id="31a14-p116">Before you can discuss workflow associations and subscriptions, you must look at the Microsoft Azure publication/subscribe service, which is sometimes referred to as pub/sub, or simply PubSub. PubSub is an asynchronous messaging framework. Message senders (publishers) do not send messages directly to message receivers (subscribers). Instead, messages are rendered by publishers as classes that have no knowledge of the message subscribers. Subscribers, then, consume published messages by identifying messages of interest, regardless of the publisher, based on subscriptions that they have created.</span></span>
  
    
    
<span data-ttu-id="31a14-p117">Diese Entkoppelung von Nachrichtenerstellung von der Nachrichtenverwendung ermöglicht Skalierbarkeit und Flexibilität. Sie erlaubt Multicast-Messaging seitens des Herausgebers und promiske Nutzung seitens des Abonnenten.</span><span class="sxs-lookup"><span data-stu-id="31a14-p117">This decoupling of message creation from message consumption allows for scalability and flexibility. It enables multicast messaging on the publisher side, and for promiscuous message consumption on the subscriber side.</span></span>
  
> [!NOTE]
> <span data-ttu-id="31a14-162">Das Feature PubSub ist ein Bestandteil von Microsoft Azure Service Bus, das Verbindungsoptionen für WCF und andere Dienstendpunkte bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="31a14-162">Note: The PubSub feature is a part of the Microsoft Azure Service Bus, which provides connectivity options for WCF and other service endpoints.</span></span> <span data-ttu-id="31a14-163">Dazu gehören die REST-Endpunkte, die hinter Netzwerkadressübersetzungsgrenzen (NAT) angeordnet und/oder an sich häufig ändernde, dynamisch zugewiesene IP-Adressen gebunden werden.</span><span class="sxs-lookup"><span data-stu-id="31a14-163">These include REST endpoints, which can be located behind network address translation (NAT) boundaries, or bound to frequently changing, dynamically assigned IP addresses, or both.</span></span> <span data-ttu-id="31a14-164">Weitere Informationen zu Azure Service Bus finden Sie unter [Service Bus](http://msdn.microsoft.com/de-DE/library/ee732537.aspx).</span><span class="sxs-lookup"><span data-stu-id="31a14-164">For more information about the Azure Service Bus, see  [Service Bus](http://msdn.microsoft.com/de-DE/library/ee732537.aspx).</span></span> 
  
    
    


### <a name="workflow-associations-and-association-scope"></a><span data-ttu-id="31a14-165">Workflowzuordnungen und -zuordnungsumfang</span><span class="sxs-lookup"><span data-stu-id="31a14-165">Workflow associations and association scope</span></span>

<span data-ttu-id="31a14-p119">Workflowzuordnungen binden Workflowdefinitionen an einen bestimmten SharePoint-Bereich mit bestimmten Standardwerten. Diese Zuordnungen selbst stellen einen Satz von Abonnementregeln dar, die im Azure-Veröffentlichungs-/Abonnementdienst gespeichert werden und die eingehende Nachrichten verarbeiten, um sicherzustellen, dass sie von den entsprechenden (d. h. abonnierten) Workflowinstanzen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="31a14-p119">Workflow associations bind workflow definitions to specific SharePoint scope, with specific default values. The associations themselves represent a set of subscription rules that are stored in the Azure publication/subscription service that process incoming messages to ensure that they are consumed by appropriate (that is, subscribed) workflow instances.</span></span>
  
    
    
<span data-ttu-id="31a14-168">Die Messaging-Infrastruktur unterstützt Workflows standardmäßig in den folgenden Bereichen:</span><span class="sxs-lookup"><span data-stu-id="31a14-168">By default, the messaging infrastructure supports workflows at the following scopes:</span></span>
  
    
    

-  <span data-ttu-id="31a14-169">[SPList](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPList.aspx) (für Listenworkflows)</span><span class="sxs-lookup"><span data-stu-id="31a14-169">[SPList](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPList.aspx) (for list workflows)</span></span>
    
  
-  <span data-ttu-id="31a14-170">[SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) (für Websiteworkflows)</span><span class="sxs-lookup"><span data-stu-id="31a14-170">[SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) (for site workflows)</span></span>
    
  
<span data-ttu-id="31a14-p120">Im Gegensatz zu früheren Versionen unterstützt SharePoint keine Workflows, die einem Inhaltstyp ( [SPContentType](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPContentType.aspx) ) zugeordnet sind. Die Messaging-Infrastruktur ist allerdings erweiterbar, sodass sie jeden beliebigen Bereich unterstützen kann. Als Entwickler können Sie die [EventSourceId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscription.EventSourceId.aspx) -Eigenschaft auf einer bestimmten [WorkflowSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscription.aspx) -Instanz auf eine beliebige **guid** festlegen. Sie können diesen **EventSourceId**-Wert dann verwenden, um **PublishEvent(Guid, String, IDictionary<String, Object>)** aufzurufen, wodurch eine neue Workflowinstanz des angegebenen **WorkflowSubscription** ausgelöst wird.</span><span class="sxs-lookup"><span data-stu-id="31a14-p120">Unlike previous versions, SharePoint does not support workflows that are scoped to a content type ( [SPContentType](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPContentType.aspx) ). However, the messaging infrastructure is extensible, so it can support any arbitrary scope. As a developer, you can set the [EventSourceId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscription.EventSourceId.aspx) property on a given [WorkflowSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscription.aspx) instance to any **guid**. You can then use that **EventSourceId** value to call **PublishEvent(Guid, String, IDictionary<String, Object>)**, which triggers a new workflow instance of the specified **WorkflowSubscription**.</span></span>
  
    
    

### <a name="workflow-service-in-microsoft-azure"></a><span data-ttu-id="31a14-175">Workflowdienst in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="31a14-175">Workflow service in Microsoft Azure</span></span>

<span data-ttu-id="31a14-p121">Zuordnungen für SharePoint-Workflows werden in Microsoft Azure durch deren Workflowdienst dargestellt. Wenn eine Anwendung eine Workflowzuordnung und deren Daten abrufen muss, muss sie zuerst alle Workflowdienste abfragen, die in einem bestimmten Bereich verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="31a14-p121">Associations for SharePoint workflows are represented by their workflow service within Microsoft Azure. When an application has to acquire a workflow association and its data, it must first query for all of the workflow services that are available at a given scope.</span></span>
  
    
    
<span data-ttu-id="31a14-p122">Auf ähnliche Weise bringen Workflowinstanzen zu ihrem entsprechenden Workflowdienst einen Verweis zurück. Anhand dieses Verweises wird deren korrekte Zuordnung ermittelt.</span><span class="sxs-lookup"><span data-stu-id="31a14-p122">Similarly, workflow instances carry a pointer back to their respective workflow service. This is the means by which its correct association is determined.</span></span>
  
    
    

### <a name="starting-workflows"></a><span data-ttu-id="31a14-180">Starten von Workflows</span><span class="sxs-lookup"><span data-stu-id="31a14-180">Starting workflows</span></span>

<span data-ttu-id="31a14-181">Workflows können manuell oder automatisch gestartet werden.</span><span class="sxs-lookup"><span data-stu-id="31a14-181">Workflows can be started either manually or automatically.</span></span>
  
    
    
 <span data-ttu-id="31a14-182">**Manuelle Workflows**</span><span class="sxs-lookup"><span data-stu-id="31a14-182">**Manual workflows**</span></span>
  
    
    
<span data-ttu-id="31a14-p123">Manuelle Workflows werden gestartet, wenn der PubSub-Dienst eine **StartWorkflow** -Nachricht erhält. Die Nachricht enthält die folgenden deskriptiven Informationen:</span><span class="sxs-lookup"><span data-stu-id="31a14-p123">Manual workflows are started when the PubSub service receives a **StartWorkflow** message. The message contains the following descriptive information:</span></span>
  
    
    

- <span data-ttu-id="31a14-185">Den Bezeichner für die Zuordnung (d. h. die **WorkflowSubscription**-Instanz).</span><span class="sxs-lookup"><span data-stu-id="31a14-185">The association identifier (that is, the **WorkflowSubscription** instance).</span></span>
    
  
- <span data-ttu-id="31a14-p124">Die ID des Ursprungselementkontexts. Diese wird mit dem  _ItemId_-Parameter und der **EventSource**-Eigenschaft beim **PublishEvent**-Methodenaufruf übergeben.</span><span class="sxs-lookup"><span data-stu-id="31a14-p124">The ID of the originating item context. This is passed in with the  _ItemId_ parameter and the **EventSource** property on the **PublishEvent** method call.</span></span>
    
  
- <span data-ttu-id="31a14-188">Den Ereignistyp für einen manuellen Start ( **WorkflowStart**).</span><span class="sxs-lookup"><span data-stu-id="31a14-188">The event type for a manual start ( **WorkflowStart**).</span></span>
    
  
- <span data-ttu-id="31a14-p125">Ggf. zusätzliche Workflowinitiierungsparameter, entweder aus dem Abonnement oder dem **Init**-Formular. Für das Abonnement wäre dies die **CorrelationId**, und für das **Init**-Formular wäre dies die **WFInstanceId**.</span><span class="sxs-lookup"><span data-stu-id="31a14-p125">Additional workflow initiation parameters, either from the subscription or from the **Init** form, as appropriate. This would be **CorrelationId** for the subscription and **WFInstanceId** for the **Init** form.</span></span>
    
  
 <span data-ttu-id="31a14-191">**Automatisch gestartete Workflows**</span><span class="sxs-lookup"><span data-stu-id="31a14-191">**Auto-start workflows**</span></span>
  
    
    
<span data-ttu-id="31a14-p126">Automatisch gestartete Workflows werden mithilfe einer **Add**-Nachricht an den PubSub-Dienst initiiert. Die Nachricht enthält die folgenden deskriptiven Informationen:</span><span class="sxs-lookup"><span data-stu-id="31a14-p126">Auto-start workflows are initiated by using an **Add** message to the PubSub service. The message contains the following descriptive information:</span></span>
  
    
    

- <span data-ttu-id="31a14-194">Die ID des Ursprungselementkontexts.</span><span class="sxs-lookup"><span data-stu-id="31a14-194">The ID of the originating item context.</span></span>
    
  
- <span data-ttu-id="31a14-195">Das Ereignis selbst ist ein normales SharePoint **Add**-Ereignis.</span><span class="sxs-lookup"><span data-stu-id="31a14-195">The event itself is a normal SharePoint **Add** event.</span></span>
    
  
- <span data-ttu-id="31a14-196">Die Parameter für die Workflowinitiierung.</span><span class="sxs-lookup"><span data-stu-id="31a14-196">The workflow initiation parameters.</span></span>
    
> [!NOTE]
> <span data-ttu-id="31a14-197">Wenn ein Workflow für ein wiederholbares Ereignis (z. B. das **OnItemChanged**-Ereignis) automatisch startet, kann es erst dann einen anderen Workflow einer bestimmten Zuordnung starten, wenn die vorhandene ausgeführte Instanz des Workflows der Zuordnung abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="31a14-197">If a workflow automatically starts on a repeatable event (for example, the **OnItemChanged** event), it cannot start another workflow of a given association until the existing running instance of the association’s workflow has completed running.</span></span>
  
    
    


### <a name="workflow-subscriptions"></a><span data-ttu-id="31a14-198">Workflow-Abonnements</span><span class="sxs-lookup"><span data-stu-id="31a14-198">Workflow subscriptions</span></span>

<span data-ttu-id="31a14-p127">Die natürliche Ergänzung zu Zuordnungen sind Abonnements, die dem Workflow erlauben, mit Zuordnungen zu interagieren. Der Workflow muss mithilfe von **create**- und **delete**-Methoden Abonnements auf dem Azure-Servicebus erstellen.</span><span class="sxs-lookup"><span data-stu-id="31a14-p127">The natural complement to associations are subscriptions, which allow the workflow to interact with associations. The workflow must create subscriptions on the Azure Service Bus using **create** methods and **delete** methods.</span></span>
  
    
    
<span data-ttu-id="31a14-201">Die Signaturen der Methoden, die das Abonnement erstellen und den Workflow instanziieren, geben die Parameter optional und zwingend an.</span><span class="sxs-lookup"><span data-stu-id="31a14-201">The signatures of the methods that create the subscription and instantiate the workflow specify the parameters???both optional and required.</span></span> <span data-ttu-id="31a14-202">Die Liste der Parameter wird vom Workflowautor bestimmt, sodass die Parameter von Workflow zu Workflow unterschiedlich sein können.</span><span class="sxs-lookup"><span data-stu-id="31a14-202">The list of parameters is determined by the workflow author, so they may differ from one workflow definition to another.</span></span> <span data-ttu-id="31a14-203">Die Liste der Abonnementparameter wird als Metadaten der Workflowdefinitionen angegeben.</span><span class="sxs-lookup"><span data-stu-id="31a14-203">The list of subscription parameters is specified as metadata of the workflow definitions.</span></span> <span data-ttu-id="31a14-204">Die Abonnementparameter werden bereitgestellt, nachdem das Abonnement erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="31a14-204">The subscription parameters are provided when the subscription is created.</span></span> <span data-ttu-id="31a14-205">Die Liste der Initialisierungsparameter wird in XAML als Teil der Workflowdefinition angegeben.</span><span class="sxs-lookup"><span data-stu-id="31a14-205">The list of initialization parameters is specified in XAML as part of the workflow definition.</span></span> <span data-ttu-id="31a14-206">Die Initialisierungsparameter werden bereitgestellt, wenn der Workflow instanziiert wird.</span><span class="sxs-lookup"><span data-stu-id="31a14-206">The initialization parameters are provided when the workflow is instantiated.</span></span>
  
    
    
<span data-ttu-id="31a14-207">Abonnements sind an ein bestimmtes SharePoint-Objekt gebunden, entweder an eine **SPList**-Instanz oder eine **SPWeb**-Instanz.</span><span class="sxs-lookup"><span data-stu-id="31a14-207">Subscriptions are bound to a specific SharePoint object???either an **SPList** instance or an **SPWeb** instance.</span></span> <span data-ttu-id="31a14-208">Der Abonnement-Objekttyp wird als Wert eines erforderlichen Parameters übergeben, wenn das Abonnement erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="31a14-208">The subscription object type is passed in as a value of a required parameter when the subscription is created.</span></span> <span data-ttu-id="31a14-209">Der Objekttyp definiert den Abonnementbereich, damit das Abonnement nur auf Ereignisse reagieren kann, die für das abonnierte Objekt ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="31a14-209">The object type defines the subscription scope so that a subscription can only respond to events that occur on the object to which they are subscribed.</span></span>
  
    
    

## <a name="sharepoint-workflow-interop"></a><span data-ttu-id="31a14-210">SharePoint-Workflowinteroperabilität</span><span class="sxs-lookup"><span data-stu-id="31a14-210">SharePoint workflow interop</span></span>
<span data-ttu-id="31a14-211"><a name="bkm_InteropBridge"> </a></span><span class="sxs-lookup"><span data-stu-id="31a14-211"><a name="bkm_InteropBridge"> </a></span></span>

<span data-ttu-id="31a14-p130">SharePoint-Workflowinteroperabilität ermöglicht den Aufruf von SharePoint 2010-Workflows (die auf Windows Workflow Foundation 3 basieren) über SharePoint-Workflows, die auf Windows Workflow Foundation 4 basieren. Dadurch können Sie 2010-Workflows innerhalb von 2013-Workflows ausführen.</span><span class="sxs-lookup"><span data-stu-id="31a14-p130">SharePoint workflow interop enables SharePoint 2010 workflows (which are built on Windows Workflow Foundation 3) to be called from SharePoint workflows, which are based on Windows Workflow Foundation 4. This allows you to execute 2010 workflows from within 2013 workflows.</span></span>
  
    
    
<span data-ttu-id="31a14-p131">Dies ist wichtig, weil Sie möglicherweise SharePoint 2010 haben, das Sie in Verbindung mit Ihren SharePoint-Workflows verwenden möchten. Außerdem möchten Sie möglicherweise Aktivitäten oder Features aus SharePoint 2010 verwenden, die noch nicht in SharePoint implementiert sind.</span><span class="sxs-lookup"><span data-stu-id="31a14-p131">This is important because you may have SharePoint 2010 that you may use to reuse in conjunction with your SharePoint workflows. Additionally, you may wish to use activities or features from SharePoint 2010, which are not yet implemented in SharePoint</span></span>
  
    
    
<span data-ttu-id="31a14-216">Eine umfassende Erläuterung der SharePoint-Workflowinteroperabilität finden Sie unter  [Verwenden von Workflow-Interop für SharePoint](use-workflow-interop-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="31a14-216">For a full discussion of SharePoint workflow interop, see  [Use workflow interop for SharePoint](use-workflow-interop-for-sharepoint.md).</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="31a14-217">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="31a14-217">See also</span></span>
<span data-ttu-id="31a14-218"><a name="bk_additional"> </a></span><span class="sxs-lookup"><span data-stu-id="31a14-218"><a name="bk_additional"> </a></span></span>


-  [<span data-ttu-id="31a14-219">Erste Schritte mit Workflows in SharePoint</span><span class="sxs-lookup"><span data-stu-id="31a14-219">Get started with workflows in SharePoint</span></span>](get-started-with-workflows-in-sharepoint.md)
    
  
-  [<span data-ttu-id="31a14-220">Workflowaktions- und -aktivitätenreferenz für SharePoint</span><span class="sxs-lookup"><span data-stu-id="31a14-220">Workflow actions and activities reference for SharePoint</span></span>](workflow-actions-and-activities-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="31a14-221">Entwickeln von SharePoint-Workflows mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="31a14-221">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio.md)
    
  
-  [<span data-ttu-id="31a14-222">Workflowentwicklung in SharePoint Designer und Visio</span><span class="sxs-lookup"><span data-stu-id="31a14-222">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [<span data-ttu-id="31a14-223">Workflows in SharePoint</span><span class="sxs-lookup"><span data-stu-id="31a14-223">Workflows in SharePoint</span></span>](workflows-in-sharepoint.md)
    
  
-  [<span data-ttu-id="31a14-224">Verwenden von Workflow-Interop für SharePoint</span><span class="sxs-lookup"><span data-stu-id="31a14-224">Use workflow interop for SharePoint</span></span>](use-workflow-interop-for-sharepoint.md)
    
  

