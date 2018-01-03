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
# <a name="step-4-testing-and-calling-udfs-from-cells"></a><span data-ttu-id="09e4d-102">Step 4: Testing and Calling UDFs from Cells</span><span class="sxs-lookup"><span data-stu-id="09e4d-102">Step 4: Testing and Calling UDFs from Cells</span></span>

<span data-ttu-id="09e4d-p101">In this step, you will test the SampleUdf.dll assembly you created, deployed, and enabled in the previous steps. To test the user-defined function (UDF), you will:</span><span class="sxs-lookup"><span data-stu-id="09e4d-p101">In this step, you will test the SampleUdf.dll assembly you created, deployed, and enabled in the previous steps. To test the user-defined function (UDF), you will:</span></span>
  
    
    


1. <span data-ttu-id="09e4d-105">Create a workbook with a named range and formulas that call the functions in SampleUdf.dll.</span><span class="sxs-lookup"><span data-stu-id="09e4d-105">Create a workbook with a named range and formulas that call the functions in SampleUdf.dll.</span></span>
    
  
2. <span data-ttu-id="09e4d-106">Speichern Sie die Arbeitsmappe in einer SharePoint-Dokumentbibliothek, die einen vertrauenswürdigen Speicherort darstellt.</span><span class="sxs-lookup"><span data-stu-id="09e4d-106">Save the workbook to a SharePoint document library that is a trusted location.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="09e4d-107">Es wird vorausgesetzt, dass Sie bereits eine SharePoint-Dokumentbibliothek erstellt und diese als vertrauenswürdigen Speicherort definiert haben.</span><span class="sxs-lookup"><span data-stu-id="09e4d-107">Note: It is assumed that you have already created a SharePoint document library and made it a trusted location.</span></span> <span data-ttu-id="09e4d-108">Informationen dazu, wie Sie einen Speicherort als vertrauenswürdig einstufen, finden Sie im Abschnitt [Schritt 3: Bereitstellen und Aktivieren von UDFs](step-3-deploying-and-enabling-udfs.md).</span><span class="sxs-lookup"><span data-stu-id="09e4d-108">For information about how to trust a location, see the "Trusting a Location" section in  [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md).</span></span> 

3. <span data-ttu-id="09e4d-109">Ändern Sie die Parameter, um die Arbeitsmappe neu zu berechnen.</span><span class="sxs-lookup"><span data-stu-id="09e4d-109">Change parameters to recalculate the workbook.</span></span>
    
  

## <a name="testing-udfs"></a><span data-ttu-id="09e4d-110">Testing UDFs</span><span class="sxs-lookup"><span data-stu-id="09e4d-110">Testing UDFs</span></span>


### <a name="to-call-udfs-from-cells"></a><span data-ttu-id="09e4d-111">To call UDFs from cells</span><span class="sxs-lookup"><span data-stu-id="09e4d-111">To call UDFs from cells</span></span>


1. <span data-ttu-id="09e4d-112">Start Microsoft Office Excel 2007.</span><span class="sxs-lookup"><span data-stu-id="09e4d-112">Start Microsoft Office Excel 2007.</span></span>
    
  
2. <span data-ttu-id="09e4d-p103">In cell A1, type the formula to call the  `MyDouble` function in SampleUdf.dll. The `MyDouble` function takes an argument of type **double**. In this example, you will take the argument from cell B1. In cell A1, type =MyDouble(B1).</span><span class="sxs-lookup"><span data-stu-id="09e4d-p103">In cell A1, type the formula to call the  `MyDouble` function in SampleUdf.dll. The `MyDouble` function takes an argument of type **double**. In this example, you will take the argument from cell B1. In cell A1, type =MyDouble(B1).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="09e4d-117">Die Formel lautet „#NAME?“</span><span class="sxs-lookup"><span data-stu-id="09e4d-117">Note: The formula will evaluate to "#NAME?"</span></span> <span data-ttu-id="09e4d-118">in Excel.</span><span class="sxs-lookup"><span data-stu-id="09e4d-118">in Excel.</span></span> <span data-ttu-id="09e4d-119">Diese Formel wird nur verwendet, wenn die Arbeitsmappe in Excel Services angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="09e4d-119">The formula will be evaluated only when the workbook is displayed in Excel Services.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="09e4d-p105">Sie können UDFs sowohl auf dem Client als auch auf dem Server ausführen. Einzelheiten dazu werden in einem noch in MSDN zu veröffentlichenden Artikel erklärt, bleiben hier jedoch aus Gründen der Einfachheit unberücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="09e4d-p105">You can run UDFs on both the client and server. A future article published on MSDN will explain the details. They are omitted here for the sake of simplicity.</span></span> 

3. <span data-ttu-id="09e4d-123">Geben Sie in Zelle B1 die Zahl 8 ein.</span><span class="sxs-lookup"><span data-stu-id="09e4d-123">In cell B1, type the number 8.</span></span>
    
  
4. <span data-ttu-id="09e4d-p106">Make cell B1 a named range. First click the **Formulas** tab. Then click cell B1 to select it. On the **Formulas** tab, in the **Named Cells** group, click **Name a Range**. In the **New Name** dialog box, in the **Name** box, type **MyDoubleParam**.</span><span class="sxs-lookup"><span data-stu-id="09e4d-p106">Make cell B1 a named range. First click the **Formulas** tab. Then click cell B1 to select it. On the **Formulas** tab, in the **Named Cells** group, click **Name a Range**. In the **New Name** dialog box, in the **Name** box, type **MyDoubleParam**.</span></span>
    
  
5. <span data-ttu-id="09e4d-p107">In cell A2, type the formula to call the  `ReturnDateTimeToday` function. Type=ReturnDateTimeToday().</span><span class="sxs-lookup"><span data-stu-id="09e4d-p107">In cell A2, type the formula to call the  `ReturnDateTimeToday` function. Type=ReturnDateTimeToday().</span></span>
    
  
6. <span data-ttu-id="09e4d-p108">In cell A3, type the formula to call the  `ReturnDateTimeToday` function. Type=ReturnDateTimeToday(). Next, right-click cell A3 to display the menu. Click **Format Cells**.</span><span class="sxs-lookup"><span data-stu-id="09e4d-p108">In cell A3, type the formula to call the  `ReturnDateTimeToday` function. Type=ReturnDateTimeToday(). Next, right-click cell A3 to display the menu. Click **Format Cells**.</span></span>
    
  
7. <span data-ttu-id="09e4d-p109">In the **Format Cells** dialog box, on the **Number** tab, select **Date**. Select a date format type from the **Type** listfor example, *3/4/2001.</span><span class="sxs-lookup"><span data-stu-id="09e4d-p109">In the **Format Cells** dialog box, on the **Number** tab, select **Date**. Select a date format type from the **Type** list—for example, *3/4/2001.</span></span>
    
  
8. <span data-ttu-id="09e4d-136">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="09e4d-136">Click **OK**.</span></span>
    
  
9. <span data-ttu-id="09e4d-p110">Save the workbook to a location of your choice on the local drive. Name the workbook "TestSampleUdf.xlsx".</span><span class="sxs-lookup"><span data-stu-id="09e4d-p110">Save the workbook to a location of your choice on the local drive. Name the workbook "TestSampleUdf.xlsx".</span></span> 
    
  

### <a name="to-save-to-excel-services"></a><span data-ttu-id="09e4d-139">To save to Excel Services</span><span class="sxs-lookup"><span data-stu-id="09e4d-139">To save to Excel Services</span></span>


1. <span data-ttu-id="09e4d-140">Click the **Microsoft Office Button**, point to **Save As**, and click **Save for Excel Services**.</span><span class="sxs-lookup"><span data-stu-id="09e4d-140">Click the **Microsoft Office Button**, point to **Save As**, and click **Save for Excel Services**.</span></span> 
    
  
2. <span data-ttu-id="09e4d-141">In the **Save As** dialog box, click **Excel Services Options**.</span><span class="sxs-lookup"><span data-stu-id="09e4d-141">In the **Save As** dialog box, click **Excel Services Options**.</span></span>
    
  
3. <span data-ttu-id="09e4d-142">In the **Excel Services Options** dialog box, on the **Show** tab, make sure that **Entire Workbook** is selected.</span><span class="sxs-lookup"><span data-stu-id="09e4d-142">In the **Excel Services Options** dialog box, on the **Show** tab, make sure that **Entire Workbook** is selected.</span></span>
    
  
4. <span data-ttu-id="09e4d-143">Click **Parameters**.</span><span class="sxs-lookup"><span data-stu-id="09e4d-143">Click **Parameters**.</span></span> 
    
  
5. <span data-ttu-id="09e4d-144">In the **Add Parameters** list, select the **MyDoubleParam** check box.</span><span class="sxs-lookup"><span data-stu-id="09e4d-144">In the **Add Parameters** list, select the **MyDoubleParam** check box.</span></span>
    
  
6. <span data-ttu-id="09e4d-p111">Click **OK**. You should now see "MyDoubleParam" listed in the **Parameters** list.</span><span class="sxs-lookup"><span data-stu-id="09e4d-p111">Click **OK**. You should now see "MyDoubleParam" listed in the **Parameters** list.</span></span>
    
  
7. <span data-ttu-id="09e4d-147">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="09e4d-147">Click **OK**.</span></span>
    
  
8. <span data-ttu-id="09e4d-148">In the **Save As** dialog box, make sure that the **Open this workbook in my browser after I save** check box is selected.</span><span class="sxs-lookup"><span data-stu-id="09e4d-148">In the **Save As** dialog box, make sure that the **Open this workbook in my browser after I save** check box is selected.</span></span>
    
  
9. <span data-ttu-id="09e4d-p112">In the **File name** box, type the path to the trusted SharePoint document library where you want to store this workbook. For example, _http://MyServer002/Shared%20Documents/TestSampleUdf.xlsx_.</span><span class="sxs-lookup"><span data-stu-id="09e4d-p112">In the **File name** box, type the path to the trusted SharePoint document library where you want to store this workbook. For example, _http://MyServer002/Shared%20Documents/TestSampleUdf.xlsx_.</span></span>
    
  
10. <span data-ttu-id="09e4d-p113">Click **Save**. You should see TestSampleUdf.xlsx in Excel Web Access. In cell A1, you should see the number "72" because cell B1 * 9 = 8 * 9, which is 72. In cell A2 you should see a number. In cell A3, you should see the current date.</span><span class="sxs-lookup"><span data-stu-id="09e4d-p113">Click **Save**. You should see TestSampleUdf.xlsx in Excel Web Access. In cell A1, you should see the number "72" because cell B1 * 9 = 8 * 9, which is 72. In cell A2 you should see a number. In cell A3, you should see the current date.</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="09e4d-p114">Die Zahl in Zelle A2 stellt die Anzahl der Tage seit 1/1/1900 (bzw. 1/1/1904, wenn 1904-Datumswerte verwenden aktiviert ist) dar. So werden Datumsangaben in Excel intern dargestellt.</span><span class="sxs-lookup"><span data-stu-id="09e4d-p114">In cell A2, the number represents the number of days since 1/1/1900 (or 1/1/1904 if you have "Use 1904 Date System" turned on). It's how Excel represents dates internally.</span></span> 

### <a name="to-change-parameters-to-test-the-udf"></a><span data-ttu-id="09e4d-158">Ändern von Parametern zum Testen der UDF</span><span class="sxs-lookup"><span data-stu-id="09e4d-158">To change parameters to test the UDF</span></span>


1. <span data-ttu-id="09e4d-159">In the **Parameters** pane, you should see the named range for cell B1, that is, "MyDoubleParam".</span><span class="sxs-lookup"><span data-stu-id="09e4d-159">In the **Parameters** pane, you should see the named range for cell B1, that is, "MyDoubleParam".</span></span>
    
  
2. <span data-ttu-id="09e4d-p115">You can change the value in cell B1 by typing a number in the box next to "MyDoubleParam". For example, if you type 3 and then click **Apply**, Excel Services will recalculate the workbook. Cell A1 will contain "27" instead of "72".</span><span class="sxs-lookup"><span data-stu-id="09e4d-p115">You can change the value in cell B1 by typing a number in the box next to "MyDoubleParam". For example, if you type 3 and then click **Apply**, Excel Services will recalculate the workbook. Cell A1 will contain "27" instead of "72".</span></span> 
    
  

## <a name="see-also"></a><span data-ttu-id="09e4d-163">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="09e4d-163">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="09e4d-164">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="09e4d-164">Tasks</span></span>


  
    
    
 [<span data-ttu-id="09e4d-165">Step 1: Creating a Project and Adding a UDF Reference</span><span class="sxs-lookup"><span data-stu-id="09e4d-165">Step 1: Creating a Project and Adding a UDF Reference</span></span>](step-1-creating-a-project-and-adding-a-udf-reference.md)
  
    
    
 [<span data-ttu-id="09e4d-166">Step 2: Creating a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="09e4d-166">Step 2: Creating a Managed-Code UDF</span></span>](step-2-creating-a-managed-code-udf.md)
  
    
    
 [<span data-ttu-id="09e4d-167">Step 3: Deploying and Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="09e4d-167">Step 3: Deploying and Enabling UDFs</span></span>](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [<span data-ttu-id="09e4d-168">How to: Create a UDF That Calls a Web Service</span><span class="sxs-lookup"><span data-stu-id="09e4d-168">How to: Create a UDF That Calls a Web Service</span></span>](how-to-create-a-udf-that-calls-a-web-service.md)
#### <a name="concepts"></a><span data-ttu-id="09e4d-169">Konzepte</span><span class="sxs-lookup"><span data-stu-id="09e4d-169">Concepts</span></span>


  
    
    
 [<span data-ttu-id="09e4d-170">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="09e4d-170">Walkthrough: Developing a Managed-Code UDF</span></span>](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [<span data-ttu-id="09e4d-171">Understanding Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="09e4d-171">Understanding Excel Services UDFs</span></span>](understanding-excel-services-udfs.md)
