---
title: Stellvertretungs-Steuerelemente in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 3981faf45be7a2a5e80dae40859b023d9dda9092
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="delegate-controls-in-the-sharepoint-add-in-model"></a>Stellvertretungs-Steuerelemente in der SharePoint-add-in-Objektmodell
================================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Implementieren von stellvertretungs-Steuerelemente in Ihrem Code unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.  In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario Steuerelemente, als Benutzersteuerelemente oder Websteuerelemente erstellt wurden, Delegaten Features registriert, und über die SharePoint-Lösungen bereitgestellt.

In einem Modell Szenario SharePoint-Add-in ist JavaScript in SharePoint-Seiten implementiert die gleiche Funktion wie stellvertretungs-Steuerelemente eingebettet.

<a name="high-level-guidelines"></a>Hohe Stufe Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden Richtlinien auf hohen Ebenen bieten für das stellvertretungs-Steuerelemente in das neue SharePoint-Add-in-Modell erstellen.

- Es ist kein direkten Delegaten-Steuerelement-Ersatz im SharePoint-Add-in-Modell.
- Verwenden Sie eingebettetes JavaScript, um die gleiche Funktion wie stellvertretungs-Steuerelemente aus Sicht des Endbenutzers zu implementieren.
- Interaktion mit SharePoint-Daten und-Dienste verwenden Sie SharePoint JavaScript Client Side-Objektmodell (JSOM) und/oder SharePoint/Office365-REST-APIs.

Finden Sie unter der [Benutzersteuerelemente und Websteuerelemente (SharePoint-Add-in Modell Anleitung)](user-controls-and-web-controls-sharepoint-add-in.md) erfahren, wie JavaScript mit benutzerdefinierten Aktionen für alle SharePoint-Seiten eingebettet und JavaScript direkt in Seitenlayouts und Masterseiten einzubetten.

<a name="related-links"></a>Verwandte links
=============
- [Schneidet websitesammlungsnavigation (O365 Plug & Play-Video)](http://channel9.msdn.com/blogs/OfficeDevPnP/Cross-site-collection-navigation)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================
- [OD4B. NavLinksInjection (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/OD4B.NavLinksInjection)
- Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D)
- SharePoint 2013 lokal
