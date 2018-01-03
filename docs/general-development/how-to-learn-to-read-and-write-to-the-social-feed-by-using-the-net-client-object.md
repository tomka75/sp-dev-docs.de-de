---
title: "Lesen und Schreiben in den Feed für soziale Netzwerke mithilfe des .NET-Clientobjektmodells in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3c15ede5-8a59-47e6-a0b2-c17ec6bf4ae1
ms.openlocfilehash: 74fe67537137ffd6665a1ee0d00afdfa944ecdfa
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="read-and-write-to-the-social-feed-by-using-the-net-client-object-model-in-sharepoint"></a>Lesen und Schreiben in den Feed für soziale Netzwerke mithilfe des .NET-Clientobjektmodells in SharePoint

Erstellen Sie eine Konsolenanwendung, die den sozialen Feed mithilfe des .NET-Clientobjektmodells in SharePoint liest bzw. in den sozialen Feed schreibt.

## <a name="prerequisites-for-creating-a-console-application-that-reads-and-writes-to-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a>Voraussetzungen für das Erstellen einer Konsolenanwendung, die Lese- und Schreibvorgänge auf den Feed für soziale Netzwerke mithilfe des Clientobjektmodells für SharePoint.NET
<a name="bkmk_Prereqs"> </a>

Die Konsolenanwendung, die Sie erstellen, einen Zielbenutzer Feed abruft und druckt den Stamm-Post von jedem Thread in einer nummerierten Liste. Klicken Sie dann veröffentlicht eine einfache Text-Antwort an den ausgewählten Thread. Die gleiche-Methode ( [CreatePost]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx)) ) wird verwendet, um beide Beiträge veröffentlichen und Antworten Sie den Feed.
  
    
    
Zum Erstellen der Konsolenanwendung benötigen Sie Folgendes:
  
    
    

- SharePoint mit konfigurierter „Meine Website“, mit erstellten persönlichen Websites für den aktuellen Benutzer und einen Zielbenutzer sowie mit einigen vom Zielbenutzer erstellten Beiträgen
    
  
- Visual Studio 2012
    
  
- Zugriffsberechtigungen vom Typ **Vollzugriff** auf die Benutzerprofil-Dienstanwendung für den angemeldeten Benutzer
    
> [!NOTE]
> Wenn Sie die Entwicklungsaufgaben nicht auf dem Computer durchführen, auf dem SharePoint ausgeführt wird, laden Sie die [SharePoint-Clientkomponenten](http://www.microsoft.com/en-us/download/details.aspx?id=35585) herunter, die die SharePoint-Clientassemblys enthalten.
  
    
    


### <a name="core-concepts-to-know-about-working-with-sharepoint-social-feeds"></a>Kernkonzepte zum Arbeiten mit sozialen Feeds in SharePoint
<a name="bkmk_CoreConcepts"> </a>

Tabelle 1 enthält Links zu Artikeln, in denen wichtige Kernkonzepte zu, die Sie kennen sollten beschreiben, bevor Sie beginnen.
  
    
    

**In Tabelle 1. Zentrale Konzepte für die Arbeit mit sozialen Feeds SharePoint**


|**Titel des Artikels**|**Beschreibung**|
|:-----|:-----|
| [Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint](get-started-developing-with-social-features-in-sharepoint.md) <br/> |Hier erhalten Sie Hilfe zu den ersten Schritten beim Programmieren mit sozialen Feeds und Mikroblogbeiträgen, beim Folgen von Personen und Inhalten (Dokumente, Websites und Tags) sowie beim Arbeiten mit Benutzerprofilen.  <br/> |
| [Arbeiten mit sozialen Feeds in SharePoint](work-with-social-feeds-in-sharepoint.md) <br/> |Informationen Sie zu allgemeinen Programmieraufgaben zum Arbeiten mit sozialen Feeds und die API, die Sie zum Ausführen der Aufgaben verwenden.  <br/> |
   

## <a name="create-the-console-application-in-visual-studio-2012-and-add-references-to-client-assemblies"></a>Erstellen Sie die Konsolenanwendung in Visual Studio 2012, und fügen Sie Verweise auf Clientassemblys
<a name="bkmk_CreateApp"> </a>


1. Öffnen Sie auf Ihrem Entwicklungscomputer Visual Studio 2012.
    
  
2. Klicken Sie in der Menüleiste auf **Datei**, **Neu**, **Projekt**.
    
  
3. Wählen Sie im Dialogfeld **Neues Projekt** aus der Dropdownliste oben im Dialogfeld die Option **.NET Framework 4.5**.
    
  
4. Wählen Sie **Windows**, und wählen Sie dann die Vorlage **Konsolenanwendung**, aus der Liste **Vorlagen**.
    
  
5. Nennen Sie das Projekt ReadWriteMySite, und wählen Sie dann auf die Schaltfläche **OK**.
    
  
6. Fügen Sie wie folgt Verweise auf die Clientassemblys hinzu:
    
   a. Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü für das Projekt **ReadWriteMySite**, und wählen Sie dann **Verweis hinzufügen**.
  
   b. Wählen Sie im Dialogfeld **Verweis-Manager** die folgenden Assemblys aus:
    
     - **Microsoft.SharePoint.Client**
    
     - **Microsoft.SharePoint.Client.Runtime**
    
     - **Microsoft.SharePoint.Client.UserProfiles**  

   Wenn Sie auf dem Computer entwickeln, auf dem SharePoint ausgeführt wird, befinden sich die Assemblys in der Kategorie **Erweiterungen**. Andernfalls wechseln Sie zu dem Speicherort, der die heruntergeladenen Clientassemblys enthält (siehe [SharePoint-Clientkomponenten](http://www.microsoft.com/downloads/details.aspx?FamilyID=66da4a3e-e3b0-45d9-9e84-a84946fbf239)).
    
  
7. Fügen Sie in der Datei "Program.cs" die folgenden **using**-Anweisungen hinzu.
    
```cs
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;
```


## <a name="retrieve-the-social-feed-for-a-target-user-by-using-the-sharepoint-net-client-object-model"></a>Abrufen von den Feed für soziale Netzwerke für einen Zielbenutzer mithilfe des Clientobjektmodells für SharePoint.NET
<a name="bkmk_RetrieveFeed"> </a>


1. Deklarieren Sie Variablen für die Server-URL und die Kontoanmeldeinformationen des Zielbenutzers.
    
    ```cs
    const string serverUrl = "http://serverName/";
    const string targetUser = "domainName\\userName";
    ```

    > [!NOTE]
    > Ersetzen Sie unbedingt die Platzhalterwerte `http://serverName/` und `domainName\\userName`, bevor Sie den Code ausführen.
   
2. Initialisieren Sie in der **Main**-Methode den SharePoint-Clientkontext.
    
    ```cs
    ClientContext clientContext = new ClientContext(serverUrl);
    ```

3. Erstellen Sie die  [SocialFeedManager]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx)) -Instanz.
    
    ```cs
    SocialFeedManager feedManager = new SocialFeedManager(clientContext);
    ```

4. Geben Sie die Parameter für den feed Inhalt, den Sie abrufen möchten.
    
    ```cs
    SocialFeedOptions feedOptions = new SocialFeedOptions();
    feedOptions.MaxThreadCount = 10;
    ```

    Die Standardoptionen zurückgeben die ersten 20 Threads im Feed, sortiert nach Datum der letzten Änderung.
  
5. Rufen Sie den Feed des Zielbenutzers ab.
    
    ```cs 
    ClientResult<SocialFeed> feed = feedManager.GetFeedFor(targetUser, feedOptions);
    clientContext.ExecuteQuery();
    ```

    [GetFeedFor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeedFor.aspx)) gibt ein **ClientResult<T>** -Objekt, das die Auflistung der Threads im dessen [Value](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientResult`1.Value.aspx) -Eigenschaft gespeichert werden.
    
  

## <a name="iterate-through-and-read-from-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a>Durchlaufen und Lesen des sozialen Feeds mithilfe des SharePoint .NET-Clientobjektmodells
<a name="bkmk_ReadFeed"> </a>

Der folgende Code durchläuft die Threads im Feed. Es wird überprüft, ob jeder Thread verfügt über das Attribut  [CanReply]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadAttributes.CanReply.aspx)) und ruft dann die Thread-ID und den Text des Beitrags Stamm ab. Der Code auch ein Wörterbuch, das die Thread-ID zu speichern (zu einem Thread Antworten) erstellt und schreibt den Text des Beitrags Stamm in der Konsole angezeigt.

```cs
Dictionary<int, string> idDictionary = new Dictionary<int, string>();
for (int i = 0; i < feed.Value.Threads.Length; i++)
{
    SocialThread thread = feed.Value.Threads[i];
    string postText = thread.RootPost.Text;
    if (thread.Attributes.HasFlag(SocialThreadAttributes.CanReply))
    {
        idDictionary.Add(i, thread.Id);
        Console.WriteLine("\\t" + (i + 1) + ". " + postText);
    }
}
```


## <a name="post-a-reply-to-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a>Bereitstellen Sie eine Antwort auf den Feed für soziale Netzwerke, mit dem .NET SharePoint-Objektmodell
<a name="bkmk_WriteFeed"> </a>


1. (UI-bezogene nur) Rufen Sie den Thread Antworten zu und Aufforderung für Antwort des Benutzers.
    
```cs
Console.Write("Which post number do you want to reply to?  ");
string threadToReplyTo = "";
int threadNumber = int.Parse(Console.ReadLine()) - 1;
idDictionary.TryGetValue(threadNumber, out threadToReplyTo);
Console.Write("Type your reply:  ");
```

2. Definieren Sie die Antwort. Der folgende Code Ruft die Antwort Text aus der Konsolenanwendung ab.
    
```cs
SocialPostCreationData postCreationData = new SocialPostCreationData();
postCreationData.ContentText = Console.ReadLine();
```

3. Veröffentlichen Sie die Antwort. Der _ThreadToReplyTo_-Parameter steht für die [Id]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.Id.aspx))-Eigenschaft des Threads.
    
```cs
feedManager.CreatePost(threadToReplyTo, postCreationData);
clientContext.ExecuteQuery();
```

    > [!NOTE]
    > The  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) method is also used to publish a root post to the current user's feed by passing **null** for the first parameter.

4. (Nur in Bezug auf die Benutzeroberfläche) Beenden Sie das Programm.
    
    ```cs
    Console.WriteLine("Your reply was published.");
    Console.ReadKey(false);
    ```

5. Wählen Sie zum Testen der Konsolenanwendung, klicken Sie auf der Menüleiste **Debuggen**, **Debuggen starten** aus.
    
  

## <a name="code-example-retrieve-a-feed-and-reply-to-a-post-by-using-the-sharepoint-net-client-object-model"></a>Codebeispiel: Abrufen ein Feeds und Antworten auf einen Beitrag mithilfe des Clientobjektmodells für SharePoint.NET
<a name="bkmk_CodeExample"> </a>

Im folgende Beispiel wird der vollständige Code aus der Datei Program.cs.
  
```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace ReadWriteMySite
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the target server running SharePoint and the
            // target thread owner.
            const string serverUrl = "http://serverName/";
            const string targetUser = "domainName\\userName";

            // Connect to the client context.
            ClientContext clientContext = new ClientContext(serverUrl);

            // Get the SocialFeedManager instance.
            SocialFeedManager feedManager = new SocialFeedManager(clientContext);

            // Specify the parameters for the feed content that you want to retrieve.
            SocialFeedOptions feedOptions = new SocialFeedOptions();
            feedOptions.MaxThreadCount = 10;

            // Get the target owner's feed (posts and activities) and then run the request on the server.
            ClientResult<SocialFeed> feed = feedManager.GetFeedFor(targetUser, feedOptions);
            clientContext.ExecuteQuery();

            // Create a dictionary to store the Id property of each thread. This code example stores
            // the ID so a user can select a thread to reply to from the console application.
            Dictionary<int, string> idDictionary = new Dictionary<int, string>();
            for (int i = 0; i < feed.Value.Threads.Length; i++)
            {
                SocialThread thread = feed.Value.Threads[i];

                // Keep only the threads that can be replied to.
                if (thread.Attributes.HasFlag(SocialThreadAttributes.CanReply))
                {
                    idDictionary.Add(i, thread.Id);

                    // Write out the text of the post.
                    Console.WriteLine("\\t" + (i + 1) + ". " + thread.RootPost.Text);
                }
            }
            Console.Write("Which post number do you want to reply to?  ");

            string threadToReplyTo = "";
            int threadNumber = int.Parse(Console.ReadLine()) - 1;
            idDictionary.TryGetValue(threadNumber, out threadToReplyTo);

            Console.Write("Type your reply:  ");

            // Define properties for the reply.
            SocialPostCreationData postCreationData = new SocialPostCreationData();
            postCreationData.ContentText = Console.ReadLine();
            
            // Post the reply and make the changes on the server.
            feedManager.CreatePost(threadToReplyTo, postCreationData);
            clientContext.ExecuteQuery();

            Console.WriteLine("Your reply was published.");
            Console.ReadKey(false);

            // TODO: Add error handling and input validation.
        }
    }
}
```


## <a name="next-steps"></a>Nächste Schritte
<a name="SP15ReadWriteSocial_nextsteps"> </a>

Weitere Informationen zum mehr Aufgaben lesen und Schreiben von Aufgaben mit den Feed für soziale Netzwerke mithilfe des Clientobjektmodells .NET aus, lesen Sie Folgendes ein:
  
    
    

-  [Gewusst wie: Erstellen und Löschen von Beiträgen und Abrufen des sozialen Feeds über das .NET-Clientobjektmodell in SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md)
    
  

## <a name="see-also"></a>Siehe auch
<a name="SP15ReadWriteSocial_addlresources"> </a>


-  [Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [Arbeiten mit sozialen Feeds in SharePoint](work-with-social-feeds-in-sharepoint.md)
    
  

