# <a name="changes-introduced-in-the-sharepoint-framework-extensions-preview-release-candidate-release"></a>Änderungen, die in der Release Candidate-Version von SharePoint-Framework-Erweiterungen (Vorschau) eingeführt wurden

Wenn Sie die Developer Preview-Version der SharePoint-Framework-Erweiterungen (im Juni 2017 veröffentlicht) verwendet haben, müssen Sie einige Änderungen vornehmen, um sicherzustellen, dass Ihre Erweiterungen mit der Release Candidate (RC)-Version verwendet werden können. Dieser Artikel enthält eine kurze Liste mit den Änderungen, die in der RC-Version von SharePoint-Framework-Erweiterungen eingeführt wurden.

>**Hinweis:** Die RC-Version ist in den First Release-Mandanten in Office 365 aktiviert, wird jedoch für die Produktionsverwendung noch nicht unterstützt.

## <a name="general-solution-package-changes"></a>Allgemeine Änderungen an Lösungspaketen

- Alle SharePoint-Framework-Pakete sind jetzt auf Version 1.2 standardisiert. Alle zukünftigen Updates werden auch Standardversionen für alle Pakete haben.
- Upgrade zur Verwendung von TypeScript 2.4 und React 15-Eingaben
- Aktualisiert auf Fabric React 4.32.0.

## <a name="application-customizer-changes"></a>Änderungen am Application Customizer

- Platzhalterlogik wurde geringfügig geändert, und Platzhalter wurden umbenannt. Typische Platzhalter heißen jetzt `'top'` und `'bottom'`.
- Die **`onRender`**-Methode ist veraltet. Rufen Sie stattdessen **`render`** über die **`onInit`**-Methode auf, und fügen Sie Ereignisbehandlung für die möglichen Ereignisse hinzu, wenn Platzhalter neu gerendert werden sollen. Weitere Informationen finden Sie unter [Verwenden von Seitenplatzhaltern](./get-started/using-page-placeholder-with-extensions.md).
- Die Schemadefinitions-URL wurde in der Manifestdatei so aktualisiert, dass sie auf die Onlinedokumentation für das JSON-Schema zeigt.

## <a name="field-customizer-changes"></a>Änderungen am Field Customizer

- Die APIs, die auf Feldwerte zugreifen, wurden geändert. Verwenden Sie **`event.fieldValue`**. Andere Optionen sind veraltet.
- Die API für den Zugriff auf Benutzeroberflächenelemente zum Rendern der Field Customizer-Ausgabe wurde von **`event.cellDiv`** in **`event.domElement`** geändert. 
- Die Schemadefinitions-URL wurde in der Manifestdatei so aktualisiert, dass sie auf die Onlinedokumentation für das JSON-Schema zeigt.

## <a name="listview-command-set-changes"></a>Änderungen am ListView-Befehlssatz

- Die **`onRefreshCommand`**-Methode ist veraltet und wurde durch **`onListViewUpdated`** ersetzt.
- Die Struktur der Befehle in der JSON-Manifestdatei wurde verändert. Befehle verwenden jetzt die **`items`**-Sammlung, und die Handhabung von Befehlstiteln wurde in der JSON-Definition aktualisiert.
- Die Schemadefinitions-URL wurde in der Manifestdatei so aktualisiert, dass sie auf die Onlinedokumentation für das JSON-Schema zeigt.
