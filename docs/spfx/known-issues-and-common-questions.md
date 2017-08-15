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

- *Datum - 6. Juni*

SharePoint Extensions mit weiteren anpassbaren Funktionen für SharePoint Online sind nun für die Entwicklervorschau verfügbar. Derzeit ist noch kein Datum für die allgemeine Verfügbarkeit (GA) festgelegt. Mithilfe der folgenden Lernprogramme können Sie sich mit dem Erstellen von Erweiterungen vertraut machen.

* [Erste Schritte mit SharePoint Framework Extensions](http://aka.ms/spfx-extensions)

**Wird SharePoint Framework auch in lokalen Bereitstellungen verfügbar sein?**

- *Datum - 6. Juni*

Die clientseitigen Webparts von SharePoint-Framework werden im Rahmen des Feature Pack 2 (FP2) mit SharePoint 2016 veröffentlicht. 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
Verwenden Sie die folgenden Ressourcen, um den SharePoint-Entwicklern Feedback, Kommentare und Fragen zukommen zu lassen: 

* [Problemliste unter „sp-dev-docs“ in GitHub](https://github.com/SharePoint/sp-dev-docs/issues)
* [SharePoint Developer-Bereich in der Microsoft Tech Community](https://aka.ms/sppnp-community)
