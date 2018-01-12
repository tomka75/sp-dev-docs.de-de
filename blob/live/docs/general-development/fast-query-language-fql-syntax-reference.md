---
title: "Syntaxreferenz für die FAST Query Language (FQL)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: bd98a41b-623c-41d4-a15d-26c0d4ba4311
ms.openlocfilehash: 861199598dc650932416a5537dd3f5a3af47a1cd
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="fast-query-language-fql-syntax-reference"></a><span data-ttu-id="bc868-102">Syntaxreferenz für die FAST Query Language (FQL)</span><span class="sxs-lookup"><span data-stu-id="bc868-102">FAST Query Language (FQL) syntax reference</span></span>
<span data-ttu-id="bc868-p101">In diesem Artikel erfahren Sie mehr über den Aufbau komplexer Suchabfragen für Suche in SharePoint mit FQL (FAST Query Language). In dieser Referenz sind die Elemente einer FQL-Abfrage beschrieben, und es wird erläutert, wie Eigenschaftsspezifikationen, Tokenausdrücke und Operatoren in FQL-Abfragen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="bc868-p101">Learn about constructing complex search queries for Search in SharePoint using the FAST Query Language (FQL). This reference describes the elements of an FQL query and how to use property specifications, token expressions, and operators in your FQL queries.</span></span>
## <a name="introduction-to-fql-and-query-language-subexpressions-and-expressions-in-sharepoint"></a><span data-ttu-id="bc868-105">Einführung in FQL und Unterausdrücke und Ausdrücke der Abfragesprache in SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="bc868-105">Introduction to FQL and query language subexpressions and expressions in SharePoint</span></span>
<span data-ttu-id="bc868-106"><a name="SP15FQL_about"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-106"><a name="SP15FQL_about"> </a></span></span>

<span data-ttu-id="bc868-107">FQL (FAST Query Language) ist eine leistungsstarke Abfragesprache, die es Entwicklern ermöglicht, genaue Suchvorgänge durchzuführen und den Suchbereich auf Werte zu begrenzen, die zu einer bestimmten verwalteten Eigenschaft oder einem Volltextindex gehören.</span><span class="sxs-lookup"><span data-stu-id="bc868-107">The FAST Query Language (FQL) is a powerful query language that enables developers to perform exact searches and to narrow the scope of your search to values that belong to a specific managed property or a full-text index.</span></span>
  
    
    
<span data-ttu-id="bc868-108">Ein Ausdruck der Abfragesprache kann geschachtelte Unterausdrücke enthalten, die Abfragebegriffe, Eigenschaftsspezifikationen und Operatoren enthalten, wie in Tabelle 1 beschrieben.</span><span class="sxs-lookup"><span data-stu-id="bc868-108">A query language expression can contain nested subexpressions that include query terms, property specifications, and operators, as described in Table 1.</span></span>
  
    
    

<span data-ttu-id="bc868-109">**Tabelle 1: Unterausdrücke in Ausdrücken der Abfragesprache**</span><span class="sxs-lookup"><span data-stu-id="bc868-109">**Table 1. Subexpressions in query language expressions**</span></span>


|<span data-ttu-id="bc868-110">**Element**</span><span class="sxs-lookup"><span data-stu-id="bc868-110">**Item**</span></span>|<span data-ttu-id="bc868-111">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="bc868-111">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="bc868-112">Tokenausdrücke</span><span class="sxs-lookup"><span data-stu-id="bc868-112">Token expressions</span></span>  <br/> |<span data-ttu-id="bc868-113">Ein oder mehrere Abfragebegriffe, Phrasen oder numerische Werte, nach denen in einer Abfrage gesucht werden soll</span><span class="sxs-lookup"><span data-stu-id="bc868-113">One or more query terms, phrases, or numeric values to search for in a query.</span></span>  <br/> |
|<span data-ttu-id="bc868-114">Eigenschaftsspezifikation</span><span class="sxs-lookup"><span data-stu-id="bc868-114">Property specification</span></span>  <br/> |<span data-ttu-id="bc868-115">Eine Eigenschaft oder ein Volltextindex, die bzw. der dem betroffenen Ausdruck zugeordnet werden soll</span><span class="sxs-lookup"><span data-stu-id="bc868-115">A property or full-text index to match with the affected expression.</span></span>  <br/> |
|<span data-ttu-id="bc868-116">Operatoren</span><span class="sxs-lookup"><span data-stu-id="bc868-116">Operators</span></span>  <br/> |<span data-ttu-id="bc868-117">Schlüsselwörter, die boolesche Operationen (zum Beispiel **AND**, **OR**) oder andere Einschränkungen für Operanden angeben (zum Beispiel **FILTER**.)</span><span class="sxs-lookup"><span data-stu-id="bc868-117">Keywords that specify Boolean operations (such as **AND**, **OR**) or other constraints to operands (such as **FILTER**.)</span></span>  <br/> |
   

### <a name="fql-query-example"></a><span data-ttu-id="bc868-118">FQL-Abfrage - Beispiel</span><span class="sxs-lookup"><span data-stu-id="bc868-118">FQL query example</span></span>

<span data-ttu-id="bc868-119">Im folgenden FQL-Abfragebeispiel wird nach den Begriffen "hello" und "world" in der verwalteten Eigenschaft **body** eines indizierten Elements gesucht:</span><span class="sxs-lookup"><span data-stu-id="bc868-119">The following FQL query example searches for the terms "hello" and "world" in the **body** managed property of an indexed item:</span></span>
  
    
    
 `body:string("hello world", mode="and")`
  
    
    
<span data-ttu-id="bc868-120">Im Beispiel:</span><span class="sxs-lookup"><span data-stu-id="bc868-120">In the example:</span></span>
  
    
    

-  <span data-ttu-id="bc868-121">`body:` begrenzt den Bereich der Abfrage auf die verwaltete body-Eigenschaft innerhalb des Elements.</span><span class="sxs-lookup"><span data-stu-id="bc868-121">`body:` limits the scope of the query to the body managed property within the item.</span></span>
    
  
-  <span data-ttu-id="bc868-122">`"hello world"` ist der Operand für den **STRING** -Operator, der die zu suchenden Begriffe angibt.</span><span class="sxs-lookup"><span data-stu-id="bc868-122">`"hello world"` is the operand to the **STRING** operator, which indicates the terms to search for.</span></span>
    
  
-  <span data-ttu-id="bc868-123">`mode="and"` gibt an, dass der logische Abfrageoperator **AND** auf `"hello world"` angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="bc868-123">`mode="and"` indicates that the logical query operator **AND** will be applied to `"hello world"`.</span></span>
    
  
<span data-ttu-id="bc868-124">Die Länge der FAST Query Language-Abfragen ist auf 2.048 Zeichen beschränkt.</span><span class="sxs-lookup"><span data-stu-id="bc868-124">The length of FAST Query Language queries is limited to 2,048 characters.</span></span>
  
    
    

## <a name="property-specification-in-fql"></a><span data-ttu-id="bc868-125">Eigenschaftsspezifikation in FQL</span><span class="sxs-lookup"><span data-stu-id="bc868-125">Property specification in FQL</span></span>
<span data-ttu-id="bc868-126"><a name="property_specification"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-126"><a name="property_specification"> </a></span></span>

<span data-ttu-id="bc868-p102">Eine Eigenschaftsspezifikation begrenzt den Bereich des betroffenen Ausdrucks auf bestimmte Bereiche des indizierten Inhalts. Ein solcher Bereich kann durch einen Volltextindex oder eine verwaltete Eigenschaft angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="bc868-p102">A property specification limits the scope of the affected expression to specific regions of the indexed content. Such a region can be identified by a full-text index or a managed property.</span></span> 
  
    
    
<span data-ttu-id="bc868-p103">Verwaltete Eigenschaften des Typs **Text** und **YesNo** werden als Nächstes ausgewertet. Alle übrigen verwalteten Eigenschaftstypen, einschließlich des Typs **Datetime** werden als numerische Werte ausgewertet.</span><span class="sxs-lookup"><span data-stu-id="bc868-p103">Managed properties of type **Text** and **YesNo** are evaluated as text. All other managed property types, including the **Datetime** type, are evaluated as numeric values.</span></span>
  
    
    
<span data-ttu-id="bc868-131">Wenn Sie keine Eigenschaftsspezifikation für einen Ausdruck einfügen, versucht das Suchmodul den im Indexschema definierten standardmäßigen Volltextindex zuzuordnen.</span><span class="sxs-lookup"><span data-stu-id="bc868-131">If you don't include a property specification for an expression, the search engine attempts to match the default full-text index defined in the index schema.</span></span>
  
    
    
<span data-ttu-id="bc868-132">Dem Namen der Eigenschaft muss stets ein Doppelpunkt vorangestellt werden (Operator **In**), und numerische Operatoren müssen immer eine Eigenschaftsspezifikation enthalten.</span><span class="sxs-lookup"><span data-stu-id="bc868-132">The property name must always precede a colon ( **In** operator), and numeric operators must always include a property specification.</span></span>
  
    
    
<span data-ttu-id="bc868-133">Eine Eigenschaftsspezifikation (der Operator **In**) kann auf die folgenden Abfrageeinheiten angewendet werden:</span><span class="sxs-lookup"><span data-stu-id="bc868-133">A property specification (the **In** Operator) may be applied to the following query entities:</span></span>
  
    
    

- <span data-ttu-id="bc868-134">Einen einzelnen Begriff oder eine Phrase wie folgt:</span><span class="sxs-lookup"><span data-stu-id="bc868-134">A single term or phrase, as follows:</span></span>

    `author:shakespeare`
    
    `title:"to be or not to be"`
- <span data-ttu-id="bc868-135">Einen Operator, zum Beispiel den Operator **STRING**, wie folgt:</span><span class="sxs-lookup"><span data-stu-id="bc868-135">An operator, for example, the **STRING** operator, as follows:</span></span>
```
    title:string("to be or not to be")
```
    In this case the property specification applies to the complete operator expression.

### <a name="examples"></a><span data-ttu-id="bc868-136">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-136">Examples</span></span>

<span data-ttu-id="bc868-137">Jeder der folgenden Ausdrücke findet Elemente, die in der verwalteten **title**-Eigenschaft sowohl den Begriff "viel" als auch den Begriff "nichts" enthalten.</span><span class="sxs-lookup"><span data-stu-id="bc868-137">Each of the following expressions matches items that have both "much" and "nothing" in the **title** managed property.</span></span>

 `title:and(much, nothing)`

 `and(title:much, title:nothing)`

 `title:string("much nothing", mode="and")`

## <a name="token-expressions-in-fql"></a><span data-ttu-id="bc868-138">Tokenausdrücke in FQL</span><span class="sxs-lookup"><span data-stu-id="bc868-138">Token expressions in FQL</span></span>
<span data-ttu-id="bc868-139"><a name="token_expressions"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-139"><a name="token_expressions"> </a></span></span>

<span data-ttu-id="bc868-140">Tokenausdrücke sind Wörter, Phrasen und numerische Werte, die mit dem Index abgeglichen werden.</span><span class="sxs-lookup"><span data-stu-id="bc868-140">Token expressions are words, phrases, or numeric values that are matched against the index.</span></span>
  
    
    
<span data-ttu-id="bc868-141">Bei einem Tokenausdruck vom Typ Text kann es sich um ein einzelnes Wort oder eine in doppelte Anführungszeichen eingeschlossene Phrase handeln.</span><span class="sxs-lookup"><span data-stu-id="bc868-141">A text token expression can be a single word or a phrase enclosed in double quotation marks.</span></span>
  
    
    
<span data-ttu-id="bc868-142">Ein numerischer Tokenausdruck kann ein einzelner Wert oder Wertebereichausdruck sein.</span><span class="sxs-lookup"><span data-stu-id="bc868-142">A numeric token expression can be a single value or a value range expression.</span></span>
  
    
    

### <a name="wildcard-expressions"></a><span data-ttu-id="bc868-143">Platzhalterausdrücke</span><span class="sxs-lookup"><span data-stu-id="bc868-143">Wildcard expressions</span></span>

<span data-ttu-id="bc868-144">Mit einem Platzhalterausdruck wird ein einzelner Begriff oder eine Phrase angegeben, die ein Sternchen ("**\\***") enthält. Durch die Angabe des Sternchens können auch 0 oder mehrere Zeichen mit Ausnahme von Leerzeichen gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="bc868-144">A wildcard expression indicates a single term or phrase that includes the Asterisk ("**\\***") character; asterisk implies a match of zero or more characters, excluding whitespace.</span></span> <span data-ttu-id="bc868-145">FQL unterstützt die Präfixsuche für individuelle verwaltete Texteigenschaften und Volltextindizes.</span><span class="sxs-lookup"><span data-stu-id="bc868-145">FQL supports prefix search for individual text managed properties and full-text indexes.</span></span>
  
    
    

#### <a name="wildcard-expression-examples"></a><span data-ttu-id="bc868-146">Beispiele für Platzhalterausdrücke</span><span class="sxs-lookup"><span data-stu-id="bc868-146">Wildcard expression examples</span></span>

<span data-ttu-id="bc868-147">Nachfolgend finden Sie eine Liste gültiger Verwendungszwecke von Platzhalterausdrücken in FQL:</span><span class="sxs-lookup"><span data-stu-id="bc868-147">The following is a list of valid uses of wildcard expressions in FQL:</span></span>
  
    
    

-  `text*`
    
  
-  `string("this examp*")`
    
  

### <a name="numeric-term-expressions"></a><span data-ttu-id="bc868-148">Numerische Ausdrücke</span><span class="sxs-lookup"><span data-stu-id="bc868-148">Numeric term expressions</span></span>
<span data-ttu-id="bc868-149"><a name="fql_token_numeric"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-149"><a name="fql_token_numeric"> </a></span></span>

<span data-ttu-id="bc868-p105">Jeder numerische Ausdruck muss eine Eigenschaftsspezifikation eines kompatiblen Indexschema-Datentyps enthalten. Tabelle 2 enthält die numerischen Datentypen, die in FQL verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="bc868-p105">Each numeric term expression must include a property specification of a compatible index schema data type. Table 2 lists the numeric data types that can be used in FQL.</span></span> 
  
    
    

<span data-ttu-id="bc868-152">**Tabelle 2: Numerische Datentypen, die in FQL verwendet werden können**</span><span class="sxs-lookup"><span data-stu-id="bc868-152">**Table 2. Numeric data types that can be used in FQL**</span></span>


|<span data-ttu-id="bc868-153">**FQL-Typ**</span><span class="sxs-lookup"><span data-stu-id="bc868-153">**FQL type**</span></span>|<span data-ttu-id="bc868-154">**Kompatible Indexschematypen**</span><span class="sxs-lookup"><span data-stu-id="bc868-154">**Compatible index schema types**</span></span>|<span data-ttu-id="bc868-155">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="bc868-155">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="bc868-156">**Int**</span><span class="sxs-lookup"><span data-stu-id="bc868-156">**Int**</span></span> <br/> |<span data-ttu-id="bc868-157">**Integer**</span><span class="sxs-lookup"><span data-stu-id="bc868-157">**Integer**</span></span> <br/> |<span data-ttu-id="bc868-158">64-Bit-Ganzzahl</span><span class="sxs-lookup"><span data-stu-id="bc868-158">64 bit integer.</span></span>  <br/> |
|<span data-ttu-id="bc868-159">**Float**</span><span class="sxs-lookup"><span data-stu-id="bc868-159">**Float**</span></span> <br/> |<span data-ttu-id="bc868-160">**Double**</span><span class="sxs-lookup"><span data-stu-id="bc868-160">**Double**</span></span> <br/> |<span data-ttu-id="bc868-161">64-Bit-Gleitkommazahl mit doppelter Genauigkeit</span><span class="sxs-lookup"><span data-stu-id="bc868-161">64-bit (double precision) floating point.</span></span>  <br/> |
|<span data-ttu-id="bc868-162">**Decimal**</span><span class="sxs-lookup"><span data-stu-id="bc868-162">**Decimal**</span></span> <br/> |<span data-ttu-id="bc868-163">**Decimal**</span><span class="sxs-lookup"><span data-stu-id="bc868-163">**Decimal**</span></span> <br/> |<span data-ttu-id="bc868-164">128-Bit-Dezimal</span><span class="sxs-lookup"><span data-stu-id="bc868-164">128-bit decimal</span></span>  <br/> |
|<span data-ttu-id="bc868-165">**Datetime**</span><span class="sxs-lookup"><span data-stu-id="bc868-165">**Datetime**</span></span> <br/> |<span data-ttu-id="bc868-166">**Datetime**</span><span class="sxs-lookup"><span data-stu-id="bc868-166">**Datetime**</span></span> <br/> |<span data-ttu-id="bc868-167">Ein Wert für Datum und Uhrzeit</span><span class="sxs-lookup"><span data-stu-id="bc868-167">A date and time value.</span></span>  <br/><span data-ttu-id="bc868-168">Aufgrund der Unterstützung von Datum/Uhrzeit in FQL können die gleichen numerischen Operationen an Datum-/Uhrzeitwerten ausgeführt werden wie an anderen numerischen Werten.</span><span class="sxs-lookup"><span data-stu-id="bc868-168">The date/time support in FQL enables the same numeric operations on date/time values as on other numeric values.</span></span>  <br/> |
   

#### <a name="date-and-time-query-expressions"></a><span data-ttu-id="bc868-169">Abfrageausdrücke für Datum und Uhrzeit</span><span class="sxs-lookup"><span data-stu-id="bc868-169">Date and time query expressions</span></span>
<span data-ttu-id="bc868-170"><a name="fql_token_datetime"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-170"><a name="fql_token_datetime"> </a></span></span>

<span data-ttu-id="bc868-171">FQL stellt den **datetime**-Datentyp für Datum und Uhrzeit zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="bc868-171">FQL provides the **datetime** data type for date and time.</span></span>
  
    
    
<span data-ttu-id="bc868-172">Die folgenden ISO 8601-kompatiblen **datetime**-Formate werden in Abfragen unterstützt:</span><span class="sxs-lookup"><span data-stu-id="bc868-172">The following ISO 8601-compatible **datetime** formats are supported in queries:</span></span>
  
    
    

- <span data-ttu-id="bc868-173">JJJJ-MM-TT</span><span class="sxs-lookup"><span data-stu-id="bc868-173">YYYY-MM-DD</span></span> 
    
  
- <span data-ttu-id="bc868-174">JJJJ-MM-TTThh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="bc868-174">YYYY-MM-DDThh:mm:ss</span></span> 
    
  
- <span data-ttu-id="bc868-175">YYYY-MM-DDThh:mm:ssZ</span><span class="sxs-lookup"><span data-stu-id="bc868-175">YYYY-MM-DDThh:mm:ssZ</span></span> 
    
  
- <span data-ttu-id="bc868-176">YYYY-MM-DDThh:mm:ssfrZ</span><span class="sxs-lookup"><span data-stu-id="bc868-176">YYYY-MM-DDThh:mm:ssfrZ</span></span>
    
  
<span data-ttu-id="bc868-177">In diesen **datetime**-Formaten:</span><span class="sxs-lookup"><span data-stu-id="bc868-177">In these **datetime** formats:</span></span>
  
    
    

-  <span data-ttu-id="bc868-178">_YYYY_ gibt eine vierziffrige Jahreszahl an.</span><span class="sxs-lookup"><span data-stu-id="bc868-178">_YYYY_ specifies a four-digit year.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="bc868-179">Es werden nur vierziffrige Jahresangaben unterstützt.</span><span class="sxs-lookup"><span data-stu-id="bc868-179">Only four-digit years are supported.</span></span> 

-  <span data-ttu-id="bc868-p106">_MM_ gibt einen zweiziffrigen Monat an, z.B. 01 = Januar.</span><span class="sxs-lookup"><span data-stu-id="bc868-p106">_MM_ specifies a two-digit month. For example, 01 = January.</span></span>
    
  
-  <span data-ttu-id="bc868-182">_DD_ gibt einen zweiziffrigen Tag des Monats an (01-31).</span><span class="sxs-lookup"><span data-stu-id="bc868-182">_DD_ specifies a two-digit day of the month (01 through 31).</span></span>
    
  
-  <span data-ttu-id="bc868-183">_T_ gibt den Buchstaben „T" an.</span><span class="sxs-lookup"><span data-stu-id="bc868-183">_T_ specifies the letter "T".</span></span>
    
  
-  <span data-ttu-id="bc868-p107">_hh_ gibt eine zweiziffrige Stundenangabe an (00-23).</span><span class="sxs-lookup"><span data-stu-id="bc868-p107">_hh_ specifies a two-digits hour (00 through 23); A.M./P.M. indication is not allowed.</span></span>
    
  
-  <span data-ttu-id="bc868-186">_mm_ gibt eine zweiziffrige Minutenangabe an (00-59).</span><span class="sxs-lookup"><span data-stu-id="bc868-186">_mm_ specifies a two-digit minute (00 through 59).</span></span>
    
  
-  <span data-ttu-id="bc868-187">_ss_ gibt eine zweiziffrige Sekundenangabe an (00-59).</span><span class="sxs-lookup"><span data-stu-id="bc868-187">_ss_ specifies a two-digit second (00 through 59).</span></span>
    
  
-  <span data-ttu-id="bc868-p108">_fr_ gibt optional eine Zehntelsekundenangabe an, _ss_; zwischen 1 und 7, die nach dem **.** nach den Sekunden folgt. Beispiel: 2012-09-27T11:57:34.1234567.</span><span class="sxs-lookup"><span data-stu-id="bc868-p108">_fr_ specifies an optional fraction of seconds, _ss_; between 1 to 7 digits that follows the **.** after the seconds. For example, 2012-09-27T11:57:34.1234567.</span></span>
    
  
<span data-ttu-id="bc868-p109">Alle Datums-/Zeitwerte müssen gemäß der UTC (Coordinated Universal Time) angegeben werden, auch als GMT (Greenwich Mean Time) Zeitzone bekannt. Der UTC-Zeitzonenbezeichner (nachfolgendes "Z") ist optional.</span><span class="sxs-lookup"><span data-stu-id="bc868-p109">All date/time values must be specified according to the UTC (Coordinated Universal Time), also known as GMT (Greenwich Mean Time) time zone. The UTC time zone identifier (a trailing "Z" character) is optional.</span></span>
  
    
    

### <a name="reserved-words-special-characters-and-escaping"></a><span data-ttu-id="bc868-193">Reservierte Wörter, Sonderzeichen und Escapezeichen</span><span class="sxs-lookup"><span data-stu-id="bc868-193">Reserved words, special characters, and escaping</span></span>
<span data-ttu-id="bc868-194"><a name="fql_token_numeric"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-194"><a name="fql_token_numeric"> </a></span></span>

<span data-ttu-id="bc868-195">Die folgenden Wörter sind in FQL reserviert.</span><span class="sxs-lookup"><span data-stu-id="bc868-195">The following words are reserved within FQL.</span></span>
  
    
    
`and, or, any, andnot, count, decimal, rank, near, onear, int, in32, int64, float, double, datetime, max, min, range, phrase, scope, filter, not, string, starts-with, ends-with, equals, words, xrank.`
  
    
    
<span data-ttu-id="bc868-196">Wenn Sie diese Wörter als Begriffe in einem Abfrageausdruck ausdrücken möchten, müssen Sie sie in doppelte Anführungszeichen einschließen, wie in den folgenden Beispielen gezeigt:</span><span class="sxs-lookup"><span data-stu-id="bc868-196">If you want to express any of these words as terms in a query expression, you must enclose them in double quotation marks as shown in the following examples:</span></span> 
  
    
    

-  `or("any", "and", "xrank")`
    
  
-  `string("any and xrank", mode="OR")`
    
  
-  `phrase(this, is, a, "phrase")`
    
  

> <span data-ttu-id="bc868-197">**Tipp:** Reservierte Wörter und Zeichen unterliegen nicht der Groß-/Kleinschreibung. Es wird jedoch die Verwendung von Kleinbuchstaben empfohlen, um zukünftige Kompatibilität zu gewährleisten.</span><span class="sxs-lookup"><span data-stu-id="bc868-197">**Tip:** Reserved words and characters are not case-sensitive, but using lowercase characters are recommended for future compatibility.</span></span> 
  
    
    

<span data-ttu-id="bc868-p110">FQL erfordert nicht immer, dass Zeichenfolgen in doppelte Anführungszeichen eingeschlossen werden. Beispielsweise ist  `and(cat, dog)` gültige FQL-Syntax, obwohl `cat` und `dog` nicht in doppelte Anführungszeichen eingeschlossen sind. Wir empfehlen jedoch, doppelte Anführungszeichen zu verwenden, um Konflikte mit reservierten Wörtern zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="bc868-p110">FQL does not always require a string to be enclosed in double quotation marks. For example,  `and(cat, dog)` is valid FQL even though `cat` and `dog` are not in double quotation marks. However, we recommend that you use double quotation marks to avoid conflicts with reserved words.</span></span>
  
    
    
<span data-ttu-id="bc868-p111">Die Abfragebegriffe sind gemäß Ihren Gebietsschemaeinstellungen mit Token versehen. Beim Vorgang der Tokenisierung werden bestimmte Sonderzeichen entfernt. Da Sonderzeichen entfernt werden, stimmen die folgenden FQL-Ausdrücke überein.</span><span class="sxs-lookup"><span data-stu-id="bc868-p111">The query terms are tokenized according to your locale setting. The tokenization process removes certain special characters. Because special characters are removed, the following FQL expressions are equivalent.</span></span>
  
    
    
 `and("[king]", "<queen>")`
  
    
    
 `and("king", "queen")`
  
    
    
<span data-ttu-id="bc868-p112">Wenn eine Abfrage Begriffe aus der Benutzereingabe oder einer anderen Anwendung enthält, verwenden Sie den Operator  `string("<query terms>", mode="AND|OR|PHRASE")`, um Konflikte mit reservierten Wörtern in der Abfragesprache zu vermeiden. Sie müssen auch mögliche doppelte Anführungszeichen aus der vom Benutzer angegebenen Abfrage entfernen.</span><span class="sxs-lookup"><span data-stu-id="bc868-p112">When a query includes terms from user input or another application, use the  `string("<query terms>", mode="AND|OR|PHRASE")` operator to avoid conflict with reserved words in the query language. You must also remove possible double quotation marks from the user-provided query.</span></span>
  
    
    

## <a name="fql-operators"></a><span data-ttu-id="bc868-206">FQL-Operatoren</span><span class="sxs-lookup"><span data-stu-id="bc868-206">FQL Operators</span></span>
<span data-ttu-id="bc868-207"><a name="fql_operators"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-207"><a name="fql_operators"> </a></span></span>

<span data-ttu-id="bc868-p113">FQL-Operatoren (FAST Query Language) sind Schlüsselwörter, die boolesche Operationen oder andere Einschränkungen für Operanden angeben. Die Syntax der FQL-Operatoren lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="bc868-p113">FAST Query Language (FQL) operators are keywords that specify Boolean operations or other constraints to operands. The FQL operator syntax is as follows:</span></span>
  
    
    
 `[property-spec:]operator(operand [,operand]* [, parameter="value"]*)`
  
    
    
<span data-ttu-id="bc868-210">Inhalt der Syntax:</span><span class="sxs-lookup"><span data-stu-id="bc868-210">In the syntax:</span></span>
  
    
    

-  <span data-ttu-id="bc868-211">_property-spec_ ist eine optionale Eigenschaftsspezifikation gefolgt vom Operator "in".</span><span class="sxs-lookup"><span data-stu-id="bc868-211">_property-spec_ is an optional property specification followed by the "in" operator.</span></span>
    
  
-  <span data-ttu-id="bc868-212">_operator_ ist ein Schlüsselwort, das eine auszuführende Operation angibt.</span><span class="sxs-lookup"><span data-stu-id="bc868-212">_operator_ is a keyword that specifies an operation to perform.</span></span>
    
  
-  <span data-ttu-id="bc868-213">_operand_ ist ein Begriffsausdruck oder ein anderer Operator.</span><span class="sxs-lookup"><span data-stu-id="bc868-213">_operand_ is a term expression or another operator.</span></span>
    
  
-  <span data-ttu-id="bc868-214">_parameter_ ist der Name des Werts, der das Verhalten des Operators ändert.</span><span class="sxs-lookup"><span data-stu-id="bc868-214">_parameter_ is the name of a value that changes the behavior of the operator.</span></span>
    
  
-  <span data-ttu-id="bc868-215">_value_ ist der für den Parameternamen zu verwendende Wert.</span><span class="sxs-lookup"><span data-stu-id="bc868-215">_value_ is the value to use for the parameter name.</span></span>
    
  
<span data-ttu-id="bc868-p114">Operatornamen, Parameternamen und Textwerte für Parameter unterliegen nicht der Groß-/Kleinschreibung. Leerzeichen sind im Textkörper des Operators zulässig, werden jedoch ignoriert, sofern sie nicht in doppelte Anführungszeichen eingeschlossen sind. Die Länge der FAST Query Language-Abfragen ist auf 2.048 Zeichen beschränkt.</span><span class="sxs-lookup"><span data-stu-id="bc868-p114">Operator names, parameter names, and parameter text values are case-insensitive. White space is allowed within the operator body, but is ignored unless it is enclosed in double quotation marks. The length of FAST Query Language queries is limited to 2,048 characters.</span></span>
  
    
    
<span data-ttu-id="bc868-219">Tabelle 3 enthält die Typen der von FQL unterstützten Operatoren.</span><span class="sxs-lookup"><span data-stu-id="bc868-219">Table 3 lists the types of operators supported by FQL.</span></span> 
  
    
    

<span data-ttu-id="bc868-220">**Tabelle 3: Von FQL unterstützte Operatortypen**</span><span class="sxs-lookup"><span data-stu-id="bc868-220">**Table 3. FQL supported operator types**</span></span>


|<span data-ttu-id="bc868-221">**Typ**</span><span class="sxs-lookup"><span data-stu-id="bc868-221">**Type**</span></span>|<span data-ttu-id="bc868-222">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="bc868-222">**Description**</span></span>|<span data-ttu-id="bc868-223">**Operatoren**</span><span class="sxs-lookup"><span data-stu-id="bc868-223">**Operators**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="bc868-224">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="bc868-224">String</span></span>  <br/> |<span data-ttu-id="bc868-p115">Ermöglicht die Angabe von Abfrageoperationen in einer Begriffszeichenfolge. Dies ist der gängigste Operator für Textzeichenfolgen.</span><span class="sxs-lookup"><span data-stu-id="bc868-p115">Enables you to specify query operations on a string of terms. This is the most common operator to use on text terms.</span></span>  <br/> | [<span data-ttu-id="bc868-227">STRING</span><span class="sxs-lookup"><span data-stu-id="bc868-227">STRING</span></span>](fast-query-language-fql-syntax-reference.md#fql_string_operator) <br/> |
|<span data-ttu-id="bc868-228">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="bc868-228">Boolean</span></span>  <br/> |<span data-ttu-id="bc868-229">Ermöglicht die Kombination von Begriffen und Unterausdrücken in einer Abfrage.</span><span class="sxs-lookup"><span data-stu-id="bc868-229">Enables you to combine terms and sub-expressions in a query.</span></span>  <br/> | <span data-ttu-id="bc868-230">[AND](fast-query-language-fql-syntax-reference.md#fql_and_operator),  [OR](fast-query-language-fql-syntax-reference.md#fql_or_operator),  [ANY](fast-query-language-fql-syntax-reference.md#fql_any_operator),  [ANDNOT](fast-query-language-fql-syntax-reference.md#fql_andnot_operator),  [NOT](fast-query-language-fql-syntax-reference.md#fql_not_operator),  [COUNT](fast-query-language-fql-syntax-reference.md#fql_count_operator),  [COUNT](fast-query-language-fql-syntax-reference.md#fql_count_operator)</span><span class="sxs-lookup"><span data-stu-id="bc868-230">[AND](fast-query-language-fql-syntax-reference.md#fql_and_operator),  [OR](fast-query-language-fql-syntax-reference.md#fql_or_operator),  [ANY](fast-query-language-fql-syntax-reference.md#fql_any_operator),  [ANDNOT](fast-query-language-fql-syntax-reference.md#fql_andnot_operator),  [NOT](fast-query-language-fql-syntax-reference.md#fql_not_operator),  [COUNT](fast-query-language-fql-syntax-reference.md#fql_count_operator),  [COUNT](fast-query-language-fql-syntax-reference.md#fql_count_operator)</span></span> <br/> |
|<span data-ttu-id="bc868-231">Näherung</span><span class="sxs-lookup"><span data-stu-id="bc868-231">Proximity</span></span>  <br/> |<span data-ttu-id="bc868-232">Hiermit können Sie angeben, wie nah die Abfragebegriffe in einer übereinstimmenden Textsequenz beieinander liegen.</span><span class="sxs-lookup"><span data-stu-id="bc868-232">Enables you to specify the proximity of the query terms in a matching sequence of text.</span></span>  <br/> | <span data-ttu-id="bc868-233">[NEAR](fast-query-language-fql-syntax-reference.md#fql_near_operator),  [ONEAR](fast-query-language-fql-syntax-reference.md#fql_onear_operator),  [PHRASE](fast-query-language-fql-syntax-reference.md#fql_phrase_operator),  [STARTS-WITH](fast-query-language-fql-syntax-reference.md#fql_startswith_operator),  [ENDS-WITH](fast-query-language-fql-syntax-reference.md#fql_endswith_operator),  [EQUALS](fast-query-language-fql-syntax-reference.md#fql_equals_operator)</span><span class="sxs-lookup"><span data-stu-id="bc868-233">[NEAR](fast-query-language-fql-syntax-reference.md#fql_near_operator),  [ONEAR](fast-query-language-fql-syntax-reference.md#fql_onear_operator),  [PHRASE](fast-query-language-fql-syntax-reference.md#fql_phrase_operator),  [STARTS-WITH](fast-query-language-fql-syntax-reference.md#fql_startswith_operator),  [ENDS-WITH](fast-query-language-fql-syntax-reference.md#fql_endswith_operator),  [EQUALS](fast-query-language-fql-syntax-reference.md#fql_equals_operator)</span></span> <br/> |
|<span data-ttu-id="bc868-234">Numeric</span><span class="sxs-lookup"><span data-stu-id="bc868-234">Numeric</span></span>  <br/> |<span data-ttu-id="bc868-235">Hiermit können Sie numerische Bedingungen in der Abfrage angeben.</span><span class="sxs-lookup"><span data-stu-id="bc868-235">Enables you to specify numeric conditions in the query.</span></span>  <br/> | <span data-ttu-id="bc868-236">[RANGE](fast-query-language-fql-syntax-reference.md#fql_range_operator) , [INT](fast-query-language-fql-syntax-reference.md#fql_int_operator),  [FLOAT](fast-query-language-fql-syntax-reference.md#fql_float_operator),  [DATETIME](fast-query-language-fql-syntax-reference.md#fql_datetime_operator),  [DECIMAL](#fql_decimal_operator)</span><span class="sxs-lookup"><span data-stu-id="bc868-236">[RANGE](fast-query-language-fql-syntax-reference.md#fql_range_operator) , [INT](fast-query-language-fql-syntax-reference.md#fql_int_operator),  [FLOAT](fast-query-language-fql-syntax-reference.md#fql_float_operator),  [DATETIME](fast-query-language-fql-syntax-reference.md#fql_datetime_operator),  [DECIMAL](#fql_decimal_operator)</span></span> <br/> |
|<span data-ttu-id="bc868-237">Relevanz</span><span class="sxs-lookup"><span data-stu-id="bc868-237">Relevance</span></span>  <br/> |<span data-ttu-id="bc868-238">Hiermit können Sie die Relevanzbewertung einer Abfrage beeinflussen.</span><span class="sxs-lookup"><span data-stu-id="bc868-238">Enables you to impact the relevance evaluation of a query.</span></span>  <br/> | <span data-ttu-id="bc868-239">[XRANK](fast-query-language-fql-syntax-reference.md#fql_xrank_operator) und [FILTER](fast-query-language-fql-syntax-reference.md#fql_filter_operator)</span><span class="sxs-lookup"><span data-stu-id="bc868-239">[XRANK](fast-query-language-fql-syntax-reference.md#fql_xrank_operator) and  [FILTER](fast-query-language-fql-syntax-reference.md#fql_filter_operator)</span></span> <br/> |
   
<span data-ttu-id="bc868-240">Tabelle 4 enthält eine Liste der unterstützten Operatoren.</span><span class="sxs-lookup"><span data-stu-id="bc868-240">Table 4 provides a list of the supported operators.</span></span>
  
    
    

<span data-ttu-id="bc868-241">**Tabelle 4: Von FQL unterstützte Operatoren**</span><span class="sxs-lookup"><span data-stu-id="bc868-241">**Table 4. FQL supported operators**</span></span>


|<span data-ttu-id="bc868-242">**Operator**</span><span class="sxs-lookup"><span data-stu-id="bc868-242">**Operator**</span></span>|<span data-ttu-id="bc868-243">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="bc868-243">**Description**</span></span>|<span data-ttu-id="bc868-244">**Typ**</span><span class="sxs-lookup"><span data-stu-id="bc868-244">**Type**</span></span>|
|:-----|:-----|:-----|
| [<span data-ttu-id="bc868-245">AND</span><span class="sxs-lookup"><span data-stu-id="bc868-245">AND</span></span>](fast-query-language-fql-syntax-reference.md#fql_and_operator) <br/> |<span data-ttu-id="bc868-246">Gibt nur Elemente zurück, die mit allen **AND** -Operanden übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="bc868-246">Returns only items that match all **AND** operands.</span></span> <br/> |<span data-ttu-id="bc868-247">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="bc868-247">Boolean</span></span>  <br/> |
| [<span data-ttu-id="bc868-248">ANDNOT</span><span class="sxs-lookup"><span data-stu-id="bc868-248">ANDNOT</span></span>](fast-query-language-fql-syntax-reference.md#fql_andnot_operator) <br/> |<span data-ttu-id="bc868-249">Gibt nur Elemente zurück, die mit dem ersten Operanden und nicht mit den nachfolgenden Operanden überstimmen.</span><span class="sxs-lookup"><span data-stu-id="bc868-249">Returns only items that match the first operand and that don't match the subsequent operands.</span></span>  <br/> |<span data-ttu-id="bc868-250">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="bc868-250">Boolean</span></span>  <br/> |
| [<span data-ttu-id="bc868-251">ANY</span><span class="sxs-lookup"><span data-stu-id="bc868-251">ANY</span></span>](fast-query-language-fql-syntax-reference.md#fql_any_operator) <br/> |<span data-ttu-id="bc868-252">Ähnelt dem Operator **OR**, abgesehen davon, dass die dynamische Rangfolge (die Relevanzbewertung in der Ergebnismenge) weder von der Anzahl der übereinstimmenden Operanden noch vom Abstand zwischen den Begriffen im Element betroffen ist.</span><span class="sxs-lookup"><span data-stu-id="bc868-252">Similar to the **OR** operator except that the dynamic rank (the relevance score in the result set.md) is affected by neither the number of operands that match nor the distance between the terms in the item.</span></span> <br/> |<span data-ttu-id="bc868-253">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="bc868-253">Boolean</span></span>  <br/> |
| [<span data-ttu-id="bc868-254">COUNT</span><span class="sxs-lookup"><span data-stu-id="bc868-254">COUNT</span></span>](fast-query-language-fql-syntax-reference.md#fql_count_operator) <br/> |<span data-ttu-id="bc868-p116">Ermöglicht Ihnen, anzugeben, wie oft ein Abfragebegriff in einem Element enthalten sein muss, damit er als Ergebnis zurückgegeben wird. Der Operand kann ein einzelner Abfragebegriff, eine Phrase oder ein Abfragebegriff mit Platzhalter sein.</span><span class="sxs-lookup"><span data-stu-id="bc868-p116">Enables you to specify the number of query term occurrences an item must include to be returned as a result. The operand may be a single query term, a phrase, or wildcard query term.</span></span>  <br/> |<span data-ttu-id="bc868-257">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="bc868-257">Boolean</span></span>  <br/> |
| [<span data-ttu-id="bc868-258">DATETIME</span><span class="sxs-lookup"><span data-stu-id="bc868-258">DATETIME</span></span>](fast-query-language-fql-syntax-reference.md#fql_datetime_operator) <br/> |<span data-ttu-id="bc868-259">Stellt die explizite Eingabe numerischer Werte zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="bc868-259">Provides explicit typing of numeric values.</span></span>  <br/> <span data-ttu-id="bc868-p117">Die explizite Typumwandlung ist optional und normalerweise nicht notwendig. Der Typ des Abfragebegriffs wird gemäß dem Typ der numerischen verwalteten Zieleigenschaft erkannt.</span><span class="sxs-lookup"><span data-stu-id="bc868-p117">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>  <br/> |<span data-ttu-id="bc868-262">Numeric</span><span class="sxs-lookup"><span data-stu-id="bc868-262">Numeric</span></span>  <br/> |
| [<span data-ttu-id="bc868-263">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="bc868-263">DECIMAL</span></span>](fast-query-language-fql-syntax-reference.md#fql_decimal_operator) <br/> |<span data-ttu-id="bc868-264">Stellt die explizite Eingabe numerischer Werte zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="bc868-264">Provides explicit typing of numeric values.</span></span>  <br/> <span data-ttu-id="bc868-p118">Die explizite Typumwandlung ist optional und normalerweise nicht notwendig. Der Typ des Abfragebegriffs wird gemäß dem Typ der numerischen verwalteten Zieleigenschaft erkannt.</span><span class="sxs-lookup"><span data-stu-id="bc868-p118">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>  <br/> |<span data-ttu-id="bc868-267">Numeric</span><span class="sxs-lookup"><span data-stu-id="bc868-267">Numeric</span></span>  <br/> |
| [<span data-ttu-id="bc868-268">ENDS-WITH</span><span class="sxs-lookup"><span data-stu-id="bc868-268">ENDS-WITH</span></span>](fast-query-language-fql-syntax-reference.md#fql_endswith_operator) <br/> |<span data-ttu-id="bc868-269">Gibt an, dass ein Wort oder eine Phrase am Ende einer verwalteten Eigenschaft angezeigt werden muss.</span><span class="sxs-lookup"><span data-stu-id="bc868-269">Specifies that a word or phrase must appear in the end of a managed property.</span></span>  <br/> |<span data-ttu-id="bc868-270">Näherung</span><span class="sxs-lookup"><span data-stu-id="bc868-270">Proximity</span></span>  <br/> |
| [<span data-ttu-id="bc868-271">EQUALS</span><span class="sxs-lookup"><span data-stu-id="bc868-271">EQUALS</span></span>](fast-query-language-fql-syntax-reference.md#fql_equals_operator) <br/> |<span data-ttu-id="bc868-272">Gibt an, dass ein Wort, ein Phrasenbegriff oder eine Phrase eine genaue Tokenübereinstimmung mit der verwalteten Eigenschaft aufweisen muss.</span><span class="sxs-lookup"><span data-stu-id="bc868-272">Specifies that a word or phrase term or phrase must provide an exact token match with the managed property.</span></span>  <br/> |<span data-ttu-id="bc868-273">Näherung</span><span class="sxs-lookup"><span data-stu-id="bc868-273">Proximity</span></span>  <br/> |
| [<span data-ttu-id="bc868-274">FILTER</span><span class="sxs-lookup"><span data-stu-id="bc868-274">FILTER</span></span>](fast-query-language-fql-syntax-reference.md#fql_filter_operator) <br/> |<span data-ttu-id="bc868-275">Wird verwendet, um Metadaten oder andere strukturierte Daten abzufragen.</span><span class="sxs-lookup"><span data-stu-id="bc868-275">Used to query metadata or other structured data.</span></span>  <br/> |<span data-ttu-id="bc868-276">Relevanz</span><span class="sxs-lookup"><span data-stu-id="bc868-276">Relevance</span></span>  <br/> |
| [<span data-ttu-id="bc868-277">FLOAT</span><span class="sxs-lookup"><span data-stu-id="bc868-277">FLOAT</span></span>](fast-query-language-fql-syntax-reference.md#fql_float_operator) <br/> |<span data-ttu-id="bc868-278">Stellt die explizite Eingabe numerischer Werte zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="bc868-278">Provides explicit typing of numeric values.</span></span>  <br/> <span data-ttu-id="bc868-p119">Die explizite Typumwandlung ist optional und normalerweise nicht notwendig. Der Typ des Abfragebegriffs wird gemäß dem Typ der numerischen verwalteten Zieleigenschaft erkannt.</span><span class="sxs-lookup"><span data-stu-id="bc868-p119">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>  <br/> |<span data-ttu-id="bc868-281">Numeric</span><span class="sxs-lookup"><span data-stu-id="bc868-281">Numeric</span></span>  <br/> |
| [<span data-ttu-id="bc868-282">INT</span><span class="sxs-lookup"><span data-stu-id="bc868-282">INT</span></span>](fast-query-language-fql-syntax-reference.md#fql_int_operator) <br/> |<span data-ttu-id="bc868-283">Stellt die explizite Eingabe numerischer Werte zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="bc868-283">Provides explicit typing of numeric values.</span></span>  <br/> <span data-ttu-id="bc868-p120">Die explizite Typumwandlung ist optional und normalerweise nicht notwendig. Der Typ des Abfragebegriffs wird gemäß dem Typ der numerischen verwalteten Zieleigenschaft erkannt.</span><span class="sxs-lookup"><span data-stu-id="bc868-p120">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>  <br/> |<span data-ttu-id="bc868-286">Numeric</span><span class="sxs-lookup"><span data-stu-id="bc868-286">Numeric</span></span>  <br/> |
| [<span data-ttu-id="bc868-287">NEAR</span><span class="sxs-lookup"><span data-stu-id="bc868-287">NEAR</span></span>](fast-query-language-fql-syntax-reference.md#fql_near_operator) <br/> |<span data-ttu-id="bc868-288">Beschränkt die Ergebnismenge auf Elemente, die  `N` Begriffe innerhalb eines bestimmten Abstands voneinander aufweisen.</span><span class="sxs-lookup"><span data-stu-id="bc868-288">Restricts the result set to items that have  `N` terms within a certain distance of one another.</span></span> <br/> |<span data-ttu-id="bc868-289">Näherung</span><span class="sxs-lookup"><span data-stu-id="bc868-289">Proximity</span></span>  <br/> |
| [<span data-ttu-id="bc868-290">NOT</span><span class="sxs-lookup"><span data-stu-id="bc868-290">NOT</span></span>](fast-query-language-fql-syntax-reference.md#fql_not_operator) <br/> |<span data-ttu-id="bc868-291">Gibt nur Elemente zurück, die den Operanden ausschließen.</span><span class="sxs-lookup"><span data-stu-id="bc868-291">Returns only items that exclude the operand.</span></span>  <br/> |<span data-ttu-id="bc868-292">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="bc868-292">Boolean</span></span>  <br/> |
| [<span data-ttu-id="bc868-293">ONEAR</span><span class="sxs-lookup"><span data-stu-id="bc868-293">ONEAR</span></span>](fast-query-language-fql-syntax-reference.md#fql_onear_operator) <br/> |<span data-ttu-id="bc868-p121">Die sortierte Variante von **NEAR**, die eine sortierte Zuordnung der Begriffe erfordert. Der Operator **ONEAR** kann verwendet werden, um die Ergebnismenge auf Elemente mit `N` Begriffen zu beschränken, die sich in einem bestimmten Abstand voneinander befinden. Gibt nur Elemente zurück, die nicht mit dem Operanden übereinstimmen. Der Operand kann jeder gültige FQL-Ausdruck sein. </span><span class="sxs-lookup"><span data-stu-id="bc868-p121">The ordered variant of **NEAR**, and requires an ordered match of the terms. The **ONEAR** operator can be used to restrict the result set to items that have `N` terms within a certain distance of Returns only items that don't match the operand. The operand may be any valid FQL expression.one another. </span></span><br/> |<span data-ttu-id="bc868-297">Näherung</span><span class="sxs-lookup"><span data-stu-id="bc868-297">Proximity</span></span>  <br/> |
| [<span data-ttu-id="bc868-298">OR</span><span class="sxs-lookup"><span data-stu-id="bc868-298">OR</span></span>](fast-query-language-fql-syntax-reference.md#fql_or_operator) <br/> |<span data-ttu-id="bc868-299">Gibt nur Elemente zurück, die mindestens einem der **OR**-Operanden entsprechen.</span><span class="sxs-lookup"><span data-stu-id="bc868-299">Returns only items that match at least one of the **OR** operands.</span></span> <span data-ttu-id="bc868-300">Übereinstimmende Elemente werden in der dynamischen Rangfolge (Relevanzbewertung in der Ergebnismenge) weiter oben angegeben, wenn mehrere der **OR**-Operanden übereinstimmen. </span><span class="sxs-lookup"><span data-stu-id="bc868-300">Items that match will get a higher dynamic rank (relevance score in the result set.md) if more of the **OR** operands match.</span></span> <br/> |<span data-ttu-id="bc868-301">Boolescher Wert</span><span class="sxs-lookup"><span data-stu-id="bc868-301">Boolean</span></span>  <br/> |
| [<span data-ttu-id="bc868-302">PHRASE</span><span class="sxs-lookup"><span data-stu-id="bc868-302">PHRASE</span></span>](fast-query-language-fql-syntax-reference.md#fql_phrase_operator) <br/> | <span data-ttu-id="bc868-303">Gibt nur Elemente zurück, die einer genauen Tokenzeichenfolge entsprechen.</span><span class="sxs-lookup"><span data-stu-id="bc868-303">Returns only items that match an exact string of tokens.</span></span> <br/> |<span data-ttu-id="bc868-304">Näherung</span><span class="sxs-lookup"><span data-stu-id="bc868-304">Proximity</span></span>  <br/> |
| [<span data-ttu-id="bc868-305">RANGE</span><span class="sxs-lookup"><span data-stu-id="bc868-305">RANGE</span></span>](fast-query-language-fql-syntax-reference.md#fql_range_operator) <br/> | <span data-ttu-id="bc868-p123">Ermöglicht mit Bereichen übereinstimmende Ausdrücke. Der Operator **RANGE** wird für numerische verwaltete Eigenschaften und verwaltete Eigenschaften für Datum/Uhrzeit verwendet.</span><span class="sxs-lookup"><span data-stu-id="bc868-p123">Enables range matching expressions. The **RANGE** operator is used for numeric and date/time managed properties. </span></span><br/> |<span data-ttu-id="bc868-308">Numeric</span><span class="sxs-lookup"><span data-stu-id="bc868-308">Numeric</span></span>  <br/> |
| [<span data-ttu-id="bc868-309">STARTS-WITH</span><span class="sxs-lookup"><span data-stu-id="bc868-309">STARTS-WITH</span></span>](fast-query-language-fql-syntax-reference.md#fql_startswith_operator) <br/> |<span data-ttu-id="bc868-310">Gibt an, dass ein Wort oder eine Phrase am Anfang einer verwalteten Eigenschaft angezeigt werden muss.</span><span class="sxs-lookup"><span data-stu-id="bc868-310">Specifies that a word or phrase must appear in the start of a managed property.</span></span>  <br/> |<span data-ttu-id="bc868-311">Näherung</span><span class="sxs-lookup"><span data-stu-id="bc868-311">Proximity</span></span>  <br/> |
| [<span data-ttu-id="bc868-312">STRING</span><span class="sxs-lookup"><span data-stu-id="bc868-312">STRING</span></span>](fast-query-language-fql-syntax-reference.md#fql_string_operator) <br/> |<span data-ttu-id="bc868-313">Definiert eine übereinstimmende boolesche Bedingung für eine Textzeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="bc868-313">Define a Boolean matching condition to a text string.</span></span>  <br/> |<span data-ttu-id="bc868-314">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="bc868-314">String</span></span>  <br/> |
| [<span data-ttu-id="bc868-315">XRANK</span><span class="sxs-lookup"><span data-stu-id="bc868-315">XRANK</span></span>](fast-query-language-fql-syntax-reference.md#fql_xrank_operator) <br/> |<span data-ttu-id="bc868-p124">Ermöglicht es Ihnen, die dynamische Rangfolge von Elementen basierend auf bestimmten Begriffsvorkommen zu erhöhen, ohne zu ändern, welche Elemente mit der Abfrage übereinstimmen. Ein **XRANK** -Ausdruck enthält eine Komponente, die abgeglichen werden muss, und eine oder mehrere Komponenten, die nur für die dynamische Rangfolge relevant sind.</span><span class="sxs-lookup"><span data-stu-id="bc868-p124">Enables you to boost the dynamic rank of items based on certain term occurrences without changing which items match the query. A **XRANK** expression contains one component that must be matched, and one or more components that contribute only to dynamic ranking. </span></span><br/> |<span data-ttu-id="bc868-318">Relevanz</span><span class="sxs-lookup"><span data-stu-id="bc868-318">Relevance</span></span>  <br/> |
   
> [!NOTE]
> <span data-ttu-id="bc868-319">In SharePoint wird der Operator **RANK** nicht mehr unterstützt und ist daher wirkungslos.</span><span class="sxs-lookup"><span data-stu-id="bc868-319">Note: In SharePoint, the **RANK** operator is deprecated and will no longer have any effect.</span></span> <span data-ttu-id="bc868-320">Verwenden Sie stattdessen den Operator **XRANK**.</span><span class="sxs-lookup"><span data-stu-id="bc868-320">Use **XRANK** instead.</span></span>
  
    
    


### <a name="and"></a><span data-ttu-id="bc868-321">AND</span><span class="sxs-lookup"><span data-stu-id="bc868-321">AND</span></span>
<span data-ttu-id="bc868-322"><a name="fql_and_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-322"><a name="fql_and_operator"> </a></span></span>

<span data-ttu-id="bc868-p126">Gibt nur Elemente zurück, die mit allen **AND** -Operanden übereinstimmen. Bei den Operanden kann es sich um einen einzelnen Begriff oder einen beliebigen gültigen FQL-Unterausdruck handeln.</span><span class="sxs-lookup"><span data-stu-id="bc868-p126">Returns only items that match all **AND** operands. The operands may be a single term or any valid FQL sub-expression.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-325">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-325">Syntax</span></span>

 `and(operand, operand [, operand]*)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-326">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-326">Parameters</span></span>

<span data-ttu-id="bc868-327">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="bc868-327">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="bc868-328">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-328">Examples</span></span>

<span data-ttu-id="bc868-329">Der folgende Ausdruck gleicht Elemente ab, bei denen der Standard-Volltextindex den Begriff „Katze", „Hund" und „Fuchs" enthält.</span><span class="sxs-lookup"><span data-stu-id="bc868-329">The following expression matches items for which the default full-text index contains "cat", "dog", and "fox".</span></span>
  
    
    
 `and(cat, dog, fox)`
  
    
    

### <a name="andnot"></a><span data-ttu-id="bc868-330">ANDNOT</span><span class="sxs-lookup"><span data-stu-id="bc868-330">ANDNOT</span></span>
<span data-ttu-id="bc868-331"><a name="fql_andnot_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-331"><a name="fql_andnot_operator"> </a></span></span>

<span data-ttu-id="bc868-p127">Gibt nur Elemente zurück, die mit dem ersten Operanden und nicht mit den nachfolgenden Operanden überstimmen. Bei den Operanden kann es sich um einen einzelnen Begriff oder einen beliebigen gültigen FQL-Unterausdruck handeln.</span><span class="sxs-lookup"><span data-stu-id="bc868-p127">Returns only items that match the first operand and that don't match the subsequent operands. The operands may be a single term or any valid FQL sub-expression.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-334">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-334">Syntax</span></span>

 `andnot(operand, operand [,operand]*)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-335">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-335">Parameters</span></span>

<span data-ttu-id="bc868-336">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="bc868-336">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="bc868-337">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-337">Examples</span></span>

 <span data-ttu-id="bc868-p128">**Beispiel 1**: Der folgende Ausdruck gleicht Elemente ab, bei denen der Standard-Volltextindex den Begriff „Katze", aber nicht den Begriff „Hund" enthält.</span><span class="sxs-lookup"><span data-stu-id="bc868-p128">**Example 1.** The following expression matches items for which the default full-text index contains "cat" but not "dog".</span></span>
  
    
    
 `andnot(cat, dog)`
  
    
    
 <span data-ttu-id="bc868-p129">**Beispiel 2**: Der folgende Ausdruck gleicht Elemente ab, bei denen der Standard-Volltextindex den Begriff „Hund", aber weder „Beagle" noch „Chihuahua" enthält.</span><span class="sxs-lookup"><span data-stu-id="bc868-p129">**Example 2.** The following expression matches items for which the default full-text index contains "dog" but neither "beagle" nor "chihuahua".</span></span>
  
    
    
 `andnot(dog, beagle, chihuahua)`
  
    
    

### <a name="any"></a><span data-ttu-id="bc868-342">ANY</span><span class="sxs-lookup"><span data-stu-id="bc868-342">ANY</span></span>
<span data-ttu-id="bc868-343"><a name="fql_any_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-343"><a name="fql_any_operator"> </a></span></span>

> [!NOTE]
> <span data-ttu-id="bc868-344">In SharePoint wird der **ANY**-Operator nicht mehr unterstützt.</span><span class="sxs-lookup"><span data-stu-id="bc868-344">Note: In SharePoint, the **ANY** operator is deprecated.</span></span> <span data-ttu-id="bc868-345">Verwenden Sie stattdessen den **OR**-Operator.</span><span class="sxs-lookup"><span data-stu-id="bc868-345">Use the **OR** operator instead.</span></span>
  
    
    

<span data-ttu-id="bc868-p131">Ähnelt dem Operanden  [OR](fast-query-language-fql-syntax-reference.md#fql_or_operator), abgesehen davon, dass die dynamische Rangfolge (die Relevanzbewertung in der Ergebnismenge) weder von der Anzahl der übereinstimmenden Operanden noch vom Abstand zwischen den Begriffen im Element betroffen ist. Bei den Operanden kann es sich um einen einzelnen Begriff oder einen beliebigen gültigen FQL-Unterausdruck handeln.</span><span class="sxs-lookup"><span data-stu-id="bc868-p131">Similar to the  [OR](fast-query-language-fql-syntax-reference.md#fql_or_operator) operator except that the dynamic rank (the relevance score in the result set) is affected by neither the number of operands that match nor the distance between the terms in the item. The operands may be a single term or any valid FQL sub-expression.</span></span>
  
    
    
<span data-ttu-id="bc868-348">Die dynamische Rangkomponente für diesen Teil der Abfrage basiert auf dem am besten passenden Begriff im **ANY**-Ausdruck.</span><span class="sxs-lookup"><span data-stu-id="bc868-348">The dynamic ranking component for this part of the query is based on the best matching term within the **ANY** expression.</span></span>
  
> [!NOTE]
> <span data-ttu-id="bc868-349">Der Unterschied zu **OR** bezieht sich nur auf die Rangfolge innerhalb der Ergebnismenge.</span><span class="sxs-lookup"><span data-stu-id="bc868-349">Note: The difference from **OR** is related only to the ranking within the result set.</span></span> <span data-ttu-id="bc868-350">Die Abfrage gleicht dieselbe Gesamtmenge von Elementen ab.</span><span class="sxs-lookup"><span data-stu-id="bc868-350">The same total set of items will match the query.</span></span>
  
    
    


#### <a name="syntax"></a><span data-ttu-id="bc868-351">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-351">Syntax</span></span>

 `any(operand, operand [,operand]*)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-352">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-352">Parameters</span></span>

<span data-ttu-id="bc868-353">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="bc868-353">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="bc868-354">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-354">Examples</span></span>

 <span data-ttu-id="bc868-355">Der folgende Ausdruck gleicht Elemente ab, bei denen der Standard-Volltextindex den Begriff „Katze" oder „Hund" enthält.</span><span class="sxs-lookup"><span data-stu-id="bc868-355">The following expression matches items for which the default full-text index contains "cat" or "dog".</span></span>
  
    
    
<span data-ttu-id="bc868-356">Wenn der Index sowohl „Katze" als auch „Hund" enthält, „Katze" aber als der bessere Treffer betrachtet wird, basiert die dynamische Rangfolge des Elements auf dem Begriff „Katze", und der Begriff „Hund" wird nicht berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="bc868-356">If the index contains both "cat" and "dog", but "cat" is considered a better match, the 'item's dynamic rank will be based on "cat" with no consideration given to "dog".</span></span>
  
    
    
 `any(cat, dog)`
  
    
    

### <a name="count"></a><span data-ttu-id="bc868-357">COUNT</span><span class="sxs-lookup"><span data-stu-id="bc868-357">COUNT</span></span>
<span data-ttu-id="bc868-358"><a name="fql_count_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-358"><a name="fql_count_operator"> </a></span></span>

<span data-ttu-id="bc868-p133">Gibt an, wie oft ein Abfragebegriff in einem Element enthalten sein muss, damit das Element als Ergebnis zurückgegeben wird. Der Operand kann ein einzelner Abfragebegriff, eine Phrase oder ein Abfragebegriff mit Platzhalter sein.</span><span class="sxs-lookup"><span data-stu-id="bc868-p133">Specifies the of number query term occurrences an item must include for the item to be returned as a result. The operand may be a single query term, a phrase, or a wildcard query term.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-361">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-361">Syntax</span></span>

 `property-spec:count(operand [,from=<numeric value>, to=<numeric value>])`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-362">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-362">Parameters</span></span>



|<span data-ttu-id="bc868-363">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="bc868-363">**Parameter**</span></span>|<span data-ttu-id="bc868-364">**Wert**</span><span class="sxs-lookup"><span data-stu-id="bc868-364">**Value**</span></span>|<span data-ttu-id="bc868-365">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="bc868-365">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="bc868-366">_From_</span><span class="sxs-lookup"><span data-stu-id="bc868-366">_From_</span></span> <br/> | <span data-ttu-id="bc868-367">_\<numeric_value\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-367">_\<numeric_value\>_</span></span> <br/> |<span data-ttu-id="bc868-368">Der Wert des Parameters  _from_ muss eine positive ganze Zahl sein, die angibt, wie oft eine Übereinstimmung des Operanden mindestens erzielt werden muss.</span><span class="sxs-lookup"><span data-stu-id="bc868-368">The value of the  _from_ parameter must be a positive integer that specifies the minimum number of times that the specified operand must be matched.</span></span> <br/> <span data-ttu-id="bc868-369">Wenn der Parameter  _from_ nicht angegeben ist, ist kein unterer Grenzwert vorhanden.</span><span class="sxs-lookup"><span data-stu-id="bc868-369">If the  _from_ parameter is not specified, no lower limit will exist.</span></span> <br/> |
| <span data-ttu-id="bc868-370">_to_</span><span class="sxs-lookup"><span data-stu-id="bc868-370">_to_</span></span> <br/> | <span data-ttu-id="bc868-371">_\<numeric_value\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-371">_\<numeric_value\>_</span></span> <br/> |<span data-ttu-id="bc868-p134">Der Wert des Parameters  _to_ muss eine positive ganze Zahl sein, die angibt, wie oft eine Übereinstimmung des Operanden höchstens (nicht inklusive) erzielt werden muss. Beispielsweise gibt ein _to_-Wert von **11** eine Übereinstimmung von 10 Mal oder weniger an. </span><span class="sxs-lookup"><span data-stu-id="bc868-p134">The value of the  _to_ parameter must be a positive integer that specifies the non-inclusive maximum number of times that the specified operand must be matched. For example, a _to_ value of **11** specifies 10 times or fewer. </span></span><br/> <span data-ttu-id="bc868-374">Wenn der Parameter  _to_ nicht angegeben ist, ist kein oberer Grenzwert vorhanden.</span><span class="sxs-lookup"><span data-stu-id="bc868-374">If the  _to_ parameter is not specified, no upper limit will exist.</span></span> <br/> |
   

#### <a name="examples"></a><span data-ttu-id="bc868-375">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-375">Examples</span></span>

 <span data-ttu-id="bc868-p135">**Beispiel 1**: Der folgende Ausdruck gleicht mindestens 5 Vorkommen des Begriffs "Katze" ab.</span><span class="sxs-lookup"><span data-stu-id="bc868-p135">**Example 1.** The following expression matches at least 5 occurrences of the word "cat".</span></span>
  
    
    
 `count(cat, from=5)`
  
    
    
 <span data-ttu-id="bc868-p136">**Beispiel 2**: Der folgende Ausdruck gleicht mindestens 5, aber nicht 10 oder mehr Vorkommen des Begriffs "Katze" ab.</span><span class="sxs-lookup"><span data-stu-id="bc868-p136">**Example 2.** The following expression matches at least 5 but not 10 or more occurrences of the word "cat".</span></span>
  
    
    
 `count(cat, from=5, to=10)`
  
    
    
 <span data-ttu-id="bc868-p137">**Beispiel 3**: Jeder der folgenden Ausdrücke gleicht mindestens 3 Vorkommen eines bestimmten Worts ab. Das Wort kann entweder „Katze" oder „Hund" sein.</span><span class="sxs-lookup"><span data-stu-id="bc868-p137">**Example 3.** Each of the following expressions matches at least 3 occurrences of a certain word, and that word can be either "cat" or "dog".</span></span>
  
    
    
 `count(or(cat, dog), from=3)count(string("cat dog", mode="or"), from=3)`
  
    
    
<span data-ttu-id="bc868-382">Die folgende Tabelle enthält Beispiele der Zeichenfolgenwerte der verwalteten Eigenschaft und gibt an, ob diese mit den beiden Ausdrücken in Beispiel 3 übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="bc868-382">The following table contains examples of managed property string values and states whether they match the two expressions in Example 3.</span></span>
  
    
    


|<span data-ttu-id="bc868-383">**Treffer?**</span><span class="sxs-lookup"><span data-stu-id="bc868-383">**Match?**</span></span>|<span data-ttu-id="bc868-384">**Text**</span><span class="sxs-lookup"><span data-stu-id="bc868-384">**Text**</span></span>|
|:-----|:-----|
|<span data-ttu-id="bc868-385">Ja</span><span class="sxs-lookup"><span data-stu-id="bc868-385">Yes</span></span>  <br/> |<span data-ttu-id="bc868-386">Meine Katze mag meinen Hund, aber mein Hund hasst meine Katze.</span><span class="sxs-lookup"><span data-stu-id="bc868-386">My cat likes my dog, but my dog hates my cat.</span></span>  <br/> |
|<span data-ttu-id="bc868-387">Nein</span><span class="sxs-lookup"><span data-stu-id="bc868-387">No</span></span>  <br/> |<span data-ttu-id="bc868-388">Mein Vogel mag meinen Molch, aber mein Hund hasst meine Katze.</span><span class="sxs-lookup"><span data-stu-id="bc868-388">My bird likes my newt, but my dog hates my cat.</span></span>  <br/> |
   

### <a name="datetime"></a><span data-ttu-id="bc868-389">DATETIME</span><span class="sxs-lookup"><span data-stu-id="bc868-389">DATETIME</span></span>
<span data-ttu-id="bc868-390"><a name="fql_datetime_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-390"><a name="fql_datetime_operator"> </a></span></span>

<span data-ttu-id="bc868-p138">Stellt die explizite Eingabe numerischer Werte für Datum/Uhrzeit zur Verfügung. Der Operand ist eine Datum-/Uhrzeitzeichenfolge, die gemäß der unter  [Tokenausdrücke in FQL](fast-query-language-fql-syntax-reference.md#token_expressions) angegebenen Syntax formatiert ist.</span><span class="sxs-lookup"><span data-stu-id="bc868-p138">Provides explicit typing of date/time numeric values. The operand is a date/time string formatted according to the syntax specified in  [Token expressions in FQL](fast-query-language-fql-syntax-reference.md#token_expressions).</span></span>
  
    
    
<span data-ttu-id="bc868-p139">Die explizite Typumwandlung ist optional und normalerweise nicht notwendig. Der Typ des Abfragebegriffs wird gemäß dem Typ der numerischen verwalteten Zieleigenschaft erkannt.</span><span class="sxs-lookup"><span data-stu-id="bc868-p139">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-395">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-395">Syntax</span></span>

 `datetime(<date/time string>)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-396">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-396">Parameters</span></span>

<span data-ttu-id="bc868-397">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="bc868-397">Not applicable.</span></span>
  
    
    

### <a name="decimal"></a><span data-ttu-id="bc868-398">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="bc868-398">DECIMAL</span></span>
<span data-ttu-id="bc868-399"><a name="fql_decimal_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-399"><a name="fql_decimal_operator"> </a></span></span>

<span data-ttu-id="bc868-p140">Stellt die explizite Eingabe von Dezimalwerten zur Verfügung. Der Operand ist ein Dezimalwert gemäß der unter  [Tokenausdrücke in FQL](fast-query-language-fql-syntax-reference.md#token_expressions) angegebenen Syntax.</span><span class="sxs-lookup"><span data-stu-id="bc868-p140">Provides explicit typing of decimal values. The operand is a decimal value according to the syntax specified in  [Token expressions in FQL](fast-query-language-fql-syntax-reference.md#token_expressions).</span></span>
  
    
    
<span data-ttu-id="bc868-p141">Die explizite Typumwandlung ist optional und normalerweise nicht notwendig. Der Typ des Abfragebegriffs wird gemäß dem Typ der numerischen verwalteten Zieleigenschaft erkannt.</span><span class="sxs-lookup"><span data-stu-id="bc868-p141">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-404">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-404">Syntax</span></span>

 `decimal(<decimal point value>)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-405">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-405">Parameters</span></span>

<span data-ttu-id="bc868-406">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="bc868-406">Not applicable.</span></span>
  
    
    

### <a name="ends-with"></a><span data-ttu-id="bc868-407">ENDS-WITH</span><span class="sxs-lookup"><span data-stu-id="bc868-407">ENDS-WITH</span></span>
<span data-ttu-id="bc868-408"><a name="fql_endswith_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-408"><a name="fql_endswith_operator"> </a></span></span>

<span data-ttu-id="bc868-409">Gibt an, dass ein Wort oder eine Phrase am Ende einer verwalteten Eigenschaft angezeigt werden muss (Begrenzungsabgleich).</span><span class="sxs-lookup"><span data-stu-id="bc868-409">Specifies that a word or phrase must appear in the end of a managed property (boundary matching).</span></span>
  
    
    
<span data-ttu-id="bc868-p142">Der Begrenzungsabgleich wird bei numerischen verwalteten Eigenschaften nicht unterstützt. Numerische verwaltete Eigenschaften unterliegen stets dem Abgleich von exakten Werten oder Wertebereichen.</span><span class="sxs-lookup"><span data-stu-id="bc868-p142">Boundary matching is not supported on numeric managed properties. Numeric managed properties will always be subject to exact or value range matching.</span></span> 
  
    
    
<span data-ttu-id="bc868-p143">Einige Anwendungen erfordern möglicherweise, dass Sie einen exakten Abgleich einer verwalteten Eigenschaft durchführen können. Dies kann beispielsweise eine verwaltete **product name**-Eigenschaft sein, bei der der vollständige Name eines Produkts eine Teilzeichenfolge eines anderen Produktnamens ist.</span><span class="sxs-lookup"><span data-stu-id="bc868-p143">Some applications may require that you are able to perform an exact match of a managed property. For example, this may be a **product name** managed property, where the full name of one product is a substring of another product name.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-414">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-414">Syntax</span></span>

 `ends-with(<term or phrase>)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-415">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-415">Parameters</span></span>

<span data-ttu-id="bc868-416">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="bc868-416">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="bc868-417">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-417">Examples</span></span>

<span data-ttu-id="bc868-p144">Der folgende Ausdruck gleicht Elemente mit den Werten „Herr Adam Jones" und „Adam Jones" in der verwalteten Eigenschaft „author" ab. Elemente mit dem Wert „Mr. Adam Jones" werden nicht gefunden.</span><span class="sxs-lookup"><span data-stu-id="bc868-p144">The following expression matches items with the values "Mr Adam Jones" and "Adam Jones" in the "author" managed property. It will not match items with the value "Adam Jones sr".</span></span>
  
    
    
 `author:ends-with("adam jones")`
  
    
    

#### <a name="remarks"></a><span data-ttu-id="bc868-420">HinwBemerkungeneise</span><span class="sxs-lookup"><span data-stu-id="bc868-420">Remarks</span></span>

<span data-ttu-id="bc868-p145">Der Begrenzungsabgleich kann auf den gesamten Text der verwalteten Eigenschaft angewendet werden, oder auf einzelne Zeichenfolgen innerhalb einer verwalteten Eigenschaft, die eine Liste von Werten enthält (beispielsweise eine Liste mit Namen). In diesem Fall empfiehlt es sich, den genauen Inhalt jeder Zeichenfolge abzugleichen, und Abgleichsabfragen über Zeichenfolgengrenzen hinweg zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="bc868-p145">Boundary matching can be applied to all the text of the managed property, or to individual strings within a managed property that contains a list of string values, for example, a list of names. In this case, you may want to match the exact content of each string, and to avoid query matching across string boundaries.</span></span> 
  
    
    
<span data-ttu-id="bc868-423">Um Begrenzungsabgleichsabfragen durchzuführen, müssen Sie die relevante verwaltete Eigenschaft im Indexschema konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="bc868-423">To apply boundary match queries, you must configure the relevant managed property in the index schema.</span></span> 
  
    
    
<span data-ttu-id="bc868-424">Wenn Sie das Begrenzungsabgleichsfeature für die verwaltete Eigenschaft aktivieren, können Sie Folgendes durchführen:</span><span class="sxs-lookup"><span data-stu-id="bc868-424">By enabling the Boundary Match feature for the managed property, you can do the following:</span></span> 
  
    
    

- <span data-ttu-id="bc868-425">Verwenden expliziter Begrenzungsabgleichsabfragen</span><span class="sxs-lookup"><span data-stu-id="bc868-425">Use explicit boundary match queries.</span></span> 
    
  
- <span data-ttu-id="bc868-p146">Verhindern, dass Phrasen über Zeichenfolgengrenzen hinweg abgeglichen werden. Für verwaltete Eigenschaften, die mehrere Zeichenfolgen enthalten, stellt dieses Feature sicher, dass eine Zeichenfolge vor oder nach einer Begrenzungsangabe keine Wörter abgleicht.</span><span class="sxs-lookup"><span data-stu-id="bc868-p146">Prevent phrases from matching across string boundaries. For managed properties that contain multiple strings, this feature will ensure that a string does not match words before or after a boundary indication.</span></span>
    
  

### <a name="equals"></a><span data-ttu-id="bc868-428">EQUALS</span><span class="sxs-lookup"><span data-stu-id="bc868-428">EQUALS</span></span>
<span data-ttu-id="bc868-429"><a name="fql_equals_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-429"><a name="fql_equals_operator"> </a></span></span>

<span data-ttu-id="bc868-430">Gibt an, dass ein Wort oder eine Phrase eine genaue Tokenübereinstimmung mit der verwalteten Eigenschaft aufweisen muss.</span><span class="sxs-lookup"><span data-stu-id="bc868-430">Specifies that a word or phrase must provide an exact token match with the managed property.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-431">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-431">Syntax</span></span>

 `equals(<term or phrase>)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-432">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-432">Parameters</span></span>

<span data-ttu-id="bc868-433">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="bc868-433">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="bc868-434">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-434">Examples</span></span>

<span data-ttu-id="bc868-p147">Das folgende Beispiel gleicht Elemente mit den Werten „Adam Jones"" in der verwalteten Eigenschaft „author" ab. Elemente mit den Werten „Mr. Adam Jones" oder „Herr Adam Jones" werden nicht gefunden.</span><span class="sxs-lookup"><span data-stu-id="bc868-p147">The following example will match items with the values "Adam Jones" in the "author" managed property. It will not match items with the values "Adam Jones sr" or "Mr Adam Jones".</span></span>
  
    
    
 `author:equals("adam jones")`
  
    
    

#### <a name="remarks"></a><span data-ttu-id="bc868-437">HinwBemerkungeneise</span><span class="sxs-lookup"><span data-stu-id="bc868-437">Remarks</span></span>

<span data-ttu-id="bc868-438">Siehe auch  [ENDS-WITH](fast-query-language-fql-syntax-reference.md#fql_endswith_operator).</span><span class="sxs-lookup"><span data-stu-id="bc868-438">See also  [ENDS-WITH](fast-query-language-fql-syntax-reference.md#fql_endswith_operator).</span></span>
  
    
    

### <a name="filter"></a><span data-ttu-id="bc868-439">FILTER</span><span class="sxs-lookup"><span data-stu-id="bc868-439">FILTER</span></span>
<span data-ttu-id="bc868-440"><a name="fql_filter_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-440"><a name="fql_filter_operator"> </a></span></span>

<span data-ttu-id="bc868-441">Wird verwendet, um Metadaten oder andere strukturierte Daten abzufragen.</span><span class="sxs-lookup"><span data-stu-id="bc868-441">Used to query metadata or other structured data.</span></span> 
  
    
    
<span data-ttu-id="bc868-442">Die Verwendung des Operators **FILTER** impliziert Folgendes für die angegebene Abfrage:</span><span class="sxs-lookup"><span data-stu-id="bc868-442">Using the **FILTER** operator automatically implies the following for the specified query:</span></span>
  
    
    

- <span data-ttu-id="bc868-443">Die Linguistik wird auf linguistics="OFF" festgelegt.</span><span class="sxs-lookup"><span data-stu-id="bc868-443">Linguistics will be set to linguistics="OFF".</span></span>
    
  
- <span data-ttu-id="bc868-444">Die Rangfolge wird deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="bc868-444">Ranking will be disabled.</span></span>
    
  
- <span data-ttu-id="bc868-445">Es wird keine Hervorhebung der Abfrage in der hervorgehobenen Trefferzusammenfassung für den Abfrage-Ergebnistreffer verwendet.</span><span class="sxs-lookup"><span data-stu-id="bc868-445">No query highlighting will be used in the hit highlighted summary for the query result hit.</span></span>
    
  

> <span data-ttu-id="bc868-446">**Tipp:** Wenn Sie den **STRING**-Operator in einem **FILTER**-Ausdruck verwenden, ist Linguistik standardmäßig deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="bc868-446">**Tip:** If you use the **STRING** operator inside a **FILTER** expression, by default, linguistics is disabled.</span></span> <span data-ttu-id="bc868-447">Sie können die Linguistikverarbeitung, die in jedem **STRING**-Ausdruck im **FILTER** durchgeführt wird, mit dem Operand `linguistics="ON"` aktivieren.</span><span class="sxs-lookup"><span data-stu-id="bc868-447">You can enable linguistics processing within each **STRING** expression inside **FILTER** by using the operand `linguistics="ON"`.</span></span> 
  
    
    


#### <a name="syntax"></a><span data-ttu-id="bc868-448">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-448">Syntax</span></span>

 `filter(<any valid FQL operator expression>)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-449">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-449">Parameters</span></span>

<span data-ttu-id="bc868-450">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="bc868-450">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="bc868-451">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-451">Examples</span></span>

<span data-ttu-id="bc868-p149">Der folgende Ausdruck gleicht Elemente mit einer verwalteten **Title**-Eigenschaft ab, die „Sonate" enthält, und einer verwalteten **Doctype**-Eigenschaft, die nur das Token „Audio" enthält. Für „Audio" wird kein linguistischer Abgleich durchgeführt. Da das Token **FILTER** zum Abgleich von „Audio" verwendet wird, wird dieser Text in der Zusammenfassung mit hervorgehobenen Treffern nicht hervorgehoben.</span><span class="sxs-lookup"><span data-stu-id="bc868-p149">The following expression matches items that have a **Title** managed property that contains "sonata" and a **Doctype** managed property that contains only the token "audio". No linguistic matching will be performed on "audio". Because the **FILTER** token will be used to match "audio", that text will not be highlighted in the hit highlighted summary.</span></span>
  
    
    
 `and(title:sonata, filter(doctype:equals("audio")))`
  
    
    

#### <a name="remarks"></a><span data-ttu-id="bc868-455">HinwBemerkungeneise</span><span class="sxs-lookup"><span data-stu-id="bc868-455">Remarks</span></span>

<span data-ttu-id="bc868-456">Wenn Sie die Abfrage so einschränken müssen, dass wenigstens ein umfangreicher Satz von Ganzzahlen in einer numerischen Eigenschaft abgeglichen werden muss, können Sie dies auf zwei funktional äquivalente Arten ausdrücken:</span><span class="sxs-lookup"><span data-stu-id="bc868-456">If you must restrict your query to match at least one of a large set of integer values in a numeric property, you can express this in two functionally equivalent ways:</span></span> 
  
    
    

-  `and(string("hello world"), filter(property-spec:or(1, 20, 453, ... , 3473)))`
    
  
-  `and(string("hello world"), filter(property-spec:int("1 20 453 ... 3473", mode="or")))`
    
  
<span data-ttu-id="bc868-p150">Im zweiten Beispiel wird der Operator **INT** mit einer Zeichenfolge verwendet, deren Gruppe numerischer Werte in doppelte Anführungszeichen eingeschlossen ist. Dadurch wird eine erheblich bessere Abfrageleistung erzielt, wenn eine umfangreiche Gruppe numerischer Werte gefiltert wird.</span><span class="sxs-lookup"><span data-stu-id="bc868-p150">The second example uses the **INT** operator by using a string with the set of numeric values in double quotation marks. This provides a significantly better query performance when filtering with a large set of numeric values.</span></span>
  
    
    
<span data-ttu-id="bc868-459">Wenn eine große Gruppe von Werten gefiltert werden muss, sollten Sie erwägen, anstelle von Zeichenfolgewerten numerische Werte zu verwenden, und Ihre Abfrage mit der optimierten Syntax ausdrücken.</span><span class="sxs-lookup"><span data-stu-id="bc868-459">If you must filter a large set of values, you should consider using numeric values instead of string values, and express your queries by using the optimized syntax.</span></span>
  
    
    

### <a name="float"></a><span data-ttu-id="bc868-460">FLOAT</span><span class="sxs-lookup"><span data-stu-id="bc868-460">FLOAT</span></span>
<span data-ttu-id="bc868-461"><a name="fql_float_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-461"><a name="fql_float_operator"> </a></span></span>

<span data-ttu-id="bc868-p151">Stellt die explizite Eingabe numerischer Gleitkommawerte zur Verfügung. Der Operand ist ein Gleitkommawert gemäß der unter  [Tokenausdrücke in FQL](fast-query-language-fql-syntax-reference.md#token_expressions) angegebenen Syntax.</span><span class="sxs-lookup"><span data-stu-id="bc868-p151">Provides explicit typing of floating point numeric values. The operand is a floating point value according to the syntax specified in  [Token expressions in FQL](fast-query-language-fql-syntax-reference.md#token_expressions).</span></span>
  
    
    
<span data-ttu-id="bc868-p152">Die explizite Typumwandlung ist optional und normalerweise nicht notwendig. Der Typ des Abfragebegriffs wird gemäß dem Typ der numerischen verwalteten Zieleigenschaft erkannt.</span><span class="sxs-lookup"><span data-stu-id="bc868-p152">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-466">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-466">Syntax</span></span>

 `float(<floating point value>)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-467">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-467">Parameters</span></span>

<span data-ttu-id="bc868-468">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="bc868-468">Not applicable.</span></span>
  
    
    

### <a name="int"></a><span data-ttu-id="bc868-469">INT</span><span class="sxs-lookup"><span data-stu-id="bc868-469">INT</span></span>
<span data-ttu-id="bc868-470"><a name="fql_int_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-470"><a name="fql_int_operator"> </a></span></span>

<span data-ttu-id="bc868-p153">Stellt die explizite Eingabe von Ganzzahlwerten zur Verfügung. Der Operand ist ein Ganzzahlwert gemäß der unter  [Tokenausdrücke in FQL](fast-query-language-fql-syntax-reference.md#token_expressions) angegebenen Syntax.</span><span class="sxs-lookup"><span data-stu-id="bc868-p153">Provides explicit typing of integer values. The operand is an integer value according to the syntax specified in  [Token expressions in FQL](fast-query-language-fql-syntax-reference.md#token_expressions).</span></span>
  
    
    
<span data-ttu-id="bc868-p154">Die explizite Typumwandlung ist optional und normalerweise nicht notwendig. Der Typ des Abfragebegriffs wird gemäß dem Typ der numerischen verwalteten Zieleigenschaft erkannt.</span><span class="sxs-lookup"><span data-stu-id="bc868-p154">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>
  
    
    
<span data-ttu-id="bc868-p155">Der Operator **INT** kann auch verwendet werden, um eine Gruppe von Ganzzahlwerten als Argumente für boolesche FQL-Operatoren auszudrücken. Dadurch wird ein leistungseffizientes Verfahren zur Verfügung gestellt, um eine Gruppe von Ganzzahlwerten in einer Abfrage anzugeben, da die Werte, die mit dem Operator **INT** übergeben werden, nicht mit der FQL-Abfrageanalyse analysiert werden, sondern direkt an die Komponente für den Abfrageabgleich übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="bc868-p155">The **INT** operator can also be used to express a set of integer values as arguments to Boolean FQL operators. This provides a performance efficient way to provide a set of integer values in a query, as the values that are passed by using the **INT** operator are not parsed by the FQL query parser but passed directly to the query matching component.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-477">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-477">Syntax</span></span>

 `int(<integer value>)`
  
    
    
 `int("value, value, ??? , value")`
  
    
    
<span data-ttu-id="bc868-p156">In der ersten Syntax wird eine einzelne ganze Zahl angegeben. Die zweite Syntax gibt eine kommagetrennte Liste von Ganzzahlwerten an, die in doppelte Anführungszeichen eingeschlossen sind.</span><span class="sxs-lookup"><span data-stu-id="bc868-p156">The first syntax specifies a single integer. The second syntax specifies a comma-separated list of integer values enclosed in double quotation marks.</span></span>
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-480">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-480">Parameters</span></span>

<span data-ttu-id="bc868-481">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="bc868-481">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="bc868-482">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-482">Examples</span></span>

<span data-ttu-id="bc868-483">Wenn Sie die Abfrage so einschränken müssen, dass mindestens ein Wert aus einer großen Gruppe von Ganzzahlwerten in einer numerischen Eigenschaft gefunden wird, können Sie dies mit dem Operator **INT** ausdrücken:</span><span class="sxs-lookup"><span data-stu-id="bc868-483">If you need to restrict your query to match at least one of a large set of integer values in a numeric property, you can express this by using the **INT** operator:</span></span>
  
    
    
 `and(string("hello world"), filter(id:int("1 20 49 124 453 985 3473", mode="or")))`
  
    
    

### <a name="near"></a><span data-ttu-id="bc868-484">NEAR</span><span class="sxs-lookup"><span data-stu-id="bc868-484">NEAR</span></span>
<span data-ttu-id="bc868-485"><a name="fql_near_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-485"><a name="fql_near_operator"> </a></span></span>

<span data-ttu-id="bc868-486">Beschränkt die Ergebnismenge auf Elemente, die  _N_ Begriffe innerhalb eines bestimmten Abstands voneinander aufweisen.</span><span class="sxs-lookup"><span data-stu-id="bc868-486">Restricts the result set to items that have  _N_ terms within a certain distance of one another.</span></span>
  
    
    
<span data-ttu-id="bc868-487">Die Reihenfolge der Abfragebegriffe ist für die Übereinstimmung nicht von Bedeutung, sondern nur der Abstand.</span><span class="sxs-lookup"><span data-stu-id="bc868-487">The order of the query terms is not important for the matching, only the distance.</span></span> 
  
    
    
<span data-ttu-id="bc868-488">Mit den **NEAR** -Operatoren kann eine beliebige Anzahl von Begriffen kombiniert werden.</span><span class="sxs-lookup"><span data-stu-id="bc868-488">Any number of terms can be combined with the **NEAR** operators.</span></span>
  
    
    
 <span data-ttu-id="bc868-p157">**NEAR** -Operanden können einzelne Begriffe, Phrasen oder boolesche Ausdrücke des Operators **OR** oder **ANY** sein. Platzhalter werden akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="bc868-p157">**NEAR** operands may be single terms, phrases, or Boolean **OR** or **ANY** operator expressions. Wildcards are accepted.</span></span>
  
    
    
<span data-ttu-id="bc868-491">Wenn mehrere Operanden des Operators **NEAR** das gleiche indizierte Token abgleichen, werden sie als nah beieinander liegend betrachtet.</span><span class="sxs-lookup"><span data-stu-id="bc868-491">If multiple operands of the **NEAR** operator match the same indexed token, they are considered near one another.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-492">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-492">Syntax</span></span>

 `near(arg, arg [, arg]* [, N=<numeric value>])`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-493">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-493">Parameters</span></span>



|<span data-ttu-id="bc868-494">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="bc868-494">**Parameter**</span></span>|<span data-ttu-id="bc868-495">**Wert**</span><span class="sxs-lookup"><span data-stu-id="bc868-495">**Value**</span></span>|<span data-ttu-id="bc868-496">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="bc868-496">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="bc868-497">_N_</span><span class="sxs-lookup"><span data-stu-id="bc868-497">_N_</span></span> <br/> | <span data-ttu-id="bc868-498">_\<numeric_value\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-498">_\<numeric_value\>_</span></span> <br/> |<span data-ttu-id="bc868-499">Gibt die maximale Anzahl von Wörtern an, die zwischen den Begriffen angezeigt werden darf (explizite Nähe).</span><span class="sxs-lookup"><span data-stu-id="bc868-499">Specifies the maximum number of words that is allowed to appear between the terms (explicit proximity).</span></span>  <br/> <span data-ttu-id="bc868-500">Wenn **NEAR** mehr als zwei Operanden enthält, wird die maximale Anzahl der zwischen den Begriffen zulässigen Wörter ( _N_) innerhalb des ganzen Ausdrucks gezählt.</span><span class="sxs-lookup"><span data-stu-id="bc868-500">If **NEAR** includes more than two operands, the maximum number of words allowed between the terms ( _N_) is counted within the whole expression.</span></span>  <br/> <span data-ttu-id="bc868-501">Standardwert: **4**</span><span class="sxs-lookup"><span data-stu-id="bc868-501">Default: **4**</span></span> <br/> |
   

#### <a name="examples"></a><span data-ttu-id="bc868-502">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-502">Examples</span></span>

 <span data-ttu-id="bc868-p158">**Beispiel 1**: Der folgende Ausdruck gleicht Zeichenfolgen ab, die die Begriffe „Katze" und „Hund" enthalten, wenn diese durch höchstens vier indizierte Token (Standardwert) getrennt sind.</span><span class="sxs-lookup"><span data-stu-id="bc868-p158">**Example 1.** The following expression matches strings that contain both "cat" and "dog" if no more than four indexed tokens (default) separate them.</span></span>
  
    
    
 `near(cat, dog)`
  
    
    
 <span data-ttu-id="bc868-p159">**Beispiel 2**: Der folgende Ausdruck gleicht Zeichenfolgen ab, die „Katze", „Hund", „Fuchs" und „Wolf" enthalten, wenn diese durch höchstens vier indizierte Token getrennt sind.</span><span class="sxs-lookup"><span data-stu-id="bc868-p159">**Example 2.** The following expression matches strings that contain "cat", "dog", "fox", and "wolf" if no more than four indexed tokens separate them.</span></span>
  
    
    
 `near(cat, dog, fox, wolf)`
  
    
    
<span data-ttu-id="bc868-507">Die folgende Tabelle enthält Beispiele der Zeichenfolgenwerte der verwalteten Eigenschaft und gibt an, ob diese mit dem vorherigen Ausdruck in Beispiel 2 übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="bc868-507">The following table contains examples of managed property string values and states whether they match the previous expression in Example 2.</span></span>
  
    
    


|<span data-ttu-id="bc868-508">**Treffer?**</span><span class="sxs-lookup"><span data-stu-id="bc868-508">**Match?**</span></span>|<span data-ttu-id="bc868-509">**Text**</span><span class="sxs-lookup"><span data-stu-id="bc868-509">**Text**</span></span>|
|:-----|:-----|
|<span data-ttu-id="bc868-510">Ja</span><span class="sxs-lookup"><span data-stu-id="bc868-510">Yes</span></span>  <br/> |<span data-ttu-id="bc868-511">Die Abbildung zeigt eine Katze, einen Hund, einen Fuchs und einen Wolf.</span><span class="sxs-lookup"><span data-stu-id="bc868-511">The picture shows a cat, a dog, a fox, and a wolf.</span></span>  <br/> |
|<span data-ttu-id="bc868-512">Ja (mit Wortstammerkennung)</span><span class="sxs-lookup"><span data-stu-id="bc868-512">Yes (with stemming)</span></span>  <br/> |<span data-ttu-id="bc868-513">Hunde, Füchse und Wölfe sind hundeartig, Katzen hingegen sind katzenartig.</span><span class="sxs-lookup"><span data-stu-id="bc868-513">Dogs, foxes, and wolves are canines, but cats are felines.</span></span>  <br/> |
|<span data-ttu-id="bc868-514">Nein</span><span class="sxs-lookup"><span data-stu-id="bc868-514">No</span></span>  <br/> |<span data-ttu-id="bc868-515">Die Abbildung zeigt eine Katze mit einem Hund, einem Fuchs und einem Wolf.</span><span class="sxs-lookup"><span data-stu-id="bc868-515">The picture shows a cat with a dog, a fox, and a wolf.</span></span>  <br/> |
   
<span data-ttu-id="bc868-516">Der folgende Ausdruck gleicht alle Zeichenfolgen in der vorherigen Tabelle ab.</span><span class="sxs-lookup"><span data-stu-id="bc868-516">The following expression matches all the strings in the previous table.</span></span>
  
    
    
 `near(cat, dog, fox, wolf, N=5)`
  
    
    

#### <a name="remarks"></a><span data-ttu-id="bc868-517">HinwBemerkungeneise</span><span class="sxs-lookup"><span data-stu-id="bc868-517">Remarks</span></span>

 <span data-ttu-id="bc868-518">**Überlegungen zum Abstand zwischen NEAR/ONEAR-Begriffen**</span><span class="sxs-lookup"><span data-stu-id="bc868-518">**NEAR/ONEAR term distance considerations**</span></span>
  
    
    
 <span data-ttu-id="bc868-p160">_N_ gibt die maximale Anzahl der Wörter an, die zwischen den Abfragebegriffen innerhalb des übereinstimmenden Segments des Elements angezeigt werden dürfen. Wenn **NEAR** oder **ONEAR** mehr als zwei Operanden enthält, wird die maximal zulässige Anzahl der Wörter zwischen den Abfragebegriffen ( _N_) innerhalb des Segments des Elements gezählt, das mit allen **NEAR** - oder **ONEAR** -Begriffen übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="bc868-p160">_N_ indicates the maximum number of words that are allowed to appear between the query terms within the matching segment of the item. If **NEAR** or **ONEAR** includes more than two operands, the maximum number of words allowed between the query terms ( _N_) is counted within the segment of the item matching all the **NEAR** or **ONEAR** terms.</span></span>
  
    
    
 <span data-ttu-id="bc868-p161">**NEAR** oder **ONEAR** fungiert als Text mit Token. Dies bedeutet, dass Sonderzeichen wie Komma („ **,** "), Punkt („ **.** "), Doppelpunkt („ **:** ") oder Semikolon („ **;** ") als Leerzeichen behandelt werden. Der Begriff „Abstand" bezieht sich auf Token innerhalb des indizierten Texts.</span><span class="sxs-lookup"><span data-stu-id="bc868-p161">**NEAR** or **ONEAR** operates on tokenized text. This means that special characters such as comma (" **,** "), period (" **.** "), colon (" **:** "), or semicolon (" **;** ") will be treated as white space. The term "distance" relates to tokens within the indexed text.</span></span>
  
    
    
<span data-ttu-id="bc868-525">Wenn Sie **ONEAR** oder **NEAR** mit gleichen Operanden verwenden, funktioniert der Operator wie folgt:</span><span class="sxs-lookup"><span data-stu-id="bc868-525">If you use **ONEAR** or **NEAR** with equal operands, the operator will work as follows:</span></span>
  
    
    
 `near(a, a, n=x)`
  
    
    
<span data-ttu-id="bc868-p162">Diese Abfrage gibt immer **true** zurück, wenn mindestens eine Instanz des Buchstabens „ `a`"' im Kontext angezeigt wird. Dies bedeutet auch, dass **NEAR** nicht als **COUNT**-Operator verwendet werden kann. Weitere Informationen zum Zählen von Begriffsvorkommen finden Sie unter Operator  [COUNT](fast-query-language-fql-syntax-reference.md#fql_count_operator).</span><span class="sxs-lookup"><span data-stu-id="bc868-p162">This query will always return **true** if at least one instance of '' `a`'' appears within the context. This also means that **NEAR** cannot be used as a **COUNT** operator. For more information about counting term occurrences, see the [COUNT](fast-query-language-fql-syntax-reference.md#fql_count_operator) operator.</span></span>
  
    
    
 <span data-ttu-id="bc868-529">Wenn **NEAR** auf Phrasen angewendet wird, werden ebenfalls sich überlappende Phrase im Text gefunden.</span><span class="sxs-lookup"><span data-stu-id="bc868-529">**NEAR** applied to phrases will also match overlapping phrases in the text.</span></span>
  
    
    
<span data-ttu-id="bc868-p163">Wenn ein Token im übereinstimmenden Segment mehr als einen Operanden dem **NEAR** - oder dem **ONEAR** -Ausdruck zuordnet, kann die Abfrage die Elemente möglicherweise auch dann abgleichen, wenn die Anzahl der nicht übereinstimmenden Token innerhalb des übereinstimmenden Segments den Wert von _N_ im Ausdruck des **NEAR**- oder des **ONEAR**-Operators überschreitet. Bei einer Überlappung kann es sich beispielsweise um sich überlappende Phrasen handeln. Wenn die Anzahl der Treffer bei Tokenüberlappungen  `O` ist, gleicht die Abfrage Elemente ab, wenn nicht mehr als `N+O` nicht übereinstimmende Token innerhalb des übereinstimmenden Segments des Elements angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="bc868-p163">If a token in the matching segment matches more than one operand to the **NEAR** or **ONEAR** expression, the query may match even if the number of nonmatching tokens within the matching segment exceeds the value of ' _N_' in the **NEAR** or **ONEAR** operator expression. For example, an overlap can be overlapping phrases. If the number of token overlap matches is ' `O`', the query will match if not more than ' `N+O`' non-matching tokens appear within the matching segment of the item.</span></span> 
  
    
    
<span data-ttu-id="bc868-533">**NEAR or ONEAR with NOT**</span><span class="sxs-lookup"><span data-stu-id="bc868-533">**NEAR or ONEAR with NOT**</span></span>
  
    
    
<span data-ttu-id="bc868-p164">Der **NOT**-Operator kann nicht im **NEAR**- oder **ONEAR**-Operator verwendet werden. Beispiele für falsche FQL-Syntax:</span><span class="sxs-lookup"><span data-stu-id="bc868-p164">The **NOT** operator cannot be used inside the **NEAR** or **ONEAR** operator. The following is incorrect FQL syntax:</span></span>
  
    
    
 `near(audi,not(bmw),n=2)`
  
    
    

### <a name="not"></a><span data-ttu-id="bc868-536">NOT</span><span class="sxs-lookup"><span data-stu-id="bc868-536">NOT</span></span>
<span data-ttu-id="bc868-537"><a name="fql_not_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-537"><a name="fql_not_operator"> </a></span></span>

<span data-ttu-id="bc868-p165">Gibt nur Elemente zurück, die dem Operanden nicht entsprechen. Der Operand kann ein beliebiger gültiger FQL-Ausdruck sein.</span><span class="sxs-lookup"><span data-stu-id="bc868-p165">Returns only items that don't match the operand. The operand may be any valid FQL expression.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-540">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-540">Syntax</span></span>

 `not(operand)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-541">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-541">Parameters</span></span>

<span data-ttu-id="bc868-542">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="bc868-542">Not applicable.</span></span>
  
    
    

### <a name="onear"></a><span data-ttu-id="bc868-543">ONEAR</span><span class="sxs-lookup"><span data-stu-id="bc868-543">ONEAR</span></span>
<span data-ttu-id="bc868-544"><a name="fql_onear_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-544"><a name="fql_onear_operator"> </a></span></span>

<span data-ttu-id="bc868-p166">Die sortierte Variante von **NEAR**, die eine sortierte Zuordnung der Begriffe erfordert. The Operator **ONEAR** kann verwendet werden, um die Ergebnismenge auf Elemente mit _N_-Begriffen zu beschränken, die sich in einem bestimmten Abstand voneinander befinden.</span><span class="sxs-lookup"><span data-stu-id="bc868-p166">The ordered variant of **NEAR**, and requires an ordered match of the terms. The **ONEAR** operator can be used to restrict the result set to items that have _N_ terms within a certain distance of one another.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-547">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-547">Syntax</span></span>

 `onear(arg, arg [, arg]* [, N=<numeric value>])`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-548">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-548">Parameters</span></span>



|<span data-ttu-id="bc868-549">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="bc868-549">**Parameter**</span></span>|<span data-ttu-id="bc868-550">**Wert**</span><span class="sxs-lookup"><span data-stu-id="bc868-550">**Value**</span></span>|<span data-ttu-id="bc868-551">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="bc868-551">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="bc868-552">_N_</span><span class="sxs-lookup"><span data-stu-id="bc868-552">_N_</span></span> <br/> | <span data-ttu-id="bc868-553">_\<numeric_value\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-553">_\<numeric_value\>_</span></span> <br/> |<span data-ttu-id="bc868-554">Gibt die maximale Anzahl von Wörtern an, die zwischen den Begriffen angezeigt werden darf (explizite Nähe).</span><span class="sxs-lookup"><span data-stu-id="bc868-554">Specifies the maximum number of words that are allowed to appear between the terms (explicit proximity).</span></span>  <br/> <span data-ttu-id="bc868-555">Wenn **ONEAR** mehr als zwei Operanden enthält, wird die maximale Anzahl der zwischen den Begriffen zulässigen Wörter ( _N_) innerhalb des ganzen Ausdrucks gezählt.</span><span class="sxs-lookup"><span data-stu-id="bc868-555">If **ONEAR** includes more than two operands, the maximum number of words allowed between the terms ( _N_) is counted within the whole expression.</span></span>  <br/> <span data-ttu-id="bc868-556">Standardwert: **4**</span><span class="sxs-lookup"><span data-stu-id="bc868-556">Default: **4**</span></span> <br/> |
   

#### <a name="examples"></a><span data-ttu-id="bc868-557">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-557">Examples</span></span>

 <span data-ttu-id="bc868-p167">**Beispiel 1**: Der folgende Ausdruck gleicht alle Vorkommen der Wörter „Katze", „Hund", „Fuchs" und „Wolf" ab, die nacheinander angezeigt werden, wenn diese durch maximal vier indizierte Token getrennt sind.</span><span class="sxs-lookup"><span data-stu-id="bc868-p167">**Example 1.** The following expression matches all the occurrences of the words "cat", "dog", "fox", and "wolf" that appears in order, if no more than four indexed tokens separate them.</span></span>
  
    
    
 `onear(cat, dog, fox, wolf)`
  
    
    
<span data-ttu-id="bc868-560">Die folgende Tabelle enthält Beispiele der Zeichenfolgenwerte der verwalteten Eigenschaft und gibt an, ob diese mit dem vorherigen Ausdruck in Beispiel 2 übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="bc868-560">The following table contains examples of managed property string values, and states whether they match the previous expression.</span></span>
  
    
    


|<span data-ttu-id="bc868-561">**Treffer?**</span><span class="sxs-lookup"><span data-stu-id="bc868-561">**Match?**</span></span>|<span data-ttu-id="bc868-562">**Text**</span><span class="sxs-lookup"><span data-stu-id="bc868-562">**Text**</span></span>|
|:-----|:-----|
|<span data-ttu-id="bc868-563">Ja</span><span class="sxs-lookup"><span data-stu-id="bc868-563">Yes</span></span>  <br/> |<span data-ttu-id="bc868-564">Die Abbildung zeigt eine Katze, einen Hund, einen Fuchs und einen Wolf.</span><span class="sxs-lookup"><span data-stu-id="bc868-564">The picture shows a cat, a dog, a fox, and a wolf.</span></span>  <br/> |
|<span data-ttu-id="bc868-565">Nein</span><span class="sxs-lookup"><span data-stu-id="bc868-565">No</span></span>  <br/> |<span data-ttu-id="bc868-566">Hunde, Füchse und Wölfe sind hundeartig, Katzen hingegen sind katzenartig.</span><span class="sxs-lookup"><span data-stu-id="bc868-566">Dogs, foxes, and wolves are canines, but cats are felines.</span></span>  <br/> |
|<span data-ttu-id="bc868-567">Nein</span><span class="sxs-lookup"><span data-stu-id="bc868-567">No</span></span>  <br/> |<span data-ttu-id="bc868-568">Die Abbildung zeigt eine Katze mit einem Hund, einem Fuchs und einem Wolf.</span><span class="sxs-lookup"><span data-stu-id="bc868-568">The picture shows a cat with a dog, a fox, and a wolf.</span></span>  <br/> |
   
 <span data-ttu-id="bc868-p168">**Beispiel 2**: Der folgende Ausdruck (mit Wortstammerkennung) gleicht den Text in der zweiten Zeile der vorherigen Tabelle ab.</span><span class="sxs-lookup"><span data-stu-id="bc868-p168">**Example 2.** The following expression matches (with stemming) the text in the second row of the previous table.</span></span>
  
    
    
 `onear(dog, fox, wolf, cat, N=5)`
  
    
    
 <span data-ttu-id="bc868-p169">**Beispiel 3**: Der folgende Ausdruck gleicht den Text in der ersten und dritten Zeile der vorherigen Tabelle ab.</span><span class="sxs-lookup"><span data-stu-id="bc868-p169">**Example 3.** The following expression matches the text in the first and third rows of the preceding table.</span></span>
  
    
    
 `onear(cat, dog, fox, wolf, N=5)`
  
    
    

#### <a name="remarks"></a><span data-ttu-id="bc868-573">HinwBemerkungeneise</span><span class="sxs-lookup"><span data-stu-id="bc868-573">Remarks</span></span>

<span data-ttu-id="bc868-574">Siehe auch  [NEAR](fast-query-language-fql-syntax-reference.md#fql_near_operator).</span><span class="sxs-lookup"><span data-stu-id="bc868-574">See also  [NEAR](fast-query-language-fql-syntax-reference.md#fql_near_operator).</span></span>
  
    
    

### <a name="or"></a><span data-ttu-id="bc868-575">ODER</span><span class="sxs-lookup"><span data-stu-id="bc868-575">OR</span></span>
<span data-ttu-id="bc868-576"><a name="fql_or_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-576"><a name="fql_or_operator"> </a></span></span>

<span data-ttu-id="bc868-p170">Gibt nur Elemente zurück, die mindestens einem der **OR** -Operanden entsprechen. Übereinstimmende Elemente werden in der dynamischen Rangfolge (Relevanzbewertung in der Ergebnismenge) weiter oben angegeben, wenn mehrere der **OR** -Operanden übereinstimmen. Bei den Operanden kann es sich um einen einzelnen Begriff oder einen beliebigen gültigen FQL-Unterausdruck handeln.</span><span class="sxs-lookup"><span data-stu-id="bc868-p170">Returns only items that match at least one of the **OR** operands. Items that match will get a higher dynamic rank (relevance score in the result set) if more of the **OR** operands match. The operands may be a single term or any valid FQL sub-expression.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-580">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-580">Syntax</span></span>

 `or(operand, operand [,operand]*)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-581">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-581">Parameters</span></span>

<span data-ttu-id="bc868-582">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="bc868-582">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="bc868-583">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-583">Examples</span></span>

<span data-ttu-id="bc868-p171">Der folgende Ausdruck gleicht alle Elemente ab, bei denen der Standard-Volltextindex entweder „Katze" oder „Hund" enthält. Wenn der Standard-Volltextindex eines Elements sowohl den Begriff „Katze" als auch den Begriff „Hund" enthält, wird das Element abgeglichen und erhält eine höhere dynamische Bewertung als der Fall wäre, wenn das Element nur eines der Token enthielte.</span><span class="sxs-lookup"><span data-stu-id="bc868-p171">The following expression matches all the items for which the default full-text index contains either "cat" or "dog". If an item's default full-text index contains both "cat" and "dog", it will match and have a higher dynamic rank than it would if it contained only one of the tokens.</span></span>
  
    
    
 `or(cat, dog)`
  
    
    

### <a name="phrase"></a><span data-ttu-id="bc868-586">PHRASE</span><span class="sxs-lookup"><span data-stu-id="bc868-586">PHRASE</span></span>
<span data-ttu-id="bc868-587"><a name="fql_phrase_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-587"><a name="fql_phrase_operator"> </a></span></span>

<span data-ttu-id="bc868-588">Sucht nach einer exakten Tokenzeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="bc868-588">Searches for an exact string of tokens.</span></span> 
  
    
    
<span data-ttu-id="bc868-p172">Die **PHRASE** -Operanden können einzelne Begriffe sein. Platzhalter werden akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="bc868-p172">The **PHRASE** operands can be single terms. Wildcards are accepted.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-591">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-591">Syntax</span></span>

 `phrase(term [, term]*)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-592">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-592">Parameters</span></span>

<span data-ttu-id="bc868-593">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="bc868-593">Not applicable.</span></span>
  
    
    

#### <a name="remarks"></a><span data-ttu-id="bc868-594">HinwBemerkungeneise</span><span class="sxs-lookup"><span data-stu-id="bc868-594">Remarks</span></span>

<span data-ttu-id="bc868-595">Siehe auch  [STRING](fast-query-language-fql-syntax-reference.md#fql_string_operator).</span><span class="sxs-lookup"><span data-stu-id="bc868-595">See also  [STRING](fast-query-language-fql-syntax-reference.md#fql_string_operator).</span></span>
  
    
    

### <a name="range"></a><span data-ttu-id="bc868-596">RANGE</span><span class="sxs-lookup"><span data-stu-id="bc868-596">RANGE</span></span>
<span data-ttu-id="bc868-597"><a name="fql_range_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-597"><a name="fql_range_operator"> </a></span></span>

<span data-ttu-id="bc868-p173">Verwenden Sie den Operator **RANGE** für numerische verwaltete Eigenschaften und verwaltete Eigenschaften für Datum/Uhrzeit.</span><span class="sxs-lookup"><span data-stu-id="bc868-p173">Use the **RANGE** operator for numeric and date/time managed properties. The operator enables range matching expressions.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-600">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-600">Syntax</span></span>

 `range(start, stop [,from="GE"|"GT"] [,to="LE"|"LT"])`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-601">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-601">Parameters</span></span>



|<span data-ttu-id="bc868-602">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="bc868-602">**Parameter**</span></span>|<span data-ttu-id="bc868-603">**Wert**</span><span class="sxs-lookup"><span data-stu-id="bc868-603">**Value**</span></span>|<span data-ttu-id="bc868-604">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="bc868-604">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="bc868-605">_start_</span><span class="sxs-lookup"><span data-stu-id="bc868-605">_start_</span></span> <br/> | <span data-ttu-id="bc868-606">_\<numeric_value\>\\</span><span class="sxs-lookup"><span data-stu-id="bc868-606">_\<numeric_value\>\\</span></span>|<span data-ttu-id="bc868-607">\<date/time_value\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-607">\<date/time_value\>_</span></span> <br/> |<span data-ttu-id="bc868-608">Startwert für den Bereich.</span><span class="sxs-lookup"><span data-stu-id="bc868-608">Start value for the range.</span></span>  <br/> <span data-ttu-id="bc868-609">Verwenden Sie das reservierte Wort **min**, um anzugeben, dass der Bereich keine untere Grenze hat.</span><span class="sxs-lookup"><span data-stu-id="bc868-609">To specify that the range has no lower bound, use the reserved word **min**.</span></span> <br/> |
| <span data-ttu-id="bc868-610">_stop_</span><span class="sxs-lookup"><span data-stu-id="bc868-610">_stop_</span></span> <br/> | <span data-ttu-id="bc868-611">_\<numeric_value\>\\</span><span class="sxs-lookup"><span data-stu-id="bc868-611">_\<numeric_value\>\\</span></span>|<span data-ttu-id="bc868-612">\<date/time_value\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-612">\<date/time_value\>_</span></span> <br/> |<span data-ttu-id="bc868-613">Endwert für den Bereich.</span><span class="sxs-lookup"><span data-stu-id="bc868-613">End value for the range.</span></span>  <br/> <span data-ttu-id="bc868-614">Verwenden Sie das reservierte Wort **max**, um anzugeben, dass der Bereich keine obere Grenze hat.</span><span class="sxs-lookup"><span data-stu-id="bc868-614">To specify that the range has no upper bound, use the reserved word **max**.</span></span> <br/> |
| <span data-ttu-id="bc868-615">_from_</span><span class="sxs-lookup"><span data-stu-id="bc868-615">_from_</span></span> <br/> |<span data-ttu-id="bc868-616">**GE\\</span><span class="sxs-lookup"><span data-stu-id="bc868-616">**GE\\</span></span>|<span data-ttu-id="bc868-617">GT**</span><span class="sxs-lookup"><span data-stu-id="bc868-617">GT**</span></span> <br/> | <span data-ttu-id="bc868-618">Optionaler Parameter, der das öffnende oder schließende Startintervall angibt.</span><span class="sxs-lookup"><span data-stu-id="bc868-618">Optional parameter that indicates the open or close start interval.</span></span> <br/>  <span data-ttu-id="bc868-619">Gültige Werte:</span><span class="sxs-lookup"><span data-stu-id="bc868-619">Valid values:</span></span> <br/><ul><li> <span data-ttu-id="bc868-620">**GE** Größer als oder gleich dem Startwert (>= Start des Intervalls)</span><span class="sxs-lookup"><span data-stu-id="bc868-620">**GE** Greater than or equal to the start value (>= start of interval).</span></span> </li><li> <span data-ttu-id="bc868-621">**GT** Größer als der Startwert (> Start des Intervalls)</span><span class="sxs-lookup"><span data-stu-id="bc868-621">**GT** Greater than the start value (> start of interval).</span></span> </li></ul>  <span data-ttu-id="bc868-622">Standardwert: **GE**</span><span class="sxs-lookup"><span data-stu-id="bc868-622">Default: **GE**</span></span>  |
| <span data-ttu-id="bc868-623">_to_</span><span class="sxs-lookup"><span data-stu-id="bc868-623">_to_</span></span> <br/> |<span data-ttu-id="bc868-624">**LE\\</span><span class="sxs-lookup"><span data-stu-id="bc868-624">**LE\\</span></span>|<span data-ttu-id="bc868-625">LT**</span><span class="sxs-lookup"><span data-stu-id="bc868-625">LT**</span></span> <br/> | <span data-ttu-id="bc868-626">Optionaler Parameter, der das öffnende oder schließende Endintervall angibt</span><span class="sxs-lookup"><span data-stu-id="bc868-626">Optional parameter that indicates the open or close end interval.</span></span> <br/>  <span data-ttu-id="bc868-627">Gültige Werte:</span><span class="sxs-lookup"><span data-stu-id="bc868-627">Valid values:</span></span> <br/><ul><li> <span data-ttu-id="bc868-628">**LE** Kleiner oder gleich dem Endwert (<= Ende des Intervalls)</span><span class="sxs-lookup"><span data-stu-id="bc868-628">**LE** Less than or equal to the end value (<= end of interval).</span></span> </li><li> <span data-ttu-id="bc868-629">**LT** Kleiner als der Endwert (< Ende des Intervalls)</span><span class="sxs-lookup"><span data-stu-id="bc868-629">**LT** Less than the end value (< end of interval).</span></span> </li></ul>  <span data-ttu-id="bc868-630">Standardwert: **LT**</span><span class="sxs-lookup"><span data-stu-id="bc868-630">Default: **LT**</span></span> |
   

#### <a name="examples"></a><span data-ttu-id="bc868-631">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-631">Examples</span></span>

<span data-ttu-id="bc868-632">Der folgende Ausdruck gleicht eine Beschreibungseigenschaft ab, die mit der Phrase „Olympische Spiele" beginnt, die in Elementen mit einer Größe von mindestens 10.000 Byte angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="bc868-632">The following expression matches a description property starting with the phrase "olympic games" appearing in items with a size of at least 10 000 bytes.</span></span>
  
    
    
 `and(size:range(10000, max), description:starts-with("olympic games"))`
  
    
    

### <a name="starts-with"></a><span data-ttu-id="bc868-633">STARTS-WITH</span><span class="sxs-lookup"><span data-stu-id="bc868-633">STARTS-WITH</span></span>
<span data-ttu-id="bc868-634"><a name="fql_startswith_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-634"><a name="fql_startswith_operator"> </a></span></span>

<span data-ttu-id="bc868-635">Gibt ein Wort oder eine Phrase an, die am Anfang einer verwalteten Eigenschaft angezeigt werden muss.</span><span class="sxs-lookup"><span data-stu-id="bc868-635">Specifies a word or phrase that must appear at the start of a managed property.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-636">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-636">Syntax</span></span>

 `starts-with(<term or phrase>)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-637">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-637">Parameters</span></span>

<span data-ttu-id="bc868-638">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="bc868-638">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="bc868-639">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-639">Examples</span></span>

<span data-ttu-id="bc868-p174">Der folgende Ausdruck gleicht Elemente mit den Werten „Mr. Adam Jones" und „Adam Jones" in der verwalteten **author**-Eigenschaft ab. Er gleicht keine Elemente mit dem Wert „Herr Adam Jones" ab.</span><span class="sxs-lookup"><span data-stu-id="bc868-p174">The following expression will match items with the values "Adam Jones sr" and "Adam Jones" in the **author** managed property. It will not match items with the value "Mr Adam Jones".</span></span>
  
    
    
 `author:starts-with("adam jones")`
  
    
    

#### <a name="remarks"></a><span data-ttu-id="bc868-642">HinwBemerkungeneise</span><span class="sxs-lookup"><span data-stu-id="bc868-642">Remarks</span></span>

<span data-ttu-id="bc868-643">Weitere Informationen zum Begrenzungsabgleich finden Sie unter  [ENDS-WITH](fast-query-language-fql-syntax-reference.md#fql_endswith_operator).</span><span class="sxs-lookup"><span data-stu-id="bc868-643">For additional remarks on boundary matching, see  [ENDS-WITH](fast-query-language-fql-syntax-reference.md#fql_endswith_operator).</span></span>
  
    
    

### <a name="string"></a><span data-ttu-id="bc868-644">STRING</span><span class="sxs-lookup"><span data-stu-id="bc868-644">STRING</span></span>
<span data-ttu-id="bc868-645"><a name="fql_string_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-645"><a name="fql_string_operator"> </a></span></span>

<span data-ttu-id="bc868-646">Definiert eine boolesche Abgleichbedingung für eine Textzeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="bc868-646">Defines a Boolean matching condition to a text string.</span></span>
  
    
    
<span data-ttu-id="bc868-p175">Der Operand ist eine Textzeichenfolge (ein oder mehrere Begriffe), die abgeglichen werden soll. Auf die Zeichenfolge folgt der Wert null, oder es folgen mehrere Parameter.</span><span class="sxs-lookup"><span data-stu-id="bc868-p175">The operand is a text string (one or more terms) that is to be matched. The string is followed by zero or more parameters.</span></span> 
  
    
    
<span data-ttu-id="bc868-p176">Der Parameter **STRING** kann auch als Typumwandlung verwendet werden. Die Abfrage `string("24.5")` beispielsweise behandelt den numerischen Wert „24.5" als Textzeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="bc868-p176">The **STRING** operator can also be used as a type conversion. The query `string("24.5")`, for example, will treat the numeric value "24.5" as a text string.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="bc868-651">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-651">Syntax</span></span>

 `string("<text string>"`
  
    
    
 ` [, mode=<mode>]`
  
    
    
 ` [, n=<near>]`
  
    
    
 ` [, weight=<n>]`
  
    
    
 ` [, linguistics=<on|off>]`
  
    
    
 ` [, wildcard=<on|off>])`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-652">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-652">Parameters</span></span>



|<span data-ttu-id="bc868-653">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="bc868-653">**Parameter**</span></span>|<span data-ttu-id="bc868-654">**Wert**</span><span class="sxs-lookup"><span data-stu-id="bc868-654">**Value**</span></span>|<span data-ttu-id="bc868-655">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="bc868-655">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="bc868-656">_mode_</span><span class="sxs-lookup"><span data-stu-id="bc868-656">_mode_</span></span> <br/> | <span data-ttu-id="bc868-657">_\<mode\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-657">_\<mode\>_</span></span> <br/> | <span data-ttu-id="bc868-658">Der Parameter _mode_ gibt an, wie der Wert \<text string\> ausgewertet werden soll.</span><span class="sxs-lookup"><span data-stu-id="bc868-658">The _mode_ parameter specifies how to evaluate the \<text string\> value.</span></span> <span data-ttu-id="bc868-659">Die folgende Liste enthält gültige Werte.</span><span class="sxs-lookup"><span data-stu-id="bc868-659">The following list shows valid values.</span></span> <br/> <span data-ttu-id="bc868-660">**"PHRASE"** - `phrase(term [,term]*)`</span><span class="sxs-lookup"><span data-stu-id="bc868-660">**"PHRASE"** - `phrase(term [,term]*)`</span></span> <br/> <table><tr><th><span data-ttu-id="bc868-661">**Mode**</span><span class="sxs-lookup"><span data-stu-id="bc868-661">**Mode**</span></span></th><th><span data-ttu-id="bc868-662">**Entsprechender Operatorausdruck**</span><span class="sxs-lookup"><span data-stu-id="bc868-662">**Equivalent operator expression**</span></span></th></tr><tr><td><span data-ttu-id="bc868-663">**"PHRASE"**</span><span class="sxs-lookup"><span data-stu-id="bc868-663">**"PHRASE"**</span></span>  </td><td> `phrase(term [,term]*)` </td></tr><tr><td><span data-ttu-id="bc868-664">**"AND"**</span><span class="sxs-lookup"><span data-stu-id="bc868-664">**"AND"**</span></span> </td><td> `and(term, term [,term]*)` </td></tr><tr><td><span data-ttu-id="bc868-665">**"OR"**</span><span class="sxs-lookup"><span data-stu-id="bc868-665">**"OR"**</span></span> </td><td> `or(term, term [,term]*)` </td></tr><tr><td><span data-ttu-id="bc868-666">**"ANY"**</span><span class="sxs-lookup"><span data-stu-id="bc868-666">**"ANY"**</span></span> </td><td> `any(term, term [,term]*)` </td></tr><tr><td><span data-ttu-id="bc868-667">**"NEAR"**</span><span class="sxs-lookup"><span data-stu-id="bc868-667">**"NEAR"**</span></span> </td><td> `near(term, term [,term]*, N)` </td></tr><tr><td><span data-ttu-id="bc868-668">**"ONEAR"**</span><span class="sxs-lookup"><span data-stu-id="bc868-668">**"ONEAR"**</span></span> </td><td> `onear(term, term [,term]*, N)` </td></tr></table><br/><span data-ttu-id="bc868-669">Standard: **"PHRASE"**</span><span class="sxs-lookup"><span data-stu-id="bc868-669">Default: **"PHRASE"**</span></span> |
| _n_ <br/> | <span data-ttu-id="bc868-670">_\<numeric_value\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-670">_\<numeric_value\>_</span></span> <br/> |<span data-ttu-id="bc868-671">Dieser Parameter gibt den maximalen Abstand eines Begriffs für  _mode_= **"NEAR"** oder _mode_= **"ONEAR"** an.</span><span class="sxs-lookup"><span data-stu-id="bc868-671">This parameter indicates the maximum term distance for  _mode_= **"NEAR"** or _mode_= **"ONEAR"**.</span></span> <br/> <span data-ttu-id="bc868-672">Die folgenden Ausdrücke sind gleichwertig:</span><span class="sxs-lookup"><span data-stu-id="bc868-672">The following expressions are equivalent:</span></span>  <br/>  `string("hello world", mode="NEAR", n=5)` <br/>  `near(hello, world, n=5)` <br/> <span data-ttu-id="bc868-673">Standard: **4**</span><span class="sxs-lookup"><span data-stu-id="bc868-673">Default: **4**</span></span> <br/> |
| <span data-ttu-id="bc868-674">_weight_</span><span class="sxs-lookup"><span data-stu-id="bc868-674">_weight_</span></span> <br/> | <span data-ttu-id="bc868-675">_\<numeric_value\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-675">_\<numeric_value\>_</span></span> <br/> |<span data-ttu-id="bc868-676">Dieser Parameter ist ein positiver numerischer Wert, der die Begriffsgewichtung für die dynamische Rangfolge angibt.</span><span class="sxs-lookup"><span data-stu-id="bc868-676">This parameter is a positive numeric value indicating term weight for dynamic ranking.</span></span>  <br/> <span data-ttu-id="bc868-p178">Ein niedrigerer Wert gibt an, dass ein Begriff in der dynamischen Rangfolge weniger relevant ist. Ein höherer Wert gibt an, dass ein Begriff in der Rangfolge relevanter ist. Der Wert null für den gewichteten Parameter gibt an, dass ein Begriff für die dynamische Rangfolge nicht relevant ist.</span><span class="sxs-lookup"><span data-stu-id="bc868-p178">A lower value indicates that a term should contribute less to the ranking. A higher value indicates that a term should contribute more to the ranking. A value of zero for the weight parameter specifies that a term should not affect dynamic rank.  </span></span><br/> <span data-ttu-id="bc868-680">Der Parameter _weight_ gilt für alle Begriffe im **STRING**-Ausdruck.</span><span class="sxs-lookup"><span data-stu-id="bc868-680">The  _weight_ parameter applies to all the terms in the **STRING** expression.</span></span> <br/> <span data-ttu-id="bc868-681">**TIPP:** Der weight-Parameter ist nur für Volltextindex-Abfragen relevant.</span><span class="sxs-lookup"><span data-stu-id="bc868-681">**TIP:** The weight parameter will affect only full-text index queries.</span></span>           <span data-ttu-id="bc868-682">Standard: **100**.</span><span class="sxs-lookup"><span data-stu-id="bc868-682">Default: **100**.</span></span> <br/> |
| <span data-ttu-id="bc868-683">_linguistics_</span><span class="sxs-lookup"><span data-stu-id="bc868-683">_linguistics_</span></span> <br/> |<span data-ttu-id="bc868-684">**on\\</span><span class="sxs-lookup"><span data-stu-id="bc868-684">**on\\</span></span>|<span data-ttu-id="bc868-685">off**</span><span class="sxs-lookup"><span data-stu-id="bc868-685">off**</span></span> <br/> |<span data-ttu-id="bc868-686">Deaktiviert/Aktiviert alle Linguistik-Features für die Zeichenfolge (Lemmatisierung, Synonyme, Rechtschreibprüfung), wenn sie für die Abfrage aktiviert wurden.</span><span class="sxs-lookup"><span data-stu-id="bc868-686">Disables/enables all linguistics features for the string (lemmatization, synonyms, spelling checking) if they are enabled for the query.</span></span>  <br/> <span data-ttu-id="bc868-687">Mit diesem Parameter können Sie die linguistische Verarbeitung für einen bestimmten Begriff oder eine bestimmte Zeichenfolge ändern, während der Begriff oder die Zeichenfolge weiterhin für die Rangfolge relevant sein soll.</span><span class="sxs-lookup"><span data-stu-id="bc868-687">You can use this parameter to switch off linguistic processing for a given term or string while you still want the term or string to contribute to ranking.</span></span>  <br/> <span data-ttu-id="bc868-688">Standard: **"ON"**</span><span class="sxs-lookup"><span data-stu-id="bc868-688">Default: **"ON"**</span></span> <br/> |
| <span data-ttu-id="bc868-689">_wildcard_</span><span class="sxs-lookup"><span data-stu-id="bc868-689">_wildcard_</span></span> <br/> |<span data-ttu-id="bc868-690">**on\\</span><span class="sxs-lookup"><span data-stu-id="bc868-690">**on\\</span></span>|<span data-ttu-id="bc868-691">off**</span><span class="sxs-lookup"><span data-stu-id="bc868-691">off**</span></span> <br/> | <span data-ttu-id="bc868-692">Dieser Parameter steuert die Platzhaltererweiterung von Begriffen innerhalb der _\<Textzeichenfolge\>_.</span><span class="sxs-lookup"><span data-stu-id="bc868-692">This parameter controls wildcard expansion of terms inside the _\<text string\>_.</span></span> <span data-ttu-id="bc868-693">Diese Einstellung setzt alle Platzhaltereinstellungen in Abfrageparametern außer Kraft und ermöglicht die Aktivierung oder Deaktivierung von erweiterten Platzhalterzeichen für bestimmte Teile der Abfrage.  </span><span class="sxs-lookup"><span data-stu-id="bc868-693">This setting overrides any wildcard settings in query parameters, and allows extended wildcard characters to be enabled or disabled on specific parts of the query.</span></span>  <br/>  <span data-ttu-id="bc868-694">Die folgenden Werte sind gültig:</span><span class="sxs-lookup"><span data-stu-id="bc868-694">The following are valid values:</span></span> <br/><ul><li> <span data-ttu-id="bc868-695">**"ON"**  Gibt an, dass das Zeichen "\\*" als Platzhalter ausgewertet wird.</span><span class="sxs-lookup"><span data-stu-id="bc868-695">**"ON"** Specifies that the character "\\*" is evaluated as wildcard.</span></span> <span data-ttu-id="bc868-696">Ein "\\*"-Zeichen entspricht null oder mehr Zeichen.</span><span class="sxs-lookup"><span data-stu-id="bc868-696">A "\\*" character matches zero or more characters.</span></span>  </li><li> <span data-ttu-id="bc868-697"> *\*"OFF"**  Gibt an, dass das Zeichen "\\*" nicht als Platzhalter ausgewertet wird.</span><span class="sxs-lookup"><span data-stu-id="bc868-697">**"OFF"** Specifies that the characters "\\*" is not evaluated as wildcard.</span></span>  </li></ul>  <span data-ttu-id="bc868-698">Standard: **"ON"**</span><span class="sxs-lookup"><span data-stu-id="bc868-698">Default: **"ON"**</span></span> <br/> |
   
> [!NOTE]
> <span data-ttu-id="bc868-699">In SharePoint gelten die Parameter _minexpansion_,  _maxexpansion_ und _annotation_class_ für den Operator **STRING** als veraltet.</span><span class="sxs-lookup"><span data-stu-id="bc868-699">_Note:_ In SharePoint the  _minexpansion_,  _maxexpansion_ and **annotation_class** parameters for the STRING operator are obsolete.</span></span>
  
    
    


#### <a name="examples"></a><span data-ttu-id="bc868-700">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-700">Examples</span></span>

 <span data-ttu-id="bc868-p182">**Beispiel 1**: Da der standardmäßige Zeichenfolgemodus **PHRASE** ist, gibt jeder der folgenden Ausdrücke die gleichen Ergebnisse zurück.</span><span class="sxs-lookup"><span data-stu-id="bc868-p182">**Example 1.** Because the default string mode is " **PHRASE** ", each of the following expressions returns the same results.</span></span>
  
    
    
 `"what light through yonder window breaks"string("what light through yonder window breaks")string("what light through yonder window breaks", mode="phrase")phrase(what, light, through, yonder, window, breaks)`
  
    
    
 <span data-ttu-id="bc868-p183">**Beispiel 2**: Der folgende Zeichenfolge-Tokenausdruck und der **AND** -Operatorausdruck geben die gleichen Ergebnisse zurück.</span><span class="sxs-lookup"><span data-stu-id="bc868-p183">**Example 2.** The following string token expression and the **AND** operator expression return the same results.</span></span>
  
    
    
 `string("cat dog fox", mode="and")and(cat, dog, fox)`
  
    
    
 <span data-ttu-id="bc868-p184">**Beispiel 3**: Der folgende Zeichenfolge-Tokenausdruck und der **OR** -Operatorausdruck geben die gleichen Ergebnisse zurück.</span><span class="sxs-lookup"><span data-stu-id="bc868-p184">**Example 3.** The following string token expression and **OR** operator expression return the same results.</span></span>
  
    
    
 `string("coyote saguaro", mode="or")or(coyote, saguaro)`
  
    
    
 <span data-ttu-id="bc868-p185">**Beispiel 4**: Der folgende Zeichenfolge-Tokenausdruck und der **ANY** -Operatorausdruck geben die gleichen Ergebnisse zurück.</span><span class="sxs-lookup"><span data-stu-id="bc868-p185">**Example 4.** The following string token expression and **ANY** operator expression return the same results.</span></span>
  
    
    
 `string("coyote saguaro", mode="any")any(coyote, saguaro)`
  
    
    
 <span data-ttu-id="bc868-p186">**Beispiel 5**: Der folgende Zeichenfolge-Tokenausdruck und der **NEAR** -Operatorausdruck geben die gleichen Ergebnisse zurück.</span><span class="sxs-lookup"><span data-stu-id="bc868-p186">**Example 5.** The following string token expression and **NEAR** operator expression return the same results.</span></span>
  
    
    
 `string("coyote saguaro", mode="near")near(coyote, saguaro)`
  
    
    
 <span data-ttu-id="bc868-p187">**Beispiel 6**: Der folgende Zeichenfolge-Tokenausdruck und der **NEAR** -Operatorausdruck geben die gleichen Ergebnisse zurück.</span><span class="sxs-lookup"><span data-stu-id="bc868-p187">**Example 6.** The following string token expression and **NEAR** operator expression return the same results.</span></span>
  
    
    
 `string("cat dog fox wolf", mode="near", N=4)near(cat, dog, fox, wolf, N=4)`
  
    
    
 <span data-ttu-id="bc868-p188">**Beispiel 7**: Der folgende Zeichenfolge-Tokenausdruck und der **ONEAR** -Operatorausdruck geben die gleichen Ergebnisse zurück.</span><span class="sxs-lookup"><span data-stu-id="bc868-p188">**Example 7.** The following string token expression and **ONEAR** operator expression return the same results.</span></span>
  
    
    
 `string("cat dog fox wolf", mode="onear")onear(cat, dog, fox, wolf)`
  
    
    
 <span data-ttu-id="bc868-p189">**Beispiel 8**: Der folgende Zeichenfolge-Tokenausdruck gleicht das Wort „Adel" mit deaktivierten linguistischen Features ab, sodass andere Wortformen (zum Beispiel „adelnd") nicht über die Wortstammerkennung abgeglichen werden.</span><span class="sxs-lookup"><span data-stu-id="bc868-p189">**Example 8.** The following string token expression matches the word "nobler" with linguistic features disabled, so other forms of the word (such as "ennobling") are not matched by using stemming.</span></span>
  
    
    
 `string("nobler", linguistics="off")`
  
    
    
 <span data-ttu-id="bc868-p190">**Beispiel 9**: Der folgende Ausdruck gleicht Elemente ab, die entweder „Katze" oder „Hund" enthalten. Der Ausdruck erhöht jedoch die Position der Elemente, die den Begriff „Hund" enthalten, in der dynamischen Rangfolge stärker, als die von Elementen, die „Katze" enthalten.</span><span class="sxs-lookup"><span data-stu-id="bc868-p190">**Example 9.** The following expression matches items that contain either "cat" or "dog ", but the expression increases the dynamic rank of items that contain "dog" more than items that contain "cat".</span></span>
  
    
    
 `or(string("cat", weight="200"), string("dog", weight="500"))`
  
    
    

#### <a name="remarks"></a><span data-ttu-id="bc868-719">HinwBemerkungeneise</span><span class="sxs-lookup"><span data-stu-id="bc868-719">Remarks</span></span>

 <span data-ttu-id="bc868-720">**Relevanzgewichtung für die dynamische Rangfolge**</span><span class="sxs-lookup"><span data-stu-id="bc868-720">**Relevance weight for dynamic ranking**</span></span>
  
    
    
<span data-ttu-id="bc868-p191">Die Hauptauswirkung des Parameters **weight** betrifft **OR** -Abfragen. Er kann zudem eine gewisse Auswirkung auf **AND** -Abfragen haben. Der Algorithmus der dynamischen Rangfolge kann implizieren, dass verschiedene Begriffe eine unterschiedliche Relevanz in der Rangfolge haben, je nachdem, wo in dem Element die Begriffsübereinstimmung auftritt.</span><span class="sxs-lookup"><span data-stu-id="bc868-p191">The main effect of the **weight** parameter is for **OR** queries. It can also have some effect on **AND** queries. The dynamic rank algorithm can imply that different terms give different rank contribution depending on where in the item the term match occurs.</span></span>
  
    
    
<span data-ttu-id="bc868-p192">Dem Unterschied bei der Relevanz in der Rangfolge kann auch die Häufigkeit des Begriffs und die inverse Häufigkeit des Begriffs zugrunde liegen. Bei den folgenden Angaben handelt es sich um ein Beispiel:</span><span class="sxs-lookup"><span data-stu-id="bc868-p192">The difference in rank contribution can also be based on term frequency and inverse item frequency. The following is an example:</span></span>
  
    
    

- <span data-ttu-id="bc868-726">Abfrage:  `and(string("a"), string("b", weight=200))`</span><span class="sxs-lookup"><span data-stu-id="bc868-726">Query:  `and(string("a"), string("b", weight=200))`</span></span>
    
  
- <span data-ttu-id="bc868-727">Indexschema: Die verwaltete **title** -Eigenschaft hat eine höhere Gewichtung als die verwaltete **body** -Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="bc868-727">Index schema: The **title** managed property has more weight than the **body** managed property.</span></span>
    
  
- <span data-ttu-id="bc868-728">Das Indexelement 1 enthält den Begriff „a" im Titel (title) und den Begriff „b" im Textkörper (body).</span><span class="sxs-lookup"><span data-stu-id="bc868-728">Index item 1 includes term 'a' in the title and term 'b' in the body.</span></span> 
    
  
- <span data-ttu-id="bc868-729">Das Indexelement 2 enthält den Begriff „a" im Textkörper (body) und den Begriff „b" im Titel (title).</span><span class="sxs-lookup"><span data-stu-id="bc868-729">Index item 2 includes term 'a' in the body and term 'b' in the title.</span></span> 
    
  
<span data-ttu-id="bc868-730">In diesem Beispiel erhält Element 2 die höchste Position in der Rangfolge, da die Elemente mit höherer Relevanz in der Rangfolge eine größere Verstärkung erhalten.</span><span class="sxs-lookup"><span data-stu-id="bc868-730">In this example, item 2 will get the highest total rank, as the items with higher dynamic rank contribution will get even more boost.</span></span>
  
    
    

> <span data-ttu-id="bc868-731">**Tipp:** Die relative Begriffsoptimierung (positiv oder negativ) wird auf die dynamische Rangfolgekomponente der Gesamtrangfolge angewendet.</span><span class="sxs-lookup"><span data-stu-id="bc868-731">**Tip:** The relative term boost (positive or negative) is applied to the dynamic rank component of the total rank.</span></span> <span data-ttu-id="bc868-732">Die Rangberechnungen der Näheoptimierung (Abstand zwischen den Wörtern) werden nicht durch die Begriffsgewichtung beeinflusst.</span><span class="sxs-lookup"><span data-stu-id="bc868-732">However, proximity boost (distance between words) rank calculations are not affected by the term weighting.</span></span> <span data-ttu-id="bc868-733">Die relative Gewichtung impliziert nicht immer, dass die Gesamtrangfolge für das Element entsprechend dem angegebenen Prozentsatz geändert wird.</span><span class="sxs-lookup"><span data-stu-id="bc868-733">The relative weighting does not always imply that the total rank for the item is modified according to the percentage given.</span></span> <span data-ttu-id="bc868-734">> Mit der folgenden Abfrage wird nach den Begriffen "Peter", "Paul" oder "Mary" gesucht, wobei "Peter" zweimal so viel Relevanz in der Rangfolge hat wie die beiden anderen Begriffe.</span><span class="sxs-lookup"><span data-stu-id="bc868-734">> The following query will search for the terms "peter", "paul", or "mary", where "peter" will have twice as much rank contribution as the two other terms.</span></span> >  `or(peter, string("paul mary", mode="OR", weight=50))`
  
    
    

 <span data-ttu-id="bc868-735">**Verarbeitung von Zeichenfolgen mit Sonderzeichen**</span><span class="sxs-lookup"><span data-stu-id="bc868-735">**Handling strings with special characters**</span></span>
  
    
    
<span data-ttu-id="bc868-p194">Sonderzeichen wie Komma („,"), Semikolon („;"), Doppelpunkt („:"), Punkt („."), Minuszeichen („-"), Unterstrich („_"), oder Schrägstrich („/") werden innerhalb eines Zeichenfolgeausdrucks, der in doppelte Anführungszeichen eingeschlossen ist, als Leerzeichen behandelt. Dieses Verhalten steht im Zusammenhang mit dem Vorgang der Tokenisierung. Diese Zeichen schließen zudem eine implizite Phrasierung der Token ein, die durch diese Zeichen voneinander getrennt sind.</span><span class="sxs-lookup"><span data-stu-id="bc868-p194">Special characters such as comma (","), semicolon (";"), colon (":"), period ("."), minus ("-"), underline ("_"), or forward slash ("/") are treated as white space inside a string expression enclosed in double quotation marks. This is related to the tokenization process. These characters also imply an implicit phrasing of the tokens separated by these characters.</span></span> 
  
    
    
<span data-ttu-id="bc868-739">Die folgenden Abfrageausdrücke sind gleichwertig:</span><span class="sxs-lookup"><span data-stu-id="bc868-739">The following query expressions are equivalent.</span></span>
  
    
    
 `title:string("animals birds", mode="phrase")title:"animals/birds"title:string("animals/birds", mode="and")title:string("animals/birds", mode="or")`
  
    
    
<span data-ttu-id="bc868-740">Die folgenden Abfrageausdrücke sind gleichwertig:</span><span class="sxs-lookup"><span data-stu-id="bc868-740">The following query expressions are equivalent.</span></span>
  
    
    
 `title:or(string("animals birds", mode="phrase"), string("animals insects", mode="phrase"))title:string("animals/birds animals/insects", mode="or")`
  
    
    
<span data-ttu-id="bc868-741">Die folgenden Abfrageausdrücke sind gleichwertig:</span><span class="sxs-lookup"><span data-stu-id="bc868-741">The following query expressions are equivalent.</span></span>
  
    
    
 `body:string("help contoso com", mode="phrase")body:string("help@contoso.com")`
  
    
    
 <span data-ttu-id="bc868-742">**Phrasenabgleich mit Token**</span><span class="sxs-lookup"><span data-stu-id="bc868-742">**Tokenized phrase matching**</span></span>
  
    
    
<span data-ttu-id="bc868-743">Sie können mithilfe des **STRING**-Operators mit _mode_= "Ausdruck" oder dem **PHRASE**- Operator nach einer genauen Token-Zeichenfolge suchen.</span><span class="sxs-lookup"><span data-stu-id="bc868-743">You can search for an exact string of tokens by using the **STRING** operator with _mode_="phrase" or the **PHRASE** operator.</span></span>
  
    
    
<span data-ttu-id="bc868-744">Alle Ausdrucksvorgänge dieser Art setzen eine in Token übersetzte Übereinstimmung des Ausdrucks voraus.</span><span class="sxs-lookup"><span data-stu-id="bc868-744">All such phrase operations imply a tokenized phrase match.</span></span> <span data-ttu-id="bc868-745">Dies bedeutet, dass Sonderzeichen wie Komma (" **,** "), Semikolon (" **;** "), Doppelpunkt (" **:** "), Unterstrich (" \_ "), Minuszeichen (" ** - ** "), oder Schrägstrich (" ** / ** ") als Leerraum behandelt werden.</span><span class="sxs-lookup"><span data-stu-id="bc868-745">This means that special characters such as comma (" **,** "), semicolon (" **;** "), colon (" **:** "), underscore (" \_ "), minus (" **-** "), or forward slash (" **/** ") are treated as white space.</span></span> <span data-ttu-id="bc868-746">Dies bezieht sich auf den Tokenisierungsvorgang.</span><span class="sxs-lookup"><span data-stu-id="bc868-746">This is related to the tokenization process.</span></span>
  
    
    

### <a name="xrank"></a><span data-ttu-id="bc868-747">XRANK</span><span class="sxs-lookup"><span data-stu-id="bc868-747">XRANK</span></span>
<span data-ttu-id="bc868-748"><a name="fql_xrank_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-748"><a name="fql_xrank_operator"> </a></span></span>

<span data-ttu-id="bc868-p196">Verstärkt den dynamischen Rang von Elementen basierend auf bestimmten Vorkommnissen von Begriffen im  _match expression_, ohne die Abfrage dahingehend zu verändern, welche Elemente mit der Abfrage übereinstimmen. Ein **XRANK** -Ausdruck besteht aus einer Komponente, die abgeglichen werden muss, dem _match expression_ und einer oder mehreren Komponenten, die nur in der dynamischen Rangfolge relevant sind, dem _rank expression_. Es muss mindestens **einer** der Parameter angegeben werden, abgesehen von _n_, damit ein XRANK-Ausdruck gültig ist.</span><span class="sxs-lookup"><span data-stu-id="bc868-p196">Boosts the dynamic rank of items based on certain term occurrences within the  _match expression_, without changing which items match the query. An **XRANK** expression consists of one component that must be matched, the _match expression_, and one or more components that contribute only to dynamic ranking, the  _rank expression_. At least **one** of the parameters, excluding _n_, must be specified for an XRANK expression to be valid.</span></span>
  
    
    
 <span data-ttu-id="bc868-p197">_Match expressions_ kann ein beliebiger gültiger FQL-Ausdruck sein, einschließlich geschachtelter **XRANK** -Ausdrücke. _Rank expressions_ kann ein beliebiger gültiger FQL-Ausdruck ohne **XRANK**-Ausdrücke sein. Wenn Ihre FQL-Abfragen über mehrere **XRANK**-Operatoren verfügen, wird der endgültige dynamische Rangfolgewert als Summe der Verstärkungen aller **XRANK**-Operatoren berechnet.</span><span class="sxs-lookup"><span data-stu-id="bc868-p197">_Match expressions_ may be any valid FQL expression, including nested **XRANK** expressions. _Rank expressions_ may be any valid FQL expression without **XRANK** expressions. If your FQL queries have multiple **XRANK** operators, the final dynamic rank value is calculated as a sum of boosts across all **XRANK** operators.</span></span>
  
> [!NOTE]
> <span data-ttu-id="bc868-755">In SharePoint Server 2010 besaß der **XRANK**-Operator die beiden Parameter _boost_ und _boostall_ sowie die folgende Syntax: `xrank(operand, rank-operand [, rank-operand]* [,boost=n] [,boostall=yes])` .</span><span class="sxs-lookup"><span data-stu-id="bc868-755">Note: In SharePoint Server 2010, the **XRANK** operator had two parameters: _boost_ and _boostall_, as well as the following syntax:  `xrank(operand, rank-operand [, rank-operand]* [,boost=n] [,boostall=yes])`.</span></span> <span data-ttu-id="bc868-756">Diese Syntax und die dazugehörigen Parametern werden in SharePoint nicht mehr unterstützt.</span><span class="sxs-lookup"><span data-stu-id="bc868-756">This syntax along with its parameters is deprecated in SharePoint.</span></span> <span data-ttu-id="bc868-757">Wir empfehlen stattdessen, eine neue Syntax und neue Parameter zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="bc868-757">We recommend the use of the new syntax and parameters instead.</span></span> 
  
    
    


#### <a name="syntax"></a><span data-ttu-id="bc868-758">Syntax</span><span class="sxs-lookup"><span data-stu-id="bc868-758">Syntax</span></span>

 `xrank(<match expression> [, <rank-expression>]*, rank-parameter[, rank-parameter]*)`
  
    
    

#### <a name="formula"></a><span data-ttu-id="bc868-759">Formel</span><span class="sxs-lookup"><span data-stu-id="bc868-759">Formula</span></span>


  
    
    
![Formel für XRANK-Operator](../images/XRANKFormula.gif)
  
    
    

  
    
    

  
    
    

#### <a name="parameters"></a><span data-ttu-id="bc868-761">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-761">Parameters</span></span>



|<span data-ttu-id="bc868-762">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="bc868-762">**Parameter**</span></span>|<span data-ttu-id="bc868-763">**Wert**</span><span class="sxs-lookup"><span data-stu-id="bc868-763">**Value**</span></span>|<span data-ttu-id="bc868-764">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="bc868-764">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="bc868-765">_N_</span><span class="sxs-lookup"><span data-stu-id="bc868-765">_N_</span></span> <br/> | <span data-ttu-id="bc868-766">_\<integer_value\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-766">_\<integer_value\>_</span></span> <br/> |<span data-ttu-id="bc868-767">Gibt die Anzahl der Ergebnisse für die Berechnung von Statistiken an.</span><span class="sxs-lookup"><span data-stu-id="bc868-767">Specifies the number of results to compute statistics from.</span></span>  <br/> <span data-ttu-id="bc868-768">Dieser Parameter hat keine Auswirkungen auf die Anzahl der Ergebnisse, die durch die dynamische Rangfolge hinzu kommen; es handelt sich dabei lediglich um eine Methode zum Ausschließen irrelevanter Elemente aus den Berechnungen der Statistik.</span><span class="sxs-lookup"><span data-stu-id="bc868-768">This parameter does not affect the number of results that the dynamic rank contributes to; it is just a means to exclude irrelevant items from the statistics calculations.</span></span>  <br/> <span data-ttu-id="bc868-p199"> Standardwert: **0**. Ein Nullwert trägt die Semantik *aller Dokumente*  . </span><span class="sxs-lookup"><span data-stu-id="bc868-p199">Default: **0**. A zero value carries the sematic of *all documents*  . </span></span><br/> |
| <span data-ttu-id="bc868-771">_Nb_</span><span class="sxs-lookup"><span data-stu-id="bc868-771">_Nb_</span></span> <br/> | <span data-ttu-id="bc868-772">_\<float_value\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-772">_\<float_value\>_</span></span> <br/> |<span data-ttu-id="bc868-p200">Der  _nb_-Parameter verweist auf die normale Verstärkung. Dieser Parameter gibt den Faktor an, der mit dem Produkt der Abweichung und der Durchschnittsbewertung der Rangwerte der Ergebnisgruppe multipliziert wird.</span><span class="sxs-lookup"><span data-stu-id="bc868-p200">The  _nb_ parameter refers to normalized boost. This parameter specifies the factor that is multiplied with the product of the variance and average score of the rank values of the results set. </span></span><br/>  <span data-ttu-id="bc868-775">_f_ in der XRANK-Formel.</span><span class="sxs-lookup"><span data-stu-id="bc868-775">_f_ in the XRANK formula.</span></span> <br/> |
   
<span data-ttu-id="bc868-p201">In der Regel ist die normale Verstärkung ( _nb_) der einzige Parameter, der geändert wird. Dieser Parameter stellt das benötigte Steuerelement bereit, um ein bestimmtes Element höher oder niedriger zu stufen, ohne dabei die Standardabweichung zu berücksichtigen.</span><span class="sxs-lookup"><span data-stu-id="bc868-p201">Typically normalized boost,  _nb_, is the only parameter that is modified. This parameter provides the necessary control to promote or demote a particular item, without taking standard deviation into account.</span></span> 
  
    
    

#### <a name="advanced-parameters"></a><span data-ttu-id="bc868-778">Erweiterte Parameter</span><span class="sxs-lookup"><span data-stu-id="bc868-778">Advanced parameters</span></span>

<span data-ttu-id="bc868-p202">Außerdem sind folgende erweiterte Parameter verfügbar. In der Regel werden sie jedoch nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="bc868-p202">The following advanced parameters are also available. However, typically they aren't used.</span></span>
  
    
    


|<span data-ttu-id="bc868-781">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="bc868-781">**Parameter**</span></span>|<span data-ttu-id="bc868-782">**Wert**</span><span class="sxs-lookup"><span data-stu-id="bc868-782">**Value**</span></span>|<span data-ttu-id="bc868-783">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="bc868-783">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="bc868-784">_cb_</span><span class="sxs-lookup"><span data-stu-id="bc868-784">_cb_</span></span> <br/> | <span data-ttu-id="bc868-785">_\<float_value\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-785">_\<float_value\>_</span></span> <br/> |<span data-ttu-id="bc868-786">Der _cb_-Parameter bezieht sich auf eine konstante Steigerung.</span><span class="sxs-lookup"><span data-stu-id="bc868-786">The  _cb_ parameter refers to constant boost.</span></span> <br/> <span data-ttu-id="bc868-787">Standardwert: **0**.</span><span class="sxs-lookup"><span data-stu-id="bc868-787">Default: **0**.</span></span> <br/>  <span data-ttu-id="bc868-788">_a_ in der XRANK-Formel.</span><span class="sxs-lookup"><span data-stu-id="bc868-788">_a_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="bc868-789">_stdb_</span><span class="sxs-lookup"><span data-stu-id="bc868-789">_stdb_</span></span> <br/> | <span data-ttu-id="bc868-790">_\<float_value\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-790">_\<float_value\>_</span></span> <br/> |<span data-ttu-id="bc868-791">Die _stdb_-Parameter bezieht sich auf die Steigerung der Standardabweichung.</span><span class="sxs-lookup"><span data-stu-id="bc868-791">The  _stdb_ parameter refers to standard deviation boost.</span></span> <br/> <span data-ttu-id="bc868-792">Standardwert: **0**.</span><span class="sxs-lookup"><span data-stu-id="bc868-792">Default: **0**.</span></span> <br/>  <span data-ttu-id="bc868-793">_e_ in der XRANK-Formel.</span><span class="sxs-lookup"><span data-stu-id="bc868-793">_e_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="bc868-794">_avgb_</span><span class="sxs-lookup"><span data-stu-id="bc868-794">_avgb_</span></span> <br/> | <span data-ttu-id="bc868-795">_\<float_value\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-795">_\<float_value\>_</span></span> <br/> |<span data-ttu-id="bc868-p203">Der _avgb_-Parameter bezieht sich auf die durchschnittliche Steigerung. Dieser Faktor wird mit dem durchschnittlichen Rangfolgewert des Resultsets multipliziert.</span><span class="sxs-lookup"><span data-stu-id="bc868-p203">The  _avgb_ parameter refers to average boost. This factor is multiplied with the average rank value of the results set. </span></span><br/> <span data-ttu-id="bc868-798">Standardwert: **0**.</span><span class="sxs-lookup"><span data-stu-id="bc868-798">Default: **0**.</span></span> <br/>  <span data-ttu-id="bc868-799">_d_ in der XRANK-Formel.</span><span class="sxs-lookup"><span data-stu-id="bc868-799">_d_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="bc868-800">_rb_</span><span class="sxs-lookup"><span data-stu-id="bc868-800">_rb_</span></span> <br/> | <span data-ttu-id="bc868-801">_\<float_value\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-801">_\<float_value\>_</span></span> <br/> |<span data-ttu-id="bc868-p204">Der _rb_-Parameter bezieht sich auf die Rangsteigerung. Dieser Faktor wird mit der Rangfolge der Rangwerte im Resultset multipliziert.</span><span class="sxs-lookup"><span data-stu-id="bc868-p204">The  _rb_ parameter refers to range boost. This factor is multiplied with the range of rank values in the results set. </span></span><br/> <span data-ttu-id="bc868-804">Standardwert: **0**.</span><span class="sxs-lookup"><span data-stu-id="bc868-804">Default: **0**.</span></span> <br/>  <span data-ttu-id="bc868-805">_b_ in der XRANK-Formel.</span><span class="sxs-lookup"><span data-stu-id="bc868-805">_b_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="bc868-806">_pb_</span><span class="sxs-lookup"><span data-stu-id="bc868-806">_pb_</span></span> <br/> | <span data-ttu-id="bc868-807">_\<float_value\>_</span><span class="sxs-lookup"><span data-stu-id="bc868-807">_\<float_value\>_</span></span> <br/> |<span data-ttu-id="bc868-p205">Der  _pb_-Parameter verweist auf die Prozentwertverstärkung. Dieser Faktor wird im Vergleich zum Mindestwert des Korpus mit der Rangfolge des Elements multipliziert.</span><span class="sxs-lookup"><span data-stu-id="bc868-p205">The  _pb_ parameter refers to percentage boost. This factor is multiplied with the item's own rank compared to the minimum value in the corpus. </span></span><br/> <span data-ttu-id="bc868-810">Standardwert: **0**.</span><span class="sxs-lookup"><span data-stu-id="bc868-810">Default: **0**.</span></span> <br/>  <span data-ttu-id="bc868-811">_c_ in der XRANK-Formel.</span><span class="sxs-lookup"><span data-stu-id="bc868-811">_c_ in the XRANK formula.</span></span> <br/> |
   

#### <a name="examples"></a><span data-ttu-id="bc868-812">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bc868-812">Examples</span></span>

 <span data-ttu-id="bc868-p206">**Beispiel 1.** Der folgende Ausdruck gleicht Elemente ab, bei denen der Standard-Volltextindex den Begriff „Katze" oder „Hund" enthält. Der Ausdruck erhöht die dynamische Rangfolge der Elemente mit einer konstanten Verstärkung von 100 für Elemente, die zusätzlich den Begriff „Vollblutpferd" enthalten.</span><span class="sxs-lookup"><span data-stu-id="bc868-p206">**Example 1.** The following expression matches items for which the default full-text index contains either "cat" or "dog". The expression increases dynamic rank of those items with a constant boost of 100 for items that also contain "thoroughbred".</span></span>
  
    
    
 `xrank(or(cat, dog), thoroughbred, cb=100)`
  
    
    
 <span data-ttu-id="bc868-p207">**Beispiel 2.** Der folgende Ausdruck gleicht Elemente ab, bei denen der Standard-Volltextindex den Begriff „Katze" oder „Hund" enthält. Der Ausdruck erhöht die dynamische Rangfolge der Elemente mit einer normalen Verstärkung von 1,5 für Elemente, die zusätzlich den Begriff „Vollblutpferd" enthalten.</span><span class="sxs-lookup"><span data-stu-id="bc868-p207">**Example 2.** The following expression matches items for which the default full-text index contains either "cat" or "dog". The expression increases dynamic rank of those items with a normalized boost of 1.5 for items that also contain "thoroughbred".</span></span>
  
    
    
 `xrank(or(cat, dog), thoroughbred, nb=1.5)`
  
    
    
 <span data-ttu-id="bc868-p208">**Beispiel 3.** Der folgende Ausdruck gleicht Elemente ab, bei denen der Standard-Volltextindex den Begriff „Katze" oder „Hund" enthält. Der Ausdruck erhöht die dynamische Rangfolge der Elemente mit einer konstanten Verstärkung von 100 und einer normalen Verstärkung von 1,5, für Elemente, die zusätzlich den Begriff „Vollblutpferd" enthalten.</span><span class="sxs-lookup"><span data-stu-id="bc868-p208">**Example 3.** The following expression matches items for which the default full-text index contains either "cat" or "dog". The expression increases dynamic rank of those items with a constant boost of 100 and a normalized boost of 1.5, for items that also contain "thoroughbred".</span></span>
  
    
    
 `xrank(or(cat, dog), thoroughbred, cb=100, nb=1.5)`
  
    
    
 <span data-ttu-id="bc868-p209">**Beispiel 4.** Der folgende Ausdruck gleicht alle Elemente ab, die den Begriff „Tiere" enthalten und die dynamische Rangfolge wie folgt verstärken:</span><span class="sxs-lookup"><span data-stu-id="bc868-p209">**Example 4.** The following expression matches all items containing the term "animals", and boosts dynamic rank as follows:</span></span>
  
    
    

- <span data-ttu-id="bc868-824">Die dynamische Rangfolge von Elementen, die den Begriff „Hunde" enthalten, werden um 100 Punkte verstärkt.</span><span class="sxs-lookup"><span data-stu-id="bc868-824">Dynamic rank of items that contain the term "dogs" is boosted by 100 points.</span></span>
    
  
- <span data-ttu-id="bc868-825">Die dynamische Rangfolge der Elemente, die den Begriff „Katzen" enthalten, werden um 200 Punkte verstärkt.</span><span class="sxs-lookup"><span data-stu-id="bc868-825">Dynamic rank of items that contain the term "cats" is boosted by 200 points.</span></span>
    
  
- <span data-ttu-id="bc868-826">Die dynamische Rangfolge der Elemente, die die Begriffe „Hunde" und „Katzen" enthalten, werden um 300 Punkte verstärkt.</span><span class="sxs-lookup"><span data-stu-id="bc868-826">Dynamic rank of items that contain both the terms "dogs" and "cats" is boosted by 300 points.</span></span>
    
  
 `xrank(xrank(animals, dogs, cb=100), cats, cb=200)`
  
    
    

## <a name="see-also"></a><span data-ttu-id="bc868-827">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="bc868-827">See also</span></span>
<span data-ttu-id="bc868-828"><a name="SP15FQL_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="bc868-828"><a name="SP15FQL_addlresources"> </a></span></span>


-  [<span data-ttu-id="bc868-829">Erstellen von Suchabfragen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="bc868-829">Building search queries in SharePoint</span></span>](building-search-queries-in-sharepoint.md)
    
  
