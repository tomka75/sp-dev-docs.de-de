---
title: Erstellen von Suchabfragen in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c4372fcc-4574-4c81-a345-a1bb282ca8f7
ms.openlocfilehash: d2dfcbbe782057d012f72ca05328316638db635f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="building-search-queries-in-sharepoint"></a><span data-ttu-id="43ea2-102">Erstellen von Suchabfragen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="43ea2-102">Building search queries in SharePoint</span></span>
<span data-ttu-id="43ea2-103">Hier erhalten Sie Informationen zur Suchsyntax, die in SharePoint zum Erstellen von Abfrageregeln und Suchabfragen unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="43ea2-103">Learn about the search syntax supported in SharePoint for building query rules and search queries.</span></span>
## <a name="supported-search-syntax-in-sharepoint-for-building-search-queries"></a><span data-ttu-id="43ea2-104">Unterstützte Suchsyntax in SharePoint zum Erstellen von Suchabfragen</span><span class="sxs-lookup"><span data-stu-id="43ea2-104">Supported search syntax in SharePoint for building search queries</span></span>
<span data-ttu-id="43ea2-105"><a name="SP15Buildquery_support"> </a></span><span class="sxs-lookup"><span data-stu-id="43ea2-105"><a name="SP15Buildquery_support"> </a></span></span>

<span data-ttu-id="43ea2-106">Die SharePoint-Suche unterstützt die KQL- (Keyword Query Language) und FQL-Suchsyntax (FAST Query Language) zum Erstellen von Suchabfragen.</span><span class="sxs-lookup"><span data-stu-id="43ea2-106">SharePoint search supports Keyword Query Language (KQL) and FAST Query Language (FQL) search syntax for building search queries.</span></span>
  
    
    
 <span data-ttu-id="43ea2-107">**Keyword Query Language (KQL)**</span><span class="sxs-lookup"><span data-stu-id="43ea2-107">**Keyword Query Language (KQL)**</span></span>
  
    
    
<span data-ttu-id="43ea2-p101">KQL ist die Standardabfragesprache für die Erstellung von Suchabfragen. Mithilfe von KQL geben Sie die Suchbegriffe oder die Eigenschaftseinschränkungen an, die an den SharePoint-Suchdienst übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="43ea2-p101">KQL is the default query language for building search queries. Using KQL, you specify the search terms or property restrictions that are passed to the SharePoint search service.</span></span>
  
    
    
 <span data-ttu-id="43ea2-110">**FAST Query Language (FQL)**</span><span class="sxs-lookup"><span data-stu-id="43ea2-110">**FAST Query Language (FQL)**</span></span>
  
    
    
<span data-ttu-id="43ea2-p102">Bei FQL handelt es sich um eine strukturierte Abfragesprache, die erweiterte Abfrageoperatoren unterstützt. Mithilfe von FQL können Sie komplexe Abfragen erstellen, die dem SharePoint-Suchdienst programmgesteuert übergeben werden sollen. FQL ist nicht für Endbenutzer vorgesehen und wird standardmäßig deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="43ea2-p102">FQL is a structured query language that supports advanced query operators. You can use FQL when you want to create complex queries that you want to pass programmatically to the SharePoint search service. FQL isn't intended to be exposed to end users, and is disabled by default.</span></span> 
  
    
    
<span data-ttu-id="43ea2-p103">Verwenden Sie zur Aktivierung von FQL die **EnableFQL**-Eigenschaft. Kopieren Sie dann die Standardergebnisquelle, und ändern Sie die Zeichenfolge für die  `{?{searchTerms} -ContentClass=urn:content-class:SPSPeople}` auf einer der folgenden Ebenen - Suchdienstanwendung (SSA), Websitesammlung oder Website. Dazu müssen Sie eine der folgenden Methoden verwenden:</span><span class="sxs-lookup"><span data-stu-id="43ea2-p103">To enable FQL, use the **EnableFQL** property. Then, copy the default result source and modify the Query Transformation string `{?{searchTerms} -ContentClass=urn:content-class:SPSPeople}`, at one of these levels -- Search Service Application (SSA), Site Collection, or Site -- and in one of the following ways:</span></span>
  
    
    

- <span data-ttu-id="43ea2-p104">Entfernen Sie den KQL-Filter,  `-ContentClass:urn:content-class:SPSPeople`, aus der Abfragetransformation. Die sich ergebende Zeichenfolge für die Abfragetransformation lautet:  `{?{searchTerms}}`</span><span class="sxs-lookup"><span data-stu-id="43ea2-p104">Remove the KQL filter,  `-ContentClass:urn:content-class:SPSPeople`, from the Query Transformation. The resulting Query Transformation string will be:  `{?{searchTerms}}`</span></span>
    
  
- <span data-ttu-id="43ea2-118">Ersetzen Sie die Zeichenfolge für die Abfragetransformation durch ein FQL-Äquivalent wie z. B. `{?andnot({searchTerms},filter(contentclass:"urn:content-class:SPSPeople*"))}`.</span><span class="sxs-lookup"><span data-stu-id="43ea2-118">Replace the Query Transformation string with an FQL equivalent, such as  `{?andnot({searchTerms},filter(contentclass:"urn:content-class:SPSPeople*"))}`.</span></span>
    
  
<span data-ttu-id="43ea2-119">Weitere Informationen zu Ergebnisquellen und deren Funktionsweise finden Sie unter:  [Informationen zu Ergebnisquellen](http://office.microsoft.com/de-DE/support/sharepoint/sharepointsearch/understanding-result-sources-HA102848849.aspx) und [Konfigurieren der Ergebnisquellen für die Suche in SharePoint](http://technet.microsoft.com/de-DE/library/jj683115%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="43ea2-119">For more information about result sources and how they work, see to:  [Understanding result sources](http://office.microsoft.com/de-DE/support/sharepoint/sharepointsearch/understanding-result-sources-HA102848849.aspx) and [Configure result sources for search in SharePoint](http://technet.microsoft.com/de-DE/library/jj683115%28v=office.15%29.aspx).</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="43ea2-120">Inhalt dieses Abschnitts</span><span class="sxs-lookup"><span data-stu-id="43ea2-120">In this section</span></span>
<span data-ttu-id="43ea2-121"><a name="SP15Buildquery_support"> </a></span><span class="sxs-lookup"><span data-stu-id="43ea2-121"><a name="SP15Buildquery_support"> </a></span></span>


-  [<span data-ttu-id="43ea2-122">Syntaxreferenz für die Keyword Query Language (KQL)</span><span class="sxs-lookup"><span data-stu-id="43ea2-122">Keyword Query Language (KQL) syntax reference</span></span>](keyword-query-language-kql-syntax-reference.md)
    
  
-  [<span data-ttu-id="43ea2-123">Syntaxreferenz für FQL (FAST Query Language)</span><span class="sxs-lookup"><span data-stu-id="43ea2-123">FAST Query Language (FQL) syntax reference</span></span>](fast-query-language-fql-syntax-reference.md)
    
  
-  [<span data-ttu-id="43ea2-124">Verwenden der SharePoint-Suchabfrage-APIs</span><span class="sxs-lookup"><span data-stu-id="43ea2-124">Using the SharePoint search Query APIs</span></span>](using-the-sharepoint-search-query-apis.md)
    
  

## <a name="see-also"></a><span data-ttu-id="43ea2-125">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="43ea2-125">See also</span></span>
<span data-ttu-id="43ea2-126"><a name="SP15Buildquery_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="43ea2-126"><a name="SP15Buildquery_addlresources"> </a></span></span>


-  [<span data-ttu-id="43ea2-127">Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="43ea2-127">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="43ea2-128">Übersicht über Abfrageverarbeitung in SharePoint</span><span class="sxs-lookup"><span data-stu-id="43ea2-128">Overview of query processing in SharePoint</span></span>](http://technet.microsoft.com/de-DE/library/jj219620%28v=office.15%29.aspx)
    
  
-  [<span data-ttu-id="43ea2-129">Abfragevariablen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="43ea2-129">Query variables in SharePoint</span></span>](http://technet.microsoft.com/de-DE/library/jj683123.aspx)
    
  

