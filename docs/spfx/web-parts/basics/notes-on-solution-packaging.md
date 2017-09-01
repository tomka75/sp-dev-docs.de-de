# <a name="notes-on-solution-packaging"></a><span data-ttu-id="76096-101">Hinweise zu Lösungspaketen</span><span class="sxs-lookup"><span data-stu-id="76096-101">Notes on solution packaging</span></span>

<span data-ttu-id="76096-102">Die Gulp-Aufgabe **package-solution** sucht unter **/config/package-solution.json** nach unterschiedlichen Konfigurationsdetails, einschließlich einiger allgemeiner Dateipfade, und definiert die Beziehung zwischen Komponenten (_WebParts_ und _Anwendungen_) in einem Paket.</span><span class="sxs-lookup"><span data-stu-id="76096-102">The package-solution gulp task looks at /config/package-solution.json for various configuration details, including some generic filepaths, as well as defining the relationship between components (WebParts  Applications) in a package.</span></span>

## <a name="configuration-file"></a><span data-ttu-id="76096-103">Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="76096-103">Configuration File</span></span>

<span data-ttu-id="76096-104">Das Schema für die Konfigurationsdatei ist wie folgt:</span><span class="sxs-lookup"><span data-stu-id="76096-104">The schema for the configuration file is as follows:</span></span>

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

<span data-ttu-id="76096-p101">Jede Paketkonfigurationsdatei weist einige optionale Einstellungen zum Überschreiben der Stellen auf, an denen die Aufgabe nach unterschiedlichen Quelldateien und Manifesten sucht, und definiert den Ort zum Schreiben des Pakets. Darüber hinaus weist sie eine erforderliche Lösungsdefinition auf, die dem Packager bezüglich der Beziehungen verschiedener Komponenten Anweisungen gibt.</span><span class="sxs-lookup"><span data-stu-id="76096-p101">Each package configuration file has some optional settings to override the places where the task will look for various source files & manifests, as well as defining the location to write the package. Additionally, it has a required solution definition, which instructs the packager on the relationships of various components.</span></span>

### <a name="solution-definition-isolution"></a><span data-ttu-id="76096-107">Lösungsdefinition (_ISolution_)</span><span class="sxs-lookup"><span data-stu-id="76096-107">Solution definition (_ISolution_)</span></span>

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

<span data-ttu-id="76096-p102">Jede Lösungsdatei muss einen **Namen** haben, der das Paket in der SharePoint-Benutzeroberfläche identifiziert. Darüber hinaus muss jedes Paket einen Globally Unique Identifier (global eindeutigen Bezeichner) (**id**) aufweisen, der intern von SharePoint verwendet wird. Optional können Sie auch eine **Versionsnummer** im Format "X.X.X.X" angeben, die zum Identifizieren unterschiedlicher Versionen des Pakets beim Upgraden verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="76096-p102">Each solution file must have a **name**, which identifies the package in the SharePoint UI. Additionally, each package must contain a globally unique identifier (**id**), which is used internally by SharePoint. Optionally, you may also specify a **version** number in the format "X.X.X.X", which is used to identify various versions of the package when upgrading.</span></span>

<span data-ttu-id="76096-111">Die Lösungsdefinition enthält optional eine Liste der SharePoint-Featuredefinitionen.</span><span class="sxs-lookup"><span data-stu-id="76096-111">The solution definition also optionally contains a list of SharePoint Feature definitions.</span></span>

> <span data-ttu-id="76096-112">**Hinweis:** Wenn dies nicht angegeben oder leer ist, erstellt die Aufgabe eine einzelne Funktion für jede Komponente (eine 1:1-Zuordnung).</span><span class="sxs-lookup"><span data-stu-id="76096-112">The solution definition also optionally contains a list of SharePoint Feature definitions. **Note:** If this is omitted or empty, the task will create a single Feature for every component (a 1:1 mapping).</span></span>

### <a name="feature-definition-ifeature"></a><span data-ttu-id="76096-113">Funktionsdefinition (_IFeature_)</span><span class="sxs-lookup"><span data-stu-id="76096-113">Feature definition (_IFeature_)</span></span>

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

<span data-ttu-id="76096-p103">Es ist wichtig zu beachten, dass dies eine Definition für das Erstellen einer SharePoint-Funktion ist und dass einige dieser Optionen in der Benutzeroberfläche verfügbar gemacht werden. Ähnlich wie die Lösung weist jede Funktion einen obligatorischen **Titel**, eine **Beschreibung**, eine **ID** und eine **Versionsnummer** (im Format X.X.X.X) auf. Beachten Sie, dass die Feature-**ID** auch ein Globally Unique Identifier (Global eindeutiger Bezeichner) sein sollte.</span><span class="sxs-lookup"><span data-stu-id="76096-p103">It's important to note that this is a definition for creating a SharePoint Feature, and that some of these options will be exposed in the UI. Similarly to the solution, each Feature has a mandatory **title**, **description**, **id**, and **version** number (in the X.X.X.X format). Please note that the Feature **id** should also be a globally unique identifier.</span></span>

<span data-ttu-id="76096-p104">Jede Funktion kann auch eine beliebige Anzahl von Komponenten enthalten, die beim Aktivieren der Funktion aktiviert werden. Dies wird über eine Liste von **componentIds** definiert, bei denen es sich um global eindeutige Bezeichner handelt, die mit der **ID** in der Manifestdatei der Komponente übereinstimmen **MÜSSEN**. Wenn diese Liste nicht definiert oder leer ist, schließt der Packager **jede** Komponente in die Funktion ein.</span><span class="sxs-lookup"><span data-stu-id="76096-p104">Each feature can also contain any number of components, which will be activated when the feature is activated. This is defined via a list of **componentIds**, which are globally unique identifiers that **MUST** match the **ID** in the component's Manifest file. If this list is undefined or empty the packager will include **every** component in the feature.</span></span>

### <a name="file-paths"></a><span data-ttu-id="76096-120">Dateipfade</span><span class="sxs-lookup"><span data-stu-id="76096-120">File paths (IPackageSolutionPathOptions)</span></span>

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

* <span data-ttu-id="76096-p105">**packageDir**: Stammordner für die Verpackung. Standardmäßig „./sharepoint“. Alle anderen Pfade sind relativ zu diesem Ordner.</span><span class="sxs-lookup"><span data-stu-id="76096-p105">**packageDir**: packaging root folder. Defaults to './sharepoint'. All other paths are relative to this folder</span></span>
* <span data-ttu-id="76096-p106">**debugDir**: Ordner, in dem das unformatierte Paket zum Debuggen auf die Festplatte geschrieben wird. Standardmäßig „solution/debug“.</span><span class="sxs-lookup"><span data-stu-id="76096-p106">**debugDir**: folder to write the raw package to disk for debugging. Defaults to 'solution/debug'</span></span>
* <span data-ttu-id="76096-126">**zippedPackage**: Name der zu erstellenden SPPKG-Datei (einschließlich Erweiterung). Standardmäßig „ClientSolution.sppkg“.</span><span class="sxs-lookup"><span data-stu-id="76096-126">**zippedPackage**: name of the sppkg file to create (including extension) Defaults to 'ClientSolution.sppkg'</span></span>
* <span data-ttu-id="76096-p107">**featureXmlDir**: Ordner, der die benutzerdefinierte Funktions-XML enthält, die in das Paket importiert werden soll. Standardmäßig „feature_xml“.</span><span class="sxs-lookup"><span data-stu-id="76096-p107">**featureXmlDir**: folder containing the custom feature xml to import into the package. Defaults to 'feature_xml'.</span></span>
  > <span data-ttu-id="76096-129">**Wichtig:** Beachten Sie, dass alle Dateien in diesem Ordner in die SPPKG-Datei eingeschlossen werden. Sie müssen jedoch eine RELS-Datei für die benutzerdefinierte Funktion erstellen, damit diese in das Paketmanifest eingeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="76096-129">**Important:** Note that all files in this folder will be included in the SPPKG, however, you must create a .rels file for your custom feature for it to be included in the package manifest.</span></span>
* <span data-ttu-id="76096-p108">**manifestsMatch**: Zum Suchen von Manifestdateien. Sucht in **dist/** bei normaler Ausführung, aber für die Produktion in **deploy/**.</span><span class="sxs-lookup"><span data-stu-id="76096-p108">**manifestsMatch**: glob to match against to find manifest files. Looks in **dist/** when running in normal, but **deploy/** for production.</span></span>
* <span data-ttu-id="76096-p109">**manifestDir**: Pfad zu dem Ordner, in dem Manifeste gespeichert werden. Standardmäßig „buildConfig.distFolder“.</span><span class="sxs-lookup"><span data-stu-id="76096-p109">**manifestDir**: path to the folder where manifests are stored. Defaults to 'buildConfig.distFolder'</span></span>
* <span data-ttu-id="76096-p110">**sharepointAssetDir**: Verzeichnis mit SharePoint-Ressourcen (z. B. Funktionselemente, Elementmanifeste und Upgradeaktionen), die automatisch in das SharePoint-Paket eingeschlossen werden. Standardmäßig „assets“.</span><span class="sxs-lookup"><span data-stu-id="76096-p110">**sharepointAssetDir**: directory containing SharePoint assets (such as feature elements, element manifests, and upgrade actions), which will be automatically included in the SharePoint package. Defaults to 'assets'.</span></span>

### <a name="examples"></a><span data-ttu-id="76096-136">Beispiele</span><span class="sxs-lookup"><span data-stu-id="76096-136">Examples</span></span>

#### <a name="default-configuration"></a><span data-ttu-id="76096-137">Standardkonfiguration</span><span class="sxs-lookup"><span data-stu-id="76096-137">Default Configuration</span></span>

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

### <a name="custom-featurexml"></a><span data-ttu-id="76096-138">Benutzerdefinierte Funktions-XML</span><span class="sxs-lookup"><span data-stu-id="76096-138">Custom Feature.xml</span></span>

<span data-ttu-id="76096-p111">Um mehrere SharePoint-Ressourcen (z. B. Listenvorlagen, Seiten oder Inhaltstypen) bereitzustellen, kann die Funktions-XML auch in das Paket eingefügt werden. Dies wird verwendet, um für Anwendungen erforderliche Ressourcen bereitzustellen, kann aber auch für WebParts verwendet werden. Die Dokumentation für die Funktions-XML befindet sich [hier](https://msdn.microsoft.com/en-us/library/office/ms475601.aspx?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="76096-p111">In order support provisioning of various SharePoint resources (such as List Templates, Pages, or Content Types), custom Feature XML may also be injected into the package. This is used in order to provision resources necessary for applications, but may also be used for WebParts. The documentation for Feature XML is located [here](https://msdn.microsoft.com/en-us/library/office/ms475601.aspx?f=255&MSPPError=-2147217396).</span></span>

<span data-ttu-id="76096-p112">Die Verpackungsaufgabe sucht standardmäßig nach der benutzerdefinierten Funktions-XML unter **./sharepoint/feature_xml**. Alle Dateien in diesem Ordner werden im endgültigen Anwendungspaket berücksichtigt. Die Aufgabe ist jedoch vom Inhalt des **_rels/**-Ordners abhängig, um zu bestimmen, welche benutzerdefinierten Funktionen definiert werden. Im Wesentlichen wird davon ausgegangen, dass jede **.xml.rels**-Datei mit einer feature.xml-Datei mit demselben Namen auf der obersten Ebene von **feature_xml/** verknüpft ist und eine Beziehung zu der **AppManifest.xml.rels**-Datei hinzufügt, einschließlich dieser Funktion im Paket.</span><span class="sxs-lookup"><span data-stu-id="76096-p112">By default, the packaging task looks for the custom Feature XML in **./sharepoint/feature_xml**. Every file in this folder will be included in the final application package. However, the task relies on the contents of the  _rels/ folder to determine which custom features are defined. Essentially, it assumes that each **.xml.rels** file is related to a feature.xml of the same name at the top level of the **feature_xml/**, and will add a relationship to the **AppManifest.xml.rels** file including that Feature in the package.</span></span>