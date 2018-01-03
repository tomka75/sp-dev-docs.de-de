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
# <a name="overview-of-sharepoint-and-the-volume-shadow-copy-service"></a>Übersicht über SharePoint und den Volumeschattenkopie-Dienst
 **Zusammenfassung:** Lernen Sie die Microsoft SharePoint -Schnittstelle zu Volume Shadow Copy Service (VSS). Für Sicherungsanbieter wird durch den Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) das Sichern von Microsoft-Serverlösungen mit einer zentralisierten API vereinfacht. Microsoft SharePoint Foundation enthält einen referenziellen VSS Writer (nachfolgend "SPF-VSS Writer" genannt), der in das Windows VSS-Sicherungsframework integriert ist. Dadurch wird das Sichern und Wiederherstellen von SharePoint Foundation-Daten durch Sicherungsanwendungen ermöglicht. Es wird ein Überschreibungsszenario mit schwerwiegenden Folgen für die gesamte Farm (einschließlich Suchindex) unterstützt. Bei der Wiederherstellung werden Datenbanken eingebunden und Websitezuordnungen synchronisiert.
  
    
    


## <a name="design-of-the-system"></a>Entwurf des Systems

Die folgende Abbildung zeigt die Hauptkomponenten des Systems: Microsoft Windows Server (und Volume Shadow Copy Service), SharePoint Foundation (und SPF-VSS-Writer für die Windows Server-Volume Shadow Copy Service) und Anwendung von Drittanbietern (oder benutzerdefinierte) Backup und Wiederherstellung (einschließlich der Anforderer und Anbieter).
  
    
    

  
    
    
![Beziehungen zwischen SharePoint und VSS](../images/77a290e8-e4aa-4c54-b1ec-3d74bf3962b6.gif)
  
    
    
Der VSS kommuniziert mit dem Windows Server-Dateisystem und der Massenspeicher-Gerätetreiber über einen Anbieter von Drittanbietern (oder benutzerdefinierte). Der Hardwareanbieter muss ermitteln, in dem die Schattenkopie erstellt wird. Der VSS abstrahiert die hardwarespezifischen Schattenkopie damit Sicherungs-bzw. Wiederherstellungsvorgang die Schattenkopie einheitlich zugreifen kann, ohne zu wissen, die Implementierungsdetails der Hardware. 
  
    
    
SharePoint Foundation Speicher ist eine Komponente des SharePoint Foundation und greift auf SharePoint Foundation Speichergruppen über das Dateisystem von Windows Server. Innerhalb des Dateisystems enthält jede Speichergruppe SharePoint Foundation Konfiguration, Inhalt, Suche Datenbanken und Datenbanken von Drittanbietern in die Konfiguration Datenbank und Indexdateien registriert. Ebenfalls enthalten sind Dienste auf den SharePoint Foundation Service Application Framework aufgebaut. 
  
    
    
Zur Unterstützung des VSS enthält SharePoint Foundation den SPF-VSS Writer. Der SPF-VSS Writer wird mit dem SharePoint Foundation-Speicher (der im Auftrag des Anforderers betrieben wird) koordiniert, um die Speichergruppe zu sperren und deren Bereitstellung aufzuheben, bevor sie gesichert wird. Nach Abschluss der Sicherung wird dann die Sperrung der Speichergruppe aufgehoben und die Speichergruppe bereitgestellt.
  
    
    
Während einer Wiederherstellung wird der SPF-VSS Writer von der Sicherungs-/Wiederherstellungsanwendung in Koordinierung mit dem SharePoint Foundation-Speicher (der im Auftrag des Anforderers betrieben wird) angewiesen, die Bereitstellung der Speichergruppe aufzuheben, die Datenbankdateien zu ersetzen und die Speichergruppe wieder bereitzustellen.
  
> [!NOTE]
> Wichtige Informationen zur Wiederherstellung finden Sie im Abschnitt „Wiederherstellen“ im Artikel [VSS-Anforderer und SharePoint](vss-requestors-and-sharepoint.md).
  
    
    

Als Anforderer wird eine Anwendung eines Drittanbieters (oder benutzerdefinierte Anwendung) bezeichnet, die den VSS zum ordnungsgemäßen Sichern und Wiederherstellen von SharePoint Foundation-Daten verwendet. Der Anforderer kommunizierte mit dem VSS, um Informationen zu SharePoint Foundation anzufordern, die Erstellung von Schattenkopien zu veranlassen und Zugriff auf die Daten für die Sicherung zu erhalten. 
  
    
    
Beim Wiederherstellen, kommuniziert des Anforderers auch mit den VSS So bereiten Sie die Wiederherstellung des Systems und zum Einfügen die Daten zurück auf das Massenspeichergerät. Die Sicherungs-bzw. Wiederherstellungsanwendung ist auch verantwortlich für die Arbeit mit Windows-Server zum Lesen und Schreiben von Daten in die backup-Datenträger, gibt an, ob ein Band zu archivieren, ein Storage Area Network oder andere Sicherungsmedien. 
  
    
    
Die Informationen, die zum erfolgreichen Ausführen von Sicherungs- und Wiederherstellungsvorgängen mit SharePoint Foundation, dem VSS und der Sicherungs-/Wiederherstellungsanwendung erforderlich sind, werden als Teil der SPF-VSS Writer-Metadaten übertragen.
  
    
    
Die Abfolge oberster Ebene von Ergebnissen während der Sicherungs- und Wiederherstellungsvorgänge lautet wie folgt:
  
    
    

  
    
    

1. Vom Sicherungsprogramm (oder Agent) wird ein geplanter Auftrag ausgeführt. 
    
  
2. Der VSS-Anforderer in der Sicherungs-/Wiederherstellungsanwendung sendet einen Befehl zum Erstellen einer Schattenkopie der ausgewählten SharePoint Foundation-Speichergruppen an den VSS. 
    
  
3. Der VSS kommuniziert mit dem SPF-VSS Writer, um eine Momentaufnahmensicherung vorzubereiten. SharePoint Foundation lässt Verwaltungsaktionen an der Speichergruppe nicht zu, überprüft Volumeabhängigkeiten und hält alle Schreibvorgänge in Datenbank- und Transaktionsprotokolldateien an, während Nur-Lese-Zugriff erteilt wird. 
    
  
4. Der VSS kommuniziert mit dem entsprechenden Speicheranbieter, damit eine Schattenkopie des Speichervolumes erstellt wird, das die SharePoint Foundation-Speichergruppe enthält. 
    
  
5. Der VSS gibt SharePoint Foundation frei, um die normalen Vorgänge fortzusetzen.
    
  
6. Der VSS-Anforderer überprüft die Integrität des Sicherungssatzes, bevor der Erfolg der Sicherung angezeigt wird. Die Zeit der letzten Datenbanksicherung wird von SharePoint Foundation erfasst.
    
  

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [SharePoint VSS Writer](sharepoint-vss-writer.md)
    
  
-  [VSS-Anforderer und SharePoint](vss-requestors-and-sharepoint.md)
    
  
-  [Vorgehensweise: Erstellen ein Volumenschattenkopie-Anforderers für die Verwendung mit SharePoint](how-to-create-a-vss-requestor-for-use-with-sharepoint.md)
    
  
-  [Vorgehensweise: Sichern und Wiederherstellen von SharePoint verwenden eines VSS-Requestors](how-to-back-up-and-restore-sharepoint-using-a-vss-requestor.md)
    
  
-  [Vorgehensweise: Sichern und Wiederherstellen eine Suchdienstanwendung in SharePoint mit VSS](how-to-back-up-and-restore-a-search-service-application-in-sharepoint-using.md)
    
  
-  [Starting and Configuring the WSS Writer Service]((http://msdn.microsoft.com/library/c9243dd6-e61e-4783-9fef-48d0122f1c09.aspx))
    
  
-  
  [Volumeschattenkopie-Dienst](http://msdn.microsoft.com/en-us/library/windows/desktop/bb968832%28v=vs.85%29.aspx)
    
  
-  
  [Volume Shadow Copy Service Technical Reference](http://msdn.microsoft.com/en-us/library/windows/desktop/aa384648%28v=vs.85%29.aspx)
    
  

