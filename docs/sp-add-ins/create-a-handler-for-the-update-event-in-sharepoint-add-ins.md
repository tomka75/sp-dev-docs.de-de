---
title: "Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins"
description: "Erstellen und verwenden Sie einen Handler und wenden Sie Rollbacklogik für das Updateereignis eines SharePoint-Add-Ins an."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 8c781f0c03b6d2fa46a2def5ed9eef8026771b1d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="create-a-handler-for-the-update-event-in-sharepoint-add-ins"></a><span data-ttu-id="b9645-103">Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="b9645-103">Create a handler for the update event in SharePoint Add-ins</span></span>

<span data-ttu-id="b9645-104">Bevor Sie beginnen, sollten Sie sich umfassend mit den Themen [Behandeln von Add-In-Ereignissen](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) und [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins.md) sowie den darin aufgeführten Voraussetzungen und Kernkonzepten vertraut machen.</span><span class="sxs-lookup"><span data-stu-id="b9645-104">Before you begin, be thoroughly familiar with both [Handling add-in events](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) and [Update SharePoint Add-ins](update-sharepoint-add-ins.md) and the prerequisites and core concepts listed in them.</span></span>

> [!NOTE]
> <span data-ttu-id="b9645-105">**Versionsnummernsystem:** Aus Gründen der Konsistenz wird in diesem Thema davon ausgegangen, dass die Add-In-Versionsnummern 1.0.0.0, 2.0.0.0, 3.0.0.0 usw. sind.</span><span class="sxs-lookup"><span data-stu-id="b9645-105">**Version numbering system:** For consistency, this topic assumes that the add-in version numbers are 1.0.0.0, 2.0.0.0, 3.0.0.0, and so on.</span></span> <span data-ttu-id="b9645-106">Die Logik und Anleitungen gelten jedoch unabhängig davon, welches Nummernsystem Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="b9645-106">However, the logic and guidance applies no matter what your numbering system is.</span></span>

<span data-ttu-id="b9645-107"><a name="UpgradedEventEndpoint"> </a></span><span class="sxs-lookup"><span data-stu-id="b9645-107"><a name="UpgradedEventEndpoint"> </a></span></span>
## <a name="create-an-upgradedeventendpoint-receiver"></a><span data-ttu-id="b9645-108">Erstellen eines UpgradedEventEndpoint-Empfängers</span><span class="sxs-lookup"><span data-stu-id="b9645-108">Create an UpgradedEventEndpoint receiver</span></span>

<span data-ttu-id="b9645-109">Für die benutzerdefinierte Aktualisierungslogik können Sie einen SharePoint-Remoteereignisempfänger erstellen, der das Add-In-Updated-Ereignis verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="b9645-109">For custom update logic, you can create a SharePoint remote event receiver that handles the add-in updated event.</span></span> <span data-ttu-id="b9645-110">Sie sollten mit dieser Methode vorsichtig sein.</span><span class="sxs-lookup"><span data-stu-id="b9645-110">You should be conservative in using this technique.</span></span> <span data-ttu-id="b9645-111">Verwenden Sie sie nur, wenn Schritte nicht auf eine andere Weise aktualisiert werden können.</span><span class="sxs-lookup"><span data-stu-id="b9645-111">Use it only for updating steps that can't be done any other way.</span></span> <span data-ttu-id="b9645-112">Die Anleitung unter [Behandeln von Add-in-Ereignissen](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) gilt ebenso für das Add-In-Updated- wie das Add-In-Installed- und das Add-In-Uninstalling-Ereignis.</span><span class="sxs-lookup"><span data-stu-id="b9645-112">Also, the guidance found in [Handling add-in events](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) applies for the add-in updated event as much as the add-in installed and add-in uninstalling events.</span></span> <span data-ttu-id="b9645-113">Dies umfasst Folgendes:</span><span class="sxs-lookup"><span data-stu-id="b9645-113">This includes:</span></span>

- <span data-ttu-id="b9645-114">Der Handler muss entweder einen Abbruch- oder einen Fortfahren-Status abschließen und diesen innerhalb von 30 Sekunden an SharePoint zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="b9645-114">Your handler has to complete and return either a cancel or a continue status to SharePoint in 30 seconds.</span></span> <span data-ttu-id="b9645-115">Wenn dies nicht der Fall ist, ruft SharePoint den Handler bis zu drei Mal erneut auf.</span><span class="sxs-lookup"><span data-stu-id="b9645-115">If it does not, SharePoint calls the handler again up to three more times.</span></span>

- <span data-ttu-id="b9645-116">Wenn der Handler einen Abbruchstatus zurückgibt, versucht SharePoint es bis zu drei Mal erneut.</span><span class="sxs-lookup"><span data-stu-id="b9645-116">If your handler returns a cancel status, SharePoint will retry up to three more times.</span></span> 

- <span data-ttu-id="b9645-117">ie müssen in der Regel Rollback- und „Bereits erledigt“-Logik in den Ereignishandler einbeziehen.</span><span class="sxs-lookup"><span data-stu-id="b9645-117">You usually need to include rollback and "already done" logic in your handler.</span></span>

<span data-ttu-id="b9645-p104">Ein Szenario, in dem ein **UpgradedEventEndpoint**-Handler nützlich ist, ist wenn ein berechnetes Feld zu einer Remotedatenbank hinzugefügt wird. Angenommen, die Spalte "Ort" wird hinzugefügt, und der Wert wird anhand einer bereits bestehenden Postleitzahl-Spalte berechnet. Ihr Code in einem **UpgradedEventEndpoint**-Handler könnte vorhandene Elemente in der Datenbank durchlaufen und den Wert für das neue Ort-Feld auf Basis des Werts des Postleitzahl-Felds und einer externen Datenquelle, die Postleitzahlen Orten zuordnet, einfügen. Die Änderung am Datenbankschema selbst sollte außerhalb des **UpgradedEventEndpoint**-Handlers mithilfe der bewährten Vorgehensweisen der Datenbankplattform vorgenommen werden.</span><span class="sxs-lookup"><span data-stu-id="b9645-p104">One scenario in which an **UpgradedEventEndpoint** handler is useful is when a computed field is added to a remote database. Suppose a City column is added, and its value is computed from an already existing Postal Code column. Your code in an **UpgradedEventEndpoint** handler could iterate through existing items in the database and fill in the value for the new City field based on the value of the Postal Code field and some external data source that maps postal codes onto cities. The change to the database schema itself is best done outside the **UpgradedEventEndpoint** handler by using the best practices of the database platform.</span></span>

<span data-ttu-id="b9645-122">Weitere Informationen zum Erstellen eines Ereignishandlers für das Add-In-Ereignis finden Sie unter [Behandeln von Ereignissen in SharePoint-Add-Ins](handle-events-in-sharepoint-add-ins.md) und [Erstellen eines Add-In-Ereignisempfängers in SharePoint-Add-Ins](create-an-add-in-event-receiver-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="b9645-122">For more details about how to create a handler for the add-in event, see [Handle events in SharePoint Add-ins](handle-events-in-sharepoint-add-ins.md) and [Create an add-in event receiver in SharePoint Add-ins](create-an-add-in-event-receiver-in-sharepoint-add-ins.md).</span></span> 

<span data-ttu-id="b9645-123">Im folgende Verfahren wird davon ausgegangen, dass Sie das Add-In-Ereignisempfänger-Element zu einem SharePoint-Add-In-Projekt in Visual Studio hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="b9645-123">The following procedure assumes that you have added the add-in event receiver item to your SharePoint Add-in project in Visual Studio.</span></span> 

### <a name="to-handle-the-add-in-updated-event-the-first-time"></a><span data-ttu-id="b9645-124">So behandeln Sie das Add-In-Updated-Ereignis beim ersten Mal</span><span class="sxs-lookup"><span data-stu-id="b9645-124">To handle the add-in updated event the first time</span></span>

1. <span data-ttu-id="b9645-125">Öffnen Sie die Datei AppEventReceiver.svc.cs und fügen Sie eine bedingte Struktur zur **ProcessEvent**-Methode hinzu, die überprüft, ob es sich bei dem Ereignis, das den Handler aufgerufen hat, um das Updated-Ereignis handelt.</span><span class="sxs-lookup"><span data-stu-id="b9645-125">Open the AppEventReceiver.svc.cs file, and add a conditional structure to the **ProcessEvent** method that tests whether the event that invoked the handler is the updated event.</span></span> <span data-ttu-id="b9645-126">Der Aktualisierungscode wird in diese Struktur eingefügt.</span><span class="sxs-lookup"><span data-stu-id="b9645-126">Your updating code goes inside this structure.</span></span> <span data-ttu-id="b9645-127">Wenn der Code auf SharePoint zugreifen muss, können Sie das SharePoint-Clientobjektmodell für verwalteten Code (CSOM) oder eine REST-Schnittstelle (Representational State Transfer) verwenden.</span><span class="sxs-lookup"><span data-stu-id="b9645-127">If your code needs to access SharePoint, you can use the SharePoint managed code client object model (CSOM) or Representational State Transfer (REST) interface.</span></span> 

   <span data-ttu-id="b9645-128">Wo sich die bedingte Struktur in der Methode befindet, hängt von der Strukturierung des übrigen Codes in der Methode ab.</span><span class="sxs-lookup"><span data-stu-id="b9645-128">Where the conditional structure is located in the method depends on how you have structured the other code in the method.</span></span> <span data-ttu-id="b9645-129">In der Regel handelt es sich um einen Peer mit ähnlichen bedingten Strukturen, der die Add-In-Installed- und Add-In-Uninstalling-Ereignisse überprüft.</span><span class="sxs-lookup"><span data-stu-id="b9645-129">Typically, it is a peer of similar conditional structures that test for the add-in installed and add-in uninstalling events.</span></span> <span data-ttu-id="b9645-130">Er kann sich innerhalb einer bedingten Struktur befinden, die bestimmte Eigenschaften oder untergeordnete Eigenschaften des Objekts **SPRemoteEventProperties**, das an **ProcessEvent** weitergegeben wird, auf **Null**- oder andere ungültige Werte überprüft.</span><span class="sxs-lookup"><span data-stu-id="b9645-130">It may be within a conditional structure that tests certain properties or subproperties of the **SPRemoteEventProperties** object that is passed to **ProcessEvent** for **null** values or other invalid values.</span></span> <span data-ttu-id="b9645-131">Er kann sich auch innerhalb eines **Try**-Blocks befinden.</span><span class="sxs-lookup"><span data-stu-id="b9645-131">It may also be within a **try** block.</span></span> 
   
   <span data-ttu-id="b9645-132">Nachfolgend finden Sie ein Beispiel für die Struktur.</span><span class="sxs-lookup"><span data-stu-id="b9645-132">The following is an example of the structure.</span></span> <span data-ttu-id="b9645-133">Das _Eigenschaften_-Objekt ist ein **SPRemoteEventProperties**-Objekt.</span><span class="sxs-lookup"><span data-stu-id="b9645-133">The _properties_ object is an **SPRemoteEventProperties** object.</span></span>
    
    ```C#
       if (properties.EventType == SPRemoteEventType.AppUpgraded)
     {
     }

    ```

2. <span data-ttu-id="b9645-134">Wenn Sie CSOM im Ereignishandler verwenden möchten, fügen Sie (im bedingten Block) einen **Using**-Block hinzu, der ein **ClientContext**-Objekt erhält, indem er die **TokenHelper.CreateAppEventClientContext**-Methode abruft.</span><span class="sxs-lookup"><span data-stu-id="b9645-134">To use CSOM in the handler, add (within the conditional block) a **using** block that gets a **ClientContext** object by calling the **TokenHelper.CreateAppEventClientContext** method.</span></span> <span data-ttu-id="b9645-135">Geben Sie **true** für den zweiten Parameter an, um auf das Add-In-Web zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="b9645-135">Specify **true** for the second parameter to access the add-in web.</span></span> <span data-ttu-id="b9645-136">Geben Sie **false** an, um auf das Hostweb zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="b9645-136">Specify **false** to access the host web.</span></span> <span data-ttu-id="b9645-137">Wenn Sie auf beide zugreifen möchten, benötigen Sie zwei verschiedene Clientkontextobjekte.</span><span class="sxs-lookup"><span data-stu-id="b9645-137">If you need to access both, you need two different client context objects.</span></span>

3. <span data-ttu-id="b9645-p109">Wenn Ihr Handler auf Nicht-SharePoint-Komponenten zugreifen muss, fügen Sie diesen Code außerhalb von Clientkontextblöcken ein. Ihr Code sollte in etwa folgendermaßen strukturiert sein:</span><span class="sxs-lookup"><span data-stu-id="b9645-p109">If your handler needs to access non-SharePoint components, put that code outside any client context blocks. Your code should be structured similarly to the following:</span></span>
    
    ```C#
       if (properties.EventType == SPRemoteEventType.AppUpgraded)
     {
         using (ClientContext cc = TokenHelper.CreateAppEventClientContext(properties, true))
         {
             // CSOM code that accesses the add-in web
         }
         using (ClientContext cc = TokenHelper.CreateAppEventClientContext(properties, false))
         {
             // CSOM code that accesses the host web
         }
         // Other update code
     }

    ```

4. <span data-ttu-id="b9645-p110">Um die REST-Schnittstelle zu verwenden, verwendet Ihr Code andere Methoden in der **TokenHelper**-Klasse, um ein Zugriffstoken zu erhalten, das dann in die Anforderungen eingefügt wird, die an SharePoint gesendet werden. Weitere Informationen finden Sie in  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](complete-basic-operations-using-sharepoint-rest-endpoints.md). Ihr Code sollte in etwa folgendermaßen strukturiert sein.</span><span class="sxs-lookup"><span data-stu-id="b9645-p110">To use the REST interface, your code uses other methods in the **TokenHelper** class to get an access token, which is then included in the requests it makes to SharePoint. For more information, see [Complete basic operations using SharePoint REST endpoints](complete-basic-operations-using-sharepoint-rest-endpoints.md). Your code should be structured similarly to the following.</span></span>
    
    ```C#
       if (properties.EventType == SPRemoteEventType.AppUpgraded)
     {
         string contextTokenString = TokenHelper.GetContextTokenFromRequest(Request);
         if (contextTokenString != null)
         {
             contextToken = TokenHelper.ReadAndValidateContextToken(contextTokenString, 
                                                                                                                       Request.Url.Authority);
             accessToken = TokenHelper.GetAccessToken(contextToken, sharepointUrl.Authority)
                                        .AccessToken;

            // REST code that accesses SharePoint
         }  
         // Other update code
     }

    ```

5. <span data-ttu-id="b9645-143">Für den Zugriff auf SharePoint muss der REST-Code zudem die URL des Hostwebs und/oder des Add-In-Webs kennen.</span><span class="sxs-lookup"><span data-stu-id="b9645-143">To access SharePoint, your REST code also needs to know the URL of the host web or add-in web or both.</span></span> <span data-ttu-id="b9645-144">Diese URLs sind beide untergeordnete Eigenschaften des **SPRemoteEventProperties**-Objekts, das an die **ProcessEvent**-Methode übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="b9645-144">These URLs are both subproperties of the **SPRemoteEventProperties** object that is passed to the **ProcessEvent** method.</span></span> <span data-ttu-id="b9645-145">Der folgende Code veranschaulicht das Abrufen der URLs.</span><span class="sxs-lookup"><span data-stu-id="b9645-145">The following code shows how to get them.</span></span>
    
    ```C#
       Uri hostWebURL = properties.AppEventProperties.HostWebFullUrl;
       Uri appWebURL = properties.AppEventProperties.AppWebFullUrl;
    ```

<span data-ttu-id="b9645-p112">Wenn Sie eine App das zweite (oder dritte usw.) Mal aktualisieren, müssen Sie möglicherweise sicherstellen, dass Updatelogik nicht mehrere Male auf der gleichen App-Instanz ausgeführt wird. Das folgende Verfahren zeigt, wie Sie dabei vorgehen.</span><span class="sxs-lookup"><span data-stu-id="b9645-p112">When you update an add-in for the second (or third, and so on) time, you may need to ensure that some update logic does not run multiple times on the same add-in instance. The following procedure shows you how.</span></span>

### <a name="to-handle-the-add-in-updated-event-on-subsequent-updates"></a><span data-ttu-id="b9645-148">So behandeln Sie das Add-In-Updated-Ereignis bei weiteren Updates</span><span class="sxs-lookup"><span data-stu-id="b9645-148">To handle the add-in updated event on subsequent updates</span></span>

1. <span data-ttu-id="b9645-149">Öffnen Sie die Datei AppEventReceiver.svc.cs und suchen Sie den Code, der beim ersten Update (von 1.0.0.0. auf 2.0.0.0) Updateaktionen</span><span class="sxs-lookup"><span data-stu-id="b9645-149">Open the AppEventReceiver.svc.cs file, and find the code that implemented update actions in the first update (from 1.0.0.0.</span></span> <span data-ttu-id="b9645-150">implementiert hat.</span><span class="sxs-lookup"><span data-stu-id="b9645-150">to 2.0.0.0).</span></span> <span data-ttu-id="b9645-151">Wir bezeichnen diesen Code als vorherigen Updatecode.</span><span class="sxs-lookup"><span data-stu-id="b9645-151">Let's call this the previous update code.</span></span> <span data-ttu-id="b9645-152">(Dieser Code ist normalerweise nach dem Autorisierungscode platziert, der Clientkontext oder Zugriffstoken abruft.) Nachdem Sie jetzt ein erneutes Update (von 2.0.0.0 auf 3.0.0.0) durchführen, befinden sich hier normalerweise Aktionen im vorherigen Updatecode, die nicht noch einmal auf der gleichen App-Instanz ausgeführt werden sollen. Sie sollen aber auf einer App-Instanz ausgeführt werden, die noch nicht auf 2.0.0.0 aktualisiert wurde (in diesem Fall wird die Instanz jetzt direkt von 1.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="b9645-152">(This code is generally located after the authorization code that gets client context or access tokens.) Now that you are updating again (from 2.0.0.0 to 3.0.0.0), there will typically be actions in the previous update code here that you don't want to run again on the same add-in instance, but you do want it to run on an add-in instance that was never updated to 2.0.0.0 (in which case, the instance is now being updated all the way from 1.0.0.0.</span></span> <span data-ttu-id="b9645-153">auf 3.0.0.0 aktualisiert).</span><span class="sxs-lookup"><span data-stu-id="b9645-153">to 3.0.0.0).</span></span>

2. <span data-ttu-id="b9645-154">Umschließen Sie den vorherigen Updatecode mit einer Bedingungsstruktur, die auf die vorherige Version der App-Instanz testet und nur ausgeführt wird, wenn der Code in der Struktur auf dieser App-Instanz zuvor noch nicht ausgeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="b9645-154">Wrap the previous update code in a conditional structure that tests for the previous version of the add-in instance and executes only if the code in the structure has not run before on this add-in instance.</span></span> <span data-ttu-id="b9645-155">Die vorherige Version der Instanz wird in der untergeordneten **PreviousVersion** -Eigenschaft des **SPRemoteEventProperties**-Objekts gespeichert.</span><span class="sxs-lookup"><span data-stu-id="b9645-155">The previous version of the instance is stored in the **PreviousVersion** subproperty of the **SPRemoteEventProperties** object.</span></span>

3. <span data-ttu-id="b9645-156">Fügen Sie die neue Updatelogik (für die Aktualisierung von 2.0.0.0 auf 3.0.0.0) zu dieser Struktur hinzu.</span><span class="sxs-lookup"><span data-stu-id="b9645-156">Add your new update logic (for the update from 2.0.0.0 to 3.0.0.0) under this structure.</span></span> <span data-ttu-id="b9645-157">Es folgt ein Beispiel.</span><span class="sxs-lookup"><span data-stu-id="b9645-157">The following is an example.</span></span>
    
    ```C#
       Version ver2OOO = new Version("2.0.0.0");
     if (properties.AppEventProperties.PreviousVersion < ver2OOO)
     {
         // Code to update from 1.0.0.0 to 2.0.0.0 (previous update code) is here.
     }
     // Code to update from 2.0.0.0 to 3.0.0.0 is here.

    ```

4. <span data-ttu-id="b9645-p116">Wiederholen Sie diese Schritte für jedes weitere Update. Für das Update von 3.0.0.0 auf 4.0.0.0 sollte Ihr Code die folgende Struktur aufweisen.</span><span class="sxs-lookup"><span data-stu-id="b9645-p116">For each subsequent update, repeat these steps. For the update from 3.0.0.0 to 4.0.0.0, your code should have the following structure.</span></span>
    
    ```C#
     Version ver2OOO = new Version("2.0.0.0");
     if (properties.AppEventProperties.PreviousVersion < ver2OOO)
     {
         // Code to update from 1.0.0.0 to 2.0.0.0 is here.
     }

     Version ver3OOO = new Version("3.0.0.0");
     if (properties.AppEventProperties.PreviousVersion < ver3OOO)
     {
         // Code to update from 2.0.0.0 to 3.0.0.0 (previous update code) is here.
     }
     // Code to update from 3.0.0.0 to 4.0.0.0 is here.

    ```

> [!IMPORTANT]
> <span data-ttu-id="b9645-160">Wenn Sie eine Komponente zu einem Add-In in einem **UpgradedEventEndpoint**-Handler hinzufügen, stellen Sie sicher, dass Sie den gleichen Code zum **InstalledEventEndpoint**-Handler hinzufügen, da diese Komponente ebenfalls im Add-In einer völlig neuen Installation enthalten sein soll.</span><span class="sxs-lookup"><span data-stu-id="b9645-160">If you add a component to an add-in in an **UpgradedEventEndpoint** handler, be sure to add the same code to an **InstalledEventEndpoint** handler because you want that component included in the add-in on a brand new installation as well.</span></span> <span data-ttu-id="b9645-161">Darüber hinaus sollten Sie einen [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx) für das Add-In hinzufügen (oder überarbeiten), um die Komponente zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="b9645-161">Also, you should add an [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx) (or revise it) for the add-in to remove the component.</span></span> 

> <span data-ttu-id="b9645-162">In den meisten Fällen sollte alles, was durch den **InstalledEventEndpoint** hinzugefügt oder geändert wurde, vom **UninstallingEventEndpoint** bearbeitet oder gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="b9645-162">For the most part, anything that was added or changed by the **InstalledEventEndpoint** should be reversed or deleted by the **UninstallingEventEndpoint**.</span></span> <span data-ttu-id="b9645-163">Eine Ausnahme bilden Daten, die nach dem Löschen des Add-Ins weiterhin nützlich sind. Diese Daten sollten nicht aus dem endgültigen Papierkorb gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="b9645-163">One exception is that data that will remain useful after the add-in is removed from the second-stage recycle bin should not be deleted.</span></span> <span data-ttu-id="b9645-164">(Websites zusätzlich zum Add-In-Web, die durch das Add-in erstellt werden, sollten als Daten betrachtet werden.)</span><span class="sxs-lookup"><span data-stu-id="b9645-164">(Websites, other than the add-in web, that are created by the add-in should be considered data.)</span></span>

<span data-ttu-id="b9645-165"><a name="AddRollbackLogic"> </a></span><span class="sxs-lookup"><span data-stu-id="b9645-165"><a name="AddRollbackLogic"> </a></span></span>
## <a name="add-rollback-logic-to-the-handler"></a><span data-ttu-id="b9645-166">Hinzufügen von Rollbacklogik zum Handler</span><span class="sxs-lookup"><span data-stu-id="b9645-166">Add rollback logic to the handler</span></span>

<span data-ttu-id="b9645-167">Wenn ein Fehler bei der Aktualisierung eines Add-Ins auftritt, stoppt die SharePoint-Infrastruktur den Updatevorgang und führt ein Rollback der Add-In-Instanz und aller dazugehörigen Komponenten auf die vorherige Version der Add-In-Instanz durch.</span><span class="sxs-lookup"><span data-stu-id="b9645-167">If an error occurs when an add-in is being updated, the SharePoint infrastructure stops the update process and rolls back the add-in instance and all its components to the previous version of the add-in instance.</span></span> <span data-ttu-id="b9645-168">Da die Infrastruktur nicht wissen kann, was Ihre **UpgradedEventEndpoint**-Handlerlogik tut, können diese Vorgänge nicht immer rückgängig gemacht werden.</span><span class="sxs-lookup"><span data-stu-id="b9645-168">But the infrastructure has no way of knowing what your **UpgradedEventEndpoint** handler logic does, so it can't always undo it.</span></span> <span data-ttu-id="b9645-169">Wenn ein unbehandelter Ausnahmefehler bei der Ausführung des **UpgradedEventEndpoint**-Handlers ausgelöst wird, bedeutet dies fast immer, dass der gesamte Add-In-Updatevorgang rückgängig gemacht werden sollte, dies aber nicht möglich ist, da die Infrastruktur nicht weiß, wie sie Aktionen rückgängig machen kann, die der **UpgradedEventEndpoint**-Code durchgeführt hat.</span><span class="sxs-lookup"><span data-stu-id="b9645-169">An unhandled exception thrown while your **UpgradedEventEndpoint** handler is executing almost certainly indicates that the entire add-in update process should be rolled back, but it won't be because the infrastructure doesn't know how to undo some things that your **UpgradedEventEndpoint** code might have done.</span></span> <span data-ttu-id="b9645-170">Aus diesem Grund muss der **UpgradedEventEndpoint**-Code folgende Aufgaben ausführen:</span><span class="sxs-lookup"><span data-stu-id="b9645-170">For this reason, the **UpgradedEventEndpoint** code must:</span></span>

- <span data-ttu-id="b9645-171">Er muss alle Ausnahmen abfangen.</span><span class="sxs-lookup"><span data-stu-id="b9645-171">Catch all exceptions.</span></span>
    
- <span data-ttu-id="b9645-172">Er muss zu benutzerdefiniertem Rollback-Code verzweigen, um alle bis zu diesem Zeitpunkt erfolgten Aktionen zurückzusetzen.</span><span class="sxs-lookup"><span data-stu-id="b9645-172">Branch to custom rollback code to undo what has been done to that point.</span></span>
    
- <span data-ttu-id="b9645-173">Er muss der SharePoint-Infrastruktur signalisieren, dass das gesamte App-Update zurückgesetzt werden sollte.</span><span class="sxs-lookup"><span data-stu-id="b9645-173">Signal to the SharePoint infrastructure that the entire add-in update should be rolled back.</span></span>
    
- <span data-ttu-id="b9645-174">Er muss eine Fehlermeldung an die Infrastruktur weiterleiten.</span><span class="sxs-lookup"><span data-stu-id="b9645-174">Pass on an error message to the infrastructure.</span></span>

<span data-ttu-id="b9645-175">Nicht alle Aktionen des **UpgradedEventEndpoint** müssen explizit im Handler rückgängig gemacht werden.</span><span class="sxs-lookup"><span data-stu-id="b9645-175">Not everything your **UpgradedEventEndpoint** does needs to be explicitly reversed inside the handler.</span></span> <span data-ttu-id="b9645-176">Das Add-In-Web wird von der Infrastruktur zurückgesetzt, sodass der Code keine Änderungen am Add-In-Web rückgängig machen muss.</span><span class="sxs-lookup"><span data-stu-id="b9645-176">The add-in web is going to be rolled back by the infrastructure, so your code does not have to undo changes to the add-in web.</span></span> <span data-ttu-id="b9645-177">Der **UpgradedEventEndpoint**-Handler muss jedoch in der Regel die Änderungen rückgängig machen, die er am Hostweb oder anderen Komponenten vorgenommen hat, die sich außerhalb des SharePoint-Add-Ins befinden.</span><span class="sxs-lookup"><span data-stu-id="b9645-177">But the **UpgradedEventEndpoint** handler usually does have to reverse the changes it has made to the host web or other components that are external to the SharePoint Add-in.</span></span>

<span data-ttu-id="b9645-p121">Beim zweiten (oder dritten usw.) Update muss Ihre Ausnahmebehandlungslogik die Tatsache berücksichtigen, dass die App-Instanz, die aktualisiert wird, nicht unbedingt die unmittelbar vorhergehende Version ist. Ist sie dies nicht, müssen möglicherweise zwei oder mehr Blöcke mit Updatecode rückgängig gemacht werden. Aus diesem Grund benötigen Sie Bedingungslogik, die auf der Nummer der vorherigen Version basiert. Es folgt ein Beispiel für die Rollback-Logik für ein Update auf Version 4.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="b9645-p121">On the second (or third, and so on) update, your exception handing logic has to take account of the fact that the add-in instance that is being updated is not necessarily the immediately previous version. If it isn't, there may be two or more blocks of update code that need to be reversed. For this reason, you need conditional logic that is based on the number of the previous version. The following is an example of the rollback logic for an update to version 4.0.0.0.</span></span>

```C#
catch (Exception e)
{ 
    // Rollback of the 3.0.0.0 to 4.0.0.0 update logic goes here.

    Version ver3OOO = new Version("3.0.0.0");
    if (properties.AppEventProperties.PreviousVersion < ver3OOO)
    {
        // Rollback of the 2.0.0.0 to 3.0.0.0 update logic goes here.
    }

    Version ver2OOO = new Version("2.0.0.0");
    if (properties.AppEventProperties.PreviousVersion < ver2OOO)
    {
        // Rollback of the 1.0.0.0 to 2.0.0.0 update logic goes here.
    }
}
```

<span data-ttu-id="b9645-182">Als letzter Schritt der Fehlerbehandlung sollten dem **SPRemoteEventResult** -Objekt eine Fehlermeldung und ein Abbruchstatus zugewiesen werden, die von der **ProcessEvent**-Methode an die SharePoint-Update-Infrastruktur zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="b9645-182">The last things your error handling should do is assign an error message and a cancel status to the **SPRemoteEventResult** object that the **ProcessEvent** method returns to the SharePoint update infrastructure.</span></span> <span data-ttu-id="b9645-183">Es folgt ein Beispiel.</span><span class="sxs-lookup"><span data-stu-id="b9645-183">The following is an example.</span></span> <span data-ttu-id="b9645-184">In diesem Code ist das _Ergebnis_ ein **SPRemoteEventResult**-Objekt, das zuvor in der **ProcessEvent**-Methode deklariert wurde.</span><span class="sxs-lookup"><span data-stu-id="b9645-184">In this code, _result_ is an **SPRemoteEventResult** object that has been declared earlier in the **ProcessEvent** method.</span></span>

```C#
catch (Exception e)
{     
    result.ErrorMessage = "custom message " + e.Message;
    result.Status = SPRemoteEventServiceStatus.CancelWithError;

     // Rollback logic from the preceding code snippet  is here. 

}
```

> [!IMPORTANT]
> <span data-ttu-id="b9645-185">Das Zuweisen von **SPRemoteEventServiceStatus.CancelWithError** (oder **SPRemoteEventServiceStatus.CancelNoError**) zu der Eigenschaft **Status** ist von entscheidender Bedeutung.</span><span class="sxs-lookup"><span data-stu-id="b9645-185">Assigning **SPRemoteEventServiceStatus.CancelWithError** (or **SPRemoteEventServiceStatus.CancelNoError**) to the **Status** property is crucial.</span></span> <span data-ttu-id="b9645-186">Diese Eigenschaft signalisiert der Infrastruktur, dass ein Rollback des Updates durchgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="b9645-186">This property is what signals the infrastructure to roll back the update.</span></span> <span data-ttu-id="b9645-187">SharePoint ruft den Handler drei Mal auf, bevor das Rollback des Updates erfolgt.</span><span class="sxs-lookup"><span data-stu-id="b9645-187">But SharePoint will retry your handler three times before it rolls back the update.</span></span>

### <a name="use-the-handler-delegation-strategy"></a><span data-ttu-id="b9645-188">Verwenden der Handlerdelegierungsstrategie</span><span class="sxs-lookup"><span data-stu-id="b9645-188">Use the handler delegation strategy</span></span>

<span data-ttu-id="b9645-189">Die unter [Behandeln von Add-In-Ereignissen](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) beschriebene Handlerdelegierungsstrategie kann ebenfalls in einem **UpdatedEventHandler** verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="b9645-189">The handler delegation strategy that is described in [Handling add-in events](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) can be used in an **UpdatedEventHandler** too.</span></span> <span data-ttu-id="b9645-190">Nicht nur die Rollback- und die „Bereits erledigt“-Logik werden gebündelt und auf der Remotekomponente ausgeführt, sondern auch die Versionsverwaltungslogik.</span><span class="sxs-lookup"><span data-stu-id="b9645-190">Not only is your rollback and "already done" logic bundled and run on the remote component, but your versioning logic is too.</span></span> <span data-ttu-id="b9645-191">Die Grenzen dieser Strategie gelten auch hier; Sie können sie in der Regel nur für die Aktualisierung eines Remotesystems verwenden.</span><span class="sxs-lookup"><span data-stu-id="b9645-191">The limitations of the strategy apply here too; you usually can't use it to update more than one remote system.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9645-192">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="b9645-192">Next steps</span></span>

<span data-ttu-id="b9645-193">Kehren Sie zu [Wichtige Schritte beim Aktualisieren eines Add-Ins](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) zurück, oder rufen Sie direkt einen der folgenden Artikel auf, um zu erfahren, wie Sie die nächste Hauptkomponente Ihres SharePoint-Add-Ins aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="b9645-193">Return to [Major steps in updating an add-in](update-sharepoint-add-ins.md#MajorAppUpgradeSteps), or go directly to one of the following articles to learn how to update the next major component of your SharePoint Add-in.</span></span>

-  [<span data-ttu-id="b9645-194">Aktualisieren von Add-In-Webkomponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b9645-194">Update add-in web components in SharePoint</span></span>](update-add-in-web-components-in-sharepoint.md)
-  [<span data-ttu-id="b9645-195">Aktualisieren von Hostwebkomponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b9645-195">Update host web components in SharePoint</span></span>](update-host-web-components-in-sharepoint.md)
-  [<span data-ttu-id="b9645-196">Aktualisieren von Remotekomponenten in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="b9645-196">Update remote components in SharePoint Add-ins</span></span>](update-remote-components-in-sharepoint-add-ins.md)

## <a name="see-also"></a><span data-ttu-id="b9645-197">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="b9645-197">See also</span></span>

-  [<span data-ttu-id="b9645-198">Aktualisieren von Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="b9645-198">Update SharePoint Add-ins</span></span>](update-sharepoint-add-ins.md)
-  [<span data-ttu-id="b9645-199">UpgradedEventEndpoint-Element (PropertiesDefinition ComplexType) (SharePoint-Add-In-Manifest)</span><span class="sxs-lookup"><span data-stu-id="b9645-199">UpgradedEventEndpoint element (PropertiesDefinition complexType) (SharePoint Add-in Manifest)</span></span>](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx)
-  [<span data-ttu-id="b9645-200">Behandeln von Ereignissen in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="b9645-200">Handle events in SharePoint Add-ins</span></span>](handle-events-in-sharepoint-add-ins.md)
-  [<span data-ttu-id="b9645-201">Erstellen eines Add-In-Ereignisempfängers in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="b9645-201">Create an add-in event receiver in SharePoint Add-ins</span></span>](create-an-add-in-event-receiver-in-sharepoint-add-ins.md)
    
 

