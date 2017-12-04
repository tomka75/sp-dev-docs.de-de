---
title: "Entwicklungstools und -bibliotheken für das SharePoint Framework"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 2df6ebaaf1d56b20e2ae96063c9d6bff339603c5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-framework-development-tools-and-libraries"></a><span data-ttu-id="f88d7-102">Entwicklungstools und -bibliotheken für das SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="f88d7-102">SharePoint Framework development tools and libraries</span></span>

<span data-ttu-id="f88d7-p101">Das SharePoint Framework umfasst mehrere clientseitige JavaScript-Bibliotheken, die Sie zum Erstellen von Lösungen verwenden können. Dieser Artikel enthält eine Übersicht über die Tools und Bibliotheken, die Sie zum Entwickeln von clientseitigen Webparts verwenden können.</span><span class="sxs-lookup"><span data-stu-id="f88d7-p101">The SharePoint Framework includes several client-side JavaScript libraries that you can use to build your solutions. This article provides an overview of the tools and libraries that you can use to develop client-side web parts.</span></span>

## <a name="typescript"></a><span data-ttu-id="f88d7-105">TypeScript</span><span class="sxs-lookup"><span data-stu-id="f88d7-105">TypeScript</span></span>
<span data-ttu-id="f88d7-p102">Bei TypeScript handelt es sich um eine typisierte Obersprache zu JavaScript, die in einfaches JavaScript kompiliert. SharePoint-Tools für die clientseitige Entwicklung werden auf Basis von TypeScript-Klassen, -Modulen und -Schnittstellen erstellt. Sie können diese verwenden, um stabile clientseitige Webparts zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="f88d7-p102">TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. SharePoint client-side development tools are built using TypeScript classes, modules, and interfaces. You can use these to build robust client-side web parts.</span></span> 

<span data-ttu-id="f88d7-109">Für die ersten Schritte mit TypeScript finden Sie in den folgenden Ressourcen Informationen:</span><span class="sxs-lookup"><span data-stu-id="f88d7-109">To get started with TypeScript, see the following resources:</span></span>

* [<span data-ttu-id="f88d7-110">TypeScript-Schnellstart</span><span class="sxs-lookup"><span data-stu-id="f88d7-110">TypeScript Quick Start</span></span>](https://www.typescriptlang.org/docs/tutorial.html)
* [<span data-ttu-id="f88d7-111">TypeScript-Umgebung</span><span class="sxs-lookup"><span data-stu-id="f88d7-111">TypeScript Playground</span></span>](https://www.typescriptlang.org/play/index.html)
* [<span data-ttu-id="f88d7-112">TypeScript-Handbuch</span><span class="sxs-lookup"><span data-stu-id="f88d7-112">TypeScript Handbook</span></span>](https://www.typescriptlang.org/docs/handbook/basic-types.html)
* [<span data-ttu-id="f88d7-113">TypeScript-Community bei Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="f88d7-113">TypeScript community on Stack Overflow</span></span>](https://stackoverflow.com/questions/tagged/typescript)

## <a name="javascript-frameworks"></a><span data-ttu-id="f88d7-114">JavaScript-Frameworks</span><span class="sxs-lookup"><span data-stu-id="f88d7-114">JavaScript frameworks</span></span>
<span data-ttu-id="f88d7-p103">Sie können eine beliebige Anzahl von JavaScript-Frameworks zum Entwickeln clientseitiger Webparts erstellen. Nachfolgend sehen Sie einige der gängigsten Frameworks:</span><span class="sxs-lookup"><span data-stu-id="f88d7-p103">You can choose any one of a number of JavaScript frameworks to develop client-side web parts. The following are some of the most popular:</span></span>

* [<span data-ttu-id="f88d7-117">React</span><span class="sxs-lookup"><span data-stu-id="f88d7-117">React</span></span>](https://facebook.github.io/react/)
* [<span data-ttu-id="f88d7-118">AngularJS 1.x</span><span class="sxs-lookup"><span data-stu-id="f88d7-118">AngularJS 1.x</span></span>](https://docs.angularjs.org/tutorial)
* [<span data-ttu-id="f88d7-119">Angular 2 for TypeScript 2.x</span><span class="sxs-lookup"><span data-stu-id="f88d7-119">Angular 2 for TypeScript 2.x</span></span>](https://angular.io/docs/ts/latest/quickstart.html)
* [<span data-ttu-id="f88d7-120">Handlebars</span><span class="sxs-lookup"><span data-stu-id="f88d7-120">Handlebars</span></span>](http://handlebarsjs.com/)

<span data-ttu-id="f88d7-p104">Da es sich bei clientseitigen Webparts um Komponenten handelt, die auf einer SharePoint-Seite abgelegt werden, wird empfohlen, dass Sie ein JavaScript-Framework auswählen, das ein ähnliches Komponentenmodell unterstützt. Einfache Frameworks, wie z. B. React, Handlebars und Angular 2, unterstützen alle ein Komponentenmodell und sind gut geeignet zum Erstellen clientseitiger Webparts.</span><span class="sxs-lookup"><span data-stu-id="f88d7-p104">Because client-side web parts are components that are dropped into a SharePoint page, we recommend that you choose a JavaScript framework that supports a similar component model. Lightweight frameworks such as React, Handlebars, and Angular 2 all support a component model and are well suited to building client-side web parts.</span></span> 

<span data-ttu-id="f88d7-123">Darüber hinaus wird empfohlen, dass Sie sich die [SharePoint PnP JavaScript-Core-Bibliothek](https://github.com/SharePoint/PnP-JS-Core) ansehen, bei der es sich um eine von der Community geförderte Initiative handelt, um einfachen Zugriff auf SharePoint-REST-APIs bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="f88d7-123">We also recommend you to have a look on [SharePoint PnP JavaScript Core library](https://github.com/SharePoint/PnP-JS-Core), which is a community driven effort targeted for providing easy access on SharePoint REST APIs.</span></span> 

## <a name="node-package-manager-npm"></a><span data-ttu-id="f88d7-124">Knotenpaket-Manager (npm)</span><span class="sxs-lookup"><span data-stu-id="f88d7-124">Node Package Manager (npm)</span></span>

<span data-ttu-id="f88d7-p105">Die SharePoint-Tools für die clientseitige Entwicklung verwenden den [npm](https://www.npmjs.com/)-Paket-Manager, der [NuGet](https://www.nuget.org/) ähnlich ist, um Abhängigkeiten und andere erforderliche JavaScript-Hilfsprogramme zu verwalten. npm ist in der Regel als Teil des Node.js-Setups enthalten.</span><span class="sxs-lookup"><span data-stu-id="f88d7-p105">SharePoint client-side development tools use the [npm](https://www.npmjs.com/) package manager, which is similar to [NuGet](https://www.nuget.org/), to manage dependencies and other required JavaScript helpers. npm is typically included as part of Node.js setup.</span></span>

<span data-ttu-id="f88d7-127">Weitere Informationen über npm finden Sie in der [npm-Dokumentation](https://docs.npmjs.com/).</span><span class="sxs-lookup"><span data-stu-id="f88d7-127">For more information about npm, see the [npm documentation](https://docs.npmjs.com/).</span></span>

## <a name="nodejs"></a><span data-ttu-id="f88d7-128">Node.js</span><span class="sxs-lookup"><span data-stu-id="f88d7-128">Node.js</span></span>

<span data-ttu-id="f88d7-p106">Node.js ist eine plattformübergeifende Open Source-Laufzeitumgebung zum Hosten und Ausführen von JavaScript-Code. Sie können node.js verwenden, um serverseitige Webanwendungen zu entwickeln, die in JavaScript geschrieben werden. Die node.js-Ökosystem ist eng mit npm und Taskausführungen wie gulp verbunden, um eine effiziente Umgebung zum Erstellen von JavaScript-basierten Anwendungen bereitzustellen. Nodel.js ist IIS Express oder IIS ähnlich, umfasst aber Tools, die die clientseitige Entwicklung vereinfachen.</span><span class="sxs-lookup"><span data-stu-id="f88d7-p106">Node.js is an open source, cross-platform runtime environment for hosting and serving JavaScript code. You can use node.js develop server-side web applications written in JavaScript. The Node.js ecosystem is tightly coupled with npm and task runners such as gulp to provide an efficient environment for building JavaScript-based applications. Node.js is similar to IIS Express or IIS, but includes tools to simplify client-side development.</span></span> 

<span data-ttu-id="f88d7-133">Weitere Informationen zu Node.js finden Sie in den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="f88d7-133">For more information about Node.js, see the following:</span></span>

* [<span data-ttu-id="f88d7-134">Informationen zu Node.js</span><span class="sxs-lookup"><span data-stu-id="f88d7-134">About Node.js</span></span>](https://nodejs.org/en/about/)
* [<span data-ttu-id="f88d7-135">API-Referenzdokumentation zu Node.js</span><span class="sxs-lookup"><span data-stu-id="f88d7-135">Node.js API reference documentation</span></span>](https://nodejs.org/api/)
* [<span data-ttu-id="f88d7-136">Node.js-Syntax und -Beispiel</span><span class="sxs-lookup"><span data-stu-id="f88d7-136">Node.js Usage and Example</span></span>](https://nodejs.org/api/synopsis.html)

## <a name="gulp-task-runner"></a><span data-ttu-id="f88d7-137">Gulp-Taskausführung</span><span class="sxs-lookup"><span data-stu-id="f88d7-137">Gulp task runner</span></span>
<span data-ttu-id="f88d7-138">Die SharePoint-Tools für clientseitige Entwicklung verwenden [gulp](http://gulpjs.com/) als Taskausführung für den Buildprozess für Folgendes:</span><span class="sxs-lookup"><span data-stu-id="f88d7-138">SharePoint client-side development tools use [gulp](http://gulpjs.com/) as the build process task runner to:</span></span>

* <span data-ttu-id="f88d7-139">Bündeln und Minimieren von JavaScript- und CSS-Dateien</span><span class="sxs-lookup"><span data-stu-id="f88d7-139">Bundle and minify JavaScript and CSS files.</span></span>
* <span data-ttu-id="f88d7-140">Ausführen von Tools zum Aufrufen der Bündelungs- und Minimierungstasks vor jedem Build</span><span class="sxs-lookup"><span data-stu-id="f88d7-140">Run tools to call the bundling and minification tasks before each build.</span></span>
* <span data-ttu-id="f88d7-141">Kompilieren von LESS- oder SASS-Dateien in CSS</span><span class="sxs-lookup"><span data-stu-id="f88d7-141">Compile LESS or SASS files to CSS.</span></span>
* <span data-ttu-id="f88d7-142">Kompilieren von TypeScript-Dateien in JavaScript</span><span class="sxs-lookup"><span data-stu-id="f88d7-142">Compile TypeScript files to JavaScript.</span></span>

<span data-ttu-id="f88d7-143">Weitere Informationen zu gulp finden Sie in den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="f88d7-143">For more information about gulp, see the following:</span></span>

* [<span data-ttu-id="f88d7-144">Erste Schritte mit Gulp</span><span class="sxs-lookup"><span data-stu-id="f88d7-144">Getting started with Gulp</span></span>](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md)
* [<span data-ttu-id="f88d7-145">TypeScript und Gulp</span><span class="sxs-lookup"><span data-stu-id="f88d7-145">TypeScript and Gulp</span></span>](https://www.typescriptlang.org/docs/handbook/gulp.html)
* [<span data-ttu-id="f88d7-146">Artikel zu Gulp</span><span class="sxs-lookup"><span data-stu-id="f88d7-146">Articles about Gulp</span></span>](https://github.com/gulpjs/gulp/blob/master/docs/README.md#articles)

## <a name="webpack"></a><span data-ttu-id="f88d7-147">Webpack</span><span class="sxs-lookup"><span data-stu-id="f88d7-147">Webpack</span></span>

<span data-ttu-id="f88d7-148">Webpack ist ein Modulbundler, der aus Ihren Webpartdateien und Abhängigkeiten ein oder mehrere JavaScript-Bündel generiert, damit Sie unterschiedliche Bündel für unterschiedliche Szenarien laden können.</span><span class="sxs-lookup"><span data-stu-id="f88d7-148">Webpack is a module bundler that takes your web part files an dependencies and generates one or more JavaScript bundles so you can load different bundles for different scenarios.</span></span>

<span data-ttu-id="f88d7-p107">Die Entwicklungstoolkette verwendet [CommonJS](https://webpack.github.io/docs/commonjs.html) zum Bündeln. Auf diese Weise können Sie Module und Verwendungsmöglichkeiten definieren. Die Toolkette verwendet [SystemJS](https://github.com/systemjs/systemjs), ein universelles Modulladeprogramm, um Ihre Module zu laden. Auf diese Weise können Sie den Bereich für Ihre Webparts festlegen, indem Sie sicherstellen, dass jedes Webpart in seinem eigenen Namespace ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="f88d7-p107">The development tool chain uses [CommonJS](https://webpack.github.io/docs/commonjs.html) for bundling. This enables you to define modules and where you want to use them. The tool chain also uses [SystemJS](https://github.com/systemjs/systemjs), a universal module loader, to load your modules. This helps you to scope your web parts by making sure that each web part is executed in its own namespace.</span></span>

<span data-ttu-id="f88d7-153">Weitere Informationen zu webpack finden Sie in den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="f88d7-153">For more information about webpack, see the following:</span></span>

* [<span data-ttu-id="f88d7-154">Webpack-Dokumentation</span><span class="sxs-lookup"><span data-stu-id="f88d7-154">Webpack documentation</span></span>](http://webpack.github.io/docs/what-is-webpack.html)
* [<span data-ttu-id="f88d7-155">TypeScript, React und Webpack</span><span class="sxs-lookup"><span data-stu-id="f88d7-155">TypeScript, React, and Webpack</span></span>](https://www.typescriptlang.org/docs/handbook/react-&-webpack.html)

## <a name="yeoman-generators"></a><span data-ttu-id="f88d7-156">Yeoman-Generatoren</span><span class="sxs-lookup"><span data-stu-id="f88d7-156">Yeoman generators</span></span>
<span data-ttu-id="f88d7-p108">[Yeoman](http://yeoman.io/) hilft Ihnen bei den ersten Schritten mit neuen Projekten und stellt bewährte Methoden und Tools bereit, mit denen Sie produktiv arbeiten können. Der SharePoint-Yeoman-Generator ist im Rahmen des Frameworks für den Einstieg in neue clientseitige Webpartprojekte verfügbar.</span><span class="sxs-lookup"><span data-stu-id="f88d7-p108">[Yeoman](http://yeoman.io/) helps you to kickstart new projects, prescribing best practices and tools to help you stay productive. SharePoint Yeoman generator will be available as part of the framework to kickstart new client-side web part projects.</span></span> 

<span data-ttu-id="f88d7-159">Weitere Informationen zu Yeoman finden Sie in den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="f88d7-159">For more information about Yeoman, see the following:</span></span>

* [<span data-ttu-id="f88d7-160">Erstellen eines Gerüsts für eine Web-App mit Yeoman</span><span class="sxs-lookup"><span data-stu-id="f88d7-160">Scaffold a web app with Yeoman</span></span>](http://yeoman.io/codelab/index.html)
* [<span data-ttu-id="f88d7-161">Liste der verfügbaren Yeoman-Generatoren</span><span class="sxs-lookup"><span data-stu-id="f88d7-161">List of available Yeoman generators</span></span>](http://yeoman.io/generators/)

<span data-ttu-id="f88d7-162">Nachfolgend finden Sie einige häufig verwendete Yeoman-Generatoren, die Sie je nach dem von Ihnen ausgewählten Framework ausprobieren können:</span><span class="sxs-lookup"><span data-stu-id="f88d7-162">The following are some common Yeoman generators that you can try, depending on your choice of framework:</span></span>

* [<span data-ttu-id="f88d7-163">generator-react-webpack</span><span class="sxs-lookup"><span data-stu-id="f88d7-163">generator-react-webpack</span></span>](https://github.com/newtriks/generator-react-webpack)
* [<span data-ttu-id="f88d7-164">generator-angular</span><span class="sxs-lookup"><span data-stu-id="f88d7-164">generator-angular</span></span>](https://www.npmjs.com/package/generator-angular)

## <a name="source-code-editors"></a><span data-ttu-id="f88d7-165">Quellcode-Editoren</span><span class="sxs-lookup"><span data-stu-id="f88d7-165">Source code editors</span></span>
<span data-ttu-id="f88d7-166">SharePoint Framework wird clientseitig gesteuert. Daher können Sie einen HTML- und JavaScript-Code-Editor Ihrer Wahl verwenden, z. B.:</span><span class="sxs-lookup"><span data-stu-id="f88d7-166">SharePoint Framework is client-side driven and thus you can use your choice of HTML/JavaScript code editors, such as:</span></span>

* [<span data-ttu-id="f88d7-167">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f88d7-167">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* [<span data-ttu-id="f88d7-168">Atom</span><span class="sxs-lookup"><span data-stu-id="f88d7-168">Atom</span></span>](https://atom.io)
* [<span data-ttu-id="f88d7-169">WebStorm</span><span class="sxs-lookup"><span data-stu-id="f88d7-169">Webstorm</span></span>](https://www.jetbrains.com/webstorm)

<span data-ttu-id="f88d7-p109">In der SharePoint Framework-Dokumentation wird Visual Studio Code in den Dokumenten und Beispielen verwendet. Visual Studio Code ist ein einfacher und dennoch leistungsfähiger Quellcode-Editor von Microsoft, der auf dem Desktop ausgeführt wird und für Windows, Mac und Linux verfügbar ist. Er verfügt über integrierte Unterstützung für JavaScript, TypeScript und Node.js und bietet ein reichhaltiges Ökosystem von Erweiterungen für andere Sprachen (wie C++, C#, Python, PHP) und Laufzeiten.</span><span class="sxs-lookup"><span data-stu-id="f88d7-p109">SharePoint Framework documentation uses Visual Studio code in the docs and examples. Visual Studio Code is a lightweight but powerful source code editor from Microsoft which runs on your desktop and is available for Windows, Mac and Linux. It comes with built-in support for JavaScript, TypeScript and Node.js and has a rich ecosystem of extensions for other languages (such as C++, C#, Python, PHP) and runtimes.</span></span>

## <a name="sharepoint-rest-apis"></a><span data-ttu-id="f88d7-173">SharePoint-REST-APIs</span><span class="sxs-lookup"><span data-stu-id="f88d7-173">SharePoint REST APIs</span></span>

<span data-ttu-id="f88d7-p110">Das SharePoint Framework ermöglicht wichtige Integrationen in SharePoint-Oberflächen und richtet sich an die Webentwicklung. Mit den REST-APIs von SharePoint können Sie mit SharePoint und anderen Arbeitslasten interagieren, aus denen Ihre Webpartfunktionalität besteht.</span><span class="sxs-lookup"><span data-stu-id="f88d7-p110">The SharePoint Framework provides key integrations with SharePoint experiences and targets web development. The SharePoint REST APIs enable you to interact with  SharePoint and other workloads that shape your web part functionality.</span></span> 

<span data-ttu-id="f88d7-176">Es wird empfohlen, dass Sie sich mit den folgenden REST-APIs vertraut machen:</span><span class="sxs-lookup"><span data-stu-id="f88d7-176">We recommend that you become familiar with the following set of REST APIs:</span></span>

* [<span data-ttu-id="f88d7-177">REST-APIs von SharePoint-Listen</span><span class="sxs-lookup"><span data-stu-id="f88d7-177">SharePoint List REST APIs</span></span>](https://msdn.microsoft.com/de-DE/library/office/dn292552.aspx)

## <a name="patterns-and-practices"></a><span data-ttu-id="f88d7-178">Patterns and Practices</span><span class="sxs-lookup"><span data-stu-id="f88d7-178">Patterns and Practices</span></span>

<span data-ttu-id="f88d7-p111">Die Initiative[Office Dev Patterns and Practices/SharePoint Pattern and Practices (PnP)](http://aka.ms/officedevpnp) bietet Codebeispiele, Muster und andere Ressourcen, die Ihnen bei der Umwandlung Ihrer vorhandenen Lösung in das SharePoint Framework behilflich sind. Machen Sie sich unbedingt mit den Codebeispielen und Anweisungen der PnP-Initiative vertraut.</span><span class="sxs-lookup"><span data-stu-id="f88d7-p111">The [Office Dev Patterns and Practices / SharePoint Pattern and Practices (PnP)](http://aka.ms/officedevpnp) initiative provides code samples, patterns, and other resources to help you transform your existing solution to the SharePoint Framework. Be sure to become familiar with the code samples and guidance that is available through the PnP effort.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f88d7-181">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f88d7-181">Additional resources</span></span>

* [<span data-ttu-id="f88d7-182">SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="f88d7-182">SharePoint Framework</span></span>](sharepoint-framework-overview.md)
* [<span data-ttu-id="f88d7-183">Erstellen eines clientseitigen Hallo Welt-Webparts</span><span class="sxs-lookup"><span data-stu-id="f88d7-183">Build a Hello World client-side web part</span></span>](web-parts/get-started/build-a-hello-world-web-part.md)
