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
# <a name="include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharepoint"></a>Einschließen von Erwähnungen, Tags und Links zu Websites und Dokumenten in Beiträgen in SharePoint

In diesem Artikel erfahren Sie, wie Sie Mikroblogbeiträgen [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx)-Objekte hinzufügen, die als Erwähnungen, Tags oder Links in sozialen Feeds für SharePoint gerendert werden.
Die einfachste Form von Beitragsinhalten in sozialen Feeds enthält nur Text, aber Sie können auch Links hinzufügen, die als Erwähnungen, Tags oder Links zu Websites, SharePoint-Websites und Dokumenten gerendert werden. Zu diesem Zweck fügen Sie [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx)-Objekte zur [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx)-Eigenschaft des [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx)-Objekts hinzu, das den Beitrag definiert. Beiträge können mehrere Links enthalten.
  
    
    


> **Hinweis:** Um eingebettete Bilder, Videos oder Dokumente zum Inhalt eines Beitrags hinzuzufügen, fügen Sie ein [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx)-Objekt zur [SocialPostCreationData.Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx)-Eigenschaft hinzu. Weitere Informationen finden Sie unter [Vorgehensweise: Einbetten von Bildern, Videos und Dokumenten in Beiträgen in SharePoint](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md). 
  
    
    


Die in diesem Artikel beschriebene API hat ihren Ursprung des Clientobjektmodells .NET. Jedoch, wenn Sie eine andere API verwenden, möglicherweise wie die JavaScript-Objektmodell, den zu verwendenden Objektnamen oder die dazugehörige API abweichen. Links zur Dokumentation für verwandte APIs finden Sie unter  [Zusätzliche Ressourcen](#bk_addresources) .
  
    
    


## <a name="prerequisites-for-using-the-code-examples-to-add-links-to-a-post-in-sharepoint"></a>Voraussetzungen für die Verwendung der Codebeispiele zum Hinzufügen von Links zu einem Beitrag in SharePoint
<a name="bk_preReqs"> </a>

Die Codebeispiele in diesem Artikel zeigen, wie Links Microblog Beiträge hinzugefügt. In diesen Beispielen werden von konsolenanwendungen, die die folgenden SharePoint-Assemblys verwenden:
  
    
    

- Microsoft.SharePoint.Client
    
  
- Microsoft.SharePoint.Client.Runtime
    
  
- Microsoft.SharePoint.Client.UserProfilies
    
  
Weitere Informationen zum Einrichten Ihrer Entwicklungsumgebung und Erstellen einer Konsolenanwendung finden Sie unter  [Vorgehensweise: Erstellen und Löschen von Beiträge und Abrufen des für soziale Netzwerke-Feed mithilfe des clientobjektmodells .NET SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md).
  
    
    

## <a name="example-include-links-to-websites-sharepoint-sites-and-documents-in-a-post-in-sharepoint"></a>Beispiel: Einschließen von Links zu Websites, SharePoint-Websites und Dokumenten in einem Beitrag in SharePoint
<a name="bkmk_addLinks"> </a>

Im folgenden Codebeispiel wird veröffentlicht einen Beitrag, der Links zu einer Website und einer SharePoint-Website zu einem Dokument enthält. Außerdem wird gezeigt, wie Sie:
  
    
    

- Erstellen Sie  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) -Objekten, die Links darstellen. Jede Instanz wird das Feld [SocialDataItemType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.aspx) für den Link, der Anzeigetext für den Link, und den Link URI festgelegt.
    
  
- Hinzufügen von Platzhaltern für den Post-Text um anzugeben, wo Anzeigetext für den Link angezeigt werden soll.
    
  
- Fügen Sie die Linkobjekte zur [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx)-Eigenschaft des [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx)-Objekts hinzu, das zum Erstellen des Beitrags verwendet wird.
    
  

> **Hinweis:** Derzeit werden in SharePoint Links zu Websites, SharePoint-Websites und Dokumenten gleich behandelt. Es empfiehlt sich jedoch, für SharePoint-Websites und Dokumente die Typen [Site](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Site.aspx) und [Document](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Document.aspx) zu wählen.
  
    
    

Wenn Sie im sozialen Feed auf einen Link zu einer Website, einer SharePoint-Website oder einem Dokument klicken, wird das Element in einem separaten Browserfenster geöffnet.
  
    
    

> **Hinweis:** Ändern Sie die Platzhalterwerte für die URL-Variablen vor dem Ausführen des Codes. 
  
    
    




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


## <a name="example-mention-someone-in-a-post-in-sharepoint"></a>Beispiel: Erwähnen einer Person in einem Beitrag in SharePoint
<a name="bkmk_addMention"> </a>

Im folgenden Codebeispiel wird veröffentlicht einen Beitrag, der einen Benutzer erwähnt. Außerdem wird gezeigt, wie Sie:
  
    
    

- Erstellen Sie ein  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) -Objekt, um einen Vermerk darstellen, der eine Verknüpfung zu einem Benutzer ist. Die [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) gibt das [SocialDataItemType.User](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.User.aspx) -Feld und die weiter oben erwähnt Person Kontonamen. Sie können den Kontonamen mithilfe der Anmeldename der Person oder e-Mail-Adresse festlegen.
    
  
- Hinzufügen eines Platzhalters für den Post-Text um anzugeben, wo der weiter oben erwähnt Person Anzeigename angezeigt werden soll.
    
  
- Fügen Sie der  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) der [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) -Eigenschaft des [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) -Objekts, das zum Erstellen der POST-Anforderung verwendet wird.
    
  
Wenn Sie in einem sozialen Feed auf eine Erwähnung klicken, werden Sie auf die **Info**-Seite der erwähnten Person umgeleitet.
  
    
    

> **Hinweis:** Ändern Sie die Platzhalterwerte für die Variablen **serverURL** und **accountName** vor dem Ausführen des Codes.
  
    
    




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


## <a name="example-include-a-tag-in-a-post-in-sharepoint"></a>Beispiel: Einschließen eines Tags in einem Beitrag in SharePoint
<a name="bkmk_addTag"> </a>

Im folgenden Codebeispiel wird veröffentlicht einen Beitrag, der ein Tag enthält. Außerdem wird gezeigt, wie Sie:
  
    
    

- Erstellen Sie ein  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) -Objekt, um das Tag darstellen. Die [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) gibt das Feld [SocialDataItemType.Tag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Tag.aspx) und der Tagname, die ein **#** Zeichen enthalten muss.
    
  
- Hinzufügen eines Platzhalters für den Post-Text um anzugeben, wo das Tag angezeigt werden soll.
    
  
- Fügen Sie der  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) der [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) -Eigenschaft des [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) -Objekts, das zum Erstellen der POST-Anforderung verwendet wird.
    
  
Wenn Sie im sozialen Feed auf ein Tag klicken, werden Sie zur **Info**-Seite des Tags umgeleitet. Wenn das Tag noch nicht vorhanden ist, wird es vom Server erstellt.
  
    
    

> **Hinweis:** Ändern Sie die Platzhalterwerte für die Variablen **serverURL** und **tagName** vor dem Ausführen des Codes.
  
    
    




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


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Arbeiten mit sozialen Feeds in SharePoint](work-with-social-feeds-in-sharepoint.md)
    
  
-  [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) und [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) in die Clientobjektmodelle
    
  
-  [SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx) und [SocialDataItem](http://msdn.microsoft.com/library/757e7b62-66a6-b03f-0ff0-769a42eb2b4a%28Office.15%29.aspx) im JavaScript-Objektmodell
    
  
-  [REST-API-Referenz für sozialen Feed für SharePoint](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [SPSocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialPostCreationData.aspx) und [SPSocialDataItem](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialDataItem.aspx) im Server-Objektmodell
    
  

