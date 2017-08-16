# <a name="build-your-first-sharepoint-client-side-web-part-hello-world-part-1"></a><span data-ttu-id="b392b-101">Erstellen Ihres ersten clientseitigen SharePoint-Webparts („Hello World“ Teil 1)</span><span class="sxs-lookup"><span data-stu-id="b392b-101">Build your first SharePoint client-side web part (Hello World part 1)</span></span>

<span data-ttu-id="b392b-p101">Clientseitige Webparts sind clientseitige Komponenten, die im Kontext einer SharePoint-Website ausgeführt werden. Clientseitige Webparts lassen sich auf SharePoint Online bereitstellen und auch mithilfe aktueller JavaScript-Tools und -Bibliotheken erstellen.</span><span class="sxs-lookup"><span data-stu-id="b392b-p101">Client-side web parts are client-side components that run inside the context of a SharePoint page. Client-side web parts can be deployed to SharePoint Online, and you can also use modern JavaScript tools and libraries to build them.</span></span>

<span data-ttu-id="b392b-104">Clientseitige Webparts unterstützen:</span><span class="sxs-lookup"><span data-stu-id="b392b-104">Client-side web parts support:</span></span>

* <span data-ttu-id="b392b-105">Die Erstellung mit HTML und JavaScript</span><span class="sxs-lookup"><span data-stu-id="b392b-105">Building with HTML and JavaScript.</span></span>
* <span data-ttu-id="b392b-106">SharePoint-Onlineumgebungen und lokale SharePoint-Umgebungen</span><span class="sxs-lookup"><span data-stu-id="b392b-106">Both SharePoint online and on-premises environments.</span></span>

><span data-ttu-id="b392b-107">**Hinweis:** Bevor Sie die Schritte in diesem Artikel durchführen, müssen Sie [Ihre Entwicklungsumgebung einrichten](../../set-up-your-development-environment).</span><span class="sxs-lookup"><span data-stu-id="b392b-107">**Note:** Before following the steps in this article, be sure to [Set up your development environment](../../set-up-your-development-environment).</span></span>

<span data-ttu-id="b392b-108">Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=QbDtsMg88Js&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq) nachvollziehen:</span><span class="sxs-lookup"><span data-stu-id="b392b-108">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=QbDtsMg88Js&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span></span> 

<a href="https://www.youtube.com/watch?v=QbDtsMg88Js&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq">
<img src="../../../../images/spfx-youtube-tutorial1.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="create-a-new-web-part-project"></a><span data-ttu-id="b392b-109">Erstellen eines neuen Webpart-Projekts</span><span class="sxs-lookup"><span data-stu-id="b392b-109">Create a new web part project</span></span>
<span data-ttu-id="b392b-110">Erstellen Sie an einem Speicherort Ihrer Wahl ein neues Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="b392b-110">Create a new project directory in your favorite location.</span></span>
    
```
md helloworld-webpart
```

<span data-ttu-id="b392b-111">Wechseln Sie in das Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="b392b-111">Go to the project directory.</span></span>

```
cd helloworld-webpart
```

<span data-ttu-id="b392b-112">Führen Sie den Yeoman-SharePoint-Generator aus, um ein neues HelloWorld-Webpart zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="b392b-112">Create a new HelloWorld web part by running the Yeoman SharePoint Generator.</span></span>

```
yo @microsoft/sharepoint
```
    
<span data-ttu-id="b392b-113">Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="b392b-113">When prompted:</span></span>

* <span data-ttu-id="b392b-114">Akzeptieren Sie den Standardnamen **helloworld-webpart** als Lösungsnamen, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="b392b-114">Accept the default **helloworld-webpart** as your solution name and choose **Enter**.</span></span>
* <span data-ttu-id="b392b-115">Wählen Sie als Speicherort für die Dateien die Option **Use the current folder** aus.</span><span class="sxs-lookup"><span data-stu-id="b392b-115">Select **Use the current folder** for where to place the files.</span></span>

<span data-ttu-id="b392b-116">Über die nächsten Eingabeaufforderungen werden spezifische Informationen zum Webpart abgefragt:</span><span class="sxs-lookup"><span data-stu-id="b392b-116">The next set of prompts will ask for specific information about your web part:</span></span>

* <span data-ttu-id="b392b-117">Akzeptieren Sie die Standardeinstellung **No javaScript web framework** als das zu verwendende Framework, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="b392b-117">Accept the default **No javascript web framework** as the framework you would like to use and choose **Enter**.</span></span>
* <span data-ttu-id="b392b-118">Akzeptieren Sie den Standardnamen **HelloWorld** als Namen für Ihr Webpart, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="b392b-118">Accept the default **HelloWorld** as your web part name and choose **Enter**.</span></span>
* <span data-ttu-id="b392b-119">Akzeptieren Sie die Standardbeschreibung **HelloWorld description** als Beschreibung für Ihr Webpart, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="b392b-119">Accept the default **HelloWorld description** as your web part description and choose **Enter**.</span></span>

![Eingabeaufforderungen im Yeoman-SharePoint-Generator zur Erstellung einer clientseitigen Webpart-Lösung](../../../../images/yeoman-sp-prompts.png)

<span data-ttu-id="b392b-p102">An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien sowie das **HelloWorld**-Webpart. Das kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="b392b-p102">At this point, Yeoman will install the required dependencies and scaffold the solution files along with the **HelloWorld** web part. This might take a few minutes.</span></span> 

<span data-ttu-id="b392b-123">Nach Abschluss der Gerüsterstellung sollte folgende Erfolgsmeldung angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="b392b-123">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

![Erfolgreiche Erstellung eines Gerüsts für die clientseitige SharePoint-Lösung](../../../../images/yeoman-sp-complete.png)

<span data-ttu-id="b392b-125">Details zur Behebung etwaiger Fehler finden Sie unter [Known issues](../basics/known-issues).</span><span class="sxs-lookup"><span data-stu-id="b392b-125">For information about troubleshooting any errors, see [Known issues](../basics/known-issues).</span></span>

### <a name="using-your-favorite-code-editor"></a><span data-ttu-id="b392b-126">Verwenden Ihres bevorzugten Code-Editors</span><span class="sxs-lookup"><span data-stu-id="b392b-126">Using your favorite Code Editor</span></span>
<span data-ttu-id="b392b-127">Da die clientseitige SharePoint-Lösung auf HTML/TypeScript basiert, können Sie zur Erstellung Ihres Webparts alle Code-Editoren verwenden, die clientseitige Entwicklung unterstützen, beispielsweise:</span><span class="sxs-lookup"><span data-stu-id="b392b-127">Because the SharePoint client-side solution is HTML/TypeScript based, you can use any code editor that supports client-side development to build your web part, such as:</span></span>

* [<span data-ttu-id="b392b-128">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b392b-128">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* [<span data-ttu-id="b392b-129">Atom</span><span class="sxs-lookup"><span data-stu-id="b392b-129">Atom</span></span>](https://atom.io)
* [<span data-ttu-id="b392b-130">WebStorm</span><span class="sxs-lookup"><span data-stu-id="b392b-130">Webstorm</span></span>](https://www.jetbrains.com/webstorm)

<span data-ttu-id="b392b-p103">In der SharePoint Framework-Dokumentation wird Visual Studio Code in den Anleitungen und Beispielen verwendet. Visual Studio Code ist ein einfacher und dennoch leistungsfähiger Quellcode-Editor von Microsoft, der auf dem Desktop ausgeführt wird und für Windows, Mac und Linux verfügbar ist. Er verfügt über integrierte Unterstützung für JavaScript, TypeScript und Node.js und bietet ein reichhaltiges Ökosystem von Erweiterungen für andere Sprachen (wie C++, C#, Python, PHP) und Laufzeiten.</span><span class="sxs-lookup"><span data-stu-id="b392b-p103">SharePoint Framework documentation uses Visual Studio code in the steps and examples. Visual Studio Code is a lightweight but powerful source code editor from Microsoft which runs on your desktop and is available for Windows, Mac and Linux. It comes with built-in support for JavaScript, TypeScript and Node.js and has a rich ecosystem of extensions for other languages (such as C++, C#, Python, PHP) and runtimes..</span></span> 
   
## <a name="preview-the-web-part"></a><span data-ttu-id="b392b-134">Anzeigen einer Webpart-Vorschau</span><span class="sxs-lookup"><span data-stu-id="b392b-134">Preview the web part</span></span>
<span data-ttu-id="b392b-p104">Um eine Vorschau Ihres Webparts anzuzeigen, erstellen Sie es und führen es auf einem lokalen Webserver aus. Die clientseitige Toolkette verwendet standardmäßig HTTPS-Endpunkte. Da für die lokale Entwicklungsumgebung jedoch kein Standardzertifikat konfiguriert ist, meldet der Browser einen Zertifikatfehler. Die SPFx-Toolkette enthält ein Entwicklerzertifikat, das Sie installieren und bei der Webpart-Erstellung nutzen können.</span><span class="sxs-lookup"><span data-stu-id="b392b-p104">To preview your web part, build and run it on a local web server. The client-side toolchain uses HTTPS endpoint by default. However, since a default certificate is not configured for the local dev environment, your browser will report a certificate error. The SPFx toolchain comes with a developer certificate that you can install for building web parts.</span></span>

<span data-ttu-id="b392b-139">Wechseln Sie zur Installation des Entwicklerzertifikats für die SPFx-Entwicklung auf die Konsole, vergewissern Sie sich, dass Sie noch im Verzeichnis **helloworld-webpart** sind, und geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="b392b-139">To install the developer certificate for use with SPFx development, switch to your console, make sure you are still in the **helloworld-webpart** directory and enter the following command:</span></span>

> <span data-ttu-id="b392b-140">Beachten Sie: Wenn Sie Chrome v58 oder eine neuere Chrome-Version als Browser verwenden, generiert der Befehl unten kein gültiges Zertifikat für Ihre Umgebung, und in der lokalen Workbench wird eine Zertifikatausnahme angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b392b-140">Notice that if you hare using Chrome v58 or newer as your browser, below command does not generate valid certificate for your environment and you will see a certificate exception in local workbench</span></span>

```
gulp trust-dev-cert
```

<span data-ttu-id="b392b-141">Damit ist das Entwicklerzertifikat installiert. Nun geben Sie den folgenden Befehl in die Konsole ein, um das Webpart zu erstellen und die Vorschau aufzurufen:</span><span class="sxs-lookup"><span data-stu-id="b392b-141">Now that we have installed the developer certificate, enter the following command in the console to build and preview your web part:</span></span>

```
gulp serve
```

<span data-ttu-id="b392b-142">Dieser Befehl führt eine Reihe von gulp-Tasks aus, um einen lokalen, Node-basierten HTTPS-Server unter „localhost:4321“ zu erstellen und eine Vorschau des Webparts aus Ihrer lokalen Entwicklungsumgebung in Ihrem Standardbrowser anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="b392b-142">This command will execute a series of gulp tasks to create a local, Node-based HTTPS server on 'localhost:4321' and launch your default browser to preview web parts from your local dev environment.</span></span>

![„gulp serve“ für das Webpart-Projekt](../../../../images/helloworld-wp-gulp-serve.png)

<span data-ttu-id="b392b-144">Die SharePoint-Tools für clientseitige Entwicklung verwenden [gulp](http://gulpjs.com/) zur Ausführung von Tasks. Unter anderem bearbeitet gulp Buildtasks wie das:</span><span class="sxs-lookup"><span data-stu-id="b392b-144">SharePoint client-side development tools use [gulp](http://gulpjs.com/) as the task runner to handle build process tasks such as:</span></span>

* <span data-ttu-id="b392b-145">Bundling und Minimieren von JavaScript- und CSS-Dateien</span><span class="sxs-lookup"><span data-stu-id="b392b-145">Bundle and minify JavaScript and CSS files.</span></span>
* <span data-ttu-id="b392b-146">Ausführen von Tools zum Aufrufen der Bündelungs- und Minimierungstasks vor jedem Build</span><span class="sxs-lookup"><span data-stu-id="b392b-146">Run tools to call the bundling and minification tasks before each build.</span></span>
* <span data-ttu-id="b392b-147">Kompilieren von SASS-Dateien in CSS</span><span class="sxs-lookup"><span data-stu-id="b392b-147">Compile SASS files to CSS.</span></span>
* <span data-ttu-id="b392b-148">Kompilieren von TypeScript-Dateien in JavaScript</span><span class="sxs-lookup"><span data-stu-id="b392b-148">Compile TypeScript files to JavaScript.</span></span>

<span data-ttu-id="b392b-149">Wenn Sie mit gulp nicht vertraut sind, empfiehlt sich der Artikel [Using Gulp](http://docs.asp.net/en/latest/client-side/using-gulp.html). Er beschreibt, wie Sie mit gulp und Visual Studio ASP.NET 5-Projekte erstellen können.</span><span class="sxs-lookup"><span data-stu-id="b392b-149">If you are new to gulp, you can read [Using Gulp](http://docs.asp.net/en/latest/client-side/using-gulp.html) which describes using gulp with Visual Studio in conjunction with building ASP.NET 5 projects.</span></span>

<span data-ttu-id="b392b-p105">Visual Studio Code bietet integrierte Unterstützung für gulp und andere Tools zur Taskausführung. Drücken Sie **STRG + UMSCHALT + B** unter Windows oder **BEFEHL + UMSCHALT + B** auf dem Mac, um Ihr Webpart zu debuggen und eine Vorschau anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="b392b-p105">Visual Studio Code provides built-in support for gulp and other task runners. Choose **Ctrl+Shift+B** on Windows or **Cmd+Shift+B** on Mac to debug and preview your web part.</span></span> 

### <a name="sharepoint-workbench"></a><span data-ttu-id="b392b-152">SharePoint Workbench</span><span class="sxs-lookup"><span data-stu-id="b392b-152">SharePoint Workbench</span></span>
<span data-ttu-id="b392b-p106">SharePoint Workbench ist eine Designoberfläche für Entwickler, mit der Sie schnell Webpart-Tests durchführen und eine Webpart-Vorschau anzeigen können, und zwar ohne die Webparts in SharePoint bereitstellen zu müssen. SharePoint Workbench enthält die clientseitige Seite und das clientseitige Canvas. Hier können Sie Webparts während der Entwicklung hinzufügen, löschen und testen.</span><span class="sxs-lookup"><span data-stu-id="b392b-p106">SharePoint Workbench is a developer design surface that enables you to quickly preview and test web parts without deploying them in SharePoint. SharePoint Workbench includes the client-side page and the client-side canvas in which you can add, delete and test your web parts in development.</span></span>

![SharePoint Workbench, lokal ausgeführt](../../../../images/sp-workbench.png)

<span data-ttu-id="b392b-p107">Klicken Sie auf die **Schaltfläche zum Hinzufügen**, um das HelloWorld-Webpart hinzuzufügen. Die Schaltfläche zum Hinzufügen öffnet die Toolbox. Hier sehen Sie eine Liste aller Webparts, die Sie hinzufügen können. In dieser Liste werden das **HelloWorld**-Webpart sowie andere Webparts aufgeführt, die lokal in Ihrer Entwicklungsumgebung verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="b392b-p107">To add the HelloWorld web part, choose the **add** button. The add button opens the toolbox where you can see a list of web parts available for you to add. The list will include the **HelloWorld** web part as well other web parts available locally in your development environment.</span></span>
   
![SharePoint Workbench-Toolbox unter „localhost“](../../../../images/sp-workbench-toolbox.png)
   
<span data-ttu-id="b392b-160">Wählen Sie **HelloWorld** aus, um das Webpart zur Seite hinzuzufügen:</span><span class="sxs-lookup"><span data-stu-id="b392b-160">Choose **HelloWorld** to add the web part to the page:</span></span>
   
![HelloWorld-Webpart in SharePoint Workbench](../../../../images/sp-workbench-helloworld-wp.png)

<span data-ttu-id="b392b-p108">Ausgezeichnet! Sie haben Ihr erstes clientseitiges Webpart zu einer clientseitigen Seite hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="b392b-p108">Congratulations! You have just added your first client-side web part to a client-side page.</span></span>
   
<span data-ttu-id="b392b-164">Klicken Sie nun auf das Stiftsymbol links oben neben dem Webpart, um den Eigenschaftenbereich des Webparts anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="b392b-164">Now, choose the pencil icon on the far left of the web part to reveal the web part property pane.</span></span>
   
![Eigenschaftenbereich für das HelloWorld-Webpart](../../../../images/sp-workbench-helloworld-pp.png)

<span data-ttu-id="b392b-p109">Im Eigenschaftenbereich können Sie Eigenschaften definieren und so Ihr Webpart anpassen. Der Bereich wird clientseitig gesteuert und ermöglicht SharePoint-übergreifend ein konsistentes Design.</span><span class="sxs-lookup"><span data-stu-id="b392b-p109">The property pane is where you can define properties to customize your web part. The property pane is client-side driven and provides a consistent design across SharePoint.</span></span> 
   
<span data-ttu-id="b392b-168">Ändern Sie den Text im Textfeld **Description** in **Clientseitige Webparts sind klasse!**.</span><span class="sxs-lookup"><span data-stu-id="b392b-168">Modify the text in the **Description** text box to **Client-side web parts are awesome!**</span></span>

<span data-ttu-id="b392b-169">Noch während Sie tippen, verändert sich der Text im Webpart.</span><span class="sxs-lookup"><span data-stu-id="b392b-169">Notice how the text in the web part also changes as you type.</span></span> 

<span data-ttu-id="b392b-p110">Eine der neuen Funktionen für den Eigenschaftenbereich betrifft das Aktualisierungsverhalten. Es lässt sich jetzt entweder als „reactive“ oder als „non-reactive“ konfigurieren. Standardmäßig ist das Aktualisierungsverhalten auf „reactive“ gesetzt. Änderungen können Sie dann bereits während der Bearbeitung der Eigenschaften sehen. Wenn das Verhalten auf „reactive“ gesetzt ist, werden Änderungen sofort gespeichert.</span><span class="sxs-lookup"><span data-stu-id="b392b-p110">One of the new capabilities available to the property pane is to configure its update behavior, which can be set to reactive or non-reactive. By default the update behavior is reactive and enables you to see the changes as you edit the properties. The changes are saved instantly as when the behavior is reactive.</span></span>  

## <a name="web-part-project-structure"></a><span data-ttu-id="b392b-173">Webpart-Projektstruktur</span><span class="sxs-lookup"><span data-stu-id="b392b-173">Web part project structure</span></span>
<span data-ttu-id="b392b-174">Sie können die Webpart-Projektstruktur in Visual Studio Code anzeigen.</span><span class="sxs-lookup"><span data-stu-id="b392b-174">You can use Visual Studio Code to explore the web part project structure.</span></span> 

* <span data-ttu-id="b392b-175">Gehen Sie auf der Konsole ins Verzeichnis **src\webparts\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="b392b-175">In the console, go to the **src\webparts\helloWorld** directory.</span></span> 
* <span data-ttu-id="b392b-176">Geben Sie folgenden Befehl ein, um das Webpart-Projekt in Visual Studio Code (oder einem Editor Ihrer Wahl) zu öffnen:</span><span class="sxs-lookup"><span data-stu-id="b392b-176">Enter the following command to open the web part project in Visual Studio Code (or use your favorite editor):</span></span>

```
code .
```

![HelloWorld-Projektstruktur](../../../../images/helloworld-wp-vscode-project-structure.png)

<span data-ttu-id="b392b-178">Falls ein Fehler gemeldet wird, müssen Sie eventuell [den Codebefehl in PATH installieren](https://code.visualstudio.com/docs/editor/setup).</span><span class="sxs-lookup"><span data-stu-id="b392b-178">If you get an error, you might need to [install the code command in PATH](https://code.visualstudio.com/docs/editor/setup).</span></span>

<span data-ttu-id="b392b-p111">TypeScript ist die primäre Sprache zur Erstellung von clientseitigen SharePoint-Webparts. Bei TypeScript handelt es sich um eine typisierte Obersprache zu JavaScript, die in einfaches JavaScript kompiliert. SharePoint-Tools für die clientseitige Entwicklung werden auf Basis von TypeScript-Klassen, -Modulen und -Schnittstellen erstellt. Das hilft Entwicklern, stabile clientseitige Webparts zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b392b-p111">TypeScript is the primary language for building SharePoint client-side web parts. TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. SharePoint client-side development tools are built using TypeScript classes, modules, and interfaces to help developers build robust client-side web parts.</span></span> 

<span data-ttu-id="b392b-182">Nachfolgend beschreiben wir einige der wichtigsten Dateien eines Projekts.</span><span class="sxs-lookup"><span data-stu-id="b392b-182">The following are some key files in the project.</span></span>

### <a name="web-part-class"></a><span data-ttu-id="b392b-183">Webpart-Klasse</span><span class="sxs-lookup"><span data-stu-id="b392b-183">Web part class</span></span>
<span data-ttu-id="b392b-p112">**HelloWorldWebPart.ts** definiert den Haupteinstiegspunkt des Webparts. Die Webpart-Klasse **HelloWorldWebPart** erweitert die Klasse **BaseClientSideWebPart**. Jedes clientseitige Webpart muss die Klasse **BaseClientSideWebPart** erweitern, damit es als gültiges Webpart definiert wird.</span><span class="sxs-lookup"><span data-stu-id="b392b-p112">**HelloWorldWebPart.ts** defines the main entry point for the web part. The web part class **HelloWorldWebPart** extends the **BaseClientSideWebPart**. Any client-side web part should extend the **BaseClientSideWebPart** class in order to be defined as a valid web part.</span></span>

<span data-ttu-id="b392b-p113">**BaseClientSideWebPart** implementiert das Minimum an Funktionen, das für die Erstellung eines Webparts erforderlich ist. Daneben bietet diese Klasse auch viele Parameter für die Überprüfung von und den Zugriff auf schreibgeschützte Eigenschaften wie **displayMode**, Webpart-Eigenschaften, Webpart-Kontext, die Webpart-**instanceId**, das Webpart-**domElement** und vieles mehr.</span><span class="sxs-lookup"><span data-stu-id="b392b-p113">**BaseClientSideWebPart** implements the minimal functionality that is required to build a web part. This class also provides many parameters to validate and access to read-only properties such as **displayMode**, web part properties, web part context, web part **instanceId**, the web part **domElement** and much more.</span></span>

<span data-ttu-id="b392b-189">Die Webpart-Klasse ist dabei so definiert, dass sie den Eigenschaftentyp **IHelloWorldWebPartProps** akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="b392b-189">Notice that the web part class is defined to accept a property type **IHelloWorldWebPartProps**.</span></span>

<span data-ttu-id="b392b-190">Der Eigenschaftentyp ist als Schnittstelle in einer separaten Datei **IHelloWorldWebPartProps.ts** definiert.</span><span class="sxs-lookup"><span data-stu-id="b392b-190">The property type is defined as an interface in a separate file **IHelloWorldWebPartProps.ts**.</span></span>

```ts
export interface IHelloWorldWebPartProps {
    description: string;
}
```

<span data-ttu-id="b392b-191">Anhand dieser Eigenschaftendefinition definieren Sie benutzerdefinierte Eigenschaftentypen für Ihr Webpart. Dazu mehr weiter unten im Abschnitt zum Eigenschaftenbereich.</span><span class="sxs-lookup"><span data-stu-id="b392b-191">This property definition is used to define custom property types for your web part, which is described in the property pane section later.</span></span> 

#### <a name="web-part-render-method"></a><span data-ttu-id="b392b-192">Webpart-Rendermethode</span><span class="sxs-lookup"><span data-stu-id="b392b-192">Web part render method</span></span>
<span data-ttu-id="b392b-p114">Das DOM-Element, in dem das Webpart gerendert werden soll, wird in der Methode **render** spezifiziert. Mithilfe dieser Methode wird das Webpart in dem angegebenen DOM-Element gerendert. Im Webpart **HelloWorld** ist als DOM-Element ein DIV festgelegt. Zu den Parametern der Methode gehören der Anzeigemodus (entweder „Read“ oder „Edit“) sowie etwaige konfigurierte Webpart-Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="b392b-p114">The DOM element where the web part should be rendered is available in the **render** method. This method is used to render the web part inside that DOM element. In the **HelloWorld** web part, the DOM element is set to a DIV. The method parameters include the display mode (either Read or Edit) and the configured web part properties if any:</span></span> 

```ts
  public render(): void {
    this.domElement.innerHTML = `
      <div class="${styles.helloWorld}">
        <div class="${styles.container}">
          <div class="ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}">
            <div class="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
              <span class="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
              <p class="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
              <p class="ms-font-l ms-fontColor-white">${escape(this.properties.description)}</p>
              <a href="https://aka.ms/spfx" class="${styles.button}">
                <span class="${styles.label}">Learn more</span>
              </a>
            </div>
          </div>
        </div>
      </div>`;
  }
```

<span data-ttu-id="b392b-197">Das Modell ist flexibel: Webparts können in jedem JavaScript-Framework erstellt und dann in das DOM-Element geladen werden.</span><span class="sxs-lookup"><span data-stu-id="b392b-197">This model is flexible enough so that web parts can be built in any JavaScript framework and loaded into the DOM element.</span></span> 

#### <a name="configure-the-web-part-property-pane"></a><span data-ttu-id="b392b-198">Konfigurieren des Webpart-Eigenschaftenbereichs</span><span class="sxs-lookup"><span data-stu-id="b392b-198">Configure the Web part property pane</span></span>
<span data-ttu-id="b392b-p115">Der Eigenschaftenbereich wird in der Klasse **HelloWorldWebPart** definiert, und zwar in der Eigenschaft **propertyPaneSettings**.</span><span class="sxs-lookup"><span data-stu-id="b392b-p115">The property pane is defined in the **HelloWorldWebPart** class. The **propertyPaneSettings** property is where you need to define the property pane.</span></span>

<span data-ttu-id="b392b-201">Sobald Sie die gewünschten Eigenschaften definiert haben, können Sie sie per `this.properties.<property-value>` im Webpart aufrufen. Hier ein Beispiel dafür in der Methode **render**:</span><span class="sxs-lookup"><span data-stu-id="b392b-201">When the properties are defined, you can access them in your web part using `this.properties.<property-value>`, as shown in the **render** method:</span></span>

```ts
<p class="${styles.description}">${escape(this.properties.description)}</p>
```

<span data-ttu-id="b392b-202">Beachten Sie, dass wir dem Wert der Eigenschaft ein HTML-Escapezeichen hinzufügen, damit die Zeichenfolge gültig ist.</span><span class="sxs-lookup"><span data-stu-id="b392b-202">Notice that we are performing a HTML escape on the property's value to ensure a valid string.</span></span>

<span data-ttu-id="b392b-203">Im Artikel [Integrating property pane with a web part](../basics/integrate-with-property-pane) erfahren Sie mehr über die Arbeit mit dem Eigenschaftenbereich sowie die verschiedenen Feldtypen im Eigenschaftbereich.</span><span class="sxs-lookup"><span data-stu-id="b392b-203">Read the [Integrating property pane with a web part](../basics/integrate-with-property-pane) article to learn more about how to work with the property pane and property pane field types.</span></span>

<span data-ttu-id="b392b-p116">Nun fügen wir dem Eigenschaftenbereich einige weitere Eigenschaften hinzu – ein Kontrollkästchen, ein Dropdown und einen Umschalter. Zunächst importieren wir die jeweiligen Felder des Eigenschaftenbereichs aus dem Framework.</span><span class="sxs-lookup"><span data-stu-id="b392b-p116">Lets now add few more properties - a checkbox, dropdown and a toggle - to the property pane. We first start by importing the respective property pane fields from the framework.</span></span>

<span data-ttu-id="b392b-206">Scrollen Sie zum Anfang der Datei, und tragen Sie Folgendes in den Abschnitt für den Import aus `@microsoft/sp-webpart-base` ein:</span><span class="sxs-lookup"><span data-stu-id="b392b-206">Scroll to the top of the file and add the following to the import section from `@microsoft/sp-webpart-base`:</span></span>

```ts
PropertyPaneCheckbox,
PropertyPaneDropdown,
PropertyPaneToggle
```

<span data-ttu-id="b392b-207">Der vollständige Importabschnitt sieht dann wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="b392b-207">The complete import section will look like the following:</span></span>

```ts
import {
  BaseClientSideWebPart,
  IPropertyPaneConfiguration,
  PropertyPaneTextField,
  PropertyPaneCheckbox,
  PropertyPaneDropdown,
  PropertyPaneToggle
} from '@microsoft/sp-webpart-base';
```

<span data-ttu-id="b392b-208">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="b392b-208">Save the file.</span></span>

<span data-ttu-id="b392b-p117">Aktualisieren Sie als Nächstes die Webparteigenschaften um die neuen Eigenschaften. Dadurch werden die Felder typisierten Objekten zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="b392b-p117">Next, update the web part properties to include the new properties. This maps the fields to typed objects.</span></span>

<span data-ttu-id="b392b-211">Öffnen Sie dazu **IHelloWorldWebPartProps.ts**, und ersetzen Sie den vorhandenen Code durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="b392b-211">Open **IHelloWorldWebPartProps.ts** and replace the existing code with the following code.</span></span> 

```ts
export interface IHelloWorldWebPartProps {
    description: string;
    test: string;
    test1: boolean;
    test2: string;
    test3: boolean;
}
```

<span data-ttu-id="b392b-212">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="b392b-212">Save the file.</span></span>

<span data-ttu-id="b392b-213">Wechseln Sie zurück zur Datei **HelloWorldWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="b392b-213">Switch back to the **HelloWorldWebPart.ts** file.</span></span>

<span data-ttu-id="b392b-214">Ersetzen Sie die Methode **getPropertyPaneConfiguration** durch den folgenden Code, der die neuen Felder des Eigenschaftenbereichs hinzufügt und den jeweiligen typisierten Objekten zuordnet.</span><span class="sxs-lookup"><span data-stu-id="b392b-214">Replace the **getPropertyPaneConfiguration** method with the code below which adds the new property pane fields and maps them to their respective typed objects.</span></span>

```ts
protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
  return {
    pages: [
      {
        header: {
          description: strings.PropertyPaneDescription
        },
        groups: [
          {
            groupName: strings.BasicGroupName,
            groupFields: [
            PropertyPaneTextField('description', {
              label: 'Description'
            }),
            PropertyPaneTextField('test', {
              label: 'Multi-line Text Field',
              multiline: true
            }),
            PropertyPaneCheckbox('test1', {
              text: 'Checkbox'
            }),
            PropertyPaneDropdown('test2', {
              label: 'Dropdown',
              options: [
                { key: '1', text: 'One' },
                { key: '2', text: 'Two' },
                { key: '3', text: 'Three' },
                { key: '4', text: 'Four' }
              ]}),
            PropertyPaneToggle('test3', {
              label: 'Toggle',
              onText: 'On',
              offText: 'Off'
            })
          ]
          }
        ]
      }
    ]
  };
}
```


<span data-ttu-id="b392b-215">Nachdem Sie die Eigenschaften zu den Webpart-Eigenschaften hinzugefügt haben, können Sie nun genauso auf sie zugreifen, wie Sie zuvor auf die **description**-Eigenschaft zugegriffen haben:</span><span class="sxs-lookup"><span data-stu-id="b392b-215">After you add your properties to the web part properties, you can now access the properties in the same way you accessed the **description** property earlier:</span></span>

```ts
<p class="ms-font-l ms-fontColor-white">${escape(this.properties.test)}</p>
```

<span data-ttu-id="b392b-216">Zur Festlegung des Standardwerts für die Eigenschaften müssen Sie den Eigenschaftenbehälter **properties** im Webpart-Manifest aktualisieren:</span><span class="sxs-lookup"><span data-stu-id="b392b-216">To set the default value for the properties, you will need to update the web part manifest's **properties** property bag:</span></span>

<span data-ttu-id="b392b-217">Öffnen Sie `HelloWorldWebPart.manifest.json`, und ändern Sie `properties` wie folgt:</span><span class="sxs-lookup"><span data-stu-id="b392b-217">Open `HelloWorldWebPart.manifest.json` and modify the `properties` to:</span></span>

```ts
"properties": {
  "description": "HelloWorld",
  "test": "Multi-line text field",
  "test1": true,
  "test2": "2",
  "test3": true
}
```

<span data-ttu-id="b392b-218">Der Webpart-Eigenschaftenbereich weist jetzt diese Standardwerte für die betreffenden Eigenschaften auf.</span><span class="sxs-lookup"><span data-stu-id="b392b-218">The web part property pane will now have these default values for those properties.</span></span>

### <a name="web-part-manifest"></a><span data-ttu-id="b392b-219">Webpart-Manifest</span><span class="sxs-lookup"><span data-stu-id="b392b-219">Web part manifest</span></span>
<span data-ttu-id="b392b-p118">Die Datei **HelloWorldWebPart.manifest.json** definiert die Webpart-Metadaten, beispielsweise die Version, die ID, den Anzeigenamen, das Symbol und die Beschreibung. Jedes Webpart sollte ein solches Manifest enthalten.</span><span class="sxs-lookup"><span data-stu-id="b392b-p118">The **HelloWorldWebPart.manifest.json** file defines the web part metadata such as version, id, display name, icon, and description. Every web part should contain this manifest.</span></span>

```json
{
  "$schema": "../../../node_modules/@microsoft/sp-module-interfaces/lib/manifestSchemas/jsonSchemas/clientSideComponentManifestSchema.json",

  "id": "922a9623-f92f-4971-8574-185b31554e44",
  "alias": "HelloWorldWebPart",
  "componentType": "WebPart",
  "version": "0.0.1",
  "manifestVersion": 2,

  "preconfiguredEntries": [{
    "groupId": "922a9623-f92f-4971-8574-185b31554e44",
    "group": { "default": "Under Development" },
    "title": { "default": "HelloWorld" },
    "description": { "default": "HelloWorld description" },
    "officeFabricIconFontName": "Page",
    "properties": {
      "description": "HelloWorld",
      "test": "Multi-line text field",
      "test1": true,
      "test2": "2",
      "test3": true
    }
  }]
}
```

<span data-ttu-id="b392b-p119">Da wir nun neue Eigenschaften eingeführt haben, müssen Sie sicherstellen, dass Sie das Webpart wieder aus der lokalen Entwicklungsumgebung hosten, indem Sie den folgenden Befehl ausführen. Dadurch wird auch sichergestellt, dass die oben angegebenen Änderungen ordnungsgemäß angewendet wurden.</span><span class="sxs-lookup"><span data-stu-id="b392b-p119">Now that we have introduced new properties, make sure that you are again hosting the web part from the local developement environment by executing following command. This will also ensure that the above changes were correctly applied.</span></span>

```
gulp serve
```

### <a name="preview-the-web-part-in-sharepoint"></a><span data-ttu-id="b392b-224">Anzeigen der Webpart-Vorschau in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b392b-224">Preview the web part in SharePoint</span></span>

<span data-ttu-id="b392b-p120">SharePoint Workbench lässt sich auch in SharePoint hosten, um während der Entwicklung lokaler Webparts eine Webpart-Vorschau anzuzeigen und Tests durchzuführen. Der entscheidende Vorteil: Sie führen Ihr Webpart dann im SharePoint-Kontext aus und können mit SharePoint-Daten interagieren.</span><span class="sxs-lookup"><span data-stu-id="b392b-p120">SharePoint Workbench is also hosted in SharePoint to preview and test your local web parts in development. The key advantage is that now you are running in SharePoint context and that you will be able to interact with SharePoint data.</span></span>

<span data-ttu-id="b392b-227">Rufen Sie die folgende URL auf: „https://your-sharepoint-site/_layouts/workbench.aspx“.</span><span class="sxs-lookup"><span data-stu-id="b392b-227">Go to the following URL: 'https://your-sharepoint-site/_layouts/workbench.aspx'</span></span>

><span data-ttu-id="b392b-p121">**Hinweis:** Wenn Sie das SPFx-Entwicklerzertifikat noch nicht installiert haben, meldet Workbench, dass das Laden von Skripts von „localhost“ nicht konfiguriert ist. Halten Sie den aktuell ausgeführten Prozess im Konsolenfenster an, und führen Sie in der Konsole des Projektverzeichnisses den Befehl `gulp trust-dev-cert` aus, um das Entwicklerzertifikat zu installieren, bevor Sie den `gulp serve`-Befehl erneut ausführen.</span><span class="sxs-lookup"><span data-stu-id="b392b-p121">**Note:** If you do not have the SPFx developer certificate installed, then Workbench will notify you that it is configured not to load scripts from localhost. Execute `gulp trust-dev-cert` command in your project directory console to install the developer certificate.</span></span>

![SharePoint Workbench, ausgeführt auf einer SharePoint Online-Website](../../../../images/sp-workbench-o365.png)

<span data-ttu-id="b392b-231">In SharePoint Workbench wird jetzt die Navigationsleiste der Office 365 Suite angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b392b-231">Notice that the SharePoint workbench now has the Office 365 Suite navigation bar.</span></span>

<span data-ttu-id="b392b-p122">Klicken Sie im Canvas auf das **Symbol zum Hinzufügen**, um die Toolbox aufzurufen. In der Toolbox finden Sie jetzt die Webparts, die auf der Website verfügbar sind, auf der SharePoint Workbench gehostet wird, sowie **HelloWorldWebPart**.</span><span class="sxs-lookup"><span data-stu-id="b392b-p122">Choose **add icon** in the canvas to reveal the toolbox. The toolbox now shows the web parts available on the site where the SharePoint workbench is hosted along with your **HelloWorldWebPart**.</span></span>

![Toolbox in SharePoint Workbench, ausgeführt auf einer SharePoint Online-Website](../../../../images/sp-workbench-o365-toolbox.png)

<span data-ttu-id="b392b-p123">Fügen Sie **HelloWorldWebPart** aus der Toolbox hinzu. Das Webpart wird jetzt auf einer in SharePoint gehosteten Website ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="b392b-p123">Add **HelloWorldWebPart** from the toolbox. Now you're running your web part in a page hosted in SharePoint!</span></span>

![HelloWorld-Webpart, ausgeführt in SharePoint Workbench auf einer SharePoint Online-Website](../../../../images/sp-workbench-o365-helloworld-wp.png)

<span data-ttu-id="b392b-238">Da die Entwicklung und die Tests Ihres Webparts noch nicht abgeschlossen sind, müssen Sie es weder packen noch auf SharePoint bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="b392b-238">Because you are still developing and testing your web part, there is no need to package and deploy your web part to SharePoint.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b392b-239">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="b392b-239">Next steps</span></span>
<span data-ttu-id="b392b-p124">Herzlichen Glückwunsch! Ihr erstes HelloWorld-Webpart läuft. Jetzt können Sie das HelloWorld-Webpart weiter ausbauen. Wie das funktioniert, erfahren Sie im nächsten Artikel, [Verbinden mit SharePoint](./connect-to-sharepoint). Dort verwenden Sie dasselbe HelloWorld-Webpart-Projekt und ergänzen es um eine Funktion zur Interaktion mit REST-APIs für SharePoint-Listen. Ihnen wird bereits aufgefallen sein, dass der Befehl `gulp serve` immer noch im Konsolenfenster ausgeführt wird (oder in Visual Studio Code, falls Sie den Editor verwenden). Sie können ihn einfach weiterlaufen lassen und zum nächsten Artikel wechseln.</span><span class="sxs-lookup"><span data-stu-id="b392b-p124">Congratulations on getting your first Hello World web part running! Now that your web part is running, you can continue building out your Hello World web part in the next topic, [Connect to SharePoint](./connect-to-sharepoint). You will use the same Hello World web part project and add the ability to interact with SharePoint List REST APIs. Notice that the `gulp serve` command is still running in your console window (or in Visual Studio Code if you using the editor). You can continue to let it run while you go to the next article.</span></span>
