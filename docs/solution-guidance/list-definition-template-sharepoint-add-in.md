---
title: Listendefinition / list Vorlage in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: c4a412493d0cc1768aa103b06cd98e189479d317
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="list-definition--list-template-in-the-sharepoint-add-in-model"></a>Listendefinition / list Vorlage in der SharePoint-add-in-Objektmodell
==============================================================

<a name="summary"></a>Summary
-------

Die Vorgehensweise zum Erstellen von Listendefinitionen / Listenvorlagen in unterscheidet das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.  In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario, benutzerdefinierten Listendefinitionen / Listenvorlagen mit deklarativem Code erstellt und über den SharePoint-Lösungen bereitgestellt wurden. 

In einem Szenario mit Modell SharePoint-Add-in kann nicht benutzerdefinierten Listendefinitionen tatsächlich erstellen.  Es ist nicht dazu einfach möglich.  Allerdings kann das remote provisioning Muster verwendet, um benutzerdefinierte Listenvorlagen (STP-Dateien) für Office 365 bereitstellen.

<a name="high-level-guidelines"></a>Hohe Stufe Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden high Level Richtlinien zum Implementieren von Listendefinitionen / Listenvorlagen bereitstellen.

- Verwenden Sie das remote provisioning Muster zum Bereitstellen von Vorlagen für Bibliothekslisten (STP-Dateien) für SharePoint-Websites.
- Sie können die Abwesenheitsnotiz über das Verhalten des Liste Outlook erstellen, die standardisierte Einstellungen gelten für alle Listen in einer SharePoint-Website erstellt außer Kraft setzen.  Finden Sie weitere Informationen zu diesem Ansatz unten.
- Sie können ein SharePoint-Add-in zum Erstellen von Listen mit standardisierte Einstellungen erstellen. Finden Sie weitere Informationen zu diesem Ansatz unten.

<a name="options-to-ensure-standardized-settings-templates-are-applied-to-sharepoint-lists-upon-list-creation"></a>Optionen, die standardisierte Einstellungen (Vorlagen) gewährleisten angewendet werden mit SharePoint-Listen Liste erstellt worden ist
------------------------------------------------------------------------------------------------------

Sie haben verschiedene Optionen, um sicherzustellen, dass standardisierte Einstellungen (Vorlagen) angewendet werden mit SharePoint-Listen Liste erstellt worden ist.

- Überschreiben Sie die Abwesenheitsnotiz über das Verhalten des Liste erstellen.   
- Erstellen eines SharePoint-Add-Ins. 

<a name="override-the-out-of-the-box-list-creation-behavior"></a>Überschreiben Sie die Abwesenheitsnotiz über das Verhalten des Liste erstellen
--------------------------------------------------
In diesem Muster ändern Sie die Abwesenheitsnotiz über das Verhalten des Liste Erstellung durch Hinzufügen eines Ereignisempfängers an das ListAdded-Ereignis.  Klicken Sie dann konfiguriert in den Ereignisdetails Ereignisempfänger für das ListAdded-Ereignis, das Sie das remote provisioning Muster verwenden, um standardisierten Konfigurationen auf jede Liste anzuwenden, die erstellt wird.

Hinzufügen von Inhaltstypen, den Standardinhaltstyp festlegen, Listenspalten hinzufügen, wird die versionneinstellungen, und alle anderen Liste Typ Konfigurationen, die festgelegt werden können, können diese standardisierten Konfigurationen enthalten. 
    
- Dieser Ansatz ermöglicht Ihnen, die standardisierte Einstellungen für alle Listen gelten.
- Dieser Ansatz ermöglicht Ihnen, die standardisierte Einstellungen gelten für verschiedene Arten von Listen.
    + Beispiel: Wenn Sie eine Dokumentbibliothek erstellen und eine Vorgangsliste in den Ereignisempfänger ListAdded feststellen welche Art von Liste Sie erstellt haben und Sie können unterschiedliche anwenden Einstellungen basierend auf den Listentyp standardisierte.  Alle Dokumentbibliotheken benötigen möglicherweise eine Gruppe von Inhaltstypen, die angewendet werden, während alle Aufgabenliste benötigen eine andere Menge von Inhaltstypen angewendet werden.
- Dieser Ansatz unterstützt Anwenden von mehreren verschiedenen Optionen auf Listen nicht.
    + Beispiel: Wenn Sie eine Dokumentbibliothek erstellen und eine Vorgangsliste in den Ereignisempfänger ListAdded feststellen welche Art von Liste Sie erstellt haben und Sie können unterschiedliche anwenden Einstellungen basierend auf den Listentyp standardisierte.  Sie können nicht jedoch unterschiedliche Vorlagen in einer Dokumentbibliothek anwenden, die im Vergleich zu einer anderen Dokumentbibliothek zu erstellen, die Sie erstellen.

**Wenn sie geeignet ist?**

Wenn Sie standardisierte globale Einstellungen gelten für alle Listen oder Listen eines bestimmten Typs müssen.

**Wenn es nicht geeignet ist?**

Wenn Sie mehrere Optionen für unterschiedliche Vorlagen auf Listen anwenden müssen.

**Erste Schritte**

Die folgenden SharePoint-Add-Ins Modell Anleitung wird beschrieben, wie Ereignisempfänger implementieren.

- [Ereignisempfänger (SharePoint-Add-Ins Modell Anleitung)](event-receiver-and-list-event-receiver-sharepoint-add-in.md)

<a name="create-a-sharepoint-add-in"></a>Erstellen eines SharePoint-Add-Ins
--------------------------

In diesem Muster erstellen Sie ein SharePoint-Add-in zum Erstellen von Listen mit standardisierte Einstellungen, und weisen Sie die Benutzer auf das SharePoint-Add-in verwenden, um neue Listen erstellen.  Stellt im Wesentlichen das SharePoint-Add-in Benutzern mit Auswahlmöglichkeiten von verschiedenen Listen zu erstellen.  Das SharePoint-Add-in ermöglicht Benutzern das Erstellen von verschiedenen Listen werden vom Unternehmen definiert und von einem Entwickler implementiert. Ausfüllen eines Formulars in der SharePoint Add-in für Meta-Listendaten angeben, und wählen bietet welcher Liste Sie aus der Auswahl das Add-in erstellen. Das Add-in mithilfe des remote provisioning Musters um entsprechend die Liste zu erstellen.
    
- Dieser Ansatz ermöglicht Ihnen, die standardisierte Einstellungen für alle Listen gelten.
- Dieser Ansatz ermöglicht Ihnen, die standardisierte Einstellungen gelten für verschiedene Arten von Listen.
- Dieser Ansatz ermöglicht Ihnen mehrere andere Vorlage auf Listen angewendet.

**Wenn sie geeignet ist?**

Wenn Sie mehrere Optionen für unterschiedliche Vorlagen auf Listen anwenden müssen.

**Erste Schritte**

Die folgenden O365 Plug & Play-Codebeispiel und Video wird gezeigt, wie ein SharePoint-Add-in zu erstellen, die eine Benutzeroberfläche bereitstellt, mit die Endbenutzer neue Dokumentbibliotheken erstellen können.  Darüber hinaus wird das Erstellen einer Dokumentbibliothek mit spezifischen Konfigurationen, die gemeinsam eine Vorlage darstellen veranschaulicht.

- [ECM. DocumentLibraries (O365 Plug & Play-Codebeispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)

Im folgende Video durchlaufen im Codebeispiel.

- [Dokument- und Vorlagen mit app-Modell (O365 Plug & Play-Video)](http://channel9.msdn.com/blogs/OfficeDevPnP/Document-and-list-templates-with-app-model)

<a name="related-links"></a>Verwandte links
=============

- [Listeninstanz (SharePoint-Add-Ins Modell Anleitung)](list-instance-sharepoint-add-in.md)
- [Ereignisempfänger (SharePoint-Add-Ins Modell Anleitung)](event-receiver-and-list-event-receiver-sharepoint-add-in.md)
- [Dokument- und Vorlagen mit app-Modell (O365 Plug & Play-Video)](http://channel9.msdn.com/blogs/OfficeDevPnP/Document-and-list-templates-with-app-model)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [ECM. DocumentLibraries (O365 Plug & Play-Codebeispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)
- Beispiele und Inhalte am https://github.com/SharePoint/PnP

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D) *teilweise*
- SharePoint 2013 lokal – *teilweise*

*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*
