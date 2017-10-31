---
title: "Erstellen eines Add-In-Ereignisempfängers in SharePoint-Add-Ins"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: cd2e90745acbc17353db12c350127dc793126337
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="create-an-add-in-event-receiver-in-sharepoint-add-ins"></a><span data-ttu-id="55e17-102">Erstellen eines Add-In-Ereignisempfängers in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="55e17-102">Create an add-in event receiver in SharePoint Add-ins</span></span>
<span data-ttu-id="55e17-103">Erstellen von Handlern für SharePoint-Add-In-Installations- und Deinstallationsereignisse in SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="55e17-103">Create handlers for the SharePoint Add-in install and uninstall events in SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="55e17-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="55e17-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="prerequisites"></a><span data-ttu-id="55e17-107">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="55e17-107">Prerequisites</span></span>
<span data-ttu-id="55e17-108"><a name="SP15appevent_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="55e17-108"><a name="SP15appevent_prereq"> </a></span></span>

<span data-ttu-id="55e17-p102">In diesem Artikel wird vorausgesetzt, dass Sie die Grundlagen vom Anbieter gehosteter SharePoint-Add-Ins verstehen und bereits Apps entwickelt haben, die wenigstens geringfügig über die Komplexität von "Hello World" hinausgehen. Ferner sollten Sie mit dem  [Behandeln von Ereignissen in SharePoint-Add-Ins](handle-events-in-sharepoint-add-ins.md) vertraut sein.</span><span class="sxs-lookup"><span data-stu-id="55e17-p102">This article presupposes that you have an understanding of provider-hosted SharePoint Add-ins, and that you have developed a few that go a least a little beyond the "Hello World" level. Also, you should be familiar with  [Handle events in SharePoint Add-ins](handle-events-in-sharepoint-add-ins.md).</span></span> 
 

 

## <a name="get-more-code-samples"></a><span data-ttu-id="55e17-111">Abrufen weiterer Codebeispiele</span><span class="sxs-lookup"><span data-stu-id="55e17-111">Get more code samples</span></span>
<span data-ttu-id="55e17-112"><a name="SP15appevent_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="55e17-112"><a name="SP15appevent_prereq"> </a></span></span>

<span data-ttu-id="55e17-p103">Wenn Sie das fortlaufende Beispiel in diesem Artikel durcharbeiten, verfügen Sie über ein fertiges Codebeispiel. Im Folgenden finden Sie weitere Beispiele. Sie folgen nicht alle der hier beschriebenen Architektur. Es kann mehr als eine gute Möglichkeit geben, einen Add-In-Ereignisempfänger zu entwerfen. Bedenken Sie auch, dass Microsoft möglicherweise mit der Zeit weitere Anleitungen bereitstellen wird.</span><span class="sxs-lookup"><span data-stu-id="55e17-p103">If you work through the continuing example in this article, you will have a finished code sample. The following are some other samples. They don't all follow the architecture described in this article. There can be more than one good way to architect an add-in event receiver, and keep in mind also that Microsoft's guidance can evolve over time.</span></span> 
 

 

-  <span data-ttu-id="55e17-117">[OfficeDev/PnP/Samples/Core.AppEvents.HandlerDelegation](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.AppEvents.HandlerDelegation) stimmt weitgehend mit dem fortlaufenden Beispiel in diesem Artikel überein.</span><span class="sxs-lookup"><span data-stu-id="55e17-117">[OfficeDev/PnP/Samples/Core.AppEvents.HandlerDelegation](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.AppEvents.HandlerDelegation) is a close match to the continuing example in this article.</span></span>
    
 
-  <span data-ttu-id="55e17-118">[OfficeDev/PnP/Samples/Core.AppEvents](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.AppEvents) zeigt, wie Sie dieselbe Aufgabe wie im vorstehenden Beispiel in Szenarien durchführen können, in denen die Handlerdelegierungsstrategie nicht verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="55e17-118">[OfficeDev/PnP/Samples/Core.AppEvents](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.AppEvents) shows how to do the same task as the preceding sample in scenarios where the handler delegation strategy cannot be used.</span></span>
    
 
-  [<span data-ttu-id="55e17-119">OfficeDev/PnP/Samples/Core.EventReceivers</span><span class="sxs-lookup"><span data-stu-id="55e17-119">OfficeDev/PnP/Samples/Core.EventReceivers</span></span>](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.EventReceivers)
    
 
-  [<span data-ttu-id="55e17-120">Erstellen eines vom Anbieter gehosteten Add-Ins mit angepasster Add-In-Installation</span><span class="sxs-lookup"><span data-stu-id="55e17-120">Create a provider-hosted add-in that customizes add-in installation</span></span>](https://code.msdn.microsoft.com/SharePoint-Create-a-f27752e0)
    
 

## <a name="add-an-add-in-installed-event-receiver"></a><span data-ttu-id="55e17-121">Hinzufügen eines Ereignisempfängers für das installierte Add-In</span><span class="sxs-lookup"><span data-stu-id="55e17-121">Add an add-in installed event receiver</span></span>
<span data-ttu-id="55e17-122"><a name="SP15appevent_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="55e17-122"><a name="SP15appevent_prereq"> </a></span></span>


1. <span data-ttu-id="55e17-p104">Öffnen Sie in Visual Studio das Projekt für das vom Anbieter gehostete SharePoint-Add-In. (Wenn Sie einen Add-In-Ereignishandler für ein in SharePoint gehostetes Add-In hinzufügen, wird sie von den Office-Entwicklertools für Visual Studio in ein vom Anbieter gehostetes Add-In umgewandelt.)</span><span class="sxs-lookup"><span data-stu-id="55e17-p104">In Visual Studio, open the project for the provider-hosted SharePoint Add-in. (If you add an add-in event handler to a SharePoint-hosted add-in, the Office Developer Tools for Visual Studio convert it to a provider-hosted app.)</span></span>
    
 
2. <span data-ttu-id="55e17-125">Wählen Sie im **Projektmappen-Explorer** den Knoten für das SharePoint-Add-In aus.</span><span class="sxs-lookup"><span data-stu-id="55e17-125">In  **Solution Explorer**, choose the node for the SharePoint Add-in.</span></span>
    
 
3. <span data-ttu-id="55e17-126">Legen Sie im Fenster **Eigenschaften** den Wert von **Installiertes Add-In verarbeiten** auf **True** fest.</span><span class="sxs-lookup"><span data-stu-id="55e17-126">In the  **Properties** window, set the value of **Handle Add-in Installed** to **True**.</span></span> 
    
    <span data-ttu-id="55e17-127">**Abbildung 1: Add-In-Ereignisse im Eigenschaftenfenster**</span><span class="sxs-lookup"><span data-stu-id="55e17-127">**Figure 1. Add-in events in the properties window**</span></span>

 

  ![Add-In-Ereignisse im Eigenschaftenfenster](../images/SP_VS_Properties_Window_AppEvents.PNG)
 

    <span data-ttu-id="55e17-129">Von den Office-Entwicklertools für Visual Studio wird Folgendes ausgeführt:</span><span class="sxs-lookup"><span data-stu-id="55e17-129">The Office Developer Tools for Visual Studio will do the following:</span></span>
    
 

      - <span data-ttu-id="55e17-p105">Eine Datei AppEventReceiver.svc mit grundlegendem C#- (oder VB.NET-)Code wird hinzugefügt. Dies ist der Dienst, der das Add-In-Ereignis behandelt.</span><span class="sxs-lookup"><span data-stu-id="55e17-p105">Add a file named AppEventReceiver.svc. that contains some skeletal C# (or VB.NET) code. This is the service that will handle the add-in event.</span></span>
    
 
  - <span data-ttu-id="55e17-p106">Der folgende Eintrag wird im Abschnitt **Eigenschaften** der Datei AppManifest.xml hinzugefügt: `<InstalledEventEndpoint>~remoteAppUrl/AppEventReceiver.svc</InstalledEventEndpoint>`. Dieser Eintrag registriert den Add-In-Ereignisempfänger in SharePoint. (Beachten Sie, dass das Token **~remoteAppUrl** das gleiche ist, das für die Remotewebanwendung in dem vom Anbieter gehosteten SharePoint-Add-In verwendet wurde. In den Office Developer Tools für Visual Studio wird davon ausgegangen, dass die Domäne der Webanwendung mit der des Ereignishandlers identisch ist. In den seltenen Fällen, wo dies nicht gilt, müssen Sie das Token **~remoteAppUrl** manuell durch die tatsächliche Domäne des Diensts ersetzen.)</span><span class="sxs-lookup"><span data-stu-id="55e17-p106">The following entry is added to the  **Properties** section of the AppManifest.xml file: `<InstalledEventEndpoint>~remoteAppUrl/AppEventReceiver.svc</InstalledEventEndpoint>`. This entry registers the add-in event receiver to SharePoint. (Note that the  **~remoteAppUrl** token is the same one used for the remote web application in the provider-hosted SharePoint Add-in. The Office Developer Tools for Visual Studio assume the domain of the web application and the event handler is the same. In the rare case where it is not, you need to manually replace the token **~remoteAppUrl** with the actual domain of your service.)</span></span>
    
 
  - <span data-ttu-id="55e17-p107">Wenn das SharePoint-Add-In-Projekt nicht bereits ein Webprojekt aufweist, wird eines von den Office Developer Tools für Visual Studio erstellt. Die Tools stellen außerdem sicher, dass das Add-In-Manifest für ein vom Anbieter gehostetes Add-In konfiguriert ist. Außerdem fügen sie Seiten, Skripts, CSS-Dateien und andere Artefakte hinzu. (Wenn die einzige Remotekomponente, die Ihr Add-In benötigt, der Webdienst für die Ereignisbehandlung ist, können Sie diese aus dem Projekt löschen. Außerdem sollten Sie sicherstellen, dass das **StartPage**-Element im Add-In-Manifest nicht auf eine Seite verweist, die Sie gelöscht haben.)</span><span class="sxs-lookup"><span data-stu-id="55e17-p107">If the SharePoint Add-in project doesn't already have a web project, the Office Developer Tools for Visual Studio create one. The tools also ensure that add-in manifest is configured for a provider-hosted add-in. They will also add pages, scripts, CSS files, and other artifacts. (If the only remote component that your add-in needs is the event-handling web service, you can delete these from the project. You also should ensure that the  **StartPage** element in the add-in manifest is not pointing to a page that you have deleted.)</span></span>
    
 
4. <span data-ttu-id="55e17-p108">Wenn sich die SharePoint-Testfarm nicht auf dem Computer mit Visual Studio befindet, konfigurieren Sie das Projekt zum Debuggen mit dem Microsoft Azure Service Bus. Weitere Informationen finden Sie unter  [Debugging und Problembehandlung eines Remoteereignisempfängers in einem Add-In für SharePoint](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="55e17-p108">If your test SharePoint farm is not on the same computer that is running Visual Studio, configure the project for debugging using the Microsoft Azure Service Bus. For more information, see  [Debug and troubleshoot a remote event receiver in a SharePoint Add-in](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in.md).</span></span> 
    
 
5. <span data-ttu-id="55e17-p109">Wenn die Datei AppEventReceiver.svc eine `ProcessOneWayEvent`-Methode enthält, sollte ihre Implementierung lediglich die Zeile `throw new NotImplementedException();` umfassen, da diese Methode nicht in einem Add-In-Ereignishandler verwendet werden kann. *Add-In-Ereignishandler müssen ein Objekt zurückgeben, das SharePoint mitteilt, ob das Ereignis abgeschlossen oder zurückgesetzt werden soll. Die `ProcessOneWayEvent`-Methode gibt jedoch nichts zurück.*</span><span class="sxs-lookup"><span data-stu-id="55e17-p109">If there is a  `ProcessOneWayEvent` method in the AppEventReceiver.svc file, it's implementation should consist of just the line `throw new NotImplementedException();`, because this method cannot be used in an add-in event handler.  *Add-in event handlers have to return an object that tells SharePoint whether to finish or roll back the event and the  `ProcessOneWayEvent` method doesn't return anything.*</span></span> 
    
 
6. <span data-ttu-id="55e17-p110">Die Datei enthält eine  `ProcessEvent`-Methode, die etwa wie folgt aussieht. (Sie kann auch einen Codeblock enthalten, der veranschaulicht, wie ein Clientkontext abgerufen wird. Löschen Sie diesen, oder kommentieren Sie ihn aus.)</span><span class="sxs-lookup"><span data-stu-id="55e17-p110">The file will include a  `ProcessEvent` method that looks something like the following. (There may also a block of code that illustrates how to get a client context. Delete it or comment out.)</span></span>
    
    <span data-ttu-id="55e17-150">Beachten Sie Folgendes zu diesem Code:</span><span class="sxs-lookup"><span data-stu-id="55e17-150">Note the following about this code:</span></span>
    
      - <span data-ttu-id="55e17-151">Das  **SPRemoteEventProperties** -Objekt wird an den Handlerwebdienst als SOAP-Nachricht gesendet, die Kontextinformationen von SharePoint enthält, beispielsweise eine **EventType** -Eigenschaft zur Identifizierung des Ereignisses.</span><span class="sxs-lookup"><span data-stu-id="55e17-151">The  **SPRemoteEventProperties** object is sent to your handler web service as a SOAP message that contains context information from SharePoint, including an **EventType** property that identifies the event.</span></span>
    
 
  - <span data-ttu-id="55e17-p111">Das vom Handler zurückgegebene **SPRemoteEventResult**-Objekt enthält eine **Status**-Eigenschaft mit den möglichen Werten **SPRemoteEventServiceStatus**. **Continue**, **SPRemoteEventServiceStatus.CancelNoError** und **SPRemoteEventServiceStatus.CancelWithError**. Der Standardwert der **Status**-Eigenschaft ist **Continue** und weist SharePoint an, das Ereignis abzuschließen. Die anderen beiden Werte weisen SharePoint an, Folgendes zu tun:</span><span class="sxs-lookup"><span data-stu-id="55e17-p111">The  **SPRemoteEventResult** object that your handler returns contains a **Status** property whose possible values are **SPRemoteEventServiceStatus**. **Continue**,  **SPRemoteEventServiceStatus.CancelNoError**, and  **SPRemoteEventServiceStatus.CancelWithError**. The default value of the  **Status** property is **Continue**, which tells SharePoint to finish the event. The other two values tell SharePoint to:</span></span>
    
      - <span data-ttu-id="55e17-156">Der Handler wird noch maximal drei Mal ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="55e17-156">Run your handler up to three more times.</span></span>
    
 
  - <span data-ttu-id="55e17-157">Wenn weiterhin ein „Cancel“-Status zurückgegeben wird, wird das Ereignis abgebrochen, und alles, was als Teil des Ereignisses ausgeführt wurde, wird zurückgesetzt.</span><span class="sxs-lookup"><span data-stu-id="55e17-157">If it is still getting a cancel status, cancel the event and roll back anything it has done as part of the event.</span></span> 
    
 



```C#
  public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
{
    SPRemoteEventResult result = new SPRemoteEventResult();

    return result;
}
```

7. <span data-ttu-id="55e17-158">Fügen Sie direkt unter der Zeile mit der Deklaration der `result`-Variable die folgende Verzweigungsstruktur hinzu, um das behandelte Ereignis zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="55e17-158">Immediately below the line that declares the  `result` variable, add the following switch structure to identify which event is being handled.</span></span>
    
```C#
  switch (properties.EventType)
{
    case SPRemoteEventType.AppInstalled:
        break;
    case SPRemoteEventType.AppUpgraded:
        break;
    case SPRemoteEventType.AppUninstalling:
        break;
}
```


     **Note**  The  **AppInstalled**,  **AppUpdated**, and  **AppInstalling** events, if you have handlers for them, will each get their own URL registered in the add-in manifest. So you *can*  have different endpoints for them; but this article (and the Office Developer Tools for Visual Studio) assume they have exactly the same endpoint; that's why the code needs to determine which event called it.
8. <span data-ttu-id="55e17-p112">Wie unter [Einbeziehen von Rollbacklogik und „Bereits erledigt“-Logik in Add-In-Ereignishandler](handle-events-in-sharepoint-add-ins.md#Rollback) erläutert wurde, möchten Sie bei einem Fehler in der Installationslogik fast immer, dass die Installation des Add-Ins abgebrochen wird und alle Installationsaktionen von SharePoint zurückgesetzt werden. Außerdem sollen die Aktionen Ihres Handlers zurückgesetzt werden. Eine Möglichkeit dazu besteht darin, folgenden Code in der **case**-Struktur für das AppInstalled-Ereignis hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="55e17-p112">As explained in  [Include rollback logic and "already done" logic in your add-in event handlers](handle-events-in-sharepoint-add-ins.md#Rollback), if anything goes wrong in your installation logic, you almost always want the add-in installation canceled, and you want SharePoint to roll back what it has done for the installation, and you want to roll back what your handler has done. One way to accomplish these goals is to add the following code inside the  **case** for the AppInstalled event.</span></span>
    
```C#
  case SPRemoteEventType.AppInstalled:
  try
  {
      // Add-in installed event logic goes here.
  }
  catch (Exception e)
  {
      result.ErrorMessage = e.ErrorMessage;
      result.Status = SPRemoteEventServiceStatus.CancelWithError;

      // Rollback logic goes here.
  }
  break;
```


     **Note**  Move installation code that takes more than 30 seconds into the add-in itself. You can add it to "first run" logic that executes the first time the add-in runs. The add-in can display a message saying something like "We're getting things ready for you." Alternatively, the add-in can prompt the user to run the initialization code.If "first run" logic is not feasible for your add-in, another option is to have your event handler start a remote asynchronous process and then immediately return a  **SPRemoteEventResult** object with the **Status** set to **Continue**. A weakness of this strategy is that if the remote process fails, it has no way to tell SharePoint to roll back the add-in installation.
9. <span data-ttu-id="55e17-p113">Wie unter  [Strategien für die Architektur von Add-In-Ereignishandlern](handle-events-in-sharepoint-add-ins.md#Strategies) erläutert, wird die Handlerdelegierungsstrategie bevorzugt, auch wenn sie nicht in jedem Szenario möglich ist. Im fortlaufenden Beispiel zeigen wir Ihnen, wie Sie die Handlerdelegierungsstrategie implementieren, wenn Sie eine Liste zum Hostweb hinzufügen. (Informationen zum Erstellen eines ähnlichen AppInstalled-Ereignishandlers, der nicht die Handlerdelegierungsstrategie verwendet, finden Sie im Beispiel [OfficeDev/PnP/Samples/Core.AppEvents](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.AppEvents).)</span><span class="sxs-lookup"><span data-stu-id="55e17-p113">As explained in  [Add-in event handler architecture strategies](handle-events-in-sharepoint-add-ins.md#Strategies), the handler delegation strategy is preferred, although not possible in every scenario. In the continuing example, we show you how to implement the handler delegation strategy when adding a list to the host web. (For information on how to create a similar AppInstalled event handler that does not use the handler delegation strategy, see the sample  [OfficeDev/PnP/Samples/Core.AppEvents](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.AppEvents).)</span></span>
    
    <span data-ttu-id="55e17-p114">Im Folgenden finden Sie die neue Version des **case**-Blocks für AppInstalled. Beachten Sie, dass Initialisierungslogik, die für alle Ereignisse gilt, über dem **switch**-Block steht. Da die gleiche Liste, die installiert wird, im AppUninstalling-Ereignishandler entfernt wird, wird die Liste hier identifiziert.</span><span class="sxs-lookup"><span data-stu-id="55e17-p114">The following is the new version of the AppInstalled  **case** block. Note that initialization logic that applies to all events goes above the **switch** block. Since the same list that is installed will be removed in the AppUninstalling handler, the list is identified there.</span></span>
    


```C#
  SPRemoteEventResult result = new SPRemoteEventResult();
String listTitle = "MyList";

switch (properties.EventType)
{               
    case SPRemoteEventType.AppInstalled:
                    
   try
   {
        string error = TryCreateList(listTitle, properties);
        if (error != String.Empty)
        {
            throw new Exception(error);            
        }
   }
    catch (Exception e)
   {
        // Tell SharePoint to cancel the event.
        result.ErrorMessage = e.Message;
        result.Status = SPRemoteEventServiceStatus.CancelWithError;               
    }
        break;
    case SPRemoteEventType.AppUpgraded:
       break;
    case SPRemoteEventType.AppUninstalling:
       break;
}                      
```

10. <span data-ttu-id="55e17-p115">Fügen Sie die Listenerstellungsmethode zur **AppEventReceiver**-Klasse als **private**-Methode mit folgendem Code hinzu. Beachten Sie, dass die `TokenHelper`-Klasse eine besondere Methode aufweist, die für das Abrufen eines Clientkontexts für ein Add-In-Ereignis optimiert ist. Durch die Übergabe von **false** für den letzten Parameter wird sichergestellt, dass der Kontext für das Hostweb gilt.</span><span class="sxs-lookup"><span data-stu-id="55e17-p115">Add the list creation method to the  **AppEventReceiver** class as a **private** method with the following code. Note that the `TokenHelper` class has a special method that is optimized for getting a client context for an add-in event. Passing **false** for the last parameter ensures that the context is for the host web.</span></span>
    
```C#
  private string TryCreateList(String listTitle, SPRemoteEventProperties properties)
 {    
    string errorMessage = String.Empty;          

    using (ClientContext clientContext =
        TokenHelper.CreateAppEventClientContext(properties, useAppWeb: false))
    {
        if (clientContext != null)
        {
        }
    }
    return errorMessage;
}

```

11. <span data-ttu-id="55e17-p116">Rollbacklogik besteht im Wesentlichen aus Ausnahmebehandlungslogik, und das SharePoint-CSOM (clientseitige Objektmodell) hat einen **ExceptionHandlingScope**, der es Ihrem Webdienst ermöglicht, die Ausnahmebehandlung an den SharePoint-Server zu delegieren. (Siehe auch [Gewusst wie: Verwenden des Ausnahmebehandlungsbereichs](http://msdn.microsoft.com/library/103619ef-1ba3-44e3-93e1-5e0685bc616e%28Office.15%29.aspx).) Fügen Sie den folgenden Code im **if**-Block des vorhergehenden Codeausschnitts hinzu.</span><span class="sxs-lookup"><span data-stu-id="55e17-p116">Rollback logic is basically exception handling logic and the SharePoint CSOM (Client-side object model) has a  **ExceptionHandlingScope** that enables your web service to delegate exception handling to the SharePoint server. (See also, [How to: Use Exception Handling Scope](http://msdn.microsoft.com/library/103619ef-1ba3-44e3-93e1-5e0685bc616e%28Office.15%29.aspx).) Add the following code to the  **if** block in the preceding snippet.</span></span>
    
```C#
  ExceptionHandlingScope scope = new ExceptionHandlingScope(clientContext); 

using (scope.StartScope()) 
{ 
    using (scope.StartTry()) 
    { 
    }         
    using (scope.StartCatch()) 
    {                                 
    } 
    using (scope.StartFinally()) 
    { 
    } 
} 
 clientContext.ExecuteQuery();

if (scope.HasException)
{
    errorMessage = String.Format("{0}: {1}; {2}; {3}; {4}; {5}", 
        scope.ServerErrorTypeName, scope.ErrorMessage, 
        scope.ServerErrorDetails, scope.ServerErrorValue, 
        scope.ServerStackTrace, scope.ServerErrorCode);
}
```

12. <span data-ttu-id="55e17-p117">Es gibt nur einen Aufruf von SharePoint ( **ExecuteQuery**) im vorherigen Codeausschnitt, aber leider bleibt es nicht bei dem einen. Jedes Objekt, auf das in unserem Ausnahmebereich verwiesen wird, muss zuerst in den Client geladen werden. Fügen Sie also den folgenden Code  *über*  dem Konstruktor für den **ExceptionHandlingScope** hinzu.</span><span class="sxs-lookup"><span data-stu-id="55e17-p117">There is only one call to SharePoint ( **ExecuteQuery**) in the preceding snippet, but unfortunately we can't quite do with only one. Every object that is going to be referenced in our exception scope has to first be loaded to the client. So add the following code  *above*  the constructor for the **ExceptionHandlingScope**.</span></span>
    
```C#
  ListCollection allLists = clientContext.Web.Lists;
IEnumerable<List> matchingLists =
    clientContext.LoadQuery(allLists.Where(list => list.Title == listTitle));
clientContext.ExecuteQuery();

var foundList = matchingLists.FirstOrDefault();
 List createdList = null;
```

13. <span data-ttu-id="55e17-p118">Der Code zum Erstellen einer Hostwebliste gehört in den **StartTry** -Block, aber zuerst muss überprüft werden, ob die Liste bereits hinzugefügt wurde (wie unter [Einbeziehen von Rollbacklogik und „Bereits erledigt“-Logik in Add-In-Ereignishandler](handle-events-in-sharepoint-add-ins.md#Rollback) erläutert). If-then-else-Logik kann über die **ConditionalScope** -Klasse an den SharePoint-Server delegiert werden. (Siehe auch [Gewusst wie: Verwenden des bedingten Bereichs](http://msdn.microsoft.com/library/560112e9-c3ed-4b8f-9cd4-c8bc5d60d63c%28Office.15%29.aspx).) Fügen Sie den folgenden Code im **StartTry**-Block hinzu.</span><span class="sxs-lookup"><span data-stu-id="55e17-p118">The code to create a host web list will go into the  **StartTry** block, but the code must first check whether the list has already been added (as explained in [Include rollback logic and "already done" logic in your add-in event handlers](handle-events-in-sharepoint-add-ins.md#Rollback)). If-then-else logic can be delegated to the SharePoint server by using the  **ConditionalScope** class. (See also, [How to: Use Conditional Scope](http://msdn.microsoft.com/library/560112e9-c3ed-4b8f-9cd4-c8bc5d60d63c%28Office.15%29.aspx).) Add the following code inside the  **StartTry** block.</span></span>
    
```C#
  ConditionalScope condScope = new ConditionalScope(clientContext, 
        () => foundList.ServerObjectIsNull.Value == true, true);
using (condScope.StartScope())
{
    ListCreationInformation listInfo = new ListCreationInformation();
    listInfo.Title = listTitle;
    listInfo.TemplateType = (int)ListTemplateType.GenericList;
    listInfo.Url = listTitle;
    createdList = clientContext.Web.Lists.Add(listInfo);                                
}
```

14. <span data-ttu-id="55e17-p119">Der  **StartCatch** -Block sollte die Erstellung der Liste rückgängig machen, aber zuvor muss überprüft werden, ob die Liste erstellt wurde. Denn möglicherweise wurde eine Ausnahme im **StartTry**-Block ausgelöst, bevor die Erstellung der Liste abgeschlossen war. Fügen Sie den folgenden Code im **StartCatch**-Block hinzu.</span><span class="sxs-lookup"><span data-stu-id="55e17-p119">The  **StartCatch** block should undo the creation of the list, but it needs to first check that the list was created, because an exception might have been thrown in the **StartTry** block before it finished creating the list. Add the following code to the **StartCatch** block.</span></span>
    
```C#
  ConditionalScope condScope = new ConditionalScope(clientContext, 
        () => createdList.ServerObjectIsNull.Value != true, true);
using (condScope.StartScope())
{
    createdList.DeleteObject();
} 
```


     **Tip**   **TROUBLESHOOTING:** To test whether your **StartCatch** block is entered when it should be, you need a way to throw a runtime exception on the SharePoint server. Using a **throw** or dividing by zero won't work because they cause *client-side*  exceptions before the client runtime can even bundle up the code and send it to the server (with the **ExecuteQuery** method). Instead, add the following lines to the **StartTry** block. The client-side runtime accepts this, but it causes a server-side exception, which is what you want. `List fakeList = clientContext.Web.Lists.GetByTitle("NoSuchList");`
 
 `clientContext.Load(fakeList);`

    The entire TryCreateList method should look like the following. (The  **StartFinally** block is required even when it is not being used.)
    


```C#
  private string TryCreateList(String listTitle, SPRemoteEventProperties properties)
{    
    string errorMessage = String.Empty;  

    using (ClientContext clientContext = 
        TokenHelper.CreateAppEventClientContext(properties, useAppWeb: false))
    {
        if (clientContext != null)
        {
            ListCollection allLists = clientContext.Web.Lists;
            IEnumerable<List> matchingLists = 
                clientContext.LoadQuery(allLists.Where(list => list.Title == listTitle));
            clientContext.ExecuteQuery();
            var foundList = matchingLists.FirstOrDefault();
            List createdList = null;

            ExceptionHandlingScope scope = new ExceptionHandlingScope(clientContext); 
            using (scope.StartScope()) 
            { 
                using (scope.StartTry()) 
                { 
                    ConditionalScope condScope = new ConditionalScope(clientContext, 
                            () => foundList.ServerObjectIsNull.Value == true, true);  
                    using (condScope.StartScope())
                    {
                        ListCreationInformation listInfo = new ListCreationInformation();
                        listInfo.Title = listTitle;
                        listInfo.TemplateType = (int)ListTemplateType.GenericList;
                        listInfo.Url = listTitle;
                        createdList = clientContext.Web.Lists.Add(listInfo);
                    }
                } 
                
                using (scope.StartCatch()) 
                { 
                    ConditionalScope condScope = new ConditionalScope(clientContext, 
                            () => createdList.ServerObjectIsNull.Value != true, true);
                    using (condScope.StartScope())
                    {
                        createdList.DeleteObject();
                    }    
                } 

                using (scope.StartFinally()) 
                { 
                } 
            } 
            clientContext.ExecuteQuery();

            if (scope.HasException)
            {
                    errorMessage = String.Format("{0}: {1}; {2}; {3}; {4}; {5}", 
                    scope.ServerErrorTypeName, scope.ErrorMessage, 
                    scope.ServerErrorDetails, scope.ServerErrorValue, 
                    scope.ServerStackTrace, scope.ServerErrorCode);
            }
        }
    }
    return errorMessage;
}
```


     **Tip**   **DEBUGGING:** Regardless of whether you are using the handler delegation strategy, when you are stepping through the code with the debugger, keep in mind that, in any scenario in which your handler returns a cancel status, SharePoint is going to call your handler again, up to three more times. So the debugger will cycle through the code up to four times.

     **Tip**   **CODE ARCHITECTURE:** Since you can install components on the add-in web with declarative markup outside your handler, you usually won't want to use up any of the 30 seconds your handler has available to interact with the add-in web. But if you do, keep in mind that your code requires a separate **ClientContext** object for the add-in web. This means that the add-in web and host web are different components, just as much as an SQL Server database is different from each of them. So a method that calls to the add-in web is in the **try** block of the AppInstalled **case** block, just like the TryCreateList method in the continuing example. However, your handler does *not*  need to roll back actions taken on the add-in web. If it encounters an error, it only needs to cancel the event, because SharePoint will delete the entire add-in web if the event is cancelled.

## <a name="create-an-add-in-uninstalling-event-receiver"></a><span data-ttu-id="55e17-180">Erstellen eines Ereignisempfängers für die Deinstallation des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="55e17-180">Create an add-in uninstalling event receiver</span></span>
<span data-ttu-id="55e17-181"><a name="SP15appevent_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="55e17-181"><a name="SP15appevent_prereq"> </a></span></span>


1. <span data-ttu-id="55e17-p120">Legen Sie die Eigenschaft **Deinstallation des Add-Ins verarbeiten** des Projekts auf **True** fest. Von den Tools wird *keine* weitere Webdienstdatei erstellt, falls eine vorhanden ist. Aber sie fügen dem Add-In-Manifest ein **UninstallingEventEndpoint**-Element hinzu.</span><span class="sxs-lookup"><span data-stu-id="55e17-p120">Set the  **Handle Add-in Uninstalling** property of the project to **True**. The tools do  *not*  create another web service file, if one already exists; but they do add an **UninstallingEventEndpoint** element to the add-in manifest.</span></span>
    
 
2. <span data-ttu-id="55e17-p121">Code im **case**-Block für AppUninstalling sollte Artefakte des Add-Ins entfernen, die nicht mehr benötigt werden, nachdem das Add-In aus dem endgültigen Papierkorb entfernt wurde, wodurch das Ereignis ausgelöst wird. Allerdings müssen Sie die Komponenten möglichst „außer Kraft setzen“, anstatt sie vollständig zu löschen. Der Grund ist, dass Sie sie wiederherstellen müssen, wenn das Deinstallationsereignis rückgängig gemacht werden muss. In diesem Fall befindet sich das Add-In noch im endgültigen Papierkorb, und ein Benutzer kann es wiederherstellen und erneut verwenden. Das Neuerstellen einer gelöschten Komponente in der Rollbacklogik ist möglicherweise ausreichend, um das Add-In wieder funktionsfähig zu machen, aber Daten oder Konfigurationseinstellungen in der Komponente würden dann verloren gehen.</span><span class="sxs-lookup"><span data-stu-id="55e17-p121">Code in the AppUninstalling  **case** block should remove artifacts of the add-in that aren't needed after the add-in is removed from the second stage recycle bin, which is what triggers the event. However, whenever possible you need to "retire" the components rather than totally delete them. This is because, you need to restore them if the uninstalling event has to be rolled back. If that happens, the add-in is still in the second stage recycle bin and a user could restore it and start using it again. Merely recreating a deleted component in your rollback logic might be enough to enable the add-in to work again, but any data or configuration settings in the component would be lost.</span></span>
    
    <span data-ttu-id="55e17-p122">Diese Strategie ist für SharePoint-Komponenten relativ einfach, da SharePoint über einen Papierkorb verfügt, aus dem Elemente wiederhergestellt werden können, und es CSOM-APIs für den Zugriff gibt. Spätere Schritte in diesem Verfahren zeigen, wie das geht. Für andere Plattformen können unterschiedliche Techniken erforderlich sein. Wenn Sie beispielsweise eine Zeile in einer SQL Server-Tabelle in Ihrem Add-In-Deinstallationshandler außer Kraft setzen möchten, kann eine gespeicherte T-SQL-Prozedur im Ereignishandler eine IsDeleted-Spalte zur Tabelle hinzufügen und für die Zeile auf **True** festlegen. Wenn in der Prozedur ein Fehler auftritt, setzt die Rollbacklogik den Wert auf **False** zurück. Wenn die Prozedur ohne Fehler abgeschlossen wird, kann sie kurz vor der Rückgabe eines Erfolgsflags einen Zeitgeberauftrag für die spätere Löschung der Zeile festlegen.</span><span class="sxs-lookup"><span data-stu-id="55e17-p122">This strategy is relatively easy for SharePoint components, since SharePoint has a recycle bin from which things can be restored, and there are CSOM APIs for accessing it. Later steps of this procedure show how. For other platforms, different techniques may be needed. For example, if you want to retire a row in an SQL Server table in your add-in uninstalling handler, a T-SQL stored procedure in the handler can add an IsDeleted column to the table and set it to  **True** for the row. If the procedure encounters an error, the rollback logic resets the value to **False**. If the procedure completes without error, then just before it returns a success flag, it can set a timer job to delete the row later.</span></span>
    
    <span data-ttu-id="55e17-195">Manchmal möchten Sie Daten, wie z. B. Listen, auch nach dem Löschen des Add-Ins behalten, aber als Beispiel in diesem Artikel wird im folgenden Deinstallationsereignishandler die Liste gelöscht, die mit dem Installationsereignishandler erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="55e17-195">Sometimes you want to keep data, such as lists, even after the add-in is deleted; but as an example for this article, the following is an uninstalling event handler that deletes the list that was created with the installed event handler.</span></span>
    


```C#
  case SPRemoteEventType.AppUninstalling:

try
{
    string error = TryRecycleList(listTitle, properties);
    if (error != String.Empty)
    {
        throw new Exception(error);
    }
}
catch (Exception e)
{
    // Tell SharePoint to cancel the event.
    result.ErrorMessage = e.Message;
    result.Status = SPRemoteEventServiceStatus.CancelWithError;
}
break;
```

3. <span data-ttu-id="55e17-p123">Fügen Sie die Hilfsmethode für die Wiederverwendung der Liste hinzu. Beachten Sie Folgendes zu diesem Code:</span><span class="sxs-lookup"><span data-stu-id="55e17-p123">Add the helper method for recycling the list. Note the following about this code:</span></span>
    
      - <span data-ttu-id="55e17-p124">Der Code verschiebt die Liste in den Papierkorb, anstatt sie dauerhaft zu löschen. Dies ermöglicht das Wiederherstellen der Liste und der zugehörigen Daten nach einem Fehler im Ereignis, was im **StartCatch**-Block geschieht. Wenn die Methode erfolgreich ist und das Ereignis abgeschlossen ist, wird das Add-In dauerhaft aus dem endgültigen Papierkorb gelöscht, aber die Liste befindet sich noch im Papierkorb.</span><span class="sxs-lookup"><span data-stu-id="55e17-p124">The code recycles the list, instead of permanently deleting it. This makes it possible to restore it, including its data, if the event fails, which is what the  **StartCatch** block does. So, if the method succeeds and the event completes, the add-in is permanently deleted from the second stage recycle bin, but the list is still in the first stage recycle bin.</span></span>
    
 
  - <span data-ttu-id="55e17-p125">Der Code prüft das Vorhandensein der Liste, bevor sie wieder verwendet wird, da ein Benutzer sie bereits auf der SharePoint-Benutzeroberfläche wieder verwendet haben könnte. Auf ähnliche Weise überprüft der Rollbackcode das Vorhandensein der Liste im Papierkorb, bevor sie wiederhergestellt wird, da ein Benutzer sie möglicherweise bereits wiederhergestellt haben oder in den endgültigen Papierkorb verschoben haben könnte.</span><span class="sxs-lookup"><span data-stu-id="55e17-p125">The code tests for the existence of the list before it recycles it because a user might have already recycled it in the SharePoint UI. Similiarly, the rollback code checks for the existence of the list in the recycle bin before it restores it, because a user might have already restored it or moved it to the second-stage recycle bin.</span></span> 
    
 
  - <span data-ttu-id="55e17-p126">Es gibt zwei bedingte Bereiche, die das Vorhandensein einer Liste testen, indem sie überprüfen, ob ein Verweis darauf **null** ist. Aber beide verfügen über einen inneren **if**-Block, der dasselbe Objekt ein zweites Mal auf null überprüft. Die äußeren Tests mit Blocks mit bedingten Bereichen werden auf dem Server ausgeführt, aber die inneren Tests auf null sind ebenfalls erforderlich. Denn die Client-Laufzeit durchläuft den Code Zeile für Zeile zum Erstellen der XML-Meldung, die die **ExecuteQuery**-Methode an den Server sendet. Wenn die Verweise auf die Objekte **foundList** und **recycledList** erreicht werden, löst die eine oder andere dieser Zeilen eine Nullverweisausnahme aus, sofern sie nicht innerhalb der inneren null-Überprüfungen eingeschlossen sind.</span><span class="sxs-lookup"><span data-stu-id="55e17-p126">There are two conditional scopes that test for a list's existence by checking to see if a reference to it is  **null**. But both of them have an inner  **if** block that test the very same object for nullity a second time. The outer tests, with conditional scope blocks, run on the server, but the inner nullity tests are also needed. This is because the client runtime moves through the code line-by-line to create the XML message that the **ExecuteQuery** method will send to the server. When the references to the **foundList** and **recycledList** objects are reached, one or another of these lines throws a Null Reference exception unless they are encased inside the inner nullity checks.</span></span>
    
 

```C#
  private string TryRecycleList(String listTitle, SPRemoteEventProperties properties)
{
    string errorMessage = String.Empty;

    using (ClientContext clientContext = 
        TokenHelper.CreateAppEventClientContext(properties, useAppWeb: false))
    {
        if (clientContext != null)
        {
            ListCollection allLists = clientContext.Web.Lists;
            IEnumerable<List> matchingLists = 
                clientContext.LoadQuery(allLists.Where(list => list.Title == listTitle));
            RecycleBinItemCollection bin = clientContext.Web.RecycleBin;
            IEnumerable<RecycleBinItem> matchingRecycleBinItems = 
                clientContext.LoadQuery(bin.Where(item => item.Title == listTitle));        
            clientContext.ExecuteQuery();

            List foundList = matchingLists.FirstOrDefault();
            RecycleBinItem recycledList = matchingRecycleBinItems.FirstOrDefault();    

            ExceptionHandlingScope scope = new ExceptionHandlingScope(clientContext);
            using (scope.StartScope())
            {
                using (scope.StartTry())
                {
                    ConditionalScope condScope = new ConditionalScope(clientContext, 
                        () => foundList.ServerObjectIsNull.Value == false, true);
                    using (condScope.StartScope())
                    {
                        if (foundList != null)
                        {
                            foundList.Recycle();
                        }
                    }
                }
                using (scope.StartCatch())
                {
                    ConditionalScope condScope = new ConditionalScope(clientContext, 
                         () => recycledList.ServerObjectIsNull.Value == false, true);
                    using (condScope.StartScope())
                    {
                        if (recycledList != null)
                        {
                            recycledList.Restore(); 
                        }
                    }
                }
                using (scope.StartFinally())
                {
                }
            }
            clientContext.ExecuteQuery();

            if (scope.HasException)
            {
                errorMessage = String.Format("{0}: {1}; {2}; {3}; {4}; {5}", 
                    scope.ServerErrorTypeName, scope.ErrorMessage, 
                    scope.ServerErrorDetails, scope.ServerErrorValue, 
                    scope.ServerStackTrace, scope.ServerErrorCode);
            }
        }
    }
    return errorMessage;
}
```


### <a name="to-debug-and-test-an-add-in-uninstalling-event-receiver"></a><span data-ttu-id="55e17-208">So debuggen und testen Sie einen Ereignisempfänger für die Deinstallation des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="55e17-208">To debug and test an add-in uninstalling event receiver</span></span>


1. <span data-ttu-id="55e17-209">Öffnen Sie alle folgenden Seiten in verschiedenen Fenstern oder Registerkarten:</span><span class="sxs-lookup"><span data-stu-id="55e17-209">Open all of the following pages in separate windows or tabs:</span></span>
    
      -  <span data-ttu-id="55e17-210">**Websiteinhalte**</span><span class="sxs-lookup"><span data-stu-id="55e17-210">**Site Contents**</span></span>
    
 
  -  <span data-ttu-id="55e17-211">**Websiteeinstellungen – Papierkorb** (_layouts/15/AdminRecycleBin.aspx?ql=1)</span><span class="sxs-lookup"><span data-stu-id="55e17-211">**Site Settings - Recycle Bin** (_layouts/15/AdminRecycleBin.aspx?ql=1)</span></span>
    
 
  -  <span data-ttu-id="55e17-212">**Papierkorb – Endgültiger Papierkorb** (_layouts/15/AdminRecycleBin.aspxView=2&amp;?ql=1)</span><span class="sxs-lookup"><span data-stu-id="55e17-212">**Recycle Bin - Second-Stage Recycle Bin** (_layouts/15/AdminRecycleBin.aspxView=2&amp;?ql=1)</span></span>
    
 
2. <span data-ttu-id="55e17-p127">Drücken Sie F5, und vertrauen Sie dem Add-In, wenn Sie dazu aufgefordert werden. Die Startseite des Add-Ins wird geöffnet. Wenn Sie nur den Deinstallationsereignishandler testen möchten, können Sie dieses Browserfenster schließen.  *Wenn Sie den Handler jedoch debuggen, lassen Sie es geöffnet. Beim Schließen wird die Debuggingsitzung beendet.*</span><span class="sxs-lookup"><span data-stu-id="55e17-p127">Press F5 and trust the add-in when prompted. The add-in's start page opens. If you are only going to test the uninstallation handler, you can close this browser window.  *But if you are debugging the handler, leave it open. Closing it will end the debugging session.*</span></span> 
    
 
3. <span data-ttu-id="55e17-217">Aktualisieren Sie die Seite **Websiteinhalte**, und wenn das Add-In angezeigt wird, entfernen Sie es.</span><span class="sxs-lookup"><span data-stu-id="55e17-217">Refresh the  **Site Contents** page, and when the add-in appears, remove it.</span></span>
    
 
4. <span data-ttu-id="55e17-p128">Aktualisieren Sie die Seite **Websiteeinstellungen – Papierkorb**. Das Add-In wird als das erste Element angezeigt. Aktivieren Sie das Kontrollkästchen daneben, und klicken Sie auf **Auswahl löschen**.</span><span class="sxs-lookup"><span data-stu-id="55e17-p128">Refresh the  **Site Settings - Recycle Bin** page. The add-in will appear as the top item. Select the check box beside it and click **Delete Selection**.</span></span>
    
 
5. <span data-ttu-id="55e17-p129">Aktualisieren Sie die Seite **Papierkorb – Endgültiger Papierkorb**. Das Add-In wird als das erste Element angezeigt. Aktivieren Sie das Kontrollkästchen daneben, und klicken Sie auf **Auswahl löschen**. SharePoint wird sofort Ihren Ereignishandler für die Deinstallation des Add-Ins aufrufen.</span><span class="sxs-lookup"><span data-stu-id="55e17-p129">Refresh the  **Recycle Bin - Second-Stage Recycle Bin** page. The add-in will appear as the top item. Select the checkbox beside it and click **Delete Selection**. SharePoint will immediately call your add-in uninstalling handler.</span></span>
    
 

## <a name="create-an-add-in-updated-event-receiver"></a><span data-ttu-id="55e17-225">Erstellen eines Ereignisempfängers für die Aktualisierung des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="55e17-225">Create an add-in updated event receiver</span></span>
<span data-ttu-id="55e17-226"><a name="SP15appevent_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="55e17-226"><a name="SP15appevent_prereq"> </a></span></span>

<span data-ttu-id="55e17-227">Ausführliche Informationen zum Erstellen eines Handlers für das aktualisierte Add-In finden Sie unter [Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="55e17-227">For details about creating an add-in updated handler, see  [Create a handler for the update event in SharePoint Add-ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md).</span></span>
 

 

## <a name="url-and-hosting-restrictions-on-production-add-in-event-receivers"></a><span data-ttu-id="55e17-228">URL- und Hostingeinschränkungen für Add-In-Ereignisempfänger in Produktion</span><span class="sxs-lookup"><span data-stu-id="55e17-228">URL and hosting restrictions on production add-in event receivers</span></span>
<span data-ttu-id="55e17-229"><a name="SP15appevent_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="55e17-229"><a name="SP15appevent_prereq"> </a></span></span>

<span data-ttu-id="55e17-p130">Der Add-In-Ereignisempfänger kann in der Cloud oder auf einem lokalen Server gehostet werden, der nich gleichzeitig als SharePoint-Server verwendet wird. Die URL eines Produktionsempfängers kann keinen bestimmten Port angeben. Daher müssen Sie entweder Port 443 für HTTPS verwenden, was empfohlen wird, oder Port 80 für HTTP. Wenn Sie HTTPS verwenden und der Empfängerdienst lokal gehostet wird, sich das Add-In jedoch auf Microsoft SharePoint Online befindet, muss der Hostingserver über ein öffentlich vertrauenswürdiges Zertifikat einer Zertifikatstelle verfügen. (Ein selbstsigniertes Zertifikat kann nur verwendet werden, wens sich das Add-In in einer lokalen SharePoint-Farm befindet.)</span><span class="sxs-lookup"><span data-stu-id="55e17-p130">The add-in event receiver can be hosted in the cloud or in an on-premise server that is not also being used as a SharePoint server. The URL of a production receiver cannot specify a particular port. This means that you must use either port 443 for HTTPS, which we recommend, or port 80 for HTTP. If you are using HTTPS and the receiver service is hosted on-premise, but the add-in is on Microsoft SharePoint Online, then the hosting server must have a publically trusted certificate from a certificate authority. (A self-signed certificate works only if the add-in is in an on-premise SharePoint farm.)</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="55e17-235">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="55e17-235">Additional resources</span></span>
<span data-ttu-id="55e17-236"><a name="SP15appevent_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="55e17-236"><a name="SP15appevent_addlresources"> </a></span></span>


-  [<span data-ttu-id="55e17-237">Behandeln von Ereignissen in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="55e17-237">Handle events in SharePoint Add-ins</span></span>](handle-events-in-sharepoint-add-ins.md)
    
 

