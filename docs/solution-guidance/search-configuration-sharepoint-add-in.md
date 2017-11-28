---
title: Konfiguration der Suche im SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 9a84ae5aa1a12322227c9182c9ff0f5fb1798e48
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="search-configuration-in-the-sharepoint-add-in-model"></a>Konfiguration der Suche im SharePoint-add-in-Objektmodell
===================================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Konfigurieren der Suche unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war. In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario der SharePoint Server-Side Object Model zum Konfigurieren der Suche und über SharePoint-Lösungen bereitgestellt wurde.

In einem Szenario mit SharePoint-Add-Ins Modell verwenden Sie die SharePoint-Client-Side-Objekt Objektmodell (CSOM) oder REST-API zum Konfigurieren der Suche. Dieses Muster wird häufig als *remote provisioning Muster*bezeichnet.

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien zum Konfigurieren der Suche in das neue SharePoint-Add-in-Modell bereitstellen.

- Verwenden Sie SharePoint-Client-Side Object Model (CSOM)-API zum Konfigurieren der Suche nach Möglichkeit durch Importieren und Exportieren der Konfiguration für die Suche.
- Nicht alle suchkonfigurationseinstellungen stehen derzeit über die SharePoint-CSOM-API.
    + Finden Sie unter den [Export und Import suchkonfigurationseinstellungen in SharePoint Server 2013 (TechNet-Artikel)](https://technet.microsoft.com/en-us/library/jj871675.aspx#BKMK_2) eine Liste der suchkonfigurationseinstellungen, die exportiert und importiert werden können.
    + Wenn ein suchkonfigurationseinstellung nicht mit dem Clientobjektmodell festgelegt werden kann ist die Benutzeroberfläche für die Verwaltung So legen Sie Konfigurationswerte erforderlich.
- Die SharePoint-REST-API kann keinen (zu diesem Zeitpunkt) importieren oder Exportieren von suchkonfigurationseinstellungen.

**Erste Schritte**

Im folgende Beispiel wird gezeigt, wie zum Importieren und Exportieren von Einstellungen für Suchfeld zwischen SharePoint-Mandanten, Websitesammlungen und Websites.

- [Core.SearchSettingsPortability (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SearchSettingsPortability)

<a name="related-links"></a>Verwandte links
=============

- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [Core.SearchSettingsPortability (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SearchSettingsPortability)
- Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D)
- SharePoint 2013 lokal
