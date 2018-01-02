---
title: "Hosten clientseitiger Webparts in Office 365 CDN"
ms.date: 12/11/2017
ms.prod: sharepoint
ms.openlocfilehash: 3abc6748269fe9709678c6b02b514662cc156587
ms.sourcegitcommit: 6018dbb696faef5f60ebf0f79f830385fab2a4d8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/11/2017
---
# <a name="hosting-client-side-web-part-from-office-365-cdn-hello-world-part-4"></a><span data-ttu-id="3713d-102">Hosten clientseitiger Webparts in Office 365 CDN (Hello Word, Teil 4)</span><span class="sxs-lookup"><span data-stu-id="3713d-102">Hosting extension from Office 365 CDN (Hello world part 4)</span></span>

<span data-ttu-id="3713d-p101">In diesem Artikel wird beschrieben, wie Sie clientseitige Webparts in Office 365 CDN hosten. Office 365 CDN ist eine einfache Lösung, mit der Sie Ihre Ressourcen direkt in Ihrem eigenen Office 365-Mandanten hosten können. Es können beliebige statische Ressourcen gehostet werden, die in SharePoint Online verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="3713d-p101">This article describes how to host your client-side web part from Office 365 CDN. Office 365 CDN provide you easy solution to host your assets directly from your own Office 365 tenant. It can be used for hosting any static assets, which are used in SharePoint Online. You can find more details around the Office 365 CDN capability from following blog post.</span></span> 

> [!NOTE]
> <span data-ttu-id="3713d-106">Es gibt mehrere unterschiedliche Hostingoptionen für Webpart-Objekte.</span><span class="sxs-lookup"><span data-stu-id="3713d-106">There are multiple different hosting options for your web part assets.</span></span> <span data-ttu-id="3713d-107">In diesem Lernprogramm steht die Option „Office 365 CDN“ im Vordergrund, Sie können jedoch auch das [Azure CDN](./deploy-web-part-to-cdn.md) verwenden oder einfach Ihre Objekte aus der SharePoint-Bibliothek aus dem Mandanten hosten.</span><span class="sxs-lookup"><span data-stu-id="3713d-107">This tutorial concentrates on showing the Azure CDN option, but you could also use the [Office 365 CDN](./deploy-web-part-to-cdn.md) or simply host your assets from SharePoint library from your tenant.</span></span> <span data-ttu-id="3713d-108">Im letzteren Fall würden Sie nicht von den CDN-Leistungssteigerungen profitieren, im Hinblick auf die Funktionalität wäre dies jedoch möglich.</span><span class="sxs-lookup"><span data-stu-id="3713d-108">In the latter case, you would not benefit from the CDN performance improvements, but that would also work from the functionality perspective.</span></span> <span data-ttu-id="3713d-109">Technisch gesehen wäre jeder Ort zum Hosten der Objekte für Endbenutzer denkbar, auf den Endbenutzer über HTTP(S) zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="3713d-109">Any location which end users can access using HTTP would be technically suitable for hosting the assets for end users.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3713d-110">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="3713d-110">Prerequisites</span></span>

<span data-ttu-id="3713d-111">Führen Sie die folgenden Schritte aus, bevor Sie starten:</span><span class="sxs-lookup"><span data-stu-id="3713d-111">Make sure that you have completed the following tasks before you begin:</span></span>

* [<span data-ttu-id="3713d-112">Erstellen des ersten clientseitigen Webparts</span><span class="sxs-lookup"><span data-stu-id="3713d-112">Build your first client-side web part</span></span>](./build-a-hello-world-web-part.md)
* [<span data-ttu-id="3713d-113">Verbinden des clientseitigen Webparts mit SharePoint</span><span class="sxs-lookup"><span data-stu-id="3713d-113">Connect your client-side web part to SharePoint</span></span>](./connect-to-sharepoint.md)
* [<span data-ttu-id="3713d-114">Bereitstellen des clientseitigen SharePoint-Webparts auf einer klassischen SharePoint-Seite</span><span class="sxs-lookup"><span data-stu-id="3713d-114">Deploy your client-side web part to a classic SharePoint page</span></span>](./serve-your-web-part-in-a-sharepoint-page.md)


<span data-ttu-id="3713d-115">Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=MEZMs8VMVQ0&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq) nachvollziehen:</span><span class="sxs-lookup"><span data-stu-id="3713d-115">You can also follow follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=MEZMs8VMVQ0&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span></span>

<a href="https://www.youtube.com/watch?v=MEZMs8VMVQ0&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq">
<img src="../../../images/spfx-youtube-tutorial4.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>



## <a name="enable-cdn-in-your-office-365-tenant"></a><span data-ttu-id="3713d-116">Aktivieren von CDN in Ihrem Office 365-Mandanten</span><span class="sxs-lookup"><span data-stu-id="3713d-116">Enable CDN in your Office 365 tenant</span></span>
<span data-ttu-id="3713d-117">Stellen Sie sicher, dass Sie die neueste Version der SharePoint Online-Verwaltungsshell verwenden. Herunterladen können Sie sie im [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span><span class="sxs-lookup"><span data-stu-id="3713d-117">Ensure that you have latest version of the SharePoint Online Management Shell by downloading it from [Microsoft Download site](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span>

> [!TIP]
> <span data-ttu-id="3713d-118">Wenn Sie keinen Windows-Computer verwenden, können Sie die SPO-Verwaltungsshell nicht verwenden.</span><span class="sxs-lookup"><span data-stu-id="3713d-118">If you are using non-Windows machine, you cannot use the SPO Management Shell.</span></span> <span data-ttu-id="3713d-119">Sie können diese Einstellungen jedoch über die [Office 365 CLI](https://sharepoint.github.io/office365-cli/) verwalten.</span><span class="sxs-lookup"><span data-stu-id="3713d-119">You can however manage these settings using [Office 365 CLI](https://sharepoint.github.io/office365-cli/).</span></span>

<span data-ttu-id="3713d-120">Verbinden Sie sich über eine PowerShell-Sitzung mit Ihrem SharePoint Online-Mandanten.</span><span class="sxs-lookup"><span data-stu-id="3713d-120">Connect to your SharePoint Online tenant with PowerShell session.</span></span>
```
Connect-SPOService -Url https://contoso-admin.sharepoint.com
```

<span data-ttu-id="3713d-121">Führen Sie nacheinander die folgenden Befehle aus, um den aktuellen Status der auf Mandantenebene festgelegten Einstellungen für öffentliche CDNs abzurufen:</span><span class="sxs-lookup"><span data-stu-id="3713d-121">Get current status of public CDN settings from tenant level by executing following commands one-by-one.</span></span> 
```
Get-SPOTenantCdnEnabled -CdnType Public
Get-SPOTenantCdnOrigins -CdnType Public
Get-SPOTenantCdnPolicies -CdnType Public
```
<span data-ttu-id="3713d-122">Aktivieren Sie öffentliche CDNs im Mandanten</span><span class="sxs-lookup"><span data-stu-id="3713d-122">Enable public CDN in the tenant</span></span>
```
Set-SPOTenantCdnEnabled -CdnType Public
```
<span data-ttu-id="3713d-123">Bestätigen Sie Einstellungen, indem Sie „Y“ wählen und Sie **EINGABETASTE** drücken.</span><span class="sxs-lookup"><span data-stu-id="3713d-123">Confirm settings by selecting 'Y' and pressing **Enter**</span></span>

![Aktivieren Sie öffentliche CDNs im Mandanten](../../../images/cdn-enable-o365-public-cdn.png)

<span data-ttu-id="3713d-p104">Jetzt sind öffentliche CDNs im Mandanten aktiviert, mit der Standardkonfiguration für zulässige Dateitypen. Dies bedeutet, dass die folgenden Dateitypen unterstützt werden: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF und WOFF.</span><span class="sxs-lookup"><span data-stu-id="3713d-p104">Now public CDN has been enabled in the tenant using the default file type configuration allowed. This means that the following file type extensions are supported: "CSS,EOT,GIF,ICO,JPEG,JPG,JS,MAP,PNG,SVG,TTF,WOFF".</span></span>

<span data-ttu-id="3713d-127">SharePoint-Framework-Lösungen können automatisch von den öffentlichen CDNs in Office 365 profitieren, solange diese in Ihrem Mandanten aktiviert sind.</span><span class="sxs-lookup"><span data-stu-id="3713d-127">SharePoint Framework solutions can automatically benefit from the Office 365 Public CDN as long as it's enabled in your tenant.</span></span> <span data-ttu-id="3713d-128">Wenn CDN aktiviert ist, wird der `*/CLIENTSIDEASSETS`-Ursprung automatisch als gültiger Ursprung hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="3713d-128">When CDN is enabled, `*/CLIENTSIDEASSETS` origin is automatically added as valid a valid origin.</span></span>

> [!NOTE]
> <span data-ttu-id="3713d-129">Wenn Sie zuvor Office 365 CDN aktiviert haben, sollten Sie das öffentliche CDN erneut aktivieren, damit der `*/CLIENTSIDEASSETS`-Eintrag als gültiger CDN-Ursprung für das öffentliche CDN hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="3713d-129">If you have previously enabled Office 365 CDN, you should re-enable the public CDN, so that you will have the `*/CLIENTSIDEASSETS`entry added as valid CDN origin for public CDN.</span></span>

<span data-ttu-id="3713d-130">Sie können die aktuelle Konfiguration Ihrer Endpunkte nochmals prüfen. Führen Sie den folgenden Befehl aus, um die Liste der CDN-Ursprünge aus Ihrem Mandanten abzurufen.</span><span class="sxs-lookup"><span data-stu-id="3713d-130">You can double check the current setup of your end-points.Execute the following command to get the list of CDN origins from your tenant</span></span>
```
Get-SPOTenantCdnOrigins -CdnType Public
```
<span data-ttu-id="3713d-p106">Sie sehen, dass der neu hinzugefügte Ursprung als gültiger CDN-Ursprung aufgeführt ist. Die endgültige Konfiguration des Ursprungs dauert einige Zeit (ca. 15 Minuten). Während Sie warten, können Sie ein Testwebpart erstellen, das nach Abschluss der Bereitstellung im Ursprung gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="3713d-p106">Notice that your newly added origin is listed as a valid CDN origin. Final configuration of the origin will take a while (approximately 15 minutes), so we can continue by creating your test web part, which will be hosted from the origin, when the deployment is completed.</span></span> 

![Liste der öffentlichen Ursprünge im Mandanten](../../../images/cdn-public-origins.png)

> [!NOTE]
> <span data-ttu-id="3713d-134">Sobald ein Ursprung nicht mehr mit *(Konfiguration steht aus)* gekennzeichnet ist, kann er in Ihrem Mandanten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="3713d-134">When origin is listed without the *(configuration pending)* text, it is ready to be used in your tenant.</span></span> <span data-ttu-id="3713d-135">Dieser Text weist auf laufende Konfigurationsaktivitäten zwischen SharePoint Online und dem CDN-System hin.</span><span class="sxs-lookup"><span data-stu-id="3713d-135">This is the indication of an on-going configuration between SharePoint Online and CDN system.</span></span> 


## <a name="project-directory"></a><span data-ttu-id="3713d-136">Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="3713d-136">Project directory</span></span>

<span data-ttu-id="3713d-137">Wechseln Sie zur Konsole, und stellen Sie sicher, dass Sie sich noch in dem Projektverzeichnis befinden, das Sie zum Einrichten des Webpart-Projekts verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="3713d-137">Switch to console and make sure you are still in the project directory you used to set up your web part project.</span></span>

<span data-ttu-id="3713d-138">Beenden Sie die Aufgabe **gulp serve**, indem Sie **STRG + C** auswählen, und wechseln Sie zu Ihrem Projektverzeichnis:</span><span class="sxs-lookup"><span data-stu-id="3713d-138">End the possible **gulp serve** task by choosing **Ctrl+C** and ensure that you are in your project directory:</span></span>

```
cd helloworld-webpart
```

# <a name="review-solution-settings"></a><span data-ttu-id="3713d-139">Prüfen von Projektmappeneinstellungen</span><span class="sxs-lookup"><span data-stu-id="3713d-139">Review solution settings</span></span> 

<span data-ttu-id="3713d-140">Öffnen Sie das **HelloWorldWebPart**-Webpart-Projekt in Visual Studio Code oder in Ihrer bevorzugten IDE.</span><span class="sxs-lookup"><span data-stu-id="3713d-140">Open the **HelloWorldWebPart** web part project in Visual Studio Code, or your preferred IDE.</span></span>

<span data-ttu-id="3713d-141">Öffnen Sie **package-solution.json** im Ordner **config**.</span><span class="sxs-lookup"><span data-stu-id="3713d-141">Open **package-solution.json** from the **config** folder.</span></span>

<span data-ttu-id="3713d-142">Die Datei **package-solution.json** definiert die Paketmetadaten, wie im folgenden Code dargestellt:</span><span class="sxs-lookup"><span data-stu-id="3713d-142">The **package-solution.json** file defines the package metadata as shown in the following code:</span></span>

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
  "solution": {
    "name": "helloworld-webpart-client-side-solution",
    "id": "4432f33b-5845-4ca0-827e-a8ae68c7b945",
    "version": "1.0.0.0",
    "includeClientSideAssets": true
  },
  "paths": {
    "zippedPackage": "solution/helloworld-webpart.sppkg"
  }
}

```

<span data-ttu-id="3713d-143">Standardwert für **includeClientSideAssets** ist `true`. Dies bedeutet, dass statische Objekte automatisch in den *.sppkg*-Dateien gepackt werden und nicht separat von einem externen System gehostet werden müssen.</span><span class="sxs-lookup"><span data-stu-id="3713d-143">Default value for the **includeClientSideAssets** is `true`, which means that static assets are packaged automatically inside of the *.sppkg* files and you do not need to separately host your assets from external system.</span></span> 

<span data-ttu-id="3713d-144">Wenn *Office 365 CDN* aktiviert ist, werden automatisch die Standardeinstellungen verwendet.</span><span class="sxs-lookup"><span data-stu-id="3713d-144">If *Office 365 CDN* is enabled, it will be used automatically with default settings.</span></span> <span data-ttu-id="3713d-145">Wenn *Office 365 CDN* nicht aktiviert ist, werden Objekte von der App-Katalog-Websitesammlung bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="3713d-145">If *Office 365 CDN* is not enabled, assets will be served from app catalog site collection.</span></span> 

> [!NOTE]
> <span data-ttu-id="3713d-146">Ab SharePoint-Framework v1. 4 werden statische Objekte standardmäßig in das .sppkg-Paket gepackt.</span><span class="sxs-lookup"><span data-stu-id="3713d-146">Starting from the SharePoint Framework v1.4, static assets are by default packaged inside of the sppkg package.</span></span> <span data-ttu-id="3713d-147">Wenn das Paket im App-Katalog bereitgestellt wird, werden sie automatisch in Office 365 CDN (falls aktiviert) oder in der App-Katalog-URL gehostet.</span><span class="sxs-lookup"><span data-stu-id="3713d-147">When package is deployed in app catalog, they are automatically being hosted either from Office 365 CDN (if enabled) or from app catalog URL.</span></span> <span data-ttu-id="3713d-148">Sie können dieses Verhalten mit der `includeClientSideAssets`-Einstellung in der `package-solution.json`-Datei steuern.</span><span class="sxs-lookup"><span data-stu-id="3713d-148">You can control this behavior with the `includeClientSideAssets` setting in `package-solution.json` file.</span></span>

## <a name="prepare-web-part-assets-to-deploy"></a><span data-ttu-id="3713d-149">Vorbereiten der bereitzustellenden Webpartressourcen</span><span class="sxs-lookup"><span data-stu-id="3713d-149">Prepare web part assets to deploy</span></span>

<span data-ttu-id="3713d-150">Führen Sie die folgenden Aufgaben aus, um Ihre Lösung in einem Bundle zu verpacken.</span><span class="sxs-lookup"><span data-stu-id="3713d-150">Execute the following tasks to bundle your solution</span></span>
* <span data-ttu-id="3713d-151">Dadurch wird ein Versionsbuild des Projekts ausgeführt, indem eine dynamische Bezeichnung als die Host-URL für Ihre Objekte verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="3713d-151">This will execute a release build of your project by using a dynamic label as the host URL for your assets.</span></span> <span data-ttu-id="3713d-152">Diese URL wird automatisch auf Grundlage Ihrer CDN-Mandanteneinstellungen aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="3713d-152">This URL will be automatically updated based on your tenant CDN settings.</span></span>

```
gulp bundle --ship
```

<span data-ttu-id="3713d-153">Führen Sie die folgende Aufgaben aus, um Ihre Lösung zu packen.</span><span class="sxs-lookup"><span data-stu-id="3713d-153">Execute the following task to package your solution</span></span>

```
gulp package-solution --ship
```

<span data-ttu-id="3713d-154">Mit diesem Befehl wird ein aktualisiertes **helloworld-webpart.sppkg**-Paket im Ordner **sharepoint/solution** erstellt.</span><span class="sxs-lookup"><span data-stu-id="3713d-154">This command will create an updated **helloworld-webpart.sppkg** package on the **sharepoint/solution** folder.</span></span>

> [!NOTE]
> <span data-ttu-id="3713d-155">Informationen zu den Elementen, die in die .sppkg-Datei gepackt werden, finden Sie in dem Ordner **sharepoint/solution/debug**.</span><span class="sxs-lookup"><span data-stu-id="3713d-155">If you are interested on what actually got packaged inside of the sppkg file, you can have a look omn the content of the **sharepoint/solution/debug** folder.</span></span>

<span data-ttu-id="3713d-156">Laden Sie das neu erstellte Paket mit ihrer clientseitigen Lösung in den App-Katalog in Ihrem Mandanten hoch. Alternativ können Sie es auch per Drag & Drop verschieben.</span><span class="sxs-lookup"><span data-stu-id="3713d-156">Upload or drag & drop the newly created client-side solution package to the app catalog in your tenant.</span></span> 

<span data-ttu-id="3713d-157">Da Sie das Paket bereits bereitgestellt haben, werden Sie gefragt, ob das vorhandene Paket ersetzt werden soll.</span><span class="sxs-lookup"><span data-stu-id="3713d-157">Because you already  deployed the package, you will be prompted as to whether to replace the existing package.</span></span>

![Überschreiben einer vorhandenen Lösung](../../../images/cdn-override-helloworld-webpart-package.png)

<span data-ttu-id="3713d-159">Wählen Sie „Ersetzen“.</span><span class="sxs-lookup"><span data-stu-id="3713d-159">Choose Replace it.</span></span>

![Im App-Katalog angezeigtes Installationspopup für die SPFx-Lösung](../../../images/cnd-trust-helloworld-webpart-solution.png)

<span data-ttu-id="3713d-161">Beachten Sie, dass die **Domänenliste** in der Aufforderung *SharePoint Online* enthält.</span><span class="sxs-lookup"><span data-stu-id="3713d-161">Notice how the **domain** list in the prompt is saying *SharePoint Online*.</span></span> <span data-ttu-id="3713d-162">Dies ist der Fall, da der Inhalt, je nach Mandanteneinstellungen, entweder von dem Office 365 CDN oder dem App-Katalog bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="3713d-162">This is since the content is either served from the Office 365 CDN or from app catalog, depending on the tenant settings.</span></span>

<span data-ttu-id="3713d-163">Wählen Sie **Bereitstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="3713d-163">Choose **Deploy**</span></span>

<span data-ttu-id="3713d-164">Öffnen Sie eine Website, auf der Sie zuvor die **helloworld-webpart-client-side-solution**-Lösung installiert haben, oder installieren Sie die Lösung auf einer neuen Website.</span><span class="sxs-lookup"><span data-stu-id="3713d-164">Open a site where previously installed the **helloworld-webpart-client-side-solution** solution or install solution to a new site.</span></span>

<span data-ttu-id="3713d-165">Nachdem die Lösung installiert wurde, wählen Sie **Seite hinzufügen** im Menü mit dem *Zahnradsymbol*, und wählen Sie **HelloWorld** in der Webpartauswahl für die moderne Seite aus, um Ihr benutzerdefiniertes Webpart zur Seite hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="3713d-165">After the solution has been installed, chose **Add a page** from the *gear* menu and pick **HelloWorld** from the modern page web part picker</span></span>

![HelloWorld-Webpart in der Webpartauswahl für die moderne Seite](../../../images/cdn-web-part-picker.png)

<span data-ttu-id="3713d-167">Sie sehen: Das Webpart wird gerendert, obwohl der node.js-Dienst nicht lokal ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="3713d-167">Notice how the web part is rendered even though you are not running the node.js service locally.</span></span> 

![HelloWorld-Webpart, gerendert auf einer modernen Seite im Bearbeitungsmodus](../../../images/cdn-web-part-rendering.png)

<span data-ttu-id="3713d-169">Speichern Sie die Änderungen auf der Seite mit dem Webpart.</span><span class="sxs-lookup"><span data-stu-id="3713d-169">Save changes on the page with web part on it.</span></span>

<span data-ttu-id="3713d-170">Drücken Sie **F12**, um die Entwicklungstools zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="3713d-170">Press **F12** to open up developer tools.</span></span>

<span data-ttu-id="3713d-171">Erweitern Sie **publiccdn.sharepointonline.com** unter Quellen, und achten Sie darauf, dass die Datei **hello-world-web-part** von der URL des öffentlichen CDN geladen wird, die dynamisch auf eine Bibliothek in der App-Katalog-Websitesammlung verweist.</span><span class="sxs-lookup"><span data-stu-id="3713d-171">Extend **publiccdn.sharepointonline.com** under the source and notice how the **hello-world-web-part** file is loaded from the Public CDN URL pointing dynamically to a library located under the app catalog site collection.</span></span>

![HelloWorld-Webpartbundle, geladen von der URL des öffentlichen CDN, auf der Registerkarte „Sources“ in den Chrome Developer Tools](../../../images/cdn-web-part-f12-source.png)

> [!NOTE]
> <span data-ttu-id="3713d-173">Wenn Sie CDN nicht in Ihrem Mandanten aktiviert hätten und die `includeClientSideAssets`-Einstellung in **package-solution.json** `true` lauten würde, würde das Laden der URL für die Objekte dynamisch aktualisiert und sie würden direkt auf den ClientSideAssets-Ordner in der App-Katalog-Websitesammlung verweisen.</span><span class="sxs-lookup"><span data-stu-id="3713d-173">If you would not have CDN enabled in your tenant and the `includeClientSideAssets` setting would be `true`in the **package-solution.json**, loading URL for the assets would be dynamically updated and pointing directly to the ClientSideAssets folder located in the app catalog site collection.</span></span> <span data-ttu-id="3713d-174">In diesem Beispiel lautet die URL: `https://sppnp.microsoft.com/sites/apps/ClientSideAssets/`.</span><span class="sxs-lookup"><span data-stu-id="3713d-174">In this example case, URL would be `https://sppnp.microsoft.com/sites/apps/ClientSideAssets/`.</span></span>

<span data-ttu-id="3713d-175">Ihr benutzerdefiniertes Webpart ist jetzt in SharePoint Online bereitgestellt und wird automatisch in Office 365 CDN gehostet.</span><span class="sxs-lookup"><span data-stu-id="3713d-175">Now you have deployed your custom web part to SharePoint Online and it's being hosted from the Office 365 CDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3713d-176">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="3713d-176">Next steps</span></span>

<span data-ttu-id="3713d-177">Sie können jQuery und jQueryUI laden und ein jQuery Accordion-Webpart erstellen.</span><span class="sxs-lookup"><span data-stu-id="3713d-177">You can load jQuery, jQuery UI and build a jQuery Accordion web part.</span></span> <span data-ttu-id="3713d-178">Lesen Sie die Informationen unter [Hinzufügen von jQueryUI Accordion zu Ihrem clientseitigen Webpart](./add-jqueryui-accordion-to-web-part.md), um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="3713d-178">To continue, see [Add jQueryUI Accordion to your client-side web part](./add-jqueryui-accordion-to-web-part.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3713d-179">Wenn Sie einen Fehler in der Dokumentation oder im SharePoint-Framework finden, melden Sie ihn an das SharePoint Engineering unter Verwendung der [Fehlerliste im sp-dev-docs-Repository](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="3713d-179">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="3713d-180">Vielen Dank im Voraus für Ihr Feedback.</span><span class="sxs-lookup"><span data-stu-id="3713d-180">Thanks for your input advance.</span></span>