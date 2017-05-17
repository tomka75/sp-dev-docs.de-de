# <a name="known-issues-and-frequently-asked-questions"></a>Bekannte Probleme und häufig gestellte Fragen

Auf dieser Seite finden Sie eine Liste bekannter Probleme mit SharePoint Framework sowie Antworten auf häufig gestellte Fragen. 

## <a name="known-issues"></a>Bekannte Probleme

**Problem mit dem Entwicklerzertifikat unter Chrome (ab v58)**

- *Datum – 28. April*
- *Aktualisiert – 2. Mai*

Wenn Sie Chrome als Entwicklungsbrowser verwenden, treten möglicherweise Probleme mit dem Entwicklerzertifikat auf, unabhängig davon, ob Sie den Befehl `gulp trust-dev-cert` ausführen. Chrome hat sein Modell für die Überprüfung von Zertifikaten ab Version 58 geändert. Beim Zugriff auf die lokale Workbench wird Ihnen daher möglicherweise die Warnmeldung „Ihre Verbindung ist nicht privat“ angezeigt.

Sie sollten Ihre Yeoman-Vorlagenpakete aktualisieren. Wir haben die Zertifizierungserstellungslogik im Paket *@microsoft/gulp-core-build-serve* aktualisiert. In vorhandenen Lösungen können Sie einfach diesen Ordner löschen und `npm install` ausführen, um das aktualisierte Paket abzurufen. Darüber hinaus müssen Sie die Befehle `untrust-dev-cert` und `trust-dev-cert` auf Ihrem Computer ausführen, um das Problem der Zertifizierungserstellungslogik zu behoben. 

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

**Ab wann werden benutzerdefinierte Aktionen und JSLink im SharePoint Framework verfügbar sein?**

- *Datum – 28. April*

Aktuell können wir noch kein Datum für die öffentliche Verfügbarkeit nennen. Wir arbeiten daran, moderne Anpassungsfunktionen für benutzerdefinierte Benutzeraktionen und JSLink-Funktionen zu implementieren, die sowohl in der klassischen als auch in der modernen Oberfläche unterstützt werden. 

**Wird SharePoint Framework auch in lokalen Bereitstellungen verfügbar sein?**

- *Datum – 28. April*

Wir arbeiten derzeit daran, SharePoint Framework noch im Laufe des Kalenderjahres 2017 für SharePoint 2016 zu veröffentlichen. Aktuell können wir keine weiteren Veröffentlichungsdaten nennen. 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
Verwenden Sie die folgenden Ressourcen, um den SharePoint-Entwicklern Feedback, Kommentare und Fragen zukommen zu lassen: 

* [Problemliste unter „sp-dev-docs“ in GitHub](https://github.com/SharePoint/sp-dev-docs/issues)
* [SharePoint Developer-Bereich in der Microsoft Tech Community](https://aka.ms/sppnp-community)
