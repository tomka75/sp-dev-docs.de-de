---
title: Speichern auf dem Server zur Vorbereitung auf programmgesteuerten Zugriff
ms.date: 09/25/2017
keywords: how to,howdoi,howto
f1_keywords: how to,howdoi,howto
ms.prod: sharepoint
ms.assetid: 80b34a29-3d40-4d11-9ba1-b4886ffcfd42
ms.openlocfilehash: 47d2d9cd97c6fff52de770b4701f2c77d830e7ed
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="save-to-the-server-to-prepare-for-programmatic-access"></a>Speichern auf dem Server zur Vorbereitung auf programmgesteuerten Zugriff

In diesem Beispiel wird gezeigt, wie Sie eine Excel-Arbeitsmappe auf dem Server zur Vorbereitung auf programmgesteuerten Zugriff speichern. Die Schritte sind wie folgt:

1. Create a workbook with named ranges.
    
  
2. Speichern Sie die Arbeitsmappe an einem vertrauenswürdigen Speicherort der SharePoint-Bibliothek. 
    
    > [!NOTE]
    > Es wird vorausgesetzt, dass Sie bereits eine SharePoint-Dokumentbibliothek erstellt und diese als vertrauenswürdigen Speicherort definiert haben. Weitere Informationen finden Sie unter [Gewusst wie: Vertrauen zu einem Standort](how-to-trust-a-location.md). 

3. Programmatically specify values for the worksheet, named range, and cell value by using the Excel Web Services **SetCellA1** method. The values are passed in as argumentsthat is, _args [1]_ and _args [2]_:
    
```cs
  
status = xlServices.SetCellA1(sessionId, String.Empty, args[1], args[2]);
```


```VB.net
  status = xlServices.SetCellA1(sessionId, String.Empty, args(1), args(2))
```


You can specify the values of  _args [1]_ and _args [2]_ by using a Web form or from the command line:
  
    
    




```
GetSnapshot.exe http://MyServer002/MyTrustedDocumentLibrary/TestMyParam.xlsx MyParam28 > MySnapshot.xlsx 
```

In this example,  _args [1]_ is **MyParam**, **args [2]** is _28_ and _GetSnapshot.exe_ is the name of the application that you create. To find a sample program, see [How to: Get an Entire Workbook or a Snapshot](how-to-get-an-entire-workbook-or-a-snapshot.md).
### <a name="to-create-a-named-range"></a>To create a named range


1. Start Excel.
    
  
2. Rename **Sheet1** to beMyParamSheet.
    
  
3. In cell B2, type 20.
    
  
4. In cell B3, type =2+B2.
    
  
5. Make cell B3 bold.
    
  
6. Make cell B2 into a named range: 
    
1. On the ribbon, click the **Formulas** tab, and then click cell B2 to select it.
    
  
2. In the **Defined Names** group, click **Define Name**.
    
  
3. In the **New Name** dialog box, in the **Name** text box, typeMyParam.
    
  
7. Save the workbook to a location of your choice on the local drive. Name the workbook TestMyParam.xlsx. 
    
  

### <a name="to-save-to-a-sharepoint-library"></a>To save to a SharePoint library


1. On the **File** menu, click **Save &amp; Send**, and then click **Save to SharePoint**. 
    
  
2. In the **Save to SharePoint** dialog box, click **Publish Options**.
    
  
3. In the **Publish Options** dialog box, on the **Show** tab, ensure that **Entire Workbook** is selected.
    
  
4. Click **Parameters**. 
    
  
5. Klicken Sie auf **Hinzufügen**.
    
  
6. In the **Add Parameters** list, you should see **MyParam**. Select the **MyParam** check box.
    
  
7. Click **OK**. You should now see **MyParam** in the **Parameters** list.
    
  
8. Klicken Sie auf **OK**.
    
  
9. In the **Save to SharePoint** dialog box, click **Save As**.
    
  
10. In the **Save As** dialog box, clear the **Open with Excel in the browser** check box.
    
  
11. In the **File name** box, type the path to the trusted SharePoint document library where you want to store this workbook. For example,http:// _MyServer002_/MyDocumentLibrary/TestParam.xlsx.
    
  
12. Klicken Sie auf **Speichern**.
    
  

### <a name="to-specify-values-programmatically"></a>To specify values programmatically


1. Following is the signature for the **SetCellA1** method in Excel Web Services:
    
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

2. In the preceding code: 
    
  -  _args [1]_ is the name of the named range. In this example, it is **MyParam**.
    
  
  -  _args [2]_ is the value that you want to set in the cell. The cell where the value will be set is the named range in _args [1]_ called **MyParam**.
    
  
3. If you are using a command line, you can pass in the arguments as follows:
    
     `GetSnapshot.exe http://` _MyServer002_ `/` _MyTrustedDocumentLibrary_ `/TestMyParam.xlsx MyParam 28 > MySnapshot.xlsx`
    
  
4. If you generate a snapshot of the workbook, you see the following: 
    
  - Cell B2 (with the named range **MyParam**) now has a value that you fed through the program, which is **28**.
    
  
  - Cell B3 has a new calculated value of **30**.
    
  
  - Cell B3 does not show the original formula, which was "=2+B2".
    
  
  - Zelle B3 behält die Schriftformatierung bei, d. h. Fettformatierung.
    
  

> [!NOTE]
> Weitere Informationen zu Momentaufnahmen finden Sie unter [Gewusst wie: Abrufen einer kompletten Arbeitsmappe oder einer Momentaufnahme](how-to-get-an-entire-workbook-or-a-snapshot.md). Weitere Informationen zu der **SetCellA1**-Methode finden Sie in der Dokumentation der Excel-Webdienste. Der Namespace des Webdiensts ist [Microsoft.Office.Excel.Server.WebServices]((https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.WebServices.aspx)).
  
    
    


## <a name="see-also"></a>Siehe auch


#### <a name="tasks"></a>Aufgaben


  
    
    
 [How to: Save from Excel Client to the Server](how-to-save-from-excel-client-to-the-server.md)
#### <a name="reference"></a>Referenz


  
    
    
 [Microsoft.Office.Excel.Server.WebServices]((https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.WebServices.aspx))
#### <a name="concepts"></a>Konzepte


  
    
    
 [Accessing the SOAP API](accessing-the-soap-api.md)
  
    
    
 [Loop-Back SOAP Calls and Direct Linking](loop-back-soap-calls-and-direct-linking.md)
  
    
    
 [Excel Services Alerts](excel-services-alerts.md)
#### <a name="other-resources"></a>Sonstige Ressourcen


  
    
    
 [Walkthrough: Developing a Custom Application Using Excel Web Services](walkthrough-developing-a-custom-application-using-excel-web-services.md)
