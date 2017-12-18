---
title: Folgen von Dokumenten und Websites mithilfe des .NET-Client-Objektmodells in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 84366e01-4961-459d-8109-2f1d2d714353
ms.openlocfilehash: 6e6690c40b37b65fe58100f7412e68ee827a970e
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="follow-documents-and-sites-by-using-the-net-client-object-model-in-sharepoint"></a><span data-ttu-id="07e01-102">Folgen von Dokumenten und Websites mithilfe des .NET-Client-Objektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="07e01-102">How to: Follow documents and sites by using the .NET client object model in SharePoint</span></span>

<span data-ttu-id="07e01-103">In diesem Artikel erfahren Sie, wie Sie mithilfe des .NET-Clientobjektmodells in SharePoint mit Features zum Folgen von Inhalten arbeiten.</span><span class="sxs-lookup"><span data-stu-id="07e01-103">Learn how to work with Following Content features by using the SharePoint .NET client object model.</span></span>

## <a name="how-do-i-use-the-net-client-object-model-to-follow-content"></a><span data-ttu-id="07e01-104">Wie verwende ich das .NET-Clientobjektmodell zum Folgen von Inhalten?</span><span class="sxs-lookup"><span data-stu-id="07e01-104">How do I use the .NET client object model to follow content?</span></span>
<span data-ttu-id="07e01-105"><a name="bk_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="07e01-105"><a name="bk_intro"> </a></span></span>

<span data-ttu-id="07e01-106">SharePoint-Benutzer können Dokumenten, Websites und Tags folgen, um Updates zu den Elementen in ihre Newsfeeds abzurufen und gefolgte Dokumente und Websites schnell zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="07e01-106">SharePoint users can follow documents, sites, and tags can follow documents, sites, and tags to get updates about the items in their newsfeeds and to quickly open followed documents and sites.</span></span> <span data-ttu-id="07e01-107">Sie können das .NET-Clientobjektmodell in Ihrer App oder Lösung verwenden, um mit dem Folgen von Inhalten zu beginnen, das Folgen von Inhalten zu beenden und gefolgte Inhalte im Auftrag des aktuellen Benutzers abzurufen.</span><span class="sxs-lookup"><span data-stu-id="07e01-107">You can use the .NET client object model in your app or solution to start following content, stop following content, and get followed content on behalf of the current user.</span></span> <span data-ttu-id="07e01-108">In diesem Artikel erfahren Sie, wie Sie eine Konsolenanwendung erstellen, die das .NET-Clientobjektmodell verwendet, um mit Features zum Folgen von Inhalten für Dokumente und Websites zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="07e01-108">This article shows you how to create a console application that uses the .NET client object model to work with Following Content features for documents and sites.</span></span>
  
    
    
<span data-ttu-id="07e01-109">Die folgenden Objekte sind die primären APIs für Aufgaben zum Folgen von Inhalten:</span><span class="sxs-lookup"><span data-stu-id="07e01-109">The following objects are the primary APIs for Following Content tasks:</span></span>
  
    
    

-  <span data-ttu-id="07e01-110">[SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) bietet Methoden zum Verwalten eines Benutzers Liste besuchter Akteure.</span><span class="sxs-lookup"><span data-stu-id="07e01-110">[SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) provides methods for managing a user's list of followed actors.</span></span>
    
  
-  <span data-ttu-id="07e01-111">[SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) stellt ein Dokument, Website oder Tag, der der Server als Antwort auf eine Anforderung mithilfe der clientseitigen zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="07e01-111">[SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) represents a document, site, or tag that the server returns in response to a client-side request.</span></span>
    
  
-  <span data-ttu-id="07e01-112">[SocialActorInfo](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorInfo.aspx) gibt ein Dokument, Website oder Tag in clientseitige Anforderungen an den Server.</span><span class="sxs-lookup"><span data-stu-id="07e01-112">[SocialActorInfo](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorInfo.aspx) specifies a document, site, or tag in client-side requests to the server.</span></span>
    
  
-  <span data-ttu-id="07e01-113">[Microsoft.SharePoint.Client.Social.SocialActorType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorType.aspx) und [Microsoft.SharePoint.Client.Social.SocialActorTypes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorTypes.aspx) geben Inhaltstypen in clientseitigen Anforderungen an den Server an.</span><span class="sxs-lookup"><span data-stu-id="07e01-113">[Microsoft.SharePoint.Client.Social.SocialActorType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorType.aspx) and [Microsoft.SharePoint.Client.Social.SocialActorTypes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorTypes.aspx) specify content types in client-side requests to the server.</span></span>
    
  

> <span data-ttu-id="07e01-114">**Hinweis:** Sie verwenden diese APIs auch für Aufgaben zum Folgen von Personen, allerdings unterstützen die Methoden **GetSuggestions** und **GetFollowers**, die über [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) verfügbar sind, nur das Folgen von Personen, nicht von Inhalten.</span><span class="sxs-lookup"><span data-stu-id="07e01-114">**Note:** You also use these APIs for Following People tasks, but the **GetSuggestions** and **GetFollowers** methods available from [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) only support following people, not content.</span></span> <span data-ttu-id="07e01-115">Weitere Informationen zur Verwendung von [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) finden Sie unter [Folgen von Inhalten in SharePoint](follow-content-in-sharepoint.md) und [Folgen von Personen in SharePoint](follow-people-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="07e01-115">For more information about how you can use [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) , see [Follow content in SharePoint](follow-content-in-sharepoint.md) and [Follow people in SharePoint](follow-people-in-sharepoint.md).</span></span> <span data-ttu-id="07e01-116">Codebeispiele zum Folgen von Personen finden Sie unter [Vorgehensweise: Folgen von Personen mithilfe des .NET-Clientobjektmodells in SharePoint](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="07e01-116">For code examples that show how to follow people, see  [How to: Follow people by using the .NET client object model in SharePoint](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md).</span></span> 
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-following-content-features-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="07e01-117">Voraussetzungen für das Einrichten Ihrer Entwicklungsumgebung zum Arbeiten mit Features zum Folgen von Inhalten mithilfe des .NET-Clientobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="07e01-117">Prerequisites for setting up your development environment to work with Following Content features by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="07e01-118"><a name="bkmk_SetUpDevEnv"> </a></span><span class="sxs-lookup"><span data-stu-id="07e01-118"><a name="bkmk_SetUpDevEnv"> </a></span></span>

<span data-ttu-id="07e01-119">Um eine Konsolenanwendung erstellen, die das Clientobjektmodell .NET verwendet folgende Inhaltsfunktionen für Dokumente und Websites entwickelt, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="07e01-119">To create a console application that uses the .NET client object model to work with Following Content features for documents and sites, you'll need the following:</span></span>
  
    
    

- <span data-ttu-id="07e01-120">SharePoint mit konfigurierter „Meine Website“, mit erstellter Website „Meine Website“ für den aktuellen Benutzer und mit einem in eine SharePoint-Dokumentbibliothek hochgeladenen Dokument</span><span class="sxs-lookup"><span data-stu-id="07e01-120">SharePoint with My Site configured, with the My Site site created for the current user, and with a document uploaded to a SharePoint document library</span></span>
    
  
- <span data-ttu-id="07e01-121">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="07e01-121">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="07e01-122">Zugriffsberechtigungen vom Typ **Vollzugriff** auf die Benutzerprofil-Dienstanwendung für den angemeldeten Benutzer</span><span class="sxs-lookup"><span data-stu-id="07e01-122">**Full Control** access permissions to the User Profile service application for the logged-on user</span></span>
    
  

> <span data-ttu-id="07e01-123">**Hinweis:** Wenn Sie die Entwicklungsaufgaben nicht auf dem Computer durchführen, auf dem SharePoint ausgeführt wird, laden Sie die [SharePoint-Clientkomponenten](http://www.microsoft.com/en-us/download/details.aspx?id=35585) herunter, die die SharePoint-Clientassemblys enthalten.</span><span class="sxs-lookup"><span data-stu-id="07e01-123">**Note:** If you are not developing on the computer that is running SharePoint, get the  [SharePoint Client Components](http://www.microsoft.com/en-us/download/details.aspx?id=35585) download that contains SharePoint client assemblies.</span></span>
  
    
    


## <a name="create-a-console-application-to-work-with-following-content-features-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="07e01-124">Erstellen einer Konsolenanwendung zum Arbeiten mit Features zum Folgen von Inhalten mithilfe des .NET_Clientobjektmodells für SharePoint</span><span class="sxs-lookup"><span data-stu-id="07e01-124">Create a console application to work with Following Content features by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="07e01-125"><a name="bkmk_CreateConsoleApp"> </a></span><span class="sxs-lookup"><span data-stu-id="07e01-125"><a name="bkmk_CreateConsoleApp"> </a></span></span>


1. <span data-ttu-id="07e01-126">Wählen Sie in Visual Studio die Optionen **Datei**, **Neu**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="07e01-126">In Visual Studio, choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="07e01-127">Wählen Sie im Dialogfeld **Neues Projekt** aus der Dropdownliste oben im Dialogfeld die Option **.NET Framework 4.5**.</span><span class="sxs-lookup"><span data-stu-id="07e01-127">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="07e01-128">Klicken Sie in der Liste **Vorlagen** wählen Sie **Windows**, und wählen Sie dann die Vorlage **Konsolenanwendung**.</span><span class="sxs-lookup"><span data-stu-id="07e01-128">In the **Templates** list, choose **Windows**, and then choose the **Console Application** template.</span></span>
    
  
4. <span data-ttu-id="07e01-129">Nennen Sie das Projekt FollowContentCSOM, und wählen Sie dann auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="07e01-129">Name the project FollowContentCSOM, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="07e01-130">Fügen Sie Verweise auf die folgenden Assemblys hinzu:</span><span class="sxs-lookup"><span data-stu-id="07e01-130">Add references to the following assemblies:</span></span>
    
  - <span data-ttu-id="07e01-131">**Microsoft.SharePoint.Client**</span><span class="sxs-lookup"><span data-stu-id="07e01-131">**Microsoft.SharePoint.Client**</span></span>   
  - <span data-ttu-id="07e01-132">**Microsoft.SharePoint.ClientRuntime**</span><span class="sxs-lookup"><span data-stu-id="07e01-132">**Microsoft.SharePoint.ClientRuntime**</span></span>
  - <span data-ttu-id="07e01-133">**Microsoft.SharePoint.Client.UserProfiles**</span><span class="sxs-lookup"><span data-stu-id="07e01-133">**Microsoft.SharePoint.Client.UserProfiles**</span></span>
    
6. <span data-ttu-id="07e01-134">Ersetzen Sie die Inhalte der **Program**-Klasse durch das Codebeispiel aus einem der folgenden Szenarien:</span><span class="sxs-lookup"><span data-stu-id="07e01-134">Replace the contents of the **Program** class with the code example from one of the following scenarios:</span></span>
    
  -  [<span data-ttu-id="07e01-135">Starten Sie und beenden Sie die folgenden Inhalte</span><span class="sxs-lookup"><span data-stu-id="07e01-135">Start and stop following content</span></span>](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md#bkmk_FollowContent)  
  -  [<span data-ttu-id="07e01-136">Abrufen von verfolgten Inhalt für den aktuellen Benutzer</span><span class="sxs-lookup"><span data-stu-id="07e01-136">Get followed content for the current user</span></span>](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md#bkmk_GetFollowed)
    
7. <span data-ttu-id="07e01-137">Wählen Sie zum Testen der Konsolenanwendung, klicken Sie auf der Menüleiste **Debuggen**, **Debuggen starten** aus.</span><span class="sxs-lookup"><span data-stu-id="07e01-137">To test the console application, on the menu bar, choose **Debug**, **Start Debugging**.</span></span>
    
  

## <a name="code-example-start-and-stop-following-content-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="07e01-138">Codebeispiel: Starten und beenden nach Inhalt mithilfe des Clientobjektmodells für SharePoint.NET</span><span class="sxs-lookup"><span data-stu-id="07e01-138">Code example: Start and stop following content by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="07e01-139"><a name="bkmk_FollowContent"> </a></span><span class="sxs-lookup"><span data-stu-id="07e01-139"><a name="bkmk_FollowContent"> </a></span></span>

<span data-ttu-id="07e01-p103">Im folgenden Codebeispiel wird der aktuelle Benutzer Start nach oder nach einem Zielelement beenden. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="07e01-p103">The following code example makes the current user start following or stop following a target item. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="07e01-142">Überprüfen Sie, ob der aktuelle Benutzer ein bestimmtes Dokument oder Website folgt mithilfe der  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) -Methode.</span><span class="sxs-lookup"><span data-stu-id="07e01-142">Check whether the current user is following a particular document or site by using the  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) method.</span></span>
    
  
- <span data-ttu-id="07e01-143">Starten Sie nach einem Dokument oder einer Website mithilfe der  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) -Methode.</span><span class="sxs-lookup"><span data-stu-id="07e01-143">Start following a document or site by using the  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) method.</span></span>
    
  
- <span data-ttu-id="07e01-144">Beenden Sie nach einem Dokument oder einer Website mithilfe der  [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) -Methode.</span><span class="sxs-lookup"><span data-stu-id="07e01-144">Stop following a document or site by using the  [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) method.</span></span>
    
  
- <span data-ttu-id="07e01-145">Rufen Sie die Anzahl von Dokumenten oder Websites, die der aktuelle Benutzer mithilfe der Methode  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) folgt.</span><span class="sxs-lookup"><span data-stu-id="07e01-145">Get the count of documents or sites that the current user is following by using the  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) method.</span></span>
    
  
<span data-ttu-id="07e01-146">Dieses Codebeispiel verwendet das  [SocialFollowResult](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowResult.aspx) -Objekt, das von der [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) -Methode, um festzustellen, ob starten oder beenden Sie das Zielelement folgt zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="07e01-146">This code example uses the  [SocialFollowResult](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowResult.aspx) object that is returned by the [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) method to determine whether to start or stop following the target item.</span></span>
  
    
    

> <span data-ttu-id="07e01-147">**Hinweis:** Ändern Sie die Platzhalterwerte für die Variablen **serverUrl** und **contentUrl**, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="07e01-147">**Note:** Change the placeholder values for the **serverUrl** and **contentUrl** variables before you run the code.</span></span> <span data-ttu-id="07e01-148">Wenn Sie eine Website anstelle eines Dokuments verwenden möchten, verwenden Sie die auskommentierten Variablen.</span><span class="sxs-lookup"><span data-stu-id="07e01-148">To use a site instead of a document, use the variables that are commented out.</span></span>
  
    
    




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


## <a name="code-example-get-followed-content-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="07e01-149">Codebeispiel: Abrufen von gefolgten Inhalten mithilfe des .NET-Clientobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="07e01-149">Code example: Get followed content by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="07e01-150"><a name="bkmk_GetFollowed"> </a></span><span class="sxs-lookup"><span data-stu-id="07e01-150"><a name="bkmk_GetFollowed"> </a></span></span>

<span data-ttu-id="07e01-p105">Im folgenden Codebeispiel wird dient zum Abrufen der Dokumente und Websites, dass der aktuelle Benutzer folgt und ruft Informationen zum Status des folgenden Inhalts des Benutzers ab. Außerdem wird gezeigt, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="07e01-p105">The following code example gets the documents and sites that the current user is following and gets information about the user's Following Content status. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="07e01-153">Überprüfen Sie, ob der aktuelle Benutzer das Zieldokument und Website folgt mithilfe der  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) -Methode.</span><span class="sxs-lookup"><span data-stu-id="07e01-153">Check whether the current user is following the target document and site by using the  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) method.</span></span>
    
  
- <span data-ttu-id="07e01-154">Rufen Sie die Anzahl von Dokumenten und Websites, die der aktuelle Benutzer mithilfe der Methode  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) folgt.</span><span class="sxs-lookup"><span data-stu-id="07e01-154">Get the count of documents and sites that the current user is following by using the  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) method.</span></span>
    
  
- <span data-ttu-id="07e01-155">Rufen Sie die Dokumente und Websites, die der aktuelle Benutzer mithilfe der Methode  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx) folgt.</span><span class="sxs-lookup"><span data-stu-id="07e01-155">Get the documents and sites that the current user is following by using the  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx) method.</span></span>
    
  
- <span data-ttu-id="07e01-156">Iterieren Sie durch die Inhaltsgruppen, und rufen Sie den Namen, den Inhalts-URI und den URI jedes Elements ab.</span><span class="sxs-lookup"><span data-stu-id="07e01-156">Iterate through the groups of content and get each item's name, content URI, and URI.</span></span>
    
  

> <span data-ttu-id="07e01-157">**Hinweis:** Ändern Sie den Platzhalterwert für die Variablen **serverUrl**, **docContentUrl** und **siteContentUrl**, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="07e01-157">**Note:** Change the placeholder value for the **serverUrl**, **docContentUrl**, and **siteContentUrl** variables before you run the code.</span></span>
  
    
    


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


## <a name="additional-resources"></a><span data-ttu-id="07e01-158">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="07e01-158">Additional resources</span></span>
<span data-ttu-id="07e01-159"><a name="bkmk_AddtionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="07e01-159"><a name="bkmk_AddtionalResources"> </a></span></span>


-  [<span data-ttu-id="07e01-160">Folgen von Inhalten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="07e01-160">Follow content in SharePoint</span></span>](follow-content-in-sharepoint.md)
    
  
-  [<span data-ttu-id="07e01-161">Vorgehensweise: führen Sie Dokumente, Websites und Tags mithilfe des REST-Diensts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="07e01-161">How to: Follow documents, sites, and tags by using the REST service in SharePoint</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)
    
  
-  [<span data-ttu-id="07e01-162">Vorgehensweise: führen Sie die Personen mithilfe des clientobjektmodells .NET SharePoint</span><span class="sxs-lookup"><span data-stu-id="07e01-162">How to: Follow people by using the .NET client object model in SharePoint</span></span>](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md)
    
  

