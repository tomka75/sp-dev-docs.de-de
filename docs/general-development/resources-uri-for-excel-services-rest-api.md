---
title: "Ressourcen-URI für Excel Services-REST-API"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 79f95305-ec9e-4842-b937-85f66ced98e4
ms.openlocfilehash: e1b77373e293051315900e9fb06cb287c46e509e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="resources-uri-for-excel-services-rest-api"></a><span data-ttu-id="d1695-102">Ressourcen-URI für Excel Services-REST-API</span><span class="sxs-lookup"><span data-stu-id="d1695-102">Resources URI for Excel Services REST API</span></span>

<span data-ttu-id="d1695-103">Mit der REST-API in Excel Services können Sie eine direkte Verknüpfung zu Entitäten herstellen.</span><span class="sxs-lookup"><span data-stu-id="d1695-103">You can link to entities directly by using the REST API in Excel Services.</span></span>
  
> [!NOTE]
> <span data-ttu-id="d1695-104">Die Excel Services-REST-API kann in lokalen Bereitstellungen von SharePoint und SharePoint 2016 verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="d1695-104">Note: The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="d1695-105">Für Office 365 Education-, Business- und Enterprise-Konten verwenden Sie die Excel-REST-APIs, die Bestandteil des [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
)-Endpunkts sind.</span><span class="sxs-lookup"><span data-stu-id="d1695-105">For Office 365 Education, Business, and Enterprise accounts, use the Excel REST APIs that are part of the  [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
) endpoint.</span></span>
  
    
    


## <a name="base-rest-url"></a><span data-ttu-id="d1695-106">Basis-REST-URL</span><span class="sxs-lookup"><span data-stu-id="d1695-106">Base REST URL</span></span>

<span data-ttu-id="d1695-107">Es folgt ein Beispiel für eine REST-URL zu einem bestimmten Element in einer Arbeitsmappe.</span><span class="sxs-lookup"><span data-stu-id="d1695-107">The following is an example of a REST URL to a specific element in a workbook.</span></span>
  
    
    

```

http://<ServerName>/_vti_bin/ExcelRest.aspx/<DocumentLibrary>/<FileName>/<ResourceLocation>
```

<span data-ttu-id="d1695-p102">Deaktiviert die Basis-REST-URL ist eine relative URL der REST basiert. Es folgt ein Beispiel für ein Basis-REST-URL zu einer bestimmten Arbeitsmappe.</span><span class="sxs-lookup"><span data-stu-id="d1695-p102">A relative REST URL is based off the base REST URL. The following is an example of a base REST URL to a specific workbook.</span></span>
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/<DocumentLibrary>/<FileName>
```

<span data-ttu-id="d1695-110">Angenommen, Sie verfügen über eine Arbeitsmappe mit dem Namen „sampleWorkbook.xlsx“ in der folgenden Dokumentbibliothek: </span><span class="sxs-lookup"><span data-stu-id="d1695-110">For example, if you have a workbook named "sampleWorkbook.xlsx" in the following document library:</span></span> 
  
    
    



```
http://<ServerName>/Docs/Documents/sampleWorkbook.xlsx
```

<span data-ttu-id="d1695-111">Die Basis-REST-URL zur Arbeitsmappe lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="d1695-111">The base REST URL to the workbook is:</span></span>
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx
```


## <a name="resources-uri"></a><span data-ttu-id="d1695-112">Ressourcen-URI</span><span class="sxs-lookup"><span data-stu-id="d1695-112">Resources URI</span></span>

<span data-ttu-id="d1695-p103">In Tabelle 1 sind alle Ressourcen in der REST-API in Excel Services aufgeführt, auf die zugegriffen werden kann. Für den Zugriff auf eine bestimmte Ressource fügen Sie den Ressourcenspeicherort an die Basis-REST-URL zu einer Arbeitsmappe an.</span><span class="sxs-lookup"><span data-stu-id="d1695-p103">Table 1 shows all the accessible resources in the Excel Services REST API. To access a particular resource, append the resource location to the base REST URL to a workbook.</span></span>
  
    
    

<span data-ttu-id="d1695-115">**Tabelle 1. Ressourcen, auf die in der Excel Services-REST-API zugegriffen werden kann**</span><span class="sxs-lookup"><span data-stu-id="d1695-115">**Table 1. Accessible resources in the Excel Services REST API**</span></span>


|<span data-ttu-id="d1695-116">**Speicherort der Ressource**</span><span class="sxs-lookup"><span data-stu-id="d1695-116">**Resource Location**</span></span>|<span data-ttu-id="d1695-117">**Format**</span><span class="sxs-lookup"><span data-stu-id="d1695-117">**Format**</span></span>|<span data-ttu-id="d1695-118">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="d1695-118">**Example**</span></span>|<span data-ttu-id="d1695-119">**Hinweise**</span><span class="sxs-lookup"><span data-stu-id="d1695-119">**Notes**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="d1695-120">/model</span><span class="sxs-lookup"><span data-stu-id="d1695-120">/model</span></span>  <br/> |<span data-ttu-id="d1695-121">Atom (Standard)</span><span class="sxs-lookup"><span data-stu-id="d1695-121">Atom (default)</span></span>  <br/> |<span data-ttu-id="d1695-122">/model</span><span class="sxs-lookup"><span data-stu-id="d1695-122">/model</span></span>  <br/> |<span data-ttu-id="d1695-p104">Gibt einen ATOM-Feed mit den von der REST-API in Excel Services unterstützten Ressourcen zurück. Zu den unterstützten Ressourcen zählen Bereiche, Diagramme, Tabellen und PivotTables.</span><span class="sxs-lookup"><span data-stu-id="d1695-p104">Returns an Atom feed with the resources supported by the Excel Services REST API. The supported resources are ranges, charts, tables, and PivotTables.</span></span>  <br/> |
|<span data-ttu-id="d1695-125">/model</span><span class="sxs-lookup"><span data-stu-id="d1695-125">/model</span></span>  <br/> |<span data-ttu-id="d1695-126">Arbeitsmappe</span><span class="sxs-lookup"><span data-stu-id="d1695-126">workbook</span></span>  <br/> |<span data-ttu-id="d1695-127">/model?$format=workbook</span><span class="sxs-lookup"><span data-stu-id="d1695-127">/model?$format=workbook</span></span>  <br/> |<span data-ttu-id="d1695-p105">Dies ist die Arbeitsmappe. Unterstützte Arbeitsmappenformate sind XLSX, XLSB und XLSM.</span><span class="sxs-lookup"><span data-stu-id="d1695-p105">This is the workbook. Supported workbook formats are xlsx, xlsb, and xlsm.</span></span>  <br/> |
|<span data-ttu-id="d1695-130">/model/Ranges</span><span class="sxs-lookup"><span data-stu-id="d1695-130">/model/Ranges</span></span>  <br/> |<span data-ttu-id="d1695-131">Atom (Standard)</span><span class="sxs-lookup"><span data-stu-id="d1695-131">Atom (default)</span></span>  <br/> |<span data-ttu-id="d1695-132">/model/Ranges?$format=atom</span><span class="sxs-lookup"><span data-stu-id="d1695-132">/model/Ranges?$format=atom</span></span>  <br/> |<span data-ttu-id="d1695-133">Ein ATOM-Feed, der alle benannten Bereiche in der Arbeitsmappe auflistet.</span><span class="sxs-lookup"><span data-stu-id="d1695-133">An Atom feed that listis all the named ranges in the workbook.</span></span>  <br/> |
|<span data-ttu-id="d1695-134">/model/Ranges('[Name]')</span><span class="sxs-lookup"><span data-stu-id="d1695-134">/model/Ranges('[Name]')</span></span>  <br/> |<span data-ttu-id="d1695-135">HTML (Standard)</span><span class="sxs-lookup"><span data-stu-id="d1695-135">HTML (default)</span></span>  <br/> |<span data-ttu-id="d1695-136">/model/Ranges('MyRange')?$format=html</span><span class="sxs-lookup"><span data-stu-id="d1695-136">/model/Ranges('MyRange')?$format=html</span></span>  <br/> |<span data-ttu-id="d1695-137">Ein HTML-Fragment für den angeforderten Bereich.</span><span class="sxs-lookup"><span data-stu-id="d1695-137">An HTML fragment for the requested range.</span></span>  <br/> |
|<span data-ttu-id="d1695-138">/model/Ranges('[Name]')</span><span class="sxs-lookup"><span data-stu-id="d1695-138">/model/Ranges('[Name]')</span></span>  <br/> |<span data-ttu-id="d1695-139">Atom</span><span class="sxs-lookup"><span data-stu-id="d1695-139">Atom</span></span>  <br/> |<span data-ttu-id="d1695-140">/model/Ranges('MyRange')?$format=atom</span><span class="sxs-lookup"><span data-stu-id="d1695-140">/model/Ranges('MyRange')?$format=atom</span></span>  <br/> |<span data-ttu-id="d1695-141">Ein ATOM-Eintrag, der eine XML-Darstellung der Daten in diesem Bereich enthält.</span><span class="sxs-lookup"><span data-stu-id="d1695-141">An Atom entry that contains an XML representation of the data within the range.</span></span>  <br/> |
|<span data-ttu-id="d1695-142">/model/Charts</span><span class="sxs-lookup"><span data-stu-id="d1695-142">/model/Charts</span></span>  <br/> |<span data-ttu-id="d1695-143">Atom (Standard)</span><span class="sxs-lookup"><span data-stu-id="d1695-143">Atom (default)</span></span>  <br/> |<span data-ttu-id="d1695-144">/model/Charts?$format=atom</span><span class="sxs-lookup"><span data-stu-id="d1695-144">/model/Charts?$format=atom</span></span>  <br/> |<span data-ttu-id="d1695-145">Ein ATOM-Feed, der alle Diagramme in der Arbeitsmappe auflistet.</span><span class="sxs-lookup"><span data-stu-id="d1695-145">An Atom feed that lists all the charts in the workbook.</span></span>  <br/> |
|<span data-ttu-id="d1695-146">/model/Charts('[Name]')</span><span class="sxs-lookup"><span data-stu-id="d1695-146">/model/Charts('[Name]')</span></span>  <br/> |<span data-ttu-id="d1695-147">Bild (Standard)</span><span class="sxs-lookup"><span data-stu-id="d1695-147">Image (default)</span></span>  <br/> |<span data-ttu-id="d1695-148">/model/Charts('MyChart')?$format=image</span><span class="sxs-lookup"><span data-stu-id="d1695-148">/model/Charts('MyChart')?$format=image</span></span>  <br/> |<span data-ttu-id="d1695-p106">Ein Bild des Diagramms. Das Bild hat das PNG-Format (Portable Network Graphics).</span><span class="sxs-lookup"><span data-stu-id="d1695-p106">An image of the chart. The image is in Portable Network Graphics (PNG) format.</span></span>  <br/> |
|<span data-ttu-id="d1695-151">/model/Tables</span><span class="sxs-lookup"><span data-stu-id="d1695-151">/model/Tables</span></span>  <br/> |<span data-ttu-id="d1695-152">Atom (Standard)</span><span class="sxs-lookup"><span data-stu-id="d1695-152">Atom (default)</span></span>  <br/> |<span data-ttu-id="d1695-153">/model/Tables?$format=atom</span><span class="sxs-lookup"><span data-stu-id="d1695-153">/model/Tables?$format=atom</span></span>  <br/> |<span data-ttu-id="d1695-154">Ein ATOM-Feed, der alle verfügbaren Tabellen in der Arbeitsmappe auflistet.</span><span class="sxs-lookup"><span data-stu-id="d1695-154">An Atom feed that lists all the available tables in the workbook.</span></span>  <br/> |
|<span data-ttu-id="d1695-155">/model/Tables('[Name]')</span><span class="sxs-lookup"><span data-stu-id="d1695-155">/model/Tables('[Name]')</span></span>  <br/> |<span data-ttu-id="d1695-156">HTML (Standard)</span><span class="sxs-lookup"><span data-stu-id="d1695-156">HTML (default)</span></span>  <br/> |<span data-ttu-id="d1695-157">/model/Tables('MyTable')?$format=html</span><span class="sxs-lookup"><span data-stu-id="d1695-157">/model/Tables('MyTable')?$format=html</span></span>  <br/> |<span data-ttu-id="d1695-158">Ein HTML-Fragment für die angeforderte Tabelle.</span><span class="sxs-lookup"><span data-stu-id="d1695-158">An HTML fragment for the requested table.</span></span>  <br/> |
|<span data-ttu-id="d1695-159">/model/Tables('[Name]')</span><span class="sxs-lookup"><span data-stu-id="d1695-159">/model/Tables('[Name]')</span></span>  <br/> |<span data-ttu-id="d1695-160">Atom</span><span class="sxs-lookup"><span data-stu-id="d1695-160">Atom</span></span>  <br/> |<span data-ttu-id="d1695-161">/model/Tables('MyTable')?$format=atom</span><span class="sxs-lookup"><span data-stu-id="d1695-161">/model/Tables('MyTable')?$format=atom</span></span>  <br/> |<span data-ttu-id="d1695-162">Ein ATOM-Eintrag, der eine XML-Darstellung der Daten in dieser Tabelle enthält.</span><span class="sxs-lookup"><span data-stu-id="d1695-162">An Atom entry that contains an XML representation of the data within the table.</span></span>  <br/> |
|<span data-ttu-id="d1695-163">/model/PivotTables</span><span class="sxs-lookup"><span data-stu-id="d1695-163">/model/PivotTables</span></span>  <br/> |<span data-ttu-id="d1695-164">Atom (Standard)</span><span class="sxs-lookup"><span data-stu-id="d1695-164">Atom (default)</span></span>  <br/> |<span data-ttu-id="d1695-165">/model/PivotTables?$format=atom</span><span class="sxs-lookup"><span data-stu-id="d1695-165">/model/PivotTables?$format=atom</span></span>  <br/> |<span data-ttu-id="d1695-166">Ein ATOM-Feed, der alle verfügbaren PivotTables in der Arbeitsmappe auflistet.</span><span class="sxs-lookup"><span data-stu-id="d1695-166">An Atom feed that lists all the available PivotTables in the workbook</span></span>  <br/> |
|<span data-ttu-id="d1695-167">/model/PivotTables('[Name]')</span><span class="sxs-lookup"><span data-stu-id="d1695-167">/model/PivotTables('[Name]')</span></span>  <br/> |<span data-ttu-id="d1695-168">HTML (Standard)</span><span class="sxs-lookup"><span data-stu-id="d1695-168">HTML (default)</span></span>  <br/> |<span data-ttu-id="d1695-169">/model/PivotTables('MyPivotTable)?$format=html</span><span class="sxs-lookup"><span data-stu-id="d1695-169">/model/PivotTables('MyPivotTable)?$format=html</span></span>  <br/> |<span data-ttu-id="d1695-170">Ein HTML-Fragment für die angeforderte PivotTable.</span><span class="sxs-lookup"><span data-stu-id="d1695-170">An HTML fragment for the requested PivotTable.</span></span>  <br/> |
|<span data-ttu-id="d1695-171">/model/PivotTables('[Name]')</span><span class="sxs-lookup"><span data-stu-id="d1695-171">/model/PivotTables('[Name]')</span></span>  <br/> |<span data-ttu-id="d1695-172">Atom</span><span class="sxs-lookup"><span data-stu-id="d1695-172">Atom</span></span>  <br/> |<span data-ttu-id="d1695-173">/model/PivotTables('MyPivotTable')?$format=atom</span><span class="sxs-lookup"><span data-stu-id="d1695-173">/model/PivotTables('MyPivotTable')?$format=atom</span></span>  <br/> |<span data-ttu-id="d1695-174">Ein Atom-Eintrag, der eine XML-Darstellung der Daten aus den PivotTables enthält.</span><span class="sxs-lookup"><span data-stu-id="d1695-174">An Atom entry that contains an XML representation of the data within the PivotTables.</span></span>  <br/> |
   
> [!NOTE]
> <span data-ttu-id="d1695-175">Excel Services begrenzt die Anzahl der Bereiche, die Sie in eine URL einfügen können auf 10.</span><span class="sxs-lookup"><span data-stu-id="d1695-175">Note: Excel Services limits the number of ranges that you can include in a URL to 10.</span></span> <span data-ttu-id="d1695-176">Wenn Sie mehr als 10 Bereiche in eine URL einfügen, erhalten Sie eine Fehlermeldung, die darauf hinweist, dass der Dienst nicht verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="d1695-176">If you include more than 10 Ranges in a URL, you will get an error that indicates that the service is unavailable.</span></span> 

## <a name="see-also"></a><span data-ttu-id="d1695-177">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="d1695-177">See also</span></span>

- [<span data-ttu-id="d1695-178">Grundlegende URI-Struktur und Pfad</span><span class="sxs-lookup"><span data-stu-id="d1695-178">Basic URI Structure and Path</span></span>](basic-uri-structure-and-path.md)
