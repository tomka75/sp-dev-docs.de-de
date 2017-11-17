---
title: How to Set Values of Ranges
ms.date: 09/25/2017
keywords: how to,howdoi,howto,set range
f1_keywords: how to,howdoi,howto,set range
ms.prod: sharepoint
ms.assetid: ccc7e204-f857-45a9-81ec-3a8484e6d454
ms.openlocfilehash: 124be9f8cc71e14976913ec77a92d60a1a34cd03
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-set-values-of-ranges"></a><span data-ttu-id="1e587-103">How to: Set Values of Ranges</span><span class="sxs-lookup"><span data-stu-id="1e587-103">How to: Set Values of Ranges</span></span>

<span data-ttu-id="1e587-104">Excel Web Services bietet vier Methoden zum Festlegen von Werten in einer Excel-Arbeitsmappe: **SetCell**, **SetCellA1**, **SetRange** und **SetRangeA1**.</span><span class="sxs-lookup"><span data-stu-id="1e587-104">Excel Web Services exposes four methods for setting values into an Excel workbook: **SetCell**, **SetCellA1**, **SetRange**, and **SetRangeA1**.</span></span> 
  
    
    


> <span data-ttu-id="1e587-105">**Hinweis:** Wenn Sie Änderungen an einer Arbeitsmappe vornehmen, z. B. durch Festlegen von Werten für einen Bereich mithilfe von Excel Web Services, bleiben die Änderungen an der Arbeitsmappe nur für diese bestimmte Sitzung erhalten.</span><span class="sxs-lookup"><span data-stu-id="1e587-105">**Note** When you make changes to a workbook—for example, by setting values to a range by using Excel Web Services—the changes to the workbook are preserved only for that particular session. The changes are not saved or persisted back to the original workbook. When the current workbook session ends (for example, when you call the CloseWorkbook method, or when the session times out), changes that you made are lost.</span></span> <span data-ttu-id="1e587-106">Die Änderungen werden nicht in der ursprünglichen Arbeitsmappe gespeichert oder persistent gemacht.</span><span class="sxs-lookup"><span data-stu-id="1e587-106">The changes are not saved or persisted back to the original workbook.</span></span> <span data-ttu-id="1e587-107">Wenn die aktuelle Arbeitsmappensitzung endet (z. B. beim Aufruf der Methode **CloseWorkbook** oder bei einem Sitzungstimeout), gehen die vorgenommenen Änderungen verloren.> Wenn Sie Änderungen speichern möchten, die Sie an einer Arbeitsmappe vornehmen, können Sie die Methode **GetWorkbook** verwenden und die Arbeitsmappe dann mit der API der Zieldatei speichern.</span><span class="sxs-lookup"><span data-stu-id="1e587-107">Note When you make changes to a workbook—for example, by setting values to a range using Excel Web Services—the changes to the workbook are preserved only for that particular session. The changes are not saved or persisted back to the original workbook. When the current workbook session ends (for example, when you call the **CloseWorkbook** method, or the session times out), changes you made will be lost.> If you want to save changes you make to a workbook, you can use the **GetWorkbook** method and then save the workbook using the API of the destination file store. For more information, see How to: Get an Entire Workbook or a Snapshot and How to: Save a Workbook.</span></span> <span data-ttu-id="1e587-108">Weitere Informationen finden Sie unter [Abrufen einer kompletten Arbeitsmappe oder einer Momentaufnahme](how-to-get-an-entire-workbook-or-a-snapshot.md) und [Vorgehensweise: Speichern einer Arbeitsmappe](http://msdn.microsoft.com/library/feb74f7a-2d8f-4672-911b-de85f8852aea%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e587-108">For more information, see [How to: Get an Entire Workbook or a Snapshot](how-to-get-an-entire-workbook-or-a-snapshot.md) and [How to: Save a Workbook](http://msdn.microsoft.com/library/feb74f7a-2d8f-4672-911b-de85f8852aea%28Office.15%29.aspx).</span></span> 
  
    
    


<span data-ttu-id="1e587-p102">Use the **SetCell** and **SetCellA1** methods to set values in a single cell. If you try to set values in a range of cellsfor example, by passing in a range reference such as "D3:G5" or a named range that is larger than a single cell, and so onyour method call will fail. If you want to set values in a range of cells, use the **SetRange** and **SetRangeA1** methods instead.</span><span class="sxs-lookup"><span data-stu-id="1e587-p102">Use the **SetCell** and **SetCellA1** methods to set values in a single cell. If you try to set values in a range of cells—for example, by passing in a range reference such as "D3:G5" or a named range that is larger than a single cell, and so on—your method call will fail. If you want to set values in a range of cells, use the **SetRange** and **SetRangeA1** methods instead.</span></span>
  
    
    

<span data-ttu-id="1e587-p103">Methods that have the A1 suffix ( **SetCellA1** and **SetRangeA1**) use a different coordinate system than those that do not ( **SetCell** and **SetRange**). If you want to use Excel-style references to cells, such as range references (for example, H8, A3:D5, Sheet2!A12:G18) or named ranges, you should use the methods with the A1 suffix. Those methods allow you to pass in the name of a sheet and range.If you want to access an Excel range by using a numeric coordinate system, you should use the methods that do not have the A1 suffix. It is easier to use range coordinates when you have code that iterates through a set of cells in a loop, or when the range coordinates are calculated dynamically as part of the algorithm.The row and column coordinates of a cell are 0-based. Therefore, "0,0" will return cell A1, as in this example:</span><span class="sxs-lookup"><span data-stu-id="1e587-p103">Methods that have the A1 suffix ( **SetCellA1** and **SetRangeA1**) use a different coordinate system than those that do not ( **SetCell** and **SetRange**). If you want to use Excel-style references to cells, such as range references (for example, H8, A3:D5, Sheet2!A12:G18) or named ranges, you should use the methods with the A1 suffix. Those methods allow you to pass in the name of a sheet and range.If you want to access an Excel range by using a numeric coordinate system, you should use the methods that do not have the A1 suffix. It is easier to use range coordinates when you have code that iterates through a set of cells in a loop, or when the range coordinates are calculated dynamically as part of the algorithm.The row and column coordinates of a cell are 0-based. Therefore, "0,0" will return cell A1, as in this example:</span></span>


```cs

// Call the SetCell method to set a value, 8, into a cell.
// The cell is in the first row and first column; that is, cell A1.
xlservice.SetCell(sessionId, sheetName, 0, 0, 8);
```




```VB.net

' Call the SetCell method to set a value, 8, into a cell.
' The cell is in the first row and first column; that is, cell A1.
xlservice.SetCell(sessionId, sheetName, 0, 0, 8)
```

<span data-ttu-id="1e587-p104">If you are getting values from multiple adjacent cells, you may want to consider using the **SetRange** method instead of making multiple calls to the **SetCell** method. This results in a single round trip to the server instead of multiple round trips. Therefore, in some cases, you may gain a noticeable performance improvement by using the **SetRange** method instead of the **SetCell** method.When setting values into a range of cells using the **SetRange** and **SetRangeA1** methods, you use an object array ( **object[]** in C# and **Object ()** in Visual Basic .NET). The object array is actually a jagged array; each entry in the array is another array of objects representing the cells. For more information about jagged arrays, see [Jagged Arrays (C# Programming Guide)](http://go.microsoft.com/fwlink/?LinkId=65619) (http://msdn.microsoft.com/de-DE/library/2s05feca.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e587-p104">If you are getting values from multiple adjacent cells, you may want to consider using the **SetRange** method instead of making multiple calls to the **SetCell** method. This results in a single round trip to the server instead of multiple round trips. Therefore, in some cases, you may gain a noticeable performance improvement by using the **SetRange** method instead of the **SetCell** method.When setting values into a range of cells using the **SetRange** and **SetRangeA1** methods, you use an object array ( **object[]** in C# and **Object ()** in Visual Basic .NET). The object array is actually a jagged array; each entry in the array is another array of objects representing the cells. For more information about jagged arrays, see [Jagged Arrays (C# Programming Guide)](http://go.microsoft.com/fwlink/?LinkId=65619) (http://msdn.microsoft.com/en-us/library/2s05feca.aspx).</span></span>
### <a name="to-set-values-by-using-the-setcell-and-setrange-methods"></a><span data-ttu-id="1e587-122">To set values by using the SetCell and SetRange methods</span><span class="sxs-lookup"><span data-stu-id="1e587-122">To set values by using the SetCell and SetRange methods</span></span>


1. <span data-ttu-id="1e587-123">Use the **SetCell** method to set a value in a cell in the open workbook by using numeric range coordinates:</span><span class="sxs-lookup"><span data-stu-id="1e587-123">Use the **SetCell** method to set a value in a cell in the open workbook by using numeric range coordinates:</span></span>
    
```cs
  
// Instantiate the Web service and make a status array object.
ExcelService xlservice = new ExcelService();
Status[] outStatus;
RangeCoordinates rangeCoordinates = new RangeCoordinates();
string sheetName = "Sheet2";

// Set the path to a workbook.
// The workbook must be in a trusted location.
string targetWorkbookPath = "http://myserver02/example/Shared%20Documents/Book1.xlsx";

// Set credentials for requests.
xlservice.Credentials = System.Net.CredentialCache.DefaultCredentials;

// Call the open workbook, and point to the trusted 
// location of the workbook to open.
string sessionId = xlservice.OpenWorkbook(targetWorkbookPath, "en-US", "en-US", out outStatus);

// Call the SetCell method to set the cell's value to 28.
// The cell is in the ninth row and second column, which is cell B9.
xlservice.SetCell(sessionId, sheetName, 8, 1, 28);
```


```
  
' Instantiate the Web service and make a status array object.
Dim xlservice As New ExcelService()
Dim outStatus() As Status
Dim rangeCoordinates As New RangeCoordinates()
Dim sheetName As String = "Sheet2"

' Set the path to a workbook.
' The workbook must be in a trusted location.
Dim targetWorkbookPath As String = "http://myserver02/example/Shared%20Documents/Book1.xlsx"

' Set credentials for requests.
xlservice.Credentials = System.Net.CredentialCache.DefaultCredentials

' Call the open workbook, and point to the trusted 
' location of the workbook to open.
Dim sessionId As String = xlservice.OpenWorkbook(targetWorkbookPath, "en-US", "en-US", outStatus)

' Call the SetCell method to set the cell's value to 28.
' The cell is in the ninth row and second column, which is cell B9.
xlservice.SetCell(sessionId, sheetName, 8, 1, 28)

```

2. <span data-ttu-id="1e587-124">Use the **SetRange** method to set values in a range in the open workbook by using numeric range coordinates:</span><span class="sxs-lookup"><span data-stu-id="1e587-124">Use the **SetRange** method to set values in a range in the open workbook by using numeric range coordinates:</span></span>
    
```cs
  
// Instantiate the Web service and make a status array object.
ExcelService xlservice = new ExcelService();
Status[] outStatus;
RangeCoordinates rangeCoordinates = new RangeCoordinates();

...
private void Form1_Load(object sender, EventArgs e)
{
...
...
//Prepare object to define range coordinates
//and call the GetRange method.
//startCol, startRow, startHeight, and startWidth
//get their values from user input.
rangeCoordinates.Column = (int)startCol.Value;
rangeCoordinates.Row = (int)startRow.Value;
rangeCoordinates.Height = (int)startHeight.Value;
rangeCoordinates.Width = (int)startWidth.Value;
...
...
}
private void SetRangeButton_Click(object sender, EventArgs e)
{
object[] values = new object[rangeCoordinates.Height];
string[] fieldValues =    
    SetRangeTextBox.Text.Split((",").ToCharArray());

if (fieldValues.Length != rangeCoordinates.Height * 
rangeCoordinate.Width)
    {
        throw new Exception("The number of inputs (" + 
            fieldValues.Length + ") does not match" +
            " the product of Height (" +             rangeCoordinates.Height + ") and Width (" + 
            rangeCoordinates.Width + ")");
    }

for (int i = 0; i < rangeCoordinates.Height; i++)
    {
        object[] currentRow = 
            new object[rangeCoordinates.Width];
        for (int j = 0; j < rangeCoordinates.Width; j++)
        {
            currentRow[j] = fieldValues[i *             rangeCoordinates.Width + j];
        }
        values[i] = currentRow;
    }

SetStatusText("Waiting for SetRange...");
outStatus = xlservice.SetRange(
    sessionID, SheetNameTextBox.Text, 
    rangeCoordinates, values);
}
catch (SoapException exc)
{
StopTimer("SetRange");
GenerateErrorMessage("SetRange", exc);
}
catch (Exception exc)
{
StopTimer("SetRange");
GenerateToolErrorMessage("While calling SetRange", exc);
}
}

```


```VB.net
  
' Instantiate the Web service and make a status array object.
Private xlservice As New ExcelService()
Private outStatus() As Status
Private rangeCoordinates As New RangeCoordinates()

...
Private Sub Form1_Load(ByVal sender As Object, ByVal e As EventArgs)
...
...
'Prepare object to define range coordinates
'and call the GetRange method.
'startCol, startRow, startHeight, and startWidth
'get their values from user input.
rangeCoordinates.Column = CInt(Fix(startCol.Value))
rangeCoordinates.Row = CInt(Fix(startRow.Value))
rangeCoordinates.Height = CInt(Fix(startHeight.Value))
rangeCoordinates.Width = CInt(Fix(startWidth.Value))
...
...
End Sub
Private Sub SetRangeButton_Click(ByVal sender As Object, ByVal e As EventArgs)
Dim values(rangeCoordinates.Height - 1) As Object
Dim fieldValues() As String = SetRangeTextBox.Text.Split((",").ToCharArray())

If fieldValues.Length <> rangeCoordinates.Height * rangeCoordinate.Width Then
        Throw New Exception("The number of inputs (" &amp; fieldValues.Length &amp; ") does not match" &amp; " the product of Height (" &amp; rangeCoordinates.Height &amp; ") and Width (" &amp; rangeCoordinates.Width &amp; ")")
End If

For i As Integer = 0 To rangeCoordinates.Height - 1
        Dim currentRow(rangeCoordinates.Width - 1) As Object
        For j As Integer = 0 To rangeCoordinates.Width - 1
            currentRow(j) = fieldValues(i * rangeCoordinates.Width + j)
        Next j
        values(i) = currentRow
Next i
Try
SetStatusText("Waiting for SetRange...")
outStatus = xlservice.SetRange(sessionID, SheetNameTextBox.Text, rangeCoordinates, values)
Catch exc As SoapException
StopTimer("SetRange")
GenerateErrorMessage("SetRange", exc)
Catch exc As Exception
StopTimer("SetRange")
GenerateToolErrorMessage("While calling SetRange", exc)
End Try
End Sub
```


### <a name="to-set-values-by-using-the-setcella1-and-setrangea1-methods"></a><span data-ttu-id="1e587-125">To set values by using the SetCellA1 and SetRangeA1 methods</span><span class="sxs-lookup"><span data-stu-id="1e587-125">To set values by using the SetCellA1 and SetRangeA1 methods</span></span>


1. <span data-ttu-id="1e587-126">Use the **SetCellA1** method to set a value in a cell in the open workbook, using the Excel "A1" range specification:</span><span class="sxs-lookup"><span data-stu-id="1e587-126">Use the **SetCellA1** method to set a value in a cell in the open workbook, using the Excel "A1" range specification:</span></span>
    
```cs
  
// Instantiate the Web service and make a status array object.
ExcelService xlservice = new ExcelService();
Status[] outStatus;

xlservice.SetCellA1(sessionId, String.Empty, "InterestRateParam", 8);
```


```VB.net
  
' Instantiate the Web service and make a status array object.
Dim xlservice As New ExcelService()
Dim outStatus() As Status

xlservice.SetCellA1(sessionId, String.Empty, "InterestRateParam", 8)
```

2. <span data-ttu-id="1e587-127">Use the **SetRangeA1** method to get a value from a range in the open workbook, using the Excel "A1" range specification:</span><span class="sxs-lookup"><span data-stu-id="1e587-127">Use the **SetRangeA1** method to get a value from a range in the open workbook, using the Excel "A1" range specification:</span></span>
    
```cs
  
// Instantiate the Web service and make a status array object.
ExcelService xlservice = new ExcelService();
Status[] outStatus;
...

void SetRangeA1Button_ServerClick(object sender, EventArgs e)
{
    int height, width;
    CalculateHeightAndWidth(RangeNameTextBox5.Value.Trim(), 
        out height, out width);

    object[] values = new object[height];
    string[] fieldValues = 
        RangeValuesTextBox1.Value.Split((",").ToCharArray());
    if (fieldValues.Length != height * width)
    {
        throw new Exception("The number of inputs (" + 
            fieldValues.Length + ") does not match" +
            " the product of Height (" + height + ") and 
            Width (" + width + ")");
    }

    for (int i = 0; i < height; i++)
    {
        object[] currentRow = new object[width];
        for (int j = 0; j < width; j++)
        {
            currentRow[j] = fieldValues[i * width + j];
        }
        values[i] = currentRow;
    }
    try
    {
        xlservice.SetRangeA1(SessionIDTextBox.Value, 
            SheetNameTextBox1.Value,RangeNameTextBox5.Value,
            values, out outStatus);
    }
    catch (SoapException exc)
    {
        ExceptionTextBox1.Value = exc.Message;
    }

}
```


```VB.net
  
' Instantiate the Web service and make a status array object.
Private xlservice As New ExcelService()
Private outStatus() As Status
...

Private Sub SetRangeA1Button_ServerClick(ByVal sender As Object, ByVal e As EventArgs)
    Dim height, width As Integer
    CalculateHeightAndWidth(RangeNameTextBox5.Value.Trim(), height, width)

    Dim values(height - 1) As Object
    Dim fieldValues() As String = RangeValuesTextBox1.Value.Split((",").ToCharArray())
    If fieldValues.Length <> height * width Then
        Throw New Exception("The number of inputs (" &amp; fieldValues.Length &amp; ") does not match" &amp; " the product of Height (" &amp; height &amp; ") and Width (" &amp; width &amp; ")")
    End If

    For i As Integer = 0 To height - 1
        Dim currentRow(width - 1) As Object
        For j As Integer = 0 To width - 1
            currentRow(j) = fieldValues(i * width + j)
        Next j
        values(i) = currentRow
    Next i
    Try
        xlservice.SetRangeA1(SessionIDTextBox.Value, SheetNameTextBox1.Value,RangeNameTextBox5.Value, values, outStatus)
    Catch exc As SoapException
        ExceptionTextBox1.Value = exc.Message
    End Try

End Sub
```


## <a name="see-also"></a><span data-ttu-id="1e587-128">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="1e587-128">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="1e587-129">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="1e587-129">Tasks</span></span>


  
    
    
 [<span data-ttu-id="1e587-130">How to: Specify a Range Address and Sheet Name</span><span class="sxs-lookup"><span data-stu-id="1e587-130">How to: Specify a Range Address and Sheet Name</span></span>](how-to-specify-a-range-address-and-sheet-name.md)
  
    
    
 [<span data-ttu-id="1e587-131">How to: Get Values from Ranges</span><span class="sxs-lookup"><span data-stu-id="1e587-131">How to: Get Values from Ranges</span></span>](how-to-get-values-from-ranges.md)
#### <a name="concepts"></a><span data-ttu-id="1e587-132">Konzepte</span><span class="sxs-lookup"><span data-stu-id="1e587-132">Concepts</span></span>


  
    
    
 [<span data-ttu-id="1e587-133">Accessing the SOAP API</span><span class="sxs-lookup"><span data-stu-id="1e587-133">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
#### <a name="other-resources"></a><span data-ttu-id="1e587-134">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="1e587-134">Other resources</span></span>


  
    
    
 [<span data-ttu-id="1e587-135">Walkthrough: Developing a Custom Application Using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="1e587-135">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
