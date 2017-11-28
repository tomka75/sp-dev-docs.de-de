---
title: Bearbeiten von MMS in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 0d1509b65fcd33068182b3747f21e1cb1db86238
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="mms-manipulation-in-the-sharepoint-add-in-model"></a>Bearbeiten von MMS in der SharePoint-add-in-Objektmodell
===============================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zur Durchführung von Create, Read, Update und Delete (CRUD) Vorgänge in Managed Metadata Service (MMS) unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war. In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario MMS CRUD-Vorgänge wurden mit SharePoint Server-Side-Objektmodellcode ausgeführt und über Farmlösungen bereitgestellt. 

In einem Szenario mit SharePoint-Add-Ins Modell werden MMS CRUD-Vorgänge mit dem clientseitigen Objektmodell (CSOM) ausgeführt.

**Das CSOM enthält alle Vorgänge zum Replizieren und Synchronisieren von Daten in die MMS erforderlich.**

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt empfehlen wir die folgenden allgemeinen Richtlinien für die Durchführung von MMS CRUD-Vorgänge.

- MMS CRUD-Vorgänge sollte mit dem clientseitigen Objektmodell implementiert werden.
- Führen Sie den CSOM-Code mit einem Konto mit den entsprechenden Berechtigungen zur Ausführung von MMS CRUD-Vorgänge aus.
- Bei der Begriff Synchronisierung legt die ChangeInformation-Klasse verwendet werden, da es eine höhere Leistung führt als GetAllTerms verwenden und Auflisten der Begriffe jedes Mal, wenn Sie synchronisieren möchten. 


<a name="options-to-copy-and-synchronize-mms-data"></a>Optionen zum Kopieren und Synchronisieren von MMS-Daten
----------------------------------------

Sie haben verschiedene Optionen zum Kopieren und Synchronisieren von MMS-Daten.

- Der lokale
    + Kopieren Sie die Datenbank
    + Verwenden Sie CSOM, um Daten zu kopieren
    + Verwenden Sie CSOM, um Daten synchronisieren
- Office 365
    + Verwenden Sie CSOM, um Daten zu kopieren
    + Verwenden Sie CSOM, um Daten synchronisieren

<a name="on-premises---copy-database"></a>Der lokale - Datenbank kopieren
---------------------------
Wenn Sie eine lokale SharePoint-Umgebung verfügen können Sie die MMS-Datenbank von einer Farm in eine andere Begriffe schnell replizieren kopieren.

**Wenn sie geeignet ist?**

Wenn Sie über eine lokale SharePoint-Umgebung verfügen, und Sie eine unidirektionale Kopie von Ausdrücken durchgeführt werden, ist dies eine gute Wahl, da sie schnell und einfach implementiert werden kann, ohne Code schreiben.

<a name="on-premises--o365---use-csom-to-copy-data"></a>Lokale & O365 - CSOM verwenden, um Daten zu kopieren
------------------------------------------
Wenn Sie einem lokalen oder Office 365 SharePoint-Umgebung können CSOM zum Kopieren von MMS-Daten aus einer Farm-Instanz in eine andere.  ***Sie können die lokalen und Office 365-Farmen mit diesem Ansatz einschließen.***

**Wenn sie geeignet ist?**

Wenn Sie eine lokale SharePoint oder Office 365 oder eine hybridumgebung, und Sie werden MMS Daten zwischen mindestens zwei SharePoint-Farmen/Mandanten kopieren, ist dies eine gute Wahl, da Sie die Flexibilität, die MMS-Daten aus einer Farm in eine andere kopiert eine.

**Erste Schritte**

Im folgende Beispiel veranschaulicht, wie MMS CRUD-Vorgänge auszuführen.

- [Core.MMS (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS)

<a name="on-premises--o365---use-csom-to-sync-data"></a>Lokale & O365 - CSOM zum Synchronisieren von Daten verwenden
------------------------------------------
Wenn Sie eine lokale SharePoint-Umgebung verfügen, können Sie CSOM auf Sync MMS Daten zwischen Farmen verwenden. ***Sie können die lokalen und Office 365-Farmen/Mandanten mit diesem Ansatz einschließen.***

**Wenn sie geeignet ist?**

Wenn Sie ein lokales SharePoint oder Office 365 oder eine hybridumgebung und Sie Daten zwischen zwei oder mehr SharePoint-Farmen/Mandanten MMS synchronisiert werden, ist dies eine gute Wahl, da es Sie, die Flexibilität auf true Synchronisierung durchführen, und fügen Sie als viele Quellen aus.

**Erste Schritte**

Im folgende Beispiel wird gezeigt, wie eine Synchronisierungstool für MMS Daten erstellen.

- [Core.MMSSync (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync)

<a name="related-links"></a>Verwandte links
=============
- [Synchronisieren von Ausdruckssätzen mit CSOM (MSDN-Blog-Artikel Dokumentation)](http://blogs.msdn.com/b/frank_marasco/archive/2014/06/29/synchronize-term-sets-with-the-term-store-csom.aspx)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [Core.MMS (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS)
- [Core.MMSSync (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync)
- Beispiele und Inhalte am [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D) *teilweise*
- SharePoint 2013 lokal – *teilweise*

*Muster für dedizierte und lokalen sind identisch mit-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*
