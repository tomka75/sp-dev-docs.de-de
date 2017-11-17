---
title: How to Trust a Location
ms.date: 09/25/2017
keywords: how to,howdoi,howto,trusted location
f1_keywords: how to,howdoi,howto,trusted location
ms.prod: sharepoint
ms.assetid: 0f396c0b-f578-4d1a-9e6b-a75f352265ab
ms.openlocfilehash: 9c769a0d046a112253a61265373355eece0dade9
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-trust-a-location"></a><span data-ttu-id="47ac9-103">How to: Trust a Location</span><span class="sxs-lookup"><span data-stu-id="47ac9-103">How to: Trust a Location</span></span>

<span data-ttu-id="47ac9-p101">Workbooks that you want to access must be placed in a trusted location. If they are not, calls to open the workbooks will fail. This example shows you how to trust a location by using the SharePoint Central Administration page.</span><span class="sxs-lookup"><span data-stu-id="47ac9-p101">Workbooks that you want to access must be placed in a trusted location. If they are not, calls to open the workbooks will fail. This example shows you how to trust a location by using the SharePoint Central Administration page.</span></span> 
  
    
    

<span data-ttu-id="47ac9-p102">You can also trust a location by using Windows PowerShell. For more information, see the Microsoft SharePoint Server 2010 IT Pro and administration documentation on  [TechNet](http://technet.microsoft.com/en-us/library/ee428287%28office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="47ac9-p102">You can also trust a location by using Windows PowerShell. For more information, see the Microsoft SharePoint Server 2010 IT Pro and administration documentation on  [TechNet](http://technet.microsoft.com/en-us/library/ee428287%28office.14%29.aspx).</span></span> 
> <span data-ttu-id="47ac9-109">**Tipp:** Weitere Informationen über die Administrationsverbesserung und das Anzeigen von Screenshots der Seite Trusted File Locations finden Sie im Blog-Eintrag [Administrationsverbesserungen für Excel Services in SharePoint 2010](http://blogs.msdn.com/excel/archive/2009/11/16/excel-services-in-sharepoint-2010-administration-improvements.aspx).</span><span class="sxs-lookup"><span data-stu-id="47ac9-109">**TIP** For more information about administration improvement and to view screen shots of the Trusted File Locations page, see the blog post  [Excel Services in SharePoint 2010 Administration Improvements](http://blogs.msdn.com/excel/archive/2009/11/16/excel-services-in-sharepoint-2010-administration-improvements.aspx).</span></span> 
  
    
    


### <a name="to-trust-a-location"></a><span data-ttu-id="47ac9-110">Vertrauen zu einem Speicherort</span><span class="sxs-lookup"><span data-stu-id="47ac9-110">To trust a location</span></span>


1. <span data-ttu-id="47ac9-111">On the **Start** menu, click **All Programs**.</span><span class="sxs-lookup"><span data-stu-id="47ac9-111">On the **Start** menu, click **All Programs**.</span></span> 
    
  
2. <span data-ttu-id="47ac9-112">Point to **Microsoft SharePoint 2010 Products**, and then click **SharePoint 2010 Central Administration**.</span><span class="sxs-lookup"><span data-stu-id="47ac9-112">Point to **Microsoft SharePoint 2010 Products**, and then click **SharePoint 2010 Central Administration**.</span></span> 
    
  
3. <span data-ttu-id="47ac9-113">On the SharePoint 2010 Central Administration page, under **Application Management**, click **Manage service applications**.</span><span class="sxs-lookup"><span data-stu-id="47ac9-113">On the SharePoint 2010 Central Administration page, under **Application Management**, click **Manage service applications**.</span></span>
    
  
4. <span data-ttu-id="47ac9-114">On the Manage Service Application page, click **Excel Services Application**.</span><span class="sxs-lookup"><span data-stu-id="47ac9-114">On the Manage Service Application page, click **Excel Services Application**.</span></span>
    
  
5. <span data-ttu-id="47ac9-115">On the Manage Excel Services Application page, click **Trusted File Locations**.</span><span class="sxs-lookup"><span data-stu-id="47ac9-115">On the Manage Excel Services Application page, click **Trusted File Locations**.</span></span> 
    
  
6. <span data-ttu-id="47ac9-116">On the Excel Services Application Trusted File Locations page, click **Add Trusted File Location**.</span><span class="sxs-lookup"><span data-stu-id="47ac9-116">On the Excel Services Application Trusted File Locations page, click **Add Trusted File Location**.</span></span> 
    
  
7. <span data-ttu-id="47ac9-117">On the Excel Services Application Add Trusted File Location page, in the **Address** text box, type the location to save your workbookfor example,http:// _MyServer002_/Shared%20Documents.</span><span class="sxs-lookup"><span data-stu-id="47ac9-117">On the Excel Services Application Add Trusted File Location page, in the **Address** text box, type the location to save your workbook—for example,http:// _MyServer002_/Shared%20Documents.</span></span> 
    
  
8. <span data-ttu-id="47ac9-p103">Under **Location type**, click the appropriate location type. In this example, select **SharePoint Foundation**.</span><span class="sxs-lookup"><span data-stu-id="47ac9-p103">Under **Location type**, click the appropriate location type. In this example, select **SharePoint Foundation**.</span></span>
    
  
9. <span data-ttu-id="47ac9-120">Under **Trust Children**, select **Children trusted** if you want to trust child libraries or directories.</span><span class="sxs-lookup"><span data-stu-id="47ac9-120">Under **Trust Children**, select **Children trusted** if you want to trust child libraries or directories.</span></span>
    
  
10. <span data-ttu-id="47ac9-121">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="47ac9-121">Click **OK**.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="47ac9-122">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="47ac9-122">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="47ac9-123">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="47ac9-123">Tasks</span></span>


  
    
    
 [<span data-ttu-id="47ac9-124">Step 3: Deploying and Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="47ac9-124">Step 3: Deploying and Enabling UDFs</span></span>](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [<span data-ttu-id="47ac9-125">How to: Save from Excel Client to the Server</span><span class="sxs-lookup"><span data-stu-id="47ac9-125">How to: Save from Excel Client to the Server</span></span>](how-to-save-from-excel-client-to-the-server.md)
#### <a name="concepts"></a><span data-ttu-id="47ac9-126">Konzepte</span><span class="sxs-lookup"><span data-stu-id="47ac9-126">Concepts</span></span>


  
    
    
 [<span data-ttu-id="47ac9-127">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="47ac9-127">Excel Services Alerts</span></span>](excel-services-alerts.md)
#### <a name="other-resources"></a><span data-ttu-id="47ac9-128">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="47ac9-128">Other resources</span></span>


  
    
    
 [<span data-ttu-id="47ac9-129">Walkthrough: Developing a Custom Application Using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="47ac9-129">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
