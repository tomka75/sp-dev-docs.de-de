---
title: Verwenden des Websitesammlungs-App-Katalogs
ms.date: 12/14/2017
ms.prod: sharepoint
ms.assetid: fdf7ecb1-9951-475b-b058-3285fba77b68
ms.openlocfilehash: 2a2e17f0f33bb6f801872965289663fbcca4e28e
ms.sourcegitcommit: 1845925102fabc55de2c6c60b47c20303b22b173
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="use-the-site-collection-app-catalog"></a><span data-ttu-id="33b0b-102">Verwenden des Websitesammlungs-App-Katalogs</span><span class="sxs-lookup"><span data-stu-id="33b0b-102">Use the site collection app catalog</span></span>

<span data-ttu-id="33b0b-103">_**Gilt für:** Office 365_</span><span class="sxs-lookup"><span data-stu-id="33b0b-103">*Applies to: Office 365</span></span>

<span data-ttu-id="33b0b-104">Durch Verwendung von Websitesammlungs-App-Katalogs können SharePoint-Mandantenadministratoren die Verwaltung und den Bereich der Bereitstellung von SharePoint-Add-Ins und SharePoint Framework-Lösungen auf bestimmten Websites dezentralisieren.</span><span class="sxs-lookup"><span data-stu-id="33b0b-104">Using site collection app catalogs, SharePoint tenant administrators can decentralize the management and scope the deployment of SharePoint add-ins and SharePoint Framework solutions to specific sites.</span></span>

## <a name="why-site-collection-app-catalogs"></a><span data-ttu-id="33b0b-105">Vorteile von Websitesammlungs-App-Katalogen</span><span class="sxs-lookup"><span data-stu-id="33b0b-105">Why site collection app catalogs</span></span>

<span data-ttu-id="33b0b-106">Bisher mussten alle Add-Ins und SharePoint Framework-Lösungen zentral im Mandanten-App-Katalog verwaltet werden.</span><span class="sxs-lookup"><span data-stu-id="33b0b-106">Previously, all add-ins and SharePoint Framework solutions had to be managed centrally in the tenant app catalog.</span></span> <span data-ttu-id="33b0b-107">Mandantenadministratoren konnten zwar den Zugriff für andere Personen im Unternehmen delegieren, in allen Websitesammlungen war jedoch ein bereitgestelltes Paket zu sehen.</span><span class="sxs-lookup"><span data-stu-id="33b0b-107">While tenant administrators could delegate the access to other people in the organization, a deployed package was visible on all site collections.</span></span> <span data-ttu-id="33b0b-108">SharePoint umfasste keine unterstützte Möglichkeit zum Bereitstellen von Add-Ins und SharePoint Framework-Lösungen nur auf bestimmten Websites.</span><span class="sxs-lookup"><span data-stu-id="33b0b-108">SharePoint offered no supported way of deploying add-ins and SharePoint Framework solutions only to specific sites.</span></span>

<span data-ttu-id="33b0b-109">Mit der Einführung von Websitesammlungs-App-Katalogen können Mandantenadministratoren den App-Katalog auf bestimmten Websites aktivieren.</span><span class="sxs-lookup"><span data-stu-id="33b0b-109">With the introduction of site collection app catalogs, tenant administrators can enable app catalog on the specific sites.</span></span> <span data-ttu-id="33b0b-110">Nach der Aktivierung können Websitesammlungsadministratoren SharePoint-Add-Ins und SharePoint Framework-Lösungen bereitstellen, die nur in dieser Websitesammlung verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="33b0b-110">Once enabled, site collection administrators can deploy SharePoint add-ins and SharePoint Framework solutions that will be available only in that particular site collection.</span></span>

<span data-ttu-id="33b0b-111">Im folgenden Schema ist die Verwendung von Websitesammlungs-App-Katalogen dargestellt:</span><span class="sxs-lookup"><span data-stu-id="33b0b-111">The following schema illustrates using site collection app catalogs:</span></span>

![Diagramm, in dem das Konzept des Websitesammlungs-App-Katalogs veranschaulicht wird](../images/site-collection-app-catalog-diagram.png)

<span data-ttu-id="33b0b-113">In Ihrem Office 365-Mandanten haben Sie einen Mandanten-App-Katalog.</span><span class="sxs-lookup"><span data-stu-id="33b0b-113">In your Office 365 tenant you have a tenant app catalog.</span></span> <span data-ttu-id="33b0b-114">Lösungen, die in diesem App-Katalog bereitgestellt werden, können in einer beliebigen Websitesammlung im Mandanten installiert werden.</span><span class="sxs-lookup"><span data-stu-id="33b0b-114">Solutions deployed to this app catalog, can be installed in any site collection in the tenant.</span></span> <span data-ttu-id="33b0b-115">Mandantenadministratoren können Websitesammlungs-App-Kataloge in bestimmten Websitesammlungen aktivieren.</span><span class="sxs-lookup"><span data-stu-id="33b0b-115">Tenant administrators can choose to enable site collection app catalogs on specific site collections.</span></span> <span data-ttu-id="33b0b-116">Lösungen, die in den Websitesammlungs-App-Katalogen bereitgestellt werden, können nur in dieser bestimmten Websitesammlung installiert werden.</span><span class="sxs-lookup"><span data-stu-id="33b0b-116">Solutions deployed to the site collection app catalogs can only be installed in that particular site collection.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="33b0b-117">Unterstützte Funktionen</span><span class="sxs-lookup"><span data-stu-id="33b0b-117">Supported capabilities</span></span>

### <a name="support-for-both-sharepoint-add-ins-and-sharepoint-framework-packages"></a><span data-ttu-id="33b0b-118">Unterstützung für SharePoint-Add-Ins und SharePoint Framework-Pakete</span><span class="sxs-lookup"><span data-stu-id="33b0b-118">Support for both SharePoint add-ins and SharePoint Framework packages</span></span>

<span data-ttu-id="33b0b-119">In Websitesammlungs-App-Katalogen können Sie, genau wie im Mandanten-App-Katalog, sowohl SharePoint-Add-Ins als auch SharePoint Framework-Lösungen (SSPKG) bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="33b0b-119">In site collection app catalogs, just as in tenant app catalog, you can deploy both SharePoint add-ins and SharePoint Framework solutions (.sppkg).</span></span>

### <a name="including-assets-in-solution-packages"></a><span data-ttu-id="33b0b-120">Einschließen von Ressourcen in Lösungspakete</span><span class="sxs-lookup"><span data-stu-id="33b0b-120">Including assets in solution packages</span></span>

<span data-ttu-id="33b0b-121">SharePoint Framework-Lösungspakete, die Ressourcen enthalten, können in Websitesammlungs-App-Katalogen bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="33b0b-121">SharePoint Framework solution packages that contain assets, can be deployed to site collection app catalogs.</span></span> <span data-ttu-id="33b0b-122">Eingeschlossene Ressourcen werden in einer vorkonfigurierten Dokumentbibliothek in derselben Websitesammlung bereitgestellt, in der sich auch der Websitesammlungs-App-Katalog befindet.</span><span class="sxs-lookup"><span data-stu-id="33b0b-122">Included assets will be deployed to a preconfigured document library in the same site collection as where the site collection app catalog is located.</span></span> <span data-ttu-id="33b0b-123">Wenn das öffentliche Office 365 CDN konfiguriert ist, werden Ressourcen vom CDN bedient.</span><span class="sxs-lookup"><span data-stu-id="33b0b-123">If the Office 365 Public CDN is configured, assets will be served from the CDN.</span></span> <span data-ttu-id="33b0b-124">Andernfalls werden Ressourcen direkt von der Dokumentbibliothek bedient.</span><span class="sxs-lookup"><span data-stu-id="33b0b-124">Otherwise, assets will be served directly from the document library.</span></span>

> [!NOTE]
> <span data-ttu-id="33b0b-125">Derzeit wird ein Bugfix für die korrekte Unterstützung der Ressourcenverpackung in Websitesammlungs-App-Katalogen eingeführt, der vor Ablauf des Kalenerjahrs 2017 auf allen Mandanten verfügbar sein sollte.</span><span class="sxs-lookup"><span data-stu-id="33b0b-125">A bugfix for correctly supporting assets packaging in site collection app catalogs is currently being rolled out and should be available on all tenants before the end of the calendar year 2017.</span></span>

### <a name="tenant-scoped-deployment"></a><span data-ttu-id="33b0b-126">Mandantenweite Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="33b0b-126">Tenant-scoped deployment</span></span>

<span data-ttu-id="33b0b-127">Bei der Bereitstellung von SharePoint Framework-Lösungen, die die mandantenweite Bereitstellung in einem Websitesammlungs-App-Katalog unterstützen, werden Sie gefragt, ob Sie diese Lösung auf allen Websites in der Organisation verfügbar machen möchten.</span><span class="sxs-lookup"><span data-stu-id="33b0b-127">When deploying SharePoint Framework solutions that support tenant-wide deployment to a site collection app catalog, you will be prompted if you want to make this solution available to all sites in the organization.</span></span> <span data-ttu-id="33b0b-128">Wenn Sie dieses Kontrollkästchen aktivieren, wird die Lösung trotz dieser Formulierung sofort **nur in derselben Websitesammlung verfügbar gemacht, in der sich auch der App-Katalog befindet**.</span><span class="sxs-lookup"><span data-stu-id="33b0b-128">Despite the wording, if you check this box, the solution will be available immediately **only in the same site collection as where the app catalog is**.</span></span> <span data-ttu-id="33b0b-129">Andere Websitesammlungen in Ihren Organisationen können die Lösung nicht verwenden.</span><span class="sxs-lookup"><span data-stu-id="33b0b-129">Other site collections in your organizations will not be able to use the solution.</span></span> <span data-ttu-id="33b0b-130">Wenn Sie diese Option nicht aktivieren, müssen Sie die Lösung auf Ihrer Website explizit installieren, bevor Sie diese verwenden können.</span><span class="sxs-lookup"><span data-stu-id="33b0b-130">If you don't check this option, you will have to explicitly install the solution in your site, before you will be able to use it.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="33b0b-131">Aktuelle Einschränkungen</span><span class="sxs-lookup"><span data-stu-id="33b0b-131">Current limitations:</span></span>

### <a name="application-lifecycle-management-alm-apis-are-not-yet-supported"></a><span data-ttu-id="33b0b-132">Application Lifecycle Management (ALM)-APIs werden noch nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="33b0b-132">Application Lifecycle Management (ALM) APIs are not yet supported</span></span>

<span data-ttu-id="33b0b-133">Derzeit ist es nicht möglich, die vor kurzem veröffentlichten ALM-APIs für die Verwaltung des Lebenszyklus von Lösungen in Websitesammlungs-App-Katalogen zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="33b0b-133">At this moment, it's not possible to use the recently released ALM APIs to manage the lifecycle of solutions in site collection app catalogs.</span></span> <span data-ttu-id="33b0b-134">Daran wird derzeit gearbeitet, und dies sollte zu Beginn des Jahres 2018 verfügbar sein.</span><span class="sxs-lookup"><span data-stu-id="33b0b-134">This is currently being worked on and should be available in the early 2018.</span></span>

## <a name="configure-and-manage-site-collection-app-catalogs"></a><span data-ttu-id="33b0b-135">Konfigurieren und Verwalten von Websitesammlungs-App-Katalogen</span><span class="sxs-lookup"><span data-stu-id="33b0b-135">Configure and manage site collection app catalogs</span></span>

<span data-ttu-id="33b0b-136">Sie können Websitesammlungs-App-Kataloge mithilfe der SharePoint Online-Verwaltungsshell konfigurieren und verwalten.</span><span class="sxs-lookup"><span data-stu-id="33b0b-136">You can configure and manage site collection app catalogs using the SharePoint Online Management Shell.</span></span>

> [!NOTE]
> <span data-ttu-id="33b0b-137">Bevor Sie Websitesammlungs-App-Kataloge in Ihrem Mandanten verwalten können, müssen Sie sicherstellen, dass Sie die [SharePoint Online-Verwaltungshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) vom November 2017 oder eine höhere Version verwenden.</span><span class="sxs-lookup"><span data-stu-id="33b0b-137">Before you can manage site collection app catalogs in your tenant, ensure that you have installed [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) from November '17 or newer.</span></span>

### <a name="create-a-site-collection-app-catalog"></a><span data-ttu-id="33b0b-138">Erstellen eines Websitesammlungs-App-Katalogs</span><span class="sxs-lookup"><span data-stu-id="33b0b-138">Create a site collection app catalog</span></span>

> [!NOTE]
> <span data-ttu-id="33b0b-139">Bevor Sie das folgende Skript ausführen, stellen Sie eine Verbindung zu Ihrem SharePoint Online-Mandanten mithilfe des `Connect-SPOService`-Cmdlets her.</span><span class="sxs-lookup"><span data-stu-id="33b0b-139">Before running the following script, connect to your SharePoint Online tenant using the `Connect-SPOService` cmdlet.</span></span> <span data-ttu-id="33b0b-140">Stellen Sie auch sicher, dass Sie einen Mandanten-App-Katalog in Ihrem Mandanten erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="33b0b-140">Also ensure, that you have a tenant app catalog created in your tenant.</span></span> <span data-ttu-id="33b0b-141">Wenn Sie dies nicht tun, schlägt das Cmdlet mit dem folgenden Fehler fehl:</span><span class="sxs-lookup"><span data-stu-id="33b0b-141">If you don't, the cmdlet will fail with the following error:</span></span>
> ```text
> Cannot invoke method or retrieve property from null object. Object returned by the
> following call stack is null. "TenantAppCatalog
> RootWeb
> GetSiteByUrl
> new Microsoft.Online.SharePoint.TenantAdministration.Tenant()
> "
> ```

<span data-ttu-id="33b0b-142">Zum Erstellen eines Websitesammlungs-App-Katalogs verwenden Sie das `Add-SPOSiteCollectionAppCatalog`-Cmdlet, das die Websitesammlung übergibt, wobei der App-Katalog als der `-Site`-Parameter erstellt werden sollte.</span><span class="sxs-lookup"><span data-stu-id="33b0b-142">To create a site collection app catalog, use the `Add-SPOSiteCollectionAppCatalog` cmdlet passing the site collection where the app catalog should be created as the `-Site` parameter.</span></span>

```powershell
# get a reference to the site collection where the
# site collection app catalog should be created
$site = Get-SPOSite https://contoso.sharepoint.com/sites/marketing

# create site collection app catalog
Add-SPOSiteCollectionAppCatalog -Site $site
```

<span data-ttu-id="33b0b-143">Nach dem Ausführen dieses Skripts, wird die **Apps für SharePoint**-Bibliothek zu Ihrer Websitesammlung hinzugefügt, wo Sie SharePoint-Add-Ins und SharePoint Framework-Lösungen bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="33b0b-143">After executing this script, the **Apps for SharePoint** library will be added to your site collection where you will be able to deploy SharePoint add-ins and SharePoint Framework solutions.</span></span>

### <a name="disable-the-site-collection-app-catalog"></a><span data-ttu-id="33b0b-144">Deaktivieren des Websitesammlungs-App-Katalogs</span><span class="sxs-lookup"><span data-stu-id="33b0b-144">Disable the site collection app catalog</span></span>

> [!NOTE]
> <span data-ttu-id="33b0b-145">Bevor Sie das folgende Skript ausführen, stellen Sie eine Verbindung zu Ihrem SharePoint Online-Mandanten mithilfe des `Connect-SPOService`-Cmdlets her.</span><span class="sxs-lookup"><span data-stu-id="33b0b-145">Before running the following script, connect to your SharePoint Online tenant using the `Connect-SPOService` cmdlet.</span></span>

<span data-ttu-id="33b0b-146">Zum Deaktivieren des Websitesammlungs-App-Katalogs in Ihrer Websitesammlung verwenden Sie das `Remove-SPOSiteCollectionAppCatalog`-Cmdlet, das die Websitesammlung übergibt, wobei der App-Katalog als der `-Site`-Parameter deaktiviert werden sollte.</span><span class="sxs-lookup"><span data-stu-id="33b0b-146">To disable the site collection app catalog in your site collection, use the `Remove-SPOSiteCollectionAppCatalog` cmdlet passing the site collection where the app catalog should be disabled as the `-Site` parameter.</span></span> <span data-ttu-id="33b0b-147">Wenn Sie über die ID Ihrer Websitesammlung verfügen, können Sie alternativ das `Remove-SPOSiteCollectionAppCatalogById`-Cmdlet verwenden.</span><span class="sxs-lookup"><span data-stu-id="33b0b-147">Alternatively, if you have your site collection's ID, you can use the `Remove-SPOSiteCollectionAppCatalogById` cmdlet instead.</span></span>

> [!NOTE]
> <span data-ttu-id="33b0b-148">Trotz des Namens entfernen die Cmdlets `Remove-SPOSiteCollectionAppCatalog` und `Remove-SPOSiteCollectionAppCatalogById` den Websitesammlungs-App-Katalog nicht aus der Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="33b0b-148">Despite the naming, the `Remove-SPOSiteCollectionAppCatalog` and `Remove-SPOSiteCollectionAppCatalogById` cmdlets don't remove the site collection app catalog from the site collection.</span></span> <span data-ttu-id="33b0b-149">Sie deaktivieren diesen vielmehr, sodass Sie keine Lösungen darin bereitstellen oder darin bereitgestellte Lösungen verwenden können.</span><span class="sxs-lookup"><span data-stu-id="33b0b-149">Instead, they disable it so that it's not possible to deploy or use any solutions deployed in it.</span></span>

```powershell
# get a reference to the site collection in which
# the site collection app catalog should be disabled
$site = Get-SPOSite https://contoso.sharepoint.com/sites/marketing

# disable the site collection app catalog
Remove-SPOSiteCollectionAppCatalog -Site $site
```

<span data-ttu-id="33b0b-150">Nach dem Ausführen dieses Skript ist die **Apps für SharePoint**-Bibliothek immer noch in Ihrer Websitesammlung sichtbar, Sie können jedoch keine Lösungen darin bereitstellen oder darin bereitgestellte Lösungen verwenden.</span><span class="sxs-lookup"><span data-stu-id="33b0b-150">After executing this script, the **Apps for SharePoint** library will be still visible in your site collection, but you will not be able to deploy or use any solutions deployed in it.</span></span>

## <a name="considerations"></a><span data-ttu-id="33b0b-151">Überlegungen</span><span class="sxs-lookup"><span data-stu-id="33b0b-151">Considerations</span></span>

### <a name="governance"></a><span data-ttu-id="33b0b-152">Steuerung</span><span class="sxs-lookup"><span data-stu-id="33b0b-152">Governance considerations</span></span>

<span data-ttu-id="33b0b-153">Derzeit ist es nicht möglich, alle Websitesammlungen in dem Mandanten aufzuführen, die den Websitesammlungs-App-Katalog aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="33b0b-153">Currently, it's not possible to list all site collections in the tenant that have the site collection app catalog enabled.</span></span>

### <a name="security"></a><span data-ttu-id="33b0b-154">Sicherheit</span><span class="sxs-lookup"><span data-stu-id="33b0b-154">Security</span></span>

<span data-ttu-id="33b0b-155">Vor dem Bereitstellen von Lösungen in Websitesammlungs-App-Katalogen sollten Websitesammlungsadministratoren überprüfen, dass diese Lösungen den Organisationsrichtlinien entsprechen.</span><span class="sxs-lookup"><span data-stu-id="33b0b-155">Before deploying solutions to site collection app catalogs, site collection administrators should verify that these solutions meet organizational policies.</span></span> <span data-ttu-id="33b0b-156">Lösungen, die in Websitesammlungs-App-Katalogen installiert sind, können zwar nur in diesen bestimmten Websitesammlungen verwendet werden, sie können jedoch möglicherweise auf Ressourcen von anderen Websites in dem Mandanten zugreifen, Administratoren sollten daher sicherstellen, dass die Lösungen, die sie bereitstellen, wie beabsichtigt funktionieren.</span><span class="sxs-lookup"><span data-stu-id="33b0b-156">Although solutions installed in site collection app catalogs can only be used in these particular site collections, they can potentially access resources from other sites in the tenant so administrators should ensure that the solutions they are about to deploy work as intended.</span></span>

## <a name="see-also"></a><span data-ttu-id="33b0b-157">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="33b0b-157">See also</span></span>

- <span data-ttu-id="33b0b-158">[Verwalten des Websitesammlungs-App-Katalogs](https://support.office.com/de-DE/article/Manage-the-Site-Collection-App-Catalog-928b9b61-a9de-4563-a7d1-6231aa9d4d19)</span><span class="sxs-lookup"><span data-stu-id="33b0b-158">[Manage the Site Collection App Catalog](https://support.office.com/de-DE/article/Manage-the-Site-Collection-App-Catalog-928b9b61-a9de-4563-a7d1-6231aa9d4d19)</span></span>