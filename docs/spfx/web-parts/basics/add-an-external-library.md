# <a name="add-an-external-library-to-your-sharepoint-client-side-web-part"></a>Hinzufügen einer externen Bibliothek zu Ihrem clientseitigen SharePoint-Webpart

Vielleicht möchten Sie eine oder mehrere JavaScript-Bibliotheken in Ihr Webpart einfügen. In diesem Artikel wird gezeigt, wie Sie eine externe Bibliothek bündeln und Bibliotheken freigeben.

## <a name="bundling-a-script"></a>Bündeln eines Skripts

Der Webpart-Bundler schließt standardmäßig automatisch jede Bibliothek ein, die eine Abhängigkeit des Webpartmoduls. Dies bedeutet, dass die Bibliothek in derselben JavaScript-Bundledatei wie Ihr Webpart bereitgestellt wird. Dies ist bei kleineren Bibliotheken hilfreich, die nicht in mehreren Webparts verwendet werden.

### <a name="example"></a>Beispiel

Schließen Sie die Zeichenfolge, die das [validator](https://www.npmjs.com/package/validator)-Paket der Bibliothek überprüft, in ein Webpart ein.

Laden Sie das validator-Paket von npm herunter:

```sh
npm install validator --save
```

>**Hinweis:** Da Sie TypeScript verwenden, benötigen Sie für das Paket, das Sie hinzufügen, Eingaben. Dies ist wichtig, wenn Sie Code schreiben, da TypeScript nur eine Obermenge von JavaScript ist. Der gesamte TypeScript-Code wird beim Kompilieren nach wie vor in JavaScript-Code konvertiert. Sie können mithilfe von  **npm** nach Eingaben suchen, beispielsweise: `npm install @types/{package} --save`

Erstellen Sie im Ordner Ihres Webparts eine Datei mit dem Namen `validator.d.ts`, und fügen Sie den nachfolgenden Code in die Datei ein:

>**Hinweis:** Einige Bibliotheken verfügen nicht über Eingaben. Zwar gibt es für die Bibliothek „Validator“ eine [von der Community bereitgestellte Eingabendatei](https://www.npmjs.com/package/@types/validator); in diesem Artikel gehen wir aber davon aus, dass keine solche Datei existiert. In einem solchen Fall müssen Sie eine eigene Eingabendefinitionsdatei `.d.ts` für die Bibliothek erstellen. Der Code unten ist hierfür ein Beispiel.

```typescript
declare module "validator" {
    export function isEmail(email: string): boolean;
    export function isAscii(text: string): boolean;
}
```

Importieren Sie die Eingaben in Ihre Webpartdatei:

```typescript
import * as validator from 'validator';
```

Verwenden Sie die validator-Bibliothek im Webpartcode:

```typescript
validator.isEmail('someone@example.com');
```

## <a name="sharing-a-library-among-multiple-webparts"></a>Freigeben einer Bibliothek zwischen mehreren WebParts

Ihre clientseitige Lösung umfasst möglicherweise mehrere Webparts. Diese Webparts müssen möglicherweise die gleiche Bibliothek importieren oder freigeben. In solchen Fällen sollten Sie die Bibliothek in eine separate JavaScript-Datei einschließen, anstatt sie zu bündeln, um Leistung und Zwischenspeicherung zu verbessern. Dies gilt besonders für größere Bibliotheken.

### <a name="example"></a>Beispiel

In diesem Beispiel geben Sie das [marked](https://www.npmjs.com/package/marked)-Paket - einen Markdown-Compiler - in einem separaten Bundle frei.

Herunterladen des **marked**-Pakets von npm:

```sh
npm install marked --save
```

Herunterladen der Eingaben:

```
npm install @types/marked --save
```

Bearbeiten Sie **config/config.json**, und fügen Sie einen Eintrag zur Zuordnung **externals** hinzu. Dadurch wird dem Bundler mitgeteilt, dies in einer separaten Datei zu platzieren. Dadurch wird verhindert, dass der Bundler diese Bibliothek bündelt:

```json
"marked": "node_modules/marked/marked.min.js"
```

Fügen Sie die Anweisung zum Importieren der `marked`-Bibliothek nun in das Webpart ein, nachdem Sie das Paket und die Eingaben für die Bibliothek hinzugefügt haben:

```typescript
import * as marked from 'marked';
```

Verwenden der Bibliothek im Webpart:

```typescript
console.log(marked('I am using __markdown__.'));
```

## <a name="loading-a-script-from-a-cdn"></a>Laden eines Skripts aus einem CDN

Anstatt die Bibliothek aus einem npm-Paket zu laden, können Sie ein Skript aus einem CDN laden. Bearbeiten Sie hierzu die **config.json**-Datei, um die Bibliothek von ihrer CDN-URL zu laden.

### <a name="example"></a>Beispiel

In diesem Beispiel laden Sie jQuery aus einem CDN. Sie müssen nicht das npm-Paket installieren. Sie müssen jedoch die Eingaben installieren.

Installieren der Eingaben für jQuery:

```sh
npm install --save @types/jquery
```

Aktualisieren Sie `config.json` im Ordner `config`, um jQuery aus einem CDN zu laden. Hinzufügen eines Eintrags zum `externals`-Feld:

```json
"jquery": "https://code.jquery.com/jquery-3.1.0.min.js"
```

Importieren von jQuery in das Webpart:

```typescript
import * as $ from 'jquery';
```

Verwenden von jQuery in das Webpart:

```javascript
alert( $('#foo').val() );
```

## <a name="loading-a-non-amd-module"></a>Laden eines Nicht-AMD-Moduls

Einige Skripts folgen dem veralteten JavaScript-Muster des Speicherns der Bibliothek im globalen Namespace. Dieses Muster wurde nun durch [Universal Modul Definitions (UMD)](https://github.com/umdjs/umd), /[Asynchronous Module Definitions (AMD)](https://en.wikipedia.org/wiki/Asynchronous_module_definition) oder [ES6-Module](https://github.com/lukehoban/es6features/blob/master/README.md#modules) ersetzt. Möglicherweise müssen Sie solche Bibliotheken jedoch in das Webpart laden.

> **Tipp:** Es ist schwierig, manuell zu ermitteln, ob das Skript, das Sie versuchen zu laden, ein AMD- oder ein Nicht-AMD-Skript ist. Dies trifft insbesondere dann zu, wenn das Skript, das Sie laden möchten, minimiert ist. Wenn das Skript auf einer öffentlich zugänglichen URL gehostet wird, können Sie das kostenlose Tool [Rencore SharePoint Framework Script Check](https://rencore.com/sharepoint-framework/script-check/) verwenden, um den Skripttyp zu ermitteln. Außerdem stellt das Tool fest, ob der Hostingspeicherort, von dem Sie das Skript laden, ordnungsgemäß konfiguriert ist.

Um ein Nicht-AMD-Modul zu laden, fügen Sie eine zusätzliche Eigenschaft zu dem Eintrag in der **config.json**-Datei hinzu.

### <a name="example"></a>Beispiel

In diesem Beispiel laden Sie ein fiktives Nicht-AMD-Modul aus dem Contoso-CDN. Diese Schritte gelten für alle Nicht-AMD Skripts im Verzeichnis „src/“ oder „node_modules/“.

Das Skript heißt **Contoso.js** und ist unter **https://contoso.com/contoso.js** gespeichert. Sein Inhalt ist wie folgt:

```javascript
var ContosoJS = {
  say: function(text) { alert(text); },
  sayHello: function(name) { alert('Hello, ' + name + '!'); }
};
```

Erstellen von Eingaben für das Skript in einer Datei mit dem Namen **contoso.d.ts** im Webpartordner.

```typescript
declare module "contoso" {
    interface IContoso {
        say(text: string): void;
        sayHello(name: string): void;
    }
    var contoso: IContoso;
    export = contoso;
}
```

Aktualisieren der **config.json**-Datei derart, dass dieses Skript eingeschlossen wird. Hinzufügen eines Eintrags zur **externals**-Zuordnung:

```json
{
    "contoso": {
        "path": "https://contoso.com/contoso.js",
        "globalName": "ContosoJS"
    }
}
```

Hinzufügen eines Imports zum Webpartcode:

```typescript
import contoso from 'contoso';
```

Verwenden der Contoso-Bibliothek im Code:

```typescript
contoso.sayHello(username);
```

## <a name="loading-a-library-that-has-a-dependency-on-another-library"></a>Laden einer Bibliothek, die eine Abhängigkeit von einer anderen Bibliothek aufweist

Viele Bibliotheken weisen Abhängigkeiten von einer anderen Bibliothek auf. Sie können solche Abhängigkeiten in der **config.json**-Datei mithilfe der **globalDependencies**-Eigenschaft angeben.

> **Wichtig:** Beachten Sie, dass Sie dieses Feld für AMD-Module nicht angeben müssen; diese importieren sich ordnungsgemäß gegenseitig. Ein Nicht-AMD-Modul kann jedoch kein AMD-Modul als Abhängigkeit aufweisen. In einigen Fällen kann ein AMD-Skript als Nicht-AMD-Skript geladen werden. Dies ist häufig erforderlich, wenn mit jQuery (selbst ein AMD-Skript) und jQuery-Plug-Ins gearbeitet wird, die meistens als Nicht-AMD-Skripts verteilt werden und von jQuery abhängig sind.

Hierfür gibt es zwei Beispiele.

### <a name="non-amd-module-has-a-non-amd-module-dependency"></a>Nicht-AMD-Modul weist eine Abhängigkeit zu einem Nicht-AMD-Modul auf

In diesem Beispiel gibt es zwei fiktive Skripts. Sie befinden sich im Ordner **src/**, können jedoch auch aus einem CDN geladen werden.

**ContosoUI.js**

```javascript
Contoso.EventList = {
    alert: function() {
        var events = Contoso.getEvents();
        events.forEach( function(event) {
            alert(event);
        });
    }
}
```

**ContosoCore.js**

```javascript
var Contoso = {
    getEvents: function() {
        return ['A', 'B', 'C'];
    }
};
```

Fügen Sie Eingaben für diese Klasse hinzu, oder erstellen Sie sie. In diesem Fall erstellen Sie `Contoso.d.ts` mit Eingaben für beide JavaScript-Dateien.

**contoso.d.ts**

```typescript
declare module "contoso" {
    interface IEventList {
        alert(): void;
    }
    interface IContoso {
        getEvents(): string[];
        EventList: IEventList;
    }
    var contoso: IContoso;
    export = contoso;
}
```

Aktualisieren Sie die **config.json**-Datei. Hinzufügen von zwei Einträgen zu **externals**:

```json
{
     "contoso": {
         "path": "/src/ContosoCore.js",
         "globalName": "Contoso"
     },
     "contoso-ui": {
         "path": "/src/ContosoUI.js",
         "globalName": "Contoso",
         "globalDependencies": ["contoso"]
     }
}
```

Hinzufügen von Importen für Contoso und ContosoUI:

```typescript
import contoso = require('contoso');
require('contoso-ui');
```

Verwenden der Bibliotheken im Code:

```typescript
contoso.EventList.alert();
```

## <a name="loading-sharepoint-jsom"></a>Laden von SharePoint JSOM

Das Laden von SharePoint JSOM ist im Wesentlichen das gleiche Szenario wie das Laden von Nicht-AMD-Skripts, die Abhängigkeiten haben. Hierfür wird sowohl die Option **globalName** als auch die Option **globalDependency** verwendet.

> **Wichtig:** Beachten Sie, dass bei dem folgenden Ansatz Fehler in klassischen SharePoint-Seiten verursacht werden, auf denen SharePoint JSOM bereits geladen ist. Wenn Sie möchten, dass Ihr Webpart sowohl mit klassischen als auch mit modernen Seiten funktioniert, sollten Sie zuerst prüfen, ob SharePoint JSOM bereits verfügbar ist. Falls nicht, laden Sie es dynamisch mithilfe von **SPComponentLoader**.

Installieren von Eingaben für Microsoft Ajax (Abhängigkeit für JSOM-Eingaben):

```sh
npm install @types/microsoft-ajax --save
```

Installieren von Eingaben für JSOM:

```sh
npm install @types/sharepoint --save
```

Hinzufügen von Einträgen zu `config.json`:

```json
{
    "sp-init": {
        "path": "https://CONTOSO.sharepoint.com/_layouts/15/init.js",
        "globalName": "$_global_init"
    },
    "microsoft-ajax": {
        "path": "https://CONTOSO.sharepoint.com/_layouts/15/MicrosoftAjax.js",
        "globalName": "Sys",
        "globalDependencies": [ "sp-init" ]
    },
    "sp-runtime": {
        "path": "https://CONTOSO.sharepoint.com/_layouts/15/SP.Runtime.js",
        "globalName": "SP",
        "globalDependencies": [ "microsoft-ajax" ]
    },
    "sharepoint": {
        "path": "https://CONTOSO.sharepoint.com/_layouts/15/SP.js",
        "globalName": "SP",
        "globalDependencies": [ "sp-runtime" ]
    }
}
```

Fügen Sie in Ihrem Webpart die require-Anweisungen hinzu:

```typescript
require('sp-init');
require('microsoft-ajax');
require('sp-runtime');
require('sharepoint');
```

## <a name="load-localized-resources"></a>Laden lokalisierter Ressourcen

Es gibt eine Zuordnung in **config.json** mit dem Namen **localizedResources**, mit der Sie beschreiben können, wie lokalisierte Ressourcen geladen werden. Pfade in dieser Zuordnung sind relativ zum **lib**-Ordner und dürfen keinen vorangestellten Schrägstrich (**/**) enthalten.

In diesem Beispiel haben Sie den Ordner **src/strings/**. In diesem Ordner befinden sich mehrere JavaScript-Dateien mit Namen wie **en-us.js**, **fr-fr.js**, **de-de.js**. Da jede dieser Dateien vom Modulladeprogramm geladen werden muss, müssen sie einen CommonJS-Wrapper enthalten. In **en-us.js** beispielsweise:

```typescript
  define([], function() {
    return {
      "PropertyPaneDescription": "Description",
      "BasicGroupName": "Group Name",
      "DescriptionFieldLabel": "Description Field"
    }
  });
```

Bearbeiten Sie die **config.json**-Datei. Fügen Sie einen Eintrag zu **localizedResources** hinzu. **{locale}** ist ein Platzhaltertoken für den Gebietsschemanamen:

```json
{
    "strings": "strings/{locale}.js"
}
```

Fügen Sie Eingaben für Ihre Zeichenfolgen hinzu. In diesem Fall haben Sie die Datei **MyStrings.d.ts**:

```typescript
declare interface IStrings {
    webpartTitle: string;
    initialPrompt: string;
    exitPrompt: string;
}

declare module 'mystrings' {
    const strings: IStrings;
    export = strings;
}
```

Hinzufügen von Importen für die Zeichenfolgen in Ihrem Projekt:

```typescript
import * as strings from 'mystrings';
```

Verwenden der Zeichenfolgen in Ihrem Projekt:

```typescript
alert(strings.initialPrompt);
```
