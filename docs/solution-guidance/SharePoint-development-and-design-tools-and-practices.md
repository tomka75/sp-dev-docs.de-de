---
title: SharePoint-Entwicklung und Design Tools und Methoden
ms.date: 11/03/2017
ms.openlocfilehash: 155558fb24f4be14919e83b881e70db7950ef26a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="sharepoint-development-and-design-tools-and-practices"></a><span data-ttu-id="82250-102">SharePoint-Entwicklung und Design Tools und Methoden</span><span class="sxs-lookup"><span data-stu-id="82250-102">SharePoint development and design tools and practices</span></span>

<span data-ttu-id="82250-103">Entwurf und Entwicklung SharePoint-Tools können branding zu Ihrer SharePoint-Websites anwenden.</span><span class="sxs-lookup"><span data-stu-id="82250-103">You can use SharePoint design and development tools to apply branding to your SharePoint sites.</span></span>

<span data-ttu-id="82250-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="82250-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="82250-105">Dieser Artikel enthält Informationen zu den Entwicklungs- und Optionen, die in SharePoint zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="82250-105">This article provides information about the development and design options that are available in SharePoint.</span></span> <span data-ttu-id="82250-106">Hier finden Sie Informationen zur Verwendung von remote provisioning Muster branding-Objekte auf einer SharePoint-Website anwenden.</span><span class="sxs-lookup"><span data-stu-id="82250-106">You can also find information about how to use the remote provisioning pattern to apply branding assets to a SharePoint site.</span></span>

## <a name="key-sharepoint-development-and-design-terms-and-concepts"></a><span data-ttu-id="82250-107">SharePoint-Taste Entwicklungs- und Begriffe und Konzepte</span><span class="sxs-lookup"><span data-stu-id="82250-107">Key SharePoint development and design terms and concepts</span></span>
<span data-ttu-id="82250-108"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="82250-108"></span></span>

|<span data-ttu-id="82250-109">**Begriff oder Konzept**</span><span class="sxs-lookup"><span data-stu-id="82250-109">**Term or concept**</span></span>|<span data-ttu-id="82250-110">**Definition**</span><span class="sxs-lookup"><span data-stu-id="82250-110">**Definition**</span></span>|<span data-ttu-id="82250-111">**Weitere Informationen**</span><span class="sxs-lookup"><span data-stu-id="82250-111">**More information**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="82250-112">Design-Manager</span><span class="sxs-lookup"><span data-stu-id="82250-112">Design Manager</span></span>|<span data-ttu-id="82250-113">Ein Feature in der SharePoint-Veröffentlichung Websites oder Teamwebsites mit aktivierter Veröffentlichung, die verwendet wird, importieren und Verwalten von Website-branding-Objekte und Exportieren eines entwurfspakets aktiviert.</span><span class="sxs-lookup"><span data-stu-id="82250-113">A feature activated in SharePoint publishing sites or Team sites with publishing enabled that is used to import and manage site branding assets and export them to a design package.</span></span>|<span data-ttu-id="82250-114">Mit Design Manager branding in anderen Tools wie Adobe PhotoShop oder Adobe DreamWeaver in SharePoint erstellten Objekte zu importieren.</span><span class="sxs-lookup"><span data-stu-id="82250-114">Use Design Manager to import branding assets created in other tools, such as Adobe PhotoShop or Adobe DreamWeaver, into SharePoint.</span></span><br/><span data-ttu-id="82250-115">SharePoint Designer ist nicht verfügbar für die Verwendung mit OneDrive für Unternehmen oder SharePoint Team-Websites, auf dem Veröffentlichung nicht aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="82250-115">SharePoint Designer is not available for use with OneDrive for Business or SharePoint Team sites where publishing is not enabled.</span></span>|
|<span data-ttu-id="82250-116">Design-Paket</span><span class="sxs-lookup"><span data-stu-id="82250-116">Design package</span></span>|<span data-ttu-id="82250-117">Für die Verwendung mit SharePoint 2013-Veröffentlichungswebsites vereinfacht, enthält der branding-Objekte, die im Entwurfs-Manager gespeichert sind.</span><span class="sxs-lookup"><span data-stu-id="82250-117">Designed for use with SharePoint 2013 Publishing sites, contains branding assets that are stored in Design Manager.</span></span>| [<span data-ttu-id="82250-118">SharePoint 2013 Design Manager Designpakete</span><span class="sxs-lookup"><span data-stu-id="82250-118">SharePoint 2013 Design Manager design packages</span></span>](http://msdn.microsoft.com/library/85ad1993-4d75-4806-9097-b934865a899a.aspx)|
|<span data-ttu-id="82250-119">Remotebereitstellung</span><span class="sxs-lookup"><span data-stu-id="82250-119">Remote provisioning</span></span>|<span data-ttu-id="82250-120">Ein Modell, bei dem Bereitstellen von Websites mithilfe von Vorlagen und Code, ausgeführt wird, außerhalb von SharePoint in einer vom Anbieter gehosteten-add-in.</span><span class="sxs-lookup"><span data-stu-id="82250-120">A model that involves provisioning sites by using templates and code that runs outside SharePoint in a provider-hosted add-in.</span></span>| [<span data-ttu-id="82250-121">Websitebereitstellungsmethoden und Remotebereitstellung in SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="82250-121">Site provisioning techniques and remote provisioning in SharePoint 2013</span></span>](http://blogs.msdn.com/b/vesku/archive/2013/08/23/site-provisioning-techniques-and-remote-provisioning-in-sharepoint-2013.aspx)<br/>[<span data-ttu-id="82250-122">Self-service Site-Bereitstellung von apps in SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="82250-122">Self-service site provisioning using apps in SharePoint 2013</span></span>](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/04/04/self-service-site-provisioning-using-apps-for-sharepoint-2013.aspx)|
|<span data-ttu-id="82250-123">Stammwebsite</span><span class="sxs-lookup"><span data-stu-id="82250-123">Root web</span></span>|<span data-ttu-id="82250-124">Das erste Web innerhalb einer Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="82250-124">The first web inside a site collection.</span></span> <span data-ttu-id="82250-125">Das Stammweb wird manchmal auch als the Web Application Root bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="82250-125">The root web is also sometimes referred to as the Web Application Root.</span></span>||
|<span data-ttu-id="82250-126">Sandkastenlösungen (engl.)</span><span class="sxs-lookup"><span data-stu-id="82250-126">Sandboxed solutions</span></span>|<span data-ttu-id="82250-127">WSP-Dateien, die enthalten Assemblys, andere nicht kompilierten Komponenten und eine XML-Manifestdatei.</span><span class="sxs-lookup"><span data-stu-id="82250-127">.wsp files that contain assemblies, other non-compiled components, and an XML manifest file.</span></span> <span data-ttu-id="82250-128">Eine Sandkasten-Lösung wird teilweise vertrauenswürdigem Code verwendet.</span><span class="sxs-lookup"><span data-stu-id="82250-128">A sandbox solution uses partial-trust code.</span></span>| [<span data-ttu-id="82250-129">Sandkastenlösungen (engl.)</span><span class="sxs-lookup"><span data-stu-id="82250-129">Sandboxed solutions</span></span>](https://msdn.microsoft.com/en-us/library/ff798382.aspx)|
|<span data-ttu-id="82250-130">SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="82250-130">SharePoint Designer 2013</span></span>|<span data-ttu-id="82250-131">Ein HTML-Designer und Entwurf Asset Management-Tools für die Verwaltung in SharePoint-branding-Elemente.</span><span class="sxs-lookup"><span data-stu-id="82250-131">An HTML designer and design asset management tool for managing branding elements in SharePoint.</span></span> <span data-ttu-id="82250-132">In SharePoint 2013 unterstützt SharePoint Designer hauptsächlich benutzerdefinierte Workflows.</span><span class="sxs-lookup"><span data-stu-id="82250-132">In SharePoint 2013, SharePoint Designer mainly supports custom workflows.</span></span>| [<span data-ttu-id="82250-133">Was ist in SharePoint Designer 2013 geändert?</span><span class="sxs-lookup"><span data-stu-id="82250-133">What's changed in SharePoint Designer 2013?</span></span>](https://msdn.microsoft.com/en-us/library/office/jj728659.aspx)<br/>[<span data-ttu-id="82250-134">What's new in SharePoint 2013-Websiteentwicklung?</span><span class="sxs-lookup"><span data-stu-id="82250-134">What's new with SharePoint 2013 site development?</span></span>](https://msdn.microsoft.com/en-us/library/office/jj163942.aspx)|
|<span data-ttu-id="82250-135">WSP-Datei</span><span class="sxs-lookup"><span data-stu-id="82250-135">.wsp file</span></span>|<span data-ttu-id="82250-136">Eine SharePoint-Lösungsdatei.</span><span class="sxs-lookup"><span data-stu-id="82250-136">A SharePoint solution file.</span></span> <span data-ttu-id="82250-137">Eine WSP-Datei ist eine CAB-Datei, die Website-Objekten kategorisiert und mit einer manifest.xml-Datei organisiert.</span><span class="sxs-lookup"><span data-stu-id="82250-137">A .wsp is a .cab file that categorizes site assets and organizes them with a manifest.xml file.</span></span>| [<span data-ttu-id="82250-138">Lösungsübersicht</span><span class="sxs-lookup"><span data-stu-id="82250-138">Solutions overview</span></span>](https://msdn.microsoft.com/en-us/library/office/aa543214%28v=office.14%29.aspx)|

## <a name="development-options"></a><span data-ttu-id="82250-139">Entwicklungsoptionen</span><span class="sxs-lookup"><span data-stu-id="82250-139">Development options</span></span>
<span data-ttu-id="82250-140"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="82250-140"></span></span>

<span data-ttu-id="82250-141">Wenn Sie SharePoint 2013 als Entwicklungsplattform verwenden, müssen Sie zum Erstellen einer Umgebung zum Entwickeln, testen, erstellen und Bereitstellen von Inhalten.</span><span class="sxs-lookup"><span data-stu-id="82250-141">When you use SharePoint 2013 as a development platform, you'll need to create an environment to develop, test, build, and deploy your content.</span></span> <span data-ttu-id="82250-142">Informationen zu den Optionen für die Entwicklung finden Sie unter [Überlegungen zur Entwicklungsumgebung](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx#DevEnvironment) in die [Anwendungslebenszyklus-Verwaltung von SharePoint Server 2013](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx)-Artikel.</span><span class="sxs-lookup"><span data-stu-id="82250-142">For information about the options for development, see  [Development environment considerations](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx#DevEnvironment) in the article [SharePoint Server 2013 Application Lifecycle Management](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx).</span></span> <span data-ttu-id="82250-143">In Tabelle 2 sind die Kriterien für die verschiedenen Entwicklungsoptionen.</span><span class="sxs-lookup"><span data-stu-id="82250-143">Table 2 lists the considerations for the various development options.</span></span> 

<span data-ttu-id="82250-144">**Optionen für die SharePoint-Entwicklung, testen und Abnahme**</span><span class="sxs-lookup"><span data-stu-id="82250-144">**Options for SharePoint development, testing, and acceptance**</span></span>

|<span data-ttu-id="82250-145">**Option**</span><span class="sxs-lookup"><span data-stu-id="82250-145">**Option**</span></span>|<span data-ttu-id="82250-146">**Überlegungen**</span><span class="sxs-lookup"><span data-stu-id="82250-146">**Considerations**</span></span>|
|:-----|:-----|
|<span data-ttu-id="82250-147">Team Foundation server</span><span class="sxs-lookup"><span data-stu-id="82250-147">Team foundation server</span></span>|<span data-ttu-id="82250-148">-Für den einfachen Zugriff auf Visual Studio Online befinden.</span><span class="sxs-lookup"><span data-stu-id="82250-148">- Located on Visual Studio Online for easy access.</span></span><br/><span data-ttu-id="82250-149">-Enthält eine zentrale Quelle Code und Lebenszyklus-Management-System.</span><span class="sxs-lookup"><span data-stu-id="82250-149">- Includes a centralized source code and life cycle management system.</span></span>|
|<span data-ttu-id="82250-150">Test und Abnahme Cloud-Umgebungen</span><span class="sxs-lookup"><span data-stu-id="82250-150">Cloud test and acceptance environments</span></span>|<span data-ttu-id="82250-151">-Verwenden Sie einen separaten Mandanten für Tests der Benutzerakzeptanz.</span><span class="sxs-lookup"><span data-stu-id="82250-151">- Use a separate tenant for acceptance testing.</span></span><br/><span data-ttu-id="82250-152">-Separate testumgebung für lokale testen.</span><span class="sxs-lookup"><span data-stu-id="82250-152">- Separate test environment for on-premises testing.</span></span>|
|<span data-ttu-id="82250-153">Lokale Test- und Akzeptanz Umgebungen</span><span class="sxs-lookup"><span data-stu-id="82250-153">On-premises test and acceptance environments</span></span>|<span data-ttu-id="82250-154">-Verwendung für lokale SharePoint-Bereitstellungen.</span><span class="sxs-lookup"><span data-stu-id="82250-154">- Use for on-premises SharePoint deployments.</span></span><br/><span data-ttu-id="82250-155">-Durch Kunden lokalen oder in Microsoft Azure gehostet.</span><span class="sxs-lookup"><span data-stu-id="82250-155">- Hosted by customer on-premises or in Microsoft Azure.</span></span>|
 
<span data-ttu-id="82250-156">In den meisten Fällen benötigen mindestens die folgenden Mandanten, Sie Obwohl dies je nach Ihren Anforderungen variieren kann:</span><span class="sxs-lookup"><span data-stu-id="82250-156">In most cases, you'll need at least the following tenants, although this can vary depending on your requirements:</span></span>

-  <span data-ttu-id="82250-157">**Entwickler-Mandanten**.</span><span class="sxs-lookup"><span data-stu-id="82250-157">**Developer tenant**.</span></span> <span data-ttu-id="82250-158">Es empfiehlt sich bereitstellen und Verwenden von Ihrer eigenen Developer Site.</span><span class="sxs-lookup"><span data-stu-id="82250-158">As a best practice, provision and use your own developer site.</span></span> <span data-ttu-id="82250-159">Auf diese Weise vermeiden Sie Ihre Daten mit der produktionsumgebung mischen.</span><span class="sxs-lookup"><span data-stu-id="82250-159">This way, you avoid mixing your data with the production environment.</span></span> <span data-ttu-id="82250-160">Melden Sie sich für und Bereitstellen einer Entwicklerwebsite, finden Sie unter [Sign up for an Office 365 Developer Site](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54.aspx#o365_signup) im Artikel [Melden Sie sich für ein Office 365 Developer-Abonnement und richten Sie Ihre Tools und die Umgebung](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54.aspx).</span><span class="sxs-lookup"><span data-stu-id="82250-160">To sign up for and provision a developer site, see  [Sign up for an Office 365 Developer Site](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54.aspx#o365_signup) in the article [Sign up for an Office 365 Developer Subscription and set up your tools and environment](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54.aspx).</span></span>
    
-  <span data-ttu-id="82250-161">**Integrationstests/Mandanten**.</span><span class="sxs-lookup"><span data-stu-id="82250-161">**Integration/testing tenant**.</span></span> <span data-ttu-id="82250-162">Verwenden Sie diese Website, um sicherzustellen, dass neue apps und Funktionen in mehr als eine Websitesammlung und gegen die Dienste und Daten in der produktionsumgebung funktionieren.</span><span class="sxs-lookup"><span data-stu-id="82250-162">Use this site to make sure that new apps and functionality work across more than one site collection and against the services and data in the production environment.</span></span> <span data-ttu-id="82250-163">Konfigurieren der Umgebung, um Funktionen enthalten, die in der Vorschau sind.</span><span class="sxs-lookup"><span data-stu-id="82250-163">Configure the environment to include capabilities that are in preview.</span></span> <span data-ttu-id="82250-164">(Dazu in Ihrem Mandanten-Verwaltungskonsole wählen Sie **Einstellungen für den Webdienst**, und wählen Sie dann unter der Einstellung für **Updates** , die **Erste Version**.) Visual Studio können online automatisierte Tests und alle anderen Fortlaufende Integrationstests ausführen.</span><span class="sxs-lookup"><span data-stu-id="82250-164">(To do this, in your tenant admin console, choose  **Service Settings**, and then under the  **Updates** setting, choose **First Release**.) You can use Visual Studio online to run automated testing and any other continuous integration testing.</span></span>
    
-  <span data-ttu-id="82250-165">**Produktionsmandanten**.</span><span class="sxs-lookup"><span data-stu-id="82250-165">**Production tenant**.</span></span> <span data-ttu-id="82250-166">Version getestet, akzeptiert und genehmigt apps, die diese Mandanten.</span><span class="sxs-lookup"><span data-stu-id="82250-166">Release tested, accepted, and approved apps to this tenant.</span></span> <span data-ttu-id="82250-167">Erstellen einer Entwicklerwebsite können Sie auf diesen Mandanten zu entwickeln und Testen von apps, die im Gültigkeitsbereich klein sind oder haben Auswirkungen isoliert.</span><span class="sxs-lookup"><span data-stu-id="82250-167">You can create a developer site on this tenant to develop and test apps that are small in scope or have isolated impact.</span></span> <span data-ttu-id="82250-168">Im Allgemeinen vermeiden Sie Ihren Umgebungen für Entwicklung und Produktion mischen.</span><span class="sxs-lookup"><span data-stu-id="82250-168">In general, avoid mixing your development and production environments.</span></span>
    
## <a name="design-tools"></a><span data-ttu-id="82250-169">Designtools</span><span class="sxs-lookup"><span data-stu-id="82250-169">Design tools</span></span>
<span data-ttu-id="82250-170"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="82250-170"></span></span>

<span data-ttu-id="82250-171">Mithilfe von standardmäßigen-Entwurf und Entwicklung Tools wie HTML, Bilder, CSS-Dateien und JavaScript-Dateien branding Anlagen SharePoint-Website erstellen.</span><span class="sxs-lookup"><span data-stu-id="82250-171">Use standard web design and development tools, such as HTML, images, CSS files, and JavaScript files to create SharePoint site branding assets.</span></span> <span data-ttu-id="82250-172">Beispielsweise können Sie Adobe DreamWeaver und Adobe PhotoShop entwerfen, die HTML, CSS, JavaScript und Bilddateien, mit denen Sie Ihre SharePoint-Websites mit Branding versehen werden.</span><span class="sxs-lookup"><span data-stu-id="82250-172">For example, you can use Adobe DreamWeaver and Adobe PhotoShop to design the HTML, CSS, JavaScript, and image files you'll use to brand your SharePoint sites.</span></span> <span data-ttu-id="82250-173">Alternativ können Sie SharePoint Designer 2013 erstellen, verwalten und Anpassen von Anlagen von branding oder erstellen benutzerdefinierte Lösungen in Visual Studio 2013 verwenden.</span><span class="sxs-lookup"><span data-stu-id="82250-173">Alternatively, you can use SharePoint Designer 2013 to create, manage, and customize branding assets, or create custom solutions in Visual Studio 2013.</span></span>

### <a name="sharepoint-design-packages-and-wsp-files"></a><span data-ttu-id="82250-174">SharePoint-Designpakete und WSP-Dateien</span><span class="sxs-lookup"><span data-stu-id="82250-174">SharePoint design packages and .wsp files</span></span>

<span data-ttu-id="82250-175">Designpakete sind durch Entwurfs-Manager erstellte WSP-Dateien, die vorhersehbare Regeln für die Verpackung Entwurfsressourcen einhalten.</span><span class="sxs-lookup"><span data-stu-id="82250-175">Design packages are .wsp files created by Design Manager that follow predictable rules for packaging design assets.</span></span> <span data-ttu-id="82250-176">Sie sind im Wesentlichen sandboxed Solutions.</span><span class="sxs-lookup"><span data-stu-id="82250-176">They are, essentially, sandboxed solutions.</span></span> <span data-ttu-id="82250-177">Wenn Sie ein anderes Tool Paket branding-Objekte in eine WSP-Datei verwenden, werden Ihre branding Anlagen in einem Zustand weniger festen und vorhersehbar bleibt.</span><span class="sxs-lookup"><span data-stu-id="82250-177">If you're using another tool to package branding assets in a .wsp file, your branding assets will be in a less fixed and predictable state.</span></span>

<span data-ttu-id="82250-178">Das Design-Paket enthält alle Dateien, die angepasst wurden.</span><span class="sxs-lookup"><span data-stu-id="82250-178">The design package includes all files that have been customized.</span></span> <span data-ttu-id="82250-179">Wenn Sie ein Seitenlayout, die einen benutzerdefinierten Inhaltstyp verwendet wird erstellen, umfasst das Design-Paket beispielsweise das Seitenlayout, den benutzerdefinierten Inhaltstyp verwendeten und alle benutzerdefinierten Websitespalten.</span><span class="sxs-lookup"><span data-stu-id="82250-179">For example, if you create a page layout that uses a custom content type, the design package includes the page layout, the custom content type it uses, and all custom site columns.</span></span> <span data-ttu-id="82250-180">Das Design-Paket enthält auch mehrere Dateien im Zusammenhang mit jeder zusammengesetzten, die auf der SharePoint-Website, einschließlich Dateien, die an den folgenden Orten hochgeladen angewendet wurden:</span><span class="sxs-lookup"><span data-stu-id="82250-180">The design package also includes several files related to any composed looks that have been applied to your SharePoint site, including files uploaded to the following locations:</span></span>

- <span data-ttu-id="82250-181">Website-Ressourcen-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="82250-181">Site assets library</span></span>
    
- <span data-ttu-id="82250-182">Formatbibliothek</span><span class="sxs-lookup"><span data-stu-id="82250-182">Style library</span></span>
    
- <span data-ttu-id="82250-183">Masterseitenkatalog</span><span class="sxs-lookup"><span data-stu-id="82250-183">Master Page gallery</span></span>
    
<span data-ttu-id="82250-184">Falls zusammengesetzten werden auf eine Website angewendet, bevor Sie benutzerdefiniertes branding angewendet wird, muss das Design-Paket-Dateien mit .themedcss und .themedpng Dateierweiterungen enthalten.</span><span class="sxs-lookup"><span data-stu-id="82250-184">If you applied composed looks to a site before you applied custom branding, the design package will include files with .themedcss and .themedpng file extensions.</span></span> <span data-ttu-id="82250-185">Zum Anwenden der branding-Objekte in einem Paket Design auf einer SharePoint-Website exportieren Sie das Design-Paket, und verwenden Sie das remote provisioning Muster, um den Inhalt des designpakets übernehmen.</span><span class="sxs-lookup"><span data-stu-id="82250-185">To apply the branding assets in a design package to a SharePoint site, export the design package and use the remote provisioning pattern to apply the contents of the design package.</span></span>

<span data-ttu-id="82250-186">SharePoint 2013 enthält die APIs, die Sie verwenden können, Designpakete entwickelt.</span><span class="sxs-lookup"><span data-stu-id="82250-186">SharePoint 2013 includes the APIs that you can use to work with design packages.</span></span> <span data-ttu-id="82250-187">Wenn Sie entweder SSOM, CSOM oder JSOM verwenden, können Sie die Klassen [DesignPackage](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.aspx) oder [DesignPackageInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.designpackageinfo.aspx) verwenden.</span><span class="sxs-lookup"><span data-stu-id="82250-187">If you're using either SSOM, CSOM, or JSOM, you can use the  [DesignPackage](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.aspx) or [DesignPackageInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.designpackageinfo.aspx) classes.</span></span>

#### <a name="using-the-design-package-csom-to-apply-the-contents-of-design-packages-to-a-sharepoint-site"></a><span data-ttu-id="82250-188">Mithilfe des entwurfspakets CSOM den Inhalt der Designpakete auf einer SharePoint-Website anwenden</span><span class="sxs-lookup"><span data-stu-id="82250-188">Using the design package CSOM to apply the contents of design packages to a SharePoint site</span></span>

<span data-ttu-id="82250-189">Das folgende Beispiel veranschaulicht die Design-Paket-APIs in das remote provisioning Muster verwenden, um den Inhalt der Designpakete auf einer SharePoint-Website anwenden.</span><span class="sxs-lookup"><span data-stu-id="82250-189">The following example shows how to use the Design Package APIs in the remote provisioning pattern to apply the contents of design packages to a SharePoint site.</span></span>

<span data-ttu-id="82250-190">Dieser Code wurde für die Verwendung mit Veröffentlichungswebsites entwickelt.</span><span class="sxs-lookup"><span data-stu-id="82250-190">This code was designed for use with Publishing sites.</span></span> <span data-ttu-id="82250-191">Es ist zwar möglich, die Design-Pakete-API verwenden, einem Branding Teamwebsites, die dem Standardseitenlayout Feature aktiviert ist, kann dies langfristige Supportanfragen führen.</span><span class="sxs-lookup"><span data-stu-id="82250-191">Although it is possible to use the Design Packages API to apply branding to Team sites that have the Publishing feature enabled, this can introduce long-term support issues.</span></span>

<span data-ttu-id="82250-192">**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.</span><span class="sxs-lookup"><span data-stu-id="82250-192">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```
using Microsoft.SharePoint.Client;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Microsoft.SharePoint.Client.Publishing;
namespace ProviderSharePointAppWeb
{
    public partial class Default : System.Web.UI.Page
    {
        protected void Page_PreInit(object sender, EventArgs e)
        {
            Uri redirectUrl;
            switch (SharePointContextProvider.CheckRedirectionStatus(Context, out redirectUrl))
            {
                case RedirectionStatus.Ok:
                    return;
                case RedirectionStatus.ShouldRedirect:
                    Response.Redirect(redirectUrl.AbsoluteUri, endResponse: true);
                    break;
                case RedirectionStatus.CanNotRedirect:
                    Response.Write("An error occurred while processing your request.");
                    Response.End();
                    break;
            }
        }

        protected void Page_Load(object sender, EventArgs e)
        {
            // Use TokenHelper to get the client context and Title property.
            // To access other properties, the add-in might need to request permissions
            // on the host web.
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            
            // Publishing feature GUID to use the infrastructure for publishing. 
            Guid PublishingFeature = Guid.Parse("f6924d36-2fa8-4f0b-b16d-06b7250180fa");

            // The site-relative URL of the design package to install.
            // This sandbox design package should be uploaded to a document library.
            // For practical purposes, this can be a configuration setting in web.config.
            string fileRelativePath = @"/sites/devsite/brand/Dev.wsp";

            //string fileUrl = @"https://SPXXXXX.com/sites/devsite/brand/Dev.wsp";
            
        
            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                // Load the site context explicitly or while installing the API, the path for
// the package will not be resolved.
                // If the package cannot be found, an exception is thrown. 
                var site = clientContext.Site;
                clientContext.Load(site);
                clientContext.ExecuteQuery();
              
                // Validate whether the Publishing feature is active. 
                if (IsSiteFeatureActivated(clientContext,PublishingFeature))
                {
                    DesignPackageInfo info = new DesignPackageInfo()
                    {
                        PackageGuid = Guid.Empty,
                        MajorVersion = 1,
                        MinorVersion = 1,
                        PackageName = "Dev"
                    };
                    Console.WriteLine("Installing design package ");
                    
                    DesignPackage.Install(clientContext, clientContext.Site, info, fileRelativePath);
                    clientContext.ExecuteQuery();

                    Console.WriteLine("Applying design package");
                    DesignPackage.Apply(clientContext, clientContext.Site, info);
                    clientContext.ExecuteQuery();
                }
            }
        }
        public  bool IsSiteFeatureActivated( ClientContext context, Guid guid)
        {
            var features = context.Site.Features;
            context.Load(features);
            context.ExecuteQuery();

            foreach (var f in features)
            {
                if (f.DefinitionId.Equals(guid))
                    return true;
            }
            return false;
        }
 
    }
}
```

#### <a name="using-filecreationinformation-to-upload-branding-assets-and-a-master-page-to-a-team-site"></a><span data-ttu-id="82250-193">Verwenden komplexer FileCreationInformation zum Hochladen von Anlagen von branding und einer Gestaltungsvorlage auf eine Teamwebsite</span><span class="sxs-lookup"><span data-stu-id="82250-193">Using FileCreationInformation to upload branding assets and a master page to a Team site</span></span>

<span data-ttu-id="82250-194">Funktionen von SharePoint 2013-Clientobjektmodell können zum Installieren und deinstallieren Designpakete und Exportieren von Designpakete in SharePoint Online-Websites.</span><span class="sxs-lookup"><span data-stu-id="82250-194">You can use SharePoint 2013 CSOM functionality to install and uninstall design packages and export design packages to SharePoint Online sites.</span></span> <span data-ttu-id="82250-195">Verwenden Sie beispielsweise die [SP. Publishing.DesignPackage.install-Methode (sp.publishing)](http://msdn.microsoft.com/library/26500127-210f-6c52-c0de-cf2894939a91.aspx) , klicken Sie auf der Website das Design-Paket zu installieren, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="82250-195">For example, use the  [SP.Publishing.DesignPackage.install Method (sp.publishing)](http://msdn.microsoft.com/library/26500127-210f-6c52-c0de-cf2894939a91.aspx) to install the design package on the site, as shown in the following example.</span></span>

```
public static void Install(
        ClientRuntimeContext context,
        Site site,
        DesignPackageInfo info,
        string path
)
```

<span data-ttu-id="82250-196">Die [DesignPackageInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.designpackageinfo.aspx) -Klasse gibt Metadaten, die beschreiben, den Inhalt des designpakets installiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="82250-196">The  [DesignPackageInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.designpackageinfo.aspx) class specifies metadata that describe the contents of the design package to be installed.</span></span> <span data-ttu-id="82250-197">Verwenden Sie die [Uninstall](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.uninstall.aspx) -Methode zum Deinstallieren des designpakets von der Website, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="82250-197">Use the [Uninstall](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.uninstall.aspx) method to uninstall the design package from the site, as shown in the following example.</span></span>

```
public static void UnInstall(
        ClientRuntimeContext context,
        Site site,
        DesignPackageInfo info
)
```

<span data-ttu-id="82250-198">Wenn Sie mit der Veröffentlichung eine Teamwebsite mit Branding versehen müssen feature aktiviert ist, oder eine Veröffentlichung Website auf SharePoint Online, können die [ExportEnterprise](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.exportenterprise.aspx) oder die [ExportSmallBusiness](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.exportsmallbusiness.aspx) -Methode zum Exportieren von Designpakete für Websitevorlagen in der Lösung Katalog.</span><span class="sxs-lookup"><span data-stu-id="82250-198">If you need to brand a Team site with the Publishing feature enabled, or a Publishing site on SharePoint Online, you can use the  [ExportEnterprise](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.exportenterprise.aspx) or the [ExportSmallBusiness](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.exportsmallbusiness.aspx) method to export design packages for site templates to the Solution Gallery.</span></span> <span data-ttu-id="82250-199">Verwenden Sie die **ExportSmallBusiness** -Methode mit der small Business-Websitevorlage, und verwenden Sie die Methode **ExportEnterprise** für alle anderen Websitevorlagen, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="82250-199">Use the **ExportSmallBusiness** method with the small business site template, and use the **ExportEnterprise** method for all other site templates, as shown in the following example.</span></span> <span data-ttu-id="82250-200">Im Beispiel ist Hinweis ThatpackageName eine Zeichenfolge, die den Namen des entwurfspakets darstellt.</span><span class="sxs-lookup"><span data-stu-id="82250-200">In the example, note thatpackageName is a string that represents the name of the design package.</span></span>

```
public static ClientResult<DesignPackageInfo> ExportEnterprise(
        ClientRuntimeContext context,
        Site site,
        bool includeSearchConfiguration
)
```

<span data-ttu-id="82250-201">Wenn Sie diese Methode verwenden, können Sie die Suchkonfiguration in das Design-Paket einschließen, wie im nächsten Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="82250-201">When you use this method, you can include the search configuration in the design package, as shown in the next example.</span></span> <span data-ttu-id="82250-202">Beachten Sie, dass alle Design Paket Methoden auf der Ebene der Websitesammlung ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="82250-202">Note that all design package methods operate at the level of the site collection.</span></span>

```
public static ClientResult<DesignPackageInfo> ExportSmallBusiness(
        ClientRuntimeContext context,
        Site site,
        string packageName,
        bool includeSearchConfiguration
)
```

## <a name="design-tool-options-for-sharepoint-online"></a><span data-ttu-id="82250-203">Tool Entwurfsoptionen für SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="82250-203">Design tool options for SharePoint Online</span></span>
<span data-ttu-id="82250-204"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="82250-204"></span></span>

<span data-ttu-id="82250-205">Die Tools, die Sie verwenden können, um eine SharePoint Online-Website mit Branding versehen ist abhängig von Ihrer SharePoint Online-Edition und den Typ der Website, den Sie erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="82250-205">The tools you can use to brand a SharePoint Online site depend on your SharePoint Online edition and the type of site you want to build.</span></span> <span data-ttu-id="82250-206">Die Small Business Edition enthält beispielsweise eine Teamwebsite und eine öffentliche Website.</span><span class="sxs-lookup"><span data-stu-id="82250-206">The Small Business edition, for example, includes one Team site and one public site.</span></span> <span data-ttu-id="82250-207">Enthält keine Veröffentlichung Website.</span><span class="sxs-lookup"><span data-stu-id="82250-207">It does not include a Publishing site.</span></span> <span data-ttu-id="82250-208">Des Website-Generator-add-Ins können in SharePoint Online öffentliche Websitebranding anpassen.</span><span class="sxs-lookup"><span data-stu-id="82250-208">You can use the Site Builder add-in in SharePoint Online to customize public site branding.</span></span>

<span data-ttu-id="82250-209">Die Enterprise Edition enthält eine teamwebsitesammlung am Stamm Webanwendung an, für die Domäne, die Veröffentlichung nicht enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="82250-209">The Enterprise edition includes a Team site collection at the root web application for the domain that does not include Publishing.</span></span> <span data-ttu-id="82250-210">Es ist nicht öffentliche Website enthalten.</span><span class="sxs-lookup"><span data-stu-id="82250-210">It does not include a public site.</span></span> <span data-ttu-id="82250-211">Verwendung Entwurfs-Manager zum Verwalten von SharePoint-Website-branding-Elemente für die Veröffentlichung der Website in der SharePoint Online Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="82250-211">Use Design Manager to manage SharePoint site branding elements for the Publishing site in the SharePoint Online Enterprise edition.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="82250-212">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="82250-212">Additional resources</span></span>
<span data-ttu-id="82250-213"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="82250-213"></span></span>

-  [<span data-ttu-id="82250-214">Branding und Bereitstellen von Lösungen für SharePoint 2013 und SharePoint Online-Website</span><span class="sxs-lookup"><span data-stu-id="82250-214">Branding and site provisioning solutions for SharePoint 2013 and SharePoint Online</span></span>](Branding-and-site-provisioning-solutions-for-SharePoint.md)
    
-  [<span data-ttu-id="82250-215">Anwendungslebenszyklus-Verwaltung in SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="82250-215">SharePoint Server 2013 Application Lifecycle Management</span></span>](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx)
    
-  [<span data-ttu-id="82250-216">Sandkastenlösungen (engl.)</span><span class="sxs-lookup"><span data-stu-id="82250-216">Sandboxed solutions</span></span>](https://msdn.microsoft.com/en-us/library/ff798382.aspx)
    
-  [<span data-ttu-id="82250-217">Websitebereitstellungsmethoden und Remotebereitstellung in SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="82250-217">Site provisioning techniques and remote provisioning in SharePoint 2013</span></span>](http://blogs.msdn.com/b/vesku/archive/2013/08/23/site-provisioning-techniques-and-remote-provisioning-in-sharepoint-2013.aspx)
    
-  [<span data-ttu-id="82250-218">SharePoint 2013 Design Manager Designpakete</span><span class="sxs-lookup"><span data-stu-id="82250-218">SharePoint 2013 Design Manager design packages</span></span>](http://msdn.microsoft.com/library/85ad1993-4d75-4806-9097-b934865a899a.aspx)
