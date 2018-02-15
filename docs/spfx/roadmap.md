---
title: SharePoint-Framework-Roadmap
description: "Wichtige moderne Anpassungsfunktionen nach der Version mit allgemeiner Verfügbarkeit veröffentlicht"
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: 8b50c0a6ec81f27001d9abafc5e8a9e0a2fa957e
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="sharepoint-framework-roadmap"></a>SharePoint-Framework-Roadmap

Die Erstveröffentlichung von SharePoint-Framework enthielt nur Unterstützung für clientseitige Webparts. Dies war jedoch nur der Beginn der Bereitstellung zusätzlicher moderner Anpassungsfunktionen für SharePoint. Im Folgenden werden die wichtigsten Funktionen aufgeführt, die nach der Version mit allgemeiner Verfügbarkeit veröffentlicht wurden:

- [Unterstützung für mandantenweite Bereitstellung](./tenant-scoped-deployment.md)
- [Lokale Unterstützung für SharePoint 2016 (Feature Pack 2)](./sharepoint-2016-support.md)
- [SharePoint-Framework-Erweiterungen](./extensions/overview-extensions.md)
- [Mandanteneigenschaften](./tenant-properties.md)
- [Application Lifecycle Management (ALM)-APIs für SPFx Lösungen und Add-Ins](../apis/alm-api-for-spfx-add-ins.md)
- [Unterstützung für Office UI Fabric Core](https://dev.office.com/blogs/improved-support-for-office-ui-fabric-core)
- [Verpacken von Objekten und Websitesammlungs-App-Katalog](../general-development/site-collection-app-catalog.md)


> [!NOTE]
> Dies ist eine Liste von Bereichen, die von den SharePoint-Entwicklern abgearbeitet und untersucht werden. Das bedeutet **NICHT**, dass all diese Bereiche tatsächlich bereitgestellt werden, wir bemühen uns jedoch, Elemente und Themen aus dieser Liste in den künftigen Versionen von SharePoint-Framework schrittweise zu veröffentlichen.

## <a name="general-improvements"></a>Allgemeine Verbesserungen

- Einfacher Zugriff auf die Graph-API zum Zugreifen auf benutzerspezifische Informationen (GraphHttpClient in der Vorschau)
- Webhooks auf Website-Ebene
- Textabschnitt zum Store mit Unterstützung für SharePoint-Framework aktualisiert
- Textabschnitt zum Store für SharePoint-Framework-Lösungen mit einfachem Vertriebskanal für ISVs 

## <a name="client-side-web-parts-and-add-ins"></a>Clientseitige Webparts und Add-Ins

- Unterstützung für komplexere Szenarios und Interaktionen mit Webparts
    - Kommunikation von Webpart zu Webpart
    - JavaScript-Framework-Isolierung
    - „Citizen Developer“-Modell für einfache Entwicklung

- Add-Ins für die moderne Welt: Ansprechendere Wiedergabe mit der neuen UX.
    - Azure AD-Registrierung
    - Native, reaktionsschnelle Unterstützung
    - Erstellen von Add-Ins mit SharePoint-Framework


## <a name="application-lifecycle-management"></a>Application Lifecycle Management

- Optimierte Genehmigungsoberfläche: Sie müssen nicht mehr wissen, wer Ihr Mandantenadministrator ist.
    - Besitzer initiiert den Genehmigungsprozess.
    - Mandantenadministrator wird automatisch benachrichtigt.
    - Einstellungen zum Steuern der Standardoberfläche um den Genehmigungsprozess herum.


## <a name="developer-experience"></a>Entwickleroberfläche

- SharePoint-Framework-Workbench 2.0: Entwicklungsgeschichte für SharePoint-Framework-Erweiterungen
- Komponenten der Toolkette
- Zusätzliche Yeoman-Vorlagen

## <a name="already-shipped-capabilities"></a>Bereits ausgeliefert Funktionen

In den folgenden Abschnitten werden ältere Elemente aufgeführt, die bereits ausgeliefert wurden.

### <a name="asset-packaging"></a>Verpacken von Objekten

- Automatisches CDN-Hosting für Code Das JavaScript-Bundle wird im App-Paket verpackt, das automatisch in einer Bibliothek bereitgestellt wird, die auf dem Mandanten-Office 365-CDN gehostet wird.

### <a name="alm-rest-apis"></a>ALM-REST-APIs

- ALM-REST-APIs. Bereitstellen, Aktivieren, Löschen und Aktualisieren von Apps und Add-Ins.
- ALM-REST-APIs zielen darauf ab, *alles* aus dem App-Katalog zu unterstützen, einschließlich Add-Ins.
- CSOM- und PowerShell-Cmdlets als Initiative der Open-Source-Community veröffentlicht.

### <a name="javascript-embedding-support-jslink-user-custom-actions"></a>Eingebettete JavaScript-Unterstützung (JSLink, benutzerdefinierte Benutzeraktionen) 

- Dieselbe Toolkette und dasselbe Bereitstellungsmodell wie bei clientseitigen Webparts
- Ableitung von einer stark typisierten Basisklasse wann immer möglich, anstelle der direkten Bearbeitung des Seiten-DOM
- Moderne Erweiterungsverwendung mit modernen Benutzerumgebungen ähnlich wie benutzerdefinierte Aktionen und JS-Link in der klassischen Umgebung
- Arbeiten mit NoScript über Mandanten-App-Katalog

### <a name="on-premises-support---sharepoint-2016-feature-pack-2"></a>Lokale Unterstützung – SharePoint 2016 Feature Pack 2

- Bereitstellung als Teil des Feature Pack 2 für SharePoint 2016
- Ähnliche Funktionen wie in SharePoint Online
- Ziel ist die Bereitstellung einer gemeinsamen Entwicklungsplattform, lokal und in der Cloud
- Nutzung der modernen Toolkette und von Open Soure für lokale Umgebungen
- Abzielen auf SharePoint 2016-Version während des Kalenderjahrs 2017


## <a name="see-also"></a>Siehe auch

- [dev.office.com-Blog](https://dev.office.com/blogs)
- [OfficeDev-Twitterkonto](https://twitter.com/officedev)
- [Übersicht über das SharePoint-Framework](sharepoint-framework-overview.md)
