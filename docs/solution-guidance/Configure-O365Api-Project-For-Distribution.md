---
title: "Konfigurieren von Projekten für Office 365-API für die Verteilung"
ms.date: 11/03/2017
ms.openlocfilehash: 4dde15a519cd313b26b07e11b2bde7d8bb349f45
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="configure-office-365-api-projects-for-distribution"></a>Konfigurieren von Projekten für Office 365-API für die Verteilung

### <a name="summary"></a>Summary ###
Auf dieser Seite wird erläutert, dass einige Schritte Entwickler berücksichtigen sollten auf ihre Projekte, die die Office 365-APIs vor deren Verteilung mit anderen Entwicklern, ihren Kunden oder Quellcode-Verwaltungssysteme wie Team Foundation Server, Git oder Visual Studio nutzen Online.

Insbesondere auf dieser Seite sehen sich zwei Schritte:

- [Fixup Azure AD-Diagramm Client NuGet-Paket (engl.)](#fixup-azure-ad-graph-client-nuget-package-reference)
- [Bereinigen der `web.config` für app-spezifischen Details](#cleaning-the-webconfig-for-app-specific-details)

# <a name="fixup-azure-ad-graph-client-nuget-package-reference"></a>Fixup Azure AD-Diagramm Client NuGet-Paket (engl.)

Alle Projekte, die die Office 365-API-SDKs über einen verbundenen Dienst hinzufügen nutzen enthalten ein NuGet-Paket, das Office 365 und Azure AD-Verweise auf das Projekt in Visual Studio erstellten hinzugefügt. 

Durch die **Office 365-API-Tools** in Visual Studio dem Projekt hinzugefügte NuGet-Paket ist nicht in der Registrierung des NuGet-Paket vorhanden und daher Versuche zum Erstellen einer NuGet-Paket-Wiederherstellung schlägt fehl, da ein passendes Paket gefunden werden kann.

## <a name="understanding-the-problem"></a>Beschreibung des Problems ##

Die **Office 365-API-Tools für Visual Studio 2013**, Version 1.3.41104.1, hinzugefügt Projekte im Rahmen des Assistenten zum verbundenen Dienst Hinzufügen mehrerer NuGet-Pakete. Ein Paket insbesondere stellt eine Herausforderung: **Microsoft Azure Active Directory Graph-Clientbibliothek**.

Die Arbeitsweise von Visual Studio ist, dass oder Addins, enthalten eine lokale Kopie der NuGet-Paket in der Regel damit Entwickler nicht immer mit dem Internet NuGet-Pakete herunterladen verbunden sein. Das Paket, das die Tools enthalten hat eine ID von **Microsoft.Azure.ActiveDirectory.GraphClient** & einer Version von **1.0.22**.

Wenn Projekte in Datenquellen-Steuerelement übernommen werden, sind in der Regel die Pakete nicht eingeschlossen als Teil des Commit, da sie viel extra Speicher Speicherplatz Bedarfs und unnötig hinzufügen können erhöhen Sie die Größe eines Pakets, wenn es gemeinsam mit anderen Entwicklern. Aus diesem Grund einer der ersten Aufgaben Entwickler Schritt nach Abrufen einer Kopie des Projekts aus der quellcodeverwaltung [Wiederherstellen NuGet-Paket](http://docs.nuget.org/docs/reference/package-restore)ausgeführt wird.

Die Herausforderung besteht darin, dass ein Paket mit dem gleichen ID & Version nicht in der Registrierung des NuGet-Paket vorhanden ist; Es ist kein Paket mit einer ID mit **Microsoft.Azure.ActiveDirectory.GraphClient** & einer Version von **1.0.22**. Das Paket ist in der Registrierung NuGet-Paket **[Microsoft.Azure.ActiveDirectory.GraphClient](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)**, aber unter verschiedenen Versionen vorhanden.

## <a name="fixing-the-azure-ad-graph-client-nuget-package-reference"></a>Beheben von NuGet-Paket-Referenz zu Azure AD-Grafik-Clients ##

Bis die Office 365-API-Tools für Visual Studio 2013 aktualisiert werden, um dieses Problem zu beheben, empfiehlt es sich um das Projekt vor dem Ausführen eines Commits zu Ihrem Quellcodeverwaltungssystem, unabhängig davon ändern, wenn mithilfe von Team Foundation Server, Visual Studio Online, Git oder andere Lösung.

Suchen Sie nach dem Erstellen des Projekts innerhalb des Projekts `packages.config` -Datei, und suchen Sie nach einem Paket mit einer ID mit **Microsoft.Azure.ActiveDirectory.GraphClient** & Version von **1.0.22**. Die sicherste Methode zum Aktualisieren des Projekts ist zum Deinstallieren und Neuinstallieren von des Pakets.

Öffnen Sie die **Paket-Manager-Konsole** in Visual Studio, und geben Sie Folgendes ein, um das Paket zu deinstallieren:

  ````powershell
  PM> Uninstall-Package -Id Microsoft.Azure.ActiveDirectory.GraphClient
  ````

  > Wenn die Deinstallation einen Fehler zum Suchen nach nicht das Paket auslöst, entfernen Sie einfach den Paket-Verweis aus der `packages.config` Datei manuell & Ihre Änderungen zu speichern.

Installieren Sie nun die öffentliche Version der gleichen NuGet-Paket aus der öffentlichen Registrierung:

  ````powershell
  PM> Install-Package -Id Microsoft.Azure.ActiveDirectory.GraphClient -Version 2.0.2
  ````

  > Das vorstehende Beispiel verweist auf eine bestimmte Version des Azure AD Graph-Clients, die die Office 365-APIs entwickelt bekannt ist. Zukünftige Versionen so auslassen funktionieren möglicherweise die `-Version` -Argument ist optional.

[zurück zum Seitenanfang](#configure-office-365-api-projects-for-distribution)

# <a name="cleaning-the-webconfig-for-app-specific-details"></a>Bereinigen der `web.config` für App-spezifischen Details

Die **Office 365-API-Tools** für Visual Studio hinzufügen, die Möglichkeit zum Erstellen eines neuen Azure AD-Anwendung mit den erforderlichen Berechtigungen für die Office 365-APIs, die mit dem **Dienst verbunden** -Assistenten in Visual Studio. Wenn der Assistent abgeschlossen ist, mehrere Einträge und Anpassungen werden dem Projekt vorgenommen `web.config` Datei.

Diese Änderungen gehören die folgenden Add-in-Einstellungen:

- **Ida: ClientID**: die eindeutige ID der Anwendung in Ihrem Azure AD-Mandanten erstellt.
- **IDA: Kennwort**: die Azure AD-Anwendung-Schlüssel, der mit dem Dienst verbunden-Assistenten generiert wurde.
- **Ida: AuthorizationUri**: den Endpunkt zur Authentifizierung mit Azure AD verwendet.

Die **Ida: ClientID** und **Ida: Kennwort** sind für die Azure AD-app eindeutig. Einige Entwicklungsteams möglicherweise wählen Sie für jeden Entwickler auf Code anhand ihrer eigenen app, ähnlich wie Entwickler eigene lokale Entwicklungsdatenbank verwenden. Daher können Sie sich vorstellen der die **Ida: ClientID** und **Ida: Kennwort** Datenbank-Verbindungszeichenfolgen ähnelt. 

Das nächste Mal verwendet ein Entwickler die Connected-Service-Assistent zum Erstellen eines neuen Azure AD-Anwendung des Projekts, der Assistent erkennt die **Ida: CliendID** und Versuch der Verbindung zu einer Anwendung in Azure AD-Mandanten des aktuellen Benutzers. Wenn eine Übereinstimmung gefunden wird, wird der Connected-Service-Assistenten ein Fehler ausgelöst.

Aus diesem Grund vor dem Ausführen eines Commits für das Projekt aus, bevor Sie mit anderen Entwicklern freigeben oder Datenquellen-Steuerelement, es wird empfohlen, die Werte aus der **Ida: ClientID**entfernen & **Ida: Kennwort** Add-in-Einstellungen in der `web.config`.

[zurück zum Seitenanfang](#configure-office-365-api-projects-for-distribution)

----------

### <a name="related-links"></a>Verwandte links ###
- [NuGet: App für SharePoint-Web-Toolkit](http://www.nuget.org/packages/AppForSharePointWebToolkit)
- [NuGet: Paket wiederherstellen](http://docs.nuget.org/docs/reference/package-restore)
- [MSDN: NuGet-Pakete für Office 365-Client-API-Bibliothek](http://msdn.microsoft.com/office/office365/HowTo/adding-service-to-your-Visual-Studio-project#O365NuGets)

### <a name="applies-to"></a>Gilt für ###
-  Office 365 mit mehreren Mandanten (MT)
-  Office 365 dedizierte (D)

### <a name="author"></a>Autor
Andrew Connell - [@andrewconnell](https://twitter.com/andrewconnell)

### <a name="version-history"></a>Versionsverlauf ###
Version  | Datum | Kommentare
---------| -----| --------
0,1  | 31 Dezember 2014 | Erster Entwurf


