---
title: "Hinzufügen von jQueryUI Accordion zu Ihrem clientseitigen SharePoint-Webpart"
description: "Wenn Sie jQueryUI Accordion zu Ihrem Webpartprojekt hinzufügen möchten, müssen Sie ein neues Webpart erstellen."
ms.date: 01/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 3c692687133db378dd23842d1ef28ad202e733eb
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/05/2018
---
# <a name="add-jqueryui-accordion-to-your-sharepoint-client-side-web-part"></a><span data-ttu-id="db3e9-103">Hinzufügen von jQueryUI Accordion zu Ihrem clientseitigen SharePoint-Webpart</span><span class="sxs-lookup"><span data-stu-id="db3e9-103">Add jQueryUI Accordion to your SharePoint client-side web part</span></span>

<span data-ttu-id="db3e9-104">Wenn Sie jQueryUI Accordion zu Ihrem Webpartprojekt hinzufügen möchten, müssen Sie ein neues Webpart erstellen, wie im folgenden Bild dargestellt.</span><span class="sxs-lookup"><span data-stu-id="db3e9-104">Adding the jQueryUI Accordion to your web part project involves creating a new web part, as shown in the following image.</span></span> 

![Screenshot eines Webparts, das ein jQuery Accordion umfasst](../../../images/jquery-accordion-wb.png)

<span data-ttu-id="db3e9-106">Stellen Sie sicher, dass Sie die folgenden Schritte ausgeführt haben, bevor Sie starten:</span><span class="sxs-lookup"><span data-stu-id="db3e9-106">Ensure that you've completed the following steps before you start:</span></span>

* [<span data-ttu-id="db3e9-107">Erstellen des ersten Webparts</span><span class="sxs-lookup"><span data-stu-id="db3e9-107">Build your first web part</span></span>](build-a-hello-world-web-part.md)
* [<span data-ttu-id="db3e9-108">Verbinden des Webparts mit SharePoint</span><span class="sxs-lookup"><span data-stu-id="db3e9-108">Connect your web part to SharePoint</span></span>](connect-to-sharepoint.md)

<span data-ttu-id="db3e9-109">Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=7UOxTbMMPrQ&index=6&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq) nachvollziehen.</span><span class="sxs-lookup"><span data-stu-id="db3e9-109">You can also follow these steps by watching this video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=7UOxTbMMPrQ&index=6&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span></span> 

<a href="https://www.youtube.com/watch?v=7UOxTbMMPrQ&index=6&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq">
<img src="../../../images/spfx-youtube-tutorial5.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

<span data-ttu-id="db3e9-110">Die Entwicklertoolkette verwendet Webpack, SystemJS und CommonJS zum Bündeln der Webparts.</span><span class="sxs-lookup"><span data-stu-id="db3e9-110">The developer toolchain uses Webpack, SystemJS, and CommonJS to bundle your web parts.</span></span> <span data-ttu-id="db3e9-111">Dies schließt das Laden externer Abhängigkeiten, z. B. jQuery oder jQueryUI, ein.</span><span class="sxs-lookup"><span data-stu-id="db3e9-111">This includes loading any external dependencies such as jQuery or jQueryUI.</span></span> <span data-ttu-id="db3e9-112">Um externe Abhängigkeiten zu laden, müssen Sie folgende Schritte ausführen:</span><span class="sxs-lookup"><span data-stu-id="db3e9-112">To load external dependencies, at a high level, you need to:</span></span>

* <span data-ttu-id="db3e9-113">Rufen Sie die externe Bibliothek über npm ab, oder laden Sie sie vom Anbieter herunter.</span><span class="sxs-lookup"><span data-stu-id="db3e9-113">Acquire the external library, either via npm or download from the vendor.</span></span>
* <span data-ttu-id="db3e9-114">Falls verfügbar, installieren Sie die [TypeScript-Typdefinitionen](http://definitelytyped.org/) des entsprechenden Frameworks.</span><span class="sxs-lookup"><span data-stu-id="db3e9-114">If available, install the respective framework's [TypeScript type definitions](http://definitelytyped.org/).</span></span>
* <span data-ttu-id="db3e9-115">Aktualisieren Sie, falls erforderlich, die Lösungskonfiguration, um die externe Abhängigkeit nicht standardmäßig in das Webpartbundle einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="db3e9-115">If required, update your solution config to not include the external dependency in your web part bundle by default.</span></span>

## <a name="create-a-new-web-part-project"></a><span data-ttu-id="db3e9-116">Erstellen eines neuen Webpart-Projekts</span><span class="sxs-lookup"><span data-stu-id="db3e9-116">Create a new web part project</span></span>

1. <span data-ttu-id="db3e9-117">Erstellen Sie an einem Speicherort Ihrer Wahl ein neues Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="db3e9-117">Create a new project directory in your favorite location:</span></span>

  ```
  md jquery-webpart
  ```
      
  > [!WARNING] 
  > <span data-ttu-id="db3e9-118">Erstellen Sie dieses Verzeichnis unbedingt in einem neuen Ordner und nicht als Unterverzeichnis von `helloworld-webpart`.</span><span class="sxs-lookup"><span data-stu-id="db3e9-118">Make sure to create this directory in a new folder, not as a subdirectory of `helloworld-webpart`.</span></span>

2. <span data-ttu-id="db3e9-119">Wechseln Sie in das Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="db3e9-119">Go to the project directory:</span></span>

  ```
  cd jquery-webpart
  ```
    
3. <span data-ttu-id="db3e9-120">Führen Sie den Yeoman-SharePoint-Generator aus, um ein neues jQuery-Webpart zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="db3e9-120">Create a new jQuery web part by running the Yeoman SharePoint Generator:</span></span>

  ```
  yo @microsoft/sharepoint
  ```

4. <span data-ttu-id="db3e9-121">Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="db3e9-121">When prompted:</span></span>

  * <span data-ttu-id="db3e9-122">Akzeptieren Sie den Standardnamen **jquery-webpart** als Lösungsnamen.</span><span class="sxs-lookup"><span data-stu-id="db3e9-122">Accept the default **jquery-webpart** as your solution name.</span></span> <span data-ttu-id="db3e9-123">Drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="db3e9-123">and select Enter.</span></span>
  * <span data-ttu-id="db3e9-124">Wählen Sie **SharePoint Online only (latest)**, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="db3e9-124">Select **SharePoint Online only (latest)**, and select Enter.</span></span>
  * <span data-ttu-id="db3e9-125">Wählen Sie die Option **Use the current folder** als Speicherort für die Dateien aus.</span><span class="sxs-lookup"><span data-stu-id="db3e9-125">Select **Use the current folder** for where to place the files.</span></span>
  * <span data-ttu-id="db3e9-126">Wählen Sie **N**, damit die Erweiterung auf jeder Website explizit installiert werden muss, wenn sie verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="db3e9-126">Select **N** to require the extension to be installed on each site explicitly when it's being used.</span></span> 
  * <span data-ttu-id="db3e9-127">Wählen Sie **Webpart** als den zu erstellenden Typ von clientseitiger Komponente aus.</span><span class="sxs-lookup"><span data-stu-id="db3e9-127">Select **WebPart** as the client-side component type to be created.</span></span> 

5. <span data-ttu-id="db3e9-128">Über die nächsten Eingabeaufforderungen werden spezifische Informationen zum Webpart abgefragt:</span><span class="sxs-lookup"><span data-stu-id="db3e9-128">The next set of prompts ask for specific information about your web part:</span></span>

  * <span data-ttu-id="db3e9-129">Geben Sie **jQuery** als Webpartnamen ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="db3e9-129">Enter **jQuery** for the web part name, and select Enter.</span></span>
  * <span data-ttu-id="db3e9-130">Geben Sie **jQuery-Webpart** als Beschreibung des Webparts ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="db3e9-130">Enter **jQuery Web Part** as the description of the web part, and select Enter.</span></span> 
  * <span data-ttu-id="db3e9-131">Akzeptieren Sie die Standardeinstellung **No JavaScript framework** als Framework, und drücken Sie die EINGABETASTE, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="db3e9-131">Accept the default **No JavaScript framework** option for the framework, and select Enter to continue.</span></span>

  <span data-ttu-id="db3e9-p103">An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien. Dies kann einige Minuten dauern. Yeoman erstellt ein Gerüst für das Projekt, um auch das **jQueryWebPart** einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="db3e9-p103">At this point, Yeoman installs the required dependencies and scaffolds the solution files. This might take a few minutes. Yeoman scaffolds the project to include your **jQueryWebPart** as well.</span></span>

6. <span data-ttu-id="db3e9-135">Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="db3e9-135">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

  ```sh
  npm shrinkwrap
  ```

7. <span data-ttu-id="db3e9-136">Geben Sie Folgendes ein, um das Webpart-Projekt in Visual Studio Code zu öffnen:</span><span class="sxs-lookup"><span data-stu-id="db3e9-136">Enter the following to open the web part project in Visual Studio Code:</span></span>

  ```
  code .
  ```


## <a name="install-jquery-and-jquery-ui-npm-packages"></a><span data-ttu-id="db3e9-137">Installieren Sie die Pakete „jQuery“ und „jQueryUI NPM“.</span><span class="sxs-lookup"><span data-stu-id="db3e9-137">Install jQuery and jQuery UI NPM Packages</span></span>

1. <span data-ttu-id="db3e9-138">Geben Sie in der Konsole Folgendes ein, um das Paket „jQuery npm“ zu installieren:</span><span class="sxs-lookup"><span data-stu-id="db3e9-138">In the console, enter the following to install the jQuery npm package:</span></span>

  ```
  npm install --save jquery@2
  ```

2. <span data-ttu-id="db3e9-139">Geben Sie nun Folgendes ein, um das Paket „jQuery npm“ zu installieren:</span><span class="sxs-lookup"><span data-stu-id="db3e9-139">Now enter the following to install the jQueryUI npm package:</span></span>

  ```
  npm install --save jqueryui
  ```

  <span data-ttu-id="db3e9-p104">Als Nächstes müssen die Eingaben für unser Projekt installiert werden. Ab TypeScript 2.0 kann npm zum Installieren erforderlicher Eingaben verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="db3e9-p104">Next, we need to install the typings for our project. Starting from TypeScript 2.0, we can use npm to install needed typings.</span></span>

3. <span data-ttu-id="db3e9-142">Öffnen Sie Ihre Konsole, und installieren Sie die erforderlichen Eingaben:</span><span class="sxs-lookup"><span data-stu-id="db3e9-142">Open your console and install the needed types:</span></span>

  ```
  npm install --save @types/jquery@2
  npm install --save @types/jqueryui
  ```

### <a name="to-unbundle-external-dependencies-from-web-part-bundle"></a><span data-ttu-id="db3e9-143">So entfernen Sie externe Abhängigkeiten aus dem Webpartbundle</span><span class="sxs-lookup"><span data-stu-id="db3e9-143">To unbundle external dependencies from web part bundle</span></span>

<span data-ttu-id="db3e9-p105">Standardmäßig werden hinzugefügte Abhängigkeiten im Webpartbundle gebündelt. In einigen Fällen ist dies nicht ideal. Sie können diese Abhängigkeiten aus dem Webpartbundle entfernen.</span><span class="sxs-lookup"><span data-stu-id="db3e9-p105">By default, any dependencies you add are bundled into the web part bundle. In some cases, this is not ideal. You can choose to unbundle these dependencies from the web part bundle.</span></span>

1. <span data-ttu-id="db3e9-147">Öffnen Sie in Visual Studio Code die Datei **config\config.json**.</span><span class="sxs-lookup"><span data-stu-id="db3e9-147">In Visual Studio Code, open the file **config\config.json**.</span></span>

  <span data-ttu-id="db3e9-148">Diese Datei enthält Informationen zu Ihren Bundles und externen Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="db3e9-148">This file contains information about your bundle(s) and any external dependencies.</span></span> 

  <span data-ttu-id="db3e9-p106">Der Bereich `bundles` enthält die Standardbundleinformationen - in diesem Fall jQuery-Webpartbundle. Wenn Sie Ihrer Lösung weitere Webparts hinzufügen, wird pro Webpart ein Eintrag angezeigt.</span><span class="sxs-lookup"><span data-stu-id="db3e9-p106">The `bundles` region contains the default bundle information; in this case, the jQuery web part bundle. When you add more web parts to your solution, you see one entry per web part.</span></span>

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

2. <span data-ttu-id="db3e9-151">Der Bereich `externals` enthält die Bibliotheken, die nicht im Standardbundle gebündelt sind.</span><span class="sxs-lookup"><span data-stu-id="db3e9-151">The `externals` section contains the libraries that are not bundled with the default bundle.</span></span> 

  ```json
    "externals": {},
  ```

3. <span data-ttu-id="db3e9-152">Um `jQuery` und `jQueryUI` aus dem Standardbundle zu entfernen, fügen Sie dem Bereich `externals` die Module hinzu:</span><span class="sxs-lookup"><span data-stu-id="db3e9-152">To exclude `jQuery` and `jQueryUI` from the default bundle, add the modules to the `externals` section:</span></span>

  ```json
  "jquery":"node_modules/jquery/dist/jquery.min.js",
  "jqueryui":"node_modules/jqueryui/jquery-ui.min.js"
  ```

<span data-ttu-id="db3e9-153">Wenn Sie nun Ihr Projekt erstellen, werden `jQuery` und `jQueryUI` nicht im standardmäßigen Webpartbundle gebündelt.</span><span class="sxs-lookup"><span data-stu-id="db3e9-153">Now when you build your project, `jQuery` and `jQueryUI` are not bundled into your default web part bundle.</span></span>

<span data-ttu-id="db3e9-154">Der vollständige Inhalt der config.json-Datei ist derzeit wie folgt:</span><span class="sxs-lookup"><span data-stu-id="db3e9-154">The full content of the config.json file is currently as follows:</span></span>

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


## <a name="build-the-accordion"></a><span data-ttu-id="db3e9-155">Erstellen von Accordion</span><span class="sxs-lookup"><span data-stu-id="db3e9-155">Build the Accordion</span></span>

<span data-ttu-id="db3e9-156">Öffnen Sie den Projektordner **jquery-webpart** in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="db3e9-156">Open the project folder **jquery-webpart** in Visual Studio Code.</span></span> <span data-ttu-id="db3e9-157">Ihr Projekt sollte das jQuery-Webpart aufweisen, das Sie zuvor im Ordner `/src/webparts/jQuery` hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="db3e9-157">Your project should have the jQuery web part that you added earlier under the `/src/webparts/jQuery` folder.</span></span>

### <a name="to-add-the-accordion-html"></a><span data-ttu-id="db3e9-158">So fügen Sie die Accordion-HTML hinzu</span><span class="sxs-lookup"><span data-stu-id="db3e9-158">To add the Accordion HTML</span></span>

1. <span data-ttu-id="db3e9-159">Fügen Sie eine neue Datei im `src/webparts/jQuery`-Ordner namens **MyAccordionTemplate.ts** hinzu.</span><span class="sxs-lookup"><span data-stu-id="db3e9-159">Add a new file in the `src/webparts/jQuery` folder called **MyAccordionTemplate.ts**.</span></span>

2. <span data-ttu-id="db3e9-160">Erstellen und exportieren Sie eine Klasse `MyAccordionTemplate` (als Modul), die den HTML-Code für das Accordion enthält.</span><span class="sxs-lookup"><span data-stu-id="db3e9-160">Create and export (as a module) a class `MyAccordionTemplate` that holds the HTML code for the accordion.</span></span>

  ```HTML
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

3. <span data-ttu-id="db3e9-161">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="db3e9-161">Save the file.</span></span>

### <a name="to-import-the-accordion-html"></a><span data-ttu-id="db3e9-162">So importieren Sie die Accordion-HTML</span><span class="sxs-lookup"><span data-stu-id="db3e9-162">To import the Accordion HTML</span></span>

1. <span data-ttu-id="db3e9-163">Öffnen Sie in Visual Studio Code **src\webparts\jQuery\JQueryWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="db3e9-163">In Visual Studio Code, open **src\webparts\jQuery\JQueryWebPart.ts**.</span></span>

2. <span data-ttu-id="db3e9-164">Fügen Sie am Anfang der Datei, wo sich auch andere Importe befinden, den folgenden Import hinzu:</span><span class="sxs-lookup"><span data-stu-id="db3e9-164">At the top of the file, where you can find other imports, add the following import:</span></span>

  ```typescript
  import MyAccordionTemplate from './MyAccordionTemplate';
  ```

### <a name="to-import-jquery-and-jqueryui"></a><span data-ttu-id="db3e9-165">So importieren Sie jQuery und jQueryUI</span><span class="sxs-lookup"><span data-stu-id="db3e9-165">To import jQuery and jQueryUI</span></span>

1. <span data-ttu-id="db3e9-166">Sie können jQuery auf die gleiche Weise in Ihr Webpart importieren, wie Sie „MyAccordionTemplate“ importiert haben.</span><span class="sxs-lookup"><span data-stu-id="db3e9-166">You can import jQuery to your web part in the same way that you imported MyAccordionTemplate.</span></span> <span data-ttu-id="db3e9-167">Fügen Sie am Anfang der Datei, wo sich auch andere Importe befinden, die folgenden Importe hinzu:</span><span class="sxs-lookup"><span data-stu-id="db3e9-167">At the top of the file, where you can find other imports, add the following imports:</span></span>

  ```typescript
  import * as jQuery from 'jquery';
  import 'jqueryui';
  ```

2. <span data-ttu-id="db3e9-168">Laden Sie einige externe CSS-Dateien mithilfe des Modulladeprogramms.</span><span class="sxs-lookup"><span data-stu-id="db3e9-168">Load some external CSS files by using the module loader.</span></span> <span data-ttu-id="db3e9-169">Fügen Sie den folgenden Import hinzu:</span><span class="sxs-lookup"><span data-stu-id="db3e9-169">Add the following import:</span></span>

  ```typescript
  import { SPComponentLoader } from '@microsoft/sp-loader';
  ```

3. <span data-ttu-id="db3e9-170">Laden Sie die jQueryUI-Formatvorlagen in der `JQueryWebPart`-Webpartklasse, indem Sie einen Konstruktor hinzufügen und den neu importierten SPComponentLoader verwenden.</span><span class="sxs-lookup"><span data-stu-id="db3e9-170">Load the jQueryUI styles in the `JQueryWebPart` web part class by adding a constructor and using the newly imported SPComponentLoader.</span></span> <span data-ttu-id="db3e9-171">Fügen Sie den folgenden Konstruktor zu Ihrem Webpart hinzu.</span><span class="sxs-lookup"><span data-stu-id="db3e9-171">Add the following constructor to your web part:</span></span> 

  ```typescript
    public constructor() {
      super();

      SPComponentLoader.loadCss('//code.jquery.com/ui/1.11.4/themes/smoothness/jquery-ui.css');
    }
  ```

  <span data-ttu-id="db3e9-172">Durch diesen Code wird Folgendes ausgeführt:</span><span class="sxs-lookup"><span data-stu-id="db3e9-172">This code does the following:</span></span>

  * <span data-ttu-id="db3e9-173">Aufruf des übergeordneten Konstruktors mit dem Kontext zum Initialisieren des Webparts.</span><span class="sxs-lookup"><span data-stu-id="db3e9-173">Calls the parent constructor with the context to initialize the web part.</span></span>
  * <span data-ttu-id="db3e9-174">Asynchrones Laden der Accordion-Formatvorlagen aus einem CDN.</span><span class="sxs-lookup"><span data-stu-id="db3e9-174">Loads the accordion styles from a CDN asynchronously.</span></span>


### <a name="to-render-accordion"></a><span data-ttu-id="db3e9-175">So rendern Sie Accordion</span><span class="sxs-lookup"><span data-stu-id="db3e9-175">To render Accordion</span></span>

1. <span data-ttu-id="db3e9-176">Wechseln Sie in der `jQueryWebPart.ts` zur `render`-Methode.</span><span class="sxs-lookup"><span data-stu-id="db3e9-176">In the `jQueryWebPart.ts`, go to the `render` method.</span></span>

2. <span data-ttu-id="db3e9-177">Legen Sie die innere HTML des Webparts so fest, dass die Accordion-HTML wiedergegeben wird:</span><span class="sxs-lookup"><span data-stu-id="db3e9-177">Set the web part's inner HTML to render the accordion HTML:</span></span>

  ```typescript
  this.domElement.innerHTML = MyAccordionTemplate.templateHtml;
  ```

3. <span data-ttu-id="db3e9-178">jQueryUI Accordion weist einige Optionen auf, die Sie zum Anpassen des Accordions festlegen können.</span><span class="sxs-lookup"><span data-stu-id="db3e9-178">jQueryUI Accordion has a few options that you can set to customize the accordion.</span></span> <span data-ttu-id="db3e9-179">Definieren Sie einige Optionen für Ihr Accordion direkt unter `this.domElement.innerHTML = MyAccordionTemplate.templateHtml;`:</span><span class="sxs-lookup"><span data-stu-id="db3e9-179">Define a few options for your accordion just under `this.domElement.innerHTML = MyAccordionTemplate.templateHtml;`:</span></span>

  ```typescript
  const accordionOptions: JQueryUI.AccordionOptions = {
    animate: true,
    collapsible: false,
    icons: {
      header: 'ui-icon-circle-arrow-e',
      activeHeader: 'ui-icon-circle-arrow-s'
    }
  };
  ```

  <span data-ttu-id="db3e9-180">Wie Sie sehen können, können Sie über die jQueryUI-Typdefinition eine Typvariable mit dem Namen `JQueryUI.AccordionOptions` und die unterstützten Eigenschaften angeben.</span><span class="sxs-lookup"><span data-stu-id="db3e9-180">As you can see, the jQueryUI typed definition allows you to create a typed variable called `JQueryUI.AccordionOptions` and specify the supported properties.</span></span> 

  <span data-ttu-id="db3e9-181">Wenn Sie mit IntelliSense experimentieren, werden Sie feststellen, dass Sie volle Unterstützung für in `JQueryUI.` verfügbare Methoden sowie die Methodenparameter erhalten.</span><span class="sxs-lookup"><span data-stu-id="db3e9-181">If you play around with the IntelliSense, you notice that you get full support for available methods under `JQueryUI.` as well as the method parameters.</span></span>

4. <span data-ttu-id="db3e9-182">Initialisieren Sie schließlich das Accordion:</span><span class="sxs-lookup"><span data-stu-id="db3e9-182">Finally, initialize the accordion:</span></span>

  ```typescript
  jQuery('.accordion', this.domElement).accordion(accordionOptions);
  ```

  <span data-ttu-id="db3e9-p112">Wie Sie sehen können, verwenden Sie die Variable `jQuery`, die Sie zum Importieren des `jquery`-Moduls verwendet haben. Initialisieren Sie dann das Accordion.</span><span class="sxs-lookup"><span data-stu-id="db3e9-p112">As you can see, you use the variable `jQuery` that you used to import the `jquery` module. You then initialize the accordion.</span></span>

  <span data-ttu-id="db3e9-185">Die vollständige `render`-Methodenklasse sieht wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="db3e9-185">The complete `render` method looks like this:</span></span>

  ```typescript
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

5. <span data-ttu-id="db3e9-186">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="db3e9-186">Save the file.</span></span>


## <a name="preview-the-web-part"></a><span data-ttu-id="db3e9-187">Anzeigen des Webparts</span><span class="sxs-lookup"><span data-stu-id="db3e9-187">Preview the web part</span></span>

1. <span data-ttu-id="db3e9-188">Stellen Sie in der Konsole sicher, dass Sie sich immer noch im Ordner „jquery-webpart“ befinden, und geben Sie Folgendes ein, um das Webpart zu erstellen und in der Vorschau anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="db3e9-188">In your console, ensure that you are still in the jquery-webpart folder, and enter the following to build and preview your web part:</span></span>

  ```
  gulp serve
  ```

  > [!NOTE]
  > <span data-ttu-id="db3e9-189">Visual Studio Code bietet integrierte Unterstützung für gulp und andere Tools zur Taskausführung.</span><span class="sxs-lookup"><span data-stu-id="db3e9-189">Visual Studio Code provides built-in support for gulp and other task runners.</span></span> <span data-ttu-id="db3e9-190">Sie können STRG + UMSCHALT + B unter Windows oder BEFEHL + UMSCHALT + B auf dem Mac drücken, um Ihr Webpart zu debuggen und eine Vorschau anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="db3e9-190">You can select Ctrl+Shift+B in Windows or Cmd+Shift+B on a Mac to debug and preview your web part.</span></span>

  <span data-ttu-id="db3e9-191">Gulp führt die Aufgaben aus und öffnet die lokale SharePoint-Webpart-Workbench.</span><span class="sxs-lookup"><span data-stu-id="db3e9-191">Gulp executes the tasks and opens the local SharePoint web part Workbench.</span></span>

2. <span data-ttu-id="db3e9-192">Drücken Sie im Seitenbereich auf das **+** (Pluszeichen), um die Liste von Webparts anzuzeigen, und führen Sie das jQuery-Webpart hinzu.</span><span class="sxs-lookup"><span data-stu-id="db3e9-192">In the page canvas, select the **+** (plus sign) to show the list of web parts, and add the jQuery web part.</span></span> <span data-ttu-id="db3e9-193">Jetzt sollte das jQueryUI Accordion angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="db3e9-193">You should now see the jQueryUI Accordion!</span></span>

  ![Screenshot eines Webparts, das ein jQuery Accordion umfasst](../../../images/jquery-accordion-wb.png)

3. <span data-ttu-id="db3e9-195">Drücken Sie in der Konsole, in der `gulp serve` ausgeführt wird, auf STRG + C, um die Aufgabe abzubrechen.</span><span class="sxs-lookup"><span data-stu-id="db3e9-195">In the console where you have `gulp serve` running, select Ctrl+C to terminate the task.</span></span>

> [!NOTE]
> <span data-ttu-id="db3e9-196">Wenn Sie einen Fehler in der Dokumentation oder im SharePoint-Framework finden, melden Sie ihn an das SharePoint Engineering unter Verwendung der [Fehlerliste im sp-dev-docs-Repository](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="db3e9-196">If you find an issue in the documentation or in the SharePoint Framework, report that to SharePoint engineering by using the [issue list at the sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="db3e9-197">Vielen Dank im Voraus für Ihr Feedback.</span><span class="sxs-lookup"><span data-stu-id="db3e9-197">Thanks for your input in advance.</span></span>

