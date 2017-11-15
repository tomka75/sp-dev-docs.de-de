---
title: "Vorgehensweise führen Sie die Personen mithilfe des clientobjektmodells .NET SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 0fdb7ca5-d408-4256-b52b-886c4bc3b5b8
ms.openlocfilehash: 3c097c476f3bb020a26f0baf9b2dcdb23babb1a3
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint"></a><span data-ttu-id="80899-102">Vorgehensweise: Folgen von Personen mithilfe des .NET-Clientobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="80899-102">How to: Follow people by using the .NET client object model in SharePoint</span></span>
<span data-ttu-id="80899-103">In diesem Artikel erfahren Sie, wie Sie mithilfe des .NET-Clientobjektmodells in SharePoint mit Features zum Folgen von Personen arbeiten.</span><span class="sxs-lookup"><span data-stu-id="80899-103">Learn how to work with Following People features by using the SharePoint Server 2013 .NET client object model.</span></span>
## <a name="why-use-following-people-features-in-sharepoint"></a><span data-ttu-id="80899-104">Gründe für die Verwendung von Features zum Folgen von Personen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="80899-104">Why use Following People features in SharePoint Server 2013?</span></span>

<span data-ttu-id="80899-105">Wenn in SharePoint ein Benutzer Personen folgt, werden die Beiträge und Aktivitäten der gefolgten Personen im Newsfeed des Benutzers angezeigt.</span><span class="sxs-lookup"><span data-stu-id="80899-105">In SharePoint, when a user follows people, the posts and activities of the followed people show up in the user's newsfeed.</span></span> <span data-ttu-id="80899-106">Indem Sie Features zum Folgen von Personen nutzen, damit sich Benutzer auf die Personen konzentrieren können, die für sie wichtig sind, können Sie die Relevanz Ihrer App oder Lösung verbessern.</span><span class="sxs-lookup"><span data-stu-id="80899-106">By using Following People features to focus on the people who users care about, you can improve the relevance of your app or solution.</span></span> <span data-ttu-id="80899-107">Im .NET-Clientobjektmodell werden Personen, denen Sie folgen, durch [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx)-Objekte dargestellt.</span><span class="sxs-lookup"><span data-stu-id="80899-107">In the .NET client object model, people that you follow are represented by  [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) objects.</span></span> <span data-ttu-id="80899-108">Zum Durchführen der Hauptaufgaben zum Folgen von Personen im .NET-Clientobjektmodell verwenden Sie das [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)-Objekt.</span><span class="sxs-lookup"><span data-stu-id="80899-108">To perform core Following People tasks in the .NET client object model, you use the [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) object.</span></span> <span data-ttu-id="80899-109">In diesem Artikel erfahren Sie, wie Sie mithilfe des .NET-Clientobjektmodells mit Features zum Folgen von Personen arbeiten.</span><span class="sxs-lookup"><span data-stu-id="80899-109">This article shows how to use the .NET client object model to work with Following People features.</span></span>
  
    
    

> <span data-ttu-id="80899-110">**Hinweis:** Wir konzentrieren uns auf [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx), da es die grundlegenden Funktionen zum Folgen von Personen und Inhalten konsolidiert.</span><span class="sxs-lookup"><span data-stu-id="80899-110">**Note:** We focus on  [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) because it consolidates the core functionality for following people and content.</span></span> <span data-ttu-id="80899-111">Das [PeopleManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.aspx)-Objekt enthält jedoch zusätzliche Funktionen zum Folgen von Personen, wie die Methode [AmIFollowedBy(String)](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.AmIFollowedBy.aspx) und Methoden, die den Folgen-Status anderer Benutzer abrufen.</span><span class="sxs-lookup"><span data-stu-id="80899-111">Note We focus on  SocialFollowingManager because it consolidates the core functionality for following people and content. However, the [PeopleManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.aspx) object contains additional functionality for following people, such as the [AmIFollowedBy(String)](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.AmIFollowedBy.aspx) method and methods that obtain the following status of other users.</span></span>
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-following-people-features-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="80899-112">Voraussetzungen für das Einrichten Ihrer Entwicklungsumgebung zum Arbeiten mit Features zum Folgen von Personen mithilfe des .NET-Clientobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="80899-112">Prerequisites for setting up your development environment to work with Following People features by using the SharePoint .NET client object model</span></span>

<span data-ttu-id="80899-113">Zum Erstellen einer Konsolenanwendung, die das .NET-Clientobjektmodell zum Arbeiten mit Features zum Folgen von Personen verwendet, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="80899-113">To create a console application that uses the .NET client object model to work with Following People features, you'll need the following:</span></span>
  
    
    

- <span data-ttu-id="80899-114">SharePoint mit konfigurierter „Meine Website“ und mit Benutzerprofilen und persönlichen Websites für den aktuellen Benutzer und einen Zielbenutzer</span><span class="sxs-lookup"><span data-stu-id="80899-114">SharePoint Server 2013 with My Site configured, and with user profiles and personal sites created for the current user and a target user</span></span>
    
  
- <span data-ttu-id="80899-115">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="80899-115">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="80899-116">Zugriffsberechtigungen vom Typ **Vollzugriff** auf die Benutzerprofil-Dienstanwendung für den angemeldeten Benutzer</span><span class="sxs-lookup"><span data-stu-id="80899-116">**Full Control** access permissions to the User Profile service application for the logged-on user</span></span>
    
  

> <span data-ttu-id="80899-117">**Hinweis:** Wenn Sie die Entwicklungsaufgaben nicht auf dem Computer durchführen, auf dem SharePoint ausgeführt wird, laden Sie die [SharePoint-Clientkomponenten](http://www.microsoft.com/en-us/download/details.aspx?id=35585) herunter, die die SharePoint-Clientassemblys enthalten.</span><span class="sxs-lookup"><span data-stu-id="80899-117">**Note** If you're not developing on the computer that is running SharePoint Server 2013, get the  [SharePoint Client Components](http://www.microsoft.com/en-us/download/details.aspx?id=35585) download that contains SharePoint client assemblies.</span></span>
  
    
    


## <a name="create-a-console-application-in-visual-studio-2012"></a><span data-ttu-id="80899-118">Erstellen einer Konsolenanwendung in Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="80899-118">Create a console application in Visual Studio 2012</span></span>
<span data-ttu-id="80899-119"><a name="bkmk_CreateConsoleApp"> </a></span><span class="sxs-lookup"><span data-stu-id="80899-119"></span></span>


1. <span data-ttu-id="80899-120">Öffnen Sie Visual Studio, und wählen Sie **Datei**, **Neu**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="80899-120">Open Visual Studio, and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="80899-121">Wählen Sie im Dialogfeld **Neues Projekt** aus der Dropdownliste oben im Dialogfeld die Option **.NET Framework 4.5**.</span><span class="sxs-lookup"><span data-stu-id="80899-121">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="80899-122">Klicken Sie in der Liste **Vorlagen** wählen Sie **Windows**, und wählen Sie dann die Vorlage **Konsolenanwendung**.</span><span class="sxs-lookup"><span data-stu-id="80899-122">In the **Templates** list, choose **Windows**, and then choose the **Console Application** template.</span></span>
    
  
4. <span data-ttu-id="80899-123">Nennen Sie das Projekt FollowPeopleCSOM, und wählen Sie dann auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="80899-123">Name the project FollowPeopleCSOM, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="80899-124">Fügen Sie Verweise auf die folgenden Assemblys hinzu:</span><span class="sxs-lookup"><span data-stu-id="80899-124">Add references to the following assemblies:</span></span>
    
  - <span data-ttu-id="80899-125">**Microsoft.SharePoint.Client**</span><span class="sxs-lookup"><span data-stu-id="80899-125">**Microsoft.SharePoint.Client**</span></span>  
  - <span data-ttu-id="80899-126">**Microsoft.SharePoint.ClientRuntime**</span><span class="sxs-lookup"><span data-stu-id="80899-126">**Microsoft.SharePoint.ClientRuntime**</span></span> 
  - <span data-ttu-id="80899-127">**Microsoft.SharePoint.Client.UserProfiles**</span><span class="sxs-lookup"><span data-stu-id="80899-127">Primary namespace:            **Microsoft.SharePoint.Client.UserProfiles**</span></span>
    
  
6. <span data-ttu-id="80899-128">Ersetzen Sie die Inhalte der **Program**-Klasse durch das Codebeispiel aus einem der folgenden Szenarien:</span><span class="sxs-lookup"><span data-stu-id="80899-128">Replace the contents of the **Program** class with the code example from one of the following scenarios:</span></span>
    
  -  [<span data-ttu-id="80899-129">Starten und Beenden von Personen folgen</span><span class="sxs-lookup"><span data-stu-id="80899-129">Start and stop following people</span></span>](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md#bkmk_FollowPeople)  
  -  [<span data-ttu-id="80899-130">Nachfolgende Aktivitäten und beobachteter Personen heranziehen.</span><span class="sxs-lookup"><span data-stu-id="80899-130">Get followers and followed people</span></span>](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md#bkmk_GetFollowednFollowers)
    
  
7. <span data-ttu-id="80899-131">Wählen Sie zum Testen der Konsolenanwendung, klicken Sie auf der Menüleiste **Debuggen**, **Debuggen starten** aus.</span><span class="sxs-lookup"><span data-stu-id="80899-131">To test the console application, on the menu bar, choose **Debug**, **Start Debugging**.</span></span>
    
  

## <a name="code-example-start-or-stop-following-people-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="80899-132">Codebeispiel: Starten oder beenden nach Personen, für die mithilfe des Clientobjektmodells für SharePoint.NET</span><span class="sxs-lookup"><span data-stu-id="80899-132">Code example: Start or stop following people by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="80899-133"><a name="bkmk_FollowPeople"> </a></span><span class="sxs-lookup"><span data-stu-id="80899-133"></span></span>

<span data-ttu-id="80899-p103">Im folgenden Codebeispiel wird der aktuelle Benutzer Start nach oder einen Zielbenutzer nach Beenden. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="80899-p103">The following code example makes the current user start following or stop following a target user. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="80899-136">Überprüfen Sie, ob der aktuelle Benutzer einen Zielbenutzer folgt, mit der  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) -Methode.</span><span class="sxs-lookup"><span data-stu-id="80899-136">Check whether the current user is following a target user by using the  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) method.</span></span>
    
  
- <span data-ttu-id="80899-137">Rufen Sie die Anzahl der Personen, die der aktuelle Benutzer mithilfe der Methode  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) folgt.</span><span class="sxs-lookup"><span data-stu-id="80899-137">Get the count of people who the current user is following by using the  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) method.</span></span>
    
  
- <span data-ttu-id="80899-138">Starten Sie nach der Zielbenutzer mithilfe der  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) -Methode.</span><span class="sxs-lookup"><span data-stu-id="80899-138">Start following the target user by using the  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) method.</span></span>
    
  
- <span data-ttu-id="80899-139">Folgen den Zielbenutzer mithilfe der  [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) -Methode nicht mehr.</span><span class="sxs-lookup"><span data-stu-id="80899-139">Stop following the target user by using the  [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) method.</span></span>
    
  
<span data-ttu-id="80899-140">Dieses Codebeispiel verwendet das  [SocialFollowResult](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowResult.aspx) -Objekt, das von der [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) -Methode zu bestimmen, ob das Starten oder beenden, folgen den Zielbenutzer zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="80899-140">This code example uses the  [SocialFollowResult](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowResult.aspx) object that is returned by the [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) method to determine whether to start or stop following the target user.</span></span>
  
    
    

> <span data-ttu-id="80899-141">**Hinweis:** Ändern Sie die Platzhalterwerte für die Variablen **serverUrl** und **targetUser**, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="80899-141">**Note** Change the placeholder values for the **serverUrl** and **targetUser** variables before you run the code.</span></span>
  
    
    




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


## <a name="code-example-get-followers-and-followed-people-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="80899-142">Codebeispiel: Abrufen von Followern und gefolgten Personen mithilfe des .NET-Clientobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="80899-142">Code example: Get followers and followed people by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="80899-143"><a name="bkmk_GetFollowednFollowers"> </a></span><span class="sxs-lookup"><span data-stu-id="80899-143"></span></span>

<span data-ttu-id="80899-p104">Der folgende Code Beispiel ruft die Personen, die der aktuelle Benutzer folgt, ruft die Personen, gefolgt von den aktuellen Benutzer und ruft Informationen über die folgenden Personen Status des aktuellen Benutzers, ab. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="80899-p104">The following code example gets the people who the current user is following, gets the people who are followed by the current user, and gets information about the current user's Following People status. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="80899-146">Überprüfen Sie, ob der aktuelle Benutzer einen Zielbenutzer folgt, mit der  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) -Methode.</span><span class="sxs-lookup"><span data-stu-id="80899-146">Check whether the current user is following a target user by using the  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) method.</span></span>
    
  
- <span data-ttu-id="80899-147">Rufen Sie die Anzahl der Personen, die der aktuelle Benutzer mithilfe der Methode  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) folgt.</span><span class="sxs-lookup"><span data-stu-id="80899-147">Get the count of people who the current user is following by using the  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) method.</span></span>
    
  
- <span data-ttu-id="80899-148">Rufen Sie die Personen, die der aktuelle Benutzer mithilfe der Methode  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx) folgt.</span><span class="sxs-lookup"><span data-stu-id="80899-148">Get the people who the current user is following by using the  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx) method.</span></span>
    
  
- <span data-ttu-id="80899-149">Rufen Sie die Personen, die den aktuellen Benutzer mithilfe der Methode  [GetFollowers](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowers.aspx) folgen.</span><span class="sxs-lookup"><span data-stu-id="80899-149">Get the people who are following the current user by using the  [GetFollowers](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowers.aspx) method.</span></span>
    
  
- <span data-ttu-id="80899-150">Iterieren Sie durch die Gruppen von Personen, und rufen Sie den Anzeigenamen, den persönlichen URI und den Bild-URI jeder Person ab.</span><span class="sxs-lookup"><span data-stu-id="80899-150">Iterate through the groups of people and get each person's display name, personal URI, and picture URI.</span></span>
    
  

> <span data-ttu-id="80899-151">**Hinweis:** Ändern Sie die Platzhalterwerte für die Variablen **serverUrl** und **targetUser**, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="80899-151">**Note** Change the placeholder values for the **serverUrl** and **targetUser** variables before you run the code.</span></span>
  
    
    


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


## <a name="additional-resources"></a><span data-ttu-id="80899-152">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="80899-152">Additional resources</span></span>
<span data-ttu-id="80899-153"><a name="bkmk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="80899-153"></span></span>


-  [<span data-ttu-id="80899-154">Folgen von Personen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="80899-154">Follow people in SharePoint</span></span>](follow-people-in-sharepoint.md)
    
  
-  [<span data-ttu-id="80899-155">Vorgehensweise: folgen Sie Menschen mit der JavaScript-Objektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="80899-155">How to: Follow people by using the JavaScript object model in SharePoint</span></span>](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md)
    
  
-  [<span data-ttu-id="80899-156">Vorgehensweise: Führen Sie Dokumente und Websites mit .NET Client-Objektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="80899-156">How to: Follow documents and sites by using the .NET client object model in SharePoint</span></span>](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)
    
  

