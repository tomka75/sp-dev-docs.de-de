---
title: Suchen Sie in einer Serverfarm mit mehreren geografisch SharePoint Mandanten
ms.date: 11/03/2017
ms.openlocfilehash: 214c1b7ca1a6e2b985f1be780c29ea8b34165ef0
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="search-in-a-multi-geo-sharepoint-tenant"></a><span data-ttu-id="e2af1-102">Suchen Sie in einer Serverfarm mit mehreren geografisch SharePoint Mandanten</span><span class="sxs-lookup"><span data-stu-id="e2af1-102">Search in a Multi-Geo SharePoint tenant</span></span>

> <span data-ttu-id="e2af1-103">**Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.</span><span class="sxs-lookup"><span data-stu-id="e2af1-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="e2af1-104">In einem Mandanten Multi-Geo SharePoint hat jeder Standort Geo eigene Suchindex als auch einen eigenen unabhängigen Suchcenter.</span><span class="sxs-lookup"><span data-stu-id="e2af1-104">In a Multi-Geo SharePoint tenant, each geo location has its own search index, as well as its own independent search center.</span></span> <span data-ttu-id="e2af1-105">Beim Konfigurieren eines Suchcenters verwendet standardmäßig im Suchcenter in der folgenden URL-Muster.</span><span class="sxs-lookup"><span data-stu-id="e2af1-105">By default, when you configure a search center, the search center uses the following URL pattern.</span></span>

```
https://<tenanturl>.sharepoint.com/sites/search
```

<span data-ttu-id="e2af1-106">Im Szenario mit in der folgenden Abbildung dargestellt hat ein Mandanten Multi-Geo drei Geo-Standorte mit einer geografisch standortspezifische Search-URL.</span><span class="sxs-lookup"><span data-stu-id="e2af1-106">In the scenario shown in the following image, a Multi-Geo tenant has three geo locations, each with a geo location-specific search URL.</span></span>

|<span data-ttu-id="e2af1-107">**Geo-Speicherort**</span><span class="sxs-lookup"><span data-stu-id="e2af1-107">**Geo location**</span></span>|<span data-ttu-id="e2af1-108">**Search-URL**</span><span class="sxs-lookup"><span data-stu-id="e2af1-108">**Search URL**</span></span>|
|:---------------|:-------------|
|<span data-ttu-id="e2af1-109">Nordamerika (Standardspeicherort)</span><span class="sxs-lookup"><span data-stu-id="e2af1-109">North America (default location)</span></span>|<span data-ttu-id="e2af1-110">https://contoso.SharePoint.com/search</span><span class="sxs-lookup"><span data-stu-id="e2af1-110">https://contoso.sharepoint.com/search</span></span>|
|<span data-ttu-id="e2af1-111">Europa (Satelliten Speicherort)</span><span class="sxs-lookup"><span data-stu-id="e2af1-111">Europe (satellite location)</span></span>|<span data-ttu-id="e2af1-112">https://contosoeur.SharePoint.com/search</span><span class="sxs-lookup"><span data-stu-id="e2af1-112">https://contosoeur.sharepoint.com/search</span></span>|
|<span data-ttu-id="e2af1-113">Asien (Satelliten Speicherort)</span><span class="sxs-lookup"><span data-stu-id="e2af1-113">Asia (satellite location)</span></span>|<span data-ttu-id="e2af1-114">https://contosoapc.SharePoint.com/search</span><span class="sxs-lookup"><span data-stu-id="e2af1-114">https://contosoapc.sharepoint.com/search</span></span>|


![World Karte zur Erläuterung von Geo Speicherorte in Nordamerika und Europa Asien mit der Mandanten-spezifische Suche Website-URLs](media/multigeo/multigeosearch_intro.png)

<span data-ttu-id="e2af1-116">Suche ist aus Sicht des ein Endbenutzer auf den aktuellen Speicherort des Geo beschränkt.</span><span class="sxs-lookup"><span data-stu-id="e2af1-116">From an end user point of view, search is scoped to the current geo location.</span></span> <span data-ttu-id="e2af1-117">Wenn Benutzer von einer Website gehostet in Nordamerika Suchvorgänge ausführen, sehen sie nur Ergebnisse aus dem Speicherort der Geo North America an.</span><span class="sxs-lookup"><span data-stu-id="e2af1-117">When users perform searches from a site hosted in North America, they will only see results from the North America geo location.</span></span> <span data-ttu-id="e2af1-118">Suchvorgänge aus einer Website in Europa gehostet werden Ergebnisse aus Websites in Europa Geo Speicherort zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="e2af1-118">Searches from a site hosted in Europe will return results from sites in the Europe geo location.</span></span>

> [!NOTE] 
> <span data-ttu-id="e2af1-119">Suche wird in der Zukunft Multi-Geo bewusst sein.</span><span class="sxs-lookup"><span data-stu-id="e2af1-119">In the future, search will be Multi-Geo aware.</span></span> <span data-ttu-id="e2af1-120">Eine Suchabfrage führen Sie von einer beliebigen Stelle in den Mandanten wird allen geografisch Standorten in den Mandanten suchen und kombinierten Ergebnisse zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="e2af1-120">A search query run from any location within the tenant will search all geo locations within the tenant and return combined results.</span></span>

## <a name="working-with-search-programmatically-in-a-multi-geo-tenant"></a><span data-ttu-id="e2af1-121">Arbeiten mit der Suche programmgesteuert in einem Multi-Geo-Mandanten</span><span class="sxs-lookup"><span data-stu-id="e2af1-121">Working with search programmatically in a Multi-Geo tenant</span></span>
<span data-ttu-id="e2af1-122">Programmgesteuertes Arbeiten mit der Suche ähnelt dem durch die Endbenutzer-Suche.</span><span class="sxs-lookup"><span data-stu-id="e2af1-122">Working with search programmatically is similar to the end user search experience.</span></span> <span data-ttu-id="e2af1-123">Wenn Sie eine Suchabfrage ausführen, nur erhalten Ergebnisse für den Speicherort der Geo Sie in denen Sie die Abfrage ausführen.</span><span class="sxs-lookup"><span data-stu-id="e2af1-123">If you perform a search query, you'll only get results for the geo location in which you run the query.</span></span> <span data-ttu-id="e2af1-124">Anwendungen, jedoch mit mehreren geografisch Mandanten Suchvorgänge ausführen können.</span><span class="sxs-lookup"><span data-stu-id="e2af1-124">Your applications can, however, perform Multi-Geo tenant searches.</span></span> <span data-ttu-id="e2af1-125">Zu diesem Zweck durchlaufen die Geo Speicherorte in Ihrem Mandanten, die gleichen Suchabfrage an jedem Standort Geo Problem, und die Ergebnisse verketten.</span><span class="sxs-lookup"><span data-stu-id="e2af1-125">To do this, iterate over the geo locations in your tenant, issue the same search query in each geo location, and then concatenate the results.</span></span>

<span data-ttu-id="e2af1-126">Dieser Ansatz möglicherweise reicht für in einigen Szenarien (beispielsweise sucht nach Websites eines bestimmten Typs).</span><span class="sxs-lookup"><span data-stu-id="e2af1-126">This approach might be sufficient for in some scenarios (for example, searches for sites of a given type).</span></span> <span data-ttu-id="e2af1-127">In einigen Fällen möchten Sie jedoch die Suchergebnissen in der Sortierung nach Relevanz enthalten sein.</span><span class="sxs-lookup"><span data-stu-id="e2af1-127">However, in some cases, you want the search results to be ranked according to relevancy.</span></span> <span data-ttu-id="e2af1-128">Dies ist nicht möglich, wenn Sie mehrere Resultsets haben.</span><span class="sxs-lookup"><span data-stu-id="e2af1-128">You can't do this when you have multiple result sets.</span></span> <span data-ttu-id="e2af1-129">Wenn Ihr Szenario Suche Rangfolge erforderlich sind, müssen Sie warten, bis eine Umgebung mit mehreren geografisch verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="e2af1-129">If your scenario requires search ranking, you will need to wait until a Multi-Geo search experience is available.</span></span>


## <a name="see-also"></a><span data-ttu-id="e2af1-130">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="e2af1-130">See also</span></span>

- [<span data-ttu-id="e2af1-131">Verwalten der Suchcenter in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="e2af1-131">Manage the Search Center in SharePoint Online</span></span>](https://support.office.com/en-us/article/Manage-the-Search-Center-in-SharePoint-Online-174d36e0-2f85-461a-ad9a-8b3f434a4213?ui=en-US&rs=en-US&ad=US)
- [<span data-ttu-id="e2af1-132">Übersicht über die Suche in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="e2af1-132">Overview of search in SharePoint Online</span></span>](https://support.office.com/en-us/article/Overview-of-search-in-SharePoint-Online-479cfd6b-900b-46aa-b497-c13787771d3f?ui=en-US&rs=en-US&ad=US)
