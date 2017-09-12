---
title: VSS-Anforderer und SharePoint
ms.prod: SHAREPOINT
ms.assetid: 0b2e5a4e-40f0-4ccf-a21a-7274921f2169
ms.openlocfilehash: 39286286f913fc2674892fb0db585ebe401c2a9c
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2017
---
# <a name="vss-requestors-and-sharepoint"></a><span data-ttu-id="ce626-102">VSS-Anforderer und SharePoint</span><span class="sxs-lookup"><span data-stu-id="ce626-102">VSS requestors and SharePoint</span></span>
 <span data-ttu-id="ce626-p101">**Zusammenfassung:** Informieren Sie sich über die Funktionsweise des Requestors-Systems des Systems Gruppenrichtlinien-Verwaltungskonsole (Volume Shadow Copy Service, VSS) mit Microsoft SharePoint. VSS in Windows Server kann verwendet werden, um Anwendungen erstellen, die sichern und Wiederherstellen von Microsoft SharePoint Foundation. Der VSS stellt eine Infrastruktur, die Speicherlösung-Management-Programme, Business-Programme und Hardwareanbietern zusammenzuarbeiten erstellen und Verwalten von Schattenkopien können. Für diese Infrastruktur-basierte Lösungen können die Schatten Kopien (oder gespiegelte Kopien) zum Sichern und Wiederherstellen von Datenbanken für eine oder mehrere- SharePoint Foundation .</span><span class="sxs-lookup"><span data-stu-id="ce626-p101">**Summary:** Learn about how the requestor system of the Volume Shadow Copy Service (VSS) system works with Microsoft SharePoint. VSS in Windows Server can be used to create applications that back up and restore Microsoft SharePoint Foundation. The VSS provides an infrastructure that enables third-party storage management programs, business programs, and hardware providers to cooperate in creating and managing shadow copies. Solutions based on this infrastructure can use the shadow copies (or mirrored copies) to back up and restore one or more SharePoint Foundation databases.</span></span>
  
    
    


## <a name="vss-requestor-system"></a><span data-ttu-id="ce626-107">VSS-Requestors system</span><span class="sxs-lookup"><span data-stu-id="ce626-107">VSS requestor system</span></span>

<span data-ttu-id="ce626-p102">Der VSS koordiniert die Kommunikation zwischen den Requestors (backup-Anwendungen), Autoren (Windows-Anwendungen wie SharePoint Foundation und Microsoft SQL Server) und Anbieter (System, Software oder Hardware Komponenten, die die Schattenkopien erstellen). Zum Sichern von SharePoint Foundationmithilfe des VSS-Features, muss das Sicherungsprogramm ein Volumenschattenkopie-Anforderers enthalten, das SharePoint Foundationkennt. Da das Sicherungsprogramm, das mit Windows Server bereitgestellt ist keine solche Requestors verfügt, müssen Organisationen Sicherung Anwendungen von Drittanbietern verwenden.</span><span class="sxs-lookup"><span data-stu-id="ce626-p102">The VSS coordinates communication among requestors (backup applications), Writers (Windows applications such as SharePoint Foundation and Microsoft SQL Server), and Providers (system, software, or hardware components that create the shadow copies). To use the VSS feature to back up SharePoint Foundation, the backup program must include a VSS requestor that is aware of SharePoint Foundation. Because the backup program that is provided with Windows Server has no such requestor, organizations must use third-party backup applications.</span></span>
  
    
    
<span data-ttu-id="ce626-p103">Im Hinblick auf die Kompatibilität mit SharePoint Foundation müssen bei auf VSS basierenden Sicherungsanwendungen zwei Basisvoraussetzungen erfüllt sein, damit die Integrität und Wiederherstellbarkeit von Schattenkopiesicherungen sichergestellt ist. Kunden sollten sich von ihren Sicherungsanbietern bestätigen lassen, dass die Sicherungsanwendung die in diesem Thema genannten Kompatibilitätsanforderungen für SharePoint Foundation erfüllt.</span><span class="sxs-lookup"><span data-stu-id="ce626-p103">To be compliant with SharePoint Foundation, backup applications that are based on VSS must follow two basic requirements to ensure the integrity and recoverability of shadow copy backups. Customers should verify with their backup vendors that the backup application fulfills the compliance requirements for SharePoint Foundation listed in this topic.</span></span>
  
    
    
<span data-ttu-id="ce626-113">Die folgenden SharePoint Foundation-Anforderungen gelten für eine auf Schattenkopien basierende Sicherungsanwendung, um die Integrität und Wiederherstellbarkeit von SharePoint Foundation-Datenbanken sicherzustellen:</span><span class="sxs-lookup"><span data-stu-id="ce626-113">Following are the SharePoint Foundation requirements that a shadow copy backup application must follow to ensure the integrity and recoverability of SharePoint Foundation databases:</span></span> 
  
    
    

- <span data-ttu-id="ce626-114">SharePoint Foundation-Datenbanken und Suchindexdateien dürfen ausschließlich über SPF-VSS Writer gesichert werden.</span><span class="sxs-lookup"><span data-stu-id="ce626-114">SharePoint Foundation databases and search index files must be backed up exclusively through the SPF-VSS Writer.</span></span>
    
  
- <span data-ttu-id="ce626-p104">Die Integrität des Schattenkopie-Sicherungssatzes muss von der Sicherungsanwendung überprüft werden. Wiederherstellungsvorgänge am ursprünglichen Speicherort dürfen ausschließlich mit SPF-VSS Writer ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="ce626-p104">The backup application must validate the integrity of the shadow copy backup set. Restore operations to original location must be done exclusively with the SPF-VSS Writer.</span></span>
    
  

## <a name="restoring"></a><span data-ttu-id="ce626-117">Wiederherstellen</span><span class="sxs-lookup"><span data-stu-id="ce626-117">Restoring</span></span>

<span data-ttu-id="ce626-118">Für die Ausführung einer Wiederherstellung müssen die folgenden Bedingungen erfüllt sein:</span><span class="sxs-lookup"><span data-stu-id="ce626-118">Before executing a restoration, the following conditions must be met:</span></span>
  
    
    

- <span data-ttu-id="ce626-119">Die folgenden Dienste müssen  *gestartet*  sein:</span><span class="sxs-lookup"><span data-stu-id="ce626-119">The following services must be  *started*  :</span></span>
    
  - <span data-ttu-id="ce626-120">SharePoint VSS Writer</span><span class="sxs-lookup"><span data-stu-id="ce626-120">SharePoint VSS Writer</span></span>
    
  
  - <span data-ttu-id="ce626-121">Volumeschattenkopie</span><span class="sxs-lookup"><span data-stu-id="ce626-121">Volume Shadow Copy</span></span>
    
  
  - <span data-ttu-id="ce626-122">SharePoint-Ablaufverfolgung</span><span class="sxs-lookup"><span data-stu-id="ce626-122">SharePoint Tracing</span></span>
    
  
- <span data-ttu-id="ce626-123">Die folgenden Dienste müssen  *beendet*  sein:</span><span class="sxs-lookup"><span data-stu-id="ce626-123">The following services must be  *stopped*  :</span></span>
    
  - <span data-ttu-id="ce626-124">SharePoint-Verwaltung</span><span class="sxs-lookup"><span data-stu-id="ce626-124">SharePoint Administration</span></span>
    
  
  - <span data-ttu-id="ce626-125">SharePoint-Suche</span><span class="sxs-lookup"><span data-stu-id="ce626-125">SharePoint Search</span></span>
    
  
  - <span data-ttu-id="ce626-126">SharePoint-Timer</span><span class="sxs-lookup"><span data-stu-id="ce626-126">SharePoint Timer</span></span>
    
  
  - <span data-ttu-id="ce626-127">SharePoint Server-Suche (wenn SharePoint Server installiert ist)</span><span class="sxs-lookup"><span data-stu-id="ce626-127">SharePoint Server Search (If SharePoint Server is installed.)</span></span>
    
  
- <span data-ttu-id="ce626-128">Wenn die gesamte Farm wiederhergestellt wird, müssen SharePoint Foundation und die Internetinformationsdienste (Internet Information Services, IIS) heruntergefahren werden.</span><span class="sxs-lookup"><span data-stu-id="ce626-128">If the whole farm is being restored, SharePoint Foundation *and Internet Information Server (IIS)*  must be shutdown.</span></span>
    
  
- <span data-ttu-id="ce626-129">Wenn nur ausgewählte Webanwendungen oder andere Komponenten wiederhergestellt werden, müssen die Webanwendungen heruntergefahren werden, und die Komponenten können während der Wiederherstellung nicht verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="ce626-129">If only selected Web applications or other components are being restored, the Web applications must be shutdown and the components may not be in use during the restoration.</span></span>
    
  

## <a name="next-steps"></a><span data-ttu-id="ce626-130">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="ce626-130">Next steps</span></span>
<span data-ttu-id="ce626-131"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="ce626-131"></span></span>

<span data-ttu-id="ce626-132">Erfahren Sie, wie erstellen und Verwenden eines VSS-Requestors für SharePoint:</span><span class="sxs-lookup"><span data-stu-id="ce626-132">Learn how to create and use a VSS requestor for SharePoint:</span></span>
  
    
    

-  [<span data-ttu-id="ce626-133">Vorgehensweise: Erstellen ein Volumenschattenkopie-Anforderers für die Verwendung mit SharePoint</span><span class="sxs-lookup"><span data-stu-id="ce626-133">How to: Create a VSS requestor for use with SharePoint</span></span>](how-to-create-a-vss-requestor-for-use-with-sharepoint)
    
  
-  [<span data-ttu-id="ce626-134">Vorgehensweise: Sichern und Wiederherstellen von SharePoint verwenden eines VSS-Requestors</span><span class="sxs-lookup"><span data-stu-id="ce626-134">How to: Back up and restore SharePoint using a VSS requestor</span></span>](how-to-back-up-and-restore-sharepoint-using-a-vss-requestor)
    
  
-  [<span data-ttu-id="ce626-135">Vorgehensweise: Sichern und Wiederherstellen eine Suchdienstanwendung in SharePoint mit VSS</span><span class="sxs-lookup"><span data-stu-id="ce626-135">How to: Back up and restore a search service application in SharePoint using VSS</span></span>](how-to-back-up-and-restore-a-search-service-application-in-sharepoint-using)
    
  

## <a name="additional-resources"></a><span data-ttu-id="ce626-136">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="ce626-136">Additional resources</span></span>
<span data-ttu-id="ce626-137"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ce626-137"></span></span>


-  [<span data-ttu-id="ce626-138">Übersicht über SharePoint und der Volumeschattenkopie-Dienst</span><span class="sxs-lookup"><span data-stu-id="ce626-138">Overview of SharePoint and the Volume Shadow Copy Service</span></span>](overview-of-sharepoint-and-the-volume-shadow-copy-service)
    
  
-  [<span data-ttu-id="ce626-139">Vorgehensweise: Erstellen ein Volumenschattenkopie-Anforderers für die Verwendung mit SharePoint</span><span class="sxs-lookup"><span data-stu-id="ce626-139">How to: Create a VSS requestor for use with SharePoint</span></span>](how-to-create-a-vss-requestor-for-use-with-sharepoint)
    
  
-  [<span data-ttu-id="ce626-140">Vorgehensweise: Sichern und Wiederherstellen von SharePoint verwenden eines VSS-Requestors</span><span class="sxs-lookup"><span data-stu-id="ce626-140">How to: Back up and restore SharePoint using a VSS requestor</span></span>](how-to-back-up-and-restore-sharepoint-using-a-vss-requestor)
    
  
-  [<span data-ttu-id="ce626-141">Vorgehensweise: Sichern und Wiederherstellen eine Suchdienstanwendung in SharePoint mit VSS</span><span class="sxs-lookup"><span data-stu-id="ce626-141">How to: Back up and restore a search service application in SharePoint using VSS</span></span>](how-to-back-up-and-restore-a-search-service-application-in-sharepoint-using)
    
  

