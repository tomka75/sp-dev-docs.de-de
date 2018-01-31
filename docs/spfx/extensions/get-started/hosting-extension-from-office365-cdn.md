---
title: Hostingerweiterung von Office 365 CDN (Hello World, Teil 4)
description: "Bereitstellen Ihres SharePoint-Framework Application Customizer für das Hosting über Office 365 CDN und Bereitstellen über SharePoint für Endbenutzer."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: 95bf41477668d5848fccaafa586491fd36f2a7ca
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="host-extension-from-office-365-cdn-hello-world-part-4"></a><span data-ttu-id="09acb-103">Hostingerweiterung von Office 365 CDN (Hello World, Teil 4)</span><span class="sxs-lookup"><span data-stu-id="09acb-103">Host extension from Office 365 CDN (Hello World part 4)</span></span>

<span data-ttu-id="09acb-104">In diesem Artikel wird beschrieben, wie Sie den SharePoint-Framework Application Customizer über Office 365 CDN bereitstellen und wie dieser über SharePoint für Endbenutzer bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="09acb-104">This article describes how to deploy your SharePoint Framework Application Customizer to be hosted from an Office 365 CDN and how to deploy that to SharePoint for end users.</span></span> 

<span data-ttu-id="09acb-105">Stellen Sie sicher, dass Sie die Verfahren in den folgenden Artikeln abgeschlossen haben, bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="09acb-105">Be sure you have completed the procedures in the following articles before you begin:</span></span>

* [<span data-ttu-id="09acb-106">Erstellen Ihrer ersten SharePoint-Framework-Erweiterung (Hello World, Teil 1)</span><span class="sxs-lookup"><span data-stu-id="09acb-106">Build your first SharePoint Framework Extension (Hello World part 1)</span></span>](./build-a-hello-world-extension.md)
* [<span data-ttu-id="09acb-107">Verwenden von Seitenplatzhaltern aus dem Application Customizer (Hello World, Teil 2)</span><span class="sxs-lookup"><span data-stu-id="09acb-107">Use page placeholders from Application Customizer (Hello World part 2)</span></span>](./using-page-placeholder-with-extensions.md)
* [<span data-ttu-id="09acb-108">Bereitstellen Ihrer Erweiterung in SharePoint (Hello World, Teil 3)</span><span class="sxs-lookup"><span data-stu-id="09acb-108">Deploy your extension to SharePoint (Hello World part 3)</span></span>](./serving-your-extension-from-sharepoint.md)

<span data-ttu-id="09acb-109">Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=oOIHWamPr34&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV) nachvollziehen:</span><span class="sxs-lookup"><span data-stu-id="09acb-109">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=oOIHWamPr34&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span></span> 

<a href="https://www.youtube.com/watch?v=nh1qFArXG2Y">
<img src="../../../images/spfx-ext-youtube-tutorial4.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="enable-the-cdn-in-your-office-365-tenant"></a><span data-ttu-id="09acb-110">Aktivieren von CDN in Ihrem Office 365-Mandanten</span><span class="sxs-lookup"><span data-stu-id="09acb-110">Enable the CDN in your Office 365 tenant</span></span>

<span data-ttu-id="09acb-111">Office 365 CDN ist die einfachste Möglichkeit, SharePoint-Framework-Lösungen direkt von Ihrem Mandanten aus zu hosten und dabei weiterhin die Vorteile des CDN (Content Delivery Network) zum schnelleren Laden der Objekte zu nutzen.</span><span class="sxs-lookup"><span data-stu-id="09acb-111">Office 365 CDN is the easiest way to host SharePoint Framework solutions directly from your tenant while still taking advantage of the Content Delivery Network (CDN) service for faster load times of your assets.</span></span>

1. <span data-ttu-id="09acb-112">Laden Sie die [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunter, um sicherzustellen, dass Sie die neueste Version verwenden.</span><span class="sxs-lookup"><span data-stu-id="09acb-112">Download the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) to ensure that you have the latest version.</span></span>

2. <span data-ttu-id="09acb-113">Verbinden Sie sich über PowerShell mit Ihrem SharePoint Online-Mandanten:</span><span class="sxs-lookup"><span data-stu-id="09acb-113">Connect to your SharePoint Online tenant by using PowerShell:</span></span>
    
    ```powershell
    Connect-SPOService -Url https://contoso-admin.sharepoint.com
    ```
    
3. <span data-ttu-id="09acb-114">Führen Sie nacheinander die folgenden Befehle aus, um den aktuellen Status der auf Mandantenebene festgelegten Einstellungen für öffentliche CDNs abzurufen:</span><span class="sxs-lookup"><span data-stu-id="09acb-114">Get the current status of public CDN settings from the tenant level by executing the following commands one-by-one:</span></span> 
    
    ```powershell
    Get-SPOTenantCdnEnabled -CdnType Public
    Get-SPOTenantCdnOrigins -CdnType Public
    Get-SPOTenantCdnPolicies -CdnType Public
    ```
    
4. <span data-ttu-id="09acb-115">Aktivieren Sie öffentliche CDNs im Mandanten:</span><span class="sxs-lookup"><span data-stu-id="09acb-115">Enable public CDN in the tenant:</span></span>
    
    ```powershell
    Set-SPOTenantCdnEnabled -CdnType Public
    ```
    
    <span data-ttu-id="09acb-116">Jetzt sind öffentliche CDNs im Mandanten aktiviert, mit der Standardkonfiguration für zulässige Dateitypen.</span><span class="sxs-lookup"><span data-stu-id="09acb-116">Public CDN has now been enabled in the tenant by using the default file type configuration allowed.</span></span> <span data-ttu-id="09acb-117">Dies bedeutet, dass die folgenden Dateitypen unterstützt werden: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF und WOFF.</span><span class="sxs-lookup"><span data-stu-id="09acb-117">This means that the following file type extensions are supported: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF, and WOFF.</span></span>

5. <span data-ttu-id="09acb-p102">Öffnen Sie einen Browser, und navigieren Sie zu der Websitesammlung, in der Sie Ihre CDN-Bibliothek hosten möchten. Das kann jede beliebige Websitesammlung in Ihrem Mandanten sein. In diesem Tutorial erstellen Sie eine spezifische Bibliothek, die als Ihre CDN-Bibliothek fungiert. Sie können aber auch einen spezifischen Ordner in einer beliebigen bereits vorhandenen Dokumentbibliothek als CDN-Endpunkt nutzen.</span><span class="sxs-lookup"><span data-stu-id="09acb-p102">Open up a browser and move to a site collection where you'd like to host your CDN library. This could be any site collection in your tenant. In this tutorial, we create a specific library to act as your CDN library, but you can also use a specific folder in any existing document library as the CDN endpoint.</span></span>

6. <span data-ttu-id="09acb-121">Erstellen Sie in Ihrer Websitesammlung eine neue Dokumentbibliothek namens **CDN**, und fügen Sie ihr einen Ordner namens **helloworld** hinzu.</span><span class="sxs-lookup"><span data-stu-id="09acb-121">Create a new document library on your site collection called **CDN** and add a folder named **helloworld** to it.</span></span>
    
    ![Helloworld-Erweiterungsordner in der CDN-Bibliothek](../../../images/ext-app-cdn-folder-created.png) 
    
    <br/>
    
7. <span data-ttu-id="09acb-123">Fügen Sie in der PowerShell-Konsole einen neuen CDN-Ursprung hinzu.</span><span class="sxs-lookup"><span data-stu-id="09acb-123">In the PowerShell console, add a new CDN origin.</span></span> <span data-ttu-id="09acb-124">In diesem Fall legen Sie als Ursprung `*/cdn` fest; auf diese Weise fungieren alle relativen Ordner mit dem Namen **cdn** als ein CDN-Ursprung.</span><span class="sxs-lookup"><span data-stu-id="09acb-124">In this case, we are setting the origin as `*/cdn`, which means that any relative folder with the name of **cdn** acts as a CDN origin.</span></span>
    
    ```powershell
    Add-SPOTenantCdnOrigin -CdnType Public -OriginUrl */cdn
    ```
    
8. <span data-ttu-id="09acb-125">Führen Sie den folgenden Befehl aus, um eine Liste aller CDN-Ursprünge von Ihrem Mandanten abzurufen:</span><span class="sxs-lookup"><span data-stu-id="09acb-125">Execute the following command to get the list of CDN origins from your tenant:</span></span>
    
    ```powershell
    Get-SPOTenantCdnOrigins -CdnType Public
    ```
    
    <span data-ttu-id="09acb-126">Sie sehen, dass der neu hinzugefügte Ursprung als gültiger CDN-Ursprung aufgeführt ist.</span><span class="sxs-lookup"><span data-stu-id="09acb-126">Note that your newly added origin is listed as a valid CDN origin.</span></span> <span data-ttu-id="09acb-127">Die endgültige Konfiguration des Ursprungs dauert ca. 15 Minuten. Während Sie warten, können Sie eine Testerweiterung erstellen, die nach Abschluss der Bereitstellung im Ursprung gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="09acb-127">Final configuration of the origin takes approximately 15 minutes, so we can continue creating your test extension, which will be hosted from the origin after deployment is completed.</span></span> 

    ![Liste der öffentlichen Ursprünge im Mandanten](../../../images/ext-app-cdn-origins-pending.png)

    <span data-ttu-id="09acb-129">Sobald der Ursprung nicht mehr mit `(configuration pending)` gekennzeichnet ist, kann er in Ihrem Mandanten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="09acb-129">When the origin is listed without the `(configuration pending)` text, it is ready to be used in your tenant.</span></span> <span data-ttu-id="09acb-130">Dieser Text weist auf laufende Konfigurationsaktivitäten zwischen SharePoint Online und dem CDN-System hin.</span><span class="sxs-lookup"><span data-stu-id="09acb-130">This indicates an on-going configuration between SharePoint Online and the CDN system.</span></span> 

## <a name="update-your-solution-project-for-the-cdn-urls"></a><span data-ttu-id="09acb-131">Aktualisieren des Lösungsprojekts für die CDN-URLs</span><span class="sxs-lookup"><span data-stu-id="09acb-131">Update your solution project for the CDN URLs</span></span>

1. <span data-ttu-id="09acb-132">Kehren Sie zu der zuvor erstellten Lösung zurück, um die erforderliche URL-Updates auszuführen.</span><span class="sxs-lookup"><span data-stu-id="09acb-132">Return to the previously created solution to perform the needed URL updates.</span></span>
    
2. <span data-ttu-id="09acb-133">Aktualisieren Sie die Datei **write-manifests.json** (im Ordner **config**) wie unten dargestellt, damit sie auf Ihren CDN-Endpunkt verweist.</span><span class="sxs-lookup"><span data-stu-id="09acb-133">Update the **write-manifests.json** file (under the **config** folder) as follows to point to your CDN endpoint.</span></span> <span data-ttu-id="09acb-134">Verwenden Sie `publiccdn.sharepointonline.com` als Präfix, und erweitern Sie dann die URL um den tatsächlichen Pfad Ihres Mandanten.</span><span class="sxs-lookup"><span data-stu-id="09acb-134">Use `publiccdn.sharepointonline.com` as the prefix, and then extend the URL with the actual path of your tenant.</span></span> <span data-ttu-id="09acb-135">Die CDN-URL hat folgendes Format:</span><span class="sxs-lookup"><span data-stu-id="09acb-135">The format of the CDN URL is as follows:</span></span>
    
    ```json
    https://publiccdn.sharepointonline.com/<tenant host name>/sites/site/library/folder
    ```
    
    ![Aktualisierte Datei „write-manifests“ mit dem Pfad zum CDN-Endpunkt](../../../images/ext-app-cdn-write-manifest.png)

3. <span data-ttu-id="09acb-137">Speichern Sie Ihre Änderungen.</span><span class="sxs-lookup"><span data-stu-id="09acb-137">Save your changes.</span></span>

4. <span data-ttu-id="09acb-138">Führen Sie die folgenden Aufgaben aus, um Ihre Lösung in einem Bundle zu verpacken.</span><span class="sxs-lookup"><span data-stu-id="09acb-138">Execute the following tasks to bundle your solution.</span></span> <span data-ttu-id="09acb-139">Es wird ein Releasebuild Ihres Projekts ausgeführt, unter Verwendung der in der Datei **write-manifests.json** angegebenen CDN-URL.</span><span class="sxs-lookup"><span data-stu-id="09acb-139">This executes a release build of your project using the CDN URL specified in the **write-manifests.json** file.</span></span> <span data-ttu-id="09acb-140">Die Ausgabe dieses Befehls finden Sie im Ordner **./temp/deploy**.</span><span class="sxs-lookup"><span data-stu-id="09acb-140">The output of this command is located in the **./temp/deploy** folder.</span></span> <span data-ttu-id="09acb-141">Dies sind die Dateien, die Sie in den SharePoint-Ordner hochladen müssen, der als CDN-Endpunkt fungiert.</span><span class="sxs-lookup"><span data-stu-id="09acb-141">These are the files that you need to upload to the SharePoint folder acting as your CDN endpoint.</span></span> 
    
    ```
    gulp bundle --ship
    ```
    
5. <span data-ttu-id="09acb-142">Führen Sie die folgende Aufgabe aus, um Ihre Lösung zu packen.</span><span class="sxs-lookup"><span data-stu-id="09acb-142">Execute the following task to package your solution.</span></span> <span data-ttu-id="09acb-143">Dieser Befehl erstellt ein Paket namens **app-extension.sppkg** im Ordner **sharepoint/solution** und bereitet die Ressourcen im Ordner **temp/deploy** für die Bereitstellung im CDN vor.</span><span class="sxs-lookup"><span data-stu-id="09acb-143">This command creates an **app-extension.sppkg** package in the **sharepoint/solution** folder and also prepares the assets in the **temp/deploy** folder to be deployed to the CDN.</span></span>
    
    ```
    gulp package-solution --ship
    ```
    
6. <span data-ttu-id="09acb-144">Laden Sie das neu erstellte Paket mit ihrer clientseitigen Lösung in den App-Katalog in Ihrem Mandanten hoch. Alternativ können Sie es auch per Drag-and-Drop verschieben. Klicken Sie auf die Schaltfläche **Bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="09acb-144">Upload or drag-and-drop the newly created client-side solution package to the app catalog in your tenant, and then select the **Deploy** button.</span></span>

    ![Dialogfeld „Vertrauen“ des App-Katalogs mit dem Pfad zum CDN-Endpunkt](../../../images/ext-app-approve-cdn-address.png)

7. <span data-ttu-id="09acb-146">Laden Sie die Dateien im Ordner **temp/deploy** in den Ordner **CDN/helloworld** hoch, den Sie zuvor erstellt haben. Sie können die Dateien auch mit Drag-and-Drop verschieben.</span><span class="sxs-lookup"><span data-stu-id="09acb-146">Upload or drag-and-drop the files in the **temp/deploy** folder to the **CDN/helloworld** folder created earlier.</span></span>

8. <span data-ttu-id="09acb-147">Installieren Sie die neue Version der Lösung auf Ihrer Website, und stellen Sie sicher, dass sie ordnungsgemäß funktioniert, ohne dass *locahost* die JavaScript-Datei hostet.</span><span class="sxs-lookup"><span data-stu-id="09acb-147">Install the new version of the solution to your site and ensure that it's working properly without your *locahost* hosting the JavaScript file.</span></span>

    ![Benutzerdefinierte Kopf- und Fußzeilenelemente, auf der Seite gerendert](../../../images/ext-app-header-footer-visible.png)

<br/>

<span data-ttu-id="09acb-149">Herzlichen Glückwunsch! Sie haben ein öffentliches CDN in Ihrem Office 365-Mandanten aktiviert und es in der Lösung genutzt.</span><span class="sxs-lookup"><span data-stu-id="09acb-149">Congratulations, you have enabled a public CDN in your Office 365 tenant and taken advantage of it from your solution!</span></span>

> [!NOTE]
> <span data-ttu-id="09acb-150">Wenn Sie einen Fehler in der Dokumentation oder im SharePoint-Framework finden, melden Sie ihn an das SharePoint Engineering unter Verwendung der [Fehlerliste im sp-dev-docs-Repository](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="09acb-150">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="09acb-151">Vielen Dank im Voraus für Ihr Feedback.</span><span class="sxs-lookup"><span data-stu-id="09acb-151">Thanks for your input advance.</span></span>

## <a name="see-also"></a><span data-ttu-id="09acb-152">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="09acb-152">See also</span></span>

- [<span data-ttu-id="09acb-153">Erstellen Ihrer ersten Erweiterung des Typs „ListView Command Set“</span><span class="sxs-lookup"><span data-stu-id="09acb-153">Build your first ListView Command Set Extension</span></span>](./building-simple-cmdset-with-dialog-api.md)
- [<span data-ttu-id="09acb-154">Erstellen Ihrer ersten Field Customizer-Erweiterung</span><span class="sxs-lookup"><span data-stu-id="09acb-154">Build your first Field Customizer Extension</span></span>](./building-simple-field-customizer.md)
- [<span data-ttu-id="09acb-155">Übersicht über SharePoint-Framework-Erweiterungen</span><span class="sxs-lookup"><span data-stu-id="09acb-155">Overview of SharePoint Framework Extensions</span></span>](../overview-extensions.md)