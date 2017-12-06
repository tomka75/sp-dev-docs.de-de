---
title: Step 3 Accessing the Web Service
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d27f654d-242f-4f34-8385-be857c170532
ms.openlocfilehash: be159956d3799a2c9dac2d3aef309a178889f494
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="step-3-accessing-the-web-service"></a><span data-ttu-id="c88fb-102">Step 3: Accessing the Web Service</span><span class="sxs-lookup"><span data-stu-id="c88fb-102">Step 3: Accessing the Web Service</span></span>

<span data-ttu-id="c88fb-p101">Nachdem Sie Ihrem Projekt einen Verweis auf Excel Web Services hinzugefügt haben, erstellen Sie im nächsten Schritt eine Instanz der Proxyklasse des Webdiensts. Anschließend können Sie auf die Methoden des Webdiensts zugreifen, indem Sie die Methoden in der Proxyklasse aufrufen. Wenn diese Methoden von der Anwendung aufgerufen werden, verarbeitet der von Visual Studio generierte Code für die Proxyklasse die Kommunikation zwischen Anwendung und Webdienst.</span><span class="sxs-lookup"><span data-stu-id="c88fb-p101">After you have added a reference to Excel Web Services to your project, the next step is to create an instance of the Web service's proxy class. You can then access the methods of the Web service by calling the methods in the proxy class. When your application calls these methods, the proxy class code generated by Visual Studio handles the communications between your application and the Web service.</span></span> 
  
    
    

<span data-ttu-id="c88fb-106">Zuerst erstellen Sie eine Instanz der Proxyklasse des Webdiensts, ExcelWebService.</span><span class="sxs-lookup"><span data-stu-id="c88fb-106">First you create an instance of the Web service's proxy class, ExcelWebService. Next you call several of the Web service's methods and properties using the proxy class.</span></span> <span data-ttu-id="c88fb-107">Als Nächstes rufen Sie mehrere Methoden und Eigenschaften des Webdiensts mithilfe der Proxyklasse auf.</span><span class="sxs-lookup"><span data-stu-id="c88fb-107">First you create an instance of the Web service's proxy class, ExcelWebService. Next you call several of the Web service's methods and properties using the proxy class.</span></span> <span data-ttu-id="c88fb-108">Sie verwenden die Aufrufe, um eine Arbeitsmappe zu öffnen, die Sitzungs-ID abzurufen, die Standardanmeldeinformationen zu übergeben, das Bereichskoordinatenobjekt zu definieren, den Bereich abzurufen, der das Bereichskoordinatenobjekt verwendet, die Arbeitsmappe zu schließen und die SOAP-Ausnahmen abzufangen.</span><span class="sxs-lookup"><span data-stu-id="c88fb-108">You use the calls to open a workbook, get the session ID, pass in the default credentials, define the range coordinate object, get the range that uses the range coordinate object, close the workbook, and catch the SOAP exceptions.</span></span>
  
    
    


## <a name="accessing-the-web-service"></a><span data-ttu-id="c88fb-109">Zugreifen auf den Webdienst</span><span class="sxs-lookup"><span data-stu-id="c88fb-109">Accessing the Web Service</span></span>


### <a name="to-add-directives"></a><span data-ttu-id="c88fb-110">So fügen Sie Anweisungen hinzu</span><span class="sxs-lookup"><span data-stu-id="c88fb-110">To add directives</span></span>


1. <span data-ttu-id="c88fb-111">Als Sie zu einem früheren Zeitpunkt den Webverweis hinzugefügt haben, wurde ein Objekt namens „ExcelService“ in einem Namespace namens <yourProject>.<webReferenceName> erstellt.</span><span class="sxs-lookup"><span data-stu-id="c88fb-111">When you added the Web reference earlier, it created an object named ExcelService in a namespace called <yourProject>.<webReferenceName>.</span></span> <span data-ttu-id="c88fb-112">In diesem Beispiel heißt das Objekt „SampleApplication.ExcelWebService“.</span><span class="sxs-lookup"><span data-stu-id="c88fb-112">In this example, the object is named SampleApplication.ExcelWebService.</span></span> <span data-ttu-id="c88fb-113">Diese exemplarische Vorgehensweise zeigt auch das Abfangen von SOAP-Ausnahmen.</span><span class="sxs-lookup"><span data-stu-id="c88fb-113">This walkthrough also shows how to catch SOAP exceptions.</span></span> <span data-ttu-id="c88fb-114">Zu diesem Zweck verwenden Sie das **System.Web.Services.Protocols**-Objekt.</span><span class="sxs-lookup"><span data-stu-id="c88fb-114">To do so, you use the **System.Web.Services.Protocols** object.</span></span> <span data-ttu-id="c88fb-115">Der Namespace **System.Web.Services.Protocols** besteht aus den Klassen, die die Protokolle definieren, die zum Übertragen von Daten über das Netzwerk während der Kommunikation zwischen den XML-Webdienstclients und mit ASP-NET erstellten XML-Webdiensten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="c88fb-115">The **System.Web.Services.Protocols** namespace consists of the classes that define the protocols used to transmit data across the wire during the communication between XML Web service clients and XML Web services created using ASP.NET.</span></span>
  
    
    
<span data-ttu-id="c88fb-116">Um die Verwendung dieser Objekte zu vereinfachen, müssen Sie zuerst die Namespaces als Anweisunge zur Datei „Class1.cs“ hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c88fb-116">To facilitate using these objects, you must first add the namespaces as directives to the Class1.cs file.</span></span> <span data-ttu-id="c88fb-117">Auf diese Weise müssen Sie bei Verwendung dieser Richtlinien die Typen nicht vollständig im Namespace qualifizieren.</span><span class="sxs-lookup"><span data-stu-id="c88fb-117">This way, if you use these directives, you do not need to fully qualify the types in the namespace.</span></span> 
    
  
2. <span data-ttu-id="c88fb-118">Zum Hinzufügen dieser Anweisungen fügen Sie am Anfang des Codes in der Datei „Class1.cs“ nach `using System:` den folgenden Code hinzu:</span><span class="sxs-lookup"><span data-stu-id="c88fb-118">To add these directives, add the following code to the beginning of your code in the Class1.cs file, after using System:`using System:`</span></span>
    
```cs
  
using SampleApplication.ExcelWebService;
using System.Web.Services.Protocols;
```


```VB.net
  
Imports SampleApplication.ExcelWebService
Imports System.Web.Services.Protocols
```


### <a name="to-call-the-web-service"></a><span data-ttu-id="c88fb-119">So rufen Sie den Webdienst auf</span><span class="sxs-lookup"><span data-stu-id="c88fb-119">To call the Web service</span></span>


1. <span data-ttu-id="c88fb-120">Instanziieren und initialisieren Sie das Webdienst-Proxyobjekt, indem Sie nach der öffnenden Klammer in  `static void Main(string[] args)` den folgenden Code einfügen:</span><span class="sxs-lookup"><span data-stu-id="c88fb-120">Instantiate and initialize the Web service proxy object by adding the following code after the opening bracket in  `static void Main(string[] args)`:</span></span>
    
```cs
  
ExcelService es = new ExcelService();
```


```VB.net
  Dim es As New ExcelService()
```

2. <span data-ttu-id="c88fb-121">Fügen Sie folgenden Code hinzu, um ein Statusarray und Bereichskoordinatenobjekte zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="c88fb-121">Add the following code to create a status array and range coordinate objects:</span></span>
    
```cs
  Status[] outStatus;
RangeCoordinates rangeCoordinates = new RangeCoordinates();
```


```VB.net
  
Dim outStatus() As Status
Dim rangeCoordinates As New RangeCoordinates()
```

3. <span data-ttu-id="c88fb-p105">Fügen Sie den Code hinzu, der auf die Arbeitsmappe zeigt, auf die Sie zugreifen möchten. In diesem Beispiel heißt die Arbeitsmappe "Sheet1". Fügen Sie Folgendes in den Code ein:</span><span class="sxs-lookup"><span data-stu-id="c88fb-p105">Add the code to point to the worksheet you want to access. In this example, the worksheet is called "Sheet1". Add the following to your code:</span></span> 
    
```cs
  
string sheetName = "Sheet1";
```


```VB.net
  Dim sheetName As String = "Sheet1"
```


    > **Note:**
      > Make sure the workbook you want to open has a worksheet called "Sheet1" that contains values. Alternatively, you can change "Sheet1" in the code to the name of your worksheet. 
4.  <span data-ttu-id="c88fb-125">`Add the following code to point to the workbook you want to open`:</span><span class="sxs-lookup"><span data-stu-id="c88fb-125"></span></span>
    
```cs
  string targetWorkbookPath = "http://myserver02/example/Shared%20Documents/Book1.xlsx";
```


```VB.net
  Dim targetWorkbookPath As String = "http://myserver02/example/Shared%20Documents/Book1.xlsx"
```


    > **Important:**
      > Change the workbook path to match the location of the workbook you are using for this walkthrough. Make sure the workbook exists and that the location where the workbook is saved is a trusted location. Using an HTTP URL to point to the location of a workbook allows you to access it remotely. 

    > **Note:**
      > You can get the path to a workbook in Microsoft SharePoint Server 2010 by right-clicking the workbook and selecting **Copy Shortcut**. Alternatively, you can select **Properties** and copy the path to the workbook from there.
5. <span data-ttu-id="c88fb-126">Fügen Sie den folgenden Code hinzu, um die Anmeldeinformationen für die Anforderung festzulegen.</span><span class="sxs-lookup"><span data-stu-id="c88fb-126">Add the following code to set the credentials for the request.</span></span> 
    
    > <span data-ttu-id="c88fb-127">**Hinweis:** Sie müssen die Anmeldeinformationen explizit festlegen, selbst dann, wenn Sie vorhaben, die Standardanmeldeinformationen zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="c88fb-127">**Note** You have to explicitly set the credentials even if you intend to use the default credentials.</span></span> 

```cs
  es.Credentials = System.Net.CredentialCache.DefaultCredentials;
```


```VB.net
  es.Credentials = System.Net.CredentialCache.DefaultCredentials
```

6. <span data-ttu-id="c88fb-p106">Fügen Sie den folgenden Code hinzu, um die Arbeitsmappe zu öffnen und auf den vertrauenswürdigen Speicherort zu zeigen, an dem die Arbeitsmappe sich befindet. Platzieren Sie den Code in einem **try**-Block:</span><span class="sxs-lookup"><span data-stu-id="c88fb-p106">Add the following code to open the workbook and point to the trusted location where the workbook is located. Place the code in a **try** block:</span></span>
    
```cs
  try
{
string sessionId = es.OpenWorkbook(targetWorkbookPath, "en-US", 
    "en-US", out outStatus);
```


```VB.net
  
Try
Dim sessionId As String = es.OpenWorkbook(targetWorkbookPath, "en-US", "en-US", outStatus)
```

7. <span data-ttu-id="c88fb-p107">Fügen Sie den folgenden Code hinzu, um ein Objekt zum Definieren von Bereichskoordinaten vorzubereiten, und rufen Sie die **GetRange**-Methode auf. Der Code gibt außerdem die Gesamtzahl der Zeilen in dem Bereich und den Wert in einem bestimmten Bereich aus.</span><span class="sxs-lookup"><span data-stu-id="c88fb-p107">Add the following code to prepare an object to define range coordinates, and call the **GetRange** method. The code will also print the total number of rows in the range and the value in a particular range.</span></span>
    
```cs
  
rangeCoordinates.Column = 3;
rangeCoordinates.Row = 9;
rangeCoordinates.Height = 18;
rangeCoordinates.Width = 12;

object[] rangeResult1 = es.GetRange(sessionId, sheetName,
    rangeCoordinates, false, out outStatus);
Console.WriteLine("Total rows in range: " + rangeResult1.Length);
Console.WriteLine("Value in range is: " + ((object[])rangeResult1[5])[2]);
```


```VB.net
  
rangeCoordinates.Column = 3
rangeCoordinates.Row = 9
rangeCoordinates.Height = 18
rangeCoordinates.Width = 12

Dim rangeResult1() As Object = es.GetRange(sessionId, sheetName, rangeCoordinates, False, outStatus)
Console.WriteLine("Total rows in range: " &amp; rangeResult1.Length)
Console.WriteLine("Value in range is: " &amp; (CType(rangeResult1(5), Object()))(2))
```

8. <span data-ttu-id="c88fb-p108">Fügen Sie Code zum Schließen der Arbeitsmappe und der aktuellen Sitzung hinzu. Fügen Sie außerdem eine schließende Klammer am Ende des **try**-Blocks hinzu.</span><span class="sxs-lookup"><span data-stu-id="c88fb-p108">Add code to close the workbook and close the current session. Also add a close bracket to end the **try** block.</span></span>
    
    > <span data-ttu-id="c88fb-134">**Wichtig:** Es empfiehlt sich, die Arbeitsmappe zu schließen, wenn Sie mit der Sitzung fertig sind.</span><span class="sxs-lookup"><span data-stu-id="c88fb-134">**Important** It is good practice to close the workbook if you are done using the session. This will close the session and free resources.</span></span> <span data-ttu-id="c88fb-135">Dadurch wird die Sitzung geschlossen, und Ressourcen werden freigegeben.</span><span class="sxs-lookup"><span data-stu-id="c88fb-135">This will close the session and free resources.</span></span> 

```cs
  
es.CloseWorkbook(sessionId);
}
```


```VB.net
  
es.CloseWorkbook(sessionId)
```

9. <span data-ttu-id="c88fb-136">Fügen Sie einen **catch**-Block hinzu, um die SOAP-Ausnahme abzufangen und die Ausnahmemeldung zu drucken:</span><span class="sxs-lookup"><span data-stu-id="c88fb-136">Add a **catch** block to catch the SOAP exception and print the exception message:</span></span>
    
```cs
  catch (SoapException e)
{
    Console.WriteLine("SOAP Exception Message: {0}", e.Message);
}
```


```VB.net
  
Catch e As SoapException
    Console.WriteLine("SOAP Exception Message: {0}", e.Message)
End Try
```


## <a name="complete-code"></a><span data-ttu-id="c88fb-137">Vollständiger Code</span><span class="sxs-lookup"><span data-stu-id="c88fb-137">Complete Code</span></span>

<span data-ttu-id="c88fb-138">Das folgende Codebeispiel ist der vollständige Code in der Beispieldatei „Class1.cs“ aus dem vorherigen Verfahren.</span><span class="sxs-lookup"><span data-stu-id="c88fb-138">The following code sample is the complete code in the Class1.cs example file described in the previous procedures.</span></span>
  
    
    

> <span data-ttu-id="c88fb-139">**Wichtig:** Ändern Sie je nach Bedarf den Pfad der Arbeitsmappe, den Namen des Arbeitsblatts usw.</span><span class="sxs-lookup"><span data-stu-id="c88fb-139">**Important** Make changes to the workbook path, sheet name, and so on, as appropriate.</span></span> 
  
    
    


```cs

using System;
using SampleApplication.ExcelWebService;
using System.Web.Services.Protocols;

namespace SampleApplication
{
    class Class1
    {
        [STAThread]
        static void Main(string[] args)
        {            
            // Instantiate the Web service and create a status array object and range coordinate object
            ExcelService es = new ExcelService();
            Status[] outStatus;
            RangeCoordinates rangeCoordinates = new RangeCoordinates();
            
string sheetName = "Sheet1";
            // Using workbookPath this way will allow 
            // you to call the workbook remotely.
            // TODO: change the workbook path to 
            // point to workbook in a trusted location
            // that you have access to 
            string targetWorkbookPath = "http://myserver02/example/Shared%20Documents/Book1.xlsx";
//you can also use .xlsb files, for example, //"http://myserver02/example/Shared%20Documents/Book1.xlsb";

            // Set credentials for requests
            es.Credentials = System.Net.CredentialCache.DefaultCredentials;
            //Console.WriteLine("Cred: {0}", es.Credentials);
            try
            {
                // Call open workbook, and point to the trusted   
                // location of the workbook to open.
                string sessionId = es.OpenWorkbook(targetWorkbookPath, "en-US", "en-US", out outStatus);
                // Console.WriteLine("sessionID : {0}", sessionId);

                // Prepare object to define range coordinates
                // and the GetRange method.
                rangeCoordinates.Column = 3;
                rangeCoordinates.Row = 9;
                rangeCoordinates.Height = 18;
                rangeCoordinates.Width = 12;

                object[] rangeResult1 = es.GetRange(sessionId, sheetName, rangeCoordinates, false, out outStatus);
                Console.WriteLine("Total Rows in Range: " + rangeResult1.Length);
                Console.WriteLine("Value in range is: " + ((object[])rangeResult1[5])[3]); 
        
                // Close workbook. This also closes session.
                es.CloseWorkbook(sessionId);
            }
            catch (SoapException e)
            {
                Console.WriteLine("SOAP Exception Message: {0}", e.Message);
            }
            // catch (Exception e)
//            {
//                Console.WriteLine("Exception Message: {0}", e.Message);
//            }
//            Console.ReadLine();
        }
    }
}
     
```


```VB.net

Imports System
Imports SampleApplication.ExcelWebService
Imports System.Web.Services.Protocols

Namespace SampleApplication
    Friend Class Class1
        <STAThread> _
        Shared Sub Main(ByVal args() As String)
            ' Instantiate the Web service and create a status array object and range coordinate object
            Dim es As New ExcelService()
            Dim outStatus() As Status
            Dim rangeCoordinates As New RangeCoordinates()

Dim sheetName As String = "Sheet1"
            ' Using workbookPath this way will allow 
            ' you to call the workbook remotely.
            ' TODO: change the workbook path to 
            ' point to workbook in a trusted location
            ' that you have access to 
            Dim targetWorkbookPath As String = "http://myserver02/example/Shared%20Documents/Book1.xlsx"
'you can also use .xlsb files, for example, //"http://myserver02/example/Shared%20Documents/Book1.xlsb";

            ' Set credentials for requests
            es.Credentials = System.Net.CredentialCache.DefaultCredentials
            'Console.WriteLine("Cred: {0}", es.Credentials);
            Try
                ' Call open workbook, and point to the trusted   
                ' location of the workbook to open.
                Dim sessionId As String = es.OpenWorkbook(targetWorkbookPath, "en-US", "en-US", outStatus)
                ' Console.WriteLine("sessionID : {0}", sessionId)

                ' Prepare object to define range coordinates
                ' and the GetRange method.
                rangeCoordinates.Column = 3
                rangeCoordinates.Row = 9
                rangeCoordinates.Height = 18
                rangeCoordinates.Width = 12

                Dim rangeResult1() As Object = es.GetRange(sessionId, sheetName, rangeCoordinates, False, outStatus)
                Console.WriteLine("Total Rows in Range: " &amp; rangeResult1.Length)
                Console.WriteLine("Value in range is: " &amp; (CType(rangeResult1(5), Object()))(3))

                ' Close workbook. This also closes session.
                es.CloseWorkbook(sessionId)
            Catch e As SoapException
                Console.WriteLine("SOAP Exception Message: {0}", e.Message)
            ' Catch e As Exception
            '    Console.WriteLine("Exception Message: {0}", e.Message)
            End Try
            'Console.ReadLine()
        End Sub
    End Class
End Namespace
```


## <a name="see-also"></a><span data-ttu-id="c88fb-140">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="c88fb-140">See also</span></span>


#### <a name="concepts"></a><span data-ttu-id="c88fb-141">Konzepte</span><span class="sxs-lookup"><span data-stu-id="c88fb-141">Concepts</span></span>


  
    
    
 [<span data-ttu-id="c88fb-142">Accessing the SOAP API</span><span class="sxs-lookup"><span data-stu-id="c88fb-142">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
#### <a name="other-resources"></a><span data-ttu-id="c88fb-143">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="c88fb-143">Other resources</span></span>


  
    
    
 [<span data-ttu-id="c88fb-144">Step 1: Creating the Web Service Client Project</span><span class="sxs-lookup"><span data-stu-id="c88fb-144">Step 1: Creating the Web Service Client Project</span></span>](step-1-creating-the-web-service-client-project.md)
  
    
    
 [<span data-ttu-id="c88fb-145">Step 2: Adding a Web Reference</span><span class="sxs-lookup"><span data-stu-id="c88fb-145">Step 2: Adding a Web Reference</span></span>](step-2-adding-a-web-reference.md)
  
    
    
 [<span data-ttu-id="c88fb-146">Step 4: Building and Testing the Application</span><span class="sxs-lookup"><span data-stu-id="c88fb-146">Step 4: Building and Testing the Application</span></span>](step-4-building-and-testing-the-application.md)
  
    
    
 [<span data-ttu-id="c88fb-147">Walkthrough: Developing a Custom Application Using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="c88fb-147">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
  
    
    
 [<span data-ttu-id="c88fb-148">How to: Trust Workbook Locations Using Script</span><span class="sxs-lookup"><span data-stu-id="c88fb-148">How to: Trust Workbook Locations Using Script</span></span>](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx)