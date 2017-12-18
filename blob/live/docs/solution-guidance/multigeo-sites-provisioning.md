---
title: Arbeiten mit Websites in einer Umgebung mit mehreren geografisch
ms.date: 11/03/2017
ms.openlocfilehash: 581df53ac1a9527d8078401c90bf472a93849b7d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="working-with-sites-in-a-multi-geo-environment"></a><span data-ttu-id="4f155-102">Arbeiten mit Websites in einer Umgebung mit mehreren geografisch</span><span class="sxs-lookup"><span data-stu-id="4f155-102">Working with sites in a Multi-Geo environment</span></span>

> <span data-ttu-id="4f155-103">**Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.</span><span class="sxs-lookup"><span data-stu-id="4f155-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="4f155-104">SharePoint-Websites können über die standardmäßigen und Satelliten Geo Speicherorte Multi-Geo-Mandanten verteilt werden.</span><span class="sxs-lookup"><span data-stu-id="4f155-104">SharePoint sites can be spread across the default and satellite geo locations of a Multi-Geo tenant.</span></span> <span data-ttu-id="4f155-105">Wenn Ihre benutzerdefinierte Entwicklung (Skript, app, Konsolenanwendung, node.js app) muss Websites bereitstellen, ist es wichtig, die geografisch Speicherorte in Ihrem Mandanten Multi-Geo beachten.</span><span class="sxs-lookup"><span data-stu-id="4f155-105">When your custom development (script, app, console application, node.js app,...) needs to provision sites then it's important to be aware of the geo locations in your Multi-Geo tenant.</span></span> 

### <a name="provisioning-classic-team-sites"></a><span data-ttu-id="4f155-106">Bereitstellung der klassische Teamwebsites</span><span class="sxs-lookup"><span data-stu-id="4f155-106">Provisioning classic team sites</span></span>
<span data-ttu-id="4f155-107">Beim Bereitstellen von klassischen teamwebsitesammlungen (z. B. STS #0-basierte Websitesammlungen) muss eine verwendet die [CSOM `CreateSite` Methode](https://msdn.microsoft.com/en-us/library/microsoft.online.sharepoint.tenantadministration.tenant.createsite(v=office.15).aspx) Anruf als erklärt und gezeigt in folgenden Artikeln und Beispiele:</span><span class="sxs-lookup"><span data-stu-id="4f155-107">When provisioning classic team site collections (e.g. STS#0 based site collections) one has to use the [CSOM `CreateSite` method](https://msdn.microsoft.com/en-us/library/microsoft.online.sharepoint.tenantadministration.tenant.createsite(v=office.15).aspx) call as explained and shown in following articles and samples:</span></span>
- [<span data-ttu-id="4f155-108">Der websitebereitstellung in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="4f155-108">Site provisioning in the SharePoint add-in model</span></span>](site-provisioning-sharepoint-add-in.md)
- [<span data-ttu-id="4f155-109">Bereitstellen von Websites in Batches mit dem Add-In-Modell</span><span class="sxs-lookup"><span data-stu-id="4f155-109">Provision sites in batches with the add-in model</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Batch)
- [<span data-ttu-id="4f155-110">Erstellen der Websitesammlung oder Unterwebsite mithilfe der Plug & Play-Websites Core-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="4f155-110">Create site collection or sub site using the PnP Sites Core library</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.CreateSite)

<span data-ttu-id="4f155-111">Die `CreateSite` Methodenaufruf ausgeführt werden soll auf instanziierten `Tenant` ... und ein Mandant-Objekt müssen Sie Sie zum Angeben einer SPO Admin Center-URL erstellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="4f155-111">The `CreateSite` method call needs to be executed on an instantiated `Tenant` object...and a tenant object requires you to specify an SPO Admin center URL to be created.</span></span> <span data-ttu-id="4f155-112">So gehen zum Erstellen einer Teamwebsite klassische folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="4f155-112">So to create a classic team site you follow these steps:</span></span>
- <span data-ttu-id="4f155-113">Ermitteln Sie zunächst den Geo-Speicherort, der zum Hosten der Websitesammlung (z. B. der Europäischen Satelliten) benötigt</span><span class="sxs-lookup"><span data-stu-id="4f155-113">First determine the geo location that needs to host the site collection (e.g. the European satellite)</span></span>
- <span data-ttu-id="4f155-114">Sie anhand des Leitfadens im Artikel [Multi-Geo Discovery](multigeo-discovery.md) erläutert den Mandanten Verwaltungssite und SharePoint Stamm-Url für den Speicherort der Geo suchen</span><span class="sxs-lookup"><span data-stu-id="4f155-114">Use the guidance explained in the [Multi-Geo Discovery](multigeo-discovery.md) article to find the tenant admin site and SharePoint root url's for the geo location</span></span>
- <span data-ttu-id="4f155-115">Erstellen einer `Tenant` -Objekts verwenden die gefundenen Admin-Website-Url</span><span class="sxs-lookup"><span data-stu-id="4f155-115">Create a `Tenant` object using the found admin site url</span></span>
- <span data-ttu-id="4f155-116">Verwendung der `CreateSite` -Methodenaufrufs Inline an die Websitesammlung erstellen</span><span class="sxs-lookup"><span data-stu-id="4f155-116">Use the `CreateSite` method call to create the site collection</span></span>

<span data-ttu-id="4f155-117">Unter Beispiel zeigt, wie eine Websitesammlung in der Europäischen Geo-Speicherort bereit:</span><span class="sxs-lookup"><span data-stu-id="4f155-117">Below sample shows how to provision a site collection in the European geo location:</span></span>

```C#
// Use the Multi-Geo discovery guidance to discover the tenant admin and root site urls for this geo location
string tenantAdminSiteForMyGeoLocation = "https://contoso-europe-admin.sharepoint.com";
string targetUrl = "https://contoso-europe.sharepoint.com/sites/demosite";
string owner = "UserA@contoso.onmicrosoft.com";

using (var ctx = new ClientRuntimeContext(tenantAdminSiteForMyGeoLocation))
{
    ctx.Credentials = adminCredentials;
    
    var tenant = new Tenant(ctx);
    
    //Create new site
    var newsite = new SiteCreationProperties()
    {
        Url = targetUrl,
        Owner = owner,
        Template = "STS#0",
        Title = title,
        StorageMaximumLevel = 1000,
        StorageWarningLevel = 500,
        TimeZoneId = 7,
    };
    
    var spoOperation = tenant.CreateSite(newsite);
    
    ctx.Load(spoOperation);
    ctx.ExecuteQuery();
    
    while (!spoOperation.IsComplete)
    {
        Thread.Sleep(2000);
        ctx.Load(spoOperation);
        ctx.ExecuteQuery();
        Console.WriteLine("Site creation status: " + (spoOperation.IsComplete ? "waiting" : "complete"));
    }
}
```

> [!NOTE] 
> <span data-ttu-id="4f155-118">Wenn Sie erfahren mehr über die benötigten Berechtigungen und wie Sie Ihre Anwendung konfigurieren, und klicken Sie dann bitte Auschecken im Artikel [Einrichten der Multi-Geo Beispielanwendungen](multigeo-sampleapplicationsetup.md) möchten.</span><span class="sxs-lookup"><span data-stu-id="4f155-118">If you want to learn more about the needed permissions and how to configure your applications then please checkout the [Setting up the Multi-Geo sample applications](multigeo-sampleapplicationsetup.md) article.</span></span>

## <a name="resources"></a><span data-ttu-id="4f155-119">Ressourcen</span><span class="sxs-lookup"><span data-stu-id="4f155-119">Resources</span></span>
<span data-ttu-id="4f155-120">Unterhalb der Liste der Ressourcen sind hilfreich, wenn Sie weitere Informationen zum Arbeiten mit Websites vertraut machen:</span><span class="sxs-lookup"><span data-stu-id="4f155-120">Below list of resources are useful when you're learning more about working with sites:</span></span>
- [<span data-ttu-id="4f155-121">Bereitstellen von modernen Teamwebsites</span><span class="sxs-lookup"><span data-stu-id="4f155-121">Provisioning modern team sites</span></span>](https://msdn.microsoft.com/en-us/pnp_articles/modern-experience-customizations-provisioning-sites)
- [<span data-ttu-id="4f155-122">Der websitebereitstellung in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="4f155-122">Site provisioning in the SharePoint add-in model</span></span>](site-provisioning-sharepoint-add-in.md)
- [<span data-ttu-id="4f155-123">Bereitstellen von Websites in Batches mit dem Add-In-Modell</span><span class="sxs-lookup"><span data-stu-id="4f155-123">Provision sites in batches with the add-in model</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Batch)
- [<span data-ttu-id="4f155-124">Erstellen der Websitesammlung oder Unterwebsite mithilfe der Plug & Play-Websites Core-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="4f155-124">Create site collection or sub site using the PnP Sites Core library</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.CreateSite)