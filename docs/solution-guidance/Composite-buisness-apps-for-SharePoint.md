---
title: "Zusammengesetzte Geschäfts-apps für SharePoint 2013 und SharePoint Online"
ms.date: 11/03/2017
ms.openlocfilehash: 73bd4b9fd9d37cd72271cdce38320c8fdb3c67eb
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="composite-business-apps-for-sharepoint-2013-and-sharepoint-online"></a>Zusammengesetzte Geschäfts-apps für SharePoint 2013 und SharePoint Online

Zusammengesetzte Business-Apps für die Integration Ihrer SharePoint-Lösungen in Ihre Geschäftsprozesse und Technologien verwenden. Entscheiden Sie, ob eine SharePoint gehostet oder vom Anbieter gehosteten add-in für Ihre Lösung die richtige Wahl ist.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Zusammengesetzte Geschäfts-apps sind apps, die Ihre Geschäftsprozesse und Line-of-Business (LOB) Technologies (wie Datenbanken und Webdienste) eng integriert sind. Diese apps enthalten in der Regel eine Anzahl von komplexen Interaktionen mit Benutzern und mit anderen Technologien.
In diesem Abschnitt beschriebene Beispiel zusammengesetzte Business apps bieten Bausteine, die Sie verwenden können, um Ihre Technologien und Prozesse in SharePoint 2013-add-in-Modell zu integrieren.

## <a name="sharepoint-hosted-vs-provider-hosted-add-ins"></a>SharePoint-Hosting im Vergleich zu vom Anbieter gehosteten-add-ins
<a name="sectionSection0"> </a>

Bevor Sie zusammengesetzte Geschäfts-apps erstellen, müssen Sie zuerst entscheiden, wo die apps gehostet werden. SharePoint-Hosting-add-ins am besten, wenn Sie Ihren Anforderungen an einem Standort Implementierungen Bereich können, die Sie mit JavaScript behandeln können. Vom Anbieter gehosteten-add-ins sind besser für komplexere geschäftsanforderungen.

In der folgenden Tabelle werden die Faktoren zu berücksichtigen sind, wenn Sie entscheiden, wo Sie Ihre apps hosten zusammengefasst.

|**SharePoint-Hosting-add-ins**|**Vom Anbieter gehosteten-add-ins**|
|:-----|:-----|
|Alles möglich mit JavaScript benötigten.|Sie müssen anderen Sprachen als JavaScript verwenden.|
|Das Add-in muss sich nicht über mehr als einen Standort eine beliebige Arbeit leisten; Team Kalender-apps und empfohlene News Rotators.|Das Add-in muss Zugriff auf Informationen und über mehr als eine einzelne Website funktionieren. Bereitstellen von apps beispielsweise Websitesammlung.|
|Inhalt vertrauliche ist und sicher und vollständig in SharePoint bleiben muss.|Das Add-in muss mit anderen Line-of-Business-Technologien integriert werden soll.|
||Das Add-in erfordert erhöhte Berechtigungen, die durch die nur-app-Richtlinie vorgenommen werden.|
||Das Add-in erfordert eine stark angepasste Benutzeroberfläche.|

## <a name="in-this-section"></a>Inhalt dieses Abschnitts
<a name="sectionSection1"> </a>

|**Artikel**|**Beispiel**|**Zeigt, wie Sie auf...**|
|:-----|:-----|:-----|
|[Migrieren von InfoPath-Formularen in SharePoint 2013](Migrate-InfoPath-forms-to-SharePoint.md) ||Migrieren von InfoPath 2013-Formularen und anderen unterstützten Technologien.|
|[Datenspeicheroptionen in SharePoint Online](Data-storage-options-in-SharePoint-Online.md) |[Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) |Wird mit verschiedenen Arten von Speichermodellen zum Speichern Ihrer SharePoint Online-Daten.|
|[Unternehmens-Ereignis Add-in-Integration in SharePoint](Corporate-app-event-registration-with-SharePoint.md)|[BusinessApps.CorporateEventsApp](https://github.com/SharePoint/PnP/tree/master/Solutions/BusinessApps.CorporateEventsApp)|Verwenden Sie eine vom Anbieter gehosteten-add-in, um komplexe geschäftliche Aufgaben implementieren.|
|[Aufrufen von Webdiensten in SharePoint-workflows](Call-web-services-from-SharePoint-workflows.md)|<p>[Workflow.CallCustomService](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)</p><p>[Workflow.CallServiceUpdateSPViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)</p><p>[Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb)</p>|Verwenden Sie vom Anbieter gehostete apps remote-Webdienste aufrufen, die Geschäftsdaten enthalten.|

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [Office 365-Entwicklungsmuster und -übungen auf GitHub](https://github.com/SharePoint/PnP)
