---
title: How to Save to the Server to Prepare for Programmatic Access
ms.date: 09/25/2017
keywords: how to,howdoi,howto
f1_keywords: how to,howdoi,howto
ms.prod: sharepoint
ms.assetid: 80b34a29-3d40-4d11-9ba1-b4886ffcfd42
ms.openlocfilehash: e17d155f2c67b957990a119cae8f7d2a2eb00049
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-save-to-the-server-to-prepare-for-programmatic-access"></a><span data-ttu-id="ede6b-103">How to: Save to the Server to Prepare for Programmatic Access</span><span class="sxs-lookup"><span data-stu-id="ede6b-103">How to: Save to the Server to Prepare for Programmatic Access</span></span>

<span data-ttu-id="ede6b-p101">This example shows how to save an Excel workbook to the server to to prepare it for programmatic access. The steps are:</span><span class="sxs-lookup"><span data-stu-id="ede6b-p101">This example shows how to save an Excel workbook to the server to to prepare it for programmatic access. The steps are:</span></span>
  
    
    


1. <span data-ttu-id="ede6b-106">Create a workbook with named ranges.</span><span class="sxs-lookup"><span data-stu-id="ede6b-106">Create a workbook with named ranges.</span></span>
    
  
2. <span data-ttu-id="ede6b-107">Speichern Sie die Arbeitsmappe an einem vertrauenswürdigen Speicherort der SharePoint-Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="ede6b-107">Save the workbook to a trusted SharePoint library location.</span></span> 
    
    > <span data-ttu-id="ede6b-108">**Hinweis:** Es wird vorausgesetzt, dass Sie bereits eine SharePoint-Dokumentbibliothek erstellt und diese als vertrauenswürdigen Speicherort definiert haben.</span><span class="sxs-lookup"><span data-stu-id="ede6b-108">**Note** It is assumed that you have already created a SharePoint document library and made it a trusted location. For more information, see  How to: Trust a Location.</span></span> <span data-ttu-id="ede6b-109">Weitere Informationen finden Sie unter [Gewusst wie: Vertrauen zu einem Standort](how-to-trust-a-location.md).</span><span class="sxs-lookup"><span data-stu-id="ede6b-109">Note For more information about trusting a location, see  [How to: Trust a Location](how-to-trust-a-location.md).</span></span> 
3. <span data-ttu-id="ede6b-p103">Programmatically specify values for the worksheet, named range, and cell value by using the Excel Web Services **SetCellA1** method. The values are passed in as argumentsthat is, _args [1]_ and _args [2]_:</span><span class="sxs-lookup"><span data-stu-id="ede6b-p103">Programmatically specify values for the worksheet, named range, and cell value by using the Excel Web Services **SetCellA1** method. The values are passed in as arguments—that is, _args [1]_ and _args [2]_:</span></span>
    
```cs
  
status = xlServices.SetCellA1(sessionId, String.Empty, args[1], args[2]);
```


```VB.net
  status = xlServices.SetCellA1(sessionId, String.Empty, args(1), args(2))
```


<span data-ttu-id="ede6b-112">You can specify the values of  _args [1]_ and _args [2]_ by using a Web form or from the command line:</span><span class="sxs-lookup"><span data-stu-id="ede6b-112">You can specify the values of  _args [1]_ and _args [2]_ by using a Web form or from the command line:</span></span>
  
    
    




```
GetSnapshot.exe http://MyServer002/MyTrustedDocumentLibrary/TestMyParam.xlsx MyParam28 > MySnapshot.xlsx 
```

<span data-ttu-id="ede6b-p104">In this example,  _args [1]_ is **MyParam**, **args [2]** is _28_ and _GetSnapshot.exe_ is the name of the application that you create. To find a sample program, see [How to: Get an Entire Workbook or a Snapshot](how-to-get-an-entire-workbook-or-a-snapshot.md).</span><span class="sxs-lookup"><span data-stu-id="ede6b-p104">In this example,  _args [1]_ is **MyParam**, **args [2]** is _28_ and _GetSnapshot.exe_ is the name of the application that you create. To find a sample program, see [How to: Get an Entire Workbook or a Snapshot](how-to-get-an-entire-workbook-or-a-snapshot.md).</span></span>
### <a name="to-create-a-named-range"></a><span data-ttu-id="ede6b-115">To create a named range</span><span class="sxs-lookup"><span data-stu-id="ede6b-115">To create a named range</span></span>


1. <span data-ttu-id="ede6b-116">Start Excel.</span><span class="sxs-lookup"><span data-stu-id="ede6b-116">Start Excel.</span></span>
    
  
2. <span data-ttu-id="ede6b-117">Rename **Sheet1** to beMyParamSheet.</span><span class="sxs-lookup"><span data-stu-id="ede6b-117">Rename **Sheet1** to beMyParamSheet.</span></span>
    
  
3. <span data-ttu-id="ede6b-118">In cell B2, type 20.</span><span class="sxs-lookup"><span data-stu-id="ede6b-118">In cell B2, type 20.</span></span>
    
  
4. <span data-ttu-id="ede6b-119">In cell B3, type =2+B2.</span><span class="sxs-lookup"><span data-stu-id="ede6b-119">In cell B3, type =2+B2.</span></span>
    
  
5. <span data-ttu-id="ede6b-120">Make cell B3 bold.</span><span class="sxs-lookup"><span data-stu-id="ede6b-120">Make cell B3 bold.</span></span>
    
  
6. <span data-ttu-id="ede6b-121">Make cell B2 into a named range:</span><span class="sxs-lookup"><span data-stu-id="ede6b-121">Make cell B2 into a named range:</span></span> 
    
1. <span data-ttu-id="ede6b-122">On the ribbon, click the **Formulas** tab, and then click cell B2 to select it.</span><span class="sxs-lookup"><span data-stu-id="ede6b-122">On the ribbon, click the **Formulas** tab, and then click cell B2 to select it.</span></span>
    
  
2. <span data-ttu-id="ede6b-123">In the **Defined Names** group, click **Define Name**.</span><span class="sxs-lookup"><span data-stu-id="ede6b-123">In the **Defined Names** group, click **Define Name**.</span></span>
    
  
3. <span data-ttu-id="ede6b-124">In the **New Name** dialog box, in the **Name** text box, typeMyParam.</span><span class="sxs-lookup"><span data-stu-id="ede6b-124">In the **New Name** dialog box, in the **Name** text box, typeMyParam.</span></span>
    
  
7. <span data-ttu-id="ede6b-p105">Save the workbook to a location of your choice on the local drive. Name the workbook TestMyParam.xlsx.</span><span class="sxs-lookup"><span data-stu-id="ede6b-p105">Save the workbook to a location of your choice on the local drive. Name the workbook TestMyParam.xlsx.</span></span> 
    
  

### <a name="to-save-to-a-sharepoint-library"></a><span data-ttu-id="ede6b-127">To save to a SharePoint library</span><span class="sxs-lookup"><span data-stu-id="ede6b-127">To save to a SharePoint library</span></span>


1. <span data-ttu-id="ede6b-128">On the **File** menu, click **Save &amp; Send**, and then click **Save to SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="ede6b-128">On the **File** menu, click **Save &amp; Send**, and then click **Save to SharePoint**.</span></span> 
    
  
2. <span data-ttu-id="ede6b-129">In the **Save to SharePoint** dialog box, click **Publish Options**.</span><span class="sxs-lookup"><span data-stu-id="ede6b-129">In the **Save to SharePoint** dialog box, click **Publish Options**.</span></span>
    
  
3. <span data-ttu-id="ede6b-130">In the **Publish Options** dialog box, on the **Show** tab, ensure that **Entire Workbook** is selected.</span><span class="sxs-lookup"><span data-stu-id="ede6b-130">In the **Publish Options** dialog box, on the **Show** tab, ensure that **Entire Workbook** is selected.</span></span>
    
  
4. <span data-ttu-id="ede6b-131">Click **Parameters**.</span><span class="sxs-lookup"><span data-stu-id="ede6b-131">Click **Parameters**.</span></span> 
    
  
5. <span data-ttu-id="ede6b-132">Klicken Sie auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="ede6b-132">Click **Add**.</span></span>
    
  
6. <span data-ttu-id="ede6b-p106">In the **Add Parameters** list, you should see **MyParam**. Select the **MyParam** check box.</span><span class="sxs-lookup"><span data-stu-id="ede6b-p106">In the **Add Parameters** list, you should see **MyParam**. Select the **MyParam** check box.</span></span>
    
  
7. <span data-ttu-id="ede6b-p107">Click **OK**. You should now see **MyParam** in the **Parameters** list.</span><span class="sxs-lookup"><span data-stu-id="ede6b-p107">Click **OK**. You should now see **MyParam** in the **Parameters** list.</span></span>
    
  
8. <span data-ttu-id="ede6b-137">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="ede6b-137">Click **OK**.</span></span>
    
  
9. <span data-ttu-id="ede6b-138">In the **Save to SharePoint** dialog box, click **Save As**.</span><span class="sxs-lookup"><span data-stu-id="ede6b-138">In the **Save to SharePoint** dialog box, click **Save As**.</span></span>
    
  
10. <span data-ttu-id="ede6b-139">In the **Save As** dialog box, clear the **Open with Excel in the browser** check box.</span><span class="sxs-lookup"><span data-stu-id="ede6b-139">In the **Save As** dialog box, clear the **Open with Excel in the browser** check box.</span></span>
    
  
11. <span data-ttu-id="ede6b-p108">In the **File name** box, type the path to the trusted SharePoint document library where you want to store this workbook. For example,http:// _MyServer002_/MyDocumentLibrary/TestParam.xlsx.</span><span class="sxs-lookup"><span data-stu-id="ede6b-p108">In the **File name** box, type the path to the trusted SharePoint document library where you want to store this workbook. For example,http:// _MyServer002_/MyDocumentLibrary/TestParam.xlsx.</span></span>
    
  
12. <span data-ttu-id="ede6b-142">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="ede6b-142">Click **Save**.</span></span>
    
  

### <a name="to-specify-values-programmatically"></a><span data-ttu-id="ede6b-143">To specify values programmatically</span><span class="sxs-lookup"><span data-stu-id="ede6b-143">To specify values programmatically</span></span>


1. <span data-ttu-id="ede6b-144">Following is the signature for the **SetCellA1** method in Excel Web Services:</span><span class="sxs-lookup"><span data-stu-id="ede6b-144">Following is the signature for the **SetCellA1** method in Excel Web Services:</span></span>
    
```cs
  public void SetCellA1 (
string sessionId,
string sheetName,
string rangeName,
Object cellValue,
Out Status[] status
)
```


```VB.net
  
Public Sub SetCellA1(ByVal sessionId As String,
              ByVal sheetName As String, 
             ByVal rangeName As String, 
             ByVal cellValue As Object, 
             Out ByVal status() As Status)
End Sub
```


    Set the values for the worksheet, named range, and cell value to the **SetCellA1** method as follows:
    


```cs
  
// Set a value into a cell.
status = xlSrv.SetCellA1(sessionId, String.Empty, args[1], args[2]);

```

2. <span data-ttu-id="ede6b-145">In the preceding code:</span><span class="sxs-lookup"><span data-stu-id="ede6b-145">In the preceding code:</span></span> 
    
  -  <span data-ttu-id="ede6b-p109">_args [1]_ is the name of the named range. In this example, it is **MyParam**.</span><span class="sxs-lookup"><span data-stu-id="ede6b-p109">_args [1]_ is the name of the named range. In this example, it is **MyParam**.</span></span>
    
  
  -  <span data-ttu-id="ede6b-p110">_args [2]_ is the value that you want to set in the cell. The cell where the value will be set is the named range in _args [1]_ called **MyParam**.</span><span class="sxs-lookup"><span data-stu-id="ede6b-p110">_args [2]_ is the value that you want to set in the cell. The cell where the value will be set is the named range in _args [1]_ called **MyParam**.</span></span>
    
  
3. <span data-ttu-id="ede6b-150">If you are using a command line, you can pass in the arguments as follows:</span><span class="sxs-lookup"><span data-stu-id="ede6b-150">If you are using a command line, you can pass in the arguments as follows:</span></span>
    
     <span data-ttu-id="ede6b-151">`GetSnapshot.exe http://` _MyServer002_ `/` _MyTrustedDocumentLibrary_ `/TestMyParam.xlsx MyParam 28 > MySnapshot.xlsx`</span><span class="sxs-lookup"><span data-stu-id="ede6b-151">`GetSnapshot.exe http://` _MyServer002_ `/` _MyTrustedDocumentLibrary_ `/TestMyParam.xlsx MyParam 28 > MySnapshot.xlsx`</span></span>
    
  
4. <span data-ttu-id="ede6b-152">If you generate a snapshot of the workbook, you see the following:</span><span class="sxs-lookup"><span data-stu-id="ede6b-152">If you generate a snapshot of the workbook, you see the following:</span></span> 
    
  - <span data-ttu-id="ede6b-153">Cell B2 (with the named range **MyParam**) now has a value that you fed through the program, which is **28**.</span><span class="sxs-lookup"><span data-stu-id="ede6b-153">Cell B2 (with the named range **MyParam**) now has a value that you fed through the program, which is **28**.</span></span>
    
  
  - <span data-ttu-id="ede6b-154">Cell B3 has a new calculated value of **30**.</span><span class="sxs-lookup"><span data-stu-id="ede6b-154">Cell B3 has a new calculated value of **30**.</span></span>
    
  
  - <span data-ttu-id="ede6b-155">Cell B3 does not show the original formula, which was "=2+B2".</span><span class="sxs-lookup"><span data-stu-id="ede6b-155">Cell B3 does not show the original formula, which was "=2+B2".</span></span>
    
  
  - <span data-ttu-id="ede6b-156">Zelle B3 behält die Schriftformatierung bei, d. h. Fettformatierung.</span><span class="sxs-lookup"><span data-stu-id="ede6b-156">Cell B3 retains its font format, which is bold.</span></span>
    
  

> <span data-ttu-id="ede6b-157">**Hinweis:** Weitere Informationen zu Momentaufnahmen finden Sie unter  [Gewusst wie: Abrufen einer kompletten Arbeitsmappe oder einer Momentaufnahme](how-to-get-an-entire-workbook-or-a-snapshot.md).</span><span class="sxs-lookup"><span data-stu-id="ede6b-157">**Note** For more information about snapshots, see  [How to: Get an Entire Workbook or a Snapshot](how-to-get-an-entire-workbook-or-a-snapshot.md).</span></span> <span data-ttu-id="ede6b-158">Weitere Informationen zu der **SetCellA1**-Methode finden Sie in der Dokumentation der Excel-Webdienste.</span><span class="sxs-lookup"><span data-stu-id="ede6b-158">For more information about the **SetCellA1** method, see the Excel Web Services reference documentation.</span></span> <span data-ttu-id="ede6b-159">Der Namespace des Webdiensts ist [Microsoft.Office.Excel.Server.WebServices](https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.WebServices.aspx).</span><span class="sxs-lookup"><span data-stu-id="ede6b-159">The namespace of the Web service is [Microsoft.Office.Excel.Server.WebServices](https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.WebServices.aspx) .</span></span>
  
    
    


## <a name="see-also"></a><span data-ttu-id="ede6b-160">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="ede6b-160">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="ede6b-161">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="ede6b-161">Tasks</span></span>


  
    
    
 [<span data-ttu-id="ede6b-162">How to: Save from Excel Client to the Server</span><span class="sxs-lookup"><span data-stu-id="ede6b-162">How to: Save from Excel Client to the Server</span></span>](how-to-save-from-excel-client-to-the-server.md)
#### <a name="reference"></a><span data-ttu-id="ede6b-163">Referenz</span><span class="sxs-lookup"><span data-stu-id="ede6b-163">Reference</span></span>


  
    
    
 [<span data-ttu-id="ede6b-164">Microsoft.Office.Excel.Server.WebServices</span><span class="sxs-lookup"><span data-stu-id="ede6b-164">Microsoft.Office.Excel.Server.WebServices</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.WebServices.aspx)
#### <a name="concepts"></a><span data-ttu-id="ede6b-165">Konzepte</span><span class="sxs-lookup"><span data-stu-id="ede6b-165">Concepts</span></span>


  
    
    
 [<span data-ttu-id="ede6b-166">Accessing the SOAP API</span><span class="sxs-lookup"><span data-stu-id="ede6b-166">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
  
    
    
 [<span data-ttu-id="ede6b-167">Loop-Back SOAP Calls and Direct Linking</span><span class="sxs-lookup"><span data-stu-id="ede6b-167">Loop-Back SOAP Calls and Direct Linking</span></span>](loop-back-soap-calls-and-direct-linking.md)
  
    
    
 [<span data-ttu-id="ede6b-168">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="ede6b-168">Excel Services Alerts</span></span>](excel-services-alerts.md)
#### <a name="other-resources"></a><span data-ttu-id="ede6b-169">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="ede6b-169">Other resources</span></span>


  
    
    
 [<span data-ttu-id="ede6b-170">Walkthrough: Developing a Custom Application Using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="ede6b-170">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
