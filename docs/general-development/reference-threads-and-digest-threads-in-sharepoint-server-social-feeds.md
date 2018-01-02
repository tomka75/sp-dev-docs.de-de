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
# <a name="reference-threads-and-digest-threads-in-sharepoint-social-feeds"></a>Verweisthreads und Digestthreads in sozialen SharePoint-Feeds
In diesem Artikel werden die Threadtypen Verweisthread und Digestthread beschrieben. Sie können in den Threadsammlungen enthalten sein, die soziale Feeds in SharePoint bilden.
Wenn Sie einen sozialen Feed abrufen, gibt SharePoint ein Objekt des Typs [SocialFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeed.aspx) zurück. Dieses Objekt enthält die Sammlung von Objekten des Typs [SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx), die den Feed bilden. Diese Threads können Unterhaltungen, einzelne Mikroblogbeiträge oder Benachrichtigungen darstellen, einschließlich Ereignissen und Verweisthreads. Threads, die Unterhaltungen darstellen, werden vom Server möglicherweise als Digestthreads zurückgegeben.
  
> [!NOTE]
> Die API, auf die in diesem Artikel Bezug genommen wird, stammt aus dem .NET-Clientobjektmodell. Die entsprechenden Objekte in anderen APIs können anders angelegt sein. Links zu anderen themenverwandten APIs finden Sie unter [Zusätzliche Ressourcen](#bk_addresources).
  
    
    


## <a name="what-are-reference-threads-in-sharepoint-social-feeds"></a>Was sind Verweisthreads in sozialen SharePoint-Feeds?
<a name="bk_whatAreRefThreads"> </a>

Wenn ein Benutzer einen Beitrag likt, jemanden in einem Beitrag erwähnt, auf einen Beitrag antwortet oder ein Tag in einen Beitrag einfügt, erzeugt SharePoint einen Verweisthread. Ein Verweisthread verfügt über zwei Eigenschaften, über die Sie Informationen zu dem Verweisthread oder dem Beitrag abrufen: [ThreadType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.ThreadType.aspx) und [PostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.PostReference.aspx).
  
    
    
Verweisthreads lassen sich anhand ihrer Eigenschaft [ThreadType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.ThreadType.aspx) identifizieren. Sie kann einen der in Tabelle 1 aufgeführten Werte zurückgeben.
  
    
    

**In Tabelle 1. Typen von Verweis thread**


|**Verweistyp**|**Beschreibung**|
|:-----|:-----|
| [LikeReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.LikeReference.aspx) **** <br/> |Ein Verweis auf einen Beitrag, den ein Benutzer "gefällt mir".  <br/> |
| [MentionReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.MentionReference.aspx) <br/> |Ein Verweis auf einen Beitrag, der einen Benutzer erwähnt.  <br/> |
| [ReplyReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.ReplyReference.aspx) <br/> |Ein Verweis auf eine Antwort.  <br/> |
| [TagReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.TagReference.aspx) <br/> |Ein Verweis auf ein Beitrag, der ein Tag enthält.  <br/> |
| [Normal](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.Normal.aspx) <br/> |Ein Verweis-Thread.  <br/> |
   
Die  [PostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.PostReference.aspx) -Eigenschaft gibt ein [SocialPostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostReference.aspx) -Objekt, das Informationen über den Thread enthält, die das Ereignis ausgelöst hat. Mindestens enthält sie die ID des Quellthreads, die Sie dann mit der [SocialFeedManager.GetFullThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFullThread.aspx) -Methode verwenden können, den Thread abrufen, wenn es noch vorhanden ist.
  
    
    
 [SocialPostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostReference.aspx) kann auch eine Kopie der Quelle Beitrag oder Thread enthalten. Diese Verfügbarkeit hängt davon ab, die Feedtyp sowie die Threadtyp und die Einschränkung aus Sicherheitsgründen. Enthält die Referenz einen Beitrag oder Thread, diese Objekte stellen Momentaufnahmen des Post oder Threads zum Zeitpunkt des Ereignisses dar.
  
    
    
Nicht alle feedbezogene Aktivitäten werden in den Feed als Referenz Threads gebucht. Beispielsweise sind folgende Benachrichtigungen (beispielsweise wenn eine Person nach einem Standort gestartet wird) nicht Verweis Threads.
  
> [!NOTE]
> SharePoint führt für Inhalte in automatisch generierten Beiträgen automatisch Sicherheitskürzungen durch. Gleiches gilt für Websitezugriffe in allen Beiträgen, die auf einen Websitefeed verweisen. Mithilfe des Attributs **SecurityUris** können Sie die Sicherheitskürzung jedoch auch auf jeden beliebigen anderen Beitrag anwenden. Dazu müssen Sie lediglich die URL des Beitrags angeben. Benutzer, die keinen Zugriff auf die URL haben, erhalten den Beitrag nicht.
  
    
    

Antwort-, Like- und Erwähnungsverweise werden unbefristet im persönlichen Feed des Benutzers gespeichert. Tagverweise werden im verteilten Cache gespeichert, also nur vorübergehend. Weitere Informationen zur Zwischenspeicherung finden Sie unter [Übersicht über Mikrobloggingfeatures, Feeds und den verteilten Cachedienst in SharePoint](http://technet.microsoft.com/de-DE/library/jj219700%28v=office.15%29.aspx#cache).
  
    
    

## <a name="what-are-digest-threads-in-sharepoint-social-feeds"></a>Was sind Digestthreads in sozialen SharePoint-Feeds?
<a name="bk_whatAreDigests"> </a>

Ein Digest-Thread stellt eine kompakte Version einer Unterhaltung - enthält des Threads Stamm Post und zwei neuesten Antworten. Sie können einen Digest-Thread identifizieren, indem Sie überprüfen, ob der Thread das  [IsDigest](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadAttributes.IsDigest.aspx) -Attribut in der [Attributes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.Attributes.aspx) -Eigenschaft angewendet. Um herauszufinden, ob ein Thread mehr als zwei Threads hat, überprüfen Sie die [TotalReplyCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.TotalReplyCount.aspx) -Eigenschaft.
  
    
    
Zum Optimieren der Leistung, wenn ein Thread mehr als zwei Antworten enthält, gibt der Server einen Digest-Thread zurück. Wenn Sie alle Antworten für einen Thread abrufen möchten, rufen Sie die  [SocialFeedManager.GetFullThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFullThread.aspx) -Methode, und übergeben Sie die Thread-ID
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Arbeiten mit sozialen Feeds in SharePoint](work-with-social-feeds-in-sharepoint.md)
    
  
-  [SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) im .NET Client-Objektmodell
    
  
-  [SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx) im JavaScript-Objektmodell
    
  
-  [SPSocialThread](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialThread.aspx) im Server-Objektmodell
    
  

