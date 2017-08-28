# <a name="tenant-scoped-solution-deployment-for-sharepoint-framework-solutions"></a><span data-ttu-id="ec54d-101">Mandantenweite Lösungsbereitstellung für SharePoint Framework-Lösungen</span><span class="sxs-lookup"><span data-stu-id="ec54d-101">Tenant-Scoped solution deployment for SharePoint Framework solutions</span></span>

<span data-ttu-id="ec54d-p101">Sie können Ihre SharePoint Framework-Komponenten so konfigurieren, dass sie sofort nach der Installation des Lösungspakets im App-Katalog eines Mandanten mandantenweit verfügbar sind. Hierzu verwenden Sie das Attribut **skipFeatureDeployment** in der Datei **package-solution.json**.</span><span class="sxs-lookup"><span data-stu-id="ec54d-p101">You can configure your SharePoint Framework components to be immediately available cross the tenant when solution package is installed to tenant app catalog. This can be configured by using **skipFeatureDeployment** attribute in the **package-solution.json** file.</span></span>

<span data-ttu-id="ec54d-104">Ist dieses Attribut für eine Lösung aktiviert, wird dem Mandantenadministrator bei der Installation des Lösungspakets im App-Katalog des Mandanten angeboten, die Lösung automatisch in allen Websitesammlungen und auf allen Websites im Mandanten verfügbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="ec54d-104">When solution has this attribute enabled, tenant administrator will be provided option to enable the solution to be available automatically cross all site collections and sites in tenant, when the solution package is installed to the tenant app catalog.</span></span> 

<span data-ttu-id="ec54d-105">Eine Demonstration der mandantenweiten Bereitstellung finden Sie in dem folgenden Video in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=pemHOZCSwZI).</span><span class="sxs-lookup"><span data-stu-id="ec54d-105">You can also see the tenant-wide deployment option demonstrated by watching following video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=pemHOZCSwZI).</span></span>

<a href="https://www.youtube.com/watch?v=pemHOZCSwZI&list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG">
<img src="../../images/tenant-deploy-youtube-video.png" alt="PnP Short Guidance video on tenant-wide deployment option" />
</a>

> <span data-ttu-id="ec54d-p102">Beachten Sie: Sie müssen auf die neueste Version der SharePoint Framework-Yeoman-Vorlage aktualisieren, um diese Funktion nutzen zu können. Aktualisieren können Sie Ihre globale Installation mit dem Befehl `npm install -g @microsoft/generator-sharepoint`.</span><span class="sxs-lookup"><span data-stu-id="ec54d-p102">Notice. You have to update to latest SharePoint Framework Yeoman template version to be able to use this capability. You can update your global installation by executing `npm install -g @microsoft/generator-sharepoint`.</span></span> 

## <a name="solution-specific-requirements"></a><span data-ttu-id="ec54d-109">Lösungsspezifische Anforderungen</span><span class="sxs-lookup"><span data-stu-id="ec54d-109">Solution specific requirements</span></span>

<span data-ttu-id="ec54d-p103">Wenn diese Option verwendet wird, werden alle Featureframeworkdefinitionen in der SharePoint Framework-Lösung ignoriert. Enthält Ihre Lösung Featureframeworkdefinitionen, beispielsweise zur Erstellung einer benutzerdefinierten Liste, sollten Sie diese lösungsspezifische Option nicht nutzen.</span><span class="sxs-lookup"><span data-stu-id="ec54d-p103">When this option is used, any feature framework definitions in the SharePoint Framework solution will be ignored. If solution contains Feature Framework definitions, for example for creating a custom list, you should not use this solution specific option.</span></span>

* [<span data-ttu-id="ec54d-112">Bereitstellen von SharePoint-Objekten mit Ihrem Lösungspaket</span><span class="sxs-lookup"><span data-stu-id="ec54d-112">Provision SharePoint assets with your solution package</span></span>](#)

> <span data-ttu-id="ec54d-p104">Beachten Sie: Lösungen, für die eine automatische mandantenweite Bereitstellung konfiguriert ist, werden auf Website-Ebene nicht unter „App hinzufügen“ aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="ec54d-p104">Notice. Solutions which are configured to be automatically deployed cross tenants are not visible in the add an app capability at the site level.</span></span> 

## <a name="configuring-solution-to-be-available-cross-tenant"></a><span data-ttu-id="ec54d-115">Konfigurieren von Lösungen für mandantenweite Verfügbarkeit</span><span class="sxs-lookup"><span data-stu-id="ec54d-115">Configuring solution to be available cross tenant</span></span>

<span data-ttu-id="ec54d-p105">In der SharePoint Framework-Yeoman-Vorlage ist eine spezifische Frage für diese Option enthalten. Ihre Antwort auf diese Frage hat direkte Auswirkungen auf das Attribut **skipFeatureDeployment** in der Datei **package-solution.json**.</span><span class="sxs-lookup"><span data-stu-id="ec54d-p105">SharePoint Framework Yeoman template will ask a specific question related on this option. This question will impact directly on the **skipFeatureDeployment** attribute in the **package-solution.json** file.</span></span> 

![Yeoman-Frage zur mandantenweiten Bereitstellung](../../images/tenant-deploy-yeoman.png)

<span data-ttu-id="ec54d-119">In der folgenden Beispielkonfiguration ist **skipFeatureDeployment** auf „true“ gesetzt. Das bedeutet, dass die Lösung zentral im gesamten Mandanten bereitgestellt werden kann.</span><span class="sxs-lookup"><span data-stu-id="ec54d-119">In following example configuration, **skipFeatureDeployment** is set to true, which indicates that solution can be centrally deployed cross the tenant.</span></span> 

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

### <a name="approving-tenant-wide-deployment-in-app-catalog"></a><span data-ttu-id="ec54d-120">Genehmigen einer mandantenweiten Bereitstellung im App-Katalog</span><span class="sxs-lookup"><span data-stu-id="ec54d-120">Approving tenant wide deployment in app catalog</span></span>

<span data-ttu-id="ec54d-121">Wird eine Lösung, für die das Attribut **skipFeatureDeployment** auf **true** gesetzt ist, im App-Katalog eines Mandanten bereitgestellt, wird dem Administrator angeboten, sie zentral für den gesamten Mandantenbereich bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="ec54d-121">When solution with **skipFeatureDeployment** attribute set to **true** is deployed to tenant app catalog, administrator is given an option to configure solution to be deployed centrally cross the tenant.</span></span>

<span data-ttu-id="ec54d-p106">Das Kontrollkästchen **Make this solution available to all sites in the organization** ist standardmäßig deaktiviert. Wenn der Administrator das Kontrollkästchen aktiviert, sind die Komponenten der Lösung automatisch im gesamten Mandantenbereich sichtbar und verfügbar.</span><span class="sxs-lookup"><span data-stu-id="ec54d-p106">By default, "**Make this solution available to all sites in the organization**" checkbox is unchecked. If the checkbox is checked by the administrator, components in the solutions will be automatically visible and available cross the tenant.</span></span> 

![Einstellung „Make this solution available to all sites in an organization“ bei der Bereitstellung der Lösung im App-Katalog](../../images/tenant-deploy-app-catalog.png)

<span data-ttu-id="ec54d-p107">Beachten Sie: Da die lösungs- und websitespezifischen Aktualisierungsaktionen nur bei Verwendung eines Featureframeworks verfügbar sind, gibt es keine spezifische Aktualisierungsoption für zentral bereitgestellte Lösungen. Lösungen dieses Typs lassen sich einfach über eine Aktualisierung der lösungsspezifischen Objekte im CDN sowie eine Aktualisierung des Pakets im App-Katalog aktualisieren. Dadurch werden automatisch sämtliche vorhandenen Komponenteninstanzen im Mandantenbereich so aktualisiert, dass sie die neuesten Komponentenobjekte verwenden (z. B. JavaScript-Dateien und aktualisierte CSS-Dateien).</span><span class="sxs-lookup"><span data-stu-id="ec54d-p107">Notice that since the solution and site -specific upgrade actions are only available when you use feature framework, there's no specific upgrade option for the centrally deployed solutions. These solutions can be simply updated by updating solution specific assets in the CDN and by updating package in the app catalog. This will update automatically all existing component instances cross the tenant to use the latest component assets, like JavaScript files and updated CSS files.</span></span>

## <a name="client-side-web-part-visibility-in-sharepoint-sites"></a><span data-ttu-id="ec54d-128">Sichtbarkeit clientseitiger Webparts auf SharePoint-Websites</span><span class="sxs-lookup"><span data-stu-id="ec54d-128">Client-side web part visibility in SharePoint sites</span></span>

<span data-ttu-id="ec54d-129">In zentral bereitgestellten Lösungen enthaltene Webparts sind sofort in der Webpartauswahl sichtbar, sowohl auf klassischen als auch auf modernen Seiten.</span><span class="sxs-lookup"><span data-stu-id="ec54d-129">Web parts included in solutions which have been centrally deployed, will be immediately visible in the web part picker in both classic and modern pages.</span></span> 

## <a name="impact-of-skipfeaturedeployment-setting-with-extensions"></a><span data-ttu-id="ec54d-130">Auswirkungen der Einstellung „skipFeatureDeployment“ auf Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="ec54d-130">Impact of skipFeatureDeployment setting with Extensions</span></span>

<span data-ttu-id="ec54d-p108">SharePoint Framework-Erweiterungen stehen sofort zur Verwendung auf SharePoint-Websites zur Verfügung. Das bedeutet, dass sie mit der Eigenschaft **ClientSideComponentId** von SharePoint-Elementen verknüpft werden können, beispielsweise von *Feldern* und *benutzerdefinierten Aktionen von Benutzern*.</span><span class="sxs-lookup"><span data-stu-id="ec54d-p108">SharePoint Framework extensions will be immediately available to be used in the SharePoint sites. This means that they can be associated to be used with **ClientSideComponentId** properties in the specific SharePoint elements, like *fields* and *user custom actions*.</span></span> 

