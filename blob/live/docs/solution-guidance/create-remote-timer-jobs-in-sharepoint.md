---
title: "Erstellen Sie remote Zeitgeberaufträge in SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 12f4abd507328afd19da562c8dbb569118bc91a9
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="create-remote-timer-jobs-in-sharepoint"></a><span data-ttu-id="23cd7-102">Erstellen Sie remote Zeitgeberaufträge in SharePoint</span><span class="sxs-lookup"><span data-stu-id="23cd7-102">Create remote timer jobs in SharePoint</span></span>

<span data-ttu-id="23cd7-103">Erstellen Sie remote Zeitgeberaufträge in SharePoint Hintergrund Aufgaben zum Verwalten von oder Ihrer Umgebung steuern.</span><span class="sxs-lookup"><span data-stu-id="23cd7-103">Create remote timer jobs in SharePoint to perform background tasks to manage or govern your environment.</span></span>

<span data-ttu-id="23cd7-104">_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="23cd7-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="23cd7-105">Erstellen Sie remote Zeitgeberaufträge zum Verwalten von SharePoint durch Überwachung und Aktion zu SharePoint-Daten.</span><span class="sxs-lookup"><span data-stu-id="23cd7-105">Create remote timer jobs to manage SharePoint by monitoring and taking action on SharePoint data.</span></span> <span data-ttu-id="23cd7-106">Remote Zeitgeberaufträge auf dem SharePoint-Server nicht ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="23cd7-106">Remote timer jobs do not run on your SharePoint server.</span></span> <span data-ttu-id="23cd7-107">Stattdessen werden remote Zeitgeberaufträge geplante Vorgänge, die auf einem anderen Server ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="23cd7-107">Instead remote timer jobs are scheduled tasks that run on another server.</span></span> <span data-ttu-id="23cd7-108">Beispiele dafür, wie Zeitgeberaufträge verwendet werden können:</span><span class="sxs-lookup"><span data-stu-id="23cd7-108">Examples of how timer jobs are used include:</span></span>

- <span data-ttu-id="23cd7-109">Governance Aufgaben wie auf der Website eine Meldung angezeigt, wenn bestimmte Kriterien nicht erfüllt sind, oder erzwingen Aufbewahrungsrichtlinien ausführen.</span><span class="sxs-lookup"><span data-stu-id="23cd7-109">Performing governance tasks, such as displaying a message on the site when certain criteria are not met, or enforcing retention policies.</span></span>
    
- <span data-ttu-id="23cd7-110">Ausgeführt geplanten Prozesse, die intensive Prozessor sind.</span><span class="sxs-lookup"><span data-stu-id="23cd7-110">Running scheduled processes that are processor intensive.</span></span>

## <a name="before-you-begin-to-create-a-remote-timer-job"></a><span data-ttu-id="23cd7-111">Bevor Sie beginnen, erstellen Sie einen remote-Zeitgeberauftrag</span><span class="sxs-lookup"><span data-stu-id="23cd7-111">Before you begin to create a remote timer job</span></span>

<span data-ttu-id="23cd7-112">Laden Sie Sie zuerst [Core.TimerJobs.Samples](https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="23cd7-112">To get started, download the [Core.TimerJobs.Samples ](https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="23cd7-113">Vor der Verwendung der Lösung Core.TimerJobs.Samples, müssen Sie ein Startprojekt, beispielsweise das SimpleJob Projekt auswählen von öffnen das Kontextmenü (Rechtsklick) das **Core.TimerJobs.Samples.SimpleJob**auswählen und dann **festgelegt als Startprojekt**.</span><span class="sxs-lookup"><span data-stu-id="23cd7-113">To start using the Core.TimerJobs.Samples solution, you need to select a startup project, for example the SimpleJob project, by opening the shortcut menu for (right-clicking) the  **Core.TimerJobs.Samples.SimpleJob**, and then choosing  **Set as StartUp Project**.</span></span>

<span data-ttu-id="23cd7-114">**Hinweis:**  Bei der Erstellung eines neuen Projekts in Visual Studio zum Erstellen des neuen remote-Zeitgeberauftrags, das **OfficeDevPnP.Core** NuGet-Paket dem Projekt hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="23cd7-114">**Note:**  When you create a new project in Visual Studio, to start building your new remote timer job, add the  **OfficeDevPnP.Core** NuGet package to your project.</span></span> <span data-ttu-id="23cd7-115">Wählen Sie in Visual Studio **TOOLS** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="23cd7-115">In Visual Studio, choose **TOOLS** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**.</span></span>

## <a name="schedule-your-remote-timer-job"></a><span data-ttu-id="23cd7-116">Planen des remote-Zeitgeberauftrags</span><span class="sxs-lookup"><span data-stu-id="23cd7-116">Schedule your remote timer job</span></span>

<span data-ttu-id="23cd7-117">Ein Zeitgeberauftrag einmal ausführen geplant werden kann oder ein wiederkehrendes Projekt handeln.</span><span class="sxs-lookup"><span data-stu-id="23cd7-117">A timer job can be scheduled to run once or can be a recurring job.</span></span> <span data-ttu-id="23cd7-118">Planen des remote-Zeitgeberauftrags in Ihrer produktionsumgebung, müssen Sie zum Kompilieren des Codes in einer .exe-Datei, und führen Sie die .exe-Datei mithilfe von Windows-Taskplaner oder eine Microsoft Azure WebJob.</span><span class="sxs-lookup"><span data-stu-id="23cd7-118">To schedule your remote timer job in your production environment, you need to compile your code into an .exe file, and then run the .exe file using Windows Task Scheduler or an Microsoft Azure WebJob.</span></span> <span data-ttu-id="23cd7-119">Erfahren Sie unter [Timer Job-Bereitstellungsoptionen](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md#timer-job-deployment-options).</span><span class="sxs-lookup"><span data-stu-id="23cd7-119">You can learn more at [Timer job deployment options](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md#timer-job-deployment-options).</span></span>

## <a name="use-the-coretimerjobssamplessimplejob-add-in"></a><span data-ttu-id="23cd7-120">Verwenden des Core.TimerJobs.Samples.SimpleJob-add-Ins</span><span class="sxs-lookup"><span data-stu-id="23cd7-120">Use the Core.TimerJobs.Samples.SimpleJob add-in</span></span>

<span data-ttu-id="23cd7-121">In Core.TimerJobs.Samples.SimpleJob führt **Main** in Program.cs die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="23cd7-121">In Core.TimerJobs.Samples.SimpleJob,  **Main** in Program.cs performs the following steps:</span></span>

1. <span data-ttu-id="23cd7-122">Erstellt ein SimpleJob-Objekt, das von der Basisklasse [OfficeDevPnP.Core.Framework.TimerJobs.TimerJob](https://github.com/SharePoint/PnP/blob/dev/OfficeDevPnP.Core/OfficeDevPnP.Core/Framework/TimerJobs/TimerJob.cs) erbt.</span><span class="sxs-lookup"><span data-stu-id="23cd7-122">Creates a SimpleJob object, which inherits from the [OfficeDevPnP.Core.Framework.TimerJobs.TimerJob](https://github.com/SharePoint/PnP/blob/dev/OfficeDevPnP.Core/OfficeDevPnP.Core/Framework/TimerJobs/TimerJob.cs) base class.</span></span>
    
2. <span data-ttu-id="23cd7-123">Legt die Anmeldeinformationen des Office 365-Benutzer zu verwenden, wenn den Zeitgeberauftrag mit **TimerJob.UseOffice365Authentication**ausführen.</span><span class="sxs-lookup"><span data-stu-id="23cd7-123">Sets the Office 365 user credentials to use when running the timer job using  **TimerJob.UseOffice365Authentication**.</span></span> <span data-ttu-id="23cd7-124">Die Anmeldeinformationen des Benutzers benötigen Zugriff auf die Websitesammlungen.</span><span class="sxs-lookup"><span data-stu-id="23cd7-124">The user credentials must have appropriate access to the site collections.</span></span> <span data-ttu-id="23cd7-125">Erfahren Sie unter [Authentifizierung](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="23cd7-125">You can learn more at [Authentication](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md#authentication).</span></span>
    
3. <span data-ttu-id="23cd7-126">Fügt die Websites, die der Zeitgeberauftrag zur Verwendung von **TimerJob.AddSite**Aufgaben auszuführen.</span><span class="sxs-lookup"><span data-stu-id="23cd7-126">Adds sites that the timer job should perform tasks on using  **TimerJob.AddSite**.</span></span> <span data-ttu-id="23cd7-127">Optional können Sie wiederholen Sie die **TimerJob.AddSite** -Anweisung, um mehr als einen Standort hinzuzufügen, oder fügen alle Websites unter einer bestimmten URL mithilfe von Platzhalterzeichen *. Beispielsweise http://contoso.sharepoint.com/sites/* wird auf alle Websites unter der verwaltete **Sites** -Pfad den Zeitgeberauftrag ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="23cd7-127">Optionally, you can repeat the **TimerJob.AddSite** statement to add more than one site, or add all sites under a particular URL using the wildcard character *. For example, http://contoso.sharepoint.com/sites/* will run the timer job on all sites under the **sites** managed path.</span></span>
    
4. <span data-ttu-id="23cd7-128">Druckt Timer-Job-Informationen und führt den Zeitgeberauftrag mithilfe von **PrintJobSettingsAndRunJob**.</span><span class="sxs-lookup"><span data-stu-id="23cd7-128">Prints timer job information and runs the timer job using  **PrintJobSettingsAndRunJob**.</span></span>

<span data-ttu-id="23cd7-129">**Hinweis:**  Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="23cd7-129">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
 static void Main(string[] args)
        {
            SimpleJob simpleJob = new SimpleJob();
            
            // The user credentials must have access to the site collections you supply.
            simpleJob.UseOffice365Authentication(User, Password);

            // Use the following code if you are using SharePoint Server 2013 on-premises. 
            //simpleJob.UseNetworkCredentialsAuthentication(User, Password, Domain);
            
            // Add one or more sites that the timer job should work with.
            simpleJob.AddSite("https://contoso.sharepoint.com/sites/dev");
            
            // Prints timer job information and then calls Run().
            PrintJobSettingsAndRunJob(simpleJob);
        }
```

<span data-ttu-id="23cd7-130">Wenn das **SimpleJob** -Objekt instanziiert wird, den Konstruktor **SimpleJob** :</span><span class="sxs-lookup"><span data-stu-id="23cd7-130">When the  **simpleJob** object is instantiated, the **SimpleJob** constructor:</span></span>

1. <span data-ttu-id="23cd7-131">Ruft den allgemeinen Basisklassenkonstruktor.</span><span class="sxs-lookup"><span data-stu-id="23cd7-131">Calls the TimerJob base class constructor.</span></span> 
    
2. <span data-ttu-id="23cd7-132">Weist den **SimpleJob_TimerJobRun** -Ereignishandler die **TimerJobRun** Ereignisse behandeln.</span><span class="sxs-lookup"><span data-stu-id="23cd7-132">Assigns the  **SimpleJob_TimerJobRun** event handler to handle the **TimerJobRun** events.</span></span> <span data-ttu-id="23cd7-133">**SimpleJob_TimerJobRun** ausgeführt, wenn ein Aufruf **TimerJob.Run**, erfolgt die weiter unten in diesem Artikel ausführlich beschrieben wird.</span><span class="sxs-lookup"><span data-stu-id="23cd7-133">**SimpleJob_TimerJobRun** runs when a call is made to **TimerJob.Run**, which is described in more detail later in this article.</span></span>

```C#
public SimpleJob() : base("SimpleJob")
        {
            TimerJobRun += SimpleJob_TimerJobRun;
        }
```

<span data-ttu-id="23cd7-134">Wenn **PrintJobSettingsAndRunJob** ausgeführt wird, wird die Ausgabe aus der allgemeinen im Konsolenfenster geschrieben, und klicken Sie dann **TimerJob.Run** aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="23cd7-134">When  **PrintJobSettingsAndRunJob** runs, output from the TimerJob is written to the console window, and then **TimerJob.Run** is called.</span></span>

```C#
 private static void PrintJobSettingsAndRunJob(TimerJob job)
        {
            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("************************************************");
            Console.WriteLine("Job name: {0}", job.Name);
            Console.WriteLine("Job version: {0}", job.Version);
            Console.WriteLine("Use threading: {0}", job.UseThreading);
            Console.WriteLine("Maximum threads: {0}", job.MaximumThreads);
            Console.WriteLine("Expand sub sites: {0}", job.ExpandSubSites);
            Console.WriteLine("Authentication type: {0}", job.AuthenticationType);
            Console.WriteLine("Manage state: {0}", job.ManageState);
            Console.WriteLine("SharePoint version: {0}", job.SharePointVersion);
            Console.WriteLine("************************************************");
            Console.ForegroundColor = ConsoleColor.Gray;

            // Run job.
            job.Run();
        }
```

<span data-ttu-id="23cd7-135">**TimerJob.Run** löst **TimerJobRun** Ereignisse.</span><span class="sxs-lookup"><span data-stu-id="23cd7-135">**TimerJob.Run** raises **TimerJobRun** events.</span></span> <span data-ttu-id="23cd7-136">**TimerJob.Run** ruft **SimpleJob_TimerJobRun** in SimpleJob.cs, der zum Verarbeiten von Ereignissen in den Konstruktor **SimpleJob** **TimerJobRun** als Ereignishandler festgelegt.</span><span class="sxs-lookup"><span data-stu-id="23cd7-136">**TimerJob.Run** calls **SimpleJob_TimerJobRun** in SimpleJob.cs, which you set as the event handler to handle **TimerJobRun** events in the constructor of **SimpleJob**.</span></span> <span data-ttu-id="23cd7-137">In **SimpleJob_TimerJobRun**können Sie den benutzerdefinierten Code hinzufügen, den des Zeitgeberauftrags ausführen, wenn der Zeitgeberauftrag ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="23cd7-137">In **SimpleJob_TimerJobRun**, you can add your custom code that you want your timer job to perform when the timer job runs.</span></span> <span data-ttu-id="23cd7-138">**SimpleJob_TimerJobRun** führt den benutzerdefinierten Code auf die Websites, die Sie hinzugefügt haben, verwenden **TimerJob.AddSite** in Program.cs.</span><span class="sxs-lookup"><span data-stu-id="23cd7-138">**SimpleJob_TimerJobRun** runs your custom code on the sites you added using **TimerJob.AddSite** in Program.cs.</span></span> <span data-ttu-id="23cd7-139">In diesem Codebeispiel wird mit **SimpleJob_TimerJobRun** der **ClientContext** aus der **allgemeinen** den Titel der Website im Konsolenfenster geschrieben.</span><span class="sxs-lookup"><span data-stu-id="23cd7-139">In this code sample, **SimpleJob_TimerJobRun** uses the **ClientContext** from the **TimerJob** to write the title of the site to the console window.</span></span> <span data-ttu-id="23cd7-140">Wenn mehrere Websites mithilfe von **TimerJob.AddSite** hinzugefügt wurden, wird die **SimpleJob_TimerJobRun** für jede Website aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="23cd7-140">If multiple sites were added using **TimerJob.AddSite** , **SimpleJob_TimerJobRun** is called for each site.</span></span>

```C#
 void SimpleJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
        {
            e.WebClientContext.Load(e.WebClientContext.Web, p => p.Title);
            e.WebClientContext.ExecuteQueryRetry();
            Console.WriteLine("Site {0} has title {1}", e.Url, e.WebClientContext.Web.Title);
        }
```

## <a name="example-content-type-retention-enforcement-timer-job"></a><span data-ttu-id="23cd7-141">Beispiel: Inhaltstyp Aufbewahrung Erzwingung Zeitgeberauftrag</span><span class="sxs-lookup"><span data-stu-id="23cd7-141">Example: Content type retention enforcement timer job</span></span>

<span data-ttu-id="23cd7-142">Das Projekt Core.TimerJobs.Samples.ContentTypeRetentionEnforcementJob zeigt, wie Sie SharePoint-Zeitgeberaufträgen zum Erzwingen von Aufbewahrungsrichtlinien für Inhaltstypen verwenden können.</span><span class="sxs-lookup"><span data-stu-id="23cd7-142">The Core.TimerJobs.Samples.ContentTypeRetentionEnforcementJob project shows how you can use SharePoint timer jobs to enforce retention policies on content types.</span></span> <span data-ttu-id="23cd7-143">Verwenden das **ContentTypeRetentionPolicyPeriod** -Element in app.config, angeben:</span><span class="sxs-lookup"><span data-stu-id="23cd7-143">Using the  **ContentTypeRetentionPolicyPeriod** element in app.config, specify:</span></span>

-  <span data-ttu-id="23cd7-144">**Schlüssel**, den Inhaltstyp-ID des Inhaltstyps, für die die Aufbewahrungsdauer gilt.</span><span class="sxs-lookup"><span data-stu-id="23cd7-144">**key**, which is the content type ID of the content type that the retention period applies to.</span></span>
    
-  <span data-ttu-id="23cd7-145">**Wert**, der die Aufbewahrungszeit in Tagen darstellt.</span><span class="sxs-lookup"><span data-stu-id="23cd7-145">**value**, which is the retention period in days.</span></span> <span data-ttu-id="23cd7-146">Die Aufbewahrungsdauer wird für alle Listenelemente mit der im **Schlüssel**angegebene Inhaltstyp erstellt angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="23cd7-146">The retention period will be applied to all list items created using the content type specified in **key**.</span></span>

```XML
<ContentTypeRetentionPolicyPeriod>
    <!-- Key is the content type ID, and value is the retention period in days -->
    <!-- Specifies an audio content type should be kept for 183 days -->
    <add key="0x0101009148F5A04DDD49cbA7127AADA5FB792B006973ACD696DC4858A76371B2FB2F439A" value="183" />
    <!-- Specifies a document content type should be kept for 365 days -->   
    <add key="0x0101" value="365" />
</ContentTypeRetentionPolicyPeriod>
```

<span data-ttu-id="23cd7-147">**ContentTypeRetentionEnforcementJob_TimerJobRun** wird als den Ereignishandler für das Ereignis **TimerJobRun** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="23cd7-147">**ContentTypeRetentionEnforcementJob_TimerJobRun** is set as the event handler for the **TimerJobRun** event.</span></span> <span data-ttu-id="23cd7-148">Wenn **TimerJob.Run** in Program.cs aufgerufen wird, führt **ContentTypeRetentionEnforcementJob_TimerJobRun** die folgenden Schritte auf jeder Website durch, die mit **TimerJob.AddSite** in Program.cs hinzugefügt wurde:</span><span class="sxs-lookup"><span data-stu-id="23cd7-148">When **TimerJob.Run** is called in Program.cs, **ContentTypeRetentionEnforcementJob_TimerJobRun** performs the following steps on each site that was added using **TimerJob.AddSite** in Program.cs:</span></span>


1. <span data-ttu-id="23cd7-149">Ruft alle Dokumentbibliotheken auf der Website ab.</span><span class="sxs-lookup"><span data-stu-id="23cd7-149">Gets all document libraries on the site.</span></span>
    
2. <span data-ttu-id="23cd7-150">Für jedes Dokument-Bibliothek auf der Website liest die Konfigurationsinformationen in **ContentTypeRetentionPolicyPeriod** in ' App.config ' angegeben. Für jeden Inhaltstyp-ID und Aufbewahrung Period Pair, die von ' App.config ' gelesen wurde, wird die **ApplyRetentionPolicy** aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="23cd7-150">For each document library on the site, reads the configuration information specified in  **ContentTypeRetentionPolicyPeriod** in app.config. For each content type ID and retention period pair that was read from app.config, **ApplyRetentionPolicy** is called.</span></span>

```C#
 void ContentTypeRetentionEnforcementJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
        {
            try
            {
                Log.Info("ContentTypeRetentionEnforcementJob", "Scanning web {0}", e.Url);

                // Get all document libraries. Lists are excluded.
                var documentLibraries = GetAllDocumentLibrariesInWeb(e.WebClientContext, e.WebClientContext.Web);

                // Iterate through all document libraries.
                foreach (var documentLibrary in documentLibraries)
                {
                    Log.Info("ContentTypeRetentionEnforcementJob", "Scanning library {0}", documentLibrary.Title);

                    // Iterate through configured content type retention policies specified in app.config.
                    foreach (var contentTypeName in configContentTypeRetentionPolicyPeriods.Keys)
                    {
                        var retentionPeriods = configContentTypeRetentionPolicyPeriods.GetValues(contentTypeName as string);
                        if (retentionPeriods != null)
                        {
                            var retentionPeriod = int.Parse(retentionPeriods[0]);
                            ApplyRetentionPolicy(e.WebClientContext, documentLibrary, contentTypeName, retentionPeriod);
                        }
                    }
                }
            }
            catch(Exception ex)
            {
                Log.Error("ContentTypeRetentionEnforcementJob", "Exception processing site {0}. Exception is {1}", e.Url, ex.Message);
            }
        }
```

<span data-ttu-id="23cd7-151">**ApplyRetentionPolicy** erzwingt Ihrer benutzerdefinierten Retention Policy Aktionen durch:</span><span class="sxs-lookup"><span data-stu-id="23cd7-151">**ApplyRetentionPolicy** enforces your custom retention policy actions by:</span></span>

1. <span data-ttu-id="23cd7-152">**ValidationDate**zu berechnen.</span><span class="sxs-lookup"><span data-stu-id="23cd7-152">Calculating  **validationDate**.</span></span> <span data-ttu-id="23cd7-153">Die **ApplyRetentionPolicy** -Methode erzwingt Retention Policy Aktionen für Dokumente, die vor **ValidationDate**geändert.</span><span class="sxs-lookup"><span data-stu-id="23cd7-153">The **ApplyRetentionPolicy** method enforces retention policy actions on documents modified before **validationDate**.</span></span> <span data-ttu-id="23cd7-154">Klicken Sie dann **ValidationDate** wird als CAML Datum formatiert und **CamlDate**zugewiesen ist.</span><span class="sxs-lookup"><span data-stu-id="23cd7-154">Then **validationDate** is formatted as a CAML date and is assigned to **camlDate**.</span></span>
    
2. <span data-ttu-id="23cd7-155">CAML-Abfrage zum Filtern von Dokumenten in der Dokumentbibliothek basierend auf den Inhaltstyp-ID, die in ' App.config ' angegeben wurde, und das Datum **Geändert von** kleiner ist als **CamlDate**ausführen.</span><span class="sxs-lookup"><span data-stu-id="23cd7-155">Running a CAML query to filter documents in the document library based on the content type ID, which was specified in app.config, and where the  **Modified By** date is less than **camlDate**.</span></span>
    
3. <span data-ttu-id="23cd7-156">Für jedes Listenelement Anwenden von benutzerdefinierten aufbewahrungsaktionen auf die Dokumente mithilfe von benutzerdefiniertem Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="23cd7-156">For each list item, applying custom retention actions to perform on the documents using custom code.</span></span>

```C#
private void ApplyRetentionPolicy(ClientContext clientContext, List documentLibrary, object contentTypeId, int retentionPeriodDays)
        {
            // Calculate validation date. You need to enforce the retention policy on any document modified before validation date.
            var validationDate = DateTime.Now.AddDays(-retentionPeriodDays);
            var camlDate = validationDate.ToString("yyyy-MM-ddTHH:mm:ssZ");

            // Get old documents in the library that match the content type.
            if (documentLibrary.ItemCount > 0)
            {
                var camlQuery = new CamlQuery();
                
                camlQuery.ViewXml = String.Format(
                    @"<View>
                        <Query>
                            <Where><And>
                                <BeginsWith><FieldRef Name='ContentTypeId'/><Value Type='ContentTypeId'>{0}</Value></BeginsWith>
                                <Lt><FieldRef Name='Modified' /><Value Type='DateTime'>{1}</Value></Lt>
                            </And></Where>
                        </Query>
                    </View>", contentTypeId, camlDate);

                var listItems = documentLibrary.GetItems(camlQuery);
                clientContext.Load(listItems,
                    items => items.Include(
                        item => item.Id,
                        item => item.DisplayName,
                        item => item.ContentType));

                clientContext.ExecuteQueryRetry(); 

                foreach (var listItem in listItems)
                {
                    Log.Info("ContentTypeRetentionEnforcementJob", "Document '{0}' has been modified earlier than {1}. Retention policy will be applied.", listItem.DisplayName, validationDate);
                    Console.WriteLine("Document '{0}' has been modified earlier than {1}. Retention policy will be applied.", listItem.DisplayName, validationDate);
                    
                    // Apply your custom retention actions here. For example, archiving documents, or starting a disposition workflow.
                }
            }
        }
```

## <a name="example-governance-timer-job"></a><span data-ttu-id="23cd7-157">Beispiel: Governance-Zeitgeberauftrag</span><span class="sxs-lookup"><span data-stu-id="23cd7-157">Example: Governance timer job</span></span>

<span data-ttu-id="23cd7-158">Das Projekt Core.TimerJobs.Samples.GovernanceJob Zeitgeberaufträge verwendet, um sicherzustellen, dass zwei Administratoren Ihrer Websitesammlungen zugeordnet sind, und wenn nicht, wird eine Benachrichtigung auf der Website angezeigt.</span><span class="sxs-lookup"><span data-stu-id="23cd7-158">The Core.TimerJobs.Samples.GovernanceJob project uses timer jobs to ensure two administrators are assigned to your site collections, and if not, displays a notification message on the site.</span></span>

<span data-ttu-id="23cd7-159">**SiteGovernanceJob_TimerJobRun** wird als den Ereignishandler für das Ereignis **TimerJobRun** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="23cd7-159">**SiteGovernanceJob_TimerJobRun** is set as the event handler for the **TimerJobRun** event.</span></span> <span data-ttu-id="23cd7-160">Wenn **TimerJob.Run** in Program.cs aufgerufen wird, führt **SiteGovernanceJob_TimerJobRun** die folgenden Schritte für jede Websitesammlung, die mit **TimerJob.AddSite** in Program.cs hinzugefügt wurde:</span><span class="sxs-lookup"><span data-stu-id="23cd7-160">When **TimerJob.Run** is called in Program.cs, **SiteGovernanceJob_TimerJobRun** performs the following steps on each site collection that was added using **TimerJob.AddSite** in Program.cs:</span></span>

1. <span data-ttu-id="23cd7-161">Ruft die Anzahl der Administratoren in der Websitesammlung mithilfe der Extension-Methode [GetAdministrators](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/SecurityExtensions.cs) [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core)gehört.</span><span class="sxs-lookup"><span data-stu-id="23cd7-161">Gets the number of administrators assigned to the site collection using the extension method [GetAdministrators](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/SecurityExtensions.cs) which is part of [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core).</span></span>
    
2. <span data-ttu-id="23cd7-162">Lädt die JavaScript-Datei in der Liste SiteAssets oder Formatbibliothek mit [UploadFile](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/FileFolderExtensions.cs), der Teil des [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core)ist hoch.</span><span class="sxs-lookup"><span data-stu-id="23cd7-162">Uploads the JavaScript file to the SiteAssets or Style Library list using [UploadFile](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/FileFolderExtensions.cs), which is part of [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core).</span></span> 
    
3. <span data-ttu-id="23cd7-163">Wenn der Standort weniger als zwei Administratoren verfügt, fügt [AddJSLink](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/JavaScriptExtensions.cs) eine Benachrichtigung zu einer Website mithilfe von JavaScript.</span><span class="sxs-lookup"><span data-stu-id="23cd7-163">If the site has less than two administrators, [AddJSLink](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/JavaScriptExtensions.cs) adds a notification message to a site using JavaScript.</span></span> <span data-ttu-id="23cd7-164">Erfahren Sie unter [Anpassen der Benutzeroberfläche mithilfe von JavaScript für die SharePoint-Website](Customize-your-SharePoint-site-UI-by-using-JavaScript.md).</span><span class="sxs-lookup"><span data-stu-id="23cd7-164">You can learn more at [Customize your SharePoint site UI by using JavaScript](Customize-your-SharePoint-site-UI-by-using-JavaScript.md).</span></span>
    
4. <span data-ttu-id="23cd7-165">Wenn die Website zwei oder mehr Administratoren verfügt, wird die Benachrichtigung mit [DeleteJsLink](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/JavaScriptExtensions.cs)entfernt.</span><span class="sxs-lookup"><span data-stu-id="23cd7-165">If the site has two or more administrators, the notification message is removed using [DeleteJsLink](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/JavaScriptExtensions.cs).</span></span>

```C#
void SiteGovernanceJob_TimerJobRun(object o, TimerJobRunEventArgs e)
        {
            try
            {
                string library = "";

                // Get the number of administrators.
                var admins = e.WebClientContext.Web.GetAdministrators();

                Log.Info("SiteGovernanceJob", "ThreadID = {2} | Site {0} has {1} administrators.", e.Url, admins.Count, Thread.CurrentThread.ManagedThreadId);

                // Get a reference to the list.
                library = "SiteAssets";
                List list = e.WebClientContext.Web.GetListByUrl(library);

                if (!e.GetProperty("ScriptFileVersion").Equals("1.0", StringComparison.InvariantCultureIgnoreCase))
                {
                    if (list == null)
                    {
                        // Get a reference to the list.
                        library = "Style%20Library";
                        list = e.WebClientContext.Web.GetListByUrl(library);
                    }

                    if (list != null)
                    {
                        // Upload js file to list.
                        list.RootFolder.UploadFile("sitegovernance.js", "sitegovernance.js", true);

                        e.SetProperty("ScriptFileVersion", "1.0");
                    }
                }

                if (admins.Count < 2)
                {
                    // Show notification message because you need at least two site collection administrators.
                    e.WebClientContext.Site.AddJsLink(SiteGovernanceJobKey, BuildJavaScriptUrl(e.Url, library));
                    Console.WriteLine("Site {0} marked as incompliant!", e.Url);
                    e.SetProperty("SiteCompliant", "false");
                }
                else
                {
                    // Remove the notification message because two administrators are assigned.
                    e.WebClientContext.Site.DeleteJsLink(SiteGovernanceJobKey);
                    Console.WriteLine("Site {0} is compliant", e.Url);
                    e.SetProperty("SiteCompliant", "true");
                }

                e.CurrentRunSuccessful = true;
                e.DeleteProperty("LastError");
            }
            catch(Exception ex)
            {
                Log.Error("SiteGovernanceJob", "Error while processing site {0}. Error = {1}", e.Url, ex.Message);
                e.CurrentRunSuccessful = false;
                e.SetProperty("LastError", ex.Message);
            }
        }
```

## <a name="additional-resources"></a><span data-ttu-id="23cd7-166">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="23cd7-166">Additional resources</span></span>
<span data-ttu-id="23cd7-167"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="23cd7-167"></span></span>

- [<span data-ttu-id="23cd7-168">Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen</span><span class="sxs-lookup"><span data-stu-id="23cd7-168">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
- [<span data-ttu-id="23cd7-169">Leitfaden zur Verwendung von den Timer Job-Framework</span><span class="sxs-lookup"><span data-stu-id="23cd7-169">Guide to using the Timer Job Framework</span></span>](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md)
    
- [<span data-ttu-id="23cd7-170">Timer-Job-framework</span><span class="sxs-lookup"><span data-stu-id="23cd7-170">Timer job framework</span></span>](https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples)
