---
title: Verweisthreads und Digestthreads in sozialen SharePoint-Feeds
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 58e68fb2-ba40-4861-912f-355e119a1c41
ms.openlocfilehash: b902efe9ba6579d534ebc15bda7a15cf7d7c4ec6
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="reference-threads-and-digest-threads-in-sharepoint-social-feeds"></a><span data-ttu-id="dacfc-102">Verweisthreads und Digestthreads in sozialen SharePoint-Feeds</span><span class="sxs-lookup"><span data-stu-id="dacfc-102">Reference threads and digest threads in SharePoint social feeds</span></span>
<span data-ttu-id="dacfc-103">In diesem Artikel werden die Threadtypen Verweisthread und Digestthread beschrieben. Sie können in den Threadsammlungen enthalten sein, die soziale Feeds in SharePoint bilden.</span><span class="sxs-lookup"><span data-stu-id="dacfc-103">Learn about reference threads and digest threads, which are thread types that may be included in the collection of threads that make up a social feed in SharePoint.</span></span>
<span data-ttu-id="dacfc-104">Wenn Sie einen sozialen Feed abrufen, gibt SharePoint ein Objekt des Typs [SocialFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeed.aspx) zurück. Dieses Objekt enthält die Sammlung von Objekten des Typs [SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx), die den Feed bilden.</span><span class="sxs-lookup"><span data-stu-id="dacfc-104">When you retrieve a social feed, SharePoint returns a  [SocialFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeed.aspx) object that contains the collection of [SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) objects that make up the feed.</span></span> <span data-ttu-id="dacfc-105">Diese Threads können Unterhaltungen, einzelne Mikroblogbeiträge oder Benachrichtigungen darstellen, einschließlich Ereignissen und Verweisthreads.</span><span class="sxs-lookup"><span data-stu-id="dacfc-105">These threads can represent conversations, single microblog posts, and notifications, which include events and reference threads.</span></span> <span data-ttu-id="dacfc-106">Threads, die Unterhaltungen darstellen, werden vom Server möglicherweise als Digestthreads zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="dacfc-106">Threads that represent conversations may be returned by the server as digest threads.</span></span>
  
> [!NOTE]
> <span data-ttu-id="dacfc-107">Die API, auf die in diesem Artikel Bezug genommen wird, stammt aus dem .NET-Clientobjektmodell.</span><span class="sxs-lookup"><span data-stu-id="dacfc-107">Note: The API referenced in this article is from the .NET client object model.</span></span> <span data-ttu-id="dacfc-108">Die entsprechenden Objekte in anderen APIs können anders angelegt sein.</span><span class="sxs-lookup"><span data-stu-id="dacfc-108">However, corresponding objects in other APIs might be different.</span></span> <span data-ttu-id="dacfc-109">Links zu anderen themenverwandten APIs finden Sie unter [Zusätzliche Ressourcen](#bk_addresources).</span><span class="sxs-lookup"><span data-stu-id="dacfc-109">See  [Additional resources](#bk_addresources) for links to other related APIs.</span></span>
  
    
    


## <a name="what-are-reference-threads-in-sharepoint-social-feeds"></a><span data-ttu-id="dacfc-110">Was sind Verweisthreads in sozialen SharePoint-Feeds?</span><span class="sxs-lookup"><span data-stu-id="dacfc-110">What are reference threads in SharePoint social feeds?</span></span>
<span data-ttu-id="dacfc-111"><a name="bk_whatAreRefThreads"> </a></span><span class="sxs-lookup"><span data-stu-id="dacfc-111"><a name="bk_whatAreRefThreads"> </a></span></span>

<span data-ttu-id="dacfc-112">Wenn ein Benutzer einen Beitrag likt, jemanden in einem Beitrag erwähnt, auf einen Beitrag antwortet oder ein Tag in einen Beitrag einfügt, erzeugt SharePoint einen Verweisthread.</span><span class="sxs-lookup"><span data-stu-id="dacfc-112">When a user likes a post, mentions someone in a post, replies to a post, or includes a tag in a post, SharePoint generates a reference thread.</span></span> <span data-ttu-id="dacfc-113">Ein Verweisthread verfügt über zwei Eigenschaften, über die Sie Informationen zu dem Verweisthread oder dem Beitrag abrufen: [ThreadType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.ThreadType.aspx) und [PostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.PostReference.aspx).</span><span class="sxs-lookup"><span data-stu-id="dacfc-113">Reference threads have two properties that you use to get information about the referenced thread or post:  [ThreadType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.ThreadType.aspx) and [PostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.PostReference.aspx) .</span></span>
  
    
    
<span data-ttu-id="dacfc-114">Verweisthreads lassen sich anhand ihrer Eigenschaft [ThreadType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.ThreadType.aspx) identifizieren. Sie kann einen der in Tabelle 1 aufgeführten Werte zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="dacfc-114">You can identify a reference thread by its  [ThreadType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.ThreadType.aspx) property, which can return one of the values shown in Table 1.</span></span>
  
    
    

<span data-ttu-id="dacfc-115">**In Tabelle 1. Typen von Verweis thread**</span><span class="sxs-lookup"><span data-stu-id="dacfc-115">**Table 1. Types of reference thread**</span></span>


|<span data-ttu-id="dacfc-116">**Verweistyp**</span><span class="sxs-lookup"><span data-stu-id="dacfc-116">**Reference type**</span></span>|<span data-ttu-id="dacfc-117">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="dacfc-117">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="dacfc-118">[LikeReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.LikeReference.aspx) **** </span><span class="sxs-lookup"><span data-stu-id="dacfc-118">[LikeReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.LikeReference.aspx) **** </span></span><br/> |<span data-ttu-id="dacfc-119">Ein Verweis auf einen Beitrag, den ein Benutzer "gefällt mir".</span><span class="sxs-lookup"><span data-stu-id="dacfc-119">A reference to a post that a user likes.</span></span>  <br/> |
| [<span data-ttu-id="dacfc-120">MentionReference</span><span class="sxs-lookup"><span data-stu-id="dacfc-120">MentionReference</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.MentionReference.aspx) <br/> |<span data-ttu-id="dacfc-121">Ein Verweis auf einen Beitrag, der einen Benutzer erwähnt.</span><span class="sxs-lookup"><span data-stu-id="dacfc-121">A reference to a post that mentions a user.</span></span>  <br/> |
| [<span data-ttu-id="dacfc-122">ReplyReference</span><span class="sxs-lookup"><span data-stu-id="dacfc-122">ReplyReference</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.ReplyReference.aspx) <br/> |<span data-ttu-id="dacfc-123">Ein Verweis auf eine Antwort.</span><span class="sxs-lookup"><span data-stu-id="dacfc-123">A reference to a reply.</span></span>  <br/> |
| [<span data-ttu-id="dacfc-124">TagReference</span><span class="sxs-lookup"><span data-stu-id="dacfc-124">TagReference</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.TagReference.aspx) <br/> |<span data-ttu-id="dacfc-125">Ein Verweis auf ein Beitrag, der ein Tag enthält.</span><span class="sxs-lookup"><span data-stu-id="dacfc-125">A reference to a post that contains a tag.</span></span>  <br/> |
| [<span data-ttu-id="dacfc-126">Normal</span><span class="sxs-lookup"><span data-stu-id="dacfc-126">Normal</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.Normal.aspx) <br/> |<span data-ttu-id="dacfc-127">Ein Verweis-Thread.</span><span class="sxs-lookup"><span data-stu-id="dacfc-127">Not a reference thread.</span></span>  <br/> |
   
<span data-ttu-id="dacfc-p104">Die  [PostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.PostReference.aspx) -Eigenschaft gibt ein [SocialPostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostReference.aspx) -Objekt, das Informationen über den Thread enthält, die das Ereignis ausgelöst hat. Mindestens enthält sie die ID des Quellthreads, die Sie dann mit der [SocialFeedManager.GetFullThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFullThread.aspx) -Methode verwenden können, den Thread abrufen, wenn es noch vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="dacfc-p104">The  [PostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.PostReference.aspx) property returns a [SocialPostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostReference.aspx) object that contains information about the thread that triggered the event. At a minimum, it contains the ID of the source thread, which you can then use with the [SocialFeedManager.GetFullThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFullThread.aspx) method to retrieve the thread if it still exists.</span></span>
  
    
    
 <span data-ttu-id="dacfc-p105">[SocialPostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostReference.aspx) kann auch eine Kopie der Quelle Beitrag oder Thread enthalten. Diese Verfügbarkeit hängt davon ab, die Feedtyp sowie die Threadtyp und die Einschränkung aus Sicherheitsgründen. Enthält die Referenz einen Beitrag oder Thread, diese Objekte stellen Momentaufnahmen des Post oder Threads zum Zeitpunkt des Ereignisses dar.</span><span class="sxs-lookup"><span data-stu-id="dacfc-p105">[SocialPostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostReference.aspx) might also contain a copy of the source post or thread. This availability depends on the feed type, thread type, and security trimming. If the reference does contain a post or thread, these objects represent snapshots of the post or thread at the time the event occurred.</span></span>
  
    
    
<span data-ttu-id="dacfc-p106">Nicht alle feedbezogene Aktivitäten werden in den Feed als Referenz Threads gebucht. Beispielsweise sind folgende Benachrichtigungen (beispielsweise wenn eine Person nach einem Standort gestartet wird) nicht Verweis Threads.</span><span class="sxs-lookup"><span data-stu-id="dacfc-p106">Not all feed-related activities are posted to the feed as reference threads. For example, Following notifications (such as when someone starts following a site) are not reference threads.</span></span>
  
> [!NOTE]
> <span data-ttu-id="dacfc-135">SharePoint führt für Inhalte in automatisch generierten Beiträgen automatisch Sicherheitskürzungen durch. Gleiches gilt für Websitezugriffe in allen Beiträgen, die auf einen Websitefeed verweisen.</span><span class="sxs-lookup"><span data-stu-id="dacfc-135">Note: SharePoint automatically security trims for content in autogenerated posts and for site access in all posts that are directed to a site feed.</span></span> <span data-ttu-id="dacfc-136">Mithilfe des Attributs **SecurityUris** können Sie die Sicherheitskürzung jedoch auch auf jeden beliebigen anderen Beitrag anwenden. Dazu müssen Sie lediglich die URL des Beitrags angeben.</span><span class="sxs-lookup"><span data-stu-id="dacfc-136">However, you can use the **SecurityUris** attribute to security trim any post by specifying a URL.</span></span> <span data-ttu-id="dacfc-137">Benutzer, die keinen Zugriff auf die URL haben, erhalten den Beitrag nicht.</span><span class="sxs-lookup"><span data-stu-id="dacfc-137">Users who do not have access to the URL do not receive the post.</span></span>
  
    
    

<span data-ttu-id="dacfc-138">Antwort-, Like- und Erwähnungsverweise werden unbefristet im persönlichen Feed des Benutzers gespeichert.</span><span class="sxs-lookup"><span data-stu-id="dacfc-138">Reply, like, and mention references are stored indefinitely in the user's personal feed.</span></span> <span data-ttu-id="dacfc-139">Tagverweise werden im verteilten Cache gespeichert, also nur vorübergehend.</span><span class="sxs-lookup"><span data-stu-id="dacfc-139">Tag references are stored in the Distributed Cache, so they are stored temporarily.</span></span> <span data-ttu-id="dacfc-140">Weitere Informationen zur Zwischenspeicherung finden Sie unter [Übersicht über Mikrobloggingfeatures, Feeds und den verteilten Cachedienst in SharePoint](http://technet.microsoft.com/de-DE/library/jj219700%28v=office.15%29.aspx#cache).</span><span class="sxs-lookup"><span data-stu-id="dacfc-140">For more information about caching, see  [Overview of microblog features, feeds, and the Distributed Cache service in SharePoint](http://technet.microsoft.com/de-DE/library/jj219700%28v=office.15%29.aspx#cache).</span></span>
  
    
    

## <a name="what-are-digest-threads-in-sharepoint-social-feeds"></a><span data-ttu-id="dacfc-141">Was sind Digestthreads in sozialen SharePoint-Feeds?</span><span class="sxs-lookup"><span data-stu-id="dacfc-141">What are digest threads in SharePoint social feeds?</span></span>
<span data-ttu-id="dacfc-142"><a name="bk_whatAreDigests"> </a></span><span class="sxs-lookup"><span data-stu-id="dacfc-142"><a name="bk_whatAreDigests"> </a></span></span>

<span data-ttu-id="dacfc-p109">Ein Digest-Thread stellt eine kompakte Version einer Unterhaltung - enthält des Threads Stamm Post und zwei neuesten Antworten. Sie können einen Digest-Thread identifizieren, indem Sie überprüfen, ob der Thread das  [IsDigest](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadAttributes.IsDigest.aspx) -Attribut in der [Attributes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.Attributes.aspx) -Eigenschaft angewendet. Um herauszufinden, ob ein Thread mehr als zwei Threads hat, überprüfen Sie die [TotalReplyCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.TotalReplyCount.aspx) -Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="dacfc-p109">A digest thread represents a compact version of a conversation—it contains the thread's root post and two most recent replies. You can identify a digest thread by checking whether the thread has the  [IsDigest](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadAttributes.IsDigest.aspx) attribute applied in its [Attributes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.Attributes.aspx) property. To see whether a thread has more than two threads, check the [TotalReplyCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.TotalReplyCount.aspx) property.</span></span>
  
    
    
<span data-ttu-id="dacfc-p110">Zum Optimieren der Leistung, wenn ein Thread mehr als zwei Antworten enthält, gibt der Server einen Digest-Thread zurück. Wenn Sie alle Antworten für einen Thread abrufen möchten, rufen Sie die  [SocialFeedManager.GetFullThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFullThread.aspx) -Methode, und übergeben Sie die Thread-ID</span><span class="sxs-lookup"><span data-stu-id="dacfc-p110">To optimize performance, when a thread contains more than two replies, the server returns a digest thread. If you want to get all the replies for a thread, call the  [SocialFeedManager.GetFullThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFullThread.aspx) method and pass in the thread ID.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="dacfc-148">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="dacfc-148">See also</span></span>
<span data-ttu-id="dacfc-149"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="dacfc-149"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="dacfc-150">Arbeiten mit sozialen Feeds in SharePoint</span><span class="sxs-lookup"><span data-stu-id="dacfc-150">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  
-  <span data-ttu-id="dacfc-151">[SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) im .NET Client-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="dacfc-151">[SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) in the .NET client object model</span></span>
    
  
-  <span data-ttu-id="dacfc-152">[SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx) im JavaScript-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="dacfc-152">[SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx) in the JavaScript object model</span></span>
    
  
-  <span data-ttu-id="dacfc-153">[SPSocialThread](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialThread.aspx) im Server-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="dacfc-153">[SPSocialThread](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialThread.aspx) in the server object model</span></span>
    
  

