---
title: Aktualisieren von Remotekomponenten in SharePoint-Add-Ins
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: a15890881bb4269ef21e5a2f22865509e9834750
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="update-remote-components-in-sharepoint-add-ins"></a>Aktualisieren von Remotekomponenten in SharePoint-Add-Ins
Aktualisieren Sie die Remotewebanwendungen und -datenbanken in einem SharePoint-Add-In.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).
 


## <a name="prerequisites-for-updating-the-remote-components-of-a-sharepoint-add-in"></a>Voraussetzungen für die Aktualisierung der Remotekomponenten eines SharePoint-Add-Ins
<a name="Prerequistes"> </a>

Kenntnisse des Themas [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins.md) und der darin aufgeführten erforderlichen Komponenten und Kernkonzepte.
 

 

## <a name="update-remote-components"></a>Aktualisieren von Remotekomponenten
<a name="UpdateRemote"> </a>

Aufgrund der großen Unterschiede bei Plattformen und Mandantensystemen können zur Aktualisierung der Remotekomponenten größtenteils nur sehr allgemeine Hinweise gegeben werden. Die folgenden zwei Abschnitte bieten eine Orientierung.
 

 

### <a name="update-remote-components-in-a-provider-hosted-add-in"></a>Aktualisieren von Remotekomponenten in einem von einem Anbieter gehosteten Add-In
<a name="UpdateProviderHosted"> </a>

Bei einem vom Anbieter gehosteten SharePoint-Add-In aktualisieren Sie die Remotekomponenten mithilfe der für Updates bewährten Vorgehensweisen der Plattform, auf der die Komponenten gehostet werden. Ebenso wie die Remotekomponenten eines vom Anbieter gehosteten Add-Ins separat von der Installation des SharePoint-Add-Ins selbst installiert werden, werden sie auch separat aktualisiert. Hier einige Punkte, die berücksichtigt werden sollten:
 

 

- Die aktualisierten Remotekomponenten sollten weiterhin mit allen früheren Versionen des SharePoint-Add-Ins verwendet werden können.
    
 
- Wenn Sie für Ihre Remotekomponenten ein Mandantenisolationssystem implementiert haben, beachten Sie, dass unterschiedliche Mandanten möglicherweise mehrere Versionen Ihrer App verwenden. Außerdem können auf einem bestimmten Mandanten auf verschiedenen SharePoint-Websites sogar unterschiedliche Versionen installiert sein.
    
 
Für ein vom Anbieter gehostetes SharePoint-Add-In, das Microsoft Azure SQL-Datenbank oder SQL Server verwendet, gibt es mehrere Methoden zum Aktualisieren der Datenbank. Lesen Sie zum Einstieg  [Upgrade a Data-tier Application](http://msdn.microsoft.com/library/c117df94-f02b-403f-9383-ec5b3ac3763c.aspx).
 

 

## <a name="next-steps"></a>Nächste Schritte
<a name="Next"> </a>

Kehren Sie zu  [Wichtige Schritte beim Aktualisieren eines Add-Ins](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) zurück, oder rufen Sie direkt einen der folgenden Artikel auf, um zu erfahren, wie Sie die nächste Hauptkomponente Ihres SharePoint-Add-Ins aktualisieren.
 

 

-  [Aktualisieren von Add-In-Webkomponenten in SharePoint](update-add-in-web-components-in-sharepoint.md)
    
 
-  [Aktualisieren von Hostwebkomponenten in SharePoint](update-host-web-components-in-sharepoint.md)
    
 
-  [Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md)
    
 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins.md)
    
 
-  [Aktualisierungsverfahren für SharePoint-Add-Ins](sharepoint-add-ins-update-process.md)
    
 

