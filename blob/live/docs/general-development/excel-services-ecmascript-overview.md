---
title: "Übersicht über Excel Services-ECMAScript"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f8c1be86-df19-44c3-a3bc-c0da2b80df10
ms.openlocfilehash: 542923e7b37ccdc63d86dcc0cf546879ffddc119
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="excel-services-ecmascript-overview"></a><span data-ttu-id="5dcd8-102">Übersicht über Excel Services-ECMAScript</span><span class="sxs-lookup"><span data-stu-id="5dcd8-102">Excel Services ECMAScript Overview</span></span>

<span data-ttu-id="5dcd8-p101">In Microsoft SharePoint Server 2010, Excel Services added support for ECMAScript (JavaScript, JScript). JavaScript enables a new set of solutions by using Excel Services.</span><span class="sxs-lookup"><span data-stu-id="5dcd8-p101">In Microsoft SharePoint Server 2010, Excel Services added support for ECMAScript (JavaScript, JScript). JavaScript enables a new set of solutions by using Excel Services.</span></span> 
  
    
    

<span data-ttu-id="5dcd8-p102">The JavaScript object model in Excel Services enables developers to automate, customize, and interact with the Excel Web Access Web Part control on a page. By using the JavaScript object model, you can build mashups and other integrated solutions that interact with one or more Excel Web Access Web Part controls on a page. It also enables you to add more capabilities to your workbooks and to code around them. By using the JavaScript object model, it is possible to detect and react to a user's interactions with an Excel Web Access Web Part and to programmatically interact with one or multiple Excel Web Access Web Parts.</span><span class="sxs-lookup"><span data-stu-id="5dcd8-p102">The JavaScript object model in Excel Services enables developers to automate, customize, and interact with the Excel Web Access Web Part control on a page. By using the JavaScript object model, you can build mashups and other integrated solutions that interact with one or more Excel Web Access Web Part controls on a page. It also enables you to add more capabilities to your workbooks and to code around them. By using the JavaScript object model, it is possible to detect and react to a user's interactions with an Excel Web Access Web Part and to programmatically interact with one or multiple Excel Web Access Web Parts.</span></span>
  
    
    


## <a name="using-the-ecmascript-object-model"></a><span data-ttu-id="5dcd8-109">Using the ECMAScript Object Model</span><span class="sxs-lookup"><span data-stu-id="5dcd8-109">Using the ECMAScript Object Model</span></span>

<span data-ttu-id="5dcd8-p103">To use the JavaScript object model in Excel Services, you insert the JavaScript code on the page that contains the Excel Web Access Web Part. This can be done by adding the code to the Web Part page by using the Content Editor Web Part or by directly editing the .aspx page.</span><span class="sxs-lookup"><span data-stu-id="5dcd8-p103">To use the JavaScript object model in Excel Services, you insert the JavaScript code on the page that contains the Excel Web Access Web Part. This can be done by adding the code to the Web Part page by using the Content Editor Web Part or by directly editing the .aspx page.</span></span>
  
    
    
<span data-ttu-id="5dcd8-112">The JavaScript object model in Excel Services enables developers to:</span><span class="sxs-lookup"><span data-stu-id="5dcd8-112">The JavaScript object model in Excel Services enables developers to:</span></span> 
  
    
    

- <span data-ttu-id="5dcd8-113">Access items in a workbook such as ranges, tables, PivotTables, charts, and sheets.</span><span class="sxs-lookup"><span data-stu-id="5dcd8-113">Access items in a workbook such as ranges, tables, PivotTables, charts, and sheets.</span></span>
    
  
- <span data-ttu-id="5dcd8-114">Set and retrieve values from cells by using ranges or named ranges.</span><span class="sxs-lookup"><span data-stu-id="5dcd8-114">Set and retrieve values from cells by using ranges or named ranges.</span></span>
    
  
- <span data-ttu-id="5dcd8-115">Raise events when the user changes the active selection or active cell or when the user starts editing a cell.</span><span class="sxs-lookup"><span data-stu-id="5dcd8-115">Raise events when the user changes the active selection or active cell or when the user starts editing a cell.</span></span>
    
  
- <span data-ttu-id="5dcd8-116">Scroll to a different region and to switch the displayed sheet or named item.</span><span class="sxs-lookup"><span data-stu-id="5dcd8-116">Scroll to a different region and to switch the displayed sheet or named item.</span></span> 
    
  
<span data-ttu-id="5dcd8-117">Weitere Informationen hierzu finden Sie unter folgenden Links:</span><span class="sxs-lookup"><span data-stu-id="5dcd8-117">For more information, see the following links:</span></span>
  
    
    

- <span data-ttu-id="5dcd8-118">For more information about the JavaScript object model in Excel Services, see the  [Ewa](http://msdn.microsoft.com/library/6fe73191-3213-b986-1ad6-2c3b918a2241%28Office.15%29.aspx) namespace reference documentation.</span><span class="sxs-lookup"><span data-stu-id="5dcd8-118">For more information about the JavaScript object model in Excel Services, see the  [Ewa](http://msdn.microsoft.com/library/6fe73191-3213-b986-1ad6-2c3b918a2241%28Office.15%29.aspx) namespace reference documentation.</span></span>
    
  
- <span data-ttu-id="5dcd8-119">For an example of how to interact with the JavaScript object model in Excel Services by using the Content Editor Web Part, see  [Walkthrough: Developing Using the Content Editor Web Part](walkthrough-developing-using-the-content-editor-web-part.md).</span><span class="sxs-lookup"><span data-stu-id="5dcd8-119">For an example of how to interact with the JavaScript object model in Excel Services by using the Content Editor Web Part, see  [Walkthrough: Developing Using the Content Editor Web Part](walkthrough-developing-using-the-content-editor-web-part.md).</span></span>
    
  

## <a name="ecmascript-js-file-location"></a><span data-ttu-id="5dcd8-120">ECMAScript .js File Location</span><span class="sxs-lookup"><span data-stu-id="5dcd8-120">ECMAScript .js File Location</span></span>

<span data-ttu-id="5dcd8-p104">Minified .js files for the JavaScript object model are installed in the %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS directory. The name of the file is EwaMoss.js.</span><span class="sxs-lookup"><span data-stu-id="5dcd8-p104">Minified .js files for the JavaScript object model are installed in the %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS directory. The name of the file is EwaMoss.js.</span></span>
  
    
    
<span data-ttu-id="5dcd8-123">For basic information about how to use the JavaScript object model within an .aspx page or .js file, see  [Einrichten einer Anwendungsseite für ECMAScript](http://msdn.microsoft.com/library/48582a0b-f787-4868-8298-958717ec8ff8%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="5dcd8-123">For basic information about how to use the JavaScript object model within an .aspx page or .js file, see  [Setting Up an Application Page for JavaScript](http://msdn.microsoft.com/library/48582a0b-f787-4868-8298-958717ec8ff8%28Office.15%29.aspx).</span></span>
  
    
    
