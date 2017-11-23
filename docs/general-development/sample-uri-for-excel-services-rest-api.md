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
# <a name="sample-uri-for-excel-services-rest-api"></a><span data-ttu-id="d3046-102">Beispiel-URI für Excel Services-REST-API</span><span class="sxs-lookup"><span data-stu-id="d3046-102">Sample URI For Excel Services REST API</span></span>

<span data-ttu-id="d3046-103">Dieses Thema enthält Beispiel-URIs für die REST-Dienstbefehle (Representational State Transfer) in Excel Services.</span><span class="sxs-lookup"><span data-stu-id="d3046-103">This topic lists sample URIs for the representational state transfer (REST) service commands in Excel Services.</span></span>
  
    
    


> <span data-ttu-id="d3046-104">**Hinweis:** Die Excel Services-REST-API bezieht sich auf SharePoint und SharePoint 2016 (lokal).</span><span class="sxs-lookup"><span data-stu-id="d3046-104">**Note:** The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="d3046-105">Für Office 365 Education-, Business- und Enterprise-Konten verwenden Sie die Excel-REST-APIs, die Bestandteil des [Microsoft Graph](http://graph.microsoft.io/de-de/docs/api-reference/v1.0/resources/excel
> )-Endpunkts sind.</span><span class="sxs-lookup"><span data-stu-id="d3046-105">Note The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises. For Office 365 Education, Business, and Enterprise accounts, use the Excel REST APIs that are part of the  [Microsoft Graph](http://graph.microsoft.io/de-de/docs/api-reference/v1.0/resources/excel
) endpoint.</span></span>
  
    
    


## <a name="sample-uri-for-rest-commands-in-excel-services"></a><span data-ttu-id="d3046-106">Beispiel-URI für die REST-Befehle in Excel Services</span><span class="sxs-lookup"><span data-stu-id="d3046-106">Sample URI for REST Commands in Excel Services</span></span>

<span data-ttu-id="d3046-107">In den folgenden Beispielen verweist jeder URI auf eine Arbeitsmappe mit dem Namen  *sampleWorkbook.xlsx*  .</span><span class="sxs-lookup"><span data-stu-id="d3046-107">In the following examples, each URI references a workbook named  *sampleWorkbook.xlsx*  .</span></span>
  
    
    

- <span data-ttu-id="d3046-108">Die Datei sampleWorkbook.xlsx enthält benannte Bereiche und Diagramme.</span><span class="sxs-lookup"><span data-stu-id="d3046-108">The sampleWorkbook.xlsx file contains named ranges and charts.</span></span>
    
  
- <span data-ttu-id="d3046-p102">Die Datei sampleWorkbook.xlsx wird in einer vertrauenswürdigen SharePoint-Dokumentbibliothek gespeichert. In diesem Beispiel lautet der Pfad zum Speicherort von sampleWorkbook.xlsx wie folgt:</span><span class="sxs-lookup"><span data-stu-id="d3046-p102">The sampleWorkbook.xlsx file is saved to a trusted SharePoint document library. In this example, the path to the location of sampleWorkbook.xlsx is:</span></span>
    
```
  
http://<ServerName>/Docs/Documents/sampleWorkbook.xlsx
```


### <a name="sample-uri"></a><span data-ttu-id="d3046-111">Beispiel-URI</span><span class="sxs-lookup"><span data-stu-id="d3046-111">Sample URI</span></span>

<span data-ttu-id="d3046-112">Die ASPX-Seite für den REST-Dienst in Excel Services lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="d3046-112">The .aspx page for the REST service in Excel Services is:</span></span> 
  
    
    

```
http://<ServerName>/_vti_bin/ExcelRest.aspx

```

<span data-ttu-id="d3046-113">Es folgen Beispiel-URIs für den Zugriff auf die Arbeitsmappe sampleWorkbook.xlsx mithilfe des REST-Diensts in Excel Services. </span><span class="sxs-lookup"><span data-stu-id="d3046-113">The following are example URIs to access the sampleWorkbook.xlsx workbook by using the REST service in esesshort.</span></span> 
  
    
    

- <span data-ttu-id="d3046-114">Modell der obersten Ebene für die Arbeitsmappe (nur Bereiche und Diagramme im aktuellen Build):</span><span class="sxs-lookup"><span data-stu-id="d3046-114">Top-level model for the workbook (only ranges and charts in the current build):</span></span>
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model

```

- <span data-ttu-id="d3046-115">Abrufen der vollständigen Arbeitsmappe:</span><span class="sxs-lookup"><span data-stu-id="d3046-115">Get the full workbook:</span></span>
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model?$format=workbook

```

- <span data-ttu-id="d3046-p103">Zurückgeben eines Bereichs (Standard-HTML). Die folgenden beiden URI-Beispiele sind gleichwertig:</span><span class="sxs-lookup"><span data-stu-id="d3046-p103">Return a range (default html). The following two URI examples are equivalent:</span></span>
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1|G5')

```


```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1|G5')?$format=html
```

- <span data-ttu-id="d3046-118">Abrufen eines benannten Bereichs:</span><span class="sxs-lookup"><span data-stu-id="d3046-118">Get a named range:</span></span>
    
```
  http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('nameOfTheNamedRange')

```

- <span data-ttu-id="d3046-119">Zurückgeben eines ATOM-XML-Feeds:</span><span class="sxs-lookup"><span data-stu-id="d3046-119">Return an Atom XML feed:</span></span>
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model?$format=atom

```

- <span data-ttu-id="d3046-120">Festlegen und Zurückgeben einer Zelle:</span><span class="sxs-lookup"><span data-stu-id="d3046-120">Set a cell and return it:</span></span>
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1|G5')?Ranges('Sheet1!C3')=demo

```

- <span data-ttu-id="d3046-121">Abrufen eines Diagramms:</span><span class="sxs-lookup"><span data-stu-id="d3046-121">Get a chart:</span></span>
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart 1')

```

- <span data-ttu-id="d3046-122">Festlegen eines Werts und Abrufen eines Diagramms:</span><span class="sxs-lookup"><span data-stu-id="d3046-122">Set a value and get a chart:</span></span>
    
```
  
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart%201')?Ranges('Sheet1!A1')=5.5

```


