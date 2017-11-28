---
title: Lokalisierung in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 33a39ac3c656c9de086432da14ce6fa6cac34870
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="localization-in-the-sharepoint-add-in-model"></a>Lokalisierung in der SharePoint-add-in-Objektmodell
===========================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Implementieren der Lokalisierung für Add-ins unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war. In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario, Lokalisierung für benutzerdefinierte Komponenten wie Webparts, Benutzersteuerelemente und Websteuerelemente mit einer Kombination von Ressourcendateien, verwalteter Code, Eigenschaften und deklarativen Code implementiert wurde.  In Features, die über den SharePoint-Lösungen bereitgestellt wurden alle Artefakte gepackt.

In einem Modell Szenario SharePoint-Add-in verwenden Sie JavaScript oder der Lokalisierung Funktionen der Web-Technologie, wenn, der Sie die Add-ins mit Lokalisierung implementieren erstellen, zugeordnet. Je nach den lokalisierten Ressource können Sie auch klassische Ressourcendateien verwenden, beispielsweise wenn müssen Sie Lozalize-Elemente mithilfe von featureelementen Framework in der Definition-Add-in-Add-in-Web bereitgestellt.

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien für die Implementierung der Lokalisierung bereitzustellen.

- Sie müssen die entsprechenden Language Packs in Ihre lokale SharePoint- und Office 365-Umgebungen ermöglichen Benutzern das Erstellen von Websites in eine bestimmte Kultur und Sprache installieren.
- Verwenden von JavaScript Lokalisierung in SharePoint-Add-ins implementiert ist auch ein Ansatz, mit denen Sie Inhalte im Skript-Editor-Add-in Webparts lokalisieren können. 

<a name="localization-scenarios"></a>Lokalisierung Szenarien
----------------------

Es gibt zwei verschiedene Szenarien, in dem Sie Lokalisierung für ein Add-In implementieren müssen.

- SharePoint-Hosting-Add-ins
- Vom Anbieter gehosteten-Add-ins

<a name="add-in-web-components-or-assets"></a>Add-Ins Web Components oder Objekte
-------------------------
In diesem Szenario wird die Lokalisierung auf das Add-in über JavaScript angewendet.

- SharePoint-Hosting-Add-ins haben keinen Zugriff auf Server-basierte Ressourcendateien in den SharePoint-Servern, aber Sie haben Zugriff auf die Feature-Element Resx-Dateien 
- Die Vorgehensweise zum Lokalisieren eines SharePoint-Hosting-Add-Ins und ein Office-Add-in sind sehr ähnlich, da beide JavaScript verwenden.

**Wenn sie geeignet ist?**

Beim Erstellen eines SharePoint-Hosting-Add-Ins wird mithilfe von JavaScript Ihre optimale Breite, da Sie JavaScript-Lokalisierung implementieren und alle erforderlichen zur Unterstützung der Lokalisierung mit dem SharePoint-Hosting-Add-in JavaScript-Dateien bereitstellen können. Sie können auch diesem Ansatz nutzen, wenn das vom Anbieter gehosteten-add-in auch bestimmte-add-ins Web enthält.

**Erste Schritte**

Szenario 2 in der [Core.JavaScriptCustomization (O365 Plug & Play-Beispiel))](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) wird gezeigt, wie JavaScript verwenden, um den Text in ein Add-in als auch die HTML-Elemente in das Add-in zugeordneten Attribute lokalisieren.

Die [Lokalisieren von SharePoint-Add-ins](https://msdn.microsoft.com/en-us/library/fp179919(v=office.15).aspx) wird veranschaulicht, wie JavaScript für die Lokalisierung von Ressourcen im Web-Add-in verwenden.

<a name="remote-components"></a>Remotekomponenten
-------------------------
In diesem Szenario gilt Lokalisierung für das Add-in über die Lokalisierung Technologien mit der Web-Technologie hosten das Add-in verknüpft ist.

- Wenn ASP.NET verwendet wird, um das Add-in zu implementieren, werden Ressourcendateien und JavaScript-Dateien für die Lokalisierung von es verwendet.
- Wenn eine andere Technologie wie PHP, Python oder Ruby werden verwendet, um das Add-in zu implementieren die Lokalisierung-Funktionen, die diesen Plattformen zugeordnet verwendet.

**Wenn sie geeignet ist?**

Wenn Sie ein vom Anbieter gehosteten-Add-in erstellen, ist mithilfe der Lokalisierung-Technologie, die mit dem Web Hostingplattform kommt die am besten passt, da Sie das Add-in auf eine Weise erstellen, die kein benutzerdefinierten Code oder zusätzliche Komplexität einleitet.

**Erste Schritte**

In den folgenden Artikeln wird beschrieben, wie vom Anbieter gehosteten-Add-ins mit Ressourcendateien und JavaScript lokalisieren.

- [Lokalisieren von SharePoint-Add-ins (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/fp179919(v=office.15).aspx)
- [Lokalisieren Sie die Add-ins Web, Hostwebsite und Remotekomponenten ein Add-in (MSDN Code Sample)](https://code.msdn.microsoft.com/office/SharePoint-2013-Bookstore-328060fc)

<a name="related-links"></a>Verwandte links
=============

- [Lokalisieren von SharePoint-Add-ins (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/fp179919(v=office.15).aspx)
- [Lokalisieren Sie die Web-Add-in, Host-Web und Remotekomponenten ein Add-in (Office Dev GitHub-Beispiel)](https://github.com/SharePoint/SharePoint-Add-in-Localization)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [VariationsExtensions.cs-Klasse (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core/OfficeDevPnP.Core/AppModelExtensions/VariationExtensions.cs)
- Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D)
- SharePoint 2013 lokal
