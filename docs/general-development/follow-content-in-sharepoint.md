---
title: Folgen von Inhalten in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 30e68cd6-6e55-4cf9-afd6-7139b0a97288
ms.openlocfilehash: e670bd3dbf8c50a98c1ac5c5599b565bd42aef7e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="follow-content-in-sharepoint"></a>Folgen von Inhalten in SharePoint
Erfahren Sie mehr über allgemeine Programmierungsaufgaben für das Folgen von Inhalten (Dokumente, Websites und Tags) in SharePoint.
## <a name="apis-for-following-content-in-sharepoint"></a>APIs für das Folgen von Inhalten in SharePoint
<a name="bkmk_APIversions"> </a>

Wenn Benutzer Dokumenten, Websites oder Tags folgen, werden Statusupdates von Dokumenten, Unterhaltungen auf Websites und Benachrichtigungen zuTags in ihrem Newsfeed angezeigt. Die Features im Zusammenhang mit dem Folgen von Inhalten werden auf den Inhaltsseiten **Newsfeed** und **Folgen** angezeigt.
  
    
    
SharePoint stellt die folgenden APIs bereit, mit denen Sie Inhalten programmgesteuert folgen können:
  
    
    

- Clientobjektmodelle für verwalteten Code
    
  - .NET-Clientobjektmodell
    
  
  - Silverlight-Clientobjektmodell
    
  
  - Mobiles Clientobjektmodell
    
  
- JavaScript-Objektmodell
    
  
- REST (Representational State Transfer)-Dienst
    
  
- Serverobjektmodell
    
  
In der SharePoint-Entwicklung wird empfohlen, so oft wie möglich Client-APIs zu verwenden. Client-APIs umfassen Clientobjektmodelle, das JavaScript-Objektmodell und einen REST-Dienst. Weitere Informationen zu APIs in SharePoint und zu ihrer Verwendung finden Sie unter  [Auswählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md).
  
    
    
Jede API enthält ein Manager-Objekt, das Sie verwenden, um wichtige Aufgaben für das Folgen von Inhalten auszuführen.
  
> [!NOTE]
> Die gleichen APIs werden verwendet, um Personen zu folgen. Einen Überblick über Aufgaben beim Folgen von Personen finden Sie unter [Folgen von Personen in SharePoint](follow-people-in-sharepoint.md).
  
    
    

Tabelle 1 zeigt den Manager und andere Schlüsselobjekte (oder REST-Ressourcen) in den APIs und die Klassenbibliothek (oder Zugriffspunkt), in dem Sie diese finden können.
  
> [!NOTE]
> Die Silverlight- und mobilen Clientobjektmodelle sind in Tabelle 1 oder Tabelle 2 nicht enthalten, da sie dieselben Kernfunktionen wie das .NET-Clientobjektmodell bereitstellen und dieselben Signaturen verwenden. Das Silverlight-Clientobjektmodell ist in Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll definiert und das mobile Clientobjektmodell in Microsoft.SharePoint.Client.UserProfiles.Phone.dll. 
  
    
    


**Tabelle 1: Für das programmgesteuerte Folgen von Inhalten verwendete SharePoint-APIs**

|**API**|**Schlüsselobjekte**|
|:-----|:-----|
|.NET-Clientobjektmodell  <br/> Weitere Informationen:  [Vorgehensweise: Führen Sie Dokumente und Websites mit .NET Client-Objektmodell in SharePoint](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)|Manager-Objekt:            [SocialFollowingManager]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)) <br/> Primärer Namespace:            [Microsoft.SharePoint.Client.Social]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx)) <br/> Sonstige Schlüsselobjekte:            [SocialActor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx)) , [SocialActorInfo]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorInfo.aspx)) , [SocialActorType]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorType.aspx)) , [SocialActorTypes]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorTypes.aspx)) <br/> Klassenbibliothek:           Microsoft.SharePoint.Client.UserProfiles.dll  |
|JavaScript-Objektmodell|Manager-Objekt:            [SocialFollowingManager]((http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx)) <br/> Primärer Namespace:            [SP.Social]((http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx)) <br/> Andere wichtige Objekte:            [SocialActor]((http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)),  [SocialActorInfo]((http://msdn.microsoft.com/library/d940db32-1561-c868-bb66-0612e2031f17%28Office.15%29.aspx)),  [SocialActorType]((http://msdn.microsoft.com/library/fbde74da-f292-dc87-0b7e-81bc5b7a880c%28Office.15%29.aspx)),  [SocialActorTypes]((http://msdn.microsoft.com/library/a460c3e6-ed88-117d-6755-4c5803a154a0%28Office.15%29.aspx)) <br/> Klassenbibliothek:           SP.UserProfiles.js  |
|REST-Dienst  <br/> Weitere Informationen:  [Vorgehensweise: führen Sie Dokumente, Websites und Tags mithilfe des REST-Diensts in SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)|Manager-Ressource:            [social.following](following-people-and-content-rest-api-reference-for-sharepoint.md) <br/> Primärer Namespace (OData):           **sp.social.SocialRestFollowingManager** <br/> Andere wichtige Ressourcen:           **SocialActor**, **SocialActorInfo**, **SocialActorType**, **SocialActorTypes** <br/> Zugriffspunkt:            `<siteUri>/_api/social.following` |
|Serverobjektmodell|Manager-Objekt:            [SPSocialFollowingManager]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx)) <br/> Primärer Namespace:            [Microsoft.Office.Server.Social]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.aspx)) <br/> Sonstige Schlüsselobjekte:            [SPSocialActor]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActor.aspx)) , [SPSocialActorInfo]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorInfo.aspx)) , [SPSocialActorType]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorType.aspx)) , [SPSocialActorTypes]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorTypes.aspx)) <br/> Klassenbibliothek:           Microsoft.Office.Server.UserProfiles.dll  |
   

## <a name="common-programming-tasks-for-following-content-in-sharepoint"></a>Allgemeine Programmierungsaufgaben für das Folgen von Inhalten in SharePoint
<a name="bkmk_CommonTasks"> </a>

Tabelle 2 zeigt allgemeine Programmierungsaufgaben für das Folgen von Inhalten sowie die Elemente, die Sie zur Ausführung verwenden. Die Elemente stammen aus dem .NET-Clientobjektmodell (CSOM), dem JavaScript-Objektmodell (JSOM), dem REST-Dienst und dem Serverobjektmodell (SSOM).
  
> [!NOTE]
> Die gleichen APIs werden verwendet, um Personen zu folgen. Einen Überblick über Aufgaben beim Folgen von Personen finden Sie unter [Folgen von Personen in SharePoint](follow-people-in-sharepoint.md).
  
    
    


**Tabelle 2: API für allgemeine Aufgaben für das Folgen von Inhalten in SharePoint Server**


|**Aufgabe**|**Elemente**|
|:-----|:-----|
|Erstellen einer Instanz eines Manager-Objekts im Kontext des aktuellen Benutzers|CSOM:  [SocialFollowingManager]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)) <br/> JSOM:  [SocialFollowingManager]((http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx)) <br/> REST:  `<siteUri>/_api/social.following` <br/> SSOM:  [SPSocialFollowingManager]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx))|
|Erstellen einer Instanz eines Manager-Objekts im Kontext eines angegebenen Benutzers|CSOM: nicht implementiert  <br/> JSOM: nicht implementiert  <br/> REST: nicht implementiert  <br/> SSOM:  [SPSocialFollowingManager]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx)) (überladen)|
|Zulassen, dass der aktuelle Benutzer beginnt, einem Element zu folgen (das Folgen zu beenden)|CSOM:  [Follow]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx)) ( [StopFollowing]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx)) ) <br/> JSOM:  [follow]((http://msdn.microsoft.com/library/40d14320-27ba-2941-b0e2-be3b5a407c89%28Office.15%29.aspx)) ( [stopFollowing]((http://msdn.microsoft.com/library/65b0e9be-dc5e-09fb-c57f-7a933de09a4c%28Office.15%29.aspx)))  <br/> REST: **POST** [`<siteUri>/_api/social.following/Follow`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_Follow) ( [`<siteUri>/_api/social.following/StopFollowing`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_StopFollowing))           und Übergeben des Parameters _actor_ im Text der Anforderung <br/> SSOM:  [Follow]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.Follow.aspx)) ( [StopFollowing]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.StopFollowing.aspx)) )|
|Herausfinden, ob der aktuelle Benutzer einem bestimmten Element folgt|CSOM:  [IsFollowed]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx)) <br/> JSOM:  [isFollowed]((http://msdn.microsoft.com/library/2c1f62e6-fb75-ad4d-c081-36408b418c21%28Office.15%29.aspx)) <br/> REST: **POST** [`<siteUri>/_api/social.following/IsFollowed`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_IsFollowed) und Übergeben des Parameters _actor_ im Text der Anforderung <br/> SSOM:  [IsFollowed]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.IsFollowed.aspx))|
|Abrufen von Benutzern, Dokumenten, Websites und Tags denen der aktuelle Benutzer folgt|CSOM:  [GetFollowed]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx)) <br/> JSOM:  [getFollowed]((http://msdn.microsoft.com/library/432a7cec-6add-fdb1-a79f-a93414ee8cd3%28Office.15%29.aspx)) <br/> REST: **GET** [`<siteUri>/_api/social.following/my/Followed(types=2)`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_Followed) (documents = **2**, sites = **4**, tags = **8**.md)  <br/> SSOM:  [GetFollowed]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetFollowed.aspx))|
|Abrufen der Anzahl von Benutzern, Dokumenten, Websites und Tags denen der Benutzer folgt|CSOM:  [GetFollowedCount]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx)) <br/> JSOM:  [getFollowedCount]((http://msdn.microsoft.com/library/97b53b4f-481a-cf41-1854-8f3ff860b2bb%28Office.15%29.aspx)) <br/> REST: **GET** [`<siteUri>/_api/social.following/my/FollowedCount(types=2)`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_FollowedCount) (documents = **2**, sites = **4**, tags = **8**.md)  <br/> SSOM:  [GetFollowedCount]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetFollowedCount.aspx))|
|Abrufen des URI der Website, die die Dokumente des aktuellen Benutzers auflistet, denen gefolgt wird|CSOM:  [FollowedDocumentsUri]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.FollowedDocumentsUri.aspx)) <br/> JSOM:  [followedDocumentsUri]((http://msdn.microsoft.com/library/3a70b9c7-abd7-94ff-d730-70298673d6ec%28Office.15%29.aspx)) <br/> REST: **GET** [`<siteUri>/_api/social.following/my/FollowedDocumentsUri`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_MyFollowedDocumentsUri) <br/> SSOM:  [FollowedDocumentsUri]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.FollowedDocumentsUri.aspx))|
|Abrufen des URI der Website, die die Websites des aktuellen Benutzers auflistet, denen gefolgt wird|CSOM:  [FollowedSitesUri]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.FollowedSitesUri.aspx)) <br/> JSOM:  [followedSitesUri]((http://msdn.microsoft.com/library/829404bc-1b3a-7545-5e95-0922df330084%28Office.15%29.aspx)) <br/> REST: **GET** [`<siteUri>/_api/social.following/my/FollowedSitesUri`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_MyFollowedSitesUri) <br/> SSOM:  [FollowedSitesUri]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.FollowedSitesUri.aspx))|
   
> [!NOTE]
> Beispiele für die Verwendung des REST-Diensts, um Inhalten zu folgen, finden Sie unter [Vorgehensweise: Folgen von Dokumenten, Websites und Tags mithilfe des REST-Diensts in SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md). 
  
    
    


## <a name="how-to-get-a-tags-guid-based-on-the-tags-name-by-using-the-javascript-object-model"></a>Abrufen der GUID eines Tags basierend auf dem Namen des Tags mithilfe des JavaScript-Objektmodells
<a name="bk_getTagGuid"> </a>

Um das Folgen eines Tags zu starten und zu beenden oder herauszufinden, ob der aktuelle Benutzer ihm folgt, benötigen Sie die GUID des Tags. Der folgende Code zeigt, wie Sie die GUID basierend auf dem Namen des Tags abrufen.
  
    
    
Bevor Sie den Code ausführen, müssen Sie einen Verweis zu **sp.taxonomy.js** hinzufügen und den Namen des Platzhaltertags in den Namen eines vorhandenen Tags ändern.
  
    
    



```

function getTagGuid() {
    var tagName = '#tally';
    var clientContext = new SP.ClientContext.get_current();
    var label = SP.Taxonomy.LabelMatchInformation.newObject(clientContext);
    label.set_termLabel(tagName);
    label.set_trimUnavailable(false);
    var taxSession = SP.Taxonomy.TaxonomySession.getTaxonomySession(clientContext);
    var termStore = taxSession.getDefaultKeywordsTermStore();
    var termSet = termStore.get_hashTagsTermSet();
    terms = termSet.getTerms(label);
    clientContext.load(terms);
    clientContext.executeQueryAsync(
        function () {
            var tag = terms.get_item(0);
            if (tag !== null) {
                var tagGuid = tag.get_id().toString();
                if (!SP.ScriptUtility.isNullOrEmptyString(tagGuid)) {
                    alert(tagGuid);
                }
            }
        },
        function (sender, args) {
            alert(args.get_message());
        }
    );
}

```


## <a name="see-also"></a>Siehe auch
<a name="bk_addResources"> </a>


-  [Vorgehensweise: Führen Sie Dokumente und Websites mit .NET Client-Objektmodell in SharePoint](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)
    
  
-  [Vorgehensweise: führen Sie Dokumente, Websites und Tags mithilfe des REST-Diensts in SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)
    
  
-  [REST-API-Referenz zum Folgen von Personen und Inhalten für SharePoint](following-people-and-content-rest-api-reference-for-sharepoint.md)
    
  
-  [Soziale Funktionen und Zusammenarbeit in SharePoint](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [Folgen von Personen in SharePoint](follow-people-in-sharepoint.md)
    
  
