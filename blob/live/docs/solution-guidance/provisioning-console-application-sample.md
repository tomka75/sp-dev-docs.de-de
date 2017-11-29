---
title: Beispiel einer Anwendung in Konsole-Bereitstellung
ms.date: 11/03/2017
ms.openlocfilehash: 29d14151ccea3bebec3c7e1a899bdf8067321193
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="provisioning-console-application-sample"></a><span data-ttu-id="94a41-102">Beispiel einer Anwendung in Konsole-Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="94a41-102">Provisioning console application sample</span></span>

<span data-ttu-id="94a41-103">Grundlagen Sie der Verwendung des Plug & Play-provisioning-Moduls zum Erstellen und beibehalten, und wenden Sie dann provisioning Vorlagen für neue SharePoint-Websitesammlungen.</span><span class="sxs-lookup"><span data-stu-id="94a41-103">Learn the fundamentals of using the PnP provisioning engine to create and persist, and then apply provisioning templates to new SharePoint site collections.</span></span>

<span data-ttu-id="94a41-104">Um das neue Add-In-Modell zu unterstützen, hat die Anwendung Office 365 Developer Mustern und Methoden (Plug & Play-) einer Bereitstellung Framework eingeführt, das ermöglicht es Benutzern, benutzerdefinierte Websitevorlagen erstellen, indem Sie einfach auf den in einem Website-Modell, das Modell als provisioning Vorlage beibehalten, und klicken Sie dann die benutzerdefinierte Vorlage für neue oder vorhandene Websitesammlungen übernehmen, je nach Bedarf.</span><span class="sxs-lookup"><span data-stu-id="94a41-104">To support the new add-in model, the Office 365 Developer Patterns and Practices program (PnP) has introduced a provisioning framework that allows users to create custom site templates by simply pointing at a site model, persist the model as a provisioning template, and then apply the custom template to new or existing site collections as needed.</span></span>

<span data-ttu-id="94a41-105">In diesem Beispiel erstellen wir eine grundlegende Konsolenanwendung, die Klassen in der Bereitstellung Plug & Play-Hauptbibliothek das Bereitstellung Plug & Play-Modul für die Durchführung dieser Bereitstellung wichtige Aufgaben aktiviert implementiert wird:</span><span class="sxs-lookup"><span data-stu-id="94a41-105">In this sample, we create a basic console application that implements classes in the provisioning PnP Core library to enable the PnP provisioning engine to complete these essential provisioning tasks:</span></span> 

- <span data-ttu-id="94a41-106">Entwerfen und modellieren einer Website Anpassungstools.</span><span class="sxs-lookup"><span data-stu-id="94a41-106">Design and model your site customization.</span></span> <span data-ttu-id="94a41-107">Dies kann ein neues Design der Website sein, oder Sie können zu einer vorhandenen Website zeigen und als provisioning Vorlage zu speichern.</span><span class="sxs-lookup"><span data-stu-id="94a41-107">This can be a new site design, or you can point to an existing site and save it as a provisioning template.</span></span>
    
- <span data-ttu-id="94a41-108">Speichern und das Modell für die Website als Vorlage provisioning beibehalten von, damit Sie wiederverwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="94a41-108">Save and persist the site model as a provisioning template so that you can reuse it.</span></span>
    
- <span data-ttu-id="94a41-109">Die Bereitstellung Vorlage auf einer neuen oder vorhandenen Websitesammlung anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="94a41-109">Apply the provisioning template to a new or existing site collection.</span></span>
    
<span data-ttu-id="94a41-110">**Hinweis:**  Diese exemplarische Vorgehensweise ist eine Ergänzung zu einer Stichprobe, die derzeit auf GitHub: [Erste Schritte mit der Plug & Play-Bereitstellung Engine](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Framework.Console).</span><span class="sxs-lookup"><span data-stu-id="94a41-110">**Note:**  This sample walkthrough is a companion to a sample currently available on GitHub: [Getting Started with the PnP Provisioning Engine](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Framework.Console).</span></span> <span data-ttu-id="94a41-111">Den Code (Program.cs) und die Lösungsdateien für das Beispiel stehen zum Download zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="94a41-111">The code (Program.cs) and solution files for the sample are available for download.</span></span> <span data-ttu-id="94a41-112">Auch steht eine 20 Minuten video Präsentation dieses Prozesses (mit geringfügig Code) auf der Website Microsoft Channel 9: [Erste Schritte mit der Plug & Play-Bereitstellung Engine](https://channel9.msdn.com/blogs/OfficeDevPnP/Getting-Started-with-PnP-Provisioning-Engine).</span><span class="sxs-lookup"><span data-stu-id="94a41-112">There also is a 20-minute video presentation of this process (with slightly different code) available on the Microsoft Channel 9 site: [Getting Started with the PnP Provisioning Engine](https://channel9.msdn.com/blogs/OfficeDevPnP/Getting-Started-with-PnP-Provisioning-Engine).</span></span>

## <a name="remote-provisioning-walkthrough"></a><span data-ttu-id="94a41-113">Remote provisioning Exemplarische Vorgehensweise</span><span class="sxs-lookup"><span data-stu-id="94a41-113">Remote provisioning walkthrough</span></span>

<span data-ttu-id="94a41-114">Erstellen Sie zunächst ein Visual Studio-Projekt.</span><span class="sxs-lookup"><span data-stu-id="94a41-114">To begin, create a Visual Studio project.</span></span> <span data-ttu-id="94a41-115">In diesem Beispiel zur Vereinfachung erstellen wir eine standardkonsolenanwendung, die die Plug & Play-Bereitstellung Engine mithilfe der Plug & Play-Hauptbibliothek provisioning Framework implementiert.</span><span class="sxs-lookup"><span data-stu-id="94a41-115">In this sample, for simplicity, we create a basic console application that implements the PnP provisioning engine by using the PnP Core library of the provisioning framework.</span></span> <span data-ttu-id="94a41-116">Um die beispiellösung zu unterstützen, müssen wir jedoch herunterladen und installieren die Bereitstellung Framework Plug & Play-Kern-Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="94a41-116">To support the sample solution, however, we must download and install the provisioning framework PnP Core library.</span></span> <span data-ttu-id="94a41-117">Führen Sie die Anweisungen zur Folge.</span><span class="sxs-lookup"><span data-stu-id="94a41-117">Instructions for doing so follow.</span></span>

### <a name="create-and-prepare-a-visual-studio-project"></a><span data-ttu-id="94a41-118">Erstellen und Vorbereiten eines Visual Studio-Projekts</span><span class="sxs-lookup"><span data-stu-id="94a41-118">Create and prepare a Visual Studio project</span></span>

1. <span data-ttu-id="94a41-119">Starten Sie Visual Studio, und wählen Sie dann **Datei** > **New** > **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="94a41-119">Launch Visual Studio, and then choose  **File** > **New** > **Project**.</span></span>
    
2. <span data-ttu-id="94a41-120">Assistenten **Neues Projekt** wählen Sie **Visual c#**, und wählen Sie dann **Konsolenanwendung**.</span><span class="sxs-lookup"><span data-stu-id="94a41-120">In the  **New Project** wizard, choose **Visual C#**, then choose  **Console Application**.</span></span>
    
3. <span data-ttu-id="94a41-121">Nennen Sie das Projekt "Programm", und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="94a41-121">Name the project "Program," and then click  **OK**.</span></span> <span data-ttu-id="94a41-122">(Sie können das Projekt einen beliebigen, aber beim Beachten Sie, dass dieser exemplarischen Vorgehensweise verweisen Sie auf den Projektnamen als "Program." wird, Namen)</span><span class="sxs-lookup"><span data-stu-id="94a41-122">(You can name the project anything you like, but be mindful that this walkthrough will reference the project name as "program.")</span></span>
    
4. <span data-ttu-id="94a41-123">Herunterladen und installieren Sie die Plug & Play-Core-Bibliothek, die als ein NuGet-Paket zur Verfügung steht: [OfficeDevPnP.Core Pakete](https://www.nuget.org/profiles/officedevpnp).</span><span class="sxs-lookup"><span data-stu-id="94a41-123">Download and install the PnP Core library that is available as a NuGet package here: [OfficeDevPnP.Core packages](https://www.nuget.org/profiles/officedevpnp).</span></span>
    
    <span data-ttu-id="94a41-124">**Hinweis:**  Es gibt zwei Versionen der Kernbibliothek.</span><span class="sxs-lookup"><span data-stu-id="94a41-124">**Note:**  There are two versions of the core library.</span></span> <span data-ttu-id="94a41-125">Eine Version ist der **OfficeDevPnP.Core** -Bibliothek, die SharePoint Online und Office 365 beruht.</span><span class="sxs-lookup"><span data-stu-id="94a41-125">One version is the **OfficeDevPnP.Core** library, which targets SharePoint Online and Office 365.</span></span> <span data-ttu-id="94a41-126">Die zweite Version ist **OfficeDevPnP.Core (lokal)**, die SharePoint 2013 lokal beruht.</span><span class="sxs-lookup"><span data-stu-id="94a41-126">The second version is **OfficeDevPnP.Core (on-premises)**, which targets SharePoint 2013 on-premises.</span></span> <span data-ttu-id="94a41-127">Hier ist ein Screenshot der verfügbaren Optionen aus.</span><span class="sxs-lookup"><span data-stu-id="94a41-127">Here is a screenshot of the available options.</span></span>

    ![Zwei zentrale Bibliothek Download-Optionen](media/provisioning-console-application-sample/5b1adb8d-52e5-4c67-8792-6ef0ae41d655.png)

<span data-ttu-id="94a41-129">Im folgenden Beispiel wird die erste Option in SharePoint Online-Ziel verwendet.</span><span class="sxs-lookup"><span data-stu-id="94a41-129">In this sample walkthrough, we're using the first option to target SharePoint Online.</span></span>

1. <span data-ttu-id="94a41-130">Installieren Sie zuerst den NuGet-Client durch das Aufrufen der [NuGet-Clientinstallationsprogramm](http://docs.nuget.org/consume/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="94a41-130">First, install the NuGet client by going to the [NuGet client installer](http://docs.nuget.org/consume/installing-nuget).</span></span>

2. <span data-ttu-id="94a41-131">Nach der NuGet ist führen Sie den **NuGet-Paket-Manager-**Client installiert.</span><span class="sxs-lookup"><span data-stu-id="94a41-131">After the NuGet client is installed, run the  **NuGet Package manager**.</span></span> <span data-ttu-id="94a41-132">Maustaste auf den Knoten **Verweise** im Visual Studio- **Projektmappen-Explorer**, und wählen Sie dann **NuGet-Pakete verwalten**aus.</span><span class="sxs-lookup"><span data-stu-id="94a41-132">Right-click the  **References** node in the Visual Studio **Solution Explorer**, and then select  **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="94a41-133">Wählen Sie im Paket-Manager **Online**, klicken Sie dann **EntityFramework**, und geben Sie den Suchbegriff "OfficeDev", um die Bibliothek OfficeDevPnP.Core verfügbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="94a41-133">In the Package Manager, choose **Online**, then  **EntityFramework**, and then enter the search term "OfficeDev" to expose the OfficeDevPnP.Core library.</span></span>

4. <span data-ttu-id="94a41-134">Führen Sie die Schritte zum Herunterladen und Installieren der **OfficeDevPnP.Core** -Bibliothek nach der angegebenen Richtung.</span><span class="sxs-lookup"><span data-stu-id="94a41-134">Follow directions to download and install the  **OfficeDevPnP.Core** library, following the given directions.</span></span>

   <span data-ttu-id="94a41-135">Nachdem die Plug & Play-Core-Bibliothek in Visual Studio-Projekt verwiesen wird, werden alle Bibliotheksmitglieder als [Erweiterungsmethoden](https://msdn.microsoft.com/en-us/library/bb383977.aspx) für vorhandene Objektinstanzen, zum **Beispiel, **Web** und** Listeninstanzen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="94a41-135">After the PnP Core library is referenced in your Visual Studio project, all library members are available to you as [extension methods](https://msdn.microsoft.com/en-us/library/bb383977.aspx) on existing object instances, for example, **web** and **list** instances.</span></span>

5. <span data-ttu-id="94a41-136">Stellen Sie sicher, dass Ihre Datei Program.cs die folgenden enthält `using` Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="94a41-136">Ensure that your Program.cs file contains all of the following  `using` statements.</span></span>

    ```c#
    using Microsoft.SharePoint.Client;
    using OfficeDevPnP.Core.Framework.Provisioning.Connectors;
    using OfficeDevPnP.Core.Framework.Provisioning.Model;
    using OfficeDevPnP.Core.Framework.Provisioning.ObjectHandlers;
    using OfficeDevPnP.Core.Framework.Provisioning.Providers.Xml;
    using System;
    using System.Net;
    using System.Security;
    using System.Threading;
    ```

<span data-ttu-id="94a41-137">**Nachdem wir das Projekt eingerichtet haben**</span><span class="sxs-lookup"><span data-stu-id="94a41-137">**Once we have set up your project**</span></span>

<span data-ttu-id="94a41-138">Nachdem Sie Ihrem Projekt eingerichtet haben, können Sie Ihre websiteanpassungen erstellen.</span><span class="sxs-lookup"><span data-stu-id="94a41-138">Once your project is set up, you can create your site customizations.</span></span> <span data-ttu-id="94a41-139">Sie können dies manuell tun oder zeigen Sie auf einer Website, deren Design verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="94a41-139">You can do this by hand or by pointing to a site whose design you wish to use.</span></span> <span data-ttu-id="94a41-140">Speichern Sie den Entwurf der gewünschten Website einfach als provisioning Vorlage.</span><span class="sxs-lookup"><span data-stu-id="94a41-140">Simply save the chosen site design as a provisioning template.</span></span> <span data-ttu-id="94a41-141">Oder Sie können eine Mischung aus beiden Ansätze verwenden.</span><span class="sxs-lookup"><span data-stu-id="94a41-141">Or, you can use a mix of both approaches.</span></span> <span data-ttu-id="94a41-142">Für dieses Beispiel wird es einfach zu einer vorhandenen Website, und speichern Sie die zusammengesetztes Design und websiteartefakte (nicht jedoch seinen Inhalt) als provisioning Vorlage verweisen.</span><span class="sxs-lookup"><span data-stu-id="94a41-142">For the purpose of this sample, we will simply point to an existing site and save its composed look and site artifacts (but not its content) as a provisioning template.</span></span>

<span data-ttu-id="94a41-143">Zunächst müssen wir für die Verbindung zu der Website, die wir als Grundlage unserer Vorlage provisioning modellieren möchten.</span><span class="sxs-lookup"><span data-stu-id="94a41-143">To begin, we need to connect to the site that we wish to model as our provisioning template.</span></span> <span data-ttu-id="94a41-144">Zunächst Sammeln der Verbindungsinformationen, einschließlich Benutzername, Kennwort und die Quell-URL.</span><span class="sxs-lookup"><span data-stu-id="94a41-144">Let's start by gathering connection information, including user name, password, and the source URL.</span></span>

### <a name="create-and-extract-and-persist-the-provisioning-template"></a><span data-ttu-id="94a41-145">Erstellen und extrahieren und die Bereitstellung Vorlage beibehalten</span><span class="sxs-lookup"><span data-stu-id="94a41-145">Create and extract and persist the provisioning template</span></span>

1. <span data-ttu-id="94a41-146">Sammeln von Informationen zur Verbindung vom Benutzer.</span><span class="sxs-lookup"><span data-stu-id="94a41-146">Collect connection information from the user.</span></span> <span data-ttu-id="94a41-147">Beachten Sie, dass in der Anwendung `Main` routinemäßige, wir drei einfachen Dinge tun: Sammeln der Verbindungsinformationen, die Bereitstellung Vorlage erhalten möchten, und die Bereitstellung Vorlage anwenden.</span><span class="sxs-lookup"><span data-stu-id="94a41-147">Note that in the program's  `Main` routine, we do three simple things: collect connection information, GET the provisioning template, and APPLY the provisioning template.</span></span> <span data-ttu-id="94a41-148">Die schwierigsten wird von den Methoden **GetProvisioningTemplate** und **ApplyProvisioningTemplate** durchgeführt, die wir unten definieren.</span><span class="sxs-lookup"><span data-stu-id="94a41-148">The heavy lifting is done by the **GetProvisioningTemplate** and **ApplyProvisioningTemplate** methods that we define below.</span></span>
    
    ```C#
    static void Main(string[] args)
        {
            ConsoleColor defaultForeground = Console.ForegroundColor;
    
            // Collect information 
            string templateWebUrl = GetInput("Enter the URL of the template site: ", false, defaultForeground);
            string targetWebUrl = GetInput("Enter the URL of the target site: ", false, defaultForeground);
            string userName = GetInput("Enter your user name:", false, defaultForeground);
            string pwdS = GetInput("Enter your password:", true, defaultForeground);
            SecureString pwd = new SecureString();
            foreach (char c in pwdS.ToCharArray()) pwd.AppendChar(c);
    
            // GET the template from existing site and serialize
            // Serializing the template for later reuse is optional
            ProvisioningTemplate template = GetProvisioningTemplate(defaultForeground, templateWebUrl, userName, pwd);
    
            // APPLY the template to new site from 
            ApplyProvisioningTemplate(defaultForeground, targetWebUrl, userName, pwd, template);
    
            // Pause and modify the UI to indicate that the operation is complete
            Console.ForegroundColor = ConsoleColor.White;
            Console.WriteLine("We're done. Press Enter to continue.");
            Console.ReadLine();
        }
    ```

2. <span data-ttu-id="94a41-149">Erstellen Sie und verwenden Sie eine private **GetInput** -Methode, um die erforderlichen Anmeldeinformationen abzurufen.</span><span class="sxs-lookup"><span data-stu-id="94a41-149">Create and use a private  **GetInput** method to obtain the required user credentials.</span></span>
    
    ```c#
    private static string GetInput(string label, bool isPassword, ConsoleColor defaultForeground)
        {
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine("{0} : ", label);
            Console.ForegroundColor = defaultForeground;
    
            string value = "";
    
            for (ConsoleKeyInfo keyInfo = Console.ReadKey(true); keyInfo.Key != ConsoleKey.Enter; keyInfo = Console.ReadKey(true))
            {
                if (keyInfo.Key == ConsoleKey.Backspace)
                {
                    if (value.Length > 0)
                    {
                        value = value.Remove(value.Length - 1);
                        Console.SetCursorPosition(Console.CursorLeft - 1, Console.CursorTop);
                        Console.Write(" ");
                        Console.SetCursorPosition(Console.CursorLeft - 1, Console.CursorTop);
                    }
                }
                else if (keyInfo.Key != ConsoleKey.Enter)
                {
                    if (isPassword)
                    {
                        Console.Write("*");
                    }
                    else
                    {
                        Console.Write(keyInfo.KeyChar);
                    }
                    value += keyInfo.KeyChar;
    
                }
    
            }
            Console.WriteLine("");
    
            return value;
        }
    ```

3. <span data-ttu-id="94a41-150">Zeigen Sie auf der Website, die das Modell für die Bereitstellung der Grundlage unserer Vorlage ist.</span><span class="sxs-lookup"><span data-stu-id="94a41-150">Point to the site that's the model for our provisioning template.</span></span> <span data-ttu-id="94a41-151">Während der GET auf der Quellwebsite mit einer einzelnen Codezeile, sehen Sie sich `GetProvisioningTemplate()`, der GET-Methode, die wir definiert.</span><span class="sxs-lookup"><span data-stu-id="94a41-151">While doing the GET on the source site with a single line of code, look at  `GetProvisioningTemplate()`, the GET method we defined.</span></span> 
    
    ```c#
    private static ProvisioningTemplate GetProvisioningTemplate(ConsoleColor defaultForeground, string webUrl, string userName, SecureString pwd)
        {
            using (var ctx = new ClientContext(webUrl))
            {
                // ctx.Credentials = new NetworkCredentials(userName, pwd);
                ctx.Credentials = new SharePointOnlineCredentials(userName, pwd);
                ctx.RequestTimeout = Timeout.Infinite;
    
                // Just to output the site details
                Web web = ctx.Web;
                ctx.Load(web, w => w.Title);
                ctx.ExecuteQueryRetry();
    
                Console.ForegroundColor = ConsoleColor.White;
                Console.WriteLine("Your site title is:" + ctx.Web.Title);
                Console.ForegroundColor = defaultForeground;
    
                ProvisioningTemplateCreationInformation ptci
                        = new ProvisioningTemplateCreationInformation(ctx.Web);
    
                // Create FileSystemConnector to store a temporary copy of the template 
                ptci.FileConnector = new FileSystemConnector(@"c:\temp\pnpprovisioningdemo", "");
                ptci.PersistComposedLookFiles = true;
                ptci.ProgressDelegate = delegate(String message, Int32 progress, Int32 total)
                {
                    // Only to output progress for console UI
                    Console.WriteLine("{0:00}/{1:00} - {2}", progress, total, message);
                };
    
                // Execute actual extraction of the template
                ProvisioningTemplate template = ctx.Web.GetProvisioningTemplate(ptci);
    
                // We can serialize this template to save and reuse it
                // Optional step 
                XMLTemplateProvider provider =
                        new XMLFileSystemTemplateProvider(@"c:\temp\pnpprovisioningdemo", "");
                provider.SaveAs(template, "PnPProvisioningDemo.xml");
    
                return template;
            }
        }
    ```

    <span data-ttu-id="94a41-152">Im obigen Codeausschnitt definiert wir auch eine Variable, **ProvisioningTemplateCreationInformation** - **Pcti**.</span><span class="sxs-lookup"><span data-stu-id="94a41-152">In the above code snippet, we also defined a  **ProvisioningTemplateCreationInformation** variable, **pcti**.</span></span> <span data-ttu-id="94a41-153">Die Variable liefert uns die Option zum Speichern von Informationen über Artefakte, die zusammen mit der Vorlage gespeichert werden können.</span><span class="sxs-lookup"><span data-stu-id="94a41-153">The variable gives us the option to store information about artifacts that we can save along with the template.</span></span>
    
4. <span data-ttu-id="94a41-154">Erstellen Sie ein File System Connector-Objekt, sodass wir eine temporäre Kopie der Bereitstellung Vorlage speichern können, die wir zu einer anderen Website anwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="94a41-154">Create a file system connector object so that we can store a temporary copy of the provisioning template that we're going to apply to another site.</span></span>
    
    <span data-ttu-id="94a41-155">**Hinweis:**  Dieser Schritt ist optional.</span><span class="sxs-lookup"><span data-stu-id="94a41-155">**Note:**  This step is optional.</span></span> <span data-ttu-id="94a41-156">Es ist nicht erforderlich, dass Sie die Bereitstellung Vorlage XML serialisieren.</span><span class="sxs-lookup"><span data-stu-id="94a41-156">It's not required that you serialize the provisioning template to XML.</span></span> <span data-ttu-id="94a41-157">Zu diesem Zeitpunkt ist die Vorlage einfach C#-Code.</span><span class="sxs-lookup"><span data-stu-id="94a41-157">At this stage, the template is simply C# code.</span></span> <span data-ttu-id="94a41-158">Nicht nur Serialisierung optional ist, sondern auch können Serialisierungsformat werden soll.</span><span class="sxs-lookup"><span data-stu-id="94a41-158">Not only is serialization optional, but you also can use whatever serialization format you wish.</span></span>

5. <span data-ttu-id="94a41-159">Führen Sie die Extrahierung der Bereitstellung Vorlage mithilfe von nur diese einzelnen Codezeile.</span><span class="sxs-lookup"><span data-stu-id="94a41-159">Execute the extraction of the provisioning template by using just this single line of code.</span></span>      `ProvisioningTemplate template = ctx.Web.GetProvisioningTemplate(ptci);`
    
6. <span data-ttu-id="94a41-160">(Optional) Speichern Sie und speichern Sie eine serialisierte Version der Bereitstellung Vorlage zu, damit Sie wiederverwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="94a41-160">(Optional) Save and store a serialized version of the provisioning template so that you can reuse it.</span></span> <span data-ttu-id="94a41-161">Sie können die Bereitstellung Vorlage in Standarddateiformate serialisieren gewünschte.</span><span class="sxs-lookup"><span data-stu-id="94a41-161">You can serialize the provisioning template in whichever format you prefer.</span></span> <span data-ttu-id="94a41-162">In diesem Beispiel haben wir in eine XML-Datei mit dem Namen **PnPProvisioningDemo.xml**serialisiert.</span><span class="sxs-lookup"><span data-stu-id="94a41-162">In this sample, we've serialized to an XML file named  **PnPProvisioningDemo.xml**.</span></span> <span data-ttu-id="94a41-163">Die Datei selbst ist ein **XMLFileSystemTemplateProvider** -Objekt für die wir einen Speicherort im Dateisystem bereitgestellt haben.</span><span class="sxs-lookup"><span data-stu-id="94a41-163">The file itself is an **XMLFileSystemTemplateProvider** object for which we've provided a file system location.</span></span>
    
<span data-ttu-id="94a41-164">**Nachdem wir extrahieren, speichern und die Bereitstellung Vorlage beibehalten**</span><span class="sxs-lookup"><span data-stu-id="94a41-164">**Once we extract, save and persist the provisioning template**</span></span>

<span data-ttu-id="94a41-165">Nachdem wir extrahieren, speichern und die Bereitstellung Vorlage beibehalten, ist der nächste und letzte Schritt der Bereitstellung Vorlage auf einer neuen SharePoint-Websitesammlung an, mit der **ApplyProvisioningTemplate** -Methode.</span><span class="sxs-lookup"><span data-stu-id="94a41-165">Once we extract, save, and persist the provisioning template, the next and final step is to apply the provisioning template to a new SharePoint site collection by using the  **ApplyProvisioningTemplate** method.</span></span>

### <a name="apply-the-provisioning-template-to-a-new-or-existing-site"></a><span data-ttu-id="94a41-166">Wenden Sie die Bereitstellung Vorlage zu einer neuen oder vorhandenen Website</span><span class="sxs-lookup"><span data-stu-id="94a41-166">Apply the provisioning template to a new or existing site</span></span>

1. <span data-ttu-id="94a41-167">Anmeldeinformationen für die Zielwebsite zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="94a41-167">Obtain credentials to the target site.</span></span>
    
    ```c#
    // ctx.Credentials = new NetworkCredentials(userName, pwd);
                ctx.Credentials = new SharePointOnlineCredentials(userName, pwd);
                ctx.RequestTimeout = Timeout.Infinite;
    ```

2. <span data-ttu-id="94a41-168">Erfassen Sie websiteartefakte, die mit der **ProvisioningTemplateCreationInformation** -Methode mit der **ProvisioningTemplateApplyingInformation**-Methode Companion gespeichert wurden.</span><span class="sxs-lookup"><span data-stu-id="94a41-168">Capture site artifacts that were stored using the  **ProvisioningTemplateCreationInformation** method by using the companion method, **ProvisioningTemplateApplyingInformation**.</span></span>
    
    ```c#
    ProvisioningTemplateApplyingInformation ptai
                        = new ProvisioningTemplateApplyingInformation();
                ptai.ProgressDelegate = delegate(String message, Int32 progress, Int32 total)
                {
                    Console.WriteLine("{0:00}/{1:00} - {2}", progress, total, message);
                };
    ```

3. <span data-ttu-id="94a41-169">Rufen Sie eine Zuordnung und der Datei-Konnektor für die Objekte.</span><span class="sxs-lookup"><span data-stu-id="94a41-169">Get an association to the file connector for the assets.</span></span>
    
    ```c#
    // Associate file connector for assets
                FileSystemConnector connector = new FileSystemConnector(@"c:\temp\pnpprovisioningdemo", "");
                template.Connector = connector;
    
    ```

4. <span data-ttu-id="94a41-170">(Optional) Da Bereitstellung eine Objektinstanz verwendet wird, können wir Code, um websiteartefakte dynamisch anpassen schreiben.</span><span class="sxs-lookup"><span data-stu-id="94a41-170">(Optional) Because the provisioning template is an object instance, we can write code to customize site artifacts on the fly.</span></span> <span data-ttu-id="94a41-171">In diesem Fall haben wir eine neue "Kontaktliste" hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="94a41-171">In this instance, we're adding a new "contact" list.</span></span>
    
    ```c#
    // Since template is actual object, we can modify this using code as needed
                template.Lists.Add(new ListInstance()
                {
                    Title = "PnP Sample Contacts",
                    Url = "lists/PnPContacts",
                    TemplateType = (Int32)ListTemplateType.Contacts,
                    EnableAttachments = true
                });
    ```

5.  <span data-ttu-id="94a41-172">Anzuwenden Sie die Bereitstellung Vorlage auf die neue Website erneut mit einer Codezeile.</span><span class="sxs-lookup"><span data-stu-id="94a41-172">Apply the provisioning template to the new site, again using one line of code.</span></span>
    
    ```c#
        web.ApplyProvisioningTemplate(template, ptai);
    ```

## <a name="additional-resources"></a><span data-ttu-id="94a41-173">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="94a41-173">Additional resources</span></span>
<span data-ttu-id="94a41-174"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="94a41-174"></span></span>

- [<span data-ttu-id="94a41-175">Plug & Play-Bereitstellung framework</span><span class="sxs-lookup"><span data-stu-id="94a41-175">PnP provisioning framework</span></span>](pnp-provisioning-framework.md)
    
- [<span data-ttu-id="94a41-176">Plug & Play-Bereitstellung Modul- und die Core-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="94a41-176">PnP provisioning engine and the core library</span></span>](pnp-provisioning-engine-and-the-core-library.md)
