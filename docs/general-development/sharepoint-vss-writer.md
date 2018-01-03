---
title: SharePoint VSS Writer
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f83577e4-ebb8-44e5-8dec-a3ca5878b7fd
ms.openlocfilehash: 98e80844bdf8adf482307db51a4b049f8429c1b5
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-vss-writer"></a><span data-ttu-id="5862f-102">SharePoint VSS Writer</span><span class="sxs-lookup"><span data-stu-id="5862f-102">SharePoint VSS Writer</span></span>
 <span data-ttu-id="5862f-p101">**Zusammenfassung:** Informationen Sie zu den Eigenschaften und Features von der Gruppenrichtlinien-Verwaltungskonsole (Volume Shadow Copy Service, VSS) Writer für Microsoft SharePoint. Der VSS im Lieferumfang von Windows Server ist die Infrastruktur, die Funktionen der integrierten Shadow-Kopien bereitstellt. Schattenkopien erstellt von VSS ergänzen des Administrators die Speicher Band Archivierung Sicherungslösungen, Bereitstellung von High Fidelity Point-in-Time-Kopien, die erstellt werden können und auf einfache Weise und verbessern, damit helfen, die verschiedene Aspekte der Speicherung und Verwaltung vereinfachen wiederhergestellt. Microsoft SharePoint Foundation verwendet VSS zum Vereinfachen der Sicherung und Wiederherstellungsvorgängen.</span><span class="sxs-lookup"><span data-stu-id="5862f-p101">**Summary:** Learn about the characteristics and features of the Volume Shadow Copy Service (VSS) writer for Microsoft SharePoint. The VSS included with Windows Server is the infrastructure that provides built-in shadow copy capabilities. Shadow copies created by VSS augment the storage administrator's tape backup archival solutions, providing high fidelity point-in-time copies that can be created and restored easily and effectively, thereby helping to simplify several aspects of storage and data management. Microsoft SharePoint Foundation uses VSS to simplify backup and restore operations.</span></span> 
  
    
    


## <a name="characteristics-of-the-system"></a><span data-ttu-id="5862f-107">Eigenschaften des Systems</span><span class="sxs-lookup"><span data-stu-id="5862f-107">Characteristics of the System</span></span>

<span data-ttu-id="5862f-108">Im folgenden sind die SharePoint Foundation VSS-Lösung Funktionen und Merkmale:</span><span class="sxs-lookup"><span data-stu-id="5862f-108">Following are the SharePoint Foundation VSS solution features and characteristics:</span></span>
  
    
    

- <span data-ttu-id="5862f-p102">**Ein einzelner VSS-Verweisschreiber.** Das Schreiben von Daten von Anwendungen zu Sicherungsanwendungen war nie einfach. Zum erfolgreichen Sichern verschiedener Windows-Plattformanwendungen besitzen Sicherungsanwendungen eine sehr große Anzahl von APIs, für die spezifischer Code geschrieben werden muss. Der SharePoint Foundation VSS Writer (nachfolgend "SPF VSS Writer" genannt) ermöglicht das Nutzen des einzelnen Writers zum Sichern von SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="5862f-p102">**A single VSS reference writer.** There has been no easy way for applications to describe their data to backup applications. To successfully back up various Windows platform applications, backup applications have an excessive number of APIs that they need to write specific code for. The SharePoint Foundation VSS writer (hereafter called "the SPF-VSS Writer") enables backup applications to take advantage of the single writer to backup SharePoint Foundation.</span></span>
    
  
- <span data-ttu-id="5862f-p103">**Sicherung und Wiederherstellung der vollständigen Farm für den Notfall.** Mit dem SPF VSS Writer kann eine Sicherungsanwendung (Anforderer) auf die VSS-API zugreifen, um einen Sicherungs- oder Wiederherstellungsvorgang für eine gesamte SharePoint Foundation-Farm anzufordern, einschließlich eines Setups in einem einzelnen System oder einer Farmkonfiguration. (Der IIS-Konfigurationsspeicher, bei dem es sich hauptsächlich um die Datei `applicationhost.config` handelt, ist nicht enthalten. Er muss separat gesichert und wiederhergestellt werden.)</span><span class="sxs-lookup"><span data-stu-id="5862f-p103">**Full farm backup and restore for catastrophe.** The SPF-VSS Writer enables a backup application (requestor) to access the VSS API to request a backup or a restore operation for an entire SharePoint Foundation farm, including a single box setup or a farm configuration. (The IIS configuration store, which is primarily the `applicationhost.config` file, is not included. It must be backed up and restored separately.)</span></span>
    
  
- <span data-ttu-id="5862f-p104">**Granularität auf Datenbankebene**. Mit dem SPF VSS Writer kann ein Anforderer alle Datenbanken, ein Segment der Datenbanken (Mehrfachauswahl) oder eine einzelne Datenbank (Einzelauswahl) sowohl für Sicherungs- als auch für Wiederherstellungsvorgänge auswählen. Alle Datenbanken mit Ausnahme der Konfigurations- und der Inhaltsdatenbank der Zentraladministration können über den Writer ausgewählt werden. Die Konfigurations- und die Inhaltsdatenbank der Zentraladministration können nur als Teil der ganzen Farm gesichert und wiederhergestellt werden. (Der IIS-Konfigurationsspeicher ist nicht enthalten. Er muss separat gesichert und wiederhergestellt werden.)</span><span class="sxs-lookup"><span data-stu-id="5862f-p104">**Database level granularity**. The SPF-VSS Writer enables a requestor to select all databases, a segment of the databases (multiple select), or a single database (single select) for both backup and restore operations. All databases, except configuration and the Central Administration content database, are selectable through the writer. The configuration and Central Administration content databases can be backed up and restored only as part of the whole farm. (The IIS configuration store is not included. It must be backed up and restored separately.)</span></span>
    
  
- <span data-ttu-id="5862f-p105">**Inventur von Datenbanken.** Vor der Sicherung generiert der SPF VSS Writer eine flache Liste der für eine Sicherung in der Farm ausgewählten Datenbanken. Die Liste wird an den Anforderer zurückgegeben, sodass die Sicherung an dem Speicherort ausgeführt werden kann, an dem sich die Datenbank physikalisch befindet.</span><span class="sxs-lookup"><span data-stu-id="5862f-p105">**Inventory of databases.** Before backup, the SPF-VSS Writer generates a flat list of databases selected for backup within the farm. The list is returned to the requestor so that backup can be run on the location where the database is physically located.</span></span>
    
  
- <span data-ttu-id="5862f-p106">**Farmunterstützung.** Vom Writer wird Unterstützung für die Synchronisierung der Sicherung und Wiederherstellung in einer SharePoint Foundation-Farm auf begrenzte Art und Weise bereitgestellt. Der Anforderer erhält vom Writer eine Liste der Server, Datenbanken und Dateien, die der Farm zugeordnet sind. Der Anforderer ist für das Herstellen einer separaten Verbindung mit jedem Server verantwortlich, um den SPF VSS Writer auf diesem Server zum Generieren der Sicherung oder zum Ausführen des Wiederherstellungsvorgangs aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="5862f-p106">**Farm support.** The writer understands and provides support to synchronize backup and recovery on a SharePoint Foundation farm in a limited way. The writer provides the requestor with a list of servers, databases, and files associated with the farm. The requestor is responsible for making a separate connection to each server to call the SPF-VSS Writer on that server to generate the backup or to run the restore operation.</span></span>
    
  
- <span data-ttu-id="5862f-p107">**Sichern von Inhalt ohne Unterbrechung.** Falls eine Datei von einer Anwendung während der Sicherung geändert wird, kann die Datei dadurch beschädigt werden. Mit VSS wird eine rasche Momentaufnahme der Dateien für die Schattenkopie erstellt, während die Anwendung am ursprünglichen Speicherort ohne Unterbrechung weiter ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="5862f-p107">**Backup content without interruption.** If an application modifies a file while it is being backed up, the file could become corrupt. VSS enables a quick snapshot of the files to the shadow copy, while the application continues to operate at the original location without interruption.</span></span>
    
  
- <span data-ttu-id="5862f-p108">**Austauschbare Datenbanksicherung und -wiederherstellung von Drittanbietern.** Mit dem SPF VSS Writer wird die austauschbare/erweiterbare Sicherung für Lösungen von Drittanbietern angeboten, die auf SharePoint Foundation aufbauen. Es sind jedoch nur die Datenbanken im Writer enthalten, die in der Konfigurationsdatenbank registriert sind. Alle weiteren Dateien und nicht registrierten Datenbanken sind nicht enthalten.</span><span class="sxs-lookup"><span data-stu-id="5862f-p108">**Third-party pluggable database backup and recovery.** The SPF-VSS Writer offers pluggable/extensible backup for third-party solutions built on top of SharePoint Foundation. However, only databases that are registered within the configuration database are included in the writer. Any additional files and unregistered databases are not included.</span></span>
    
  
- <span data-ttu-id="5862f-p109">**Sicherung und Wiederherstellung von Suchindexdateien.** Da Suchindexdateien im Dateisystem gespeichert werden, ist zu ihrer Sicherung ein separater Dateischreiber erforderlich. Zur Lösung dieses Problems enthält SharePoint Foundation einen separaten Suchschreiber, der Suchindexdateien behandelt. Zur Vereinfachung des Sicherns von Anwendungsschreibern deklariert SharePoint Foundation schreiberübergreifende Abhängigkeiten so, dass Suchindexdateien beim Sichern von registrierten Datenbanken in der Farm gesichert oder wiederhergestellt werden.</span><span class="sxs-lookup"><span data-stu-id="5862f-p109">**Search index files backup and recovery.** Because search index files are stored in the file system, a separate file writer is needed to them up back up. To resolve this, SharePoint Foundation includes a separate search writer that handles search index files. To simplify the process for backup application writers, SharePoint Foundation declares cross-writer dependencies in such a way that search index files are also backed up or restored when backing up registered databases in the farm.</span></span>
    
  
- <span data-ttu-id="5862f-p110">**Vollständiges Rollback.** Der SPF VSS Writer behandelt alle Komponenten in einer SharePoint Foundation-Bereitstellung, einschließlich der Konfigurationsdatenbank und der Inhaltsdatenbanken und der Suchdatenbank und des Suchindexes. Wie bereits zuvor erwähnt, besitzt der Writer auch eine Abhängigkeit vom Suchschreiber, der alle Suchindexdateien für die Sicherung und Wiederherstellung behandelt. Zum Zeitpunkt der Wiederherstellung kann der Writer ein Rollback der gesamten SharePoint Foundation-Bereitstellung durchführen, indem eine vorherige Farmsicherung wiederhergestellt wird. (Der IIS-Konfigurationsspeicher ist nicht enthalten. Er muss separat gesichert und wiederhergestellt werden.)</span><span class="sxs-lookup"><span data-stu-id="5862f-p110">**Full rollback.** The SPF-VSS Writer handles all components within a SharePoint Foundation deployment, including the configuration database and the content databases and the Search database and index. As mentioned previously, the writer also has a dependency on the Search writer, which handles all the Search index files for backup and recovery. At the time of recovery, the writer can roll back the entire SharePoint Foundation deployment by restoring a previous farm backup. (The IIS configuration store is not included. It must be backed up and restored separately.)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="5862f-147">Wichtige Informationen zur Wiederherstellung finden Sie im Abschnitt „Wiederherstellen“ im Artikel [VSS-Anforderer und SharePoint](vss-requestors-and-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="5862f-147">[Note:](vss-requestors-and-sharepoint.md) See "Restoring" in  VSS requestors and SharePoint for important information about restorations.</span></span>

- <span data-ttu-id="5862f-p111">**Synchronisierung von Datenbanken nach der Wiederherstellung.** Zur Sicherstellung, dass alle Datenbanken nach Abschluss eines Wiederherstellungsvorgangs mit der Farm synchronisiert werden, wird jede Datenbank automatisch nach der Wiederherstellung getrennt und wieder mit der Farm verbunden. Administratoren müssen keine zusätzlichen Verfahren ausführen, um die wiederhergestellten Datenbanken erneut zu synchronisieren.</span><span class="sxs-lookup"><span data-stu-id="5862f-p111">**Post-restore synchronization of databases.** To ensure that all databases are synchronized with the farm after a restore operation is complete, each of the databases are automatically detached and reattached to the farm post recovery. Administrators do not need to run additional procedures to resynchronize the restored databases.</span></span>
    
> [!IMPORTANT]
> <span data-ttu-id="5862f-151">Wenn Sie in Ihrer SharePoint Foundation-Farm SQL-Aliasse zur Anbindung an SQL Server verwenden, müssen Sie die Komponenten für SQL-Clientkonnektivität auf den Farmservern installieren, um SPF-VSS Writer für Sicherungen/Wiederherstellungen nutzen zu können.</span><span class="sxs-lookup"><span data-stu-id="5862f-151">Important: If you use SQL aliases in your SharePoint Foundation farm to connect to the SQL Server, then you must install the SQL client connectivity components on your farm servers in order to use the SPF-VSS writer for backup/restore.</span></span> <span data-ttu-id="5862f-152">Zu diesen Komponenten gehört der SQL-WMI-Anbieter für die Konfigurationsverwaltung. SPF-VSS Writer benötigt diesen Anbieter, um die SQL-Aliasse auf die richtige SQL Server-Instanz auflösen zu können.</span><span class="sxs-lookup"><span data-stu-id="5862f-152">The components include SQL WMI provider for configuration management, which the SPF-VSS writer needs to resolve SQL aliases to the correct SQL Server.</span></span> <span data-ttu-id="5862f-153">Eine Installation von Verwaltungstools wie SQL Management Studio ist nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="5862f-153">It is not necessary to install any of the management tools such as SQL Management Studio.</span></span> <span data-ttu-id="5862f-154">Sie müssen dieselbe Installationsquelle verwenden wie für die Installation der SQL Server-Vollversion, beispielsweise eine Daten-DVD.</span><span class="sxs-lookup"><span data-stu-id="5862f-154">You must use the same installation source (for example, a data DVD) that you would use to install the full SQL Server product.</span></span> <span data-ttu-id="5862f-155">(Verwenden Sie auf keinen Fall die separaten, eigenständigen Versionen der Clientkomponenten.</span><span class="sxs-lookup"><span data-stu-id="5862f-155">(Do not use the separate, stand-alone, version of the client components.</span></span> <span data-ttu-id="5862f-156">Der SQL-WMI-Anbieter ist in diesen Versionen nicht enthalten.) Entscheiden Sie sich für eine benutzerdefinierte Installation, und installieren Sie lediglich die Clientkomponenten.</span><span class="sxs-lookup"><span data-stu-id="5862f-156">That version does not include the SQL WMI provider.) Choose to make a custom installation and choose only the client components to install.</span></span> 
  
    
    


## <a name="functions-performed-by-the-spf-vss-writer"></a><span data-ttu-id="5862f-157">Von SPF-VSS Writer ausgeführte Funktionen</span><span class="sxs-lookup"><span data-stu-id="5862f-157">Functions Performed by the SPF-VSS Writer</span></span>

<span data-ttu-id="5862f-158">Vom SPF VSS Writer werden die folgenden Funktionen ausgeführt:</span><span class="sxs-lookup"><span data-stu-id="5862f-158">The SPF-VSS Writer performs the following functions:</span></span>
  
    
    

1. <span data-ttu-id="5862f-159">Erstellt SharePoint Foundation-Komponenten.</span><span class="sxs-lookup"><span data-stu-id="5862f-159">Builds SharePoint Foundation components.</span></span>
    
  - <span data-ttu-id="5862f-160">Generiert eine vollständige Liste aller Komponenten in der SharePoint Foundation-Farm.</span><span class="sxs-lookup"><span data-stu-id="5862f-160">Generates a full list of all components within the SharePoint Foundation farm.</span></span>
    
  
  - <span data-ttu-id="5862f-161">Er muss nicht an den Sicherungsprozess oder Wiederherstellungsprozess gebunden sein.</span><span class="sxs-lookup"><span data-stu-id="5862f-161">Is not necessarily tied to backup process or restore process.</span></span>
    
  

  ![SharePoint und Volumeschattenkopie-Dienst](../images/99376713-6a54-4d88-9b05-068578169506.gif)
  

  

  
2. <span data-ttu-id="5862f-163">Sichert Farm oder Datenbank.</span><span class="sxs-lookup"><span data-stu-id="5862f-163">Backs up farm or database.</span></span>
    
  - <span data-ttu-id="5862f-164">Fordert eine SharePoint Foundation-Sicherung (Farm/Datenbank) über VSS an.</span><span class="sxs-lookup"><span data-stu-id="5862f-164">Requests a SharePoint Foundation (farm/database) backup via VSS.</span></span>
    
  

  ![SharePoint und Volumeschattenkopie-Dienst](../images/97765b6d-51e9-4d07-8b5d-3e93c0508b16.gif)
  

  

  
3. <span data-ttu-id="5862f-166">Stellt eine Farm oder Datenbank wieder her.</span><span class="sxs-lookup"><span data-stu-id="5862f-166">Restores a farm or database.</span></span>
    
  - <span data-ttu-id="5862f-167">Fordert eine SharePoint Foundation-Wiederherstellung (Farm/Datenbank) über VSS an.</span><span class="sxs-lookup"><span data-stu-id="5862f-167">Requests a SharePoint Foundation (farm/database) recovery via VSS.</span></span>
    
  
  - <span data-ttu-id="5862f-168">Implementiert **postRestore()** zum Synchronisieren von Websitetabellen.</span><span class="sxs-lookup"><span data-stu-id="5862f-168">Implements **postRestore()** to synchronize sites table.</span></span>
    
  

  ![SharePoint und Volumeschattenkopie-Dienst](../images/b86ecdb8-88a7-4407-af86-07d2442235dc.gif)
  

  

  

## <a name="next-steps"></a><span data-ttu-id="5862f-170">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="5862f-170">Next steps</span></span>
<span data-ttu-id="5862f-171"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="5862f-171"><a name="Next"> </a></span></span>

<span data-ttu-id="5862f-172">Erfahren Sie, wie erstellen und Verwenden eines VSS-Requestors für SharePoint:</span><span class="sxs-lookup"><span data-stu-id="5862f-172">Learn how to create and use a VSS requestor for SharePoint:</span></span>
  
    
    

-  [<span data-ttu-id="5862f-173">VSS-Anforderer und SharePoint</span><span class="sxs-lookup"><span data-stu-id="5862f-173">VSS requestors and SharePoint</span></span>](vss-requestors-and-sharepoint.md)
    
  

## <a name="see-also"></a><span data-ttu-id="5862f-174">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="5862f-174">See also</span></span>
<span data-ttu-id="5862f-175"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="5862f-175"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="5862f-176">Übersicht über SharePoint und der Volumeschattenkopie-Dienst</span><span class="sxs-lookup"><span data-stu-id="5862f-176">Overview of SharePoint and the Volume Shadow Copy Service</span></span>](overview-of-sharepoint-and-the-volume-shadow-copy-service.md)
    
  

