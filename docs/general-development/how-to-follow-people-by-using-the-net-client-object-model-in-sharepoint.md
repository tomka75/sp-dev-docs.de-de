---
title: Folgen von Personen mithilfe des .NET-Clientobjektmodells in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 0fdb7ca5-d408-4256-b52b-886c4bc3b5b8
ms.openlocfilehash: f910e2cd067ba4cb13d543bc651b779a9a601066
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="follow-people-by-using-the-net-client-object-model-in-sharepoint"></a><span data-ttu-id="4815c-102">Folgen von Personen mithilfe des .NET-Clientobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="4815c-102">How to: Follow people by using the .NET client object model in SharePoint</span></span>

<span data-ttu-id="4815c-103">In diesem Artikel erfahren Sie, wie Sie mithilfe des .NET-Clientobjektmodells in SharePoint mit Features zum Folgen von Personen arbeiten.</span><span class="sxs-lookup"><span data-stu-id="4815c-103">Learn how to work with Following People features by using the SharePoint .NET client object model.</span></span>

## <a name="why-use-following-people-features-in-sharepoint"></a><span data-ttu-id="4815c-104">Gründe für die Verwendung von Features zum Folgen von Personen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="4815c-104">Why use Following People features in SharePoint?</span></span>

<span data-ttu-id="4815c-105">Wenn in SharePoint ein Benutzer Personen folgt, werden die Beiträge und Aktivitäten der gefolgten Personen im Newsfeed des Benutzers angezeigt.</span><span class="sxs-lookup"><span data-stu-id="4815c-105">In SharePoint, when a user follows people, the posts and activities of the followed people show up in the user's newsfeed.</span></span> <span data-ttu-id="4815c-106">Indem Sie Features zum Folgen von Personen nutzen, damit sich Benutzer auf die Personen konzentrieren können, die für sie wichtig sind, können Sie die Relevanz Ihrer App oder Lösung verbessern.</span><span class="sxs-lookup"><span data-stu-id="4815c-106">By using Following People features to focus on the people who users care about, you can improve the relevance of your app or solution.</span></span> <span data-ttu-id="4815c-107">Im .NET-Clientobjektmodell werden Personen, denen Sie folgen, durch [SocialActor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx))-Objekte dargestellt.</span><span class="sxs-lookup"><span data-stu-id="4815c-107">In the .NET client object model, people that you follow are represented by  [SocialActor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx)) objects.</span></span> <span data-ttu-id="4815c-108">Zum Durchführen der Hauptaufgaben zum Folgen von Personen im .NET-Clientobjektmodell verwenden Sie das [SocialFollowingManager]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx))-Objekt.</span><span class="sxs-lookup"><span data-stu-id="4815c-108">To perform core Following People tasks in the .NET client object model, you use the [SocialFollowingManager]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)) object.</span></span> <span data-ttu-id="4815c-109">In diesem Artikel erfahren Sie, wie Sie mithilfe des .NET-Clientobjektmodells mit Features zum Folgen von Personen arbeiten.</span><span class="sxs-lookup"><span data-stu-id="4815c-109">This article shows how to use the .NET client object model to work with Following People features.</span></span>
  
> [!NOTE]
> <span data-ttu-id="4815c-110">Wir konzentrieren uns auf [SocialFollowingManager]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)), da es die grundlegenden Funktionen zum Folgen von Personen und Inhalten konsolidiert.</span><span class="sxs-lookup"><span data-stu-id="4815c-110">Note: We focus on  [SocialFollowingManager]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)) because it consolidates the core functionality for following people and content.</span></span> <span data-ttu-id="4815c-111">Das [PeopleManager]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.aspx))-Objekt enthält jedoch zusätzliche Funktionen zum Folgen von Personen, wie die Methode [AmIFollowedBy(String)]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.AmIFollowedBy.aspx)) und Methoden, die den Folgen-Status anderer Benutzer abrufen.</span><span class="sxs-lookup"><span data-stu-id="4815c-111">However, the [PeopleManager]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.aspx)) object contains additional functionality for following people, such as the [AmIFollowedBy(String)]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.AmIFollowedBy.aspx)) method and methods that obtain the following status of other users.</span></span>
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-following-people-features-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="4815c-112">Voraussetzungen für das Einrichten Ihrer Entwicklungsumgebung zum Arbeiten mit Features zum Folgen von Personen mithilfe des .NET-Clientobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="4815c-112">Prerequisites for setting up your development environment to work with Following People features by using the SharePoint .NET client object model</span></span>

<span data-ttu-id="4815c-113">Zum Erstellen einer Konsolenanwendung, die das .NET-Clientobjektmodell zum Arbeiten mit Features zum Folgen von Personen verwendet, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="4815c-113">To create a console application that uses the .NET client object model to work with Following People features, you'll need the following:</span></span>
  
    
    

- <span data-ttu-id="4815c-114">SharePoint mit konfigurierter „Meine Website“ und mit Benutzerprofilen und persönlichen Websites für den aktuellen Benutzer und einen Zielbenutzer</span><span class="sxs-lookup"><span data-stu-id="4815c-114">SharePoint with My Site configured, and with user profiles and personal sites created for the current user and a target user</span></span>
    
  
- <span data-ttu-id="4815c-115">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="4815c-115">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="4815c-116">Zugriffsberechtigungen vom Typ **Vollzugriff** auf die Benutzerprofil-Dienstanwendung für den angemeldeten Benutzer</span><span class="sxs-lookup"><span data-stu-id="4815c-116">**Full Control** access permissions to the User Profile service application for the logged-on user</span></span>
    
> [!NOTE]
> <span data-ttu-id="4815c-117">Wenn Sie die Entwicklungsaufgaben nicht auf dem Computer durchführen, auf dem SharePoint ausgeführt wird, laden Sie die [SharePoint-Clientkomponenten](http://www.microsoft.com/en-us/download/details.aspx?id=35585) herunter, die die SharePoint-Clientassemblys enthalten.</span><span class="sxs-lookup"><span data-stu-id="4815c-117">[Note:](http://www.microsoft.com/en-us/download/details.aspx?id=35585) If you're not developing on the computer that is running SharePoint, get the  SharePoint Client Components download that contains SharePoint client assemblies.</span></span>
  
    
    


## <a name="create-a-console-application-in-visual-studio-2012"></a><span data-ttu-id="4815c-118">Erstellen einer Konsolenanwendung in Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="4815c-118">Create a console application in Visual Studio 2012</span></span>
<span data-ttu-id="4815c-119"><a name="bkmk_CreateConsoleApp"> </a></span><span class="sxs-lookup"><span data-stu-id="4815c-119"><a name="bkmk_CreateConsoleApp"> </a></span></span>


1. <span data-ttu-id="4815c-120">Öffnen Sie Visual Studio, und wählen Sie **Datei**, **Neu**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="4815c-120">Open Visual Studio, and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="4815c-121">Wählen Sie im Dialogfeld **Neues Projekt** aus der Dropdownliste oben im Dialogfeld die Option **.NET Framework 4.5**.</span><span class="sxs-lookup"><span data-stu-id="4815c-121">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="4815c-122">Klicken Sie in der Liste **Vorlagen** wählen Sie **Windows**, und wählen Sie dann die Vorlage **Konsolenanwendung**.</span><span class="sxs-lookup"><span data-stu-id="4815c-122">In the **Templates** list, choose **Windows**, and then choose the **Console Application** template.</span></span>
    
  
4. <span data-ttu-id="4815c-123">Nennen Sie das Projekt FollowPeopleCSOM, und wählen Sie dann auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="4815c-123">Name the project FollowPeopleCSOM, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="4815c-124">Fügen Sie Verweise auf die folgenden Assemblys hinzu:</span><span class="sxs-lookup"><span data-stu-id="4815c-124">Add references to the following assemblies:</span></span>
    
  - <span data-ttu-id="4815c-125">**Microsoft.SharePoint.Client**</span><span class="sxs-lookup"><span data-stu-id="4815c-125">**Microsoft.SharePoint.Client**</span></span>  
  - <span data-ttu-id="4815c-126">**Microsoft.SharePoint.ClientRuntime**</span><span class="sxs-lookup"><span data-stu-id="4815c-126">**Microsoft.SharePoint.ClientRuntime**</span></span> 
  - <span data-ttu-id="4815c-127">**Microsoft.SharePoint.Client.UserProfiles**</span><span class="sxs-lookup"><span data-stu-id="4815c-127">**Microsoft.SharePoint.Client.UserProfiles**</span></span>
    
  
6. <span data-ttu-id="4815c-128">Ersetzen Sie die Inhalte der **Program**-Klasse durch das Codebeispiel aus einem der folgenden Szenarien:</span><span class="sxs-lookup"><span data-stu-id="4815c-128">Replace the contents of the **Program** class with the code example from one of the following scenarios:</span></span>
    
  -  [<span data-ttu-id="4815c-129">Starten und Beenden von Personen folgen</span><span class="sxs-lookup"><span data-stu-id="4815c-129">Start and stop following people</span></span>](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md#bkmk_FollowPeople)  
  -  [<span data-ttu-id="4815c-130">Nachfolgende Aktivitäten und beobachteter Personen heranziehen.</span><span class="sxs-lookup"><span data-stu-id="4815c-130">Get followers and followed people</span></span>](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md#bkmk_GetFollowednFollowers)
    
  
7. <span data-ttu-id="4815c-131">Wählen Sie zum Testen der Konsolenanwendung, klicken Sie auf der Menüleiste **Debuggen**, **Debuggen starten** aus.</span><span class="sxs-lookup"><span data-stu-id="4815c-131">To test the console application, on the menu bar, choose **Debug**, **Start Debugging**.</span></span>
    
  

## <a name="code-example-start-or-stop-following-people-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="4815c-132">Codebeispiel: Starten oder beenden nach Personen, für die mithilfe des Clientobjektmodells für SharePoint.NET</span><span class="sxs-lookup"><span data-stu-id="4815c-132">Code example: Start or stop following people by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="4815c-133"><a name="bkmk_FollowPeople"> </a></span><span class="sxs-lookup"><span data-stu-id="4815c-133"><a name="bkmk_FollowPeople"> </a></span></span>

<span data-ttu-id="4815c-p103">Im folgenden Codebeispiel wird der aktuelle Benutzer Start nach oder einen Zielbenutzer nach Beenden. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="4815c-p103">The following code example makes the current user start following or stop following a target user. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="4815c-136">Überprüfen Sie, ob der aktuelle Benutzer einen Zielbenutzer folgt, mit der  [IsFollowed]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx)) -Methode.</span><span class="sxs-lookup"><span data-stu-id="4815c-136">Check whether the current user is following a target user by using the  [IsFollowed]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx)) method.</span></span>
    
  
- <span data-ttu-id="4815c-137">Rufen Sie die Anzahl der Personen, die der aktuelle Benutzer mithilfe der Methode  [GetFollowedCount]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx)) folgt.</span><span class="sxs-lookup"><span data-stu-id="4815c-137">Get the count of people who the current user is following by using the  [GetFollowedCount]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx)) method.</span></span>
    
  
- <span data-ttu-id="4815c-138">Starten Sie nach der Zielbenutzer mithilfe der  [Follow]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx)) -Methode.</span><span class="sxs-lookup"><span data-stu-id="4815c-138">Start following the target user by using the  [Follow]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx)) method.</span></span>
    
  
- <span data-ttu-id="4815c-139">Folgen den Zielbenutzer mithilfe der  [StopFollowing]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx)) -Methode nicht mehr.</span><span class="sxs-lookup"><span data-stu-id="4815c-139">Stop following the target user by using the  [StopFollowing]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx)) method.</span></span>
    
  
<span data-ttu-id="4815c-140">Dieses Codebeispiel verwendet das  [SocialFollowResult]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowResult.aspx)) -Objekt, das von der [Follow]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx)) -Methode zu bestimmen, ob das Starten oder beenden, folgen den Zielbenutzer zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="4815c-140">This code example uses the  [SocialFollowResult]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowResult.aspx)) object that is returned by the [Follow]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx)) method to determine whether to start or stop following the target user.</span></span>
  
> [!NOTE]
> <span data-ttu-id="4815c-141">Ändern Sie die Platzhalterwerte für die Variablen **serverUrl** und **targetUser**, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="4815c-141">**Note:** Change the placeholder values for the **serverUrl** and targetUser variables before you run the code.</span></span>
  
    
    




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


## <a name="code-example-get-followers-and-followed-people-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="4815c-142">Codebeispiel: Abrufen von Followern und gefolgten Personen mithilfe des .NET-Clientobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="4815c-142">Code example: Get followers and followed people by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="4815c-143"><a name="bkmk_GetFollowednFollowers"> </a></span><span class="sxs-lookup"><span data-stu-id="4815c-143"><a name="bkmk_GetFollowednFollowers"> </a></span></span>

<span data-ttu-id="4815c-p104">Der folgende Code Beispiel ruft die Personen, die der aktuelle Benutzer folgt, ruft die Personen, gefolgt von den aktuellen Benutzer und ruft Informationen über die folgenden Personen Status des aktuellen Benutzers, ab. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="4815c-p104">The following code example gets the people who the current user is following, gets the people who are followed by the current user, and gets information about the current user's Following People status. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="4815c-146">Überprüfen Sie, ob der aktuelle Benutzer einen Zielbenutzer folgt, mit der  [IsFollowed]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx)) -Methode.</span><span class="sxs-lookup"><span data-stu-id="4815c-146">Check whether the current user is following a target user by using the  [IsFollowed]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx)) method.</span></span>
    
  
- <span data-ttu-id="4815c-147">Rufen Sie die Anzahl der Personen, die der aktuelle Benutzer mithilfe der Methode  [GetFollowedCount]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx)) folgt.</span><span class="sxs-lookup"><span data-stu-id="4815c-147">Get the count of people who the current user is following by using the  [GetFollowedCount]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx)) method.</span></span>
    
  
- <span data-ttu-id="4815c-148">Rufen Sie die Personen, die der aktuelle Benutzer mithilfe der Methode  [GetFollowed]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx)) folgt.</span><span class="sxs-lookup"><span data-stu-id="4815c-148">Get the people who the current user is following by using the  [GetFollowed]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx)) method.</span></span>
    
  
- <span data-ttu-id="4815c-149">Rufen Sie die Personen, die den aktuellen Benutzer mithilfe der Methode  [GetFollowers]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowers.aspx)) folgen.</span><span class="sxs-lookup"><span data-stu-id="4815c-149">Get the people who are following the current user by using the  [GetFollowers]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowers.aspx)) method.</span></span>
    
  
- <span data-ttu-id="4815c-150">Iterieren Sie durch die Gruppen von Personen, und rufen Sie den Anzeigenamen, den persönlichen URI und den Bild-URI jeder Person ab.</span><span class="sxs-lookup"><span data-stu-id="4815c-150">Iterate through the groups of people and get each person's display name, personal URI, and picture URI.</span></span>
    
> [!NOTE]
> <span data-ttu-id="4815c-151">Ändern Sie die Platzhalterwerte für die Variablen **serverUrl** und **targetUser**, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="4815c-151">**Note:** Change the placeholder values for the **serverUrl** and targetUser variables before you run the code.</span></span>
  
    
    


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


## <a name="see-also"></a><span data-ttu-id="4815c-152">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="4815c-152">See also</span></span>
<span data-ttu-id="4815c-153"><a name="bkmk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="4815c-153"><a name="bkmk_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="4815c-154">Folgen von Personen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="4815c-154">Follow people in SharePoint</span></span>](follow-people-in-sharepoint.md)
    
  
-  [<span data-ttu-id="4815c-155">Vorgehensweise: folgen Sie Menschen mit der JavaScript-Objektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="4815c-155">How to: Follow people by using the JavaScript object model in SharePoint</span></span>](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md)
    
  
-  [<span data-ttu-id="4815c-156">Vorgehensweise: Führen Sie Dokumente und Websites mit .NET Client-Objektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="4815c-156">How to: Follow documents and sites by using the .NET client object model in SharePoint</span></span>](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)
    
  

