---
title: Benutzerdefinierte Aktionen in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: d721746d8db8b5a6b01e71a1ea8d031bfd7b4330
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="custom-actions-in-the-sharepoint-add-in-model"></a>Benutzerdefinierte Aktionen in der SharePoint-add-in-Objektmodell
=============================================

<a name="summary"></a>Summary
-------

Der Ansatz für die Liste elementmenüs ändern und des Menübands in SharePoint unterscheidet sich im neuen SharePoint-Add-in-Modell befand mit vollständigen Code, der als vertrauenswürdig. In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario, elementmenüs Liste Menüband Änderungen wurden in XML (benutzerdefinierte Aktionen) definiert, in Features gepackt und über SharePoint-Lösungen bereitgestellt.

In einem Modell Szenario SharePoint-Add-in verwenden Sie die SharePoint-Client-Side-Objekt Objektmodell (CSOM) oder die REST-API, um benutzerdefinierte Aktionen zu erstellen, die Liste elementmenüs und des Menübands ändern. Dieses Muster wird häufig als *remote provisioning Muster*bezeichnet.

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien für das Erstellen und Bereitstellen von benutzerdefinierten Aktionen in das neue SharePoint-Add-in-Modell bereitstellen.

- Benutzerdefinierte Aktionen können zum Ändern der Liste elementmenüs und des Menübands verwendet werden.
- Sie können nicht mithilfe einer benutzerdefinierten Aktion direkt über ein Add-in, das eine benutzerdefinierte Aktion implementiert Menüelemente ausgeblendet.
    + Dies ist, da das [HideCustomAction-Element (MSDN-API-Dokumentation)](https://msdn.microsoft.com/en-us/library/office/ms414790.aspx) nicht in der SharePoint ECMA Clients Ide Object Model (CSOM) - [UserCustomAction-Eigenschaften (MSDN-API-Dokumentation)](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.usercustomaction_properties.aspx)oder die REST-APIs in SharePoint/Office 365 - verfügbar ist [SP. UserCustomActionCollection Object (sp.js) (MSDN-API-Dokumentation)](https://msdn.microsoft.com/en-us/library/office/jj247124.aspx).
    + Wenn Sie Menüelemente ausblenden möchten, müssen Sie eine benutzerdefinierte Aktion verwenden, JavaScript oder angepasste CSS in SharePoint-Seiten eingebettet. Die JavaScript- oder -CSS in der SharePoint-Seiten eingebettet werden das Menüelement ausgeblendet.
- Verwenden Sie die SharePoint-Client-Side-Objekt Objektmodell (CSOM) und/oder der REST-APIs in SharePoint/Office 365, um benutzerdefinierte Aktionen zu implementieren.

**Erste Schritte**

Das folgende Beispiel veranschaulicht, wie eine benutzerdefinierte Aktion im Einstellungsmenü in der Hostwebsite hinzugefügt, wie ein Dialogfeld in einer benutzerdefinierten Aktion angezeigt, wie ein Dialogfeld ausgeblendet wird, die eine Seite aus einem remote-add-ins Web gehostet wird und wie Sie mithilfe einer benutzerdefinierten Aktion zum Erstellen von Listen und Festlegen der Design eines Webs.

- [Provisioning.SiteModifier (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteModifier)

    Hier können Sie sehen, dass die Verknüpfung im Beispiel für die benutzerdefinierte Aktion im Menü Websiteeinstellungen hinzufügt.
    
    ![Im Einstellungsmenü von Office 365 wird die Menüoption Website ändern hervorgehoben angezeigt.](media/Recipes/CustomActions/Custom-Action-In-Site-Settings.png)
    
    Hier sehen Sie das Popup-Fenster geöffnet wird, über den Link Site ändern.
    
    ![Website ändern Popup-Fenster wird mit einer das Kontrollkästchen Gruppe mit dem Namen Listen angezeigt, die zwei Kontrollkästchen Projekte und Kontakte enthält. Unterhalb der Listen eine Gruppe das Kontrollkästchen heißt verschiedene die enthält das Kontrollkästchen mit dem Namen Design anwenden. Darunter heißen zwei Schaltflächen bestätigen und Abbrechen.](media/Recipes/CustomActions/Custom-Action-Popup-Menu.png)

<a name="related-links"></a>Verwandte links
=============

- [Benutzersteuerelemente und Websteuerelemente (SharePoint-Add-in-Anleitung)](user-controls-and-web-controls-sharepoint-add-in.md)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [Provisioning.SiteModifier (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteModifier)
- Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D)
- SharePoint 2013 lokal
