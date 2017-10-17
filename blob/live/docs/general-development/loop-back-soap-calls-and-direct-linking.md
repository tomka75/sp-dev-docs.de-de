---
title: "Zurückschleifen von SOAP-Aufrufen und Direct Linking"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: bffc6565-636f-40d4-ba17-2511070ba5db
ms.openlocfilehash: 618715458b7906ee96a1d9bfd26502d3c6f6a622
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="loop-back-soap-calls-and-direct-linking"></a><span data-ttu-id="34cac-102">Zurückschleifen von SOAP-Aufrufen und Direct Linking</span><span class="sxs-lookup"><span data-stu-id="34cac-102">Loop-Back SOAP Calls and Direct Linking</span></span>

<span data-ttu-id="34cac-p101">If you are writing code within Microsoft SharePoint Foundation, for example, a custom Web Part, custom aspx page, and so on, you should make direct calls to Microsoft.Office.Excel.Server.WebServices.dll. You do this by linking directly to Microsoft.Office.Excel.Server.WebServices.dll.</span><span class="sxs-lookup"><span data-stu-id="34cac-p101">If you are writing code within Microsoft SharePoint Foundation, for example, a custom Web Part, custom aspx page, and so on, you should make direct calls to Microsoft.Office.Excel.Server.WebServices.dll. You do this by linking directly to Microsoft.Office.Excel.Server.WebServices.dll.</span></span> 
  
    
    

<span data-ttu-id="34cac-p102">Using Simple Object Access Protocol (SOAP) from a Web server to communicate with the same Web server is also known as using loop-back SOAP calls. It is strongly recommended that you do not attempt to use loop-back SOAP calls. If you are writing code within SharePoint Foundation, you should not use SOAP to call the Excel Web Services. You should instead link to Microsoft.Office.Excel.Server.WebServices.dll locally and make calls to it as you would any local assembly.</span><span class="sxs-lookup"><span data-stu-id="34cac-p102">Using Simple Object Access Protocol (SOAP) from a Web server to communicate with the same Web server is also known as using loop-back SOAP calls. It is strongly recommended that you do not attempt to use loop-back SOAP calls. If you are writing code within SharePoint Foundation, you should not use SOAP to call the Excel Web Services. You should instead link to Microsoft.Office.Excel.Server.WebServices.dll locally and make calls to it as you would any local assembly.</span></span>
## <a name="location-of-microsoftofficeexcelserverwebservicesdll"></a><span data-ttu-id="34cac-109">Location of Microsoft.Office.Excel.Server.WebServices.dll</span><span class="sxs-lookup"><span data-stu-id="34cac-109">Location of Microsoft.Office.Excel.Server.WebServices.dll</span></span>

<span data-ttu-id="34cac-110">You can find Microsoft.Office.Excel.Server.WebServices.dll in one of the following locations:</span><span class="sxs-lookup"><span data-stu-id="34cac-110">You can find Microsoft.Office.Excel.Server.WebServices.dll in one of the following locations:</span></span>
  
    
    

-  <span data-ttu-id="34cac-111">_[drive:]_\\Program Files\\Common Files\\Microsoft Shared\\web server extensions\\14\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="34cac-111">_[drive:]_\\Program Files\\Common Files\\Microsoft Shared\\web server extensions\\14\\ISAPI</span></span>
    
  
- <span data-ttu-id="34cac-112">Global assembly cache</span><span class="sxs-lookup"><span data-stu-id="34cac-112">Global assembly cache</span></span> 
    
  

## <a name="adding-a-reference-to-microsoftofficeexcelserverwebservicesdll"></a><span data-ttu-id="34cac-113">Adding a Reference to Microsoft.Office.Excel.Server.WebServices.dll</span><span class="sxs-lookup"><span data-stu-id="34cac-113">Adding a Reference to Microsoft.Office.Excel.Server.WebServices.dll</span></span>

<span data-ttu-id="34cac-p103">To link directly to Microsoft.Office.Excel.Server.WebServices.dll in your project and call it from your code, you add a reference to it. On the computer where you have installed Microsoft SharePoint Server 2010, using the **Add Reference** dialog box in Microsoft Visual Studio, you can do one of the following:</span><span class="sxs-lookup"><span data-stu-id="34cac-p103">To link directly to Microsoft.Office.Excel.Server.WebServices.dll in your project and call it from your code, you add a reference to it. On the computer where you have installed Microsoft SharePoint Server 2010, using the **Add Reference** dialog box in Microsoft Visual Studio, you can do one of the following:</span></span>
  
    
    

- <span data-ttu-id="34cac-116">Select **Excel Web Services** from the **Component Name** list in the **.NET** tab.</span><span class="sxs-lookup"><span data-stu-id="34cac-116">Select **Excel Web Services** from the **Component Name** list in the **.NET** tab.</span></span>
    
  
- <span data-ttu-id="34cac-117">Browse to Microsoft.Office.Excel.Server.WebServices.dll located in:</span><span class="sxs-lookup"><span data-stu-id="34cac-117">Browse to Microsoft.Office.Excel.Server.WebServices.dll located in:</span></span>
  
    
    
 <span data-ttu-id="34cac-118">_[drive:]_\\Program Files\\Common Files\\Microsoft Shared\\web server extensions\\14\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="34cac-118">_[drive:]_\\Program Files\\Common Files\\Microsoft Shared\\web server extensions\\14\\ISAPI</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="34cac-119">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="34cac-119">See also</span></span>


#### <a name="concepts"></a><span data-ttu-id="34cac-120">Konzepte</span><span class="sxs-lookup"><span data-stu-id="34cac-120">Concepts</span></span>


  
    
    
 [<span data-ttu-id="34cac-121">Accessing the SOAP API</span><span class="sxs-lookup"><span data-stu-id="34cac-121">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
  
    
    
 [<span data-ttu-id="34cac-122">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="34cac-122">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
  
    
    
 [<span data-ttu-id="34cac-123">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="34cac-123">Excel Services Alerts</span></span>](excel-services-alerts.md)
#### <a name="other-resources"></a><span data-ttu-id="34cac-124">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="34cac-124">Other resources</span></span>


  
    
    
 [<span data-ttu-id="34cac-125">Walkthrough: Developing a Custom Application Using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="34cac-125">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
