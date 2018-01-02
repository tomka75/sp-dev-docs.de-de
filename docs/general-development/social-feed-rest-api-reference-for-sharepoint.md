---
title: "REST-API-Referenz für sozialen Feed für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f1cb914f-1e91-4e23-bf53-d2ab323eac13
ms.openlocfilehash: 2cb778e590d8c504bcaf5b962a6345cf581e9e6b
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="social-feed-rest-api-reference-for-sharepoint"></a><span data-ttu-id="43d79-102">REST-API-Referenz für sozialen Feed für SharePoint</span><span class="sxs-lookup"><span data-stu-id="43d79-102">Social feed REST API reference for SharePoint</span></span>
<span data-ttu-id="43d79-p101">Suchen Sie SharePoint-REST-Endpunkte, um mithilfe der **SocialRestFeedManager**-Ressource Beiträge in sozialen Feeds zu lesen und zu verfassen. Sie können den REST-Dienst (Representational State Transfer) in SharePoint für die gleichen Dinge verwenden, die Sie auch mit den .NET-Clientobjektmodellen und dem JavaScript-Objektmodell ausführen können. Der REST-Dienst macht Ressourcen verfügbar, die SharePoint-Objekten, -Eigenschaften und -Methoden entsprechen. Um den REST-Dienst zu verwenden, erstellen und senden Sie HTTP- **GET**- und **POST**-Anforderungen an die Ressourcenendpunkte, die den Aufgaben entsprechen, die Sie ausführen möchten.</span><span class="sxs-lookup"><span data-stu-id="43d79-p101">Find SharePoint REST endpoints for reading and writing to social feeds by using the **SocialRestFeedManager** resource. You can use the SharePoint Representational State Transfer (REST) service to do the same things that you can do with the .NET client object models and the JavaScript object model. The REST service exposes resources that correspond to SharePoint objects, properties, and methods. To use the REST service, you build and send HTTP **GET** and **POST** requests to the resource endpoints that represent the tasks you want to do.</span></span>
  
    
    

<span data-ttu-id="43d79-107">Die Endpunkt-URIs für die meisten Feedaufgaben beginnen mit der **SocialRestFeedManager**-Ressource ( `social.feed`), gefolgt von der  `my`-Ressource oder der  `post`-Ressource:</span><span class="sxs-lookup"><span data-stu-id="43d79-107">The endpoint URIs for most feed tasks begin with the **SocialRestFeedManager** resource ( `social.feed`), followed by the  `my` resource or the `post` resource:</span></span>
- <span data-ttu-id="43d79-p102">Die  `my`-Ressource stellt den aktuellen Benutzer dar. Wenn diese inline im Endpunkt-URI verwendet wird, wird der Kontext der Anforderung auf den aktuellen Benutzer festgelegt.  `http://contoso.com/_api/social.feed/my/news` ruft beispielsweise den Newsfeed für den aktuellen Benutzer ab.</span><span class="sxs-lookup"><span data-stu-id="43d79-p102">The  `my` resource represents the current user. When used inline in the endpoint URI, it sets the context of the request to the current user. For example, `http://contoso.com/_api/social.feed/my/news` gets the newsfeed for the current user.</span></span>
    
  
- <span data-ttu-id="43d79-p103">Die  `post`-Ressource stellt einen bestimmten Thread oder Beitrag dar. Wenn diese inline im Endpunkt-URI verwendet wird, wird der Kontext der Anforderung auf den angegeben Thread oder Beitrag festgelegt.  `http://contoso.com/_api/social.feed/post/lock` sperrt beispielsweise den angegebenen Thread.</span><span class="sxs-lookup"><span data-stu-id="43d79-p103">The  `post` resource represents a specific thread or post. When used inline in the endpoint URI, it sets the context of the request to the specified thread or post. For example, `http://contoso.com/_api/social.feed/post/lock` locks the specified thread.</span></span>
    
  
<span data-ttu-id="43d79-p104">Wenn der Ressourcenendpunkt einen Parameter verwendet, werden die Parametermetadaten im URI oder im Anforderungstext angegeben. Der REST-Dienst gibt standardmäßig Antworten zurück, die im Atom-Protokoll formatiert sind, Sie können mithilfe von HTTP- **Accept**-Headern jedoch das JSON-Format anfordern. Unter  [Beispiel-REST-Anforderungen für den Feedaufgaben](social-feed-rest-api-reference-for-sharepoint.md#bk_exampleRequests) finden Sie Beispiele von vollständigen Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="43d79-p104">If the resource endpoint takes a parameter, the parameter metadata is specified in the URI or in the request body. By default, the REST service returns responses formatted in the Atom protocol, but you can request the JSON format by using HTTP **Accept** headers. See [Example REST requests for feed tasks](social-feed-rest-api-reference-for-sharepoint.md#bk_exampleRequests) for examples of complete requests.</span></span>
## <a name="resource-endpoints-for-feed-tasks"></a><span data-ttu-id="43d79-117">Ressourcenendpunkte für Feedaufgaben</span><span class="sxs-lookup"><span data-stu-id="43d79-117">Resource endpoints for feed tasks</span></span>
<span data-ttu-id="43d79-118"><a name="bk_Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-118"><a name="bk_Overview"> </a></span></span>


|<span data-ttu-id="43d79-119">**Endpunkt**</span><span class="sxs-lookup"><span data-stu-id="43d79-119">**Endpoint**</span></span>|<span data-ttu-id="43d79-120">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="43d79-120">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="43d79-121">My</span><span class="sxs-lookup"><span data-stu-id="43d79-121">My</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_my)|<span data-ttu-id="43d79-122">Ruft Informationen zu dem aktuellen Benutzer ab.</span><span class="sxs-lookup"><span data-stu-id="43d79-122">Gets information about the current user.</span></span>|
| [<span data-ttu-id="43d79-123">My/Feed/Post</span><span class="sxs-lookup"><span data-stu-id="43d79-123">My/Feed/Post</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myFeedPost)|<span data-ttu-id="43d79-124">Erstellt einen Stammbeitrag in dem Feed des aktuellen Benutzers.</span><span class="sxs-lookup"><span data-stu-id="43d79-124">Creates a root post in the current user's feed.</span></span>|
| [<span data-ttu-id="43d79-125">My/Feed</span><span class="sxs-lookup"><span data-stu-id="43d79-125">My/Feed</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myFeed)|<span data-ttu-id="43d79-126">Ruft den Feed der Aktivitäten des aktuellen Benutzers ab.</span><span class="sxs-lookup"><span data-stu-id="43d79-126">Gets the feed of activity by the current user.</span></span>|
| [<span data-ttu-id="43d79-127">My/News</span><span class="sxs-lookup"><span data-stu-id="43d79-127">My/News</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myNews)|<span data-ttu-id="43d79-128">Ruft den Feed der Aktivitäten des aktuellen Benutzers und von Personen und Inhalten ab, denen der Benutzer folgt.</span><span class="sxs-lookup"><span data-stu-id="43d79-128">Gets the feed of activity by the current user and by people and content the user is following.</span></span>|
| [<span data-ttu-id="43d79-129">My/TimelineFeed</span><span class="sxs-lookup"><span data-stu-id="43d79-129">My/TimelineFeed</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myTimelineFeed)|<span data-ttu-id="43d79-130">Ruft den Feed der Aktivitäten des aktuellen Benutzers und von Personen und Inhalten ab, denen der Benutzer folgt, sortiert nach dem Erstellungsdatum.</span><span class="sxs-lookup"><span data-stu-id="43d79-130">Gets the feed of activity by the current user and by people and content the user is following, sorted by created date.</span></span>|
| [<span data-ttu-id="43d79-131">My/Likes</span><span class="sxs-lookup"><span data-stu-id="43d79-131">My/Likes</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myLikes)|<span data-ttu-id="43d79-132">Ruft den Feed von Beiträgen ab, die dem aktuellen Benutzer gefallen.</span><span class="sxs-lookup"><span data-stu-id="43d79-132">Gets the feed of posts that the current user likes.</span></span>|
| [<span data-ttu-id="43d79-133">My/MentionFeed</span><span class="sxs-lookup"><span data-stu-id="43d79-133">My/MentionFeed</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myMentionFeed)|<span data-ttu-id="43d79-134">Ruft den Feed von Beiträgen ab, in denen der aktuelle Benutzer erwähnt wird.</span><span class="sxs-lookup"><span data-stu-id="43d79-134">Gets the feed of posts that mention the current user.</span></span>|
| [<span data-ttu-id="43d79-135">My/MentionFeed/ClearUnreadMentionCount</span><span class="sxs-lookup"><span data-stu-id="43d79-135">My/MentionFeed/ClearUnreadMentionCount</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myMentionFeedClearUnreadMentionCount)|<span data-ttu-id="43d79-136">Ruft den Feed von Beiträgen ab, in denen der aktuelle Benutzer erwähnt wird, und löscht die Anzahl ungelesener Erwähnungen.</span><span class="sxs-lookup"><span data-stu-id="43d79-136">Gets the feed of posts that mention the current user and clears the unread mention count.</span></span>|
| [<span data-ttu-id="43d79-137">My/UnreadMentionCount</span><span class="sxs-lookup"><span data-stu-id="43d79-137">My/UnreadMentionCount</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myUnreadMentionCount)|<span data-ttu-id="43d79-138">Ruft die Anzahl der ungelesenen Erwähnungen für den aktuellen Benutzer ab.</span><span class="sxs-lookup"><span data-stu-id="43d79-138">Gets the count of unread mentions for the current user.</span></span>|
| [<span data-ttu-id="43d79-139">Akteur</span><span class="sxs-lookup"><span data-stu-id="43d79-139">Actor</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_actor)|<span data-ttu-id="43d79-140">Ruft Informationen zu dem angegebenen und dem aktuellen Benutzer ab.</span><span class="sxs-lookup"><span data-stu-id="43d79-140">Gets information about the specified user and the current user.</span></span>|
| [<span data-ttu-id="43d79-141">Actor/Feed</span><span class="sxs-lookup"><span data-stu-id="43d79-141">Actor/Feed</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_actorFeed)|<span data-ttu-id="43d79-142">Ruft den Feed der Aktivitäten des angegebenen Benutzers ab.</span><span class="sxs-lookup"><span data-stu-id="43d79-142">Gets the feed of activity by the specified user.</span></span>|
| [<span data-ttu-id="43d79-143">Actor/Feed/Post</span><span class="sxs-lookup"><span data-stu-id="43d79-143">Actor/Feed/Post</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_actorFeedPost)|<span data-ttu-id="43d79-144">Erstellt einen Stammbeitrag in dem angegebenen Websitefeed.</span><span class="sxs-lookup"><span data-stu-id="43d79-144">Creates a root post in the specified site feed.</span></span>|
| [<span data-ttu-id="43d79-145">Post</span><span class="sxs-lookup"><span data-stu-id="43d79-145">Post</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_post)|<span data-ttu-id="43d79-146">Ruft einen vollständigen Thread ab, der den angegebenen Beitrag enthält.</span><span class="sxs-lookup"><span data-stu-id="43d79-146">Gets a full thread that contains the specified post.</span></span>|
| [<span data-ttu-id="43d79-147">Post/Reply</span><span class="sxs-lookup"><span data-stu-id="43d79-147">Post/Reply</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_postReply)|<span data-ttu-id="43d79-148">Postet eine Antwort auf den angegebenen Beitrag.</span><span class="sxs-lookup"><span data-stu-id="43d79-148">Posts a reply to the specified post.</span></span>|
| [<span data-ttu-id="43d79-149">Post/Delete</span><span class="sxs-lookup"><span data-stu-id="43d79-149">Post/Delete</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_postDelete)|<span data-ttu-id="43d79-150">Löscht den angegebenen Beitrag.</span><span class="sxs-lookup"><span data-stu-id="43d79-150">Deletes the specified post.</span></span>|
| [<span data-ttu-id="43d79-151">Post/Like</span><span class="sxs-lookup"><span data-stu-id="43d79-151">Post/Like</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_postLike)|<span data-ttu-id="43d79-152">Damit wird angegeben, dass der angegebene Beitrag dem aktuellen Benutzer gefällt.</span><span class="sxs-lookup"><span data-stu-id="43d79-152">Makes the current user a liker of the specified post.</span></span>|
| [<span data-ttu-id="43d79-153">Post/Unlike</span><span class="sxs-lookup"><span data-stu-id="43d79-153">Post/Unlike</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_postUnlike)|<span data-ttu-id="43d79-154">Entfernt den aktuellen Benutzer aus der Liste der Benutzer, denen der angegebene Beitrag gefällt.</span><span class="sxs-lookup"><span data-stu-id="43d79-154">Removes the current user from the list of likers for the specified post.</span></span>|
| [<span data-ttu-id="43d79-155">Post/Likers</span><span class="sxs-lookup"><span data-stu-id="43d79-155">Post/Likers</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_postLikers)|<span data-ttu-id="43d79-156">Ruft die Benutzer ab, denen der angegebene Beitrag gefällt.</span><span class="sxs-lookup"><span data-stu-id="43d79-156">Gets the users who like the specified post.</span></span>|
| [<span data-ttu-id="43d79-157">Post/Lock</span><span class="sxs-lookup"><span data-stu-id="43d79-157">Post/Lock</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_postLock)|<span data-ttu-id="43d79-158">Sperrt den angegebenen Thread.</span><span class="sxs-lookup"><span data-stu-id="43d79-158">Locks the specified thread.</span></span>|
| [<span data-ttu-id="43d79-159">Post/Unlock</span><span class="sxs-lookup"><span data-stu-id="43d79-159">Post/Unlock</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_postUnlock)|<span data-ttu-id="43d79-160">Hebt die Sperre für den angegebenen Thread auf.</span><span class="sxs-lookup"><span data-stu-id="43d79-160">Unlocks the specified thread.</span></span>|
   
> [!NOTE]
> <span data-ttu-id="43d79-161">Die folgenden Feed-bezogenen REST-Ressourcen verwenden für die Erstellung des Endpunkt-URI dasselbe Muster wie die übrigen SharePoint-REST-APIs. Im Fall von **CreateImageAttachment** senden Sie eine Anforderung des Typs **POST** an `http://<siteCollection>/<site>/_api/SP.Social.SocialFeedManager/CreateImageAttachment`. Im Fall von **GetPreview** senden Sie eine Anforderung des Typs **POST** an `http://<siteCollection>/<site>/_api/SP.Social.SocialFeedManager/GetPreview`. Im Fall von **SuppressThreadNotifications** senden Sie eine Anforderung des Typs **POST** an `http://<siteCollection>/<site>/_api/SP.Social.SocialFeedManager/SuppressThreadNotifications`.</span><span class="sxs-lookup"><span data-stu-id="43d79-161">**Note:** The following feed-related REST resources use the same pattern as the other SharePoint REST APIs to construct the endpoint URI.>  For **CreateImageAttachment**, send a `http://<siteCollection>/<site>/_api/SP.Social.SocialFeedManager/CreateImageAttachment` request to ****>  For **GetPreview**, send a `http://<siteCollection>/<site>/_api/SP.Social.SocialFeedManager/GetPreview` request to ****>  For **SuppressThreadNotifications**, send a `http://<siteCollection>/<site>/_api/SP.Social.SocialFeedManager/SuppressThreadNotifications` request to </span></span>
  
    
    


## <a name="my"></a><span data-ttu-id="43d79-162">Eigene</span><span class="sxs-lookup"><span data-stu-id="43d79-162">My</span></span>
<span data-ttu-id="43d79-163"><a name="bk_my"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-163"><a name="bk_my"> </a></span></span>

<span data-ttu-id="43d79-164">Ruft Informationen zu dem aktuellen Benutzer ab.</span><span class="sxs-lookup"><span data-stu-id="43d79-164">Gets information about the current user.</span></span>
  
    
    
<span data-ttu-id="43d79-p105">Der **my**-Endpunkt legt den aktuellen Benutzer als Kontext für alle nachfolgenden Ressourcen in dem URI fest.  `http://contoso.com/_api/social.feed/my/news` ruft z. B. den Newsfeed für den aktuellen Benutzer ab.</span><span class="sxs-lookup"><span data-stu-id="43d79-p105">The **my** endpoint sets the current user as the context for any subsequent resource in the URI. For example, `http://contoso.com/_api/social.feed/my/news` gets the newsfeed for the current user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-167">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-167">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-168">**GET** `http://<siteCollection>/<site>/_api/social.feed/my`</span><span class="sxs-lookup"><span data-stu-id="43d79-168">**GET** `http://<siteCollection>/<site>/_api/social.feed/my`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-169">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-169">Request parameter</span></span>

<span data-ttu-id="43d79-170">Keine</span><span class="sxs-lookup"><span data-stu-id="43d79-170">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43d79-171">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-171">Response</span></span>

<span data-ttu-id="43d79-172">Typ:  [SP.Social.SocialRestActor](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestActor)</span><span class="sxs-lookup"><span data-stu-id="43d79-172">Type:  [SP.Social.SocialRestActor](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestActor)</span></span>
  
    
    
<span data-ttu-id="43d79-173">Informationen über den aktuellen Benutzer.</span><span class="sxs-lookup"><span data-stu-id="43d79-173">Information about the current user.</span></span>
  
    
    
<span data-ttu-id="43d79-174">Sie können **SocialRestActor**-Eigenschaften einzeln im URI aufrufen,  `http://<siteCollection>/<site>/_api/social.feed/my/me` ruft z. B. nur die **Me**-Eigenschaft ab.</span><span class="sxs-lookup"><span data-stu-id="43d79-174">You can call **SocialRestActor** properties individually in the URI, for example `http://<siteCollection>/<site>/_api/social.feed/my/me` gets only the **Me** property.</span></span>
  
    
    
<span data-ttu-id="43d79-175">In den folgenden Antwortbeispielen sind Informationen zu dem aktuellen Benutzer dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-175">The following response example represents information about the current user.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/my",
    "uri":"http://serverName/sites/dev/_api/social.feed/my",
    "type":"SP.Social.SocialRestActor"
   },
  "FollowableItem":"domain\\username1",
  "FollowableItemActor":null,
  "Me":{
    "__metadata":{"type":"SP.Social.SocialActor"},
    "AccountName":"domain\\username1",
    "ActorType":0,
    "CanFollow":false,
    "ContentUri":null,
    "EmailAddress":null,
    "FollowedContentUri":null,
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
    "ImageUri":null,
    "IsFollowed":false,
    "LibraryUri":null,
    "Name":"User1 Name",
    "PersonalSiteUri":"http://serverName/my/personal/username1/",
    "Status":0,
    "StatusText":"This is post 2",
    "TagGuid":"00000000-0000-0000-0000-000000000000",
    "Title":null,
    "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
  }
}}
```


## <a name="myfeedpost"></a><span data-ttu-id="43d79-176">My/Feed/Post</span><span class="sxs-lookup"><span data-stu-id="43d79-176">My/Feed/Post</span></span>
<span data-ttu-id="43d79-177"><a name="bk_myFeedPost"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-177"><a name="bk_myFeedPost"> </a></span></span>

<span data-ttu-id="43d79-178">Erstellt einen Stammbeitrag in dem Feed des aktuellen Benutzers.</span><span class="sxs-lookup"><span data-stu-id="43d79-178">Creates a root post in the current user's feed.</span></span>
  
    
    
<span data-ttu-id="43d79-p106">Sie können nur im Kontext des aktuellen Benutzers Beiträge posten. Sie können keinen Stammbeitrag im Feed eines anderen Benutzers erstellen, Sie können aber auf den Beitrag eines anderen Benutzers antworten. Weitere Informationen finden Sie unter  [Post/Reply](social-feed-rest-api-reference-for-sharepoint.md#bk_postReply).</span><span class="sxs-lookup"><span data-stu-id="43d79-p106">You can post only in the context of the current user. You cannot create a root post in a different user's feed, but you can reply to another user's post. See  [Post/Reply](social-feed-rest-api-reference-for-sharepoint.md#bk_postReply).</span></span>
  
> [!NOTE]
> <span data-ttu-id="43d79-182">Verwechseln Sie diese `Post`-Ressource nicht mit der `Post`-Ressource, die einen bestimmten Thread oder Beitrag darstellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-182">`Post` Don't confuse this  `Post` resource with the  resource that represents a specific thread or post.</span></span>
  
    
    


### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-183">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-183">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-184">**POST** `http://<siteCollection>/<site>/_api/social.feed/my/feed/post`</span><span class="sxs-lookup"><span data-stu-id="43d79-184">**POST** `http://<siteCollection>/<site>/_api/social.feed/my/feed/post`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-185">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-185">Request parameter</span></span>

 <span data-ttu-id="43d79-186">_restCreationData_</span><span class="sxs-lookup"><span data-stu-id="43d79-186">_restCreationData_</span></span>
  
    
    
<span data-ttu-id="43d79-187">Typ:  [SP.Social.SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData)</span><span class="sxs-lookup"><span data-stu-id="43d79-187">Type:  [SP.Social.SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData)</span></span>
  
    
    
<span data-ttu-id="43d79-188">Eine **null**-ID und die Eigenschaften des neuen Beitrags, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-188">A **null** ID and the properties of the new post, as shown in the following example.</span></span>
  
    
    

```

"restCreationData":{
  "__metadata":{
    "type":"SP.Social.SocialRestPostCreationData"
  },
  "ID":null,
  "creationData":{
    "__metadata":{
      "type":"SP.Social.SocialPostCreationData"
    },
    "ContentText":"This post was published using REST.", 
    "UpdateStatusText":false
  }
}
```


### <a name="response"></a><span data-ttu-id="43d79-189">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-189">Response</span></span>

<span data-ttu-id="43d79-190">Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43d79-190">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43d79-191">Ein Thread, der den neuen Stammbeitrag enthält.</span><span class="sxs-lookup"><span data-stu-id="43d79-191">A thread that contains the new root post.</span></span>
  
    
    
<span data-ttu-id="43d79-192">Im folgenden Antwortbeispiel ist der Thread dargestellt, der den neuen Stammbeitrag enthält.</span><span class="sxs-lookup"><span data-stu-id="43d79-192">The following response example represents the thread that contains the new root post.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "SocialThread":{
    "__metadata":{"type":"SP.Social.SocialThread"},
    "Actors":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":"domain\\username1",
        "ActorType":0, 
        "CanFollow":false, 
        "ContentUri":null, 
        "EmailAddress":null, 
        "FollowedContentUri":null, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
        "ImageUri":null, 
        "IsFollowed":false, 
        "LibraryUri":null, 
        "Name":"User1 Name",
        "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
        "Status":0, 
        "StatusText":"",
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":null, 
        "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
      }]
    },
    "Attributes":6,
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "OwnerIndex":0,
    "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "PostReference":null, 
    "Replies":{"results":[]},
    "RootPost":{
      "__metadata":{"type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":23, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T19:31:57.204511Z",
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[]},
        "TotalCount":0
      },
      "ModifiedTime":"2013-04-17T19:31:57.204511Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":0,
    "ThreadType":0,
    "TotalReplyCount":0
  }
}}
```


## <a name="myfeed"></a><span data-ttu-id="43d79-193">My/Feed</span><span class="sxs-lookup"><span data-stu-id="43d79-193">My/Feed</span></span>
<span data-ttu-id="43d79-194"><a name="bk_myFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-194"><a name="bk_myFeed"> </a></span></span>

<span data-ttu-id="43d79-195">Ruft den Feed der Aktivitäten des aktuellen Benutzers ab ( **Personal**-Feedtyp).</span><span class="sxs-lookup"><span data-stu-id="43d79-195">Gets the feed of activity by the current user ( **Personal** feed type).</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-196">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-196">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-197">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/feed`</span><span class="sxs-lookup"><span data-stu-id="43d79-197">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/feed`</span></span>
  
    
    
 <span data-ttu-id="43d79-198">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/feed(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span><span class="sxs-lookup"><span data-stu-id="43d79-198">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/feed(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-199">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-199">Request parameter</span></span>

 <span data-ttu-id="43d79-200">_feedOptions_ (optional)</span><span class="sxs-lookup"><span data-stu-id="43d79-200">_feedOptions_ (optional)</span></span>
  
    
    
<span data-ttu-id="43d79-201">Typ:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span><span class="sxs-lookup"><span data-stu-id="43d79-201">Type:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span></span>
  
    
    
<span data-ttu-id="43d79-p107">Die maximale Anzahl von Threads, Datums-/Uhrzeitbereich und Sortierreihenfolge. Sie können optional beliebige Kombinationen dieser Eigenschaften angeben, Sie können beispielsweise nur die **MaxThreadCount**-Eigenschaft angeben.</span><span class="sxs-lookup"><span data-stu-id="43d79-p107">The maximum number of threads, date-time range, and sort order. You can optionally specify any combination of these properties, for example, you can specify only the **MaxThreadCount** property.</span></span>
  
    
    
<span data-ttu-id="43d79-p108">Sie können einen **@**-Alias verwenden, um Sonderzeichen zu übergeben.  `<siteUri>/_api/social.feed/my/feed(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` verwendet z. B. den **@v**-Alias, um das Zeichen **:** zu senden.</span><span class="sxs-lookup"><span data-stu-id="43d79-p108">You can use an **@** alias to pass special characters. For example, `<siteUri>/_api/social.feed/my/feed(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` uses the **@v** alias to send a **:** character.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43d79-206">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-206">Response</span></span>

<span data-ttu-id="43d79-207">Typ:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span><span class="sxs-lookup"><span data-stu-id="43d79-207">Type:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span></span>
  
    
    
<span data-ttu-id="43d79-208">Der persönliche Feed des aktuellen Benutzers.</span><span class="sxs-lookup"><span data-stu-id="43d79-208">The current user's personal feed.</span></span>
  
    
    
<span data-ttu-id="43d79-209">Im folgenden Antwortbeispiel ist der persönliche Feed des aktuellen Benutzers dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-209">The following response example represents the current user's personal feed.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/my/feed",
    "uri":"http://serverName/sites/dev/_api/social.feed/my/feed",
    "type":"SP.Social.SocialRestFeed"
  },
  "SocialFeed":{
    "__metadata":{"type":"SP.Social.SocialFeed"},
    "Attributes":1, 
    "NewestProcessed":"2013-04-15T06:10:11Z",
    "OldestProcessed":"2013-04-15T05:33:12Z",
    "Threads":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":null, 
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          },{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username2",
            "ActorType":0, 
            "CanFollow":true, 
            "ContentUri":null, 
            "EmailAddress":"username2@somecompany.com",
            "FollowedContentUri":null, 
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
            "IsFollowed":true, 
            "LibraryUri":null, 
            "Name":"User2 Name",
            "PersonalSiteUri":"http://serverName/my/personal/username2",
            "Status":6, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":"SOME TITLE",
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
          }]
        },
        "Attributes":6, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "PostReference":null, 
        "Replies":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialPost"},
            "Attachment":null, 
            "Attributes":23, 
            "AuthorIndex":1, 
            "CreatedTime":"2013-04-15T06:10:11.3480926Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.59c0273c6c7b41e784b496c9aaa909a8.17.24.S-1-5-21-2127521184-1604012920-1887927527-66602",
            "LikerInfo":{
              "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
              "IncludesCurrentUser":false,
              "Indexes":{"results":[]},
              "TotalCount":0
            },
            "ModifiedTime":"2013-04-15T06:10:11.3480926Z",
            "Overlays":{"results":[]},
            "PostType":1, 
            "PreferredImageUri":null, 
            "Source":{
              "__metadata":{"type":"SP.Social.SocialLink"},
              "Text":null, 
              "Uri":null
            },
            "Text":"This is a reply to post 1."
          }]
        },
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null,
          "Attributes":23, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-15T05:58:24Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":false,
            "Indexes":{"results":[]},
            "TotalCount":0
          },
          "ModifiedTime":"2013-04-15T06:10:11Z",
          "Overlays":{"results":[]},
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"This is post 1." 
        },
        "Status":0, 
        "ThreadType":0, 
        "TotalReplyCount":1
      },{
      "__metadata":{"type":"SP.Social.SocialThread"},
      "Actors":{
        "results":[{
          "__metadata":{"type":"SP.Social.SocialActor"},
          "AccountName":"domain\\username1",
          "ActorType":0, 
          "CanFollow":false, 
          "ContentUri":null, 
          "EmailAddress":null, 
          "FollowedContentUri":null, 
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
          "ImageUri":null, 
          "IsFollowed":false, 
          "LibraryUri":null, 
          "Name":"User1 Name",
          "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
          "Status":0, 
          "StatusText":"",
          "TagGuid":"00000000-0000-0000-0000-000000000000",
          "Title":null, 
          "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
        }]
      },
      "Attributes":6, 
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "OwnerIndex":0, 
      "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "PostReference":null, 
      "Replies":{"results":[]},
      "RootPost":{
        "__metadata":{"type":"SP.Social.SocialPost"},
        "Attachment":null, 
        "Attributes":23, 
        "AuthorIndex":0, 
        "CreatedTime":"2013-04-15T06:07:05Z",
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "LikerInfo":{
          "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
          "IncludesCurrentUser":false, 
          "Indexes":{"results":[]},
          "TotalCount":0},
          "ModifiedTime":"2013-04-15T06:07:05Z",
          "Overlays":{"results":[]},
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null,"Uri":null},
            "Text":"This is post 2." 
          }, 
          "Status":0, 
          "ThreadType":0, 
          "TotalReplyCount":0
        },{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":null, 
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          },{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username2",
            "ActorType":0, 
            "CanFollow":true, 
            "ContentUri":null, 
            "EmailAddress":"username2@somecompany.com",
            "FollowedContentUri":null, 
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
            "IsFollowed":true, 
            "LibraryUri":null, 
            "Name":"User2 Name",
            "PersonalSiteUri":"http://serverName/my/personal/username2",
            "Status":6, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":"SOME TITLE",
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
          }]
      },
      "Attributes":0, 
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.cecc0de3d7d04520bb87a181b24c105a.16.16.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "OwnerIndex":0, 
      "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
      "PostReference":{
        "__metadata":{"type":"SP.Social.SocialPostReference"},
        "Digest":null, 
        "Post":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":23, 
          "AuthorIndex":1, 
          "CreatedTime":"2013-04-15T05:05:13Z",
          "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":true, 
            "Indexes":{"results":[]},
            "TotalCount":1
          },
          "ModifiedTime":"2013-04-15T05:05:13Z",
          "Overlays":{
            "results":[{
              "__metadata":{"type":"SP.Social.SocialDataOverlay"},
              "ActorIndexes":{"results":[0]}, 
              "Index":1, 
              "Length":18, 
              "LinkUri":null, 
              "OverlayType":1
            }]
          },
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"@User1 Name presented at the conference."}, 
          "ThreadId":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
          "ThreadOwnerIndex":1
        },
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":14, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-15T05:33:12Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.cecc0de3d7d04520bb87a181b24c105a.16.16.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":null, 
          "ModifiedTime":"2013-04-15T05:33:12Z",
          "Overlays":{
            "results":[{
              "__metadata":{"type":"SP.Social.SocialDataOverlay"},
              "ActorIndexes":{"results":[0]}, 
              "Index":0, 
              "Length":18, 
              "LinkUri":null, 
              "OverlayType":1
            },{
            "__metadata":{"type":"SP.Social.SocialDataOverlay"},
              "ActorIndexes":{"results":[1]}, 
              "Index":35, 
              "Length":10, 
              "LinkUri":null, 
              "OverlayType":1
            }]
          },
          "PostType":0, 
          "PreferredImageUri":"http://serverName:80/_layouts/15/Images/Like.11x11x32.png",
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null,"Uri":null
          },
          "Text":"User1 Name liked a post by User2 Name."
        }, 
        "Status":0, 
        "ThreadType":1, 
        "TotalReplyCount":0
      }]
    },
    "UnreadMentionCount":1
  }
}}
```


## <a name="mynews"></a><span data-ttu-id="43d79-210">My/News</span><span class="sxs-lookup"><span data-stu-id="43d79-210">My/News</span></span>
<span data-ttu-id="43d79-211"><a name="bk_myNews"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-211"><a name="bk_myNews"> </a></span></span>

<span data-ttu-id="43d79-212">Ruft den Feed der Aktivitäten des aktuellen Benutzers und von Personen und Inhalten ab, denen der Benutzer folgt, sortiert nach dem Datum der letzten Änderung. **News**-Feedtyp).</span><span class="sxs-lookup"><span data-stu-id="43d79-212">Gets the feed of activity by the current user and by people and content the user is following, sorted by last modified date ( **News** feed type).</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-213">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-213">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-214">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/news`</span><span class="sxs-lookup"><span data-stu-id="43d79-214">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/news`</span></span>
  
    
    
 <span data-ttu-id="43d79-215">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/news(MaxThreadCount=10,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span><span class="sxs-lookup"><span data-stu-id="43d79-215">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/news(MaxThreadCount=10,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-216">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-216">Request parameter</span></span>

 <span data-ttu-id="43d79-217">_feedOptions_ (optional)</span><span class="sxs-lookup"><span data-stu-id="43d79-217">_feedOptions_ (optional)</span></span>
  
    
    
<span data-ttu-id="43d79-218">Typ:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span><span class="sxs-lookup"><span data-stu-id="43d79-218">Type:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span></span>
  
    
    
<span data-ttu-id="43d79-p109">Die maximale Anzahl von Threads, Datums-/Uhrzeitbereich und Sortierreihenfolge. Sie können optional beliebige Kombinationen dieser Eigenschaften angeben, Sie können beispielsweise nur die **MaxThreadCount**-Eigenschaft angeben.</span><span class="sxs-lookup"><span data-stu-id="43d79-p109">The maximum number of threads, date-time range, and sort order. You can optionally specify any combination of these properties, for example, you can specify only the **MaxThreadCount** property.</span></span>
  
    
    
<span data-ttu-id="43d79-p110">Sie können einen **@**-Alias verwenden, um Sonderzeichen zu übergeben.  `<siteUri>/_api/social.feed/my/News(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` verwendet z. B. den **@v**-Alias, um das Zeichen **:** zu senden.</span><span class="sxs-lookup"><span data-stu-id="43d79-p110">You can use an **@** alias to pass special characters. For example, `<siteUri>/_api/social.feed/my/News(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` uses the **@v** alias to send a **:** character.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43d79-223">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-223">Response</span></span>

<span data-ttu-id="43d79-224">Typ:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span><span class="sxs-lookup"><span data-stu-id="43d79-224">Type:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span></span>
  
    
    
<span data-ttu-id="43d79-225">Der Newsfeed des aktuellen Benutzers.</span><span class="sxs-lookup"><span data-stu-id="43d79-225">The current user's newsfeed.</span></span>
  
    
    
<span data-ttu-id="43d79-226">Im folgenden Antwortbeispiel ist der Newsfeed des aktuellen Benutzers dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-226">The following response example represents the current user's newsfeed.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/my/news",
    "uri":"http://serverName/sites/dev/_api/social.feed/my/news",
    "type":"SP.Social.SocialRestFeed"
  },
  "SocialFeed":{
    "__metadata":{"type":"SP.Social.SocialFeed"},
    "Attributes":1, 
    "NewestProcessed":"2013-04-15T06:10:11.4730902Z",
    "OldestProcessed":"2013-04-12T20:51:51Z",
    "Threads":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":"http://serverName:80/my/_layouts/15/MySite.aspx?MySiteRedirect=FollowedDocuments",
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          },{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username2",
            "ActorType":0, 
            "CanFollow":true, 
            "ContentUri":null, 
            "EmailAddress":"username2@somecompany.com",
            "FollowedContentUri":null, 
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
            "IsFollowed":true, 
            "LibraryUri":null, 
            "Name":"User2 Name",
            "PersonalSiteUri":"http://serverName/my/personal/username2",
            "Status":0, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":"SOME TITLE",
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
          }]
        },
        "Attributes":6, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "PostReference":null, 
        "Replies":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialPost"},
            "Attachment":null, 
            "Attributes":23, 
            "AuthorIndex":1, 
            "CreatedTime":"2013-04-15T06:10:11.3480926Z",
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.59c0273c6c7b41e784b496c9aaa909a8.17.24.S-1-5-21-2127521184-1604012920-1887927527-66602",
            "LikerInfo":{
              "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
              "IncludesCurrentUser":false, 
              "Indexes":{"results":[]},
              "TotalCount":0
            },
            "ModifiedTime":"2013-04-15T06:10:11.3480926Z",
            "Overlays":{"results":[]},
            "PostType":1, 
            "PreferredImageUri":null, 
            "Source":{
              "__metadata":{"type":"SP.Social.SocialLink"},
              "Text":null, 
              "Uri":null
            },
            "Text":"This is a reply to post 1." 
          }]
        },
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":23, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-15T05:58:24Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":false, 
            "Indexes":{"results":[]},
            "TotalCount":0},
            "ModifiedTime":"2013-04-15T06:10:11.4730902Z",
            "Overlays":{"results":[]},
            "PostType":0, 
            "PreferredImageUri":null, 
            "Source":{
              "__metadata":{"type":"SP.Social.SocialLink"},
              "Text":null, 
              "Uri":null
            },
            "Text":"This is post 1." 
          },
          "Status":0, 
          "ThreadType":0, 
          "TotalReplyCount":1
        },{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":"http://serverName:80/my/_layouts/15/MySite.aspx?MySiteRedirect=FollowedDocuments",
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          }]
        },
        "Attributes":6, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "PostReference":null, 
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":23, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-15T06:07:05.4804434Z","Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":false, 
            "Indexes":{"results":[]},
            "TotalCount":0
          },
          "ModifiedTime":"2013-04-15T06:07:05.4804434Z",
          "Overlays":{"results":[]},
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"This is post 2." 
        },
        "Status":0, 
        "ThreadType":0, 
        "TotalReplyCount":0
      }]
    },
    "UnreadMentionCount":1
  }
}}
```


## <a name="mytimelinefeed"></a><span data-ttu-id="43d79-227">My/TimelineFeed</span><span class="sxs-lookup"><span data-stu-id="43d79-227">My/TimelineFeed</span></span>
<span data-ttu-id="43d79-228"><a name="bk_myTimelineFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-228"><a name="bk_myTimelineFeed"> </a></span></span>

<span data-ttu-id="43d79-229">Ruft den Feed der Aktivitäten des aktuellen Benutzers und von Personen und Inhalten ab, denen der Benutzer folgt, sortiert nach dem Erstellungsdatum ( **Timeline**-Feedtyp).</span><span class="sxs-lookup"><span data-stu-id="43d79-229">Gets the feed of activity by the current user and by people and content the user is following, sorted by created date ( **Timeline** feed type).</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-230">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-230">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-231">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/timelinefeed`</span><span class="sxs-lookup"><span data-stu-id="43d79-231">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/timelinefeed`</span></span>
  
    
    
 <span data-ttu-id="43d79-232">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/timelinefeed(MaxThreadCount=10,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span><span class="sxs-lookup"><span data-stu-id="43d79-232">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/timelinefeed(MaxThreadCount=10,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-233">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-233">Request parameter</span></span>

 <span data-ttu-id="43d79-234">_feedOptions_ (optional)</span><span class="sxs-lookup"><span data-stu-id="43d79-234">_feedOptions_ (optional)</span></span>
  
    
    
<span data-ttu-id="43d79-235">Typ:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span><span class="sxs-lookup"><span data-stu-id="43d79-235">Type:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span></span>
  
    
    
<span data-ttu-id="43d79-p111">Die maximale Anzahl von Threads, Datums-/Uhrzeitbereich und Sortierreihenfolge. Sie können optional beliebige Kombinationen dieser Eigenschaften angeben, Sie können beispielsweise nur die **MaxThreadCount**-Eigenschaft angeben.</span><span class="sxs-lookup"><span data-stu-id="43d79-p111">The maximum number of threads, date-time range, and sort order. You can optionally specify any combination of these properties, for example, you can specify only the **MaxThreadCount** property.</span></span>
  
    
    
<span data-ttu-id="43d79-p112">Sie können einen **@**-Alias verwenden, um Sonderzeichen zu übergeben.  `<siteUri>/_api/social.feed/my/timelinefeed(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` verwendet z. B. den **@v**-Alias, um das Zeichen **:** zu senden.</span><span class="sxs-lookup"><span data-stu-id="43d79-p112">You can use an **@** alias to pass special characters. For example, `<siteUri>/_api/social.feed/my/timelinefeed(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` uses the **@v** alias to send a **:** character.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43d79-240">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-240">Response</span></span>

<span data-ttu-id="43d79-241">Typ:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span><span class="sxs-lookup"><span data-stu-id="43d79-241">Type:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span></span>
  
    
    
<span data-ttu-id="43d79-242">Der Zeitachsenfeed des aktuellen Benutzers.</span><span class="sxs-lookup"><span data-stu-id="43d79-242">The current user's timeline feed.</span></span>
  
    
    
<span data-ttu-id="43d79-243">Im folgenden Antwortbeispiel ist der Zeitachsenfeed des aktuellen Benutzers, sortiert nach Erstellungsdatum, dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-243">The following response example represents the current user's timeline feed, which is sorted by created date.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/my/timelinefeed",
    "uri":"http://serverName/sites/dev/_api/social.feed/my/timelinefeed",
    "type":"SP.Social.SocialRestFeed"
  },
  "SocialFeed":{
    "__metadata":{"type":"SP.Social.SocialFeed"},
    "Attributes":1, 
    "NewestProcessed":"2013-04-15T06:07:05.4804434Z",
    "OldestProcessed":"2013-04-12T20:51:51Z",
    "Threads":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":"http://serverName:80/my/_layouts/15/MySite.aspx?MySiteRedirect=FollowedDocuments",
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"This is post 2.", 
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          }]
        },
        "Attributes":6, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "PostReference":null, 
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":23, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-15T06:07:05.4804434Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":false, 
            "Indexes":{"results":[]},
            "TotalCount":0
          },
          "ModifiedTime":"2013-04-15T06:07:05.4804434Z",
          "Overlays":{"results":[]},
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"This is post 2." 
        },
        "Status":0, 
        "ThreadType":0, 
        "TotalReplyCount":0
      },{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":"http://serverName:80/my/_layouts/15/MySite.aspx?MySiteRedirect=FollowedDocuments",
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"This is post 2.", 
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          }]
        },
        "Attributes":6, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "PostReference":null, 
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":23, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-15T05:58:24Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":false, 
            "Indexes":{"results":[]},
            "TotalCount":0
          },
          "ModifiedTime":"2013-04-15T06:04:49Z",
          "Overlays":{"results":[]},
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"This is post 1." 
        },
        "Status":0, 
        "ThreadType":0, 
        "TotalReplyCount":0
      }]
    },
    "UnreadMentionCount":1
  }
}}
```


## <a name="mylikes"></a><span data-ttu-id="43d79-244">My/Likes</span><span class="sxs-lookup"><span data-stu-id="43d79-244">My/Likes</span></span>
<span data-ttu-id="43d79-245"><a name="bk_myLikes"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-245"><a name="bk_myLikes"> </a></span></span>

<span data-ttu-id="43d79-246">Ruft den Feed von Mikroblogbeiträgen ab, die dem aktuellen Benutzer gefallen, dargestellt durch den Threadtyp **LikeReference**.</span><span class="sxs-lookup"><span data-stu-id="43d79-246">Gets the feed of microblog posts that the current user likes, represented by **LikeReference** thread types.</span></span> <span data-ttu-id="43d79-247">Weitere Informationen finden Sie unter [Verweisthreads und Digestthreads in sozialen SharePoint-Feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="43d79-247">See [Reference threads and digest threads in SharePoint social feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-248">Struktur des Endpunkt-URI</span><span class="sxs-lookup"><span data-stu-id="43d79-248">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-249">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/likes`</span><span class="sxs-lookup"><span data-stu-id="43d79-249">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/likes`</span></span>
  
    
    
 <span data-ttu-id="43d79-250">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/likes(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span><span class="sxs-lookup"><span data-stu-id="43d79-250">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/likes(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-251">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-251">Request parameter</span></span>

 <span data-ttu-id="43d79-252">_feedOptions_ (optional)</span><span class="sxs-lookup"><span data-stu-id="43d79-252">_feedOptions_ (optional)</span></span>
  
    
    
<span data-ttu-id="43d79-253">Typ:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span><span class="sxs-lookup"><span data-stu-id="43d79-253">Type:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span></span>
  
    
    
<span data-ttu-id="43d79-p114">Die maximale Anzahl von Threads, Datums-/Uhrzeitbereich und Sortierreihenfolge. Sie können optional beliebige Kombinationen dieser Eigenschaften angeben, Sie können beispielsweise nur die **MaxThreadCount**-Eigenschaft angeben.</span><span class="sxs-lookup"><span data-stu-id="43d79-p114">The maximum number of threads, date-time range, and sort order. You can optionally specify any combination of these properties, for example, you can specify only the **MaxThreadCount** property.</span></span>
  
    
    
<span data-ttu-id="43d79-p115">Sie können optional Abrufoptionen in der Abfragezeichenfolge angeben. Sie können einen **@**-Alias verwenden, um Sonderzeichen zu übergeben.  `<siteUri>/_api/social.feed/my/likes(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` verwendet z. B. den **@v**-Alias, um das Zeichen **:** zu senden.</span><span class="sxs-lookup"><span data-stu-id="43d79-p115">You can optionally specify retrieval options in the query string. You can use an **@** alias to pass special characters. For example, `<siteUri>/_api/social.feed/my/likes(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` uses the **@v** alias to send a **:** character.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43d79-259">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-259">Response</span></span>

<span data-ttu-id="43d79-260">Typ:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span><span class="sxs-lookup"><span data-stu-id="43d79-260">Type:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span></span>
  
    
    
<span data-ttu-id="43d79-261">Ein Feed, der Beiträge enthält, die dem aktuellen Benutzer gefallen.</span><span class="sxs-lookup"><span data-stu-id="43d79-261">A feed that contains posts that the current user likes.</span></span>
  
    
    
<span data-ttu-id="43d79-p116">Im folgenden Antwortbeispiel ist ein Verweis auf einen Beitrag dargestellt, der dem aktuellen Benutzer gefällt. Der Thread ist ein **LikeReference**-Threadtyp (Wert = **1**), dessen **PostReference**-Eigenschaft auf den tatsächlichen Beitrag verweist.</span><span class="sxs-lookup"><span data-stu-id="43d79-p116">The following response example represents a reference to a post that the current user likes. The thread is a **LikeReference** thread type (value = **1**) whose **PostReference** property references the actual post.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/my/likes",
    "uri":"http://serverName/sites/dev/_api/social.feed/my/likes",
    "type":"SP.Social.SocialRestFeed"
  },
  "SocialFeed":{
    "__metadata":{"type":"SP.Social.SocialFeed"}.
    "Attributes":1,
    "NewestProcessed":"2013-04-15T05:33:12Z",
    "OldestProcessed":"2013-04-15T05:33:12Z",
    "Threads":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0,
            "CanFollow":false,
            "ContentUri":null,
            "EmailAddress":null,
            "FollowedContentUri":null,
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"This is post 2",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null,
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          },{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username2",
            "ActorType":0, 
            "CanFollow":true, 
            "ContentUri":null, 
            "EmailAddress":"username2@somecompany.com",
            "FollowedContentUri":null, 
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
            "IsFollowed":true, 
            "LibraryUri":null, 
            "Name":"User2 Name",
            "PersonalSiteUri":"http://serverName/my/personal/username2",
            "Status":6, 
            "StatusText":"@User1 Name presented at the conference.",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":"SOME TITLE",
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"}]
          },
          "Attributes":0, 
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.cecc0de3d7d04520bb87a181b24c105a.16.16.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "OwnerIndex":0, 
          "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
          "PostReference":{
            "__metadata":{"type":"SP.Social.SocialPostReference"},
            "Digest":null, 
            "Post":{
              "__metadata":{"type":"SP.Social.SocialPost"},
              "Attachment":null, 
              "Attributes":23, 
              "AuthorIndex":1, 
              "CreatedTime":"2013-04-15T05:05:13Z",
              "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
              "LikerInfo":{
                "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
                "IncludesCurrentUser":true, 
                "Indexes":{"results":[]},
                "TotalCount":1
              },
              "ModifiedTime":"2013-04-15T05:05:13Z",
              "Overlays":{
                "results":[{
                  "__metadata":{"type":"SP.Social.SocialDataOverlay"},
                  "ActorIndexes":{"results":[0]}, 
                  "Index":1, 
                  "Length":18, 
                  "LinkUri":null, 
                  "OverlayType":1
                }]
              },
              "PostType":0, 
              "PreferredImageUri":null, 
              "Source":{
                "__metadata":{"type":"SP.Social.SocialLink"},
                "Text":null, 
                "Uri":null
              },
              "Text":"@User1 Name presented at the conference." 
            },
            "ThreadId":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
            "ThreadOwnerIndex":1
          },
          "Replies":{"results":[]},
          "RootPost":{
            "__metadata":{"type":"SP.Social.SocialPost"},
            "Attachment":null, 
            "Attributes":14, 
            "AuthorIndex":0, 
            "CreatedTime":"2013-04-15T05:33:12Z",
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.cecc0de3d7d04520bb87a181b24c105a.16.16.S-1-5-21-2127521184-1604012920-1887927527-66602",
            "LikerInfo":null, 
            "ModifiedTime":"2013-04-15T05:33:12Z",
            "Overlays":{
              "results":[{
                "__metadata":{"type":"SP.Social.SocialDataOverlay"},
                "ActorIndexes":{"results":[0]}, 
                "Index":0, 
                "Length":18, 
                "LinkUri":null, 
                "OverlayType":1
              },{
                "__metadata":{"type":"SP.Social.SocialDataOverlay"},
                "ActorIndexes":{"results":[1]}, 
                "Index":35, 
                "Length":10, 
                "LinkUri":null, 
                "OverlayType":1
              }]
            },
            "PostType":0, 
            "PreferredImageUri":"http://serverName:80/_layouts/15/Images/Like.11x11x32.png",
            "Source":{
              "__metadata":{"type":"SP.Social.SocialLink"},
              "Text":null, 
              "Uri":null
            },
            "Text":"User1 Name liked a post by User2 Name." 
          },
          "Status":0, 
          "ThreadType":1, 
          "TotalReplyCount":0
        }]
      },
    "UnreadMentionCount":1
  }
}}
```


## <a name="mymentionfeed"></a><span data-ttu-id="43d79-264">My/MentionFeed</span><span class="sxs-lookup"><span data-stu-id="43d79-264">My/MentionFeed</span></span>
<span data-ttu-id="43d79-265"><a name="bk_myMentionFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-265"><a name="bk_myMentionFeed"> </a></span></span>

<span data-ttu-id="43d79-266">Ruft den Feed von Mikroblogbeiträgen ab, in denen der aktuelle Benutzer erwähnt wird, dargestellt durch den Threadtyp **MentionReference**.</span><span class="sxs-lookup"><span data-stu-id="43d79-266">Gets the feed of microblog posts that mention the current user, represented by **MentionReference** thread types.</span></span> <span data-ttu-id="43d79-267">Weitere Informationen finden Sie unter [Verweisthreads und Digestthreads in sozialen SharePoint-Feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="43d79-267">See [Reference threads and digest threads in SharePoint social feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-268">Struktur des Endpunkt-URI</span><span class="sxs-lookup"><span data-stu-id="43d79-268">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-269">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/mentionfeed`</span><span class="sxs-lookup"><span data-stu-id="43d79-269">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/mentionfeed`</span></span>
  
    
    
 <span data-ttu-id="43d79-270">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/mentionfeed(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span><span class="sxs-lookup"><span data-stu-id="43d79-270">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/mentionfeed(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-271">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-271">Request parameter</span></span>

 <span data-ttu-id="43d79-272">_feedOptions_ (optional)</span><span class="sxs-lookup"><span data-stu-id="43d79-272">_feedOptions_ (optional)</span></span>
  
    
    
<span data-ttu-id="43d79-273">Typ:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span><span class="sxs-lookup"><span data-stu-id="43d79-273">Type:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span></span>
  
    
    
<span data-ttu-id="43d79-p118">Die maximale Anzahl von Threads, Datums-/Uhrzeitbereich und Sortierreihenfolge. Sie können optional beliebige Kombinationen dieser Eigenschaften angeben, Sie können beispielsweise nur die **MaxThreadCount**-Eigenschaft angeben.</span><span class="sxs-lookup"><span data-stu-id="43d79-p118">The maximum number of threads, date-time range, and sort order. You can optionally specify any combination of these properties, for example, you can specify only the **MaxThreadCount** property.</span></span>
  
    
    
<span data-ttu-id="43d79-p119">Sie können einen **@**-Alias verwenden, um Sonderzeichen zu übergeben.  `<siteUri>/_api/social.feed/my/likes(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` verwendet z. B. den **@v**-Alias, um das Zeichen **:** zu senden.</span><span class="sxs-lookup"><span data-stu-id="43d79-p119">You can use an **@** alias to pass special characters. For example, `<siteUri>/_api/social.feed/my/likes(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` uses the **@v** alias to send a **:** character.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43d79-278">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-278">Response</span></span>

<span data-ttu-id="43d79-279">Typ:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span><span class="sxs-lookup"><span data-stu-id="43d79-279">Type:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span></span>
  
    
    
<span data-ttu-id="43d79-280">Ein Feed, der Beiträge enthält, in denen der aktuelle Benutzer erwähnt wird.</span><span class="sxs-lookup"><span data-stu-id="43d79-280">A feed that contains posts that mention the current user.</span></span>
  
    
    
<span data-ttu-id="43d79-p120">Im folgenden Antwortbeispiel ist ein Thread dargestellt, in dem der aktuelle Benutzer erwähnt wird. Der Thread ist ein **MentionReference**-Threadtyp (Wert = **3**), dessen **PostReference**-Eigenschaft auf den tatsächlichen Beitrag verweist.</span><span class="sxs-lookup"><span data-stu-id="43d79-p120">The following response example represents one thread that mentions the current user. The thread is a **MentionReference** thread type (value = **3**) whose **PostReference** property references the actual post.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/my/mentionfeed",
    "uri":"http://serverName/sites/dev/_api/social.feed/my/mentionfeed",
    "type":"SP.Social.SocialRestFeed"
  },
  "SocialFeed":{
    "__metadata":{"type":"SP.Social.SocialFeed"},
    "Attributes":1,
    "NewestProcessed":"2013-04-15T05:05:19Z",
    "OldestProcessed":"2013-04-15T05:05:19Z",
    "Threads":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":null, 
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"This is post 2",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          },{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username2",
            "ActorType":0, 
            "CanFollow":true, 
            "ContentUri":null, 
            "EmailAddress":"username2@somecompany.com",
            "FollowedContentUri":null, 
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
            "IsFollowed":true, 
            "LibraryUri":null, 
            "Name":"User2 Name",
            "PersonalSiteUri":"http://serverName/my/personal/username2",
            "Status":6, 
            "StatusText":"@User1 Name presented at the conference.", 
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":"SOME TITLE",
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
          }]
        },
        "Attributes":0, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ec5198399300401fb44f0f5c9d8dea80.15.15.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
        "PostReference":{
          "__metadata":{"type":"SP.Social.SocialPostReference"},
          "Digest":null,
          "Post":{
            "__metadata":{"type":"SP.Social.SocialPost"},
            "Attachment":null,
            "Attributes":23,
            "AuthorIndex":1,
            "CreatedTime":"2013-04-15T05:05:12.0102795Z",
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
            "LikerInfo":{
              "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
              "IncludesCurrentUser":false,
              "Indexes":{"results":[]},
              "TotalCount":0
            },
            "ModifiedTime":"2013-04-15T05:05:12.0102795Z",
            "Overlays":{
              "results":[{
                "__metadata":{"type":"SP.Social.SocialDataOverlay"},
                "ActorIndexes":{"results":[0]},
                "Index":1,
                "Length":18,
                "LinkUri":null,
                "OverlayType":1
              }]
            },
            "PostType":0,
            "PreferredImageUri":null,
            "Source":{
              "__metadata":{"type":"SP.Social.SocialLink"},
              "Text":null,
              "Uri":null
            },
            "Text":"@User1 Name presented at the conference."
          },
          "ThreadId":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
          "ThreadOwnerIndex":1
        },
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null,
          "Attributes":14, 
          "AuthorIndex":1, 
          "CreatedTime":"2013-04-15T05:05:19Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ec5198399300401fb44f0f5c9d8dea80.15.15.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":null, 
          "ModifiedTime":"2013-04-15T05:05:19Z",
          "Overlays":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialDataOverlay"},
            "ActorIndexes":{"results":[1]}, 
            "Index":13, 
            "Length":10, 
            "LinkUri":null, 
            "OverlayType":1
          }]
        },
        "PostType":0, 
        "PreferredImageUri":"http://serverName:80/_layouts/15/Images/mention.11x11x32.png",
        "Source":{
          "__metadata":{"type":"SP.Social.SocialLink"},
          "Text":null,
          "Uri":null
        },
        "Text":"Mentioned by User2 Name."},
        "Status":0,
        "ThreadType":3,
        "TotalReplyCount":0
      }]
    },
    "UnreadMentionCount":1
  }
}}
```


## <a name="mymentionfeedclearunreadmentioncount"></a><span data-ttu-id="43d79-283">My/MentionFeed/ClearUnreadMentionCount</span><span class="sxs-lookup"><span data-stu-id="43d79-283">My/MentionFeed/ClearUnreadMentionCount</span></span>
<span data-ttu-id="43d79-284"><a name="bk_myMentionFeedClearUnreadMentionCount"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-284"><a name="bk_myMentionFeedClearUnreadMentionCount"> </a></span></span>

<span data-ttu-id="43d79-285">Ruft den Feed von Mikroblogbeiträgen ab, in denen der aktuelle Benutzer erwähnt wird, dargestellt durch den Threadtyp **MentionReference**. Setzt außerdem die Anzahl ungelesener Erwähnungen des Benutzers auf 0.</span><span class="sxs-lookup"><span data-stu-id="43d79-285">Gets the feed of microblog posts that mention the current user, represented by **MentionReference** thread types, and sets the user's unread mention count to 0.</span></span> <span data-ttu-id="43d79-286">Weitere Informationen finden Sie unter [Verweisthreads und Digestthreads in sozialen SharePoint-Feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="43d79-286">See [Reference threads and digest threads in SharePoint social feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-287">Struktur des Endpunkt-URI</span><span class="sxs-lookup"><span data-stu-id="43d79-287">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-288">**POST** `http://<siteCollection>/<site>/_api/social.feed/my/mentionfeed/clearunreadmentioncount`</span><span class="sxs-lookup"><span data-stu-id="43d79-288">**POST** `http://<siteCollection>/<site>/_api/social.feed/my/mentionfeed/clearunreadmentioncount`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-289">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-289">Request parameter</span></span>

 <span data-ttu-id="43d79-290">_feedOptions_</span><span class="sxs-lookup"><span data-stu-id="43d79-290">_feedOptions_</span></span>
  
    
    
<span data-ttu-id="43d79-291">Typ:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span><span class="sxs-lookup"><span data-stu-id="43d79-291">Type:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span></span>
  
    
    
<span data-ttu-id="43d79-292">Dieser Parameter muss als leere Zeichenfolge im **data**-Attribut des Anforderungstexts gesendet werden, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-292">This parameter must be sent as an empty string in the **data** attribute of the request body, as shown in the following example.</span></span>
  
    
    

```

'feedOptions': {
  '__metadata': {
    'type': 'SP.Social.SocialFeedOptions'
  }, 
}
```


### <a name="response"></a><span data-ttu-id="43d79-293">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-293">Response</span></span>

<span data-ttu-id="43d79-294">Typ:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span><span class="sxs-lookup"><span data-stu-id="43d79-294">Type:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span></span>
  
    
    
<span data-ttu-id="43d79-295">Der Erwähnungsfeed des aktuellen Benutzers.</span><span class="sxs-lookup"><span data-stu-id="43d79-295">The current user's mention feed.</span></span>
  
    
    
<span data-ttu-id="43d79-p122">Im folgenden Antwortbeispiel ist der Erwähnungsfeed des aktuellen Benutzers dargestellt. Der Thread ist ein **MentionReference**-Threadtyp (Wert = **3**), dessen **PostReference**-Eigenschaft auf den tatsächlichen Beitrag verweist. Die Anzahl ungelesener Erwähnungen wird gelöscht, nachdem der Feed abgerufen wurde.</span><span class="sxs-lookup"><span data-stu-id="43d79-p122">The following response example represents the current user's mention feed. The thread is a **MentionReference** thread type (value = **3**) whose **PostReference** property references the actual post. The unread mention count is cleared after the feed is retrieved.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/my/mentionfeed",
    "uri":"http://serverName/sites/dev/_api/social.feed/my/mentionfeed",
    "type":"SP.Social.SocialRestFeed" 
  },
  "SocialFeed":{
    "__metadata":{"type":"SP.Social.SocialFeed"},
    "Attributes":1,
    "NewestProcessed":"2013-04-15T05:05:19Z",
    "OldestProcessed":"2013-04-15T05:05:19Z",
    "Threads":{
      "results":[{
      "__metadata":{"type":"SP.Social.SocialThread"},
      "Actors":{
        "results":[{
          "__metadata":{"type":"SP.Social.SocialActor"},
          "AccountName":"domain\\username1",
          "ActorType":0, 
          "CanFollow":false, 
          "ContentUri":null, 
          "EmailAddress":null, 
          "FollowedContentUri":null, 
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
          "ImageUri":null, 
          "IsFollowed":false, 
          "LibraryUri":null, 
          "Name":"User1 Name",
          "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
          "Status":0, 
          "StatusText":"Posted with REST.", 
          "TagGuid":"00000000-0000-0000-0000-000000000000",
          "Title":null, 
          "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
        },{
          "__metadata":{"type":"SP.Social.SocialActor"},
          "AccountName":"domain\\username2",
          "ActorType":0, 
          "CanFollow":true, 
          "ContentUri":null, 
          "EmailAddress":"username2@somecompany.com",
          "FollowedContentUri":null, 
          "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
          "ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
          "IsFollowed":true, 
          "LibraryUri":null, 
          "Name":"User2 Name",
          "PersonalSiteUri":"http://serverName/my/personal/username2",
          "Status":6, 
          "StatusText":"This is post 1 from the specified user.", 
          "TagGuid":"00000000-0000-0000-0000-000000000000",
          "Title":"SOME TITLE",
          "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
        }]
      },
      "Attributes":0, 
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ec5198399300401fb44f0f5c9d8dea80.15.15.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "OwnerIndex":0, 
      "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
      "PostReference":{
        "__metadata":{"type":"SP.Social.SocialPostReference"},
        "Digest":null, 
        "Post":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":23, 
          "AuthorIndex":1, 
          "CreatedTime":"2013-04-15T05:05:12.0102795Z",
          "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":false, 
            "Indexes":{"results":[]},
            "TotalCount":0
          },
          "ModifiedTime":"2013-04-15T05:05:12.0102795Z",
          "Overlays":{
            "results":[{
              "__metadata":{"type":"SP.Social.SocialDataOverlay"},
              "ActorIndexes":{"results":[0]}, 
              "Index":1, 
              "Length":18, 
              "LinkUri":null, 
              "OverlayType":1
            }]
          },
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"@User1 Name presented at the conference."}, 
          "ThreadId":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
          "ThreadOwnerIndex":1
        },
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":14, 
          "AuthorIndex":1, 
          "CreatedTime":"2013-04-15T05:05:19Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ec5198399300401fb44f0f5c9d8dea80.15.15.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":null, 
          "ModifiedTime":"2013-04-15T05:05:19Z",
          "Overlays":{
            "results":[{
              "__metadata":{"type":"SP.Social.SocialDataOverlay"},
              "ActorIndexes":{"results":[1]}, 
              "Index":13, 
              "Length":10, 
              "LinkUri":null, 
              "OverlayType":1
            }]
          },
          "PostType":0, 
          "PreferredImageUri":"http://serverName:80/_layouts/15/Images/mention.11x11x32.png",
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"Mentioned by User2 Name."
        }, 
        "Status":0, 
        "ThreadType":3, 
        "TotalReplyCount":0
      }]
    },
    "UnreadMentionCount":1
  }
}}
```


## <a name="myunreadmentioncount"></a><span data-ttu-id="43d79-299">My/UnreadMentionCount</span><span class="sxs-lookup"><span data-stu-id="43d79-299">My/UnreadMentionCount</span></span>
<span data-ttu-id="43d79-300"><a name="bk_myUnreadMentionCount"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-300"><a name="bk_myUnreadMentionCount"> </a></span></span>

<span data-ttu-id="43d79-301">Ruft die Anzahl der ungelesenen Erwähnungen für den aktuellen Benutzer ab.</span><span class="sxs-lookup"><span data-stu-id="43d79-301">Gets the count of unread mentions for the current user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-302">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-302">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-303">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/unreadmentioncount`</span><span class="sxs-lookup"><span data-stu-id="43d79-303">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/unreadmentioncount`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-304">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-304">Request parameter</span></span>

<span data-ttu-id="43d79-305">Keine</span><span class="sxs-lookup"><span data-stu-id="43d79-305">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43d79-306">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-306">Response</span></span>

<span data-ttu-id="43d79-307">Typ: **Int32**</span><span class="sxs-lookup"><span data-stu-id="43d79-307">Type: **Int32**</span></span>
  
    
    
<span data-ttu-id="43d79-308">Die Anzahl ungelesener Erwähnungen für den aktuellen Benutzer.</span><span class="sxs-lookup"><span data-stu-id="43d79-308">The count of unread mentions for the current user.</span></span>
  
    
    
<span data-ttu-id="43d79-309">Im folgenden Antwortbeispiel ist die Anzahl 1 für ungelesene Erwähnungen dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-309">The following response example represents an unread mention count of 1.</span></span>
  
    
    



```

{"d":{"UnreadMentionCount":1}}
```


## <a name="actor"></a><span data-ttu-id="43d79-310">Akteur</span><span class="sxs-lookup"><span data-stu-id="43d79-310">Actor</span></span>
<span data-ttu-id="43d79-311"><a name="bk_actor"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-311"><a name="bk_actor"> </a></span></span>

<span data-ttu-id="43d79-312">Ruft Informationen zu dem angegebenen und dem aktuellen Benutzer ab.</span><span class="sxs-lookup"><span data-stu-id="43d79-312">Gets information about the specified user and the current user.</span></span>
  
> [!NOTE]
> <span data-ttu-id="43d79-313">Der Endpunkt `actor` legt den angegebenen Benutzer- oder Websitefeed als Kontext für alle zukünftigen Ressourcen in dem URI fest.</span><span class="sxs-lookup"><span data-stu-id="43d79-313">Note: The  `actor` endpoint sets the specified user or site feed as the context for any subsequent resource in the URI.</span></span> <span data-ttu-id="43d79-314">So ruft beispielsweise `http://contoso.com/_api/social.feed/actor(item='domain\\user')/feed` den persönlichen Feed des angegebenen Benutzers ab und `http://contoso.com/_api/social.feed/actor(item=@v)/feed?@v='http://<server>/<teamSite>/newsfeed.aspx'` den Websitefeed der angegebenen Teamwebsite.</span><span class="sxs-lookup"><span data-stu-id="43d79-314">For example, `http://contoso.com/_api/social.feed/actor(item='domain\\user')/feed` gets the personal feed for the specified user and `http://contoso.com/_api/social.feed/actor(item=@v)/feed?@v='http://<server>/<teamSite>/newsfeed.aspx'` gets the site feed for the specified team site.</span></span>
  
    
    


### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-315">Struktur des Endpunkt-URI</span><span class="sxs-lookup"><span data-stu-id="43d79-315">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-316">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')`</span><span class="sxs-lookup"><span data-stu-id="43d79-316">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')`</span></span>
  
    
    
 <span data-ttu-id="43d79-317">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span><span class="sxs-lookup"><span data-stu-id="43d79-317">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-318">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-318">Request parameter</span></span>

 <span data-ttu-id="43d79-319">_item_</span><span class="sxs-lookup"><span data-stu-id="43d79-319">_item_</span></span>
  
    
    
<span data-ttu-id="43d79-320">Typ: **String**</span><span class="sxs-lookup"><span data-stu-id="43d79-320">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43d79-321">Der Kontoname des angegebenen Benutzers.</span><span class="sxs-lookup"><span data-stu-id="43d79-321">The account name of the specified user.</span></span>
  
    
    
<span data-ttu-id="43d79-p124">Sie senden den  _item_-Parameter in der Abfragezeichenfolge. Sie können einen **@**-Alias verwenden, um Sonderzeichen zu übergeben.  `<siteUri>/_api/social.feed/actor(item=@v)?@v='i:0"%23".f|membership|user@domain.com'` verwendet z. B. den **@v**-Alias und die **"%23"**-Codierung, um das Zeichen **#** zu senden.</span><span class="sxs-lookup"><span data-stu-id="43d79-p124">You send the  _item_ parameter in the query string. You can use an **@** alias to pass special characters. For example, `<siteUri>/_api/social.feed/actor(item=@v)?@v='i:0"%23".f|membership|user@domain.com'` uses the **@v** alias and the **"%23"** encoding to send a **#** character.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43d79-325">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-325">Response</span></span>

<span data-ttu-id="43d79-326">Typ:  [SP.Social.SocialRestActor](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestActor)</span><span class="sxs-lookup"><span data-stu-id="43d79-326">Type:  [SP.Social.SocialRestActor](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestActor)</span></span>
  
    
    
<span data-ttu-id="43d79-327">Informationen zu dem angegebenen Benutzer und dem aktuellen Benutzer.</span><span class="sxs-lookup"><span data-stu-id="43d79-327">Information about the specified user and the current user.</span></span>
  
    
    
<span data-ttu-id="43d79-328">Sie können **SocialRestActor**-Eigenschaften einzeln im URI aufrufen,  `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')/followableitem` ruft z. B. nur die **FollowableItem**-Eigenschaft für den angegebenen Akteur ab.</span><span class="sxs-lookup"><span data-stu-id="43d79-328">You can call **SocialRestActor** properties individually in the URI, for example `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')/followableitem` gets only the **FollowableItem** property for the specified actor.</span></span>
  
    
    
<span data-ttu-id="43d79-329">Im folgenden Antwortbeispiel sind Informationen zu dem angegebenen und dem aktuellen Benutzer dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-329">The following response example represents information about the specified user and the current user.</span></span>
  
    
    



```
{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/actor(Item=@ai)/?@ai='domain\\username2'",
    "uri":"http://serverName/sites/dev/_api/social.feed/actor(Item=@ai)/?@ai='domain%5cusername2'",
    "type":"SP.Social.SocialRestActor"
  },
  "FollowableItem":"domain\\username2",
  "FollowableItemActor":{
    "__metadata":{"type":"SP.Social.SocialActor"},
    "AccountName":"domain\\username2",
    "ActorType":0,
    "CanFollow":true,
    "ContentUri":null,
    "EmailAddress":"username2@somecompany.com",
    "FollowedContentUri":null,
    "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
    "ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
    "IsFollowed":true,
    "LibraryUri":null,
    "Name":"User2 Name",
    "PersonalSiteUri":"http://serverName/my/personal/username2",
    "Status":0,
    "StatusText":"",
    "TagGuid":"00000000-0000-0000-0000-000000000000",
    "Title":"SOME TITLE",
    "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
  },
  "Me":{
    "__metadata":{"type":"SP.Social.SocialActor"},
    "AccountName":"domain\\username1",
    "ActorType":0,
    "CanFollow":false,
    "ContentUri":null,
    "EmailAddress":null,
    "FollowedContentUri":null,
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
    "ImageUri":null,
    "IsFollowed":false,
    "LibraryUri":null,
    "Name":"User1 Name",
    "PersonalSiteUri":"http://serverName/my/personal/username1/",
    "Status":0,
    "StatusText":"This is post 2",
    "TagGuid":"00000000-0000-0000-0000-000000000000",
    "Title":null,
    "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
  }
}}
```


## <a name="actorfeed"></a><span data-ttu-id="43d79-330">Actor/Feed</span><span class="sxs-lookup"><span data-stu-id="43d79-330">Actor/Feed</span></span>
<span data-ttu-id="43d79-331"><a name="bk_actorFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-331"><a name="bk_actorFeed"> </a></span></span>

<span data-ttu-id="43d79-332">Ruft den Feed der Aktivitäten des angegebenen Benutzers ab ( **Personal**-Feedtyp) oder ruft den angegebenen Websitefeed ab.</span><span class="sxs-lookup"><span data-stu-id="43d79-332">Gets the feed of activity by the specified user ( **Personal** feed type) or gets the specified site feed.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-333">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-333">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-334">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')/feed`</span><span class="sxs-lookup"><span data-stu-id="43d79-334">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')/feed`</span></span>
  
    
    
 <span data-ttu-id="43d79-335">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)/feed?@v='i:0"%23".f|membership|user@domain.com'`</span><span class="sxs-lookup"><span data-stu-id="43d79-335">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)/feed?@v='i:0"%23".f|membership|user@domain.com'`</span></span>
  
    
    
 <span data-ttu-id="43d79-336">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')/feed(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span><span class="sxs-lookup"><span data-stu-id="43d79-336">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')/feed(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span></span>
  
    
    
 <span data-ttu-id="43d79-337">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)/feed?@v='http://<teamSiteUri>/newsfeed.aspx'`</span><span class="sxs-lookup"><span data-stu-id="43d79-337">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)/feed?@v='http://<teamSiteUri>/newsfeed.aspx'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-338">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-338">Request parameter</span></span>

 <span data-ttu-id="43d79-339">_feedOptions_ (optional)</span><span class="sxs-lookup"><span data-stu-id="43d79-339">_feedOptions_ (optional)</span></span>
  
    
    
<span data-ttu-id="43d79-340">Typ:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span><span class="sxs-lookup"><span data-stu-id="43d79-340">Type:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span></span>
  
    
    
<span data-ttu-id="43d79-p125">Die maximale Anzahl von Threads, Datums-/Uhrzeitbereich und Sortierreihenfolge. Sie können optional beliebige Kombinationen dieser Eigenschaften angeben, Sie können beispielsweise nur die **MaxThreadCount**-Eigenschaft angeben.</span><span class="sxs-lookup"><span data-stu-id="43d79-p125">The maximum number of threads, date-time range, and sort order. You can optionally specify any combination of these properties, for example, you can specify only the **MaxThreadCount** property.</span></span>
  
    
    
<span data-ttu-id="43d79-p126">Sie können einen **@**-Alias verwenden, um Sonderzeichen zu übergeben.  `<siteUri>/_api/social.feed/actor(item=@v)/feed(NewerThan=@x)?@v='i:0"%23".f|membership|user@domain.com'&amp;@x=datetime'2013-01-01T08:00'` verwendet z. B. den **@v**-Alias und die **"%23"**-Codierung, um das Zeichen **#** zu senden, und den **@x**-Alias, um das Zeichen **:** zu senden.</span><span class="sxs-lookup"><span data-stu-id="43d79-p126">You can use an **@** alias to pass special characters. For example, `<siteUri>/_api/social.feed/actor(item=@v)/feed(NewerThan=@x)?@v='i:0"%23".f|membership|user@domain.com'&amp;@x=datetime'2013-01-01T08:00'` uses the **@v** alias and the **"%23"** encoding to send a **#** character, and the **@x** alias to send a **:** character.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43d79-345">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-345">Response</span></span>

<span data-ttu-id="43d79-346">Typ:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span><span class="sxs-lookup"><span data-stu-id="43d79-346">Type:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span></span>
  
    
    
<span data-ttu-id="43d79-347">Der persönliche Feed des angegebenen Benutzers oder der Websitefeed an dem angegebenen URI.</span><span class="sxs-lookup"><span data-stu-id="43d79-347">The personal feed of the specified user or the site feed at the specified URI.</span></span>
  
    
    
<span data-ttu-id="43d79-348">Im folgenden Antwortbeispiel ist der persönliche Feed des angegebenen Benutzers dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-348">The following response example represents personal feed of the specified user.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/actor(Item=@ai)/feed/?@ai='domain\\username2'",
    "uri":"http://serverName/sites/dev/_api/social.feed/actor(Item=@ai)/feed/?@ai='domain%5cusername2'",
    "type":"SP.Social.SocialRestFeed"
  },
  "SocialFeed":{
    "__metadata":{"type":"SP.Social.SocialFeed"},
    "Attributes":1, 
    "NewestProcessed":"2013-04-16T22:40:55Z",
    "OldestProcessed":"2013-04-16T22:40:07Z",
    "Threads":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username2",
            "ActorType":0, 
            "CanFollow":true, 
            "ContentUri":null, 
            "EmailAddress":"username2@somecompany.com",
            "FollowedContentUri":null, 
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":"http://serverName:80/my/User%20Photos/Profile%20Pictures/username2_MThumb.jpg",
            "IsFollowed":true, 
            "LibraryUri":null, 
            "Name":"User2 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username2",
            "Status":0, 
            "StatusText":"This is post 1 from the specified user.", 
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":"SOME TITLE",
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
          },{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":null, 
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName/my/personal/username1/",
            "Status":0, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          }]
        },
        "Attributes":0, 
        "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.4cb7a5d36cb14d62b0fb68ef98f9765e.15.15.S-1-5-21-124525095-708259637-1543119021-628175",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "PostReference":{
          "__metadata":{"type":"SP.Social.SocialPostReference"},
          "Digest":null, 
          "Post":null, 
          "ThreadId":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "ThreadOwnerIndex":1
        },
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":14, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-16T22:40:55Z",
          "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.4cb7a5d36cb14d62b0fb68ef98f9765e.15.15.S-1-5-21-124525095-708259637-1543119021-628175",
          "LikerInfo":null, 
          "ModifiedTime":"2013-04-16T22:40:55Z",
          "Overlays":{
            "results":[{
              "__metadata":{"type":"SP.Social.SocialDataOverlay"},
              "ActorIndexes":{"results":[0]}, 
              "Index":0, 
              "Length":10, 
              "LinkUri":null, 
              "OverlayType":1
            },{
              "__metadata":{"type":"SP.Social.SocialDataOverlay"},
              "ActorIndexes":{"results":[1]}, 
              "Index":32, 
              "Length":18, 
              "LinkUri":null, 
              "OverlayType":1
            }]
          },
          "PostType":0, 
          "PreferredImageUri":"http://serverName:80/_layouts/15/Images/RepliedTo.11x11x32.png",
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"User2 Name replied to a post by User1 Name." 
        },
        "Status":0, 
        "ThreadType":2, 
        "TotalReplyCount":0
      },{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username2",
            "ActorType":0, 
            "CanFollow":true, 
            "ContentUri":null, 
            "EmailAddress":"username2@somecompany.com",
            "FollowedContentUri":null, 
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":"http://serverName:80/my/User%20Photos/Profile%20Pictures/username2_MThumb.jpg",
            "IsFollowed":true,
            "LibraryUri":null,
            "Name":"User2 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username2",
            "Status":0, 
            "StatusText":"This is post 1 from the specified user.", 
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":"SOME TITLE",
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
          }]
        },
        "Attributes":6, 
        "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.b83675d28e264e69823205ad4e76df9f.14.14.S-1-5-21-124525095-708259637-1543119021-628175",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.b83675d28e264e69823205ad4e76df9f.14.14.S-1-5-21-124525095-708259637-1543119021-628175",
        "PostReference":null, 
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":23, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-16T22:40:07Z",
          "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.b83675d28e264e69823205ad4e76df9f.14.14.S-1-5-21-124525095-708259637-1543119021-628175",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":false, 
            "Indexes":{"results":[]},
            "TotalCount":0
          },
          "ModifiedTime":"2013-04-16T22:40:07Z",
          "Overlays":{"results":[]},
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"This is post 1 from the specified user."
        }, 
        "Status":0, 
        "ThreadType":0, 
        "TotalReplyCount":0
      }]
    },
    "UnreadMentionCount":0
  }
}}
```


## <a name="actorfeedpost"></a><span data-ttu-id="43d79-349">Actor/Feed/Post</span><span class="sxs-lookup"><span data-stu-id="43d79-349">Actor/Feed/Post</span></span>
<span data-ttu-id="43d79-350"><a name="bk_actorFeedPost"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-350"><a name="bk_actorFeedPost"> </a></span></span>

<span data-ttu-id="43d79-351">Erstellt einen Stammbeitrag in dem angegebenen Websitefeed.</span><span class="sxs-lookup"><span data-stu-id="43d79-351">Creates a root post in the specified site feed.</span></span>
  
    
    
<span data-ttu-id="43d79-p127">Sie können nur im Kontext des aktuellen Benutzers Beiträge posten. Sie können keinen Stammbeitrag im Feed eines anderen Benutzers erstellen, Sie können aber auf den Beitrag eines anderen Benutzers antworten. Weitere Informationen finden Sie unter  [Post/Reply](social-feed-rest-api-reference-for-sharepoint.md#bk_postReply).</span><span class="sxs-lookup"><span data-stu-id="43d79-p127">You can post only in the context of the current user. You cannot create a root post in a different user's feed, but you can reply to another user's post. See  [Post/Reply](social-feed-rest-api-reference-for-sharepoint.md#bk_postReply).</span></span>
  
> [!NOTE]
> <span data-ttu-id="43d79-355">Verwechseln Sie diese `Post`-Ressource nicht mit der `Post`-Ressource, die einen bestimmten Thread oder Beitrag darstellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-355">`Post` Don't confuse this  `Post` resource with the  resource that represents a specific thread or post.</span></span>
  
    
    


### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-356">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-356">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-357">**POST** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)/feed/post?@v='http://<siteCollection>/<teamSite>/newsfeed.aspx'`</span><span class="sxs-lookup"><span data-stu-id="43d79-357">**POST** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)/feed/post?@v='http://<siteCollection>/<teamSite>/newsfeed.aspx'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-358">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-358">Request parameter</span></span>

 <span data-ttu-id="43d79-359">_restCreationData_</span><span class="sxs-lookup"><span data-stu-id="43d79-359">_restCreationData_</span></span>
  
    
    
<span data-ttu-id="43d79-360">Typ:  [SP.Social.SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData)</span><span class="sxs-lookup"><span data-stu-id="43d79-360">Type:  [SP.Social.SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData)</span></span>
  
    
    
<span data-ttu-id="43d79-361">Eine **null**-ID und die Eigenschaften des neuen Beitrags, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-361">A **null** ID and the properties of the new post, as shown in the following example.</span></span>
  
    
    

```

'restCreationData':{
  '__metadata':{ 
    'type':'SP.Social.SocialRestPostCreationData'
  },
  'ID':null, 
  'creationData':{ 
    '__metadata':{ 
      'type':'SP.Social.SocialPostCreationData'
    },
    'ContentText':'This post was published using REST.', 
    'UpdateStatusText':false
  } 
}
```


### <a name="response"></a><span data-ttu-id="43d79-362">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-362">Response</span></span>

<span data-ttu-id="43d79-363">Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43d79-363">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43d79-364">Ein Thread, der den neuen Stammbeitrag enthält.</span><span class="sxs-lookup"><span data-stu-id="43d79-364">A thread that contains the new root post.</span></span>
  
    
    
<span data-ttu-id="43d79-365">Im folgenden Antwortbeispiel ist der Thread dargestellt, der den neuen Stammbeitrag enthält.</span><span class="sxs-lookup"><span data-stu-id="43d79-365">The following response example represents the thread that contains the new root post.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='8.c4bb19b167a448a3be9b597522152420.c305b669c2b649e9b820e7feabe3c095.c4bb19b167a448a3be9b597522152420.0c37852b34d0418e91c62ac25af4be5b.866d920d78d949a394f26073b767cb19.3.3.1'",
    "uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='8.c4bb19b167a448a3be9b597522152420.c305b669c2b649e9b820e7feabe3c095.c4bb19b167a448a3be9b597522152420.0c37852b34d0418e91c62ac25af4be5b.866d920d78d949a394f26073b767cb19.3.3.1'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"8.c4bb19b167a448a3be9b597522152420.c305b669c2b649e9b820e7feabe3c095.c4bb19b167a448a3be9b597522152420.0c37852b34d0418e91c62ac25af4be5b.866d920d78d949a394f26073b767cb19.3.3.1",
  "SocialThread":{
    "__metadata":{"type":"SP.Social.SocialThread"},
    "Actors":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":null, 
        "ActorType":2, 
        "CanFollow":true, 
        "ContentUri":"http://serverName:80/sites/teamSite",
        "EmailAddress":null, 
        "FollowedContentUri":null, 
        "Id":"8.c4bb19b167a448a3be9b597522152420.c305b669c2b649e9b820e7feabe3c095.c4bb19b167a448a3be9b597522152420.0c37852b34d0418e91c62ac25af4be5b",
        "ImageUri":null, 
        "IsFollowed":true, 
        "LibraryUri":null, 
        "Name":"Team Site",
        "PersonalSiteUri":null, 
        "Status":0, 
        "StatusText":null, 
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":null, 
        "Uri":"http://serverName:80/sites/teamSite"
      },{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":"domain\\username1",
        "ActorType":0, 
        "CanFollow":false, 
        "ContentUri":null, 
        "EmailAddress":null, 
        "FollowedContentUri":null, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
        "ImageUri":null, 
        "IsFollowed":false, 
        "LibraryUri":null, 
        "Name":"User1 Name",
        "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
        "Status":0, 
        "StatusText":"Posted with REST.", 
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":null, 
        "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
      }]
    },
    "Attributes":6,
    "Id":"8.c4bb19b167a448a3be9b597522152420.c305b669c2b649e9b820e7feabe3c095.c4bb19b167a448a3be9b597522152420.0c37852b34d0418e91c62ac25af4be5b.866d920d78d949a394f26073b767cb19.3.3.1",
    "OwnerIndex":0,
    "Permalink":"http://serverName/sites/teamSite/newsfeed.aspx?ThreadID=8.c4bb19b167a448a3be9b597522152420.c305b669c2b649e9b820e7feabe3c095.c4bb19b167a448a3be9b597522152420.0c37852b34d0418e91c62ac25af4be5b.866d920d78d949a394f26073b767cb19.3.3.1",
    "PostReference":null,
    "Replies":{"results":[]},
    "RootPost":{
      "__metadata":{"type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":23, 
      "AuthorIndex":1, 
      "CreatedTime":"2013-04-18T22:44:11.8485085Z",
      "Id":"8.c4bb19b167a448a3be9b597522152420.c305b669c2b649e9b820e7feabe3c095.c4bb19b167a448a3be9b597522152420.0c37852b34d0418e91c62ac25af4be5b.866d920d78d949a394f26073b767cb19.3.3.1",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[]},
        "TotalCount":0
      },
      "ModifiedTime":"2013-04-18T22:44:11.8485085Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":0, 
    "ThreadType":0, 
    "TotalReplyCount":0
  }
}}
```


## <a name="post"></a><span data-ttu-id="43d79-366">Beitrag</span><span class="sxs-lookup"><span data-stu-id="43d79-366">Post</span></span>
<span data-ttu-id="43d79-367"><a name="bk_post"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-367"><a name="bk_post"> </a></span></span>

<span data-ttu-id="43d79-368">Ruft einen vollständigen Thread ab, der den angegebenen Mikroblogbeitrag enthält.</span><span class="sxs-lookup"><span data-stu-id="43d79-368">Gets a full thread that contains the specified microblog post.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-369">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-369">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-370">**POST** `http://<siteCollection>/<site>/_api/social.feed/post`</span><span class="sxs-lookup"><span data-stu-id="43d79-370">**POST** `http://<siteCollection>/<site>/_api/social.feed/post`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-371">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-371">Request parameter</span></span>

 <span data-ttu-id="43d79-372">**ID**</span><span class="sxs-lookup"><span data-stu-id="43d79-372">**ID**</span></span>
  
    
    
<span data-ttu-id="43d79-373">Typ: **String**</span><span class="sxs-lookup"><span data-stu-id="43d79-373">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43d79-374">Der eindeutige Bezeichner des Beitrags, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-374">The unique identifier of the post, as shown in the following example.</span></span>
  
    
    

```

'ID':'1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.644240140e0b43379883ebcb859deaab.27.32.S-1-5-21-2127521184-1604012920-1887927527-66602'
```


### <a name="response"></a><span data-ttu-id="43d79-375">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-375">Response</span></span>

<span data-ttu-id="43d79-376">Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43d79-376">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43d79-377">Ein vollständiger Thread, der den angegebenen Beitrag enthält.</span><span class="sxs-lookup"><span data-stu-id="43d79-377">A full thread that contains the specified post.</span></span>
  
    
    
<span data-ttu-id="43d79-p128">Im folgenden Antwortbeispiel ist der vollständige Thread dargestellt, der den angegebenen Beitrag enthält. Im Gegensatz zu Digest-Threads (die nur die zwei letzten Antworten enthalten), enthält ein vollständiger Thread alle Antworten.</span><span class="sxs-lookup"><span data-stu-id="43d79-p128">The following response example represents the full thread that contains the specified post. Unlike digest threads (which contain only the two most recent replies), a full thread contains all replies.</span></span>
  
    
    



```
{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.62bff48184bd433b8f7b04f6ea76268b.27.27.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.62bff48184bd433b8f7b04f6ea76268b.27.27.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.62bff48184bd433b8f7b04f6ea76268b.27.27.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "SocialThread":{
    "__metadata":{"type":"SP.Social.SocialThread"},
    "Actors":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":"domain\\username1",
        "ActorType":0, 
        "CanFollow":false, 
        "ContentUri":null, 
        "EmailAddress":null, 
        "FollowedContentUri":null, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
        "ImageUri":null, 
        "IsFollowed":false, 
        "LibraryUri":null, 
        "Name":"User1 Name",
        "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
        "Status":0, 
        "StatusText":"Posted with REST.", 
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":null, 
        "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
      },{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":"domain\\username2",
        "ActorType":0, 
        "CanFollow":true, 
        "ContentUri":null, 
        "EmailAddress":"username2@somecompany.com",
        "FollowedContentUri":null, 
        "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b","ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
        "IsFollowed":true, 
        "LibraryUri":null,"Name":"User2 Name","PersonalSiteUri":"http://serverName/my/personal/username2","Status":6,"StatusText":"This is post 1 from the specified user.", 
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":"SOME TITLE",
        "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
      }]
    },
    "Attributes":6, 
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.62bff48184bd433b8f7b04f6ea76268b.27.27.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "OwnerIndex":0, 
    "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.62bff48184bd433b8f7b04f6ea76268b.27.27.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "PostReference":null, 
    "Replies":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialPost"},
        "Attachment":null, 
        "Attributes":23, 
        "AuthorIndex":1, 
        "CreatedTime":"2013-04-23T23:02:40Z",
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.644240140e0b43379883ebcb859deaab.27.32.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "LikerInfo":{
          "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
          "IncludesCurrentUser":false, 
          "Indexes":{"results":[]},
          "TotalCount":0
        },
        "ModifiedTime":"2013-04-23T23:02:40Z",
        "Overlays":{"results":[]},
        "PostType":1, 
        "PreferredImageUri":null, 
        "Source":{
          "__metadata":{"type":"SP.Social.SocialLink"},
          "Text":null, 
          "Uri":null
        },
        "Text":"This is a reply." 
      }]
    },
    "RootPost":{
      "__metadata":{"type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":23, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T19:45:45Z",
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.62bff48184bd433b8f7b04f6ea76268b.27.27.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[1]}, 
        "TotalCount":1
      },
      "ModifiedTime":"2013-04-23T23:02:41Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":0, 
    "ThreadType":0, 
    "TotalReplyCount":1
  }
}}
```


## <a name="postreply"></a><span data-ttu-id="43d79-380">Post/Reply</span><span class="sxs-lookup"><span data-stu-id="43d79-380">Post/Reply</span></span>
<span data-ttu-id="43d79-381"><a name="bk_postReply"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-381"><a name="bk_postReply"> </a></span></span>

<span data-ttu-id="43d79-382">Postet eine Antwort auf den angegebenen Beitrag.</span><span class="sxs-lookup"><span data-stu-id="43d79-382">Posts a reply to the specified post.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-383">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-383">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-384">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/reply`</span><span class="sxs-lookup"><span data-stu-id="43d79-384">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/reply`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-385">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-385">Request parameter</span></span>

 <span data-ttu-id="43d79-386">_restCreationData_</span><span class="sxs-lookup"><span data-stu-id="43d79-386">_restCreationData_</span></span>
  
    
    
<span data-ttu-id="43d79-387">Type:  [SP.Social.SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData)</span><span class="sxs-lookup"><span data-stu-id="43d79-387">Type:  [SP.Social.SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData)</span></span>
  
    
    
<span data-ttu-id="43d79-388">Die ID des Beitrags, auf den geantwortet werden soll, und die Eigenschaften der Antwort, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-388">The ID of the post to reply to and the properties of the reply, as shown in the following example.</span></span>
  
    
    

```

'restCreationData':{
  '__metadata':{
    'type': 'SP.Social.SocialRestPostCreationData'
  },
  'ID':'1.4975bef1e1bc42608c1dfae9f320c751.35c9fd7b79904800aaa5f74684bf0f75.623664921f034e8d814c000267d3e5e4.0c37852b34d0418e91c62ac25af4be5b.230d3c5272fc499f88ac0b74b2f4512f.119.119.S-1-5-21-124525095-708259637-1543119021-565461',
  'creationData':{
    '__metadata':{
      'type':'SP.Social.SocialPostCreationData'
    },
    'ContentText':'Posted with REST.', 
    'UpdateStatusText':false
  }
}
```


### <a name="response"></a><span data-ttu-id="43d79-389">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-389">Response</span></span>

<span data-ttu-id="43d79-390">Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43d79-390">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43d79-391">Ein Digest des geänderten Threads, der den angegebenen Beitrag enthält.</span><span class="sxs-lookup"><span data-stu-id="43d79-391">A digest of the modified thread that includes the specified post.</span></span>
  
    
    
<span data-ttu-id="43d79-392">Im folgenden Antwortbeispiel ist der Thread dargestellt, der den angegebenen Beitrag und die Antwort enthält.</span><span class="sxs-lookup"><span data-stu-id="43d79-392">The following response example represents the thread that contains the specified post and reply.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "SocialThread":{
    "__metadata":{"type":"SP.Social.SocialThread"},
    "Actors":{
      "results":[{
      "__metadata":{
        "type":"SP.Social.SocialActor"
      },
      "AccountName":"domain\\username1",
      "ActorType":0, 
      "CanFollow":false, 
      "ContentUri":null, 
      "EmailAddress":null, 
      "FollowedContentUri":null, 
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
      "ImageUri":null, 
      "IsFollowed":false, 
      "LibraryUri":null, 
      "Name":"User1 Name",
      "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
      "Status":0, 
      "StatusText":"Posted with REST.", 
      "TagGuid":"00000000-0000-0000-0000-000000000000",
      "Title":null,"Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"}
    ]}, 
    "Attributes":6, 
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "OwnerIndex":0, 
    "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "PostReference":null, 
    "Replies":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialPost"},
        "Attachment":null, 
        "Attributes":23, 
        "AuthorIndex":0, 
        "CreatedTime":"2013-04-17T20:52:51.0650454Z",
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ce3ac812293c4903b5c406efe01b9432.26.29.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "LikerInfo":{
          "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
          "IncludesCurrentUser":false, 
          "Indexes":{"results":[]},
          "TotalCount":0
        },
        "ModifiedTime":"2013-04-17T20:52:51.0650454Z",
        "Overlays":{"results":[]},
        "PostType":1, 
        "PreferredImageUri":null, 
        "Source":{
          "__metadata":{"type":"SP.Social.SocialLink"},
          "Text":null, 
          "Uri":null
        },
        "Text":"Replied with REST." 
      }]
    },
    "RootPost":{
      "__metadata":{"type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":23, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T19:33:17Z",
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[]},
        "TotalCount":0
      },
      "ModifiedTime":"2013-04-17T20:52:51.6900774Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":0, 
    "ThreadType":0, 
    "TotalReplyCount":1
  }
}}
```


## <a name="postdelete"></a><span data-ttu-id="43d79-393">Post/Delete</span><span class="sxs-lookup"><span data-stu-id="43d79-393">Post/Delete</span></span>
<span data-ttu-id="43d79-394"><a name="bk_postDelete"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-394"><a name="bk_postDelete"> </a></span></span>

<span data-ttu-id="43d79-p129">Löscht den Mikroblobbeitrag. Wenn es sich bei dem Beitrag um einen Stammbeitrag handelt, wird der gesamte Thread gelöscht.</span><span class="sxs-lookup"><span data-stu-id="43d79-p129">Deletes the specified microblog post. If the post is the root post, the whole thread is deleted.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-397">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-397">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-398">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/delete`</span><span class="sxs-lookup"><span data-stu-id="43d79-398">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/delete`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-399">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-399">Request parameter</span></span>

 <span data-ttu-id="43d79-400">**ID**</span><span class="sxs-lookup"><span data-stu-id="43d79-400">**ID**</span></span>
  
    
    
<span data-ttu-id="43d79-401">Typ: **String**</span><span class="sxs-lookup"><span data-stu-id="43d79-401">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43d79-402">Die ID des zu löschenden Beitrags, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-402">The ID of the post to delete, as shown in the following example.</span></span>
  
    
    

```

'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a><span data-ttu-id="43d79-403">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-403">Response</span></span>

<span data-ttu-id="43d79-404">Keine</span><span class="sxs-lookup"><span data-stu-id="43d79-404">None.</span></span>
  
    
    

```
{"d":{"Delete":null}}
```


## <a name="postlike"></a><span data-ttu-id="43d79-405">Post/Like</span><span class="sxs-lookup"><span data-stu-id="43d79-405">Post/Like</span></span>
<span data-ttu-id="43d79-406"><a name="bk_postLike"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-406"><a name="bk_postLike"> </a></span></span>

<span data-ttu-id="43d79-407">Damit wird angegeben, dass der angegebene Mikroblogbeitrag dem aktuellen Benutzer gefällt.</span><span class="sxs-lookup"><span data-stu-id="43d79-407">Makes the current user a liker of the specified microblog post.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-408">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-408">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-409">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/like`</span><span class="sxs-lookup"><span data-stu-id="43d79-409">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/like`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-410">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-410">Request parameter</span></span>

 <span data-ttu-id="43d79-411">**ID**</span><span class="sxs-lookup"><span data-stu-id="43d79-411">**ID**</span></span>
  
    
    
<span data-ttu-id="43d79-412">Typ: **String**</span><span class="sxs-lookup"><span data-stu-id="43d79-412">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43d79-413">Die ID des Beitrags, der mit "Gefällt mir" markiert werden soll, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-413">The ID of the post to like, as shown in the following example.</span></span>
  
    
    

```
'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a><span data-ttu-id="43d79-414">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-414">Response</span></span>

<span data-ttu-id="43d79-415">Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43d79-415">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43d79-416">Ein Digest-Thread, der den angegebenen Beitrag enthält.</span><span class="sxs-lookup"><span data-stu-id="43d79-416">A digest thread that contains the specified post.</span></span>
  
    
    
<span data-ttu-id="43d79-417">Im folgenden Antwortbeispiel ist der Thread dargestellt, der den Beitrag enthält, der mit "Gefällt mir" markiert wurde.</span><span class="sxs-lookup"><span data-stu-id="43d79-417">The following response example represents the thread that contains the liked post.</span></span>
  
    
    



```
{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "SocialThread":{
    "__metadata":{"type":"SP.Social.SocialThread"},
    "Actors":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":"domain\\username1",
        "ActorType":0, 
        "CanFollow":false, 
        "ContentUri":null, 
        "EmailAddress":null, 
        "FollowedContentUri":null, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
        "ImageUri":null, 
        "IsFollowed":false, 
        "LibraryUri":null, 
        "Name":"User1 Name",
        "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
        "Status":0, 
        "StatusText":"Posted with REST.", 
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":null, 
        "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
      }]
    },
    "Attributes":6, 
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "OwnerIndex":0, 
    "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "PostReference":null, 
    "Replies":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialPost"},
        "Attachment":null, 
        "Attributes":23, 
        "AuthorIndex":0, 
        "CreatedTime":"2013-04-17T20:52:51.0650454Z",
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ce3ac812293c4903b5c406efe01b9432.26.29.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "LikerInfo":{
          "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
          "IncludesCurrentUser":false, 
          "Indexes":{"results":[]},
          "TotalCount":0
        },
        "ModifiedTime":"2013-04-17T20:52:51.0650454Z",
        "Overlays":{"results":[]},
        "PostType":1, 
        "PreferredImageUri":null, 
        "Source":{
          "__metadata":{"type":"SP.Social.SocialLink"},
          "Text":null, 
          "Uri":null
        },
        "Text":"Replied with REST." 
      }]
    },
    "RootPost":{
      "__metadata":{"type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":23, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T19:33:17Z",
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":true, 
        "Indexes":{"results":[]},
        "TotalCount":1
      },
      "ModifiedTime":"2013-04-17T20:52:51Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":0, 
    "ThreadType":0, 
    "TotalReplyCount":1
  }
}}
```


## <a name="postunlike"></a><span data-ttu-id="43d79-418">Post/Unlike</span><span class="sxs-lookup"><span data-stu-id="43d79-418">Post/Unlike</span></span>
<span data-ttu-id="43d79-419"><a name="bk_postUnlike"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-419"><a name="bk_postUnlike"> </a></span></span>

<span data-ttu-id="43d79-p130">Entfernt den aktuellen Benutzer aus der Liste der Benutzer, denen der angegebene Mikroblogbeitrag gefällt. Wenn dem angegebenen Benutzer der Beitrag nicht gefällt, wird diese Anforderung ignoriert.</span><span class="sxs-lookup"><span data-stu-id="43d79-p130">Removes the current user from the list of likers for the specified microblog post. If the current user is not a liker of the post, this request is ignored.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-422">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-422">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-423">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/unlike`</span><span class="sxs-lookup"><span data-stu-id="43d79-423">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/unlike`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-424">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-424">Request parameter</span></span>

 <span data-ttu-id="43d79-425">**ID**</span><span class="sxs-lookup"><span data-stu-id="43d79-425">**ID**</span></span>
  
    
    
<span data-ttu-id="43d79-426">Typ: **String**</span><span class="sxs-lookup"><span data-stu-id="43d79-426">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43d79-427">Die ID des Beitrags, für den die Markierung "Gefällt mir" entfernt werden soll, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-427">The ID of the post to stop liking, as shown in the following example.</span></span>
  
    
    

```

'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a><span data-ttu-id="43d79-428">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-428">Response</span></span>

<span data-ttu-id="43d79-429">Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43d79-429">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43d79-430">Ein Digest des geänderten Threads, der den angegebenen Beitrag enthält.</span><span class="sxs-lookup"><span data-stu-id="43d79-430">A digest of the modified thread that includes the specified post.</span></span>
  
    
    
<span data-ttu-id="43d79-431">Im folgenden Antwortbeispiel ist der Thread dargestellt, der den Beitrag enthält, für den der Benutzer die Markierung "Gefällt mir" entfernt hat.</span><span class="sxs-lookup"><span data-stu-id="43d79-431">The following response example represents the thread that contains the post that the user stopped liking.</span></span>
  
    
    



```
{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "SocialThread":{
    "__metadata":{"type":"SP.Social.SocialThread"},
    "Actors":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":"domain\\username1",
        "ActorType":0, 
        "CanFollow":false, 
        "ContentUri":null, 
        "EmailAddress":null, 
        "FollowedContentUri":null, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
        "ImageUri":null, 
        "IsFollowed":false, 
        "LibraryUri":null, 
        "Name":"User1 Name",
        "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
        "Status":0, 
        "StatusText":"Posted with REST.", 
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":null, 
        "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
      }]
    },
    "Attributes":6, 
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "OwnerIndex":0, 
    "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "PostReference":null, 
    "Replies":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialPost"},
        "Attachment":null, 
        "Attributes":23, 
        "AuthorIndex":0, 
        "CreatedTime":"2013-04-17T20:52:51.0650454Z",
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ce3ac812293c4903b5c406efe01b9432.26.29.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "LikerInfo":{
          "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
          "IncludesCurrentUser":false, 
          "Indexes":{"results":[]},
          "TotalCount":0
        },
        "ModifiedTime":"2013-04-17T20:52:51.0650454Z",
        "Overlays":{"results":[]},
        "PostType":1, 
        "PreferredImageUri":null, 
        "Source":{
          "__metadata":{"type":"SP.Social.SocialLink"},
          "Text":null, 
          "Uri":null
        },
        "Text":"Replied with REST." 
      }]
    },
    "RootPost":{
      "__metadata":{"type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":23, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T19:33:17Z","Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[]},
        "TotalCount":0
      },
      "ModifiedTime":"2013-04-17T20:52:51Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":0,
    "ThreadType":0,
    "TotalReplyCount":1
  }
}}
```


## <a name="postlikers"></a><span data-ttu-id="43d79-432">Post/Likers</span><span class="sxs-lookup"><span data-stu-id="43d79-432">Post/Likers</span></span>
<span data-ttu-id="43d79-433"><a name="bk_postLikers"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-433"><a name="bk_postLikers"> </a></span></span>

<span data-ttu-id="43d79-434">Ruft die Benutzer ab, denen der angegebene Mikroblogbeitrag gefällt.</span><span class="sxs-lookup"><span data-stu-id="43d79-434">Gets the users who like the specified microblog post.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-435">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-435">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-436">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/likers`</span><span class="sxs-lookup"><span data-stu-id="43d79-436">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/likers`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-437">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-437">Request parameter</span></span>

 <span data-ttu-id="43d79-438">**ID**</span><span class="sxs-lookup"><span data-stu-id="43d79-438">**ID**</span></span>
  
    
    
<span data-ttu-id="43d79-439">Typ: **String**</span><span class="sxs-lookup"><span data-stu-id="43d79-439">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43d79-440">Die ID des Beitrags, der Benutzern gefallen soll, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-440">The ID of the post to get the likers for, as shown in the following example.</span></span>
  
    
    

```

'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a><span data-ttu-id="43d79-441">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-441">Response</span></span>

 <span data-ttu-id="43d79-442">**Likers**</span><span class="sxs-lookup"><span data-stu-id="43d79-442">**Likers**</span></span>
  
    
    
<span data-ttu-id="43d79-443">Typ:  [SP.Social.SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)[]</span><span class="sxs-lookup"><span data-stu-id="43d79-443">Type:  [SP.Social.SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)[]</span></span>
  
    
    
<span data-ttu-id="43d79-444">Die Benutzer, denen der angegebene Beitrag gefällt.</span><span class="sxs-lookup"><span data-stu-id="43d79-444">The users who like the specified post.</span></span>
  
    
    
<span data-ttu-id="43d79-445">Im folgenden Antwortbeispiel sind die Benutzer dargestellt, denen der angegebene Beitrag gefällt.</span><span class="sxs-lookup"><span data-stu-id="43d79-445">The following response example represents the users that like the specified post.</span></span>
  
    
    



```
{"d":{
  "Likers":{
    "results":[{
      "__metadata":{"type":"SP.Social.SocialActor"},
      "AccountName":"domain\\username1",
      "ActorType":0, 
      "CanFollow":false, 
      "ContentUri":null, 
      "EmailAddress":null, 
      "FollowedContentUri":null, 
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
      "ImageUri":null, 
      "IsFollowed":false, 
      "LibraryUri":null, 
      "Name":"User1 Name",
      "PersonalSiteUri":"http://serverName/my/personal/username1/",
      "Status":0, 
      "StatusText":"Posted with REST.", 
      "TagGuid":"00000000-0000-0000-0000-000000000000",
      "Title":null, 
      "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
    }]
  }
}}
```


## <a name="postlock"></a><span data-ttu-id="43d79-446">Post/Lock</span><span class="sxs-lookup"><span data-stu-id="43d79-446">Post/Lock</span></span>
<span data-ttu-id="43d79-447"><a name="bk_postLock"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-447"><a name="bk_postLock"> </a></span></span>

<span data-ttu-id="43d79-p131">Sperrt den angegebenen Thread. Wenn ein Thread gesperrt ist, können dem Thread erst Antwortbeiträge hinzugefügt werden, nachdem er entsperrt wurde.</span><span class="sxs-lookup"><span data-stu-id="43d79-p131">Locks the specified thread. If a thread is locked, no reply posts can be added to the thread until it is unlocked.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-450">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-450">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-451">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/lock`</span><span class="sxs-lookup"><span data-stu-id="43d79-451">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/lock`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-452">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-452">Request parameter</span></span>

 <span data-ttu-id="43d79-453">**ID**</span><span class="sxs-lookup"><span data-stu-id="43d79-453">**ID**</span></span>
  
    
    
<span data-ttu-id="43d79-454">Typ: **String**</span><span class="sxs-lookup"><span data-stu-id="43d79-454">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43d79-455">Die ID des zu sperrenden Threads, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-455">The ID of the thread to lock, as shown in the following example.</span></span>
  
    
    

```

'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a><span data-ttu-id="43d79-456">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-456">Response</span></span>

<span data-ttu-id="43d79-457">Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43d79-457">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43d79-458">Ein Digest des gesperrten Threads.</span><span class="sxs-lookup"><span data-stu-id="43d79-458">A digest of the locked thread.</span></span>
  
    
    
<span data-ttu-id="43d79-p132">Im folgend Antwortbeispiel ist ein gesperrter Thread dargestellt. Die **Attributes**-Eigenschaft des Threads enthält einen bitweisen Wert aus der  [SP.Social.SocialThreadAttributes](http://msdn.microsoft.com/library/21ff9f92-3223-bcc7-ceec-7b899ee29b6e%28Office.15%29.aspx)-Enumeration, der angibt, ob der Thread gesperrt ist.</span><span class="sxs-lookup"><span data-stu-id="43d79-p132">The following response example represents a locked thread. The **Attributes** property of the thread contains a bitwise value from the [SP.Social.SocialThreadAttributes](http://msdn.microsoft.com/library/21ff9f92-3223-bcc7-ceec-7b899ee29b6e%28Office.15%29.aspx) enumeration, which indicates whether the thread is locked.</span></span>
  
    
    



```
{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'
    uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "SocialThread":{
  "__metadata":{"type":"SP.Social.SocialThread"},
  "Actors":{
    "results":[{
      "__metadata":{"type":"SP.Social.SocialActor"},
      "AccountName":"domain\\username1",
      "ActorType":0, 
      "CanFollow":false, 
      "ContentUri":null, 
      EmailAddress":null, 
      "FollowedContentUri":null, 
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
      "ImageUri":null, 
      "IsFollowed":false, 
      "LibraryUri":null, 
      "Name":"User1 Name",
      "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
      "Status":0, 
      "StatusText":"Posted with REST.", 
      "TagGuid":"00000000-0000-0000-0000-000000000000",
      "Title":null, 
      "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
    }]
  },
  "Attributes":12,
  "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "OwnerIndex":0,
  "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "PostReference":null,
  "Replies":{
    "results":[{
      "__metadata":{"type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":22, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T20:52:51.0650454Z",
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ce3ac812293c4903b5c406efe01b9432.26.29.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[]},
        "TotalCount":0
      },
      "ModifiedTime":"2013-04-17T20:52:51.0650454Z",
      "Overlays":{"results":[]},
      "PostType":1, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Replied with REST." 
    }]
  },
  "RootPost":{
    "__metadata":{
      "type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":22, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T19:33:17Z",
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[]},
        "TotalCount":0
      },
      "ModifiedTime":"2013-04-17T20:52:51Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":0,
    "ThreadType":0,
    "TotalReplyCount":1
  }
}}
```


## <a name="postunlock"></a><span data-ttu-id="43d79-461">Post/Unlock</span><span class="sxs-lookup"><span data-stu-id="43d79-461">Post/Unlock</span></span>
<span data-ttu-id="43d79-462"><a name="bk_postUnlock"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-462"><a name="bk_postUnlock"> </a></span></span>

<span data-ttu-id="43d79-463">Hebt die Sperre für den angegebenen Thread auf.</span><span class="sxs-lookup"><span data-stu-id="43d79-463">Unlocks the specified thread.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43d79-464">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="43d79-464">Endpoint URI structure</span></span>

 <span data-ttu-id="43d79-465">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/unlock`</span><span class="sxs-lookup"><span data-stu-id="43d79-465">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/unlock`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43d79-466">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43d79-466">Request parameter</span></span>

 <span data-ttu-id="43d79-467">**ID**</span><span class="sxs-lookup"><span data-stu-id="43d79-467">**ID**</span></span>
  
    
    
<span data-ttu-id="43d79-468">Typ: **String**</span><span class="sxs-lookup"><span data-stu-id="43d79-468">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43d79-469">Die ID des zu entsperrenden Threads, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="43d79-469">The ID of the thread to unlock, as shown in the following example.</span></span>
  
    
    

```

'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a><span data-ttu-id="43d79-470">Antwort</span><span class="sxs-lookup"><span data-stu-id="43d79-470">Response</span></span>

<span data-ttu-id="43d79-471">Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43d79-471">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43d79-472">Ein Digest des entsperrten Threads.</span><span class="sxs-lookup"><span data-stu-id="43d79-472">A digest of the unlocked thread.</span></span>
  
    
    
<span data-ttu-id="43d79-p133">Im folgenden Antwortbeispiel ist ein entsperrter Thread dargestellt. Die **Attributes**-Eigenschaft des Threads enthält einen bitweisen Wert aus der  [SP.Social.SocialThreadAttributes](http://msdn.microsoft.com/library/21ff9f92-3223-bcc7-ceec-7b899ee29b6e%28Office.15%29.aspx)-Enumeration, der angibt, ob der Thread gesperrt ist.</span><span class="sxs-lookup"><span data-stu-id="43d79-p133">The following response example represents the unlocked thread. The **Attributes** property of the thread contains a bitwise value from the [SP.Social.SocialThreadAttributes](http://msdn.microsoft.com/library/21ff9f92-3223-bcc7-ceec-7b899ee29b6e%28Office.15%29.aspx) enumeration, which indicates whether the thread is locked.</span></span>
  
    
    



```
{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "SocialThread":{
    "__metadata":{"type":"SP.Social.SocialThread"},
    "Actors":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":"domain\\username1",
        "ActorType":0, 
        "CanFollow":false, 
        "ContentUri":null, 
        "EmailAddress":null, 
        "FollowedContentUri":null, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
        "ImageUri":null, 
        "IsFollowed":false, 
        "LibraryUri":null, 
        "Name":"User1 Name",
        "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
        "Status":0, 
        "StatusText":"Posted with REST.", 
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":null, 
        "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
      }
    ]}, 
    "Attributes":6, 
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "OwnerIndex":0, 
    "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "PostReference":null, 
    "Replies":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialPost"},
        "Attachment":null, 
        "Attributes":23, 
        "AuthorIndex":0, 
        "CreatedTime":"2013-04-17T20:52:51.0650454Z",
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ce3ac812293c4903b5c406efe01b9432.26.29.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "LikerInfo":{
          "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
          "IncludesCurrentUser":false, 
          "Indexes":{"results":[]},
          "TotalCount":0
        },
        "ModifiedTime":"2013-04-17T20:52:51.0650454Z",
        "Overlays":{"results":[]},
        "PostType":1, 
        "PreferredImageUri":null, 
        "Source":{
          "__metadata":{"type":"SP.Social.SocialLink"},
          "Text":null, 
          "Uri":null
        },
        "Text":"Replied with REST." 
      }]
    },
    "RootPost":{
      "__metadata":{"type":"SP.Social.SocialPost"},
      
      "Attachment":null, 
      "Attributes":23, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T19:33:17Z",
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[]},
        "TotalCount":0
      },
      "ModifiedTime":"2013-04-17T20:52:51Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":5,
    "ThreadType":0,
    "TotalReplyCount":1
  }
}}
```


## <a name="example-rest-requests-for-feed-tasks"></a><span data-ttu-id="43d79-475">Beispiel-REST-Anforderungen für den Feedaufgaben</span><span class="sxs-lookup"><span data-stu-id="43d79-475">Example REST requests for feed tasks</span></span>
<span data-ttu-id="43d79-476"><a name="bk_exampleRequests"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-476"><a name="bk_exampleRequests"> </a></span></span>

 <span data-ttu-id="43d79-p134">**GET**-Anforderungen für Feedaufgaben geben Parameter im URI oder im **url**-Attribut der Anforderung an. **POST**-Anforderungen geben Parameter im **data**-Attribut des Anforderungstexts im XML- oder JavaScript Object Notation (JSON)-Format an. HTTP-Anforderungen können in einer beliebigen Sprache erfolgen, einschließlich JavaScript und C#. In den folgenden Beispielanforderungen wird veranschaulicht, wie Anforderungen mithilfe von JavaScript erfolgen und wie Entitätsinformaitonen im JSON-Format übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="43d79-p134">**GET** requests for feed tasks specify parameters in the URI or in the **url** attribute of the request. **POST** requests specify parameters in the **data** attribute of the request body in XML or JavaScript Object Notation (JSON) format. You can make HTTP requests in any language, including JavaScript and C#. The following example requests show how to make requests by using JavaScript and how to pass entity information in JSON format.</span></span>
  
    
    
 <span data-ttu-id="43d79-481">**Beispiel:** Angeben des Parameters _ID_ im Anforderungstext (im Attribut **data**)</span><span class="sxs-lookup"><span data-stu-id="43d79-481">**Example:** How to specify the _ID_ parameter in the request body (in the **data** attribute).</span></span>
  
> [!NOTE]
> <span data-ttu-id="43d79-482">Die Werte für die Eigenschaft **Id** von Threads und Beiträgen sind zu lang, um als URL gesendet werden zu können. Sie müssen im Anforderungstext gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="43d79-482">Note: The values of thread and post **Id** properties are too long to send in a URL, so you have to send them in the request body.</span></span> <span data-ttu-id="43d79-483">Selbst schreibgeschützte Vorgänge, die logisch gesehen Anforderungen des Typs **GET** sind, müssen daher als Anforderungen des Typs **POST** gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="43d79-483">As a result, even read-only operations that are logically **GET** requests must be sent as **POST** requests.</span></span> <span data-ttu-id="43d79-484">Wenn Sie beispielsweise einen Thread abrufen möchten, müssen Sie eine Anforderung des Typs **POST** senden und den Wert **Id** des Threads als Entität im Anforderungstext übergeben.</span><span class="sxs-lookup"><span data-stu-id="43d79-484">For example, to get a thread, you have to send a **POST** request and pass the thread **Id** as an entity in the request body.</span></span>
  
    
    




```

var endpoint = siteUrl + '/_api/social.feed/post';
var postId = '1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602';

$.ajax({
    url: endpoint,
    type: 'POST',
    data: JSON.stringify({
        'ID': postId
    }),
    headers: {
        "accept": "application/json;odata=verbose",
        "content-type": "application/json;odata=verbose",
        "X-RequestDigest": $("#__REQUESTDIGEST").val()
    },
    success: function(data) { 
        var stringData = JSON.stringify(data);
        alert(stringData);

        // Converts the response data into an object that you can work with.
        var jsonObject = JSON.parse(stringData);
    },
    error: function(xhr, ajaxOptions, thrownError) {
        alert("Error: " + xhr.status + " " + thrownError + "\\nResponseText: " + xhr.responseText);
    }
});
```

 <span data-ttu-id="43d79-485">**Beispiel:** Veröffentlichen eines Stammbeitrags und Angeben des Parameters _restCreationData_ im Attribut **data**</span><span class="sxs-lookup"><span data-stu-id="43d79-485">**Example:** How to publish a root post and specify the _restCreationData_ parameter in the **data** attribute.</span></span>
  
    
    



```

var endpoint = <site url> + '/_api/social.feed/my/feed/post';
var postContent = 'Posted with REST.';

$.ajax({
    url: endpoint,
    type: 'POST',
    data: JSON.stringify({
        'restCreationData': {
            '__metadata': {
                'type': 'SP.Social.SocialRestPostCreationData'
            },
            'ID': null,
            'creationData': {
                '__metadata': {
                    'type': 'SP.Social.SocialPostCreationData'
                },
                'ContentText': postContent
            }
        }
    }),
    headers: {
        "accept": "application/json;odata=verbose",
        "content-type": "application/json;odata=verbose",
        "X-RequestDigest": $("#__REQUESTDIGEST").val()
    },
    success: function(data) { 
        var stringData = JSON.stringify(data);
        alert(stringData);

        // Converts the response data into an object that you can work with.
        var jsonObject = JSON.parse(stringData);
    },
    error: function(xhr, ajaxOptions, thrownError) {
        alert("Error: " + xhr.status + " " + thrownError + "\\nResponseText: " + xhr.responseText);
    }
});
```

<span data-ttu-id="43d79-486">Um eine Antwort auf einen angegebenen Thread zu veröffentlichen, senden Sie eine **POST**-Anforderung an die **Reply**-Ressource ( `<site url>/_api/social.feed/Post/Reply`), und übergeben **restCreationData**-Informationen, die die ID des Zielbeitrags enthalten.</span><span class="sxs-lookup"><span data-stu-id="43d79-486">To publish a reply to a specified thread, send a **POST** request to the **Reply** resource ( `<site url>/_api/social.feed/Post/Reply`) and pass **restCreationData** information that includes the target post ID.</span></span>
  
    
    



```

{ 'restCreationData': {
    '__metadata': { 'type': 'SP.Social.SocialRestPostCreationData' },
    'ID':'1.4975bef1e1bc42608c1dfae9f320c751.35c9fd7b79904800aaa5f74684bf0f75.623664921f034e8d814c000267d3e5e4.0c37852b34d0418e91c62ac25af4be5b.230d3c5272fc499f88ac0b74b2f4512f.119.119.S-1-5-21-124525095-708259637-1543119021-565461',
    'creationData':{
        '__metadata':{ 'type':'SP.Social.SocialPostCreationData' },
        'ContentText':'This is a reply to the specified post.',
        'UpdateStatusText':false
    }
} }
```


## <a name="resources-used-in-feed-related-rest-requests-and-responses"></a><span data-ttu-id="43d79-487">Ressourcen, die in den feedbezogene REST-Anforderungen und -Antworten verwendet werden</span><span class="sxs-lookup"><span data-stu-id="43d79-487">Resources used in feed-related REST requests and responses</span></span>
<span data-ttu-id="43d79-488"><a name="bk_FeedRelatedRestResources"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-488"><a name="bk_FeedRelatedRestResources"> </a></span></span>

<span data-ttu-id="43d79-489">Die folgenden REST-Ressourcen dienen als Parameter in clientseitigen Anforderungen oder werden in Serverantworten zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="43d79-489">The following REST resources are used as parameters in client-side requests or are returned in server responses.</span></span>
  
    
    

### <a name="spsocialsocialfeedoptions"></a><span data-ttu-id="43d79-490">SP.Social.SocialFeedOptions</span><span class="sxs-lookup"><span data-stu-id="43d79-490">SP.Social.SocialFeedOptions</span></span>
<span data-ttu-id="43d79-491"><a name="bk_SocialFeedOptions"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-491"><a name="bk_SocialFeedOptions"> </a></span></span>

<span data-ttu-id="43d79-492">Stellt Optionen dar, die Sie angeben können, wenn Sie einen Feed abrufen.</span><span class="sxs-lookup"><span data-stu-id="43d79-492">Represents options that you can specify when retrieving a feed.</span></span>
  
    
    
<span data-ttu-id="43d79-p136">In clientseitigen Anforderungen des Typs **GET** für Feeds können Sie optional Eigenschaften des Typs **SocialFeedOptions** als Parameter angeben. Diese Eigenschaften werden in der Abfragezeichenfolge angegeben.</span><span class="sxs-lookup"><span data-stu-id="43d79-p136">Client-side **GET** requests for feeds can optionally specify **SocialFeedOptions** properties as parameters. These properties are specified in the query string.</span></span>
  
    
    

|<span data-ttu-id="43d79-495">**Option**</span><span class="sxs-lookup"><span data-stu-id="43d79-495">**Option**</span></span>|<span data-ttu-id="43d79-496">**Typ**</span><span class="sxs-lookup"><span data-stu-id="43d79-496">**Type**</span></span>|<span data-ttu-id="43d79-497">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="43d79-497">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="43d79-498">MaxThreadCount</span><span class="sxs-lookup"><span data-stu-id="43d79-498">MaxThreadCount</span></span>|<span data-ttu-id="43d79-499">**Int32**</span><span class="sxs-lookup"><span data-stu-id="43d79-499">**Int32**</span></span>|<span data-ttu-id="43d79-p137">Die maximale Anzahl von Threads, die abgerufen werden. Die Standardanzahl ist 20.</span><span class="sxs-lookup"><span data-stu-id="43d79-p137">The maximum number of threads to retrieve. The default number is 20.</span></span>|
|<span data-ttu-id="43d79-502">NewerThan</span><span class="sxs-lookup"><span data-stu-id="43d79-502">NewerThan</span></span>|<span data-ttu-id="43d79-503">**String**</span><span class="sxs-lookup"><span data-stu-id="43d79-503">**String**</span></span>|<span data-ttu-id="43d79-p138">Die Grenze "neuer als" für den abzurufenden Zeitraum, als Zeichenfolgendarstellung eines **DateTime**-Objekts. Standardmäßig ist keine Grenze angegeben.</span><span class="sxs-lookup"><span data-stu-id="43d79-p138">The "newer than" boundary of the time span to retrieve, as a string representation of a **DateTime** object. The default is no specified boundary.</span></span>|
|<span data-ttu-id="43d79-506">OlderThan</span><span class="sxs-lookup"><span data-stu-id="43d79-506">OlderThan</span></span>|<span data-ttu-id="43d79-507">**String**</span><span class="sxs-lookup"><span data-stu-id="43d79-507">**String**</span></span>|<span data-ttu-id="43d79-p139">Die Grenze "älter als" für den abzurufenden Zeitraum, als Zeichenfolgendarstellung eines **DateTime**-Objekts. Standardmäßig ist keine Grenze angegeben.</span><span class="sxs-lookup"><span data-stu-id="43d79-p139">The "older than" boundary of the time span to retrieve, as a string representation of a **DateTime** object. The default is no specified boundary.</span></span>|
|<span data-ttu-id="43d79-510">SortOrder</span><span class="sxs-lookup"><span data-stu-id="43d79-510">SortOrder</span></span>|<span data-ttu-id="43d79-511">**Int32**</span><span class="sxs-lookup"><span data-stu-id="43d79-511">**Int32**</span></span>|<span data-ttu-id="43d79-512">Gibt die Sortierreihenfolge der Threads im Feed an.</span><span class="sxs-lookup"><span data-stu-id="43d79-512">The sort order of the threads in the feed.</span></span> <span data-ttu-id="43d79-513">Standardmäßig werden Threads nach dem Änderungsdatum sortiert. Nur der Zeitachsenfeed wird nach Erstellungsdatum sortiert.</span><span class="sxs-lookup"><span data-stu-id="43d79-513">The default sort order is by modified date, except for the timeline feed, which is sorted by created date.</span></span><br/>          <span data-ttu-id="43d79-514">Ist **0** gesetzt, werden Threads nach dem Änderungszeitpunkt sortiert, ausgehend vom Änderungszeitpunkt des zuletzt geänderten Beitrags.</span><span class="sxs-lookup"><span data-stu-id="43d79-514">**0** sorts threads by modified time, according to the most recent modification times of their posts.</span></span><br/>          <span data-ttu-id="43d79-515">Ist **1** gesetzt, werden Threads nach dem Erstellungszeitpunkt sortiert, basierend auf dem Erstellungszeitpunkt ihrer Stammbeiträge.</span><span class="sxs-lookup"><span data-stu-id="43d79-515">**1** sorts threads by created time, according to the creation times of their root posts.</span></span>|
   

  
    
    

  
    
    

### <a name="spsocialsocialrestactor"></a><span data-ttu-id="43d79-516">SP.Social.SocialRestActor</span><span class="sxs-lookup"><span data-stu-id="43d79-516">SP.Social.SocialRestActor</span></span>
<span data-ttu-id="43d79-517"><a name="bk_SocialRestActor"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-517"><a name="bk_SocialRestActor"> </a></span></span>

<span data-ttu-id="43d79-518">Stellt einen Benutzer, ein Dokument, eine Website oder ein Tag dar.</span><span class="sxs-lookup"><span data-stu-id="43d79-518">Represents a user, document, site, or tag.</span></span>
  
    
    
<span data-ttu-id="43d79-519">Der Server gibt eine **SocialRestActor**-Ressource in der Antwort an eine clientseitige Anforderung für Akteurinformationen zurück.</span><span class="sxs-lookup"><span data-stu-id="43d79-519">The server returns a **SocialRestActor** resource in the response to a client-side request for actor information.</span></span>
  
    
    
 <span data-ttu-id="43d79-520">**SocialRestActor** hat die folgenden Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="43d79-520">**SocialRestActor** has the following properties.</span></span>
  
    
    

|<span data-ttu-id="43d79-521">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="43d79-521">**Property**</span></span>|<span data-ttu-id="43d79-522">**Typ**</span><span class="sxs-lookup"><span data-stu-id="43d79-522">**Type**</span></span>|<span data-ttu-id="43d79-523">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="43d79-523">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="43d79-524">FollowableItem</span><span class="sxs-lookup"><span data-stu-id="43d79-524">FollowableItem</span></span>|<span data-ttu-id="43d79-525">**String**</span><span class="sxs-lookup"><span data-stu-id="43d79-525">**String**</span></span>|<span data-ttu-id="43d79-p141">Der eindeutige Bezeichner des angegebenen Akteurs. Gibt den Kontonamen für einen Benutzer oder den URI für ein Dokument, eine Website oder ein Tag zurück.</span><span class="sxs-lookup"><span data-stu-id="43d79-p141">The unique identifier of the specified actor. Returns the account name for a user or the URI for a document, site, or tag.</span></span>|
|<span data-ttu-id="43d79-528">FollowableItemActor</span><span class="sxs-lookup"><span data-stu-id="43d79-528">FollowableItemActor</span></span>| [<span data-ttu-id="43d79-529">SP.Social.SocialActor</span><span class="sxs-lookup"><span data-stu-id="43d79-529">SP.Social.SocialActor</span></span>](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)|<span data-ttu-id="43d79-p142">Der angegebene Benutzer. Gibt **null** zurück, wenn der Benutzer der aktuelle Benutzer ist oder wenn die Ressource kein Benutzertypakteur ist.</span><span class="sxs-lookup"><span data-stu-id="43d79-p142">The specified user. Returns **null** if the user is the current user or if the resource is not a user-type actor.</span></span>|
|<span data-ttu-id="43d79-532">Me</span><span class="sxs-lookup"><span data-stu-id="43d79-532">Me</span></span>| [<span data-ttu-id="43d79-533">SP.Social.SocialActor</span><span class="sxs-lookup"><span data-stu-id="43d79-533">SP.Social.SocialActor</span></span>](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)|<span data-ttu-id="43d79-534">Der aktuelle Benutzer.</span><span class="sxs-lookup"><span data-stu-id="43d79-534">The current user.</span></span>|
   

  
    
    

  
    
    

### <a name="spsocialsocialrestfeed"></a><span data-ttu-id="43d79-535">SP.Social.SocialRestFeed</span><span class="sxs-lookup"><span data-stu-id="43d79-535">SP.Social.SocialRestFeed</span></span>
<span data-ttu-id="43d79-536"><a name="bk_SocialRestFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-536"><a name="bk_SocialRestFeed"> </a></span></span>

<span data-ttu-id="43d79-537">Stellt einen Newsfeed für soziale Netzwerke dar.</span><span class="sxs-lookup"><span data-stu-id="43d79-537">Represents a social feed.</span></span>
  
    
    
<span data-ttu-id="43d79-538">Der Server gibt eine **SocialRestFeed**-Ressource in der Antwort an eine clientseitige Anforderung für Feedinhaltsinformationen zurück.</span><span class="sxs-lookup"><span data-stu-id="43d79-538">The server returns a **SocialRestFeed** resource in the response to a client-side request for feed content.</span></span>
  
    
    
 <span data-ttu-id="43d79-539">**SocialRestFeed** enthält ein umschlossenes Objekt des Typs [SP.Social.SocialFeed](http://msdn.microsoft.com/library/356c5475-2fd6-a655-c271-5d7f21af45e2%28Office.15%29.aspx) mit den folgenden Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="43d79-539">**SocialRestFeed** contains a wrapped [SP.Social.SocialFeed](http://msdn.microsoft.com/library/356c5475-2fd6-a655-c271-5d7f21af45e2%28Office.15%29.aspx) object, which has the following properties.</span></span>
  
    
    

|<span data-ttu-id="43d79-540">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="43d79-540">**Property**</span></span>|<span data-ttu-id="43d79-541">**Typ**</span><span class="sxs-lookup"><span data-stu-id="43d79-541">**Type**</span></span>|<span data-ttu-id="43d79-542">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="43d79-542">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="43d79-543">Attributes</span><span class="sxs-lookup"><span data-stu-id="43d79-543">Attributes</span></span>| [<span data-ttu-id="43d79-544">SP.Social.SocialFeedAttributes</span><span class="sxs-lookup"><span data-stu-id="43d79-544">SP.Social.SocialFeedAttributes</span></span>](http://msdn.microsoft.com/library/9ea7d3c5-7f96-88a6-5bdf-d7749b044ad3%28Office.15%29.aspx)|<span data-ttu-id="43d79-545">Ein bitweiser Satz von Attributen, die für den Feed gelten.</span><span class="sxs-lookup"><span data-stu-id="43d79-545">A bitwise set of attributes that apply to the feed.</span></span>|
|<span data-ttu-id="43d79-546">NewestProcessed</span><span class="sxs-lookup"><span data-stu-id="43d79-546">NewestProcessed</span></span>|<span data-ttu-id="43d79-547">**DateTime**</span><span class="sxs-lookup"><span data-stu-id="43d79-547">**DateTime**</span></span>|<span data-ttu-id="43d79-548">Datum und Uhrzeit des neuesten abgerufenen Beitrags.</span><span class="sxs-lookup"><span data-stu-id="43d79-548">The date and time of the newest retrieved post.</span></span>|
|<span data-ttu-id="43d79-549">OldestProcessed</span><span class="sxs-lookup"><span data-stu-id="43d79-549">OldestProcessed</span></span>|<span data-ttu-id="43d79-550">**DateTime**</span><span class="sxs-lookup"><span data-stu-id="43d79-550">**DateTime**</span></span>|<span data-ttu-id="43d79-551">Datum und Uhrzeit des ältesten abgerufenen Beitrags.</span><span class="sxs-lookup"><span data-stu-id="43d79-551">The date and time of the oldest retrieved post.</span></span>|
|<span data-ttu-id="43d79-552">Threads</span><span class="sxs-lookup"><span data-stu-id="43d79-552">Threads</span></span>| <span data-ttu-id="43d79-553">[SP.Social.SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx)[]</span><span class="sxs-lookup"><span data-stu-id="43d79-553">[SP.Social.SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx)[]</span></span>|<span data-ttu-id="43d79-554">Die Threads, aus denen der Feed besteht.</span><span class="sxs-lookup"><span data-stu-id="43d79-554">The threads that make up the feed.</span></span>|
|<span data-ttu-id="43d79-555">UnreadMentionCount</span><span class="sxs-lookup"><span data-stu-id="43d79-555">UnreadMentionCount</span></span>|<span data-ttu-id="43d79-556">**Int32**</span><span class="sxs-lookup"><span data-stu-id="43d79-556">**Int32**</span></span>|<span data-ttu-id="43d79-557">Die Anzahl ungelesener Erwähnungen für den aktuellen Benutzer.</span><span class="sxs-lookup"><span data-stu-id="43d79-557">The count of unread mentions for the current user.</span></span>|
   

  
    
    

  
    
    

### <a name="spsocialsocialrestpostcreationdata"></a><span data-ttu-id="43d79-558">SP.Social.SocialRestPostCreationData</span><span class="sxs-lookup"><span data-stu-id="43d79-558">SP.Social.SocialRestPostCreationData</span></span>
<span data-ttu-id="43d79-559"><a name="bk_SocialRestPostCreationData"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-559"><a name="bk_SocialRestPostCreationData"> </a></span></span>

<span data-ttu-id="43d79-560">Gibt Inhalts- und damit verbundene Informationen für einen neuen Beitrag an.</span><span class="sxs-lookup"><span data-stu-id="43d79-560">Represents content and related information for a new post.</span></span>
  
    
    
<span data-ttu-id="43d79-p143">Clients geben **SocialRestPostCreationData**-Eigenschaften als Parameter in einer Anforderung an, um einen Stammbeitrag oder eine Antwort zu veröffentlichen. Diese Eigenschaften werden im **data**-Attribut des Anforderungstexts angegeben.</span><span class="sxs-lookup"><span data-stu-id="43d79-p143">Clients specify **SocialRestPostCreationData** properties as parameters in a request to publish a root post or a reply. These properties are specified in the **data** attribute of the request body.</span></span>
  
    
    
 <span data-ttu-id="43d79-p144">**SocialRestPostCreationData** enthält eine **ID**-Eigenschaft und ein umschlossenes  [SP.Social.SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx)-Objekt. **ID** ist erforderlich, die **SocialPostCreationData**-Eigenschaften sind jedoch optional.</span><span class="sxs-lookup"><span data-stu-id="43d79-p144">**SocialRestPostCreationData** contains an **ID** property and a wrapped [SP.Social.SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx) object. **ID** is required but the **SocialPostCreationData** properties are optional.</span></span>
  
    
    

|<span data-ttu-id="43d79-565">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="43d79-565">**Property**</span></span>|<span data-ttu-id="43d79-566">**Typ**</span><span class="sxs-lookup"><span data-stu-id="43d79-566">**Type**</span></span>|<span data-ttu-id="43d79-567">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="43d79-567">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="43d79-568">ID (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="43d79-568">ID (required)</span></span>|<span data-ttu-id="43d79-569">**null** oder **String**</span><span class="sxs-lookup"><span data-stu-id="43d79-569">**null** or **String**</span></span>|<span data-ttu-id="43d79-570">Gibt das Ziel des Beitrags an.</span><span class="sxs-lookup"><span data-stu-id="43d79-570">The target destination for the post.</span></span> <span data-ttu-id="43d79-571">Folgende Werte sind möglich:</span><span class="sxs-lookup"><span data-stu-id="43d79-571">The value can be one of the following:</span></span><br/>           <span data-ttu-id="43d79-572">**null** zur Veröffentlichung eines Stammbeitrags im Feed des aktuellen Benutzers</span><span class="sxs-lookup"><span data-stu-id="43d79-572">**null** to publish a root post to the current user's feed</span></span><br/>           <span data-ttu-id="43d79-573">Die ID eines zu beantwortenden Beitrags</span><span class="sxs-lookup"><span data-stu-id="43d79-573">The ID of a post to reply to</span></span><br/>           <span data-ttu-id="43d79-574">Die URL eines Websitefeeds als Veröffentlichungsziel (Beispiel: `http://<teamSiteURL>/newsfeed.aspx`)</span><span class="sxs-lookup"><span data-stu-id="43d79-574">The URL of a site feed to post to (for example: `http://<teamSiteURL>/newsfeed.aspx`)</span></span>|
   
<span data-ttu-id="43d79-575">Das Objekt **SocialPostCreationData** hat folgende Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="43d79-575">The following properties belong to the **SocialPostCreationData** object.</span></span>
  
    
    

|<span data-ttu-id="43d79-576">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="43d79-576">**Property**</span></span>|<span data-ttu-id="43d79-577">**Typ**</span><span class="sxs-lookup"><span data-stu-id="43d79-577">**Type**</span></span>|<span data-ttu-id="43d79-578">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="43d79-578">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="43d79-579">Attachment</span><span class="sxs-lookup"><span data-stu-id="43d79-579">Attachment</span></span>| [<span data-ttu-id="43d79-580">SP.Social.SocialAttachment</span><span class="sxs-lookup"><span data-stu-id="43d79-580">SP.Social.SocialAttachment</span></span>](http://msdn.microsoft.com/library/dfdee790-a1b0-19c8-0e92-5a6e058ba4db%28Office.15%29.aspx)|<span data-ttu-id="43d79-581">Ein Bild, Video oder eine Dokumentanlage für den Beitrag.</span><span class="sxs-lookup"><span data-stu-id="43d79-581">An image, video, or document attachment for the post.</span></span>|
|<span data-ttu-id="43d79-582">ContentItems</span><span class="sxs-lookup"><span data-stu-id="43d79-582">ContentItems</span></span>| <span data-ttu-id="43d79-583">[SP.Social.SocialDataItem](http://msdn.microsoft.com/library/757e7b62-66a6-b03f-0ff0-769a42eb2b4a%28Office.15%29.aspx)[]</span><span class="sxs-lookup"><span data-stu-id="43d79-583">[SP.Social.SocialDataItem](http://msdn.microsoft.com/library/757e7b62-66a6-b03f-0ff0-769a42eb2b4a%28Office.15%29.aspx)[]</span></span>|<span data-ttu-id="43d79-584">Die Elemente, mit denen die entsprechenden Token im Inhaltstext des Beitrags ersetzt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="43d79-584">The items to replace the corresponding tokens in the post's content text</span></span>|
|<span data-ttu-id="43d79-585">ContentText</span><span class="sxs-lookup"><span data-stu-id="43d79-585">ContentText</span></span>|<span data-ttu-id="43d79-586">**String**</span><span class="sxs-lookup"><span data-stu-id="43d79-586">**String**</span></span>|<span data-ttu-id="43d79-587">Der reine Text des Beitrags, der positionale Einfügetoken enthalten kann (z. B. "Heute ist {0}s Geburtstag!").</span><span class="sxs-lookup"><span data-stu-id="43d79-587">The plain text of the post, which can include positional insertion tokens (for example, "Today is {0}'s birthday!").</span></span>|
|<span data-ttu-id="43d79-588">SecurityUris</span><span class="sxs-lookup"><span data-stu-id="43d79-588">SecurityUris</span></span>|<span data-ttu-id="43d79-589">**String[]**</span><span class="sxs-lookup"><span data-stu-id="43d79-589">**String[]**</span></span>|<span data-ttu-id="43d79-590">Zeichenfolgendarstellungen der URIs für SharePoint-Objekte, die Zugriffsberechtigungen für den Beitrag definieren.</span><span class="sxs-lookup"><span data-stu-id="43d79-590">String representations of the URIs to SharePoint objects that define access permissions for the post.</span></span>|
|<span data-ttu-id="43d79-591">Quelle</span><span class="sxs-lookup"><span data-stu-id="43d79-591">Source</span></span>| [<span data-ttu-id="43d79-592">SP.Social.SocialLink</span><span class="sxs-lookup"><span data-stu-id="43d79-592">SP.Social.SocialLink</span></span>](http://msdn.microsoft.com/library/c71efc66-c9ca-ea35-b1c0-cb9ec3bbfcd3%28Office.15%29.aspx)|<span data-ttu-id="43d79-593">Die Quelle des Beitrags.</span><span class="sxs-lookup"><span data-stu-id="43d79-593">The source of the post.</span></span>|
|<span data-ttu-id="43d79-594">UpdateStatusText</span><span class="sxs-lookup"><span data-stu-id="43d79-594">UpdateStatusText</span></span>|<span data-ttu-id="43d79-595">**Boolean**</span><span class="sxs-lookup"><span data-stu-id="43d79-595">**Boolean**</span></span>|<span data-ttu-id="43d79-596">Ein Wert, der steuert, ob der Nur-Text-Inhalt des Beitrags den Statustext des aktuellen Benutzers ersetzen soll.</span><span class="sxs-lookup"><span data-stu-id="43d79-596">A value that controls whether the post's plain-text content should replace the current user's status text.</span></span>|
   

  
    
    

  
    
    

### <a name="spsocialsocialrestthread"></a><span data-ttu-id="43d79-597">SP.Social.SocialRestThread</span><span class="sxs-lookup"><span data-stu-id="43d79-597">SP.Social.SocialRestThread</span></span>
<span data-ttu-id="43d79-598"><a name="bk_SocialRestThread"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-598"><a name="bk_SocialRestThread"> </a></span></span>

<span data-ttu-id="43d79-599">Stellt einen Thread dar, der einen Stammbeitrag sowie eine Reihe von Antworten enthält.</span><span class="sxs-lookup"><span data-stu-id="43d79-599">Represents a thread that contains a root post and a set of replies.</span></span>
  
    
    
<span data-ttu-id="43d79-600">Der Server gibt eine **SocialRestThread**-Ressource in der Antwort auf eine clientseitige Anforderung zurück, um einen Beitrag zu erstellen oder um einen volllständigen Thread abzurufen.</span><span class="sxs-lookup"><span data-stu-id="43d79-600">The server returns a **SocialRestThread** resource in the response to a client-side request to create a post or to get a full thread.</span></span>
  
    
    
 <span data-ttu-id="43d79-601">**SocialRestThread** enthält eine Eigenschaft **ID** sowie ein umschlossenes Objekt des Typs [SP.Social.SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="43d79-601">**SocialRestThread** contains an **ID** property and a wrapped [SP.Social.SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx) object.</span></span>
  
    
    

|<span data-ttu-id="43d79-602">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="43d79-602">**Property**</span></span>|<span data-ttu-id="43d79-603">**Typ**</span><span class="sxs-lookup"><span data-stu-id="43d79-603">**Type**</span></span>|<span data-ttu-id="43d79-604">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="43d79-604">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="43d79-605">ID</span><span class="sxs-lookup"><span data-stu-id="43d79-605">ID</span></span>|<span data-ttu-id="43d79-606">**String**</span><span class="sxs-lookup"><span data-stu-id="43d79-606">**String**</span></span>|<span data-ttu-id="43d79-607">Der eindeutige Bezeichner des Threads.</span><span class="sxs-lookup"><span data-stu-id="43d79-607">The unique identifier of the thread.</span></span>|
   
<span data-ttu-id="43d79-608">Das Objekt **SocialThread** hat die folgenden Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="43d79-608">The following properties belong to the **SocialThread** object.</span></span>
  
    
    

|<span data-ttu-id="43d79-609">**Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="43d79-609">**Property**</span></span>|<span data-ttu-id="43d79-610">**Typ**</span><span class="sxs-lookup"><span data-stu-id="43d79-610">**Type**</span></span>|<span data-ttu-id="43d79-611">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="43d79-611">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="43d79-612">Actors</span><span class="sxs-lookup"><span data-stu-id="43d79-612">Actors</span></span>| <span data-ttu-id="43d79-613">[SP.Social.SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)[]</span><span class="sxs-lookup"><span data-stu-id="43d79-613">[SP.Social.SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)[]</span></span>|<span data-ttu-id="43d79-614">Das zusammengeführte Array teilnehmender Akteure.</span><span class="sxs-lookup"><span data-stu-id="43d79-614">The merged array of participating actors.</span></span>|
|<span data-ttu-id="43d79-615">Attribute</span><span class="sxs-lookup"><span data-stu-id="43d79-615">Attributes</span></span>|<span data-ttu-id="43d79-616">**Int32**</span><span class="sxs-lookup"><span data-stu-id="43d79-616">**Int32**</span></span>|<span data-ttu-id="43d79-p146">Der bitweise Wert, der den Satz von Attributen für den Thread darstellt. Siehe  [SP.Social.SocialThreadAttributes](http://msdn.microsoft.com/library/21ff9f92-3223-bcc7-ceec-7b899ee29b6e%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="43d79-p146">The bitwise value that represents the set of attributes for the thread. See  [SP.Social.SocialThreadAttributes](http://msdn.microsoft.com/library/21ff9f92-3223-bcc7-ceec-7b899ee29b6e%28Office.15%29.aspx).</span></span>|
|<span data-ttu-id="43d79-619">Id</span><span class="sxs-lookup"><span data-stu-id="43d79-619">Id</span></span>|<span data-ttu-id="43d79-620">**String**</span><span class="sxs-lookup"><span data-stu-id="43d79-620">**String**</span></span>|<span data-ttu-id="43d79-621">Der eindeutige Bezeichner des Threads.</span><span class="sxs-lookup"><span data-stu-id="43d79-621">The unique identifier of the thread.</span></span>|
|<span data-ttu-id="43d79-622">OwnerIndex</span><span class="sxs-lookup"><span data-stu-id="43d79-622">OwnerIndex</span></span>|<span data-ttu-id="43d79-623">**Int32**</span><span class="sxs-lookup"><span data-stu-id="43d79-623">**Int32**</span></span>|<span data-ttu-id="43d79-624">Der Index des Threadbesitzers innerhalb der Threadakteure.</span><span class="sxs-lookup"><span data-stu-id="43d79-624">The index of the thread's owner within the thread's actors.</span></span>|
|<span data-ttu-id="43d79-625">Permalink</span><span class="sxs-lookup"><span data-stu-id="43d79-625">Permalink</span></span>|<span data-ttu-id="43d79-626">**String**</span><span class="sxs-lookup"><span data-stu-id="43d79-626">**String**</span></span>|<span data-ttu-id="43d79-627">Die Zeichenfolgendarstellung des stabilen URIs für die Navigation zum Thread, sofern einer verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="43d79-627">The string representation of the stable URI for navigating directly to the thread, if one is available.</span></span>|
|<span data-ttu-id="43d79-628">PostReference</span><span class="sxs-lookup"><span data-stu-id="43d79-628">PostReference</span></span>| [<span data-ttu-id="43d79-629">SP.Social.SocialPostReference</span><span class="sxs-lookup"><span data-stu-id="43d79-629">SP.Social.SocialPostReference</span></span>](http://msdn.microsoft.com/library/529e1db7-2e9a-5141-6b1e-94a5c63e7c16%28Office.15%29.aspx)|<span data-ttu-id="43d79-630">Der Beitrag, auf den verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="43d79-630">The referenced post.</span></span>|
|<span data-ttu-id="43d79-631">Antworten</span><span class="sxs-lookup"><span data-stu-id="43d79-631">Replies</span></span>| <span data-ttu-id="43d79-632">[SP.Social.SocialPost](http://msdn.microsoft.com/library/a761ce71-d3d7-420a-1e06-962674124dfa%28Office.15%29.aspx)[]</span><span class="sxs-lookup"><span data-stu-id="43d79-632">[SP.Social.SocialPost](http://msdn.microsoft.com/library/a761ce71-d3d7-420a-1e06-962674124dfa%28Office.15%29.aspx)[]</span></span>|<span data-ttu-id="43d79-633">Die Antworten auf den Thread.</span><span class="sxs-lookup"><span data-stu-id="43d79-633">The replies to the thread.</span></span>|
|<span data-ttu-id="43d79-634">RootPost</span><span class="sxs-lookup"><span data-stu-id="43d79-634">RootPost</span></span>| [<span data-ttu-id="43d79-635">SP.Social.SocialPost</span><span class="sxs-lookup"><span data-stu-id="43d79-635">SP.Social.SocialPost</span></span>](http://msdn.microsoft.com/library/a761ce71-d3d7-420a-1e06-962674124dfa%28Office.15%29.aspx)|<span data-ttu-id="43d79-636">Der Stammbeitrag des Threads.</span><span class="sxs-lookup"><span data-stu-id="43d79-636">The root post of the thread.</span></span>|
|<span data-ttu-id="43d79-637">Status</span><span class="sxs-lookup"><span data-stu-id="43d79-637">Status</span></span>|<span data-ttu-id="43d79-638">**Int32**</span><span class="sxs-lookup"><span data-stu-id="43d79-638">**Int32**</span></span>|<span data-ttu-id="43d79-p147">Der Code, der behebbare Fehler identifiziert, die beim Abrufen des Threads aufgetreten sind. Siehe  [SP.Social.SocialStatusCode](http://msdn.microsoft.com/library/79292329-19de-43e1-5928-60b0edc36c94%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="43d79-p147">The code that identifies recoverable errors that occurred during thread retrieval. See  [SP.Social.SocialStatusCode](http://msdn.microsoft.com/library/79292329-19de-43e1-5928-60b0edc36c94%28Office.15%29.aspx).</span></span>|
|<span data-ttu-id="43d79-641">ThreadType</span><span class="sxs-lookup"><span data-stu-id="43d79-641">ThreadType</span></span>| [<span data-ttu-id="43d79-642">SP.Social.SocialThreadType</span><span class="sxs-lookup"><span data-stu-id="43d79-642">SP.Social.SocialThreadType</span></span>](http://msdn.microsoft.com/library/7444217e-ddda-d3a0-b19f-146cf8c6fcaa%28Office.15%29.aspx)|<span data-ttu-id="43d79-643">Der Threadtyp.</span><span class="sxs-lookup"><span data-stu-id="43d79-643">The thread type.</span></span>|
|<span data-ttu-id="43d79-644">TotalReplyCount</span><span class="sxs-lookup"><span data-stu-id="43d79-644">TotalReplyCount</span></span>|<span data-ttu-id="43d79-645">**Int32**</span><span class="sxs-lookup"><span data-stu-id="43d79-645">**Int32**</span></span>|<span data-ttu-id="43d79-646">Die Gesamtanzahl von Antworten für den Thread.</span><span class="sxs-lookup"><span data-stu-id="43d79-646">The count of the total number of replies for the thread.</span></span>|
   

## <a name="see-also"></a><span data-ttu-id="43d79-647">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="43d79-647">See also</span></span>
<span data-ttu-id="43d79-648"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="43d79-648"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="43d79-649">Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint</span><span class="sxs-lookup"><span data-stu-id="43d79-649">Get started developing with social features in SharePoint</span></span>](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [<span data-ttu-id="43d79-650">Vorgehensweise: Lesen und Schreiben der sozialen Feed mithilfe des REST-Diensts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="43d79-650">How to: Learn to read and write to the social feed by using the REST service in SharePoint</span></span>](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)
    
  
-  [<span data-ttu-id="43d79-651">Arbeiten mit sozialen Feeds in SharePoint</span><span class="sxs-lookup"><span data-stu-id="43d79-651">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  
-  [<span data-ttu-id="43d79-652">REST-API-Referenz zum Folgen von Personen und Inhalten für SharePoint</span><span class="sxs-lookup"><span data-stu-id="43d79-652">Following people and content REST API reference for SharePoint</span></span>](following-people-and-content-rest-api-reference-for-sharepoint.md)
    
  
- <span data-ttu-id="43d79-653">Um die Mitglieder im **SP.Social**-OData-Schema anzuzeigen, die vom SharePoint-REST-Dienst verwendet werden, navigieren Sie zu  `http://<siteUri>/_api/$metadata`.</span><span class="sxs-lookup"><span data-stu-id="43d79-653">To see the members in the **SP.Social** OData schema used by the SharePoint REST service, browse to `http://<siteUri>/_api/$metadata`.</span></span>
    
  
