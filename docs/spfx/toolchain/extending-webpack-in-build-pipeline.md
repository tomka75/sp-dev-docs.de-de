<span data-ttu-id="c4bf0-p108">Erstellen Sie die Datei `copy-static-assets.json` im Verzeichnis `config`. So wird das Buildsystem angewiesen, einige zusätzliche Dateien von `src` zu `lib` zu kopieren. Von dieser Buildaufgabe werden Dateien mit Erweiterungen, die von der Webpack-Standardkonfiguration der Toolkette verstanden werden, standardmäßig kopiert (wie z. B. `png` und `json`). Sie muss also nur angewiesen werden, auch `md`-Dateien zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="c4bf0-p108">Create a file `copy-static-assets.json` in the `config` directory to tell the build system to copy some additional files from `src` to `lib`. By default, this build task copies files with extensions that the default toolchain webpack configuration understands (like `png` and `json`), so we just need to tell it to also copy `md` files.</span></span> 

Erstellen Sie die Datei `copy-static-assets.json` im Verzeichnis `config`. So wird das Buildsystem angewiesen, einige zusätzliche Dateien von `src` zu `lib` zu kopieren. Von dieser Buildaufgabe werden Dateien mit Erweiterungen, die von der Webpack-Standardkonfiguration der Toolkette verstanden werden, standardmäßig kopiert (wie z. B. `png` und `json`). Sie muss also nur angewiesen werden, auch `md`-Dateien zu kopieren.

```JSON
{
  "includeExtensions": [
    "md"
  ]
}
```

<span data-ttu-id="c4bf0-144">Anstelle des relativen Pfads können Sie nun den Dateipfad in Ihrer `require`-Anweisung verwenden, z. B.:</span><span class="sxs-lookup"><span data-stu-id="c4bf0-144">Now instead of using the relative path, you can use the file path in your `require` statement, for example:</span></span>

```TypeScript
const strMarkdownString = require("../../readme.md") as string;
```
 
<span data-ttu-id="c4bf0-145">Dann können Sie in Ihrem Code auf diese Zeichenfolge verweisen, z. B.:</span><span class="sxs-lookup"><span data-stu-id="c4bf0-145">You can then reference this string in your code, for example:</span></span>

``` TypeScript
public render(): void {
  this.domElement.innerHTML = strMarkdownString;
}
```

### <a name="step-4---build-and-test-your-code"></a><span data-ttu-id="c4bf0-146">Schritt 4: Erstellen und Testen des Codes</span><span class="sxs-lookup"><span data-stu-id="c4bf0-146">Step 4 - Build and test your code</span></span>
<span data-ttu-id="c4bf0-147">Führen Sie zum Erstellen und Testen des Codes den folgenden Befehl in einer Konsole im Stammverzeichnis des Projekts aus:</span><span class="sxs-lookup"><span data-stu-id="c4bf0-147">To build and test your code, execute the following command in a console in the root of your project directory:</span></span>

```
gulp serve
```