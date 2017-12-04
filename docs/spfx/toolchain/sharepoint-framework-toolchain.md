---
title: "SharePoint Framework-Toolkette"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: cf62390105b5e32f9255cb8b35d8f660a249f9fc
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-framework-toolchain"></a>SharePoint Framework-Toolkette

Die SharePoint Framework-Toolkette ist eine Sammlung von Buildtools, Frameworkpaketen und anderen Elementen, mit denen Sie clientseitige Projekte erstellen und bereitstellen können. Die Toolkette unterstützt Sie bei der Erstellung clientseitiger Komponenten wie Webparts. Außerdem ermöglicht sie es Ihnen mit Tools wie der SharePoint Workbench, diese Komponenten in Ihrer lokalen Entwicklungsumgebung zu testen. Auch zum Packen und Bereitstellen auf SharePoint lässt sich die Toolkette nutzen. Darüber hinaus stellt sie verschiedene Buildbefehle für wichtige Buildtasks zur Verfügung, darunter unter anderem Befehle für die Codekompilierung und für das Packen clientseitiger Projekte in SharePoint-App-Pakete. 

## <a name="npm"></a>npm
Bevor wir auf die verschiedenen Komponenten der Toolkette eingehen, ist es wichtig, dass Sie verstehen, wie das SharePoint Framework [npm](https://www.npmjs.com/) zur Verwaltung der verschiedenen Module innerhalb eines Projekts verwendet. npm ist einer der bevorzugten Open Source-Paket-Manager für clientseitige JavaScript-Entwicklung. 

Ein typisches npm-Paket besteht aus einer oder mehreren wiederverwendbaren JavaScript-Codedateien (Modulen) sowie einer Liste von Abhängigkeitspaketen. Wenn Sie ein solches Paket installieren, installiert npm auch diese Abhängigkeiten. Die offizielle [npm-Registrierung](https://www.npmjs.com/) enthält Hunderte Pakete, die Sie herunterladen und zur Erstellung von Anwendungen verwenden können. Sie können auch [eigene Pakete auf npm veröffentlichen](https://docs.npmjs.com/getting-started/what-is-npm) und damit anderen Entwicklern zur Verfügung stellen. Das SharePoint Framework verwendet verschiedene npm-Pakete in der Toolkette und veröffentlicht auch [eigene Pakete in der npm-Registrierung](https://www.npmjs.com/search?q=%40microsoft%2Fsp-). 

### <a name="sharepoint-framework-packages"></a>SharePoint Framework-Pakete
Das SharePoint Framework besteht aus mehreren npm-Paketen, die ineinandergreifen und Sie bei der Erstellung clientseitiger Lösungen für SharePoint unterstützen. 

Folgende Pakete sind im SharePoint Framework enthalten:

* [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint): ein [Yeoman](http://yeoman.io/)-Plug-In zur Verwendung mit dem SharePoint Framework. Mit diesem Generator können Entwickler schnell neue Projekte für clientseitige Webparts mit sinnvollen Standardeinstellungen und Best Practices aufsetzen.

* [@microsoft/sp-client-base](https://www.npmjs.com/package/@microsoft/sp-client-base): Definiert die Kernbibliotheken für clientseitige Anwendungen, die mit dem SharePoint Framework erstellt werden.

* [@microsoft/sp-webpart-workbench](https://www.npmjs.com/package/@microsoft/sp-webpart-workbench): Die SharePoint Workbench ist eine eigenständige Umgebung, in der clientseitige Webparts getestet und debuggt werden können.

* [@microsoft/sp-module-loader](https://www.npmjs.com/package/@microsoft/sp-module-loader): ein Modulladeprogramm, das die Versionsverwaltung für clientseitige Komponenten, Webparts und andere Objekte übernimmt und diese lädt. Es stellt auch grundlegende Diagnosedienste bereit. Das Programm basiert auf bekannten Standards wie SystemJS und WebPack und ist die erste SharePoint Framework-Komponente, die auf einer Seite geladen wird.

* [@microsoft/sp-module-interfaces](https://www.npmjs.com/package/@microsoft/sp-module-interfaces): Definiert verschiedene Modulschnittstellen, die vom SharePoint Framework-Modulladeprogramm und dem SharePoint Framework-Buildsystem gemeinsam genutzt werden.

* [@microsoft/sp-lodash-subset](https://www.npmjs.com/package/@microsoft/sp-lodash-subset): Stellt ein benutzerdefiniertes [Lodash](https://lodash.com/)-Bundle bereit, das mit dem SharePoint Framework-Modulladeprogramm verwendet werden kann. Für bessere Leistung zur Laufzeit enthält es zudem einige der essenziellsten Lodash-Funktionen.

* [@microsoft/sp-tslint-rules](https://www.npmjs.com/package/@microsoft/sp-tslint-rules): Definiert benutzerdefinierte tslint-Regeln zur Verwendung in clientseitigen SharePoint-Projekten.

* [@microsoft/office-ui-fabric-react-bundle](https://www.npmjs.com/package/@microsoft/office-ui-fabric-react-bundle): Stellt ein benutzerdefiniertes [office-ui-fabric-react](https://www.npmjs.com/package/office-ui-fabric-react)-Bundle bereit, das für die Verwendung mit dem SharePoint Framework-Modulladeprogramm optimiert wurde.

### <a name="common-build-tool-packages"></a>Gängige Buildtoolpakete
Neben den SharePoint Framework-Paketen werden für Buildtasks wie die Kompilierung von TypeScript-Code in JavaScript und die Konvertierung von SCSS in CSS auch verschiedene weitere gängige Buildtools verwendet.

Die folgenden Pakete gängiger Buildtools sind im SharePoint Framework enthalten:

* [@microsoft/sp-build-core-tasks](https://www.npmjs.com/package/@microsoft/sp-build-core-tasks): eine Sammlung von Tasks für das SharePoint Framework-Buildsystem, basierend auf gulp. Das Paket `sp-build-core-tasks` implementiert SharePoint-spezifische Operationen wie das Packen von Lösungen und das Schreiben von Manifesten.

* [@microsoft/sp-build-web](https://www.npmjs.com/package/@microsoft/sp-build-web): Importiert und konfiguriert verschiedene Buildtasks für Buildziele, die in einem Webbrowser ausgeführt werden (statt in einer Node.js-Umgebung). Dieses Paket muss direkt über eine gulp-Datei importiert werden, die das SharePoint Framework-Buildsystem verwendet. 

* [@microsoft/gulp-core-build](https://www.npmjs.com/package/@microsoft/gulp-core-build): Die wichtigsten gulp-Buildtasks zur Erstellung von TypeScript-, HTML-, Less- und anderen Buildformaten. Dieses Paket hängt von mehreren anderen npm-Paketen ab, die folgende Tasks enthalten:
    - [@microsoft/gulp-core-build-typescript](https://www.npmjs.com/package/@microsoft/gulp-core-build-typescript)
    - [@microsoft/gulp-core-build-sass](https://www.npmjs.com/package/@microsoft/gulp-core-build-sass)
    - [@microsoft/gulp-core-build-webpack](https://www.npmjs.com/package/@microsoft/gulp-core-build-webpack)
    - [@microsoft/gulp-core-build-serve](https://www.npmjs.com/package/@microsoft/gulp-core-build-serve)
    - [@microsoft/gulp-core-build-karma](https://www.npmjs.com/package/@microsoft/gulp-core-build-karma)
    - [@microsoft/gulp-core-build-mocha](https://www.npmjs.com/package/@microsoft/gulp-core-build-mocha)

* [@microsoft/loader-cased-file](https://www.npmjs.com/package/@microsoft/loader-cased-file): ein Wrapper für das webpack-Modul [file-loader](https://www.npmjs.com/package/file-loader), der zur Modifizierung der Schreibweise des ausgegebenen Dateinamens verwendet werden kann. Das ist in verschiedenen Szenarien nützlich, zum Beispiel bei der Verwendung eines CDNs (Content Delivery Network), das nur Dateinamen aus Kleinbuchstaben zulässt.

* [@microsoft/loader-load-themed-styles](https://www.npmjs.com/package/@microsoft/loader-load-themed-styles): ein Ladeprogramm, das das Laden von CSS in ein Skript wie <code>require('load-themed-styles').loadStyles( /* css text */ )</code> einschließt. Es ist als Ersatz für „style-loader“ gedacht.

* [@microsoft/loader-raw-script](https://www.npmjs.com/package/@microsoft/loader-raw-script): ein Ladeprogramm, das die Inhalte von Skriptdateien per `eval(…)` direkt in ein webpack-Bündel lädt

* [@microsoft/loader-set-webpack-public-path](https://www.npmjs.com/package/@microsoft/loader-set-webpack-public-path): ein Ladeprogramm, das die Variable __webpack_public_path__ auf einen in den Argumenten spezifizierten Wert setzt, optional als Ergänzung zur SystemJs-Eigenschaft „baseURL“

## <a name="scaffolding-a-new-client-side-project"></a>Erstellen eines Gerüsts für ein neues clientseitiges Projekt
Der SharePoint-Generator erstellt ein Gerüst für ein clientseitiges Webpart-Projekt. Zudem lädt der Generator die erforderlichen Toolkettenkomponenten für das jeweilige clientseitige Projekt herunter und konfiguriert sie.  

### <a name="packages-installation"></a>Installieren von Paketen
Der Generator installiert die erforderlichen npm-Pakete lokal im Projektordner. Mit npm können Pakete entweder lokal im Projekt oder global installiert werden. Beide Varianten haben Vorteile, die [generelle Empfehlung](https://nodejs.org/en/blog/npm/npm-1-0-global-vs-local-installation/) ist jedoch, die npm-Pakete lokal zu installieren, wenn der Code von diesen Paketmodulen abhängt. Bei einem Webpart-Projekt hängt der Webpart-Code von den verschiedenen SharePoint-Buildpaketen und anderen gängigen Buildpaketen ab. Diese Pakete müssen daher lokal installiert werden. 

Bei der lokalen Installation der Pakete installiert npm auch die Abhängigkeiten jedes Pakets. Die installierten Pakete finden Sie im Ordner `node_modules` im Projektordner. Dieser Ordner enthält die Pakete sowie alle ihre Abhängigkeiten. Im Idealfall sollte dieser Ordner mehrere Dutzend bis mehrere Hundert Ordner enthalten, da npm-Pakete immer in kleinere Module aufgeteilt werden und daher mehrere Dutzend bis mehrere Hundert Pakete installiert werden. Die wichtigsten SharePoint Framework-Pakete liegen im Ordner `node_modules\@microsoft`. `@microsoft` ist ein npm-Bereich, der [von Microsoft veröffentlichte Pakete](https://www.npmjs.com/~microsoft) abbildet.

Immer, wenn ein neues Projekt mit dem Generator erstellt wird, installiert der Generator die SharePoint Framework-Pakete für das jeweilige Projekt samt ihrer Abhängigkeiten lokal. So macht npm es einfacher, Webpart-Projekte zu verwalten, ohne dass es Auswirkungen auf andere Projekte in der lokalen Entwicklungsumgebung gibt. 

### <a name="packagejson"></a>package.json
Die Datei `package.json` im clientseitigen Projekt enthält eine Liste der Abhängigkeiten des Projekts. Diese Liste definiert, welche Abhängigkeiten installiert werden müssen. Wie oben erwähnt kann jede Abhängigkeit wiederum weitere Abhängigkeiten enthalten. In npm können Sie über die Eigenschaften `dependencies` und `devDependencies` sowohl Laufzeit- als auch Buildabhängigkeiten definieren. Die Eigenschaft `devDependencies` kommt zum Einsatz, wenn das jeweilige Modul im Code verwendet werden soll. Das ist beispielsweise bei der Erstellung von Webparts der Fall.

Nachfolgend sehen Sie die Datei `package.json` für das [helloworld-Webpart](../web-parts/get-started/build-a-hello-world-web-part.md):

```json 
{
  "name": "helloword-webpart",
  "version": "0.0.1",
  "private": true,
  "engines": {
    "node": ">=0.10.0"
  },
  "dependencies": {
    "@microsoft/sp-client-base": "~1.0.0",
    "@microsoft/sp-core-library": "~1.0.0",
    "@microsoft/sp-webpart-base": "~1.0.0",
    "@types/webpack-env": ">=1.12.1 <1.14.0"
  },
  "devDependencies": {
    "@microsoft/sp-build-web": "~1.0.0",
    "@microsoft/sp-module-interfaces": "~1.0.0",
    "@microsoft/sp-webpart-workbench": "~1.0.0",
    "gulp": "~3.9.1",
    "@types/chai": ">=3.4.34 <3.6.0",
    "@types/mocha": ">=2.2.33 <2.6.0"
  },
  "scripts": {
    "build": "gulp bundle",
    "clean": "gulp clean",
    "test": "gulp test"
  }
}
```

Zwar werden für ein Projekt sehr viele Pakete installiert; sie sind aber nur für die Erstellung des Webparts in der Entwicklungsumgebung erforderlich. Mithilfe dieser Pakete können Sie alle nötigen Module und Abhängigkeiten implementieren, um Ihr Webpart zu erstellen, es zu kompilieren, ein Bundling für es durchzuführen und es für die Bereitstellung zu packen. Die finale und minimierte Bundle-Version des Webparts, die Sie auf einem CDN-Server oder auf SharePoint bereitstellen, enthält keines dieser Pakete. Allerdings können Sie Ihr Webpart je nach den konkreten Anforderungen auch so konfigurieren, dass es bestimmte Module enthält. Weitere Informationen finden Sie unter [Add an external library to a web part](../web-parts/basics/add-an-external-library.md).

### <a name="working-with-source-control-systems"></a>Arbeiten mit Quellcodeverwaltungssystemen
Je mehr Projektabhängigkeiten es gibt, desto mehr Pakete müssen installiert werden. Es empfiehlt sich nicht, den Ordner `node_modules` in das Quellcodeverwaltungssystem einzuchecken, da er alle Abhängigkeiten enthält. Sie sollten den Ordner `node_modules` in die Liste der Dateien aufnehmen, die beim Einchecken ignoriert werden. 

Wenn Sie `git` als Quellcodeverwaltungssystem verwenden: Webpart-Projekte mit Yeoman-Gerüst enthalten eine Datei `.gitignore`, die den Ordner `node_modules` und andere Elemente vom Einchecken ausschließt. Beim ersten Auschecken oder Klonen eines Webpart-Projekts aus dem Quellcodeverwaltungssystem müssen Sie den Befehl zur Initialisierung und lokalen Installation aller Projektabhängigkeiten ausführen:

```
npm i
```

npm überprüft die Datei `package.json` und installiert alle erforderlichen Abhängigkeiten. 

## <a name="build-tasks"></a>Buildtasks
Das SharePoint Framework verwendet [gulp](http://gulpjs.com/) zur Taskausführung. gulp bearbeitet Prozesse wie die folgenden:

* Bundling und Minimieren von JavaScript- und CSS-Dateien
* Ausführen von Tools zum Aufrufen der Bündelungs- und Minimierungstasks vor jedem Build
* Kompilieren von LESS- oder SASS-Dateien in CSS
* Kompilieren von TypeScript-Dateien in JavaScript

Die Toolkette besteht aus den folgenden gulp-Tasks, die im Paket [@microsoft/sp-build-core-tasks](https://www.npmjs.com/package/@microsoft/sp-build-core-tasks) definiert sind:

* build
  * Erstellt das clientseitige Lösungsprojekt.
* bundle
  * Bündelt den Einstiegspunkt des clientseitigen Lösungsprojekts sowie alle seine Abhängigkeiten in einer einzigen JavaScript-Datei.
* serve
  * Liefert das clientseitige Lösungsprojekt sowie andere Objekte vom lokalen Rechner aus.
* clean
  * Löscht die Buildartefakte des clientseitigen Lösungsprojekts aus dem vorherigen Build und den Buildzielverzeichnissen („lib“ und „dist“).
* test
  * Führt Einheitentests für das clientseitige Lösungsprojekt durch (falls verfügbar). 
* package-solution
  * Packt die clientseitige Lösung in ein SharePoint-Paket.
* deploy-azure-storage
  * Stellt die Objekte des clientseitigen Lösungsprojekts in Azure Storage bereit. 

Zur Initiierung der Tasks hängen Sie den Tasknamen an den gulp-Befehl an. Wenn Sie zum Beispiel Ihr Webpart kompilieren und eine Vorschau in der SharePoint Workbench anzeigen wollen, führen Sie den folgenden Befehl aus:

```
gulp serve
```

>**Hinweis**: Es lassen sich nicht mehrere Tasks gleichzeitig ausführen.

`serve` führt die verschiedenen Tasks aus und startet im Anschluss SharePoint Workbench.

![Task „gulp serve“](../../images/toolchain-gulp-serve-task.png)

### <a name="build-targets"></a>Buildziele
Im Screenshot oben sehen Sie, dass der Task folgendes Buildziel setzt:

```
Build target: DEBUG
```

Wird kein Parameter angegeben, setzen die Befehle automatisch den BUILD-Modus als Ziel. Wenn Sie den Parameter `ship` angeben, setzen die Befehle den SHIP-Modus als Ziel.

In der Regel setzen Sie SHIP als Ziel, wenn das Webpart-Projekt zur Auslieferung an oder Bereitstellung auf einem Produktionsserver bereit ist. Für andere Szenarien wie Tests und Debugging würden Sie BUILD als Ziel setzen. Das Ziel SHIP stellt auch sicher, dass die minimierte Version des Webpart-Bundles erstellt wird. 

Um den SHIP-Modus als Ziel zu setzen, hängen Sie `--ship` an den Task an:

```
gulp --ship
```

Im DEBUG-Modus kopieren die Buildtasks alle Webpart-Objekte inklusive des Webpart-Bundles in den Ordner `dist`.

Im SHIP-Modus kopieren die Buildtasks alle Webpart-Objekte inklusive des Webpart-Bundles in den Ordner `temp\deploy`.
