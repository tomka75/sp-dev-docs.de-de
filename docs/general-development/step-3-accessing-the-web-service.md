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
# <a name="step-3-accessing-the-web-service"></a>Step 3: Accessing the Web Service

Nachdem Sie Ihrem Projekt einen Verweis auf Excel Web Services hinzugefügt haben, erstellen Sie im nächsten Schritt eine Instanz der Proxyklasse des Webdiensts. Anschließend können Sie auf die Methoden des Webdiensts zugreifen, indem Sie die Methoden in der Proxyklasse aufrufen. Wenn diese Methoden von der Anwendung aufgerufen werden, verarbeitet der von Visual Studio generierte Code für die Proxyklasse die Kommunikation zwischen Anwendung und Webdienst. 
  
    
    

Zuerst erstellen Sie eine Instanz der Proxyklasse des Webdiensts, ExcelWebService. Als Nächstes rufen Sie mehrere Methoden und Eigenschaften des Webdiensts mithilfe der Proxyklasse auf. Sie verwenden die Aufrufe, um eine Arbeitsmappe zu öffnen, die Sitzungs-ID abzurufen, die Standardanmeldeinformationen zu übergeben, das Bereichskoordinatenobjekt zu definieren, den Bereich abzurufen, der das Bereichskoordinatenobjekt verwendet, die Arbeitsmappe zu schließen und die SOAP-Ausnahmen abzufangen.
  
    
    


## <a name="accessing-the-web-service"></a>Zugreifen auf den Webdienst


### <a name="to-add-directives"></a>So fügen Sie Anweisungen hinzu


1. Als Sie zu einem früheren Zeitpunkt den Webverweis hinzugefügt haben, wurde ein Objekt namens „ExcelService“ in einem Namespace namens <yourProject>.<webReferenceName> erstellt. In diesem Beispiel heißt das Objekt „SampleApplication.ExcelWebService“. Diese exemplarische Vorgehensweise zeigt auch das Abfangen von SOAP-Ausnahmen. Zu diesem Zweck verwenden Sie das **System.Web.Services.Protocols**-Objekt. Der Namespace **System.Web.Services.Protocols** besteht aus den Klassen, die die Protokolle definieren, die zum Übertragen von Daten über das Netzwerk während der Kommunikation zwischen den XML-Webdienstclients und mit ASP-NET erstellten XML-Webdiensten verwendet werden.
  
    
    
Um die Verwendung dieser Objekte zu vereinfachen, müssen Sie zuerst die Namespaces als Anweisunge zur Datei „Class1.cs“ hinzufügen. Auf diese Weise müssen Sie bei Verwendung dieser Richtlinien die Typen nicht vollständig im Namespace qualifizieren. 
    
  
2. Zum Hinzufügen dieser Anweisungen fügen Sie am Anfang des Codes in der Datei „Class1.cs“ nach `using System:` den folgenden Code hinzu:
    
```cs
  
using SampleApplication.ExcelWebService;
using System.Web.Services.Protocols;
```


```VB.net
  
Imports SampleApplication.ExcelWebService
Imports System.Web.Services.Protocols
```


### <a name="to-call-the-web-service"></a>So rufen Sie den Webdienst auf


1. Instanziieren und initialisieren Sie das Webdienst-Proxyobjekt, indem Sie nach der öffnenden Klammer in  `static void Main(string[] args)` den folgenden Code einfügen:
    
```cs
  
ExcelService es = new ExcelService();
```


```VB.net
  Dim es As New ExcelService()
```

2. Fügen Sie folgenden Code hinzu, um ein Statusarray und Bereichskoordinatenobjekte zu erstellen:
    
```cs
  Status[] outStatus;
RangeCoordinates rangeCoordinates = new RangeCoordinates();
```


```VB.net
  
Dim outStatus() As Status
Dim rangeCoordinates As New RangeCoordinates()
```

3. Fügen Sie den Code hinzu, der auf die Arbeitsmappe zeigt, auf die Sie zugreifen möchten. In diesem Beispiel heißt die Arbeitsmappe "Sheet1". Fügen Sie Folgendes in den Code ein: 
    
```cs
  
string sheetName = "Sheet1";
```


```VB.net
  Dim sheetName As String = "Sheet1"
```


    > **Note:**
      > Make sure the workbook you want to open has a worksheet called "Sheet1" that contains values. Alternatively, you can change "Sheet1" in the code to the name of your worksheet. 
4.  `Add the following code to point to the workbook you want to open`:
    
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
5. Fügen Sie den folgenden Code hinzu, um die Anmeldeinformationen für die Anforderung festzulegen. 
    
    > **Hinweis:** Sie müssen die Anmeldeinformationen explizit festlegen, selbst dann, wenn Sie vorhaben, die Standardanmeldeinformationen zu verwenden. 

```cs
  es.Credentials = System.Net.CredentialCache.DefaultCredentials;
```


```VB.net
  es.Credentials = System.Net.CredentialCache.DefaultCredentials
```

6. Fügen Sie den folgenden Code hinzu, um die Arbeitsmappe zu öffnen und auf den vertrauenswürdigen Speicherort zu zeigen, an dem die Arbeitsmappe sich befindet. Platzieren Sie den Code in einem **try**-Block:
    
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

7. Fügen Sie den folgenden Code hinzu, um ein Objekt zum Definieren von Bereichskoordinaten vorzubereiten, und rufen Sie die **GetRange**-Methode auf. Der Code gibt außerdem die Gesamtzahl der Zeilen in dem Bereich und den Wert in einem bestimmten Bereich aus.
    
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

8. Fügen Sie Code zum Schließen der Arbeitsmappe und der aktuellen Sitzung hinzu. Fügen Sie außerdem eine schließende Klammer am Ende des **try**-Blocks hinzu.
    
    > **Wichtig:** Es empfiehlt sich, die Arbeitsmappe zu schließen, wenn Sie mit der Sitzung fertig sind. Dadurch wird die Sitzung geschlossen, und Ressourcen werden freigegeben. 

```cs
  
es.CloseWorkbook(sessionId);
}
```


```VB.net
  
es.CloseWorkbook(sessionId)
```

9. Fügen Sie einen **catch**-Block hinzu, um die SOAP-Ausnahme abzufangen und die Ausnahmemeldung zu drucken:
    
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


## <a name="complete-code"></a>Vollständiger Code

Das folgende Codebeispiel ist der vollständige Code in der Beispieldatei „Class1.cs“ aus dem vorherigen Verfahren.
  
    
    

> **Wichtig:** Ändern Sie je nach Bedarf den Pfad der Arbeitsmappe, den Namen des Arbeitsblatts usw. 
  
    
    


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


## <a name="see-also"></a>Siehe auch


#### <a name="concepts"></a>Konzepte


  
    
    
 [Accessing the SOAP API](accessing-the-soap-api.md)
#### <a name="other-resources"></a>Sonstige Ressourcen


  
    
    
 [Step 1: Creating the Web Service Client Project](step-1-creating-the-web-service-client-project.md)
  
    
    
 [Step 2: Adding a Web Reference](step-2-adding-a-web-reference.md)
  
    
    
 [Step 4: Building and Testing the Application](step-4-building-and-testing-the-application.md)
  
    
    
 [Walkthrough: Developing a Custom Application Using Excel Web Services](walkthrough-developing-a-custom-application-using-excel-web-services.md)
  
    
    
 [How to: Trust Workbook Locations Using Script](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx)
