---
title: Zugreifen auf ein Schema
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 02613912-36f6-4edc-a915-165d12e60bc8
ms.openlocfilehash: 9f9bb2513eb8c2dbbe5951d86391ebb239a6c389
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="accessing-a-schema"></a><span data-ttu-id="7bcd7-102">Zugreifen auf ein Schema</span><span class="sxs-lookup"><span data-stu-id="7bcd7-102">Accessing a Schema</span></span>

<span data-ttu-id="7bcd7-p101">In diesem Thema zeigt ein Beispiel zum zugreifen und Anzeigen eines Schemas für den REST-Dienst in Excel Services. In diesem Thema wird davon ausgegangen, dass Sie  [Beispiel-URI für die REST-API in Excel Services](sample-uri-for-excel-services-rest-api.md).d gelesen haben.</span><span class="sxs-lookup"><span data-stu-id="7bcd7-p101">This topic shows one example of how you can access and look at a schema for the REST service in Excel Services. This topic assumes that you have read  [Sample URI For Excel Services REST API](sample-uri-for-excel-services-rest-api.md).d</span></span>
  
    
    


> <span data-ttu-id="7bcd7-105">**Hinweis:** Die Excel Services-REST-API bezieht sich auf SharePoint und SharePoint 2016 (lokal).</span><span class="sxs-lookup"><span data-stu-id="7bcd7-105">**Note:** The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="7bcd7-106">Für Office 365 Education-, Business- und Enterprise-Konten verwenden Sie die Excel-REST-APIs, die Bestandteil des [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
> )-Endpunkts sind.</span><span class="sxs-lookup"><span data-stu-id="7bcd7-106">Note The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises. For Office 365 Education, Business, and Enterprise accounts, use the Excel REST APIs that are part of the  [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
) endpoint.</span></span>
  
    
    


## <a name="viewing-a-schema"></a><span data-ttu-id="7bcd7-107">Anzeigen eines Schemas</span><span class="sxs-lookup"><span data-stu-id="7bcd7-107">Viewing a Schema</span></span>

 <span data-ttu-id="7bcd7-108">Geben Sie in der Adressleiste des Browsers den URI zu einem ATOM-XML-Feed mithilfe des folgenden URI ein:</span><span class="sxs-lookup"><span data-stu-id="7bcd7-108">In the browser address bar, type the URI to an Atom XML feed by using a URI, as follows:</span></span>
  
    
    

```

http://myserver/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1|H3')?$format=atom
```

<span data-ttu-id="7bcd7-109">Klicken Sie mit der rechten Maustaste auf die Webseite, und klicken Sie dann auf **Quelltext anzeigen**.</span><span class="sxs-lookup"><span data-stu-id="7bcd7-109">Right-click the Web page, and then click **View Source**.</span></span>
  
    
    
<span data-ttu-id="7bcd7-110">Es sollte ein Schema ähnlich dem folgenden Beispiel angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="7bcd7-110">You should see a schema that looks similar to the following example:</span></span>
  
    
    



```XML
<?xml version="1.0" encoding="utf-8"?>
<entry xml:base="http://excel.live.com/REST" xmlns:x="http://schemas.microsoft.com/office/2008/07/excelservices/rest" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservice" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
  <title type="text">Sheet1!A1:H3</title>
  <id>http://myserver/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1%7CH3')</id>
  <updated>2009-06-25T00:41:37Z</updated>
  <author>
    <name />
  </author>
  <link rel="self" href="http://myserver/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Ranges('Sheet1!A1%7CH3')?$format=atom" title="Sheet1!A1:H3" />
  <category term="ExcelServices.Range" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <content type="application/xml">
    <x:range name="Sheet1!A1:H3">
      <x:row>
        <x:c>
          <x:fv>Name </x:fv>
        </x:c>
        <x:c>
          <x:fv>Name </x:fv>
        </x:c>
        <x:c>
          <x:fv>Exchange  </x:fv>
        </x:c>
        <x:c>
          <x:fv>Symbol  </x:fv>
        </x:c>
        <x:c>
          <x:fv>Last Trade </x:fv>
        </x:c>
        <x:c />
        <x:c>
          <x:fv>Change </x:fv>
        </x:c>
        <x:c>
          <x:fv>Mkt Cap</x:fv>
        </x:c>
      </x:row>
      <x:row>
        <x:c>
          <x:fv>Microsoft Corporation </x:fv>
        </x:c>
        <x:c>
          <x:fv>Microsoft Corporation </x:fv>
        </x:c>
        <x:c>
          <x:fv> </x:fv>
        </x:c>
        <x:c>
          <x:fv>MSFT </x:fv>
        </x:c>
        <x:c>
          <x:v>26.25</x:v>
          <x:fv>26.25</x:fv>
        </x:c>
        <x:c />
        <x:c>
          <x:fv>-0.23 (-0.87%) </x:fv>
        </x:c>
        <x:c>
          <x:v>239670000000</x:v>
          <x:fv> $239,670,000,000 </x:fv>
        </x:c>
      </x:row>
      <x:row>
        <x:c />
        <x:c />
        <x:c>
          <x:fv> </x:fv>
        </x:c>
        <x:c />
        <x:c>
          <x:v>15.58</x:v>
          <x:fv>15.58</x:fv>
        </x:c>
        <x:c />
        <x:c>
          <x:fv>-1.38 (-8.14%) </x:fv>
        </x:c>
        <x:c>
          <x:v>21590000000</x:v>
          <x:fv> $21,590,000,000 </x:fv>
        </x:c>
      </x:row>
    </x:range>
  </content>
</entry>

```


