---
title: "Syntax für Trigger Ausdrücken in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: bb466b4bff566808c970b4015815fd94651aff43
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="trigger-expressions-syntax-in-sharepoint"></a><span data-ttu-id="f097f-102">Syntax von Triggerausdrücken in SharePoint</span><span class="sxs-lookup"><span data-stu-id="f097f-102">Trigger expressions syntax in SharePoint</span></span>
<span data-ttu-id="f097f-103">Dieser Artikel beschreibt Triggerausdrücke, mit denen Sie Triggerbedingungen zur Konfiguration von Webdienstcallouts in SharePoint erstellen können.</span><span class="sxs-lookup"><span data-stu-id="f097f-103">Learn about trigger expressions you can use to create trigger conditions to configure the web service callout in SharePoint Server 2013.</span></span> 
## <a name="elements-used-in-the-syntax-of-trigger-expressions"></a><span data-ttu-id="f097f-104">Elemente in der Syntax von Triggerausdrücken</span><span class="sxs-lookup"><span data-stu-id="f097f-104">Elements used in the syntax of trigger expressions</span></span>
<span data-ttu-id="f097f-105"><a name="SP15triggerex_elements"> </a></span><span class="sxs-lookup"><span data-stu-id="f097f-105"></span></span>

<span data-ttu-id="f097f-106">Elemente, die in einem Ausdruck für Trigger verwendet werden können, sind:</span><span class="sxs-lookup"><span data-stu-id="f097f-106">Elements that can be used in a trigger expression are:</span></span>
  
    
    

- <span data-ttu-id="f097f-107">Operatoren</span><span class="sxs-lookup"><span data-stu-id="f097f-107">Operators</span></span>
    
  
- <span data-ttu-id="f097f-108">Verwaltete Eigenschaft Wert Zugriff</span><span class="sxs-lookup"><span data-stu-id="f097f-108">Managed property value access</span></span>
    
  
- <span data-ttu-id="f097f-109">Literale</span><span class="sxs-lookup"><span data-stu-id="f097f-109">Literals</span></span>
    
  
- <span data-ttu-id="f097f-110">Funktionen</span><span class="sxs-lookup"><span data-stu-id="f097f-110">Functions</span></span>
    
  
- <span data-ttu-id="f097f-111">Konstanten</span><span class="sxs-lookup"><span data-stu-id="f097f-111">Constants</span></span>
    
  

> <span data-ttu-id="f097f-112">**Hinweis:** Die Zeichenfolge „**Null**“ ist für den Wert **Null** reserviert.</span><span class="sxs-lookup"><span data-stu-id="f097f-112">**Note** The string " **Null**" is reserved for the value **Null**.</span></span> 
  
    
    


## <a name="operators-in-trigger-expression-syntax"></a><span data-ttu-id="f097f-113">Operatoren in der Syntax von Triggerausdrücken</span><span class="sxs-lookup"><span data-stu-id="f097f-113">Operators in trigger expression syntax</span></span>
<span data-ttu-id="f097f-114"><a name="SP15triggerex_operators"> </a></span><span class="sxs-lookup"><span data-stu-id="f097f-114"></span></span>

<span data-ttu-id="f097f-p101">Tabelle 1 beschreibt die Operatoren, die von der Sprache des Trigger-Ausdruck, mit der Reihenfolge der Priorität von der höchsten zur niedrigsten wird unterstützt. Operatoren in der gleichen Kategorie haben dieselbe Rangfolge. Mehrere Operatoren haben zwei Versionen von deren Syntax.</span><span class="sxs-lookup"><span data-stu-id="f097f-p101">Table 1 describes the operators supported by the trigger expression language, with order of precedence being from highest to lowest. Operators in the same category have equal precedence. Several operators have two versions of their syntax.</span></span>
  
    
    

<span data-ttu-id="f097f-118">**In Tabelle 1. Operatoren für Trigger Ausdruck-Syntax unterstützt**</span><span class="sxs-lookup"><span data-stu-id="f097f-118">**Table 1. Supported operators for trigger expression syntax**</span></span>


|<span data-ttu-id="f097f-119">**Kategorie**</span><span class="sxs-lookup"><span data-stu-id="f097f-119">**Category**</span></span>|<span data-ttu-id="f097f-120">**Ausdruck**</span><span class="sxs-lookup"><span data-stu-id="f097f-120">**Expression**</span></span>|<span data-ttu-id="f097f-121">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="f097f-121">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="f097f-122">Unärer Operator</span><span class="sxs-lookup"><span data-stu-id="f097f-122">Unary</span></span>  <br/> |-  <br/> <span data-ttu-id="f097f-123">!, NICHT</span><span class="sxs-lookup"><span data-stu-id="f097f-123">!, NOT</span></span>  <br/> |<span data-ttu-id="f097f-124">Arithmetische negation</span><span class="sxs-lookup"><span data-stu-id="f097f-124">Arithmetic negation</span></span>  <br/> <span data-ttu-id="f097f-125">Logische negation</span><span class="sxs-lookup"><span data-stu-id="f097f-125">Logical negation</span></span>  <br/> |
|<span data-ttu-id="f097f-126">Mit</span><span class="sxs-lookup"><span data-stu-id="f097f-126">Multiplicative</span></span>  <br/> |*  <br/> /  <br/> <span data-ttu-id="f097f-127">%, mod</span><span class="sxs-lookup"><span data-stu-id="f097f-127">%, mod</span></span>  <br/> |<span data-ttu-id="f097f-128">Multiplikation</span><span class="sxs-lookup"><span data-stu-id="f097f-128">Multiplication</span></span>  <br/> <span data-ttu-id="f097f-129">Abteilung</span><span class="sxs-lookup"><span data-stu-id="f097f-129">Division</span></span>  <br/> <span data-ttu-id="f097f-130">Rest</span><span class="sxs-lookup"><span data-stu-id="f097f-130">Remainder</span></span>  <br/> |
|<span data-ttu-id="f097f-131">Additive</span><span class="sxs-lookup"><span data-stu-id="f097f-131">Additive</span></span>  <br/> |+  <br/> -  <br/> &amp;  <br/> |<span data-ttu-id="f097f-132">Ergänzungen</span><span class="sxs-lookup"><span data-stu-id="f097f-132">Addition</span></span>  <br/> <span data-ttu-id="f097f-133">Subtraktion</span><span class="sxs-lookup"><span data-stu-id="f097f-133">Subtraction</span></span>  <br/> <span data-ttu-id="f097f-134">Zeichenfolgenverknüpfung</span><span class="sxs-lookup"><span data-stu-id="f097f-134">String concatenation</span></span>  <br/> |
|<span data-ttu-id="f097f-135">Relational</span><span class="sxs-lookup"><span data-stu-id="f097f-135">Relational</span></span>  <br/> |<span data-ttu-id="f097f-136">=, ==</span><span class="sxs-lookup"><span data-stu-id="f097f-136">=, ==</span></span>  <br/> <span data-ttu-id="f097f-137">! = <></span><span class="sxs-lookup"><span data-stu-id="f097f-137">!=, <></span></span>  <br/> <  <br/> >  <br/> <=  <br/> >=  <br/> |<span data-ttu-id="f097f-138">Gleichheit</span><span class="sxs-lookup"><span data-stu-id="f097f-138">Equality</span></span>  <br/> <span data-ttu-id="f097f-139">Ungleichheit</span><span class="sxs-lookup"><span data-stu-id="f097f-139">Inequality</span></span>  <br/> <span data-ttu-id="f097f-140">Kleiner als</span><span class="sxs-lookup"><span data-stu-id="f097f-140">Less than</span></span>  <br/> <span data-ttu-id="f097f-141">Größer als</span><span class="sxs-lookup"><span data-stu-id="f097f-141">Greater than</span></span>  <br/> <span data-ttu-id="f097f-142">Kleiner oder gleich</span><span class="sxs-lookup"><span data-stu-id="f097f-142">Less than or equal</span></span>  <br/> <span data-ttu-id="f097f-143">Größer oder gleich</span><span class="sxs-lookup"><span data-stu-id="f097f-143">Greater than or equal</span></span>  <br/> |
|<span data-ttu-id="f097f-144">Logisches UND</span><span class="sxs-lookup"><span data-stu-id="f097f-144">Logical AND</span></span>  <br/> |<span data-ttu-id="f097f-145">&amp; &amp;, AND</span><span class="sxs-lookup"><span data-stu-id="f097f-145">&amp;&amp;, AND</span></span>  <br/> |<span data-ttu-id="f097f-146">Logisches UND</span><span class="sxs-lookup"><span data-stu-id="f097f-146">Logical AND</span></span>  <br/> |
|<span data-ttu-id="f097f-147">Logisches ODER</span><span class="sxs-lookup"><span data-stu-id="f097f-147">Logical OR</span></span>  <br/> | <span data-ttu-id="f097f-148">OR</span><span class="sxs-lookup"><span data-stu-id="f097f-148">OR</span></span>  <br/> |<span data-ttu-id="f097f-149">Logisches ODER</span><span class="sxs-lookup"><span data-stu-id="f097f-149">Logical OR</span></span>  <br/> |
   

## <a name="managed-property-access-in-trigger-expressions"></a><span data-ttu-id="f097f-150">Verwaltete Eigenschaftenzugriff in Trigger Ausdrücken</span><span class="sxs-lookup"><span data-stu-id="f097f-150">Managed property access in trigger expressions</span></span>
<span data-ttu-id="f097f-151"><a name="SP15triggerex_managed"> </a></span><span class="sxs-lookup"><span data-stu-id="f097f-151"></span></span>

<span data-ttu-id="f097f-152">Verwaltete Eigenschaften in der durchforsteten Elemente werden nach ihren Namen verwiesen; der Name ist nicht in Anführungszeichen ("") und die Groß-/Kleinschreibung beachtet wird.</span><span class="sxs-lookup"><span data-stu-id="f097f-152">Managed properties in the crawled items are referenced by their name; the name is not in quotation marks ("") and is case-sensitive.</span></span>
  
    
    

## <a name="literals-in-trigger-expressions"></a><span data-ttu-id="f097f-153">Literale in Ausdrücken trigger</span><span class="sxs-lookup"><span data-stu-id="f097f-153">Literals in trigger expressions</span></span>
<span data-ttu-id="f097f-154"><a name="SP15triggerex_literals"> </a></span><span class="sxs-lookup"><span data-stu-id="f097f-154"></span></span>

<span data-ttu-id="f097f-155">Die folgenden Datentypen können als Literale ausgedrückt werden: **String**, **Int32**, **Double**und **Boolean**.</span><span class="sxs-lookup"><span data-stu-id="f097f-155">The following data types can be expressed as literals: **String**, **Int32**, **Double**, and **Boolean**.</span></span>
  
    
    

## <a name="functions-in-trigger-expressions"></a><span data-ttu-id="f097f-156">Funktionen in Ausdrücken trigger</span><span class="sxs-lookup"><span data-stu-id="f097f-156">Functions in trigger expressions</span></span>
<span data-ttu-id="f097f-157"><a name="SP15triggerex_functions"> </a></span><span class="sxs-lookup"><span data-stu-id="f097f-157"></span></span>

<span data-ttu-id="f097f-p102">Breites Zusammenstellung von Funktionen von mathematische Funktionen wie  `Floor` bis hin zu den Funktionen für die Verwendung mit bestimmten Datentypen, wie etwa `Lists`. Sie können diese Funktionen einzeln oder schachteln Sie sie.</span><span class="sxs-lookup"><span data-stu-id="f097f-p102">A wide collection of functions ranging from mathematical functions such as  `Floor` to functions for use with particular data types, such as `Lists`. You can use these functions individually or you can nest them.</span></span>
  
    
    

-  `bool? ListContains<T>(IList<T> list, T obj)`
    
  
-  `int? Count<TElement>(IList<TElement> list)`
    
  
-  `TElement Item<TElement>(IList<TElement> list, int? index)`
    
  
-  `bool IsInsideRange(DateTime? date, long? fromTicks, long? toTicks)`
    
  
-  `DateTime Now()`
    
  
-  `DateTime? ToDate(string date, string format)`
    
  
-  `int? Day(DateTime? date)`
    
  
-  `int? DayOfWeek(DateTime? date)`
    
  
-  `int? DayOfYear(DateTime? date)`
    
  
-  `int? GetDatePart(DateTime? date, DatePartConstant datePartConstant)`
    
  
-  `int? Hour(DateTime? date)`
    
  
-  `int? Minute(DateTime? date)`
    
  
-  `int? Month(DateTime? date)`
    
  
-  `int? Quarter(DateTime? date)`
    
  
-  `int? Second(DateTime? date)`
    
  
-  `int? Year(DateTime? date)`
    
  
-  `long? GetDateDiff(DateTime? occursFirst, DateTime? occursLast, DatePartConstant datePartConstant)`
    
  
-  `string Extension(string arg)`
    
  
-  `string FileName(string arg)`
    
  
-  `string FileName(string arg, bool? excludeExtension)`
    
  
-  `bool IsNull(object value)`
    
  
-  `bool? IsDate(string input, string format)`
    
  
-  `object IfThenElse(bool? condition, object thenBranch, object elseBranch)`
    
  
-  `decimal? Ceiling(decimal? number)`
    
  
-  `decimal? Floor(decimal? number)`
    
  
-  `double? Ceiling(double? number)`
    
  
-  `double? Floor(double? number)`
    
  
-  `double? Sqrt(double? number)`
    
  
-  `bool? Contains(string arg, string contained)`
    
  
-  `bool? EndsWith(string arg, string suffix)`
    
  
-  `bool? IsMatch(string input, string pattern)`
    
  
-  `bool? IsMatch(string input, string pattern, int? start, RegexOptionConstant options)`
    
  
-  `bool? IsMatch(string input, string pattern, RegexOptionConstant options)`
    
  
-  `bool? IsNullOrEmpty(string input)`
    
  
-  `bool? StartsWith(string arg, string prefix)`
    
  
-  `int? IndexOf(string arg, string toFind)`
    
  
-  `int? IndexOfRegex(string input, string regex)`
    
  
-  `int? LastIndexOf(string arg, string toFind)`
    
  
-  `int? Length(string arg)`
    
  
-  `string Match(string input, string pattern)`
    
  
-  `string Match(string input, string pattern, int? start, int? length, RegexOptionConstant options)`
    
  
-  `string Match(string input, string pattern, int? start, RegexOptionConstant options)`
    
  
-  `string Match(string input, string pattern, RegexOptionConstant options)`
    
  
-  `string Substring(string arg, int? start)`
    
  
-  `string Substring(string arg, int? start, int? length)`
    
  
-  `string ToLower(string arg)`
    
  
-  `string Trim(string value)`
    
  

## <a name="constants-in-trigger-expressions"></a><span data-ttu-id="f097f-160">Konstanten in Ausdrücken trigger</span><span class="sxs-lookup"><span data-stu-id="f097f-160">Constants in trigger expressions</span></span>
<span data-ttu-id="f097f-161"><a name="SP15triggerex_constants"> </a></span><span class="sxs-lookup"><span data-stu-id="f097f-161"></span></span>

<span data-ttu-id="f097f-p103">Es gibt zwei Sätze von Konstanten, die mit bestimmten Funktionen verwendet werden können: **DatePartConstant** und **RegexOptionConstant**. Tabelle 2 sind die beiden Beispiele der folgenden Konstanten und, in dem Sie sie verwenden können.</span><span class="sxs-lookup"><span data-stu-id="f097f-p103">There are two sets of constants that can be used with specific functions: **DatePartConstant** and **RegexOptionConstant**. Table 2 lists the two examples of these constants and where you can use them.</span></span>
  
    
    

<span data-ttu-id="f097f-164">**In Tabelle 2. Trigger Ausdruck Konstanten und Verwendung von Diensten in SharePoint**</span><span class="sxs-lookup"><span data-stu-id="f097f-164">**Table 2. Trigger expression constants and usage in SharePoint**</span></span>


|<span data-ttu-id="f097f-165">**Gruppe von Konstanten**</span><span class="sxs-lookup"><span data-stu-id="f097f-165">**Group of constants**</span></span>|<span data-ttu-id="f097f-166">**Beispiele**</span><span class="sxs-lookup"><span data-stu-id="f097f-166">**Examples**</span></span>|<span data-ttu-id="f097f-167">**Verwendung**</span><span class="sxs-lookup"><span data-stu-id="f097f-167">**Usage**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="f097f-168">**DatePartConstant**</span><span class="sxs-lookup"><span data-stu-id="f097f-168">**DatePartConstant**</span></span> <br/> |<span data-ttu-id="f097f-169">**Day**, **Month**, **Year**, **Hour**, **Minute**, **Second**.</span><span class="sxs-lookup"><span data-stu-id="f097f-169">**Day**, **Month**, **Year**, **Hour**, **Minute**, **Second**.</span></span>  <br/> |<span data-ttu-id="f097f-170">Mit der **GetDatePart** -Funktion</span><span class="sxs-lookup"><span data-stu-id="f097f-170">With the **GetDatePart** function</span></span> <br/> |
|<span data-ttu-id="f097f-171">**RegexOptionConstant**</span><span class="sxs-lookup"><span data-stu-id="f097f-171">**RegexOptionConstant**</span></span> <br/> |<span data-ttu-id="f097f-172">**IgnoreCase**</span><span class="sxs-lookup"><span data-stu-id="f097f-172">**IgnoreCase**</span></span> <br/> |<span data-ttu-id="f097f-173">Mit den Funktionen **IsMatch**, **Match**, **ReplaceRegex**und **IndexOfRegex**.</span><span class="sxs-lookup"><span data-stu-id="f097f-173">With the **IsMatch**, **Match**, **ReplaceRegex**, and **IndexOfRegex** functions.</span></span> <br/> |
   

## <a name="additional-resources"></a><span data-ttu-id="f097f-174">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f097f-174">Additional resources</span></span>
<span data-ttu-id="f097f-175"><a name="SP15triggerex_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f097f-175"></span></span>


-  [<span data-ttu-id="f097f-176">Benutzerdefinierte Inhaltsverarbeitung mit dem Webdienstpopup zur Inhaltsanreicherung</span><span class="sxs-lookup"><span data-stu-id="f097f-176">Custom content processing with the Content Enrichment web service callout</span></span>](custom-content-processing-with-the-content-enrichment-web-service-callout.md)
    
  
-  [<span data-ttu-id="f097f-177">Vorgehensweise: verwenden die Anreicherung Web Service als Legende für SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="f097f-177">How to: Use the Content Enrichment web service callout for SharePoint Server</span></span>](how-to-use-the-content-enrichment-web-service-callout-for-sharepoint-server.md)
    
  

  
    
    

