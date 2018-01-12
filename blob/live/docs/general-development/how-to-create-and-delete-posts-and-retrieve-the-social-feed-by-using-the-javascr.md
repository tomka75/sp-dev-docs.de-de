---
title: "Erstellen und Löschen von Beiträgen und Abrufen des sozialen Feeds über das JavaScript-Objektmodell in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e8c21960-6ea0-43c0-821e-2db2a0ecec90
ms.openlocfilehash: 4963dbb97f6106c9536353112e9f4a2ffb15c5b4
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascript-object-model-in-sharepoint"></a><span data-ttu-id="afec7-102">Erstellen und Löschen von Beiträgen und Abrufen des sozialen Feeds über das JavaScript-Objektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="afec7-102">How to: Create and delete posts and retrieve the social feed by using the JavaScript object model in SharePoint</span></span>

<span data-ttu-id="afec7-103">In diesem Artikel erfahren Sie, wie Sie mithilfe des SharePoint JavaScript-Objektmodells Mikroblogbeiträge erstellen und löschen und soziale Feeds abrufen.</span><span class="sxs-lookup"><span data-stu-id="afec7-103">Learn how to create and delete microblog posts and retrieve social feeds by using the SharePoint JavaScript object model.</span></span>

## <a name="what-are-social-feeds-in-sharepoint"></a><span data-ttu-id="afec7-104">Was sind thematische Feeds in SharePoint?</span><span class="sxs-lookup"><span data-stu-id="afec7-104">What are social feeds in SharePoint?</span></span>
<span data-ttu-id="afec7-105"><a name="bk_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="afec7-105"><a name="bk_intro"> </a></span></span>

<span data-ttu-id="afec7-106">Ein Feed für soziale Netzwerke ist in SharePoint eine Sammlung von Threads, die Unterhaltungen, einzelne Mikroblogbeiträge oder Benachrichtigungen darstellen.</span><span class="sxs-lookup"><span data-stu-id="afec7-106">In SharePoint, a social feed is a collection of threads that represent conversations, single microblog posts, or notifications.</span></span> <span data-ttu-id="afec7-107">Threads enthalten einen Stammbeitrag und eine Sammlung von Antwortbeiträgen.</span><span class="sxs-lookup"><span data-stu-id="afec7-107">Threads contain a root post and a collection of reply posts.</span></span> <span data-ttu-id="afec7-108">Im JavaScript-Objektmodell werden Feeds durch [SocialFeed]((http://msdn.microsoft.com/library/356c5475-2fd6-a655-c271-5d7f21af45e2%28Office.15%29.aspx))-Objekte dargestellt, Threads durch [SocialThread]((http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx))-Objekte und Beiträge und Antworten durch [SocialPost]((http://msdn.microsoft.com/library/a761ce71-d3d7-420a-1e06-962674124dfa%28Office.15%29.aspx))-Objekte.</span><span class="sxs-lookup"><span data-stu-id="afec7-108">In the JavaScript object model, feeds are represented by  [SocialFeed]((http://msdn.microsoft.com/library/356c5475-2fd6-a655-c271-5d7f21af45e2%28Office.15%29.aspx)) objects, threads are represented by [SocialThread]((http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx)) objects, and post and replies are represented by [SocialPost]((http://msdn.microsoft.com/library/a761ce71-d3d7-420a-1e06-962674124dfa%28Office.15%29.aspx)) objects.</span></span> <span data-ttu-id="afec7-109">Um wichtige Feed-bezogene Aufgaben auszuführen, verwenden Sie das [SocialFeedManager]((http://msdn.microsoft.com/library/651fdf0f-841d-88f9-1e07-fcb3ad8c9410%28Office.15%29.aspx))-Objekt.</span><span class="sxs-lookup"><span data-stu-id="afec7-109">To perform core feed-related tasks, you use the [SocialFeedManager]((http://msdn.microsoft.com/library/651fdf0f-841d-88f9-1e07-fcb3ad8c9410%28Office.15%29.aspx)) object.</span></span> <span data-ttu-id="afec7-110">In diesem Artikel wird gezeigt, wie Sie eine Anwendungsseite erstellen, die das JavaScript-Objektmodell zum Arbeiten mit sozialen Feeds verwendet.</span><span class="sxs-lookup"><span data-stu-id="afec7-110">In this article, we'll show you how to create an application page that uses the JavaScript object model to work with social feeds.</span></span>
  
    
    
<span data-ttu-id="afec7-111">For more information about working with  [SocialFeedManager]((http://msdn.microsoft.com/library/651fdf0f-841d-88f9-1e07-fcb3ad8c9410%28Office.15%29.aspx)) or for information about using other APIs to work with social feeds, see [Arbeiten mit sozialen Feeds in SharePoint](work-with-social-feeds-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="afec7-111">For more information about working with  [SocialFeedManager]((http://msdn.microsoft.com/library/651fdf0f-841d-88f9-1e07-fcb3ad8c9410%28Office.15%29.aspx)) or for information about using other APIs to work with social feeds, see [Work with social feeds in SharePoint](work-with-social-feeds-in-sharepoint.md).</span></span>
  
    
    

## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-social-feeds-in-the-sharepoint-javascript-object-model"></a><span data-ttu-id="afec7-112">Voraussetzungen für das Einrichten Ihrer Entwicklungsumgebung thematischer Feeds im Objektmodell von SharePoint JavaScript entwickelt</span><span class="sxs-lookup"><span data-stu-id="afec7-112">Prerequisites for setting up your development environment to work with social feeds in the SharePoint JavaScript object model</span></span>
<span data-ttu-id="afec7-113"><a name="bkmk_SetUpDevEnv"> </a></span><span class="sxs-lookup"><span data-stu-id="afec7-113"><a name="bkmk_SetUpDevEnv"> </a></span></span>

<span data-ttu-id="afec7-114">Um eine Anwendungsseite zu erstellen, die das JavaScript-Objektmodell zum Arbeiten mit sozialen Feeds verwendet, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="afec7-114">To create an application page that uses the JavaScript object model to work with social feeds, you'll need:</span></span>
  
    
    

- <span data-ttu-id="afec7-115">SharePoint mit Meine Website konfiguriert als öffentlich mit persönlichen Websites, die für den aktuellen Benutzer und einen Zielbenutzer erstellt, mit dem aktuellen Benutzer nach der Zielbenutzer und mit ein paar Beiträge, die von den Zielbenutzer geschrieben</span><span class="sxs-lookup"><span data-stu-id="afec7-115">SharePoint with My Site configured as public, with personal sites created for the current user and a target user, with the current user following the target user, and with a few posts written by the target user</span></span>
    
  
- <span data-ttu-id="afec7-116">Visual Studio 2012 oder Visual Studio 2013 mit Office Developer Tools für Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="afec7-116">Visual Studio 2012 or Visual Studio 2013 with Office Developer Tools for Visual Studio 2013</span></span>
    
  
- <span data-ttu-id="afec7-117">**Vollzugriff auf die Benutzerprofildienst-Anwendung und die Berechtigungen zum Bereitstellen einer Farmlösung des angemeldeten Benutzers**</span><span class="sxs-lookup"><span data-stu-id="afec7-117">**Full Control** access permissions to the User Profile service application and permissions to deploy a farm solution for the logged-on user</span></span>
    
  
- <span data-ttu-id="afec7-118">Über ausreichende Berechtigungen für das Anwendungspoolkonto greifen Sie auf die Inhaltsdatenbank von Meine Websites-Webanwendung</span><span class="sxs-lookup"><span data-stu-id="afec7-118">Sufficient permissions for the application pool account to access the content database of the My Sites web application</span></span>
    
  

## <a name="create-an-application-page-that-works-with-social-feeds-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="afec7-119">Erstellen einer Anwendungsseite, das mit sozialen Feeds mithilfe der SharePoint JavaScript-Objektmodells</span><span class="sxs-lookup"><span data-stu-id="afec7-119">Create an application page that works with social feeds by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="afec7-120"><a name="bk_CreateApp"> </a></span><span class="sxs-lookup"><span data-stu-id="afec7-120"><a name="bk_CreateApp"> </a></span></span>


1. <span data-ttu-id="afec7-121">Öffnen Sie Visual Studio, und wählen Sie **Datei**, **Neu**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="afec7-121">Open Visual Studio and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="afec7-122">Wählen Sie im Dialogfeld **Neues Projekt** aus der Dropdownliste oben im Dialogfeld die Option **.NET Framework 4.5**.</span><span class="sxs-lookup"><span data-stu-id="afec7-122">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="afec7-123">In der Liste der **Vorlagen** erweitern Sie **Office SharePoint**, wählen Sie die Kategorie **SharePoint-Lösungen** und wählen Sie dann die Vorlage **SharePoint-Projekts**.</span><span class="sxs-lookup"><span data-stu-id="afec7-123">In the **Templates** list, expand **Office SharePoint**, choose the **SharePoint Solutions** category, and then choose the **SharePoint Project** template.</span></span>
    
  
4. <span data-ttu-id="afec7-124">Nennen Sie das Projekt SocialFeedJSOM, und wählen Sie dann auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="afec7-124">Name the project SocialFeedJSOM, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="afec7-125">Klicken Sie im **Assistenten zum Anpassen von SharePoint**-Dialogfeld Wählen Sie **als Farmlösung bereitstellen**, und wählen Sie dann auf die Schaltfläche **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="afec7-125">In the **SharePoint Customization Wizard** dialog box, choose **Deploy as a farm solution**, and then choose the **Finish** button.</span></span>
    
  
6. <span data-ttu-id="afec7-126">Im **Projektmappen-Explorer** das Kontextmenü für das ProjektSocialFeedJSOM öffnen, und fügen Sie eine SharePoint "Layouts" Ordner zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="afec7-126">In **Solution Explorer**, open the shortcut menu for the SocialFeedJSOM project, and then add a SharePoint "Layouts" mapped folder.</span></span>
    
  
7. <span data-ttu-id="afec7-127">Öffnen Sie im Ordner **Layouts** das Kontextmenü für den Ordner „SocialFeedJSOM“, und fügen Sie anschließend eine neue SharePoint-Anwendungsseite mit dem Namen „SocialFeed.aspx“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="afec7-127">In the **Layouts** folder, open the shortcut menu for theSocialFeedJSOM folder, and then add a new SharePoint application page namedSocialFeed.aspx.</span></span>
    
  > <span data-ttu-id="afec7-128">Hinweis: Die Codebeispiele in diesem Artikel definieren benutzerdefinierten Code im Seitenmarkup, verwenden jedoch keine Code-Behind-Klasse, die Visual Studio für die Seite erstellt.</span><span class="sxs-lookup"><span data-stu-id="afec7-128">Note: The code examples in this article define custom code in the page markup but do not use the code-behind class that Visual Studio creates for the page.</span></span> 

8. <span data-ttu-id="afec7-129">Öffnen Sie das Kontextmenü für die Seite „SocialFeed.aspx“, und wählen Sie dann **Als Startelement festlegen** aus.</span><span class="sxs-lookup"><span data-stu-id="afec7-129">Open the shortcut menu for the SocialFeed.aspx page, and then choose **Set as Startup Item**.</span></span>
    
  
9. <span data-ttu-id="afec7-130">Definieren Sie im Markup für die Seite „SocialFeed.aspx“ die Steuerelemente innerhalb der **asp:Content**-Tags „Main“, wie im folgenden Code dargestellt.</span><span class="sxs-lookup"><span data-stu-id="afec7-130">In the markup for the SocialFeed.aspx page, define controls inside the "Main" **asp:Content** tags, as shown in the following code.</span></span>
    
```HTML
<table width="100%" id="tblPosts"></table><br/>
<button id="btnDelete" type="button"></button><br />
<span id="spanMessage" style="color: #FF0000;"></span>
```

  > <span data-ttu-id="afec7-131">Hinweis: Diese Steuerelemente können möglicherweise nicht in jedem Szenario verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="afec7-131">Note: These controls may not be used in every scenario.</span></span> <span data-ttu-id="afec7-132">Das Szenario „Beiträge und Antworten veröffentlichen“ verwendet beispielsweise nur das Steuerelement **span**.</span><span class="sxs-lookup"><span data-stu-id="afec7-132">For example, the "Publish posts and replies" scenario only uses the **span** control.</span></span>

10. <span data-ttu-id="afec7-p103">Nach dem schließenden **span** markieren, fügen Sie **SharePoint:ScriptLink** -Steuerelemente, ein Steuerelement **SharePoint:FormDigest** und **script** -Tags, wie im folgenden Code dargestellt. Die Tags **SharePoint:ScriptLink** verweisen auf die Bibliothek Klassendateien, die das Objektmodell JavaScript definieren, das Sie für die Entwicklung von Meine Website - soziale Netzwerke verwenden können. Das **SharePoint:FormDigest** -Tag generiert einen Nachrichtenhash für die Sicherheitsüberprüfung bei Bedarf von Operationen, die den Inhalt zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="afec7-p103">After the closing **span** tag, add **SharePoint:ScriptLink** controls, a **SharePoint:FormDigest** control, and **script** tags, as shown in the following code. The **SharePoint:ScriptLink** tags reference the class library files that define the JavaScript object model that you can use for My Site Social development. The **SharePoint:FormDigest** tag generates a message digest for security validation when required by operations that update server content.</span></span>
    
```HTML
<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" ondemand="false" localizable="false" loadafterui="true" />
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" ondemand="false" localizable="false" loadafterui="true" />
<SharePoint:FormDigest id="FormDigest" runat="server"/>
<script type="text/javascript">
    // Replace this comment with the code for your scenario.
</script>
```

11. <span data-ttu-id="afec7-136">Um die Logik für die Arbeit mit Feeds hinzuzufügen, ersetzen Sie den Kommentar zwischen den Tags **script** durch das Codebeispiel aus einem der folgenden Szenarien:</span><span class="sxs-lookup"><span data-stu-id="afec7-136">To add the logic to work with feeds, replace the comment between the **script** tags with the code example from one of the following scenarios:</span></span>
    
  -  [<span data-ttu-id="afec7-137">Veröffentlichen von Beiträgen und Antworten auf den Feed für soziale Netzwerke</span><span class="sxs-lookup"><span data-stu-id="afec7-137">Publish posts and replies to the social feed</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bkmk_PubPosts)
  -  [<span data-ttu-id="afec7-138">Abrufen von sozialen feeds</span><span class="sxs-lookup"><span data-stu-id="afec7-138">Retrieve social feeds</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bkmk_GetFeeds)
  -  [<span data-ttu-id="afec7-139">Delete-Beiträgen und Antworten aus dem sozialen feed</span><span class="sxs-lookup"><span data-stu-id="afec7-139">Delete posts and replies from the social feed</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bkmk_DeletePosts)
    
  
12. <span data-ttu-id="afec7-p104">Wählen Sie zum Testen der Anwendungsseite in der Menüleiste **Debuggen**, **Debuggen starten** aus. Wenn Sie aufgefordert werden, ändern Sie die Datei "Web.config", und wählen Sie die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="afec7-p104">To test the application page, on the menu bar, choose **Debug**, **Start Debugging**. If you are prompted to modify the web.config file, choose the **OK** button.</span></span>
    
  <span data-ttu-id="afec7-142">Wenn die Antwort die Ausfall Callback-Methode aufruft, legen Sie einen Haltepunkt in der Methode und fügen Sie eine Überwachung auf dem **args** -Objekt hinzu oder Überprüfen Sie die ULS-Protokolle und der Ereignisanzeige Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="afec7-142">If the response calls the failure callback method, set a breakpoint in the method and add a watch on the **args** object or check the ULS logs and the event viewer for more information.</span></span>
    
  

## <a name="code-example-publish-posts-and-replies-to-the-social-feed-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="afec7-143">Codebeispiel: Veröffentlichen von Beiträgen und Antworten auf die Nutzung von sozialen Netzwerken feed mithilfe der SharePoint JavaScript-Objektmodells</span><span class="sxs-lookup"><span data-stu-id="afec7-143">Code example: Publish posts and replies to the social feed by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="afec7-144"><a name="bkmk_PubPosts"> </a></span><span class="sxs-lookup"><span data-stu-id="afec7-144"><a name="bkmk_PubPosts"> </a></span></span>

<span data-ttu-id="afec7-p105">Im folgenden Codebeispiel wird veröffentlicht ein Beitrag und einer Antwort. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="afec7-p105">The following code example publishes a post and a reply. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="afec7-p106">Definieren Sie nach Inhalt. Dieses Beispiel enthält einen Link in der POST-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="afec7-p106">Define post content. This example includes a link in the post.</span></span>
    
  
- <span data-ttu-id="afec7-149">Veröffentlichen Sie einen Post-Feed des aktuellen Benutzers mithilfe der **createPost** -Methode und übergeben **null** als _targetId_ -Parameter.</span><span class="sxs-lookup"><span data-stu-id="afec7-149">Publish a post to the current user's feed by using the **createPost** method and passing **null** as the _targetId_ parameter.</span></span>
    
  
- <span data-ttu-id="afec7-150">Antworten Sie auf einen Beitrag, indem Sie die **createPost**-Methode verwenden und die Thread-ID als _targetId_-Parameter übergeben.</span><span class="sxs-lookup"><span data-stu-id="afec7-150">Reply to a post by using the **createPost** method and passing the thread identifier as the _targetId_ parameter.</span></span>
    
> [!NOTE]
> <span data-ttu-id="afec7-151">Fügen Sie den folgenden Code zwischen den **script**-Tags ein, die Sie in der Prozedur [Erstellen der Anwendungsseite](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bk_CreateApp) hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="afec7-151">**Note:** Paste the following code between the [script](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bk_CreateApp) tags that you added in the Create the application page procedure.</span></span>
  
    
    


```javascript
// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs.
SP.SOD.executeOrDelayUntilScriptLoaded(PublishPost, 'SP.UserProfiles.js');

// Declare global variables.
var clientContext;
var feedManager;
var resultThread;

function PublishPost() {

    // Initialize the current client context and the SocialFeedManager instance.
    clientContext = SP.ClientContext.get_current();
    feedManager = new SP.Social.SocialFeedManager(clientContext);

    // Create a link to include in the post.
    var linkDataItem = new SP.Social.SocialDataItem();
    linkDataItem.set_itemType(SP.Social.SocialDataItemType.link);
    linkDataItem.set_text('link');
    linkDataItem.set_uri('http://bing.com');
    var socialDataItems = [ linkDataItem ];

    // Create the post content.
    var postCreationData = new SP.Social.SocialPostCreationData();
    postCreationData.set_contentText('The text for the post, which contains a {0}.');
    postCreationData.set_contentItems(socialDataItems);

    // Publish the post. Pass null for the "targetId" parameter because this is a root post.
    resultThread = feedManager.createPost(null, postCreationData);
    clientContext.executeQueryAsync(PublishReply, PostFailed);
    }
function PublishReply(sender, args) {

    // Create the reply content.
    var postCreationData = new SP.Social.SocialPostCreationData();
    postCreationData.set_contentText('The text for the reply.');

    // Publish the reply.
    resultThread = feedManager.createPost(resultThread.get_id(), postCreationData);
    clientContext.executeQueryAsync(PostSucceeded, PostFailed);
}
function PostSucceeded(sender, args) {
    $get("spanMessage").innerText = 'The post and reply were published.';
}
function PostFailed(sender, args) {
    $get("spanMessage").innerText = 'Request failed: ' + args.get_message();
}
```


## <a name="code-example-retrieve-social-feeds-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="afec7-152">Codebeispiel: Abrufen von sozialen Feeds mithilfe des SharePoint-JavaScript-Objektmodells</span><span class="sxs-lookup"><span data-stu-id="afec7-152">Code example: Retrieve social feeds by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="afec7-153"><a name="bkmk_GetFeeds"> </a></span><span class="sxs-lookup"><span data-stu-id="afec7-153"><a name="bkmk_GetFeeds"> </a></span></span>

<span data-ttu-id="afec7-p107">Im folgenden Codebeispiel werden die Feeds für den aktuellen Benutzer und einen Zielbenutzer abgerufen. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="afec7-p107">The following code example retrieves feeds for the current user and a target user. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="afec7-156">Rufen Sie die **Personal**, **News**und **Timeline** feed Typen für den aktuellen Benutzer mithilfe der **getFeed** -Methode.</span><span class="sxs-lookup"><span data-stu-id="afec7-156">Get the **Personal**, **News**, and **Timeline** feed types for the current user by using the **getFeed** method.</span></span>
    
  
- <span data-ttu-id="afec7-157">Rufen Sie die **Personal** feed Typ für einen Zielbenutzer mithilfe der **getFeedFor** -Methode.</span><span class="sxs-lookup"><span data-stu-id="afec7-157">Get the **Personal** feed type for a target user by using the **getFeedFor** method.</span></span>
    
  
- <span data-ttu-id="afec7-p108">Durchlaufen Sie die Feeds, um alle Threads im nicht-Verweis zu suchen und Abrufen von Informationen zu Threads und Beiträge. Verweis Threads darstellen Benachrichtigungen, die Informationen zu einem anderen Thread enthalten. Wenn ein Benutzer eine Person in einem Beitrag erwähnt wird, generiert der Server beispielsweise ein **MentionReference**-Thread, der den Link zur ursprünglichen Beitrags und andere Metadaten zu dem Beitrag enthält geben.</span><span class="sxs-lookup"><span data-stu-id="afec7-p108">Iterate through the feeds to find all non-reference threads and to get information about threads and posts. Reference threads represent notifications that contain information about another thread. For example, if a user mentions someone in a post, the server generates a **MentionReference**-type thread that contains the link to the original post and other metadata about the post.</span></span>
    
  
<span data-ttu-id="afec7-161">Weitere Informationen zu Feedtypen finden Sie unter [Übersicht über Feedtypen in der Meine Website-API](work-with-social-feeds-in-sharepoint.md#bkmk_FeedTypes).</span><span class="sxs-lookup"><span data-stu-id="afec7-161">For more information about feed types, see  [Overview of feed types in the My Site Social API](work-with-social-feeds-in-sharepoint.md#bkmk_FeedTypes).</span></span> <span data-ttu-id="afec7-162">Weitere Informationen zu Referenzthreads finden Sie unter [Referenzthreads und Digest-Threads in sozialen Feeds für SharePoint](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="afec7-162">For more information about reference threads, see  [Reference threads and digest threads in SharePoint social feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span></span>
  
> [!NOTE]
> <span data-ttu-id="afec7-163">Fügen Sie den folgenden Code zwischen den **script**-Tags ein, die Sie in der Prozedur [Erstellen der Anwendungsseite](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bk_CreateApp) hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="afec7-163">Note: Paste the following code between the **script** tags that you added in the [Create the application page](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bk_CreateApp) procedure.</span></span> <span data-ttu-id="afec7-164">Ändern Sie dann den Platzhalterwert für die Variable **targetUser**, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="afec7-164">Then, change the placeholder value for the **targetUser** variable before you run the code.</span></span>
  
    
    




```cs
// Replace the placeholder value with the account name of the target user.
var targetUser = 'domainName\\\\userName';

// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs.
SP.SOD.executeOrDelayUntilScriptLoaded(GetFeeds, 'SP.UserProfiles.js');

// Declare global variables.
var clientContext;
var feedManager;
var personalFeed;
var newsFeed;
var timelineFeed;
var targetUserFeed;

function GetFeeds() {

    // Initialize the current client context and the SocialFeedManager instance.
    clientContext = SP.ClientContext.get_current();
    feedManager = new SP.Social.SocialFeedManager(clientContext);

    // Set parameters for the feed content that you want to retrieve.
    var feedOptions = new SP.Social.SocialFeedOptions();
    feedOptions.set_maxThreadCount(10); // default is 20

    // Get all feed types for current user and get the Personal feed
    // for the target user.
    personalFeed = feedManager.getFeed(SP.Social.SocialFeedType.personal, feedOptions);
    newsFeed = feedManager.getFeed(SP.Social.SocialFeedType.news, feedOptions);
    targetUserFeed = feedManager.getFeedFor(targetUser, feedOptions);

    // Change the sort order to optimize the Timeline feed results.
    feedOptions.set_sortOrder(SP.Social.SocialFeedSortOrder.byCreatedTime); 
    timelineFeed = feedManager.getFeed(SP.Social.SocialFeedType.timeline, feedOptions);

    clientContext.load(feedManager);
    clientContext.executeQueryAsync(CallIterateFunctionForFeeds, RequestFailed);
}
function CallIterateFunctionForFeeds() {
    IterateThroughFeed(personalFeed, "Personal", true);
    IterateThroughFeed(newsFeed, "News", true);
    IterateThroughFeed(timelineFeed, "Timeline", true); 
    IterateThroughFeed(targetUserFeed, "Personal", false);
}
function IterateThroughFeed(feed, feedType, isCurrentUser) {
    tblPosts.insertRow().insertCell();
    var feedHeaderRow = tblPosts.insertRow();
    var feedOwner = feedManager.get_owner().get_name();

    // Iterate through the array of threads in the feed.
    var threads = feed.get_threads();
    for (var i = 0; i < threads.length ; i++) {
        var thread = threads[i];
        var actors = thread.get_actors();

        if (i == 0) {

            // Get the name of the target user for the feed header row. Users are 
            // owners of all threads in their Personal feed.
            if (!isCurrentUser) {
                feedOwner = actors[thread.get_ownerIndex()].get_name();
            }
            feedHeaderRow.insertCell().innerText = feedType.toUpperCase() + ' FEED FOR '
                + feedOwner.toUpperCase();
        }

        // Use only Normal-type threads and ignore reference-type threads. (SocialThreadType.Normal = 0)
        if (thread.get_threadType() == 0) {

            // Get the root post's author, content, and number of replies.
            var post = thread.get_rootPost();
            var authorName = actors[post.get_authorIndex()].get_name();
            var postContent = post.get_text();
            var totalReplies = thread.get_totalReplyCount();

            var postRow = tblPosts.insertRow();
            postRow.insertCell().innerText = authorName + ' posted \\"' + postContent
                + '\\" (' + totalReplies + ' replies)';

            // If there are any replies, iterate through the array and
            // get the author and content. 
            // If a thread contains more than two replies, the server
            // returns a thread digest that contains only the two most
            // recent replies. To get all replies, call the 
            // SocialFeedManager.getFullThread method.
            if (totalReplies > 0) {
                var replies = thread.get_replies();

                for (var j = 0; j < replies.length; j++) {
                    var replyRow = tblPosts.insertRow();

                    var reply = replies[j];
                    replyRow.insertCell().innerText = '  - ' + actors[reply.get_authorIndex()].get_name()
                        + ' replied \\"' + reply.get_text() + '\\"';
                }
            }
        }
    }
}
function RequestFailed(sender, args) {
    $get("spanMessage").innerText = 'Request failed: ' + args.get_message();
}
```


## <a name="code-example-delete-posts-and-replies-from-the-social-feed-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="afec7-165">Codebeispiel: Löschen von Beiträgen und Antworten aus dem sozialen Feed mithilfe des SharePoint-JavaScript-Objektmodells</span><span class="sxs-lookup"><span data-stu-id="afec7-165">Code example: Delete posts and replies from the social feed by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="afec7-166"><a name="bkmk_DeletePosts"> </a></span><span class="sxs-lookup"><span data-stu-id="afec7-166"><a name="bkmk_DeletePosts"> </a></span></span>

<span data-ttu-id="afec7-p111">Im folgenden Codebeispiel wird Löscht ein Beitrag oder eine Antwort. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="afec7-p111">The following code example deletes a post or a reply. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="afec7-169">Rufen Sie die **News** feed Typ für den aktuellen Benutzer mithilfe der **getFeed** -Methode.</span><span class="sxs-lookup"><span data-stu-id="afec7-169">Get the **News** feed type for the current user by using the **getFeed** method.</span></span>
    
  
- <span data-ttu-id="afec7-170">Durchlaufen Sie die Beiträge und Antworten in den Feed zum Abrufen der **id** -Eigenschaft, mit denen Sie die Beitrag oder eine Antwort zu löschen.</span><span class="sxs-lookup"><span data-stu-id="afec7-170">Iterate through the posts and replies in the feed to get the **id** property that you use to delete the post or reply.</span></span>
    
  
- <span data-ttu-id="afec7-171">Löschen Sie einen Stammbeitrag oder eine Antwort mithilfe der **deletePost**-Methode (durch Löschen eines Stammbeitrags wird der gesamte Thread gelöscht).</span><span class="sxs-lookup"><span data-stu-id="afec7-171">Delete a root post or reply by using the **deletePost** method (deleting a root post deletes the whole thread).</span></span>
    
> [!NOTE]
> <span data-ttu-id="afec7-172">Fügen Sie den folgenden Code zwischen den **script**-Tags ein, die Sie in der Prozedur [Erstellen der Anwendungsseite](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bk_CreateApp) hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="afec7-172">Note: Paste the following code between the **script** tags that you added in the [Create the application page](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bk_CreateApp) procedure.</span></span> <span data-ttu-id="afec7-173">In diesem Beispiel wird vorausgesetzt, dass der Newsfeed des aktuellen Benutzers mindestens einen Beitrag enthält.</span><span class="sxs-lookup"><span data-stu-id="afec7-173">This example assumes that the current user's newsfeed contains at least one post.</span></span>
  
    
    


```cs
// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs.
SP.SOD.executeOrDelayUntilScriptLoaded(GetFeeds, 'SP.UserProfiles.js');

// Declare global variables.
var clientContext;
var feedManager;
var feed;
var postOrReplyToDelete;

function GetFeeds() {

    // Initialize the current client context and the SocialFeedManager instance.
    clientContext = SP.ClientContext.get_current();
    feedManager = new SP.Social.SocialFeedManager(clientContext);

    // Set parameters for the feed content that you want to retrieve.
    var feedOptions = new SP.Social.SocialFeedOptions();
    feedOptions.set_maxThreadCount(10); // default is 20

    // Get all the News feed type for current user.
    feed = feedManager.getFeed(SP.Social.SocialFeedType.news, feedOptions);
    clientContext.executeQueryAsync(IterateThroughFeed, RequestFailed);
}
function IterateThroughFeed() {

    // Iterate through the array of threads in the feed.
    var threads = feed.get_threads();
    for (var i = 0; i < threads.length ; i++) {
        var thread = threads[i];
        var actors = thread.get_actors();

        // Get the root post's author, content, and number of replies.
        var post = thread.get_rootPost();

        var authorName = actors[post.get_authorIndex()].get_name();
        var postContent = post.get_text();
        var totalReplies = thread.get_totalReplyCount();

        var postRow = tblPosts.insertRow();
        postRow.insertCell().innerText = authorName + ' posted \\"' + postContent
            + '\\" (' + totalReplies + ' replies)';
        postOrReplyToDelete = post.get_id();

        // If there are any replies, iterate through the array and
        // get the author and content.
            // If a thread contains more than two replies, the server
            // returns a thread digest that contains only the two most
            // recent replies. To get all replies, call the 
            // SocialFeedManager.getFullThread method.
        if (totalReplies > 0) {
            var replies = thread.get_replies();
            for (var j = 0; j < replies.length; j++) {
                var replyRow = tblPosts.insertRow();

                var reply = replies[j];
                replyRow.insertCell().innerText = '  - ' + actors[reply.get_authorIndex()].get_name()
                    + ' replied \\"' + reply.get_text() + '\\"';
                postOrReplyToDelete = reply.get_id();
            }
        }

        // Initialize button properties.
        $get("btnDelete").onclick = function () { DeletePostOrReply(); };
        $get("btnDelete").innerText = 'Click to delete the last post or reply';
    }
}

// Delete the last post or reply listed on the page.
function DeletePostOrReply() {
    feedManager.deletePost(postOrReplyToDelete);
    clientContext.executeQueryAsync(DeleteSucceeded, RequestFailed);
}
function DeleteSucceeded(sender, args) {
    $get("spanMessage").innerText = 'The post or reply was deleted. Refresh the page to see your changes.';
}
function RequestFailed(sender, args) {
    $get("spanMessage").innerText = 'Request failed: ' + args.get_message();
}
```


## <a name="see-also"></a><span data-ttu-id="afec7-174">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="afec7-174">See also</span></span>
<span data-ttu-id="afec7-175"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="afec7-175"><a name="bk_addResources"> </a></span></span>


-  [<span data-ttu-id="afec7-176">Arbeiten mit sozialen Feeds in SharePoint</span><span class="sxs-lookup"><span data-stu-id="afec7-176">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  
-  <span data-ttu-id="afec7-177">[SP. Social-Namespace (sp.userprofiles)]((http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx))</span><span class="sxs-lookup"><span data-stu-id="afec7-177">[SP.Social namespace (sp.userprofiles)]((http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx))</span></span>
    
  
-  [<span data-ttu-id="afec7-178">Vorgehensweise: Erstellen und Löschen von Beiträge und Abrufen des für soziale Netzwerke-Feed mithilfe des clientobjektmodells .NET SharePoint</span><span class="sxs-lookup"><span data-stu-id="afec7-178">How to: Create and delete posts and retrieve the social feed by using the .NET client object model in SharePoint</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md)
    
  
-  [<span data-ttu-id="afec7-179">Vorgehensweise: Lesen und Schreiben des sozialen Feeds mithilfe des REST-Diensts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="afec7-179">How to: Learn to read and write to the social feed by using the REST service in SharePoint</span></span>](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)
    
  
-  [<span data-ttu-id="afec7-180">Referenzthreads und Digest-Threads in sozialen Feeds für SharePoint</span><span class="sxs-lookup"><span data-stu-id="afec7-180">Reference threads and digest threads in SharePoint social feeds</span></span>](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md)
    
  

