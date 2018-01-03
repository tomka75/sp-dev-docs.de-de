---
title: Folgen von Dokumenten und Websites mithilfe des .NET-Client-Objektmodells in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 84366e01-4961-459d-8109-2f1d2d714353
ms.openlocfilehash: b499f866a482eae50a0721382c1ddd28f76d6750
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="follow-documents-and-sites-by-using-the-net-client-object-model-in-sharepoint"></a>Folgen von Dokumenten und Websites mithilfe des .NET-Client-Objektmodells in SharePoint

In diesem Artikel erfahren Sie, wie Sie mithilfe des .NET-Clientobjektmodells in SharePoint mit Features zum Folgen von Inhalten arbeiten.

## <a name="how-do-i-use-the-net-client-object-model-to-follow-content"></a>Wie verwende ich das .NET-Clientobjektmodell zum Folgen von Inhalten?
<a name="bk_intro"> </a>

SharePoint-Benutzer können Dokumenten, Websites und Tags folgen, um Updates zu den Elementen in ihre Newsfeeds abzurufen und gefolgte Dokumente und Websites schnell zu öffnen. Sie können das .NET-Clientobjektmodell in Ihrer App oder Lösung verwenden, um mit dem Folgen von Inhalten zu beginnen, das Folgen von Inhalten zu beenden und gefolgte Inhalte im Auftrag des aktuellen Benutzers abzurufen. In diesem Artikel erfahren Sie, wie Sie eine Konsolenanwendung erstellen, die das .NET-Clientobjektmodell verwendet, um mit Features zum Folgen von Inhalten für Dokumente und Websites zu arbeiten.
  
    
    
Die folgenden Objekte sind die primären APIs für Aufgaben zum Folgen von Inhalten:
  
    
    

-  [SocialFollowingManager]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)) bietet Methoden zum Verwalten eines Benutzers Liste besuchter Akteure.
    
  
-  [SocialActor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx)) stellt ein Dokument, Website oder Tag, der der Server als Antwort auf eine Anforderung mithilfe der clientseitigen zurückgibt.
    
  
-  [SocialActorInfo]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorInfo.aspx)) gibt ein Dokument, Website oder Tag in clientseitige Anforderungen an den Server.
    
  
-  [Microsoft.SharePoint.Client.Social.SocialActorType]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorType.aspx)) und [Microsoft.SharePoint.Client.Social.SocialActorTypes]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorTypes.aspx)) geben Inhaltstypen in clientseitigen Anforderungen an den Server an.
    
> [!NOTE]
> Sie verwenden diese APIs auch für Aufgaben zum Folgen von Personen, allerdings unterstützen die Methoden **GetSuggestions** und **GetFollowers**, die über [SocialFollowingManager]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)) verfügbar sind, nur das Folgen von Personen, nicht von Inhalten. Weitere Informationen zur Verwendung von [SocialFollowingManager]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)) finden Sie unter [Folgen von Inhalten in SharePoint](follow-content-in-sharepoint.md) und [Folgen von Personen in SharePoint](follow-people-in-sharepoint.md). Codebeispiele zum Folgen von Personen finden Sie unter [Vorgehensweise: Folgen von Personen mithilfe des .NET-Clientobjektmodells in SharePoint](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md) 
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-following-content-features-by-using-the-sharepoint-net-client-object-model"></a>Voraussetzungen für das Einrichten Ihrer Entwicklungsumgebung zum Arbeiten mit Features zum Folgen von Inhalten mithilfe des .NET-Clientobjektmodells in SharePoint
<a name="bkmk_SetUpDevEnv"> </a>

Um eine Konsolenanwendung erstellen, die das Clientobjektmodell .NET verwendet folgende Inhaltsfunktionen für Dokumente und Websites entwickelt, benötigen Sie Folgendes:
  
    
    

- SharePoint mit konfigurierter „Meine Website“, mit erstellter Website „Meine Website“ für den aktuellen Benutzer und mit einem in eine SharePoint-Dokumentbibliothek hochgeladenen Dokument
    
  
- Visual Studio 2012
    
  
- Zugriffsberechtigungen vom Typ **Vollzugriff** auf die Benutzerprofil-Dienstanwendung für den angemeldeten Benutzer
    
> [!NOTE]
> Wenn Sie die Entwicklungsaufgaben nicht auf dem Computer durchführen, auf dem SharePoint ausgeführt wird, laden Sie die [SharePoint-Clientkomponenten](http://www.microsoft.com/en-us/download/details.aspx?id=35585) herunter, die die SharePoint-Clientassemblys enthalten.
  
    
    


## <a name="create-a-console-application-to-work-with-following-content-features-by-using-the-sharepoint-net-client-object-model"></a>Erstellen einer Konsolenanwendung zum Arbeiten mit Features zum Folgen von Inhalten mithilfe des .NET_Clientobjektmodells für SharePoint
<a name="bkmk_CreateConsoleApp"> </a>


1. Wählen Sie in Visual Studio die Optionen **Datei**, **Neu**, **Projekt**.
    
  
2. Wählen Sie im Dialogfeld **Neues Projekt** aus der Dropdownliste oben im Dialogfeld die Option **.NET Framework 4.5**.
    
  
3. Klicken Sie in der Liste **Vorlagen** wählen Sie **Windows**, und wählen Sie dann die Vorlage **Konsolenanwendung**.
    
  
4. Nennen Sie das Projekt FollowContentCSOM, und wählen Sie dann auf die Schaltfläche **OK**.
    
  
5. Fügen Sie Verweise auf die folgenden Assemblys hinzu:
    
  - **Microsoft.SharePoint.Client**   
  - **Microsoft.SharePoint.ClientRuntime**
  - **Microsoft.SharePoint.Client.UserProfiles**
    
6. Ersetzen Sie die Inhalte der **Program**-Klasse durch das Codebeispiel aus einem der folgenden Szenarien:
    
  -  [Starten Sie und beenden Sie die folgenden Inhalte](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md#bkmk_FollowContent)  
  -  [Abrufen von verfolgten Inhalt für den aktuellen Benutzer](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md#bkmk_GetFollowed)
    
7. Wählen Sie zum Testen der Konsolenanwendung, klicken Sie auf der Menüleiste **Debuggen**, **Debuggen starten** aus.
    
  

## <a name="code-example-start-and-stop-following-content-by-using-the-sharepoint-net-client-object-model"></a>Codebeispiel: Starten und beenden nach Inhalt mithilfe des Clientobjektmodells für SharePoint.NET
<a name="bkmk_FollowContent"> </a>

Im folgenden Codebeispiel wird der aktuelle Benutzer Start nach oder nach einem Zielelement beenden. Außerdem wird gezeigt, wie Sie:
  
    
    

- Überprüfen Sie, ob der aktuelle Benutzer ein bestimmtes Dokument oder Website folgt mithilfe der  [IsFollowed]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx)) -Methode.
    
  
- Starten Sie nach einem Dokument oder einer Website mithilfe der  [Follow]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx)) -Methode.
    
  
- Beenden Sie nach einem Dokument oder einer Website mithilfe der  [StopFollowing]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx)) -Methode.
    
  
- Rufen Sie die Anzahl von Dokumenten oder Websites, die der aktuelle Benutzer mithilfe der Methode  [GetFollowedCount]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx)) folgt.
    
  
Dieses Codebeispiel verwendet das  [SocialFollowResult]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowResult.aspx)) -Objekt, das von der [Follow]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx)) -Methode, um festzustellen, ob starten oder beenden Sie das Zielelement folgt zurückgegeben wird.
  
> [!NOTE]
> Ändern Sie die Platzhalterwerte für die Variablen **serverUrl** und **contentUrl**, bevor Sie den Code ausführen. Wenn Sie eine Website anstelle eines Dokuments verwenden möchten, verwenden Sie die auskommentierten Variablen.
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace FollowContentCSOM
{
    class Program
    {
        static ClientContext clientContext;
        static SocialFollowingManager followingManager;
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the URL of the target
            // server and target document (or site).
            const string serverUrl = "http://serverName";
            const string contentUrl = @"http://serverName/libraryName/fileName";
            const SocialActorType contentType = SocialActorType.Document;
            // Do not use a trailing '/' for a subsite.
            //const string contentUrl = @"http://serverName/subsiteName"; 
            //const SocialActorType contentType = SocialActorType.Site;

            // Get the client context.
            clientContext = new ClientContext(serverUrl);

            // Get the SocialFeedManager instance.
            followingManager = new SocialFollowingManager(clientContext);

            // Create a SocialActorInfo object to represent the target item.
            SocialActorInfo actorInfo = new SocialActorInfo();
            actorInfo.ContentUri = contentUrl;
            actorInfo.ActorType = contentType;

            // Find out whether the current user is following the target item.
            ClientResult<bool> isFollowed = followingManager.IsFollowed(actorInfo);

            // Get the information from the server.
            clientContext.ExecuteQuery();

            Console.WriteLine("Was the current user following the target {0}? {1}\\n",
                actorInfo.ActorType.ToString().ToLower(), isFollowed.Value);
            Console.Write("Initial count: ");

            // Get the current count of followed items.
            WriteFollowedCount(actorInfo.ActorType);

            // Try to follow the target item. If the result is OK, then
            // the request succeeded.
            ClientResult<SocialFollowResult> result = followingManager.Follow(actorInfo);
            clientContext.ExecuteQuery();

            // If the result is AlreadyFollowing, then stop following 
            // the target item.
            if (result.Value == SocialFollowResult.AlreadyFollowing)
            {
                followingManager.StopFollowing(actorInfo);
                clientContext.ExecuteQuery();
            }

            // Handle other SocialFollowResult return values.
            else if (result.Value == SocialFollowResult.LimitReached
                || result.Value == SocialFollowResult.InternalError)
            {
                Console.WriteLine(result.Value);
            }

            // Get the updated count of followed items.
            Console.Write("Updated count: ");
            WriteFollowedCount(actorInfo.ActorType);
            Console.ReadKey();
        }

        // Get the count of the items that the current user is following.
        static void WriteFollowedCount(SocialActorType type)
        {

            // Set the parameter for the GetFollowedCount method, and
            // handle the case where the item is a site. 
            SocialActorTypes types = SocialActorTypes.Documents;
            if (type != SocialActorType.Document)
            {
                types = SocialActorTypes.Sites;
            }

            ClientResult<int> followedCount = followingManager.GetFollowedCount(types);
            clientContext.ExecuteQuery();
            Console.WriteLine("{0} followed {1}", followedCount.Value, types.ToString().ToLower());
        }
    }
}
```


## <a name="code-example-get-followed-content-by-using-the-sharepoint-net-client-object-model"></a>Codebeispiel: Abrufen von gefolgten Inhalten mithilfe des .NET-Clientobjektmodells in SharePoint
<a name="bkmk_GetFollowed"> </a>

Im folgenden Codebeispiel wird dient zum Abrufen der Dokumente und Websites, dass der aktuelle Benutzer folgt und ruft Informationen zum Status des folgenden Inhalts des Benutzers ab. Außerdem wird gezeigt, wie Sie:
  
    
    

- Überprüfen Sie, ob der aktuelle Benutzer das Zieldokument und Website folgt mithilfe der  [IsFollowed]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx)) -Methode.
    
  
- Rufen Sie die Anzahl von Dokumenten und Websites, die der aktuelle Benutzer mithilfe der Methode  [GetFollowedCount]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx)) folgt.
    
  
- Rufen Sie die Dokumente und Websites, die der aktuelle Benutzer mithilfe der Methode  [GetFollowed]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx)) folgt.
    
  
- Iterieren Sie durch die Inhaltsgruppen, und rufen Sie den Namen, den Inhalts-URI und den URI jedes Elements ab.
    
> [!NOTE]
> Ändern Sie den Platzhalterwert für die Variablen **serverUrl**, **docContentUrl** und **siteContentUrl**, bevor Sie den Code ausführen.
  
    
    


```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace FollowContentCSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the URLs of
            // the target server, document, and site.
            const string serverUrl = "http://serverName";
            const string docContentUrl = @"http://serverName/libraryName/fileName";
            const string siteContentUrl = @"http://serverName/subsiteName"; // do not use a trailing '/' for a subsite

            // Get the client context.
            ClientContext clientContext = new ClientContext(serverUrl);

            // Get the SocialFollowingManager instance.
            SocialFollowingManager followingManager = new SocialFollowingManager(clientContext);

            // Create SocialActorInfo objects to represent the target 
            // document and site.
            SocialActorInfo docActorInfo = new SocialActorInfo();
            docActorInfo.ContentUri = docContentUrl;
            docActorInfo.ActorType = SocialActorType.Document;
            SocialActorInfo siteActorInfo = new SocialActorInfo();
            siteActorInfo.ContentUri = siteContentUrl;
            siteActorInfo.ActorType = SocialActorType.Site;

            // Find out whether the current user is following the target
            // document and site.
            ClientResult<bool> isDocFollowed = followingManager.IsFollowed(docActorInfo);
            ClientResult<bool> isSiteFollowed = followingManager.IsFollowed(siteActorInfo);

            // Get the count of documents and sites that the current
            // user is following.
            ClientResult<int> followedDocCount = followingManager.GetFollowedCount(SocialActorTypes.Documents);
            ClientResult<int> followedSiteCount = followingManager.GetFollowedCount(SocialActorTypes.Sites);

            // Get the documents and the sites that the current user
            // is following.
            ClientResult<SocialActor[]> followedDocResult = followingManager.GetFollowed(SocialActorTypes.Documents);
            ClientResult<SocialActor[]> followedSiteResult = followingManager.GetFollowed(SocialActorTypes.Sites);

            // Get the information from the server.
            clientContext.ExecuteQuery();

            // Write the results to the console window.
            Console.WriteLine("Is the current user following the target document? {0}", isDocFollowed.Value);
            Console.WriteLine("Is the current user following the target site? {0}", isSiteFollowed.Value);
            if (followedDocCount.Value > 0)
            {
                IterateThroughContent(followedDocCount.Value, followedDocResult.Value);
            } if (followedSiteCount.Value > 0)
            {
                IterateThroughContent(followedSiteCount.Value, followedSiteResult.Value);
            }
            Console.ReadKey();
        }

        // Iterate through the items and get each item's display
        // name, content URI, and absolute URI.
        static void IterateThroughContent(int count, SocialActor[] actors)
        {
            SocialActorType actorType = actors[0].ActorType;
            Console.WriteLine("\\nThe current user is following {0} {1}s:", count, actorType.ToString().ToLower());
            foreach (SocialActor actor in actors)
            {
                Console.WriteLine("  - {0}", actor.Name);
                Console.WriteLine("\\tContent URI: {0}", actor.ContentUri);
                Console.WriteLine("\\tURI: {0}", actor.Uri);
            }
        }
    }
}
```


## <a name="see-also"></a>Siehe auch
<a name="bkmk_AddtionalResources"> </a>


-  [Folgen von Inhalten in SharePoint](follow-content-in-sharepoint.md)
    
  
-  [Vorgehensweise: führen Sie Dokumente, Websites und Tags mithilfe des REST-Diensts in SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)
    
  
-  [Vorgehensweise: führen Sie die Personen mithilfe des clientobjektmodells .NET SharePoint](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md)
    
  

