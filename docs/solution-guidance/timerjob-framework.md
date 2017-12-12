---
title: 'Das Timer Job-Framework #'
ms.date: 11/03/2017
ms.openlocfilehash: caaa5342ac1a680821b8095a247d4fe89bc700e0
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="the-timer-job-framework"></a><span data-ttu-id="bfc54-102">Das Timer Job-Framework</span><span class="sxs-lookup"><span data-stu-id="bfc54-102">The Timer Job Framework</span></span> #

<span data-ttu-id="bfc54-103">Die Plug & Play-Timer Job-Framework ist ein Satz von Klassen entwickelt, um einfache Erstellung Hintergrundprozesse, die Arbeiten mit SharePoint-Websites.</span><span class="sxs-lookup"><span data-stu-id="bfc54-103">The PnP Timer Job Framework is a set of classes designed to ease the creation of background processes that operate against SharePoint sites.</span></span> <span data-ttu-id="bfc54-104">Den Timer Job-Framework ist vergleichbar mit lokalen voll vertrauenswürdiger Code Timer Jobs (`SPJobDefinition`).</span><span class="sxs-lookup"><span data-stu-id="bfc54-104">The Timer Job Framework is similar to on-premises full trust code Timer Jobs (`SPJobDefinition`).</span></span> <span data-ttu-id="bfc54-105">Der Hauptunterschied zwischen den Timer Job-Framework und den Code volle Vertrauenswürdigkeit Zeitgeberauftrag mit ist, den Timer Job-Framework nur Client-seitigen APIs verwendet und daher können (und sollten) außerhalb von SharePoint ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-105">The primary difference with between the Timer Job Framework and the full trust code Timer Job is that the Timer Job Framework only uses client side APIs and therefore can (and should) be run outside of SharePoint.</span></span> <span data-ttu-id="bfc54-106">Den Timer Job-Framework ermöglicht die Zeitgeberaufträge erstellen, die mit SharePoint Online arbeiten.</span><span class="sxs-lookup"><span data-stu-id="bfc54-106">The Timer Job Framework makes it possible to build Timer Jobs that operate against SharePoint Online.</span></span>

<span data-ttu-id="bfc54-107">Sobald ein Zeitgeberauftrag, es erstellt wurden muss geplant und ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-107">Once a Timer Job has been created it needs to be scheduled and executed.</span></span> <span data-ttu-id="bfc54-108">Die beiden am häufigsten verwendeten Optionen sind:</span><span class="sxs-lookup"><span data-stu-id="bfc54-108">The two most common options are:</span></span>

- <span data-ttu-id="bfc54-109">Wenn **Microsoft Azure** die Hostingplattform ist, können Zeitgeberaufträge bereitgestellt und als **Azure WebJobs**ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-109">When **Microsoft Azure** is the hosting platform, Timer Jobs can be deployed and run as **Azure WebJobs**.</span></span>
- <span data-ttu-id="bfc54-110">Wenn **Windows Server** ist kann im **Windows-Taskplaner**die Zeitgeberaufträge für hosting-Plattform (z. B. für lokale SharePoint) bereitgestellt und ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-110">When **Windows Server** is the hosting platform (e.g. for on-premises SharePoint) Timer Jobs can be deployed and run in **Windows scheduler**.</span></span>

<span data-ttu-id="bfc54-111">Video eine Einführung in die Zeitgeberaufträge [in diesem Video Plug & Play-](http://channel9.msdn.com/blogs/OfficeDevPnP/Introduction-to-the-PnP-timer-job-framework) führt den Timer Job-Framework und das Zeitgeberauftrag für die einfachen Beispiel veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="bfc54-111">For a video introduction to Timer Jobs, [this PnP video](http://channel9.msdn.com/blogs/OfficeDevPnP/Introduction-to-the-PnP-timer-job-framework) introduces the Timer Job Framework and demonstrates the Simple Timer Job example.</span></span>

## <a name="simple-timer-job-example"></a><span data-ttu-id="bfc54-112">Einfaches Beispiel für Zeitgeberauftrag</span><span class="sxs-lookup"><span data-stu-id="bfc54-112">Simple Timer Job example</span></span> ##
<span data-ttu-id="bfc54-113">In diesem Kapitel erfahren Sie, wie Sie eine sehr einfache Zeitgeberauftrag zum Erstellen: das Ziel der in diesem Beispiel wird dem Leser einen schnellen Einblick in bereitstellen, später bieten wir eine ausführlichere Erläuterung der den Timer Job-Framework.</span><span class="sxs-lookup"><span data-stu-id="bfc54-113">In this chapter you'll see how to create a very simple Timer Job: the goal of this sample is to provide the reader a quick view, later on we'll provide a more detailed explanation of the Timer Job Framework.</span></span> 

> [!NOTE] 
> <span data-ttu-id="bfc54-114">Eine umfangreichere Plug & Play-Lösung mit zehn einzelne Zeitgeberauftrag-Beispiele von "Hello World" herunter, die tatsächliche Inhaltsablauf Aufträge finden Sie unter https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples</span><span class="sxs-lookup"><span data-stu-id="bfc54-114">For a more extensive PnP solution with ten individual Timer Job examples, from "Hello world" samples to actual content expiration jobs, see https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples</span></span>

<span data-ttu-id="bfc54-115">Die folgenden wird beschrieben, wie eine einfache Zeitgeberauftrag zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="bfc54-115">The following describes how to create a simple Timer Job:</span></span>

### <a name="step-1-create-a-console-project-and-reference-pnp-core"></a><span data-ttu-id="bfc54-116">Schritt 1: Erstellen eines Konsolenprojekts und verweisen auf Plug & Play-Core</span><span class="sxs-lookup"><span data-stu-id="bfc54-116">Step 1: Create a Console project and reference PnP Core</span></span> ###
<span data-ttu-id="bfc54-117">Erstellen Sie in diesem ersten Schritt ein neues Projekt vom Typ "Konsole" und verweisen Sie die Plug & Play-Core-Bibliothek zu, indem Sie einen der folgenden Schritte ausführen:</span><span class="sxs-lookup"><span data-stu-id="bfc54-117">In this first step, create a new project of the type "console" and reference the PnP core library by doing one of the following:</span></span>

- <span data-ttu-id="bfc54-118">Fügen Sie Sie dem Projekt das Office 365 Developer Mustern und Methoden Core Nuget-Paket.</span><span class="sxs-lookup"><span data-stu-id="bfc54-118">Add the Office 365 Developer Patterns and Practices Core Nuget package to your project.</span></span> <span data-ttu-id="bfc54-119">Es wird ein [Nuget-Paket für v15 (lokal) und für v16 (Office 365)](https://www.nuget.org/packages?q=pnp).</span><span class="sxs-lookup"><span data-stu-id="bfc54-119">There's a [nuget package for v15 (on-premises) and for v16 (Office 365)](https://www.nuget.org/packages?q=pnp).</span></span> <span data-ttu-id="bfc54-120">Dies ist die bevorzugte Option.</span><span class="sxs-lookup"><span data-stu-id="bfc54-120">This is the preferred option.</span></span>
- <span data-ttu-id="bfc54-121">Fügen Sie Sie dem Projekt das vorhandene Plug & Play-Kern-Source-Projekt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-121">Add the existing PnP Core source project to your project.</span></span> <span data-ttu-id="bfc54-122">Dadurch können Sie den Plug & Play-Kerncode schrittweise beim Debuggen.</span><span class="sxs-lookup"><span data-stu-id="bfc54-122">This will allow you to step into the PnP core code when debugging.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="bfc54-123">Dafür verantwortlich ist dieser Code aktualisiert mit den neuesten Änderungen Plug & Play-hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-123">You will be responsible for keeping this code updated with the latest changes added to PnP.</span></span>

### <a name="step-2-create-a-timer-job-class-and-add-your-timer-job-logic"></a><span data-ttu-id="bfc54-124">Schritt 2: Erstellen Sie eine Zeitgeberauftrag-Klasse und fügen Ihre Zeitgeberauftrag Logik hinzu</span><span class="sxs-lookup"><span data-stu-id="bfc54-124">Step 2: Create a Timer Job class and add your Timer Job logic</span></span> ###
1. <span data-ttu-id="bfc54-125">Fügen Sie eine Klasse für den Zeitgeberauftrag mit dem Namen `SimpleJob`.</span><span class="sxs-lookup"><span data-stu-id="bfc54-125">Add a class for the Timer Job named `SimpleJob`.</span></span>
2. <span data-ttu-id="bfc54-126">Klasse erben die `TimerJob` abstrakte Basisklasse.</span><span class="sxs-lookup"><span data-stu-id="bfc54-126">Have the class inherit the `TimerJob` abstract base class.</span></span>
3. <span data-ttu-id="bfc54-127">In den Konstruktor benennen Sie den Zeitgeberauftrag (`base("SimpleJob")`) und Verbinden der `TimerJobRun` -Ereignishandler.</span><span class="sxs-lookup"><span data-stu-id="bfc54-127">In the constructor give the Timer Job a name (`base("SimpleJob")`) and connect the `TimerJobRun` event handler.</span></span>
4. <span data-ttu-id="bfc54-128">Die Zeitgeberauftrag für die Logik zum Hinzufügen der `TimerJobRun` -Ereignishandler.</span><span class="sxs-lookup"><span data-stu-id="bfc54-128">Add your Timer Job logic to the `TimerJobRun` event handler.</span></span>

<span data-ttu-id="bfc54-129">Das Ergebnis wird ähnlich der folgenden sein:</span><span class="sxs-lookup"><span data-stu-id="bfc54-129">The result will be similar to the following:</span></span>
```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using OfficeDevPnP.Core.Framework.TimerJobs;

namespace Core.TimerJobs.Samples.SimpleJob
{
    public class SimpleJob: TimerJob
    {
        public SimpleJob() : base("SimpleJob")
        {
            TimerJobRun += SimpleJob_TimerJobRun;
        }

        void SimpleJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
        {
            e.WebClientContext.Load(e.WebClientContext.Web, p => p.Title);
            e.WebClientContext.ExecuteQueryRetry();
            Console.WriteLine("Site {0} has title {1}", e.Url, e.WebClientContext.Web.Title);
        }
    }
}
```

### <a name="step-3-update-programcs-to-use-the-timer-job"></a><span data-ttu-id="bfc54-130">Schritt 3: Update Program.cs, verwenden Sie den Zeitgeberauftrag</span><span class="sxs-lookup"><span data-stu-id="bfc54-130">Step 3: Update Program.cs to use the Timer Job</span></span> ###
<span data-ttu-id="bfc54-131">Der Zeitgeberauftrag mit dem im vorherigen Schritt erstellten weiterhin soll ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-131">The Timer Job created in the previous step still needs to be executed.</span></span> <span data-ttu-id="bfc54-132">Aktualisieren Sie dazu `Program.cs` mithilfe der folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="bfc54-132">To do so, update `Program.cs` by using the following steps:</span></span>

1. <span data-ttu-id="bfc54-133">Die Zeitgeberauftrag für die Klasse zu instanziieren.</span><span class="sxs-lookup"><span data-stu-id="bfc54-133">Instantiate your Timer Job class.</span></span>
2. <span data-ttu-id="bfc54-134">Geben Sie die Authentifizierungsdetails für den Zeitgeberauftrag.</span><span class="sxs-lookup"><span data-stu-id="bfc54-134">Provide the authentication details for the Timer Job.</span></span> <span data-ttu-id="bfc54-135">In diesem Beispiel verwendet den Benutzernamen und das Kennwort, um die Authentifizierung für SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="bfc54-135">This example uses the user name and password to authenticate against SharePoint Online.</span></span>
3. <span data-ttu-id="bfc54-136">Fügen Sie einen oder mehrere Standorte für das Programm Zeitgeberauftrag für den Zugriff auf.</span><span class="sxs-lookup"><span data-stu-id="bfc54-136">Add one or more sites for the Timer Job program to access.</span></span> <span data-ttu-id="bfc54-137">In diesem Beispiel wird ein Platzhalterzeichen in der URL.</span><span class="sxs-lookup"><span data-stu-id="bfc54-137">This example uses a wild card character in the URL.</span></span> <span data-ttu-id="bfc54-138">Der Zeitgeberauftrag wird auf alle Websites ausgeführt, die mit dieser Platzhalter URL übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="bfc54-138">The Timer Job will run on all sites that match this wild card URL.</span></span>
4. <span data-ttu-id="bfc54-139">Starten Sie den Zeitgeberauftrag durch Aufrufen der `Run` Methode.</span><span class="sxs-lookup"><span data-stu-id="bfc54-139">Start the Timer Job by calling the `Run` method.</span></span>

```C#
static void Main(string[] args)
{
    // Instantiate the Timer Job class
    SimpleJob simpleJob = new SimpleJob();
    
    // The provided credentials need access to the site collections you want to use
    simpleJob.UseOffice365Authentication("user@tenant.onmicrosoft.com", "pwd");

    // Add one or more sites to operate on
    simpleJob.AddSite("https://<tenant>.sharepoint.com/sites/d*");
    
    // Run the job
    simpleJob.Run();
}
```

## <a name="timer-job-deployment-options"></a><span data-ttu-id="bfc54-140">Timer-Job-Bereitstellungsoptionen</span><span class="sxs-lookup"><span data-stu-id="bfc54-140">Timer Job deployment options</span></span> ##
<span data-ttu-id="bfc54-141">Im vorherige Schritt veranschaulicht eine einfache Zeitgeberauftrag.</span><span class="sxs-lookup"><span data-stu-id="bfc54-141">The previous step demonstrates a simple Timer Job.</span></span> <span data-ttu-id="bfc54-142">Der nächste Schritt besteht darin, den Zeitgeberauftrag bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="bfc54-142">The next step is to deploy the Timer Job.</span></span>

<span data-ttu-id="bfc54-143">Ein Zeitgeberauftrag ist eine .exe-Datei, die auf einer Hostingplattform eingeplant werden muss.</span><span class="sxs-lookup"><span data-stu-id="bfc54-143">A Timer Job is an .exe file that must be scheduled on a hosting platform.</span></span> <span data-ttu-id="bfc54-144">Abhängig von der gewählten Hostingplattform unterscheidet sich in die Bereitstellung.</span><span class="sxs-lookup"><span data-stu-id="bfc54-144">Depending on the chosen hosting platform the deployment differs.</span></span> <span data-ttu-id="bfc54-145">In den folgenden Abschnitten werden die beiden am häufigsten verwendeten Plattform Hostingoptionen beschrieben:</span><span class="sxs-lookup"><span data-stu-id="bfc54-145">The following sections describe the two most common hosting platform options:</span></span>
- <span data-ttu-id="bfc54-146">Verwenden von Microsoft Azure als die hosting-Plattform</span><span class="sxs-lookup"><span data-stu-id="bfc54-146">Using Microsoft Azure as the hosting platform</span></span>
- <span data-ttu-id="bfc54-147">Mithilfe von Windows Server als hosting-Plattform</span><span class="sxs-lookup"><span data-stu-id="bfc54-147">Using Windows Server as the hosting platform</span></span>

### <a name="deploying-timer-jobs-to-microsoft-azure-using-azure-webjobs"></a><span data-ttu-id="bfc54-148">Bereitstellen von Zeitgeberaufträgen in Microsoft Azure mithilfe von Azure WebJobs</span><span class="sxs-lookup"><span data-stu-id="bfc54-148">Deploying Timer Jobs to Microsoft Azure using Azure WebJobs</span></span> ###
<span data-ttu-id="bfc54-149">Bevor Sie einen Zeitgeberauftrag bereitstellen, stellen Sie sicher, dass der Auftrag ohne Benutzereingriff ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="bfc54-149">Before deploying a Timer Job, ensure that the job can run without user interaction.</span></span> <span data-ttu-id="bfc54-150">Im Beispiel in diesem Artikel der Benutzer aufgefordert, ein Kennwort oder den Clientsecret angeben (Siehe auch bei der **Authentifizierung**) welche funktioniert while testen, aber die funktionieren nicht, wenn bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-150">The sample in this article prompts the user to provide a password or clientsecret (see more in **Authentication**) which works while testing but will not work when deployed.</span></span> <span data-ttu-id="bfc54-151">Die alle vorhandenen Beispielen ermöglichen Benutzern das Geben Sie ein Kennwort oder Clientsecret mithilfe der `app.config` Datei:</span><span class="sxs-lookup"><span data-stu-id="bfc54-151">The existing samples all allow the user to provide a password or clientsecret by using the `app.config` file:</span></span>

```XML
  <appSettings>
    <add key="user" value="user@tenant.onmicrosoft.com"/>
    <add key="password" value="your password goes here!"/>
    <add key="domain" value="Contoso"/>
    <add key="clientid" value="a4cdf20c-3385-4664-8302-5eab57ee6f14"/>
    <add key="clientsecret" value="your clientsecret goes here!"/>
  </appSettings>
```

<span data-ttu-id="bfc54-152">Nachdem diese Änderungen hinzugefügt werden die `app.config` Datei, und führen Sie den Zeitgeberauftrag von Visual Studio zu bestätigen, dass sie ohne Benutzereingriff ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="bfc54-152">After these changes are added to the `app.config` file, run the Timer Job from Visual Studio to confirm that it runs without user interaction.</span></span> 

<span data-ttu-id="bfc54-153">Die tatsächliche Bereitstellung in Azure basiert auf Azure Webaufträge.</span><span class="sxs-lookup"><span data-stu-id="bfc54-153">The actual deployment to Azure is based on Azure Web Jobs.</span></span> <span data-ttu-id="bfc54-154">In diesem Beispiel der Zeitgeberauftrag für die Bereitstellung die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="bfc54-154">To deploy this Timer Job example, follow these steps:</span></span>

1. <span data-ttu-id="bfc54-155">Klicken Sie mit der rechten Maustaste auf das Projekt in Visual Studio, und wählen Sie **Veröffentlichen als Azure WebJob...**</span><span class="sxs-lookup"><span data-stu-id="bfc54-155">Right click the project in Visual Studio and choose **Publish as Azure WebJob...**</span></span>
2. <span data-ttu-id="bfc54-156">Geben Sie einen Zeitplan für den Zeitgeberauftrag, und klicken Sie auf **OK**</span><span class="sxs-lookup"><span data-stu-id="bfc54-156">Provide a schedule for the Timer Job and click **OK**</span></span>
3. <span data-ttu-id="bfc54-157">Wählen Sie **Microsoft Azure-Websites** als Veröffentlichungsziel.</span><span class="sxs-lookup"><span data-stu-id="bfc54-157">Select **Microsoft Azure Websites** as a publish target.</span></span> <span data-ttu-id="bfc54-158">Sie werden aufgefordert, in Azure anmelden, und wählen Sie die Azure-Website, die den Zeitgeberauftrag hostet (Sie können auch einen neuen Anwendungspool erstellen, die benötigt werden)</span><span class="sxs-lookup"><span data-stu-id="bfc54-158">You'll be asked to login to Azure and select the Azure Web Site that will host the Timer Job (you can also create a new one if that would be needed)</span></span>
4. <span data-ttu-id="bfc54-159">Drücken Sie **Veröffentlichen** , drücken Sie die WebJob in Azure</span><span class="sxs-lookup"><span data-stu-id="bfc54-159">Press **Publish** to push the WebJob to Azure</span></span>
5. <span data-ttu-id="bfc54-160">Nachdem der Zeitgeberauftrag veröffentlicht wurde können Sie den Auftrag auslösen und überprüfen Sie die Ausführung des Auftrags aus Visual Studio oder dem [Azure-Verwaltungsportal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="bfc54-160">Once the Timer Job has been published you can trigger the job and check the job execution from Visual Studio or the [Azure management portal](https://manage.windowsazure.com).</span></span>

![Azure-Verwaltungsportal](media/timerjob-framework/4xDUvXv.png)

<span data-ttu-id="bfc54-162">Darüber hinaus kann der Zeitgeberauftrag, indem Markieren des Auftrags und **Führen Sie**über das neue [Portal Azure](https://portal.azure.com) ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-162">Also, the timer job can be run from the new [Azure portal](https://portal.azure.com) by selecting the job and choosing **Run**.</span></span> <span data-ttu-id="bfc54-163">Weitere Informationen zum Arbeiten mit WebJobs über das neue Portal finden Sie im Artikel [Hintergrund ausführen von Aufgaben mit WebJobs](https://azure.microsoft.com/en-us/documentation/articles/web-sites-create-web-jobs/).</span><span class="sxs-lookup"><span data-stu-id="bfc54-163">More details about how to work with WebJobs from the new portal can be found in the article, [Run Background tasks with WebJobs](https://azure.microsoft.com/en-us/documentation/articles/web-sites-create-web-jobs/).</span></span>

![Azure-portal](media/timerjob-framework/n4wGS5x.png)

> [!NOTE] 
> <span data-ttu-id="bfc54-165">Ausführliche Anleitungen ein Azure WebJob bereitstellen finden Sie unter [Erste Schritte mit Azure WebJobs ("Zeitgeberaufträge") für Ihre Office 365-Websites](https://github.com/SharePoint/PnP-Guidance/blob/master/articles/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites.md).</span><span class="sxs-lookup"><span data-stu-id="bfc54-165">For in-depth guidance on deploying an Azure WebJob, see [Getting Started with azure WebJobs ("Timer Jobs") for your Office 365 Sites](https://github.com/SharePoint/PnP-Guidance/blob/master/articles/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites.md).</span></span> 

### <a name="deploying-timer-jobs-to-windows-server-using-the-windows-scheduler"></a><span data-ttu-id="bfc54-166">Bereitstellen von Zeitgeberaufträgen in Windows Server mithilfe der Windows-Taskplaner</span><span class="sxs-lookup"><span data-stu-id="bfc54-166">Deploying Timer Jobs to Windows Server using the Windows Scheduler</span></span> ###
<span data-ttu-id="bfc54-167">Wenn in Windows Server bereitgestellt wird, müssen den Zeitgeberauftrag ohne Benutzereingriff ausführen.</span><span class="sxs-lookup"><span data-stu-id="bfc54-167">When deployed to Windows Server, the Timer Job must run without user interaction.</span></span> <span data-ttu-id="bfc54-168">Ändern der `app.config` speichern unter **Bereitstellen von Zeitgeberaufträgen für Microsoft Azure mithilfe von Azure WebJobs**beschrieben.</span><span class="sxs-lookup"><span data-stu-id="bfc54-168">Modify the `app.config` file as described in **Deploying Timer Jobs to Microsoft Azure using Azure WebJobs**.</span></span> 

<span data-ttu-id="bfc54-169">Kopieren Sie die endgültige Produktversion von Ihre Arbeit an den Server, auf ausführen soll.</span><span class="sxs-lookup"><span data-stu-id="bfc54-169">Copy the release version of your job to the server you want it to run on.</span></span> <span data-ttu-id="bfc54-170">**Wichtig:** Kopieren Sie alle relevanten Assemblys, die .exe-Datei und die .config-Datei, um sicherzustellen, dass der Auftrag auf dem Server ausführen kann, ohne zusätzliche Dateien oder Programme auf dem Server installieren.</span><span class="sxs-lookup"><span data-stu-id="bfc54-170">**Important:** Copy all the relevant assemblies, the .exe file and the .config file to ensure the job can run on the server without installing any additional files or programs on the server.</span></span> 

<span data-ttu-id="bfc54-171">Planen Sie die Ausführung des Zeitgeberauftrags.</span><span class="sxs-lookup"><span data-stu-id="bfc54-171">Schedule the execution of the Timer Job.</span></span> <span data-ttu-id="bfc54-172">Es wird empfohlen, die integrierte [Windows-Taskplaner](https://technet.microsoft.com/en-us/library/cc721871.aspx)verwendet.</span><span class="sxs-lookup"><span data-stu-id="bfc54-172">It is recommended to use the built in [Windows Task Scheduler](https://technet.microsoft.com/en-us/library/cc721871.aspx).</span></span> <span data-ttu-id="bfc54-173">Um die Windows-Taskplaner verwenden zu können, müssen Sie die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="bfc54-173">To use the Windows Task Scheduler, take the following steps:</span></span>

1. <span data-ttu-id="bfc54-174">Öffnen Sie den Taskplaner (Control Panel-Taskplaner >).</span><span class="sxs-lookup"><span data-stu-id="bfc54-174">Open the task scheduler (Control Panel -> Task Scheduler).</span></span>
2. <span data-ttu-id="bfc54-175">Klicken Sie auf **Aufgabe erstellen** , und geben Sie einen Namen und ein Konto, das die Aufgabe ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="bfc54-175">Click on **Create Task** and specify a name and an account that will execute the task.</span></span>
3. <span data-ttu-id="bfc54-176">Klicken Sie auf **Trigger** , und fügen Sie einen neuen Trigger hinzu.</span><span class="sxs-lookup"><span data-stu-id="bfc54-176">Click on **Triggers** and add a new trigger.</span></span> <span data-ttu-id="bfc54-177">Geben Sie den Zeitplan für den Zeitgeberauftrag gewünschten.</span><span class="sxs-lookup"><span data-stu-id="bfc54-177">Specify the schedule you want for the Timer Job.</span></span>
4. <span data-ttu-id="bfc54-178">Klicken Sie auf **Aktionen** und wählen Sie die Aktion "Einen Programm starten", wählen Sie die Zeitgeberauftrag .exe-Datei ein, und legen Sie den Start im Ordner.</span><span class="sxs-lookup"><span data-stu-id="bfc54-178">Click on **Actions** and choose action "Start a program", select the Timer Job .exe file and set the start in folder.</span></span>
5. <span data-ttu-id="bfc54-179">Klicken Sie auf **OK** , um den Vorgang zu speichern.</span><span class="sxs-lookup"><span data-stu-id="bfc54-179">Click on **OK** to save the task.</span></span>

![Die Windows-Taskplaner](media/timerjob-framework/hkRc0Bo.png)

## <a name="timer-job-framework-in-depth"></a><span data-ttu-id="bfc54-181">Timer-Job-Framework fundierte</span><span class="sxs-lookup"><span data-stu-id="bfc54-181">Timer Job Framework in-depth</span></span> ##
<span data-ttu-id="bfc54-182">In diesem Abschnitt Details wie den Timer Job Framework-Features und deren Funktionsweise.</span><span class="sxs-lookup"><span data-stu-id="bfc54-182">This section details how the Timer Job Framework features and how it works.</span></span>

### <a name="structure"></a><span data-ttu-id="bfc54-183">Struktur</span><span class="sxs-lookup"><span data-stu-id="bfc54-183">Structure</span></span> ###
<span data-ttu-id="bfc54-184">Die `TimerJob` Klasse ist eine abstrakte Basisklasse, die die folgenden öffentlichen Eigenschaften, Methoden und Ereignisse enthält:</span><span class="sxs-lookup"><span data-stu-id="bfc54-184">The `TimerJob` class is an abstract base class which contains the following public properties, methods and events:</span></span>

![Die Struktur einer allgemeinen](media/timerjob-framework/4XsZ1pN.png)

<span data-ttu-id="bfc54-186">Die meisten Eigenschaften und Methoden werden in den folgenden Abschnitten ausführlich erläutert.</span><span class="sxs-lookup"><span data-stu-id="bfc54-186">Most properties and methods will be explained in more detail in the coming sections.</span></span> <span data-ttu-id="bfc54-187">Hier werden die restlichen Eigenschaften und Methoden beschrieben:</span><span class="sxs-lookup"><span data-stu-id="bfc54-187">The rest of the properties and methods are described here:</span></span>

- <span data-ttu-id="bfc54-188">**IsRunning** -Eigenschaft: Ruft einen Wert zurück, der angibt, ob der Zeitgeberauftrag ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="bfc54-188">**IsRunning** property: Gets a value indicating whether the Timer Job is executing.</span></span> <span data-ttu-id="bfc54-189">Der Wert **true,** Wenn ausgeführt; **false,** wenn er nicht ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-189">Value of **true** if executing; **false** if not executing.</span></span>
- <span data-ttu-id="bfc54-190">**Name** -Eigenschaft: Ruft den Namen des Zeitgeberauftrags ab.</span><span class="sxs-lookup"><span data-stu-id="bfc54-190">**Name** property: Gets the name of the Timer Job.</span></span> <span data-ttu-id="bfc54-191">Der Name wird in den Zeitgeberauftrag Konstruktor ursprünglich festgelegt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-191">The name is initially set in the Timer Job constructor.</span></span>
- <span data-ttu-id="bfc54-192">**SharePointVersion** -Eigenschaft: Dient zum Abrufen oder festlegen die SharePoint-Version.</span><span class="sxs-lookup"><span data-stu-id="bfc54-192">**SharePointVersion** property: Gets or sets the SharePoint version.</span></span> <span data-ttu-id="bfc54-193">Diese Eigenschaft wird automatisch festgelegt, basierend auf der Version von der geladenen Microsoft.SharePoint.Client.dll und im Allgemeinen sollten nicht ändern.</span><span class="sxs-lookup"><span data-stu-id="bfc54-193">this property is automatically set based on the version of the loaded Microsoft.SharePoint.Client.dll and in general should not change.</span></span> <span data-ttu-id="bfc54-194">Sie können diese Eigenschaft jedoch ändern, falls Sie beispielsweise die v16 CSOM Bibliotheken in einem v15 verwenden möchten (lokal)-Bereitstellung.</span><span class="sxs-lookup"><span data-stu-id="bfc54-194">You can, however, change this property in case you for example want to use the v16 CSOM libraries in a v15 (on-premises) deployment.</span></span>
- <span data-ttu-id="bfc54-195">**Version** -Eigenschaft: Ruft die Version des diesen Zeitgeberauftrag.</span><span class="sxs-lookup"><span data-stu-id="bfc54-195">**Version** property: Gets the version of this Timer Job.</span></span> <span data-ttu-id="bfc54-196">Die Version im Konstruktor Zeitgeberauftrag ursprünglich festgelegt ist oder in der Standardeinstellung werden 1.0, wenn nicht über den Konstruktor festgelegt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-196">The version is initially set in the Timer Job constructor or defaults to 1.0 when not set via the constructor.</span></span>

<span data-ttu-id="bfc54-197">Vorbereiten für einen Zeitgeberauftrag führen Sie erste **Konfigurieren** müssen sie:</span><span class="sxs-lookup"><span data-stu-id="bfc54-197">To prepare for a Timer Job run you must first **configure** it:</span></span>

1. <span data-ttu-id="bfc54-198">Geben Sie **Authentifizierungseinstellungen** .</span><span class="sxs-lookup"><span data-stu-id="bfc54-198">Provide **authentication** settings.</span></span>
2. <span data-ttu-id="bfc54-199">Geben Sie einen **Bereich**, der eine Liste der Websites ist.</span><span class="sxs-lookup"><span data-stu-id="bfc54-199">Provide a **scope**, which is a list of sites.</span></span>
3. <span data-ttu-id="bfc54-200">Festlegen Sie **Zeitgeberauftrag für die Eigenschaften**optional.</span><span class="sxs-lookup"><span data-stu-id="bfc54-200">Optionally set **Timer Job properties**.</span></span>

<span data-ttu-id="bfc54-201">Aus der Sicht Ausführung werden die folgenden allgemeinen Schritte übernommen, wenn eine Ausführung des Zeitgeberauftrags gestartet wurde:</span><span class="sxs-lookup"><span data-stu-id="bfc54-201">From an execution perspective the following overall steps are taken when a Timer Job run is started:</span></span>

1. <span data-ttu-id="bfc54-202">**Beheben von Websites**: Platzhalter Website-Urls (beispielsweise https://tenant.sharepoint.com/sites/d *) in eine aktuelle Liste der vorhandenen Websites aufgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-202">**Resolve sites**: Wild card site urls (for example, https://tenant.sharepoint.com/sites/d*) are resolved into an actual list of existing sites.</span></span> <span data-ttu-id="bfc54-203">Wenn Sub Website erweitern angefordert wurde, wird die Websiteliste aufgelöst mit allen Unterwebsites erweitert.</span><span class="sxs-lookup"><span data-stu-id="bfc54-203">If sub site expanding was requested then the resolved sites list is expanded with all sub sites.</span></span>
2. <span data-ttu-id="bfc54-204">**Erstellen der Arbeit Batches** basierend auf der aktuellen Einstellungen treading sowie einen Thread pro Batch.</span><span class="sxs-lookup"><span data-stu-id="bfc54-204">**Create batches of work** based on the current treading settings and create one thread per batch.</span></span>
3. <span data-ttu-id="bfc54-205">Das **Threads Arbeit Batches ausführen** , und rufen die `TimerJobRun` -Ereignis für jeden Standort in der Liste.</span><span class="sxs-lookup"><span data-stu-id="bfc54-205">The **threads execute work batches** and call the `TimerJobRun` event for each site in the list.</span></span>

<span data-ttu-id="bfc54-206">Weitere Informationen zu den einzelnen Schritten finden Sie unter.</span><span class="sxs-lookup"><span data-stu-id="bfc54-206">Further details on each step can be found below.</span></span>

### <a name="authentication"></a><span data-ttu-id="bfc54-207">Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="bfc54-207">Authentication</span></span> ###
<span data-ttu-id="bfc54-208">Bevor ein Zeitgeberauftrag verwendet werden können muss den Zeitgeberauftrag wissen, wie Sie SharePoint authentifiziert.</span><span class="sxs-lookup"><span data-stu-id="bfc54-208">Before a Timer Job can be used the Timer Job needs to know how to authenticate back to SharePoint.</span></span> <span data-ttu-id="bfc54-209">Das Framework unterstützt derzeit die Ansätze im **AuthenticationType** -Enumeration. **Office365**, **Netzwerk-Anmeldeinformationen weisen** und **AppOnly**.</span><span class="sxs-lookup"><span data-stu-id="bfc54-209">The framework currently supports the approaches in the **AuthenticationType** enum; **Office365**, **NetworkCredentials** and **AppOnly**.</span></span> <span data-ttu-id="bfc54-210">Mit den Methoden die **AuthenticationType** -Eigenschaft auf den entsprechenden Wert von **Office365**, **Netzwerk-Anmeldeinformationen weisen** und **AppOnly**, folgenden auch automatisch dargestellt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-210">Using the methods illustrated below also automatically sets the **AuthenticationType** property to the appropriate value of **Office365**, **NetworkCredentials** and **AppOnly**.</span></span> <span data-ttu-id="bfc54-211">Im folgenden Flussdiagramm zeigt die Schritte.</span><span class="sxs-lookup"><span data-stu-id="bfc54-211">The flowchart below shows the steps to take.</span></span> <span data-ttu-id="bfc54-212">Ausführliche Erklärungen auf jeder Ansatz finden Sie unter.</span><span class="sxs-lookup"><span data-stu-id="bfc54-212">Detailed explanations on each approach are found below.</span></span>

![Flussdiagramm für die Authentifizierung Schritte](media/timerjob-framework/rt4dZa3.png)

#### <a name="user-credentials"></a><span data-ttu-id="bfc54-214">Anmeldeinformationen des Benutzers</span><span class="sxs-lookup"><span data-stu-id="bfc54-214">User credentials</span></span> ####
<span data-ttu-id="bfc54-215">Zum Angeben der Anmeldeinformationen des Benutzers zum Ausführen für **Office 365** können Sie diese 2 Methoden verwenden:</span><span class="sxs-lookup"><span data-stu-id="bfc54-215">To specify user credentials for running against **Office 365** you can use these 2 methods:</span></span>
```C#
public void UseOffice365Authentication(string userUPN, string password)
public void UseOffice365Authentication(string credentialName)
```

<span data-ttu-id="bfc54-216">Die erste Methode akzeptiert einfach einen Benutzernamen und ein Kennwort ein.</span><span class="sxs-lookup"><span data-stu-id="bfc54-216">The first method simply accepts a user name and password.</span></span> <span data-ttu-id="bfc54-217">Im zweiten Beispiel können Sie eine generische Anmeldeinformationen gespeichert im Windows-Anmeldeinformations-Manager angeben.</span><span class="sxs-lookup"><span data-stu-id="bfc54-217">The second one allows you to specify a generic credential stored in the Windows Credential Manager.</span></span> <span data-ttu-id="bfc54-218">Der Screenshot zeigt die `bertonline` generische Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="bfc54-218">The screen shot below shows the `bertonline` generic credential.</span></span> <span data-ttu-id="bfc54-219">Um, die zum Authentifizieren der Zeitgeberauftrag verwenden, geben Sie "Bertonline" als Parameter für die zweite Methode.</span><span class="sxs-lookup"><span data-stu-id="bfc54-219">To use that to authenticate the Timer Job, provide "bertonline" as the parameter of the second method.</span></span>

![Der Anmeldeinformations-Manager für Windows](media/timerjob-framework/HdqvsHy.png)

<span data-ttu-id="bfc54-221">Es gibt ähnliche Methoden, um für **SharePoint lokal**auszuführen:</span><span class="sxs-lookup"><span data-stu-id="bfc54-221">There are similar methods for running against **SharePoint on-premises**:</span></span>
```C#
public void UseNetworkCredentialsAuthentication(string samAccountName, string password, string domain)
public void UseNetworkCredentialsAuthentication(string credentialName)
```

#### <a name="app-only"></a><span data-ttu-id="bfc54-222">Nur-App</span><span class="sxs-lookup"><span data-stu-id="bfc54-222">App Only</span></span> ####
<span data-ttu-id="bfc54-223">App ist nur die **bevorzugte Methode** , wie Sie Mandanten bezogenen Berechtigungen gewähren können.</span><span class="sxs-lookup"><span data-stu-id="bfc54-223">App only is the **preferred method** as you can grant tenant scoped permissions.</span></span> <span data-ttu-id="bfc54-224">Für Benutzeranmeldeinformationen muss das Benutzerkonto die erforderlichen Berechtigungen verfügen.</span><span class="sxs-lookup"><span data-stu-id="bfc54-224">For user credentials the user account must have the needed permissions.</span></span> 

> [!NOTE] 
> <span data-ttu-id="bfc54-225">Bestimmte Website lösen mit nur-App-Authentifizierung Logik funktionieren nicht.</span><span class="sxs-lookup"><span data-stu-id="bfc54-225">Certain site resolving logic wont work with App-only authentication.</span></span> <span data-ttu-id="bfc54-226">Ausführliche Informationen finden Sie im nächsten Abschnitt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-226">Details can be found in the next section.</span></span> 

<span data-ttu-id="bfc54-227">Um den Auftrag für nur-app-Authentifizierung zu konfigurieren, verwenden Sie eine der folgenden Methoden:</span><span class="sxs-lookup"><span data-stu-id="bfc54-227">To configure the job for app-only authentication, use one of the following methods:</span></span>
```C#
public void UseAppOnlyAuthentication(string clientId, string clientSecret)
public void UseAzureADAppOnlyAuthentication(string clientId, string clientSecret)
```

<span data-ttu-id="bfc54-228">Die gleiche-Methode kann für Office 365 oder SharePoint lokal Zeitgeberaufträge mithilfe der nur-app-Authentifizierung auf einfache Weise zwischen Umgebungen Portable wodurch verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-228">The same method can be used for either Office 365 or SharePoint on-premises which makes Timer Jobs using app-only authentication easily transportable between environments.</span></span>

> [!NOTE] 
> <span data-ttu-id="bfc54-229">Bei Verwendung der nur-app-wird die Logik Zeitgeberauftrag misslingen, wenn APIs verwendet werden, die mit **AuthenticationType.AppOnly**nicht funktionsfähig.</span><span class="sxs-lookup"><span data-stu-id="bfc54-229">When you use app-only your Timer Job logic will fail when APIs are used that do not work with **AuthenticationType.AppOnly**.</span></span> <span data-ttu-id="bfc54-230">Standardsamples sind die Such-API, an den Taxonomie-Store schreiben und das Benutzerprofil API verwenden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-230">Typical samples are the Search API, writing to the taxonomy store, and using the user profile API.</span></span>

### <a name="sites-to-operate-on"></a><span data-ttu-id="bfc54-231">Websites für den Betrieb</span><span class="sxs-lookup"><span data-stu-id="bfc54-231">Sites to operate on</span></span> ###
<span data-ttu-id="bfc54-232">Der Ausführung eines Zeitgeberauftrags benötigt es einen oder mehrere Standorte für ausführen.</span><span class="sxs-lookup"><span data-stu-id="bfc54-232">When a Timer Job runs it needs one or more sites to run against.</span></span> <span data-ttu-id="bfc54-233">Um einen Zeitgeberauftrag Websites hinzuzufügen, verwenden Sie die unten Satz von Methoden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-233">To add sites to a Timer Job, use the below set of methods.</span></span>

```C#
public void AddSite(string site)
public void ClearAddedSites()
```

<span data-ttu-id="bfc54-234">Geben Sie zum Hinzufügen einer Website eine vollqualifizierte URL (beispielsweise https://tenant.sharepoint.com/sites/dev) oder eine Platzhalter-URL ein.</span><span class="sxs-lookup"><span data-stu-id="bfc54-234">To add a site, specify either a fully qualified URL (for example, https://tenant.sharepoint.com/sites/dev) or a wild card URL.</span></span> <span data-ttu-id="bfc54-235">Ein Platzhalter-URL ist eine URL mit der Endung ein * (nur eine einzige * ist zulässig, und es muss das letzte Zeichen der Url).</span><span class="sxs-lookup"><span data-stu-id="bfc54-235">A wild card URL is a URL that ends with a * (only one single * is allowed and it must be the last character of the url).</span></span> <span data-ttu-id="bfc54-236">Ein Beispiel Platzhalter-URL ist https://tenant.sharepoint.com/sites/ *, durch den **Alle** Websitesammlungen unterhalb der verwaltete Pfad dieser Website zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="bfc54-236">A sample wild card URL is https://tenant.sharepoint.com/sites/* which will return **all** the site collections underneath the managed path of that site.</span></span> <span data-ttu-id="bfc54-237">Ein weiteres Beispiel gibt https://tenant.sharepoint.com/sites/dev * alle Websitesammlungen zurück, bei denen die URL "Developer" enthält.</span><span class="sxs-lookup"><span data-stu-id="bfc54-237">For another example, https://tenant.sharepoint.com/sites/dev* will return all site collections where the URL contains "dev".</span></span>

<span data-ttu-id="bfc54-238">In der Regel werden die Websites von der Anwendung hinzugefügt, die das Objekt Zeitgeberauftrag, außer wenn instanziiert der Zeitgeberauftrag zum Steuern der übergebenen Liste der Websites ergreifen können, benötigt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-238">Typically the sites are added by the program that instantiates the Timer Job object, but if needed the Timer Job can take control over the passed list of sites.</span></span> <span data-ttu-id="bfc54-239">Fügen Sie eine Methode zum Überschreiben für die `UpdateAddedSites`virtuelle-Methode, wie im folgenden Beispiel:</span><span class="sxs-lookup"><span data-stu-id="bfc54-239">Do this by adding a method override for the `UpdateAddedSites`virtual method as shown in sample below:</span></span>

```C#
public override List<string> UpdateAddedSites(List<string> addedSites)
{
    // Let's assume we're not happy with the provided list of sites, so first clear it
    addedSites.Clear();

    // Manually adding a new wildcard Url, without an added URL the Timer Job will do...nothing
    addedSites.Add("https://bertonline.sharepoint.com/sites/d*");

    // Return the updated list of sites
    return addedSites;
}
```

<span data-ttu-id="bfc54-240">Geben Sie nach dem hinzufügen einen Platzhalter-URL und die Einstellung Authentifizierung nur-app, die Enumeration Anmeldeinformationen ein.</span><span class="sxs-lookup"><span data-stu-id="bfc54-240">After adding a wild card URL and setting authentication to app-only, specify the enumeration credentials.</span></span> <span data-ttu-id="bfc54-241">Enumeration Anmeldeinformationen werden verwendet, um eine Liste der Websitesammlungen abgerufen, die in der entsprechenden Website-Algorithmus verwendet werden, um eine echte Liste der Websites zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="bfc54-241">Enumeration credentials are used to fetch a list of site collections which are used in the site matching algorithm to return a real list of sites.</span></span> <span data-ttu-id="bfc54-242">Um eine Liste der Websitesammlungen erhalten das Timer-Framework unterschiedlich zwischen Office 365 (v16) und lokale (v15) verhält sich:</span><span class="sxs-lookup"><span data-stu-id="bfc54-242">To acquire a list of site collections the timer framework will behave differently between Office 365 (v16) and on-premises (v15):</span></span>
- <span data-ttu-id="bfc54-243">Office 365: Die `Tenant.GetSiteProperties` Methode dient dazu, lesen Sie die "normaler" Websitesammlungen, die Such-API wird verwendet, um die OneDrive for Business-Websitesammlungen zu lesen.</span><span class="sxs-lookup"><span data-stu-id="bfc54-243">Office 365: The `Tenant.GetSiteProperties` method is used to read the 'regular' site collections, the search API is used to read the OneDrive for Business site collections.</span></span>
- <span data-ttu-id="bfc54-244">Lokal: Such-API wird verwendet, um alle Websitesammlungen zu lesen.</span><span class="sxs-lookup"><span data-stu-id="bfc54-244">On-Premises: The search API is used to read all site collections.</span></span>

<span data-ttu-id="bfc54-245">Wenn die API für die Suche nicht mit einem Benutzerkontext funktioniert, greift den Zeitgeberauftrag auf der angegebenen Enumeration Anmeldeinformationen zurück.</span><span class="sxs-lookup"><span data-stu-id="bfc54-245">Given that the search API doesn't work with a user context, the Timer Job falls back to the specified enumeration credentials.</span></span> 

<span data-ttu-id="bfc54-246">Zum Angeben der Anmeldeinformationen des Benutzers zum Ausführen für **Office 365** können Sie diese 2 Methoden verwenden:</span><span class="sxs-lookup"><span data-stu-id="bfc54-246">To specify user credentials for running against **Office 365** you can use these 2 methods:</span></span>
```C#
public void SetEnumerationCredentials(string userUPN, string password)
public void SetEnumerationCredentials(string credentialName)
```

<span data-ttu-id="bfc54-247">Es gibt ähnliche Methoden, um für **SharePoint lokal**auszuführen:</span><span class="sxs-lookup"><span data-stu-id="bfc54-247">There are similar methods for running against **SharePoint on-premises**:</span></span>
```C#
public void SetEnumerationCredentials(string samAccountName, string password, string domain)
public void SetEnumerationCredentials(string credentialName)
```

<span data-ttu-id="bfc54-248">Die erste Methode akzeptiert einfach ein Benutzername, Kennwort und optional Domäne (in der lokalen).</span><span class="sxs-lookup"><span data-stu-id="bfc54-248">The first method simply accepts a user name, password and optionally domain (when in on-premises).</span></span> <span data-ttu-id="bfc54-249">Die zweite gibt die generische Anmeldeinformationen, die in der Windows-Anmeldeinformationsverwaltung gespeichert.</span><span class="sxs-lookup"><span data-stu-id="bfc54-249">The second specifies a generic credential stored in the Windows Credential Manager.</span></span> <span data-ttu-id="bfc54-250">Finden Sie das **Authentifizierung** Kapitel erhalten Sie weitere Informationen zum Anmeldeinformations-Manager.</span><span class="sxs-lookup"><span data-stu-id="bfc54-250">See the **Authentication** chapter to learn more about the Credential Manager.</span></span>

#### <a name="sub-site-expanding"></a><span data-ttu-id="bfc54-251">Sub-Website erweitern</span><span class="sxs-lookup"><span data-stu-id="bfc54-251">Sub site expanding</span></span> ####
<span data-ttu-id="bfc54-252">Häufig soll der Zeitgeberauftrag für Code, der Stammwebsite der Websitesammlung und mit den alle Unterwebsites dieser Websitesammlung ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="bfc54-252">Often you want the Timer Job code to be executed against the root site of the site collection and against all the sub sites of that site collection.</span></span> <span data-ttu-id="bfc54-253">Zu diesem Zweck müssen Sie die **ExpandSubSites** -Eigenschaft auf **true**festgelegt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-253">To do this, set the **ExpandSubSites** property to **true**.</span></span> <span data-ttu-id="bfc54-254">Dadurch wird der Zeitgeberauftrag für die Sub-Websites als Teil der Website Auflösen von Schritt zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="bfc54-254">This will cause the Timer Job to expand the sub sites as part of the site resolving step.</span></span>

#### <a name="override-resolved-andor-expanded-sites"></a><span data-ttu-id="bfc54-255">Außer Kraft setzen Sie aufgelöst und/oder erweiterte Websites</span><span class="sxs-lookup"><span data-stu-id="bfc54-255">Override resolved and/or expanded sites</span></span> ####
<span data-ttu-id="bfc54-256">Sobald das Timer-Framework die Platzhalter-Websites löst und optional die Sub-Websites erweitert, besteht der nächste Schritt die Liste der Websites zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="bfc54-256">Once the timer framework resolves the wild card sites, and optionally expands the sub sites, the next step is to process the list of sites.</span></span> <span data-ttu-id="bfc54-257">Vor der Verarbeitung der Liste der Websites, empfiehlt es sich um die Liste der Websites zu ändern.</span><span class="sxs-lookup"><span data-stu-id="bfc54-257">Prior to processing the list of sites, you might want to modify the list of sites.</span></span> <span data-ttu-id="bfc54-258">Angenommen, möchten Sie der Liste weitere Websites hinzufügen oder Entfernen von bestimmten Websites.</span><span class="sxs-lookup"><span data-stu-id="bfc54-258">For example, you may want to remove specific sites or add more sites to the list.</span></span> <span data-ttu-id="bfc54-259">Hierfür kann durch Überschreiben der `ResolveAddedSites` virtuelle Methode.</span><span class="sxs-lookup"><span data-stu-id="bfc54-259">This can be accomplished by overriding the `ResolveAddedSites` virtual method.</span></span> <span data-ttu-id="bfc54-260">Im folgenden Beispiel wird das Überschreiben der `ResolveAddedSites` -Methode, um einen Standort aus der Liste zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="bfc54-260">The sample below shows how to override the `ResolveAddedSites` method to remove one site from the list.</span></span> 

```C#
public override List<string> ResolveAddedSites(List<string> addedSites)
{
    // Use default TimerJob base class site resolving
    addedSites = base.ResolveAddedSites(addedSites);

    //Delete the first one from the list...simple change. A real life case could be reading the site scope 
    //from a SQL (Azure) DB to prevent the whole site resolving. 
    addedSites.RemoveAt(0);

    // return the updated list of resolved sites...this list will be processed by the Timer Job
    return addedSites;
}
```

### <a name="timerjobrun-event"></a><span data-ttu-id="bfc54-261">TimerJobRun-Ereignis</span><span class="sxs-lookup"><span data-stu-id="bfc54-261">TimerJobRun event</span></span> ###
<span data-ttu-id="bfc54-262">Den Timer Job-Framework wird die Liste der Websites in Batches Arbeit geteilt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-262">The Timer Job Framework splits the list of sites into work batches.</span></span> <span data-ttu-id="bfc54-263">Jedem Batch von Websites werden in einem eigenen Thread ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-263">Each batch of sites will be run on its own thread.</span></span> <span data-ttu-id="bfc54-264">In der Standardeinstellung erstellt das Framework fünf Batches und fünf Threads an, die diese fünf Batches ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-264">By default, the framework will create five batches and five threads to run those five batches.</span></span> <span data-ttu-id="bfc54-265">Siehe Abschnitt **Threading** erfahren Sie mehr über Zeitgeberauftrag threading-Optionen.</span><span class="sxs-lookup"><span data-stu-id="bfc54-265">See the **Threading** section to learn more about Timer Job threading options.</span></span> <span data-ttu-id="bfc54-266">Wenn ein Thread einen Batch verarbeitet die `TimerJobRun` -Ereignis wird ausgelöst, durch den Timer-Framework und bietet die erforderliche Informationen zum Ausführen des Zeitgeberauftrags.</span><span class="sxs-lookup"><span data-stu-id="bfc54-266">When a thread processes a batch the `TimerJobRun` event is triggered by the timer framework and will provide all the necessary information to run the Timer Job.</span></span> <span data-ttu-id="bfc54-267">Zeitgeberaufträge als Ereignisse, ausgeführt werden, sodass der Code einen Ereignishandler für eine Verbindung herstellen muss die `TimerJobRun` Ereignis:</span><span class="sxs-lookup"><span data-stu-id="bfc54-267">Timer Jobs are run as events, so the code must connect an event handler to the `TimerJobRun` event:</span></span>

```C#
public SimpleJob() : base("SimpleJob")
{
    TimerJobRun += SimpleJob_TimerJobRun;
}

void SimpleJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
{
    // your Timer Job logic goes here
}
```

<span data-ttu-id="bfc54-268">Ein alternativer Ansatz ist einen Inline-Delegaten wie folgt verwenden:</span><span class="sxs-lookup"><span data-stu-id="bfc54-268">An alternative approach is using an inline delegate as shown here:</span></span>

```C#
public SimpleJob() : base("SimpleJob")
{
    // Inline delegate
    TimerJobRun += delegate(object sender, TimerJobRunEventArgs e)
    {
        // your Timer Job logic goes here
    };
}
```

<span data-ttu-id="bfc54-269">Wenn die `TimerJobRun` -Ereignis ausgelöst wird eine `TimerJobRunEventArgs` Objekt, das die erforderliche Informationen zum Schreiben der Zeitgeberauftrag für die Logik ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="bfc54-269">When the `TimerJobRun` event fires you receive a `TimerJobRunEventArgs` object which provides the necessary information to write the Timer Job logic.</span></span> <span data-ttu-id="bfc54-270">Die folgenden Attribute und Methoden sind in dieser Klasse verfügbar:</span><span class="sxs-lookup"><span data-stu-id="bfc54-270">The following attributes and methods are available in this class:</span></span>

![Die Struktur der TimerJobRunEventArgs-Klasse](media/timerjob-framework/CRFBdwS.png)

<span data-ttu-id="bfc54-272">Mehrere Eigenschaften und alle Methoden sind in die optionale State Management-Funktion verwendet, die im nächsten Abschnitt erläutert werden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-272">Several of the properties and all of the methods are used in the optional state management feature which will be discussed in the next section.</span></span> <span data-ttu-id="bfc54-273">Die folgenden Eigenschaften können jedoch immer in jedes Ereignis, unabhängig von der verwendeten Konfiguration verfügbar sein:</span><span class="sxs-lookup"><span data-stu-id="bfc54-273">However the following properties will always be available in every event, regardless of the used configuration:</span></span>
- <span data-ttu-id="bfc54-274">**URL** -Eigenschaft: Dient zum Abrufen oder Festlegen der URL der Website für den Zeitgeberauftrag auswirken.</span><span class="sxs-lookup"><span data-stu-id="bfc54-274">**Url** property: Gets or sets the URL of the site for the Timer Job to operate against.</span></span> <span data-ttu-id="bfc54-275">Dies kann der Stammwebsite der Websitesammlung sein, aber eine Unterwebsite kann auch sein, für den Fall, dass Website erweitern vorgenommen wurde.</span><span class="sxs-lookup"><span data-stu-id="bfc54-275">This can be the root site of the site collection, but it can also be a sub site in case site expanding was done.</span></span>
- <span data-ttu-id="bfc54-276">**ConfigurationData** -Eigenschaft: Dient zum Abrufen oder Festlegen zusätzlicher Timer Job-Konfigurationsdaten (optional).</span><span class="sxs-lookup"><span data-stu-id="bfc54-276">**ConfigurationData** property: Gets or sets additional timer job configuration data (optional).</span></span> <span data-ttu-id="bfc54-277">Diese Konfigurationsdaten werden als Teil des übergeben der `TimerJobRunEventArgs` Objekt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-277">This configuration data is passed along as part of the `TimerJobRunEventArgs` object.</span></span>
- <span data-ttu-id="bfc54-278">**WebClientContext** -Eigenschaft: Dient zum Abrufen oder Festlegen der `ClientContext` -Objekt für den aktuellen URL.</span><span class="sxs-lookup"><span data-stu-id="bfc54-278">**WebClientContext** property: Gets or sets the `ClientContext` object for the current URL.</span></span> <span data-ttu-id="bfc54-279">Diese Eigenschaft ist ein `ClientContext` -Objekt für die Website in der *Url* -Eigenschaft definiert.</span><span class="sxs-lookup"><span data-stu-id="bfc54-279">This property is a `ClientContext` object for the site defined in the *Url* property.</span></span> <span data-ttu-id="bfc54-280">Dies ist üblicherweise der `ClientContext` -Objekt, das Sie in Ihrem Code Zeitgeberauftrag verwenden würden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-280">This is typically the `ClientContext` object that you would use in your Timer Job code.</span></span>
- <span data-ttu-id="bfc54-281">**SiteClientContext** -Eigenschaft: Dient zum Abrufen oder Festlegen der `ClientContext` -Objekt für die Stammwebsite der Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="bfc54-281">**SiteClientContext** property: Gets or sets the `ClientContext` object for the root site of the site collection.</span></span> <span data-ttu-id="bfc54-282">Diese Eigenschaft bietet Zugriff auf die Stammwebsite der Zeitgeberauftrag zum Zugriff darauf erforderlich sein soll.</span><span class="sxs-lookup"><span data-stu-id="bfc54-282">This property provides access to the root site should the Timer Job require access to it.</span></span> <span data-ttu-id="bfc54-283">Beispielsweise kann der Zeitgeberauftrag für ein Seitenlayout Gestaltungsvorlagenkatalog mithilfe der *SiteClientContext* -Eigenschaft hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="bfc54-283">For example, the Timer Job can add a page layout to the master page gallery using the *SiteClientContext* property.</span></span>
- <span data-ttu-id="bfc54-284">**TenantClientContext** -Eigenschaft: Dient zum Abrufen oder Festlegen der `ClientContext` -Objekt mit der Mandanten-API zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="bfc54-284">**TenantClientContext** property: Gets or sets the `ClientContext` object to work with the Tenant API.</span></span> <span data-ttu-id="bfc54-285">Diese Eigenschaft bietet eine `ClientContext`-Objekt, mit dem Mandanten Admin-Website-URL erstellt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-285">This property provides a `ClientContext`object constructed by using the tenant admin site URL.</span></span> <span data-ttu-id="bfc54-286">Verwenden der `Tenant` -API in den Zeitgeberauftrag `TimerJobRun` -Ereignishandler erstellen Sie ein neues `Tenant` Objekt unter Verwendung dieser Eigenschaft TenantClientContext.</span><span class="sxs-lookup"><span data-stu-id="bfc54-286">To use the `Tenant` API in the Timer Job `TimerJobRun` event handler, create a new `Tenant` object by using this TenantClientContext property.</span></span>

<span data-ttu-id="bfc54-287">Alle `ClientContext`Objekte verwenden, die Authentifizierungsinformationen angeben im Abschnitt **Authentifizierung** beschrieben.</span><span class="sxs-lookup"><span data-stu-id="bfc54-287">All `ClientContext`objects use the authentication information described in the **Authentication** section.</span></span> <span data-ttu-id="bfc54-288">Wenn Sie, für die Anmeldeinformationen des Benutzers entschieden haben stellen Sie sicher, dass das verwendete Konto die erforderlichen Berechtigungen für die angegebenen Websites ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-288">If you've opted for user credentials please ensure that the used account has the needed permissions to operate against the specified sites.</span></span> <span data-ttu-id="bfc54-289">Wenn Sie nur-app-verwenden, empfiehlt es sich für den nur-app-Prinzipal mandantenbereichsbezogenen Berechtigungen festzulegen.</span><span class="sxs-lookup"><span data-stu-id="bfc54-289">When using app-only, it is best to set tenant-scoped permissions to the app-only principal.</span></span>

### <a name="state-management"></a><span data-ttu-id="bfc54-290">State management</span><span class="sxs-lookup"><span data-stu-id="bfc54-290">State management</span></span> ###
<span data-ttu-id="bfc54-291">Beim Schreiben von Zeitgeberauftrag Logik müssen Sie häufig Zustand beizubehalten.</span><span class="sxs-lookup"><span data-stu-id="bfc54-291">When you write Timer Job logic you often need to persist state.</span></span> <span data-ttu-id="bfc54-292">Beispielsweise aufzeichnen, wenn der letzten Verarbeitung einer Website oder zum Speichern von Daten, um Ihre Geschäftslogik Zeitgeberauftrag zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="bfc54-292">For example, to record when a site was last processed, or to store data to support your Timer Job business logic.</span></span> <span data-ttu-id="bfc54-293">Aus diesem Grund hat den Timer Job-Framework State Management-Funktionen.</span><span class="sxs-lookup"><span data-stu-id="bfc54-293">For this reason, the Timer Job Framework has state management capabilities.</span></span> <span data-ttu-id="bfc54-294">State Management speichert und ruft eine Reihe von standardmäßigen und benutzerdefinierten Eigenschaften als serialisierten JSON-Zeichenfolge in der Web-Eigenschaftensammlung der verarbeiteten Website (Name = "_Properties" + Zeitgeberauftrag Name).</span><span class="sxs-lookup"><span data-stu-id="bfc54-294">State management stores and retrieves a set of standard and custom properties as a JSON serialized string in the web property bag of the processed site (name = Timer Job name + "_Properties").</span></span> <span data-ttu-id="bfc54-295">Im folgenden sind die Standardeigenschaften des der `TimerJobRunEventArgs`Objekt:</span><span class="sxs-lookup"><span data-stu-id="bfc54-295">The following are the default properties of the `TimerJobRunEventArgs`object:</span></span>
- <span data-ttu-id="bfc54-296">**PreviousRun** -Eigenschaft: Dient zum Abrufen oder festlegen, das Datum und die Uhrzeit der vorherigen Ausführung.</span><span class="sxs-lookup"><span data-stu-id="bfc54-296">**PreviousRun** property: Gets or sets the date and time of the previous run.</span></span>
- <span data-ttu-id="bfc54-297">**PreviousRunSuccessful** -Eigenschaft: Dient zum Abrufen oder Festlegen eines Werts, der angibt, ob die vorherige Ausführung erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="bfc54-297">**PreviousRunSuccessful** property: Gets or sets a value indicating whether the previous run was successful.</span></span> <span data-ttu-id="bfc54-298">Beachten Sie, dass der Zeitgeberauftrag zum Autor für kennzeichnen ein Projekt als erfolgreich ausführen, indem Sie die **CurrentRunSuccessful** -Eigenschaft als Teil der Zeitgeberauftrag für die Implementierung von zuständig ist</span><span class="sxs-lookup"><span data-stu-id="bfc54-298">Note that the Timer Job author is responsible for flagging a job run as successful by setting the **CurrentRunSuccessful** property as part of your Timer Job implementation</span></span>
- <span data-ttu-id="bfc54-299">**PreviousRunVersion** -Eigenschaft: Dient zum Abrufen oder festlegen die Zeitgeberauftrag für die Version von der vorherigen Ausführung.</span><span class="sxs-lookup"><span data-stu-id="bfc54-299">**PreviousRunVersion** property: Gets or sets the Timer Job version of the previous run.</span></span>

<span data-ttu-id="bfc54-300">Neben diesen Standardeigenschaften haben Sie auch die Möglichkeit, Ihre eigenen Eigenschaften festlegen, indem Sie Schlüsselwort - Wert-Paare an die `Properties` -Auflistung der `TimerJobRunEventArgs`Objekt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-300">Next to these standard properties you also have the option to specify your own properties by adding keyword - value pairs to the `Properties` collection of the `TimerJobRunEventArgs`object.</span></span> <span data-ttu-id="bfc54-301">Dies erleichtert es gibt drei Methoden, die Sie unterstützen:</span><span class="sxs-lookup"><span data-stu-id="bfc54-301">To make this easier there are three methods to help you:</span></span>
- <span data-ttu-id="bfc54-302">**SetProperty** fügt oder eine Eigenschaft aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="bfc54-302">**SetProperty** adds or updates a property.</span></span>
- <span data-ttu-id="bfc54-303">**GetProperty** gibt den Wert einer Eigenschaft zurück.</span><span class="sxs-lookup"><span data-stu-id="bfc54-303">**GetProperty** returns the value of a property.</span></span>
- <span data-ttu-id="bfc54-304">**DeleteProperty** entfernt eine Eigenschaft aus der Auflistung Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="bfc54-304">**DeleteProperty** removes a property from the property collection.</span></span>

<span data-ttu-id="bfc54-305">Der folgende Code zeigt, wie Statusverwaltung verwendet werden kann:</span><span class="sxs-lookup"><span data-stu-id="bfc54-305">The following code shows how state management can be used:</span></span>

```C#
void SiteGovernanceJob_TimerJobRun(object o, TimerJobRunEventArgs e)
{
    try
    {
        string library = "";

        // Get the number of admins
        var admins = e.WebClientContext.Web.GetAdministrators();

        Log.Info("SiteGovernanceJob", "ThreadID = {2} | Site {0} has {1} administrators.", e.Url, admins.Count, Thread.CurrentThread.ManagedThreadId);

        // grab reference to list
        library = "SiteAssets";
        List list = e.WebClientContext.Web.GetListByUrl(library);

        if (!e.GetProperty("ScriptFileVersion").Equals("1.0", StringComparison.InvariantCultureIgnoreCase))
        {
            if (list == null)
            {
                // grab reference to list
                library = "Style%20Library";
                list = e.WebClientContext.Web.GetListByUrl(library);
            }

            if (list != null)
            {
                // upload js file to list
                list.RootFolder.UploadFile("sitegovernance.js", "sitegovernance.js", true);

                e.SetProperty("ScriptFileVersion", "1.0");
            }
        }

        if (admins.Count < 2)
        {
            // Oops, we need at least 2 site collection administrators
            e.WebClientContext.Site.AddJsLink(SiteGovernanceJobKey, BuildJavaScriptUrl(e.Url, library));
            Console.WriteLine("Site {0} marked as incompliant!", e.Url);
            e.SetProperty("SiteCompliant", "false");
        }
        else
        {
            // We're all good...let's remove the notification
            e.WebClientContext.Site.DeleteJsLink(SiteGovernanceJobKey);
            Console.WriteLine("Site {0} is compliant", e.Url);
            e.SetProperty("SiteCompliant", "true");
        }

        e.CurrentRunSuccessful = true;
        e.DeleteProperty("LastError");
    }
    catch(Exception ex)
    {
        e.CurrentRunSuccessful = false;
        e.SetProperty("LastError", ex.Message);
    }
}
```

<span data-ttu-id="bfc54-306">Der Status wird gespeichert, wie eine einzelne JSON Eigenschaft, d. h. serialisiert dieser von anderen Anpassungen als auch verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="bfc54-306">The state is stored as a single JSON serialized property which means it can be used by other customizations as well.</span></span> <span data-ttu-id="bfc54-307">Wenn der Zeitgeberauftrag für den Zustandseintrag geschrieben haben beispielsweise "SiteCompliant = False", eine JavaScript-Routine konnte fordert den Benutzer auf, da der Zeitgeberauftrag festgestellt, dass die Website incompliant wurde fungieren.</span><span class="sxs-lookup"><span data-stu-id="bfc54-307">For example, if the Timer Job wrote the state entry "SiteCompliant=false", a JavaScript routine could prompt the user to act because the Timer Job determined that the site was incompliant.</span></span>

### <a name="threading"></a><span data-ttu-id="bfc54-308">Threading</span><span class="sxs-lookup"><span data-stu-id="bfc54-308">Threading</span></span> ###
<span data-ttu-id="bfc54-309">Den Timer Job-Framework standardmäßig verwendet Threads, um Arbeit zu parallelisieren.</span><span class="sxs-lookup"><span data-stu-id="bfc54-309">The Timer Job Framework by default uses threads to parallelize work.</span></span> <span data-ttu-id="bfc54-310">Threading wird für beide die Sub-Website-Erweiterung (falls erforderlich) und für die Ausführung verwendet die eigentliche Zeitgeberauftrag Logik (`TimerJobRun` -Ereignis) für jeden Standort.</span><span class="sxs-lookup"><span data-stu-id="bfc54-310">Threading is used for both the sub site expansion (when requested) and for the running the actual Timer Job logic (`TimerJobRun` event) for each site.</span></span> <span data-ttu-id="bfc54-311">Die folgenden Eigenschaften können zur Steuerung der Threads Implementierung verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="bfc54-311">The following properties can be used to control the threading implementation:</span></span>
- <span data-ttu-id="bfc54-312">**UseThreading** -Eigenschaft: Dient zum Abrufen oder Festlegen eines Werts, der angibt, ob threading verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="bfc54-312">**UseThreading** property: Gets or sets a value indicating whether threading will be used.</span></span> <span data-ttu-id="bfc54-313">Der Standardwert ist **true**.</span><span class="sxs-lookup"><span data-stu-id="bfc54-313">Defaults to **true**.</span></span>  <span data-ttu-id="bfc54-314">Alle Aktionen ausführen, mithilfe des Hauptfensters der Anwendungsthreads auf **false** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-314">Set to **false** to perform all actions by using the main application thread.</span></span>
- <span data-ttu-id="bfc54-315">**MaximumThreads** -Eigenschaft: Ruft ab oder legt die Anzahl der Threads an, die für diesen Zeitgeberauftrag verwenden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-315">**MaximumThreads** property: Gets or sets the number of threads to use for this Timer Job.</span></span> <span data-ttu-id="bfc54-316">Gültige Werte sind 2 bis 100.</span><span class="sxs-lookup"><span data-stu-id="bfc54-316">Valid values are 2 to 100.</span></span> <span data-ttu-id="bfc54-317">Der Standardwert ist 5.</span><span class="sxs-lookup"><span data-stu-id="bfc54-317">The default is 5.</span></span> <span data-ttu-id="bfc54-318">Viele der Threads ist nicht unbedingt schneller, und klicken Sie dann mit nur wenigen Threads.</span><span class="sxs-lookup"><span data-stu-id="bfc54-318">Having lots of threads is not necessarily faster then having just few threads.</span></span> <span data-ttu-id="bfc54-319">Die optimale Anzahl sollte über Tests mit einer Vielzahl von Thread zählt erworben werden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-319">The optimal number should be acquired via testing using a variety of thread counts.</span></span> <span data-ttu-id="bfc54-320">Der Standardwert von 5 Threads wurde erheblich steigern der Leistung in den meisten Szenarien gefunden.</span><span class="sxs-lookup"><span data-stu-id="bfc54-320">The default of 5 threads has been found to significantly boost performance in most scenarios.</span></span> 

#### <a name="throttling"></a><span data-ttu-id="bfc54-321">Drosselung</span><span class="sxs-lookup"><span data-stu-id="bfc54-321">Throttling</span></span> ####
<span data-ttu-id="bfc54-322">Da Zeitgeberauftrag threading verwendet und Zeitgeberauftrag Vorgänge in der Regel ressourcenintensive Vorgänge sind, konnte eine Ausführung des Zeitgeberauftrags gedrosselt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-322">Because Timer Job uses threading and Timer Job operations are typically resource intensive operations, a Timer Job run could be throttled.</span></span> <span data-ttu-id="bfc54-323">Um ordnungsgemäß befassen sich mit den Timer Job-Framework und dem gesamten verwendet Plug & Play-Core-Einschränkung der `ExecuteQueryRetry` Methode anstatt vom standardmäßigen `ExecuteQuery`Methode.</span><span class="sxs-lookup"><span data-stu-id="bfc54-323">In order to correctly deal with throttling the Timer Job Framework and the whole of PnP Core uses the `ExecuteQueryRetry` method instead of the default `ExecuteQuery`method.</span></span>

> [!NOTE] 
> <span data-ttu-id="bfc54-324">Es ist wichtig, verwenden Sie `ExecuteQueryRetry` in Ihrem Code zur Implementierung des Zeitgeberauftrags.</span><span class="sxs-lookup"><span data-stu-id="bfc54-324">It is important to use `ExecuteQueryRetry` in your Timer Job implementation code.</span></span>

#### <a name="concurrency-issues---process-all-sub-sites-of-a-site-collection-in-the-same-thread"></a><span data-ttu-id="bfc54-325">Parallelität Probleme mit – verarbeiten alle Unterwebsites einer Websitesammlung in demselben thread</span><span class="sxs-lookup"><span data-stu-id="bfc54-325">Concurrency issues - process all sub sites of a site collection in the same thread</span></span> ####

<span data-ttu-id="bfc54-326">Zeitgeberaufträge möglicherweise Parallelitätsprobleme bei der Verwendung von mehreren Threads zum Verarbeiten von Unterwebsites.</span><span class="sxs-lookup"><span data-stu-id="bfc54-326">Timer Jobs may have concurrency issues when using multiple threads to process sub sites.</span></span> <span data-ttu-id="bfc54-327">Nehmen Sie dieses Beispiel: Thread A verarbeitet den ersten Satz von Sub-Websites aus der Websitesammlung 1 und Thread B die restlichen die Sub-Websites aus der Websitesammlung 1 verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="bfc54-327">Take this example: Thread A processes the first set of sub sites from site collection 1, and thread B processes the rest of the sub sites from site collection 1.</span></span> <span data-ttu-id="bfc54-328">Wenn der Zeitgeberauftrag für die Unterwebsite und der Stammwebsite verarbeitet (mithilfe der `SiteClientContext` Object), es kann ein Problem Parallelität seit beide Thread A und Thread B Verarbeiten der Stammwebsite.</span><span class="sxs-lookup"><span data-stu-id="bfc54-328">If the Timer Job processes the sub site and the root site (by using the `SiteClientContext` object), there could be a concurrency issue since both thread A and thread B process the root site.</span></span> <span data-ttu-id="bfc54-329">Die Verwendung der Parallelität Problem (ohne den Timer Jobs in einen einzelnen Thread ausgeführt) vermeiden der `GetAllSubSites` Methode innerhalb des Zeitgeberauftrags.</span><span class="sxs-lookup"><span data-stu-id="bfc54-329">To avoid the concurrency issue (without running the Timer Jobs in a single thread) use the `GetAllSubSites` method within the Timer Job.</span></span>

<span data-ttu-id="bfc54-330">Der folgende Code zeigt, wie Sie mit der `GetAllSubSites` Methode innerhalb eines Zeitgeberauftrags:</span><span class="sxs-lookup"><span data-stu-id="bfc54-330">The following code shows how to use the `GetAllSubSites` method within a Timer Job:</span></span>

```C#
public class SiteCollectionScopedJob: TimerJob
{
    public SiteCollectionScopedJob() : base("SiteCollectionScopedJob")
    {
        // ExpandSites *must* be false as we'll deal with that at TimerJobEvent level
        ExpandSubSites = false;
        TimerJobRun += SiteCollectionScopedJob_TimerJobRun;
    }

    void SiteCollectionScopedJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
    {
        // Get all the sub sites in the site we're processing
        IEnumerable<string> expandedSites = GetAllSubSites(e.SiteClientContext.Site);

        // Manually iterate over the content
        foreach (string site in expandedSites)
        {
            // Clone the existing ClientContext for the sub web
            using (ClientContext ccWeb = e.SiteClientContext.Clone(site))
            {
                // Here's the Timer Job logic, but now a single site collection is handled in a single thread which 
                // allows for further optimization or prevents race conditions
                ccWeb.Load(ccWeb.Web, s => s.Title);
                ccWeb.ExecuteQueryRetry();
                Console.WriteLine("Here: {0} - {1}", site, ccWeb.Web.Title);
            }
        }
    }
}
```

### <a name="logging"></a><span data-ttu-id="bfc54-331">Protokollierung</span><span class="sxs-lookup"><span data-stu-id="bfc54-331">Logging</span></span> ###
<span data-ttu-id="bfc54-332">Den Timer Job-Framework verwendet die Protokollierung Plug & Play-Core-Komponenten als Teil der die Plug & Play-Core-Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="bfc54-332">The Timer Job Framework uses the PnP Core logging components as it's part of the PnP Core library.</span></span> <span data-ttu-id="bfc54-333">Um die integrierten Plug & Play-Kern-Protokollierung zu aktivieren, konfigurieren sie mithilfe der entsprechenden Konfigurationsdatei (app.config oder web.config).</span><span class="sxs-lookup"><span data-stu-id="bfc54-333">To activate the built-in PnP Core logging, configure it using the appropriate config file (app.config or web.config).</span></span> <span data-ttu-id="bfc54-334">Das folgende Beispiel zeigt die erforderliche Syntax:</span><span class="sxs-lookup"><span data-stu-id="bfc54-334">The following example shows the required syntax:</span></span>

```XML
  <system.diagnostics>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="DebugListenter" type="System.Diagnostics.TextWriterTraceListener" initializeData="trace.log" />
        <!--<add name="consoleListener" type="System.Diagnostics.ConsoleTraceListener" />-->
      </listeners>
    </trace>
  </system.diagnostics>
```

<span data-ttu-id="bfc54-335">Mithilfe der oben genannten Konfigurationsdatei den Timer Job-Framework verwendet die `System.Diagnostics.TextWriterTraceListener` , Protokolle in eine Datei namens trace.log im selben Ordner wie die .exe-Zeitgeberauftrag zu schreiben.</span><span class="sxs-lookup"><span data-stu-id="bfc54-335">Using the above configuration file the Timer Job Framework will use the `System.Diagnostics.TextWriterTraceListener` to write logs to a file called trace.log in the same folder as the Timer Job .exe.</span></span> <span data-ttu-id="bfc54-336">Andere Trace-Listener sind verfügbar, wie beispielsweise:</span><span class="sxs-lookup"><span data-stu-id="bfc54-336">Other trace listeners are available such as:</span></span>
- <span data-ttu-id="bfc54-337">**ConsoleTraceListener** schreibt Protokolle in der Konsole angezeigt.</span><span class="sxs-lookup"><span data-stu-id="bfc54-337">**ConsoleTraceListener** writes logs to the console.</span></span>
- <span data-ttu-id="bfc54-338">Die Methode in der [Cloud Diagnose - Steuerelement übernehmen der Protokollierung werden und Verfolgung in Windows Azure](https://msdn.microsoft.com/en-us/magazine/ff714589.aspx)beschrieben.</span><span class="sxs-lookup"><span data-stu-id="bfc54-338">The method described in [Cloud Diagnostics - Take Control of Logging and Tracing in Windows Azure](https://msdn.microsoft.com/en-us/magazine/ff714589.aspx).</span></span> <span data-ttu-id="bfc54-339">Diese Methode wird die Microsoft.WindowsAzure.Diagnostics verwendet. **DiagnosticMonitorTraceListener**.</span><span class="sxs-lookup"><span data-stu-id="bfc54-339">This method uses Microsoft.WindowsAzure.Diagnostics.**DiagnosticMonitorTraceListener**.</span></span> <span data-ttu-id="bfc54-340">Zusätzliche Ressourcen Azure finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="bfc54-340">Additional Azure resources can be found here:</span></span>
    - [<span data-ttu-id="bfc54-341">Aktivieren Sie das Diagnoseprotokoll für Azure-Websites</span><span class="sxs-lookup"><span data-stu-id="bfc54-341">Enable diagnostic logging for Azure Websites</span></span>](http://azure.microsoft.com/en-us/documentation/articles/web-sites-enable-diagnostic-log/)
    - [<span data-ttu-id="bfc54-342">Problembehandlung von Azure Websites in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bfc54-342">Troubleshooting Azure Websites in Visual Studio</span></span>](http://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<span data-ttu-id="bfc54-343">Es wird dringend empfohlen, den gleichen Ansatz für die Protokollierung für den benutzerdefinierten Zeitgeberauftrag Code verwenden, wie für den Timer Job-Framework.</span><span class="sxs-lookup"><span data-stu-id="bfc54-343">It is strongly advised to use the same logging approach for your custom Timer Job code as you do for the Timer Job Framework.</span></span> <span data-ttu-id="bfc54-344">In Ihrem Code Zeitgeberauftrag können die Plug & Play-Core `Log` Klasse:</span><span class="sxs-lookup"><span data-stu-id="bfc54-344">In your Timer Job code you can use the PnP Core `Log` class:</span></span>

```C#
void SiteGovernanceJob_TimerJobRun(object o, TimerJobRunEventArgs e)
{
    try
    {
        string library = "";

        // Get the number of admins
        var admins = e.WebClientContext.Web.GetAdministrators();

        Log.Info("SiteGovernanceJob", "ThreadID = {2} | Site {0} has {1} administrators.", e.Url, admins.Count, Thread.CurrentThread.ManagedThreadId);

        // Additional Timer Job logic...

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
