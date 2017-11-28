---
title: "Verwenden Sie asynchrone Vorgänge in SharePoint-Add-ins"
ms.date: 11/03/2017
ms.openlocfilehash: 3bf311c7084c6dba5e4faecb2ebfbd9edd6e4f86
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="use-asynchronous-operations-in-sharepoint-add-ins"></a><span data-ttu-id="fd484-102">Verwenden Sie asynchrone Vorgänge in SharePoint-Add-ins</span><span class="sxs-lookup"><span data-stu-id="fd484-102">Use asynchronous operations in SharePoint Add-ins</span></span>

<span data-ttu-id="fd484-103">Implementieren Sie asynchrone Vorgänge in SharePoint-Add-ins mithilfe von Microsoft Azure WebJobs.</span><span class="sxs-lookup"><span data-stu-id="fd484-103">Implement asynchronous operations in SharePoint Add-ins by using Microsoft Azure WebJobs.</span></span>

<span data-ttu-id="fd484-104">_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="fd484-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="fd484-105">Das [Core.QueueWebJobUsage](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.QueueWebJobUsage) -Beispiel zeigt, wie Sie erstellen und Ausführen von asynchrone Vorgänge mithilfe von vom Anbieter gehosteten-add-ins und Azure WebJobs in Office 365.</span><span class="sxs-lookup"><span data-stu-id="fd484-105">The [Core.QueueWebJobUsage](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.QueueWebJobUsage) sample shows you how to create and run asynchronous operations by using provider-hosted add-ins and Azure WebJobs in Office 365.</span></span>

<span data-ttu-id="fd484-106">Mit dieser Lösung können:</span><span class="sxs-lookup"><span data-stu-id="fd484-106">Use this solution to:</span></span>

- <span data-ttu-id="fd484-107">Verbessern der Leistung von Ihrer remote-Ereignisempfänger.</span><span class="sxs-lookup"><span data-stu-id="fd484-107">Improve performance of your remote event receivers.</span></span>
    
- <span data-ttu-id="fd484-108">Migrieren zu SharePoint Online, und implementieren Sie die gleiche Timer-Job-Funktionalität, die Sie in Ihrer lokalen SharePoint-Umgebung kommuniziert.</span><span class="sxs-lookup"><span data-stu-id="fd484-108">Migrate to SharePoint Online and implement the same timer job functionality that you had in your SharePoint on-premises environment.</span></span> 
    
- <span data-ttu-id="fd484-109">Implementieren Sie langer Vorgänge, die für Ihre SharePoint-Umgebung ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="fd484-109">Implement long-running operations that you want to run against your SharePoint environment.</span></span> <span data-ttu-id="fd484-110">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="fd484-110">For example:</span></span>
    
    -  <span data-ttu-id="fd484-111">**AppInstalled** Ereignisse, die länger als das Timeoutintervall 30 Sekunden ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="fd484-111">**AppInstalled** events that run longer than the 30-second time-out interval.</span></span> <span data-ttu-id="fd484-112">Asynchrone Prozesse sind in Add-in-Ereignishandler vorhanden.</span><span class="sxs-lookup"><span data-stu-id="fd484-112">There are asynchronous processes in add-in event handlers.</span></span> <span data-ttu-id="fd484-113">Weitere Informationen finden Sie unter [Behandeln von Ereignissen in SharePoint-Add-ins](http://msdn.microsoft.com/library/c050d056-8548-4496-a053-016779d723d9%28Office.15%29.aspx) und [Erstellen Sie ein Add-in - Ereignisempfänger in SharePoint-Add-ins](http://msdn.microsoft.com/library/f40c910f-12a2-4caa-8e91-c7a61ae540db%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd484-113">For more information, see [Handle events in SharePoint Add-ins](http://msdn.microsoft.com/library/c050d056-8548-4496-a053-016779d723d9%28Office.15%29.aspx) and [Create an add-in event receiver in SharePoint Add-ins](http://msdn.microsoft.com/library/f40c910f-12a2-4caa-8e91-c7a61ae540db%28Office.15%29.aspx).</span></span>
    
    - <span data-ttu-id="fd484-114">Benutzerdefinierte provisioning von Websitesammlungen.</span><span class="sxs-lookup"><span data-stu-id="fd484-114">Custom site collection provisioning.</span></span>
    
    - <span data-ttu-id="fd484-115">Vorgänge, die zum Synchronisieren von Daten zwischen Office 365 und die lokale-Systeme.</span><span class="sxs-lookup"><span data-stu-id="fd484-115">Operations that synchronize data between Office 365 and your on-premises systems.</span></span>
    
    - <span data-ttu-id="fd484-116">Vorgänge, die komplexe Berechnungen auszuführen.</span><span class="sxs-lookup"><span data-stu-id="fd484-116">Operations that perform complex calculations.</span></span>
    
<span data-ttu-id="fd484-117">Das folgende Diagramm zeigt eine allgemeine Architektur von erforderlichen Komponenten und der Verarbeitungsablauf zwischen diesen Komponenten aus, wenn eine asynchrone Operation ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="fd484-117">The following diagram shows a high-level architecture of the required components, and the processing flow among those components when an asynchronous operation is performed.</span></span>

![Diagramm des Datenflusses von asynchrone Vorgänge.](media/use-asynchronous-operations-in-sharepoint-add-ins/a4abdcc1-504c-46d7-9f6d-ea209d994605.png)

<span data-ttu-id="fd484-121">Asynchrone Vorgänge in Ihr Add-in vom Anbieter gehosteten mithilfe von Azure WebJobs zu implementieren:</span><span class="sxs-lookup"><span data-stu-id="fd484-121">To implement asynchronous operations in your provider-hosted add-in by using Azure WebJobs:</span></span>

1. <span data-ttu-id="fd484-122">Benutzer führen Sie das Add-in in SharePoint Online bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="fd484-122">Users run the add-in deployed in SharePoint Online.</span></span>
    
2. <span data-ttu-id="fd484-123">Das Add-in vom Anbieter gehosteten bietet der Azure-WebJob erforderlichen Eingabeparameter und fügt dann eine neue Nachricht an die Warteschlange Azure-Speicher.</span><span class="sxs-lookup"><span data-stu-id="fd484-123">The provider-hosted add-in gives input parameters required by the Azure WebJob, and then adds a new message to the Azure Storage queue.</span></span>
    
3. <span data-ttu-id="fd484-124">Die Warteschlange Azure Storage löst ein Ereignis in einer fortlaufend ausgeführten Azure WebJob, mit der Verarbeitung der neuen Nachricht.</span><span class="sxs-lookup"><span data-stu-id="fd484-124">The Azure Storage queue triggers an event in a continuously running Azure WebJob to start processing the new message.</span></span>
    
4. <span data-ttu-id="fd484-125">Der Azure-WebJob führt benutzerdefinierte Geschäftslogik für Ihre SharePoint Online-Website.</span><span class="sxs-lookup"><span data-stu-id="fd484-125">The Azure WebJob runs custom business logic against your SharePoint Online site.</span></span> 
    
<span data-ttu-id="fd484-126">**Hinweis:**  Hinzufügen einer Nachricht an die Warteschlange Azure Storage verwendet einen anderen Prozess aus dem Prozess, der die WebJob Azure ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="fd484-126">**Note:**  Adding a message to the Azure Storage queue uses a different process from the process that runs the Azure WebJob.</span></span> <span data-ttu-id="fd484-127">Ihr Add-In kann daher asynchrone Vorgänge durch Hinzufügen von neuen Nachrichten an die Warteschlange mit einem Prozess, und klicken Sie dann mithilfe der Azure-WebJob zum Verarbeiten von Nachrichten in einem anderen Prozess implementieren.</span><span class="sxs-lookup"><span data-stu-id="fd484-127">Therefore, your add-in can implement asynchronous operations by adding new messages to the queue using one process, and then by using the Azure WebJob to handle those messages in another process.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="fd484-128">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="fd484-128">Before you begin</span></span>

<span data-ttu-id="fd484-129">Zum Einstieg laden [Core.QueueWebJobUsage](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.QueueWebJobUsage) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub, und klicken Sie dann ein Azure-Konto erstellen, Hinzufügen von Details zu diesem Konto, und stellen Sie sicher, dass Azure WebJob ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="fd484-129">To get started, download the [Core.QueueWebJobUsage](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.QueueWebJobUsage) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub, and then create an Azure account, add details to that account, and verify that Azure WebJob is running.</span></span>

<span data-ttu-id="fd484-130">So erstellen Sie ein Azure Storage Konto Zugriff auf die Warteschlange Azure-Speicher</span><span class="sxs-lookup"><span data-stu-id="fd484-130">To create an Azure Storage account to access the Azure storage queue:</span></span>

1. <span data-ttu-id="fd484-131">Melden Sie sich bei Ihrem Microsoft [Azure-Verwaltungsportal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fd484-131">Sign in to your Microsoft [Azure Management Portal](https://manage.windowsazure.com).</span></span>
    
2. <span data-ttu-id="fd484-132">Wählen Sie **neue** > **Datendienste** > **Speicher** > **schnell zu erstellen**.</span><span class="sxs-lookup"><span data-stu-id="fd484-132">Choose  **New** > **Data Services** > **Storage** > **Quick Create**.</span></span>
    
3. <span data-ttu-id="fd484-133">Geben Sie in **URL**-Namen Ihrer Domäne aus.</span><span class="sxs-lookup"><span data-stu-id="fd484-133">In  **URL**, enter your domain name.</span></span> <span data-ttu-id="fd484-134">Geben Sie beispielsweise **"Contoso"**aus.</span><span class="sxs-lookup"><span data-stu-id="fd484-134">For example, enter  **contoso**.</span></span> 
    
4. <span data-ttu-id="fd484-135">Wählen Sie in **Standort/AFFINITÄT Gruppe**einen geeigneten Speicherort.</span><span class="sxs-lookup"><span data-stu-id="fd484-135">In  **LOCATION/AFFINITY GROUP**, choose an appropriate location.</span></span>
    
5. <span data-ttu-id="fd484-136">Wählen Sie bei der **Replikation** **Georedundantes**.</span><span class="sxs-lookup"><span data-stu-id="fd484-136">In  **REPLICATION**, choose  **Geo-Redundant**.</span></span> 
    
6. <span data-ttu-id="fd484-137">Wählen Sie **die Speicherung Konto erstellen**.</span><span class="sxs-lookup"><span data-stu-id="fd484-137">Choose  **CREATE STORAGE ACCOUNT**.</span></span>
    
<span data-ttu-id="fd484-138">Details zu Ihrer neu erstellten Speicher-Konto hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="fd484-138">To add details to your newly created storage account:</span></span>

1. <span data-ttu-id="fd484-139">Wenn das Konto Azure Storage erstellt wird, wählen Sie **ZUGRIFFSTASTEN verwalten**.</span><span class="sxs-lookup"><span data-stu-id="fd484-139">When the Azure Storage account is created, choose  **MANAGE ACCESS KEYS**.</span></span>
    
2. <span data-ttu-id="fd484-140">Kopieren Sie unter **Zugriffstasten verwalten**den **Speicher-Kontonamen** und **PRIMÄRSCHLÜSSEL ACCESS**.</span><span class="sxs-lookup"><span data-stu-id="fd484-140">In  **Manage Access Keys**, copy the  **STORAGE ACCOUNT NAME** and **PRIMARY ACCESS KEY**.</span></span>
    
3. <span data-ttu-id="fd484-141">Die Client-ID, geheimer Clientschlüssel und Ihre Kontoinformationen Azure-Speicher auf einige der Konfigurationsdateien anwenden.</span><span class="sxs-lookup"><span data-stu-id="fd484-141">Apply the client ID, client secret, and your Azure Storage account information to several of the configuration files.</span></span> 
    
4. <span data-ttu-id="fd484-142">Hilfsprogramm Project\Core.QueueWebJobUsage.Console.SendMessage öffnen Sie Program.cs und geben Sie die URL der Website im Feld **SiteUrl** .</span><span class="sxs-lookup"><span data-stu-id="fd484-142">In Helper Project\Core.QueueWebJobUsage.Console.SendMessage, open Program.cs and enter the URL of your site in the  **siteUrl** box.</span></span>
    
5. <span data-ttu-id="fd484-143">In den **Eigenschaften** auf die Core.QueueWebJobUsage.Job **Lokale Kopie** auf **True** festgelegt auf die Verweise **Microsoft.SharePoint.Client** und **Microsoft.SharePoint.Client.Runtime** .</span><span class="sxs-lookup"><span data-stu-id="fd484-143">In  **Properties** on the Core.QueueWebJobUsage.Job, set **Copy Local** to **True** on the **Microsoft.SharePoint.Client** and **Microsoft.SharePoint.Client.Runtime** references.</span></span> <span data-ttu-id="fd484-144">Durch Festlegen **Lokale Kopie** auf **True** Kopien der referenzierten Assemblys in Azure, damit der Azure-WebJob die Verweise auf die folgenden Assemblys auflösen können.</span><span class="sxs-lookup"><span data-stu-id="fd484-144">Setting **Copy Local** to **True** copies the referenced assemblies to Azure so that the Azure WebJob can resolve the references to these assemblies.</span></span>
    
6. <span data-ttu-id="fd484-145">Bereitstellen der Azure WebJob.</span><span class="sxs-lookup"><span data-stu-id="fd484-145">Deploy the Azure WebJob.</span></span> <span data-ttu-id="fd484-146">Weitere Informationen finden Sie unter [Bereitstellen eines Projekts WebJobs](https://azure.microsoft.com/documentation/articles/websites-dotnet-deploy-webjobs/#deploy).</span><span class="sxs-lookup"><span data-stu-id="fd484-146">For more information, see [Deploy a WebJobs project](https://azure.microsoft.com/documentation/articles/websites-dotnet-deploy-webjobs/#deploy).</span></span> 
    
<span data-ttu-id="fd484-147">So überprüfen, dass Ihre WebJob Azure ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="fd484-147">To verify that your Azure WebJob is running:</span></span>

1. <span data-ttu-id="fd484-148">Melden Sie sich bei Ihrem [Azure-Verwaltungsportal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fd484-148">Sign in to your [Azure Management Portal](https://manage.windowsazure.com).</span></span>
    
2. <span data-ttu-id="fd484-149">Wählen Sie **Web-apps**, und wählen Sie dann den Microsoft Azure-Websites, die Sie eingegeben haben.</span><span class="sxs-lookup"><span data-stu-id="fd484-149">Choose  **web apps**, and then choose the Microsoft Azure Websites you entered.</span></span> 
    
3. <span data-ttu-id="fd484-150">Wählen Sie **WEBJOBS**.</span><span class="sxs-lookup"><span data-stu-id="fd484-150">Choose  **WEBJOBS**.</span></span>
    
4. <span data-ttu-id="fd484-151">Überprüfen Sie, ob Ihre Azure WebJob in der Liste angezeigt wird, und **Zeitplan** auf **kontinuierlich ausgeführt wird**.</span><span class="sxs-lookup"><span data-stu-id="fd484-151">Verify that your Azure WebJob appears in the list, and that  **SCHEDULE** is set to **Runs continuously**.</span></span>
    
5. <span data-ttu-id="fd484-152">Wählen Sie auf **Konfigurieren**.</span><span class="sxs-lookup"><span data-stu-id="fd484-152">Choose  **CONFIGURE**.</span></span>
    
6. <span data-ttu-id="fd484-153">Erstellen Sie in den **Einstellungen für Add-Ins**neue Add-in-Einstellungen für **ClientId** und **ClientSecret**.</span><span class="sxs-lookup"><span data-stu-id="fd484-153">In  **add-in settings**, create new add-in settings for  **ClientId** and **ClientSecret**.</span></span> <span data-ttu-id="fd484-154">Kopieren Sie die **ClientId** **ClientSecret** -Schlüssel / Wert-Paare aus der Datei Core.QueueWebJobUsage.Job\app.config.</span><span class="sxs-lookup"><span data-stu-id="fd484-154">Copy the **ClientId** and **ClientSecret** key-value pairs from the Core.QueueWebJobUsage.Job\app.config file.</span></span>
    
7. <span data-ttu-id="fd484-155">Erstellen Sie in **Verbindungszeichenfolgen**neue Verbindungszeichenfolgen für **AzureWebJobsDashboard** und **AzureWebJobsStorage**.</span><span class="sxs-lookup"><span data-stu-id="fd484-155">In  **connection strings**, create new connection strings for  **AzureWebJobsDashboard** and **AzureWebJobsStorage**.</span></span> <span data-ttu-id="fd484-156">Kopieren Sie die **AzureWebJobsDashboard** und **AzureWebJobsStorage** Schlüssel (Name) und den Wert-Paare aus der Datei Core.QueueWebJobUsage.Job\app.config, und legen Sie den Typ klicken Sie dann auf **Benutzerdefiniert**.</span><span class="sxs-lookup"><span data-stu-id="fd484-156">Copy the **AzureWebJobsDashboard** and **AzureWebJobsStorage** key (name) and value pairs from the Core.QueueWebJobUsage.Job\app.config file, and then set the type to **Custom**.</span></span>
    
8. <span data-ttu-id="fd484-157">Wählen Sie **Speichern**aus.</span><span class="sxs-lookup"><span data-stu-id="fd484-157">Choose  **Save**.</span></span>

### <a name="apply-configuration-settings"></a><span data-ttu-id="fd484-158">Anwenden von Konfigurationseinstellungen</span><span class="sxs-lookup"><span data-stu-id="fd484-158">Apply configuration settings</span></span>

<span data-ttu-id="fd484-159">Verwenden Sie die Informationen in der folgenden Tabelle, um Konfigurationseinstellungen für die Core.QueueWebJobUsage Visual Studio-Projektmappe gelten.</span><span class="sxs-lookup"><span data-stu-id="fd484-159">Use the information in the following table to apply configuration settings to the Core.QueueWebJobUsage Visual Studio solution.</span></span>

|<span data-ttu-id="fd484-160">**Dateispeicherort**</span><span class="sxs-lookup"><span data-stu-id="fd484-160">**File location**</span></span>|<span data-ttu-id="fd484-161">**Schlüssel aktualisieren**</span><span class="sxs-lookup"><span data-stu-id="fd484-161">**Key to update**</span></span>|<span data-ttu-id="fd484-162">**Informationen zum Aktualisieren**</span><span class="sxs-lookup"><span data-stu-id="fd484-162">**Value information to update**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="fd484-163">Hilfsprogramm Project\Core.QueueWebJobUsage.Console.SendMessage\app.config</span><span class="sxs-lookup"><span data-stu-id="fd484-163">Helper Project\Core.QueueWebJobUsage.Console.SendMessage\app.config</span></span>| <span data-ttu-id="fd484-164">**StorageConnectionString**</span><span class="sxs-lookup"><span data-stu-id="fd484-164">**StorageConnectionString**</span></span>| <span data-ttu-id="fd484-165">Ersetzen Sie **[Your Account Name]** mit dem Speicher Kontonamen aus dem Azure-Verwaltungsportal kopiert.</span><span class="sxs-lookup"><span data-stu-id="fd484-165">Replace **[Your Account name]** with the storage account name copied from the Azure Management Portal.</span></span>|
||| <span data-ttu-id="fd484-166">Ersetzen Sie **[Your Account Key]** zusammen mit der primären Zugriffstaste aus dem Azure-Verwaltungsportal kopiert.</span><span class="sxs-lookup"><span data-stu-id="fd484-166">Replace **[Your Account Key]** with the primary access key copied from the Azure Management Portal.</span></span>|
|<span data-ttu-id="fd484-167">Core.QueueWebJobUsageWeb\web.config</span><span class="sxs-lookup"><span data-stu-id="fd484-167">Core.QueueWebJobUsageWeb\web.config</span></span>| <span data-ttu-id="fd484-168">**StorageConnectionString**</span><span class="sxs-lookup"><span data-stu-id="fd484-168">**StorageConnectionString**</span></span>| <span data-ttu-id="fd484-169">Ersetzen Sie **[YourAccountName]** durch den Speicher Kontonamen aus dem Azure-Verwaltungsportal kopiert.</span><span class="sxs-lookup"><span data-stu-id="fd484-169">Replace **[YourAccountName]** with the storage account name copied from the Azure Management Portal.</span></span>|
||| <span data-ttu-id="fd484-170">Ersetzen Sie **[YourAccountKey]** zusammen mit der primären Zugriffstaste aus dem Azure-Verwaltungsportal kopiert.</span><span class="sxs-lookup"><span data-stu-id="fd484-170">Replace **[YourAccountKey]** with the primary access key copied from the Azure Management Portal.</span></span>|
|<span data-ttu-id="fd484-171">Core.QueueWebJobUsage.Job\app.config</span><span class="sxs-lookup"><span data-stu-id="fd484-171">Core.QueueWebJobUsage.Job\app.config</span></span>| <span data-ttu-id="fd484-172">**StorageConnectionString**</span><span class="sxs-lookup"><span data-stu-id="fd484-172">**StorageConnectionString**</span></span>| <span data-ttu-id="fd484-173">Ersetzen Sie **[YourAccountName]** durch den Speicher Kontonamen aus dem Azure-Verwaltungsportal kopiert.</span><span class="sxs-lookup"><span data-stu-id="fd484-173">Replace **[YourAccountName]** with the storage account name copied from the Azure Management Portal.</span></span>|
||| <span data-ttu-id="fd484-174">Ersetzen Sie **[YourAccountKey]** zusammen mit der primären Zugriffstaste aus dem Azure-Verwaltungsportal kopiert.</span><span class="sxs-lookup"><span data-stu-id="fd484-174">Replace **[YourAccountKey]** with the primary access key copied from the Azure Management Portal.</span></span>|
|| <span data-ttu-id="fd484-175">**ClientId**</span><span class="sxs-lookup"><span data-stu-id="fd484-175">**ClientId**</span></span>| <span data-ttu-id="fd484-176">Ersetzen Sie **[Ihr Add-in - ID]** durch die Client-ID aus der Core.QueueWebJobUsageWeb\web.config kopiert.</span><span class="sxs-lookup"><span data-stu-id="fd484-176">Replace **[Your Add-in ID]** with the client ID copied from the Core.QueueWebJobUsageWeb\web.config.</span></span>|
|| <span data-ttu-id="fd484-177">**ClientSecret**</span><span class="sxs-lookup"><span data-stu-id="fd484-177">**ClientSecret**</span></span>| <span data-ttu-id="fd484-178">Ersetzen Sie **[Ihr Add-in - Clientschlüssel]** mit dem geheimen Clientschlüssel aus der Core.QueueWebJobUsageWeb\web.config kopiert.</span><span class="sxs-lookup"><span data-stu-id="fd484-178">Replace **[Your Add-in Secret]** with the client secret copied from the Core.QueueWebJobUsageWeb\web.config.</span></span>|
|| <span data-ttu-id="fd484-179">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="fd484-179">**AzureWebJobsDashboard**</span></span>| <span data-ttu-id="fd484-180">Ersetzen Sie **[YourAccount]** durch den Speicher Kontonamen aus dem Azure-Verwaltungsportal kopiert.</span><span class="sxs-lookup"><span data-stu-id="fd484-180">Replace **[YourAccount]** with the storage account name copied from the Azure Management Portal.</span></span>|
||| <span data-ttu-id="fd484-181">Ersetzen Sie **[YourKey]** zusammen mit der primären Zugriffstaste aus dem Azure-Verwaltungsportal kopiert.</span><span class="sxs-lookup"><span data-stu-id="fd484-181">Replace **[YourKey]** with the primary access key copied from the Azure Management Portal.</span></span>|
|| <span data-ttu-id="fd484-182">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="fd484-182">**AzureWebJobsStorage**</span></span>| <span data-ttu-id="fd484-183">Ersetzen Sie **[YourAccount]** durch den Speicher Kontonamen aus dem Azure-Verwaltungsportal kopiert.</span><span class="sxs-lookup"><span data-stu-id="fd484-183">Replace **[YourAccount]** with the storage account name copied from the Azure Management Portal.</span></span>|
||| <span data-ttu-id="fd484-184">Ersetzen Sie **[YourKey]** zusammen mit der primären Zugriffstaste aus dem Azure-Verwaltungsportal kopiert.</span><span class="sxs-lookup"><span data-stu-id="fd484-184">Replace **[YourKey]** with the primary access key copied from the Azure Management Portal.</span></span>|

<span data-ttu-id="fd484-185">**Hinweis:**  Stellen Sie **ClientId** und den **ClientSecret** in Core.QueueWebJobUsageWeb ruft aktualisiert, beispielsweise wenn Sie die Versionsnummer in der Datei AppManifest.xml erhöhen sicher, dass Sie **ClientId** und in den **ClientSecret** Aktualisieren der Core.QueueWebJobUsage.Job\app.config.</span><span class="sxs-lookup"><span data-stu-id="fd484-185">**Note:**  If the  **ClientId** and the **ClientSecret** in Core.QueueWebJobUsageWeb gets updated, for example, when you increment the version number in the AppManifest.xml, make sure you update the **ClientId** and the **ClientSecret** in the Core.QueueWebJobUsage.Job\app.config.</span></span>

## <a name="using-the-corequeuewebjobusage-add-in"></a><span data-ttu-id="fd484-186">Mithilfe des Core.QueueWebJobUsage-add-Ins</span><span class="sxs-lookup"><span data-stu-id="fd484-186">Using the Core.QueueWebJobUsage add-in</span></span>

<span data-ttu-id="fd484-187">Die folgende Tabelle beschreibt die Visual Studio-Projekte in der Projektmappe Core.QueueWebJobUsage.</span><span class="sxs-lookup"><span data-stu-id="fd484-187">The following table describes all the Visual Studio projects in the Core.QueueWebJobUsage solution.</span></span>

|<span data-ttu-id="fd484-188">**Visual Studio-Projekt**</span><span class="sxs-lookup"><span data-stu-id="fd484-188">**Visual Studio project**</span></span>|<span data-ttu-id="fd484-189">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="fd484-189">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="fd484-190">Core.QueueWebJobUsage</span><span class="sxs-lookup"><span data-stu-id="fd484-190">Core.QueueWebJobUsage</span></span>|<span data-ttu-id="fd484-191">Ihre SharePoint-Add-in-Projekt.</span><span class="sxs-lookup"><span data-stu-id="fd484-191">Your SharePoint Add-in project.</span></span> <span data-ttu-id="fd484-192">Die folgenden Berechtigungen sind erforderlich:</span><span class="sxs-lookup"><span data-stu-id="fd484-192">The following permissions are required:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="fd484-193">AllowAppOnlyPolicy</span><span class="sxs-lookup"><span data-stu-id="fd484-193">AllowAppOnlyPolicy</span></span></p></li><li><p><span data-ttu-id="fd484-194">Vollzugriff-Berechtigungen für das Web.</span><span class="sxs-lookup"><span data-stu-id="fd484-194">FullControl permissions on the Web.</span></span></p></li></ul>|
|<span data-ttu-id="fd484-195">Core.QueueWebJobUsage.Common</span><span class="sxs-lookup"><span data-stu-id="fd484-195">Core.QueueWebJobUsage.Common</span></span>|<span data-ttu-id="fd484-196">Enthält die Geschäftsobjekte und Code für die Geschäftslogik &mdash; wie Methoden zum Hinzufügen von Nachrichten an die Speicherwarteschlange &mdash; für diese Lösung.</span><span class="sxs-lookup"><span data-stu-id="fd484-196">Contains the business objects and business logic code &mdash; such as the methods to add messages to the storage queue &mdash; for this solution.</span></span> <span data-ttu-id="fd484-197">Dieses Projekt ist Freigabe von Geschäftsobjekten und zwischen verschiedenen Projekten Geschäftslogik enthalten.</span><span class="sxs-lookup"><span data-stu-id="fd484-197">This project is included to share business objects and business logic between different projects.</span></span> <span data-ttu-id="fd484-198">Sie können diese nicht in der Implementierung erforderlich.</span><span class="sxs-lookup"><span data-stu-id="fd484-198">You may not need this in your implementation.</span></span>|
|<span data-ttu-id="fd484-199">Core.QueueWebJobUsage.Job</span><span class="sxs-lookup"><span data-stu-id="fd484-199">Core.QueueWebJobUsage.Job</span></span>|<span data-ttu-id="fd484-200">Der Azure-WebJob, der ausgeführt wird, wenn eine neue Nachricht an die Warteschlange Azure Storage hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="fd484-200">The Azure WebJob that runs when a new message is added to the Azure Storage queue.</span></span> <span data-ttu-id="fd484-201">Dieses Projekt enthält Ihre benutzerdefinierten Code für die Geschäftslogik.</span><span class="sxs-lookup"><span data-stu-id="fd484-201">This project contains your custom business logic code.</span></span> |
|<span data-ttu-id="fd484-202">Core.QueueWebJobUsageWeb</span><span class="sxs-lookup"><span data-stu-id="fd484-202">Core.QueueWebJobUsageWeb</span></span>|<span data-ttu-id="fd484-203">Das vom Anbieter gehosteten add-in, das die Benutzeroberfläche für das Projekt Core.QueueWebJobUsage enthält.</span><span class="sxs-lookup"><span data-stu-id="fd484-203">The provider-hosted add-in that contains the UI for the Core.QueueWebJobUsage project.</span></span> |
|<span data-ttu-id="fd484-204">Hilfsprogramm Project\Core.QueueWebJobUsage.Console.SendMessage</span><span class="sxs-lookup"><span data-stu-id="fd484-204">Helper Project\Core.QueueWebJobUsage.Console.SendMessage</span></span>|<span data-ttu-id="fd484-205">Ein Hilfsprogramm-Projekt, das die Kontoinformationen Speicher und die Warteschlange Erstellungsprozess überprüfen und zum Senden von Nachrichten zur Verarbeitung an die Warteschlange, ohne die gesamte in diesem Artikel beschriebene Lösung einrichten verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="fd484-205">A helper project that can be used to validate the storage account information and queue creation process, and to send messages to the queue for processing without setting up the entire solution described in this article.</span></span> |

<span data-ttu-id="fd484-206">Wenn Sie das Codebeispiel Core.QueueWebJobUsage ausführen, die vom Anbieter gehosteten add-in angezeigt wird und zwei Schaltflächen angezeigt: **Vorgang synchrone** und **asynchrone Operation**.</span><span class="sxs-lookup"><span data-stu-id="fd484-206">When you run the Core.QueueWebJobUsage code sample, the provider-hosted add-in appears and displays two buttons:  **Synchronous operation** and **Asynchronous operation**.</span></span> <span data-ttu-id="fd484-207">Bei der Auswahl **synchronen Vorgang**simuliert **BtnSync_Click** in Pages\Default.aspx ein synchrone zeitintensiver Vorgang.</span><span class="sxs-lookup"><span data-stu-id="fd484-207">When you choose  **Synchronous operation**,  **btnSync_Click** in Pages\Default.aspx simulates a long-running synchronous process.</span></span> <span data-ttu-id="fd484-208">In diesem Codebeispiel **BtnSync_Click** des aktuellen Threads bis 10 Sekunden Energiesparmodus versetzt, und anschließend wird eine Dokumentbibliothek.</span><span class="sxs-lookup"><span data-stu-id="fd484-208">In this code sample, **btnSync_Click** puts the current thread to sleep for 10 seconds, and then creates a document library.</span></span> <span data-ttu-id="fd484-209">Wenn Sie eine **asynchrone Operation**auswählen, führt **BtnAsync_Click** in Pages\Default.aspx Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="fd484-209">When you choose **Asynchronous operation**,  **btnAsync_Click** in Pages\Default.aspx does the following:</span></span>

1. <span data-ttu-id="fd484-210">Ruft den aktuellen Benutzer ab.</span><span class="sxs-lookup"><span data-stu-id="fd484-210">Gets the current user.</span></span>
    
2. <span data-ttu-id="fd484-211">Erstellt ein **SiteModifyRequest** Business-Objekt, das die Daten zum Einschließen in die Nachricht an die Warteschlange Azure-Speicher gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="fd484-211">Creates a  **SiteModifyRequest** business object that stores the data to include in the message being sent to the Azure Storage queue.</span></span> <span data-ttu-id="fd484-212">In diesem Codebeispiel enthält die gesendeten Daten den Namen des aktuellen Benutzers und der aktuellen Website-URL.</span><span class="sxs-lookup"><span data-stu-id="fd484-212">In this code sample, the data being sent includes the current user's name and the current site's URL.</span></span>
    
3. <span data-ttu-id="fd484-213">Ruft die **SiteManager(). AddAsyncOperationRequestToQueue** um die Nachricht an die Warteschlange Azure Storage hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="fd484-213">Calls  **SiteManager().AddAsyncOperationRequestToQueue** to add the message to the Azure Storage queue.</span></span>
    
<span data-ttu-id="fd484-214">**Hinweis:**  Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="fd484-214">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="fd484-215">In Core.QueueWebJobUsage.Common, in SiteManager.cs führt **AddAsyncOperationRequestToQueue** Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="fd484-215">In Core.QueueWebJobUsage.Common, in SiteManager.cs,  **AddAsyncOperationRequestToQueue** does the following:</span></span>

1. <span data-ttu-id="fd484-216">Erstellt ein [CloudStorageAccount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx) -Objekt mithilfe der **Kontoname** und **AccountKey** Konfigurationsinformationen in der Datei Core.QueueWebJobUsageWeb\web.config.</span><span class="sxs-lookup"><span data-stu-id="fd484-216">Creates a [CloudStorageAccount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx) object by using the **AccountName** and **AccountKey** configuration information in the Core.QueueWebJobUsageWeb\web.config file.</span></span>
    
2. <span data-ttu-id="fd484-217">Erstellt einen Azure Storage Warteschlange Client mithilfe von [CloudStorageAccount.CreateCloudQueueClient](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.createcloudqueueclient.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd484-217">Creates an Azure Storage queue client by using [CloudStorageAccount.CreateCloudQueueClient](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.createcloudqueueclient.aspx).</span></span>
    
3. <span data-ttu-id="fd484-218">[CloudQueueClient.GetQueueReference](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueueclient.getqueuereference.aspx) verwendet, um einen Verweis auf die Warteschlange Azure-Speicher mit dem Namen gleich dem Wert, der die **SiteManager.StorageQueueName** Konstante abzurufen.</span><span class="sxs-lookup"><span data-stu-id="fd484-218">Uses [CloudQueueClient.GetQueueReference](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueueclient.getqueuereference.aspx) to get a reference to the Azure Storage queue with name equal to the value of the **SiteManager.StorageQueueName** constant.</span></span>
    
4. <span data-ttu-id="fd484-219">Verwendet [CloudQueue.CreateIfNotExists](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.createifnotexists.aspx) die Warteschlange Azure-Speicher zu erstellen, wenn er nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="fd484-219">Uses [CloudQueue.CreateIfNotExists](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.createifnotexists.aspx) to create the Azure Storage queue if it does not exist.</span></span>
    
5. <span data-ttu-id="fd484-220">Verwendet [CloudQueue.AddMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) , um eine neue Nachricht an die Warteschlange Azure Storage hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="fd484-220">Uses [CloudQueue.AddMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) to add a new message to the Azure Storage queue.</span></span> <span data-ttu-id="fd484-221">Das Geschäftsobjekt **ModifyRequest aufgefordert** wird in ein Objekt [CloudQueueMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.aspx) serialisiert, die an die Warteschlange Azure Storage hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="fd484-221">The **modifyRequest** business object is serialized into a [CloudQueueMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.aspx) object, which is added to the Azure Storage queue.</span></span>

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

<span data-ttu-id="fd484-222">Nachdem die Nachricht an die Warteschlange der Azure-Speicher hinzugefügt wurde, eine ständig ausgeführten Azure WebJob wartet und klicken Sie dann die neue Nachricht verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="fd484-222">After the message is added to the Azure Storage Queue, a continuously running Azure WebJob waits for and then processes the new message.</span></span> <span data-ttu-id="fd484-223">Der Azure-WebJob ist in Core.QueueWebJobUsage.Job definiert.</span><span class="sxs-lookup"><span data-stu-id="fd484-223">The Azure WebJob is defined in Core.QueueWebJobUsage.Job.</span></span> <span data-ttu-id="fd484-224">Wenn der Azure-WebJob ausgeführt wird, wird in Core.QueueWebJobUsage.Job\Program.cs Main erstellt eine neue **JobHost**und ruft dann **RunAndBlock**.</span><span class="sxs-lookup"><span data-stu-id="fd484-224">When the Azure WebJob runs, Main in Core.QueueWebJobUsage.Job\Program.cs creates a new  **JobHost**, and then calls **RunAndBlock**.</span></span> <span data-ttu-id="fd484-225">Die **JobHost** Koordinaten Aufrufe von Methoden mit dem **QueueTrigger** -Attribut und Überwachungen für Nachrichten auf einer bestimmten Warteschlange markiert.</span><span class="sxs-lookup"><span data-stu-id="fd484-225">The **JobHost** coordinates calls to methods marked with the **QueueTrigger** attribute, and watches for messages on a specific queue.</span></span> <span data-ttu-id="fd484-226">**RunAndBlock** wird sichergestellt, dass der Azure-WebJob kontinuierlich ausgeführt wird, und ruft **ProcessQueueMessage**, also die Methode, die ausgelöst wird, wenn eine neue Nachricht an die Warteschlange der Azure-Speicher hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="fd484-226">**RunAndBlock** ensures that the Azure WebJob runs continuously and calls **ProcessQueueMessage**, which is the method to trigger when a new message is added to the Azure Storage Queue.</span></span> <span data-ttu-id="fd484-227">Die Azure WebJobs SDK zuordnet **ProcessQueueMessage** **den Hauptthread** .</span><span class="sxs-lookup"><span data-stu-id="fd484-227">The Azure WebJobs SDK associates the **Main** thread with **ProcessQueueMessage**.</span></span> <span data-ttu-id="fd484-228">Weitere Informationen finden Sie unter [Erstellen einer .NET WebJob in Azure-Add-in-Diensts](https://azure.microsoft.com/documentation/articles/websites-dotnet-webjobs-sdk-get-started/).</span><span class="sxs-lookup"><span data-stu-id="fd484-228">For more information, see [Create a .NET WebJob in Azure Add-in Service](https://azure.microsoft.com/documentation/articles/websites-dotnet-webjobs-sdk-get-started/).</span></span>

```C#
static void Main()
        {
            var host = new JobHost();
            // The following code ensures that the WebJob will run continuously.
            host.RunAndBlock();
        }
```

<span data-ttu-id="fd484-229">**ProcessQueueMessage** verarbeitet neue Nachrichten, die an die Warteschlange Azure Storage durch hinzugefügt werden:</span><span class="sxs-lookup"><span data-stu-id="fd484-229">**ProcessQueueMessage** processes new messages that are added to the Azure Storage queue by:</span></span>

1. <span data-ttu-id="fd484-230">Verwenden das **QueueTrigger** -Attribut angegeben wird, dass **ProcessQueueMessage** ausgelöst werden soll, wenn eine neue Nachricht an die Warteschlange mit dem Namen gleich dem Wert der **SiteManager.StorageQueueName**geschrieben wird.</span><span class="sxs-lookup"><span data-stu-id="fd484-230">Using the  **QueueTrigger** attribute to specify that **ProcessQueueMessage** should be triggered when a new message is written to the queue with name equal to the value of **SiteManager.StorageQueueName**.</span></span>
    
2. <span data-ttu-id="fd484-231">Schreiben in die Protokolldatei für die Azure WebJob mithilfe der **Log** -Variable, die als Parameter an **ProcessQueueMessage**übergeben wurde.</span><span class="sxs-lookup"><span data-stu-id="fd484-231">Writing to the log for the Azure WebJob by using the  **log** variable that was passed as a parameter to **ProcessQueueMessage**.</span></span>
    
3. <span data-ttu-id="fd484-232">Aufrufen von **SiteManager(). PerformSiteModification** einen Geschäftsprozess langer auf der Website ausführen.</span><span class="sxs-lookup"><span data-stu-id="fd484-232">Calling  **SiteManager().PerformSiteModification** to perform a long-running business process on the site.</span></span> <span data-ttu-id="fd484-233">In diesem Codebeispiel der Thread um 10 Sekunden Energiesparmodus versetzt wird, und klicken Sie dann eine Dokumentbibliothek erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="fd484-233">In this code sample, the thread is put to sleep for 10 seconds, and then a document library is created.</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="fd484-234">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="fd484-234">Additional resources</span></span>
<span data-ttu-id="fd484-235"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="fd484-235"></span></span>

- <span data-ttu-id="fd484-236">[Office 365 Development Mustern und Methoden ausgesprochen](Office-365-development-patterns-and-practices-solution-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="fd484-236">[Office 365 development patterns and practices solution guidance](Office-365-development-patterns-and-practices-solution-guidance.md).</span></span>
    
- [<span data-ttu-id="fd484-237">Verwenden von remote-Ereignisempfänger in SharePoint</span><span class="sxs-lookup"><span data-stu-id="fd484-237">Use remote event receivers in SharePoint</span></span>](Use-remote-event-receivers-in-SharePoint.md)
    
- [<span data-ttu-id="fd484-238">Abfragen von SharePoint-Änderungsprotokoll mit komplexer ChangeQuery und komplexer ChangeToken</span><span class="sxs-lookup"><span data-stu-id="fd484-238">Query SharePoint change log with ChangeQuery and ChangeToken</span></span>](query-sharepoint-change-log-with-changequery-and-changeToken.md)
