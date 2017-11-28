---
title: Dokument-ID-Anbieter in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: a20320887a17b26a4eb247b6c2968b82ab5d715b
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="document-id-provider-in-the-sharepoint-add-in-model"></a>Dokument-ID-Anbieter in der SharePoint-add-in-Objektmodell
===================================================

<a name="summary"></a>Summary
-------

Der gewählten Ansatz festlegen Eindeutiger Bezeichner für Dokumente in SharePoint unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war. In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario Ausführen von SharePoint Server-Side Object Model Code Ereignishandler Element Liste wurden eindeutige Bezeichner für Dokumente festgelegt und sie über die SharePoint-Lösungen bereitgestellt wurden.

In einem Modell Szenario SharePoint-Add-in SharePoint mithilfe der clientseitigen Objekt Objektmodell (CSOM) und/oder der SharePoint-REST-API dienen zum eindeutige Bezeichnern für Dokumente festgelegt.

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien für die Einstellung eindeutigen Bezeichnern für Dokumente in das neue SharePoint-Add-in-Modell bereitstellen.

- Verwenden Sie die SharePoint-Client Side-Objekt Objektmodell (CSOM) und/oder der SharePoint-REST-APIs zum eindeutige Bezeichnern für Dokumente festlegen.
- Es ist derzeit keine unterstützte Out-of-Box-Mechanismus zum Zuordnen von remote verarbeiteten Code, um die Out-of-Box-Dokument-ID-Anbieter zu ersetzen, damit diese Funktion nicht nativ unterstützt wird, um mit remote-APIs geändert werden.
- Allerdings werden wie in vielen Fällen mit dem-Add-in-Objektmodell, alternative Routen untersucht wird.

<a name="how-are-unique-identifiers-set-on-documents"></a>Wie werden eindeutige Bezeichner für Dokumente werden festgelegt?
--------------------------------------------

***Im Wesentlichen durch einen eindeutigen Bezeichner für ein Dokument Mittel Festlegen des Werts einer Spalte in einer SharePoint-Liste /-Dokumentbibliothek festlegen.***  

Die SharePoint-(CSOM) und/oder den REST-APIs können verwendet werden, um die Spaltenwerte festgelegt, und dafür festlegen Eindeutiger Bezeichner für Dokumente genutzt werden können. Finden Sie die folgenden Artikel enthalten weitere Informationen zu diesen APIs und wie Sie mit diesen Spaltenwerte festgelegt.  

- [Führen Sie grundlegender Vorgänge unter Verwendung von SharePoint 2013-clientbibliothekscode (MSDN-Artikel aus)](https://msdn.microsoft.com/en-us/library/office/fp179912.aspx#BasicOps_SPListItemTasks) 
- [Arbeiten mit Listen und Listenelemente mit REST (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/office/dn292552.aspx#ListItems)

<a name="options-to-set-unique-identifiers-for-documents"></a>Optionen zum Festlegen der eindeutige Bezeichner für Dokumente
-----------------------------------------------
Sie müssen einige Optionen zum eindeutige Bezeichnern für Dokumente in SharePoint gespeicherten festgelegt.

- Verwenden von remote-Ereignisempfänger
- Verwenden Sie einen Hintergrundprozess

<a name="use-remote-event-receivers"></a>Verwenden von remote-Ereignisempfänger
--------------------------
In diesem Muster ausgelöst werden remote-Ereignisempfänger, wenn neue Dokumente in SharePoint-Bibliotheken hochgeladen werden. Stellen Sie die remote-Ereignisempfänger CSOM oder REST-API aufruft, um die eindeutigen IDs für Dokumente festgelegt.

- Dieses Muster wird ausgeführt, unmittelbar nachdem ein Dokument in SharePoint hochgeladen wird.
    + Solange der Code im Zusammenhang mit der remote-Ereignisempfänger-Dienst in einem angemessenen Zeitraum ausgeführt wird, werden die Dokument-IDs schnell festgelegt, nachdem ein neues Dokument in SharePoint hochgeladen wird.
- Dieses Muster gilt nur für neue Dokumente in SharePoint hochgeladen, nicht eindeutige Bezeichnern für Dokumente, die bereits in SharePoint gespeicherten fest.
- Upload Mengenoperationen werden mehrere Aufrufe an den Dienst zugeordnet der remote-Ereignisempfänger ausgelöst. Planen Sie entsprechend um sicherzustellen, dass Mengenoperationen hochladen den Dienst nicht überlastet.
- Es gibt keine Möglichkeit für einen remote-Ereignisempfänger SharePoint zu benachrichtigen, wenn eine einzigartige Dokument-ID konnte nicht festlegen.

**Wenn sie geeignet ist?**

Wenn Sie eindeutige Bezeichner für Dokumente schnell festgelegt, wenn für SharePoint hochladen, und Sie nicht hochladen Mengenoperationen erwarten müssen.

**Erste Schritte**

[Ereignisempfänger und Liste-Ereignisempfänger (SharePoint-Add-in-Anleitung)](event-receiver-and-list-event-receiver-sharepoint-add-in.md) wird beschrieben, wie Ereignisempfänger im Add-In-Modell zu implementieren, und enthält Links zu mehreren Artikeln und Beispiele.

<a name="use-a-background-process"></a>Verwenden Sie einen Hintergrundprozess
------------------------
In diesem Muster überprüft Prozess im Hintergrund Dokumente in SharePoint zu ermitteln, ob sie einen eindeutigen Bezeichner festgelegt haben. Wenn keine Eindeutiger Bezeichner für ein Dokument gefunden wird, wird der Hintergrund-Prozess einen eindeutigen Bezeichner für das Dokument. Der Hintergrund-Prozess macht CSOM oder REST-API aufruft, um die eindeutigen IDs für Dokumente festgelegt.

- Dieses Muster wird entsprechend den dafür festgelegten Zeitplan ausgeführt.
- Dieses Muster wirkt sich auf alle Dokumente, die zum Durchforsten der Code geschrieben ist.
- Wir empfehlen die Verwendung des SharePoint-Suchdiensts zum Ausführen von Abfragen, die enthalten Filter zum Zurückgeben einer Liste von Dokumenten, die keine eindeutige Bezeichnern für sie festgelegt haben.
    + Dieses Muster führt der schnellsten und Skalen Abfragen eine höhere Leistung als andere Muster.
    + Dieses Muster entfällt benutzerdefinierte Abfragelogik aus dem Hintergrunddienst.
    + Dieses Muster erfordert einige Suchkonfiguration.

        Weitere Informationen zum Konfigurieren der Suche finden Sie die [Suchkonfiguration (SharePoint-Add-in-Anleitung)](search-configuration-sharepoint-add-in.md).
- Es wird nicht rekursiv Abfragen und return Metadaten für alle Dokumente in einer SharePoint-Umgebung empfohlen, durch Web- und Liste Objekte durchlaufen.
    + Dieses Muster führt die langsamste und Skalen schlechter als andere Abfragen Muster.  
    + API steuerungsgrenzwerte für auftreten, wenn dieses Muster verwenden.
    + In diesem Muster enthält benutzerdefinierte Abfragelogik im Hintergrunddienst.
    + Dieses Muster kann mit einer Azure-Web-Projekt implementiert werden.

**Wenn sie geeignet ist?**

- Wenn Sie legen Sie eindeutige Bezeichner für Dokumente und remote-Ereignisempfänger müssen sind keine Option zur Verfügung.
- Wenn Sie erwarten, dass Dokumente in einer Sammeloperation hochgeladen haben.
- Wenn Sie benötigen, um sicherzustellen, dass werden einzigartige Dokument-IDs für Dokumente festgelegt.
    + Es gibt keine Möglichkeit für einen Ereignisempfänger SharePoint zu benachrichtigen, wenn eine einzigartige Dokument-ID konnte nicht festlegen.
- Wenn Sie bereits in SharePoint gespeicherten Dokumente verarbeiten müssen.

**Erste Schritte**

Die [Remote Zeitgeberaufträge (SharePoint-Add-in-Anleitung)](remote-timer-jobs-sharepoint-add-in.md) beschreibt, wie Sie remote Zeitgeberaufträge im Add-In-Modell zu implementieren und enthält Links zu mehreren Artikeln und Beispiele.

<a name="related-links"></a>Verwandte links
=============
- [Ereignisempfänger und Liste-Ereignisempfänger (Anleitung SharePoint-Add-Ins)](event-receiver-and-list-event-receiver-sharepoint-add-in.md)
- [Konfigurieren der Suche (SharePoint-Add-Ins Anleitung)](search-configuration-sharepoint-add-in.md)
- [Remote Zeitgeberaufträge (SharePoint-Add-Ins Anleitung)](remote-timer-jobs-sharepoint-add-in.md)
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
