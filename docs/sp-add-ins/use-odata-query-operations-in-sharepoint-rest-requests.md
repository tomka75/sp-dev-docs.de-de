---
title: "Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: a0cd291475b492183a57de1db2a9272154fea3f4
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="use-odata-query-operations-in-sharepoint-rest-requests"></a>Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen
Hier erfahren Sie, wie Sie eine Reihe von OData-Abfragezeichenfolgeoperatoren verwenden, um die vom SharePoint REST-Dienst angeforderten Daten auszuwählen, zu filtern und zu ordnen. 
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).
 

 **Bevor Sie beginnen**
 

-  [Grundlegendes zum SharePoint REST-Dienst](get-to-know-the-sharepoint-rest-service.md)
    
 
-  [Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur](navigate-the-sharepoint-data-structure-represented-in-the-rest-service.md)
    
 
-  [Ermitteln von URIs von SharePoint REST-Dienstendpunkten](determine-sharepoint-rest-service-endpoint-uris.md)
    
 
Der SharePoint REST-Dienst unterstütz eine Reihe von OData-Abfragezeichenfolgeoperatoren, mit denen SIe die angeforderten Daten auswählen, filtern und ordnen können.
 

 **Tipp**  Der SharePoint Online-REST-Dienst (und der Dienst von SharePoint 2016 (lokal) und höher) unterstützt die Kombination mehrerer Anforderungen in einem einzelnen Dienstaufruf mithilfe der OData-Abfrageoption `$batch`. Einzelheiten und Links zu Codebeispielen finden Sie unter [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis.md) (Erstellen von Batchanforderungen mit den REST-APIs).
 


## <a name="select-fields-to-return"></a>Auswählen der Felder, die zurückgegeben werden sollen

Verwenden Sie die Abfrageoption [$select](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#SelectSystemQueryOption), um anzugeben, welche Felder für eine bestimmte Liste, ein Listenelement oder ein anderes, durch eine Entitätenmenge dargestelltes SharePoint-Objekt zurückgegeben werden sollen. Sie können `$select=*` verwenden, um alle verfügbaren Felder zurückzugeben.
 

 

 **Hinweis**  Im Allgemeinen gibt der REST-Dienst standardmäßig alle verfügbaren Felder zurück, wenn Sie die Abfrageoption `$select` nicht angeben. Es kann jedoch manchmal vorkommen, dass einige SharePoint-Objekte Eigenschaften enthalten, deren Abruf äußerst ressourcenintensiv ist. Um die Leistung des REST-Dienstes zu optimieren, sind diese Eigenschaften in der Standardabfrage nicht enthalten und müssen explizit angefordert werden. Beispielsweise wird die Eigenschaft **SPWeb.EffectiveBasePermissions** nicht standardmäßig zurückgegeben und muss explizit mittels der Abfrageoption `$select` angefordert werden.
 

Darüber hinaus können Sie angeben, dass die Anforderung projizierte Felder aus anderen Listen und die Werte von Suchvorgängen zurückgeben soll. Geben Sie hierzu in den beiden Abfrageoptionen `$select` und `$expand` den Feldnamen an. Beispiel:
 

 
 `http://server/site/_api/web/lists('guid')/items?$select=Title,Products/Name&amp;$expand=Products/Name`
 

 
Massenerweiterung und die Auswahl damit zusammenhängender Elemente wird nicht unterstützt.
 

 

## <a name="select-items-to-return"></a>Auswählen der Elemente, die zurückgegeben werden sollen

Verwenden Sie die Abfrageoption [$filter](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#FilterSystemQueryOption), um auszuwählen, welche Elemente zurückgegeben werden sollen. Unter [OData query operators supported in the SharePoint REST service](#bk_supported) (Im SharePoint REST-Dienst unterstützte OData-Abfrageoperatoren) sind die Optionen und Funktionen zum Vergleich der Filterabfragen aufgeführt, die Sie im SharePoint REST-Dienst verwenden können.
 

 

## <a name="query-for-single-value-lookup-fields"></a>Abfrage für Einzelwert-Suchfelder

Einzelwert-Suchfelder werden beim SharePoint REST-Dienst als zwei separate Felder dargestellt: ein Feld für den tatsächlichen Feldwert und ein weiteres für den Feldnamen. Sie können Abfragen des Suchfeldwerts durchführen wie bei jedem anderen Feld dieses Datentyps. Wenn beispielsweise der Wert des Suchfelds eine Zeichenfolge ist, können Sie die Vergleichsoptionen für Zeichenfolgen in Ihrer Abfrage verwenden.
 

 

## <a name="query-for-users"></a>Abfrage von Benutzern

Beim SharePoint REST-Dienst werden die Benutzer durch ihren Anzeigennamen repräsentiert und nicht ihrem Alias oder ihrer Domäne\Alias-Kombination. Daher müssen Sie sich bei Benutzerabfragen nach den Anzeigenamen richten.
 

 

 **Hinweis**  Auf Mitgliedschaft basierende Benutzeranfragen werden nicht unterstützt. Der Operator **Current** zum Ausführen von Abfragen mithilfe der ID des aktuellen Benutzers wird nicht unterstützt.
 


## <a name="query-for-multi-value-lookup-fields-and-users"></a>Abfrage für Suchfelder und Benutzer mit mehreren Werten

Da Suchfelder mit mehreren Werten als eine Zeichenfolge mehrerer Werte zurückgegeben werden, ist es nicht möglich, sie abzufragen (z. B. wird das Äquivalent eines **Includes**-Elements oder **NotIncludes**-Elements nicht unterstützt).
 

 

## <a name="sort-returned-items"></a>Sortieren der zurückgegebenen Elemente

Verwenden Sie die Abfrageoption [$orderby](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#OrderBySystemQueryOption), um anzugeben, wie die Elemente bei der Rückgabe geordnet sein sollen. Geben Sie zum Sortieren nach mehreren Feldern eine durch Komma getrennte Liste der Felder an. Sie können auch angeben, ob die Elemente in aufsteigender oder absteigender Reihenfolge sortiert werden sollen. Fügen Sie Ihrer Abfrage dazu das Schlüsselwort **asc** oder **desc** an.
 

 

## <a name="page-through-returned-items"></a>Unterteilen der zurückgegebenen Elemente

Verwenden Sie die Abfrageoptionen  [$top](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#TopSystemQueryOption) und [$skiptoken](http://msdn.microsoft.com/library/dd942121.aspx), um eine Teilmenge von Elementen auszuwählen, die nicht von der Abfrage zurückgegeben werden sollen.
 

 

 **Hinweis** Die Abfrageoption „$skip“ funktioniert nicht bei Abfragen für SharePoint-Listenelemente.
 

Die Option  `$top` ermöglicht Ihnen, die ersten *n*  Elemente des Rückgabesatzes für die Rückgabe auszuwählen. Die folgende URI fordert beispielsweise an, dass nur die ersten zehn Elemente des potenziellen Rückgabesatzes tatsächlich zurückgegeben werden:
 

 
 `http://server/site/_api/web/lists('<guid>')/items$top=10`
 

 
Mit der Option „$skiptoken“ können Sie Elemente bis zum angegebenen Element überspringen und den Rest zurückgeben.
 

 
 `$skiptoken=Paged=TRUE&amp;p_ID=5`
 

 

 **Hinweis**  Berücksichtigen Sie bei diesen Abfrageoptionen, dass die Seitenverwaltung in OData Ordnungszahlen verwendet. Nehmen wir beispielsweise an, dass Sie eine Schaltfläche „nächste Seite“ für die Anzeige von SharePoint-Listenelementen implementieren. Mithilfe des REST-Diensts aktivieren Sie die Schaltfläche für die Rückgabe der Elemente 1 bis 20, dann 21 bis 40 usw., wenn darauf geklickt wird. Nehmen Sie jedoch an, dass ein anderer Benutzer die Elemente 4 und 18 zwischen den Klicks auf die Schaltfläche löscht. In diesem Fall wird die Positionierung der verbleibenden Elemente zurückgesetzt und beim Anzeigen der Elemente 21 bis 40 werden zwei Elemente übersprungen.
 


## <a name="odata-query-operators-supported-in-the-sharepoint-rest-service"></a>Vom SharePoint REST-Dienst unterstützte OData-Abfrageoperatoren
<a name="bk_supported"> </a>



|**Unterstützt**|**Nicht unterstützt**|
|:-----|:-----|
|**Numerische Vergleiche** Lt Le Gt Ge Eq Ne| Arithmetische Operatoren (Add, Sub, Mul, Div, Mod) Grundlegende mathematische Funktionen (round, floor, ceiling) |
|**String-Vergleiche** startsWith substringof Eq Ne| endsWith replace substring tolower toupper trim concat|
|**Datums- und Uhrzeitfunktionen** day() month() year() hour() minute() second()| Operator „DateTimeRangesOverlap“: Abfrage, ob Datum-Zeit in ein wiederkehrendes Datum-Zeit-Muster fällt|
Die untenstehende Abbildung zeigt unterstützte OData-Abfrageoptionen.
 

 

**Unterstützte OData-Abfrageoptionen**

 

 
![Abfrageoptionssyntax des SharePoint REST-Diensts](../images/SPF15Con_REST_queryOptionSyntax.png)
 

 

 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Grundlegendes zum SharePoint REST-Dienst](get-to-know-the-sharepoint-rest-service.md)
    
 
-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten](complete-basic-operations-using-sharepoint-rest-endpoints.md)
    
 
-  [Arbeiten mit Listen und Listenelementen unter Verwendung von REST](working-with-lists-and-list-items-with-rest.md)
    
 
-  [Arbeiten mit Ordnern und Dateien unter Verwendung von REST](working-with-folders-and-files-with-rest.md)
    
 
-  [Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur](navigate-the-sharepoint-data-structure-represented-in-the-rest-service.md)
    
 
-  [Ermitteln von URIs von SharePoint REST-Dienstendpunkten](determine-sharepoint-rest-service-endpoint-uris.md)
    
 
-  [REST-API-Referenz und Beispiele](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)
    
 

 

 
