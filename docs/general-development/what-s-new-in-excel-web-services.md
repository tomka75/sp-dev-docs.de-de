---
title: Neuigkeiten in Excel Web Services
ms.prod: SHAREPOINT
ms.assetid: cb342e94-0308-4608-b027-b73ebe8107b0
ms.openlocfilehash: f5aceebaf28e8caf4ac99beb97de6b87e21d149c
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2017
---
# <a name="whats-new-in-excel-web-services"></a><span data-ttu-id="2fda1-102">Neuigkeiten in Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="2fda1-102">What's New in Excel Web Services</span></span>

<span data-ttu-id="2fda1-103">This topic lists the new types and members added to Excel Web Services.</span><span class="sxs-lookup"><span data-stu-id="2fda1-103">This topic lists the new types and members added to Excel Web Services.</span></span>
  
    
    


## <a name="excel-web-services-enhancements"></a><span data-ttu-id="2fda1-104">Excel Web Services Enhancements</span><span class="sxs-lookup"><span data-stu-id="2fda1-104">Excel Web Services Enhancements</span></span>

<span data-ttu-id="2fda1-p101">Excel Web Services is expanded and enhanced in Microsoft SharePoint Server 2010. In SharePoint Server 2010, you can edit and save a workbook programmatically. In addition, the Excel Web Services now supports opening workbooks in edit sessions in SharePoint Server 2010. In this scenario, you can use code to edit a workbook at the same time that other users are co-authoring the workbook.</span><span class="sxs-lookup"><span data-stu-id="2fda1-p101">Excel Web Services is expanded and enhanced in Microsoft SharePoint Server 2010. In SharePoint Server 2010, you can edit and save a workbook programmatically. In addition, the Excel Web Services now supports opening workbooks in edit sessions in SharePoint Server 2010. In this scenario, you can use code to edit a workbook at the same time that other users are co-authoring the workbook.</span></span>
  
    
    
<span data-ttu-id="2fda1-109">For more information about the Excel Web Services API and more detailed remarks about the new methods, enumerations, and types, see **Microsoft.Office.Excel.Server.WebServices**.</span><span class="sxs-lookup"><span data-stu-id="2fda1-109">For more information about the Excel Web Services API and more detailed remarks about the new methods, enumerations, and types, see **Microsoft.Office.Excel.Server.WebServices**.</span></span>
  
    
    

### <a name="new-methods"></a><span data-ttu-id="2fda1-110">Neue Methoden</span><span class="sxs-lookup"><span data-stu-id="2fda1-110">New Methods</span></span>

<span data-ttu-id="2fda1-111">The following are new methods added to Excel Web Services, in alphabetical order:</span><span class="sxs-lookup"><span data-stu-id="2fda1-111">The following are new methods added to Excel Web Services, in alphabetical order:</span></span> 
  
    
    

- <span data-ttu-id="2fda1-112">**GetChartImageUrl** Gets a URL value to the chart or PivotChart image file in a workbook.</span><span class="sxs-lookup"><span data-stu-id="2fda1-112">**GetChartImageUrl** Gets a URL value to the chart or PivotChart image file in a workbook.</span></span>
    
  
- <span data-ttu-id="2fda1-113">**GetPublishedItemNames** Gets a list of published items in a workbook.</span><span class="sxs-lookup"><span data-stu-id="2fda1-113">**GetPublishedItemNames** Gets a list of published items in a workbook.</span></span>
    
  
- <span data-ttu-id="2fda1-114">**GetSheetNames** Gets a list of all of the sheet names present in a workbook.</span><span class="sxs-lookup"><span data-stu-id="2fda1-114">**GetSheetNames** Gets a list of all of the sheet names present in a workbook.</span></span>
    
  
- <span data-ttu-id="2fda1-115">**OpenWorkbookForEditing** Opens a workbook for editing.</span><span class="sxs-lookup"><span data-stu-id="2fda1-115">**OpenWorkbookForEditing** Opens a workbook for editing.</span></span>
    
  
- <span data-ttu-id="2fda1-116">**SaveWorkbook** Saves a workbook in the original format (.xlsx, .xlsb, .xlsm).</span><span class="sxs-lookup"><span data-stu-id="2fda1-116">**SaveWorkbook** Saves a workbook in the original format (.xlsx, .xlsb, .xlsm).</span></span>
    
  
- <span data-ttu-id="2fda1-117">**SaveWorkbookCopy** Saves a workbook by using a different file name and/or saves a workbook to a different SharePoint document library.</span><span class="sxs-lookup"><span data-stu-id="2fda1-117">**SaveWorkbookCopy** Saves a workbook by using a different file name and/or saves a workbook to a different SharePoint document library.</span></span>
    
  
- <span data-ttu-id="2fda1-118">**SetCalculationOptions** Changes the calculation mode setting for workbooks.</span><span class="sxs-lookup"><span data-stu-id="2fda1-118">**SetCalculationOptions** Changes the calculation mode setting for workbooks.</span></span>
    
  
- <span data-ttu-id="2fda1-119">**SetParameters** Sets multiple published parameters with a single Web Service call.</span><span class="sxs-lookup"><span data-stu-id="2fda1-119">**SetParameters** Sets multiple published parameters with a single Web Service call.</span></span>
    
  
<span data-ttu-id="2fda1-120">Weitere Schritte:</span><span class="sxs-lookup"><span data-stu-id="2fda1-120">In addition:</span></span>
  
    
    

- <span data-ttu-id="2fda1-121">You can now set formulas by using the set value methods.</span><span class="sxs-lookup"><span data-stu-id="2fda1-121">You can now set formulas by using the set value methods.</span></span>
    
  
- <span data-ttu-id="2fda1-122">Dynamic ranges are supported in Excel Web Services in SharePoint Server 2010.</span><span class="sxs-lookup"><span data-stu-id="2fda1-122">Dynamic ranges are supported in Excel Web Services in SharePoint Server 2010.</span></span>
    
  

### <a name="new-enumerations"></a><span data-ttu-id="2fda1-123">New Enumerations</span><span class="sxs-lookup"><span data-stu-id="2fda1-123">New Enumerations</span></span>

<span data-ttu-id="2fda1-124">The following are new enumerations added to Excel Web Services, in alphabetical order:</span><span class="sxs-lookup"><span data-stu-id="2fda1-124">The following are new enumerations added to Excel Web Services, in alphabetical order:</span></span>
  
    
    

- <span data-ttu-id="2fda1-125">**ItemType** Indicates the types of the returned items.</span><span class="sxs-lookup"><span data-stu-id="2fda1-125">**ItemType** Indicates the types of the returned items.</span></span>
    
  
- <span data-ttu-id="2fda1-126">**SheetType** Indicates the types of the returned sheets.</span><span class="sxs-lookup"><span data-stu-id="2fda1-126">**SheetType** Indicates the types of the returned sheets.</span></span>
    
  
- <span data-ttu-id="2fda1-127">**SheetVisibility** Indicates whether the returned sheets are visible.</span><span class="sxs-lookup"><span data-stu-id="2fda1-127">**SheetVisibility** Indicates whether the returned sheets are visible.</span></span>
    
  
- <span data-ttu-id="2fda1-128">**SaveOptions** Specifies whether to overwrite an existing, unlocked file.</span><span class="sxs-lookup"><span data-stu-id="2fda1-128">**SaveOptions** Specifies whether to overwrite an existing, unlocked file.</span></span>
    
  
- <span data-ttu-id="2fda1-129">**WorkbookCalculation** Defines the calculation mode setting for a workbook.</span><span class="sxs-lookup"><span data-stu-id="2fda1-129">**WorkbookCalculation** Defines the calculation mode setting for a workbook.</span></span>
    
  

### <a name="new-types"></a><span data-ttu-id="2fda1-130">New Types</span><span class="sxs-lookup"><span data-stu-id="2fda1-130">New Types</span></span>

<span data-ttu-id="2fda1-131">The following are new types added to Excel Web Services, in alphabetical order:</span><span class="sxs-lookup"><span data-stu-id="2fda1-131">The following are new types added to Excel Web Services, in alphabetical order:</span></span>
  
    
    

- <span data-ttu-id="2fda1-132">**ParameterInfo** Gets or sets the name and values of a parameter.</span><span class="sxs-lookup"><span data-stu-id="2fda1-132">**ParameterInfo** Gets or sets the name and values of a parameter.</span></span>
    
  
- <span data-ttu-id="2fda1-133">**SheetInfo** Contains information about a sheet in a workbook.</span><span class="sxs-lookup"><span data-stu-id="2fda1-133">**SheetInfo** Contains information about a sheet in a workbook.</span></span>
    
  
- <span data-ttu-id="2fda1-134">**Size** Defines the width and height of the chart image</span><span class="sxs-lookup"><span data-stu-id="2fda1-134">**Size** Defines the width and height of the chart image</span></span>
    
  
- <span data-ttu-id="2fda1-135">**WorkbookItem** Represents named items in the workbook.</span><span class="sxs-lookup"><span data-stu-id="2fda1-135">**WorkbookItem** Represents named items in the workbook.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="2fda1-136">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="2fda1-136">See also</span></span>


#### <a name="other-resources"></a><span data-ttu-id="2fda1-137">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="2fda1-137">Other resources</span></span>


  
    
    
 [<span data-ttu-id="2fda1-138">Walkthrough: Developing a Custom Application Using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="2fda1-138">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services)
