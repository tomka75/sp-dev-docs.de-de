---
title: "Erstellen von Farmlösungen in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 96c32f08-ad93-49af-b8d0-9d194a48cc79
ms.openlocfilehash: 8cc5fbc9d9b26d0048cd0e42e611ff9707847079
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="build-farm-solutions-in-sharepoint"></a><span data-ttu-id="7d76c-102">Erstellen von Farmlösungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="7d76c-102">Build farm solutions in SharePoint</span></span>
<span data-ttu-id="7d76c-103">Übersicht über unsere Dokumentation und die Entwicklung, Verpackung und Bereitstellung von administrativen Erweiterungen für SharePoint mit Farmlösungen.</span><span class="sxs-lookup"><span data-stu-id="7d76c-103">Get an overview of our documentation about developing, packaging, and deploying administrative extensions to SharePoint using farm solutions.</span></span>
## <a name="what-are-farm-solutions"></a><span data-ttu-id="7d76c-104">Was sind Farmlösungen?</span><span class="sxs-lookup"><span data-stu-id="7d76c-104">What are farm solutions?</span></span>
<span data-ttu-id="7d76c-105"><a name="WhatAreFarmSolutions"> </a></span><span class="sxs-lookup"><span data-stu-id="7d76c-105"><a name="WhatAreFarmSolutions"> </a></span></span>

<span data-ttu-id="7d76c-p101">SharePoint verfügt über ein eigenes System für die Installation von Erweiterungen für administrative SharePoint-Funktionen, das sich von anderen Windows-Anwendungen und -Plattformen unterscheidet. Es ist keine MSI-Datei und ClickOnce-Technologie implementiert. Die Assemblys, XML- und andere Dateien in die Erweiterung werden stattdessen in einer einzelnen Datei gebündelt, die Lösungspaket genannt wird. Ein Lösungspaket verfügt über ein CAB-basiertes Format mit einer WSP-Dateierweiterung. Das Paket kann SharePoint-Features und deren untergeordnete Komponenten sowie bestimmte Arten von Komponenten beinhalten, die nicht in Features bereitgestellt werden. Farmadministratoren laden die Pakete an einem farmübergreifenden Speicherort hoch, von wo sie bereitgestellt und die zugehörigen Features aktiviert werden können.</span><span class="sxs-lookup"><span data-stu-id="7d76c-p101">SharePoint has its own system for installing extensions to SharePoint administrative functions that is different from other Windows applications and platforms. No MSI file or ClickOnce technology is involved. Instead, the assemblies, XML, and other files in the extension are bundled into a single file, which is called a solution package. A solution package has a .cab-based format but a .wsp file extension. The package can contain SharePoint Features and all their child components in addition to certain kinds of components that are not deployed in Features. Farm administrators upload the packages to a farm-wide storage location from where they can be deployed and their Features activated.</span></span>
  
    
    
<span data-ttu-id="7d76c-p102">Im Gegensatz zu SharePoint-Add-Ins enthalten Farmlösungen Code, der auf SharePoint-Servern bereitgestellt wird und Aufrufe des SharePoint-Serverobjektmodells ausführen kann. Diese Assemblys werden immer mit voller Vertrauenswürdigkeit ausgeführt. Der Bereich der Features in Farmlösungen kann, neben des Websitebereichs der Features in SharePoint-Add-Ins, die Websitesammlung, Webanwendung oder die gesamte Farm umfassen. Aufgrund dieser Aspekte der Farmlösungen sind Farmadministratoren nur dann zur Installation von diesen bereit, wenn sie von einer bekannten und vertrauenswürdigen Quelle stammen. Aus diesem Grund sollten SharePoint-Erweiterungen, die in erster Linie für die Verwendung durch Endbenutzer entwickelt werden, als SharePoint-Add-Ins, und nicht Farmlösungen, entwickelt werden. Farmlösungen sollten für Anpassungen von SharePoint-Verwaltungsfunktionen wie benutzerdefinierte Zeitgeberaufträge, benutzerdefinierte Windows PowerShell-Cmdlets und Erweiterungen der Zentralverwaltung verwendet werden. Weitere Informationen über die Vorteile der SharePoint-Add-Ins und die Verwendung von Farmlösungen finden Sie unter  [SharePoint-Add-Ins im Vergleich zu SharePoint-Lösungen](sharepoint-add-ins-compared-with-sharepoint-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="7d76c-p102">Unlike SharePoint Add-ins, farm solutions contain code that is deployed to the SharePoint servers and makes calls to the SharePoint server object model. These assemblies always run with full trust. Moreover, the Features in farm solutions can have scope as wide as the site collection, web application, or whole farm, in addition to the website scope of Features in SharePoint Add-ins. These aspects of farm solutions sometimes make farm administrators reluctant to install them, unless they come from a well-known and trusted source. For this reason, SharePoint extensions that are primarily for use by end users should be developed as SharePoint Add-ins, not farm solutions. Farm solutions should be used for customizations of SharePoint administrative functions, such as custom timer jobs, custom Windows PowerShell cmdlets, and extensions of Central Administration. For more on the advantages of SharePoint Add-ins and the uses of farm solutions, see  [SharePoint Add-ins compared with SharePoint solutions](sharepoint-add-ins-compared-with-sharepoint-solutions.md).</span></span>
  
    
    

## <a name="guide-to-the-developer-documentation-for-farm-solutions"></a><span data-ttu-id="7d76c-118">Leitfaden für die Dokumentation für Entwickler von Farmlösungen</span><span class="sxs-lookup"><span data-stu-id="7d76c-118">Guide to the developer documentation for farm solutions</span></span>
<span data-ttu-id="7d76c-119"><a name="Guide"> </a></span><span class="sxs-lookup"><span data-stu-id="7d76c-119"><a name="Guide"> </a></span></span>

<span data-ttu-id="7d76c-p103">Die Entwicklung von Farmlösungen hat sich seit SharePoint 2010geändert. Deshalb sind in diesem Abschnitt Links zum SharePoint 2010 SDK enthalten. Um Verwirrung zu vermeiden, beachten Sie die folgenden Punkte bei der Verwendung des SharePoint 2010 SDK für die Entwicklung für SharePoint:</span><span class="sxs-lookup"><span data-stu-id="7d76c-p103">Development of farm solutions has changed very little since SharePoint 2010, so this section contains links to the SharePoint 2010 SDK. To avoid confusion, keep the following points in mind at all times when using the SharePoint 2010 SDK to develop against SharePoint:</span></span>
  
    
    

- <span data-ttu-id="7d76c-p104">Im SharePoint 2010 SDK wird häufig auf „Sandkastenlösungen" verwiesen. Sandkastenlösungen mit benutzerdefiniertem Code sind in SharePoint veraltet. Sandkastenlösungen „ohne Code" werden weiterhin verwendet.</span><span class="sxs-lookup"><span data-stu-id="7d76c-p104">You will see many references to "sandboxed solutions" in the SharePoint 2010 SDK. Sandboxed solutions with custom code are deprecated in SharePoint. "no code" sandboxed solutions are still viable.</span></span>
    
  
- <span data-ttu-id="7d76c-p105">Unsere Empfehlung, Farmlösungenin erster Linie für administrative Erweiterungen zu verwenden, gilt nicht in SharePoint 2010. Aus diesem Grund beziehen sich möglicherweise viele Beispiele und andere Dokumentationen im SharePoint 2010 SDK auf Endbenutzer-Erweiterungen, die als Farmlösungen bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="7d76c-p105">Our recommendation that farm solutions be used primarily for administrative extensions did not apply in SharePoint 2010. Therefore, many of the samples and other documentation in the SharePoint 2010 SDK may be about end-user extensions that are deployed as farm solutions.</span></span>
    
  
- <span data-ttu-id="7d76c-p106">Die Begriffe „serverseitig" oder „Servercode" im SharePoint 2010 SDK beziehen sich auf den Code, der das SharePoint-Serverobjektmodell aufruft. Diese Begriffe beziehen sich  *nicht*  auf den Code, der auf Remote-Webservern ausgeführt wird (d. h. Webservern außerhalb der SharePoint-Farm). Der Code, der SharePoint von Remote-Webservern aufruft, verwendet sowohl in SharePoint 2010 als auch in SharePoint, immer eins der SharePoint- *Client*  objektmodelle. Im SharePoint 2010 SDK, wird diese Art von Code „clientseitiger" Code oder „Clientcode" genannt.</span><span class="sxs-lookup"><span data-stu-id="7d76c-p106">The terms "server-side" or "server code" in the SharePoint 2010 SDK refer to code that calls the SharePoint server object model. These terms do  *not*  refer to code that runs on remote web servers (that is, web servers external to the SharePoint farm). Code that calls SharePoint from remote web servers, in both SharePoint 2010 and SharePoint, always uses one of the SharePoint *client*  object models. In the SharePoint 2010 SDK, such code would be called "client-side" or "client code."</span></span>
    
  
- <span data-ttu-id="7d76c-p107">Die Assemblys in einer Farmlösung in SharePoint 2010 können mit CAS-Richtlinien (Custom Access Security, CAS) bereitgestellt werden. Solche Richtlinien werden in SharePoint ignoriert; alle Assemblys in Farmlösungen in SharePoint werden mit voller Vertrauenswürdigkeit ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="7d76c-p107">The assemblies in a farm solution in SharePoint 2010 could be deployed with Custom Access Security (CAS) policies. Such policies are ignored in SharePoint; all assemblies in farm solutions in SharePoint run with full trust.</span></span>
    
  

### <a name="packaging-and-deployment"></a><span data-ttu-id="7d76c-133">Verpackung und Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="7d76c-133">Packaging and deployment</span></span>

<span data-ttu-id="7d76c-p108">Die Grundlagen der Verpackung, Installation, Aktualisierung und Lokalisierung in Farmlösungen werden unter  [Übersicht über Lösungen](http://msdn.microsoft.com/library/1983cab9-4b29-494a-a62a-0f8e83908744%28Office.15%29.aspx) und [Farmlösungen](http://msdn.microsoft.com/library/845f7524-b9ff-412b-aa29-3afacda91100%28Office.15%29.aspx) erläutert. Die Entwicklung bestimmter SharePoint-Komponenten für die Integration in einer Farmlösung wird in den entsprechenden Artikeln zum SharePoint 2010 SDK beschrieben. Die meisten Komponenten in einer Farmlösung sollten in einem oder mehreren benutzerdefinierten SharePoint-Features eingeschlossen werden. Informationen zum Entwerfen und Erstellen von Features finden Sie unter [Verwenden von Features](http://msdn.microsoft.com/library/ce5f5ce5-1429-439e-9261-2c4ba9788cc1%28Office.15%29.aspx) im SharePoint 2010 SDK.</span><span class="sxs-lookup"><span data-stu-id="7d76c-p108">The basics of packaging, installing, updating, and localizing farm solutions are explained in  [Solutions Overview](http://msdn.microsoft.com/library/1983cab9-4b29-494a-a62a-0f8e83908744%28Office.15%29.aspx) and the node [Farm Solutions in SharePoint 2010](http://msdn.microsoft.com/library/845f7524-b9ff-412b-aa29-3afacda91100%28Office.15%29.aspx). Development of particular SharePoint components for inclusion in a farm solution is explained in the relevant nodes of SharePoint 2010 SDK. Most of the components in a farm solution should be encapsulated in one or more custom SharePoint Features. For information about designing and creating Features, see the  [Working with Features](http://msdn.microsoft.com/library/ce5f5ce5-1429-439e-9261-2c4ba9788cc1%28Office.15%29.aspx) node of the SharePoint 2010 SDK.</span></span>
  
    
    

### <a name="administrative-extensions"></a><span data-ttu-id="7d76c-138">Administrative Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="7d76c-138">Administrative extensions</span></span>

<span data-ttu-id="7d76c-p109">Eine Anleitung zum Erweitern der Verwaltungsfunktionen in einer SharePoint-Farm finden Sie unter  [SharePoint Foundation-Administration](http://msdn.microsoft.com/library/cdcc1b8a-4144-446f-b471-03d4a754a8ab%28Office.15%29.aspx) im SharePoint 2010 SDK. Dort sind Erläuterungen zur Erweiterung der Zentraladministration, Erstellen von benutzerdefinierten Windows PowerShell-Cmdlets, Anpassen von Upgrades und Migration, Anpassung von Backups und Anpassen der SharePoint-Ereignisprotokollierung enthalten. In einem Abschnitt wird die Anpassung der SharePoint-Farmintegrität und des Leistungsmesssystems erläutert. Anweisungen zum Erstellen eines benutzerdefinierten Zeitgeberauftrags finden Sie unter [Gewusst wie: Ausführen von Code auf allen Webservern](http://msdn.microsoft.com/library/1bbb11b4-a342-4bed-9e7a-b8b13edd0ccc%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d76c-p109">Guidance about extending the administrative functions in a SharePoint farm is in the  [Windows SharePoint Services Administration](http://msdn.microsoft.com/library/cdcc1b8a-4144-446f-b471-03d4a754a8ab%28Office.15%29.aspx) node of the SharePoint 2010 SDK. There you can find explanations about extending Central Administration, creating custom Windows PowerShell cmdlets, customizing upgrades and migration, customizing backups, and customizing SharePoint event logging. One section explains how to customize the SharePoint farm health and performance measuring system. For instructions about creating a custom timer job, see [How to: Run Code on All Web Servers](http://msdn.microsoft.com/library/1bbb11b4-a342-4bed-9e7a-b8b13edd0ccc%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="7d76c-143">Inhalt dieses Abschnitts</span><span class="sxs-lookup"><span data-stu-id="7d76c-143">In this section</span></span>
<span data-ttu-id="7d76c-144"><a name="Guide"> </a></span><span class="sxs-lookup"><span data-stu-id="7d76c-144"><a name="Guide"> </a></span></span>

<span data-ttu-id="7d76c-145">Die Themen in diesem Abschnitt beschreiben die  *Änderungen*  bei der Entwicklung von SharePoint-Lösungen.</span><span class="sxs-lookup"><span data-stu-id="7d76c-145">The topics in this section describe the ways in which development of SharePoint solutions  *has*  changed.</span></span>
  
    
    

-  [<span data-ttu-id="7d76c-146">Vorgehensweise: Anpassen eines Feldtyps mithilfe vom clientseitigem Rendering</span><span class="sxs-lookup"><span data-stu-id="7d76c-146">How to: Customize a field type using client-side rendering</span></span>](how-to-customize-a-field-type-using-client-side-rendering.md)
    
  
-  [<span data-ttu-id="7d76c-147">URLs und Token in SharePoint</span><span class="sxs-lookup"><span data-stu-id="7d76c-147">URLs and tokens in SharePoint</span></span>](urls-and-tokens-in-sharepoint.md)
    
  
-  [<span data-ttu-id="7d76c-148">Virtuelle Verzeichnisse in SharePoint-Lösungen</span><span class="sxs-lookup"><span data-stu-id="7d76c-148">Virtual directories in SharePoint solutions</span></span>](virtual-directories-in-sharepoint-solutions.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="7d76c-149">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="7d76c-149">Additional resources</span></span>
<span data-ttu-id="7d76c-150"><a name="SP15buildfarm_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="7d76c-150"><a name="SP15buildfarm_addlresources"> </a></span></span>


-  [<span data-ttu-id="7d76c-151">Programmiermodelle in SharePoint</span><span class="sxs-lookup"><span data-stu-id="7d76c-151">Programming models in SharePoint</span></span>](programming-models-in-sharepoint.md)
    
  

