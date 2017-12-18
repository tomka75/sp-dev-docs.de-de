# <a name="application-lifecycle-management-alm-apis"></a><span data-ttu-id="23960-101">Application Lifecycle Management (ALM)-APIs</span><span class="sxs-lookup"><span data-stu-id="23960-101">Application Lifecycle Management (ALM) APIs</span></span>  

<span data-ttu-id="23960-102">ALM-APIs bieten einfache APIs für die Verwaltung der Bereitstellung Ihrer SharePoint-Framework-Lösungen und Add-Ins Ihres Mandanten.</span><span class="sxs-lookup"><span data-stu-id="23960-102">ALM APIs are providing simple APIs to manage deployment of your SharePoint Framework solutions and add-ins cross your tenant.</span></span> <span data-ttu-id="23960-103">ALM-APIs unterstützen die folgenden Funktionen.</span><span class="sxs-lookup"><span data-stu-id="23960-103">ALM APIs support following capabilities.</span></span>

- <span data-ttu-id="23960-104">Hinzufügen einer SharePoint-Framework-Lösung oder eines SharePoint-Add-Ins zu einem Mandanten-App-Katalog</span><span class="sxs-lookup"><span data-stu-id="23960-104">Add SharePoint Framework solution or SharePoint add-in to tenant app catalog</span></span>
- <span data-ttu-id="23960-105">Aktivieren einer SharePoint-Framework-Lösung oder eines SharePoint-Add-Ins, damit diese für die Installation in einem Mandanten-App-Katalog verfügbar sind</span><span class="sxs-lookup"><span data-stu-id="23960-105">Enable SharePoint Framework solution or SharePoint add-in to be available for installation in tenant app catalog</span></span>
- <span data-ttu-id="23960-106">Deaktivieren einer SharePoint-Framework-Lösung oder eines SharePoint-Add-Ins, damit diese nicht für die Installation in einem Mandanten-App-Katalog verfügbar sind</span><span class="sxs-lookup"><span data-stu-id="23960-106">Disable SharePoint Framework solution or SharePoint add-in not to be available for installation in tenant app catalog</span></span>
- <span data-ttu-id="23960-107">Installieren einer SharePoint-Framework-Lösung oder eines SharePoint-Add-Ins aus einem Mandanten-App-Katalog in eine Seite</span><span class="sxs-lookup"><span data-stu-id="23960-107">Install SharePoint Framework solution or SharePoint add-in from tenant app catalog to a site</span></span>
- <span data-ttu-id="23960-108">Aktualisieren einer SharePoint-Framework-Lösung oder eines SharePoint-Add-Ins, wenn eine neuere Version im Mandanten-App-Katalog enthalten ist</span><span class="sxs-lookup"><span data-stu-id="23960-108">Upgrade SharePoint Framework solution or SharePoint add-in to a site, which has a newer version available in the tenant app catalog</span></span>
- <span data-ttu-id="23960-109">Deinstallieren einer SharePoint-Framework-Lösung oder eines SharePoint-Add-Ins von einer Seite</span><span class="sxs-lookup"><span data-stu-id="23960-109">Uninstall SharePoint Framework solution or SharePoint add-in from the site</span></span>

<span data-ttu-id="23960-110">ALM-APIs können verwendet werden, um genau die gleichen Operationen durchzuführen, die über die Benutzeroberfläche verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="23960-110">ALM APIs can be used to perform exactly the same operations which are available from UI perspective.</span></span> <span data-ttu-id="23960-111">Wenn diese APIs verwendet werden, können alle typischen Aktionen ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="23960-111">When these APIs are used, all typical actions will be performed.</span></span> <span data-ttu-id="23960-112">Nachfolgend finden Sie einige der Eigenschaften für ALM-APIs.</span><span class="sxs-lookup"><span data-stu-id="23960-112">Here are some of the characteristics for ALM APIs.</span></span>

- <span data-ttu-id="23960-113">Installieren und Deinstallieren von Ereignissen werden für vom Anbieter gehostete Add-Ins ausgelöst, wenn entsprechende Vorgänge aufgetreten sind</span><span class="sxs-lookup"><span data-stu-id="23960-113">Install and UnInstall events are being fired for provider hosted add-ins when corresponding operations are occurred</span></span>
- <span data-ttu-id="23960-114">ALM-APIs unterstützen nur app-basierte Vorgänge</span><span class="sxs-lookup"><span data-stu-id="23960-114">ALM APIs supports app-only based operations</span></span>

<span data-ttu-id="23960-115">ALM-APIs systemeigen über REST-APIs bereitgestellt, aber es gibt auch zusätzliche CSOM-Erweiterungen und PowerShell-Commandlets über SharePoint Patterns and Practices</span><span class="sxs-lookup"><span data-stu-id="23960-115">ALM APIs are natively provided using REST APIs, but there is also additional CSOM extensions and PowerShell commandlets available through SharePoint Patterns and Practices</span></span> 

## <a name="rest-api"></a><span data-ttu-id="23960-116">REST-API</span><span class="sxs-lookup"><span data-stu-id="23960-116">REST API</span></span>

### <a name="add-solution-package-to-tenant-app-catalog"></a><span data-ttu-id="23960-117">Hinzufügen eines Lösungspakets zum Mandanten-App-Katalog</span><span class="sxs-lookup"><span data-stu-id="23960-117">Add solution package to tenant app catalog</span></span> 

<span data-ttu-id="23960-118">Fügen Sie eine Lösung zum Mandanten-App-Katalog hinzu.</span><span class="sxs-lookup"><span data-stu-id="23960-118">Adding solution to the tenant app catalog.</span></span> <span data-ttu-id="23960-119">Diese API wird im Kontext der Mandanten-App-Katalogwebsite ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="23960-119">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
/_api/web/tenantappcatalog/Add(overwrite=true, url='test.txt')";
method: POST
binaryStringRequestBody: true
body: 'byte array of the file'
```

### <a name="deploy-solution-package-in-tenant-app-catalog"></a><span data-ttu-id="23960-120">Bereitstellen eines Lösungspakets im Mandanten-App-Katalog</span><span class="sxs-lookup"><span data-stu-id="23960-120">Deploy solution package in tenant app catalog</span></span>

<span data-ttu-id="23960-121">Aktivieren Sie die Lösung, damit Sie für die Installation in eine bestimmte Website zur Verfügung steht.</span><span class="sxs-lookup"><span data-stu-id="23960-121">Enable solution to be available to install to specific sites.</span></span> <span data-ttu-id="23960-122">Diese API wird im Kontext der Mandanten-App-Katalogwebsite ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="23960-122">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
/_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Deploy";
```

> [!NOTE]
> <span data-ttu-id="23960-123">Dieser Vorgang muss nach dem Hinzufügen abgeschlossen werden, damit Sie Pakete in bestimmte Websites integrieren können.</span><span class="sxs-lookup"><span data-stu-id="23960-123">This operation is required to be completed after add, before you can install packages to specific sites.</span></span> 

### <a name="retract-solution-package-in-the-tenant-app-catalog"></a><span data-ttu-id="23960-124">Zurückziehen eines Lösungspakets in den Mandanten-App-Katalog</span><span class="sxs-lookup"><span data-stu-id="23960-124">Retract solution package in the tenant app catalog</span></span>

<span data-ttu-id="23960-125">Ziehen Sie Lösungen zurück, sodass diese nicht mehr auf Websites zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="23960-125">Retract solution to be available from the sites.</span></span> <span data-ttu-id="23960-126">Diese API wird im Kontext der Mandanten-App-Katalogwebsite ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="23960-126">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
/_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Retract";
```

> [!NOTE]
> <span data-ttu-id="23960-127">Wenn Sie diesen Vorgang nach der Installation von Lösungen in Websites durchführen, funktionieren diese nicht mehr, da die Lösung auf Mandantenebene deaktiviert wurde.</span><span class="sxs-lookup"><span data-stu-id="23960-127">If you run this operation after you have already installed solutions to site, they will stop working since solution is disabled from the tenant level.</span></span>

### <a name="remove-solution-package-from-tenant-app-catalog"></a><span data-ttu-id="23960-128">Entfernen eines Lösungspakets aus dem Mandanten-App-Katalog</span><span class="sxs-lookup"><span data-stu-id="23960-128">Remove solution package from tenant app catalog</span></span>

<span data-ttu-id="23960-129">Entfernen Sie das Lösungspaket aus dem Mandanten-App-Katalog.</span><span class="sxs-lookup"><span data-stu-id="23960-129">Remove the solution package from the tenant app catalog.</span></span> <span data-ttu-id="23960-130">Diese API wird im Kontext der Mandanten-App-Katalogwebsite ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="23960-130">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
/_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Remove";
```

> [!NOTE]
> <span data-ttu-id="23960-131">Die Lösung wird ebenfalls automatisch zurückgezogen, wenn dieser Vorgang nicht vor dem Entfernen ausgeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="23960-131">Solution will be also automatically retracted, if that operation has not performed before Remove operation.</span></span>

### <a name="list-available-packages-from-tenant-app-catalog"></a><span data-ttu-id="23960-132">Auflisten verfügbarer Pakete aus dem Mandanten-App-Katalog</span><span class="sxs-lookup"><span data-stu-id="23960-132">List available packages from tenant app catalog</span></span>

<span data-ttu-id="23960-133">Rufen Sie mit der REST-API eine Liste der verfügbaren SharePoint-Framework-Lösungen oder -Add-Ins im Mandanten-App-Katalog ab.</span><span class="sxs-lookup"><span data-stu-id="23960-133">REST API for getting list of available SharePoint Framework solutions or add-ins in tenant app catalog.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps
method: GET
```

### <a name="details-on-individual-solution-package-from-tenant-app-catalog"></a><span data-ttu-id="23960-134">Einzelheiten zu einzelnen Lösungspaketen aus dem Mandanten-App-Katalog</span><span class="sxs-lookup"><span data-stu-id="23960-134">Details on individual solution package from tenant app catalog</span></span>

<span data-ttu-id="23960-135">Rufen Sie mit der REST-API Einzelheiten zu einzelnen SharePoint-Framework-Lösungen oder -Add-Ins im Mandanten-App-Katalog ab.</span><span class="sxs-lookup"><span data-stu-id="23960-135">REST API for getting details on individual SharePoint Framework solution or add-in available in the tenant app catalog.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')
method: GET
```

### <a name="install-solution-package-from-tenant-app-catalog-to-sharepoint-site"></a><span data-ttu-id="23960-136">Integrieren eines Lösungspakets aus dem Mandanten-App-Katalog in eine SharePoint-Website</span><span class="sxs-lookup"><span data-stu-id="23960-136">Install solution package from tenant app catalog to SharePoint site</span></span>

<span data-ttu-id="23960-137">Integrieren Sie ein Lösungspaket mit bestimmten Bezeichnern aus einem Mandanten-App-Katalog in eine auf URL-Kontext basierende Website.</span><span class="sxs-lookup"><span data-stu-id="23960-137">Install a solution package with specific identifier from tenant app catalog to the site based on URL context.</span></span> <span data-ttu-id="23960-138">Dieser REST-Aufruf kann im Kontext der Website ausgeführt werden, für die der Installationsvorgang ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="23960-138">This REST call can be executed in the context of the site where the install operation should happen.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Install";
method: POST
```

### <a name="upgrade-solution-package-in-sharepoint-site"></a><span data-ttu-id="23960-139">Aktualisieren eines Lösungspakets einer SharePoint-Website</span><span class="sxs-lookup"><span data-stu-id="23960-139">Upgrade solution package in SharePoint site</span></span>

<span data-ttu-id="23960-140">Aktualisieren Sie ein Lösungspaket der Seite auf eine neuere, im Mandanten-App-Katalog verfügbare Version.</span><span class="sxs-lookup"><span data-stu-id="23960-140">Upgrade a solution package from the site to a newer version available in the tenant app catalog.</span></span> <span data-ttu-id="23960-141">Dieser REST-Aufruf kann im Kontext der Website ausgeführt werden, für die der Aktualisierungsvorgang ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="23960-141">This REST call can be executed in the context of the site where the upgrade operation should happen.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Upgrade";
method: POST
```

### <a name="uninstall-solution-package-from-sharepoint-site"></a><span data-ttu-id="23960-142">Deinstallieren eines Lösungspakets von einer SharePoint-Website</span><span class="sxs-lookup"><span data-stu-id="23960-142">Uninstall solution package from SharePoint site</span></span>

<span data-ttu-id="23960-143">Deinstallieren Sie ein Lösungspaket von einer SharePoint-Website.</span><span class="sxs-lookup"><span data-stu-id="23960-143">Uninstall a solution package from the site.</span></span> <span data-ttu-id="23960-144">Dieser REST-Aufruf kann im Kontext der Website ausgeführt werden, für die der Deinstallationsvorgang ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="23960-144">This REST call can be executed in the context of the site where the uninstall operation should happen.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Uninstall";
method: POST
```
> [!NOTE]
> <span data-ttu-id="23960-145">Wenn Sie die REST-API verwenden, um ein Lösungspaket von der Website zu deinstallieren, wird es nicht in den Papierkorb verschoben.</span><span class="sxs-lookup"><span data-stu-id="23960-145">When you use the REST API to uninstall solution package from the site, it is not relocated to the recycle bin.</span></span>


## <a name="sharepoint-pnp-powershell-cmdlets-to-programmatically-add-and-deploy-sharepoint-apps"></a><span data-ttu-id="23960-146">SharePoint PnP PowerShell-Cmdlets zum programmgesteuerten Hinzufügen und Bereitstellen von SharePoint-Apps</span><span class="sxs-lookup"><span data-stu-id="23960-146">SharePoint PnP PowerShell cmdlets to programmatically add and deploy SharePoint Apps</span></span>

<span data-ttu-id="23960-147">Mit [PnP PowerShell](https://msdn.microsoft.com/de-DE/pnp_powershell/pnp-powershell-overview) können Sie die Bereitstellung, Veröffentlichung, Installation, Aktualisierung und das Zurückziehen Ihrer Apps automatisieren.</span><span class="sxs-lookup"><span data-stu-id="23960-147">Using [PnP PowerShell](https://msdn.microsoft.com/de-DE/pnp_powershell/pnp-powershell-overview) you can automate the deployment, publishing, installing, upgrading and retracting your apps.</span></span> <span data-ttu-id="23960-148">Sehen Sie sich das Kapitel unten an, um mehr über Cmdlets zu erfahren.</span><span class="sxs-lookup"><span data-stu-id="23960-148">Checkout below chapter to learn more about this cmdlets.</span></span>

### <a name="adding-and-publishing-your-app-to-the-app-catalog"></a><span data-ttu-id="23960-149">Hinzufügen Ihrer App zum App-Katalog und Veröffentlichen Ihrer App im App-Katalog</span><span class="sxs-lookup"><span data-stu-id="23960-149">Adding and publishing your app to the app catalog</span></span>
<span data-ttu-id="23960-150">Sie müssen Ihre App (.sppkg-Datei, .app-Datei) zu Ihrem Mandanten-App-Katalog hinzufügen, damit Sie sie später auf Ihrer SharePoint-Seite zur Verfügung stellen können.</span><span class="sxs-lookup"><span data-stu-id="23960-150">Adding your app (.sppkg file, .app file) to the tenant app catalog is a per-requisite to later on make your app available for use in your SharePoint sites.</span></span> <span data-ttu-id="23960-151">Dieser Vorgang kann mit einem einfachen cmdlet durchgeführt werden:</span><span class="sxs-lookup"><span data-stu-id="23960-151">Doing so can be done using below simple cmdlet:</span></span>

```PowerShell
Add-PnPApp -Path ./myapp.sppkg"
```

<span data-ttu-id="23960-152">Nachdem Sie die App hinzugefügt haben, müssen Sie sie veröffentlichen, damit sie von anderen Benutzern Ihres Mandanten verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="23960-152">Once added you'll need to continue with publishing your app, effectively making the app available to be used by the users of your tenant.</span></span> <span data-ttu-id="23960-153">Unter PnP PowerShell-Cmdlets finden Sie die entsprechende Vorgehensweise:</span><span class="sxs-lookup"><span data-stu-id="23960-153">Below PnP PowerShell cmdlets shows how this can be done:</span></span>

```PowerShell
Publish-PnPApp -Identity <app id> -SkipFeatureDeployment
```


> [!NOTE]
> <span data-ttu-id="23960-154">Verwenden Sie die Kennzeichnung SkipFeatureDeployment, damit eine App, die für die Mandanten-weite Bereitstellung entwickelt wurde, auch tatsächlich als Mandanten-weit bereitgestellte App verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="23960-154">Use the SkipFeatureDeployment flag to allow an app that was developed for tenant wide deployment to be actually available as a tenant wide deployed app.</span></span>



### <a name="removing-the-app-from-the-app-catalog"></a><span data-ttu-id="23960-155">Entfernen der App aus dem App-Katalog</span><span class="sxs-lookup"><span data-stu-id="23960-155">Removing the app from the app catalog</span></span>
<span data-ttu-id="23960-156">Möglicherweise möchten Sie auch eine zuvor hinzugefügte App entfernen. Dieser Vorgang kann mit dem folgenden Cmdlet ausgeführt werden:</span><span class="sxs-lookup"><span data-stu-id="23960-156">Obviously you might also want to remove an earlier added app and that can be done using the following cmdlet:</span></span>

```PowerShell
Remove-PnPApp -Identity <app id>
```


### <a name="using-apps-on-your-site"></a><span data-ttu-id="23960-157">Verwenden von Apps auf Ihrer Website</span><span class="sxs-lookup"><span data-stu-id="23960-157">Using apps on your site</span></span>
<span data-ttu-id="23960-158">Nachdem die App zum App-Katalog hinzugefügt und veröffentlicht wurde, können Sie mit der Installation der App in Ihre Website beginnen.</span><span class="sxs-lookup"><span data-stu-id="23960-158">Once the app was added to the app catalog and published you can continue with installing the app to your site.</span></span>

```PowerShell
Install-PnPApp -Identity <app id>
```


<span data-ttu-id="23960-159">Eine hinzugefügte App muss außerdem aktualisiert werden:</span><span class="sxs-lookup"><span data-stu-id="23960-159">An added app also needs be upgraded:</span></span>

```PowerShell
Update-PnPApp -Identity <app id>
```


<span data-ttu-id="23960-160">Möglicherweise möchten Sie die App auch von Ihrer Seite deinstallieren:</span><span class="sxs-lookup"><span data-stu-id="23960-160">And you off course also uninstall the app again from your site:</span></span>

```PowerShell
Uninstall-PnPApp -Identity <app id>
```


> [!NOTE]
> <span data-ttu-id="23960-161">Wenn Sie eine App von Ihrer Website deinstallieren, wird die App vollständig gelöscht, sodass sie nicht im Papierkorb der Website landen.</span><span class="sxs-lookup"><span data-stu-id="23960-161">When you uninstall an app from your site the app is completely deleted, so it will not end up in the site's recycle bin.</span></span>



### <a name="knowing-which-apps-are-there-for-you-to-use"></a><span data-ttu-id="23960-162">Informieren Sie sich, welche Apps für die Verwendung zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="23960-162">Knowing which apps are there for you to use</span></span>
<span data-ttu-id="23960-163">Sie können eine Liste der Apps abrufen, die zu der Website hinzugefügt werden können:</span><span class="sxs-lookup"><span data-stu-id="23960-163">Getting a list of apps that can be added to the site is possible using:</span></span>

```PowerShell
Get-PnPAvailableApp
```