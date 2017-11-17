---
title: "Neuigkeiten für Entwickler hinsichtlich der thematischen Features und der Zusammenarbeitsfeatures in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 65365b1d-cde5-47cd-8b04-1b76be0e3490
ms.openlocfilehash: e07b0d576b096667251b2aff377593bae634823e
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-for-developers-in-social-and-collaboration-features-in-sharepoint"></a>Neuigkeiten für Entwickler hinsichtlich der thematischen Features und der Zusammenarbeitsfeatures in SharePoint
Informationen Sie zu neuen und geänderten thematische Features und Zusammenarbeitsfeatures für Meine Website und Communitywebsite Entwicklungsszenarien in SharePoint. Thematische Features und Zusammenarbeitsfeatures in SharePoint erleichtern Benutzern kommunizieren und bleiben anderweitig und informiert. Der verbesserte für soziale Netzwerke-Feed für persönliche Websites und Teamwebsites hilft Benutzern bei auf dem neuesten Stand mit den Personen und Inhalten, die sie interessieren. Das neue Feature für Communitywebsite bietet umfassende Community, mit der Benutzer auf einfache Weise suchen und Freigeben von Informationen und Personen mit ähnlichen Interessen finden.
  
    
    

Eine ausführliche Übersicht über die neuen sozialen und Zusammenarbeitsfunktionen in SharePoint finden Sie unter  [Neuigkeiten bei sozialen Netzwerken in SharePoint](http://technet.microsoft.com/en-us/library/jj219766%28v=office.15%29) auf TechNet. Weitere Informationen zum Programmieren mit der Nutzung von sozialen Netzwerken und Zusammenarbeit zur Verfügung finden Sie unter [Soziale Funktionen und Zusammenarbeit in SharePoint](social-and-collaboration-features-in-sharepoint.md).
## <a name="new-and-changed-my-site-features-in-sharepoint"></a>Neue und geänderte Meine Website-Features in SharePoint
<a name="bkmk_Social"> </a>

Die Meine Website - soziale Netzwerke-API, die von Benutzerprofilen und Daten in sozialen Netzwerken umfasst, enthält viele neue und geänderte Features. Neuer Funktionen für Meine Websites und Teamwebsites bietet eine interaktive, gesprochene wünschen in Feeds, die für Benutzer bleiben Sie auf der Personen und Inhalte vereinfacht, die für diese sind.
  
    
    
Auf der Seite **Newsfeed** in SharePoint werden mehrere dieser Verbesserungen angezeigt, darunter auch ein Textfeld, mit dem Benutzer schnell Mikroblogbeiträge veröffentlichen können und ein interaktiver, dialogorientierter Feed für Beiträge und Updates der Personen und Inhalte, denen der Benutzer folgt.
  
    
    

### <a name="new-social-namespace-provides-apis-for-social-feeds-and-following-people-and-content"></a>Ein neuer sozialer Namespace enthält APIs für Feeds in sozialen Netzwerken und zum Folgen von Personen und Inhalten.

Der **Social** -Namespace enthält die primäre-API für die Arbeit mit Feeds und Microblog-Beiträge und für folgende Personen und Inhalte. Weitere Informationen finden Sie unter [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) für den .NET Clientobjektmodell [SP. Soziale](http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx) für JavaScript-Objektmodell und [Microsoft.Office.Server.Social](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.aspx) für das Serverobjektmodell.
  
    
    

> **Hinweis:** Die API im Namespace [Microsoft.Office.Server.ActivityFeed](https://msdn.microsoft.com/library/Microsoft.Office.Server.ActivityFeed.aspx) wird nicht mehr unterstützt. Siehe [Veraltete und entfernte Meine Website-Soziale Netzwerke-API und -Features](#bkmk_DeprecatedAPI) 
  
    
    


### <a name="new-client-apis-for-social-feeds-following-people-and-content-and-user-properties-in-sharepoint"></a>Neue Client-APIs für Feeds in sozialen Netzwerken zum Folgen von Personen und Inhalten und Benutzereigenschaften in SharePoint

SharePoint enthält neuen Client-APIs, die Sie zum Arbeiten mit sozialen Feeds, folgen von Personen und Inhalte und Abrufen von Benutzereigenschaften in online, lokalen und Mobilgeräte-Entwicklung verwenden können. Wenn möglich, sollten Sie die Client-APIs für die Entwicklung von SharePoint statt der Server-Objekt-Objektmodell oder den Webdienst-Dienste verwenden. Client-APIs gehören verwalteten clientobjektmodellen, ein JavaScript-Objektmodell und einen Dienst Representational State Transfer (REST). Wenn Sie eine SharePoint-Add-In entwickeln, müssen Sie eine Client-API verwenden.
  
    
    
Nicht alle serverseitigen-Funktionen in der Assembly Microsoft.Office.Server.UserProfiles ist von Client-APIs zur Verfügung. Es ist beispielsweise keine clientseitige Zugriff auf die API in der  [Microsoft.Office.Server.Audience](https://msdn.microsoft.com/library/Microsoft.Office.Server.Audience.aspx) -Namespace, den Namespace [Microsoft.Office.Server.ReputationModel](https://msdn.microsoft.com/library/Microsoft.Office.Server.ReputationModel.aspx) oder den [Microsoft.Office.Server.SocialData](https://msdn.microsoft.com/library/Microsoft.Office.Server.SocialData.aspx) -Namespace. Die APIs zur Verfügung stehen, finden Sie unter den [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) -Namespace und den [Microsoft.SharePoint.Client.UserProfiles](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx) -Namespace.
  
    
    
Informationen dazu, wie Sie für den Zugriff auf die Meine Website - soziale Netzwerke-Client-APIs finden Sie unter  [Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint](get-started-developing-with-social-features-in-sharepoint.md). Weitere Informationen zu den API-Sätze in SharePoint und wann sie verwendet werden finden Sie unter  [Auswählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md).
  
    
    

### <a name="use-the-profileloadercreatepersonalsiteenqueuebulk-method-to-provision-personal-sites-and-onedrive-for-business-for-multiple-users-my-site-host-administrators-on-sharepoint-online-only"></a>Verwenden Sie die ProfileLoader.CreatePersonalSiteEnqueueBulk-Methode zum Bereitstellen von persönlichen Websites und OneDrive für Unternehmen für mehrere Benutzer (hostadministratoren auf SharePoint Online nurMeine Website )
<a name="bk_CreatePersonalSiteEnqueueBulk"> </a>

Meine Website Host-Administratoren können die **ProfileLoader.CreatePersonalSiteEnqueueBulk** -Methode programmgesteuert persönliche Websites für mehrere Benutzer auf SharePoint Online, bereitgestellt werden sollen, Features wie beispielsweise OneDrive für Unternehmen und der Seite Websites enthalten.
  
    
    
Im folgenden Codebeispiel verwendet das Clientobjektmodell .NET in eine Konsolenanwendung. Fügen Sie bevor Sie das Beispiel auszuführen Verweise auf Microsoft.SharePoint.Client.dll und Microsoft.SharePoint.Client.Runtime.dll aus zu Microsoft.SharePoint.Client.UserProfiles.dll, und ändern Sie die Platzhalterwerte für die Variablen **userName**, **passwordStr**und **serverUrl**. Die **serverUrl** -Variable muss die URL der SharePoint Online-Verwaltungskonsole.
  
    
    

> **Hinweis:** Um den erforderlichen Client-DLLs aufzurufen, laden Sie die  [SharePoint Online-Clientkomponenten- SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038). 
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Security;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.UserProfiles;

namespace CreatePersonalSiteBulkConsole
{
    class Program
    {
        static void Main(string[] args)
        {
            string userName = "administrator@contoso.onmicrosoft.com";
            string passwordStr = "password";
            string serverUrl = "https://contoso-admin.sharepoint.com/";

            using (var clientContext = new ClientContext(serverUrl))
            {
                SecureString password = new SecureString();
                Array.ForEach(passwordStr.ToCharArray(), c => password.AppendChar(c));

                var credentials = new SharePointOnlineCredentials(userName, password);

                clientContext.Credentials = credentials;

                var web = clientContext.Web;
                clientContext.Load(web);
                clientContext.ExecuteQuery();
                ProfileLoader loader = ProfileLoader.GetProfileLoader(clientContext);

                if (loader == null)
                {
                    throw new InvalidOperationException("Failed to get ProfileLoader");
                }

                string[] userEmails = { "usera@contoso.onmicrosoft.com", "userb@contoso.onmicrosoft.com" };
                loader.CreatePersonalSiteEnqueueBulk(userEmails);
                loader.Context.ExecuteQuery();
            }
        }
    }
}
```

Um die **CreatePersonalSiteEnqueueBulk** -Methode mit Windows PowerShell verwenden, ändern Sie zunächst die Platzhalterwerte (die URL der SharePoint Online-Verwaltungskonsole und Benutzernamen) in den folgenden Befehlen, und führen Sie die Befehle in der SharePoint-Verwaltungsshell.
  
    
    



```

$webUrl = "https://yoursharepointadmin.sharepoint.com"
$ctx = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)

$web = $ctx.Web
$username = "admin@myadmin.sharepoint.com"
$password = read-host -AsSecureString

$ctx.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($username,$password)

$ctx.Load($web)
$ctx.ExecuteQuery()

[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SharePoint.Client.UserProfiles")

$loader =[Microsoft.SharePoint.Client.UserProfiles.ProfileLoader]::GetProfileLoader($ctx)

#To get profile
$profile = $loader.GetUserProfile()
$ctx.Load($profile)
$ctx.ExecuteQuery()
$profile 
#To enqueue profile
$loader.CreatePersonalSiteEnqueueBulk(@("user1@domain.com")) 
$loader.Context.ExecuteQuery()
```

Weitere Informationen finden Sie unter  [, damit Sie programmgesteuert persönliche Websites (ein Drive für Unternehmen) in Office 365 bereitstellen möchten?](http://blogs.msdn.com/b/frank_marasco/archive/2014/03/25/so-you-want-to-programmatically-provision-personal-sites-one-drive-for-business-in-office-365.aspx) und [Use Windows PowerShell zum Verwalten von SharePoint](http://technet.microsoft.com/en-us/library/ee806878%28v=office.15%29.aspx).
  
    
    

### <a name="new-objects-for-users-and-user-properties-in-sharepoint"></a>Neue Objekte für Benutzer und Benutzereigenschaften in SharePoint
<a name="bkmk_NewUserObjects"> </a>

SharePoint enthält neue Objekte, die Benutzer und Benutzereigenschaften darstellen:
  
    
    

- Das Objekt [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) stellt Benutzer (und andere Entitäten) für Feed- und die folgenden anderen Aktivitäten dar.
    
  
- Das Objekt [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) enthält allgemeine Benutzereigenschaften und Benutzerprofileigenschaften.
    
  

> **Hinweis:** Serverobjektmodellversionen sind das Objekt [SPSocialActor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActor.aspx) und das Objekt [PersonProperties](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PersonProperties.aspx).
  
    
    

SharePoint umfasst auch ein neues clientseitiges [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx)-Objekt, das Methoden bereitstellt, die Sie zum Erstellen einer persönlichen Website für den aktuellen Benutzer verwenden können. Es enthält jedoch nicht alle Benutzereigenschaften des serverseitigen Objekts [UserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx). Um auf alle Benutzereigenschaften des clientseitigen Codes zuzugreifen, verwenden Sie die Methode [PeopleManager.GetMyProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetMyProperties.aspx) oder [PeopleManager.GetPropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetPropertiesFor.aspx) (Benutzerprofileigenschaften werden in der Eigenschaft [PersonProperties.UserProfileProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx) gespeichert). Sie können auch die Methode [PeopleManager.GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) oder [PeopleManager.GetUserProfilePropertyFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx) verwenden.
  
    
    

### <a name="new-client-side-people-picker-control"></a>Neues clientseitiges Steuerelement "Personenauswahl"
<a name="bkmk_NewUserObjects"> </a>

Das clientseitige Personenauswahl-Steuerelement ist ein HTML- und JavaScript-Steuerelement, das Browserübergreifende Unterstützung für die Auswahl von Personen, Gruppen und Ansprüche bereitstellt. Sie können Konfigurieren der Personenauswahl mit denselben Einstellungen wie die serverseitige Version des Steuerelements, einschließlich der Steuerelement-spezifische Eigenschaften (wie ermöglicht mehrere Benutzer oder Benutzer und Gruppen) und web-Konfigurationseinstellungen auf Anwendungsebene (wie Active Directory-Domänendienste Parameter oder für bestimmte Gesamtstrukturen). Weitere Informationen finden Sie unter  [Verwenden des clientseitigen Steuerelements "Personenauswahl" in von SharePoint gehosteten Share Point-Add-Ins](http://msdn.microsoft.com/library/383f265f-ed44-4d09-b2f6-366f13d52347%28Office.15%29.aspx).
  
    
    

### <a name="deprecated-and-removed-my-site-social-api-and-features"></a>Veraltete und entfernte Meine Website - soziale Netzwerke API und features
<a name="bkmk_DeprecatedAPI"> </a>

Die folgenden Meine Website-Soziale Netzwerke-APIs und Features sind in SharePoint veraltet:
  
    
    

- Die im  [Microsoft.Office.Server.ActivityFeed](https://msdn.microsoft.com/library/Microsoft.Office.Server.ActivityFeed.aspx) -Namespace-API ist veraltet. Der **Social** -Namespace stellt die API für Programmgesteuertes Arbeiten mit sozialen Feeds in SharePoint. Für die Abwärtskompatibilität werden **ActivityEvent** Elemente aus SharePoint 2010 in SharePoint Feeds als Ereignisse angezeigt, die eine Antwort werden nicht möglich. (Legacy-Ereignismigration muss in der Zentraladministration aktiviert sein.)
    
  
- Meine Website RSS-feed (ActivityFeed.aspx) wurde mit neuen APIs in der REST-Dienst, das Clientobjektmodell und das Objektmodell JavaScript ersetzt. Um benutzerdefinierte SharePoint 2010 Code zu migrieren, die diese API (vorzugsweise eine Client-API) verwendet, ersetzen Sie alle Anfragen zu ActivityFeed.aspx durch Aufrufe der neuen API und Handle Speisen Sie Daten, die im JavaScript Object Notation (JSON)-Format zurückgegeben wird.
    
  
- Das Webpart **Letzte Aktivitäten** wird durch das neue Webpart **Newsfeed** ersetzt, das die Multithread-Konversation und das Abrufen eines dynamischen Feeds unterstützt.
    
    > **Hinweis:** Die Anpassung des Newsfeed-Webparts oder anderer Feed-Webparts (wie z. B. das Website-Feed-Webpart auf einer Teamwebsite) wird nicht unterstützt. Wenn Sie diese Webparts zum Beispiel durch JavaScript-Außerkraftsetzungen ändern, können diese Anpassungen bei SharePoint-Updates beschädigt werden. 
- Das Webpart **Kommentare in sozialen Netzwerken** ist veraltet.
    
  
- Die folgenden Aktivitätsereignisse informieren nicht mehr automatisch den Feed: profile Update, anstehende gehören Geburtstage, anstehende Jahrestag im Unternehmen, neue Mitgliedschaft und Ändern des Managers. Sie können jedoch auch benutzerdefinierte Ereignisempfänger für das Rollout erstellen. Keine neuen Ereignisse für soziale Netzwerke wurden hinzugefügt.
    
  
- Die folgenden Felder in der  [Privacy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.Privacy.aspx) -Enumeration sind veraltet: **Contacts**, **Organization**und **Manager**. SharePoint bietet nur **Private** ( **Privat** ) und **Public** datenschutzeinstellungen ( **Alle** ). Vorhandene datenschutzeinstellungen werden beibehalten, bis sie vom Benutzer geändert werden. Um benutzerdefinierte SharePoint 2010 Code zu migrieren, die diese API verwendet, ersetzen Sie alle Verweise auf die veraltete Privacy-Felder.
    
  
- Die **Folgenden Personen** API, die über die **SocialFollowingManager** erfolgt ersetzt die Funktionalität **Kollegen** aus SharePoint Server 2010. Die Seite **Kollegen** wird mit der Seite **Personen, die ich Folge** ersetzt. Das Feature für **Gruppen**, die Benutzern von Kollegen in Gruppen organisieren aktiviert ist nicht mehr verfügbar.
    
  
- Organisationsprofile in SharePoint veraltet sind, und die folgenden Typen sind veraltet: **OrganizationProfile**, **OrganizationProfileManager**, **OrganizationMembershipType**, **OrganizationNotFoundException**, **OrganizationProfileChange**, **OrganizationProfileChangeQuery**, **OrganizationProfileMembershipChange**und **OrganizationProfileValueCollection**.
    
  
- Das Feature **Meine Hyperlinks** ist in SharePoint veraltet.
    
  

## <a name="new-community-site-feature-in-sharepoint"></a>Neues Feature für die Community-Website in SharePoint
<a name="bkmk_Collab"> </a>

Das neue Feature für Communitywebsite enthält eine neue Websitevorlage und Diskussion Erfahrung verbessert. Features finden wie Ruf, Kategorien, empfohlener Diskussionen, eine Frage-Post-Typ und beste Antworten Communitymitglieder einfach per Sie beliebte Diskussionen, relevante Informationen und Personen mit ähnlichen Interessen. Mitglieder erstellen Reputation, wie sie Communitys teilnehmen.
  
    
    
Das Feature Communitywebsite macht eine bestimmte API für die Entwicklung nicht verfügbar. Um Communitywebsite Features zu erweitern, verwenden Sie SharePoint-Website und Liste APIs direkt. Beispielsweise können Sie SharePoint-APIs zum Anpassen der Website- und Listenvorlagen, erstellen Sie benutzerdefinierte Aktivitäten von Communitys für den Feed für soziale Netzwerke, Reputation Informationen in den Suchergebnissen integrieren, Details des Modells Reputation anpassen oder Erstellen von Workflows an Diskussionen moderieren.
  
    
    
Die folgende Liste enthält Informationen zum Entwickeln mit Communitywebsite Features:
  
    
    

- Community-Websites verwenden Sie die Websitevorlage **Community** ( [Id](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WebTemplate.Id.aspx) = **62**). Die Websitevorlage ist nicht verfügbar für Öffentliche Websites. Der Vorlage die Pinnwand Diskussionsliste ist  [DiscussionBoard](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ListTemplateType.DiscussionBoard.aspx) (Wert = **108**).
    
  
- Aktivieren des Features **Communitywebsite** aktiviert den Ereignisempfänger **CommunityEventReceiver**.
    
  
- Zum Anpassen der Client-seitigen gerenderte Listenansicht müssen Sie JavaScript Außerkraftsetzungen verwenden, um die Ansicht zu ersetzen. Listenansichten können nicht über die API SharePoint erweitert werden. Weitere Informationen finden Sie unter  [Anpassen einer Listenansicht in Add-Ins für SharePoint durch clientseitiges Rendering](http://msdn.microsoft.com/library/8d5cabb2-70d0-46a0-bfe0-9e21f8d67d86%28Office.15%29.aspx).
    
  
- Community-Websites verwenden asynchrone Ereignisse, um Objekte zu aktualisieren. Wenn asynchrone Ereignisse im Hintergrund ausgeführt werden soll, können, wenn Sie versuchen, Listen oder Listenelementen aktualisieren und Ihre Handle für das Objekt möglicherweise veraltet  *Speichern*  Konflikte auftreten.
    
    Um dieses Problem zu umgehen Ausnahmen behandeln, die von der **Update** -Aufrufe zurückgegeben werden aktualisieren Sie die Instanz vor wiederholen Sie den Anruf, und für mehrere Wiederholungsversuche Schleife wie im folgenden Codebeispiel dargestellt.
    


```cs
  
int retries = 1;
while (retries <= 10)
{
    try
    {
        spListItem.IconOverlay = urlString;
        spListItem.Update();
        break;
    }
    catch (SPException saveConflict)
    {
        spListItem = web.Lists.GetItemById(spListItem.ID);
        retries++;
        if (retries > 10) throw;
        System.Threading.Thread.Sleep(1000);
    }
}

```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15NewSocial_addlresources"> </a>


-  [Soziale Funktionen und Zusammenarbeit in SharePoint](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [Neuerungen für Entwickler in SharePoint](what-s-new-for-developers-in-sharepoint.md)
    
  
-  
  [Was ist neu in sozialen Netzwerken in SharePoint](http://technet.microsoft.com/en-us/library/jj219766%28v=office.15%29)
    
  

