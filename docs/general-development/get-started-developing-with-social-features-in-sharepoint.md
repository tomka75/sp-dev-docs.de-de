---
title: Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8852ce36-8309-45a7-a141-2e10ac17a123
ms.openlocfilehash: c8ecb5d92ed472137c5053dcb46e81b6d7e72f5f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="get-started-developing-with-social-features-in-sharepoint"></a><span data-ttu-id="ed530-102">Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-102">Get started developing with social features in SharePoint</span></span>
<span data-ttu-id="ed530-103">Erste Schritte zum Programmieren mit sozialen Feeds von SharePoint und Mikroblogeinträgen, Folgen von Personen und Inhalten (Dokumente, Websites und Tags) und Arbeiten mit Benutzerprofilen.</span><span class="sxs-lookup"><span data-stu-id="ed530-103">Get started programming with SharePoint social feeds and microblog posts, following people and content (documents, sites, and tags), and working with user profiles.</span></span>

    
 [<span data-ttu-id="ed530-104">Wie kann ich in sozialen Netzwerken Apps und Lösungen verwenden?</span><span class="sxs-lookup"><span data-stu-id="ed530-104">How can I use social features in apps and solutions?</span></span>](get-started-developing-with-social-features-in-sharepoint.md#bk_HowToUseSocialFeatures)
  
    
    
 [<span data-ttu-id="ed530-105">Einrichten der Entwicklungsumgebung</span><span class="sxs-lookup"><span data-stu-id="ed530-105">Setting up the development environment</span></span>](get-started-developing-with-social-features-in-sharepoint.md#DevEnvironment)
  
    
    
 [<span data-ttu-id="ed530-106">Entwicklungsszenarien für Features für soziale Netzwerke</span><span class="sxs-lookup"><span data-stu-id="ed530-106">Development scenarios for social features</span></span>](get-started-developing-with-social-features-in-sharepoint.md#DevScenarios)
  
    
    
 [<span data-ttu-id="ed530-107">Vorgehensweisen für die Programmierung mit Features für soziale Netzwerke</span><span class="sxs-lookup"><span data-stu-id="ed530-107">How-tos for programming with social features</span></span>](get-started-developing-with-social-features-in-sharepoint.md#bk_GetStarted)
  
    
    
 [<span data-ttu-id="ed530-108">APIs für die Programmierung mit Features für soziale Netzwerke</span><span class="sxs-lookup"><span data-stu-id="ed530-108">APIs for programming with social features</span></span>](get-started-developing-with-social-features-in-sharepoint.md#SocialApis)
  
    
    
 [<span data-ttu-id="ed530-109">App-Berechtigungsanforderungen für den Zugriff auf Features für soziale Netzwerke</span><span class="sxs-lookup"><span data-stu-id="ed530-109">App permission requests for accessing social features</span></span>](get-started-developing-with-social-features-in-sharepoint.md#bkmk_AppPerms)
  
    
    
 [<span data-ttu-id="ed530-110">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="ed530-110">Additional resources</span></span>](get-started-developing-with-social-features-in-sharepoint.md#bk_AddResources)
  
    
    


## <a name="how-can-i-use-social-features-in-sharepoint-apps-and-solutions"></a><span data-ttu-id="ed530-111">Wie kann ich Features für soziale Netzwerke in SharePoint apps und -Lösungen verwenden?</span><span class="sxs-lookup"><span data-stu-id="ed530-111">How can I use social features in SharePoint apps and solutions?</span></span>
<span data-ttu-id="ed530-112"><a name="bk_HowToUseSocialFeatures"> </a></span><span class="sxs-lookup"><span data-stu-id="ed530-112"><a name="bk_HowToUseSocialFeatures"> </a></span></span>

<span data-ttu-id="ed530-p101">Features für soziale Netzwerke in SharePoint apps und -Lösungen können Benutzer eine Verbindung herstellen, für die Kommunikation und Zusammenarbeit miteinander und finden, nachverfolgen und wichtige Inhalte und Informationen freigeben verbessern. Sie können neue Features für soziale Netzwerke hinzufügen oder erweitern die Funktionen, die bereits in SharePoint verfügbar sind. Beispielsweise können Sie eine app erstellen, mit die Sie suchen und führen Sie die Personen, die ein gemeinsames Interesse haben, erstellen Sie eine benutzerdefinierte Visualisierung der feed-Daten oder benutzerdefinierte Aktivitäten Sie den Feed veröffentlichen können.</span><span class="sxs-lookup"><span data-stu-id="ed530-p101">Social features in SharePoint apps and solutions can help people to connect, communicate, and collaborate with each other and find, track, and share important content and information. You can add new social features or extend the features that are already available in SharePoint. For example, you can create an app that lets you find and follow people who have a common interest, create a custom visualization of feed data, or publish custom activities to the feed.</span></span>
  
    
    
<span data-ttu-id="ed530-p102">In diesem Artikel beschriebenen Features Ausrichten der Personen, Feeds und folgende Funktionalität, die auf persönliche Websites und Teamwebsites hilfreich. Das Forum Erfahrungen und Reputation Modell auf Community-Websites nicht verfügbar machen eine bestimmte API, sodass Sie mit SharePoint-Website und Liste APIs direkt an um die Funktionalität zu erweitern. Weitere Informationen finden Sie unter  [neue Community-Website-Feature](what-s-new-for-developers-in-social-and-collaboration-features-in-sharepoint-201.md#bkmk_Collab).</span><span class="sxs-lookup"><span data-stu-id="ed530-p102">The features described in this article align to the people, feeds, and following functionality that you find on personal sites and team sites. The forum experience and reputation model on Community Sites don't expose a specific API, so you use SharePoint site and list APIs directly to extend that functionality. For more information, see  [New Community Site feature](what-s-new-for-developers-in-social-and-collaboration-features-in-sharepoint-201.md#bkmk_Collab).</span></span>
  
    
    
<span data-ttu-id="ed530-119">Bevor Sie mit der Entwicklung beginnen, sollten Sie wissen, wo der Code ausgeführt wird, in welcher SharePoint-Umgebung er ausgeführt wird und welche Funktionen er bereitstellen soll.</span><span class="sxs-lookup"><span data-stu-id="ed530-119">Before you start developing, you should know where your code will run, what SharePoint environment it will run on, and what functionality it will provide.</span></span> <span data-ttu-id="ed530-120">Diese Faktoren helfen Ihnen zu entscheiden, welche Art von App Sie erstellen und welche API oder APIs Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="ed530-120">These factors help you choose the kind of app to create and which API or APIs to use.</span></span> <span data-ttu-id="ed530-121">Weitere Informationen, die Ihnen bei der Entscheidungsfindung helfen können, finden Sie unter [Wählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md) und [SharePoint-Add-Ins im Vergleich zu SharePoint-Lösungen](sharepoint-add-ins-compared-with-sharepoint-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ed530-121">See  [Choose the right API set in SharePoint](choose-the-right-api-set-in-sharepoint.md) and [SharePoint Add-ins compared with SharePoint solutions](sharepoint-add-ins-compared-with-sharepoint-solutions.md) for information that can help you decide.</span></span>
  
    
    

### <a name="setting-up-your-development-environment"></a><span data-ttu-id="ed530-122">Einrichten der Entwicklungsumgebung</span><span class="sxs-lookup"><span data-stu-id="ed530-122">Setting up your development environment</span></span>
<span data-ttu-id="ed530-123"><a name="DevEnvironment"> </a></span><span class="sxs-lookup"><span data-stu-id="ed530-123"><a name="DevEnvironment"> </a></span></span>

<span data-ttu-id="ed530-124">Voraussetzungen für die Entwicklung von Features für soziale Medien:</span><span class="sxs-lookup"><span data-stu-id="ed530-124">To get started developing with social features, you'll need:</span></span>
  
    
    

- <span data-ttu-id="ed530-125">SharePoint oder SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="ed530-125">SharePoint or SharePoint Online</span></span>
    
- <span data-ttu-id="ed530-126">Visual Studio 2012 oder Visual Studio 2013 mit Office Developer Tools für Visual Studio 2013 oder höher</span><span class="sxs-lookup"><span data-stu-id="ed530-126">Visual Studio 2012 or Visual Studio 2013, with Office Developer Tools for Visual Studio 2013 - or newer</span></span>
  

  
<span data-ttu-id="ed530-127">Weitere Anleitungen finden Sie unter  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md) und [Features für soziale Netzwerke in SharePoint konfigurieren](http://technet.microsoft.com/en-us/library/fp161267%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed530-127">For more guidance, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md) and [Configure social computing features in SharePoint](http://technet.microsoft.com/en-us/library/fp161267%28v=office.15%29.aspx).</span></span>
  
    
    

### <a name="development-scenarios-for-social-features-in-sharepoint"></a><span data-ttu-id="ed530-128">Entwicklungsszenarien für Features für soziale Netzwerke in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-128">Development scenarios for social features in SharePoint</span></span>
<span data-ttu-id="ed530-129"><a name="DevScenarios"> </a></span><span class="sxs-lookup"><span data-stu-id="ed530-129"><a name="DevScenarios"> </a></span></span>

<span data-ttu-id="ed530-p104">Allgemeine Entwicklungsszenarien für Features für soziale Netzwerke zählen arbeiten mit sozialen Feeds, folgen von Personen und Inhalte (Dokumente, Websites und Tags) und Arbeiten mit Benutzereigenschaften. Tabelle 1 enthält Links zu Artikeln, in denen die primären APIs beschrieben, mit denen Sie Zugriff auf Funktionen für jedes Szenario und allgemeine Programmieraufgaben.</span><span class="sxs-lookup"><span data-stu-id="ed530-p104">High-level development scenarios for social features include working with social feeds, following people and content (documents, sites, and tags), and working with user properties. Table 1 contains links to articles that describe the primary APIs that you use to access functionality for each scenario and common programming tasks.</span></span>
  
    
    
<span data-ttu-id="ed530-132">Die folgenden Artikel beschreiben die primäre APIs und Programmieraufgaben für die Entwicklungsszenario:</span><span class="sxs-lookup"><span data-stu-id="ed530-132">The following articles describe the primary APIs and programming tasks for the particular development scenario:</span></span>
  
    
    

-  [<span data-ttu-id="ed530-133">Arbeiten mit sozialen Feeds in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-133">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ed530-134">Folgen von Personen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-134">Follow people in SharePoint</span></span>](follow-people-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ed530-135">Folgen von Inhalten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-135">Follow content in SharePoint</span></span>](follow-content-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ed530-136">Arbeiten mit Benutzerprofilen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-136">Work with user profiles in SharePoint</span></span>](work-with-user-profiles-in-sharepoint.md)
    
  

### <a name="how-tos-for-programming-with-social-features-in-sharepoint"></a><span data-ttu-id="ed530-137">Vorgehensweisen für die Programmierung mit Features für soziale Netzwerke in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-137">How-tos for programming with social features in SharePoint</span></span>
<span data-ttu-id="ed530-138"><a name="bk_GetStarted"> </a></span><span class="sxs-lookup"><span data-stu-id="ed530-138"><a name="bk_GetStarted"> </a></span></span>

<span data-ttu-id="ed530-p105">Nachdem Sie Ihre Entwicklungsumgebung einrichten, und wählen Sie das Szenario, Sie können ersten Schritte beim Programmieren mit Features für soziale Netzwerke. Tabelle 1 enthält Links zu Artikeln, die zeigen, wie Sie einfache Programmieraufgaben mit Features für soziale Netzwerke.</span><span class="sxs-lookup"><span data-stu-id="ed530-p105">After you set up your development environment and choose your scenario, you can get started programming with social features. Table 1 contains links to articles that show how to do basic programming tasks with social features.</span></span>
  
    
    

<span data-ttu-id="ed530-141">**In Tabelle 1. Artikel mit Anleitungen für die Entwicklung mit thematischen features**</span><span class="sxs-lookup"><span data-stu-id="ed530-141">**Table 1. How-to articles for developing with social features**</span></span>


|<span data-ttu-id="ed530-142">**Funktionsbereich**</span><span class="sxs-lookup"><span data-stu-id="ed530-142">**Feature area**</span></span>|<span data-ttu-id="ed530-143">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="ed530-143">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="ed530-144">Vorgehensweise: Lesen und schreiben für soziale Netzwerke-Feed mithilfe des clientobjektmodells .NET SharePoint lernen</span><span class="sxs-lookup"><span data-stu-id="ed530-144">How to: Learn to read and write to the social feed by using the .NET client object model in SharePoint</span></span>](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-net-client-object.md)|<span data-ttu-id="ed530-145">Ausführliche Schritte zum Erstellen einer Anwendung, die Lese- und Schreibvorgänge auf den Feed für soziale Netzwerke mithilfe des Clientobjektmodells .NET durchgehen.</span><span class="sxs-lookup"><span data-stu-id="ed530-145">Walk through detailed steps for creating an application that reads and writes to the social feed by using the .NET client object model.</span></span>|
| [<span data-ttu-id="ed530-146">Vorgehensweise: Lesen und Schreiben der sozialen Feed mithilfe des REST-Diensts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-146">How to: Learn to read and write to the social feed by using the REST service in SharePoint</span></span>](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)|<span data-ttu-id="ed530-147">Ausführliche Schritte zum Erstellen einer Anwendung, die Lese- und Schreibvorgänge auf den Feed für soziale Netzwerke mithilfe des REST-Diensts durchgehen.</span><span class="sxs-lookup"><span data-stu-id="ed530-147">Walk through detailed steps for creating an application that reads and writes to the social feed by using the REST service.</span></span>|
| [<span data-ttu-id="ed530-148">Vorgehensweise: Erstellen und Löschen von Beiträge und Abrufen des für soziale Netzwerke-Feed mithilfe des clientobjektmodells .NET SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-148">How to: Create and delete posts and retrieve the social feed by using the .NET client object model in SharePoint</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md)|<span data-ttu-id="ed530-149">Informationen zum Erstellen und Löschen von und Beiträge Microblog und Abrufen von sozialen Feeds mithilfe des Clientobjektmodells .NET.</span><span class="sxs-lookup"><span data-stu-id="ed530-149">Learn how to create and delete and microblog posts and retrieve social feeds by using the .NET client object model.</span></span>|
| [<span data-ttu-id="ed530-150">Vorgehensweise: Erstellen und Löschen von Beiträgen und sozialen Feed abrufen, indem Sie mit der JavaScript-Objektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-150">How to: Create and delete posts and retrieve the social feed by using the JavaScript object model in SharePoint</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md)|<span data-ttu-id="ed530-151">In diesem Artikel erfahren Sie, wie Sie mithilfe des JavaScript-Objektmodells Beiträge erstellen, löschen und mikrobloggen sowie soziale Feeds abrufen können.</span><span class="sxs-lookup"><span data-stu-id="ed530-151">Learn how to create and delete and microblog posts and retrieve social feeds by using the JavaScript object model.</span></span>|
| [<span data-ttu-id="ed530-152">Vorgehensweise: Einschließen von Erwähnungen, Tags und Links zu Websites und Dokumenten in Beiträgen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-152">How to: Include mentions, tags, and links to sites and documents in posts in SharePoint</span></span>](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md)|<span data-ttu-id="ed530-153">In diesem Artikel erfahren Sie, wie Sie Mikroblogbeiträgen  **SocialDataItem**-Objekte hinzufügen, die als Erwähnungen, Tags und Links in sozialen Feeds gerendert werden.</span><span class="sxs-lookup"><span data-stu-id="ed530-153">Learn how to add **SocialDataItem** objects to microblog posts, which render as mentions, tags, and links in social feeds.</span></span>|
| [<span data-ttu-id="ed530-154">Vorgehensweise: Einbetten von Bildern, Videos und Dokumenten in Beiträgen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-154">How to: Embed images, videos, and documents in posts in SharePoint</span></span>](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md)|<span data-ttu-id="ed530-155">In diesem Artikel erfahren Sie, wie Sie Mikroblogbeiträgen **SocialAttachment**-Objekte hinzufügen, die als eingebettete Bilder, Videos und Dokumente in sozialen Feeds gerendert werden.</span><span class="sxs-lookup"><span data-stu-id="ed530-155">Learn how to add **SocialAttachment** objects to microblog posts, which render as embedded pictures, videos, and documents in social feeds.</span></span>|
| [<span data-ttu-id="ed530-156">Vorgehensweise: führen Sie die Personen mithilfe des clientobjektmodells .NET SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-156">How to: Follow people by using the .NET client object model in SharePoint</span></span>](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md)|<span data-ttu-id="ed530-157">Erfahren Sie, wie in der folgenden personenfeatures mithilfe des Clientobjektmodells .NET entwickelt.</span><span class="sxs-lookup"><span data-stu-id="ed530-157">Learn how to work with Following People features by using the .NET client object model.</span></span>|
| [<span data-ttu-id="ed530-158">Vorgehensweise: folgen Sie Menschen mit der JavaScript-Objektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-158">How to: Follow people by using the JavaScript object model in SharePoint</span></span>](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md)|<span data-ttu-id="ed530-159">Erfahren Sie, wie in der folgenden personenfeatures mithilfe des Objektmodells JavaScript entwickelt.</span><span class="sxs-lookup"><span data-stu-id="ed530-159">Learn how to work with Following People features by using the JavaScript object model.</span></span>|
| [<span data-ttu-id="ed530-160">Vorgehensweise: Führen Sie Dokumente und Websites mit .NET Client-Objektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-160">How to: Follow documents and sites by using the .NET client object model in SharePoint</span></span>](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)|<span data-ttu-id="ed530-161">Erfahren Sie, wie in der folgenden Inhaltsfunktionen mithilfe des Clientobjektmodells .NET entwickelt.</span><span class="sxs-lookup"><span data-stu-id="ed530-161">Learn how to work with Following Content features by using the .NET client object model.</span></span>|
| [<span data-ttu-id="ed530-162">Vorgehensweise: führen Sie Dokumente, Websites und Tags mithilfe des REST-Diensts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-162">How to: Follow documents, sites, and tags by using the REST service in SharePoint</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)|<span data-ttu-id="ed530-163">Erfahren Sie, wie in der folgenden Inhaltsfunktionen entwickelt, mithilfe des REST-Diensts.</span><span class="sxs-lookup"><span data-stu-id="ed530-163">Learn how to work with Following Content features by using the REST service.</span></span>|
| [<span data-ttu-id="ed530-164">Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des .NET-Clientobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-164">How to: Retrieve user profile properties by using the .NET client object model in SharePoint</span></span>](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md)|<span data-ttu-id="ed530-165">Informationen Sie zum Abrufen von Benutzerprofileigenschaften mithilfe des Clientobjektmodells .NET.</span><span class="sxs-lookup"><span data-stu-id="ed530-165">Learn how to retrieve user profile properties by using the .NET client object model.</span></span>|
| [<span data-ttu-id="ed530-166">Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des JavaScript-Objektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-166">How to: Retrieve user profile properties by using the JavaScript object model in SharePoint</span></span>](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md)|<span data-ttu-id="ed530-167">Informationen Sie zum Abrufen von Benutzerprofileigenschaften mithilfe der JavaScript-Objektmodells.</span><span class="sxs-lookup"><span data-stu-id="ed530-167">Learn how to retrieve user profile properties by using the JavaScript object model.</span></span>|
| [<span data-ttu-id="ed530-168">Vorgehensweise: Arbeiten mit Benutzerprofilen und Organisationsprofilen mithilfe des Serverobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-168">How to: Work with user profiles and organization profiles by using the server object model in SharePoint</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)|<span data-ttu-id="ed530-169">Informationen Sie zum Erstellen, abrufen und Verwalten von Benutzerprofilen und Eigenschaften mithilfe des Serverobjektmodells.</span><span class="sxs-lookup"><span data-stu-id="ed530-169">Learn how to create, retrieve, and manage user profiles and properties by using the server object model.</span></span>|
   

### <a name="apis-for-programming-with-sharepoint-social-features"></a><span data-ttu-id="ed530-170">APIs für die Programmierung mit SharePoint Features für soziale Netzwerke</span><span class="sxs-lookup"><span data-stu-id="ed530-170">APIs for programming with SharePoint social features</span></span>
<span data-ttu-id="ed530-171"><a name="SocialApis"> </a></span><span class="sxs-lookup"><span data-stu-id="ed530-171"><a name="SocialApis"> </a></span></span>

<span data-ttu-id="ed530-p106">Zwar apps und -Lösungen SharePoint unterschiedlich zugreifen, nachdem Sie SharePoint zugreifen verwenden die APIs für soziale Netzwerke im Wesentlichen die gleiche Weise. In Tabelle 2 sind die APIs für die Programmierung mit der Feed profiles Folgendes und Benutzer Features in SharePoint und die Pfade auf die Quelldateien auf dem Server.</span><span class="sxs-lookup"><span data-stu-id="ed530-p106">Although apps and solutions access SharePoint differently, after you do access SharePoint you use the social APIs in basically the same way. Table 2 shows the APIs for programming with feed, following, and user profiles features in SharePoint and the paths to the source files on the server.</span></span>
  
    
    

<span data-ttu-id="ed530-174">**In Tabelle 2. APIs für die Programmierung mit Features für soziale Netzwerke**</span><span class="sxs-lookup"><span data-stu-id="ed530-174">**Table 2. APIs for programming with social features**</span></span>


|<span data-ttu-id="ed530-175">**API-Name**</span><span class="sxs-lookup"><span data-stu-id="ed530-175">**API name**</span></span>|<span data-ttu-id="ed530-176">**Quell- und Pfad**</span><span class="sxs-lookup"><span data-stu-id="ed530-176">**Source and path**</span></span>|
|:-----|:-----|
| <span data-ttu-id="ed530-177">[.NET-Clientobjektmodell](http://msdn.microsoft.com/library/9cc3f70c-78ac-4d2d-b46e-77522ee5d937%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="ed530-177">[.NET client object model](http://msdn.microsoft.com/library/9cc3f70c-78ac-4d2d-b46e-77522ee5d937%28Office.15%29.aspx)</span></span>|<span data-ttu-id="ed530-178">Microsoft.SharePoint.Client.UserProfiles.dll</span><span class="sxs-lookup"><span data-stu-id="ed530-178">Microsoft.SharePoint.Client.UserProfiles.dll</span></span><br/><span data-ttu-id="ed530-179">im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="ed530-179">in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span></span>|
|<span data-ttu-id="ed530-180">Silverlight-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="ed530-180">Silverlight client object model</span></span>|<span data-ttu-id="ed530-181">Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll</span><span class="sxs-lookup"><span data-stu-id="ed530-181">Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll</span></span><br/><span data-ttu-id="ed530-182">im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin</span><span class="sxs-lookup"><span data-stu-id="ed530-182">in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin</span></span>|
|<span data-ttu-id="ed530-183">Mobiles Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="ed530-183">Mobile client object model</span></span>|<span data-ttu-id="ed530-184">Microsoft.SharePoint.Client.UserProfiles.Phone.dll</span><span class="sxs-lookup"><span data-stu-id="ed530-184">Microsoft.SharePoint.Client.UserProfiles.Phone.dll</span></span><br/><span data-ttu-id="ed530-185">im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin</span><span class="sxs-lookup"><span data-stu-id="ed530-185">in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin</span></span>|
| <span data-ttu-id="ed530-186">[JavaScript-Objektmodell](http://msdn.microsoft.com/library/95cb5427-8514-4e9a-8eee-7ed4b82ec01b%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="ed530-186">[JavaScript object model](http://msdn.microsoft.com/library/95cb5427-8514-4e9a-8eee-7ed4b82ec01b%28Office.15%29.aspx)</span></span>|<span data-ttu-id="ed530-187">SP.UserProfiles.js</span><span class="sxs-lookup"><span data-stu-id="ed530-187">SP.UserProfiles.js</span></span><br/><span data-ttu-id="ed530-188">im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS</span><span class="sxs-lookup"><span data-stu-id="ed530-188">in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS</span></span>|
|<span data-ttu-id="ed530-189">REST (Representational State Transfer)-Dienst</span><span class="sxs-lookup"><span data-stu-id="ed530-189">Representational State Transfer (REST) service</span></span>| [`http://<site url>/_api/social.feed`](social-feed-rest-api-reference-for-sharepoint.md)<br/>[`http://<site url>/_api/social.following`](following-people-and-content-rest-api-reference-for-sharepoint.md)<br/>[`http://<site url>/_api/SP.UserProfiles.PeopleManager`](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx.md#bk_PeopleManager)|
| <span data-ttu-id="ed530-190">[Serverobjektmodell](http://msdn.microsoft.com/library/87c5118c-ac0e-4bd9-a75f-7452a9eb0e41%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="ed530-190">[Server object model](http://msdn.microsoft.com/library/87c5118c-ac0e-4bd9-a75f-7452a9eb0e41%28Office.15%29.aspx)</span></span>|<span data-ttu-id="ed530-191">Microsoft.Office.Server.UserProfiles.dll</span><span class="sxs-lookup"><span data-stu-id="ed530-191">Microsoft.Office.Server.UserProfiles.dll</span></span><br/><span data-ttu-id="ed530-192">im Ordner %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="ed530-192">in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span></span>|
   
> [!NOTE]
> <span data-ttu-id="ed530-193">Nicht alle serverseitigen Funktionen im Assembly Microsoft.Office.Server.UserProfiles sind in den Client-APIs verfügbar.</span><span class="sxs-lookup"><span data-stu-id="ed530-193">Note: Not all server-side functionality in the Microsoft.Office.Server.UserProfiles assembly is available from client APIs.</span></span> <span data-ttu-id="ed530-194">Im Namespace [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) und im Namespace [Microsoft.SharePoint.Client.UserProfiles](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx) erfahren Sie, welche APIs verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="ed530-194">To see which APIs are available, see the  [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) namespace and the [Microsoft.SharePoint.Client.UserProfiles](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx) namespace.</span></span>
  
    
    


## <a name="app-permission-requests-for-accessing-social-features-in-sharepoint-add-ins"></a><span data-ttu-id="ed530-195">App-Berechtigungsanforderungen für den Zugriff auf Features für soziale Netzwerke in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="ed530-195">App permission requests for accessing social features in SharePoint Add-ins</span></span>
<span data-ttu-id="ed530-196"><a name="bkmk_AppPerms"> </a></span><span class="sxs-lookup"><span data-stu-id="ed530-196"><a name="bkmk_AppPerms"> </a></span></span>

<span data-ttu-id="ed530-197">Eine SharePoint-Add-In muss die für den Zugriff auf SharePoint-Ressourcen benötigte Berechtigung bei dem Benutzer anfordern, der die Installation vornimmt.</span><span class="sxs-lookup"><span data-stu-id="ed530-197">An SharePoint Add-in must request the permissions that it needs to access SharePoint resources from the user who installs it.</span></span> <span data-ttu-id="ed530-198">Beispielsweise muss eine App, die im Feed Beiträge veröffentlicht, (mindestens) die **Schreibberechtigung** beim Feed anfragen.</span><span class="sxs-lookup"><span data-stu-id="ed530-198">For example, an app that posts to the feed should request **Write** permission (at minimum) to the feed.</span></span> <span data-ttu-id="ed530-199">Geben Sie die Berechtigungen, die Ihre App benötigt, in der AppManifest.xml-Datei in Visual Studio an.</span><span class="sxs-lookup"><span data-stu-id="ed530-199">You specify the permissions that your app need in the AppManifest.xml file in Visual Studio.</span></span>
  
    
    
<span data-ttu-id="ed530-p109">App-Berechtigungsanforderungen sind auf der SharePoint-Bereitstellung im Querformat beschränkt. Tabelle 3 zeigt die Bereichsnamen (mit den entsprechenden Bereich URIs) und die verfügbaren Rechte für den Zugriff auf Features für soziale Netzwerke. Weitere Informationen finden Sie unter  [Add-In-Berechtigungen in SharePoint](http://msdn.microsoft.com/library/5f7a8440-3c09-4cf8-83ec-c236bfa2d6c4%28Office.15%29.aspx),  [Add-In-Autorisierungsrichtlinientypen in SharePoint](http://msdn.microsoft.com/library/124879c7-a746-4c10-96a7-da76ad5327f0%28Office.15%29.aspx)und  [Planen der app-Berechtigungsverwaltung in SharePoint](http://technet.microsoft.com/de-DE/library/jj219576%28office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed530-p109">App permission requests are scoped to the SharePoint deployment landscape. Table 3 shows the scope names (with corresponding scope URIs) and the available rights for accessing social features. For more information, see  [Add-in permissions in SharePoint](http://msdn.microsoft.com/library/5f7a8440-3c09-4cf8-83ec-c236bfa2d6c4%28Office.15%29.aspx),  [Add-in authorization policy types in SharePoint](http://msdn.microsoft.com/library/124879c7-a746-4c10-96a7-da76ad5327f0%28Office.15%29.aspx), and  [Plan app permissions management in SharePoint](http://technet.microsoft.com/de-DE/library/jj219576%28office.15%29.aspx).</span></span>
  
    
    

<span data-ttu-id="ed530-203">**Tabelle 3. App-Berechtigungsbereiche und verfügbare Rechte für Features für soziale Netzwerke in SharePoint**</span><span class="sxs-lookup"><span data-stu-id="ed530-203">**Table 3. App permission scopes and available rights for social features in SharePoint**</span></span>


|<span data-ttu-id="ed530-204">**Bereichsname**</span><span class="sxs-lookup"><span data-stu-id="ed530-204">**Scope name**</span></span>|<span data-ttu-id="ed530-205">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="ed530-205">**Description**</span></span>|<span data-ttu-id="ed530-206">**Verfügbare Rechte**</span><span class="sxs-lookup"><span data-stu-id="ed530-206">**Available rights**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="ed530-207">Benutzerprofile</span><span class="sxs-lookup"><span data-stu-id="ed530-207">User Profiles</span></span><br/>`http://sharepoint/social/tenant`|<span data-ttu-id="ed530-p110">Den berechtigungsanforderungsbereich verwendet, um alle Benutzerprofile zugreifen. Nur das Benutzerprofildienst-Bild kann geändert werden. alle anderen Benutzerprofileigenschaften sind für SharePoint-Add-Ins schreibgeschützt. Muss von einem mandantenadministrator installiert werden.</span><span class="sxs-lookup"><span data-stu-id="ed530-p110">The permission request scope used to access all user profiles. Only the profile picture can be changed; all other user profile properties are read-only for SharePoint Add-ins. Must be installed by a tenant administrator.</span></span>|<span data-ttu-id="ed530-210">Read, Write, Manage, FullControl</span><span class="sxs-lookup"><span data-stu-id="ed530-210">Read, Write, Manage, FullControl</span></span>|
|<span data-ttu-id="ed530-211">Core</span><span class="sxs-lookup"><span data-stu-id="ed530-211">Core</span></span><br/>`http://sharepoint/social/core`|<span data-ttu-id="ed530-p111">Der berechtigungsanforderungsbereich für den Zugriff des Benutzers auf beobachteten Inhalte und einem freigegebenen Metadaten, die von mikroblogging Features verwendet wird. In diesem Bereich gilt nur für persönliche Websites, die nach Inhalten zu unterstützen. Wenn die app auf eine andere Art von Website installiert wurde, verwenden Sie die mandantenbereich.</span><span class="sxs-lookup"><span data-stu-id="ed530-p111">The permission request scope used to access the user's followed content and shared metadata that is used by microblogging features. This scope applies only to personal sites that support following content. If the app installs on any other type of site, use the Tenant scope.</span></span>|<span data-ttu-id="ed530-215">Read, Write, Manage, FullControl</span><span class="sxs-lookup"><span data-stu-id="ed530-215">Read, Write, Manage, FullControl</span></span>|
|<span data-ttu-id="ed530-216">Newsfeed</span><span class="sxs-lookup"><span data-stu-id="ed530-216">News Feed</span></span><br/>`http://sharepoint/social/microfeed`|<span data-ttu-id="ed530-p112">Den berechtigungsanforderungsbereich des Benutzers Feed oder den Feed Team Zugriff auf verwendet. In diesem Bereich gilt für persönliche Websites, die mikroblogging unterstützen oder Teamwebsites, in dem das **Website-Feed**-Feature aktiviert ist. Wenn die app auf eine andere Art von Website installiert wurde, verwenden Sie die mandantenbereich.</span><span class="sxs-lookup"><span data-stu-id="ed530-p112">The permission request scope used to access the user's feed or the team feed. This scope applies to personal sites that support microblogging or to team sites where the **Site Feed** feature is activated. If the app installs on any other type of site, use the Tenant scope.</span></span>|<span data-ttu-id="ed530-220">Read, Write, Manage, FullControl</span><span class="sxs-lookup"><span data-stu-id="ed530-220">Read, Write, Manage, FullControl</span></span>|
| `http://sharepoint/social/trimming`|<span data-ttu-id="ed530-p113">In diesem berechtigungsanforderungsbereich verwendet, um festzustellen, ob Sicherheit verkürzt Inhalte in den Feed für soziale Netzwerke für apps anzuzeigen. Wenn diese Berechtigung hoher Vertrauenswürdigkeit nicht gewährt wurde, wird bestimmter Inhalte (wie Aktivitäten zu Dokumenten und Websites, denen die app zum berechtigt nicht) abgeschnitten aus der feed-Daten, die an die app zurückgegeben werden, auch wenn der Benutzer über ausreichende Berechtigungen verfügt. Diese Berechtigung muss die app-manifest-Datei manuell hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="ed530-p113">This permission request scope used to determine whether to display security-trimmed content in the social feed to apps. If this high-trust permission is not granted, some content (such as activities about documents and sites that the app doesn't have permissions to) is trimmed from the feed data that's returned to the app, even if the user has sufficient permissions. This permission must be manually added to the app's manifest file.</span></span>|<span data-ttu-id="ed530-224">Read, Write, Manage, FullControl</span><span class="sxs-lookup"><span data-stu-id="ed530-224">Read, Write, Manage, FullControl</span></span>|
   

### <a name="what-youll-need-to-consider-when-requesting-app-permissions"></a><span data-ttu-id="ed530-225">Was Sie benötigen, bei der app-Berechtigungen anfordern</span><span class="sxs-lookup"><span data-stu-id="ed530-225">What you'll need to consider when requesting app permissions</span></span>

<span data-ttu-id="ed530-226">Beachten Sie die folgenden Überlegungen beim app-Berechtigungen für Features für soziale Netzwerke angeben:</span><span class="sxs-lookup"><span data-stu-id="ed530-226">You should be aware of the following considerations when you specify app permissions for social features:</span></span>
  
    
    

- <span data-ttu-id="ed530-p114">Apps, die angeben, **FullControl** Rechte sind für Office Store apps nicht zulässig. Nur **Read**, **Write**und **Manage** Rechte sind für Office Store apps zulässig.</span><span class="sxs-lookup"><span data-stu-id="ed530-p114">Apps that specify **FullControl** rights are not allowed for Office Store apps. Only **Read**, **Write**, and **Manage** rights are allowed for Office Store apps.</span></span>
    
  
- <span data-ttu-id="ed530-p115">Sie können Berechtigungen für Feeds und die folgenden Features mithilfe von Core, Newsfeed und Mandant ( `http://sharepoint/content/tenant`) Bereiche angeben. Die mandantenbereich stellt die gesamte Instanz, in eine app, einschließlich der Kern und Newsfeed Bereiche installiert ist. Wenn Ihre app bereits die Rechte, die auf Standortebene Mandanten erforderlich sind angibt, klicken Sie dann Sie müssen nicht auf Standortebene Core oder Newsfeed Berechtigungen anzufordern.</span><span class="sxs-lookup"><span data-stu-id="ed530-p115">You can specify permissions for feed and following features by using the Core, News Feed, and Tenant ( `http://sharepoint/content/tenant`) scopes. The Tenant scope represents the whole tenancy where an app is installed, including the Core and News Feed scopes. So if your app already specifies the rights that it needs at the Tenant scope, then you don't need to request permissions at the Core or News Feed scope.</span></span>
    
  
- <span data-ttu-id="ed530-p116">Während der Entwicklung der mandantenbereich verwenden, wenn Sie erhalten eine "SocialListNotFound: die Liste für soziale Netzwerke in Ihrer persönlichen Website nicht vorhanden" oder "Datei nicht gefunden" angezeigt. Wenn Sie den Bereich Core oder Newsfeed in Ihrer app verwenden möchten, können Sie die Berechtigungen testen, indem Sie die app aus dem app-Katalog öffnen.</span><span class="sxs-lookup"><span data-stu-id="ed530-p116">During development, use the Tenant scope if you get a "SocialListNotFound : The Social list does not exist in your personal site" or "File Not Found" message. If you want to use the Core or News Feed scope in your app, you can test the permissions by opening the app from the app catalog.</span></span>
    
  
- <span data-ttu-id="ed530-p117">Der Bereich Core gilt für persönliche Websites, die nach Inhalten zu unterstützen. Der Bereich Newsfeed gilt für persönliche Websites, die mikroblogging unterstützen oder Teamwebsites, in dem das **Website-Feed**-Feature aktiviert ist. Wenn die app auf eine andere Art von Website installiert werden sollen, müssen Sie die mandantenbereich verwenden. Finden Sie unter  [Mandantschaften und Bereitstellungsbereiche von Add-Ins für SharePoint](http://msdn.microsoft.com/library/1ceb3142-a7a5-453e-920f-5f953a79401a%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed530-p117">The Core scope applies to personal sites that support following content. The News Feed scope applies to personal sites that support microblogging or to team sites where the **Site Feed** feature is activated. If the app will be installed on any other type of site, you must use the Tenant scope. See [Tenancies and deployment scopes for SharePoint Add-ins](http://msdn.microsoft.com/library/1ceb3142-a7a5-453e-920f-5f953a79401a%28Office.15%29.aspx).</span></span>
    
  
- <span data-ttu-id="ed530-238">Apps, die zur Anforderung von Rechten für den Bereich von Benutzerprofilen müssen von einem mandantenadministrator installiert sein, und sie können nicht in Office 365 Small Business Premium-Version von SharePoint Online installiert werden.</span><span class="sxs-lookup"><span data-stu-id="ed530-238">Apps that request rights for the User Profiles scope must be installed by a tenant administrator, and they cannot be installed in Office 365 Small Business Premium version of SharePoint Online.</span></span>
    
  
- <span data-ttu-id="ed530-239">Wenn Lizenzierung oder ein Feature Aktivierung für Features für soziale Netzwerke und mikroblogs nicht erfüllt sind, erhalten die Benutzer eine Meldung angezeigt, dass die app installiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="ed530-239">If licensing or feature activation requirements for social and microblogging features are not met, users get a message saying that they can't install the app.</span></span>
    
  
- <span data-ttu-id="ed530-p118">Apps, die außerhalb von SharePoint gestartet werden können Berechtigung auf spontane (mit Ausnahme von **Full Control**) anfordern. Weitere Informationen finden Sie unter  [OAuth-Ablauf mit Authentifizierungscode für SharePoint-Add-Ins](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed530-p118">Apps that are launched outside of SharePoint can request permission on-the-fly (except **Full Control**). For more information, see  [Authorization Code OAuth flow for SharePoint Add-ins](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="ed530-242">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="ed530-242">See also</span></span>
<span data-ttu-id="ed530-243"><a name="bk_AddResources"> </a></span><span class="sxs-lookup"><span data-stu-id="ed530-243"><a name="bk_AddResources"> </a></span></span>

 <span data-ttu-id="ed530-244">**Konzeptionelle Artikel**</span><span class="sxs-lookup"><span data-stu-id="ed530-244">**Conceptual articles**</span></span>
  
    
    

-  [<span data-ttu-id="ed530-245">Soziale Funktionen und Zusammenarbeit in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-245">Social and collaboration features in SharePoint</span></span>](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ed530-246">Neuigkeiten für Entwickler hinsichtlich der thematischen Features und der Zusammenarbeitsfeatures in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-246">What's new for developers in social and collaboration features in SharePoint</span></span>](what-s-new-for-developers-in-social-and-collaboration-features-in-sharepoint-201.md)
    
  
-  <span data-ttu-id="ed530-247">
  [Soziale Netzwerke und Zusammenarbeit in SharePoint Server](http://technet.microsoft.com/en-us/library/ee662531%28v=office.15%29)</span><span class="sxs-lookup"><span data-stu-id="ed530-247">[Plan for social computing and collaboration in SharePoint](http://technet.microsoft.com/en-us/library/ee662531%28v=office.15%29)</span></span>
    
  
-  <span data-ttu-id="ed530-248">
  [Features für soziale Netzwerke in SharePoint konfigurieren](http://technet.microsoft.com/en-us/library/fp161267%28v=office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="ed530-248">[Configure social computing features in SharePoint](http://technet.microsoft.com/en-us/library/fp161267%28v=office.15%29.aspx)</span></span>
    
  
-  <span data-ttu-id="ed530-249">
  [Terminologie und Konzepte sozialer Netzwerke in SharePoint](http://technet.microsoft.com/en-us/library/jj219804%28v=office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="ed530-249">[Social computing terminology and concepts in SharePoint](http://technet.microsoft.com/en-us/library/jj219804%28v=office.15%29.aspx)</span></span>
    
  
 <span data-ttu-id="ed530-250">**Referenzdokumentation**</span><span class="sxs-lookup"><span data-stu-id="ed530-250">**Reference documentation**</span></span>
  
    
    

-  <span data-ttu-id="ed530-251">[Clientklassenbibliothek für Funktionen und Daten für das soziale Netzwerk](http://msdn.microsoft.com/library/9cc3f70c-78ac-4d2d-b46e-77522ee5d937%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="ed530-251">[Social client class library](http://msdn.microsoft.com/library/9cc3f70c-78ac-4d2d-b46e-77522ee5d937%28Office.15%29.aspx)</span></span>
    
  
-  <span data-ttu-id="ed530-252">[SP. UserProfiles.js JavaScript-Referenz](http://msdn.microsoft.com/library/80cf5436-6aa2-6f11-a782-66a04f6e2fb0%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="ed530-252">[SP.UserProfiles.js JavaScript Reference](http://msdn.microsoft.com/library/80cf5436-6aa2-6f11-a782-66a04f6e2fb0%28Office.15%29.aspx)</span></span>
    
  
-  [<span data-ttu-id="ed530-253">REST-API-Referenz für sozialen Feed für SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-253">Social feed REST API reference for SharePoint</span></span>](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="ed530-254">REST-API-Referenz zum Folgen von Personen und Inhalten für SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed530-254">Following people and content REST API reference for SharePoint</span></span>](following-people-and-content-rest-api-reference-for-sharepoint.md)
    
  
-  <span data-ttu-id="ed530-255">[Benutzerprofile - REST-API-Referenz](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="ed530-255">[User profiles REST API reference](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)</span></span>
    
  
-  <span data-ttu-id="ed530-256">[Serverklassenbibliothek für Funktionen und Daten für das soziale Netzwerk für SharePoint](http://msdn.microsoft.com/library/87c5118c-ac0e-4bd9-a75f-7452a9eb0e41%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="ed530-256">[SharePoint Social server class library](http://msdn.microsoft.com/library/87c5118c-ac0e-4bd9-a75f-7452a9eb0e41%28Office.15%29.aspx)</span></span>
    
  
