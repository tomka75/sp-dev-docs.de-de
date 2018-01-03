---
title: Sichern und Wiederherstellen von SharePoint unter Verwendung eines VSS-Anforderers
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: cab5ba90-bd23-4cec-82d7-529e3f86ba88
ms.openlocfilehash: cebe16cbc4a7094658c762664a1088f799492aa6
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="back-up-and-restore-sharepoint-using-a-vss-requestor"></a>Sichern und Wiederherstellen von SharePoint unter Verwendung eines VSS-Anforderers

Informationen Sie zum Sichern und Wiederherstellen von mithilfe eines Gruppenrichtlinien-Verwaltungskonsole (Volume Shadow Copy Service, VSS)-Anforderers für Microsoft SharePoint.

## <a name="backing-up-and-restoring-with-the-requestor"></a>Sicherung und Wiederherstellung mit der Anforderer

Verwenden Sie das folgende Verfahren zum Sichern und Wiederherstellen von Microsoft SharePoint Foundation -Daten mithilfe des VSS-Requestors.
  
    
    

### <a name="to-back-up-and-restore-data-by-using-your-requestor"></a>Zum Sichern und Wiederherstellen von Daten mithilfe des Requestors


1. Starten Sie den VSS Writer-Dienst von SharePoint Foundation manuell. Öffnen Sie **Verwaltung**, dann **Dienste**, und starten Sie die Dienste **Volumeschattenkopie** und **SharePoint 2010 VSS Writer**.
    
  
2. Registrieren Sie den Writer in der Windows-Registrierung, indem Sie den `STSADM -o registerwsswriter`-Befehl von einer Systemkonsole aus ausführen. Die ausführbare Datei befindet sich im Verzeichnis %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\BIN.
    
  
3. Wiederholen Sie die Schritte 1 und 2 auf allen für SharePoint Foundation-Servern.
    
  
4. Verwenden Sie den Requestor, um Daten zu sichern und wiederherzustellen. Sie können entweder Ihren Requestor (wie unter  [Übersicht über den Volumeschattenkopie-Dienst]((http://msdn.microsoft.com/de-DE/library/aa384649%28VS.85%29.aspx)) beschrieben) oder das Testprogramm BETest (erhältlich im [VSS SDK](http://www.microsoft.com/downloads/details.aspx?FamilyID=0B4F56E4-0CCC-4626-826A-ED2C4C95C871&amp;displaylang=en)) verwenden, um eine Sicherung oder Wiederherstellung aus SharePoint Foundation durchzuführen. 
    
  

## <a name="security-for-running-vss"></a>Sicherheit beim Ausführen des Volumeschattenkopie-Diensts

Für den Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) gelten besondere Bedingungen für die Konten, unter denen die Writer auf allen Zielserverinstanzen für die Sicherung und Wiederherstellung ausgeführt werden.
  
    
    

- Das ausführende Konto muss die Berechtigung für Aufrufe in VSS haben. Für VSS muss ein VSS Writer standardmäßig ein Mitglied der Gruppe Administratoren oder Sicherungs-Operatoren auf der Zielserverinstanz sein. Sie können einen Registrierungsschlüssel so konfigurieren, dass andere Konten die Berechtigung zum Zugriff auf VSS haben.
    
  
- Das Konto muss die Berechtigung zum Ausgeben von **BACKUP DATABASE**- und **RESTORE DATABASE**-Befehlen für die Datenbankserver haben.
    
  
- Das Konto muss die Berechtigung zum Öffnen von VDI für SQL  Server haben. Dazu muss der Client ein Mitglied der SQL Server-Gruppe sysadmin sein.
    
  
- Das Konto muss in der Lage sein, Abfragen für die sys.master_files-Katalogansicht in der Masterdatenbank auf dem SQL-Server auszuführen.
    
  
Außerdem muss der Writer-Dienst, damit er vom SharePoint Foundation-Timerdienst (owstimer.exe) gehostet wird, unter dem Anwendungspoolkonto der Zentraladministration ausgeführt werden, das in einer einfachen Installation von SharePoint Foundation das Netzwerkdienstkonto ist. 
  
> [!NOTE]
> Es ist sehr unwahrscheinlich, dass dieses Konto ein Administratorkonto eines lokalen Computers ist, d. h. die Anforderung für VSS nicht erfüllt wird, nach der das verarbeitende Konto als lokales System ausgeführt werden muss.
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Übersicht über SharePoint und der Volumeschattenkopie-Dienst](overview-of-sharepoint-and-the-volume-shadow-copy-service.md)
    
  

