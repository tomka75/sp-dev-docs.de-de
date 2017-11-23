---
title: Grundlegende URI-Struktur und Pfad
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d73cf6c2-0677-4726-8a3e-2ad130e1a12c
ms.openlocfilehash: 2902dca96c5325250d8e1cd31647172e6968d632
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="basic-uri-structure-and-path"></a><span data-ttu-id="486f8-102">Grundlegende URI-Struktur und Pfad</span><span class="sxs-lookup"><span data-stu-id="486f8-102">Basic URI Structure and Path</span></span>

<span data-ttu-id="486f8-103">In diesem Thema wird erläutert, wie Sie die URI-Struktur und den Pfad für die Befehle des REST-Diensts in Excel Services erstellen.</span><span class="sxs-lookup"><span data-stu-id="486f8-103">This topic explains how to construct the URI structure and path for REST service commands in Excel Services.</span></span>
  
    
    


> <span data-ttu-id="486f8-104">**Hinweis:** Die Excel Services-REST-API bezieht sich auf SharePoint und SharePoint 2016 (lokal).</span><span class="sxs-lookup"><span data-stu-id="486f8-104">**Note:** The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="486f8-105">Für Office 365 Education-, Business- und Enterprise-Konten verwenden Sie die Excel-REST-APIs, die Bestandteil des [Microsoft Graph](http://graph.microsoft.io/de-de/docs/api-reference/v1.0/resources/excel
> )-Endpunkts sind.</span><span class="sxs-lookup"><span data-stu-id="486f8-105">Note The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises. For Office 365 Education, Business, and Enterprise accounts, use the Excel REST APIs that are part of the  [Microsoft Graph](http://graph.microsoft.io/de-de/docs/api-reference/v1.0/resources/excel
) endpoint.</span></span>
  
    
    


## <a name="basic-url-structure-and-path"></a><span data-ttu-id="486f8-106">Grundlegende URL-Struktur und Pfad</span><span class="sxs-lookup"><span data-stu-id="486f8-106">Basic URL Structure and Path</span></span>

<span data-ttu-id="486f8-p102">Die REST-API in Excel Services ermöglicht den Zugriff auf Ressourcen wie Diagramme, PivotTables, Tabellen und benannte Bereiche in einer Arbeitsmappe direkt über eine URL. Jede REST-URL in Excel Services besteht aus drei Teilen. Im Anschluss finden Sie die grundlegende Struktur der URL für den Zugriff auf die Ressourcen in der Arbeitsmappe:</span><span class="sxs-lookup"><span data-stu-id="486f8-p102">The REST API in Excel Services gives you the ability to access resources like charts, PivotTables, tables, and named ranges in a workbook directly through a URL. Each REST URL in Excel Services is built of three parts. Following is the basic structure of the URL to access the resources in a workbook:</span></span> 
  
    
    

1. <span data-ttu-id="486f8-110">**REST-URI zur ASPX-Seite** Der Einstiegspunkt zu einer ASPX-Seite</span><span class="sxs-lookup"><span data-stu-id="486f8-110">**REST aspx Page URI**  The entry point to an .aspx page</span></span>
    
  
2. <span data-ttu-id="486f8-111">**Speicherort der Arbeitsmappe** Der Pfad zu der Arbeitsmappe</span><span class="sxs-lookup"><span data-stu-id="486f8-111">**Workbook Location** The path to the workbook</span></span>
    
  
3. <span data-ttu-id="486f8-112">**Speicherort der Ressource** Der Pfad zu der angeforderten Ressource in der Arbeitsmappe</span><span class="sxs-lookup"><span data-stu-id="486f8-112">**Resource Location** The path to the requested resource inside the workbook</span></span>
    
  
<span data-ttu-id="486f8-113">Es folgt das Konstrukt für die REST-URL für ein bestimmtes Element in einer Arbeitsmappe:</span><span class="sxs-lookup"><span data-stu-id="486f8-113">Following is the construct for the REST URL to a specific element in a workbook:</span></span>
  
    
    



```

http://<ServerName>/_vti_bin/ExcelRest.aspx/<DocumentLibrary>/<FileName>/<ResourceLocation>
```

<span data-ttu-id="486f8-114">Es folgt ein Beispiel für eine REST-URL in Excel Services mit Kombination aller drei Teile.</span><span class="sxs-lookup"><span data-stu-id="486f8-114">Following is an example of how a REST URL in Excel Services looks with all three parts combined.</span></span> <span data-ttu-id="486f8-115">In diesem Beispiel greift die REST-URL auf eine Arbeitsmappe namens „sampleWorkbook.xlsx“ zu, die ein Diagramm namens „SampleChart“ enthält:</span><span class="sxs-lookup"><span data-stu-id="486f8-115">In this example, the REST URL is accessing a workbook called "sampleWorkbook.xlsx" that contains a chart called "SampleChart":</span></span>
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('SampleChart')
```

<span data-ttu-id="486f8-116">Die Arbeitsmappe ist in einer Dokumentbibliothek gespeichert.</span><span class="sxs-lookup"><span data-stu-id="486f8-116">The workbook is stored in a document library. The full path to the workbook is  ServerName.</span></span> <span data-ttu-id="486f8-117">Der vollständige Pfad zur Arbeitsmappe lautet `http://` _<ServerName>_ `/Docs/Documents/sampleWorkbook.xlsx`.</span><span class="sxs-lookup"><span data-stu-id="486f8-117">The workbook is stored in a document library. The full path to the workbook is  `http://` _<ServerName>ServerName_ `/Docs/Documents/sampleWorkbook.xlsx`.</span></span>
  
    
    
<span data-ttu-id="486f8-118">Die drei Teile der REST-URL sind folgende:</span><span class="sxs-lookup"><span data-stu-id="486f8-118">The three parts of the REST URL are:</span></span>
  
    
    

1. <span data-ttu-id="486f8-119">**REST-URI zur ASPX-Seite**: `http://` _<ServerName>_ `/_vti_bin/ExcelRest.aspx`</span><span class="sxs-lookup"><span data-stu-id="486f8-119">**REST aspx Page URI**: `http://` _<ServerName>ServerName_ `/_vti_bin/ExcelRest.aspx`</span></span>
    
  
2. <span data-ttu-id="486f8-120">**Speicherort der Arbeitsmappe**: `/Docs/Documents/sampleWorkbook.xlsx`</span><span class="sxs-lookup"><span data-stu-id="486f8-120">**Workbook Location**: `/Docs/Documents/sampleWorkbook.xlsx`</span></span>
    
  
3. <span data-ttu-id="486f8-121">**Speicherort der Ressource**: `/model/Ranges('nameOfTheNamedRange')`</span><span class="sxs-lookup"><span data-stu-id="486f8-121">**Resource Location**: `/model/Ranges('nameOfTheNamedRange')`</span></span>
    
  

### <a name="accessing-by-using-the-discovery-user-interface"></a><span data-ttu-id="486f8-122">Zugriff unter Verwendung der Discovery-Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="486f8-122">Accessing by Using the Discovery User Interface</span></span>

<span data-ttu-id="486f8-p105">Sie können auf das Diagramm auch unter Verwendung der Discovery-Benutzeroberfläche zugreifen. Informationen dazu, wie Sie auf Ressourcen wie Diagramme, Tabellen, PivotTables und Bereiche unter Verwendung des im folgenden Screenshot dargestellten Ermittlungsmechanismus zugreifen, finden Sie unter  [Ermittlung in der Excel Services-REST-API](discovery-in-excel-services-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="486f8-p105">You can also access the chart by using the discovery user interface. To learn how access resources like charts, tables, PivotTables, and ranges by using the discovery mechanism shown in the following screen shot, see  [Discovery in Excel Services REST API](discovery-in-excel-services-rest-api.md).</span></span>
  
    
    

  
    
    
![Excel Services REST-Modell-URL](../images/SharePointServer14Con_XLSvcs_RESTModel.gif)
  
    
    

  
    
    

  
    
    

  
    
    

### <a name="marker-path"></a><span data-ttu-id="486f8-126">Markierungspfad</span><span class="sxs-lookup"><span data-stu-id="486f8-126">Marker Path</span></span>

<span data-ttu-id="486f8-127">Nachfolgend sehen Sie die ASPX-Seite für den REST-Dienst in Excel Services:</span><span class="sxs-lookup"><span data-stu-id="486f8-127">Following is the aspx page for the REST service in esesshort:</span></span>
  
    
    

```
http://<ServerName>/_vti_bin/ExcelRest.aspx
```

<span data-ttu-id="486f8-128">Um auf den REST-Dienst in Excel Services zuzugreifen, müssen Sie der URL `http://` _<ServerName>_ `/_vti_bin/ExcelRest.aspx` voranstellen.</span><span class="sxs-lookup"><span data-stu-id="486f8-128">To access the REST service in Excel Services, you must preface the URL with  `http://` _<ServerName>ServerName_ `/_vti_bin/ExcelRest.aspx`.</span></span>
  
    
    

### <a name="workbook-location"></a><span data-ttu-id="486f8-129">Speicherort der Arbeitsmappe</span><span class="sxs-lookup"><span data-stu-id="486f8-129">Workbook Location</span></span>

<span data-ttu-id="486f8-p106">Der Speicherort der Arbeitsmappe ist der relative Pfad zu der Arbeitsmappe, die die Ressourcen enthält, auf die Sie zugreifen möchten. Angenommen, Sie haben eine Arbeitsmappe mit dem Namen sampleWorkbook.xlsx, die in einer vertrauenswürdigen SharePoint-Dokumentbibliothek gespeichert ist. Für dieses Beispiel folgt im Anschluss der Pfad zu dem Speicherort von sampleWorkbook.xlsx: </span><span class="sxs-lookup"><span data-stu-id="486f8-p106">The workbook location is the relative path to the workbook that has resources that you are interested in accessing. For example, assume that you have a workbook named sampleWorkbook.xlsx, saved to a trusted SharePoint document library. In this example, following is the path to the location of sampleWorkbook.xlsx:</span></span> 
  
    
    

```
http://<ServerName>/Docs/Documents/sampleWorkbook.xlsx
```

<span data-ttu-id="486f8-p107">Sie nehmen den relativen Pfad zu der Arbeitsmappe ( `Docs/Documents/sampleWorkbook.xlsx`) und hängen diesen an den Markierungspfad an. Im Anschluss finden Sie die URL mit angehängtem Markierungspfad und angehängtem Speicherort der Arbeitsmappe:</span><span class="sxs-lookup"><span data-stu-id="486f8-p107">You take the relative path to the workbook ( `Docs/Documents/sampleWorkbook.xlsx`) and append it to the marker path. Following is the URL with the marker path and workbook location appended:</span></span>
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx
```


### <a name="resource-location"></a><span data-ttu-id="486f8-135">Speicherort der Ressource</span><span class="sxs-lookup"><span data-stu-id="486f8-135">Resource Location</span></span>

<span data-ttu-id="486f8-p108">Der Speicherort der Ressource ist der Pfad innerhalb der Arbeitsmappe zu dem gewünschten Element. Wenn Sie beispielsweise auf ein Diagramm zugreifen möchten, würde der Speicherort der Ressource in etwa folgendermaßen aussehen:  `/model/Charts('Chart 1')`.</span><span class="sxs-lookup"><span data-stu-id="486f8-p108">The resource location is the path inside the workbook to the element that you request. For example, if you want to get a chart, the resource location would be similar to  `/model/Charts('Chart 1')`.</span></span>
  
    
    
<span data-ttu-id="486f8-p109">Um die vollständige URL zu erhalten, hängen Sie dieses an den Markierungspfad und den relativen Pfad zu der Arbeitsmappe an. Die vollständige Beispiel-URL sieht dann folgendermaßen aus: :</span><span class="sxs-lookup"><span data-stu-id="486f8-p109">For the full URL, you append this to the marker path and the relative path to the workbook. Following is the full example URL:</span></span>
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart 1')

```


## <a name="see-also"></a><span data-ttu-id="486f8-140">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="486f8-140">See also</span></span>


#### <a name="concepts"></a><span data-ttu-id="486f8-141">Konzepte</span><span class="sxs-lookup"><span data-stu-id="486f8-141">Concepts</span></span>


  
    
    
 [<span data-ttu-id="486f8-142">Ressourcen-URI für die REST API in Excel Services</span><span class="sxs-lookup"><span data-stu-id="486f8-142">Resources URI for Excel Services REST API</span></span>](resources-uri-for-excel-services-rest-api.md)
  
    
    
 [<span data-ttu-id="486f8-143">Ermittlung in der Excel Services-REST-API</span><span class="sxs-lookup"><span data-stu-id="486f8-143">Discovery in Excel Services REST API</span></span>](discovery-in-excel-services-rest-api.md)
