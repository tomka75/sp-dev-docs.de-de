---
title: Aktualisieren von SharePoint-Hostwebkomponenten
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 24d1752c1618551b85fa63fbab7ef747a4873bc6
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="update-host-web-components-in-sharepoint"></a>Aktualisieren von SharePoint-Hostwebkomponenten
Aktualisieren von Add-In-Webparts und benutzerdefinierten Aktionen im Hostweb eines SharePoint-Add-Ins
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).
 


## <a name="prerequisites-for-updating-host-web-components"></a>Voraussetzungen für die Aktualisierung von Hostwebkomponenten
<a name="Prerequisites"> </a>

Kenntnisse des Themas [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins.md) und der darin aufgeführten erforderlichen Komponenten und Kernkonzepte.
 

 

## <a name="update-host-web-components"></a>Aktualisieren von Hostwebkomponenten
<a name="UpdateHostWeb"> </a>

Ihr Add-In kann zwei Arten von Komponenten auf einem Hostweb mit beschreibendem Markup im SharePoint-Add-In installieren: benutzerdefinierte Aktionen undAdd-In-Webparts. Das Aktualisieren dieser Komponenten ist im Hostweb einacher als im Add-In-Web. Sie müssen keine Semantik aktualisieren, fügen Sie einfach die benutzerdefinierten Aktionen und Add-In-Webparts hinzu bzw. ändern Sie diese. Wenn das SharePoint-Add-In aktualisiert wird, wendet SharePoint immer alle neuen Elementmanifestdateien an und wendet dann alle geänderten Elementmanifestdateien in ihrer aktuellen Version erneut an. Die erneute Anwendung verursacht keine Probleme; z. B wird eine Menübandschaltfläche für eine benutzerdefinierte Aktion nicht mehrfach zum Menüband hinzugefügt.
 

 
Wenn Sie ein Add-In-Webpart aktualisieren, ersetzt SharePoint die alte Version durch die neue Version im Webpartkatalog. Achten Sie darauf, die Eigenschaft **Name** des **ClientWebPart**-Objekts zu ändern, wenn Sie ein Add-In-Webpart aktualisieren. Dies gewährleistet beim Aktualisieren des Add-Ins, dass SharePoint die alte Version des Add-In-Webparts (diese ist nicht mehr Teil des Add-Ins) von allen Seiten entfernt, zu denen sie hinzugefügt wurde. Die Benutzer müssen die neue Version erneut zu den Seiten hinzufügen.
 

 
Wenn Sie die Eigenschaft **Name** unverändert lassen, bleibt die alte Version auf Seiten erhalten, denen sie hinzugefügt wurde. Dadurch ist es unwahrscheinlich, dass die Benutzer bemerken, dass eine neue Version des Add-In-Webparts verfügbar ist. Außerdem wird beim Hinzufügen des Add-In-Webparts zu einer Seite die neue Version verwendet. Dadurch hätte eine Version eines SharePoint-Add-Ins unterschiedliche Add-In-Webparts auf unterschiedlichen Seiten.
 

 
Sie können andere Hostwebkomponenten programmgesteuert bereitstellen, indem Sie einen Remoteereignisempfänger verwenden, den Sie im App-Manifest mit einem  [InstalledEventEndpoint](http://msdn.microsoft.com/library/af9f83d8-8325-3ede-d7b0-bb82c0445eb9%28Office.15%29.aspx)-Element registrieren. Sie sollten einen  [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx)-Empfänger verwenden, um Komponenten zu aktualisieren, die ursprünglich mit einem **InstalledEventEndpoint**-Empfänger bereitgestellt wurden. Weitere Informationen zu  [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx)-Empfängern finden Sie unter  [Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md).
 

 

## <a name="next-steps"></a>Nächste Schritte
<a name="Next"> </a>

Wechseln Sie zu  [Wichtige Schritte beim Aktualisieren eines Add-Ins](update-sharepoint-add-ins.md#MajorAppUpgradeSteps), oder rufen Sie direkt einen der folgenden Artikel auf, um zu erfahren, wie Sie die nächste Hauptkomponente Ihres SharePoint-Add-Ins aktualisieren.
 

 

-  [Aktualisieren von Add-In-Webkomponenten in SharePoint](update-add-in-web-components-in-sharepoint.md)
    
 
-  [Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md)
    
 
-  [Aktualisieren von Remotekomponenten in SharePoint-Add-Ins](update-remote-components-in-sharepoint-add-ins.md)
    
 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins.md)
    
 
-  [Hostwebs, Add-In-Webs und SharePoint-Komponenten in SharePoint 2013](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)
    
 

