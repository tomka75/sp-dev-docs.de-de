---
title: "Hinweise zu Lösungspaketen"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 41baeeed27f08f155b425d7886f1f54aae4e670d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="notes-on-solution-packaging"></a>Hinweise zu Lösungspaketen

Die Gulp-Aufgabe **package-solution** sucht unter **/config/package-solution.json** nach unterschiedlichen Konfigurationsdetails, einschließlich einiger allgemeiner Dateipfade, und definiert die Beziehung zwischen Komponenten (_WebParts_ und _Anwendungen_) in einem Paket.

## <a name="configuration-file"></a>Konfigurationsdatei

Das Schema für die Konfigurationsdatei ist wie folgt:

```ts
interface IPackageSolutionTaskConfig {
    paths?: {
        packageDir?: string;
        debugDir?: string;
        zippedPackage?: string;
        featureXmlDir?: string;
        manifestsMatch?: string;
        manifestDir?: string;
        sharepointAssetDir?: string;
    };
    solution?: ISolution;
}
```

Jede Paketkonfigurationsdatei weist einige optionale Einstellungen zum Überschreiben der Stellen auf, an denen die Aufgabe nach unterschiedlichen Quelldateien und Manifesten sucht, und definiert den Ort zum Schreiben des Pakets. Darüber hinaus weist sie eine erforderliche Lösungsdefinition auf, die dem Packager bezüglich der Beziehungen verschiedener Komponenten Anweisungen gibt.

### <a name="solution-definition-isolution"></a>Lösungsdefinition (_ISolution_)

```ts
interface ISolution {
    name: string;
    id: string;
    title?: string;
    supportedLocales?: string[];
    version?: string;
    features?: IFeature[];
    iconPath?: string;
    skipFeatureDeployment?: boolean;
}
```

Jede Lösungsdatei muss einen **Namen** haben, der das Paket in der SharePoint-Benutzeroberfläche identifiziert. Darüber hinaus muss jedes Paket einen Globally Unique Identifier (global eindeutigen Bezeichner) (**id**) aufweisen, der intern von SharePoint verwendet wird. Optional können Sie auch eine **Versionsnummer** im Format "X.X.X.X" angeben, die zum Identifizieren unterschiedlicher Versionen des Pakets beim Upgraden verwendet wird.

Die Lösungsdefinition enthält optional eine Liste der SharePoint-Featuredefinitionen.

> **Hinweis:** Wenn dies nicht angegeben oder leer ist, erstellt die Aufgabe eine einzelne Funktion für jede Komponente (eine 1:1-Zuordnung).

### <a name="feature-definition-ifeature"></a>Funktionsdefinition (_IFeature_)

```ts
interface IFeature {
    title: string;
    description: string;
    id: string;
    version?: string;
    componentIds?: string[];
    components: IComponent[];
    assets: ISharepointAssets<string>;
}
```

Es ist wichtig zu beachten, dass dies eine Definition für das Erstellen einer SharePoint-Funktion ist und dass einige dieser Optionen in der Benutzeroberfläche verfügbar gemacht werden. Ähnlich wie die Lösung weist jede Funktion einen obligatorischen **Titel**, eine **Beschreibung**, eine **ID** und eine **Versionsnummer** (im Format X.X.X.X) auf. Beachten Sie, dass die Feature-**ID** auch ein Globally Unique Identifier (Global eindeutiger Bezeichner) sein sollte.

Jede Funktion kann auch eine beliebige Anzahl von Komponenten enthalten, die beim Aktivieren der Funktion aktiviert werden. Dies wird über eine Liste von **componentIds** definiert, bei denen es sich um global eindeutige Bezeichner handelt, die mit der **ID** in der Manifestdatei der Komponente übereinstimmen **MÜSSEN**. Wenn diese Liste nicht definiert oder leer ist, schließt der Packager **jede** Komponente in die Funktion ein.

### <a name="file-paths"></a>Dateipfade

```ts
interface IPackageSolutionTaskConfig {
    paths?: {
        packageDir?: string;
        debugDir?: string;
        zippedPackage?: string;
        featureXmlDir?: string;
        manifestsMatch?: string;
        manifestDir?: string;
        sharepointAssetDir?: string;
    };
    solution?: ISolution;
}
```

* **packageDir**: Stammordner für die Verpackung. Standardmäßig „./sharepoint“. Alle anderen Pfade sind relativ zu diesem Ordner.
* **debugDir**: Ordner, in dem das unformatierte Paket zum Debuggen auf die Festplatte geschrieben wird. Standardmäßig „solution/debug“.
* **zippedPackage**: Name der zu erstellenden SPPKG-Datei (einschließlich Erweiterung). Standardmäßig „ClientSolution.sppkg“.
* **featureXmlDir**: Ordner, der die benutzerdefinierte Funktions-XML enthält, die in das Paket importiert werden soll. Standardmäßig „feature_xml“.
  > **Wichtig:** Beachten Sie, dass alle Dateien in diesem Ordner in die SPPKG-Datei eingeschlossen werden. Sie müssen jedoch eine RELS-Datei für die benutzerdefinierte Funktion erstellen, damit diese in das Paketmanifest eingeschlossen wird.
* **manifestsMatch**: Zum Suchen von Manifestdateien. Sucht in **dist/** bei normaler Ausführung, aber für die Produktion in **deploy/**.
* **manifestDir**: Pfad zu dem Ordner, in dem Manifeste gespeichert werden. Standardmäßig „buildConfig.distFolder“.
* **sharepointAssetDir**: Verzeichnis mit SharePoint-Ressourcen (z. B. Funktionselemente, Elementmanifeste und Upgradeaktionen), die automatisch in das SharePoint-Paket eingeschlossen werden. Standardmäßig „assets“.

### <a name="examples"></a>Beispiele

#### <a name="default-configuration"></a>Standardkonfiguration

```json
{
  "solution": {
    "name": "spfx-hello-world-client-side-solution",
    "id": "77fd2eed-55b0-42bf-8b4d-f66730cb0c34",
    "version": "1.0.0.0"
  },
  "paths": {
    "zippedPackage": "solution/spfx-hello-world.sppkg"
  }
}
```

### <a name="custom-featurexml"></a>Benutzerdefinierte Funktions-XML

Um mehrere SharePoint-Ressourcen (z. B. Listenvorlagen, Seiten oder Inhaltstypen) bereitzustellen, kann die Funktions-XML auch in das Paket eingefügt werden. Dies wird verwendet, um für Anwendungen erforderliche Ressourcen bereitzustellen, kann aber auch für WebParts verwendet werden. Die Dokumentation für die Funktions-XML befindet sich [hier](https://msdn.microsoft.com/en-us/library/office/ms475601.aspx?f=255&MSPPError=-2147217396).

Die Verpackungsaufgabe sucht standardmäßig nach der benutzerdefinierten Funktions-XML unter **./sharepoint/feature_xml**. Alle Dateien in diesem Ordner werden im endgültigen Anwendungspaket berücksichtigt. Die Aufgabe ist jedoch vom Inhalt des **_rels/**-Ordners abhängig, um zu bestimmen, welche benutzerdefinierten Funktionen definiert werden. Im Wesentlichen wird davon ausgegangen, dass jede **.xml.rels**-Datei mit einer feature.xml-Datei mit demselben Namen auf der obersten Ebene von **feature_xml/** verknüpft ist und eine Beziehung zu der **AppManifest.xml.rels**-Datei hinzufügt, einschließlich dieser Funktion im Paket.