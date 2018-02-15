---
title: "Hinzufügen einer externen Bibliothek zu Ihrem clientseitigen SharePoint-Webpart"
description: "Bündeln einer externen JavaScript-Bibliothek und Freigeben von Bibliotheken."
ms.date: 01/29/2018
ms.prod: sharepoint
ms.openlocfilehash: 7b5091f531ad16127aa71299f9c1951cbb2c853c
ms.sourcegitcommit: e4bf60eabffe63dc07f96824167d249c0678db82
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/30/2018
---
# <a name="add-an-external-library-to-your-sharepoint-client-side-web-part"></a>Hinzufügen einer externen Bibliothek zu Ihrem clientseitigen SharePoint-Webpart

Vielleicht möchten Sie eine oder mehrere JavaScript-Bibliotheken in Ihr Webpart einfügen. In diesem Artikel wird gezeigt, wie Sie eine externe Bibliothek bündeln und Bibliotheken freigeben.

## <a name="bundle-a-script"></a>Bündeln eines Skripts

Der Webpart-Bundler schließt standardmäßig automatisch jede Bibliothek ein, die eine Abhängigkeit des Webpartmoduls aufweist. Dies bedeutet, dass die Bibliothek in derselben JavaScript-Bundledatei wie Ihr Webpart bereitgestellt wird. Dies ist bei kleineren Bibliotheken hilfreich, die nicht in mehreren Webparts verwendet werden.

### <a name="example"></a>Beispiel

1. Schließen Sie die Zeichenfolge, die das [validator](https://www.npmjs.com/package/validator)-Paket der Bibliothek überprüft, in ein Webpart ein.

2. Laden Sie das validator-Paket von npm herunter:

    ```sh
    npm install validator --save
    ```

    > [!NOTE] 
    > Da Sie TypeScript verwenden, benötigen Sie für das Paket, das Sie hinzufügen, Eingaben. Dies ist wichtig, wenn Sie Code schreiben, da TypeScript nur eine Obermenge von JavaScript ist. Der gesamte TypeScript-Code wird beim Kompilieren nach wie vor in JavaScript-Code konvertiert. Sie können mithilfe von **npm** nach Eingaben suchen, beispielsweise: `npm install @types/{package} --save`

3. Erstellen Sie im Ordner Ihres Webparts eine Datei mit dem Namen `validator.d.ts`, und fügen Sie den nachfolgenden Code in die Datei ein:

    ```typescript
    declare module "validator" {
        export function isEmail(email: string): boolean;
        export function isAscii(text: string): boolean;
    }
    ```

    > [!NOTE] 
    > Manche Bibliotheken verfügen nicht über Eingaben. Die validator-Bibliothek verfügt zwar über eine [von der Community bereitgestellte Eingabendatei](https://www.npmjs.com/package/@types/validator), in diesem Szenario wird aber davon ausgegangen, dass dies nicht der Fall ist. In diesem Fall müssen Sie Ihre eigene `.d.ts`-Datei für die Eingabedefinition für die Bibliothek definieren. Im vorherigen Code ist ein Beispiel dargestellt:

4. Importieren Sie die Eingaben in Ihre Webpartdatei:

    ```typescript
    import * as validator from 'validator';
    ```

5. Verwenden Sie die validator-Bibliothek im Webpartcode:

    ```typescript
    validator.isEmail('someone@example.com');
    ```

## <a name="share-a-library-among-multiple-web-parts"></a>Freigeben einer Bibliothek zwischen mehreren Webparts

Ihre clientseitige Lösung umfasst möglicherweise mehrere Webparts. Diese Webparts müssen möglicherweise die gleiche Bibliothek importieren oder freigeben. In solchen Fällen sollten Sie die Bibliothek in eine separate JavaScript-Datei einschließen, anstatt sie zu bündeln, um Leistung und Zwischenspeicherung zu verbessern. Dies gilt besonders für größere Bibliotheken.

### <a name="example"></a>Beispiel

In diesem Beispiel geben Sie das [marked](https://www.npmjs.com/package/marked)-Paket - einen Markdown-Compiler - in einem separaten Bundle frei.

1. Herunterladen des **marked**-Pakets von npm:

    ```sh
    npm install marked --save
    ```

2. Herunterladen der Eingaben:

    ```sh
    npm install @types/marked --save
    ```

3. Bearbeiten Sie **config/config.json**, und fügen Sie einen Eintrag zur Zuordnung **externals** hinzu. Dadurch wird dem Bundler mitgeteilt, dies in einer separaten Datei zu platzieren. Dadurch wird verhindert, dass der Bundler diese Bibliothek bündelt:

    ```json
    "marked": "node_modules/marked/marked.min.js"
    ```

4. Fügen Sie die Anweisung zum Importieren der `marked`-Bibliothek nun in das Webpart ein, nachdem Sie das Paket und die Eingaben für die Bibliothek hinzugefügt haben:

    ```typescript
    import * as marked from 'marked';
    ```

5. Verwenden der Bibliothek im Webpart:

    ```typescript
    console.log(marked('I am using __markdown__.'));
    ```

## <a name="load-a-script-from-a-cdn"></a>Laden eines Skripts aus einem CDN

Anstatt die Bibliothek aus einem npm-Paket zu laden, können Sie ein Skript aus einem Content Delivery Network (CDN) laden. Bearbeiten Sie hierzu die **config.json**-Datei, um die Bibliothek von ihrer CDN-URL zu laden.

### <a name="example"></a>Beispiel

In diesem Beispiel laden Sie jQuery aus einem CDN. Sie müssen nicht das npm-Paket installieren. Sie müssen jedoch die Eingaben installieren.

1. Installieren der Eingaben für jQuery:

    ```sh
    npm install --save @types/jquery
    ```

2. Aktualisieren Sie `config.json` im Ordner `config`, um jQuery aus einem CDN zu laden. Hinzufügen eines Eintrags zum `externals`-Feld:

    ```json
    "jquery": "https://code.jquery.com/jquery-3.1.0.min.js"
    ```

3. Importieren von jQuery in das Webpart:

    ```typescript
    import * as $ from 'jquery';
    ```

4. Verwenden von jQuery im Webpart:

    ```javascript
    alert( $('#foo').val() );
    ```

## <a name="load-a-non-amd-module"></a>Laden eines Nicht-AMD-Moduls

Einige Skripts folgen dem veralteten JavaScript-Muster des Speicherns der Bibliothek im globalen Namespace. Dieses Muster wurde nun durch [Universal Modul Definitions (UMD)](https://github.com/umdjs/umd),  / [Asynchronous Module Definitions (AMD)](https://en.wikipedia.org/wiki/Asynchronous_module_definition) oder [ES6-Module](https://github.com/lukehoban/es6features/blob/master/README.md#modules) ersetzt. Möglicherweise müssen Sie solche Bibliotheken jedoch in das Webpart laden.

> [!TIP] 
> Es ist schwierig, manuell ermitteln, ob das Skript, das Sie laden möchten, ein AMD- oder ein Nicht-AMD-Skript ist. Dies ist insbesondere dann der Fall, wenn das Skript minimiert ist. Wenn das Skript auf einer öffentlich zugänglichen URL gehostet wird, können Sie das kostenlose Tool [Rencore SharePoint Framework Script Check](https://rencore.com/sharepoint-framework/script-check/) verwenden, um die Art des Skripts zu ermitteln. Dieses Tool teilt Ihnen außerdem mit, ob der Hostingspeicherort, vom dem aus Sie das Skript laden, korrekt konfiguriert ist.

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

<br/>

1. Erstellen von Eingaben für das Skript in einer Datei mit dem Namen **contoso.d.ts** im Webpartordner.

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

2. Aktualisieren der **config.json**-Datei derart, dass dieses Skript eingeschlossen wird. Hinzufügen eines Eintrags zur **externals**-Zuordnung:

    ```json
    {
        "contoso": {
            "path": "https://contoso.com/contoso.js",
            "globalName": "ContosoJS"
        }
    }
    ```

3. Hinzufügen eines Imports zum Webpartcode:

    ```typescript
    import contoso from 'contoso';
    ```

4. Verwenden der Contoso-Bibliothek im Code:

    ```typescript
    contoso.sayHello(username);
    ```

## <a name="load-a-library-that-has-a-dependency-on-another-library"></a>Laden einer Bibliothek, die eine Abhängigkeit von einer anderen Bibliothek aufweist

Viele Bibliotheken weisen Abhängigkeiten von einer anderen Bibliothek auf. Sie können solche Abhängigkeiten in der **config.json**-Datei mithilfe der **globalDependencies**-Eigenschaft angeben.

> [!IMPORTANT] 
> Beachten Sie, dass Sie dieses Feld für AMD-Module nicht angeben müssen; diese importieren sich gegenseitig ordnungsgemäß. Ein Nicht-AMD-Modul kann jedoch kein AMD-Modul als Abhängigkeit aufweisen. In einigen Fällen ist es möglich, ein AMD-Skript als Nicht-AMD-Skript zu laden. Dies ist häufig bei der Arbeit mit jQuery (selbst ein AMD-Skript) und jQuery-Plug-Ins erforderlich, die meistens als Nicht-AMD-Skripts verteilt werden und von jQuery abhängig sind.

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

<br/>

1. Fügen Sie Eingaben für diese Klasse hinzu, oder erstellen Sie sie. In diesem Fall erstellen Sie `Contoso.d.ts` mit Eingaben für beide JavaScript-Dateien.

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

2. Aktualisieren Sie die **config.json**-Datei. Hinzufügen von zwei Einträgen zu **externals**:

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

3. Hinzufügen von Importen für Contoso und ContosoUI:

    ```typescript
    import contoso = require('contoso');
    require('contoso-ui');
    ```

4. Verwenden der Bibliotheken im Code:

    ```typescript
    contoso.EventList.alert();
    ```

## <a name="load-sharepoint-jsom"></a>Laden von SharePoint JSOM

Das Laden von SharePoint JSOM ist im Wesentlichen das gleiche Szenario wie das Laden von Nicht-AMD-Skripts, die Abhängigkeiten haben. Hierfür wird sowohl die Option **globalName** als auch die Option **globalDependency** verwendet.

> [!IMPORTANT] 
> Beachten Sie, dass der folgende Ansatz auf klassischen SharePoint-Seiten Fehler verursacht, auf denen SharePoint JSOM bereits geladen ist. Wenn Ihr Webpart sowohl mit klassischen als auch mit modernen Seiten arbeiten soll, sollten Sie zuerst überprüfen, ob SharePoint JSOM bereits verfügbar ist. Ist dies nicht der fall, laden Sie es dynamisch mithilfe von **SPComponentLoader**.

<br/>

1. Installieren von Eingaben für Microsoft Ajax (Abhängigkeit für JSOM-Eingaben):

    ```sh
    npm install @types/microsoft-ajax --save
    ```

2. Installieren von Eingaben für JSOM:

    ```sh
    npm install @types/sharepoint --save
    ```

3. Hinzufügen von Einträgen zu `config.json`:

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

4. Fügen Sie in Ihrem Webpart die `require`-Anweisungen hinzu:

    ```typescript
    require('sp-init');
    require('microsoft-ajax');
    require('sp-runtime');
    require('sharepoint');
    ```

## <a name="load-localized-resources"></a>Laden lokalisierter Ressourcen

Sie können eine Zuordnung in **config.json** mit dem Namen **localizedResources** verwenden, um zu beschreiben, wie lokalisierte Ressourcen geladen werden. Pfade in dieser Zuordnung sind relativ zum **lib**-Ordner und dürfen keinen vorangestellten Schrägstrich (**/**) enthalten.

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

<br/>

1. Bearbeiten Sie die **config.json**-Datei. Fügen Sie einen Eintrag zu **localizedResources** hinzu. `{locale}` ist ein Platzhaltertoken für den Gebietsschemanamen:

    ```json
    {
        "strings": "strings/{locale}.js"
    }
    ```

2. Fügen Sie Eingaben für Ihre Zeichenfolgen hinzu. In diesem Fall haben Sie die Datei **MyStrings.d.ts**:

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

3. Hinzufügen von Importen für die Zeichenfolgen in Ihrem Projekt:

    ```typescript
    import * as strings from 'mystrings';
    ```

4. Verwenden der Zeichenfolgen in Ihrem Projekt:

    ```typescript
    alert(strings.initialPrompt);
    ```

## <a name="see-also"></a>Weitere Artikel

- [SharePoint Framework-Übersicht](../../sharepoint-framework-overview.md)