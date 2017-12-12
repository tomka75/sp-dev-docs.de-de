---
title: Verbinden von SharePoint-app-Webparts mithilfe von SignalR
ms.date: 11/03/2017
ms.openlocfilehash: 0219f20e399522c1b41b093fe23f2480b4273822
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="connect-sharepoint-app-parts-by-using-signalr"></a>Verbinden von SharePoint-app-Webparts mithilfe von SignalR

Implementieren Sie Echtzeitkommunikation zwischen SharePoint-app-Webparts mithilfe von SignalR.

_**Gilt für:** Add-Ins für SharePoint | SharePoint 2013 | SharePoint Online_

Das [Core.ConnectedAppParts](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ConnectedAppParts) -Beispiel zeigt, wie mithilfe eine vom Anbieter gehosteten app eine Nachricht Broker oder Chat Hub senden und Empfangen von Nachrichten aus allen app-Teilen Hubs Chat. Verwenden Sie diese Lösung, wenn Sie Ihre SharePoint-Webparts in app-Webparts konvertieren sind und benötigen Ihre app-Webparts miteinander kommunizieren.

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zunächst die [Core.ConnectedAppParts](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ConnectedAppParts) Beispiel-app des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

## <a name="connected-app-parts-and-chat-hub-architecture"></a>App-Webparts und Chat Hub Architektur verbunden
<a name="sectionSection1"> </a>

Abbildung 1 zeigt die verbundenen app-Webparts und Chat Hub Architektur.

**Abbildung 1. App-Webparts und Chat Hub Architektur verbunden**

![Abbildung zeigt die Architektur des Codebeispiels Core.ConnectedAppParts](media/f835d4b8-a84e-4484-8fdf-370d9f308b53.png)

Die verbundenen app-Webparts und Chat Hub-Architektur umfasst die folgenden Komponenten:

1. SharePoint-Seiten, die app-Webparts enthalten. Verwenden Sie die app-Webparts SignalR jQuery-Bibliothek. Die app-Webparts enthalten JavaScript-Code, das Senden und Empfangen von Nachrichten vom Hub Chat in der vom Anbieter gehosteten-add-in ausgeführt. Jeder app-Webpart muss zuerst mit der Chat-Hub verbinden. Nach dem Herstellen einer Verbindung mit dem Hub Chat, können app-Webparts Nachrichten senden und Empfangen von anderen Teilen verbundenen app.
    
2. Eine SignalR Hub-Proxy, der eine Socketverbindung mit dem Chat Hub herstellt. Der SignalR Hub-Proxy bereitstellt, Nachrichten zwischen JavaScript-Code für das app-Webpart und den Chat Hub C#-Code.
    
3. Chat-Hub, der die SignalR-Bibliothek zum Weiterleiten von Nachrichten verwendet wird, zum Empfangen von app-Webparts zu senden. In diesem Codebeispiel empfangen alle app-Webparts von Nachrichten aus der Chat bereit, einschließlich des app-Webparts, die die Nachricht gesendet hat.
    
> [!NOTE] 
> Da app-Webparts in einem IFRAME ausgeführt werden, können nicht Sie JavaScript verwenden, nur für die Kommunikation zwischen app-WebParts. 

## <a name="use-the-coreconnectedappparts-app"></a>Verwenden Sie die Core.ConnectedAppParts-app
<a name="sectionSection2"> </a>

Um eine Demo von zwei Kommunikation mithilfe von SignalR app-Webparts finden Sie unter: 

1. Wenn Sie die app ausführen, und die Startseite angezeigt wird, wählen Sie **zurück zur Website**.
    
2. **Auswählen von** > **Seite hinzufügen**.
    
3. Klicken Sie im Feld **Name der neuen Seite**Geben Sie **ConnectedAppParts**, und wählen Sie dann auf **Erstellen**.
    
4. Wählen Sie **Einfügen** > **App-Webpart**.
    
5. Wählen Sie **verbunden Teil – eine** > **Hinzufügen**.
    
6. Wählen Sie **Einfügen** > **App-Webpart**.
    
7. Wählen Sie **verbunden Teil – zwei** > **Hinzufügen**.
    
8. Wählen Sie **Speichern**aus.
    
9. In **verbunden Teil – eine**, geben Sie **"Hello World" von App-Part 1**ein, und wählen Sie dann auf **Senden**.
    
10. Stellen Sie sicher, dass die Meldung **"Hello World" von App-Part 1** in beiden angezeigt wird **verbunden Teil – eine** und **verbunden Teil – zwei** app-WebParts.
    
In diesem Codebeispiel enthält das Projekt Core.ConnectedAppParts zwei app-Webparts (ConnectedPartOne und ConnectedPartTwo), die mit der Hostwebsite bereitgestellt werden. Führen Sie in einem IFRAME ConnectedPartOne und ConnectedPartTwo. Die Inhalte von Webseiten für ConnectedPartOne und ConnectedPartTwo werden im Projekt Core.ConnectedAppPartsWeb in Pages\ConnectedPartOne.aspx und Pages\ConnectedPartTwo.aspx definiert. Beide Seiten führen Sie in der vom Anbieter gehostete app mit dem Hub Chat (ChatHub.cs) und Verwenden von Inline-JavaScript an:

1. Enthalten Sie die SignalR jQuery-Bibliothek.
    
2. Eine Verbindung mit der SignalR Hub-Proxys unter Verwendung von **connection.chatHub**. 
    
3. Verwenden Sie **chat.client.broadcastMessage** , um eine Funktion Empfang übermittelte Nachrichten vom Hub Chat definieren. In diesem Codebeispiel wird der Name des app-Webparts und die Nachricht gesendet wird in der Liste **Diskussion** angezeigt.
    
4. Starten Sie die Verbindung mit dem Chat Hub mithilfe **$. Connection.hub.start () .done**. Ein Ereignishandler wird definiert, wenn die Verbindung hergestellt wird, klicken Sie auf die **Sendmessage** auf der Schaltfläche Ereignis. Dieser Ereignishandler ruft **chat.server.send** , um den Namen des app-Webparts und die Nachricht an den Hub Chat vom Benutzer eingegebene zu senden.

> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

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

Wenn der Inline-JavaScript-Code in ConnectedPartOne.aspx **chat.server.send**ausgeführt wird, wird die Methode **Send** in ChatHub.cs aufgerufen. Die Methode **Send** in ChatHub.cs das Senden app-Webpart Name und die Nachricht empfängt, und klicken Sie dann die Informationen zu allen verbundenen app-Webparts mithilfe von **Clients.All.broadcastMessage**überträgt.  **Clients.All.broadcastMessage** Ruft die JavaScript-Funktion (in allen verbundenen app-Webparts), die mithilfe von **chat.client.broadcastMessage**definiert wurde.

```C#
 public void Send(string name, string message)
        {
            // Call the broadcastMessage method to update the app parts.
            Clients.All.broadcastMessage(name, message);
        }
```

**Wichtige**  In diesem Codebeispiel erhalten alle app-Webparts Hubs Chat aller Nachrichten, die über den Hub Chat. Erwägen Sie das Filtern von Nachrichten basierend auf ID für eine Sitzung, um zu bestimmen, welche app-Webparts, welche Nachrichten empfangen sollen.

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [Einführung in die SignalR](http://www.asp.net/signalr/overview/getting-started/introduction-to-signalr)
    
-  [Lernprogramm: Erste Schritte mit SignalR 2](http://www.asp.net/signalr/overview/getting-started/tutorial-getting-started-with-signalr)
    
