# <a name="sharepoint-framework-roadmap"></a>SharePoint Framework-Roadmap

Die Erstveröffentlichung von SharePoint Framework enthält Unterstützung für clientseitige Webparts. Dies ist jedoch nur der Beginn der Bereitstellung zusätzlicher moderner Anpassungsfunktionen für SharePoint. In diesem Artikel sind die verschiedenen Bereiche aufgeführt, die wir für die künftigen Versionen von SharePoint Framework bereit halten.

> Hinweis: Dies ist eine Liste von Bereichen, die von den SharePoint-Entwicklern abgearbeitet und untersucht werden. Das bedeutet **NICHT**, dass all diese Bereiche auch wirklich bereitgestellt werden, wir bemühen uns jedoch, Elemente und Themen aus dieser Liste in den künftigen Versionen von SharePoint Framework schrittweise zu veröffentlichen.  

## <a name="on-premises-support"></a>Lokaler Support

- Versand als Teil des Feature Packs 
- Ähnliche Funktionen wie in SharePoint Online
- Ziel ist die Bereitstellung einer gemeinsamen Entwicklungsplattform, lokal und in der Cloud
- Nutzung der modernen Toolkette und von Open Soure für „Legacy“-Umgebungen
- Abzielen auf SharePoint 2016-Version während des Kalenderjahrs 2017

## <a name="client-side-web-parts-and-add-ins"></a>Clientseitige Webparts und Add-Ins

- Einfacher Zugriff auf die Graph-API zum Zugreifen auf benutzerspezifische Informationen
- Unterstützung für komplexere Szenarios und Interaktionen mit Webparts
    - Kommunikation von Webpart zu Webpart
    - JS Framework-Isolierung
    - „Citizen Developer“-Modell für einfache Entwicklung

- Add-Ins für die moderne Welt: Ansprechendere Wiedergabe mit der neuen UX. 
    - Azure AD-Registrierung
    - Systemeigene dynamische Unterstützung 
    - Erstellen von Add-Ins mit SharePoint Framework

## <a name="javascript-embedding-support-jslink-user-custom-actions"></a>Eingebettete JavaScript-Unterstützung (JSLink, benutzerdefinierte Benutzeraktionen)

- Dieselbe Toolkette und dasselbe Bereitstellungsmodell wie bei clientseitigen Webparts
- Leiten Sie von einer stark typisierten Basisklasse, wann immer möglich, ab, anstatt das Seiten-DOM direkt zu bearbeiten.
- Ersetzung von benutzerdefinierten Aktionen und JSLinks durch SharePoint Framework-basierte Erweiterungen
- Arbeiten mit NoScript über Mandanten-App-Katalog
- Arbeiten im Websitesammlungs-App-Katalog
- PnP-gesteuerte beste Vorgehensweisen und Tools für die Migration


## <a name="application-lifecyle-management"></a>Application Lifecycle Management (ALM)


- Optimierte Genehmigungsoberfläche: Sie müssen nicht mehr wissen, wer Ihr Mandantenadministrator ist
    - Besitzer initiiert den Genehmigungsprozess
    - Mandantenadministrator wird automatisch benachrichtigt 
    - Einstellungen zum Steuern der Standardoberfläche um den Genehmigungsprozess herum

- ALM-REST-APIs - Bereitstellen, Aktivieren, Löschen und Aktualisieren von Apps und Add-Ins
- ALM-REST-APIs zielen darauf ab, *alles* aus dem App-Katalog zu unterstützen, einschließlich Add-Ins
- Automatisches CDN-Hosting für Code
    - Das JavaScript-Bundle wird im App-Paket verpackt, das dann automatisch in einer Bibliothek bereitgestellt wird, die auf dem Mandanten-Office 365-CDN gehostet wird.


## <a name="developer-experience"></a>Entwickleroberfläche
- SharePoint Framework Workbench 2.0: Entwicklungsgeschichte hinter Webparts mit Unterstützung neuer Komponententypen zusätzlich zu clientseitigen Webparts
- Toolkettenkomponenten
- Zusätzliche Yeoman-Vorlagen

## <a name="full-page-apps"></a>Ganzseitige Apps
- Erstellen von SharePoint Framework-Apps, die im Modus „Ganze Seite“ und nicht als clientseitiges Webpart gerendert werden
- Listenebene: Benutzerdefiniertes Ansichtselement, Element bearbeiten, Element löschen, Element hinzufügen
- Seitenebene: Zuweisen einer App zu einer Seite für eine benutzerdefinierte ganzseitige Oberfläche
- Mobil

## <a name="additional-resources"></a>Zusätzliche Ressourcen
Verwenden Sie die folgenden Ressourcen, um über die neuen Versionen und Funktionen auf dem Laufenden zu bleiben, die für SharePoint Framework veröffentlicht werden.

* [dev.office.com-Blog](https://dev.office.com/blogs)
* [OfficeDev-Twitterkonto](https://twitter.com/officedev)
