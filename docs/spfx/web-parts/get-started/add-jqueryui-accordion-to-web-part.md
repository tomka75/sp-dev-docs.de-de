# <a name="add-jqueryui-accordion-to-your-sharepoint-client-side-web-part"></a><span data-ttu-id="bfc8b-101">Hinzufügen von jQueryUI Accordion zu Ihrem clientseitigen SharePoint-Webpart</span><span class="sxs-lookup"><span data-stu-id="bfc8b-101">Add jQueryUI Accordion to your SharePoint client-side web part</span></span>

<span data-ttu-id="bfc8b-p101">In diesem Artikel wird beschrieben, wie das jQueryUI Accordion zu Ihrem Webpart-Projekt hinzugefügt wird. Dazu gehört das Erstellen eines neuen Webparts, wie in der folgenden Abbildung gezeigt.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-p101">This article describes how to add the jQueryUI Accordion to your web part project. This involves creating a new web part, as shown in the following image.</span></span> 

![Screenshot eines Webparts, das ein jQuery Accordion umfasst](../../../../images/jquery-accordion-wb.png)

<span data-ttu-id="bfc8b-105">Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=-3m__hRQxEI&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq) nachvollziehen:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-105">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=-3m__hRQxEI&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span></span> 

<a href="https://www.youtube.com/watch?v=-3m__hRQxEI&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq">
<img src="../../../../images/spfx-youtube-tutorial5.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="prerequisites"></a><span data-ttu-id="bfc8b-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="bfc8b-106">Prerequisites</span></span>
<span data-ttu-id="bfc8b-107">Führen Sie die folgenden Schritte aus, bevor Sie starten:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-107">Complete the following steps before you start:</span></span>

* [<span data-ttu-id="bfc8b-108">Erstellen des ersten Webparts</span><span class="sxs-lookup"><span data-stu-id="bfc8b-108">Build your first web part</span></span>](build-a-hello-world-web-part.md)
* [<span data-ttu-id="bfc8b-109">Verbinden mit SharePoint</span><span class="sxs-lookup"><span data-stu-id="bfc8b-109">Connect to SharePoint</span></span>](connect-to-sharepoint.md)

<span data-ttu-id="bfc8b-p102">Die Entwicklertoolkette verwendet Webpack, SystemJS und CommonJS zum Bündeln der Webparts. Dies schließt das Laden externer Abhängigkeiten, z. B. jQuery oder jQueryUI, ein. Um externe Abhängigkeiten zu laden, müssen Sie folgende Schritte ausführen:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-p102">The developer toolchain uses Webpack, SystemJS and CommonJS to bundle your web parts. This includes loading any external dependencies such as jQuery or jQueryUI. To load external dependencies, at a high level, you will need to:</span></span>

* <span data-ttu-id="bfc8b-113">Rufen Sie die externe Bibliothek über npm ab oder laden Sie sie vom Anbieter herunter.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-113">Acquire the external library, either via npm or download from the vendor.</span></span>
* <span data-ttu-id="bfc8b-114">Falls verfügbar, installieren Sie die [TypeScript-Typdefinitionen](http://definitelytyped.org/) des entsprechenden Frameworks.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-114">If available, install the respective framework's [TypeScript type definitions](http://definitelytyped.org/).</span></span>
* <span data-ttu-id="bfc8b-115">Aktualisieren Sie, falls erforderlich, die Lösungskonfiguration, um die externe Abhängigkeit nicht standardmäßig in das Webpartbundle einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-115">If required, update your solution config to not include the external dependency in your web part bundle by default.</span></span>

## <a name="create-a-new-web-part-project"></a><span data-ttu-id="bfc8b-116">Erstellen eines neuen Webpart-Projekts</span><span class="sxs-lookup"><span data-stu-id="bfc8b-116">Create a new web part project</span></span>

<span data-ttu-id="bfc8b-117">Erstellen Sie an einem Speicherort Ihrer Wahl ein neues Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-117">Create a new project directory in your favorite location:</span></span>

```
md jquery-webpart
```
    
> <span data-ttu-id="bfc8b-118">**Warnung:** Erstellen Sie dieses Verzeichnis unbedingt in einem neuen Ordner und nicht als Unterverzeichnis von `helloworld-webpart`.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-118">**Warning:** Make sure to create this directory in a new folder, not as a subdirectory of `helloworld-webpart`.</span></span>

<span data-ttu-id="bfc8b-119">Wechseln Sie in das Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-119">Go to the project directory:</span></span>

```
cd jquery-webpart
```
    
<span data-ttu-id="bfc8b-120">Führen Sie den Yeoman-SharePoint-Generator aus, um ein neues jQuery-Webpart zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-120">Create a new jQuery web part by running the Yeoman SharePoint Generator:</span></span>

```
yo @microsoft/sharepoint
```

<span data-ttu-id="bfc8b-121">Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-121">When prompted:</span></span>

* <span data-ttu-id="bfc8b-122">Akzeptieren Sie den Standardnamen **jquery-webpart** als Lösungsnamen, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-122">Accept the default **jquery-webpart** as your solution name and choose **Enter**.</span></span>
* <span data-ttu-id="bfc8b-123">Wählen Sie **Aktuellen Ordner verwenden** als Speicherort für die Dateien aus.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-123">Select **Use the current folder** as the location for the files.</span></span>

<span data-ttu-id="bfc8b-124">Über die nächsten Eingabeaufforderungen werden spezifische Informationen zum Webpart abgefragt:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-124">The next set of prompts will ask for specific information about your web part:</span></span>

* <span data-ttu-id="bfc8b-125">Akzeptieren Sie die Standardeinstellung **No javascript web framework** als Framework, und drücken Sie die **EINGABETASTE**, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-125">Accept the default No **javascript web framework** option for the framework and choose **Enter** to continue.</span></span>
* <span data-ttu-id="bfc8b-126">Geben Sie **jQuery** als Webpartnamen ein, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-126">Type **jQuery** for the web part name and choose **Enter**.</span></span>
* <span data-ttu-id="bfc8b-127">Geben Sie**jQuery-Webpart** als Beschreibung des Webparts ein, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-127">Enter **jQuery Web Part** as the description of the web part and choose **Enter**.</span></span> 

<span data-ttu-id="bfc8b-p103">An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien. Das kann einige Minuten dauern. Yeoman erstellt ein Gerüst für das Projekt, um auch das **jQueryWebPart**-Webpart einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-p103">At this point, Yeoman will install the required dependencies and scaffold the solution files. This might take a few minutes. Yeoman will scaffold the project to include your **jQueryWebPart** web part as well.</span></span>

<span data-ttu-id="bfc8b-131">Geben Sie in der Konsole Folgendes ein, um das Webpart-Projekt in Visual Studio-Code zu öffnen:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-131">In the console, type the following to open the web part project in Visual Studio Code:</span></span>

```
code .
```

## <a name="install-jquery-and-jquery-ui-npm-packages"></a><span data-ttu-id="bfc8b-132">Installieren Sie die Pakete „jQuery“ und „jQueryUI NPM“.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-132">Install jQuery and jQuery UI NPM Packages</span></span>

<span data-ttu-id="bfc8b-133">Geben Sie in der Konsole Folgendes ein, um das Paket „jQuery npm“ zu installieren:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-133">In the console, type the following to install jQuery npm package:</span></span>

```
npm install --save jquery@2
```

 <span data-ttu-id="bfc8b-134">Geben Sie nun Folgendes ein, um das Paket „jQueryUI npm“ zu installieren:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-134">Now type the following to install jQueryUI npm package:</span></span>

```
npm install --save jqueryui
```

<span data-ttu-id="bfc8b-p104">Als Nächstes müssen die Eingaben für unser Projekt installiert werden. Ab TypeScript 2.0 kann npm zum Installieren erforderlicher Eingaben verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-p104">Next we'll need to install the typings for our project. Starting from TypeScript 2.0, we can use npm to install needed typings.</span></span>

<span data-ttu-id="bfc8b-137">Öffnen Sie Ihre Konsole, und installieren Sie die erforderlichen Eingaben:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-137">Open your console and install needed types:</span></span>

```
npm install --save @types/jquery@2
npm install --save @types/jqueryui
```

### <a name="unbundle-external-dependencies-from-web-part-bundle"></a><span data-ttu-id="bfc8b-138">Entfernen externer Abhängigkeiten aus dem Webpartbundle</span><span class="sxs-lookup"><span data-stu-id="bfc8b-138">Unbundle external dependencies from web part bundle</span></span>
<span data-ttu-id="bfc8b-p105">Standardmäßig werden hinzugefügte Abhängigkeiten im Webpartbundle gebündelt. In einigen Fällen ist dies nicht ideal. Sie können diese Abhängigkeiten aus dem Webpartbundle entfernen.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-p105">By default, any dependencies you add are bundled into the web part bundle. In some cases, this is not ideal. You can choose to unbundle these dependencies from the web part bundle.</span></span>

<span data-ttu-id="bfc8b-142">Öffnen Sie in Visual Studio Code die Datei „config\config.json“.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-142">In Visual Studio Code, open the file config\config.json.</span></span>

<span data-ttu-id="bfc8b-143">Diese Datei enthält Informationen zu Ihren Bundles und externen Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-143">This file contains information about your bundle(s) and any external dependencies.</span></span> 

<span data-ttu-id="bfc8b-p106">Der Bereich `entries` enthält die Standardbundleinformationen - in diesem Fall jQuery-Webpartbundle. Wenn Sie Ihrer Lösung weitere Webparts hinzufügen, wird pro Webpart ein Eintrag angezeigt.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-p106">The `entries` region contains the default bundle information - in this case, the jQuery web part bundle. When you add more web parts to your solution, you will see one entry per web part.</span></span>

```json
"entries": [
  {
    "entry": "./lib/webparts/jQuery/jQueryWebPart.js",
    "manifest": "./src/webparts/jQuery/jQueryWebPart.manifest.json",
    "outputPath": "./dist/j-query.bundle.js",
  }
]
```

<span data-ttu-id="bfc8b-146">Der Bereich `externals` enthält die Bibliotheken, die nicht im Standardbundle gebündelt sind.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-146">You can use the `externals` section contains the libraries that are not bundled with the default bundle.</span></span> 

```json
  "externals": {},
```

<span data-ttu-id="bfc8b-147">Um `jQuery` und `jQueryUI` aus dem Standardbundle zu entfernen, fügen Sie dem Bereich `externals` die Module hinzu:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-147">To exclude `jQuery` and `jQueryUI` from the default bundle, add the modules to the `externals` section:</span></span>

```json
"jquery":"node_modules/jquery/dist/jquery.min.js",
"jqueryui":"node_modules/jqueryui/jquery-ui.min.js"
```

<span data-ttu-id="bfc8b-148">Wenn Sie nun Ihr Projekt erstellen, werden `jQuery` und `jQueryUI` nicht im standardmäßigen Webpartbundle gebündelt.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-148">Now when you build your project, `jQuery` and `jQueryUI` will not be bundled into your default web part bundle.</span></span>

<span data-ttu-id="bfc8b-149">Der vollständige Inhalt der config.json-Datei ist derzeit wie folgt:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-149">Full content of the config.json file as currently as follows</span></span>

```json
{
  "entries": [
    {
      "entry": "./lib/webparts/jQuery/JQueryWebPart.js",
      "manifest": "./src/webparts/jQuery/JQueryWebPart.manifest.json",
      "outputPath": "./dist/j-query.bundle.js"
    }
  ],
  "externals": {
    "jquery":"node_modules/jquery/dist/jquery.min.js",
    "jqueryui":"node_modules/jqueryui/jquery-ui.min.js"
  },
  "localizedResources": {
    "jQueryStrings": "webparts/jQuery/loc/{locale}.js"
  }
}
```


## <a name="build-the-accordion"></a><span data-ttu-id="bfc8b-150">Erstellen von Accordion</span><span class="sxs-lookup"><span data-stu-id="bfc8b-150">Build the Accordion</span></span>

<span data-ttu-id="bfc8b-p107">Öffnen Sie den Projektordner **jquery-webpart** in Visual Studio Code. Ihr Projekt sollte das jQuery-Webpart aufweisen, das Sie zuvor im Ordner „/src/webparts/jQuery“ hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-p107">Open the project folder **jquery-webpart** in Visual Studio Code. Your project should have the jQuery web part that you added earlier under the /src/webparts/jQuery folder.</span></span>

### <a name="add-accordion-html"></a><span data-ttu-id="bfc8b-153">Hinzufügen von Accordion-HTML</span><span class="sxs-lookup"><span data-stu-id="bfc8b-153">Add Accordion HTML</span></span>
<span data-ttu-id="bfc8b-154">Fügen Sie eine neue Datei im `src/webparts/jQuery`-Ordner namens **MyAccordionTemplate.ts** hinzu.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-154">Add a new file in the `src/webparts/jQuery` folder called **MyAccordionTemplate.ts**.</span></span>

<span data-ttu-id="bfc8b-155">Erstellen und exportieren Sie eine Klasse `MyAccordionTemplate` (als Modul), die den HTML-Code für das Accordion enthält.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-155">Create and export (as a module) a class `MyAccordionTemplate` that holds the HTML code for the accordion.</span></span>

```ts
export default class MyAccordionTemplate {
    public static templateHtml: string =  `
      <div class="accordion">
        <h3>Section 1</h3>
        <div>
            <p>
            Mauris mauris ante, blandit et, ultrices a, suscipit eget, quam. Integer
            ut neque. Vivamus nisi metus, molestie vel, gravida in, condimentum sit
            amet, nunc. Nam a nibh. Donec suscipit eros. Nam mi. Proin viverra leo ut
            odio. Curabitur malesuada. Vestibulum a velit eu ante scelerisque vulputate.
            </p>
        </div>
        <h3>Section 2</h3>
        <div>
            <p>
            Sed non urna. Donec et ante. Phasellus eu ligula. Vestibulum sit amet
            purus. Vivamus hendrerit, dolor at aliquet laoreet, mauris turpis porttitor
            velit, faucibus interdum tellus libero ac justo. Vivamus non quam. In
            suscipit faucibus urna.
            </p>
        </div>
        <h3>Section 3</h3>
        <div>
            <p>
            Nam enim risus, molestie et, porta ac, aliquam ac, risus. Quisque lobortis.
            Phasellus pellentesque purus in massa. Aenean in pede. Phasellus ac libero
            ac tellus pellentesque semper. Sed ac felis. Sed commodo, magna quis
            lacinia ornare, quam ante aliquam nisi, eu iaculis leo purus venenatis dui.
            </p>
            <ul>
            <li>List item one</li>
            <li>List item two</li>
            <li>List item three</li>
            </ul>
        </div>
        <h3>Section 4</h3>
        <div>
            <p>
            Cras dictum. Pellentesque habitant morbi tristique senectus et netus
            et malesuada fames ac turpis egestas. Vestibulum ante ipsum primis in
            faucibus orci luctus et ultrices posuere cubilia Curae; Aenean lacinia
            mauris vel est.
            </p>
            <p>
            Suspendisse eu nisl. Nullam ut libero. Integer dignissim consequat lectus.
            Class aptent taciti sociosqu ad litora torquent per conubia nostra, per
            inceptos himenaeos.
            </p>
        </div>
     </div>`;
}
```

<span data-ttu-id="bfc8b-156">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-156">Save the file.</span></span>

### <a name="import-accordion-html"></a><span data-ttu-id="bfc8b-157">Importieren von Accordion-HTML</span><span class="sxs-lookup"><span data-stu-id="bfc8b-157">Import Accordion HTML</span></span>

<span data-ttu-id="bfc8b-158">Öffnen Sie in Visual Studio Code **src\webparts\jQuery\JQueryWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-158">In Visual Studio Code, open **src\webparts\jQuery\JQueryWebPart.ts**.</span></span>

<span data-ttu-id="bfc8b-159">Fügen Sie am Anfang der Datei, wo sich auch andere Importe befinden, den folgenden Import hinzu:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-159">At the top of the file, where you can find other imports, add the following import:</span></span>

```ts
import MyAccordionTemplate from './MyAccordionTemplate';
```

### <a name="import-jquery-and-jqueryui"></a><span data-ttu-id="bfc8b-160">Importieren von jQuery und jQueryUI</span><span class="sxs-lookup"><span data-stu-id="bfc8b-160">Import jQuery and jQueryUI</span></span>
<span data-ttu-id="bfc8b-161">Sie können jQuery auf die gleiche Weise in Ihr Webpart importieren, wie Sie „MyAccordionTemplate“ importiert haben.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-161">You can import jQuery your web part in the same way that you imported MyAccordionTemplate.</span></span>

<span data-ttu-id="bfc8b-162">Fügen Sie am Anfang der Datei, wo sich auch andere Importe befinden, die folgenden Importe hinzu:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-162">At the top of the file, where you can find other imports, add the following imports:</span></span>

```ts
import * as jQuery from 'jquery';
import 'jqueryui';
```

<span data-ttu-id="bfc8b-p108">Als Nächstes laden Sie einige externe CSS-Dateien. Verwenden Sie dazu das Modulladeprogramm. Fügen Sie den folgenden Import hinzu:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-p108">Next, you'll load some external css files. To do that, use the module loader. Add the following import:</span></span>

```ts
import { SPComponentLoader } from '@microsoft/sp-loader';
```

<span data-ttu-id="bfc8b-p109">Um die jQueryUI-Formatvorlagen zu laden, müssen Sie in der `JQueryWebPart`-Webpartklasse einen Konstruktor hinzufügen und den neu importierten SPComponentLoader verwenden. Fügen Sie den folgenden Konstruktor zu Ihrem Webpart hinzu.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-p109">To load the jQueryUI styles, in the `JQueryWebPart` web part class, you'll need to add a constructor and use the newly imported SPComponentLoader. Add following constructor to your web part.</span></span> 

```ts
  public constructor() {
    super();

    SPComponentLoader.loadCss('//code.jquery.com/ui/1.11.4/themes/smoothness/jquery-ui.css');
  }
```

<span data-ttu-id="bfc8b-168">Durch diesen Code wird Folgendes ausgeführt:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-168">This code does the following:</span></span>

* <span data-ttu-id="bfc8b-169">Aufruf des übergeordneten Konstruktors mit dem Kontext zum Initialisieren des Webparts.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-169">Calls the parent constructor with the context to initialize the web part.</span></span>
* <span data-ttu-id="bfc8b-170">Asynchrones Laden der Accordion-Formatvorlagen aus einem CDN.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-170">Loads the accordion styles from a CDN asynchronously.</span></span>

### <a name="render-accordion"></a><span data-ttu-id="bfc8b-171">Rendern von Accordion</span><span class="sxs-lookup"><span data-stu-id="bfc8b-171">Render Accordion</span></span>

<span data-ttu-id="bfc8b-172">Wechseln Sie in der `jQueryWebPart.ts` zur `render`-Methode.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-172">In the `jQueryWebPart.ts`, go to the `render` method.</span></span>

<span data-ttu-id="bfc8b-173">Legen Sie die innere HTML des Webparts so fest, dass die Accordion-HTML wiedergegeben wird:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-173">Set the web part's inner HTML to render the accordion HTML:</span></span>

```ts
this.domElement.innerHTML = MyAccordionTemplate.templateHtml;
```

<span data-ttu-id="bfc8b-p110">jQueryUI Accordion weist einige Optionen auf, die Sie zum Anpassen des Accordions festlegen können. Definieren Sie einige Optionen für Ihr Accordion direkt unter `this.domElement.innerHTML = MyAccordionTemplate.templateHtml;`:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-p110">jQueryUI Accordion has few options that you can set to customize the accordion. Define a few options for your accordion just below `this.domElement.innerHTML = MyAccordionTemplate.templateHtml;`:</span></span>

```ts
const accordionOptions: JQueryUI.AccordionOptions = {
  animate: true,
  collapsible: false,
  icons: {
    header: 'ui-icon-circle-arrow-e',
    activeHeader: 'ui-icon-circle-arrow-s'
  }
};
```

<span data-ttu-id="bfc8b-176">Wie Sie sehen können, können Sie über die TypeScript-Typdefinition eine Typvariable mit dem Namen `JQueryUI.AccordionOptions` und die unterstützten Eigenschaften angeben.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-176">As you can see, jQueryUI typed definition allows you to create a typed variable called `JQueryUI.AccordionOptions` and specify the supported properties.</span></span> 

<span data-ttu-id="bfc8b-177">Wenn Sie mit IntelliSense experimentieren, werden Sie feststellen, dass Sie volle Unterstützung für in `JQueryUI.` verfügbare Methoden sowie die Methodenparameter erhalten.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-177">If you play around with the IntelliSense, you will notice you will get full support for available methods under `JQueryUI.` as well as the method parameters.</span></span>

<span data-ttu-id="bfc8b-178">Initialisieren Sie schließlich das Accordion:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-178">Finally, initialize the accordion:</span></span>

```ts
jQuery('.accordion', this.domElement).accordion(accordionOptions);
```

<span data-ttu-id="bfc8b-p111">Wie Sie sehen können, verwenden Sie die Variable `jQuery`, die Sie zum Importieren des `jquery`-Moduls verwendet haben. Initialisieren Sie dann das Accordion.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-p111">As you can see, you use the variable `jQuery` that you used to import the `jquery` module. You then initialize the accordion.</span></span>

<span data-ttu-id="bfc8b-181">Die vollständige `render`-Methodenklasse sieht wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-181">The complete `render` method looks like this:</span></span>

```ts
public render(): void {
  this.domElement.innerHTML = MyAccordionTemplate.templateHtml;

  const accordionOptions: JQueryUI.AccordionOptions = {
    animate: true,
    collapsible: false,
    icons: {
      header: 'ui-icon-circle-arrow-e',
      activeHeader: 'ui-icon-circle-arrow-s'
    }
  };

  jQuery('.accordion', this.domElement).accordion(accordionOptions);
}
```

<span data-ttu-id="bfc8b-182">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-182">Save the file.</span></span>

## <a name="preview-the-web-part"></a><span data-ttu-id="bfc8b-183">Anzeigen einer Webpart-Vorschau</span><span class="sxs-lookup"><span data-stu-id="bfc8b-183">Preview the web part</span></span>

<span data-ttu-id="bfc8b-184">Stellen Sie in der Konsole sicher, dass Sie sich immer noch im Ordner „jquery-webpart“ befinden, und geben Sie Folgendes ein, um das Webpart zu erstellen und in der Vorschau anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="bfc8b-184">In your console, make sure you are still in the jquery-webpart folder and type the following to build and preview your web part:</span></span>

```
gulp serve
```

> <span data-ttu-id="bfc8b-p112">**Hinweis:** Visual Studio Code bietet integrierte Unterstützung für gulp und andere Tools zur Taskausführung. Sie können STRG + UMSCHALT + B unter Windows oder **BEFEHL + UMSCHALT + B** auf dem Mac drücken, um Ihr Webpart zu debuggen und eine Vorschau anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-p112">**Note:** Visual Studio Code provides built-in support for gulp and other task runners. You can choose **Ctrl+Shift+B** in Windows or **Cmd+Shift+B** on a Mac to debug and preview your web part.</span></span>

<span data-ttu-id="bfc8b-187">Gulp führt die Aufgaben aus und öffnet die lokale SharePoint-Webpart Workbench.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-187">Gulp will execute the tasks and open the local SharePoint web part workbench.</span></span>

<span data-ttu-id="bfc8b-p113">Drücken Sie im Seitenbereich auf das **+** (Pluszeichen), um die Liste von Webparts anzuzeigen, und führen Sie das jQuery-Webpart hinzu. Jetzt sollte das jQueryUI Accordion angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-p113">In the page canvas, choose the **+** (plus sign) to show the list of web parts, and add the jQuery web part. You should now see the jQueryUI Accordion!</span></span>

![Screenshot eines Webparts, das ein jQuery Accordion umfasst](../../../../images/jquery-accordion-wb.png)

<span data-ttu-id="bfc8b-191">Drücken Sie in der Konsole, in der `gulp serve` ausgeführt wird, auf **STRG + C**, um die Aufgabe abzubrechen.</span><span class="sxs-lookup"><span data-stu-id="bfc8b-191">In the console where you have `gulp serve` running, choose **Ctrl+C** to terminate the task.</span></span>
