---
title: Aktualisieren von SharePoint-Framework-Paketen
ms.date: 11/29/2017
ms.prod: sharepoint
ms.openlocfilehash: 665c22ffea27a8b62d433cfb4932625664638e0a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="update-sharepoint-framework-packages"></a><span data-ttu-id="b8dfd-102">Aktualisieren von SharePoint-Framework-Paketen</span><span class="sxs-lookup"><span data-stu-id="b8dfd-102">Update SharePoint Framework packages</span></span>

<span data-ttu-id="b8dfd-103">Die SharePoint-Tools für die clientseitige Entwicklung verwenden den [npm]((https://www.npmjs.com/))-Paket-Manager, um Abhängigkeiten und andere erforderliche JavaScript-Hilfsprogramme zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-103">SharePoint client-side development tools use the [npm]((https://www.npmjs.com/)) package manager to manage dependencies and other required JavaScript helpers. npm is typically included as part of Node.js setup.</span></span> <span data-ttu-id="b8dfd-104">npm ist in der Regel als Teil des Node.js-Setups enthalten.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-104">npm is typically included as part of Node.js setup.</span></span>

<span data-ttu-id="b8dfd-105">Beim Erstellen einer neuen clientseitigen Lösung ruft der Yeoman-Generator für SharePoint die neuesten SharePoint-Framework-Pakete ab, die für Ihr clientseitiges Projekt erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-105">When you create a new client-side solution, the yeoman generator for SharePoint fetches the latest SharePoint Framework packages required for your client-side project.</span></span> <span data-ttu-id="b8dfd-106">Ihre vorhandenen Pakete sind ggf. veraltet und möglicherweise stehen zum Erstellen Ihres Projekts neue Versionen der Pakete zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-106">As you build your project, your existing packages could be outdated as there could be new versions of one or more packages available.</span></span> <span data-ttu-id="b8dfd-107">Entsprechend den [Versionshinweisen]((https://aka.ms/spfx-release-notes)) für eine bestimmte Version oder das neueste Paket können Sie die in Ihrem Projekt verwendeten SharePoint-Framework-Pakete aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-107">Based on the [release notes]((https://aka.ms/spfx-release-notes)) for a particular release or the latest package, you may decide to update your SharePoint Framework packages used in your project.</span></span> <span data-ttu-id="b8dfd-108">SharePoint Framework-Pakete enthalten die npm-Pakete, die Sie in Ihrem Projekt installiert haben (Beispiel: [@microsoft/sp-core-library]((https://www.npmjs.com/)package/@microsoft/sp-core-library)), sowie die global installierten npm-Pakete (Beispiel: [@microsoft/generator-sharepoint]((https://www.npmjs.com/)package/@microsoft/generator-sharepoint)).</span><span class="sxs-lookup"><span data-stu-id="b8dfd-108">SharePoint Framework packages include both the npm packages you have installed in your project, for example: [@microsoft/sp-core-library]((https://www.npmjs.com/)package/@microsoft/sp-core-library), and npm packages installed globally, for example: [@microsoft/generator-sharepoint]((https://www.npmjs.com/)package/@microsoft/generator-sharepoint).</span></span> 

> [!TIP]
> <span data-ttu-id="b8dfd-109">Obwohl nicht erforderlich, empfiehlt es sich, die SharePoint Framework-Pakete regelmäßig zu aktualisieren, um alle neuesten Änderungen und Updates zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-109">While it may not be required, it is recommended you update the SharePoint Framework packages every so often so that you can get the latest changes and fixes that have been released.</span></span>

## <a name="find-outdated-packages-in-your-project"></a><span data-ttu-id="b8dfd-110">Suche nach veralteten Paketen im Projekt</span><span class="sxs-lookup"><span data-stu-id="b8dfd-110">Find outdated packages in your project</span></span>

<span data-ttu-id="b8dfd-111">Führen Sie in einer Konsole im selben Verzeichnis wie das Projekt den folgenden Befehl aus, um nach veralteten Paketen in Ihrem clientseitigen Projekt zu suchen, einschließlich SharePoint Framework-Paketen und anderen, von denen Ihr Projekt abhängt.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-111">To find the outdated packages in your client-side project, including SharePoint Framework and other packages your project depends on, run the following command in a console in the same directory as your project.</span></span> 

```sh
npm outdated
```

<span data-ttu-id="b8dfd-112">Der Befehl listet die folgenden Informationen zu den Paketen auf, von denen Ihr Projekt abhängt.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-112">The command will list the following information about the packages your project depends on. This information is looked up from the  file located in the root of your project directory and npm registry.</span></span> <span data-ttu-id="b8dfd-113">Diese Informationen werden der Datei `package.json` im Stammverzeichnis des Projekts und der npm-Registry entnommen.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-113">The command will list the following information about the packages your project depends on. This information is looked up from the `package.json` file located in the root of your project directory and npm registry.</span></span>

* <span data-ttu-id="b8dfd-114">Aktuelle, in Ihrem Projekt installierte Version</span><span class="sxs-lookup"><span data-stu-id="b8dfd-114">Current version installed in your project</span></span>
* <span data-ttu-id="b8dfd-115">Von Ihrem Projekt angeforderte Version (verfügbar in `package.json`)</span><span class="sxs-lookup"><span data-stu-id="b8dfd-115">Version requested by your project (available in `package.json`)</span></span>
* <span data-ttu-id="b8dfd-116">Neueste verfügbare Version</span><span class="sxs-lookup"><span data-stu-id="b8dfd-116">Latest version available</span></span>

![Veraltete NPM-Pakete](../../images/npm-outdated-packages-list.png)

<span data-ttu-id="b8dfd-118">Um die SharePoint Framework Pakete zu identifizieren, suchen Sie nach den Paketnamen, die mit dem folgenden npm-Bereich und -Präfix beginnen:</span><span class="sxs-lookup"><span data-stu-id="b8dfd-118">To identify the SharePoint Framework packages, look for the package names that start with the following npm scope and prefix:</span></span>

```text
@microsoft/sp-
```

<span data-ttu-id="b8dfd-119">Zusammen mit den Framework-Paketen müssen Sie ggf. auch die Pakete `react` und `office-ui-fabric-react` aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-119">Along with the framework packages, you may also need to update `react` and `office-ui-fabric-react` packages.</span></span> <span data-ttu-id="b8dfd-120">Lesen Sie unbedingt die [Versionshinweise]((https://aka.ms/spfx-release-notes)) für die jeweilige Version, um zu erfahren, welche Pakete eine Aktualisierung erfordern, und entsprechend planen zu können.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-120">Along with the framework packages, you may also need to update  and  packages. Make sure you read the [release notes]((https://aka.ms/spfx-release-notes)) for that specific release to infer which packages require updates and plan accordingly.</span></span>

### <a name="using-npm-outdated-with-project-targeting-sharepoint-2016"></a><span data-ttu-id="b8dfd-121">Verwenden veralteter npm-Pakete mit Projekten für SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="b8dfd-121">Using npm outdated with project targeting SharePoint 2016</span></span>

<span data-ttu-id="b8dfd-122">Ab Feature Pack 2 werden SharePoint-Framework-Lösungen in SharePoint 2016 unterstützt.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-122">Starting from Feature Pack 2, SharePoint 2016 supports SharePoint Framework solutions.</span></span> <span data-ttu-id="b8dfd-123">SharePoint 2016 verwendet eine ältere Version von SharePoint-Framework als die Version, die in SharePoint Online verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-123">SharePoint 2016 uses an older version of the SharePoint Framework, than the version available in SharePoint Online.</span></span> <span data-ttu-id="b8dfd-124">Beim Erstellen des Gerüsts für neue Projekte müssen Sie im SharePoint-Framework-Yeoman-Generator angeben, ob Ihre Lösung die aktuelle Version von SharePoint-Framework verwenden und nur mit SharePoint Online verwendet werden kann oder eine ältere Version von SharePoint-Framework verwenden und sowohl mit SharePoint 2016 als auch mit SharePoint Online verwende werden kann.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-124">When scaffolding new projects, the SharePoint Framework Yeoman generator prompts you to choose if your solution should be using the latest version of the SharePoint Framework and be working only with SharePoint Online or if it should use an older version of the SharePoint Framework and work with both SharePoint 2016 and SharePoint Online.</span></span>

<span data-ttu-id="b8dfd-125">Beim Ausführen des `npm outdated`-Befehls in einem Projekt, das sowohl für SharePoint Online als auch für SharePoint 2016 entwickelt wurde, werden die aktuellen Versionen der SharePoint-Framework-Pakete angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-125">When you run the `npm outdated` command in a project targeting both SharePoint Online and SharePoint 2016, it will show you the latest versions of the SharePoint Framework packages.</span></span> <span data-ttu-id="b8dfd-126">Diese Versionen funktionieren jedoch nur mit SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-126">These versions however work only with SharePoint Online.</span></span> <span data-ttu-id="b8dfd-127">Wenn Sie Ihre Lösung für die Verwendung mit den aktuellen Paketen aktualisieren, funktioniert diese nicht länger mit SharePoint 2016.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-127">If you would update your solution to use these latest packages, it would not work with SharePoint 2016 anymore.</span></span>

<span data-ttu-id="b8dfd-128">Beim Arbeiten mit SharePoint-Framework-Lösungen, die mit lokalen SharePoint-Bereitstellungen kompatibel sind, sollten Sie immer prüfen, welche Patchebene die SharePoint-Zielfarm aufweist und welche Version von SharePoint-Framework unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-128">When working with SharePoint Framework solutions compatible with SharePoint hosted on-premises, you should always verify which patch level the target SharePoint farm has and which version of the SharePoint Framework it supports.</span></span>

### <a name="update-packages"></a><span data-ttu-id="b8dfd-129">Aktualisieren der Pakete</span><span class="sxs-lookup"><span data-stu-id="b8dfd-129">Update packages</span></span>

<span data-ttu-id="b8dfd-130">Beim Aktualisieren von Paketen auf neuere Versionen sollten Sie immer Ihren Paket-Manager (npm oder Yarn) verwenden.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-130">When updating packages to newer versions, you should always use your package manager (npm or Yarn).</span></span> <span data-ttu-id="b8dfd-131">Bearbeiten Sie die Datei `package.json` nicht manuell.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-131">You should not edit the `package.json` file manually.</span></span> <span data-ttu-id="b8dfd-132">Wenn Sie, wie empfohlen, eine Sperrdatei verwenden, werden die Änderungen ignoriert, die Sie an der Datei `package.json` vornehmen.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-132">If you follow the recommended practice of using a lock file, your changes to the `package.json` file would be ignored.</span></span>

<span data-ttu-id="b8dfd-133">Beginnen Sie damit, zu ermitteln, welche Pakete aktualisiert werden sollen und welche neuere Version verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-133">Start with identifying which packages need updating and which newer version you want to use.</span></span> <span data-ttu-id="b8dfd-134">Beachten Sie, dass es ggf. nicht möglich ist, die neueste Version des angegebenen Pakets zu verwenden, da sie möglicherweise nicht mit anderen SharePoint-Framework-Abhängigkeiten wie TypeScript kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-134">Please note, that it might not always be possible for you to use the latest version of the given package as it might be incompatible with other SharePoint Framework dependencies, such as TypeScript.</span></span>

<span data-ttu-id="b8dfd-135">Führen Sie für jedes Paket, das Sie aktualisieren möchten, den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="b8dfd-135">For each package that you want to update, run the following command:</span></span>

```sh
npm install mypackage@newversion --save
```

<span data-ttu-id="b8dfd-136">Wenn Sie zum Beispiel bisher AngularJS Version v1.5.9 verwendet haben und auf Version 1.6.5 aktualisieren möchten, müssen Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="b8dfd-136">For example, if you were using AngularJS version v1.5.9 and wanted to update to version 1.6.5, you would run:</span></span>

```sh
npm install angular@1.6.5 --save
```

<span data-ttu-id="b8dfd-137">Beim Aktualisieren des Pakets mit npm werden die angegebene Version des Pakets in Ihrem Projekt installiert sowie die Versionsnummer in den Abhängigkeiten der Datei „package.json“ und der im Projekt verwendeten Sperrdatei aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-137">Updating the package using npm will install the specified version of the package in your project, update the version number in the package.json file dependencies and the lock file used in your project.</span></span>

<span data-ttu-id="b8dfd-138">Führen Sie danach den folgenden Befehl aus, um alte Buildartefakte zu entfernen:</span><span class="sxs-lookup"><span data-stu-id="b8dfd-138">Once the packages are installed, execute the following command to clean up any old build artifacts:</span></span>

```sh
gulp clean
```

### <a name="update-your-code"></a><span data-ttu-id="b8dfd-139">Aktualisieren des Codes</span><span class="sxs-lookup"><span data-stu-id="b8dfd-139">Update your code</span></span>

<span data-ttu-id="b8dfd-140">Bei wichtigen API-Änderungen müssen Sie ggf. den vorhandenen Projektcode und die Konfigurationsdateien aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-140">Depending on breaking API changes, you may have to update your existing project code and config files.</span></span> <span data-ttu-id="b8dfd-141">In jeder Version werden wichtige Änderungen sowie die an Ihrem Code erforderlichen Änderungen in den [Versionshinweisen]((https://aka.ms/spfx-release-notes)) hervorgehoben.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-141">For each release, the [release notes]((https://aka.ms/spfx-release-notes)) will highlight any such breaking changes and the modifications required to your existing code.</span></span> <span data-ttu-id="b8dfd-142">Sie müssen den Code mit diesen Fehlerbehebungen aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-142">You will need to make sure you update your code with those fixes.</span></span>

<span data-ttu-id="b8dfd-143">Sie können das Projekt jederzeit erstellen, um zu erfahren, ob Fehler und Warnungen vorliegen. Führen Sie dazu den Befehl in einer Konsole im Projektverzeichnis aus:</span><span class="sxs-lookup"><span data-stu-id="b8dfd-143">You can always build the project to see if you have any errors and warnings by running the command in a console in your project directory:</span></span>

```sh
gulp build
```

## <a name="update-yeoman-generator-for-sharepoint"></a><span data-ttu-id="b8dfd-144">Aktualisieren des Yeoman-Generators für SharePoint</span><span class="sxs-lookup"><span data-stu-id="b8dfd-144">Update yeoman generator for SharePoint</span></span>

<span data-ttu-id="b8dfd-145">Wenn Sie den SharePoint-Framework-Yeoman-Generator global installiert haben, können Sie mit dem folgenden Befehl ermitteln, ob eine Aktualisierung erforderlich ist:</span><span class="sxs-lookup"><span data-stu-id="b8dfd-145">If you have installed the SharePoint Framework Yeoman generator globally, you can find out if it requires updating by running the following command:</span></span>

```sh
npm outdated -g
```

<span data-ttu-id="b8dfd-p110">Der Befehl listet die folgenden Informationen zu den Paketen auf, die global auf Ihrem Computer installiert sind. Diese Informationen stammen aus den auf Ihrem Computer und in der npm-Registry installierten Versionen.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-p110">The command will list the following information about the packages installed globally in your machine. This information is looked up from the versions installed in your machine and the npm registry.</span></span>

* <span data-ttu-id="b8dfd-148">Aktuelle, global auf Ihrem Computer installierte Version</span><span class="sxs-lookup"><span data-stu-id="b8dfd-148">Current version installed globally in your machine</span></span>
* <span data-ttu-id="b8dfd-149">Von Ihnen bei der Installation angeforderte Version</span><span class="sxs-lookup"><span data-stu-id="b8dfd-149">Version requested by you when you installed</span></span>
* <span data-ttu-id="b8dfd-150">Neueste verfügbare Version</span><span class="sxs-lookup"><span data-stu-id="b8dfd-150">Latest version available</span></span>

![Veraltete globale npm-Pakete](../../images/npm-outdated-global-packages-list.png)

<span data-ttu-id="b8dfd-152">Um das Generator-Paket zu ermitteln, suchen Sie nach folgendem Paketnamen:</span><span class="sxs-lookup"><span data-stu-id="b8dfd-152">To identify the generator package, look for the following package name:</span></span>

```sh
@microsoft/generator-sharepoint
```

### <a name="update-generator-package"></a><span data-ttu-id="b8dfd-153">Aktualisieren des Generator-Pakets</span><span class="sxs-lookup"><span data-stu-id="b8dfd-153">Update generator package</span></span>

<span data-ttu-id="b8dfd-154">Öffnen Sie Ihre bevorzugte Konsole und führen Sie den folgenden Befehl aus, um den Generator auf die neueste veröffentlichte Version zu aktualisieren:</span><span class="sxs-lookup"><span data-stu-id="b8dfd-154">Open your favorite console and execute the following command to update the generator to its latest published version:</span></span>

```sh
npm install @microsoft/generator-sharepoint@latest -g
```

<span data-ttu-id="b8dfd-155">Mit dem Befehl wird der Yeoman-Generator für SharePoint zusammen mit allen Abhängigkeiten auf die neueste veröffentlichte Version aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="b8dfd-155">The command will update the yeoman generator for SharePoint to the latest published version along with its depedencies. You can validate this by executing the following command in the console:</span></span> <span data-ttu-id="b8dfd-156">Sie können dies überprüfen, indem Sie den folgenden Befehl in der Verwaltungskonsole ausführen:</span><span class="sxs-lookup"><span data-stu-id="b8dfd-156">You can validate this by executing the following command in the console:</span></span>

```sh
npm ls @microsoft/generator-sharepoint -g --depth=0
```

## <a name="see-also"></a><span data-ttu-id="b8dfd-157">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="b8dfd-157">See also</span></span>

* [<span data-ttu-id="b8dfd-158">Aktualisieren von SharePoint-Framework-Projekten (Anleitung für Team-basierte Entwicklung)</span><span class="sxs-lookup"><span data-stu-id="b8dfd-158">Upgrading SharePoint Framework projects (Team-based development guidance)</span></span>](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/team-based-development-on-sharepoint-framework#upgrading-sharepoint-framework-projects)
* [<span data-ttu-id="b8dfd-159">Aktualisieren von SharePoint-Elementen (Bereitstellen von SharePoint-Objekten)</span><span class="sxs-lookup"><span data-stu-id="b8dfd-159">Upgrade SharePoint items (Provisioning SharePoint assets)</span></span>](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/toolchain/provision-sharepoint-assets#upgrade-sharepoint-items)