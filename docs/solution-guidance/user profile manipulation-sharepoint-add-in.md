---
title: Profil Bearbeitung durch den Benutzer im SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 6512313eb59dc62cab4f09d109a3b67f87e67b68
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="user-profile-manipulation-in-the-sharepoint-add-in-model"></a>Profil Bearbeitung durch den Benutzer im SharePoint-add-in-Objektmodell
========================================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zur Durchführung von Create, Read, Update und Delete (CRUD) Vorgänge in User Profile Service (USV) unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war. In einer typischen vollständige vertrauen Code (FTC) / Farmlösung-Szenario wurden USV CRUD-Vorgänge mit SharePoint Server-Side-Objektmodellcode ausgeführt oder der Benutzerprofildienst-Webdienst und über Farmlösungen bereitgestellt. 

In einem Szenario mit SharePoint-Add-Ins Modell werden USV CRUD-Vorgänge mit dem clientseitigen Objektmodell (CSOM) oder der Benutzerprofildienst-Webdienst ausgeführt.  

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt empfehlen wir die folgenden allgemeinen Richtlinien für die Durchführung von USV CRUD-Vorgänge.

- In der folgenden Tabelle wird beschrieben, welche Arten von Vorgängen in Office 365 und lokale SharePoint-Umgebungen für die CSOM und Benutzerprofil Web Service-APIs unterstützt werden.

    Vorgang  | API | Lokal | Office 365
    ---------| -----| ---------| ------
    LESEN | CSOM | Unterstützt | Unterstützt
    ERSTELLEN | CSOM | Nicht unterstützt | Unterstützt
    UPDATE | CSOM | Nicht unterstützt | Unterstützt
    DELETE | CSOM | Nicht unterstützt | Unterstützt
    LESEN | Benutzerprofildienst-Web | Unterstützt | Nicht unterstützt
    ERSTELLEN | Benutzerprofildienst-Web | Unterstützt | Nicht unterstützt
    UPDATE | Benutzerprofildienst-Web | Unterstützt | Nicht unterstützt
    DELETE | Benutzerprofildienst-Web | Unterstützt | Nicht unterstützt

- Sie werden in der Regel ein Add-in einer SharePoint-Mandanten USV Kopieren von Daten behandelt oder Synchronisierung nicht bereitgestellt.  In der Regel ist das Add-in Form von eine Konsolenanwendung, die als geplante Aufgabe oder ein langer Cloud-Dienst wie ein Azure Webauftrag ausgeführt.
    + Finden Sie unter [Remote Zeitgeberaufträge (SharePoint-Add-in Modell Anleitung)](remote-timer-jobs-sharepoint-add-in.md) für Weitere Informationen zu diesen Technologien und wie sie in der SharePoint-Add-in-Objektmodell verwenden.
- Verwendung AppOnly ist Authentifizierung nicht für alle User Profile Service-Vorgänge unterstützt.
- Führen Sie den CSOM-Code mit einem Konto mit den entsprechenden Berechtigungen zur Ausführung der USV CRUD-Vorgänge aus.
- Bei der Synchronisierung von Active Directory, um den Benutzerprofildienst werden einige Attribute standardmäßig synchronisiert.
    + Die [standardmäßigen Zuordnungen der Benutzerprofileigenschaften in SharePoint Server 2013 (TechNet-Artikel)](https://technet.microsoft.com/en-us/library/hh147510.aspx) enthält eine Liste der Attribute standardmäßig synchronisiert.
    + Wenn Sie zusätzliche Attribute synchronisieren müssen müssen Sie ein benutzerdefiniertes Tool mit einer der in diesem Artikel beschriebenen Vorgehensweisen zu erstellen.

<a name="options-to-copy-and-synchronize-ups-data"></a>Optionen zum Kopieren und Synchronisieren von Daten (USV)
----------------------------------------

Sie haben eine Reihe von Optionen zum Kopieren und Synchronisieren von Daten (USV).

- Der lokale
    + Kopieren Sie die Datenbank
    + Verwenden Sie den Benutzerprofildienst Web zum Kopieren von Daten
    + Verwenden Sie den Benutzerprofildienst Web zum Synchronisieren von Daten
- Office 365
    + Verwenden Sie CSOM, um Daten zu kopieren
    + Verwenden Sie CSOM, um Daten synchronisieren

<a name="on-premises---copy-database"></a>Der lokale - Datenbank kopieren
---------------------------
Wenn Sie eine lokale SharePoint-Umgebung verfügen können Sie die USV-Datenbank von einer Farm in eine andere Attribute schnell replizieren kopieren.

**Wenn sie geeignet ist?**

Wenn Sie über eine lokale SharePoint-Umgebung verfügen, und Sie eine unidirektionale Kopie der Benutzerprofil-Attribute durchgeführt werden, ist dies eine gute Wahl, da sie schnell implementiert werden kann und auf einfache Weise ohne Schreiben von Code.

<a name="on-premises---use-the-user-profile-web-service-to-copy-data"></a>Lokale - verwenden Sie den Benutzerprofildienst Web zum Kopieren von Daten
-----------------------------------------------------------
Wenn Sie eine lokale SharePoint-Umgebung verfügen können Sie den Benutzerprofildienst Web, USV Daten von einer Farm in eine andere kopiert.

**Wenn sie geeignet ist?**

Wenn Sie über eine lokale SharePoint-Umgebung verfügen, und Sie USV Daten zwischen mindestens zwei SharePoint-Farmen kopieren ist dies eine gute Wahl, da Sie die Flexibilität, die USV Daten aus einer Farm in eine andere kopiert eine.

**Erste Schritte**

Im folgende Beispiel wird gezeigt, wie USV CRUD-Vorgänge mit der Benutzerprofildienst Web ausführen.

- [Core.UserProfilePropertyUpdater (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.UserProfilePropertyUpdater)

<a name="on-premises---use-the-user-profile-web-service-to-sync-data"></a>Lokale - verwenden Sie den Benutzerprofildienst Web zum Synchronisieren von Daten
-----------------------------------------------------------
Wenn Sie eine lokale SharePoint-Umgebung verfügen können Sie den Benutzerprofildienst Web, USV Daten zwischen Farmen zu synchronisieren.

**Wenn sie geeignet ist?**

Wenn Sie eine lokale SharePoint-Umgebung und Sie USV Daten zwischen mindestens zwei SharePoint-Farmen synchronisieren ist dies eine gute Wahl, da es Sie, die Flexibilität auf true Synchronisierung ausführen und wie viele Quellen wie gewünscht.

**Erste Schritte**

Die [Core.UserProfilePropertyUpdater (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.UserProfilePropertyUpdater) wird gezeigt, wie USV CRUD-Vorgänge mit der Benutzerprofildienst Web auszuführen.

Die [Core.MMSSync (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync) wird gezeigt, wie eine Synchronisierungstool for Managed Metadata Service (MMS Daten) zu erstellen.  Obwohl in diesem Beispiel auf die MMS-APIs konzentriert, kann das allgemeine Muster für die Synchronisierung auf USV Daten als auch angewendet werden.

<a name="office-365---use-csom-to-copy-data"></a>Office 365 - CSOM zum Kopieren von Daten verwenden
----------------------------------
Wenn Sie eine Office 365 SharePoint-Umgebung haben können Sie CSOM, USV Daten aus einem Mandanten in eine andere kopiert.  

**Wenn sie geeignet ist?**

Wenn Sie eine Office 365-Umgebung verfügen, und Sie USV Daten zwischen mindestens zwei SharePoint-Mandanten kopieren ist dies eine gute Wahl, da Sie die Flexibilität, die USV Daten aus einem Mandanten in eine andere kopiert eine.

**Erste Schritte**

Die [UserProfile.Manipulation.CSOM (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM) wird gezeigt, wie USV CRUD-Vorgänge mit CSOM auszuführen.

Das [Benutzerprofil CSOM zum Lesen und Updates (Office 365 Plug & Play-Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/User-profile-CSOM-for-reading-and-updates) führt Sie durch die [UserProfile.Manipulation.CSOM (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM).

<a name="office-365---use-csom-to-sync-data"></a>Office 365 - CSOM zum Synchronisieren von Daten verwenden
----------------------------------
Wenn Sie eine Office 365 SharePoint-Umgebung und Sie USV Daten zwischen zwei oder mehr Mandanten synchronisieren ist dies eine gute Wahl, da es Sie, die Flexibilität auf true Synchronisierung ausführen und wie viele Quellen wie gewünscht.

**Wenn sie geeignet ist?**

Wenn Sie eine Office 365-Umgebung und Sie USV Daten zwischen mindestens zwei SharePoint-Mandanten synchronisieren ist dies eine gute Wahl, da es Sie, die Flexibilität auf true Synchronisierung ausführen und wie viele Quellen wie gewünscht.

**Erste Schritte**

Die [Core.UserProfiles.Sync (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.UserProfiles.Sync) wird gezeigt, wie eine-Synchronisierungstools zur Benutzerprofildienst-Daten erstellen.

<a name="hybrid-environments"></a>Hybridumgebungen
-------------------

In einem Szenario, in denen Sie lokalen und Office 365 SharePoint-Umgebungen und von Benutzerprofilinformationen über, muss, mit denen Sie eine Kombination aus der Benutzerprofildienst Web und dem Clientobjektmodell können Sie die Möglichkeit zum Ausführen von CRUD Bereitstellen in beiden Umgebungen verwaltet werden Vorgänge für USV Daten.

<a name="related-links"></a>Verwandte links
=============
- [Benutzerprofil-CSOM zum Lesen und Updates (Office 365 Plug & Play-Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/User-profile-CSOM-for-reading-and-updates)
- [Remote Zeitgeberaufträge (SharePoint-Add-in-Modell Anleitung)](remote-timer-jobs-sharepoint-add-in.md)
- [Standardmäßigen Zuordnungen der Benutzerprofileigenschaften in SharePoint Server 2013 (TechNet-Artikel)](https://technet.microsoft.com/en-us/library/hh147510.aspx)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================
- [Core.UserProfilePropertyUpdater (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.UserProfilePropertyUpdater)
- [Core.MMSSync (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync)
- [UserProfile.Manipulation.CSOM (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM)
- [Core.UserProfiles.Sync (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.UserProfiles.Sync) 
- Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D)
- SharePoint 2013 lokal
