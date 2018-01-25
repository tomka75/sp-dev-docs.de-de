---
title: "Migrieren von jQuery- und FullCalendar-Lösungen, die mit dem Script Editor-Webpart erstellt wurden, in das SharePoint-Framework"
description: Migrieren Sie eine SharePoint-Anpassung mithilfe von FullCalendar, der mit dem Skript-Editor-Webpart erstellt wird, in das SharePoint Framework.
ms.date: 01/09/2018
ms.prod: sharepoint
ms.openlocfilehash: 5127e9f8598ff087bdbc34f9f1e678226bd127da
ms.sourcegitcommit: 2188f21ce207c9d62d7d8af93822bd101058ba2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/10/2018
---
# <a name="migrate-jquery-and-fullcalendar-solution-built-using-script-editor-web-part-to-sharepoint-framework"></a>Migrieren von jQuery- und FullCalendar-Lösungen, die mit dem Script Editor-Webpart erstellt wurden, in das SharePoint-Framework

Beim Erstellen von SharePoint-Lösungen, verwenden SharePoint-Entwickler häufig das [FullCalendar](https://fullcalendar.io)- jQuery-Plug-In zum Anzeigen von Daten in der Kalenderansicht. FullCalendar ist eine großartige Alternative zu der standardmäßigen SharePoint-Kalenderansicht, da sie das Rendern von Daten als Kalenderdaten aus mehreren Kalenderlisten, von Daten aus Nicht-Kalenderlisten oder sogar von Daten außerhalb von SharePoint ermöglicht. In diesem Artikel wird beschrieben, wie Sie eine SharePoint-Anpassung mithilfe von FullCalendar, der mit dem Skript-Editor-Webpart erstellt wird, in das SharePoint Framework migrieren.

## <a name="list-of-tasks-displayed-as-a-calendar-built-using-the-script-editor-web-part"></a>Als Kalender angezeigte Liste von Aufgaben, erstellt mithilfe des Skript-Editor-Webparts

Um das Verfahren der Migration einer SharePoint-Anpassung in das SharePoint-Framework mithilfe von FullCalendar zu veranschaulichen, verwenden Sie die folgende Lösung, die eine Kalenderansicht von Aufgaben zeigt, die aus einer SharePoint-Liste abgerufen wurden.

![Kalenderansicht von Aufgaben, angezeigt auf einer SharePoint-Seite](../../../images/fullcalendar-sewp.png)

Die Lösung wird anhand des standardmäßigen Skript-Editor-Webparts von SharePoint erstellt. Nachfolgend ist der in der Anpassung verwendete Code aufgeführt.

```html
<script src="//code.jquery.com/jquery-1.11.1.min.js"></script>
<script src="//cdnjs.cloudflare.com/ajax/libs/moment.js/2.10.6/moment.min.js"></script>
<script src="//cdnjs.cloudflare.com/ajax/libs/fullcalendar/3.4.0/fullcalendar.min.js"></script>
<link type="text/css" rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/fullcalendar/3.4.0/fullcalendar.min.css" />
<div id="calendar"></div>

<script>
  var PATH_TO_DISPFORM = _spPageContextInfo.webAbsoluteUrl + "/Lists/Tasks/DispForm.aspx";
  var TASK_LIST = "Tasks";
  var COLORS = ['#466365', '#B49A67', '#93B7BE', '#E07A5F', '#849483', '#084C61', '#DB3A34'];

  displayTasks();

  function displayTasks() {
    $('#calendar').fullCalendar('destroy');
    $('#calendar').fullCalendar({
      weekends: false,
      header: {
        left: 'prev,next today',
        center: 'title',
        right: 'month,basicWeek,basicDay'
      },
      displayEventTime: false,
      // open up the display form when a user clicks on an event
      eventClick: function (calEvent, jsEvent, view) {
        window.location = PATH_TO_DISPFORM + "?ID=" + calEvent.id;
      },
      editable: true,
      timezone: "UTC",
      droppable: true, // this allows things to be dropped onto the calendar
      // update the end date when a user drags and drops an event 
      eventDrop: function (event, delta, revertFunc) {
        updateTask(event.id, event.start, event.end);
      },
      // put the events on the calendar 
      events: function (start, end, timezone, callback) {
        var startDate = start.format('YYYY-MM-DD');
        var endDate = end.format('YYYY-MM-DD');

        var restQuery = "/_api/Web/Lists/GetByTitle('" + TASK_LIST + "')/items?$select=ID,Title,\
Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
$filter=((DueDate ge '" + startDate + "' and DueDate le '" + endDate + "')or(StartDate ge '" + startDate + "' and StartDate le '" + endDate + "'))";

        $.ajax({
          url: _spPageContextInfo.webAbsoluteUrl + restQuery,
          type: "GET",
          dataType: "json",
          headers: {
            Accept: "application/json;odata=nometadata"
          }
        })
          .done(function (data, textStatus, jqXHR) {
            var personColors = {};
            var colorNo = 0;

            var events = data.value.map(function (task) {
              var assignedTo = task.AssignedTo.map(function (person) {
                return person.Title;
              }).join(', ');

              var color = personColors[assignedTo];
              if (!color) {
                color = COLORS[colorNo++];
                personColors[assignedTo] = color;
              }
              if (colorNo >= COLORS.length) {
                colorNo = 0;
              }

              return {
                title: task.Title + " - " + assignedTo,
                id: task.ID,
                color: color, // specify the background color and border color can also create a class and use className parameter. 
                start: moment.utc(task.StartDate).add("1", "days"),
                end: moment.utc(task.DueDate).add("1", "days") // add one day to end date so that calendar properly shows event ending on that day
              };
            });

            callback(events);
          });
      }
    });
  }

  function updateTask(id, startDate, dueDate) {
    // subtract the previously added day to the date to store correct date
    var sDate = moment.utc(startDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
      startDate.format("hh:mm") + ":00Z";
    if (!dueDate) {
      dueDate = startDate;
    }
    var dDate = moment.utc(dueDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
      dueDate.format("hh:mm") + ":00Z";

    $.ajax({
      url: _spPageContextInfo.webAbsoluteUrl + '/_api/contextinfo',
      type: 'POST',
      headers: {
        'Accept': 'application/json;odata=nometadata'
      }
    })
      .then(function (data, textStatus, jqXHR) {
        return $.ajax({
          url: _spPageContextInfo.webAbsoluteUrl +
          "/_api/Web/Lists/getByTitle('" + TASK_LIST + "')/Items(" + id + ")",
          type: 'POST',
          data: JSON.stringify({
            StartDate: sDate,
            DueDate: dDate,
          }),
          headers: {
            Accept: "application/json;odata=nometadata",
            "Content-Type": "application/json;odata=nometadata",
            "X-RequestDigest": data.FormDigestValue,
            "IF-MATCH": "*",
            "X-Http-Method": "PATCH"
          }
        });
      })
      .done(function (data, textStatus, jqXHR) {
        alert("Update Successful");
      })
      .fail(function (jqXHR, textStatus, errorThrown) {
        alert("Update Failed");
      })
      .always(function () {
        displayTasks();
      });
  }
</script>
```

> [!NOTE] 
> Diese Lösung basiert auf der Arbeit von Mark Rackley, Office Servers and Services MVP und Chief Strategy Officer bei der PAIT Group. Weitere Informationen zu der ursprünglichen Lösung finden Sie unter [Erstellen von benutzerdefinierten Kalendern in SharePoint mithilfe von FullCalender.io](http://www.markrackley.net/2017/06/07/using-fullcalendar-io-to-create-custom-calendars-in-sharepoint/).

Die Anpassung lädt zuerst die verwendeten Bibliotheken: jQuery, DataTables und FullCalendar (Zeilen 1-4). 

Als Nächstes wird die div definiert, in die die generierte Kalenderansicht eingeschleust wird (Zeile 5). 

Dann werden zwei Funktionen definiert: **displayTasks**, zum Anzeigen von Aufgaben in der Kalenderansicht, und **updateTask**, die ausgelöst wird, nachdem eine Aufgabe per Drag & Drop auf einem anderen Datum abgelegt wurde und die die Datumsangaben im zugrunde liegenden Listenelement aktualisiert. Jede Funktion definiert eine eigene REST-Abfrage, die dann zum Kommunizieren mit der REST-API der SharePoint-Liste verwendet wird, um die Listenelemente abzurufen oder zu aktualisieren.

Mithilfe des jQuery-Plug-Ins FullCalendar erhalten Benutzer mit wenig Aufwand reichhaltige Lösungen, die z. B. verschiedene Farben zum Kennzeichnen von verschiedenen Ereignissen verwenden oder mit Drag & Drop Ereignisse neu organisieren können.

![Ziehen von Ereignissen in FullCalendar, um zugrunde liegende Aufgaben neu zu planen](../../../images/fullcalendar-sewp-draganddrop.png)

## <a name="migrate-the-tasks-calendar-solution-from-the-script-editor-web-part-to-the-sharepoint-framework"></a>Migrieren der Aufgabenkalenderlösung vom Script Editor-Webpart in das SharePoint-Framework

> [!NOTE] 
> Bevor Sie die Schritte in diesem Artikel durchführen, müssen Sie [eine Entwicklungsumgebung einrichten](../../set-up-your-development-environment.md), in der Sie SharePoint-Framework-Lösungen erstellen können.

Das Umwandeln einer Anpassung, die auf dem Skript-Editor-Webpart basiert, in SharePoint Framework bietet zahlreiche Vorteile, z. B. die benutzerfreundlichere Konfiguration und die zentrale Verwaltung der Lösung. Nachfolgend finden Sie eine schrittweise Beschreibung der Migration der Lösung in SharePoint Framework. 

Zuerst migrieren Sie die Lösung in das SharePoint Framework mit so wenig Änderungen am ursprünglichen Code wie möglich. Später wandeln Sie den Code der Lösung in TypeScript um, um von den Typsicherheitsfeatures zur Entwicklungszeit zu profitieren, und ersetzen einen Teil des Codes durch die SharePoint Framework-API, um deren Funktionen voll auszunutzen und die Lösung weiter zu vereinfachen.

> [!NOTE] 
> Der Quellcode des Projekts in den verschiedenen Phasen der Migration steht unter [Lernprogramm: Migrieren von jQuery- und FullCalendar-Lösungen, die mit Skript- Editor-Webpart erstellt wurden, in SharePoint Framework](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/tutorials/tutorial-migrate-fullcalendar) zur Verfügung.

### <a name="create-new-sharepoint-framework-project"></a>Erstellen eines neuen SharePoint-Framework-Projekts

1. Erstellen Sie zunächst einen neuen Ordner für Ihr Projekt:

  ```sh
  md fullcalendar-taskscalendar
  ```

2. Navigieren Sie zum Projektordner:

  ```sh
  cd fullcalendar-taskscalendar
  ```

3. Führen Sie im Projektordner den SharePoint Framework-Yeoman-Generator aus, um ein Gerüst für ein neues SharePoint Framework-Projekt zu erstellen:

  ```sh
  yo @microsoft/sharepoint
  ```

4. Es werden mehrere Eingabeaufforderungen angezeigt. Definieren Sie die Werte jeweils wie folgt:
  - **fullcalendar-taskscalendar** als Ihren Lösungsnamen
  - **Aktuellen Ordner verwenden** als Speicherort für die Dateien
  - **WebPart** als die zu erstellende clientseitige Komponente
  - **Aufgabenkalender** als Name des Webparts
  - **Zeigt Aufgaben in der Kalenderansicht** als Beschreibung des Webparts
  - **No javaScript web framework** als Eintrittspunkt für die Webpart-Erstellung

  ![SharePoint-Framework-Yeoman-Generator mit den Standardoptionen](../../../images/fullcalendar-yeoman.png)

5. Sobald das Gerüst abgeschlossen ist, sperren Sie die Version der Projektabhängigkeiten, indem Sie den folgenden Befehl ausführen:

  ```sh
  npm shrinkwrap
  ```

6. Öffnen Sie den Projektordner in einem Code-Editor. In diesem Tutorial verwenden Sie Visual Studio Code.

  ![SharePoint Framework-Projekt in Visual Studio Code](../../../images/fullcalendar-vscode.png)

### <a name="load-javascript-libraries"></a>Laden von JavaScript-Bibliotheken

Ähnlich wie bei der ursprünglichen Lösung, die mithilfe des Skript-Editor-Webparts erstellt wurde, müssen Sie zuerst die JavaScript-Bibliotheken laden, die für die Lösung erforderlich sind. In SharePoint Framework besteht dies in der Regel aus zwei Schritten: Festlegen der URL, von der die Bibliothek geladen werden soll, und Verweisen auf die Bibliothek im Code.

1. Geben Sie die URLs an, von der Bibliotheken geladen werden sollen. Öffnen Sie im Code-Editor die Datei **./config/config.json**, und ändern Sie den Abschnitt **externals** in Folgendes:

  ```json
  {
    "externals": {
      "jquery": "https://code.jquery.com/jquery-1.11.1.min.js",
      "moment": "https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.10.6/moment.min.js",
      "fullcalendar": "https://cdnjs.cloudflare.com/ajax/libs/fullcalendar/3.4.0/fullcalendar.min.js"
    }
  }
  ```

2. Öffnen Sie die Datei **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts**, und fügen Sie nach der letzten **import**-Anweisung Folgendes hinzu:

  ```ts
  import 'jquery';
  import 'moment';
  import 'fullcalendar';
  ```

### <a name="define-container-div"></a>Definieren des div-Containers

Wie bei der ursprünglichen Lösung besteht der nächste Schritt darin, die Position zu definieren, an der der Kalender wiedergegeben werden soll. 

Öffnen Sie im Code-Editor die Datei **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts**, und ändern Sie die **render**-Methode in Folgendes:

```ts
  export default class ItRequestsWebPart extends BaseClientSideWebPart<IItRequestsWebPartProps> {
    public render(): void {
      this.domElement.innerHTML = `
        <div class="${styles.tasksCalendar}">
          <link type="text/css" rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/fullcalendar/3.4.0/fullcalendar.min.css" />
          <div id="calendar"></div>
        </div>`;
    }
    // ...
  }
```

### <a name="initiate-fullcalendar-and-load-data"></a>Initiieren von FullCalendar und Laden von Daten

Der letzte Schritt besteht darin, den Code einzuschließen, der das jQuery-Plug-In „FullCalendar“ initiiert und die Daten aus SharePoint lädt. 

1.  Erstellen Sie im Ordner **./src/webparts/tasksCalendar** eine neue Datei mit dem Namen **script.js**, und fügen Sie den folgenden Code in die Datei ein:

  ```js
  var moment = require('moment');

  var PATH_TO_DISPFORM = window.webAbsoluteUrl + "/Lists/Tasks/DispForm.aspx";
  var TASK_LIST = "Tasks";
  var COLORS = ['#466365', '#B49A67', '#93B7BE', '#E07A5F', '#849483', '#084C61', '#DB3A34'];

  displayTasks();

  function displayTasks() {
    $('#calendar').fullCalendar('destroy');
    $('#calendar').fullCalendar({
      weekends: false,
      header: {
        left: 'prev,next today',
        center: 'title',
        right: 'month,basicWeek,basicDay'
      },
      displayEventTime: false,
      // open up the display form when a user clicks on an event
      eventClick: function (calEvent, jsEvent, view) {
        window.location = PATH_TO_DISPFORM + "?ID=" + calEvent.id;
      },
      editable: true,
      timezone: "UTC",
      droppable: true, // this allows things to be dropped onto the calendar
      // update the end date when a user drags and drops an event 
      eventDrop: function (event, delta, revertFunc) {
        updateTask(event.id, event.start, event.end);
      },
      // put the events on the calendar 
      events: function (start, end, timezone, callback) {
        var startDate = start.format('YYYY-MM-DD');
        var endDate = end.format('YYYY-MM-DD');

        var restQuery = "/_api/Web/Lists/GetByTitle('" + TASK_LIST + "')/items?$select=ID,Title,\
  Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
  $filter=((DueDate ge '" + startDate + "' and DueDate le '" + endDate + "')or(StartDate ge '" + startDate + "' and StartDate le '" + endDate + "'))";

        $.ajax({
          url: window.webAbsoluteUrl + restQuery,
          type: "GET",
          dataType: "json",
          headers: {
            Accept: "application/json;odata=nometadata"
          }
        })
          .done(function (data, textStatus, jqXHR) {
            var personColors = {};
            var colorNo = 0;

            var events = data.value.map(function (task) {
              var assignedTo = task.AssignedTo.map(function (person) {
                return person.Title;
              }).join(', ');

              var color = personColors[assignedTo];
              if (!color) {
                color = COLORS[colorNo++];
                personColors[assignedTo] = color;
              }
              if (colorNo >= COLORS.length) {
                colorNo = 0;
              }

              return {
                title: task.Title + " - " + assignedTo,
                id: task.ID,
                color: color, // specify the background color and border color can also create a class and use className parameter. 
                start: moment.utc(task.StartDate).add("1", "days"),
                end: moment.utc(task.DueDate).add("1", "days") // add one day to end date so that calendar properly shows event ending on that day
              };
            });

            callback(events);
          });
      }
    });
  }

  function updateTask(id, startDate, dueDate) {
    // subtract the previously added day to the date to store correct date
    var sDate = moment.utc(startDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
      startDate.format("hh:mm") + ":00Z";
    if (!dueDate) {
      dueDate = startDate;
    }
    var dDate = moment.utc(dueDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
      dueDate.format("hh:mm") + ":00Z";

    $.ajax({
      url: window.webAbsoluteUrl + '/_api/contextinfo',
      type: 'POST',
      headers: {
        'Accept': 'application/json;odata=nometadata'
      }
    })
      .then(function (data, textStatus, jqXHR) {
        return $.ajax({
          url: window.webAbsoluteUrl +
          "/_api/Web/Lists/getByTitle('" + TASK_LIST + "')/Items(" + id + ")",
          type: 'POST',
          data: JSON.stringify({
            StartDate: sDate,
            DueDate: dDate,
          }),
          headers: {
            Accept: "application/json;odata=nometadata",
            "Content-Type": "application/json;odata=nometadata",
            "X-RequestDigest": data.FormDigestValue,
            "IF-MATCH": "*",
            "X-Http-Method": "PATCH"
          }
        });
      })
      .done(function (data, textStatus, jqXHR) {
        alert("Update Successful");
      })
      .fail(function (jqXHR, textStatus, errorThrown) {
        alert("Update Failed");
      })
      .always(function () {
        displayTasks();
      });
  }
  ```

  Dieser Code ist fast identisch mit den ursprünglichen Code der Anpassung des Skript-Editor-Webparts. Der einzige Unterschied besteht darin, dass der ursprüngliche Code die URL des aktuellen Webs aus der globalen **\_SpPageContextInfo**-Variablen abruft, die von SharePoint festgelegt wird (Zeile 8, 45, 96 und 104), wohingegen der Code im SharePoint Framework eine benutzerdefinierte Variable verwendet, die Sie im Webpart festlegen müssen. 
  
  Clientseitige SharePoint Framework-Webparts können sowohl in klassischen als auch in modernen Seiten verwendet werden. Die **_spPageContextInfo**-Variable ist zwar auf klassischen Seiten, aber nicht auf modernen Seiten vorhanden. Deshalb können Sie sich nicht darauf verlassen und benötigen eine benutzerdefinierte Eigenschaft, die Sie selbst steuern können.

2. Um auf diese Datei im Webpart zu verweisen, öffnen Sie im Code-Editor die Datei **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts**, und ändern Sie die **render**-Methode in:

  ```ts
  export default class ItRequestsWebPart extends BaseClientSideWebPart<IItRequestsWebPartProps> {
    public render(): void {
      this.domElement.innerHTML = `
        <div class="${styles.tasksCalendar}">
          <link type="text/css" rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/fullcalendar/3.4.0/fullcalendar.min.css" />
          <div id="calendar"></div>
        </div>`;

      (window as any).webAbsoluteUrl = this.context.pageContext.web.absoluteUrl;
      require('./script');
    }
    // ...
  }
  ```

3. Führen Sie folgenden Befehl über die Befehlszeile aus, um zu überprüfen, ob das Webpart wie erwartet funktioniert:

  ```sh
  gulp serve --nobrowser
  ```

  Da das Webpart die Daten von SharePoint lädt, müssen Sie das Webpart mithilfe der gehosteten SharePoint Framework Workbench testen. 
  
4. Navigieren Sie zu `https://yourtenant.sharepoint.com/_layouts/workbench.aspx`, und fügen Sie das Webpart zum Zeichenbereich hinzu. Nun sollten die Aufgaben mithilfe des jQuery-Plug-Ins „FullCalendar“ in einer Kalenderansicht angezeigt werden.

  ![Aufgaben, dargestellt in einer Kalenderansicht in einem clientseitigen Webpart aus dem SharePoint-Framework](../../../images/fullcalendar-spfx.png)

## <a name="add-support-for-configuring-the-web-part-through-web-part-properties"></a>Hinzufügen von Unterstützung zum Konfigurieren des Webparts über Webparteigenschaften

In den vorherigen Schritten haben Sie die Aufgabenkalenderlösungen vom Skript-Editor-Webpart in das SharePoint-Framework migriert. Die Lösung arbeitet zwar bereits wie erwartet, nutzt aber keine der Vorteile von SharePoint Framework. Der Name der Liste, aus der Aufgaben geladen werden, ist im Code enthalten; bei dem Code selbst handelt es sich um reines JavaScript, das schwieriger umzugestalten ist als TypeScript. 

Die folgenden Schritte veranschaulichen, wie Sie die vorhandene Lösung erweitern können, damit Benutzer den Namen der Liste angeben können, aus der die Daten geladen werden sollen. Später wandeln Sie den Code in TypeScript um, um von den Typsicherheitsfeatures zu profitieren.

### <a name="define-web-part-property-for-storing-the-name-of-the-list"></a>Definieren der Webparteigenschaft zum Speichern des Listennamens

1. Definieren Sie eine Webparteigenschaft, um den Namen der Liste zu speichern, aus der Aufgaben geladen werden sollten. Öffnen Sie im Code-Editor die Datei **./src/webparts/tasksCalendar/TasksCalendarWebPart.manifest.json**, und benennen Sie die Standardeinstellung **description** in **listName** um, und löschen Sie ihren Wert.

  ![Die listName-Eigenschaft im Webpartmanifest, hervorgehoben in Visual Studio Code](../../../images/fullcalendar-spfx-listname-property.png)

2. Aktualisieren Sie die Webparteigenschaften, um die Änderungen im Manifest widerzuspiegeln. Öffnen Sie im Code-Editor die Datei **./src/webparts/tasksCalendar/ITasksCalendarWebPartProps.ts**, und ändern Sie den Inhalt in Folgendes:

  ```ts
  export interface ITasksCalendarWebPartProps {
    listName: string;
  }
  ```

3. Aktualisieren Sie die Anzeigebezeichnungen für die **listName**-Eigenschaft. Öffnen Sie die Datei **./src/webparts/tasksCalendar/loc/mystrings.d.ts**, und ändern Sie den Inhalt in:

  ```ts
  declare interface ITasksCalendarStrings {
    PropertyPaneDescription: string;
    BasicGroupName: string;
    ListNameFieldLabel: string;
  }

  declare module 'tasksCalendarStrings' {
    const strings: ITasksCalendarStrings;
    export = strings;
  }
  ```

4. Öffnen Sie die Datei **./src/webparts/tasksCalendar/loc/en-us.js**, und ändern Sie den Inhalt in:

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Tasks calendar settings",
      "BasicGroupName": "Data",
      "ListNameFieldLabel": "List name"
    }
  });
  ```

5. Aktualisieren Sie das Webpart so, dass die neu definierte Eigenschaft verwendet wird. Öffnen Sie im Code-Editor die Datei **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts**, und ändern Sie die **getPropertyPaneConfiguration**-Methode in:

  ```ts
  export default class TasksCalendarWebPart extends BaseClientSideWebPart<ITasksCalendarWebPartProps> {
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

Zunächst wurde der Name der Liste, aus der die Daten geladen werden sollen, in die REST-Abfragen eingebettet. Da Benutzer diesen Namen nun konfigurieren können, sollte der konfigurierte Wert in die REST-Abfragen injiziert werden, bevor diese ausgeführt werden. Die einfachste Möglichkeit hierzu besteht darin, den Inhalt der **script.js**-Datei in die Haupt-Webpartdatei zu verschieben.

1. Öffnen Sie im Code-Editor die Datei **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts**.

2. Ändern Sie die import-Anweisung, sodass die erforderlichen Bibliotheken geladen werden:

  ```ts
  var $: any = require('jquery');
  var moment: any = require('moment');

  import 'fullcalendar';

  var COLORS = ['#466365', '#B49A67', '#93B7BE', '#E07A5F', '#849483', '#084C61', '#DB3A34'];
  ```

  Da in dem Code, den Sie später verwenden werden, auf Moment.js verwiesen wird, muss dieser Name für TypeScript bekannt sein, da sonst das Erstellen des Projekts fehlschlägt. Das gleiche gilt für jQuery. Da FullCalendar ein jQuery-Plug-In ist, das sich selbst an das jQuery-Objekt anheftet, kann es auf die gleiche Weise wie zuvor importiert werden.

  Der letzte Teil umfasst das Kopieren der Liste von Farben, die zum Kennzeichnen der unterschiedlichen Ereignisse verwendet werden.

3. Kopieren Sie die Funktionen **displayTasks** und **updateTask** aus der Datei **script.js**, und fügen Sie sie wie folgt innerhalb der **TasksCalendarWebPart**-Klasse ein:

  ```ts
  export default class TasksCalendarWebPart extends BaseClientSideWebPart<ITasksCalendarWebPartProps> {
    // ...

    private displayTasks() {
      $('#calendar').fullCalendar('destroy');
      $('#calendar').fullCalendar({
        weekends: false,
        header: {
          left: 'prev,next today',
          center: 'title',
          right: 'month,basicWeek,basicDay'
        },
        displayEventTime: false,
        // open up the display form when a user clicks on an event
        eventClick: (calEvent, jsEvent, view) => {
          (window as any).location = this.context.pageContext.web.absoluteUrl +
            "/Lists/" + escape(this.properties.listName) + "/DispForm.aspx?ID=" + calEvent.id;
        },
        editable: true,
        timezone: "UTC",
        droppable: true, // this allows things to be dropped onto the calendar
        // update the end date when a user drags and drops an event 
        eventDrop: (event, delta, revertFunc) => {
          this.updateTask(event.id, event.start, event.end);
        },
        // put the events on the calendar 
        events: (start, end, timezone, callback) => {
          var startDate = start.format('YYYY-MM-DD');
          var endDate = end.format('YYYY-MM-DD');

          var restQuery = "/_api/Web/Lists/GetByTitle('" + escape(this.properties.listName) + "')/items?$select=ID,Title,\
  Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
  $filter=((DueDate ge '" + startDate + "' and DueDate le '" + endDate + "')or(StartDate ge '" + startDate + "' and StartDate le '" + endDate + "'))";

          $.ajax({
            url: this.context.pageContext.web.absoluteUrl + restQuery,
            type: "GET",
            dataType: "json",
            headers: {
              Accept: "application/json;odata=nometadata"
            }
          })
            .done((data, textStatus, jqXHR) => {
              var personColors = {};
              var colorNo = 0;

              var events = data.value.map((task) => {
                var assignedTo = task.AssignedTo.map((person) => {
                  return person.Title;
                }).join(', ');

                var color = personColors[assignedTo];
                if (!color) {
                  color = COLORS[colorNo++];
                  personColors[assignedTo] = color;
                }
                if (colorNo >= COLORS.length) {
                  colorNo = 0;
                }

                return {
                  title: task.Title + " - " + assignedTo,
                  id: task.ID,
                  color: color, // specify the background color and border color can also create a class and use className parameter. 
                  start: moment.utc(task.StartDate).add("1", "days"),
                  end: moment.utc(task.DueDate).add("1", "days") // add one day to end date so that calendar properly shows event ending on that day
                };
              });

              callback(events);
            });
        }
      });
    }

    private updateTask(id, startDate, dueDate) {
      // subtract the previously added day to the date to store correct date
      var sDate = moment.utc(startDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
        startDate.format("hh:mm") + ":00Z";
      if (!dueDate) {
        dueDate = startDate;
      }
      var dDate = moment.utc(dueDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
        dueDate.format("hh:mm") + ":00Z";

      $.ajax({
        url: this.context.pageContext.web.absoluteUrl + '/_api/contextinfo',
        type: 'POST',
        headers: {
          'Accept': 'application/json;odata=nometadata'
        }
      })
        .then((data, textStatus, jqXHR) => {
          return $.ajax({
            url: this.context.pageContext.web.absoluteUrl +
            "/_api/Web/Lists/getByTitle('" + escape(this.properties.listName) + "')/Items(" + id + ")",
            type: 'POST',
            data: JSON.stringify({
              StartDate: sDate,
              DueDate: dDate,
            }),
            headers: {
              Accept: "application/json;odata=nometadata",
              "Content-Type": "application/json;odata=nometadata",
              "X-RequestDigest": data.FormDigestValue,
              "IF-MATCH": "*",
              "X-Http-Method": "PATCH"
            }
          });
        })
        .done((data, textStatus, jqXHR) => {
          alert("Update Successful");
        })
        .fail((jqXHR, textStatus, errorThrown) => {
          alert("Update Failed");
        })
        .always(() => {
          this.displayTasks();
        });
    }

    // ...
  }
  ```

  <br/>

   Im Vergleich zur vorherigen Situation gibt es ein paar Änderungen am Code. Einfache JavaScript-Funktionen wurden in TypeScript Methoden-geändert, indem das **function**-Schlüsselwort durch den **private**-Modifizierer ersetzt wurde. Dies ist erforderlich, damit diese der **TaskCalendarWebPart**-Klasse hinzugefügt werden können. Da sich beide Methoden nun in derselben Datei als Webpart befinden können Sie direkt vom Webpartkontext mithilfe der `this.context.pageContext.web.absoluteUrl` Eigenschaft darauf zugreifen, anstatt eine globale Variable für die URL der aktuellen Website zu definieren. Außerdem wird in allen REST-Abfragen der feste Listenname durch den Wert der **listName**-Eigenschaft ersetzt, die den Namen der Liste wie vom Benutzer konfiguriert enthält. Bevor Sie den Wert verwenden, wird dieser mithilfe der **escape**-Funktion mit Escapezeichen versehen, um eine Skripteinschleusung zu verhindern.

4. Als letzten Schritt ändern Sie die **render**-Methode, um die neu hinzugefügte **displayTasks**-Methode aufzurufen:

  ```ts
  export default class TasksCalendarWebPart extends BaseClientSideWebPart<ITasksCalendarWebPartProps> {
    public render(): void {
      this.domElement.innerHTML = `
        <div class="${styles.tasksCalendar}">
          <link type="text/css" rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/fullcalendar/3.4.0/fullcalendar.min.css" />
          <div id="calendar"></div>
        </div>`;

      this.displayTasks();
    }
    // ...
  }
  ```

5. Da Sie den Inhalt der Datei **script.js** gerade in die Haupt-Webpartdatei verschoben haben, ist **script.js** nicht mehr erforderlich, und Sie können die Datei aus dem Projekt löschen.

6. Um zu überprüfen, ob das Webpart wie erwartet funktioniert, führen Sie Folgendes in der Befehlszeile aus:

  ```sh
  gulp serve --nobrowser
  ```

7. Navigieren Sie zu der gehosteten Workbench, und fügen Sie das Webpart zum Zeichenbereich hinzu. Öffnen Sie den Webpart-Eigenschaftenbereich, geben Sie den Namen der Liste mit Aufgaben an, und wählen Sie die Schaltfläche **Übernehmen** aus, um die Änderungen zu bestätigen. Jetzt sollten Aufgaben in einer Kalenderansicht im Webpart angezeigt werden.

  ![Aufgaben, geladen aus der konfigurierten Liste und angezeigt in einem clientseitigen Webpart des SharePoint-Framework](../../../images/fullcalendar-spfx-list-configured.png)

## <a name="transform-the-plain-javascript-code-to-typescript"></a>Transformieren des einfachen JavaScript-Codes in TypeScript

Die Verwendung von TypeScript bietet gegenüber der Verwendung von JavaScript eine Reihe von Vorteilen. TypeScript kann nicht nur einfacher verwaltet und umgestaltet werden, sondern ermöglicht auch ein früheres Abfangen von Fehlern. Die folgenden Schritte beschreiben, wie Sie den ursprünglichen JavaScript-Code in TypeScript umwandeln.

### <a name="add-type-definitions-for-used-libraries"></a>Hinzufügen von Typdefinitionen für verwendete Bibliotheken

Um ordnungsgemäß zu funktionieren, erfordert TypeScript Typdefinitionen für die verschiedenen Bibliotheken, die im Projekt verwendet werden. Typdefinitionen werden häufig als npm-Pakete im @types-Namespace bereitgestellt.

1. Installieren Sie die Typdefinitionen für jQuery und FullCalendar, indem Sie in der Befehlszeile Folgendes ausführen:

  ```sh
  npm install --save-dev @types/jquery@1 @types/fullcalendar
  ```

  Typdefinitionen für Moment.js werden zusammen mit dem Moment.js-Paket bereitgestellt. Obwohl Sie Moment.js über eine URL laden, müssen Sie das Moment.js-Paket trotzdem noch im Projekt installieren, um ihre Eingaben verwenden zu können.

2. Installieren Sie das Moment.js-Paket, indem Sie in der Befehlszeile Folgendes ausführen:

  ```sh
  npm install --save moment
  ```

### <a name="update-package-references"></a>Aktualisieren von Paketverweisen

Um Typen von den installierten Typdefinitionen zu verwenden, müssen Sie ändern, wie auf Bibliotheken verwiesen wird. 

Öffnen Sie im Code-Editor die Datei **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts**, und ändern Sie die import-Anweisungen in Folgendes:

```ts
import * as $ from 'jquery';
import 'fullcalendar';
import * as moment from 'moment';
```

### <a name="update-main-web-part-files-to-typescript"></a>Aktualisieren der Haupt-Webpartdateien in TypeScript

Da jetzt die Typdefinitionen für alle im Projekt installierten Bibliotheken vorhanden sind, können Sie mit dem Transformieren des einfachen JavaScript-Codes in TypeScript beginnen.

1. Definieren Sie eine Schnittstelle für eine Aufgabe, die Sie aus der SharePoint-Liste abrufen. Öffnen Sie im Code-Editor die Datei **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts**, und fügen Sie direkt über der Webpartklasse den folgenden Codeausschnitt hinzu:

  ```ts
  interface ITask {
    ID: number;
    Title: string;
    StartDate: string;
    DueDate: string;
    AssignedTo: [{ Title: string }];
  }
  ```

2. Ändern Sie in der Webpartklasse die Methoden **displayTasks** und **updateTask** in:

  ```ts
  export default class TasksCalendarWebPart extends BaseClientSideWebPart<ITasksCalendarWebPartProps> {
    private readonly colors: string[] = ['#466365', '#B49A67', '#93B7BE', '#E07A5F', '#849483', '#084C61', '#DB3A34'];

    // ...

    private displayTasks(): void {
      $('#calendar').fullCalendar('destroy');
      $('#calendar').fullCalendar({
        weekends: false,
        header: {
          left: 'prev,next today',
          center: 'title',
          right: 'month,basicWeek,basicDay'
        },
        displayEventTime: false,
        // open up the display form when a user clicks on an event
        eventClick: (calEvent: FC.EventObject, jsEvent: MouseEvent, view: FC.ViewObject): void => {
          (window as any).location = `${this.context.pageContext.web.absoluteUrl}\
  /Lists/${escape(this.properties.listName)}/DispForm.aspx?ID=${calEvent.id}`;
        },
        editable: true,
        timezone: "UTC",
        droppable: true, // this allows things to be dropped onto the calendar
        // update the end date when a user drags and drops an event 
        eventDrop: (event: FC.EventObject, delta: moment.Duration, revertFunc: Function): void => {
          this.updateTask(event.id, <moment.Moment>event.start, <moment.Moment>event.end);
        },
        // put the events on the calendar 
        events: (start: moment.Moment, end: moment.Moment, timezone: string, callback: Function): void => {
          const startDate: string = start.format('YYYY-MM-DD');
          const endDate: string = end.format('YYYY-MM-DD');

          const restQuery: string = `/_api/Web/Lists/GetByTitle('${escape(this.properties.listName)}')/items?$select=ID,Title,\
  Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
  $filter=((DueDate ge '${startDate}' and DueDate le '${endDate}')or(StartDate ge '${startDate}' and StartDate le '${endDate}'))`;

          $.ajax({
            url: this.context.pageContext.web.absoluteUrl + restQuery,
            type: "GET",
            dataType: "json",
            headers: {
              Accept: "application/json;odata=nometadata"
            }
          })
            .done((data: { value: ITask[] }, textStatus: string, jqXHR: JQueryXHR): void => {
              let personColors: { [person: string]: string; } = {};
              let colorNo: number = 0;

              const events: FC.EventObject[] = data.value.map((task: ITask): FC.EventObject => {
                const assignedTo: string = task.AssignedTo.map((person: { Title: string }): string => {
                  return person.Title;
                }).join(', ');

                let color: string = personColors[assignedTo];
                if (!color) {
                  color = this.colors[colorNo++];
                  personColors[assignedTo] = color;
                }
                if (colorNo >= this.colors.length) {
                  colorNo = 0;
                }

                return {
                  title: `${task.Title} - ${assignedTo}`,
                  id: task.ID,
                  // specify the background color and border color can also create a class and use className parameter
                  color: color,
                  start: moment.utc(task.StartDate).add("1", "days"),
                  // add one day to end date so that calendar properly shows event ending on that day
                  end: moment.utc(task.DueDate).add("1", "days")
                };
              });

              callback(events);
            });
        }
      });
    }

    private updateTask(id: number, startDate: moment.Moment, dueDate: moment.Moment): void {
      // subtract the previously added day to the date to store correct date
      const sDate: string = moment.utc(startDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
        startDate.format("hh:mm") + ":00Z";
      if (!dueDate) {
        dueDate = startDate;
      }
      const dDate: string = moment.utc(dueDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
        dueDate.format("hh:mm") + ":00Z";

      $.ajax({
        url: this.context.pageContext.web.absoluteUrl + '/_api/contextinfo',
        type: 'POST',
        headers: {
          'Accept': 'application/json;odata=nometadata'
        }
      })
        .then((data: { FormDigestValue: string }, textStatus: string, jqXHR: JQueryXHR): JQueryXHR => {
          return $.ajax({
            url: `${this.context.pageContext.web.absoluteUrl}\
  /_api/Web/Lists/getByTitle('${escape(this.properties.listName)}')/Items(${id})`,
            type: 'POST',
            data: JSON.stringify({
              StartDate: sDate,
              DueDate: dDate,
            }),
            headers: {
              Accept: "application/json;odata=nometadata",
              "Content-Type": "application/json;odata=nometadata",
              "X-RequestDigest": data.FormDigestValue,
              "IF-MATCH": "*",
              "X-Http-Method": "PATCH"
            }
          });
        })
        .done((data: {}, textStatus: string, jqXHR: JQueryXHR): void => {
          alert("Update Successful");
        })
        .fail((jqXHR: JQueryXHR, textStatus: string, errorThrown: string): void => {
          alert("Update Failed");
        })
        .always((): void => {
          this.displayTasks();
        });
    }

    // ...
  }
  ```

  <br/>

  Die erste und offensichtlichste Änderung beim Umwandeln von einfachem JavaScript in TypeScript sind explizite Typen. Diese sind zwar nicht erforderlich, machen aber deutlich, welcher Typ von Daten an welcher Stelle erwartet wird. Jede Abweichung von dem angegebenen Vertrag wird von TypeScript sofort abgefangen, sodass Sie mögliche Probleme während der Entwicklung so schnell wie möglich entdecken können. Dies ist besonders hilfreich, wenn Sie mit AJAX-Antworten und deren Daten arbeiten.

  Eine weitere Änderung, die Sie vielleicht schon bemerkt haben, ist die Interpolation der TypeScript-Zeichenfolge. Mit der Zeichenfolgeninterpolation wird die dynamische Zeichenfolgenzusammensetzung vereinfacht und die Lesbarkeit des Codes erhöht. 
  
  Vergleichen Sie einfaches JavaScript:

  ```js
  var restQuery = "/_api/Web/Lists/GetByTitle('" + TASK_LIST + "')/items?$select=ID,Title,\
  Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
  $filter=((DueDate ge '" + startDate + "' and DueDate le '" + endDate + "')or(StartDate ge '" + startDate + "' and StartDate le '" + endDate + "'))";
  ```

  mit:

  ```ts
  const restQuery: string = `/_api/Web/Lists/GetByTitle('${escape(this.properties.listName)}')/items?$select=ID,Title,\
  Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
  $filter=((DueDate ge '${startDate}' and DueDate le '${endDate}')or(StartDate ge '${startDate}' and StartDate le '${endDate}'))`;
  ```

  Ein weiterer Vorteil der Verwendung der TypeScript-Zeichenfolgeninterpolation ist, dass Sie Anführungszeichen nicht mit Escapezeichen versehen müssen, was auch die Erstellung von REST-Abfragen vereinfacht.

3. Führen Sie in der Befehlszeile Folgendes aus, um zu überprüfen, dass alles wie erwartet funktioniert:

  ```sh
  gulp serve --nobrowser
  ```

4. Navigieren Sie zu der gehosteten Workbench, und fügen Sie das Webpart zum Zeichenbereich hinzu. Obwohl sich visuell nichts geändert hat, verwendet die neue Codebasis TypeScript und seine Typdefinitionen, um Sie bei der Verwaltung der Lösung zu unterstützen.

### <a name="replace-jquery-ajax-calls-with-sharepoint-framework-api"></a>Ersetzen von jQuery-AJAX-Aufrufen durch die SharePoint-Framework-API

Im Moment verwendet die Lösung jQuery-AJAX-Aufrufe, um mit der SharePoint-REST-API zu kommunizieren. Für normale GET-Anforderungen ist die jQuery-AJAX-API ebenso einfach wie die Verwendung des SharePoint-Framework-SPHttpClient. Der wirkliche Unterschied liegt bei der Ausführung von POST-Anforderungen wie der folgenden zur Aktualisierung des Ereignisses:

```ts
$.ajax({
  url: this.context.pageContext.web.absoluteUrl + '/_api/contextinfo',
  type: 'POST',
  headers: {
    'Accept': 'application/json;odata=nometadata'
  }
})
  .then((data: { FormDigestValue: string }, textStatus: string, jqXHR: JQueryXHR): JQueryXHR => {
    return $.ajax({
      url: `${this.context.pageContext.web.absoluteUrl}\
/_api/Web/Lists/getByTitle('${escape(this.properties.listName)}')/Items(${id})`,
      type: 'POST',
      data: JSON.stringify({
        StartDate: sDate,
        DueDate: dDate,
      }),
      headers: {
        Accept: "application/json;odata=nometadata",
        "Content-Type": "application/json;odata=nometadata",
        "X-RequestDigest": data.FormDigestValue,
        "IF-MATCH": "*",
        "X-Http-Method": "PATCH"
      }
    });
  })
  .done((data: {}, textStatus: string, jqXHR: JQueryXHR): void => {
    alert("Update Successful");
  })
  // ...
```

Da Sie ein Listenelement aktualisieren möchten, müssen Sie für SharePoint ein gültiges Anforderungs-Digest-Token bereitstellen. Dieses ist zwar auf klassischen Seiten verfügbar, jedoch nur für 3 Minuten gültig. Die sicherste Lösung besteht daher darin, dass Sie selbst ein gültiges Token abrufen, bevor Sie einen Aktualisierungsvorgang ausführen. Nachdem Sie das Anforderungs-Digest abgerufen haben, müssen Sie es den Anforderungsheadern der Update-Anforderung hinzufügen. Wenn Sie dies nicht tun, schlägt die Anforderung fehl.

SPHttpClient in SharePoint Framework vereinfacht die Kommunikation mit SharePoint, da er automatisch erkennt, ob es sich bei der Anforderung um eine POST-Anforderung handelt, die ein gültiges Anforderungs-Digest erfordert. Wenn dies der Fall ist, ruft der SPHttpClient dieses von SharePoint ab und fügt es der Anforderung hinzu. Die gleiche Anforderung würde im Vergleich dazu folgendermaßen aussehen, wenn sie mithilfe von SPHttpClient ausgestellt wird:

```ts
this.context.spHttpClient.post(`${this.context.pageContext.web.absoluteUrl}\
/_api/Web/Lists/getByTitle('${escape(this.properties.listName)}')/Items(${id})`, SPHttpClient.configurations.v1, {
  body: JSON.stringify({
    StartDate: sDate,
    DueDate: dDate,
  }),
  headers: {
    Accept: "application/json;odata=nometadata",
    "Content-Type": "application/json;odata=nometadata",
    "IF-MATCH": "*",
    "X-Http-Method": "PATCH"
  }
})
.then((response: SPHttpClientResponse): void => {
  // ...
});
```

<br/>

1. Um die ursprünglichen jQuery-AJAX-Aufrufe durch die SharePoint-Framework-SPHttpClient-API zu ersetzen, öffnen Sie im Code-Editor die Datei **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts**. Fügen Sie der Liste der Importe Folgendes hinzu:

  ```ts
  import { SPHttpClient, SPHttpClientResponse } from '@microsoft/sp-http';
  ```

2. Ersetzen Sie in der **TasksCalendarWebPart**-Klasse die Methoden **displayTasks** und **updateTask** durch den folgenden Code:

  ```ts
  export default class TasksCalendarWebPart extends BaseClientSideWebPart<ITasksCalendarWebPartProps> {
    // ...

    private displayTasks(): void {
      $('#calendar').fullCalendar('destroy');
      $('#calendar').fullCalendar({
        weekends: false,
        header: {
          left: 'prev,next today',
          center: 'title',
          right: 'month,basicWeek,basicDay'
        },
        displayEventTime: false,
        // open up the display form when a user clicks on an event
        eventClick: (calEvent: FC.EventObject, jsEvent: MouseEvent, view: FC.ViewObject): void => {
          (window as any).location = `${this.context.pageContext.web.absoluteUrl}\
  /Lists/${escape(this.properties.listName)}/DispForm.aspx?ID=${calEvent.id}`;
        },
        editable: true,
        timezone: "UTC",
        droppable: true, // this allows things to be dropped onto the calendar
        // update the end date when a user drags and drops an event 
        eventDrop: (event: FC.EventObject, delta: moment.Duration, revertFunc: Function): void => {
          this.updateTask(event.id, <moment.Moment>event.start, <moment.Moment>event.end);
        },
        // put the events on the calendar 
        events: (start: moment.Moment, end: moment.Moment, timezone: string, callback: Function): void => {
          const startDate: string = start.format('YYYY-MM-DD');
          const endDate: string = end.format('YYYY-MM-DD');

          const restQuery: string = `/_api/Web/Lists/GetByTitle('${escape(this.properties.listName)}')/items?$select=ID,Title,\
  Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
  $filter=((DueDate ge '${startDate}' and DueDate le '${endDate}')or(StartDate ge '${startDate}' and StartDate le '${endDate}'))`;

          this.context.spHttpClient.get(this.context.pageContext.web.absoluteUrl + restQuery, SPHttpClient.configurations.v1, {
            headers: {
              'Accept': "application/json;odata.metadata=none"
            }
          })
            .then((response: SPHttpClientResponse): Promise<{ value: ITask[] }> => {
              return response.json();
            })
            .then((data: { value: ITask[] }): void => {
              let personColors: { [person: string]: string; } = {};
              let colorNo: number = 0;

              const events: FC.EventObject[] = data.value.map((task: ITask): FC.EventObject => {
                const assignedTo: string = task.AssignedTo.map((person: { Title: string }): string => {
                  return person.Title;
                }).join(', ');

                let color: string = personColors[assignedTo];
                if (!color) {
                  color = this.colors[colorNo++];
                  personColors[assignedTo] = color;
                }
                if (colorNo >= this.colors.length) {
                  colorNo = 0;
                }

                return {
                  title: `${task.Title} - ${assignedTo}`,
                  id: task.ID,
                  // specify the background color and border color can also create a class and use className paramter
                  color: color,
                  start: moment.utc(task.StartDate).add("1", "days"),
                  // add one day to end date so that calendar properly shows event ending on that day
                  end: moment.utc(task.DueDate).add("1", "days")
                };
              });

              callback(events);
            });
        }
      });
    }

    private updateTask(id: number, startDate: moment.Moment, dueDate: moment.Moment): void {
      // subtract the previously added day to the date to store correct date
      const sDate: string = moment.utc(startDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
        startDate.format("hh:mm") + ":00Z";
      if (!dueDate) {
        dueDate = startDate;
      }
      const dDate: string = moment.utc(dueDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
        dueDate.format("hh:mm") + ":00Z";

      this.context.spHttpClient.post(`${this.context.pageContext.web.absoluteUrl}\
  /_api/Web/Lists/getByTitle('${escape(this.properties.listName)}')/Items(${id})`, SPHttpClient.configurations.v1, {
          body: JSON.stringify({
            StartDate: sDate,
            DueDate: dDate,
          }),
          headers: {
            Accept: "application/json;odata=nometadata",
            "Content-Type": "application/json;odata=nometadata",
            "IF-MATCH": "*",
            "X-Http-Method": "PATCH"
          }
        })
        .then((response: SPHttpClientResponse): void => {
          if (response.ok) {
            alert("Update Successful");
          }
          else {
            alert("Update Failed");
          }

          this.displayTasks();
        });
    }

    // ...
  }
  ```

  <br/>

  > [!IMPORTANT] 
  > Wenn Sie bei Verwendung des SPHttpClient von SharePoint Framework Metadaten in den Antworten der SharePoint-REST-API unterdrücken, müssen Sie sicherstellen, dass Sie `application/json;odata.metadata=none` und nicht `application/json;odata=nometadata` als Wert des **Accept**-Headers verwenden. SPHttpClient verwendet OData 4.0 und erfordert den ersten Wert. Wenn Sie stattdessen letzteren verwenden, schlägt die Anforderung mit der Antwort **406 Not Acceptable** fehl.

3. Führen Sie in der Befehlszeile Folgendes aus, um zu überprüfen, dass alles wie erwartet funktioniert:

  ```sh
  gulp serve --nobrowser
  ```

4. Navigieren Sie zu der gehosteten Workbench, und fügen Sie das Webpart zum Zeichenbereich hinzu. Zwar gibt es immer noch keine visuellen Änderungen, aber der neue Code verwendet den SharePoint-Framework-SPHttpClient, was Ihren Code und die Verwaltung Ihre Lösung vereinfacht.
