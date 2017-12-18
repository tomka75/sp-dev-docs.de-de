---
title: >+
  Anwenden einer Gestaltungsvorlage auf eine Website in SharePoint

ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 04861390-84d5-40ea-b0db-6c0748eff196
ms.openlocfilehash: 8ee3d32510e02ffd6874dda5bbad9846e5a16442
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="apply-a-master-page-to-a-site-in-sharepoint"></a><span data-ttu-id="32745-102">Anwenden einer Gestaltungsvorlage auf eine Website in SharePoint
</span><span class="sxs-lookup"><span data-stu-id="32745-102">How to: Apply a master page to a site in SharePoint</span></span>
<span data-ttu-id="32745-103">In diesem Artikel erfahren Sie, wie Sie eine Gestaltungsvorlage einer SharePoint-Website zuordnen.</span><span class="sxs-lookup"><span data-stu-id="32745-103">Learn how to map a master page to a SharePoint site.</span></span>
## <a name="mapping-a-master-page-to-a-site"></a><span data-ttu-id="32745-104">Zuordnen einer Gestaltungsvorlage zu einer Website</span><span class="sxs-lookup"><span data-stu-id="32745-104">Mapping a master page to a site</span></span>

<span data-ttu-id="32745-p101">In SharePoint definiert eine Gestaltungsvorlage die gemeinsam genutzten Rahmenelemente, z. B. den Chrom, für alle Seiten Ihrer Website. Nach der Erstellung der Gestaltungsvorlage kann diese einer Website zugeordnet werden. Dies kann für alle Veröffentlichungsseiten erfolgen, die für alle Benutzer vorgesehen sind, aber auch für die administrativen Seiten, die zur Verwaltung der Website verwendet werden. Wenn Sie die untergeordnete Website einer übergeordneten Website konfigurieren, können Sie alternativ die Gestaltungsvorlage der übergeordneten Website übernehmen. In diesem Artikel sind die Schritte zum Zuordnen einer erstellten Gestaltungsvorlage zu einer Website, zum Übernehmen der Gestaltungsvorlage von einer übergeordneten Website, oder zum Zuordnen einer Gestaltungsseite zu einem bestimmten Gerätekanal enthalten.</span><span class="sxs-lookup"><span data-stu-id="32745-p101">In SharePoint, a master page defines the shared framing elements such as the chrome for all pages in your site. After a master page is created, it can be mapped to a site. This could be for all publishing pages designated for all users, or for the administrative pages used for site maintenance. Alternatively, if you are configuring a child site of a parent site, you can inherit the master page from the parent. This article provides the steps to map a created master page to a site, inherit the master page from a parent site, or map a master page to a specific device channel.</span></span>
  
    
    

> <span data-ttu-id="32745-110">**Hinweis:** Weitere Informationen zum Entwurfs-Manager und zu Gestaltungsvorlagen finden Sie unter [Übersicht über den Entwurfs-Manager in SharePoint](overview-of-design-manager-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="32745-110">**Note:** For more information about Design Manager and master pages, see  [Overview of Design Manager in SharePoint](overview-of-design-manager-in-sharepoint.md).</span></span> <span data-ttu-id="32745-111">Weitere Informationen zum Erstellen von Gerätekanälen finden Sie unter [SharePoint-Entwurfs-Manager-Gerätekanäle](sharepoint-design-manager-device-channels.md).</span><span class="sxs-lookup"><span data-stu-id="32745-111">For more information about how to create device channels, see  [SharePoint Design Manager device channels](sharepoint-design-manager-device-channels.md).</span></span> 
  
    
    


### <a name="to-map-a-master-page-to-a-sharepoint-site"></a><span data-ttu-id="32745-112">So ordnen Sie eine Gestaltungsvorlage einer SharePoint-Website zu</span><span class="sxs-lookup"><span data-stu-id="32745-112">To map a master page to a SharePoint site</span></span>


1.  <span data-ttu-id="32745-113">Klicken Sie in den **Websiteeinstellungen** für die vorgesehene Website im Abschnitt **Aussehen und Verhalten** auf **Gestaltungsvorlage**.</span><span class="sxs-lookup"><span data-stu-id="32745-113">In **Site Settings** for the designated site, under the **Look and Feel** section, choose **Master Page**.</span></span>
    
    > <span data-ttu-id="32745-114">**Hinweis:** Wenn der Link **Gestaltungsvorlage** nicht vorhanden ist, müssen Sie das Veröffentlichungsfeature mit den folgenden Schritten aktivieren.</span><span class="sxs-lookup"><span data-stu-id="32745-114">**Note:** If the **Master Page** link is not there, you need to enable the publishing feature with these steps.</span></span> <span data-ttu-id="32745-115">Navigieren Sie zu **Websiteeinstellungen | Websitesammlungsverwaltung | Websitesammlungsfeatures**.</span><span class="sxs-lookup"><span data-stu-id="32745-115">Navigate to **Site Settings | Site Collection Administration | Site Collection Features**.</span></span> <span data-ttu-id="32745-116">Scrollen Sie nach unten zum Feature **SharePoint Server-Veröffentlichungsinfrastruktur**, und klicken Sie auf **Aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="32745-116">Scroll down to the **SharePoint Server Publishing Infrastructure** feature and press **Activate**.</span></span> 
2. <span data-ttu-id="32745-117">Wählen Sie in den **Einstellungen für die Gestaltungsvorlage der Website** eine der beiden Optionen für die Abschnitte **Gestaltungsvorlage der Website** oder **Systemgestaltungsvorlage** aus:</span><span class="sxs-lookup"><span data-stu-id="32745-117">On **Site Master Page Settings**, select one of the two options for the **Site Master Page** or **System Master Page** sections:</span></span>
    
  - <span data-ttu-id="32745-118">**Gestaltungsvorlage für die Website von der übergeordneten Website erben**: Wählen Sie diese Option aus, wenn Sie eine untergeordnete SharePoint-Website konfigurieren und die Gestaltungsvorlage der übergeordneten Website verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="32745-118">**Inherit site master page from parent site** Choose this option if you are configuring a child SharePoint site and want to use the parent master page.</span></span>
    
    > <span data-ttu-id="32745-119">**Hinweis: ** Diese Option ist nicht verfügbar, wenn Sie auf der übergeordneten Website der obersten Ebene arbeiten.</span><span class="sxs-lookup"><span data-stu-id="32745-119">**Note:** If you are working on the top-level parent site this option is unavailable.</span></span> 
  - <span data-ttu-id="32745-p104">**Eine Gestaltungsvorlage für die Website und alle erbenden Websites angeben**: Wählen Sie diese Option, wenn Sie eine bestimmte Gestaltungsvorlage zur Website oder eine bestimmte Gestaltungsvorlage für administrative Seiten zuordnen möchten. Es ist das Dropdownfeld **Standard** oder **Alle Kanäle** in Abhängigkeit von Ihrer Website oder Systemkonfiguration verfügbar, daher können Sie eine bestimmte Gestaltungsvorlage auswählen, die im Gestaltungsvorlagenkatalog enthalten ist. Wählen Sie die gewünschte Gestaltungsvorlage aus dem Dropdownfeld aus.</span><span class="sxs-lookup"><span data-stu-id="32745-p104">**Specify a master page to be used by this site and all sites that inherit from it** Choose this option if you want to map a specific master page to the site, or if you want to map a specific master page for administrative pages. A drop-down box named **Default** or **All Channels** is available for you, depending on your site or system configuration, so you can select a specific master page stored in the master page gallery. Select the desired master page from the drop-down box.</span></span>
    
    > <span data-ttu-id="32745-123">**Hinweis:** Wenn Gerätekanäle konfiguriert sind, stehen weitere Dropdownfelder für zusätzliche Zuordnungsoptionen für Gestaltungsvorlagen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="32745-123">**Note:** If you have any device channels configured, there are additional drop-down boxes available for additional master page mapping options.</span></span> 
3. <span data-ttu-id="32745-124">Wählen Sie **OK** aus.</span><span class="sxs-lookup"><span data-stu-id="32745-124">Choose **OK**.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="32745-125">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="32745-125">Additional resources</span></span>
<span data-ttu-id="32745-126"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="32745-126"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="32745-127">Entwickeln des Website-Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="32745-127">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  
-  [<span data-ttu-id="32745-128">Übersicht über den Entwurfs-Manager in SharePoint</span><span class="sxs-lookup"><span data-stu-id="32745-128">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="32745-129">Neuerung bei SharePoint-Websiteentwicklung</span><span class="sxs-lookup"><span data-stu-id="32745-129">What's new with SharePoint site development</span></span>](what-s-new-with-sharepoint-site-development.md)
    
  

