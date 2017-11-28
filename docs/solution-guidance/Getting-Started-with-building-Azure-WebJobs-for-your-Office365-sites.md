---
title: "Erste Schritte mit Azure WebJobs (\"Zeitgeberaufträge\") für Ihre Office 365-Websites #"
ms.date: 11/03/2017
ms.openlocfilehash: 34adf8616224a7f098f336165f120dcb3cde1a6f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="getting-started-with-azure-webjobs-timer-jobs-for-your-office-365-sites"></a><span data-ttu-id="fe9ef-102">Erste Schritte mit Azure WebJobs ("Zeitgeberaufträge") für Ihre Office 365-Websites</span><span class="sxs-lookup"><span data-stu-id="fe9ef-102">Getting Started with azure WebJobs ("timer jobs") for your Office 365 Sites</span></span> #

### <a name="summary"></a><span data-ttu-id="fe9ef-103">Summary</span><span class="sxs-lookup"><span data-stu-id="fe9ef-103">Summary</span></span> ###
<span data-ttu-id="fe9ef-104">In diesem Beitrag werde ich über wie ein Azure WebJob als ein geplanter Auftrag für Ihre Office 365 verwenden erstellt werden kann (oder Prem, sollten Sie gern) SharePoint-Installation.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-104">In this post I’ll talk about how you can build an Azure WebJob to act as a scheduled job for your Office 365 (or on-prem, should you like) SharePoint installation.</span></span> <span data-ttu-id="fe9ef-105">Mit Office 365 ausführen, wenn Sie und im SharePoint Online-Dienst nutzen, Sie die erneut weiterführen müssen Sie die Aktionen, die verwendet, um *Zeitgeberaufträge* in Ihrer herkömmlichen farmlösungen werden.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-105">With Office 365, if you’re running and utilizing the SharePoint Online service, you’ll need to re-think the way you run the things that used to be *timer jobs* in your traditional Farm-solutions.</span></span> <span data-ttu-id="fe9ef-106">Führen Sie entlang, während wir die grundlegenden Konzepte von Erste Schritte mit der Erstellung von benutzerdefinierten Aufträge für Office 365-Websites durchlaufen.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-106">Follow along while we walk through the basic concepts of getting started with building custom jobs for Office 365 sites.</span></span>

# <a name="introduction-to-azure-webjob-as-a-timer-job-for-your-office-365-sites"></a><span data-ttu-id="fe9ef-107">Einführung in Azure WebJob als einen Zeitgeberauftrag für die Office 365-Websites</span><span class="sxs-lookup"><span data-stu-id="fe9ef-107">Introduction to Azure WebJob as a Timer Job for your Office 365 sites</span></span> #
<span data-ttu-id="fe9ef-108">In herkömmlichen SharePoint-Entwicklung haben wir [Zeitgeberaufträge](http://tz.nu/1DNtqH8), die in der SharePoint-Farmen geplante Aufgaben ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-108">In traditional SharePoint development we have [Timer Jobs](http://tz.nu/1DNtqH8), which performs scheduled tasks in your SharePoint farms.</span></span> <span data-ttu-id="fe9ef-109">Eine häufig verwendete Methode ist zum Entwickeln von benutzerdefinierten Zeitgeberaufträge, um kontinuierlich oder iterativ in Ihrer Umgebung bestimmte Aufgaben ausführen.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-109">A commonly used technique is to develop custom timer jobs in order to continuously or iteratively perform certain tasks in your environment.</span></span>

<span data-ttu-id="fe9ef-110">Mit Office 365 und SharePoint Online müssen Sie nicht entscheidender Vorteil, Bereitstellen von farmlösungen ist, auf dem die herkömmlichen Zeitgeberaufträge normalerweise live.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-110">With Office 365 and SharePoint Online, you don’t have the luxury to deploy your farm solutions, which is where your traditional timer jobs normally live.</span></span> <span data-ttu-id="fe9ef-111">Stattdessen wir haben, erhalten eine andere Möglichkeit zum Planen von unseren Tasks – Dies führt zu dem Konzept einer [Azure WebJob](http://tz.nu/1ueFvMZ).</span><span class="sxs-lookup"><span data-stu-id="fe9ef-111">Instead, we have to find another way to schedule our tasks – this brings us to the concept of an [Azure WebJob](http://tz.nu/1ueFvMZ).</span></span>

## <a name="steps-for-building-the-webjob-using-visual-studio-2015-preview"></a><span data-ttu-id="fe9ef-112">Schritte zum Erstellen von der WebJob mithilfe von Visual Studio 2015 (Preview)</span><span class="sxs-lookup"><span data-stu-id="fe9ef-112">Steps for building the WebJob using Visual Studio 2015 (Preview)</span></span>  ##
<span data-ttu-id="fe9ef-113">Um eine neue WebJob von Grund auf zu erstellen, müssen wir, nur erstellen eine neue Konsolenanwendung, und stellen Sie sicher, dass wir die erforderlichen Assemblys zum Projekt hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-113">In order to build a new WebJob from scratch, all we need to do is create a new console application and make sure we add the required assemblies to the project.</span></span> <span data-ttu-id="fe9ef-114">In diesem Beispiel wird [Visual Studio 2015 (Preview)](http://tz.nu/1CagngX)verwendet, wie der Name schon sagt derzeit eine Beta-Version ist.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-114">In this sample I’ll use [Visual Studio 2015 (preview)](http://tz.nu/1CagngX), which as its name implies is currently in a beta release.</span></span>

### <a name="step-1-create-your-console-application"></a><span data-ttu-id="fe9ef-115">Schritt 1: Erstellen der Konsolenanwendung</span><span class="sxs-lookup"><span data-stu-id="fe9ef-115">Step 1: Create your console application</span></span> ###
<span data-ttu-id="fe9ef-116">Starten Sie, indem Sie ein neues Projekt erstellen, und stellen Sie sicher, dass Sie die Vorlage "**Console Application**" ausgewählt haben.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-116">Start by creating a new project and make sure you’ve selected the "**Console Application**" template.</span></span> <span data-ttu-id="fe9ef-117">Darüber hinaus und dies ist wichtig, stellen Sie sicher, dass Sie **.NET Framework 4.5**gewählten!</span><span class="sxs-lookup"><span data-stu-id="fe9ef-117">Also, and this is important, make sure you've chosen **.NET Framework 4.5**!</span></span>

![Das Dialogfeld Neues Projekt, so erstellen Sie eine Konsolenanwendung, die mit den Punkt festgelegt net Framework 4.5](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/1.Create-Console-Application.png)

### <a name="step-2-add-the-sharepoint-specific-assemblies-from-nuget"></a><span data-ttu-id="fe9ef-119">Schritt 2: Hinzufügen der SharePoint-spezifische Assemblys aus NuGet</span><span class="sxs-lookup"><span data-stu-id="fe9ef-119">Step 2: Add the SharePoint-specific assemblies from NuGet</span></span> ###
<span data-ttu-id="fe9ef-120">Wenn Sie Visual Studio 2015 wie ich mache verwenden, sieht das NuGet-Paket-Manager-Dialogfeld geringfügig von früheren Versionen von Visual Studio, aber das Konzept des identisch.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-120">If you’re using Visual Studio 2015 as I’m doing, the NuGet package manager dialog will look slightly different from earlier versions of Visual Studio, but the concept’s the same.</span></span>

 - <span data-ttu-id="fe9ef-121">Wechseln Sie zu**"Extras**"->"**NuGet-Paket-Manager**-">"**Verwalten von NuGet-Pakete für Lösung..."**</span><span class="sxs-lookup"><span data-stu-id="fe9ef-121">Go to "**Tools**" -> "**NuGet Package Manager**" -> "**Manage NuGet Packages for Solution…**"</span></span>
 - <span data-ttu-id="fe9ef-122">Suchen Sie nach "**App für SharePoint**"</span><span class="sxs-lookup"><span data-stu-id="fe9ef-122">Search for "**App for SharePoint**"</span></span>
 - <span data-ttu-id="fe9ef-123">Installieren Sie das Paket "**AppForSharePointWebToolkit**" dem installieren die erforderlichen Hilfsklassen für die Arbeit mit dem SharePoint-Clientobjektmodells aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-123">Install the package called "**AppForSharePointWebToolkit**" which will install the required helper classes for working with the SharePoint Client Object Model.</span></span>

<span data-ttu-id="fe9ef-124">![Die NuGet Package Manager-Dialogfeld mit den Suchbegriff App für SharePoint.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-124">![The NuGet Package Manager dialog showing the search term, App for SharePoint.</span></span> <span data-ttu-id="fe9ef-125">App für SharePoint Web Toolkit wird hervorgehoben, und die Schaltfläche "installieren" geklickt werden kann.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/2.Add-App-For-SharePoint-Web-Toolkit-from-Nuget.png)</span><span class="sxs-lookup"><span data-stu-id="fe9ef-125">App For SharePoint Web Toolkit is highlighted and the Install button is ready to be clicked.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/2.Add-App-For-SharePoint-Web-Toolkit-from-Nuget.png)</span></span>
<span data-ttu-id="fe9ef-126">Stellen Sie sicher, dass das NuGet-Paket erfolgreich war, indem Sie sicherstellen, dass diese beiden neuen Klassen in Ihrer Konsolenanwendungsprojekt vorhanden ist: ![der Projektmappen-Explorer zeigt die neu hinzugefügten Klassen Share Point Kontext und Hilfsprogramm-Token.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/3.Project-Overview-With-Added-Files.png)</span><span class="sxs-lookup"><span data-stu-id="fe9ef-126">Make sure the NuGet package worked by making sure there’s these two new classes in your console application project: ![The Solution Explorer shows the newly added classes, Share Point Context and Token Helper.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/3.Project-Overview-With-Added-Files.png)</span></span>

### <a name="step-3-add-the-required-code-to-execute-the-job-on-your-office-365-site"></a><span data-ttu-id="fe9ef-127">Schritt 3: Hinzufügen des erforderlichen Codes zum Ausführen des Auftrags auf Ihrer Office 365-Website</span><span class="sxs-lookup"><span data-stu-id="fe9ef-127">Step 3: Add the required code to execute the job on your Office 365 site</span></span> ###
<span data-ttu-id="fe9ef-128">An dieser Stelle haben wir unsere Konsolenanwendung erstellt, und wir haben die erforderlichen Assemblys, die für uns zur Kommunikation mit SharePoint vereinfachen werden hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-128">At this point we’ve created our Console Application and we’ve added the required assemblies that will make it easy for us to communicate with SharePoint.</span></span> <span data-ttu-id="fe9ef-129">Nächste Schritte stellen sind der Hilfsklassen, um das Ausführen von Befehlen im unseren SharePoint-Umgebung über unsere Console Application verwenden.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-129">Next steps are to make use of these helper classes in order to execute commands in our SharePoint environment through our Console Application.</span></span> <span data-ttu-id="fe9ef-130">Markieren Sie entlang.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-130">Tag along.</span></span>

<span data-ttu-id="fe9ef-131">***Hinweis:*** In diesem Beispiel nach Abschluss des Vorgangs ich werde verwenden ein Konto + Kennwort Ansatz (wie ein Dienstkonto).</span><span class="sxs-lookup"><span data-stu-id="fe9ef-131">***Note:*** In the finished sample I’ll be using an account+password approach (like a service account).</span></span> <span data-ttu-id="fe9ef-132">Authentifizierung erläutert Optionen weiter unten im Artikel und Links zu anderen alternativen Auschecken.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-132">We’ll discuss authentication options further down in the article and check out links to other alternatives.</span></span>

#### <a name="wire-up-the-calls-to-the-sharepoint-online-site-collection"></a><span data-ttu-id="fe9ef-133">Definieren der Anrufe für die SharePoint Online-Websitesammlung</span><span class="sxs-lookup"><span data-stu-id="fe9ef-133">Wire up the calls to the SharePoint Online site collection</span></span> ####

<span data-ttu-id="fe9ef-134">Der folgende Code veranschaulicht den Anruf an Ihre Website leicht verbinden kann, nun, da wir die Hilfsklassen aus unseren NuGet-Paket hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-134">The following code demonstrates how to wire up the call to your site quite easily now that we’ve added the helper classes from our NuGet package.</span></span>

```C#
 static void Main(string[] args)
  {
      using (ClientContext context = new ClientContext("https://redacted.sharepoint.com"))
      {
          // Use default authentication mode
          context.AuthenticationMode = ClientAuthenticationMode.Default;
          // Specify the credentials for the account that will execute the request
          context.Credentials = new SharePointOnlineCredentials(GetSPOAccountName(), GetSPOSecureStringPassword());

          // TODO: Add your logic here!
      }
  }
 
 
  private static SecureString GetSPOSecureStringPassword()
  {
      try
      {
          Console.WriteLine(" --> Entered GetSPOSecureStringPassword()");
          var secureString = new SecureString();
          foreach (char c in ConfigurationManager.AppSettings["SPOPassword"])
          {
              secureString.AppendChar(c);
          }
          Console.WriteLine(" --> Constructed the secure password");
 
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
          Console.WriteLine(" --> Entered GetSPOAccountName()");
          return ConfigurationManager.AppSettings["SPOAccount"];
      }
      catch
      {
          throw;
      }
   }
``` 

<span data-ttu-id="fe9ef-135">In der beispielanwendung finden Sie, dass ich zwei Hilfsmethoden für das Abrufen von den Kontonamen und das Kennwort des Kontos aus der App.config.Datei hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-135">You can see in my sample application that I’ve added two helper methods for fetching the Account Name and Account Password from the app.config file.</span></span> <span data-ttu-id="fe9ef-136">Diese werden im Abschnitt Authentifizierung erläutert weiter unten in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-136">These are explained in the authentication-section further down in this article.</span></span>

<span data-ttu-id="fe9ef-137">Wie bei der main-Methode ist, müssen wir nur Dinge bis zu unserem Portal verbinden.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-137">As for the main method, that’s all we need to wire things up to our portal.</span></span> <span data-ttu-id="fe9ef-138">Bevor wir tiefer wie wir SharePoint in unseren Code bearbeiten können untersuchen, Erläuterung der Optionen für die Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-138">Before we dig deeper into how we can manipulate SharePoint from our code, let’s discuss options for authentication.</span></span>

## <a name="authentication-considerations"></a><span data-ttu-id="fe9ef-139">Überlegungen zur Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="fe9ef-139">Authentication considerations</span></span> ##
<span data-ttu-id="fe9ef-140">Wir sehen Sie sich zwei Optionen für die Authentifizierung und finden Sie, wie sie sich unterscheiden.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-140">We’ll check out two options for authentication and see how they differ.</span></span> <span data-ttu-id="fe9ef-141">Weitere Optionen für die Authentifizierung in der Zukunft möglicherweise, aber hier sind zwei Ansätze häufig verwendete.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-141">There may be other options for authentication down the road, but here are two commonly used approaches.</span></span>

### <a name="option-1-use-a-service-account-username--password"></a><span data-ttu-id="fe9ef-142">Option 1: Verwenden eines Dienstkontos (Username + Kennwort)</span><span class="sxs-lookup"><span data-stu-id="fe9ef-142">Option 1: Use a Service Account (Username + Password)</span></span> ###
<span data-ttu-id="fe9ef-143">Dieser Ansatz ist relativ einfach und ermöglicht es Ihnen, geben Sie einfach ein Konto und Kennwort Ihrem Office 365-Mandanten und verwenden Sie beispielsweise CSOM zum Ausführen von Code für Ihre Websites.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-143">This approach is pretty straight forward and enables you to simply enter an account and password to your Office 365 tenant and then use for example CSOM to execute code on your sites.</span></span> <span data-ttu-id="fe9ef-144">Dies ist, was Sie auch in meinem Beispielcode oben angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-144">This is what you see in my sample code above as well.</span></span>

#### <a name="create-a-new-service-account-in-office-365"></a><span data-ttu-id="fe9ef-145">Erstellen eines neuen Dienstkontos in Office 365</span><span class="sxs-lookup"><span data-stu-id="fe9ef-145">Create a new Service Account in Office 365</span></span> ####
<span data-ttu-id="fe9ef-146">In der Reihenfolge zu diesem Zweck sollte ein bestimmtes Konto erstellt werden, die fungiert als Dienstkonto – entweder für dieses bestimmte Anwendung oder eine generische dienstanwendungskonto, die alle Aufträge und Dienste verwenden können.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-146">In order for this to work a specific account should be created that acts as a service account – either for this specific application or a generic service application account that all your jobs and services can use.</span></span>

<span data-ttu-id="fe9ef-147">Aus Gründen der in dieser Demo habe ich ein neues Konto namens "**SP WebJob**" erstellt: ![das Dashboard zeigt das neu erstellte SP WebJob Konto.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/4.Service-Account-Overview.png)</span><span class="sxs-lookup"><span data-stu-id="fe9ef-147">For the sake of this demo, I’ve created a new account called "**SP WebJob**": ![The dashboard shows the newly created SP WebJob account.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/4.Service-Account-Overview.png)</span></span>

<span data-ttu-id="fe9ef-148">Je nach den Auftrag auf welche Berechtigungen sollten haben, müssen Sie die Berechtigungen des Benutzerkontos bearbeiten, beim Einrichten von.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-148">Depending on what permissions the job should have, you will have to edit the permissions of the account when you set it up.</span></span>

#### <a name="store-credentials-in-your-appconfig"></a><span data-ttu-id="fe9ef-149">Speichern von Anmeldeinformationen in der Datei app.config</span><span class="sxs-lookup"><span data-stu-id="fe9ef-149">Store credentials in your app.config</span></span> ####
<span data-ttu-id="fe9ef-150">Innerhalb des Projekts ' App.config ' Datei können Sie die Anmeldeinformationen angeben, damit sie auf einfache Weise fetchable aus dem ausführbaren Code sind.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-150">Within your project’s app.config file you can specify the credentials so they’re easily fetchable from the code executable.</span></span> <span data-ttu-id="fe9ef-151">Dies ist mein app.config aussieht:</span><span class="sxs-lookup"><span data-stu-id="fe9ef-151">This is what my app.config looks like:</span></span>
```XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
 <startup> 
   <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
 </startup>
 <appSettings>
   <add key="SPOAccount" value="spwebjob@redacted.onmicrosoft.com"/>
   <add key="SPOPassword" value="redacted"/>
 </appSettings>
</configuration>

```
<span data-ttu-id="fe9ef-152">Sie können die zwei Einstellungen in App.config finden Sie unter:</span><span class="sxs-lookup"><span data-stu-id="fe9ef-152">You can see the two settings in the App.config:</span></span>

 - <span data-ttu-id="fe9ef-153">SPOAccount</span><span class="sxs-lookup"><span data-stu-id="fe9ef-153">SPOAccount</span></span>
 - <span data-ttu-id="fe9ef-154">SPOPassword</span><span class="sxs-lookup"><span data-stu-id="fe9ef-154">SPOPassword</span></span>

<span data-ttu-id="fe9ef-155">Wenn Sie den ersten Codeausschnitt überprüfen, erhalte ich diese Einstellungen aus der App.config.Datei abgerufen.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-155">If you review the first code snippet, I’m fetching these settings from the app.config file.</span></span> <span data-ttu-id="fe9ef-156">Beachten Sie, dass das Speichern von den Kontonamen und das Kennwort in Klartext in der Datei app.config bedeutet halten. Sie müssen Treffen einer Entscheidung in eigene Projekte dafür, wie und wo Sie gespeichert und schützen Sie Ihre Kennwörter sollten Sie diesen Ansatz wählen.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-156">Just keep in mind that this means storing the account name and password in clear text in your app.config. You need to make a decision in your own projects for how and where to store and protect your passwords, should you choose this approach.</span></span>

#### <a name="the-job-runs-under-the-specified-account"></a><span data-ttu-id="fe9ef-157">Der Auftrag wird unter dem angegebenen Konto ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-157">The job runs under the specified account</span></span> ####
<span data-ttu-id="fe9ef-158">Sobald die Anwendung ausgeführt wird, sehen Sie, dass er ausgeführt wird, mit dem Konto im Konstruktor SharePointOnlineCredentials() angegeben:</span><span class="sxs-lookup"><span data-stu-id="fe9ef-158">Once the application runs, you will see that it runs using the account specified in the SharePointOnlineCredentials() constructor:</span></span>

![Automatische Konvertierung Protokoll zeigt vier Text Übersetzungen SP WebJob zugeordnet.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/5.Running-Job-Overview.png)

<span data-ttu-id="fe9ef-160">In diesem Beispiel oben bin ich eine WebJob angezeigt, die auf eine benutzerdefinierte Liste in einem der "Meine Websites" in meiner SharePoint Online-Websitesammlung gehostet Aktionen ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-160">In my sample above I’m showing a WebJob that is executing actions on a custom list in one of my sites hosted in my SharePoint Online site collection.</span></span>

<span data-ttu-id="fe9ef-161">Aus diesem Grund erhalten wir einen guten zurückverfolgt werden Änderungen können im Portal unsere Dienstkonto ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-161">Because of this, we can get a pretty good traceability of changes in the portal performed by our service account.</span></span> <span data-ttu-id="fe9ef-162">Hierbei handelt es sich deshalb Achten Sie darauf, nennen Sie das Konto mit Bedacht – jeder kennt, dass die Änderungen automatisch von unseren Dienst durchgeführt wurden, indem Sie einfach auf die Metadaten geändert/erstellt.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-162">This is why its important to name the account wisely – everyone will know that the modifications were done automatically by our service simply by looking at the modified/created metadata.</span></span>

### <a name="option-2-use-oauth-and-include-authentication-tokens-in-your-requests-to-avoid-specifying-accountpassword"></a><span data-ttu-id="fe9ef-163">Option 2: Verwendung OAuth und enthalten Authentifizierungstoken in Ihre Anforderungen zu vermeiden, Konto und Kennwort angeben</span><span class="sxs-lookup"><span data-stu-id="fe9ef-163">Option 2: Use OAuth and include authentication tokens in your requests to avoid specifying account/password</span></span> ###
<span data-ttu-id="fe9ef-164">Dies wurde durch schätze [Kirk Evans](http://blogs.msdn.com/b/kaevans/) bei Microsoft ausführlich erläutert.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-164">This has been explained in great detail by my friend [Kirk Evans](http://blogs.msdn.com/b/kaevans/) at Microsoft.</span></span>

<span data-ttu-id="fe9ef-165">In seinem buchen gewählte "[Erstellen eines SharePoint-Add-Ins als einen Zeitgeberauftrag](http://tz.nu/1xBA76K)" erläutert er das können Sie nutzen und Durchlauf entlang des Zugriffs für das Token, um zu vermeiden und Kennwort Setupprogrammen wie bereits erwähnt, falls Sie nicht die Kennwörter speichern möchten und Anmeldeinformationen in die Anwendung.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-165">In his post called "[Building a SharePoint Add-in as a Timer Job](http://tz.nu/1xBA76K)" he explains how you can utilize and pass along the access tokens in order to avoid username/password setups like I explained above, in case you don't want to store the passwords and credentials in your application.</span></span>

## <a name="extending-the-code-with-some-csom-magic"></a><span data-ttu-id="fe9ef-166">Erweitern Sie den Code mit einigen magischen CSOM</span><span class="sxs-lookup"><span data-stu-id="fe9ef-166">Extending the code with some CSOM magic</span></span> ##
<span data-ttu-id="fe9ef-167">An dieser Stelle haben wir eine funktionsfähige Console Application authentifizieren und Anforderungen an den Office 365-Websites ausführen kann.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-167">At this point we have a working Console Application which can authenticate and execute requests to your Office 365 sites.</span></span> <span data-ttu-id="fe9ef-168">Nicht besonders interessant ausgeführt wurde im Code noch, sodass hier ist ein Beispiel-Ausschnitt, Abrufen von Informationen aus einer Liste bezeichnet "Automatische Übersetzungen", die ich erstellt haben, und die Codelogik wird angezeigt, wenn alle Elemente in der Liste, die übersetzt wurde noch nicht vorhanden ist und dann Es werden führen Sie einen Anruf an einen Übersetzungsdienst und den Text, der die gewünschte Ausgabe Sprache übersetzen.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-168">Nothing fancy has been done in the code yet, so here’s a sample snippet for pulling out some information from a list called "Automatic Translations" that I have created, and the code logic will see if there’s any items in the list that haven’t been translated and then it’ll execute a call to a translation-service and translate the text to the desired output language.</span></span>
```C#
static void Main(string[] args)
{
   try
   {
      Console.WriteLine("Initiating Main()");

      using (ClientContext context = new ClientContext("https://redacted.sharepoint.com"))
      {
         Console.WriteLine("New ClientContext('https://redacted.sharepoint.com') opened. ");

         context.AuthenticationMode = ClientAuthenticationMode.Default;
         context.Credentials = new SharePointOnlineCredentials(GetSPOAccountName(), GetSPOSecureStringPassword());

         Console.WriteLine("Authentication Mode and Credentials configured");

         List translationlist = context.Web.Lists.GetByTitle("Automatic Translations");
         context.Load(translationlist);
         context.ExecuteQuery();

         Console.WriteLine("TranslationList fetched, loaded and ExecuteQuery'ed");

         if (translationlist != null && translationlist.ItemCount > 0)
         {
             Console.WriteLine("The list exist, let's do some magic");

             CamlQuery camlQuery = new CamlQuery();
             camlQuery.ViewXml =
             @"<View>  
             <Query> 
                 <Where><Eq><FieldRef Name='IsTranslated' /><Value Type='Boolean'>0</Value></Eq></Where> 
             </Query> 
         </View>";

             ListItemCollection listItems = translationlist.GetItems(camlQuery);
             context.Load(listItems);
             context.ExecuteQuery();

             Console.WriteLine("Query for listItems executed.");

             foreach (ListItem item in listItems)
             {
                 item["Output"] = TranslatorHelper.GetTranslation(item["Title"], item["Target Language"], item["Original Language"]);
                 item["IsTranslated"] = true;
                 item.Update();
             }


             context.ExecuteQuery();
             Console.WriteLine("Updated all the list items we found. Carry on...");
         }
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

```
<span data-ttu-id="fe9ef-169">Die **TranslatorHelper** -Klasse ist eine Hilfsklasse, die eine benutzerdefinierte Übersetzung API ruft aber es nicht erläutert ausführlich in diesem Beitrag, da es sehr weit außerhalb des Bereichs ist.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-169">The **TranslatorHelper** class is a helper class which calls a custom translation API but it will not be discussed in detail in this post since it's pretty far outside of the scope.</span></span>

<span data-ttu-id="fe9ef-170">**Hinweis:** *Ressourcenverfügbarkeitsdaten aus dem Code Dies ist eine Demo definitiv nicht für die Verwendung in der Produktion, überprüfen sie und passen Sie entsprechend Ihrer codieren Standards und Sicherheitsprinzipien. Jedoch alle Console.WriteLine Ergänzungen für uns, überprüfen Sie die Ausführung der Aufträge auf einfache Weise über das Portal Azure hinzugefügt werden. Klicken Sie auf Protokollierung und Überwachung weiteren unten in diesem Artikel weitere.*</span><span class="sxs-lookup"><span data-stu-id="fe9ef-170">**Note:** *As seen from the code this is a demo and definitely not for production use, please revise it and adjust according to your coding standards and security principles. However all the Console.WriteLine additions are added in order for us to review the execution of the jobs easily from the Azure Portal. More on logging and monitoring further down in this article.*</span></span>

## <a name="publishing-your-webjob-to-azure"></a><span data-ttu-id="fe9ef-171">Veröffentlichen Sie Ihre WebJob in Azure</span><span class="sxs-lookup"><span data-stu-id="fe9ef-171">Publishing your WebJob to Azure</span></span> ##
<span data-ttu-id="fe9ef-172">Wenn Sie Ihre WebJob entwickelt haben, und Sie können sie auf der Azure-Umgebung bereitstellen (an eine Azure-WebSite bereitgestellt), können Sie zwei grundlegende Optionen wie unten beschrieben.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-172">When you’ve developed your WebJob and you’re ready to deploy it to your Azure environment (deploys to an Azure WebSite), you have two main options as described below.</span></span>

### <a name="option-1-upload-a-zip-file-with-the-webjob-binaries-to-your-azure-portal"></a><span data-ttu-id="fe9ef-173">Option 1: Hochladen einer Zip-Datei mit den WebJob Binärdateien in der Azure-Verwaltungsportal</span><span class="sxs-lookup"><span data-stu-id="fe9ef-173">Option 1: Upload a zip file with the WebJob binaries to your Azure Portal</span></span> ###
<span data-ttu-id="fe9ef-174">Verwenden der Azure-Verwaltungsportal, in dem Sie alle Ihre Awesomeness in Azure aufbewahren, können Sie eine Zip-Datei, enthält die Ausgabe aus Visual Studio Build hochladen.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-174">Using the Azure Portal where you keep all of your awesomeness in Azure, you can upload a zip-file containing the output from Visual Studio’s build.</span></span> <span data-ttu-id="fe9ef-175">Dies ist eine einfache Möglichkeit zum Kompilieren und Versand von Ihrem Code an eine andere Person, die die Bereitstellung für Sie ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-175">This is an easy way for compiling and shipping your code to someone else who will do the deployment for you.</span></span>

#### <a name="create-the-zip-file"></a><span data-ttu-id="fe9ef-176">Erstellen Sie die Zipdatei</span><span class="sxs-lookup"><span data-stu-id="fe9ef-176">Create the zip file</span></span> ####
<span data-ttu-id="fe9ef-177">Einfach abgerufen Sie werden, der die Ausgabedateien aus Ihrem Visual Studio (normalerweise im Ordner Bin/Debug oder Bin-Version) zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="fe9ef-177">Simply grab all the output files from your Visual Studio build (normally in your bin/Debug or bin/Release folder):</span></span>

<span data-ttu-id="fe9ef-178">![Eine Windows Explorer-Ansicht Bin/Debug-Ordner wird angezeigt.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/6.Zip-File-Overview.png)</span><span class="sxs-lookup"><span data-stu-id="fe9ef-178">![A Windows Explorer view of the bin/Debug folder is displayed.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/6.Zip-File-Overview.png)</span></span>
<span data-ttu-id="fe9ef-179">Komprimieren Sie, damit eine gute Zip-Datei für Ihre Arbeit Web Sie erzielen:</span><span class="sxs-lookup"><span data-stu-id="fe9ef-179">Compress them so you’ll get a nice Zip file for your web job:</span></span>

![Windows Explorer-Ansicht einer abgeschlossenen ZIP-Datei wird angezeigt.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/7.Zip-File-Created.png)

#### <a name="find-a-web-site-where-the-job-should-be-deployed"></a><span data-ttu-id="fe9ef-181">Suchen nach einer Website, in dem der Auftrag bereitgestellt werden</span><span class="sxs-lookup"><span data-stu-id="fe9ef-181">Find a web site where the job should be deployed</span></span> ####

<span data-ttu-id="fe9ef-182">Gut, damit Sie Ihr Paket haben.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-182">Okay, so you’ve got your package.</span></span> <span data-ttu-id="fe9ef-183">Das ist einfach.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-183">That’s easy enough.</span></span> <span data-ttu-id="fe9ef-184">Nächste Schritt besteht darin, gleich https://portal.azure.com und melden Sie sich Ihre Windows Azure-Verwaltungsportal.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-184">Next step is to head on to https://portal.azure.com and login to your Windows Azure Portal.</span></span> <span data-ttu-id="fe9ef-185">Sie müssen entweder eine neue Website erstellen, oder verwenden Sie eine vorhandene – dieser Website werden den Host für unsere Webauftrag, von dort aus.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-185">From there you’ll need to either create a new web site, or use an existing one – this website will be the host for our web job.</span></span>

<span data-ttu-id="fe9ef-186">In unserem Fall habe ich bereits eine Azure-WebSite für einige der Demos für meine Office 365 damit ich, dass eine gerade verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-186">In my case, I already have an Azure WebSite for some of my Office 365 demos so I’ll just use that one.</span></span>

<span data-ttu-id="fe9ef-187">Wenn Sie unten im Einstellungsbereich für Ihre Website navigieren, finden Sie eine etwas "**WebJobs**" unter der Kopfzeile "**Vorgänge**" aufgerufen:</span><span class="sxs-lookup"><span data-stu-id="fe9ef-187">If you scroll down in the settings pane for your website, you’ll find a something called "**WebJobs**" under the "**Operations**" header:</span></span>

<span data-ttu-id="fe9ef-188">![Des Autors Azure-Verwaltungsportal wird angezeigt, mit einem Pfeil auf WebJobs zeigen. ](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/8.Find-WebJobs-in-Azure-Portal.png)
 **Klicken, auf dem der Pfeil zeigt!**</span><span class="sxs-lookup"><span data-stu-id="fe9ef-188">![The author's Azure Portal is displayed, with an arrow pointing to WebJobs.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/8.Find-WebJobs-in-Azure-Portal.png)
**Click where the arrow points!**</span></span>

#### <a name="upload-your-webjob"></a><span data-ttu-id="fe9ef-189">Hochladen der WebJob</span><span class="sxs-lookup"><span data-stu-id="fe9ef-189">Upload your WebJob</span></span> ####

<span data-ttu-id="fe9ef-190">Hochladen der Webauftrag durch Klicken auf das Zeichen **[+ hinzufügen]** :</span><span class="sxs-lookup"><span data-stu-id="fe9ef-190">Upload your web job by clicking the **[+ Add]** sign:</span></span>

![Die WebJobs Azure-Verwaltungsportal wird angezeigt, mit einem Pfeil auf Hinzufügen.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/9.Upload-Azure-WebJob-from-Azure-Portal.png)

<span data-ttu-id="fe9ef-192">Wählen Sie einen Namen, wie der Auftrag ausgeführt werden soll und die tatsächlichen Zip-Datei:</span><span class="sxs-lookup"><span data-stu-id="fe9ef-192">Choose a Name, how the job should run and the actual zip file:</span></span>

![Das Dialogfeld WebJob hinzufügen wird angezeigt.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/10.Configure-Name-of-Uploaded-WebJob.png)

<span data-ttu-id="fe9ef-195">***Wichtig:*** Die Alternative "Wie zur Ausführung" nur bietet "On Demand" oder "Fortlaufend" zu diesem Zeitpunkt, aber bald vorhanden sein Support für "Geplant" sowie – das ist wirklich möchten.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-195">***Important:*** The "How To Run" alternative only offers "On Demand" or "Continuous" at this point, but soon there will be support for "Scheduled" as well – which is what we really want.</span></span>

<span data-ttu-id="fe9ef-196">*(Hinweis: im nächsten Abschnitt für die Veröffentlichung direkt von Azure, Planen Sie es aus in VS).*</span><span class="sxs-lookup"><span data-stu-id="fe9ef-196">*(Hint: In the next section for publishing directly from Azure, you can schedule it from inside VS).*</span></span>

<span data-ttu-id="fe9ef-197">Okay, können geschieht – Sie nun Ihre Webjob aus der Azure-Verwaltungsportal ausführen:</span><span class="sxs-lookup"><span data-stu-id="fe9ef-197">Okay, done – you can now run your webjob from your Azure Portal:</span></span>

![Die WebJobs Azure-Verwaltungsportal wird mit der neuen Liste angezeigt.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/11.Run-WebJob-from-Azure-Portal.png)

<span data-ttu-id="fe9ef-200">Dies ist zwar schön und Sicherheitsdeskriptor, da das Portal verfügt nicht über die Dialogfelder für die Unterstützung der Planung noch – ich würden Sie Informationen zum Veröffentlichen von auszuchecken intensiv über in Visual Studio 2015 stattdessen (oder 2013, wenn das Ihrer Wahl ist).</span><span class="sxs-lookup"><span data-stu-id="fe9ef-200">While this is all fine and dandy, since the portal doesn’t have the dialogs for supporting scheduling just yet – I would urge you to check out how to publish from inside Visual Studio 2015 instead (or 2013, if that’s your choice).</span></span>

### <a name="option-2-publish-directly-to-azure-from-visual-studio"></a><span data-ttu-id="fe9ef-201">Option 2: Veröffentlichen Sie direkt in Azure von Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fe9ef-201">Option 2: Publish directly to Azure from Visual Studio</span></span> ###
<span data-ttu-id="fe9ef-202">Dies ist meine bevorzugten zu diesem Zeitpunkt, da ich die Tools in Visual Studio verwenden können, um alle Änderungen direkt mit einem gehosteten Dienst schnell veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-202">This is my favorite one at this point because I can use the tooling in Visual Studio to quickly publish any changes directly to my hosted service.</span></span> <span data-ttu-id="fe9ef-203">Ein weiterer Vorteil werden deaktivieren bald, wie Sie auch den Auftrag planen können, genau wie Sie direkt in den Dialogfeldern in Visual Studio ausführen soll.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-203">The other benefit will become clear soon, as you can also schedule the job exactly how you want it to execute directly from the dialogs in Visual Studio.</span></span>

#### <a name="choose-to-publish-the-webjob-from-visual-studio-2015"></a><span data-ttu-id="fe9ef-204">Wählen Sie die WebJob von Visual Studio 2015 veröffentlichen</span><span class="sxs-lookup"><span data-stu-id="fe9ef-204">Choose to publish the WebJob from Visual Studio 2015</span></span> ####

<span data-ttu-id="fe9ef-205">***Hinweis:*** *Diese Dialogfelder abweichen etwas, wenn Sie eine frühere Version von Visual Studio ausführen. Darüber hinaus habe ich bereits angemeldet, wenn Sie dies zum ersten Mal tun ein Anmeldedialogfeld abrufen kann, um Azure-Konto anmelden. Dies ist eine Voraussetzung.*</span><span class="sxs-lookup"><span data-stu-id="fe9ef-205">***Note:*** *These dialogs may differ slightly if you’re running an earlier version of Visual Studio. Also, I am already logged in so if you’re doing this for the first time you may get a login-dialog in order to sign in to your Azure account. That’s a pre-requisite.*</span></span>

<span data-ttu-id="fe9ef-206">Klicken Sie einfach mit der rechten Maustaste in des Projekts, und wählen Sie "**Veröffentlichen als einem Azure WebJob...**":</span><span class="sxs-lookup"><span data-stu-id="fe9ef-206">Simply right-click your project and select "**Publish as an Azure WebJob…**":</span></span>

![Im Kontextmenü Projektmappen-Explorer wird angezeigt, mit der veröffentlichen als Azure WebJob Option hervorgehoben.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/12.Publish-WebJob-from-Visual-Studio-2015.png)

#### <a name="add-azure-webjob"></a><span data-ttu-id="fe9ef-208">Hinzufügen von Azure WebJob</span><span class="sxs-lookup"><span data-stu-id="fe9ef-208">Add Azure WebJob</span></span> ####
<span data-ttu-id="fe9ef-209">Dadurch gelangen Sie zu einer neuen Dialogfeld, in denen können Sie den Auftrag konfigurieren, und da wir ein wiederkehrendes Projekt soll, die nach einem Zeitplan (in meinem Fall einmal für jeden Abend) ausgeführt wird, können Sie den Zeitplan direkt in den Dialogfeldern konfigurieren: ![das Hinzufügen von Azure WebJob Dialogfeld Benachrichtigung wird ayed.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-209">This will bring you to a new dialog where you can configure the job, and since we want a recurring job that should be executed on a schedule (in my case once every night) you can configure the schedule directly from the dialogs: ![The Add Azure WebJob dialog is displayed.</span></span> <span data-ttu-id="fe9ef-210">Das Namensfeld WebJob enthält den Text Zimmergren-O365-WebJobSample, Feld Modus ausführen WebJob enthält die Option nach einem Zeitplan ausführen, serienfelds enthält den Option periodisch Auftrag und das Kontrollkästchen kein Enddatum wird überprüft, die als Serie festlegen jedes Feld auf 1 gesetzt ist Tage , und die starten Datum 9 Januari 2015 ist.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/13.Add-Azure-WebJob-Dialog.png)</span><span class="sxs-lookup"><span data-stu-id="fe9ef-210">The WebJob name field contains the text Zimmergren-O365-WebJobSample, the WebJob run mode field contains the option Run on a Schedule, the Recurrence field contains the option Recurring job and the check box No end date is checked, the Recur every field is set to 1 days, and the Starting on date is 9 Januari 2015.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/13.Add-Azure-WebJob-Dialog.png)</span></span>

 - <span data-ttu-id="fe9ef-211">Stellen Sie sicher, dass der Name angezeigten Web ist</span><span class="sxs-lookup"><span data-stu-id="fe9ef-211">Make sure the name is web friendly</span></span>
 - <span data-ttu-id="fe9ef-212">Wählen Sie Ihre Ausführmodus, ich bin "Auf einen Zeitplan", da es in einem bestimmten Zeitpunkt täglich kommen haben sollen</span><span class="sxs-lookup"><span data-stu-id="fe9ef-212">Select your run mode, I’m on "Run on a Schedule" because we want to have it occur on a specific time every day</span></span>
 - <span data-ttu-id="fe9ef-213">Der Auftrag ein wiederkehrendes Projekt oder einen einmaligen Auftrag sein sollte?</span><span class="sxs-lookup"><span data-stu-id="fe9ef-213">Should the job be a recurring job or a one-time job?</span></span> <span data-ttu-id="fe9ef-214">Da wir möchten, können Sie einen Zeitgeberauftrag das wiederholt werden, muss in meinem Fall ohne jedes Enddatum, da es immer nachts ausgeführt werden kann</span><span class="sxs-lookup"><span data-stu-id="fe9ef-214">Since we want to simulate a Timer Job it needs to be recurring, and in my case without any end date since it’ll be running every night</span></span>
 - <span data-ttu-id="fe9ef-215">Sie können die Serie nach unten zu einer Minute, planen möchten, sollten.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-215">You can schedule the recurrence down to every minute, should you want.</span></span>
 - <span data-ttu-id="fe9ef-216">Wenn starte wir?</span><span class="sxs-lookup"><span data-stu-id="fe9ef-216">When do we start?</span></span> <span data-ttu-id="fe9ef-217">:-)</span><span class="sxs-lookup"><span data-stu-id="fe9ef-217"></span></span>

<span data-ttu-id="fe9ef-218">Trefferposition **OK** und Sie sehen, dass Sie Visual Studio eine Meldung "**Installieren von WebJobs Publishing NuGet-Paket**" ablegen.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-218">Hit **OK** and you’ll see that Visual Studio will drop you a message saying "**Installing WebJobs Publishing NuGet Package**".</span></span>

#### <a name="visual-studio-added-webjobs-publishing-nuget-package"></a><span data-ttu-id="fe9ef-219">Visual Studio hinzugefügt WebJobs Publishing NuGet-Paket</span><span class="sxs-lookup"><span data-stu-id="fe9ef-219">Visual Studio added WebJobs Publishing NuGet Package</span></span> ####
![Klicken Sie im Dialogfeld WebJobs NuGet-Paket zu installieren wird angezeigt, der ein Drehfeld und der Text, Installieren von WebJobs Publishing NuGet-Paket angezeigt.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/14.WebJobs-NuGet-Package-Install.png)

<span data-ttu-id="fe9ef-221">Dadurch wird eine neue Datei mit dem Namen "**Webjob veröffentlichen settings.json**", um unseren Projekt, mit der Konfiguration für den Auftrag tatsächlich hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-221">This actually adds a new file called "**webjob-publish-settings.json**" to our project, containing the configuration for the job.</span></span>

<span data-ttu-id="fe9ef-222">Die Datei sieht folgendermaßen aus:</span><span class="sxs-lookup"><span data-stu-id="fe9ef-222">The file looks like this:</span></span>
```json
{
  "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
  "webJobName": "Zimmergren-O365-WebJobSample",
  "startTime": "2015-01-09T01:00:00+01:00",
  "endTime": null,
  "jobRecurrenceFrequency": "Day",
  "interval": 1,
  "runMode": "Scheduled"
}
```
<span data-ttu-id="fe9ef-223">Rechts, müssen wir nicht mit dieser Datei gegenwärtig Mühe, da es bereits konzipiert, die Planung in Dialogfeldern.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-223">Right, we don’t need to bother with this file at the moment since we already designed the scheduling using the dialogs.</span></span>

#### <a name="select-publishingdeployment-target"></a><span data-ttu-id="fe9ef-224">Wählen Sie Ziel Veröffentlichung-Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="fe9ef-224">Select publishing/deployment target</span></span> ####
<span data-ttu-id="fe9ef-225">Im nächste Schritt im Dialogfeld werden, wo Sie veröffentlichen/Bereitstellen Ihrer WebJob.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-225">The next step in the dialog will be where to publish/deploy your WebJob.</span></span> <span data-ttu-id="fe9ef-226">Sie können ein Veröffentlichungsprofil importieren oder Microsoft Azure-WebSites, um zu authentifizieren, und wählen Sie eine vorhandene Websites aktivieren.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-226">You can either import a publishing profile or select Microsoft Azure WebSites in order to authenticate and select one of your existing sites.</span></span>

<span data-ttu-id="fe9ef-227">Seit ich eine auch immer Meine Veröffentlichungsprofile von Meine Azure-Verwaltungsportal heruntergeladen haben, ich fahren Sie fort, und wählen Sie "**Import**" und geben Sie einfach die Veröffentlichung Profildatei, die ich meine Azure-Website heruntergeladen haben:</span><span class="sxs-lookup"><span data-stu-id="fe9ef-227">Since I’ve got a habit of always downloading my publishing profiles from my Azure Portal, I’ll go ahead and select "**Import**" and simply specify the publishing profile file that I’ve downloaded from my Azure website:</span></span>

![Klicken Sie im Dialogfeld Web veröffentlichen wird mit der Registerkarte Verbindung sichtbar angezeigt.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/15.Publish-Web-Dialog.png)

<span data-ttu-id="fe9ef-229">Anschließend müssen wir nur auf die Schaltfläche "Veröffentlichen" klicken.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-229">With that done, all we need to do is click the button called "Publish".</span></span> <span data-ttu-id="fe9ef-230">Keine Angst, es nicht kompakten.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-230">Don’t be afraid, it wont bite.</span></span> <span data-ttu-id="fe9ef-231">Ich denke.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-231">I think.</span></span>

#### <a name="publish"></a><span data-ttu-id="fe9ef-232">Veröffentlichen</span><span class="sxs-lookup"><span data-stu-id="fe9ef-232">Publish</span></span> ####
<span data-ttu-id="fe9ef-233">Nachdem Sie veröffentlichen treffen, wird das Dialogfeld "Web veröffentlichen Aktivität" den Fortschritt der Bereitstellung Webauftrag angezeigt: ![im Dialogfeld Web veröffentlichen Aktivität wird angezeigt.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/16.Publish-Progress-Visual-Studio-2015.png)</span><span class="sxs-lookup"><span data-stu-id="fe9ef-233">Once you hit Publish, the Web Publish Activity dialog will display the progress of your Web Job deployment: ![The dialog Web Publish Activity is displayed.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/16.Publish-Progress-Visual-Studio-2015.png)</span></span>

<span data-ttu-id="fe9ef-234">Nachdem es erfolgt ist, sollte die WebJob in der Azure-Verwaltungsportal angezeigt: ![der Azure-Verwaltungsportal zeigt Zimmergren-O365-WebJobSample in der Liste der WebJobs mit dem Status abgeschlossen 2 Minuten vor.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/17.Web-Job-Published-as-seen-in-Azure-Portal.png)</span><span class="sxs-lookup"><span data-stu-id="fe9ef-234">Once it’s done, you should see the WebJob in your Azure Portal: ![The Azure Portal shows Zimmergren-O365-WebJobSample in the list of WebJobs with the status of, Completed 2 min ago.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/17.Web-Job-Published-as-seen-in-Azure-Portal.png)</span></span>

<span data-ttu-id="fe9ef-235">Der Status WebJob wird nun als abgeschlossen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-235">The WebJob status is now displayed as Completed.</span></span> <span data-ttu-id="fe9ef-236">Sie würden Fehler/sagen, wenn er nicht behandelten Ausnahmen auslösen oder anderweitig zur Verfügung fehlerhaft Verhalten stellen würde.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-236">It would say failure/error if it would throw any unhandled exceptions or otherwise provide unhealthy behavior.</span></span>

<span data-ttu-id="fe9ef-237">Er tut weiterhin "On Demand", aber dieser Auftrag wird stündlich jetzt tatsächlich ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-237">It still says "On Demand", but this job actually runs once every hour now.</span></span>

## <a name="monitoring-the-job-and-reviewing-logs"></a><span data-ttu-id="fe9ef-238">Überwachung des Auftrags und Protokolle überprüfen</span><span class="sxs-lookup"><span data-stu-id="fe9ef-238">Monitoring the job and reviewing logs</span></span> ##
<span data-ttu-id="fe9ef-239">Wenn Sie die oben beschriebenen Schritte durchgeführt haben, haben Sie einen Auftrag für Sie als geplante Aufgabe in der Cloud arbeiten Ausführen von Aktionen in Richtung der Office 365-Sites.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-239">If you’ve done all the previous steps, you’ve got a job working for you as a scheduled task in the cloud, performing actions toward your Office 365 site(s).</span></span>

### <a name="view-all-job-executions-and-status"></a><span data-ttu-id="fe9ef-240">Zeigen Sie aller Auftrag Ausführungen und Status an</span><span class="sxs-lookup"><span data-stu-id="fe9ef-240">View all job executions and status</span></span> ###
<span data-ttu-id="fe9ef-241">Wenn Sie überprüfen, wenn der Auftrag letzten Ausführung was das Ergebnis der jeder Ausführung des Auftrags war oder während der Ausführung des Auftrags für Änderungen überprüfen möchten, Sie können klicken Sie auf den Link unter "Protokolle" klicken Sie in der Übersicht über die WebJobs Vorgangs: ![der WebJobs-Dialogfeld , mit einem Pfeil auf den Link "Upgradeprotokolle" zeigen.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/18.View-All-WebJobs-and-status-of-execution.png)</span><span class="sxs-lookup"><span data-stu-id="fe9ef-241">If you want to review when the job last ran, what the outcome of every execution of the job was or review what happened during execution of the job, you can click on the link under "Logs" when you’re in the WebJobs overview: ![The WebJobs dialog, with an arrow pointing to the Logs link.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/18.View-All-WebJobs-and-status-of-execution.png)</span></span>

<span data-ttu-id="fe9ef-242">Dadurch erhalten Sie eine Übersicht über alle Ausführungen der ausgewählten Aufträge, einschließlich der /outcome Status:</span><span class="sxs-lookup"><span data-stu-id="fe9ef-242">This will give you an overview of all the executions of the selected jobs, including the status /outcome:</span></span>

![Die WebJob Details, einschließlich der letzte Auftrag ausgeführt wird.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/19.WebJob-Details-Overview.png)

<span data-ttu-id="fe9ef-244">Auf den hervorgehobenen Link klicken, können Sie nach unten Architekturprinzipien eine bestimmte Ausführung zum Überprüfen der Protokolle des Auftrags und stellen Sie sicher, dass Dinge kein Problem.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-244">By clicking the highlighted link, you can dig down into a specific execution to review the logs of the job and make sure things look okay.</span></span> <span data-ttu-id="fe9ef-245">Dies ist wahrscheinlich mehr relevant, wenn der Auftrag tatsächlich einen Fehler verursacht, und Sie benötigen, Fehlerursache untersuchen, wenn das Ergebnis des Auftrags falsch ist oder nicht wie erwartet.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-245">This is probably more relevant if the job actually caused an error and you needed to investigate what went wrong, or if the outcome of the job is incorrect or not as expected.</span></span>

<span data-ttu-id="fe9ef-246">Sie können auch sehen, dass die Console.WriteLine-Anweisungen, die ich so gut in Meine Console Application für diese Demo jetzt verwendet wird im Protokoll Ausführung Auftrag:</span><span class="sxs-lookup"><span data-stu-id="fe9ef-246">You can also see that the Console.WriteLine statements that I so nicely used in my Console Application for this demo now shows up in the job execution log:</span></span>

![Die WebJob-Details die Zeilen in der Protokolldatei angezeigt.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/20.Review-Logs-and-Monitor-WebJob-Execution.png)

## <a name="tips--tricks"></a><span data-ttu-id="fe9ef-248">Tipps und Tricks</span><span class="sxs-lookup"><span data-stu-id="fe9ef-248">Tips & Tricks</span></span> ##
<span data-ttu-id="fe9ef-249">Alle mit früheren Versionen von Visual Studio ausgeführt werden können, habe ich alles mit Visual Studio 2015 arbeiten.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-249">While this can all be done with earlier versions of Visual Studio, I made everything work with Visual Studio 2015.</span></span> <span data-ttu-id="fe9ef-250">Aber dabei, die es einige Punkte wurden, ich bin Hinzufügen dieser hier für den Fall, dass Sie in das gleiche umbricht.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-250">But along the way there were some gotchas, I’m adding them here in case you bump into the same thing.</span></span>

### <a name="exit-code--2146232576-problem-when-running-the-job"></a><span data-ttu-id="fe9ef-251">Exit Code-2146232576 Problem bei der Ausführung des Auftrags</span><span class="sxs-lookup"><span data-stu-id="fe9ef-251">Exit code -2146232576 problem when running the job</span></span> ###
<span data-ttu-id="fe9ef-252">Seit dem Start eines Projekts Visual Studio 2015 (Preview) Serverstart es das Projekt als eine Konsolenanwendung, die auf **.NET Framework 4.5.3**basiert.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-252">Since I started a Visual Studio 2015 (Preview) project, it started the project up as a Console Application based on **.NET Framework 4.5.3**.</span></span>

<span data-ttu-id="fe9ef-253">Ausführen des Auftrags lokal funktioniert, da .NET Framework 4.5.3 auf meinem Computer Dev vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-253">Running the job locally works fine, since .NET Framework 4.5.3 exist on my dev machine.</span></span> <span data-ttu-id="fe9ef-254">Wenn ich den Auftrag zur eigene Windows Azure-Website als eine WebJob bereitgestellt, ist fehlgeschlagen, es mit "**Code-2146232576 beenden**".</span><span class="sxs-lookup"><span data-stu-id="fe9ef-254">However, once I deployed the job to My Windows Azure Web Site as a WebJob, it failed with "**exit code -2146232576**".</span></span>

#### <a name="solution-make-sure-youre-on-the-correct-net-version"></a><span data-ttu-id="fe9ef-255">Lösung: Stellen Sie sicher, dass Sie die richtige Version .NET sind</span><span class="sxs-lookup"><span data-stu-id="fe9ef-255">Solution: Make sure you’re on the correct .NET version</span></span> ####
<span data-ttu-id="fe9ef-256">Eine Weile gedauert hat, bevor ich, wenn ich in **.NET Framework 4.5**geändert, funktioniert aber nicht Azure .NET Framework, Version 4.5.3 gefallen realisiert.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-256">It took a while before I realized that Azure didn’t like .NET Framework version 4.5.3, but when I changed to **.NET Framework 4.5**, it works.</span></span>

<span data-ttu-id="fe9ef-257">Sie in das Problem umbricht, stellen Sie nur sicher, dass Ihre Arbeit unter die richtige .NET Framework-Version ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-257">If you bump into that problem, just make sure your job is executing under the correct .NET framework version.</span></span>
<span data-ttu-id="fe9ef-258">![Zeigt die Eigenschaften von Visual Studio-Projekt-Seite, Registerkarte Anwendung, mit der Ziel-Framework-Dropdown-, Hervorheben Punkt NET Framework 4.5.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/21.Change-NET-Framework-In-Visual-Studio-2015.png)</span><span class="sxs-lookup"><span data-stu-id="fe9ef-258">![Displays the Visual Studio Project Properties page, Application tab, showing the Target framework drop down, highlighting dot NET Framework 4.5.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/21.Change-NET-Framework-In-Visual-Studio-2015.png)</span></span>

# <a name="summary"></a><span data-ttu-id="fe9ef-259">Summary</span><span class="sxs-lookup"><span data-stu-id="fe9ef-259">Summary</span></span> #
<span data-ttu-id="fe9ef-260">Es ist, zwar nicht sehr viel bis hin zum Erstellen einer Azure WebJob können Sie sie sehr komplex haben.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-260">While there’s not very much to building an Azure WebJob, you can make them quite complex.</span></span> <span data-ttu-id="fe9ef-261">Das allgemeine Konzept sehr gerade vorwärts ist jedoch klicken Sie dann als alle komplexe Projekte im Lieferumfang der Entscheidungen um Authentifizierung, Code Stabilität und Zuverlässigkeit, hohe Verfügbarkeit Szenarien, Wartungsfreundlichkeit und so weiter.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-261">The overall concept is very straight forward – but then as with all complex projects comes the decisions around authentication, code stability and reliability, high availability scenarios, maintainability and so on.</span></span> <span data-ttu-id="fe9ef-262">Diese Variablen für jedes Projekt eindeutig sind und vor dem "nur Bereitstellen von" sorgfältig geplant werden sollte einen Auftrag zum Azure.</span><span class="sxs-lookup"><span data-stu-id="fe9ef-262">These are variables unique to each project and should be carefully considered before "just deploying" a job to Azure.</span></span>

### <a name="related-links"></a><span data-ttu-id="fe9ef-263">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="fe9ef-263">Related links</span></span> ###
-  <span data-ttu-id="fe9ef-264">[Ursprüngliche Blogbeitrag auf Azure WebJobs](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites) , indem Sie Tobias Zimmergren</span><span class="sxs-lookup"><span data-stu-id="fe9ef-264">[Original blog post on Azure WebJobs](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites) by Tobias Zimmergren</span></span>
-  [<span data-ttu-id="fe9ef-265">Empfohlene Ressourcen für Azure WebJobs</span><span class="sxs-lookup"><span data-stu-id="fe9ef-265">Recommended Resources for Azure WebJobs</span></span>](http://azure.microsoft.com/en-us/documentation/articles/websites-webjobs-resources/)
-  [<span data-ttu-id="fe9ef-266">Visual Studio 2015 (Preview) herunterladen</span><span class="sxs-lookup"><span data-stu-id="fe9ef-266">Visual Studio 2015 (Preview) Download</span></span>](http://www.visualstudio.com/en-us/downloads/visual-studio-2015-downloads-vs.aspx)
-  <span data-ttu-id="fe9ef-267">[Erstellen einer SharePoint-Add-Ins als einen Zeitgeberauftrag](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx) , indem Kirk Evans</span><span class="sxs-lookup"><span data-stu-id="fe9ef-267">[Building a SharePoint Add-in as a Timer Job](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx) by Kirk Evans</span></span>
-  [<span data-ttu-id="fe9ef-268">Zum Bereitstellen von Azure WebJobs zu Azure-Websites:</span><span class="sxs-lookup"><span data-stu-id="fe9ef-268">How to Deploy Azure WebJobs to Azure Websites</span></span>](http://azure.microsoft.com/en-us/documentation/articles/websites-dotnet-deploy-webjobs/)
-  <span data-ttu-id="fe9ef-269">[Einfache remote Zeitgeberauftrag, die Interaktion mit SharePoint Online,](http://channel9.msdn.com/Blogs/Office-365-Dev/Simple-remote-timer-job-that-interacts-with-SharePoint-Online-Office-365-Developer-Patterns-and-Prac) von Andrew Connell auf Channel 9</span><span class="sxs-lookup"><span data-stu-id="fe9ef-269">[Simple remote timer job that interacts with SharePoint Online](http://channel9.msdn.com/Blogs/Office-365-Dev/Simple-remote-timer-job-that-interacts-with-SharePoint-Online-Office-365-Developer-Patterns-and-Prac) by Andrew Connell on Channel9</span></span>

### <a name="applies-to"></a><span data-ttu-id="fe9ef-270">Gilt für</span><span class="sxs-lookup"><span data-stu-id="fe9ef-270">Applies to</span></span> ###
-  <span data-ttu-id="fe9ef-271">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="fe9ef-271">Office 365 Multi Tenant (MT)</span></span>
-  <span data-ttu-id="fe9ef-272">Office 365 dedizierte (D)</span><span class="sxs-lookup"><span data-stu-id="fe9ef-272">Office 365 Dedicated (D)</span></span>
-  <span data-ttu-id="fe9ef-273">SharePoint 2013 lokal</span><span class="sxs-lookup"><span data-stu-id="fe9ef-273">SharePoint 2013 on-premises</span></span> 
