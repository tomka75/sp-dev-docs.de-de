---
title: Informationsverwaltungsrichtlinie in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 6b98c863dd21c5769ee03f3898970c90ee46e08c
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
<a name="information-management-policy-in-the-sharepoint-add-in-model"></a>Informationsverwaltungsrichtlinie in der SharePoint-add-in-Objektmodell
============================================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Anwenden der Informationsverwaltungsrichtlinie unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.  In einer typischen vollständige vertrauen Code (FTC) / in der Regel als Teil eines Zeitgebers Job Farmlösung Szenario Informationen Richtlinie zur Verwaltung wurde verwaltete und über die SharePoint Server-Side Object Model angewendet und über die SharePoint-Farmlösungen bereitgestellt. 

In einem Szenario mit Modell SharePoint-Add-in die SharePoint-Client Side-Objekt Objektmodell (CSOM) und remote Zeitgeberaufträge dienen zum Verwalten und Informationsverwaltungsrichtlinie anzuwenden.

<a name="high-level-guidelines"></a>Hohe Stufe Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden high Level Richtlinien zum Verwalten und Anwenden von Informationsverwaltungsrichtlinien für SharePoint-Websites bereitstellen.  

- Beachten Sie, wenn Informationsverwaltungsrichtlinien auf der Ebene der Websitesammlung definiert sind, und klicken Sie dann die Besitzer der Websitesammlung, die sie deaktivieren können.
    + Wenn von Informationsverwaltungsrichtlinien Besitzer einer Websitesammlung festlegen mit dem remote-Modell und CSOM sie nicht deaktivieren können.  Der remote-Modell Ansatz ist ein weitere benutzerfreundliche Enterprise-Modell, das Informationsverwaltungsrichtlinien wird sichergestellt werden immer in der gesamten einer SharePoint-Umgebung aktiviert.
- Verwenden des SharePoint-CSOM in einem remote Zeitgeberauftrag zum Verwalten und Anwenden von Informationsverwaltungsrichtlinien.

- Stellen Sie sicher, dass Sie nicht die Grenzwerte für die SharePoint-API für Office 365 Throttle verletzt werden beim Arbeiten mit großen Datenmengen und rekursive crawlt beim Überprüfen von Artefakten in Ihrer SharePoint-Websites und Informationsverwaltungsrichtlinien für diese entsprechend anzuwenden.
    + Die [Core.Throttling (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.Throttling) wird gezeigt, wie intelligent Code SharePoint-API für Office 365-Einschränkung zu schreiben.

> [!NOTE] 
> Das CSOM hat derzeit keine Methoden verwenden, um die Aufbewahrung für Inhaltstypen (nur auf Websites) festgelegt.

**Erste Schritte**

Die folgenden O365 Plug & Play-Codebeispiel und Video wird gezeigt, wie zum Verwalten und Anwenden von Informationsverwaltungsrichtlinie für SharePoint-Websites.  In diesem Beispiel wird der Code durchläuft die Inhaltstypen zu Dokumentbibliotheken in SharePoint-Websitesammlungen angewendet und eine Aufbewahrungsrichtlinie gilt.

- [Governance.ContentTypeEnforceRetention (O365 Plug & Play-Codebeispiel)](https://github.com/SharePoint/PnP/tree/master/Solutions/Governance.ContentTypeEnforceRetention)

Im folgende Video durchlaufen im Codebeispiel.

- [Informationsverwaltungsrichtlinie mit app-Modell (O365 Plug & Play-Video)](http://channel9.msdn.com/blogs/OfficeDevPnP/Information-management-policy-wtih-app-model)

<a name="related-links"></a>Verwandte links
=============
- [Informationsverwaltungsrichtlinie mit app-Modell (O365 Plug & Play-Video)](http://channel9.msdn.com/blogs/OfficeDevPnP/Information-management-policy-wtih-app-model)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [Governance.ContentTypeEnforceRetention (O365 Plug & Play-Codebeispiel)](https://github.com/SharePoint/PnP/tree/master/Solutions/Governance.ContentTypeEnforceRetention)
- Beispiele und Inhalte am https://github.com/SharePoint/PnP

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D) *teilweise*
- SharePoint 2013 lokal – *teilweise*

*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*
