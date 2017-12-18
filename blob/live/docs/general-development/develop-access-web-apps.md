---
title: Entwickeln von Access-Web-Apps
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 41131b27-d750-4d11-b3c7-c17ad4d666e2
ms.openlocfilehash: 39a559d2ca5cfe223d6ef84956e2af6604d23c0a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="develop-access-web-apps"></a><span data-ttu-id="99a33-102">Entwickeln von Access-Web-Apps</span><span class="sxs-lookup"><span data-stu-id="99a33-102">Develop Access web apps</span></span>
<span data-ttu-id="99a33-103">Erfahren Sie, wie Sie mit Microsoft Access 2013 auf einfache Weise lokal oder in der Cloud webbasierte Zusammenarbeitsanwendungen erstellen, bereitstellen und verwalten.</span><span class="sxs-lookup"><span data-stu-id="99a33-103">Learn how Microsoft Access 2013 makes it easy to create, deploy, and manage collaborative web-based applications on premise or in the cloud.</span></span>
## <a name="introduction"></a><span data-ttu-id="99a33-104">Einführung</span><span class="sxs-lookup"><span data-stu-id="99a33-104">Introduction</span></span>
<span data-ttu-id="99a33-105"><a name="dk2_DevelopingAccess15WebApps_Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="99a33-105"><a name="dk2_DevelopingAccess15WebApps_Introduction"> </a></span></span>

<span data-ttu-id="99a33-p101">Microsoft Access 2013 ist darauf ausgelegt, die Webentwicklung auf die gleiche Weise zu erleichtern, wie es dies in früheren Zeiten der Windows-Entwicklung getan hat. Access 2013 ermöglicht Experten, schnell eine Anwendung zur Geschäftsausführung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="99a33-p101">Microsoft Access 2013 is designed to simplify web development in the same manner that it did in previous eras of Windows development. Access 2013 is designed to enable subject matter experts to quickly create an application that can be used to run their business.</span></span>
  
    
    

  
    
    

## <a name="whats-new-in-access-2013"></a><span data-ttu-id="99a33-108">Neuerungen in Access 2013</span><span class="sxs-lookup"><span data-stu-id="99a33-108">What's new in Access 2013</span></span>
<span data-ttu-id="99a33-109"><a name="dk2_DevelopingAccess15WebApps_whatsNewInAccess15"> </a></span><span class="sxs-lookup"><span data-stu-id="99a33-109"><a name="dk2_DevelopingAccess15WebApps_whatsNewInAccess15"> </a></span></span>

<span data-ttu-id="99a33-p102">Access 2013 bietet ein neues Anwendungsmodell, mit dem Benutzer datenorientierte Webanwendungen erstellen können. Benutzer mit wenig oder keiner Programmiererfahrung müssen häufig schnell eine Anwendung erstellen, welche ihre Geschäftsanforderungen erfüllt, und sie mit ihren Kollegen, Bekannten oder Verwandten teilen. Access 2013 bietet Benutzern eine interaktive Methode, mit der die Anwendung schnell zum Einsatz gebracht werden kann, indem Tabellen und Formulare erstellt werden, die auf den ausgewählten Kriterien basieren.</span><span class="sxs-lookup"><span data-stu-id="99a33-p102">Access 2013 features a new application model that is designed to allow users to create data-centric web applications. Users with little or no programming experience often need to quickly build an application that addresses their business needs and share it with their colleagues, friends, or family. Access 2013 offers users an interactive method that can be used to get up and running quickly with by creating tables and forms that are based on the selected criteria.</span></span>
  
    
    
<span data-ttu-id="99a33-p103">Access 2013 verwendet Microsoft SharePoint zum Hosten des Front-Ends Ihrer Anwendung und SQL Server zur Datenspeicherung. Access 2013 stellt über die Office 365- und SQL Azure-Dienste eine Methode zur Bereitstellung einer Access-Anwendung im Internet bereit. Zum Teilen einer Access 2013-App muss nur die URL der App an die gewünschten Benutzer gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="99a33-p103">Access 2013 uses Microsoft SharePoint to host the front end of your application while it is using SQL Server for data storage. Access 2013, through the Office 365 and SQL Azure services, provides a method to deploy an Access application to the Internet. Sharing an Access 2013 app is as easy as sending the URL of the app to the intended users.</span></span>
  
    
    
<span data-ttu-id="99a33-116">Weitere Informationen zu den Neuerungen in Access 2013-Apps finden Sie unter  [Neuerungen in Access](what-s-new-in-access.md)</span><span class="sxs-lookup"><span data-stu-id="99a33-116">For more information about what's new in Access 2013 apps, see  [What's new in Access](what-s-new-in-access.md)</span></span>
  
    
    

## <a name="creating-an-access-2013-application"></a><span data-ttu-id="99a33-117">Erstellen einer Access 2013-Anwendung</span><span class="sxs-lookup"><span data-stu-id="99a33-117">Creating an Access 2013 application</span></span>
<span data-ttu-id="99a33-118"><a name="dk2_DevelopingAccess15WebApps_CreatingAnAccess15App"> </a></span><span class="sxs-lookup"><span data-stu-id="99a33-118"><a name="dk2_DevelopingAccess15WebApps_CreatingAnAccess15App"> </a></span></span>

<span data-ttu-id="99a33-119">Im Gegensatz zu vielen der SharePoint-Anwendungsdienste macht Access Services 2013 keine API verfügbar, die Sie zum Entwickeln von Access-Apps in Visual Studio verwenden können.</span><span class="sxs-lookup"><span data-stu-id="99a33-119">Unlike many of the SharePointapplication services, Access Services 2013 doesn't expose an API that you can use to develop Access apps in Visual Studio.</span></span> <span data-ttu-id="99a33-120">Access 2013 ist die Umgebung, die Sie zum Entwickeln von Access 2013-Apps verwenden.</span><span class="sxs-lookup"><span data-stu-id="99a33-120">Access 2013 is the environment that you use to develop Access 2013 apps.</span></span>
  
    
    
<span data-ttu-id="99a33-121">Weitere Informationen zur Entwicklung von Access 2013-Apps finden Sie unter [Gewusst wie: Erstellen und Anpassen einer Web-App in Access](http://msdn.microsoft.com/library/628745f4-82e9-4838-9726-6f3e506a654f%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="99a33-121">For more information about how to develop Access 2013 apps, see  [How to: Create and customize a web app in Access](http://msdn.microsoft.com/library/628745f4-82e9-4838-9726-6f3e506a654f%28Office.15%29.aspx)</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="99a33-122">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="99a33-122">See also</span></span>
<span data-ttu-id="99a33-123"><a name="dk2_DevelopingAccess15WebApps_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="99a33-123"><a name="dk2_DevelopingAccess15WebApps_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="99a33-124">Neuerungen in Access</span><span class="sxs-lookup"><span data-stu-id="99a33-124">What's new in Access</span></span>](what-s-new-in-access.md)
    
  
-  [<span data-ttu-id="99a33-125">Gewusst wie: Erstellen und Anpassen einer Web-App in Access</span><span class="sxs-lookup"><span data-stu-id="99a33-125">How to: Create and customize a web app in Access</span></span>](http://msdn.microsoft.com/library/628745f4-82e9-4838-9726-6f3e506a654f%28Office.15%29.aspx)
    
  

