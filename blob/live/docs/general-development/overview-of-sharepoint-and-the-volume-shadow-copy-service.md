---
title: "Übersicht über SharePoint und den Volumeschattenkopie-Dienst"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d1cb6653-bfc0-4af2-b221-d7d30cb40d84
ms.openlocfilehash: 16ba81e41273df0243063aeae3d80030b718fa61
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="overview-of-sharepoint-and-the-volume-shadow-copy-service"></a><span data-ttu-id="c5f78-102">Übersicht über SharePoint und den Volumeschattenkopie-Dienst</span><span class="sxs-lookup"><span data-stu-id="c5f78-102">Overview of SharePoint and the Volume Shadow Copy Service</span></span>
 <span data-ttu-id="c5f78-p101">**Zusammenfassung:** Lernen Sie die Microsoft SharePoint -Schnittstelle zu Volume Shadow Copy Service (VSS). Für Sicherungsanbieter wird durch den Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) das Sichern von Microsoft-Serverlösungen mit einer zentralisierten API vereinfacht. Microsoft SharePoint Foundation enthält einen referenziellen VSS Writer (nachfolgend "SPF-VSS Writer" genannt), der in das Windows VSS-Sicherungsframework integriert ist. Dadurch wird das Sichern und Wiederherstellen von SharePoint Foundation-Daten durch Sicherungsanwendungen ermöglicht. Es wird ein Überschreibungsszenario mit schwerwiegenden Folgen für die gesamte Farm (einschließlich Suchindex) unterstützt. Bei der Wiederherstellung werden Datenbanken eingebunden und Websitezuordnungen synchronisiert.</span><span class="sxs-lookup"><span data-stu-id="c5f78-p101">**Summary:** Learn about the Microsoft SharePoint interface to the Volume Shadow Copy Service (VSS). For backup vendors, the Volume Shadow Copy Service (VSS) simplifies backing up Microsoft server solutions by using a centralized API. Microsoft SharePoint Foundation includes a referential VSS writer (hereafter, called "the SPF-VSS Writer") that integrates with the Windows VSS backup framework, enabling backup applications to back up and restore SharePoint Foundation data. It supports a catastrophic overwrite scenario for the entire farm (search index included). On recovery, it hooks up databases and synchronizes site mappings.</span></span>
  
    
    


## <a name="design-of-the-system"></a><span data-ttu-id="c5f78-108">Entwurf des Systems</span><span class="sxs-lookup"><span data-stu-id="c5f78-108">Design of the System</span></span>

<span data-ttu-id="c5f78-109">Die folgende Abbildung zeigt die Hauptkomponenten des Systems: Microsoft Windows Server (und Volume Shadow Copy Service), SharePoint Foundation (und SPF-VSS-Writer für die Windows Server-Volume Shadow Copy Service) und Anwendung von Drittanbietern (oder benutzerdefinierte) Backup und Wiederherstellung (einschließlich der Anforderer und Anbieter).</span><span class="sxs-lookup"><span data-stu-id="c5f78-109">The following figure shows the main components in the system: Microsoft Windows Server (and the Volume Shadow Copy Service), SharePoint Foundation (and the SPF-VSS Writer for the Windows Server Volume Shadow Copy Service), and the third-party (or custom) backup/restore application (including the requestor and the provider).</span></span>
  
    
    

  
    
    
![Beziehungen zwischen SharePoint und VSS](../images/77a290e8-e4aa-4c54-b1ec-3d74bf3962b6.gif)
  
    
    
<span data-ttu-id="c5f78-p102">Der VSS kommuniziert mit dem Windows Server-Dateisystem und der Massenspeicher-Gerätetreiber über einen Anbieter von Drittanbietern (oder benutzerdefinierte). Der Hardwareanbieter muss ermitteln, in dem die Schattenkopie erstellt wird. Der VSS abstrahiert die hardwarespezifischen Schattenkopie damit Sicherungs-bzw. Wiederherstellungsvorgang die Schattenkopie einheitlich zugreifen kann, ohne zu wissen, die Implementierungsdetails der Hardware.</span><span class="sxs-lookup"><span data-stu-id="c5f78-p102">The VSS communicates with the Windows Server file system and with the mass storage device driver through a third-party (or custom) provider. The hardware provider must determine where the shadow copy is created. The VSS abstracts the hardware-specific shadow copy so the backup/restore application can access the shadow copy in a uniform manner without knowing the hardware implementation details.</span></span> 
  
    
    
<span data-ttu-id="c5f78-p103">SharePoint Foundation Speicher ist eine Komponente des SharePoint Foundation und greift auf SharePoint Foundation Speichergruppen über das Dateisystem von Windows Server. Innerhalb des Dateisystems enthält jede Speichergruppe SharePoint Foundation Konfiguration, Inhalt, Suche Datenbanken und Datenbanken von Drittanbietern in die Konfiguration Datenbank und Indexdateien registriert. Ebenfalls enthalten sind Dienste auf den SharePoint Foundation Service Application Framework aufgebaut.</span><span class="sxs-lookup"><span data-stu-id="c5f78-p103">The SharePoint Foundation store is a component of SharePoint Foundation and accesses SharePoint Foundation storage groups through the Windows Server file system. Within the file system, each SharePoint Foundation storage group includes configuration, content, Search databases, and any third-party databases registered in the configuration database and search index files. Also included are any services built on the SharePoint Foundation Service Application Framework.</span></span> 
  
    
    
<span data-ttu-id="c5f78-p104">Zur Unterstützung des VSS enthält SharePoint Foundation den SPF-VSS Writer. Der SPF-VSS Writer wird mit dem SharePoint Foundation-Speicher (der im Auftrag des Anforderers betrieben wird) koordiniert, um die Speichergruppe zu sperren und deren Bereitstellung aufzuheben, bevor sie gesichert wird. Nach Abschluss der Sicherung wird dann die Sperrung der Speichergruppe aufgehoben und die Speichergruppe bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="c5f78-p104">To support the VSS, SharePoint Foundation includes the SPF-VSS Writer. The SPF-VSS Writer coordinates with the SharePoint Foundation store (operating on behalf of the requestor) to freeze and dismount the storage group before backing it up, and then to unfreeze and mount the storage group after the backup is complete.</span></span>
  
    
    
<span data-ttu-id="c5f78-119">Während einer Wiederherstellung wird der SPF-VSS Writer von der Sicherungs-/Wiederherstellungsanwendung in Koordinierung mit dem SharePoint Foundation-Speicher (der im Auftrag des Anforderers betrieben wird) angewiesen, die Bereitstellung der Speichergruppe aufzuheben, die Datenbankdateien zu ersetzen und die Speichergruppe wieder bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="c5f78-119">During a recovery, the backup/restore application instructs the SPF-VSS Writer to coordinate with the SharePoint Foundation store (operating on behalf of the requestor) to dismount the storage group, replace the database files, and mount the storage group.</span></span>
  
> [!NOTE]
> <span data-ttu-id="c5f78-120">Wichtige Informationen zur Wiederherstellung finden Sie im Abschnitt „Wiederherstellen“ im Artikel [VSS-Anforderer und SharePoint](vss-requestors-and-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="c5f78-120">[Note:](vss-requestors-and-sharepoint.md) See "Restoring" in  VSS requestors and SharePoint for important information about restorations.</span></span>
  
    
    

<span data-ttu-id="c5f78-p105">Als Anforderer wird eine Anwendung eines Drittanbieters (oder benutzerdefinierte Anwendung) bezeichnet, die den VSS zum ordnungsgemäßen Sichern und Wiederherstellen von SharePoint Foundation-Daten verwendet. Der Anforderer kommunizierte mit dem VSS, um Informationen zu SharePoint Foundation anzufordern, die Erstellung von Schattenkopien zu veranlassen und Zugriff auf die Daten für die Sicherung zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="c5f78-p105">A requestor is a third-party (or custom) application designed to use the VSS to properly back up and restore SharePoint Foundation data. The requestor communicates with the VSS to obtain information about SharePoint Foundation, command the creation of shadow copies, and gain access to the data for backup.</span></span> 
  
    
    
<span data-ttu-id="c5f78-p106">Beim Wiederherstellen, kommuniziert des Anforderers auch mit den VSS So bereiten Sie die Wiederherstellung des Systems und zum Einfügen die Daten zurück auf das Massenspeichergerät. Die Sicherungs-bzw. Wiederherstellungsanwendung ist auch verantwortlich für die Arbeit mit Windows-Server zum Lesen und Schreiben von Daten in die backup-Datenträger, gibt an, ob ein Band zu archivieren, ein Storage Area Network oder andere Sicherungsmedien.</span><span class="sxs-lookup"><span data-stu-id="c5f78-p106">When restoring, the requestor also communicates with the VSS to prepare the system for the restore operation, and then to put the data back onto the mass storage device. The backup/restore application is also responsible for working with Windows Server to read data from and write data to the backup storage media, whether a tape archive, a storage area network, or other backup medium.</span></span> 
  
    
    
<span data-ttu-id="c5f78-125">Die Informationen, die zum erfolgreichen Ausführen von Sicherungs- und Wiederherstellungsvorgängen mit SharePoint Foundation, dem VSS und der Sicherungs-/Wiederherstellungsanwendung erforderlich sind, werden als Teil der SPF-VSS Writer-Metadaten übertragen.</span><span class="sxs-lookup"><span data-stu-id="c5f78-125">Information needed to successfully complete backup and restore operations among SharePoint Foundation, the VSS, and the backup/restore application is transferred as part of the SPF-VSS Writer metadata.</span></span>
  
    
    
<span data-ttu-id="c5f78-126">Die Abfolge oberster Ebene von Ergebnissen während der Sicherungs- und Wiederherstellungsvorgänge lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="c5f78-126">The following is the high-level sequence of events during backup or restore operations:</span></span>
  
    
    

  
    
    

1. <span data-ttu-id="c5f78-127">Vom Sicherungsprogramm (oder Agent) wird ein geplanter Auftrag ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="c5f78-127">The backup program (or agent) runs a scheduled job.</span></span> 
    
  
2. <span data-ttu-id="c5f78-128">Der VSS-Anforderer in der Sicherungs-/Wiederherstellungsanwendung sendet einen Befehl zum Erstellen einer Schattenkopie der ausgewählten SharePoint Foundation-Speichergruppen an den VSS.</span><span class="sxs-lookup"><span data-stu-id="c5f78-128">The VSS requestor in the backup/restore application sends a command to the VSS to take a shadow copy of the selected SharePoint Foundation storage groups.</span></span> 
    
  
3. <span data-ttu-id="c5f78-p107">Der VSS kommuniziert mit dem SPF-VSS Writer, um eine Momentaufnahmensicherung vorzubereiten. SharePoint Foundation lässt Verwaltungsaktionen an der Speichergruppe nicht zu, überprüft Volumeabhängigkeiten und hält alle Schreibvorgänge in Datenbank- und Transaktionsprotokolldateien an, während Nur-Lese-Zugriff erteilt wird.</span><span class="sxs-lookup"><span data-stu-id="c5f78-p107">The VSS communicates with the SPF-VSS Writer to prepare for a snapshot backup. SharePoint Foundation prohibits administrative actions against the storage group, checks volume dependencies, and suspends all write operations to database and transaction log files while allowing read-only access.</span></span> 
    
  
4. <span data-ttu-id="c5f78-131">Der VSS kommuniziert mit dem entsprechenden Speicheranbieter, damit eine Schattenkopie des Speichervolumes erstellt wird, das die SharePoint Foundation-Speichergruppe enthält.</span><span class="sxs-lookup"><span data-stu-id="c5f78-131">The VSS communicates with the appropriate storage provider to create a shadow copy of the storage volume that contains the SharePoint Foundation storage group.</span></span> 
    
  
5. <span data-ttu-id="c5f78-132">Der VSS gibt SharePoint Foundation frei, um die normalen Vorgänge fortzusetzen.</span><span class="sxs-lookup"><span data-stu-id="c5f78-132">The VSS releases SharePoint Foundation to resume ordinary operations.</span></span>
    
  
6. <span data-ttu-id="c5f78-p108">Der VSS-Anforderer überprüft die Integrität des Sicherungssatzes, bevor der Erfolg der Sicherung angezeigt wird. Die Zeit der letzten Datenbanksicherung wird von SharePoint Foundation erfasst.</span><span class="sxs-lookup"><span data-stu-id="c5f78-p108">The VSS requestor verifies the integrity of the backup set prior to signaling that the backup succeeded. SharePoint Foundation records the time of the last backup for the database.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="c5f78-135">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="c5f78-135">See also</span></span>
<span data-ttu-id="c5f78-136"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c5f78-136"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="c5f78-137">SharePoint VSS Writer</span><span class="sxs-lookup"><span data-stu-id="c5f78-137">SharePoint VSS Writer</span></span>](sharepoint-vss-writer.md)
    
  
-  [<span data-ttu-id="c5f78-138">VSS-Anforderer und SharePoint</span><span class="sxs-lookup"><span data-stu-id="c5f78-138">VSS requestors and SharePoint</span></span>](vss-requestors-and-sharepoint.md)
    
  
-  [<span data-ttu-id="c5f78-139">Vorgehensweise: Erstellen ein Volumenschattenkopie-Anforderers für die Verwendung mit SharePoint</span><span class="sxs-lookup"><span data-stu-id="c5f78-139">How to: Create a VSS requestor for use with SharePoint</span></span>](how-to-create-a-vss-requestor-for-use-with-sharepoint.md)
    
  
-  [<span data-ttu-id="c5f78-140">Vorgehensweise: Sichern und Wiederherstellen von SharePoint verwenden eines VSS-Requestors</span><span class="sxs-lookup"><span data-stu-id="c5f78-140">How to: Back up and restore SharePoint using a VSS requestor</span></span>](how-to-back-up-and-restore-sharepoint-using-a-vss-requestor.md)
    
  
-  [<span data-ttu-id="c5f78-141">Vorgehensweise: Sichern und Wiederherstellen eine Suchdienstanwendung in SharePoint mit VSS</span><span class="sxs-lookup"><span data-stu-id="c5f78-141">How to: Back up and restore a search service application in SharePoint using VSS</span></span>](how-to-back-up-and-restore-a-search-service-application-in-sharepoint-using.md)
    
  
-  <span data-ttu-id="c5f78-142">[Starting and Configuring the WSS Writer Service]((http://msdn.microsoft.com/library/c9243dd6-e61e-4783-9fef-48d0122f1c09.aspx))</span><span class="sxs-lookup"><span data-stu-id="c5f78-142">[Starting and Configuring the WSS Writer Service]((http://msdn.microsoft.com/library/c9243dd6-e61e-4783-9fef-48d0122f1c09.aspx))</span></span>
    
  
-  <span data-ttu-id="c5f78-143">
  [Volumeschattenkopie-Dienst](http://msdn.microsoft.com/en-us/library/windows/desktop/bb968832%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="c5f78-143">[Volume Shadow Copy Service](http://msdn.microsoft.com/en-us/library/windows/desktop/bb968832%28v=vs.85%29.aspx)</span></span>
    
  
-  <span data-ttu-id="c5f78-144">
  [Volume Shadow Copy Service Technical Reference](http://msdn.microsoft.com/en-us/library/windows/desktop/aa384648%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="c5f78-144">[Volume Shadow Copy Service Technical Reference](http://msdn.microsoft.com/en-us/library/windows/desktop/aa384648%28v=vs.85%29.aspx)</span></span>
    
  

