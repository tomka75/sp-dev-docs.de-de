---
title: Variationen in SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 8d389a61ed6af1edcdc4485d1e28d366496b29d1
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="variations-in-the-sharepoint-add-in-model"></a>Variationen in SharePoint-add-in-Objektmodell
=========================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Konfigurieren von Variationen unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war. In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario der SharePoint Server-Side Object Model (Microsoft.SharePoint.Publishing.Variations) wurde verwendet, um Variationen konfigurieren und Features, die den Code ausgeführt über SharePoint-Lösungen bereitgestellt wurden.

In einem Szenario mit SharePoint-Add-Ins Modell verwenden Sie die SharePoint-Client-Side-Objekt Objektmodell (CSOM) oder REST-API Variationen konfigurieren. Dieses Muster wird häufig als *remote provisioning Muster*bezeichnet.

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien zur Konfiguration von Variationen in das neue SharePoint-Add-in-Modell enthalten.

- Verwenden Sie die SharePoint-Client-Side Object Model (CSOM)-API, um Variationen möglichst konfigurieren.
    - .NET clientseitigen Objektmodell [Variationen-Klasse (MSDN-API-Dokumentation)](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.variations.aspx)
    - JavaScript clientseitigen Objektmodell [Variationen-Klasse (MSDN-API-Dokumentation)](https://msdn.microsoft.com/en-us/library/office/jj994778.aspx)
- Nicht alle Einstellungen für Variationen Konfiguration stehen derzeit über den oben aufgeführten Klassen SharePoint CSOM API-Varianten.
- Sie können hinausgehen, was die oben aufgeführten CSOM API Variationen Klassen bereitstellen und einige variationseinstellungen konfigurieren.  Zu diesem Zweck legen Sie die Werte für Variationen Einstellungen in Website-Eigenschaftenbehälter gespeichert und/oder Ändern von Listenelementen in den Listen mit Variationen verknüpft ist.
    + Die [VariationsExtensions.cs-Klasse (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core/OfficeDevPnP.Core/Extensions/VariationExtensions.cs) enthält einige Beispiele, die Eigenschaftensammlung und Liste Element Eigenschaftswerte zum Konfigurieren der variationseinstellungen zu ändern.
    + Die [VariationsExtensions.cs-Klasse (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Extensions/VariationExtensions.cs) veranschaulicht, wie ***Alle Einstellungen*** konfigurieren, die Sie in der Einstellungsseite Variationen festlegen können.
    + Das [Aktivieren der variationseinstellungen, sodass Sie Varianten Ihrer Website (Office 365-Support-Artikel) erstellen können](https://support.office.com/en-za/article/Turn-on-variations-settings-so-you-can-create-variations-of-your-site-fc021610-bdb5-4b5c-9d59-ce8af6699b4b) , sind die Elemente können in der Einstellungsseite Variationen konfigurieren und beschreibt, was sie tun aufgelistet.

<a name="related-links"></a>Verwandte links
=============

- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [VariationsExtensions.cs-Klasse (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Extensions/VariationExtensions.cs)
- Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D)
- SharePoint 2013 lokal
