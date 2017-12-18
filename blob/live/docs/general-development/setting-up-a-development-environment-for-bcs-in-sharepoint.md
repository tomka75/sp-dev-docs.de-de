---
title: "Einrichten einer Entwicklungsumgebung für BCS in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d83c8a43-49dd-47eb-94d4-23aa2cf71a9a
ms.openlocfilehash: 33956da39dedd23fa5f81ce131d84e22eca9d60f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="setting-up-a-development-environment-for-bcs-in-sharepoint"></a><span data-ttu-id="f0511-102">Einrichten einer Entwicklungsumgebung für BCS in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f0511-102">Setting up a development environment for BCS in SharePoint</span></span>
<span data-ttu-id="f0511-p101">Informationen Sie zum Einrichten einer Entwicklungsumgebung für die Entwicklung von Lösungen SharePoint und SharePoint-Add-Ins mit Business Connectivity Services (BCS). Sie können die SharePoint Lösungen und SharePoint-Add-Ins erstellen, mithilfe von BCS auf einem Clientcomputer oder auf einem Servercomputer, abhängig von der Art der Lösung, die Sie erstellen.</span><span class="sxs-lookup"><span data-stu-id="f0511-p101">Learn about setting up a development environment for developing SharePoint solutions and SharePoint Add-ins using Business Connectivity Services (BCS). You can create SharePoint solutions and SharePoint Add-ins by using BCS on a client computer or on a server computer, depending on the type of solution you are building.</span></span>
  
    
    


## <a name="building-server-based-solutions-and-sharepoint-add-ins"></a><span data-ttu-id="f0511-105">Erstellen von Server-basierte Lösungen und SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f0511-105">Building server-based solutions and SharePoint Add-ins</span></span>
<span data-ttu-id="f0511-106"><a name="SP15SettingupdevenvBCS_server"> </a></span><span class="sxs-lookup"><span data-stu-id="f0511-106"><a name="SP15SettingupdevenvBCS_server"> </a></span></span>

<span data-ttu-id="f0511-p102">In der Regel wird die Mehrheit der BCS Lösungen und apps in einer Server-Umgebung gehostet werden. Diese Lösungen für Server und apps bieten die größte Maß an Flexibilität mit allen Features von BCS in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f0511-p102">Typically, the majority of BCS solutions and apps will be hosted in a server environment. These server solutions and apps provide the greatest amount of flexibility with all of the features of BCS in SharePoint.</span></span>
  
    
    
<span data-ttu-id="f0511-p103">Für Server-basierte Lösungen empfiehlt es sich in der Regel die Lösung auf einem lokalen Computer zu entwickeln, auf dem SharePoint installiert ist, und dann, wenn die Lösung wird erstellt und getestet, Bereitstellen auf den Produktionsserver. Sie können eine Entwicklungsumgebung installieren, auf einer Host-Arbeitsstation oder auf einen oder mehrere virtuelle Computer, auf dem Windows Server 2008 Service Pack 2 ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="f0511-p103">For server-based solutions, it is usually best to develop the solution on a local computer where SharePoint is installed and then, when the solution is built and tested, deploy it to the production server. You can install a development environment on either a host workstation or on one or more virtual computers that are running Windows Server 2008 Service Pack 2.</span></span>
  
    
    

### <a name="setting-up-an-environment-to-build-sharepoint-add-ins"></a><span data-ttu-id="f0511-111">Einrichten einer Umgebung SharePoint-Add-Ins erstellen</span><span class="sxs-lookup"><span data-stu-id="f0511-111">Setting up an environment to build SharePoint Add-ins</span></span>

<span data-ttu-id="f0511-112">Die Umgebung, die Sie verwenden, für die Entwicklung von apps mit BCS ist die gleichen wie für eine beliebige SharePoint-Add-In entwickeln.</span><span class="sxs-lookup"><span data-stu-id="f0511-112">The environment that you use for developing apps with BCS is the same as for developing any SharePoint Add-in.</span></span> 
  
    
    
<span data-ttu-id="f0511-113">Weitere Informationen zum Installieren der Komponenten von einer Entwicklungsumgebung, einschließlich Betriebssystem, SharePoint, Visual Studio 2012 und Office Developer Tools für Visual Studio 2012, befolgen Sie die Anweisungen in  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="f0511-113">To learn how to install the components of a development environment, including the operating system, SharePoint, Visual Studio 2012, and Office Developer Tools for Visual Studio 2012, follow the instructions in  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

## <a name="building-client-based-solutions"></a><span data-ttu-id="f0511-114">Erstellen von Client-basierte Lösungen</span><span class="sxs-lookup"><span data-stu-id="f0511-114">Building client-based solutions</span></span>
<span data-ttu-id="f0511-115"><a name="SP15SettingupdevenvBCS_client"> </a></span><span class="sxs-lookup"><span data-stu-id="f0511-115"><a name="SP15SettingupdevenvBCS_client"> </a></span></span>

<span data-ttu-id="f0511-p104">Client-basierter Lösungen aktivieren Office 2013-Clientanwendungen auf die gleichen externen Daten zugreifen, die eine SharePoint Lösung oder SharePoint-Add-In kann. Hierzu können Sie Code mithilfe von BCS-Clientcache implementieren. Die Clientkomponenten kommunizieren mit BCS über den clientseitigen Code und Clientcache. Dadurch wird die Office-Clientanwendungen mit den umfangreichen Daten, die über externe Inhaltstypen in SharePoint verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="f0511-p104">Client-based solutions enable Office 2013 client applications to access the same external data that a SharePoint solution or SharePoint Add-in can. You can do this by implementing code using the BCS Client Cache. The client components communicate with BCS through client-side code and the client cache. This provides Office client applications with the rich data that is available to SharePoint through external content types.</span></span>
  
    
    
<span data-ttu-id="f0511-120">Da diese Lösungen Code nicht erforderlich ist, können Sie SharePoint Designer 2013 und Office 2013 verwenden.</span><span class="sxs-lookup"><span data-stu-id="f0511-120">Because these solutions don't require code, you can use SharePoint Designer 2013 and Office 2013.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="f0511-121">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="f0511-121">See also</span></span>
<span data-ttu-id="f0511-122"><a name="SP15SettingupdevenvBCS_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f0511-122"><a name="SP15SettingupdevenvBCS_addresources"> </a></span></span>


-  [<span data-ttu-id="f0511-123">Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f0511-123">Set up an on-premises development environment for SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="f0511-124">Erste Schritte mit den Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f0511-124">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f0511-125">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f0511-125">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f0511-126">Übersicht über die SharePoint-Entwicklung</span><span class="sxs-lookup"><span data-stu-id="f0511-126">SharePoint development overview</span></span>](sharepoint-development-overview.md)
    
  

