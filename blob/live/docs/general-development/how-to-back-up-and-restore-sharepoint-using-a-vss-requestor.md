---
title: Sichern und Wiederherstellen von SharePoint unter Verwendung eines VSS-Anforderers
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: cab5ba90-bd23-4cec-82d7-529e3f86ba88
ms.openlocfilehash: 76664d750be4e8ecf98dae4fc5aa106d2c8864e7
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="back-up-and-restore-sharepoint-using-a-vss-requestor"></a><span data-ttu-id="373b3-102">Sichern und Wiederherstellen von SharePoint unter Verwendung eines VSS-Anforderers</span><span class="sxs-lookup"><span data-stu-id="373b3-102">How to: Back up and restore SharePoint using a VSS requestor</span></span>

<span data-ttu-id="373b3-103">Informationen Sie zum Sichern und Wiederherstellen von mithilfe eines Gruppenrichtlinien-Verwaltungskonsole (Volume Shadow Copy Service, VSS)-Anforderers für Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="373b3-103">Summary: Learn how to back and restore using a Volume Shadow Copy Service (VSS) requestor for Microsoft SharePoint.</span></span>

## <a name="backing-up-and-restoring-with-the-requestor"></a><span data-ttu-id="373b3-104">Sicherung und Wiederherstellung mit der Anforderer</span><span class="sxs-lookup"><span data-stu-id="373b3-104">Backing up and restoring with the requestor</span></span>

<span data-ttu-id="373b3-105">Verwenden Sie das folgende Verfahren zum Sichern und Wiederherstellen von Microsoft SharePoint Foundation -Daten mithilfe des VSS-Requestors.</span><span class="sxs-lookup"><span data-stu-id="373b3-105">Use the following procedure to back up and restore Microsoft SharePoint Foundation data using your VSS requestor.</span></span>
  
    
    

### <a name="to-back-up-and-restore-data-by-using-your-requestor"></a><span data-ttu-id="373b3-106">Zum Sichern und Wiederherstellen von Daten mithilfe des Requestors</span><span class="sxs-lookup"><span data-stu-id="373b3-106">To back up and restore data by using your requestor</span></span>


1. <span data-ttu-id="373b3-p101">Starten Sie den VSS Writer-Dienst von SharePoint Foundation manuell. Öffnen Sie **Verwaltung**, dann **Dienste**, und starten Sie die Dienste **Volumeschattenkopie** und **SharePoint 2010 VSS Writer**.</span><span class="sxs-lookup"><span data-stu-id="373b3-p101">Manually start the SharePoint Foundation VSS Writer service. Open **Administrative Tools**, navigate to and open **Services** and start the services called **Volume Shadow Copy** and **SharePoint 2010 VSS Writer**.</span></span>
    
  
2. <span data-ttu-id="373b3-109">Registrieren Sie den Writer in der Windows-Registrierung, indem Sie den `STSADM -o registerwsswriter`-Befehl von einer Systemkonsole aus ausführen.</span><span class="sxs-lookup"><span data-stu-id="373b3-109">Register the writer in the Windows registry by running the  `STSADM -o registerwsswriter` command from a system console.</span></span> <span data-ttu-id="373b3-110">Die ausführbare Datei befindet sich im Verzeichnis %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\BIN.</span><span class="sxs-lookup"><span data-stu-id="373b3-110">The executable is located in the %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\BIN directory.</span></span>
    
  
3. <span data-ttu-id="373b3-111">Wiederholen Sie die Schritte 1 und 2 auf allen für SharePoint Foundation-Servern.</span><span class="sxs-lookup"><span data-stu-id="373b3-111">Repeat steps 1 and 2 on all SharePoint Foundation servers.</span></span>
    
  
4. <span data-ttu-id="373b3-p103">Verwenden Sie den Requestor, um Daten zu sichern und wiederherzustellen. Sie können entweder Ihren Requestor (wie unter  [Übersicht über den Volumeschattenkopie-Dienst](http://msdn.microsoft.com/de-DE/library/aa384649%28VS.85%29.aspx) beschrieben) oder das Testprogramm BETest (erhältlich im [VSS SDK](http://www.microsoft.com/downloads/details.aspx?FamilyID=0B4F56E4-0CCC-4626-826A-ED2C4C95C871&amp;displaylang=en)) verwenden, um eine Sicherung oder Wiederherstellung aus SharePoint Foundation durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="373b3-p103">Use your requestor to back up and restore data. You can either use your requestor (as outlined in the  [Volume Shadow Copy Service Overview](http://msdn.microsoft.com/de-DE/library/aa384649%28VS.85%29.aspx)) or the BETest test utility (available in the  [VSS SDK](http://www.microsoft.com/downloads/details.aspx?FamilyID=0B4F56E4-0CCC-4626-826A-ED2C4C95C871&amp;displaylang=en)) to back up or restore from SharePoint Foundation.</span></span> 
    
  

## <a name="security-for-running-vss"></a><span data-ttu-id="373b3-114">Sicherheit beim Ausführen des Volumeschattenkopie-Diensts</span><span class="sxs-lookup"><span data-stu-id="373b3-114">Security for Running VSS</span></span>

<span data-ttu-id="373b3-115">Für den Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) gelten besondere Bedingungen für die Konten, unter denen die Writer auf allen Zielserverinstanzen für die Sicherung und Wiederherstellung ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="373b3-115">VSS has special requirements for the accounts running the writers on all targeted server instances for backup and restore</span></span>
  
    
    

- <span data-ttu-id="373b3-p104">Das ausführende Konto muss die Berechtigung für Aufrufe in VSS haben. Für VSS muss ein VSS Writer standardmäßig ein Mitglied der Gruppe Administratoren oder Sicherungs-Operatoren auf der Zielserverinstanz sein. Sie können einen Registrierungsschlüssel so konfigurieren, dass andere Konten die Berechtigung zum Zugriff auf VSS haben.</span><span class="sxs-lookup"><span data-stu-id="373b3-p104">The running account must have permission to call into VSS. By default, VSS requires a VSS writer to be a member of the Administrator or Backup Operators group on the targeted server instance. You can configure a registry key to allow other accounts to have access to VSS.</span></span>
    
  
- <span data-ttu-id="373b3-119">Das Konto muss die Berechtigung zum Ausgeben von **BACKUP DATABASE**- und **RESTORE DATABASE**-Befehlen für die Datenbankserver haben.</span><span class="sxs-lookup"><span data-stu-id="373b3-119">The account must have permission to issue **BACKUP DATABASE** and **RESTORE DATABASE** commands against the database servers.</span></span>
    
  
- <span data-ttu-id="373b3-120">Das Konto muss die Berechtigung zum Öffnen von VDI für SQL  Server haben. Dazu muss der Client ein Mitglied der SQL Server-Gruppe sysadmin sein.</span><span class="sxs-lookup"><span data-stu-id="373b3-120">The account must have permission to open up VDI against SQL Server, which requires the client to be a member of the SQL Server sysadmin group.</span></span>
    
  
- <span data-ttu-id="373b3-121">Das Konto muss in der Lage sein, Abfragen für die sys.master_files-Katalogansicht in der Masterdatenbank auf dem SQL-Server auszuführen.</span><span class="sxs-lookup"><span data-stu-id="373b3-121">The account must be able to perform queries against the sys.master_files catalog view in the master database on the SQL server.</span></span>
    
  
<span data-ttu-id="373b3-122">Außerdem muss der Writer-Dienst, damit er vom SharePoint Foundation-Timerdienst (owstimer.exe) gehostet wird, unter dem Anwendungspoolkonto der Zentraladministration ausgeführt werden, das in einer einfachen Installation von SharePoint Foundation das Netzwerkdienstkonto ist.</span><span class="sxs-lookup"><span data-stu-id="373b3-122">Also, to be hosted by the SharePoint Foundation Timer service (owstimer.exe), the writer service must run under the administration application pool account, which is the "Network Service" account in a basic installation of SharePoint Foundation.</span></span> 
  
    
    
 <span data-ttu-id="373b3-123">**Hinweis** Es ist sehr unwahrscheinlich, dass dieses Konto ein Administratorkonto eines lokalen Computers ist, d. h. die Anforderung für VSS nicht erfüllt wird, nach der das verarbeitende Konto als lokales System ausgeführt werden muss.</span><span class="sxs-lookup"><span data-stu-id="373b3-123">**Note** It is very unlikely that this account will be a local machine admin account, which differs from the requirement for VSS where the processing account must be running as local system.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="373b3-124">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="373b3-124">Additional resources</span></span>
<span data-ttu-id="373b3-125"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="373b3-125"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="373b3-126">Übersicht über SharePoint und der Volumeschattenkopie-Dienst</span><span class="sxs-lookup"><span data-stu-id="373b3-126">Overview of SharePoint and the Volume Shadow Copy Service</span></span>](overview-of-sharepoint-and-the-volume-shadow-copy-service.md)
    
  

