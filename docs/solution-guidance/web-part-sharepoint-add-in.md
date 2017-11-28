---
title: Webparts in SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 65e236df834b82d9649d2e43cd3dfef37ebdcdb4
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="web-part-in-the-sharepoint-add-in-model"></a>Webparts in SharePoint-add-in-Objektmodell
=======================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Erstellen von tragbaren Seitenkomponenten unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.  In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario-Webparts zum Implementieren der tragbaren Seitenkomponenten erstellt wurden.

In einem Szenario mit SharePoint-Add-Ins Modell werden Add-in-Webparts (App-Webparts) zum Implementieren der tragbaren Seitenkomponenten erstellt.  Add-in-Komponenten nutzen clientseitigem Code.

<a name="high-level-guidelines"></a>Hohe Stufe Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden high Level Richtlinien bezüglich-Add-in-Teile enthalten.

- Sie können nicht in Add-in-Webparts serverseitigen Code ausführen.
- Sie können nicht benutzerdefinierter EditorParts für Webparts-Add-in erstellen.
- Verwenden Sie das Webpart-Add-in-Skript mit JavaScript verknüpfen, die für die Interaktion mit SharePoint und andere Dienste und Erstellen einer Benutzeroberfläche verwendet wird.
- Standardmäßig werden benutzerdefinierte Eigenschaften, die Sie EditorParts hinzufügen immer als letzte Gruppe in einem Editor-Webpart angezeigt.
    + JavaScript können Sie um das Aussehen und Verhalten der ein Editor-Webpart für ein Webpart-Add-in zu überschreiben.
    + Finden Sie im folgende Beispiel wird veranschaulicht, wie Sie dies tun, die ein. 
    + [Core.AppPartPropertyUIOverride (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppPartPropertyUIOverride)

**Erste Schritte**

Add-in-Webparts können auf einfache Weise mithilfe von außerhalb der Feld-Add-in-Skript Teil erstellt werden.  Dadurch können Sie einen Link zu einer JavaScript-Datei an einer beliebigen Stelle gehostet bereitzustellen.  Die JavaScript-Datei wird clientseitigem Code für die Interaktion mit SharePoint oder andere Dienste und Rendern einer Benutzeroberfläche verwendet.

Im folgende Artikel wird beschrieben, das Add-in-Skript Teil Muster und dessen Verwendung.

- [Einführung in die app Skript Teil Muster für Office365 app-Modell (MSDN-Blog-Artikel)](http://blogs.msdn.com/b/vesku/archive/2014/07/08/introducing-app-script-part-pattern-for-office365-app-model.aspx)

Das folgende Beispiel veranschaulicht, wie Sie ein Webpart-Add-in-Skript verwenden, um mit Yammer, Bing Maps und Google Maps integrieren.

- [Core.AppScriptPart (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppScriptPart)

Das folgende Video führt Sie durch das Codebeispiel.

- [Core.AppScriptPart (O365 Plug & Play-Video)](https://channel9.msdn.com/Blogs/Office-365-Dev/App-Script-Parts-in-SharePoint-Office-365-Developer-Patterns-and-Practices)

<a name="related-links"></a>Verwandte links
=============

- [Einführung in die app Skript Teil Muster für Office365 app-Modell (MSDN-Blog-Artikel)](http://blogs.msdn.com/b/vesku/archive/2014/07/08/introducing-app-script-part-pattern-for-office365-app-model.aspx)
- [Core.AppScriptPart (O365 Plug & Play-Video)](https://channel9.msdn.com/Blogs/Office-365-Dev/App-Script-Parts-in-SharePoint-Office-365-Developer-Patterns-and-Practices)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [Core.AppPartPropertyUIOverride (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppPartPropertyUIOverride)
- [Core.AppScriptPart (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppScriptPart)
- Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D)
- SharePoint 2013 lokal
