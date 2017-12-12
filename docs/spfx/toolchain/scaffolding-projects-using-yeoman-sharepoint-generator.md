# <a name="scaffold-projects-using-yeoman-sharepoint-generator"></a><span data-ttu-id="e8730-101">Erstellen von Gerüsten für Projekte unter Verwendung des Yeoman-Generators von SharePoint</span><span class="sxs-lookup"><span data-stu-id="e8730-101">Scaffold projects using yeoman SharePoint generator</span></span>

<span data-ttu-id="e8730-p101">[Yeoman](http://yeoman.io/) hilft Ihnen bei den ersten Schritten mit neuen Projekten und stellt bewährte Methoden und Tools bereit, mit denen Sie produktiv arbeiten können. Unter Verwendung des Yeoman-Generators von SharePoint können Entwickler Gerüste für neue clientseitige Lösungsprojekte zum Erstellen, Verpacken und Bereitstellen von SharePoint-Lösungen bereitstellen. Der Generator bietet allgemeine Buildtools, Codebausteine und eine allgemeine Textwebsite zum testweisen Hosten von Webparts.</span><span class="sxs-lookup"><span data-stu-id="e8730-p101">[Yeoman](http://yeoman.io/) helps you to kickstart new projects, prescribing best practices and tools to help you stay productive. Using the yeoman SharePoint generator, developers are able to scaffold new client-side solution projects to build, package and deploy SharePoint solutions. The generator provides common build tools, boilerplate code, and a common playground web site to host web parts for testing.</span></span>

## <a name="installing-the-yeoman-sharepoint-generator"></a><span data-ttu-id="e8730-105">Installieren des Yeoman SharePoint-Generators</span><span class="sxs-lookup"><span data-stu-id="e8730-105">Installing the yeoman SharePoint generator</span></span>

<span data-ttu-id="e8730-p102">Der Yeoman SharePoint-Generator steht als Teil des Framework als ein [npm-Paket](https://www.npmjs.com/package/@microsoft/generator-sharepoint) zur Verfügung. Sie können den Generator installieren, indem Sie den folgenden Befehl in einer Konsole ausführen:</span><span class="sxs-lookup"><span data-stu-id="e8730-p102">Yeoman SharePoint generator is available as part of the framework as a [npm package](https://www.npmjs.com/package/@microsoft/generator-sharepoint). You can install the generator by executing the following command in a console:</span></span>

```
npm install @microsoft/generator-sharepoint -g
```

><span data-ttu-id="e8730-p103">**Hinweis:** Der Yeoman-Generator für SharePoint ist für die globale Bereitstellung mit der Erstversion General Availability (GA) vorgesehen. Bei lokaler Installation im Projekt treten bekannte Probleme auf, die nach der GA-Version behoben werden.</span><span class="sxs-lookup"><span data-stu-id="e8730-p103">**Note:** Yeoman generator for SharePoint is targeted to get deployed globally with the initial General Availability (GA) version. There are some known issues if it's installed locally to the project, which are planned to be addressed post GA.</span></span>

<span data-ttu-id="e8730-110">Es wird empfohlen, dass Sie [die Einrichtung Ihrer Entwicklungsumgebung](../set-up-your-development-environment.md) befolgen, um Ihren Computer mit dem vollständigen Satz der Entwicklertools, einschließlich Yeoman SharePoint-Generator, zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="e8730-110">It is recommended you follow the [set up your development environment](../set-up-your-development-environment.md) to configure your machine with the complete set of developer tools, including yeoman SharePoint generator.</span></span> 

## <a name="using-the-yeoman-sharepoint-generator"></a><span data-ttu-id="e8730-111">Verwenden des Yeoman SharePoint-Generators</span><span class="sxs-lookup"><span data-stu-id="e8730-111">Using the yeoman SharePoint generator</span></span>

<span data-ttu-id="e8730-112">Nach der Installation des Generators können Sie den Generator aufrufen, indem Sie einfach den folgenden Befehl in einer Konsole eingeben:</span><span class="sxs-lookup"><span data-stu-id="e8730-112">Once the generator is installed, you can invoke the generator by just typing the following command in a console:</span></span>

```
yo
```

<span data-ttu-id="e8730-p104">Der Befehl führt alle der auf Ihrem Computer verfügbaren Generatoren auf. Wählen Sie `@microsoft/sharepoint` aus, um den SharePoint-Generator aufzurufen, und fahren Sie mit den Aufforderungen fort, um die clientseitige Lösung erfolgreich zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="e8730-p104">The command will list all of the generators available in your machine. Select the `@microsoft/sharepoint` to invoke the SharePoint generator and continue with the prompts to successfully create your client-side solution:</span></span>

![Yeoman SharePoint-Generator](../../images/yeoman-sp-generator.png)

## <a name="available-command-line-options-for-the-generator"></a><span data-ttu-id="e8730-116">Verfügbare Befehlszeilenoptionen für den Generator</span><span class="sxs-lookup"><span data-stu-id="e8730-116">Available command line options for the generator</span></span>

<span data-ttu-id="e8730-117">Sie können die im Yeoman SharePoint-Generator verfügbaren Befehlszeilenoptionen verwenden, um Gerüste für Projekte in einem Befehl anstelle der Aufforderungen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="e8730-117">You can use the command line options available with the yeoman SharePoint generator to scaffold projects in one command instead of going through the prompts. Execute the following command to see the list of  command line options available for the SharePoint generator:</span></span> <span data-ttu-id="e8730-118">Führen Sie den folgenden Befehl aus, um die Liste der für den SharePoint-Generator verfügbaren Befehlszeilenoptionen anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="e8730-118">Execute the following command to see the list of command line options available for the SharePoint generator:</span></span>

```
yo @microsoft/generator-sharepoint --help
```

![Befehlszeilenoptionen für den Yeoman SharePoint-Generator ](../../images/yeoman-sp-cmdline-options.png)

<span data-ttu-id="e8730-120">Option</span><span class="sxs-lookup"><span data-stu-id="e8730-120">Option</span></span> | <span data-ttu-id="e8730-121">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="e8730-121">Description</span></span> 
-----|------
<span data-ttu-id="e8730-122">--help</span><span class="sxs-lookup"><span data-stu-id="e8730-122">Help</span></span>|<span data-ttu-id="e8730-123">Ausgabe der Generator-Optionen und -Nutzung.</span><span class="sxs-lookup"><span data-stu-id="e8730-123">Print the generator's options and usage.</span></span>
<span data-ttu-id="e8730-124">--skip-cache</span><span class="sxs-lookup"><span data-stu-id="e8730-124">--skip-cache</span></span>|<span data-ttu-id="e8730-125">Antworten der Eingabeaufforderungen werden nicht gespeichert.</span><span class="sxs-lookup"><span data-stu-id="e8730-125">Do not remember prompt answers.</span></span> <span data-ttu-id="e8730-126">Standard: *False*.</span><span class="sxs-lookup"><span data-stu-id="e8730-126">Default: *False*</span></span>
<span data-ttu-id="e8730-127">--skip-install</span><span class="sxs-lookup"><span data-stu-id="e8730-127">--skip-install</span></span>|<span data-ttu-id="e8730-128">Abhängigkeiten werden nicht automatisch installiert.</span><span class="sxs-lookup"><span data-stu-id="e8730-128">Do no automatically install dependencies.</span></span> <span data-ttu-id="e8730-129">Standard: *False*.</span><span class="sxs-lookup"><span data-stu-id="e8730-129">Default: *False*</span></span>
<span data-ttu-id="e8730-130">--componentType</span><span class="sxs-lookup"><span data-stu-id="e8730-130">--componentType</span></span>|<span data-ttu-id="e8730-131">Der Typ der Komponente.</span><span class="sxs-lookup"><span data-stu-id="e8730-131">The type of component.</span></span> <span data-ttu-id="e8730-132">Aktuell werden „Webpart“ oder „Erweiterung“ unterstützt.</span><span class="sxs-lookup"><span data-stu-id="e8730-132">Currently "webpart" or "extension" is supported</span></span>
<span data-ttu-id="e8730-133">--componentDescription</span><span class="sxs-lookup"><span data-stu-id="e8730-133">--componentDescription</span></span>|<span data-ttu-id="e8730-134">Beschreibung der Komponente.</span><span class="sxs-lookup"><span data-stu-id="e8730-134">Description of the component.</span></span>
<span data-ttu-id="e8730-135">--componentName</span><span class="sxs-lookup"><span data-stu-id="e8730-135">--componentName</span></span>|<span data-ttu-id="e8730-136">Name der Komponente.</span><span class="sxs-lookup"><span data-stu-id="e8730-136">Name of the component.</span></span>
<span data-ttu-id="e8730-137">--framework</span><span class="sxs-lookup"><span data-stu-id="e8730-137">--framework</span></span>|<span data-ttu-id="e8730-p109">Für die Lösung zu verwendendes Framework. Wählen Sie eine Option aus „Keines“, „React“, „Knockout“ aus.</span><span class="sxs-lookup"><span data-stu-id="e8730-p109">Framework to use for the solution. Choose one from "none", "react", "knockout".</span></span>
<span data-ttu-id="e8730-140">--extensionType</span><span class="sxs-lookup"><span data-stu-id="e8730-140">--extensionType</span></span>|<span data-ttu-id="e8730-141">Der Typ der Erweiterung: Derzeit „ApplicationCustomizer“, „FieldCustomizer“, „ListViewCommandSet“</span><span class="sxs-lookup"><span data-stu-id="e8730-141">The type of extension: Currently "ApplicationCustomizer", "FieldCustomizer", "ListViewCommandSet"</span></span>
<span data-ttu-id="e8730-142">--solutionName</span><span class="sxs-lookup"><span data-stu-id="e8730-142">--solutionName</span></span>|<span data-ttu-id="e8730-143">Clientseitiger Lösungsname und Ordnername.</span><span class="sxs-lookup"><span data-stu-id="e8730-143">Client-side solution name, as well as folder name.</span></span>
<span data-ttu-id="e8730-144">--environment</span><span class="sxs-lookup"><span data-stu-id="e8730-144">Environment</span></span>|<span data-ttu-id="e8730-145">Die Zielumgebung für die Lösung.</span><span class="sxs-lookup"><span data-stu-id="e8730-145">The target environment for the solution.</span></span> <span data-ttu-id="e8730-146">Entweder „onprem“ oder „spo“.</span><span class="sxs-lookup"><span data-stu-id="e8730-146">Either "onprem" or "spo".</span></span>

<span data-ttu-id="e8730-147">Die folgende Tabelle enthält die verfügbaren Argumente.</span><span class="sxs-lookup"><span data-stu-id="e8730-147">Following table lists the available arguments.</span></span>

<span data-ttu-id="e8730-148">Argument</span><span class="sxs-lookup"><span data-stu-id="e8730-148">Argument</span></span> | <span data-ttu-id="e8730-149">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="e8730-149">Description</span></span> | <span data-ttu-id="e8730-150">Typ</span><span class="sxs-lookup"><span data-stu-id="e8730-150">Type</span></span> | <span data-ttu-id="e8730-151">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="e8730-151">Required</span></span> |
-- | -- | -- | -- |
<span data-ttu-id="e8730-152">skipFeatureDeployment</span><span class="sxs-lookup"><span data-stu-id="e8730-152">skipFeatureDeployment</span></span> | <span data-ttu-id="e8730-153">Wenn angegeben, können Mandantenadministratoren festlegen, ob die Komponenten unmittelbar für alle Websites bereitgestellt werden, ohne die Bereitstellung von Features oder das Hinzufügen von Apps zu Websites.</span><span class="sxs-lookup"><span data-stu-id="e8730-153">If specified, allow the tenant admin the choice of being able to deploy the components to all sites immediately without running any feature deployment or adding apps in sites.</span></span> | <span data-ttu-id="e8730-154">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="e8730-154">Boolean</span></span> | <span data-ttu-id="e8730-155">false</span><span class="sxs-lookup"><span data-stu-id="e8730-155">false</span></span> | 

<span data-ttu-id="e8730-156">Nachfolgend sehen Sie ein Beispiel eines Befehls, der eine Lösung mit dem Namen „hello-world“ mit dem Webpart „HelloWorld“ mit dem Framework „React“ nur für SharePoint Online mit optional aktivierter mandantenweiten Bereitstellung erstellt:</span><span class="sxs-lookup"><span data-stu-id="e8730-156">Below is an example of a command that creates a solution called "hello-world" with a web part "HelloWorld" with "react" framework targeted only to SharePoint Online with tenant-scoped deployment optional enabled:</span></span>

```
yo @microsoft/sharepoint --solutionName "hello-world" --framework "react" --componentType "webpart" --componentName "HelloWorld" --componentDescription "HelloWorld web part" --skip-install --environment "spo" skipFeatureDeployment true
```

> <span data-ttu-id="e8730-157">Beachten Sie, dass bei einigen Optionen Abhängigkeiten untereinander bestehen.</span><span class="sxs-lookup"><span data-stu-id="e8730-157">Notice that some of the options have dependencies between each other.</span></span> <span data-ttu-id="e8730-158">Sie können zum Beispiel die Erweiterung nicht mit der lokalen Option erstellen.</span><span class="sxs-lookup"><span data-stu-id="e8730-158">You cannot for example create extension with on-premises option.</span></span>

### <a name="notes-on---skip-install"></a><span data-ttu-id="e8730-159">Hinweise zu --skip-install</span><span class="sxs-lookup"><span data-stu-id="e8730-159">Notes on --skip-install</span></span> 

<span data-ttu-id="e8730-p112">Mithilfe des `--skip-install`-Befehls wird ein Gerüst für das Projekt erstellt, und die Installation von Abhängigkeiten wird übersprungen. Dies bedeutet, dass Sie für ein erfolgreiches Erstellen des Projekts die Abhängigkeiten später installieren müssen, nachdem ein Gerüst für das Projekt erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="e8730-p112">Using the `--skip-install` command will scaffold the project and skip installing dependencies. This means, to successfully build the project, you will need to install the dependencies later once the project is scaffolded.</span></span> 

<span data-ttu-id="e8730-p113">Wenn Sie versuchen, das Projekt zu erstellen, ohne die Abhängigkeiten zu installieren, wird der folgende Fehler zurückgegeben. Dies deutet darauf hin, dass Sie die Abhängigkeiten installieren müssen, bevor Sie das Projekt erstellen:</span><span class="sxs-lookup"><span data-stu-id="e8730-p113">If you try to build your project without installing the dependencies, then you will get the following error. This indicates you need to install the dependencies before building the project:</span></span>

```
Local gulp not found in ~/<project-name>
Try running: npm install gulp
```

<span data-ttu-id="e8730-164">Zum Installieren der Abhängigkeiten können Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="e8730-164">You can execute the following command to install the dependencies:</span></span>

```
npm install
```
