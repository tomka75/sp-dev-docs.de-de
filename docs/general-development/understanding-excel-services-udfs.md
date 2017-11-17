---
title: Grundlegendes zu Excel Services-UDFs
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a1567278-fac4-4b3b-a814-56f2376c1217
ms.openlocfilehash: 175e916ef29f1211cc158634a883020da444b49b
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="understanding-excel-services-udfs"></a><span data-ttu-id="da91c-102">Grundlegendes zu Excel Services-UDFs</span><span class="sxs-lookup"><span data-stu-id="da91c-102">Understanding Excel Services UDFs</span></span>

<span data-ttu-id="da91c-p101">User-defined functions (UDFs) are custom functions that extend the calculation and data-import capabilities of Excel. Developers create custom calculation packages to provide:</span><span class="sxs-lookup"><span data-stu-id="da91c-p101">User-defined functions (UDFs) are custom functions that extend the calculation and data-import capabilities of Excel. Developers create custom calculation packages to provide:</span></span>
  
    
    


- <span data-ttu-id="da91c-105">Functions that are not built into Excel.</span><span class="sxs-lookup"><span data-stu-id="da91c-105">Functions that are not built into Excel.</span></span>
    
  
- <span data-ttu-id="da91c-106">Custom implementations to built-in functions.</span><span class="sxs-lookup"><span data-stu-id="da91c-106">Custom implementations to built-in functions.</span></span>
    
  
- <span data-ttu-id="da91c-107">Custom data feeds for legacy or unsupported data sources, and application-specific data flows.</span><span class="sxs-lookup"><span data-stu-id="da91c-107">Custom data feeds for legacy or unsupported data sources, and application-specific data flows.</span></span>
    
  

<span data-ttu-id="da91c-108">Users who create workbooks can call UDFs from a cell through formulasfor example, "=MyUdf(A1*3.42)"just like they call built-in functions.</span><span class="sxs-lookup"><span data-stu-id="da91c-108">Users who create workbooks can call UDFs from a cell through formulas—for example, "=MyUdf(A1*3.42)"—just like they call built-in functions.</span></span>
  
    
    

<span data-ttu-id="da91c-p102">Excel Services UDFs give you the ability to use formulas in cells to call custom functions written in managed code and deployed to Microsoft SharePoint Server 2010. You can create UDFs to:</span><span class="sxs-lookup"><span data-stu-id="da91c-p102">Excel Services UDFs give you the ability to use formulas in cells to call custom functions written in managed code and deployed to Microsoft SharePoint Server 2010. You can create UDFs to:</span></span>
- <span data-ttu-id="da91c-111">Call custom mathematical functions.</span><span class="sxs-lookup"><span data-stu-id="da91c-111">Call custom mathematical functions.</span></span>
    
  
- <span data-ttu-id="da91c-112">Get data from custom data sources into worksheets.</span><span class="sxs-lookup"><span data-stu-id="da91c-112">Get data from custom data sources into worksheets.</span></span>
    
  
- <span data-ttu-id="da91c-113">Call Web services from the UDFs.</span><span class="sxs-lookup"><span data-stu-id="da91c-113">Call Web services from the UDFs.</span></span>
    
  

## <a name="creating-managed-code-udfs"></a><span data-ttu-id="da91c-114">Creating Managed-Code UDFs</span><span class="sxs-lookup"><span data-stu-id="da91c-114">Creating Managed-Code UDFs</span></span>

<span data-ttu-id="da91c-p103">An easy way to create an Excel Services managed-code UDF is to use the Microsoft Visual Studio 2005 class library template. You will need to reference the Excel Services UDF dynamic link library (DLL), named Microsoft.Office.Excel.Server.Udf.dll, in your managed-code UDF project.</span><span class="sxs-lookup"><span data-stu-id="da91c-p103">An easy way to create an Excel Services managed-code UDF is to use the Microsoft Visual Studio 2005 class library template. You will need to reference the Excel Services UDF dynamic link library (DLL), named Microsoft.Office.Excel.Server.Udf.dll, in your managed-code UDF project.</span></span> 
  
    
    
<span data-ttu-id="da91c-p104">Microsoft.Office.Excel.Server.Udf.dll has been compiled using Microsoft .NET Framework 2.0. If you use Visual Studio 2003 to create your managed-code UDF, you will not be able to reference Microsoft.Office.Excel.Server.Udf.dll. It is not possible for an assembly created with an older version of the .NET Framework to reference an assembly created with .NET Framework 2.0.</span><span class="sxs-lookup"><span data-stu-id="da91c-p104">Microsoft.Office.Excel.Server.Udf.dll has been compiled using Microsoft .NET Framework 2.0. If you use Visual Studio 2003 to create your managed-code UDF, you will not be able to reference Microsoft.Office.Excel.Server.Udf.dll. It is not possible for an assembly created with an older version of the .NET Framework to reference an assembly created with .NET Framework 2.0.</span></span>
  
    
    

### <a name="required-attributes"></a><span data-ttu-id="da91c-120">Required Attributes</span><span class="sxs-lookup"><span data-stu-id="da91c-120">Required Attributes</span></span>

<span data-ttu-id="da91c-p105">To use custom functions in a class as an Excel Services UDF class, you must mark your UDF class with the **Microsoft.Office.Excel.Server.Udf.UdfClass** attribute. Any classes that are not marked with this attribute in the UDF assembly will be ignored by Dienste für Excel-Berechnungen. They are not considered to be Excel Services UDF classes.</span><span class="sxs-lookup"><span data-stu-id="da91c-p105">To use custom functions in a class as an Excel Services UDF class, you must mark your UDF class with the **Microsoft.Office.Excel.Server.Udf.UdfClass** attribute. Any classes that are not marked with this attribute in the UDF assembly will be ignored by Excel Calculation Services. They are not considered to be Excel Services UDF classes.</span></span>
  
    
    
<span data-ttu-id="da91c-p106">To use custom functions in a class as Excel Services UDF methods, you must mark your UDF methods with the **Microsoft.Office.Excel.Server.Udf.UdfMethod** attribute. Any methods that are not marked with this attribute in the UDF assembly will be ignored because they are not considered to be Excel Services UDF methods.</span><span class="sxs-lookup"><span data-stu-id="da91c-p106">To use custom functions in a class as Excel Services UDF methods, you must mark your UDF methods with the **Microsoft.Office.Excel.Server.Udf.UdfMethod** attribute. Any methods that are not marked with this attribute in the UDF assembly will be ignored because they are not considered to be Excel Services UDF methods.</span></span>
  
    
    
<span data-ttu-id="da91c-p107">The **Microsoft.Office.Excel.Server.Udf.UdfMethod**attribute has an **IsVolatile** property. You use the **IsVolatile** property to specify a UDF method as volatile or nonvolatile. The **IsVolatile** property takes a Boolean value. The default value is **false**, which means that particular UDF method is nonvolatile.</span><span class="sxs-lookup"><span data-stu-id="da91c-p107">The **Microsoft.Office.Excel.Server.Udf.UdfMethod**attribute has an **IsVolatile** property. You use the **IsVolatile** property to specify a UDF method as volatile or nonvolatile. The **IsVolatile** property takes a Boolean value. The default value is **false**, which means that particular UDF method is nonvolatile.</span></span>
  
    
    

### <a name="location-of-microsoftofficeexcelserverudfdll"></a><span data-ttu-id="da91c-130">Location of Microsoft.Office.Excel.Server.Udf.dll</span><span class="sxs-lookup"><span data-stu-id="da91c-130">Location of Microsoft.Office.Excel.Server.Udf.dll</span></span>

<span data-ttu-id="da91c-131">On the computer where you have installed SharePoint Server 2010, you can find a copy of Microsoft.Office.Excel.Server.Udf.dll at:</span><span class="sxs-lookup"><span data-stu-id="da91c-131">On the computer where you have installed SharePoint Server 2010, you can find a copy of Microsoft.Office.Excel.Server.Udf.dll at:</span></span>
  
    
    
 `[drive:]\\Program Files\\Common Files\\Microsoft Shared\\web server extensions\\14\\ISAPI`
  
    
    

## <a name="deployment-and-security"></a><span data-ttu-id="da91c-132">Deployment and Security</span><span class="sxs-lookup"><span data-stu-id="da91c-132">Deployment and Security</span></span>


### <a name="deployment-location-type"></a><span data-ttu-id="da91c-133">Deployment Location Type</span><span class="sxs-lookup"><span data-stu-id="da91c-133">Deployment Location Type</span></span>

<span data-ttu-id="da91c-p108">UDF assemblies can reside in a local directory, global assembly cache, or network share. In a farm scenario, the local directory path must be identical across the farm.</span><span class="sxs-lookup"><span data-stu-id="da91c-p108">UDF assemblies can reside in a local directory, global assembly cache, or network share. In a farm scenario, the local directory path must be identical across the farm.</span></span>
  
    
    

### <a name="identification-of-udf-assemblies"></a><span data-ttu-id="da91c-136">Identification of UDF Assemblies</span><span class="sxs-lookup"><span data-stu-id="da91c-136">Identification of UDF Assemblies</span></span>

<span data-ttu-id="da91c-137">You can expose the identity of a UDF assembly by using the full path or strong name of the assembly for Dienste für Excel-Berechnungen to call.</span><span class="sxs-lookup"><span data-stu-id="da91c-137">You can expose the identity of a UDF assembly by using the full path or strong name of the assembly for Excel Calculation Services to call.</span></span> 
  
    
    
<span data-ttu-id="da91c-138">For example, you can use:</span><span class="sxs-lookup"><span data-stu-id="da91c-138">For example, you can use:</span></span>
  
    
    

- <span data-ttu-id="da91c-139">C:\\UDFs\\MySampleUdf.dll</span><span class="sxs-lookup"><span data-stu-id="da91c-139">C:\UDFs\MySampleUdf.dll</span></span> 
    
  
- <span data-ttu-id="da91c-140">\\\\MyNetworkServer\\UDFs\\MySampleUdf.dll</span><span class="sxs-lookup"><span data-stu-id="da91c-140">\\MyNetworkServer\UDFs\MySampleUdf.dll</span></span>
    
  
- <span data-ttu-id="da91c-141">CompanyName.Hierarchichal.MyUdfNamespace.MyUdfClassName.dll, Version=1.1.0.0, Culture=en, PublicKeyToken=e8123117d7ba9ae38</span><span class="sxs-lookup"><span data-stu-id="da91c-141">CompanyName.Hierarchichal.MyUdfNamespace.MyUdfClassName.dll, Version=1.1.0.0, Culture=en, PublicKeyToken=e8123117d7ba9ae38</span></span>
    
  

### <a name="enabling-udf-assemblies"></a><span data-ttu-id="da91c-142">Enabling UDF Assemblies</span><span class="sxs-lookup"><span data-stu-id="da91c-142">Enabling UDF Assemblies</span></span>

<span data-ttu-id="da91c-143">UDF assemblies are disabled by default.</span><span class="sxs-lookup"><span data-stu-id="da91c-143">UDF assemblies are disabled by default.</span></span> 
  
    
    
<span data-ttu-id="da91c-144">Jeder vertrauenswürdige Excel Services-Speicherort verfügt über ein **AllowUdfs**-Flag.</span><span class="sxs-lookup"><span data-stu-id="da91c-144">Each Excel Services trusted location has an **AllowUdfs** flag.</span></span>
  
    
    

> <span data-ttu-id="da91c-145">**Hinweis:** Das **AllowUdfs**-Flag wird durch die Option **Benutzerdefinierte Funktionen sind zugelassen** auf der Seite „Vertrauenswürdige Dateispeicherorte von Excel Services“ bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="da91c-145">**Note** The **AllowUdfs** flag is denoted by the **User-defined functions allowed** option on the Excel Services Trusted File Locations page.</span></span> <span data-ttu-id="da91c-146">Informationen zum Navigieren zur Seite „Vertrauenswürdige Dateispeicherorte“ finden Sie in [Schritt 3: Bereitstellen und Aktivieren von UDFs](step-3-deploying-and-enabling-udfs.md).</span><span class="sxs-lookup"><span data-stu-id="da91c-146">The AllowUdfs flag is denoted by the User-defined functions allowed option on the esesshort  Trusted File Locations page. To learn how to navigate to the Trusted File Locations page, see [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md).</span></span> 
  
    
    

<span data-ttu-id="da91c-p110">The default **AllowUdfs** value is **false**. If the **AllowUdfs** value is set to **false** in a particular trusted location, the workbooks in that trusted location are not allowed to call UDFs.</span><span class="sxs-lookup"><span data-stu-id="da91c-p110">The default **AllowUdfs** value is **false**. If the **AllowUdfs** value is set to **false** in a particular trusted location, the workbooks in that trusted location are not allowed to call UDFs.</span></span>
  
    
    
<span data-ttu-id="da91c-149">In order to allow UDFs to be called from a specific trusted location, you set the **AllowUdfs** value to **true**.</span><span class="sxs-lookup"><span data-stu-id="da91c-149">In order to allow UDFs to be called from a specific trusted location, you set the **AllowUdfs** value to **true**.</span></span>
  
    
    
<span data-ttu-id="da91c-p111">If the **AllowUdfs** value is **false** when a session is started on a workbook that has UDF calls in this trusted location, the UDF calls will fail. If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session, after the configuration database has been updated.</span><span class="sxs-lookup"><span data-stu-id="da91c-p111">If the **AllowUdfs** value is **false** when a session is started on a workbook that has UDF calls in this trusted location, the UDF calls will fail. If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session, after the configuration database has been updated.</span></span>
  
    
    

### <a name="allowing-udf-assemblies-to-run"></a><span data-ttu-id="da91c-153">Allowing UDF Assemblies to Run</span><span class="sxs-lookup"><span data-stu-id="da91c-153">Allowing UDF Assemblies to Run</span></span>

<span data-ttu-id="da91c-154">If administrators want to allow UDF assemblies to run, they have to register all UDF assemblies, and enable workbooks to call UDFs by setting the **AllowUdfs** flag to **true** in the trusted locations.</span><span class="sxs-lookup"><span data-stu-id="da91c-154">If administrators want to allow UDF assemblies to run, they have to register all UDF assemblies, and enable workbooks to call UDFs by setting the **AllowUdfs** flag to **true** in the trusted locations.</span></span>
  
    
    

### <a name="reloading-a-udf-assembly"></a><span data-ttu-id="da91c-155">Reloading a UDF Assembly</span><span class="sxs-lookup"><span data-stu-id="da91c-155">Reloading a UDF Assembly</span></span>

<span data-ttu-id="da91c-156">Um ein UDF-Assembly erneut zu laden, führen Sie **iisreset** aus oder starten Sie die Anwendungsdomäne Dienste für Excel-Berechnungen neu.</span><span class="sxs-lookup"><span data-stu-id="da91c-156">To reload a UDF assembly, you can run **iisreset** or restart the Excel Calculation Services application domain.</span></span>
  
    
    

> <span data-ttu-id="da91c-157">**Vorsicht:** Durch das Zurücksetzen von IIS werden alle laufenden Sitzungen beendet.</span><span class="sxs-lookup"><span data-stu-id="da91c-157">**Caution** Resetting IIS will end all current sessions.</span></span> <span data-ttu-id="da91c-158">Weitere Informationen finden Sie unter [Vorgehensweise: Aktivieren von UDFs](how-to-enable-udfs.md).</span><span class="sxs-lookup"><span data-stu-id="da91c-158">For more information, see  [How to: Enable UDFs](how-to-enable-udfs.md).</span></span> 
  
    
    

<span data-ttu-id="da91c-159">Weitere Informationen finden Sie unter [Entladen einer Anwendung aus dem Speicher](http://go.microsoft.com/fwlink/?LinkId=65706) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/csvr2002/htm/cs_mmc_administering_myhj.asp).</span><span class="sxs-lookup"><span data-stu-id="da91c-159">For more information, see  [Unloading an Application from Memory](http://go.microsoft.com/fwlink/?LinkId=65706) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/csvr2002/htm/cs_mmc_administering_myhj.asp).</span></span>
  
    
    

### <a name="default-code-access-security-permission-for-udf-assemblies"></a><span data-ttu-id="da91c-160">Default Code Access Security Permission for UDF Assemblies</span><span class="sxs-lookup"><span data-stu-id="da91c-160">Default Code Access Security Permission for UDF Assemblies</span></span>

<span data-ttu-id="da91c-161">By default, UDF assemblies run with full trust.</span><span class="sxs-lookup"><span data-stu-id="da91c-161">By default, UDF assemblies run with full trust.</span></span> 
  
    
    

### <a name="restricting-code-access-security-permission-for-udf-assemblies"></a><span data-ttu-id="da91c-162">Restricting Code Access Security Permission for UDF Assemblies</span><span class="sxs-lookup"><span data-stu-id="da91c-162">Restricting Code Access Security Permission for UDF Assemblies</span></span>

<span data-ttu-id="da91c-p113">If you do not want a particular UDF assembly to run with full trust, you must explicitly restrict code access security permission for that UDF assembly. You can configure the code groups and restrict permission by using the .NET Framework 2.0 Configuration tool.</span><span class="sxs-lookup"><span data-stu-id="da91c-p113">If you do not want a particular UDF assembly to run with full trust, you must explicitly restrict code access security permission for that UDF assembly. You can configure the code groups and restrict permission by using the .NET Framework 2.0 Configuration tool.</span></span> 
  
    
    
<span data-ttu-id="da91c-165">Developers can also use the **RequestMinimum** and **RequestOptional** methods in their code to ensure that their UDF assemblies don't get more permission than they require.</span><span class="sxs-lookup"><span data-stu-id="da91c-165">Developers can also use the **RequestMinimum** and **RequestOptional** methods in their code to ensure that their UDF assemblies don't get more permission than they require.</span></span>
  
    
    
<span data-ttu-id="da91c-166">For more information about configuring code groups, as well as the **RequestMinimum** and **RequestOptional** methods, see the following articles on MSDN:</span><span class="sxs-lookup"><span data-stu-id="da91c-166">For more information about configuring code groups, as well as the **RequestMinimum** and **RequestOptional** methods, see the following articles on MSDN:</span></span>
  
    
    

-  <span data-ttu-id="da91c-167">[Configuring Code Groups Using the .NET Framework Configuration Tool](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpguide/html/cpconUsingNETConfigurationToolToWorkWithCodeGroups.asp?frame=true) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpguide/html/cpconUsingNETConfigurationToolToWorkWithCodeGroups.asp?frame=true)</span><span class="sxs-lookup"><span data-stu-id="da91c-167">[Configuring Code Groups Using the .NET Framework Configuration Tool](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpguide/html/cpconUsingNETConfigurationToolToWorkWithCodeGroups.asp?frame=true) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpguide/html/cpconUsingNETConfigurationToolToWorkWithCodeGroups.asp?frame=true)</span></span>
    
  
-  <span data-ttu-id="da91c-168">[Code Access Security in Practice](http://go.microsoft.com/fwlink/?LinkId=65465) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnnetsec/html/thcmch08.asp)</span><span class="sxs-lookup"><span data-stu-id="da91c-168">[Code Access Security in Practice](http://go.microsoft.com/fwlink/?LinkId=65465) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnnetsec/html/thcmch08.asp)</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="da91c-169">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="da91c-169">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="da91c-170">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="da91c-170">Tasks</span></span>


  
    
    
 [<span data-ttu-id="da91c-171">How to: Create a UDF That Calls a Web Service</span><span class="sxs-lookup"><span data-stu-id="da91c-171">How to: Create a UDF That Calls a Web Service</span></span>](how-to-create-a-udf-that-calls-a-web-service.md)
  
    
    
 [<span data-ttu-id="da91c-172">How to: Trust a Location</span><span class="sxs-lookup"><span data-stu-id="da91c-172">How to: Trust a Location</span></span>](how-to-trust-a-location.md)
  
    
    
 [<span data-ttu-id="da91c-173">How to: Catch Exceptions</span><span class="sxs-lookup"><span data-stu-id="da91c-173">How to: Catch Exceptions</span></span>](how-to-catch-exceptions.md)
  
    
    
 [<span data-ttu-id="da91c-174">How to: Enable UDFs</span><span class="sxs-lookup"><span data-stu-id="da91c-174">How to: Enable UDFs</span></span>](how-to-enable-udfs.md)
#### <a name="concepts"></a><span data-ttu-id="da91c-175">Konzepte</span><span class="sxs-lookup"><span data-stu-id="da91c-175">Concepts</span></span>


  
    
    
 [<span data-ttu-id="da91c-176">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="da91c-176">Walkthrough: Developing a Managed-Code UDF</span></span>](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [<span data-ttu-id="da91c-177">Frequently Asked Questions About Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="da91c-177">Frequently Asked Questions About Excel Services UDFs</span></span>](frequently-asked-questions-about-excel-services-udfs.md)
  
    
    
 [<span data-ttu-id="da91c-178">Excel Services-Architektur</span><span class="sxs-lookup"><span data-stu-id="da91c-178">Excel Services Architecture</span></span>](excel-services-architecture.md)
  
    
    
 [<span data-ttu-id="da91c-179">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="da91c-179">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="da91c-180">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="da91c-180">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
  
    
    
 [<span data-ttu-id="da91c-181">Excel Services Best Practices</span><span class="sxs-lookup"><span data-stu-id="da91c-181">Excel Services Best Practices</span></span>](excel-services-best-practices.md)
