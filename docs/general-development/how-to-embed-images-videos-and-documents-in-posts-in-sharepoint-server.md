---
title: "Einbetten von Bildern, Videos und Dokumenten in Beiträgen in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 9927b9e7-daea-4261-80fa-4cc25f489e22
ms.openlocfilehash: 13724f464dab3f1b5da94e65df7728b38976ec2a
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-embed-images-videos-and-documents-in-posts-in-sharepoint"></a><span data-ttu-id="74153-102">Vorgehensweise: Einbetten von Bildern, Videos und Dokumenten in Beiträgen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="74153-102">How to: Embed images, videos, and documents in posts in SharePoint Server 2013</span></span>
<span data-ttu-id="74153-103">In diesem Artikel erfahren Sie, wie Sie Mikroblogbeiträgen  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx)-Objekte hinzufügen, die als eingebettete Bilder, Videos und Dokumente in sozialen Feeds für SharePoint gerendert werden.</span><span class="sxs-lookup"><span data-stu-id="74153-103">Learn how to add  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) objects to microblog posts, which render as embedded pictures, videos, and documents in SharePoint Server 2013 social feeds.</span></span>
<span data-ttu-id="74153-104">Die einfachste Form von Beitragsinhalten in einem sozialen Feed enthält nur Text, aber Sie können auch eingebettete Bilder, Videos und Dokumente hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="74153-104">In a social feed, the simplest form of post content contains only text, but you can also add embedded pictures, videos, and documents.</span></span> <span data-ttu-id="74153-105">Zu diesem Zweck verwenden Sie die [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx)-Eigenschaft des [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx)-Objekts, das den Beitrag definiert.</span><span class="sxs-lookup"><span data-stu-id="74153-105">To do this, you use the  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) property on the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that defines the post.</span></span> <span data-ttu-id="74153-106">Beiträge können eine Anlage enthalten, die durch ein [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx)-Objekt dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="74153-106">Posts can contain one attachment, which is represented by a [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) object.</span></span>
  
    
    


> <span data-ttu-id="74153-107">**Hinweis:** Um eine Erwähnung, ein Tag oder einen Link zum Inhalt eines Beitrags hinzuzufügen, fügen Sie ein [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx)-Objekts zur [SocialPostCreationData.ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx)-Eigenschaft hinzu.</span><span class="sxs-lookup"><span data-stu-id="74153-107">**Note** To add a mention, tag, or link to a post's content, you add a  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) object to the [SocialPostCreationData.ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) property. For more information, see How to: Include mentions, tags, and links to sites and documents in posts in SharePoint Server 2013.</span></span> <span data-ttu-id="74153-108">Weitere Informationen finden Sie unter [Vorgehensweise: Einschließen von Erwähnungen, Tags und Links zu Websites und Dokumenten in Beiträgen in SharePoint](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md).</span><span class="sxs-lookup"><span data-stu-id="74153-108">[How to: Include mentions, tags, and links to sites and documents in posts in SharePoint Server 2013](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md)</span></span> 
  
    
    


<span data-ttu-id="74153-p103">Die in diesem Artikel beschriebene API hat ihren Ursprung des Clientobjektmodells .NET. Wenn Sie eine andere API verwenden, kann beispielsweise die JavaScript-Objektmodell, den zu verwendenden Objektnamen oder die dazugehörige API abweichen. Links zur Dokumentation für verwandte APIs finden Sie unter  [Zusätzliche Ressourcen](#bk_addresources) .</span><span class="sxs-lookup"><span data-stu-id="74153-p103">The API described in this article is from the .NET client object model. If you're using another API, such as the JavaScript object model, the object names or corresponding API might be different. See  [Additional resources](#bk_addresources) for links to documentation for related APIs.</span></span>
  
    
    


## <a name="prerequisites-for-using-the-code-examples-to-add-attachments-to-a-post"></a><span data-ttu-id="74153-112">Voraussetzung für die Verwendung der Codebeispiele zum Hinzufügen von Anlagen auf einen Beitrag</span><span class="sxs-lookup"><span data-stu-id="74153-112">Prerequisites for using the code examples to add attachments to a post</span></span>
<span data-ttu-id="74153-113"><a name="bk_preReqs"> </a></span><span class="sxs-lookup"><span data-stu-id="74153-113"></span></span>

<span data-ttu-id="74153-p104">Die Codebeispiele in diesem Artikel wird gezeigt, wie hinzuzufügende Bild, video und Dokument Anlagen Microblog sendet. In diesen Beispielen werden über eine Konsolenanwendung, die die folgenden Assemblys SharePoint verwendet:</span><span class="sxs-lookup"><span data-stu-id="74153-p104">The code examples in this article show how to add image, video, and document attachments to microblog posts. These examples are from a console application that uses the following SharePoint assemblies:</span></span>
  
    
    

- <span data-ttu-id="74153-116">Microsoft.SharePoint.Client</span><span class="sxs-lookup"><span data-stu-id="74153-116">Microsoft.SharePoint.Client</span></span>
    
  
- <span data-ttu-id="74153-117">Microsoft.SharePoint.Client.Runtime</span><span class="sxs-lookup"><span data-stu-id="74153-117">Microsoft.SharePoint.Client.Runtime</span></span>
    
  
- <span data-ttu-id="74153-118">Microsoft.SharePoint.Client.UserProfilies</span><span class="sxs-lookup"><span data-stu-id="74153-118">Microsoft.SharePoint.Client.UserProfilies</span></span>
    
  
<span data-ttu-id="74153-119">Um die Beispiele in diesem Artikel zu verwenden, müssen Sie ein Bild, ein Video und ein Dokument hochladen.</span><span class="sxs-lookup"><span data-stu-id="74153-119">To use the examples in this article, you'll need to upload an image, a video, and a document.</span></span> <span data-ttu-id="74153-120">Damit Sie das Videobeispiel verwenden können, muss das Feature „Video“ auf dem Server aktiviert sein, und die Videodatei muss in einer Objektbibliothek gespeichert sein.</span><span class="sxs-lookup"><span data-stu-id="74153-120">To use the video example, the video feature must be enabled on the server and the video file must be stored in an asset library.</span></span> <span data-ttu-id="74153-121">Zum Verwendung des Dokumentbeispiels in einer lokalen Umgebung muss Office Online in der Umgebung konfiguriert sein.</span><span class="sxs-lookup"><span data-stu-id="74153-121">To use the document example in an on-premises environment, Office Online must be configured in the environment.</span></span> <span data-ttu-id="74153-122">Weitere Informationen finden Sie unter [Planen digitaler Objektbibliotheken in SharePoint](http://technet.microsoft.com/de-de/library/ee414275.aspx) und [Konfigurieren von SharePoint für die Verwendung von Office Online](http://technet.microsoft.com/de-de/library/ff431687.aspx).</span><span class="sxs-lookup"><span data-stu-id="74153-122">For more information, see  [Plan digital asset libraries in SharePoint](http://technet.microsoft.com/de-de/library/ee414275.aspx) and [Configure SharePoint to use Office Online](http://technet.microsoft.com/de-de/library/ff431687.aspx).</span></span>
  
    
    
<span data-ttu-id="74153-123">Weitere Informationen zum Einrichten Ihrer Entwicklungsumgebung und Erstellen einer Konsolenanwendung finden Sie unter  [Vorgehensweise: Erstellen und Löschen von Beiträge und Abrufen des für soziale Netzwerke-Feed mithilfe des clientobjektmodells .NET SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md).</span><span class="sxs-lookup"><span data-stu-id="74153-123">For instructions about how to set up your development environment and create a console application, see  [How to: Create and delete posts and retrieve the social feed by using the .NET client object model in SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md).</span></span>
  
    
    

## <a name="example-embed-an-image-in-a-post-in-sharepoint"></a><span data-ttu-id="74153-124">Beispiel: Einbetten eines Bilds in einen Beitrag in SharePoint</span><span class="sxs-lookup"><span data-stu-id="74153-124">Example: Embed an image in a post in SharePoint Server 2013</span></span>
<span data-ttu-id="74153-125"><a name="bkmk_addImage"> </a></span><span class="sxs-lookup"><span data-stu-id="74153-125"></span></span>

<span data-ttu-id="74153-p106">Im folgenden Codebeispiel wird veröffentlicht einen Beitrag, der ein eingebettetes Bild enthält. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="74153-p106">The following code example publishes a post that contains an embedded image. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="74153-p107">Erstellen Sie ein  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) -Objekt, das das Bild darstellt. Die [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) gibt das Feld [SocialAttachmentKind.Image](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachmentKind.Image.aspx) und den URI der Bilddatei an.</span><span class="sxs-lookup"><span data-stu-id="74153-p107">Create a  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) object that represents the image. The [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) specifies the [SocialAttachmentKind.Image](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachmentKind.Image.aspx) field and the URI of the image file.</span></span>
    
  
- <span data-ttu-id="74153-130">Fügen Sie das Image-Objekt an die  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) -Eigenschaft des [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) -Objekts, das zum Erstellen der POST-Anforderung verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="74153-130">Add the image object to the  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) property of the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that's used to create the post.</span></span>
    
  
<span data-ttu-id="74153-131">Ändern Sie die Platzhalterwerte für die URL-Variablen vor dem Ausführen des Codes.</span><span class="sxs-lookup"><span data-stu-id="74153-131">Change the placeholder values for the URL variables before you run the code.</span></span>
  
    
    



```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace EmbedImageInPost
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the actual values.
            const string serverUrl = "http://serverName/siteName/";
            const string imageUrl = "http://serverName/Shared%20Documents/imageName.jpg";

            // Define the image attachment that you want to embed in the post.
            SocialAttachment attachment = new SocialAttachment()
            {
                AttachmentKind = SocialAttachmentKind.Image,
                Uri = imageUrl
            };

            // Define properties for the post and add the attachment.
            SocialPostCreationData postCreationData = new SocialPostCreationData();
            postCreationData.ContentText = "Look at this!";
            postCreationData.Attachment = attachment;

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


## <a name="embed-a-video-in-a-post-in-sharepoint"></a><span data-ttu-id="74153-132">Einbetten eines Videos in einem Beitrag in SharePoint</span><span class="sxs-lookup"><span data-stu-id="74153-132">Embed a video in a post in SharePoint Server 2013</span></span>
<span data-ttu-id="74153-133"><a name="bkmk_addVideo"> </a></span><span class="sxs-lookup"><span data-stu-id="74153-133"></span></span>

<span data-ttu-id="74153-p108">Im folgenden Codebeispiel wird veröffentlicht einen Beitrag, der ein eingebettetes Video enthält. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="74153-p108">The following code example publishes a post that contains an embedded video. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="74153-136">Rufen Sie das  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) -Objekt, das video Attachment-Objekt darstellt, mithilfe der [SocialFeedManager.GetPreview](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetPreview.aspx) -Methode.</span><span class="sxs-lookup"><span data-stu-id="74153-136">Get the  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) object that represents the video attachment by using the [SocialFeedManager.GetPreview](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetPreview.aspx) method.</span></span>
    
  
- <span data-ttu-id="74153-137">Fügen Sie das video Attachment-Objekts die  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) -Eigenschaft des [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) -Objekts, das zum Erstellen der POST-Anforderung verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="74153-137">Add the video attachment to the  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) property of the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that's used to create the post.</span></span>
    
  
<span data-ttu-id="74153-p109">Dieses Beispiel erfordert die Videofunktionen in einer Objektbibliothek hochgeladen werden auf dem Server und die Videodatei aktiviert werden soll. Finden Sie unter der  [Voraussetzung für die Verwendung in den Codebeispielen](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md#bk_preReqs) für Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="74153-p109">This example requires the video features to be enabled on the server and the video file to be uploaded to an asset library. See the  [prerequisites for using the code examples](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md#bk_preReqs) for more information.</span></span>
  
    
    
<span data-ttu-id="74153-140">Ändern Sie die Platzhalterwerte für die URL-Variablen vor dem Ausführen des Codes.</span><span class="sxs-lookup"><span data-stu-id="74153-140">Change the placeholder values for the URL variables before you run the code.</span></span>
  
    
    



```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace EmbedVideoInPost
{
    class Program
    {
        static void Main(string[] args)
        {
            // Replace the following placeholder values with the actual values.
            const string serverUrl = "http://serverName/siteName/";
            const string videoUrl = "http://serverName/Asset%20Library/fileName?Web=1";

            try
            {

                // Get the context and the SocialFeedManager instance.
                ClientContext clientContext = new ClientContext(serverUrl);
                SocialFeedManager feedManager = new SocialFeedManager(clientContext);

                // Get the video attachment from the server.
                ClientResult<SocialAttachment> attachment = feedManager.GetPreview(videoUrl);
                clientContext.ExecuteQuery();

                // Define properties for the post and add the attachment.
                SocialPostCreationData postCreationData = new SocialPostCreationData();
                postCreationData.ContentText = "Look at this!";
                postCreationData.Attachment = attachment.Value;

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


## <a name="example-embed-a-document-in-a-post-in-sharepoint"></a><span data-ttu-id="74153-141">Beispiel: Einbetten eines Dokuments in einem Beitrag in SharePoint</span><span class="sxs-lookup"><span data-stu-id="74153-141">Example: Embed a document in a post in SharePoint Server 2013</span></span>
<span data-ttu-id="74153-142"><a name="bkmk_addDoc"> </a></span><span class="sxs-lookup"><span data-stu-id="74153-142"></span></span>

<span data-ttu-id="74153-p110">Im folgenden Codebeispiel wird veröffentlicht einen Beitrag, der ein eingebettetes Dokument enthält. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="74153-p110">The following code example publishes a post that contains an embedded document. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="74153-145">Ruft das  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) -Objekt, das die Anlage Dokument darstellt, mithilfe der [SocialFeedManager.GetPreview](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetPreview.aspx) -Methode.</span><span class="sxs-lookup"><span data-stu-id="74153-145">Get the  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) object that represents the document attachment by using the [SocialFeedManager.GetPreview](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetPreview.aspx) method.</span></span>
    
  
- <span data-ttu-id="74153-146">Fügen Sie die Dokumentanlage der [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx)-Eigenschaft des [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx)-Objekts hinzu, das verwendet wird, um den Beitrag zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="74153-146">Add the document attachment to the  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) property of the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that's used to create the post.</span></span>
    
  
<span data-ttu-id="74153-147">Wenn Sie dieses Beispiel in einer lokalen Umgebung verwenden möchten, muss Ihre Umgebung für die Verwendung von Office Online konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="74153-147">To use this example in an on-premises environment, your environment must be configured to use Office Online.</span></span> <span data-ttu-id="74153-148">Weitere Informationen finden Sie unter [Voraussetzungen für die Verwendung der Codebeispiele](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md#bk_preReqs).</span><span class="sxs-lookup"><span data-stu-id="74153-148">See the  [prerequisites for using the code examples](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md#bk_preReqs) for more information.</span></span> <span data-ttu-id="74153-149">Andernfalls können Sie einen Link zum Dokument bereitstellen, wie unter [Vorgehensweise: Einschließen von Erwähnungen, Tags und Links zu Websites und Dokumenten in Beiträgen in SharePoint](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="74153-149">To use this example in an on-premises environment, your environment must be configured to use Office Online. See the  prerequisites for using the code examples for more information. Otherwise, you can post a link to the document as described in [How to: Include mentions, tags, and links to sites and documents in posts in SharePoint Server 2013](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md).</span></span>
  
    
    
<span data-ttu-id="74153-150">Ändern Sie die Platzhalterwerte für die URL-Variablen vor dem Ausführen des Codes.</span><span class="sxs-lookup"><span data-stu-id="74153-150">Change the placeholder values for the URL variables before you run the code.</span></span>
  
    
    



```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace EmbedDocumentInPost
{
    class Program
    {
        static void Main(string[] args)
        {
            // Replace the following placeholder values with the actual values.
            const string serverUrl = "http://serverName";
            const string documentUrl = "http://serverName/Shared%20Documents/fileName.docx";

            try
            {

                // Get the context and the SocialFeedManager instance.
                ClientContext clientContext = new ClientContext(serverUrl);
                SocialFeedManager feedManager = new SocialFeedManager(clientContext);

                // Get the document attachment from the server.
                ClientResult<SocialAttachment> attachment = feedManager.GetPreview(documentUrl);
                clientContext.ExecuteQuery();

                // Define properties for the post and add the attachment.
                SocialPostCreationData postCreationData = new SocialPostCreationData();
                postCreationData.ContentText = "Post with a document.";
                postCreationData.Attachment = attachment.Value;

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


## <a name="additional-resources"></a><span data-ttu-id="74153-151">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="74153-151">Additional resources</span></span>
<span data-ttu-id="74153-152"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="74153-152"></span></span>


-  [<span data-ttu-id="74153-153">Arbeiten mit sozialen Feeds in SharePoint</span><span class="sxs-lookup"><span data-stu-id="74153-153">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  
-  [<span data-ttu-id="74153-154">Vorgehensweise: Einschließen von Erwähnungen, Tags und Links zu Websites und Dokumenten in Beiträgen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="74153-154">How to: Include mentions, tags, and links to sites and documents in posts in SharePoint Server 2013</span></span>](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md)
    
  
-  <span data-ttu-id="74153-155">[SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) und [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) in den Clientobjektmodellen</span><span class="sxs-lookup"><span data-stu-id="74153-155">[SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) and [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) in the client object models</span></span>
    
  
-  <span data-ttu-id="74153-156">[SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx) und [SocialAttachment](http://msdn.microsoft.com/library/dfdee790-a1b0-19c8-0e92-5a6e058ba4db%28Office.15%29.aspx) im JavaScript-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="74153-156">[SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx) and [SocialAttachment](http://msdn.microsoft.com/library/dfdee790-a1b0-19c8-0e92-5a6e058ba4db%28Office.15%29.aspx) in the JavaScript object model</span></span>
    
  
-  [<span data-ttu-id="74153-157">REST-API-Referenz für sozialen Feed für SharePoint</span><span class="sxs-lookup"><span data-stu-id="74153-157">Social feed REST API reference for SharePoint</span></span>](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  <span data-ttu-id="74153-158">[SPSocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialPostCreationData.aspx) und [SPSocialAttachment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialAttachment.aspx) im Server-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="74153-158">[SPSocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialPostCreationData.aspx) and [SPSocialAttachment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialAttachment.aspx) in the server object model</span></span>
    
  

