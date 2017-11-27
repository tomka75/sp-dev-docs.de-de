---
title: Erstellen einer Mashup, die eine eingebettete Arbeitsmappe und Bing Maps verwendet
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3cfeb8d7-84b8-4673-bc92-b176cba4ac3e
ms.openlocfilehash: 3ffda7629e52045086e8dcd45e97c959058d7951
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="create-a-mashup-that-uses-an-embedded-workbook-and-bing-maps"></a>Erstellen einer Mashup, die eine eingebettete Arbeitsmappe und Bing Maps verwendet

Dieser Artikel führt Sie durch eine leistungsfähige webbasierten Mashup, die eine eingebettete Excel-Arbeitsmappe und Bing Maps kombiniert.
  
    
    


## <a name="about-the-destination-explorer"></a>Informationen zu "Ziel-Explorer"

Der Ziel-Explorer ist ein Mashup, mit der Benutzer wählen Sie einen Bereich, einen Zieltyp (Ort oder Peters), ein bestimmtes Ziel innerhalb des Bereichs, und Lesen Sie Informationen zum Wetter oder die Anzahl der Besucher das Ziel nach Monat.
  
    
    
Wenn der Benutzer über die Benutzeroberfläche verschiedene Optionen auswählt, wird JavaScript Verarbeiten der Ereignisse und die Änderungen an der Arbeitsmappe auf OneDrive verwendet. Die Arbeitsmappe neu berechnet, basierend auf der die Änderungen, und die Ziel-Explorer benachrichtigt, wenn der Vorgang abgeschlossen ist Rückruffunktionen verwenden. Je nachdem, was der Benutzer geändert die Ziel-Explorer möglicherweise entweder rufen Sie weitere Daten in der Arbeitsmappe Reisen, aktualisieren die Ansicht der Bing-Karte, ausblenden die Diagramme oder Austauschen des Diagramms, die derzeit angezeigt wird.
  
    
    
 **Die Arbeitsmappe"Reise"**
  
    
    
Die Ziel-Explorer hängt stark von einer eingebetteten Arbeitsmappe, die alle Zielnamen, statistische Daten für Wetter und Besucher Zahlen und zwei Diagramme zum Anzeigen von Wetterdaten für monatliche und monatliche Besucher Daten enthält.
  
    
    
 **JavaScript-API von Excel Services**
  
    
    
Der Mashup verwendet der Excel Services-JavaScript-API, die Arbeitsmappe einbetten und damit interagieren. Wenn der Excel Services-JavaScript-API verwenden möchten, müssen Sie nur am Quellspeicherort API im Code verweisen. Nachdem Sie Zugriff auf die Excel Services-JavaScript-API haben, können Sie programmgesteuert einbetten und Arbeiten mit einer Excel-Arbeitsmappe.
  
    
    
 **Bing Maps-JavaScript-APIs**
  
    
    
Auch mithilfe der Mashup der Bing Maps-API die jeweiligen Speicherorten auf die Arbeitsmappe innerhalb einer Bing-Karte ausgewählt angezeigt. Ebenso wie eine beliebige andere JavaScript-Bibliothek Sie müssen, lediglich Bezug der API-Bibliothek im Code müssen, um zu einer Bing-Karte in Ihre Mashup aufnehmen möchten.
  
    
    

## <a name="creating-the-destination-explorer-mashup"></a>Erstellen der Mashup "Ziel-Explorer"

Zum Erstellen dieses Mashup gefolgt wir 3 grundlegenden Schritte aus:
  
    
    

1. Speichern Sie die Arbeitsmappe auf OneDrive aus. Finden Sie weitere Informationen auf der Seite  [OneDrive](https://onedrive.live.com/about/en-us/) .
    
  
2. Einbetten der Arbeitsmappe klicken Sie auf der Seite an. Finden Sie weitere Informationen zum Einbetten von Arbeitsmappen von OneDrive  [hier](http://office.microsoft.com/en-us/excel-help/share-it-embed-an-excel-workbook-on-your-blog-HA102029502.aspx?CTT=5&amp;origin=HA102775335).
    
  
3. Kombinieren Sie es nach oben mit Bing Maps. Dieser Schritt wird in den folgenden Abschnitten ausführlicher behandelt.
    
  

  
    
    

## <a name="mashup-excel-services-and-bing-maps"></a>Mashup Excel Services und Bing Maps

Nach dem Speichern der Arbeitsmappe in einen öffentlichen Ordner auf OneDrive und nach dem Einbetten der Arbeitsmappe auf der Hostwebseite wird die Bing Maps-Funktionalität mit Interaktionen auf die eingebettete Arbeitsmappe zum Erstellen der  *Ziel-Explorer*  Mashup kombiniert.
  
    
    
Die Integration geschieht in den folgenden 3 Schritten:
  
    
    

- Erstellen Sie die Seitenstruktur für die mashup
    
  
- Initialisierung die eingebettete Arbeitsmappe Diagramme und der Bing-Karte
    
  
- Erstellen der entsprechenden Rückruffunktionen
    
  

1. **Erstellen der Seitenstruktur für die mashup**
    
    Beim Laden der Seite, oder wenn der Benutzer den aktuellen Bereich oder in der Zieltyp ändert, wird ein HTML-select-Steuerelement auf der Webseite mit Daten aus der Arbeitsmappe Reisen aufgefüllt. Die Definition für dieses select-Steuerelement ( *Ziele*  ) wird **Codeausschnitt 1** angezeigt. **1 Codeausschnitt** zeigt die Definition für die anderen Hauptelemente auch auf der Seite: **ChartDiv**, **chartDiv2** und **MapDiv**. Div Diagrammelemente sind Container für die zwei Diagramme in der Arbeitsmappe Reisekosten definiert. Das Karte Div ist der Container für das Steuerelement Bing-Karte.
    
    **Codeausschnitt 1: Strukturierung der Webseite**
    


```HTML
  
<!-- HTML omitted for brevity -->
    <select id="destinations" style="width: 150px" name="destinations"
      onchange="onDestinationChange()">
    </select>
    <!-- HTML omitted for brevity -->
    <div id="chartDiv" style="width: 483px; height: 318px"></div>
    <div id="chartDiv2" style="width: 483px; height: 318px; display: none"></div>
    <!-- HTML omitted for brevity -->
    <div id="mapDiv" style="position:relative; width:693px; height:400px;"></div>
    <!-- HTML omitted for brevity -->

```

2. **Initialisierung die eingebettete Arbeitsmappe Diagramme und der Bing-Karte**
    
    Im nächsten Schritt wird die Excel-Komponenten und der Bing-Karte Initialisierung, wenn die Seite geladen. Um eine eingebettete Excel-Arbeitsmappe programmgesteuert zugreifen zu können, müssen Sie nach einer Dateitoken darauf verweisen. Finden Sie unter  [http://msdn.microsoft.com/en-us/library/hh315812.aspx](http://msdn.microsoft.com/en-us/library/hh315812.aspx%28Office.15%29.aspx) Informationen zum Abrufen des entsprechenden Datei Tokens für die Arbeitsmappe ein.
    
    Abgeschlossener Ausführung des Codes in **Codeausschnitt 2** drei Wichtigste Aufgaben im **Page_Load** -Ereignishandler aus. Zunächst wird hergestellt einen Verweis auf die Arbeitsmappe Reisen, um das Diagramm mit der Bezeichnung *Diagramm 1*  innerhalb des **ChartDiv** -Elements auf der Webseite anzuzeigen. Zweites, ruft sie eine einfache Funktion mit dem Namen **GetMap** Initialisierung der Bing-Karte. Wird kein zweiten Verweis auf die Arbeitsmappe Reisen zum Anzeigen des Diagramms mit dem Namen *Diagramm 2*  innerhalb des Elements **chartDiv2** erstellt.
    
    **Codeausschnitt 2: Initialisierung der Seite**
    


```
  
// Use this file token to reference your OneDrive hosted workbook in Excel's APIs
    var fileToken = "TOKEN TO YOUR WORKBOOK GOES HERE";
    var map;
    var ewaChart = null;
    var ewaChart2 = null;
  
    // Set the page event handlers for onload and unload.
    if (window.attachEvent) {
    window.attachEvent("onload", Page_Load);
    }
    else {
    // For some browsers window.attachEvent does not exist.
    window.addEventListener("DOMContentLoaded", Page_Load, false);
    }
  
    hideCharts();
     
    // Page load event handler
    function Page_Load() {
     
    // Load Excel Chart
    var props = {
    item: "Chart 1",
    uiOptions: {
    showParametersTaskPane: false
    },
    interactivityOptions: {
    allowTypingAndFormulaEntry: true,
    allowParameterModification: false,
    allowSorting: false,
    allowFiltering: false,
    allowPivotTableInteractivity: false
    }
    };
    Ewa.EwaControl.loadEwaAsync(fileToken, "chartDiv", props, onEwaChartLoaded);
     
    // Load the Bing map
    GetMap();

    // Load the 2nd Excel Chart
    var props = {
    item: "Chart 2",
    uiOptions: {
    showParametersTaskPane: false
    },
    interactivityOptions: {
    allowTypingAndFormulaEntry: true,
    allowParameterModification: false,
    allowSorting: false,
    allowFiltering: false,
    allowPivotTableInteractivity: false
    }
    };
    Ewa.EwaControl.loadEwaAsync(fileToken, "chartDiv2", props, onEwaChart2Loaded);
    }
     
    // Setup the Bing Map's initial view
    function GetMap() {
     
    map = new Microsoft.Maps.Map(document.getElementById("mapDiv"),
    { credentials: "YOUR CREDENTIALS",
    center: new Microsoft.Maps.Location(37.2802459560, -112.738963),
    mapTypeId: Microsoft.Maps.MapTypeId.road,
    zoom: 3 });

```

3. **Erstellen Sie die entsprechenden Rückruffunktionen**
    
    Alle Aufrufe von Funktionen in der Excel Services-JavaScript-API nehmen in der Regel einen Rückruf als Parameter für die Funktion ein. Der Rückrufparameter ist der Name der Funktion in Ihrem JavaScript, die ausgeführt werden soll, wenn der Anruf an die JavaScript-API von Excel Services abgeschlossen ist. Sie können einen Rückruf, der in der Funktion **EwaControl.loadEwaAsync** in **Codeausschnitt 2** verwendet finden Sie unter:
    


```
  
Ewa.EwaControl.loadEwaAsync(fileToken, "chartDiv", props, onEwaChartLoaded);
```


    The callback used here is **onEwaChartLoaded**. This launches the following chain of calls to the Excel Services JavaScript API and callbacks within the Destination Explorer. The callbacks used in this chain are:
    
  - **onEwaChartLoaded()** - speichert diese Funktion einen Verweis auf das Excel Web Access-Steuerelement, das im Diagramm zugeordnet. Wenn das Steuerelement vorhanden sind, wird die Methode **getRangeA1Async()**, um den Bereich gesetzt, den Namen *OutputTopFiveDetails*  zu erhalten.
    
  
  - **onGotDetailRange()** - gibt der Anruf an die **getRangeA1Async()** des Bereichs, nicht die Werte, damit Anrufe von dieser Rückruf die Methode **getValuesAsync()** zum Abrufen der Werte im Bereich zugeordnet.
    
  
  - **onGotDetailValues()** - die Werte im Bereich zugeordnet werden in einer Variablen zur späteren Verwendung gespeichert und dann diese Methode ruft die folgenden Methoden innerhalb der Ziel-Explorer definiert:
    
  - **loadDestinations()** - füllt das select-Element mit der Ziele im Bereich *OutputTopFiveDetails* 
    
  
  - **updateMap()** - Aktualisierungen die Karte, falls erforderlich
    
  
  - **updateChart()** - aktualisiert das Diagramm bei Bedarf
    
  

    Der Zweck der Kette von Rückrufen in **Codeausschnitt 3** dargestellt ist zum Aktualisieren der Daten auf der HTML-Seite angezeigt. Es ist ein anderes Kette Rückruffunktionen verwendet, um Daten innerhalb der Arbeitsmappe Reisen ändern. Wenn Sie die Region in Europa von Nordamerika ändern, müssen verschiedene Funktionen beispielsweise geschehen, z. B. erneutes Auffüllen der Liste der Ziele, aktualisieren die Karte und die Diagramme ausblenden. Erneutes Auffüllen der Liste der Ziel wird als erstes, die erfolgen muss, und dies umfasst das Ändern von Daten in Excel. **3 Codeausschnitt** zeigt den Code für diese Aufgaben. Beachten Sie, dass die Funktion mit dem Namen **updateExcel()** und eine zugeordnete Rückruf mit dem Namen **onGotRange()** der AutoWert ändern Werte auf dem Arbeitsblatt Eingabe der Arbeitsmappe Reisen behandeln.
    
    **Codeausschnitt 3: Der Rückruf Kette zum Ändern von Eingaben in der Arbeitsmappe Reisen**
    


```
  // Event handler called when user selects a different region.
    function onRegionChange() {
    currentDestination = '';
    var e = document.getElementById("regions");
    currentRegion = e.options[e.selectedIndex].text;
    updateExcel();
    }
     
    // Event handler called when user selects a different destination.
    function onDestinationChange() {
    var select = document.getElementById('destinations');
    var i = select.selectedIndex;
    currentDestination = select.options[i].text;
    updateChart();
    updateMap(false);
    }
    // Event handler called when user selects a different destination type.
    function onTypeChange(type) {
    currentDestination = '';
    currentDestinationType = type;
    updateExcel();
    }
     
    // Called from onTypeChange and onRegionChange when user selects a different destination type or region
    function updateExcel() {
    ewaChart.getActiveWorkbook().getRangeA1Async("Input!Inputs", onGotRange, 0);
    ewaChart2.getActiveWorkbook().getRangeA1Async("Input!Inputs", onGotRange, 1);
    }
     
    // Callback - called from updateExcel - sets input values according to user selections
    function onGotRange(result) {
    var range = result.getReturnValue();
    var values = new Array(2);
    values[0] = new Array(1);
    values[0][0] = currentRegion;
    values[1] = new Array(1);
    values[1][0] = currentDestinationType;
    range.setValuesAsync(values, null, null);
     
    // Initiate process of refreshing the script variable detailRangeValues
    if (result.getUserContext() == 0)
    ewaChart.getActiveWorkbook().getRangeA1Async("Output!OutputTopFiveDetails", onGotDetailRange, null);
    }

```


## <a name="conclusion"></a>Schlussbemerkung
<a name="bk_addresources"> </a>

Diese exemplarische Vorgehensweise bietet ein Beispiel für wie Web-Entwickler leistungsfähigen, interaktiven Mashups mithilfe von Excel Services und andere Technologien erstellen können. 
  
    
    

