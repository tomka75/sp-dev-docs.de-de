# <a name="overview-of-sharepoint-framework-extensions-preview"></a>Übersicht über SharePoint Framework Extensions (Preview)

Mit SharePoint Framework Extensions können Entwickler die Benutzeroberfläche von SharePoint erweitern und umfassendere Bereiche der SharePoint-Umgebung noch besser an die Bedürfnisse der Endbenutzer anpassen, einschließlich Benachrichtigungsbereiche, die SharePoint-Symbolleisten und die Ansicht von Listendaten. SharePoint-Framework-Erweiterungen sind zu Testzwecken über Office 365-Entwicklermandanten während der Vorschau sowie später für alle Mandanten verfügbar, wenn die allgemeine Verfügbarkeit bekannt gegeben wurde. 

> Sie können einen kostenlosen Office 365-Entwicklermandanten erhalten, indem Sie das [Developer-Programm für Office 365](http://dev.office.com/devprogram) abonnieren.

SharePoint Framework Extensions fügen neue Funktionen hinzu, um die Benutzerumgebung von SharePoint innerhalb von modernen Seiten und Dokumentbibliotheken zu erweitern, wobei gleichzeitig die vertrauten Tools und Bibliotheken für die clientseitige Entwicklung von SharePoint Framework genutzt werden können. Das SharePoint-Framework umfasst insbesondere drei neue Erweiterungstypen:

- **ApplicationCustomizers** (Anwendungsanpasser) ermöglichen Entwicklern, der Seite Skripte hinzuzufügen sowie auf bekannte HTML-Elementplatzhalter zuzugreifen und diese durch benutzerdefinierte Renderings zu erweitern.
- **FieldCustomizers** (Feldanpasser) können verwendet werden, um geänderte Ansichten von Daten für Felder in einer Liste bereitzustellen.
- **CommandSets** (Befehlssätze) ermöglichen Entwicklern, die Befehlsfläche von SharePoint zu erweitern, um neue Aktionen sowie clientseitigen Code hinzuzufügen, der zum implementieren von Verhalten verwendet werden kann.

Zusätzlich zu einfachen JavaScript-Projekten können Sie Erweiterungen parallel mit allgemeinen Scripting-Frameworks wie z. B. AngularJS und React erstellen. Sie können beispielsweise React zusammen mit Komponenten des Office-UI-Fabric-React nutzen, um schnell Umgebungen basierend auf den gleichen Komponenten erstellen, die in Office 365 verwendet werden.

## <a name="getting-started"></a>Erste Schritte
Wenn Sie das SharePoint-Framework noch nicht installiert haben, sehen Sie sich das folgende Lernprogramm an, um sich auf die Entwicklung im SharePoint-Framework vorzubereiten:

* [Einrichten der Entwicklungsumgebung](../set-up-your-development-environment)

Wenn Sie das SharePoint-Framework bereits installiert haben, führen Sie den folgenden Befehl zum Aktualisieren Ihrer Yeoman-Vorlagen auf die neueste Version aus:

```
npm install -g @microsoft/generator-sharepoint
```

Erste Schritte mit den Lernprogrammen für die Entwicklung mit SharePoint Framework Extensions:

* [Erstellen Ihrer ersten SharePoint-Framework-Erweiterung (Hello World, Teil 1)](./get-started/build-a-hello-world-extension)

## <a name="updates--feedback"></a>Updates & Feedback

Um keine Verbesserung des SharePoint-Framework, einschließlich der Veröffentlichung von Erweiterungen, zu verpassen, sehen Sie sich Folgendes an:

* [@SharePoint](https://twitter.com/sharepoint) und [@OfficeDev](https://twitter.com/officedev) auf Twitter
* [Office-Entwicklerblog](http://dev.office.com/blogs)

## <a name="provide-feedback-during-preview"></a>Ihr Feedback während der Vorschauphase
Die Preview-Version von SharePoint Framework Extensions wird zur Verfügung gestellt, um Feedback von Entwicklern bezüglich der geplanten Funktionen zu erhalten. Nutzen Sie die folgenden Ressourcen, um mit dem SharePoint Engineering zu diskutieren:

- [sp-dev-docs Repository-Problemliste](https://github.com/SharePoint/sp-dev-docs/issues): Fragen, Probleme und Kommentare
* [SharePoint StackExchange](http://sharepoint.stackexchange.com/) (verwenden Sie die Tags [#spfx](http://sharepoint.stackexchange.com/tags/spfx/), [#spfx-extensions](http://sharepoint.stackexchange.com/tags/spfx-extensions/) und [#spfx-tooling](http://sharepoint.stackexchange.com/tags/spfx-tooling/))
* [SharePoint Developer](https://techcommunity.microsoft.com/t5/SharePoint-Developer/bd-p/SharePointDev)-Gruppe der Microsoft Tech Community
* [SharePoint-Entwickler-Benutzerfeedback](https://sharepoint.uservoice.com/forums/329220-sharepoint-dev-platform) - Anforderung neuer Funktionen und Features


## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [Übersicht über das SharePoint Framework](../sharepoint-framework-overview)
- [Entwicklungstools und -bibliotheken für das SharePoint Framework](../tools-and-libraries)
