
# <a name="build-your-first-sharepoint-framework-extension-hello-world-part-1"></a><span data-ttu-id="60a38-101">Erstellen Ihrer ersten SharePoint-Framework-Erweiterung (Hello World, Teil 1)</span><span class="sxs-lookup"><span data-stu-id="60a38-101">Build your first SharePoint Framework Extension (Hello World part 1)</span></span>

><span data-ttu-id="60a38-p101">**Hinweis:** Die SharePoint-Framework-Erweiterungen befinden sich derzeit in der Preview-Phase. Änderungen sind vorbehalten. Die Verwendung von SharePoint-Framework-Erweiterungen in Produktionsumgebungen wird aktuell nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="60a38-p101">**Note:** The SharePoint Framework Extensions are currently in preview and are subject to change. SharePoint Framework Extensions are not currently supported for use in production environments.</span></span>

<span data-ttu-id="60a38-p102">Erweiterungen sind clientseitige Komponenten, die im Kontext einer SharePoint-Seite ausgeführt werden. Sie lassen sich in SharePoint Online bereitstellen und auch mithilfe aktueller JavaScript-Tools und -Bibliotheken erstellen.</span><span class="sxs-lookup"><span data-stu-id="60a38-p102">Extensions are client-side components that run inside the context of a SharePoint page. Extensions can be deployed to SharePoint Online, and you can also use modern JavaScript tools and libraries to build them.</span></span>

<span data-ttu-id="60a38-106">Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=0BeS0HukW24&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV) nachvollziehen:</span><span class="sxs-lookup"><span data-stu-id="60a38-106">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=0BeS0HukW24&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span></span> 

<a href="https://www.youtube.com/watch?v=0BeS0HukW24&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV">
<img src="../../../../images/spfx-ext-youtube-tutorial1.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="create-an-extension-project"></a><span data-ttu-id="60a38-107">Erstellen eines Erweiterungsprojekts</span><span class="sxs-lookup"><span data-stu-id="60a38-107">Create an extension project</span></span>
<span data-ttu-id="60a38-108">Erstellen Sie an einem Speicherort Ihrer Wahl ein neues Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="60a38-108">Create a new project directory in your favorite location.</span></span>

```
md app-extension
```

<span data-ttu-id="60a38-109">Wechseln Sie in das Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="60a38-109">Go to the project directory.</span></span>

```
cd app-extension
```

<span data-ttu-id="60a38-110">Führen Sie den Yeoman-SharePoint-Generator aus, um eine neue HelloWorld-Erweiterung zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="60a38-110">Create a new HelloWorld extension by running the Yeoman SharePoint Generator.</span></span>

```
yo @microsoft/sharepoint
```

<span data-ttu-id="60a38-111">Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="60a38-111">When prompted:</span></span>

* <span data-ttu-id="60a38-112">Übernehmen Sie den Standardwert **app-extension** als Lösungsnamen, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="60a38-112">Accept the default **app-extension** as your solution name and press **Enter**.</span></span>
* <span data-ttu-id="60a38-113">Wählen Sie **Use the current folder (Aktuellen Ordner verwenden)** aus, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="60a38-113">Choose **Use the current folder** and press **Enter**</span></span>
* <span data-ttu-id="60a38-114">Wählen Sie **N**, damit die Erweiterung auf jeder Website explizit installiert werden muss, wenn diese verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="60a38-114">Choose **N** to require extension to be installed on each site explicitly when it's being used</span></span> 
* <span data-ttu-id="60a38-115">Wählen Sie **Extension (Preview)** als den zu erstellenden Typ von clientseitiger Komponente aus.</span><span class="sxs-lookup"><span data-stu-id="60a38-115">Choose **Extension (Preview)** as the client-side component type to be created.</span></span> 
* <span data-ttu-id="60a38-116">Wählen Sie **Application Customizer (Preview)** als den zu erstellenden Erweiterungstyp aus.</span><span class="sxs-lookup"><span data-stu-id="60a38-116">Choose **Application Customizer (Preview)** as the extension type to be created.</span></span>

<span data-ttu-id="60a38-117">Über die nächsten Eingabeaufforderungen werden spezifische Informationen zu der Erweiterung abgefragt:</span><span class="sxs-lookup"><span data-stu-id="60a38-117">The next set of prompts will ask for specific information about your extension:</span></span>

* <span data-ttu-id="60a38-118">Übernehmen Sie den Standardwert **HelloWorld** als Namen für Ihre Erweiterung, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="60a38-118">Accept the default **HelloWorld** as your extension name and press **Enter**.</span></span>
* <span data-ttu-id="60a38-119">Übernehmen Sie den Standardwert **HelloWorld description** als Beschreibung Ihrer Erweiterung, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="60a38-119">Accept the default **HelloWorld description** as your extension description and press **Enter**.</span></span>

![Yeoman-SharePoint-Generator mit Eingabeaufforderungen zur Erstellung einer Erweiterungslösung](../../../../images/ext-yeoman-app-prompts.png)

> <span data-ttu-id="60a38-p103">Beachten Sie, dass zu lange Namen für die Erweiterung zu Problemen führen können. Bereitgestellte Einträge werden verwendet, um einen Alias-Eintrag für die Json-Datei des Anwendungsanpassermanifests zu generieren. Wenn der Alias mehr als 40 Zeichen enthält, führt dies zu einer Ausnahme, wenn Sie versuchen, die Erweiterung mit `gulp serve --nobrowser` zu bedienen. Sie können dieses Problem auch später lösen, indem Sie den Alias-Eintrag aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="60a38-p103">Notice that if you use too long naming for the extension, that can cause issues. Provided entries are used to generate alias entry for the application customizer manifest json file. If alias is longer than 40 characters, you will have an exception when you are trying to serve the extension using `gulp serve --nobrowser`. You can solve this by updating the alias entry also afterwards.</span></span>

<span data-ttu-id="60a38-p104">An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien sowie die **HelloWorld**-Erweiterung. Das kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="60a38-p104">At this point, Yeoman will install the required dependencies and scaffold the solution files along with the **HelloWorld** extension. This might take a few minutes.</span></span> 

<span data-ttu-id="60a38-127">Nach Abschluss der Gerüsterstellung sollte folgende Erfolgsmeldung angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="60a38-127">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

![Erfolgreiche Erstellung eines Gerüsts für die clientseitige SharePoint-Lösung](../../../../images/ext-yeoman-app-complete.png)

<span data-ttu-id="60a38-129">Details zur Behebung etwaiger Fehler finden Sie unter [Known issues](../basics/known-issues).</span><span class="sxs-lookup"><span data-stu-id="60a38-129">For information about troubleshooting any errors, see [Known issues](../basics/known-issues).</span></span>

<span data-ttu-id="60a38-130">Geben Sie nach der Erstellung des Lösungsgerüsts Folgendes in die Konsole ein, um Visual Studio Code zu starten:</span><span class="sxs-lookup"><span data-stu-id="60a38-130">Once solution scaffolding is completed, type the following into the console to start Visual Studio Code.</span></span>

```
code .
```

> <span data-ttu-id="60a38-131">Beachten Sie: Da die clientseitige SharePoint-Lösung auf HTML/TypeScript basiert, können Sie zur Erstellung Ihrer Erweiterung jeden Code-Editor verwenden, der clientseitige Entwicklung unterstützt.</span><span class="sxs-lookup"><span data-stu-id="60a38-131">Notice that because the SharePoint client-side solution is HTML/TypeScript based, you can use any code editor that supports client-side development to build your extension.</span></span>

<span data-ttu-id="60a38-p105">Wie Sie sehen, entspricht die Standardlösungsstruktur der Lösungsstruktur clientseitiger Webparts. Hierbei handelt es sich um die grundlegende SharePoint-Framework-Lösungsstruktur, die für alle Lösungstypen vergleichbare Konfigurationsoptionen bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="60a38-p105">Notice how the default solution structure is like the solution structure of client-side web parts. This is the basic SharePoint Framework solution structure, with similar configuration options across all solution types.</span></span>

![SharePoint-Framework-Lösung nach der Erstellung des anfänglichen Gerüsts](../../../../images/ext-app-vscode-solution-structure.png)

<span data-ttu-id="60a38-135">Öffnen Sie **HelloWorldApplicationCustomizer.manifest.json** im Ordner „src\extensions\helloWorld“.</span><span class="sxs-lookup"><span data-stu-id="60a38-135">Open **HelloWorldApplicationCustomizer.manifest.json** at the src\extensions\helloWorld folder.</span></span>

<span data-ttu-id="60a38-p106">In dieser Datei sind der Erweiterungstyp und ein eindeutiger Bezeichner **„id“** für die Erweiterung definiert. Sie benötigen diesen eindeutigen Bezeichner später, um die Erweiterung zu debuggen und in SharePoint bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="60a38-p106">This file defines your extension type and a unique identifier **“id”** for your extension. You’ll need this unique identifier later when debugging and deploying your extension to SharePoint.</span></span>

![Json-Inhalt des Anwendungsanpasser-Manifests](../../../../images/ext-app-vscode-manifest.png)

## <a name="coding-your-application-customizer"></a><span data-ttu-id="60a38-139">Codieren des Application Customizer</span><span class="sxs-lookup"><span data-stu-id="60a38-139">Coding your Application Customizer</span></span> 
<span data-ttu-id="60a38-140">Öffnen Sie die Datei **HelloWorldApplicationCustomizer.ts** im Ordner **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="60a38-140">Open the **HelloWorldApplicationCustomizer.ts** file in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="60a38-141">Beachten Sie, dass die Basisklasse für den Application Customizer aus dem **sp-application-base**-Paket importiert wird, das den SharePoint-Framework-Code enthält, der für den Application Customizer erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="60a38-141">Notice that base class for the Application Customizer is imported from the **sp-application-base** package, which contains SharePoint framework code required by the Application Customizer.</span></span>

![Import-Anweisung für BaseApplicationCustomizer von @microsoft/sp-application-base](../../../../images/ext-app-vscode-app-base.png)

<span data-ttu-id="60a38-143">Die Logik für den Application Customizer ist in der **onInit**-Methode enthalten</span><span class="sxs-lookup"><span data-stu-id="60a38-143">The logic for your Application Customizer is contained in the two methods onInit and onRender.</span></span>

- <span data-ttu-id="60a38-p107">**onInit()** wird aufgerufen, wenn die clientseitige Erweiterung das erste Mal auf der Seite aktiviert wird. Dieses Ereignis tritt auf, nachdem ```this.context``` und ```this.properties``` zugeordnet wurden. Wie bei Webparts gibt ```onInit()``` eine Zusage zurück, die Sie zum Ausführen von asynchronen Vorgängen verwenden können.</span><span class="sxs-lookup"><span data-stu-id="60a38-p107">**onInit()** is called when the client-side extension is first activated on the page. This event occurs after ```this.context``` and ```this.properties``` are assigned. As with web parts, ```onInit()``` returns a promise that you can use to perform asynchronous operations.</span></span>

> <span data-ttu-id="60a38-p108">Beachten Sie: Der Klassenkonstruktor wird in einer frühen Phase aufgerufen, wenn ```this.context``` und ```this.properties``` noch nicht definiert sind. Das Einschließen benutzerdefinierter Initiierungslogik wird an dieser Stelle nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="60a38-p108">Notice. The class constructor is called at an early stage, when ```this.context``` and ```this.properties``` are undefined. We do not support including custom initiation logic here.</span></span>

<span data-ttu-id="60a38-p109">Im Folgenden sind die Inhalte von **onInit()** in der Standardlösung aufgelistet. Die Standardlösung schreibt einfach ein Protokoll in das Dev Dashboard und zeigt dann beim Rendern der Seite eine einfache JavaScript-Warnung an.</span><span class="sxs-lookup"><span data-stu-id="60a38-p109">Below are the contents of **onInit()** and onRender() in the default solution. This default solution simply writes a log to the Dev Dashboard, and then displays a simple JavaScript alert when the page renders.</span></span>

![Standardmäßige onInit-Methode im code](../../../../images/ext-app-vscode-methods.png)

>  <span data-ttu-id="60a38-p110">Wenn die Anpassung Ihrer Anwendung die JSON-Eingabe ClientSideComponentProperties verwendet, wird sie in das Objekt BaseExtension.properties deserialisiert. Sie können eine Benutzeroberfläche definieren, um sie zu beschreiben. Die Standardvorlage sucht nach einer Eigenschaft mit dem Namen testMessage und gibt sie, wenn sie bereitgestellt wird, in einer Warnmeldung aus.</span><span class="sxs-lookup"><span data-stu-id="60a38-p110">If your application customizer uses the ClientSideComponentProperties JSON input, it will be deserialized into the BaseExtension.properties object. You can define an interface to describe it. The default template is looking for a property called testMessage, and if it's provided, outputting it in an alert message.</span></span>

## <a name="debugging-your-application-customizer-using-gulp-serve-and-query-string-parameters"></a><span data-ttu-id="60a38-156">Debuggen Ihres Application Customizer mit gulp serve- und Abfragezeichenfolgen-Parametern</span><span class="sxs-lookup"><span data-stu-id="60a38-156">Debugging your Application Customizer using gulp serve and query string parameters</span></span>
<span data-ttu-id="60a38-p111">SharePoint-Framework-Erweiterungen lassen sich aktuell nicht mithilfe der lokalen Workbench testen. Sie müssen direkt auf einer aktiven SharePoint Online-Website getestet und entwickelt werden. Dazu ist es jedoch nicht nötig, Ihre Anpassung im App-Katalog bereitzustellen. Dadurch bleibt das Debuggen einfach und effizient.</span><span class="sxs-lookup"><span data-stu-id="60a38-p111">SharePoint Framework extensions cannot currently be tested using the local workbench, so you'll need to test and develop them directly against a live SharePoint Online site. You do not, however, need to deploy your customization to the app catalog to do this, which keeps the debugging experience simple and efficient.</span></span> 

<span data-ttu-id="60a38-159">Zunächst führen Sie den folgenden Befehl aus, um den Code zu kompilieren und die kompilierten Dateien auf Ihrem lokalen Computer zu hosten:</span><span class="sxs-lookup"><span data-stu-id="60a38-159">First, compile your code and host the compiled files from your local machine by running this command:</span></span>
```
gulp serve --nobrowser
```

><span data-ttu-id="60a38-p112">**Hinweis:** Wenn Sie das SPFx-Entwicklerzertifikat noch nicht installiert haben, meldet Workbench, dass das Laden von Skripts von „localhost“ nicht konfiguriert ist. Halten Sie den aktuell ausgeführten Prozess im Konsolenfenster an, und führen Sie in der Konsole des Projektverzeichnisses den Befehl `gulp trust-dev-cert` aus, um das Entwicklerzertifikat zu installieren, bevor Sie den `gulp serve --nobrowser`-Befehl erneut ausführen.</span><span class="sxs-lookup"><span data-stu-id="60a38-p112">**Note:** If you do not have the SPFx developer certificate installed, then Workbench will notify you that it is configured not to load scripts from localhost. Stop currently running process in the console window, execute `gulp trust-dev-cert` command in your project directory console to install the developer certificate before running `gulp serve --nobrowser`command again.</span></span>

<span data-ttu-id="60a38-162">Die Option ```--nobrowser``` verwenden wir, weil Erweiterungen derzeit nicht lokal debuggt werden können und daher keine Notwendigkeit besteht, die lokale Workbench zu starten.</span><span class="sxs-lookup"><span data-stu-id="60a38-162">Notice that we used the ```--nobrowser``` option, since there's no value in launching the local workbench since you currently cannot debug extensions locally.</span></span>

<span data-ttu-id="60a38-163">Sobald der Code ohne Fehler kompiliert wurde, wird das resultierende Manifest von http://localhost:4321 ausgeliefert.</span><span class="sxs-lookup"><span data-stu-id="60a38-163">Once it compiles the code without errors, it will serve the resulting manifest from http://localhost:4321.</span></span>

![gulp serve](../../../../images/ext-app-gulp-serve.png)

<span data-ttu-id="60a38-p113">Um die Erweiterung zu testen, navigieren Sie zu einer modernen Seite mit Listenansicht in Ihrer SharePoint-Umgebung und fügen die folgenden Zeichenfolgen-Abfrageparameter an die URL an. Beachten Sie, dass Sie die ID aktualisieren müssen, damit diese Ihrer Erweiterungs-ID entspricht, die in **HelloWorldApplicationCustomizer.manifest.json** verfügbar ist:</span><span class="sxs-lookup"><span data-stu-id="60a38-p113">To test your extension, navigate to a modern list view page in your SharePoint environment and append the following query string parameters to the URL. Notice that you will need to update the id to match your own extension identifier available from the **HelloWorldApplicationCustomizer.manifest.json** file:</span></span>
```
?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"testMessage":"Hello as property!"}}}
```

<span data-ttu-id="60a38-167">Weitere Details zu den URL-Abfrageparametern:</span><span class="sxs-lookup"><span data-stu-id="60a38-167">More detail about the URL query parameters:</span></span>

* <span data-ttu-id="60a38-p114">**loadSPFX=true:** Dieser Parameter stellt sicher, dass das SharePoint-Framework auf der Seite geladen wird. Aus Leistungsgründen wird das Framework normalerweise erst geladen, wenn mindestens eine Erweiterung registriert ist. Da aktuell noch keine Komponenten registriert sind, müssen Sie das Framework explizit laden.</span><span class="sxs-lookup"><span data-stu-id="60a38-p114">**loadSPFX=true:**  ensures that the SharePoint Framework is loaded on the page. For performance reasons, the framework is not normally loaded unless at least one extension is registered. Since no components are registered yet, we must explicitly load the framework.</span></span>

* <span data-ttu-id="60a38-p115">**debugManifestsFile:** Dieser Parameter gibt an, dass lokal ausgelieferte SPFx-Komponenten geladen werden sollen. Normalerweise sucht das Ladeprogramm nur an zwei Orten nach Komponenten: im App-Katalog (nach Komponenten der bereitgestellten Lösung) und auf dem SharePoint-Manifestserver (nach den Systembibliotheken).</span><span class="sxs-lookup"><span data-stu-id="60a38-p115">**debugManifestsFile:**  specifies that we want to load SPFx components that are being locally served. Normally the loader only looks for components in the App Catalog (for your deployed solution) and the SharePoint manifest server (for the system libraries).</span></span>

* <span data-ttu-id="60a38-p116">**customActions:** Dieser URL-Abfrageparameter simuliert eine benutzerdefinierte Aktion. Wenn wir diese Komponente später in diesem Kurs tatsächlich bereitstellen und auf einer Website registrieren, erstellen wir dieses CustomAction-Objekt tatsächlich und beschreiben alle anderen Eigenschaften, die Sie dafür festlegen können.</span><span class="sxs-lookup"><span data-stu-id="60a38-p116">**customActions:**  this URL query parameter simulates a custom action. When we actually deploy and register this component in a site later in this lab, we’ll create this CustomAction object for real and describe all the different properties you can set on it.</span></span> 
    * <span data-ttu-id="60a38-p117">**Key:** Verwenden Sie die GUID der Erweiterung als Schlüssel, der der benutzerdefinierten Aktion zuzuordnen ist. Diese muss mit dem ID-Wert der Erweiterung übereinstimmen, die in „manifest.json“ der Erweiterung verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="60a38-p117">**Key:** use the Guid of the extension as the key to associate with the custom action. This has to match on the id value of your extension available from the extension manifest.json.</span></span>
    * <span data-ttu-id="60a38-177">**Location:** Der Typ der benutzerdefinierten Aktion, verwenden Sie "ClientSideExtension.ApplicationCustomizer" für die Application Customizer-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="60a38-177">**Location:** the type of custom action, use "ClientSideExtension.ApplicationCustomizer" for the Application Customizer extension</span></span>
    * <span data-ttu-id="60a38-p118">**Properties:** Ein optionales JSON-Objekt mit Eigenschaften, die über das Mitglied this.properties zur Verfügung stehen. In diesem „HelloWorld“-Beispiel definiert es eine „testMessage“-Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="60a38-p118">**Properties:** an optional JSON object containing properties that will be available via the this.properties member. In this HelloWorld example, it defined a ‘testMessage’ property.</span></span>


<span data-ttu-id="60a38-p119">Navigieren Sie zu einer vordefinierten modernen Liste in SharePoint Online. Dies kann für die anfänglichen Tests eine Liste oder eine Bibliothek sein. Application Customizers werden ebenfalls auf modernen Seiten und auf der Seite „Websiteinhalte“ unterstützt.</span><span class="sxs-lookup"><span data-stu-id="60a38-p119">Navigate to a out of the box modern list in SharePoint Online. This can be a list or a library for the initial testing. Application customizers are also supported in modern pages and on the Site Contents page.</span></span> 

<span data-ttu-id="60a38-p120">Erweitern Sie die URL mit den oben definierten zusätzlichen Abfrageparametern. Beachten Sie, dass Sie die GUID entsprechend der ID Ihres benutzerdefinierten Application Customizers aktualisieren müssen, die in **HelloWorldApplicationCustomizer.manifest.json** im Ordner „src\extensions\helloWorld“ verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="60a38-p120">Extend the URL with the additional query parameters defined above. Notice that you'll need to update the GUID to match the ID of your custom Application Customizer available from  **HelloWorldApplicationCustomizer.manifest.json** at the src\extensions\helloWorld folder.</span></span> 

<span data-ttu-id="60a38-185">Die vollständige URL sollte abhängig von der URL Ihres Mandanten in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="60a38-185">The full URL should look similar to the following depending on your tenant URL:</span></span>

```
contoso.sharepoint.com/Lists/Contoso/AllItems.aspx?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"testMessage":"Hello as property!"}}}
```

![Abfragen des Debugging-Manifests für die Seite zulassen](../../../../images/ext-app-debug-manifest-message.png)

<span data-ttu-id="60a38-187">Klicken Sie auf die Schaltfläche zum **Laden von Debugging-Skripts**, um weiter Skripts von Ihrem lokalen Host zu laden.</span><span class="sxs-lookup"><span data-stu-id="60a38-187">Click the "**Load debug scripts**" button to continue loading scripts from your local host.</span></span>

<span data-ttu-id="60a38-188">Die Warnmeldung sollte nun auf Ihrer Seite angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="60a38-188">You should now see the alert message on your page.</span></span>

![Abfragen des Debugging-Manifests für die Seite zulassen](../../../../images/ext-app-alert-sp-page.png)

<span data-ttu-id="60a38-p121">Diese Warnung wird von der SharePoint-Framework-Erweiterung ausgelöst. Da wir die testMessage-Eigenschaft als Teil der Debug-Abfrageparameter bereitgestellt haben, ist sie in der Warnmeldung enthalten. Sie können Ihre Erweiterungsinstanzen auf Grundlage der Clientkomponenteneigenschaften konfigurieren, die für die Instanz auch im Laufzeitmodus übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="60a38-p121">This alert is thrown by your SharePoint Framework Extension. Notice also that since we provided the testMessage property as part of the debug query parameters, it's included in the alert message. You can configure your extension instances based on the client component properties, which are passed for the instance also in runtime mode.</span></span> 

> <span data-ttu-id="60a38-p122">Wenn Sie Probleme beim Debuggen haben, überprüfen Sie die URL-Abfrageparameter für die Abfrage. Einige Browser codieren in der Regel die Parameter, und in einigen Fällen wirkt sich das auf das Verhalten aus.</span><span class="sxs-lookup"><span data-stu-id="60a38-p122">If you are having challenges in getting debugging to work, double check the URL query parameters used for the query. Some browsers tend to encode the parameters and in some scenarios this will impact the behavior.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="60a38-195">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="60a38-195">Next steps</span></span>
<span data-ttu-id="60a38-p123">Herzlichen Glückwunsch! Ihre erste SharePoint-Framework-Erweiterung läuft. Jetzt können Sie die Erweiterung weiter ausbauen. Wie das funktioniert, erfahren Sie im nächsten Thema, [Verwenden von Seitenplatzhaltern aus dem Anwendungsanpasser (Hello World, Teil 2)](./using-page-placeholder-with-extensions.md). Dort verwenden Sie dasselbe Projekt und nutzen spezifische Inhaltsplatzhalter für die Änderung der Benutzeroberfläche von SharePoint. Beachten Sie, dass der Befehl ```gulp serve``` immer noch im Konsolenfenster ausgeführt wird (oder in Visual Studio Code, falls Sie den Editor verwenden). Sie können ihn einfach weiterlaufen lassen und zum nächsten Artikel wechseln.</span><span class="sxs-lookup"><span data-stu-id="60a38-p123">Congratulations on getting your first SharePoint Framework Extension running! Now that your extension is running, you can continue building out your extension in the next topic, [Using page placeholders from Application Customizer (Hello World part 2)](./using-page-placeholder-with-extensions.md). You will use the same project and take advantage of specific content placeholders for modifying the UI of SharePoint. Notice that the ```gulp serve``` command is still running in your console window (or in Visual Studio Code if you are using the editor). You can continue to let it run while you go to the next article.</span></span>
