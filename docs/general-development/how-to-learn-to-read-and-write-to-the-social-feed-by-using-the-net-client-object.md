---
title: "Lesen und Schreiben in den Feed für soziale Netzwerke mithilfe des .NET-Clientobjektmodells in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3c15ede5-8a59-47e6-a0b2-c17ec6bf4ae1
ms.openlocfilehash: 74fe67537137ffd6665a1ee0d00afdfa944ecdfa
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="read-and-write-to-the-social-feed-by-using-the-net-client-object-model-in-sharepoint"></a><span data-ttu-id="ba804-102">Lesen und Schreiben in den Feed für soziale Netzwerke mithilfe des .NET-Clientobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba804-102">How to: Learn to read and write to the social feed by using the .NET client object model in SharePoint</span></span>

<span data-ttu-id="ba804-103">Erstellen Sie eine Konsolenanwendung, die den sozialen Feed mithilfe des .NET-Clientobjektmodells in SharePoint liest bzw. in den sozialen Feed schreibt.</span><span class="sxs-lookup"><span data-stu-id="ba804-103">Create a console application that reads and writes to the social feed by using the SharePoint .NET client object model.</span></span>

## <a name="prerequisites-for-creating-a-console-application-that-reads-and-writes-to-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="ba804-104">Voraussetzungen für das Erstellen einer Konsolenanwendung, die Lese- und Schreibvorgänge auf den Feed für soziale Netzwerke mithilfe des Clientobjektmodells für SharePoint.NET</span><span class="sxs-lookup"><span data-stu-id="ba804-104">Prerequisites for creating a console application that reads and writes to the social feed by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="ba804-105"><a name="bkmk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="ba804-105"><a name="bkmk_Prereqs"> </a></span></span>

<span data-ttu-id="ba804-p101">Die Konsolenanwendung, die Sie erstellen, einen Zielbenutzer Feed abruft und druckt den Stamm-Post von jedem Thread in einer nummerierten Liste. Klicken Sie dann veröffentlicht eine einfache Text-Antwort an den ausgewählten Thread. Die gleiche-Methode ( [CreatePost]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx)) ) wird verwendet, um beide Beiträge veröffentlichen und Antworten Sie den Feed.</span><span class="sxs-lookup"><span data-stu-id="ba804-p101">The console application that you'll create retrieves a target user's feed and prints the root post from each thread in a numbered list. Then, it publishes a simple text reply to the selected thread. The same method ( [CreatePost]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx)) ) is used to publish both posts and replies to the feed.</span></span>
  
    
    
<span data-ttu-id="ba804-109">Zum Erstellen der Konsolenanwendung benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="ba804-109">To create the console application, you'll need the following:</span></span>
  
    
    

- <span data-ttu-id="ba804-110">SharePoint mit konfigurierter „Meine Website“, mit erstellten persönlichen Websites für den aktuellen Benutzer und einen Zielbenutzer sowie mit einigen vom Zielbenutzer erstellten Beiträgen</span><span class="sxs-lookup"><span data-stu-id="ba804-110">SharePoint with My Site configured, with personal sites created for the current user and a target user, and with a few posts written by the target user</span></span>
    
  
- <span data-ttu-id="ba804-111">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="ba804-111">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="ba804-112">Zugriffsberechtigungen vom Typ **Vollzugriff** auf die Benutzerprofil-Dienstanwendung für den angemeldeten Benutzer</span><span class="sxs-lookup"><span data-stu-id="ba804-112">**Full Control** access permissions to the User Profile service application for the logged-on user</span></span>
    
> [!NOTE]
> <span data-ttu-id="ba804-113">Wenn Sie die Entwicklungsaufgaben nicht auf dem Computer durchführen, auf dem SharePoint ausgeführt wird, laden Sie die [SharePoint-Clientkomponenten](http://www.microsoft.com/en-us/download/details.aspx?id=35585) herunter, die die SharePoint-Clientassemblys enthalten.</span><span class="sxs-lookup"><span data-stu-id="ba804-113">[Note:](http://www.microsoft.com/en-us/download/details.aspx?id=35585) If you're not developing on the computer that is running SharePoint, get the  SharePoint Client Components download that contains SharePoint client assemblies.</span></span>
  
    
    


### <a name="core-concepts-to-know-about-working-with-sharepoint-social-feeds"></a><span data-ttu-id="ba804-114">Kernkonzepte zum Arbeiten mit sozialen Feeds in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba804-114">Core concepts to know about working with SharePoint social feeds</span></span>
<span data-ttu-id="ba804-115"><a name="bkmk_CoreConcepts"> </a></span><span class="sxs-lookup"><span data-stu-id="ba804-115"><a name="bkmk_CoreConcepts"> </a></span></span>

<span data-ttu-id="ba804-116">Tabelle 1 enthält Links zu Artikeln, in denen wichtige Kernkonzepte zu, die Sie kennen sollten beschreiben, bevor Sie beginnen.</span><span class="sxs-lookup"><span data-stu-id="ba804-116">Table 1 contains links to articles that describe core concepts you should know before you get started.</span></span>
  
    
    

<span data-ttu-id="ba804-117">**In Tabelle 1. Zentrale Konzepte für die Arbeit mit sozialen Feeds SharePoint**</span><span class="sxs-lookup"><span data-stu-id="ba804-117">**Table 1. Core concepts for working with SharePoint social feeds**</span></span>


|<span data-ttu-id="ba804-118">**Titel des Artikels**</span><span class="sxs-lookup"><span data-stu-id="ba804-118">**Article title**</span></span>|<span data-ttu-id="ba804-119">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="ba804-119">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="ba804-120">Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba804-120">Get started developing with social features in SharePoint</span></span>](get-started-developing-with-social-features-in-sharepoint.md) <br/> |<span data-ttu-id="ba804-121">Hier erhalten Sie Hilfe zu den ersten Schritten beim Programmieren mit sozialen Feeds und Mikroblogbeiträgen, beim Folgen von Personen und Inhalten (Dokumente, Websites und Tags) sowie beim Arbeiten mit Benutzerprofilen.</span><span class="sxs-lookup"><span data-stu-id="ba804-121">Find out how to get started programming with social feeds and microblog posts, following people and content (documents, sites, and tags.md), and working with user profiles.</span></span>  <br/> |
| [<span data-ttu-id="ba804-122">Arbeiten mit sozialen Feeds in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba804-122">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md) <br/> |<span data-ttu-id="ba804-123">Informationen Sie zu allgemeinen Programmieraufgaben zum Arbeiten mit sozialen Feeds und die API, die Sie zum Ausführen der Aufgaben verwenden.</span><span class="sxs-lookup"><span data-stu-id="ba804-123">Learn about common programming tasks for working with social feeds and the API that you use to perform the tasks.</span></span>  <br/> |
   

## <a name="create-the-console-application-in-visual-studio-2012-and-add-references-to-client-assemblies"></a><span data-ttu-id="ba804-124">Erstellen Sie die Konsolenanwendung in Visual Studio 2012, und fügen Sie Verweise auf Clientassemblys</span><span class="sxs-lookup"><span data-stu-id="ba804-124">Create the console application in Visual Studio 2012 and add references to client assemblies</span></span>
<span data-ttu-id="ba804-125"><a name="bkmk_CreateApp"> </a></span><span class="sxs-lookup"><span data-stu-id="ba804-125"><a name="bkmk_CreateApp"> </a></span></span>


1. <span data-ttu-id="ba804-126">Öffnen Sie auf Ihrem Entwicklungscomputer Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="ba804-126">On your development computer, open Visual Studio 2012.</span></span>
    
  
2. <span data-ttu-id="ba804-127">Klicken Sie in der Menüleiste auf **Datei**, **Neu**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="ba804-127">On the menu bar, choose **File**, **New**, **Project**.</span></span>
    
  
3. <span data-ttu-id="ba804-128">Wählen Sie im Dialogfeld **Neues Projekt** aus der Dropdownliste oben im Dialogfeld die Option **.NET Framework 4.5**.</span><span class="sxs-lookup"><span data-stu-id="ba804-128">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
4. <span data-ttu-id="ba804-129">Wählen Sie **Windows**, und wählen Sie dann die Vorlage **Konsolenanwendung**, aus der Liste **Vorlagen**.</span><span class="sxs-lookup"><span data-stu-id="ba804-129">From the **Templates** list, choose **Windows**, and then choose the **Console Application** template.</span></span>
    
  
5. <span data-ttu-id="ba804-130">Nennen Sie das Projekt ReadWriteMySite, und wählen Sie dann auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="ba804-130">Name the project ReadWriteMySite, and then choose the **OK** button.</span></span>
    
  
6. <span data-ttu-id="ba804-131">Fügen Sie wie folgt Verweise auf die Clientassemblys hinzu:</span><span class="sxs-lookup"><span data-stu-id="ba804-131">Add references to the client assemblies, as follows:</span></span>
    
   <span data-ttu-id="ba804-132">a.</span><span class="sxs-lookup"><span data-stu-id="ba804-132">a.</span></span> <span data-ttu-id="ba804-133">Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü für das Projekt **ReadWriteMySite**, und wählen Sie dann **Verweis hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="ba804-133">In **Solution Explorer**, open the shortcut menu for the **ReadWriteMySite** project, and then choose **Add Reference**.</span></span>
  
   <span data-ttu-id="ba804-134">b.</span><span class="sxs-lookup"><span data-stu-id="ba804-134">b.</span></span> <span data-ttu-id="ba804-135">Wählen Sie im Dialogfeld **Verweis-Manager** die folgenden Assemblys aus:</span><span class="sxs-lookup"><span data-stu-id="ba804-135">In the **Reference Manager** dialog box, choose the following assemblies:</span></span>
    
     - <span data-ttu-id="ba804-136">**Microsoft.SharePoint.Client**</span><span class="sxs-lookup"><span data-stu-id="ba804-136">**Microsoft.SharePoint.Client**</span></span>
    
     - <span data-ttu-id="ba804-137">**Microsoft.SharePoint.Client.Runtime**</span><span class="sxs-lookup"><span data-stu-id="ba804-137">**Microsoft.SharePoint.Client.Runtime**</span></span>
    
     - <span data-ttu-id="ba804-138">**Microsoft.SharePoint.Client.UserProfiles**</span><span class="sxs-lookup"><span data-stu-id="ba804-138">**Microsoft.SharePoint.Client.UserProfiles**</span></span>  

   <span data-ttu-id="ba804-139">Wenn Sie auf dem Computer entwickeln, auf dem SharePoint ausgeführt wird, befinden sich die Assemblys in der Kategorie **Erweiterungen**.</span><span class="sxs-lookup"><span data-stu-id="ba804-139">If you are developing on the computer that is running SharePoint, the assemblies are in the **Extensions** category.</span></span> <span data-ttu-id="ba804-140">Andernfalls wechseln Sie zu dem Speicherort, der die heruntergeladenen Clientassemblys enthält (siehe [SharePoint-Clientkomponenten](http://www.microsoft.com/downloads/details.aspx?FamilyID=66da4a3e-e3b0-45d9-9e84-a84946fbf239)).</span><span class="sxs-lookup"><span data-stu-id="ba804-140">Otherwise, browse to the location that has the client assemblies you downloaded (see [SharePoint Client Components](http://www.microsoft.com/downloads/details.aspx?FamilyID=66da4a3e-e3b0-45d9-9e84-a84946fbf239)).</span></span>
    
  
7. <span data-ttu-id="ba804-141">Fügen Sie in der Datei "Program.cs" die folgenden **using**-Anweisungen hinzu.</span><span class="sxs-lookup"><span data-stu-id="ba804-141">In the Program.cs file, add the following **using** statements.</span></span>
    
```cs
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;
```


## <a name="retrieve-the-social-feed-for-a-target-user-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="ba804-142">Abrufen von den Feed für soziale Netzwerke für einen Zielbenutzer mithilfe des Clientobjektmodells für SharePoint.NET</span><span class="sxs-lookup"><span data-stu-id="ba804-142">Retrieve the social feed for a target user by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="ba804-143"><a name="bkmk_RetrieveFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="ba804-143"><a name="bkmk_RetrieveFeed"> </a></span></span>


1. <span data-ttu-id="ba804-144">Deklarieren Sie Variablen für die Server-URL und die Kontoanmeldeinformationen des Zielbenutzers.</span><span class="sxs-lookup"><span data-stu-id="ba804-144">Declare variables for the server URL and target user's account credentials.</span></span>
    
    ```cs
    const string serverUrl = "http://serverName/";
    const string targetUser = "domainName\\userName";
    ```

    > [!NOTE]
    > <span data-ttu-id="ba804-145">Ersetzen Sie unbedingt die Platzhalterwerte `http://serverName/` und `domainName\\userName`, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="ba804-145">`http://serverName/` Remember to replace the  `domainName\\userName` and  placeholder values before you run the code.</span></span>
   
2. <span data-ttu-id="ba804-146">Initialisieren Sie in der **Main**-Methode den SharePoint-Clientkontext.</span><span class="sxs-lookup"><span data-stu-id="ba804-146">In the **Main** method, initialize the SharePoint client context.</span></span>
    
    ```cs
    ClientContext clientContext = new ClientContext(serverUrl);
    ```

3. <span data-ttu-id="ba804-147">Erstellen Sie die  [SocialFeedManager]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx)) -Instanz.</span><span class="sxs-lookup"><span data-stu-id="ba804-147">Create the  [SocialFeedManager]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx)) instance.</span></span>
    
    ```cs
    SocialFeedManager feedManager = new SocialFeedManager(clientContext);
    ```

4. <span data-ttu-id="ba804-148">Geben Sie die Parameter für den feed Inhalt, den Sie abrufen möchten.</span><span class="sxs-lookup"><span data-stu-id="ba804-148">Specify the parameters for the feed content that you want to retrieve.</span></span>
    
    ```cs
    SocialFeedOptions feedOptions = new SocialFeedOptions();
    feedOptions.MaxThreadCount = 10;
    ```

    <span data-ttu-id="ba804-149">Die Standardoptionen zurückgeben die ersten 20 Threads im Feed, sortiert nach Datum der letzten Änderung.</span><span class="sxs-lookup"><span data-stu-id="ba804-149">The default options return the first 20 threads in the feed, sorted by last modified date.</span></span>
  
5. <span data-ttu-id="ba804-150">Rufen Sie den Feed des Zielbenutzers ab.</span><span class="sxs-lookup"><span data-stu-id="ba804-150">Get the target user's feed.</span></span>
    
    ```cs 
    ClientResult<SocialFeed> feed = feedManager.GetFeedFor(targetUser, feedOptions);
    clientContext.ExecuteQuery();
    ```

    <span data-ttu-id="ba804-151">[GetFeedFor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeedFor.aspx)) gibt ein **ClientResult<T>** -Objekt, das die Auflistung der Threads im dessen [Value](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientResult\`1.Value.aspx) -Eigenschaft gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="ba804-151">[GetFeedFor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeedFor.aspx)) returns a **ClientResult<T>** object that stores the collection of threads in its [Value](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientResult\`1.Value.aspx) property.</span></span>
    
  

## <a name="iterate-through-and-read-from-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="ba804-152">Durchlaufen und Lesen des sozialen Feeds mithilfe des SharePoint .NET-Clientobjektmodells</span><span class="sxs-lookup"><span data-stu-id="ba804-152">Iterate through and read from the social feed by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="ba804-153"><a name="bkmk_ReadFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="ba804-153"></span></span>

<span data-ttu-id="ba804-p105">Der folgende Code durchläuft die Threads im Feed. Es wird überprüft, ob jeder Thread verfügt über das Attribut  [CanReply]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadAttributes.CanReply.aspx)) und ruft dann die Thread-ID und den Text des Beitrags Stamm ab. Der Code auch ein Wörterbuch, das die Thread-ID zu speichern (zu einem Thread Antworten) erstellt und schreibt den Text des Beitrags Stamm in der Konsole angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ba804-p105">The following code iterates through the threads in the feed. It checks whether each thread has the  [CanReply]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadAttributes.CanReply.aspx)) attribute and then gets the thread identifier and the text of the root post. The code also creates a dictionary to store the thread identifier (which is used to reply to a thread) and writes the text of the root post to the console.</span></span>

```cs
Dictionary<int, string> idDictionary = new Dictionary<int, string>();
for (int i = 0; i < feed.Value.Threads.Length; i++)
{
    SocialThread thread = feed.Value.Threads[i];
    string postText = thread.RootPost.Text;
    if (thread.Attributes.HasFlag(SocialThreadAttributes.CanReply))
    {
        idDictionary.Add(i, thread.Id);
        Console.WriteLine("\\t" + (i + 1) + ". " + postText);
    }
}
```


## <a name="post-a-reply-to-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="ba804-157">Bereitstellen Sie eine Antwort auf den Feed für soziale Netzwerke, mit dem .NET SharePoint-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="ba804-157">Post a reply to the social feed by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="ba804-158"><a name="bkmk_WriteFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="ba804-158"></span></span>


1. <span data-ttu-id="ba804-159">(UI-bezogene nur) Rufen Sie den Thread Antworten zu und Aufforderung für Antwort des Benutzers.</span><span class="sxs-lookup"><span data-stu-id="ba804-159">(UI-related only) Get the thread to reply to and prompt for the user's reply.</span></span>
    
```cs
Console.Write("Which post number do you want to reply to?  ");
string threadToReplyTo = "";
int threadNumber = int.Parse(Console.ReadLine()) - 1;
idDictionary.TryGetValue(threadNumber, out threadToReplyTo);
Console.Write("Type your reply:  ");
```

2. <span data-ttu-id="ba804-p106">Definieren Sie die Antwort. Der folgende Code Ruft die Antwort Text aus der Konsolenanwendung ab.</span><span class="sxs-lookup"><span data-stu-id="ba804-p106">Define the reply. The following code gets the reply's text from the console application.</span></span>
    
```cs
SocialPostCreationData postCreationData = new SocialPostCreationData();
postCreationData.ContentText = Console.ReadLine();
```

3. <span data-ttu-id="ba804-p107">Veröffentlichen Sie die Antwort. Der _ThreadToReplyTo_-Parameter steht für die [Id]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.Id.aspx))-Eigenschaft des Threads.</span><span class="sxs-lookup"><span data-stu-id="ba804-p107">Publish the reply. The  _threadToReplyTo_ parameter represents of the thread's [Id]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.Id.aspx)) property.</span></span>
    
```cs
feedManager.CreatePost(threadToReplyTo, postCreationData);
clientContext.ExecuteQuery();
```

    > [!NOTE]
    > The  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) method is also used to publish a root post to the current user's feed by passing **null** for the first parameter.

4. <span data-ttu-id="ba804-164">(Nur in Bezug auf die Benutzeroberfläche) Beenden Sie das Programm.</span><span class="sxs-lookup"><span data-stu-id="ba804-164">(UI-related only) Exit the program.</span></span>
    
    ```cs
    Console.WriteLine("Your reply was published.");
    Console.ReadKey(false);
    ```

5. <span data-ttu-id="ba804-165">Wählen Sie zum Testen der Konsolenanwendung, klicken Sie auf der Menüleiste **Debuggen**, **Debuggen starten** aus.</span><span class="sxs-lookup"><span data-stu-id="ba804-165">To test the console application, on the menu bar, choose **Debug**, **Start Debugging**.</span></span>
    
  

## <a name="code-example-retrieve-a-feed-and-reply-to-a-post-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="ba804-166">Codebeispiel: Abrufen ein Feeds und Antworten auf einen Beitrag mithilfe des Clientobjektmodells für SharePoint.NET</span><span class="sxs-lookup"><span data-stu-id="ba804-166">Code example: Retrieve a feed and reply to a post by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="ba804-167"><a name="bkmk_CodeExample"> </a></span><span class="sxs-lookup"><span data-stu-id="ba804-167"></span></span>

<span data-ttu-id="ba804-168">Im folgende Beispiel wird der vollständige Code aus der Datei Program.cs.</span><span class="sxs-lookup"><span data-stu-id="ba804-168">The following example is the complete code from the Program.cs file.</span></span>
  
```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace ReadWriteMySite
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the target server running SharePoint and the
            // target thread owner.
            const string serverUrl = "http://serverName/";
            const string targetUser = "domainName\\userName";

            // Connect to the client context.
            ClientContext clientContext = new ClientContext(serverUrl);

            // Get the SocialFeedManager instance.
            SocialFeedManager feedManager = new SocialFeedManager(clientContext);

            // Specify the parameters for the feed content that you want to retrieve.
            SocialFeedOptions feedOptions = new SocialFeedOptions();
            feedOptions.MaxThreadCount = 10;

            // Get the target owner's feed (posts and activities) and then run the request on the server.
            ClientResult<SocialFeed> feed = feedManager.GetFeedFor(targetUser, feedOptions);
            clientContext.ExecuteQuery();

            // Create a dictionary to store the Id property of each thread. This code example stores
            // the ID so a user can select a thread to reply to from the console application.
            Dictionary<int, string> idDictionary = new Dictionary<int, string>();
            for (int i = 0; i < feed.Value.Threads.Length; i++)
            {
                SocialThread thread = feed.Value.Threads[i];

                // Keep only the threads that can be replied to.
                if (thread.Attributes.HasFlag(SocialThreadAttributes.CanReply))
                {
                    idDictionary.Add(i, thread.Id);

                    // Write out the text of the post.
                    Console.WriteLine("\\t" + (i + 1) + ". " + thread.RootPost.Text);
                }
            }
            Console.Write("Which post number do you want to reply to?  ");

            string threadToReplyTo = "";
            int threadNumber = int.Parse(Console.ReadLine()) - 1;
            idDictionary.TryGetValue(threadNumber, out threadToReplyTo);

            Console.Write("Type your reply:  ");

            // Define properties for the reply.
            SocialPostCreationData postCreationData = new SocialPostCreationData();
            postCreationData.ContentText = Console.ReadLine();
            
            // Post the reply and make the changes on the server.
            feedManager.CreatePost(threadToReplyTo, postCreationData);
            clientContext.ExecuteQuery();

            Console.WriteLine("Your reply was published.");
            Console.ReadKey(false);

            // TODO: Add error handling and input validation.
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="ba804-169">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="ba804-169">Next steps</span></span>
<span data-ttu-id="ba804-170"><a name="SP15ReadWriteSocial_nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="ba804-170"></span></span>

<span data-ttu-id="ba804-171">Weitere Informationen zum mehr Aufgaben lesen und Schreiben von Aufgaben mit den Feed für soziale Netzwerke mithilfe des Clientobjektmodells .NET aus, lesen Sie Folgendes ein:</span><span class="sxs-lookup"><span data-stu-id="ba804-171">To learn how to do more read tasks and write tasks with the social feed by using the .NET client object model, see the following:</span></span>
  
    
    

-  [<span data-ttu-id="ba804-172">Gewusst wie: Erstellen und Löschen von Beiträgen und Abrufen des sozialen Feeds über das .NET-Clientobjektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba804-172">How to: Create and delete posts and retrieve the social feed by using the .NET client object model in SharePoint</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md)
    
  

## <a name="see-also"></a><span data-ttu-id="ba804-173">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="ba804-173">See also</span></span>
<span data-ttu-id="ba804-174"><a name="SP15ReadWriteSocial_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ba804-174"></span></span>


-  [<span data-ttu-id="ba804-175">Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba804-175">Get started developing with social features in SharePoint</span></span>](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ba804-176">Arbeiten mit sozialen Feeds in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba804-176">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  

