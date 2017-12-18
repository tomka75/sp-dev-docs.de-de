---
title: "Erstellen und Löschen von Beiträgen und Abrufen des sozialen Feeds über das .NET-Clientobjektmodell in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c8d68632-1b55-454c-961a-f3ddad731bf6
ms.openlocfilehash: dfbf3dccf1212b967a19385f51d12c6bafcd04a1
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-client-object-model-in-sharepoint"></a><span data-ttu-id="85ba3-102">Erstellen und Löschen von Beiträgen und Abrufen des sozialen Feeds über das .NET-Clientobjektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="85ba3-102">How to: Create and delete posts and retrieve the social feed by using the .NET client object model in SharePoint</span></span>

<span data-ttu-id="85ba3-103">In diesem Artikel erfahren Sie, wie Sie mithilfe des .NET-Clientobjektmodells in SharePoint Mikroblogbeiträge erstellen und löschen und soziale Feeds abrufen.</span><span class="sxs-lookup"><span data-stu-id="85ba3-103">Learn how to create and delete microblog posts and retrieve social feeds by using the SharePoint .NET client object model.</span></span>

## <a name="what-are-social-feeds-in-sharepoint"></a><span data-ttu-id="85ba3-104">Was sind thematische Feeds in SharePoint?</span><span class="sxs-lookup"><span data-stu-id="85ba3-104">What are social feeds in SharePoint?</span></span>
<span data-ttu-id="85ba3-105"><a name="bk_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="85ba3-105"><a name="bk_intro"> </a></span></span>

<span data-ttu-id="85ba3-106">Ein Feed für soziale Netzwerke ist in SharePoint eine Sammlung von Threads, die Unterhaltungen, einzelne Mikroblogbeiträge oder Benachrichtigungen darstellen.</span><span class="sxs-lookup"><span data-stu-id="85ba3-106">In SharePoint, a social feed is a collection of threads that represent conversations, single microblog posts, or notifications.</span></span> <span data-ttu-id="85ba3-107">Threads enthalten einen Stammbeitrag und eine Sammlung von Antwortbeiträgen und stellen Unterhaltungen, einzelne Mikroblogbeiträge oder Benachrichtigungen dar.</span><span class="sxs-lookup"><span data-stu-id="85ba3-107">Threads contain a root post and a collection of reply posts, and they represent conversations, single microblog posts, or notifications.</span></span> <span data-ttu-id="85ba3-108">Im .NET-Objektmodell werden Feeds durch [SocialFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeed.aspx)-Objekte dargestellt, Threads durch [SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx)-Objekte und Beiträge und Antworten durch [SocialPost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPost.aspx)-Objekte.</span><span class="sxs-lookup"><span data-stu-id="85ba3-108">In the .NET client object model, feeds are represented by  [SocialFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeed.aspx) objects, threads are represented by [SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) objects, and posts and replies are represented by [SocialPost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPost.aspx) objects.</span></span> <span data-ttu-id="85ba3-109">Um wichtige Feed-bezogene Aufgaben im .NET-Clientobjektmodell auszuführen, verwenden Sie das [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx)-Objekt.</span><span class="sxs-lookup"><span data-stu-id="85ba3-109">To perform core feed-related tasks in the .NET client object model, you use the [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) object.</span></span> <span data-ttu-id="85ba3-110">In diesem Artikel wird gezeigt, wie Sie eine Konsolenanwendung erstellen, die das .NET-Clientobjektmodell zum Arbeiten mit sozialen Feeds verwendet.</span><span class="sxs-lookup"><span data-stu-id="85ba3-110">In this article, we'll show you how to create a console application that uses the .NET client object model to work with social feeds.</span></span>
  
    
    
<span data-ttu-id="85ba3-111">Weitere Informationen zum Arbeiten mit  [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) oder Informationen zur Verwendung von anderen APIs mit sozialen Feeds arbeiten finden Sie unter [Arbeiten mit sozialen Feeds in SharePoint](work-with-social-feeds-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="85ba3-111">For more information about working with  [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) or for information about using other APIs to work with social feeds, see [Work with social feeds in SharePoint](work-with-social-feeds-in-sharepoint.md).</span></span>
  
    
    

## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-social-feeds-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="85ba3-112">Voraussetzungen für das Einrichten Ihrer Entwicklungsumgebung sozialen Feeds mithilfe des Clientobjektmodells für SharePoint.NET entwickelt</span><span class="sxs-lookup"><span data-stu-id="85ba3-112">Prerequisites for setting up your development environment to work with social feeds by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="85ba3-113"><a name="bkmk_SetUpDevEnv"> </a></span><span class="sxs-lookup"><span data-stu-id="85ba3-113"><a name="bkmk_SetUpDevEnv"> </a></span></span>

<span data-ttu-id="85ba3-114">Zum Erstellen einer Konsolenanwendung, die das .NET-Clientobjektmodell zum Arbeiten mit sozialen Feeds verwendet, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="85ba3-114">To create a console application that uses the .NET client object model to work with social feeds, you'll need:</span></span>
  
    
    

- <span data-ttu-id="85ba3-115">SharePoint mit konfigurierter „Meine Website“, mit erstellten persönlichen Websites für den aktuellen Benutzer und einen Zielbenutzer, wobei der aktuelle Benutzer dem Zielbenutzer folgt, und mit einigen vom Zielbenutzer erstellten Beiträgen</span><span class="sxs-lookup"><span data-stu-id="85ba3-115">SharePoint with My Site configured, with personal sites created for the current user and a target user, with the current user following the target user, and with a few posts written by the target user</span></span>
    
  
- <span data-ttu-id="85ba3-116">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="85ba3-116">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="85ba3-117">Zugriffsberechtigungen vom Typ **Vollzugriff** auf die Benutzerprofil-Dienstanwendung für den angemeldeten Benutzer</span><span class="sxs-lookup"><span data-stu-id="85ba3-117">**Full Control** access permissions to the User Profile service application for the logged-on user</span></span>
    
  

> <span data-ttu-id="85ba3-118">**Hinweis:** Wenn Sie die Entwicklungsaufgaben nicht auf dem Computer durchführen, auf dem SharePoint ausgeführt wird, laden Sie die [SharePoint-Clientkomponenten](http://www.microsoft.com/en-us/download/details.aspx?id=35585) herunter, die die SharePoint-Clientassemblys enthalten.</span><span class="sxs-lookup"><span data-stu-id="85ba3-118">**Note:** If you are not developing on the computer that is running SharePoint, get the  [SharePoint Client Components](http://www.microsoft.com/en-us/download/details.aspx?id=35585) download that contains SharePoint client assemblies.</span></span>
  
    
    


## <a name="create-a-console-application-that-works-with-social-feeds-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="85ba3-119">Erstellen einer Konsolenanwendung, die mit sozialen Feeds arbeitet, mithilfe des SharePoint .NET-Clientobjektmodells</span><span class="sxs-lookup"><span data-stu-id="85ba3-119">Create a console application that works with social feeds by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="85ba3-120"><a name="bk_createconsole"> </a></span><span class="sxs-lookup"><span data-stu-id="85ba3-120"><a name="bk_createconsole"> </a></span></span>


1. <span data-ttu-id="85ba3-121">Öffnen Sie Visual Studio, und wählen Sie **Datei**, **Neu**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="85ba3-121">Open Visual Studio and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="85ba3-122">Wählen Sie im Dialogfeld **Neues Projekt** aus der Dropdownliste oben im Dialogfeld die Option **.NET Framework 4.5**.</span><span class="sxs-lookup"><span data-stu-id="85ba3-122">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="85ba3-123">Klicken Sie in der Liste **Vorlagen** wählen Sie **Windows**, und wählen Sie dann die Vorlage **Konsolenanwendung**.</span><span class="sxs-lookup"><span data-stu-id="85ba3-123">In the **Templates** list, choose **Windows**, and then choose the **Console Application** template.</span></span>
    
  
4. <span data-ttu-id="85ba3-124">Nennen Sie das Projekt SocialFeedCSOM, und wählen Sie dann auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="85ba3-124">Name the project SocialFeedCSOM, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="85ba3-125">Fügen Sie Verweise auf die folgenden Assemblys hinzu:</span><span class="sxs-lookup"><span data-stu-id="85ba3-125">Add references to the following assemblies:</span></span>
    
   - <span data-ttu-id="85ba3-126">**Microsoft.SharePoint.Client**</span><span class="sxs-lookup"><span data-stu-id="85ba3-126">**Microsoft.SharePoint.Client**</span></span>
   - <span data-ttu-id="85ba3-127">**Microsoft.SharePoint.ClientRuntime**</span><span class="sxs-lookup"><span data-stu-id="85ba3-127">**Microsoft.SharePoint.ClientRuntime**</span></span>
   - <span data-ttu-id="85ba3-128">**Microsoft.SharePoint.Client.UserProfiles**</span><span class="sxs-lookup"><span data-stu-id="85ba3-128">**Microsoft.SharePoint.Client.UserProfiles**</span></span>
  
6. <span data-ttu-id="85ba3-129">Ersetzen Sie die Inhalte der **Program**-Klasse durch das Codebeispiel aus einem der folgenden Szenarien:</span><span class="sxs-lookup"><span data-stu-id="85ba3-129">Replace the contents of the **Program** class with the code example from one of the following scenarios:</span></span>
    
   -  [<span data-ttu-id="85ba3-130">Veröffentlichen von Beiträgen und Antworten Sie den Feed für soziale Netzwerke</span><span class="sxs-lookup"><span data-stu-id="85ba3-130">Publish posts and replies to the social feed</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md#bkmk_PubPosts) 
   -  [<span data-ttu-id="85ba3-131">Abrufen von sozialen feeds</span><span class="sxs-lookup"><span data-stu-id="85ba3-131">Retrieve social feeds</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md#bkmk_GetFeeds) 
   -  [<span data-ttu-id="85ba3-132">Delete-Beiträgen und Antworten aus dem sozialen feed</span><span class="sxs-lookup"><span data-stu-id="85ba3-132">Delete posts and replies from the social feed</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md#bkmk_DeletePosts)
    
7. <span data-ttu-id="85ba3-133">Wählen Sie zum Testen der Konsolenanwendung, klicken Sie auf der Menüleiste **Debuggen**, **Debuggen starten** aus.</span><span class="sxs-lookup"><span data-stu-id="85ba3-133">To test the console application, on the menu bar, choose **Debug**, **Start Debugging**.</span></span>
    
  

## <a name="code-example-publish-posts-and-replies-to-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="85ba3-134">Codebeispiel: Veröffentlichen von Beiträgen und Antworten auf die Nutzung von sozialen Netzwerken feed mithilfe des Clientobjektmodells für SharePoint.NET</span><span class="sxs-lookup"><span data-stu-id="85ba3-134">Code example: Publish posts and replies to the social feed by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="85ba3-135"><a name="bkmk_PubPosts"> </a></span><span class="sxs-lookup"><span data-stu-id="85ba3-135"><a name="bkmk_PubPosts"> </a></span></span>

<span data-ttu-id="85ba3-p102">Im folgenden Codebeispiel wird veröffentlicht ein Beitrag und aus dem aktuellen Benutzer eine Antwort. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="85ba3-p102">The following code example publishes a post and a reply from the current user. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="85ba3-p103">Nach Inhalt definiert. Dieses Beispiel enthält einen Link in der POST-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="85ba3-p103">Define post content. This example includes a link in the post.</span></span>
    
  
- <span data-ttu-id="85ba3-140">Veröffentlichen Sie einen Post im Feed des aktuellen Benutzers mithilfe der  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx)-Methode, und übergeben Sie dabei **null** als _targetId_-Parameter.</span><span class="sxs-lookup"><span data-stu-id="85ba3-140">Publish a post to the current user's feed by using the  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) method and passing **null** as the _targetId_ parameter.</span></span>
    
  
- <span data-ttu-id="85ba3-141">Rufen Sie den **News**-[Feedtyp](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.aspx) für den aktuellen Benutzer mithilfe der [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx)-Methode ab.</span><span class="sxs-lookup"><span data-stu-id="85ba3-141">Get the **News** [feed type](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.aspx) for the current user by using the [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx) method.</span></span>
    
  
- <span data-ttu-id="85ba3-142">Durchlaufen Sie den Feed, um alle Threads zu finden, die beantwortet werden können, und um Informationen zu Threads und Beiträgen zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="85ba3-142">Iterate through the feed to find all threads that can be replied to and to get information about threads and posts.</span></span>
    
  
- <span data-ttu-id="85ba3-143">Antworten Sie auf einen Beitrag mithilfe der  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx)-Methode, und übergeben Sie dabei die Thread-ID als _targetId_-Parameter.</span><span class="sxs-lookup"><span data-stu-id="85ba3-143">Reply to a post by using the  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) method and passing the thread identifier as the _targetId_ parameter.</span></span>
    
  

> <span data-ttu-id="85ba3-144">**Hinweis:** Ändern Sie den Platzhalterwert für die Variable **serverUrl**, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="85ba3-144">**Note:** Change the placeholder value for the **serverUrl** variable before you run the code.</span></span>
  
    
    


```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace SocialFeedCSOM
{
    class Program
    {
        static void Main(string[] args)
        {
            // Replace the following placeholder value with the target server URL.
            const string serverUrl = "http://serverName/";

            Console.Write("Type your post text:  ");

            // Create a link to include in the post.
            SocialDataItem linkDataItem = new SocialDataItem();
            linkDataItem.ItemType = SocialDataItemType.Link;
            linkDataItem.Text = "link";
            linkDataItem.Uri = "http://bing.com";

            // Define properties for the post.
            SocialPostCreationData postCreationData = new SocialPostCreationData();
            postCreationData.ContentText = Console.ReadLine() + " Plus a {0}.";
            postCreationData.ContentItems = new SocialDataItem[1] { linkDataItem };

            // Get the client context.
            ClientContext clientContext = new ClientContext(serverUrl);

            // Get the SocialFeedManager instance.
            SocialFeedManager feedManager = new SocialFeedManager(clientContext);

            // Publish the post. This is a root post, so specify null for the
            // targetId parameter. 
            feedManager.CreatePost(null, postCreationData); 
            clientContext.ExecuteQuery();

            Console.WriteLine("\\nCurrent user's newsfeed:");

            // Set parameters for the feed content that you want to retrieve.
            SocialFeedOptions feedOptions = new SocialFeedOptions();

            // Get the target owner's feed and then run the request on the server.
            ClientResult<SocialFeed> feed = feedManager.GetFeed(SocialFeedType.News, feedOptions);
            clientContext.ExecuteQuery();

            // Create a dictionary to store the Id property of each thread. This 
            // code example stores the Id so you can select a thread to reply to.
            Dictionary<int, string> idDictionary = new Dictionary<int, string>();

            // Iterate through each thread in the feed.
            for (int i = 0; i < feed.Value.Threads.Length; i++)
            {
                SocialThread thread = feed.Value.Threads[i];

                // Keep only the threads that can be replied to.
                if (thread.Attributes.HasFlag(SocialThreadAttributes.CanReply))
                {
                    idDictionary.Add(i, thread.Id);

                    // Get properties from the root post and thread.
                    // If a thread contains more than two replies, the server returns
                    // a thread digest that contains only the two most recent replies.
                    // To get all replies, call SocialFeedManager.GetFullThread.
                    SocialPost rootPost = thread.RootPost;
                    SocialActor author = thread.Actors[rootPost.AuthorIndex];
                    Console.WriteLine(string.Format("{0}. {1} said \\"{2}\\" ({3} replies)",
                        (i + 1), author.Name, rootPost.Text, thread.TotalReplyCount));
                }
            }
            Console.Write("\\nWhich thread number do you want to reply to?  ");

            string threadToReplyTo = "";
            int threadNumber = int.Parse(Console.ReadLine()) - 1;
            idDictionary.TryGetValue(threadNumber, out threadToReplyTo);

            Console.Write("Type your reply:  ");

            // Define properties for the reply. This example reuses the 
            // SocialPostCreationData object that was used to create a post.
            postCreationData.ContentText = Console.ReadLine();

            // Publish the reply and make the changes on the server.
            ClientResult<SocialThread> result = feedManager.CreatePost(threadToReplyTo, postCreationData);
            clientContext.ExecuteQuery();

            Console.WriteLine("\\nThe reply was published. The thread now has {0} replies.", result.Value.TotalReplyCount);
            Console.ReadLine();
         }
    }
}
```


## <a name="code-example-retrieve-social-feeds-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="85ba3-145">Codebeispiel: Abrufen von sozialen Feeds mithilfe des Clientobjektmodells für SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="85ba3-145">Code example: Retrieve social feeds by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="85ba3-146"><a name="bkmk_GetFeeds"> </a></span><span class="sxs-lookup"><span data-stu-id="85ba3-146"><a name="bkmk_GetFeeds"> </a></span></span>

<span data-ttu-id="85ba3-p104">Das folgende Codebeispiel ruft Feeds für den aktuellen Benutzer sowie einen Zielbenutzer ab. Es zeigt, wie Sie die folgenden Schritte ausführen:</span><span class="sxs-lookup"><span data-stu-id="85ba3-p104">The following code example retrieves feeds for the current user and a target user. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="85ba3-149">Rufen Sie die [Feedtypen](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.aspx) **Personal**, **News** und **Timeline** für den aktuellen Benutzer mithilfe der [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx)-Methode ab.</span><span class="sxs-lookup"><span data-stu-id="85ba3-149">Get the **Personal**, **News**, and **Timeline**[feed types](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.aspx) for the current user by using the [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx) method.</span></span>
    
  
- <span data-ttu-id="85ba3-150">Rufen Sie den **Personal**-[Feedtyp](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.Personal.aspx) für einen Zielbenutzer mithilfe der [getFeedFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeedFor.aspx)-Methode ab.</span><span class="sxs-lookup"><span data-stu-id="85ba3-150">Get the **Personal** [feed type](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.Personal.aspx) for a target user by using the [GetFeedFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeedFor.aspx) method.</span></span>
    
  
- <span data-ttu-id="85ba3-p105">Durchlaufen Sie die Feeds, um alle Threads im nicht-Verweis zu suchen und Abrufen von Informationen zu Threads und Beiträge. Verweis Threads darstellen Benachrichtigungen, die Informationen zu einem anderen Thread enthalten. Wenn ein Benutzer eine Person in einem Beitrag erwähnt wird, generiert der Server beispielsweise ein **MentionReference**-Thread, der den Link zur ursprünglichen Beitrags und andere Metadaten zu dem Beitrag enthält geben.</span><span class="sxs-lookup"><span data-stu-id="85ba3-p105">Iterate through the feeds to find all non-reference threads and to get information about threads and posts. Reference threads represent notifications that contain information about another thread. For example, if a user mentions someone in a post, the server generates a **MentionReference**-type thread that contains the link to the original post and other metadata about the post.</span></span>
    
  
<span data-ttu-id="85ba3-154">Weitere Informationen zu Feedtypen finden Sie unter [Übersicht über Feedtypen](work-with-social-feeds-in-sharepoint.md#bkmk_FeedTypes).</span><span class="sxs-lookup"><span data-stu-id="85ba3-154">For more information about feed types, see  [Overview of feed types](work-with-social-feeds-in-sharepoint.md#bkmk_FeedTypes).</span></span> <span data-ttu-id="85ba3-155">Weitere Informationen zu Referenzthreads finden Sie unter [Referenzthreads und Digest-Threads in sozialen Feeds für SharePoint](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="85ba3-155">For more information about reference threads, see  [Reference threads and digest threads in SharePoint social feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span></span>
  
    
    

> <span data-ttu-id="85ba3-156">**Hinweis:** Ändern Sie die Platzhalterwerte für die Variablen **serverUrl** und **targetUser**, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="85ba3-156">**Note:** Change the placeholder values for the **serverUrl** and **targetUser** variables before you run the code.</span></span>
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace SocialFeedCSOM
{
    class Program
    {
        static string owner;
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the target
            // server URL and target thread owner.
            const string serverUrl = "http://serverName/";
            const string targetUser = "domainName\\\\userName";

            // Get the client context.
            ClientContext clientContext = new ClientContext(serverUrl);

            // Get the SocialFeedManager instance. 
            // Load the instance to get the Owner property.
            SocialFeedManager feedManager = new SocialFeedManager(clientContext);
            clientContext.Load(feedManager, f => f.Owner);

            // Set parameters for the feed content that you want to retrieve.
            SocialFeedOptions feedOptions = new SocialFeedOptions();
            feedOptions.MaxThreadCount = 10; // default is 20

            // Get all feed types for current user and get the Personal feed
            // for the target user.
            ClientResult<SocialFeed> personalFeed = feedManager.GetFeed(SocialFeedType.Personal, feedOptions);
            ClientResult<SocialFeed> newsFeed = feedManager.GetFeed(SocialFeedType.News, feedOptions);
            ClientResult<SocialFeed> targetUserFeed = feedManager.GetFeedFor(targetUser, feedOptions);

            // Change the sort order to optimize the Timeline feed results.
            feedOptions.SortOrder = SocialFeedSortOrder.ByCreatedTime;
            ClientResult<SocialFeed> timelineFeed = feedManager.GetFeed(SocialFeedType.Timeline, feedOptions);

            // Run the request on the server.
            clientContext.ExecuteQuery();

            // Get the name of the current user within this instance.
            owner = feedManager.Owner.Name;

            // Iterate through the feeds and write the content.
            IterateThroughFeed(personalFeed.Value, SocialFeedType.Personal, true);
            IterateThroughFeed(newsFeed.Value, SocialFeedType.News, true);
            IterateThroughFeed(timelineFeed.Value, SocialFeedType.Timeline, true);
            IterateThroughFeed(targetUserFeed.Value, SocialFeedType.Personal, false);

            Console.ReadKey(false);
        }

        // Iterate through the feed and write to the console window.
        static void IterateThroughFeed(SocialFeed feed, SocialFeedType feedType, bool isCurrentUserOwner)
        {
            SocialThread[] threads = feed.Threads;

            // If this is the target user's feed, get the user's name.
            // A user is the owner of all threads in his or her Personal feed.
            if (!isCurrentUserOwner)
            {
                SocialThread firstThread = threads[0];
                owner = firstThread.Actors[firstThread.OwnerIndex].Name;
            }
            Console.WriteLine(string.Format("\\n{0} feed type for {1}:", feedType.ToString(), owner));

            // Iterate through each thread in the feed.
            foreach (SocialThread thread in threads)
            {

                // Ignore reference thread types.
                if (thread.ThreadType == SocialThreadType.Normal)
                {

                    // Get properties from the root post and thread. 
                    // If a thread contains more than two replies, the server returns
                    // a thread digest that contains only the two most recent replies.
                    // To get all replies, call SocialFeedManager.GetFullThread.
                    SocialPost rootPost = thread.RootPost;
                    SocialActor author = thread.Actors[rootPost.AuthorIndex];
                    Console.WriteLine(string.Format("  - {0} posted \\"{1}\\" on {2}. This thread has {3} replies.",
                        author.Name, rootPost.Text, rootPost.CreatedTime.ToShortDateString(), thread.TotalReplyCount));
                }
            }
        }
    }
}
```


## <a name="code-example-delete-posts-and-replies-from-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="85ba3-157">Codebeispiel: Löschen von Beiträgen und Antworten aus dem sozialen Feed mithilfe des SharePoint .NET-Clientobjektmodells</span><span class="sxs-lookup"><span data-stu-id="85ba3-157">Code example: Delete posts and replies from the social feed by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="85ba3-158"><a name="bkmk_DeletePosts"> </a></span><span class="sxs-lookup"><span data-stu-id="85ba3-158"><a name="bkmk_DeletePosts"> </a></span></span>

<span data-ttu-id="85ba3-p107">Das folgende Codebeispiel löscht einen Beitrag oder eine Antwort aus dem persönlichen Feed des aktuellen Benutzers. Es zeigt, wie Sie folgende Schritte ausführen:</span><span class="sxs-lookup"><span data-stu-id="85ba3-p107">The following code example deletes a post or a reply from the current user's personal feed. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="85ba3-161">Rufen Sie den **Personal**-[Feedtyp](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.aspx) für den aktuellen Benutzer mithilfe der [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx)-Methode ab.</span><span class="sxs-lookup"><span data-stu-id="85ba3-161">Get the **Personal** [feed type](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.aspx) for the current user by using the [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx) method.</span></span>
    
  
- <span data-ttu-id="85ba3-162">Durchlaufen Sie die Threads im Feed, um Informationen zum Stammbeitrag und Antworten zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="85ba3-162">Iterate through the threads in the feed to get information about the root post and replies.</span></span>
    
  
- <span data-ttu-id="85ba3-163">Löschen Sie einen Stammbeitrag, eine Antwort oder einen Thread mithilfe der [DeletePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.DeletePost.aspx)-Methode (durch Löschen eines Stammbeitrags wird der gesamte Thread gelöscht).</span><span class="sxs-lookup"><span data-stu-id="85ba3-163">Delete a root post, reply, or thread by using the  [DeletePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.DeletePost.aspx) method (deleting a root post deletes the whole thread).</span></span>
    
  

> <span data-ttu-id="85ba3-164">**Hinweis:** Ändern Sie den Platzhalterwert für die Variable **serverUrl**, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="85ba3-164">**Note:** Change the placeholder value for the **serverUrl** variable before you run the code.</span></span>
  
    
    


```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace SocialFeedCSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder value with the target SharePoint server.
            const string serverUrl = "http://serverName/";

            // Get the client context.
            ClientContext clientContext = new ClientContext(serverUrl);

            // Get the SocialFeedManager instance.
            SocialFeedManager feedManager = new SocialFeedManager(clientContext);

            Console.WriteLine("\\nCurrent user's personal feed:");

            // Set the parameters for the feed content that you want to retrieve.
            SocialFeedOptions feedOptions = new SocialFeedOptions();

            // Get the target owner's feed (posts and activities) and
            // then run the request on the server.
            ClientResult<SocialFeed> feed = feedManager.GetFeed(SocialFeedType.Personal, feedOptions);
            clientContext.ExecuteQuery();

            // Create a dictionary to store the Id property of each post and
            // reply. This code example stores the Id so you can select a post
            // or a reply to delete.
            Dictionary<int, string> idDictionary = new Dictionary<int, string>();

            // Iterate through each thread in the feed.
            for (int i = 0; i < feed.Value.Threads.Length; i++)
            {
                SocialThread thread = feed.Value.Threads[i];
                SocialPost rootPost = thread.RootPost;

                // Only keep posts that can be deleted.
                if (rootPost.Attributes.HasFlag(SocialPostAttributes.CanDelete)) 
                {
                    idDictionary.Add(i, rootPost.Id);

                    Console.WriteLine(string.Format("{0}. \\"{1}\\" has {2} replies.",
                        (i + 1), rootPost.Text, thread.TotalReplyCount));

                    // Get the replies.
                    // If a thread contains more than two replies, the server returns
                    // a thread digest that contains only the two most recent replies.
                    // To get all replies, call SocialFeedManager.GetFullThread.
                    if (thread.TotalReplyCount > 0)
                    {
                        foreach (SocialPost reply in thread.Replies)
                        {

                            // Only keep replies that can be deleted.
                            if (reply.Attributes.HasFlag(SocialPostAttributes.CanDelete)) 
                            {
                                i++;
                                idDictionary.Add(i, reply.Id);

                                SocialActor author = thread.Actors[reply.AuthorIndex];
                                Console.WriteLine(string.Format("\\t{0}. {1} replied \\"{2}\\"",
                                    (i + 1), author.Name, reply.Text));
                            }
                        }
                    }
                }
            }
            Console.Write("\\nEnter the number of the post or reply to delete. "
                + "(If you choose a root post, the whole thread is deleted.)");
            string postToDelete = "";
            int postNumber = int.Parse(Console.ReadLine()) - 1;
            idDictionary.TryGetValue(postNumber, out postToDelete);

            // Delete the reply and make the changes on the server.
            ClientResult<SocialThread> result = feedManager.DeletePost(postToDelete);
            clientContext.ExecuteQuery();

            // DeletePost returns digest thread if the deleted post is not the
            // root post. If it is the root post, the whole thread is deleted
            // and DeletePost returns null.
            if (result.Value != null)
            {
                SocialThread threadResult = result.Value;
                Console.WriteLine("\\nThe reply was deleted. The thread now has {0} replies.", threadResult.TotalReplyCount);
            }
            else
            {
                Console.WriteLine("\\nThe post and thread were deleted.");
            }
            Console.ReadKey(false);
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="85ba3-165">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="85ba3-165">Next steps</span></span>
<span data-ttu-id="85ba3-166"><a name="bkmk_DeletePosts"> </a></span><span class="sxs-lookup"><span data-stu-id="85ba3-166"><a name="bkmk_DeletePosts"> </a></span></span>

 [<span data-ttu-id="85ba3-167">Vorgehensweise: Einschließen von Erwähnungen, Tags und Links zu Websites und Dokumenten in Beiträgen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="85ba3-167">How to: Include mentions, tags, and links to sites and documents in posts in SharePoint</span></span>](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md)
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="85ba3-168">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="85ba3-168">Additional resources</span></span>
<span data-ttu-id="85ba3-169"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="85ba3-169"><a name="bk_addResources"> </a></span></span>


-  [<span data-ttu-id="85ba3-170">Arbeiten mit sozialen Feeds in SharePoint</span><span class="sxs-lookup"><span data-stu-id="85ba3-170">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  
-  [<span data-ttu-id="85ba3-171">Vorgehensweise: Erstellen und Löschen von Beiträgen und sozialen Feed abrufen, indem Sie mit der JavaScript-Objektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="85ba3-171">How to: Create and delete posts and retrieve the social feed by using the JavaScript object model in SharePoint</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md)
    
  
-  [<span data-ttu-id="85ba3-172">Vorgehensweise: Lesen und Schreiben des sozialen Feeds mithilfe des REST-Diensts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="85ba3-172">How to: Learn to read and write to the social feed by using the REST service in SharePoint</span></span>](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)
    
  
-  [<span data-ttu-id="85ba3-173">Referenzthreads und Digest-Threads in sozialen Feeds für SharePoint</span><span class="sxs-lookup"><span data-stu-id="85ba3-173">Reference threads and digest threads in SharePoint social feeds</span></span>](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md)
    
  

