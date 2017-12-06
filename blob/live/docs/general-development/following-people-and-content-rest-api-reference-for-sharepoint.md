---
title: "REST-API-Referenz zum Folgen von Personen und Inhalten für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c05755df-846d-4a39-941d-950d066cc6d4
ms.openlocfilehash: d18faadfbb6ea259fb073609e892d2fa4dcd344d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="following-people-and-content-rest-api-reference-for-sharepoint"></a><span data-ttu-id="b4bab-102">REST-API-Referenz zum Folgen von Personen und Inhalten für SharePoint</span><span class="sxs-lookup"><span data-stu-id="b4bab-102">Following people and content REST API reference for SharePoint</span></span>
<span data-ttu-id="b4bab-p101">Suchen Sie nach SharePoint-REST-Endpunkten, um über die Ressourcen **SocialRestFollowingManager** und **PeopleManager** Personen und Inhalten zu folgen. Sie können den SharePoint-REST-Dienst (Representational State Transfer) verwenden, um dieselben Aufgaben durchzuführen wie bei Verwendung der .NET-Clientobjektmodelle und des JavaScript-Objektmodells. Für die Verwendung des REST-Diensts erstellen und senden Sie HTTP **GET**- und **POST**-Anforderungen an die Ressourcenendpunkte, die die gewünschten Aufgaben darstellen. Diese Ressourcenendpunkte entsprechen SharePoint-Objekten, -Eigenschaften und -Methoden.</span><span class="sxs-lookup"><span data-stu-id="b4bab-p101">Find SharePoint REST endpoints for following people and content by using the **SocialRestFollowingManager** resource and the **PeopleManager** resource. You can use the SharePoint Representational State Transfer (REST) service to do the same tasks you can do when you use the .NET client object models and the JavaScript object model. To use the REST service, you build and send HTTP **GET** and **POST** requests to the resource endpoints that represent the tasks you want to do. These resource endpoints correspond to SharePoint objects, properties, and methods.</span></span>
  
    
    

<span data-ttu-id="b4bab-p102">Der Endpunkt-URI für die meisten Aufgaben zum Folgen beginnt mit der Ressource **SocialRestFollowingManager** ( `social.following`) und endet mit der Ressource, die die bestimmte Aufgabe ausführt. Sie verwenden beispielsweise den URI  `http://www.contoso.com/_api/social.following/follow`, damit der aktuelle Benutzer beginnt, Personen oder Inhalten zu folgen, und den URI  `https://www.contoso.com/sites/devSite/_api/social.following/followed`, um die Personen oder Inhalte abzurufen, denen der aktuelle Benutzer folgt.</span><span class="sxs-lookup"><span data-stu-id="b4bab-p102">The endpoint URI for most Following tasks begins with the **SocialRestFollowingManager** resource ( `social.following`) and ends with the resource that performs the specific task. For example, you use the URI  `http://www.contoso.com/_api/social.following/follow` to make the current user start following people or content, and the URI `https://www.contoso.com/sites/devSite/_api/social.following/followed` to get the people or content the current user is following.</span></span>
> <span data-ttu-id="b4bab-109">**Hinweis:** In diesem Artikel werden der Endpunkt-URI und die Parameterkomponenten der HTTP-Anforderungen gezeigt.</span><span class="sxs-lookup"><span data-stu-id="b4bab-109">**Note:** This article shows the endpoint URI and parameter components of HTTP requests.</span></span> <span data-ttu-id="b4bab-110">Beispiele zu vollständigen Anfragen finden Sie unter [Vorgehensweise: Nachverfolgen von Dokumenten, Websites und Tags mit dem REST-Dienst von SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md).</span><span class="sxs-lookup"><span data-stu-id="b4bab-110">Note This article shows the endpoint URI and parameter components of HTTP requests. For examples of complete requests, see  [How to: Follow documents, sites, and tags by using the REST service in SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md).</span></span> 
  
    
    

<span data-ttu-id="b4bab-p104">Wir empfehlen die Verwendung der **SocialRestFollowingManager**-API für Aufgaben zum Folgen von Personen und Inhalten, aber Sie können auch die Ressource **PeopleManager** für einige Aufgaben rund um das Folgen von Personen verwenden, die **SocialRestFollowingManager** nicht unterstützt. Sie können z. B. herausfinden, ob jemand dem aktuellen Benutzer folgt oder die Follower eines anderen Benutzers abrufen. Für diese Aufgaben senden Sie HTTP **GET**-Anforderungen an Endpunkt-URIs, die mit der Ressource **PeopleManager** ( `sp.userprofiles.peoplemanager`) beginnen und mit der Ressource enden, die die bestimmte Aufgabe ausführt.Wenn der Endpunkt einen Parameter annimmt, werden die Parametermetadaten im URI oder im Anforderungstext im XML- oder JavaScript Object Notation (JSON)-Format gesendet. Sie können HTTP-Anforderungen in jeder Sprache, einschließlich JavaScript und C# durchführen. Standardmäßig gibt der REST-Dienst Antworten zurück, die mithilfe des Atom-Protokolls formatiert sind, aber Sie können das JSON-Format mithilfe von HTTP **Accept**-Headern anfordern. Weitere Informationen finden Sie unter  [Programmieren mit dem SharePoint REST-Dienst](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4bab-p104">We recommend that you use the **SocialRestFollowingManager** API for Following People and Following Content tasks, but you can use the **PeopleManager** resource for some Following People tasks that **SocialRestFollowingManager** doesn't support. For example, you can find out whether someone is following the current user or get another user's followers. For these tasks, you send HTTP **GET** requests to endpoint URIs that begin with the **PeopleManager** resource ( `sp.userprofiles.peoplemanager`) and end with the resource that performs the specific task.If the endpoint takes a parameter, the parameter metadata is sent in the URI or in the request body in XML or JavaScript Object Notation (JSON) format. You can make HTTP requests in any language, including JavaScript and C#. By default, the REST service returns responses that are formatted by using the Atom protocol, but you can request the JSON format by using HTTP **Accept** headers. See [Use OData query operations in SharePoint REST requests](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span></span>
## <a name="resource-endpoints-for-following-people-and-following-content-tasks"></a><span data-ttu-id="b4bab-117">Ressourcenendpunkte für das Folgen von Personen und Inhalten folgen</span><span class="sxs-lookup"><span data-stu-id="b4bab-117">Resource endpoints for Following People and Following Content tasks</span></span>
<span data-ttu-id="b4bab-118"><a name="bk_Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-118"></span></span>


[<span data-ttu-id="b4bab-119">Follow</span><span class="sxs-lookup"><span data-stu-id="b4bab-119">Follow</span></span>](#bk_Follow)  
[<span data-ttu-id="b4bab-120">StopFollowing</span><span class="sxs-lookup"><span data-stu-id="b4bab-120">StopFollowing</span></span>](#bk_StopFollowing)  
<span data-ttu-id="b4bab-121">[IsFollowed](#bk_IsFollowed)</span><span class="sxs-lookup"><span data-stu-id="b4bab-121">SSOM:  [IsFollowed](#bk_IsFollowed)</span></span>  
[<span data-ttu-id="b4bab-122">My</span><span class="sxs-lookup"><span data-stu-id="b4bab-122">My</span></span>](#bk_My)  
[<span data-ttu-id="b4bab-123">My/FollowedDocumentsUri</span><span class="sxs-lookup"><span data-stu-id="b4bab-123">My/FollowedDocumentsUri</span></span>](#bk_MyFollowedDocumentsUri)  
[<span data-ttu-id="b4bab-124">My/FollowedSitesUri</span><span class="sxs-lookup"><span data-stu-id="b4bab-124">My/FollowedSitesUri</span></span>](#bk_MyFollowedSitesUri)  
[<span data-ttu-id="b4bab-125">My/Followed</span><span class="sxs-lookup"><span data-stu-id="b4bab-125">My/Followed</span></span>](#bk_Followed)  
[<span data-ttu-id="b4bab-126">My/FollowedCount</span><span class="sxs-lookup"><span data-stu-id="b4bab-126">My/FollowedCount</span></span>](#bk_FollowedCount)  
[<span data-ttu-id="b4bab-127">My/Followers</span><span class="sxs-lookup"><span data-stu-id="b4bab-127">My/Followers</span></span>](#bk_Followers)  
[<span data-ttu-id="b4bab-128">My/Suggestions</span><span class="sxs-lookup"><span data-stu-id="b4bab-128">My/Suggestions</span></span>](#bk_Suggestions)  
[<span data-ttu-id="b4bab-129">GetMySuggestions</span><span class="sxs-lookup"><span data-stu-id="b4bab-129">/getmysuggestions</span></span>](#bk_GetMySuggestions)  
<span data-ttu-id="b4bab-130">[IsMyPeopleListPublic](#bk_IsMyPeopleListPublic)</span><span class="sxs-lookup"><span data-stu-id="b4bab-130">SSOM:  [IsMyPeopleListPublic](#bk_IsMyPeopleListPublic)</span></span>  
<span data-ttu-id="b4bab-131">[AmIFollowedBy](#bk_AmIFollowedBy)</span><span class="sxs-lookup"><span data-stu-id="b4bab-131">SSOM:  [AmIFollowedBy](#bk_AmIFollowedBy)</span></span>  
<span data-ttu-id="b4bab-132">[GetPeopleFollowedBy](#bk_GetPeopleFollowedBy)</span><span class="sxs-lookup"><span data-stu-id="b4bab-132">SSOM:  [GetPeopleFollowedBy](#bk_GetPeopleFollowedBy)</span></span>  
<span data-ttu-id="b4bab-133">[GetFollowersFor](#bk_GetFollowersFor)</span><span class="sxs-lookup"><span data-stu-id="b4bab-133">SSOM:  [GetFollowersFor](#bk_GetFollowersFor)</span></span>  
   

## <a name="follow"></a><span data-ttu-id="b4bab-134">Folgen</span><span class="sxs-lookup"><span data-stu-id="b4bab-134">Follow</span></span>
<span data-ttu-id="b4bab-135"><a name="bk_Follow"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-135"></span></span>

<span data-ttu-id="b4bab-136">Sorgt dafür, dass der aktuelle Benutzer beginnt, einem Benutzer, einem Dokument, einer Website oder einem Tag zu folgen.</span><span class="sxs-lookup"><span data-stu-id="b4bab-136">Makes the current user start following a user, document, site, or tag.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="b4bab-137">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="b4bab-137">Endpoint URI structure</span></span>

 <span data-ttu-id="b4bab-138">**POST** `http://<siteCollection>/<site>/_api/social.following/follow`</span><span class="sxs-lookup"><span data-stu-id="b4bab-138">**POST** `http://<siteCollection>/<site>/_api/social.following/follow`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="b4bab-139">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="b4bab-139">Request parameter</span></span>

 <span data-ttu-id="b4bab-140">_actor_</span><span class="sxs-lookup"><span data-stu-id="b4bab-140">_actor_</span></span>
  
    
    
<span data-ttu-id="b4bab-141">Typ: **SP.Social.SocialActorInfo**</span><span class="sxs-lookup"><span data-stu-id="b4bab-141">Type: **SP.Social.SocialActorInfo**</span></span>
  
    
    
<span data-ttu-id="b4bab-142">Der Akteur, dem gefolgt werden soll.</span><span class="sxs-lookup"><span data-stu-id="b4bab-142">The actor to start following.</span></span>
  
    
    
 <span data-ttu-id="b4bab-143">**Benutzer  _actor_ im URI**</span><span class="sxs-lookup"><span data-stu-id="b4bab-143">**User  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=0,AccountName=@v,Id=null)?@v='domain\\user'
```

 <span data-ttu-id="b4bab-144">**Benutzer _actor_ im Anforderungstext**</span><span class="sxs-lookup"><span data-stu-id="b4bab-144">**User  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":0,
  "AccountName":"domain\\user",
  "Id":null
}
```

<span data-ttu-id="b4bab-145">Wenn Sie ein anspruchsbasiertes Identitätsmodell verwenden, können Sie den Kontonamen mithilfe des Formats  `@v='i:0"%23".f|membership|user@domain.com'` in der Abfragezeichenfolge oder des Formats `"i:0#.f|membership|user@domain.com"` im Anforderungstext übergeben.</span><span class="sxs-lookup"><span data-stu-id="b4bab-145">If you're using a claims-based identity model, you can pass the account name by using the format  `@v='i:0"%23".f|membership|user@domain.com'` in the query string or `"i:0#.f|membership|user@domain.com"` in the request body.</span></span>
  
    
    
 <span data-ttu-id="b4bab-146">**Dokument _actor_ im URI**</span><span class="sxs-lookup"><span data-stu-id="b4bab-146">**Document  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=1,ContentUri=@v,Id=null)?@v='http://server/Shared%20Documents/fileName.docx'
```

 <span data-ttu-id="b4bab-147">**Dokument _actor_ im Anforderungstext**</span><span class="sxs-lookup"><span data-stu-id="b4bab-147">**Document  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":1,
  "ContentUri":"http://server/Shared%20Documents/fileName.docx",
  "Id":null
}
```

 <span data-ttu-id="b4bab-148">**Website _actor_ im URI**</span><span class="sxs-lookup"><span data-stu-id="b4bab-148">**Site  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=2,ContentUri=@v,Id=null)?@v='http://server/site'
```

 <span data-ttu-id="b4bab-149">**Website  _actor_ im Anforderungstext**</span><span class="sxs-lookup"><span data-stu-id="b4bab-149">**Site  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":2,
  "ContentUri":"http://siteCollection/site",
  "Id":null
}
```

 <span data-ttu-id="b4bab-150">**Tag _actor_ im URI**</span><span class="sxs-lookup"><span data-stu-id="b4bab-150">**Tag  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=3,TagGuid='19a4a484-c1dc-4bc5-8c93-bb96245ce928',Id=null)
```

 <span data-ttu-id="b4bab-151">**Tag _actor_ im Anforderungstext**</span><span class="sxs-lookup"><span data-stu-id="b4bab-151">**Tag  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":3,
  "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928",
  "Id":null
}
```

<span data-ttu-id="b4bab-p105">Sie benötigen die Tag-GUID, um zu beginnen, einem Tag zu folgen. Die GUID kann nicht mithilfe des REST-Diensts abgerufen werden, jedoch können Sie das .NET-Clientobjektmodell oder das JavaScript-Objektmodell verwenden. Weitere Informationen finden Sie unter  [So rufen die GUID eines Tags basierend auf dem Namen des Tags mithilfe des JavaScript-Objektmodells ab](follow-content-in-sharepoint.md#bk_getTagGuid).</span><span class="sxs-lookup"><span data-stu-id="b4bab-p105">You need the tag GUID to start following a tag. You can't get the GUID by using the REST service, but you can use the .NET client object model or the JavaScript object model. See  [How to get a tag's GUID based on the tag's name by using the JavaScript object model](follow-content-in-sharepoint.md#bk_getTagGuid).</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="b4bab-155">Antwort</span><span class="sxs-lookup"><span data-stu-id="b4bab-155">Response</span></span>

 <span data-ttu-id="b4bab-156">**Follow**</span><span class="sxs-lookup"><span data-stu-id="b4bab-156">**Follow**</span></span>
  
    
    
<span data-ttu-id="b4bab-157">Typ: **SP.Social.SocialFollowResult**</span><span class="sxs-lookup"><span data-stu-id="b4bab-157">Type: **SP.Social.SocialFollowResult**</span></span>
  
    
    
<span data-ttu-id="b4bab-158">Der Status der Anforderung: 0 = OK; 1 = AlreadyFollowing; 2 = LimitReached oder 3 = InternalError.</span><span class="sxs-lookup"><span data-stu-id="b4bab-158">The status of the request: 0 = OK; 1 = AlreadyFollowing; 2 = LimitReached; or 3 = InternalError.</span></span>
  
    
    
<span data-ttu-id="b4bab-159">Die folgende Antwort weist darauf hin, dass die Anforderung erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="b4bab-159">The following response indicates that the request succeeded.</span></span>
  
    
    



```

{"d":{"Follow":0}}
```


## <a name="stopfollowing"></a><span data-ttu-id="b4bab-160">StopFollowing</span><span class="sxs-lookup"><span data-stu-id="b4bab-160">StopFollowing method</span></span>
<span data-ttu-id="b4bab-161"><a name="bk_StopFollowing"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-161"></span></span>

<span data-ttu-id="b4bab-162">Sorgt dafür, dass der aktuelle Benutzer aufhört, einem Benutzer, einem Dokument, einer Website oder einem Tag zu folgen.</span><span class="sxs-lookup"><span data-stu-id="b4bab-162">Makes the current user stop following a user, document, site, or tag.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="b4bab-163">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="b4bab-163">Endpoint URI structure</span></span>

 <span data-ttu-id="b4bab-164">**POST** `http://<siteCollection>/<site>/_api/social.following/stopfollowing`</span><span class="sxs-lookup"><span data-stu-id="b4bab-164">**POST** `http://<siteCollection>/<site>/_api/social.following/stopfollowing`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="b4bab-165">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="b4bab-165">Request parameter</span></span>

 <span data-ttu-id="b4bab-166">_actor_</span><span class="sxs-lookup"><span data-stu-id="b4bab-166">_actor_</span></span>
  
    
    
<span data-ttu-id="b4bab-167">Typ: **SP.Social.SocialActorInfo**</span><span class="sxs-lookup"><span data-stu-id="b4bab-167">Type: **SP.Social.SocialActorInfo**</span></span>
  
    
    
<span data-ttu-id="b4bab-168">Der Akteur, dem nicht mehr gefolgt werden soll.</span><span class="sxs-lookup"><span data-stu-id="b4bab-168">The actor to stop following.</span></span>
  
    
    
 <span data-ttu-id="b4bab-169">**Benutzer _actor_ im URI**</span><span class="sxs-lookup"><span data-stu-id="b4bab-169">**User  _actor_ in the URI**</span></span>
  
    
    



```
http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=0,AccountName=@v,Id=null)?@v='domain\\user'
```

 <span data-ttu-id="b4bab-170">**Benutzer _actor_ im Anforderungstext**</span><span class="sxs-lookup"><span data-stu-id="b4bab-170">**User  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":0,
  "AccountName":"domain\\user",
  "Id":null
}
```

<span data-ttu-id="b4bab-171">Wenn Sie ein anspruchsbasiertes Identitätsmodell verwenden, können Sie den Kontonamen mithilfe des Formats  `@v='i:0"%23".f|membership|user@domain.com'` in der Abfragezeichenfolge oder des Formats `"i:0#.f|membership|user@domain.com"` im Anforderungstext übergeben.</span><span class="sxs-lookup"><span data-stu-id="b4bab-171">If you're using a claims-based identity model, you can pass the account name by using the format  `@v='i:0"%23".f|membership|user@domain.com'` in the query string or `"i:0#.f|membership|user@domain.com"` in the request body.</span></span>
  
    
    
 <span data-ttu-id="b4bab-172">**Dokument _actor_ im URI**</span><span class="sxs-lookup"><span data-stu-id="b4bab-172">**Document  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=1,ContentUri=@v,Id=null)?@v='http://server/Shared%20Documents/fileName.docx'
```

 <span data-ttu-id="b4bab-173">**Dokument _actor_ im Anforderungstext**</span><span class="sxs-lookup"><span data-stu-id="b4bab-173">**Document  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":1,
  "ContentUri":"http://server/Shared%20Documents/fileName.docx",
  "Id":null
}
```

 <span data-ttu-id="b4bab-174">**Website _actor_ im URI**</span><span class="sxs-lookup"><span data-stu-id="b4bab-174">**Site  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=2,ContentUri=@v,Id=null)?@v='http://server/site'
```

 <span data-ttu-id="b4bab-175">**Website  _actor_ im Anforderungstext**</span><span class="sxs-lookup"><span data-stu-id="b4bab-175">**Site  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":2,
  "ContentUri":"http://siteCollection/site",
  "Id":null
}
```

 <span data-ttu-id="b4bab-176">**Tag _actor_ im URI**</span><span class="sxs-lookup"><span data-stu-id="b4bab-176">**Tag  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=3,TagGuid='19a4a484-c1dc-4bc5-8c93-bb96245ce928',Id=null)
```

 <span data-ttu-id="b4bab-177">**Tag _actor_ im Anforderungstext**</span><span class="sxs-lookup"><span data-stu-id="b4bab-177">**Tag  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":3,
  "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928",
  "Id":null
}
```

<span data-ttu-id="b4bab-p106">Sie benötigen die Tag-GUID, um zu beginnen, einem Tag zu folgen. Die GUID kann nicht mithilfe des REST-Diensts abgerufen werden, jedoch können Sie das .NET-Clientobjektmodell oder das JavaScript-Objektmodell verwenden. Weitere Informationen finden Sie unter  [So rufen die GUID eines Tags basierend auf dem Namen des Tags mithilfe des JavaScript-Objektmodells ab](follow-content-in-sharepoint.md#bk_getTagGuid).</span><span class="sxs-lookup"><span data-stu-id="b4bab-p106">You need the tag GUID to start following a tag. You can't get the GUID by using the REST service, but you can use the .NET client object model or the JavaScript object model. See  [How to get a tag's GUID based on the tag's name by using the JavaScript object model](follow-content-in-sharepoint.md#bk_getTagGuid).</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="b4bab-181">Antwort</span><span class="sxs-lookup"><span data-stu-id="b4bab-181">Response</span></span>

<span data-ttu-id="b4bab-182">Keine</span><span class="sxs-lookup"><span data-stu-id="b4bab-182">None.</span></span>
  
    
    

```

{"d":{"StopFollowing":null}}
```


## <a name="isfollowed"></a><span data-ttu-id="b4bab-183">IsFollowed</span><span class="sxs-lookup"><span data-stu-id="b4bab-183">SSOM:  IsFollowed</span></span>
<span data-ttu-id="b4bab-184"><a name="bk_IsFollowed"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-184"></span></span>

<span data-ttu-id="b4bab-185">Gibt an, ob der aktuelle Benutzer einem angegebenen Benutzer, einem Dokument, einer Website oder einem Tag folgt.</span><span class="sxs-lookup"><span data-stu-id="b4bab-185">Indicates whether the current user is following a specified user, document, site, or tag.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="b4bab-186">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="b4bab-186">Endpoint URI structure</span></span>

 <span data-ttu-id="b4bab-187">**POST** `http://<siteCollection>/<site>/_api/social.following/isfollowed`</span><span class="sxs-lookup"><span data-stu-id="b4bab-187">**POST** `http://<siteCollection>/<site>/_api/social.following/isfollowed`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="b4bab-188">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="b4bab-188">Request parameter</span></span>

 <span data-ttu-id="b4bab-189">_actor_</span><span class="sxs-lookup"><span data-stu-id="b4bab-189">_actor_</span></span>
  
    
    
<span data-ttu-id="b4bab-190">Typ: **SP.Social.SocialActorInfo**</span><span class="sxs-lookup"><span data-stu-id="b4bab-190">Type: **SP.Social.SocialActorInfo**</span></span>
  
    
    
<span data-ttu-id="b4bab-191">Der Akteur, für den der folgende Status gefunden werden soll.</span><span class="sxs-lookup"><span data-stu-id="b4bab-191">The actor to find the following status for.</span></span>
  
    
    
 <span data-ttu-id="b4bab-192">**Benutzer _actor_ im URI**</span><span class="sxs-lookup"><span data-stu-id="b4bab-192">**User  _actor_ in the URI**</span></span>
  
    
    



```
http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=0,AccountName=@v,Id=null)?@v='domain\\user'
```

 <span data-ttu-id="b4bab-193">**Benutzer _actor_ im Anforderungstext**</span><span class="sxs-lookup"><span data-stu-id="b4bab-193">**User  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":0,
  "AccountName":"domain\\user",
  "Id":null
}
```

<span data-ttu-id="b4bab-194">Wenn Sie ein anspruchsbasiertes Identitätsmodell verwenden, können Sie den Kontonamen mithilfe des Formats  `@v='i:0"%23".f|membership|user@domain.com'` in der Abfragezeichenfolge oder des Formats `"i:0#.f|membership|user@domain.com"` im Anforderungstext übergeben.</span><span class="sxs-lookup"><span data-stu-id="b4bab-194">If you're using a claims-based identity model, you can pass the account name by using the format  `@v='i:0"%23".f|membership|user@domain.com'` in the query string or `"i:0#.f|membership|user@domain.com"` in the request body.</span></span>
  
    
    
 <span data-ttu-id="b4bab-195">**Dokument _actor_ im URI**</span><span class="sxs-lookup"><span data-stu-id="b4bab-195">**Document  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=1,ContentUri=@v,Id=null)?@v='https://domain.sharepoint.com/Shared%20Documents/fileName.docx'
```

 <span data-ttu-id="b4bab-196">**Dokument _actor_ im Anforderungstext**</span><span class="sxs-lookup"><span data-stu-id="b4bab-196">**Document  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":1,
  "ContentUri":"http://server/Shared%20Documents/fileName.docx",
  "Id":null
}
```

 <span data-ttu-id="b4bab-197">**Website _actor_ im URI**</span><span class="sxs-lookup"><span data-stu-id="b4bab-197">**Site  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=2,ContentUri=@v,Id=null)?@v='http://domain.sharepoint.com'
```

 <span data-ttu-id="b4bab-198">**Website  _actor_ im Anforderungstext**</span><span class="sxs-lookup"><span data-stu-id="b4bab-198">**Site  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":2,
  "ContentUri":"http://siteCollection/site",
  "Id":null
}
```

 <span data-ttu-id="b4bab-199">**Tag _actor_ im URI**</span><span class="sxs-lookup"><span data-stu-id="b4bab-199">**Tag  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=3,TagGuid='19a4a484-c1dc-4bc5-8c93-bb96245ce928',Id=null)
```

 <span data-ttu-id="b4bab-200">**Tag _actor_ im Anforderungstext**</span><span class="sxs-lookup"><span data-stu-id="b4bab-200">**Tag  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":3,
  "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928",
  "Id":null
}
```

<span data-ttu-id="b4bab-p107">Sie benötigen die Tag-GUID, um zu beginnen, einem Tag zu folgen. Die GUID kann nicht mithilfe des REST-Diensts abgerufen werden, jedoch können Sie das .NET-Clientobjektmodell oder das JavaScript-Objektmodell verwenden. Weitere Informationen finden Sie unter  [So rufen die GUID eines Tags basierend auf dem Namen des Tags mithilfe des JavaScript-Objektmodells ab](follow-content-in-sharepoint.md#bk_getTagGuid).</span><span class="sxs-lookup"><span data-stu-id="b4bab-p107">You need the tag GUID to start following a tag. You can't get the GUID by using the REST service, but you can use the .NET client object model or the JavaScript object model. See  [How to get a tag's GUID based on the tag's name by using the JavaScript object model](follow-content-in-sharepoint.md#bk_getTagGuid).</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="b4bab-204">Antwort</span><span class="sxs-lookup"><span data-stu-id="b4bab-204">Response</span></span>

 <span data-ttu-id="b4bab-205">**IsFollowed**</span><span class="sxs-lookup"><span data-stu-id="b4bab-205">SSOM:  **IsFollowed**</span></span>
  
    
    
<span data-ttu-id="b4bab-206">Typ: **bool**</span><span class="sxs-lookup"><span data-stu-id="b4bab-206">Type: **bool**</span></span>
  
    
    
 <span data-ttu-id="b4bab-207">**true**, wenn der Benutzer dem Akteur folgt, andernfalls **false**.</span><span class="sxs-lookup"><span data-stu-id="b4bab-207">**true** if the current user is following the actor; otherwise **false**.</span></span>
  
    
    
<span data-ttu-id="b4bab-208">Die folgende Antwort weist darauf hin, dass der Benutzer dem angegebenen Akteur nicht folgt.</span><span class="sxs-lookup"><span data-stu-id="b4bab-208">The following response indicates that the user is not following the specified actor.</span></span>
  
    
    



```

{"d":{"IsFollowed":false}}
```


## <a name="my"></a><span data-ttu-id="b4bab-209">My</span><span class="sxs-lookup"><span data-stu-id="b4bab-209">My</span></span>
<span data-ttu-id="b4bab-210"><a name="bk_My"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-210"></span></span>

<span data-ttu-id="b4bab-211">Ruft Informationen über die **SocialRestFollowingManager**-Instanz sowie Informationen über den aktuellen Benutzer ab.</span><span class="sxs-lookup"><span data-stu-id="b4bab-211">Gets information about the **SocialRestFollowingManager** instance and information about the current user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="b4bab-212">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="b4bab-212">Endpoint URI structure</span></span>

 <span data-ttu-id="b4bab-213">**GET** `http://<siteCollection>/<site>/_api/social.following/my`</span><span class="sxs-lookup"><span data-stu-id="b4bab-213">**GET** `http://<siteCollection>/<site>/_api/social.following/my`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="b4bab-214">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="b4bab-214">Request parameter</span></span>

<span data-ttu-id="b4bab-215">Keine</span><span class="sxs-lookup"><span data-stu-id="b4bab-215">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="b4bab-216">Antwort</span><span class="sxs-lookup"><span data-stu-id="b4bab-216">Response</span></span>

<span data-ttu-id="b4bab-217">Typ: **SP.Social.SocialRestFollowingManager**</span><span class="sxs-lookup"><span data-stu-id="b4bab-217">Type: **SP.Social.SocialRestFollowingManager**</span></span>
  
    
    
<span data-ttu-id="b4bab-218">Information über die **SocialRestFollowingManager**-Instanz und die Eigenschaften **MyFollowedDocumentsUri**, **MyFollowedSitesUri** und **SocialActor** für den aktuellen Benutzer.</span><span class="sxs-lookup"><span data-stu-id="b4bab-218">Information about the **SocialRestFollowingManager** instance, and the **MyFollowedDocumentsUri**, **MyFollowedSitesUri**, and **SocialActor** properties for the current user.</span></span>
  
    
    
<span data-ttu-id="b4bab-219">Die folgende Antwort stellt die **SocialRestFollowingManager**-Instanz für den aktuellen Benutzer dar.</span><span class="sxs-lookup"><span data-stu-id="b4bab-219">The following response represents the **SocialRestFollowingManager** instance for the current user.</span></span>
  
    
    



```
{"d":{
  "__metadata":{
    "id":"https://somecompany-a2ef5dfc05b1da.sharepoint.com/appInstance/_api/social.following/my/following",
    "uri":"https://somecompany-a2ef5dfc05b1da.sharepoint.com/appInstance/_api/social.following/my/following",
    "type":"SP.Social.SocialRestFollowingManager"
  },
  "MyFollowedDocumentsUri":"https://somecompany-my.sharepoint.com/personal/someone_somecompany_onmicrosoft_com/Social/FollowedContent.aspx",
  "MyFollowedSitesUri":"https://somecompany-my.sharepoint.com/personal/someone_somecompany_onmicrosoft_com/Social/Sites.aspx",
  "SocialActor":
    {"__metadata":{"type":"SP.Social.SocialActor"},
    "AccountName":"i:0#.f|membership|someone@somecompany.onmicrosoft.com",
    "ActorType":0,
    "CanFollow":false,
    "ContentUri":null,
    "EmailAddress":"someone@somecompany.onmicrosoft.com",
    "FollowedContentUri":null,
    "Id":"1.0f435d74164149cfa76e19ad21dc7c2e.8a7874906a9348189f2fb83295b598d5.06ff4087162c48dcb43828e4ddf82c38.98b9fc73d5224265b039586688b15b98",
    "ImageUri":"https://somecompany-my.sharepoint.com/User%20Photos/Profile%20Pictures/someone_somecompany_onmicrosoft_com_MThumb.jpg",
    "IsFollowed":false,
    "LibraryUri":null,
    "Name":"User Name",
    "PersonalSiteUri":"https://somecompany-my.sharepoint.com/personal/someone_somecompany_onmicrosoft_com/",
    "Status":0,
    "StatusText":"I like rabbits.",
    "TagGuid":"00000000-0000-0000-0000-000000000000",
    "Title":null,
    "Uri":"https://somecompany-my.sharepoint.com:443/Person.aspx?accountname=i%3A0%23%2Ef%7Cmembership%7Csomeone%40somecompany%2Eonmicrosoft%2Ecom"
  }
}}
```


## <a name="myfolloweddocumentsuri"></a><span data-ttu-id="b4bab-220">My/FollowedDocumentsUri</span><span class="sxs-lookup"><span data-stu-id="b4bab-220">My/FollowedDocumentsUri</span></span>
<span data-ttu-id="b4bab-221"><a name="bk_MyFollowedDocumentsUri"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-221"></span></span>

<span data-ttu-id="b4bab-222">Ruft den URI für die Seite **Dokumente, denen ich folge** für den aktuellen Benutzer ab.</span><span class="sxs-lookup"><span data-stu-id="b4bab-222">Gets the URI to the **Docs I'm following** page for the current user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="b4bab-223">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="b4bab-223">Endpoint URI structure</span></span>

 <span data-ttu-id="b4bab-224">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followeddocumentsuri`</span><span class="sxs-lookup"><span data-stu-id="b4bab-224">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followeddocumentsuri`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="b4bab-225">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="b4bab-225">Request parameter</span></span>

<span data-ttu-id="b4bab-226">Keine</span><span class="sxs-lookup"><span data-stu-id="b4bab-226">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="b4bab-227">Antwort</span><span class="sxs-lookup"><span data-stu-id="b4bab-227">Response</span></span>

 <span data-ttu-id="b4bab-228">**FollowedDocumentsUri**</span><span class="sxs-lookup"><span data-stu-id="b4bab-228">SSOM:  **FollowedDocumentsUri**</span></span>
  
    
    
<span data-ttu-id="b4bab-229">Typ: **String**</span><span class="sxs-lookup"><span data-stu-id="b4bab-229">Type: **String**</span></span>
  
    
    
<span data-ttu-id="b4bab-230">Der URI zur Seite **Dokumente, denen ich folge** für den aktuellen Benutzer.</span><span class="sxs-lookup"><span data-stu-id="b4bab-230">The URI to the **Docs I'm following** page for the current user.</span></span>
  
    
    
<span data-ttu-id="b4bab-231">Die folgende Antwort stellt die **FollowedDocumentsUri**-Instanz für den aktuellen Benutzer dar.</span><span class="sxs-lookup"><span data-stu-id="b4bab-231">The following response represents the **FollowedDocumentsUri** for the current user.</span></span>
  
    
    



```

{"d":{"FollowedDocumentsUri":"https://somecompany-my.sharepoint.com/personal/someone_somecompany_onmicrosoft_com/Social/FollowedContent.aspx"}}
```


## <a name="myfollowedsitesuri"></a><span data-ttu-id="b4bab-232">My/FollowedSitesUri</span><span class="sxs-lookup"><span data-stu-id="b4bab-232">My/FollowedSitesUri</span></span>
<span data-ttu-id="b4bab-233"><a name="bk_MyFollowedSitesUri"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-233"></span></span>

<span data-ttu-id="b4bab-234">Ruft den URI für die Seite **Website, denen ich folge** für den aktuellen Benutzer ab.</span><span class="sxs-lookup"><span data-stu-id="b4bab-234">Gets the URI to the **Sites I'm following** page for the current user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="b4bab-235">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="b4bab-235">Endpoint URI structure</span></span>

 <span data-ttu-id="b4bab-236">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followedsitesuri`</span><span class="sxs-lookup"><span data-stu-id="b4bab-236">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followedsitesuri`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="b4bab-237">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="b4bab-237">Request parameter</span></span>

<span data-ttu-id="b4bab-238">Keine</span><span class="sxs-lookup"><span data-stu-id="b4bab-238">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="b4bab-239">Antwort</span><span class="sxs-lookup"><span data-stu-id="b4bab-239">Response</span></span>

 <span data-ttu-id="b4bab-240">**FollowedSitesUri**</span><span class="sxs-lookup"><span data-stu-id="b4bab-240">SSOM:  **FollowedSitesUri**</span></span>
  
    
    
<span data-ttu-id="b4bab-241">Typ: **String**</span><span class="sxs-lookup"><span data-stu-id="b4bab-241">Type: **String**</span></span>
  
    
    
<span data-ttu-id="b4bab-242">Der URI zur Seite **Websites, denen ich folge** für den aktuellen Benutzer.</span><span class="sxs-lookup"><span data-stu-id="b4bab-242">The URI to the **Sites I'm following** page for the current user.</span></span>
  
    
    
<span data-ttu-id="b4bab-243">Die folgende Antwort stellt die **FollowedSitesUri**-Instanz für den aktuellen Benutzer dar.</span><span class="sxs-lookup"><span data-stu-id="b4bab-243">The following response represents the **FollowedSitesUri** for the current user.</span></span>
  
    
    



```
{"d":{"FollowedSitesUri":"https://somecompany-my.sharepoint.com/personal/someone_somecompany_onmicrosoft_com/Social/Sites.aspx"}}
```


## <a name="myfollowed"></a><span data-ttu-id="b4bab-244">My/Followed</span><span class="sxs-lookup"><span data-stu-id="b4bab-244">My/Followed</span></span>
<span data-ttu-id="b4bab-245"><a name="bk_Followed"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-245"></span></span>

<span data-ttu-id="b4bab-246">Ruft Benutzer, Dokumente, Websites und Tags ab, denen der aktuelle Benutzer folgt.</span><span class="sxs-lookup"><span data-stu-id="b4bab-246">Gets users, documents, sites, and tags that the current user is following.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="b4bab-247">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="b4bab-247">Endpoint URI structure</span></span>

 <span data-ttu-id="b4bab-248">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followed(types=15)`</span><span class="sxs-lookup"><span data-stu-id="b4bab-248">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followed(types=15)`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="b4bab-249">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="b4bab-249">Request parameter</span></span>

 <span data-ttu-id="b4bab-250">_types_</span><span class="sxs-lookup"><span data-stu-id="b4bab-250">_types_</span></span>
  
    
    
<span data-ttu-id="b4bab-251">Typ: **Int32**</span><span class="sxs-lookup"><span data-stu-id="b4bab-251">Type: **Int32**</span></span>
  
    
    
<span data-ttu-id="b4bab-p108">Die einzuschließenden Akteurtypen. Benutzer = 1, Dokumente = 2, Websites = 4, Tags = 8. Bitweise Kombinationen sind zulässig.</span><span class="sxs-lookup"><span data-stu-id="b4bab-p108">The actor types to include. Users = 1, Documents = 2, Sites = 4, Tags = 8. Bitwise combinations are allowed.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="b4bab-255">Antwort</span><span class="sxs-lookup"><span data-stu-id="b4bab-255">Response</span></span>

 <span data-ttu-id="b4bab-256">**Followed**</span><span class="sxs-lookup"><span data-stu-id="b4bab-256">**Followed**</span></span>
  
    
    
<span data-ttu-id="b4bab-257">Typ: Array von **SP.Social.SocialActor**</span><span class="sxs-lookup"><span data-stu-id="b4bab-257">Type: Array of **SP.Social.SocialActor**</span></span>
  
    
    
<span data-ttu-id="b4bab-258">Die Benutzer, Dokumente, Websites und Tags, denen der aktuelle Benutzer folgt.</span><span class="sxs-lookup"><span data-stu-id="b4bab-258">The users, documents, sites, and tags that the current user is following.</span></span>
  
    
    
<span data-ttu-id="b4bab-p109">Die folgende Antwort stellt ein Dokument, eine Website und ein Tag dar. Der Parameter  _types_ in der Anforderung gibt die Typen der einzuschließenden Akteure an.</span><span class="sxs-lookup"><span data-stu-id="b4bab-p109">The following response represents a document, a site, and a tag. The  _types_ parameter in the request specifies the types of actors to include.</span></span>
  
    
    



```
{"d":{"Followed":{"results":[
  {"__metadata":{"type":"SP.Social.SocialActor"}
  "AccountName":null
  "ActorType":1
  "CanFollow":true
  "ContentUri":"https://domain.sharepoint.com:443/Shared%20Documents/fileName.docx"
  "EmailAddress":null
  "FollowedContentUri":null
  "Id":"2.089f4944a6374a64b52b7af5ba140392.9340a4837688405daa6b83f2b58f973d.51bbb5d8e214457ba794669345d23040.98b9fc73d5224265b039586688b15b98"
  "ImageUri":null
  "IsFollowed":true
  "LibraryUri":null
  "Name":"snippets.txt"
  "PersonalSiteUri":null
  "Status":0
  "StatusText":null
  "TagGuid":"00000000-0000-0000-0000-000000000000"
  "Title":null
  "Uri":"https://domain.sharepoint.com:443/Shared%20Documents/fileName.docx"}
  {"__metadata":{"type":"SP.Social.SocialActor"}
  "AccountName":null
  "ActorType":2
  "CanFollow":true
  "ContentUri":"https://domain.sharepoint.com:443/"
  "EmailAddress":null
  "FollowedContentUri":null
  "Id":"8.089f4944a6374a64b52b7af5ba140392.9340a4837688405daa6b83f2b58f973d.089f4944a6374a64b52b7af5ba140392.98b9fc73d5224265b039586688b15b98"
  "ImageUri":null
  "IsFollowed":true
  "LibraryUri":null
  "Name":"Developer Site"
  "PersonalSiteUri":null
  "Status":0
  "StatusText":null
  "TagGuid":"00000000-0000-0000-0000-000000000000"
  "Title":null
  "Uri":"https://domain.sharepoint.com:443/"}
  {"__metadata":{"type":"SP.Social.SocialActor"}
  "AccountName":null
  "ActorType":3
  "CanFollow":true
  "ContentUri":null
  "EmailAddress":null
  "FollowedContentUri":null
  "Id":"16.00000000000000000000000000000000.00000000000000000000000000000000.19a4a484c1dc4bc58c93bb96245ce928.98b9fc73d5224265b039586688b15b98"
  "ImageUri":null
  "IsFollowed":true
  "LibraryUri":null
  "Name":"#someTag"
  "PersonalSiteUri":null
  "Status":0
  "StatusText":null
  "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928"
  "Title":null
  "Uri":"https://somecompany-my.sharepoint.com:443/_layouts/15/HashTagProfile.aspx?
    TermID=19a4a484-c1dc-4bc5-8c93-bb96245ce928"}
]}}}
```


## <a name="myfollowedcount"></a><span data-ttu-id="b4bab-261">My/FollowedCount</span><span class="sxs-lookup"><span data-stu-id="b4bab-261">My/FollowedCount</span></span>
<span data-ttu-id="b4bab-262"><a name="bk_FollowedCount"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-262"></span></span>

<span data-ttu-id="b4bab-263">Ruft die Anzahl der Benutzer, Dokumente, Websites und Tags ab, denen der aktuelle Benutzer folgt.</span><span class="sxs-lookup"><span data-stu-id="b4bab-263">Gets the count of users, documents, sites, and tags that the current user is following.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="b4bab-264">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="b4bab-264">Endpoint URI structure</span></span>

 <span data-ttu-id="b4bab-265">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followedcount(types=15)`</span><span class="sxs-lookup"><span data-stu-id="b4bab-265">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followedcount(types=15)`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="b4bab-266">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="b4bab-266">Request parameter</span></span>

 <span data-ttu-id="b4bab-267">_types_</span><span class="sxs-lookup"><span data-stu-id="b4bab-267">_types_</span></span>
  
    
    
<span data-ttu-id="b4bab-268">Typ: **Int32**</span><span class="sxs-lookup"><span data-stu-id="b4bab-268">Type: **Int32**</span></span>
  
    
    
<span data-ttu-id="b4bab-p110">Die einzuschließenden Akteurtypen. Benutzer = 1, Dokumente = 2, Websites = 4, Tags = 8. Bitweise Kombinationen sind zulässig.</span><span class="sxs-lookup"><span data-stu-id="b4bab-p110">The types of actors to include. Users = 1, Documents = 2, Sites = 4, Tags = 8. Bitwise combinations are allowed.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="b4bab-272">Antwort</span><span class="sxs-lookup"><span data-stu-id="b4bab-272">Response</span></span>

 <span data-ttu-id="b4bab-273">**FollowedCount**</span><span class="sxs-lookup"><span data-stu-id="b4bab-273">**FollowedCount**</span></span>
  
    
    
<span data-ttu-id="b4bab-274">Typ: **Int32**</span><span class="sxs-lookup"><span data-stu-id="b4bab-274">Type: **Int32**</span></span>
  
    
    
<span data-ttu-id="b4bab-275">Die Anzahl der Benutzer, Dokumente, Websites und Tags, denen der aktuelle Benutzer folgt.</span><span class="sxs-lookup"><span data-stu-id="b4bab-275">The count of users, documents, sites, and tags that the current user is following.</span></span>
  
    
    
<span data-ttu-id="b4bab-p111">Die folgende Antwort weist darauf hin, dass der aktuelle Benutzer 3 Akteuren des angegebenen Typs folgt. Der Parameter  _types_ in der Anforderung gibt die Typen einzuschließenden Akteure an.</span><span class="sxs-lookup"><span data-stu-id="b4bab-p111">The following response indicates that the current user is following 3 actors of the specified type. The  _types_ parameter in the request specifies the types of actors to include.</span></span>
  
    
    



```

{"d":{"FollowedCount":3}}
```


## <a name="myfollowers"></a><span data-ttu-id="b4bab-278">My/Followers</span><span class="sxs-lookup"><span data-stu-id="b4bab-278">My/Followers</span></span>
<span data-ttu-id="b4bab-279"><a name="bk_Followers"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-279"></span></span>

<span data-ttu-id="b4bab-280">Ruft die Benutzer ab, die dem aktuellen Benutzer folgen.</span><span class="sxs-lookup"><span data-stu-id="b4bab-280">Gets the users who are following the current user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="b4bab-281">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="b4bab-281">Endpoint URI structure</span></span>

 <span data-ttu-id="b4bab-282">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followers`</span><span class="sxs-lookup"><span data-stu-id="b4bab-282">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followers`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="b4bab-283">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="b4bab-283">Request parameter</span></span>

<span data-ttu-id="b4bab-284">Keine</span><span class="sxs-lookup"><span data-stu-id="b4bab-284">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="b4bab-285">Antwort</span><span class="sxs-lookup"><span data-stu-id="b4bab-285">Response</span></span>

 <span data-ttu-id="b4bab-286">**Followers**</span><span class="sxs-lookup"><span data-stu-id="b4bab-286">**Followers**</span></span>
  
    
    
<span data-ttu-id="b4bab-287">Typ: Array von **SP.Social.SocialActor**</span><span class="sxs-lookup"><span data-stu-id="b4bab-287">Type: Array of **SP.Social.SocialActor**</span></span>
  
    
    

  
    
    
<span data-ttu-id="b4bab-288">Die folgende Antwort stellt einen Benutzer dar, der dem aktuellen Benutzer folgt.</span><span class="sxs-lookup"><span data-stu-id="b4bab-288">The following response represents one user who is following the current user.</span></span>
  
    
    



```
{"d":{"Followers":{"results":[
  {"__metadata":{"type":"SP.Social.SocialActor"},
  "AccountName":"domain\\user",
  "ActorType":0, 
  "CanFollow":true, 
  "ContentUri":null, 
  "EmailAddress":"user@domain.com", 
  "FollowedContentUri":null, 
  "Id":"1.60a6bd2d1537446880bb4a5a5b07fd63.3a6c6893e6b549cebffefcfa97412dcf.00093edb336e47ac8791bab0a0b77c5d.0c37852b34d0418e91c62ac25af4be5b",
  "ImageUri":null, 
  "IsFollowed":true, 
  "LibraryUri":null, 
  "Name":"User Name",
  "PersonalSiteUri":"http://server/my/personal/user/",
  "Status":0, 
  "StatusText":"",
  "TagGuid":"00000000-0000-0000-0000-000000000000",
  "Title":"SALES DIRECTOR", 
  "Uri":"http://server:80/my/Person.aspx?accountname=domain%5Cuser"}
]}}}
```


## <a name="mysuggestions"></a><span data-ttu-id="b4bab-289">My/Suggestions</span><span class="sxs-lookup"><span data-stu-id="b4bab-289">My/Suggestions</span></span>
<span data-ttu-id="b4bab-290"><a name="bk_Suggestions"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-290"></span></span>

<span data-ttu-id="b4bab-291">Ruft die Benutzer ab, denen der aktuelle Benutzer möglicherweise folgen möchte.</span><span class="sxs-lookup"><span data-stu-id="b4bab-291">Gets users who the current user might want to follow.</span></span>
  
    
    

> <span data-ttu-id="b4bab-292">**Hinweis:** Die Funktion für Personenvorschläge hängt von den Folgeaktivitäten des Benutzers, Suchdurchforstungen und Suchanalysen ab.</span><span class="sxs-lookup"><span data-stu-id="b4bab-292">**Note** People Suggestions functionality depends on users' following activities, search crawls, and search analytics. See  How People Suggestions works on SharePoint Online.</span></span> <span data-ttu-id="b4bab-293">Siehe [Funktionsweise von Personenvorschlägen auf SharePoint Online](follow-people-in-sharepoint.md#bk_PeopleSuggestions).</span><span class="sxs-lookup"><span data-stu-id="b4bab-293">How People Suggestions works on SharePoint Online</span></span> 
  
    
    


### <a name="endpoint-uri-structure"></a><span data-ttu-id="b4bab-294">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="b4bab-294">Endpoint URI structure</span></span>

 <span data-ttu-id="b4bab-295">**GET** `http://<siteCollection>/<site>/_api/social.following/my/suggestions`</span><span class="sxs-lookup"><span data-stu-id="b4bab-295">**GET** `http://<siteCollection>/<site>/_api/social.following/my/suggestions`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="b4bab-296">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="b4bab-296">Request parameter</span></span>

<span data-ttu-id="b4bab-297">Keine</span><span class="sxs-lookup"><span data-stu-id="b4bab-297">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="b4bab-298">Antwort</span><span class="sxs-lookup"><span data-stu-id="b4bab-298">Response</span></span>

 <span data-ttu-id="b4bab-299">**Suggestions**</span><span class="sxs-lookup"><span data-stu-id="b4bab-299">**Suggestions**</span></span>
  
    
    
<span data-ttu-id="b4bab-300">Typ: Array von **SP.Social.SocialActor**</span><span class="sxs-lookup"><span data-stu-id="b4bab-300">Type: Array of **SP.Social.SocialActor**</span></span>
  
    
    
<span data-ttu-id="b4bab-301">Benutzer, dem der aktuelle Benutzer möglicherweise folgen möchte.</span><span class="sxs-lookup"><span data-stu-id="b4bab-301">Users who the current user might want to follow.</span></span>
  
    
    

## <a name="getmysuggestions"></a><span data-ttu-id="b4bab-302">GetMySuggestions</span><span class="sxs-lookup"><span data-stu-id="b4bab-302">/getmysuggestions</span></span>
<span data-ttu-id="b4bab-303"><a name="bk_GetMySuggestions"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-303"></span></span>

<span data-ttu-id="b4bab-304">Ruft die Benutzer ab, denen der aktuelle Benutzer möglicherweise folgen möchte.</span><span class="sxs-lookup"><span data-stu-id="b4bab-304">Gets users who the current user might want to follow.</span></span>
  
    
    

> <span data-ttu-id="b4bab-305">**Hinweis:** Die Funktion für Personenvorschläge hängt von den Folgeaktivitäten des Benutzers, Suchdurchforstungen und Suchanalysen ab.</span><span class="sxs-lookup"><span data-stu-id="b4bab-305">**Note** People Suggestions functionality depends on users' following activities, search crawls, and search analytics. See  How People Suggestions works on SharePoint Online.</span></span> <span data-ttu-id="b4bab-306">Siehe [Funktionsweise von Personenvorschlägen auf SharePoint Online](follow-people-in-sharepoint.md#bk_PeopleSuggestions).</span><span class="sxs-lookup"><span data-stu-id="b4bab-306">How People Suggestions works on SharePoint Online</span></span> 
  
    
    


### <a name="endpoint-uri-structure"></a><span data-ttu-id="b4bab-307">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="b4bab-307">Endpoint URI structure</span></span>

 <span data-ttu-id="b4bab-308">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getmysuggestions`</span><span class="sxs-lookup"><span data-stu-id="b4bab-308">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getmysuggestions`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="b4bab-309">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="b4bab-309">Request parameter</span></span>

<span data-ttu-id="b4bab-310">Keine</span><span class="sxs-lookup"><span data-stu-id="b4bab-310">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="b4bab-311">Antwort</span><span class="sxs-lookup"><span data-stu-id="b4bab-311">Response</span></span>

 <span data-ttu-id="b4bab-312">**Suggestions**</span><span class="sxs-lookup"><span data-stu-id="b4bab-312">**Suggestions**</span></span>
  
    
    
<span data-ttu-id="b4bab-313">Typ: Liste von **SP.UserProfiles.PersonProperties**</span><span class="sxs-lookup"><span data-stu-id="b4bab-313">Type: List of **SP.UserProfiles.PersonProperties**</span></span>
  
    
    
<span data-ttu-id="b4bab-314">Benutzer, dem der aktuelle Benutzer möglicherweise folgen möchte.</span><span class="sxs-lookup"><span data-stu-id="b4bab-314">Users who the current user might want to follow.</span></span>
  
    
    

## <a name="ismypeoplelistpublic"></a><span data-ttu-id="b4bab-315">IsMyPeopleListPublic</span><span class="sxs-lookup"><span data-stu-id="b4bab-315">SSOM:  IsMyPeopleListPublic</span></span>
<span data-ttu-id="b4bab-316"><a name="bk_IsMyPeopleListPublic"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-316"></span></span>

<span data-ttu-id="b4bab-317">Findet heraus, ob die Liste **Personen, denen ich folge** für den aktuellen Benutzer öffentlich ist.</span><span class="sxs-lookup"><span data-stu-id="b4bab-317">Finds out whether the **People I'm Following** list for the current user is public.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="b4bab-318">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="b4bab-318">Endpoint URI structure</span></span>

 <span data-ttu-id="b4bab-319">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/ismypeoplelistpublic`</span><span class="sxs-lookup"><span data-stu-id="b4bab-319">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/ismypeoplelistpublic`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="b4bab-320">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="b4bab-320">Request parameter</span></span>

<span data-ttu-id="b4bab-321">Keine</span><span class="sxs-lookup"><span data-stu-id="b4bab-321">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="b4bab-322">Antwort</span><span class="sxs-lookup"><span data-stu-id="b4bab-322">Response</span></span>

 <span data-ttu-id="b4bab-323">**IsMyPeopleListPublic**</span><span class="sxs-lookup"><span data-stu-id="b4bab-323">SSOM:  **IsMyPeopleListPublic**</span></span>
  
    
    
<span data-ttu-id="b4bab-324">Typ: **bool**</span><span class="sxs-lookup"><span data-stu-id="b4bab-324">Type: **bool**</span></span>
  
    
    
 <span data-ttu-id="b4bab-325">**true**, wenn die Personenliste des aktuellen Benutzer öffentlich ist, andernfalls **false**.</span><span class="sxs-lookup"><span data-stu-id="b4bab-325">**true** if the current user's people list is public; otherwise **false**.</span></span>
  
    
    
<span data-ttu-id="b4bab-326">Die folgende Antwort weist darauf hin, dass die Personenliste des aktuellen Benutzers öffentlich ist.</span><span class="sxs-lookup"><span data-stu-id="b4bab-326">The following response indicates that the current user's people list is public.</span></span>
  
    
    



```

{"d":{"IsMyPeopleListPublic":true}}
```


## <a name="amifollowedby"></a><span data-ttu-id="b4bab-327">AmIFollowedBy</span><span class="sxs-lookup"><span data-stu-id="b4bab-327">SSOM:  AmIFollowedBy</span></span>
<span data-ttu-id="b4bab-328"><a name="bk_AmIFollowedBy"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-328"></span></span>

<span data-ttu-id="b4bab-329">Findet heraus, ob ein bestimmter Benutzer dem aktuellen Benutzer folgt.</span><span class="sxs-lookup"><span data-stu-id="b4bab-329">Finds out whether a specified user is following the current user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="b4bab-330">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="b4bab-330">Endpoint URI structure</span></span>

 <span data-ttu-id="b4bab-331">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/amifollowedby(accountName=@v)?@v='domain\\user'`</span><span class="sxs-lookup"><span data-stu-id="b4bab-331">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/amifollowedby(accountName=@v)?@v='domain\\user'`</span></span>
  
    
    
 <span data-ttu-id="b4bab-332">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/amifollowedby(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span><span class="sxs-lookup"><span data-stu-id="b4bab-332">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/amifollowedby(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="b4bab-333">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="b4bab-333">Request parameter</span></span>

 <span data-ttu-id="b4bab-334">_accountName_</span><span class="sxs-lookup"><span data-stu-id="b4bab-334">_accountName_</span></span>
  
    
    
<span data-ttu-id="b4bab-335">Typ: **String**</span><span class="sxs-lookup"><span data-stu-id="b4bab-335">Type: **String**</span></span>
  
    
    
<span data-ttu-id="b4bab-336">Der Kontoname des Zielbenutzers.</span><span class="sxs-lookup"><span data-stu-id="b4bab-336">The account name of the target user.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="b4bab-337">Antwort</span><span class="sxs-lookup"><span data-stu-id="b4bab-337">Response</span></span>

 <span data-ttu-id="b4bab-338">**AmIFollowedBy**</span><span class="sxs-lookup"><span data-stu-id="b4bab-338">SSOM:  **AmIFollowedBy**</span></span>
  
    
    
<span data-ttu-id="b4bab-339">Typ: **bool**</span><span class="sxs-lookup"><span data-stu-id="b4bab-339">Type: **bool**</span></span>
  
    
    
 <span data-ttu-id="b4bab-340">**true**, wenn der angegebene Benutzer dem aktuellen Benutzer folgt, andernfalls **false**.</span><span class="sxs-lookup"><span data-stu-id="b4bab-340">**true** if the specified user is following the current user; otherwise **false**.</span></span>
  
    
    
<span data-ttu-id="b4bab-341">Die folgende Antwort weist darauf hin, dass der angegebene Benutzer dem aktuellen Benutzer nicht folgt.</span><span class="sxs-lookup"><span data-stu-id="b4bab-341">The following response indicates that the specified user is not following the current user.</span></span>
  
    
    



```
{"d":{"AmIFollowedBy":false}}
```


## <a name="getpeoplefollowedby"></a><span data-ttu-id="b4bab-342">GetPeopleFollowedBy</span><span class="sxs-lookup"><span data-stu-id="b4bab-342">SSOM:  GetPeopleFollowedBy</span></span>
<span data-ttu-id="b4bab-343"><a name="bk_GetPeopleFollowedBy"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-343"></span></span>

<span data-ttu-id="b4bab-344">Ruft die Benutzer ab, denen von einem angegebenen Benutzer gefolgt wird.</span><span class="sxs-lookup"><span data-stu-id="b4bab-344">Gets the users followed by a specified user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="b4bab-345">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="b4bab-345">Endpoint URI structure</span></span>

 <span data-ttu-id="b4bab-346">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getpeoplefollowedby(accountName=@v)?@v='domain\\user'`</span><span class="sxs-lookup"><span data-stu-id="b4bab-346">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getpeoplefollowedby(accountName=@v)?@v='domain\\user'`</span></span>
  
    
    
 <span data-ttu-id="b4bab-347">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getpeoplefollowedby(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span><span class="sxs-lookup"><span data-stu-id="b4bab-347">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getpeoplefollowedby(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="b4bab-348">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="b4bab-348">Request parameter</span></span>

 <span data-ttu-id="b4bab-349">_accountName_</span><span class="sxs-lookup"><span data-stu-id="b4bab-349">_accountName_</span></span>
  
    
    
<span data-ttu-id="b4bab-350">Typ: **String**</span><span class="sxs-lookup"><span data-stu-id="b4bab-350">Type: **String**</span></span>
  
    
    
<span data-ttu-id="b4bab-351">Der Kontoname des Zielbenutzers.</span><span class="sxs-lookup"><span data-stu-id="b4bab-351">The account name of the target user.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="b4bab-352">Antwort</span><span class="sxs-lookup"><span data-stu-id="b4bab-352">Response</span></span>

 <span data-ttu-id="b4bab-353">**GetPeopleFollowedBy**</span><span class="sxs-lookup"><span data-stu-id="b4bab-353">SSOM:  **GetPeopleFollowedBy**</span></span>
  
    
    
<span data-ttu-id="b4bab-354">Typ: Liste von **SP.UserProfiles.PersonProperties**</span><span class="sxs-lookup"><span data-stu-id="b4bab-354">Type: List of **SP.UserProfiles.PersonProperties**</span></span>
  
    
    
<span data-ttu-id="b4bab-355">Die Benutzer, denen vom angegebenen Benutzer gefolgt wird.</span><span class="sxs-lookup"><span data-stu-id="b4bab-355">The users followed by the specified user.</span></span>
  
    
    
<span data-ttu-id="b4bab-356">Die folgende Antwort stellt zwei Benutzer dar, die dem angegebenen Benutzer folgen.</span><span class="sxs-lookup"><span data-stu-id="b4bab-356">The following response represents two users followed by the specified user.</span></span>
  
    
    



```
{"d":{"results":[
  {"__metadata":{
    "id":"http://server/sites/dev/_api/SP.UserProfiles.PersonPropertiesa776ccd0-5566-47d2-9d59-3422cf1fb362",
    "uri":"http://server/sites/dev/_api/SP.UserProfiles.PersonPropertiesa776ccd0-5566-47d2-9d59-3422cf1fb362",
    "type":"SP.UserProfiles.PersonProperties"
  },
  "AccountName":"domain\\user1",
  "DirectReports":{"results":[]},
  "DisplayName":"User Name",
  "Email":"user@domain.com",
  "ExtendedManagers":{"results":[]},
  "ExtendedReports":{"results":["domain\\user1"]},
  "IsFollowed":true,
  "LatestPost":null,
  "Peers":{"results":[]},
  "PersonalUrl":"http://server/my/personal/user1/",
  "PictureUrl":null,
  "Title":null,
  "UserProfileProperties":{"results":[
    {"__metadata":{"type":"SP.KeyValue"},"Key":"UserProfile_GUID","Value":"00093edb-336e-47ac-8791-bab0a0b77c5d","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SID","Value":"S-1-5-09-4830882673-197582990-1037597527-29477","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"ADGuid","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"AccountName","Value":"domain\\user1","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"FirstName","Value":"User","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticFirstName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"LastName","Value":"Name","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticLastName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PreferredName","Value":"User Name","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticDisplayName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WorkPhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Department","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Title","Value":"SALES DIRECTOR","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-JobTitle","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Department","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Manager","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"AboutMe","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PersonalSpace","Value":"/my/personal/user1/","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PictureURL","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"UserName","Value":"user1","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"QuickLinks","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WebSite","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PublicSiteRedirect","Value":"http://cox64-096/my/personal/user1/","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Dotted-line","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Peers","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Responsibility","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SipAddress","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MySiteUpgrade","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ProxyAddresses","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-HireDate","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DisplayOrder","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimProviderID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimProviderType","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SavedAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SavedSID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ResourceSID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ResourceAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ObjectExists","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MasterAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-UserPrincipalName","Value":"user1@company.com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PersonalSiteCapabilities","Value":"14","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-O15FirstRunExperience","Value":"15","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PersonalSiteInstantiationState","Value":"2","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DistinguishedName","Value":"CN=user1 (User Name),OU=UserAccounts,DC=domain,DC=corp,DC=company,DC=com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SourceObjectDN","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-FeedIdentifier","Value":"http://server/my/personal/user1;1.60a6bd2d1537446880bb4a5a5b07fd63.3a6c6893e6b549cebffefcfa97412dcf.50dcee8186ae4dd6904d1650d3d39e54.0c37852b34d0418e91c62ac25af4be5b","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WorkEmail","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"CellPhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Fax","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"HomePhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Office","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Location","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Assistant","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PastProjects","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Skills","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-School","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Birthday","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-StatusNotes","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Interests","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-HashTags","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-EmailOptin","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PrivacyPeople","Value":"True","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PrivacyActivity","Value":"4095","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-TimeZone","Value":"","ValueType":"Edm.String"}]
  },
  "UserUrl":"http://server:80/my/Person.aspx?accountname=domain%5Cuser1"},
  {"__metadata":{
    "id":"http://server/sites/dev/_api/SP.UserProfiles.PersonPropertiesf0ddf6e4-e69c-453f-9a7f-44e0e47d89d4",
    "uri":"http://server/sites/dev/_api/SP.UserProfiles.PersonPropertiesf0ddf6e4-e69c-453f-9a7f-44e0e47d89d4",
    "type":"SP.UserProfiles.PersonProperties"},
  "AccountName":"domain\\user2",
  "DirectReports":{"results":[]},
  "DisplayName":"User Name",
  "Email":"user2@company.com", 
  "ExtendedManagers":{"results":[]},
  "ExtendedReports":{"results":["domain\\user2"]},
  "IsFollowed":true,"LatestPost":null, 
  "Peers":{"results":[]},
  "PersonalUrl":"http://server/my/Person.aspx?accountname=domain%5Cuser2",
  "PictureUrl":null, 
  "Title":null, 
  "UserProfileProperties":{"results":[
    {"__metadata":{"type":"SP.KeyValue"},"Key":"UserProfile_GUID","Value":"40deca2e-6231-43f9-9559-9a51b0135067","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SID","Value":" S-1-5-09-4830882673-197582990-1037597527-0688328","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"ADGuid","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"AccountName","Value":"domain\\user2","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"FirstName","Value":"User","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticFirstName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"LastName","Value":"Name","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticLastName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PreferredName","Value":"User2","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticDisplayName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WorkPhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Department","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Title","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-JobTitle","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Department","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Manager","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"AboutMe","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PersonalSpace","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PictureURL","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"UserName","Value":"user2","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"QuickLinks","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WebSite","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PublicSiteRedirect","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Dotted-line","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Peers","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Responsibility","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SipAddress","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MySiteUpgrade","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ProxyAddresses","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-HireDate","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DisplayOrder","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimProviderID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimProviderType","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SavedAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SavedSID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ResourceSID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ResourceAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ObjectExists","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MasterAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-UserPrincipalName","Value":"user2@company.com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PersonalSiteCapabilities","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-O15FirstRunExperience","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PersonalSiteInstantiationState","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DistinguishedName","Value":"CN=User2,OU=UserAccounts,DC=domain,DC=corp,DC=company,DC=com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SourceObjectDN","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-FeedIdentifier","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WorkEmail","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"CellPhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Fax","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"HomePhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Office","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Location","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Assistant","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PastProjects","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Skills","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-School","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Birthday","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-StatusNotes","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Interests","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-HashTags","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-EmailOptin","Value":"0","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PrivacyPeople","Value":"True","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PrivacyActivity","Value":"4095","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-TimeZone","Value":"","ValueType":"Edm.String"}]
  },
  "UserUrl":"http://server:80/my/Person.aspx?accountname=domain%5Cuser2"}
]}}
```


## <a name="getfollowersfor"></a><span data-ttu-id="b4bab-357">GetFollowersFor</span><span class="sxs-lookup"><span data-stu-id="b4bab-357">CSOM:  GetFollowersFor</span></span>
<span data-ttu-id="b4bab-358"><a name="bk_GetFollowersFor"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-358"></span></span>

<span data-ttu-id="b4bab-359">Ruft die Benutzer ab, die einem angegebenen Benutzer folgen.</span><span class="sxs-lookup"><span data-stu-id="b4bab-359">Gets the users who are following a specified user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="b4bab-360">Endpunkt-URI-Struktur</span><span class="sxs-lookup"><span data-stu-id="b4bab-360">Endpoint URI structure</span></span>

 <span data-ttu-id="b4bab-361">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getfollowersfor(accountName=@v)?@v='domain\\user'`</span><span class="sxs-lookup"><span data-stu-id="b4bab-361">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getfollowersfor(accountName=@v)?@v='domain\\user'`</span></span>
  
    
    
 <span data-ttu-id="b4bab-362">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getfollowersfor(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span><span class="sxs-lookup"><span data-stu-id="b4bab-362">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getfollowersfor(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="b4bab-363">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="b4bab-363">Request parameter</span></span>

 <span data-ttu-id="b4bab-364">_accountName_</span><span class="sxs-lookup"><span data-stu-id="b4bab-364">_accountName_</span></span>
  
    
    
<span data-ttu-id="b4bab-365">Typ: **String**</span><span class="sxs-lookup"><span data-stu-id="b4bab-365">Type: **String**</span></span>
  
    
    
<span data-ttu-id="b4bab-366">Der Kontoname des Zielbenutzers.</span><span class="sxs-lookup"><span data-stu-id="b4bab-366">The account name of the target user.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="b4bab-367">Antwort</span><span class="sxs-lookup"><span data-stu-id="b4bab-367">Response</span></span>

 <span data-ttu-id="b4bab-368">**GetFollowersFor**</span><span class="sxs-lookup"><span data-stu-id="b4bab-368">SSOM:  **GetFollowersFor**</span></span>
  
    
    
<span data-ttu-id="b4bab-369">Typ: Liste von **SP.UserProfiles.PersonProperties**</span><span class="sxs-lookup"><span data-stu-id="b4bab-369">Type: List of **SP.UserProfiles.PersonProperties**</span></span>
  
    
    
<span data-ttu-id="b4bab-370">Die Benutzer, die dem angegebenen Benutzer folgen.</span><span class="sxs-lookup"><span data-stu-id="b4bab-370">The users who are following the specified user.</span></span>
  
    
    
<span data-ttu-id="b4bab-371">Die folgende Antwort stellt einen Benutzer dar, der dem angegebenen Benutzer folgt.</span><span class="sxs-lookup"><span data-stu-id="b4bab-371">The following response represents a user who is following the specified user.</span></span>
  
    
    



```

{"d":{"results":[
  {"__metadata":{
    "id":"http://server/sites/dev/_api/SP.UserProfiles.PersonPropertiesabe0c40e-ce77-4631-9fc9-ec20b859061c",
    "uri":"http://server/sites/dev/_api/SP.UserProfiles.PersonPropertiesabe0c40e-ce77-4631-9fc9-ec20b859061c",
    "type":"SP.UserProfiles.PersonProperties"
  },
  "AccountName":"domain\\user",
  "DirectReports":{"results":[]},
  "DisplayName":"User Name",
  "Email":"user@domain.com",
  "ExtendedManagers":{"results":[]},
  "ExtendedReports":{"results":["domain\\user"]},
  "IsFollowed":false,
  "LatestPost":"#tally",
  "Peers":{"results":[]},
  "PersonalUrl":"http://server/my/personal/user/",
  "PictureUrl":null,
  "Title":"MARKETING DIRECTOR",
  "UserProfileProperties":{"results":[
    {"__metadata":{"type":"SP.KeyValue"},"Key":"UserProfile_GUID","Value":"fa59ba73-edd4-4dc9-97d1-8ada702aae7f","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SID","Value":" S-1-5-09-4830882673-197582990-1037597527-002428","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"ADGuid","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"AccountName","Value":"domain\\user","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"FirstName","Value":"User","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticFirstName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"LastName","Value":"Name","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticLastName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PreferredName","Value":"User Name","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticDisplayName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WorkPhone","Value":"+1 (208) 3192190 X2190","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Department","Value":"Marketing","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Title","Value":"MARKETING DIRECTOR","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-JobTitle","Value":"MARKETING DIRECTOR","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Department","Value":"Marketing","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Manager","Value":"DOMAIN\\randalli","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"AboutMe","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PersonalSpace","Value":"/my/personal/user/","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PictureURL","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"UserName","Value":"user","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"QuickLinks","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WebSite","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PublicSiteRedirect","Value":"http://my/sites/user/","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DataSource","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MemberOf","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Dotted-line","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Peers","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Responsibility","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SipAddress","Value":"user@domain.com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MySiteUpgrade","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DontSuggestList","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ProxyAddresses","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-HireDate","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DisplayOrder","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimProviderID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimProviderType","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-LastColleagueAdded","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-OWAUrl","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SavedAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SavedSID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ResourceSID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ResourceAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ObjectExists","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MasterAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-UserPrincipalName","Value":"user@domain.com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PersonalSiteCapabilities","Value":"14","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-O15FirstRunExperience","Value":"15","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PersonalSiteInstantiationState","Value":"2","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DistinguishedName","Value":"CN=User Name,OU=UserAccounts,DC=domain,DC=corp,DC=company,DC=com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SourceObjectDN","Value":"CN=User Name,OU=UserAccounts,DC=domain,DC=corp,DC=company,DC=com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-LastKeywordAdded","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-FeedIdentifier","Value":"http://server/my/personal/user;1.64769ec247734e699a5616f1701f7d94.ab42c829ec534daa99fc5909ef940213.3fb2a502be274948a665fcb5e8b2a58d.0c37852b34d0418e91c62ac25af4be5b","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WorkEmail","Value":"user@domain.com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"CellPhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Fax","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"HomePhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Office","Value":"2253","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Location","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Assistant","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PastProjects","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Skills","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-School","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Birthday","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-StatusNotes","Value":"#tally","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Interests","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-HashTags","Value":"#tally","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-EmailOptin","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PrivacyPeople","Value":"True","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PrivacyActivity","Value":"4095","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MUILanguages","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ContentLanguages","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-TimeZone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-RegionalSettings-FollowWeb","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Locale","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-CalendarType","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-AltCalendarType","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-AdjustHijriDays","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ShowWeeks","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-WorkDays","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-WorkDayStartHour","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-WorkDayEndHour","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Time24","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-FirstDayOfWeek","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-FirstWeekOfYear","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-RegionalSettings-Initialized","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"EduUserRole","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"EduPersonalSiteState","Value":"","ValueType":"Edm.String"}, 
    {"__metadata":{"type":"SP.KeyValue"},"Key":"EduOAuthTokenProviders","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SISUserId","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"EduExternalSyncState","Value":"","ValueType":"Edm.String"}]
  },
  "UserUrl":"http://server:80/my/Person.aspx?accountname=domain%5Cuser"}
]}}
```


## <a name="additional-resources"></a><span data-ttu-id="b4bab-372">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="b4bab-372">Additional resources</span></span>
<span data-ttu-id="b4bab-373"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b4bab-373"></span></span>


-  [<span data-ttu-id="b4bab-374">Vorgehensweise: führen Sie Dokumente, Websites und Tags mithilfe des REST-Diensts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b4bab-374">How to: Follow documents, sites, and tags by using the REST service in SharePoint</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)
    
  
-  [<span data-ttu-id="b4bab-375">REST-API-Referenz für sozialen Feed für SharePoint</span><span class="sxs-lookup"><span data-stu-id="b4bab-375">Social feed REST API reference for SharePoint</span></span>](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="b4bab-376">SharePoint User Profiles JavaScript Reference (sp.userprofiles.js)</span><span class="sxs-lookup"><span data-stu-id="b4bab-376">SharePoint User Profiles JavaScript Reference (sp.userprofiles.js)</span></span>](http://msdn.microsoft.com/library/80cf5436-6aa2-6f11-a782-66a04f6e2fb0%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="b4bab-377">Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b4bab-377">Get started developing with social features in SharePoint</span></span>](get-started-developing-with-social-features-in-sharepoint.md)
    
  