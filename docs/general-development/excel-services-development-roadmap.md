---
title: Excel Services-Entwicklungsroadmap
ms.date: 09/25/2017
keywords: roadmap
f1_keywords: roadmap
ms.prod: sharepoint
ms.assetid: 5c789f58-9cdb-4601-9047-9c6f83f2fbba
ms.openlocfilehash: fdd3793c25280dd5dd0ae6de26eb7c731048d8fa
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="excel-services-development-roadmap"></a><span data-ttu-id="c0478-103">Excel Services-Entwicklungsroadmap</span><span class="sxs-lookup"><span data-stu-id="c0478-103">Excel Services Development Roadmap</span></span>

<span data-ttu-id="c0478-p101">An important aspect of Excel Services is that solution developers can use its power programmatically from their applications. These applications can be line-of-business (LOB) products or custom enterprise solutions that an organization develops internally.</span><span class="sxs-lookup"><span data-stu-id="c0478-p101">An important aspect of Excel Services is that solution developers can use its power programmatically from their applications. These applications can be line-of-business (LOB) products or custom enterprise solutions that an organization develops internally.</span></span> 
  
    
    

<span data-ttu-id="c0478-106">Following are examples of these applications:</span><span class="sxs-lookup"><span data-stu-id="c0478-106">Following are examples of these applications:</span></span> 
- <span data-ttu-id="c0478-107">Multitiered applications, with the presentation layer implemented as a Web application (for example, an ASP.NET application) that calls Excel Web Services.</span><span class="sxs-lookup"><span data-stu-id="c0478-107">Multitiered applications, with the presentation layer implemented as a Web application (for example, an ASP.NET application) that calls Excel Web Services.</span></span>
    
  
- <span data-ttu-id="c0478-108">Applications within Microsoft SharePoint Server 2010, or integrated with LOB products.</span><span class="sxs-lookup"><span data-stu-id="c0478-108">Applications within Microsoft SharePoint Server 2010, or integrated with LOB products.</span></span>
    
  
<span data-ttu-id="c0478-109">There are five types of development that you can do by using Excel Services:</span><span class="sxs-lookup"><span data-stu-id="c0478-109">There are five types of development that you can do by using Excel Services:</span></span>
- <span data-ttu-id="c0478-110">Develop solutions by using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="c0478-110">Develop solutions by using Excel Web Services</span></span>
    
  
- <span data-ttu-id="c0478-111">Extend the Microsoft Excel function library in Excel Services by using user-defined functions (UDFs)</span><span class="sxs-lookup"><span data-stu-id="c0478-111">Extend the Microsoft Excel function library in Excel Services by using user-defined functions (UDFs)</span></span> 
    
  
- <span data-ttu-id="c0478-112">Customize the Excel Web Access Web Part</span><span class="sxs-lookup"><span data-stu-id="c0478-112">Customize the Excel Web Access Web Part</span></span>
    
  
- <span data-ttu-id="c0478-113">Develop solutions by using ECMAScript (JavaScript, JScript)</span><span class="sxs-lookup"><span data-stu-id="c0478-113">Develop solutions by using ECMAScript (JavaScript, JScript)</span></span>
    
  
- <span data-ttu-id="c0478-114">Use the REST API to perform operations against Excel workbooks</span><span class="sxs-lookup"><span data-stu-id="c0478-114">Use the REST API to perform operations against Excel workbooks</span></span>
    
  

## <a name="excel-web-service"></a><span data-ttu-id="c0478-115">Excel Web Service</span><span class="sxs-lookup"><span data-stu-id="c0478-115">Excel Web Service</span></span>

<span data-ttu-id="c0478-116">Following are the main scenarios for Excel Web Services:</span><span class="sxs-lookup"><span data-stu-id="c0478-116">Following are the main scenarios for Excel Web Services:</span></span>
  
    
    

- <span data-ttu-id="c0478-117">**Server-side Excel calculation**</span><span class="sxs-lookup"><span data-stu-id="c0478-117">**Server-side Excel calculation**</span></span>
    
    <span data-ttu-id="c0478-p102">This scenario is application-centric. In this scenario, you use models defined in Excel workbooks and calculated on the server as part of application logic.</span><span class="sxs-lookup"><span data-stu-id="c0478-p102">This scenario is application-centric. In this scenario, you use models defined in Excel workbooks and calculated on the server as part of application logic.</span></span>
    
  
- <span data-ttu-id="c0478-120">**Automating workbook updates on the server**</span><span class="sxs-lookup"><span data-stu-id="c0478-120">**Automating workbook updates on the server**</span></span>
    
    <span data-ttu-id="c0478-p103">This scenario is file-centric. In this scenario, Excel Web Services processes a workbook, and saves copies of the workbook or snapshots.</span><span class="sxs-lookup"><span data-stu-id="c0478-p103">This scenario is file-centric. In this scenario, Excel Web Services processes a workbook, and saves copies of the workbook or snapshots.</span></span>
    
  
- <span data-ttu-id="c0478-123">**Opening workbooks in edit sessions**</span><span class="sxs-lookup"><span data-stu-id="c0478-123">**Opening workbooks in edit sessions**</span></span>
    
    <span data-ttu-id="c0478-p104">Excel Web Services supports opening workbooks in edit sessions in SharePoint Server 2010. In this scenario, you can use code to edit a workbook.</span><span class="sxs-lookup"><span data-stu-id="c0478-p104">Excel Web Services supports opening workbooks in edit sessions in SharePoint Server 2010. In this scenario, you can use code to edit a workbook.</span></span>
    
  

### <a name="server-side-excel-calculation"></a><span data-ttu-id="c0478-126">Server-Side Excel Calculation</span><span class="sxs-lookup"><span data-stu-id="c0478-126">Server-Side Excel Calculation</span></span>

<span data-ttu-id="c0478-p105">For server-side Excel calculation, a custom application typically uses an Excel model as part of its logic. Instead of having to re-code Excel workbook business logic in a programming language, the business user can maintain the model in Excel in a server location. The developer never needs to change a line of code in the application that uses the model created by the business user.</span><span class="sxs-lookup"><span data-stu-id="c0478-p105">For server-side Excel calculation, a custom application typically uses an Excel model as part of its logic. Instead of having to re-code Excel workbook business logic in a programming language, the business user can maintain the model in Excel in a server location. The developer never needs to change a line of code in the application that uses the model created by the business user.</span></span>
  
    
    
<span data-ttu-id="c0478-p106">In this scenario, the custom application repeatedly calls Excel Web Services, which sends the calls to a back-end calculation service. Dienste für Excel-Berechnungen does the following:</span><span class="sxs-lookup"><span data-stu-id="c0478-p106">In this scenario, the custom application repeatedly calls Excel Web Services, which sends the calls to a back-end calculation service. Excel Calculation Services does the following:</span></span>
  
    
    

- <span data-ttu-id="c0478-132">Loads the specified Excel workbook</span><span class="sxs-lookup"><span data-stu-id="c0478-132">Loads the specified Excel workbook</span></span> 
    
  
- <span data-ttu-id="c0478-133">Receives inputs</span><span class="sxs-lookup"><span data-stu-id="c0478-133">Receives inputs</span></span>
    
  
- <span data-ttu-id="c0478-134">Processes the workbook (for example, refreshes data or performs calculations)</span><span class="sxs-lookup"><span data-stu-id="c0478-134">Processes the workbook (for example, refreshes data or performs calculations)</span></span>
    
  
- <span data-ttu-id="c0478-135">Sends the results to the custom application</span><span class="sxs-lookup"><span data-stu-id="c0478-135">Sends the results to the custom application</span></span>
    
  

### <a name="automating-workbook-updates-on-the-server"></a><span data-ttu-id="c0478-136">Automating Workbook Updates on the Server</span><span class="sxs-lookup"><span data-stu-id="c0478-136">Automating Workbook Updates on the Server</span></span>

<span data-ttu-id="c0478-137">When developers automate the updating of Excel workbooks on the server, they often have two objectives:</span><span class="sxs-lookup"><span data-stu-id="c0478-137">When developers automate the updating of Excel workbooks on the server, they often have two objectives:</span></span>
  
    
    

- <span data-ttu-id="c0478-138">Generate Excel files or modify Excel templates by using the Open XML-Dateiformate, and then calculate the generated Excel file.</span><span class="sxs-lookup"><span data-stu-id="c0478-138">Generate Excel files or modify Excel templates by using the Open XML File Formats, and then calculate the generated Excel file.</span></span>
    
  
- <span data-ttu-id="c0478-139">Periodically open an Excel file to refresh external data (once, or maybe multiple times per user), and then calculate the resulting workbooks and save them or send them in e-mail messages to various users.</span><span class="sxs-lookup"><span data-stu-id="c0478-139">Periodically open an Excel file to refresh external data (once, or maybe multiple times per user), and then calculate the resulting workbooks and save them or send them in e-mail messages to various users.</span></span>
    
  
<span data-ttu-id="c0478-140">In this scenario, a custom application uses Excel Web Services to do the following:</span><span class="sxs-lookup"><span data-stu-id="c0478-140">In this scenario, a custom application uses Excel Web Services to do the following:</span></span>
  
    
    

- <span data-ttu-id="c0478-141">Load the specified Excel workbook</span><span class="sxs-lookup"><span data-stu-id="c0478-141">Load the specified Excel workbook</span></span> 
    
  
- <span data-ttu-id="c0478-142">Input parameters</span><span class="sxs-lookup"><span data-stu-id="c0478-142">Input parameters</span></span>
    
  
- <span data-ttu-id="c0478-143">Process the workbook (for example, refresh data or perform calculations)</span><span class="sxs-lookup"><span data-stu-id="c0478-143">Process the workbook (for example, refresh data or perform calculations)</span></span> 
    
  
<span data-ttu-id="c0478-144">The custom application retrieves the live version of the workbook or snapshot and then saves the workbook or snapshot by using Excel Web Services.</span><span class="sxs-lookup"><span data-stu-id="c0478-144">The custom application retrieves the live version of the workbook or snapshot and then saves the workbook or snapshot by using Excel Web Services.</span></span>
  
> [!NOTE]
> <span data-ttu-id="c0478-145">Wenn Sie Änderungen an einer Arbeitsmappe vornehmen, z. B. durch Festlegen von Werten für einen Bereich mithilfe von Excel Web Services, bleiben die Änderungen an der Arbeitsmappe nur für diese bestimmte Sitzung erhalten.</span><span class="sxs-lookup"><span data-stu-id="c0478-145">Note: When you make changes to a workbook—for example, by setting values to a range by using Excel Web Services—the changes to the workbook are preserved only for that particular session.</span></span> <span data-ttu-id="c0478-146">Die Änderungen werden nicht in der ursprünglichen Arbeitsmappe gespeichert oder persistent gemacht.</span><span class="sxs-lookup"><span data-stu-id="c0478-146">The changes are not saved or persisted back to the original workbook.</span></span> <span data-ttu-id="c0478-147">Wenn die aktuelle Arbeitsmappensitzung endet (z. B. beim Aufruf der Methode **CloseWorkbook** oder bei einem Sitzungstimeout), gehen die vorgenommenen Änderungen verloren. Wenn Sie Änderungen speichern möchten, die Sie an einer Arbeitsmappe vornehmen, können Sie die Methode **GetWorkbook** verwenden und die Arbeitsmappe dann mithilfe der Methode **SaveWorkbook** oder **SaveWorkbookCopy** speichern.</span><span class="sxs-lookup"><span data-stu-id="c0478-147">When the current workbook session ends (for example, when you call the **CloseWorkbook** method, or when the session times out), changes that you made are lost.> If you want to save changes that you make to a workbook, you can use the **GetWorkbook** method and then save the workbook by using the **SaveWorkbook** method or the **SaveWorkbookCopy** method.</span></span> <span data-ttu-id="c0478-148">Weitere Informationen zur Excel Web Services-API finden Sie unter [Microsoft.Office.Excel.Server.WebServices](((https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.Webservices.aspx))) .</span><span class="sxs-lookup"><span data-stu-id="c0478-148">For more information about the Excel Web Services API, see [Microsoft.Office.Excel.Server.WebServices](((https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.Webservices.aspx))) .</span></span>
  
    
    


### <a name="using-excel-web-services"></a><span data-ttu-id="c0478-149">Verwenden von Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="c0478-149">Using Excel Web Services</span></span>

<span data-ttu-id="c0478-150">You can use Excel Web Services as:</span><span class="sxs-lookup"><span data-stu-id="c0478-150">You can use Excel Web Services as:</span></span>
  
    
    

- <span data-ttu-id="c0478-151">A regular Web service, by calling the Web methods through SOAP over HTTP.</span><span class="sxs-lookup"><span data-stu-id="c0478-151">A regular Web service, by calling the Web methods through SOAP over HTTP.</span></span>
    
  
- <span data-ttu-id="c0478-152">A local assembly, by linking directly to **Microsoft.Office.Excel.Server.Webservices.dll**.</span><span class="sxs-lookup"><span data-stu-id="c0478-152">A local assembly, by linking directly to **Microsoft.Office.Excel.Server.Webservices.dll**.</span></span>
    
  
<span data-ttu-id="c0478-153">For more information about when you should link directly to **Microsoft.Office.Excel.Server.Webservices.dll**, see  [Loop-Back SOAP Calls and Direct Linking](loop-back-soap-calls-and-direct-linking.md).</span><span class="sxs-lookup"><span data-stu-id="c0478-153">For more information about when you should link directly to **Microsoft.Office.Excel.Server.Webservices.dll**, see  [Loop-Back SOAP Calls and Direct Linking](loop-back-soap-calls-and-direct-linking.md).</span></span> 
  
    
    
<span data-ttu-id="c0478-p108">For information about the Excel Web Services API, see the  [Microsoft.Office.Excel.Server.Webservices](((https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.Webservices.aspx))) namespace reference documentation. For an example of how to develop a custom application by using Excel Web Services, see [Walkthrough: Developing a Custom Application Using Excel Web Services](walkthrough-developing-a-custom-application-using-excel-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="c0478-p108">For information about the Excel Web Services API, see the  [Microsoft.Office.Excel.Server.Webservices](((https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.Webservices.aspx))) namespace reference documentation. For an example of how to develop a custom application by using Excel Web Services, see [Walkthrough: Developing a Custom Application Using Excel Web Services](walkthrough-developing-a-custom-application-using-excel-web-services.md).</span></span>
  
    
    

## <a name="user-defined-functions-udfs"></a><span data-ttu-id="c0478-156">User-Defined Functions (UDFs)</span><span class="sxs-lookup"><span data-stu-id="c0478-156">User-Defined Functions (UDFs)</span></span>

<span data-ttu-id="c0478-p109">Excel Services supports managed-code UDFs. Excel Services UDFs give you the ability to use formulas in cells to call custom functions written in managed code and deployed to SharePoint Server 2010. You can create UDFs to:</span><span class="sxs-lookup"><span data-stu-id="c0478-p109">Excel Services supports managed-code UDFs. Excel Services UDFs give you the ability to use formulas in cells to call custom functions written in managed code and deployed to SharePoint Server 2010. You can create UDFs to:</span></span>
  
    
    

- <span data-ttu-id="c0478-160">Call custom mathematical functions.</span><span class="sxs-lookup"><span data-stu-id="c0478-160">Call custom mathematical functions.</span></span>
    
  
- <span data-ttu-id="c0478-161">Get data from custom data sources into worksheets.</span><span class="sxs-lookup"><span data-stu-id="c0478-161">Get data from custom data sources into worksheets.</span></span>
    
  
- <span data-ttu-id="c0478-162">Call Web services from the UDFs.</span><span class="sxs-lookup"><span data-stu-id="c0478-162">Call Web services from the UDFs.</span></span>
    
  
- <span data-ttu-id="c0478-163">Wrap calls to existing native code library functionsfor example, existing Excel UDFs.</span><span class="sxs-lookup"><span data-stu-id="c0478-163">Wrap calls to existing native code library functions—for example, existing Excel UDFs.</span></span>
    
  
<span data-ttu-id="c0478-164">For more information about Excel Services UDFs, see  [Understanding Excel Services UDFs](understanding-excel-services-udfs.md).</span><span class="sxs-lookup"><span data-stu-id="c0478-164">For more information about Excel Services UDFs, see  [Understanding Excel Services UDFs](understanding-excel-services-udfs.md).</span></span> 
  
    
    

### <a name="using-udfs"></a><span data-ttu-id="c0478-165">Using UDFs</span><span class="sxs-lookup"><span data-stu-id="c0478-165">Using UDFs</span></span>

<span data-ttu-id="c0478-166">For information about Excel Services UDF definitions, see the  [Microsoft.Office.Excel.Server.Udf](https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.Udf.aspx) namespace reference documentation.</span><span class="sxs-lookup"><span data-stu-id="c0478-166">For information about Excel Services UDF definitions, see the  [Microsoft.Office.Excel.Server.Udf](https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.Udf.aspx) namespace reference documentation.</span></span>
  
    
    
<span data-ttu-id="c0478-167">For an example of how to create managed-code UDFs, see  [Walkthrough: Developing a Managed-Code UDF](walkthrough-developing-a-managed-code-udf.md).</span><span class="sxs-lookup"><span data-stu-id="c0478-167">For an example of how to create managed-code UDFs, see  [Walkthrough: Developing a Managed-Code UDF](walkthrough-developing-a-managed-code-udf.md).</span></span>
  
    
    

## <a name="excel-web-access"></a><span data-ttu-id="c0478-168">Excel Web Access</span><span class="sxs-lookup"><span data-stu-id="c0478-168">Excel Web Access</span></span>

<span data-ttu-id="c0478-169">You can use the extensible properties of the Excel Web Access Web Part to:</span><span class="sxs-lookup"><span data-stu-id="c0478-169">You can use the extensible properties of the Excel Web Access Web Part to:</span></span>
  
    
    

- <span data-ttu-id="c0478-170">Configure Excel Web Access programmatically.</span><span class="sxs-lookup"><span data-stu-id="c0478-170">Configure Excel Web Access programmatically.</span></span>
    
  
- <span data-ttu-id="c0478-171">Change Excel Web Access properties programmatically.</span><span class="sxs-lookup"><span data-stu-id="c0478-171">Change Excel Web Access properties programmatically.</span></span>
    
  
- <span data-ttu-id="c0478-172">Apply a theme or brand a Web Part page by using cascading style sheets (CSS).</span><span class="sxs-lookup"><span data-stu-id="c0478-172">Apply a theme or brand a Web Part page by using cascading style sheets (CSS).</span></span>
    
  

### <a name="using-excel-web-access-web-part-extensibility"></a><span data-ttu-id="c0478-173">Using Excel Web Access Web Part Extensibility</span><span class="sxs-lookup"><span data-stu-id="c0478-173">Using Excel Web Access Web Part Extensibility</span></span>

<span data-ttu-id="c0478-174">Informationen über:</span><span class="sxs-lookup"><span data-stu-id="c0478-174">For information about:</span></span>
  
    
    

- <span data-ttu-id="c0478-175">Erweiterbare Excel Web Access-Eigenschaften finden Sie in der Referenzdokumentation zum Namespace **Microsoft.Office.Excel.Server.WebUI**.</span><span class="sxs-lookup"><span data-stu-id="c0478-175">Excel Web Access extensible properties, see the **Microsoft.Office.Excel.Server.WebUI** namespace reference documentation.</span></span>
    
  
- <span data-ttu-id="c0478-176">Excel Web Access-CSS finden Sie in der Referenzdokumentation zu CSS.</span><span class="sxs-lookup"><span data-stu-id="c0478-176">Excel Web Access CSS, see the CSS reference documentation.</span></span>
    
  
- <span data-ttu-id="c0478-177">How to programmatically configure a Web Part, see the SharePoint Foundation SDK.</span><span class="sxs-lookup"><span data-stu-id="c0478-177">How to programmatically configure a Web Part, see the SharePoint Foundation SDK.</span></span> 
    
  

## <a name="ecmascript-javascript-jscript"></a><span data-ttu-id="c0478-178">ECMAScript (JavaScript, JScript)</span><span class="sxs-lookup"><span data-stu-id="c0478-178">ECMAScript (JavaScript, JScript)</span></span>

<span data-ttu-id="c0478-p110">In SharePoint Server 2010, Excel Services added support for JavaScript. The JavaScript object model in Excel Services enables developers to automate, customize, and interact with the Excel Web Access Web Part control on a page. By using the JavaScript object model, you can build mashups and other integrated solutions that interact with one or more Excel Web Access Web Part controls on a page. It also enables you to add more capabilities to your workbooks and code around them.</span><span class="sxs-lookup"><span data-stu-id="c0478-p110">In SharePoint Server 2010, Excel Services added support for JavaScript. The JavaScript object model in Excel Services enables developers to automate, customize, and interact with the Excel Web Access Web Part control on a page. By using the JavaScript object model, you can build mashups and other integrated solutions that interact with one or more Excel Web Access Web Part controls on a page. It also enables you to add more capabilities to your workbooks and code around them.</span></span>
  
    
    
<span data-ttu-id="c0478-183">For more information about the JavaScript object model in Excel Services, see the  [Ewa](http://msdn.microsoft.com/library/6fe73191-3213-b986-1ad6-2c3b918a2241%28Office.15%29.aspx) namespace reference documentation.</span><span class="sxs-lookup"><span data-stu-id="c0478-183">For more information about the JavaScript object model in Excel Services, see the  [Ewa](http://msdn.microsoft.com/library/6fe73191-3213-b986-1ad6-2c3b918a2241%28Office.15%29.aspx) namespace reference documentation.</span></span>
  
    
    

### <a name="using-ecmascript-javascript-jscript"></a><span data-ttu-id="c0478-184">Using ECMAScript (JavaScript, JScript)</span><span class="sxs-lookup"><span data-stu-id="c0478-184">Using ECMAScript (JavaScript, JScript)</span></span>

<span data-ttu-id="c0478-185">For more information about JavaScript, see the following links:</span><span class="sxs-lookup"><span data-stu-id="c0478-185">For more information about JavaScript, see the following links:</span></span>
  
    
    

- <span data-ttu-id="c0478-186">For more information about the JavaScript object model in Excel Services, see the  [Ewa](http://msdn.microsoft.com/library/6fe73191-3213-b986-1ad6-2c3b918a2241%28Office.15%29.aspx) namespace reference documentation.</span><span class="sxs-lookup"><span data-stu-id="c0478-186">For more information about the JavaScript object model in Excel Services, see the  [Ewa](http://msdn.microsoft.com/library/6fe73191-3213-b986-1ad6-2c3b918a2241%28Office.15%29.aspx) namespace reference documentation.</span></span>
    
  
- <span data-ttu-id="c0478-187">For an example of how to interact with the JavaScript object model in Excel Services by using the Content Editor Web Part, see  [Walkthrough: Developing Using the Content Editor Web Part](walkthrough-developing-using-the-content-editor-web-part.md).</span><span class="sxs-lookup"><span data-stu-id="c0478-187">For an example of how to interact with the JavaScript object model in Excel Services by using the Content Editor Web Part, see  [Walkthrough: Developing Using the Content Editor Web Part](walkthrough-developing-using-the-content-editor-web-part.md).</span></span>
    
  

## <a name="rest-api"></a><span data-ttu-id="c0478-188">REST-API</span><span class="sxs-lookup"><span data-stu-id="c0478-188">REST API</span></span>

<span data-ttu-id="c0478-p111">The REST API in Excel Services is new in SharePoint Server 2010. By using the REST API, you can access workbook parts or elements directly through a URL.</span><span class="sxs-lookup"><span data-stu-id="c0478-p111">The REST API in Excel Services is new in SharePoint Server 2010. By using the REST API, you can access workbook parts or elements directly through a URL.</span></span> 
  
    
    
<span data-ttu-id="c0478-p112">The discovery mechanisms built into the Excel Services REST API also enable developers and users to explore the content of a workbook manually or programmatically, by supplying Atom feeds that contain information about the elements that reside in a specific workbook. The resources that you can access through the REST API are ranges, charts, tables, and PivotTables.</span><span class="sxs-lookup"><span data-stu-id="c0478-p112">The discovery mechanisms built into the Excel Services REST API also enable developers and users to explore the content of a workbook manually or programmatically, by supplying Atom feeds that contain information about the elements that reside in a specific workbook. The resources that you can access through the REST API are ranges, charts, tables, and PivotTables.</span></span> 
  
    
    
<span data-ttu-id="c0478-p113">Using the Atom feed provided by the REST API enables an easier way to get to the data that you care about. The feed contains traversable elements that allow any piece of code to discover what elements exist in a workbook.</span><span class="sxs-lookup"><span data-stu-id="c0478-p113">Using the Atom feed provided by the REST API enables an easier way to get to the data that you care about. The feed contains traversable elements that allow any piece of code to discover what elements exist in a workbook.</span></span> 
  
    
    
<span data-ttu-id="c0478-195">For more information, see  [Excel Services REST API](excel-services-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="c0478-195">For more information, see  [Excel Services REST API](excel-services-rest-api.md).</span></span>
  
    
    

### <a name="using-the-rest-api"></a><span data-ttu-id="c0478-196">Verwenden der REST-API</span><span class="sxs-lookup"><span data-stu-id="c0478-196">Using the REST API</span></span>

<span data-ttu-id="c0478-197">Thema:</span><span class="sxs-lookup"><span data-stu-id="c0478-197">For information about:</span></span>
  
    
    

- <span data-ttu-id="c0478-198">Accessing the REST service, and to view sample URIs for the REST service in Excel Services, see  [Accessing Excel Services REST API](sample-uri-for-excel-services-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="c0478-198">Accessing the REST service, and to view sample URIs for the REST service in Excel Services, see  [Accessing Excel Services REST API](sample-uri-for-excel-services-rest-api.md).</span></span>
    
  
- <span data-ttu-id="c0478-199">Accessing a schema for the REST service in Excel Services, see  [Accessing a Schema](accessing-a-schema.md).</span><span class="sxs-lookup"><span data-stu-id="c0478-199">Accessing a schema for the REST service in Excel Services, see  [Accessing a Schema](accessing-a-schema.md).</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="c0478-200">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="c0478-200">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="c0478-201">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="c0478-201">Tasks</span></span>


  
    
    
 [<span data-ttu-id="c0478-202">How to: Programmatically Add an Excel Web Access Web Part to a Page</span><span class="sxs-lookup"><span data-stu-id="c0478-202">How to: Programmatically Add an Excel Web Access Web Part to a Page</span></span>](how-to-programmatically-add-an-excel-web-access-web-part-to-a-page.md)
#### <a name="concepts"></a><span data-ttu-id="c0478-203">Konzepte</span><span class="sxs-lookup"><span data-stu-id="c0478-203">Concepts</span></span>


  
    
    
 [<span data-ttu-id="c0478-204">Excel Services (Übersicht)</span><span class="sxs-lookup"><span data-stu-id="c0478-204">Excel Services Overview</span></span>](excel-services-overview.md)
  
    
    
 [<span data-ttu-id="c0478-205">Excel Services-Architektur</span><span class="sxs-lookup"><span data-stu-id="c0478-205">Excel Services Architecture</span></span>](excel-services-architecture.md)
  
    
    
 [<span data-ttu-id="c0478-206">Unterstützte und nicht unterstützte Features</span><span class="sxs-lookup"><span data-stu-id="c0478-206">Supported and Unsupported Features</span></span>](supported-and-unsupported-features.md)
  
    
    
 [<span data-ttu-id="c0478-207">Excel Services - Blogs, Foren und Ressourcen</span><span class="sxs-lookup"><span data-stu-id="c0478-207">Excel Services Blogs, Forums, and Resources</span></span>](excel-services-blogs-forums-and-resources.md)
#### <a name="other-resources"></a><span data-ttu-id="c0478-208">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="c0478-208">Other resources</span></span>


  
    
    
 [<span data-ttu-id="c0478-209">Walkthrough: Developing a Custom Application Using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="c0478-209">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
