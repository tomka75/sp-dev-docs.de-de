---
title: "REST-API-Referenz zum Folgen von Personen und Inhalten für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c05755df-846d-4a39-941d-950d066cc6d4
ms.openlocfilehash: 4e2cbe5819a0e5d2e5c58a1675503d5e899d6805
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="following-people-and-content-rest-api-reference-for-sharepoint"></a>REST-API-Referenz zum Folgen von Personen und Inhalten für SharePoint
Suchen Sie nach SharePoint-REST-Endpunkten, um über die Ressourcen **SocialRestFollowingManager** und **PeopleManager** Personen und Inhalten zu folgen. Sie können den SharePoint-REST-Dienst (Representational State Transfer) verwenden, um dieselben Aufgaben durchzuführen wie bei Verwendung der .NET-Clientobjektmodelle und des JavaScript-Objektmodells. Für die Verwendung des REST-Diensts erstellen und senden Sie HTTP **GET**- und **POST**-Anforderungen an die Ressourcenendpunkte, die die gewünschten Aufgaben darstellen. Diese Ressourcenendpunkte entsprechen SharePoint-Objekten, -Eigenschaften und -Methoden.
  
    
    

Der Endpunkt-URI für die meisten Aufgaben zum Folgen beginnt mit der Ressource **SocialRestFollowingManager** ( `social.following`) und endet mit der Ressource, die die bestimmte Aufgabe ausführt. Sie verwenden beispielsweise den URI  `http://www.contoso.com/_api/social.following/follow`, damit der aktuelle Benutzer beginnt, Personen oder Inhalten zu folgen, und den URI  `https://www.contoso.com/sites/devSite/_api/social.following/followed`, um die Personen oder Inhalte abzurufen, denen der aktuelle Benutzer folgt.

> [!NOTE]
> In diesem Artikel werden der Endpunkt-URI und die Parameterkomponenten der HTTP-Anforderungen gezeigt. Beispiele zu vollständigen Anfragen finden Sie unter [Vorgehensweise: Nachverfolgen von Dokumenten, Websites und Tags mit dem REST-Dienst von SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md). 
  
    
    

Wir empfehlen die Verwendung der **SocialRestFollowingManager**-API für Aufgaben zum Folgen von Personen und Inhalten, aber Sie können auch die Ressource **PeopleManager** für einige Aufgaben rund um das Folgen von Personen verwenden, die **SocialRestFollowingManager** nicht unterstützt. Sie können z. B. herausfinden, ob jemand dem aktuellen Benutzer folgt oder die Follower eines anderen Benutzers abrufen. Für diese Aufgaben senden Sie HTTP **GET**-Anforderungen an Endpunkt-URIs, die mit der Ressource **PeopleManager** ( `sp.userprofiles.peoplemanager`) beginnen und mit der Ressource enden, die die bestimmte Aufgabe ausführt.Wenn der Endpunkt einen Parameter annimmt, werden die Parametermetadaten im URI oder im Anforderungstext im XML- oder JavaScript Object Notation (JSON)-Format gesendet. Sie können HTTP-Anforderungen in jeder Sprache, einschließlich JavaScript und C# durchführen. Standardmäßig gibt der REST-Dienst Antworten zurück, die mithilfe des Atom-Protokolls formatiert sind, aber Sie können das JSON-Format mithilfe von HTTP **Accept**-Headern anfordern. Weitere Informationen finden Sie unter  [Programmieren mit dem SharePoint REST-Dienst]((http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)).
## <a name="resource-endpoints-for-following-people-and-following-content-tasks"></a>Ressourcenendpunkte für das Folgen von Personen und Inhalten folgen
<a name="bk_Overview"> </a>


[Follow](#bk_Follow)  
[StopFollowing](#bk_StopFollowing)  
[IsFollowed](#bk_IsFollowed)  
[My](#bk_My)  
[My/FollowedDocumentsUri](#bk_MyFollowedDocumentsUri)  
[My/FollowedSitesUri](#bk_MyFollowedSitesUri)  
[My/Followed](#bk_Followed)  
[My/FollowedCount](#bk_FollowedCount)  
[My/Followers](#bk_Followers)  
[My/Suggestions](#bk_Suggestions)  
[GetMySuggestions](#bk_GetMySuggestions)  
[IsMyPeopleListPublic](#bk_IsMyPeopleListPublic)  
[AmIFollowedBy](#bk_AmIFollowedBy)  
[GetPeopleFollowedBy](#bk_GetPeopleFollowedBy)  
[GetFollowersFor](#bk_GetFollowersFor)  
   

## <a name="follow"></a>Folgen
<a name="bk_Follow"> </a>

Sorgt dafür, dass der aktuelle Benutzer beginnt, einem Benutzer, einem Dokument, einer Website oder einem Tag zu folgen.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **POST** `http://<siteCollection>/<site>/_api/social.following/follow`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _actor_
  
    
    
Typ: **SP.Social.SocialActorInfo**
  
    
    
Der Akteur, dem gefolgt werden soll.
  
    
    
 **Benutzer  _actor_ im URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=0,AccountName=@v,Id=null)?@v='domain\\user'
```

 **Benutzer _actor_ im Anforderungstext**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":0,
  "AccountName":"domain\\user",
  "Id":null
}
```

Wenn Sie ein anspruchsbasiertes Identitätsmodell verwenden, können Sie den Kontonamen mithilfe des Formats  `@v='i:0"%23".f|membership|user@domain.com'` in der Abfragezeichenfolge oder des Formats `"i:0#.f|membership|user@domain.com"` im Anforderungstext übergeben.
  
    
    
 **Dokument _actor_ im URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=1,ContentUri=@v,Id=null)?@v='http://server/Shared%20Documents/fileName.docx'
```

 **Dokument _actor_ im Anforderungstext**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":1,
  "ContentUri":"http://server/Shared%20Documents/fileName.docx",
  "Id":null
}
```

 **Website _actor_ im URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=2,ContentUri=@v,Id=null)?@v='http://server/site'
```

 **Website  _actor_ im Anforderungstext**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":2,
  "ContentUri":"http://siteCollection/site",
  "Id":null
}
```

 **Tag _actor_ im URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=3,TagGuid='19a4a484-c1dc-4bc5-8c93-bb96245ce928',Id=null)
```

 **Tag _actor_ im Anforderungstext**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":3,
  "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928",
  "Id":null
}
```

Sie benötigen die Tag-GUID, um zu beginnen, einem Tag zu folgen. Die GUID kann nicht mithilfe des REST-Diensts abgerufen werden, jedoch können Sie das .NET-Clientobjektmodell oder das JavaScript-Objektmodell verwenden. Weitere Informationen finden Sie unter  [So rufen die GUID eines Tags basierend auf dem Namen des Tags mithilfe des JavaScript-Objektmodells ab](follow-content-in-sharepoint.md#bk_getTagGuid).
  
    
    

### <a name="response"></a>Antwort

 **Follow**
  
    
    
Typ: **SP.Social.SocialFollowResult**
  
    
    
Der Status der Anforderung: 0 = OK; 1 = AlreadyFollowing; 2 = LimitReached oder 3 = InternalError.
  
    
    
Die folgende Antwort weist darauf hin, dass die Anforderung erfolgreich war.
  
    
    



```

{"d":{"Follow":0}}
```


## <a name="stopfollowing"></a>StopFollowing
<a name="bk_StopFollowing"> </a>

Sorgt dafür, dass der aktuelle Benutzer aufhört, einem Benutzer, einem Dokument, einer Website oder einem Tag zu folgen.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **POST** `http://<siteCollection>/<site>/_api/social.following/stopfollowing`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _actor_
  
    
    
Typ: **SP.Social.SocialActorInfo**
  
    
    
Der Akteur, dem nicht mehr gefolgt werden soll.
  
    
    
 **Benutzer _actor_ im URI**
  
    
    



```
http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=0,AccountName=@v,Id=null)?@v='domain\\user'
```

 **Benutzer _actor_ im Anforderungstext**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":0,
  "AccountName":"domain\\user",
  "Id":null
}
```

Wenn Sie ein anspruchsbasiertes Identitätsmodell verwenden, können Sie den Kontonamen mithilfe des Formats  `@v='i:0"%23".f|membership|user@domain.com'` in der Abfragezeichenfolge oder des Formats `"i:0#.f|membership|user@domain.com"` im Anforderungstext übergeben.
  
    
    
 **Dokument _actor_ im URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=1,ContentUri=@v,Id=null)?@v='http://server/Shared%20Documents/fileName.docx'
```

 **Dokument _actor_ im Anforderungstext**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":1,
  "ContentUri":"http://server/Shared%20Documents/fileName.docx",
  "Id":null
}
```

 **Website _actor_ im URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=2,ContentUri=@v,Id=null)?@v='http://server/site'
```

 **Website  _actor_ im Anforderungstext**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":2,
  "ContentUri":"http://siteCollection/site",
  "Id":null
}
```

 **Tag _actor_ im URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=3,TagGuid='19a4a484-c1dc-4bc5-8c93-bb96245ce928',Id=null)
```

 **Tag _actor_ im Anforderungstext**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":3,
  "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928",
  "Id":null
}
```

Sie benötigen die Tag-GUID, um zu beginnen, einem Tag zu folgen. Die GUID kann nicht mithilfe des REST-Diensts abgerufen werden, jedoch können Sie das .NET-Clientobjektmodell oder das JavaScript-Objektmodell verwenden. Weitere Informationen finden Sie unter  [So rufen die GUID eines Tags basierend auf dem Namen des Tags mithilfe des JavaScript-Objektmodells ab](follow-content-in-sharepoint.md#bk_getTagGuid).
  
    
    

### <a name="response"></a>Antwort

Keine
  
    
    

```

{"d":{"StopFollowing":null}}
```


## <a name="isfollowed"></a>IsFollowed
<a name="bk_IsFollowed"> </a>

Gibt an, ob der aktuelle Benutzer einem angegebenen Benutzer, einem Dokument, einer Website oder einem Tag folgt.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **POST** `http://<siteCollection>/<site>/_api/social.following/isfollowed`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _actor_
  
    
    
Typ: **SP.Social.SocialActorInfo**
  
    
    
Der Akteur, für den der folgende Status gefunden werden soll.
  
    
    
 **Benutzer _actor_ im URI**
  
    
    



```
http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=0,AccountName=@v,Id=null)?@v='domain\\user'
```

 **Benutzer _actor_ im Anforderungstext**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":0,
  "AccountName":"domain\\user",
  "Id":null
}
```

Wenn Sie ein anspruchsbasiertes Identitätsmodell verwenden, können Sie den Kontonamen mithilfe des Formats  `@v='i:0"%23".f|membership|user@domain.com'` in der Abfragezeichenfolge oder des Formats `"i:0#.f|membership|user@domain.com"` im Anforderungstext übergeben.
  
    
    
 **Dokument _actor_ im URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=1,ContentUri=@v,Id=null)?@v='https://domain.sharepoint.com/Shared%20Documents/fileName.docx'
```

 **Dokument _actor_ im Anforderungstext**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":1,
  "ContentUri":"http://server/Shared%20Documents/fileName.docx",
  "Id":null
}
```

 **Website _actor_ im URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=2,ContentUri=@v,Id=null)?@v='http://domain.sharepoint.com'
```

 **Website  _actor_ im Anforderungstext**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":2,
  "ContentUri":"http://siteCollection/site",
  "Id":null
}
```

 **Tag _actor_ im URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=3,TagGuid='19a4a484-c1dc-4bc5-8c93-bb96245ce928',Id=null)
```

 **Tag _actor_ im Anforderungstext**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":3,
  "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928",
  "Id":null
}
```

Sie benötigen die Tag-GUID, um zu beginnen, einem Tag zu folgen. Die GUID kann nicht mithilfe des REST-Diensts abgerufen werden, jedoch können Sie das .NET-Clientobjektmodell oder das JavaScript-Objektmodell verwenden. Weitere Informationen finden Sie unter  [So rufen die GUID eines Tags basierend auf dem Namen des Tags mithilfe des JavaScript-Objektmodells ab](follow-content-in-sharepoint.md#bk_getTagGuid).
  
    
    

### <a name="response"></a>Antwort

 **IsFollowed**
  
    
    
Typ: **bool**
  
    
    
 **true**, wenn der Benutzer dem Akteur folgt, andernfalls **false**.
  
    
    
Die folgende Antwort weist darauf hin, dass der Benutzer dem angegebenen Akteur nicht folgt.
  
    
    



```

{"d":{"IsFollowed":false}}
```


## <a name="my"></a>My
<a name="bk_My"> </a>

Ruft Informationen über die **SocialRestFollowingManager**-Instanz sowie Informationen über den aktuellen Benutzer ab.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/social.following/my`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

Keine
  
    
    

### <a name="response"></a>Antwort

Typ: **SP.Social.SocialRestFollowingManager**
  
    
    
Information über die **SocialRestFollowingManager**-Instanz und die Eigenschaften **MyFollowedDocumentsUri**, **MyFollowedSitesUri** und **SocialActor** für den aktuellen Benutzer.
  
    
    
Die folgende Antwort stellt die **SocialRestFollowingManager**-Instanz für den aktuellen Benutzer dar.
  
    
    



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


## <a name="myfolloweddocumentsuri"></a>My/FollowedDocumentsUri
<a name="bk_MyFollowedDocumentsUri"> </a>

Ruft den URI für die Seite **Dokumente, denen ich folge** für den aktuellen Benutzer ab.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/social.following/my/followeddocumentsuri`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

Keine
  
    
    

### <a name="response"></a>Antwort

 **FollowedDocumentsUri**
  
    
    
Typ: **String**
  
    
    
Der URI zur Seite **Dokumente, denen ich folge** für den aktuellen Benutzer.
  
    
    
Die folgende Antwort stellt die **FollowedDocumentsUri**-Instanz für den aktuellen Benutzer dar.
  
    
    



```

{"d":{"FollowedDocumentsUri":"https://somecompany-my.sharepoint.com/personal/someone_somecompany_onmicrosoft_com/Social/FollowedContent.aspx"}}
```


## <a name="myfollowedsitesuri"></a>My/FollowedSitesUri
<a name="bk_MyFollowedSitesUri"> </a>

Ruft den URI für die Seite **Website, denen ich folge** für den aktuellen Benutzer ab.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/social.following/my/followedsitesuri`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

Keine
  
    
    

### <a name="response"></a>Antwort

 **FollowedSitesUri**
  
    
    
Typ: **String**
  
    
    
Der URI zur Seite **Websites, denen ich folge** für den aktuellen Benutzer.
  
    
    
Die folgende Antwort stellt die **FollowedSitesUri**-Instanz für den aktuellen Benutzer dar.
  
    
    



```
{"d":{"FollowedSitesUri":"https://somecompany-my.sharepoint.com/personal/someone_somecompany_onmicrosoft_com/Social/Sites.aspx"}}
```


## <a name="myfollowed"></a>My/Followed
<a name="bk_Followed"> </a>

Ruft Benutzer, Dokumente, Websites und Tags ab, denen der aktuelle Benutzer folgt.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/social.following/my/followed(types=15)`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _types_
  
    
    
Typ: **Int32**
  
    
    
Die einzuschließenden Akteurtypen. Benutzer = 1, Dokumente = 2, Websites = 4, Tags = 8. Bitweise Kombinationen sind zulässig.
  
    
    

### <a name="response"></a>Antwort

 **Followed**
  
    
    
Typ: Array von **SP.Social.SocialActor**
  
    
    
Die Benutzer, Dokumente, Websites und Tags, denen der aktuelle Benutzer folgt.
  
    
    
Die folgende Antwort stellt ein Dokument, eine Website und ein Tag dar. Der Parameter  _types_ in der Anforderung gibt die Typen der einzuschließenden Akteure an.
  
    
    



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


## <a name="myfollowedcount"></a>My/FollowedCount
<a name="bk_FollowedCount"> </a>

Ruft die Anzahl der Benutzer, Dokumente, Websites und Tags ab, denen der aktuelle Benutzer folgt.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/social.following/my/followedcount(types=15)`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _types_
  
    
    
Typ: **Int32**
  
    
    
Die einzuschließenden Akteurtypen. Benutzer = 1, Dokumente = 2, Websites = 4, Tags = 8. Bitweise Kombinationen sind zulässig.
  
    
    

### <a name="response"></a>Antwort

 **FollowedCount**
  
    
    
Typ: **Int32**
  
    
    
Die Anzahl der Benutzer, Dokumente, Websites und Tags, denen der aktuelle Benutzer folgt.
  
    
    
Die folgende Antwort weist darauf hin, dass der aktuelle Benutzer 3 Akteuren des angegebenen Typs folgt. Der Parameter  _types_ in der Anforderung gibt die Typen einzuschließenden Akteure an.
  
    
    



```

{"d":{"FollowedCount":3}}
```


## <a name="myfollowers"></a>My/Followers
<a name="bk_Followers"> </a>

Ruft die Benutzer ab, die dem aktuellen Benutzer folgen.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/social.following/my/followers`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

Keine
  
    
    

### <a name="response"></a>Antwort

 **Followers**
  
    
    
Typ: Array von **SP.Social.SocialActor**
  
    
    

  
    
    
Die folgende Antwort stellt einen Benutzer dar, der dem aktuellen Benutzer folgt.
  
    
    



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


## <a name="mysuggestions"></a>My/Suggestions
<a name="bk_Suggestions"> </a>

Ruft die Benutzer ab, denen der aktuelle Benutzer möglicherweise folgen möchte.
  
> [!NOTE]
> Die Funktion für Personenvorschläge hängt von den Folgeaktivitäten des Benutzers, Suchdurchforstungen und Suchanalysen ab. Siehe [Funktionsweise von Personenvorschlägen auf SharePoint Online](follow-people-in-sharepoint.md#bk_PeopleSuggestions). 
  
    
    


### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/social.following/my/suggestions`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

Keine
  
    
    

### <a name="response"></a>Antwort

 **Suggestions**
  
    
    
Typ: Array von **SP.Social.SocialActor**
  
    
    
Benutzer, dem der aktuelle Benutzer möglicherweise folgen möchte.
  
    
    

## <a name="getmysuggestions"></a>GetMySuggestions
<a name="bk_GetMySuggestions"> </a>

Ruft die Benutzer ab, denen der aktuelle Benutzer möglicherweise folgen möchte.
  
> [!NOTE]
> Die Funktion für Personenvorschläge hängt von den Folgeaktivitäten des Benutzers, Suchdurchforstungen und Suchanalysen ab. Siehe [Funktionsweise von Personenvorschlägen auf SharePoint Online](follow-people-in-sharepoint.md#bk_PeopleSuggestions). 
  
    
    


### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getmysuggestions`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

Keine
  
    
    

### <a name="response"></a>Antwort

 **Suggestions**
  
    
    
Typ: Liste von **SP.UserProfiles.PersonProperties**
  
    
    
Benutzer, dem der aktuelle Benutzer möglicherweise folgen möchte.
  
    
    

## <a name="ismypeoplelistpublic"></a>IsMyPeopleListPublic
<a name="bk_IsMyPeopleListPublic"> </a>

Findet heraus, ob die Liste **Personen, denen ich folge** für den aktuellen Benutzer öffentlich ist.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/ismypeoplelistpublic`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

Keine
  
    
    

### <a name="response"></a>Antwort

 **IsMyPeopleListPublic**
  
    
    
Typ: **bool**
  
    
    
 **true**, wenn die Personenliste des aktuellen Benutzer öffentlich ist, andernfalls **false**.
  
    
    
Die folgende Antwort weist darauf hin, dass die Personenliste des aktuellen Benutzers öffentlich ist.
  
    
    



```

{"d":{"IsMyPeopleListPublic":true}}
```


## <a name="amifollowedby"></a>AmIFollowedBy
<a name="bk_AmIFollowedBy"> </a>

Findet heraus, ob ein bestimmter Benutzer dem aktuellen Benutzer folgt.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/amifollowedby(accountName=@v)?@v='domain\\user'`
  
    
    
 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/amifollowedby(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _accountName_
  
    
    
Typ: **String**
  
    
    
Der Kontoname des Zielbenutzers.
  
    
    

### <a name="response"></a>Antwort

 **AmIFollowedBy**
  
    
    
Typ: **bool**
  
    
    
 **true**, wenn der angegebene Benutzer dem aktuellen Benutzer folgt, andernfalls **false**.
  
    
    
Die folgende Antwort weist darauf hin, dass der angegebene Benutzer dem aktuellen Benutzer nicht folgt.
  
    
    



```
{"d":{"AmIFollowedBy":false}}
```


## <a name="getpeoplefollowedby"></a>GetPeopleFollowedBy
<a name="bk_GetPeopleFollowedBy"> </a>

Ruft die Benutzer ab, denen von einem angegebenen Benutzer gefolgt wird.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getpeoplefollowedby(accountName=@v)?@v='domain\\user'`
  
    
    
 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getpeoplefollowedby(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _accountName_
  
    
    
Typ: **String**
  
    
    
Der Kontoname des Zielbenutzers.
  
    
    

### <a name="response"></a>Antwort

 **GetPeopleFollowedBy**
  
    
    
Typ: Liste von **SP.UserProfiles.PersonProperties**
  
    
    
Die Benutzer, denen vom angegebenen Benutzer gefolgt wird.
  
    
    
Die folgende Antwort stellt zwei Benutzer dar, die dem angegebenen Benutzer folgen.
  
    
    



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


## <a name="getfollowersfor"></a>GetFollowersFor
<a name="bk_GetFollowersFor"> </a>

Ruft die Benutzer ab, die einem angegebenen Benutzer folgen.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getfollowersfor(accountName=@v)?@v='domain\\user'`
  
    
    
 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getfollowersfor(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _accountName_
  
    
    
Typ: **String**
  
    
    
Der Kontoname des Zielbenutzers.
  
    
    

### <a name="response"></a>Antwort

 **GetFollowersFor**
  
    
    
Typ: Liste von **SP.UserProfiles.PersonProperties**
  
    
    
Die Benutzer, die dem angegebenen Benutzer folgen.
  
    
    
Die folgende Antwort stellt einen Benutzer dar, der dem angegebenen Benutzer folgt.
  
    
    



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


## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Vorgehensweise: führen Sie Dokumente, Websites und Tags mithilfe des REST-Diensts in SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)
    
  
-  [REST-API-Referenz für sozialen Feed für SharePoint](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [SharePoint User Profiles JavaScript Reference (sp.userprofiles.js)]((http://msdn.microsoft.com/library/80cf5436-6aa2-6f11-a782-66a04f6e2fb0%28Office.15%29.aspx))
    
  
-  [Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
