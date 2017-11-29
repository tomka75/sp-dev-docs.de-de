---
title: Verwenden Sie Microsoft Azure WebJobs mit Office 365
ms.date: 11/03/2017
ms.openlocfilehash: 0b3eb304efb291dfa4c0bb7c0809f2c5b044d28f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="use-microsoft-azure-webjobs-with-office-365"></a><span data-ttu-id="50565-102">Verwenden Sie Microsoft Azure WebJobs mit Office 365</span><span class="sxs-lookup"><span data-stu-id="50565-102">Use Microsoft Azure WebJobs with Office 365</span></span>

<span data-ttu-id="50565-103">Verwenden von Azure WebJobs Zeitgeberaufträge implementieren, die SharePoint Online zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="50565-103">Use Azure WebJobs to implement timer jobs that can access SharePoint Online.</span></span>

<span data-ttu-id="50565-104">_**Gilt für:** Add-Ins für SharePoint | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="50565-104">_**Applies to:** add-ins for SharePoint | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="50565-105">**Bereitgestellt von:** Tobias Zimmergren</span><span class="sxs-lookup"><span data-stu-id="50565-105">**Provided by:** Tobias Zimmergren</span></span>

<span data-ttu-id="50565-106">Implementieren Sie Timer Job Funktionen mit [Microsoft Azure WebJobs](http://azure.microsoft.com/documentation/articles/websites-webjobs-resources/) oder Windows-Taskplaner zum Ausführen von Aufgaben in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="50565-106">Implement timer job functionality using  [Microsoft Azure WebJobs](http://azure.microsoft.com/documentation/articles/websites-webjobs-resources/) or Windows Task Scheduler to perform tasks in SharePoint Online.</span></span> <span data-ttu-id="50565-107">Ein Zeitgeberauftrag ist ein wiederholte, geplanten, Hintergrundprozess, der in SharePoint für bestimmte Aufgaben ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="50565-107">A timer job is a repetitive, scheduled, background process that runs in SharePoint to perform certain tasks.</span></span> <span data-ttu-id="50565-108">Beispielsweise sollten Sie einen Zeitgeberauftrag zum Kopieren von Daten in einer SharePoint-Liste in eine Datenbank eingegeben.</span><span class="sxs-lookup"><span data-stu-id="50565-108">For example, you may want a timer job to copy data entered in a SharePoint list to a database.</span></span> <span data-ttu-id="50565-109">In SharePoint Online und kann nicht farmlösungen, bereitgestellt werden, also wie Zeitgeberaufträge in der Vergangenheit bereitgestellt wurden.</span><span class="sxs-lookup"><span data-stu-id="50565-109">In SharePoint Online, you cannot deploy farm solutions, which is how timer jobs were deployed in the past.</span></span> <span data-ttu-id="50565-110">Um ähnliche Timer Job-Funktionen in SharePoint Online zu implementieren, müssen Sie eine Konsolenanwendung als ein WebJob Azure ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="50565-110">To implement similar timer job functionality in SharePoint Online, you need to run a console application as an Azure WebJob.</span></span> <span data-ttu-id="50565-111">Die Konsolenanwendung greift auf SharePoint Online mit dem clientseitigen Objektmodell (CSOM).</span><span class="sxs-lookup"><span data-stu-id="50565-111">The console application accesses SharePoint Online using the client-side object model (CSOM).</span></span> <span data-ttu-id="50565-112">Dieser Artikel enthält Informationen zu den grundlegenden Konzepten vertraut, die bei der Bereitstellung von konsolenanwendungen als Azure WebJobs zum Ausführen von und Zugreifen auf SharePoint Online-Websites und den Inhalt.</span><span class="sxs-lookup"><span data-stu-id="50565-112">This article presents the basic concepts involved in deploying console applications as Azure WebJobs to run and access your SharePoint Online sites and content.</span></span>

## <a name="create-and-run-a-console-application-as-an-azure-webjob"></a><span data-ttu-id="50565-113">Erstellen Sie und führen Sie eine Konsolenanwendung als ein WebJob Azure</span><span class="sxs-lookup"><span data-stu-id="50565-113">Create and run a console application as an Azure WebJob</span></span>
<span data-ttu-id="50565-114"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="50565-114"></span></span>

<span data-ttu-id="50565-115">Informationen zum Einrichten der Konsolenanwendung zum Ausführen als einem Azure WebJob müssen Sie:</span><span class="sxs-lookup"><span data-stu-id="50565-115">To set up your console application to run as an Azure WebJob, you need to:</span></span>

1. <span data-ttu-id="50565-116">Erstellen eines Kontos Organisation für die Azure WebJob zu verwenden, um SharePoint-Websites und Inhalte zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="50565-116">Create an organization account for the Azure WebJob to use to access your SharePoint sites and content.</span></span>
    
2. <span data-ttu-id="50565-117">Erstellen und Einrichten der Konsolenanwendung.</span><span class="sxs-lookup"><span data-stu-id="50565-117">Create and set up the console application.</span></span>
    
3. <span data-ttu-id="50565-118">Fügen Sie Code hinzu, um die Konsolenanwendung.</span><span class="sxs-lookup"><span data-stu-id="50565-118">Add code to the console application.</span></span>
    
4. <span data-ttu-id="50565-119">Veröffentlichen Sie die Konsolenanwendung als einem Azure WebJob.</span><span class="sxs-lookup"><span data-stu-id="50565-119">Publish your console application as an Azure WebJob.</span></span>
    
5. <span data-ttu-id="50565-120">Führen Sie aus, und überprüfen Sie Ihre Azure WebJob.</span><span class="sxs-lookup"><span data-stu-id="50565-120">Run and verify your Azure WebJob.</span></span>

## <a name="create-an-organization-account"></a><span data-ttu-id="50565-121">Erstellen Sie ein Konto für die Organisation</span><span class="sxs-lookup"><span data-stu-id="50565-121">Create an organization account</span></span>
<span data-ttu-id="50565-122"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="50565-122"></span></span>

<span data-ttu-id="50565-123">Sie müssen zum Erstellen eines Kontos für die Azure WebJob beim Zugriff auf SharePoint-Websites und Inhalte verwenden.</span><span class="sxs-lookup"><span data-stu-id="50565-123">You need to create an account for the Azure WebJob to use when accessing SharePoint sites and content.</span></span> <span data-ttu-id="50565-124">Weitere Informationen finden Sie unter [Hinzufügen von Benutzern einzeln zu Office 365-Admin-Hilfe](https://support.office.microsoft.com/article/Add-users-individually-to-Office-365---Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec).</span><span class="sxs-lookup"><span data-stu-id="50565-124">For more information, see  [Add users individually to Office 365-Admin Help](https://support.office.microsoft.com/article/Add-users-individually-to-Office-365---Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec).</span></span> <span data-ttu-id="50565-125">Wenn der Azure-WebJob ausgeführt wird, wird das Feld **Geändert von** speichert und zeigt den Wert im **Anzeigename den Namen** des Kontos Organisation eingegeben.</span><span class="sxs-lookup"><span data-stu-id="50565-125">When the Azure WebJob runs, the  **Modified By** field stores and displays the value entered in **Display name** of the organization account.</span></span> <span data-ttu-id="50565-126">Stellen Sie sicher, dass Sie einen Anzeigenamen auswählen, den Ihre Benutzer auf einfache Weise als das Konto für den Zugriff auf SharePoint, die WebJob Azure verwendet identifizieren können.</span><span class="sxs-lookup"><span data-stu-id="50565-126">Ensure you choose a display name that your users can easily identify as the account used by the Azure WebJob for accessing SharePoint.</span></span>

## <a name="create-and-set-up-the-console-application"></a><span data-ttu-id="50565-127">Erstellen und Einrichten der Konsolenanwendung</span><span class="sxs-lookup"><span data-stu-id="50565-127">Create and set up the console application</span></span>
<span data-ttu-id="50565-128"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="50565-128"></span></span>

<span data-ttu-id="50565-129">So erstellen Sie eine Konsolenanwendung zum Ausführen als einem Azure WebJob, führen Sie die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="50565-129">To create a console application to run as an Azure WebJob, perform the following steps:</span></span>

1. <span data-ttu-id="50565-130">Erstellen Sie ein neues Konsolenanwendungsprojekt durch:</span><span class="sxs-lookup"><span data-stu-id="50565-130">Create a new console application project by:</span></span>
    
    1. <span data-ttu-id="50565-131">Wählen Sie **Neues Projekt**in Visual Studio > **Visual C#-** > **Konsolenanwendung** > **OK**.</span><span class="sxs-lookup"><span data-stu-id="50565-131">In Visual Studio, choose  **New Project** > **Visual C#** > **Console Application** > **OK**.</span></span>
    
    2. <span data-ttu-id="50565-132">Nachdem die Konsolenanwendung erstellt wurde, wählen Sie **Extras** > **NuGet Package Manager** > **Manage NuGet Packages for Solution...**  >  **Online** > **Alle**.</span><span class="sxs-lookup"><span data-stu-id="50565-132">After the console application is created, choose  **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution...** > **Online** > **All**.</span></span>
    
    3. <span data-ttu-id="50565-133">Suche für **App für SharePoint Web Toolkit**.</span><span class="sxs-lookup"><span data-stu-id="50565-133">Search for  **App for SharePoint Web Toolkit**.</span></span>
    
    4. <span data-ttu-id="50565-134">Wählen Sie **Installieren aus**, und wählen Sie dann **OK**.</span><span class="sxs-lookup"><span data-stu-id="50565-134">Choose  **Install**, then choose  **OK**.</span></span>
    
    5. <span data-ttu-id="50565-135">Wählen Sie **Schließen**.</span><span class="sxs-lookup"><span data-stu-id="50565-135">Choose  **Close**.</span></span>
    
    6. <span data-ttu-id="50565-136">Stellen Sie sicher, dass die Konsolenanwendungsprojekt SharePointContext.cs und TokenHelper.cs hinzugefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="50565-136">Verify that SharePointContext.cs and TokenHelper.cs were added to the console application project.</span></span>
    
2. <span data-ttu-id="50565-137">Speichern Sie Ihre Kontoinformationen in app.config durch Hinzufügen des **AppSettings** -Elements dargestellt.</span><span class="sxs-lookup"><span data-stu-id="50565-137">Save your account information in the app.config by adding the  **appSettings** element shown.</span></span> <span data-ttu-id="50565-138">Ändern Sie **SPOAccount** und **SPOPassword** in den Benutzernamen und das Kennwort des Kontos Organisation an, die Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="50565-138">Change **SPOAccount** and **SPOPassword** to the user name and password of the organization account you created previously.</span></span>
    
    ```XML
    <?xml version="1.0" encoding="utf-8" ?>
     <configuration>
      <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
      </startup>
      <appSettings>
        <add key="SPOAccount" value="admin@contoso.onmicrosoft.com"/>
        <add key="SPOPassword" value="Contoso"/>
      </appSettings>
     </configuration>
    ```

    <span data-ttu-id="50565-139">**Vorsicht**  App.config werden Benutzernamen und das Kennwort des Kontos der Organisation in Klartext gespeichert.</span><span class="sxs-lookup"><span data-stu-id="50565-139">**Caution**  App.config stores the organization account's username and password in clear text.</span></span> <span data-ttu-id="50565-140">Diese Methode wird nur zur Veranschaulichung verwendet und sollte nicht in der produktionsbereitstellung von Ihrer WebJobs Azure verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="50565-140">This method is used for demonstration purposes only, and should not be used in your production deployment of your Azure WebJobs.</span></span> <span data-ttu-id="50565-141">Es wird empfohlen, das Kennwort verschlüsseln oder authentifizieren Zugriffstoken mit OAuth.</span><span class="sxs-lookup"><span data-stu-id="50565-141">We recommend encrypting the password, or authenticating using OAuth with access tokens.</span></span> <span data-ttu-id="50565-142">Weitere Informationen finden Sie unter Kirk Evans Blogbeitrag zum [Erstellen eines SharePoint-Add-Ins als einen Zeitgeberauftrag](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx).</span><span class="sxs-lookup"><span data-stu-id="50565-142">For more information, see Kirk Evans blog post on  [Building a SharePoint Add-in as a Timer Job](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx).</span></span>

## <a name="add-code-to-the-console-application"></a><span data-ttu-id="50565-143">Fügen Sie Code hinzu, um die Konsolenanwendung</span><span class="sxs-lookup"><span data-stu-id="50565-143">Add code to the console application</span></span>
<span data-ttu-id="50565-144"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="50565-144"></span></span>

<span data-ttu-id="50565-145">Fügen Sie den folgenden Code in Program.cs um die Konsolenanwendung.</span><span class="sxs-lookup"><span data-stu-id="50565-145">In Program.cs, add the following code to the console application.</span></span>

<span data-ttu-id="50565-146">**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.</span><span class="sxs-lookup"><span data-stu-id="50565-146">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>


1. <span data-ttu-id="50565-147">Fügen Sie **using** -Anweisungen hinzu.</span><span class="sxs-lookup"><span data-stu-id="50565-147">Add  **using** statements.</span></span>
    
    ```C#
    using Microsoft.SharePoint.Client;
    using System.Security;
    using System.Configuration; 
    ```

2. <span data-ttu-id="50565-148">Fügen Sie der Klasse die folgenden Methoden:</span><span class="sxs-lookup"><span data-stu-id="50565-148">Add the following methods to your class:</span></span>
    
    -  <span data-ttu-id="50565-149">**Main** meldet sich in Ihrer SharePoint-Website, und klicken Sie dann das CSOM zum Ausführen von Aufgaben auf Ihrer Website oder einer Inhaltsdatenbank verwendet.</span><span class="sxs-lookup"><span data-stu-id="50565-149">**Main** signs into your SharePoint site, and then uses the CSOM to perform tasks on your site or content.</span></span> <span data-ttu-id="50565-150">In diesem Codebeispiel wird das CSOM zum Hier finden eine Liste und die Ausgabe der Gesamtanzahl der Elemente, die in der Liste im Konsolenfenster sind verwendet.</span><span class="sxs-lookup"><span data-stu-id="50565-150">This code sample uses the CSOM to find a list and output the total number of items that are in the list to the console window.</span></span> <span data-ttu-id="50565-151">Bei Verwendung von Azure WebJobs sehen Sie die Ausgabe im Konsolenfenster WebJob führen Sie nähere Informationen dazu, die in [führen, und überprüfen Sie Ihre Azure WebJob](Use-Microsoft-Azure-WebJobs-with-Office-365.md#runandverify)erläutert wird.</span><span class="sxs-lookup"><span data-stu-id="50565-151">When using Azure WebJobs, you can see the console window output in the WebJob Run Details, which is explained in [Run and verify your Azure WebJob](Use-Microsoft-Azure-WebJobs-with-Office-365.md#runandverify).</span></span>
    
  -  <span data-ttu-id="50565-152">**GetSPOSecureStringPassword** liest das Kennwort aus app.config.</span><span class="sxs-lookup"><span data-stu-id="50565-152">**GetSPOSecureStringPassword** reads your password from app.config.</span></span>
    
  -  <span data-ttu-id="50565-153">**GetSPOAccountName** liest Ihren Benutzernamen in app.config.</span><span class="sxs-lookup"><span data-stu-id="50565-153">**GetSPOAccountName** reads your username from app.config.</span></span>

    ```C#
    static void Main(string[] args)
        {
            using (ClientContext context = new ClientContext("https://contoso.sharepoint.com"))
            {
                // Use default authentication mode.
                context.AuthenticationMode = ClientAuthenticationMode.Default;                 
                context.Credentials = new SharePointOnlineCredentials(GetSPOAccountName(), GetSPOSecureStringPassword());
    
                // Add your CSOM code to perform tasks on your sites and content.
    
                try
                {
                    List objList = context.Web.Lists.GetByTitle("Docs");
                    context.Load(objList);
                    context.ExecuteQuery();
    
                    if (objList != null &amp;&amp; objList.ItemCount > 0)
                    {
                        Console.WriteLine(objList.Title.ToString() + " has " + objList.ItemCount + " items.");
                    }
    
                }
                catch (Exception ex)
                {
                    Console.WriteLine("ERROR: " + ex.Message);
                    Console.WriteLine("ERROR: " + ex.Source);
                    Console.WriteLine("ERROR: " + ex.StackTrace);
                    Console.WriteLine("ERROR: " + ex.InnerException);
    
                }
            }
                
        }
    
    private static SecureString GetSPOSecureStringPassword()
    {
      try
      {
          Console.WriteLine("Entered GetSPOSecureStringPassword.");
          var secureString = new SecureString();
          foreach (char c in ConfigurationManager.AppSettings["SPOPassword"])
          {
              secureString.AppendChar(c);
          }
          Console.WriteLine("Constructed the secure password.");
    
          return secureString;
      }
      catch
      {
          throw;
      }
    }
    
    private static string GetSPOAccountName()
    {
      try
      {
          Console.WriteLine("Entered GetSPOAccountName.");
          return ConfigurationManager.AppSettings["SPOAccount"];
      }
      catch
      {
          throw;
      }
    }
    
    ```

## <a name="publish-your-console-application-as-an-azure-webjob"></a><span data-ttu-id="50565-154">Veröffentlichen Sie die Konsolenanwendung als einem Azure WebJob</span><span class="sxs-lookup"><span data-stu-id="50565-154">Publish your console application as an Azure WebJob</span></span>
<span data-ttu-id="50565-155"><a name="sectionSection4"> </a></span><span class="sxs-lookup"><span data-stu-id="50565-155"></span></span>

<span data-ttu-id="50565-156">Sie abschließend Konsolenanwendung entwickeln, müssen Sie die Konsolenanwendung als einem Azure WebJob bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="50565-156">When you are finished developing your console application, you need to deploy the console application as an Azure WebJob.</span></span> <span data-ttu-id="50565-157">Zum Bereitstellen der Konsolenanwendung als einem Azure WebJob können Sie folgende Aktionen ausführen:</span><span class="sxs-lookup"><span data-stu-id="50565-157">To deploy your console application as an Azure WebJob, you can:</span></span>

- <span data-ttu-id="50565-158">Hochladen der Binärdateien zu einer Azure-Web-App, und Erstellen einer Azure WebJob mithilfe des [Microsoft Azure-Verwaltungsportal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="50565-158">Upload your binaries to an Azure Web App, and create an Azure WebJob using the  [Microsoft Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="50565-159">Die Binärdateien für Visual Studio-Projekt befindet sich im Bin/Debug oder Bin/Release Ordner der Visual Studio-Projekt.</span><span class="sxs-lookup"><span data-stu-id="50565-159">The binaries for your Visual Studio project can be found in the bin/Debug or bin/Release folders of your Visual Studio project.</span></span> <span data-ttu-id="50565-160">Zum Erstellen der Azure-Web-App, und Laden Sie die Binärdateien hoch, führen Sie die Schritte in [Erstellen einer ASP.NET Web-app in Azure App-Dienst](http://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span><span class="sxs-lookup"><span data-stu-id="50565-160">To create the Azure Web App and upload the binaries, follow the steps in  [Create an ASP.NET web app in Azure App Service](http://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span> <span data-ttu-id="50565-161">So erstellen Sie Ihre auf Anforderung, fortlaufenden oder geplanten Azure WebJob, finden Sie unter [Hintergrund ausführen von Aufgaben mit WebJobs](http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/).</span><span class="sxs-lookup"><span data-stu-id="50565-161">To create your on demand, continuous, or scheduled Azure WebJob, see  [Run Background tasks with WebJobs](http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/).</span></span>
    
- <span data-ttu-id="50565-162">Veröffentlichen Sie Ihre Azure WebJob von Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="50565-162">Publish your Azure WebJob from Visual Studio.</span></span> <span data-ttu-id="50565-163">Weitere Informationen finden Sie unter [Aktivieren WebJobs Bereitstellung ohne ein Webprojekt](http://azure.microsoft.com/documentation/articles/websites-dotnet-deploy-webjobs/#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="50565-163">For more information, see  [Enable WebJobs deployment without a web project](http://azure.microsoft.com/documentation/articles/websites-dotnet-deploy-webjobs/#convertnolink).</span></span>
    
## <a name="run-and-verify-your-azure-webjob"></a><span data-ttu-id="50565-164">Führen Sie aus und überprüfen Sie Ihre Azure WebJob</span><span class="sxs-lookup"><span data-stu-id="50565-164">Run and verify your Azure WebJob</span></span>
<span data-ttu-id="50565-165"><a name="runandverify"> </a></span><span class="sxs-lookup"><span data-stu-id="50565-165"></span></span>

<span data-ttu-id="50565-166">Klicken Sie nach Abschluss der vorherigen Schritte aus, sollte Ihre WebJob Azure ausgeführt und Aufgaben in Office 365-Abonnements.</span><span class="sxs-lookup"><span data-stu-id="50565-166">After completing all the previous steps, your Azure WebJob should be running and performing tasks in your Office 365 subscription.</span></span> <span data-ttu-id="50565-167">Unter Umständen müssen Sie zum Ausführen der Wartung oder Problembehandlung Ihrer Azure WebJobs.</span><span class="sxs-lookup"><span data-stu-id="50565-167">At times, you may need to perform maintenance or troubleshoot your Azure WebJobs.</span></span> <span data-ttu-id="50565-168">So überprüfen, dass Ihre WebJob Azure ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="50565-168">To verify that your Azure WebJob is running:</span></span>

- <span data-ttu-id="50565-169">Wenn Ihre Azure WebJob ein SharePoint-Element, wie ein Listenelement aktualisiert wird das Feld **Geändert von** der Organisation Konto an, dem die Azure WebJob verwendet, um Zugriff auf SharePoint angezeigt.</span><span class="sxs-lookup"><span data-stu-id="50565-169">If your Azure WebJob updated a SharePoint item, like a list item, the  **Modified By** field displays the organization account that the Azure WebJob used to access SharePoint.</span></span>
    
- <span data-ttu-id="50565-170">Überprüfen Sie die Protokolle WebJob Details für Ihre Azure WebJob.</span><span class="sxs-lookup"><span data-stu-id="50565-170">Review the WebJob Details logs for your Azure WebJob.</span></span> <span data-ttu-id="50565-171">Mit dem WebJob Details Protokolle können Sie überprüfen, wenn ein Auftrag ausgeführt haben, den Erfolg oder Misserfolg eines Auftrags für den führen keine Ausgabe aus der WebJob (beispielsweise beim Aufruf von Console.WriteLine) sowie andere Details des Auftrags ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="50565-171">The WebJob Details logs lets you review when a job ran, the success or failure of a job run, any output from the WebJob (for example, when Console.WriteLine was called), and other details of the job run.</span></span> <span data-ttu-id="50565-172">Weitere Informationen finden Sie im Abschnitt Auftragsverlauf anzeigen für [Vorgänge mit WebJobs Hintergrund ausführen](http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/).</span><span class="sxs-lookup"><span data-stu-id="50565-172">For more information, see the section View the job history on  [Run Background tasks with WebJobs](http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="50565-173">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="50565-173">Additional resources</span></span>
<span data-ttu-id="50565-174"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="50565-174"></span></span>

-  <span data-ttu-id="50565-175">[Office 365 Development Mustern und Methoden ausgesprochen](Office-365-development-patterns-and-practices-solution-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="50565-175">[Office 365 development patterns and practices solution guidance](Office-365-development-patterns-and-practices-solution-guidance.md).</span></span>
    
-  <span data-ttu-id="50565-176">[Erstellen Sie eine .NET WebJob in Azure App-Dienst](http://azure.microsoft.com/documentation/articles/websites-dotnet-webjobs-sdk-get-started/).</span><span class="sxs-lookup"><span data-stu-id="50565-176">[Create a .NET WebJob in Azure App Service](http://azure.microsoft.com/documentation/articles/websites-dotnet-webjobs-sdk-get-started/).</span></span>
    
-  <span data-ttu-id="50565-177">[Azure WebJobs Ressourcen](http://azure.microsoft.com/documentation/articles/websites-webjobs-resources/).</span><span class="sxs-lookup"><span data-stu-id="50565-177">[Azure WebJobs resources](http://azure.microsoft.com/documentation/articles/websites-webjobs-resources/).</span></span>
