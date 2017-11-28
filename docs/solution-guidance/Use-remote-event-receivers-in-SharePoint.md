---
title: "Verwenden von remote-Ereignisempfänger in SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 713e1b42682a315626e2d121710931c64e86961e
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="use-remote-event-receivers-in-sharepoint"></a>Verwenden von remote-Ereignisempfänger in SharePoint

Verwenden Sie remote-Ereignisempfänger zum Verarbeiten von Ereignissen in der SharePoint-add-in-Objektmodell. Verwenden Sie Ereignisse AppInstalled und AppUninstalling festlegen oder Entfernen von SharePoint-Objekten und anderen Ereignisempfänger, die Ihr Add-in benötigt.

_**Gilt für:** Add-Ins für SharePoint | SharePoint 2013 | SharePoint Online_

>**Wichtige** Ab Januar 2017 SharePoint Online unterstützt Liste Webhooks, die Sie, anstatt verwenden können "-Ed" remote-Ereignisempfänger. Checkout- [Übersicht von SharePoint-Webhooks](https://dev.office.com/sharepoint/docs/apis/webhooks/overview-sharepoint-webhooks) erfahren Sie mehr über Webhooks. Beachten Sie außerdem, dass mehrere Webhook Beispiele aus GitHub Repository [sp-Dev-Beispiele](https://github.com/SharePoint/sp-dev-samples/tree/master/Samples) verfügbar sind.

Das [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) -Beispiel veranschaulicht, wie ein vom Anbieter gehosteten add-in mit einer remote-Ereignisempfänger verwenden, um die AppInstalled und AppUninstalling Ereignisse behandeln. Die Ereignisse AppInstalled und AppUninstalling einrichten und Entfernen von SharePoint-Objekten, die das Add-in verwendet wird, wenn es ausgeführt wird. Darüber hinaus der AppInstalled-Ereignishandler den Ereignishandler ItemAdded einer Liste hinzugefügt. Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:

- Konfigurieren Sie Ihr Add-in auf führen Sie mithilfe des AppInstalled-Ereignisses zum Einrichten von verschiedenen SharePoint-Objekte oder zusätzliche Ereignisempfängern, denen vom Add-in verwendet.
    
- Ersetzen Sie Ereignisempfänger mit Lösungen voll vertrauenswürdiger Code implementiert. Voll vertrauenswürdiger Code-Lösungen können Sie Ereignisempfänger auf dem SharePoint-Server ausführen. Im neuen SharePoint-add-in-Modell da Sie nicht den Ereignisempfänger auf dem SharePoint-Server ausführen können müssen Sie einen remote-Ereignisempfänger auf einem Webserver implementieren.
    
- Empfangen von Benachrichtigungen über nicht mehr auftritt Änderungen in SharePoint. Eine Liste ein neues Element hinzugefügt wird, möchten Sie beispielsweise eine Aufgabe auszuführen.

- Ergänzen Sie die Änderung Log-Lösung. Verwenden das remote-Ereignisempfänger Muster mit einem Change-Log-Muster bietet eine zuverlässigere Architektur für die Verarbeitung aller Änderungen an SharePoint-Inhaltsdatenbanken, Websitesammlungen, Websites oder Listen. Remote-Ereignisempfänger sofort ausgeführt, aber, da sie auf einem Remoteserver ausgeführt werden, treten möglicherweise ein Fehler bei der Kommunikation. Das Muster der Änderung Protokoll wird sichergestellt, dass alle Änderungen für die Verarbeitung verfügbar sind, aber die Anwendung die Änderungen bei der Verarbeitung in der Regel nach einem Zeitplan (beispielsweise einen Zeitgeberauftrag) ausgeführt wird. Dies bedeutet, dass die Änderungen nicht sofort verarbeitet werden. Wenn Sie diese beiden Muster gemeinsam verwenden, stellen Sie sicher, dass Sie einen Mechanismus verwenden, um zu verhindern, dass die gleiche Änderung zweimal verarbeiten. Weitere Informationen finden Sie unter [Abfrage SharePoint Änderungsprotokoll mit komplexer ChangeQuery und komplexer ChangeToken](query-sharepoint-change-log-with-changequery-and-changeToken.md).

**Hinweis**  SharePoint-Hosting-add-ins unterstützt remote-Ereignisempfänger nicht. Um remote-Ereignisempfänger verwenden, müssen Sie eine vom Anbieter gehosteten-add-in verwenden. Sollten Sie remote-Ereignisempfänger nicht verwenden, für die Synchronisierung oder lange ausgeführte Prozesse. Weitere Informationen finden Sie unter [Vorgehensweise: Erstellen eines Ereignisempfängers-Add-in](https://msdn.microsoft.com/library/office/jj220052.aspx).

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zuerst [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

Vor dem Ausführen dieses Add-in führen Sie die folgenden Schritte aus:

1. In den Eigenschaften auf das Projekt Core.EventReceivers stellen Sie sicher, dass **Handle App Installed** und **App-Deinstallation behandeln** auf **True**festgelegt ist. **Handle App Installed** und **App-Deinstallation behandeln** auf **True** festlegen, erstellt einen WCF-Dienst, der den Ereignishandler für das Ereignis **AppInstalled** und **AppUninstalling** definiert. Klicken Sie im Core.EventReceivers öffnen Sie das Kontextmenü (Rechtsklick) auf AppManifest.xml, und wählen Sie **Eigenschaften**. Zeigen Sie auf der remote-Ereignisempfänger, der die **AppInstalled** und **AppUninstalling** Ereignisse behandelt, die **InstalledEventEndpoint** und **UninstallingEventEndpoint** .
    
2. Anfügen eines remote-Ereignisempfängers zu einem Objekt in der Hostwebsite in der Regel erfordert Berechtigung **Verwalten** für dieses Objekt nur. Beispielsweise erfordert beim Anfügen eines Ereignisempfängers zu einer vorhandenen Liste das Add-in Berechtigung in der **Liste** nur **Verwalten** . In diesem Codebeispiel erfordert **Verwalten** von Berechtigungen auf dem **Web** , da es eine Liste hinzugefügt und ein Feature auf dem hostweb aktiviert. So legen Sie fest Verwalten von Berechtigungen im Web:
    
    1. Klicken Sie mit der Doppelklicken auf Core.EventReceivers\AppManifest.xml.
    
    2. Wählen Sie **Berechtigungen**aus.
    
    3. Stellen Sie sicher, dass der **Bereich** **Web**festgelegt ist und **die Berechtigung** zum **Verwalten**festgelegt ist.
    
3. Um dieses Codebeispiel auszuführen, benötigen Sie ein Azure-Abonnement. Um für eine Testversion zu registrieren, finden Sie unter [kostenlose einmonatige Testversion](http://azure.microsoft.com/en-us/pricing/free-trial/).
    
4. Erstellen einer Azure Servicebus-Namespace mit ACS-Unterstützung.
    
    1. Installieren von Azure PowerShell. Weitere Informationen finden Sie unter [Vorgehensweise: Installieren von Azure PowerShell](http://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/#Install).
    
    2. **Azure PowerShell**zu starten.
    
    3. Geben Sie **Add AzureAccount**.
    
    4. Geben Sie Ihre e-Mail-Adresse in das Dialogfeld **Anmelden bei Windows Azure** , und wählen Sie dann auf **Weiter**.
    
    5. Geben Sie Ihr Kennwort ein, und wählen Sie dann auf **Anmelden**.
    
    6. Erstellen Sie einen neuen Servicebus-Namespace, mit dem folgenden PowerShell-Cmdlet.
    
        ```powershell
        New-AzureSBNamespace NamespaceNameRegion -CreateACSNamespace $true -NamespaceType Messaging
        
        ```
    
       Dabei gilt:
    
       -  _NamespaceName_ ist der Name des Azure-Servicebus-Namespace.
    
       -  _Bereich_ ist die Region, die Sie am nächsten. Beispielsweise können Sie **"West US"**eingeben. Sie müssen den Bereichsnamen in doppelte Anführungszeichen einschließen.
    
    7. Geben Sie an der Azure-Verwaltungsportal. Wählen Sie **SERVICE BUS**, und wählen Sie dann den Namespacenamen, den Sie angegeben haben.
    
    8. Wählen Sie die **Verbindungszeichenfolgen zu verwalten**, und klicken Sie dann in der **VERBINDUNGSZEICHENFOLGE ACS**, wählen Sie die Schaltfläche kopieren.
    
    9. Zurück zu Visual Studio.
    
    10. Mit der rechten Maustaste Core.EventReceivers > **Eigenschaften** > **SharePoint**.
    
    11. Wählen Sie **über die Microsoft Azure-Servicebus-debugging aktivieren**.
    
    12. Fügen Sie in **Microsoft Azure-Servicebus-Verbindungszeichenfolge**die ACS-Verbindungszeichenfolge.
    
    13. Wählen Sie **Speichern**aus.
    
5. Führen Sie das Codebeispiel, und führen Sie die folgenden zusätzlichen Schritte aus:
    
    - Klicken Sie auf **Vertrauen** in das **Erteilen von Berechtigungen für die app** -Fenster.
    
    - Schließen Sie das **Erteilen von Berechtigungen für die app** -Fenster.
    
    - Nach Abschluss der Installation des-Add-in und der WCF-Dienst wird der Browser geöffnet.
    
    - Melden Sie sich bei Ihrem Office 365-Website. Die Startseite des Core.EventReceivers-add-Ins wird angezeigt.

## <a name="use-the-coreeventreceivers-add-in"></a>Verwenden des Core.EventReceivers-add-Ins
<a name="sectionSection1"> </a>

Um eine Demo des Codebeispiels Core.EventReceivers finden Sie unter:

1. Führen Sie das Beispiel, und wählen Sie auf der Startseite **zur Website**.
    
2. Wählen Sie **Websiteinhalte**.
    
3. Wählen Sie **Remote Event Receiver Aufträge**.
    
4. Wählen Sie **Neues Element**aus.
    
5. **Titel**Geben Sie **Contoso**, und geben Sie im Feld **Beschreibung** ein **Contoso testen**.
    
6. Zurück zur Liste, und aktualisieren Sie die Seite.
    
7. Stellen Sie sicher, dass die Beschreibung des neu hinzugefügten Elements auf **Contoso Test wurde aktualisiert, indem ReR 192336**aktualisiert wurde, in dem **192336** Zeitstempel ist.
    
In Services/AppEventReceiver.cs implementiert **AppEventReceiver** die **IRemoteEventService** -Schnittstelle. In diesem Codebeispiel stellt eine Implementierung für die **ProcessEvent** -Methode, da sie synchrone Ereignisse verwendet. Wenn Sie asynchrone Ereignisse verwenden, müssen Sie eine Implementierung für die Methode **ProcessOneWayEvent** bereitstellen.

Die **ProcessEvent** behandelt die folgenden remote **SPRemoteEventType** -Ereignisse:

-  **AppInstalled** Ereignisse aus, wenn das Add-in zu installieren. Wenn ein **AppInstalled** -Ereignis eintritt, **ProcessEvent** Anrufe **HandleAppInstalled**.
    
-  **AppUninstalling** Ereignisse aus, wenn das Add-in zu deinstallieren. Wenn ein **AppUninstalling** -Ereignis eintritt, **ProcessEvent** Anrufe **HandleAppUninstalling**. Das **AppUninstalling** -Ereignis wird nur ausgeführt, wenn ein Benutzer das Add-in durch Löschen des Add-Ins aus dem Papierkorb der Website (für Endbenutzer) oder durch das Add-in aus der Liste **Apps im Test** (für Entwickler) entfernen entfernt vollständig.
    
-  **ItemAdded** -Ereignisse, wenn eine Liste ein Element hinzugefügt wird. **ItemAdded** -Ereignis tritt auf, **ProcessEvent** Anrufe **HandleItemAdded**.

**Hinweis**  In den Projekteigenschaften Core.EventReceiver stehen nur Eigenschaften **Handle App Installed** und **App-Deinstallation behandeln** . In diesem Codebeispiel wird veranschaulicht, wie Sie den **ItemAdded** -Ereignis-Handler zu einer Liste auf dem hostweb mithilfe des **AppInstalled** -Ereignisses während der Add-in-Installation hinzufügen.

**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.

```C#
public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
        {

            SPRemoteEventResult result = new SPRemoteEventResult();

            switch (properties.EventType)
            {
                case SPRemoteEventType.AppInstalled:
                    HandleAppInstalled(properties);
                    break;
                case SPRemoteEventType.AppUninstalling:
                    HandleAppUninstalling(properties);
                    break;
                case SPRemoteEventType.ItemAdded:
                    HandleItemAdded(properties);
                    break;
            }


            return result;
        }
```

**HandleAppInstalled** ruft **RemoteEventReceiverManager.AssociateRemoteEventsToHostWeb** in RemoteEventReceiverManager.cs.

```C#
 private void HandleAppInstalled(SPRemoteEventProperties properties)
        {
            using (ClientContext clientContext =
                TokenHelper.CreateAppEventClientContext(properties, false))
            {
                if (clientContext != null)
                {
                    new RemoteEventReceiverManager().AssociateRemoteEventsToHostWeb(clientContext);
                }
            }
        }
```

**AssociateRemoteEventsToHostWeb** erstellt oder ermöglicht verschiedenen SharePoint-Objekten, die das Core.EventReceivers-add-in verwendet. Standarddateispeicherort abweichen. **AssociateRemoteEventsToHostWeb** bewirkt Folgendes:

- Aktiviert das Pushbenachrichtigung-Feature mithilfe von **Web.Features.Add**.
    
- Verwendet das **ClientContext** -Objekt um eine Liste zu suchen. Wenn die Liste nicht vorhanden ist, wird **CreateJobsList** die Liste erstellt. Wenn die Liste vorhanden ist, wird **List.EventReceivers** verwendet, um für einen vorhandenen Ereignisempfänger zu suchen, deren Namen **ItemAddedEvent**ist.
    
- Wenn der **ItemAddedEvent** -Ereignisempfänger nicht vorhanden ist:
    
    - Instanziiert ein neues **komplexer EventReceiverDefinitionCreationInformation** -Objekt zum Erstellen des neuen remote-Ereignisempfängers. Der **ItemAdded** Receiver Ereignistyp wird **EventReceiverDefinitionCreationInformation.EventType**hinzugefügt.
    
    - Die **EventReceiverDefinitionCreationInformation.ReceiverURL** festgelegt auf die URL der der **AppInstalled** remote-Ereignisempfänger.
    
    - Fügt einen neuen-Ereignisempfänger zur Liste mithilfe von **List.EventReceivers.Add**.

```C#
public void AssociateRemoteEventsToHostWeb(ClientContext clientContext)
        {
            // Add Push Notification feature to host web.
            // Not required but it is included here to show you
            // how to activate features.
            clientContext.Web.Features.Add(
                     new Guid("41e1d4bf-b1a2-47f7-ab80-d5d6cbba3092"),
                     true, FeatureDefinitionScope.None);


            // Get the Title and EventReceivers lists.
            clientContext.Load(clientContext.Web.Lists,
                lists => lists.Include(
                    list => list.Title,
                    list => list.EventReceivers).Where
                        (list => list.Title == LIST_TITLE));

            clientContext.ExecuteQuery();

            List jobsList = clientContext.Web.Lists.FirstOrDefault();

            bool rerExists = false;
            if (null == jobsList)
            {
                // List does not exist, create it. 
                jobsList = CreateJobsList(clientContext);

            }
            else
            {
                foreach (var rer in jobsList.EventReceivers)
                {
                    if (rer.ReceiverName == RECEIVER_NAME)
                    {
                        rerExists = true;
                        System.Diagnostics.Trace.WriteLine("Found existing ItemAdded receiver at "
                            + rer.ReceiverUrl);
                    }
                }
            }

            if (!rerExists)
            {
                EventReceiverDefinitionCreationInformation receiver =
                    new EventReceiverDefinitionCreationInformation();
                receiver.EventType = EventReceiverType.ItemAdded;
                
                // Get WCF URL where this message was handled.
                OperationContext op = OperationContext.Current;
                Message msg = op.RequestContext.RequestMessage;
                receiver.ReceiverUrl = msg.Headers.To.ToString();

                receiver.ReceiverName = RECEIVER_NAME;
                receiver.Synchronization = EventReceiverSynchronization.Synchronous;

                // Add the new event receiver to a list in the host web.
                jobsList.EventReceivers.Add(receiver);
                clientContext.ExecuteQuery();

                System.Diagnostics.Trace.WriteLine("Added ItemAdded receiver at " + receiver.ReceiverUrl);
            }
        }
```

Wenn der **Remote Event Receiver Aufträge** Liste ein Element hinzugefügt wird, **ProcessEvent** in AppEventReceiver.svc.cs behandelt das **ItemAdded** -Ereignis und ruft dann **HandleItemAdded**.  **HandleItemAdded** ruft **RemoteEventReceiverManager.ItemAddedToListEventHandler**.  **ItemAddedToListEventHandler** Ruft das Listenelement, das hinzugefügt wurde, und das Listenelement Beschreibung die Zeichenfolge **aktualisiert durch ReR** hinzugefügt.

```C#
 public void ItemAddedToListEventHandler(ClientContext clientContext, Guid listId, int listItemId)
        {
            try
            {
                List photos = clientContext.Web.Lists.GetById(listId);
                ListItem item = photos.GetItemById(listItemId);
                clientContext.Load(item);
                clientContext.ExecuteQuery();

                item["Description"] += "\nUpdated by RER " +
                    System.DateTime.Now.ToLongTimeString();
                item.Update();
                clientContext.ExecuteQuery();
            }
            catch (Exception oops)
            {
                System.Diagnostics.Trace.WriteLine(oops.Message);
            }

        }
```

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [Core.AppEvents.HandlerDelegation](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents.HandlerDelegation)
    
