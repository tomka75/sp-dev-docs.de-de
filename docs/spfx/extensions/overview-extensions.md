# <a name="overview-of-sharepoint-framework-extensions-preview"></a>Übersicht über SharePoint Framework-Erweiterungen (Preview)

SharePoint Framework-Erweiterungen sind Erweiterungen der SharePoint-Benutzeroberfläche. Mit ihnen können Sie mehr Aspekte der SharePoint-Oberfläche individuell anpassen, beispielsweise Infobereiche, Symbolleisten und Listenansichten von Daten. SharePoint Framework-Erweiterungen können während der Preview-Phase in Office 365-Entwicklermandanten getestet werden. 

> **Hinweis:** Sie erhalten einen kostenlosen Office 365-Entwicklermandanten, wenn Sie sich für das [Office 365 Developer Program](http://dev.office.com/devprogram) registrieren.

Mithilfe von SharePoint Framework-Erweiterungen können Sie die SharePoint-Benutzeroberfläche auf modernen Seiten und in Dokumentbibliotheken erweitern. Dabei können Sie für die clientseitige Entwicklung die vertrauten SharePoint Framework-Tools und -Bibliotheken nutzen. Im Besonderen bietet SharePoint Framework drei neue Erweiterungstypen:

- **ApplicationCustomizers:** Erweiterungen dieses Typs fügen einer Seite Skripts hinzu. Außerdem greifen sie auf bekannte HTML-Element-Platzhalter zu und erweitern sie um benutzerdefinierte Renderings.
- **FieldCustomizers:** Über Erweiterungen dieses Typs können sie modifizierte Datenansichten für Felder in einer Liste bereitstellen.
- **CommandSets:** Erweiterungen dieses Typs erweitern die SharePoint-Befehlsoberfläche um neue Aktionen und stellen clientseitigen Code bereit, mit dessen Hilfe Sie bestimmte Verhaltensweisen implementieren können.

Zusätzlich zu einfachen JavaScript-Projekten können Sie auch gängige Skripterstellungsframeworks wie AngularJS und React zur Erstellung Ihrer Erweiterungen nutzen. So können Sie beispielsweise React mit Komponenten aus Office UI Fabric React kombinieren und Oberflächen erstellen, die dieselben Komponenten verwenden wie Office 365.

## <a name="get-started"></a>Erste Schritte
Falls Sie SharePoint Framework noch nicht installiert haben, müssen Sie die Schritt-für-Schritt-Anleitung im Artikel zum Thema [Einrichten Ihrer Entwicklungsumgebung](../set-up-your-development-environment) befolgen.

Führen Sie nach der Installation von SharePoint Framework den folgenden Befehl aus, um Ihre Yeoman-Vorlagen auf die neueste Version zu aktualisieren:

```
npm install -g @microsoft/generator-sharepoint
```

Anschließend erstellen Sie Ihre erste SharePoint Framework-Erweiterung mithilfe der Anleitung im Artikel [Build your first SharePoint Framework Extension (Hello World part 1)](./get-started/build-a-hello-world-extension).

## <a name="stay-up-to-date"></a>Immer auf dem neuen Stand
Die neuesten Informationen zu SharePoint Framework-Verbesserungen, einschließlich Erweiterungsaktualisierungen, finden Sie hier:

* [@SharePoint](https://twitter.com/sharepoint) und [@OfficeDev](https://twitter.com/officedev) auf Twitter
* [Office-Entwicklerblog](http://dev.office.com/blogs)

## <a name="provide-feedback"></a>Übermitteln von Feedback 
Wir würden uns über Ihr Feedback zur Preview-Version der SharePoint Framework-Erweiterungen freuen. Sie können die folgenden Ressourcen nutzen, um dem SharePoint-Entwicklerteam Feedback zu übermitteln:

- [Problemliste im Repository „sp-dev-docs“](https://github.com/SharePoint/sp-dev-docs/issues): Fragen, Probleme und Kommentare
* [SharePoint StackExchange](http://sharepoint.stackexchange.com/): Verwenden Sie die Tags [#spfx](http://sharepoint.stackexchange.com/tags/spfx/), [#spfx-extensions](http://sharepoint.stackexchange.com/tags/spfx-extensions/) und [#spfx-tooling](http://sharepoint.stackexchange.com/tags/spfx-tooling/).
* [SharePoint Developer](https://techcommunity.microsoft.com/t5/SharePoint-Developer/bd-p/SharePointDev): Gruppe in der Microsoft Tech Community
* [SharePoint Developer UserVoice](https://sharepoint.uservoice.com/forums/329220-sharepoint-dev-platform): Plattform zur Anforderung neuer Funktionen und Features


## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [Übersicht über das SharePoint Framework](../sharepoint-framework-overview)
- [Entwicklungstools und -bibliotheken für das SharePoint Framework](../tools-and-libraries)
