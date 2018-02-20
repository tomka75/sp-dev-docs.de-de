---
title: Feature Heften in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 204f53d47256b51ef6c2495deae4c69ce810fa23
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/19/2018
---
<a name="feature-stapling-in-the-sharepoint-add-in-model"></a><span data-ttu-id="e0fce-102">Feature Heften in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="e0fce-102">Feature Stapling in the SharePoint add-in model</span></span>
===============================================

<a name="summary"></a><span data-ttu-id="e0fce-103">Summary</span><span class="sxs-lookup"><span data-stu-id="e0fce-103">Summary</span></span>
-------

<span data-ttu-id="e0fce-104">Ansatz verwenden Sie zum Ausführen von Code, und stellen Sie Artefakte aus, wenn eine SharePoint-Website bereitgestellt wird unterscheidet in das neue SharePoint-Add-in-Modell es von der Benutzeroberfläche mit vollständigen Code, der als vertrauenswürdig.</span><span class="sxs-lookup"><span data-stu-id="e0fce-104">The approach you take to run code and deploy artifacts when a SharePoint site is provisioned is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="e0fce-105">In einer typischen vollständige vertrauen Code (FTC) / Out-of-Box-Website, die Definitionen mit geändert wurden Farmlösung Szenario geheftet Features.</span><span class="sxs-lookup"><span data-stu-id="e0fce-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, out-of-the-box site definitions were modified with stapled features.</span></span>  <span data-ttu-id="e0fce-106">Features zum Verpacken und Bereitstellen von Artefakten, Konfigurationen und branding-Objekte mit einer SharePoint-Website verknüpft ist verwendet wurden, und Features auf die Websitedefinition geheftet wurden.</span><span class="sxs-lookup"><span data-stu-id="e0fce-106">Features were used to package and deploy artifacts, configurations, and branding assets associated with a SharePoint site and features were stapled to the site definition.</span></span>  <span data-ttu-id="e0fce-107">Die geheftet Features wurden dann automatisch installiert und bei der websitebereitstellung aktiviert.</span><span class="sxs-lookup"><span data-stu-id="e0fce-107">Then the stapled features were automatically installed and activated upon site provisioning.</span></span>

<span data-ttu-id="e0fce-108">In einem Modell Szenario SharePoint-Add-in können Sie Heften Features, heften-Add-ins oder SharePoint Client Side Object Model (CSOM), zu erstellen und Konfigurieren von Websitesammlungen und Websites sub Bereitstellen von Artefakten, Konfigurationen und branding-Objekten für diese verwenden.</span><span class="sxs-lookup"><span data-stu-id="e0fce-108">In an SharePoint Add-in model scenario, you may staple features, staple Add-ins, or use the SharePoint Client Side Object Model (CSOM) to create and configure site collections and sub sites then deploy artifacts, configurations, and branding assets to them.</span></span> <span data-ttu-id="e0fce-109">Dieses Muster wird häufig als *remote provisioning Muster*bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="e0fce-109">This pattern is commonly referred to as the *remote provisioning pattern*.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="e0fce-110">Hohe Stufe Richtlinien</span><span class="sxs-lookup"><span data-stu-id="e0fce-110">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="e0fce-111">In der Regel von einer Ziehpunkt möchten wir bieten die folgenden high Level Richtlinien zum Erstellen und Konfigurieren von Websitesammlungen und Websites sub dann Artefakte, Konfigurationen und branding-Objekten für diese bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="e0fce-111">As a rule of a thumb, we would like to provide the following high level guidelines to create and configure site collections and sub sites then deploy artifacts, configurations, and branding assets to them.</span></span>

- <span data-ttu-id="e0fce-112">Ist die einzige Möglichkeit, die Sie weiterhin Heften Feature verwenden können, wenn Sie Features für Websitesammlungen für das Heften werden und Sie sandkastenlösungen verwenden, um die Websitedefinitionen und die geheftet Features bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="e0fce-112">The only way you can still use feature stapling is when you are stapling features to site collections and you are using sandbox solutions to deploy the site definitions and the stapled features.</span></span>    
- <span data-ttu-id="e0fce-113">Sie können das Add-In Modell mit Mandanten Heften-Add-ins zum Implementieren der Funktion Heften ähnliche Funktionalität bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="e0fce-113">You can use the Add-in stapling model with tenant deployed Add-ins to implement functionality similar to feature stapling.</span></span>
- <span data-ttu-id="e0fce-114">Das remote provisioning Muster können Sie mit der Aktivierung der zusätzlichen Features auf der Basis der Websitedefinition Out-of-Box-Feld über remote-APIs Heften Feature ähnliche Funktionalität implementieren.</span><span class="sxs-lookup"><span data-stu-id="e0fce-114">You can use the remote provisioning pattern to implement functionality similar to feature stapling by activating additional features on top of the out-of-the-box box site definition via remote APIs.</span></span>

<a name="options-to-create-and-configure-site-collections-and-sub-sites-then-deploy-artifacts-configurations-and-branding-assets-to-them"></a><span data-ttu-id="e0fce-115">Optionen zum Erstellen und Konfigurieren von Websitesammlungen und Websites dann sub Bereitstellen von Artefakten, Konfigurationen und branding-Objekte für diese</span><span class="sxs-lookup"><span data-stu-id="e0fce-115">Options to create and configure site collections and sub sites then deploy artifacts, configurations, and branding assets to them</span></span>
---------------------------------------------------------------------------------------------------------------------------------

<span data-ttu-id="e0fce-116">Sie müssen einige Optionen zum Erstellen und Konfigurieren von Websitesammlungen und Websites sub dann Artefakte, Konfigurationen und branding-Objekten für diese bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="e0fce-116">You have a few options to to create and configure site collections and sub sites then deploy artifacts, configurations, and branding assets to them.</span></span>

- <span data-ttu-id="e0fce-117">Heften features</span><span class="sxs-lookup"><span data-stu-id="e0fce-117">Staple features</span></span>
- <span data-ttu-id="e0fce-118">Heften-Add-ins</span><span class="sxs-lookup"><span data-stu-id="e0fce-118">Staple Add-ins</span></span>
- <span data-ttu-id="e0fce-119">Verwenden Sie das remote provisioning Muster</span><span class="sxs-lookup"><span data-stu-id="e0fce-119">Use the remote provisioning pattern</span></span>   

<a name="staple-features"></a><span data-ttu-id="e0fce-120">Heften features</span><span class="sxs-lookup"><span data-stu-id="e0fce-120">Staple features</span></span>
---------------
<span data-ttu-id="e0fce-121">In diesem Muster heften Sie Features, Websitedefinitionen.</span><span class="sxs-lookup"><span data-stu-id="e0fce-121">In this pattern you staple features to site definitions.</span></span>
    
- <span data-ttu-id="e0fce-122">Dieses Muster ist nur auf der Ebene der Websitesammlung verfügbar.</span><span class="sxs-lookup"><span data-stu-id="e0fce-122">This pattern is only available at the site collection level.</span></span>
- <span data-ttu-id="e0fce-123">Es ist nicht möglich, Funktionen, die in Sub Websites heften.</span><span class="sxs-lookup"><span data-stu-id="e0fce-123">It is not possible to staple features to sub sites.</span></span>
- <span data-ttu-id="e0fce-124">Dies ist keine optimale oder empfohlene Ansatz, da sie veraltete sandkastenlösungen verwendet und nicht mehr geeignet für Upgrades Sie legen.</span><span class="sxs-lookup"><span data-stu-id="e0fce-124">This is not an optimal or recommended approach because it uses deprecated sandbox solutions and does not set you up well for upgrades.</span></span>

<span data-ttu-id="e0fce-125">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="e0fce-125">**When is it a good fit?**</span></span>

<span data-ttu-id="e0fce-126">Wenn Sie legacy-Code in einer lokalen SharePoint-Umgebung migrieren, und Sie haben keine Zeit, es ordnungsgemäß erneut schreiben.</span><span class="sxs-lookup"><span data-stu-id="e0fce-126">When you are migrating legacy code in an on-premises SharePoint environment and you do not have time to re-write it properly.</span></span>

<span data-ttu-id="e0fce-127">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="e0fce-127">**Getting Started**</span></span>

<span data-ttu-id="e0fce-128">Im folgende Artikel beschreibt die Funktionen, die in einer Websitedefinition heften.</span><span class="sxs-lookup"><span data-stu-id="e0fce-128">The following article describes how to staple features to a site definition.</span></span>

- [<span data-ttu-id="e0fce-129">Feature Heften In SharePoint 2010 (MSDN-Blog-Artikel)</span><span class="sxs-lookup"><span data-stu-id="e0fce-129">Feature Stapling In SharePoint 2010 (MSDN Blog Article)</span></span>](http://blogs.msdn.com/b/kunal_mukherjee/archive/2011/01/11/feature-stapling-in-sharepoint-2010.aspx)

<a name="staple-add-ins"></a><span data-ttu-id="e0fce-130">Heften-Add-ins</span><span class="sxs-lookup"><span data-stu-id="e0fce-130">Staple Add-ins</span></span>
--------------
<span data-ttu-id="e0fce-131">In diesem Muster stellen Sie in der app-Katalog bestimmte Websitesammlungen, verwaltete Pfade und Websitevorlagen gespeicherten-Add-ins bereit.</span><span class="sxs-lookup"><span data-stu-id="e0fce-131">In this pattern you deploy Add-ins stored in the app catalog to specific site collections, managed paths, and site templates.</span></span>

- <span data-ttu-id="e0fce-132">Finden Sie unter der [SharePoint 2013-App-Bereitstellung über ' App Heften ' (MSDN-Blogartikel - Richard DiZerega)](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/09/18/10399333.aspx) ausführliche Informationen zum Anordnen-Modell-Add-in.</span><span class="sxs-lookup"><span data-stu-id="e0fce-132">See the [SharePoint 2013 App Deployment through 'App Stapling' (MSDN Blog Article - Richard DiZerega)](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/09/18/10399333.aspx) for more details about the Add-in stapling model.</span></span>
- <span data-ttu-id="e0fce-133">Da das Add-in von einem Administrator abgelegt ist, werden Websitebesitzer werden nicht an das Add-in aus einer Website zu entfernen, die die Bereitstellungskriterien erfüllt.</span><span class="sxs-lookup"><span data-stu-id="e0fce-133">Because the add-in is pushed by an administrator, site owners will not be able to remove the add-in from a site that meets the deployment criteria.</span></span>  <span data-ttu-id="e0fce-134">Nicht auch ein Websitesammlungsadministrator kann das Add-in entfernen.</span><span class="sxs-lookup"><span data-stu-id="e0fce-134">Not even a site collection administrator can remove the add-in.</span></span>
- <span data-ttu-id="e0fce-135">Diese zentralisierte Bereitstellung freigegeben dieselben zentralisierten Add-in-Ressourcen (Web-Add-in und Remotewebsite).</span><span class="sxs-lookup"><span data-stu-id="e0fce-135">This centralized deployment also shares the same centralized add-in resources (Add-in Web and Remote Web).</span></span>  <span data-ttu-id="e0fce-136">Im Wesentlichen ist das Add-in bereitgestellt, aber nicht auf den Websites installiert.</span><span class="sxs-lookup"><span data-stu-id="e0fce-136">Essentially, the Add-in is deployed, but not installed in the sites.</span></span>  <span data-ttu-id="e0fce-137">Alle Websites werden die Add-Ins Web und die Remotewebsite aus der Instanz in der app-Katalog installiert nutzen.</span><span class="sxs-lookup"><span data-stu-id="e0fce-137">All sites will leverage the Add-in Web and Remote Web from the instance installed in the app catalog.</span></span>
- <span data-ttu-id="e0fce-138">Aufgrund von zentrale Bereitstellung werden remote Ereignisse wie "Handle App Installed", 'Behandeln App deinstalliert' und 'Behandeln App Upgrade' nur einmal ausgelöst werden (wenn das Add-in in der app-Katalog installiert ist).</span><span class="sxs-lookup"><span data-stu-id="e0fce-138">Because of centralized deployment, remote events such as 'Handle App Installed', 'Handle App Uninstalled', and 'Handle App Upgrade' will only fire once (when the Add-In is installed in the app catalog).</span></span>
    + <span data-ttu-id="e0fce-139">Dies kann erschweren Heften-Muster-Add-in verwenden, um automatisch Änderungen auf Websites angewendet, auf dem sie bereitgestellt wird, da diese Ereignisse nicht ausgelöst werden, wenn es Websites bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="e0fce-139">This can make it difficult to use the Add-in stapling pattern to automatically apply changes to sites where it is deployed because these events do not fire when it is deployed to sites.</span></span>
- <span data-ttu-id="e0fce-140">Add-in-Komponenten werden bei-Add-ins auf Websites geheftet werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="e0fce-140">Add-in parts are not supported when Add-ins are stapled to sites.</span></span>
- <span data-ttu-id="e0fce-141">Dieses Muster erfordert die manuelle Benutzeraktionen zum Bereitstellen von Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="e0fce-141">This pattern requires manual user actions to deploy the Add-ins.</span></span>

<a name="use-the-remote-provisioning-pattern"></a><span data-ttu-id="e0fce-142">Verwenden Sie das remote provisioning Muster</span><span class="sxs-lookup"><span data-stu-id="e0fce-142">Use the remote provisioning pattern</span></span>
-----------------------------------

<span data-ttu-id="e0fce-143">In diesem Muster verwenden Sie SharePoint Client Side Object Model (CSOM) zum Erstellen und Konfigurieren von Websitesammlungen und Websites sub dann Artefakte, Konfigurationen und branding-Objekten für diese bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="e0fce-143">In this pattern you use the SharePoint Client Side Object Model (CSOM) to create and configure site collections and sub sites then deploy artifacts, configurations, and branding assets to them.</span></span>

- <span data-ttu-id="e0fce-144">Dieses Muster erforderlich keine Packen Artefakte, Konfigurationen und branding-Objekte in separaten Features oder -Add-ins.  Alles kann in ein einzelnes Add-in gepackt.</span><span class="sxs-lookup"><span data-stu-id="e0fce-144">This pattern does not require packaging artifacts, configurations, and branding assets in separate features, or Add-ins.  Everything may be packaged in a single Add-in.</span></span>
- <span data-ttu-id="e0fce-145">Bei Verwendung dieses Muster für die websitebereitstellung überschreiben Sie in der Regel die Abwesenheitsnotiz der Feld-Seite, um eine neue Website erstellen.</span><span class="sxs-lookup"><span data-stu-id="e0fce-145">When you use this pattern for site provisioning you typically override the out of the box page to create a new site.</span></span>
- <span data-ttu-id="e0fce-146">Weitere Informationen zu diesem Muster finden Sie unter der [Website-Bereitstellung (SharePoint-Add-in-Anleitung)](site-provisioning-sharepoint-add-in.md)</span><span class="sxs-lookup"><span data-stu-id="e0fce-146">For more information about this pattern see the [Site Provisioning (SharePoint Add-in Recipe)](site-provisioning-sharepoint-add-in.md)</span></span>
- <span data-ttu-id="e0fce-147">Wenn Sie-Add-ins auf einer SharePoint-Website bereitstellen möchten, kann dies über CSOM erfolgen.</span><span class="sxs-lookup"><span data-stu-id="e0fce-147">If you wish to deploy Add-ins to a SharePoint site, this can be done via CSOM.</span></span>  <span data-ttu-id="e0fce-148">Es folgt ein Beispiel der lädt ein Office-Add-in über ein manifest-Datei am Seitenrand und werden in einer SharePoint-Website installiert.</span><span class="sxs-lookup"><span data-stu-id="e0fce-148">Here is an example which loads an Office Add-in via a .app manifest file and installs it in a SharePoint site.</span></span>

    ```
    //Create a FileStream object to access the Mail Office Add-in .app file 
    using (FileStream fsSource = new FileStream(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "Innovation.Management.AFO.app",
    FileMode.Open, FileAccess.Read))
    {
        //Return the subweb where you want to install the Add-in
        var subweb = ctx.Web;
        ctx.Load(subweb);
        ctx.ExecuteQuery();

        //Load and Install the Add-in on the subweb
        AppInstance appInstance = subweb.LoadAndInstallApp(fsSource);
        ctx.Load(appInstance);
        ctx.ExecuteQuery();
    }
    ```

    + <span data-ttu-id="e0fce-149">Überwachen der [Erstellen Cloud gehostet Zeile Of Business Applications mit der Add-ins für Office, Office 365, Azure und WP8 (Todd Baginski, Michael Sherman - SharePoint-Konferenz 2014)](https://channel9.msdn.com/Events/SharePoint-Conference/2014/SPC361) video sehen, wie diese Vorgehensweise zum Installieren von Office-Add-ins in SharePoint-Websites verwendet wurde Bei der websitebereitstellung.</span><span class="sxs-lookup"><span data-stu-id="e0fce-149">Watch the [Creating Cloud Hosted Line Of Business Applications with Add-ins for Office, O365, Azure, and WP8 (Todd Baginski, Michael Sherman - SharePoint Conference 2014)](https://channel9.msdn.com/Events/SharePoint-Conference/2014/SPC361) video to see how this approach was used to install Office Add-ins in SharePoint sites upon site provisioning.</span></span>
    + <span data-ttu-id="e0fce-150">Vollständige Automation kann nur mit-Add-ins, die vollständige Mandanten Berechtigung verfügen, die bereits als vertrauenswürdig eingestuft haben.</span><span class="sxs-lookup"><span data-stu-id="e0fce-150">Full automation is only possible with Add-ins that have full tenant permission that have already been trusted.</span></span>
        + <span data-ttu-id="e0fce-151">Finden Sie ein Beispiel für die [Core.Sideloading (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SideLoading) .</span><span class="sxs-lookup"><span data-stu-id="e0fce-151">See the [Core.Sideloading (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SideLoading) for an example.</span></span> 

<a name="related-links"></a><span data-ttu-id="e0fce-152">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="e0fce-152">Related links</span></span>
=============
- [<span data-ttu-id="e0fce-153">Feature Heften In SharePoint 2010 (MSDN-Blog-Artikel)</span><span class="sxs-lookup"><span data-stu-id="e0fce-153">Feature Stapling In SharePoint 2010 (MSDN Blog Article)</span></span>](http://blogs.msdn.com/b/kunal_mukherjee/archive/2011/01/11/feature-stapling-in-sharepoint-2010.aspx)
- [<span data-ttu-id="e0fce-154">Self-Service Site Provisioning von Add-Ins für SharePoint 2013 (MSDN-Blog)</span><span class="sxs-lookup"><span data-stu-id="e0fce-154">Self-Service Site Provisioning using add-ins for SharePoint 2013 (MSDN Blog)</span></span>](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/04/04/self-service-site-provisioning-using-apps-for-sharepoint-2013.aspx)
- [<span data-ttu-id="e0fce-155">SharePoint 2013-App-Bereitstellung über 'App Heften' (MSDN-Blogartikel - Richard DiZerega)</span><span class="sxs-lookup"><span data-stu-id="e0fce-155">SharePoint 2013 App Deployment through 'App Stapling' (MSDN Blog Article - Richard DiZerega)</span></span>](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/09/18/10399333.aspx)
- [<span data-ttu-id="e0fce-156">Website-Bereitstellung (SharePoint-Add-Ins Anleitung)</span><span class="sxs-lookup"><span data-stu-id="e0fce-156">Site Provisioning (SharePoint Add-in Recipe)</span></span>](site-provisioning-sharepoint-add-in.md)
- [<span data-ttu-id="e0fce-157">Erstellen der Cloud gehostet Geschäftsanwendungen mit-Add-ins für Office, Office 365, Azure und WP8 (Todd Baginski, Michael Sherman - SharePoint-Konferenz 2014)</span><span class="sxs-lookup"><span data-stu-id="e0fce-157">Creating Cloud Hosted Line Of Business Applications with Add-ins for Office, O365, Azure, and WP8 (Todd Baginski, Michael Sherman - SharePoint Conference 2014)</span></span>](https://channel9.msdn.com/Events/SharePoint-Conference/2014/SPC361)
- <span data-ttu-id="e0fce-158">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="e0fce-158">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="e0fce-159">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="e0fce-159">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="e0fce-160">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="e0fce-160">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="e0fce-161">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="e0fce-161">Related PnP samples</span></span>
===================

- [<span data-ttu-id="e0fce-162">Provisioning.Cloud.Sync (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="e0fce-162">Provisioning.Cloud.Sync (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Provisioning.Cloud.Sync)
- [<span data-ttu-id="e0fce-163">Provisioning.SubSiteCreationApp (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="e0fce-163">Provisioning.SubSiteCreationApp (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SubSiteCreationApp)
- [<span data-ttu-id="e0fce-164">Provisioning.Services.SiteManager (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="e0fce-164">Provisioning.Services.SiteManager (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Services.SiteManager)
- [<span data-ttu-id="e0fce-165">Provisioning.SiteCollectionCreation (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="e0fce-165">Provisioning.SiteCollectionCreation (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteCollectionCreation)
- <span data-ttu-id="e0fce-166">Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="e0fce-166">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="e0fce-167">Gilt für</span><span class="sxs-lookup"><span data-stu-id="e0fce-167">Applies to</span></span>
==========
- <span data-ttu-id="e0fce-168">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="e0fce-168">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="e0fce-169">Office 365 dedizierte (D)</span><span class="sxs-lookup"><span data-stu-id="e0fce-169">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="e0fce-170">SharePoint 2013 lokal</span><span class="sxs-lookup"><span data-stu-id="e0fce-170">SharePoint 2013 on-premises</span></span>
