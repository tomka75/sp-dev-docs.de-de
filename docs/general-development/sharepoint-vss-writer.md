---
title: SharePoint VSS Writer
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f83577e4-ebb8-44e5-8dec-a3ca5878b7fd
ms.openlocfilehash: 017a84bf57af7bf675a3825cb3a8a3dd2a9076fa
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-vss-writer"></a>SharePoint VSS Writer
 **Zusammenfassung:** Informationen Sie zu den Eigenschaften und Features von der Gruppenrichtlinien-Verwaltungskonsole (Volume Shadow Copy Service, VSS) Writer für Microsoft SharePoint. Der VSS im Lieferumfang von Windows Server ist die Infrastruktur, die Funktionen der integrierten Shadow-Kopien bereitstellt. Schattenkopien erstellt von VSS ergänzen des Administrators die Speicher Band Archivierung Sicherungslösungen, Bereitstellung von High Fidelity Point-in-Time-Kopien, die erstellt werden können und auf einfache Weise und verbessern, damit helfen, die verschiedene Aspekte der Speicherung und Verwaltung vereinfachen wiederhergestellt. Microsoft SharePoint Foundation verwendet VSS zum Vereinfachen der Sicherung und Wiederherstellungsvorgängen. 
  
    
    


## <a name="characteristics-of-the-system"></a>Eigenschaften des Systems

Im folgenden sind die SharePoint Foundation VSS-Lösung Funktionen und Merkmale:
  
    
    

- **Ein einzelner VSS-Verweisschreiber.** Das Schreiben von Daten von Anwendungen zu Sicherungsanwendungen war nie einfach. Zum erfolgreichen Sichern verschiedener Windows-Plattformanwendungen besitzen Sicherungsanwendungen eine sehr große Anzahl von APIs, für die spezifischer Code geschrieben werden muss. Der SharePoint Foundation VSS Writer (nachfolgend "SPF VSS Writer" genannt) ermöglicht das Nutzen des einzelnen Writers zum Sichern von SharePoint Foundation.
    
  
- **Sicherung und Wiederherstellung der vollständigen Farm für den Notfall.** Mit dem SPF VSS Writer kann eine Sicherungsanwendung (Anforderer) auf die VSS-API zugreifen, um einen Sicherungs- oder Wiederherstellungsvorgang für eine gesamte SharePoint Foundation-Farm anzufordern, einschließlich eines Setups in einem einzelnen System oder einer Farmkonfiguration. (Der IIS-Konfigurationsspeicher, bei dem es sich hauptsächlich um die Datei `applicationhost.config` handelt, ist nicht enthalten. Er muss separat gesichert und wiederhergestellt werden.)
    
  
- **Granularität auf Datenbankebene**. Mit dem SPF VSS Writer kann ein Anforderer alle Datenbanken, ein Segment der Datenbanken (Mehrfachauswahl) oder eine einzelne Datenbank (Einzelauswahl) sowohl für Sicherungs- als auch für Wiederherstellungsvorgänge auswählen. Alle Datenbanken mit Ausnahme der Konfigurations- und der Inhaltsdatenbank der Zentraladministration können über den Writer ausgewählt werden. Die Konfigurations- und die Inhaltsdatenbank der Zentraladministration können nur als Teil der ganzen Farm gesichert und wiederhergestellt werden. (Der IIS-Konfigurationsspeicher ist nicht enthalten. Er muss separat gesichert und wiederhergestellt werden.)
    
  
- **Inventur von Datenbanken.** Vor der Sicherung generiert der SPF VSS Writer eine flache Liste der für eine Sicherung in der Farm ausgewählten Datenbanken. Die Liste wird an den Anforderer zurückgegeben, sodass die Sicherung an dem Speicherort ausgeführt werden kann, an dem sich die Datenbank physikalisch befindet.
    
  
- **Farmunterstützung.** Vom Writer wird Unterstützung für die Synchronisierung der Sicherung und Wiederherstellung in einer SharePoint Foundation-Farm auf begrenzte Art und Weise bereitgestellt. Der Anforderer erhält vom Writer eine Liste der Server, Datenbanken und Dateien, die der Farm zugeordnet sind. Der Anforderer ist für das Herstellen einer separaten Verbindung mit jedem Server verantwortlich, um den SPF VSS Writer auf diesem Server zum Generieren der Sicherung oder zum Ausführen des Wiederherstellungsvorgangs aufzurufen.
    
  
- **Sichern von Inhalt ohne Unterbrechung.** Falls eine Datei von einer Anwendung während der Sicherung geändert wird, kann die Datei dadurch beschädigt werden. Mit VSS wird eine rasche Momentaufnahme der Dateien für die Schattenkopie erstellt, während die Anwendung am ursprünglichen Speicherort ohne Unterbrechung weiter ausgeführt wird.
    
  
- **Austauschbare Datenbanksicherung und -wiederherstellung von Drittanbietern.** Mit dem SPF VSS Writer wird die austauschbare/erweiterbare Sicherung für Lösungen von Drittanbietern angeboten, die auf SharePoint Foundation aufbauen. Es sind jedoch nur die Datenbanken im Writer enthalten, die in der Konfigurationsdatenbank registriert sind. Alle weiteren Dateien und nicht registrierten Datenbanken sind nicht enthalten.
    
  
- **Sicherung und Wiederherstellung von Suchindexdateien.** Da Suchindexdateien im Dateisystem gespeichert werden, ist zu ihrer Sicherung ein separater Dateischreiber erforderlich. Zur Lösung dieses Problems enthält SharePoint Foundation einen separaten Suchschreiber, der Suchindexdateien behandelt. Zur Vereinfachung des Sicherns von Anwendungsschreibern deklariert SharePoint Foundation schreiberübergreifende Abhängigkeiten so, dass Suchindexdateien beim Sichern von registrierten Datenbanken in der Farm gesichert oder wiederhergestellt werden.
    
  
- **Vollständiges Rollback.** Der SPF VSS Writer behandelt alle Komponenten in einer SharePoint Foundation-Bereitstellung, einschließlich der Konfigurationsdatenbank und der Inhaltsdatenbanken und der Suchdatenbank und des Suchindexes. Wie bereits zuvor erwähnt, besitzt der Writer auch eine Abhängigkeit vom Suchschreiber, der alle Suchindexdateien für die Sicherung und Wiederherstellung behandelt. Zum Zeitpunkt der Wiederherstellung kann der Writer ein Rollback der gesamten SharePoint Foundation-Bereitstellung durchführen, indem eine vorherige Farmsicherung wiederhergestellt wird. (Der IIS-Konfigurationsspeicher ist nicht enthalten. Er muss separat gesichert und wiederhergestellt werden.)
    
    > **Hinweis:** Wichtige Informationen zur Wiederherstellung finden Sie im Abschnitt „Wiederherstellen“ im Artikel [VSS-Anforderer und SharePoint](vss-requestors-and-sharepoint.md).
- **Synchronisierung von Datenbanken nach der Wiederherstellung.** Zur Sicherstellung, dass alle Datenbanken nach Abschluss eines Wiederherstellungsvorgangs mit der Farm synchronisiert werden, wird jede Datenbank automatisch nach der Wiederherstellung getrennt und wieder mit der Farm verbunden. Administratoren müssen keine zusätzlichen Verfahren ausführen, um die wiederhergestellten Datenbanken erneut zu synchronisieren.
    
  

> **Wichtig:** Wenn Sie in Ihrer SharePoint Foundation-Farm SQL-Aliasse zur Anbindung an SQL Server verwenden, müssen Sie die Komponenten für SQL-Clientkonnektivität auf den Farmservern installieren, um SPF-VSS Writer für Sicherungen/Wiederherstellungen nutzen zu können. Zu diesen Komponenten gehört der SQL-WMI-Anbieter für die Konfigurationsverwaltung. SPF-VSS Writer benötigt diesen Anbieter, um die SQL-Aliasse auf die richtige SQL Server-Instanz auflösen zu können. Eine Installation von Verwaltungstools wie SQL Management Studio ist nicht erforderlich. Sie müssen dieselbe Installationsquelle verwenden wie für die Installation der SQL Server-Vollversion, beispielsweise eine Daten-DVD. (Verwenden Sie auf keinen Fall die separaten, eigenständigen Versionen der Clientkomponenten. Der SQL-WMI-Anbieter ist in diesen Versionen nicht enthalten.) Entscheiden Sie sich für eine benutzerdefinierte Installation, und installieren Sie lediglich die Clientkomponenten. 
  
    
    


## <a name="functions-performed-by-the-spf-vss-writer"></a>Von SPF-VSS Writer ausgeführte Funktionen

Vom SPF VSS Writer werden die folgenden Funktionen ausgeführt:
  
    
    

1. Erstellt SharePoint Foundation-Komponenten.
    
  - Generiert eine vollständige Liste aller Komponenten in der SharePoint Foundation-Farm.
    
  
  - Er muss nicht an den Sicherungsprozess oder Wiederherstellungsprozess gebunden sein.
    
  

  ![SharePoint und Volumeschattenkopie-Dienst](../images/99376713-6a54-4d88-9b05-068578169506.gif)
  

  

  
2. Sichert Farm oder Datenbank.
    
  - Fordert eine SharePoint Foundation-Sicherung (Farm/Datenbank) über VSS an.
    
  

  ![SharePoint und Volumeschattenkopie-Dienst](../images/97765b6d-51e9-4d07-8b5d-3e93c0508b16.gif)
  

  

  
3. Stellt eine Farm oder Datenbank wieder her.
    
  - Fordert eine SharePoint Foundation-Wiederherstellung (Farm/Datenbank) über VSS an.
    
  
  - Implementiert **postRestore()** zum Synchronisieren von Websitetabellen.
    
  

  ![SharePoint und Volumeschattenkopie-Dienst](../images/b86ecdb8-88a7-4407-af86-07d2442235dc.gif)
  

  

  

## <a name="next-steps"></a>Nächste Schritte
<a name="Next"> </a>

Erfahren Sie, wie erstellen und Verwenden eines VSS-Requestors für SharePoint:
  
    
    

-  [VSS-Anforderer und SharePoint](vss-requestors-and-sharepoint.md)
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Übersicht über SharePoint und der Volumeschattenkopie-Dienst](overview-of-sharepoint-and-the-volume-shadow-copy-service.md)
    
  

