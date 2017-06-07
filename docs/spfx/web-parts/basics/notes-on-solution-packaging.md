# <a name="notes-on-solution-packaging"></a>Hinweise zu Lösungspaketen

Die Gulp-Aufgabe **package-solution** sucht unter **/config/package-solution.json** nach unterschiedlichen Konfigurationsdetails, einschließlich einiger allgemeiner Dateipfade, und definiert die Beziehung zwischen Komponenten (_WebParts_ & _-Anwendungen_) in einem Paket.

## <a name="configuration-file"></a>Konfigurationsdatei

Das Schema für die Konfigurationsdatei ist wie folgt:

```javascript
interface IPackageSolutionOptions {
  paths?: IPackageSolutionPathOptions;
  solution: ISolution;
}
```

Jede Paketkonfigurationsdatei weist einige optionale Einstellungen zum Überschreiben der Stellen auf, an denen die Aufgabe nach unterschiedlichen Quelldateien und Manifesten sucht und definiert den Ort zum Schreiben des Pakets. Darüber hinaus weist sie eine erforderliche Lösungsdefinition auf, die dem Packager bezüglich der Beziehungen verschiedener Komponenten Anweisungen gibt.

### <a name="solution-definition-isolution"></a>Lösungsdefinition (_ISolution_)

```javascript
interface ISolution {
  name: string;
  id: string;
  version?: string;
  features?: IFeature[];
}
```

Jede Lösungsdatei muss einen **Namen** haben, der das Paket in der SharePoint-Benutzeroberfläche identifiziert. Darüber hinaus muss jedes Paket einen Globally Unique Identifier (global eindeutigen Bezeichner) (**id**) aufweisen, der intern von SharePoint verwendet wird. Optional können Sie auch eine **Versionsnummer** im Format "X.X.X.X" angeben, die zum Identifizieren unterschiedlicher Versionen des Pakets beim Upgraden verwendet wird.

Die Lösungsdefinition enthält optional eine Liste der SharePoint-Featuredefinitionen. **Hinweis:** Wenn dies nicht angegeben oder leer ist, erstellt die Aufgabe eine einzelne Funktion für jede Komponente (eine 1:1-Zuordnung).

### <a name="feature-definition-ifeature"></a>Funktionsdefinition (_IFeature_)

```javascript
interface IFeature {
  title: string;
  description: string;
  id: string;
  version?: string;
  componentIds?: string[];
}
```

Es ist wichtig zu beachten, dass dies eine Definition für das Erstellen einer SharePoint-Funktion ist und dass einige dieser Optionen in der Benutzeroberfläche verfügbar gemacht werden. Ähnlich wie die Lösung weist jede Funktion einen obligatorischen **Titel**, eine **Beschreibung**, eine **ID** und eine **Versionsnummer** (im Format X.X.X.X) auf. Beachten Sie, dass die Feature-**ID** auch ein Globally Unique Identifier (Global eindeutiger Bezeichner) sein sollte.

Jede Funktion kann auch eine beliebige Anzahl von Komponenten enthalten, die beim Aktivieren der Funktion aktiviert werden. Dies wird über eine Liste von **componentIds** definiert, bei denen es sich um global eindeutige Bezeichner handelt, die mit der **ID** in der Manifestdatei der Komponente übereinstimmen **MÜSSEN**. Wenn diese Liste nicht definiert oder leer ist, schließt der Packager **jede** Komponente in die Funktion ein.

### <a name="file-paths-ipackagesolutionpathoptions"></a>Dateipfade (_IPackageSolutionPathOptions_)

```javascript
interface IPackageSolutionPathOptions {
  rawPackageDir: string;
  zippedPackage: string;
  featureXmlDir: string;
}
```

* **rawPackageDir** ist das Verzeichnis, in das die entpackten Paketdateien geschrieben werden.
* **zippedPackage** ist der Name des ZIP-Pakets, einschließlich der Erweiterung (.spapp).
* **featureXmlDir** ist das Verzeichnis, in dem sich die benutzerdefinierte Funktions-XML befindet.

### <a name="examples"></a>Beispiele

#### <a name="default-configuration"></a>Standardkonfiguration

```json
{
  "paths": {
    "rawPackageDir": "./sharepoint/solution/debug",
    "zippedPackage": "ClientSolution.spapp",
    "featureXmlDir": "./sharepoint/feature_xml"
  },
  "solution": {
    "name": "A Sample Solution",
    "id": "00000000-0000-0000-0000-000000000000",
    "version": "1.0.0.0"
  }
}
```

### <a name="custom-featurexml"></a>Benutzerdefinierte Funktions-XML

Um mehrere SharePoint-Ressourcen (z. B. Listenvorlagen, Seiten oder Inhaltstypen) bereitzustellen, kann die Funktions-XML auch in das Paket eingefügt werden. Dies wird verwendet, um für Anwendungen erforderliche Ressourcen bereitzustellen, kann aber auch für WebParts verwendet werden. Die Dokumentation für die Funktions-XML befindet sich [hier](https://msdn.microsoft.com/en-us/library/office/ms475601.aspx?f=255&MSPPError=-2147217396).

Die Verpackungsaufgabe sucht standardmäßig nach der benutzerdefinierten Funktions-XML unter **./sharepoint/feature_xml**. Alle Dateien in diesem Ordner werden im endgültigen Anwendungspaket berücksichtigt. Die Aufgabe ist jedoch vom Inhalt des _rels/-Ordners abhängig, um zu bestimmen, welche benutzerdefinierten Funktionen definiert werden. Im Wesentlichen wird davon ausgegangen, dass jede **. xml.rels**-Datei mit einer feature.xml-Datei mit demselben Namen auf der obersten Ebene von **feature_xml /** verknüpft ist und eine Beziehung zu der **AppManifest.xml.rels**-Datei hinzufügt, einschließlich dieser Funktion im Paket.