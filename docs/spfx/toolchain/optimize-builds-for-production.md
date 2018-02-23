---
title: "Optimieren von SharePoint-Framework-Builds für die Produktion"
description: "Die Unterschiede zwischen Debug- und Releasebuilds und Optimierung Ihres Bundles für die Verwendung in Produktionsumgebungen."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: 95bd3bc98c5a0bf509ffd3bf790d22a9d5e9ac93
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/05/2018
---
# <a name="optimize-sharepoint-framework-builds-for-production"></a><span data-ttu-id="64a38-103">Optimieren von SharePoint-Framework-Builds für die Produktion</span><span class="sxs-lookup"><span data-stu-id="64a38-103">Optimize SharePoint Framework builds for production</span></span>

<span data-ttu-id="64a38-104">Beim Bereitstellen von SharePoint-Framework-Lösungen für die Produktion sollten Sie immer einen Releasebuild Ihres Projekts verwenden, der für Leistung optimiert ist.</span><span class="sxs-lookup"><span data-stu-id="64a38-104">When deploying SharePoint Framework solutions to production you should always use a release build of your project which is optimized for performance. This article illustrates the main differences between debug and release builds and shows how you can optimize your bundle for use in production environments.</span></span> <span data-ttu-id="64a38-105">Dieser Artikel beschreibt die wichtigsten Unterschiede zwischen Debug- und Releasebuilds und zeigt, wie Sie Ihr Bundle für die Verwendung in Produktionsumgebungen optimieren können.</span><span class="sxs-lookup"><span data-stu-id="64a38-105">When deploying SharePoint Framework solutions to production you should always use a release build of your project which is optimized for performance. This article illustrates the main differences between debug and release builds and shows how you can optimize your bundle for use in production environments.</span></span>

## <a name="use-release-builds-in-production"></a><span data-ttu-id="64a38-106">Verwenden von Releasebuilds in der Produktion</span><span class="sxs-lookup"><span data-stu-id="64a38-106">Use release builds in production</span></span>

<span data-ttu-id="64a38-p102">Beim Erstellen eines SharePoint Framework-Projekts können Sie auswählen, ob es im Debug- oder Releasemodus erstellt werden soll. Standardmäßig werden SharePoint Framework-Projekte im Debugmodus erstellt, in dem Code leichter gedebuggt werden kann. Wenn der Code jedoch abgeschlossen ist und wie erwartet funktioniert, sollten Sie ihn im Releasemodus erstellen, um ihn für die Ausführung in der Produktionsumgebung zu optimieren.</span><span class="sxs-lookup"><span data-stu-id="64a38-p102">When building a SharePoint Framework project, you can choose whether you want to build it in a debug or release mode. By default, SharePoint Framework projects are built in debug mode, which makes it easier for you to debug code. But when your code is finished and is working as expected, you should build it in release mode to optimize it for running in the production environment.</span></span>

<span data-ttu-id="64a38-110">Weitere Informationen zum Erstellen des Projekts im Releasemodus finden Sie unter [SharePoint-Framework-Toolkette](./sharepoint-framework-toolchain.md).</span><span class="sxs-lookup"><span data-stu-id="64a38-110">For more information about building your project in release mode, see the [SharePoint Framework Toolchain](./sharepoint-framework-toolchain.md) article.</span></span>

<span data-ttu-id="64a38-111">Der Hauptunterschied zwischen der Ausgabe eines Debug- und eines Releasebuilds besteht darin, dass die Releaseversion des generierten Bundles minimiert und wesentlich kleiner ist als ihre Debugentsprechung.</span><span class="sxs-lookup"><span data-stu-id="64a38-111">The main difference between the output of a debug and release build is, that the release version of the generated bundle is minified and significantly smaller in size than its debug equivalent. To illustrate the difference, compare the size of the debug and release version of a SharePoint Framework project with a web part using Angular.</span></span> <span data-ttu-id="64a38-112">Um den Unterschied zu verdeutlichen, vergleichen Sie die Größe der Debug- und der Releaseversion eines SharePoint-Framework-Projekts mit einem Webpart unter Verwendung von Angular.</span><span class="sxs-lookup"><span data-stu-id="64a38-112">The main difference between the output of a debug and release build is, that the release version of the generated bundle is minified and significantly smaller in size than its debug equivalent. To illustrate the difference, compare the size of the debug and release version of a SharePoint Framework project with a web part using Angular.</span></span>

![Bild mit zwei Explorer-Fenstern, die nebeneinander angezeigt werden, wobei die Debug- und die Releaseversion des Bundles hervorgehoben ist.](../../images/guidance-productionbuilds-debug-vs-ship-bundle.png)

<span data-ttu-id="64a38-114">Die Größe der Debugversion des Bundles beträgt 1255 KB, während die Releaseversion nur 177 KB groß ist.</span><span class="sxs-lookup"><span data-stu-id="64a38-114">The debug version of the bundle is 1255 KB while its release equivalent is only 177 KB.</span></span> <span data-ttu-id="64a38-115">Der Größenunterschied zwischen der Debug- und der Releaseversion des generierten Bundles variiert in Abhängigkeit von den in Ihrem Projekt verwendeten Bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="64a38-115">The difference in size between the debug and release version of the generated bundle differs depending on the libraries used in your project.</span></span> <span data-ttu-id="64a38-116">Der Releasebuild ist doch immer wesentlich kleiner als der Debugbuild, deshalb sollten Sie immer die Ausgabe von Releasebuilds für die Produktion bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="64a38-116">Still, the release build is always significantly smaller than a debug build, which is why you should always deploy the output of release builds to production.</span></span>

## <a name="dont-include-third-party-libraries-in-the-bundle"></a><span data-ttu-id="64a38-117">Schließen Sie keine Drittanbieterbibliotheken in das Bundle ein.</span><span class="sxs-lookup"><span data-stu-id="64a38-117">Don't include third party libraries in the bundle</span></span>

<span data-ttu-id="64a38-118">Beim Erstellen von SharePoint-Framework-Lösungen können Sie von vielen vorhandenen JavaScript-Bibliotheken zur Lösung häufig auftretender Probleme profitieren.</span><span class="sxs-lookup"><span data-stu-id="64a38-118">When building SharePoint Framework solutions, you can benefit from many existing JavaScript libraries to solve common problems.</span></span> <span data-ttu-id="64a38-119">Dank der Verwendung vorhandener Bibliotheken können Sie produktiver arbeiten und sich auf den Mehrwert für Ihre Organisation konzentrierten anstatt allgemeine Funktionen zu entwickeln.</span><span class="sxs-lookup"><span data-stu-id="64a38-119">When building SharePoint Framework solutions, you can benefit of many existing JavaScript libraries to solve common problems. Using existing libraries allows you to be more productive and lets you focus on the added value for your organization, instead of on developing generic functionality, required by your solution.</span></span>

<span data-ttu-id="64a38-120">Beim Verweisen auf Drittanbieterbibliotheken schließt SharePoint-Framework diese standardmäßig in das generierte Bundle ein.</span><span class="sxs-lookup"><span data-stu-id="64a38-120">By default, when referencing third-party libraries in your project, SharePoint Framework includes them in the generated bundle.</span></span> <span data-ttu-id="64a38-121">Benutzer, die mit Ihrer Lösung arbeiten, laden daher letztendlich dieselbe Bibliothek mehrmals herunter - einmal pro Komponente.</span><span class="sxs-lookup"><span data-stu-id="64a38-121">As a result, users working with your solution end up downloading the same library multiple times, once with each component.</span></span> <span data-ttu-id="64a38-122">Die Gesamtgröße der Seite steigt stark an, sodass der Ladevorgang länger dauert, was zu einer schlechteren Erfahrung für den Benutzer, insbesondere in langsameren Netzwerken, führt.</span><span class="sxs-lookup"><span data-stu-id="64a38-122">The total page size grows significantly, taking longer to load and leading to a poor user experience, particularly on slower networks.</span></span>

![Microsoft Edge-Entwicklertools auf der Registerkarte „Netzwerk“, es werden zwei Webpartbundles angezeigt, die gerade geladen werden](../../images/guidance-productionbuilds-two-bundles-with-libraries.png)

<span data-ttu-id="64a38-124">Beim Arbeiten mit Drittanbieterbibliotheken sollten Sie immer in Betracht ziehen, diese von einem externen Speicherort zu laden: entweder aus einem öffentlichen CDN oder von einem Hostingspeicherort im Besitz Ihrer Organisation.</span><span class="sxs-lookup"><span data-stu-id="64a38-124">When working with third-party libraries, you should always consider loading them from an external location: either a public CDN or a hosting location owned by your organization.</span></span> <span data-ttu-id="64a38-125">Sie können auf diese Weise die Bibliothek aus dem Bundle ausschließen, wodurch die Größe wesentlich reduziert wird.</span><span class="sxs-lookup"><span data-stu-id="64a38-125">This allows you to exclude the library from your bundle, significantly decreasing its size.</span></span> 

<span data-ttu-id="64a38-126">Wenn der Hostingspeicherort, von dem Sie die Bibliothek laden, für statische Ressourcen optimiert ist, müssen Benutzer, die mit Ihrer Lösung arbeiten, die Bibliothek nur einmal laden.</span><span class="sxs-lookup"><span data-stu-id="64a38-126">Additionally, if the hosting location from which you are loading the library is optimized for serving static assets, users working with your solution need to load the library only once.</span></span> <span data-ttu-id="64a38-127">Bei nachfolgenden Anforderungen oder auch, wenn die Lösung in der Zukunft verwendet wird, verwendet der Webbrowser die zuvor zwischengespeicherte Kopie der Bibliothek wieder und lädt diese nicht erneut herunter.</span><span class="sxs-lookup"><span data-stu-id="64a38-127">On subsequent requests, or even when using your solution in the future, the web browser reuses the previously cached copy of the library rather than downloading it again.</span></span> <span data-ttu-id="64a38-128">Dementsprechend wird die Seite mit der Lösung wesentlich schneller geladen.</span><span class="sxs-lookup"><span data-stu-id="64a38-128">As a result, the page with your solution loads significantly faster.</span></span>

## <a name="verify-the-contents-of-your-bundle"></a><span data-ttu-id="64a38-129">Überprüfen des Bundleinhalts</span><span class="sxs-lookup"><span data-stu-id="64a38-129">Verify the contents of your bundle</span></span>

<span data-ttu-id="64a38-130">Zum besseren Verständnis der Größe der generierten Bundles können Sie die Webpack-Konfiguration in Ihrem Projekt so erweitern, dass SharePoint-Framework Bundlestatistiken generiert.</span><span class="sxs-lookup"><span data-stu-id="64a38-130">To better understand the size of the generated bundles, you can extend the webpack configuration in your project and have the SharePoint Framework generate bundle statistics.</span></span>

<span data-ttu-id="64a38-131">Installieren Sie zunächst das Paket **webpack-bundle-analyzer** in Ihrem Projekt, indem Sie den folgenden Befehl in der Befehlszeile ausführen:</span><span class="sxs-lookup"><span data-stu-id="64a38-131">First, install the **webpack-bundle-analyzer** package in your project, by executing in the command line:</span></span>

```sh
npm install webpack-bundle-analyzer --save-dev
```

<br/>

<span data-ttu-id="64a38-132">Ändern Sie anschließend den Inhalt der Datei **gulpfile.js** in Ihrem Projekt zu:</span><span class="sxs-lookup"><span data-stu-id="64a38-132">Next, change the contents of the **gulpfile.js** file in your project to:</span></span>

```js
'use strict';

const gulp = require('gulp');
const path = require('path');
const build = require('@microsoft/sp-build-web');
const bundleAnalyzer = require('webpack-bundle-analyzer');

build.configureWebpack.mergeConfig({
  additionalConfiguration: (generatedConfiguration) => {
    const lastDirName = path.basename(__dirname);
    const dropPath = path.join(__dirname, 'temp', 'stats');
    generatedConfiguration.plugins.push(new bundleAnalyzer.BundleAnalyzerPlugin({
      openAnalyzer: false,
      analyzerMode: 'static',
      reportFilename: path.join(dropPath, `${lastDirName}.stats.html`),
      generateStatsFile: true,
      statsFilename: path.join(dropPath, `${lastDirName}.stats.json`),
      logLevel: 'error'
    }));

    return generatedConfiguration;
  }
});

build.initialize(gulp);
```

<br/>

<span data-ttu-id="64a38-133">Beim nächsten Bündeln des Projekts mithilfe der `gulp bundle`-Aufgabe werden die generierten Bundlestatistikdateien im Ordner **temp/stats** in Ihrem Projekt angezeigt.</span><span class="sxs-lookup"><span data-stu-id="64a38-133">Next time you bundle your project using the `gulp bundle` task, you will see the bundle stats files generated in the **temp/stats** folder in your project.</span></span> <span data-ttu-id="64a38-134">Bei einer der generierten Statistikdateien handelt es sich um ein Treemap-Diagramm mit den anderen Skripts, die im generierten Bundle enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="64a38-134">One of the generated stats file, is a treemap showing the different scripts included in the generated bundle.</span></span> <span data-ttu-id="64a38-135">Sie finden diese Darstellung in der Datei **./temp/stats/[solution-name].stats.html**.</span><span class="sxs-lookup"><span data-stu-id="64a38-135">You can find this visualization in the **./temp/stats/[solution-name].stats.html** file.</span></span>

<br/>

<img alt="Webpack bundle analyzer treemap illustrating the contents of a sample SharePoint Framework bundle" src="../../images/guidance-productionbuilds-webpack-bundlestats-chart-angular.png" width="800">

<span data-ttu-id="64a38-136">Mit dem Treemap-Diagramm „Webpack Bundle Analyzer“ können Sie ganz einfach überprüfen, ob das generierte Bundle unnötige Skripts enthält und verstehen, wie sich die enthaltenen Skripts auf die Gesamtgröße des Bundles auswirken.</span><span class="sxs-lookup"><span data-stu-id="64a38-136">Using the Webpack bundle analyzer treemap is a convenient way for you to verify, that the generated bundle doesn't contain any unnecessary scripts and how the included scripts affect the total bundle size.</span></span> <span data-ttu-id="64a38-137">Bedenken Sie, dass die angezeigte Größe den Debugbuild widerspiegelt und bei einem Releasebuild wesentlich kleiner ist.</span><span class="sxs-lookup"><span data-stu-id="64a38-137">Keep in mind, that the displayed size reflects the debug build and would be significantly smaller for a release build.</span></span>

<span data-ttu-id="64a38-138">Ausführlichere Informationen, die zum Generieren des Diagramms verwendet werden, sind in der Datei **./dist/[solution-name].stats.json** enthalten.</span><span class="sxs-lookup"><span data-stu-id="64a38-138">More detailed information, used to generate the visualization, is included in the **./dist/[solution-name].stats.json** file.</span></span> <span data-ttu-id="64a38-139">Mithilfe dieser Datei können Sie herausfinden, warum ein bestimmtes Skript in das Bundle einschlossen wurde oder ob ein bestimmtes Skript in mehreren Bundles verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="64a38-139">Using this file you can find out why a specific script has been included in the bundle or if a particular script is used in multiple bundles.</span></span> <span data-ttu-id="64a38-140">Mithilfe dieser Informationen können Sie Ihre Pakete optimieren, um die Ladezeit für Ihre Lösung zu verbessern.</span><span class="sxs-lookup"><span data-stu-id="64a38-140">With this information you can optimize your bundles improving the loading time of your solution.</span></span>

## <a name="choose-your-primary-client-side-library"></a><span data-ttu-id="64a38-141">Auswählen der primären clientseitigen Bibliothek</span><span class="sxs-lookup"><span data-stu-id="64a38-141">Choose your primary client-side library</span></span>

<span data-ttu-id="64a38-142">Wenn es mehrere Komponenten auf derselben Seite oder auch auf unterschiedlichen Seiten über das Portal hinweg gibt und alle dieselbe Bibliothek verwenden, die von der gleichen URL geladen wurde, verwendet der Webbrowser die zuvor zwischengespeicherte Kopie wieder, was dazu führt, dass das Portal schneller geladen wird.</span><span class="sxs-lookup"><span data-stu-id="64a38-142">If there are multiple components on the same page, or even on different pages across the portal, and they all use the same library loaded from the same URL, the web browser also reuses the copy it cached previously, which leads to the portal loading faster.</span></span> 

<span data-ttu-id="64a38-143">Das ist genau der Grund, warum es für Organisationen so wichtig ist zu erkennen, welche Bibliotheken und welche Version sie verwenden und woher diese geladen werden, und zwar nicht nur für ein bestimmtes Projekt, sondern für die gesamte Organisation.</span><span class="sxs-lookup"><span data-stu-id="64a38-143">This is exactly why it is essential for organizations to rationalize which libraries and versions they use and where they load from, not only for a specific project but for the whole organization.</span></span> <span data-ttu-id="64a38-144">Mit einer derartigen Richtlinie können Benutzer, die mit den unterschiedlichen Anwendungen arbeiten, produktiver arbeiten, da die Anwendungen schneller geladen werden.</span><span class="sxs-lookup"><span data-stu-id="64a38-144">Such a policy allows users working with the different applications to be more productive by loading the applications faster.</span></span> <span data-ttu-id="64a38-145">Indem die zuvor heruntergeladenen Ressourcen wiederverwendet werden, wird auch die Last im Netzwerk eingeschränkt, sodass Bandbreite für andere Zwecke freigegeben wird.</span><span class="sxs-lookup"><span data-stu-id="64a38-145">By reusing the previously downloaded assets, the load on the network is limited, freeing its bandwidth for other purposes.</span></span>

<span data-ttu-id="64a38-146">Weitere Informationen zum Arbeiten mit externen Bibliotheken finden Sie unter [Verwenden vorhandener JavaScript-Bibliotheken in clientseitigen SharePoint-Framework-Webparts](../web-parts/guidance/use-existing-javascript-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="64a38-146">For more information about working with external libraries see the [Use existing JavaScript libraries in SharePoint Framework client-side web parts](../web-parts/guidance/use-existing-javascript-libraries.md) article.</span></span>

## <a name="reference-only-the-necessary-components"></a><span data-ttu-id="64a38-147">Nur auf die notwendigen Komponenten verweisen</span><span class="sxs-lookup"><span data-stu-id="64a38-147">Reference only the necessary components</span></span>

<span data-ttu-id="64a38-148">Wenn Sie mit externen Bibliotheken arbeiten, benötigen Sie manchmal vielleicht nicht die gesamte Bibliothek, sondern nur einen kleinen Teil davon.</span><span class="sxs-lookup"><span data-stu-id="64a38-148">Sometimes when working with external libraries, you might actually not need the whole library but only a small portion of it.</span></span> <span data-ttu-id="64a38-149">Das Einschließen der gesamten Bibliothek erhöht die Größe des Bundles unnötig, sodass sich auch die Ladezeit verlängert.</span><span class="sxs-lookup"><span data-stu-id="64a38-149">Including the whole library unnecessarily adds to the size of your bundle, increasing its load time.</span></span> <span data-ttu-id="64a38-150">Stattdessen sollten Sie immer in Betracht ziehen, nur die Teile der jeweiligen Bibliothek zu laden, die Sie tatsächlich benötigen.</span><span class="sxs-lookup"><span data-stu-id="64a38-150">Instead, you should always consider loading only the specific parts of the particular library that you actually need.</span></span>

<span data-ttu-id="64a38-151">Um dies zu verdeutlichen, nehmen wir die Bibliothek [Lodash](https://lodash.com) als Beispiel.</span><span class="sxs-lookup"><span data-stu-id="64a38-151">To illustrate this, take the [Lodash](https://lodash.com) library as an example.</span></span> <span data-ttu-id="64a38-152">Lodash ist eine Sammlung von Dienstprogrammen, die Ihnen beim Ausführen bestimmter Vorgänge in Ihrem Code behilflich sind.</span><span class="sxs-lookup"><span data-stu-id="64a38-152">Lodash is a collection of utilities helping you to perform certain operations in your code.</span></span> <span data-ttu-id="64a38-153">Die Wahrscheinlichkeit ist hoch, dass Sie beim Arbeiten mit Lodash nur ein paar spezifische Methoden und nicht die vollständige Bibliothek benötigen.</span><span class="sxs-lookup"><span data-stu-id="64a38-153">The odds are high, that when working with Lodash, you will only need a few specific methods rather than the complete library.</span></span> 

<span data-ttu-id="64a38-154">Wenn Sie jedoch auf die gesamte Bibliothek mit dem folgenden Code verwiesen haben, werden 527 KB zu Ihrem nicht optimierten Bundle hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="64a38-154">However, if you referenced the whole library by using the following code, it adds 527 KB to your unoptimized bundle:</span></span>

```typescript
import * as _ from 'lodash';
```

<br/>

<img alt="The complete Lodash library included in a bundle, highlighted in the Webpack bundle analyzer treemap" src="../../images/guidance-productionbuilds-import-lodash.png" width="800">

<br/>

<span data-ttu-id="64a38-155">Wenn Sie stattdessen nur auf die bestimmte Lodash-Methode mit dem folgenden Code verwiesen haben, werden 45 KB zu Ihrem nicht optimierten Bundle hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="64a38-155">Instead, if you referenced only the specific Lodash method by using the following code, it adds 45 KB to your unoptimized bundle:</span></span>

```typescript
const at: any = require('lodash/at');
```

<br/>

![Bestimmte Lodash-Methode in einem Bundle enthalten, markiert im Treemap-Diagramm „Webpack Bundle Analyzer“](../../images/guidance-productionbuilds-import-lodash-at.png)

<span data-ttu-id="64a38-157">Das Verweisen auf spezifische Methoden im Gegensatz zur gesamten Bibliothek hat, insbesondere im Hinblick auf Lodash, aber auch bei anderen Bibliotheken, seinen Preis.</span><span class="sxs-lookup"><span data-stu-id="64a38-157">Specifically with regards to Lodash, but which could also be the case with other libraries, referencing specific methods instead of the whole library comes with a price.</span></span> 

<span data-ttu-id="64a38-158">In Lodash wird das Laden spezifischer Methoden innerhalb von SharePoint-Framework-Projekten mithilfe der **import**-Notation derzeit nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="64a38-158">Currently, Lodash doesn't support loading specific methods inside of SharePoint Framework projects using the **import** notation.</span></span> <span data-ttu-id="64a38-159">Stattdessen müssen Sie eine **require**-Anweisung verwenden, die nicht die typesafety-Funktionen wie die Verwendung der **import**-Anweisung bietet.</span><span class="sxs-lookup"><span data-stu-id="64a38-159">Instead, you have to use a **require** statement which doesn't offer you the typesafety capabilities that using the **import** statement does.</span></span> <span data-ttu-id="64a38-160">Letztendlich müssen Sie entscheiden, ob das Laden von wesentlich mehr Code in Ihren Bundles das Aufrechterhalten der typesafety-Funktionen wert ist.</span><span class="sxs-lookup"><span data-stu-id="64a38-160">Eventually it is up to you to decide if loading significantly more code into your bundles is worth preserving the typesafety capabilities.</span></span>

> [!NOTE] 
> <span data-ttu-id="64a38-161">Einige der Lodash-Methoden werden im SharePoint-Framework in der Bibliothek **@microsoft/sp-lodash-subset** bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="64a38-161">Some of the Lodash methods are provided with the SharePoint Framework in the **@microsoft/sp-lodash-subset** library.</span></span> <span data-ttu-id="64a38-162">Überprüfen Sie vor der Verwendung von Lodash, ob die Methode, die Sie verwenden möchten, nicht bereits in der **@microsoft/sp-lodash-subset**-Bibliothek verfügbar ist, die bereits als Teil des SharePoint-Framework verfügbar ist und nicht in Ihr Bundle eingeschlossen werden muss.</span><span class="sxs-lookup"><span data-stu-id="64a38-162">Before using Lodash, verify if the method that you want to use isn't already available in the **@microsoft/sp-lodash-subset** library, which is already available as a part of the SharePoint Framework and does not need to be included in your bundle.</span></span>

## <a name="see-also"></a><span data-ttu-id="64a38-163">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="64a38-163">See also</span></span>

- [<span data-ttu-id="64a38-164">SharePoint-Framework-Übersicht</span><span class="sxs-lookup"><span data-stu-id="64a38-164">SharePoint Framework Extensions Overview</span></span>](../sharepoint-framework-overview.md)