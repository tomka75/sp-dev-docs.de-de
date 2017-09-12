# <a name="changes-between-dev-preview-and-release-candidate-for-sharepoint-framework-extensions-preview"></a>Unterschiede zwischen der Developer Preview und Release Candidate für SharePoint Framework-Erweiterungen (Preview)

Wenn Sie SharePoint Framework-Erweiterungen mit der Developer Preview-Version (veröffentlicht im Juni 2017) erstellt haben, müssen Sie einige Änderungen vornehmen, damit diese mit der Release Candidate-Version funktionieren. Nachfolgend finden Sie eine kurze Liste der Änderungen, die in der aktuellen Version eingeführt wurden.

Release Candidate ist in den Mandanten der First Release in Office 365 aktiviert, wird jedoch in der Produktion noch nicht unterstützt.

## <a name="general-solution-package-changes"></a>Allgemeine Änderungen an Lösungspaketen

- Alle SharePoint Framework-Pakete sind jetzt auf Version 1.2 standardisiert. Alle zukünftigen Updates werden auch eine Versionsstandardisierung über alle Pakete hinweg aufweisen, um Verwirrungen im Zusammenhang mit verwendeten Versionen zu vermeiden.
- Aktualisierung zur Verwendung von TypeScript 2.4 und React 15-Eingaben
- Update auf Fabric React 4.32.0.

### <a name="application-customizer-changes"></a>Änderungen am Application Customizer

- Platzhalterlogik wurde geringfügig geändert und umbenannt.
- Typische Platzhalter werden jetzt als `'top'` und `'bottom'` bezeichnet.
- Die `onRender`-Methode ist veraltet – rufen Sie „render“ ggf. über „onInit“ auf, und fügen Sie auch eine Ereignisbehandlung für die möglichen Ereignisse hinzu, wenn Platzhalter erneut gerendert werden sollen. Weitere Informationen finden Sie im [Lernprogramm zu aktualisierten Platzhaltern](./get-started/using-page-placeholder-with-extensions.md).
- Die Schemadefinitions-URL wurde in der Manifestdatei so aktualisiert, dass sie auf die JSON-Schemadatei von dev.office.com zeigt.

### <a name="field-customizer-changes"></a>Änderungen am Field Customizer

- Es wurden Änderungen an den APIs zum Zugreifen auf die tatsächlichen Feldwerte vorgenommen. Sie sollten `event.fieldValue` verwenden. Andere Optionen sind veraltet.
- Die API für den Zugriff auf das Benutzeroberflächenelement zum Rendern der Field Customizer-Ausgabe wurde von `event.cellDiv` in `event.domElement` geändert. 
- Die Schemadefinitions-URL wurde in der Manifestdatei so aktualisiert, dass sie auf die JSON-Schemadatei von dev.office.com zeigt.

### <a name="listview-command-set-changes"></a>Änderungen am ListView-Befehlssatz

- Die `onRefreshCommand`-Methode ist veraltet und wurde durch `onListViewUpdated` ersetzt.
- Manifest-JSON-Änderungen an der Befehlsstruktur. Jetzt werden `items`-Sammlungen und Änderungen in der Titelbehandlung der Befehle in der JSON-Definition verwendet.
- Die Schemadefinitions-URL wurde in der Manifestdatei so aktualisiert, dass sie auf die JSON-Schemadatei von dev.office.com zeigt.
