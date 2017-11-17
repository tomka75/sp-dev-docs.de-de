---
title: Neuigkeiten in Access
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 625bc1d0-55db-4420-a02e-aee04028b215
ms.openlocfilehash: df9d6abbc550bf070968d479e5639c5f7fba08df
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-in-access"></a>Neuigkeiten in Access
Hier finden Sie Informationen zu den Features in Access 2013, welche die Erstellung, Bereitstellung und Verwaltung von webbasierten Anwendungen für die Zusammenarbeit lokal oder in der Cloud erleichtern.
## <a name="introduction"></a>Einführung
<a name="SP15_access15overview_Introduction"> </a>

Access 2013 verfügt über ein neues Anwendungsmodell, das für den Zweck entworfen wurde, die Webentwicklung ähnlich wie frühere Versionen von Access mit der Windows-Bereitstellung zu vereinfachen. Access 2013 ermöglicht Experten das schnelle Erstellen einer Anwendung, die zum Leiten ihres Unternehmens verwendet werden kann. Durch die Verwendung von Microsoft SharePoint zum Hosten des Front-Ends der App und von Microsoft SQL Server 2012 als die entsprechende Datenspeichertechnologie, verbessert Access 2013 die Verwaltbarkeit und Skalierbarkeit von Access-Anwendungen erheblich. Durch die Kompatibilität mit Office 365 und SQL Azure wird die Reichweite von Access-Anwendungen maßgeblich erweitert.
  
    
    

## <a name="architecture"></a>Architektur
<a name="SP15_access15overview_Architecture"> </a>

In einer lokalen Umgebung werden Access 2013-Apps durch SharePoint gehostet, während die Daten in SQL Server 2012 gespeichert werden. SharePoint stellt Authentifizierung, Autorisierung und Sicherheit für Access 2013-Apps bereit. Die Back-End-Tabellen, -Ansichten, -Makros und -Abfragen werden in einer SQL Server 2012-Datenbank gespeichert.
  
    
    
Access 2013 bietet über die Dienste Office 365 und SQL Azure eine Methode zur Bereitstellung einer Access-App in der Cloud.
  
    
    
In Abbildung 1 wird eine Übersicht der Access 2013-Architektur dargestellt.
  
    
    

**Abbildung 1. Access 2013-Architektur**

  
    
    

  
    
    
![Architektur von Access 2013](../images/odc_Office15_Access15OverviewDK2_Figure07.jpg)
  
    
    
Beim Erstellen einer neuen Access-Anwendung erstellt Access Services in SharePoint eine neue Anwendungsdatenbank, die die in der Anwendung enthaltenen Daten, Ansichten, Abfragen und Makros speichert. Die Access Services 2013 System-Datenbank kann so konfiguriert werden, dass neue Anwendungsdatenbanken auf einem separaten Server SQL Server 2012-Server erstellt werden.
  
    
    
Die Verwendung von SQL Server 2012 zum Speichern von Daten bietet eine zuvor in Access-Anwendungen nicht gekannte Verwaltbarkeit und Skalierbarkeit. Nun sind die Tage Geschichte, in denen eine Access-Anwendung neu entwickelt und in einer leistungsstärkeren Umgebung erneut implementiert werden müsste.
  
    
    
Eine Access 2013-App ist in dem Moment online, in dem sie entwickelt wird. Sie können die App für andere Benutzer freigeben, im privaten Unternehmenskatalog oder im Office Store bereitstellen.
  
    
    

## <a name="developing-access-apps"></a>Entwickeln von Access-Apps
<a name="SP15_access15overview_DevelopingAccessapps"> </a>

Im Gegensatz zu vielen der SharePoint-Anwendungsdienste macht Access Services 2013 keine API verfügbar, die Sie zum Entwickeln von Access-Apps in Visual Studio verwenden können. Access 2013 ist die Umgebung, die Sie zum Entwickeln von Access 2013-Apps verwenden.
  
    
    
Weitere Informationen zur Entwicklung von Access 2013-Apps finden Sie unter [Gewusst wie: Erstellen und Anpassen einer Web-App in Access](http://msdn.microsoft.com/library/628745f4-82e9-4838-9726-6f3e506a654f%28Office.15%29.aspx)
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15_access15overview_addres"> </a>


-  [Neuigkeiten in Access für Entwickler](http://msdn.microsoft.com/library/df778f51-d65e-4c30-b618-65003ceb39b3%28Office.15%29.aspx)
    
  
-  [Benutzerdefinierte Web-App-Referenz für Access](http://msdn.microsoft.com/library/8d696fa4-a6f2-4fb1-8662-a313bf0b5989%28Office.15%29.aspx)
    
  

