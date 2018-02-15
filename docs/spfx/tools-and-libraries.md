---
title: "Entwicklungstools und -bibliotheken für das SharePoint Framework"
description: "Verwenden Sie clientseitige JavaScript-Bibliotheken, um Ihre Lösungen zu erstellen und clientseitige Webparts zu entwickeln."
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: 929d7abd3fa99573e5df2baa6af44c93b91b17de
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="sharepoint-framework-development-tools-and-libraries"></a><span data-ttu-id="b52c1-103">Entwicklungstools und -bibliotheken für das SharePoint-Framework</span><span class="sxs-lookup"><span data-stu-id="b52c1-103">SharePoint Framework development tools and libraries</span></span>

<span data-ttu-id="b52c1-p101">Das SharePoint Framework umfasst mehrere clientseitige JavaScript-Bibliotheken, die Sie zum Erstellen von Lösungen verwenden können. Dieser Artikel enthält eine Übersicht über die Tools und Bibliotheken, die Sie zum Entwickeln von clientseitigen Webparts verwenden können.</span><span class="sxs-lookup"><span data-stu-id="b52c1-p101">The SharePoint Framework includes several client-side JavaScript libraries that you can use to build your solutions. This article provides an overview of the tools and libraries that you can use to develop client-side web parts.</span></span>

## <a name="typescript"></a><span data-ttu-id="b52c1-106">TypeScript</span><span class="sxs-lookup"><span data-stu-id="b52c1-106">TypeScript</span></span>

<span data-ttu-id="b52c1-p102">Bei TypeScript handelt es sich um eine typisierte Obersprache zu JavaScript, die in einfaches JavaScript kompiliert. SharePoint-Tools für die clientseitige Entwicklung werden auf Basis von TypeScript-Klassen, -Modulen und -Schnittstellen erstellt. Sie können diese verwenden, um stabile clientseitige Webparts zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b52c1-p102">TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. SharePoint client-side development tools are built using TypeScript classes, modules, and interfaces. You can use these to build robust client-side web parts.</span></span> 

<span data-ttu-id="b52c1-110">Für die ersten Schritte mit TypeScript finden Sie in den folgenden Ressourcen Informationen:</span><span class="sxs-lookup"><span data-stu-id="b52c1-110">To get started with TypeScript, see the following resources:</span></span>

* [<span data-ttu-id="b52c1-111">TypeScript-Schnellstart</span><span class="sxs-lookup"><span data-stu-id="b52c1-111">TypeScript Quick Start</span></span>](https://www.typescriptlang.org/docs/tutorial.html)
* [<span data-ttu-id="b52c1-112">TypeScript-Umgebung</span><span class="sxs-lookup"><span data-stu-id="b52c1-112">TypeScript Playground</span></span>](https://www.typescriptlang.org/play/index.html)
* [<span data-ttu-id="b52c1-113">TypeScript-Handbuch</span><span class="sxs-lookup"><span data-stu-id="b52c1-113">TypeScript Handbook</span></span>](https://www.typescriptlang.org/docs/handbook/basic-types.html)
* [<span data-ttu-id="b52c1-114">TypeScript-Community bei Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="b52c1-114">TypeScript community on Stack Overflow</span></span>](https://stackoverflow.com/questions/tagged/typescript)

## <a name="javascript-frameworks"></a><span data-ttu-id="b52c1-115">JavaScript-Frameworks</span><span class="sxs-lookup"><span data-stu-id="b52c1-115">JavaScript frameworks</span></span>
<span data-ttu-id="b52c1-p103">Sie können eine beliebige Anzahl von JavaScript-Frameworks zum Entwickeln clientseitiger Webparts erstellen. Nachfolgend sehen Sie einige der gängigsten Frameworks:</span><span class="sxs-lookup"><span data-stu-id="b52c1-p103">You can choose any one of a number of JavaScript frameworks to develop client-side web parts. The following are some of the most popular:</span></span>

* [<span data-ttu-id="b52c1-118">React</span><span class="sxs-lookup"><span data-stu-id="b52c1-118">React</span></span>](https://facebook.github.io/react/)
* [<span data-ttu-id="b52c1-119">AngularJS 1.x</span><span class="sxs-lookup"><span data-stu-id="b52c1-119">AngularJS 1.x</span></span>](https://docs.angularjs.org/tutorial)
* [<span data-ttu-id="b52c1-120">Angular 2 for TypeScript 2.x</span><span class="sxs-lookup"><span data-stu-id="b52c1-120">Angular 2 for TypeScript 2.x</span></span>](https://angular.io/guide/quickstart)
* [<span data-ttu-id="b52c1-121">Handlebars</span><span class="sxs-lookup"><span data-stu-id="b52c1-121">Handlebars</span></span>](http://handlebarsjs.com/)

<span data-ttu-id="b52c1-p104">Da es sich bei clientseitigen Webparts um Komponenten handelt, die auf einer SharePoint-Seite abgelegt werden, wird empfohlen, dass Sie ein JavaScript-Framework auswählen, das ein ähnliches Komponentenmodell unterstützt. Einfache Frameworks, wie z. B. React, Handlebars und Angular 2, unterstützen alle ein Komponentenmodell und sind gut geeignet zum Erstellen clientseitiger Webparts.</span><span class="sxs-lookup"><span data-stu-id="b52c1-p104">Because client-side web parts are components that are dropped into a SharePoint page, we recommend that you choose a JavaScript framework that supports a similar component model. Lightweight frameworks such as React, Handlebars, and Angular 2 all support a component model and are well suited to building client-side web parts.</span></span> 

<span data-ttu-id="b52c1-124">Darüber hinaus wird empfohlen, dass Sie sich die [SharePoint PnP JavaScript-Core-Bibliothek](https://github.com/SharePoint/PnP-JS-Core) ansehen, bei der es sich um eine von der Community geförderte Initiative handelt, um einfachen Zugriff auf SharePoint-REST-APIs bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="b52c1-124">We also recommend you to have a look on [SharePoint PnP JavaScript Core library](https://github.com/SharePoint/PnP-JS-Core), which is a community driven effort targeted for providing easy access on SharePoint REST APIs.</span></span> 

## <a name="node-package-manager-npm"></a><span data-ttu-id="b52c1-125">Knotenpaket-Manager (npm)</span><span class="sxs-lookup"><span data-stu-id="b52c1-125">Node Package Manager (npm)</span></span>

<span data-ttu-id="b52c1-p105">Die SharePoint-Tools für die clientseitige Entwicklung verwenden den [npm](https://www.npmjs.com/)-Paket-Manager, der [NuGet](https://www.nuget.org/) ähnlich ist, um Abhängigkeiten und andere erforderliche JavaScript-Hilfsprogramme zu verwalten. npm ist in der Regel als Teil des Node.js-Setups enthalten.</span><span class="sxs-lookup"><span data-stu-id="b52c1-p105">SharePoint client-side development tools use the [npm](https://www.npmjs.com/) package manager, which is similar to [NuGet](https://www.nuget.org/), to manage dependencies and other required JavaScript helpers. npm is typically included as part of Node.js setup.</span></span>

<span data-ttu-id="b52c1-128">Weitere Informationen über npm finden Sie in der [npm-Dokumentation](https://docs.npmjs.com/).</span><span class="sxs-lookup"><span data-stu-id="b52c1-128">For more information about npm, see the [npm documentation](https://docs.npmjs.com/).</span></span>

## <a name="nodejs"></a><span data-ttu-id="b52c1-129">Node.js</span><span class="sxs-lookup"><span data-stu-id="b52c1-129">Node.js</span></span>

<span data-ttu-id="b52c1-130">Node.js ist eine plattformübergeifende Open Source-Laufzeitumgebung zum Hosten und Ausführen von JavaScript-Code.</span><span class="sxs-lookup"><span data-stu-id="b52c1-130">Node.js is an open source, cross-platform runtime environment for hosting and serving JavaScript code.</span></span> <span data-ttu-id="b52c1-131">Sie können Node.js verwenden, um serverseitige Webanwendungen zu entwickeln, die in JavaScript geschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="b52c1-131">You can use Node.js to develop server-side web applications written in JavaScript.</span></span> <span data-ttu-id="b52c1-132">Das Node.js-Ökosystem ist eng mit npm und Taskausführungen wie gulp verbunden, um eine effiziente Umgebung zum Erstellen von JavaScript-basierten Anwendungen bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="b52c1-132">The Node.js ecosystem is tightly coupled with npm and task runners such as gulp to provide an efficient environment for building JavaScript-based applications.</span></span> <span data-ttu-id="b52c1-133">Nodel.js ist IIS Express oder IIS ähnlich, umfasst aber Tools, die die clientseitige Entwicklung vereinfachen.</span><span class="sxs-lookup"><span data-stu-id="b52c1-133">Node.js is similar to IIS Express or IIS, but includes tools to simplify client-side development.</span></span> 

<span data-ttu-id="b52c1-134">Weitere Informationen zu Node.js finden Sie in den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="b52c1-134">For more information about Node.js, see the following:</span></span>

* [<span data-ttu-id="b52c1-135">Informationen zu Node.js</span><span class="sxs-lookup"><span data-stu-id="b52c1-135">About Node.js</span></span>](https://nodejs.org/en/about/)
* [<span data-ttu-id="b52c1-136">API-Referenzdokumentation zu Node.js</span><span class="sxs-lookup"><span data-stu-id="b52c1-136">Node.js API reference documentation</span></span>](https://nodejs.org/api/)
* [<span data-ttu-id="b52c1-137">Node.js-Syntax und -Beispiel</span><span class="sxs-lookup"><span data-stu-id="b52c1-137">Node.js Usage and Example</span></span>](https://nodejs.org/api/synopsis.html)

## <a name="gulp-task-runner"></a><span data-ttu-id="b52c1-138">Gulp-Taskausführung</span><span class="sxs-lookup"><span data-stu-id="b52c1-138">Gulp task runner</span></span>
<span data-ttu-id="b52c1-139">Die SharePoint-Tools für clientseitige Entwicklung verwenden [gulp](http://gulpjs.com/) als Taskausführung für den Buildprozess für Folgendes:</span><span class="sxs-lookup"><span data-stu-id="b52c1-139">SharePoint client-side development tools use [gulp](http://gulpjs.com/) as the build process task runner to:</span></span>

* <span data-ttu-id="b52c1-140">Bündeln und Minimieren von JavaScript- und CSS-Dateien</span><span class="sxs-lookup"><span data-stu-id="b52c1-140">Bundle and minify JavaScript and CSS files.</span></span>
* <span data-ttu-id="b52c1-141">Ausführen von Tools zum Aufrufen der Bündelungs- und Minimierungstasks vor jedem Build</span><span class="sxs-lookup"><span data-stu-id="b52c1-141">Run tools to call the bundling and minification tasks before each build.</span></span>
* <span data-ttu-id="b52c1-142">Kompilieren von LESS- oder SASS-Dateien in CSS</span><span class="sxs-lookup"><span data-stu-id="b52c1-142">Compile LESS or SASS files to CSS.</span></span>
* <span data-ttu-id="b52c1-143">Kompilieren von TypeScript-Dateien in JavaScript</span><span class="sxs-lookup"><span data-stu-id="b52c1-143">Compile TypeScript files to JavaScript.</span></span>

<span data-ttu-id="b52c1-144">Weitere Informationen zu gulp finden Sie in den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="b52c1-144">For more information about gulp, see the following:</span></span>

* [<span data-ttu-id="b52c1-145">Erste Schritte mit Gulp</span><span class="sxs-lookup"><span data-stu-id="b52c1-145">Getting started with Gulp</span></span>](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md)
* [<span data-ttu-id="b52c1-146">TypeScript und Gulp</span><span class="sxs-lookup"><span data-stu-id="b52c1-146">TypeScript and Gulp</span></span>](https://www.typescriptlang.org/docs/handbook/gulp.html)
* [<span data-ttu-id="b52c1-147">Artikel zu Gulp</span><span class="sxs-lookup"><span data-stu-id="b52c1-147">Articles about Gulp</span></span>](https://github.com/gulpjs/gulp/blob/master/docs/README.md#articles)

## <a name="webpack"></a><span data-ttu-id="b52c1-148">Webpack</span><span class="sxs-lookup"><span data-stu-id="b52c1-148">Webpack</span></span>

<span data-ttu-id="b52c1-149">Webpack ist ein Modulbundler, der aus Ihren Webpartdateien und Abhängigkeiten ein oder mehrere JavaScript-Bündel generiert, damit Sie unterschiedliche Bündel für unterschiedliche Szenarien laden können.</span><span class="sxs-lookup"><span data-stu-id="b52c1-149">Webpack is a module bundler that takes your web part files an dependencies and generates one or more JavaScript bundles so you can load different bundles for different scenarios.</span></span>

<span data-ttu-id="b52c1-p107">Die Entwicklungstoolkette verwendet [CommonJS](https://webpack.js.org/) zum Bündeln. Auf diese Weise können Sie Module und Verwendungsmöglichkeiten definieren. Die Toolkette verwendet [SystemJS](https://github.com/systemjs/systemjs), ein universelles Modulladeprogramm, um Ihre Module zu laden. Auf diese Weise können Sie den Bereich für Ihre Webparts festlegen, indem Sie sicherstellen, dass jedes Webpart in seinem eigenen Namespace ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b52c1-p107">The development tool chain uses [CommonJS](https://webpack.js.org/) for bundling. This enables you to define modules and where you want to use them. The tool chain also uses [SystemJS](https://github.com/systemjs/systemjs), a universal module loader, to load your modules. This helps you to scope your web parts by making sure that each web part is executed in its own namespace.</span></span>

<span data-ttu-id="b52c1-154">Weitere Informationen zu webpack finden Sie in den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="b52c1-154">For more information about webpack, see the following:</span></span>

* [<span data-ttu-id="b52c1-155">Webpack-Dokumentation</span><span class="sxs-lookup"><span data-stu-id="b52c1-155">Webpack documentation</span></span>](https://webpack.js.org/)
* [<span data-ttu-id="b52c1-156">TypeScript, React und Webpack</span><span class="sxs-lookup"><span data-stu-id="b52c1-156">TypeScript, React, and Webpack</span></span>](https://www.typescriptlang.org/docs/handbook/react-&-webpack.html)

## <a name="yeoman-generators"></a><span data-ttu-id="b52c1-157">Yeoman-Generatoren</span><span class="sxs-lookup"><span data-stu-id="b52c1-157">Yeoman generators</span></span>

<span data-ttu-id="b52c1-158">[Yeoman](http://yeoman.io/) hilft Ihnen bei den ersten Schritten mit neuen Projekten und stellt bewährte Methoden und Tools bereit, mit denen Sie produktiv arbeiten können.</span><span class="sxs-lookup"><span data-stu-id="b52c1-158">[Yeoman](http://yeoman.io/) helps you kick-start new projects, and prescribes best practices and tools to help you stay productive.</span></span> <span data-ttu-id="b52c1-159">Der Yeoman-Generator von SharePoint ist im Rahmen des Frameworks für den Einstieg in neue clientseitige Webpartprojekte verfügbar.</span><span class="sxs-lookup"><span data-stu-id="b52c1-159">The Yeoman SharePoint generator is available as part of the framework to kickstart new client-side web part projects.</span></span> 

<span data-ttu-id="b52c1-160">Weitere Informationen zu Yeoman finden Sie in den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="b52c1-160">For more information about Yeoman, see the following:</span></span>

* [<span data-ttu-id="b52c1-161">Erstellen eines Gerüsts für eine Web-App mit Yeoman</span><span class="sxs-lookup"><span data-stu-id="b52c1-161">Scaffold a web app with Yeoman</span></span>](http://yeoman.io/codelab/index.html)
* [<span data-ttu-id="b52c1-162">Liste der verfügbaren Yeoman-Generatoren</span><span class="sxs-lookup"><span data-stu-id="b52c1-162">List of available Yeoman generators</span></span>](http://yeoman.io/generators/)
* [<span data-ttu-id="b52c1-163">Erstellen von Gerüsten für Projekte unter Verwendung des Yeoman-Generators von SharePoint</span><span class="sxs-lookup"><span data-stu-id="b52c1-163">Scaffold projects using yeoman SharePoint generator</span></span>](toolchain/scaffolding-projects-using-yeoman-sharepoint-generator.md)

<span data-ttu-id="b52c1-164">Nachfolgend finden Sie einige häufig verwendete Yeoman-Generatoren, die Sie je nach dem von Ihnen ausgewählten Framework ausprobieren können:</span><span class="sxs-lookup"><span data-stu-id="b52c1-164">The following are some common Yeoman generators that you can try, depending on your choice of framework:</span></span>

* [<span data-ttu-id="b52c1-165">generator-react-webpack</span><span class="sxs-lookup"><span data-stu-id="b52c1-165">generator-react-webpack</span></span>](https://github.com/react-webpack-generators/generator-react-webpack)
* [<span data-ttu-id="b52c1-166">generator-angular</span><span class="sxs-lookup"><span data-stu-id="b52c1-166">generator-angular</span></span>](https://www.npmjs.com/package/generator-angular)

## <a name="source-code-editors"></a><span data-ttu-id="b52c1-167">Quellcode-Editoren</span><span class="sxs-lookup"><span data-stu-id="b52c1-167">Source code editors</span></span>

<span data-ttu-id="b52c1-168">SharePoint Framework wird clientseitig gesteuert. Daher können Sie einen HTML- und JavaScript-Code-Editor Ihrer Wahl verwenden, z. B.:</span><span class="sxs-lookup"><span data-stu-id="b52c1-168">SharePoint Framework is client-side driven and thus you can use your choice of HTML/JavaScript code editors, such as:</span></span>

* [<span data-ttu-id="b52c1-169">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b52c1-169">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* [<span data-ttu-id="b52c1-170">Atom</span><span class="sxs-lookup"><span data-stu-id="b52c1-170">Atom</span></span>](https://atom.io)
* [<span data-ttu-id="b52c1-171">WebStorm</span><span class="sxs-lookup"><span data-stu-id="b52c1-171">Webstorm</span></span>](https://www.jetbrains.com/webstorm)

<span data-ttu-id="b52c1-172">In der SharePoint-Framework-Dokumentation wird Visual Studio Code in den Dokumenten und Beispielen verwendet.</span><span class="sxs-lookup"><span data-stu-id="b52c1-172">SharePoint Framework documentation uses Visual Studio code in the steps and examples.</span></span> <span data-ttu-id="b52c1-173">Visual Studio Code ist ein einfacher und dennoch leistungsfähiger Quellcode-Editor von Microsoft, der auf dem Desktop ausgeführt wird und für Windows, Mac und Linux verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="b52c1-173">Visual Studio Code is a lightweight but powerful source code editor from Microsoft that runs on your desktop and is available for Windows, Mac, and Linux.</span></span> <span data-ttu-id="b52c1-174">Er verfügt über integrierte Unterstützung für JavaScript, TypeScript und Node.js und bietet ein reichhaltiges Ökosystem von Erweiterungen für andere Sprachen (wie C++, C#, Python, PHP) und Laufzeiten.</span><span class="sxs-lookup"><span data-stu-id="b52c1-174">It comes with built-in support for JavaScript, TypeScript, and Node.js, and has a rich ecosystem of extensions for other languages (such as C++, C#, Python, PHP) and runtimes.</span></span>

## <a name="sharepoint-rest-apis"></a><span data-ttu-id="b52c1-175">SharePoint-REST-APIs</span><span class="sxs-lookup"><span data-stu-id="b52c1-175">SharePoint REST APIs</span></span>

<span data-ttu-id="b52c1-p110">Das SharePoint Framework ermöglicht wichtige Integrationen in SharePoint-Oberflächen und richtet sich an die Webentwicklung. Mit den REST-APIs von SharePoint können Sie mit SharePoint und anderen Arbeitslasten interagieren, aus denen Ihre Webpartfunktionalität besteht.</span><span class="sxs-lookup"><span data-stu-id="b52c1-p110">The SharePoint Framework provides key integrations with SharePoint experiences and targets web development. The SharePoint REST APIs enable you to interact with  SharePoint and other workloads that shape your web part functionality.</span></span> 

<span data-ttu-id="b52c1-178">Es wird empfohlen, dass Sie sich mit den folgenden REST-APIs vertraut machen:</span><span class="sxs-lookup"><span data-stu-id="b52c1-178">We recommend that you become familiar with the following set of REST APIs:</span></span>

* [<span data-ttu-id="b52c1-179">REST-APIs von SharePoint-Listen</span><span class="sxs-lookup"><span data-stu-id="b52c1-179">SharePoint List REST APIs</span></span>](../sp-add-ins/working-with-lists-and-list-items-with-rest.md)

## <a name="patterns-and-practices"></a><span data-ttu-id="b52c1-180">Patterns and Practices</span><span class="sxs-lookup"><span data-stu-id="b52c1-180">Patterns and Practices</span></span>

<span data-ttu-id="b52c1-p111">Die Initiative[Office Dev Patterns and Practices/SharePoint Pattern and Practices (PnP)](http://aka.ms/officedevpnp) bietet Codebeispiele, Muster und andere Ressourcen, die Ihnen bei der Umwandlung Ihrer vorhandenen Lösung in das SharePoint Framework behilflich sind. Machen Sie sich unbedingt mit den Codebeispielen und Anweisungen der PnP-Initiative vertraut.</span><span class="sxs-lookup"><span data-stu-id="b52c1-p111">The [Office Dev Patterns and Practices / SharePoint Pattern and Practices (PnP)](http://aka.ms/officedevpnp) initiative provides code samples, patterns, and other resources to help you transform your existing solution to the SharePoint Framework. Be sure to become familiar with the code samples and guidance that is available through the PnP effort.</span></span>

## <a name="see-also"></a><span data-ttu-id="b52c1-183">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="b52c1-183">See also</span></span>

* [<span data-ttu-id="b52c1-184">SharePoint-Framework-Toolkette</span><span class="sxs-lookup"><span data-stu-id="b52c1-184">SharePoint Framework Toolchain</span></span>](toolchain/sharepoint-framework-toolchain.md)
* [<span data-ttu-id="b52c1-185">Erstellen eines clientseitigen Hallo Welt-Webparts</span><span class="sxs-lookup"><span data-stu-id="b52c1-185">Build a Hello World client-side web part</span></span>](web-parts/get-started/build-a-hello-world-web-part.md)
* [<span data-ttu-id="b52c1-186">Übersicht über das SharePoint-Framework</span><span class="sxs-lookup"><span data-stu-id="b52c1-186">SharePoint Framework Extensions Overview</span></span>](sharepoint-framework-overview.md)
