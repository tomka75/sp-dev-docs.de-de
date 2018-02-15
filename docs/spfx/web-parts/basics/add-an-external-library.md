---
title: "Hinzufügen einer externen Bibliothek zu Ihrem clientseitigen SharePoint-Webpart"
description: "Bündeln einer externen JavaScript-Bibliothek und Freigeben von Bibliotheken."
ms.date: 01/29/2018
ms.prod: sharepoint
ms.openlocfilehash: 7b5091f531ad16127aa71299f9c1951cbb2c853c
ms.sourcegitcommit: e4bf60eabffe63dc07f96824167d249c0678db82
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/30/2018
---
# <a name="add-an-external-library-to-your-sharepoint-client-side-web-part"></a><span data-ttu-id="3adbb-103">Hinzufügen einer externen Bibliothek zu Ihrem clientseitigen SharePoint-Webpart</span><span class="sxs-lookup"><span data-stu-id="3adbb-103">Add an external library to your SharePoint client-side web part</span></span>

<span data-ttu-id="3adbb-p101">Vielleicht möchten Sie eine oder mehrere JavaScript-Bibliotheken in Ihr Webpart einfügen. In diesem Artikel wird gezeigt, wie Sie eine externe Bibliothek bündeln und Bibliotheken freigeben.</span><span class="sxs-lookup"><span data-stu-id="3adbb-p101">You might want to include one or more JavaScript libraries in your web part. This article shows you how to bundle an external library and share libraries.</span></span>

## <a name="bundle-a-script"></a><span data-ttu-id="3adbb-106">Bündeln eines Skripts</span><span class="sxs-lookup"><span data-stu-id="3adbb-106">Bundle a script</span></span>

<span data-ttu-id="3adbb-107">Der Webpart-Bundler schließt standardmäßig automatisch jede Bibliothek ein, die eine Abhängigkeit des Webpartmoduls aufweist.</span><span class="sxs-lookup"><span data-stu-id="3adbb-107">By default, the web part bundler automatically includes any library that is a dependency of the web part module.</span></span> <span data-ttu-id="3adbb-108">Dies bedeutet, dass die Bibliothek in derselben JavaScript-Bundledatei wie Ihr Webpart bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="3adbb-108">This means that the library is deployed in the same JavaScript bundle file as your web part.</span></span> <span data-ttu-id="3adbb-109">Dies ist bei kleineren Bibliotheken hilfreich, die nicht in mehreren Webparts verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="3adbb-109">This is more useful for smaller libraries that are not used in multiple web parts.</span></span>

### <a name="example"></a><span data-ttu-id="3adbb-110">Beispiel</span><span class="sxs-lookup"><span data-stu-id="3adbb-110">Example</span></span>

1. <span data-ttu-id="3adbb-111">Schließen Sie die Zeichenfolge, die das [validator](https://www.npmjs.com/package/validator)-Paket der Bibliothek überprüft, in ein Webpart ein.</span><span class="sxs-lookup"><span data-stu-id="3adbb-111">Include the string validating library [validator](https://www.npmjs.com/package/validator) package into a web part.</span></span>

2. <span data-ttu-id="3adbb-112">Laden Sie das validator-Paket von npm herunter:</span><span class="sxs-lookup"><span data-stu-id="3adbb-112">Download the validator package from npm:</span></span>

    ```sh
    npm install validator --save
    ```

    > [!NOTE] 
    > <span data-ttu-id="3adbb-p103">Da Sie TypeScript verwenden, benötigen Sie für das Paket, das Sie hinzufügen, Eingaben. Dies ist wichtig, wenn Sie Code schreiben, da TypeScript nur eine Obermenge von JavaScript ist. Der gesamte TypeScript-Code wird beim Kompilieren nach wie vor in JavaScript-Code konvertiert. Sie können mithilfe von **npm** nach Eingaben suchen, beispielsweise: `npm install @types/{package} --save`</span><span class="sxs-lookup"><span data-stu-id="3adbb-p103">Because you're using TypeScript, you need typings for the package you add. This is essential when you are writing code because TypeScript is just a superset of JavaScript. All the TypeScript code is still converted to JavaScript code when you compile. You can search for and find typings by using **npm**, for example: `npm install @types/{package} --save`</span></span>

3. <span data-ttu-id="3adbb-117">Erstellen Sie im Ordner Ihres Webparts eine Datei mit dem Namen `validator.d.ts`, und fügen Sie den nachfolgenden Code in die Datei ein:</span><span class="sxs-lookup"><span data-stu-id="3adbb-117">Create a file in the your web part's folder called `validator.d.ts` and add the following:</span></span>

    ```typescript
    declare module "validator" {
        export function isEmail(email: string): boolean;
        export function isAscii(text: string): boolean;
    }
    ```

    > [!NOTE] 
    > <span data-ttu-id="3adbb-118">Manche Bibliotheken verfügen nicht über Eingaben.</span><span class="sxs-lookup"><span data-stu-id="3adbb-118">Some libraries do not have typings.</span></span> <span data-ttu-id="3adbb-119">Die validator-Bibliothek verfügt zwar über eine [von der Community bereitgestellte Eingabendatei](https://www.npmjs.com/package/@types/validator), in diesem Szenario wird aber davon ausgegangen, dass dies nicht der Fall ist.</span><span class="sxs-lookup"><span data-stu-id="3adbb-119">While the validator library does have a [community provided typings file](https://www.npmjs.com/package/@types/validator), for this scenario let's assume it does not.</span></span> <span data-ttu-id="3adbb-120">In diesem Fall müssen Sie Ihre eigene `.d.ts`-Datei für die Eingabedefinition für die Bibliothek definieren.</span><span class="sxs-lookup"><span data-stu-id="3adbb-120">Note: Some libraries do not have typings. Validator is one of them. In this case you would want to define your own typings definition `.d.ts` file for the library. The following code shows an example.</span></span> <span data-ttu-id="3adbb-121">Im vorherigen Code ist ein Beispiel dargestellt:</span><span class="sxs-lookup"><span data-stu-id="3adbb-121">The following code shows an example token file.</span></span>

4. <span data-ttu-id="3adbb-122">Importieren Sie die Eingaben in Ihre Webpartdatei:</span><span class="sxs-lookup"><span data-stu-id="3adbb-122">In your web part file, import the typings:</span></span>

    ```typescript
    import * as validator from 'validator';
    ```

5. <span data-ttu-id="3adbb-123">Verwenden Sie die validator-Bibliothek im Webpartcode:</span><span class="sxs-lookup"><span data-stu-id="3adbb-123">Use the validator library in your web part code:</span></span>

    ```typescript
    validator.isEmail('someone@example.com');
    ```

## <a name="share-a-library-among-multiple-web-parts"></a><span data-ttu-id="3adbb-124">Freigeben einer Bibliothek zwischen mehreren Webparts</span><span class="sxs-lookup"><span data-stu-id="3adbb-124">Share a library among multiple web parts</span></span>

<span data-ttu-id="3adbb-p105">Ihre clientseitige Lösung umfasst möglicherweise mehrere Webparts. Diese Webparts müssen möglicherweise die gleiche Bibliothek importieren oder freigeben. In solchen Fällen sollten Sie die Bibliothek in eine separate JavaScript-Datei einschließen, anstatt sie zu bündeln, um Leistung und Zwischenspeicherung zu verbessern. Dies gilt besonders für größere Bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="3adbb-p105">Your client-side solution might include multiple web parts. These web parts might need to import or share the same library. In such cases, instead of bundling the library, you should include it in a separate JavaScript file to improve performance and caching. This is especially true of larger libraries.</span></span>

### <a name="example"></a><span data-ttu-id="3adbb-129">Beispiel</span><span class="sxs-lookup"><span data-stu-id="3adbb-129">Example</span></span>

<span data-ttu-id="3adbb-130">In diesem Beispiel geben Sie das [marked](https://www.npmjs.com/package/marked)-Paket - einen Markdown-Compiler - in einem separaten Bundle frei.</span><span class="sxs-lookup"><span data-stu-id="3adbb-130">In this example, you will share the [marked](https://www.npmjs.com/package/marked) package - a Markdown compiler - in a separate bundle.</span></span>

1. <span data-ttu-id="3adbb-131">Herunterladen des **marked**-Pakets von npm:</span><span class="sxs-lookup"><span data-stu-id="3adbb-131">Download the **marked** package from npm:</span></span>

    ```sh
    npm install marked --save
    ```

2. <span data-ttu-id="3adbb-132">Herunterladen der Eingaben:</span><span class="sxs-lookup"><span data-stu-id="3adbb-132">Download the typings:</span></span>

    ```sh
    npm install @types/marked --save
    ```

3. <span data-ttu-id="3adbb-133">Bearbeiten Sie **config/config.json**, und fügen Sie einen Eintrag zur Zuordnung **externals** hinzu.</span><span class="sxs-lookup"><span data-stu-id="3adbb-133">Edit the **config/config.json**, and add an entry to the **externals** map.</span></span> <span data-ttu-id="3adbb-134">Dadurch wird dem Bundler mitgeteilt, dies in einer separaten Datei zu platzieren.</span><span class="sxs-lookup"><span data-stu-id="3adbb-134">This is what tells the bundler to put this in a separate file.</span></span> <span data-ttu-id="3adbb-135">Dadurch wird verhindert, dass der Bundler diese Bibliothek bündelt:</span><span class="sxs-lookup"><span data-stu-id="3adbb-135">This prevents the bundler from bundling this library:</span></span>

    ```json
    "marked": "node_modules/marked/marked.min.js"
    ```

4. <span data-ttu-id="3adbb-136">Fügen Sie die Anweisung zum Importieren der `marked`-Bibliothek nun in das Webpart ein, nachdem Sie das Paket und die Eingaben für die Bibliothek hinzugefügt haben:</span><span class="sxs-lookup"><span data-stu-id="3adbb-136">Add the statement to import the `marked` library in your web part now that we have added the package and typings for the library:</span></span>

    ```typescript
    import * as marked from 'marked';
    ```

5. <span data-ttu-id="3adbb-137">Verwenden der Bibliothek im Webpart:</span><span class="sxs-lookup"><span data-stu-id="3adbb-137">Use the library in your web part:</span></span>

    ```typescript
    console.log(marked('I am using __markdown__.'));
    ```

## <a name="load-a-script-from-a-cdn"></a><span data-ttu-id="3adbb-138">Laden eines Skripts aus einem CDN</span><span class="sxs-lookup"><span data-stu-id="3adbb-138">Loading a script from a CDN</span></span>

<span data-ttu-id="3adbb-139">Anstatt die Bibliothek aus einem npm-Paket zu laden, können Sie ein Skript aus einem Content Delivery Network (CDN) laden.</span><span class="sxs-lookup"><span data-stu-id="3adbb-139">Instead of loading the library from an npm package, you might want to load a script from a Content Delivery Network (CDN).</span></span> <span data-ttu-id="3adbb-140">Bearbeiten Sie hierzu die **config.json**-Datei, um die Bibliothek von ihrer CDN-URL zu laden.</span><span class="sxs-lookup"><span data-stu-id="3adbb-140">Instead of loading the library from a npm package, you might want to load a script from a CDN. To do so, edit the **config.json** file to load the library from its CDN URL.</span></span>

### <a name="example"></a><span data-ttu-id="3adbb-141">Beispiel</span><span class="sxs-lookup"><span data-stu-id="3adbb-141">Example</span></span>

<span data-ttu-id="3adbb-p108">In diesem Beispiel laden Sie jQuery aus einem CDN. Sie müssen nicht das npm-Paket installieren. Sie müssen jedoch die Eingaben installieren.</span><span class="sxs-lookup"><span data-stu-id="3adbb-p108">In this example, you will load jQuery from CDN. You don't need to install the npm package. However, you still need to install the typings.</span></span>

1. <span data-ttu-id="3adbb-145">Installieren der Eingaben für jQuery:</span><span class="sxs-lookup"><span data-stu-id="3adbb-145">Install the typings for jQuery:</span></span>

    ```sh
    npm install --save @types/jquery
    ```

2. <span data-ttu-id="3adbb-p109">Aktualisieren Sie `config.json` im Ordner `config`, um jQuery aus einem CDN zu laden. Hinzufügen eines Eintrags zum `externals`-Feld:</span><span class="sxs-lookup"><span data-stu-id="3adbb-p109">Update the `config.json` in the `config` folder to load jQuery from CDN. Add an entry to the `externals` field:</span></span>

    ```json
    "jquery": "https://code.jquery.com/jquery-3.1.0.min.js"
    ```

3. <span data-ttu-id="3adbb-148">Importieren von jQuery in das Webpart:</span><span class="sxs-lookup"><span data-stu-id="3adbb-148">Import jQuery in your web part:</span></span>

    ```typescript
    import * as $ from 'jquery';
    ```

4. <span data-ttu-id="3adbb-149">Verwenden von jQuery im Webpart:</span><span class="sxs-lookup"><span data-stu-id="3adbb-149">Use jQuery in your web part:</span></span>

    ```javascript
    alert( $('#foo').val() );
    ```

## <a name="load-a-non-amd-module"></a><span data-ttu-id="3adbb-150">Laden eines Nicht-AMD-Moduls</span><span class="sxs-lookup"><span data-stu-id="3adbb-150">Loading a non-AMD module</span></span>

<span data-ttu-id="3adbb-p110">Einige Skripts folgen dem veralteten JavaScript-Muster des Speicherns der Bibliothek im globalen Namespace. Dieses Muster wurde nun durch [Universal Modul Definitions (UMD)](https://github.com/umdjs/umd),  / [Asynchronous Module Definitions (AMD)](https://en.wikipedia.org/wiki/Asynchronous_module_definition) oder [ES6-Module](https://github.com/lukehoban/es6features/blob/master/README.md#modules) ersetzt. Möglicherweise müssen Sie solche Bibliotheken jedoch in das Webpart laden.</span><span class="sxs-lookup"><span data-stu-id="3adbb-p110">Some scripts follow the legacy JavaScript pattern of storing the library on the global namespace. This pattern is now deprecated in favor of [Universal Module Definitions (UMD)](https://github.com/umdjs/umd) / [Asynchronous Module Definitions (AMD)](https://en.wikipedia.org/wiki/Asynchronous_module_definition) or [ES6 modules](https://github.com/lukehoban/es6features/blob/master/README.md#modules). However, you might need to load such libraries in your web part.</span></span>

> [!TIP] 
> <span data-ttu-id="3adbb-154">Es ist schwierig, manuell ermitteln, ob das Skript, das Sie laden möchten, ein AMD- oder ein Nicht-AMD-Skript ist.</span><span class="sxs-lookup"><span data-stu-id="3adbb-154">It's difficult to determine manually whether the script that you're trying to load is an AMD or a non-AMD script.</span></span> <span data-ttu-id="3adbb-155">Dies ist insbesondere dann der Fall, wenn das Skript minimiert ist.</span><span class="sxs-lookup"><span data-stu-id="3adbb-155">This is especially the case if the script that you're trying to load is minified.</span></span> <span data-ttu-id="3adbb-156">Wenn das Skript auf einer öffentlich zugänglichen URL gehostet wird, können Sie das kostenlose Tool [Rencore SharePoint Framework Script Check](https://rencore.com/sharepoint-framework/script-check/) verwenden, um die Art des Skripts zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="3adbb-156">If your script is hosted on a publicly accessible URL, you can use the free [Rencore SharePoint Framework Script Check](https://rencore.com/sharepoint-framework/script-check/) tool to determine the type of script for you.</span></span> <span data-ttu-id="3adbb-157">Dieses Tool teilt Ihnen außerdem mit, ob der Hostingspeicherort, vom dem aus Sie das Skript laden, korrekt konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="3adbb-157">Additionally, this tool lets you know whether the hosting location from which you're loading the script is properly configured.</span></span>

<span data-ttu-id="3adbb-158">Um ein Nicht-AMD-Modul zu laden, fügen Sie eine zusätzliche Eigenschaft zu dem Eintrag in der **config.json**-Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="3adbb-158">To load a non-AMD module, you add an additional property to the entry in your **config.json** file.</span></span>

### <a name="example"></a><span data-ttu-id="3adbb-159">Beispiel</span><span class="sxs-lookup"><span data-stu-id="3adbb-159">Example</span></span>

<span data-ttu-id="3adbb-p112">In diesem Beispiel laden Sie ein fiktives Nicht-AMD-Modul aus dem Contoso-CDN. Diese Schritte gelten für alle Nicht-AMD Skripts im Verzeichnis „src/“ oder „node_modules/“.</span><span class="sxs-lookup"><span data-stu-id="3adbb-p112">In this example, you will load a fictional non-AMD module from Contoso's CDN. These steps  apply for any non-AMD script in your src/ or node_modules/ directory.</span></span>

<span data-ttu-id="3adbb-p113">Das Skript heißt **Contoso.js** und ist unter **https://contoso.com/contoso.js** gespeichert. Sein Inhalt ist wie folgt:</span><span class="sxs-lookup"><span data-stu-id="3adbb-p113">The script is called **Contoso.js** and is stored at **https://contoso.com/contoso.js**. Its contents are:</span></span>

```javascript
var ContosoJS = {
  say: function(text) { alert(text); },
  sayHello: function(name) { alert('Hello, ' + name + '!'); }
};
```

<br/>

1. <span data-ttu-id="3adbb-164">Erstellen von Eingaben für das Skript in einer Datei mit dem Namen **contoso.d.ts** im Webpartordner.</span><span class="sxs-lookup"><span data-stu-id="3adbb-164">Create typings for the script in a file called **contoso.d.ts** in the web part folder.</span></span>

    ```typescript
    declare module "contoso" {
        interface IContoso {
            say(text: string): void;
            sayHello(name: string): void;
        }
        var contoso: IContoso;
        export = contoso;
    }
    ```

2. <span data-ttu-id="3adbb-p114">Aktualisieren der **config.json**-Datei derart, dass dieses Skript eingeschlossen wird. Hinzufügen eines Eintrags zur **externals**-Zuordnung:</span><span class="sxs-lookup"><span data-stu-id="3adbb-p114">Update the **config.json** file to include this script. Add an entry to the **externals** map:</span></span>

    ```json
    {
        "contoso": {
            "path": "https://contoso.com/contoso.js",
            "globalName": "ContosoJS"
        }
    }
    ```

3. <span data-ttu-id="3adbb-167">Hinzufügen eines Imports zum Webpartcode:</span><span class="sxs-lookup"><span data-stu-id="3adbb-167">Add an import to your web part code:</span></span>

    ```typescript
    import contoso from 'contoso';
    ```

4. <span data-ttu-id="3adbb-168">Verwenden der Contoso-Bibliothek im Code:</span><span class="sxs-lookup"><span data-stu-id="3adbb-168">Use the contoso library in your code:</span></span>

    ```typescript
    contoso.sayHello(username);
    ```

## <a name="load-a-library-that-has-a-dependency-on-another-library"></a><span data-ttu-id="3adbb-169">Laden einer Bibliothek, die eine Abhängigkeit von einer anderen Bibliothek aufweist</span><span class="sxs-lookup"><span data-stu-id="3adbb-169">Loading a library that has a dependency on another library</span></span>

<span data-ttu-id="3adbb-170">Viele Bibliotheken weisen Abhängigkeiten von einer anderen Bibliothek auf.</span><span class="sxs-lookup"><span data-stu-id="3adbb-170">Many libraries have dependencies on another library.</span></span> <span data-ttu-id="3adbb-171">Sie können solche Abhängigkeiten in der **config.json**-Datei mithilfe der **globalDependencies**-Eigenschaft angeben.</span><span class="sxs-lookup"><span data-stu-id="3adbb-171">Many libraries have dependencies on another library. You can specify such dependencies in the **config.json** file using the **globalDependencies** property.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="3adbb-172">Beachten Sie, dass Sie dieses Feld für AMD-Module nicht angeben müssen; diese importieren sich gegenseitig ordnungsgemäß.</span><span class="sxs-lookup"><span data-stu-id="3adbb-172">Note that you don't have to specify this field for non-AMD modules; they will properly import each other. However, it is important to note that a non-AMD module have a AMD module as a dependency.</span></span> <span data-ttu-id="3adbb-173">Ein Nicht-AMD-Modul kann jedoch kein AMD-Modul als Abhängigkeit aufweisen.</span><span class="sxs-lookup"><span data-stu-id="3adbb-173">However, a non-AMD module cannot have an AMD module as a dependency.</span></span> <span data-ttu-id="3adbb-174">In einigen Fällen ist es möglich, ein AMD-Skript als Nicht-AMD-Skript zu laden.</span><span class="sxs-lookup"><span data-stu-id="3adbb-174">In some cases, it is possible to load an AMD script as a non-AMD script.</span></span> <span data-ttu-id="3adbb-175">Dies ist häufig bei der Arbeit mit jQuery (selbst ein AMD-Skript) und jQuery-Plug-Ins erforderlich, die meistens als Nicht-AMD-Skripts verteilt werden und von jQuery abhängig sind.</span><span class="sxs-lookup"><span data-stu-id="3adbb-175">This is often required when working with jQuery, which by itself is an AMD script, and jQuery plug-ins, which most of the time are distributed as non-AMD scripts and which depend on jQuery.</span></span>

<span data-ttu-id="3adbb-176">Hierfür gibt es zwei Beispiele.</span><span class="sxs-lookup"><span data-stu-id="3adbb-176">There are two examples of this.</span></span>

### <a name="non-amd-module-has-a-non-amd-module-dependency"></a><span data-ttu-id="3adbb-177">Nicht-AMD-Modul weist eine Abhängigkeit zu einem Nicht-AMD-Modul auf</span><span class="sxs-lookup"><span data-stu-id="3adbb-177">Non-AMD module has a non-AMD module dependency</span></span>

<span data-ttu-id="3adbb-p117">In diesem Beispiel gibt es zwei fiktive Skripts. Sie befinden sich im Ordner **src/**, können jedoch auch aus einem CDN geladen werden.</span><span class="sxs-lookup"><span data-stu-id="3adbb-p117">This example involves two fictional scripts. These are in the **src/** folder, although they can also be loaded from a CDN.</span></span>

<span data-ttu-id="3adbb-180">**ContosoUI.js**</span><span class="sxs-lookup"><span data-stu-id="3adbb-180">**ContosoUI.js**</span></span>

```javascript
Contoso.EventList = {
    alert: function() {
        var events = Contoso.getEvents();
        events.forEach( function(event) {
            alert(event);
        });
    }
}
```

<span data-ttu-id="3adbb-181">**ContosoCore.js**</span><span class="sxs-lookup"><span data-stu-id="3adbb-181">**ContosoCore.js**</span></span>

```javascript
var Contoso = {
    getEvents: function() {
        return ['A', 'B', 'C'];
    }
};
```

<br/>

1. <span data-ttu-id="3adbb-p118">Fügen Sie Eingaben für diese Klasse hinzu, oder erstellen Sie sie. In diesem Fall erstellen Sie `Contoso.d.ts` mit Eingaben für beide JavaScript-Dateien.</span><span class="sxs-lookup"><span data-stu-id="3adbb-p118">Add or create typings for this class. In this case, you will create `Contoso.d.ts`, which contains typings for both JavaScript files.</span></span>

    <span data-ttu-id="3adbb-184">**contoso.d.ts**</span><span class="sxs-lookup"><span data-stu-id="3adbb-184">**contoso.d.ts**</span></span>

    ```typescript
    declare module "contoso" {
        interface IEventList {
            alert(): void;
        }
        interface IContoso {
            getEvents(): string[];
            EventList: IEventList;
        }
        var contoso: IContoso;
        export = contoso;
    }
    ```

2. <span data-ttu-id="3adbb-p119">Aktualisieren Sie die **config.json**-Datei. Hinzufügen von zwei Einträgen zu **externals**:</span><span class="sxs-lookup"><span data-stu-id="3adbb-p119">Update the **config.json** file. Add two entries to **externals**:</span></span>

    ```json
    {
        "contoso": {
            "path": "/src/ContosoCore.js",
            "globalName": "Contoso"
        },
        "contoso-ui": {
            "path": "/src/ContosoUI.js",
            "globalName": "Contoso",
            "globalDependencies": ["contoso"]
        }
    }
    ```

3. <span data-ttu-id="3adbb-187">Hinzufügen von Importen für Contoso und ContosoUI:</span><span class="sxs-lookup"><span data-stu-id="3adbb-187">Add imports for Contoso and ContosoUI:</span></span>

    ```typescript
    import contoso = require('contoso');
    require('contoso-ui');
    ```

4. <span data-ttu-id="3adbb-188">Verwenden der Bibliotheken im Code:</span><span class="sxs-lookup"><span data-stu-id="3adbb-188">Use the libraries in your code:</span></span>

    ```typescript
    contoso.EventList.alert();
    ```

## <a name="load-sharepoint-jsom"></a><span data-ttu-id="3adbb-189">Laden von SharePoint JSOM</span><span class="sxs-lookup"><span data-stu-id="3adbb-189">Load SharePoint JSOM Scripts Using SPComponentLoader</span></span>

<span data-ttu-id="3adbb-p120">Das Laden von SharePoint JSOM ist im Wesentlichen das gleiche Szenario wie das Laden von Nicht-AMD-Skripts, die Abhängigkeiten haben. Hierfür wird sowohl die Option **globalName** als auch die Option **globalDependency** verwendet.</span><span class="sxs-lookup"><span data-stu-id="3adbb-p120">Loading SharePoint JSOM is essentially the same scenario as loading non-AMD scripts that have dependencies. This means using both the **globalName** and **globalDependency** options.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="3adbb-192">Beachten Sie, dass der folgende Ansatz auf klassischen SharePoint-Seiten Fehler verursacht, auf denen SharePoint JSOM bereits geladen ist.</span><span class="sxs-lookup"><span data-stu-id="3adbb-192">Note that the following approach causes errors in classic SharePoint pages, where SharePoint JSOM is already loaded.</span></span> <span data-ttu-id="3adbb-193">Wenn Ihr Webpart sowohl mit klassischen als auch mit modernen Seiten arbeiten soll, sollten Sie zuerst überprüfen, ob SharePoint JSOM bereits verfügbar ist. Ist dies nicht der fall, laden Sie es dynamisch mithilfe von **SPComponentLoader**.</span><span class="sxs-lookup"><span data-stu-id="3adbb-193">Important: Please note, that the following approach will cause error in classic SharePoint pages, where SharePoint JSOM is already loaded. If you require your web part to work with both classic and modern pages then you should first check if SharePoint JSOM is already available and if it isn't, load it dynamically using the **SPComponentLoader**.</span></span>

<br/>

1. <span data-ttu-id="3adbb-194">Installieren von Eingaben für Microsoft Ajax (Abhängigkeit für JSOM-Eingaben):</span><span class="sxs-lookup"><span data-stu-id="3adbb-194">Install typings for Microsoft Ajax which is a dependency for JSOM typings:</span></span>

    ```sh
    npm install @types/microsoft-ajax --save
    ```

2. <span data-ttu-id="3adbb-195">Installieren von Eingaben für JSOM:</span><span class="sxs-lookup"><span data-stu-id="3adbb-195">Install typings for the JSOM:</span></span>

    ```sh
    npm install @types/sharepoint --save
    ```

3. <span data-ttu-id="3adbb-196">Hinzufügen von Einträgen zu `config.json`:</span><span class="sxs-lookup"><span data-stu-id="3adbb-196">Add entries to the `config.json`:</span></span>

    ```json
    {
        "sp-init": {
            "path": "https://CONTOSO.sharepoint.com/_layouts/15/init.js",
            "globalName": "$_global_init"
        },
        "microsoft-ajax": {
            "path": "https://CONTOSO.sharepoint.com/_layouts/15/MicrosoftAjax.js",
            "globalName": "Sys",
            "globalDependencies": [ "sp-init" ]
        },
        "sp-runtime": {
            "path": "https://CONTOSO.sharepoint.com/_layouts/15/SP.Runtime.js",
            "globalName": "SP",
            "globalDependencies": [ "microsoft-ajax" ]
        },
        "sharepoint": {
            "path": "https://CONTOSO.sharepoint.com/_layouts/15/SP.js",
            "globalName": "SP",
            "globalDependencies": [ "sp-runtime" ]
        }
    }
    ```

4. <span data-ttu-id="3adbb-197">Fügen Sie in Ihrem Webpart die `require`-Anweisungen hinzu:</span><span class="sxs-lookup"><span data-stu-id="3adbb-197">In your web part, add the require statements:</span></span>

    ```typescript
    require('sp-init');
    require('microsoft-ajax');
    require('sp-runtime');
    require('sharepoint');
    ```

## <a name="load-localized-resources"></a><span data-ttu-id="3adbb-198">Laden lokalisierter Ressourcen</span><span class="sxs-lookup"><span data-stu-id="3adbb-198">Load localized resources</span></span>

<span data-ttu-id="3adbb-199">Sie können eine Zuordnung in **config.json** mit dem Namen **localizedResources** verwenden, um zu beschreiben, wie lokalisierte Ressourcen geladen werden.</span><span class="sxs-lookup"><span data-stu-id="3adbb-199">You can use a map in **config.json** called **localizedResources** to describe how to load localized resources.</span></span> <span data-ttu-id="3adbb-200">Pfade in dieser Zuordnung sind relativ zum **lib**-Ordner und dürfen keinen vorangestellten Schrägstrich (**/**) enthalten.</span><span class="sxs-lookup"><span data-stu-id="3adbb-200">There is a map in config.json called localizedResources with which you can describe how to load localized resources. Paths in this map are relative to the **lib** folder and must not contain a leading slash (**/**).</span></span>

<span data-ttu-id="3adbb-p123">In diesem Beispiel haben Sie den Ordner **src/strings/**. In diesem Ordner befinden sich mehrere JavaScript-Dateien mit Namen wie **en-us.js**, **fr-fr.js**, **de-de.js**. Da jede dieser Dateien vom Modulladeprogramm geladen werden muss, müssen sie einen CommonJS-Wrapper enthalten. In **en-us.js** beispielsweise:</span><span class="sxs-lookup"><span data-stu-id="3adbb-p123">In this example, you have a folder **src/strings/**. In this folder are several JavaScript files with names such as **en-us.js**, **fr-fr.js**, **de-de.js**. Because each of these files must be loadable by the module loader, they must contain a CommonJS wrapper. For example, in **en-us.js**:</span></span>

```typescript
  define([], function() {
    return {
      "PropertyPaneDescription": "Description",
      "BasicGroupName": "Group Name",
      "DescriptionFieldLabel": "Description Field"
    }
  });
```

<br/>

1. <span data-ttu-id="3adbb-205">Bearbeiten Sie die **config.json**-Datei.</span><span class="sxs-lookup"><span data-stu-id="3adbb-205">Edit the **config.json** file.</span></span> <span data-ttu-id="3adbb-206">Fügen Sie einen Eintrag zu **localizedResources** hinzu.</span><span class="sxs-lookup"><span data-stu-id="3adbb-206">Add an entry to **localizedResources**.</span></span> <span data-ttu-id="3adbb-207">`{locale}` ist ein Platzhaltertoken für den Gebietsschemanamen:</span><span class="sxs-lookup"><span data-stu-id="3adbb-207">`{locale}` is a placeholder token for the locale name:</span></span>

    ```json
    {
        "strings": "strings/{locale}.js"
    }
    ```

2. <span data-ttu-id="3adbb-p125">Fügen Sie Eingaben für Ihre Zeichenfolgen hinzu. In diesem Fall haben Sie die Datei **MyStrings.d.ts**:</span><span class="sxs-lookup"><span data-stu-id="3adbb-p125">Add typings for your strings. In this case, you have a file **MyStrings.d.ts**:</span></span>

    ```typescript
    declare interface IStrings {
        webpartTitle: string;
        initialPrompt: string;
        exitPrompt: string;
    }

    declare module 'mystrings' {
        const strings: IStrings;
        export = strings;
    }
    ```

3. <span data-ttu-id="3adbb-210">Hinzufügen von Importen für die Zeichenfolgen in Ihrem Projekt:</span><span class="sxs-lookup"><span data-stu-id="3adbb-210">Add imports for the strings in your project:</span></span>

    ```typescript
    import * as strings from 'mystrings';
    ```

4. <span data-ttu-id="3adbb-211">Verwenden der Zeichenfolgen in Ihrem Projekt:</span><span class="sxs-lookup"><span data-stu-id="3adbb-211">Use the strings in your project:</span></span>

    ```typescript
    alert(strings.initialPrompt);
    ```

## <a name="see-also"></a><span data-ttu-id="3adbb-212">Weitere Artikel</span><span class="sxs-lookup"><span data-stu-id="3adbb-212">See also</span></span>

- [<span data-ttu-id="3adbb-213">SharePoint Framework-Übersicht</span><span class="sxs-lookup"><span data-stu-id="3adbb-213">SharePoint Framework Extensions Overview</span></span>](../../sharepoint-framework-overview.md)