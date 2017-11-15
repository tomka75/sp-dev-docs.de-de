---
title: Zugriff auf die SOAP-API
ms.date: 09/25/2017
keywords: soap
f1_keywords: soap
ms.prod: sharepoint
ms.assetid: 36e8e3d5-83ac-4bd3-b556-1af132add3eb
ms.openlocfilehash: 41b6656034d9e67fedca44684444bfb73d667e02
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="accessing-the-soap-api"></a><span data-ttu-id="3f42f-103">Zugriff auf die SOAP-API</span><span class="sxs-lookup"><span data-stu-id="3f42f-103">Accessing the SOAP API</span></span>

<span data-ttu-id="3f42f-p101">Excel Web Services verwendet SOAP (Simple Object Access-Protokoll) über HTTP und dient als Kommunikationsschnittstelle zwischen Clientprogrammen und Excel Services. Der Webdienst besteht aus Methoden und einer Reihe komplexer Objekte, mit denen Sie auf die gesamten Funktionen von Excel Web Services zugreifen können. Zum Aufrufen dieses Diensts müssen Sie Web Services Description Language (WSDL) von Excel Web Services verwenden.</span><span class="sxs-lookup"><span data-stu-id="3f42f-p101">Excel Web Services uses Simple Object Access Protocol (SOAP) over HTTP and acts as a communications interface between client programs and Excel Services. The Web service consists of methods and a set of complex type objects that you can use to access the complete functionality of Excel Web Services. To call the service, you must reference the Excel Web Services Web Services Description Language (WSDL).</span></span>
  
    
    


## <a name="referencing-the-wsdl"></a><span data-ttu-id="3f42f-107">Verwenden von WSDL</span><span class="sxs-lookup"><span data-stu-id="3f42f-107">Referencing the WSDL</span></span>

<span data-ttu-id="3f42f-p102">Für den erfolgreichen Aufruf eines Webdiensts müssen Sie wissen, wie auf den Dienst zugegriffen wird, welche Vorgänge von dem Dienst unterstützt werden, welche Parameter von dem Dienst erwartet werden und was von dem Dienst zurückgegeben wird. WSDL stellt diese Informationen in einem XML-Dokument bereit, das von einem Computer gelesen oder verarbeitet werden kann.</span><span class="sxs-lookup"><span data-stu-id="3f42f-p102">To call a Web service successfully, you must know how to access the service, what operations the service supports, what parameters the service expects, and what the service returns. WSDL provides this information in an XML document that can be read or processed by a computer.</span></span>
  
    
    
<span data-ttu-id="3f42f-p103">Der Zugriff auf WSDL für den Endpunkt von Excel Web Services erfolgt über  `ExcelServices.asmx?wsdl`. WSDL kann von Development Kits verwendet werden, die SOAP und Webdienste unterstützen, wie z. B. das Microsoft .NET Framework SDK.</span><span class="sxs-lookup"><span data-stu-id="3f42f-p103">The WSDL for the Excel Web Services endpoint is accessed through  `ExcelServices.asmx?wsdl`. WSDL can be consumed by development kits that support SOAP and Web services, such as the Microsoft .NET Framework SDK.</span></span>
  
    
    
<span data-ttu-id="3f42f-112">Im folgenden Beispiel wird das Format der URL zur WSDL-Datei von Excel Web Services gezeigt:</span><span class="sxs-lookup"><span data-stu-id="3f42f-112">The following example shows the format of the URL to the Excel Web Services WSDL file:</span></span>
  
    
    
 `http://<server>/<customsite>/_vti_bin/excelservice.asmx?WSDL`
  
    
    
<span data-ttu-id="3f42f-113">Wenn keine benutzerdefinierte Website vorhanden ist, kann temporär die folgende URL verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="3f42f-113">If you do not have a custom site, you can use the following URL temporarily:</span></span>
  
    
    
 `http://<server>/_vti_bin/excelservice.asmx?WSDL`
  
    
    
<span data-ttu-id="3f42f-114">Es wird empfohlen, eine benutzerdefinierte Website zu erstellen und dann die URL, die die benutzerdefinierte Website enthält, im URL-Format zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="3f42f-114">It is recommended that you create a custom site, and then use the URL that includes the custom site in the URL format.</span></span>
  
    
    
<span data-ttu-id="3f42f-115">In der folgenden Tabelle werden die jeweiligen Elemente in der URL erläutert.</span><span class="sxs-lookup"><span data-stu-id="3f42f-115">The following table describes each element in the URL.</span></span>
  
    
    


|<span data-ttu-id="3f42f-116">**URL-Element**</span><span class="sxs-lookup"><span data-stu-id="3f42f-116">******URL element******</span></span>|<span data-ttu-id="3f42f-117">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="3f42f-117">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="3f42f-118">_server_</span><span class="sxs-lookup"><span data-stu-id="3f42f-118">_server_</span></span> <br/> |<span data-ttu-id="3f42f-119">Der Name des Servers, auf dem Microsoft SharePoint Server 2010 bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="3f42f-119">The name of the server on which Microsoft SharePoint Server 2010 is deployed.</span></span>  <br/> |
| <span data-ttu-id="3f42f-120">_customsite_</span><span class="sxs-lookup"><span data-stu-id="3f42f-120">_customsite_</span></span> <br/> |<span data-ttu-id="3f42f-121">Eine benutzerdefinierte SharePoint Server 2010-Website, die vom Serveradministrator erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="3f42f-121">A custom SharePoint Server 2010 site that the server administrator creates.</span></span>  <br/> |
| <span data-ttu-id="3f42f-122">_<endpointname>.asmx_</span><span class="sxs-lookup"><span data-stu-id="3f42f-122">_<endpointname>.asmx_</span></span> <br/> |<span data-ttu-id="3f42f-p104">Der Name des Webdienstendpunkts. Für Excel Web Services ist dies  `ExcelService.asmx`.</span><span class="sxs-lookup"><span data-stu-id="3f42f-p104">The name of the Web service endpoint. For Excel Web Services, it is  `ExcelService.asmx`.  </span></span><br/> |
   
<span data-ttu-id="3f42f-125">Weitere Informationen über das WSDL-Format finden Sie in der World Wide Web Consortium (W3C) WSDL-Spezifikation unter http://www.w3.org/TR/wsdl.</span><span class="sxs-lookup"><span data-stu-id="3f42f-125">For more information about the WSDL format, see the World Wide Web Consortium (W3C) WSDL specification at http://www.w3.org/TR/wsdl.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="3f42f-126">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="3f42f-126">See also</span></span>


#### <a name="other-resources"></a><span data-ttu-id="3f42f-127">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="3f42f-127">Other resources</span></span>


  
    
    
 [<span data-ttu-id="3f42f-128">Step 1: Creating the Web Service Client Project</span><span class="sxs-lookup"><span data-stu-id="3f42f-128">Step 1: Creating the Web Service Client Project</span></span>](step-1-creating-the-web-service-client-project.md)
  
    
    
 [<span data-ttu-id="3f42f-129">Step 2: Adding a Web Reference</span><span class="sxs-lookup"><span data-stu-id="3f42f-129">Step 2: Adding a Web Reference</span></span>](step-2-adding-a-web-reference.md)
  
    
    
 [<span data-ttu-id="3f42f-130">Step 3: Accessing the Web Service</span><span class="sxs-lookup"><span data-stu-id="3f42f-130">Step 3: Accessing the Web Service</span></span>](step-3-accessing-the-web-service.md)
  
    
    
 [<span data-ttu-id="3f42f-131">Step 4: Building and Testing the Application</span><span class="sxs-lookup"><span data-stu-id="3f42f-131">Step 4: Building and Testing the Application</span></span>](step-4-building-and-testing-the-application.md)
  
    
    
 [<span data-ttu-id="3f42f-132">Walkthrough: Developing a Custom Application Using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="3f42f-132">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
