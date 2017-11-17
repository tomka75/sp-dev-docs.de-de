---
title: Step 2 Adding a Web Reference
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e9175863-ddb4-4750-847d-d53cb59b33cb
ms.openlocfilehash: ced2da0e9fcbdfdca79175d0219f13dcce4e63d4
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="step-2-adding-a-web-reference"></a><span data-ttu-id="f26cb-102">Step 2: Adding a Web Reference</span><span class="sxs-lookup"><span data-stu-id="f26cb-102">Step 2: Adding a Web Reference</span></span>

<span data-ttu-id="f26cb-p101">Webdiensterkennung ist der Prozess, durch den ein Client einen Webdienst findet und die Dienstbeschreibung abruft. In Visual Studio umfasst die Webdiensterkennung das Abfragen einer Website nach einem vordefinierten Algorithmus. Das Ziel des Prozesses ist es, die Dienstbeschreibung zu finden, ein in Web Services Description Language (WSDL) erstelltes XML-Dokument.</span><span class="sxs-lookup"><span data-stu-id="f26cb-p101">Web service discovery is the process by which a client locates a Web service and obtains its service description. The process of Web service discovery in Visual Studio involves interrogating a Web site following a predetermined algorithm. The goal of the process is to locate the service description, which is an XML document that uses the Web Services Description Language (WSDL).</span></span>
  
    
    

<span data-ttu-id="f26cb-p102">In der Dienstbeschreibung werden die verfügbaren Dienste und die Interaktion mit diesen Diensten beschrieben. Ohne Dienstbeschreibung ist keine programmgesteuerte Interaktion mit einem Webdienst möglich. Die Anwendung muss in der Lage sein, mit dem Webdienst zu kommunizieren und ihn zur Laufzeit zu finden. Das geschieht beim Hinzufügen eines Webverweises zu Ihrem Projekt, indem eine Proxyklasse generiert wird, die eine Schnittstelle zu dem Webdienst und eine lokale Darstellung des Webdiensts bereitstellt. Weitere Informationen finden Sie unter "Webverweise und Generieren eines XML-Webdienstproxys" in der Dokumentation zu Microsoft Visual Studio 2005.</span><span class="sxs-lookup"><span data-stu-id="f26cb-p102">The service description describes what services are available and how to interact with those services. Without a service description, it is impossible to programmatically interact with a Web service. Your application must have a means to communicate with the Web service and to locate it at run time. Adding a Web reference to your project for the Web service does this by generating a proxy class that interfaces with the Web service and provides a local representation of the Web service. For more information, see "Web References and Generating an XML Web Service Proxy" in the Microsoft Visual Studio 2005 documentation.</span></span>
  
    
    


## <a name="to-add-a-web-reference"></a><span data-ttu-id="f26cb-111">So fügen Sie einen Webverweis hinzu</span><span class="sxs-lookup"><span data-stu-id="f26cb-111">To add a Web Reference</span></span>


1. <span data-ttu-id="f26cb-112">Klicken Sie im Menü **Projekt** auf **Webverweis hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="f26cb-112">On the **Project** menu, click **Add Web Reference**.</span></span>
    
  
2. <span data-ttu-id="f26cb-p103">Geben Sie im Feld **URL** im Dialogfeld **Webverweis hinzufügen** die URL zum Abrufen der Dienstbeschreibung des Excel Web Services ein, z. B. `http://<server>/<customsite>/_vti_bin/excelservice.asmx` oder `http://<server>/_vti_bin/excelservice.asmx`. Klicken Sie dann auf **Los**, um Informationen über den Webdienst abzurufen.</span><span class="sxs-lookup"><span data-stu-id="f26cb-p103">In the **URL** box of the **Add Web Reference** dialog box, type the URL to obtain the service description of the Excel Web Services, such as `http://<server>/<customsite>/_vti_bin/excelservice.asmx` or `http://<server>/_vti_bin/excelservice.asmx`. Then click **Go** to retrieve information about the Web service.</span></span>
    
    > <span data-ttu-id="f26cb-115">**Hinweis:** Sie können das Dialogfeld **Webverweis hinzufügen** auch im Bereich **Projektmappen-Explorer** öffnen, indem Sie mit der rechten Maustaste auf **Verweise** klicken und **Webverweis hinzufügen** auswählen.</span><span class="sxs-lookup"><span data-stu-id="f26cb-115">**Note** You can also open the **Add Web Reference** dialog box in the **Solution Explorer** pane by right-clicking **References** and selecting **Add Web Reference**.</span></span> 
3. <span data-ttu-id="f26cb-116">Benennen Sie im Feld **Webverweis-Name** den Webverweis in toExcelWebService um.</span><span class="sxs-lookup"><span data-stu-id="f26cb-116">In the **Web reference name** box, rename the Web reference toExcelWebService.</span></span>
    
  
4. <span data-ttu-id="f26cb-117">Klicken Sie auf **Verweis hinzufügen**, um einen Webverweis für den Zielwebdienst hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="f26cb-117">Click **Add Reference** to add a Web reference for the target Web service.</span></span>
    
  
5. <span data-ttu-id="f26cb-118">Visual Studio lädt die Dienstbeschreibung herunter und generiert eine Proxyklasse, die als Schnittstelle zwischen der Anwendung und Excel Web Services fungiert.</span><span class="sxs-lookup"><span data-stu-id="f26cb-118">Visual Studio downloads the service description and generates a proxy class to interface between your application and Excel Web Services.</span></span> 
    
  
6. <span data-ttu-id="f26cb-119">Weitere Informationen finden Sie unter  [Accessing the SOAP API](accessing-the-soap-api.md).</span><span class="sxs-lookup"><span data-stu-id="f26cb-119">For more information, see  [Accessing the SOAP API](accessing-the-soap-api.md).</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="f26cb-120">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="f26cb-120">See also</span></span>


#### <a name="concepts"></a><span data-ttu-id="f26cb-121">Konzepte</span><span class="sxs-lookup"><span data-stu-id="f26cb-121">Concepts</span></span>


  
    
    
 [<span data-ttu-id="f26cb-122">Loop-Back SOAP Calls and Direct Linking</span><span class="sxs-lookup"><span data-stu-id="f26cb-122">Loop-Back SOAP Calls and Direct Linking</span></span>](loop-back-soap-calls-and-direct-linking.md)
#### <a name="other-resources"></a><span data-ttu-id="f26cb-123">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f26cb-123">Other resources</span></span>


  
    
    
 [<span data-ttu-id="f26cb-124">Step 1: Creating the Web Service Client Project</span><span class="sxs-lookup"><span data-stu-id="f26cb-124">Step 1: Creating the Web Service Client Project</span></span>](step-1-creating-the-web-service-client-project.md)
  
    
    
 [<span data-ttu-id="f26cb-125">Step 3: Accessing the Web Service</span><span class="sxs-lookup"><span data-stu-id="f26cb-125">Step 3: Accessing the Web Service</span></span>](step-3-accessing-the-web-service.md)
  
    
    
 [<span data-ttu-id="f26cb-126">Step 4: Building and Testing the Application</span><span class="sxs-lookup"><span data-stu-id="f26cb-126">Step 4: Building and Testing the Application</span></span>](step-4-building-and-testing-the-application.md)
  
    
    
 [<span data-ttu-id="f26cb-127">Walkthrough: Developing a Custom Application Using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="f26cb-127">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
