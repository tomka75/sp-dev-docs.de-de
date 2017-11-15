---
title: "Bewährte Methoden für Excel Services"
ms.date: 09/25/2017
keywords: Richtlinien
f1_keywords: guidelines
ms.prod: sharepoint
ms.assetid: 56fa3913-c156-49da-bed0-a6a106fc129f
ms.openlocfilehash: 0e425e366f3dd54e1d7eaff609e0854a6f82a9d7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="excel-services-best-practices"></a><span data-ttu-id="96a99-103">Bewährte Methoden für Excel Services</span><span class="sxs-lookup"><span data-stu-id="96a99-103">Excel Services Best Practices</span></span>

<span data-ttu-id="96a99-104">This topic contains a list of best-practice recommendations for working with Excel Services.</span><span class="sxs-lookup"><span data-stu-id="96a99-104">This topic contains a list of best-practice recommendations for working with Excel Services.</span></span>
  
    
    


## <a name="mitigating-threats"></a><span data-ttu-id="96a99-105">Mitigating Threats</span><span class="sxs-lookup"><span data-stu-id="96a99-105">Mitigating Threats</span></span>


### <a name="anonymous-access-and-information-disclosure"></a><span data-ttu-id="96a99-106">Anonymous Access and Information Disclosure</span><span class="sxs-lookup"><span data-stu-id="96a99-106">Anonymous Access and Information Disclosure</span></span>

<span data-ttu-id="96a99-p101">The following settings combination gives anonymous users access to any files in the share to which the process account has access. Therefore, the following combination of settings is not recommended, because of the possibility of information disclosure:</span><span class="sxs-lookup"><span data-stu-id="96a99-p101">The following settings combination gives anonymous users access to any files in the share to which the process account has access. Therefore, the following combination of settings is not recommended, because of the possibility of information disclosure:</span></span>
  
    
    

- <span data-ttu-id="96a99-109">Anonymous access to Microsoft SharePoint Foundation is turned on.</span><span class="sxs-lookup"><span data-stu-id="96a99-109">Anonymous access to Microsoft SharePoint Foundation is turned on.</span></span>
    
  
- <span data-ttu-id="96a99-110">Sie verfügen über einen vertrauenswürdigen UNC-Speicherort und das **Prozesskonto** ist aktiviert.</span><span class="sxs-lookup"><span data-stu-id="96a99-110">You have a UNC trusted location and the **Process account** is turned on.</span></span>
    
  

> <span data-ttu-id="96a99-111">**Hinweis:** Das **Prozesskonto** ist eine globale Einstellung von Excel Services, die Auswirkung auf alle vertrauenswürdigen Speicherorte hat.</span><span class="sxs-lookup"><span data-stu-id="96a99-111">**Note** The **Process account** is a global Excel Services setting that affects all trusted locations.</span></span>
  
    
    


### <a name="to-view-the-process-account-option"></a><span data-ttu-id="96a99-112">So zeigen Sie die Option „Prozesskonto“ an</span><span class="sxs-lookup"><span data-stu-id="96a99-112">To view the Process account option</span></span>


1. <span data-ttu-id="96a99-113">On the **Start** menu, click **All Programs**.</span><span class="sxs-lookup"><span data-stu-id="96a99-113">On the **Start** menu, click **All Programs**.</span></span>
    
  
2. <span data-ttu-id="96a99-114">Point to **Microsoft SharePoint 2010 Products**, and then click **SharePoint Central Administration**.</span><span class="sxs-lookup"><span data-stu-id="96a99-114">Point to **Microsoft SharePoint 2010 Products**, and then click **SharePoint Central Administration**.</span></span>
    
  
3. <span data-ttu-id="96a99-115">Under **Application Management**, click **Manage service applications**.</span><span class="sxs-lookup"><span data-stu-id="96a99-115">Under **Application Management**, click **Manage service applications**.</span></span>
    
  
4. <span data-ttu-id="96a99-116">On the Manage Service Applications page, click **Excel Services Application**.</span><span class="sxs-lookup"><span data-stu-id="96a99-116">On the Manage Service Applications page, click **Excel Services Application**.</span></span>
    
  
5. <span data-ttu-id="96a99-117">On the **Excel Services Application** page, click **Global Settings**.</span><span class="sxs-lookup"><span data-stu-id="96a99-117">On the **Excel Services Application** page, click **Global Settings**.</span></span>
    
  
6. <span data-ttu-id="96a99-118">In the **Security** section, look under **File Access Method** for the **Process account** option.</span><span class="sxs-lookup"><span data-stu-id="96a99-118">In the **Security** section, look under **File Access Method** for the **Process account** option.</span></span>
    
  

### <a name="denial-of-service-attack"></a><span data-ttu-id="96a99-119">Denial of Service Attack</span><span class="sxs-lookup"><span data-stu-id="96a99-119">Denial of Service Attack</span></span>

<span data-ttu-id="96a99-p102">In a denial of service attack against a Web service, an attacker generates very large, individual requests against the Web service. The purpose is to attempt to exploit the limits of one or more Web service input values.</span><span class="sxs-lookup"><span data-stu-id="96a99-p102">In a denial of service attack against a Web service, an attacker generates very large, individual requests against the Web service. The purpose is to attempt to exploit the limits of one or more Web service input values.</span></span>
  
    
    
<span data-ttu-id="96a99-122">We recommend that you use the Microsoft Internet Information Services (IIS) setting to set the maximum request size for the Web service.</span><span class="sxs-lookup"><span data-stu-id="96a99-122">We recommend that you use the Microsoft Internet Information Services (IIS) setting to set the maximum request size for the Web service.</span></span>
  
    
    
<span data-ttu-id="96a99-p103">Use the **maxRequestLength** attribute in the **httpRuntime** element in the **system.web** element to prevent denial of service attacks that are caused by users posting large files to the server. The default size is 4096 KB (4 MB).</span><span class="sxs-lookup"><span data-stu-id="96a99-p103">Use the **maxRequestLength** attribute in the **httpRuntime** element in the **system.web** element to prevent denial of service attacks that are caused by users posting large files to the server. The default size is 4096 KB (4 MB).</span></span>
  
    
    
<span data-ttu-id="96a99-125">Weitere Informationen finden Sie unter [\<httpRuntime\>-Element](http://msdn.microsoft.com/library/e9b81350-8aaf-47cc-9843-5f7d0c59f369.aspx) und [\<maxRequestLength\>-Element](http://msdn.microsoft.com/library/fd52b2c5-5014-4e6f-b869-4ea666dc83d6.aspx).</span><span class="sxs-lookup"><span data-stu-id="96a99-125">For more information, see <httpRuntime> Element and <maxRequestLength> Element.</span></span>
  
    
    

### <a name="sniffing-between-the-calling-application-and-the-web-service-computer"></a><span data-ttu-id="96a99-126">Ermitteln zwischen der aufrufenden Anwendung und dem Webdienstcomputer</span><span class="sxs-lookup"><span data-stu-id="96a99-126">Sniffing Between the Calling Application and the Web Service Computer</span></span>

<span data-ttu-id="96a99-p104">If the calling application and Excel Web Services are deployed to different computers, an attacker can listen to the network traffic for data transfer between the calling application and the Web service. This threat is also called "sniffing" or "eavesdropping."</span><span class="sxs-lookup"><span data-stu-id="96a99-p104">If the calling application and Excel Web Services are deployed to different computers, an attacker can listen to the network traffic for data transfer between the calling application and the Web service. This threat is also called "sniffing" or "eavesdropping."</span></span>
  
    
    
<span data-ttu-id="96a99-129">To help mitigate this threat, we recommend that you:</span><span class="sxs-lookup"><span data-stu-id="96a99-129">To help mitigate this threat, we recommend that you:</span></span>
  
    
    

- <span data-ttu-id="96a99-p105">Use Secure Sockets Layer (SSL) to set up a secure channel to protect data transfer between the client and the server. The SSL protocol helps to protect data against packet sniffing by anyone with physical access to the network.</span><span class="sxs-lookup"><span data-stu-id="96a99-p105">Use Secure Sockets Layer (SSL) to set up a secure channel to protect data transfer between the client and the server. The SSL protocol helps to protect data against packet sniffing by anyone with physical access to the network.</span></span>
    
  
- <span data-ttu-id="96a99-132">Physically protect the relevant network if a custom application using Excel Web Services is running in a confined networkfor example, if Excel Web Services is deployed on a Web front-end computer within the enterprise.</span><span class="sxs-lookup"><span data-stu-id="96a99-132">Physically protect the relevant network if a custom application using Excel Web Services is running in a confined network—for example, if Excel Web Services is deployed on a Web front-end computer within the enterprise.</span></span>
    
  
<span data-ttu-id="96a99-133">For more information, see  [Securing Your Network](http://msdn.microsoft.com/library/af62ece0-0dd7-4b8e-ad12-4d13f2d60816.aspx) and [SOAP Security](http://msdn.microsoft.com/en-us/library/aa912494.aspx).</span><span class="sxs-lookup"><span data-stu-id="96a99-133">For more information, see  [Securing Your Network](http://msdn.microsoft.com/library/af62ece0-0dd7-4b8e-ad12-4d13f2d60816.aspx) and [SOAP Security](http://msdn.microsoft.com/en-us/library/aa912494.aspx).</span></span>
  
    
    
<span data-ttu-id="96a99-134">For information about Excel Services topology, scalability, performance, and security, see the Microsoft SharePoint Server 2010 TechCenter.</span><span class="sxs-lookup"><span data-stu-id="96a99-134">For information about Excel Services topology, scalability, performance, and security, see the Microsoft SharePoint Server 2010 TechCenter.</span></span>
  
    
    

### <a name="spoofing"></a><span data-ttu-id="96a99-135">Spoofing</span><span class="sxs-lookup"><span data-stu-id="96a99-135">Spoofing</span></span>

<span data-ttu-id="96a99-136">We recommend that you use SSL to help mitigate the threats of hijacked Web service Internet Protocol (IP) addresses and ports, and to help prevent attackers from receiving requests and replying on behalf of the Web service.</span><span class="sxs-lookup"><span data-stu-id="96a99-136">We recommend that you use SSL to help mitigate the threats of hijacked Web service Internet Protocol (IP) addresses and ports, and to help prevent attackers from receiving requests and replying on behalf of the Web service.</span></span>
  
    
    
<span data-ttu-id="96a99-p106">The SSL certificate is matched against a few properties, one of which is the IP address from which the message is coming. The attacker cannot spoof the IP address if it does not have the Web service SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="96a99-p106">The SSL certificate is matched against a few properties, one of which is the IP address from which the message is coming. The attacker cannot spoof the IP address if it does not have the Web service SSL certificate.</span></span>
  
    
    
<span data-ttu-id="96a99-139">For more information, see  [Securing Your Network](http://msdn.microsoft.com/library/af62ece0-0dd7-4b8e-ad12-4d13f2d60816.aspx).</span><span class="sxs-lookup"><span data-stu-id="96a99-139">For more information, see  [Securing Your Network](http://msdn.microsoft.com/library/af62ece0-0dd7-4b8e-ad12-4d13f2d60816.aspx).</span></span>
  
    
    

## <a name="excel-services-user-defined-functions-udfs"></a><span data-ttu-id="96a99-140">Excel Services User-Defined Functions (UDFs)</span><span class="sxs-lookup"><span data-stu-id="96a99-140">Excel Services User-Defined Functions (UDFs)</span></span>


### <a name="strong-name-dependencies"></a><span data-ttu-id="96a99-141">Strong Name Dependencies</span><span class="sxs-lookup"><span data-stu-id="96a99-141">Strong Name Dependencies</span></span>

<span data-ttu-id="96a99-p107">In some cases, a user-defined function (UDF) assembly depends on other assemblies that are deployed with it. These dependent DLLs load successfully if they are in the global assembly cache, or if they are located in the same folder as the UDF assembly.</span><span class="sxs-lookup"><span data-stu-id="96a99-p107">In some cases, a user-defined function (UDF) assembly depends on other assemblies that are deployed with it. These dependent DLLs load successfully if they are in the global assembly cache, or if they are located in the same folder as the UDF assembly.</span></span>
  
    
    
<span data-ttu-id="96a99-p108">In the latter case, however, it is possible for the load to fail if Dienste für Excel-Berechnungen has already loaded another assembly with the same name. (It fails either because the assembly is not strongly named, or because another version with the same name has been deployed and loaded.)</span><span class="sxs-lookup"><span data-stu-id="96a99-p108">In the latter case, however, it is possible for the load to fail if Excel Calculation Services has already loaded another assembly with the same name. (It fails either because the assembly is not strongly named, or because another version with the same name has been deployed and loaded.)</span></span>
  
    
    
<span data-ttu-id="96a99-146">Consider the following scenario, with the following directory structure:</span><span class="sxs-lookup"><span data-stu-id="96a99-146">Consider the following scenario, with the following directory structure:</span></span>
  
    
    

1. <span data-ttu-id="96a99-147">C:\\Udfs\\Udf01</span><span class="sxs-lookup"><span data-stu-id="96a99-147">C:\Udfs\Udf01</span></span>
    
    <span data-ttu-id="96a99-148">The Udf01 folder contains:</span><span class="sxs-lookup"><span data-stu-id="96a99-148">The Udf01 folder contains:</span></span>
    
  - <span data-ttu-id="96a99-149">Udf01.dll</span><span class="sxs-lookup"><span data-stu-id="96a99-149">Udf01.dll</span></span> 
    
  
  - <span data-ttu-id="96a99-150">dependent.dll (not strongly named)</span><span class="sxs-lookup"><span data-stu-id="96a99-150">dependent.dll (not strongly named)</span></span>
    
  

    <span data-ttu-id="96a99-151">The Udf01.dll file has a dependency on the dependent.dll file.</span><span class="sxs-lookup"><span data-stu-id="96a99-151">The Udf01.dll file has a dependency on the dependent.dll file.</span></span>
    
  
2. <span data-ttu-id="96a99-152">C:\\Udfs\\Udf02</span><span class="sxs-lookup"><span data-stu-id="96a99-152">C:\Udfs\Udf02</span></span>
    
    <span data-ttu-id="96a99-153">The Udf02 folder contains:</span><span class="sxs-lookup"><span data-stu-id="96a99-153">The Udf02 folder contains:</span></span>
    
  - <span data-ttu-id="96a99-154">Udf02.dll (which depends on Interop.dll)</span><span class="sxs-lookup"><span data-stu-id="96a99-154">Udf02.dll (which depends on Interop.dll)</span></span>
    
  
  - <span data-ttu-id="96a99-155">dependent.dll (which is not strongly named)</span><span class="sxs-lookup"><span data-stu-id="96a99-155">dependent.dll (which is not strongly named)</span></span>
    
  

    <span data-ttu-id="96a99-p109">The Udf02.dll file has a dependency on the dependent.dll file. Udf01.dll's dependency and Udf02.dll's dependency share the same name. But Udf02.dll's dependent.dll file is not the same as Udf01.dll's dependent.dll file.</span><span class="sxs-lookup"><span data-stu-id="96a99-p109">The Udf02.dll file has a dependency on the dependent.dll file. Udf01.dll's dependency and Udf02.dll's dependency share the same name. But Udf02.dll's dependent.dll file is not the same as Udf01.dll's dependent.dll file.</span></span>
    
  
<span data-ttu-id="96a99-159">Assume the following flow:</span><span class="sxs-lookup"><span data-stu-id="96a99-159">Assume the following flow:</span></span>
  
    
    

1. <span data-ttu-id="96a99-p110">Udf01.dll is the first DLL to be loaded. Dienste für Excel-Berechnungen looks for dependent.dll and loads Udf01.dll's dependency, which in this case is dependent.dll.</span><span class="sxs-lookup"><span data-stu-id="96a99-p110">Udf01.dll is the first DLL to be loaded. Excel Calculation Services looks for dependent.dll and loads Udf01.dll's dependency, which in this case is dependent.dll.</span></span> 
    
  
2. <span data-ttu-id="96a99-p111">Udf02.dll is loaded after Udf01.dll. Dienste für Excel-Berechnungen sees that Udf02.dll depends on dependent.dll. However, a DLL with the name "dependent.dll" is already loaded. Therefore, Udf02.dll's dependent.dll file is not loaded, and the currently loaded dependent.dll file is used as the dependency.</span><span class="sxs-lookup"><span data-stu-id="96a99-p111">Udf02.dll is loaded after Udf01.dll. Excel Calculation Services sees that Udf02.dll depends on dependent.dll. However, a DLL with the name "dependent.dll" is already loaded. Therefore, Udf02.dll's dependent.dll file is not loaded, and the currently loaded dependent.dll file is used as the dependency.</span></span>
    
  
<span data-ttu-id="96a99-166">As a result, the objectin this case, the dependent.dll file that Udf02.dll needsis not loaded into memory.</span><span class="sxs-lookup"><span data-stu-id="96a99-166">As a result, the object—in this case, the dependent.dll file that Udf02.dll needs—is not loaded into memory.</span></span>
  
    
    
<span data-ttu-id="96a99-167">To avoid name collision, we recommend that you strongly name your dependencies, and name them uniquely.</span><span class="sxs-lookup"><span data-stu-id="96a99-167">To avoid name collision, we recommend that you strongly name your dependencies, and name them uniquely.</span></span>
  
    
    

## <a name="general"></a><span data-ttu-id="96a99-168">Allgemein</span><span class="sxs-lookup"><span data-stu-id="96a99-168">General</span></span>


### <a name="naming-managed-code-dlls"></a><span data-ttu-id="96a99-169">Naming Managed-Code DLLs</span><span class="sxs-lookup"><span data-stu-id="96a99-169">Naming Managed-Code DLLs</span></span>

<span data-ttu-id="96a99-170">To ensure that your assembly names are unique, use the fully qualified class name, following the  [Namespace Naming Guidelines](http://msdn.microsoft.com/library/c08bc0d8-9b3a-4564-9af6-71699f62e00d.aspx).</span><span class="sxs-lookup"><span data-stu-id="96a99-170">To ensure that your assembly names are unique, use the fully qualified class name, following the  [Namespace Naming Guidelines](http://msdn.microsoft.com/library/c08bc0d8-9b3a-4564-9af6-71699f62e00d.aspx).</span></span>
  
    
    
<span data-ttu-id="96a99-171">For example, use CompanyName.Hierarchichal.Namespace.ClassName instead ofNamespace.ClassName.</span><span class="sxs-lookup"><span data-stu-id="96a99-171">For example, use CompanyName.Hierarchichal.Namespace.ClassName instead ofNamespace.ClassName.</span></span> 
  
    
    

## <a name="see-also"></a><span data-ttu-id="96a99-172">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="96a99-172">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="96a99-173">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="96a99-173">Tasks</span></span>


  
    
    
 [<span data-ttu-id="96a99-174">How to: Trust a Location</span><span class="sxs-lookup"><span data-stu-id="96a99-174">How to: Trust a Location</span></span>](how-to-trust-a-location.md)
#### <a name="concepts"></a><span data-ttu-id="96a99-175">Konzepte</span><span class="sxs-lookup"><span data-stu-id="96a99-175">Concepts</span></span>


  
    
    
 [<span data-ttu-id="96a99-176">Excel Services-Architektur</span><span class="sxs-lookup"><span data-stu-id="96a99-176">Excel Services Architecture</span></span>](excel-services-architecture.md)
  
    
    
 [<span data-ttu-id="96a99-177">Accessing the SOAP API</span><span class="sxs-lookup"><span data-stu-id="96a99-177">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
  
    
    
 [<span data-ttu-id="96a99-178">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="96a99-178">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="96a99-179">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="96a99-179">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
  
    
    
 [<span data-ttu-id="96a99-180">Excel Services - Blogs, Foren und Ressourcen</span><span class="sxs-lookup"><span data-stu-id="96a99-180">Excel Services Blogs, Forums, and Resources</span></span>](excel-services-blogs-forums-and-resources.md)
