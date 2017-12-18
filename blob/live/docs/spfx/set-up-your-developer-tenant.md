---
title: Einrichten des Office 365-Mandanten
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 3f9b57d55b0e23c3acb4587552a2fad5626bbbd0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="0105c-102">Einrichten des Office 365-Mandanten</span><span class="sxs-lookup"><span data-stu-id="0105c-102">Set up your Office 365 tenant</span></span>

<span data-ttu-id="0105c-103">Zum Erstellen und Bereitstellen von clientseitigen Webparts mithilfe der Preview-Version von SharePoint Framework benötigen Sie einen Office 365-Mandanten.</span><span class="sxs-lookup"><span data-stu-id="0105c-103">To build and deploy client-side web parts using the preview release of the SharePoint Framework, you will need a normal Office 365 tenant.</span></span> 

## <a name="sign-up-for-an-office-365-tenant"></a><span data-ttu-id="0105c-104">Registrieren für einen Office 365-Mandanten</span><span class="sxs-lookup"><span data-stu-id="0105c-104">Sign up for an Office 365 tenant</span></span>
<span data-ttu-id="0105c-105">Wenn Sie bereits einen Office 365-Mandanten haben, finden Sie Informationen unter [Erstellen der App-Katalogwebsite](#create-app-catalog-site).</span><span class="sxs-lookup"><span data-stu-id="0105c-105">If you already have an Office 365 tenant, see [create your app catalog site](#create-app-catalog-site).</span></span>

<span data-ttu-id="0105c-106">Wenn Sie keinen Mandanten haben, können Sie einen Testmandanten erstellen, oder melden Sie sich beispielsweise für das [Office Developer-Programm](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=7a6e3d71-b057-49cc-b2aa-158ff23432f3&lcid=1033&culture=en-us&dir=LTR) an.</span><span class="sxs-lookup"><span data-stu-id="0105c-106">If you don't have one, you can create a trial tenant or for example sign up for the Office Developer Program. You will receive a welcome mail with a link to sign up for an Office 365 Developer Tenant.</span></span> <span data-ttu-id="0105c-107">Sie erhalten eine Willkommens-E-Mail mit einem Link zum Registrieren für einen Office 365-Entwicklermandanten.</span><span class="sxs-lookup"><span data-stu-id="0105c-107">If you don't have one, you can create a trial tenant or for example sign up for the Office Developer Program. You will receive a welcome mail with a link to sign up for an Office 365 Developer Tenant.</span></span> 

><span data-ttu-id="0105c-108">**Hinweis:** Stellen Sie sicher, dass Sie von allen vorhandenen Office 365-Mandanten abgemeldet sind, bevor Sie sich anmelden.</span><span class="sxs-lookup"><span data-stu-id="0105c-108">**Note:** Make sure that you are signed out of any existing Office 365 tenants before you sign up.</span></span>

## <a name="create-app-catalog-site"></a><span data-ttu-id="0105c-109">Erstellen der App-Katalogwebsite</span><span class="sxs-lookup"><span data-stu-id="0105c-109">Create app catalog site</span></span>
<span data-ttu-id="0105c-110">Sie benötigen einen App-Katalog zum Hochladen und Bereitstellen von Webparts.</span><span class="sxs-lookup"><span data-stu-id="0105c-110">You will need an app catalog to upload and deploy web parts. If you've already set up an app catalog, see create a new Developer Site collection.</span></span> <span data-ttu-id="0105c-111">Wenn Sie bereits einen App-Katalog eingerichtet haben, finden Sie Informationen unter [Erstellen einer neuen Entwicklerwebsitesammlung](#create-a-new-developer-site-collection).</span><span class="sxs-lookup"><span data-stu-id="0105c-111">You will need an app catalog to upload and deploy web parts. If you've already set up an app catalog, see [create a new Developer Site collection](#create-a-new-developer-site-collection).</span></span>  

<span data-ttu-id="0105c-112">Wechseln Sie zum **SharePoint Admin Center**, indem Sie die folgende URL in den Browser eingeben.</span><span class="sxs-lookup"><span data-stu-id="0105c-112">Go to the **SharePoint Admin Center** by entering the following URL in your browser. Replace yourtenantprefix with your Office 365 Developer Tenant prefix.</span></span> <span data-ttu-id="0105c-113">Ersetzen Sie **yourtenantprefix** durch das Präfix Ihres Office 365-Entwicklermandanten.</span><span class="sxs-lookup"><span data-stu-id="0105c-113">Replace **yourtenantprefix** with your Office 365 Developer Tenant prefix.</span></span>
    
```
https://yourtenantprefix-admin.sharepoint.com
```
    
<span data-ttu-id="0105c-114">Wählen Sie in der linken Randleiste das Menüelement **Apps** und dann **App-Katalog** aus.</span><span class="sxs-lookup"><span data-stu-id="0105c-114">In the left sidebar, choose the **apps** menu item and then choose **App Catalog**.</span></span>

<span data-ttu-id="0105c-115">Wählen Sie **OK** aus, um eine neue App-Katalogwebsite zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0105c-115">Choose **OK** to create a new app catalog site.</span></span>

<span data-ttu-id="0105c-116">Geben Sie auf der nächsten Seite die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="0105c-116">In the next page, enter the following details:</span></span>

* <span data-ttu-id="0105c-117">**Titel**: Geben Sie **App-Katalog** ein.</span><span class="sxs-lookup"><span data-stu-id="0105c-117">**Title**: Enter **App Catalog**.</span></span>
* <span data-ttu-id="0105c-118">**Websiteadressen_-Suffix_**: Geben Sie Ihren bevorzugten Suffix für den App-Katalog ein. Beispiel: **Apps**.</span><span class="sxs-lookup"><span data-stu-id="0105c-118">**Web Site Address _suffix_**: Enter your preferred suffix for the app catalog; for example: **apps**.</span></span>
* <span data-ttu-id="0105c-119">**Administrator**: Geben Sie Ihren Benutzernamen ein, und wählen Sie die Schaltfläche **Auflösen** aus, um den Benutzernamen aufzulösen.</span><span class="sxs-lookup"><span data-stu-id="0105c-119">**Administrator**: Enter your username and choose the **resolve** button to resolve the username.</span></span>

<span data-ttu-id="0105c-120">Wählen Sie **OK** aus, um die App-Katalogwebsite zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0105c-120">Choose **OK** to create the app catalog site.</span></span>

<span data-ttu-id="0105c-121">SharePoint erstellt die App-Katalogwebsite. Den Fortschritt können Sie im SharePoint Admin Center ablesen.</span><span class="sxs-lookup"><span data-stu-id="0105c-121">SharePoint will create the app catalog site and you will be able to see its progress in the SharePoint admin center.</span></span>

## <a name="create-a-new-developer-site-collection"></a><span data-ttu-id="0105c-122">Erstellen einer neuen Entwicklerwebsitesammlung</span><span class="sxs-lookup"><span data-stu-id="0105c-122">Create a new Developer Site collection</span></span>
<span data-ttu-id="0105c-123">Sie benötigen ferner eine Websitesammlung und eine Website zum Testen.</span><span class="sxs-lookup"><span data-stu-id="0105c-123">You also need a site collection and a site for your testing.</span></span> <span data-ttu-id="0105c-124">Sie können eine neue Websitesammlung mit jeder der verfügbaren Vorlagen erstellen.</span><span class="sxs-lookup"><span data-stu-id="0105c-124">You can create a new site collection using any of the available templates.</span></span> <span data-ttu-id="0105c-125">Sie können die **Entwicklerwebsitesammlung** verwenden, dies hat aber nicht wirklich einen Mehrwert, da Workbench- und Basistests mit einer beliebigen Website ausgeführt werden können.</span><span class="sxs-lookup"><span data-stu-id="0105c-125">You also need a site collection and a site for your testing. You can create a new site collection using any of the available templates. You may chose to use **developer site collection**, but that does not really add additional value, since workbench and basic testing can be performed under any site.</span></span>

<span data-ttu-id="0105c-126">Im Folgenden sind die Schritte zum Erstellen einer neuen Entwicklerwebsitesammlung aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="0105c-126">Here are steps for creating new developer site collection.</span></span>

 <span data-ttu-id="0105c-127">Wechseln Sie zum **SharePoint Admin Center**, indem Sie die folgende URL in den Browser eingeben.</span><span class="sxs-lookup"><span data-stu-id="0105c-127">Go to the **SharePoint Admin Center** by entering the following URL in your browser. Replace yourtenantprefix with your Office 365 Developer Tenant prefix.</span></span> <span data-ttu-id="0105c-128">Ersetzen Sie **yourtenantprefix** durch das Präfix Ihres Office 365-Entwicklermandanten.</span><span class="sxs-lookup"><span data-stu-id="0105c-128">Replace **yourtenantprefix** with your Office 365 Developer Tenant prefix.</span></span>
    
```
https://yourtenantprefix-admin.sharepoint.com
```
    
<span data-ttu-id="0105c-129">Wählen Sie im SharePoint-Menüband **Neu** -> **Private Websitesammlung** aus.</span><span class="sxs-lookup"><span data-stu-id="0105c-129">In the SharePoint ribbon, choose **New** -> **Private Site Collection**.</span></span>

<span data-ttu-id="0105c-130">Geben Sie in das Dialogfeld die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="0105c-130">In the dialog box, enter the following details:</span></span>

* <span data-ttu-id="0105c-131">**Titel**: Geben Sie einen Titel für Ihre Entwicklerwebsitesammlung ein. Beispiel: **Entwicklerwebsite**.</span><span class="sxs-lookup"><span data-stu-id="0105c-131">**Title**: Enter a title for your developer site collection; for example: **Developer Site**.</span></span>
* <span data-ttu-id="0105c-132">**Websiteadressen_-Suffix_**: Geben Sie einen Suffix für Ihre Entwicklerwebsitesammlung ein. Beispiel: **Dev**</span><span class="sxs-lookup"><span data-stu-id="0105c-132">**Web Site Address _suffix_**: Enter a suffix for your developer site collection; for example: **dev**.</span></span>
* <span data-ttu-id="0105c-133">**Vorlagenauswahl**: Wählen Sie **Entwicklerwebsite** als die Vorlage für die Websitesammlung aus.</span><span class="sxs-lookup"><span data-stu-id="0105c-133">**Template Selection**: Select **Developer Site** as the site collection template.</span></span>
* <span data-ttu-id="0105c-134">**Administrator**: Geben Sie Ihren Benutzernamen ein, und wählen Sie die Schaltfläche **Auflösen** aus, um den Benutzernamen aufzulösen.</span><span class="sxs-lookup"><span data-stu-id="0105c-134">**Administrator**: Enter your username and choose the **resolve** button to resolve the username.</span></span>

<span data-ttu-id="0105c-135">Klicken Sie auf **OK**, um die Websitesammlung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0105c-135">Choose **OK** to create the site collection.</span></span>

<span data-ttu-id="0105c-p106">SharePoint erstellt die Entwicklerwebsite. Den Fortschritt können Sie im SharePoint Admin Center ablesen. Nachdem die Website erstellt wurde, können Sie zu Ihrer Entwicklerwebsitesammlung wechseln.</span><span class="sxs-lookup"><span data-stu-id="0105c-p106">SharePoint will create the developer site and you will be able to see its progress in the SharePoint admin center. After the site is created, you can browse to your developer site collection.</span></span>

## <a name="sharepoint-workbench"></a><span data-ttu-id="0105c-138">SharePoint Workbench</span><span class="sxs-lookup"><span data-stu-id="0105c-138">SharePoint Workbench</span></span>
<span data-ttu-id="0105c-p107">SharePoint Workbench ist eine Designoberfläche für Entwickler, mit der Sie schnell Webpart-Tests durchführen und eine Webpart-Vorschau anzeigen können, und zwar ohne die Webparts in SharePoint bereitstellen zu müssen. Die SharePoint Framework Developer-Toolkette enthält eine Version der Workbench, die lokal ausgeführt wird und Ihnen hilft, erstellte Lösungen schnell zu testen und zu überprüfen. Sie lässt sich auch in Ihrem Mandanten hosten, um während der Entwicklung lokaler Webparts eine Webpart-Vorschau anzuzeigen und Tests durchzuführen. Unter der folgenden URL können Sie auf die SharePoint Workbench von jeder SharePoint-Website in Ihrem Mandanten aus zugreifen:</span><span class="sxs-lookup"><span data-stu-id="0105c-p107">SharePoint Workbench is a developer design surface that enables you to quickly preview and test web parts without deploying them in SharePoint. SharePoint Framework developer toolchain contains a version of the Workbench that works locally and helps you quickly test and validate solutions you are building. It is also hosted in your tenancy to preview and test your local web parts in development. You can access the SharePoint Workbench from any SharePoint site in your tenancy by browsing to the following URL:</span></span>

```
https://your-sharepoint-site/_layouts/workbench.aspx
```

## <a name="next-steps"></a><span data-ttu-id="0105c-143">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="0105c-143">Next steps</span></span>
<span data-ttu-id="0105c-144">Da Sie jetzt Ihren SharePoint-Mandanten konfiguriert, [richten Sie Ihre Entwicklungsumgebung ein](./set-up-your-development-environment.md), um clientseitige Webparts zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0105c-144">Now that you have configured your SharePoint tenant, [set up your development environment](./set-up-your-development-environment.md) to build client-side web parts.</span></span>
