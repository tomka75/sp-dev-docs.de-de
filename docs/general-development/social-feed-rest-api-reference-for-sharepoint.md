---
title: "REST-API-Referenz für sozialen Feed für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f1cb914f-1e91-4e23-bf53-d2ab323eac13
ms.openlocfilehash: 90b0bfe6f81335b27300f9ef5af332177cd7e8c1
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="social-feed-rest-api-reference-for-sharepoint"></a>REST-API-Referenz für sozialen Feed für SharePoint
Suchen Sie SharePoint-REST-Endpunkte, um mithilfe der **SocialRestFeedManager**-Ressource Beiträge in sozialen Feeds zu lesen und zu verfassen. Sie können den REST-Dienst (Representational State Transfer) in SharePoint für die gleichen Dinge verwenden, die Sie auch mit den .NET-Clientobjektmodellen und dem JavaScript-Objektmodell ausführen können. Der REST-Dienst macht Ressourcen verfügbar, die SharePoint-Objekten, -Eigenschaften und -Methoden entsprechen. Um den REST-Dienst zu verwenden, erstellen und senden Sie HTTP- **GET**- und **POST**-Anforderungen an die Ressourcenendpunkte, die den Aufgaben entsprechen, die Sie ausführen möchten.
  
    
    

Die Endpunkt-URIs für die meisten Feedaufgaben beginnen mit der **SocialRestFeedManager**-Ressource ( `social.feed`), gefolgt von der  `my`-Ressource oder der  `post`-Ressource:
- Die  `my`-Ressource stellt den aktuellen Benutzer dar. Wenn diese inline im Endpunkt-URI verwendet wird, wird der Kontext der Anforderung auf den aktuellen Benutzer festgelegt.  `http://contoso.com/_api/social.feed/my/news` ruft beispielsweise den Newsfeed für den aktuellen Benutzer ab.
    
  
- Die  `post`-Ressource stellt einen bestimmten Thread oder Beitrag dar. Wenn diese inline im Endpunkt-URI verwendet wird, wird der Kontext der Anforderung auf den angegeben Thread oder Beitrag festgelegt.  `http://contoso.com/_api/social.feed/post/lock` sperrt beispielsweise den angegebenen Thread.
    
  
Wenn der Ressourcenendpunkt einen Parameter verwendet, werden die Parametermetadaten im URI oder im Anforderungstext angegeben. Der REST-Dienst gibt standardmäßig Antworten zurück, die im Atom-Protokoll formatiert sind, Sie können mithilfe von HTTP- **Accept**-Headern jedoch das JSON-Format anfordern. Unter  [Beispiel-REST-Anforderungen für den Feedaufgaben](social-feed-rest-api-reference-for-sharepoint.md#bk_exampleRequests) finden Sie Beispiele von vollständigen Anforderungen.
## <a name="resource-endpoints-for-feed-tasks"></a>Ressourcenendpunkte für Feedaufgaben
<a name="bk_Overview"> </a>


|**Endpunkt**|**Beschreibung**|
|:-----|:-----|
| [My](social-feed-rest-api-reference-for-sharepoint.md#bk_my)|Ruft Informationen zu dem aktuellen Benutzer ab.|
| [My/Feed/Post](social-feed-rest-api-reference-for-sharepoint.md#bk_myFeedPost)|Erstellt einen Stammbeitrag in dem Feed des aktuellen Benutzers.|
| [My/Feed](social-feed-rest-api-reference-for-sharepoint.md#bk_myFeed)|Ruft den Feed der Aktivitäten des aktuellen Benutzers ab.|
| [My/News](social-feed-rest-api-reference-for-sharepoint.md#bk_myNews)|Ruft den Feed der Aktivitäten des aktuellen Benutzers und von Personen und Inhalten ab, denen der Benutzer folgt.|
| [My/TimelineFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_myTimelineFeed)|Ruft den Feed der Aktivitäten des aktuellen Benutzers und von Personen und Inhalten ab, denen der Benutzer folgt, sortiert nach dem Erstellungsdatum.|
| [My/Likes](social-feed-rest-api-reference-for-sharepoint.md#bk_myLikes)|Ruft den Feed von Beiträgen ab, die dem aktuellen Benutzer gefallen.|
| [My/MentionFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_myMentionFeed)|Ruft den Feed von Beiträgen ab, in denen der aktuelle Benutzer erwähnt wird.|
| [My/MentionFeed/ClearUnreadMentionCount](social-feed-rest-api-reference-for-sharepoint.md#bk_myMentionFeedClearUnreadMentionCount)|Ruft den Feed von Beiträgen ab, in denen der aktuelle Benutzer erwähnt wird, und löscht die Anzahl ungelesener Erwähnungen.|
| [My/UnreadMentionCount](social-feed-rest-api-reference-for-sharepoint.md#bk_myUnreadMentionCount)|Ruft die Anzahl der ungelesenen Erwähnungen für den aktuellen Benutzer ab.|
| [Akteur](social-feed-rest-api-reference-for-sharepoint.md#bk_actor)|Ruft Informationen zu dem angegebenen und dem aktuellen Benutzer ab.|
| [Actor/Feed](social-feed-rest-api-reference-for-sharepoint.md#bk_actorFeed)|Ruft den Feed der Aktivitäten des angegebenen Benutzers ab.|
| [Actor/Feed/Post](social-feed-rest-api-reference-for-sharepoint.md#bk_actorFeedPost)|Erstellt einen Stammbeitrag in dem angegebenen Websitefeed.|
| [Post](social-feed-rest-api-reference-for-sharepoint.md#bk_post)|Ruft einen vollständigen Thread ab, der den angegebenen Beitrag enthält.|
| [Post/Reply](social-feed-rest-api-reference-for-sharepoint.md#bk_postReply)|Postet eine Antwort auf den angegebenen Beitrag.|
| [Post/Delete](social-feed-rest-api-reference-for-sharepoint.md#bk_postDelete)|Löscht den angegebenen Beitrag.|
| [Post/Like](social-feed-rest-api-reference-for-sharepoint.md#bk_postLike)|Damit wird angegeben, dass der angegebene Beitrag dem aktuellen Benutzer gefällt.|
| [Post/Unlike](social-feed-rest-api-reference-for-sharepoint.md#bk_postUnlike)|Entfernt den aktuellen Benutzer aus der Liste der Benutzer, denen der angegebene Beitrag gefällt.|
| [Post/Likers](social-feed-rest-api-reference-for-sharepoint.md#bk_postLikers)|Ruft die Benutzer ab, denen der angegebene Beitrag gefällt.|
| [Post/Lock](social-feed-rest-api-reference-for-sharepoint.md#bk_postLock)|Sperrt den angegebenen Thread.|
| [Post/Unlock](social-feed-rest-api-reference-for-sharepoint.md#bk_postUnlock)|Entsperrt den angegebenen Thread.|
   

> **Hinweis:** Die folgenden Feed-bezogenen REST-Ressourcen verwenden für die Erstellung des Endpunkt-URI dasselbe Muster wie die übrigen SharePoint-REST-APIs. Im Fall von **CreateImageAttachment** senden Sie eine Anforderung des Typs **POST** an `http://<siteCollection>/<site>/_api/SP.Social.SocialFeedManager/CreateImageAttachment`. Im Fall von **GetPreview** senden Sie eine Anforderung des Typs **POST** an `http://<siteCollection>/<site>/_api/SP.Social.SocialFeedManager/GetPreview`. Im Fall von **SuppressThreadNotifications** senden Sie eine Anforderung des Typs **POST** an `http://<siteCollection>/<site>/_api/SP.Social.SocialFeedManager/SuppressThreadNotifications`.
  
    
    


## <a name="my"></a>My
<a name="bk_my"> </a>

Ruft Informationen zu dem aktuellen Benutzer ab.
  
    
    
Der **my**-Endpunkt legt den aktuellen Benutzer als Kontext für alle nachfolgenden Ressourcen in dem URI fest.  `http://contoso.com/_api/social.feed/my/news` ruft z. B. den Newsfeed für den aktuellen Benutzer ab.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/social.feed/my`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

Keine
  
    
    

### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestActor](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestActor)
  
    
    
Informationen über den aktuellen Benutzer.
  
    
    
Sie können **SocialRestActor**-Eigenschaften einzeln im URI aufrufen,  `http://<siteCollection>/<site>/_api/social.feed/my/me` ruft z. B. nur die **Me**-Eigenschaft ab.
  
    
    
In den folgenden Antwortbeispielen sind Informationen zu dem aktuellen Benutzer dargestellt.
  
    
    



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


## <a name="myfeedpost"></a>My/Feed/Post
<a name="bk_myFeedPost"> </a>

Erstellt einen Stammbeitrag in dem Feed des aktuellen Benutzers.
  
    
    
Sie können nur im Kontext des aktuellen Benutzers Beiträge posten. Sie können keinen Stammbeitrag im Feed eines anderen Benutzers erstellen, Sie können aber auf den Beitrag eines anderen Benutzers antworten. Weitere Informationen finden Sie unter  [Post/Reply](social-feed-rest-api-reference-for-sharepoint.md#bk_postReply).
  
    
    

> **Hinweis:** Verwechseln Sie diese Ressource des Typs `Post` nicht mit der Ressource des Typs `Post`, die einen bestimmten Thread oder Beitrag darstellt.
  
    
    


### <a name="endpoint-uri-structure"></a>Struktur des Endpunkt-URI

 **POST** `http://<siteCollection>/<site>/_api/social.feed/my/feed/post`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _restCreationData_
  
    
    
Typ:  [SP.Social.SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData)
  
    
    
Eine **null**-ID und die Eigenschaften des neuen Beitrags, wie im folgenden Beispiel dargestellt.
  
    
    

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


### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)
  
    
    
Ein Thread, der den neuen Stammbeitrag enthält.
  
    
    
Im folgenden Antwortbeispiel ist der Thread dargestellt, der den neuen Stammbeitrag enthält.
  
    
    



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


## <a name="myfeed"></a>My/Feed
<a name="bk_myFeed"> </a>

Ruft den Feed der Aktivitäten des aktuellen Benutzers ab ( **Personal**-Feedtyp).
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/social.feed/my/feed`
  
    
    
 **GET** `http://<siteCollection>/<site>/_api/social.feed/my/feed(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _feedOptions_ (optional)
  
    
    
Typ:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)
  
    
    
Die maximale Anzahl von Threads, Datums-/Uhrzeitbereich und Sortierreihenfolge. Sie können optional beliebige Kombinationen dieser Eigenschaften angeben, Sie können beispielsweise nur die **MaxThreadCount**-Eigenschaft angeben.
  
    
    
Sie können einen **@**-Alias verwenden, um Sonderzeichen zu übergeben.  `<siteUri>/_api/social.feed/my/feed(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` verwendet z. B. den **@v**-Alias, um das Zeichen **:** zu senden.
  
    
    

### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)
  
    
    
Der persönliche Feed des aktuellen Benutzers.
  
    
    
Im folgenden Antwortbeispiel ist der persönliche Feed des aktuellen Benutzers dargestellt.
  
    
    



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


## <a name="mynews"></a>My/News
<a name="bk_myNews"> </a>

Ruft den Feed der Aktivitäten des aktuellen Benutzers und von Personen und Inhalten ab, denen der Benutzer folgt, sortiert nach dem Datum der letzten Änderung. **News**-Feedtyp).
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/social.feed/my/news`
  
    
    
 **GET** `http://<siteCollection>/<site>/_api/social.feed/my/news(MaxThreadCount=10,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _feedOptions_ (optional)
  
    
    
Typ:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)
  
    
    
Die maximale Anzahl von Threads, Datums-/Uhrzeitbereich und Sortierreihenfolge. Sie können optional beliebige Kombinationen dieser Eigenschaften angeben, Sie können beispielsweise nur die **MaxThreadCount**-Eigenschaft angeben.
  
    
    
Sie können einen **@**-Alias verwenden, um Sonderzeichen zu übergeben.  `<siteUri>/_api/social.feed/my/News(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` verwendet z. B. den **@v**-Alias, um das Zeichen **:** zu senden.
  
    
    

### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)
  
    
    
Der Newsfeed des aktuellen Benutzers.
  
    
    
Im folgenden Antwortbeispiel ist der Newsfeed des aktuellen Benutzers dargestellt.
  
    
    



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


## <a name="mytimelinefeed"></a>My/TimelineFeed
<a name="bk_myTimelineFeed"> </a>

Ruft den Feed der Aktivitäten des aktuellen Benutzers und von Personen und Inhalten ab, denen der Benutzer folgt, sortiert nach dem Erstellungsdatum ( **Timeline**-Feedtyp).
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/social.feed/my/timelinefeed`
  
    
    
 **GET** `http://<siteCollection>/<site>/_api/social.feed/my/timelinefeed(MaxThreadCount=10,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _feedOptions_ (optional)
  
    
    
Typ:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)
  
    
    
Die maximale Anzahl von Threads, Datums-/Uhrzeitbereich und Sortierreihenfolge. Sie können optional beliebige Kombinationen dieser Eigenschaften angeben, Sie können beispielsweise nur die **MaxThreadCount**-Eigenschaft angeben.
  
    
    
Sie können einen **@**-Alias verwenden, um Sonderzeichen zu übergeben.  `<siteUri>/_api/social.feed/my/timelinefeed(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` verwendet z. B. den **@v**-Alias, um das Zeichen **:** zu senden.
  
    
    

### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)
  
    
    
Der Zeitachsenfeed des aktuellen Benutzers.
  
    
    
Im folgenden Antwortbeispiel ist der Zeitachsenfeed des aktuellen Benutzers, sortiert nach Erstellungsdatum, dargestellt.
  
    
    



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


## <a name="mylikes"></a>My/Likes
<a name="bk_myLikes"> </a>

Ruft den Feed von Mikroblogbeiträgen ab, die dem aktuellen Benutzer gefallen, dargestellt durch den Threadtyp **LikeReference**. Weitere Informationen finden Sie unter [Verweisthreads und Digestthreads in sozialen SharePoint-Feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).
  
    
    

### <a name="endpoint-uri-structure"></a>Struktur des Endpunkt-URI

 **GET** `http://<siteCollection>/<site>/_api/social.feed/my/likes`
  
    
    
 **GET** `http://<siteCollection>/<site>/_api/social.feed/my/likes(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _feedOptions_ (optional)
  
    
    
Typ:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)
  
    
    
Die maximale Anzahl von Threads, Datums-/Uhrzeitbereich und Sortierreihenfolge. Sie können optional beliebige Kombinationen dieser Eigenschaften angeben, Sie können beispielsweise nur die **MaxThreadCount**-Eigenschaft angeben.
  
    
    
Sie können optional Abrufoptionen in der Abfragezeichenfolge angeben. Sie können einen **@**-Alias verwenden, um Sonderzeichen zu übergeben.  `<siteUri>/_api/social.feed/my/likes(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` verwendet z. B. den **@v**-Alias, um das Zeichen **:** zu senden.
  
    
    

### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)
  
    
    
Ein Feed, der Beiträge enthält, die dem aktuellen Benutzer gefallen.
  
    
    
Im folgenden Antwortbeispiel ist ein Verweis auf einen Beitrag dargestellt, der dem aktuellen Benutzer gefällt. Der Thread ist ein **LikeReference**-Threadtyp (Wert = **1**), dessen **PostReference**-Eigenschaft auf den tatsächlichen Beitrag verweist.
  
    
    



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


## <a name="mymentionfeed"></a>My/MentionFeed
<a name="bk_myMentionFeed"> </a>

Ruft den Feed von Mikroblogbeiträgen ab, in denen der aktuelle Benutzer erwähnt wird, dargestellt durch den Threadtyp **MentionReference**. Weitere Informationen finden Sie unter [Verweisthreads und Digestthreads in sozialen SharePoint-Feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).
  
    
    

### <a name="endpoint-uri-structure"></a>Struktur des Endpunkt-URI

 **GET** `http://<siteCollection>/<site>/_api/social.feed/my/mentionfeed`
  
    
    
 **GET** `http://<siteCollection>/<site>/_api/social.feed/my/mentionfeed(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _feedOptions_ (optional)
  
    
    
Typ:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)
  
    
    
Die maximale Anzahl von Threads, Datums-/Uhrzeitbereich und Sortierreihenfolge. Sie können optional beliebige Kombinationen dieser Eigenschaften angeben, Sie können beispielsweise nur die **MaxThreadCount**-Eigenschaft angeben.
  
    
    
Sie können einen **@**-Alias verwenden, um Sonderzeichen zu übergeben.  `<siteUri>/_api/social.feed/my/likes(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` verwendet z. B. den **@v**-Alias, um das Zeichen **:** zu senden.
  
    
    

### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)
  
    
    
Ein Feed, der Beiträge enthält, in denen der aktuelle Benutzer erwähnt wird.
  
    
    
Im folgenden Antwortbeispiel ist ein Thread dargestellt, in dem der aktuelle Benutzer erwähnt wird. Der Thread ist ein **MentionReference**-Threadtyp (Wert = **3**), dessen **PostReference**-Eigenschaft auf den tatsächlichen Beitrag verweist.
  
    
    



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


## <a name="mymentionfeedclearunreadmentioncount"></a>My/MentionFeed/ClearUnreadMentionCount
<a name="bk_myMentionFeedClearUnreadMentionCount"> </a>

Ruft den Feed von Mikroblogbeiträgen ab, in denen der aktuelle Benutzer erwähnt wird, dargestellt durch den Threadtyp **MentionReference**. Setzt außerdem die Anzahl ungelesener Erwähnungen des Benutzers auf 0. Weitere Informationen finden Sie unter [Verweisthreads und Digestthreads in sozialen SharePoint-Feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).
  
    
    

### <a name="endpoint-uri-structure"></a>Struktur des Endpunkt-URI

 **POST** `http://<siteCollection>/<site>/_api/social.feed/my/mentionfeed/clearunreadmentioncount`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _feedOptions_
  
    
    
Typ:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)
  
    
    
Dieser Parameter muss als leere Zeichenfolge im **data**-Attribut des Anforderungstexts gesendet werden, wie im folgenden Beispiel dargestellt.
  
    
    

```

'feedOptions': {
  '__metadata': {
    'type': 'SP.Social.SocialFeedOptions'
  }, 
}
```


### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)
  
    
    
Der Erwähnungsfeed des aktuellen Benutzers.
  
    
    
Im folgenden Antwortbeispiel ist der Erwähnungsfeed des aktuellen Benutzers dargestellt. Der Thread ist ein **MentionReference**-Threadtyp (Wert = **3**), dessen **PostReference**-Eigenschaft auf den tatsächlichen Beitrag verweist. Die Anzahl ungelesener Erwähnungen wird gelöscht, nachdem der Feed abgerufen wurde.
  
    
    



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


## <a name="myunreadmentioncount"></a>My/UnreadMentionCount
<a name="bk_myUnreadMentionCount"> </a>

Ruft die Anzahl der ungelesenen Erwähnungen für den aktuellen Benutzer ab.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/social.feed/my/unreadmentioncount`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

Keine
  
    
    

### <a name="response"></a>Antwort

Typ: **Int32**
  
    
    
Die Anzahl ungelesener Erwähnungen für den aktuellen Benutzer.
  
    
    
Im folgenden Antwortbeispiel ist die Anzahl 1 für ungelesene Erwähnungen dargestellt.
  
    
    



```

{"d":{"UnreadMentionCount":1}}
```


## <a name="actor"></a>Akteur
<a name="bk_actor"> </a>

Ruft Informationen zu dem angegebenen Benutzer und dem aktuellen Benutzer ab.
  
    
    

> **Hinweis:** Der Endpunkt `actor` legt den angegebenen Benutzer- oder Websitefeed als Kontext für alle zukünftigen Ressourcen in dem URI fest. So ruft beispielsweise `http://contoso.com/_api/social.feed/actor(item='domain\\user')/feed` den persönlichen Feed des angegebenen Benutzers ab und `http://contoso.com/_api/social.feed/actor(item=@v)/feed?@v='http://<server>/<teamSite>/newsfeed.aspx'` den Websitefeed der angegebenen Teamwebsite.
  
    
    


### <a name="endpoint-uri-structure"></a>Struktur des Endpunkt-URI

 **GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')`
  
    
    
 **GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)?@v='i:0"%23".f|membership|user@domain.com'`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _item_
  
    
    
Typ: **String**
  
    
    
Der Kontoname des angegebenen Benutzers.
  
    
    
Sie senden den  _item_-Parameter in der Abfragezeichenfolge. Sie können einen **@**-Alias verwenden, um Sonderzeichen zu übergeben.  `<siteUri>/_api/social.feed/actor(item=@v)?@v='i:0"%23".f|membership|user@domain.com'` verwendet z. B. den **@v**-Alias und die **"%23"**-Codierung, um das Zeichen **#** zu senden.
  
    
    

### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestActor](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestActor)
  
    
    
Informationen zu dem angegebenen Benutzer und dem aktuellen Benutzer.
  
    
    
Sie können **SocialRestActor**-Eigenschaften einzeln im URI aufrufen,  `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')/followableitem` ruft z. B. nur die **FollowableItem**-Eigenschaft für den angegebenen Akteur ab.
  
    
    
Im folgenden Antwortbeispiel sind Informationen zu dem angegebenen und dem aktuellen Benutzer dargestellt.
  
    
    



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


## <a name="actorfeed"></a>Actor/Feed
<a name="bk_actorFeed"> </a>

Ruft den Feed der Aktivitäten des angegebenen Benutzers ab ( **Personal**-Feedtyp) oder ruft den angegebenen Websitefeed ab.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')/feed`
  
    
    
 **GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)/feed?@v='i:0"%23".f|membership|user@domain.com'`
  
    
    
 **GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')/feed(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`
  
    
    
 **GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)/feed?@v='http://<teamSiteUri>/newsfeed.aspx'`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _feedOptions_ (optional)
  
    
    
Typ:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)
  
    
    
Die maximale Anzahl von Threads, Datums-/Uhrzeitbereich und Sortierreihenfolge. Sie können optional beliebige Kombinationen dieser Eigenschaften angeben, Sie können beispielsweise nur die **MaxThreadCount**-Eigenschaft angeben.
  
    
    
Sie können einen **@**-Alias verwenden, um Sonderzeichen zu übergeben.  `<siteUri>/_api/social.feed/actor(item=@v)/feed(NewerThan=@x)?@v='i:0"%23".f|membership|user@domain.com'&amp;@x=datetime'2013-01-01T08:00'` verwendet z. B. den **@v**-Alias und die **"%23"**-Codierung, um das Zeichen **#** zu senden, und den **@x**-Alias, um das Zeichen **:** zu senden.
  
    
    

### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)
  
    
    
Der persönliche Feed des angegebenen Benutzers oder der Websitefeed an dem angegebenen URI.
  
    
    
Im folgenden Antwortbeispiel ist der persönliche Feed des angegebenen Benutzers dargestellt.
  
    
    



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


## <a name="actorfeedpost"></a>Actor/Feed/Post
<a name="bk_actorFeedPost"> </a>

Erstellt einen Stammbeitrag in dem angegebenen Websitefeed.
  
    
    
Sie können nur im Kontext des aktuellen Benutzers Beiträge posten. Sie können keinen Stammbeitrag im Feed eines anderen Benutzers erstellen, Sie können aber auf den Beitrag eines anderen Benutzers antworten. Weitere Informationen finden Sie unter  [Post/Reply](social-feed-rest-api-reference-for-sharepoint.md#bk_postReply).
  
    
    

> **Hinweis:** Verwechseln Sie diese Ressource des Typs `Post` nicht mit der Ressource des Typs `Post`, die einen bestimmten Thread oder Beitrag darstellt.
  
    
    


### <a name="endpoint-uri-structure"></a>Struktur des Endpunkt-URI

 **POST** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)/feed/post?@v='http://<siteCollection>/<teamSite>/newsfeed.aspx'`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _restCreationData_
  
    
    
Typ:  [SP.Social.SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData)
  
    
    
Eine **null**-ID und die Eigenschaften des neuen Beitrags, wie im folgenden Beispiel dargestellt.
  
    
    

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


### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)
  
    
    
Ein Thread, der den neuen Stammbeitrag enthält.
  
    
    
Im folgenden Antwortbeispiel ist der Thread dargestellt, der den neuen Stammbeitrag enthält.
  
    
    



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


## <a name="post"></a>Beitrag
<a name="bk_post"> </a>

Ruft einen vollständigen Thread ab, der den angegebenen Mikroblogbeitrag enthält.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **POST** `http://<siteCollection>/<site>/_api/social.feed/post`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 **ID**
  
    
    
Typ: **String**
  
    
    
Der eindeutige Bezeichner des Beitrags, wie im folgenden Beispiel dargestellt.
  
    
    

```

'ID':'1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.644240140e0b43379883ebcb859deaab.27.32.S-1-5-21-2127521184-1604012920-1887927527-66602'
```


### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)
  
    
    
Ein vollständiger Thread, der den angegebenen Beitrag enthält.
  
    
    
Im folgenden Antwortbeispiel ist der vollständige Thread dargestellt, der den angegebenen Beitrag enthält. Im Gegensatz zu Digest-Threads (die nur die zwei letzten Antworten enthalten), enthält ein vollständiger Thread alle Antworten.
  
    
    



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


## <a name="postreply"></a>Post/Reply
<a name="bk_postReply"> </a>

Postet eine Antwort auf den angegebenen Beitrag.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **POST** `http://<siteCollection>/<site>/_api/social.feed/post/reply`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 _restCreationData_
  
    
    
Type:  [SP.Social.SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData)
  
    
    
Die ID des Beitrags, auf den geantwortet werden soll, und die Eigenschaften der Antwort, wie im folgenden Beispiel dargestellt.
  
    
    

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


### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)
  
    
    
Ein Digest des geänderten Threads, der den angegebenen Beitrag enthält.
  
    
    
Im folgenden Antwortbeispiel ist der Thread dargestellt, der den angegebenen Beitrag und die Antwort enthält.
  
    
    



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


## <a name="postdelete"></a>Post/Delete
<a name="bk_postDelete"> </a>

Löscht den Mikroblobbeitrag. Wenn es sich bei dem Beitrag um einen Stammbeitrag handelt, wird der gesamte Thread gelöscht.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **POST** `http://<siteCollection>/<site>/_api/social.feed/post/delete`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 **ID**
  
    
    
Typ: **String**
  
    
    
Die ID des zu löschenden Beitrags, wie im folgenden Beispiel dargestellt.
  
    
    

```

'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a>Antwort

Keine
  
    
    

```
{"d":{"Delete":null}}
```


## <a name="postlike"></a>Post/Like
<a name="bk_postLike"> </a>

Damit wird angegeben, dass der angegebene Mikroblogbeitrag dem aktuellen Benutzer gefällt.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **POST** `http://<siteCollection>/<site>/_api/social.feed/post/like`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 **ID**
  
    
    
Typ: **String**
  
    
    
Die ID des Beitrags, der mit "Gefällt mir" markiert werden soll, wie im folgenden Beispiel dargestellt.
  
    
    

```
'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)
  
    
    
Ein Digest-Thread, der den angegebenen Beitrag enthält.
  
    
    
Im folgenden Antwortbeispiel ist der Thread dargestellt, der den Beitrag enthält, der mit "Gefällt mir" markiert wurde.
  
    
    



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


## <a name="postunlike"></a>Post/Unlike
<a name="bk_postUnlike"> </a>

Entfernt den aktuellen Benutzer aus der Liste der Benutzer, denen der angegebene Mikroblogbeitrag gefällt. Wenn dem angegebenen Benutzer der Beitrag nicht gefällt, wird diese Anforderung ignoriert.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **POST** `http://<siteCollection>/<site>/_api/social.feed/post/unlike`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 **ID**
  
    
    
Typ: **String**
  
    
    
Die ID des Beitrags, für den die Markierung "Gefällt mir" entfernt werden soll, wie im folgenden Beispiel dargestellt.
  
    
    

```

'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)
  
    
    
Ein Digest des geänderten Threads, der den angegebenen Beitrag enthält.
  
    
    
Im folgenden Antwortbeispiel ist der Thread dargestellt, der den Beitrag enthält, für den der Benutzer die Markierung "Gefällt mir" entfernt hat.
  
    
    



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


## <a name="postlikers"></a>Post/Likers
<a name="bk_postLikers"> </a>

Ruft die Benutzer ab, denen der angegebene Mikroblogbeitrag gefällt.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **POST** `http://<siteCollection>/<site>/_api/social.feed/post/likers`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 **ID**
  
    
    
Typ: **String**
  
    
    
Die ID des Beitrags, der Benutzern gefallen soll, wie im folgenden Beispiel dargestellt.
  
    
    

```

'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a>Antwort

 **Likers**
  
    
    
Typ:  [SP.Social.SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)[]
  
    
    
Die Benutzer, denen der angegebene Beitrag gefällt.
  
    
    
Im folgenden Antwortbeispiel sind die Benutzer dargestellt, denen der angegebene Beitrag gefällt.
  
    
    



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


## <a name="postlock"></a>Post/Lock
<a name="bk_postLock"> </a>

Sperrt den angegebenen Thread. Wenn ein Thread gesperrt ist, können dem Thread erst Antwortbeiträge hinzugefügt werden, nachdem er entsperrt wurde.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **POST** `http://<siteCollection>/<site>/_api/social.feed/post/lock`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 **ID**
  
    
    
Typ: **String**
  
    
    
Die ID des zu sperrenden Threads, wie im folgenden Beispiel dargestellt.
  
    
    

```

'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)
  
    
    
Ein Digest des gesperrten Threads.
  
    
    
Im folgend Antwortbeispiel ist ein gesperrter Thread dargestellt. Die **Attributes**-Eigenschaft des Threads enthält einen bitweisen Wert aus der  [SP.Social.SocialThreadAttributes](http://msdn.microsoft.com/library/21ff9f92-3223-bcc7-ceec-7b899ee29b6e%28Office.15%29.aspx)-Enumeration, der angibt, ob der Thread gesperrt ist.
  
    
    



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


## <a name="postunlock"></a>Post/Unlock
<a name="bk_postUnlock"> </a>

Hebt die Sperre für den angegebenen Thread auf.
  
    
    

### <a name="endpoint-uri-structure"></a>Endpunkt-URI-Struktur

 **POST** `http://<siteCollection>/<site>/_api/social.feed/post/unlock`
  
    
    

### <a name="request-parameter"></a>Anforderungsparameter

 **ID**
  
    
    
Typ: **String**
  
    
    
Die ID des zu entsperrenden Threads, wie im folgenden Beispiel dargestellt.
  
    
    

```

'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a>Antwort

Typ:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)
  
    
    
Ein Digest des entsperrten Threads.
  
    
    
Im folgenden Antwortbeispiel ist ein entsperrter Thread dargestellt. Die **Attributes**-Eigenschaft des Threads enthält einen bitweisen Wert aus der  [SP.Social.SocialThreadAttributes](http://msdn.microsoft.com/library/21ff9f92-3223-bcc7-ceec-7b899ee29b6e%28Office.15%29.aspx)-Enumeration, der angibt, ob der Thread gesperrt ist.
  
    
    



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


## <a name="example-rest-requests-for-feed-tasks"></a>Beispiel-REST-Anforderungen für den Feedaufgaben
<a name="bk_exampleRequests"> </a>

 **GET**-Anforderungen für Feedaufgaben geben Parameter im URI oder im **url**-Attribut der Anforderung an. **POST**-Anforderungen geben Parameter im **data**-Attribut des Anforderungstexts im XML- oder JavaScript Object Notation (JSON)-Format an. HTTP-Anforderungen können in einer beliebigen Sprache erfolgen, einschließlich JavaScript und C#. In den folgenden Beispielanforderungen wird veranschaulicht, wie Anforderungen mithilfe von JavaScript erfolgen und wie Entitätsinformaitonen im JSON-Format übergeben werden.
  
    
    
 **Beispiel:** Angeben des Parameters _ID_ im Anforderungstext (im Attribut **data**)
  
    
    

> **Hinweis:** Die Werte für die Eigenschaft **Id** von Threads und Beiträgen sind zu lang, um als URL gesendet werden zu können. Sie müssen im Anforderungstext gesendet werden. Selbst schreibgeschützte Vorgänge, die logisch gesehen Anforderungen des Typs **GET** sind, müssen daher als Anforderungen des Typs **POST** gesendet werden. Wenn Sie beispielsweise einen Thread abrufen möchten, müssen Sie eine Anforderung des Typs **POST** senden und den Wert **Id** des Threads als Entität im Anforderungstext übergeben.
  
    
    




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

 **Beispiel:** Veröffentlichen eines Stammbeitrags und Angeben des Parameters _restCreationData_ im Attribut **data**
  
    
    



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

Um eine Antwort auf einen angegebenen Thread zu veröffentlichen, senden Sie eine **POST**-Anforderung an die **Reply**-Ressource ( `<site url>/_api/social.feed/Post/Reply`), und übergeben **restCreationData**-Informationen, die die ID des Zielbeitrags enthalten.
  
    
    



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


## <a name="resources-used-in-feed-related-rest-requests-and-responses"></a>Ressourcen, die in den feedbezogene REST-Anforderungen und -Antworten verwendet werden
<a name="bk_FeedRelatedRestResources"> </a>

Die folgenden REST-Ressourcen dienen als Parameter in clientseitigen Anforderungen oder werden in Serverantworten zurückgegeben.
  
    
    

### <a name="spsocialsocialfeedoptions"></a>SP.Social.SocialFeedOptions
<a name="bk_SocialFeedOptions"> </a>

Stellt Optionen dar, die Sie angeben können, wenn Sie einen Feed abrufen.
  
    
    
In clientseitigen Anforderungen des Typs **GET** für Feeds können Sie optional Eigenschaften des Typs **SocialFeedOptions** als Parameter angeben. Diese Eigenschaften werden in der Abfragezeichenfolge angegeben.
  
    
    

|**Option**|**Typ**|**Beschreibung**|
|:-----|:-----|:-----|
|MaxThreadCount|**Int32**|Die maximale Anzahl von Threads, die abgerufen werden. Die Standardanzahl ist 20.|
|NewerThan|**String**|Die Grenze "neuer als" für den abzurufenden Zeitraum, als Zeichenfolgendarstellung eines **DateTime**-Objekts. Standardmäßig ist keine Grenze angegeben.|
|OlderThan|**String**|Die Grenze "älter als" für den abzurufenden Zeitraum, als Zeichenfolgendarstellung eines **DateTime**-Objekts. Standardmäßig ist keine Grenze angegeben.|
|SortOrder|**Int32**|Gibt die Sortierreihenfolge der Threads im Feed an. Standardmäßig werden Threads nach dem Änderungsdatum sortiert. Nur der Zeitachsenfeed wird nach Erstellungsdatum sortiert.<br/>          Ist **0** gesetzt, werden Threads nach dem Änderungszeitpunkt sortiert, ausgehend vom Änderungszeitpunkt des zuletzt geänderten Beitrags.<br/>          Ist **1** gesetzt, werden Threads nach dem Erstellungszeitpunkt sortiert, basierend auf dem Erstellungszeitpunkt ihrer Stammbeiträge.|
   

  
    
    

  
    
    

### <a name="spsocialsocialrestactor"></a>SP.Social.SocialRestActor
<a name="bk_SocialRestActor"> </a>

Stellt einen Benutzer, ein Dokument, eine Website oder ein Tag dar.
  
    
    
Der Server gibt eine **SocialRestActor**-Ressource in der Antwort an eine clientseitige Anforderung für Akteurinformationen zurück.
  
    
    
 **SocialRestActor** hat die folgenden Eigenschaften:
  
    
    

|**Eigenschaft**|**Typ**|**Beschreibung**|
|:-----|:-----|:-----|
|FollowableItem|**String**|Der eindeutige Bezeichner des angegebenen Akteurs. Gibt den Kontonamen für einen Benutzer oder den URI für ein Dokument, eine Website oder ein Tag zurück.|
|FollowableItemActor| [SP.Social.SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)|Der angegebene Benutzer. Gibt **null** zurück, wenn der Benutzer der aktuelle Benutzer ist oder wenn die Ressource kein Benutzertypakteur ist.|
|Me| [SP.Social.SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)|Der aktuelle Benutzer.|
   

  
    
    

  
    
    

### <a name="spsocialsocialrestfeed"></a>SP.Social.SocialRestFeed
<a name="bk_SocialRestFeed"> </a>

Stellt einen Newsfeed für soziale Netzwerke dar.
  
    
    
Der Server gibt eine **SocialRestFeed**-Ressource in der Antwort an eine clientseitige Anforderung für Feedinhaltsinformationen zurück.
  
    
    
 **SocialRestFeed** enthält ein umschlossenes Objekt des Typs [SP.Social.SocialFeed](http://msdn.microsoft.com/library/356c5475-2fd6-a655-c271-5d7f21af45e2%28Office.15%29.aspx) mit den folgenden Eigenschaften:
  
    
    

|**Eigenschaft**|**Typ**|**Beschreibung**|
|:-----|:-----|:-----|
|Attributes| [SP.Social.SocialFeedAttributes](http://msdn.microsoft.com/library/9ea7d3c5-7f96-88a6-5bdf-d7749b044ad3%28Office.15%29.aspx)|Ein bitweiser Satz von Attributen, die für den Feed gelten.|
|NewestProcessed|**DateTime**|Datum und Uhrzeit des neuesten abgerufenen Beitrags.|
|OldestProcessed|**DateTime**|Datum und Uhrzeit des ältesten abgerufenen Beitrags.|
|Threads| [SP.Social.SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx)[]|Die Threads, aus denen der Feed besteht.|
|UnreadMentionCount|**Int32**|Die Anzahl ungelesener Erwähnungen für den aktuellen Benutzer.|
   

  
    
    

  
    
    

### <a name="spsocialsocialrestpostcreationdata"></a>SP.Social.SocialRestPostCreationData
<a name="bk_SocialRestPostCreationData"> </a>

Gibt Inhalts- und damit verbundene Informationen für einen neuen Beitrag an.
  
    
    
Clients geben **SocialRestPostCreationData**-Eigenschaften als Parameter in einer Anforderung an, um einen Stammbeitrag oder eine Antwort zu veröffentlichen. Diese Eigenschaften werden im **data**-Attribut des Anforderungstexts angegeben.
  
    
    
 **SocialRestPostCreationData** enthält eine **ID**-Eigenschaft und ein umschlossenes  [SP.Social.SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx)-Objekt. **ID** ist erforderlich, die **SocialPostCreationData**-Eigenschaften sind jedoch optional.
  
    
    

|**Eigenschaft**|**Typ**|**Beschreibung**|
|:-----|:-----|:-----|
|ID (erforderlich)|**null** oder **String**|Gibt das Ziel des Beitrags an. Folgende Werte sind möglich:<br/>           **null** zur Veröffentlichung eines Stammbeitrags im Feed des aktuellen Benutzers<br/>           Die ID eines zu beantwortenden Beitrags<br/>           Die URL eines Websitefeeds als Veröffentlichungsziel (Beispiel: `http://<teamSiteURL>/newsfeed.aspx`)|
   
Das Objekt **SocialPostCreationData** hat folgende Eigenschaften:
  
    
    

|**Eigenschaft**|**Typ**|**Beschreibung**|
|:-----|:-----|:-----|
|Attachment| [SP.Social.SocialAttachment](http://msdn.microsoft.com/library/dfdee790-a1b0-19c8-0e92-5a6e058ba4db%28Office.15%29.aspx)|Ein Bild, Video oder eine Dokumentanlage für den Beitrag.|
|ContentItems| [SP.Social.SocialDataItem](http://msdn.microsoft.com/library/757e7b62-66a6-b03f-0ff0-769a42eb2b4a%28Office.15%29.aspx)[]|Die Elemente, mit denen die entsprechenden Token im Inhaltstext des Beitrags ersetzt werden sollen.|
|ContentText|**String**|Der reine Text des Beitrags, der positionale Einfügetoken enthalten kann (z. B. "Heute ist {0}s Geburtstag!").|
|SecurityUris|**String[]**|Zeichenfolgendarstellungen der URIs für SharePoint-Objekte, die Zugriffsberechtigungen für den Beitrag definieren.|
|Quelle| [SP.Social.SocialLink](http://msdn.microsoft.com/library/c71efc66-c9ca-ea35-b1c0-cb9ec3bbfcd3%28Office.15%29.aspx)|Die Quelle des Beitrags.|
|UpdateStatusText|**Boolean**|Ein Wert, der steuert, ob der Nur-Text-Inhalt des Beitrags den Statustext des aktuellen Benutzers ersetzen soll.|
   

  
    
    

  
    
    

### <a name="spsocialsocialrestthread"></a>SP.Social.SocialRestThread
<a name="bk_SocialRestThread"> </a>

Stellt einen Thread dar, der einen Stammbeitrag sowie eine Reihe von Antworten enthält.
  
    
    
Der Server gibt eine **SocialRestThread**-Ressource in der Antwort auf eine clientseitige Anforderung zurück, um einen Beitrag zu erstellen oder um einen volllständigen Thread abzurufen.
  
    
    
 **SocialRestThread** enthält eine Eigenschaft **ID** sowie ein umschlossenes Objekt des Typs [SP.Social.SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx).
  
    
    

|**Eigenschaft**|**Typ**|**Beschreibung**|
|:-----|:-----|:-----|
|ID|**String**|Der eindeutige Bezeichner des Threads.|
   
Das Objekt **SocialThread** hat die folgenden Eigenschaften:
  
    
    

|**Eigenschaft**|**Typ**|**Beschreibung**|
|:-----|:-----|:-----|
|Actors| [SP.Social.SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)[]|Das zusammengeführte Array teilnehmender Akteure.|
|Attribute|**Int32**|Der bitweise Wert, der den Satz von Attributen für den Thread darstellt. Siehe  [SP.Social.SocialThreadAttributes](http://msdn.microsoft.com/library/21ff9f92-3223-bcc7-ceec-7b899ee29b6e%28Office.15%29.aspx).|
|Id|**String**|Der eindeutige Bezeichner des Threads.|
|OwnerIndex|**Int32**|Der Index des Threadbesitzers innerhalb der Threadakteure.|
|Permalink|**String**|Die Zeichenfolgendarstellung des stabilen URIs für die Navigation zum Thread, sofern einer verfügbar ist.|
|PostReference| [SP.Social.SocialPostReference](http://msdn.microsoft.com/library/529e1db7-2e9a-5141-6b1e-94a5c63e7c16%28Office.15%29.aspx)|Der Beitrag, auf den verwiesen wird.|
|Antworten| [SP.Social.SocialPost](http://msdn.microsoft.com/library/a761ce71-d3d7-420a-1e06-962674124dfa%28Office.15%29.aspx)[]|Die Antworten auf den Thread.|
|RootPost| [SP.Social.SocialPost](http://msdn.microsoft.com/library/a761ce71-d3d7-420a-1e06-962674124dfa%28Office.15%29.aspx)|Der Stammbeitrag des Threads.|
|Status|**Int32**|Der Code, der behebbare Fehler identifiziert, die beim Abrufen des Threads aufgetreten sind. Siehe  [SP.Social.SocialStatusCode](http://msdn.microsoft.com/library/79292329-19de-43e1-5928-60b0edc36c94%28Office.15%29.aspx).|
|ThreadType| [SP.Social.SocialThreadType](http://msdn.microsoft.com/library/7444217e-ddda-d3a0-b19f-146cf8c6fcaa%28Office.15%29.aspx)|Der Threadtyp.|
|TotalReplyCount|**Int32**|Die Gesamtanzahl von Antworten für den Thread.|
   

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [Vorgehensweise: Lesen und Schreiben der sozialen Feed mithilfe des REST-Diensts in SharePoint](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)
    
  
-  [Arbeiten mit sozialen Feeds in SharePoint](work-with-social-feeds-in-sharepoint.md)
    
  
-  [REST-API-Referenz zum Folgen von Personen und Inhalten für SharePoint](following-people-and-content-rest-api-reference-for-sharepoint.md)
    
  
- Um die Mitglieder im **SP.Social**-OData-Schema anzuzeigen, die vom SharePoint-REST-Dienst verwendet werden, navigieren Sie zu  `http://<siteUri>/_api/$metadata`.
    
  
