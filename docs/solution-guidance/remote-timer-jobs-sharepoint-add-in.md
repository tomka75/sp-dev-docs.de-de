---
title: "Remote Zeitgeberaufträge in der SharePoint-add-in-Objektmodell"
ms.date: 11/03/2017
ms.openlocfilehash: edd7747655afb18aee647a17e7c4e47d7af0b394
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="remote-timer-jobs-in-the-sharepoint-add-in-model"></a><span data-ttu-id="1bae9-102">Remote Zeitgeberaufträge in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="1bae9-102">Remote timer jobs in the SharePoint add-in model</span></span>
================================================

<a name="summary"></a><span data-ttu-id="1bae9-103">Summary</span><span class="sxs-lookup"><span data-stu-id="1bae9-103">Summary</span></span>
-------

<span data-ttu-id="1bae9-104">Ansatz verwenden Sie zum Implementieren von Zeitgeberaufträgen unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.</span><span class="sxs-lookup"><span data-stu-id="1bae9-104">The approach you take to implement timer jobs is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="1bae9-105">In einer typischen vollständige vertrauen Code (FTC) / SharePoint-Zeitgeberaufträgen Farmlösung Szenario wurden durch den SharePoint Server-Side Object Model Code erstellt, über Farmlösungen bereitgestellt und in der Website der SharePoint-Zentraladministration verwaltet.</span><span class="sxs-lookup"><span data-stu-id="1bae9-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, SharePoint Timer Jobs were created with the SharePoint Server Side Object Model code, deployed via Farm Solutions and managed in the SharePoint Central Administration web site.</span></span> <span data-ttu-id="1bae9-106">SharePoint verarbeitet die Planung und die Ausführung des Zeitgeberauftrags in diesem Szenario.</span><span class="sxs-lookup"><span data-stu-id="1bae9-106">SharePoint handles both the scheduling and the execution of the timer job in this scenario.</span></span> 

<span data-ttu-id="1bae9-107">Im Modell SharePoint-Add-in Szenario Zeitgeberaufträge erstellt und außerhalb von SharePoint geplant.</span><span class="sxs-lookup"><span data-stu-id="1bae9-107">In the SharePoint Add-in model scenario, timer jobs are created and scheduled outside of SharePoint.</span></span>  <span data-ttu-id="1bae9-108">SharePoint ist nicht für die Planung oder die Ausführung des Zeitgeberauftrags in diesem Szenario verantwortlich.</span><span class="sxs-lookup"><span data-stu-id="1bae9-108">SharePoint is not responsible for the scheduling or the execution of the timer job in this scenario.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="1bae9-109">Allgemeine Richtlinien</span><span class="sxs-lookup"><span data-stu-id="1bae9-109">High-Level Guidelines</span></span>
---------------------

<span data-ttu-id="1bae9-110">In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien für das Erstellen von Zeitgeberaufträgen bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="1bae9-110">As a rule of a thumb, we would like to provide the following high-level guidelines for creating timer jobs.</span></span>

- <span data-ttu-id="1bae9-111">Zeitgeberaufträge sollte außerhalb von SharePoint implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="1bae9-111">Timer jobs should be implemented outside of SharePoint.</span></span>
- <span data-ttu-id="1bae9-112">Planen von Zeitgeberaufträgen sollte außerhalb von SharePoint implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="1bae9-112">Scheduling timer jobs should be implemented outside of SharePoint.</span></span>
- <span data-ttu-id="1bae9-113">Zeitgeberaufträge sollte über ein Dienstkonto oder OAuth authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="1bae9-113">Timer jobs should authenticate via a service account or OAuth.</span></span>

<a name="challenges-creating-timer-jobs"></a><span data-ttu-id="1bae9-114">Erstellen von Zeitgeberaufträgen Herausforderungen</span><span class="sxs-lookup"><span data-stu-id="1bae9-114">Challenges creating timer jobs</span></span>
------------------------------

<span data-ttu-id="1bae9-115">Die größte Herausforderung Erstellen von Zeitgeberaufträgen in Office 365-Mandanten zugeordnet ist, dass die Tatsache, dass Sie die Farm bereitstellen können nicht als Lösungen zu Office 365-Instanz Bereich.</span><span class="sxs-lookup"><span data-stu-id="1bae9-115">The biggest challenge associated with creating timer jobs in Office 365 tenancies is the fact that you cannot deploy farm scoped solutions to an Office 365 tenancy.</span></span> <span data-ttu-id="1bae9-116">Ohne eine farmlösung bezogenen kann keinen SharePoint-Zeitgeberauftrag bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="1bae9-116">Without a farm scoped solution, you cannot deploy a SharePoint timer job.</span></span>

<span data-ttu-id="1bae9-117">Die neue Möglichkeit zum Erstellen eines Zeitgeberauftrags ist außerhalb von SharePoint erstellt und zum Verarbeiten von außerhalb von SharePoint als auch planen.</span><span class="sxs-lookup"><span data-stu-id="1bae9-117">The new way to create a timer job is to build it outside of SharePoint and to handle the scheduling outside of SharePoint as well.</span></span> <span data-ttu-id="1bae9-118">Faktoren Sie die folgenden zugeordneten SharePoint-Zeitgeberaufträgen für eine lokale SharePoint-Umgebung.</span><span class="sxs-lookup"><span data-stu-id="1bae9-118">Consider the following factors associated with SharePoint timer jobs for an on-premises SharePoint environment.</span></span>

- <span data-ttu-id="1bae9-119">SharePoint mit Hunderten von Out-of-Box Zeitgeberaufträge, mit denen der SharePoint-Scheduler zu struggles verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="1bae9-119">SharePoint ships with hundreds of out-of-the-box timer jobs that the SharePoint scheduler struggles to keep up with.</span></span>  
<span data-ttu-id="1bae9-120">OK-Sie können die Menge an Arbeitsspeicher und Power reduzieren erforderlich auf dem SharePoint-Server durch die Implementierung verschieben code in Azure oder einer anderen Umgebung.</span><span class="sxs-lookup"><span data-stu-id="1bae9-120">ok- You can reduce the amount of memory and processor power needed on your SharePoint server by moving the implementation code to Azure or another environment.</span></span>
- <span data-ttu-id="1bae9-121">Planung und Implementierung Code für die Zeitgeberaufträge auf einen anderen Server verschieben legt den sharepointserver besser skalierbar und stabil als Ergebnis.</span><span class="sxs-lookup"><span data-stu-id="1bae9-121">Moving the scheduling and implementation code associated with timer jobs to another server makes your SharePoint server more scalable and stable as a result.</span></span>

<a name="options-to-schedule-timer-jobs"></a><span data-ttu-id="1bae9-122">Optionen zum Planen von Zeitgeberaufträgen</span><span class="sxs-lookup"><span data-stu-id="1bae9-122">Options to schedule timer jobs</span></span>
----------------------------

<span data-ttu-id="1bae9-123">Sie haben eine Reihe von Optionen für die Implementierung der Planung für einen Zeitgeberauftrag.</span><span class="sxs-lookup"><span data-stu-id="1bae9-123">You have a couple of options to implement the scheduling for a timer job.</span></span>

- <span data-ttu-id="1bae9-124">Windows-Taskplaner</span><span class="sxs-lookup"><span data-stu-id="1bae9-124">Windows Scheduler</span></span>
    + <span data-ttu-id="1bae9-125">Windows-Dienst</span><span class="sxs-lookup"><span data-stu-id="1bae9-125">Windows Service</span></span>
- <span data-ttu-id="1bae9-126">Azure WebJob</span><span class="sxs-lookup"><span data-stu-id="1bae9-126">Azure WebJob</span></span>
    + <span data-ttu-id="1bae9-127">Azure-Arbeitsprozess</span><span class="sxs-lookup"><span data-stu-id="1bae9-127">Azure worker process</span></span>

<a name="windows-scheduler"></a><span data-ttu-id="1bae9-128">Windows-Taskplaner</span><span class="sxs-lookup"><span data-stu-id="1bae9-128">Windows Scheduler</span></span>
-----------------
<span data-ttu-id="1bae9-129">In diesem Muster verarbeitet die Windows-Taskplaner die Planung Aspekte eines Zeitgeberauftrags zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="1bae9-129">In this pattern, the Windows Scheduler handles the scheduling aspects associated with a timer job.</span></span>  <span data-ttu-id="1bae9-130">Code zur Implementierung möglicherweise eine Konsolenanwendung oder ein PowerShell-Skript oder anderen Code, den die Windows-Taskplaner aufrufen können.</span><span class="sxs-lookup"><span data-stu-id="1bae9-130">Implementation code can be a console application or a PowerShell script or any other code that the Windows Scheduler can invoke.</span></span>

<span data-ttu-id="1bae9-131">**Windows Service Sub-Option** Ein Windows-Dienst hat die gleichen Merkmale wie die Windows-Taskplaner.</span><span class="sxs-lookup"><span data-stu-id="1bae9-131">**Windows Service Sub Option** A Windows Service has the same characteristics as the Windows Scheduler.</span></span> <span data-ttu-id="1bae9-132">Microsoft empfiehlt sich nicht auf dieses Muster, aber es ist erwähnt, da sie häufig verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="1bae9-132">Microsoft does not recommend this pattern but it is worth mentioning because it is commonly used.</span></span>

<span data-ttu-id="1bae9-133">**Ist Windows-Taskplaner geeignet?**</span><span class="sxs-lookup"><span data-stu-id="1bae9-133">**When is Windows Scheduler a good fit?**</span></span>

<span data-ttu-id="1bae9-134">Wenn Sie keinen Zugriff auf ein Azure-Abonnement zum Planen von Zeitgeberaufträgen mit Azure WebJobs ist mit einem Windows-Taskplaner gut geeignet, da diese Option auf allen Computern mit Windows-Betriebssystems implementiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="1bae9-134">When you do not have access to an Azure subscription to schedule timer jobs with Azure WebJobs, Using a Windows Scheduler is a good option because this option may be implemented on any machine with the Windows operating system.</span></span>

- <span data-ttu-id="1bae9-135">Erfordert zusätzliche Hardware zum Ausführen der Windows-Taskplaner.</span><span class="sxs-lookup"><span data-stu-id="1bae9-135">Requires additional hardware to run the Windows Scheduler.</span></span>
- <span data-ttu-id="1bae9-136">Erfordert zusätzliche Hardware, um den Timer Job Code auszuführen.</span><span class="sxs-lookup"><span data-stu-id="1bae9-136">Requires additional hardware to run the timer job code.</span></span>

<span data-ttu-id="1bae9-137">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="1bae9-137">**Getting Started**</span></span>

<span data-ttu-id="1bae9-138">In den folgenden Artikeln verwenden Sie das Windows-Taskplaner Muster und bieten die Codebeispiele, um Ihnen den Einstieg erleichtern.</span><span class="sxs-lookup"><span data-stu-id="1bae9-138">The following articles use the Windows Scheduler pattern and provide code samples to get you started.</span></span>

- [<span data-ttu-id="1bae9-139">Core.SimpleTimerJob (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="1bae9-139">Core.SimpleTimerJob (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)
    + <span data-ttu-id="1bae9-140">End-to-End-Artikel zu diesem Muster mit begleitendem Video.</span><span class="sxs-lookup"><span data-stu-id="1bae9-140">End-to-end article about this pattern with accompanying video.</span></span>
- [<span data-ttu-id="1bae9-141">Core.TimerJobs.Samples (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="1bae9-141">Core.TimerJobs.Samples (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples)
    + <span data-ttu-id="1bae9-142">Hervorragende Codebeispiele 10 verschiedene Beispiele einschließt.</span><span class="sxs-lookup"><span data-stu-id="1bae9-142">Excellent code samples encompassing 10 different examples.</span></span> <span data-ttu-id="1bae9-143">*Hinweis: Nicht alle zehn Codebeispiele gelten für das Windows-Taskplaner-Muster.*</span><span class="sxs-lookup"><span data-stu-id="1bae9-143">*Note: Not all ten code examples are applicable to the Windows Scheduler pattern.*</span></span>

<a name="azure-webjob"></a><span data-ttu-id="1bae9-144">Azure WebJob</span><span class="sxs-lookup"><span data-stu-id="1bae9-144">Azure WebJob</span></span>
------------
<span data-ttu-id="1bae9-145">In diesem Muster der Azure-WebJob behandelt die Planung Aspekte eines Zeitgeberauftrags zugeordnet und enthält den Code zur Implementierung.</span><span class="sxs-lookup"><span data-stu-id="1bae9-145">In this pattern, the Azure WebJob handles the scheduling aspects associated with a timer job and includes the implementation code.</span></span>

- <span data-ttu-id="1bae9-146">Keine erforderlich zusätzliche Hardware zum Ausführen der Azure-WebJob (Planung und Implementierung Code).</span><span class="sxs-lookup"><span data-stu-id="1bae9-146">Does not require additional hardware to run the Azure WebJob (scheduling and implementation code).</span></span>
- <span data-ttu-id="1bae9-147">Vorteilhaft, da sie für die Planung sowie den Code zur Implementierung der Azure-WebJob verwendet, erleichtert die zentral verwalten.</span><span class="sxs-lookup"><span data-stu-id="1bae9-147">Advantageous because it uses the Azure WebJob for scheduling as well as the implementation code, which makes it easy to manage in one location.</span></span>

<span data-ttu-id="1bae9-148">**Azure Worker Sub Serverrollenoption** Ein Azure-Workerrolle hat die gleichen Merkmale wie ein Azure WebJob.</span><span class="sxs-lookup"><span data-stu-id="1bae9-148">**Azure Worker Role Sub Option** An Azure Worker Role has the same characteristics as an Azure WebJob.</span></span> <span data-ttu-id="1bae9-149">Microsoft empfiehlt sich nicht auf dieses Muster, aber es ist erwähnt, da sie häufig verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="1bae9-149">Microsoft does not recommend this pattern but it is worth mentioning because it is commonly used.</span></span>

<span data-ttu-id="1bae9-150">**Ist Azure WebJob geeignet?**</span><span class="sxs-lookup"><span data-stu-id="1bae9-150">**When is Azure WebJob a good fit?**</span></span>

<span data-ttu-id="1bae9-151">Wann haben Sie Zugriff auf ein Azure-Abonnement Zeitgeberaufträge mit Azure WebJobs planen.</span><span class="sxs-lookup"><span data-stu-id="1bae9-151">When you have access to an Azure subscription to schedule timer jobs with Azure WebJobs.</span></span>

<span data-ttu-id="1bae9-152">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="1bae9-152">**Getting Started**</span></span>

<span data-ttu-id="1bae9-153">Die folgenden Artikel beschreiben das Muster Azure WebJob und geben Codebeispiele, um Ihnen den Einstieg.</span><span class="sxs-lookup"><span data-stu-id="1bae9-153">The following articles describe the Azure WebJob pattern and provide code samples to get you started.</span></span>

- [<span data-ttu-id="1bae9-154">Erste Schritte mit Azure WebJobs ("Zeitgeberaufträge") für Ihre Office 365-Websites (Office 365 Plug & Play-Artikel)</span><span class="sxs-lookup"><span data-stu-id="1bae9-154">Getting Started with azure WebJobs ("timer jobs") for your Office 365 Sites (O365 PnP Article)</span></span>](https://github.com/SharePoint/PnP-Guidance/blob/master/articles/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites.md)
    + <span data-ttu-id="1bae9-155">Beschreibt das Erstellen einer Azure WebJob als ein geplanter Auftrag für Ihre Office 365 verwenden, oder klicken Sie mit der lokalen SharePoint-Umgebung.</span><span class="sxs-lookup"><span data-stu-id="1bae9-155">Describes how to build an Azure WebJob to act as a scheduled job for your Office 365 or on-premises SharePoint environment.</span></span> <span data-ttu-id="1bae9-156">Enthält veröffentlichen und Überwachungsinformationen.</span><span class="sxs-lookup"><span data-stu-id="1bae9-156">Includes publishing and monitoring information.</span></span>
- [<span data-ttu-id="1bae9-157">Core.SimpleTimerJob (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="1bae9-157">Core.SimpleTimerJob (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples)
    + <span data-ttu-id="1bae9-158">Hervorragende Codebeispiele 10 verschiedene Beispiele einschließt.</span><span class="sxs-lookup"><span data-stu-id="1bae9-158">Excellent code samples encompassing 10 different examples.</span></span> <span data-ttu-id="1bae9-159">*Hinweis: Nicht alle zehn Codebeispiele sind für das Muster Azure WebJob gelten.*</span><span class="sxs-lookup"><span data-stu-id="1bae9-159">*Note: Not all ten code examples are applicable to the Azure WebJob pattern.*</span></span>

<a name="authentication-options"></a><span data-ttu-id="1bae9-160">Authentifizierungsoptionen</span><span class="sxs-lookup"><span data-stu-id="1bae9-160">Authentication Options</span></span>
----------------------

<span data-ttu-id="1bae9-161">Sie müssen in der Reihenfolge für die Zeitgeberaufträge für die Interaktion mit SharePoint authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="1bae9-161">In order for your timer jobs to interact with SharePoint they must authenticate.</span></span> <span data-ttu-id="1bae9-162">Zurzeit stehen zwei Muster, mit denen Sie Zeitgeberaufträge authentifizieren können.</span><span class="sxs-lookup"><span data-stu-id="1bae9-162">Currently, there are two patterns you may use to authenticate timer jobs.</span></span>

- <span data-ttu-id="1bae9-163">Verwenden eines Dienstkontos</span><span class="sxs-lookup"><span data-stu-id="1bae9-163">Use a service account</span></span>
- <span data-ttu-id="1bae9-164">Verwenden von OAuth</span><span class="sxs-lookup"><span data-stu-id="1bae9-164">Use OAuth</span></span>

<a name="use-a-service-account"></a><span data-ttu-id="1bae9-165">Verwenden eines Dienstkontos</span><span class="sxs-lookup"><span data-stu-id="1bae9-165">Use a service account</span></span>
---------------------
<span data-ttu-id="1bae9-166">In diesem Muster definieren Sie einen oder mehrere Dienstkonten verwendet, um Zeitgeberaufträge authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="1bae9-166">In this pattern, you define one or more service accounts used to authenticate timer jobs.</span></span>

- <span data-ttu-id="1bae9-167">Dienstkonten werden in SharePoint definiert.</span><span class="sxs-lookup"><span data-stu-id="1bae9-167">Service accounts are defined in SharePoint.</span></span>
    + <span data-ttu-id="1bae9-168">In Office 365-Instanz, je nachdem, welche Funktionalität Ihre Zeitgeberaufträge verfügen, die Dienstkonten eine Office 365-Lizenz zugewiesen werden möglicherweise.</span><span class="sxs-lookup"><span data-stu-id="1bae9-168">In an Office 365 tenancy, depending what functionality your timer jobs have, the service accounts may need an Office 365 license assigned to them.</span></span>
    + <span data-ttu-id="1bae9-169">Erstellen Sie Dienstkonten auf einer pro Timer-Job-Basis, oder verwenden Sie ein einzelnes Konto für alle Zeitgeberaufträge.</span><span class="sxs-lookup"><span data-stu-id="1bae9-169">You can create service accounts on a per timer job basis, or use a single account for all timer jobs.</span></span>
    + <span data-ttu-id="1bae9-170">Erstellen Sie klare und beschreibende Namen für die Dienstkonten, damit Sie auf einfache Weise die Vorgänge überwachen können, die sie durchführen.</span><span class="sxs-lookup"><span data-stu-id="1bae9-170">Create clear and descriptive names for the service accounts so you can easily track the operations they perform.</span></span>
    
    <span data-ttu-id="1bae9-171">Beispiel: Wenn des Zeitgeberauftrags Listenelemente geändert wird, zeigt die Spalte geändert von für Listenelemente den Namen des Dienstkontos den Zeitgeberauftrag zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="1bae9-171">For example: If your timer job modifies list items, the Modified By column for the list items will display the name of the service account associated with the timer job.</span></span>

- <span data-ttu-id="1bae9-172">Bei der Authentifizierung mit Dienstkonten müssen Sie einen Benutzernamen und ein Kennwort für das Dienstkonto abrufen.</span><span class="sxs-lookup"><span data-stu-id="1bae9-172">When authenticating with service accounts, you must retrieve a user name and password for the service account.</span></span>
    + <span data-ttu-id="1bae9-173">Der folgende Codeausschnitt veranschaulicht die Verwendung von einen Benutzernamen und ein Kennwort um zu authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="1bae9-173">The code snippet below illustrates using a user name and password to authenticate.</span></span>
    + <span data-ttu-id="1bae9-174">Achten Sie zum Speichern und abrufen, den Benutzernamen und das Kennwort auf sichere Weise.</span><span class="sxs-lookup"><span data-stu-id="1bae9-174">Take care to store and retrieve the user name and password in a secure fashion.</span></span>

    ```
    using (ClientContext context = new ClientContext("https://tenancy.sharepoint.com"))
    {   
        // Use default authentication mode
        context.AuthenticationMode = ClientAuthenticationMode.Default;  
        // Specify the credentials for the account that will execute the request
        context.Credentials = new SharePointOnlineCredentials("User Name", "Password");
    }
    ```

<span data-ttu-id="1bae9-175">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="1bae9-175">**Getting Started**</span></span>

<span data-ttu-id="1bae9-176">In den folgenden Artikeln wird beschrieben, wie ein Dienstkonto authentifizierungsmuster verwenden, und geben Sie Codebeispiele, um Ihnen den Einstieg erleichtern.</span><span class="sxs-lookup"><span data-stu-id="1bae9-176">The following articles describe how to use a service account authentication pattern and provide code samples to get you started.</span></span>

- [<span data-ttu-id="1bae9-177">Erstellen einer SharePoint-App als eines Zeitgeberauftrags (MSDN-Blog)</span><span class="sxs-lookup"><span data-stu-id="1bae9-177">Building a SharePoint App as a Timer Job (MSDN Blog)</span></span>](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx)
    + <span data-ttu-id="1bae9-178">End-to-End-Artikel zu diesem Muster.</span><span class="sxs-lookup"><span data-stu-id="1bae9-178">End-to-end article about this pattern.</span></span>
- [<span data-ttu-id="1bae9-179">Core.SimpleTimerJob (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="1bae9-179">Core.SimpleTimerJob (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)
    + <span data-ttu-id="1bae9-180">End-to-End-Artikel zu diesem Muster mit begleitendem Video.</span><span class="sxs-lookup"><span data-stu-id="1bae9-180">End-to-end article about this pattern with accompanying video.</span></span>
- [<span data-ttu-id="1bae9-181">Core.TimerJobs.Samples (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="1bae9-181">Core.TimerJobs.Samples (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples)
    + <span data-ttu-id="1bae9-182">Hervorragende Codebeispiele 10 verschiedene Beispiele einschließt.</span><span class="sxs-lookup"><span data-stu-id="1bae9-182">Excellent code samples encompassing 10 different examples.</span></span> <span data-ttu-id="1bae9-183">*Hinweis: Nicht alle zehn Codebeispiele gelten für die authentifizierungsmuster für die Service-Konto.*</span><span class="sxs-lookup"><span data-stu-id="1bae9-183">*Note: Not all ten code examples are applicable to the service account authentication pattern.*</span></span>

<a name="use-oauth"></a><span data-ttu-id="1bae9-184">Verwenden von OAuth</span><span class="sxs-lookup"><span data-stu-id="1bae9-184">Use OAuth</span></span>
-----------
<span data-ttu-id="1bae9-185">In diesem Muster definieren eine Anwendung in SharePoint oder Azure Active Directory und die der Anwendung zugeordneten Authentifizierungstoken zur Authentifizierung verwenden.</span><span class="sxs-lookup"><span data-stu-id="1bae9-185">In this pattern, you define an application in SharePoint or Azure Active Directory and use the authentication tokens associated with the application to authenticate.</span></span>

- <span data-ttu-id="1bae9-186">Wenn Sie eine SharePoint-Anwendung mit authentifizieren Sie Erstellen einer app principal und Berechtigungen zuweisen.</span><span class="sxs-lookup"><span data-stu-id="1bae9-186">When using a SharePoint application to authenticate you create an app principal and assign permissions to it.</span></span>
    + <span data-ttu-id="1bae9-187">In diesem Muster möglicherweise Zeitgeberaufträge über eine vom Anbieter gehosteten SharePoint-Add-in oder eine Konsolenanwendung implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="1bae9-187">In this pattern, timer jobs may be implemented via a Provider-hosted SharePoint Add-in or a console application.</span></span>
    + <span data-ttu-id="1bae9-188">Verwenden Sie zum Registrieren eines app-Prinzipals für die SharePoint-Add-in vom Anbieter gehostete oder Konsolenanwendung, die AppRegNew-Seite in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1bae9-188">To register an app principal for the Provider-hosted SharePoint Add-in or console application, use the AppRegNew page in SharePoint.</span></span>
    
    <span data-ttu-id="1bae9-189">Zugriff auf diese Seite unter der folgenden URL http://<tenancy>/<site>/_layouts/AppRegNew.aspx</span><span class="sxs-lookup"><span data-stu-id="1bae9-189">This page is accessed at the following URL  http://<tenancy>/<site>/_layouts/AppRegNew.aspx</span></span>

    + <span data-ttu-id="1bae9-190">Verwenden Sie zum Erteilen von Berechtigungen zu einem app-Prinzipal der Seite AppInv in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1bae9-190">To grant permissions to an app principal, use the AppInv page in SharePoint.</span></span>
    
    <span data-ttu-id="1bae9-191">Zugriff auf diese Seite unter der folgenden URL http://<tenancy>/<site>/_layouts/AppInv.aspx</span><span class="sxs-lookup"><span data-stu-id="1bae9-191">This page is accessed at the following URL  http://<tenancy>/<site>/_layouts/AppInv.aspx</span></span>

- <span data-ttu-id="1bae9-192">Zeitgeberaufträge verwenden nur-App-Berechtigungen, da sie nicht über ein interaktiver Benutzer, der ihnen zugeordneten verfügen.</span><span class="sxs-lookup"><span data-stu-id="1bae9-192">Timer jobs use App Only permissions because they do not have an interactive user associated with them.</span></span> 
    + <span data-ttu-id="1bae9-193">Der folgende Codeausschnitt veranschaulicht ein Zugriffstoken beziehen und Verwenden von nur-App-Berechtigungen in SharePoint zu authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="1bae9-193">The code snippet below illustrates obtaining an access token and using App Only permissions to authenticate to SharePoint.</span></span>

    ```
    string accessToken = TokenHelper.GetAppOnlyAccessToken(TokenHelper.SharePointPrincipal, siteUri.Authority, realm).AccessToken;
    
    using(var clientContext = TokenHelper.GetClientContextWithAccessToken(siteUri.ToString(),accessToken))
    {
        //Implement timer job code
    }
    ```

- <span data-ttu-id="1bae9-194">Bei Verwendung einer Anwendung Azure Active Directory authentifiziert, die Sie erstellen eine Azure Active Directory-Anwendung in der Azure-Verwaltungsportal und Berechtigungen zuweisen.</span><span class="sxs-lookup"><span data-stu-id="1bae9-194">When using an Azure Active Directory application to authenticate, you create an Azure Active Directory application in the Azure Management Portal and assign permissions to it.</span></span>
    + <span data-ttu-id="1bae9-195">In diesem Muster möglicherweise Zeitgeberaufträge über eine vom Anbieter gehosteten SharePoint-Add-in oder eine Konsolenanwendung implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="1bae9-195">In this pattern, timer jobs may be implemented via a Provider-hosted SharePoint Add-in or a console application.</span></span>
    + <span data-ttu-id="1bae9-196">In diesem Muster interagieren Sie mit der Active Directory-Authentifizierungsbibliothek oder die Microsoft Graph-API, um ein Zugriffstoken abzurufen.</span><span class="sxs-lookup"><span data-stu-id="1bae9-196">In this pattern, you interact with the Active Directory Authentication Library or the Microsoft Graph API to retrieve an access token.</span></span>
    + <span data-ttu-id="1bae9-197">Das Zugriffstoken wird zur Authentifizierung in SharePoint (und möglicherweise andere Office 365-Diensten in Office 365-Instanz) verwendet.</span><span class="sxs-lookup"><span data-stu-id="1bae9-197">The access token is used to authenticate to SharePoint (and possibly other Office 365 services in an Office 365 tenancy).</span></span>

<span data-ttu-id="1bae9-198">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="1bae9-198">**Getting Started**</span></span>

<span data-ttu-id="1bae9-199">Die folgenden Artikel beschreiben das Muster der OAUth-Authentifizierung und geben Codebeispiele, um Ihnen den Einstieg erleichtern.</span><span class="sxs-lookup"><span data-stu-id="1bae9-199">The following articles describe the OAUth authentication pattern and provide code samples to get you started.</span></span>

- [<span data-ttu-id="1bae9-200">Erstellen einer SharePoint-App als eines Zeitgeberauftrags (MSDN-Blog)</span><span class="sxs-lookup"><span data-stu-id="1bae9-200">Building a SharePoint App as a Timer Job (MSDN Blog)</span></span>](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx)
    + <span data-ttu-id="1bae9-201">End-to-End-Artikel zu diesem Muster.</span><span class="sxs-lookup"><span data-stu-id="1bae9-201">End-to-end article about this pattern.</span></span>
- [<span data-ttu-id="1bae9-202">Core.TimerJobs.Samples (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="1bae9-202">Core.TimerJobs.Samples (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples)
    + <span data-ttu-id="1bae9-203">Hervorragende Codebeispiele 10 verschiedene Beispiele einschließt.</span><span class="sxs-lookup"><span data-stu-id="1bae9-203">Excellent code samples encompassing 10 different examples.</span></span> <span data-ttu-id="1bae9-204">*Hinweis: Nicht alle zehn Codebeispiele gelten für das Muster der OAUth-Authentifizierung.*</span><span class="sxs-lookup"><span data-stu-id="1bae9-204">*Note: Not all ten code examples are applicable to the OAUth authentication pattern.*</span></span>

<a name="related-links"></a><span data-ttu-id="1bae9-205">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="1bae9-205">Related links</span></span>
=============
- [<span data-ttu-id="1bae9-206">Azure WebJob Ressourcen (Azure-Dokumentation)</span><span class="sxs-lookup"><span data-stu-id="1bae9-206">Azure WebJob resources (Azure Documentation)</span></span>](http://azure.microsoft.com/en-us/documentation/articles/websites-webjobs-resources/)
- [<span data-ttu-id="1bae9-207">Bereitstellen von WebJobs mithilfe von Visual Studio (Azure-Dokumentation)</span><span class="sxs-lookup"><span data-stu-id="1bae9-207">Deploy WebJobs using Visual Studio (Azure Documentation)</span></span>](http://azure.microsoft.com/en-us/documentation/articles/websites-dotnet-deploy-webjobs/)
- <span data-ttu-id="1bae9-208">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="1bae9-208">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="1bae9-209">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="1bae9-209">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="1bae9-210">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="1bae9-210">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="1bae9-211">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="1bae9-211">Related PnP samples</span></span>
===================

- [<span data-ttu-id="1bae9-212">Core.SimpleTimerJob (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="1bae9-212">Core.SimpleTimerJob (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)
- [<span data-ttu-id="1bae9-213">Core.TimerJobs.Samples (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="1bae9-213">Core.TimerJobs.Samples (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples)
- [<span data-ttu-id="1bae9-214">Provisioning.Services.SiteManager (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="1bae9-214">Provisioning.Services.SiteManager (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Services.SiteManager)
- [<span data-ttu-id="1bae9-215">Provisioning.SiteCollectionCreation (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="1bae9-215">Provisioning.SiteCollectionCreation (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteCollectionCreation)
- <span data-ttu-id="1bae9-216">Beispiele und Inhalte am https://github.com/SharePoint/PnP</span><span class="sxs-lookup"><span data-stu-id="1bae9-216">Samples and content at https://github.com/SharePoint/PnP</span></span>

<a name="applies-to"></a><span data-ttu-id="1bae9-217">Gilt für</span><span class="sxs-lookup"><span data-stu-id="1bae9-217">Applies to</span></span>
==========
- <span data-ttu-id="1bae9-218">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="1bae9-218">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="1bae9-219">Office 365 dedizierte (D) *teilweise*</span><span class="sxs-lookup"><span data-stu-id="1bae9-219">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="1bae9-220">SharePoint 2013 lokal – *teilweise*</span><span class="sxs-lookup"><span data-stu-id="1bae9-220">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="1bae9-221">*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*</span><span class="sxs-lookup"><span data-stu-id="1bae9-221">*Patterns for dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
