# <a name="host-extension-from-office-365-cdn-hello-world-part-4"></a><span data-ttu-id="7f78c-101">Hostingerweiterung von Office 365 CDN (Hello World, Teil 4)</span><span class="sxs-lookup"><span data-stu-id="7f78c-101">Hosting extension from Office 365 CDN (Hello world part 4)</span></span>

<span data-ttu-id="7f78c-102">In diesem Artikel wird beschrieben, wie Sie den SharePoint-Framework Application Customizer über Office 365 CDN bereitstellen und wie dieser über SharePoint für Endbenutzer bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="7f78c-102">This article describes how to deploy your SharePoint Framework Application Customizer to be hosted from an Office 365 CDN and how to deploy that to SharePoint for end users.</span></span> <span data-ttu-id="7f78c-103">In diesem Artikel wird weiterhin die Hello World-Erweiterung aus dem vorherigen Artikel [Bereitstellen Ihrer Erweiterung in SharePoint (Hello World, Teil 3)](./serving-your-extension-from-sharepoint.md) verwendet, in dem der Customizer weitherhin von localhost gehostet wurde.</span><span class="sxs-lookup"><span data-stu-id="7f78c-103">This article continues with the Hello World extension built in the previous article [Deploy your extension to SharePoint (Hello World part 3)](./serving-your-extension-from-sharepoint.md), where we were still hosting the customizer from localhost.</span></span>

<span data-ttu-id="7f78c-104">Stellen Sie sicher, dass Sie die Verfahren in den folgenden Artikeln abgeschlossen haben, bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="7f78c-104">Be sure you have completed the procedures in the following articles before you begin:</span></span>

* [<span data-ttu-id="7f78c-105">Erstellen Ihrer ersten SharePoint-Framework-Erweiterung (Hello World, Teil 1)</span><span class="sxs-lookup"><span data-stu-id="7f78c-105">Build your first SharePoint Framework Extension (Hello World part 1)</span></span>](./build-a-hello-world-extension.md)
* [<span data-ttu-id="7f78c-106">Verwenden von Seitenplatzhaltern aus dem Application Customizer (Hello World, Teil 2)</span><span class="sxs-lookup"><span data-stu-id="7f78c-106">Use page placeholders from Application Customizer (Hello World part 2)</span></span>](./using-page-placeholder-with-extensions.md)
* [<span data-ttu-id="7f78c-107">Bereitstellen Ihrer Erweiterung in SharePoint (Hello World, Teil 3)</span><span class="sxs-lookup"><span data-stu-id="7f78c-107">Deploy your extension to SharePoint (Hello world part 3)</span></span>](./serving-your-extension-from-sharepoint.md)

<span data-ttu-id="7f78c-108">Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=oOIHWamPr34&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV) nachvollziehen:</span><span class="sxs-lookup"><span data-stu-id="7f78c-108">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=oOIHWamPr34&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span></span> 

<a href="https://www.youtube.com/watch?v=nh1qFArXG2Y">
<img src="../../../images/spfx-ext-youtube-tutorial4.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="enable-the-cdn-in-your-office-365-tenant"></a><span data-ttu-id="7f78c-109">Aktivieren von CDN in Ihrem Office 365-Mandanten</span><span class="sxs-lookup"><span data-stu-id="7f78c-109">Enable CDN in your Office 365 tenant</span></span>
<span data-ttu-id="7f78c-110">Office 365 CDN ist die einfachste Möglichkeit, SharePoint-Framework-Lösungen direkt von Ihrem Mandanten aus zu hosten und dabei weiterhin die Vorteile des CDN (Content Delivery Network) zum schnelleren Laden der Objekte zu nutzen.</span><span class="sxs-lookup"><span data-stu-id="7f78c-110">Office 365 CDN is the easiest way to host SharePoint Framework solutions directly from your tenant while still taking advantage of the Content Delivery Network (CDN) service for faster load times of your assets.</span></span>

1. <span data-ttu-id="7f78c-111">Laden Sie die [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunter, um sicherzustellen, dass Sie die neueste Version verwenden.</span><span class="sxs-lookup"><span data-stu-id="7f78c-111">Download the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) to ensure that you have the latest version.</span></span>

2. <span data-ttu-id="7f78c-112">Verbinden Sie sich über PowerShell mit Ihrem SharePoint Online-Mandanten:</span><span class="sxs-lookup"><span data-stu-id="7f78c-112">Connect to your SharePoint Online tenant through PowerShell:</span></span>
    
    ```
    Connect-SPOService -Url https://contoso-admin.sharepoint.com
    ```
    
3. <span data-ttu-id="7f78c-113">Führen Sie nacheinander die folgenden Befehle aus, um den aktuellen Status der auf Mandantenebene festgelegten Einstellungen für öffentliche CDNs abzurufen:</span><span class="sxs-lookup"><span data-stu-id="7f78c-113">Get the current status of public CDN settings from the tenant level by executing the following commands one-by-one.</span></span> 
    
    ```
    Get-SPOTenantCdnEnabled -CdnType Public
    Get-SPOTenantCdnOrigins -CdnType Public
    Get-SPOTenantCdnPolicies -CdnType Public
    ```
    
4. <span data-ttu-id="7f78c-114">Aktivieren Sie öffentliche CDNs im Mandanten:</span><span class="sxs-lookup"><span data-stu-id="7f78c-114">Enable public CDN in the tenant</span></span>
    
    ```
    Set-SPOTenantCdnEnabled -CdnType Public
    ```
    
    <span data-ttu-id="7f78c-115">Jetzt sind öffentliche CDNs im Mandanten aktiviert, mit der Standardkonfiguration für zulässige Dateitypen.</span><span class="sxs-lookup"><span data-stu-id="7f78c-115">Public CDN has now been enabled in the tenant by using the default file type configuration allowed.</span></span> <span data-ttu-id="7f78c-116">Dies bedeutet, dass die folgenden Dateitypen unterstützt werden: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF und WOFF.</span><span class="sxs-lookup"><span data-stu-id="7f78c-116">Now public CDN has been enabled in the tenant using the default file type configuration allowed. This means that the following file type extensions are supported: "CSS,EOT,GIF,ICO,JPEG,JPG,JS,MAP,PNG,SVG,TTF,WOFF".</span></span>

5. <span data-ttu-id="7f78c-p103">Öffnen Sie einen Browser, und navigieren Sie zu der Websitesammlung, in der Sie Ihre CDN-Bibliothek hosten möchten. Das kann jede beliebige Websitesammlung in Ihrem Mandanten sein. In diesem Tutorial erstellen Sie eine spezifische Bibliothek, die als Ihre CDN-Bibliothek fungiert. Sie können aber auch einen spezifischen Ordner in einer beliebigen bereits vorhandenen Dokumentbibliothek als CDN-Endpunkt nutzen.</span><span class="sxs-lookup"><span data-stu-id="7f78c-p103">Open up a browser and move to a site collection where you'd like to host your CDN library. This could be any site collection in your tenant. In this tutorial, we will create a specific library to act as your CDN library, but you can also use a specific folder in any existing document library as the CDN endpoint.</span></span>

6. <span data-ttu-id="7f78c-120">Erstellen Sie in Ihrer Websitesammlung eine neue Dokumentbibliothek namens **CDN**, und fügen Sie ihr einen Ordner namens **helloworld** hinzu.</span><span class="sxs-lookup"><span data-stu-id="7f78c-120">Create a new document library on your site collection called **CDN** and add a folder named **helloworld** to it.</span></span>
    
    ![Helloworld-Erweiterungsordner in der CDN-Bibliothek](../../../images/ext-app-cdn-folder-created.png) 
    
    <br/>
    
7. <span data-ttu-id="7f78c-122">Fügen Sie in der PowerShell-Konsole einen neuen CDN-Ursprung hinzu.</span><span class="sxs-lookup"><span data-stu-id="7f78c-122">In the PowerShell console, add a new CDN origin.</span></span> <span data-ttu-id="7f78c-123">In diesem Fall legen Sie als Ursprung `*/cdn` fest; auf diese Weise fungieren alle relativen Ordner mit dem Namen **cdn** als ein CDN-Ursprung.</span><span class="sxs-lookup"><span data-stu-id="7f78c-123">Move back to the PowerShell console and add a new CDN origin. In this case, we are setting the origin as `*/cdn`, which means that any relative folder with the name of **cdn** will act as a CDN origin.</span></span>
    
    ```
    Add-SPOTenantCdnOrigin -CdnType Public -OriginUrl */cdn
    ```
    
8. <span data-ttu-id="7f78c-124">Führen Sie den folgenden Befehl aus, um eine Liste aller CDN-Ursprünge von Ihrem Mandanten abzurufen:</span><span class="sxs-lookup"><span data-stu-id="7f78c-124">Execute the following command to get the list of CDN origins from your tenant</span></span>
    
    ```
    Get-SPOTenantCdnOrigins -CdnType Public
    ```
    
<span data-ttu-id="7f78c-125">Sie sehen, dass der neu hinzugefügte Ursprung als gültiger CDN-Ursprung aufgeführt ist.</span><span class="sxs-lookup"><span data-stu-id="7f78c-125">Note that your newly added origin is listed as a valid CDN origin.</span></span> <span data-ttu-id="7f78c-126">Die endgültige Konfiguration des Ursprungs dauert ca. 15 Minuten. Während Sie warten, können Sie eine Testerweiterung erstellen, die nach Abschluss der Bereitstellung im Ursprung gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="7f78c-126">Notice that your newly added origin is listed as a valid CDN origin. Final configuration of the origin will take a while (approximately 15 minutes), so we can continue creating your test extension, which will be hosted from the origin once deployment is completed.</span></span> 

![Liste der öffentlichen Ursprünge im Mandanten](../../../images/ext-app-cdn-origins-pending.png)

<span data-ttu-id="7f78c-128">Sobald der Ursprung nicht mehr mit `(configuration pending)` gekennzeichnet ist, kann er in Ihrem Mandanten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="7f78c-128">When origin is listed without the (configuration pending)`(configuration pending)` text, it is ready to be used in your tenant. This is the indication of an on-going configuration between SharePoint Online and CDN system.</span></span> <span data-ttu-id="7f78c-129">Dieser Text weist auf laufende Konfigurationsaktivitäten zwischen SharePoint Online und dem CDN-System hin.</span><span class="sxs-lookup"><span data-stu-id="7f78c-129">This indicates an on-going configuration between SharePoint Online and the CDN system.</span></span> 

## <a name="update-your-solution-project-for-the-cdn-urls"></a><span data-ttu-id="7f78c-130">Aktualisieren des Lösungsprojekts für die CDN-URLs</span><span class="sxs-lookup"><span data-stu-id="7f78c-130">Updating your solution project for the CDN URLs</span></span>

1. <span data-ttu-id="7f78c-131">Kehren Sie zu der zuvor erstellten Lösung zurück, um die erforderliche URL-Updates auszuführen.</span><span class="sxs-lookup"><span data-stu-id="7f78c-131">Return to the previously created solution to perform the needed URL updates.</span></span>
    
2. <span data-ttu-id="7f78c-132">Aktualisieren Sie die Datei **write-manifests.json** (im Ordner **config**) wie unten dargestellt, damit sie auf Ihren CDN-Endpunkt verweist.</span><span class="sxs-lookup"><span data-stu-id="7f78c-132">Update the **write-manifests.json** file (under the **config** folder) as follows to point to your CDN endpoint.</span></span> <span data-ttu-id="7f78c-133">Verwenden Sie `publiccdn.sharepointonline.com` als Präfix, und erweitern Sie dann die URL um den tatsächlichen Pfad Ihres Mandanten.</span><span class="sxs-lookup"><span data-stu-id="7f78c-133">You will need to use the publiccdn.sharepointonline.com as the prefix and then extend the URL with the actual path of your tenant</span></span> <span data-ttu-id="7f78c-134">Die CDN-URL hat folgendes Format:</span><span class="sxs-lookup"><span data-stu-id="7f78c-134">Format of the CDN URL is as follows</span></span>
    
    ```
    https://publiccdn.sharepointonline.com/<tenant host name>/sites/site/library/folder
    ```
    
    ![Aktualisierte Datei „write-manifests“ mit dem Pfad zum CDN-Endpunkt](../../../images/ext-app-cdn-write-manifest.png)

3. <span data-ttu-id="7f78c-136">Speichern Sie Ihre Änderungen.</span><span class="sxs-lookup"><span data-stu-id="7f78c-136">Save your changes.</span></span>

4. <span data-ttu-id="7f78c-137">Führen Sie die folgenden Aufgaben aus, um Ihre Lösung in einem Bundle zu verpacken.</span><span class="sxs-lookup"><span data-stu-id="7f78c-137">Execute the following tasks to bundle your solution</span></span> <span data-ttu-id="7f78c-138">Es wird ein Releasebuild Ihres Projekts ausgeführt, unter Verwendung der in der Datei **write-manifests.json** angegebenen CDN-URL.</span><span class="sxs-lookup"><span data-stu-id="7f78c-138">This executes a release build of your project using the CDN URL specified in the **write-manifests.json** file.</span></span> <span data-ttu-id="7f78c-139">Die Ausgabe dieses Befehls finden Sie im Ordner **./temp/deploy**.</span><span class="sxs-lookup"><span data-stu-id="7f78c-139">The output of this command is located in the **./temp/deploy** folder.</span></span> <span data-ttu-id="7f78c-140">Dies sind die Dateien, die Sie in den SharePoint-Ordner hochladen müssen, der als CDN-Endpunkt fungiert.</span><span class="sxs-lookup"><span data-stu-id="7f78c-140">These are the files that you need to upload to the SharePoint folder acting as your CDN endpoint.</span></span> 
    
    ```
    gulp bundle --ship
    ```
    
5. <span data-ttu-id="7f78c-141">Führen Sie die folgende Aufgaben aus, um Ihre Lösung zu packen.</span><span class="sxs-lookup"><span data-stu-id="7f78c-141">Execute the following task to package your solution</span></span> <span data-ttu-id="7f78c-142">Dieser Befehl erstellt ein Paket namens **app-extension.sppkg** im Ordner **sharepoint/solution** und bereitet außerdem die Ressourcen im Ordner **temp/deploy** für die Bereitstellung im CDN vor.</span><span class="sxs-lookup"><span data-stu-id="7f78c-142">This command will create an **app-extension.sppkg** package in the **sharepoint/solution** folder and also prepare the assets in the **temp/deploy** folder to be deployed to the CDN.</span></span>
    
    ```
    gulp package-solution --ship
    ```
    
6. <span data-ttu-id="7f78c-143">Laden Sie das neu erstellte Paket mit ihrer clientseitigen Lösung in den App-Katalog in Ihrem Mandanten hoch. Alternativ können Sie es auch per Drag-and-Drop verschieben. Klicken Sie auf die Schaltfläche **Bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="7f78c-143">Upload or drag & drop the newly created client-side solution package to the app catalog in your tenant. Click the **Deploy** button.</span></span>

    ![Dialogfeld „Vertrauen“ des App-Katalogs mit dem Pfad zum CDN-Endpunkt](../../../images/ext-app-approve-cdn-address.png)

7. <span data-ttu-id="7f78c-145">Laden Sie die Dateien im Ordner **temp/deploy** in den Ordner **CDN/helloworld** hoch, den Sie zuvor erstellt haben. Sie können die Dateien auch mit Drag-and-Drop verschieben.</span><span class="sxs-lookup"><span data-stu-id="7f78c-145">Upload or drag & drop the files in the **temp/deploy** folder to the **CDN/helloworld** folder created earlier.</span></span>

8. <span data-ttu-id="7f78c-146">Installieren Sie die neue Version der Lösung auf Ihrer Website, und stellen Sie sicher, dass sie ordnungsgemäß funktioniert, ohne dass *locahost* die JavaScript-Datei hostet.</span><span class="sxs-lookup"><span data-stu-id="7f78c-146">Install the new version of the solution to your site and ensure that it's working properly without your *locahost* hosting the JavaScript file.</span></span>

    ![Benutzerdefinierte Kopf- und Fußzeilenelemente, auf der Seite gerendert](../../../images/ext-app-header-footer-visible.png)

<br/>

<span data-ttu-id="7f78c-148">Herzlichen Glückwunsch! Sie haben ein öffentliches CDN in Ihrem Office 365-Mandanten aktiviert und es in der Lösung genutzt.</span><span class="sxs-lookup"><span data-stu-id="7f78c-148">Congratulations, you have enabled a public CDN in your Office 365 tenant and taken advantage of it from your solution!</span></span>

> [!NOTE]
> <span data-ttu-id="7f78c-149">Wenn Sie einen Fehler in der Dokumentation oder im SharePoint-Framework finden, melden Sie ihn an das SharePoint Engineering unter Verwendung der [Fehlerliste im sp-dev-docs-Repository]((https://github.com/SharePoint/sp-dev-docs/issues)).</span><span class="sxs-lookup"><span data-stu-id="7f78c-149">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository]((https://github.com/SharePoint/sp-dev-docs/issues)).</span></span> <span data-ttu-id="7f78c-150">Vielen Dank im Voraus für Ihr Feedback.</span><span class="sxs-lookup"><span data-stu-id="7f78c-150">Thanks for your input advance.</span></span>