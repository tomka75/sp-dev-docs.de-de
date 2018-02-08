---
title: Aktualisieren von Remotekomponenten in SharePoint-Add-Ins
description: Aktualisieren Sie die Remotewebanwendungen und -datenbanken in einem SharePoint-Add-In.
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: c8d74f691253b882846411d671ac808f67bcd057
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="update-remote-components-in-sharepoint-add-ins"></a>Aktualisieren von Remotekomponenten in SharePoint-Add-Ins

Machen Sie sich vor Beginn mit dem Thema [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins.md) und den darin aufgeführten erforderlichen Komponenten und Kernkonzepten vertraut.

Aufgrund der großen Unterschiede bei Plattformen und Mandantensystemen können zur Aktualisierung der Remotekomponenten größtenteils nur sehr allgemeine Hinweise gegeben werden. Im folgende Abschnitt finden Sie einige Richtlinien.

Für ein vom Anbieter gehostetes SharePoint-Add-In aktualisieren Sie die Remotekomponenten mit der bewährten Aktualisierungsmethode der Plattform, auf der die Komponenten gehostet werden. Ebenso wie die Remotekomponenten eines vom Anbieter gehosteten Add-Ins separat von der Installation des SharePoint-Add-Ins installiert werden, werden sie auch separat aktualisiert. Überlegungen:

- Die aktualisierten Remotekomponenten sollten weiterhin mit allen früheren Versionen des SharePoint-Add-Ins verwendet werden können.

- Wenn Sie für Ihre Remotekomponenten ein Mandantenisolationssystem implementiert haben, beachten Sie, dass unterschiedliche Mandanten möglicherweise mehrere Versionen Ihrer App verwenden. Außerdem können auf einem bestimmten Mandanten auf verschiedenen SharePoint-Websites sogar unterschiedliche Versionen installiert sein.

Für ein vom Anbieter gehostetes SharePoint-Add-In, das Microsoft Azure SQL-Datenbank oder SQL Server verwendet, gibt es mehrere Methoden zum Aktualisieren der Datenbank. Lesen Sie zum Einstieg [Upgraden einer Datenschichtanwendung](http://msdn.microsoft.com/library/c117df94-f02b-403f-9383-ec5b3ac3763c.aspx).

## <a name="next-steps"></a>Nächste Schritte

Kehren Sie zu [Wichtige Schritte beim Aktualisieren eines Add-Ins](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) zurück, oder rufen Sie direkt einen der folgenden Artikel auf, um zu erfahren, wie Sie die nächste Hauptkomponente Ihres SharePoint-Add-Ins aktualisieren.

-  [Aktualisieren von Add-In-Webkomponenten in SharePoint](update-add-in-web-components-in-sharepoint.md)
-  [Aktualisieren von Hostwebkomponenten in SharePoint](update-host-web-components-in-sharepoint.md)
-  [Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md)

## <a name="see-also"></a>Siehe auch

-  [Aktualisieren von Add-Ins für SharePoint](update-sharepoint-add-ins.md)
-  [Aktualisierungsverfahren für SharePoint-Add-Ins](sharepoint-add-ins-update-process.md) 
    
 

