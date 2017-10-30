---
title: So Erstellen einer Mashup, die eine eingebettete Arbeitsmappe und Bing Maps verwendet.
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3cfeb8d7-84b8-4673-bc92-b176cba4ac3e
ms.openlocfilehash: 4fd4caf9c77aec37a888fd74cf819037e7372af1
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-a-mashup-that-uses-an-embedded-workbook-and-bing-maps"></a><span data-ttu-id="e3467-102">So: Erstellen einer Mashup, die eine eingebettete Arbeitsmappe und Bing Maps verwendet.</span><span class="sxs-lookup"><span data-stu-id="e3467-102">How to: Create a mashup that uses an embedded workbook and Bing Maps</span></span>

<span data-ttu-id="e3467-103">Dieser Artikel führt Sie durch eine leistungsfähige webbasierten Mashup, die eine eingebettete Excel-Arbeitsmappe und Bing Maps kombiniert.</span><span class="sxs-lookup"><span data-stu-id="e3467-103">This article walks you through a powerful Web-based mashup that combines an embedded Excel workbook and Bing Maps.</span></span>
  
    
    


## <a name="about-the-destination-explorer"></a><span data-ttu-id="e3467-104">Informationen zu "Ziel-Explorer"</span><span class="sxs-lookup"><span data-stu-id="e3467-104">About the "Destination Explorer"</span></span>

<span data-ttu-id="e3467-105">Der Ziel-Explorer ist ein Mashup, mit der Benutzer wählen Sie einen Bereich, einen Zieltyp (Ort oder Peters), ein bestimmtes Ziel innerhalb des Bereichs, und Lesen Sie Informationen zum Wetter oder die Anzahl der Besucher das Ziel nach Monat.</span><span class="sxs-lookup"><span data-stu-id="e3467-105">The Destination Explorer is a mashup that lets the user choose a region, a destination type (city or park), a specific destination within the region, and then see weather information or number of visitors to the destination by month.</span></span>
  
    
    
<span data-ttu-id="e3467-p101">Wenn der Benutzer über die Benutzeroberfläche verschiedene Optionen auswählt, wird JavaScript Verarbeiten der Ereignisse und die Änderungen an der Arbeitsmappe auf OneDrive verwendet. Die Arbeitsmappe neu berechnet, basierend auf der die Änderungen, und die Ziel-Explorer benachrichtigt, wenn der Vorgang abgeschlossen ist Rückruffunktionen verwenden. Je nachdem, was der Benutzer geändert die Ziel-Explorer möglicherweise entweder rufen Sie weitere Daten in der Arbeitsmappe Reisen, aktualisieren die Ansicht der Bing-Karte, ausblenden die Diagramme oder Austauschen des Diagramms, die derzeit angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="e3467-p101">When the user selects different options from the UI, JavaScript is used to process the events and pass the changes to the workbook on OneDrive. The workbook recalculates itself based on the changes and notifies the Destination Explorer when it is finished using callback functions. Depending on what the user changed, the Destination Explorer may either get more data from the Travel workbook, update the view of the Bing Map, hide the charts, or swap the chart that is currently showing.</span></span>
  
    
    
 <span data-ttu-id="e3467-109">**Die Arbeitsmappe"Reise"**</span><span class="sxs-lookup"><span data-stu-id="e3467-109">**The "Travel workbook"**</span></span>
  
    
    
<span data-ttu-id="e3467-110">Die Ziel-Explorer hängt stark von einer eingebetteten Arbeitsmappe, die alle Zielnamen, statistische Daten für Wetter und Besucher Zahlen und zwei Diagramme zum Anzeigen von Wetterdaten für monatliche und monatliche Besucher Daten enthält.</span><span class="sxs-lookup"><span data-stu-id="e3467-110">The Destination Explorer depends heavily on an embedded workbook that contains all the destination names, statistics for weather and visitor numbers, and two charts for displaying monthly weather data and monthly visitor data.</span></span>
  
    
    
 <span data-ttu-id="e3467-111">**JavaScript-API von Excel Services**</span><span class="sxs-lookup"><span data-stu-id="e3467-111">**Excel Services JavaScript API**</span></span>
  
    
    
<span data-ttu-id="e3467-p102">Der Mashup verwendet der Excel Services-JavaScript-API, die Arbeitsmappe einbetten und damit interagieren. Wenn der Excel Services-JavaScript-API verwenden möchten, müssen Sie nur am Quellspeicherort API im Code verweisen. Nachdem Sie Zugriff auf die Excel Services-JavaScript-API haben, können Sie programmgesteuert einbetten und Arbeiten mit einer Excel-Arbeitsmappe.</span><span class="sxs-lookup"><span data-stu-id="e3467-p102">The mashup uses the Excel Services JavaScript API to embed the workbook and to interact with it. To use the Excel Services JavaScript API, you only have to reference the API source location in your code. Once you have access to the Excel Services JavaScript API, you can programmatically embed and work with an Excel workbook.</span></span>
  
    
    
 <span data-ttu-id="e3467-115">**Bing Maps-JavaScript-APIs**</span><span class="sxs-lookup"><span data-stu-id="e3467-115">**Bing Maps JavaScript API**</span></span>
  
    
    
<span data-ttu-id="e3467-p103">Auch mithilfe der Mashup der Bing Maps-API die jeweiligen Speicherorten auf die Arbeitsmappe innerhalb einer Bing-Karte ausgewählt angezeigt. Ebenso wie eine beliebige andere JavaScript-Bibliothek Sie müssen, lediglich Bezug der API-Bibliothek im Code müssen, um zu einer Bing-Karte in Ihre Mashup aufnehmen möchten.</span><span class="sxs-lookup"><span data-stu-id="e3467-p103">The mashup also uses the Bing Maps API to display the locations selected on the workbook inside a Bing Map. Just like any other JavaScript library, all you have to do is reference the API library in your code in order to include a Bing Map in your mashup.</span></span>
  
    
    

## <a name="creating-the-destination-explorer-mashup"></a><span data-ttu-id="e3467-118">Erstellen der Mashup "Ziel-Explorer"</span><span class="sxs-lookup"><span data-stu-id="e3467-118">Creating the "Destination Explorer" Mashup</span></span>

<span data-ttu-id="e3467-119">Zum Erstellen dieses Mashup gefolgt wir 3 grundlegenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="e3467-119">To create this mashup, we followed 3 basic steps:</span></span>
  
    
    

1. <span data-ttu-id="e3467-p104">Speichern Sie die Arbeitsmappe auf OneDrive aus. Finden Sie weitere Informationen auf der Seite  [OneDrive](https://onedrive.live.com/about/en-us/) .</span><span class="sxs-lookup"><span data-stu-id="e3467-p104">Store the workbook on OneDrive. Find more information on the  [OneDrive](https://onedrive.live.com/about/en-us/) page.</span></span>
    
  
2. <span data-ttu-id="e3467-p105">Einbetten der Arbeitsmappe klicken Sie auf der Seite an. Finden Sie weitere Informationen zum Einbetten von Arbeitsmappen von OneDrive  [hier](http://office.microsoft.com/en-us/excel-help/share-it-embed-an-excel-workbook-on-your-blog-HA102029502.aspx?CTT=5&amp;origin=HA102775335).</span><span class="sxs-lookup"><span data-stu-id="e3467-p105">Embed the workbook on the page. Find more information on embedding workbooks from OneDrive  [here](http://office.microsoft.com/en-us/excel-help/share-it-embed-an-excel-workbook-on-your-blog-HA102029502.aspx?CTT=5&amp;origin=HA102775335).</span></span>
    
  
3. <span data-ttu-id="e3467-p106">Kombinieren Sie es nach oben mit Bing Maps. Dieser Schritt wird in den folgenden Abschnitten ausführlicher behandelt.</span><span class="sxs-lookup"><span data-stu-id="e3467-p106">Mash it up with Bing Maps. This step is covered in more detail in the following sections.</span></span>
    
  

  
    
    

## <a name="mashup-excel-services-and-bing-maps"></a><span data-ttu-id="e3467-126">Mashup Excel Services und Bing Maps</span><span class="sxs-lookup"><span data-stu-id="e3467-126">Mashup Excel Services and Bing Maps</span></span>

<span data-ttu-id="e3467-127">Nach dem Speichern der Arbeitsmappe in einen öffentlichen Ordner auf OneDrive und nach dem Einbetten der Arbeitsmappe auf der Hostwebseite wird die Bing Maps-Funktionalität mit Interaktionen auf die eingebettete Arbeitsmappe zum Erstellen der  *Ziel-Explorer*  Mashup kombiniert.</span><span class="sxs-lookup"><span data-stu-id="e3467-127">After storing the workbook in a public folder on OneDrive, and after embedding the workbook on the host web page, the Bing Maps functionality is combined with interactions on the embedded workbook to create the  *Destination Explorer*  Mashup.</span></span>
  
    
    
<span data-ttu-id="e3467-128">Die Integration geschieht in den folgenden 3 Schritten:</span><span class="sxs-lookup"><span data-stu-id="e3467-128">The integration happens in the following 3 steps:</span></span>
  
    
    

- <span data-ttu-id="e3467-129">Erstellen Sie die Seitenstruktur für die mashup</span><span class="sxs-lookup"><span data-stu-id="e3467-129">Create the page structure for the mashup</span></span>
    
  
- <span data-ttu-id="e3467-130">Initialisierung die eingebettete Arbeitsmappe Diagramme und der Bing-Karte</span><span class="sxs-lookup"><span data-stu-id="e3467-130">Initialize the embedded workbook charts and the Bing Map</span></span>
    
  
- <span data-ttu-id="e3467-131">Erstellen der entsprechenden Rückruffunktionen</span><span class="sxs-lookup"><span data-stu-id="e3467-131">Create the appropriate callback functions</span></span>
    
  

1. <span data-ttu-id="e3467-132">**Erstellen der Seitenstruktur für die mashup**</span><span class="sxs-lookup"><span data-stu-id="e3467-132">**Create the page structure for the mashup**</span></span>
    
    <span data-ttu-id="e3467-p107">Beim Laden der Seite, oder wenn der Benutzer den aktuellen Bereich oder in der Zieltyp ändert, wird ein HTML-select-Steuerelement auf der Webseite mit Daten aus der Arbeitsmappe Reisen aufgefüllt. Die Definition für dieses select-Steuerelement ( *Ziele*  ) wird **Codeausschnitt 1** angezeigt. **1 Codeausschnitt** zeigt die Definition für die anderen Hauptelemente auch auf der Seite: **ChartDiv**, **chartDiv2** und **MapDiv**. Div Diagrammelemente sind Container für die zwei Diagramme in der Arbeitsmappe Reisekosten definiert. Das Karte Div ist der Container für das Steuerelement Bing-Karte.</span><span class="sxs-lookup"><span data-stu-id="e3467-p107">An HTML select control on the web page is populated with data from the Travel workbook when the page loads or whenever the user changes the current region or the destination type. The definition for this select control ( *destinations*  ) is shown in **Snippet 1**. **Snippet 1** also shows the definition for the other key elements on the page: **chartDiv**, **chartDiv2**, and **mapDiv**. The chart div elements are containers for the two charts defined in the Travel workbook. The map div is the container for the Bing Map control.</span></span>
    
    <span data-ttu-id="e3467-138">**Codeausschnitt 1: Strukturierung der Webseite**</span><span class="sxs-lookup"><span data-stu-id="e3467-138">**Snippet 1: Structuring the web page**</span></span>
    


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

2. <span data-ttu-id="e3467-139">**Initialisierung die eingebettete Arbeitsmappe Diagramme und der Bing-Karte**</span><span class="sxs-lookup"><span data-stu-id="e3467-139">**Initialize the embedded workbook charts and the Bing Map**</span></span>
    
    <span data-ttu-id="e3467-p108">Im nächsten Schritt wird die Excel-Komponenten und der Bing-Karte Initialisierung, wenn die Seite geladen. Um eine eingebettete Excel-Arbeitsmappe programmgesteuert zugreifen zu können, müssen Sie nach einer Dateitoken darauf verweisen. Finden Sie unter  [http://msdn.microsoft.com/en-us/library/hh315812.aspx](http://msdn.microsoft.com/en-us/library/hh315812.aspx%28Office.15%29.aspx) Informationen zum Abrufen des entsprechenden Datei Tokens für die Arbeitsmappe ein.</span><span class="sxs-lookup"><span data-stu-id="e3467-p108">The next step is to initialize the Excel components and the Bing Map when the page loads. In order to access an embedded Excel workbook programmatically, you need to refer to it by a file token. See  [http://msdn.microsoft.com/en-us/library/hh315812.aspx](http://msdn.microsoft.com/en-us/library/hh315812.aspx%28Office.15%29.aspx) for information on how to get the appropriate file token for your workbook.</span></span>
    
    <span data-ttu-id="e3467-p109">Abgeschlossener Ausführung des Codes in **Codeausschnitt 2** drei Wichtigste Aufgaben im **Page_Load** -Ereignishandler aus. Zunächst wird hergestellt einen Verweis auf die Arbeitsmappe Reisen, um das Diagramm mit der Bezeichnung *Diagramm 1*  innerhalb des **ChartDiv** -Elements auf der Webseite anzuzeigen. Zweites, ruft sie eine einfache Funktion mit dem Namen **GetMap** Initialisierung der Bing-Karte. Wird kein zweiten Verweis auf die Arbeitsmappe Reisen zum Anzeigen des Diagramms mit dem Namen *Diagramm 2*  innerhalb des Elements **chartDiv2** erstellt.</span><span class="sxs-lookup"><span data-stu-id="e3467-p109">The code in **Snippet 2** completes three main tasks inside the **Page_Load** event handler. First, it establishes a reference to the Travel workbook to display the chart named *Chart 1*  inside the **chartDiv** element on the web page. Second, it calls a simple function named **GetMap** to initialize the Bing Map. Third, it creates a second reference to the Travel workbook to display the chart named *Chart 2*  inside the **chartDiv2** element.</span></span>
    
    <span data-ttu-id="e3467-147">**Codeausschnitt 2: Initialisierung der Seite**</span><span class="sxs-lookup"><span data-stu-id="e3467-147">**Snippet 2: Initializing the Page**</span></span>
    


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

3. <span data-ttu-id="e3467-148">**Erstellen Sie die entsprechenden Rückruffunktionen**</span><span class="sxs-lookup"><span data-stu-id="e3467-148">**Create the appropriate callback functions**</span></span>
    
    <span data-ttu-id="e3467-p110">Alle Aufrufe von Funktionen in der Excel Services-JavaScript-API nehmen in der Regel einen Rückruf als Parameter für die Funktion ein. Der Rückrufparameter ist der Name der Funktion in Ihrem JavaScript, die ausgeführt werden soll, wenn der Anruf an die JavaScript-API von Excel Services abgeschlossen ist. Sie können einen Rückruf, der in der Funktion **EwaControl.loadEwaAsync** in **Codeausschnitt 2** verwendet finden Sie unter:</span><span class="sxs-lookup"><span data-stu-id="e3467-p110">All calls to functions in the Excel Services JavaScript API usually take a callback as a parameter to the function. The callback parameter is the name of the function in your JavaScript that should be run when the call to the Excel Services JavaScript API completes. You can see a callback used in the **EwaControl.loadEwaAsync** function in **Snippet 2**:</span></span>
    


```
  
Ewa.EwaControl.loadEwaAsync(fileToken, "chartDiv", props, onEwaChartLoaded);
```


    The callback used here is **onEwaChartLoaded**. This launches the following chain of calls to the Excel Services JavaScript API and callbacks within the Destination Explorer. The callbacks used in this chain are:
    
  - <span data-ttu-id="e3467-p111">**onEwaChartLoaded()** - speichert diese Funktion einen Verweis auf das Excel Web Access-Steuerelement, das im Diagramm zugeordnet. Wenn das Steuerelement vorhanden sind, wird die Methode **getRangeA1Async()**, um den Bereich gesetzt, den Namen *OutputTopFiveDetails*  zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="e3467-p111">**onEwaChartLoaded()** - This function saves a reference to the Excel Web Access Control associated with the chart. After it has the control, it calls the method **getRangeA1Async()** to get the range represented by the name *OutputTopFiveDetails*  .</span></span>
    
  
  - <span data-ttu-id="e3467-154">**onGotDetailRange()** - gibt der Anruf an die **getRangeA1Async()** des Bereichs, nicht die Werte, damit Anrufe von dieser Rückruf die Methode **getValuesAsync()** zum Abrufen der Werte im Bereich zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="e3467-154">**onGotDetailRange()** - The call to **getRangeA1Async()** returns the range, not the values so this callback calls the method **getValuesAsync()** to get the values associated with the range.</span></span>
    
  
  - <span data-ttu-id="e3467-155">**onGotDetailValues()** - die Werte im Bereich zugeordnet werden in einer Variablen zur späteren Verwendung gespeichert und dann diese Methode ruft die folgenden Methoden innerhalb der Ziel-Explorer definiert:</span><span class="sxs-lookup"><span data-stu-id="e3467-155">**onGotDetailValues()** - The values associated with the range are stored in a variable for later use and then this method calls the following methods defined within the Destination Explorer:</span></span>
    
  - <span data-ttu-id="e3467-156">**loadDestinations()** - füllt das select-Element mit der Ziele im Bereich *OutputTopFiveDetails*</span><span class="sxs-lookup"><span data-stu-id="e3467-156">**loadDestinations()** - Populates the select element with the destinations within the range *OutputTopFiveDetails*</span></span> 
    
  
  - <span data-ttu-id="e3467-157">**updateMap()** - Aktualisierungen die Karte, falls erforderlich</span><span class="sxs-lookup"><span data-stu-id="e3467-157">**updateMap()** - Updates the map if necessary</span></span>
    
  
  - <span data-ttu-id="e3467-158">**updateChart()** - aktualisiert das Diagramm bei Bedarf</span><span class="sxs-lookup"><span data-stu-id="e3467-158">**updateChart()** - Updates the chart if necessary</span></span>
    
  

    <span data-ttu-id="e3467-p112">Der Zweck der Kette von Rückrufen in **Codeausschnitt 3** dargestellt ist zum Aktualisieren der Daten auf der HTML-Seite angezeigt. Es ist ein anderes Kette Rückruffunktionen verwendet, um Daten innerhalb der Arbeitsmappe Reisen ändern. Wenn Sie die Region in Europa von Nordamerika ändern, müssen verschiedene Funktionen beispielsweise geschehen, z. B. erneutes Auffüllen der Liste der Ziele, aktualisieren die Karte und die Diagramme ausblenden. Erneutes Auffüllen der Liste der Ziel wird als erstes, die erfolgen muss, und dies umfasst das Ändern von Daten in Excel. **3 Codeausschnitt** zeigt den Code für diese Aufgaben. Beachten Sie, dass die Funktion mit dem Namen **updateExcel()** und eine zugeordnete Rückruf mit dem Namen **onGotRange()** der AutoWert ändern Werte auf dem Arbeitsblatt Eingabe der Arbeitsmappe Reisen behandeln.</span><span class="sxs-lookup"><span data-stu-id="e3467-p112">The purpose of the chain of callbacks shown in **Snippet 3** is to update the data shown on the HTML page. There is another chain of callback functions used to modify data within the Travel workbook. For example, if you change the region from North America to Europe, several things need to happen such as repopulating the list of destinations, updating the map, and hiding the charts. Repopulating the list of destination is the first thing that needs to happen and this involves modifying data in Excel. **Snippet 3** shows the code for these tasks. Note that the function named **updateExcel()** and an associated callback named **onGotRange()** handle the chore of changing values on the Input worksheet of the Travel workbook.</span></span>
    
    <span data-ttu-id="e3467-165">**Codeausschnitt 3: Der Rückruf Kette zum Ändern von Eingaben in der Arbeitsmappe Reisen**</span><span class="sxs-lookup"><span data-stu-id="e3467-165">**Snippet 3: The callback chain for modifying inputs in the Travel workbook**</span></span>
    


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


## <a name="conclusion"></a><span data-ttu-id="e3467-166">Schlussbemerkung</span><span class="sxs-lookup"><span data-stu-id="e3467-166">Conclusion</span></span>
<span data-ttu-id="e3467-167"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e3467-167"></span></span>

<span data-ttu-id="e3467-168">Diese exemplarische Vorgehensweise bietet ein Beispiel für wie Web-Entwickler leistungsfähigen, interaktiven Mashups mithilfe von Excel Services und andere Technologien erstellen können.</span><span class="sxs-lookup"><span data-stu-id="e3467-168">This walkthrough gives an example of how web developers can create rich, interactive mashups using Excel Services and other technologies.</span></span> 
  
    
    

