---
title: "Auswählen des richtigen API-Satzes in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f36645da-77c5-47f1-a2ca-13d4b62b320d
ms.openlocfilehash: 7d2fb4dadd47e19483ff22e93f0b990c41a75540
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="choose-the-right-api-set-in-sharepoint"></a><span data-ttu-id="d8e7f-102">Auswählen des richtigen API-Satzes in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d8e7f-102">Choose the right API set in SharePoint</span></span>
<span data-ttu-id="d8e7f-103">Erfahren Sie mehr über die verschiedenen API-Gruppen, die in SharePoint bereitgestellt werden, einschließlich des Serverobjektmodells und der verschiedenen Clientobjektmodellen und des REST/OData-Webdiensts.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-103">Learn about the several sets of APIs that are provided in SharePoint, including the server object model and the various client object models, and the REST/OData web service.</span></span>
    
    

## <a name="factors-that-determine-which-api-set-to-use"></a><span data-ttu-id="d8e7f-104">Faktoren, die bestimmen, welche API-Gruppe verwendet werden soll</span><span class="sxs-lookup"><span data-stu-id="d8e7f-104">Factors that determine which API set to use</span></span>
<span data-ttu-id="d8e7f-105"><a name="Factors"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e7f-105"><a name="Factors"> </a></span></span>

<span data-ttu-id="d8e7f-p101">Sie können aus verschiedenen API-Gruppen wählen, um auf die SharePoint-Plattform zuzugreifen. Welche Sie verwenden sollten, hängt von folgenden Faktoren ab:</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p101">You can choose from several sets of APIs to access the SharePoint platform. Which one you use depends on the following factors:</span></span>
  
    
    

- <span data-ttu-id="d8e7f-p102">**Der Anwendungstyp.** Zu den Möglichkeiten gehören u. a. folgende, sich nicht gegenseitig ausschließende Kategorien: eine SharePoint-Add-In, ein Webpart auf einer SharePoint-Seite, eine Silverlight-Anwendung, die auf einem Client-Computer oder einem Client-Mobilgerät ausgeführt wird, eine ASP.NET-Anwendung, die in SharePoint über ein IFrame-Element verfügbar ist, JavaScript, das auf einer SharePoint-Websiteseite ausgeführt wird, eine SharePoint-Anwendungsseite, eine Microsoft .NET Framework-Anwendung, die auf einem Client-Computer ausgeführt wird, ein Windows PowerShell-Skript und ein Zeitgeberauftrag, der auf einem SharePoint-Server ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p102">**The type of application.** The possibilities include, but are not limited to, the following, which are not mutually exclusive categories: an SharePoint Add-in, a Web Part on a SharePoint page, a Silverlight application running on either a client computer or a client mobile device, an ASP.NET application exposed in SharePoint by an IFrame, JavaScript running in a SharePoint site page, a SharePoint application page, a Microsoft .NET Framework application running on a client computer, a Windows PowerShell script, and a timer job running on a SharePoint server.</span></span>
    
  
- <span data-ttu-id="d8e7f-p103">**Ihre vorhandenen Fachkenntnisse.** Überraschenderweise können Sie Anwendungen in SharePoint erstellen, ohne sich mit dem Programmieren in SharePoint beschäftigen zu müssen. Sie können direkt mit der SharePoint-Entwicklung beginnen, wenn Sie bereits versiert im Umgang mit folgenden Programmierungsmodellen sind:</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p103">**Your existing skills.** To a surprising degree, you can create applications in SharePoint without needing to learn a lot about SharePoint programming. You can jump right into SharePoint development if you already have experience in any of the following programming models:</span></span>
    
  - <span data-ttu-id="d8e7f-113">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d8e7f-113">JavaScript</span></span>
    
  
  - <span data-ttu-id="d8e7f-114">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d8e7f-114">ASP.NET</span></span>
    
  
  - <span data-ttu-id="d8e7f-115">REST/OData</span><span class="sxs-lookup"><span data-stu-id="d8e7f-115">REST/OData</span></span>
    
  
  - <span data-ttu-id="d8e7f-116">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="d8e7f-116">.NET Framework</span></span>
    
  
  - <span data-ttu-id="d8e7f-117">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="d8e7f-117">Windows Phone</span></span>
    
  
  - <span data-ttu-id="d8e7f-118">Silverlight</span><span class="sxs-lookup"><span data-stu-id="d8e7f-118">Silverlight</span></span>
    
  
  - <span data-ttu-id="d8e7f-119">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-119">Windows PowerShell</span></span>
    
  
- <span data-ttu-id="d8e7f-p104">**Das Gerät, auf dem der Code ausgeführt wird.** Zu den Möglichkeiten gehört ein Server in der SharePoint-Farm, ein externer Server, wie z. B. ein Server in der Cloud, ein Client-Computer und ein Mobilgerät.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p104">**The device on which the code runs.** The possibilities include a server in the SharePoint farm, an external server such as a server in the cloud, a client computer, and a mobile device.</span></span>
    
  
<span data-ttu-id="d8e7f-p105">In diesem Thema erhalten Sie einen Überblick zu den verschiedenen API-Gruppen, die von SharePoint bereitgestellt werden. In Abbildung 1 ist dargestellt, welche API-Gruppen verwendet werden können, um eine der 13 allgemeinen SharePoint-bezogenen Anwendungen zu entwickeln. Bei vielen Anwendungen können Sie verschiedene APIs auswählen.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p105">This topic provides an overview of the various API sets that are provided by SharePoint. Figure 1 shows which sets of APIs can be used to develop each of 13 common SharePoint-related applications. For many applications, you can choose from more than one API.</span></span>
  
    
    

<span data-ttu-id="d8e7f-125">**Abbildung 1. Ausgewählte SharePoint-Erweiterungstypen und API-Gruppen in SharePoint**</span><span class="sxs-lookup"><span data-stu-id="d8e7f-125">**Figure 1. Selected SharePoint extension types and SharePoint sets of APIs**</span></span>

  
    
    

  
    
    
![Mengendiagramm von API-Sätzen und SharePoint-App-Typen](../images/SharePointAPIsetsandselectedSharePointextensions.png)
  
    
    

  
    
    
<span data-ttu-id="d8e7f-p106">In der folgenden Tabelle finden Sie Anleitungen dazu, welche API-Gruppen Sie für eine ausgewählte Liste allgemeiner SharePoint-Erweiterungsprojekte verwenden sollten. In den restlichen Abschnitten dieses Themas werden die verschiedenen API-Gruppen erläutert.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p106">The following table provides guidance on which set of APIs to use for a selected list of common SharePoint extensibility projects. The remaining sections of this topic describe the various sets of APIs.</span></span>
  
    
    


|<span data-ttu-id="d8e7f-129">**Wenn Sie diese Funktionen verwenden möchten...**</span><span class="sxs-lookup"><span data-stu-id="d8e7f-129">**If you want to do this ...**</span></span>|<span data-ttu-id="d8e7f-130">**... sollten Sie diese APIs einsetzen**</span><span class="sxs-lookup"><span data-stu-id="d8e7f-130">**... use these APIs**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d8e7f-131">Erstellen Sie eine ASP.NET-Webanwendung, die Erstell-/Lese-/Aktualisier-/Lösch-Vorgänge über eine Firewall zu SharePoint-Daten oder externen Daten durchführt, die in SharePoint durch einen Microsoft Business Connectivity Services (BCS) externen Inhaltstyp dargestellt werden</span><span class="sxs-lookup"><span data-stu-id="d8e7f-131">Create an ASP.NET web application that performs create/read/update/deleted (CRUD) operations across a firewall on SharePoint data or external data that is surfaced in SharePoint by a Microsoft Business Connectivity Services (BCS) external content type</span></span>  <br/> |<span data-ttu-id="d8e7f-132">JavaScript-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-132">JavaScript client object model</span></span>  <br/> |
|<span data-ttu-id="d8e7f-133">Erstellen Sie eine ASP.NET-Webanwendung, die CRUD-Vorgänge zu SharePoint-Daten oder externen Daten durchführt, die in SharePoint durch einen externen BCS-Inhaltstyp dargestellt werden, SharePoint jedoch nicht über eine Firewall aufrufen müssen</span><span class="sxs-lookup"><span data-stu-id="d8e7f-133">Create an ASP.NET web application that performs CRUD operations on SharePoint data or external data that is surfaced in SharePoint by a BCS external content type, but does not have to call SharePoint across a firewall</span></span>  <br/> |<span data-ttu-id="d8e7f-134">.NET Framework-Clientobjektmodell, Silverlight-Clientobjektmodell oder REST/OData-Endpunkte</span><span class="sxs-lookup"><span data-stu-id="d8e7f-134">.NET Framework client object model, Silverlight client object model, or REST/OData endpoints</span></span>  <br/> |
|<span data-ttu-id="d8e7f-135">Erstellen Sie eine LAMP-Webanwendung, die CRUD-Vorgänge zu SharePoint-Daten oder externen Daten durchführt, die in SharePoint durch einen externen BCS-Inhaltstyp dargestellt werden</span><span class="sxs-lookup"><span data-stu-id="d8e7f-135">Create a LAMP web application that performs CRUD operations on SharePoint data or external data that is surfaced in SharePoint by a BCS external content type</span></span>  <br/> |<span data-ttu-id="d8e7f-136">REST/OData-Endpunkte</span><span class="sxs-lookup"><span data-stu-id="d8e7f-136">REST/OData endpoints</span></span>  <br/> |
|<span data-ttu-id="d8e7f-137">Erstellen Sie eine Windows Phone-App, die CRUD-Vorgänge zu SharePoint-Daten durchführt</span><span class="sxs-lookup"><span data-stu-id="d8e7f-137">Create a Windows Phone app that performs CRUD operations on SharePoint data</span></span>  <br/> |<span data-ttu-id="d8e7f-138">Mobiles Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-138">Mobile client object model</span></span>  <br/> |
|<span data-ttu-id="d8e7f-139">Erstellen Sie eine Windows Phone-App, die den Microsoft-Pushbenachrichtigungsdienst verwendet, um das Mobilgerät über Ereignisse in SharePoint zu benachrichtigen</span><span class="sxs-lookup"><span data-stu-id="d8e7f-139">Create a Windows Phone app that uses the Microsoft Push Notification Service to alert the mobile device of events in SharePoint</span></span>  <br/> |<span data-ttu-id="d8e7f-140">Mobiles Clientobjektmodell und das Serverobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-140">Mobile client object model and the server object model</span></span>  <br/> |
|<span data-ttu-id="d8e7f-141">Erstellen Sie eine iOS- oder Android-App, die CRUD-Vorgänge zu SharePoint-Daten durchführt</span><span class="sxs-lookup"><span data-stu-id="d8e7f-141">Create an iOS or Android app that performs CRUD operations on SharePoint data</span></span>  <br/> |<span data-ttu-id="d8e7f-142">REST-/OData-Endpunkte</span><span class="sxs-lookup"><span data-stu-id="d8e7f-142">REST/OData endpoints</span></span>  <br/> |
|<span data-ttu-id="d8e7f-143">Erstellen Sie eine .NET Framework-Anwendung, die CRUD-Vorgänge zu SharePoint-Daten durchführt</span><span class="sxs-lookup"><span data-stu-id="d8e7f-143">Create a .NET Framework application that performs CRUD operations on SharePoint data</span></span>  <br/> |<span data-ttu-id="d8e7f-144">.NET Framework-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-144">.NET Framework client object model</span></span>  <br/> |
|<span data-ttu-id="d8e7f-145">Erstellen Sie eine Silverlight-Anwendung, die CRUD-Vorgänge zu SharePoint-Daten durchführt</span><span class="sxs-lookup"><span data-stu-id="d8e7f-145">Create a Silverlight application that performs CRUD operations on SharePoint data</span></span>  <br/> |<span data-ttu-id="d8e7f-146">Silverlight-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-146">Silverlight client object model</span></span>  <br/> |
|<span data-ttu-id="d8e7f-147">Erstellen Sie eine HTML/JavaScript-Anwendung, die CRUD-Vorgänge zu SharePoint-Daten durchführt</span><span class="sxs-lookup"><span data-stu-id="d8e7f-147">Create an HTML/JavaScript application that performs CRUD operations on SharePoint data</span></span>  <br/> |<span data-ttu-id="d8e7f-148">JavaScript-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-148">JavaScript client object model</span></span>  <br/> |
|<span data-ttu-id="d8e7f-149">Erstellen Sie eine Office-Add-In, die mit SharePoint funktioniert</span><span class="sxs-lookup"><span data-stu-id="d8e7f-149">Create an Office Add-in that works with SharePoint</span></span>  <br/> |<span data-ttu-id="d8e7f-150">JavaScript-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-150">JavaScript client object model</span></span>  <br/> |
|<span data-ttu-id="d8e7f-151">Erstellen Sie einen benutzerdefinierten Windows PowerShell-Befehl</span><span class="sxs-lookup"><span data-stu-id="d8e7f-151">Create a custom Windows PowerShell command</span></span>  <br/> |<span data-ttu-id="d8e7f-152">Serverobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-152">Server object model</span></span>  <br/> |
|<span data-ttu-id="d8e7f-153">Erstellen eines Zeitgeberauftrags</span><span class="sxs-lookup"><span data-stu-id="d8e7f-153">Create a timer job</span></span>  <br/> |<span data-ttu-id="d8e7f-154">Serverobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-154">Server object model</span></span>  <br/> |
|<span data-ttu-id="d8e7f-155">Erstellen einer Erweiterung der Zentraladministration</span><span class="sxs-lookup"><span data-stu-id="d8e7f-155">Create an extension of Central Administration</span></span>  <br/> |<span data-ttu-id="d8e7f-156">Serverobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-156">Server object model</span></span>  <br/> |
|<span data-ttu-id="d8e7f-157">Erstellen eines konsistenten Branding in einer ganzen SharePoint-Farm</span><span class="sxs-lookup"><span data-stu-id="d8e7f-157">Create consistent branding across an entire SharePoint farm</span></span>  <br/> |<span data-ttu-id="d8e7f-158">Serverobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-158">Server object model</span></span>  <br/> |
|<span data-ttu-id="d8e7f-159">Erstellen eines benutzerdefinierten Webparts, einer Anwendungsseite oder eines ASP.NET-Benutzersteuerelements</span><span class="sxs-lookup"><span data-stu-id="d8e7f-159">Create a custom Web Part, application page, or ASP.NET user control</span></span>  <br/> |<span data-ttu-id="d8e7f-160">Serverobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-160">Server object model</span></span>  <br/> <span data-ttu-id="d8e7f-161">**Wichtig:** Wenn sich die Funktion, die Sie Kunden anbieten möchten, nicht an der SharePoint-Verwaltung in einem breiteren Bereich als eine Websitesammlung orientiert, wird empfohlen, anstatt das Serverobjektmodell zu verwenden, ein SharePoint-Add-In zu erstellen, das eine ASP.NET-Remote-Webanwendung mit benutzerdefinierten Webparts und ggf. Benutzersteuerelementen umfasst.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-161">**Important:** If the functionality you want to offer customers is not oriented to SharePoint administration at a scope broader than site collection, we recommend that, instead of using the server object model, you create an SharePoint Add-in that includes a remote ASP.NET web application with custom Web Parts and user controls as needed.</span></span> <span data-ttu-id="d8e7f-162">Weitere Informationen dazu finden Sie in den oberen beiden Zeilen dieser Tabelle.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-162">See the top two rows of this table.</span></span>           |
   

## <a name="server-object-model"></a><span data-ttu-id="d8e7f-163">Serverobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-163">Server object model</span></span>
<span data-ttu-id="d8e7f-164"><a name="ServerOM"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e7f-164"><a name="ServerOM"> </a></span></span>

<span data-ttu-id="d8e7f-p108">Die größte API-Gruppe befindet sich im Serverobjektmodell der verwalteten Klassen. Auf der SharePoint Foundation 2013-Ebene umfasst dieses Objektmodell Klassen und Elemente, mit denen die Programmsteuerung der Basiswebsite und der Listenstruktur von SharePoint Foundation erfolgen kann. Der Großteil dieser Klassen befindet sich im  [Microsoft.SharePoint](https://msdn.microsoft.com/library/Microsoft.SharePoint.aspx) -Namespace. Außerdem können Sie fast jede SharePoint Foundation-Komponente erweitern, indem Sie das Serverobjektmodell verwenden, dazu gehören auch Workflows, Warnungen, Webparts, Standardsuchen und Microsoft Business Connectivity Services (BCS). Das Serverobjektmodell umfasst außerdem umfangreiche API-Gruppen-Aktivierungserweiterungen der Verwaltung und des Sicherheitssystems von SharePoint Foundation, einschließlich Sicherung, Farmintegrität und Diagnose, Protokollierung, Farm- und Webanwendungsverwaltung, Upgrade, Bereitstellung, Zwischenspeicherung und Windows PowerShell-Anpassung.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p108">The largest set of APIs is in the server object model of managed classes. At the level of SharePoint Foundation 2013, this object model includes classes and members that enable programmatic control of the basic site and list structure of SharePoint Foundation. Most of these classes are in the  [Microsoft.SharePoint](https://msdn.microsoft.com/library/Microsoft.SharePoint.aspx) namespace. In addition, you can extend almost every SharePoint Foundation component by using the server object model, including workflows, alerts, Web Parts, basic search, and Microsoft Business Connectivity Services (BCS). The server object model also includes an extensive set of APIs enable extensions of the administration and security system of SharePoint Foundation, including backup, farm health and diagnostics, logging, farm and web application management, upgrade, deployment, caching, and Windows PowerShell customization.</span></span>
  
    
    
<span data-ttu-id="d8e7f-170">Auf der SharePoint-Ebene werden noch viele weitere Klassen hinzugefügt, um die Programmierung von Enterprise Content Management (ECM), Benutzerprofilen, Taxonomien, der erweiterten Suche und weiterer Features von SharePoint zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-170">At the level of SharePoint, many more classes are added to enable programming of Enterprise Content Management (ECM), user profiles, taxonomy, advanced search, and other features of SharePoint.</span></span>
  
    
    
<span data-ttu-id="d8e7f-p109">Sie können  [LINQ to Objects](http://msdn.microsoft.com/de-DE/library/bb397919.aspx) verwenden, um jede **IEnumerable**-Sammlung im Speicher abzufragen, mit  [LINQ to SharePoint-Anbieter](http://msdn.microsoft.com/library/3fa2dc5f-d308-4337-aefd-191a5df8dbbe%28Office.15%29.aspx) haben Sie jedoch die Möglichkeit, die Listen direkt in den SharePoint-Inhaltsdatenbanken abzufragen. Genau genommen ist dieser Anbieter nicht für die anderen in diesem Thema erläuterten API-Gruppen verfügbar; es gibt jedoch Möglichkeiten, LINQ-Syntax für den Großteil der anderen Gruppen zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p109">You can use  [LINQ to Objects](http://msdn.microsoft.com/de-DE/library/bb397919.aspx) to query any **IEnumerable** collection in memory, but a [LINQ to SharePoint provider](http://msdn.microsoft.com/library/3fa2dc5f-d308-4337-aefd-191a5df8dbbe%28Office.15%29.aspx) enables direct querying of the lists in the SharePoint content databases. Strictly speaking, this provider is not available with any other set of APIs discussed in this topic; however, there are ways to use LINQ syntax in most of the others.</span></span>
  
    
    
<span data-ttu-id="d8e7f-p110">Die Assemblys, die die integrierten serverseitigen Klassen definieren, sind im globalen Assemblycache jedes Servers installiert, wenn SharePoint installiert ist. Wenn Sie etwas für das Serverobjektmodell programmieren, werden Ihre Assemblys als Farmlösungen im globalen Assemblycache installiert.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p110">The assemblies that define the built-in server-side classes are installed to the global assembly cache of each server when SharePoint is installed. When you program against the server object model, your assemblies are installed as farm solutions to the global assembly cache.</span></span>
  
> [!NOTE]
> <span data-ttu-id="d8e7f-175">Das Entwickeln von neuen Sandkastenlösungen für SharePoint ist eine veraltete Methode, die dem Entwickeln von SharePoint-Add-Ins gewichen ist. Sandkastenlösungen können jedoch weiterhin in Websitesammlungen in SharePoint installiert werden.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-175">Note: Developing new sandboxed solutions against SharePoint is deprecated in favor of developing SharePoint Add-ins, but sandboxed solutions can still be installed to site collections on SharePoint.</span></span> <span data-ttu-id="d8e7f-176">Die Assemblys dieser Lösungen verbleiben im Paket, sofern sie nicht verwendet werden, ansonsten werden sie temporär in einem Ordner auf dem Server installiert.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-176">The assemblies of these solutions remain in the package except when they are actually in use, at which time they are temporarily installed to a folder on the server.</span></span> <span data-ttu-id="d8e7f-177">Weitere Informationen finden Sie unter [Wo werden Assemblys in Sandkastenlösungen bereitgestellt?](http://msdn.microsoft.com/library/dadbb20b-1bf7-442c-9eeb-bd9f01dbda45%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8e7f-177">For more information, see  [Where are Assemblies in Sandboxed Solutions Deployed?](http://msdn.microsoft.com/library/dadbb20b-1bf7-442c-9eeb-bd9f01dbda45%28Office.15%29.aspx).</span></span> 
  
    
    


### <a name="limitations-on-when-you-can-use-the-server-object-model"></a><span data-ttu-id="d8e7f-178">Beschränkungen zum Verwenden des Serverobjektmodells</span><span class="sxs-lookup"><span data-stu-id="d8e7f-178">Limitations on when you can use the server object model</span></span>

<span data-ttu-id="d8e7f-p112">Die benutzerdefinierte Logik in SharePoint-Add-Ins wird immer "hinunter" bis zum Client oder "hinauf" zur Cloud verteilt (oder "hinüber" zu einem Server außerhalb der SharePoint-Farm). In all diesen Verteilungsmodellen muss eines der Clientobjektmodelle oder die die REST/OData-Endpunkte verwendet werden. (Sie können das Serverobjektmodell nicht in einer SharePoint-Add-In verwenden). Wenn die App beispielsweise von SharePoint gehostete Seiten enthält, können diese Seiten auf SharePoint-Daten zugreifen, indem Sie das JavaScript-Clientobjektmodell verwenden. Diese Seiten können auch Silverlight-Anwendungen verfügbar machen, die das SharePoint Silverlight-Clientobjektmodell verwenden. Weitere Informationen über SharePoint-Add-Ins finden Sie unter  [Wichtige Aspekte der Architektur und Entwicklungslandschaft von Add-Ins für SharePoint](http://msdn.microsoft.com/library/ae96572b-8f06-4fd3-854f-fc312f7f2d88%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p112">Custom logic in SharePoint Add-ins is always distributed "down" to the client or "up" to the cloud (or "over" to some server outside the SharePoint farm). In all of these distribution models, one of the client object models or the REST/OData endpoints must be used. (You cannot use the server object model in an SharePoint Add-in.) For example, if the app contains SharePoint-hosted pages, those pages can access SharePoint data by using the JavaScript client object model. Such pages could also expose Silverlight applications that use the SharePoint Silverlight client object model. For more information about SharePoint Add-ins, see  [Important aspects of the SharePoint Add-in architecture and development landscape](http://msdn.microsoft.com/library/ae96572b-8f06-4fd3-854f-fc312f7f2d88%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="client-object-models-for-managed-code"></a><span data-ttu-id="d8e7f-184">Clientobjektmodelle für verwalteten Code</span><span class="sxs-lookup"><span data-stu-id="d8e7f-184">Client object models for managed code</span></span>
<span data-ttu-id="d8e7f-185"><a name="ClientManagedOM"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e7f-185"><a name="ClientManagedOM"> </a></span></span>

<span data-ttu-id="d8e7f-186">SharePoint verfügt über drei Clientobjektmodelle für verwalteten Code: .NET, Silverlight und Mobil.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-186">SharePoint has three client object models for managed code: .NET, Silverlight, and mobile.</span></span>
  
    
    

### <a name="net-client-object-model"></a><span data-ttu-id="d8e7f-187">.NET-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-187">.NET client object model</span></span>

<span data-ttu-id="d8e7f-p113">Das SharePoint-Objektmodell für .NET Framework wird in .NET Framework-Anwendungen verwendet, die auf einem Windows-Client (kein Telefon) ausgeführt werden. Folgende Clients gehören zu dieser Gruppe:</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p113">The SharePoint object model for .NET Framework is used in .NET Framework applications that run on a non-phone Windows client. Any of the following counts as such a client:</span></span>
  
    
    

- <span data-ttu-id="d8e7f-190">Ein Benutzer-Computer</span><span class="sxs-lookup"><span data-stu-id="d8e7f-190">A user's computer</span></span>
    
  
- <span data-ttu-id="d8e7f-191">Ein Server außerhalb der SharePoint-Farm</span><span class="sxs-lookup"><span data-stu-id="d8e7f-191">A server that is external to the SharePoint farm</span></span>
    
  
- <span data-ttu-id="d8e7f-192">Eine Webrolle oder Workerrolle in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d8e7f-192">A web role or worker role on Microsoft Azure</span></span>
    
  
<span data-ttu-id="d8e7f-193">Nahezu jede Klasse im zentralen serverseitigen Objektmodell für Websites und Listen verfügt über eine entsprechende Klasse im .NET Framework-Clientobjektmodell.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-193">Almost every class in the core site and list server object model has a corresponding class in the .NET Framework client object model.</span></span> <span data-ttu-id="d8e7f-194">Außerdem macht das .NET Framework-Clientobjektmodell eine vollständige API-Gruppe zum Erweitern weiterer Features verfügbar. Dazu gehören einige SharePoint-Features, wie z. B. ECM, Taxonomie, Benutzerprofile, erweiterte Suche, Analyse, BCS und andere.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-194">In addition, the .NET Framework client object model exposes a full set of APIs for extending other features, including some SharePoint features such as ECM, taxonomy, user profiles, advanced search, analytics, BCS, and others.</span></span>
  
    
    
<span data-ttu-id="d8e7f-p115">Um die Leistung zu verbessern, werden im .NET Framework-Clientobjektmodell geschriebene Codezeilen in Batches an den SharePoint-Server gesendet. Dort werden sie in serverseitigen Code konvertiert und ausgeführt. Die abgefragten Ergebnisse und der neue Status aller Variablen werden anschließend an den Client zurückgegeben. Als Entwickler können Sie bestimmen, ob ein Batch synchron oder asynchron ausgeführt wird. (Bei einem synchronen Batch wartet die .NET Framework-Anwendung auf die vom Server zurückgegebenen Ergebnisse, bevor sie fortfährt; bei einem asynchronen Batch wird die clientseitige Verarbeitung sofort fortgesetzt und Client-Benutzeroberfläche bleibt reaktionsfähig.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p115">To improve performance, lines of code written against in the .NET Framework client object model are sent to the SharePoint server in batches where they are converted to server-side code and executed. The queried results, and the new state of all variables, are then returned to the client. You as the developer determine whether a batch runs synchronously or asynchronously. (In a synchronous batch, the .NET Framework application waits for the returned results from the server before continuing; in an asynchronous batch, client-side processing continues immediately and the client user interface (UI) remains responsive.)</span></span>
  
    
    
<span data-ttu-id="d8e7f-p116">Sie können LINQ-Abfragesyntax in Ihrem Clientcode verwenden, um beliebige **IEnumerable**-Objekte abzufragen, dazu gehören auch SharePoint-Objekte, in denen **IEnumerable** implementiert ist. Wenn Sie so vorgehen, verwenden Sie jedoch [LINQ to Objects](http://msdn.microsoft.com/de-DE/library/bb397919.aspx) und nicht [LINQ to SharePoint-Anbieter](http://msdn.microsoft.com/library/3fa2dc5f-d308-4337-aefd-191a5df8dbbe%28Office.15%29.aspx), die dazugehörige Dokumentation ist also für clientseitigen Code nicht relevant.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p116">You can use LINQ query syntax in your client code to query any **IEnumerable** object, including SharePoint objects that implement **IEnumerable**. However, when you do this, you are using  [LINQ to Objects](http://msdn.microsoft.com/de-DE/library/bb397919.aspx), not the  [LINQ to SharePoint provider](http://msdn.microsoft.com/library/3fa2dc5f-d308-4337-aefd-191a5df8dbbe%28Office.15%29.aspx), so documentation of the latter is not relevant to client-side code.</span></span>
  
    
    
<span data-ttu-id="d8e7f-p117">Die Assemblys für das .NET Framework-Clientobjektmodel muss auf dem Client installiert sein. Sie sind in einem verteilbaren Paket enthalten, das Sie unter  [SharePoint-Clientkomponenten](http://www.microsoft.com/en-us/download/details.aspx?id=35585) abrufen können.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p117">The assemblies for the .NET Framework client object model must be installed on the client. They are included in a redistributable package that you can obtain on the  [SharePoint Client Components](http://www.microsoft.com/en-us/download/details.aspx?id=35585).</span></span>
  
    
    
<span data-ttu-id="d8e7f-203">Beispiele zur Verwendung des .NET Framework-Objektmodells finden Sie unter [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8e7f-203">For examples of using the .NET Framework object model, see  [Complete basic operations using SharePoint client library code](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx).</span></span>
  
> [!NOTE]
> <span data-ttu-id="d8e7f-204">Sie können auch die SharePoint REST/OData-Endpunkte in einer .NET Framework-Anwendung verwenden.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-204">Note: You can also use the SharePoint REST/OData endpoints in a .NET Framework application.</span></span> <span data-ttu-id="d8e7f-205">Einen Vergleich des .NET Framework-Clientobjektmodells mit den SharePoint REST-/OData-Endpunkten finden Sie im Abschnitt [REST-/OData-Endpunkte](#RESTOData) weiter unten in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-205">For a comparison of the .NET Framework client object model with the SharePoint REST/OData endpoints, see the section  [REST/OData endpoints](#RESTOData) later in this article.</span></span>
  
    
    


### <a name="silverlight-client-object-model"></a><span data-ttu-id="d8e7f-206">Silverlight-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-206">Silverlight client object model</span></span>

<span data-ttu-id="d8e7f-p119">Das SharePoint-Objektmodell für Silverlight wird in Silverlight-Anwendungen unabhängig davon verwendet, wo die kompilierte XAP-Datei gespeichert ist. Das kann eine Objektbibliothek auf einer SharePoint-Website, ein Client-Computer, ein Cloud-Speicher oder ein externer Server sein. In der Regel wird eine Silverlight-Anwendung SharePoint in einem  [SilverlightWebPart](https://msdn.microsoft.com/library/Microsoft.SharePoint.WebPartPages.SilverlightWebPart.aspx) -Objekt dargestellt. Das Silverlight-Clientobjektmodell in SharePoint ist fast identisch mit dem .NET Framework-Clientobjektmodell und umfasst Unterstützung für die gleichen Erweiterbarkeitsbereiche. Der Hauptunterschied liegt darin, dass in der Silverlight-Version alle Batches der Befehle asynchron an den Server gesendet werden, damit die Benutzeroberfläche aktiv bleibt.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p119">The SharePoint object model for Silverlight is used in Silverlight applications, regardless of where the compiled .xap file is persisted. It may be in an assets library on a SharePoint website, on a client computer, in cloud storage, or on an external server. Typically, a Silverlight application is surfaced in SharePoint in a  [SilverlightWebPart](https://msdn.microsoft.com/library/Microsoft.SharePoint.WebPartPages.SilverlightWebPart.aspx) object. The Silverlight client object model in SharePoint is nearly identical to the .NET Framework client object model, and it includes support for the same extensibility areas. The principal difference is that in the Silverlight version, all batches of commands are sent to the server asynchronously so that the UI of the application remains active.</span></span>
  
    
    
<span data-ttu-id="d8e7f-p120">Die Assemblys für das Silverlight-Clientobjektmodel werden auf jedem SharePoint-Server unter %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin gespeichert. Sie müssen nicht auf dem Computer installiert werden, auf dem die Silverlight-Anwendung läuft, haben jedoch die Möglichkeit dazu. Sie können sie auch in der XAP-Datei der Anwendung zu einem Paket zusammenfassen.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p120">The assemblies for the Silverlight client object model are persisted on every SharePoint server at %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin. They do not have to be installed on the computer that is running the Silverlight application, although you have the option of doing so. Also, you can package them into the .xap file of the application.</span></span>
  
    
    
<span data-ttu-id="d8e7f-p121">Silverlight XAP-Dateien können einer SharePoint-Add-Ins hinzugefügt werden, darunter auch von SharePoint gehostete Apps. Dabei wird die XAP-Datei in einer Bibliothek im App-Web bereitgestellt. (Weitere Informationen zu App-Webs finden Sie unter [Hostwebsites, Add-In-Websites und SharePoint-Komponenten in SharePoint](http://msdn.microsoft.com/library/b791cdf5-8aa2-47fa-bc4c-aee437354759%28Office.15%29.aspx).) So erhält man mit der Silverlight-App eine nützliche Methode zum Hinzufügen von benutzerdefiniertem SharePoint-Code in einer App, da benutzerdefinierter serverseitiger Code in SharePoint-Add-Ins nicht zulässig ist. Zudem können Silverlight-Entwickler für die Erstellung von SharePoint-Anwendungen mit einer minimalen Lernkurve nutzen.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p121">Silverlight .xap files can be included in SharePoint Add-ins, including SharePoint-hosted apps. In the latter case, the .xap file is deployed to a library on the app web. (For more information about app webs, see  [Host webs, add-in webs, and SharePoint components in SharePoint](http://msdn.microsoft.com/library/b791cdf5-8aa2-47fa-bc4c-aee437354759%28Office.15%29.aspx).) This makes a Silverlight application a useful way of including custom SharePoint code in an app, because custom server-side code is not allowed in SharePoint Add-ins. It also enables Silverlight developers to use their existing skills to create SharePoint applications with a minimal learning curve.</span></span>
  
> [!NOTE]
> <span data-ttu-id="d8e7f-218">Sie können auch die SharePoint REST-/OData-Endpunkte in einer Silverlight-Anwendung verwenden.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-218">Note: You can also use the SharePoint REST/OData endpoints in a Silverlight application.</span></span> <span data-ttu-id="d8e7f-219">Einen Vergleich des Silverlight-Clientobjektmodells mit den SharePoint REST-/OData-Endpunkten finden Sie im Abschnitt [REST-/OData-Endpunkte](#RESTOData) weiter unten in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-219">For a comparison of the Silverlight client object model with the SharePoint REST/OData endpoints, see the section  [REST/OData endpoints](#RESTOData) later in this article.</span></span>
  
    
    


### <a name="mobile-object-model"></a><span data-ttu-id="d8e7f-220">Mobiles Objektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-220">Mobile object model</span></span>

<span data-ttu-id="d8e7f-p123">Für Windows Phone-Geräte ist eine spezielle Version des Silverlight-Clientobjektmodells verfügbar. Es umfasst zusätzliche APIs, die nur für Telefone relevant sind, wie z. B. APIs, mit der sich eine Smartphone-App für Benachrichtigungen vom Microsoft-Pushbenachrichtigungsdienst registrieren kann. Sie unterstützt alle wichtigen SharePoint-Funktionen; es bietet jedoch keine Unterstützung für Nebenerweiterungsbereiche, die von den anderen beiden Clientobjektmodellen für verwalteten Code unterstützt werden. Verwenden Sie zum Zugreifen auf diese zusätzlichen Bereiche die SharePoint REST/OData-Endpunkte in Ihrer mobilen App. Weitere Informationen dazu finden Sie im Abschnitt  [REST/OData-Endpunkte](#RESTOData) weiter unten in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p123">A special version of the Silverlight client object model is available for Windows Phone devices. It includes some additional APIs that are relevant only to telephones, such as APIs that enable a phone app to register for notifications from the Microsoft Push Notification Service. It supports all core SharePoint functionality; however, it does not provide support for any of the non-core extensibility areas that are supported by the other two client object models for managed code. To access those additional areas, use the SharePoint REST/OData endpoints in your mobile app. See the section  [REST/OData endpoints](#RESTOData) later in this article.</span></span>
  
    
    
<span data-ttu-id="d8e7f-p124">Die Assemblys für das mobile Objektmodell werden auf jedem SharePoint-Server unter %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin gespeichert. Sie können Sie in der XAP-Datei in Ihrer Windows Phone-Anwendung zu einem Paket zusammenfassen.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p124">The assemblies for the mobile object model are persisted on every SharePoint server at %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin. You package them into the .xap file of your Windows Phone application.</span></span>
  
    
    

## <a name="javascript-object-model"></a><span data-ttu-id="d8e7f-228">JavaScript-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="d8e7f-228">JavaScript object model</span></span>
<span data-ttu-id="d8e7f-229"><a name="JavaScriptOM"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e7f-229"><a name="JavaScriptOM"> </a></span></span>

<span data-ttu-id="d8e7f-p125">SharePoint stellt ein JavaScript-Objektmodell für die Nutzung in einem Inline-Skript oder separaten JS-Dateien bereit. Es umfasst die gleichen Funktionen wie die Clientobjektmodelle .NET Framework und Silverlight. Genau wie das Silverlight-Clientobjektmodell bietet das JavaScript-Objektmodell eine nützliche Methode zum Hinzufügen von benutzerdefiniertem SharePoint-Code in einer App, da benutzerdefinierter serverseitiger Code in SharePoint-Add-Ins nicht zulässig ist. Zudem können Webentwickler ihre vorhandenen JavaScript-Kenntnisse für die Erstellung von SharePoint-Anwendungen mit einer minimalen Lernkurve nutzen.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p125">SharePoint provides a JavaScript object model for use in either inline script or separate .js files. It includes all the same functionality as the .NET Framework and Silverlight client object models. Like the Silverlight client object model, the JavaScript object model is a useful way of including custom SharePoint code in an app, because custom server-side code is not allowed in SharePoint Add-ins. It also enables web developers to use their existing JavaScript skills to create SharePoint applications with a minimal learning curve.</span></span>
  
    
    
<span data-ttu-id="d8e7f-p126">Genau wie Objektmodelle mit verwaltetem Code interagiert die JavaScript-Infrastruktur für SharePoint mit den Farm-Servern in Batches. Diese Batches werden immer asynchron ausgeführt. Außerdem ist es nun möglich, in JavaScript domänenübergreifend auf SharePoint-Daten zuzugreifen (jedoch nur Daten, die sich in der gleichen übergeordneten Websitesammlung befinden), was in vorherigen SharePoint-Versionen nicht möglich war. Weitere Informationen finden Sie unter  [Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx). Daten werden in JavaScript Object Notation (JSON) vom Server zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p126">Just like the managed-code client object models, the JavaScript infrastructure for SharePoint interacts with the farm servers in batches. These batches always run asynchronously. In addition, it is now possible to access SharePoint data across domains in JavaScript (but only data that is within the same parent site collection), which was not allowed in previous versions of SharePoint. For more information, see  [Access SharePoint data from add-ins using the cross-domain library](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx). Data is returned from the server in JavaScript Object Notation (JSON).</span></span>
  
    
    
<span data-ttu-id="d8e7f-238">Das JavaScript-Objektmodell ist in einer JS-Dateigruppe definiert, die sich auf jedem Server unter %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS befinden.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-238">The JavaScript object model is defined in a set of \*.js files located at %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS on each server.</span></span>
  
    
    
<span data-ttu-id="d8e7f-239">Beispiele zur Verwendung des .NET Framework-Objektmodells finden Sie unter [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8e7f-239">For examples of using the .NET Framework object model, see  [Complete basic operations using JavaScript library code in SharePoint](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx).</span></span>
  
> [!NOTE]
> <span data-ttu-id="d8e7f-240">Sie können auch die SharePoint REST-/OData-Endpunkte in einer JavaScript-Anwendung verwenden.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-240">Note: You can also use the SharePoint REST/OData endpoints in a JavaScript application.</span></span> <span data-ttu-id="d8e7f-241">Einen Vergleich des JavaScript-Clientobjektmodells mit den SharePoint REST-/OData-Endpunkten finden Sie im Abschnitt [REST-/OData-Endpunkte](#RESTOData).</span><span class="sxs-lookup"><span data-stu-id="d8e7f-241">For a comparison of the JavaScript client object model with SharePoint's REST/OData endpoints, see the following section,  [REST/OData endpoints](#RESTOData).</span></span> 
  
    
    


## <a name="restodata-endpoints"></a><span data-ttu-id="d8e7f-242">REST-/OData-Endpunkte</span><span class="sxs-lookup"><span data-stu-id="d8e7f-242">REST/OData endpoints</span></span>
<span data-ttu-id="d8e7f-243"><a name="RESTOData"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e7f-243"><a name="RESTOData"> </a></span></span>

<span data-ttu-id="d8e7f-p128">Für den Zugriff auf SharePoint-Entitäten über Clienttechnologien, die nicht JavaScript verwenden und nicht auf den Plattformen .NET Framework oder Silverlight basieren, bietet SharePoint eine Implementierung eines REST-Webdiensts, der CRUDQ-Vorgänge bei SharePoint-Listendaten über das  [OData-Protokoll](http://www.odata.org/) ausführt. Zudem verfügt nahezu jede API in den Clientobjektmodellen über einen entsprechenden REST-Endpunkt. Dadurch kann im Code mithilfe jeder Technologie, die REST-Standardfunktionen unterstützt, direkt mit SharePoint interagiert werden. Der Webdienst "svc.web" behandelt die HTTP-Anforderung und liefert eine Antwort im Atom- oder JSON-Format.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p128">For scenarios in which you need to access SharePoint entities from client technologies that do not use JavaScript and are not built on the .NET Framework or Silverlight platforms, SharePoint provides an implementation of a Representational State Transfer (REST) web service that uses the  [OData protocol](http://www.odata.org/) to perform CRUD operations on SharePoint list data. In addition, almost every API in the client object models has a corresponding REST endpoint. This enables your code to interact directly with SharePoint artifacts by using any technology that supports standard HTTP requests and responses. To use the REST capabilities that are built into SharePoint, your code constructs a RESTful HTTP request to an endpoint that corresponds to the desired client object model API. The client.svc web service handles the HTTP request and serves a response in either Atom or JSON format.</span></span>
  
    
    
<span data-ttu-id="d8e7f-249">Weitere Informationen über den REST/OData-Webdienst finden Sie unter dem Knoten  [Programmieren mit dem SharePoint REST-Dienst](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx); Beispiele dazu finden Sie im Thema  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8e7f-249">For more information about using the REST/OData web service, see the node  [Use OData query operations in SharePoint REST requests](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx); for examples, see the topic  [Complete basic operations using SharePoint REST endpoints](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx).</span></span>
  
    
    

### <a name="comparing-restodata-programming-with-client-object-model-programming"></a><span data-ttu-id="d8e7f-250">Vergleich zur REST/OData-Programmierung mit der Clientobjektmodell-Programmierung</span><span class="sxs-lookup"><span data-stu-id="d8e7f-250">Comparing REST/OData programming with client object model programming</span></span>

<span data-ttu-id="d8e7f-p129">In einigen Situationen ist die Verwendung von REST-Endpunkten möglicherweise vorzuziehen, selbst in Anwendungen, in denen ein SharePoint-Objektmodell verfügbar ist. Insbesondere für Entwickler, die über keine Erfahrung Im Entwickeln von Windows-basiertem Code haben. In der folgenden Tabelle finden Sie einen Vergleich zwischen den wichtigsten Funktionen dieser Programmierungsoptionen für einen Entwickler, der eine Anwendung auf einer Windows-Plattform oder mit einer Plattform erstellt, die JavaScript unterstützt.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p129">In some situations, it might be preferable to use the REST endpoints even in applications for which a SharePoint object model is available, especially for developers who do not have Windows development experience. The following table provides a comparison of the major features of these programming choices for a developer creating an application on a Windows platform or with a platform that supports JavaScript.</span></span>
  
    
    


|<span data-ttu-id="d8e7f-253">**Funktion**</span><span class="sxs-lookup"><span data-stu-id="d8e7f-253">**Feature**</span></span>|<span data-ttu-id="d8e7f-254">**.NET Framework oder Silverlight-Objektmodelle**</span><span class="sxs-lookup"><span data-stu-id="d8e7f-254">**.NET Framework or Silverlight object models**</span></span>|<span data-ttu-id="d8e7f-255">**JavaScript-Objektmodell**</span><span class="sxs-lookup"><span data-stu-id="d8e7f-255">**JavaScript object model**</span></span>|<span data-ttu-id="d8e7f-256">**Von einer Windows-Plattform oder von JavaScript abgerufene REST/OData-Endpunkte**</span><span class="sxs-lookup"><span data-stu-id="d8e7f-256">**REST/OData endpoints called from a Windows platform or JavaScript**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="d8e7f-257">Objektorientiertes Programmieren</span><span class="sxs-lookup"><span data-stu-id="d8e7f-257">Object-oriented programming</span></span>  <br/> |<span data-ttu-id="d8e7f-258">Ja</span><span class="sxs-lookup"><span data-stu-id="d8e7f-258">Yes</span></span>  <br/> |<span data-ttu-id="d8e7f-259">Ja</span><span class="sxs-lookup"><span data-stu-id="d8e7f-259">Yes</span></span>  <br/> |<span data-ttu-id="d8e7f-260">Nein</span><span class="sxs-lookup"><span data-stu-id="d8e7f-260">No</span></span>  <br/> |
|<span data-ttu-id="d8e7f-261">Batch-Verarbeitung</span><span class="sxs-lookup"><span data-stu-id="d8e7f-261">Batch processing</span></span>  <br/> |<span data-ttu-id="d8e7f-262">Ja</span><span class="sxs-lookup"><span data-stu-id="d8e7f-262">Yes</span></span>  <br/> |<span data-ttu-id="d8e7f-263">Ja</span><span class="sxs-lookup"><span data-stu-id="d8e7f-263">Yes</span></span>  <br/> |<span data-ttu-id="d8e7f-264">Ja</span><span class="sxs-lookup"><span data-stu-id="d8e7f-264">Yes</span></span>  <br/> |
|<span data-ttu-id="d8e7f-265">APIs für die bedingte Verarbeitung und Ausnahmebehandlungen</span><span class="sxs-lookup"><span data-stu-id="d8e7f-265">APIs for conditional processing and exception handling</span></span>  <br/> |<span data-ttu-id="d8e7f-266">Ja</span><span class="sxs-lookup"><span data-stu-id="d8e7f-266">Yes</span></span>  <br/> |<span data-ttu-id="d8e7f-267">Nein</span><span class="sxs-lookup"><span data-stu-id="d8e7f-267">No</span></span>  <br/> |<span data-ttu-id="d8e7f-268">Nein</span><span class="sxs-lookup"><span data-stu-id="d8e7f-268">No</span></span>  <br/> |
|<span data-ttu-id="d8e7f-269">Verfügbarkeit der LINQ-Syntax</span><span class="sxs-lookup"><span data-stu-id="d8e7f-269">Availability of LINQ syntax</span></span>  <br/> |<span data-ttu-id="d8e7f-270">Ja</span><span class="sxs-lookup"><span data-stu-id="d8e7f-270">Yes</span></span>  <br/> |<span data-ttu-id="d8e7f-271">Nein</span><span class="sxs-lookup"><span data-stu-id="d8e7f-271">No</span></span>  <br/> |<span data-ttu-id="d8e7f-272">Nein</span><span class="sxs-lookup"><span data-stu-id="d8e7f-272">No</span></span>  <br/> |
|<span data-ttu-id="d8e7f-273">Kombinieren von Listendaten aus verschiedenen SharePoint-Webanwendungen</span><span class="sxs-lookup"><span data-stu-id="d8e7f-273">Combining list data from different SharePoint web applications</span></span>  <br/> |<span data-ttu-id="d8e7f-274">Ja</span><span class="sxs-lookup"><span data-stu-id="d8e7f-274">Yes</span></span>  <br/> |<span data-ttu-id="d8e7f-275">Nein</span><span class="sxs-lookup"><span data-stu-id="d8e7f-275">No</span></span>  <br/> |<span data-ttu-id="d8e7f-276">Ja</span><span class="sxs-lookup"><span data-stu-id="d8e7f-276">Yes</span></span>  <br/> |
|<span data-ttu-id="d8e7f-277">Vertrautheit für erfahrene REST/OData-Entwickler</span><span class="sxs-lookup"><span data-stu-id="d8e7f-277">Familiarity to experienced REST/OData developers</span></span>  <br/> |<span data-ttu-id="d8e7f-278">Nein</span><span class="sxs-lookup"><span data-stu-id="d8e7f-278">No</span></span>  <br/> |<span data-ttu-id="d8e7f-279">Nein</span><span class="sxs-lookup"><span data-stu-id="d8e7f-279">No</span></span>  <br/> |<span data-ttu-id="d8e7f-280">Ja</span><span class="sxs-lookup"><span data-stu-id="d8e7f-280">Yes</span></span>  <br/> |
|<span data-ttu-id="d8e7f-281">Ähnlichkeiten zur nicht-Windows-Programmierung oder JavaScript-Programmierung</span><span class="sxs-lookup"><span data-stu-id="d8e7f-281">Similarity to non-Windows programming or JavaScript programming</span></span>  <br/> |<span data-ttu-id="d8e7f-282">Nein</span><span class="sxs-lookup"><span data-stu-id="d8e7f-282">No</span></span>  <br/> |<span data-ttu-id="d8e7f-283">Ja</span><span class="sxs-lookup"><span data-stu-id="d8e7f-283">Yes</span></span>  <br/> |<span data-ttu-id="d8e7f-284">Ja</span><span class="sxs-lookup"><span data-stu-id="d8e7f-284">Yes</span></span>  <br/> |
|<span data-ttu-id="d8e7f-285">Starke Typisierung für Listenelementfelder</span><span class="sxs-lookup"><span data-stu-id="d8e7f-285">Strong typing for list item fields</span></span>  <br/> |<span data-ttu-id="d8e7f-286">Nein (außer mit LINQ)</span><span class="sxs-lookup"><span data-stu-id="d8e7f-286">No (except with LINQ)</span></span>  <br/> |<span data-ttu-id="d8e7f-287">Nein</span><span class="sxs-lookup"><span data-stu-id="d8e7f-287">No</span></span>  <br/> |<span data-ttu-id="d8e7f-288">Ja, von einer Windows-Plattform          Nein, von JavaScript</span><span class="sxs-lookup"><span data-stu-id="d8e7f-288">Yes, from Windows platform          No, from JavaScript</span></span>  <br/> |
|<span data-ttu-id="d8e7f-289">Nutzen von jQuery, Knockout und anderen JavaScript-Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="d8e7f-289">Leveraging jQuery, Knockout, and other JavaScript libraries</span></span>  <br/> |<span data-ttu-id="d8e7f-290">Nein</span><span class="sxs-lookup"><span data-stu-id="d8e7f-290">No</span></span>  <br/> |<span data-ttu-id="d8e7f-291">Ja</span><span class="sxs-lookup"><span data-stu-id="d8e7f-291">Yes</span></span>  <br/> |<span data-ttu-id="d8e7f-292">Nein, von einer Windows-Plattform          Ja, von JavaScript</span><span class="sxs-lookup"><span data-stu-id="d8e7f-292">No, from Windows platform          Yes, from JavaScript</span></span>  <br/> |
   

## <a name="wcf-data-services-framework"></a><span data-ttu-id="d8e7f-293">Framework für die WCF Data Services</span><span class="sxs-lookup"><span data-stu-id="d8e7f-293">WCF Data Services Framework</span></span>
<span data-ttu-id="d8e7f-294"><a name="WCFDataServices"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e7f-294"><a name="WCFDataServices"> </a></span></span>

<span data-ttu-id="d8e7f-p130">Wenn Sie LINQ-Syntax in .NET Framework- oder Silverlight-Clientanwendungen bevorzugen, unterstützt SharePoint die  [WCF Data Services](http://msdn.microsoft.com/de-DE/library/cc668792.aspx) als LINQ-Anbieter. Sie können wie in vorherigen Versionen von SharePoint Foundation die "listdata.svc" (nur für Listendaten) vorgeben, oder die gleiche "client.svc" vorgeben, die die OData-Schnittstelle für den Zugriff auf alle SharePoint-Entitäten und Listendaten unterstützt. Weitere Informationen dazu finden Sie unter [Abfragen von SharePoint Foundation mit ADO.NET Data Services](http://msdn.microsoft.com/library/3e3e16f7-620a-4710-a3f3-19d0236f4b4a%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p130">If you prefer to use LINQ syntax in .NET Framework or Silverlight client applications, SharePoint supports  [WCF Data Services](http://msdn.microsoft.com/de-DE/library/cc668792.aspx) as a LINQ provider. You can target either the listdata.svc (for list data only) as in earlier versions of SharePoint Foundation, or you can target the same client.svc that supports the OData interface for access to all SharePoint entities in addition to list data. For more information, see [Query SharePoint Foundation with ADO.NET Data Services](http://msdn.microsoft.com/library/3e3e16f7-620a-4710-a3f3-19d0236f4b4a%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="d8e7f-p131">In Abbildung 2 ist die Beziehung zwischen den verschiedenen Client-APIs, verschiedenen Client-Anwendungstypen und SharePoint dargestellt. Die unterschiedlichen _api\*-URLs sind die farmrelativen URLs für die REST-Endpunkte. Weitere Informationen dazu finden Sie unter dem Thema  [Weitere Informationen zum SharePoint 15 REST-Dienste](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx#bk_learnmore).</span><span class="sxs-lookup"><span data-stu-id="d8e7f-p131">Figure 2 illustrates the relationship of the various client APIs, various types of client applications, and SharePoint. The various _api\* URLs are the farm-relative URLs for the REST endpoints. For more information, see the topic  [Learning more about the SharePoint 15 REST service](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx#bk_learnmore).</span></span>
  
    
    

<span data-ttu-id="d8e7f-301">**Abbildung 2. Client-Anwendungen und APIs in SharePoint**</span><span class="sxs-lookup"><span data-stu-id="d8e7f-301">**Figure 2. Client applications and APIs in SharePoint**</span></span>

  
    
    

  
    
    
![Programmiermodell für Apps für SharePoint](../images/Sp15_app_.png)
  
    
    

  
    
    

  
    
    

## <a name="deprecated-api-sets"></a><span data-ttu-id="d8e7f-303">Veraltete API-Gruppen</span><span class="sxs-lookup"><span data-stu-id="d8e7f-303">Deprecated API sets</span></span>
<span data-ttu-id="d8e7f-304"><a name="DeprecatedAPIs"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e7f-304"><a name="DeprecatedAPIs"> </a></span></span>

<span data-ttu-id="d8e7f-305">Zwei API-Gruppen werden weiterhin im SharePoint-Framework für die Abwärtskompatibilität unterstützt, es wird jedoch empfohlen, sie nicht für neue Projekte zu verwenden: die  [ASP.NET-Webdienste (asmx)](http://msdn.microsoft.com/library/c587ee90-1f88-43f3-b1a7-5f3072d038f8%28Office.15%29.aspx) und [direkte Remoteprozeduraufrufe rufen die Datei owssvr.dll](http://msdn.microsoft.com/library/4aa5c82b-90fb-4be5-b30c-d35ecae42a81%28Office.15%29.aspx) auf.</span><span class="sxs-lookup"><span data-stu-id="d8e7f-305">Two API sets are still supported in the SharePoint framework for backward compatibility, but we recommend that you not use them for new projects: the  [ASP.NET (asmx) web services](http://msdn.microsoft.com/library/c587ee90-1f88-43f3-b1a7-5f3072d038f8%28Office.15%29.aspx), and  [direct Remote Procedure Calls (RPC) calls to the owssvr.dll](http://msdn.microsoft.com/library/4aa5c82b-90fb-4be5-b30c-d35ecae42a81%28Office.15%29.aspx) file.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="d8e7f-306">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="d8e7f-306">See also</span></span>
<span data-ttu-id="d8e7f-307"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e7f-307"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="d8e7f-308">Übersicht über die SharePoint-Entwicklung</span><span class="sxs-lookup"><span data-stu-id="d8e7f-308">SharePoint development overview</span></span>](sharepoint-development-overview.md)
    
  
-  [<span data-ttu-id="d8e7f-309">Programmiermodelle in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d8e7f-309">Programming models in SharePoint</span></span>](programming-models-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d8e7f-310">SharePoint-Add-Ins im Vergleich zu SharePoint-Lösungen</span><span class="sxs-lookup"><span data-stu-id="d8e7f-310">SharePoint Add-ins compared with SharePoint solutions</span></span>](sharepoint-add-ins-compared-with-sharepoint-solutions.md)
    
  
-  [<span data-ttu-id="d8e7f-311">Programmieren mit dem SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="d8e7f-311">Use OData query operations in SharePoint REST requests</span></span>](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="d8e7f-312">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten</span><span class="sxs-lookup"><span data-stu-id="d8e7f-312">Complete basic operations using SharePoint REST endpoints</span></span>](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="d8e7f-313">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode</span><span class="sxs-lookup"><span data-stu-id="d8e7f-313">Complete basic operations using SharePoint client library code</span></span>](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="d8e7f-314">Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d8e7f-314">Complete basic operations using JavaScript library code in SharePoint</span></span>](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="d8e7f-315">Abfragen von SharePoint Foundation mit ADO.NET Data Services</span><span class="sxs-lookup"><span data-stu-id="d8e7f-315">Query SharePoint Foundation with ADO.NET Data Services</span></span>](http://msdn.microsoft.com/library/3e3e16f7-620a-4710-a3f3-19d0236f4b4a%28Office.15%29.aspx)
    
  

  
    
    
