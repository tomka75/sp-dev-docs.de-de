---
title: "Ereignisempfänger und Liste-Ereignisempfänger in der SharePoint-add-in-Objektmodell"
ms.date: 11/03/2017
ms.openlocfilehash: db3b316f7505805a1d8237477056419535cea89c
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="event-receivers-and-list-event-receivers-in-the-sharepoint-add-in-model"></a>Ereignisempfänger und Liste-Ereignisempfänger in der SharePoint-add-in-Objektmodell
=======================================================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Verarbeiten von Ereignissen in SharePoint unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.  
In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario Ereignisempfänger und Ereignisempfänger Liste mit den SharePoint Server-Side Object Model Code erstellt und über Lösungen bereitgestellt wurden.  In diesem Szenario wird der Ereignisempfängercode auf dem SharePoint-Server ausgeführt.

In einem Modell Szenario SharePoint-Add-in sind mit SharePoint-Ereignisempfänger in einem Webdienst außerhalb von SharePoint erstellt und registriert.  
Diese werden als *Remote Ereignis Recivers (RER)*bezeichnet. In diesem Szenario führt der Ereignisempfängercode auf dem Webserver, auf dem der Webdienst gehostet wird.

>**Wichtige** Ab Januar 2017 SharePoint Online unterstützt Liste Webhooks, die Sie, anstatt verwenden können "-Ed" remote-Ereignisempfänger. Checkout- [Übersicht von SharePoint-Webhooks](https://dev.office.com/sharepoint/docs/apis/webhooks/overview-sharepoint-webhooks) erfahren Sie mehr über Webhooks. Beachten Sie außerdem, dass mehrere Webhook Beispiele aus GitHub Repository [sp-Dev-Beispiele](https://github.com/SharePoint/sp-dev-samples/tree/master/Samples) verfügbar sind.

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien für die Erstellung von Ereignisempfängern bereitstellen.

- Die Dienst-Endpunkt, die einen Ereignisempfänger implementiert wird, muss durch anonyme Benutzer zugreifen können.
- Ereignisempfänger hinzugefügt, mit dem Web-Add-in können Sie ein Zugriffstoken zurückzugeben.
- Ereignisempfänger hinzugefügt, mit der Hostwebsite Zugriffstoken wird zurückgegeben, wenn sie von app-Zugriffstoken und einen optimalen Betrieb im hostweb mit app-Kontext angewendet werden Endbenutzer gesteuerte (ItemAdded usw.)
- AppInstalled Ereignis muss innerhalb von 30 Sekunden abgeschlossen ist, oder SharePoint werden könnte ein Fehler aufgetreten ist. SharePoint wird das Ereignis erneut ausführen, 3 Mal und nach der vierten Ausführung SharePoint-add-in-Installation vor, in Betracht kommt
- Normale Ereignisse wie ItemAdded haben auch Timeout von 30 Sekunden, aber es ist kein Mechanismus "Wiederholen"
- Ereignisempfänger hinzugefügt, ohne die app-Kontext, beispielsweise mit SharePointOnlineCredentials oder auf andere Weise Host-Web nicht Zugriffstoken zurück, und Sie müssen auf der Hostwebsite mit nur-app-Zugriffstoken zugreifen
- Hinzufügen von Ereignisempfängern mit der Hostwebsite wird unterstützt.
    + Es ist nur über CSOM/REST-APIs nicht mithilfe von Visual Studio-Assistenten verwenden.
- SharePoint wird das Ereignis absolut Receiver-Endpunkte für ein bestimmtes Ereignis konfiguriert aufrufen.  Es ist jedoch keine Garantie dafür gibt, die der Code in die Event Receiver-Endpunkte ausgeführt wird, da der Code nicht auf dem SharePoint-Server ausgeführt wird.
    
    Beispiel:
    
    Wenn die Ereignis Receiver-Endpunkt-URL nicht verfügbar ist, wird der Ereignisempfängercode nicht ausgeführt.  Die URL, möglicherweise aufgrund aus verschiedenen Gründen nicht verfügbar.  Die häufigsten Ursachen gehören ein Konfigurationsfehlers beim Beenden der Endpunkt URL registriert ist, DNS-Probleme beim Versuch, die URL oder die Website Hosten der Endpunkt aufzulösen ausgefallen oder nicht mehr Zustand befindet.

    Darüber hinaus befindet sich ein Fehler in schlecht geschriebenen Ereignisempfängercode gibt es keine Möglichkeit, SharePoint benachrichtigen der Fehler aufgetreten ist und das Ereignis erneut ausgeführt werden soll.  Sie können dies zu einem gewissen Grad mit Ereignisempfängern zu SharePoint-Listen angefügt umgehen.  Weitere Informationen zu diesem Verfahren finden Sie weiter unten.  
- Wenn ein Ereignisempfängers sehr viel Code ausgeführt wird, sollte ein asynchrones Muster verwendet werden.
    + Finden Sie im MSDN Blogbeitrag für Weitere Informationen zu diesem Muster. [Verwenden von Azure-Speicher Warteschlangen und WebJobs für Async Aktionen in Office 365 (MSDN-Blog-Beitrag)](http://blogs.msdn.com/b/vesku/archive/2015/03/02/using-azure-storage-queues-and-webjobs-for-async-actions-in-office-365.aspx)
    + Finden Sie unter den folgenden MSDN-Artikel Weitere Informationen zu Timeouts in Ereignisempfängern.  (Suche nach Timeout im Artikel).  [Behandeln von Ereignissen in add-ins für SharePoint (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/office/jj220048.aspx)
- Beim Verwenden von Ereignisempfängern auf SharePoint-Listen wird empfohlen, eine bestimmte Versionsvergleich-Mechanismus zusammen mit den Ereignisempfänger verwenden, um höhere Qualität Verarbeitung sicherzustellen.
    + Finden Sie unter der folgenden O365 Plug & Play-Codebeispiel für Weitere Informationen zu diesem Muster und wie Sie sie implementieren.  [Core.ListItemChangeMonitor (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ListItemChangeMonitor)


<a name="debugging-event-receivers"></a>Debuggen von Ereignisempfängern
-------------------------
Ereignisempfänger Debuggen, die Sie verschiedene Funktionen in Azure und Visual Studio zu konfigurieren müssen.  Die folgenden Artikel enthalten schrittweise Anleitungen und Weitere Informationen zum Debuggen. 
- [Debuggen Sie und Problembehandlung bei einer remote-Ereignisempfänger in einem Add-in für SharePoint MSDN-Blog-Beitrag)](https://msdn.microsoft.com/en-us/library/office/dn275975.aspx) 
- [Debuggen von Remote-Ereignisempfänger mit Visual Studio (MSDN-Blog-Beitrag)](http://blogs.msdn.com/b/officeapps/archive/2013/01/03/debugging-remote-event-receivers-with-visual-studio.aspx)
- [Aktualisieren Sie auf Debuggen von remoteereignissen von SharePoint 2013 mit Visual Studio 2012 (MSDN-Blog-Beitrag)](http://blogs.msdn.com/b/officeapps/archive/2013/03/21/update-to-debugging-sharepoint-2013-remote-events-using-visual-studio-2012.aspx)
- [Erstellen und Debuggen von Remote-Ereignisempfänger "Installer Apps" in SharePoint Online (Scott Hillier)](http://www.itunity.com/article/create-debug-remote-event-receiver-installer-apps-sharepoint-online-775)

<a name="more-examples"></a>Weitere Beispiele
-------------
- [Core.EventReceivers (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers)
    + Dieses Beispiel zeigt wie ein SharePoint-Add-in können das App installiert Ereignis zusätzliche Arbeiten im hostweb, wie beispielsweise Anfügen von Ereignisempfängern zu Listen auf der Hostwebsite ausführen.
    + Finden Sie im MSDN Blogbeitrag für Weitere Informationen zu diesem Muster. [Anfügen von Remote-Ereignisempfänger zu Listen auf der Hostwebsite (MSDN-Blog-Beitrag)](http://blogs.msdn.com/b/kaevans/archive/2014/02/26/attaching-remote-event-receivers-to-lists-in-the-host-web.aspx)
- [Core.AppEvents.HandlerDelegation (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents.HandlerDelegation)
    + Dieses Beispiel zeigt, wie Ereignishandler für das AppInstalled und AppUninstalling implementieren, die:
        1. Integrieren Sie Rollback-Logik, wenn der Ereignishandler ein Fehler auftritt.
        2. Integrieren Sie Logik "bereits getan", um die Tatsache berücksichtigen, dass SharePoint dem Handler bis zu drei Mal erneut versucht, wenn es treten Fehler auf oder mehr als 30 Sekunden dauert.
        3. Verwenden Sie die Ereignishandler Delegierung Strategie, um Anrufe vom Webdienst Handler für SharePoint zu minimieren.
        4. Verwenden Sie CSOM-Klassen ExceptionHandlingScope und ConditionalScope.
- [Core.AppEvents (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents)
    + Dieses Beispiel zeigt, wie Ereignishandler für das AppInstalled und AppUninstalling implementieren, die:
        1. Integrieren Sie Rollback-Logik, wenn der Ereignishandler ein Fehler auftritt.
        2. Integrieren Sie Logik "bereits getan", um die Tatsache berücksichtigen, dass SharePoint dem Handler bis zu drei Mal erneut versucht, wenn es treten Fehler auf oder mehr als 30 Sekunden dauert.

<a name="related-links"></a>Verwandte links
=============
- [Remoteereignisempfänger in SharePoint 2013 – häufig gestellte Fragen (MSDN-Artikel)](https://msdn.microsoft.com/EN-US/library/office/dn456315.aspx)
- [Erstellen Sie einen remote-Ereignisempfänger in-add-ins für SharePoint (MSDN-Artikel)](https://msdn.microsoft.com/EN-US/library/office/jj220043.aspx)
- [Erstellen eines app-Ereignisempfängers in SharePoint 2013 (MSDN-Artikel)](https://msdn.microsoft.com/EN-US/library/office/jj220052.aspx)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [Core.ListItemChangeMonitor (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ListItemChangeMonitor)
- [Core.EventReceivers (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers)
- [Core.AppEvents.HandlerDelegation (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents.HandlerDelegation)
- [Core.AppEvents (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents)
- Beispiele und Inhalte am https://github.com/SharePoint/PnP

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D) 
- SharePoint 2013 lokal
