---
title: Aktualisieren von SharePoint-Framework-Paketen
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: b8d542ac73d1739faff65f4636cffdef062a3c00
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="update-sharepoint-framework-packages"></a><span data-ttu-id="2f1fc-102">Aktualisieren von SharePoint-Framework-Paketen</span><span class="sxs-lookup"><span data-stu-id="2f1fc-102">Update SharePoint Framework packages</span></span> 

<span data-ttu-id="2f1fc-103">Die SharePoint-Tools für die clientseitige Entwicklung verwenden den [npm](https://www.npmjs.com/)-Paket-Manager, um Abhängigkeiten und andere erforderliche JavaScript-Hilfsprogramme zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-103">SharePoint client-side development tools use the [npm](https://www.npmjs.com/) package manager to manage dependencies and other required JavaScript helpers. npm is typically included as part of Node.js setup.</span></span> <span data-ttu-id="2f1fc-104">npm ist in der Regel als Teil des Node.js-Setups enthalten.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-104">npm is typically included as part of Node.js setup.</span></span>

<span data-ttu-id="2f1fc-105">Beim Erstellen einer neuen clientseitigen Lösung ruft der Yeoman-Generator für SharePoint die neuesten SharePoint-Framework-Pakete ab, die für Ihr clientseitiges Projekt erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-105">When you create a new client-side solution, the yeoman generator for SharePoint fetches the latest SharePoint Framework packages required for your client-side project.</span></span> <span data-ttu-id="2f1fc-106">Ihre vorhandenen Pakete sind ggf. veraltet und möglicherweise stehen zum Erstellen Ihres Projekts neue Versionen der Pakete zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-106">As you build your project, your existing packages could be outdated as there could be new versions of one or more packages available.</span></span> <span data-ttu-id="2f1fc-107">Entsprechend den [Versionshinweisen](https://aka.ms/spfx-release-notes) für eine bestimmte Version oder das neueste Paket können Sie die in Ihrem Projekt verwendeten SharePoint-Framework-Pakete aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-107">Based on the [release notes](https://aka.ms/spfx-release-notes) for a particular release or the latest package, you may decide to update your SharePoint Framework packages used in your project.</span></span> <span data-ttu-id="2f1fc-108">SharePoint Framework-Pakete enthalten die npm-Pakete, die Sie in Ihrem Projekt installiert haben (Beispiel: [@microsoft/sp-core-library](https://www.npmjs.com/package/@microsoft/sp-core-library)), sowie die global installierten npm-Pakete (Beispiel: [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint)).</span><span class="sxs-lookup"><span data-stu-id="2f1fc-108">SharePoint Framework packages include both the npm packages you have installed in your project, for example: [@microsoft/sp-core-library](https://www.npmjs.com/package/@microsoft/sp-core-library), and npm packages installed globally, for example: [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint).</span></span> 

<span data-ttu-id="2f1fc-109">Obwohl nicht erforderlich, empfiehlt es sich, die SharePoint Framework-Pakete regelmäßig zu aktualisieren, um alle neuesten Änderungen und Updates zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-109">While it may not be required, it is recommended you update the SharePoint Framework packages every so often so that you can get the latest changes and fixes that have been released.</span></span> 

## <a name="find-outdated-packages-in-your-project"></a><span data-ttu-id="2f1fc-110">Suche nach veralteten Paketen im Projekt</span><span class="sxs-lookup"><span data-stu-id="2f1fc-110">Find outdated packages in your project</span></span>
<span data-ttu-id="2f1fc-111">Führen Sie in einer Konsole im selben Verzeichnis wie das Projekt den folgenden Befehl aus, um nach veralteten Paketen in Ihrem clientseitigen Projekt zu suchen, einschließlich SharePoint Framework-Paketen und anderen, von denen Ihr Projekt abhängt.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-111">To find the outdated packages in your client-side project, including SharePoint Framework and other packages your project depends on, run the following command in a console in the same directory as your project.</span></span> 

```
npm outdated
```

<span data-ttu-id="2f1fc-112">Der Befehl listet die folgenden Informationen zu den Paketen auf, von denen Ihr Projekt abhängt.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-112">The command will list the following information about the packages your project depends on. This information is looked up from the  file located in the root of your project directory and npm registry.</span></span> <span data-ttu-id="2f1fc-113">Diese Informationen werden der Datei `package.json` im Stammverzeichnis des Projekts und der npm-Registry entnommen.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-113">The command will list the following information about the packages your project depends on. This information is looked up from the `package.json` file located in the root of your project directory and npm registry.</span></span>

* <span data-ttu-id="2f1fc-114">Aktuelle, in Ihrem Projekt installierte Version</span><span class="sxs-lookup"><span data-stu-id="2f1fc-114">Current version installed in your project</span></span>
* <span data-ttu-id="2f1fc-115">Von Ihrem Projekt angeforderte Version (verfügbar in `package.json`)</span><span class="sxs-lookup"><span data-stu-id="2f1fc-115">Version requested by your project (available in `package.json`)</span></span>
* <span data-ttu-id="2f1fc-116">Neueste verfügbare Version</span><span class="sxs-lookup"><span data-stu-id="2f1fc-116">Latest version available</span></span>

![Veraltete NPM-Pakete](../../images/npm-outdated-packages-list.png)

<span data-ttu-id="2f1fc-118">Um die SharePoint Framework Pakete zu identifizieren, suchen Sie nach den Paketnamen, die mit dem folgenden npm-Bereich und -Präfix beginnen:</span><span class="sxs-lookup"><span data-stu-id="2f1fc-118">To identify the SharePoint Framework packages, look for the package names that start with the following npm scope and prefix:</span></span>

```
@microsoft/sp-
```
<span data-ttu-id="2f1fc-119">Zusammen mit den Framework-Paketen müssen Sie ggf. auch die Pakete `react` und `office-ui-fabric-react` aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-119">Along with the framework packages, you may also need to update `react` and `office-ui-fabric-react` packages.</span></span> <span data-ttu-id="2f1fc-120">Lesen Sie unbedingt die [Versionshinweise](https://aka.ms/spfx-release-notes) für die jeweilige Version, um zu erfahren, welche Pakete eine Aktualisierung erfordern, und entsprechend planen zu können.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-120">Along with the framework packages, you may also need to update  and  packages. Make sure you read the [release notes](https://aka.ms/spfx-release-notes) for that specific release to infer which packages require updates and plan accordingly.</span></span>

### <a name="update-packages"></a><span data-ttu-id="2f1fc-121">Aktualisieren der Pakete</span><span class="sxs-lookup"><span data-stu-id="2f1fc-121">Update packages</span></span>
<span data-ttu-id="2f1fc-122">Um ein oder mehrere Pakete auf die neueste Version zu aktualisieren, müssen Sie die Paketinformationen in der Datei `package.json` bearbeiten und dann die neuesten Pakete abrufen.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-122">To update one or more packages to the latest version, you will need to edit the package(s) information in the `package.json` file and then fetch the latest packages.</span></span>

#### <a name="update-package-versions"></a><span data-ttu-id="2f1fc-123">Aktualisieren der Paketversionen</span><span class="sxs-lookup"><span data-stu-id="2f1fc-123">Update package versions</span></span>
<span data-ttu-id="2f1fc-124">Öffnen Sie das Projekt in Ihrem bevorzugten Codeeditor, und suchen Sie im Stammverzeichnis des Projekts nach der Datei `package.json`.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-124">Open your project in your favorite code editor and locate the `package.json` file in the root of your project directory.</span></span>

<span data-ttu-id="2f1fc-125">Suchen Sie in der Datei `package.json` im Abschnitt `dependencies` und `devDependencies` nach den Paketen und aktualisieren Sie diese auf die neueste, im Befehl `npm outdated` aufgeführte Version.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-125">In the `package.json` file, locate the package(s) under the `dependencies` and `devDependencies` section and update the version to the latest version available that was listed in the `npm outdated` command. For example, the image below highlights the version updates to SharePoint Framework packages, the left section referring to the old and the right section referring to the latest package versions.</span></span> <span data-ttu-id="2f1fc-126">Beispiel: Im nachfolgenden Bild sind die Versionsaktualisierungen der SharePoint Framework-Pakete hervorgehoben. Links befinden sich die alten und rechts die neuen Versionen.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-126">In the  file, locate the package(s) under the  and  section and update the version to the latest version available that was listed in the  command. For example, the image below highlights the version updates to SharePoint Framework packages, the left section referring to the old and the right section referring to the latest package versions.</span></span>

![Bearbeiten der Paketversionen in der Datei „package.json“](../../images/npm-update-packagejson-versions.png)

<span data-ttu-id="2f1fc-128">Nachdem Sie die Paketversionen aktualisiert haben, speichern Sie die Datei `package.json`.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-128">Once you have updated the package versions, Save the `package.json` file.</span></span>

#### <a name="update-packages"></a><span data-ttu-id="2f1fc-129">Aktualisieren der Pakete</span><span class="sxs-lookup"><span data-stu-id="2f1fc-129">Update packages</span></span>
<span data-ttu-id="2f1fc-p106">Öffnen Sie Ihre bevorzugte Konsole und navigieren Sie zum Stammverzeichnis des Projekts. Führen Sie zum Aktualisieren der Pakete die nachstehenden Anweisungen aus:</span><span class="sxs-lookup"><span data-stu-id="2f1fc-p106">Open your favorite console and navigate to the root of your project directory. Follow the instructions below to successfully update the packages to its latest version.</span></span>

<span data-ttu-id="2f1fc-132">Löschen Sie den Ordner `node_modules`.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-132">Delete the content of the folder `node_modules`.</span></span> <span data-ttu-id="2f1fc-133">Dies ist der Ordner, in dem npm die Pakete für Ihr Projekt lokal installiert.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-133">Delete the  folder. This is the folder where npm installs the packages locally for your project. Deleting this folder forces npm to fetch the latest and not duplicate existing packages.</span></span> <span data-ttu-id="2f1fc-134">Durch Löschen dieses Ordners wird npm gezwungen, die neuesten Pakete abzurufen, anstatt die vorhandenen zu duplizieren.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-134">Delete the  folder. This is the folder where npm installs the packages locally for your project. Deleting this folder forces npm to fetch the latest and not duplicate existing packages.</span></span>

<span data-ttu-id="2f1fc-135">Wenn Sie eine Mac- oder Linux-Umgebung verwenden, führen Sie den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="2f1fc-135">If you are using a Mac or a Linux environment, then run the following command:</span></span>

```
rm -rf node_modules/
```

<span data-ttu-id="2f1fc-136">Wenn Sie eine Windows-Umgebung verwenden, führen Sie den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="2f1fc-136">If you are using a Windows environment, then run the following command:</span></span>

```
 rd /s /q node_modules/
```

<span data-ttu-id="2f1fc-137">Führen Sie nun zum Abrufen der neuesten Pakete aus der npm-Registry den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="2f1fc-137">Now, execute the following command to fetch the latest packages from the npm registry:</span></span>

```
npm install
```

<span data-ttu-id="2f1fc-138">Mit diesem Befehl wird der Ordner `node_modules` erstellt und es werden auf Grundlage der Informationen aus der Datei `package.json` alle Pakete und Abhängigkeiten installiert, die für Ihr Projekt erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-138">This command will create the `node_modules` folder and install all the packages your project depends on and its dependencies based on the information available in the `package.json` file. As we updated the file with the latest versions, npm will now have the latest packages and their dependencies installed.</span></span> <span data-ttu-id="2f1fc-139">Nach dem Aktualisieren der Datei mit den neuesten Versionen sind nun die neuesten Pakete und Abhängigkeiten installiert.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-139">This command will create the  folder and install all the packages your project depends on and its dependencies based on the information available in the  file. As we updated the file with the latest versions, npm will now have the latest packages and their dependencies installed.</span></span> 

<span data-ttu-id="2f1fc-140">Führen Sie danach den folgenden Befehl aus, um alte Buildartefakte zu entfernen:</span><span class="sxs-lookup"><span data-stu-id="2f1fc-140">Once the packages are installed, execute the following command to clean up any old build artifacts:</span></span>

```
gulp clean
```

### <a name="update-your-code"></a><span data-ttu-id="2f1fc-141">Aktualisieren des Codes</span><span class="sxs-lookup"><span data-stu-id="2f1fc-141">Update your code</span></span>
<span data-ttu-id="2f1fc-142">Bei wichtigen API-Änderungen müssen Sie ggf. den vorhandenen Projektcode und die Konfigurationsdateien aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-142">Depending on breaking API changes, you may have to update your existing project code and config files.</span></span> <span data-ttu-id="2f1fc-143">In jeder Version werden wichtige Änderungen sowie die an Ihrem Code erforderlichen Änderungen in den [Versionshinweisen](https://aka.ms/spfx-release-notes) hervorgehoben.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-143">For each release, the [release notes](https://aka.ms/spfx-release-notes) will highlight any such breaking changes and the modifications required to your existing code.</span></span> <span data-ttu-id="2f1fc-144">Sie müssen den Code mit diesen Fehlerbehebungen aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-144">You will need to make sure you update your code with those fixes.</span></span>

<span data-ttu-id="2f1fc-145">Sie können das Projekt jederzeit erstellen, um zu erfahren, ob Fehler und Warnungen vorliegen. Führen Sie dazu den Befehl in einer Konsole im Projektverzeichnis aus:</span><span class="sxs-lookup"><span data-stu-id="2f1fc-145">You can always build the project to see if you have any errors and warnings by running the command in a console in your project directory:</span></span>

```
gulp build
```

## <a name="update-yeoman-generator-for-sharepoint"></a><span data-ttu-id="2f1fc-146">Aktualisieren des Yeoman-Generators für SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f1fc-146">Update yeoman generator for SharePoint</span></span>
<span data-ttu-id="2f1fc-147">Im Gegensatz zu den npm-Paketen, die für ein bestimmtes clientseitiges Projekt installiert werden, wird der Yeoman-Generator für SharePoint global auf Ihrem Computer installiert.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-147">Unlike the npm packages that are installed to a specific client-side project, the yeoman generator for SharePoint is installed globally in your machine.</span></span>

<span data-ttu-id="2f1fc-148">Um herauszufinden, ob der Yeoman-Generator für SharePoint aktuell ist, führen Sie den folgenden Befehl in einem Konsolenfenster aus.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-148">To find if the yeoman generator for SharePoint is out of date, run the following command in a console window.</span></span> 

```
npm outdated -g
```

<span data-ttu-id="2f1fc-p110">Der Befehl listet die folgenden Informationen zu den Paketen auf, die global auf Ihrem Computer installiert sind. Diese Informationen stammen aus den auf Ihrem Computer und in der npm-Registry installierten Versionen.</span><span class="sxs-lookup"><span data-stu-id="2f1fc-p110">The command will list the following information about the packages installed globally in your machine. This information is looked up from the versions installed in your machine and the npm registry.</span></span>

* <span data-ttu-id="2f1fc-151">Aktuelle, global auf Ihrem Computer installierte Version</span><span class="sxs-lookup"><span data-stu-id="2f1fc-151">Current version installed globally in your machine</span></span>
* <span data-ttu-id="2f1fc-152">Von Ihnen bei der Installation angeforderte Version</span><span class="sxs-lookup"><span data-stu-id="2f1fc-152">Version requested by you when you installed</span></span>
* <span data-ttu-id="2f1fc-153">Neueste verfügbare Version</span><span class="sxs-lookup"><span data-stu-id="2f1fc-153">Latest version available</span></span>

![Veraltete globale npm-Pakete](../../images/npm-outdated-global-packages-list.png)

<span data-ttu-id="2f1fc-155">Um das Generator-Paket zu ermitteln, suchen Sie nach folgendem Paketnamen:</span><span class="sxs-lookup"><span data-stu-id="2f1fc-155">To identify the generator package, look for the following package name:</span></span>

```
@microsoft/generator-sharepoint
```

### <a name="update-generator-package"></a><span data-ttu-id="2f1fc-156">Aktualisieren des Generator-Pakets</span><span class="sxs-lookup"><span data-stu-id="2f1fc-156">Update generator package</span></span>
<span data-ttu-id="2f1fc-157">Öffnen Sie Ihre bevorzugte Konsole und führen Sie den folgenden Befehl aus, um den Generator auf die neueste veröffentlichte Version zu aktualisieren:</span><span class="sxs-lookup"><span data-stu-id="2f1fc-157">Open your favorite console and execute the following command to update the generator to its latest published version:</span></span>

```
npm install @microsoft/generator-sharepoint@latest -g
```

<span data-ttu-id="2f1fc-p111">Mit dem Befehl wird der Yeoman-Generator für SharePoint zusammen mit allen Abhängigkeiten auf die neueste veröffentlichte Version aktualisiert. Sie können dies überprüfen, indem Sie den folgenden Befehl in der Verwaltungskonsole ausführen:</span><span class="sxs-lookup"><span data-stu-id="2f1fc-p111">The command will update the yeoman generator for SharePoint to the latest published version along with its depedencies. You can validate this by executing the following command in the console:</span></span>

```
npm ls @microsoft/generator-sharepoint -g --depth=0
```






 
