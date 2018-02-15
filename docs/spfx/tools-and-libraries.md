---
title: "Entwicklungstools und -bibliotheken für das SharePoint Framework"
description: "Verwenden Sie clientseitige JavaScript-Bibliotheken, um Ihre Lösungen zu erstellen und clientseitige Webparts zu entwickeln."
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: 5c256aae2c4fb4453f1b6a2b5fb4e91ede8ce78f
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/05/2018
---
# <a name="sharepoint-framework-development-tools-and-libraries"></a>Entwicklungstools und -bibliotheken für das SharePoint-Framework

Das SharePoint Framework umfasst mehrere clientseitige JavaScript-Bibliotheken, die Sie zum Erstellen von Lösungen verwenden können. Dieser Artikel enthält eine Übersicht über die Tools und Bibliotheken, die Sie zum Entwickeln von clientseitigen Webparts verwenden können.

## <a name="typescript"></a>TypeScript

Bei TypeScript handelt es sich um eine typisierte Obersprache zu JavaScript, die in einfaches JavaScript kompiliert. SharePoint-Tools für die clientseitige Entwicklung werden auf Basis von TypeScript-Klassen, -Modulen und -Schnittstellen erstellt. Sie können diese verwenden, um stabile clientseitige Webparts zu erstellen. 

Für die ersten Schritte mit TypeScript finden Sie in den folgenden Ressourcen Informationen:

* [TypeScript-Schnellstart](https://www.typescriptlang.org/docs/tutorial.html)
* [TypeScript-Umgebung](https://www.typescriptlang.org/play/index.html)
* [TypeScript-Handbuch](https://www.typescriptlang.org/docs/handbook/basic-types.html)
* [TypeScript-Community bei Stack Overflow](https://stackoverflow.com/questions/tagged/typescript)

## <a name="javascript-frameworks"></a>JavaScript-Frameworks
Sie können eine beliebige Anzahl von JavaScript-Frameworks zum Entwickeln clientseitiger Webparts erstellen. Nachfolgend sehen Sie einige der gängigsten Frameworks:

* [React](https://facebook.github.io/react/)
* [AngularJS 1.x](https://docs.angularjs.org/tutorial)
* [Angular 2 for TypeScript 2.x](https://angular.io/guide/quickstart)
* [Handlebars](http://handlebarsjs.com/)

Da es sich bei clientseitigen Webparts um Komponenten handelt, die auf einer SharePoint-Seite abgelegt werden, wird empfohlen, dass Sie ein JavaScript-Framework auswählen, das ein ähnliches Komponentenmodell unterstützt. Einfache Frameworks, wie z. B. React, Handlebars und Angular 2, unterstützen alle ein Komponentenmodell und sind gut geeignet zum Erstellen clientseitiger Webparts. 

Darüber hinaus wird empfohlen, dass Sie sich die [SharePoint PnP JavaScript-Core-Bibliothek](https://github.com/SharePoint/PnP-JS-Core) ansehen, bei der es sich um eine von der Community geförderte Initiative handelt, um einfachen Zugriff auf SharePoint-REST-APIs bereitzustellen. 

## <a name="node-package-manager-npm"></a>Knotenpaket-Manager (npm)

Die SharePoint-Tools für die clientseitige Entwicklung verwenden den [npm](https://www.npmjs.com/)-Paket-Manager, der [NuGet](https://www.nuget.org/) ähnlich ist, um Abhängigkeiten und andere erforderliche JavaScript-Hilfsprogramme zu verwalten. npm ist in der Regel als Teil des Node.js-Setups enthalten.

Weitere Informationen über npm finden Sie in der [npm-Dokumentation](https://docs.npmjs.com/).

## <a name="nodejs"></a>Node.js

Node.js ist eine plattformübergeifende Open Source-Laufzeitumgebung zum Hosten und Ausführen von JavaScript-Code. Sie können Node.js verwenden, um serverseitige Webanwendungen zu entwickeln, die in JavaScript geschrieben werden. Das Node.js-Ökosystem ist eng mit npm und Taskausführungen wie gulp verbunden, um eine effiziente Umgebung zum Erstellen von JavaScript-basierten Anwendungen bereitzustellen. Nodel.js ist IIS Express oder IIS ähnlich, umfasst aber Tools, die die clientseitige Entwicklung vereinfachen. 

Weitere Informationen zu Node.js finden Sie in den folgenden Themen:

* [Informationen zu Node.js](https://nodejs.org/en/about/)
* [API-Referenzdokumentation zu Node.js](https://nodejs.org/api/)
* [Node.js-Syntax und -Beispiel](https://nodejs.org/api/synopsis.html)

## <a name="gulp-task-runner"></a>Gulp-Taskausführung
Die SharePoint-Tools für clientseitige Entwicklung verwenden [gulp](http://gulpjs.com/) als Taskausführung für den Buildprozess für Folgendes:

* Bündeln und Minimieren von JavaScript- und CSS-Dateien
* Ausführen von Tools zum Aufrufen der Bündelungs- und Minimierungstasks vor jedem Build
* Kompilieren von LESS- oder SASS-Dateien in CSS
* Kompilieren von TypeScript-Dateien in JavaScript

Weitere Informationen zu gulp finden Sie in den folgenden Themen:

* [Erste Schritte mit Gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md)
* [TypeScript und Gulp](https://www.typescriptlang.org/docs/handbook/gulp.html)
* [Artikel zu Gulp](https://github.com/gulpjs/gulp/blob/master/docs/README.md#articles)

## <a name="webpack"></a>Webpack

Webpack ist ein Modulbundler, der aus Ihren Webpartdateien und Abhängigkeiten ein oder mehrere JavaScript-Bündel generiert, damit Sie unterschiedliche Bündel für unterschiedliche Szenarien laden können.

Die Entwicklungstoolkette verwendet [CommonJS](https://webpack.js.org/) zum Bündeln. Auf diese Weise können Sie Module und Verwendungsmöglichkeiten definieren. Die Toolkette verwendet [SystemJS](https://github.com/systemjs/systemjs), ein universelles Modulladeprogramm, um Ihre Module zu laden. Auf diese Weise können Sie den Bereich für Ihre Webparts festlegen, indem Sie sicherstellen, dass jedes Webpart in seinem eigenen Namespace ausgeführt wird.

Weitere Informationen zu webpack finden Sie in den folgenden Themen:

* [Webpack-Dokumentation](https://webpack.js.org/)
* [TypeScript, React und Webpack](https://www.typescriptlang.org/docs/handbook/react-&-webpack.html)

## <a name="yeoman-generators"></a>Yeoman-Generatoren

[Yeoman](http://yeoman.io/) hilft Ihnen bei den ersten Schritten mit neuen Projekten und stellt bewährte Methoden und Tools bereit, mit denen Sie produktiv arbeiten können. Der Yeoman-Generator von SharePoint ist im Rahmen des Frameworks für den Einstieg in neue clientseitige Webpartprojekte verfügbar. 

Weitere Informationen zu Yeoman finden Sie in den folgenden Themen:

* [Erstellen eines Gerüsts für eine Web-App mit Yeoman](http://yeoman.io/codelab/index.html)
* [Liste der verfügbaren Yeoman-Generatoren](http://yeoman.io/generators/)
* [Erstellen von Gerüsten für Projekte unter Verwendung des Yeoman-Generators von SharePoint](toolchain/scaffolding-projects-using-yeoman-sharepoint-generator.md)

Nachfolgend finden Sie einige häufig verwendete Yeoman-Generatoren, die Sie je nach dem von Ihnen ausgewählten Framework ausprobieren können:

* [generator-react-webpack](https://github.com/react-webpack-generators/generator-react-webpack)
* [generator-angular](https://www.npmjs.com/package/generator-angular)

## <a name="source-code-editors"></a>Quellcode-Editoren

SharePoint Framework wird clientseitig gesteuert. Daher können Sie einen HTML- und JavaScript-Code-Editor Ihrer Wahl verwenden, z. B.:

* [Visual Studio Code](https://code.visualstudio.com/)
* [Atom](https://atom.io)
* [WebStorm](https://www.jetbrains.com/webstorm)

In der SharePoint-Framework-Dokumentation wird Visual Studio Code in den Dokumenten und Beispielen verwendet. Visual Studio Code ist ein einfacher und dennoch leistungsfähiger Quellcode-Editor von Microsoft, der auf dem Desktop ausgeführt wird und für Windows, Mac und Linux verfügbar ist. Er verfügt über integrierte Unterstützung für JavaScript, TypeScript und Node.js und bietet ein reichhaltiges Ökosystem von Erweiterungen für andere Sprachen (wie C++, C#, Python, PHP) und Laufzeiten.

## <a name="sharepoint-rest-apis"></a>SharePoint-REST-APIs

Das SharePoint Framework ermöglicht wichtige Integrationen in SharePoint-Oberflächen und richtet sich an die Webentwicklung. Mit den REST-APIs von SharePoint können Sie mit SharePoint und anderen Arbeitslasten interagieren, aus denen Ihre Webpartfunktionalität besteht. 

Es wird empfohlen, dass Sie sich mit den folgenden REST-APIs vertraut machen:

* [REST-APIs von SharePoint-Listen](../sp-add-ins/working-with-lists-and-list-items-with-rest.md)

## <a name="patterns-and-practices"></a>Patterns and Practices

Die Initiative[Office Dev Patterns and Practices/SharePoint Pattern and Practices (PnP)](http://aka.ms/officedevpnp) bietet Codebeispiele, Muster und andere Ressourcen, die Ihnen bei der Umwandlung Ihrer vorhandenen Lösung in das SharePoint Framework behilflich sind. Machen Sie sich unbedingt mit den Codebeispielen und Anweisungen der PnP-Initiative vertraut.

## <a name="see-also"></a>Siehe auch

- [SharePoint-Framework-Toolkette](toolchain/sharepoint-framework-toolchain.md)
- [Erstellen eines clientseitigen Hallo Welt-Webparts](web-parts/get-started/build-a-hello-world-web-part.md)
- [Übersicht über das SharePoint-Framework](sharepoint-framework-overview.md)
