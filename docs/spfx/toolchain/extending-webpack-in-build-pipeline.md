---
title: Erweitern von Webpack in der SharePoint-Framework-Toolkette
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: c5156ce434a791658de3798ff0d7de2e73c42fb2
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="extending-webpack-in-the-sharepoint-framework-toolchain"></a><span data-ttu-id="fef80-102">Erweitern von Webpack in der SharePoint-Framework-Toolkette</span><span class="sxs-lookup"><span data-stu-id="fef80-102">Extending webpack in the SharePoint Framework toolchain</span></span>

<span data-ttu-id="fef80-103">[Webpack](https://Webpack.js.org/) ist ein JavaScript-Modulbundler, der aus Ihren JavaScript-Dateien und deren Abhängigkeiten ein oder mehrere JavaScript-Dateien generiert, damit Sie unterschiedliche Codeausschnitte für verschiedene Szenarien laden können.</span><span class="sxs-lookup"><span data-stu-id="fef80-103">[Webpack](https://Webpack.js.org/) is a JavaScript module bundler that takes your JavaScript files and its dependencies and generates one or more JavaScript bundles so you can load different bundles for different scenarios.</span></span>

<span data-ttu-id="fef80-104">Die Framework-Toolkette verwendet CommonJS zum Bündeln.</span><span class="sxs-lookup"><span data-stu-id="fef80-104">The framework toolchain uses CommonJS for bundling.</span></span> <span data-ttu-id="fef80-105">Auf diese Weise können Sie Module und Verwendungsmöglichkeiten definieren.</span><span class="sxs-lookup"><span data-stu-id="fef80-105">This enables you to define modules and where you want to use them.</span></span> <span data-ttu-id="fef80-106">Die Toolkette verwendet auch SystemJS, ein universelles Modulladeprogramm, um Ihre Module zu laden.</span><span class="sxs-lookup"><span data-stu-id="fef80-106">The toolchain also uses SystemJS, a universal module loader, to load your modules.</span></span> <span data-ttu-id="fef80-107">Auf diese Weise können Sie den Bereich für Ihre Webparts festlegen, indem Sie sicherstellen, dass jedes Webpart in seinem eigenen Namespace ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="fef80-107">This helps you to scope your web parts by making sure that each web part is executed in its own namespace.</span></span>

<span data-ttu-id="fef80-108">Eine häufige Aufgabe, die Sie ggf. der SharePoint-Framework-Toolkette hinzufügen möchten, ist die Erweiterung der Webpack-Konfiguration mit benutzerdefinierten Ladeprogrammen und Plug-Ins.</span><span class="sxs-lookup"><span data-stu-id="fef80-108">One common task you would want to add to the SharePoint Framework toolchain is to extend the webpack configuration with custom loaders and plugins.</span></span>

## <a name="using-webpack-loaders"></a><span data-ttu-id="fef80-109">Verwenden von Webpack-Ladeprogrammen</span><span class="sxs-lookup"><span data-stu-id="fef80-109">Using webpack loaders</span></span>
<span data-ttu-id="fef80-110">Es kommt häufig vor, dass eine Ressource ohne JavaScript während der Entwicklung importiert und verwendet werden soll. Dies erfolgt in der Regel mit Bildern oder Vorlagen.</span><span class="sxs-lookup"><span data-stu-id="fef80-110">There are many cases where one would like to import and utilize a non-JavaScript resource during development, typically this is done with images or templates.</span></span> <span data-ttu-id="fef80-111">A [Webpack-Ladeprogramm](https://webpack.js.org/loaders/) konvertiert die Ressource in ein Format, das von der JavaScript-Anwendung verwendet werden kann, oder bietet einen einfachen Verweis, den die JavaScript-Anwendung verstehen kann.</span><span class="sxs-lookup"><span data-stu-id="fef80-111">A [Webpack loader](https://webpack.js.org/loaders/) will convert the resource into something that can be utilized by your JavaScript application or provide a simple reference that your JavaScript application can understand.</span></span> <span data-ttu-id="fef80-112">Eine Markdownvorlage zum Beispiel wird möglicherweise kompiliert und in eine Textzeichenfolge konvertiert während eine Bildressource in ein Base64-Inlinebild konvertiert wird oder auf diese mit einer URL verwiesen wird und sie in das `dist`-Verzeichnis für die Bereitstellung kopiert wird.</span><span class="sxs-lookup"><span data-stu-id="fef80-112">For example, a Markdown template may be compiled and converted to a text string, while a image resource may be converted to an inlined Base64 image, or it may be referenced as a URL and copied to your `dist` directory for deployment.</span></span>

<span data-ttu-id="fef80-113">Es gibt eine Reihe von nützlichen Ladeprogrammen, von denen einige bereits durch die standardmäßige SharePoint-Framework-Webpack-Konfiguration verwendet werden, z. B.:</span><span class="sxs-lookup"><span data-stu-id="fef80-113">There are a number of useful loaders, several of which are already used by the standard SharePoint Framework webpack configuration, such as:</span></span>

- <span data-ttu-id="fef80-114">HTML-Ladeprogramm</span><span class="sxs-lookup"><span data-stu-id="fef80-114">html-loader</span></span>
- <span data-ttu-id="fef80-115">JSON-Ladeprogramm</span><span class="sxs-lookup"><span data-stu-id="fef80-115">json-loader</span></span>
- <span data-ttu-id="fef80-116">loader-load-themed-styles</span><span class="sxs-lookup"><span data-stu-id="fef80-116">loader-load-themed-styles</span></span>

<span data-ttu-id="fef80-117">Das Erweitern der Framework-Webpack-Konfiguration mit benutzerdefinierten Ladeprogrammen ist ein einfacher Prozess, der in der [Webpack-Dokumentation](https://webpack.js.org/contribute/writing-a-loader/) beschrieben ist.</span><span class="sxs-lookup"><span data-stu-id="fef80-117">Extending the framework webpack configuration with custom loaders is a straightforward process which is documented [here in the webpack documentation](https://webpack.js.org/contribute/writing-a-loader/).</span></span>

> <span data-ttu-id="fef80-118">Weitere Details zu Ladeprogrammen finden Sie in der [Dokumentation zu Webpack-Ladeprogrammen](https://webpack.js.org/loaders/)</span><span class="sxs-lookup"><span data-stu-id="fef80-118">You can find more details on the loaders from [webpack loaders documentation](https://webpack.js.org/loaders/)</span></span>

## <a name="example-using-the-markdown-loader-package"></a><span data-ttu-id="fef80-119">Beispiel: Verwenden des Pakets mit dem Markdown-Ladeprogramm</span><span class="sxs-lookup"><span data-stu-id="fef80-119">Example: Using the markdown-loader package</span></span>
<span data-ttu-id="fef80-120">Verwenden wir als Beispiel das Paket mit dem [Markdown-Ladeprogramm](https://www.npmjs.com/package/markdown-loader).</span><span class="sxs-lookup"><span data-stu-id="fef80-120">As an example, let's use the [markdown-loader package](https://www.npmjs.com/package/markdown-loader).</span></span>  <span data-ttu-id="fef80-121">Dies ist ein Ladeprogramm zum Verweisen auf eine `.md`-Datei und zur Ausgabe dieser als HTML-Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="fef80-121">As an example, let's use the markdown-loader package.  It's a loader which allows you to reference an `.md` file and output it as HTML string.</span></span>

<span data-ttu-id="fef80-122">Sie können das vollständige Beispiel [hier](https://aka.ms/spfx-extend-Webpack-sample) herunterladen.</span><span class="sxs-lookup"><span data-stu-id="fef80-122">You can download the completed sample [here](https://aka.ms/spfx-extend-Webpack-sample).</span></span>

### <a name="step-1---install-the-package"></a><span data-ttu-id="fef80-123">Schritt 1 – Installieren des Pakets</span><span class="sxs-lookup"><span data-stu-id="fef80-123">Step 1 - Install the package</span></span>
<span data-ttu-id="fef80-124">Wir möchten in unserem Projekt auf das Markdown-Ladeprogramm verweisen.</span><span class="sxs-lookup"><span data-stu-id="fef80-124">Let's reference markdown-loader in our project.</span></span>

```
npm i --save markdown-loader
```

### <a name="step-2---configure-webpack"></a><span data-ttu-id="fef80-125">Schritt 2 – Konfigurieren von Webpack</span><span class="sxs-lookup"><span data-stu-id="fef80-125">Step 2 - Configure Webpack</span></span>
<span data-ttu-id="fef80-126">Nun, da wir das Paket installiert haben, können wir die SharePoint-Framework-Webpack-Konfiguration so konfigurieren, dass sie `markdown-loader` einschließt.</span><span class="sxs-lookup"><span data-stu-id="fef80-126">Now that we have the package installed, lets now configure the SharePoint Framework webpack configuration to include the markdown-loader.</span></span>

<span data-ttu-id="fef80-127">In der [Dokumentation zum Markdown-Ladeprogramm](https://github.com/peerigon/markdown-loader) wird gezeigt, wie die Webpack-Konfiguration erweitert wird, sodass sie das Ladeprogramm einschließt:</span><span class="sxs-lookup"><span data-stu-id="fef80-127">In the [documentation of markdown-loader](https://github.com/peerigon/markdown-loader), it shows how to extend the webpack configuration to include the loader:</span></span>

```JavaScript
{
  module: {
    rules: [
      {
        test: /\.md$/,
        use: [
          {
            loader: 'html-loader'
          },
          {
            loader: 'markdown-loader',
            options: {
              /* options for markdown-loader here */
            }
          }
        ]
      }
    ]
  }
}
```

<span data-ttu-id="fef80-128">Werfen wir nun einen Blick auf diese Konfiguration:</span><span class="sxs-lookup"><span data-stu-id="fef80-128">Let's take a look at what this configuration is doing:</span></span>
  - <span data-ttu-id="fef80-129">Das `rules`-Array in der Webpack-Konfiguration definiert eine Reihe von Dateipfadtests und die Ladeprogramme, die verwendet werden sollen, wenn eine Ressource dem Test entspricht.</span><span class="sxs-lookup"><span data-stu-id="fef80-129">The `rules` array in the Webpack configuration defines a set of file path tests and the loaders that should be used when a resource is found that matches the test.</span></span> <span data-ttu-id="fef80-130">In diesem Fall sucht die `test`-Eigenschaft nach Dateipfaden, die mit `.md` enden.</span><span class="sxs-lookup"><span data-stu-id="fef80-130">In this case, the `test` property checks for file paths that end with `.md`.</span></span>
  - <span data-ttu-id="fef80-131">Das `use`-Array beschreibt eine Liste der Ladeprogramme, die nacheinander auf die Ressource angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="fef80-131">The `use` array describes a list of loaders that are applied sequentially to the resource.</span></span> <span data-ttu-id="fef80-132">Sie werden in der Reihenfolge vom letzten bis zum ersten angewendet.</span><span class="sxs-lookup"><span data-stu-id="fef80-132">They are applied from last to first.</span></span> <span data-ttu-id="fef80-133">In diesem Fall wird als erstes Ladeprogramm `markdown-loader` und als letztes Ladeprogramm `html-loader` angewendet.</span><span class="sxs-lookup"><span data-stu-id="fef80-133">In this case, the first loader to be applied will be `markdown-loader` and the last loader to be applied will be `html-loader`.</span></span>
  - <span data-ttu-id="fef80-134">Wenn mehrere Ladeprogramme angegeben sind, wird das Ergebnis der einzelnen Ladeprogramme an das nächste Ladeprogramm mittels Pipe übergeben.</span><span class="sxs-lookup"><span data-stu-id="fef80-134">When multiple loaders are specified, the result of each loader is piped to the next.</span></span>

<span data-ttu-id="fef80-135">Wir verwenden diese Informationen für die Konfiguration in unserem Projekt.</span><span class="sxs-lookup"><span data-stu-id="fef80-135">We will use this information to configure it in our project.</span></span>

<span data-ttu-id="fef80-136">Um dieses benutzerdefinierte Ladeprogramm zur SharePoint-Framework-Webpack-Konfiguration hinzuzufügen, muss die Buildaufgabe zur Konfiguration von Webpack angewiesen werden.</span><span class="sxs-lookup"><span data-stu-id="fef80-136">In order to add this custom loader into the SharePoint Framework Webpack configuration, we will need to instruct the build task to configure Webpack.</span></span> <span data-ttu-id="fef80-137">Die Buildaufgaben werden in der Gulp-Datei `gulpfile.js` definiert, die sich im Stammverzeichnis des Projekts befindet.</span><span class="sxs-lookup"><span data-stu-id="fef80-137">The build tasks are defined in the gulp file - `gulpfile.js` - which is located at the root of your project.</span></span>

<span data-ttu-id="fef80-138">Bearbeiten Sie `gulpfile.js` und fügen Sie folgenden Code direkt vor `build.initialize(gulp);` ein:</span><span class="sxs-lookup"><span data-stu-id="fef80-138">Edit the `gulpfile.js` and add the following code right before `build.initialize(gulp);`:</span></span>

```JavaScript
build.configureWebpack.mergeConfig({
  additionalConfiguration: (generatedConfiguration) => {
    generatedConfiguration.module.rules.push(
      {
        test: /\.md$/,
        use: [
          {
            loader: 'html-loader'
          },
          {
            loader: 'markdown-loader'
          }
        ]
      }
    );

    return generatedConfiguration;
  }
});
```

<span data-ttu-id="fef80-139">Im Folgenden gehen wir die Schritte durch, die mit diesem Codeausschnitt ausgeführt werden:</span><span class="sxs-lookup"><span data-stu-id="fef80-139">Let's walk through what this code snippet is doing:</span></span>
  - <span data-ttu-id="fef80-140">Wie der Name nahe legt, konfiguriert `ConfigureWebpackTask` (als `build.configureWebpack` instanziiert) das Webpack.</span><span class="sxs-lookup"><span data-stu-id="fef80-140">As its name implies, the `ConfigureWebpackTask` (instantiated as `build.configureWebpack`) configures webpack for us.</span></span> <span data-ttu-id="fef80-141">Es gibt zahlreiche spezielle Konfigurationsschritte, die beim Erstellen von SPFx-Projekten erforderlich sind, es gibt also nichttriviale Logik in dieser Aufgabe.</span><span class="sxs-lookup"><span data-stu-id="fef80-141">There is a lot of special configuration that happens to build SPFx projects, so there is some nontrivial logic in this task.</span></span>
  - <span data-ttu-id="fef80-142">`ConfigureWebpackTask` verwendet eine optionale `additionalConfiguration`-Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="fef80-142">The `ConfigureWebpackTask` takes an optional `additionalConfiguration` property.</span></span> <span data-ttu-id="fef80-143">Diese Eigenschaft soll auf eine Funktion festgelegt werden, die die generierte Konfiguration verwendet, unsere Änderungen an dieser vornimmt und anschließend die aktualisierte Konfiguration zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="fef80-143">We want to set this property to a function which takes the generated configuration, makes our modifications to it, and then returns the updated configuration.</span></span> <span data-ttu-id="fef80-144">**Beachten Sie, dass diese Funktion eine Webpack-Konfiguration an die Toolkette zurückgeben muss, andernfalls wird Webpack nicht ordnungsgemäß konfiguriert.**</span><span class="sxs-lookup"><span data-stu-id="fef80-144">**Note that this function must return a Webpack configuration to the toolchain, otherwise Webpack will not be configured correctly.**</span></span>
  - <span data-ttu-id="fef80-145">Übergeben Sie im Text der Funktion, die auf `additionalConfiguration` festgelegt wurde, einfach eine neue Regel an den vorhandenen Satz von Regeln in der Konfiguration.</span><span class="sxs-lookup"><span data-stu-id="fef80-145">Inside the body of the function that we set to `additionalConfiguration`, simply push a new rule onto the existing set of rules in the configuration.</span></span> <span data-ttu-id="fef80-146">Beachten Sie, dass diese neue Regel dem Beispiel in dem Konfigurationsausschnitt oben im **Schritt 2** ähnelt.</span><span class="sxs-lookup"><span data-stu-id="fef80-146">Notice that this new rule is very similar to example in the configuration snippet at the top of **Step 2**.</span></span>

> <span data-ttu-id="fef80-147">Zwar können Sie mit diesem Ansatz die standardmäßige Webpack-Konfiguration der Toolkette vollständig ersetzen, doch wird dies (sofern nicht anders in der Dokumentation angegeben) nicht empfohlen, wenn Sie von maximaler Leistung und Optimierung profitieren möchten.</span><span class="sxs-lookup"><span data-stu-id="fef80-147">While you are able to completely replace the toolchain's default webpack configuration using this approach, to get the maximum benefit with performance and optimization, it is not recommended to do so unless stated otherwise in the documentation.</span></span>

### <a name="step-3---update-your-code"></a><span data-ttu-id="fef80-148">Schritt 3 – Aktualisieren des Code</span><span class="sxs-lookup"><span data-stu-id="fef80-148">Step 3 - Update your code</span></span>
<span data-ttu-id="fef80-149">Nun, da wir das Ladeprogramm konfiguriert haben, können wir den Code aktualisieren und einige Dateien hinzufügen, um das Szenario zu testen.</span><span class="sxs-lookup"><span data-stu-id="fef80-149">Now that we have configured the loader, lets update our code and add few files to test the scenario.</span></span>

<span data-ttu-id="fef80-150">Erstellen Sie die Datei `my-markdown.md` im Verzeichnis `src` des Projektordners mit etwas Markdown-Text darin.</span><span class="sxs-lookup"><span data-stu-id="fef80-150">Create a file `my-markdown.md` in the `src` directory of your project folder with some Markdown text in it.</span></span>

```md
#Hello Markdown

*Markdown* is a simple markup format to write content.

You can also format text as **bold** or *italics* or ***bold italics***
```

<span data-ttu-id="fef80-151">Wenn Sie das Projekt erstellen, konvertiert das Webpack-Markdown-Ladeprogramm den Markdown-Text in eine HTML-Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="fef80-151">When you build the project, the Webpack markdown-loader will convert this markdown text to a HTML string.</span></span> <span data-ttu-id="fef80-152">Um diese HTML-Zeichenfolge in einer Ihrer `*.ts`-Quelldateien zu verwenden, fügen Sie die folgende Zeile `require()` nach dem Importieren oben in der Datei hinzu. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="fef80-152">When you build the project, the webpack markdown-loader will convert this markdown text to a HTML string. To use this HTML string in any of your source `*.ts` files, add the following `require()` line at the top of the file after your imports, for example:</span></span>


```TypeScript
const markdownString: string = require<string>('./../../../../src/readme.md');
```

<span data-ttu-id="fef80-153">Webpack sucht standardmäßig im `lib`-Ordner nach der Datei. `.md`-Dateien werden jedoch nicht standardmäßig in den `lib`-Ordner kopiert. Dies bedeutet, dass ein ziemlich langer relativer Pfad erstellt werden muss.</span><span class="sxs-lookup"><span data-stu-id="fef80-153">Webpack by default will look in the `lib` folder for the file, but by default `.md` files don't get copied to the `lib` folder, meaning we need to create a rather lengthy relative path. We can control this setting by defining a config file to tell the toolchain to copy  files to the lib folder.</span></span> <span data-ttu-id="fef80-154">Diese Einstellung lässt sich durch Definieren einer Konfigurationsdatei steuern, wodurch die Toolkette angewiesen wird, `md`-Dateien in den lib-Ordner zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="fef80-154">We can control this setting by defining a config file to tell the toolchain to copy `md` files to the lib folder.</span></span>

<span data-ttu-id="fef80-155">Erstellen Sie die Datei `copy-static-assets.json` im Verzeichnis `config`. So wird das Buildsystem angewiesen, einige zusätzliche Dateien von `src` zu `lib` zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="fef80-155">Create a file `copy-static-assets.json` in the `config` directory to tell the build system to copy some additional files from `src` to `lib`.</span></span> <span data-ttu-id="fef80-156">Von dieser Buildaufgabe werden Dateien mit Erweiterungen, die von der Webpack-Standardkonfiguration der Toolkette verstanden werden, standardmäßig kopiert (wie z. B. `png` und `json`). Sie muss also nur angewiesen werden, auch `md`-Dateien zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="fef80-156">Create a file  in the  directory to tell the build system to copy some additional files from  to . By default, this build task copies files with extensions that the default toolchain webpack configuration understands (like `png` and `json`), so we just need to tell it to also copy `md` files.</span></span>

```JSON
{
  "includeExtensions": [
    "md"
  ]
}
```

<span data-ttu-id="fef80-157">Anstelle des relativen Pfads können Sie nun den Dateipfad in Ihrer `require`-Anweisung verwenden, z. B.:</span><span class="sxs-lookup"><span data-stu-id="fef80-157">Now instead of using the relative path, you can use the file path in your `require` statement, for example:</span></span>

```TypeScript
const markdownString: string = require<string>('./../../readme.md');
```

<span data-ttu-id="fef80-158">Dann können Sie in Ihrem Code auf diese Zeichenfolge verweisen, z. B.:</span><span class="sxs-lookup"><span data-stu-id="fef80-158">You can then reference this string in your code, for example:</span></span>

``` TypeScript
public render(): void {
  this.domElement.innerHTML = markdownString;
}
```

### <a name="step-4---build-and-test-your-code"></a><span data-ttu-id="fef80-159">Schritt 4: Erstellen und Testen des Codes</span><span class="sxs-lookup"><span data-stu-id="fef80-159">Step 4 - Build and test your code</span></span>
<span data-ttu-id="fef80-160">Führen Sie zum Erstellen und Testen des Codes den folgenden Befehl in einer Konsole im Stammverzeichnis des Projekts aus:</span><span class="sxs-lookup"><span data-stu-id="fef80-160">To build and test your code, execute the following command in a console in the root of your project directory:</span></span>

```
gulp serve
```
