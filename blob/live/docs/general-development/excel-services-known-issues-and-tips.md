---
title: "Bekannte Probleme und Tipps für Excel Services"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: b4a41437-4f00-4f88-8510-627fa0252004
ms.openlocfilehash: fe4d36433bd8ebd2e5d4136dee746c65da741c44
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="excel-services-known-issues-and-tips"></a><span data-ttu-id="c0f0a-102">Bekannte Probleme und Tipps für Excel Services</span><span class="sxs-lookup"><span data-stu-id="c0f0a-102">Excel Services Known Issues and Tips</span></span>

<span data-ttu-id="c0f0a-103">The following are a known issues and tips for working with Excel Services.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-103">The following are a known issues and tips for working with Excel Services.</span></span>
  
    
    


## <a name="excel-web-service"></a><span data-ttu-id="c0f0a-104">Excel Web Service</span><span class="sxs-lookup"><span data-stu-id="c0f0a-104">Excel Web Service</span></span>


### <a name="viewing-the-wsdl-location"></a><span data-ttu-id="c0f0a-105">Viewing the WSDL Location</span><span class="sxs-lookup"><span data-stu-id="c0f0a-105">Viewing the WSDL Location</span></span>

<span data-ttu-id="c0f0a-106">You can view the Excel Web Services Web Services Description Language (WSDL) page by navigating to the following URL on the server:  `http://<server>/<customsite>/_vti_bin/excelservice.asmx?WSDL`</span><span class="sxs-lookup"><span data-stu-id="c0f0a-106">You can view the Excel Web Services Web Services Description Language (WSDL) page by navigating to the following URL on the server:  `http://<server>/<customsite>/_vti_bin/excelservice.asmx?WSDL`</span></span>
  
    
    
<span data-ttu-id="c0f0a-107">If you do not have a custom site, you can view the WSDL by using the following URL:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-107">If you do not have a custom site, you can view the WSDL by using the following URL:</span></span>
  
    
    
 `http://<server>/_vti_bin/excelservice.asmx?WSDL`
  
    
    
<span data-ttu-id="c0f0a-108">For more information, see  [Accessing the SOAP API](accessing-the-soap-api.md).</span><span class="sxs-lookup"><span data-stu-id="c0f0a-108">For more information, see  [Accessing the SOAP API](accessing-the-soap-api.md).</span></span>
  
    
    

### <a name="understanding-excel-web-services-and-namespaces"></a><span data-ttu-id="c0f0a-109">Understanding Excel Web Services and Namespaces</span><span class="sxs-lookup"><span data-stu-id="c0f0a-109">Understanding Excel Web Services and Namespaces</span></span>

<span data-ttu-id="c0f0a-110">The following are Excel web services and namespaces:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-110">The following are Excel web services and namespaces:</span></span>
  
    
    

- <span data-ttu-id="c0f0a-111">The single web service object that contains all the API methods: **ExcelService**</span><span class="sxs-lookup"><span data-stu-id="c0f0a-111">The single web service object that contains all the API methods: **ExcelService**</span></span>
    
  
- <span data-ttu-id="c0f0a-112">The schema namespace:  `http://schemas.microsoft.com/office/excel/server/webservices`</span><span class="sxs-lookup"><span data-stu-id="c0f0a-112">The schema namespace:  `http://schemas.microsoft.com/office/excel/server/webservices`</span></span>
    
  
- <span data-ttu-id="c0f0a-113">The web service page name: ExcelService.asmx</span><span class="sxs-lookup"><span data-stu-id="c0f0a-113">The web service page name: ExcelService.asmx</span></span>
    
  

### <a name="linking-locally-or-to-a-web-service"></a><span data-ttu-id="c0f0a-114">Linking Locally or to a Web Service</span><span class="sxs-lookup"><span data-stu-id="c0f0a-114">Linking Locally or to a Web Service</span></span>

<span data-ttu-id="c0f0a-115">In certain scenarios, you should link directly to Microsoft.Office.Excel.Server.WebServices.dll and access it as you would any local assembly, instead of calling it as a web service through SOAP over HTTP.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-115">In certain scenarios, you should link directly to Microsoft.Office.Excel.Server.WebServices.dll and access it as you would any local assembly, instead of calling it as a web service through SOAP over HTTP.</span></span> 
  
    
    
<span data-ttu-id="c0f0a-116">For more information and guidelines on when to use direct linking, see  [Loop-Back SOAP Calls and Direct Linking](loop-back-soap-calls-and-direct-linking.md).</span><span class="sxs-lookup"><span data-stu-id="c0f0a-116">For more information and guidelines on when to use direct linking, see  [Loop-Back SOAP Calls and Direct Linking](loop-back-soap-calls-and-direct-linking.md).</span></span>
  
    
    

### <a name="understanding-invalid-characters"></a><span data-ttu-id="c0f0a-117">Understanding Invalid Characters</span><span class="sxs-lookup"><span data-stu-id="c0f0a-117">Understanding Invalid Characters</span></span>

<span data-ttu-id="c0f0a-118">The calls to the **GetCell** and **GetRange** methods will fail if the workbook cells contain characters that are invalid in an XML response.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-118">The calls to the **GetCell** and **GetRange** methods will fail if the workbook cells contain characters that are invalid in an XML response.</span></span>
  
    
    
<span data-ttu-id="c0f0a-119">For example, if a cell contains characters with hexadecimal values 0x1, 0x2 ... 0x8, the ASP.NET parser will throw an exception that the value of the character being written to the XML response is invalid:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-119">For example, if a cell contains characters with hexadecimal values 0x1, 0x2 ... 0x8, the ASP.NET parser will throw an exception that the value of the character being written to the XML response is invalid:</span></span>
  
    
    
 <span data-ttu-id="c0f0a-120">**System.InvalidOperationException: Client found response content type of 'text/html; charset=utf-8', but expected 'text/xml'. The request failed with the error message: -- <html> <head> <title>' ', hexadecimal value 0x01, is an invalid character.</title>**</span><span class="sxs-lookup"><span data-stu-id="c0f0a-120">**System.InvalidOperationException: Client found response content type of 'text/html; charset=utf-8', but expected 'text/xml'. The request failed with the error message: -- <html> <head> <title>' ', hexadecimal value 0x01, is an invalid character.</title>**</span></span>
  
    
    
<span data-ttu-id="c0f0a-p101">This behavior is expected. The XML specification that defines which characters are allowed in a valid XML response specifies that hexadecimal values 0x1, 0x2 ... 0x8 are invalid XML characters:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-p101">This behavior is expected. The XML specification that defines which characters are allowed in a valid XML response specifies that hexadecimal values 0x1, 0x2 ... 0x8 are invalid XML characters:</span></span>
  
    
    
 <span data-ttu-id="c0f0a-123">**Char ::= #x9 | #xA | #xD | [#x20-#xD7FF] | [#xE000-#xFFFD] | [#x10000-#x10FFFF] /* any Unicode character, excluding the surrogate blocks, FFFE, and FFFF. */**</span><span class="sxs-lookup"><span data-stu-id="c0f0a-123">**Char ::= #x9 | #xA | #xD | [#x20-#xD7FF] | [#xE000-#xFFFD] | [#x10000-#x10FFFF] /* any Unicode character, excluding the surrogate blocks, FFFE, and FFFF. */**</span></span>
  
    
    
<span data-ttu-id="c0f0a-124">For more information, see  [W3C Extensible Markup Language (XML) Specification](http://www.w3.org/TR/REC-xml) (http://www.w3.org/TR/REC-xml#NT-Char).</span><span class="sxs-lookup"><span data-stu-id="c0f0a-124">For more information, see  [W3C Extensible Markup Language (XML) Specification](http://www.w3.org/TR/REC-xml) (http://www.w3.org/TR/REC-xml#NT-Char).</span></span>
  
    
    

### <a name="saving-a-workbook"></a><span data-ttu-id="c0f0a-125">Saving a Workbook</span><span class="sxs-lookup"><span data-stu-id="c0f0a-125">Saving a Workbook</span></span>

<span data-ttu-id="c0f0a-p102">When you make changes to a workbookfor example, by setting values to a range using Excel Web Servicesthe changes to the workbook are preserved only for that particular session. The changes are not saved or persisted back to the original workbook. When the current workbook session ends (for example, when you call the **CloseWorkbook** method, or the session times out), changes you made will be lost.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-p102">When you make changes to a workbook—for example, by setting values to a range using Excel Web Services—the changes to the workbook are preserved only for that particular session. The changes are not saved or persisted back to the original workbook. When the current workbook session ends (for example, when you call the **CloseWorkbook** method, or the session times out), changes you made will be lost.</span></span>
  
    
    
<span data-ttu-id="c0f0a-p103">If you want to save changes to a workbook, you can use the **GetWorkbook** method and then save the workbook using the API of the destination file store. For more information, see [How to: Get an Entire Workbook or a Snapshot](how-to-get-an-entire-workbook-or-a-snapshot.md) and [How to: Save a Workbook](http://msdn.microsoft.com/library/feb74f7a-2d8f-4672-911b-de85f8852aea%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0f0a-p103">If you want to save changes to a workbook, you can use the **GetWorkbook** method and then save the workbook using the API of the destination file store. For more information, see [How to: Get an Entire Workbook or a Snapshot](how-to-get-an-entire-workbook-or-a-snapshot.md) and [How to: Save a Workbook](http://msdn.microsoft.com/library/feb74f7a-2d8f-4672-911b-de85f8852aea%28Office.15%29.aspx).</span></span>
  
    
    

### <a name="understanding-the-url-property-of-an-excel-web-services-proxy-class"></a><span data-ttu-id="c0f0a-131">Understanding the Url Property of an Excel Web Services Proxy Class</span><span class="sxs-lookup"><span data-stu-id="c0f0a-131">Understanding the Url Property of an Excel Web Services Proxy Class</span></span>

<span data-ttu-id="c0f0a-p104">Do not use the **Url** property of an Excel Web Services proxy for the location of the workbook you want to open. The **Url** property of a web service proxy class generated by Visual Studio gets or sets the base URL of the XML web service the client is requesting. In the case of Excel Web Services, this is usually:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-p104">Do not use the **Url** property of an Excel Web Services proxy for the location of the workbook you want to open. The **Url** property of a web service proxy class generated by Visual Studio gets or sets the base URL of the XML web service the client is requesting. In the case of Excel Web Services, this is usually:</span></span>
  
    
    
 `http://<server name>/_vti_bin/ExcelService.asmx`
  
    
    
<span data-ttu-id="c0f0a-135">To specify the location of a workbook, use the **OpenWorkbook** method instead of the **Url** property as shown in the following code example.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-135">To specify the location of a workbook, use the **OpenWorkbook** method instead of the **Url** property as shown in the following code example.</span></span>
  
    
    



```

//Instantiate the web service and make a status array object.
ExcelService xlservice = new ExcelService();
string sheetName = "Sheet1";         

//Set the path to the workbook to open.
//TODO: Change the path to the workbook
 //to point to a workbook you have access to.
//The workbook must be in a trusted location.
string targetWorkbookPath = 
   "http://myserver02/example/Shared%20Documents/Book1.xlsx";

//Set credentials for requests.
xlservice.Credentials = System.Net.CredentialCache.DefaultCredentials;

//Call the open workbook, and point to the trusted   
//location of the workbook to open.
string sessionId = xlservice.OpenWorkbook(targetWorkbookPath, "en-US", 
    "en-US", out outStatus);
                
```

<span data-ttu-id="c0f0a-136">For more information, see  [WebClientProtocol.Url Property](http://go.microsoft.com/fwlink/?LinkId=64908) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpref/html/frlrfSystemWebServicesProtocolsWebClientProtocolClassUrlTopic.asp).</span><span class="sxs-lookup"><span data-stu-id="c0f0a-136">For more information, see  [WebClientProtocol.Url Property](http://go.microsoft.com/fwlink/?LinkId=64908) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpref/html/frlrfSystemWebServicesProtocolsWebClientProtocolClassUrlTopic.asp).</span></span>
  
    
    

## <a name="understanding-security"></a><span data-ttu-id="c0f0a-137">Understanding Security</span><span class="sxs-lookup"><span data-stu-id="c0f0a-137">Understanding Security</span></span>


### <a name="using-workbook-permissions"></a><span data-ttu-id="c0f0a-138">Using Workbook Permissions</span><span class="sxs-lookup"><span data-stu-id="c0f0a-138">Using Workbook Permissions</span></span>

<span data-ttu-id="c0f0a-139">Beware of the following issues regarding workbook permissions:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-139">Beware of the following issues regarding workbook permissions:</span></span>
  
    
    

- <span data-ttu-id="c0f0a-p105">Excel Web Services uses the Microsoft SharePoint Foundation authorization scheme to verify that the caller has the right to call APIs (that is, make web service calls) on the SharePoint Foundation site (that is, the Web site where Excel Web Services is located) remotely. If the caller does not have the "Use Remote API" right, the Excel Web Services returns an "HTTP 401 (Unauthorized)" error, and logs an "API authorization failed" event. Excel Web Services performs these authorization checks only for calls that originate as SOAP calls. Calls from applications that link locally to Microsoft.Office.Excel.Server.WebServices.dll are not considered remote calls. Therefore, they are not subject to authorization checks. However, if the application that links locally to Microsoft.Office.Excel.Server.WebServices.dll is itself a SOAP service, and handles the service's SOAP calls, the call to Excel Web Services will seem like a SOAP call (even though the application links directly to Microsoft.Office.Excel.Server.WebServices.dll). In this scenario, Excel Web Services will perform the authorization checks.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-p105">Excel Web Services uses the Microsoft SharePoint Foundation authorization scheme to verify that the caller has the right to call APIs (that is, make web service calls) on the SharePoint Foundation site (that is, the Web site where Excel Web Services is located) remotely. If the caller does not have the "Use Remote API" right, the Excel Web Services returns an "HTTP 401 (Unauthorized)" error, and logs an "API authorization failed" event. Excel Web Services performs these authorization checks only for calls that originate as SOAP calls. Calls from applications that link locally to Microsoft.Office.Excel.Server.WebServices.dll are not considered remote calls. Therefore, they are not subject to authorization checks. However, if the application that links locally to Microsoft.Office.Excel.Server.WebServices.dll is itself a SOAP service, and handles the service's SOAP calls, the call to Excel Web Services will seem like a SOAP call (even though the application links directly to Microsoft.Office.Excel.Server.WebServices.dll). In this scenario, Excel Web Services will perform the authorization checks.</span></span>
    
  
- <span data-ttu-id="c0f0a-147">To get the entire workbook (for example, by calling the **GetWorkbook** method using the `WorkbookType.FullWorkbook` argument), the caller needs "open" permission for the workbook or "read" permission in a file share.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-147">To get the entire workbook (for example, by calling the **GetWorkbook** method using the `WorkbookType.FullWorkbook` argument), the caller needs "open" permission for the workbook or "read" permission in a file share.</span></span>
    
  
- <span data-ttu-id="c0f0a-148">To call the **GetApiVersion** method, no permission is necessary.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-148">To call the **GetApiVersion** method, no permission is necessary.</span></span>
    
  
- <span data-ttu-id="c0f0a-149">For the rest of the Excel Web Services methods, besides credentials, the caller needs "view" permission (in SharePoint Foundation) or "read" permission (in a file share) for the workbook.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-149">For the rest of the Excel Web Services methods, besides credentials, the caller needs "view" permission (in SharePoint Foundation) or "read" permission (in a file share) for the workbook.</span></span>
    
  

### <a name="trusted-location"></a><span data-ttu-id="c0f0a-150">Trusted Location</span><span class="sxs-lookup"><span data-stu-id="c0f0a-150">Trusted Location</span></span>

<span data-ttu-id="c0f0a-p106">The workbooks you want to open in Excel Services must be placed in a trusted location. If not, the Excel Web Services calls to open the workbook will fail.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-p106">The workbooks you want to open in Excel Services must be placed in a trusted location. If not, the Excel Web Services calls to open the workbook will fail.</span></span>
  
    
    
<span data-ttu-id="c0f0a-153">For information about how to trust a location, see  [How to: Trust a Location](how-to-trust-a-location.md) and [How to: Trust Workbook Locations Using Script](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0f0a-153">For information about how to trust a location, see  [How to: Trust a Location](how-to-trust-a-location.md) and [How to: Trust Workbook Locations Using Script](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="visual-studio"></a><span data-ttu-id="c0f0a-154">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c0f0a-154">Visual Studio</span></span>


### <a name="microsoft-visual-studio-proxy-behavior"></a><span data-ttu-id="c0f0a-155">Microsoft Visual Studio Proxy Behavior</span><span class="sxs-lookup"><span data-stu-id="c0f0a-155">Microsoft Visual Studio Proxy Behavior</span></span>

<span data-ttu-id="c0f0a-156">When Microsoft Visual Studio creates a proxy class for a client project that calls Excel Web Services, it has the following behavior:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-156">When Microsoft Visual Studio creates a proxy class for a client project that calls Excel Web Services, it has the following behavior:</span></span> 
  
    
    
<span data-ttu-id="c0f0a-p107">If a method has no return value, and one or more **out** arguments, the first **out** argument is moved to become the return value. That is, the method in the proxy class will have one less **out** argument in the method signature. But the signature will have a return value with the type and content of what used to be the first **out** argument.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-p107">If a method has no return value, and one or more **out** arguments, the first **out** argument is moved to become the return value. That is, the method in the proxy class will have one less **out** argument in the method signature. But the signature will have a return value with the type and content of what used to be the first **out** argument.</span></span>
  
    
    
<span data-ttu-id="c0f0a-160">The affected Excel Web Services methods are:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-160">The affected Excel Web Services methods are:</span></span>
  
    
    

- <span data-ttu-id="c0f0a-161">**Calculate**</span><span class="sxs-lookup"><span data-stu-id="c0f0a-161">**Calculate**</span></span>
    
  
- <span data-ttu-id="c0f0a-162">**CalculateA1**</span><span class="sxs-lookup"><span data-stu-id="c0f0a-162">**CalculateA1**</span></span>
    
  
- <span data-ttu-id="c0f0a-163">**CalculateWorkbook**</span><span class="sxs-lookup"><span data-stu-id="c0f0a-163">**CalculateWorkbook**</span></span>
    
  
- <span data-ttu-id="c0f0a-164">**CancelRequest**</span><span class="sxs-lookup"><span data-stu-id="c0f0a-164">**CancelRequest**</span></span>
    
  
- <span data-ttu-id="c0f0a-165">**CloseWorkbook**</span><span class="sxs-lookup"><span data-stu-id="c0f0a-165">**CloseWorkbook method**</span></span>
    
  
- <span data-ttu-id="c0f0a-166">**GetSessionInformation**</span><span class="sxs-lookup"><span data-stu-id="c0f0a-166">**GetSessionInformation**</span></span>
    
  
- <span data-ttu-id="c0f0a-167">**Refresh**</span><span class="sxs-lookup"><span data-stu-id="c0f0a-167">**Refresh**</span></span>
    
  
- <span data-ttu-id="c0f0a-168">**SetCell**</span><span class="sxs-lookup"><span data-stu-id="c0f0a-168">**SetCell**</span></span>
    
  
- <span data-ttu-id="c0f0a-169">**SetCellA1**</span><span class="sxs-lookup"><span data-stu-id="c0f0a-169">**SetCellA1**</span></span>
    
  
- <span data-ttu-id="c0f0a-170">**SetRange**</span><span class="sxs-lookup"><span data-stu-id="c0f0a-170">**SetRange**</span></span>
    
  
- <span data-ttu-id="c0f0a-171">**SetRangeA1**</span><span class="sxs-lookup"><span data-stu-id="c0f0a-171">**SetRangeA1**</span></span>
    
  

## <a name="excel-services-user-defined-functions"></a><span data-ttu-id="c0f0a-172">Benutzerdefinierte Funktionen für Excel Services</span><span class="sxs-lookup"><span data-stu-id="c0f0a-172">Excel Services User-Defined Functions</span></span>


### <a name="global-assembly-cache-is-checked-first-then-the-local-folder"></a><span data-ttu-id="c0f0a-173">Global Assembly Cache is Checked First, Then the Local Folder</span><span class="sxs-lookup"><span data-stu-id="c0f0a-173">Global Assembly Cache is Checked First, Then the Local Folder</span></span>

<span data-ttu-id="c0f0a-p108">By design in the Microsoft .NET Framework, an assembly in a global assembly cache will be loaded instead of the same assembly in a local folder. The common language runtime will look for an assembly in the global assembly cache first before searching in the local folders.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-p108">By design in the Microsoft .NET Framework, an assembly in a global assembly cache will be loaded instead of the same assembly in a local folder. The common language runtime will look for an assembly in the global assembly cache first before searching in the local folders.</span></span>
  
    
    
<span data-ttu-id="c0f0a-176">Therefore, if an assembly is installed in the global assembly cache and is in the UDF list but disabled (or removed from the UDF list altogether), and an identical assembly is installed in a local folder and enabled, the assembly in the global assembly cache will still get loaded and used instead of the same assembly in the local folder.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-176">Therefore, if an assembly is installed in the global assembly cache and is in the UDF list but disabled (or removed from the UDF list altogether), and an identical assembly is installed in a local folder and enabled, the assembly in the global assembly cache will still get loaded and used instead of the same assembly in the local folder.</span></span>
  
    
    
<span data-ttu-id="c0f0a-177">This does not affect upgrade scenarios in which the assembly version has been modified, which means the assembly is not the same anymore.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-177">This does not affect upgrade scenarios in which the assembly version has been modified, which means the assembly is not the same anymore.</span></span>
  
    
    

## <a name="general"></a><span data-ttu-id="c0f0a-178">Allgemein</span><span class="sxs-lookup"><span data-stu-id="c0f0a-178">General</span></span>


### <a name="order-of-strings-in-sharedstringxml-is-not-maintained"></a><span data-ttu-id="c0f0a-179">Order of Strings in Sharedstring.xml is Not Maintained</span><span class="sxs-lookup"><span data-stu-id="c0f0a-179">Order of Strings in Sharedstring.xml is Not Maintained</span></span>

<span data-ttu-id="c0f0a-p109">Excel Services does not maintain the original order of strings in a workbook shared-string table (the Sharedstrings.xml part within the Microsoft Office Excel XML-Format file). For example, execute the following steps:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-p109">Excel Services does not maintain the original order of strings in a workbook shared-string table (the Sharedstrings.xml part within the Microsoft Office Excel XML Format file). For example, execute the following steps:</span></span>
  
    
    

1. <span data-ttu-id="c0f0a-182">Open a file using Excel.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-182">Open a file using Excel.</span></span> 
    
  
2. <span data-ttu-id="c0f0a-183">Save the file in .xlsx file format.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-183">Save the file in .xlsx file format.</span></span> 
    
  
3. <span data-ttu-id="c0f0a-184">Upload the file to a document library that is a trusted location.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-184">Upload the file to a document library that is a trusted location.</span></span>
    
  
4. <span data-ttu-id="c0f0a-185">Open the file in the document library by using Excel Web Access.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-185">Open the file in the document library by using Excel Web Access.</span></span>
    
  
5. <span data-ttu-id="c0f0a-186">Click **Open in Excel**.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-186">Click **Open in Excel**.</span></span>
    
  
6. <span data-ttu-id="c0f0a-187">Save the file in .xlsx file format.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-187">Save the file in .xlsx file format.</span></span>
    
  
<span data-ttu-id="c0f0a-188">If you compare the Sharedstrings.xml file created in Step 2 with the one created in Step 6, you will find the order of the Sharedstrings.xml parts might be different.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-188">If you compare the Sharedstrings.xml file created in Step 2 with the one created in Step 6, you will find the order of the Sharedstrings.xml parts might be different.</span></span>
  
    
    
<span data-ttu-id="c0f0a-p110">You should not write an application that assumes the order of strings in the shared-string table is fixed. For example, you cannot replace the shared-string table with an existing localized translation table. You must adjust to the new ordering of strings in the shared-string table.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-p110">You should not write an application that assumes the order of strings in the shared-string table is fixed. For example, you cannot replace the shared-string table with an existing localized translation table. You must adjust to the new ordering of strings in the shared-string table.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="c0f0a-192">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="c0f0a-192">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="c0f0a-193">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="c0f0a-193">Tasks</span></span>


  
    
    
 [<span data-ttu-id="c0f0a-194">How to: Trust a Location</span><span class="sxs-lookup"><span data-stu-id="c0f0a-194">How to: Trust a Location</span></span>](how-to-trust-a-location.md)
#### <a name="concepts"></a><span data-ttu-id="c0f0a-195">Konzepte</span><span class="sxs-lookup"><span data-stu-id="c0f0a-195">Concepts</span></span>


  
    
    
 [<span data-ttu-id="c0f0a-196">Excel Services Best Practices</span><span class="sxs-lookup"><span data-stu-id="c0f0a-196">Excel Services Best Practices</span></span>](excel-services-best-practices.md)
  
    
    
 [<span data-ttu-id="c0f0a-197">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="c0f0a-197">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="c0f0a-198">Excel Services-Architektur</span><span class="sxs-lookup"><span data-stu-id="c0f0a-198">Excel Services Architecture</span></span>](excel-services-architecture.md)
  
    
    
 [<span data-ttu-id="c0f0a-199">Unterstützte und nicht unterstützte Features</span><span class="sxs-lookup"><span data-stu-id="c0f0a-199">Supported and Unsupported Features</span></span>](supported-and-unsupported-features.md)
  
    
    
 [<span data-ttu-id="c0f0a-200">Accessing the SOAP API</span><span class="sxs-lookup"><span data-stu-id="c0f0a-200">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
  
    
    
 [<span data-ttu-id="c0f0a-201">Excel Services - Blogs, Foren und Ressourcen</span><span class="sxs-lookup"><span data-stu-id="c0f0a-201">Excel Services Blogs, Forums, and Resources</span></span>](excel-services-blogs-forums-and-resources.md)
