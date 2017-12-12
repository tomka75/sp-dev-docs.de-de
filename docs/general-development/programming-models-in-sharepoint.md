---
title: Programmiermodelle in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 061985ec-6129-4e91-991b-a72488ce1d34
ms.openlocfilehash: 1c699feb8890d3d171d1c5e251c4417347f3a313
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="programming-models-in-sharepoint"></a><span data-ttu-id="58780-102">Programmiermodelle in SharePoint</span><span class="sxs-lookup"><span data-stu-id="58780-102">Programming models in SharePoint</span></span>

<span data-ttu-id="58780-p101">Sie können auf vielfältige Weise Anwendungen für die SharePoint-Plattform entwickeln. Diese Anwendungen können - je nach deren Erstellungstools, nach den verwendeten Programmierungsmodellen, nach dem Methoden der Paketerstellung und Bereitstellung, den Methoden der Vermarktung und schließlich nach den Geräten, auf denen sie ausgeführt werden - sinnvoll in folgenden Gruppen eingeteilt werden.</span><span class="sxs-lookup"><span data-stu-id="58780-p101">You can develop applications for the SharePoint platform in many ways. These applications can be usefully categorized into the following groups based on the tools used to create them, the programming models used to develop them, the methods by which they are packaged and deployed, the methods by which they are marketed, and the devices on which they run.</span></span>
  
    
    


- <span data-ttu-id="58780-105">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="58780-105">SharePoint Add-ins</span></span>
    
  
- <span data-ttu-id="58780-106">SharePoint-Veröffentlichungssites</span><span class="sxs-lookup"><span data-stu-id="58780-106">SharePoint publishing sites</span></span>
    
  
- <span data-ttu-id="58780-107">SharePoint-Farmlösungen</span><span class="sxs-lookup"><span data-stu-id="58780-107">SharePoint farm solutions</span></span>
    
  
- <span data-ttu-id="58780-108">Mobile Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="58780-108">Mobile add-ins for SharePoint</span></span>
    
  
- <span data-ttu-id="58780-109">Wiederverwendbare Komponenten für SharePoint</span><span class="sxs-lookup"><span data-stu-id="58780-109">Reusable components for SharePoint</span></span>
    
  
<span data-ttu-id="58780-p102">Diese Kategorien schließen sich gegenseitig  *nicht*  aus. Beispiel: Sie entwickeln eine Veröffentlichungssite als eine SharePoint-Add-In. In den folgenden Abschnitten werden diese Kategorien erläutert, und Sie werden jeweils durch die Dokumentation geführt.</span><span class="sxs-lookup"><span data-stu-id="58780-p102">These categories are  *not*  mutually exclusive. For example, you can develop a publishing site as an SharePoint Add-in. The following sections define these categories and guide you to the documentation for each.</span></span>
## <a name="add-ins-for-sharepoint"></a><span data-ttu-id="58780-113">Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="58780-113">Add-ins for SharePoint</span></span>
<span data-ttu-id="58780-114"><a name="Apps"> </a></span><span class="sxs-lookup"><span data-stu-id="58780-114"><a name="Apps"> </a></span></span>

<span data-ttu-id="58780-p103">Ein SharePoint-Add-In entspricht einem Add-In auf einem mobilen Gerät. Es ist eine eigenständige Produktivitätslösung, die eine Reihe von verbundenen Aufgaben ausführt, leicht zu installieren ist und sauber deinstalliert werden kann. Benutzer finden SharePoint-Add-Ins in einem öffentlichen SharePoint-Add-In Store oder im Add-In-Katalog ihres Unternehmens und können sie dort auch herunterladen. Ein SharePoint-Add-In kann die üblichen SharePoint-Komponenten beinhalten, wie Listen, benutzerdefinierte Websiteseiten, Webparts, Workflows und Inhaltstypen. Aber ein SharePoint-Add-In kann auch eine Remote-Webanwendung und Remote-Daten in SharePoint darstellen. Ein SharePoint-Add-In kann ebenfalls sowohl SharePoint- als auch Remote-Komponenten enthalten. SharePoint-Add-Ins sind sehr sichere Anwendungen, deren benutzerdefinierte Logik immer in die Cloud oder auf Clientcomputer verschoben wird. Sie werden nie auf SharePoint-Servern ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="58780-p103">A SharePoint Add-in is similar to an add-in on a mobile device. It is a stand-alone productivity solution that does a small number of related tasks, installs easily, and uninstalls cleanly. Users can discover and download SharePoint Add-ins from a public SharePoint add-in store or from their organization's corporate add-in catalog. A SharePoint Add-in can include classic SharePoint components such as lists, custom website pages, Web Parts, workflows, and content types. But an SharePoint Add-in can also surface a remote web application and remote data in SharePoint. A SharePoint Add-in can also include both SharePoint and remote components. SharePoint Add-ins are very safe applications whose custom logic is always shifted "up" to the cloud or "down" to the client computers. It never runs on the SharePoint servers.</span></span>
  
    
    
<span data-ttu-id="58780-123">Eine Einführung in Modell für SharePoint-Add-Ins finden Sie unter  [SharePoint-Add-Ins](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx).Weitere Informationen finden Sie unter  [SharePoint-Add-Ins im Vergleich zu SharePoint-Lösungen](sharepoint-add-ins-compared-with-sharepoint-solutions.md), and  [Auswählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="58780-123">For an introduction to the model for SharePoint Add-ins, see  [SharePoint Add-ins](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx). For more information, see  [SharePoint Add-ins compared with SharePoint solutions](sharepoint-add-ins-compared-with-sharepoint-solutions.md), and  [Choose the right API set in SharePoint](choose-the-right-api-set-in-sharepoint.md).</span></span>
  
    
    

## <a name="sharepoint-publishing-sites"></a><span data-ttu-id="58780-124">SharePoint-Veröffentlichungssites</span><span class="sxs-lookup"><span data-stu-id="58780-124">SharePoint publishing sites</span></span>
<span data-ttu-id="58780-125"><a name="ECM"> </a></span><span class="sxs-lookup"><span data-stu-id="58780-125"><a name="ECM"> </a></span></span>

<span data-ttu-id="58780-p104">SharePoint-Veröffentlichungssites bieten reichhaltige Inhaltsveröffentlichung mit einem hohen Maß an Wartbarkeit und Regelkonformität. Sie stellen außerdem Dokument-, Datensatz, Taxonomie- und Inhaltstypverwaltung bereit. Weitere Informationen finden Sie unter  [Erstellen von Websites für SharePoint](build-sites-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="58780-p104">SharePoint publishing sites provide large-scale content publishing with a high degree of maintainability and regulation compliance. They also provide management of documents, records, taxonomy, and content types. For more information, see  [Build sites for SharePoint](build-sites-for-sharepoint.md).</span></span>
  
    
    

## <a name="sharepoint-farm-solutions"></a><span data-ttu-id="58780-129">SharePoint-Farmlösungen</span><span class="sxs-lookup"><span data-stu-id="58780-129">SharePoint farm solutions</span></span>
<span data-ttu-id="58780-130"><a name="Solutions"> </a></span><span class="sxs-lookup"><span data-stu-id="58780-130"><a name="Solutions"> </a></span></span>

<span data-ttu-id="58780-p105">SharePoint Farmlösungen sind vertrauenswürdige SharePoint-Erweiterungen, deren benutzerdefinierte Logik das SharePoint-Serverobjektmodell mit vollem Vertrauen in die SharePoint-Server aufruft und ausführt. Diese Lösungen dienen in erster Linie benutzerdefinierten administrativen SharePoint-Erweiterungen, wie Zeitgeberaufträge, benutzerdefinierte Windows PowerShell-Befehle und Erweiterungen der Zentraladministration. Farmlösungen werden als SharePoint-Lösungspakete bereitgestellt, die Farmadministratoren an einen farmübergreifende Speicherort laden und von dort aus bereitstellen. Komponenten in Farmlösungen können in der Farm, in der Webanwendung, in der Websitesammlung oder auf der Website gelten. Weitere Informationen finden Sie unter  [Erstellen von Farmlösungen in SharePoint](build-farm-solutions-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="58780-p105">SharePoint farm solutions are trusted SharePoint extensions whose custom logic calls the SharePoint server object model and runs with full trust on the SharePoint servers. These solutions are primarily for custom administrative extensions of SharePoint, such as timer jobs, custom Windows PowerShell commands, and extensions of Central Administration. Farm solutions are distributed as SharePoint solution packages that farm administrators upload to a farm-wide storage location from which they can be deployed. Components in farm solutions can have farm, web application, site collection, or website scope. For more information, see  [Build farm solutions in SharePoint](build-farm-solutions-in-sharepoint.md).</span></span>
  
    
    

## <a name="mobile-add-ins-for-sharepoint"></a><span data-ttu-id="58780-136">Mobile Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="58780-136">Mobile add-ins for SharePoint</span></span>
<span data-ttu-id="58780-137"><a name="Mobile"> </a></span><span class="sxs-lookup"><span data-stu-id="58780-137"><a name="Mobile"> </a></span></span>

<span data-ttu-id="58780-p106">Windows Phone-Apps und Apps, die auf mobilen Nicht-Microsoft-Plattformen basieren, können auf SharePoint-Websites und -Daten zugreifen. Tools zum Erstellen von Windows Phone-Apps, die mit SharePoint interagieren, sind für eine Installation unter Visual Studio 2010 (und Visual Studio 2012) verfügbar. Eine clientverwaltete SharePoint-API für eine Verwendung auf Windows Phone-Geräten ist erhältlich. Mobile Geräte, einschließlich Nicht-Microsoft-Geräte, können ebenfalls über REST/OData-Endpunkte auf SharePoint-Daten zugreifen. Weitere Informationen finden Sie unter  [Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen](build-windows-phone-apps-that-access-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="58780-p106">Windows Phone apps, and apps built on non-Microsoft mobile platforms, can access SharePoint websites and data. Tools for building Windows Phone apps that interact with SharePoint are available for installation on Visual Studio 2010 and Visual Studio 2012. A SharePoint client managed API just for use on Windows Phone devices is available. Mobile devices, including non-Microsoft devices, can also access SharePoint data through SharePoint REST/OData endpoints. For more information, see  [Build Windows Phone apps that access SharePoint](build-windows-phone-apps-that-access-sharepoint.md).</span></span>
  
    
    

## <a name="reusable-components-for-sharepoint"></a><span data-ttu-id="58780-143">Wiederverwendbare Komponenten für SharePoint</span><span class="sxs-lookup"><span data-stu-id="58780-143">Reusable components for SharePoint</span></span>
<span data-ttu-id="58780-144"><a name="Reuse"> </a></span><span class="sxs-lookup"><span data-stu-id="58780-144"><a name="Reuse"> </a></span></span>

<span data-ttu-id="58780-p107">Die SharePoint-Plattform und Visual Studio 2012 ermöglichen eine Kapselung und Wiederverwendung von Anwendungselementen, auch derjenigen Elemente, die mit Code, Skripten und XML-Markup erstellt wurden. Weitere Informationen finden Sie unter  [Erstellen von wiederverwendbaren Komponenten für SharePoint](build-reusable-components-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="58780-p107">The SharePoint platform and Visual Studio 2012 enable encapsulation and reuse of application elements, including elements created with code, script, and XML markup. For more information, see  [Build reusable components for SharePoint](build-reusable-components-for-sharepoint.md).</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="58780-147">Inhalt dieses Abschnitts</span><span class="sxs-lookup"><span data-stu-id="58780-147">In this section</span></span>
<span data-ttu-id="58780-148"><a name="Reuse"> </a></span><span class="sxs-lookup"><span data-stu-id="58780-148"><a name="Reuse"> </a></span></span>


-  [<span data-ttu-id="58780-149">Erstellen von Websites für SharePoint</span><span class="sxs-lookup"><span data-stu-id="58780-149">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="58780-150">Erstellen von Farmlösungen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="58780-150">Build farm solutions in SharePoint</span></span>](build-farm-solutions-in-sharepoint.md)
    
  
-  [<span data-ttu-id="58780-151">Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen</span><span class="sxs-lookup"><span data-stu-id="58780-151">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="58780-152">Erstellen von wiederverwendbaren Komponenten für SharePoint</span><span class="sxs-lookup"><span data-stu-id="58780-152">Build reusable components for SharePoint</span></span>](build-reusable-components-for-sharepoint.md)
    
  

## <a name="see-also"></a><span data-ttu-id="58780-153">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="58780-153">See also</span></span>
<span data-ttu-id="58780-154"><a name="SP15devinSP_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="58780-154"><a name="SP15devinSP_addlresources"> </a></span></span>


-  [<span data-ttu-id="58780-155">Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint</span><span class="sxs-lookup"><span data-stu-id="58780-155">Set up a general development environment for SharePoint</span></span>](set-up-a-general-development-environment-for-sharepoint.md)
    
  
-  [<span data-ttu-id="58780-156">Hinzufügen von SharePoint-Funktionen</span><span class="sxs-lookup"><span data-stu-id="58780-156">Add SharePoint capabilities</span></span>](add-sharepoint-capabilities.md)
    
  
-  [<span data-ttu-id="58780-157">Barrierefreiheit in SharePoint</span><span class="sxs-lookup"><span data-stu-id="58780-157">Accessibility in SharePoint</span></span>](accessibility-in-sharepoint.md)
    
  
