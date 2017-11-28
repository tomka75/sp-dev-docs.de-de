---
title: Benutzersteuerelemente und -Websteuerelemente in SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: cd1f3b127a7ae2eb1ac06e75f5a23c8f13563a8f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="user-controls-and-web-controls-in-the-sharepoint-add-in-model"></a>Benutzersteuerelemente und -Websteuerelemente in SharePoint-add-in-Objektmodell
=============================================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Implementieren von benutzerdefinierter Steuerelementen in Ihrem Code unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war. In einer typischen vollständige vertrauen Code (FTC) / Szenario Farmlösung, benutzerdefinierte Steuerelemente als Benutzersteuerelemente erstellt wurden oder Web steuert und über SharePoint-Lösungen bereitgestellt.

In einem Szenario mit Modell SharePoint-Add-in ist der JavaScript-Code in SharePoint-Seiten zum Implementieren von benutzerdefinierter Steuerelementen eingebettet.

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien zum Erstellen von benutzerdefinierten Steuerelementen in das neue SharePoint-Add-in-Modell bereitstellen.

- Verwenden von JavaScript zum Erstellen von benutzerdefinierter Steuerelementen embedded.
- Interaktion mit SharePoint-Daten und-Dienste verwenden Sie SharePoint ECMA Client Side-Objekt Objektmodell (CSOM) und/oder SharePoint/Office 365-REST-APIs.

<a name="options-to-embed-javascript-in-sharepoint-pages"></a>Optionen für das Einbetten von JavaScript in SharePoint-Seiten
-----------------------------------------------
Es gibt einige Optionen JavaScript in SharePoint-Seiten eingebettet.

- Verwenden von benutzerdefinierten Aktionen
- Einbetten von JavaScript direkt in Seitenlayouts
- Einbetten von JavaScript direkt in benutzerdefinierten Gestaltungsvorlagen (nicht empfohlen)

<a name="use-custom-user-actions"></a>Verwenden von benutzerdefinierten Aktionen
-----------------------
In diesem Muster werden benutzerdefinierte Aktionen Einbetten von JavaScript in eine Seite zur Laufzeit verwendet.

- Dieser Ansatz ist absolut unterstützt und ist ein gültiger Ansatz.

**Wenn sie geeignet ist?**

Wenn Sie JavaScript in alle Ihre SharePoint-Seiten eingebettet werden müssen, ist diese Option geeignet.

**Erste Schritte**

Die folgenden Artikel und zugehörige Video wird gezeigt, wie benutzerdefinierte Aktionen verwenden, um JavaScript in SharePoint-Seiten eingebettet werden sollen.

- [Core.EmbedJavaScript (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript)
- [OD4B. NavLinksInjection (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/OD4B.NavLinksInjection)
- [Schneidet websitesammlungsnavigation (O365 Plug & Play-Video)](http://channel9.msdn.com/blogs/OfficeDevPnP/Cross-site-collection-navigation)

<a name="embed-javascript-directly-into-page-layouts"></a>Einbetten von JavaScript direkt in Seitenlayouts
-------------------------------------------

In diesem Muster ist JavaScript direkt in Seitenlayouts in Veröffentlichungswebsites eingebettet.  

- Dieser Ansatz ist absolut unterstützt und ist ein gültiger Ansatz.
- Dieser Ansatz ist beim Veröffentlichen von Websites.

**Wenn sie geeignet ist?**

Wenn Sie JavaScript in bestimmten SharePoint-Seitenlayouts in Veröffentlichungswebsites in einem Szenario WCM einbetten müssen, ist diese Option geeignet.

<a name="embed-javascript-directly-into-custom-master-pages"></a>Einbetten von JavaScript direkt in benutzerdefinierten Gestaltungsvorlagen
--------------------------------------------------

In diesem Muster ist JavaScript direkt in benutzerdefinierten Gestaltungsvorlagen eingebettet.  

- Diese Vorgehensweise wird nicht empfohlen.
- Dieser Ansatz ist ein gültiger Ansatz.
- Einbetten von JavaScript direkt in benutzerdefinierten Gestaltungsvorlagen, aber behalten im Hinterkopf Dadurch werden Sie zusätzliche langfristige Kosten und Probleme mit zukünftige Updates.
    + Wenn Sie benutzerdefinierte Masterseiten verwenden möchten, bereiten Sie Änderungen der benutzerdefinierten Gestaltungsvorlagen anwenden, wenn wichtige Updates funktionsfähig zu Office 365 angewendet werden.

**Wenn sie geeignet ist?**

Wenn Sie auf JavaScript einbetten müssen eine Gestaltungsvorlage pro, ist dies eine gute Option, da es ermöglicht es Ihnen zu steuern, welche Seiten master in der JavaScript-Code eingebettet ist.

<a name="related-links"></a>Verwandte links
=============
- [Schneidet websitesammlungsnavigation (O365 Plug & Play-Video)](http://channel9.msdn.com/blogs/OfficeDevPnP/Cross-site-collection-navigation)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================
- [Core.EmbedJavaScript (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript)
- [OD4B. NavLinksInjection (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/OD4B.NavLinksInjection)
- [Core.EmbedJavaScript.WeekNumbers (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript.WeekNumbers)
- [Core.EmbedJavaScriptJSOM (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScriptJSOM)
- [Core.JavaScriptCustomization (O365 Plug & Play-Szenario mit Plug & Play-Hauptkomponente)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization)
- Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D)
- SharePoint 2013 lokal
