---
title: "SharePoint-Zugriff von mobilen und systemeigenen Geräte-Apps"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 42014171-5ee5-421d-9cde-413efc3aecef
ms.openlocfilehash: 5376b4f3f0b629669d6965d7d37c63e12eded769
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="access-sharepoint-from-mobile-and-native-device-apps"></a><span data-ttu-id="7315d-102">SharePoint-Zugriff von mobilen und systemeigenen Geräte-Apps</span><span class="sxs-lookup"><span data-stu-id="7315d-102">Access SharePoint from mobile and native device apps</span></span>
<span data-ttu-id="7315d-p101">Erfahren Sie, wie SharePoint von mobilen apps und andere apps systemeigene Gerät und von Anwendungen für externe Webdienste zugreifen. SharePoint-Add-Ins, Farmlösungen und "codeloser" Sandkastenlösungen werden alle Ausführen von in SharePoint, aber apps auf anderen Plattformen können auch SharePoint-Client-APIs zugreifen.</span><span class="sxs-lookup"><span data-stu-id="7315d-p101">Learn how to access SharePoint from mobile apps and other native device apps, and from external web applications. SharePoint Add-ins, farm solutions, and "no code" sandboxed solutions are all run from within SharePoint, but apps on other platforms can also access SharePoint client APIs.</span></span>
  
    
    


> [!IMPORTANT]
> <span data-ttu-id="7315d-105">Für Tests und Debugging auf einer beliebigen Plattform benötigen Sie ein **Entwicklerkonto auf Office 365**.</span><span class="sxs-lookup"><span data-stu-id="7315d-105">To test and debug on any platform, you need a **developer account on Office 365**.</span></span> <span data-ttu-id="7315d-106">Weitere Informationen dazu finden Sie unter: [Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins in Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx) oder [Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement](http://msdn.microsoft.com/library/2ec857d5-dc6f-4cf6-ba45-adc845ef2a25%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="7315d-106">Important To test and debug on any platform, you need a developer account on Office 365. More info: [Set up a development environment for SharePoint Add-ins on Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx) or [Create a developer site on an existing Office 365 subscription](http://msdn.microsoft.com/library/2ec857d5-dc6f-4cf6-ba45-adc845ef2a25%28Office.15%29.aspx).</span></span> 
  
    
    


## <a name="non-microsoft-mobile-and-native-device-apps"></a><span data-ttu-id="7315d-107">Nicht von Microsoft stammende mobile Apps und systemeigene Geräte-Apps</span><span class="sxs-lookup"><span data-stu-id="7315d-107">Non-Microsoft mobile and native device apps</span></span>

<span data-ttu-id="7315d-108">Gerät nicht-Microsoft-apps, einschließlich mobiler apps, **SharePoint REST/OData-APIs für CRUD-Vorgänge zu SharePoint-Daten verwenden**.</span><span class="sxs-lookup"><span data-stu-id="7315d-108">Non-Microsoft device apps, including mobile apps, **use SharePoint REST/OData APIs for CRUD operations on SharePoint data**.</span></span>
  
    
    

- <span data-ttu-id="7315d-109">See  [Erste Schritte mit den SharePoint REST-Dienst](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx) for the basics.</span><span class="sxs-lookup"><span data-stu-id="7315d-109">See  [Get to know the SharePoint REST service](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx) for the basics.</span></span>
    
  
- <span data-ttu-id="7315d-110">See  [REST-API-Referenz für SharePoint](http://msdn.microsoft.com/library/3514e753-19f9-4b41-a1ae-f35c5ffc17d2%28Office.15%29.aspx) for a complete reference.</span><span class="sxs-lookup"><span data-stu-id="7315d-110">See  [REST API reference for SharePoint](http://msdn.microsoft.com/library/3514e753-19f9-4b41-a1ae-f35c5ffc17d2%28Office.15%29.aspx) for a complete reference.</span></span>
    
  
<span data-ttu-id="7315d-111">For more information about how to create mobile apps for any platform, see  [Erstellen von mobilen Apps für andere Plattformen mit SharePoint](build-mobile-apps-for-other-platforms-using-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="7315d-111">For more information about how to create mobile apps for any platform, see  [Build mobile apps for other platforms using SharePoint](build-mobile-apps-for-other-platforms-using-sharepoint.md).</span></span>
  
    
    

## <a name="windows-phone-apps-that-access-sharepoint"></a><span data-ttu-id="7315d-112">Windows Phone-apps, die auf SharePoint zugreifen</span><span class="sxs-lookup"><span data-stu-id="7315d-112">Windows Phone apps that access SharePoint</span></span>
<span data-ttu-id="7315d-113"><a name="WinPhone"> </a></span><span class="sxs-lookup"><span data-stu-id="7315d-113"></span></span>

<span data-ttu-id="7315d-114">Windows Phone-apps können eine der folgenden verwenden:</span><span class="sxs-lookup"><span data-stu-id="7315d-114">Windows Phone apps can use one of the following:</span></span>
  
    
    

- <span data-ttu-id="7315d-115">Die .NET SharePoint-Objekt mithilfe der clientseitigen Objektmodell (CSOM) Version speziell für Windows Phone-Geräten.</span><span class="sxs-lookup"><span data-stu-id="7315d-115">The .NET SharePoint client-side object model (CSOM) version specifically for Windows Phone devices.</span></span>
    
  
- <span data-ttu-id="7315d-116">Der SharePoint REST/OData-APIs.</span><span class="sxs-lookup"><span data-stu-id="7315d-116">The SharePoint REST/OData APIs.</span></span>
    
  
 <span data-ttu-id="7315d-117">Diese mobilen apps können der Unterstützung von SharePoint für die Microsoft-pushbenachrichtigungsdienst und einen neuen Geolocation-Feldtyp nutzen.</span><span class="sxs-lookup"><span data-stu-id="7315d-117">These mobile apps can take advantage of the support in SharePoint for the Microsoft Push Notification service and a new geolocation field type.</span></span>
  
    
    
<span data-ttu-id="7315d-118">For more about creating Windows Phone apps that access SharePoint, see  [Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen](build-windows-phone-apps-that-access-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="7315d-118">For more about creating Windows Phone apps that access SharePoint, see  [Build Windows Phone apps that access SharePoint](build-windows-phone-apps-that-access-sharepoint.md).</span></span>
  
    
    

## <a name="web-applications-that-dont-start-from-sharepoint"></a><span data-ttu-id="7315d-119">Webanwendungen, die nicht aus SharePoint beginnen</span><span class="sxs-lookup"><span data-stu-id="7315d-119">Web applications that don't start from SharePoint</span></span>
<span data-ttu-id="7315d-120"><a name="WinPhone"> </a></span><span class="sxs-lookup"><span data-stu-id="7315d-120"></span></span>

<span data-ttu-id="7315d-121">Webanwendungen, die nicht aus SharePoint beginnen sind nicht unbedingt "SharePoint-Add-Ins ", obwohl sie manchmal als SharePoint-Add-Ins im MSDN und andere Dokumentationen gezählt werden. Diese apps enthalten zwischen anderen, Schriftarten, die von der Office 365 app Launcher und Office-Add-Ins ausgeführt werden, sowie alle Webanwendungen, die direkt in einem Browser ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="7315d-121">Web applications that don't start from SharePoint are not strictly "SharePoint Add-ins," although they're sometimes counted as SharePoint Add-ins in MSDN and other docs. These apps include, among others, ones that run from the Office 365 app launcher and Office Add-ins, as well as any web applications that are run directly from a browser.</span></span>
  
    
    
<span data-ttu-id="7315d-p103">Sie können diese apps auf die Plattform ASP.NET oder einen nicht-Microsoft-Stapel erstellen. Wenn Sie Ihre Webanwendung auf einem nicht-Microsoft-Stapel erstellen, werden CRUD-Vorgänge mit der REST/OData-APIs nur als app nicht von Microsoft stammenden Gerät. Bei der Erstellung auf ASP.NET es **dem SharePoint-Clientobjektmodell oder REST/OData-APIs verwenden können**.</span><span class="sxs-lookup"><span data-stu-id="7315d-p103">You can build these apps on the ASP.NET platform or a non-Microsoft stack. If you build your web application on a non-Microsoft stack, it does CRUD operations with the REST/OData APIs, just as a non-Microsoft device app. If you build it on ASP.NET it **can use the SharePoint CSOM or the REST/OData APIs**.</span></span>
  
    
    
<span data-ttu-id="7315d-p104">These apps **gain authorized access to SharePoint data by using access tokens** that are issued by the Azure Control Service (ACS) in compliance with the OAuth Authentication Code flow. For more, see [OAuth-Ablauf mit Authentifizierungscode für SharePoint-Add-Ins](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="7315d-p104">These apps **gain authorized access to SharePoint data by using access tokens** that are issued by the Azure Control Service (ACS) in compliance with the OAuth Authentication Code flow. For more, see [Authorization Code OAuth flow for SharePoint Add-ins](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).</span></span>
  
    
    

