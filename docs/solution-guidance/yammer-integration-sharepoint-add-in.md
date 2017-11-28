---
title: Yammer-Integration in die SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: a83623a32b398ae32ce7cebc7ac5d37c823a2e3f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="yammer-integration-in-the-sharepoint-add-in-model"></a>Yammer-Integration in die SharePoint-add-in-Objektmodell
=================================================

<a name="summary"></a>Summary
-------

Der gewählten Ansatz zum Integrieren von Yammer mit SharePoint ist in das neue SharePoint-Add-in-Modell identisch mit vollständigen vertrauen Code unverändert.

<a name="high-level-guidelines"></a>Hohe Stufe Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden high Level Richtlinien zum Integrieren von Yammer mit SharePoint enthalten.

- Yammer-Integration in lokalen und Office 365 SharePoint-Umgebungen verwendet werden kann.
- Das remote provisioning Muster können zum Erstellen von Yammer-Gruppen und/oder OpenGraph Yammer-Objekte, um Unterhaltungen zu erleichtern, wenn Sie neue SharePoint-Websites erstellen.
- Sie können die Out-of-the-Box einbetten Funktionalität, um schnell und einfach zu Yammer mit SharePoint integrieren.
    + Zum Einbetten verwenden Sie benötigen Sie eine HTML-Container 400 Pixel oder größer in der Anwendung.
- Die Yammer-SDKs und REST-APIs können Sie benutzerdefinierte Integration-Funktionalität erstellen.

<a name="options-to-integrate-yammer-with-sharepoint"></a>Optionen zum Integrieren von Yammer mit SharePoint
-------------------------------------------

Sie müssen einige Optionen zum Integrieren von Yammer mit SharePoint.

- Einbinden
    + Gruppe, Thema My, und Benutzer Feeds
    + OpenGraph-Feeds
- Yammer-OpenGraph API und/oder Yammer-REST-API mit Yammer SDKs
    
<a name="embed"></a>Einbinden
-----

Bei dieser Option betten Sie einen Yammer-Feeds in einer SharePoint-Webseite.
    
- Diese Option ist schnell und einfach implementiert.
- Diese Option können Sie steuern, beschränkt Aspekte des Feeds und wie es angezeigt wird.

Sieht folgendermaßen aus Ihrer SharePoint-Seite einbetten verwenden:

![Eine standard SharePoint Seite der Teamwebsite mit einem Textfeld mit dem Text, eine Unterhaltung beginnen. Unterhalb des Texts wird im Feld ein Listenfeld eine Yammer Unterhaltungsthreads anzeigen.](media/Recipes/Yammer/YammerEmbed.png)

In der folgenden Tabelle wird beschrieben, jede Art von Yammer können Sie mit zugreifen Feed Out-of-Box einbetten.

Feed | Beschreibung | FeedType | Anwendungsfall
---- | ----------- | -------- | --------
Mein Newsfeed | Meine Feeds sind, in dem Unterhaltungen für Yammer-Benutzer übermittelt werden. | MyFeed | Meine Website-Homepage oder einen Arbeitsbereich-Website.
Benutzer-Feed | Alle Unterhaltungen von einem bestimmten Benutzer in Yammer veröffentlicht. | Benutzer | Profilseiten für Benutzer in ein Verzeichnis des Systems.
Thema-Feed | Ein Feed der Unterhaltungen an, die mit einem Thema in Yammer markiert wurden. | Thema | Die Seite ein Ereignis in einem Intranet.
Gruppenfeed | Ein Feed der Unterhaltungen an, die in einer angegebenen Gruppe gebucht wurden. | Gruppe | Eine Seite Team in einem Intranet.

Wenn Sie die Funktionen des Out-of-Box-Yammer-Feeds in der Tabelle oben hinausgehen müssen kann verwenden die OpenGraph Option einbetten.  Diese Option gibt Ihnen mehr Kontrolle des Feeds.  Die folgende Tabelle veranschaulicht ein Beispiel dafür.

Feed | Beschreibung | FeedType | Anwendungsfall
---- | ----------- | -------- | --------
Kommentar-Feed | Mithilfe des Yammer-API Open Diagramm um Unterhaltung, um ein Application-Objekt zu erleichtern. | Benutzerdefiniert | Eine Möglichkeit zur Nutzung in einer benutzerdefinierten CRM-Anwendung oder ein Medium Projektdetailseite in einer digital Asset Management-System.

**Wenn sie geeignet ist?**

Wenn Sie versuchen, Integrieren von Bedürfnisse Yammer-Feeds mit SharePoint-Websites und die Out-of-Box-Funktionen von den Feed Embed Ihre.

**Erste Schritte**

Im folgende Beispiel veranschaulicht, wie Websites mit einer Yammer-Feeds des Standorts anstelle der Standard-Newsfeed für die Website bereitstellen.

- [Provisioning.Yammer (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Yammer)

Die **CreateYammerGroupDiscussionPartXml** -Methode in der Klasse [YammerUtility.cs](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Utilities/YammerUtility.cs) stammen aus dem Beispiel [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/OfficeDevPnP.Core) .  Diese Methode erstellt das XML für eine Webpart-Add-in-Definition, die einer SharePoint-Seite hinzugefügt wird, wenn eine Website bereitgestellt wird.  Beachten Sie die **FeedType: "Gruppe"** Teil des Codes.  Hier können Sie sehen, dass die FeedType gesetzt ist, verwenden Sie die FeedType Out-of-Box-Gruppe.

    public static string CreateYammerGroupDiscussionPartXml(string yammerNetworkName, int yammerGroupId, bool showHeader, bool showFooter, bool useSSO = true)
    {
        StringBuilder wp = new StringBuilder(100);
        wp.Append("<?xml version=\"1.0\" encoding=\"utf-8\" ?>");
        wp.Append("<webParts>");
        wp.Append(" <webPart xmlns='http://schemas.microsoft.com/WebPart/v3'>");
        wp.Append("     <metaData>");
        wp.Append("         <type name='Microsoft.SharePoint.WebPartPages.ScriptEditorWebPart, Microsoft.SharePoint, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c' />");
        wp.Append("         <importErrorMessage>Cannot import this Web Part.</importErrorMessage>");
        wp.Append("     </metaData>");
        wp.Append("     <data>");
        wp.Append("         <properties>");
        wp.Append("             <property name='Title' type='string'>$Resources:core,ScriptEditorWebPartTitle;</property>");
        wp.Append("             <property name='Description' type='string'>$Resources:core,ScriptEditorWebPartDescription;</property>");
        wp.Append("             <property name='ChromeType' type='chrometype'>None</property>");
        wp.Append("             <property name='Content' type='string'>");
        wp.Append("             <![CDATA[");
        wp.Append("                 <div id='embedded-feed' style='height: 500px;'></div>");
        wp.Append("                 <script type='text/javascript' src='https://assets.yammer.com/assets/platform_embed.js'></script>");
        wp.Append("                 <script type='text/javascript'>  
                                        yam.connect.embedFeed({ container: '#embedded-feed', network: '"
                                        + yammerNetworkName
                                        + @"', feedType: 'group', feedId: '" + yammerGroupId            
                                        + @"', config: { use_sso: " + useSSO.ToString().ToLower()           
                                        + @", header: " + showHeader.ToString().ToLower()
                                        + @", footer: " + showFooter.ToString().ToLower()
                                        + " }}); </script>");
        wp.Append("             ]]>");
        wp.Append("             </property>");
        wp.Append("         </properties>");
        wp.Append("     </data>");
        wp.Append(" </webPart>");
        wp.Append("</webParts>");

        return wp.ToString();
    }

Die **CreateYammerOpenGraphDiscussionPartXml** -Methode in der Klasse [YammerUtility.cs](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Utilities/YammerUtility.cs) stammen aus dem Beispiel [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/OfficeDevPnP.Core) .  Diese Methode erstellt das XML für eine Webpart-Add-in-Definition, die einer SharePoint-Seite hinzugefügt wird, wenn eine Website bereitgestellt wird.  Beachten Sie die **FeedType: 'Öffnen-Diagramm'** Teil des Codes.  Hier können Sie sehen, dass die FeedType festgelegt ist, die OpenGraph-API verwenden.

    public static string CreateYammerOpenGraphDiscussionPartXml(string yammerNetworkName, string url, bool showHeader, 
                                                                    bool showFooter, string postTitle="", string postImageUrl="", 
                                                                    bool useSso = true, string groupId = "")
        {
            StringBuilder wp = new StringBuilder(100);
            wp.Append("<?xml version=\"1.0\" encoding=\"utf-8\" ?>");
            wp.Append("<webParts>");
            wp.Append(" <webPart xmlns='http://schemas.microsoft.com/WebPart/v3'>");
            wp.Append("     <metaData>");
            wp.Append("         <type name='Microsoft.SharePoint.WebPartPages.ScriptEditorWebPart, Microsoft.SharePoint, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c' />");
            wp.Append("         <importErrorMessage>Cannot import this Web Part.</importErrorMessage>");
            wp.Append("     </metaData>");
            wp.Append("     <data>");
            wp.Append("         <properties>");
            wp.Append("             <property name='Title' type='string'>$Resources:core,ScriptEditorWebPartTitle;</property>");
            wp.Append("             <property name='Description' type='string'>$Resources:core,ScriptEditorWebPartDescription;</property>");
            wp.Append("             <property name='ChromeType' type='chrometype'>None</property>");
            wp.Append("             <property name='Content' type='string'>");
            wp.Append("             <![CDATA[");
            wp.Append("                 <div id='embedded-feed' style='height: 500px;'></div>");
            wp.Append("                 <script type='text/javascript' src='https://assets.yammer.com/assets/platform_embed.js'></script>");
            wp.Append("                 <script>");
            wp.Append("                     yam.connect.embedFeed({");
            wp.Append("                       container: '#embedded-feed'");
            wp.Append("                             , feedType: 'open-graph'");
            wp.Append("                             , feedId: ''");
            wp.Append("                             , config: {");
            wp.Append("                                  use_sso: " + useSso.ToString().ToLower());
            wp.Append("                                  , header: " + showHeader.ToString().ToLower());
            wp.Append("                                  , footer: " + showFooter.ToString().ToLower());
            wp.Append("                                  , showOpenGraphPreview: false");
            wp.Append("                                  , defaultToCanonical: false");
            wp.Append("                                  , hideNetworkName: false");
            wp.Append("                                  , promptText: 'Start a conversation'");
            if (!string.IsNullOrEmpty(groupId))
            {
                wp.Append("                              , defaultGroupId: '" + groupId + "'"); 
            }
            wp.Append("                             }");
            wp.Append("                             , objectProperties: {"); 
            wp.Append("                               url: '" + url + "'");
            wp.Append("                               , type: 'page'");
            wp.Append("                               , title: '" + postTitle + "'");
            wp.Append("                               , image: '" + postImageUrl + "'");
            wp.Append("                             }");
            wp.Append("                         });");
            wp.Append("                     </script>");
            wp.Append("             ]]>");
            wp.Append("             </property>");
            wp.Append("         </properties>");
            wp.Append("     </data>");
            wp.Append(" </webPart>");
            wp.Append("</webParts>");

            return wp.ToString();
        }

Sehen Sie sich das [Integrieren von Yammer-Feeds für SharePoint-Websites (Office 365 Plug & Play-Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/Integrate-Yammer-feeds-to-SharePoint-sites) um einen Durchlauf finden Sie unter über der- [Provisioning.Yammer (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Yammer).

Weitere Informationen zu Yammer einbetten finden Sie im Artikel [Yammer einbetten Feed (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/embed) .

Weitere Informationen zu Yammer-OpenGraph finden Sie im Artikel [Einführung in Open Diagramm & Format (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/open-graph) .

<a name="yammer-opengraph-api--yammer-rest-api-with-yammer-sdks"></a>Yammer-OpenGraph API & Yammer-REST-API mit Yammer SDKs
-------------------------------------------------------

Bei dieser Option verwenden Sie die Yammer-OpenGraph API und/oder Yammer-REST-API mit Yammer-SDKs Yammer mit SharePoint integriert werden soll.  Diese APIs kann auch zur Integration von Yammer mit Prozessen außerhalb von Webseiten verwendet werden.  Beispiele für solche Szenarien sind Dienste und lange ausgeführte Vorgänge. 
    
- Diese Option dauert länger implementieren.
- Dieser Option können Sie steuern, alle Aspekte der Feed und wie angezeigt wird und wie Sie mit ihm interagieren.

**Wenn sie geeignet ist?**

- Wenn Sie versuchen, zu Yammer-Feeds in SharePoint-Websites integrieren und die Out-of-Box-Funktionen der Embed Feeds nicht Ihren Anforderungen entsprechen.
- Wenn Sie versuchen, Yammer-Feeds in Dienste oder lange ausgeführte Vorgänge zu integrieren.

**Erste Schritte**

Weitere Informationen zu Yammer-OpenGraph finden Sie im Artikel [Einführung in Open Diagramm & Format (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/open-graph) .

Yammer-SDKs bieten Sie die Möglichkeit zum Authentifizieren bei Yammer.  Weitere Informationen zu den SDKs Yammer finden Sie unter den folgenden Artikeln:

- [JavaScript-SDK](https://developer.yammer.com/v1.0/docs/js-sdk)
- [Ruby SDK](https://developer.yammer.com/v1.0/docs/ruby-sdk)
- [Python SDK (engl.)](https://developer.yammer.com/v1.0/docs/python-sdk)
- [iOS-SDK](https://developer.yammer.com/v1.0/docs/ios-sdk)
- [.NET SDK](https://developer.yammer.com/v1.0/docs/net-sdk)
- [Windows Phone 8 SDK](https://developer.yammer.com/v1.0/docs/windows-phone-8-sdk)

Nachdem Sie bei Yammer über die Yammer-SDKs authentifiziert haben, können Sie die Yammer-REST-APIs aufrufen.  

Weitere Informationen zu Yammer-REST-APIs finden Sie im Artikel [REST-API & Rate Grenzwerte (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/rest-api-rate-limits) .

**Hinweis Authentifizierung**

In einem Szenario, in dem Sie mit den Anmeldeinformationen anmelden, die von der Anmeldeinformationen unterscheiden, die Sie verwenden Sie zum Anmelden an SharePoint mit Ihnen, möglicherweise eine Single-Sign-on-Funktion für Ihre Benutzer entwickeln möchten.  Ein Beispiel für ein solches Szenario ist, wenn Sie in SharePoint mit einer Live-ID anmelden und Sie in Yammer mit einem Microsoft persönliche oder Arbeit Konto anmelden müssen.

Zum Implementieren eines Single-Sign-on-Szenarios können Sie steuern, die Benutzer zum Anmelden bei der ersten Yammer, den sie zu einer SharePoint-Seite mit der benutzerdefinierten Komponente Yammer darauf stammen. Nachdem der Benutzer in Yammer über die Yammer-SDK signiert können Sie die Aktualisierungstoken für den Benutzer in ihrem Benutzerprofil speichern.  Anschließend können Sie bei nachfolgenden Besuchen auf der Seite Abrufen der Aktualisierungstoken aus dem Benutzerprofil und Authentifizierung verwenden.  Bei diesem Ansatz müssen Ihre Endbenutzer nur zum Anmelden bei Yammer, wenn ihre Aktualisierungstoken abläuft.

<a name="related-links"></a>Verwandte links
=============
- [Integrieren von Yammer-Feeds für SharePoint-Websites (Office 365 Plug & Play-Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/Integrate-Yammer-feeds-to-SharePoint-sites)
- [Yammer einbetten Feed (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/embed)
- [Einführung in Open Diagramm & Format (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/open-graph)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================
- [Provisioning.Yammer (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Yammer)
- [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core)
- Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D)
- SharePoint 2013 lokal
