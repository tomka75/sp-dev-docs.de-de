---
title: "Beispiel-URI für Excel Services-REST-API"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4ebe1da2-9861-416f-bef1-4a62599efe2e
ms.openlocfilehash: 003f7097ee68e014f232b3e4817ab397202675d0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sample-uri-for-excel-services-rest-api"></a>Beispiel-URI für Excel Services-REST-API

Dieses Thema enthält Beispiel-URIs für die REST-Dienstbefehle (Representational State Transfer) in Excel Services.
  
    
    


> **Hinweis:** Die Excel Services-REST-API bezieht sich auf SharePoint und SharePoint 2016 (lokal). Für Office 365 Education-, Business- und Enterprise-Konten verwenden Sie die Excel-REST-APIs, die Bestandteil des [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
> )-Endpunkts sind.
  
    
    


## <a name="sample-uri-for-rest-commands-in-excel-services"></a>Beispiel-URI für die REST-Befehle in Excel Services

In den folgenden Beispielen verweist jeder URI auf eine Arbeitsmappe mit dem Namen  *sampleWorkbook.xlsx*  .
  
    
    

- Die Datei sampleWorkbook.xlsx enthält benannte Bereiche und Diagramme.
    
  
- Die Datei sampleWorkbook.xlsx wird in einer vertrauenswürdigen SharePoint-Dokumentbibliothek gespeichert. In diesem Beispiel lautet der Pfad zum Speicherort von sampleWorkbook.xlsx wie folgt:
    
```
  
http://<ServerName>/Docs/Documents/sampleWorkbook.xlsx
```


### <a name="sample-uri"></a>Beispiel-URI

Die ASPX-Seite für den REST-Dienst in Excel Services lautet wie folgt: 
  
    
    

```
http://<ServerName>/_vti_bin/ExcelRest.aspx

```

Es folgen Beispiel-URIs für den Zugriff auf die Arbeitsmappe sampleWorkbook.xlsx mithilfe des REST-Diensts in Excel Services.  
  
    
    

- Modell der obersten Ebene für die Arbeitsmappe (nur Bereiche und Diagramme im aktuellen Build):
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model

```

- Abrufen der vollständigen Arbeitsmappe:
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model?$format=workbook

```

- Zurückgeben eines Bereichs (Standard-HTML). Die folgenden beiden URI-Beispiele sind gleichwertig:
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1|G5')

```


```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1|G5')?$format=html
```

- Abrufen eines benannten Bereichs:
    
```
  http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('nameOfTheNamedRange')

```

- Zurückgeben eines ATOM-XML-Feeds:
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model?$format=atom

```

- Festlegen und Zurückgeben einer Zelle:
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1|G5')?Ranges('Sheet1!C3')=demo

```

- Abrufen eines Diagramms:
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart 1')

```

- Festlegen eines Werts und Abrufen eines Diagramms:
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart%201')?Ranges('Sheet1!A1')=5.5

```


