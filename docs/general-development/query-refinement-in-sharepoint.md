---
title: Abfrageverfeinerung in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ec31782e-1bc5-4dc3-8df7-c29cd5f7f05c
ms.openlocfilehash: 4fcad16df080ba2bd6a8e6bea378e258559305e5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="query-refinement-in-sharepoint"></a>Abfrageeinschränkung in SharePoint
In diesem Artikel erfahren Sie, wie Sie die SharePoint-Features zur Abfrageeinschränkung bei der Arbeit mit Suchabfragen und Suchergebnissen programmgesteuert einsetzen können.
Mithilfe von Features zur Abfrageeinschränkung können Sie Endbenutzern passende Einschränkungsoptionen für ihre Abfragen bereitstellen. Die Features erlauben es Endbenutzern, Suchergebnisse anhand von spezifisch für die Ergebnisse berechneten Einschränkungsdaten detaillierter einzugrenzen. Die Einschränkungsdaten werden von der Indexkomponente berechnet, basierend auf aggregierten Statistiken zu den verwalteten Eigenschaften aller Ergebnisse einer Suchabfrage.
  
    
    

Die Abfrageeinschränkung wird typischerweise für Metadaten verwendet, die den indizierten Elementen zugeordnet sind, z. B. das Erstellungsdatum, der Autor und Personennamen, die in dem Element vorhanden sind. Mit den entsprechenden Einschränkungsoptionen können Sie eine Abfrage so präzisieren, dass nur Elemente dargestellt werden, die innerhalb einer bestimmten Zeitspanne erstellt wurden oder einen bestimmten Dateityp aufweisen.
## <a name="using-refiners-in-the-query-object-model"></a>Verwenden von Einschränkungen im Abfrageobjektmodell
<a name="SP15_Using_refiners"> </a>

An der Abfrageeinschränkung sind zwei Abfragen beteiligt:
  
    
    

1. Sie können anfordern, dass eine Reihe von Einschränkungen in den Suchergebnissen zurückgegeben wird, indem Sie  [eine Einschränkungsspezifikation](#SP15_Adding_refiners) zu der Abfrage des Benutzers hinzufügen. Eine Einschränkungsspezifikation ist die Eingabe für die [Refiners](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.Refiners.aspx) -Eigenschaft. Diese Abfrage wird gegen den Suchindex ausgeführt. Die Suchergebnisse bestehen aus relevanten Ergebnissen und Einschränkungsdaten.
    
  
2. Sie können die Einschränkungsdaten verwenden, um einen Drilldown in die Suchergebnisse auszuführen, indem Sie  [eine eingeschränkte Abfrage erstellen](#SP15_Creating_refined_query). Fügen Sie die  [RefinementFilters](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.RefinementFilters.aspx) -Eigenschaft zu der Abfrage hinzu, sodass die endgültigen Suchergebnisse sowohl den Anforderungen des ursprünglichen Abfragetexts des Benutzers als auch der ausgewählten Einschränkungsoption aus den Einschränkungsdaten entspricht.
    
  
In den folgenden Abschnitten werden diese Schritte ausführlich beschrieben un Codebeispiele bereitgestellt.
  
    
    

## <a name="adding-refiners-to-the-end-users-query-by-using-refiner-specs"></a>Hinzufügen von Einschränkungen zu der Abfrage des Benutzers mithilfe von Einschränkungsspezifikationen
<a name="SP15_Adding_refiners"> </a>

Sie können die angeforderten Abfrageeinschränkungen mithilfe der  [Refiners](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.Refiners.aspx) -Eigenschaft der [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.KeywordQuery.aspx) -Klasse angeben. Verwenden Sie die folgende Syntax, um die angeforderten Abfrageeinschränkungen anzugeben:
  
    
    
 `<refiner>[,<refiner>]*`
  
    
    

  
    
    
Jede  `refiner` weist das folgende Format auf:
  
    
    
 `<refiner-name>[(parameter=value[,parameter=value]*)]?`
  
    
    

  
    
    
Dabei gilt Folgendes:
  
    
    

-  `<refiner-name>` ist der Name der verwalteten Eigenschaft, die der Einschränkung zugeordnet ist. Diese verwaltete Eigenschaft muss im Suchschema auf [Refinable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedPropertyInfo.Refinable.aspx) oder [Sortable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedPropertyInfo.Sortable.aspx) festgelegt sein.
    
  
- Die optionale Liste von  `parameter=value`-Paaren gibt die nicht standardmäßigen Konfigurationswerte für die benannte Einschränkung an. Wenn ein Parameter für eine Einschränkung nicht innerhalb der Klammern aufgeführt ist, erhalten Sie von der Suchschemakonfiguration die Standardeinstellung. In Tabelle 1 sind mögliche Werte für die  `parameter=value`-Paare aufgeführt.
    
  

> **Hinweis:** Bei der Angabe von Einschränkungen müssen Sie zumindest einen Wert `refiner-name` angeben, also eine verwaltete Eigenschaft. 

**Beispiel**

`Refiners = "FileType"` 
 
 Sie können auch die erweiterte Syntax verwenden, um die Einschränkungseinstellungen anzupassen. 

 **Beispiel**

 `Refiners = "FileType,Write(discretize=manual/2013-01-01/2013-08-22/2013-09-15/2013-09-21/2013-09-22),companies"`
  
    
    


**Tabelle 1: Liste von Parametern für Einschränkungen**


|**Parameter**|**Beschreibung**|
|:-----|:-----|
| _deephits_ <br/>|Überschreibt die standardmäßige Anzahl von Treffern, die als Grundlage für die Berechnung der Einschränkung verwendet wird. Wenn Einschränkungen erstellt werden, werden alle Ergebnisse für die Abfrage ausgewertet. Bei Verwendung dieses Parameters wird in der Regel die Suchleistung verbessert.<br/>**Syntax** <br/>`deephits=<integer value>` <br/>**Beispiel** <br/>`price(deephits=1000)` <br/>**Hinweis:** Dieses Limit gilt innerhalb jeder Indexpartition. Da die Aggregation über alle Suchpartitionen hinweg durchgeführt wird, liegt die Anzahl der tatsächlich ausgewerteten Treffer höher als dieser Wert.           |
| _discretize_ <br/>| Legt benutzerdefinierte Intervalle (Einschränkungsbins) für numerische Einschränkungen fest. <br/>**Syntax** <br/>`discretize=manual/<threshold>/<threshold>[/<threshold>]*` <br/>**Beispiel** <br/>`write(discretize=manual/2013-01-01/2013-08-22/2013-09-15/2013-09-21/2013-09-22)` <br/>Das Attribut `<threshold>` gibt den Schwellenwert für die einzelnen Einschränkungsbins an. <br/>Es gibt ein Intervall für alle Elemente unterhalb des ersten angegebenen Schwellenwerts, ein Intervall zwischen jedem aufeinanderfolgenden Schwellenwert, und ein Intervall für alle Elemente überhalb dem letzten Schwellenwert. <br/>Für eine Einschränkung des Typs **DateTime** geben Sie den Schwellenwert gemäß einem der folgenden ISO 8601-kompatiblen Formate an:  <br/><ul><li><i>YYYY-MM-DD</i></li><li><i>YYYY-MM-DDThh:mm:ss</i></li><li><i>YYYY-MM-DDThh:mm:ss:Z</i></li></ul>Die Formatwerte geben Folgendes an: <ul><li><i>YYYY</i> - Vierziffrige Jahresangabe. Es werden nur vierziffrige Jahresangaben unterstützt.</li><li><i>MM</i> - Zweiziffriger Monat. 01 = Januar.</li><li><i>DD</i> - Zweiziffriger Tag des Monats (01 bis 31). </li><li><i>T</i> - Den Buchstaben „T". </li><li><i>hh</i> - Zweiziffrige Stundenangabe (00 bis 23). Die Angabe von A.M. oder P.M. ist nicht zulässig.</li><li><i>mm</i> - Zweiziffrige Minutenangabe (00 bis 59). </li><li><i>ss</i> - zweiziffrige Sekundenangabe (00 bis 59) </li></ul>**Wichtig:** Alle Datum/Uhrzeit-Werte müssen gemäß der Zeitzone UTC (Coordinated Universal Time, koordinierte Weltzeit) angegeben werden. Sie wird auch GMT (Greenwich Mean Time, mittlere Sonnenzeit am Nullmeridian) genannt. Der Bezeichner für die UTC-Zeitzone (ein nachstehendes „Z“) ist optional.          |
| _sort_ <br/>| Legt die Sortierreihenfolge der Bins in einer Einschränkung des Typs „String“ fest. <br/>**Syntax** <br/>`sort=<property>/<direction>` <br/>Die Attribute tun Folgendes: <ul><li><i>\<property\></i>: Gibt den Sortierungsalgorithmus an. Gültig sind die unten aufgeführten Werte (klein geschrieben). <ul><li>**frequency** - Sortiert nach Anzahl der Vorkommen innerhalb der Bins. </li><li>**name** - Anordnung nach Bezeichnungsname. </li><li>**number** - Behandelt die Zeichenfolgen als numerisch und verwendet die numerische Sortierung. Dieser Wert kann hilfreich sein, um diskrete Werte anzugeben, beispielsweise, um eine numerische Sortierung für einen Wert auszuführen, der in einer verwalteten Eigenschaft des Typs **String** enthalten ist. </li></ul></li><li><i>\<direction\></i>: Gibt die Sortierrichtung an. Gültig sind die unten aufgeführten Werte (klein geschrieben). <ul><li>**descending** </li><li>**ascending** </li></ul></li></ul>**Beispiel** <br/>`sort=name/ascending` <br/>**Standard:** frequency/descending  <br/>|
| _filter_ <br/>| Definiert, wie Bins innerhalb einer Einschränkung des Typs **String** gefiltert werden, bevor sie an den Client zurückgegeben werden. <br/>**Syntax** <br/> `filter=<bins>/<freq>/<prefix>[<levels>]` <br/>Die Attribute tun Folgendes: <ul><li><i>\<bins\></i>: Gibt an, wie viele Bins maximal zurückgegeben werden. <br/>Verwenden Sie dieses Attribut nach der Sortierung der Bins innerhalb der Einschränkung, um nachfolgende Bins abzuschneiden. Bei bins=10 werden gemäß des angegebenen Sortieralgorithmus beispielsweise nur die ersten 10 Bins zurückgegeben. </li><li><i>\<freq\></i>: Beschränkt die Anzahl der zurückgegebenen Bins. <br/>Verwenden Sie dieses Attribut, um Bins zu entfernen, die nur selten vorkommen. <i>freq</i>=2 bedeutet beispielsweise, dass nur die Bins mit 2 oder mehr Mitgliedern zurückgegeben werden.</li><li><i>\<prefix\></i>: Legt fest, dass nur Bins zurückgegeben werden, deren Name mit dem angegebenen Präfix beginnt. <br/>Wenn Sie das Platzhalterzeichen „\*“ setzen, wird der Filter namensunabhängig auf alle Bins angewendet. <br/>**Beispiel** <br/>`filter=30/2/*` </li><li><i>\<levels\></i>: Gibt die Taxonomieebenen an. <br/>Mithilfe dieses Attributs können Sie die Ausgabe hierarchischer Einschränkungen auf Basis von Taxonomieebenen filtern. Der Attributwert muss eine positive ganze Zahl <i>n</i> sein. Der **Standardwert** ist <i>n</i> = 0. Ist <i>n</i>\>0 gesetzt, werden nur Einschränkungseinträge zurückgegeben, deren Taxonomiepfad weniger als <i>n</i> Trennzeichen („/“) enthält. Wenn <i>n</i>=0 gesetzt ist, wird keine Ebenenfilterung angewendet. Das Ebenentrennzeichen ist der Schrägstrich („/“).  <br/>Bedenken Sie immer die Leistungseinbußen, die mit einem großen Taxonomienavigator einhergehen. Die Filterung wird als Teil der Ergebnisverarbeitung durchgeführt. </li></ul>**Hinweis:** Dieser Parameter wendet anwendungsspezifische ergebnisseitige Filterung an. Damit unterscheidet er sich vom Parameter „cutoff“, der aus Leistungsgründen Grenzwerte auf jede Indexpartition anwendet.          |
| _cutoff_ <br/>| Schränkt die Daten ein, die für tiefe Zeichenfolgeneinschränkungen übertragen und verarbeitet werden müssen. Sie können die Einschränkungen so konfigurieren, dass nur die relevantesten Werte (Bins) zurückgegeben werden.<br/>**Hinweis:** Die Filterung auf Basis des Parameters „cutoff“ wird innerhalb jeder Indexpartition durchgeführt. Damit unterscheidet sich dieser Parameter vom Parameter _filter_, der ausschließlich eine ergebnisseitige Filterung durchführt. Sie können die beiden Parameter miteinander kombinieren. <br/>**Syntax** <br/>`cutoff=<frequency>/<minbins>/<maxbins>` <br/>Die Attribute tun Folgendes: <ul><li><i>\<maxbins\></i>: Schränkt die Anzahl der Bins ein. <br/>Dieser Parameter schränkt die Anzahl eindeutiger Werte (Bins) ein, die für eine Einschränkung zurückgegeben werden. Dies ist die bevorzugte Methode, um die Suchleistung zu steigern, wenn Zeichenfolgeneinschränkungen mit einer großen Anzahl von Bins zurückgegeben werden. „0" bedeutet, dass der im Suchschema angegebene Standardwert verwendet wird.</li><li><i>\<frequency\></i>: Schränkt die Anzahl der Bins basierend auf der Häufigkeit ihres Vorkommens ein. <br/>Wenn die Anzahl der Vorkommnisse eines Einschränkungswerts in einem Resultset kleiner oder gleich dem Häufigkeitswert ist, wird der Einschränkungswert nicht zurückgegeben. „0" bedeutet, dass der Standardwert gemäß des Suchschemas verwendet wird.</li><li><i>\<minbins\></i>: Legt den Mindestwert für die häufigkeitsbasierte Einschränkung fest. <br/>Wenn die Anzahl eindeutiger Einschränkungswerte für die Abfrage niedriger als dieser Wert ist, wird keine Häufigkeitsabtrennung durchgeführt, und alle Einschränkungswerte werden von dieser Suchpartition zurückgegeben. Wenn eine Abtrennung nach Häufigkeit verwendet wird, kann dieser Parameter verwendet werden, um eine minimale Anzahl von eindeutigen Einschränkungswerten anzugeben, die zurückgegeben werden, unabhängig von der Anzahl von Vorkommnissen. Der Standarwert dieses Attributs ist „0"; dadurch wird angegeben, dass die Häufigkeitsabtrennung unabhängig von der Anzahl eindeutiger Navigatorwerte durchgeführt wird. „0" bedeutet, dass der im Indexschema angegebene Standardwert verwendet wird.</li></ul>**Hinweis:** Verwenden Sie die Parameter _\<frequency\>_ und _\<minbins\>_ mit Bedacht. Wir empfehlen Ihnen, nur den Parameter _\<maxbins\>_ zu verwenden.           |
   

### <a name="example-adding-refiners"></a>Beispiel: Hinzufügen von Einschränkungen
<a name="SP15_Example_adding_refiners"> </a>

Im folgenden CSOM-Beispiel wird gezeigt, wie drei Einschränkungen programmgesteuert angefordert werden: **FileType**, **Write** und **Companies**. **Write** stellt das Datum der letzten Änderung für das Element dar und verwendet die erweiterte Syntax, um Datums-/Uhrzeitbins mit fester Größe zurückzugeben.
  
    
    

```cs

using (var context = new ClientContext("http://<serverName>/<siteCollectionPath>"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home",
        Refiners = "FileType,Write(discretize=manual/2013-01-01/2013-08-22/2013-09-
            15/2013-09-21/2013-09-22),companies"
    };
    
    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    ResultTable relevantResultsTable = results.Value[0];
    ResultTable refinerResultsTable = results.Value[1];          
    Console.WriteLine(refinerResultsTable.RowCount + " refinement options:");
    foreach (var refinementOption in refinerResultsTable.ResultRows)
    {
        Console.WriteLine("RefinerName: '{0}' RefinementName: '{1}'
            RefinementValue: '{2}' RefinementToken: '{3}' RefinementCount: '{4}'", 
            refinementOption["RefinerName"],
            refinementOption["RefinementName"],
            refinementOption["RefinementValue"],
            refinementOption["RefinementToken"],
            refinementOption["RefinementCount"]
        );
    }
}
```


## <a name="understanding-the-refinement-data-in-the-search-result"></a>Verstehen der Einschränkungsdaten im Suchergebnis
<a name="SP15_Understanding_refinement_data"> </a>

Wenn Sie die Abfrageeinschränkung für eine verwaltete Eigenschaft in Ihrer Abfrage aktiviert haben, enthält das Abfrageergebnis Einschränkungsdaten, die in Einschränkungsbins unterteilt sind. Diese Daten befinden sich in der **RefinementResults**-Tabelle ( [RefinementResults](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KnownTableTypes.RefinementResults.aspx) ) innerhalb der [ResultTableCollection](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ResultTableCollection.aspx) . Ein Einschränkungsbin stellt einen bestimmten Wert oder Wertebereich für die verwaltete Eigenschaft dar. Die **RefinementResults**-Tabelle enthält eine Zeile pro Einschränkungsbin und enthält die Spalten, wie in Tabelle 2 angegeben.
  
    
    

**Tabelle 2: Für Einschränkungsbins zurückgegebene Daten**


|**Parameter**|**Beschreibung**|
|:-----|:-----|
|**RefinerName** <br/>|Der Name der Abfrageeinschränkung.  <br/>|
|**RefinementName** <br/>|Die Zeichenfolge, die das Einschränkungsbin darstellt. Diese Zeichenfolge wird in der Regel verwendet, wenn Einschränkungsoptionen für die Benutzer auf einer Suchergebnisseite präsentiert werden.  <br/>|
|**RefinementValue** <br/>|Eine implementierungsspezifische formatierte Zeichenfolge, die die Einschränkung darstellt. Diese Daten werden zum Debuggen zurückgegeben und sind normalerweise für den Client nicht erforderlich.  <br/>|
|**RefinementToken** <br/>|Eine Zeichenfolge, die das für **RefinerName** zu verwendende Einschränkungsbin darstellt, wenn Sie eine eingeschränkte Abfrage ausführen. <br/>|
|**RefinementCount** <br/>|Die Anzahl der Ergebnisse für dieses Einschränkungsbin. Diese Daten stellen die Anzahl von Elementen (einschließlich Duplikaten) im Suchergebnis mit einem Wert für die angegebene verwaltete Eigenschaft dar, der in dieses Einschränkungsbin fällt.  <br/>|
   

### <a name="example-refinement-data"></a>Beispiel: Einschränkungsdaten
<a name="SP15_Example_refinement_data"> </a>

Tabelle 3 unten enthält zwei Zeilen mit Einschränkungsdaten. Die erste Zeile enthält Einschränkungsdaten für indizierte Elemente, wobei der Dateityp HTML ist. Die zweite Zeile enthält Einschränkungsdaten für indizierte Elemente, wobei der Zeitpunkt der letzten Bearbeitung zwischen 21.09.2013 und 22.09.2013 liegt.
  
    
    

**Tabelle 3: Format und Inhalt der Einschränkungsdaten**


|**RefinerName**|**RefinementName**|**RefinementValue**|**RefinementToken**|**RefinementCount**|
|:-----|:-----|:-----|:-----|:-----|
|FileType  <br/>|HTML  <br/>|HTML  <br/>|"????68746d6c"  <br/>|50553  <br/>|
|Schreiben  <br/>|Von 2013-09-21T00:00:00Z bis 2013-09-22T00:00:00Z  <br/>|Von 2013-09-21T00:00:00Z bis 2013-09-22T00:00:00Z  <br/>|range(2013-09-21T00:00:00Z, 2013-09-22T00:00:00Z)  <br/>|37  <br/>|
   

## <a name="creating-a-refined-query"></a>Erstellen einer Einschränkungsabfrage
<a name="SP15_Creating_refined_query"> </a>

Ein Suchergebnis stellt Einschränkungsoptionen in der Form von Zeichenfolgenwerten oder Wertebereichen dar. Jeder Zeichenfolgenwert oder numerische Wertebereich wird als Einschränkungsbin bezeichnet, und jeder Einschränkungsbin weist einen zugewiesenen **RefinementToken**-Wert auf. Eine Einschränkungsoption ist einer verwalteten Eigenschaft zugeordnet, die vom **RefinerName**-Wert bereitgestellt wird.
  
    
    
Sowohl der Wert **RefinementToken** als auch der Wert **RefinerName** ist verkettet, sodass eine _refinement filter_-Zeichenfolge erstellt wird. Diese Zeichenfolge stellt einen Filter dar, der verwendet werden kann, um Suchergebnisse so einzuschränken, dass nur Elemente enthalten sind, bei denen eine verwaltete Eigenschaft einen Wert innerhalb eines Einschränkungsbin aufweist. Kurz ausgedrückt:
  
    
    
 `refinement filter = <RefinerName>:<RefinementToken>`
  
    
    
Sie können einen oder mehrere Einschränkungsfilter für eine eingeschränkte Abfrage angeben, indem Sie der  [RefinementFilters](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.RefinementFilters.aspx) -Eigenschaft der [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx) -Klasse Einschränkungsfilter hinzufügen. Mit mehreren Einschränkungsfiltern können Sie einen Drilldown über mehrere Stufen in Suchergebnisse bereitstellen und eine Einschränkung auf Eigenschaften mit mehreren Werten anwenden. Sie können beispielsweise die Abfrage auf Elemente mit zwei Autoren einschränken, von denen jeder von einem Einschränkungsbin dargestellt wird, aber Elemente ausschließen, die nur einen der Autoren enthalten.
  
    
    

### <a name="example-1-creating-a-refined-query-for-html-file-types"></a>Beispiel 1: Erstellen einer eingeschränkten Abfrage für Dateien des Typs HTML

Das folgende CSOM-Beispiel demonstriert, wie Sie programmgesteuert eine Einschränkung implementieren können, die die Suchergebnisse ausschließlich auf Dateien des Typs HTML eingrenzt. Wie bereits im Abschnitt [Beispiel: Einschränkungsdaten](#SP15_Example_refinement_data) erwähnt, ist in den zu dieser Einschränkungsoption gehörenden Einschränkungsdaten der Parameter **RefinerName** auf _Filetype_ gesetzt und der Parameter **RefinementToken** auf _"????68746d6c"_.
  
    
    

```cs

using (var context = new ClientContext("http://<serverName>/<siteCollectionPath>"))
{
    var query = new KeywordQuery(context)
    {        
        QueryText = "home"
    };
    
    query.RefinementFilters.Add("FileType:\\"????68746d6c\\"");
    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    ResultTable relevantResultsTable = results.Value[0];
    var resultCount = 1;
    foreach (var relevantResult in relevantResultsTable.ResultRows)
    {
        Console.WriteLine("Relevant result number {0} has file type {1}.", 
            resultCount, relevantResult["FileType"]);
            resultCount++;
    }
}
```


### <a name="example-2-creating-a-refined-query-by-using-previously-obtained-refinement-data"></a>Beispiel 2: Erstellen einer eingeschränkten Abfrage auf Basis von zuvor abgerufenen Einschränkungsdaten

Im folgenden CSOM-Beispiel wird veranschaulicht, wie eine Abfrage mit einer Einschränkungsspezifikation ausgeführt wird, um Einschränkungsdaten zu erstellen, die anschließend zum Durchführen einer Einschränkung verwendet werden. In diesem Beispiel wird der Prozess simuliert, bei dem ein Benutzer die erste Einschränkungsoption auswählt.
  
    
    

```cs

using (var context = new ClientContext("http://<serverName>/<siteCollectionPath>"))
{
    // Step 1: Run the query with refiner spec to provide refinement data in search result
    var query = new KeywordQuery(context)
    {
        QueryText = "home",
        Refiners = "FileType,Write(discretize=manual/2013-01-01/2013-08-22/
2013-09-15/2013-09-21/2013-09-22),companies"
    };
    
    Console.WriteLine("Run query '{0}' with refiner spec '{1}'.", query.QueryText,
query.Refiners);
    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);
    context.ExecuteQuery();

    // The query has been run and we can now look at the refinement data, to view the
    // refinement options
    ResultTable relevantResultsTable = results.Value[0];
    ResultTable refinerResultsTable = results.Value[1];
    Console.WriteLine("Got back {0} refinement options in the result:",
        refinerResultsTable.RowCount);
    
    foreach (var refinementOption in refinerResultsTable.ResultRows)
    {
        Console.WriteLine("RefinerName: '{0}' RefinementName: '{1}'
            RefinementValue: '{2}' RefinementToken: '{3}' RefinementCount: '{4}'",
            refinementOption["RefinerName"],
            refinementOption["RefinementName"],
            refinementOption["RefinementValue"],
            refinementOption["RefinementToken"],
            refinementOption["RefinementCount"]
        );
    }

    // Step 2: Run the refined query with refinement filter to drill down into 
    // the search results. This example uses the first refinement option in the refinement
    // data, if available. This simulates an end user selecting this refinement option.
    var refinementOptionArray = refinerResultsTable.ResultRows.ToArray();

    if (refinementOptionArray.Length > 0)
    {                         
        var firstRefinementOption = refinementOptionArray[6];x
        // Construct the refinement filter by concatenation
        var refinementFilter = firstRefinementOption["RefinerName"] + ":" +
            firstRefinementOption["RefinementToken"];
        var refinedQuery = new KeywordQuery(context)
        {
            QueryText = query.QueryText
        };
        refinedQuery.RefinementFilters.Add(refinementFilter);
        refinedQuery.SelectProperties.Add("FileType");
        refinedQuery.SelectProperties.Add("Write");
        refinedQuery.SelectProperties.Add("Companies");
        Console.WriteLine("Run query '{0}' with refinement filter '{1}'",            
            refinedQuery.QueryText, refinementFilter);
        var refinedResults = executor.ExecuteQuery(refinedQuery);
        context.ExecuteQuery();
        ResultTable refinedRelevantResultsTable = refinedResults.Value[0];
        var resultCount = 1;
        foreach (var relevantResult in refinedRelevantResultsTable.ResultRows)
        {
            Console.WriteLine("Relevant result number {0} has FileType='{1}',
                Write='{2}', Companies='{3}'", 
                resultCount, 
                relevantResult["FileType"],
                relevantResult["Write"],
                relevantResult["Companies"]
            );
            resultCount++;
        }
    }
}
```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15_Query_refinement_addresources"> </a>


-  [Konfigurieren der Eigenschaften des Einschränkungs-Webparts in SharePoint](http://technet.microsoft.com/de-DE/library/gg549985.aspx)
    
  
-  [Übersicht über das Suchschema in SharePoint](http://technet.microsoft.com/de-DE/library/jj219669%28office.15%29.aspx)
    
  

## <a name="see-also"></a>Weitere Artikel
<a name="SP15_Query_refinement_addresources"> </a>


#### <a name="other-resources"></a>Sonstige Ressourcen


  
    
    
 [Indexschema (FAST Search Server für SharePoint)](http://msdn.microsoft.com/library/3e1eed3f-8a6f-4911-9607-f1616e6a44f3%28Office.15%29.aspx)
  
    
    
 [Refiner-Element im Microsoft.Search.Query-Schema](http://msdn.microsoft.com/library/0512c17a-18e9-45e3-9061-9dba9cd45ef4%28Office.15%29.aspx)
