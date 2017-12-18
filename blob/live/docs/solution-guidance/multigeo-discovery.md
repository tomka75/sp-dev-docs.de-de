---
title: "Entdecken Sie eine Multi-Geo-Konfiguration für einen SharePoint-Mandanten"
ms.date: 11/03/2017
ms.openlocfilehash: 2893d093131b17e65ecd30d08aff91d49f29de91
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="discover-a-multi-geo-configuration-for-a-sharepoint-tenant"></a><span data-ttu-id="c773b-102">Entdecken Sie eine Multi-Geo-Konfiguration für einen SharePoint-Mandanten</span><span class="sxs-lookup"><span data-stu-id="c773b-102">Discover a Multi-Geo configuration for a SharePoint tenant</span></span>

> <span data-ttu-id="c773b-103">**Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.</span><span class="sxs-lookup"><span data-stu-id="c773b-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="c773b-104">Bei der Arbeit mit einer SharePoint-Mandanten, müssen Sie erkennen können, ob es sich um einen Mandanten Multi-Geo ist, und identifizieren Sie die standardmäßige und Satelliten Geo-Speicherorte.</span><span class="sxs-lookup"><span data-stu-id="c773b-104">When you're working with a SharePoint tenant, you'll need to be able to detect whether it's a Multi-Geo tenant, and identify the default and satellite geo locations.</span></span> 

<span data-ttu-id="c773b-105">Die folgende Abbildung zeigt einen Multi-Geo-Mandanten mit:</span><span class="sxs-lookup"><span data-stu-id="c773b-105">The following image shows a Multi-Geo tenant with:</span></span>

- <span data-ttu-id="c773b-106">Einen Standardspeicherort Geo in Nordamerika</span><span class="sxs-lookup"><span data-stu-id="c773b-106">A default geo location in North America</span></span>
- <span data-ttu-id="c773b-107">Einen Satelliten Geo Speicherort in Europa</span><span class="sxs-lookup"><span data-stu-id="c773b-107">A satellite geo location in Europe</span></span>
- <span data-ttu-id="c773b-108">Einen Satelliten Geo Speicherort in Asien</span><span class="sxs-lookup"><span data-stu-id="c773b-108">A satellite geo location in Asia</span></span>

![Ein World Karte zur Erläuterung von einen Standardspeicherort Geo in Nordamerika und Satelliten Geo Speicherorte in Europa und Asien, mit sprachspezifischen mandantenadministrator, Stamm und Meine Website-URLs](media/multigeo/multigeodiscovery_intro.png)

<span data-ttu-id="c773b-110">Je nach Szenario können eine oder eine Kombination der folgenden APIs Sie eine Serverfarm mit mehreren geografisch Mandanten-Website zugreifen:</span><span class="sxs-lookup"><span data-stu-id="c773b-110">Depending on your scenario, you can use one or a combination of the following APIs to access a Multi-Geo tenant site:</span></span>

- <span data-ttu-id="c773b-111">**Die Microsoft Graph-API** - Multi-Geo berücksichtigen.</span><span class="sxs-lookup"><span data-stu-id="c773b-111">**The Microsoft Graph API** - Multi-Geo aware.</span></span> <span data-ttu-id="c773b-112">Es wird empfohlen, dass Sie Microsoft Graph auf Access Multi-Geo Mandanten Websites verwenden.</span><span class="sxs-lookup"><span data-stu-id="c773b-112">We recommend that you use Microsoft Graph to access Multi-Geo tenant sites.</span></span> 
- <span data-ttu-id="c773b-113">**SharePoint-CSOM-API** - nicht Multi-Geo berücksichtigen.</span><span class="sxs-lookup"><span data-stu-id="c773b-113">**SharePoint CSOM API** - Not Multi-Geo aware.</span></span> <span data-ttu-id="c773b-114">Je nach Szenario müssen Sie die richtige Geo Zielspeicherort (beispielsweise, um ein Benutzerprofil zugreifen oder Mandanten API Vorgänge ausführen).</span><span class="sxs-lookup"><span data-stu-id="c773b-114">Depending on the scenario, you'll need to target the correct geo location (for example, to access a user profile or perform tenant API operations).</span></span>
- <span data-ttu-id="c773b-115">**SharePoint-REST-API** - normalerweise diese API ist im Kontext einer Website-URL verwendet und, ob der Mandant Multi-Geo ist also kein Faktor.</span><span class="sxs-lookup"><span data-stu-id="c773b-115">**SharePoint REST API** - Typically this API is used in the context of a site URL, and therefore whether the tenant is Multi-Geo is not a factor.</span></span> <span data-ttu-id="c773b-116">Einige Szenarien REST-API (wie Suche oder User Profile) erfordern möglicherweise Anrufe pro Standort Geo tätigen.</span><span class="sxs-lookup"><span data-stu-id="c773b-116">Some REST API scenarios (such as search or user profiles) might require you to make calls per geo location.</span></span>

## <a name="get-multi-geo-tenant-configuration-information"></a><span data-ttu-id="c773b-117">Abrufen von Multi-Geo Mandanten Konfigurationsinformationen</span><span class="sxs-lookup"><span data-stu-id="c773b-117">Get Multi-Geo tenant configuration information</span></span>

<span data-ttu-id="c773b-118">Sie können die Geo Standortinformationen für einen Mandanten mithilfe von Microsoft Graph abrufen.</span><span class="sxs-lookup"><span data-stu-id="c773b-118">You can get the geo location information for a tenant by using Microsoft Graph.</span></span> <span data-ttu-id="c773b-119">Im folgenden Beispiel wird eine Auflistung mit einem Objekt pro Geo-Standort zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="c773b-119">The following example returns a collection with one object per geo location.</span></span>

```
GET https://graph.microsoft.com/v1.0/sites?filter=siteCollection/root%20ne%20null&select=webUrl,siteCollection
```

<span data-ttu-id="c773b-120">Beispielantwort für einen Mandanten Multi-Geo:</span><span class="sxs-lookup"><span data-stu-id="c773b-120">Example response for a Multi-Geo tenant:</span></span>
```JSON
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#sites",
    "value": [
        {
            "webUrl": "https://contoso.sharepoint.com/",
            "siteCollection": {
                "dataLocationCode":"NAM",
                "hostname": "contoso.sharepoint.com"
            }
        },
        {
            "webUrl": "https://contosoeur.sharepoint.com/",
            "siteCollection": {
                "dataLocationCode":"EUR",
                "hostname": "contosoeur.sharepoint.com"
            }
        },
        {
            "webUrl": "https://contosoapc.sharepoint.com/",
            "siteCollection": {
                "dataLocationCode":"APC",
                "hostname": "contosoapc.sharepoint.com"
            }
        }
    ]
}
```

<span data-ttu-id="c773b-121">Finden Sie weitere Informationen finden Sie [MultiGeo.TenantInformationCollection](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.TenantInformationCollection) .</span><span class="sxs-lookup"><span data-stu-id="c773b-121">To learn more, see the [MultiGeo.TenantInformationCollection](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.TenantInformationCollection) sample.</span></span>

> [!NOTE] 
> <span data-ttu-id="c773b-122">Weitere Informationen zu Berechtigungen und wie Sie die Anwendung konfigurieren finden Sie unter [Einrichten einer Serverfarm mit mehreren geografisch beispielanwendung](multigeo-sampleapplicationsetup.md).</span><span class="sxs-lookup"><span data-stu-id="c773b-122">For more information about permissions and how to configure your application, see [Set up a Multi-Geo sample application](multigeo-sampleapplicationsetup.md).</span></span>

## <a name="discover-whether-your-tenant-is-multi-geo"></a><span data-ttu-id="c773b-123">Ermitteln Sie, ob es sich bei Ihrem Mandanten Multi-Geo ist</span><span class="sxs-lookup"><span data-stu-id="c773b-123">Discover whether your tenant is Multi-Geo</span></span> 

<span data-ttu-id="c773b-124">Microsoft Graph können Sie ermitteln, ob ein Mandant Multi-Geo ist, da Anforderungen über Microsoft Graph an mehreren geografisch Mandanten Weitere klicken Sie dann ein Element in der Auflistung zurück.</span><span class="sxs-lookup"><span data-stu-id="c773b-124">You can use Microsoft Graph to discover whether a tenant is Multi-Geo since requests via Microsoft Graph to Multi-Geo tenants return more then one item in the collection.</span></span> <span data-ttu-id="c773b-125">Das folgende Beispiel zeigt die Ergebnisse eines Microsoft Graph-Anrufs auf einen einzelnen Geo-Mandanten.</span><span class="sxs-lookup"><span data-stu-id="c773b-125">The following example shows the results of a Microsoft Graph call to a single-geo tenant.</span></span>

<!-- Not sure where the output for a Multi-Geo tenant is. Provide a link? -->

```
GET https://graph.microsoft.com/v1.0/sites?filter=siteCollection/root%20ne%20null&select=webUrl,siteCollection
```

<span data-ttu-id="c773b-126">Beispielantwort für einen einzelnen Geo-Mandanten:</span><span class="sxs-lookup"><span data-stu-id="c773b-126">Example response for a single-geo tenant:</span></span>
```JSON
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#sites",
    "value": [
        {
            "webUrl": "https://singlegeotest.sharepoint.com/",
            "siteCollection": {
                "dataLocationCode":"",
                "hostname": "singlegeotest.sharepoint.com"
            }
        }
    ]
}
```

## <a name="see-also"></a><span data-ttu-id="c773b-127">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="c773b-127">See also</span></span>

- [<span data-ttu-id="c773b-128">Developercenter für Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="c773b-128">Microsoft Graph developer center</span></span>](https://developer.microsoft.com/en-us/graph)
- [<span data-ttu-id="c773b-129">Microsoft Graph-Dokumentation</span><span class="sxs-lookup"><span data-stu-id="c773b-129">Microsoft Graph documentation</span></span>](https://developer.microsoft.com/en-us/graph/docs/concepts/overview)
- [<span data-ttu-id="c773b-130">Diagramm-Explorer</span><span class="sxs-lookup"><span data-stu-id="c773b-130">Graph Explorer</span></span>](https://developer.microsoft.com/en-us/graph/graph-explorer)
