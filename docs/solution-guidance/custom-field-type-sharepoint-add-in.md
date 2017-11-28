---
title: Typ des benutzerdefinierten Felds in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 550669c2e1cb7e766f93ed1ae00fc0962421bace
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="custom-field-type-in-the-sharepoint-add-in-model"></a>Typ des benutzerdefinierten Felds in der SharePoint-add-in-Objektmodell
================================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie angepasste Endbenutzer Erfahrungen anzugebende unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war. In einer typischen vollständige vertrauen Code (FTC) / Szenario Farmlösung, benutzerdefinierte Feldtypen mit SharePoint Server-Side-Objektmodellcode erstellt wurden, durch Vererbung von einer der integrierten feldtypklassen und durch Erstellen einer Feldtyp-Bereitstellungsdatei (XML). Diese Komponenten wurden über die SharePoint-Lösungen bereitgestellt. 

In einem Szenario mit SharePoint-Add-ins Modell werden angepasste Endbenutzer Erfahrungen über clientseitiges Rendering implementiert. Bei diesem Ansatz werden JavaScript-Dateien zum Implementieren von angepassten Endbenutzer Erfahrungen verwendet. Das remote provisioning Muster stellt die JavaScript-Dateien und registriert diese mit SharePoint-Felder über die JSLink-Eigenschaft.

Aus Sicht des Endbenutzers sieht das Funktion/Ergebnis gleich aus.

Es folgen einige Beispiele der Typ des benutzerdefinierten Felds, die eine Zuordnung Google implementiert wird. Diese ergeben sich aus dem [Branding.JSLink](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.JSLink) Office 365 Plug & Play-Beispiel.

**Google-Zuordnung Miniaturansichten in einer Listenansicht angezeigt:**

![Zwei Google Kartenansichten Microsoft Campus Location Point und Bereich angezeigt.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps.png)

**Inlinebearbeitung eine größere Google Map Miniaturansicht angezeigt:**
![zwei Google zugeordnet ist. Eine Ansicht mit dem Microsoft Campus Location Point mit einem Link, wählen Sie den Speicherort, der anderen Ansicht darstellen Microsoft Campus Speicherort mit einem Link zum-Shape bearbeiten.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps_Edit.png)

**Ein Dialogfeld mit dem Aktivieren der Inlinebearbeitung:**
![eine Google Wegweiser für die Microsoft Campus Form angezeigt. Text auf das Bild liest, klicken Sie auf der Karte Markierungen platzieren und erstellen Ihre Form. Fertig stellen Sie, indem Sie auf der ersten Marker. Sie können ziehen Sie jede der Markierungen um, oder klicken Sie auf klicken sie auf Weitere Optionen. Oben auf die Schaltfläche Zuordnung löschen können Sie um alle Marken zu entfernen.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps_Shape_Edit.png)

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien für die Implementierung clientseitiges Rendering bereitzustellen.

- Verwenden Sie die JavaScript-Dateien und clientseitiges Rendering benutzerdefinierte Feldtypen implementieren.
- Verwenden Sie das remote provisioning Muster JavaScript-Dateien bereitstellen und registrieren mit SharePoint-Felder oder -Listenansicht-Webparts.
- Registrieren Sie das Modul minimale herunterladen Strategie (MDS), um sicherzustellen, dass das Modul MDS sollten Sie die benutzerdefinierte Rendering JavaScript-Dateien ist die JavaScript-Dateien.
- Festlegen des JSLink-Eigenschaft mit Hostwebsite mindestens Vollzugriff auf Webebene erfordert, daher wird diese Vorgehensweise nicht geeignet für add-ins auf der SharePoint Store ist

<a name="options-to-implement-client-side-rendering-with-javascript-files-via-the-jslink-property"></a>Optionen für die Implementierung von clientseitiges Rendering mit JavaScript-Dateien über die JSLink-Eigenschaft
----------------------------------------------------------------------------------------

Sie haben eine Reihe von Optionen für die Implementierung von clientseitiges Rendering mit JavaScript-Dateien über die JSLink-Eigenschaft.

- Legen Sie die JSLink-Eigenschaft auf eine Listenansicht-Webpart, das eine Ansicht einer SharePoint-Liste rendert. 
- Legen Sie die JSLink-Eigenschaft für ein SharePoint-Feld. 
- Legen Sie die JSLink-Eigenschaft für ein SharePoint-Inhaltstyps. 
    

<a name="set-the-jslink-property-on-a-list-view-web-part-that-renders-a-view-of-a-sharepoint-list"></a>Legen Sie die JSLink-Eigenschaft auf eine Listenansicht-Webpart, das eine Ansicht einer SharePoint-Liste rendert
-----------------------------------------------------------------------------------------
Bei dieser Option legen Sie die JSLink-Eigenschaft auf eine WebPartDefinition.
    
- **Dieser Ansatz erstellen ein benutzerdefinierten Feldtyps nicht speziell auf der Ebene der SPField.**
    + Aus diesem Grund *das benutzerdefinierte Rendering gilt nur in der Listenansicht-Webpart, in dem Sie die JSLink-Eigenschaft festlegen*.
- Dieser Ansatz ermöglicht es das Rendering für eine oder mehrere SharePoint-Felder gleichzeitig zu ändern.
- Dieser Ansatz kann mit deklarativem Code, mit dem SharePoint Server-Side-Objektmodell, mit dem SharePoint mithilfe der clientseitigen Objektmodell (CSOM) oder über PowerShell erfolgen.
    + Es wird empfohlen, dass Sie das SharePoint Server-Side-Objektmodell, den SharePoint-Client-seitigen Objektmodell oder die PowerShell verwenden, um die JSLink-Eigenschaft über die remote provisioning Muster festgelegt.

**Wenn sie geeignet ist?**

Wenn Sie bestimmte Ansichten für SharePoint-Listendaten definieren, und ändern das Rendering für mehr als ein SharePoint-Feld müssen, ist dies eine gute Wahl.

**Erste Schritte**

Im folgende Beispiel wird die JSLink-Eigenschaft auf eine SharePoint Listenansicht-Webpart.

- [Branding.ClientSideRendering (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
    + Enthält 9 Beispiele, in denen die JSLink-Eigenschaft für ein SharePoint Listenansicht-Webpart und eine Erläuterung der Implementierung der jedes Beispiel festgelegt.
    + Die RegisterJStoWebPart-Methode wird die Listenansicht-Webpart des JSLink-Eigenschaft festgelegt. 

<a name="set-the-jslink-property-for-a-sharepoint-field"></a>Legen Sie die JSLink-Eigenschaft für ein SharePoint-Feld
----------------------------------------------

Bei dieser Option legen Sie die JSLink-Eigenschaft für ein SPField.
    
- **Dieser Ansatz registriert insbesondere die JSLink-Eigenschaft auf der Ebene der SPField.**
    + Aus diesem Grund *gilt das benutzerdefinierte Rendering überall der SPField gerendert wird*.
- Dieser Ansatz ermöglicht Ihnen, das Rendering für ein SharePoint-Feld zu ändern.
- Dieser Ansatz kann mit deklarativem Code, mit dem SharePoint Server-Side-Objektmodell, mit dem SharePoint-Objektmodell mithilfe der clientseitigen oder über PowerShell erfolgen.
    + Es wird empfohlen, dass Sie das SharePoint Server-Side-Objektmodell, den SharePoint-Client-seitigen Objektmodell oder die PowerShell verwenden, um die JSLink-Eigenschaft über die remote provisioning Muster festgelegt.

**Wenn sie geeignet ist?**

Wenn Sie zum Definieren einer bestimmten Ansicht für ein bestimmtes Feld SharePoint, und stellen Sie sicher, dass die Ansicht immer verwendet wird benötigen, wenn das Feld gerendert wird, ist dies eine gute Wahl.

**Erste Schritte**

In den folgenden Artikeln wird gezeigt, wie die JSLink-Eigenschaft auf eine SPField festgelegt.

- [Verwenden die JSLink-Eigenschaft die Art zu ändern, die Ihre Feld oder Ansichten in SharePoint 2013 (Tobias Zimmergren) gerendert werden](http://zimmergren.net/technical/sp-2013-using-the-spfield-jslink-property-to-change-the-way-your-field-is-rendered-in-sharepoint-2013)
- [Verwenden von JSLink mit SharePoint 2013 (MSDN Magazine)](https://msdn.microsoft.com/en-us/magazine/dn745867.aspx)

<a name="challenges-with-implementing-client-side-rendering-with-javascript-files-via-the-jslink-property"></a>Probleme bei der Implementierung von clientseitiges Rendering mit JavaScript-Dateien über die JSLink-Eigenschaft
------------------------------------------------------------------------------------------------

Benutzerdefiniertes clientseitiges Rendering Komponenten bei der Entwicklung, behalten Sie im Hinterkopf Folgendes.

- Nicht alle SharePoint-Felder können mit der JSLink-Eigenschaft außer Kraft gesetzt werden.
    + Die TaxonomyField ist ein gutes Beispiel.
- JSLink unterstützt mehrere Token.
    + _layouts
    + _SITE
    + _siteCollection
    + _siteCollectionLayouts
    + _siteLayouts
- Sie können die JSLink JavaScript-Dateien mit SharePoint Skript auf Anforderung (SOD) Framework verzögerte Laden der Datei registrieren.
    - Verwenden Sie das Tag (d) am Ende der URL JSLink die Datei mit der SOD registrieren.
 
    ```
    ~sitecollection/Style Library/JSLink-Samples/DependentFields.js(d)
    ```
- Sie können mehrere JavaScript-Dateien über die JSLink-Eigenschaft laden.
    + Dies ist insbesondere dann hilfreich, wenn eine Bibliothek der JavaScript-Dateien, die Ihre clientseitiges Rendering implementieren.
    + Erwägen Sie diese Vorgehensweise bei mobile Geräten Zielgruppenadressierung, da Sie nur das JavaScript übermitteln, Sie ein bestimmtes SharePoint-Feld clientseitiges Rendering implementieren müssen, können.
    + Verwendung der | Zeichen, trennen Sie die JavaScript-Dateien, die Sie laden möchten. 
    
    ```
    ~sitecollection/Style Library/JSLink-Samples/MainLibrary.js|~sitecollection/Style Library/JSLink-Samples/SpecificField.js**(d)**
    ```

<a name="related-links"></a>Verwandte links
=============
- [SPField.JSLink-Eigenschaft (MSDN-API-Dokumente)](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfield.jslink.aspx)
- [Verwenden die JSLink-Eigenschaft die Art zu ändern, die Ihre Feld oder Ansichten in SharePoint 2013 (Tobias Zimmergren) gerendert werden](http://zimmergren.net/technical/sp-2013-using-the-spfield-jslink-property-to-change-the-way-your-field-is-rendered-in-sharepoint-2013)
- [Verwenden von JSLink mit SharePoint 2013 (MSDN Magazine)](https://msdn.microsoft.com/en-us/magazine/dn745867.aspx)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [Branding.ClientSideRendering (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
- [Branding.JSLink (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.JSLink)
- Beispiele und Inhalte am https://github.com/SharePoint/PnP

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D) *teilweise*
- SharePoint 2013 lokal – *teilweise*

*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*
