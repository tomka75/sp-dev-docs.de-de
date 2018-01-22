---
title: Einrichten des Office 365-Mandanten
description: Erstellen Sie clientseitige Webparts mithilfe von SharePoint Framework, und stellen Sie diese bereit, indem Sie einen Office 365-Mandanten einrichten.
ms.date: 01/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 5981b4eaca349700a78cbbdf39eef376cb6d56e4
ms.sourcegitcommit: 2188f21ce207c9d62d7d8af93822bd101058ba2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/10/2018
---
# <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="cbc3f-103">Einrichten des Office 365-Mandanten</span><span class="sxs-lookup"><span data-stu-id="cbc3f-103">Set up your Office 365 tenant</span></span>

<span data-ttu-id="cbc3f-104">Zum Erstellen und Bereitstellen von clientseitigen Webparts mithilfe von SharePoint Framework benötigen Sie einen Office 365-Mandanten.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-104">To build and deploy client-side web parts using the preview release of the SharePoint Framework, you will need an Office 365 tenant with First Release options enabled.</span></span> 

<span data-ttu-id="cbc3f-105">Wenn Sie bereits einen Office 365-Mandanten haben, finden Sie Informationen unter [Erstellen der App-Katalogwebsite](#create-app-catalog-site).</span><span class="sxs-lookup"><span data-stu-id="cbc3f-105">If you already have an Office 365 tenant, see [create your app catalog site](#create-app-catalog-site).</span></span>

<span data-ttu-id="cbc3f-106">Wenn Sie keinen Mandanten haben, können Sie einen Testmandanten erstellen, oder melden Sie sich für das [Office 365 Developer-Programm](https://dev.office.com/devprogram) an.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-106">If you don't have one, you can create a trial tenant or for example sign up for the [Office Developer Program](https://dev.office.com/devprogram).</span></span>  

> [!NOTE] 
> <span data-ttu-id="cbc3f-107">Stellen Sie sicher, dass Sie von allen vorhandenen Office 365-Mandanten abgemeldet sind, bevor Sie sich anmelden.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-107">Make sure that you are signed out of any existing Office 365 tenants before you sign up.</span></span>

## <a name="create-app-catalog-site"></a><span data-ttu-id="cbc3f-108">Erstellen der App-Katalogwebsite</span><span class="sxs-lookup"><span data-stu-id="cbc3f-108">Create app catalog site</span></span>

<span data-ttu-id="cbc3f-109">Sie benötigen einen App-Katalog zum Hochladen und Bereitstellen von Webparts.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-109">You will need an app catalog to upload and deploy web parts.</span></span> <span data-ttu-id="cbc3f-110">Wenn Sie bereits einen App-Katalog eingerichtet haben, finden Sie Informationen unter [Erstellen einer neuen Entwicklerwebsitesammlung](#create-a-new-developer-site-collection).</span><span class="sxs-lookup"><span data-stu-id="cbc3f-110">If you've already set up an app catalog, see [create a new Developer Site collection](#create-a-new-developer-site-collection).</span></span>  

### <a name="to-create-an-app-catalog-site"></a><span data-ttu-id="cbc3f-111">So erstellen Sie eine App-Katalogwebsite</span><span class="sxs-lookup"><span data-stu-id="cbc3f-111">To create an app catalog site</span></span>

1. <span data-ttu-id="cbc3f-112">Wechseln Sie zum **SharePoint Admin Center**, indem Sie die folgende URL in den Browser eingeben.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-112">Go to the **SharePoint Admin Center** by entering the following URL in your browser.</span></span> <span data-ttu-id="cbc3f-113">Ersetzen Sie **yourtenantprefix** durch das Präfix Ihres Office 365-Entwicklermandanten.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-113">Replace **yourtenantprefix** with your Office 365 Developer Tenant prefix.</span></span>
    
    ```
    https://yourtenantprefix-admin.sharepoint.com
    ```
    
2. <span data-ttu-id="cbc3f-114">Wählen Sie in der linken Randleiste das Menüelement **Apps** und dann **App-Katalog** aus.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-114">In the left sidebar, choose the **apps** menu item and then choose **App Catalog**.</span></span>

3. <span data-ttu-id="cbc3f-115">Wählen Sie **OK** aus, um eine neue App-Katalogwebsite zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-115">Choose **OK** to create a new app catalog site.</span></span>

4. <span data-ttu-id="cbc3f-116">Geben Sie auf der nächsten Seite die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="cbc3f-116">In the next page, enter the following details:</span></span>

    - <span data-ttu-id="cbc3f-117">**Titel**: Geben Sie **App-Katalog** ein.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-117">**Title**: Enter **App Catalog**.</span></span>
    - <span data-ttu-id="cbc3f-118">**Websiteadressen_-Suffix_**: Geben Sie Ihren bevorzugten Suffix für den App-Katalog ein. Beispiel: **Apps**.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-118">**Web Site Address _suffix_**: Enter your preferred suffix for the app catalog; for example: **apps**.</span></span>
    - <span data-ttu-id="cbc3f-119">**Administrator**: Geben Sie Ihren Benutzernamen ein, und wählen Sie die Schaltfläche **Auflösen** aus, um den Benutzernamen aufzulösen.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-119">**Administrator**: Enter your username and choose the **resolve** button to resolve the username.</span></span>

5. <span data-ttu-id="cbc3f-120">Wählen Sie **OK** aus, um die App-Katalogwebsite zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-120">Choose **OK** to create the app catalog site.</span></span>

<span data-ttu-id="cbc3f-121">SharePoint erstellt die App-Katalogwebsite. Den Fortschritt können Sie im SharePoint Admin Center ablesen.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-121">SharePoint will create the app catalog site and you will be able to see its progress in the SharePoint admin center.</span></span>

## <a name="create-a-new-developer-site-collection"></a><span data-ttu-id="cbc3f-122">Erstellen einer neuen Entwicklerwebsitesammlung</span><span class="sxs-lookup"><span data-stu-id="cbc3f-122">Create a new Developer Site collection</span></span>

<span data-ttu-id="cbc3f-123">Sie benötigen ferner eine Websitesammlung und eine Website zum Testen.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-123">You also need a site collection and a site for your testing.</span></span> <span data-ttu-id="cbc3f-124">Sie können eine neue Websitesammlung mit jeder der verfügbaren Vorlagen erstellen.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-124">You can create a new site collection using any of the available templates.</span></span> <span data-ttu-id="cbc3f-125">Sie können die **Entwicklerwebsitesammlung** verwenden, dies hat aber nicht wirklich einen Mehrwert, da Workbench- und Basistests mit einer beliebigen Website ausgeführt werden können.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-125">You may chose to use **developer site collection**, but that does not really add additional value, since workbench and basic testing can be performed under any site.</span></span>

### <a name="to-create-a-new-developer-site-collection"></a><span data-ttu-id="cbc3f-126">So erstellen Sie eine neue Entwicklerwebsitesammlung</span><span class="sxs-lookup"><span data-stu-id="cbc3f-126">To create the new site collection</span></span>

1. <span data-ttu-id="cbc3f-127">Wechseln Sie zum **SharePoint Admin Center**, indem Sie die folgende URL in den Browser eingeben.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-127">Go to the **SharePoint Admin Center** by entering the following URL in your browser.</span></span> <span data-ttu-id="cbc3f-128">Ersetzen Sie **yourtenantprefix** durch das Präfix Ihres Office 365-Entwicklermandanten.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-128">Replace **yourtenantprefix** with your Office 365 Developer Tenant prefix.</span></span>
    
    ```
    https://yourtenantprefix-admin.sharepoint.com
    ```
    
2. <span data-ttu-id="cbc3f-129">Wählen Sie im SharePoint-Menüband **Neu** > **Private Websitesammlung** aus.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-129">In the SharePoint ribbon, choose **New** > **Private Site Collection**.</span></span>

3. <span data-ttu-id="cbc3f-130">Geben Sie in das Dialogfeld die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="cbc3f-130">In the dialog box, enter the following details:</span></span>

    - <span data-ttu-id="cbc3f-131">**Titel**: Geben Sie einen Titel für Ihre Entwicklerwebsitesammlung ein. Beispiel: **Entwicklerwebsite**.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-131">**Title**: Enter a title for your developer site collection; for example: **Developer Site**.</span></span>
    - <span data-ttu-id="cbc3f-132">**Websiteadressen_-Suffix_**: Geben Sie einen Suffix für Ihre Entwicklerwebsitesammlung ein. Beispiel: **Dev**</span><span class="sxs-lookup"><span data-stu-id="cbc3f-132">**Web Site Address _suffix_**: Enter a suffix for your developer site collection; for example: **dev**.</span></span>
    - <span data-ttu-id="cbc3f-133">**Vorlagenauswahl**: Wählen Sie **Entwicklerwebsite** als die Vorlage für die Websitesammlung aus.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-133">**Template Selection**: Select **Developer Site** as the site collection template.</span></span>
    - <span data-ttu-id="cbc3f-134">**Administrator**: Geben Sie Ihren Benutzernamen ein, und wählen Sie die Schaltfläche **Auflösen** aus, um den Benutzernamen aufzulösen.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-134">**Administrator**: Enter your username and choose the **resolve** button to resolve the username.</span></span>

4. <span data-ttu-id="cbc3f-135">Klicken Sie auf **OK**, um die Websitesammlung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-135">Choose **OK** to create the site collection.</span></span>

<span data-ttu-id="cbc3f-136">SharePoint erstellt die Entwicklerwebsite. Den Fortschritt können Sie im SharePoint Admin Center ablesen.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-136">SharePoint will create the app catalog site and you will be able to see its progress in the SharePoint admin center.</span></span> <span data-ttu-id="cbc3f-137">Nachdem die Website erstellt wurde, können Sie zu Ihrer Entwicklerwebsitesammlung wechseln.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-137">After the site is created, you can browse to your developer site collection.</span></span>

## <a name="sharepoint-workbench"></a><span data-ttu-id="cbc3f-138">SharePoint Workbench</span><span class="sxs-lookup"><span data-stu-id="cbc3f-138">SharePoint Workbench</span></span>

<span data-ttu-id="cbc3f-139">SharePoint Workbench ist eine Designoberfläche für Entwickler, mit der Sie schnell Webpart-Tests durchführen und eine Webpart-Vorschau anzeigen können, und zwar ohne die Webparts in SharePoint bereitstellen zu müssen.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-139">SharePoint Workbench is a developer design surface that enables you to quickly preview and test web parts without deploying them in SharePoint. SharePoint Workbench includes the client-side page and the client-side canvas in which you can add, delete and test your web parts in development.</span></span> <span data-ttu-id="cbc3f-140">Die SharePoint Framework Developer-Toolkette enthält eine Version der Workbench, die lokal ausgeführt wird und Ihnen hilft, erstellte Lösungen schnell zu testen und zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-140">SharePoint Framework developer toolchain contains a version of the Workbench that works locally and helps you quickly test and validate solutions that you are building.</span></span> <span data-ttu-id="cbc3f-141">Sie lässt sich auch in Ihrem Mandanten hosten, um während der Entwicklung lokaler Webparts eine Webpart-Vorschau anzuzeigen und Tests durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-141">It is also hosted in your tenancy to preview and test your local web parts in development.</span></span> <span data-ttu-id="cbc3f-142">Unter der folgenden URL können Sie auf die SharePoint Workbench von jeder SharePoint-Website in Ihrem Mandanten aus zugreifen:</span><span class="sxs-lookup"><span data-stu-id="cbc3f-142">You can access the SharePoint Workbench from any SharePoint site in your tenancy by browsing to the following URL:</span></span>

```
https://your-sharepoint-site/_layouts/workbench.aspx
```

## <a name="next-steps"></a><span data-ttu-id="cbc3f-143">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="cbc3f-143">Next steps</span></span>

<span data-ttu-id="cbc3f-144">Da Sie jetzt Ihren SharePoint-Mandanten konfiguriert, [richten Sie Ihre Entwicklungsumgebung ein](./set-up-your-development-environment.md), um clientseitige Webparts zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="cbc3f-144">Now that you have configured your SharePoint tenant, [set up your development environment](./set-up-your-development-environment.md) to build client-side web parts.</span></span>
