---
title: Step 4 Testing and Calling UDFs from Cells
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d3e6aa72-2eb8-4b4b-a0eb-273486890d00
ms.openlocfilehash: 0227b7961e0d533e3c35af13ceb707642cb911ea
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="step-4-testing-and-calling-udfs-from-cells"></a>Step 4: Testing and Calling UDFs from Cells

In this step, you will test the SampleUdf.dll assembly you created, deployed, and enabled in the previous steps. To test the user-defined function (UDF), you will:
  
    
    


1. Create a workbook with a named range and formulas that call the functions in SampleUdf.dll.
    
  
2. Speichern Sie die Arbeitsmappe in einer SharePoint-Dokumentbibliothek, die einen vertrauenswürdigen Speicherort darstellt.
    
    > [!NOTE]
    > Es wird vorausgesetzt, dass Sie bereits eine SharePoint-Dokumentbibliothek erstellt und diese als vertrauenswürdigen Speicherort definiert haben. Informationen dazu, wie Sie einen Speicherort als vertrauenswürdig einstufen, finden Sie im Abschnitt [Schritt 3: Bereitstellen und Aktivieren von UDFs](step-3-deploying-and-enabling-udfs.md). 

3. Ändern Sie die Parameter, um die Arbeitsmappe neu zu berechnen.
    
  

## <a name="testing-udfs"></a>Testing UDFs


### <a name="to-call-udfs-from-cells"></a>To call UDFs from cells


1. Start Microsoft Office Excel 2007.
    
  
2. In cell A1, type the formula to call the  `MyDouble` function in SampleUdf.dll. The `MyDouble` function takes an argument of type **double**. In this example, you will take the argument from cell B1. In cell A1, type =MyDouble(B1).
    
    > [!NOTE]
    > Die Formel lautet „#NAME?“ in Excel. Diese Formel wird nur verwendet, wenn die Arbeitsmappe in Excel Services angezeigt wird. 

    > [!NOTE]
    > Sie können UDFs sowohl auf dem Client als auch auf dem Server ausführen. Einzelheiten dazu werden in einem noch in MSDN zu veröffentlichenden Artikel erklärt, bleiben hier jedoch aus Gründen der Einfachheit unberücksichtigt. 

3. Geben Sie in Zelle B1 die Zahl 8 ein.
    
  
4. Make cell B1 a named range. First click the **Formulas** tab. Then click cell B1 to select it. On the **Formulas** tab, in the **Named Cells** group, click **Name a Range**. In the **New Name** dialog box, in the **Name** box, type **MyDoubleParam**.
    
  
5. In cell A2, type the formula to call the  `ReturnDateTimeToday` function. Type=ReturnDateTimeToday().
    
  
6. In cell A3, type the formula to call the  `ReturnDateTimeToday` function. Type=ReturnDateTimeToday(). Next, right-click cell A3 to display the menu. Click **Format Cells**.
    
  
7. In the **Format Cells** dialog box, on the **Number** tab, select **Date**. Select a date format type from the **Type** listfor example, *3/4/2001.
    
  
8. Klicken Sie auf **OK**.
    
  
9. Save the workbook to a location of your choice on the local drive. Name the workbook "TestSampleUdf.xlsx". 
    
  

### <a name="to-save-to-excel-services"></a>To save to Excel Services


1. Click the **Microsoft Office Button**, point to **Save As**, and click **Save for Excel Services**. 
    
  
2. In the **Save As** dialog box, click **Excel Services Options**.
    
  
3. In the **Excel Services Options** dialog box, on the **Show** tab, make sure that **Entire Workbook** is selected.
    
  
4. Click **Parameters**. 
    
  
5. In the **Add Parameters** list, select the **MyDoubleParam** check box.
    
  
6. Click **OK**. You should now see "MyDoubleParam" listed in the **Parameters** list.
    
  
7. Klicken Sie auf **OK**.
    
  
8. In the **Save As** dialog box, make sure that the **Open this workbook in my browser after I save** check box is selected.
    
  
9. In the **File name** box, type the path to the trusted SharePoint document library where you want to store this workbook. For example, _http://MyServer002/Shared%20Documents/TestSampleUdf.xlsx_.
    
  
10. Click **Save**. You should see TestSampleUdf.xlsx in Excel Web Access. In cell A1, you should see the number "72" because cell B1 * 9 = 8 * 9, which is 72. In cell A2 you should see a number. In cell A3, you should see the current date. 
    
    > [!NOTE]
    > Die Zahl in Zelle A2 stellt die Anzahl der Tage seit 1/1/1900 (bzw. 1/1/1904, wenn 1904-Datumswerte verwenden aktiviert ist) dar. So werden Datumsangaben in Excel intern dargestellt. 

### <a name="to-change-parameters-to-test-the-udf"></a>Ändern von Parametern zum Testen der UDF


1. In the **Parameters** pane, you should see the named range for cell B1, that is, "MyDoubleParam".
    
  
2. You can change the value in cell B1 by typing a number in the box next to "MyDoubleParam". For example, if you type 3 and then click **Apply**, Excel Services will recalculate the workbook. Cell A1 will contain "27" instead of "72". 
    
  

## <a name="see-also"></a>Siehe auch


#### <a name="tasks"></a>Aufgaben


  
    
    
 [Step 1: Creating a Project and Adding a UDF Reference](step-1-creating-a-project-and-adding-a-udf-reference.md)
  
    
    
 [Step 2: Creating a Managed-Code UDF](step-2-creating-a-managed-code-udf.md)
  
    
    
 [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [How to: Create a UDF That Calls a Web Service](how-to-create-a-udf-that-calls-a-web-service.md)
#### <a name="concepts"></a>Konzepte


  
    
    
 [Walkthrough: Developing a Managed-Code UDF](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [Understanding Excel Services UDFs](understanding-excel-services-udfs.md)
