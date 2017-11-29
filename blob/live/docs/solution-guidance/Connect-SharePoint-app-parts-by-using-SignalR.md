---
title: Verbinden von SharePoint-app-Webparts mithilfe von SignalR
ms.date: 11/03/2017
ms.openlocfilehash: cf9a011fdcca814bf248e4c8412f3232f4ba9d7a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="connect-sharepoint-app-parts-by-using-signalr"></a><span data-ttu-id="54990-102">Verbinden von SharePoint-app-Webparts mithilfe von SignalR</span><span class="sxs-lookup"><span data-stu-id="54990-102">Connect SharePoint app parts by using SignalR</span></span>

<span data-ttu-id="54990-103">Implementieren Sie Echtzeitkommunikation zwischen SharePoint-app-Webparts mithilfe von SignalR.</span><span class="sxs-lookup"><span data-stu-id="54990-103">Implement real-time communication between SharePoint app parts by using SignalR.</span></span>

<span data-ttu-id="54990-104">_**Gilt für:** Add-Ins für SharePoint | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="54990-104">_**Applies to:** add-ins for SharePoint | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="54990-105">Das [Core.ConnectedAppParts](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ConnectedAppParts) -Beispiel zeigt, wie mithilfe eine vom Anbieter gehosteten app eine Nachricht Broker oder Chat Hub senden und Empfangen von Nachrichten aus allen app-Teilen Hubs Chat.</span><span class="sxs-lookup"><span data-stu-id="54990-105">The  [Core.ConnectedAppParts](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ConnectedAppParts) sample shows you how to use a provider-hosted app as a message broker or chat hub to send and receive messages from all app parts connected to the chat hub.</span></span> <span data-ttu-id="54990-106">Verwenden Sie diese Lösung, wenn Sie Ihre SharePoint-Webparts in app-Webparts konvertieren sind und benötigen Ihre app-Webparts miteinander kommunizieren.</span><span class="sxs-lookup"><span data-stu-id="54990-106">Use this solution if you are converting your SharePoint web parts to app parts, and need your app parts to communicate with each other.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="54990-107">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="54990-107">Before you begin</span></span>
<span data-ttu-id="54990-108"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="54990-108"></span></span>

<span data-ttu-id="54990-109">Laden Sie Sie zunächst die [Core.ConnectedAppParts](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ConnectedAppParts) Beispiel-app des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="54990-109">To get started, download the  [Core.ConnectedAppParts](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ConnectedAppParts) sample app from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="connected-app-parts-and-chat-hub-architecture"></a><span data-ttu-id="54990-110">App-Webparts und Chat Hub Architektur verbunden</span><span class="sxs-lookup"><span data-stu-id="54990-110">Connected app parts and chat hub architecture</span></span>
<span data-ttu-id="54990-111"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="54990-111"></span></span>

<span data-ttu-id="54990-112">Abbildung 1 zeigt die verbundenen app-Webparts und Chat Hub Architektur.</span><span class="sxs-lookup"><span data-stu-id="54990-112">Figure 1 shows the connected app parts and chat hub architecture.</span></span>

<span data-ttu-id="54990-113">**Abbildung 1. App-Webparts und Chat Hub Architektur verbunden**</span><span class="sxs-lookup"><span data-stu-id="54990-113">**Figure 1. Connected app parts and chat hub architecture**</span></span>

![Abbildung zeigt die Architektur des Codebeispiels Core.ConnectedAppParts](media/f835d4b8-a84e-4484-8fdf-370d9f308b53.png)

<span data-ttu-id="54990-115">Die verbundenen app-Webparts und Chat Hub-Architektur umfasst die folgenden Komponenten:</span><span class="sxs-lookup"><span data-stu-id="54990-115">The connected app parts and chat hub architecture includes the following components:</span></span>

1. <span data-ttu-id="54990-116">SharePoint-Seiten, die app-Webparts enthalten.</span><span class="sxs-lookup"><span data-stu-id="54990-116">SharePoint pages that include app parts.</span></span> <span data-ttu-id="54990-117">Verwenden Sie die app-Webparts SignalR jQuery-Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="54990-117">The app parts use the SignalR jQuery library.</span></span> <span data-ttu-id="54990-118">Die app-Webparts enthalten JavaScript-Code, das Senden und Empfangen von Nachrichten vom Hub Chat in der vom Anbieter gehosteten-add-in ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="54990-118">The app parts contain JavaScript code, which send and receive messages from the chat hub running in the provider-hosted add-in.</span></span> <span data-ttu-id="54990-119">Jeder app-Webpart muss zuerst mit der Chat-Hub verbinden.</span><span class="sxs-lookup"><span data-stu-id="54990-119">Each app part must first connect to the chat hub.</span></span> <span data-ttu-id="54990-120">Nach dem Herstellen einer Verbindung mit dem Hub Chat, können app-Webparts Nachrichten senden und Empfangen von anderen Teilen verbundenen app.</span><span class="sxs-lookup"><span data-stu-id="54990-120">After connecting to the chat hub, app parts can send and receive messages from other connected app parts.</span></span>
    
2. <span data-ttu-id="54990-121">Eine SignalR Hub-Proxy, der eine Socketverbindung mit dem Chat Hub herstellt.</span><span class="sxs-lookup"><span data-stu-id="54990-121">A SignalR Hub Proxy, which establishes a socket connection to the chat hub.</span></span> <span data-ttu-id="54990-122">Der SignalR Hub-Proxy bereitstellt, Nachrichten zwischen JavaScript-Code für das app-Webpart und den Chat Hub C#-Code.</span><span class="sxs-lookup"><span data-stu-id="54990-122">The SignalR Hub Proxy brokers messages between the app part's JavaScript code and the chat hub's C# code.</span></span>
    
3. <span data-ttu-id="54990-123">Chat-Hub, der die SignalR-Bibliothek zum Weiterleiten von Nachrichten verwendet wird, zum Empfangen von app-Webparts zu senden.</span><span class="sxs-lookup"><span data-stu-id="54990-123">The chat hub, which uses the SignalR library to route messages from sending to receiving app parts.</span></span> <span data-ttu-id="54990-124">In diesem Codebeispiel empfangen alle app-Webparts von Nachrichten aus der Chat bereit, einschließlich des app-Webparts, die die Nachricht gesendet hat.</span><span class="sxs-lookup"><span data-stu-id="54990-124">In this code sample, all app parts receive messages from the chat hub, including the app part that sent the message.</span></span>
    
<span data-ttu-id="54990-125">**Hinweis**  Da app-Webparts in einem IFRAME ausgeführt werden, können nicht Sie JavaScript verwenden, nur für die Kommunikation zwischen app-WebParts.</span><span class="sxs-lookup"><span data-stu-id="54990-125">**Note**  Because app parts run in an IFRAME, you cannot use JavaScript only to communicate between app parts.</span></span> 

## <a name="use-the-coreconnectedappparts-app"></a><span data-ttu-id="54990-126">Verwenden Sie die Core.ConnectedAppParts-app</span><span class="sxs-lookup"><span data-stu-id="54990-126">Use the Core.ConnectedAppParts app</span></span>
<span data-ttu-id="54990-127"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="54990-127"></span></span>

<span data-ttu-id="54990-128">Um eine Demo von zwei Kommunikation mithilfe von SignalR app-Webparts finden Sie unter:</span><span class="sxs-lookup"><span data-stu-id="54990-128">To see a demo of two app parts communicating by using SignalR:</span></span> 

1. <span data-ttu-id="54990-129">Wenn Sie die app ausführen, und die Startseite angezeigt wird, wählen Sie **zurück zur Website**.</span><span class="sxs-lookup"><span data-stu-id="54990-129">When you run the app and the start page is displayed, choose  **Back to Site**.</span></span>
    
2. <span data-ttu-id="54990-130">**Auswählen von** > **Seite hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="54990-130">Choose  **Settings** > **Add a page**.</span></span>
    
3. <span data-ttu-id="54990-131">Klicken Sie im Feld **Name der neuen Seite**Geben Sie **ConnectedAppParts**, und wählen Sie dann auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="54990-131">In  **New page name**, enter  **ConnectedAppParts**, and then choose  **Create**.</span></span>
    
4. <span data-ttu-id="54990-132">Wählen Sie **Einfügen** > **App-Webpart**.</span><span class="sxs-lookup"><span data-stu-id="54990-132">Choose  **Insert** > **App Part**.</span></span>
    
5. <span data-ttu-id="54990-133">Wählen Sie **verbunden Teil – eine** > **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="54990-133">Choose  **Connected Part - One** > **Add**.</span></span>
    
6. <span data-ttu-id="54990-134">Wählen Sie **Einfügen** > **App-Webpart**.</span><span class="sxs-lookup"><span data-stu-id="54990-134">Choose  **Insert** > **App Part**.</span></span>
    
7. <span data-ttu-id="54990-135">Wählen Sie **verbunden Teil – zwei** > **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="54990-135">Choose  **Connected Part - Two** > **Add**.</span></span>
    
8. <span data-ttu-id="54990-136">Wählen Sie **Speichern**aus.</span><span class="sxs-lookup"><span data-stu-id="54990-136">Choose  **Save**.</span></span>
    
9. <span data-ttu-id="54990-137">In **verbunden Teil – eine**, geben Sie **"Hello World" von App-Part 1**ein, und wählen Sie dann auf **Senden**.</span><span class="sxs-lookup"><span data-stu-id="54990-137">In  **Connected Part - One**, enter  **Hello World from App Part 1**, and then choose  **Send**.</span></span>
    
10. <span data-ttu-id="54990-138">Stellen Sie sicher, dass die Meldung **"Hello World" von App-Part 1** in beiden angezeigt wird **verbunden Teil – eine** und **verbunden Teil – zwei** app-WebParts.</span><span class="sxs-lookup"><span data-stu-id="54990-138">Verify that the message  **Hello World from App Part 1** appears in both **Connected Part - One** and **Connected Part - Two** app parts.</span></span>
    
<span data-ttu-id="54990-139">In diesem Codebeispiel enthält das Projekt Core.ConnectedAppParts zwei app-Webparts (ConnectedPartOne und ConnectedPartTwo), die mit der Hostwebsite bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="54990-139">In this code sample, the Core.ConnectedAppParts project contains two app parts (ConnectedPartOne and ConnectedPartTwo) that are deployed to the host web.</span></span> <span data-ttu-id="54990-140">Führen Sie in einem IFRAME ConnectedPartOne und ConnectedPartTwo.</span><span class="sxs-lookup"><span data-stu-id="54990-140">ConnectedPartOne and ConnectedPartTwo run in an IFRAME.</span></span> <span data-ttu-id="54990-141">Die Inhalte von Webseiten für ConnectedPartOne und ConnectedPartTwo werden im Projekt Core.ConnectedAppPartsWeb in Pages\ConnectedPartOne.aspx und Pages\ConnectedPartTwo.aspx definiert.</span><span class="sxs-lookup"><span data-stu-id="54990-141">The web page contents for ConnectedPartOne and ConnectedPartTwo are defined in the Core.ConnectedAppPartsWeb project in Pages\ConnectedPartOne.aspx and Pages\ConnectedPartTwo.aspx.</span></span> <span data-ttu-id="54990-142">Beide Seiten führen Sie in der vom Anbieter gehostete app mit dem Hub Chat (ChatHub.cs) und Verwenden von Inline-JavaScript an:</span><span class="sxs-lookup"><span data-stu-id="54990-142">Both pages run in the provider-hosted app with the chat hub (ChatHub.cs) and use inline JavaScript to:</span></span>

1. <span data-ttu-id="54990-143">Enthalten Sie die SignalR jQuery-Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="54990-143">Include the SignalR jQuery library.</span></span>
    
2. <span data-ttu-id="54990-144">Eine Verbindung mit der SignalR Hub-Proxys unter Verwendung von **connection.chatHub**.</span><span class="sxs-lookup"><span data-stu-id="54990-144">Connect to the SignalR Hub Proxy using  **connection.chatHub**.</span></span> 
    
3. <span data-ttu-id="54990-145">Verwenden Sie **chat.client.broadcastMessage** , um eine Funktion Empfang übermittelte Nachrichten vom Hub Chat definieren.</span><span class="sxs-lookup"><span data-stu-id="54990-145">Use  **chat.client.broadcastMessage** to define a function to receive broadcasted messages sent by the chat hub.</span></span> <span data-ttu-id="54990-146">In diesem Codebeispiel wird der Name des app-Webparts und die Nachricht gesendet wird in der Liste **Diskussion** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="54990-146">In this code sample, the name of the app part and the message being broadcasted is displayed in the **discussion** list.</span></span>
    
4. <span data-ttu-id="54990-147">Starten Sie die Verbindung mit dem Chat Hub mithilfe **$. Connection.hub.start () .done**.</span><span class="sxs-lookup"><span data-stu-id="54990-147">Start the connection to the chat hub using  **$.connection.hub.start().done**.</span></span> <span data-ttu-id="54990-148">Ein Ereignishandler wird definiert, wenn die Verbindung hergestellt wird, klicken Sie auf die **Sendmessage** auf der Schaltfläche Ereignis.</span><span class="sxs-lookup"><span data-stu-id="54990-148">When the connection is established, an event handler is defined on the  **sendmessage** button's click event.</span></span> <span data-ttu-id="54990-149">Dieser Ereignishandler ruft **chat.server.send** , um den Namen des app-Webparts und die Nachricht an den Hub Chat vom Benutzer eingegebene zu senden.</span><span class="sxs-lookup"><span data-stu-id="54990-149">This event handler calls **chat.server.send** to send the name of the app part and the message entered by the user to the chat hub.</span></span>

<span data-ttu-id="54990-150">**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.</span><span class="sxs-lookup"><span data-stu-id="54990-150">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="../Scripts/jquery-1.6.4.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="../Scripts/jquery.signalR-2.0.3.min.js"></script>
    <!--Reference the autogenerated SignalR hub script. -->
    <script src="../signalr/hubs"></script>
    <!--Add script to update the page and send messages.--> 
    <script type="text/javascript">
        $(function () {
            // Declare a proxy to reference the hub. 
            var chat = $.connection.chatHub;
            // Create a function that the hub can call to broadcast messages.
            chat.client.broadcastMessage = function (name, message) {
                // Html encode display name and message. 
                var encodedName = $('<div />').text(name).html();
                var encodedMsg = $('<div />').text(message).html();
                // Add the message to the page. 
                $('#discussion').append('<li><strong>' + encodedName
                    + '</strong>:&amp;nbsp;&amp;nbsp;' + encodedMsg + '</li>');
            };
            // Set initial focus to message input box.  
            $('#message').focus();
            // Start the connection.
            $.connection.hub.start().done(function () {
                $('#sendmessage').click(function () {
                    // Call the Send method on the hub. 
                    chat.server.send($('#displayname').val(), $('#message').val());
                    // Clear text box and reset focus for next comment. 
                    $('#message').val('').focus();
                });
            });
        });
    </script>
```

<span data-ttu-id="54990-151">Wenn der Inline-JavaScript-Code in ConnectedPartOne.aspx **chat.server.send**ausgeführt wird, wird die Methode **Send** in ChatHub.cs aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="54990-151">When the inline JavaScript code in ConnectedPartOne.aspx runs  **chat.server.send**, a call is made to the  **Send** method in ChatHub.cs.</span></span> <span data-ttu-id="54990-152">Die Methode **Send** in ChatHub.cs das Senden app-Webpart Name und die Nachricht empfängt, und klicken Sie dann die Informationen zu allen verbundenen app-Webparts mithilfe von **Clients.All.broadcastMessage**überträgt.</span><span class="sxs-lookup"><span data-stu-id="54990-152">The **Send** method in ChatHub.cs receives the broadcasting app part's name and the message, and then broadcasts the information to all connected app parts by using **Clients.All.broadcastMessage**.</span></span>  <span data-ttu-id="54990-153">**Clients.All.broadcastMessage** Ruft die JavaScript-Funktion (in allen verbundenen app-Webparts), die mithilfe von **chat.client.broadcastMessage**definiert wurde.</span><span class="sxs-lookup"><span data-stu-id="54990-153">**Clients.All.broadcastMessage** calls the JavaScript function (in all connected app parts) that was defined by using **chat.client.broadcastMessage**.</span></span>

```C#
 public void Send(string name, string message)
        {
            // Call the broadcastMessage method to update the app parts.
            Clients.All.broadcastMessage(name, message);
        }
```

<span data-ttu-id="54990-154">**Wichtige**  In diesem Codebeispiel erhalten alle app-Webparts Hubs Chat aller Nachrichten, die über den Hub Chat.</span><span class="sxs-lookup"><span data-stu-id="54990-154">**Important**  In this code sample, all app parts connected to the chat hub receive all messages sent through the chat hub.</span></span> <span data-ttu-id="54990-155">Erwägen Sie das Filtern von Nachrichten basierend auf ID für eine Sitzung, um zu bestimmen, welche app-Webparts, welche Nachrichten empfangen sollen.</span><span class="sxs-lookup"><span data-stu-id="54990-155">Consider filtering messages based on session ID to determine which app parts should receive which messages.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="54990-156">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="54990-156">Additional resources</span></span>
<span data-ttu-id="54990-157"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="54990-157"></span></span>

-  [<span data-ttu-id="54990-158">Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen</span><span class="sxs-lookup"><span data-stu-id="54990-158">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="54990-159">Einführung in die SignalR</span><span class="sxs-lookup"><span data-stu-id="54990-159">Introduction to SignalR</span></span>](http://www.asp.net/signalr/overview/getting-started/introduction-to-signalr)
    
-  [<span data-ttu-id="54990-160">Lernprogramm: Erste Schritte mit SignalR 2</span><span class="sxs-lookup"><span data-stu-id="54990-160">Tutorial: Getting Started with SignalR 2</span></span>](http://www.asp.net/signalr/overview/getting-started/tutorial-getting-started-with-signalr)
    
