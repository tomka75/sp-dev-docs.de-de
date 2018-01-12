---
title: Verwenden von OData mit Excel Services-REST in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8a20225a-323c-4420-bbb4-eef60aed4b42
ms.openlocfilehash: 2e45347cab9befa2bf333339db59fa052ece11af
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="using-odata-with-excel-services-rest-in-sharepoint"></a><span data-ttu-id="6a30e-102">Verwenden von OData mit Excel Services-REST in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6a30e-102">Using OData with Excel Services REST in SharePoint</span></span>
<span data-ttu-id="6a30e-103">In SharePoint Server 2010 wurde die REST-API für die Verwendung beim Abrufen und Festlegen von Informationen in Excel-Arbeitsmappen eingeführt, die in SharePoint-Dokumentbibliotheken gespeichert sind.</span><span class="sxs-lookup"><span data-stu-id="6a30e-103">SharePoint Server 2010 introduced the REST API for use in getting and setting information in Excel Workbooks stored in SharePoint document libraries.</span></span> <span data-ttu-id="6a30e-104">SharePoint fügt eine neue Möglichkeit zum Abrufen von Daten aus Excel Services hinzu, die Open Data Protocol (OData) verwenden. Diese können Sie zum Abrufen von Informationen zu Excel Services-Ressourcen verwenden.</span><span class="sxs-lookup"><span data-stu-id="6a30e-104">SharePoint adds a new way to request data from Excel Services that uses the Open Data Protocol (OData) which you can use to get information about Excel Services resources.</span></span> <span data-ttu-id="6a30e-105">Dieser neue Service basiert vor allem auf der vorhandenen Excel Services-REST-API. Dieses Thema bietet eine allgemeine Übersicht über die Verwendung von OData in Excel Services.</span><span class="sxs-lookup"><span data-stu-id="6a30e-105">This new service relies heavily on the existing Excel Services REST API.This topic provides a high-level overview for using OData in Excel Services.</span></span>

> [!NOTE] 
> <span data-ttu-id="6a30e-106">Die Excel Services-REST-API kann in lokalen Bereitstellungen von SharePoint und SharePoint 2016 verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6a30e-106">Note: The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="6a30e-107">Für Konten in Office 365 Education, Office 365 Business und Office 356 Enterprise müssen Sie die Excel-REST-APIs verwenden, die in den [Microsoft Graph]((http://graph.microsoft.io/de-DE/docs/api-reference/v1.0/resources/excel))-Endpunkt integriert sind.</span><span class="sxs-lookup"><span data-stu-id="6a30e-107">For Office 365 Education, Business, and Enterprise accounts, use the Excel REST APIs that are part of the  [Microsoft Graph]((http://graph.microsoft.io/de-DE/docs/api-reference/v1.0/resources/excel)) endpoint.</span></span>
  
    
    


## <a name="what-is-odata"></a><span data-ttu-id="6a30e-108">Was ist OData?</span><span class="sxs-lookup"><span data-stu-id="6a30e-108">What is OData?</span></span>
<span data-ttu-id="6a30e-109"><a name="xlsWhatIsOdata"> </a></span><span class="sxs-lookup"><span data-stu-id="6a30e-109"><a name="xlsWhatIsOdata"> </a></span></span>

<span data-ttu-id="6a30e-p103">OData ist ein offenes Internet-Protokoll zum Abfragen und Aktualisieren von Daten. Es verwendet einen RESTful-Ansatz für die Rückgabe von Daten aus Ressourcen im Internet. Das heißt, Sie verwenden einen URI mit eingeschlossenen Abfrageparametern, um Informationen zu einer bestimmten Ressource zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="6a30e-p103">OData is an open web protocol for querying and updating data. It uses a RESTful approach to return data from resources on the web. That is, you use a URI with query parameters included to get information about a specific resource.</span></span>
  
    
    
<span data-ttu-id="6a30e-113">Weitere Informationen zu OData finden Sie auf der Website für die  [Open Data Protocol-Spezifikation]((http://www.odata.org)).</span><span class="sxs-lookup"><span data-stu-id="6a30e-113">For more information about OData, see the website for the  [Open Data Protocol specification]((http://www.odata.org)).</span></span>
  
    
    

## <a name="how-do-you-use-odata-with-excel-services"></a><span data-ttu-id="6a30e-114">Wie verwenden Sie OData mit Excel Services?</span><span class="sxs-lookup"><span data-stu-id="6a30e-114">How do you use OData with Excel Services?</span></span>
<span data-ttu-id="6a30e-115"><a name="xlsHowUseOdata"> </a></span><span class="sxs-lookup"><span data-stu-id="6a30e-115"><a name="xlsHowUseOdata"> </a></span></span>

<span data-ttu-id="6a30e-p104">Bei Excel Services verwenden Sie OData zum Abrufen von Informationen über Tabellen (einschließlich Abfragetabellen) in einer Arbeitsmappe, die in einer SharePoint-Bibliothek gespeichert ist. Der OData-Dienst gibt die angeforderten Daten im XML-Atom-Format zurück.</span><span class="sxs-lookup"><span data-stu-id="6a30e-p104">In the case of Excel Services, you use OData to get information about tables (including query tables) in a workbook that is stored in a SharePoint library. The OData service returns the data that you requested in the in the XML Atom format.</span></span>
  
    
    

### <a name="syntax-for-making-odata-requests-to-excel-services"></a><span data-ttu-id="6a30e-118">Syntax für OData-Anforderungen an Excel Services</span><span class="sxs-lookup"><span data-stu-id="6a30e-118">Syntax for making OData requests to Excel Services</span></span>
<span data-ttu-id="6a30e-119"><a name="xlsOdataSyntax"> </a></span><span class="sxs-lookup"><span data-stu-id="6a30e-119"><a name="xlsOdataSyntax"> </a></span></span>

<span data-ttu-id="6a30e-p105">SharePoint macht jede Arbeitsmappe als separate Ressource verfügbar, aus der Sie Informationen abrufen können. In dieser Version von SharePoint Server können Sie nur Daten aus Tabellen in der Arbeitsmappe abrufen.</span><span class="sxs-lookup"><span data-stu-id="6a30e-p105">SharePoint exposes each workbook as a separate resource that you can request information from. In this release of SharePoint Server, you can only get data from tables in the workbook.</span></span>
  
    
    
<span data-ttu-id="6a30e-p106">Zum Abrufen von Daten aus einer Excel-Arbeitsmappe müssen Sie eine URL erstellen, die auf die Arbeitsmappe verweist und die angibt, welche Daten Sie aus der Arbeitsmappe abrufen möchten und wie die Daten angeordnet werden sollen. Wenn Sie zum Beispiel Informationen zu Tabelle1 in einer Arbeitsmappe mit dem Namen "ProductSales.xlsx" abrufen möchten, die in einer SharePoint-Bibliothek in einem Ordner mit dem Namen "Documents" gespeichert ist, verwenden Sie die folgende URL.</span><span class="sxs-lookup"><span data-stu-id="6a30e-p106">To get data from an Excel workbook, you construct a URL that points to the workbook, and that specifies what data that you want to get from the workbook, and how to arrange that data. For example, to get information about Table1 in a workbook named ProductSales.xlsx that is stored on a SharePoint library in a folder that is named Documents, you would use a URL as follows.</span></span>
  
    
    
<span data-ttu-id="6a30e-124">http://\<serverName\>/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1</span><span class="sxs-lookup"><span data-stu-id="6a30e-124">http://\<serverName\>/_vti_bin/ExcelRest.aspx/Documents/ProductSales.xlsx/OData/Table1</span></span>
  
    
    
<span data-ttu-id="6a30e-125">Weitere Informationen zur Verwendung von OData zum Abrufen von Informationen aus einer ExcelArbeitsmappe, die in SharePoint Server gespeichert ist, finden Sie unter  [Excel-Arbeitsmappendaten aus SharePoint Server mithilfe von OData anfordern](requesting-excel-workbook-data-from-sharepoint-server-using-odata.md).</span><span class="sxs-lookup"><span data-stu-id="6a30e-125">For more information about how to use OData to request information from an Excel workbook stored on SharePoint Server, see  [Requesting Excel workbook data from SharePoint Server using OData](requesting-excel-workbook-data-from-sharepoint-server-using-odata.md).</span></span>
  
    
    

## <a name="data-returned-by-odata"></a><span data-ttu-id="6a30e-126">Von OData zurückgegebenen Daten</span><span class="sxs-lookup"><span data-stu-id="6a30e-126">Data returned by OData</span></span>
<span data-ttu-id="6a30e-127"><a name="xlsOdataReturnData"> </a></span><span class="sxs-lookup"><span data-stu-id="6a30e-127"><a name="xlsOdataReturnData"> </a></span></span>

<span data-ttu-id="6a30e-p107">Wenn Sie eine OData-Anforderung an Excel Services stellen, werden die XML-Ergebnisse im Atom-Format zurückgegeben. Das Atom-Format ist das einzige unterstützte Format in der Excel Services-Implementierung von OData. Nachfolgend ist zum Beispiel eine OData-Anforderung für die erste Zeile in der ersten Tabelle (mit dem Namen "Tabelle1") in einer Arbeitsmappe mit dem Namen "WindowsPhoneComparison.xlsx" aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="6a30e-p107">When you make an OData request to Excel Services, it returns XML in the Atom format. The Atom format is the only supported format in the Excel Services implementation of OData. For example, the following shows an OData request for the first row in the first table (named Table1) in a workbook named WindowsPhoneComparison.xlsx.</span></span>
  
    
    
<span data-ttu-id="6a30e-131">http://\<serverName\>/_vti_bin/ExcelRest.aspx/Documents/WindowsPhoneComparison.xlsx/odata/Table1</span><span class="sxs-lookup"><span data-stu-id="6a30e-131">http://\<serverName\>/_vti_bin/ExcelRest.aspx/Documents/WindowsPhoneComparison.xlsx/odata/Table1</span></span>
  
    
    
<span data-ttu-id="6a30e-132">Excel Services gibt dann die im folgenden Code dargestellte Atom-XML zurück.</span><span class="sxs-lookup"><span data-stu-id="6a30e-132">Excel Services then returns the Atom XML shown in the following code.</span></span>
  
    
    



```XML

<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<entry xml:base="http://{serverName}/_vti_bin/ExcelRest.aspx/Documents/WindowsPhoneComparison.xlsx/OData" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" m:etag="W/&amp;quot;datetime'0001-01-01T00%3A00%3A00'&amp;quot;" xmlns="http://www.w3.org/2005/Atom">
  <id>http://{serverName}/_vti_bin/ExcelRest.aspx/Documents/WindowsPhoneComparison.xlsx/OData/Table1(0)</id>
  <title type="text"></title>
  <updated>0001-01-01T00:00:00-08:00</updated>
  <author>
    <name />
  </author>
  <link rel="edit" title="Table1Item" href="/Table1(0)" />
  <category term="ExcelServices.Table1Item" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <content type="application/xml">
    <m:properties>
      <d:Phone>Samsung Focus</d:Phone>
      <d:sizeweight m:type="Edm.Double">4</d:sizeweight>
      <d:camera m:type="Edm.Double">2.5</d:camera>
      <d:battery m:type="Edm.Double">3</d:battery>
      <d:memory m:type="Edm.Double">3</d:memory>
      <d:speed m:type="Edm.Double">3</d:speed>
      <d:style m:type="Edm.Double">3</d:style>
      <d:callquality m:type="Edm.Double">3</d:callquality>
      <d:overall m:type="Edm.Double">3</d:overall>
      <d:excelRowID m:type="Edm.Int32">0</d:excelRowID>
    </m:properties>
  </content>
</entry>

```


## <a name="conclusion"></a><span data-ttu-id="6a30e-133">Schlussbemerkung</span><span class="sxs-lookup"><span data-stu-id="6a30e-133">Conclusion</span></span>
<span data-ttu-id="6a30e-134"><a name="xlsOdataReturnData"> </a></span><span class="sxs-lookup"><span data-stu-id="6a30e-134"><a name="xlsOdataReturnData"> </a></span></span>

<span data-ttu-id="6a30e-p108">OData bietet eine einfache Möglichkeit zum Abrufen von Daten aus Excel-Arbeitsmappen, die in SharePoint gespeichert sind. Durch eine einfache Syntax, die auf Webstandards wie HTTP und REST basiert, können Sie mit OData schnell und einfach Daten aus Excel-Arbeitsmappen abrufen.</span><span class="sxs-lookup"><span data-stu-id="6a30e-p108">OData provides a simple way to get data from Excel workbooks that are stored on SharePoint. Using a straightforward syntax that is based on web standards like HTTP and REST, OData lets you quickly and easily get data from Excel workbooks.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="6a30e-137">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="6a30e-137">See also</span></span>
<span data-ttu-id="6a30e-138"><a name="xlsOdataAddRes"> </a></span><span class="sxs-lookup"><span data-stu-id="6a30e-138"><a name="xlsOdataAddRes"> </a></span></span>


-  <span data-ttu-id="6a30e-139">[Was ist neu in Excel Services für Entwickler]((http://msdn.microsoft.com/library/09e96c8b-cb55-4fd1-a797-b50fbf0f9296.aspx))</span><span class="sxs-lookup"><span data-stu-id="6a30e-139">[What's new in Excel Services for developers]((http://msdn.microsoft.com/library/09e96c8b-cb55-4fd1-a797-b50fbf0f9296.aspx))</span></span>
    
  
-  [<span data-ttu-id="6a30e-140">Excel-Arbeitsmappendaten aus SharePoint Server mithilfe von OData anfordern</span><span class="sxs-lookup"><span data-stu-id="6a30e-140">Requesting Excel workbook data from SharePoint Server using OData</span></span>](requesting-excel-workbook-data-from-sharepoint-server-using-odata.md)
    
  
-  <span data-ttu-id="6a30e-141">[OData-Spezifikationsdokumentation]((http://www.odata.org))</span><span class="sxs-lookup"><span data-stu-id="6a30e-141">[OData specification documentation]((http://www.odata.org))</span></span>
    
  

