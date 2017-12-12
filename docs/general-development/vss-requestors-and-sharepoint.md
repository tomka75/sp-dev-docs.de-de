---
title: VSS-Anforderer und SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 0b2e5a4e-40f0-4ccf-a21a-7274921f2169
ms.openlocfilehash: e33fbaaaed785786e6be0abca0d691748dc0798f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="vss-requestors-and-sharepoint"></a>VSS-Anforderer und SharePoint
 **Zusammenfassung:** Informieren Sie sich über die Funktionsweise des Requestors-Systems des Systems Gruppenrichtlinien-Verwaltungskonsole (Volume Shadow Copy Service, VSS) mit Microsoft SharePoint. VSS in Windows Server kann verwendet werden, um Anwendungen erstellen, die sichern und Wiederherstellen von Microsoft SharePoint Foundation. Der VSS stellt eine Infrastruktur, die Speicherlösung-Management-Programme, Business-Programme und Hardwareanbietern zusammenzuarbeiten erstellen und Verwalten von Schattenkopien können. Für diese Infrastruktur-basierte Lösungen können die Schatten Kopien (oder gespiegelte Kopien) zum Sichern und Wiederherstellen von Datenbanken für eine oder mehrere- SharePoint Foundation .
  
    
    


## <a name="vss-requestor-system"></a>VSS-Requestors system

Der VSS koordiniert die Kommunikation zwischen den Requestors (backup-Anwendungen), Autoren (Windows-Anwendungen wie SharePoint Foundation und Microsoft SQL Server) und Anbieter (System, Software oder Hardware Komponenten, die die Schattenkopien erstellen). Zum Sichern von SharePoint Foundationmithilfe des VSS-Features, muss das Sicherungsprogramm ein Volumenschattenkopie-Anforderers enthalten, das SharePoint Foundationkennt. Da das Sicherungsprogramm, das mit Windows Server bereitgestellt ist keine solche Requestors verfügt, müssen Organisationen Sicherung Anwendungen von Drittanbietern verwenden.
  
    
    
Im Hinblick auf die Kompatibilität mit SharePoint Foundation müssen bei auf VSS basierenden Sicherungsanwendungen zwei Basisvoraussetzungen erfüllt sein, damit die Integrität und Wiederherstellbarkeit von Schattenkopiesicherungen sichergestellt ist. Kunden sollten sich von ihren Sicherungsanbietern bestätigen lassen, dass die Sicherungsanwendung die in diesem Thema genannten Kompatibilitätsanforderungen für SharePoint Foundation erfüllt.
  
    
    
Die folgenden SharePoint Foundation-Anforderungen gelten für eine auf Schattenkopien basierende Sicherungsanwendung, um die Integrität und Wiederherstellbarkeit von SharePoint Foundation-Datenbanken sicherzustellen: 
  
    
    

- SharePoint Foundation-Datenbanken und Suchindexdateien dürfen ausschließlich über SPF-VSS Writer gesichert werden.
    
  
- Die Integrität des Schattenkopie-Sicherungssatzes muss von der Sicherungsanwendung überprüft werden. Wiederherstellungsvorgänge am ursprünglichen Speicherort dürfen ausschließlich mit SPF-VSS Writer ausgeführt werden.
    
  

## <a name="restoring"></a>Wiederherstellen

Für die Ausführung einer Wiederherstellung müssen die folgenden Bedingungen erfüllt sein:
  
    
    

- Die folgenden Dienste müssen  *gestartet*  sein:
    
  - SharePoint VSS Writer
    
  
  - Volumeschattenkopie
    
  
  - SharePoint-Ablaufverfolgung
    
  
- Die folgenden Dienste müssen  *beendet*  sein:
    
  - SharePoint-Verwaltung
    
  
  - SharePoint-Suche
    
  
  - SharePoint-Timer
    
  
  - SharePoint Server-Suche (wenn SharePoint Server installiert ist)
    
  
- Wenn die gesamte Farm wiederhergestellt wird, müssen SharePoint Foundation und die Internetinformationsdienste (Internet Information Services, IIS) heruntergefahren werden.
    
  
- Wenn nur ausgewählte Webanwendungen oder andere Komponenten wiederhergestellt werden, müssen die Webanwendungen heruntergefahren werden, und die Komponenten können während der Wiederherstellung nicht verwendet werden.
    
  

## <a name="next-steps"></a>Nächste Schritte
<a name="Next"> </a>

Erfahren Sie, wie erstellen und Verwenden eines VSS-Requestors für SharePoint:
  
    
    

-  [Vorgehensweise: Erstellen ein Volumenschattenkopie-Anforderers für die Verwendung mit SharePoint](how-to-create-a-vss-requestor-for-use-with-sharepoint.md)
    
  
-  [Vorgehensweise: Sichern und Wiederherstellen von SharePoint verwenden eines VSS-Requestors](how-to-back-up-and-restore-sharepoint-using-a-vss-requestor.md)
    
  
-  [Vorgehensweise: Sichern und Wiederherstellen eine Suchdienstanwendung in SharePoint mit VSS](how-to-back-up-and-restore-a-search-service-application-in-sharepoint-using.md)
    
  

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Übersicht über SharePoint und der Volumeschattenkopie-Dienst](overview-of-sharepoint-and-the-volume-shadow-copy-service.md)
    
  
-  [Vorgehensweise: Erstellen ein Volumenschattenkopie-Anforderers für die Verwendung mit SharePoint](how-to-create-a-vss-requestor-for-use-with-sharepoint.md)
    
  
-  [Vorgehensweise: Sichern und Wiederherstellen von SharePoint verwenden eines VSS-Requestors](how-to-back-up-and-restore-sharepoint-using-a-vss-requestor.md)
    
  
-  [Vorgehensweise: Sichern und Wiederherstellen eine Suchdienstanwendung in SharePoint mit VSS](how-to-back-up-and-restore-a-search-service-application-in-sharepoint-using.md)
    
  

