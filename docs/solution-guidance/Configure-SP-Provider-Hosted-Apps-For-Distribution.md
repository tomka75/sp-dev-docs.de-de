---
title: "Konfigurieren von SharePoint gehostet durch Drittanbieter-Add-ins für die Verteilung"
ms.date: 11/03/2017
ms.openlocfilehash: 82a1c046063dda3a612f96f70e5583d58ca9a505
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="configure-sharepoint-provider-hosted-add-ins-for-distribution"></a>Konfigurieren von SharePoint gehostet durch Drittanbieter-Add-ins für die Verteilung

### <a name="summary"></a>Summary ###

Auf dieser Seite erläutert die Probleme, die bei der Freigabe eines SharePoint-Anwendung mit anderen Entwicklern vom Anbieter gehostete oder beim Abrufen einer Kopie aus einem Quellcodeverwaltungssystem wie Team Foundation Server, Git oder Visual Studio Online auftreten können.

# <a name="configure-sharepoint-provider-hosted-add-ins-for-distribution"></a>Konfigurieren von SharePoint gehostet durch Drittanbieter-Add-ins für die Verteilung

Alle SharePoint gehostet durch Drittanbieter-add-ins mit Visual Studio 2013 erstellt enthalten ein NuGet-Paket, das SharePoint-spezifische Code hinzugefügt und verweist auf die Webanwendung, die als das RemoteWeb für die SharePoint-add-in fungiert. 

Durch die Office-Entwicklertools in Visual Studio das Webanwendungsprojekt hinzugefügt NuGet-Paket ist nicht in der Registrierung des NuGet-Paket vorhanden, und daher Versuche zum Erstellen einer NuGet-Paket-Wiederherstellung schlägt fehl, da ein passendes Paket gefunden werden kann.

## <a name="understanding-the-problem"></a>Beschreibung des Problems ##

Die im **Office Developer Tools für Visual Studio 2013**Version 12.0.31105, fügt ein NuGet-Paket für Webanwendungen als die RemoteWeb für SharePoint gehostet durch Drittanbieter-add-ins erstellt. Dieses Paket, die **App für SharePoint Web Toolkit**hinzugefügt Webprojekt Folgendes:

- Assemblys & Verweise auf die Assemblys SharePoint Client-Side Object Model (CSOM)
- Eine Codedatei `TokenHelper.cs` , die bei der Authentifizierung für add-ins unterstützt.
- Eine Codedatei `SharePointContext.cs` Ihnen dabei hilft, erstellen und Verwalten von einem SharePoint-Kontext innerhalb der Webanwendung.

Die Arbeitsweise von Visual Studio ist, dass oder Addins, enthalten eine lokale Kopie der NuGet-Paket in der Regel damit Entwickler nicht immer mit dem Internet NuGet-Pakete herunterladen verbunden sein. Das Paket, das die Tools enthalten hat eine ID von **AppForSharePoint16WebToolkit**.

Wenn Projekte in Datenquellen-Steuerelement übernommen werden, sind in der Regel die Pakete nicht eingeschlossen als Teil des Commit, da sie viel extra Speicher Speicherplatz Bedarfs und unnötig hinzufügen können erhöhen Sie die Größe eines Pakets, wenn es gemeinsam mit anderen Entwicklern. Aus diesem Grund einer der ersten Aufgaben Entwickler Schritt nach Abrufen einer Kopie des Projekts aus der quellcodeverwaltung [Wiederherstellen NuGet-Paket](http://docs.nuget.org/docs/reference/package-restore)ausgeführt wird.

Die Herausforderung besteht darin, dass ein Paket mit der gleichen ID nicht in der Registrierung des NuGet-Paket vorhanden ist; Es ist kein Paket mit der ID **AppForSharePoint16WebToolkit**. Stattdessen genauen gleiche Paket wurde hinzugefügt, um die Registrierung des NuGet-Paket als **AppForSharePointWebToolkit** ([http://www.nuget.org/packages/AppForSharePointWebToolkit](http://www.nuget.org/packages/AppForSharePointWebToolkit)) ** (*Beachten Sie die mangelnde die 16 im Feld-ID*).

## <a name="preparing-a-sharepoint-provider-hosted-add-in-project-for-source-control--distribution"></a>Vorbereiten eines SharePoint gehostet durch Drittanbieter-Add-in-Projekts zur Quellcodeverwaltung / Verteilung ##

Bis die Office Developer Tools für Visual Studio 2013 aktualisiert werden, um dieses Problem zu beheben, empfiehlt es sich um das Projekt vor dem Ausführen eines Commits zu Ihrem Quellcodeverwaltungssystem, unabhängig davon ändern, wenn mithilfe von Team Foundation Server, Visual Studio Online, Git oder andere Lösung.

Suchen Sie nach dem Erstellen des Projekts innerhalb des Projekts `packages.config` -Datei, und suchen Sie für ein Paket mit der ID **AppForSharePoint16WebToolkit**. Die sicherste Methode zum Aktualisieren des Projekts ist zum Deinstallieren und Neuinstallieren von des Pakets.

Öffnen Sie die **Paket-Manager-Konsole** in Visual Studio, und geben Sie Folgendes ein, um das Paket zu deinstallieren:

  ````powershell
  PM> Uninstall-Package -Id AppForSharePoint16WebToolkit
  ````

  > Wenn die Deinstallation einen Fehler zum Suchen nach nicht das Paket auslöst, entfernen Sie einfach den Paket-Verweis aus der `packages.config` Datei manuell & Ihre Änderungen zu speichern.

Installieren Sie nun die öffentliche Version der gleichen NuGet-Paket aus der öffentlichen Registrierung:

  ````powershell
  PM> Install-Package -Id AppForSharePointWebToolkit
  ````

----------

### <a name="related-links"></a>Verwandte links ###
- [NuGet: App für SharePoint-Web-Toolkit](http://www.nuget.org/packages/AppForSharePointWebToolkit)
- [NuGet: Paket wiederherstellen](http://docs.nuget.org/docs/reference/package-restore)

### <a name="applies-to"></a>Gilt für ###
-  Office 365 mit mehreren Mandanten (MT)
-  Office 365 dedizierte (D)
-  SharePoint 2013 lokal

### <a name="author"></a>Autor
Andrew Connell - [@andrewconnell](https://twitter.com/andrewconnell)

### <a name="version-history"></a>Versionsverlauf ###
Version  | Datum | Kommentare
---------| -----| --------
0,1  | 31 Dezember 2014 | Erster Entwurf
