---
title: Websitespalten und Inhaltstypen in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 3d8ea299a9a78fc4ee9ab5bf90ee34a8f242ef8f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="site-columns-and-content-types-in-the-sharepoint-add-in-model"></a>Websitespalten und Inhaltstypen in der SharePoint-add-in-Objektmodell
=============================================================

<a name="summary"></a>Summary
-------

Die Vorgehensweise zum Erstellen von Websitespalten und Inhaltstypen in SharePoint-Websites unterscheidet sich im neuen SharePoint-Add-in-Modell befand mit vollständigen Code, der als vertrauenswürdig. In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario Sie deklarativen Code zum Erstellen von Websitespalten und Inhaltstypen verwenden. In der deklarativen Code Ansatz Sie definieren der Websitespalten und Inhaltstypen in XML-Datei und dann SharePoint Feature Frameworkelemente zu packen und bereitstellen.

In einem Modell Szenario SharePoint-Add-in verwenden Sie die SharePoint-Client Side-Objekt Objektmodell (CSOM) oder die SharePoint-REST-APIs zum Erstellen von Websitespalten und Inhaltstypen.

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt empfehlen wir die folgenden allgemeinen Richtlinien für das Erstellen von Websitespalten und Inhaltstypen.

- Sie sollten die SharePoint-CSOM oder REST-APIs zum Erstellen von Websitespalten und Inhaltstypen verwenden.
- Sie sollten nicht featureelementen Framework verwenden, um Websitespalten und Inhaltstypen zu erstellen.
    + Die einzige Ausnahme dieser Richtlinie wird bei Verwendung der deklarativen XML-basierte bereitstellen auf einer SharePoint-Add-Ins Web in ein SharePoint-hosted SharePoint Add-in. Dies ist die Tatsache, dass das CSOM nicht in einer SharePoint-hosted SharePoint Add-in zur Verfügung steht.
- Sie können das Erstellen von Websitespalten und Inhaltstypen als Teil der Website Bereitstellungsprozesses automatisieren. Finden Sie unter der [Website provisioning Anleitung](site-provisioning-sharepoint-add-in.md) für weitere Details.

<a name="challenges-creating-site-columns-and-content-types-in-sharepoint-sites"></a>Erstellen von Websitespalten und Inhaltstypen in SharePoint-Websites Probleme
----------------------------------------------------------------------

**Erstellen Sie in einem Webbrowser im Vergleich zu erstellen, mit code** 

Es ist wichtig um zu verstehen, dass das Erstellen von Websitespalten und Inhaltstypen über den Webbrowser oder über Code unterscheiden sich. In dieser Liste werden die verschiedenen Optionen beschrieben.

- **Erstellen über einen Webbrowser**
    + Bei dieser Option werden Benutzer auf eine SharePoint-Website über einen Webbrowser zugreifen und verwenden Sie die Administrative Seiten zum Erstellen von Websitespalten und Inhaltstypen.
    + In der Regel nur dann werden Sie den Webbrowser verwenden, um manuell erstellen von Websitespalten und Inhaltstypen ist bei Prototypen oder Ändern einer einzelnen SharePoint-Website, die nicht eingeschlossen andere Websitesammlungen oder Websites sub wachsen geplant ist.
- **Erstellen mithilfe von code**
    + Bei dieser Option führen Sie die SharePoint-CSOM/REST-Code zum Erstellen von Websitespalten und Inhaltstypen.
    + Weiter unten in diesem Artikel Sie über einige Optionen erfahren können Sie den SharePoint-CSOM/REST-Code ausführen.

Beim **Erstellen von über einen Webbrowser**, berücksichtigen Sie die folgenden Punkte.

- Erstellen von Websitespalten und Inhaltstypen über das Web-Browser ist in der Regel ein Prozess kompliziert und zeitraubend.
    + Diese Faktoren machen es **fehleranfällig**.
- Steuern Sie nicht die GUIDs für Websitespalten oder Inhaltstypen, die Sie über einen Webbrowser zu erstellen.
    + **Dies erschwert die Websitespalten, Inhaltstypen auf unterschiedliche Umgebungen bereitstellen und konsistent in Line-of-Business Applications verweisen.**

Beachten Sie beim **erstellen mithilfe von Code** die folgenden Punkte.

- Erstellen von Websitespalten und Inhaltstypen mit Code in der Regel beinhaltet die Verwendung von benutzerdefinierten Dienstprogramm-Bibliotheken, SharePoint-CSOM/REST Code auszuführen.
    + Im Repository OfficeDev Plug & Play-GitHub finden Sie diese Bibliotheken in viele Projekte verfügbar.  Sie sind in der gesamten Artikel und am Ende verwiesen.
    + Diese Faktoren machen Erstellen von Websitespalten und Inhaltstypen mit Code **anfällig für Erfolg**.
- Sie können steuern, die GUIDs für Websitespalten oder Inhaltstypen, die über die SharePoint-CSOM/REST erstellt werden.
    + **Dies vereinfacht die Websitespalten, Inhaltstypen auf unterschiedliche Umgebungen bereitstellen und konsistent in Line-of-Business Applications verweisen.**

**Muss schnell passieren!**

Sie erstellen in der Regel von Websitespalten und Inhaltstypen, wenn Sie eine SharePoint-Website bereitstellen. Endbenutzer werden nicht akzeptiert, müssen Sie ihre neue SharePoint-Websites bereitstellen mehrere Stunden zu warten.

**Muss konsistent perfekte!**

Websitespalten und Inhaltstypen sind Fundament dar, das die Informationsarchitektur auf der untersten Ebene, *muss es sich um perfekte*definieren.

Falsche Websitespalte sowie die Bereitstellung von Inhaltstyp auswirken können, eine gesamte LOB Anwendung in der SharePoint-Website, in dem sie bereitgestellt werden, sowie andere Teile von SharePoint, und anderen Line-of-Business-Clientanwendungen, die Zugriff auf SharePointServices .

Beispiel: Wenn Ihr Unternehmen SharePoint-Websites zum Verwalten von Projekten verwendet, in den meisten Fällen erstellen Sie eine allgemeine Listenschema für alle. Dafür ist erforderlich, dass Sie Websitespalten und Inhaltstypen erstellen.  Wenn Sie Informationen in diesen Websites über die SharePoint-Suchseite suchen, Filtern Sie die Ergebnisse nach Inhaltstyp oder Tag (Websitespalte). Wenn Ihre Websitespalten und Inhaltstypen nicht perfekt konsistent auf allen Projektwebsites sind, erhalten Sie nicht präzise Suchergebnisse.

Sie können dieses Beispiel Content von Such-Webparts, SharePoint-add-ins, anwenden mobile SharePoint-Add-ins und allen anderen Systemen, die die Informationen in der SharePoint-Websites zugreifen.

<a name="options-to-create-site-columns-and-content-types-in-sharepoint-sites"></a>Optionen zum Erstellen von Websitespalten und Inhaltstypen in SharePoint-Websites
--------------------------------------------------------------------

Sie haben verschiedene Möglichkeiten, die Sie den CSOM/REST-Code zum Erstellen von Websitespalten und Inhaltstypen aufrufen können. Diese Muster an, die alle in der oben beschriebenen **Erstellen mit Code** Ansatz fallen. Sie sehen die jeweils diese Muster der [Site provisioning Anleitung](site-provisioning-sharepoint-add-in.md)ausführlich beschrieben.

- Überschreiben Sie den Link der Website erstellen
- Überschreiben Sie den Link erstellen Sub-Website
- Verwenden einer vom Anbieter gehosteten SharePoint Add-Ins
- Verwenden Sie Windows/Java/iOS Applications oder PowerShell-Skripts

Unabhängig von der gewählten Option implementieren, werden Sie CSOM/REST letztlich zum Erstellen von Websitespalten und Inhaltstypen verwenden.

Es gibt zahlreiche verschiedene Artikel und Beispiele, die Sie verwenden können, um zu erfahren, wie Websitespalten und Inhaltstypen mit dem Clientobjektmodell können. Hier finden Sie in diesen Beispielen (klassifiziert durch das Muster, das zum Aufrufen des CSOM-Codes verwendet wird) zum Erstellen von Websitespalten und Inhaltstypen.

<a name="use-a-provider-hosted-sharepoint-add-in"></a>Verwenden einer vom Anbieter gehosteten SharePoint Add-Ins
---------------------------------------
Diese Option funktioniert gut, wenn Sie Ihre Endbenutzer mit einem Self-service Möglichkeit zum Erstellen von SharePoint-Websitesammlungen und Websites basierend auf benutzerdefinierten Vorlagen sub bereitstellen müssen.

- [Core.ContentTypesAndFields (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ContentTypesAndFields)
    + Veranschaulicht das Erstellen eines neuen Inhaltstyps im hostweb, erstellen eine Taxonomie-Felds im hostweb und bis zu der Taxonomie zu verknüpfen, erstellen Sie eine Liste und einen Inhaltstyp zuordnen und Erstellen von Inhaltstypen und Felder in bestimmten Sprachen.

<a name="use-windowsjavaios-applications-or-powershell-scripts"></a>Verwenden Sie Windows/Java/iOS Applications oder PowerShell-Skripts
-------------------------------------------------------

Diese Option eignet sich für Dev-Vorgängen in Szenarien. Es ermöglicht Ihnen das Erstellen benutzerdefinierter Anwendungen oder Skripts, die speziell für die Verwendung mit Ihrer Prozesse Dev-Vorgängen in integriert sind. Diese Option bietet die höchste Stufe der Automatisierung, da Sie die SharePoint-Add-ins und ohne Eingriffe des Benutzers Ausführen von Skripts erstellen können.  

- [Core.CreateContentTypes (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes)
    + Dieses Beispiel zeigt, wie Sie können Erstellen von Websitespalten, Inhaltstypen und dann hinzufügen die Websitespalten für den Inhaltstyp. Darüber hinaus die neuen Lokalisierungsfeatures, die für Office 365-CSOM-APIs eingeführt wurden.
- [Core.CreateDocumentContentType (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateDocumentContentType)
    + Dieses Beispiel zeigt, wie Sie können Inhaltstypen Dokument erstellen und dann eine Zuordnen einer Dokumentvorlage für den Inhaltstyp.

<a name="related-links"></a>Verwandte links
=============
- [Der websitebereitstellung im SharePoint-add-in-Modell (O365 Plug & Play-Anleitung)](site-provisioning-sharepoint-add-in.md)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [Core.CreateContentTypes (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes)
- [Core.ContentTypesAndFields (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ContentTypesAndFields)
- [Core.CreateDocumentContentType (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateDocumentContentType)
- [Branding.DisplayTemplates (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.DisplayTemplates)
- [Core.DataStorageModels (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels)
- Beispiele und Inhalte am [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D) *teilweise*
- SharePoint 2013 lokal – *teilweise*

*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*
