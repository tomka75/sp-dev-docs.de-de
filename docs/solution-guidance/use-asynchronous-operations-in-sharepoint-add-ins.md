---
title: "Verwenden Sie asynchrone Vorgänge in SharePoint-Add-ins"
ms.date: 11/03/2017
ms.openlocfilehash: c2144297453a47ae4b4ee718b5a9682181f20f5e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="use-asynchronous-operations-in-sharepoint-add-ins"></a>Verwenden Sie asynchrone Vorgänge in SharePoint-Add-ins

Implementieren Sie asynchrone Vorgänge in SharePoint-Add-ins mithilfe von Microsoft Azure WebJobs.

_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

Das [Core.QueueWebJobUsage](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.QueueWebJobUsage) -Beispiel zeigt, wie Sie erstellen und Ausführen von asynchrone Vorgänge mithilfe von vom Anbieter gehosteten-add-ins und Azure WebJobs in Office 365.

Mit dieser Lösung können:

- Verbessern der Leistung von Ihrer remote-Ereignisempfänger.
    
- Migrieren zu SharePoint Online, und implementieren Sie die gleiche Timer-Job-Funktionalität, die Sie in Ihrer lokalen SharePoint-Umgebung kommuniziert. 
    
- Implementieren Sie langer Vorgänge, die für Ihre SharePoint-Umgebung ausgeführt werden soll. Beispiel:
    
    -  **AppInstalled** Ereignisse, die länger als das Timeoutintervall 30 Sekunden ausgeführt. Asynchrone Prozesse sind in Add-in-Ereignishandler vorhanden. Weitere Informationen finden Sie unter [Behandeln von Ereignissen in SharePoint-Add-ins](http://msdn.microsoft.com/library/c050d056-8548-4496-a053-016779d723d9%28Office.15%29.aspx) und [Erstellen Sie ein Add-in - Ereignisempfänger in SharePoint-Add-ins](http://msdn.microsoft.com/library/f40c910f-12a2-4caa-8e91-c7a61ae540db%28Office.15%29.aspx).
    
    - Benutzerdefinierte provisioning von Websitesammlungen.
    
    - Vorgänge, die zum Synchronisieren von Daten zwischen Office 365 und die lokale-Systeme.
    
    - Vorgänge, die komplexe Berechnungen auszuführen.
    
Das folgende Diagramm zeigt eine allgemeine Architektur von erforderlichen Komponenten und der Verarbeitungsablauf zwischen diesen Komponenten aus, wenn eine asynchrone Operation ausgeführt wird.

![Diagramm des Datenflusses von asynchrone Vorgänge. Das SharePoint-add-in aufgerufen, die vom Anbieter gehosteten Add-in, die eine Nachricht an die Warteschlange der Azure-Speicher hinzugefügt. Ein Azure WebJob verarbeitet die Nachricht und führt die entsprechende Aktion auf der SharePoint-Website.](media/use-asynchronous-operations-in-sharepoint-add-ins/a4abdcc1-504c-46d7-9f6d-ea209d994605.png)

Asynchrone Vorgänge in Ihr Add-in vom Anbieter gehosteten mithilfe von Azure WebJobs zu implementieren:

1. Benutzer führen Sie das Add-in in SharePoint Online bereitgestellt.
    
2. Das Add-in vom Anbieter gehosteten bietet der Azure-WebJob erforderlichen Eingabeparameter und fügt dann eine neue Nachricht an die Warteschlange Azure-Speicher.
    
3. Die Warteschlange Azure Storage löst ein Ereignis in einer fortlaufend ausgeführten Azure WebJob, mit der Verarbeitung der neuen Nachricht.
    
4. Der Azure-WebJob führt benutzerdefinierte Geschäftslogik für Ihre SharePoint Online-Website. 
    
> [!NOTE] 
> Hinzufügen einer Nachricht an die Warteschlange Azure Storage verwendet einen anderen Prozess aus dem Prozess, der die WebJob Azure ausgeführt wird. Ihr Add-In kann daher asynchrone Vorgänge durch Hinzufügen von neuen Nachrichten an die Warteschlange mit einem Prozess, und klicken Sie dann mithilfe der Azure-WebJob zum Verarbeiten von Nachrichten in einem anderen Prozess implementieren. 

## <a name="before-you-begin"></a>Bevor Sie beginnen:

Zum Einstieg laden [Core.QueueWebJobUsage](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.QueueWebJobUsage) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub, und klicken Sie dann ein Azure-Konto erstellen, Hinzufügen von Details zu diesem Konto, und stellen Sie sicher, dass Azure WebJob ausgeführt wird.

So erstellen Sie ein Azure Storage Konto Zugriff auf die Warteschlange Azure-Speicher

1. Melden Sie sich bei Ihrem Microsoft [Azure-Verwaltungsportal](https://manage.windowsazure.com).
    
2. Wählen Sie **neue** > **Datendienste** > **Speicher** > **schnell zu erstellen**.
    
3. Geben Sie in **URL**-Namen Ihrer Domäne aus. Geben Sie beispielsweise **"Contoso"**aus. 
    
4. Wählen Sie in **Standort/AFFINITÄT Gruppe**einen geeigneten Speicherort.
    
5. Wählen Sie bei der **Replikation** **Georedundantes**. 
    
6. Wählen Sie **die Speicherung Konto erstellen**.
    
Details zu Ihrer neu erstellten Speicher-Konto hinzufügen:

1. Wenn das Konto Azure Storage erstellt wird, wählen Sie **ZUGRIFFSTASTEN verwalten**.
    
2. Kopieren Sie unter **Zugriffstasten verwalten**den **Speicher-Kontonamen** und **PRIMÄRSCHLÜSSEL ACCESS**.
    
3. Die Client-ID, geheimer Clientschlüssel und Ihre Kontoinformationen Azure-Speicher auf einige der Konfigurationsdateien anwenden. 
    
4. Hilfsprogramm Project\Core.QueueWebJobUsage.Console.SendMessage öffnen Sie Program.cs und geben Sie die URL der Website im Feld **SiteUrl** .
    
5. In den **Eigenschaften** auf die Core.QueueWebJobUsage.Job **Lokale Kopie** auf **True** festgelegt auf die Verweise **Microsoft.SharePoint.Client** und **Microsoft.SharePoint.Client.Runtime** . Durch Festlegen **Lokale Kopie** auf **True** Kopien der referenzierten Assemblys in Azure, damit der Azure-WebJob die Verweise auf die folgenden Assemblys auflösen können.
    
6. Bereitstellen der Azure WebJob. Weitere Informationen finden Sie unter [Bereitstellen eines Projekts WebJobs](https://azure.microsoft.com/documentation/articles/websites-dotnet-deploy-webjobs/#deploy). 
    
So überprüfen, dass Ihre WebJob Azure ausgeführt wird:

1. Melden Sie sich bei Ihrem [Azure-Verwaltungsportal](https://manage.windowsazure.com).
    
2. Wählen Sie **Web-apps**, und wählen Sie dann den Microsoft Azure-Websites, die Sie eingegeben haben. 
    
3. Wählen Sie **WEBJOBS**.
    
4. Überprüfen Sie, ob Ihre Azure WebJob in der Liste angezeigt wird, und **Zeitplan** auf **kontinuierlich ausgeführt wird**.
    
5. Wählen Sie auf **Konfigurieren**.
    
6. Erstellen Sie in den **Einstellungen für Add-Ins**neue Add-in-Einstellungen für **ClientId** und **ClientSecret**. Kopieren Sie die **ClientId** **ClientSecret** -Schlüssel / Wert-Paare aus der Datei Core.QueueWebJobUsage.Job\app.config.
    
7. Erstellen Sie in **Verbindungszeichenfolgen**neue Verbindungszeichenfolgen für **AzureWebJobsDashboard** und **AzureWebJobsStorage**. Kopieren Sie die **AzureWebJobsDashboard** und **AzureWebJobsStorage** Schlüssel (Name) und den Wert-Paare aus der Datei Core.QueueWebJobUsage.Job\app.config, und legen Sie den Typ klicken Sie dann auf **Benutzerdefiniert**.
    
8. Wählen Sie **Speichern**aus.

### <a name="apply-configuration-settings"></a>Anwenden von Konfigurationseinstellungen

Verwenden Sie die Informationen in der folgenden Tabelle, um Konfigurationseinstellungen für die Core.QueueWebJobUsage Visual Studio-Projektmappe gelten.

|**Dateispeicherort**|**Schlüssel aktualisieren**|**Informationen zum Aktualisieren**|
|:-----|:-----|:-----|
|Hilfsprogramm Project\Core.QueueWebJobUsage.Console.SendMessage\app.config| **StorageConnectionString**| Ersetzen Sie **[Your Account Name]** mit dem Speicher Kontonamen aus dem Azure-Verwaltungsportal kopiert.|
||| Ersetzen Sie **[Your Account Key]** zusammen mit der primären Zugriffstaste aus dem Azure-Verwaltungsportal kopiert.|
|Core.QueueWebJobUsageWeb\web.config| **StorageConnectionString**| Ersetzen Sie **[YourAccountName]** durch den Speicher Kontonamen aus dem Azure-Verwaltungsportal kopiert.|
||| Ersetzen Sie **[YourAccountKey]** zusammen mit der primären Zugriffstaste aus dem Azure-Verwaltungsportal kopiert.|
|Core.QueueWebJobUsage.Job\app.config| **StorageConnectionString**| Ersetzen Sie **[YourAccountName]** durch den Speicher Kontonamen aus dem Azure-Verwaltungsportal kopiert.|
||| Ersetzen Sie **[YourAccountKey]** zusammen mit der primären Zugriffstaste aus dem Azure-Verwaltungsportal kopiert.|
|| **ClientId**| Ersetzen Sie **[Ihr Add-in - ID]** durch die Client-ID aus der Core.QueueWebJobUsageWeb\web.config kopiert.|
|| **ClientSecret**| Ersetzen Sie **[Ihr Add-in - Clientschlüssel]** mit dem geheimen Clientschlüssel aus der Core.QueueWebJobUsageWeb\web.config kopiert.|
|| **AzureWebJobsDashboard**| Ersetzen Sie **[YourAccount]** durch den Speicher Kontonamen aus dem Azure-Verwaltungsportal kopiert.|
||| Ersetzen Sie **[YourKey]** zusammen mit der primären Zugriffstaste aus dem Azure-Verwaltungsportal kopiert.|
|| **AzureWebJobsStorage**| Ersetzen Sie **[YourAccount]** durch den Speicher Kontonamen aus dem Azure-Verwaltungsportal kopiert.|
||| Ersetzen Sie **[YourKey]** zusammen mit der primären Zugriffstaste aus dem Azure-Verwaltungsportal kopiert.|

> [!NOTE] 
> Stellen Sie **ClientId** und den **ClientSecret** in Core.QueueWebJobUsageWeb ruft aktualisiert, beispielsweise wenn Sie die Versionsnummer in der Datei AppManifest.xml erhöhen sicher, dass Sie **ClientId** und in den **ClientSecret** Aktualisieren der Core.QueueWebJobUsage.Job\app.config.

## <a name="using-the-corequeuewebjobusage-add-in"></a>Mithilfe des Core.QueueWebJobUsage-add-Ins

Die folgende Tabelle beschreibt die Visual Studio-Projekte in der Projektmappe Core.QueueWebJobUsage.

|**Visual Studio-Projekt**|**Beschreibung**|
|:-----|:-----|
|Core.QueueWebJobUsage|Ihre SharePoint-Add-in-Projekt. Die folgenden Berechtigungen sind erforderlich:<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>AllowAppOnlyPolicy</p></li><li><p>Vollzugriff-Berechtigungen für das Web.</p></li></ul>|
|Core.QueueWebJobUsage.Common|Enthält die Geschäftsobjekte und Code für die Geschäftslogik &mdash; wie Methoden zum Hinzufügen von Nachrichten an die Speicherwarteschlange &mdash; für diese Lösung. Dieses Projekt ist Freigabe von Geschäftsobjekten und zwischen verschiedenen Projekten Geschäftslogik enthalten. Sie können diese nicht in der Implementierung erforderlich.|
|Core.QueueWebJobUsage.Job|Der Azure-WebJob, der ausgeführt wird, wenn eine neue Nachricht an die Warteschlange Azure Storage hinzugefügt wird. Dieses Projekt enthält Ihre benutzerdefinierten Code für die Geschäftslogik. |
|Core.QueueWebJobUsageWeb|Das vom Anbieter gehosteten add-in, das die Benutzeroberfläche für das Projekt Core.QueueWebJobUsage enthält. |
|Hilfsprogramm Project\Core.QueueWebJobUsage.Console.SendMessage|Ein Hilfsprogramm-Projekt, das die Kontoinformationen Speicher und die Warteschlange Erstellungsprozess überprüfen und zum Senden von Nachrichten zur Verarbeitung an die Warteschlange, ohne die gesamte in diesem Artikel beschriebene Lösung einrichten verwendet werden kann. |

Wenn Sie das Codebeispiel Core.QueueWebJobUsage ausführen, die vom Anbieter gehosteten add-in angezeigt wird und zwei Schaltflächen angezeigt: **Vorgang synchrone** und **asynchrone Operation**. Bei der Auswahl **synchronen Vorgang**simuliert **BtnSync_Click** in Pages\Default.aspx ein synchrone zeitintensiver Vorgang. In diesem Codebeispiel **BtnSync_Click** des aktuellen Threads bis 10 Sekunden Energiesparmodus versetzt, und anschließend wird eine Dokumentbibliothek. Wenn Sie eine **asynchrone Operation**auswählen, führt **BtnAsync_Click** in Pages\Default.aspx Folgendes aus:

1. Ruft den aktuellen Benutzer ab.
    
2. Erstellt ein **SiteModifyRequest** Business-Objekt, das die Daten zum Einschließen in die Nachricht an die Warteschlange Azure-Speicher gespeichert werden. In diesem Codebeispiel enthält die gesendeten Daten den Namen des aktuellen Benutzers und der aktuellen Website-URL.
    
3. Ruft die **SiteManager(). AddAsyncOperationRequestToQueue** um die Nachricht an die Warteschlange Azure Storage hinzuzufügen.
    
> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```C#
protected void btnAsync_Click(object sender, EventArgs e)
        {

            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                // Get the current user.
                var currUser = clientContext.Web.CurrentUser;
                clientContext.Load(currUser);
                clientContext.ExecuteQuery();

                // Create business object, and then add the request to the queue.
                SiteModifyRequest request = new SiteModifyRequest() { RequestorName = currUser.Title, SiteUrl = Page.Request["SPHostUrl"] };
                new SiteManager().AddAsyncOperationRequestToQueue(request,
                                                                  ConfigurationManager.AppSettings["StorageConnectionString"]);

                processViews.ActiveViewIndex = 1;
                lblStatus.Text = "Asynchronous operation to create document library started.";
            }
        }
```

In Core.QueueWebJobUsage.Common, in SiteManager.cs führt **AddAsyncOperationRequestToQueue** Folgendes aus:

1. Erstellt ein [CloudStorageAccount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx) -Objekt mithilfe der **Kontoname** und **AccountKey** Konfigurationsinformationen in der Datei Core.QueueWebJobUsageWeb\web.config.
    
2. Erstellt einen Azure Storage Warteschlange Client mithilfe von [CloudStorageAccount.CreateCloudQueueClient](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.createcloudqueueclient.aspx).
    
3. [CloudQueueClient.GetQueueReference](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueueclient.getqueuereference.aspx) verwendet, um einen Verweis auf die Warteschlange Azure-Speicher mit dem Namen gleich dem Wert, der die **SiteManager.StorageQueueName** Konstante abzurufen.
    
4. Verwendet [CloudQueue.CreateIfNotExists](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.createifnotexists.aspx) die Warteschlange Azure-Speicher zu erstellen, wenn er nicht vorhanden ist.
    
5. Verwendet [CloudQueue.AddMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) , um eine neue Nachricht an die Warteschlange Azure Storage hinzuzufügen. Das Geschäftsobjekt **ModifyRequest aufgefordert** wird in ein Objekt [CloudQueueMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.aspx) serialisiert, die an die Warteschlange Azure Storage hinzugefügt wird.

```C#
public void AddAsyncOperationRequestToQueue(SiteModifyRequest modifyRequest, 
                                                    string storageConnectionString)
        {
            CloudStorageAccount storageAccount =
                                CloudStorageAccount.Parse(storageConnectionString);

            // Get queue or create a new one if one does not exist.
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
            CloudQueue queue = queueClient.GetQueueReference(SiteManager.StorageQueueName);
            queue.CreateIfNotExists();

            // Add a message to queue.
            queue.AddMessage(new CloudQueueMessage(JsonConvert.SerializeObject(modifyRequest)));
        }
```

Nachdem die Nachricht an die Warteschlange der Azure-Speicher hinzugefügt wurde, eine ständig ausgeführten Azure WebJob wartet und klicken Sie dann die neue Nachricht verarbeitet. Der Azure-WebJob ist in Core.QueueWebJobUsage.Job definiert. Wenn der Azure-WebJob ausgeführt wird, wird in Core.QueueWebJobUsage.Job\Program.cs Main erstellt eine neue **JobHost**und ruft dann **RunAndBlock**. Die **JobHost** Koordinaten Aufrufe von Methoden mit dem **QueueTrigger** -Attribut und Überwachungen für Nachrichten auf einer bestimmten Warteschlange markiert. **RunAndBlock** wird sichergestellt, dass der Azure-WebJob kontinuierlich ausgeführt wird, und ruft **ProcessQueueMessage**, also die Methode, die ausgelöst wird, wenn eine neue Nachricht an die Warteschlange der Azure-Speicher hinzugefügt wird. Die Azure WebJobs SDK zuordnet **ProcessQueueMessage** **den Hauptthread** . Weitere Informationen finden Sie unter [Erstellen einer .NET WebJob in Azure-Add-in-Diensts](https://azure.microsoft.com/documentation/articles/websites-dotnet-webjobs-sdk-get-started/).

```C#
static void Main()
        {
            var host = new JobHost();
            // The following code ensures that the WebJob will run continuously.
            host.RunAndBlock();
        }
```

**ProcessQueueMessage** verarbeitet neue Nachrichten, die an die Warteschlange Azure Storage durch hinzugefügt werden:

1. Verwenden das **QueueTrigger** -Attribut angegeben wird, dass **ProcessQueueMessage** ausgelöst werden soll, wenn eine neue Nachricht an die Warteschlange mit dem Namen gleich dem Wert der **SiteManager.StorageQueueName**geschrieben wird.
    
2. Schreiben in die Protokolldatei für die Azure WebJob mithilfe der **Log** -Variable, die als Parameter an **ProcessQueueMessage**übergeben wurde.
    
3. Aufrufen von **SiteManager(). PerformSiteModification** einen Geschäftsprozess langer auf der Website ausführen. In diesem Codebeispiel der Thread um 10 Sekunden Energiesparmodus versetzt wird, und klicken Sie dann eine Dokumentbibliothek erstellt wird.

```C#
public static void ProcessQueueMessage(
            [QueueTrigger(SiteManager.StorageQueueName)] 
            SiteModifyRequest modifyRequest, TextWriter log)
        {
            log.WriteLine(string.Format("{0} '{1}' {2} '{3}'.",
                            "Received new site modification request with URL", 
                            modifyRequest.SiteUrl, 
                            "from person named as ", 
                            modifyRequest.RequestorName));
            
            try
            {
                Uri targetSite = new Uri(modifyRequest.SiteUrl);
                
                // Get the realm for the URL.
                string realm = TokenHelper.GetRealmFromTargetUrl(targetSite);

                // Get the access token for the URL.  
                // Requires this add-in to be registered with the tenant.
                string accessToken = TokenHelper.GetAppOnlyAccessToken(
                                                    TokenHelper.SharePointPrincipal,
                                                    targetSite.Authority, realm).AccessToken;

                // Get client context with access token.
                using (var ctx =
                    TokenHelper.GetClientContextWithAccessToken(
                                                    targetSite.ToString(), accessToken))
                {
                    // Call business logic code.
                    new SiteManager().PerformSiteModification(ctx, modifyRequest);
                }
            }
            catch (Exception ex)
            {
                log.WriteLine(string.Format("Site modification to URL {0} failed with following details.", modifyRequest.SiteUrl));
                log.WriteLine(ex.ToString());
                throw;
            }
        }
```

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

- [Office 365 Development Mustern und Methoden ausgesprochen](Office-365-development-patterns-and-practices-solution-guidance.md).
    
- [Verwenden von remote-Ereignisempfänger in SharePoint](Use-remote-event-receivers-in-SharePoint.md)
    
- [Abfragen von SharePoint-Änderungsprotokoll mit komplexer ChangeQuery und komplexer ChangeToken](query-sharepoint-change-log-with-changequery-and-changeToken.md)
