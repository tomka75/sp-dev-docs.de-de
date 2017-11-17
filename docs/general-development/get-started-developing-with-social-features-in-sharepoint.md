---
title: Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8852ce36-8309-45a7-a141-2e10ac17a123
ms.openlocfilehash: 9566ab4fde6513c7a22e537bac66a6880ded981a
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="get-started-developing-with-social-features-in-sharepoint"></a>Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint
Erste Schritte zum Programmieren mit sozialen Feeds von SharePoint und Mikroblogeinträgen, Folgen von Personen und Inhalten (Dokumente, Websites und Tags) und Arbeiten mit Benutzerprofilen.

    
 [Wie kann ich in sozialen Netzwerken Apps und Lösungen verwenden?](get-started-developing-with-social-features-in-sharepoint.md#bk_HowToUseSocialFeatures)
  
    
    
 [Einrichten der Entwicklungsumgebung](get-started-developing-with-social-features-in-sharepoint.md#DevEnvironment)
  
    
    
 [Entwicklungsszenarien für Features für soziale Netzwerke](get-started-developing-with-social-features-in-sharepoint.md#DevScenarios)
  
    
    
 [Vorgehensweisen für die Programmierung mit Features für soziale Netzwerke](get-started-developing-with-social-features-in-sharepoint.md#bk_GetStarted)
  
    
    
 [APIs für die Programmierung mit Features für soziale Netzwerke](get-started-developing-with-social-features-in-sharepoint.md#SocialApis)
  
    
    
 [App-Berechtigungsanforderungen für den Zugriff auf Features für soziale Netzwerke](get-started-developing-with-social-features-in-sharepoint.md#bkmk_AppPerms)
  
    
    
 [Weitere Ressourcen](get-started-developing-with-social-features-in-sharepoint.md#bk_AddResources)
  
    
    


## <a name="how-can-i-use-social-features-in-sharepoint-apps-and-solutions"></a>Wie kann ich Features für soziale Netzwerke in SharePoint apps und -Lösungen verwenden?
<a name="bk_HowToUseSocialFeatures"> </a>

Features für soziale Netzwerke in SharePoint apps und -Lösungen können Benutzer eine Verbindung herstellen, für die Kommunikation und Zusammenarbeit miteinander und finden, nachverfolgen und wichtige Inhalte und Informationen freigeben verbessern. Sie können neue Features für soziale Netzwerke hinzufügen oder erweitern die Funktionen, die bereits in SharePoint verfügbar sind. Beispielsweise können Sie eine app erstellen, mit die Sie suchen und führen Sie die Personen, die ein gemeinsames Interesse haben, erstellen Sie eine benutzerdefinierte Visualisierung der feed-Daten oder benutzerdefinierte Aktivitäten Sie den Feed veröffentlichen können.
  
    
    
In diesem Artikel beschriebenen Features Ausrichten der Personen, Feeds und folgende Funktionalität, die auf persönliche Websites und Teamwebsites hilfreich. Das Forum Erfahrungen und Reputation Modell auf Community-Websites nicht verfügbar machen eine bestimmte API, sodass Sie mit SharePoint-Website und Liste APIs direkt an um die Funktionalität zu erweitern. Weitere Informationen finden Sie unter  [neue Community-Website-Feature](what-s-new-for-developers-in-social-and-collaboration-features-in-sharepoint-201.md#bkmk_Collab).
  
    
    
Bevor Sie mit der Entwicklung beginnen, sollten Sie wissen, wo der Code ausgeführt wird, in welcher SharePoint-Umgebung er ausgeführt wird und welche Funktionen er bereitstellen soll. Diese Faktoren helfen Ihnen zu entscheiden, welche Art von App Sie erstellen und welche API oder APIs Sie verwenden. Weitere Informationen, die Ihnen bei der Entscheidungsfindung helfen können, finden Sie unter [Wählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md) und [SharePoint-Add-Ins im Vergleich zu SharePoint-Lösungen](sharepoint-add-ins-compared-with-sharepoint-solutions.md).
  
    
    

### <a name="setting-up-your-development-environment"></a>Einrichten der Entwicklungsumgebung
<a name="DevEnvironment"> </a>

Voraussetzungen für die Entwicklung von Features für soziale Medien:
  
    
    

- SharePoint oder SharePoint Online
    
- Visual Studio 2012 oder Visual Studio 2013 mit Office Developer Tools für Visual Studio 2013 oder höher
  

  
Weitere Anleitungen finden Sie unter  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md) und [Features für soziale Netzwerke in SharePoint konfigurieren](http://technet.microsoft.com/en-us/library/fp161267%28v=office.15%29.aspx).
  
    
    

### <a name="development-scenarios-for-social-features-in-sharepoint"></a>Entwicklungsszenarien für Features für soziale Netzwerke in SharePoint
<a name="DevScenarios"> </a>

Allgemeine Entwicklungsszenarien für Features für soziale Netzwerke zählen arbeiten mit sozialen Feeds, folgen von Personen und Inhalte (Dokumente, Websites und Tags) und Arbeiten mit Benutzereigenschaften. Tabelle 1 enthält Links zu Artikeln, in denen die primären APIs beschrieben, mit denen Sie Zugriff auf Funktionen für jedes Szenario und allgemeine Programmieraufgaben.
  
    
    
Die folgenden Artikel beschreiben die primäre APIs und Programmieraufgaben für die Entwicklungsszenario:
  
    
    

-  [Arbeiten mit sozialen Feeds in SharePoint](work-with-social-feeds-in-sharepoint.md)
    
  
-  [Folgen von Personen in SharePoint](follow-people-in-sharepoint.md)
    
  
-  [Folgen von Inhalten in SharePoint](follow-content-in-sharepoint.md)
    
  
-  [Arbeiten mit Benutzerprofilen in SharePoint](work-with-user-profiles-in-sharepoint.md)
    
  

### <a name="how-tos-for-programming-with-social-features-in-sharepoint"></a>Vorgehensweisen für die Programmierung mit Features für soziale Netzwerke in SharePoint
<a name="bk_GetStarted"> </a>

Nachdem Sie Ihre Entwicklungsumgebung einrichten, und wählen Sie das Szenario, Sie können ersten Schritte beim Programmieren mit Features für soziale Netzwerke. Tabelle 1 enthält Links zu Artikeln, die zeigen, wie Sie einfache Programmieraufgaben mit Features für soziale Netzwerke.
  
    
    

**In Tabelle 1. Artikel mit Anleitungen für die Entwicklung mit thematischen features**


|**Funktionsbereich**|**Beschreibung**|
|:-----|:-----|
| [Vorgehensweise: Lesen und schreiben für soziale Netzwerke-Feed mithilfe des clientobjektmodells .NET SharePoint lernen](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-net-client-object.md)|Ausführliche Schritte zum Erstellen einer Anwendung, die Lese- und Schreibvorgänge auf den Feed für soziale Netzwerke mithilfe des Clientobjektmodells .NET durchgehen.|
| [Vorgehensweise: Lesen und Schreiben der sozialen Feed mithilfe des REST-Diensts in SharePoint](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)|Ausführliche Schritte zum Erstellen einer Anwendung, die Lese- und Schreibvorgänge auf den Feed für soziale Netzwerke mithilfe des REST-Diensts durchgehen.|
| [Vorgehensweise: Erstellen und Löschen von Beiträge und Abrufen des für soziale Netzwerke-Feed mithilfe des clientobjektmodells .NET SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md)|Informationen zum Erstellen und Löschen von und Beiträge Microblog und Abrufen von sozialen Feeds mithilfe des Clientobjektmodells .NET.|
| [Vorgehensweise: Erstellen und Löschen von Beiträgen und sozialen Feed abrufen, indem Sie mit der JavaScript-Objektmodell in SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md)|In diesem Artikel erfahren Sie, wie Sie mithilfe des JavaScript-Objektmodells Beiträge erstellen, löschen und mikrobloggen sowie soziale Feeds abrufen können.|
| [Vorgehensweise: Einschließen von Erwähnungen, Tags und Links zu Websites und Dokumenten in Beiträgen in SharePoint](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md)|In diesem Artikel erfahren Sie, wie Sie Mikroblogbeiträgen  **SocialDataItem**-Objekte hinzufügen, die als Erwähnungen, Tags und Links in sozialen Feeds gerendert werden.|
| [Vorgehensweise: Einbetten von Bildern, Videos und Dokumenten in Beiträgen in SharePoint](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md)|In diesem Artikel erfahren Sie, wie Sie Mikroblogbeiträgen **SocialAttachment**-Objekte hinzufügen, die als eingebettete Bilder, Videos und Dokumente in sozialen Feeds gerendert werden.|
| [Vorgehensweise: führen Sie die Personen mithilfe des clientobjektmodells .NET SharePoint](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md)|Erfahren Sie, wie in der folgenden personenfeatures mithilfe des Clientobjektmodells .NET entwickelt.|
| [Vorgehensweise: folgen Sie Menschen mit der JavaScript-Objektmodell in SharePoint](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md)|Erfahren Sie, wie in der folgenden personenfeatures mithilfe des Objektmodells JavaScript entwickelt.|
| [Vorgehensweise: Führen Sie Dokumente und Websites mit .NET Client-Objektmodell in SharePoint](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)|Erfahren Sie, wie in der folgenden Inhaltsfunktionen mithilfe des Clientobjektmodells .NET entwickelt.|
| [Vorgehensweise: führen Sie Dokumente, Websites und Tags mithilfe des REST-Diensts in SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)|Erfahren Sie, wie in der folgenden Inhaltsfunktionen entwickelt, mithilfe des REST-Diensts.|
| [Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des .NET-Clientobjektmodells in SharePoint](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md)|Informationen Sie zum Abrufen von Benutzerprofileigenschaften mithilfe des Clientobjektmodells .NET.|
| [Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des JavaScript-Objektmodells in SharePoint](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md)|Informationen Sie zum Abrufen von Benutzerprofileigenschaften mithilfe der JavaScript-Objektmodells.|
| [Vorgehensweise: Arbeiten mit Benutzerprofilen und Organisationsprofilen mithilfe des Serverobjektmodells in SharePoint](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)|Informationen Sie zum Erstellen, abrufen und Verwalten von Benutzerprofilen und Eigenschaften mithilfe des Serverobjektmodells.|
   

### <a name="apis-for-programming-with-sharepoint-social-features"></a>APIs für die Programmierung mit SharePoint Features für soziale Netzwerke
<a name="SocialApis"> </a>

Zwar apps und -Lösungen SharePoint unterschiedlich zugreifen, nachdem Sie SharePoint zugreifen verwenden die APIs für soziale Netzwerke im Wesentlichen die gleiche Weise. In Tabelle 2 sind die APIs für die Programmierung mit der Feed profiles Folgendes und Benutzer Features in SharePoint und die Pfade auf die Quelldateien auf dem Server.
  
    
    

**In Tabelle 2. APIs für die Programmierung mit Features für soziale Netzwerke**


|**API-Name**|**Quell- und Pfad**|
|:-----|:-----|
| [.NET-Clientobjektmodell](http://msdn.microsoft.com/library/9cc3f70c-78ac-4d2d-b46e-77522ee5d937%28Office.15%29.aspx)|Microsoft.SharePoint.Client.UserProfiles.dll<br/>im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI|
|Silverlight-Clientobjektmodell|Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll<br/>im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin|
|Mobiles Clientobjektmodell|Microsoft.SharePoint.Client.UserProfiles.Phone.dll<br/>im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin|
| [JavaScript-Objektmodell](http://msdn.microsoft.com/library/95cb5427-8514-4e9a-8eee-7ed4b82ec01b%28Office.15%29.aspx)|SP.UserProfiles.js<br/>im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS|
|REST (Representational State Transfer)-Dienst| [`http://<site url>/_api/social.feed`](social-feed-rest-api-reference-for-sharepoint.md)<br/>[`http://<site url>/_api/social.following`](following-people-and-content-rest-api-reference-for-sharepoint.md)<br/>[`http://<site url>/_api/SP.UserProfiles.PeopleManager`](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx.md#bk_PeopleManager)|
| [Serverobjektmodell](http://msdn.microsoft.com/library/87c5118c-ac0e-4bd9-a75f-7452a9eb0e41%28Office.15%29.aspx)|Microsoft.Office.Server.UserProfiles.dll<br/>im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI|
   

> **Hinweis:** Nicht alle serverseitigen Funktionen im Assembly Microsoft.Office.Server.UserProfiles sind in den Client-APIs verfügbar. Im Namespace [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) und im Namespace [Microsoft.SharePoint.Client.UserProfiles](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx) erfahren Sie, welche APIs verfügbar sind.
  
    
    


## <a name="app-permission-requests-for-accessing-social-features-in-sharepoint-add-ins"></a>App-Berechtigungsanforderungen für den Zugriff auf Features für soziale Netzwerke in SharePoint-Add-Ins
<a name="bkmk_AppPerms"> </a>

Eine SharePoint-Add-In muss die für den Zugriff auf SharePoint-Ressourcen benötigte Berechtigung bei dem Benutzer anfordern, der die Installation vornimmt. Beispielsweise muss eine App, die im Feed Beiträge veröffentlicht, (mindestens) die **Schreibberechtigung** beim Feed anfragen. Geben Sie die Berechtigungen, die Ihre App benötigt, in der AppManifest.xml-Datei in Visual Studio an.
  
    
    
App-Berechtigungsanforderungen sind auf der SharePoint-Bereitstellung im Querformat beschränkt. Tabelle 3 zeigt die Bereichsnamen (mit den entsprechenden Bereich URIs) und die verfügbaren Rechte für den Zugriff auf Features für soziale Netzwerke. Weitere Informationen finden Sie unter  [Add-In-Berechtigungen in SharePoint](http://msdn.microsoft.com/library/5f7a8440-3c09-4cf8-83ec-c236bfa2d6c4%28Office.15%29.aspx),  [Add-In-Autorisierungsrichtlinientypen in SharePoint](http://msdn.microsoft.com/library/124879c7-a746-4c10-96a7-da76ad5327f0%28Office.15%29.aspx)und  [Planen der app-Berechtigungsverwaltung in SharePoint](http://technet.microsoft.com/en-us/library/jj219576%28office.15%29.aspx).
  
    
    

**Tabelle 3. App-Berechtigungsbereiche und verfügbare Rechte für Features für soziale Netzwerke in SharePoint**


|**Bereichsname**|**Beschreibung**|**Verfügbare Rechte**|
|:-----|:-----|:-----|
|Benutzerprofile<br/>`http://sharepoint/social/tenant`|Den berechtigungsanforderungsbereich verwendet, um alle Benutzerprofile zugreifen. Nur das Benutzerprofildienst-Bild kann geändert werden. alle anderen Benutzerprofileigenschaften sind für SharePoint-Add-Ins schreibgeschützt. Muss von einem mandantenadministrator installiert werden.|Read, Write, Manage, FullControl|
|Core<br/>`http://sharepoint/social/core`|Der berechtigungsanforderungsbereich für den Zugriff des Benutzers auf beobachteten Inhalte und einem freigegebenen Metadaten, die von mikroblogging Features verwendet wird. In diesem Bereich gilt nur für persönliche Websites, die nach Inhalten zu unterstützen. Wenn die app auf eine andere Art von Website installiert wurde, verwenden Sie die mandantenbereich.|Read, Write, Manage, FullControl|
|Newsfeed<br/>`http://sharepoint/social/microfeed`|Den berechtigungsanforderungsbereich des Benutzers Feed oder den Feed Team Zugriff auf verwendet. In diesem Bereich gilt für persönliche Websites, die mikroblogging unterstützen oder Teamwebsites, in dem das **Website-Feed**-Feature aktiviert ist. Wenn die app auf eine andere Art von Website installiert wurde, verwenden Sie die mandantenbereich.|Read, Write, Manage, FullControl|
| `http://sharepoint/social/trimming`|In diesem berechtigungsanforderungsbereich verwendet, um festzustellen, ob Sicherheit verkürzt Inhalte in den Feed für soziale Netzwerke für apps anzuzeigen. Wenn diese Berechtigung hoher Vertrauenswürdigkeit nicht gewährt wurde, wird bestimmter Inhalte (wie Aktivitäten zu Dokumenten und Websites, denen die app zum berechtigt nicht) abgeschnitten aus der feed-Daten, die an die app zurückgegeben werden, auch wenn der Benutzer über ausreichende Berechtigungen verfügt. Diese Berechtigung muss die app-manifest-Datei manuell hinzugefügt werden.|Read, Write, Manage, FullControl|
   

### <a name="what-youll-need-to-consider-when-requesting-app-permissions"></a>Was Sie benötigen, bei der app-Berechtigungen anfordern

Beachten Sie die folgenden Überlegungen beim app-Berechtigungen für Features für soziale Netzwerke angeben:
  
    
    

- Apps, die angeben, **FullControl** Rechte sind für Office Store apps nicht zulässig. Nur **Read**, **Write**und **Manage** Rechte sind für Office Store apps zulässig.
    
  
- Sie können Berechtigungen für Feeds und die folgenden Features mithilfe von Core, Newsfeed und Mandant ( `http://sharepoint/content/tenant`) Bereiche angeben. Die mandantenbereich stellt die gesamte Instanz, in eine app, einschließlich der Kern und Newsfeed Bereiche installiert ist. Wenn Ihre app bereits die Rechte, die auf Standortebene Mandanten erforderlich sind angibt, klicken Sie dann Sie müssen nicht auf Standortebene Core oder Newsfeed Berechtigungen anzufordern.
    
  
- Während der Entwicklung der mandantenbereich verwenden, wenn Sie erhalten eine "SocialListNotFound: die Liste für soziale Netzwerke in Ihrer persönlichen Website nicht vorhanden" oder "Datei nicht gefunden" angezeigt. Wenn Sie den Bereich Core oder Newsfeed in Ihrer app verwenden möchten, können Sie die Berechtigungen testen, indem Sie die app aus dem app-Katalog öffnen.
    
  
- Der Bereich Core gilt für persönliche Websites, die nach Inhalten zu unterstützen. Der Bereich Newsfeed gilt für persönliche Websites, die mikroblogging unterstützen oder Teamwebsites, in dem das **Website-Feed**-Feature aktiviert ist. Wenn die app auf eine andere Art von Website installiert werden sollen, müssen Sie die mandantenbereich verwenden. Finden Sie unter  [Mandantschaften und Bereitstellungsbereiche von Add-Ins für SharePoint](http://msdn.microsoft.com/library/1ceb3142-a7a5-453e-920f-5f953a79401a%28Office.15%29.aspx).
    
  
- Apps, die zur Anforderung von Rechten für den Bereich von Benutzerprofilen müssen von einem mandantenadministrator installiert sein, und sie können nicht in Office 365 Small Business Premium-Version von SharePoint Online installiert werden.
    
  
- Wenn Lizenzierung oder ein Feature Aktivierung für Features für soziale Netzwerke und mikroblogs nicht erfüllt sind, erhalten die Benutzer eine Meldung angezeigt, dass die app installiert werden kann.
    
  
- Apps, die außerhalb von SharePoint gestartet werden können Berechtigung auf spontane (mit Ausnahme von **Full Control**) anfordern. Weitere Informationen finden Sie unter  [OAuth-Ablauf mit Authentifizierungscode für SharePoint-Add-Ins](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_AddResources"> </a>

 **Konzeptionelle Artikel**
  
    
    

-  [Soziale Funktionen und Zusammenarbeit in SharePoint](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [Neuigkeiten für Entwickler hinsichtlich der thematischen Features und der Zusammenarbeitsfeatures in SharePoint](what-s-new-for-developers-in-social-and-collaboration-features-in-sharepoint-201.md)
    
  
-  
  [Soziale Netzwerke und Zusammenarbeit in SharePoint Server](http://technet.microsoft.com/en-us/library/ee662531%28v=office.15%29)
    
  
-  
  [Features für soziale Netzwerke in SharePoint konfigurieren](http://technet.microsoft.com/en-us/library/fp161267%28v=office.15%29.aspx)
    
  
-  
  [Terminologie und Konzepte sozialer Netzwerke in SharePoint](http://technet.microsoft.com/en-us/library/jj219804%28v=office.15%29.aspx)
    
  
 **Referenzdokumentation**
  
    
    

-  [Clientklassenbibliothek für Funktionen und Daten für das soziale Netzwerk](http://msdn.microsoft.com/library/9cc3f70c-78ac-4d2d-b46e-77522ee5d937%28Office.15%29.aspx)
    
  
-  [SP. UserProfiles.js JavaScript-Referenz](http://msdn.microsoft.com/library/80cf5436-6aa2-6f11-a782-66a04f6e2fb0%28Office.15%29.aspx)
    
  
-  [REST-API-Referenz für sozialen Feed für SharePoint](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [REST-API-Referenz zum Folgen von Personen und Inhalten für SharePoint](following-people-and-content-rest-api-reference-for-sharepoint.md)
    
  
-  [Benutzerprofile - REST-API-Referenz](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)
    
  
-  [Serverklassenbibliothek für Funktionen und Daten für das soziale Netzwerk für SharePoint](http://msdn.microsoft.com/library/87c5118c-ac0e-4bd9-a75f-7452a9eb0e41%28Office.15%29.aspx)
    
  
