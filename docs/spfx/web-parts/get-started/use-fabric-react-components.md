<span data-ttu-id="72708-p108">Beachten Sie die Verwendung des relativen Pfads mit einer `require`-Anweisung, um Bilder zu laden. Derzeit müssen Sie das Plug-In für den öffentlichen Pfad von webpack verwenden und den relativen Pfad der Datei aus der Quelldatei oder aus dem Quellordner in den `lib`-Ordner eingeben. Dies sollte derselbe Speicherort wie die aktuelle Arbeitsquelle sein.</span><span class="sxs-lookup"><span data-stu-id="72708-p108">Notice the use of relative path with a `require` statement to load images. Currently, you need to use the webpack public path plugin and input the file's relative path from your source file or folder to the `lib` folder. This should be the same as your current working source location.</span></span>

Beachten Sie die Verwendung des relativen Pfads mit einer `require`-Anweisung, um Bilder zu laden. Derzeit müssen Sie das Plug-In für den öffentlichen Pfad von webpack verwenden und den relativen Pfad der Datei aus der Quelldatei oder aus dem Quellordner in den `lib`-Ordner eingeben. Dies sollte derselbe Speicherort wie die aktuelle Arbeitsquelle sein.
    
<span data-ttu-id="72708-152">Öffnen Sie **DocumentCardExampleWebPart.ts** im Ordner **src\webparts\documentCardExample**.</span><span class="sxs-lookup"><span data-stu-id="72708-152">Open **DocumentCardExampleWebPart.ts** from the **src\webparts\documentCardExample** folder.</span></span> 
    
<span data-ttu-id="72708-153">Fügen Sie den folgenden Code am Anfang der Datei hinzu, um das Plug-In für den öffentlichen Pfad von webpack anzufordern.</span><span class="sxs-lookup"><span data-stu-id="72708-153">Add the following code at the top of the file to require the webpack public path plugin.</span></span>
    
```ts
require('set-webpack-public-path!');
```
    
<span data-ttu-id="72708-154">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="72708-154">Save the file.</span></span>

### <a name="copy-the-image-assets"></a><span data-ttu-id="72708-155">Kopieren der Bildanlagen</span><span class="sxs-lookup"><span data-stu-id="72708-155">Copy the image assets</span></span>

<span data-ttu-id="72708-156">Kopieren Sie die folgenden Bilder in den Ordner **src\webparts\documentCardExample**:</span><span class="sxs-lookup"><span data-stu-id="72708-156">Copy the following images to your **src\webparts\documentCardExample** folder:</span></span>

* [<span data-ttu-id="72708-157">avatar-kat.png</span><span class="sxs-lookup"><span data-stu-id="72708-157">avatar-kat.png</span></span>](https://github.com/SharePoint/sp-dev-docs/blob/master/assets/avatar-kat.png)
* [<span data-ttu-id="72708-158">icon-ppt.png</span><span class="sxs-lookup"><span data-stu-id="72708-158">icon-ppt.png</span></span>](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/icon-ppt.png)
* [<span data-ttu-id="72708-159">document-preview.png</span><span class="sxs-lookup"><span data-stu-id="72708-159">document-preview.png</span></span>](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/document-preview.png)

### <a name="preview-the-web-part-in-workbench"></a><span data-ttu-id="72708-160">Anzeigen der Webpart-Vorschau in der Workbench</span><span class="sxs-lookup"><span data-stu-id="72708-160">Preview the web part in workbench</span></span>

<span data-ttu-id="72708-161">Geben Sie in der Konsole Folgendes ein, um das Webpart in der Workbench der Vorschau anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="72708-161">In the console, type the following to preview your web part in workbench:</span></span>
    
```
gulp serve
```
    
<span data-ttu-id="72708-162">Wählen Sie in der Toolbox Ihr `DocumentCardExample`-Webpart aus, das hinzugefügt werden soll:</span><span class="sxs-lookup"><span data-stu-id="72708-162">In the toolbox, select your `DocumentCardExample` web part to add:</span></span>
    
![Abbildung der Fabric-Komponente „DocumentCard“ in einer SharePoint-Workbench](../../../../images/fabric-components-doc-card-view-ex.png)


## <a name="updating-an-existing-project"></a><span data-ttu-id="72708-164">Aktualisieren vorhandener Projekte</span><span class="sxs-lookup"><span data-stu-id="72708-164">Updating an existing project</span></span>

<span data-ttu-id="72708-165">Aktualisieren Sie in der Datei `package.json` Ihres Projekts die Abhängigkeit `@microsoft/sp-build-web` mindestens auf Version 1.0.1, löschen Sie das Verzeichnis `node_modules` Ihres Projekts, und führen Sie den Befehl `npm install` aus.</span><span class="sxs-lookup"><span data-stu-id="72708-165">In your project's `package.json`, update the `@microsoft/sp-build-web` dependency to at least version 1.0.1, delete your project's `node_modules` directory, and run `npm install`.</span></span>
