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
# <a name="excel-services-best-practices"></a>Bewährte Methoden für Excel Services

This topic contains a list of best-practice recommendations for working with Excel Services.
  
    
    


## <a name="mitigating-threats"></a>Mitigating Threats


### <a name="anonymous-access-and-information-disclosure"></a>Anonymous Access and Information Disclosure

The following settings combination gives anonymous users access to any files in the share to which the process account has access. Therefore, the following combination of settings is not recommended, because of the possibility of information disclosure:
  
    
    

- Anonymous access to Microsoft SharePoint Foundation is turned on.
    
  
- Sie verfügen über einen vertrauenswürdigen UNC-Speicherort und das **Prozesskonto** ist aktiviert.
    
  

> **Hinweis:** Das **Prozesskonto** ist eine globale Einstellung von Excel Services, die Auswirkung auf alle vertrauenswürdigen Speicherorte hat.
  
    
    


### <a name="to-view-the-process-account-option"></a>So zeigen Sie die Option „Prozesskonto“ an


1. On the **Start** menu, click **All Programs**.
    
  
2. Point to **Microsoft SharePoint 2010 Products**, and then click **SharePoint Central Administration**.
    
  
3. Under **Application Management**, click **Manage service applications**.
    
  
4. On the Manage Service Applications page, click **Excel Services Application**.
    
  
5. On the **Excel Services Application** page, click **Global Settings**.
    
  
6. In the **Security** section, look under **File Access Method** for the **Process account** option.
    
  

### <a name="denial-of-service-attack"></a>Denial of Service Attack

In a denial of service attack against a Web service, an attacker generates very large, individual requests against the Web service. The purpose is to attempt to exploit the limits of one or more Web service input values.
  
    
    
We recommend that you use the Microsoft Internet Information Services (IIS) setting to set the maximum request size for the Web service.
  
    
    
Use the **maxRequestLength** attribute in the **httpRuntime** element in the **system.web** element to prevent denial of service attacks that are caused by users posting large files to the server. The default size is 4096 KB (4 MB).
  
    
    
Weitere Informationen finden Sie unter [\<httpRuntime\>-Element](http://msdn.microsoft.com/library/e9b81350-8aaf-47cc-9843-5f7d0c59f369.aspx) und [\<maxRequestLength\>-Element](http://msdn.microsoft.com/library/fd52b2c5-5014-4e6f-b869-4ea666dc83d6.aspx).
  
    
    

### <a name="sniffing-between-the-calling-application-and-the-web-service-computer"></a>Ermitteln zwischen der aufrufenden Anwendung und dem Webdienstcomputer

If the calling application and Excel Web Services are deployed to different computers, an attacker can listen to the network traffic for data transfer between the calling application and the Web service. This threat is also called "sniffing" or "eavesdropping."
  
    
    
To help mitigate this threat, we recommend that you:
  
    
    

- Use Secure Sockets Layer (SSL) to set up a secure channel to protect data transfer between the client and the server. The SSL protocol helps to protect data against packet sniffing by anyone with physical access to the network.
    
  
- Physically protect the relevant network if a custom application using Excel Web Services is running in a confined networkfor example, if Excel Web Services is deployed on a Web front-end computer within the enterprise.
    
  
For more information, see  [Securing Your Network](http://msdn.microsoft.com/library/af62ece0-0dd7-4b8e-ad12-4d13f2d60816.aspx) and [SOAP Security](http://msdn.microsoft.com/en-us/library/aa912494.aspx).
  
    
    
For information about Excel Services topology, scalability, performance, and security, see the Microsoft SharePoint Server 2010 TechCenter.
  
    
    

### <a name="spoofing"></a>Spoofing

We recommend that you use SSL to help mitigate the threats of hijacked Web service Internet Protocol (IP) addresses and ports, and to help prevent attackers from receiving requests and replying on behalf of the Web service.
  
    
    
The SSL certificate is matched against a few properties, one of which is the IP address from which the message is coming. The attacker cannot spoof the IP address if it does not have the Web service SSL certificate.
  
    
    
For more information, see  [Securing Your Network](http://msdn.microsoft.com/library/af62ece0-0dd7-4b8e-ad12-4d13f2d60816.aspx).
  
    
    

## <a name="excel-services-user-defined-functions-udfs"></a>Excel Services User-Defined Functions (UDFs)


### <a name="strong-name-dependencies"></a>Strong Name Dependencies

In some cases, a user-defined function (UDF) assembly depends on other assemblies that are deployed with it. These dependent DLLs load successfully if they are in the global assembly cache, or if they are located in the same folder as the UDF assembly.
  
    
    
In the latter case, however, it is possible for the load to fail if Dienste für Excel-Berechnungen has already loaded another assembly with the same name. (It fails either because the assembly is not strongly named, or because another version with the same name has been deployed and loaded.)
  
    
    
Consider the following scenario, with the following directory structure:
  
    
    

1. C:\\Udfs\\Udf01
    
    The Udf01 folder contains:
    
  - Udf01.dll 
    
  
  - dependent.dll (not strongly named)
    
  

    The Udf01.dll file has a dependency on the dependent.dll file.
    
  
2. C:\\Udfs\\Udf02
    
    The Udf02 folder contains:
    
  - Udf02.dll (which depends on Interop.dll)
    
  
  - dependent.dll (which is not strongly named)
    
  

    The Udf02.dll file has a dependency on the dependent.dll file. Udf01.dll's dependency and Udf02.dll's dependency share the same name. But Udf02.dll's dependent.dll file is not the same as Udf01.dll's dependent.dll file.
    
  
Assume the following flow:
  
    
    

1. Udf01.dll is the first DLL to be loaded. Dienste für Excel-Berechnungen looks for dependent.dll and loads Udf01.dll's dependency, which in this case is dependent.dll. 
    
  
2. Udf02.dll is loaded after Udf01.dll. Dienste für Excel-Berechnungen sees that Udf02.dll depends on dependent.dll. However, a DLL with the name "dependent.dll" is already loaded. Therefore, Udf02.dll's dependent.dll file is not loaded, and the currently loaded dependent.dll file is used as the dependency.
    
  
As a result, the objectin this case, the dependent.dll file that Udf02.dll needsis not loaded into memory.
  
    
    
To avoid name collision, we recommend that you strongly name your dependencies, and name them uniquely.
  
    
    

## <a name="general"></a>Allgemein


### <a name="naming-managed-code-dlls"></a>Naming Managed-Code DLLs

To ensure that your assembly names are unique, use the fully qualified class name, following the  [Namespace Naming Guidelines](http://msdn.microsoft.com/library/c08bc0d8-9b3a-4564-9af6-71699f62e00d.aspx).
  
    
    
For example, use CompanyName.Hierarchichal.Namespace.ClassName instead ofNamespace.ClassName. 
  
    
    

## <a name="see-also"></a>Siehe auch


#### <a name="tasks"></a>Aufgaben


  
    
    
 [How to: Trust a Location](how-to-trust-a-location.md)
#### <a name="concepts"></a>Konzepte


  
    
    
 [Excel Services-Architektur](excel-services-architecture.md)
  
    
    
 [Accessing the SOAP API](accessing-the-soap-api.md)
  
    
    
 [Excel Services Alerts](excel-services-alerts.md)
  
    
    
 [Excel Services Known Issues and Tips](excel-services-known-issues-and-tips.md)
  
    
    
 [Excel Services - Blogs, Foren und Ressourcen](excel-services-blogs-forums-and-resources.md)