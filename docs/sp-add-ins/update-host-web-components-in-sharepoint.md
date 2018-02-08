---
title: Aktualisieren von SharePoint-Hostwebkomponenten
description: Aktualisieren Sie benutzerdefinierte Aktionen und Add-In-Webparts im Hostweb eines SharePoint-Add-Ins.
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 88396b03d4c45385c866947388fadc71966ff815
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="update-host-web-components-in-sharepoint"></a>Aktualisieren von Hostwebkomponenten in SharePoint

Machen Sie sich vor Beginn mit dem Thema [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins.md) und den darin aufgeführten erforderlichen Komponenten und Kernkonzepten vertraut.

Das Add-In kann zwei Arten von Komponenten in einem Hostweb mit aussagekräftigem Markup in der SharePoint-Add-In installieren: **benutzerdefinierte Aktionen** und **Add-In-Webparts**. Die Aktualisierung dieser Komponenten ist im Hostweb einfacher als im Add-In-Web. Es wird keine Aktualisierungssemantik benötigt. Ändern Sie einfach die benutzerdefinierten Aktionen und Add-In-Webparts oder fügen Sie diese neu hinzu. Wenn das SharePoint-Add-In aktualisiert wurde, wendet SharePoint immer alle neuen Elementmanifestdateien an und wendet alle geänderten Elementmanifestdateien mit der neuesten Version erneut an. Bei erneuter Anwendung wird kein Schaden angerichtet; zum Beispiel wird eine Menüband-Schaltfläche für eine benutzerdefinierte Aktion nicht mehrmals zu dem Menüband hinzugefügt.

Wenn Sie ein App-Webpart aktualisieren, ersetzt SharePoint die alte Version durch die neue Version im Webpartkatalog. Achten Sie darauf, die Eigenschaft **Name** des **ClientWebPart**-Objekts zu ändern, wenn Sie ein App-Webpart aktualisieren. Dies gewährleistet beim Aktualisieren der App, dass SharePoint die alte Version des App-Webparts (diese ist nicht mehr Teil der App) von allen Seiten entfernt, zu denen sie hinzugefügt wurde. Die Benutzer müssen die neue Version erneut zu den Seiten hinzufügen.

Wenn Sie die Eigenschaft **Name** unverändert lassen, bleibt die alte Version auf den Seiten, zu denen Sie hinzugefügt wurde. Dadurch ist es unwahrscheinlich, dass die Benutzer bemerken, dass eine neue Version des Add-In-Webparts verfügbar ist. Außerdem wird beim Hinzufügen des Add-In-Webparts zu einer Seite die neue Version verwendet. Dadurch hätte eine Version eines SharePoint-Add-Ins unterschiedliche Add-In-Webparts auf unterschiedlichen Seiten.

Sie können programmgesteuert andere Arten von Hostweb-Komponenten bereitstellen, indem Sie einen mit einem [InstalledEventEndpoint](http://msdn.microsoft.com/library/af9f83d8-8325-3ede-d7b0-bb82c0445eb9%28Office.15%29.aspx)-Element im Add-In-Manifest registrierten Remoteereignisempfänger verwenden. Sie sollten einen [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx)-Empfänger verwenden, um Komponenten zu aktualisieren, die ursprünglich mit einem **InstalledEventEndpoint**-Empfänger bereitgestellt wurden. Eine Beschreibung der [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx)-Empfänger finden Sie unter [Erstellen eines Handlers für das Aktualisierungsereignis in SharePoint-Add-Ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md).

## <a name="next-steps"></a>Nächste Schritte
<a name="Next"> </a>

Wechseln Sie zu [Wichtige Schritte beim Aktualisieren eines Add-Ins](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) oder rufen Sie direkt einen der folgenden Artikel auf, um zu erfahren, wie Sie die nächste Hauptkomponente Ihres SharePoint-Add-Ins aktualisieren.

-  [Aktualisieren von Add-In-Webkomponenten in SharePoint](update-add-in-web-components-in-sharepoint.md)
-  [Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md)
-  [Aktualisieren von Remotekomponenten in SharePoint-Add-Ins](update-remote-components-in-sharepoint-add-ins.md)
 
## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins.md)
-  [Hostwebs, Add-In-Webs und SharePoint-Komponenten in SharePoint 2013](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md) 
    
 

