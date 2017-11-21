---
title: "Nicht unterstützte Features in Excel Services-REST-API"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4139901f-255b-4556-b8c8-3d986a07c587
ms.openlocfilehash: ca6b94c9743c251acd034cfd42126bbec623163c
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="unsupported-features-in-excel-services-rest-api"></a><span data-ttu-id="a2f4b-102">Nicht unterstützte Features in Excel Services-REST-API</span><span class="sxs-lookup"><span data-stu-id="a2f4b-102">Unsupported Features in Excel Services REST API</span></span>

<span data-ttu-id="a2f4b-103">Die erste Version der Excel Services-REST-API unterstützt nicht alle Excel-Features.</span><span class="sxs-lookup"><span data-stu-id="a2f4b-103">The first version of the Excel Services REST API does not support every Excel feature.</span></span> 
  
    
    


> <span data-ttu-id="a2f4b-104">**Hinweis:** Die Excel Services-REST-API bezieht sich auf SharePoint und SharePoint 2016 (lokal).</span><span class="sxs-lookup"><span data-stu-id="a2f4b-104">**Note:** The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="a2f4b-105">Für Office 365 Education-, Business- und Enterprise-Konten verwenden Sie die Excel-REST-APIs, die Bestandteil des [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
> )-Endpunkts sind.</span><span class="sxs-lookup"><span data-stu-id="a2f4b-105">Note The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises. For Office 365 Education, Business, and Enterprise accounts, use the Excel REST APIs that are part of the  [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
) endpoint.</span></span>
  
    
    


<span data-ttu-id="a2f4b-106">Es folgt eine partielle Liste einiger wichtiger Features, die derzeit nicht unterstützt werden oder in der REST-API Excel Services arbeiten:</span><span class="sxs-lookup"><span data-stu-id="a2f4b-106">Following is a partial list of some of the more important features that are currently not supported or working in the Excel Services REST API:</span></span>
  
    
    


- <span data-ttu-id="a2f4b-p102">**Keine unverankerten Diagramme.** Wenn ein Bereich ein Diagramm enthält und Sie den Bereich über REST anfordern, erhalten Sie nur den Bereich.</span><span class="sxs-lookup"><span data-stu-id="a2f4b-p102">**No floating charts.** If a range contains a chart, and you request the range through REST, you get only the range.</span></span>
    
  
- <span data-ttu-id="a2f4b-p103">**Keine Sparklines, keine bedingte Formatierung für Symbole.** Derzeit nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="a2f4b-p103">**No sparklines, no icon conditional formatting.** Currently not supported.</span></span>
    
  
- <span data-ttu-id="a2f4b-p104">**Keine Pixelperfektion mit EWA.** Das von REST produzierte HTML ist dem von Excel Web Access produzierten HTML sehr ähnlich. Mit der REST-API in Excel Services kann jedoch nicht auf alle CSS-Elemente (Cascading Stylesheets) zugegriffen werden, auf die Excel Web Access Zugriff hat. Die REST-API in Excel Services gibt ein HTML-Fragment zurück. Das HTML-Fragment muss eigenständig sein.</span><span class="sxs-lookup"><span data-stu-id="a2f4b-p104">**Not pixel-perfect with EWA.** The HTML that REST produces is very close to the HTML that Excel Web Access produces. However, the Excel Services REST API cannot access all the Cascading Style Sheets (CSS) elements that Excel Web Access can access. The Excel Services REST API returns an HTML fragment. The HTML fragment must be self-contained.</span></span>
    
  
- <span data-ttu-id="a2f4b-p105">**Keine Unterscheidung in Tabellen.** Wenn eine Tabelle als ATOM angefordert wird, kann nicht festgestellt werden, ob es sich bei der Zelle oder den Daten um eine Spaltenüberschrift, eine Summe oder allgemeine Daten handelt. In der Tabelle wird diesbezüglich nämlich keine Unterscheidung gemacht. Alle Tabellenzeilen in der gesamten Tabelle werden gleich behandelt.</span><span class="sxs-lookup"><span data-stu-id="a2f4b-p105">**No distinction in tables.** When a table is requested as Atom to see whether the cell or data is a column head, a total or general data, there is no distinction made in the table. That is, there is no distinction that specifies whether a cell or data is a header, a total or just general data. All table cells throughout a table are treated equally.</span></span>
    
  
- <span data-ttu-id="a2f4b-p106">**URL-Größenbeschränkungen.** Die URL-Größe ist auf etwa 2000 Zeichen begrenzt. Das heißt, wenn in einer Arbeitsmappe sehr viele Parameter vorhanden sind, können Sie möglicherweise nicht alle Parameter festlegen. Dies gilt insbesondere, wenn die Arbeitsmappe tief in der Hierarchie einer Ordnerstruktur angeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="a2f4b-p106">**URL size limits.** URL size is limited to approximately 2000 characters. This means that, if you have a large number of parameters in a workbook, you may not be able to set all of them. This is especially so if the workbook is located deep in a folder structure.</span></span>
    
  
- <span data-ttu-id="a2f4b-p107">**Sonderzeichen.** Zeichen wie "?" und "#" werden nicht unterstützt. Um ordnungsgemäß auf Blattnamen zu verweisen, die Sonderzeichen enthalten, gilt die Grundregel "Feststellen, was der Excel-Client macht", wenn Sie in einer Formel auf ein Blatt mit Sonderzeichen verweisen, und diesem Beispiel folgen.</span><span class="sxs-lookup"><span data-stu-id="a2f4b-p107">**Special characters.** Characters like "?" and "#" are unsupported. To correctly reference sheet names that contain special characters, the basic guideline is "see what the Excel client does" when referencing a formula to a sheet with special characters and follow that example.</span></span>
    
  

