---
title: "Verwenden von remote-Ereignisempfänger in SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 713e1b42682a315626e2d121710931c64e86961e
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="use-remote-event-receivers-in-sharepoint"></a><span data-ttu-id="a6e0a-102">Verwenden von remote-Ereignisempfänger in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a6e0a-102">Use remote event receivers in SharePoint</span></span>

<span data-ttu-id="a6e0a-103">Verwenden Sie remote-Ereignisempfänger zum Verarbeiten von Ereignissen in der SharePoint-add-in-Objektmodell.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-103">Use remote event receivers to handle events in the SharePoint add-in model.</span></span> <span data-ttu-id="a6e0a-104">Verwenden Sie Ereignisse AppInstalled und AppUninstalling festlegen oder Entfernen von SharePoint-Objekten und anderen Ereignisempfänger, die Ihr Add-in benötigt.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-104">Use AppInstalled and AppUninstalling events to set up or remove SharePoint objects and other event receivers your add-in needs.</span></span>

<span data-ttu-id="a6e0a-105">_**Gilt für:** Add-Ins für SharePoint | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="a6e0a-105">_**Applies to:** add-ins for SharePoint | SharePoint 2013 | SharePoint Online_</span></span>

><span data-ttu-id="a6e0a-106">**Wichtige** Ab Januar 2017 SharePoint Online unterstützt Liste Webhooks, die Sie, anstatt verwenden können "-Ed" remote-Ereignisempfänger.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-106">**Important** As of January 2017 SharePoint Online does support list webhooks which you can use instead of "-ed" remote event receivers.</span></span> <span data-ttu-id="a6e0a-107">Checkout- [Übersicht von SharePoint-Webhooks](https://dev.office.com/sharepoint/docs/apis/webhooks/overview-sharepoint-webhooks) erfahren Sie mehr über Webhooks.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-107">Checkout [Overview of SharePoint webhooks](https://dev.office.com/sharepoint/docs/apis/webhooks/overview-sharepoint-webhooks) to learn more about webhooks.</span></span> <span data-ttu-id="a6e0a-108">Beachten Sie außerdem, dass mehrere Webhook Beispiele aus GitHub Repository [sp-Dev-Beispiele](https://github.com/SharePoint/sp-dev-samples/tree/master/Samples) verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-108">Also note that several webhook samples are available from the [sp-dev-samples](https://github.com/SharePoint/sp-dev-samples/tree/master/Samples) GitHub repository.</span></span>

<span data-ttu-id="a6e0a-109">Das [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) -Beispiel veranschaulicht, wie ein vom Anbieter gehosteten add-in mit einer remote-Ereignisempfänger verwenden, um die AppInstalled und AppUninstalling Ereignisse behandeln.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-109">The  [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) sample shows how to use a provider-hosted add-in with a remote event receiver to handle the AppInstalled and AppUninstalling events.</span></span> <span data-ttu-id="a6e0a-110">Die Ereignisse AppInstalled und AppUninstalling einrichten und Entfernen von SharePoint-Objekten, die das Add-in verwendet wird, wenn es ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-110">The AppInstalled and AppUninstalling events set up and remove SharePoint objects that the add-in uses when it runs.</span></span> <span data-ttu-id="a6e0a-111">Darüber hinaus der AppInstalled-Ereignishandler den Ereignishandler ItemAdded einer Liste hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-111">Additionally, the AppInstalled event handler adds the ItemAdded event handler to a list.</span></span> <span data-ttu-id="a6e0a-112">Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:</span><span class="sxs-lookup"><span data-stu-id="a6e0a-112">Use this solution if you want to:</span></span>

- <span data-ttu-id="a6e0a-113">Konfigurieren Sie Ihr Add-in auf führen Sie mithilfe des AppInstalled-Ereignisses zum Einrichten von verschiedenen SharePoint-Objekte oder zusätzliche Ereignisempfängern, denen vom Add-in verwendet.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-113">Configure your add-in on first run using the AppInstalled event to set up various SharePoint objects or additional event receivers that your add-in works with.</span></span>
    
- <span data-ttu-id="a6e0a-114">Ersetzen Sie Ereignisempfänger mit Lösungen voll vertrauenswürdiger Code implementiert.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-114">Replace event receivers implemented using fully trusted code solutions.</span></span> <span data-ttu-id="a6e0a-115">Voll vertrauenswürdiger Code-Lösungen können Sie Ereignisempfänger auf dem SharePoint-Server ausführen.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-115">In fully trusted code solutions, you can run event receivers on the SharePoint server.</span></span> <span data-ttu-id="a6e0a-116">Im neuen SharePoint-add-in-Modell da Sie nicht den Ereignisempfänger auf dem SharePoint-Server ausführen können müssen Sie einen remote-Ereignisempfänger auf einem Webserver implementieren.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-116">In the new SharePoint add-in model, because you cannot run the event receiver on the SharePoint server, you need to implement a remote event receiver on a web server.</span></span>
    
- <span data-ttu-id="a6e0a-117">Empfangen von Benachrichtigungen über nicht mehr auftritt Änderungen in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-117">Receive notifications of changes occuring in SharePoint.</span></span> <span data-ttu-id="a6e0a-118">Eine Liste ein neues Element hinzugefügt wird, möchten Sie beispielsweise eine Aufgabe auszuführen.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-118">For example, when a new item is added to a list, you want to perform a task.</span></span>

- <span data-ttu-id="a6e0a-119">Ergänzen Sie die Änderung Log-Lösung.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-119">Complement your change log solution.</span></span> <span data-ttu-id="a6e0a-120">Verwenden das remote-Ereignisempfänger Muster mit einem Change-Log-Muster bietet eine zuverlässigere Architektur für die Verarbeitung aller Änderungen an SharePoint-Inhaltsdatenbanken, Websitesammlungen, Websites oder Listen.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-120">Using the remote event receiver pattern with a change log pattern provides a more reliable architecture for handling all changes made to SharePoint content databases, site collections, sites, or lists.</span></span> <span data-ttu-id="a6e0a-121">Remote-Ereignisempfänger sofort ausgeführt, aber, da sie auf einem Remoteserver ausgeführt werden, treten möglicherweise ein Fehler bei der Kommunikation.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-121">Remote event receivers run immediately, but because they run on a remote server, you might encounter a communication failure.</span></span> <span data-ttu-id="a6e0a-122">Das Muster der Änderung Protokoll wird sichergestellt, dass alle Änderungen für die Verarbeitung verfügbar sind, aber die Anwendung die Änderungen bei der Verarbeitung in der Regel nach einem Zeitplan (beispielsweise einen Zeitgeberauftrag) ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-122">The change log pattern ensures that all changes are available for processing, but the application processing the changes usually runs on a schedule (for example, a timer job).</span></span> <span data-ttu-id="a6e0a-123">Dies bedeutet, dass die Änderungen nicht sofort verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-123">This means that changes are not processed immediately.</span></span> <span data-ttu-id="a6e0a-124">Wenn Sie diese beiden Muster gemeinsam verwenden, stellen Sie sicher, dass Sie einen Mechanismus verwenden, um zu verhindern, dass die gleiche Änderung zweimal verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-124">If you use these two patterns together, ensure you use a mechanism to prevent processing the same change twice.</span></span> <span data-ttu-id="a6e0a-125">Weitere Informationen finden Sie unter [Abfrage SharePoint Änderungsprotokoll mit komplexer ChangeQuery und komplexer ChangeToken](query-sharepoint-change-log-with-changequery-and-changeToken.md).</span><span class="sxs-lookup"><span data-stu-id="a6e0a-125">For more information, see [Query SharePoint change log with ChangeQuery and ChangeToken](query-sharepoint-change-log-with-changequery-and-changeToken.md).</span></span>

<span data-ttu-id="a6e0a-126">**Hinweis**  SharePoint-Hosting-add-ins unterstützt remote-Ereignisempfänger nicht.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-126">**Note**  SharePoint-hosted add-ins do not support remote event receivers.</span></span> <span data-ttu-id="a6e0a-127">Um remote-Ereignisempfänger verwenden, müssen Sie eine vom Anbieter gehosteten-add-in verwenden.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-127">To use remote event receivers, you need to use a provider-hosted add-in.</span></span> <span data-ttu-id="a6e0a-128">Sollten Sie remote-Ereignisempfänger nicht verwenden, für die Synchronisierung oder lange ausgeführte Prozesse.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-128">You should not use remote event receivers for synchronization scenarios, or for long running processes.</span></span> <span data-ttu-id="a6e0a-129">Weitere Informationen finden Sie unter [Vorgehensweise: Erstellen eines Ereignisempfängers-Add-in](https://msdn.microsoft.com/library/office/jj220052.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6e0a-129">For more information, see  [How to: Create an add-in event receiver](https://msdn.microsoft.com/library/office/jj220052.aspx).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a6e0a-130">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="a6e0a-130">Before you begin</span></span>
<span data-ttu-id="a6e0a-131"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="a6e0a-131"></span></span>

<span data-ttu-id="a6e0a-132">Laden Sie Sie zuerst [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-132">To get started, download the  [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="a6e0a-133">Vor dem Ausführen dieses Add-in führen Sie die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="a6e0a-133">Before you run this add-in, do the following:</span></span>

1. <span data-ttu-id="a6e0a-134">In den Eigenschaften auf das Projekt Core.EventReceivers stellen Sie sicher, dass **Handle App Installed** und **App-Deinstallation behandeln** auf **True**festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-134">In the properties on the Core.EventReceivers project, verify that  **Handle App Installed** and **Handle App Uninstalling** is set to **True**.</span></span> <span data-ttu-id="a6e0a-135">**Handle App Installed** und **App-Deinstallation behandeln** auf **True** festlegen, erstellt einen WCF-Dienst, der den Ereignishandler für das Ereignis **AppInstalled** und **AppUninstalling** definiert.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-135">Setting  **Handle App Installed** and **Handle App Uninstalling** to **True** creates a WCF service that defines the event handler for the **AppInstalled** and **AppUninstalling** event.</span></span> <span data-ttu-id="a6e0a-136">Klicken Sie im Core.EventReceivers öffnen Sie das Kontextmenü (Rechtsklick) auf AppManifest.xml, und wählen Sie **Eigenschaften**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-136">In Core.EventReceivers, open the shortcut menu (right-click) on AppManifest.xml, and choose **Properties**.</span></span> <span data-ttu-id="a6e0a-137">Zeigen Sie auf der remote-Ereignisempfänger, der die **AppInstalled** und **AppUninstalling** Ereignisse behandelt, die **InstalledEventEndpoint** und **UninstallingEventEndpoint** .</span><span class="sxs-lookup"><span data-stu-id="a6e0a-137">The  **InstalledEventEndpoint** and **UninstallingEventEndpoint** point to the remote event receiver that handles the **AppInstalled** and **AppUninstalling** events.</span></span>
    
2. <span data-ttu-id="a6e0a-138">Anfügen eines remote-Ereignisempfängers zu einem Objekt in der Hostwebsite in der Regel erfordert Berechtigung **Verwalten** für dieses Objekt nur.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-138">Attaching a remote event receiver to an object in the host web usually requires  **Manage** permission for that object only.</span></span> <span data-ttu-id="a6e0a-139">Beispielsweise erfordert beim Anfügen eines Ereignisempfängers zu einer vorhandenen Liste das Add-in Berechtigung in der **Liste** nur **Verwalten** .</span><span class="sxs-lookup"><span data-stu-id="a6e0a-139">For example, when attaching an event receiver to an existing list, the add-in requires **Manage** permission on the **List** only.</span></span> <span data-ttu-id="a6e0a-140">In diesem Codebeispiel erfordert **Verwalten** von Berechtigungen auf dem **Web** , da es eine Liste hinzugefügt und ein Feature auf dem hostweb aktiviert.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-140">This code sample requires **Manage** permissions on the **Web** because it adds a list and activates a feature on the host web.</span></span> <span data-ttu-id="a6e0a-141">So legen Sie fest Verwalten von Berechtigungen im Web:</span><span class="sxs-lookup"><span data-stu-id="a6e0a-141">To set manage permissions on the web:</span></span>
    
    1. <span data-ttu-id="a6e0a-142">Klicken Sie mit der Doppelklicken auf Core.EventReceivers\AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-142">Double click Core.EventReceivers\AppManifest.xml.</span></span>
    
    2. <span data-ttu-id="a6e0a-143">Wählen Sie **Berechtigungen**aus.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-143">Choose  **Permissions**.</span></span>
    
    3. <span data-ttu-id="a6e0a-144">Stellen Sie sicher, dass der **Bereich** **Web**festgelegt ist und **die Berechtigung** zum **Verwalten**festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-144">Verify that  **Scope** is set to **Web**, and  **Permission** is set to **Manage**.</span></span>
    
3. <span data-ttu-id="a6e0a-145">Um dieses Codebeispiel auszuführen, benötigen Sie ein Azure-Abonnement.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-145">To run this code sample, you need an Azure subscription.</span></span> <span data-ttu-id="a6e0a-146">Um für eine Testversion zu registrieren, finden Sie unter [kostenlose einmonatige Testversion](http://azure.microsoft.com/en-us/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a6e0a-146">To sign up for a trial, see  [Free one-month trial](http://azure.microsoft.com/en-us/pricing/free-trial/).</span></span>
    
4. <span data-ttu-id="a6e0a-147">Erstellen einer Azure Servicebus-Namespace mit ACS-Unterstützung.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-147">Create an Azure Service Bus Namespace with ACS Support.</span></span>
    
    1. <span data-ttu-id="a6e0a-148">Installieren von Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-148">Install Azure PowerShell.</span></span> <span data-ttu-id="a6e0a-149">Weitere Informationen finden Sie unter [Vorgehensweise: Installieren von Azure PowerShell](http://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/#Install).</span><span class="sxs-lookup"><span data-stu-id="a6e0a-149">For more information, see  [How to: Install Azure PowerShell](http://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/#Install).</span></span>
    
    2. <span data-ttu-id="a6e0a-150">**Azure PowerShell**zu starten.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-150">Start  **Azure PowerShell**.</span></span>
    
    3. <span data-ttu-id="a6e0a-151">Geben Sie **Add AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-151">Enter  **Add-AzureAccount**.</span></span>
    
    4. <span data-ttu-id="a6e0a-152">Geben Sie Ihre e-Mail-Adresse in das Dialogfeld **Anmelden bei Windows Azure** , und wählen Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-152">Enter your email address in the  **Sign in to Windows Azure** dialog, and then choose **Continue**.</span></span>
    
    5. <span data-ttu-id="a6e0a-153">Geben Sie Ihr Kennwort ein, und wählen Sie dann auf **Anmelden**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-153">Enter your password, and then choose  **Sign in**.</span></span>
    
    6. <span data-ttu-id="a6e0a-154">Erstellen Sie einen neuen Servicebus-Namespace, mit dem folgenden PowerShell-Cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-154">Create a new service bus namespace using the following PowerShell cmdlet.</span></span>
    
        ```powershell
        New-AzureSBNamespace NamespaceNameRegion -CreateACSNamespace $true -NamespaceType Messaging
        
        ```
    
       <span data-ttu-id="a6e0a-155">Dabei gilt:</span><span class="sxs-lookup"><span data-stu-id="a6e0a-155">Where:</span></span>
    
       -  <span data-ttu-id="a6e0a-156">_NamespaceName_ ist der Name des Azure-Servicebus-Namespace.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-156">_NamespaceName_ is the name of your Azure Service Bus namespace.</span></span>
    
       -  <span data-ttu-id="a6e0a-157">_Bereich_ ist die Region, die Sie am nächsten.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-157">_Region_ is the region closest to you.</span></span> <span data-ttu-id="a6e0a-158">Beispielsweise können Sie **"West US"**eingeben.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-158">For example, you may enter **"West US"**.</span></span> <span data-ttu-id="a6e0a-159">Sie müssen den Bereichsnamen in doppelte Anführungszeichen einschließen.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-159">You must include the region name in double quotes.</span></span>
    
    7. <span data-ttu-id="a6e0a-160">Geben Sie an der Azure-Verwaltungsportal.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-160">Return to your Azure Management Portal.</span></span> <span data-ttu-id="a6e0a-161">Wählen Sie **SERVICE BUS**, und wählen Sie dann den Namespacenamen, den Sie angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-161">Choose  **SERVICE BUS**, and then choose the namespace name you entered.</span></span>
    
    8. <span data-ttu-id="a6e0a-162">Wählen Sie die **Verbindungszeichenfolgen zu verwalten**, und klicken Sie dann in der **VERBINDUNGSZEICHENFOLGE ACS**, wählen Sie die Schaltfläche kopieren.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-162">Choose  **Manage Connection Strings**, and then in  **ACS CONNECTION STRING**, choose the copy button.</span></span>
    
    9. <span data-ttu-id="a6e0a-163">Zurück zu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-163">Return to Visual Studio.</span></span>
    
    10. <span data-ttu-id="a6e0a-164">Mit der rechten Maustaste Core.EventReceivers > **Eigenschaften** > **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-164">Right-click Core.EventReceivers >  **Properties** > **SharePoint**.</span></span>
    
    11. <span data-ttu-id="a6e0a-165">Wählen Sie **über die Microsoft Azure-Servicebus-debugging aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-165">Select  **Enable debugging via Microsoft Azure Service Bus**.</span></span>
    
    12. <span data-ttu-id="a6e0a-166">Fügen Sie in **Microsoft Azure-Servicebus-Verbindungszeichenfolge**die ACS-Verbindungszeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-166">In  **Microsoft Azure Service Bus connection string**, paste the ACS Connection String.</span></span>
    
    13. <span data-ttu-id="a6e0a-167">Wählen Sie **Speichern**aus.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-167">Choose  **Save**.</span></span>
    
5. <span data-ttu-id="a6e0a-168">Führen Sie das Codebeispiel, und führen Sie die folgenden zusätzlichen Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="a6e0a-168">Run the code sample, and perform the following additional steps:</span></span>
    
    - <span data-ttu-id="a6e0a-169">Klicken Sie auf **Vertrauen** in das **Erteilen von Berechtigungen für die app** -Fenster.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-169">Click  **Trust It** in the **Grant permissions to the app** window.</span></span>
    
    - <span data-ttu-id="a6e0a-170">Schließen Sie das **Erteilen von Berechtigungen für die app** -Fenster.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-170">Close the  **Grant permissions to the app** window.</span></span>
    
    - <span data-ttu-id="a6e0a-171">Nach Abschluss der Installation des-Add-in und der WCF-Dienst wird der Browser geöffnet.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-171">When installation of the add-in and WCF service is completed, your browser will open.</span></span>
    
    - <span data-ttu-id="a6e0a-172">Melden Sie sich bei Ihrem Office 365-Website.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-172">Sign in to your Office 365 site.</span></span> <span data-ttu-id="a6e0a-173">Die Startseite des Core.EventReceivers-add-Ins wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-173">The start page of the Core.EventReceivers add-in is displayed.</span></span>

## <a name="use-the-coreeventreceivers-add-in"></a><span data-ttu-id="a6e0a-174">Verwenden des Core.EventReceivers-add-Ins</span><span class="sxs-lookup"><span data-stu-id="a6e0a-174">Use the Core.EventReceivers add-in</span></span>
<span data-ttu-id="a6e0a-175"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="a6e0a-175"></span></span>

<span data-ttu-id="a6e0a-176">Um eine Demo des Codebeispiels Core.EventReceivers finden Sie unter:</span><span class="sxs-lookup"><span data-stu-id="a6e0a-176">To see a demo of the Core.EventReceivers code sample:</span></span>

1. <span data-ttu-id="a6e0a-177">Führen Sie das Beispiel, und wählen Sie auf der Startseite **zur Website**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-177">Run the sample, and on the start page, choose  **Back to Site**.</span></span>
    
2. <span data-ttu-id="a6e0a-178">Wählen Sie **Websiteinhalte**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-178">Choose  **Site Contents**.</span></span>
    
3. <span data-ttu-id="a6e0a-179">Wählen Sie **Remote Event Receiver Aufträge**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-179">Choose  **Remote Event Receiver Jobs**.</span></span>
    
4. <span data-ttu-id="a6e0a-180">Wählen Sie **Neues Element**aus.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-180">Choose  **new item**.</span></span>
    
5. <span data-ttu-id="a6e0a-181">**Titel**Geben Sie **Contoso**, und geben Sie im Feld **Beschreibung** ein **Contoso testen**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-181">In  **Title**, enter  **Contoso**, and in  **Description** enter **Contoso test**.</span></span>
    
6. <span data-ttu-id="a6e0a-182">Zurück zur Liste, und aktualisieren Sie die Seite.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-182">Return to the list and refresh the page.</span></span>
    
7. <span data-ttu-id="a6e0a-183">Stellen Sie sicher, dass die Beschreibung des neu hinzugefügten Elements auf **Contoso Test wurde aktualisiert, indem ReR 192336**aktualisiert wurde, in dem **192336** Zeitstempel ist.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-183">Verify that the description of the newly added item was updated to  **Contoso test Updated by ReR 192336**, where  **192336** is a timestamp.</span></span>
    
<span data-ttu-id="a6e0a-184">In Services/AppEventReceiver.cs implementiert **AppEventReceiver** die **IRemoteEventService** -Schnittstelle.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-184">In Services/AppEventReceiver.cs,  **AppEventReceiver** implements the **IRemoteEventService** interface.</span></span> <span data-ttu-id="a6e0a-185">In diesem Codebeispiel stellt eine Implementierung für die **ProcessEvent** -Methode, da sie synchrone Ereignisse verwendet.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-185">This code sample provides an implementation for the **ProcessEvent** method because it uses synchronous events.</span></span> <span data-ttu-id="a6e0a-186">Wenn Sie asynchrone Ereignisse verwenden, müssen Sie eine Implementierung für die Methode **ProcessOneWayEvent** bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-186">If you use asynchronous events, you need to provide an implementation for the **ProcessOneWayEvent** method.</span></span>

<span data-ttu-id="a6e0a-187">Die **ProcessEvent** behandelt die folgenden remote **SPRemoteEventType** -Ereignisse:</span><span class="sxs-lookup"><span data-stu-id="a6e0a-187">The  **ProcessEvent** handles the following **SPRemoteEventType** remote events:</span></span>

-  <span data-ttu-id="a6e0a-188">**AppInstalled** Ereignisse aus, wenn das Add-in zu installieren.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-188">**AppInstalled** events when installing the add-in.</span></span> <span data-ttu-id="a6e0a-189">Wenn ein **AppInstalled** -Ereignis eintritt, **ProcessEvent** Anrufe **HandleAppInstalled**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-189">When an **AppInstalled** event occurs, **ProcessEvent** calls **HandleAppInstalled**.</span></span>
    
-  <span data-ttu-id="a6e0a-190">**AppUninstalling** Ereignisse aus, wenn das Add-in zu deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-190">**AppUninstalling** events when uninstalling the add-in.</span></span> <span data-ttu-id="a6e0a-191">Wenn ein **AppUninstalling** -Ereignis eintritt, **ProcessEvent** Anrufe **HandleAppUninstalling**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-191">When an **AppUninstalling** event occurs, **ProcessEvent** calls **HandleAppUninstalling**.</span></span> <span data-ttu-id="a6e0a-192">Das **AppUninstalling** -Ereignis wird nur ausgeführt, wenn ein Benutzer das Add-in durch Löschen des Add-Ins aus dem Papierkorb der Website (für Endbenutzer) oder durch das Add-in aus der Liste **Apps im Test** (für Entwickler) entfernen entfernt vollständig.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-192">The  **AppUninstalling** event only runs when a user completely removes the add-in either by deleting the add-in from the site recycle bin (for end users) or by removing the add-in from the **Apps in testing** list (for developers).</span></span>
    
-  <span data-ttu-id="a6e0a-193">**ItemAdded** -Ereignisse, wenn eine Liste ein Element hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-193">**ItemAdded** events when an item is added to a list.</span></span> <span data-ttu-id="a6e0a-194">**ItemAdded** -Ereignis tritt auf, **ProcessEvent** Anrufe **HandleItemAdded**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-194">When an **ItemAdded** event occurs, **ProcessEvent** calls **HandleItemAdded**.</span></span>

<span data-ttu-id="a6e0a-195">**Hinweis**  In den Projekteigenschaften Core.EventReceiver stehen nur Eigenschaften **Handle App Installed** und **App-Deinstallation behandeln** .</span><span class="sxs-lookup"><span data-stu-id="a6e0a-195">**Note**  In the Core.EventReceiver project properties, only  **Handle App Installed** and **Handle App Uninstalling** properties are available.</span></span> <span data-ttu-id="a6e0a-196">In diesem Codebeispiel wird veranschaulicht, wie Sie den **ItemAdded** -Ereignis-Handler zu einer Liste auf dem hostweb mithilfe des **AppInstalled** -Ereignisses während der Add-in-Installation hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-196">This code sample shows how you can add the **ItemAdded** event handler to a list on the host web by using the **AppInstalled** event during add-in installation.</span></span>

<span data-ttu-id="a6e0a-197">**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-197">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="a6e0a-198">**HandleAppInstalled** ruft **RemoteEventReceiverManager.AssociateRemoteEventsToHostWeb** in RemoteEventReceiverManager.cs.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-198">**HandleAppInstalled** calls **RemoteEventReceiverManager.AssociateRemoteEventsToHostWeb** in RemoteEventReceiverManager.cs.</span></span>

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

<span data-ttu-id="a6e0a-199">**AssociateRemoteEventsToHostWeb** erstellt oder ermöglicht verschiedenen SharePoint-Objekten, die das Core.EventReceivers-add-in verwendet.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-199">**AssociateRemoteEventsToHostWeb** creates or enables various SharePoint objects that the Core.EventReceivers add-in uses.</span></span> <span data-ttu-id="a6e0a-200">Standarddateispeicherort abweichen.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-200">Your requirements might differ.</span></span> <span data-ttu-id="a6e0a-201">**AssociateRemoteEventsToHostWeb** bewirkt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a6e0a-201">**AssociateRemoteEventsToHostWeb** does the following:</span></span>

- <span data-ttu-id="a6e0a-202">Aktiviert das Pushbenachrichtigung-Feature mithilfe von **Web.Features.Add**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-202">Enables the Push Notification feature by using  **Web.Features.Add**.</span></span>
    
- <span data-ttu-id="a6e0a-203">Verwendet das **ClientContext** -Objekt um eine Liste zu suchen.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-203">Uses the  **clientContext** object to search for a list.</span></span> <span data-ttu-id="a6e0a-204">Wenn die Liste nicht vorhanden ist, wird **CreateJobsList** die Liste erstellt.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-204">If the list does not exist, **CreateJobsList** creates the list.</span></span> <span data-ttu-id="a6e0a-205">Wenn die Liste vorhanden ist, wird **List.EventReceivers** verwendet, um für einen vorhandenen Ereignisempfänger zu suchen, deren Namen **ItemAddedEvent**ist.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-205">If the list exists, **List.EventReceivers** is used to search for an existing event receiver whose name is **ItemAddedEvent**.</span></span>
    
- <span data-ttu-id="a6e0a-206">Wenn der **ItemAddedEvent** -Ereignisempfänger nicht vorhanden ist:</span><span class="sxs-lookup"><span data-stu-id="a6e0a-206">If the  **ItemAddedEvent** event receiver does not exist:</span></span>
    
    - <span data-ttu-id="a6e0a-207">Instanziiert ein neues **komplexer EventReceiverDefinitionCreationInformation** -Objekt zum Erstellen des neuen remote-Ereignisempfängers.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-207">Instantiates a new  **EventReceiverDefinitionCreationInformation** object to create the new remote event receiver.</span></span> <span data-ttu-id="a6e0a-208">Der **ItemAdded** Receiver Ereignistyp wird **EventReceiverDefinitionCreationInformation.EventType**hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-208">The **ItemAdded** event receiver type is added to **EventReceiverDefinitionCreationInformation.EventType**.</span></span>
    
    - <span data-ttu-id="a6e0a-209">Die **EventReceiverDefinitionCreationInformation.ReceiverURL** festgelegt auf die URL der der **AppInstalled** remote-Ereignisempfänger.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-209">Sets the  **EventReceiverDefinitionCreationInformation.ReceiverURL** to the URL of the **AppInstalled** remote event receiver.</span></span>
    
    - <span data-ttu-id="a6e0a-210">Fügt einen neuen-Ereignisempfänger zur Liste mithilfe von **List.EventReceivers.Add**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-210">Adds a new event receiver to the list using  **List.EventReceivers.Add**.</span></span>

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

<span data-ttu-id="a6e0a-211">Wenn der **Remote Event Receiver Aufträge** Liste ein Element hinzugefügt wird, **ProcessEvent** in AppEventReceiver.svc.cs behandelt das **ItemAdded** -Ereignis und ruft dann **HandleItemAdded**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-211">When an item is added to the  **Remote Event Receiver Jobs** list, **ProcessEvent** in AppEventReceiver.svc.cs handles the **ItemAdded** event, and then calls **HandleItemAdded**.</span></span>  <span data-ttu-id="a6e0a-212">**HandleItemAdded** ruft **RemoteEventReceiverManager.ItemAddedToListEventHandler**.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-212">**HandleItemAdded** calls **RemoteEventReceiverManager.ItemAddedToListEventHandler**.</span></span>  <span data-ttu-id="a6e0a-213">**ItemAddedToListEventHandler** Ruft das Listenelement, das hinzugefügt wurde, und das Listenelement Beschreibung die Zeichenfolge **aktualisiert durch ReR** hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="a6e0a-213">**ItemAddedToListEventHandler** fetches the list item that was added, and adds the string **Updated by ReR** to the list item's description.</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="a6e0a-214">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="a6e0a-214">Additional resources</span></span>
<span data-ttu-id="a6e0a-215"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a6e0a-215"></span></span>

-  [<span data-ttu-id="a6e0a-216">Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen</span><span class="sxs-lookup"><span data-stu-id="a6e0a-216">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="a6e0a-217">Core.AppEvents.HandlerDelegation</span><span class="sxs-lookup"><span data-stu-id="a6e0a-217">Core.AppEvents.HandlerDelegation </span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents.HandlerDelegation)
    
