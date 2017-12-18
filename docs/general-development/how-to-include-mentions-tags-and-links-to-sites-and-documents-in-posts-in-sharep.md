---
title: "Einschließen von Erwähnungen, Tags und Links zu Websites und Dokumenten in Beiträgen in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 975da333-372b-4bf6-a3f4-7452db369f04
ms.openlocfilehash: f0af1c97baf6da530358f2a2ff86f29e2f9bb03e
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharepoint"></a><span data-ttu-id="df658-102">Einschließen von Erwähnungen, Tags und Links zu Websites und Dokumenten in Beiträgen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="df658-102">How to: Include mentions, tags, and links to sites and documents in posts in SharePoint</span></span>

<span data-ttu-id="df658-103">In diesem Artikel erfahren Sie, wie Sie Mikroblogbeiträgen [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx)-Objekte hinzufügen, die als Erwähnungen, Tags oder Links in sozialen Feeds für SharePoint gerendert werden.</span><span class="sxs-lookup"><span data-stu-id="df658-103">Learn how to add  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) objects to microblog posts, which render as mentions, tags, or links in SharePoint social feeds.</span></span>
<span data-ttu-id="df658-104">Die einfachste Form von Beitragsinhalten in sozialen Feeds enthält nur Text, aber Sie können auch Links hinzufügen, die als Erwähnungen, Tags oder Links zu Websites, SharePoint-Websites und Dokumenten gerendert werden.</span><span class="sxs-lookup"><span data-stu-id="df658-104">In a social feed, the simplest form of post content contains only text, but you can also add links that render as mentions, tags, or links to websites, SharePoint sites, and documents.</span></span> <span data-ttu-id="df658-105">Zu diesem Zweck fügen Sie [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx)-Objekte zur [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx)-Eigenschaft des [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx)-Objekts hinzu, das den Beitrag definiert.</span><span class="sxs-lookup"><span data-stu-id="df658-105">To do this, you add  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) objects to the [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) property of the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that defines the post.</span></span> <span data-ttu-id="df658-106">Beiträge können mehrere Links enthalten.</span><span class="sxs-lookup"><span data-stu-id="df658-106">Posts can contain multiple links.</span></span>
  
    
    


> <span data-ttu-id="df658-107">**Hinweis:** Um eingebettete Bilder, Videos oder Dokumente zum Inhalt eines Beitrags hinzuzufügen, fügen Sie ein [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx)-Objekt zur [SocialPostCreationData.Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx)-Eigenschaft hinzu.</span><span class="sxs-lookup"><span data-stu-id="df658-107">**Note:** To add embedded pictures, videos, or documents to a post's content, you add a  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) object to the [SocialPostCreationData.Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) property.</span></span> <span data-ttu-id="df658-108">Weitere Informationen finden Sie unter [Vorgehensweise: Einbetten von Bildern, Videos und Dokumenten in Beiträgen in SharePoint](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md).</span><span class="sxs-lookup"><span data-stu-id="df658-108">For more information, see [How to: Embed images, videos, and documents in posts in SharePoint](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md).</span></span> 
  
    
    


<span data-ttu-id="df658-p103">Die in diesem Artikel beschriebene API hat ihren Ursprung des Clientobjektmodells .NET. Jedoch, wenn Sie eine andere API verwenden, möglicherweise wie die JavaScript-Objektmodell, den zu verwendenden Objektnamen oder die dazugehörige API abweichen. Links zur Dokumentation für verwandte APIs finden Sie unter  [Zusätzliche Ressourcen](#bk_addresources) .</span><span class="sxs-lookup"><span data-stu-id="df658-p103">The API described in this article is from the .NET client object model. However, if you're using another API, such as the JavaScript object model, the object names or corresponding API might be different. See  [Additional resources](#bk_addresources) for links to documentation for related APIs.</span></span>
  
    
    


## <a name="prerequisites-for-using-the-code-examples-to-add-links-to-a-post-in-sharepoint"></a><span data-ttu-id="df658-112">Voraussetzungen für die Verwendung der Codebeispiele zum Hinzufügen von Links zu einem Beitrag in SharePoint</span><span class="sxs-lookup"><span data-stu-id="df658-112">Prerequisites for using the code examples to add links to a post in SharePoint</span></span>
<span data-ttu-id="df658-113"><a name="bk_preReqs"> </a></span><span class="sxs-lookup"><span data-stu-id="df658-113"><a name="bk_preReqs"> </a></span></span>

<span data-ttu-id="df658-p104">Die Codebeispiele in diesem Artikel zeigen, wie Links Microblog Beiträge hinzugefügt. In diesen Beispielen werden von konsolenanwendungen, die die folgenden SharePoint-Assemblys verwenden:</span><span class="sxs-lookup"><span data-stu-id="df658-p104">The code examples in this article show how to add links to microblog posts. These examples are from console applications that use the following SharePoint assemblies:</span></span>
  
    
    

- <span data-ttu-id="df658-116">Microsoft.SharePoint.Client</span><span class="sxs-lookup"><span data-stu-id="df658-116">Microsoft.SharePoint.Client</span></span>
    
  
- <span data-ttu-id="df658-117">Microsoft.SharePoint.Client.Runtime</span><span class="sxs-lookup"><span data-stu-id="df658-117">Microsoft.SharePoint.Client.Runtime</span></span>
    
  
- <span data-ttu-id="df658-118">Microsoft.SharePoint.Client.UserProfilies</span><span class="sxs-lookup"><span data-stu-id="df658-118">Microsoft.SharePoint.Client.UserProfilies</span></span>
    
  
<span data-ttu-id="df658-119">Weitere Informationen zum Einrichten Ihrer Entwicklungsumgebung und Erstellen einer Konsolenanwendung finden Sie unter  [Vorgehensweise: Erstellen und Löschen von Beiträge und Abrufen des für soziale Netzwerke-Feed mithilfe des clientobjektmodells .NET SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md).</span><span class="sxs-lookup"><span data-stu-id="df658-119">For instructions about how to set up your development environment and create a console application, see  [How to: Create and delete posts and retrieve the social feed by using the .NET client object model in SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md).</span></span>
  
    
    

## <a name="example-include-links-to-websites-sharepoint-sites-and-documents-in-a-post-in-sharepoint"></a><span data-ttu-id="df658-120">Beispiel: Einschließen von Links zu Websites, SharePoint-Websites und Dokumenten in einem Beitrag in SharePoint</span><span class="sxs-lookup"><span data-stu-id="df658-120">Example: Include links to websites, SharePoint sites, and documents in a post in SharePoint</span></span>
<span data-ttu-id="df658-121"><a name="bkmk_addLinks"> </a></span><span class="sxs-lookup"><span data-stu-id="df658-121"><a name="bkmk_addLinks"> </a></span></span>

<span data-ttu-id="df658-p105">Im folgenden Codebeispiel wird veröffentlicht einen Beitrag, der Links zu einer Website und einer SharePoint-Website zu einem Dokument enthält. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="df658-p105">The following code example publishes a post that contains links to a website, a SharePoint site, and a document. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="df658-p106">Erstellen Sie  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) -Objekten, die Links darstellen. Jede Instanz wird das Feld [SocialDataItemType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.aspx) für den Link, der Anzeigetext für den Link, und den Link URI festgelegt.</span><span class="sxs-lookup"><span data-stu-id="df658-p106">Create  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) objects that represent the links. Each instance sets the [SocialDataItemType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.aspx) field for the link type, the display text for the link, and the link URI.</span></span>
    
  
- <span data-ttu-id="df658-126">Hinzufügen von Platzhaltern für den Post-Text um anzugeben, wo Anzeigetext für den Link angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="df658-126">Add placeholders to the post text to indicate where the link's display text should appear.</span></span>
    
  
- <span data-ttu-id="df658-127">Fügen Sie die Linkobjekte zur [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx)-Eigenschaft des [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx)-Objekts hinzu, das zum Erstellen des Beitrags verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="df658-127">Add the link objects to the  [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) property of the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that's used to create the post.</span></span>
    
  

> <span data-ttu-id="df658-128">**Hinweis:** Derzeit werden in SharePoint Links zu Websites, SharePoint-Websites und Dokumenten gleich behandelt. Es empfiehlt sich jedoch, für SharePoint-Websites und Dokumente die Typen [Site](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Site.aspx) und [Document](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Document.aspx) zu wählen.</span><span class="sxs-lookup"><span data-stu-id="df658-128">**Note:** Currently, SharePoint handles links to websites, SharePoint sites, and documents in the same way, but as a best practice, choose the  [Site](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Site.aspx) type and the [Document](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Document.aspx) type for SharePoint sites and documents.</span></span>
  
    
    

<span data-ttu-id="df658-129">Wenn Sie im sozialen Feed auf einen Link zu einer Website, einer SharePoint-Website oder einem Dokument klicken, wird das Element in einem separaten Browserfenster geöffnet.</span><span class="sxs-lookup"><span data-stu-id="df658-129">In the social feed, clicking a link to a website, SharePoint site, or document opens the item in a separate browser window.</span></span>
  
    
    

> <span data-ttu-id="df658-130">**Hinweis:** Ändern Sie die Platzhalterwerte für die URL-Variablen vor dem Ausführen des Codes.</span><span class="sxs-lookup"><span data-stu-id="df658-130">**Note:** Change the placeholder values for the URL variables before you run the code.</span></span> 
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace IncludeLinksInPost
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the actual values.
            const string serverUrl = "http://serverName/siteName/";
            const string websiteLinkUrl = "http://bing.com";
            const string siteLinkUrl = "http://serverName/siteName/";
            const string docLinkUrl = "http://serverName/Shared%20Documents/docName.txt";

            // Define the link to a website that you want to include in the post.
            SocialDataItem websiteLink = new SocialDataItem
            {
                ItemType = SocialDataItemType.Link,
                Text = "link to a website",
                Uri = websiteLinkUrl
            };

            // Define the link to a SharePoint site that you want to include in the post.
            SocialDataItem siteLink = new SocialDataItem
            {
                ItemType = SocialDataItemType.Site,
                Text = "link to a SharePoint site",
                Uri = siteLinkUrl
            };

            // Define the link to a document that you want to include in the post.
            SocialDataItem docLink = new SocialDataItem
            {
                ItemType = SocialDataItemType.Document,
                Text = "link to a document",
                Uri = docLinkUrl
            };

            // Add the links to the post's creation data.
            // Put placeholders ({n}) where you want the links to appear in the post text,
            // and then add the links to the post's content items.
            SocialPostCreationData postCreationData = new SocialPostCreationData();
            postCreationData.ContentText = "Check out this {0}, {1}, and {2}.";
            postCreationData.ContentItems = new SocialDataItem[3] { 
                    websiteLink, 
                    siteLink, 
                    docLink 
                };
            try
            {

                // Get the context and the SocialFeedManager instance.
                ClientContext clientContext = new ClientContext(serverUrl);
                SocialFeedManager feedManager = new SocialFeedManager(clientContext);

                // Publish the post. This is a root post to the user's feed, so specify
                // null for the targetId parameter.
                feedManager.CreatePost(null, postCreationData);
                clientContext.ExecuteQuery();
                Console.Write("The post was published.");
                Console.ReadLine();
            }
            catch (Exception ex)
            {
                Console.Write("Error publishing the post: " + ex.Message);
                Console.ReadLine();
            }
        }
    }
}

```


## <a name="example-mention-someone-in-a-post-in-sharepoint"></a><span data-ttu-id="df658-131">Beispiel: Erwähnen einer Person in einem Beitrag in SharePoint</span><span class="sxs-lookup"><span data-stu-id="df658-131">Example: Mention someone in a post in SharePoint</span></span>
<span data-ttu-id="df658-132"><a name="bkmk_addMention"> </a></span><span class="sxs-lookup"><span data-stu-id="df658-132"><a name="bkmk_addMention"> </a></span></span>

<span data-ttu-id="df658-p107">Im folgenden Codebeispiel wird veröffentlicht einen Beitrag, der einen Benutzer erwähnt. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="df658-p107">The following code example publishes a post that mentions a user. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="df658-p108">Erstellen Sie ein  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) -Objekt, um einen Vermerk darstellen, der eine Verknüpfung zu einem Benutzer ist. Die [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) gibt das [SocialDataItemType.User](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.User.aspx) -Feld und die weiter oben erwähnt Person Kontonamen. Sie können den Kontonamen mithilfe der Anmeldename der Person oder e-Mail-Adresse festlegen.</span><span class="sxs-lookup"><span data-stu-id="df658-p108">Create a  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) object to represent a mention, which is a link to a user. The [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) specifies the [SocialDataItemType.User](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.User.aspx) field and the mentioned person's account name. You can set the account name by using either the person's login or email address.</span></span>
    
  
- <span data-ttu-id="df658-138">Hinzufügen eines Platzhalters für den Post-Text um anzugeben, wo der weiter oben erwähnt Person Anzeigename angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="df658-138">Add a placeholder to the post text to indicate where the mentioned person's display name should appear.</span></span>
    
  
- <span data-ttu-id="df658-139">Fügen Sie der  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) der [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) -Eigenschaft des [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) -Objekts, das zum Erstellen der POST-Anforderung verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="df658-139">Add the  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) to the [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) property of the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that's used to create the post.</span></span>
    
  
<span data-ttu-id="df658-140">Wenn Sie in einem sozialen Feed auf eine Erwähnung klicken, werden Sie auf die **Info**-Seite der erwähnten Person umgeleitet.</span><span class="sxs-lookup"><span data-stu-id="df658-140">In the social feed, clicking a mention redirects to the mentioned person's **About** page.</span></span>
  
    
    

> <span data-ttu-id="df658-141">**Hinweis:** Ändern Sie die Platzhalterwerte für die Variablen **serverURL** und **accountName** vor dem Ausführen des Codes.</span><span class="sxs-lookup"><span data-stu-id="df658-141">**Note:** Change the placeholder values for the **serverURL** and **accountName** variables before you run the code.</span></span>
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace IncludeMentionInPost
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the actual values.
            const string serverUrl = "http://serverName/siteName/";
            const string accountName = @"domain\\name or email address";

            // Define the mention link that you want to include in the post.
            SocialDataItem userMentionLink = new SocialDataItem
            {
                ItemType = SocialDataItemType.User,
                AccountName = accountName
            };

            // Add the mention to the post's creation data.
            // Put a placeholder ({0}) where you want the mention to appear in the post text,
            // and then add the mention to the post's content items.
            SocialPostCreationData postCreationData = new SocialPostCreationData();
            postCreationData.ContentText = "{0} does great work!";
            postCreationData.ContentItems = new SocialDataItem[1] { userMentionLink, };

            try
            {

                // Get the context and the SocialFeedManager instance.
                ClientContext clientContext = new ClientContext(serverUrl);
                SocialFeedManager feedManager = new SocialFeedManager(clientContext);

                // Publish the post. This is a root post to the user's feed, so specify
                // null for the targetId parameter.
                feedManager.CreatePost(null, postCreationData);
                clientContext.ExecuteQuery();
                Console.Write("The post was published.");
                Console.ReadLine();
            }
            catch (Exception ex)
            {
                Console.Write("Error publishing the post: " + ex.Message);
                Console.ReadLine();
            }
        }
    }
}

```


## <a name="example-include-a-tag-in-a-post-in-sharepoint"></a><span data-ttu-id="df658-142">Beispiel: Einschließen eines Tags in einem Beitrag in SharePoint</span><span class="sxs-lookup"><span data-stu-id="df658-142">Example: Include a tag in a post in SharePoint</span></span>
<span data-ttu-id="df658-143"><a name="bkmk_addTag"> </a></span><span class="sxs-lookup"><span data-stu-id="df658-143"><a name="bkmk_addTag"> </a></span></span>

<span data-ttu-id="df658-p109">Im folgenden Codebeispiel wird veröffentlicht einen Beitrag, der ein Tag enthält. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="df658-p109">The following code example publishes a post that includes a tag. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="df658-p110">Erstellen Sie ein  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) -Objekt, um das Tag darstellen. Die [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) gibt das Feld [SocialDataItemType.Tag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Tag.aspx) und der Tagname, die ein **#** Zeichen enthalten muss.</span><span class="sxs-lookup"><span data-stu-id="df658-p110">Create a  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) object to represent the tag. The [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) specifies the [SocialDataItemType.Tag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Tag.aspx) field and the tag name, which must include a **#** character.</span></span>
    
  
- <span data-ttu-id="df658-148">Hinzufügen eines Platzhalters für den Post-Text um anzugeben, wo das Tag angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="df658-148">Add a placeholder to the post text to indicate where the tag should appear.</span></span>
    
  
- <span data-ttu-id="df658-149">Fügen Sie der  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) der [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) -Eigenschaft des [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) -Objekts, das zum Erstellen der POST-Anforderung verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="df658-149">Add the  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) to the [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) property of the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that's used to create the post.</span></span>
    
  
<span data-ttu-id="df658-p111">Wenn Sie im sozialen Feed auf ein Tag klicken, werden Sie zur **Info**-Seite des Tags umgeleitet. Wenn das Tag noch nicht vorhanden ist, wird es vom Server erstellt.</span><span class="sxs-lookup"><span data-stu-id="df658-p111">In the social feed, clicking a tag redirects to the tag's **About** page. If the tag doesn't already exist, the server creates it.</span></span>
  
    
    

> <span data-ttu-id="df658-152">**Hinweis:** Ändern Sie die Platzhalterwerte für die Variablen **serverURL** und **tagName** vor dem Ausführen des Codes.</span><span class="sxs-lookup"><span data-stu-id="df658-152">**Note:** Change the placeholder values for the **serverURL** and **tagName** variables before you run the code.</span></span>
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace IncludeTagInPost
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the actual values.
            const string serverUrl = "http://serverName/siteName/";
            const string tagName = "#" + "tagName";

            // Define the link to a tag that you want to include in the post. If the tag is new, the
            // server adds it to the tags collection.
            SocialDataItem tagLink = new SocialDataItem
            {
                ItemType = SocialDataItemType.Tag,
                Text = tagName
            };

            // Add the tag to the post's creation data.
            // Put a placeholder ({0}) where you want the tag to appear in the post text,
            // and then add the tag to the post's content items.
            SocialPostCreationData postCreationData = new SocialPostCreationData();
            postCreationData.ContentText = "I like {0}.";
            postCreationData.ContentItems = new SocialDataItem[1] { tagLink };

            try
            {

                // Get the context and the SocialFeedManager instance.
                ClientContext clientContext = new ClientContext(serverUrl);
                SocialFeedManager feedManager = new SocialFeedManager(clientContext);

                // Publish the post. This is a root post to the user's feed, so specify
                // null for the targetId parameter.
                feedManager.CreatePost(null, postCreationData);
                clientContext.ExecuteQuery();
                Console.Write("The post was published.");
                Console.ReadLine();
            }
            catch (Exception ex)
            {
                Console.Write("Error publishing the post: " + ex.Message);
                Console.ReadLine();
            }
        }
    }
}

```


## <a name="additional-resources"></a><span data-ttu-id="df658-153">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="df658-153">Additional resources</span></span>
<span data-ttu-id="df658-154"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="df658-154"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="df658-155">Arbeiten mit sozialen Feeds in SharePoint</span><span class="sxs-lookup"><span data-stu-id="df658-155">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  
-  <span data-ttu-id="df658-156">[SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) und [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) in die Clientobjektmodelle</span><span class="sxs-lookup"><span data-stu-id="df658-156">[SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) and [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) in the client object models</span></span>
    
  
-  <span data-ttu-id="df658-157">[SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx) und [SocialDataItem](http://msdn.microsoft.com/library/757e7b62-66a6-b03f-0ff0-769a42eb2b4a%28Office.15%29.aspx) im JavaScript-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="df658-157">[SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx) and [SocialDataItem](http://msdn.microsoft.com/library/757e7b62-66a6-b03f-0ff0-769a42eb2b4a%28Office.15%29.aspx) in the JavaScript object model</span></span>
    
  
-  [<span data-ttu-id="df658-158">REST-API-Referenz für sozialen Feed für SharePoint</span><span class="sxs-lookup"><span data-stu-id="df658-158">Social feed REST API reference for SharePoint</span></span>](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  <span data-ttu-id="df658-159">[SPSocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialPostCreationData.aspx) und [SPSocialDataItem](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialDataItem.aspx) im Server-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="df658-159">[SPSocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialPostCreationData.aspx) and [SPSocialDataItem](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialDataItem.aspx) in the server object model</span></span>
    
  

