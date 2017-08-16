# <a name="build-your-first-listview-command-set-extension"></a><span data-ttu-id="9e800-101">Erstellen Ihrer ersten Erweiterung des Typs „ListView Command Set“</span><span class="sxs-lookup"><span data-stu-id="9e800-101">Build your first ListView Command Set extension</span></span>

><span data-ttu-id="9e800-p101">**Hinweis:** Die SharePoint Framework-Erweiterungen befinden sich derzeit in der Preview-Phase. Änderungen sind vorbehalten. Die Verwendung von SharePoint Framework-Erweiterungen in Produktionsumgebungen wird aktuell nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="9e800-p101">**Note:** The SharePoint Framework Extensions are currently in preview and are subject to change. SharePoint Framework Extensions are not currently supported for use in production environments.</span></span>

<span data-ttu-id="9e800-p102">Erweiterungen sind clientseitige Komponenten, die im Kontext einer SharePoint-Seite ausgeführt werden. Sie lassen sich in SharePoint Online bereitstellen und mithilfe aktueller JavaScript-Tools und -Bibliotheken erstellen.</span><span class="sxs-lookup"><span data-stu-id="9e800-p102">Extensions are client-side components that run inside the context of a SharePoint page. Extensions can be deployed to SharePoint Online and you can use modern JavaScript tools and libraries to build them.</span></span>

><span data-ttu-id="9e800-p103">**Hinweis:** Bevor Sie die Schritte in diesem Artikel durchführen, müssen Sie [Ihre Entwicklungsumgebung einrichten](../../set-up-your-development-environment). Beachten Sie, dass Erweiterungen derzeit **AUSSCHLIESSLICH** über Office 365-Entwicklermandanten verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="9e800-p103">**Note:** Before following the steps in this article, be sure to [Set up your development environment](../../set-up-your-development-environment). Notice that extensions are currently **ONLY** available from Office 365 developer tenants.</span></span>

><span data-ttu-id="9e800-p104">**Hinweis:** Erweiterungen des Typs „ListView Command Set“ lassen sich derzeit nur mit der modernen Oberfläche auf klassischen SharePoint-Websites debuggen. Stellen Sie sicher, dass Sie für die Tests eine klassische Teamwebsite mit moderner Listenoberfläche verwenden.</span><span class="sxs-lookup"><span data-stu-id="9e800-p104">**Note:** Currently ListView Command Set Extension can only be debugged with the modern experience in classic SharePoint sites. Please ensure that you use a classic team site with modern list experience for the testing.</span></span>

## <a name="create-an-extension-project"></a><span data-ttu-id="9e800-110">Erstellen eines Erweiterungsprojekts</span><span class="sxs-lookup"><span data-stu-id="9e800-110">Create an extension project</span></span>
<span data-ttu-id="9e800-111">Erstellen Sie an einem Speicherort Ihrer Wahl ein neues Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="9e800-111">Create a new project directory in your favorite location.</span></span>

```
md command-extension
```

<span data-ttu-id="9e800-112">Wechseln Sie in das Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="9e800-112">Go to the project directory.</span></span>

```
cd command-extension
```

<span data-ttu-id="9e800-113">Führen Sie den Yeoman-SharePoint-Generator aus, um eine neue HelloWorld-Erweiterung zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="9e800-113">Create a new HelloWorld extension by running the Yeoman SharePoint Generator.</span></span>

```
yo @microsoft/sharepoint
```

<span data-ttu-id="9e800-114">Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="9e800-114">When prompted:</span></span>

* <span data-ttu-id="9e800-115">Übernehmen Sie den Standardwert **command-extension** als Namen der Lösung, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="9e800-115">Accept the default value of **command-extension** as your solution name and press **Enter**.</span></span>
* <span data-ttu-id="9e800-116">Wählen Sie **Extension (Preview)** als den zu erstellenden Typ von clientseitiger Komponente aus.</span><span class="sxs-lookup"><span data-stu-id="9e800-116">Choose **Extension (Preview)** as the client-side component type to be created.</span></span> 
* <span data-ttu-id="9e800-117">Wählen Sie **ListView Command Set (Preview)** als den zu erstellenden Typ von Erweiterung aus.</span><span class="sxs-lookup"><span data-stu-id="9e800-117">Choose **ListView Command Set (Preview)** as the extension type to be created.</span></span>

<span data-ttu-id="9e800-118">Über die nächsten Eingabeaufforderungen werden spezifische Informationen zu der Erweiterung abgefragt:</span><span class="sxs-lookup"><span data-stu-id="9e800-118">The next set of prompts will ask for specific information about your extension:</span></span>

* <span data-ttu-id="9e800-119">Übernehmen Sie den Standardwert **HelloWorld** als Namen für Ihre Erweiterung, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="9e800-119">Accept the default value of **HelloWorld** as your extension name and press **Enter**.</span></span>
* <span data-ttu-id="9e800-120">Übernehmen Sie den Standardwert **HelloWorld description** als Beschreibung Ihrer Erweiterung, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="9e800-120">Accept the default value of **HelloWorld description** as your extension description and press **Enter**.</span></span>

![Yeoman-SharePoint-Generator mit Eingabeaufforderungen zur Erstellung einer Erweiterungslösung](../../../../images/ext-com-yeoman-prompts.png)

<span data-ttu-id="9e800-p105">An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien sowie die **HelloWorld**-Erweiterung. Das kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="9e800-p105">At this point, Yeoman will install the required dependencies and scaffold the solution files along with the **HelloWorld** extension. This might take a few minutes.</span></span> 

<span data-ttu-id="9e800-124">Nach Abschluss der Gerüsterstellung sollte folgende Erfolgsmeldung angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="9e800-124">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

![Erfolgreiche Erstellung eines Gerüsts für die clientseitige SharePoint-Lösung](../../../../images/ext-com-yeoman-complete.png)

<span data-ttu-id="9e800-126">Details zur Behebung etwaiger Fehler finden Sie unter [Known issues](../../web-parts/basics/known-issues).</span><span class="sxs-lookup"><span data-stu-id="9e800-126">For information about troubleshooting any errors, see [Known issues](../../web-parts/basics/known-issues).</span></span>

<span data-ttu-id="9e800-127">Geben Sie nach der Erstellung des Lösungsgerüsts Folgendes in die Konsole ein, um Visual Studio Code zu starten:</span><span class="sxs-lookup"><span data-stu-id="9e800-127">Once the solution scaffolding is completed, type the following into the console to start Visual Studio Code.</span></span>

```
code .
```

> <span data-ttu-id="9e800-128">Beachten Sie: Da die clientseitige SharePoint-Lösung auf HTML/TypeScript basiert, können Sie zur Erstellung Ihrer Erweiterung jeden Code-Editor verwenden, der clientseitige Entwicklung unterstützt.</span><span class="sxs-lookup"><span data-stu-id="9e800-128">Notice that because the SharePoint client-side solution is HTML/TypeScript based, you can use any code editor that supports client-side development to build your extension.</span></span>

<span data-ttu-id="9e800-p106">Wie Sie sehen, entspricht die Standardlösungsstruktur der Lösungsstruktur clientseitiger Webparts. Hierbei handelt es sich um die grundlegende SharePoint Framework-Lösungsstruktur, die für alle Lösungstypen vergleichbare Konfigurationsoptionen bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="9e800-p106">Notice how the default solution structure is like the solution structure of client-side web parts. This is the basic SharePoint Framework solution structure, with similar configuration options across all solution types.</span></span>

![SharePoint Framework-Lösung nach der Erstellung des anfänglichen Gerüsts](../../../../images/ext-com-vscode-solution-structure.png)

<span data-ttu-id="9e800-132">Öffnen Sie die Datei **HelloWorldCommandSet.manifest.json** im Ordner **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="9e800-132">Open **HelloWorldCommandSet.manifest.json** in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="9e800-p107">In dieser Datei sind der Erweiterungstyp und ein eindeutiger Bezeichner **„id“** für die Erweiterung definiert. Sie benötigen diesen eindeutigen Bezeichner später, um die Erweiterung zu debuggen und in SharePoint bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="9e800-p107">This file defines your extension type and a unique identifier **“id”** for your extension. You’ll need this unique identifier later when debugging and deploying your extension to SharePoint.</span></span>

<span data-ttu-id="9e800-p108">In der Manifestdatei finden Sie auch die tatsächlichen Befehlsdefinitionen. Hierbei handelt es sich um die Schaltflächen, die später basierend auf dem Registrierungsziel verfügbar gemacht werden. In der Standardvorlage sind zwei Schaltflächen definiert: *„Command One“* und *„Command Two“*.</span><span class="sxs-lookup"><span data-stu-id="9e800-p108">Notice also the actual command definitions in the manifest file. These are the actual buttons which will be exposed based on the registration target. In the default template, you'll find two different buttons: *"Command One"* and *"Command Two"*</span></span>

![Inhalt der JSON-Manifestdatei für die Erweiterung des Typs „ListView Command Set“](../../../../images/ext-com-vscode-manifest.png)

> <span data-ttu-id="9e800-p109">Derzeit lassen sich Bilder nur von absoluten Speicherorten in einem CDN korrekt im Manifest referenzieren. Dies wird in zukünftigen Versionen verbessert werden.</span><span class="sxs-lookup"><span data-stu-id="9e800-p109">Currently, images are not properly referenced unless you are referring to them from absolute locations in a CDN within your manifest. This will be improved in future releases.</span></span>

## <a name="coding-your-listview-command-set"></a><span data-ttu-id="9e800-141">Programmieren Ihrer Erweiterung des Typs „ListView Command Set“</span><span class="sxs-lookup"><span data-stu-id="9e800-141">Coding your ListView Command Set</span></span> 
<span data-ttu-id="9e800-142">Öffnen Sie die Datei **HelloWorldCommandSet.ts** im Ordner **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="9e800-142">Open the **HelloWorldCommandSet.ts** file in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="9e800-143">Wie Sie sehen, wird die Basisklasse Ihrer Erweiterung des Typs „ListView Command Set“ aus dem Paket **sp-listview-extensibility** importiert. Es enthält SharePoint Framework-Code, der von „ListView Command Set“ benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="9e800-143">Notice that the base class for the ListView Command Set is imported from the **sp-listview-extensibility** package, which contains SharePoint framework code required by the ListView Command Set.</span></span>

![Importanweisung zum Importieren von „BaseListViewCommandSet“ aus „@microsoft/sp-listview-extensibility“](../../../../images/ext-com-vscode-base.png)

<span data-ttu-id="9e800-145">Das Verhalten Ihrer benutzerdefinierten Schaltflächen wird in den Methoden **onRefreshCommand()** und **OnExecute()** definiert.</span><span class="sxs-lookup"><span data-stu-id="9e800-145">The behavior for your custom buttons is contained in the **onRefreshCommand()** and **OnExecute()** methods.</span></span>

<span data-ttu-id="9e800-p110">Das Ereignis **onRefreshCommand()** tritt für jeden Befehl (d. h. für jedes Menüelement) separat ein, und zwar immer dann, wenn die Anwendung versucht, den Befehl auf der Benutzeroberfläche anzuzeigen. Der Funktionsparameter `“event”` enthält Informationen über den zu rendernden Befehl. Anhand dieser Informationen kann der Handler den Titel und die Sichtbarkeit anpassen. Soll ein Befehl beispielsweise nur angezeigt werden, wenn eine bestimmte Anzahl von Elementen in der Listenansicht ausgewählt wurde, würde das standardmäßig wie folgt implementiert:</span><span class="sxs-lookup"><span data-stu-id="9e800-p110">The **onRefreshCommand()** event occurs separately for each command (e.g. menu item), whenever the application attempts to display it in the UI. The `“event”` function parameter represents information about the command being rendered. The handler can use this information to customize the title or adjust the visibility. For example, if a command should only be shown when a certain number of items are selected in the list view. Here's the default implementation:</span></span>

```ts
  @override
  public onRefreshCommand(event: IListViewCommandSetRefreshEventParameters): void {
    event.visible = true; // assume true by default

    if (this.properties.disabledCommandIds) {
      if (this.properties.disabledCommandIds.indexOf(event.commandId) >= 0) {
        Log.info(LOG_SOURCE, 'Hiding command ' + event.commandId);
        event.visible = false;
      }
    }
  }
```
<span data-ttu-id="9e800-p111">Die Methode **OnExecute()** definiert, was passiert, wenn ein Befehl ausgeführt wird (d. h. wenn der Benutzer auf das Menüelement klickt). In der Standardimplementierung werden unterschiedliche Meldungen angezeigt, je nachdem, auf welche Schaltfläche der Benutzer klickt:</span><span class="sxs-lookup"><span data-stu-id="9e800-p111">The **OnExecute()** method defines what happens when a command is executed (e.g. the menu item is clicked). In the default implementation, different messages are shown based on which button was clicked:</span></span> 

```ts
  @override
  public onExecute(event: IListViewCommandSetExecuteEventParameters): void {
    switch (event.commandId) {
      case 'COMMAND_1':
        alert(`Clicked ${strings.Command1}`);
        break;
      case 'COMMAND_2':
        alert(`Clicked ${strings.Command2}`);
        break;
      default:
        throw new Error('Unknown command');
    }
  }
```


## <a name="debugging-your-listview-command-set-using-gulp-serve-and-query-string-parameters"></a><span data-ttu-id="9e800-153">Debuggen Ihrer Erweiterung des Typs „ListView Command Set“ mit gulp serve und Abfragezeichenfolgeparametern</span><span class="sxs-lookup"><span data-stu-id="9e800-153">Debugging your ListView Command Set using gulp serve and query string parameters</span></span>
<span data-ttu-id="9e800-p112">SharePoint Framework-Erweiterungen lassen sich aktuell nicht mithilfe der lokalen Workbench testen. Sie müssen direkt auf einer aktiven SharePoint Online-Website getestet und entwickelt werden. Dazu ist es jedoch nicht nötig, Ihre Anpassung im App-Katalog bereitzustellen. Dadurch bleibt das Debuggen einfach und effizient.</span><span class="sxs-lookup"><span data-stu-id="9e800-p112">SharePoint Framework extensions cannot be currently tested using the local workbench, so you'll need to test and develop them directly against a live SharePoint Online site. You do not, however, need to deploy your customization to the app catalog to do this, which keeps the debugging experience simple and efficient.</span></span> 

<span data-ttu-id="9e800-156">Zunächst führen Sie den folgenden Befehl aus, um den Code zu kompilieren und die Dateien auf Ihrem lokalen Computer zu hosten:</span><span class="sxs-lookup"><span data-stu-id="9e800-156">First, compile your code and host the compiled files from the local machine by running this command:</span></span>
```
gulp serve --nobrowser
```

<span data-ttu-id="9e800-157">Die Option `--nobrowser` verwenden wir, weil Erweiterungen derzeit nicht lokal debuggt werden können und daher keine Notwendigkeit besteht, die lokale Workbench zu starten.</span><span class="sxs-lookup"><span data-stu-id="9e800-157">Notice that we used the `--nobrowser` option, since there's no value in launching the local workbench since you currently cannot debug extensions locally.</span></span>

<span data-ttu-id="9e800-158">Sobald der Code ohne Fehler kompiliert wurde, wird das resultierende Manifest von *http://localhost:4321* ausgeliefert.</span><span class="sxs-lookup"><span data-stu-id="9e800-158">Once it compiles the code without errors, it will serve the resulting manifest from *http://localhost:4321*.</span></span>

<span data-ttu-id="9e800-159">Navigieren Sie auf Ihrer SharePoint Online-Website zu einer beliebigen SharePoint-Liste, die die moderne Oberfläche verwendet.</span><span class="sxs-lookup"><span data-stu-id="9e800-159">Navigate to any SharePoint list in your SharePoint Online site using the modern experience.</span></span>

<span data-ttu-id="9e800-160">Da unsere Erweiterung des Typs „ListView Command Set“ auf Localhost gehostet wird und aktuell ausgeführt wird, können wir den Code mithilfe spezifischer Debugabfrageparameter in der Listenansicht ausführen.</span><span class="sxs-lookup"><span data-stu-id="9e800-160">Since our ListView Command Set is hosted from localhost and is running, we can use specific debug query parameters to execute the code in the list view.</span></span>

<span data-ttu-id="9e800-p113">Fügen Sie die folgenden Abfragezeichenfolgeparameter an die URL an. Dabei müssen Sie die GUID durch die ID Ihrer Erweiterung des Typs „ListView Command Set“ aus der Datei **HelloWorldCommandSet.manifest.json** ersetzen:</span><span class="sxs-lookup"><span data-stu-id="9e800-p113">Append the following query string parameters to the URL. Notice that you will need to update the GUID to match the ID of your list view command set extension available in the **HelloWorldCommandSet.manifest.json** file:</span></span>

```
?loadSpfx=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"81b6a3d7-e408-43a4-8ef1-180d0f2582cc":{"location":"ClientSideExtension.ListViewCommandSet.CommandBar"}}
```

* <span data-ttu-id="9e800-p114">**loadSPFX=true:** Dieser Parameter stellt sicher, dass SharePoint Framework auf der Seite geladen wird. Aus Leistungsgründen wird das Framework normalerweise erst geladen, wenn mindestens eine Erweiterung registriert ist. Da aktuell noch keine Komponenten registriert sind, müssen Sie das Framework explizit laden.</span><span class="sxs-lookup"><span data-stu-id="9e800-p114">**loadSPFX=true:**  ensures that the SharePoint Framework is loaded on the page. For performance reasons, the framework is not normally loaded unless at least one extension is registered. Since no components are registered yet, we must explicitly load the framework.</span></span>
* <span data-ttu-id="9e800-p115">**debugManifestsFile:** Dieser Parameter gibt an, dass lokal ausgelieferte SPFx-Komponenten geladen werden sollen. Normalerweise sucht das Ladeprogramm nur an zwei Orten nach Komponenten: im App-Katalog (nach Komponenten der bereitgestellten Lösung) und auf dem SharePoint-Manifestserver (nach den Systembibliotheken).</span><span class="sxs-lookup"><span data-stu-id="9e800-p115">**debugManifestsFile:**  specifies that we want to load SPFx components that are being locally served. Normally the loader only looks for components in the App Catalog (for your deployed solution) and the SharePoint manifest server (for the system libraries).</span></span>
* <span data-ttu-id="9e800-p116">**customActions:** Dieser URL-Abfrageparameter simuliert eine benutzerdefinierte Aktion. Für das Objekt *CustomAction* lassen sich zahlreiche Eigenschaften festlegen, die das Design und die Position Ihrer Schaltfläche beeinflussen. Mehr dazu finden Sie weiter unten in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="9e800-p116">**customActions:**  this URL query parameter simulates a custom action. There are many properties you can set on this *CustomAction* object that affect the look, feel, and location of your button; we’ll cover them all later.</span></span>
    * <span data-ttu-id="9e800-170">**Key:** die GUID der Erweiterung</span><span class="sxs-lookup"><span data-stu-id="9e800-170">**Key:** guid of the extension</span></span>
    * <span data-ttu-id="9e800-p117">**location:** wo die Befehle angezeigt werden sollen. Die möglichen Werte sind:</span><span class="sxs-lookup"><span data-stu-id="9e800-p117">**Location:** where the commands are displayed. The possible values are:</span></span>
        * <span data-ttu-id="9e800-173">**ClientSideExtension.ListViewCommandSet.ContextMenu:** im Kontextmenü der Elemente</span><span class="sxs-lookup"><span data-stu-id="9e800-173">**ClientSideExtension.ListViewCommandSet.ContextMenu:**  The context menu of the item(s)</span></span>
        * <span data-ttu-id="9e800-174">**ClientSideExtension.ListViewCommandSet.CommandBar:** im oberen Befehlssatzmenü in einer Liste oder Bibliothek</span><span class="sxs-lookup"><span data-stu-id="9e800-174">**ClientSideExtension.ListViewCommandSet.CommandBar:** The top command set menu in a list or library</span></span>
        * <span data-ttu-id="9e800-175">**ClientSideExtension.ListViewCommandSet:** sowohl im Kontextmenü als auch auf der Befehlsleiste (entspricht SPUserCustomAction.Location="CommandUI.Ribbon")</span><span class="sxs-lookup"><span data-stu-id="9e800-175">**ClientSideExtension.ListViewCommandSet:** Both the context menu and the command bar (Corresponds to SPUserCustomAction.Location="CommandUI.Ribbon")</span></span>
* <span data-ttu-id="9e800-176">**Properties:** ein optionales JSON-Objekt mit Eigenschaften, die über den Member `this.properties` verfügbar gemacht werden.</span><span class="sxs-lookup"><span data-stu-id="9e800-176">**Properties:** an optional JSON object containing properties that will be available via the `this.properties` member.</span></span>

<span data-ttu-id="9e800-177">Die vollständige URL sollte in etwa wie folgt aussehen, abhängig von der URL Ihres Mandanten und der Position der Liste.</span><span class="sxs-lookup"><span data-stu-id="9e800-177">The full URL should look similar to the following, depending on your tenant URL and the location of the list.</span></span>

```
contoso.sharepoint.com/Lists/Orders/AllItems.aspx?loadSpfx=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"81b6a3d7-e408-43a4-8ef1-180d0f2582cc":{"location":"ClientSideExtension.ListViewCommandSet.CommandBar"}}
```

<span data-ttu-id="9e800-178">Klicken Sie bei Aufforderung auf **Load debug scripts**, um das Laden der Debugmanifeste zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="9e800-178">Accept the loading of Debug Manifests, by clicking **Load debug scripts** when prompted.</span></span>

![Akzeptieren des Ladens der Debugskripte](../../../../images/ext-com-accept-debug-scripts.png)

<span data-ttu-id="9e800-180">Nun sehen Sie zwei neue Schaltflächen auf der Symbolleiste mit den Titeln *Command One* und *Command Two*.</span><span class="sxs-lookup"><span data-stu-id="9e800-180">Notice two new buttons available in the toolbar with titles of *Command One* and *Command Two*.</span></span>

![Akzeptieren des Ladens der Debugskripte](../../../../images/ext-com-default-customizer-output.png)

## <a name="enhancing-the-listview-command-set-rendering"></a><span data-ttu-id="9e800-182">Erweitern der Darstellung von Erweiterungen des Typs „ListView Command Set“</span><span class="sxs-lookup"><span data-stu-id="9e800-182">Enhancing the ListView Command Set rendering</span></span>
<span data-ttu-id="9e800-183">Für dieses Beispiel nutzen wir eine neue Dialogfeld-API, mit der Sie über Ihren Code ganz einfach modale Dialogfelder anzeigen lassen können.</span><span class="sxs-lookup"><span data-stu-id="9e800-183">We'll take advantage of a new Dialog API, which can be used to show modal dialogs easily from your code.</span></span> 

<span data-ttu-id="9e800-184">Wechseln Sie wieder zur Konsole, und führen Sie den folgenden Befehl aus, um die Dialogfeld-API in die Lösung einzuschließen:</span><span class="sxs-lookup"><span data-stu-id="9e800-184">Return to the console and execute the following command to include the dialog API in our solution.</span></span>

``` 
npm install @microsoft/sp-dialog --save
```

<span data-ttu-id="9e800-185">Wechseln Sie wieder zu Visual Studio Code (oder Ihrem bevorzugten Editor).</span><span class="sxs-lookup"><span data-stu-id="9e800-185">Return to Visual Studio Code (or your preferred editor).</span></span>

<span data-ttu-id="9e800-186">Öffnen Sie die Datei **HelloWorldCommandSet.ts** im Ordner **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="9e800-186">Open **HelloWorldCommandSet.ts** from the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="9e800-187">Fügen Sie hinter den bereits vorhandenen Importanweisungen die folgende Importanweisung für den Import der Klasse `Dialog` aus `@microsoft/sp-dialog/lib/index` ein.</span><span class="sxs-lookup"><span data-stu-id="9e800-187">Add the following import statement for the `Dialog` class from `@microsoft/sp-dialog/lib/index` after the existing import statements.</span></span> 

```ts
import { Dialog } from '@microsoft/sp-dialog/lib/index';
``` 

<span data-ttu-id="9e800-188">Aktualisieren Sie die Methode **onExecute** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="9e800-188">Update the **onExecute** method as follows</span></span>

```ts
  @override
  public onExecute(event: IListViewCommandSetExecuteEventParameters): void {
    switch (event.commandId) {
      case 'COMMAND_1':
        Dialog.alert(`Clicked ${strings.Command1}`);
        break;
      case 'COMMAND_2':
        Dialog.prompt(`Clicked ${strings.Command2}. Enter something to alert:`).then((value: string) => {
          Dialog.alert(value);
        });
        break;
      default:
        throw new Error('Unknown command');
    }
  }
``` 
<span data-ttu-id="9e800-p118">Wechseln Sie wieder in das Konsolenfenster, und vergewissern Sie sich, dass keine Ausnahmen angezeigt werden. Sollte die Lösung noch nicht auf Localhost ausgeführt werden, führen Sie den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="9e800-p118">Switch back to your console window and ensure that you do not have any exceptions. If you do not already have the solution running in localhost, execute the following command:</span></span>

```
gulp serve --nobrowser
```

<span data-ttu-id="9e800-191">Rufen Sie wieder die Listenansicht auf, und verwenden Sie dieselben Abfrageparameter wie zuvor, nun mit der ID des Bezeichners Ihrer Erweiterung aus der Datei **HelloWorldCommandSet.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="9e800-191">Return to the list view and use the same query parameters used previously with the Id matching your extension identifier available in the **HelloWorldCommandSet.manifest.json** file.</span></span>

<span data-ttu-id="9e800-192">Klicken Sie bei Aufforderung auf **Load debug scripts**, um das Laden der Debugmanifeste zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="9e800-192">Accept the loading of Debug Manifests, by clicking **Load debug scripts** when prompted.</span></span>

![Akzeptieren des Ladens der Debugskripte](../../../../images/ext-com-accept-debug-scripts.png)

<span data-ttu-id="9e800-p119">Es werden immer noch dieselben Schaltflächen auf der Symbolleiste angezeigt, sie verhalten sich nun aber anders, wenn Sie auf sie klicken. Jetzt wird die neue Dialogfeld-API verwendet, die sich selbst in komplexe Lösungsszenarien unkompliziert integrieren lässt.</span><span class="sxs-lookup"><span data-stu-id="9e800-p119">We still have the same buttons in the toolbar, but you'll notice they behave differently if you click them one-by-one. Now we are using the new dialog API, which can be easily used with your solutions even for complex scenarios.</span></span> 

![Dialogfeld auf der Seite](../../../../images/ext-com-dialog-output.png)

## <a name="adding-a-listview-command-set-to-a-solution-package-for-deployment"></a><span data-ttu-id="9e800-197">Hinzufügen einer Erweiterung des Typs „ListView Command Set“ zu einem Lösungspaket zwecks Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="9e800-197">Adding a ListView Command Set to a solution package for deployment</span></span>

<span data-ttu-id="9e800-198">Wechseln Sie wieder zu Ihrer Lösung in Visual Studio Code (oder Ihrem bevorzugten Editor).</span><span class="sxs-lookup"><span data-stu-id="9e800-198">Return to your solution in Visual Studio Code (or to your preferred editor).</span></span>

<span data-ttu-id="9e800-199">Hier müssen Sie zunächst einen Ordner **assets** erstellen, in dem Sie alle Featureframeworkobjekte ablegen, die bei der Paketinstallation zur Bereitstellung von SharePoint-Strukturen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="9e800-199">We'll first need to create an **assets** folder where we will place all feature framework assets used to provision SharePoint structures when the package is installed.</span></span>

* <span data-ttu-id="9e800-200">Erstellen Sie einen Ordner mit dem Namen **sharepoint** im Stammverzeichnis der Lösung.</span><span class="sxs-lookup"><span data-stu-id="9e800-200">Create a folder named **sharepoint** in the root of the solution</span></span>
* <span data-ttu-id="9e800-201">Erstellen Sie einen Ordner mit dem Namen **assets** als Unterordner im soeben erstellten Ordner **sharepoint**.</span><span class="sxs-lookup"><span data-stu-id="9e800-201">Create a folder named **assets** as a sub folder within the just created **sharepoint** folder</span></span>

<span data-ttu-id="9e800-202">Die Lösungsstruktur sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="9e800-202">Your solution structure should look similar to the following picture:</span></span>

![Ordner „assets“ in der Lösungsstruktur](../../../../images/ext-app-assets-folder.png)

### <a name="add-an-elementsxml-file-for-sharepoint-definitions"></a><span data-ttu-id="9e800-204">Hinzufügen einer Datei „elements.xml“ mit SharePoint-Definitionen</span><span class="sxs-lookup"><span data-stu-id="9e800-204">Add an elements.xml file for SharePoint definitions</span></span>

<span data-ttu-id="9e800-205">Erstellen Sie im Ordner **sharepoint\assets** eine neue Datei mit dem Namen **elements.xml**.</span><span class="sxs-lookup"><span data-stu-id="9e800-205">Create a new file inside the **sharepoint\assets** folder named **elements.xml**</span></span>

<span data-ttu-id="9e800-p120">Kopieren Sie die nachfolgende XML-Struktur in die Datei **elements.xml**. Vergessen Sie dabei nicht, für die Eigenschaft **ClientSideComponentId** die eindeutige ID Ihrer Erweiterung des Typs „ListView Command Set“ aus der Datei **HelloWorldCommandSet.manifest.json** im Ordner **src\extensions\helloWorld** anzugeben.</span><span class="sxs-lookup"><span data-stu-id="9e800-p120">Copy the following xml structure into **elements.xml**. Be sure to update the **ClientSideComponentId** property to the unique Id of your ListView Command Set available in the **HelloWorldCommandSet.manifest.json** file in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="9e800-p121">Wie Sie sehen, verwenden wir den Positionswert `ClientSideExtension.ListViewCommandSet.CommandBar`, um anzugeben, dass es sich um eine Erweiterung des Typs „ListView Command Set“ handelt, die auf der Befehlsleiste angezeigt werden soll. Wir legen außerdem für `RegistrationId` den Wert **100** fest und für `RegistrationType` den Wert **List**, um diese benutzerdefinierte Aktion automatisch mit generischen Listen zu verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="9e800-p121">Notice that we use a specific location value of `ClientSideExtension.ListViewCommandSet.CommandBar` to define that this is a ListView Command Set and it should be displayed in the command bar. We also define the `RegistrationId` as **100** and the `RegistrationType` as **List** to associate this custom action automatically with generic lists.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">

    <CustomAction 
        Title="SPFxListViewCommandSet"
        RegistrationId="100"
        RegistrationType="List"
        Location="ClientSideExtension.ListViewCommandSet.CommandBar"
        ClientSideComponentId="5fc73e12-8085-4a4b-8743-f6d02ffe1240">

    </CustomAction>

</Elements>
```

<span data-ttu-id="9e800-210">Für eine Erweiterung des Typs „ListView Command Set“ können Sie folgende Positionswerte angeben:</span><span class="sxs-lookup"><span data-stu-id="9e800-210">Possible location values which can be used with a ListView Command Set:</span></span>

* <span data-ttu-id="9e800-211">`ClientSideExtension.ListViewCommandSet.CommandBar`: auf der Symbolleiste der Liste oder Bibliothek</span><span class="sxs-lookup"><span data-stu-id="9e800-211">`ClientSideExtension.ListViewCommandSet.CommandBar` - Toolbar of the list or library</span></span>
* <span data-ttu-id="9e800-212">`ClientSideExtension.ListViewCommandSet.ContextMenu`: im Kontextmenü von Listen- oder Bibliothekselementen</span><span class="sxs-lookup"><span data-stu-id="9e800-212">`ClientSideExtension.ListViewCommandSet.ContextMenu` - Context menu for list or library items</span></span>
* <span data-ttu-id="9e800-213">`ClientSideExtension.ListViewCommandSet`: Registrierung von Befehlen sowohl auf der Symbolleiste als auch im Kontextmenü</span><span class="sxs-lookup"><span data-stu-id="9e800-213">`ClientSideExtension.ListViewCommandSet` - Register commands to both the toolbar and to the context menu</span></span>

### <a name="ensure-that-definitions-are-taken-into-account-within-the-build-pipeline"></a><span data-ttu-id="9e800-214">Gewährleisten der Berücksichtigung von Definitionen in der Buildpipeline</span><span class="sxs-lookup"><span data-stu-id="9e800-214">Ensure that definitions are taken into account within the build pipeline</span></span>

<span data-ttu-id="9e800-p122">Öffnen Sie die Datei **package-solution.json** im Ordner **config**. Die Datei **package-solution.json** enthält die Paketmetadaten, definiert wie folgt:</span><span class="sxs-lookup"><span data-stu-id="9e800-p122">Open **package-solution.json** from the **config** folder. The **package-solution.json** file defines the package metadata as shown in the following code:</span></span>

```json
{
  "solution": {
    "name": "command-extension-client-side-solution",
    "id": "dfffbe21-e422-4c0f-a302-d7d62a30c1bf",
    "version": "1.0.0.0"
  },
  "paths": {
    "zippedPackage": "solution/command-extension.sppkg"
  }
}
```

<span data-ttu-id="9e800-p123">Um sicherzustellen, dass die neu hinzugefügte Datei **elements.xml** beim Verpacken der Lösung berücksichtigt wird, müssen wir eine Featureframework-Featuredefinition für das Lösungspaket einschließen. Dazu integrieren wir wie nachfolgend demonstriert eine JSON-Definition des benötigten Features in die Lösungsstruktur.</span><span class="sxs-lookup"><span data-stu-id="9e800-p123">To ensure that our newly added **elements.xml** file is taken into account while the solution is being packaged, we'll need to include a Feature Framework feature definition for the solution package. Let's include a JSON definition for the needed feature inside of the solution structure as demonstrated below.</span></span>

```json
{
  "solution": {
    "name": "command-extension-client-side-solution",
    "id": "dfffbe21-e422-4c0f-a302-d7d62a30c1bf",
    "version": "1.0.0.0",
    "features": [{
      "title": "ListView Command Set - Deployment of custom action.",
      "description": "Deploys a custom action with ClientSideComponentId association",
      "id": "456da147-ced2-3036-b564-8dad5c1c2e35",
      "version": "1.0.0.0",
      "assets": {        
        "elementManifests": [
          "elements.xml"
        ]
      }
    }]
  },
  "paths": {
    "zippedPackage": "solution/command-extension.sppkg"
  }
}
```

## <a name="deploy-the-extension-to-sharepoint-online-and-host-javascript-from-local-host"></a><span data-ttu-id="9e800-219">Bereitstellen der Erweiterung in SharePoint Online und Hosten des JavaScript-Codes über Localhost</span><span class="sxs-lookup"><span data-stu-id="9e800-219">Deploy the Extension to SharePoint Online and host JavaScript from local host</span></span>

<span data-ttu-id="9e800-220">Nun können Sie die Lösung auf einer SharePoint-Website bereitstellen und das Objekt *CustomAction* automatisch auf Website-Ebene verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="9e800-220">Now you are ready to deploy the solution to a SharePoint site and to have the *CustomAction* automatically associated on the site level.</span></span>

<span data-ttu-id="9e800-221">Geben Sie im Konsolenfenster den folgenden Befehl ein, um die clientseitige Lösung, die die Erweiterung enthält, zu verpacken und so die Grundstruktur für die Paketierung zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="9e800-221">In the console window, enter the following command to package your client-side solution that contains the extension, so that we get the basic structure ready for packaging:</span></span>

```
gulp bundle
```

<span data-ttu-id="9e800-222">Führen Sie als Nächstes den folgenden Befehl aus, um das Lösungspaket zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="9e800-222">Next, execute the following command so that the solution package is created:</span></span>

```
gulp package-solution
```

<span data-ttu-id="9e800-223">Der Befehl erstellt das Paket im Ordner **sharepoint/solution**:</span><span class="sxs-lookup"><span data-stu-id="9e800-223">The command will create the package in the **sharepoint/solution** folder:</span></span>

```
command-extension.sppkg
```

<span data-ttu-id="9e800-224">Als Nächstes müssen Sie das Paket, das generiert wurde, im App-Katalog bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="9e800-224">Next you need to deploy the package that was generated to the App Catalog.</span></span>

<span data-ttu-id="9e800-225">Wechseln Sie zum **App-Katalog** Ihres Mandanten, und öffnen Sie die Bibliothek **Apps für SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="9e800-225">Go to your tenant's **App Catalog** and open the **Apps for SharePoint** library.</span></span>

<span data-ttu-id="9e800-p124">Laden Sie das Paket `command-extension.sppkg` aus dem Ordner **sharepoint/solution** in den App-Katalog hoch, oder platzieren Sie es dort per Drag & Drop. SharePoint fordert Sie in einem Dialogfeld auf, der clientseitigen Lösung zu vertrauen.</span><span class="sxs-lookup"><span data-stu-id="9e800-p124">Upload or drag and drop the `command-extension.sppkg` located in the **sharepoint/solution** folder to the App Catalog. SharePoint will display a dialog and ask you to trust the client-side solution.</span></span>

<span data-ttu-id="9e800-p125">Da wir die Host-URLs der Lösung für diese Bereitstellung nicht aktualisiert haben, verweist die URL immer noch auf `https://localhost:4321`. Klicken Sie auf die Schaltfläche **Bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="9e800-p125">Notice that we did not update the URLs for hosting the solution for this deployment, so the URL is still pointing to `https://localhost:4321`. Click the **Deploy** button.</span></span>

![Bestätigen des Vertrauens beim Upload in den App-Katalog](../../../../images/ext-com-sppkg-deploy-trust.png)

<span data-ttu-id="9e800-p126">Wechseln Sie wieder zur Konsole, und vergewissern Sie sich, dass die Lösung ausgeführt wird. Sollte Sie nicht ausgeführt werden, führen Sie den folgenden Befehl im Lösungsordner aus:</span><span class="sxs-lookup"><span data-stu-id="9e800-p126">Move back to your console and ensure that the solution is running. If it's not running, execute the following command in the solution folder:</span></span>

```
gulp serve --nobrowser
```

<span data-ttu-id="9e800-p127">Wechseln Sie zu der Website, auf der Sie die Bereitstellung der SharePoint-Ressource testen möchten. Dies könnte eine Websitesammlung im Mandanten sein, auf dem Sie dieses Lösungspaket bereitgestellt haben.</span><span class="sxs-lookup"><span data-stu-id="9e800-p127">Go to the site where you want to test SharePoint asset provisioning. This could be any site collection in the tenant where you deployed this solution package.</span></span>

<span data-ttu-id="9e800-235">Klicken Sie auf der oberen Navigationsleiste rechts auf das Zahnradsymbol und anschließend auf **App hinzufügen**, um Ihre Apps-Seite aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="9e800-235">Chose the gear icon on the top navigation bar on the right and choose **Add an app** to go to your Apps page.</span></span>

<span data-ttu-id="9e800-236">Geben Sie in das **Suchfeld** die Zeichenfolge **command** ein, und drücken Sie die *EINGABETASTE*, um Ihre Apps zu filtern.</span><span class="sxs-lookup"><span data-stu-id="9e800-236">In the **Search** box, enter '**command**' and press *Enter* to filter your apps.</span></span>

![Installieren einer Erweiterung des Typs „ListView Command Set“ auf einer Website](../../../../images/ext-com-install-solution-to-site.png)

<span data-ttu-id="9e800-p128">Wählen Sie die App **command-extension-client-side-solution** aus, um die Lösung auf der Website zu installieren. Aktualisieren Sie die Seite nach Abschluss der Installation mithilfe der Taste **F5**.</span><span class="sxs-lookup"><span data-stu-id="9e800-p128">Choose the **command-extension-client-side-solution** app to install the solution on the site. When the installation is completed, refresh the page by pressing **F5**.</span></span>

<span data-ttu-id="9e800-240">Klicken Sie nach der Installation der Anwendung auf **Neu** auf der Symbolleiste auf der Seite **Websiteinhalte**, und wählen Sie die Option **Liste** aus.</span><span class="sxs-lookup"><span data-stu-id="9e800-240">When the application has been successfully installed, Click **New** from the toolbar on the **Site Contents** page and choose **List**</span></span>

![Erstellen einer neuen Liste](../../../../images/ext-field-create-new-list.png)

<span data-ttu-id="9e800-242">Geben Sie als Namen **Sample** ein, und klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="9e800-242">Provide the name as **Sample** and click **Create**.</span></span>

<span data-ttu-id="9e800-243">**Command One** und **Command Two** werden nun gemäß den Anpassungen in der Erweiterung des Typs „ListView Command Set“ auf der Symbolleiste gerendert.</span><span class="sxs-lookup"><span data-stu-id="9e800-243">Notice how **Command One** and **Command Two** are being rendered in the toolbar based on your ListView Command Set customizations.</span></span> 

![Symbolleiste mit zusätzlichen Schaltflächen](../../../../images/ext-com-dialog-visible-deployment.png)
