---
title: "Migrieren von jQuery- und DataTables-Lösungen, die mit Script Editor-Webpart erstellt wurden, in SharePoint Framework"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: a50a56f3b433d9152e047bd51525747abf9d2865
ms.sourcegitcommit: 9c458121628425716442abddbc97a1f61f18a74c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/20/2017
---
# <a name="migrate-jquery-and-datatables-solution-built-using-script-editor-web-part-to-sharepoint-framework"></a>Migrieren von jQuery- und DataTables-Lösungen, die mit Script Editor-Webpart erstellt wurden, in SharePoint Framework

Eines der am häufigsten verwendeten jQuery-Plug-Ins ist [DataTables](https://datatables.net/). Mit DataTables können Sie problemlos leistungsstarke Übersichten über die Daten erstellen, die aus SharePoint und externen APIs stammen. In diesem Artikel wird erläutert, wie Sie eine SharePoint-Anpassung mithilfe von DataTables, die mit dem Script Editor-Webpart erstellt wurden, in das SharePoint-Framework migrieren.

## <a name="list-of-it-requests-built-using-the-script-editor-web-part"></a>Liste der IT-Anfragen, die mit dem Script Editor-Webpart erstellt wurde

Um das Verfahren der Migration einer SharePoint-Anpassung in das SharePoint-Framework mithilfe von DataTables zu veranschaulichen, verwenden Sie die folgende Lösung, die einen Überblick über die IT-Supportanfragen zeigt, die aus einer SharePoint-Liste abgerufen wurden.

![Übersicht über die IT-Supportanfragen, angezeigt auf einer SharePoint-Seite](../../../images/datatables-sewp.png)

Die Lösung wird anhand des standardmäßigen Script Editor-Webparts von SharePoint erstellt. Nachfolgend ist der in der Anpassung verwendete Code aufgeführt.

```html
<script src="https://code.jquery.com/jquery-1.12.4.js"></script>
<script src="https://cdn.datatables.net/1.10.15/js/jquery.dataTables.js"></script>
<script src="https://momentjs.com/downloads/moment.min.js"></script>
<link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.15/css/jquery.dataTables.min.css" />
<table id="requests" class="display" cellspacing="0" width="100%">
    <thead>
        <tr>
            <th>ID</th>
            <th>Business unit</th>
            <th>Category</th>
            <th>Status</th>
            <th>Due date</th>
            <th>Assigned to</th>
        </tr>
    </thead>
</table>
<script>
// UMD
(function(factory) {
    "use strict";

    if (typeof define === 'function' && define.amd) {
        // AMD
        define(['jquery'], function ($) {
            return factory( $, window, document );
        });
    }
    else if (typeof exports === 'object') {
        // CommonJS
        module.exports = function (root, $) {
            if (!root) {
                root = window;
            }

            if (!$) {
                $ = typeof window !== 'undefined' ?
                    require('jquery') :
                    require('jquery')( root );
            }

            return factory($, root, root.document);
        };
    }
    else {
        // Browser
        factory(jQuery, window, document);
    }
}
(function($, window, document) {
    $.fn.dataTable.render.moment = function (from, to, locale) {
        // Argument shifting
        if (arguments.length === 1) {
            locale = 'en';
            to = from;
            from = 'YYYY-MM-DD';
        }
        else if (arguments.length === 2) {
            locale = 'en';
        }

        return function (d, type, row) {
            var m = window.moment(d, from, locale, true);

            // Order and type get a number value from Moment, everything else
            // sees the rendered value
            return m.format(type === 'sort' || type === 'type' ? 'x' : to);
        };
    };
}));
</script>
<script>
$(document).ready(function() {
    $('#requests').DataTable({
        'ajax': {
        'url': "../_api/web/lists/getbytitle('IT Requests')/items?$select=ID,BusinessUnit,Category,Status,DueDate,AssignedTo/Title&$expand=AssignedTo/Title",
        'headers': { 'Accept': 'application/json;odata=nometadata' },
        'dataSrc': function(data) {
            return data.value.map(function(item) {
                return [
                    item.ID,
                    item.BusinessUnit,
                    item.Category,
                    item.Status,
                    new Date(item.DueDate),
                    item.AssignedTo.Title
                ];
            });
        }
    },
    columnDefs: [{
        targets: 4,
        render: $.fn.dataTable.render.moment('YYYY/MM/DD')
    }]
    });
});
</script>
```

Die Anpassung lädt zunächst die von ihr verwendeten Bibliotheken: jQuery, DataTables und Moment.js (Zeilen 1 bis 4). Als Nächstes gibt sie die Struktur der Tabelle an, die zum Darstellen der Daten verwendet wird (Zeilen 5 bis 16). Nach dem Erstellen der Tabelle umschließt sie Moment.js in einem DataTables-Plug-In, damit die in der Tabelle aufgeführten Datumsangaben formatiert werden können (erster Skriptblock in den Zeilen 17 bis 70). Schließlich verwendet die Anpassung DataTables zum Laden und Darstellen der Liste von IT-Supportanfragen. Die Daten werden mit AJAX aus einer SharePoint-Liste geladen (Zeilen 71 bis 96).

Durch die Verwendung von DataTables erhalten Endbenutzer eine leistungsfähige Lösung, mit der sie die Ergebnisse auf einfache Weise filtern, sortieren und darin blättern können, ohne dass weitere Entwicklungsschritte erforderlich sind.

![Die Liste der IT-Supportanfragen, angezeigt mit DataTables und gefiltert nach Anfragen, die Lidia zugeordnet sind, sowie in absteigender Reihenfolge nach Fälligkeitsdatum sortiert](../../../images/datatables-sewp-filter.png)

## <a name="migrate-the-it-requests-overview-solution-from-the-script-editor-web-part-to-the-sharepoint-framework"></a>Migrieren der Übersichtslösung für IT-Anfragen vom Script Editor-Webpart in das SharePoint-Framework

> **Hinweis:** Bevor Sie die Schritte in diesem Artikel durchführen, müssen Sie [eine Entwicklungsumgebung einrichten](../../set-up-your-development-environment.md), in der Sie SharePoint Framework-Lösungen erstellen können.

Das Umwandeln dieser Anpassung in das SharePoint-Framework bietet eine Reihe von Vorteilen, wie z. B. eine benutzerfreundlichere Konfiguration und die zentrale Verwaltung der Lösung. Es folgt eine Schritt-für-Schritt-Beschreibung dazu, wie Sie die Lösung in das SharePoint-Framework migrieren können. Sie migrieren die Lösung zunächst in das SharePoint-Framework, wobei so wenige Änderungen am ursprünglichen Code wie möglich vorgenommen werden. Später transformieren Sie den Code der Lösung in TypeScript, um die Sicherheitsfeatures nutzen zu können, die es während der Entwicklung bietet.

> Der Quellcode des Projekts in den verschiedenen Phasen der Migration steht unter [https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/tutorials/tutorial-migrate-datatables](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/tutorials/tutorial-migrate-datatables) zur Verfügung.

### <a name="create-new-sharepoint-framework-project"></a>Erstellen eines neuen SharePoint Framework-Projekts

Erstellen Sie zunächst einen neuen Ordner für Ihr Projekt:

```sh
md datatables-itrequests
```

Navigieren Sie zum Projektordner:

```sh
cd datatables-itrequests
```

Führen Sie im Projektordner den SharePoint Framework-Yeoman-Generator aus, um ein Gerüst für ein neues SharePoint Framework-Projekt zu erstellen:

```sh
yo @microsoft/sharepoint
```

Es werden mehrere Eingabeaufforderungen angezeigt. Definieren Sie die Werte jeweils wie folgt:
- **datatables-itrequests** als Name der Lösung
- **Aktuellen Ordner verwenden** als Speicherort für die Dateien
- **No javaScript web framework** als Eintrittspunkt für die Webpart-Erstellung
- **IT-Anfragen** als Name des Webparts
- **Übersicht über die IT-Supportanfragen** als Beschreibung für das Webpart

![SharePoint Framework-Yeoman-Generator mit den Standardoptionen](../../../images/datatables-yeoman.png)

Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:

```sh
npm shrinkwrap
```

Öffnen Sie dann den Projektordner im Code-Editor. In diesem Tutorial verwenden Sie Visual Studio Code.

![SharePoint Framework-Projekt in Visual Studio Code](../../../images/datatables-vscode.png)

### <a name="load-javascript-libraries"></a>Laden von JavaScript-Bibliotheken

Ähnlich wie bei der ursprünglichen Lösung, die mit dem Script Editor-Webpart erstellt wurde, müssen Sie zunächst die JavaScript-Bibliotheken laden, die von der Lösung benötigt werden. In SharePoint-Framework umfasst dies in der Regel zwei Schritte: die Angabe der URL, über die die Bibliothek geladen werden soll, und ein Verweis auf die Bibliothek im Code.

Beginnen Sie, indem Sie die URLs angeben, über die die Bibliotheken geladen werden sollen. Öffnen Sie im Code-Editor die Datei **./config/config.json**, und ändern Sie den Abschnitt **externals** wie folgt:

```json
{
  "externals": {
    "jquery": "https://code.jquery.com/jquery-1.12.4.min.js",
    "datatables.net": "https://cdn.datatables.net/1.10.15/js/jquery.dataTables.min.js",
    "moment": "https://momentjs.com/downloads/moment.min.js"
  }
}
```

Öffnen Sie als Nächstes die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und fügen Sie nach der letzten **import**-Anweisung Folgendes hinzu:

```ts
import 'jquery';
import 'datatables.net';
import 'moment';
```

### <a name="define-data-table"></a>Definieren einer Datentabelle

Genau wie bei der ursprünglichen Lösung müssen Sie im nächsten Schritt die Struktur der Tabelle definieren, die zum Anzeigen der Daten verwendet wird. Öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und ändern Sie die **render**-Methode in:

```ts
export default class ItRequestsWebPart extends BaseClientSideWebPart<IItRequestsWebPartProps> {
  public render(): void {
    this.domElement.innerHTML = `
      <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.15/css/jquery.dataTables.min.css" />
      <table id="requests" class="display ${styles.helloWorld}" cellspacing="0" width="100%">
        <thead>
            <tr>
                <th>ID</th>
                <th>Business unit</th>
                <th>Category</th>
                <th>Status</th>
                <th>Due date</th>
                <th>Assigned to</th>
            </tr>
        </thead>
      </table>`;
  }
  // ...
}
```

### <a name="register-momentjs-plugin-for-datatables"></a>Registrieren des Moment.js-Plug-Ins für DataTables

Im nächsten Schritt definieren Sie das Moment.js-Plug-In für DataTables so, dass die Datumsangaben in der Tabelle formatiert werden können. Erstellen Sie im Ordner **./src/webparts/itRequests** eine neue Datei namens **moment-plugin.js**, und fügen Sie den folgenden Code ein:

```js
// UMD
(function (factory) {
    "use strict";

    if (typeof define === 'function' && define.amd) {
        // AMD
        define(['jquery'], function ($) {
            return factory($, window, document);
        });
    }
    else if (typeof exports === 'object') {
        // CommonJS
        module.exports = function (root, $) {
            if (!root) {
                root = window;
            }

            if (!$) {
                $ = typeof window !== 'undefined' ?
                    require('jquery') :
                    require('jquery')(root);
            }

            return factory($, root, root.document);
        };
    }
    else {
        // Browser
        factory(jQuery, window, document);
    }
}

(function ($, window, document) {
    $.fn.dataTable.render.moment = function (from, to, locale) {
        // Argument shifting
        if (arguments.length === 1) {
            locale = 'en';
            to = from;
            from = 'YYYY-MM-DD';
        }
        else if (arguments.length === 2) {
            locale = 'en';
        }

        return function (d, type, row) {
            var moment = require('moment');
            var m = moment(d, from, locale, true);

            // Order and type get a number value from Moment, everything else
            // sees the rendered value
            return m.format(type === 'sort' || type === 'type' ? 'x' : to);
        };
    };
}));
```

Damit das Webpart das Plug-In lädt, muss es die neu erstellte Datei **moment-plugin.js** referenzieren. Öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und fügen Sie nach der letzten **import**-Anweisung Folgendes ein:

```ts
import './moment-plugin';
```

> **Hinweis:** Sie müssen beim Referenzieren von anderen Dateien die Erweiterung **js** nicht einbeziehen. SharePoint-Framework löst die Erweiterung automatisch auf.

### <a name="initiate-datatables-and-load-data"></a>Initiieren von DataTables und laden der Daten

Der letzte Schritt besteht darin, den Code einzubeziehen, der die Datentabelle initiiert und die Daten aus SharePoint lädt. Erstellen Sie im Ordner **./src/webparts/itRequests** eine neue Datei namens **script.js**, und fügen Sie den folgenden Code ein:

```js
$(document).ready(function () {
    $('#requests').DataTable({
        'ajax': {
            'url': "../../_api/web/lists/getbytitle('IT Requests')/items?$select=ID,BusinessUnit,Category,Status,DueDate,AssignedTo/Title&$expand=AssignedTo/Title",
            'headers': { 'Accept': 'application/json;odata=nometadata' },
            'dataSrc': function (data) {
                return data.value.map(function (item) {
                    return [
                        item.ID,
                        item.BusinessUnit,
                        item.Category,
                        item.Status,
                        new Date(item.DueDate),
                        item.AssignedTo.Title
                    ];
                });
            }
        },
        columnDefs: [{
            targets: 4,
            render: $.fn.dataTable.render.moment('YYYY/MM/DD')
        }]
    });
});
```

Um diese Datei im Webpart zu referenzieren, öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und ändern Sie die **render**-Methode in:

```ts
export default class ItRequestsWebPart extends BaseClientSideWebPart<IItRequestsWebPartProps> {
  public render(): void {
    this.domElement.innerHTML = `
      <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.15/css/jquery.dataTables.min.css" />
      <table id="requests" class="display ${styles.helloWorld}" cellspacing="0" width="100%">
        <thead>
            <tr>
                <th>ID</th>
                <th>Business unit</th>
                <th>Category</th>
                <th>Status</th>
                <th>Due date</th>
                <th>Assigned to</th>
            </tr>
        </thead>
      </table>`;

      require('./script');
  }
  // ...
}
```

Überprüfen Sie, ob das Webpart wie erwartet funktioniert, indem Sie in der Befehlszeile Folgendes ausführen:

```sh
gulp serve --nobrowser
```

Da das Webpart die Daten aus SharePoint lädt, müssen Sie das Webpart mit der gehosteten SharePoint Framework-Arbeitsfläche testen. Navigieren Sie zu **https://yourtenant.sharepoint.com/_layouts/workbench.aspx**, und fügen Sie das Webpart zum Canvas hinzu. Die IT-Anfragen sollten nun mit dem jQuery-Plug-In von DataTables angezeigt werden.

![IT-Anfragen, dargestellt in einem clientseitigen Webpart des SharePoint-Framework](../../../images/datatables-spfx.png)

## <a name="add-support-for-configuring-the-web-part-through-web-part-properties"></a>Hinzufügen von Unterstützung zum Konfigurieren des Webparts über Webpart-Eigenschaften

In den vorherigen Schritten haben Sie die IT-Anfragenlösung aus dem Script Editor-Webpart in das SharePoint-Framework migriert. Obwohl die Lösung bereits wie erwartet funktioniert, nutzt sie keine der Vorteile des SharePoint-Framework. Der Name der Liste, aus der die IT-Anfragen geladen werden, isst im Code enthalten, und der Code selbst ist einfaches JavaScript, das schwerer umgestaltet werden kann als TypeScript. Die folgenden Schritte veranschaulichen, wie Sie die vorhandene Lösung erweitern können, um Benutzern zu ermöglichen, den Namen der Liste anzugeben, aus der Daten geladen werden sollen. Später wandeln Sie den Code in TypeScript um, um seine Typsicherheitfeatures nutzen zu können.

### <a name="define-web-part-property-for-storing-the-name-of-the-list"></a>Definieren der Webparteigenschaft zum Speichern des Listennamens

Beginnen Sie mit der Definition einer Webparteigenschaft, um den Namen der Liste zu speichern, aus der IT-Anfragen geladen werden sollen. Öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/ItRequestsWebPart.manifest.json**, benennen Sie die standardmäßige **description**-Eigenschaft in **listName** um, und löschen Sie den Wert.

![Die listName-Eigenschaft im Webpartmanifest, hervorgehoben im Visual Studio-Code](../../../images/datatables-spfx-listname-property.png)

Aktualisieren Sie als Nächstes die Oberfläche der Webparteigenschaften, um die Änderungen im Manifest zu übernehmen. Öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/IItRequestsWebPartProps.ts**, und ändern Sie den Inhalt in:

```ts
export interface IItRequestsWebPartProps {
  listName: string;
}
```

Aktualisieren Sie dann die Anzeigebeschriftungen für die Eigenschaft **listName**. Öffnen Sie die Datei **./src/webparts/itRequests/loc/mystrings.d.ts**, und ändern Sie den Inhalt in:

```ts
declare interface IItRequestsStrings {
  PropertyPaneDescription: string;
  BasicGroupName: string;
  ListNameFieldLabel: string;
}

declare module 'itRequestsStrings' {
  const strings: IItRequestsStrings;
  export = strings;
}
```

Öffnen Sie als Nächstes die Datei **./src/webparts/itRequests/loc/en-us.js**, und ändern Sie den Inhalt in:

```js
define([], function() {
  return {
    "PropertyPaneDescription": "IT Requests settings",
    "BasicGroupName": "Data",
    "ListNameFieldLabel": "List name"
  }
});
```

Aktualisieren Sie zum Schluss das Webpart, damit es die neu definierte Eigenschaft verwendet. Öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und ändern Sie die **getPropertyPaneConfiguration**-Methode in:

```ts
export default class ItRequestsWebPart extends BaseClientSideWebPart<IItRequestsWebPartProps> {
  // ...
  protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
    return {
      pages: [
        {
          header: {
            description: strings.PropertyPaneDescription
          },
          groups: [
            {
              groupName: strings.BasicGroupName,
              groupFields: [
                PropertyPaneTextField('listName', {
                  label: strings.ListNameFieldLabel
                })
              ]
            }
          ]
        }
      ]
    };
  }

  protected get disableReactivePropertyChanges(): boolean {
    return true;
  }
}
```

Um zu verhindern, dass das Webpart neu geladen wird, wenn Benutzer den Namen der Liste eingeben, haben Sie das Webpart darüber hinaus so konfiguriert, dass es den nicht reaktiven Eigenschaftenbereich verwendet, indem Sie die **disableReactivePropertyChanges**-Methode hinzugefügt und den Rückgabewert auf **true** festgelegt haben.

### <a name="use-the-configured-name-of-the-list-to-load-the-data-from"></a>Verwenden des Namens der konfigurierten Liste, aus der Daten geladen werden

Anfangs war der Name der Liste, aus der die Daten geladen werden sollen, in die REST-Abfrage eingebettet. Nun, da Benutzer diesen Namen konfigurieren können, sollte der konfigurierte Wert in die REST-Abfrage eingefügt werden, bevor die Daten geladen werden. Die einfachste Möglichkeit, dies zu tun, besteht darin, den Inhalt der Datei **script.js** in die Haupt-Webpartdatei zu verschieben.

Öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und ändern Sie die **render**-Methode in:

```ts
var $: any = (window as any).$;

export default class ItRequestsWebPart extends BaseClientSideWebPart<IItRequestsWebPartProps> {
  public render(): void {
    this.domElement.innerHTML = `
      <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.15/css/jquery.dataTables.min.css" />
      <table class="display ${styles.helloWorld}" cellspacing="0" width="100%">
        <thead>
            <tr>
                <th>ID</th>
                <th>Business unit</th>
                <th>Category</th>
                <th>Status</th>
                <th>Due date</th>
                <th>Assigned to</th>
            </tr>
        </thead>
      </table>`;

    $(document).ready(() => {
      $('table', this.domElement).DataTable({
        'ajax': {
          'url': `../../_api/web/lists/getbytitle('${escape(this.properties.listName)}')/items?$select=ID,BusinessUnit,Category,Status,DueDate,AssignedTo/Title&$expand=AssignedTo/Title`,
          'headers': { 'Accept': 'application/json;odata=nometadata' },
          'dataSrc': function (data) {
            return data.value.map(function (item) {
              return [
                item.ID,
                item.BusinessUnit,
                item.Category,
                item.Status,
                new Date(item.DueDate),
                item.AssignedTo.Title
              ];
            });
          }
        },
        columnDefs: [{
          targets: 4,
          render: $.fn.dataTable.render.moment('YYYY/MM/DD')
        }]
      });
    });
  }

  // ...
}
```

Anstatt den Code aus der Datei **script.js** zu referenzieren, ist der gesamte Inhalt Teil der **render**-Methode des Webparts. In der REST-Abfrage können Sie nun in Zeile 40 den festen Namen der Liste durch den Wert der Eigenschaft **listName** ersetzen, der den Namen der Liste wie vom Benutzer konfiguriert enthält. Vor der Verwendung des Werts wird dieser mit der **escape**-Funktion von lodash auskommentiert, um eine Skripteinschleusung zu verhindern.

Zu diesem Zeitpunkt ist immer noch der größte Teil des Codes in einfachem JavaScript geschrieben. Um Buildprobleme mit der **$** jQuery-Variablen zu vermeiden, mussten Sie diese als Typ**any** in Zeile 18 definieren. Wenn Sie den Code später in TypeScript transformieren, ersetzen Sie dies durch eine geeignete Typdefinition.

Da Sie den Inhalt der Datei **script.js** gerade in die Haupt-Webpartdatei verschoben haben, ist **script.js** nicht mehr erforderlich, und Sie können die Datei aus dem Projekt löschen.

Um zu überprüfen, ob das Webpart wie erwartet funktioniert, führen Sie Folgendes in der Befehlszeile aus:

```sh
gulp serve --nobrowser
```

Navigieren Sie zu der gehosteten Workbench, und fügen Sie das Webpart zum Canvas hinzu. Öffnen Sie den Eigenschaftenbereich des Webparts, geben Sie den Namen der Liste mit IT-Anfragen an, und klicken Sie auf die Schaltfläche **Übernehmen**, um die Änderungen zu bestätigen. Sie sollten nun die im Webpart angezeigten IT-Anfragen sehen.

![IT-Anfragen, geladen aus der konfigurierten Liste und angezeigt im clientseitigen Webpart des SharePoint-Framework](../../../images/datatables-spfx-list-configured.png)

## <a name="transform-the-plain-javascript-code-to-typescript"></a>Transformieren des einfachen JavaScript-Codes in TypeScript

Die Verwendung von TypeScript anstatt von JavaScript bietet eine Reihe von Vorteilen. TypeScript ist nicht nur einfacher zu verwalten und umzugestalten, sondern ermöglicht auch, Fehler früher abzufangen. Die nachfolgenden Schritte beschreiben, wie Sie den ursprünglichen JavaScript-Code in TypeScript transformieren.

### <a name="add-type-definitions-for-used-libraries"></a>Hinzufügen von Typdefinitionen für verwendete Bibliotheken

Um ordnungsgemäß zu funktionieren, erfordert TypeScript Typdefinitionen für die verschiedenen Bibliotheken, die im Projekt verwendet werden. Typdefinitionen werden häufig als npm-Pakete im @types-Namespace bereitgestellt.

Beginnen Sie, indem Sie die Typdefinitionen für jQuery und DataTables installieren, indem Sie in der Befehlszeile Folgendes ausführen:

```sh
npm install --save-dev @types/jquery @types/jquery.datatables
```

Typdefinitionen für Moment.js werden zusammen mit dem Moment.js-Paket bereitgestellt. Obwohl Sie Moment.js über eine URL laden, müssen das Moment.js-Paket trotzdem noch im Projekt installieren, um ihre Eingaben verwenden zu können.

Installieren Sie das Moment.js-Paket, indem Sie in der Befehlszeile Folgendes ausführen:

```sh
npm install --save moment
```

### <a name="update-package-references"></a>Aktualisieren von Paketverweisen

Um Typen der installierten Typdefinitionen verwenden zu können, müssen Sie die Verweismethode auf die Bibliotheken ändern. Öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und ändern Sie die `import 'jquery';`-Anweisung in:

```ts
import * as $ from 'jquery';
```

Da Sie **$** als jQuery definiert haben, können Sie nun die lokale Definition von **$** entfernen, die Sie zuvor hinzugefügt hatten:

```ts
var $: any = (window as any).$;
```

Da DataTables ein jQuery-Plug-In ist, das sich selbst an jQuery anfügt, können Sie die Typdefinition nicht direkt laden. Stattdessen müssen Sie sie zur Liste der global geladenen Typen hinzufügen. Öffnen Sie im Code-Editor die Datei **./tsconfig.json**, und fügen Sie zum Array **types** **jquery.datatables** hinzu:

```json
{
  "compilerOptions": {
    "target": "es5",
    "forceConsistentCasingInFileNames": true,
    "module": "commonjs",
    "jsx": "react",
    "declaration": true,
    "sourceMap": true,
    "types": [
      "es6-promise",
      "es6-collections",
      "jquery.datatables",
      "webpack-env"
    ]
  }
}
```

### <a name="update-main-web-part-files-to-typescript"></a>Aktualisieren der Haupt-Webpartdatei in TypeScript

Da jetzt die Typdefinitionen für alle im Projekt installierten Bibliotheken vorhanden sind, können Sie beginnen mit dem Transformieren des einfachen JavaScript-Codes in TypeScript beginnen.

Beginnen Sie mit der Definition einer Oberfläche für die IT-Anfrageinformationen, die Sie aus der SharePoint-Liste abrufen. Öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und fügen Sie direkt oberhalb der Webpartklasse den folgende Codeausschnitt ein:

```ts
interface IRequestItem {
  ID: number;
  BusinessUnit: string;
  Category: string;
  Status: string;
  DueDate: string;
  AssignedTo: { Title: string; };
}
```

Ändern Sie im nächsten Schritt die **render**-Methode in:

```ts
export default class ItRequestsWebPart extends BaseClientSideWebPart<IItRequestsWebPartProps> {
  public render(): void {
    this.domElement.innerHTML = `
      <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.15/css/jquery.dataTables.min.css" />
      <table class="display ${styles.helloWorld}" cellspacing="0" width="100%">
        <thead>
            <tr>
                <th>ID</th>
                <th>Business unit</th>
                <th>Category</th>
                <th>Status</th>
                <th>Due date</th>
                <th>Assigned to</th>
            </tr>
        </thead>
      </table>`;

    $('table', this.domElement).DataTable({
      'ajax': {
        'url': `../../_api/web/lists/getbytitle('${escape(this.properties.listName)}')/items?$select=ID,BusinessUnit,Category,Status,DueDate,AssignedTo/Title&$expand=AssignedTo/Title`,
        'headers': { 'Accept': 'application/json;odata=nometadata' },
        'dataSrc': (data: { value: IRequestItem[] }): any[][] => {
          return data.value.map((item: IRequestItem): any[] => {
            return [
              item.ID,
              item.BusinessUnit,
              item.Category,
              item.Status,
              new Date(item.DueDate),
              item.AssignedTo.Title
            ];
          });
        }
      },
      columnDefs: [{
        targets: 4,
        render: $.fn.dataTable.render.moment('YYYY/MM/DD')
      }]
    });
  }

  // ...
}
```

Beachten Sie, wie nun die AJAX-Anforderung zum Abrufen der Daten aus der SharePoint-Liste eingegeben wird und Sie dabei unterstützt sicherzustellen, dass Sie sich beim Übergeben der Eigenschaften in ein Array an DataTables auf die richtigen Eigenschaften beziehen. Die Datenstruktur, mit der DataTables eine Tabellenzeile darstellt, ist ein Array von gemischten Typen; daher wurde es der Einfachheit halber als **any[]**. Die Verwendung des Typs **any** in diesem Kontext ist nicht schlecht, da die in der Eigenschaft **dataSrc** zurückgegebenen Daten intern von DataTables verwendet werden.

Beim Aktualisieren der **render**-Methode haben Sie darüber hinaus zwei weitere Änderungen vorgenommen. Sie haben erstens das **id**-Attribut aus der Tabelle entfernt. Dies ermöglicht Ihnen, mehrere Instanzen des gleichen Webparts auf der Seite zu platzieren. Außerdem haben Sie den Verweise auf die Funktion `$(document).ready()` entfernt, die nicht notwendig ist, da das DOM des Elements, in dem die Datentabelle gerendert wird, vor dem Initialisierungscode von DataTables festgelegt wird.

### <a name="update-the-momentjs-datatables-plugin-to-typescript"></a>Aktualisieren des Moment.js-DataTables-Plug-Ins in TypeScript

Der letzte Teil der Lösung, der in TypeScript umgewandelt werden muss, ist das Moment.js-DataTable-Plug-In. Benennen Sie zunächst die Datei **./src/webparts/itRequests/moment-plugin.js** in **./src/webparts/itRequests/moment-plugin.ts** um, damit sie vom TypeScript-Compiler verarbeitet wird. Öffnen Sie als Nächstes die Datei **moment-plugin.ts** im Code-Editor, und ersetzen Sie den Inhalt mit:

```ts
import * as $ from 'jquery';
import * as moment from 'moment';

/* tslint:disable:no-function-expression */
$.fn.dataTable.render.moment = function (from: string, to: string, locale: string): (d: any, type: string, row: any) => string {
/* tslint:enable */
    // Argument shifting
    if (arguments.length === 1) {
        locale = 'en';
        to = from;
        from = 'YYYY-MM-DD';
    }
    else if (arguments.length === 2) {
        locale = 'en';
    }

    return (d: any, type: string, row: any): string => {
        let m: moment.Moment = moment(d, from, locale, true);

        // Order and type get a number value from Moment, everything else
        // sees the rendered value
        return m.format(type === 'sort' || type === 'type' ? 'x' : to);
    };
};
```

Sie beginnen mit dem Laden von Verweisen auf jQuery und Moment.js, um TypeScript darüber zu informieren, worauf sich die entsprechenden Variablen beziehen. Als Nächstes definieren Sie die Plug-In-Funktion. In TypeScript verwenden Sie in der Regel die Pfeilnotation für Funktionen (`=>`). In diesem Fall jedoch, da Sie Zugriff auf die **arguments**-Eigenschaft benötigen, müssen Sie die reguläre Funktionsdefinition verwenden. Um zu verhindern, dass tslint Warnungen wegen der nicht verwendeten Pfeilnotation ausgibt, können Sie die Regel **no-function-expression** um die Funktionsdefinition explizit deaktivieren.

Führen Sie in der Befehlszeile Folgendes aus, um zu überprüfen, dass alles wie erwartet funktioniert:

```sh
gulp serve --nobrowser
```

Navigieren Sie zu der gehosteten Workbench, und fügen Sie das Webpart zum Canvas hinzu. Obwohl sich visuell nichts geändert hat, verwendet die neue Codebasis TypeScript und seine Typdefinitionen, um Sie bei der Verwaltung der Lösung zu unterstützen.
