---
title: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7d416f6e-2471-4d03-97ae-4e8d907784c6
ms.openlocfilehash: 7b86188fe330436d271cd4568dd161bb000e85c5
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="map-a-network-drive-to-the-sharepoint-master-page-gallery"></a>Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog

In diesem Artikel erfahren Sie, wie Sie dem Gestaltungsvorlagenkatalog ein Netzlaufwerk zuordnen, damit Sie den Entwurfs-Manager zum Hochladen von Designdateien in SharePoint verwenden können.
Sie können mithilfe eines beliebigen Webdesigntools oder HTML-Editors ein visuelles Design für Ihre Website erstellen und dieses Design dann mit dem Entwurfs-Manager in SharePoint importieren. Zu diesem Zweck müssen Sie sicherstellen, dass das Designtool seine Dateien im Gestaltungsvorlagenkatalog Ihrer Website speichert; dies ist der Ort, an dem SharePoint die Dateien zu finden erwartet. Es wird empfohlen, dem Gestaltungsvorlagenkatalog ein Netzlaufwerk zuzuordnen, um das Speichern von Dateien am richtigen Speicherort zu vereinfachen.
  
    
    

Ermitteln Sie zunächst den Speicherort des Gestaltungsvorlagenkatalogs.
### <a name="to-find-the-location-of-the-master-page-gallery"></a>So suchen Sie den Speicherort des Gestaltungsvorlagenkatalogs


1. Starten Sie den Entwurfs-Manager auf der Website, für die Sie ein Design erstellen. (Wählen Sie z. B. im Menü **Einstellungen** die Option **Entwurfs-Manager** aus.)
    
    > **Wichtig:** Wenn Ihre Website in SharePoint Online gehostet wird, vergewissern Sie sich, dass Sie beim Anmelden bei der Website mit Ihren Office 365-Anmeldeinformationen das Kontrollkästchen **Angemeldet bleiben** aktivieren. Weitere Informationen finden Sie im Artikel zur [Konfiguration und Problembehandlung von zugeordneten Laufwerken, die eine Verbindung mit SharePoint Online-Websites in Office 365 für Unternehmen herstellen](http://support.microsoft.com/kb/2616712). 
2. Wählen Sie in der nummerierten Liste den Eintrag **Designdateien hochladen** aus.
    
  
3. Die Seite "Entwurfs-Manager: Designdateien hochladen" enthält den Speicherort des Gestaltungsvorlagenkatalogs. Der Speicherort endet vermutlich mit  `/_catalogs/masterpage/`. Dies ist der Speicherort, dem Sie ein Netzlaufwerk zuordnen.
    
  
4. Notieren Sie sich den Speicherort des Gestaltungsvorlagenkatalogs, oder kopieren Sie ihn in die Zwischenablage.
    
  
Ordnen Sie auf dem Computer, auf dem das Designtool oder der HTML-Editor ausgeführt wird, dem soeben kopierten Speicherort ein Netzlaufwerk zu. Das Verfahren zum Zuordnen von Netzwerklaufwerken unterscheidet sich je nach Betriebssystem des Computers:
- Führen Sie für einen Computer unter Windows 8 die Schritte aus, die in der Windows 8-Version des Artikels  [Erstellen einer Verknüpfung (Zuordnung) mit einem Netzlaufwerk](http://windows.microsoft.com/de-DE/windows-8/create-shortcut-to-map-network-drive) beschrieben werden.
    
  
- Führen Sie für einen Computer unter Windows 7 die Schritte aus, die in der Windows 7-Version des Artikels  [Erstellen einer Verknüpfung (Zuordnung) mit einem Netzlaufwerk](http://windows.microsoft.com/de-DE/windows7/Create-a-shortcut-to-map-a-network-drive) beschrieben werden.
    
  
- Führen Sie für einen Computer unter Windows Vista die Schritte aus, die in der -Version des Artikels  [Erstellen einer Verknüpfung (Zuordnung) mit einem Netzlaufwerk](http://windows.microsoft.com/de-DE/windows-vista/Create-a-shortcut-to-map-a-network-drive) beschrieben werden.
    
  
- Führen Sie auf einem Computer unter Windows XP die im Artikel  [Verbinden und Trennen eines Netzlaufwerks in Windows XP](http://support.microsoft.com/kb/308582) beschriebenen Schritte aus.
    
  
- ***Wenn auf dem Computer ein anderes Betriebssystem ausgeführt wird, führen Sie die Schritte zum Erstellen einer Verknüpfung mit einem neuen Speicherort für dieses Betriebssystem aus.*** Möglicherweise müssen Sie für die Verbindung mit der SharePoint-Website andere Anmeldeinformationen bereitstellen und angeben, dass die Verbindung bei jeder Anmeldung beim Computer erneut hergestellt werden soll.
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Vorgehensweise: Anwenden einer Gestaltungsvorlage auf eine Website in SharePoint](how-to-apply-a-master-page-to-a-site-in-sharepoint.md)
    
  
-  [Entwickeln des Website-Designs in SharePoint](develop-the-site-design-in-sharepoint.md)
    
  
-  [SharePoint-Design-Manager-Gerätekanäle](sharepoint-design-manager-device-channels.md)
    
  
-  [Vorgehensweise: ändern die Vorschauseite in SharePoint-Design-Manager](how-to-change-the-preview-page-in-sharepoint-design-manager.md)
    
  
-  [SharePoint Design Manager - Bilddarstellungen](sharepoint-design-manager-image-renditions.md)
    
  

