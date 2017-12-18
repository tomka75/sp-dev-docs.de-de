---
title: "Hinzufügen von jQueryUI Accordion zu Ihrem clientseitigen SharePoint-Webpart"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: fb93d06b47d54a2836c33f832440a054475e563d
ms.sourcegitcommit: 64ea77c00eea763edc4c524b678af9226d5aba35
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/31/2017
---
# <a name="add-jqueryui-accordion-to-your-sharepoint-client-side-web-part"></a><span data-ttu-id="99ab9-102">Hinzufügen von jQueryUI Accordion zu Ihrem clientseitigen SharePoint-Webpart</span><span class="sxs-lookup"><span data-stu-id="99ab9-102">Add jQueryUI Accordion to your SharePoint client-side web part</span></span>

<span data-ttu-id="99ab9-p101">In diesem Artikel wird beschrieben, wie das jQueryUI Accordion zu Ihrem Webpart-Projekt hinzugefügt wird. Dazu gehört das Erstellen eines neuen Webparts, wie in der folgenden Abbildung gezeigt.</span><span class="sxs-lookup"><span data-stu-id="99ab9-p101">This article describes how to add the jQueryUI Accordion to your web part project. This involves creating a new web part, as shown in the following image.</span></span> 

![Screenshot eines Webparts, das ein jQuery Accordion umfasst](../../../images/jquery-accordion-wb.png)

<span data-ttu-id="99ab9-106">Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=-3m__hRQxEI&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq) nachvollziehen:</span><span class="sxs-lookup"><span data-stu-id="99ab9-106">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=-3m__hRQxEI&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span></span> 

<a href="https://www.youtube.com/watch?v=-3m__hRQxEI&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq">
<img src="../../../images/spfx-youtube-tutorial5.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="prerequisites"></a><span data-ttu-id="99ab9-107">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="99ab9-107">Prerequisites</span></span>
<span data-ttu-id="99ab9-108">Führen Sie die folgenden Schritte aus, bevor Sie starten:</span><span class="sxs-lookup"><span data-stu-id="99ab9-108">Complete the following steps before you start:</span></span>

* [<span data-ttu-id="99ab9-109">Erstellen des ersten Webparts</span><span class="sxs-lookup"><span data-stu-id="99ab9-109">Build your first web part</span></span>](build-a-hello-world-web-part.md)
* [<span data-ttu-id="99ab9-110">Verbinden mit SharePoint</span><span class="sxs-lookup"><span data-stu-id="99ab9-110">Connect to SharePoint</span></span>](connect-to-sharepoint.md)

<span data-ttu-id="99ab9-p102">Die Entwicklertoolkette verwendet Webpack, SystemJS und CommonJS zum Bündeln der Webparts. Dies schließt das Laden externer Abhängigkeiten, z. B. jQuery oder jQueryUI, ein. Um externe Abhängigkeiten zu laden, müssen Sie folgende Schritte ausführen:</span><span class="sxs-lookup"><span data-stu-id="99ab9-p102">The developer toolchain uses Webpack, SystemJS and CommonJS to bundle your web parts. This includes loading any external dependencies such as jQuery or jQueryUI. To load external dependencies, at a high level, you will need to:</span></span>

* <span data-ttu-id="99ab9-114">Rufen Sie die externe Bibliothek über npm ab oder laden Sie sie vom Anbieter herunter.</span><span class="sxs-lookup"><span data-stu-id="99ab9-114">Acquire the external library, either via npm or download from the vendor.</span></span>
* <span data-ttu-id="99ab9-115">Falls verfügbar, installieren Sie die [TypeScript-Typdefinitionen](http://definitelytyped.org/) des entsprechenden Frameworks.</span><span class="sxs-lookup"><span data-stu-id="99ab9-115">If available, install the respective framework's [TypeScript type definitions](http://definitelytyped.org/).</span></span>
* <span data-ttu-id="99ab9-116">Aktualisieren Sie, falls erforderlich, die Lösungskonfiguration, um die externe Abhängigkeit nicht standardmäßig in das Webpartbundle einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="99ab9-116">If required, update your solution config to not include the external dependency in your web part bundle by default.</span></span>

## <a name="create-a-new-web-part-project"></a><span data-ttu-id="99ab9-117">Erstellen eines neuen Webpart-Projekts</span><span class="sxs-lookup"><span data-stu-id="99ab9-117">Create a new web part project</span></span>

<span data-ttu-id="99ab9-118">Erstellen Sie an einem Speicherort Ihrer Wahl ein neues Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="99ab9-118">Create a new project directory in your favorite location:</span></span>

```
md jquery-webpart
```
    
> <span data-ttu-id="99ab9-119">**Warnung:** Erstellen Sie dieses Verzeichnis unbedingt in einem neuen Ordner und nicht als Unterverzeichnis von `helloworld-webpart`.</span><span class="sxs-lookup"><span data-stu-id="99ab9-119">**Warning:** Make sure to create this directory in a new folder, not as a subdirectory of `helloworld-webpart`.</span></span>

<span data-ttu-id="99ab9-120">Wechseln Sie in das Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="99ab9-120">Go to the project directory:</span></span>

```
cd jquery-webpart
```
    
<span data-ttu-id="99ab9-121">Führen Sie den Yeoman-SharePoint-Generator aus, um ein neues jQuery-Webpart zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="99ab9-121">Create a new jQuery web part by running the Yeoman SharePoint Generator:</span></span>

```
yo @microsoft/sharepoint
```

<span data-ttu-id="99ab9-122">Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="99ab9-122">When prompted:</span></span>

* <span data-ttu-id="99ab9-123">Akzeptieren Sie den Standardnamen **jquery-webpart** als Lösungsnamen, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="99ab9-123">Accept the default **jquery-webpart** as your solution name and choose **Enter**.</span></span>
* <span data-ttu-id="99ab9-124">Wählen Sie **SharePoint Online only (latest)**, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="99ab9-124">Choose **SharePoint Online only (latest)**, and press **Enter**.</span></span>
* <span data-ttu-id="99ab9-125">Wählen Sie als Speicherort für die Dateien die Option **Use the current folder** aus.</span><span class="sxs-lookup"><span data-stu-id="99ab9-125">Select **Use the current folder** for where to place the files.</span></span>
* <span data-ttu-id="99ab9-126">Wählen Sie **N**, damit die Erweiterung auf jeder Website explizit installiert werden muss, wenn sie verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="99ab9-126">Choose **N** to require the extension to be installed on each site explicitly when it's being used.</span></span> 
* <span data-ttu-id="99ab9-127">Wählen Sie **Webpart** als den zu erstellenden Typ von clientseitiger Komponente aus.</span><span class="sxs-lookup"><span data-stu-id="99ab9-127">Choose **Webpart** as the client-side component type to be created.</span></span> 

<span data-ttu-id="99ab9-128">Über die nächsten Eingabeaufforderungen werden spezifische Informationen zum Webpart abgefragt:</span><span class="sxs-lookup"><span data-stu-id="99ab9-128">The next set of prompts will ask for specific information about your web part:</span></span>

* <span data-ttu-id="99ab9-129">Geben Sie **jQuery** als Webpartnamen ein, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="99ab9-129">Type **jQuery** for the web part name and choose **Enter**.</span></span>
* <span data-ttu-id="99ab9-130">Geben Sie**jQuery-Webpart** als Beschreibung des Webparts ein, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="99ab9-130">Enter **jQuery Web Part** as the description of the web part and choose **Enter**.</span></span> 
* <span data-ttu-id="99ab9-131">Akzeptieren Sie die Standardeinstellung **No JavaScript framework** als Framework, und drücken Sie die **EINGABETASTE**, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="99ab9-131">Accept the default **No JavaScipt web framework** option for the framework and choose **Enter** to continue.</span></span>

<span data-ttu-id="99ab9-p103">An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien. Das kann einige Minuten dauern. Yeoman erstellt ein Gerüst für das Projekt, um auch das **jQueryWebPart**-Webpart einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="99ab9-p103">At this point, Yeoman will install the required dependencies and scaffold the solution files. This might take a few minutes. Yeoman will scaffold the project to include your **jQueryWebPart** web part as well.</span></span>

<span data-ttu-id="99ab9-135">Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="99ab9-135">Once the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

```sh
npm shrinkwrap
```

<span data-ttu-id="99ab9-136">Geben Sie Folgendes ein, um das Webpart-Projekt in Visual Studio Code zu öffnen:</span><span class="sxs-lookup"><span data-stu-id="99ab9-136">In the console, type the following to open the web part project in Visual Studio Code:</span></span>

```
code .
```

## <a name="install-jquery-and-jquery-ui-npm-packages"></a><span data-ttu-id="99ab9-137">Installieren Sie die Pakete „jQuery“ und „jQueryUI NPM“.</span><span class="sxs-lookup"><span data-stu-id="99ab9-137">Install jQuery and jQuery UI NPM Packages</span></span>

<span data-ttu-id="99ab9-138">Geben Sie in der Konsole Folgendes ein, um das Paket „jQuery npm“ zu installieren:</span><span class="sxs-lookup"><span data-stu-id="99ab9-138">In the console, type the following to install jQuery npm package:</span></span>

```
npm install --save jquery@2
```

 <span data-ttu-id="99ab9-139">Geben Sie nun Folgendes ein, um das Paket „jQueryUI npm“ zu installieren:</span><span class="sxs-lookup"><span data-stu-id="99ab9-139">Now type the following to install jQueryUI npm package:</span></span>

```
npm install --save jqueryui
```

<span data-ttu-id="99ab9-p104">Als Nächstes müssen die Eingaben für unser Projekt installiert werden. Ab TypeScript 2.0 kann npm zum Installieren erforderlicher Eingaben verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="99ab9-p104">Next we'll need to install the typings for our project. Starting from TypeScript 2.0, we can use npm to install needed typings.</span></span>

<span data-ttu-id="99ab9-142">Öffnen Sie Ihre Konsole, und installieren Sie die erforderlichen Eingaben:</span><span class="sxs-lookup"><span data-stu-id="99ab9-142">Open your console and install needed types:</span></span>

```
npm install --save @types/jquery@2
npm install --save @types/jqueryui
```

### <a name="unbundle-external-dependencies-from-web-part-bundle"></a><span data-ttu-id="99ab9-143">Entfernen externer Abhängigkeiten aus dem Webpartbundle</span><span class="sxs-lookup"><span data-stu-id="99ab9-143">Unbundle external dependencies from web part bundle</span></span>
<span data-ttu-id="99ab9-p105">Standardmäßig werden hinzugefügte Abhängigkeiten im Webpartbundle gebündelt. In einigen Fällen ist dies nicht ideal. Sie können diese Abhängigkeiten aus dem Webpartbundle entfernen.</span><span class="sxs-lookup"><span data-stu-id="99ab9-p105">By default, any dependencies you add are bundled into the web part bundle. In some cases, this is not ideal. You can choose to unbundle these dependencies from the web part bundle.</span></span>

<span data-ttu-id="99ab9-147">Öffnen Sie in Visual Studio Code die Datei **config\config.json**.</span><span class="sxs-lookup"><span data-stu-id="99ab9-147">In Visual Studio Code, open the file config\config.json.</span></span>

<span data-ttu-id="99ab9-148">Diese Datei enthält Informationen zu Ihren Bundles und externen Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="99ab9-148">This file contains information about your bundle(s) and any external dependencies.</span></span> 

<span data-ttu-id="99ab9-p106">Der Bereich `bundles` enthält die Standardbundleinformationen - in diesem Fall jQuery-Webpartbundle. Wenn Sie Ihrer Lösung weitere Webparts hinzufügen, wird pro Webpart ein Eintrag angezeigt.</span><span class="sxs-lookup"><span data-stu-id="99ab9-p106">The `bundles` region contains the default bundle information - in this case, the jQuery web part bundle. When you add more web parts to your solution, you will see one entry per web part.</span></span>

```json
  "bundles": {
    "j-query-web-part": {
      "components": [
        {
          "entrypoint": "./lib/webparts/jQuery/JQueryWebPart.js",
          "manifest": "./src/webparts/jQuery/JQueryWebPart.manifest.json"
        }
      ]
    }
  },
```

<span data-ttu-id="99ab9-151">Der Bereich `externals` enthält die Bibliotheken, die nicht im Standardbundle gebündelt sind.</span><span class="sxs-lookup"><span data-stu-id="99ab9-151">You can use the `externals` section contains the libraries that are not bundled with the default bundle.</span></span> 

```json
  "externals": {},
```

<span data-ttu-id="99ab9-152">Um `jQuery` und `jQueryUI` aus dem Standardbundle zu entfernen, fügen Sie dem Bereich `externals` die Module hinzu:</span><span class="sxs-lookup"><span data-stu-id="99ab9-152">To exclude `jQuery` and `jQueryUI` from the default bundle, add the modules to the `externals` section:</span></span>

```json
"jquery":"node_modules/jquery/dist/jquery.min.js",
"jqueryui":"node_modules/jqueryui/jquery-ui.min.js"
```

<span data-ttu-id="99ab9-153">Wenn Sie nun Ihr Projekt erstellen, werden `jQuery` und `jQueryUI` nicht im standardmäßigen Webpartbundle gebündelt.</span><span class="sxs-lookup"><span data-stu-id="99ab9-153">Now when you build your project, `jQuery` and `jQueryUI` will not be bundled into your default web part bundle.</span></span>

<span data-ttu-id="99ab9-154">Der vollständige Inhalt der config.json-Datei ist derzeit wie folgt:</span><span class="sxs-lookup"><span data-stu-id="99ab9-154">Full content of the config.json file as currently as follows</span></span>

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx-build/config.2.0.schema.json",
  "version": "2.0",
  "bundles": {
    "j-query-web-part": {
      "components": [
        {
          "entrypoint": "./lib/webparts/jQuery/JQueryWebPart.js",
          "manifest": "./src/webparts/jQuery/JQueryWebPart.manifest.json"
        }
      ]
    }
  },
  "externals": {
    "jquery":"node_modules/jquery/dist/jquery.min.js",
    "jqueryui":"node_modules/jqueryui/jquery-ui.min.js"
  },
  "localizedResources": {
    "JQueryWebPartStrings": "lib/webparts/jQuery/loc/{locale}.js"
  }
}
```


## <a name="build-the-accordion"></a><span data-ttu-id="99ab9-155">Erstellen von Accordion</span><span class="sxs-lookup"><span data-stu-id="99ab9-155">Build the Accordion</span></span>

<span data-ttu-id="99ab9-156">Öffnen Sie den Projektordner **jquery-webpart** in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="99ab9-156">Open the project folder **jquery-webpart** in Visual Studio Code.</span></span> <span data-ttu-id="99ab9-157">Ihr Projekt sollte das jQuery-Webpart aufweisen, das Sie zuvor im Ordner `/src/webparts/jQuery` hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="99ab9-157">Open the project folder `/src/webparts/jQuery` in Visual Studio Code. Your project should have the jQuery web part that you added earlier under the /src/webparts/jQuery folder.</span></span>

### <a name="add-accordion-html"></a><span data-ttu-id="99ab9-158">Hinzufügen von Accordion-HTML</span><span class="sxs-lookup"><span data-stu-id="99ab9-158">Add Accordion HTML</span></span>
<span data-ttu-id="99ab9-159">Fügen Sie eine neue Datei im `src/webparts/jQuery`-Ordner namens **MyAccordionTemplate.ts** hinzu.</span><span class="sxs-lookup"><span data-stu-id="99ab9-159">Add a new file in the `src/webparts/jQuery` folder called **MyAccordionTemplate.ts**.</span></span>

<span data-ttu-id="99ab9-160">Erstellen und exportieren Sie eine Klasse `MyAccordionTemplate` (als Modul), die den HTML-Code für das Accordion enthält.</span><span class="sxs-lookup"><span data-stu-id="99ab9-160">Create and export (as a module) a class `MyAccordionTemplate` that holds the HTML code for the accordion.</span></span>

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

<span data-ttu-id="99ab9-161">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="99ab9-161">Save the file.</span></span>

### <a name="import-accordion-html"></a><span data-ttu-id="99ab9-162">Importieren von Accordion-HTML</span><span class="sxs-lookup"><span data-stu-id="99ab9-162">Import Accordion HTML</span></span>

<span data-ttu-id="99ab9-163">Öffnen Sie in Visual Studio Code **src\webparts\jQuery\JQueryWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="99ab9-163">In Visual Studio Code, open **src\webparts\jQuery\JQueryWebPart.ts**.</span></span>

<span data-ttu-id="99ab9-164">Fügen Sie am Anfang der Datei, wo sich auch andere Importe befinden, den folgenden Import hinzu:</span><span class="sxs-lookup"><span data-stu-id="99ab9-164">At the top of the file, where you can find other imports, add the following import:</span></span>

```ts
import MyAccordionTemplate from './MyAccordionTemplate';
```

### <a name="import-jquery-and-jqueryui"></a><span data-ttu-id="99ab9-165">Importieren von jQuery und jQueryUI</span><span class="sxs-lookup"><span data-stu-id="99ab9-165">Import jQuery and jQueryUI</span></span>
<span data-ttu-id="99ab9-166">Sie können jQuery auf die gleiche Weise in Ihr Webpart importieren, wie Sie „MyAccordionTemplate“ importiert haben.</span><span class="sxs-lookup"><span data-stu-id="99ab9-166">You can import jQuery your web part in the same way that you imported MyAccordionTemplate.</span></span>

<span data-ttu-id="99ab9-167">Fügen Sie am Anfang der Datei, wo sich auch andere Importe befinden, die folgenden Importe hinzu:</span><span class="sxs-lookup"><span data-stu-id="99ab9-167">At the top of the file, where you can find other imports, add the following imports:</span></span>

```ts
import * as jQuery from 'jquery';
import 'jqueryui';
```

<span data-ttu-id="99ab9-p108">Als Nächstes laden Sie einige externe CSS-Dateien. Verwenden Sie dazu das Modulladeprogramm. Fügen Sie den folgenden Import hinzu:</span><span class="sxs-lookup"><span data-stu-id="99ab9-p108">Next, you'll load some external css files. To do that, use the module loader. Add the following import:</span></span>

```ts
import { SPComponentLoader } from '@microsoft/sp-loader';
```

<span data-ttu-id="99ab9-p109">Um die jQueryUI-Formatvorlagen zu laden, müssen Sie in der `JQueryWebPart`-Webpartklasse einen Konstruktor hinzufügen und den neu importierten SPComponentLoader verwenden. Fügen Sie den folgenden Konstruktor zu Ihrem Webpart hinzu.</span><span class="sxs-lookup"><span data-stu-id="99ab9-p109">To load the jQueryUI styles, in the `JQueryWebPart` web part class, you'll need to add a constructor and use the newly imported SPComponentLoader. Add following constructor to your web part.</span></span> 

```ts
  public constructor() {
    super();

    SPComponentLoader.loadCss('//code.jquery.com/ui/1.11.4/themes/smoothness/jquery-ui.css');
  }
```

<span data-ttu-id="99ab9-173">Durch diesen Code wird Folgendes ausgeführt:</span><span class="sxs-lookup"><span data-stu-id="99ab9-173">This code does the following:</span></span>

* <span data-ttu-id="99ab9-174">Aufruf des übergeordneten Konstruktors mit dem Kontext zum Initialisieren des Webparts.</span><span class="sxs-lookup"><span data-stu-id="99ab9-174">Calls the parent constructor with the context to initialize the web part.</span></span>
* <span data-ttu-id="99ab9-175">Asynchrones Laden der Accordion-Formatvorlagen aus einem CDN.</span><span class="sxs-lookup"><span data-stu-id="99ab9-175">Loads the accordion styles from a CDN asynchronously.</span></span>

### <a name="render-accordion"></a><span data-ttu-id="99ab9-176">Rendern von Accordion</span><span class="sxs-lookup"><span data-stu-id="99ab9-176">Render Accordion</span></span>

<span data-ttu-id="99ab9-177">Wechseln Sie in der `jQueryWebPart.ts` zur `render`-Methode.</span><span class="sxs-lookup"><span data-stu-id="99ab9-177">In the `jQueryWebPart.ts`, go to the `render` method.</span></span>

<span data-ttu-id="99ab9-178">Legen Sie die innere HTML des Webparts so fest, dass die Accordion-HTML wiedergegeben wird:</span><span class="sxs-lookup"><span data-stu-id="99ab9-178">Set the web part's inner HTML to render the accordion HTML:</span></span>

```ts
this.domElement.innerHTML = MyAccordionTemplate.templateHtml;
```

<span data-ttu-id="99ab9-p110">jQueryUI Accordion weist einige Optionen auf, die Sie zum Anpassen des Accordions festlegen können. Definieren Sie einige Optionen für Ihr Accordion direkt unter `this.domElement.innerHTML = MyAccordionTemplate.templateHtml;`:</span><span class="sxs-lookup"><span data-stu-id="99ab9-p110">jQueryUI Accordion has few options that you can set to customize the accordion. Define a few options for your accordion just below `this.domElement.innerHTML = MyAccordionTemplate.templateHtml;`:</span></span>

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

<span data-ttu-id="99ab9-181">Wie Sie sehen können, können Sie über die TypeScript-Typdefinition eine Typvariable mit dem Namen `JQueryUI.AccordionOptions` und die unterstützten Eigenschaften angeben.</span><span class="sxs-lookup"><span data-stu-id="99ab9-181">As you can see, jQueryUI typed definition allows you to create a typed variable called `JQueryUI.AccordionOptions` and specify the supported properties.</span></span> 

<span data-ttu-id="99ab9-182">Wenn Sie mit IntelliSense experimentieren, werden Sie feststellen, dass Sie volle Unterstützung für in `JQueryUI.` verfügbare Methoden sowie die Methodenparameter erhalten.</span><span class="sxs-lookup"><span data-stu-id="99ab9-182">If you play around with the IntelliSense, you will notice you will get full support for available methods under `JQueryUI.` as well as the method parameters.</span></span>

<span data-ttu-id="99ab9-183">Initialisieren Sie schließlich das Accordion:</span><span class="sxs-lookup"><span data-stu-id="99ab9-183">Finally, initialize the accordion:</span></span>

```ts
jQuery('.accordion', this.domElement).accordion(accordionOptions);
```

<span data-ttu-id="99ab9-p111">Wie Sie sehen können, verwenden Sie die Variable `jQuery`, die Sie zum Importieren des `jquery`-Moduls verwendet haben. Initialisieren Sie dann das Accordion.</span><span class="sxs-lookup"><span data-stu-id="99ab9-p111">As you can see, you use the variable `jQuery` that you used to import the `jquery` module. You then initialize the accordion.</span></span>

<span data-ttu-id="99ab9-186">Die vollständige `render`-Methodenklasse sieht wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="99ab9-186">The complete `render` method looks like this:</span></span>

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

<span data-ttu-id="99ab9-187">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="99ab9-187">Save the file.</span></span>

## <a name="preview-the-web-part"></a><span data-ttu-id="99ab9-188">Anzeigen einer Webpart-Vorschau</span><span class="sxs-lookup"><span data-stu-id="99ab9-188">Preview the web part</span></span>

<span data-ttu-id="99ab9-189">Stellen Sie in der Konsole sicher, dass Sie sich immer noch im Ordner „jquery-webpart“ befinden, und geben Sie Folgendes ein, um das Webpart zu erstellen und in der Vorschau anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="99ab9-189">In your console, make sure you are still in the jquery-webpart folder and type the following to build and preview your web part:</span></span>

```
gulp serve
```

> [!NOTE]
> <span data-ttu-id="99ab9-190">Visual Studio Code bietet integrierte Unterstützung für gulp und andere Tools zur Taskausführung.</span><span class="sxs-lookup"><span data-stu-id="99ab9-190">Visual Studio Code provides built-in support for gulp and other task runners. Choose Ctrl+Shift+B on Windows or Cmd+Shift+B on Mac to debug and preview your web part.</span></span> <span data-ttu-id="99ab9-191">Sie können **STRG + UMSCHALT + B** unter Windows oder **BEFEHL + UMSCHALT + B** auf dem Mac drücken, um Ihr Webpart zu debuggen und eine Vorschau anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="99ab9-191">Note: Visual Studio Code provides built-in support for gulp and other task runners. You can choose **Ctrl+Shift+B** in Windows or **Cmd+Shift+B** on a Mac to debug and preview your web part.</span></span>

<span data-ttu-id="99ab9-192">Gulp führt die Aufgaben aus und öffnet die lokale SharePoint-Webpart Workbench.</span><span class="sxs-lookup"><span data-stu-id="99ab9-192">Gulp will execute the tasks and open the local SharePoint web part workbench.</span></span>

<span data-ttu-id="99ab9-p113">Drücken Sie im Seitenbereich auf das **+** (Pluszeichen), um die Liste von Webparts anzuzeigen, und führen Sie das jQuery-Webpart hinzu. Jetzt sollte das jQueryUI Accordion angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="99ab9-p113">In the page canvas, choose the **+** (plus sign) to show the list of web parts, and add the jQuery web part. You should now see the jQueryUI Accordion!</span></span>

![Screenshot eines Webparts, das ein jQuery Accordion umfasst](../../../images/jquery-accordion-wb.png)

<span data-ttu-id="99ab9-196">Drücken Sie in der Konsole, in der `gulp serve` ausgeführt wird, auf **STRG + C**, um die Aufgabe abzubrechen.</span><span class="sxs-lookup"><span data-stu-id="99ab9-196">In the console where you have `gulp serve` running, choose **Ctrl+C** to terminate the task.</span></span>
