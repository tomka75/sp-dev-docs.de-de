---
title: Anpassen von Suchergebnissen in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1b30f6df-643a-4570-ae5c-d3d8df5609b8
ms.openlocfilehash: 66856c768d51d8de633bc7419148aa9d8b48a7e8
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="customizing-search-results-in-sharepoint"></a><span data-ttu-id="f5940-102">Anpassen von Suchergebnissen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f5940-102">Customizing search results in SharePoint</span></span>
<span data-ttu-id="f5940-103">In diesem Artikel erfahren Sie, wie Sie in einem Suchergebnissatz in SharePoint ähnliche Elemente gruppieren oder doppelte Elemente entfernen, sodass die Ergebnisse übersichtlich und gut lesbar angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="f5940-103">Learn how to group similar items or remove duplicate items in a search result set in sps15short so you can display these results in a concise, readable way.</span></span>
<span data-ttu-id="f5940-104">In Suchergebnissen werden durch Gruppierung zwei oder mehr ähnliche Elemente in einem Suchergebnissatz reduziert, damit die Anzeige für einen Benutzer besser lesbar ist.</span><span class="sxs-lookup"><span data-stu-id="f5940-104">In search results, grouping collapses two or more similar items in a search result set to make their display more readable for a user.</span></span> <span data-ttu-id="f5940-105">Die Duplikatentfernung in Suchergebnissen ist Teil der Gruppierung; hierbei werden identische oder nahezu identische Elemente aus dem Resultset entfernt.</span><span class="sxs-lookup"><span data-stu-id="f5940-105">Duplicate removal of search results is a part of grouping, where items that are identical or nearly identical are removed from the result set.</span></span> <span data-ttu-id="f5940-106">Je nach den vom SharePoint-Administrator festgelegten Einstellungen kann der Benutzer möglicherweise die Suchergebnisse später erweitern und die einzelnen reduzierten Ergebnisse anzeigen.</span><span class="sxs-lookup"><span data-stu-id="f5940-106">Depending on the settings set by the SharePoint administrator, the user might be able to expand the search result set later and see the individual results that were collapsed.</span></span>
  
    
    

<span data-ttu-id="f5940-107">Im Folgenden sehen Sie Beispiele für Methoden zur Gruppierung von Suchergebnissen:</span><span class="sxs-lookup"><span data-stu-id="f5940-107">The following are examples of ways to group search results:</span></span>
- <span data-ttu-id="f5940-108">Duplikaterkennung - hierbei werden fast identische Dokumente aus dem Ergebnissatz entfernt.</span><span class="sxs-lookup"><span data-stu-id="f5940-108">Duplicate detection, where nearly identical documents are removed from the result set.</span></span>
    
  
- <span data-ttu-id="f5940-109">Websitereduzierung - hierbei wird nur das relevanteste Element jeder Website im Ergebnissatz angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f5940-109">Site collapsing, where only the most relevant item found in each site is shown in the result set.</span></span>
    
  
- <span data-ttu-id="f5940-110">Dokumentenmappenreduzierung - hierbei wird nur ein Treffer für jede Dokumentbibliothek in SharePoint angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f5940-110">Document set collapsing, where only one hit is displayed for each document library in SharePoint.</span></span>
    
  
<span data-ttu-id="f5940-111">Sie können die Kriterien zum Reduzieren oder zum Entfernen von Duplikaten programmgesteuert mithilfe der folgenden  [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx) -Eigenschaften im Abfrageobjektmodell angeben:</span><span class="sxs-lookup"><span data-stu-id="f5940-111">You can specify the criteria for collapsing or duplicate trimming programmatically by using the following  [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx) properties within the Query object model:</span></span>
-  [<span data-ttu-id="f5940-112">CollapseSpecification</span><span class="sxs-lookup"><span data-stu-id="f5940-112">CollapseSpecification</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.CollapseSpecification.aspx)
    
  
-  [<span data-ttu-id="f5940-113">TrimDuplicates</span><span class="sxs-lookup"><span data-stu-id="f5940-113">TrimDuplicates</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Query.TrimDuplicates.aspx)
    
  
-  [<span data-ttu-id="f5940-114">TrimDuplicatesOnProperty</span><span class="sxs-lookup"><span data-stu-id="f5940-114">TrimDuplicatesOnProperty</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.TrimDuplicatesOnProperty.aspx)
    
  
-  [<span data-ttu-id="f5940-115">TrimDuplicatesKeepCount</span><span class="sxs-lookup"><span data-stu-id="f5940-115">TrimDuplicatesKeepCount</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.TrimDuplicatesKeepCount.aspx)
    
  
-  [<span data-ttu-id="f5940-116">TrimDuplicatesIncludeId</span><span class="sxs-lookup"><span data-stu-id="f5940-116">TrimDuplicatesIncludeId</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.TrimDuplicatesIncludeId.aspx)
    
  

## <a name="collapse-similar-search-results-using-the-collapsespecification-property"></a><span data-ttu-id="f5940-117">Reduzieren ähnlicher Suchergebnisse mithilfe der CollapseSpecification-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="f5940-117">Collapse similar search results using the CollapseSpecification property</span></span>
<span data-ttu-id="f5940-118"><a name="bk_collapse_specification"> </a></span><span class="sxs-lookup"><span data-stu-id="f5940-118"></span></span>

<span data-ttu-id="f5940-119">Die **CollapseSpecification**-Eigenschaft verwendet einen  _Spec_-Parameter, der mehrere durch ein Komma oder ein Leerzeichen getrennte Felder enthalten kann, die bei gemeinsamer Auswertung einen Satz von Kriterien für den Reduziervorgang angeben.</span><span class="sxs-lookup"><span data-stu-id="f5940-119">The **CollapseSpecification** property takes a _Spec_ parameter that can contain multiple fields separated either by a comma or a space, which evaluated together specify a set of criteria used for collapsing.</span></span>
  
    
    
 <span data-ttu-id="f5940-120">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="f5940-120">**Syntax**</span></span>
  
    
    
 `CollapseSpecification = Spec`
  
    
    
<span data-ttu-id="f5940-121">Die folgende Tabelle enthält die Felder des  _Spec_-Parameters.</span><span class="sxs-lookup"><span data-stu-id="f5940-121">The following table lists the fields of the  _Spec_ parameter.</span></span>
  
    
    

<span data-ttu-id="f5940-122">**Tabelle 1. Felder des Spec-Parameters**</span><span class="sxs-lookup"><span data-stu-id="f5940-122">**Table 1. Spec parameter fields**</span></span>


|<span data-ttu-id="f5940-123">**Element in Parameter**</span><span class="sxs-lookup"><span data-stu-id="f5940-123">**Element in parameter**</span></span>|<span data-ttu-id="f5940-124">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="f5940-124">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="f5940-125">_Spec_</span><span class="sxs-lookup"><span data-stu-id="f5940-125">_Spec_</span></span> <br/> | `Subspec(<space>Subspec)*` <br/> |
| <span data-ttu-id="f5940-126">_Subspec_</span><span class="sxs-lookup"><span data-stu-id="f5940-126">_Subspec_</span></span> <br/> | `Prop(','Prop)*[':'Dups]` <br/> |
| <span data-ttu-id="f5940-127">_Prop_</span><span class="sxs-lookup"><span data-stu-id="f5940-127">_Prop_</span></span> <br/> |<span data-ttu-id="f5940-p102">Eine gültige verwaltete Eigenschaft oder ein Alias einer verwalteten Eigenschaft. Bei  _Prop_ wird die Groß-/Kleinschreibung nicht beachtet. Die verwaltete Eigenschaft muss abfragbar und entweder sortier- oder einschränkbar sein.</span><span class="sxs-lookup"><span data-stu-id="f5940-p102">A valid managed property or an alias of a managed property.  _Prop_ is case-insensitive. The managed property must be queryable and either sortable or refineable. </span></span><br/> |
| <span data-ttu-id="f5940-131">_Dups_</span><span class="sxs-lookup"><span data-stu-id="f5940-131">_Dups_</span></span> <br/> |<span data-ttu-id="f5940-p103">Eine ganze Zahl, die die Anzahl der beizubehaltenden Elemente angibt. Der Standardwert ist 1.</span><span class="sxs-lookup"><span data-stu-id="f5940-p103">An integer specifying the number of items to retain. The default value is 1.</span></span>  <br/> |
| _<space>_ <br/> |<span data-ttu-id="f5940-134">Eigenschaften werden mit dem **OR**-Operator kombiniert.</span><span class="sxs-lookup"><span data-stu-id="f5940-134">Properties are combined by using the **OR** operator.</span></span> <br/> |
| <span data-ttu-id="f5940-135">_,_</span><span class="sxs-lookup"><span data-stu-id="f5940-135"></span></span> <br/> |<span data-ttu-id="f5940-136">Eigenschaften werden mit dem **AND**-Operator kombiniert.</span><span class="sxs-lookup"><span data-stu-id="f5940-136">Properties are combined by using the **AND** operator.</span></span> <br/> |
| _*_ <br/> |<span data-ttu-id="f5940-137">Gibt mehr Elemente an.</span><span class="sxs-lookup"><span data-stu-id="f5940-137">Indicates more items.</span></span>  <br/> |
| <span data-ttu-id="f5940-138">_() or []_</span><span class="sxs-lookup"><span data-stu-id="f5940-138">_() or []_</span></span> <br/> |<span data-ttu-id="f5940-139">Gibt optionale Elemente an.</span><span class="sxs-lookup"><span data-stu-id="f5940-139">Indicates optional items.</span></span>  <br/> |
   
<span data-ttu-id="f5940-p104">Wenn die Felder in  _Spec_ durch Kommas getrennt sind, werden die Felder mit dem **AND**-Operator kombiniert. Wenn alle angegebenen Felder erfüllt sind, werden die Elemente reduziert.</span><span class="sxs-lookup"><span data-stu-id="f5940-p104">If the fields in  _Spec_ are separated by commas, the fields are combined by using the **AND** operator. If all of the specified fields are matched, the items are collapsed.</span></span>
  
    
    
<span data-ttu-id="f5940-p105">Wenn hingegen die Felder in  _Spec_ durch Leerzeichen getrennt sind, werden die Felder (oder _Subspecs_) unter Verwendung einer Erweiterung kombiniert, die den **AND**-Operator und den **OR**-Operator enthält. Beispiel: Ein Ausdruck wie  `Category:3 Product:2` wird intern in den Ausdruck `(Category AND Product) OR (Category)` mit einem Zähler für jedes Element transformiert; hier ein Maximum von zwei für das erste und drei für das letzte Element. Elemente werden reduziert, wenn einige der angegebenen Felder erfüllt sind.</span><span class="sxs-lookup"><span data-stu-id="f5940-p105">In contrast, if the fields in  _Spec_ are separated by spaces, the fields (or _Subspecs_) are combined by using an expansion that includes both the **AND** operator and **OR** operator. For example, an expression such as `Category:3 Product:2` is internally transformed to the following expression `(Category AND Product) OR (Category)` with a counter for each; hence a maximum of two of the former and three of the latter. Items are collapsed if some of the specified fields are matched.</span></span>
  
    
    

### <a name="examples-of-using-collapsespecification"></a><span data-ttu-id="f5940-145">Beispiele für die Verwendung von CollapseSpecification</span><span class="sxs-lookup"><span data-stu-id="f5940-145">Examples of using CollapseSpecification</span></span>

<span data-ttu-id="f5940-p106">Die folgende Tabelle enthält einen Produktkatalog der Firma Contoso. In den nächsten Beispielen wird anhand dieses Katalogs die Funktionsweise der **CollapseSpecification**-Eigenschaft veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="f5940-p106">The following table shows a product catalog from the Contoso company. The next set of examples use this catalog to show how the **CollapseSpecification** property works.</span></span>
  
    
    


|<span data-ttu-id="f5940-148">**Kategorie**</span><span class="sxs-lookup"><span data-stu-id="f5940-148">**Category**</span></span>|<span data-ttu-id="f5940-149">**Product**</span><span class="sxs-lookup"><span data-stu-id="f5940-149">**Product**</span></span>|<span data-ttu-id="f5940-150">**Variant**</span><span class="sxs-lookup"><span data-stu-id="f5940-150">**Variant**</span></span>|<span data-ttu-id="f5940-151">**Title**</span><span class="sxs-lookup"><span data-stu-id="f5940-151">**Title**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="f5940-152">Laptops</span><span class="sxs-lookup"><span data-stu-id="f5940-152">Laptops</span></span>  <br/> |<span data-ttu-id="f5940-153">WWI</span><span class="sxs-lookup"><span data-stu-id="f5940-153">WWI</span></span>  <br/> |<span data-ttu-id="f5940-154">19W X0196 Black</span><span class="sxs-lookup"><span data-stu-id="f5940-154">19W X0196 Black</span></span>  <br/> |<span data-ttu-id="f5940-155">Computer 1</span><span class="sxs-lookup"><span data-stu-id="f5940-155">Computer 1</span></span>  <br/> |
|<span data-ttu-id="f5940-156">Laptops</span><span class="sxs-lookup"><span data-stu-id="f5940-156">Laptops</span></span>  <br/> |<span data-ttu-id="f5940-157">Adventure Works</span><span class="sxs-lookup"><span data-stu-id="f5940-157">Adventure Works</span></span>  <br/> |<span data-ttu-id="f5940-158">12 M1201 Red</span><span class="sxs-lookup"><span data-stu-id="f5940-158">12 M1201 Red</span></span>  <br/> |<span data-ttu-id="f5940-159">Computer 2</span><span class="sxs-lookup"><span data-stu-id="f5940-159">Computer 2</span></span>  <br/> |
|<span data-ttu-id="f5940-160">Laptops</span><span class="sxs-lookup"><span data-stu-id="f5940-160">Laptops</span></span>  <br/> |<span data-ttu-id="f5940-161">Adventure Works</span><span class="sxs-lookup"><span data-stu-id="f5940-161">Adventure Works</span></span>  <br/> |<span data-ttu-id="f5940-162">15.4W M1548 White</span><span class="sxs-lookup"><span data-stu-id="f5940-162">15.4W M1548 White</span></span>  <br/> |<span data-ttu-id="f5940-163">Computer 3</span><span class="sxs-lookup"><span data-stu-id="f5940-163">Computer 3</span></span>  <br/> |
|<span data-ttu-id="f5940-164">Laptops</span><span class="sxs-lookup"><span data-stu-id="f5940-164">Laptops</span></span>  <br/> |<span data-ttu-id="f5940-165">Proseware</span><span class="sxs-lookup"><span data-stu-id="f5940-165">Proseware</span></span>  <br/> |<span data-ttu-id="f5940-166">19 X910 Black</span><span class="sxs-lookup"><span data-stu-id="f5940-166">19 X910 Black</span></span>  <br/> |<span data-ttu-id="f5940-167">Computer 4</span><span class="sxs-lookup"><span data-stu-id="f5940-167">Computer 4</span></span>  <br/> |
|<span data-ttu-id="f5940-168">Laptops</span><span class="sxs-lookup"><span data-stu-id="f5940-168">Laptops</span></span>  <br/> |<span data-ttu-id="f5940-169">Proseware</span><span class="sxs-lookup"><span data-stu-id="f5940-169">Proseware</span></span>  <br/> |<span data-ttu-id="f5940-170">Laptop19 X910 Black</span><span class="sxs-lookup"><span data-stu-id="f5940-170">Laptop19 X910 Black</span></span>  <br/> |<span data-ttu-id="f5940-171">Computer 5</span><span class="sxs-lookup"><span data-stu-id="f5940-171">Computer 5</span></span>  <br/> |
|<span data-ttu-id="f5940-172">Desktops</span><span class="sxs-lookup"><span data-stu-id="f5940-172">Desktops</span></span>  <br/> |<span data-ttu-id="f5940-173">Adventure Works</span><span class="sxs-lookup"><span data-stu-id="f5940-173">Adventure Works</span></span>  <br/> |<span data-ttu-id="f5940-174">2.33 XD233 Silver</span><span class="sxs-lookup"><span data-stu-id="f5940-174">2.33 XD233 Silver</span></span>  <br/> |<span data-ttu-id="f5940-175">Computer 6</span><span class="sxs-lookup"><span data-stu-id="f5940-175">Computer 6</span></span>  <br/> |
|<span data-ttu-id="f5940-176">Desktops</span><span class="sxs-lookup"><span data-stu-id="f5940-176">Desktops</span></span>  <br/> |<span data-ttu-id="f5940-177">WWI</span><span class="sxs-lookup"><span data-stu-id="f5940-177">WWI</span></span>  <br/> |<span data-ttu-id="f5940-178">2.33 X2330 Black</span><span class="sxs-lookup"><span data-stu-id="f5940-178">2.33 X2330 Black</span></span>  <br/> |<span data-ttu-id="f5940-179">Computer 7</span><span class="sxs-lookup"><span data-stu-id="f5940-179">Computer 7</span></span>  <br/> |
|<span data-ttu-id="f5940-180">Desktops</span><span class="sxs-lookup"><span data-stu-id="f5940-180">Desktops</span></span>  <br/> |<span data-ttu-id="f5940-181">Adventure Works</span><span class="sxs-lookup"><span data-stu-id="f5940-181">Adventure Works</span></span>  <br/> |<span data-ttu-id="f5940-182">1.60 ED160 White</span><span class="sxs-lookup"><span data-stu-id="f5940-182">1.60 ED160 White</span></span>  <br/> |<span data-ttu-id="f5940-183">Computer 8</span><span class="sxs-lookup"><span data-stu-id="f5940-183">Computer 8</span></span>  <br/> |
|<span data-ttu-id="f5940-184">Desktops</span><span class="sxs-lookup"><span data-stu-id="f5940-184">Desktops</span></span>  <br/> |<span data-ttu-id="f5940-185">WWI</span><span class="sxs-lookup"><span data-stu-id="f5940-185">WWI</span></span>  <br/> |<span data-ttu-id="f5940-186">3.0 M0300 Silver</span><span class="sxs-lookup"><span data-stu-id="f5940-186">3.0 M0300 Silver</span></span>  <br/> |<span data-ttu-id="f5940-187">Computer 9</span><span class="sxs-lookup"><span data-stu-id="f5940-187">Computer 9</span></span>  <br/> |
   

  
    
    

#### <a name="example-group-by-category"></a><span data-ttu-id="f5940-188">Beispiel: Gruppieren nach Category</span><span class="sxs-lookup"><span data-stu-id="f5940-188">Example: group by Category</span></span>

<span data-ttu-id="f5940-p107">Gruppieren Sie zunächst die Elemente nach **Category**, und zeigen Sie die zwei obersten für jede Gruppe an (also  `"Category:2"`). Zeigen Sie dann für jede **Category** eine entsprechende Anzahl eindeutiger **Products** an (also "Product:1").</span><span class="sxs-lookup"><span data-stu-id="f5940-p107">First, group the items based on **Category** and show the top two (hence `"Category:2"`) for each group. Then, for each **Category**, show a corresponding number of unique (hence "Product:1") **Products**.</span></span>
  
    
    
 <span data-ttu-id="f5940-191">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="f5940-191">**Syntax**</span></span>
  
    
    
 `CollapseSpecification="Category:2 Product:1"`
  
    
    
<span data-ttu-id="f5940-192">Die folgenden Ergebnisse sollten zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="f5940-192">This should return the following results.</span></span>
  
    
    


|<span data-ttu-id="f5940-193">**Kategorie**</span><span class="sxs-lookup"><span data-stu-id="f5940-193">**Category**</span></span>|<span data-ttu-id="f5940-194">**Product**</span><span class="sxs-lookup"><span data-stu-id="f5940-194">**Product**</span></span>|<span data-ttu-id="f5940-195">**Variant**</span><span class="sxs-lookup"><span data-stu-id="f5940-195">**Variant**</span></span>|<span data-ttu-id="f5940-196">**Title**</span><span class="sxs-lookup"><span data-stu-id="f5940-196">**Title**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="f5940-197">Laptops</span><span class="sxs-lookup"><span data-stu-id="f5940-197">Laptops</span></span>  <br/> |<span data-ttu-id="f5940-198">WWI</span><span class="sxs-lookup"><span data-stu-id="f5940-198">WWI</span></span>  <br/> |<span data-ttu-id="f5940-199">19W X0196 Black</span><span class="sxs-lookup"><span data-stu-id="f5940-199">19W X0196 Black</span></span>  <br/> |<span data-ttu-id="f5940-200">Computer 1</span><span class="sxs-lookup"><span data-stu-id="f5940-200">Computer 1</span></span>  <br/> |
|<span data-ttu-id="f5940-201">Laptops</span><span class="sxs-lookup"><span data-stu-id="f5940-201">Laptops</span></span>  <br/> |<span data-ttu-id="f5940-202">Adventure</span><span class="sxs-lookup"><span data-stu-id="f5940-202">Adventure</span></span>  <br/> |<span data-ttu-id="f5940-203">12 M1201 Red</span><span class="sxs-lookup"><span data-stu-id="f5940-203">12 M1201 Red</span></span>  <br/> |<span data-ttu-id="f5940-204">Computer 2</span><span class="sxs-lookup"><span data-stu-id="f5940-204">Computer 2</span></span>  <br/> |
|<span data-ttu-id="f5940-205">Desktops</span><span class="sxs-lookup"><span data-stu-id="f5940-205">Desktops</span></span>  <br/> |<span data-ttu-id="f5940-206">Adventure Works</span><span class="sxs-lookup"><span data-stu-id="f5940-206">Adventure Works</span></span>  <br/> |<span data-ttu-id="f5940-207">2.33 XD233 Silver</span><span class="sxs-lookup"><span data-stu-id="f5940-207">2.33 XD233 Silver</span></span>  <br/> |<span data-ttu-id="f5940-208">Computer 6</span><span class="sxs-lookup"><span data-stu-id="f5940-208">Computer 6</span></span>  <br/> |
|<span data-ttu-id="f5940-209">Desktops</span><span class="sxs-lookup"><span data-stu-id="f5940-209">Desktops</span></span>  <br/> |<span data-ttu-id="f5940-210">WWI</span><span class="sxs-lookup"><span data-stu-id="f5940-210">WWI</span></span>  <br/> |<span data-ttu-id="f5940-211">2.33 X2330 Black</span><span class="sxs-lookup"><span data-stu-id="f5940-211">2.33 X2330 Black</span></span>  <br/> |<span data-ttu-id="f5940-212">Computer 7</span><span class="sxs-lookup"><span data-stu-id="f5940-212">Computer 7</span></span>  <br/> |
   
<span data-ttu-id="f5940-213">Verwenden Sie den folgenden Code, um die Suchergebnisse mithilfe der **CollapseSpecification**-Eigenschaft zu reduzieren.</span><span class="sxs-lookup"><span data-stu-id="f5940-213">Use the following code to collapse the search results by using the **CollapseSpecification** property.</span></span>
  
    
    



```cs

using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
        {
            QueryText = "Title:Computer",
            CollapseSpecification = "Category:3 Product:1",
        };

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    {
        Console.WriteLine(result["Title"]);
    }
}

```


#### <a name="example-group-by-category-and-product"></a><span data-ttu-id="f5940-214">Beispiel: Gruppieren nach Category und Product</span><span class="sxs-lookup"><span data-stu-id="f5940-214">Example: group by Category and Product</span></span>

<span data-ttu-id="f5940-p108">Gruppieren Sie zunächst die Elemente nach **Category** und nach **Product**. Zeigen Sie anschließend jede eindeutige Kombination an.</span><span class="sxs-lookup"><span data-stu-id="f5940-p108">First, group the items based on both **Category** and **Product**. Then, show each unique combination.</span></span>
  
    
    
 <span data-ttu-id="f5940-217">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="f5940-217">**Syntax**</span></span>
  
    
    
 `CollapseSpecification="Category,Product:1"`
  
    
    
<span data-ttu-id="f5940-218">Die folgenden Ergebnisse sollten zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="f5940-218">This should return the following results.</span></span>
  
    
    


|<span data-ttu-id="f5940-219">**Kategorie**</span><span class="sxs-lookup"><span data-stu-id="f5940-219">**Category**</span></span>|<span data-ttu-id="f5940-220">**Product**</span><span class="sxs-lookup"><span data-stu-id="f5940-220">**Product**</span></span>|<span data-ttu-id="f5940-221">**Variant**</span><span class="sxs-lookup"><span data-stu-id="f5940-221">**Variant**</span></span>|<span data-ttu-id="f5940-222">**Title**</span><span class="sxs-lookup"><span data-stu-id="f5940-222">**Title**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="f5940-223">Laptops</span><span class="sxs-lookup"><span data-stu-id="f5940-223">Laptops</span></span>  <br/> |<span data-ttu-id="f5940-224">WWI</span><span class="sxs-lookup"><span data-stu-id="f5940-224">WWI</span></span>  <br/> |<span data-ttu-id="f5940-225">19W X0196 Black</span><span class="sxs-lookup"><span data-stu-id="f5940-225">19W X0196 Black</span></span>  <br/> |<span data-ttu-id="f5940-226">Computer 1</span><span class="sxs-lookup"><span data-stu-id="f5940-226">Computer 1</span></span>  <br/> |
|<span data-ttu-id="f5940-227">Laptops</span><span class="sxs-lookup"><span data-stu-id="f5940-227">Laptops</span></span>  <br/> |<span data-ttu-id="f5940-228">Adventure Works</span><span class="sxs-lookup"><span data-stu-id="f5940-228">Adventure Works</span></span>  <br/> |<span data-ttu-id="f5940-229">12 M1201 Red</span><span class="sxs-lookup"><span data-stu-id="f5940-229">12 M1201 Red</span></span>  <br/> |<span data-ttu-id="f5940-230">Computer 2</span><span class="sxs-lookup"><span data-stu-id="f5940-230">Computer 2</span></span>  <br/> |
|<span data-ttu-id="f5940-231">Laptops</span><span class="sxs-lookup"><span data-stu-id="f5940-231">Laptops</span></span>  <br/> |<span data-ttu-id="f5940-232">Proseware</span><span class="sxs-lookup"><span data-stu-id="f5940-232">Proseware</span></span>  <br/> |<span data-ttu-id="f5940-233">19 X910 Black</span><span class="sxs-lookup"><span data-stu-id="f5940-233">19 X910 Black</span></span>  <br/> |<span data-ttu-id="f5940-234">Computer 4</span><span class="sxs-lookup"><span data-stu-id="f5940-234">Computer 4</span></span>  <br/> |
|<span data-ttu-id="f5940-235">Desktops</span><span class="sxs-lookup"><span data-stu-id="f5940-235">Desktops</span></span>  <br/> |<span data-ttu-id="f5940-236">Adventure Works</span><span class="sxs-lookup"><span data-stu-id="f5940-236">Adventure Works</span></span>  <br/> |<span data-ttu-id="f5940-237">2.33 XD233 Silver</span><span class="sxs-lookup"><span data-stu-id="f5940-237">2.33 XD233 Silver</span></span>  <br/> |<span data-ttu-id="f5940-238">Computer 6</span><span class="sxs-lookup"><span data-stu-id="f5940-238">Computer 6</span></span>  <br/> |
|<span data-ttu-id="f5940-239">Desktops</span><span class="sxs-lookup"><span data-stu-id="f5940-239">Desktops</span></span>  <br/> |<span data-ttu-id="f5940-240">WWI</span><span class="sxs-lookup"><span data-stu-id="f5940-240">WWI</span></span>  <br/> |<span data-ttu-id="f5940-241">2.33 X2330 Black</span><span class="sxs-lookup"><span data-stu-id="f5940-241">2.33 X2330 Black</span></span>  <br/> |<span data-ttu-id="f5940-242">Computer 7</span><span class="sxs-lookup"><span data-stu-id="f5940-242">Computer 7</span></span>  <br/> |
   

## <a name="trim-duplicate-search-results-using-the-trimduplicates-property"></a><span data-ttu-id="f5940-243">Entfernen doppelter Suchergebnisse mithilfe der TrimDuplicates-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="f5940-243">Trim duplicate search results using the TrimDuplicates property</span></span>
<span data-ttu-id="f5940-244"><a name="bk_trim_duplicates"> </a></span><span class="sxs-lookup"><span data-stu-id="f5940-244"></span></span>

<span data-ttu-id="f5940-p109">Verwenden Sie **TrimDuplicates**, um anzugeben, ob die doppelten Suchergebnisse aus dem Suchergebnissatz entfernt werden sollen. **TrimDuplicates** ist standardmäßig auf **true** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="f5940-p109">Use **TrimDuplicates** to specify whether to trim away the duplicate search results from the result set. **TrimDuplicates** is **true** by default.</span></span>
  
    
    
<span data-ttu-id="f5940-247">Wenn Sie **TrimDuplicates** mit **TrimDuplicatesOnProperty** oder vorzugsweise mit **CollapseSpecification** verwenden, wird **TrimDuplicates** auf **false** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="f5940-247">If you use **TrimDuplicates** with either **TrimDuplicatesOnProperty** or preferably **CollapseSpecification**, **TrimDuplicates** is set to **false**.</span></span>
  
    
    
 <span data-ttu-id="f5940-248">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="f5940-248">**Syntax**</span></span>
  
    
    
 `TrimDuplicates = <$true | $false>`
  
    
    

### <a name="trim-duplicate-search-results-using-the-trimduplicatesonproperty-property"></a><span data-ttu-id="f5940-249">Entfernen doppelter Suchergebnisse mithilfe der TrimDuplicatesOnProperty-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="f5940-249">Trim duplicate search results using the TrimDuplicatesOnProperty property</span></span>
<span data-ttu-id="f5940-250"><a name="bk_trim_duplicates_on_property"> </a></span><span class="sxs-lookup"><span data-stu-id="f5940-250"></span></span>

<span data-ttu-id="f5940-p110">Verwenden Sie **TrimDuplicatesOnProperty**, um anzugeben, ob eine nicht standardmäßige verwaltete Eigenschaft als Basis für das Entfernen von Duplikaten verwendet werden soll. Der Standardwert ist die verwaltete Eigenschaft **DocumentSignature**. Die verwaltete Eigenschaft muss den Typ **Integer** oder **String** aufweisen. Indem Sie eine verwaltete Eigenschaft verwenden, die eine Elementgruppe darstellt, können Sie dieses Feature zum Reduzieren von Feldern nutzen.</span><span class="sxs-lookup"><span data-stu-id="f5940-p110">Use **TrimDuplicatesOnProperty** to specify whether to use a non-default managed property as the basis for duplicate trimming. The default value is the **DocumentSignature** managed property. The managed property must be of type **Integer** or **String**. By using a managed property that represents a grouping of items, you can use this feature for field collapsing.</span></span>
  
    
    
 <span data-ttu-id="f5940-255">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="f5940-255">**Syntax**</span></span>
  
    
    
 `TrimDuplicatesOnProperty = <managed property>`
  
    
    

> <span data-ttu-id="f5940-256">**Hinweis:** Verwenden Sie in SharePoint nach Möglichkeit **CollapseSpecification**.</span><span class="sxs-lookup"><span data-stu-id="f5940-256">**Note** In SharePoint Server 2013, use **CollapseSpecification** wherever possible. TrimDuplicatesOnProperty is available for backward compatibility only.</span></span> <span data-ttu-id="f5940-257">**TrimDuplicatesOnProperty** steht nur für Abwärtskompatibilität zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="f5940-257">In sps15short, use **CollapseSpecification** wherever possible. TrimDuplicatesOnProperty is available for backward compatibility only.</span></span>
  
    
    


### <a name="trim-duplicate-search-results-using-the-trimduplicateskeepcount-property"></a><span data-ttu-id="f5940-258">Kürzen doppelter Suchergebnisse mithilfe der Eigenschaft „TrimDuplicatesKeepCount“</span><span class="sxs-lookup"><span data-stu-id="f5940-258">Trim duplicate search results using the TrimDuplicatesKeepCount property</span></span>
<span data-ttu-id="f5940-259"><a name="bk_trim_duplicates_keep_count"> </a></span><span class="sxs-lookup"><span data-stu-id="f5940-259"></span></span>

<span data-ttu-id="f5940-p112">Verwenden Sie **TrimDuplicatesKeepCount**, um die Anzahl der beizubehaltenden Dokumente anzugeben, wenn **TrimDuplicates** auf **true** festgelegt ist. Wenn **TrimDuplicates** auf einer verwalteten Eigenschaft basiert, die als Gruppenbezeichner verwendet werden kann, z. B. eine Website-ID, können Sie steuern, wie viele Ergebnisse für jede Gruppe zurückgegeben werden. Zurückgegeben werden die Elemente mit dem höchsten dynamischen Rang in jeder Gruppe.</span><span class="sxs-lookup"><span data-stu-id="f5940-p112">Use **TrimDuplicatesKeepCount** to specify the number of documents to retain when **TrimDuplicates** is **true**. If **TrimDuplicates** is based on a managed property that can be used as a group identifier, for example a site ID, you can control how many results are returned for each group. The items returned are those with the highest dynamic rank within each group.</span></span>
  
    
    
 <span data-ttu-id="f5940-263">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="f5940-263">**Syntax**</span></span>
  
    
    
 `TrimDuplicatesKeepCount = <number>`
  
    
    

### <a name="retrieve-duplicate-search-results-using-the-trimduplicatesincludeid-property"></a><span data-ttu-id="f5940-264">Abrufen doppelter Suchergebnisse mithilfe der TrimDuplicatesIncludeId-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="f5940-264">Retrieve duplicate search results using the TrimDuplicatesIncludeId property</span></span>
<span data-ttu-id="f5940-265"><a name="bk_trim_duplicates_include_id"> </a></span><span class="sxs-lookup"><span data-stu-id="f5940-265"></span></span>

<span data-ttu-id="f5940-266">Verwenden Sie **TrimDuplicatesIncludeId**, um die Duplikate eines Dokuments abzurufen, wenn **TrimDuplicates** auf **true** und **TrimDuplicatesOnProperty** oder **CollapseSpecification** auf **false** festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="f5940-266">Use **TrimDuplicatesIncludeId** to retrieve the duplicates of a document when **TrimDuplicates** is **true** and **TrimDuplicatesOnProperty** or **CollapseSpecification** is set to **false**.</span></span>
  
    
    
<span data-ttu-id="f5940-267">Die Dokument-ID ( _docid_) wird zum Abrufen der Duplikate eines bestimmten Dokuments verwendet.</span><span class="sxs-lookup"><span data-stu-id="f5940-267">The document ID,  _docid_, is used to retrieve the duplicates of a particular document.</span></span>
  
    
    
 <span data-ttu-id="f5940-268">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="f5940-268">**Syntax**</span></span>
  
    
    
 `TrimDuplicatesIncludeId = <docid>`
  
    
    

> <span data-ttu-id="f5940-269">**Hinweis:** Die verwaltete Eigenschaft _fcoid_ in FAST Search Server 2010 for SharePoint wurde durch die verwaltete Eigenschaft _docid_ in SharePoint ersetzt.</span><span class="sxs-lookup"><span data-stu-id="f5940-269">**Note** The  _fcoid_ managed property in FAST Search Server 2010 for SharePoint has been replaced with the _docid_ managed property in SharePoint Server 2013.</span></span>
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="f5940-270">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f5940-270">Additional resources</span></span>
<span data-ttu-id="f5940-271"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f5940-271"></span></span>


-  [<span data-ttu-id="f5940-272">KeywordQuery</span><span class="sxs-lookup"><span data-stu-id="f5940-272">KeywordQuery</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx)
    
  
-  <span data-ttu-id="f5940-273">
  [Übersicht über das Suchschema in SharePoint Server 2013](http://technet.microsoft.com/de-de/library/jj219669%28office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="f5940-273">[Overview of the search schema in SharePoint](http://technet.microsoft.com/de-de/library/jj219669%28office.15%29.aspx)</span></span>
    
  

  
    
    

