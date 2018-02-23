---
title: "Mandantenweite Lösungsbereitstellung für SharePoint-Framework-Lösungen"
description: "Konfigurieren Sie Ihre SharePoint-Framework-Komponenten, damit diese sofort in dem Mandanten verfügbar sind, wenn das Lösungspaket im Mandanten-App-Katalog installiert ist."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: d48aa779602950cd589b4d5e6dbaab868b698f9e
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/05/2018
---
# <a name="tenant-scoped-solution-deployment-for-sharepoint-framework-solutions"></a><span data-ttu-id="1fb06-103">Mandantenweite Lösungsbereitstellung für SharePoint-Framework-Lösungen</span><span class="sxs-lookup"><span data-stu-id="1fb06-103">Tenant-Scoped solution deployment for SharePoint Framework solutions</span></span>

<span data-ttu-id="1fb06-104">Sie können Ihre SharePoint-Framework-Komponenten konfigurieren, damit diese sofort in dem Mandanten verfügbar sind, wenn das Lösungspaket im Mandanten-App-Katalog installiert ist.</span><span class="sxs-lookup"><span data-stu-id="1fb06-104">You can configure your SharePoint Framework components to be immediately available across the tenant when the solution package is installed to the tenant App Catalog.</span></span> <span data-ttu-id="1fb06-105">Dies kann mit dem **skipFeatureDeployment**-Attribut in der Datei **solution.json-Paket** konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="1fb06-105">This can be configured by using the **skipFeatureDeployment** attribute in the **package-solution.json** file.</span></span>

<span data-ttu-id="1fb06-106">Ist dieses Attribut für eine Lösung aktiviert, wird dem Mandantenadministrator bei der Installation des Lösungspakets im App-Katalog des Mandanten angeboten, die Lösung automatisch in allen Websitesammlungen und auf allen Websites im Mandanten verfügbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="1fb06-106">When solution has this attribute enabled, tenant administrator will be provided option to enable the solution to be available automatically cross all site collections and sites in tenant, when the solution package is installed to the tenant app catalog.</span></span> 

<span data-ttu-id="1fb06-107">Eine Demonstration der mandantenweiten Bereitstellung finden Sie in dem folgenden Video in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=pemHOZCSwZI).</span><span class="sxs-lookup"><span data-stu-id="1fb06-107">You can also see the tenant-wide deployment option demonstrated by watching following video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=pemHOZCSwZI).</span></span>

<a href="https://www.youtube.com/watch?v=pemHOZCSwZI&list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG">
<img src="../images/tenant-deploy-youtube-video.png" alt="PnP Short Guidance video on tenant-wide deployment option" />
</a>

> [!NOTE] 
> <span data-ttu-id="1fb06-108">Sie müssen auf die neueste Version der SharePoint-Framework-Yeoman-Vorlage aktualisieren, um diese Funktion nutzen zu können.</span><span class="sxs-lookup"><span data-stu-id="1fb06-108">Notice. You have to update to latest SharePoint Framework Yeoman template version to be able to use this capability. You can update your global installation by executing .</span></span> <span data-ttu-id="1fb06-109">Aktualisieren können Sie Ihre globale Installation mit dem Befehl `npm install -g @microsoft/generator-sharepoint`.</span><span class="sxs-lookup"><span data-stu-id="1fb06-109">You can update your global installation by executing `npm install -g @microsoft/generator-sharepoint`.</span></span> 

## <a name="solution-specific-requirements"></a><span data-ttu-id="1fb06-110">Lösungspezifische Anforderungen</span><span class="sxs-lookup"><span data-stu-id="1fb06-110">Solution-specific requirements</span></span>

<span data-ttu-id="1fb06-p103">Wenn diese Option verwendet wird, werden alle Featureframeworkdefinitionen in der SharePoint-Framework-Lösung ignoriert. Enthält Ihre Lösung Featureframeworkdefinitionen, beispielsweise zur Erstellung einer benutzerdefinierten Liste, sollten Sie diese lösungsspezifische Option nicht nutzen.</span><span class="sxs-lookup"><span data-stu-id="1fb06-p103">When this option is used, any feature framework definitions in the SharePoint Framework solution will be ignored. If solution contains Feature Framework definitions, for example for creating a custom list, you should not use this solution specific option.</span></span>

<span data-ttu-id="1fb06-113">Weitere Informationen finden Sie unter [Bereitstellen von SharePoint-Elementen mit Ihrem Lösungspaket](./toolchain/provision-sharepoint-assets.md).</span><span class="sxs-lookup"><span data-stu-id="1fb06-113">For more information, see [Provision SharePoint assets with your solution package](./toolchain/provision-sharepoint-assets.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="1fb06-114">Lösungen, für die eine automatische mandantenweite Bereitstellung konfiguriert ist, werden auf Website-Ebene nicht unter „App hinzufügen“ aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="1fb06-114">Notice. Solutions which are configured to be automatically deployed cross tenants are not visible in the add an app capability at the site level.</span></span> 

## <a name="configure-solution-to-be-available-across-the-tenant"></a><span data-ttu-id="1fb06-115">Konfigurieren von Lösungen für mandantenweite Verfügbarkeit</span><span class="sxs-lookup"><span data-stu-id="1fb06-115">Configure solution to be available across the tenant</span></span>

<span data-ttu-id="1fb06-116">In der SharePoint-Framework-Yeoman-Vorlage wird eine bestimmte Frage im Zusammenhang mit dieser Option gestellt.</span><span class="sxs-lookup"><span data-stu-id="1fb06-116">The SharePoint Framework Yeoman template asks a specific question related to this option.</span></span> <span data-ttu-id="1fb06-117">Diese Frage wirkt sich direkt auf das **skipFeatureDeployment**-Attribut in der Datei **solution.json-Paket**.</span><span class="sxs-lookup"><span data-stu-id="1fb06-117">This question impacts directly on the **skipFeatureDeployment** attribute in the **package-solution.json** file.</span></span> 

![Yeoman-Frage zur mandantenweiten Bereitstellung](../images/tenant-deploy-yeoman.png)

<br/>

<span data-ttu-id="1fb06-119">In der folgenden Beispielkonfiguration ist **skipFeatureDeployment** auf „true“ gesetzt. Das bedeutet, dass die Lösung zentral im gesamten Mandanten bereitgestellt werden kann.</span><span class="sxs-lookup"><span data-stu-id="1fb06-119">In following example configuration, **skipFeatureDeployment** is set to true, which indicates that solution can be centrally deployed cross the tenant.</span></span> 

```json
{
  "solution": {
    "name": "tenant-deploy-client-side-solution",
    "id": "dd4feca4-6f7e-47f1-a0e2-97de8890e3fa",
    "version": "1.0.0.0",
    "skipFeatureDeployment": true
  },
  "paths": {
    "zippedPackage": "solution/tenant-deploy-true.sppkg"
  }
}

```

### <a name="approving-tenant-wide-deployment-in-app-catalog"></a><span data-ttu-id="1fb06-120">Genehmigen einer mandantenweiten Bereitstellung im App-Katalog</span><span class="sxs-lookup"><span data-stu-id="1fb06-120">Approving tenant-wide deployment in App Catalog</span></span>

<span data-ttu-id="1fb06-121">Wird eine Lösung, für die das Attribut **skipFeatureDeployment** auf **true** gesetzt ist, im App-Katalog eines Mandanten bereitgestellt, wird dem Administrator angeboten, sie zentral für den gesamten Mandantenbereich bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="1fb06-121">When solution with **skipFeatureDeployment** attribute set to **true** is deployed to tenant app catalog, administrator is given an option to configure solution to be deployed centrally cross the tenant.</span></span>

<span data-ttu-id="1fb06-122">Standardmäßig ist das Kontrollkästchen **Diese Lösung für alle Websites der Organisation verfügbar machen** nicht aktiviert.</span><span class="sxs-lookup"><span data-stu-id="1fb06-122">By default, the **Make this solution available to all sites in the organization** check box is not selected.</span></span> <span data-ttu-id="1fb06-123">Wenn Sie das Kontrollkästchen vom Administrator aktiviert wird, werden Komponenten in den Lösungen automatisch für den gesamten Mandantenbereich angezeigt und verfügbar.</span><span class="sxs-lookup"><span data-stu-id="1fb06-123">If the check box is selected by the administrator, components in the solutions are automatically visible and available across the tenant.</span></span> 

![Die Einstellung „Diese Lösung für alle Websites der Organisation verfügbar machen“ wird bei der Bereitstellung der Lösung im App-Katalog angezeigt.](../images/tenant-deploy-app-catalog.png)

<span data-ttu-id="1fb06-125">Da die Lösung und die websitespezifischen Upgradeaktionen nur verfügbar sind, wen Sie das Featureframework verwenden, gibt es keine spezifische Upgradeoption für die zentral bereitgestellten Lösungen.</span><span class="sxs-lookup"><span data-stu-id="1fb06-125">Notice that because the solution and site-specific upgrade actions are only available when you use the feature framework, there's no specific upgrade option for the centrally deployed solutions.</span></span> <span data-ttu-id="1fb06-126">Diese Lösungen können aktualisiert werden, indem lösungsspezifische Objekte im CDN und das Paket im App-Katalog aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="1fb06-126">These solutions can be updated by updating the solution-specific assets in the CDN and by updating the package in the App Catalog.</span></span> <span data-ttu-id="1fb06-127">Dabei werden alle vorhandenen Komponenteninstanzen für den gesamten Mandanten automatisch für die Verwendung der neuesten Komponentenobjekte, u. a. JavaScript-Dateien und aktualisierte CSS-Dateien, aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="1fb06-127">This automatically updates all existing component instances across the tenant to use the latest component assets, such as JavaScript files and updated CSS files.</span></span>

## <a name="client-side-web-part-visibility-on-sharepoint-sites"></a><span data-ttu-id="1fb06-128">Sichtbarkeit clientseitiger Webparts auf SharePoint-Websites</span><span class="sxs-lookup"><span data-stu-id="1fb06-128">Client-side web part visibility in SharePoint sites</span></span>

<span data-ttu-id="1fb06-129">In zentral bereitgestellten Lösungen enthaltene Webparts sind sofort in der Webpartauswahl sichtbar, sowohl auf klassischen als auch auf modernen Seiten.</span><span class="sxs-lookup"><span data-stu-id="1fb06-129">Web parts included in solutions which have been centrally deployed, will be immediately visible in the web part picker in both classic and modern pages.</span></span> 

## <a name="impact-of-skipfeaturedeployment-setting-with-extensions"></a><span data-ttu-id="1fb06-130">Auswirkungen der Einstellung „skipFeatureDeployment“ auf Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="1fb06-130">Impact of skipFeatureDeployment setting with Extensions</span></span>

<span data-ttu-id="1fb06-131">[SharePoint-Framework-Erweiterungen](./extensions/overview-extensions.md) sind sofort verfügbar und können auf SharePoint-Websites verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="1fb06-131">[SharePoint Framework Extensions](./extensions/overview-extensions.md) are immediately available to be used on SharePoint sites.</span></span> <span data-ttu-id="1fb06-132">Das bedeutet, dass sie den **ClientSideComponentId**-Eigenschaften in bestimmten SharePoint-Elementen, z. B. **Feldern** und **benutzerdefinierten Aktionen** zugeordnet werden können.</span><span class="sxs-lookup"><span data-stu-id="1fb06-132">SharePoint Framework extensions will be immediately available to be used in the SharePoint sites. This means that they can be associated to be used with **ClientSideComponentId** properties in the specific SharePoint elements, like **fields** and **user custom actions**.</span></span> 

## <a name="see-also"></a><span data-ttu-id="1fb06-133">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="1fb06-133">See also</span></span>

- [<span data-ttu-id="1fb06-134">Übersicht über das SharePoint-Framework</span><span class="sxs-lookup"><span data-stu-id="1fb06-134">Overview of the SharePoint Framework</span></span>](sharepoint-framework-overview.md)