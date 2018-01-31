---
title: Erstellen Ihrer ersten SharePoint-Framework-Erweiterung (Hello World, Teil 1)
description: Erstellen Sie ein Erweiterungsprojekt, und codieren und debuggen Sie dann Ihren Anwendungsanpasser.
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: 3126f663ca6d7df21b37448386dd3baafe1fb1f8
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="build-your-first-sharepoint-framework-extension-hello-world-part-1"></a><span data-ttu-id="60742-103">Erstellen Ihrer ersten SharePoint-Framework-Erweiterung (Hello World, Teil 1)</span><span class="sxs-lookup"><span data-stu-id="60742-103">Build your first SharePoint Framework Extension (Hello World part 1)</span></span>

<span data-ttu-id="60742-p101">SharePoint-Framework (SPFx)-Erweiterungen sind clientseitige Komponenten, die im Kontext einer SharePoint-Seite ausgeführt werden. Sie können Erweiterungen in SharePoint Online bereitstellen und mithilfe aktueller JavaScript-Tools und -Bibliotheken erstellen.</span><span class="sxs-lookup"><span data-stu-id="60742-p101">SharePoint Framework (SPFx) Extensions are client-side components that run inside the context of a SharePoint page. You can deploy extensions to SharePoint Online, and you can use modern JavaScript tools and libraries to build them.</span></span>

<span data-ttu-id="60742-106">Sie können die in diesem Artikel beschriebenen Schritte auch anhand des Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=0BeS0HukW24&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV) nachvollziehen.</span><span class="sxs-lookup"><span data-stu-id="60742-106">You can follow the steps in this article by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=0BeS0HukW24&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span></span> 

<a href="https://www.youtube.com/watch?v=yrFNu6K7iuU">
<img src="../../../images/spfx-ext-youtube-tutorial1.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="create-an-extension-project"></a><span data-ttu-id="60742-107">Erstellen eines Erweiterungsprojekts</span><span class="sxs-lookup"><span data-stu-id="60742-107">Create an extension project</span></span>

1. <span data-ttu-id="60742-108">Erstellen Sie an einem Speicherort Ihrer Wahl ein neues Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="60742-108">Create a new project directory in your favorite location.</span></span>

    ```
    md app-extension
    ```

2. <span data-ttu-id="60742-109">Wechseln Sie in das Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="60742-109">Go to the project directory.</span></span>

    ```
    cd app-extension
    ```

3. <span data-ttu-id="60742-110">Führen Sie den Yeoman-SharePoint-Generator aus, um eine neue HelloWorld-Erweiterung zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="60742-110">Create a new HelloWorld extension by running the Yeoman SharePoint Generator.</span></span>

    ```
    yo @microsoft/sharepoint
    ```

4. <span data-ttu-id="60742-111">Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="60742-111">When prompted:</span></span>

    * <span data-ttu-id="60742-112">Übernehmen Sie den Standardwert **app-extension** als Lösungsnamen, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="60742-112">Accept the default app-extension as your solution name, and press Enter.</span></span>
    * <span data-ttu-id="60742-113">Wählen Sie **SharePoint Online only (latest)**, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="60742-113">Select **SharePoint Online only (latest)**, and select Enter.</span></span>
    * <span data-ttu-id="60742-114">Wählen Sie **Use the current folder** aus, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="60742-114">Select **Use the current folder**, and select Enter.</span></span>
    * <span data-ttu-id="60742-115">Wählen Sie **N**, damit die Erweiterung auf jeder Website explizit installiert werden muss, wenn sie verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="60742-115">Select **N** to require the extension to be installed on each site explicitly when it's being used.</span></span> 
    * <span data-ttu-id="60742-116">Wählen Sie **Extension** als den zu erstellenden Typ von clientseitiger Komponente aus.</span><span class="sxs-lookup"><span data-stu-id="60742-116">Select **Extension** as the client-side component type to be created.</span></span> 
    * <span data-ttu-id="60742-117">Wählen Sie **Application Customizer** als den zu erstellenden Erweiterungstyp aus.</span><span class="sxs-lookup"><span data-stu-id="60742-117">Select **Field Customizer** as the extension type to be created.</span></span>

5. <span data-ttu-id="60742-118">Über die nächsten Eingabeaufforderungen werden spezifische Informationen zu der Erweiterung abgefragt.</span><span class="sxs-lookup"><span data-stu-id="60742-118">The next set of prompts ask for specific information about your extension:</span></span> <span data-ttu-id="60742-119">Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="60742-119">When prompted:</span></span>

    * <span data-ttu-id="60742-120">Übernehmen Sie den Standardwert **HelloWorld** als Namen für Ihre Erweiterung, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="60742-120">Accept the default value of **HelloWorld** as your extension name, and then select Enter.</span></span>
    * <span data-ttu-id="60742-121">Übernehmen Sie den Standardwert **HelloWorld description** als Beschreibung Ihrer Erweiterung, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="60742-121">Accept the default value of **HelloWorld description** as your extension description, and select Enter.</span></span>

    <br/>

    ![Yeoman-SharePoint-Generator mit Eingabeaufforderungen zur Erstellung einer Erweiterungslösung](../../../images/ext-yeoman-app-prompts.png)

    > [!NOTE] 
    > <span data-ttu-id="60742-123">Wenn der verwendete Erweiterungsname zu lang ist, können Probleme auftreten.</span><span class="sxs-lookup"><span data-stu-id="60742-123">If you use a name for the extension that is too long, you might encounter issues.</span></span> <span data-ttu-id="60742-124">Mit den bereitgestellten Eingaben wird ein Aliaseintrag für die JSON-Manifestdatei des Application Customizer generiert.</span><span class="sxs-lookup"><span data-stu-id="60742-124">The entries provided are used to generate an alias entry for the application customizer manifest json file.</span></span> <span data-ttu-id="60742-125">Falls der Alias mehr als 40 Zeichen enthält, wird eine Ausnahme ausgelöst, wenn Sie versuchen, die Erweiterung mit `gulp serve --nobrowser` zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="60742-125">If the alias is longer than 40 characters, you will get an exception when you try to serve the extension using `gulp serve --nobrowser`.</span></span> <span data-ttu-id="60742-126">Sie können dieses Problem beheben, indem Sie den Aliaseintrag später aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="60742-126">You can resolve this by updating the alias entry afterward.</span></span>

    <span data-ttu-id="60742-127">An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien sowie die **HelloWorld**-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="60742-127">At this point, Yeoman installs the required dependencies and scaffolds the solution files along with the **HelloWorld** extension.</span></span> <span data-ttu-id="60742-128">Das kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="60742-128">This might take a few minutes.</span></span> 

    <span data-ttu-id="60742-129">Nach Abschluss der Gerüsterstellung sollte folgende Erfolgsmeldung angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="60742-129">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

    ![Erfolgreiche Erstellung eines Gerüsts für die clientseitige SharePoint-Lösung](../../../images/ext-yeoman-app-complete.png)

    <span data-ttu-id="60742-131">Details zur Behebung etwaiger Fehler finden Sie unter [Bekannte Probleme](../../known-issues-and-common-questions.md).</span><span class="sxs-lookup"><span data-stu-id="60742-131">For information about troubleshooting any errors, see [Known issues](../../known-issues-and-common-questions.md).</span></span>

6. <span data-ttu-id="60742-132">Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="60742-132">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

    ```sh
    npm shrinkwrap
    ```

7. <span data-ttu-id="60742-133">Geben Sie als Nächstes Folgendes in die Konsole ein, um Visual Studio Code zu starten.</span><span class="sxs-lookup"><span data-stu-id="60742-133">Next, type the following into the console to start Visual Studio Code.</span></span>

    ```
    code .
    ```

    > [!NOTE] 
    > <span data-ttu-id="60742-134">Da die clientseitige SharePoint-Lösung auf HTML/TypeScript basiert, können Sie zur Erstellung Ihrer Erweiterung jeden Code-Editor verwenden, der clientseitige Entwicklung unterstützt.</span><span class="sxs-lookup"><span data-stu-id="60742-134">Because the SharePoint client-side solution is HTML/TypeScript based, you can use any code editor that supports client-side development to build your extension.</span></span>

    <span data-ttu-id="60742-p105">Wie Sie sehen, sieht die Standardlösungsstruktur wie die Lösungsstruktur clientseitiger Webparts aus. Hierbei handelt es sich um die grundlegende SharePoint-Framework-Lösungsstruktur, die für alle Lösungstypen vergleichbare Konfigurationsoptionen bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="60742-p105">Notice how the default solution structure looks like the solution structure for client-side web parts. This is the basic SharePoint Framework solution structure, with similar configuration options across all solution types.</span></span>

    ![SharePoint-Framework-Lösung nach der Erstellung des anfänglichen Gerüsts](../../../images/ext-app-vscode-solution-structure.png)

8. <span data-ttu-id="60742-138">Öffnen Sie **HelloWorldApplicationCustomizer.manifest.json** im Ordner „src\extensions\helloWorld“.</span><span class="sxs-lookup"><span data-stu-id="60742-138">Open **HelloWorldApplicationCustomizer.manifest.json** in the src\extensions\helloWorld folder.</span></span>

    <span data-ttu-id="60742-p106">In dieser Datei sind der Erweiterungstyp und ein eindeutiger Bezeichner für die Erweiterung definiert. Sie benötigen diese ID später, um die Erweiterung zu debuggen und in SharePoint bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="60742-p106">This file defines your extension type and a unique identifier for your extension. You’ll need this ID later when you debug and deploy your extension to SharePoint.</span></span>

    ![JSON-Inhalt des Anwendungsanpasser-Manifests](../../../images/ext-app-vscode-manifest.png)

## <a name="code-your-application-customizer"></a><span data-ttu-id="60742-142">Codieren des Anwendungsanpassers</span><span class="sxs-lookup"><span data-stu-id="60742-142">Code your Application Customizer</span></span> 

<span data-ttu-id="60742-143">Öffnen Sie die Datei **HelloWorldApplicationCustomizer.ts** im Ordner **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="60742-143">Open the **HelloWorldApplicationCustomizer.ts** file in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="60742-144">Beachten Sie, dass die Basisklasse für den Application Customizer aus dem **sp-application-base**-Paket importiert wird, das den SharePoint-Framework-Code enthält, der für den Application Customizer erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="60742-144">Notice that base class for the Application Customizer is imported from the **sp-application-base** package, which contains SharePoint framework code required by the Application Customizer.</span></span> 

![Import-Anweisung für BaseApplicationCustomizer aus @microsoft/sp-application-base](../../../images/ext-app-vscode-app-base.png)

<span data-ttu-id="60742-146">Die Logik für den Anwendungsanpasser ist in der **onInit**-Methode enthalten, die aufgerufen wird, wenn die clientseitige Erweiterung erstmalig auf der Seite aktiviert wird.</span><span class="sxs-lookup"><span data-stu-id="60742-146">The logic for your Application Customizer is contained in the **onInit** method, which is called when the client-side extension is first activated on the page.</span></span> <span data-ttu-id="60742-147">Dieses Ereignis tritt nach Zuweisung von `this.context` und `this.properties` ein.</span><span class="sxs-lookup"><span data-stu-id="60742-147">This event occurs after `this.context` and `this.properties` are assigned.</span></span> <span data-ttu-id="60742-148">Wie bei Webparts gibt `onInit()` eine Zusage zurück, die Sie verwenden können, um asynchrone Operationen auszuführen.</span><span class="sxs-lookup"><span data-stu-id="60742-148">As with web parts, `onInit()` returns a promise that you can use to perform asynchronous operations.</span></span>

> [!NOTE] 
> <span data-ttu-id="60742-149">Der Klassenkonstruktor wird in einer frühen Phase aufgerufen, wenn `this.context` und `this.properties` noch nicht definiert sind.</span><span class="sxs-lookup"><span data-stu-id="60742-149">The class constructor is called at an early stage, when `this.context` and `this.properties` are undefined.</span></span> <span data-ttu-id="60742-150">Benutzerdefinierte Initiierungslogik wird an dieser Stelle nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="60742-150">Custom initiation logic is not supported here.</span></span>

<span data-ttu-id="60742-p109">Im Folgenden werden die Inhalte von **onInit()** in der Standardlösung aufgelistet. Die Standardlösung schreibt ein Protokoll in das Dev Dashboard und zeigt dann beim Rendern der Seite eine einfache JavaScript-Warnung an.</span><span class="sxs-lookup"><span data-stu-id="60742-p109">The following are the contents of **onInit()** in the default solution. This default solution writes a log to the Dev Dashboard, and then displays a simple JavaScript alert when the page renders.</span></span>

![Standardmäßige onInit-Methode im Code](../../../images/ext-app-vscode-methods.png)

<span data-ttu-id="60742-154">Wenn Ihr Anwendungsanpasser die JSON-Eingabe **ClientSideComponentProperties** verwendet, wird sie in das Objekt **BaseExtension.properties** deserialisiert.</span><span class="sxs-lookup"><span data-stu-id="60742-154">If your application customizer uses the **ClientSideComponentProperties** JSON input, it will be deserialized into the **BaseExtension.properties** object.</span></span> <span data-ttu-id="60742-155">Sie können eine Benutzeroberfläche definieren, um sie zu beschreiben.</span><span class="sxs-lookup"><span data-stu-id="60742-155">You can define an interface to describe it.</span></span> <span data-ttu-id="60742-156">Die Standardvorlage sucht nach einer Eigenschaft mit dem Namen **testMessage**.</span><span class="sxs-lookup"><span data-stu-id="60742-156">The default template is looking for a property called **testMessage**.</span></span> <span data-ttu-id="60742-157">Wenn diese Eigenschaft bereitgestellt wird, wird diese in einer Warnmeldung ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="60742-157">If that property is provided, it outputs it in an alert message.</span></span>

## <a name="debug-your-application-customizer"></a><span data-ttu-id="60742-158">Debuggen des Anwendungsanpassers</span><span class="sxs-lookup"><span data-stu-id="60742-158">Code your Application Customizer</span></span>

<span data-ttu-id="60742-159">SharePoint-Framework-Erweiterungen können derzeit nicht mit der lokalen Workbench getestet werden.</span><span class="sxs-lookup"><span data-stu-id="60742-159">You cannot currently use the local workbench to test SharePoint Framework Extensions.</span></span> <span data-ttu-id="60742-160">Sie müssen sie mit einer SharePoint Online-Live-Website testen.</span><span class="sxs-lookup"><span data-stu-id="60742-160">You'll need to test them  against a live SharePoint Online site.</span></span> <span data-ttu-id="60742-161">Hierzu ist es nicht erforderlich, die Anpassung im App-Katalog bereitzustellen, was das Debugging vereinfacht und beschleunigt.</span><span class="sxs-lookup"><span data-stu-id="60742-161">You don't have to deploy your customization to the App Catalog to do this, which makes the debugging experience simple and efficient.</span></span> 

1. <span data-ttu-id="60742-162">Führen Sie den folgenden Befehl aus, um den Code zu kompilieren und die kompilierten Dateien auf Ihrem lokalen Computer zu hosten:</span><span class="sxs-lookup"><span data-stu-id="60742-162">First, compile your code and host the compiled files from your local computer by running the following command.</span></span>

    ```
    gulp serve --nobrowser
    ```

    > [!NOTE] 
    > <span data-ttu-id="60742-163">Wenn Sie das SPFx-Entwicklerzertifikat noch nicht installiert haben, meldet Workbench, dass das Laden von Skripts von „localhost“ nicht konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="60742-163">If you do not have the SPFx developer certificate installed, Workbench will notify you that it is not configured to load scripts from localhost.</span></span> <span data-ttu-id="60742-164">Beenden Sie in diesem Fall den Prozess, der derzeit im Konsolenfenster ausgeüfhrt wird, führen Sie den Befehl `gulp trust-dev-cert` im Projektverzeichnis aus, um das Entwicklerzertifikat zu installieren, und führen Sie dann den Befehl `gulp serve --nobrowser` erneut aus.</span><span class="sxs-lookup"><span data-stu-id="60742-164">If this happens, stop the process that is currently running in the console window, run the `gulp trust-dev-cert` command in your project directory console to install the developer certificate, and then run the `gulp serve --nobrowser` command again.</span></span>

    <span data-ttu-id="60742-165">Sie verwenden die Option `--nobrowser`, da ein Start der lokalen Workbench nicht nötig ist, weil Erweiterungen nicht lokal gedebuggt werden können.</span><span class="sxs-lookup"><span data-stu-id="60742-165">You use the `--nobrowser` option because you don't need to launch the local workbench, since you can't debug extensions locally.</span></span>

    <span data-ttu-id="60742-166">Wenn der Code ohne Fehler kompiliert wurde, verarbeitet er das resultierende Manifest von https://localhost:4321.</span><span class="sxs-lookup"><span data-stu-id="60742-166">When the code compiles without errors, it will serve the resulting manifest from https://localhost:4321.</span></span>

    ![Gulp serve](../../../images/ext-app-gulp-serve.png)

2. <span data-ttu-id="60742-168">Zum Testen der Erweiterung wechseln Sie zu einer Seite mit der modernen Listenansicht in Ihrer SharePoint-Umgebung, und fügen Sie die folgenden Abfragezeichenfolgen-Parameter an die URL an:</span><span class="sxs-lookup"><span data-stu-id="60742-168">To test your extension, go to a modern list view page in your SharePoint environment and append the following query string parameters to the URL.</span></span> <span data-ttu-id="60742-169">Beachten Sie, dass Sie die ID entsprechend Ihrem eigenen Erweiterungsbezeichner aktualisieren müssen.</span><span class="sxs-lookup"><span data-stu-id="60742-169">Notice that you will need to update the ID to match your own extension identifier.</span></span> <span data-ttu-id="60742-170">Dieser ist in der Datei **HelloWorldApplicationCustomizer.manifest.json** verfügbar.</span><span class="sxs-lookup"><span data-stu-id="60742-170">This is available in the **HelloWorldApplicationCustomizer.manifest.json** file.</span></span>

    ```json
        ?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"testMessage":"Hello as property!"}}}
    ```

    <span data-ttu-id="60742-171">Weitere Details zu den URL-Abfrageparametern:</span><span class="sxs-lookup"><span data-stu-id="60742-171">More detail about the URL query parameters:</span></span>

    * <span data-ttu-id="60742-172">**loadSPFX=true**.</span><span class="sxs-lookup"><span data-stu-id="60742-172">**loadSPFX=true**.</span></span> <span data-ttu-id="60742-173">Dient zum Sicherstellen, dass das SharePoint-Framework auf der Seite geladen wird.</span><span class="sxs-lookup"><span data-stu-id="60742-173">loadSPFX=true - Ensures that the SharePoint Framework is loaded on the page.</span></span> <span data-ttu-id="60742-174">Aus Leistungsgründen wird das Framework erst geladen, wenn mindestens eine Erweiterung registriert wurde.</span><span class="sxs-lookup"><span data-stu-id="60742-174">For performance reasons, the framework does not load unless at least one extension is registered.</span></span> <span data-ttu-id="60742-175">Da keine Komponenten registriert sind, müssen Sie das Framework explizit laden.</span><span class="sxs-lookup"><span data-stu-id="60742-175">Because no components are registered,you must explicitly load the framework.</span></span>

    * <span data-ttu-id="60742-176">**debugManifestsFile**.</span><span class="sxs-lookup"><span data-stu-id="60742-176">**debugManifestsFile**.</span></span> <span data-ttu-id="60742-177">Gibt an, dass lokal verarbeitete SPFx-Komponenten geladen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="60742-177">debugManifestsFile - Specifies that you want to load SPFx components that are locally served.</span></span> <span data-ttu-id="60742-178">Das Ladeprogramm sucht nur an zwei Stellen nach Komponenten: im App-Katalog (nach Komponenten der bereitgestellten Lösung) und auf dem SharePoint-Manifestserver (nach den Systembibliotheken).</span><span class="sxs-lookup"><span data-stu-id="60742-178">The loader only looks for components in the App Catalog (for your deployed solution) and the SharePoint manifest server (for the system libraries).</span></span>

    * <span data-ttu-id="60742-179">**customActions**.</span><span class="sxs-lookup"><span data-stu-id="60742-179">**customActions**.</span></span> <span data-ttu-id="60742-180">Simuliert eine benutzerdefinierte Aktion.</span><span class="sxs-lookup"><span data-stu-id="60742-180">customActions - Simulates a custom action.</span></span> <span data-ttu-id="60742-181">Wenn Sie diese Komponente auf einer Website bereitstellen und registrieren, erstellen Sie dieses **CustomAction**-Objekt und beschreiben die verschiedenen Eigenschaften, die Sie dafür festlegen können.</span><span class="sxs-lookup"><span data-stu-id="60742-181">When you deploy and register this component in a site, you'll create this **CustomAction** object and describe all the different properties you can set on it.</span></span> 
        * <span data-ttu-id="60742-182">**Key**.</span><span class="sxs-lookup"><span data-stu-id="60742-182">Key</span></span> <span data-ttu-id="60742-183">Verwenden Sie die GUID der Erweiterung als Schlüssel, der der benutzerdefinierten Aktion zuzuordnen ist.</span><span class="sxs-lookup"><span data-stu-id="60742-183">Key - Use the Guid of the extension as the key to associate with the custom action.</span></span> <span data-ttu-id="60742-184">Dieser muss dem ID-Wert der Erweiterung entsprechen, der in der JSON-Manifestdatei der Erweiterung zur Verfügung steht.</span><span class="sxs-lookup"><span data-stu-id="60742-184">This has to match the ID value of your extension, which is available in the extension manifest.json file.</span></span>
        * <span data-ttu-id="60742-185">**Location**.</span><span class="sxs-lookup"><span data-stu-id="60742-185">Location</span></span> <span data-ttu-id="60742-186">Der Typ der benutzerdefinierten Aktion.</span><span class="sxs-lookup"><span data-stu-id="60742-186">Location - The type of custom action.</span></span> <span data-ttu-id="60742-187">Verwenden Sie `ClientSideExtension.ApplicationCustomizer` für die Application Customizer-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="60742-187">Use "ClientSideExtension.ApplicationCustomizer" for the Application Customizer extension.</span></span>
        * <span data-ttu-id="60742-188">**Properties**.</span><span class="sxs-lookup"><span data-stu-id="60742-188">**Properties**</span></span> <span data-ttu-id="60742-189">Ein optionales JSON-Objekt mit Eigenschaften, die über den Member **this.properties** verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="60742-189">Properties - An optional JSON object that contains properties that will be available via the **this.properties** member.</span></span> <span data-ttu-id="60742-190">In diesem HelloWorld-Beispiel definiert es eine `testMessage`-Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="60742-190">In this HelloWorld example, it defined a ‘testMessage’ property.</span></span>


3. <span data-ttu-id="60742-191">Wechseln Sie zu einer modernen Liste in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="60742-191">Go to a modern list in SharePoint Online.</span></span> <span data-ttu-id="60742-192">Dies kann eine Liste oder eine Bibliothek sein.</span><span class="sxs-lookup"><span data-stu-id="60742-192">This can be either a list or a library.</span></span> <span data-ttu-id="60742-193">Anwendungsanpasser werden auch in modernen Seiten und auf der Seite „Websiteinhalte“ unterstützt.</span><span class="sxs-lookup"><span data-stu-id="60742-193">Application customizers are also supported in modern pages and on the Site Contents page.</span></span> 

4. <span data-ttu-id="60742-194">Erweitern Sie die URL mit den beschriebenen zusätzlichen Abfrageparametern.</span><span class="sxs-lookup"><span data-stu-id="60742-194">Extend the URL with the additional query parameters described.</span></span> <span data-ttu-id="60742-195">Beachten Sie, dass Sie die GUID entsprechend der ID des benutzerdefinierten Application Customizer aktualisieren müssen.</span><span class="sxs-lookup"><span data-stu-id="60742-195">Notice that you'll need to update the GUID to match the ID of your custom Application Customizer.</span></span> 

    <span data-ttu-id="60742-196">Die vollständige URL sollte ähnlich wie im folgenden Beispiel aussehen:</span><span class="sxs-lookup"><span data-stu-id="60742-196">The full URL should look similar to the following:</span></span>

    ```json
    contoso.sharepoint.com/Lists/Contoso/AllItems.aspx?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"testMessage":"Hello as property!"}}}
    ```

5. <span data-ttu-id="60742-197">Wählen Sie **Load debug scripts** aus, um weiter Skripts von Ihrem lokalen Host zu laden.</span><span class="sxs-lookup"><span data-stu-id="60742-197">Choose **Load debug scripts** to continue loading scripts from your local host.</span></span>

    ![Abfragen des Debugging-Manifests für die Seite zulassen](../../../images/ext-app-debug-manifest-message.png)

    <br/>

    <span data-ttu-id="60742-199">Das Dialogmeldung sollte nun auf Ihrer Seite angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="60742-199">You should now see the dialog message on your page.</span></span>

    ![Warnmeldung „Hello as property“](../../../images/ext-app-alert-sp-page.png)

    <span data-ttu-id="60742-201">Dieses Dialogfeld wird von der SharePoint-Framework-Erweiterung ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="60742-201">This dialog is thrown by your SharePoint Framework Extension.</span></span> <span data-ttu-id="60742-202">Da Sie die `testMessage`-Eigenschaft als Teil der Debug-Abfrageparameter bereitgestellt haben, ist diese in der Warnmeldung enthalten.</span><span class="sxs-lookup"><span data-stu-id="60742-202">Note that because you provided the `testMessage` property as part of the debug query parameters, it's included in the alert message.</span></span> <span data-ttu-id="60742-203">Sie können Ihre Erweiterungsinstanzen basierend auf den Clientkomponenteneigenschaften konfigurieren, die für die Instanz im Laufzeitmodus übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="60742-203">You can configure your extension instances based on the client component properties, which are passed for the instance also in runtime mode.</span></span>

> [!NOTE] 
> <span data-ttu-id="60742-204">Wenn Probleme beim Debuggen auftreten, überprüfen Sie die URL-Abfrageparameter, die für die Abfrage verwendet wurden.</span><span class="sxs-lookup"><span data-stu-id="60742-204">If you have issues with debugging, double-check the URL query parameters used for the query.</span></span> <span data-ttu-id="60742-205">In einigen Browsern werden die Parameter codiert, und in einigen Szenarien hat sich Auswirkungen auf das Verhalten.</span><span class="sxs-lookup"><span data-stu-id="60742-205">Some browsers encode the parameters and in some scenarios this affects the behavior.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60742-206">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="60742-206">Next steps</span></span>

<span data-ttu-id="60742-207">Herzlichen Glückwunsch, Sie haben Ihre erste SharePoint Framework-Erweiterung erstellt!</span><span class="sxs-lookup"><span data-stu-id="60742-207">Congratulations, you've gotten your first SharePoint Framework Extension running!</span></span> 

<span data-ttu-id="60742-208">Um mit dem Erstellen der Erweiterung fortzufahren, lesen Sie [Verwenden von Seitenplatzhaltern aus dem Anwendungsanpasser (Hello World, Teil 2)](./using-page-placeholder-with-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="60742-208">To continue building out your extension, see [Using page placeholders from Application Customizer (Hello World part 2)](./using-page-placeholder-with-extensions.md).</span></span> <span data-ttu-id="60742-209">Sie verwenden das gleiche Projekt und nutzen bestimmte Inhaltsplatzhalter zum Ändern der Benutzeroberfläche von SharePoint.</span><span class="sxs-lookup"><span data-stu-id="60742-209">You will use the same project and take advantage of specific content placeholders for modifying the UI of SharePoint.</span></span> <span data-ttu-id="60742-210">Ihnen wird bereits aufgefallen sein, dass der Befehl `gulp serve` immer noch im Konsolenfenster ausgeführt wird (oder in Visual Studio Code, falls Sie den Editor verwenden).</span><span class="sxs-lookup"><span data-stu-id="60742-210">Notice that the `gulp serve` command is still running in your console window (or in Visual Studio Code if you are using the editor).</span></span> <span data-ttu-id="60742-211">Sie können ihn einfach weiterlaufen lassen und zum nächsten Artikel wechseln.</span><span class="sxs-lookup"><span data-stu-id="60742-211">You can continue to let it run while you go to the next article.</span></span>

> [!NOTE]
> <span data-ttu-id="60742-212">Wenn Sie einen Fehler in der Dokumentation oder im SharePoint-Framework finden, melden Sie ihn an das SharePoint Engineering unter Verwendung der [Fehlerliste im sp-dev-docs-Repository](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="60742-212">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="60742-213">Vielen Dank im Voraus für Ihr Feedback.</span><span class="sxs-lookup"><span data-stu-id="60742-213">Thanks for your input advance.</span></span>