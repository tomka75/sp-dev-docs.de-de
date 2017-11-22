---
title: Anfordern von Excel-Arbeitsmappendaten von SharePoint Server mithilfe von OData
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2f846e96-6c9e-4ed2-9602-4081ad0ab135
ms.openlocfilehash: 79e7a64b88e54105ad5ad846939836121621cc45
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="requesting-excel-workbook-data-from-sharepoint-server-using-odata"></a>Anfordern von Excel-Arbeitsmappendaten von SharePoint Server mithilfe von OData

> **Hinweis:** Die Excel Services-REST-API kann in lokalen Bereitstellungen von SharePoint und SharePoint 2016 verwendet werden. Für Konten in Office 365 Education, Office 365 Business und Office 356 Enterprise müssen Sie die Excel-REST-APIs verwenden, die in den [Microsoft Graph](http://graph.microsoft.io/de-DE/docs/api-reference/v1.0/resources/excel)-Endpunkt integriert sind.
  
    
    

OData verwendet URLs zum Anfordern von Informationen aus einer Ressource. Sie erstellen die URL auf eine bestimmte Weise Abfrageoptionen, die Informationen zurückgegeben, die Sie benötigen, verwenden. Die folgende URL zeigt, wie eine normale OData-Anforderung aussieht. http://contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1?$top=20
  
    
    

In diesem Beispiel für OData-Anforderung ist so strukturiert, dass es Ruft die ersten 20 Zeilen aus einer Tabelle mit dem Namen Tabelle1 in der Arbeitsmappe ProductSales.xlsx der im Ordner "Dokumente" auf dem Server contoso1 gespeichert wird. Die URL verwendet das System Abfrage Option **$top**, um die Anzahl der zurückzugebenden Zeilen angeben.Betrachtung der URL, können Sie die drei Komponentenstruktur anzeigen: der Dienst Stamm-URI; der Pfad der Ressource; und die Abfrageoptionen.
## <a name="service-root-uri"></a>Stamm-URI-Service

Der erste Teil der URL das Stammverzeichnis Service aufgerufen und bleibt gleich für jede OData-Anforderung, die Sie an eine SharePoint-Server mit Ausnahme der Name des Servers vornehmen. Sie enthält den Namen des SharePoint-Servers, auf dem die Arbeitsmappe gespeichert wird, und der Pfad, /_vti_bin/excelrest.aspx voranstellen, wie im folgenden Beispiel dargestellt.
  
    
    
http://contoso1/_vti_bin/ExcelRest.aspx
  
    
    

## <a name="resource-path"></a>Ressourcenpfad

Im zweite Teil der URL muss der Pfad zu der Excel-Arbeitsmappe und gibt an, dass dies ein OData-Anforderung ist.
  
    
    
/Documents/ProductSales.xlsx/OData
  
    
    

## <a name="system-query-options"></a>System-Abfrageoptionen

Der dritte Teil der URL wird Abfrageoptionen für die Anforderung. Abfrageoptionen immer beginnen mit einem Dollarzeichen ($) und am Ende des URIS als Abfrageparameter angefügt sind. Anforderung ist in diesem Beispiel wird für die ersten 20 Zeilen in der Tabelle mit dem Namen Tabelle1.
  
    
    
/ Table1? $top = 20
  
    
    
System-Abfrageoptionen bieten eine Möglichkeit zum Abrufen von bestimmter Daten aus einer Ressource. Die Excel Services OData-Implementierung unterstützt eine Reihe von Abfrageoptionen für wie im folgenden Abschnitt aufgeführt.
  
    
    

## <a name="system-query-options"></a>System-Abfrageoptionen
<a name="xlsSystemQueryOptions"> </a>

Die Excel Services-Implementierung der OData unterstützt eine Reihe von OData-System-Abfrage Standardoptionen. Diese Abfrageoptionen sind im Wesentlichen Anforderungen OData da Sie die Optionen zum angeben, welche Daten aus einer Ressource abgerufen werden soll. Die folgende Tabelle enthält die Abfrageoptionen System, die derzeit Excel Services-Implementierung von OData unterstützt.
  
    
    

**Tabelle 1: OData-Systemabfrageoptionen für Excel Services**


|**Systemabfrageoption**|**Beschreibung**|
|:-----|:-----|
|/\<tableName\>  <br/> |Gibt alle Zeilen der Tabelle angegeben durch \<tableName\>, wobei \<tableName\> ist der Name einer Tabelle in einer Excel-Arbeitsmappe, die die Zeilen enthält, die Sie abrufen möchten.  <br/> **Wichtig:** Eine OData-Abfrage dieses Formats gibt maximal 500 Zeilen zurück. Jeder 500-Zeilen-Satz entspricht einer Seite. Wenn Sie Zeilen auf weiteren Seiten in einer Tabelle mit mehr als 500 Zeilen abrufen möchten, müssen Sie die Abfrageoption **$skiptoken** verwenden (siehe unten).<br/>Das folgende Beispiel gibt alle Zeilen bis zur Zeile 500 in „Table1“ in der Arbeitsmappe „ProductSales.xlsx“ zurück.  <br/> |
|**$metadata** <br/> |Alle verfügbaren Tabellen und den Typ von Informationen für alle Zeilen zurückgegeben in den einzelnen Tabellen in der angegebenen Arbeitsmappe.  <br/> Das folgende Beispiel gibt die Tabellen und Typinformationen für die Tabellen in der Arbeitsmappe ProductSales.xlsx zurück.  <br/> http://contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/$metadata  <br/> |
|**$orderby** <br/> |Gibt die Zeilen in der angegebenen Tabelle, sortiert nach von **$orderby**angegebenen Wert zurück.  <br/> Das folgende Beispiel gibt alle Zeilen aus „Table1“ in der Arbeitsmappe „ProductSales.xlsx“ zurück, sortiert auf Basis der Spalte „Name“.  <br/> **Hinweis:** Der Standardwert für **$orderby** ist „ascending“.          http://contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1?$orderby=Name  <br/> |
|**$top** <br/> |Gibt zurück N Zeilen aus der Tabelle, wobei N eine Zahl, die den Wert des **$top**angegeben.  <br/> Das folgende Beispiel gibt die ersten 5 Zeilen from Tabelle1, sortiert nach der Spalte Name in der Arbeitsmappe ProductSales.xlsx.  <br/> http://contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1?$orderby=Name&amp;$top=5  <br/> |
|**$skip** <br/> |Überspringt N Zeilen, wobei N den Wert des **$skip**angegebene Nummer getestet werden, und gibt dann die restlichen Zeilen der Tabelle zurück.  <br/> Das folgende Beispiel gibt alle verbleibende Zeilen nach der fünften Zeile from Tabelle1 in der Arbeitsmappe ProductSales.xlsx zurück.  <br/> http://contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1?$skip=5  <br/> |
|**$skiptoken** <br/> |Der n-te Zeile, wobei N die Ordnungsposition Zeile durch den Wert des **$skiptoken**angegeben ist, sucht und gibt dann alle verbleibende Zeilen, beginnend bei Zeile N + 1 zurück. Die Auflistung ist nullbasiert, damit die zweite Zeile, beispielsweise durch $skiptoken angegebenen = 1.<br/> Das folgende Beispiel gibt alle verbleibende Zeilen nach der zweiten Zeile from Tabelle1 in der Arbeitsmappe ProductSales.xlsx zurück.  <br/> http://contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1?$skiptoken=1  <br/> Sie können auch die Abfrageoption **$skiptoken** verwenden, Zeilen in Seiten nach der ersten Seite aus einer Tabelle abrufen, die mehr als 500 Zeilen enthält. Im folgenden Beispiel wird veranschaulicht, die 500th Zeile abgerufen und aus einer Tabelle mit mehr als 500 Zeilen höher.<br/> http://contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1?$skiptoken=499  <br/> |
|**$filter** <br/> |Gibt die Teilmenge der Zeilen, die den Wert der **$filter**angegebenen Bedingungen erfüllen. Weitere Informationen zu den Operatoren und einen Satz von Funktionen, die Sie mit **$filter**verwenden können, finden Sie unter das OData-  [Dokumentation](http://www.odata.org/documentation/odata-version-2-0/uri-conventions/). <br/> Das folgende Beispiel gibt nur die Zeilen, wobei der Wert der Spalte Price größer als 100 ist.  <br/> http://Contoso1/_vti_bin/ExcelRest.aspx/Documents/productsales.xlsx/OData/Table1?$ Filter = Preis Gt 100  <br/> |
|**$format** <br/> |Das Atom-XML-Format ist der einzige unterstützte Wert und ist die Standardeinstellung für die Abfrageoption **$format**. <br/> |
|**$select** <br/> |Gibt die Entität, die durch **$select**angegebenen zurück.  <br/> Im folgende Beispiel werden die Spalte Name in der Arbeitsmappe ProductSales.xlsx from Tabelle1 markiert.  <br/> http://contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1?$select=Name  <br/> |
|**$inlinecount** <br/> | Gibt die Anzahl der Zeilen in der angegebenen Tabelle zurück. <br/>  $ **inlinecount** können nur 1 von 2 der folgenden Werte verwenden. <br/><ul><li>**allpages** - zurückgegeben Anzahl die für alle Zeilen in der Tabelle.</li><li>**none** - umfasst keine Anzahl der Zeilen in der Tabelle.</li></ul><br/>Im folgende Beispiel werden die Anzahl für die Gesamtanzahl der Zeilen in Tabelle1 in der ProductSales.xlsx Arbeitsmappe zurückgegeben. <br/>  http://contoso1/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1?$inlinecount=allpages <br/> |
   

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="xlsAdditionalResources"> </a>


-  [Verwenden von OData mit Excel Services-REST in SharePoint](using-odata-with-excel-services-rest-in-sharepoint.md)
    
  
-  [Was ist neu in Excel Services für Entwickler](http://msdn.microsoft.com/library/09e96c8b-cb55-4fd1-a797-b50fbf0f9296.aspx)
    
  
-  [Dokumentation für OData-Spezifikation](http://www.odata.org)
    
  
