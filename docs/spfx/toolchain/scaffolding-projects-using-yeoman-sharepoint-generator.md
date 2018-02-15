---
title: "Erstellen von Gerüsten für Projekte unter Verwendung des Yeoman-Generators von SharePoint"
description: "Unter Verwendung des Yeoman-Generators von SharePoint können Sie Gerüste für neue clientseitige Lösungsprojekte zum Erstellen, Verpacken und Bereitstellen von SharePoint-Lösungen bereitstellen."
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: ac69ce5030289fefce1563fb03b6b0fb1466d470
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="scaffold-projects-by-using-yeoman-sharepoint-generator"></a><span data-ttu-id="44356-103">Erstellen von Gerüsten für Projekte unter Verwendung des Yeoman-Generators von SharePoint</span><span class="sxs-lookup"><span data-stu-id="44356-103">Scaffold projects using yeoman SharePoint generator</span></span>

<span data-ttu-id="44356-104">[Yeoman](http://yeoman.io/) hilft Ihnen bei den ersten Schritten mit neuen Projekten und stellt bewährte Methoden und Tools bereit, mit denen Sie produktiv arbeiten können.</span><span class="sxs-lookup"><span data-stu-id="44356-104">[Yeoman](http://yeoman.io/) helps you kick-start new projects, and prescribes best practices and tools to help you stay productive.</span></span> <span data-ttu-id="44356-105">Unter Verwendung des Yeoman-Generators von SharePoint können Entwickler Gerüste für neue clientseitige Lösungsprojekte zum Erstellen, Verpacken und Bereitstellen von SharePoint-Lösungen bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="44356-105">Using the Yeoman SharePoint generator, developers are able to scaffold new client-side solution projects to build, package, and deploy SharePoint solutions.</span></span> <span data-ttu-id="44356-106">Der Generator bietet allgemeine Buildtools, Codebausteine und eine allgemeine Textwebsite zum testweisen Hosten von Webparts.</span><span class="sxs-lookup"><span data-stu-id="44356-106">The generator provides common build tools, common boilerplate code, and a common playground website to host web parts for testing.</span></span>

## <a name="install-the-yeoman-sharepoint-generator"></a><span data-ttu-id="44356-107">Installieren des Yeoman SharePoint-Generators</span><span class="sxs-lookup"><span data-stu-id="44356-107">Install Yeoman SharePoint generator</span></span>

<span data-ttu-id="44356-108">Der Yeoman SharePoint-Generator steht als Teil des Framework als ein [npm-Paket](https://www.npmjs.com/package/@microsoft/generator-sharepoint) zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="44356-108">Yeoman SharePoint generator is available as part of the framework as a [npm package](https://www.npmjs.com/package/@microsoft/generator-sharepoint). You can install the generator by executing the following command in a console:</span></span> <span data-ttu-id="44356-109">Sie können den Generator installieren, indem Sie den folgenden Befehl in einer Konsole ausführen:</span><span class="sxs-lookup"><span data-stu-id="44356-109">Yeoman SharePoint generator is available as part of the framework as a npm package. You can install the generator by executing the following command in a console:</span></span>

```
npm install @microsoft/generator-sharepoint -g
```

> [!NOTE] 
> <span data-ttu-id="44356-110">Der Yeoman-Generator für SharePoint ist für die globale Bereitstellung mit der Erstversion General Availability (GA) vorgesehen.</span><span class="sxs-lookup"><span data-stu-id="44356-110">Yeoman generator for SharePoint is targeted to get deployed globally with the initial General Availability (GA) version.</span></span> <span data-ttu-id="44356-111">Bei lokaler Installation im Projekt treten bekannte Probleme auf, die nach der GA-Version behoben werden.</span><span class="sxs-lookup"><span data-stu-id="44356-111">There are some known issues if it's installed locally to the project, which are planned to be addressed post GA.</span></span>

<span data-ttu-id="44356-112">Es wird empfohlen, dass Sie die Anweisungen zur [die Einrichtung Ihrer Entwicklungsumgebung](../set-up-your-development-environment.md) befolgen, um Ihren Computer mit dem vollständigen Satz der Entwicklertools, einschließlich Yeoman SharePoint-Generator, zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="44356-112">It is recommended you follow the [set up your development environment](../set-up-your-development-environment.md) to configure your machine with the complete set of developer tools, including yeoman SharePoint generator.</span></span> 

## <a name="use-the-yeoman-sharepoint-generator"></a><span data-ttu-id="44356-113">Verwenden des Yeoman SharePoint-Generators</span><span class="sxs-lookup"><span data-stu-id="44356-113">Use the Yeoman SharePoint generator</span></span>

<span data-ttu-id="44356-114">Nach der Installation des Generators können Sie den Generator aufrufen, indem Sie einfach den folgenden Befehl in einer Konsole eingeben:</span><span class="sxs-lookup"><span data-stu-id="44356-114">Once the generator is installed, you can invoke the generator by just typing the following command in a console:</span></span>

```
yo
```

<span data-ttu-id="44356-115">Der Befehl führt alle der auf Ihrem Computer verfügbaren Generatoren auf.</span><span class="sxs-lookup"><span data-stu-id="44356-115">The command lists all the generators available on your machine.</span></span> <span data-ttu-id="44356-116">Wählen Sie `@microsoft/sharepoint` aus, um den SharePoint-Generator aufzurufen, und fahren Sie mit den Aufforderungen fort, um die clientseitige Lösung erfolgreich zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="44356-116">The command will list all of the generators available in your machine. Select the `@microsoft/sharepoint` to invoke the SharePoint generator and continue with the prompts to successfully create your client-side solution:</span></span>

![Yeoman SharePoint-Generator](../../images/yeoman-sp-generator.png)


## <a name="use-available-command-line-options-for-the-generator"></a><span data-ttu-id="44356-118">Verwenden der verfügbaren Befehlszeilenoptionen für den Generator</span><span class="sxs-lookup"><span data-stu-id="44356-118">Use available command-line options for the generator</span></span>

<span data-ttu-id="44356-119">Sie können die im Yeoman SharePoint-Generator verfügbaren Befehlszeilenoptionen verwenden, um Gerüste für Projekte in einem Befehl anstelle der Aufforderungen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="44356-119">You can use the command line options available with the yeoman SharePoint generator to scaffold projects in one command instead of going through the prompts.</span></span> <span data-ttu-id="44356-120">Führen Sie den folgenden Befehl aus, um die Liste der für den SharePoint-Generator verfügbaren Befehlszeilenoptionen anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="44356-120">Execute the following command to see the list of command line options available for the SharePoint generator:</span></span>

```
yo @microsoft/generator-sharepoint --help
```

<br/>

![Befehlszeilenoptionen für den Yeoman SharePoint-Generator ](../../images/yeoman-sp-cmdline-options.png)

<br/>

<span data-ttu-id="44356-122">**Befehlszeilenoptionen**</span><span class="sxs-lookup"><span data-stu-id="44356-122">**Command-line options**</span></span>

<span data-ttu-id="44356-123">Option</span><span class="sxs-lookup"><span data-stu-id="44356-123">Option</span></span> | <span data-ttu-id="44356-124">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="44356-124">Description</span></span> 
-----|------
<span data-ttu-id="44356-125">--help</span><span class="sxs-lookup"><span data-stu-id="44356-125">--help</span></span>|<span data-ttu-id="44356-126">Ausgabe der Generator-Optionen und -Nutzung.</span><span class="sxs-lookup"><span data-stu-id="44356-126">Print the generator's options and usage.</span></span>
<span data-ttu-id="44356-127">--skip-cache</span><span class="sxs-lookup"><span data-stu-id="44356-127">--skip-cache</span></span>|<span data-ttu-id="44356-128">Antworten der Eingabeaufforderungen werden nicht gespeichert.</span><span class="sxs-lookup"><span data-stu-id="44356-128">Do not remember prompt answers.</span></span> <span data-ttu-id="44356-129">Standard: *False*.</span><span class="sxs-lookup"><span data-stu-id="44356-129">Default: *false*.</span></span>
<span data-ttu-id="44356-130">--skip-install</span><span class="sxs-lookup"><span data-stu-id="44356-130">--skip-install</span></span>|<span data-ttu-id="44356-131">Abhängigkeiten werden nicht automatisch installiert.</span><span class="sxs-lookup"><span data-stu-id="44356-131">Do not automatically install dependencies.</span></span> <span data-ttu-id="44356-132">Standard: *False*.</span><span class="sxs-lookup"><span data-stu-id="44356-132">Default: *false*.</span></span>
<span data-ttu-id="44356-133">--componentType</span><span class="sxs-lookup"><span data-stu-id="44356-133">--componentType</span></span>|<span data-ttu-id="44356-134">Der Typ der Komponente.</span><span class="sxs-lookup"><span data-stu-id="44356-134">The type of component.</span></span> <span data-ttu-id="44356-135">Aktuell werden „Webpart“ oder „Erweiterung“ unterstützt.</span><span class="sxs-lookup"><span data-stu-id="44356-135">Currently "webpart" or "extension" is supported</span></span>
<span data-ttu-id="44356-136">--componentDescription</span><span class="sxs-lookup"><span data-stu-id="44356-136">--componentDescription</span></span>|<span data-ttu-id="44356-137">Beschreibung der Komponente.</span><span class="sxs-lookup"><span data-stu-id="44356-137">Description of the component.</span></span>
<span data-ttu-id="44356-138">--componentName</span><span class="sxs-lookup"><span data-stu-id="44356-138">--componentName</span></span>|<span data-ttu-id="44356-139">Name der Komponente.</span><span class="sxs-lookup"><span data-stu-id="44356-139">Name of the component.</span></span>
<span data-ttu-id="44356-140">--framework</span><span class="sxs-lookup"><span data-stu-id="44356-140">--framework</span></span>|<span data-ttu-id="44356-p109">Für die Lösung zu verwendendes Framework. Wählen Sie eine Option aus „Keines“, „React“, „Knockout“ aus.</span><span class="sxs-lookup"><span data-stu-id="44356-p109">Framework to use for the solution. Choose one from "none", "react", "knockout".</span></span>
<span data-ttu-id="44356-143">--extensionType</span><span class="sxs-lookup"><span data-stu-id="44356-143">--extensionType</span></span>|<span data-ttu-id="44356-144">Der Typ der Erweiterung: Derzeit „ApplicationCustomizer“, „FieldCustomizer“, „ListViewCommandSet“</span><span class="sxs-lookup"><span data-stu-id="44356-144">The type of extension: Currently "ApplicationCustomizer", "FieldCustomizer", "ListViewCommandSet"</span></span>
<span data-ttu-id="44356-145">--solutionName</span><span class="sxs-lookup"><span data-stu-id="44356-145">--solutionName</span></span>|<span data-ttu-id="44356-146">Clientseitiger Lösungsname und Ordnername.</span><span class="sxs-lookup"><span data-stu-id="44356-146">Client-side solution name, as well as folder name.</span></span>
<span data-ttu-id="44356-147">--environment</span><span class="sxs-lookup"><span data-stu-id="44356-147">--environment</span></span>|<span data-ttu-id="44356-148">Die Zielumgebung für die Lösung.</span><span class="sxs-lookup"><span data-stu-id="44356-148">The target environment for the solution.</span></span> <span data-ttu-id="44356-149">Entweder „onprem“ oder „spo“.</span><span class="sxs-lookup"><span data-stu-id="44356-149">Either "onprem" or "spo".</span></span>

<br/>

<span data-ttu-id="44356-150">**Verfügbare Argumente**</span><span class="sxs-lookup"><span data-stu-id="44356-150">**Available arguments**</span></span>

<span data-ttu-id="44356-151">Argument</span><span class="sxs-lookup"><span data-stu-id="44356-151">Argument</span></span> | <span data-ttu-id="44356-152">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="44356-152">Description</span></span> | <span data-ttu-id="44356-153">Typ</span><span class="sxs-lookup"><span data-stu-id="44356-153">Type</span></span> | <span data-ttu-id="44356-154">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="44356-154">Required</span></span> |
-- | -- | -- | -- |
<span data-ttu-id="44356-155">skipFeatureDeployment</span><span class="sxs-lookup"><span data-stu-id="44356-155">skipFeatureDeployment</span></span> | <span data-ttu-id="44356-156">Wenn angegeben, können Mandantenadministratoren festlegen, ob die Komponenten unmittelbar für alle Websites bereitgestellt werden, ohne die Bereitstellung von Features oder das Hinzufügen von Apps zu Websites.</span><span class="sxs-lookup"><span data-stu-id="44356-156">If specified, allow the tenant admin the choice of being able to deploy the components to all sites immediately without running any feature deployment or adding apps in sites.</span></span> | <span data-ttu-id="44356-157">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="44356-157">Boolean</span></span> | <span data-ttu-id="44356-158">false</span><span class="sxs-lookup"><span data-stu-id="44356-158">false</span></span> | 

<br/>

<span data-ttu-id="44356-159">Nachfolgend sehen Sie ein Beispiel eines Befehls, der eine Lösung mit dem Namen „hello-world“ erstellt.</span><span class="sxs-lookup"><span data-stu-id="44356-159">Below is an example of a command that creates a solution called "hello-world" with a web part "HelloWorld" with "react" framework:</span></span>
- <span data-ttu-id="44356-160">Das Webpart "HelloWorld"</span><span class="sxs-lookup"><span data-stu-id="44356-160">A web part "HelloWorld"</span></span> 
- <span data-ttu-id="44356-161">Das "React"-Framework, das nur auf SharePoint Online abzielt</span><span class="sxs-lookup"><span data-stu-id="44356-161">The "react" framework targeted only to SharePoint Online</span></span> 
- <span data-ttu-id="44356-162">Mandantenweite Bereitstellung (optional aktiviert)</span><span class="sxs-lookup"><span data-stu-id="44356-162">Tenant-scoped deployment optional enabled</span></span>

<span data-ttu-id="44356-163">Beachten Sie, dass bei einigen Optionen Abhängigkeiten untereinander bestehen.</span><span class="sxs-lookup"><span data-stu-id="44356-163">Notice that some of the options have dependencies between each other.</span></span> <span data-ttu-id="44356-164">Sie können zum Beispiel die Erweiterung nicht mit der lokalen Option erstellen.</span><span class="sxs-lookup"><span data-stu-id="44356-164">You cannot for example create extension with on-premises option.</span></span>

```
yo @microsoft/sharepoint 
--solutionName "hello-world" 
--framework "react" 
--componentType "webpart" 
--componentName "HelloWorld" 
--componentDescription "HelloWorld web part" 
--skip-install 
--environment "spo" skipFeatureDeployment true
```

<br/>

> [!NOTE]
> <span data-ttu-id="44356-165">Mithilfe des `--skip-install`-Befehls wird ein Gerüst für das Projekt erstellt, und die Installation von Abhängigkeiten wird übersprungen.</span><span class="sxs-lookup"><span data-stu-id="44356-165">Using the `--skip-install` command scaffolds the project and skips installing dependencies.</span></span> <span data-ttu-id="44356-166">Dies bedeutet, dass Sie für ein erfolgreiches Erstellen des Projekts die Abhängigkeiten später installieren müssen, nachdem ein Gerüst für das Projekt erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="44356-166">Using the  command will scaffold the project and skip installing dependencies. This means, to successfully build the project, you will need to install the dependencies later once the project is scaffolded.</span></span> 

> <span data-ttu-id="44356-167">Wenn Sie versuchen, das Projekt zu erstellen, ohne die Abhängigkeiten zu installieren, wird der folgende Fehler zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="44356-167">If you try to build your project without installing the dependencies, then you will get the following error. This indicates you need to install the dependencies before building the project:</span></span> <span data-ttu-id="44356-168">Dies deutet darauf hin, dass Sie die Abhängigkeiten installieren müssen, bevor Sie das Projekt erstellen:</span><span class="sxs-lookup"><span data-stu-id="44356-168">This indicates that you need to install the dependencies before building the project:</span></span>

> ```
> Local gulp not found in ~/<project-name>
> Try running: npm install gulp
> ```

> <span data-ttu-id="44356-169">Zum Installieren der Abhängigkeiten können Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="44356-169">You can execute the following command to install the dependencies:</span></span>

> ```
> npm install
> ```


## <a name="see-also"></a><span data-ttu-id="44356-170">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="44356-170">See also</span></span>

- [<span data-ttu-id="44356-171">SharePoint Framework-Toolkette</span><span class="sxs-lookup"><span data-stu-id="44356-171">SharePoint Framework Toolchain</span></span>](sharepoint-framework-toolchain.md)
- [<span data-ttu-id="44356-172">Entwicklungstools und -bibliotheken für das SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="44356-172">SharePoint Framework development tools and libraries</span></span>](../tools-and-libraries.md)
- [<span data-ttu-id="44356-173">SharePoint Framework-Übersicht</span><span class="sxs-lookup"><span data-stu-id="44356-173">SharePoint Framework Extensions Overview</span></span>](../sharepoint-framework-overview.md)
