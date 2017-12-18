---
title: Folgen von Personen mithilfe des .NET-Clientobjektmodells in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 0fdb7ca5-d408-4256-b52b-886c4bc3b5b8
ms.openlocfilehash: 7bef2d0bdef87db1d0234acba60341ff22254df8
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="follow-people-by-using-the-net-client-object-model-in-sharepoint"></a>Folgen von Personen mithilfe des .NET-Clientobjektmodells in SharePoint

In diesem Artikel erfahren Sie, wie Sie mithilfe des .NET-Clientobjektmodells in SharePoint mit Features zum Folgen von Personen arbeiten.

## <a name="why-use-following-people-features-in-sharepoint"></a>Gründe für die Verwendung von Features zum Folgen von Personen in SharePoint

Wenn in SharePoint ein Benutzer Personen folgt, werden die Beiträge und Aktivitäten der gefolgten Personen im Newsfeed des Benutzers angezeigt. Indem Sie Features zum Folgen von Personen nutzen, damit sich Benutzer auf die Personen konzentrieren können, die für sie wichtig sind, können Sie die Relevanz Ihrer App oder Lösung verbessern. Im .NET-Clientobjektmodell werden Personen, denen Sie folgen, durch [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx)-Objekte dargestellt. Zum Durchführen der Hauptaufgaben zum Folgen von Personen im .NET-Clientobjektmodell verwenden Sie das [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)-Objekt. In diesem Artikel erfahren Sie, wie Sie mithilfe des .NET-Clientobjektmodells mit Features zum Folgen von Personen arbeiten.
  
    
    

> **Hinweis:** Wir konzentrieren uns auf [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx), da es die grundlegenden Funktionen zum Folgen von Personen und Inhalten konsolidiert. Das [PeopleManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.aspx)-Objekt enthält jedoch zusätzliche Funktionen zum Folgen von Personen, wie die Methode [AmIFollowedBy(String)](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.AmIFollowedBy.aspx) und Methoden, die den Folgen-Status anderer Benutzer abrufen.
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-following-people-features-by-using-the-sharepoint-net-client-object-model"></a>Voraussetzungen für das Einrichten Ihrer Entwicklungsumgebung zum Arbeiten mit Features zum Folgen von Personen mithilfe des .NET-Clientobjektmodells in SharePoint

Zum Erstellen einer Konsolenanwendung, die das .NET-Clientobjektmodell zum Arbeiten mit Features zum Folgen von Personen verwendet, benötigen Sie Folgendes:
  
    
    

- SharePoint mit konfigurierter „Meine Website“ und mit Benutzerprofilen und persönlichen Websites für den aktuellen Benutzer und einen Zielbenutzer
    
  
- Visual Studio 2012
    
  
- Zugriffsberechtigungen vom Typ **Vollzugriff** auf die Benutzerprofil-Dienstanwendung für den angemeldeten Benutzer
    
  

> **Hinweis:** Wenn Sie die Entwicklungsaufgaben nicht auf dem Computer durchführen, auf dem SharePoint ausgeführt wird, laden Sie die [SharePoint-Clientkomponenten](http://www.microsoft.com/en-us/download/details.aspx?id=35585) herunter, die die SharePoint-Clientassemblys enthalten.
  
    
    


## <a name="create-a-console-application-in-visual-studio-2012"></a>Erstellen einer Konsolenanwendung in Visual Studio 2012
<a name="bkmk_CreateConsoleApp"> </a>


1. Öffnen Sie Visual Studio, und wählen Sie **Datei**, **Neu**, **Projekt**.
    
  
2. Wählen Sie im Dialogfeld **Neues Projekt** aus der Dropdownliste oben im Dialogfeld die Option **.NET Framework 4.5**.
    
  
3. Klicken Sie in der Liste **Vorlagen** wählen Sie **Windows**, und wählen Sie dann die Vorlage **Konsolenanwendung**.
    
  
4. Nennen Sie das Projekt FollowPeopleCSOM, und wählen Sie dann auf die Schaltfläche **OK**.
    
  
5. Fügen Sie Verweise auf die folgenden Assemblys hinzu:
    
  - **Microsoft.SharePoint.Client**  
  - **Microsoft.SharePoint.ClientRuntime** 
  - **Microsoft.SharePoint.Client.UserProfiles**
    
  
6. Ersetzen Sie die Inhalte der **Program**-Klasse durch das Codebeispiel aus einem der folgenden Szenarien:
    
  -  [Starten und Beenden von Personen folgen](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md#bkmk_FollowPeople)  
  -  [Nachfolgende Aktivitäten und beobachteter Personen heranziehen.](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md#bkmk_GetFollowednFollowers)
    
  
7. Wählen Sie zum Testen der Konsolenanwendung, klicken Sie auf der Menüleiste **Debuggen**, **Debuggen starten** aus.
    
  

## <a name="code-example-start-or-stop-following-people-by-using-the-sharepoint-net-client-object-model"></a>Codebeispiel: Starten oder beenden nach Personen, für die mithilfe des Clientobjektmodells für SharePoint.NET
<a name="bkmk_FollowPeople"> </a>

Im folgenden Codebeispiel wird der aktuelle Benutzer Start nach oder einen Zielbenutzer nach Beenden. Außerdem wird gezeigt, wie Sie:
  
    
    

- Überprüfen Sie, ob der aktuelle Benutzer einen Zielbenutzer folgt, mit der  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) -Methode.
    
  
- Rufen Sie die Anzahl der Personen, die der aktuelle Benutzer mithilfe der Methode  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) folgt.
    
  
- Starten Sie nach der Zielbenutzer mithilfe der  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) -Methode.
    
  
- Folgen den Zielbenutzer mithilfe der  [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) -Methode nicht mehr.
    
  
Dieses Codebeispiel verwendet das  [SocialFollowResult](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowResult.aspx) -Objekt, das von der [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) -Methode zu bestimmen, ob das Starten oder beenden, folgen den Zielbenutzer zurückgegeben wird.
  
    
    

> **Hinweis:** Ändern Sie die Platzhalterwerte für die Variablen **serverUrl** und **targetUser**, bevor Sie den Code ausführen.
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace FollowPeopleCSOM
{
    class Program
    {
        static ClientContext clientContext;
        static SocialFollowingManager followingManager;
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the target
            // server URL and target user.
            const string serverUrl = "http://serverName";
            const string targetUser = "domainName\\\\userName";

            // Get the client context.
            clientContext = new ClientContext(serverUrl);

            // Get the SocialFeedManager instance.
            followingManager = new SocialFollowingManager(clientContext);

            // Create a SocialActorInfo object to represent the target user.
            SocialActorInfo actorInfo = new SocialActorInfo();
            actorInfo.AccountName = targetUser;

            // Find out whether the current user is following the target user.
            ClientResult<bool> isFollowed = followingManager.IsFollowed(actorInfo);

            // Get the information from the server.
            clientContext.ExecuteQuery();

            Console.WriteLine("Was the current user following the target user? {0}\\n", isFollowed.Value);
            Console.Write("Initial count: ");

            // Get the current count of followed people.
            WriteFollowedCount();

            // Try to follow the target user. If the result is OK, then
            // the request succeeded.
            ClientResult<SocialFollowResult> result = followingManager.Follow(actorInfo);
            clientContext.ExecuteQuery();

            // If the result is AlreadyFollowing, then stop following 
            // the target user.
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

            // Get the updated count of followed people.
            Console.Write("Updated count: ");
            WriteFollowedCount();
            Console.ReadKey();
        }

        // Get the count of the people who the current user is following.
        static void WriteFollowedCount()
        {
            ClientResult<int> followedCount = followingManager.GetFollowedCount(SocialActorTypes.Users);
            clientContext.ExecuteQuery();
            Console.WriteLine("The current user is following {0} people.", followedCount.Value);
        }
    }
}

```


## <a name="code-example-get-followers-and-followed-people-by-using-the-sharepoint-net-client-object-model"></a>Codebeispiel: Abrufen von Followern und gefolgten Personen mithilfe des .NET-Clientobjektmodells in SharePoint
<a name="bkmk_GetFollowednFollowers"> </a>

Der folgende Code Beispiel ruft die Personen, die der aktuelle Benutzer folgt, ruft die Personen, gefolgt von den aktuellen Benutzer und ruft Informationen über die folgenden Personen Status des aktuellen Benutzers, ab. Außerdem wird gezeigt, wie Sie:
  
    
    

- Überprüfen Sie, ob der aktuelle Benutzer einen Zielbenutzer folgt, mit der  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) -Methode.
    
  
- Rufen Sie die Anzahl der Personen, die der aktuelle Benutzer mithilfe der Methode  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) folgt.
    
  
- Rufen Sie die Personen, die der aktuelle Benutzer mithilfe der Methode  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx) folgt.
    
  
- Rufen Sie die Personen, die den aktuellen Benutzer mithilfe der Methode  [GetFollowers](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowers.aspx) folgen.
    
  
- Iterieren Sie durch die Gruppen von Personen, und rufen Sie den Anzeigenamen, den persönlichen URI und den Bild-URI jeder Person ab.
    
  

> **Hinweis:** Ändern Sie die Platzhalterwerte für die Variablen **serverUrl** und **targetUser**, bevor Sie den Code ausführen.
  
    
    


```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace FollowPeopleCSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the target
            // server URL and target user.
            const string serverUrl = "http://serverName";
            const string targetUser = "domainName\\\\userName";

            // Get the client context.
            ClientContext clientContext = new ClientContext(serverUrl);
            
            // Get the SocialFeedManager instance.
            SocialFollowingManager followingManager = new SocialFollowingManager(clientContext);

            // Create a SocialActorInfo object to represent the target user.
            SocialActorInfo actorInfo = new SocialActorInfo();
            actorInfo.AccountName = targetUser;

            // Find out whether the current user is following the target user.
            ClientResult<bool> isFollowed = followingManager.IsFollowed(actorInfo);

            // Get the count of people who the current user is following.
            ClientResult<int> followedCount = followingManager.GetFollowedCount(SocialActorTypes.Users);

            // Get the people who the current user is following.
            ClientResult<SocialActor[]> followedResult = followingManager.GetFollowed(SocialActorTypes.Users);

            // Get the people who are following the current user.
            ClientResult<SocialActor[]> followersResult = followingManager.GetFollowers();

            // Get the information from the server.
            clientContext.ExecuteQuery();

            // Write the results to the console window.
            Console.WriteLine("Is the current user following the target user? {0}\\n", isFollowed.Value);
            Console.WriteLine("People who the current user is following: ({0} count)", followedCount.Value);
            IterateThroughPeople(followedResult.Value);
            Console.WriteLine("\\nPeople who are following the current user:");
            IterateThroughPeople(followersResult.Value);
            Console.ReadKey();
        }

        // Iterate through the people and get each person's display
        // name, personal URI, and picture URI.
        static void IterateThroughPeople(SocialActor[] actors)
        {
            foreach (SocialActor actor in actors)
            {
                Console.WriteLine("  - {0}", actor.Name);
                Console.WriteLine("\\tPersonal URI: {0}", actor.PersonalSiteUri);
                Console.WriteLine("\\tPicture URI: {0}", actor.ImageUri);
            }
        }
    }
}

```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bkmk_AdditionalResources"> </a>


-  [Folgen von Personen in SharePoint](follow-people-in-sharepoint.md)
    
  
-  [Vorgehensweise: folgen Sie Menschen mit der JavaScript-Objektmodell in SharePoint](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md)
    
  
-  [Vorgehensweise: Führen Sie Dokumente und Websites mit .NET Client-Objektmodell in SharePoint](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)
    
  

