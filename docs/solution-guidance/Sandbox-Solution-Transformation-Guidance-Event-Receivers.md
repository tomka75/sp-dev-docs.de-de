---
title: "Sandkasten-Transformation ausgesprochen - Ereignisempfänger"
ms.date: 11/03/2017
ms.openlocfilehash: 1e49fa9b9afdb06eb9ea4ec09a866eccf703cbf7
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="sandbox-solution-transformation-guidance---event-receivers"></a>Sandkasten-Transformation ausgesprochen - Ereignisempfänger 
In diesem Artikel helfen Ihnen, um Optionen und Strategien zum Austauschen von vorhandenen Ereignisempfänger aus Ihrer sandkastenlösungen zu identifizieren.

_**Gilt für:** Add-ins für SharePoint | SharePoint 2013 | SharePoint-2016 | SharePoint Online_

Sandkasten codebasierte Lösungen [als veraltet gekennzeichnet wurden](https://blogs.msdn.microsoft.com/sharepointdev/2014/01/14/deprecation-of-custom-code-in-sandboxed-solutions/) , wieder in 2014 und SharePoint online gestartet Upgradeprozess für diese Funktion vollständig zu entfernen. Codebasierte sandkastenlösungen sind auch in SharePoint 2013 und SharePoint 2016 veraltet.

## <a name="summary"></a>Summary

Ansatz verwenden Sie zum Verarbeiten von Ereignissen in SharePoint unterscheidet sich etwas in der SharePoint-add-in-Objektmodell mit vollständigen vertrauen Code oder in der codierten sandkastenlösungen war. In früheren Lösungen typisch wurden Ereignisempfänger mithilfe der SharePoint Server-Side Object Model erstellt und bereitgestellt über Lösungspakete, die den Code auf der SharePoint-Servern ausgeführt wird. In der SharePoint-add-in-Modell; jedoch die Implementierung von Ereignissen Receiver ausgeführt wird, auf dem Webserver, der den Ereignisempfänger hostet, und diese werden Remote Event Receivers (RER) bezeichnet. Ereignisempfänger können in vielen Fällen durch eine remote-Ereignisempfänger implementiert ersetzt werden. In diesem Artikel werden die verschiedenen Optionen und Design Considerations.


## <a name="options-for-replacing-event-receivers"></a>Optionen für den Austausch von Ereignisempfängern
<a name="sectionSection2"> </a>

|**Ansatz**|**Weitere Informationen**|
|:-----|:-----|
|Remote-Ereignisempfänger|</p><lu><li>[Verwenden von remote-Ereignisempfänger in SharePoint](https://msdn.microsoft.com/en-us/pnp_articles/use-remote-event-receivers-in-sharepoint)</li><li>[Verwendung von remote-Ereignisempfänger für Ihre SharePoint-add-ins](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-use-remote-event-receivers-for-your-SharePoint-add-ins)</li><li>[Ereignisempfänger und Liste-Ereignisempfänger in der SharePoint-add-in-Objektmodell](https://msdn.microsoft.com/en-us/pnp_articles/event-receiver-and-list-event-receiver-sharepoint-add-in)</li></lu><li>[Automatisches Markieren von Beispiel-add-in für SharePoint](https://msdn.microsoft.com/en-us/pnp_articles/autotagging-sample-app-for-sharepoint)</li><li>[Behandeln von Ereignissen in SharePoint-Add-Ins](https://msdn.microsoft.com/en-us/library/office/jj220048.aspx)</li></lu></p>|
|WebHooks|<p>WebHooks für SharePoint sind noch in der Entwicklung und wird bald für Preview verfügbar sein.<lu><li>[Einführung in SharePoint WebHooks](http://dev.office.com/blogs/introducing-sharepoint-webhooks)</li></p>
|Remote Zeitgeberauftrag zum Überwachen von Änderungen|<p>Verwenden Sie das **komplexer ChangeQuery** -Objekt zum Überwachen von einer Website oder Liste, um diesen zu ändern. Dieses Muster ist eine Alternative zum Remote-Ereignisempfänger<lu><li>[SharePoint-Liste Element Änderungs-Monitor](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ListItemChangeMonitor)</li><li>[Remote Timer-Job-Muster](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)</p>|

## <a name="design-considerations"></a>Entwurfsaspekte
### <a name="remote-event-receivers"></a>Remote-Ereignisempfänger
- Erfordert Hostinginfrastruktur ab
- Hosting-Infrastruktur muss hoch verfügbar sein.
- Der Dienstendpunkt, der den remote-Ereignisempfänger hostet, muss für die anonyme Authentifizierung konfiguriert werden
- Erfordert eine vertrauenswürdige 3. Partei Zertifikat, wenn Sie SharePoint Online nutzen
- Nicht vorgesehen für Long Vorgänge ausführen 
- Remote-Ereignisempfänger, die angefügt werden Seite ausgehende im Kontext des add-Ins, angefügte mit einer Konsolenanwendung oder mit PowerShell; erhält ein Kontexttoken SharePoint beim Aufrufen nicht und Sie müssen nur-app-Berechtigungen abweichen oder verwenden Sie die SharePointOnlineCredentials-Klasse
- Es ist kein Mechanismus "Wiederholen" 

### <a name="webhooks"></a>WebHooks
- Erfordert Hostinginfrastruktur ab
- Hosting-Infrastruktur muss hoch verfügbar sein.
- Synchrone Ereignisse werden nicht unterstützt.
- Prozess geändert wird, nachdem das Ereignis eingetreten ist
- Öffentliche Vorschau in Sommer 2016 verfügbar für SharePoint Online
- Zu diesem Zeitpunkt erstellt in SharePoint lokal nicht verfügbar.

### <a name="remote-timer-job"></a>Remote-Zeitgeberauftrag
- Erfordert Hostinginfrastruktur ab
- Prozess geändert wird, nachdem das Ereignis eingetreten ist
- Verwendet einen Abrufmechanismus zum Verarbeiten von Änderungen

## <a name="removing-your-sandbox-code-from-your-site"></a>Entfernen des Sandkasten-Codes aus Ihrer Website
<a name="sectionSection3"></a>Wenn Sie Ihre vorhandenen Sandkasten-Lösung aus Ihrer Websites deaktivieren, alle Elemente oder Dateien, die mithilfe von deklarativer Optionen bereitgestellt werden nicht jedoch entfernt werden, die Features in der Sandkasten-Projektmappe werden automatisch deaktiviert und das Ereignis Receiver(s) entfernt werden . 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>
-  [Entfernen codebasierte Sandkastenlösungen in SharePoint Online](http://dev.office.com/blogs/removing-code-based-sandbox-solutions-in-sharepoint-online)
-  [Hilfestellung zur Transformation von Sandkastenlösungen](https://msdn.microsoft.com/en-us/pnp_articles/sandbox-solution-transformation-guidance)
-  [Entfernen Sie Assemblyverweis aus der Sandkasten-Lösung in Visual Studio erstellten](https://support.microsoft.com/en-us/kb/3183084)
-  [Erstellen von Add-Ins für SharePoint](https://msdn.microsoft.com/library/office/fp179930.aspx)
-  [Office 365-Entwicklung und SharePoint Mustern und Methoden ausgesprochen](https://msdn.microsoft.com/en-us/pnp_articles/office-365-development-patterns-and-practices-solution-guidance)
