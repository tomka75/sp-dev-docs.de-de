---
title: Entwickeln mit dem Mandanten Berechtigungen mit App-Only in SharePoint Online
ms.date: 11/03/2017
ms.openlocfilehash: 7e4080cf1847a1dcf98d1dbb19149a4bbfa8edd5
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="developing-using-tenant-permissions-with-app-only-in-sharepoint-online"></a><span data-ttu-id="61558-102">Entwickeln mit dem Mandanten Berechtigungen mit App-Only in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="61558-102">Developing using Tenant permissions with App-Only in SharePoint Online</span></span>

<span data-ttu-id="61558-103">Die Entwicklerarbeit wurde SharePoint **gehostet durch Drittanbieter-Add-ins** , die **in Kombination mit nur-app - Mandanten**Erlaubnis geändert.</span><span class="sxs-lookup"><span data-stu-id="61558-103">The developer experience has changed for SharePoint **Provider-hosted Add-ins** that require **Tenant permission in combination with app-only**.</span></span> <span data-ttu-id="61558-104">Dieser Artikel führt Sie durch die neue Oberfläche für die Entwicklung und das Debuggen diese Lösungen.</span><span class="sxs-lookup"><span data-stu-id="61558-104">This article walks you through the new experience for developing and debugging these solutions.</span></span> 

<span data-ttu-id="61558-105">_**Gilt für:** Vom Anbieter gehosteten-Add-ins für SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="61558-105">_**Applies to:** Provider Hosted Add-ins for SharePoint Online_</span></span>


## <a name="understanding-the-problem"></a><span data-ttu-id="61558-106">Beschreibung des Problems</span><span class="sxs-lookup"><span data-stu-id="61558-106">Understanding the Problem</span></span>
<span data-ttu-id="61558-107">In Visual Studio Navigieren Sie zum Debuggen, Debuggen starten und eine Meldung angezeigt, "**Ihrer mandantenadministrator verfügt über diese app genehmigt**" wie im folgenden dargestellt werden.</span><span class="sxs-lookup"><span data-stu-id="61558-107">In Visual Studio, you navigate to Debug, start debugging and receive a message that "**Your tenant administrator has to approve this app**" as depicted below.</span></span>
<span data-ttu-id="61558-108">![](http://i.imgur.com/oFH9oqb.png).</span><span class="sxs-lookup"><span data-stu-id="61558-108"></span></span> 

<span data-ttu-id="61558-109">Der Grund, warum Sie ist nicht möglich, **vertrauensbezogener klicken,** ist, da Visual Studio für die Websitesammlung Dev funktioniert Sie in Ihrem projekteinstellungen festgelegt haben, die Berechtigungsstufe mit nur-app-Mandanten nur über [gewährt werden können sie anhand Ihres Mandanten vertrauen Verwaltungssite](https://msdn.microsoft.com/en-us/pnp_articles/how-to-provide-add-in-app-only-tenant-administrative-permissions-in-sharepoint-online).</span><span class="sxs-lookup"><span data-stu-id="61558-109">The reason why you can't click **trust it** is because Visual Studio is working against the dev site collection you've specified in your project settings whereas tenant level permissions with app-only can only be granted via [trusting it against your tenant administration site](https://msdn.microsoft.com/en-us/pnp_articles/how-to-provide-add-in-app-only-tenant-administrative-permissions-in-sharepoint-online).</span></span>

## <a name="walkthrough"></a><span data-ttu-id="61558-110">Exemplarische Vorgehensweise</span><span class="sxs-lookup"><span data-stu-id="61558-110">Walkthrough</span></span>
### <a name="step-1-create-a-new-service-principal"></a><span data-ttu-id="61558-111">Schritt 1: Erstellen einer neuen Dienstprinzipalnamen</span><span class="sxs-lookup"><span data-stu-id="61558-111">Step 1: Create a new service principal</span></span>
<span data-ttu-id="61558-112">Navigieren Sie zu einer Websitesammlung in Ihrem Mandanten, und generieren Sie eine neue Client-Id und geheimen Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="61558-112">Navigate to a site collection in your tenant and generate a new client Id and Secret.</span></span> <span data-ttu-id="61558-113">(Z. B. https://contoso.sharepoint.com/_layouts/15/appregnew.aspx).</span><span class="sxs-lookup"><span data-stu-id="61558-113">(E.g., https://contoso.sharepoint.com/_layouts/15/appregnew.aspx).</span></span> <span data-ttu-id="61558-114">Klicken Sie auf dieser Seite auf **generieren** für sowohl die **Client-Id**, **Geheimer Clientschlüssel** Felder und geben Sie die restlichen Felder an.</span><span class="sxs-lookup"><span data-stu-id="61558-114">In this page click **Generate** for both the **Client Id**, **Client Secret** Fields and supply the remaining fields.</span></span> <span data-ttu-id="61558-115">Während Sie entwickeln des Add-Ins Stellen Sie sicher, dass Sie den Port als App-Domäne einschließlich localhost.com verwenden.</span><span class="sxs-lookup"><span data-stu-id="61558-115">While you are developing the add-in ensure you use localhost.com including the port as the App Domain.</span></span> <span data-ttu-id="61558-116">Sie sollten dann in etwa wie unten verfügen.</span><span class="sxs-lookup"><span data-stu-id="61558-116">You should have something similar as below.</span></span>

![](http://i.imgur.com/5CfHgFD.png)

### <a name="step-2-grant-tenant-permissions"></a><span data-ttu-id="61558-117">Schritt 2: Grant-Mandanten Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="61558-117">Step 2: Grant Tenant Permissions</span></span>
<span data-ttu-id="61558-118">Um diesen Schritt ausführen zu können, müssen Sie eine SharePoint Online-Administrator sein.</span><span class="sxs-lookup"><span data-stu-id="61558-118">In order to perform this step, you must be a SharePoint Online Administrator.</span></span> 

<span data-ttu-id="61558-119">Navigieren Sie zu der SharePoint-Verwaltungskonsole (z. B. https://contoso-admin.sharepoint.com/_layouts/15/appinv.aspx) und erteilen Sie den Mandanten Berechtigungen.![](http://i.imgur.com/EGuJG3a.png)</span><span class="sxs-lookup"><span data-stu-id="61558-119">Navigate to the SharePoint Admin Center (E.g., https://contoso-admin.sharepoint.com/_layouts/15/appinv.aspx) and grant the tenant permissions ![](http://i.imgur.com/EGuJG3a.png)</span></span>

![](http://i.imgur.com/dst9ZdP.png)


### <a name="step-3-update-your-manifest-and-webconfig"></a><span data-ttu-id="61558-120">Schritt 3: Aktualisieren Sie Ihrer Manifest und in "Web.config"</span><span class="sxs-lookup"><span data-stu-id="61558-120">Step 3: Update your manifest and web.config</span></span>
<span data-ttu-id="61558-121">In der Visual Studio-Lösung Aktualisieren Sie das Manifest und web.config mit die Client-Id, die in Schritt 1 erstellte.</span><span class="sxs-lookup"><span data-stu-id="61558-121">In the Visual Studio solution; update the manifest and web.config with the client id created in step 1.</span></span>
![](http://i.imgur.com/fKkLIde.png)


### <a name="step-4-package-the-app-and-add-the-app-file-to-the-app-catalog"></a><span data-ttu-id="61558-122">Schritt 4: Packen Sie die app und fügen die Datei am Seitenrand zum App-Katalog hinzu</span><span class="sxs-lookup"><span data-stu-id="61558-122">Step 4: Package the app and add the .app file to the App catalog</span></span>
<span data-ttu-id="61558-123">Klicken Sie mit der rechten Maustaste auf die SharePoint-Add-in-Projekt, und klicken Sie auf veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="61558-123">Right click on the SharePoint Add-in project and click publish.</span></span>

<span data-ttu-id="61558-124">Geben Sie die **Client-ID** und ** Clientgeheimnis ** in Schritt 1 erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="61558-124">Supply the **Client ID** and **Client Secret **created in Step 1.</span></span>

![](http://i.imgur.com/XpM9rwb.png)

<span data-ttu-id="61558-125">Da Sie das Add-in debuggen möchten, müssen sicherstellen Sie, dass Sie https://localhost.com einschließlich des Ports, wie folgt angeben.</span><span class="sxs-lookup"><span data-stu-id="61558-125">Since you want to debug the add-in, ensure that you supply https://localhost.com including the port as depicted below.</span></span>
![](http://i.imgur.com/nQmSbPC.png)

<span data-ttu-id="61558-126">Nun das Add-in in der App-Katalog-Website bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="61558-126">Now deploy the add-in in the App Catalog site.</span></span>

### <a name="step-5-install-your-add-in-in-your-developer-site-collection"></a><span data-ttu-id="61558-127">Schritt 5: Installieren der add-Ins in Ihrer Websitesammlung für Entwickler</span><span class="sxs-lookup"><span data-stu-id="61558-127">Step 5: Install your add-in in your developer site collection</span></span>

<span data-ttu-id="61558-128">Navigieren Sie zu der Entwicklerwebsite für und fügen Sie die app hinzu.</span><span class="sxs-lookup"><span data-stu-id="61558-128">Navigate to the developer site and add the app.</span></span> <span data-ttu-id="61558-129">Klicken Sie auf **App-Details**.</span><span class="sxs-lookup"><span data-stu-id="61558-129">Click on **App Details**.</span></span>
![](http://i.imgur.com/Aihr4r7.png)

<span data-ttu-id="61558-130">Wenn Sie auf die Kachel app geklickt haben, müssen Sie auf klicken auf "**erfahren Sie, warum**" und Ihre app anfordern![](http://i.imgur.com/DwWUkG0.png)</span><span class="sxs-lookup"><span data-stu-id="61558-130">If you clicked on the app tile, you will have to click on "**Find out why**" and request your app ![](http://i.imgur.com/DwWUkG0.png)</span></span>

<span data-ttu-id="61558-131">Nachdem die Anforderung gesendet wurde werden der Status in aussteht, bis der SharePoint-Administrator oder den App-Katalog-Administrator die Anforderung genehmigt hat.</span><span class="sxs-lookup"><span data-stu-id="61558-131">Once the request has been submitted the status will be in a pending state until the SharePoint Administrator or the App Catalog Administrator approves the request.</span></span> <span data-ttu-id="61558-132">Um die Anforderung zu genehmigen, navigieren Sie zu den app-Katalog, App-Anforderungen und Genehmigen der Anforderung.</span><span class="sxs-lookup"><span data-stu-id="61558-132">To approve the request, navigate to the app catalog, App Requests and approve the request.</span></span>

![](http://i.imgur.com/yZ8vNEc.png)

<span data-ttu-id="61558-133">Nachdem die Anforderung genehmigt wurde kann das Add-in jetzt installiert werden.</span><span class="sxs-lookup"><span data-stu-id="61558-133">Once the request has been approved the add-in may now be installed.</span></span>

![](http://i.imgur.com/PMitOEY.png)

### <a name="step-6-debug-your-add-in"></a><span data-ttu-id="61558-134">Schritt 6: Debuggen von Ihr Add-in</span><span class="sxs-lookup"><span data-stu-id="61558-134">Step 6: Debug your Add-in</span></span>
<span data-ttu-id="61558-135">In Visual Studio rechten Maustaste klicken Sie auf das Webprojekt, und wählen Sie neue Instanz **Debuggen** starten.</span><span class="sxs-lookup"><span data-stu-id="61558-135">In Visual Studio right click your web project and select **Debug** Start new instance.</span></span> <span data-ttu-id="61558-136">Nach dem Start, navigieren Sie zu Ihrer Website, und starten Sie das Add-in.</span><span class="sxs-lookup"><span data-stu-id="61558-136">Once started, navigate to your site and launch the add-in.</span></span>

![](http://i.imgur.com/Y5vAlDr.png)

><span data-ttu-id="61558-137">**HINWEIS**</span><span class="sxs-lookup"><span data-stu-id="61558-137">**Note**</span></span>
> - <span data-ttu-id="61558-138">Wenn aus irgendeinem Grund der app beim Ändern Verpacken müssen Sie es in der app-Katalog erneut bereitstellen und installieren es erneut mit Ihrer Websitesammlung für die Entwicklung</span><span class="sxs-lookup"><span data-stu-id="61558-138">If for some reason your app package file changes you'll need to redeploy it to the app catalog and re-install it to your development site collection</span></span>
> - <span data-ttu-id="61558-139">Wenn Sie add-Ins sind hat einen Appinstalled Ereignisempfänger, den Sie benötigen, um sicherzustellen, dass Sie Schritt 6 durchgeführt haben, bevor Sie Schritt 5</span><span class="sxs-lookup"><span data-stu-id="61558-139">If you're add-in has an appinstalled event receiver you'll need to ensure that you've done step 6 before you do step 5</span></span>


## <a name="additional-resources"></a><span data-ttu-id="61558-140">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="61558-140">Additional resources</span></span>
<span data-ttu-id="61558-141"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="61558-141"></span></span>
- [<span data-ttu-id="61558-142">Add-in-app nur Mandanten Administratorberechtigungen in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="61558-142">Add-in app only tenant administrative permissions in SharePoint Online</span></span>](https://msdn.microsoft.com/en-us/pnp_articles/how-to-provide-add-in-app-only-tenant-administrative-permissions-in-sharepoint-online)
- [<span data-ttu-id="61558-143">Add-in-Berechtigungen in SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="61558-143">Add-in permissions in SharePoint 2013</span></span>](https://msdn.microsoft.com/en-us/library/office/fp142383.aspx)
- [<span data-ttu-id="61558-144">Hinweise zur App-Manifeststruktur und zum Paket eines SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="61558-144">Explore the app manifest structure and the package of a SharePoint Add-in</span></span>](https://msdn.microsoft.com/en-us/library/office/fp179918.aspx)

