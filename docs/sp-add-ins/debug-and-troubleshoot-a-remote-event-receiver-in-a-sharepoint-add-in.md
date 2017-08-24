# <a name="debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in"></a><span data-ttu-id="66d86-101">Debugging und Problembehandlung eines Remoteereignisempfängers in einem Add-In für SharePoint</span><span class="sxs-lookup"><span data-stu-id="66d86-101">Debug and troubleshoot a remote event receiver in a SharePoint Add-in</span></span>
<span data-ttu-id="66d86-102">Richten Sie die Entwicklungsumgebung zum Debuggen von Remoteereignissen mithilfe von Visual Studio ein.</span><span class="sxs-lookup"><span data-stu-id="66d86-102">Set up the your development environment to debug remote events in by using Visual Studio.</span></span>
 

 <span data-ttu-id="66d86-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="66d86-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="configure-debugging-for-a-remote-sharepoint-test-site"></a><span data-ttu-id="66d86-106">Konfigurieren des Debuggens für eine SharePoint-Remotetestwebsite</span><span class="sxs-lookup"><span data-stu-id="66d86-106">Configure debugging for a remote SharePoint test site</span></span>


 <span data-ttu-id="66d86-p102">**Hinweis** Die Verfahren in diesem Abschnitt gelten nur, wenn sich die SharePoint-Testwebsite auf einem anderen Computer als Visual Studio befindet (oder wenn Sie eine SharePoint Online-Entwicklerwebsite als Testwebsite verwenden). Wenn sich SharePoint und Visual Studio auf demselben Computer befinden, überspringen Sie diesen Abschnitt.</span><span class="sxs-lookup"><span data-stu-id="66d86-p102">**Note** The procedures in this section apply only when your test SharePoint site is on a different computer from Visual Studio or you are using an SharePoint Online Developer Site as your test site. If SharePoint and Visual Studio are on the same computer, skip this section.</span></span>
 

<span data-ttu-id="66d86-p103">Wenn ein SharePoint-Add-In-Projekt in Visual Studio einen Remoteereignisempfänger (RER) oder einen Add-In-Ereignisempfänger enthält, müssen Sie einige zusätzliche schnelle Konfigurationsschritte in den Projekteigenschaften vornehmen, bevor Sie das Add-In mit (F5) debuggen können. Für diese Konfiguration ist wiederum eine Azure-Konfigurationsänderung erforderlich. Sie müssen die Azure-Konfiguration nicht für jedes Projekt mit einem RER oder einem Add-In-Ereignisempfänger wiederholen. (Wenn das Add-In einen AppInstalled-Ereignishandler enthält, wird das Add-In sogar erst mit F5 oder STRG+F5 [Ausführen ohne Debuggen] ausgeführt, nachdem Sie die in diesem Abschnitt beschriebene Konfiguration durchgeführt haben.)</span><span class="sxs-lookup"><span data-stu-id="66d86-p103">When a SharePoint Add-in project in Visual Studio includes a remote event receiver (RER) or an add-in event receiver, you have to do some additional quick configuration in the project properties before you can debug the add-in with (F5). This configuration, in turn, requires that you do some Azure configuration. You do not have to repeat the Azure configuration for every project that has an RER or add-in event. (If the add-in includes an AppInstalled event handler, the add-in won't even run with either F5 or Ctrl-F5 [run without debugging] unless you carry out the configuration in this section.)</span></span>
 

 

### <a name="to-configure-azure"></a><span data-ttu-id="66d86-113">So konfigurieren Sie Azure</span><span class="sxs-lookup"><span data-stu-id="66d86-113">To configure Azure</span></span>


1. <span data-ttu-id="66d86-p104">Erwerben Sie ein Microsoft Azure-Abonnement, falls noch nicht geschehen. Ein solches Abonnement ist beispielsweise als Zusatz in einem [MSDN-Abonnement](http://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits/) enthalten.</span><span class="sxs-lookup"><span data-stu-id="66d86-p104">If you don't already have one, get an Microsoft Azure subscription. One is included as a benefit with an  [MSDN Subscription](http://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits/).</span></span>
    
 
2. <span data-ttu-id="66d86-116">Führen Sie die Anweisungen unter [How To: Create or Modify a Service Bus Service Namespace](http://msdn.microsoft.com/library/fa561f70-007c-45aa-b34d-56317dbbfc87.aspx) aus.</span><span class="sxs-lookup"><span data-stu-id="66d86-116">Carry out the instructions in  [How To: Create or Modify a Service Bus Service Namespace](http://msdn.microsoft.com/library/fa561f70-007c-45aa-b34d-56317dbbfc87.aspx).</span></span>
    
 

### <a name="to-configure-the-sharepoint-add-in-project-in-visual-studio"></a><span data-ttu-id="66d86-117">So konfigurieren Sie das SharePoint-Add-In-Projekt in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="66d86-117">To configure the SharePoint Add-in project in Visual Studio</span></span>


1. <span data-ttu-id="66d86-118">Sie sollten über die neueste Version von Office Developer Tools für Visual Studio 2013 verfügen,  [führen Sie daher das WebPI-Installationsprogramm hier](http://aka.ms/OfficeDevToolsForVS2013) aus oder [Installationsprogramm für Office Developer Tools für Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015). .</span><span class="sxs-lookup"><span data-stu-id="66d86-118">You should have the latest version of the Office Developer Tools for Visual Studio 2013, so  [run the WebPI installer here](http://aka.ms/OfficeDevToolsForVS2013), or  [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span>
    
 
2. <span data-ttu-id="66d86-119">Klicken Sie nach dem Hinzufügen eines RER oder eines Add-In-Ereignishandlers zu einem SharePoint-Add-In-Projekt in Visual Studio im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie **Eigenschaften** aus.</span><span class="sxs-lookup"><span data-stu-id="66d86-119">After you add a RER or add-in event handler to a SharePoint Add-in project in Visual Studio, right-click the project in **Solution Explorer** and select **Properties**.</span></span>
    
 
3. <span data-ttu-id="66d86-120">Öffnen Sie im Eigenschaftenbereich die Registerkarte **SharePoint**, und scrollen Sie nach unten.</span><span class="sxs-lookup"><span data-stu-id="66d86-120">In the properties pane, open the **SharePoint** tab and scroll to the bottom.</span></span>
    
 
4. <span data-ttu-id="66d86-121">Aktivieren Sie das Kontrollkästchen **Debuggen über Microsoft Azure Service Bus aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="66d86-121">Select the check box for **Enable debugging via Microsoft Azure Service Bus**.</span></span>
    
 
5. <span data-ttu-id="66d86-p105">Geben Sie die vollständige Verbindungszeichenfolge in das bereitgestellte Textfeld ein. Sie erhalten die Zeichenfolge mit den folgenden Schritten.</span><span class="sxs-lookup"><span data-stu-id="66d86-p105">Enter the complete connection string in the text box provided. You obtain the string with these steps.</span></span>
    
      1. <span data-ttu-id="66d86-124">Melden Sie sich beim Azure-Portal an, und öffnen Sie die Registerkarte **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="66d86-124">Log in to the Azure portal and open the **Service Bus** tab.</span></span>
    
 
  2. <span data-ttu-id="66d86-p106">Öffnen Sie den Namespace, den Sie für das RER-Debugging erstellt haben, und navigieren Sie zu der Verbindungszeichenfolge. Die Benutzeroberfläche des Azure-Portals ändert sich häufig. Wenn Sie die Verbindungszeichenfolgen nicht finden können, finden Sie weitere Informationen in der  [Hilfe zum Azure-Portal](https://msdn.microsoft.com/en-us/library/azure/dn578292.aspx).</span><span class="sxs-lookup"><span data-stu-id="66d86-p106">Open the namespace that you created for RER debugging and navigate to the connection strings. The Azure portal UI changes frequently. See  [Azure portal help](https://msdn.microsoft.com/en-us/library/azure/dn578292.aspx) if you can't find the connection strings.</span></span>
    
 
  3. <span data-ttu-id="66d86-p107">Kopieren Sie die **SAS**-Verbindungszeichenfolge. Das ist die Zeichenfolge, die Sie in den Visual Studio-Projekteigenschaften eingeben.</span><span class="sxs-lookup"><span data-stu-id="66d86-p107">Copy the **SAS** connection string. This is the string you enter in the Visual Studio project properties.</span></span>
    
 
<span data-ttu-id="66d86-130">Wen Sie in Zukunft SharePoint-Add-In-Projekte in Visual Studio erstellen, sind diese Informationen bereits ausgefüllt, sodass Sie nicht jedes Mal das Azure-Portal öffnen müssen.</span><span class="sxs-lookup"><span data-stu-id="66d86-130">In the future, when you create SharePoint Add-in projects in Visual Studio, this information is prefilled, so you don't have to open the Azure portal each time.</span></span>
 

## <a name="test-the-configuration"></a><span data-ttu-id="66d86-131">Testen der Konfiguration</span><span class="sxs-lookup"><span data-stu-id="66d86-131">Test the configuration</span></span>
<span data-ttu-id="66d86-132"><a name="CreateRER"> </a></span><span class="sxs-lookup"><span data-stu-id="66d86-132"></span></span>

<span data-ttu-id="66d86-133">Verwenden Sie die Verfahren in diesem Abschnitt, um sicherzustellen, dass Sie ein RER debuggen können.</span><span class="sxs-lookup"><span data-stu-id="66d86-133">Use the procedures in this section to verify that you can debug an RER.</span></span>
 

 

### <a name="to-create-a-remote-event-receiver-project"></a><span data-ttu-id="66d86-134">So erstellen Sie ein Remoteereignisempfängerprojekt</span><span class="sxs-lookup"><span data-stu-id="66d86-134">To create a remote event receiver project</span></span>


1. <span data-ttu-id="66d86-135">Erstellen Sie in Visual Studio ein vom Anbieter gehostetes SharePoint-Add-In.</span><span class="sxs-lookup"><span data-stu-id="66d86-135">In Visual Studio, create a provider-hosted SharePoint Add-in.</span></span>
    
    <span data-ttu-id="66d86-136">Weitere Informationen dazu finden Sie unter [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="66d86-136">See  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins).</span></span>
    
 
2. <span data-ttu-id="66d86-137">Wählen Sie im **Projektmappen-Explorer** den Knoten des Add-In-Projekts aus.</span><span class="sxs-lookup"><span data-stu-id="66d86-137">In **Solution Explorer**, choose the add-in project's node.</span></span>
    
 
3. <span data-ttu-id="66d86-138">Wählen Sie in der Menüleiste **Projekt**, **Neues Element hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="66d86-138">On the menu bar, choose **Project**, **Add New Item**.</span></span>
    
 
4. <span data-ttu-id="66d86-139">Wählen Sie im Bereich **Vorlagen** die Vorlage **Liste** aus, und wählen Sie dann die Schaltfläche **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="66d86-139">In the **Templates** pane, choose the **List** template, and then choose the **Add** button.</span></span>
    
 
5. <span data-ttu-id="66d86-140">Wählen Sie die Schaltfläche **Fertig stellen** aus, um dem Add-In-Projekt eine benutzerdefinierte Standardliste hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="66d86-140">Choose the **Finish** button to add a default custom list to the add-in project.</span></span>
    
 
6. <span data-ttu-id="66d86-141">Fügen Sie dem Add-In-Projekt ein weiteres Element hinzu, indem Sie im Bereich **Vorlagen** die Vorlage **Remoteereignisempfänger** auswählen.</span><span class="sxs-lookup"><span data-stu-id="66d86-141">Add another item to the add-in project by, in the **Templates** pane, choosing the **Remote Event Receiver** template.</span></span>
    
 
7. <span data-ttu-id="66d86-142">Lassen Sie den Standardnamen im Feld **Name** unverändert (RemoteEventReceiver1), und wählen Sie dann **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="66d86-142">In the **Name** box, leave the default name (RemoteEventReceiver1), and then choose the **Add** button.</span></span>
    
 
8. <span data-ttu-id="66d86-143">Wählen Sie in der Liste **Welchen Typ soll der Ereignisempfänger aufweisen?** die Option **Listenelementereignisse** aus.</span><span class="sxs-lookup"><span data-stu-id="66d86-143">In the **What type of event receiver do you want?** list, choose **List Item Events**.</span></span> 
    
    <span data-ttu-id="66d86-144">Belassen Sie die Ereignisquelle als **List1**, die Liste, die Sie im vorhergehenden Schritt hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="66d86-144">Leave the event source as **List1**, the list that you added in the previous steps.</span></span>
    
 
9. <span data-ttu-id="66d86-145">Wählen Sie in der Liste **Die folgenden Ereignisse behandeln** die Option **Ein Element wird hinzugefügt** aus, und klicken Sie anschließend auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="66d86-145">In the **Handle the following events** list, choose **An item is being added**, and then choose the **Finish** button.</span></span>
    
    <span data-ttu-id="66d86-p108">Der Webanwendung wird ein Webdienst zur Behandlung des von Ihnen angegebenen Remoteereignisses hinzugefügt. Der SharePoint-Add-In wird ein Remoteereignisempfänger hinzugefügt. Der Empfänger referenziert den Webdienst und das Listenelementereignis in der Datei "Elements.xml" des Ereignisempfängers.</span><span class="sxs-lookup"><span data-stu-id="66d86-p108">A web service is added to the web application to handle the remote event that you specified. A remote event receiver is added to the SharePoint Add-in. The receiver references the web service and the list item event in the event receiver's Elements.xml file.</span></span>
    
 
10. <span data-ttu-id="66d86-149">Öffnen Sie in der Add-In-Projekt die Datei „AppManifest.xml“.</span><span class="sxs-lookup"><span data-stu-id="66d86-149">In the add-in project, open AppManifest.xml.</span></span>
    
 
11. <span data-ttu-id="66d86-150">Ändern Sie die Startseite in die Seite der Liste: _AddInProjectName _/Lists/List1.</span><span class="sxs-lookup"><span data-stu-id="66d86-150">Change the start page to the list's page:  _AddInProjectName_/Lists/List1.</span></span>
    
    <span data-ttu-id="66d86-p109">Ersetzen Sie  _AddInProjectName_ durch den Namen des Add-In-Projekts, z. B.SharePointAddIn4/Lists/List1. Bei diesem Beispiel legen wir die Seite der Liste als Startseite fest. Bei einem typischen Add-In würden Sie allerdings wahrscheinlich auf Ihre eigene UI auf der Webprojektseite verweisen.</span><span class="sxs-lookup"><span data-stu-id="66d86-p109">Replace  _AddInProjectName_ with the name of your add-in project, such asSharePointAddIn4/Lists/List1. For this example, we're setting the start page to the list's page. However, in a typical add-in, you'd likely point to your own UI on the web project page.</span></span>
    
 

### <a name="to-run-and-test-event-handler-debugging"></a><span data-ttu-id="66d86-154">So führen Sie das Debuggen des Ereignishandlers aus und testen es</span><span class="sxs-lookup"><span data-stu-id="66d86-154">To run and test event handler debugging</span></span>


1. <span data-ttu-id="66d86-155">Schließen Sie, falls noch nicht geschehen, das im früheren Verlauf dieses Artikels beschriebene Verfahren **So konfigurieren Sie das SharePoint-Add-In-Projekt in Visual Studio** ab.</span><span class="sxs-lookup"><span data-stu-id="66d86-155">If you haven't done so already, complete the **To configure the SharePoint Add-in project in Visual Studio** procedure earlier in this article.</span></span>
    
 
2. <span data-ttu-id="66d86-156">Öffnen Sie im Webprojekt den Remoteereignisempfänger-Dienst (RemoteEventReceiver1.svc), und fügen Sie dann in der  `ProcessEvent()`-Methode in eine beliebige Codezeile einen Haltepunkt ein.</span><span class="sxs-lookup"><span data-stu-id="66d86-156">In the web project, open the remote event receiver service (RemoteEventReceiver1.svc), and then add a breakpoint to any line of code inside the  `ProcessEvent()` method.</span></span>
    
 
3. <span data-ttu-id="66d86-157">Drücken Sie **F5**, um das Projekt auszuführen.</span><span class="sxs-lookup"><span data-stu-id="66d86-157">Choose the **F5** key to run the project.</span></span>
    
 
4. <span data-ttu-id="66d86-158">Wählen Sie die Schaltfläche **Neues Element hinzufügen** aus, um der Liste ein neues Element hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="66d86-158">Choose the **+ New item** button to add an item to the list.</span></span>
    
 
5. <span data-ttu-id="66d86-159">Geben Sie für das Element eine Bezeichnung an, und wählen Sie dann die Schaltfläche **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="66d86-159">Provide a title for the item, and then choose the **Save** button.</span></span>
    
    <span data-ttu-id="66d86-160">Der Haltepunkt, den Sie zum Remoteereignisempfänger hinzugefügt haben, wird erreicht, was bestätigt, dass Sie den Remoteereignisempfänger debuggen.</span><span class="sxs-lookup"><span data-stu-id="66d86-160">The breakpoint that you added to the remote event receiver is hit, verifying that you're debugging the remote event receiver.</span></span>
    
 
6. <span data-ttu-id="66d86-161">Wählen Sie die Taste **F5** aus, um das Projekt weiter auszuführen, und halten Sie dann das Debuggen an, wenn Sie fertig sind.</span><span class="sxs-lookup"><span data-stu-id="66d86-161">Choose the **F5** key to continue to run the project, and then stop debugging when you're done.</span></span>
    
 

## <a name="turn-onoff-the-notification-from-visual-studio-that-event-debugging-needs-to-be-configured"></a><span data-ttu-id="66d86-162">Aktivieren/Deaktivieren der Visual Studio-Benachrichtigung, dass das Ereignisdebugging konfiguriert werden muss</span><span class="sxs-lookup"><span data-stu-id="66d86-162">Turn on/off the notification from Visual Studio that event debugging needs to be configured</span></span>
<span data-ttu-id="66d86-163"><a name="RER_TurnOnOffNotificationsinRER"> </a></span><span class="sxs-lookup"><span data-stu-id="66d86-163"></span></span>

<span data-ttu-id="66d86-p110">Wenn Ihr Projekt ein Remoteereignis umfasst und Sie das Remotedebugging nicht konfiguriert haben, fordert Visual Studio Sie zum Konfigurieren von Remoteereignisdebugging auf (siehe Abbildung 1). Sie können dieses Verhalten ändern, indem Sie das Kontrollkästchen **Mich benachrichtigen, wenn Remoteereignisdebugging nicht konfiguriert ist** auf der Registerkarte **SharePoint** deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="66d86-p110">If you have a remote event in your project and have not configured remote event debugging, Visual Studio prompts you to configure remote event debugging (see Figure 1). You can change this behavior by clearing the **Notify me if remote event debugging is not configured** check box on the **SharePoint** tab.</span></span>
 

 

<span data-ttu-id="66d86-166">**Abbildung 1. Benachrichtigung zum Remoteereignisdebugging**</span><span class="sxs-lookup"><span data-stu-id="66d86-166">**Figure 1. Remote event debugging notification**</span></span>

 

 
![Benachrichtigungen in Remoteereignisempfängern](../../images/SP15Con_Remote_Event_Receivers_FAQ_fig3.png)
 

 

 

## <a name="verify-that-your-service-is-hosted-in-the-service-bus"></a><span data-ttu-id="66d86-168">Sicherstellen, dass der Dienst im Servicebus gehostet wird</span><span class="sxs-lookup"><span data-stu-id="66d86-168">Verify that your service is hosted in the Service Bus</span></span>
<span data-ttu-id="66d86-169"><a name="RER_HowDoIKnowWheteherMyServiceisHostedintheServiceBus"> </a></span><span class="sxs-lookup"><span data-stu-id="66d86-169"></span></span>

<span data-ttu-id="66d86-p111">Nachdem Sie F5 gedrückt und dem Add-In vertraut haben, wechseln Sie in Ihrem Browser zum Servicebus-Namespace. Beispiel: http://mynamespace.servicebus.windows.net und Ihr Endpunkt als Zahl. Abbildung 2 zeigt, wie die Seite aussieht, wenn ein Namespace  *nicht*  aufgeführt ist, d. h. bevor Sie F5 drücken.</span><span class="sxs-lookup"><span data-stu-id="66d86-p111">After you press F5 and trust the add-in, go to the Service Bus namespace in your browser; for example http://mynamespace.servicebus.windows.net, and you should see your endpoint listed as a number. Figure 2 shows what the page looks like when a namespace is  *not*  listed; that is, before you press F5.</span></span>
 

 

<span data-ttu-id="66d86-172">**Abbildung 2. Navigieren zum Servicebus-Namespace**</span><span class="sxs-lookup"><span data-stu-id="66d86-172">**Figure 2. Browsing to the Service Bus namespace**</span></span>

 

 
![Navigieren zum Servicebus-Namespace](../../images/SP15Con_Remote_Event_Receivers_FAQ_fig4.PNG)
 

 

 

## <a name="rer-does-not-hit-the-breakpoint"></a><span data-ttu-id="66d86-174">RER erreicht nicht den Haltepunkt</span><span class="sxs-lookup"><span data-stu-id="66d86-174">RER does not hit the breakpoint</span></span>
<span data-ttu-id="66d86-175"><a name="RER_DoesNotHitTheBreakPoint"> </a></span><span class="sxs-lookup"><span data-stu-id="66d86-175"></span></span>

<span data-ttu-id="66d86-p112">Je nach Ereignis kann das Remoteereignis synchron oder asynchron sein. Bei einem asynchronen Ereignis dauert es möglicherweise einige Sekunden oder mehr, bis der Haltepunkt erreicht wird.</span><span class="sxs-lookup"><span data-stu-id="66d86-p112">Depending on the event, the remote event may be synchronous or asynchronous. It might take a few seconds or more to hit your breakpoint if it is asynchronous.</span></span>
 

 

## <a name="error-there-was-no-endpoint-listening"></a><span data-ttu-id="66d86-178">Fehler: „Es war kein abhörender Endpunkt vorhanden“</span><span class="sxs-lookup"><span data-stu-id="66d86-178">Error: "There was no endpoint listening"</span></span>
<span data-ttu-id="66d86-179"><a name="RER_DoesNotHitTheBreakPoint"> </a></span><span class="sxs-lookup"><span data-stu-id="66d86-179"></span></span>

<span data-ttu-id="66d86-180">Wenn Ihr Handler in der Produktionsumgebung ausgeführt wird, erhalten Sie die folgende Fehlermeldung:</span><span class="sxs-lookup"><span data-stu-id="66d86-180">You get the following error when your handler runs in production:</span></span>
 

 
<span data-ttu-id="66d86-p113">"Das Aufrufen des Remoteereignisempfängers ist fehlgeschlagen. Details: An https:// _{domain}_: _nnnnn_/ _{path}_/AppEventReceiver.svc war kein abhörender Endpunkt vorhanden, der die Nachricht annehmen konnte. Dies wird häufig durch eine fehlerhafte Adresse oder SOAP-Aktion verursacht."  _nnnnn_ steht dabei für einen Port.</span><span class="sxs-lookup"><span data-stu-id="66d86-p113">"The remote event receiver callout failed. Details: There was no endpoint listening at https:// _{domain}_: _nnnnn_/ _{path}_/AppEventReceiver.svc that could accept the message. This is often caused by an incorrect address or SOAP action." where  _nnnnn_ is a port.</span></span>
 

 
<span data-ttu-id="66d86-p114">SharePoint erfordert, dass kein expliziter Port in der URL des Handlers in der Produktion verwendet wird. Dies bedeutet, dass Sie entweder Port 443 für HTTPS (Empfehlung) oder Port 80 für HTTP verwenden müssen.</span><span class="sxs-lookup"><span data-stu-id="66d86-p114">SharePoint requires that there be no explicit port in the URL of the handler in production. This means that you must use either port 443 for HTTPS, which we recommend, or port 80 for HTTP.</span></span> 
 

 

## <a name="error-could-not-establish-trust-relationship-for-the-ssltls-secure-channel-with-authority"></a><span data-ttu-id="66d86-187">Fehler: „Es konnte keine Vertrauensstellung für den sicheren SSL/TLS-Channel mit Autorität eingerichtet werden“</span><span class="sxs-lookup"><span data-stu-id="66d86-187">Error: "Could not establish trust relationship for the SSL/TLS secure channel with authority"</span></span>
<span data-ttu-id="66d86-188"><a name="RER_DoesNotHitTheBreakPoint"> </a></span><span class="sxs-lookup"><span data-stu-id="66d86-188"></span></span>

<span data-ttu-id="66d86-189">Wenn Ihr Handler in der Produktionsumgebung ausgeführt wird, erhalten Sie die folgende Fehlermeldung:</span><span class="sxs-lookup"><span data-stu-id="66d86-189">You get the following error when your handler runs in production:</span></span>
 

 
<span data-ttu-id="66d86-p115">"Das Aufrufen des Remoteereignisempfängers ist fehlgeschlagen. Details: Es konnte keine Vertrauensstellung für den sicheren SSL/TLS-Channel mit Autorität eingerichtet werden.</span><span class="sxs-lookup"><span data-stu-id="66d86-p115">"The remote event receiver callout failed. Details: Could not establish trust relationship for the SSL/TLS secure channel with authority"</span></span>
 

 
<span data-ttu-id="66d86-p116">Wenn sich das Add-In in Microsoft SharePoint Online befindet, der Remoteereignisempfänger-Dienst jedoch lokal ist und wie empfohlen HTTPS verwendet, kann der Server, auf dem der Empfänger gehostet wird, kein selbst signiertes Zertifkat in der Produktion verwenden. Der Server benötigt ein öffentlich akzeptiertes Zertifikat von einer Zertifizierungsstelle. Wenn sich das Add-In in einer lokalen SharePoint-Farm befindet, sind selbst signierte Zertifikate akzeptabel.</span><span class="sxs-lookup"><span data-stu-id="66d86-p116">When the add-in is in Microsoft SharePoint Online, but the remote event receiver service is on-premise, and is using HTTPS as we recommend, the server that is hosting the receiver cannot use a self-signed certificate in production. The server must have a publicly accepted certificate from a certificate authority. If the add-in is in an on-premise SharePoint farm, self-signed certificates are acceptable.</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="66d86-195">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="66d86-195">Additional resources</span></span>
<span data-ttu-id="66d86-196"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="66d86-196"></span></span>


-  [<span data-ttu-id="66d86-197">Behandeln von Ereignissen in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="66d86-197">Handle events in SharePoint Add-ins</span></span>](handle-events-in-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="66d86-198">Debuggen von SharePoint-Remoteereignissen mit Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="66d86-198">Debugging SharePoint remote events using Visual Studio 2012</span></span>](http://blogs.msdn.com/b/officeapps/archive/2013/03/21/update-to-debugging-sharepoint-2013-remote-events-using-visual-studio-2012.aspx)
    
 

