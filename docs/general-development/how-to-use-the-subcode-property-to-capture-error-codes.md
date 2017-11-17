---
title: How to Use the SubCode Property to Capture Error Codes
ms.date: 09/25/2017
keywords: how to,howdoi,howto,subcode
f1_keywords: how to,howdoi,howto,subcode
ms.prod: sharepoint
ms.assetid: 8ce4d5b2-111b-49e7-9d07-8c2c586221ec
ms.openlocfilehash: 6617f026a1d284120c27a409fd001eda6b4a58e5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-use-the-subcode-property-to-capture-error-codes"></a><span data-ttu-id="fc853-103">How to: Use the SubCode Property to Capture Error Codes</span><span class="sxs-lookup"><span data-stu-id="fc853-103">How to: Use the SubCode Property to Capture Error Codes</span></span>

<span data-ttu-id="fc853-p101">Excel Services generates errors in the SOAP exception based on errors that occur in Excel Services. To make it easier for the developer to catch specific error conditions, an Dienste für Excel-Berechnungen alert has an associated error code. The Excel Web Services then returns the error using properties from the **SoapException** class.</span><span class="sxs-lookup"><span data-stu-id="fc853-p101">Excel Services generates errors in the SOAP exception based on errors that occur in Excel Services. To make it easier for the developer to catch specific error conditions, an Excel Calculation Services alert has an associated error code. The Excel Web Services then returns the error using properties from the **SoapException** class.</span></span>
  
    
    

<span data-ttu-id="fc853-107">The following examples show how to capture the error codes using the  [SubCode](http://msdn.microsoft.com/library/frlrfSystemWebServicesProtocolsSoapExceptionClassSubCodeTopic.aspx) property (http://msdn.microsoft.com/de-DE/library/system.web.services.protocols.soapexception.subcode.aspx) of the **SoapException** class.</span><span class="sxs-lookup"><span data-stu-id="fc853-107">The following examples show how to capture the error codes using the  [SubCode](http://msdn.microsoft.com/library/frlrfSystemWebServicesProtocolsSoapExceptionClassSubCodeTopic.aspx) property (http://msdn.microsoft.com/en-us/library/system.web.services.protocols.soapexception.subcode.aspx) of the **SoapException** class.</span></span>
> <span data-ttu-id="fc853-108">**Hinweis:** Um die **SubCode**-Eigenschaft verwenden zu können, müssen Sie Microsoft Visual Studio 2005 verwenden.</span><span class="sxs-lookup"><span data-stu-id="fc853-108">**Note** To be able to use the **SubCode** property, you must use Microsoft Visual Studio 2005. The SubCode property does not exist in earlier versions of Visual Studio.</span></span> <span data-ttu-id="fc853-109">Die **SubCode**-Eigenschaft ist in früheren Versionen von Visual Studio nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="fc853-109">To be able to use the **SubCode** property, you must use Microsoft Visual Studio 2005. The SubCode property does not exist in earlier versions of Visual Studio.</span></span>
  
    
    

<span data-ttu-id="fc853-110">Eine Liste der Fehlercodes finden Sie unter [Excel Services-Fehlercodes](excel-services-error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fc853-110">For a list of error codes, see  [Excel Services Error Codes](excel-services-error-codes.md).</span></span>
### <a name="to-capture-error-codes-when-using-soap"></a><span data-ttu-id="fc853-111">To capture error codes when using SOAP</span><span class="sxs-lookup"><span data-stu-id="fc853-111">To capture error codes when using SOAP</span></span>


1. <span data-ttu-id="fc853-112">After adding a Web reference to the Excel Web Services, add the following using directive so that you can use the **SoapException** class without having to qualify it with a full namespace:</span><span class="sxs-lookup"><span data-stu-id="fc853-112">After adding a Web reference to the Excel Web Services, add the following using directive so that you can use the **SoapException** class without having to qualify it with a full namespace:</span></span>
    
```cs
  
using System.Web.Services.Protocols;
```


```VB.net
  Imports System.Web.Services.Protocols
```

2. <span data-ttu-id="fc853-p103">To capture the Excel Services error codes using the **SubCode** property, you must use the SOAP12 protocol version. After instantiating the Excel Web Services proxy class, set the SOAP protocol version as follows:</span><span class="sxs-lookup"><span data-stu-id="fc853-p103">To capture the Excel Services error codes using the **SubCode** property, you must use the SOAP12 protocol version. After instantiating the Excel Web Services proxy class, set the SOAP protocol version as follows:</span></span>
    
```cs
  // Instantiate the Web service.
 ExcelService xlservice = new ExcelService();

// Set the SOAP protocol version.           
xlservice.SoapVersion = SoapProtocolVersion.Soap12;
```


```VB.net
  
' Instantiate the Web service.
 Dim xlservice As New ExcelService()

' Set the SOAP protocol version.           
xlservice.SoapVersion = SoapProtocolVersion.Soap12
```

3. <span data-ttu-id="fc853-115">To catch the error codes using the **SubCode** property, add a SOAP exception catch block to your code, for example:</span><span class="sxs-lookup"><span data-stu-id="fc853-115">To catch the error codes using the **SubCode** property, add a SOAP exception catch block to your code, for example:</span></span>
    
```cs
  
catch (SoapException e)
{
    Console.WriteLine("SOAP Exception Message: {0}", e.Message);
    Console.WriteLine("SOAP Exception Error Code: {0}", 
        e.SubCode.Code.Name);
}
```


```VB.net
  
Catch e As SoapException
    Console.WriteLine("SOAP Exception Message: {0}", e.Message)
    Console.WriteLine("SOAP Exception Error Code: {0}", e.SubCode.Code.Name)
End Try
```


### <a name="to-capture-error-codes-when-using-direct-linking"></a><span data-ttu-id="fc853-116">To capture error codes when using direct linking</span><span class="sxs-lookup"><span data-stu-id="fc853-116">To capture error codes when using direct linking</span></span>


1. <span data-ttu-id="fc853-p104">In the direct linking scenario, you won't need to add a Web reference to the Excel Web Services. However, you will need to add a reference to **System.Web.Services** namespace.</span><span class="sxs-lookup"><span data-stu-id="fc853-p104">In the direct linking scenario, you won't need to add a Web reference to the Excel Web Services. However, you will need to add a reference to **System.Web.Services** namespace.</span></span>
    
  
2. <span data-ttu-id="fc853-119">After you add a reference, add the following **using** directive to your code so that you can use the **SoapException** class without having to qualify it with a full namespace:</span><span class="sxs-lookup"><span data-stu-id="fc853-119">After you add a reference, add the following **using** directive to your code so that you can use the **SoapException** class without having to qualify it with a full namespace:</span></span>
    
```cs
  
using System.Web.Services.Protocols;
```


```VB.net
  Imports System.Web.Services.Protocols
```

3. <span data-ttu-id="fc853-120">Unlike using SOAP over HTTP, in the direct linking scenario, you won't need to set the SOAP protocol version.</span><span class="sxs-lookup"><span data-stu-id="fc853-120">Unlike using SOAP over HTTP, in the direct linking scenario, you won't need to set the SOAP protocol version.</span></span> 
    
  
4. <span data-ttu-id="fc853-121">To catch the error codes using the **SubCode** property, add a SOAP exception catch block to your code, for example:</span><span class="sxs-lookup"><span data-stu-id="fc853-121">To catch the error codes using the **SubCode** property, add a SOAP exception catch block to your code, for example:</span></span>
    
```cs
  catch (SoapException e)
{
    Console.WriteLine("SOAP Exception Message: {0}", e.Message);
    Console.WriteLine("SOAP Exception Error Code: {0}", 
        e.SubCode.Code.Name);
}
```


```VB.net
  
Catch e As SoapException
    Console.WriteLine("SOAP Exception Message: {0}", e.Message)
    Console.WriteLine("SOAP Exception Error Code: {0}", e.SubCode.Code.Name)
End Try
```


## <a name="example"></a><span data-ttu-id="fc853-122">Beispiel</span><span class="sxs-lookup"><span data-stu-id="fc853-122">Example</span></span>

<span data-ttu-id="fc853-p105">The following program (a console application) uses the **SubCode** property to capture the error codes. The program takes different actions based on the error code that is caught. You can, for example, intentionally pass in a nonexistent sheet name to trigger a SOAP exception. In this case, the following SOAP exception message is returned:</span><span class="sxs-lookup"><span data-stu-id="fc853-p105">The following program (a console application) uses the **SubCode** property to capture the error codes. The program takes different actions based on the error code that is caught. You can, for example, intentionally pass in a nonexistent sheet name to trigger a SOAP exception. In this case, the following SOAP exception message is returned:</span></span>
  
    
    

```

The sheet that was requested could not be found. Please try a different one.
```


```cs
using System;
using System.Collections.Generic;
using System.Text;
using System.Web.Services.Protocols;
using System.Threading;
using SubCodeExample;

namespace SubCodeExample
{
    class Program
    {
        static void Main(string[] args)
        {
            if (args.Length != 3)
            {
                Console.WriteLine("This program requires 3 parameters - 
                    workbook, sheet and cell");
            }
            string workbookUrl = args[0];
            string sheetName = args[1];
            string cellRange = args[2];

            const string DataRefreshError = 
                "ExternalDataRefreshFailed";
            const string InvalidSheetNameError = "InvalidSheetName";
            const string FileOpenNotFound = "FileOpenNotFound";

            string sessionId = null;
            MyXlServices.ExcelService service = null;
            try
            {
                MyXlServices.Status[] status;
                service = new 
                    SubCodeExample.MyXlServices.ExcelService();
                service.SoapVersion = SoapProtocolVersion.Soap12;
                service.Credentials = 
                    System.Net.CredentialCache.DefaultCredentials;
                sessionId = service.OpenWorkbook(workbookUrl, "", "", 
                    out status);

                object result = service.GetCellA1(sessionId, sheetName, 
                    cellRange, true, out status);
                Console.WriteLine("GetCell result was:{0}", result);

                int retries = 3;
                while (retries > 0)
                {
                    try
                    {
                        service.Refresh(sessionId, "");
                    }
                    catch (SoapException soapException)
                    {
                        bool rethrow = true;
                        if (soapException.SubCode.Code.Name == 
                            DataRefreshError)
                        {
                            if (retries > 1)
                            {
                                Console.WriteLine("Error when 
                                    refreshing. Retrying...");
                                Thread.Sleep(5000);
                                rethrow = false;
                            }
                        }
                        if (rethrow) throw;
                    }
                    retries--;
                }
                
            }
            catch (SoapException exception)
            {
                string subCode = exception.SubCode.Code.Name;
                if (subCode == FileOpenNotFound)
                {
                    Console.WriteLine("The workbook could not be found. 
                        Change the first argument to be 
                        a valid file name.");
                }
                else if (subCode == DataRefreshError)
                {
                    Console.WriteLine("Could not refresh 
                        the workbook.");
                }
                else if (subCode == InvalidSheetNameError)
                {
                    Console.WriteLine("The sheet that was requested 
                        could not be found. Please try 
                        a different one.");
                }
                else
                {
                    Console.WriteLine("Unknown error code returned from 
                        Excel Services:{0}", subCode);
                }
            }
            
            catch (Exception)
            {
                Console.WriteLine("Unknown exception was raised.");
            }
            finally
            {
                if (service != null &amp;&amp; 
                    !String.IsNullOrEmpty(sessionId))
                {
                    try
                    {
                        service.CloseWorkbook(sessionId);
                    }
                    catch
                    {
                    }
                }
            }
        }
    }
}

```


```VB.net

Imports System
Imports System.Collections.Generic
Imports System.Text
Imports System.Web.Services.Protocols
Imports System.Threading
Imports SubCodeExample

Namespace SubCodeExample
    Friend Class Program
        Shared Sub Main(ByVal args() As String)
            If args.Length <> 3 Then
                Console.WriteLine("This program requires 3 parameters - workbook, sheet and cell")
            End If
            Dim workbookUrl As String = args(0)
            Dim sheetName As String = args(1)
            Dim cellRange As String = args(2)

            Const DataRefreshError As String = "ExternalDataRefreshFailed"
            Const InvalidSheetNameError As String = "InvalidSheetName"
            Const FileOpenNotFound As String = "FileOpenNotFound"

            Dim sessionId As String = Nothing
            Dim service As MyXlServices.ExcelService = Nothing
            Try
                Dim status() As MyXlServices.Status
                service = New SubCodeExample.MyXlServices.ExcelService()
                service.SoapVersion = SoapProtocolVersion.Soap12
                service.Credentials = System.Net.CredentialCache.DefaultCredentials
                sessionId = service.OpenWorkbook(workbookUrl, "", "", status)

                Dim result As Object = service.GetCellA1(sessionId, sheetName, cellRange, True, status)
                Console.WriteLine("GetCell result was:{0}", result)

                Dim retries As Integer = 3
                Do While retries > 0
                    Try
                        service.Refresh(sessionId, "")
                    Catch soapException As SoapException
                        Dim rethrow As Boolean = True
                        If soapException.SubCode.Code.Name = DataRefreshError Then
                            If retries > 1 Then
                                Console.WriteLine("Error when refreshing. Retrying...")
                                Thread.Sleep(5000)
                                rethrow = False
                            End If
                        End If
                        If rethrow Then
                            Throw
                        End If
                    End Try
                    retries -= 1
                Loop

            Catch exception As SoapException
                Dim subCode As String = exception.SubCode.Code.Name
                If subCode = FileOpenNotFound Then
                    Console.WriteLine("The workbook could not be found. Change the first argument to be a valid file name.")
                ElseIf subCode = DataRefreshError Then
                    Console.WriteLine("Could not refresh the workbook.")
                ElseIf subCode = InvalidSheetNameError Then
                    Console.WriteLine("The sheet that was requested could not be found. Please try a different one.")
                Else
                    Console.WriteLine("Unknown error code returned from Excel Services:{0}", subCode)
                End If

            Catch e1 As Exception
                Console.WriteLine("Unknown exception was raised.")
            Finally
                If service IsNot Nothing AndAlso (Not String.IsNullOrEmpty(sessionId)) Then
                    Try
                        service.CloseWorkbook(sessionId)
                    Catch
                    End Try
                End If
            End Try
        End Sub
    End Class
End Namespace
```


## <a name="robust-programming"></a><span data-ttu-id="fc853-127">Robuste Programmierung</span><span class="sxs-lookup"><span data-stu-id="fc853-127">Robust programming</span></span>

<span data-ttu-id="fc853-p106">Make sure that you add a Web reference to an Excel Web Services site that you have access to. Change the  `using SubCodeExample;` statement to point to the Web service site that you are referencing.</span><span class="sxs-lookup"><span data-stu-id="fc853-p106">Make sure that you add a Web reference to an Excel Web Services site that you have access to. Change the  `using SubCodeExample;` statement to point to the Web service site that you are referencing.</span></span>
  
    
    
<span data-ttu-id="fc853-130">In addition, make changes to the workbook path, sheet name, and so on, as appropriate.</span><span class="sxs-lookup"><span data-stu-id="fc853-130">In addition, make changes to the workbook path, sheet name, and so on, as appropriate.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="fc853-131">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="fc853-131">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="fc853-132">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="fc853-132">Tasks</span></span>


  
    
    
 [<span data-ttu-id="fc853-133">How to: Catch Exceptions</span><span class="sxs-lookup"><span data-stu-id="fc853-133">How to: Catch Exceptions</span></span>](how-to-catch-exceptions.md)
  
    
    
 [<span data-ttu-id="fc853-134">How to: Trust a Location</span><span class="sxs-lookup"><span data-stu-id="fc853-134">How to: Trust a Location</span></span>](how-to-trust-a-location.md)
  
    
    
 [<span data-ttu-id="fc853-135">How to: Save from Excel Client to the Server</span><span class="sxs-lookup"><span data-stu-id="fc853-135">How to: Save from Excel Client to the Server</span></span>](how-to-save-from-excel-client-to-the-server.md)
#### <a name="concepts"></a><span data-ttu-id="fc853-136">Konzepte</span><span class="sxs-lookup"><span data-stu-id="fc853-136">Concepts</span></span>


  
    
    
 [<span data-ttu-id="fc853-137">Accessing the SOAP API</span><span class="sxs-lookup"><span data-stu-id="fc853-137">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
  
    
    
 [<span data-ttu-id="fc853-138">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="fc853-138">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="fc853-139">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="fc853-139">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
  
    
    
 [<span data-ttu-id="fc853-140">Loop-Back SOAP Calls and Direct Linking</span><span class="sxs-lookup"><span data-stu-id="fc853-140">Loop-Back SOAP Calls and Direct Linking</span></span>](loop-back-soap-calls-and-direct-linking.md)
#### <a name="other-resources"></a><span data-ttu-id="fc853-141">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="fc853-141">Other resources</span></span>


  
    
    
 [<span data-ttu-id="fc853-142">Walkthrough: Developing a Custom Application Using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="fc853-142">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
