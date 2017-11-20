---
title: Arbeiten mit sozialen Feeds in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 39f2163e-15cc-43bc-b131-041d5afdcd90
ms.openlocfilehash: 20e31de9a616bdc48746ff7bba6949d404c7d02d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="work-with-social-feeds-in-sharepoint"></a>Arbeiten mit Feeds für soziale Netzwerke in SharePoint
Hier erhalten Sie Informationen zu allgemeinen Programmierungsaufgaben zum Arbeiten mit sozialen Feeds und Mikroblogbeiträgen in SharePoint.
## <a name="apis-for-working-with-social-feeds-in-sharepoint"></a>APIs zum Arbeiten mit sozialen Feeds in SharePoint
<a name="bkmk_APIversions"> </a>

In lokalen SharePoint-Serverfarmen sollen interaktive Feeds Personen dazu ermutigen, Informationen zu teilen und mit Personen und Inhalten in Verbindung zu bleiben. Sie können viele der Features für soziale Medien auf der **Newsfeed**-Seite der persönlichen Website eines Benutzers sehen. Feeds enthalten Sammlungen von Threads mit Mikroblogeinträgen, Unterhaltungen, Statusaktualisierungen und anderen Benachrichtigungen.
  
    
    
SharePoint bietet die folgenden APIs, die Sie zum programmgesteuerten Arbeiten mit sozialen Feeds verwenden können:
  
    
    

- Clientobjektmodelle für verwalteten Code
    
  - .NET-Clientobjektmodell
    
  
  - Silverlight-Clientobjektmodell
    
  
  - Mobiles Clientobjektmodell
    
  
- JavaScript-Objektmodell
    
  
- REST (Representational State Transfer)-Dienst
    
  
- Serverobjektmodell
    
  
In der SharePoint-Entwicklung wird empfohlen, so oft wie möglich Client-APIs zu verwenden. Client-APIs umfassen Clientobjektmodelle, das JavaScript-Objektmodell und den REST-Dienst. Weitere Informationen zu APIs in SharePoint ihrer Verwendung finden Sie unter  [Auswählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md).
  
    
    
Jede API umfasst ein Manager-Objekt, mit dem Sie zentrale feedbezogene Aufgaben ausführen können. In Tabelle 1 sind das Manager-Objekt und weitere Schlüsselobjekte (oder REST-Ressourcen) der APIs sowie die Klassenbibliothek aufgeführt, in der Sie diese finden.
  
    
    

> **Hinweis:** Die Objektmodelle für Silverlight und den mobilen Client sind nicht explizit in Tabelle 1 oder Tabelle 2 erwähnt, da sie dieselben Kernfunktionen wie das .NET-Clientobjektmodell bieten und die gleichen Signaturen verwenden. Das Silverlight-Clientobjektmodell ist in Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll definiert und das Objektmodell für den mobilen Client in Microsoft.SharePoint.Client.UserProfiles.Phone.dll. 
  
    
    


**Tabelle 1. SharePoint-APIs für das programmgesteuerte Arbeiten mit sozialen Feeds**

|**API**|**Schlüsselobjekte**|
|:-----|:-----|
|.NET-Clientobjektmodell  <br/> Siehe  [Vorgehensweise: Erstellen und Löschen von Beiträge und Abrufen des für soziale Netzwerke-Feed mithilfe des clientobjektmodells .NET SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md)|Manager-Objekt:            [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) <br/> Primärer Namespace:            [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) <br/> Weitere Schlüsselobjekte:            [SocialFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeed.aspx) , [SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) , [SocialPost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPost.aspx) , [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , [SocialFeedOptions](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedOptions.aspx) , [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) <br/> Klassenbibliothek:           Microsoft.SharePoint.Client.UserProfiles.dll|
|JavaScript-Objektmodell  <br/> Siehe  [Vorgehensweise: Erstellen und Löschen von Beiträgen und sozialen Feed abrufen, indem Sie mit der JavaScript-Objektmodell in SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md)|Manager-Objekt:            [SocialFeedManager](http://msdn.microsoft.com/library/651fdf0f-841d-88f9-1e07-fcb3ad8c9410%28Office.15%29.aspx) <br/> Primärer Namespace:            [SP.Social](http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx) <br/> Weitere Schlüsselobjekte:            [SocialFeed](http://msdn.microsoft.com/library/356c5475-2fd6-a655-c271-5d7f21af45e2%28Office.15%29.aspx),  [SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx),  [SocialPost](http://msdn.microsoft.com/library/a761ce71-d3d7-420a-1e06-962674124dfa%28Office.15%29.aspx),  [SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx),  [SocialFeedOptions](http://msdn.microsoft.com/library/65caf283-6e7a-50dc-ef8e-a4e12bd237ac%28Office.15%29.aspx),  [SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx) <br/> Klassenbibliothek:           SP.UserProfiles.js|
|REST-Dienst  <br/> Siehe  [Vorgehensweise: Lesen und Schreiben der sozialen Feed mithilfe des REST-Diensts in SharePoint](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)|Manager-Ressource:            [social.feed](social-feed-rest-api-reference-for-sharepoint.md) (SocialRestFeedManager) <br/> Primärer Namespace (OData):           **SP.Social** <br/> Weitere Schlüsselressourcen:           SocialFeed,  [SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed), SocialThread,  [SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread), SocialPost, SocialPostCreationData,  [SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData),  [SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions), SocialActor,  [SociaRestActor](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestActor) <br/> Zugriffspunkt:            `<siteUri>/_api/social.feed`|
|Serverobjektmodell <br/>Hinweis: Code, der mit dem Serverobjektmodell auf Feeddaten zugreift und remote ausgeführt wird, muss ein  [SPServiceContextScope](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPServiceContextScope.aspx)-Objekt verwenden.|Manager-Objekt:            [SPSocialFeedManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.aspx) <br/> Primärer Namespace:            [Microsoft.Office.Server.Social](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.aspx) <br/> Weitere Schlüsselobjekte:            [SPSocialFeed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeed.aspx) , [SPSocialThread](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialThread.aspx) , [SPSocialPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialPost.aspx) , [SPSocialFeedOptions](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedOptions.aspx) , [SPSocialActor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActor.aspx) <br/> Klassenbibliothek:           Microsoft.Office.Server.UserProfiles.dll|
   
Verwenden Sie ein  [SPServiceContextScope](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPServiceContextScope.aspx) -Objekt in Ihrem Code, wenn Sie mit dem Serverobjektmodell auf Feedinhalte zugreifen und der Code nicht in einer SharePoint-Instanz ausgeführt wird (d. h. die Erweiterung ist nicht im Ordner „Layouts" auf dem Anwendungsserver installiert). Der folgende Code stellt eine Möglichkeit dar, das [SPServiceContextScope](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPServiceContextScope.aspx) -Objekt in Ihren Code zu integrieren.
  
    
    



```cs

using (SPSite site = new SPSite(<siteURL>))
{
    using (new Microsoft.SharePoint.SPServiceContextScope(SPServiceContext.GetContext(site)))
    {
        // code
    }
}

```


## <a name="common-programming-tasks-for-working-with-social-feeds-in-sharepoint"></a>Allgemeine Programmierungsaufgaben für das Arbeiten mit sozialen Feeds in SharePoint
<a name="bkmk_CommonTasks"> </a>

Tabelle 2 zeigt allgemeine Programmierungsaufgaben für das Arbeiten mit sozialen Feeds sowie die Elemente, die Sie zur Ausführung verwenden. Die Elemente stammen aus dem .NET-Clientobjektmodell (CSOM), dem JavaScript-Objektmodell (JSOM), dem REST-Dienst und dem Serverobjektmodell (SSOM).
  
    
    

**Tabelle 2. API für allgemeine Programmierungsaufgaben für das Arbeiten mit sozialen Feeds**


|**Aufgabe**|**Elemente**|
|:-----|:-----|
|Erstellen einer Instanz des Manager-Objekts im Kontext des aktuellen Benutzers|CSOM:  [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) <br/> JSOM:  [SocialFeedManager](http://msdn.microsoft.com/library/f7cf172f-970b-6b71-9eb4-b9a8bb7a0001%28Office.15%29.aspx) <br/> REST: **GET** [`<siteUri>/_api/social.feed`](social-feed-rest-api-reference-for-sharepoint.md) <br/> SSOM:  [SPSocialFeedManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.aspx)|
|Erstellen einer Instanz des Manager-Objekts im Kontext eines bestimmten Benutzers|CSOM: nicht implementiert  <br/> JSOM: nicht implementiert  <br/> REST: nicht implementiert  <br/> SSOM:  [SPSocialFeedManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.aspx)|
|Abrufen des Benutzern für den aktuellen Kontext|CSOM:  [Owner](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.Owner.aspx) <br/> JSOM:  [owner](http://msdn.microsoft.com/library/0307264e-d733-77f0-edae-f5468e58d0b7%28Office.15%29.aspx) <br/> REST: **GET** [`<siteUri>/_api/social.feed/my`](social-feed-rest-api-reference-for-sharepoint.md#bk_my) <br/> SSOM:  [Owner](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.Owner.aspx)|
|Abrufen des Feeds für den aktuellen Benutzer  <br/> (Angeben des Feedtyps)|CSOM:  [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx) <br/> JSOM:  [getFeed](http://msdn.microsoft.com/library/cddaccd8-28da-6798-d8cb-4e9351efddf3%28Office.15%29.aspx) <br/> REST: **GET** [`<siteUri>/_api/social.feed/my/Feed`](social-feed-rest-api-reference-for-sharepoint.md#bk_myFeed) (personal feed.md), [`<siteUri>/_api/social.feed/my/News`](social-feed-rest-api-reference-for-sharepoint.md#bk_myNews),  [`<siteUri>/_api/social.feed/my/TimelineFeed`](social-feed-rest-api-reference-for-sharepoint.md#bk_myTimelineFeed), or  [`<siteUri>/_api/social.feed/my/Likes`](social-feed-rest-api-reference-for-sharepoint.md#bk_myLikes) <br/> SSOM:  [GetFeed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.GetFeed.aspx)|
|Abrufen des persönlichen Feeds für einen bestimmten Benutzer|CSOM:  [GetFeedFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeedFor.aspx) <br/> JSOM:  [getFeedFor](http://msdn.microsoft.com/library/074ed255-9393-448d-1f7e-720fdeb05f48%28Office.15%29.aspx) <br/> REST: **GET** [`<siteUri>/_api/social.feed/actor(item='domain\\user')/Feed`](social-feed-rest-api-reference-for-sharepoint.md#bk_actorFeed) <br/> SSOM:  [GetFeedFor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.GetFeedFor.aspx)|
|Abrufen des Websitefeeds für eine Teamwebsite  <br/> (Angeben der URL des Websitefeeds als Akteur (Beispiel: http://<siteCollection>/<teamSite>/newsfeed.aspx))|CSOM:  [GetFeedFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeedFor.aspx) <br/> JSOM:  [getFeedFor](http://msdn.microsoft.com/library/074ed255-9393-448d-1f7e-720fdeb05f48%28Office.15%29.aspx) <br/> REST: **GET** [`<siteUri>/_api/social.feed/actor(item=@v)/Feed?@v='http://<siteCollection>/<teamSite>/newsfeed.aspx'`](social-feed-rest-api-reference-for-sharepoint.md#bk_actorFeed) <br/> SSOM:  [GetFeedFor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.GetFeedFor.aspx)|
|Veröffentlichen eines Stammbeitrags im Feed des aktuellen Benutzers  <br/> (Angeben von **null** für das Ziel)|CSOM:  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) <br/> JSOM:  [createPost](http://msdn.microsoft.com/library/e9ad06a1-831d-8ed0-c76e-8b049f14216f%28Office.15%29.aspx) <br/> REST: **POST** [`<siteUri>/_api/social.feed/my/Feed/Post`](social-feed-rest-api-reference-for-sharepoint.md#bk_myFeedPost) und Übergeben des Parameters _restCreationData_ im Text der Anforderung <br/> JSOM: [createPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.CreatePost.aspx)|
|Veröffentlichen eines Beitrags im Websitefeed  <br/> (Angeben der URL des Websitefeeds als Ziel (Beispiel: http://<siteCollection>/teamSite>/newsfeed.aspx))|CSOM:  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) <br/> JSOM:  [createPost](http://msdn.microsoft.com/library/e9ad06a1-831d-8ed0-c76e-8b049f14216f%28Office.15%29.aspx) <br/> REST: **POST** [`<siteUri>/_api/social.feed/actor(item=@av)/feed/post/?@av='<teamSiteUri>/newsfeed.aspx'`](social-feed-rest-api-reference-for-sharepoint.md#bk_actorFeedPost) und Übergeben des Parameters _restCreationData_ im Text der Anforderung (**null** für den Parameter _ID_ angeben) <br/> JSOM: [createPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.CreatePost.aspx)|
|Veröffentlichen einer Antwort auf einen Beitrag  <br/> (Angeben der ID des Zielthreads)|CSOM:  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) <br/> JSOM:  [createPost](http://msdn.microsoft.com/library/e9ad06a1-831d-8ed0-c76e-8b049f14216f%28Office.15%29.aspx) <br/> REST: **POST** [`<siteUri>/_api/social.feed/Post/Reply`](social-feed-rest-api-reference-for-sharepoint.md#bk_postReply) und Übergeben des Parameters _restCreationData_ im Text der Anforderung <br/> JSOM: [createPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.CreatePost.aspx)|
|Löschen eines Beitrags, einer Antwort oder eines Threads im Feed des aktuellen Benutzers (durch Löschen eines Stammbeitrags wird der gesamte Thread gelöscht)|CSOM:  [DeletePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.DeletePost.aspx) <br/> JSOM: [deletePost](http://msdn.microsoft.com/library/06e03f87-c97d-8634-a02b-f7812eb7beeb%28Office.15%29.aspx) <br/> REST: **POST** [`<siteUri>/_api/social.feed/Post/Delete`](social-feed-rest-api-reference-for-sharepoint.md#bk_postDelete) und Übergeben des Parameters _ID_ im Text der Anforderung <br/> SSOM:  [DeletePost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.DeletePost.aspx)|
|Abrufen eines Threads (eines Stammbeitrags und allen dazugehörigen Antworten) aus dem Feed des Benutzers|CSOM:  [GetFullThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFullThread.aspx) <br/> JSOM:  [getFullThread](http://msdn.microsoft.com/library/6bb384f3-9474-581f-e18d-e8c4f44c3cdf%28Office.15%29.aspx) <br/> REST: **POST** [`<siteUri>/_api/social.feed/Post`](social-feed-rest-api-reference-for-sharepoint.md#bk_post) und Übergeben des Parameters _ID_ im Text der Anforderung <br/> SSOM:  [GetFullThread](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.GetFullThread.aspx)|
|Markieren eines Beitrags oder einer Antwort des Benutzers mit „Gefällt mir“ („Gefällt mir nicht mehr“)|CSOM:  [LikePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.LikePost.aspx) ( [UnlikePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.UnlikePost.aspx) ) <br/> JSOM:  [likePost](http://msdn.microsoft.com/library/f401a584-1712-50af-ee08-2999a16388d6%28Office.15%29.aspx) ( [unlikePost](http://msdn.microsoft.com/library/c778bd7d-91e5-15dc-eeb8-b571957e8338%28Office.15%29.aspx))  <br/> REST: **POST** [`<siteUri>/_api/social.feed/Post/Like`](social-feed-rest-api-reference-for-sharepoint.md#bk_postLike) ([`<siteUri>/_api/social.feed/Post/Unlike`](social-feed-rest-api-reference-for-sharepoint.md#bk_postUnlike)) und Übergeben des Parameters _ID_ im Text der Anforderung <br/> SSOM:  [LikePost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.LikePost.aspx) ( [UnlikePost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.UnlikePost.aspx) )|
|Abrufen aller Personen, denen ein Beitrag gefällt|CSOM:  [GetAllLikers](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetAllLikers.aspx) <br/> JSOM:  [getAllLikers](http://msdn.microsoft.com/library/76286fdc-002f-2b13-dc26-53097eb2e3a2%28Office.15%29.aspx) <br/> REST: **POST** [`<siteUri>/_api/social.feed/Post/Likers`](social-feed-rest-api-reference-for-sharepoint.md#bk_postLikers) und Übergeben des Parameters _ID_ im Text der Anforderung <br/> SSOM:  [GetAllLikers](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.GetAllLikers.aspx)|
|Abrufen der Beitrage, in denen ein Benutzer erwähnt wird|CSOM:  [GetMentions](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetMentions.aspx) <br/> JSOM:  [getMentions](http://msdn.microsoft.com/library/78f064c3-5b96-373e-e7f0-8603aedc5ded%28Office.15%29.aspx) <br/> REST: **GET** [`<siteUri>/_api/social.feed/my/MentionFeed`](social-feed-rest-api-reference-for-sharepoint.md#bk_myMentionFeed) <br/> SSOM:  [GetMentions](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.GetMentions.aspx)|
|Abrufen der Anzahl ungelesener Erwähnungen für den aktuellen Benutzer|CSOM:  [GetUnreadMentionCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetUnreadMentionCount.aspx) <br/> JSOM:  [getUnreadMentionCount](http://msdn.microsoft.com/library/18dde16a-f78f-f65e-0644-4eb737b1ae00%28Office.15%29.aspx) <br/> REST: **GET** [`<siteUri>/_api/social.feed/my/UnreadMentionCount`](social-feed-rest-api-reference-for-sharepoint.md#bk_myUnreadMentionCount) <br/> SSOM:  [GetUnreadMentionCount](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.GetUnreadMentionCount.aspx)|
|Sperren (Entsperren) eines Threads im Feed des aktuellen Benutzers|CSOM:  [LockThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.LockThread.aspx) ( [UnlockThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.UnlockThread.aspx) ) <br/> JSOM:  [lockThread](http://msdn.microsoft.com/library/cc696bb7-e7fd-7a57-5db5-736c3733589e%28Office.15%29.aspx) ( [unlockThread](http://msdn.microsoft.com/library/ee9288d6-ace0-1ec2-ea7c-0ee300b6e1ea%28Office.15%29.aspx))  <br/> REST: **POST** [`<siteUri>/_api/social.feed/Post/Lock`](social-feed-rest-api-reference-for-sharepoint.md#bk_postLock) ([`<siteUri>/_api/social.feed/Post/Unlock`](social-feed-rest-api-reference-for-sharepoint.md#bk_postUnlock)) und Übergeben des Parameters _ID_ im Text der Anforderung <br/> SSOM:  [LockThread](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.LockThread.aspx) ( [UnlockThread](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.UnlockThread.aspx) .md)|
   

> **Hinweis:** Der Platzhalterwert _domain\\user_ im REST-Beispiel sollte durch den Kontonamen eines tatsächlichen Benutzers ersetzt werden. Um zu erfahren, wie Sie einen REST-Parameter in einem Anforderungstext übergeben, sehen Sie sich die [Beispiele](social-feed-rest-api-reference-for-sharepoint.md#bk_exampleRequests) in der REST-API-Referenz für soziale Netzwerke an.
  
    
    

SharePoint bietet keine API zur Anpassung des Layouts oder für das direkte Rendering von Mikroblogbeiträgen an. SharePoint bietet nur die Daten an und ermöglicht es plattformübergreifenden und geräteübergreifenden Clientanwendungen,  Layouts zu definieren, die für die entsprechenden Formularfaktoren und deren Anforderungen geeignet sind. In der SharePoint-Entwicklung können Sie JavaScript-Außerkraftsetzungen beim clientseitigen Rendering verwenden. Eine Anleitung dazu finden Sie unter [Anpassen einer Listenansicht in Add-Ins für SharePoint durch clientseitiges Rendering](http://msdn.microsoft.com/library/8d5cabb2-70d0-46a0-bfe0-9e21f8d67d86%28Office.15%29.aspx).
  
    
    

## <a name="overview-of-feed-types-in-the-my-site-social-api"></a>Übersicht über die Feedtypen in der Meine Website-API für soziale Netzwerke
<a name="bkmk_FeedTypes"> </a>

Feedtypen stellen Feeddatenausschnitte dar. Beim Abrufen eines Feeds für den aktuellen Benutzer können Sie einen der folgenden Feedtypen angeben:
  
    
    

- **Personal** enthält die von einem Benutzer generierten Beiträge und Aktualisierungen. Auf Meine Website wird dieser Feed auf der Seite **Über mich** des Benutzers angezeigt.
    
  
- **News** enthält die generierten Beiträge und Aktualisierungen des aktuellen Benutzers sowie der Personen und Inhalte, denen der Benutzer folgt. Verwenden Sie beim Abrufen des **News**-Feedtyps die Option **ByModifiedTime** für die Sortierreihenfolge, um die aktuellen (zwischengespeicherten) Aktivitäten der Personen abzurufen, denen der Benutzer folgt. Auf Meine Website wird dieser Feed auf der Seite **Newsfeed** des Benutzers angezeigt.
    
  
- **Timeline** enthält die generierten Beiträge und Aktualisierungen des aktuellen Benutzers sowie der Personen und Inhalte, denen der Benutzer folgt. Die Verwendung von **Timeline** ist vor allem sinnvoll, wenn Sie Feeddaten eines bestimmten Zeitraums abrufen oder anhand der Option **ByCreatedTime** (die das größte Sampling von Personen umfasst) sortieren möchten.
    
  
- **Likes** enthält Referenzthreads mit einer **PostReference**-Eigenschaft, die einen Beitrag darstellt, den der aktuelle Benutzer mit dem Attribut **Gefällt mir** gekennzeichnet hat.
    
  
- **Everyone** enthält die Threads der gesamten Organisation des aktuellen Benutzers.
    
  
Die Server-, Client und JavaScript-Objektmodelle ermöglichen die Verwendung der **GetFeed**-Methode ,mit der Sie jeden Feedtyp für den aktuellen Benutzer abrufen können, sowie die Verwendung der **GetFeedFor**-Methode, mit der Sie (nur) den Feedtyp **Personal** für einen bestimmten Benutzer abrufen können. Bei beiden Methoden wird ein **SocialFeedOptions**-Objekt als Parameter verwendet, mit dem Sie die zeitbasierte Sortierreihenfolge, den Datumsbereich und die maximale Anzahl der zurückzugebenden Threads angeben können.
  
    
    

>  **Hinweis:** Der REST-Dienst stellt separate Ressourcen zum Abrufen der einzelnen Feedtypen bereit (siehe Tabelle 2). 
  
    
    

Wenn ein Thread mehr als zwei Antworten enthält, gibt der Server einen Digest des Threads zurück, der nur die letzten zwei Antworten enthält. (Auf Threaddigests wird das Threadattribut **IsDigest** angewendet.) Wenn Sie alle Antworten eines Threads abrufen möchten, müssen Sie die **GetFullThread**-Methode für das Feed-Manager-Objekt aufrufen und die Thread-ID übergeben.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bkmk_AdditionalResources"> </a>


- **Artikel zu Konzepten und Gewusst-wie-Artikel**
    
  
-  [Soziale Funktionen und Zusammenarbeit in SharePoint](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [Vorgehensweise: Erstellen und Löschen von Beiträge und Abrufen des für soziale Netzwerke-Feed mithilfe des clientobjektmodells .NET SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md)
    
  
-  [Vorgehensweise: Erstellen und Löschen von Beiträgen und sozialen Feed abrufen, indem Sie mit der JavaScript-Objektmodell in SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md)
    
  
-  [Vorgehensweise: Lesen und Schreiben des sozialen Feeds mithilfe des REST-Diensts in SharePoint](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)
    
  
-  [Vorgehensweise: Einschließen von Erwähnungen, Tags und Links zu Websites und Dokumenten in Beiträgen in SharePoint](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md)
    
  
-  [Vorgehensweise: Einbetten von Bildern, Videos und Dokumenten in Beiträgen in SharePoint](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md)
    
  
-  [Referenzthreads und Digest-Threads in sozialen Feeds für SharePoint](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md)
    
  
- **API-Referenzdokumentation**
    
  
-  [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) (Clientobjektmodell)
    
  
-  [SP.Social namespace](http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx) (JavaScript-Objektmodell)
    
  
-  [REST-API-Referenz für sozialen Feed für SharePoint](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [Microsoft.Office.Server.Social](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.aspx) (Serverobjektmodell)
    
  
