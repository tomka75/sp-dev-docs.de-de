---
title: "Migrieren von jQuery- und DataTables-Lösungen, die mit Script Editor-Webpart erstellt wurden, in SharePoint Framework"
description: "Migrieren Sie eine SharePoint-Anpassung mithilfe von DataTables, um leistungsstarke Datenübersichten mit Daten zu erstellen, die von SharePoint und externen APIs stammen."
ms.date: 01/09/2018
ms.prod: sharepoint
ms.openlocfilehash: eae130d79f29e1bf29cd309895d0ebddd41ffc9b
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/05/2018
---
# <a name="migrate-jquery-and-datatables-solution-built-using-script-editor-web-part-to-sharepoint-framework"></a>Migrieren von jQuery- und DataTables-Lösungen, die mit Script Editor-Webpart erstellt wurden, in SharePoint Framework

Eines der häufig verwendeten jQuery-Plug-Ins ist [DataTables](https://datatables.net/). Mit Datentabellen können Sie ganz einfach leistungsstarke Datenübersichten mit Daten erstellen, die von SharePoint und externen APIs stammen.

## <a name="list-of-it-requests-built-using-the-script-editor-web-part"></a>Liste der IT-Anfragen, die mit dem Script Editor-Webpart erstellt wurde

Um das Verfahren der Migration einer SharePoint-Anpassung in das SharePoint-Framework mithilfe von DataTables zu veranschaulichen, verwenden Sie die folgende Lösung, die einen Überblick über die IT-Supportanfragen zeigt, die aus einer SharePoint-Liste abgerufen wurden.

![Übersicht über die IT-Supportanfragen, angezeigt auf einer SharePoint-Seite](../../../images/datatables-sewp.png)

<br/>

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

Die Anpassung lädt zuerst die verwendeten Bibliotheken: jQuery, DataTables und Moment.js (Zeilen 1-4). 

Als Nächstes wird die Struktur der Tabelle angegeben, die zum Darstellen der Daten verwendet wird (Zeilen 5-16). 

Nach dem Erstellen der Tabelle, wird Moment.js in einem DataTables-Plug-In umschlossen, sodass Datumsangaben, die in der Tabelle angezeigt werden, formatiert werden können (erster Skriptblock in den Zeilen 17-70). 

Schließlich verwendet die Anpassung DataTables zum Laden und Darstellen der Liste von IT-Supportanfragen. Die Daten werden mithilfe von AJAX aus einer SharePoint-Liste (Zeilen 71-96) geladen.

Durch die Verwendung von DataTables erhalten Endbenutzer eine leistungsfähige Lösung, mit der sie die Ergebnisse auf einfache Weise filtern, sortieren und darin blättern können, ohne dass weitere Entwicklungsschritte erforderlich sind.

![Die Liste der IT-Supportanfragen, angezeigt mit DataTables und gefiltert nach Anfragen, die Lidia zugeordnet sind, sowie in absteigender Reihenfolge nach Fälligkeitsdatum sortiert](../../../images/datatables-sewp-filter.png)

## <a name="migrate-the-it-requests-overview-solution-from-the-script-editor-web-part-to-the-sharepoint-framework"></a>Migrieren der Übersichtslösung für IT-Anfragen vom Script Editor-Webpart in das SharePoint-Framework

> [!NOTE] 
> Bevor Sie die Schritte in diesem Artikel durchführen, müssen Sie [eine Entwicklungsumgebung einrichten](../../set-up-your-development-environment.md), in der Sie SharePoint-Framework-Lösungen erstellen können.

Das Umwandeln dieser Anpassung in das SharePoint-Framework bietet eine Reihe von Vorteilen, wie z. B. eine benutzerfreundlichere Konfiguration und die zentrale Verwaltung der Lösung. Es folgt eine Schritt-für-Schritt-Beschreibung dazu, wie Sie die Lösung in das SharePoint-Framework migrieren können. Sie migrieren die Lösung zunächst in das SharePoint-Framework, wobei so wenige Änderungen am ursprünglichen Code wie möglich vorgenommen werden. Später transformieren Sie den Code der Lösung in TypeScript, um die Sicherheitsfeatures nutzen zu können, die es während der Entwicklung bietet.

> [!NOTE] 
> Der Quellcode des Projekts in den verschiedenen Phasen der Migration steht unter [Lernprogramm: Migrieren von jQuery- und DataTables-Lösungen, die mit Script Editor-Webpart erstellt wurden, in SharePoint Framework](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/tutorials/tutorial-migrate-datatables) zur Verfügung.

### <a name="create-new-sharepoint-framework-project"></a>Erstellen eines neuen SharePoint-Framework-Projekts

1. Erstellen Sie zunächst einen neuen Ordner für Ihr Projekt:

    ```sh
    md datatables-itrequests
    ```

2. Navigieren Sie zum Projektordner:

    ```sh
    cd datatables-itrequests
    ```

3. Führen Sie im Projektordner den SharePoint Framework-Yeoman-Generator aus, um ein Gerüst für ein neues SharePoint Framework-Projekt zu erstellen:

    ```sh
    yo @microsoft/sharepoint
    ```

4. Es werden mehrere Eingabeaufforderungen angezeigt. Definieren Sie die Werte jeweils wie folgt:

    - **datatables-itrequests** als Name der Lösung
    - **Aktuellen Ordner verwenden** als Speicherort für die Dateien
    - **No javaScript web framework** als Eintrittspunkt für die Webpart-Erstellung
    - **IT-Anfragen** als Name des Webparts
    - **Übersicht über die IT-Supportanfragen** als Beschreibung für das Webpart

    ![SharePoint-Framework-Yeoman-Generator mit den Standardoptionen](../../../images/datatables-yeoman.png)

5. Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:

    ```sh
    npm shrinkwrap
    ```

6. Öffnen Sie den Projektordner in einem Code-Editor. In diesem Tutorial verwenden Sie Visual Studio Code.

    ![SharePoint Framework-Projekt in Visual Studio Code](../../../images/datatables-vscode.png)

### <a name="load-javascript-libraries"></a>Laden von JavaScript-Bibliotheken

Ähnlich wie bei der ursprünglichen Lösung, die mit dem Skript-Editor-Webpart erstellt wurde, müssen Sie zunächst die JavaScript-Bibliotheken laden, die von der Lösung benötigt werden. In SharePoint-Framework umfasst dies in der Regel zwei Schritte: die Angabe der URL, über die die Bibliothek geladen werden soll, und ein Verweis auf die Bibliothek im Code.

1. Geben Sie die URLs an, über die die Bibliotheken geladen werden sollen. Öffnen Sie im Code-Editor die Datei **./config/config.json**, und ändern Sie den Abschnitt **externals** wie folgt:

    ```json
    {
    "externals": {
        "jquery": "https://code.jquery.com/jquery-1.12.4.min.js",
        "datatables.net": "https://cdn.datatables.net/1.10.15/js/jquery.dataTables.min.js",
        "moment": "https://momentjs.com/downloads/moment.min.js"
    }
    }
    ```

2. Öffnen Sie die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und fügen Sie nach der letzten **import**-Anweisung Folgendes hinzu:

    ```typescript
    import 'jquery';
    import 'datatables.net';
    import 'moment';
    ```

### <a name="define-data-table"></a>Definieren einer Datentabelle

Wie bei der ursprünglichen Lösung besteht der nächste Schritt darin, die Struktur der Tabelle zu definieren, die zum Anzeigen der Daten verwendet wird. 

Öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und ändern Sie die **render**-Methode in:

```typescript
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

Der nächste Schritt besteht darin, das Moment.js-Plug-In für DataTables zu definieren, damit Datumsangaben in der Tabelle formatiert werden können. 

1. Erstellen Sie im Ordner **./src/webparts/itRequests** eine neue Datei mit dem Namen **moment-plugin.js**, und fügen Sie den folgenden Code in die Datei ein:

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

2. Damit das Webpart das Plug-In lädt, muss es auf die neu erstellte Datei **plugin.js-Moment** verweisen. Öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und fügen Sie nach der letzten **import**-Anweisung Folgendes hinzu:

    ```typescript
    import './moment-plugin';
    ```

> [!NOTE] 
> Sie müssen nicht die Erweiterung **js** einschließen, wenn Sie auf andere Dateien verweisen. SharePoint Framework löst die Erweiterung automatisch für Sie.

### <a name="initiate-datatables-and-load-data"></a>Initiieren von DataTables und Laden der Daten

Der letzte Schritt besteht darin, den Code einzuschließen, der die Datentabelle initiiert und die Daten aus SharePoint lädt. 

1. Erstellen Sie im Ordner **./src/webparts/itRequests** eine neue Datei mit dem Namen **script.js**, und fügen Sie den folgenden Code in die Datei ein:

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

2. Um auf diese Datei im Webpart zu verweisen, öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und ändern Sie die **render**-Methode in:

    ```typescript
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

3. Überprüfen Sie, ob das Webpart wie erwartet funktioniert, indem Sie in der Befehlszeile Folgendes ausführen:

    ```sh
    gulp serve --nobrowser
    ```

Da das Webpart die Daten von SharePoint lädt, müssen Sie das Webpart mithilfe der gehosteten SharePoint Framework Workbench testen. Navigieren Sie zu `https://yourtenant.sharepoint.com/_layouts/workbench.aspx`, und fügen Sie das Webpart zum Zeichenbereich hinzu. Die IT-Anfragen sollten nun mithilfe des DataTables-Plug-Ins „jQuery“ angezeigt werden.

![IT-Anfragen, dargestellt in einem clientseitigen Webpart des SharePoint Framework](../../../images/datatables-spfx.png)

## <a name="add-support-for-configuring-the-web-part-through-web-part-properties"></a>Hinzufügen von Unterstützung zum Konfigurieren des Webparts über Webparteigenschaften

In den vorherigen Schritten haben Sie die Lösungen für IT-Anfragen vom Script Editor-Webpart in das SharePoint-Framework migriert. Die Lösung arbeitet zwar bereits wie erwartet, nutzt aber keine der Vorteile von SharePoint Framework. Der Name der Liste, aus der IT-Fragen geladen werden, ist im Code enthalten; bei dem Code selbst handelt es sich um reines JavaScript, das schwieriger umzugestalten ist als TypeScript. 

Die folgenden Schritte veranschaulichen, wie Sie die vorhanden Lösung erweitern können, damit Benutzer den Namen der Liste angeben können, aus der die Daten geladen werden sollen. Später wandeln Sie den Code in TypeScript um, um von den Typsicherheitsfeatures zu profitieren.

### <a name="define-web-part-property-for-storing-the-name-of-the-list"></a>Definieren der Webparteigenschaft zum Speichern des Listennamens

1. Definieren Sie eine Webparteigenschaft, um den Namen der Liste zu speichern, aus der IT-Anfragen geladen werden sollten. Öffnen Sie im Code-Editor die Datei  **./src/webparts/itRequests/ItRequestsWebPart.manifest.json**, und benennen Sie die Standardeinstellung **description** in **listName** um, und löschen Sie ihren Wert.

    ![Die listName-Eigenschaft im Webpartmanifest, hervorgehoben in Visual Studio Code](../../../images/datatables-spfx-listname-property.png)

2. Aktualisieren Sie die Webparteigenschaften, um die Änderungen im Manifest widerzuspiegeln. Öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/IItRequestsWebPartProps.ts**, und ändern Sie den Inhalt in:

    ```typescript
    export interface IItRequestsWebPartProps {
    listName: string;
    }
    ```

3. Aktualisieren die Anzeigebezeichnung für die **listName**-Eigenschaft. Öffnen Sie als Nächstes die Datei **./src/webparts/itRequests/loc/mystrings.d.ts**, und ändern Sie den Inhalt in:

    ```typescript
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

4. Öffnen Sie die Datei **./src/webparts/itRequests/loc/en-us.js**, und ändern Sie den Inhalt in:

    ```js
    define([], function() {
    return {
        "PropertyPaneDescription": "IT Requests settings",
        "BasicGroupName": "Data",
        "ListNameFieldLabel": "List name"
    }
    });
    ```

5. Aktualisieren Sie das Webpart so, dass die neu definierte Eigenschaft verwendet wird. Öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und ändern Sie die **getPropertyPaneConfiguration**-Methode in:

    ```typescript
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

### <a name="use-the-configured-name-of-the-list-to-load-the-data-from"></a>Verwenden des konfigurierten Namens der Liste, aus der Daten geladen werden sollen

Zunächst wurde der Name der Liste, aus der die Daten geladen werden sollen, in die REST-Abfrage eingebettet. Da Benutzer diesen Namen nun konfigurieren können, sollte der konfigurierte Wert in die REST-Abfrage injiziert werden, bevor die Daten geladen werden. Die einfachste Möglichkeit hierzu besteht darin, den Inhalt der **script.js**-Datei in die Haupt-Webpartdatei zu verschieben.

1. Öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und ändern Sie die **render**-Methode in:

    ```typescript
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

2. Statt auf den Code über die **script.js** Datei, des gesamten Inhalts sind ein Bestandteil der des Webparts **Rendern** Methode. In der REST-Abfrage in Zeile 40 können Sie nun den festen Namen der Liste durch den Wert der **listName**-Eigenschaft ersetzen, die den Namen der Liste wie vom Benutzer konfiguriert enthält. Bevor Sie den Wert verwenden, wird dieser mithilfe der **escape**-Funktion mit Escapezeichen versehen, um eine Skripteinschleusung zu verhindern.

    Der Großteil des Codes wird zu diesem Zeitpunkt immer noch mithilfe von reinem JavaScript geschrieben. Um Probleme mit der **$** jQ uery-Variablen zu vermeiden, mussten Sie diese in Zeile 18 als Typ **any** definieren. Später ersetzen Sie diese beim Umwandeln des Codes in TypeScript durch eine echte Typdefinition.

    Da Sie den Inhalt der Datei **script.js** gerade in die Haupt-Webpartdatei verschoben haben, ist **script.js** nicht mehr erforderlich, und Sie können die Datei aus dem Projekt löschen.

3. Um zu überprüfen, ob das Webpart wie erwartet funktioniert, führen Sie Folgendes in der Befehlszeile aus:

    ```sh
    gulp serve --nobrowser
    ```

4. Navigieren Sie zu der gehosteten Workbench, und fügen Sie das Webpart zum Zeichenbereich hinzu. Öffnen Sie den Webpart-Eigenschaftenbereich, geben Sie den Namen der Liste mit IT-Anfragen an, und wählen Sie die Schaltfläche  **Übernehmen** aus, um die Änderungen zu bestätigen. 

    Jetzt sollten die IT-Anfragen im Webpart angezeigt werden.

    ![IT-Anfragen, geladen aus der konfigurierten Liste und angezeigt im clientseitigen Webpart des SharePoint-Framework](../../../images/datatables-spfx-list-configured.png)

## <a name="transform-the-plain-javascript-code-to-typescript"></a>Transformieren des einfachen JavaScript-Codes in TypeScript

Die Verwendung von TypeScript bietet gegenüber der Verwendung von JavaScript eine Reihe von Vorteilen. TypeScript kann nicht nur einfacher verwaltet und umgestaltet werden, sondern ermöglicht auch ein früheres Abfangen von Fehlern. Die folgenden Schritte beschreiben, wie Sie den ursprünglichen JavaScript-Code in TypeScript umwandeln.

### <a name="add-type-definitions-for-used-libraries"></a>Hinzufügen von Typdefinitionen für verwendete Bibliotheken

Um ordnungsgemäß zu funktionieren, erfordert TypeScript Typdefinitionen für die verschiedenen Bibliotheken, die im Projekt verwendet werden. Typdefinitionen werden häufig als npm-Pakete im @types-Namespace bereitgestellt.

1. Installieren Sie die Typdefinitionen für jQuery und DataTables, indem Sie in der Befehlszeile Folgendes ausführen:

    ```sh
    npm install --save-dev @types/jquery @types/jquery.datatables
    ```

    Typdefinitionen für Moment.js werden zusammen mit dem Moment.js-Paket bereitgestellt. Obwohl Sie Moment.js über eine URL laden, müssen Sie das Moment.js-Paket trotzdem noch im Projekt installieren, um ihre Eingaben verwenden zu können.

2. Installieren Sie das Moment.js-Paket, indem Sie in der Befehlszeile Folgendes ausführen:

    ```sh
    npm install --save moment
    ```

### <a name="update-package-references"></a>Aktualisieren von Paketverweisen

Um Typen von den installierten Typdefinitionen zu verwenden, müssen Sie ändern, wie auf Bibliotheken verwiesen wird. 

1. Öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und ändern Sie die `import 'jquery';`-Anweisung in:

    ```typescript
    import * as $ from 'jquery';
    ```

2. Da Sie **$** als jQuery definiert haben, können Sie nun die lokale Definition von **$** entfernen, die Sie zuvor hinzugefügt hatten:

    ```typescript
    var $: any = (window as any).$;
    ```

3. Da es sich bei DataTables um ein jQuery-Plug-In handelt, das sich selbst an jQuery anfügt, können Sie seine Typdefinition nicht direkt laden. Stattdessen müssen Sie sie zur Liste der global geladenen Typen hinzufügen. Öffnen Sie im Code-Editor die Datei **./tsconfig.json**, und fügen Sie **jquery.datatables** zum **types**-Array hinzu:

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

Da jetzt die Typdefinitionen für alle im Projekt installierten Bibliotheken vorhanden sind, können Sie mit dem Transformieren des einfachen JavaScript-Codes in TypeScript beginnen.

1. Definieren Sie eine Schnittstelle für die IT-Anfrageinformationen, die Sie aus der SharePoint-Liste abrufen. Öffnen Sie im Code-Editor die Datei **./src/webparts/itRequests/ItRequestsWebPart.ts**, und fügen Sie direkt über der Webpartklasse den folgenden Codeausschnitt hinzu:

    ```typescript
    interface IRequestItem {
    ID: number;
    BusinessUnit: string;
    Category: string;
    Status: string;
    DueDate: string;
    AssignedTo: { Title: string; };
    }
    ```

2. Ändern Sie als Nächstes die **render**-Methode in:

    ```typescript
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

3. Sie werden feststellen, dass die AJAX-Anforderung zum Abrufen der Daten aus der SharePoint-Liste jetzt eingegeben ist, damit Sie sicherstellen können, dass Sie auf die korrekten Eigenschaften verweisen, wenn Sie diese in ein Array in DataTables übergeben. Die von DataTables verwendete Datenstruktur zur Darstellung einer Zeile in der Tabelle ist ein Array gemischter Typen, der Einfachheit halber wurde diese daher als **any[]** definiert. Die Verwendung des **any**-Typs in diesem Kontext ist nicht schlecht, da die in der **dataSrc**-Eigenschaft zurückgegebenen Daten intern von DataTables verwendet werden.

    Durch Aktualisieren der  **render**-Methode haben Sie auch zwei weitere Änderungen hinzugefügt. Zuerst haben sie das **Id**-Attribut aus der Tabelle entfernt. Auf diese Weise können Sie mehrere Instanzen desselben Webparts auf der Seite platzieren. Sie haben auch den Verweis auf die `$(document).ready()`-Funktion entfernt, der nicht erforderlich ist, da das DOM des Elements, in dem die Datentabelle gerendert wird, vor dem DataTables-Initiierungscode festgelegt wird.

### <a name="update-the-momentjs-datatables-plugin-to-typescript"></a>Aktualisieren des Moment.js-DataTables-Plug-Ins in TypeScript

Der letzte Teil dieser Lösung, der in TypeScript umgewandelt werden muss, ist das Moment.js-DataTable-Plug-in. 

1. Benennen Sie die Datei **./src/webparts/itRequests/moment-plugin.js** in **./src/webparts/itRequests/moment-plugin.ts** um , damit sie vom TypeScript -Compiler verarbeitet wird. 

2. Öffnen Sie im Code-Editor die Datei **moment-plugin.ts**, und ersetzen Sie den Inhalt durch:

    ```typescript
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

3. Beginnen Sie, die Verweise in jQuery und Moment.js zu laden, um TypeScript mitzuteilen, worauf die entsprechenden Variablen verweisen. Als Nächstes definieren Sie die Plug-In-Funktion. In der Regel wird in TypeScript die Pfeilnotation für Funktionen (`=>`) verwendet. In diesem Fall müssen Sie jedoch die reguläre Funktionsdefinition verwenden, da Sie Zugriff auf die **arguments**-Eigenschaft benötigen. Um zu verhindern, dass eine Warnung angezeigt wird, weil die Pfeilnotation nicht verwendet wird, können Sie die Regel **no-function-expression** um die Funktionsdefinition explizit deaktivieren.

4. Führen Sie in der Befehlszeile Folgendes aus, um zu überprüfen, dass alles wie erwartet funktioniert:

    ```sh
    gulp serve --nobrowser
```

5. Navigieren Sie zu der gehosteten Workbench, und fügen Sie das Webpart zum Zeichenbereich hinzu. Obwohl sich visuell nichts geändert hat, verwendet die neue Codebasis TypeScript und seine Typdefinitionen, um Sie bei der Verwaltung der Lösung zu unterstützen.
