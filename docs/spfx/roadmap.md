---
title: SharePoint Framework-Roadmap
ms.date: 12/15/2017
ms.prod: sharepoint
ms.openlocfilehash: fd8577a51c3a16ffec94cca3958c8853a8ea9dcb
ms.sourcegitcommit: 202dd467c8e5b62c6469808226ad334061f70aa2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/15/2017
---
# <a name="sharepoint-framework-roadmap"></a>SharePoint-Framework-Roadmap

Die Erstveröffentlichung von SharePoint-Framework enthielt nur Unterstützung für clientseitige Webparts. Dies war jedoch nur der Beginn der Bereitstellung zusätzlicher moderner Anpassungsfunktionen für SharePoint. Im folgenden werden die wichtigsten Funktionen aufgeführt, die nach der Markteinführung veröffentlicht wurden.

- [Unterstützung für mandantenweite Bereitstellung](./tenant-scoped-deployment.md)
- [Lokale Unterstützung für SharePoint 2016 (Feature Pack 2)](./sharepoint-2016-support.md)
- [SharePoint-Framework-Erweiterungen](./extensions/overview-extensions.md)
- [Mandanteneigenschaften](./tenant-properties.md)
- [ALM-APIs für SPFx-Lösungen und -Add-Ins](../apis/alm-api-for-spfx-add-ins.md)
- [Unterstützung für Office UI Fabric Core](https://dev.office.com/blogs/improved-support-for-office-ui-fabric-core)
- [Verpacken von Objekten und Websitesammlungs-App-Katalog](../general-development/site-collection-app-catalog.md)


> [!NOTE]
> Dies ist eine Liste von Bereichen, die von den SharePoint-Entwicklern abgearbeitet und untersucht werden. Das bedeutet **NICHT**, dass all diese Bereiche auch wirklich bereitgestellt werden, wir bemühen uns jedoch, Elemente und Themen aus dieser Liste in den künftigen Versionen von SharePoint-Framework schrittweise zu veröffentlichen.

## <a name="general-improvements"></a>Allgemeine Verbesserungen

- Einfacher Zugriff auf die Graph-API zum Zugreifen auf benutzerspezifische Informationen (GraphHttpClient in der Vorschau)
- Webhooks auf Website-Ebene

## <a name="client-side-web-parts-and-add-ins"></a>Clientseitige Webparts und Add-Ins

- Unterstützung für komplexere Szenarios und Interaktionen mit Webparts
    - Kommunikation von Webpart zu Webpart
    - JS Framework-Isolierung
    - „Citizen Developer“-Modell für einfache Entwicklung

- Add-Ins für die moderne Welt: Ansprechendere Wiedergabe mit der neuen UX. 
    - Azure AD-Registrierung
    - Systemeigene dynamische Unterstützung
    - Erstellen von Add-Ins mit SharePoint-Framework


## <a name="application-lifecycle-management"></a>Application Lifecycle Management

- Optimierte Genehmigungsoberfläche: Sie müssen nicht mehr wissen, wer Ihr Mandantenadministrator ist
    - Besitzer initiiert den Genehmigungsprozess
    - Mandantenadministrator wird automatisch benachrichtigt 
    - Einstellungen zum Steuern der Standardoberfläche um den Genehmigungsprozess herum


## <a name="developer-experience"></a>Entwickleroberfläche
- SharePoint-Framework-Workbench 2.0: Entwicklungsgeschichte für SharePoint-Framework-Erweiterungen
- Toolkettenkomponenten
- Zusätzliche Yeoman-Vorlagen

## <a name="already-shipped-capabilities"></a>Bereits ausgeliefert Funktionen

In den folgenden Kapiteln werden ältere Elemente auf der Roadmap-Seite erläutert, die bereits ausgeliefert wurden.

### <a name="asset-packaging"></a>Verpacken von Objekten

- Automatisches CDN-Hosting für Code – Das JavaScript-Bundle wird im App-Paket verpackt, das dann automatisch in einer Bibliothek bereitgestellt wird, die auf dem Mandanten-Office 365-CDN gehostet wird.

### <a name="alm-rest-apis"></a>ALM-REST-APIs

- ALM-REST-APIs - Bereitstellen, Aktivieren, Löschen und Aktualisieren von Apps und Add-Ins
- ALM-REST-APIs zielen darauf ab, *alles* aus dem App-Katalog zu unterstützen, einschließlich Add-Ins
- CSOM und PowerShell-Cmdlets als Initiative der Open-Source-Community

### <a name="javascript-embedding-support-jslink-user-custom-actions"></a>Eingebettete JavaScript-Unterstützung (JSLink, benutzerdefinierte Benutzeraktionen) 

- Dieselbe Toolkette und dasselbe Bereitstellungsmodell wie bei clientseitigen Webparts
- Leiten Sie von einer stark typisierten Basisklasse, wann immer möglich, ab, anstatt das Seiten-DOM direkt zu bearbeiten.
- Moderne Erweiterungsverwendung mit modernen Benutzerumgebung ähnlich wie Benutzerdefinierte Aktionen und JS-Link in der klassischen Umgebung
- Arbeiten mit NoScript über Mandanten-App-Katalog

### <a name="on-premises-support---sharepoint-2016-feature-pack-2"></a>Lokale Unterstützung – SharePoint 2016 Feature Pack 2

- Bereitstellung als Teil des Feature Pack 2 für SharePoint 2016
- Ähnliche Funktionen wie in SharePoint Online
- Ziel ist die Bereitstellung einer gemeinsamen Entwicklungsplattform, lokal und in der Cloud
- Nutzung der modernen Toolkette und von Open Soure für lokale Umgebungen
- Abzielen auf SharePoint 2016-Version während des Kalenderjahrs 2017


## <a name="see-also"></a>Siehe auch
Verwenden Sie die folgenden Ressourcen, um über die neuen Versionen und Funktionen auf dem Laufenden zu bleiben, die für SharePoint Framework veröffentlicht werden.

* [dev.office.com-Blog](https://dev.office.com/blogs)
* [OfficeDev-Twitterkonto](https://twitter.com/officedev)
