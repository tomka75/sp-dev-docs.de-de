---
title: Erweitern von Webpack in der SharePoint-Framework-Toolkette
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: c5156ce434a791658de3798ff0d7de2e73c42fb2
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="extending-webpack-in-the-sharepoint-framework-toolchain"></a>Erweitern von Webpack in der SharePoint-Framework-Toolkette

[Webpack](https://Webpack.js.org/) ist ein JavaScript-Modulbundler, der aus Ihren JavaScript-Dateien und deren Abhängigkeiten ein oder mehrere JavaScript-Dateien generiert, damit Sie unterschiedliche Codeausschnitte für verschiedene Szenarien laden können.

Die Framework-Toolkette verwendet CommonJS zum Bündeln. Auf diese Weise können Sie Module und Verwendungsmöglichkeiten definieren. Die Toolkette verwendet auch SystemJS, ein universelles Modulladeprogramm, um Ihre Module zu laden. Auf diese Weise können Sie den Bereich für Ihre Webparts festlegen, indem Sie sicherstellen, dass jedes Webpart in seinem eigenen Namespace ausgeführt wird.

Eine häufige Aufgabe, die Sie ggf. der SharePoint-Framework-Toolkette hinzufügen möchten, ist die Erweiterung der Webpack-Konfiguration mit benutzerdefinierten Ladeprogrammen und Plug-Ins.

## <a name="using-webpack-loaders"></a>Verwenden von Webpack-Ladeprogrammen
Es kommt häufig vor, dass eine Ressource ohne JavaScript während der Entwicklung importiert und verwendet werden soll. Dies erfolgt in der Regel mit Bildern oder Vorlagen. A [Webpack-Ladeprogramm](https://webpack.js.org/loaders/) konvertiert die Ressource in ein Format, das von der JavaScript-Anwendung verwendet werden kann, oder bietet einen einfachen Verweis, den die JavaScript-Anwendung verstehen kann. Eine Markdownvorlage zum Beispiel wird möglicherweise kompiliert und in eine Textzeichenfolge konvertiert während eine Bildressource in ein Base64-Inlinebild konvertiert wird oder auf diese mit einer URL verwiesen wird und sie in das `dist`-Verzeichnis für die Bereitstellung kopiert wird.

Es gibt eine Reihe von nützlichen Ladeprogrammen, von denen einige bereits durch die standardmäßige SharePoint-Framework-Webpack-Konfiguration verwendet werden, z. B.:

- HTML-Ladeprogramm
- JSON-Ladeprogramm
- loader-load-themed-styles

Das Erweitern der Framework-Webpack-Konfiguration mit benutzerdefinierten Ladeprogrammen ist ein einfacher Prozess, der in der [Webpack-Dokumentation](https://webpack.js.org/contribute/writing-a-loader/) beschrieben ist.

> Weitere Details zu Ladeprogrammen finden Sie in der [Dokumentation zu Webpack-Ladeprogrammen](https://webpack.js.org/loaders/)

## <a name="example-using-the-markdown-loader-package"></a>Beispiel: Verwenden des Pakets mit dem Markdown-Ladeprogramm
Verwenden wir als Beispiel das Paket mit dem [Markdown-Ladeprogramm](https://www.npmjs.com/package/markdown-loader).  Dies ist ein Ladeprogramm zum Verweisen auf eine `.md`-Datei und zur Ausgabe dieser als HTML-Zeichenfolge.

Sie können das vollständige Beispiel [hier](https://aka.ms/spfx-extend-Webpack-sample) herunterladen.

### <a name="step-1---install-the-package"></a>Schritt 1 – Installieren des Pakets
Wir möchten in unserem Projekt auf das Markdown-Ladeprogramm verweisen.

```
npm i --save markdown-loader
```

### <a name="step-2---configure-webpack"></a>Schritt 2 – Konfigurieren von Webpack
Nun, da wir das Paket installiert haben, können wir die SharePoint-Framework-Webpack-Konfiguration so konfigurieren, dass sie `markdown-loader` einschließt.

In der [Dokumentation zum Markdown-Ladeprogramm](https://github.com/peerigon/markdown-loader) wird gezeigt, wie die Webpack-Konfiguration erweitert wird, sodass sie das Ladeprogramm einschließt:

```JavaScript
{
  module: {
    rules: [
      {
        test: /\.md$/,
        use: [
          {
            loader: 'html-loader'
          },
          {
            loader: 'markdown-loader',
            options: {
              /* options for markdown-loader here */
            }
          }
        ]
      }
    ]
  }
}
```

Werfen wir nun einen Blick auf diese Konfiguration:
  - Das `rules`-Array in der Webpack-Konfiguration definiert eine Reihe von Dateipfadtests und die Ladeprogramme, die verwendet werden sollen, wenn eine Ressource dem Test entspricht. In diesem Fall sucht die `test`-Eigenschaft nach Dateipfaden, die mit `.md` enden.
  - Das `use`-Array beschreibt eine Liste der Ladeprogramme, die nacheinander auf die Ressource angewendet werden. Sie werden in der Reihenfolge vom letzten bis zum ersten angewendet. In diesem Fall wird als erstes Ladeprogramm `markdown-loader` und als letztes Ladeprogramm `html-loader` angewendet.
  - Wenn mehrere Ladeprogramme angegeben sind, wird das Ergebnis der einzelnen Ladeprogramme an das nächste Ladeprogramm mittels Pipe übergeben.

Wir verwenden diese Informationen für die Konfiguration in unserem Projekt.

Um dieses benutzerdefinierte Ladeprogramm zur SharePoint-Framework-Webpack-Konfiguration hinzuzufügen, muss die Buildaufgabe zur Konfiguration von Webpack angewiesen werden. Die Buildaufgaben werden in der Gulp-Datei `gulpfile.js` definiert, die sich im Stammverzeichnis des Projekts befindet.

Bearbeiten Sie `gulpfile.js` und fügen Sie folgenden Code direkt vor `build.initialize(gulp);` ein:

```JavaScript
build.configureWebpack.mergeConfig({
  additionalConfiguration: (generatedConfiguration) => {
    generatedConfiguration.module.rules.push(
      {
        test: /\.md$/,
        use: [
          {
            loader: 'html-loader'
          },
          {
            loader: 'markdown-loader'
          }
        ]
      }
    );

    return generatedConfiguration;
  }
});
```

Im Folgenden gehen wir die Schritte durch, die mit diesem Codeausschnitt ausgeführt werden:
  - Wie der Name nahe legt, konfiguriert `ConfigureWebpackTask` (als `build.configureWebpack` instanziiert) das Webpack. Es gibt zahlreiche spezielle Konfigurationsschritte, die beim Erstellen von SPFx-Projekten erforderlich sind, es gibt also nichttriviale Logik in dieser Aufgabe.
  - `ConfigureWebpackTask` verwendet eine optionale `additionalConfiguration`-Eigenschaft. Diese Eigenschaft soll auf eine Funktion festgelegt werden, die die generierte Konfiguration verwendet, unsere Änderungen an dieser vornimmt und anschließend die aktualisierte Konfiguration zurückgibt. **Beachten Sie, dass diese Funktion eine Webpack-Konfiguration an die Toolkette zurückgeben muss, andernfalls wird Webpack nicht ordnungsgemäß konfiguriert.**
  - Übergeben Sie im Text der Funktion, die auf `additionalConfiguration` festgelegt wurde, einfach eine neue Regel an den vorhandenen Satz von Regeln in der Konfiguration. Beachten Sie, dass diese neue Regel dem Beispiel in dem Konfigurationsausschnitt oben im **Schritt 2** ähnelt.

> Zwar können Sie mit diesem Ansatz die standardmäßige Webpack-Konfiguration der Toolkette vollständig ersetzen, doch wird dies (sofern nicht anders in der Dokumentation angegeben) nicht empfohlen, wenn Sie von maximaler Leistung und Optimierung profitieren möchten.

### <a name="step-3---update-your-code"></a>Schritt 3 – Aktualisieren des Code
Nun, da wir das Ladeprogramm konfiguriert haben, können wir den Code aktualisieren und einige Dateien hinzufügen, um das Szenario zu testen.

Erstellen Sie die Datei `my-markdown.md` im Verzeichnis `src` des Projektordners mit etwas Markdown-Text darin.

```md
#Hello Markdown

*Markdown* is a simple markup format to write content.

You can also format text as **bold** or *italics* or ***bold italics***
```

Wenn Sie das Projekt erstellen, konvertiert das Webpack-Markdown-Ladeprogramm den Markdown-Text in eine HTML-Zeichenfolge. Um diese HTML-Zeichenfolge in einer Ihrer `*.ts`-Quelldateien zu verwenden, fügen Sie die folgende Zeile `require()` nach dem Importieren oben in der Datei hinzu. Beispiel:


```TypeScript
const markdownString: string = require<string>('./../../../../src/readme.md');
```

Webpack sucht standardmäßig im `lib`-Ordner nach der Datei. `.md`-Dateien werden jedoch nicht standardmäßig in den `lib`-Ordner kopiert. Dies bedeutet, dass ein ziemlich langer relativer Pfad erstellt werden muss. Diese Einstellung lässt sich durch Definieren einer Konfigurationsdatei steuern, wodurch die Toolkette angewiesen wird, `md`-Dateien in den lib-Ordner zu kopieren.

Erstellen Sie die Datei `copy-static-assets.json` im Verzeichnis `config`. So wird das Buildsystem angewiesen, einige zusätzliche Dateien von `src` zu `lib` zu kopieren. Von dieser Buildaufgabe werden Dateien mit Erweiterungen, die von der Webpack-Standardkonfiguration der Toolkette verstanden werden, standardmäßig kopiert (wie z. B. `png` und `json`). Sie muss also nur angewiesen werden, auch `md`-Dateien zu kopieren.

```JSON
{
  "includeExtensions": [
    "md"
  ]
}
```

Anstelle des relativen Pfads können Sie nun den Dateipfad in Ihrer `require`-Anweisung verwenden, z. B.:

```TypeScript
const markdownString: string = require<string>('./../../readme.md');
```

Dann können Sie in Ihrem Code auf diese Zeichenfolge verweisen, z. B.:

``` TypeScript
public render(): void {
  this.domElement.innerHTML = markdownString;
}
```

### <a name="step-4---build-and-test-your-code"></a>Schritt 4: Erstellen und Testen des Codes
Führen Sie zum Erstellen und Testen des Codes den folgenden Befehl in einer Konsole im Stammverzeichnis des Projekts aus:

```
gulp serve
```
