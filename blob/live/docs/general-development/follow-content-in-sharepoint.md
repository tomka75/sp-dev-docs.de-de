---
title: Folgen von Inhalten in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 30e68cd6-6e55-4cf9-afd6-7139b0a97288
ms.openlocfilehash: 96a334f77bbf9e5b1512290ace4e01b61435548f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="follow-content-in-sharepoint"></a><span data-ttu-id="76ff7-102">Folgen von Inhalten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="76ff7-102">Follow content in SharePoint</span></span>
<span data-ttu-id="76ff7-103">Erfahren Sie mehr über allgemeine Programmierungsaufgaben für das Folgen von Inhalten (Dokumente, Websites und Tags) in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="76ff7-103">Learn about common programming tasks for following content (documents, sites, and tags) in SharePoint Server 2013.</span></span>
## <a name="apis-for-following-content-in-sharepoint"></a><span data-ttu-id="76ff7-104">APIs für das Folgen von Inhalten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="76ff7-104">APIs for following content in SharePoint Server 2013</span></span>
<span data-ttu-id="76ff7-105"><a name="bkmk_APIversions"> </a></span><span class="sxs-lookup"><span data-stu-id="76ff7-105"></span></span>

<span data-ttu-id="76ff7-p101">Wenn Benutzer Dokumenten, Websites oder Tags folgen, werden Statusupdates von Dokumenten, Unterhaltungen auf Websites und Benachrichtigungen zuTags in ihrem Newsfeed angezeigt. Die Features im Zusammenhang mit dem Folgen von Inhalten werden auf den Inhaltsseiten **Newsfeed** und **Folgen** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="76ff7-p101">When users follow documents, sites, or tags, status updates from documents, conversations on sites, and notifications of tag use show up in their newsfeed. The features related to following content can be seen on the **Newsfeed** and the **Following** content pages.</span></span>
  
    
    
<span data-ttu-id="76ff7-108">SharePoint stellt die folgenden APIs bereit, mit denen Sie Inhalten programmgesteuert folgen können:</span><span class="sxs-lookup"><span data-stu-id="76ff7-108">SharePoint Server 2013 provides the following APIs that you can use to programmatically follow content:</span></span>
  
    
    

- <span data-ttu-id="76ff7-109">Clientobjektmodelle für verwalteten Code</span><span class="sxs-lookup"><span data-stu-id="76ff7-109">Client object models for managed code</span></span>
    
  - <span data-ttu-id="76ff7-110">.NET-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="76ff7-110">.NET client object model</span></span>
    
  
  - <span data-ttu-id="76ff7-111">Silverlight-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="76ff7-111">Silverlight client object model</span></span>
    
  
  - <span data-ttu-id="76ff7-112">Mobiles Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="76ff7-112">Mobile client object model</span></span>
    
  
- <span data-ttu-id="76ff7-113">JavaScript-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="76ff7-113">JavaScript object model</span></span>
    
  
- <span data-ttu-id="76ff7-114">REST (Representational State Transfer)-Dienst</span><span class="sxs-lookup"><span data-stu-id="76ff7-114">Representational State Transfer (REST) service</span></span>
    
  
- <span data-ttu-id="76ff7-115">Serverobjektmodell</span><span class="sxs-lookup"><span data-stu-id="76ff7-115">Server object model</span></span>
    
  
<span data-ttu-id="76ff7-p102">In der SharePoint-Entwicklung wird empfohlen, so oft wie möglich Client-APIs zu verwenden. Client-APIs umfassen Clientobjektmodelle, das JavaScript-Objektmodell und einen REST-Dienst. Weitere Informationen zu APIs in SharePoint und zu ihrer Verwendung finden Sie unter  [Auswählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="76ff7-p102">As a best practice in SharePoint development, use client APIs when you can. Client APIs include the client object models, a JavaScript object model, and a REST service. For more information about the APIs in SharePoint and when to use them, see  [Choose the right API set in SharePoint](choose-the-right-api-set-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="76ff7-119">Jede API enthält ein Manager-Objekt, das Sie verwenden, um wichtige Aufgaben für das Folgen von Inhalten auszuführen.</span><span class="sxs-lookup"><span data-stu-id="76ff7-119">Each API includes a manager object that you use to perform core tasks for following content.</span></span>
  
    
    

> <span data-ttu-id="76ff7-120">**Hinweis:** Die gleichen APIs werden verwendet, um Personen zu folgen.</span><span class="sxs-lookup"><span data-stu-id="76ff7-120">**Note** The same APIs are used to follow people. See  Follow people in SharePoint for an overview of Following People tasks.</span></span> <span data-ttu-id="76ff7-121">Einen Überblick über Aufgaben beim Folgen von Personen finden Sie unter [Folgen von Personen in SharePoint](follow-people-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="76ff7-121">Note The same APIs are used to follow people. See  [Follow people in SharePoint](follow-people-in-sharepoint.md) for an overview of Following People tasks.</span></span>
  
    
    

<span data-ttu-id="76ff7-122">Tabelle 1 zeigt den Manager und andere Schlüsselobjekte (oder REST-Ressourcen) in den APIs und die Klassenbibliothek (oder Zugriffspunkt), in dem Sie diese finden können.</span><span class="sxs-lookup"><span data-stu-id="76ff7-122">Table 1 shows the manager and other key objects (or REST resources) in the APIs and the class library (or access point) where you can find them.</span></span>
  
    
    

> <span data-ttu-id="76ff7-123">**Hinweis:** Die Objektmodelle für Silverlight und den mobilen Client sind nicht in Tabelle 1 oder Tabelle 2 enthalten, da sie dieselben Kernfunktionen wie das .NET-Clientobjektmodell bieten und die gleichen Signaturen verwenden.</span><span class="sxs-lookup"><span data-stu-id="76ff7-123">**Note** The Silverlight and mobile client object models are not explicitly included in Table 1 or Table 2 because they provide the same core functionality as the .NET client object model and use the same signatures. The Silverlight client object model is defined in Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll, and the mobile client object model is defined in Microsoft.SharePoint.Client.UserProfiles.Phone.dll.</span></span> <span data-ttu-id="76ff7-124">Das Silverlight-Clientobjektmodell ist in Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll definiert und das Objektmodell für den mobilen Client in Microsoft.SharePoint.Client.UserProfiles.Phone.dll.</span><span class="sxs-lookup"><span data-stu-id="76ff7-124">Note The Silverlight and mobile client object models are not explicitly mentioned in Table 1 or Table 2 because they provide the same core functionality as the .NET client object model and use the same signatures. The Silverlight client object model is defined in Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll, and the mobile client object model is defined in Microsoft.SharePoint.Client.UserProfiles.Phone.dll.</span></span> 
  
    
    


<span data-ttu-id="76ff7-125">**Tabelle 1: Für das programmgesteuerte Folgen von Inhalten verwendete SharePoint-APIs**</span><span class="sxs-lookup"><span data-stu-id="76ff7-125">**Table 1. SharePoint APIs used for following content programmatically**</span></span>

|<span data-ttu-id="76ff7-126">**API**</span><span class="sxs-lookup"><span data-stu-id="76ff7-126">**API**</span></span>|<span data-ttu-id="76ff7-127">**Schlüsselobjekte**</span><span class="sxs-lookup"><span data-stu-id="76ff7-127">**Key objects**</span></span>|
|:-----|:-----|
|<span data-ttu-id="76ff7-128">.NET-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="76ff7-128">.NET client object model</span></span>  <br/> <span data-ttu-id="76ff7-129">Weitere Informationen:  [Vorgehensweise: Führen Sie Dokumente und Websites mit .NET Client-Objektmodell in SharePoint](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)</span><span class="sxs-lookup"><span data-stu-id="76ff7-129">See:  [How to: Follow documents and sites by using the .NET client object model in SharePoint](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)</span></span>|<span data-ttu-id="76ff7-130">Manager-Objekt:            [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-130">Manager object:            [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)</span></span> <br/> <span data-ttu-id="76ff7-131">Primärer Namespace:            [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-131">Primary namespace:            [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx)</span></span> <br/> <span data-ttu-id="76ff7-132">Sonstige Schlüsselobjekte:            [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) , [SocialActorInfo](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorInfo.aspx) , [SocialActorType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorType.aspx) , [SocialActorTypes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorTypes.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-132">Other key objects:            [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) , [SocialActorInfo](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorInfo.aspx) , [SocialActorType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorType.aspx) , [SocialActorTypes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorTypes.aspx)</span></span> <br/> <span data-ttu-id="76ff7-133">Klassenbibliothek:           Microsoft.SharePoint.Client.UserProfiles.dll</span><span class="sxs-lookup"><span data-stu-id="76ff7-133">Class library:           Microsoft.SharePoint.Client.UserProfiles.dll</span></span>  |
|<span data-ttu-id="76ff7-134">JavaScript-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="76ff7-134">JavaScript object model</span></span>|<span data-ttu-id="76ff7-135">Manager-Objekt:            [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-135">Manager object:            [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="76ff7-136">Primärer Namespace:            [SP.Social](http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-136">Primary namespace:            [SP.Social](http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="76ff7-137">Andere wichtige Objekte:            [SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx),  [SocialActorInfo](http://msdn.microsoft.com/library/d940db32-1561-c868-bb66-0612e2031f17%28Office.15%29.aspx),  [SocialActorType](http://msdn.microsoft.com/library/fbde74da-f292-dc87-0b7e-81bc5b7a880c%28Office.15%29.aspx),  [SocialActorTypes](http://msdn.microsoft.com/library/a460c3e6-ed88-117d-6755-4c5803a154a0%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-137">Other key objects:            [SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx),  [SocialActorInfo](http://msdn.microsoft.com/library/d940db32-1561-c868-bb66-0612e2031f17%28Office.15%29.aspx),  [SocialActorType](http://msdn.microsoft.com/library/fbde74da-f292-dc87-0b7e-81bc5b7a880c%28Office.15%29.aspx),  [SocialActorTypes](http://msdn.microsoft.com/library/a460c3e6-ed88-117d-6755-4c5803a154a0%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="76ff7-138">Klassenbibliothek:           SP.UserProfiles.js</span><span class="sxs-lookup"><span data-stu-id="76ff7-138">Class library:           SP.UserProfiles.js</span></span>  |
|<span data-ttu-id="76ff7-139">REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="76ff7-139">REST service</span></span>  <br/> <span data-ttu-id="76ff7-140">Weitere Informationen:  [Vorgehensweise: führen Sie Dokumente, Websites und Tags mithilfe des REST-Diensts in SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)</span><span class="sxs-lookup"><span data-stu-id="76ff7-140">See  [How to: Follow documents, sites, and tags by using the REST service in SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)</span></span>|<span data-ttu-id="76ff7-141">Manager-Ressource:            [social.following](following-people-and-content-rest-api-reference-for-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="76ff7-141">Manager resource:            [social.following](following-people-and-content-rest-api-reference-for-sharepoint.md)</span></span> <br/> <span data-ttu-id="76ff7-142">Primärer Namespace (OData):           **sp.social.SocialRestFollowingManager**</span><span class="sxs-lookup"><span data-stu-id="76ff7-142">Primary namespace (OData):           **sp.social.SocialRestFollowingManager**</span></span> <br/> <span data-ttu-id="76ff7-143">Andere wichtige Ressourcen:           **SocialActor**, **SocialActorInfo**, **SocialActorType**, **SocialActorTypes**</span><span class="sxs-lookup"><span data-stu-id="76ff7-143">Other key resources:           **SocialActor**, **SocialActorInfo**, **SocialActorType**, **SocialActorTypes**</span></span> <br/> <span data-ttu-id="76ff7-144">Zugriffspunkt:            `<siteUri>/_api/social.following`</span><span class="sxs-lookup"><span data-stu-id="76ff7-144">Access point:            `<siteUri>/_api/social.following`</span></span> |
|<span data-ttu-id="76ff7-145">Serverobjektmodell</span><span class="sxs-lookup"><span data-stu-id="76ff7-145">Server object model</span></span>|<span data-ttu-id="76ff7-146">Manager-Objekt:            [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-146">Manager object:            [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx)</span></span> <br/> <span data-ttu-id="76ff7-147">Primärer Namespace:            [Microsoft.Office.Server.Social](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-147">Primary namespace:            [Microsoft.Office.Server.Social](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.aspx)</span></span> <br/> <span data-ttu-id="76ff7-148">Sonstige Schlüsselobjekte:            [SPSocialActor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActor.aspx) , [SPSocialActorInfo](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorInfo.aspx) , [SPSocialActorType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorType.aspx) , [SPSocialActorTypes](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorTypes.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-148">Other key objects:            [SPSocialActor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActor.aspx) , [SPSocialActorInfo](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorInfo.aspx) , [SPSocialActorType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorType.aspx) , [SPSocialActorTypes](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorTypes.aspx)</span></span> <br/> <span data-ttu-id="76ff7-149">Klassenbibliothek:           Microsoft.Office.Server.UserProfiles.dll</span><span class="sxs-lookup"><span data-stu-id="76ff7-149">Class library:           Microsoft.Office.Server.UserProfiles.dll</span></span>  |
   

## <a name="common-programming-tasks-for-following-content-in-sharepoint"></a><span data-ttu-id="76ff7-150">Allgemeine Programmierungsaufgaben für das Folgen von Inhalten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="76ff7-150">Common programming tasks for following content in SharePoint Server 2013</span></span>
<span data-ttu-id="76ff7-151"><a name="bkmk_CommonTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="76ff7-151"></span></span>

<span data-ttu-id="76ff7-p105">Tabelle 2 zeigt allgemeine Programmierungsaufgaben für das Folgen von Inhalten sowie die Elemente, die Sie zur Ausführung verwenden. Die Elemente stammen aus dem .NET-Clientobjektmodell (CSOM), dem JavaScript-Objektmodell (JSOM), dem REST-Dienst und dem Serverobjektmodell (SSOM).</span><span class="sxs-lookup"><span data-stu-id="76ff7-p105">Table 2 shows common programming tasks for following content and the members that you use to perform them. Members are from the .NET client object model (CSOM), JavaScript object model (JSOM), REST service, and server object model (SSOM).</span></span>
  
    
    

> <span data-ttu-id="76ff7-154">**Hinweis:** Die gleichen APIs werden verwendet, um Personen zu folgen.</span><span class="sxs-lookup"><span data-stu-id="76ff7-154">**Note** The same APIs are used to follow people. See  Follow people in SharePoint for an overview of Following People tasks.</span></span> <span data-ttu-id="76ff7-155">Einen Überblick über Aufgaben beim Folgen von Personen finden Sie unter [Folgen von Personen in SharePoint](follow-people-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="76ff7-155">Note The same APIs are used to follow people. See  [Follow people in SharePoint](follow-people-in-sharepoint.md) for an overview of Following People tasks.</span></span>
  
    
    


<span data-ttu-id="76ff7-156">**Tabelle 2: API für allgemeine Aufgaben für das Folgen von Inhalten in SharePoint Server**</span><span class="sxs-lookup"><span data-stu-id="76ff7-156">**Table 2. API for common tasks for following content in SharePoint Server 2013**</span></span>


|<span data-ttu-id="76ff7-157">**Aufgabe**</span><span class="sxs-lookup"><span data-stu-id="76ff7-157">**Task**</span></span>|<span data-ttu-id="76ff7-158">**Elemente**</span><span class="sxs-lookup"><span data-stu-id="76ff7-158">**Members**</span></span>|
|:-----|:-----|
|<span data-ttu-id="76ff7-159">Erstellen einer Instanz eines Manager-Objekts im Kontext des aktuellen Benutzers</span><span class="sxs-lookup"><span data-stu-id="76ff7-159">Create an instance of a manager object in the context of the current user</span></span>|<span data-ttu-id="76ff7-160">CSOM:  [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-160">CSOM:  [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)</span></span> <br/> <span data-ttu-id="76ff7-161">JSOM:  [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-161">JSOM:  [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="76ff7-162">REST:  `<siteUri>/_api/social.following`</span><span class="sxs-lookup"><span data-stu-id="76ff7-162">REST:  `<siteUri>/_api/social.following`</span></span> <br/> <span data-ttu-id="76ff7-163">SSOM:  [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-163">SSOM:  [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx)</span></span>|
|<span data-ttu-id="76ff7-164">Erstellen einer Instanz eines Manager-Objekts im Kontext eines angegebenen Benutzers</span><span class="sxs-lookup"><span data-stu-id="76ff7-164">Create an instance of a manager object in the context of a specified user</span></span>|<span data-ttu-id="76ff7-165">CSOM: nicht implementiert</span><span class="sxs-lookup"><span data-stu-id="76ff7-165">CSOM: not implemented</span></span>  <br/> <span data-ttu-id="76ff7-166">JSOM: nicht implementiert</span><span class="sxs-lookup"><span data-stu-id="76ff7-166">JSOM: not implemented</span></span>  <br/> <span data-ttu-id="76ff7-167">REST: nicht implementiert</span><span class="sxs-lookup"><span data-stu-id="76ff7-167">REST: not implemented</span></span>  <br/> <span data-ttu-id="76ff7-168">SSOM:  [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx) (überladen)</span><span class="sxs-lookup"><span data-stu-id="76ff7-168">SSOM:  [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx) (overloaded)</span></span>|
|<span data-ttu-id="76ff7-169">Zulassen, dass der aktuelle Benutzer beginnt, einem Element zu folgen (das Folgen zu beenden)</span><span class="sxs-lookup"><span data-stu-id="76ff7-169">Have the current user start following (stop following) an item</span></span>|<span data-ttu-id="76ff7-170">CSOM:  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) ( [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) )</span><span class="sxs-lookup"><span data-stu-id="76ff7-170">CSOM:  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) ( [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) )</span></span> <br/> <span data-ttu-id="76ff7-171">JSOM:  [follow](http://msdn.microsoft.com/library/40d14320-27ba-2941-b0e2-be3b5a407c89%28Office.15%29.aspx) ( [stopFollowing](http://msdn.microsoft.com/library/65b0e9be-dc5e-09fb-c57f-7a933de09a4c%28Office.15%29.aspx))</span><span class="sxs-lookup"><span data-stu-id="76ff7-171">JSOM:  [follow](http://msdn.microsoft.com/library/40d14320-27ba-2941-b0e2-be3b5a407c89%28Office.15%29.aspx) ( [stopFollowing](http://msdn.microsoft.com/library/65b0e9be-dc5e-09fb-c57f-7a933de09a4c%28Office.15%29.aspx))</span></span>  <br/> <span data-ttu-id="76ff7-172">REST: **POST** [`<siteUri>/_api/social.following/Follow`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_Follow) ( [`<siteUri>/_api/social.following/StopFollowing`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_StopFollowing))           und Übergeben des Parameters _actor_ im Text der Anforderung</span><span class="sxs-lookup"><span data-stu-id="76ff7-172">REST:  Follow ( StopFollowing)          POST  ( ) and pass the  actor parameter in the request body</span></span> <br/> <span data-ttu-id="76ff7-173">SSOM:  [Follow](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.Follow.aspx) ( [StopFollowing](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.StopFollowing.aspx) )</span><span class="sxs-lookup"><span data-stu-id="76ff7-173">SSOM:  [Follow](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.Follow.aspx) ( [StopFollowing](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.StopFollowing.aspx) )</span></span>|
|<span data-ttu-id="76ff7-174">Herausfinden, ob der aktuelle Benutzer einem bestimmten Element folgt</span><span class="sxs-lookup"><span data-stu-id="76ff7-174">Find out whether the current user is following a particular item</span></span>|<span data-ttu-id="76ff7-175">CSOM:  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-175">CSOM:  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx)</span></span> <br/> <span data-ttu-id="76ff7-176">JSOM:  [isFollowed](http://msdn.microsoft.com/library/2c1f62e6-fb75-ad4d-c081-36408b418c21%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-176">JSOM:  [isFollowed](http://msdn.microsoft.com/library/2c1f62e6-fb75-ad4d-c081-36408b418c21%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="76ff7-177">REST: **POST** [`<siteUri>/_api/social.following/IsFollowed`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_IsFollowed) und Übergeben des Parameters _actor_ im Text der Anforderung</span><span class="sxs-lookup"><span data-stu-id="76ff7-177">REST:  IsFollowed          POST  and pass the actor parameter in the request body</span></span> <br/> <span data-ttu-id="76ff7-178">SSOM:  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.IsFollowed.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-178">SSOM:  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.IsFollowed.aspx)</span></span>|
|<span data-ttu-id="76ff7-179">Abrufen von Benutzern, Dokumenten, Websites und Tags denen der aktuelle Benutzer folgt</span><span class="sxs-lookup"><span data-stu-id="76ff7-179">Get the documents, sites, and/or tags that the current user is following</span></span>|<span data-ttu-id="76ff7-180">CSOM:  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-180">CSOM:  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx)</span></span> <br/> <span data-ttu-id="76ff7-181">JSOM:  [getFollowed](http://msdn.microsoft.com/library/432a7cec-6add-fdb1-a79f-a93414ee8cd3%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-181">JSOM:  [getFollowed](http://msdn.microsoft.com/library/432a7cec-6add-fdb1-a79f-a93414ee8cd3%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="76ff7-182">REST: **GET** [`<siteUri>/_api/social.following/my/Followed(types=2)`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_Followed) (documents = **2**, sites = **4**, tags = **8**.md)</span><span class="sxs-lookup"><span data-stu-id="76ff7-182">REST: **GET** [`<siteUri>/_api/social.following/my/Followed(types=2)`/_api/social.following/my/Followed(types=2)](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_Followed) (documents = **2**, sites = **4**, tags = **8**)</span></span>  <br/> <span data-ttu-id="76ff7-183">SSOM:  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetFollowed.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-183">SSOM:  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetFollowed.aspx)</span></span>|
|<span data-ttu-id="76ff7-184">Abrufen der Anzahl von Benutzern, Dokumenten, Websites und Tags denen der Benutzer folgt</span><span class="sxs-lookup"><span data-stu-id="76ff7-184">Get the count of documents, sites, and/or tags that the user is following</span></span>|<span data-ttu-id="76ff7-185">CSOM:  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-185">CSOM:  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx)</span></span> <br/> <span data-ttu-id="76ff7-186">JSOM:  [getFollowedCount](http://msdn.microsoft.com/library/97b53b4f-481a-cf41-1854-8f3ff860b2bb%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-186">JSOM:  [getFollowedCount](http://msdn.microsoft.com/library/97b53b4f-481a-cf41-1854-8f3ff860b2bb%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="76ff7-187">REST: **GET** [`<siteUri>/_api/social.following/my/FollowedCount(types=2)`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_FollowedCount) (documents = **2**, sites = **4**, tags = **8**.md)</span><span class="sxs-lookup"><span data-stu-id="76ff7-187">REST: **GET** [`<siteUri>/_api/social.following/my/FollowedCount(types=2)`/_api/social.following/my/FollowedCount(types=2)](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_FollowedCount) (documents = **2**, sites = **4**, tags = **8**)</span></span>  <br/> <span data-ttu-id="76ff7-188">SSOM:  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetFollowedCount.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-188">SSOM:  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetFollowedCount.aspx)</span></span>|
|<span data-ttu-id="76ff7-189">Abrufen des URI der Website, die die Dokumente des aktuellen Benutzers auflistet, denen gefolgt wird</span><span class="sxs-lookup"><span data-stu-id="76ff7-189">Get the URI of the site that lists the current user's followed documents</span></span>|<span data-ttu-id="76ff7-190">CSOM:  [FollowedDocumentsUri](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.FollowedDocumentsUri.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-190">CSOM:  [FollowedDocumentsUri](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.FollowedDocumentsUri.aspx)</span></span> <br/> <span data-ttu-id="76ff7-191">JSOM:  [followedDocumentsUri](http://msdn.microsoft.com/library/3a70b9c7-abd7-94ff-d730-70298673d6ec%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-191">JSOM:  [followedDocumentsUri](http://msdn.microsoft.com/library/3a70b9c7-abd7-94ff-d730-70298673d6ec%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="76ff7-192">REST: **GET** [`<siteUri>/_api/social.following/my/FollowedDocumentsUri`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_MyFollowedDocumentsUri)</span><span class="sxs-lookup"><span data-stu-id="76ff7-192">REST:  GetPropertiesFor          GET </span></span> <br/> <span data-ttu-id="76ff7-193">SSOM:  [FollowedDocumentsUri](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.FollowedDocumentsUri.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-193">SSOM:  [FollowedDocumentsUri](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.FollowedDocumentsUri.aspx)</span></span>|
|<span data-ttu-id="76ff7-194">Abrufen des URI der Website, die die Websites des aktuellen Benutzers auflistet, denen gefolgt wird</span><span class="sxs-lookup"><span data-stu-id="76ff7-194">Get the URI of the site that lists the current user's followed sites</span></span>|<span data-ttu-id="76ff7-195">CSOM:  [FollowedSitesUri](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.FollowedSitesUri.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-195">CSOM:  [FollowedSitesUri](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.FollowedSitesUri.aspx)</span></span> <br/> <span data-ttu-id="76ff7-196">JSOM:  [followedSitesUri](http://msdn.microsoft.com/library/829404bc-1b3a-7545-5e95-0922df330084%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-196">JSOM:  [followedSitesUri](http://msdn.microsoft.com/library/829404bc-1b3a-7545-5e95-0922df330084%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="76ff7-197">REST: **GET** [`<siteUri>/_api/social.following/my/FollowedSitesUri`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_MyFollowedSitesUri)</span><span class="sxs-lookup"><span data-stu-id="76ff7-197">REST:  GetPropertiesFor          GET </span></span> <br/> <span data-ttu-id="76ff7-198">SSOM:  [FollowedSitesUri](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.FollowedSitesUri.aspx)</span><span class="sxs-lookup"><span data-stu-id="76ff7-198">SSOM:  [FollowedSitesUri](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.FollowedSitesUri.aspx)</span></span>|
   

> <span data-ttu-id="76ff7-199">**Hinweis:** Beispiele für die Verwendung des REST-Diensts, um Inhalten zu folgen, finden Sie unter  [Vorgehensweise: Folgen von Dokumenten, Websites und Tags mithilfe des REST-Diensts in SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md).</span><span class="sxs-lookup"><span data-stu-id="76ff7-199">**Note** For examples that show how to use the REST service to follow content, see  [How to: Follow documents, sites, and tags by using the REST service in SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md).</span></span> 
  
    
    


## <a name="how-to-get-a-tags-guid-based-on-the-tags-name-by-using-the-javascript-object-model"></a><span data-ttu-id="76ff7-200">Abrufen der GUID eines Tags basierend auf dem Namen des Tags mithilfe des JavaScript-Objektmodells</span><span class="sxs-lookup"><span data-stu-id="76ff7-200">How to get a tag's GUID based on the tag's name by using the JavaScript object model</span></span>
<span data-ttu-id="76ff7-201"><a name="bk_getTagGuid"> </a></span><span class="sxs-lookup"><span data-stu-id="76ff7-201"></span></span>

<span data-ttu-id="76ff7-p107">Um das Folgen eines Tags zu starten und zu beenden oder herauszufinden, ob der aktuelle Benutzer ihm folgt, benötigen Sie die GUID des Tags. Der folgende Code zeigt, wie Sie die GUID basierend auf dem Namen des Tags abrufen.</span><span class="sxs-lookup"><span data-stu-id="76ff7-p107">To start and stop following a tag or to find out whether the current user is following it, you need to use the tag's GUID. The following code shows how to get the GUID based on the tag name.</span></span>
  
    
    
<span data-ttu-id="76ff7-204">Bevor Sie den Code ausführen, müssen Sie einen Verweis zu **sp.taxonomy.js** hinzufügen und den Namen des Platzhaltertags in den Namen eines vorhandenen Tags ändern.</span><span class="sxs-lookup"><span data-stu-id="76ff7-204">Before you run the code, you need to add a reference to **sp.taxonomy.js** and change the placeholder tag name with the name of an existing tag.</span></span>
  
    
    



```

function getTagGuid() {
    var tagName = '#tally';
    var clientContext = new SP.ClientContext.get_current();
    var label = SP.Taxonomy.LabelMatchInformation.newObject(clientContext);
    label.set_termLabel(tagName);
    label.set_trimUnavailable(false);
    var taxSession = SP.Taxonomy.TaxonomySession.getTaxonomySession(clientContext);
    var termStore = taxSession.getDefaultKeywordsTermStore();
    var termSet = termStore.get_hashTagsTermSet();
    terms = termSet.getTerms(label);
    clientContext.load(terms);
    clientContext.executeQueryAsync(
        function () {
            var tag = terms.get_item(0);
            if (tag !== null) {
                var tagGuid = tag.get_id().toString();
                if (!SP.ScriptUtility.isNullOrEmptyString(tagGuid)) {
                    alert(tagGuid);
                }
            }
        },
        function (sender, args) {
            alert(args.get_message());
        }
    );
}

```


## <a name="additional-resources"></a><span data-ttu-id="76ff7-205">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="76ff7-205">Additional resources</span></span>
<span data-ttu-id="76ff7-206"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="76ff7-206"></span></span>


-  [<span data-ttu-id="76ff7-207">Vorgehensweise: Führen Sie Dokumente und Websites mit .NET Client-Objektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="76ff7-207">How to: Follow documents and sites by using the .NET client object model in SharePoint</span></span>](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)
    
  
-  [<span data-ttu-id="76ff7-208">Vorgehensweise: führen Sie Dokumente, Websites und Tags mithilfe des REST-Diensts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="76ff7-208">How to: Follow documents, sites, and tags by using the REST service in SharePoint</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)
    
  
-  [<span data-ttu-id="76ff7-209">REST-API-Referenz zum Folgen von Personen und Inhalten für SharePoint</span><span class="sxs-lookup"><span data-stu-id="76ff7-209">Following people and content REST API reference for SharePoint</span></span>](following-people-and-content-rest-api-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="76ff7-210">Soziale Funktionen und Zusammenarbeit in SharePoint</span><span class="sxs-lookup"><span data-stu-id="76ff7-210">Social and collaboration features in SharePoint</span></span>](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [<span data-ttu-id="76ff7-211">Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint</span><span class="sxs-lookup"><span data-stu-id="76ff7-211">Get started developing with social features in SharePoint</span></span>](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [<span data-ttu-id="76ff7-212">Folgen von Personen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="76ff7-212">Follow people in SharePoint</span></span>](follow-people-in-sharepoint.md)
    
  