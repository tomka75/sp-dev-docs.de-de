---
title: "Syntaxreferenz für die Keyword Query Language (KQL)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d8489f59-522f-433c-b9c1-69e597be51c7
ms.openlocfilehash: ae8691e371220e8c796267bba2f940a45219004d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="keyword-query-language-kql-syntax-reference"></a><span data-ttu-id="6a757-102">Syntaxreferenz für die Keyword Query Language (KQL)</span><span class="sxs-lookup"><span data-stu-id="6a757-102">Keyword Query Language (KQL) syntax reference</span></span>
<span data-ttu-id="6a757-p101">Erfahren Sie, wie Sie KQL-Abfragen für Suche in SharePoint erstellen können. In dieser Syntaxreferenz werden die KQL-Abfrageelemente und die Vorgehensweise zum Verwenden der Eigenschaftseinschränkungen und -operatoren in KQL-Abfragen erläutert.</span><span class="sxs-lookup"><span data-stu-id="6a757-p101">Learn to construct KQL queries for Search in SharePoint. This syntax reference describes KQL query elements and how to use property restrictions and operators in KQL queries.</span></span>
## <a name="elements-of-a-kql-query"></a><span data-ttu-id="6a757-105">Elemente einer KQL-Abfrage</span><span class="sxs-lookup"><span data-stu-id="6a757-105">Elements of a KQL query</span></span>
<span data-ttu-id="6a757-106"><a name="SP15KQL_elements"> </a></span><span class="sxs-lookup"><span data-stu-id="6a757-106"></span></span>

<span data-ttu-id="6a757-107">Eine KQL-Abfrage besteht aus einem oder mehreren der folgenden Elemente:</span><span class="sxs-lookup"><span data-stu-id="6a757-107">A KQL query consists of one or more of the following elements:</span></span> 
  
    
    

- <span data-ttu-id="6a757-108">Freitext-Schlüsselwörter, -Wörter oder -Ausdrücke</span><span class="sxs-lookup"><span data-stu-id="6a757-108">Free text-keywords—words or phrases</span></span> 
    
  
- <span data-ttu-id="6a757-109">Eigenschaftseinschränkungen</span><span class="sxs-lookup"><span data-stu-id="6a757-109">Property restrictions</span></span> 
    
  
<span data-ttu-id="6a757-110">Sie können KQL-Abfrageelemente mit einem oder mehreren der verfügbaren Operatoren kombinieren.</span><span class="sxs-lookup"><span data-stu-id="6a757-110">You can combine KQL query elements with one or more of the available operators.</span></span>
  
    
    
<span data-ttu-id="6a757-p102">Wenn die KQL-Abfrage nur Operatoren enthält oder leer ist, ist sie ungültig. Bei KQL-Abfragen muss die Groß- und Kleinschreibung nicht beachtet werden, bei den Operatoren hingegen schon (Großbuchstaben).</span><span class="sxs-lookup"><span data-stu-id="6a757-p102">If the KQL query contains only operators or is empty, it isn't valid. KQL queries are case-insensitive but the operators are case-sensitive (uppercase).</span></span>
  
    
    

> <span data-ttu-id="6a757-113">**Hinweis:** Die Längenbegrenzung einer KQL-Abfrage ist abhängig von der Erstellung unterschiedlich.</span><span class="sxs-lookup"><span data-stu-id="6a757-113">**Note:** The length limit of a KQL query varies depending on how you create it.</span></span> <span data-ttu-id="6a757-114">Wenn Sie die KQL-Abfrage mit dem standardmäßigen SharePoint-Suche-Front-End erstellt haben, beträgt die Längenbegrenzung 2.048 Zeichen.</span><span class="sxs-lookup"><span data-stu-id="6a757-114">If you create the KQL query by using the default SharePoint search front end, the length limit is 2,048 characters.</span></span> <span data-ttu-id="6a757-115">KQL-Abfragen, die Sie programmgesteuert mit dem Abfrage-Objektmodell erstellt haben, besitzen eine Längenbegrenzung von 4.096 Zeichen.</span><span class="sxs-lookup"><span data-stu-id="6a757-115">However, KQL queries you create programmatically by using the Query object model have a default length limit of 4,096 characters.</span></span> <span data-ttu-id="6a757-116">Mit der Eigenschaft [MaxKeywordQueryTextLength](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.MaxKeywordQueryTextLength.aspx) oder [DiscoveryMaxKeywordQueryTextLength](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.DiscoveryMaxKeywordQueryTextLength.aspx) (für eDiscovery) können Sie den Grenzwert auf bis zu 20.480 Zeichen erhöhen.</span><span class="sxs-lookup"><span data-stu-id="6a757-116">You can increase this limit up to 20,480 characters by using the  [MaxKeywordQueryTextLength](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.MaxKeywordQueryTextLength.aspx) property or the [DiscoveryMaxKeywordQueryTextLength](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.DiscoveryMaxKeywordQueryTextLength.aspx) property (for eDiscovery).</span></span>
  
    
    


## <a name="constructing-free-text-queries-using-kql"></a><span data-ttu-id="6a757-117">Erstellen von Freitext-Abfragen mit KQL</span><span class="sxs-lookup"><span data-stu-id="6a757-117">Constructing free-text queries using KQL</span></span>
<span data-ttu-id="6a757-118"><a name="SP15KQL_constructing_freetext_queries"> </a></span><span class="sxs-lookup"><span data-stu-id="6a757-118"></span></span>

<span data-ttu-id="6a757-p104">Wenn Sie die KQL-Abfrage mit Freitext-Ausdrücken erstellen, gleicht Suche in SharePoint die Ergebnisse mit den von Ihnen für die Abfrage ausgewählten Begriffen basierend auf den im Volltextindex gespeicherten Begriffen ab. Dazu gehören auch verwaltete Eigenschaftswerte, bei denen  [FullTextQueriable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.FullTextQueriable.aspx) auf **true** gesetzt wurde.</span><span class="sxs-lookup"><span data-stu-id="6a757-p104">When you construct your KQL query by using free-text expressions, Search in SharePoint matches results for the terms you chose for the query based on terms stored in the full-text index. This includes managed property values where  [FullTextQueriable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.FullTextQueriable.aspx) is set to **true**.</span></span>
  
    
    
<span data-ttu-id="6a757-p105">Bei Freitext-KQL-Abfragen muss die Groß- und Kleinschreibung nicht berücksichtigt werden, Operatoren müssen jedoch groß geschrieben werden. Sie können KQL-Abfragen erstellen, indem Sie eine oder mehrere der folgenden Freitext-Abfragen verwenden:</span><span class="sxs-lookup"><span data-stu-id="6a757-p105">Free text KQL queries are case-insensitive but the operators must be in uppercase. You can construct KQL queries by using one or more of the following as free-text expressions:</span></span>
  
    
    

- <span data-ttu-id="6a757-123">Ein **word** (enthält ein oder mehrere Zeichen ohne Leerzeichen oder Interpunktion)</span><span class="sxs-lookup"><span data-stu-id="6a757-123">A **word** (includes one or more characters without spaces or punctuation)</span></span>
    
  
- <span data-ttu-id="6a757-124">Ein **phrase** (enthält zwei oder mehrere Wörter, die durch Leerzeichen getrennt sind; die Wörter müssen jedoch in doppelte Anführungszeichen gesetzt werden)</span><span class="sxs-lookup"><span data-stu-id="6a757-124">A **phrase** (includes two or more words together, separated by spaces; however, the words must be enclosed in double quotation marks)</span></span>
    
  
<span data-ttu-id="6a757-p106">Um komplexe Abfragen zu erstellen, können Sie mehrere Freitext-Ausdrücke mit KQL-Abfrageoperatoren kombinieren. Wenn mehrere Freitext-Ausdrücke mit darin enthaltenen Operatoren vorhanden sind, verhält sich die Abfrage wie beim Verwenden des **AND**-Operators.</span><span class="sxs-lookup"><span data-stu-id="6a757-p106">To construct complex queries, you can combine multiple free-text expressions with KQL query operators. If there are multiple free-text expressions without any operators in between them, the query behavior is the same as using the **AND** operator.</span></span>
  
    
    

### <a name="using-words-in-the-free-text-kql-query"></a><span data-ttu-id="6a757-127">Verwenden von Wörtern in der Freitext-KQL-Abfrage</span><span class="sxs-lookup"><span data-stu-id="6a757-127">Using words in the free-text KQL query</span></span>

<span data-ttu-id="6a757-p107">Wenn Sie Wörter in einer Freitext-KQL-Abfrage verwenden, gibt Suche in SharePoint die Ergebnisse basierend auf den exakten Übereinstimmungen Ihrer Wörter mit den im Volltextindex gespeicherten Begriffen zurück. Sie können auch nur den ersten Teil eines Worts verwenden, indem Sie den Platzhalter-Operator (*) verwenden, um den Präfix-Abgleich zu aktivieren. Im Präfix-Abgleich gleicht Suche in SharePoint die Ergebnisse mit den Begriffen ab, die das Wort gefolgt von Null oder mehr Zeichen enthalten.</span><span class="sxs-lookup"><span data-stu-id="6a757-p107">When you use words in a free-text KQL query, Search in SharePoint returns results based on exact matches of your words with the terms stored in the full-text index. You can use just a part of a word, from the beginning of the word, by using the wildcard operator (*) to enable prefix matching. In prefix matching, Search in SharePoint matches results with terms that contain the word followed by zero or more characters.</span></span>
  
    
    
<span data-ttu-id="6a757-131">Folgende KQL-Abfragen geben beispielsweise Inhaltselemente zurück, die die Begriffe „Verbund" und „Suche" enthalten:</span><span class="sxs-lookup"><span data-stu-id="6a757-131">For example, the following KQL queries return content items that contain the terms "federated" and "search":</span></span> 
  
    
    
 `federated search`
  
    
    
 `federat* search`
  
    
    
 `search fed*`
  
    
    
<span data-ttu-id="6a757-132">KQL-Abfragen unterstützen keinen Suffix-Abgleich.</span><span class="sxs-lookup"><span data-stu-id="6a757-132">KQL queries don't support suffix matching.</span></span>
  
    
    

### <a name="using-phrases-in-the-free-text-kql-query"></a><span data-ttu-id="6a757-133">Verwenden von Ausdrücken in der Freitext-KQL-Abfrage</span><span class="sxs-lookup"><span data-stu-id="6a757-133">Using phrases in the free-text KQL query</span></span>

<span data-ttu-id="6a757-p108">Wenn Sie Ausdrücke in einer Freitext-KQL-Abfrage verwenden, gibt Suche in SharePoint nur die Elemente zurück, in denen sich die Wörter aus Ihrem Ausdruck direkt nebeneinander befinden. Um einen Ausdruck in einer KQL-Abfrage anzugeben, müssen Sie doppelte Anführungszeichen verwenden.</span><span class="sxs-lookup"><span data-stu-id="6a757-p108">When you use phrases in a free-text KQL query, Search in SharePoint returns only the items in which the words in your phrase are located next to each other. To specify a phrase in a KQL query, you must use double quotation marks.</span></span> 
  
    
    
<span data-ttu-id="6a757-p109">KQL-Abfragen unterstützen keinen Suffix-Abgleich, Sie können also in Freitext-Abfragen keinen Platzhalter-Operator vor einem Ausdruck verwenden. Sie können den Platzhalter-Operator jedoch nach einem Ausdruck verwenden.</span><span class="sxs-lookup"><span data-stu-id="6a757-p109">KQL queries don't support suffix matching, so you can't use the wildcard operator before a phrase in free-text queries. However, you can use the wildcard operator after a phrase.</span></span>
  
    
    

## <a name="property-restriction-queries-in-kql"></a><span data-ttu-id="6a757-138">Eigenschaftseinschränkung-Abfragen in KQL</span><span class="sxs-lookup"><span data-stu-id="6a757-138">Property restriction queries in KQL</span></span>
<span data-ttu-id="6a757-139"><a name="kql_property_restriction_queries"> </a></span><span class="sxs-lookup"><span data-stu-id="6a757-139"></span></span>

<span data-ttu-id="6a757-140">Mit KQL können Sie Abfragen erstellen, die Eigenschaftseinschränkungen verwenden, um den Fokus der Abfrage einzugrenzen, damit die Ergebnisse nur auf einer bestimmten Bedingung basierend abgeglichen werden.</span><span class="sxs-lookup"><span data-stu-id="6a757-140">Using KQL, you can construct queries that use property restrictions to narrow the focus of the query to match only results based on a specified condition.</span></span>
  
    
    

### <a name="specifying-property-restrictions"></a><span data-ttu-id="6a757-141">Angeben von Eigenschaftseinschränkungen</span><span class="sxs-lookup"><span data-stu-id="6a757-141">Specifying property restrictions</span></span>

<span data-ttu-id="6a757-142">Eine einfache Eigenschaftseinschränkung besteht aus folgenden Teilen:</span><span class="sxs-lookup"><span data-stu-id="6a757-142">A basic property restriction consists of the following:</span></span>
  
    
    
 `<Property Name><Property Operator><Property Value>`
  
    
    
<span data-ttu-id="6a757-143">In Tabelle 1 werden einige Beispiele gültiger Eigenschaftseinschränkungssyntaxen in KQL-Abfragen aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="6a757-143">Table 1 lists some examples of valid property restrictions syntax in KQL queries.</span></span>
  
    
    

<span data-ttu-id="6a757-144">**Tabelle 1: Gültige Eigenschaftseinschränkungssyntax**</span><span class="sxs-lookup"><span data-stu-id="6a757-144">**Table 1. Valid property restriction syntax**</span></span>


|<span data-ttu-id="6a757-145">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="6a757-145">**Syntax**</span></span>|<span data-ttu-id="6a757-146">**gibt zurück**</span><span class="sxs-lookup"><span data-stu-id="6a757-146">**Returns**</span></span>|
|:-----|:-----|
| `author:"John Smith"` <br/> |<span data-ttu-id="6a757-147">Gibt von John Smith verfasste Inhaltselemente zurück.</span><span class="sxs-lookup"><span data-stu-id="6a757-147">Returns content items authored by John Smith.</span></span>  <br/> |
| `filetype:docx` <br/> |<span data-ttu-id="6a757-148">Gibt Microsoft Word-Dokumente zurück.</span><span class="sxs-lookup"><span data-stu-id="6a757-148">Returns Microsoft Word documents.</span></span>  <br/> |
| `filename:budget.xlsx` <br/> |<span data-ttu-id="6a757-149">Gibt Inhaltselemente mit dem Dateinamen  `budget.xlsx` zurück.</span><span class="sxs-lookup"><span data-stu-id="6a757-149">Returns content items with the file name  `budget.xlsx`.</span></span>  <br/> |
   
<span data-ttu-id="6a757-p110">Die Eigenschaftseinschränkung darf kein Leerzeichen zwischen Eigenschaftsname, Eigenschaftsoperator und Eigenschaftswert enthalten, andernfalls wird die Eigenschaftseinschränkung als Freitext-Abfrage behandelt. Die Länge einer Eigenschaftseinschränkung ist auf 2.048 Zeichen begrenzt.</span><span class="sxs-lookup"><span data-stu-id="6a757-p110">The property restriction must not include white space between the property name, property operator, and the property value, or the property restriction is treated as a free-text query. The length of a property restriction is limited to 2,048 characters.</span></span> 
  
    
    
<span data-ttu-id="6a757-152">In den folgenden Beispielen bewirkt das Leerzeichen, dass die Abfrage Inhaltselemente zurückgibt, die die Begriffe „Autor" und „John Smith" enthalten, statt von John Smith verfasste Inhaltselemente zurückzugeben:</span><span class="sxs-lookup"><span data-stu-id="6a757-152">In the following examples, the white space causes the query to return content items containing the terms "author" and "John Smith", instead of content items authored by John Smith:</span></span>
  
    
    
 `author: "John Smith"`
  
    
    
 `author :"John Smith"`
  
    
    
 `author : "John Smith"`
  
    
    
<span data-ttu-id="6a757-153">Anders ausgedrückt, die vorherigen Eigenschaftseinschränkungen entsprechen folgendem Sachverhalt:</span><span class="sxs-lookup"><span data-stu-id="6a757-153">In other words, the previous property restrictions are equivalent to the following:</span></span>
  
    
    
 `author "John Smith"`
  
    
    

### <a name="specifying-property-names-for-property-restrictions"></a><span data-ttu-id="6a757-154">Angeben von Eigenschaftsnamen für Eigenschaftseinschränkungen</span><span class="sxs-lookup"><span data-stu-id="6a757-154">Specifying property names for property restrictions</span></span>

<span data-ttu-id="6a757-p111">Sie müssen einen gültigen verwalteten Eigenschaftsnamen für die Eigenschaftseinschränkung angeben. Standardmäßig enthält Suche in SharePoint verschiedene verwaltete Eigenschaften für Dokumente.</span><span class="sxs-lookup"><span data-stu-id="6a757-p111">You must specify a valid managed property name for the property restriction. By default, Search in SharePoint includes several managed properties for documents.</span></span>
  
    
    
<span data-ttu-id="6a757-p112">Um eine Eigenschaftseinschränkung für einen durchforsteten Eigenschaftswert anzugeben, müssen Sie die durchforstete Eigenschaft zunächst der verwalteten Eigenschaft zuordnen. Weitere Informationen dazu finden Sie unter **Verwaltete und durchforstete Eigenschaften** unter [Planen der Endbenutzer-Sucherfahrung](http://technet.microsoft.com/en-us/library/cc263089.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a757-p112">To specify a property restriction for a crawled property value, you must first map the crawled property to a managed property. See **Managed and crawled properties** in [Plan the end-user search experience](http://technet.microsoft.com/en-us/library/cc263089.aspx).</span></span> 
  
    
    
<span data-ttu-id="6a757-p113">Die verwaltete Eigenschaft muss  [Queryable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.Queryable.aspx) sein, damit Sie in einem Dokument nach der verwalteten Eigenschaft suchen können. Außerdem kann die verwaltete Eigenschaft [Retrievable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.Retrievable.aspx) sein, damit sie abgerufen werden kann. Die verwaltete Eigenschaft muss jedoch nicht [Retrievable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.Retrievable.aspx) sein, damit Eigenschaftssuchen ausgeführt werden können.</span><span class="sxs-lookup"><span data-stu-id="6a757-p113">The managed property must be  [Queryable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.Queryable.aspx) so that you can search for that managed property in a document. In addition, the managed property may be [Retrievable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.Retrievable.aspx) for the managed property to be retrieved. However, the managed property doesn't have to be [Retrievable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.Retrievable.aspx) to carry out property searches.</span></span>
  
    
    

### <a name="property-operators-that-are-supported-in-property-restrictions"></a><span data-ttu-id="6a757-162">In Eigenschaftseinschränkungen unterstützte Eigenschaftsoperatoren</span><span class="sxs-lookup"><span data-stu-id="6a757-162">Property operators that are supported in property restrictions</span></span>

<span data-ttu-id="6a757-163">Suche in SharePoint unterstützt verschiedene Eigenschaftsoperatoren für Eigenschaftseinschränkungen, siehe Tabelle 2.</span><span class="sxs-lookup"><span data-stu-id="6a757-163">Search in SharePoint supports several property operators for property restrictions, as shown in Table 2.</span></span> 
  
    
    

<span data-ttu-id="6a757-164">**Tabelle 2: Gültige Eigenschaftsoperatoren für Eigenschaftseinschränkungen**</span><span class="sxs-lookup"><span data-stu-id="6a757-164">**Table 2. Valid property operators for property restrictions**</span></span>


|<span data-ttu-id="6a757-165">**Operator**</span><span class="sxs-lookup"><span data-stu-id="6a757-165">**Operator**</span></span>|<span data-ttu-id="6a757-166">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="6a757-166">**Description**</span></span>|<span data-ttu-id="6a757-167">**Unterstützter verwalteter Eigenschaftstyp**</span><span class="sxs-lookup"><span data-stu-id="6a757-167">**Supported managed property type**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="6a757-168">:</span><span class="sxs-lookup"><span data-stu-id="6a757-168"></span></span>  <br/> |<span data-ttu-id="6a757-169">Gibt Ergebnisse zurück, in denen der in der Eigenschaftseinschränkung angegebene Wert dem in der Eigenschaftsspeicher-Datenbank gespeicherten Eigenschaftswert entspricht, oder mit einzelnen Begriffen des im Volltextindex gespeicherten Eigenschaftswerts übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="6a757-169">Returns results where the value specified in the property restriction is equal to the property value that is stored in the Property Store database, or matches individual terms in the property value that is stored in the full-text index.</span></span>  <br/> | [<span data-ttu-id="6a757-170">Text</span><span class="sxs-lookup"><span data-stu-id="6a757-170">Text</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Text.aspx) <br/>  [<span data-ttu-id="6a757-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="6a757-171">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="6a757-172">Integer</span><span class="sxs-lookup"><span data-stu-id="6a757-172">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="6a757-173">Decimal</span><span class="sxs-lookup"><span data-stu-id="6a757-173">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="6a757-174">Double</span><span class="sxs-lookup"><span data-stu-id="6a757-174">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/>  [<span data-ttu-id="6a757-175">YesNo</span><span class="sxs-lookup"><span data-stu-id="6a757-175">Yes/No</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.YesNo.aspx) <br/> |
|=  <br/> |<span data-ttu-id="6a757-176">Gibt Suchergebnisse zurück, in denen der Eigenschaftswert gleich dem in der Eigenschaftseinschränkung angegeben Wert ist.</span><span class="sxs-lookup"><span data-stu-id="6a757-176">Returns search results where the property value is equal to the value specified in the property restriction.</span></span>  <br/> <span data-ttu-id="6a757-177">**Hinweis:** Es wird nicht empfohlen, den **=**-Operator bei genauen Übereinstimmungen mit einem Sternchen (**\***) zu kombinieren.</span><span class="sxs-lookup"><span data-stu-id="6a757-177">We do not recommend combining the **=** operator together with asterisk ( *****) when you do exact matching.</span></span>           | [<span data-ttu-id="6a757-178">Text</span><span class="sxs-lookup"><span data-stu-id="6a757-178">Text</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Text.aspx) <br/>  [<span data-ttu-id="6a757-179">DateTime</span><span class="sxs-lookup"><span data-stu-id="6a757-179">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="6a757-180">Integer</span><span class="sxs-lookup"><span data-stu-id="6a757-180">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="6a757-181">Decimal</span><span class="sxs-lookup"><span data-stu-id="6a757-181">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="6a757-182">Double</span><span class="sxs-lookup"><span data-stu-id="6a757-182">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/>  [<span data-ttu-id="6a757-183">YesNo</span><span class="sxs-lookup"><span data-stu-id="6a757-183">Yes/No</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.YesNo.aspx) <br/> |
|<  <br/> |<span data-ttu-id="6a757-184">Gibt Ergebnisse zurück, in denen der Eigenschaftswert geringer als der in der Eigenschaftseinschränkung angegebene Wert ist.</span><span class="sxs-lookup"><span data-stu-id="6a757-184">Returns results where the property value is less than the value specified in the property restriction.</span></span>  <br/> | [<span data-ttu-id="6a757-185">DateTime</span><span class="sxs-lookup"><span data-stu-id="6a757-185">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="6a757-186">Integer</span><span class="sxs-lookup"><span data-stu-id="6a757-186">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="6a757-187">Decimal</span><span class="sxs-lookup"><span data-stu-id="6a757-187">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="6a757-188">Double</span><span class="sxs-lookup"><span data-stu-id="6a757-188">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/> |
|>  <br/> |<span data-ttu-id="6a757-189">Gibt Suchergebnisse zurück, in denen der Eigenschaftswert größer als der in der Eigenschaftseinschränkung angegeben Wert ist.</span><span class="sxs-lookup"><span data-stu-id="6a757-189">Returns search results where the property value is greater than the value specified in the property restriction.</span></span>  <br/> | [<span data-ttu-id="6a757-190">DateTime</span><span class="sxs-lookup"><span data-stu-id="6a757-190">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="6a757-191">Integer</span><span class="sxs-lookup"><span data-stu-id="6a757-191">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="6a757-192">Decimal</span><span class="sxs-lookup"><span data-stu-id="6a757-192">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="6a757-193">Double</span><span class="sxs-lookup"><span data-stu-id="6a757-193">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/> |
|<=  <br/> |<span data-ttu-id="6a757-194">Gibt Suchergebnisse zurück, in denen der Eigenschaftswert kleiner gleich dem in der Eigenschaftseinschränkung angegebenen Wert ist.</span><span class="sxs-lookup"><span data-stu-id="6a757-194">Returns search results where the property value is less than or equal to the value specified in the property restriction.</span></span>  <br/> | [<span data-ttu-id="6a757-195">DateTime</span><span class="sxs-lookup"><span data-stu-id="6a757-195">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="6a757-196">Integer</span><span class="sxs-lookup"><span data-stu-id="6a757-196">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="6a757-197">Decimal</span><span class="sxs-lookup"><span data-stu-id="6a757-197">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="6a757-198">Double</span><span class="sxs-lookup"><span data-stu-id="6a757-198">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/> |
|>=  <br/> |<span data-ttu-id="6a757-199">Gibt Suchergebnisse zurück, in denen der Eigenschaftswert größer gleich dem in der Eigenschaftseinschränkung angegebenen Wert ist.</span><span class="sxs-lookup"><span data-stu-id="6a757-199">Returns search results where the property value is greater than or equal to the value specified in the property restriction.</span></span>  <br/> | [<span data-ttu-id="6a757-200">DateTime</span><span class="sxs-lookup"><span data-stu-id="6a757-200">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="6a757-201">Integer</span><span class="sxs-lookup"><span data-stu-id="6a757-201">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="6a757-202">Decimal</span><span class="sxs-lookup"><span data-stu-id="6a757-202">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="6a757-203">Double</span><span class="sxs-lookup"><span data-stu-id="6a757-203">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/> |
|\<\>  <br/> |<span data-ttu-id="6a757-204">Gibt Suchergebnisse zurück, in denen der Eigenschaftswert nicht dem in der Eigenschaftseinschränkung angegebenen Wert entspricht.</span><span class="sxs-lookup"><span data-stu-id="6a757-204">Returns search results where the property value does not equal the value specified in the property restriction.</span></span>  <br/> | [<span data-ttu-id="6a757-205">DateTime</span><span class="sxs-lookup"><span data-stu-id="6a757-205">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="6a757-206">Integer</span><span class="sxs-lookup"><span data-stu-id="6a757-206">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="6a757-207">Decimal</span><span class="sxs-lookup"><span data-stu-id="6a757-207">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="6a757-208">Text</span><span class="sxs-lookup"><span data-stu-id="6a757-208">Text</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Text.aspx) <br/>  [<span data-ttu-id="6a757-209">Double</span><span class="sxs-lookup"><span data-stu-id="6a757-209">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/>  [<span data-ttu-id="6a757-210">YesNo</span><span class="sxs-lookup"><span data-stu-id="6a757-210">Yes/No</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.YesNo.aspx) <br/> |
|<span data-ttu-id="6a757-211">..</span><span class="sxs-lookup"><span data-stu-id="6a757-211"></span></span>  <br/> |<span data-ttu-id="6a757-212">Gibt Suchergebnisse zurück, in denen der Eigenschaftswert innerhalb des in der Eigenschaftseinschränkung angegebenen Bereichs liegt.</span><span class="sxs-lookup"><span data-stu-id="6a757-212">Returns search results where the property value falls within the range specified in the property restriction.</span></span>  <br/> <span data-ttu-id="6a757-p114">Der Bereich A..B stellt beispielsweise eine Gruppe von Werten zwischen A und B, in der A und B enthalten sind. Bei Datumsbereichen liegt der Bereich dann zwischen Anfang Tag A und Ende Tag B.</span><span class="sxs-lookup"><span data-stu-id="6a757-p114">For example, the range A..B represents a set of values from A to B where both A and B are inclusive. For date ranges this means from the beginning of day A to the end of day B.</span></span>  <br/> | [<span data-ttu-id="6a757-215">DateTime</span><span class="sxs-lookup"><span data-stu-id="6a757-215">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="6a757-216">Integer</span><span class="sxs-lookup"><span data-stu-id="6a757-216">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="6a757-217">Decimal</span><span class="sxs-lookup"><span data-stu-id="6a757-217">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="6a757-218">Double</span><span class="sxs-lookup"><span data-stu-id="6a757-218">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/> |
   

### <a name="specifying-property-values"></a><span data-ttu-id="6a757-219">Angeben von Eigenschaftswerten</span><span class="sxs-lookup"><span data-stu-id="6a757-219">Specifying property values</span></span>

<span data-ttu-id="6a757-p115">Sie müssen einen Eigenschaftswert angeben, der ein gültiger Datentyp für den verwalteten Eigenschaftstyp ist. In Tabelle 3 sind diese Typenzuordnungen aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="6a757-p115">You must specify a property value that is a valid data type for the managed property's type. Table 3 lists these type mappings.</span></span>
  
    
    

<span data-ttu-id="6a757-222">**Tabelle 3: Gültige Datentypenzuordnungen für verwaltete Eigenschaftstypen**</span><span class="sxs-lookup"><span data-stu-id="6a757-222">**Table 3. Valid data type mappings for managed property types**</span></span>


|<span data-ttu-id="6a757-223">**Verwalteter Typ**</span><span class="sxs-lookup"><span data-stu-id="6a757-223">**Managed type**</span></span>|<span data-ttu-id="6a757-224">**Datentyp**</span><span class="sxs-lookup"><span data-stu-id="6a757-224">**Data type**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="6a757-225">Text</span><span class="sxs-lookup"><span data-stu-id="6a757-225">Text</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Text.aspx) <br/> | [<span data-ttu-id="6a757-226">String</span><span class="sxs-lookup"><span data-stu-id="6a757-226">String</span></span>](https://msdn.microsoft.com/library/System.String.aspx) <br/> |
| [<span data-ttu-id="6a757-227">Integer</span><span class="sxs-lookup"><span data-stu-id="6a757-227">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/> | [<span data-ttu-id="6a757-228">Int64</span><span class="sxs-lookup"><span data-stu-id="6a757-228">Int64</span></span>](https://msdn.microsoft.com/library/System.Int64.aspx) <br/> |
| [<span data-ttu-id="6a757-229">Double</span><span class="sxs-lookup"><span data-stu-id="6a757-229">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/> | [<span data-ttu-id="6a757-230">System.Double</span><span class="sxs-lookup"><span data-stu-id="6a757-230">System.Double</span></span>](https://msdn.microsoft.com/library/System.Double.aspx) <br/> |
| [<span data-ttu-id="6a757-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="6a757-231">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/> | [<span data-ttu-id="6a757-232">Decimal</span><span class="sxs-lookup"><span data-stu-id="6a757-232">Decimal</span></span>](https://msdn.microsoft.com/library/System.Decimal.aspx) <br/> |
| [<span data-ttu-id="6a757-233">DateTime()</span><span class="sxs-lookup"><span data-stu-id="6a757-233">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/> | [<span data-ttu-id="6a757-234">DateTime</span><span class="sxs-lookup"><span data-stu-id="6a757-234">DateTime</span></span>](https://msdn.microsoft.com/library/System.DateTime.aspx) <br/> |
| [<span data-ttu-id="6a757-235">YesNo</span><span class="sxs-lookup"><span data-stu-id="6a757-235">Yes/No</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.YesNo.aspx) <br/> | [<span data-ttu-id="6a757-236">Boolean</span><span class="sxs-lookup"><span data-stu-id="6a757-236">Boolean</span></span>](https://msdn.microsoft.com/library/System.Boolean.aspx) <br/> |
   

#### <a name="text-property-values"></a><span data-ttu-id="6a757-237">Texteigenschaftstypen</span><span class="sxs-lookup"><span data-stu-id="6a757-237">Text property values</span></span>

<span data-ttu-id="6a757-238">Bei Texteigenschaftswerten hängt das Übereinstimmungsverhalten davon ab, ob die Eigenschaft im Volltextindex oder im Suchindex gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="6a757-238">For text property values, the matching behavior depends on whether the property is stored in the full-text index or in the search index.</span></span> 
  
    
    

#### <a name="property-values-in-the-full-text-index"></a><span data-ttu-id="6a757-239">Eigenschaftswerte im Volltextindex</span><span class="sxs-lookup"><span data-stu-id="6a757-239">Property values in the full-text index</span></span>

<span data-ttu-id="6a757-p116">Eigenschaftswerte werden im Volltextindex gespeichert, wenn die **FullTextQueriable**-Eigenschaft für eine verwaltete Eigenschaft auf **true**wurde. Sie können diese Einstellung nur für Zeichenfolgeneigenschaften konfigurieren. In der Abfrage angegebene Eigenschaftswerte werden mit den einzelnen Begriffen abgeglichen, die im Volltextindex gespeichert sind. Verwenden Sie die  [NoWordBreaker](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.NoWordBreaker.aspx) -Eigenschaft, um anzugeben, ob sie mit dem gesamten Eigenschaftswert abgeglichen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="6a757-p116">Property values are stored in the full-text index when the **FullTextQueriable** property is set to **true** for a managed property. You can configure this only for string properties. Property values that are specified in the query are matched against individual terms that are stored in the full-text index. Use the [NoWordBreaker](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.NoWordBreaker.aspx) property to specify whether to match with the whole property value.</span></span>
  
    
    
<span data-ttu-id="6a757-244">Wenn Sie beispielsweise nach einem von Paul Shakespear verfassten Inhaltselement suchen, gibt die folgende KQL-Abfrage übereinstimmende Ergebnisse zurück:</span><span class="sxs-lookup"><span data-stu-id="6a757-244">For example, if you're searching for a content item authored by Paul Shakespear, the following KQL query returns matching results:</span></span>
  
    
    
 `author:Shakespear`
  
    
    
 `author:Paul`
  
    
    
<span data-ttu-id="6a757-p117">Der Präfix-Abgleich wird auch unterstützt. Sie können den Platzhalter-Operator (*) verwenden, das ist jedoch nicht erforderlich, wenn Sie einzelne Wörter angeben. Um erneut auf das vorherige Beispiel zurückzukommen: folgende KQL-Abfrage gibt von Paul Shakespear verfasste Inhaltselemente als Übereinstimmungen zurück:</span><span class="sxs-lookup"><span data-stu-id="6a757-p117">Prefix matching is also supported. You can use the wildcard operator (*), but isn't required when you specify individual words. Continuing with the previous example, the following KQL query returns content items authored by Paul Shakespear as matches:</span></span> 
  
    
    
 `author:Shakesp*`
  
    
    
<span data-ttu-id="6a757-p118">Wenn Sie für den Eigenschaftswert einen Ausdruck angeben, müssen übereinstimmende Ergebnisse den angegebenen Ausdruck im Eigenschaftswert enthalten, der im Volltextindex gespeichert ist. Das folgende Abfrage-Beispiel gibt Inhaltselemente zurück, die den Text „Erweiterte Suche" im Titel enthalten, wie z. B. „Erweiterte Suche XML", „Weitere Informationen zur erweiterten Suche Webpart" usw.:</span><span class="sxs-lookup"><span data-stu-id="6a757-p118">When you specify a phrase for the property value, matched results must contain the specified phrase within the property value that is stored in the full-text index. The following query example returns content items with the text "Advanced Search" in the title, such as "Advanced Search XML", "Learning About the Advanced Search Web Part", and so on:</span></span>
  
    
    
 `title:"Advanced Search"`
  
    
    
<span data-ttu-id="6a757-250">Der Präfix-Abgleich wird auch für in den Eigenschaftswerten angegebene Ausdrücke unterstützt, dafür müssen Sie jedoch den Platzhalter-Operator (*) in der Abfrage verwenden. Außerdem wird er nur am Ende des Ausdrucks unterstützt, siehe folgendes Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6a757-250">Prefix matching is also supported with phrases specified in property values, but you must use the wildcard operator (*) in the query, and it is supported only at the end of the phrase, as follows:</span></span>
  
    
    
 `title:"Advanced Sear*"`
  
    
    
<span data-ttu-id="6a757-251">Folgende Abfragen geben nicht das erwartete Ergebnis zurück:</span><span class="sxs-lookup"><span data-stu-id="6a757-251">The following queries do not return the expected results:</span></span>
  
    
    
 `title:"Advan* Search"`
  
    
    
 `title:"Advanced Sear"`
  
    
    

#### <a name="numerical-values-for-properties"></a><span data-ttu-id="6a757-252">Numerische Werte für Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a757-252">Numerical values for properties</span></span>

<span data-ttu-id="6a757-253">Numerische Eigenschaftswerte, die die verwalteten Typen **Integer**, **Double** und **Decimal** enthalten, wird die Eigenschaftseinschränkung mit dem gesamten Eigenschaftswert abgeglichen.</span><span class="sxs-lookup"><span data-stu-id="6a757-253">For numerical property values, which include the **Integer**, **Double**, and **Decimal** managed types, the property restriction is matched against the entire value of the property.</span></span>
  
    
    

### <a name="date-or-time-values-for-properties"></a><span data-ttu-id="6a757-254">Datums- oder Zeitwerte für Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="6a757-254">Date or time values for properties</span></span>

<span data-ttu-id="6a757-255">KQL stellt den Datentyp **datetime** für das Datum und die Zeit bereit. Folgende mit der ISO 8601 kompatible datetime-Formate werden in Abfragen unterstützt:</span><span class="sxs-lookup"><span data-stu-id="6a757-255">KQL provides the **datetime** data type for date and time.The following ISO 8601-compatible datetime formats are supported in queries:</span></span>
  
    
    

- <span data-ttu-id="6a757-256">JJJJ-MM-TT</span><span class="sxs-lookup"><span data-stu-id="6a757-256">YYYY-MM-DD</span></span>
    
  
- <span data-ttu-id="6a757-257">JJJJ-MM-TTThh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="6a757-257">YYYY-MM-DDThh:mm:ss</span></span>
    
  
- <span data-ttu-id="6a757-258">YYYY-MM-DDThh:mm:ssZ</span><span class="sxs-lookup"><span data-stu-id="6a757-258">YYYY-MM-DDThh:mm:ssZ</span></span>
    
  
- <span data-ttu-id="6a757-259">YYYY-MM-DDThh:mm:ssfrZ</span><span class="sxs-lookup"><span data-stu-id="6a757-259">YYYY-MM-DDThh:mm:ssfrZ</span></span>
    
  
<span data-ttu-id="6a757-260">In diesen **datetime**-Formaten:</span><span class="sxs-lookup"><span data-stu-id="6a757-260">In these **datetime** formats:</span></span>
  
    
    

-  <span data-ttu-id="6a757-261">_YYYY_ gibt eine vierziffrige Jahreszahl an.</span><span class="sxs-lookup"><span data-stu-id="6a757-261">_YYYY_ specifies a four-digit year.</span></span>
    
    > <span data-ttu-id="6a757-262">**Hinweis:** Es werden nur vierziffrige Jahresangaben unterstützt.</span><span class="sxs-lookup"><span data-stu-id="6a757-262">**Note** Only four-digit years are supported.</span></span> 
-  <span data-ttu-id="6a757-p119">_MM_ gibt einen zweiziffrigen Monat an, z.B. 01 = Januar.</span><span class="sxs-lookup"><span data-stu-id="6a757-p119">_MM_ specifies a two-digit month. For example, 01 = January.</span></span>
    
  
-  <span data-ttu-id="6a757-265">_DD_ gibt einen zweiziffrigen Tag des Monats an (01-31).</span><span class="sxs-lookup"><span data-stu-id="6a757-265">_DD_ specifies a two-digit day of the month (01 through 31).</span></span>
    
  
-  <span data-ttu-id="6a757-266">_T_ gibt den Buchstaben „T" an.</span><span class="sxs-lookup"><span data-stu-id="6a757-266">_T_ specifies the letter "T".</span></span>
    
  
-  <span data-ttu-id="6a757-p120">_hh_ gibt eine zweiziffrige Stundenangabe an (00-23).</span><span class="sxs-lookup"><span data-stu-id="6a757-p120">_hh_ specifies a two-digits hour (00 through 23); A.M./P.M. indication is not allowed.</span></span>
    
  
-  <span data-ttu-id="6a757-269">_mm_ gibt eine zweiziffrige Minutenangabe an (00-59).</span><span class="sxs-lookup"><span data-stu-id="6a757-269">_mm_ specifies a two-digit minute (00 through 59).</span></span>
    
  
-  <span data-ttu-id="6a757-270">_ss_ gibt eine zweiziffrige Sekundenangabe an (00-59).</span><span class="sxs-lookup"><span data-stu-id="6a757-270">_ss_ specifies a two-digit second (00 through 59).</span></span>
    
  
-  <span data-ttu-id="6a757-p121">_fr_ gibt optional eine Zehntelsekundenangabe an, ss; zwischen 1 und 7, die als Stelle **.** nach dem Komma folgt. Z. B. 27.09.2012T11:57:34.1234567.</span><span class="sxs-lookup"><span data-stu-id="6a757-p121">_fr_ specifies an optional fraction of seconds, ss; between 1 to 7 digits that follows the **.** after the seconds. For example, 2012-09-27T11:57:34.1234567.</span></span>
    
  
<span data-ttu-id="6a757-p122">Alle Datums-/Zeitwerte müssen gemäß der UTC (Coordinated Universal Time) angegeben werden, auch als GMT (Greenwich Mean Time) Zeitzone bekannt. Der UTC-Zeitzonenbezeichner (nachfolgendes „Z") ist optional.</span><span class="sxs-lookup"><span data-stu-id="6a757-p122">All date/time values must be specified according to the UTC (Coordinated Universal Time), also known as GMT (Greenwich Mean Time) time zone. The UTC time zone identifier (a trailing "Z" character) is optional.</span></span>
  
    
    

#### <a name="relevant-date-intervals-supported-by-kql"></a><span data-ttu-id="6a757-276">Von KQL unterstützte relevante Datumsintervalle</span><span class="sxs-lookup"><span data-stu-id="6a757-276">Relevant date intervals supported by KQL</span></span>

<span data-ttu-id="6a757-p123">Mit KQL können Sie Suchabfragen erstellen, die die relative „Tag"-Bereichsabfrage mit reservierten Schlüsselwörtern unterstützt, siehe Tabelle 4. Verwenden Sie doppelte Anführungszeichen ("") für Datumsintervalle, zwischen denen sich Leerzeichen befinden.</span><span class="sxs-lookup"><span data-stu-id="6a757-p123">KQL enables you to build search queries that support relative "day" range query, with reserved keywords as shown in Table 4. Use double quotation marks ("") for date intervals with a space between their names.</span></span>
  
    
    


|<span data-ttu-id="6a757-279">**Name des Datumsintervalls**</span><span class="sxs-lookup"><span data-stu-id="6a757-279">**Name of date interval**</span></span>|<span data-ttu-id="6a757-280">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="6a757-280">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6a757-281">heute</span><span class="sxs-lookup"><span data-stu-id="6a757-281">today</span></span>  <br/> |<span data-ttu-id="6a757-282">Stellt den Zeitraum vom Anfang des aktuellen Tags bis zum Ende des aktuellen Tags dar.</span><span class="sxs-lookup"><span data-stu-id="6a757-282">Represents the time from the beginning of the current day until the end of the current day.</span></span>  <br/> |
|<span data-ttu-id="6a757-283">yesterday</span><span class="sxs-lookup"><span data-stu-id="6a757-283">yesterday</span></span>  <br/> |<span data-ttu-id="6a757-284">Stellt den Zeitraum vom Anfang des Tags bis zum Ende des Tags, der vor dem aktuellen Tag liegt, dar.</span><span class="sxs-lookup"><span data-stu-id="6a757-284">Represents the time from the beginning of the day until the end of the day that precedes the current day.</span></span>  <br/> |
|<span data-ttu-id="6a757-285">this week</span><span class="sxs-lookup"><span data-stu-id="6a757-285">this week</span></span>  <br/> |<span data-ttu-id="6a757-p124">Stellt den Zeitraum zwischen dem Anfang der aktuellen Woche und dem Ende der aktuellen Woche dar. Die Kultur, in der der Abfragetext formuliert wurde, wird dabei berücksichtigt, um den ersten Tag der Woche zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="6a757-p124">Represents the time from the beginning of the current week until the end of the current week. The culture in which the query text was formulated is taken into account to determine the first day of the week.</span></span>  <br/> |
|<span data-ttu-id="6a757-288">this month</span><span class="sxs-lookup"><span data-stu-id="6a757-288">this month</span></span>  <br/> |<span data-ttu-id="6a757-289">Stellt den Zeitraum vom Anfang des aktuellen Monats bis zum Ende des aktuellen Monats dar.</span><span class="sxs-lookup"><span data-stu-id="6a757-289">Represents the time from the beginning of the current month until the end of the current month.</span></span>  <br/> |
|<span data-ttu-id="6a757-290">last month</span><span class="sxs-lookup"><span data-stu-id="6a757-290">last month</span></span>  <br/> |<span data-ttu-id="6a757-291">Stellt den gesamten Monat dar, der vor dem aktuellen Monat liegt.</span><span class="sxs-lookup"><span data-stu-id="6a757-291">Represents the entire month that precedes the current month.</span></span>  <br/> |
|<span data-ttu-id="6a757-292">this year</span><span class="sxs-lookup"><span data-stu-id="6a757-292">this year</span></span>  <br/> |<span data-ttu-id="6a757-293">Stellt den Zeitraum vom Anfang des aktuellen Jahres bis zum Ende des aktuellen Jahres dar.</span><span class="sxs-lookup"><span data-stu-id="6a757-293">Represents the time from the beginning of the current year until the end of the current year.</span></span>  <br/> |
|<span data-ttu-id="6a757-294">last year</span><span class="sxs-lookup"><span data-stu-id="6a757-294">last year</span></span>  <br/> |<span data-ttu-id="6a757-295">Stellt das gesamte Jahr dar, das vor dem aktuellen Jahr liegt.</span><span class="sxs-lookup"><span data-stu-id="6a757-295">Represents the entire year that precedes the current year.</span></span>  <br/> |
   

### <a name="using-multiple-property-restrictions-within-a-kql-query"></a><span data-ttu-id="6a757-296">Verwenden von mehreren Eigenschaftseinschränkungen innerhalb einer KQL-Abfrage</span><span class="sxs-lookup"><span data-stu-id="6a757-296">Using multiple property restrictions within a KQL query</span></span>

<span data-ttu-id="6a757-p125">Suche in SharePoint unterstützt die Verwendung von mehreren Eigenschaftseinschränkungen innerhalb der gleichen KQL-Abfrage. Sie können entweder die gleiche Eigenschaft für mehrere Eigenschaftseinschränkungen verwenden oder für jede Eigenschaftseinschränkung eine andere Eigenschaft nutzen.</span><span class="sxs-lookup"><span data-stu-id="6a757-p125">Search in SharePoint supports the use of multiple property restrictions within the same KQL query. You can use either the same property for more than one property restriction, or a different property for each property restriction.</span></span> 
  
    
    
<span data-ttu-id="6a757-p126">Wenn Sie mehrere Instanzen der gleichen Eigenschaftseinschränkung verwenden, basieren die Übereinstimmung auf einer Verbindung der Eigenschaftseinschränkungen in der KQL-Abfrage. Die Übereinstimmungen enthalten von John Smith oder Jane Smith verfasste Inhaltselemente, siehe folgendes Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6a757-p126">When you use multiple instances of the same property restriction, matches are based on the union of the property restrictions in the KQL query. Matches would include content items authored by John Smith or Jane Smith, as follows:</span></span>
  
    
    
 `author:"John Smith" author:"Jane Smith"`
  
    
    
<span data-ttu-id="6a757-301">Diese Funktion entspricht der Verwendung des booleschen Operators **OR**, siehe folgendes Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6a757-301">This functionally is the same as using the **OR** Boolean operator, as follows:</span></span>
  
    
    
 `author:"John Smith" OR author:"Jane Smith"`
  
    
    
<span data-ttu-id="6a757-302">Wenn Sie verschiedene Eigenschaftseinschränkungen verwenden, basieren die Übereinstimmungen auf einer Schnittmenge der Eigenschaftseinschränkungen in der KQL-Abfrage, siehe folgendes Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6a757-302">When you use different property restrictions, matches are based on an intersection of the property restrictions in the KQL query, as follows:</span></span>
  
    
    
 `author:"John Smith" filetype:docx`
  
    
    
<span data-ttu-id="6a757-p127">Übereinstimmungen würden von John Smith verfasste Microsoft Word-Dokumente enthalten. Diese Funktion entspricht der Verwendung des booleschen Operators **AND**, siehe folgendes Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6a757-p127">Matches would include Microsoft Word documents authored by John Smith. This is the same as using the **AND** Boolean operator, as follows:</span></span>
  
    
    
 `author:"John Smith" AND filetype:docx`
  
    
    

## <a name="kql-operators-for-complex-queries"></a><span data-ttu-id="6a757-305">KQL-Operatoren für komplexe Abfragen</span><span class="sxs-lookup"><span data-stu-id="6a757-305">KQL operators for complex queries</span></span>
<span data-ttu-id="6a757-306"><a name="kql_operators"> </a></span><span class="sxs-lookup"><span data-stu-id="6a757-306"></span></span>

<span data-ttu-id="6a757-307">Die KQL-Syntax enthält mehrere Operatoren, die Sie zum Erstellen komplexer Abfragen verwenden können.</span><span class="sxs-lookup"><span data-stu-id="6a757-307">KQL syntax includes several operators that you can use to construct complex queries.</span></span> 
  
    
    

### <a name="boolean-operators"></a><span data-ttu-id="6a757-308">Boolesche Operatoren</span><span class="sxs-lookup"><span data-stu-id="6a757-308">Boolean operators</span></span>

<span data-ttu-id="6a757-p128">Sie können boolesche Operatoren verwenden, um die Suche zu erweitern oder einzugrenzen. Sie können boolesche Operatoren in KQL-Abfragen mit Freitext-Ausdrücken und Eigenschaftseinschränkungen verwenden. In Tabelle 5 sind die unterstützten booleschen Operatoren aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="6a757-p128">You use Boolean operators to broaden or narrow your search. You can use Boolean operators with free text expressions and property restrictions in KQL queries. Table 5 lists the supported Boolean operators.</span></span>
  
    
    

<span data-ttu-id="6a757-312">**Tabelle 5: In KQL unterstützte boolesche Operatoren**</span><span class="sxs-lookup"><span data-stu-id="6a757-312">**Table 5. Boolean operators supported in KQL**</span></span>


|<span data-ttu-id="6a757-313">**Operator**</span><span class="sxs-lookup"><span data-stu-id="6a757-313">**Operator**</span></span>|<span data-ttu-id="6a757-314">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="6a757-314">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6a757-315">**AND**</span><span class="sxs-lookup"><span data-stu-id="6a757-315">**AND**</span></span> <br/> |<span data-ttu-id="6a757-p129">Gibt Suchergebnisse zurück, die alle Freitext-Ausdrücke oder Eigenschaftseinschränkungen enthält, die mit dem Operator **AND** angegeben wurden. Sie müssen vor und nach dem **AND**-Operator einen gültigen Freitext-Ausdruck und/oder eine gültige Eigenschaftseinschränkung angeben. Diese Funktion entspricht der Verwendung des „+"-Zeichens.  </span><span class="sxs-lookup"><span data-stu-id="6a757-p129">Returns search results that include all of the free text expressions, or property restrictions specified with the **AND** operator. You must specify a valid free text expression and/or a valid property restriction both preceding and following the **AND** operator. This is the same as using the plus ("+") character. </span></span><br/> |
|<span data-ttu-id="6a757-319">**NOT**</span><span class="sxs-lookup"><span data-stu-id="6a757-319">**NOT**</span></span> <br/> |<span data-ttu-id="6a757-p130">Gibt Suchergebnisse zurück, in denen die angegebenen Freitext-Ausdrücke oder Eigenschaftseinschränkungen nicht enthalten sind. Sie müssen nach dem Operator **NOT** einen gültigen Freitext-Ausdruck und/oder eine gültige Eigenschaftseinschränkung angeben. Diese Funktion entspricht der Verwendung des „-"-Zeichens.</span><span class="sxs-lookup"><span data-stu-id="6a757-p130">Returns search results that don't include the specified free text expressions or property restrictions. You must specify a valid free text expression and/or a valid property restriction following the **NOT** operator. This is the same as using the minus ("-") character. </span></span><br/> |
|<span data-ttu-id="6a757-323">**ODER**</span><span class="sxs-lookup"><span data-stu-id="6a757-323">**OR**</span></span> <br/> |<span data-ttu-id="6a757-p131">Gibt Suchergebnisse zurück, die eine oder mehrere der angegebenen Freitext-Ausdrücke oder Eigenschaftseinschränkungen enthält. Sie müssen vor und nach dem **OR**-Operator einen gültigen Freitext-Ausdruck und/oder eine gültige Eigenschaftseinschränkung angeben.</span><span class="sxs-lookup"><span data-stu-id="6a757-p131">Returns search results that include one or more of the specified free text expressions or property restrictions. You must specify a valid free text expression and/or a valid property restriction both preceding and following the **OR** operator. </span></span><br/> |
   

  
    
    

### <a name="proximity-operators"></a><span data-ttu-id="6a757-326">Näherungsoperatoren</span><span class="sxs-lookup"><span data-stu-id="6a757-326">Proximity operators</span></span>

<span data-ttu-id="6a757-p132">Sie können Näherungsoperatoren verwenden, um die Ergebnisse abzugleichen, bei denen die Suchbegriffe nah beieinander auftauchen. Näherungsoperatoren können nur mit Freitext-Ausdrücken verwendet werden; mit Eigenschaftseinschränkungen in KQL-Abfragen werden sie nicht unterstützt. Es gibt zwei Näherungsoperatoren: **NEAR** und **ONEAR**.</span><span class="sxs-lookup"><span data-stu-id="6a757-p132">You use proximity operators to match the results where the specified search terms are within close proximity to each other. Proximity operators can be used with free-text expressions only; they are not supported with property restrictions in KQL queries. There are two proximity operators: **NEAR** and **ONEAR**.</span></span>
  
    
    

#### <a name="near-operator"></a><span data-ttu-id="6a757-330">NEAR-Operator</span><span class="sxs-lookup"><span data-stu-id="6a757-330">NEAR operator</span></span>

<span data-ttu-id="6a757-p133">Der **NEAR**-Operator gleicht die Ergebnisse ab, bei denen die Suchbegriffe nah beieinander auftauchen, ohne dabei die Reihenfolge der Begriffe einhalten zu müssen. Die Syntax für **NEAR** lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="6a757-p133">The **NEAR** operator matches the results where the specified search terms are within close proximity to each other, without preserving the order of the terms. The syntax for **NEAR** is as follows:</span></span>
  
    
    
 `<expression> NEAR(n=4) <expression>`
  
    
    
<span data-ttu-id="6a757-p134">Dabei stellt  _n_ einen optionalen Parameter dar, der den maximalen Abstand zwischen den Begriffen angibt. Der Wert _n_ ist eine ganze Zahl >= 0 mit einem Standardwert von **8**.</span><span class="sxs-lookup"><span data-stu-id="6a757-p134">Where  _n_ is an optional parameter that indicates maximum distance between the terms. The value of _n_ is an integer >= 0 with a default of **8**.</span></span>
  
    
    
<span data-ttu-id="6a757-335">Der Parameter  _n_ kann als `n=v` angegeben werden, dabei stellt _v_ den Wert dar, oder gekürzt _v_; z. B.  `NEAR(4)`, dabei beträgt  _v_ 4.</span><span class="sxs-lookup"><span data-stu-id="6a757-335">The parameter  _n_ can be specified as `n=v` where _v_ represents the value, or shortened to only _v_; such as  `NEAR(4)` where _v_ is 4.</span></span>
  
    
    
<span data-ttu-id="6a757-336">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6a757-336">For example:</span></span>
  
    
    
 `"acquisition" NEAR "debt"`
  
    
    
<span data-ttu-id="6a757-p135">Diese Abfrage gleicht Elemente ab, bei denen die Begriffe „Akquirierung" und „Forderung" im gleichen Element auftreten. Dabei wird eine Instanz „Akquirierung" gefolgt von bis zu acht weiteren Begriffen und anschließend folgt der Begriff „Forderung"; oder umgekehrt. Die Reihenfolge der Begriffe ist für den Abgleich nicht relevant.</span><span class="sxs-lookup"><span data-stu-id="6a757-p135">This query matches items where the terms "acquisition" and "debt" appear within the same item, where an instance of "acquisition" is followed by up to eight other terms, and then an instance of the term "debt"; or vice versa. The order of the terms is not significant for the match.</span></span>
  
    
    
<span data-ttu-id="6a757-p136">Wenn ein geringerer Abstand zwischen den Begriffen liegen soll, können Sie ihn angeben. Mit der folgenden Abfrage werden Elemente abgeglichen, bei denen die Begriffe „Akquirierung" und „Forderung" innerhalb des gleichen Elements auftreten, dabei beträgt der Abstand zwischen den Begriffen maximal 3. Die Reihenfolge der Begriffe hat keine Auswirkungen auf den Abgleich.</span><span class="sxs-lookup"><span data-stu-id="6a757-p136">If you need a smaller distance between the terms, you can specify it. The following query matches items where the terms "acquisition" and "debt" appear within the same item, where a maximum distance of 3 between the terms. Once again the order of the terms does not affect the match.</span></span>
  
    
    
 `"acquisition" NEAR(n=3) "debt"`
  
    
    

> <span data-ttu-id="6a757-342">**Hinweis:** In SharePoint behält der **NEAR**-Operator nicht mehr die Reihenfolge der Token bei.</span><span class="sxs-lookup"><span data-stu-id="6a757-342">**Note:** In SharePoint the **NEAR** operator no longer preserves the ordering of tokens.</span></span> <span data-ttu-id="6a757-343">Darüber hinaus erhält der **NEAR**-Operator jetzt einen optionalen Parameter, der einen maximalen Tokenabstand angibt.</span><span class="sxs-lookup"><span data-stu-id="6a757-343">In addition, the **NEAR** operator now receives an optional parameter that indicates maximum token distance.</span></span> <span data-ttu-id="6a757-344">Der Standardwert ist jedoch weiterhin **8**.</span><span class="sxs-lookup"><span data-stu-id="6a757-344">However, the default value is still **8**.</span></span> <span data-ttu-id="6a757-345">Wenn Sie das vorherige Verhalten verwenden müssen, verwenden Sie stattdessen **ONEAR**.</span><span class="sxs-lookup"><span data-stu-id="6a757-345">If you must use the previous behavior, use **ONEAR** instead.</span></span>
  
    
    


#### <a name="onear-operator"></a><span data-ttu-id="6a757-346">ONEAR-Operator</span><span class="sxs-lookup"><span data-stu-id="6a757-346">ONEAR operator</span></span>

<span data-ttu-id="6a757-p138">Der **ONEAR**-Operator gleicht die Ergebnisse ab, bei denen die angegebenen Suchbegriffe nah beieinander auftreten und behält die Reihenfolge der Begriffe bei. Die Syntax für **ONEAR** lautet wie folgt, dabei ist _n_ ein optionaler Parameter, der den maximalen Abstand zwischen den Begriffen angibt. Der Wert _n_ ist eine ganze Zahl >= 0 mit einem Standardwert **8**.</span><span class="sxs-lookup"><span data-stu-id="6a757-p138">The **ONEAR** operator matches the results where the specified search terms are within close proximity to each other, while preserving the order of the terms. The syntax for **ONEAR** is as follows, where _n_ is an optional parameter that indicates maximum distance between the terms. The value of _n_ is an integer >= 0 with a default of **8**.</span></span>
  
    
    
 `<expression> ONEAR(n=4) <expression>`
  
    
    
<span data-ttu-id="6a757-350">Der Parameter  _n_ kann als `n=v` angegeben werden, dabei stellt _v_ den Wert dar, oder gekürzt _v_; z. B.  `ONEAR(4)`, dabei beträgt  _v_ 4.</span><span class="sxs-lookup"><span data-stu-id="6a757-350">The parameter  _n_ can be specified as `n=v` where _v_ represents the value, or shortened to only _v_; such as  `ONEAR(4)` where _v_ is 4.</span></span>
  
    
    
<span data-ttu-id="6a757-p139">Die folgende Abfrage gleicht beispielsweise Elemente ab, in denen die Begriffe „Akquirierung" und „Forderung" innerhalb des gleichen Elements auftauchen, dabei folgen auf eine Instanz „Akquirierung" bis zu acht weitere Begriffe und anschließend eine Instanz des Begriffs „Forderung". Die Reihenfolge der Begriffe **muss** übereinstimmen, damit ein Element zurückgegeben werden kann:</span><span class="sxs-lookup"><span data-stu-id="6a757-p139">For example, the following query matches items where the terms "acquisition" and "debt" appear within the same item, where an instance of "acquisition" is followed by up to eight other terms, and then an instance of the term "debt". The order of the terms **must** match for an item to be returned:</span></span>
  
    
    
 `"acquisition" ONEAR "debt"`
  
    
    
<span data-ttu-id="6a757-p140">Wenn ein kleinerer Abstand zwischen den Begriffen liegen soll, können Sie ihn wie folgt angeben. Diese Abfrage gleicht Elemente ab, in denen die Begriffe „Akquirierung" und „Forderung" innerhalb des gleichen Elements auftauchen, dabei beträgt der maximale Abstand zwischen den Begriffen 3. Die Reihenfolge der Begriffe **muss** übereinstimmen, damit ein Element zurückgegeben werden kann:</span><span class="sxs-lookup"><span data-stu-id="6a757-p140">If you require a smaller distance between the terms, you can specify it as follows. This query matches items where the terms "acquisition" and "debt" appear within the same item, where a maximum distance of 3 between the terms. The order of the terms **must** match for an item to be returned:</span></span>
  
    
    
 `"acquisition" ONEAR(n=3) "debt"`
  
    
    

### <a name="synonym-operators"></a><span data-ttu-id="6a757-356">Synonym-Operatoren</span><span class="sxs-lookup"><span data-stu-id="6a757-356">Synonym operators</span></span>

<span data-ttu-id="6a757-p141">Sie können den Operator **WORDS** verwenden, um anzugeben, dass die Begriffe in der Abfrage Synonyme sind und zurückgegebene Ergebnisse mit einem der angegebenen Begriffe übereinstimmen sollten. Sie können den Operator **WORDS** nur mit Freitext-Ausdrücken verwenden; mit Eigenschaftseinschränkungen in KQL-Abfragen wird er nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="6a757-p141">You use the **WORDS** operator to specify that the terms in the query are synonyms, and that results returned should match either of the specified terms. You can use the **WORDS** operator with free text expressions only; it is not supported with property restrictions in KQL queries.</span></span>
  
    
    
<span data-ttu-id="6a757-p142">Die folgende Beispielabfrage gleicht Ergebnisse ab, die den Begriff „TV" oder den Begriff „Fernsehen" enthalten. Dieses Abgleichverhalten entspricht der Verwendung folgender Abfrage:</span><span class="sxs-lookup"><span data-stu-id="6a757-p142">The following query example matches results that contain either the term "TV" or the term "television". This matching behavior is the same as if you had used the following query:</span></span>
  
    
    
 `WORDS(TV, Television)`
  
    
    
 `TV OR Television`
  
    
    
<span data-ttu-id="6a757-p143">Diese Abfragen unterscheiden sich in der Ergebnisrangfolge. Wenn Sie den Operator **WORDS** verwenden, werden die Begriffe „TV" und „Fernsehen" als Synonyme behandelt, statt als einzelne Begriffe. Deshalb ist die Rangfolge der Instanzen der Begriffe so, als wäre es derselbe Begriff. Ein Inhaltselement, das eine Instanz des Begriffs „Fernsehen" und fünf Instanzen des Begriffs „TV" enthält, erhält die gleiche Rangfolge, als wären sechs Instanzen des Begriffs „TV" im Inhaltselement enthalten.</span><span class="sxs-lookup"><span data-stu-id="6a757-p143">These queries differ in how the results are ranked. When you use the **WORDS** operator, the terms "TV" and "television" are treated as synonyms instead of separate terms. Therefore, instances of either term are ranked as if they were the same term. For example, a content item that contained one instance of the term "television" and five instances of the term "TV" would be ranked the same as a content item with six instances of the term "TV".</span></span>
  
    
    

### <a name="wildcard-operator"></a><span data-ttu-id="6a757-365">Platzhalterzeichen</span><span class="sxs-lookup"><span data-stu-id="6a757-365">Wildcard operator</span></span>

<span data-ttu-id="6a757-366">Verwenden Sie das Platzhalterzeichen Sternchen (" ** \* ** "), um die Präfix-Anpassung zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="6a757-366">You use the wildcard operator—the asterisk character (" **\*** ")—to enable prefix matching.</span></span> <span data-ttu-id="6a757-367">In Ihrer Anfrage können Sie einen Teil des Wortes angeben. Beginnen Sie mit dem Anfang des Wortes gefolgt vom Platzhalterzeichen. </span><span class="sxs-lookup"><span data-stu-id="6a757-367">You use the wildcard operator—the asterisk character ("*")—to enable prefix matching. You can specify part of a word, from the beginning of the word, followed by the wildcard operator, in your keyword query, as follows.</span></span> <span data-ttu-id="6a757-368">Bei dieser Abfrage wird nach Übereinstimmungen gesucht, die Ausdrücke enthalten, die mit "serv" beginnen, gefolgt von null oder mehr Zeichen, wie z. B. "serve", "server", "service" usw.</span><span class="sxs-lookup"><span data-stu-id="6a757-368">This keyword query would match results that include terms beginning with "serv", followed by zero or more characters, such as serve, server, service, and so on.</span></span>
  
    
    
 `serv*`
  
    
    

### <a name="inclusion-and-exclusion-operators"></a><span data-ttu-id="6a757-369">Ein- und Ausschluss-Operatoren</span><span class="sxs-lookup"><span data-stu-id="6a757-369">Inclusion and exclusion operators</span></span>

<span data-ttu-id="6a757-370">Sie können angeben, ob die zurückgegebenen Ergebnisse Inhalte enthalten oder ausschließen sollen, die mit dem im Freitext-Ausdruck oder in der Eigenschaftseinschränkung angegebenen Wert übereinstimmen, indem Sie Inklusions- oder Ausschluss-Operatoren verwenden, siehe Tabelle 6.</span><span class="sxs-lookup"><span data-stu-id="6a757-370">You can specify whether the results that are returned should include or exclude content that matches the value specified in the free text expression or the property restriction by using the inclusion and exclusion operators, described in Table 6.</span></span>
  
    
    

<span data-ttu-id="6a757-371">**Tabelle 6: Operatoren zum Einschließen und Ausschließen von Inhalten in Ergebnissen**</span><span class="sxs-lookup"><span data-stu-id="6a757-371">**Table 6. Operators for including and excluding content in results**</span></span>


|<span data-ttu-id="6a757-372">**Name**</span><span class="sxs-lookup"><span data-stu-id="6a757-372">**Name**</span></span>|<span data-ttu-id="6a757-373">**Operator**</span><span class="sxs-lookup"><span data-stu-id="6a757-373">**Operator**</span></span>|<span data-ttu-id="6a757-374">**Verhalten**</span><span class="sxs-lookup"><span data-stu-id="6a757-374">**Behavior**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="6a757-375">Inklusion</span><span class="sxs-lookup"><span data-stu-id="6a757-375">Inclusion</span></span>  <br/> |<span data-ttu-id="6a757-376">" **+** "</span><span class="sxs-lookup"><span data-stu-id="6a757-376"></span></span> <br/> |<span data-ttu-id="6a757-377">Schließt Inhalte mit Werten ein, die mit der Inklusion übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="6a757-377">Includes content with values that match the inclusion.</span></span>  <br/> <span data-ttu-id="6a757-p145">Wenn kein Zeichen angegeben wurde, verhält sich die Abfrage standardmäßig so. Diese Funktion entspricht der Verwendung des **AND**-Operators.</span><span class="sxs-lookup"><span data-stu-id="6a757-p145">This is the default behavior if no character is specified. This is the same as using the **AND** operator. </span></span><br/> |
|<span data-ttu-id="6a757-380">Ausschluss</span><span class="sxs-lookup"><span data-stu-id="6a757-380">Exclusion</span></span>  <br/> |<span data-ttu-id="6a757-381">" **-** "</span><span class="sxs-lookup"><span data-stu-id="6a757-381"></span></span> <br/> |<span data-ttu-id="6a757-p146">Schließt Inhalte mit Werten ein, die mit der Exklusion übereinstimmen. Diese Funktion entspricht der Verwendung des Operators **NOT**.</span><span class="sxs-lookup"><span data-stu-id="6a757-p146">Excludes content with values that match the exclusion. This is the same as using the **NOT** operator. </span></span><br/> |
   

### <a name="dynamic-ranking-operator"></a><span data-ttu-id="6a757-384">Dynamischer Rangfolge-Operator</span><span class="sxs-lookup"><span data-stu-id="6a757-384">Dynamic ranking operator</span></span>

<span data-ttu-id="6a757-p147">Sie können den Operator **XRANK** verwenden, um den dynamischen Rang der Elemente basierend auf bestimmten Vorkommnissen von Begriffen im _match expression_ verstärken, ohne die Abfrage dahingehend zu verändern, welche Elemente mit der Abfrage übereinstimmen. Ein **XRANK**-Ausdruck enthält eine Komponente, die abgeglichen werden muss, der  _match expression_ und eine oder mehrere Komponenten, die nur in der dynamischen Ranfolge relevant sind und den _rank expression_. Es muss mindestens **einer** der Parameter angegeben werden, abgesehen von _n_, damit ein **XRANK**-Ausdruck gültig ist.</span><span class="sxs-lookup"><span data-stu-id="6a757-p147">You use the **XRANK** operator to boost the dynamic rank of items based on certain term occurrences within the _match expression_, without changing which items match the query. An **XRANK** expression contains one component that must be matched, the _match expression_, and one or more components that contribute only to dynamic ranking, the  _rank expression_. At least **one** of the parameters, excluding _n_, must be specified for an **XRANK** expression to be valid.</span></span>
  
    
    
 <span data-ttu-id="6a757-p148">_Match expressions_ kann ein beliebiger gültiger KQL-Ausdruck sein, einschließlich verschachtelter **XRANK**-Ausdrücke.  _Rank expressions_ kann ein beliebiger gültiger KQL-Ausdruck ohne **XRANK**-Ausdrücke sein. Wenn Ihre KQL-Abfragen über mehrere **XRANK**-Operatoren verfügt, wird der endgültige dynamische Rangfolgewert als Summe der Verstärkungen aller **XRANK**-Operatoren berechnet.</span><span class="sxs-lookup"><span data-stu-id="6a757-p148">_Match expressions_ may be any valid KQL expression, including nested **XRANK** expressions. _Rank expressions_ may be any valid KQL expression without **XRANK** expressions. If your KQL queries have multiple **XRANK** operators, the final dynamic rank value is calculated as a sum of boosts across all **XRANK** operators.</span></span>
  
    
    

> <span data-ttu-id="6a757-391">**Hinweis:** Verwenden Sie Klammern, um die Reihenfolge der Berechnungen für die KQL-Abfragen explizit anzugeben, die über mehr als einen **XRANK**-Operator auf der gleichen Ebene verfügen.</span><span class="sxs-lookup"><span data-stu-id="6a757-391">**Note** Use parenthesis to explicitly indicate the order of computation for KQL queries that have more than one **XRANK** operator at the same level.</span></span>
  
    
    

<span data-ttu-id="6a757-392">Sie können den **XRANK**-Operator in der folgenden Syntax verwenden:</span><span class="sxs-lookup"><span data-stu-id="6a757-392">You can use the **XRANK** operator in the following syntax:</span></span>
  
    
    
 `<match expression> XRANK(cb=100, rb=0.4, pb=0.4, avgb=0.4, stdb=0.4, nb=0.4, n=200) <rank expression>`
  
    
    
<span data-ttu-id="6a757-393">Die Berechnung der dynamischen Rangfolge des **XRANK**-Operators basiert auf dieser Formel:</span><span class="sxs-lookup"><span data-stu-id="6a757-393">The **XRANK** operator's dynamic ranking calculation is based on this formula:</span></span>
  
    
    

  
    
    
![Formel für XRANK-Operator](../images/XRANKFormula.gif)
  
    
    
<span data-ttu-id="6a757-395">In Tabelle 7 sind die verfügbaren Grundparameter für den **XRANK**-Operator aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="6a757-395">Table 7 lists the basic parameters available for the **XRANK** operator.</span></span>
  
    
    

<span data-ttu-id="6a757-396">**Tabelle 7: XRANK-Operatorparameter**</span><span class="sxs-lookup"><span data-stu-id="6a757-396">**Table 7. XRANK operator parameters**</span></span>


|<span data-ttu-id="6a757-397">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a757-397">**Parameter**</span></span>|<span data-ttu-id="6a757-398">**Wert**</span><span class="sxs-lookup"><span data-stu-id="6a757-398">**Value**</span></span>|<span data-ttu-id="6a757-399">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="6a757-399">**Description**</span></span>|
|:-----|:-----|:-----|
| _n_ <br/> | <span data-ttu-id="6a757-400">_<integer_value>_</span><span class="sxs-lookup"><span data-stu-id="6a757-400">_<integer_value>_</span></span> <br/> |<span data-ttu-id="6a757-401">Gibt die Anzahl der Ergebnisse an, aus denen die Statistik berechnet werden soll.</span><span class="sxs-lookup"><span data-stu-id="6a757-401">Specifies the number of results to compute statistics from.</span></span>  <br/> <span data-ttu-id="6a757-402">Dieser Parameter hat keine Auswirkungen auf die Anzahl der Ergebnisse, die durch die dynamische Rangfolge hinzu kommen; es handelt sich dabei lediglich um eine Methode zum Ausschließen irrelevanter Elemente aus den Berechnungen der Statistik.</span><span class="sxs-lookup"><span data-stu-id="6a757-402">This parameter does not affect the number of results that the dynamic rank contributes to; it is just a means to exclude irrelevant items from the statistics calculations.</span></span>  <br/> <span data-ttu-id="6a757-p149"> Standardwert: **0**. Ein Nullwert trägt die Semantik *aller Dokumente*  . </span><span class="sxs-lookup"><span data-stu-id="6a757-p149">Default: **0**. A zero value carries the semantic of *all documents*  . </span></span><br/> |
| <span data-ttu-id="6a757-405">_nb_</span><span class="sxs-lookup"><span data-stu-id="6a757-405">_nb_</span></span> <br/> | <span data-ttu-id="6a757-406">_<float_value>_</span><span class="sxs-lookup"><span data-stu-id="6a757-406">_<float_value>_</span></span> <br/> |<span data-ttu-id="6a757-p150">Der  _nb_-Parameter verweist auf die normale Verstärkung. Dieser Parameter gibt den Faktor an, der mit dem Produkt der Abweichung und der Durchschnittsbewertung der Rangwerte der Ergebnisgruppe multipliziert wird.</span><span class="sxs-lookup"><span data-stu-id="6a757-p150">The  _nb_ parameter refers to normalized boost. This parameter specifies the factor that is multiplied with the product of the variance and average score of the rank values of the results set. </span></span><br/>  <span data-ttu-id="6a757-409">_f_ in der XRANK-Formel.</span><span class="sxs-lookup"><span data-stu-id="6a757-409">_f_ in the XRANK formula.</span></span> <br/> |
   
<span data-ttu-id="6a757-p151">In der Regel ist die normale Verstärkung ( _nb_) der einzige Parameter, der geändert wird. Dieser Parameter stellt das benötigte Steuerelement bereit, um ein bestimmtes Element höher oder niedriger zu stufen, ohne dabei die Standardabweichung zu berücksichtigen.</span><span class="sxs-lookup"><span data-stu-id="6a757-p151">Typically, normalized boost,  _nb_, is the only parameter that is modified. This parameter provides the necessary control to promote or demote a particular item, without taking standard deviation into account.</span></span> 
  
    
    
<span data-ttu-id="6a757-p152">Außerdem sind folgende erweiterte Parameter verfügbar. In der Regel werden sie jedoch nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="6a757-p152">The following advanced parameters are also available. However, typically they're not used.</span></span>
  
    
    

<span data-ttu-id="6a757-414">**Tabelle 8: Erweiterte Parameter für XRANK**</span><span class="sxs-lookup"><span data-stu-id="6a757-414">**Table 8. Advanced parameters for XRANK**</span></span>


|<span data-ttu-id="6a757-415">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6a757-415">**Parameter**</span></span>|<span data-ttu-id="6a757-416">**Wert**</span><span class="sxs-lookup"><span data-stu-id="6a757-416">**Value**</span></span>|<span data-ttu-id="6a757-417">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="6a757-417">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="6a757-418">_cb_</span><span class="sxs-lookup"><span data-stu-id="6a757-418">_cb_</span></span> <br/> | <span data-ttu-id="6a757-419">_<float_value>_</span><span class="sxs-lookup"><span data-stu-id="6a757-419">_<float_value>_</span></span> <br/> |<span data-ttu-id="6a757-420">Der  _cb_-Parameter verweist auf die konstante Verstärkung.</span><span class="sxs-lookup"><span data-stu-id="6a757-420">The  _cb_ parameter refers to constant boost.</span></span> <br/> <span data-ttu-id="6a757-421">Standardwert: **0**.</span><span class="sxs-lookup"><span data-stu-id="6a757-421">Default: **0**.</span></span> <br/>  <span data-ttu-id="6a757-422">_a_ in der XRANK-Formel.</span><span class="sxs-lookup"><span data-stu-id="6a757-422">_a_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="6a757-423">_stdb_</span><span class="sxs-lookup"><span data-stu-id="6a757-423">_stdb_</span></span> <br/> | <span data-ttu-id="6a757-424">_<float_value>_</span><span class="sxs-lookup"><span data-stu-id="6a757-424">_<float_value>_</span></span> <br/> |<span data-ttu-id="6a757-425">Der  _stdb_-Parameter verweist auf die Verstärkung der Standardabweichung.</span><span class="sxs-lookup"><span data-stu-id="6a757-425">The  _stdb_ parameter refers to standard deviation boost.</span></span> <br/> <span data-ttu-id="6a757-426">Standardwert: **0**.</span><span class="sxs-lookup"><span data-stu-id="6a757-426">Default: **0**.</span></span> <br/>  <span data-ttu-id="6a757-427">_e_ in der XRANK-Formel.</span><span class="sxs-lookup"><span data-stu-id="6a757-427">_e_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="6a757-428">_avgb_</span><span class="sxs-lookup"><span data-stu-id="6a757-428">_avgb_</span></span> <br/> | <span data-ttu-id="6a757-429">_<float_value>_</span><span class="sxs-lookup"><span data-stu-id="6a757-429">_<float_value>_</span></span> <br/> |<span data-ttu-id="6a757-430">Der  _avgb_-Parameter verweist auf die durchschnittliche Verstärkung.</span><span class="sxs-lookup"><span data-stu-id="6a757-430">The  _avgb_ parameter refers to average boost.</span></span> <br/> <span data-ttu-id="6a757-431">Standardwert: **0**.</span><span class="sxs-lookup"><span data-stu-id="6a757-431">Default: **0**.</span></span> <br/>  <span data-ttu-id="6a757-432">_d_ in der XRANK-Formel.</span><span class="sxs-lookup"><span data-stu-id="6a757-432">_d_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="6a757-433">_rb_</span><span class="sxs-lookup"><span data-stu-id="6a757-433">_rb_</span></span> <br/> | <span data-ttu-id="6a757-434">_<float_value>_</span><span class="sxs-lookup"><span data-stu-id="6a757-434">_<float_value>_</span></span> <br/> |<span data-ttu-id="6a757-p153">Der  _rb_-Parameter verweist auf die Bereichsverstärkung. Dieser Faktor wird mit dem Bereich der Rangfolgewerte in der Ergebnisgruppe multipliziert.</span><span class="sxs-lookup"><span data-stu-id="6a757-p153">The  _rb_ parameter refers to range boost. This factor is multiplied with the range of rank values in the results set. </span></span><br/> <span data-ttu-id="6a757-437">Standardwert: **0**.</span><span class="sxs-lookup"><span data-stu-id="6a757-437">Default: **0**.</span></span> <br/>  <span data-ttu-id="6a757-438">_b_ in der XRANK-Formel.</span><span class="sxs-lookup"><span data-stu-id="6a757-438">_b_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="6a757-439">_pb_</span><span class="sxs-lookup"><span data-stu-id="6a757-439">_pb_</span></span> <br/> | <span data-ttu-id="6a757-440">_<float_value>_</span><span class="sxs-lookup"><span data-stu-id="6a757-440">_<float_value>_</span></span> <br/> |<span data-ttu-id="6a757-p154">Der  _pb_-Parameter verweist auf die Prozentwertverstärkung. Dieser Faktor wird im Vergleich zum Mindestwert des Korpus mit der Rangfolge des Elements multipliziert.</span><span class="sxs-lookup"><span data-stu-id="6a757-p154">The  _pb_ parameter refers to percentage boost. This factor is multiplied with the item's own rank compared to the minimum value in the corpus. </span></span><br/> <span data-ttu-id="6a757-443">Standardwert: **0**.</span><span class="sxs-lookup"><span data-stu-id="6a757-443">Default: **0**.</span></span> <br/>  <span data-ttu-id="6a757-444">_c_ in der XRANK-Formel.</span><span class="sxs-lookup"><span data-stu-id="6a757-444">_c_ in the XRANK formula.</span></span> <br/> |
   

#### <a name="examples"></a><span data-ttu-id="6a757-445">Beispiele</span><span class="sxs-lookup"><span data-stu-id="6a757-445">Examples</span></span>

 <span data-ttu-id="6a757-p155">**Beispiel 1.** Der folgende Ausdruck gleicht Elemente ab, bei denen der Standard-Volltextindex den Begriff „Katze" oder „Hund" enthält. Der Ausdruck erhöht die dynamische Rangfolge der Elemente mit einer konstanten Verstärkung von 100 für Elemente, die zusätzlich den Begriff „Vollblutpferd" enthalten.</span><span class="sxs-lookup"><span data-stu-id="6a757-p155">**Example 1.** The following expression matches items for which the default full-text index contains either "cat" or "dog". The expression increases dynamic rank of those items with a constant boost of 100 for items that also contain "thoroughbred".</span></span>
  
    
    
 `(cat OR dog) XRANK(cb=100) thoroughbred`
  
    
    
 <span data-ttu-id="6a757-p156">**Beispiel 2.** Der folgende Ausdruck gleicht Elemente ab, bei denen der Standard-Volltextindex den Begriff „Katze" oder „Hund" enthält. Der Ausdruck erhöht die dynamische Rangfolge der Elemente mit einer normalen Verstärkung von 1,5 für Elemente, die zusätzlich den Begriff „Vollblutpferd" enthalten.</span><span class="sxs-lookup"><span data-stu-id="6a757-p156">**Example 2.** The following expression matches items for which the default full-text index contains either "cat" or "dog". The expression increases dynamic rank of those items with a normalized boost of 1.5 for items that also contain "thoroughbred".</span></span>
  
    
    
 `(cat OR dog) XRANK(nb=1.5) thoroughbred`
  
    
    
 <span data-ttu-id="6a757-p157">**Beispiel 3.** Der folgende Ausdruck gleicht Elemente ab, bei denen der Standard-Volltextindex den Begriff „Katze" oder „Hund" enthält. Der Ausdruck erhöht die dynamische Rangfolge der Elemente mit einer konstanten Verstärkung von 100 und einer normalen Verstärkung von 1,5, für Elemente, die zusätzlich den Begriff „Vollblutpferd" enthalten.</span><span class="sxs-lookup"><span data-stu-id="6a757-p157">**Example 3.** The following expression matches items for which the default full-text index contains either "cat" or "dog". The expression increases dynamic rank of those items with a constant boost of 100 and a normalized boost of 1.5, for items that also contain "thoroughbred".</span></span>
  
    
    
 `(cat OR dog) XRANK(cb=100, nb=1.5) thoroughbred`
  
    
    
 <span data-ttu-id="6a757-p158">**Beispiel 4.** Der folgende Ausdruck gleicht alle Elemente ab, die den Begriff „Tiere" enthalten und die dynamische Rangfolge wie folgt verstärken:</span><span class="sxs-lookup"><span data-stu-id="6a757-p158">**Example 4.** The following expression matches all items containing the term "animals", and boosts dynamic rank as follows:</span></span>
  
    
    

- <span data-ttu-id="6a757-457">Die dynamische Rangfolge von Elementen, die den Begriff „Hunde" enthalten, werden um 100 Punkte verstärkt.</span><span class="sxs-lookup"><span data-stu-id="6a757-457">Dynamic rank of items that contain the term "dogs" is boosted by 100 points.</span></span>
    
  
- <span data-ttu-id="6a757-458">Die dynamische Rangfolge der Elemente, die den Begriff „Katzen" enthalten, werden um 200 Punkte verstärkt.</span><span class="sxs-lookup"><span data-stu-id="6a757-458">Dynamic rank of items that contain the term "cats" is boosted by 200 points.</span></span>
    
  
- <span data-ttu-id="6a757-459">Die dynamische Rangfolge der Elemente, die die Begriffe „Hunde" und „Katzen" enthalten, werden um 300 Punkte verstärkt.</span><span class="sxs-lookup"><span data-stu-id="6a757-459">Dynamic rank of items that contain both the terms "dogs" and "cats" is boosted by 300 points.</span></span>
    
  
 `(animals XRANK(cb=100) dogs) XRANK(cb=200) cats`
  
    
    

### <a name="parenthesis"></a><span data-ttu-id="6a757-460">Klammer</span><span class="sxs-lookup"><span data-stu-id="6a757-460">Parenthesis</span></span>

<span data-ttu-id="6a757-p159">Sie können verschiedene Teile einer Stichwortabfrage kombinieren, indem Sie eine öffnende „ **(** " und schließende Klammer „ **)** " verwenden. Zu jeder öffnenden Klammer „ **(** " muss eine schließende Klammer „ **)** " vorhanden sein. Ein Leerzeichen vor und nach einer Klammer hat keine Auswirkungen auf die Abfrage.</span><span class="sxs-lookup"><span data-stu-id="6a757-p159">You can combine different parts of a keyword query by using the opening parenthesis character " **(** " and closing parenthesis character " **)** ". Each opening parenthesis " **(** " must have a matching closing parenthesis " **)** ". A white space before or after a parenthesis does not affect the query.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="6a757-464">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6a757-464">Additional resources</span></span>
<span data-ttu-id="6a757-465"><a name="SP15KQL_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6a757-465"></span></span>


-  [<span data-ttu-id="6a757-466">Erstellen von Suchabfragen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6a757-466">Building search queries in SharePoint</span></span>](building-search-queries-in-sharepoint.md)
    
  
