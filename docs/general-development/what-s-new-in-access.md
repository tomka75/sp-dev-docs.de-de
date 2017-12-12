---
title: Neuigkeiten in Access
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 625bc1d0-55db-4420-a02e-aee04028b215
ms.openlocfilehash: 2e04315f9700759198cf93ba0014f0821889ea4a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="whats-new-in-access"></a><span data-ttu-id="4b22c-102">Neuigkeiten in Access</span><span class="sxs-lookup"><span data-stu-id="4b22c-102">What's new in Access</span></span>
<span data-ttu-id="4b22c-103">Hier finden Sie Informationen zu den Features in Access 2013, welche die Erstellung, Bereitstellung und Verwaltung von webbasierten Anwendungen für die Zusammenarbeit lokal oder in der Cloud erleichtern.</span><span class="sxs-lookup"><span data-stu-id="4b22c-103">Learn about the features in Access 2013 makes it easy to create, deploy, and manage collaborative web-based applications on premise or in the cloud.</span></span>
## <a name="introduction"></a><span data-ttu-id="4b22c-104">Einführung</span><span class="sxs-lookup"><span data-stu-id="4b22c-104">Introduction</span></span>
<span data-ttu-id="4b22c-105"><a name="SP15_access15overview_Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="4b22c-105"><a name="SP15_access15overview_Introduction"> </a></span></span>

<span data-ttu-id="4b22c-p101">Access 2013 verfügt über ein neues Anwendungsmodell, das für den Zweck entworfen wurde, die Webentwicklung ähnlich wie frühere Versionen von Access mit der Windows-Bereitstellung zu vereinfachen. Access 2013 ermöglicht Experten das schnelle Erstellen einer Anwendung, die zum Leiten ihres Unternehmens verwendet werden kann. Durch die Verwendung von Microsoft SharePoint zum Hosten des Front-Ends der App und von Microsoft SQL Server 2012 als die entsprechende Datenspeichertechnologie, verbessert Access 2013 die Verwaltbarkeit und Skalierbarkeit von Access-Anwendungen erheblich. Durch die Kompatibilität mit Office 365 und SQL Azure wird die Reichweite von Access-Anwendungen maßgeblich erweitert.</span><span class="sxs-lookup"><span data-stu-id="4b22c-p101">Access 2013 features a new application model that is designed for one purpose―to simplify web development much like earlier versions of Access with Windows development. Access 2013 enables subject matter experts to quickly create an application that can be used to run their business. By using Microsoft SharePoint to host the front end of the app and Microsoft SQL Server 2012 as its data storage technology, Access 2013 significantly improves the manageability and scalability of Access applications. Compatibility with Office 365 and SQL Azure significantly expand the reach of Access applications.</span></span>
  
    
    

## <a name="architecture"></a><span data-ttu-id="4b22c-110">Architektur</span><span class="sxs-lookup"><span data-stu-id="4b22c-110">Architecture</span></span>
<span data-ttu-id="4b22c-111"><a name="SP15_access15overview_Architecture"> </a></span><span class="sxs-lookup"><span data-stu-id="4b22c-111"><a name="SP15_access15overview_Architecture"> </a></span></span>

<span data-ttu-id="4b22c-p102">In einer lokalen Umgebung werden Access 2013-Apps durch SharePoint gehostet, während die Daten in SQL Server 2012 gespeichert werden. SharePoint stellt Authentifizierung, Autorisierung und Sicherheit für Access 2013-Apps bereit. Die Back-End-Tabellen, -Ansichten, -Makros und -Abfragen werden in einer SQL Server 2012-Datenbank gespeichert.</span><span class="sxs-lookup"><span data-stu-id="4b22c-p102">In an on-premise environment, Access 2013 apps are hosted by SharePoint while the data is stored in SQL Server 2012. SharePoint provides authentication, authorization, and security for Access 2013 apps. The back-end tables, views, macros, and queries are stored in an SQL Server 2012 database.</span></span>
  
    
    
<span data-ttu-id="4b22c-115">Access 2013 bietet über die Dienste Office 365 und SQL Azure eine Methode zur Bereitstellung einer Access-App in der Cloud.</span><span class="sxs-lookup"><span data-stu-id="4b22c-115">Access 2013, through the Office 365 and SQL Azure services, provides a method to deploy an Access app to the cloud.</span></span>
  
    
    
<span data-ttu-id="4b22c-116">In Abbildung 1 wird eine Übersicht der Access 2013-Architektur dargestellt.</span><span class="sxs-lookup"><span data-stu-id="4b22c-116">Figure 1 provides an overview of Access 2013 architecture.</span></span>
  
    
    

<span data-ttu-id="4b22c-117">**Abbildung 1. Access 2013-Architektur**</span><span class="sxs-lookup"><span data-stu-id="4b22c-117">**Figure 1. Access 2013 architecture**</span></span>

  
    
    

  
    
    
![Architektur von Access 2013](../images/odc_Office15_Access15OverviewDK2_Figure07.jpg)
  
    
    
<span data-ttu-id="4b22c-119">Beim Erstellen einer neuen Access-Anwendung erstellt Access Services in SharePoint eine neue Anwendungsdatenbank, die die in der Anwendung enthaltenen Daten, Ansichten, Abfragen und Makros speichert.</span><span class="sxs-lookup"><span data-stu-id="4b22c-119">When a new Access application is created, Access Services in SharePoint creates a new Application database that stores the data, view, queries and macros contained in the app.</span></span> <span data-ttu-id="4b22c-120">Die Access Services 2013 System-Datenbank kann so konfiguriert werden, dass neue Anwendungsdatenbanken auf einem separaten Server SQL Server 2012-Server erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="4b22c-120">The Access Services 2013 System database can be configured to create new Application databases on a separate SQL Server 2012 server.</span></span>
  
    
    
<span data-ttu-id="4b22c-p104">Die Verwendung von SQL Server 2012 zum Speichern von Daten bietet eine zuvor in Access-Anwendungen nicht gekannte Verwaltbarkeit und Skalierbarkeit. Nun sind die Tage Geschichte, in denen eine Access-Anwendung neu entwickelt und in einer leistungsstärkeren Umgebung erneut implementiert werden müsste.</span><span class="sxs-lookup"><span data-stu-id="4b22c-p104">Using SQL Server 2012 to store data provides manageability and scalability previously unknown to Access applications. Gone are the days when an Access application would have to be redesigned and reimplemented in a more powerful environment.</span></span>
  
    
    
<span data-ttu-id="4b22c-p105">Eine Access 2013-App ist in dem Moment online, in dem sie entwickelt wird. Sie können die App für andere Benutzer freigeben, im privaten Unternehmenskatalog oder im Office Store bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="4b22c-p105">An Access 2013 app is online the moment it's created. You can decide to share the app with other people, deploy to the private corporate catalog, or deploy to the Office Store.</span></span>
  
    
    

## <a name="developing-access-apps"></a><span data-ttu-id="4b22c-125">Entwickeln von Access-Apps</span><span class="sxs-lookup"><span data-stu-id="4b22c-125">Developing Access apps</span></span>
<span data-ttu-id="4b22c-126"><a name="SP15_access15overview_DevelopingAccessapps"> </a></span><span class="sxs-lookup"><span data-stu-id="4b22c-126"><a name="SP15_access15overview_DevelopingAccessapps"> </a></span></span>

<span data-ttu-id="4b22c-127">Im Gegensatz zu vielen der SharePoint-Anwendungsdienste macht Access Services 2013 keine API verfügbar, die Sie zum Entwickeln von Access-Apps in Visual Studio verwenden können.</span><span class="sxs-lookup"><span data-stu-id="4b22c-127">Unlike many of the SharePointapplication services, Access Services 2013 doesn't expose an API that you can use to develop Access apps in Visual Studio.</span></span> <span data-ttu-id="4b22c-128">Access 2013 ist die Umgebung, die Sie zum Entwickeln von Access 2013-Apps verwenden.</span><span class="sxs-lookup"><span data-stu-id="4b22c-128">Access 2013 is the environment that you use to develop Access 2013 apps.</span></span>
  
    
    
<span data-ttu-id="4b22c-129">Weitere Informationen zur Entwicklung von Access 2013-Apps finden Sie unter [Gewusst wie: Erstellen und Anpassen einer Web-App in Access](http://msdn.microsoft.com/library/628745f4-82e9-4838-9726-6f3e506a654f%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="4b22c-129">For more information about how to develop Access 2013 apps, see  [How to: Create and customize a web app in Access](http://msdn.microsoft.com/library/628745f4-82e9-4838-9726-6f3e506a654f%28Office.15%29.aspx)</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="4b22c-130">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="4b22c-130">See also</span></span>
<span data-ttu-id="4b22c-131"><a name="SP15_access15overview_addres"> </a></span><span class="sxs-lookup"><span data-stu-id="4b22c-131"><a name="SP15_access15overview_addres"> </a></span></span>


-  [<span data-ttu-id="4b22c-132">Neuigkeiten in Access für Entwickler</span><span class="sxs-lookup"><span data-stu-id="4b22c-132">New in Access for developers</span></span>](http://msdn.microsoft.com/library/df778f51-d65e-4c30-b618-65003ceb39b3%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="4b22c-133">Benutzerdefinierte Web-App-Referenz für Access</span><span class="sxs-lookup"><span data-stu-id="4b22c-133">Access custom web app reference</span></span>](http://msdn.microsoft.com/library/8d696fa4-a6f2-4fb1-8662-a313bf0b5989%28Office.15%29.aspx)
    
  

