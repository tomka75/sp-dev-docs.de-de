---
title: Speichern vom Excel-Client auf dem Server
ms.date: 09/25/2017
keywords: how to,howdoi,howto
f1_keywords: how to,howdoi,howto
ms.prod: sharepoint
ms.assetid: 28716ba5-0774-44df-833b-0034d2c63319
ms.openlocfilehash: 18868cec79119123cf8262b9b93e9fd7eca1571f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="save-from-excel-client-to-the-server"></a><span data-ttu-id="4bf61-103">Speichern vom Excel-Client auf dem Server</span><span class="sxs-lookup"><span data-stu-id="4bf61-103">Save from Excel client to the server</span></span>

<span data-ttu-id="4bf61-104">This example shows you how to:</span><span class="sxs-lookup"><span data-stu-id="4bf61-104">This example shows you how to:</span></span>

1. <span data-ttu-id="4bf61-105">Create a workbook with editable ranges.</span><span class="sxs-lookup"><span data-stu-id="4bf61-105">Create a workbook with editable ranges.</span></span>
    
  
2. <span data-ttu-id="4bf61-106">Speichern Sie die Arbeitsmappe in einer SharePoint-Dokumentbibliothek, die einen vertrauenswürdigen Speicherort darstellt.</span><span class="sxs-lookup"><span data-stu-id="4bf61-106">Save the workbook to a SharePoint document library that is a trusted location.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4bf61-107">Es wird vorausgesetzt, dass Sie bereits eine SharePoint-Dokumentbibliothek erstellt und diese als vertrauenswürdigen Speicherort definiert haben.</span><span class="sxs-lookup"><span data-stu-id="4bf61-107">Note: It is assumed that you have already created a SharePoint document library and made it a trusted location.</span></span> <span data-ttu-id="4bf61-108">Weitere Informationen finden Sie unter [Gewusst wie: Vertrauen zu einem Standort](how-to-trust-a-location.md).</span><span class="sxs-lookup"><span data-stu-id="4bf61-108">For more information, see  [How to: Trust a Location](how-to-trust-a-location.md).</span></span>

3. <span data-ttu-id="4bf61-109">Ändern Sie Werte in einer Arbeitsmappe mithilfe des Parameterbereich in Excel Web Access.</span><span class="sxs-lookup"><span data-stu-id="4bf61-109">Change values in a workbook by using the parameters pane in Excel Web Access.</span></span>
    
  

## <a name="saving-a-workbook-to-excel-services"></a><span data-ttu-id="4bf61-110">Saving a Workbook to Excel Services</span><span class="sxs-lookup"><span data-stu-id="4bf61-110">Saving a Workbook to Excel Services</span></span>


### <a name="to-create-a-workbook-with-ranges"></a><span data-ttu-id="4bf61-111">To create a workbook with ranges</span><span class="sxs-lookup"><span data-stu-id="4bf61-111">To create a workbook with ranges</span></span>


1. <span data-ttu-id="4bf61-112">Start Excel.</span><span class="sxs-lookup"><span data-stu-id="4bf61-112">Start Excel.</span></span>
    
  
2. <span data-ttu-id="4bf61-113">In cell A1, type 8.</span><span class="sxs-lookup"><span data-stu-id="4bf61-113">In cell A1, type 8.</span></span>
    
  
3. <span data-ttu-id="4bf61-114">In cell A2, type =3*A1.</span><span class="sxs-lookup"><span data-stu-id="4bf61-114">In cell A2, type =3*A1.</span></span>
    
  
4. <span data-ttu-id="4bf61-115">To make cell A1 editable in Excel Web Access, you must first make cell A1 into a named range:</span><span class="sxs-lookup"><span data-stu-id="4bf61-115">To make cell A1 editable in Excel Web Access, you must first make cell A1 into a named range:</span></span> 
    
1. <span data-ttu-id="4bf61-116">Click the **Formulas** tab, and then click cell **A1** to select it.</span><span class="sxs-lookup"><span data-stu-id="4bf61-116">Click the **Formulas** tab, and then click cell **A1** to select it.</span></span>
    
  
2. <span data-ttu-id="4bf61-117">On the **Formulas** tab, in the **Defined Names** group, click **Define Name**.</span><span class="sxs-lookup"><span data-stu-id="4bf61-117">On the **Formulas** tab, in the **Defined Names** group, click **Define Name**.</span></span>
    
  
3. <span data-ttu-id="4bf61-118">In the **New Name** dialog box, in the **Name** text box, typeMyAOneParam.</span><span class="sxs-lookup"><span data-stu-id="4bf61-118">In the **New Name** dialog box, in the **Name** text box, typeMyAOneParam.</span></span>
    
  

### <a name="to-save-to-excel-services"></a><span data-ttu-id="4bf61-119">To save to Excel Services</span><span class="sxs-lookup"><span data-stu-id="4bf61-119">To save to Excel Services</span></span>


1. <span data-ttu-id="4bf61-120">On the **File** menu, click **Save &amp; Send**, and then click **Save to SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="4bf61-120">On the **File** menu, click **Save &amp; Send**, and then click **Save to SharePoint**.</span></span> 
    
  
2. <span data-ttu-id="4bf61-121">In the **Save to SharePoint** dialog box, click **Publish Options**.</span><span class="sxs-lookup"><span data-stu-id="4bf61-121">In the **Save to SharePoint** dialog box, click **Publish Options**.</span></span>
    
  
3. <span data-ttu-id="4bf61-122">In the **Publish Options** dialog box, on the **Show** tab, ensure that **Entire Workbook** is selected.</span><span class="sxs-lookup"><span data-stu-id="4bf61-122">In the **Publish Options** dialog box, on the **Show** tab, ensure that **Entire Workbook** is selected.</span></span>
    
  
4. <span data-ttu-id="4bf61-123">On the **Parameters** tab, click **Add**..</span><span class="sxs-lookup"><span data-stu-id="4bf61-123">On the **Parameters** tab, click **Add**..</span></span>
    
  
5. <span data-ttu-id="4bf61-124">In the **Add Parameters** list, select the **MyAOneParam** check box.</span><span class="sxs-lookup"><span data-stu-id="4bf61-124">In the **Add Parameters** list, select the **MyAOneParam** check box.</span></span>
    
  
6. <span data-ttu-id="4bf61-p102">Click **OK**. You should now see "MyAOneParam" in the **Parameters** list.</span><span class="sxs-lookup"><span data-stu-id="4bf61-p102">Click **OK**. You should now see "MyAOneParam" in the **Parameters** list.</span></span>
    
  
7. <span data-ttu-id="4bf61-127">Click **OK** to close the **Publish Options** dialog box.</span><span class="sxs-lookup"><span data-stu-id="4bf61-127">Click **OK** to close the **Publish Options** dialog box.</span></span>
    
  
8. <span data-ttu-id="4bf61-128">In the **Save to SharePoint** dialog box, click **Save As**.</span><span class="sxs-lookup"><span data-stu-id="4bf61-128">In the **Save to SharePoint** dialog box, click **Save As**.</span></span>
    
  
9. <span data-ttu-id="4bf61-129">In the **Save As** dialog box, ensure that the **Open with Excel in the browser** check box is selected.</span><span class="sxs-lookup"><span data-stu-id="4bf61-129">In the **Save As** dialog box, ensure that the **Open with Excel in the browser** check box is selected.</span></span>
    
  
10. <span data-ttu-id="4bf61-p103">In the **File name** text box, type the path to the trusted SharePoint document library where you want to store this workbook. For example,http:// _MyServer002_/Shared%20Documents/TestParam.xlsx.</span><span class="sxs-lookup"><span data-stu-id="4bf61-p103">In the **File name** text box, type the path to the trusted SharePoint document library where you want to store this workbook. For example,http:// _MyServer002_/Shared%20Documents/TestParam.xlsx.</span></span>
    
  
11. <span data-ttu-id="4bf61-p104">Click **Save**. You should see TestParam.xlsx in Excel Web Access.</span><span class="sxs-lookup"><span data-stu-id="4bf61-p104">Click **Save**. You should see TestParam.xlsx in Excel Web Access.</span></span> 
    
  

### <a name="to-change-values-by-using-parameters"></a><span data-ttu-id="4bf61-134">To change values by using parameters</span><span class="sxs-lookup"><span data-stu-id="4bf61-134">To change values by using parameters</span></span>


1. <span data-ttu-id="4bf61-135">In the **Parameters** pane, you should see the named range for cell **A1**that is, **MyAOneParam**.</span><span class="sxs-lookup"><span data-stu-id="4bf61-135">In the **Parameters** pane, you should see the named range for cell **A1**—that is, **MyAOneParam**.</span></span> 
    
  
2. <span data-ttu-id="4bf61-p105">You can change the values in cell **A1** and cell **A2** by typing a number in the text box next to **MyAOneParam**. For example, if you type 10 and then click **Apply**, cell **A1** changes to **10** and cell **A2** changes to **30**.</span><span class="sxs-lookup"><span data-stu-id="4bf61-p105">You can change the values in cell **A1** and cell **A2** by typing a number in the text box next to **MyAOneParam**. For example, if you type 10 and then click **Apply**, cell **A1** changes to **10** and cell **A2** changes to **30**.</span></span> 
    
  

## <a name="see-also"></a><span data-ttu-id="4bf61-138">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="4bf61-138">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="4bf61-139">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="4bf61-139">Tasks</span></span>


  
    
    
 [<span data-ttu-id="4bf61-140">How to: Save to the Server to Prepare for Programmatic Access</span><span class="sxs-lookup"><span data-stu-id="4bf61-140">How to: Save to the Server to Prepare for Programmatic Access</span></span>](how-to-save-to-the-server-to-prepare-for-programmatic-access.md)
#### <a name="concepts"></a><span data-ttu-id="4bf61-141">Konzepte</span><span class="sxs-lookup"><span data-stu-id="4bf61-141">Concepts</span></span>


  
    
    
 [<span data-ttu-id="4bf61-142">Accessing the SOAP API</span><span class="sxs-lookup"><span data-stu-id="4bf61-142">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
  
    
    
 [<span data-ttu-id="4bf61-143">Loop-Back SOAP Calls and Direct Linking</span><span class="sxs-lookup"><span data-stu-id="4bf61-143">Loop-Back SOAP Calls and Direct Linking</span></span>](loop-back-soap-calls-and-direct-linking.md)
  
    
    
 [<span data-ttu-id="4bf61-144">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="4bf61-144">Excel Services Alerts</span></span>](excel-services-alerts.md)
#### <a name="other-resources"></a><span data-ttu-id="4bf61-145">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="4bf61-145">Other resources</span></span>


  
    
    
 [<span data-ttu-id="4bf61-146">Walkthrough: Developing a Custom Application Using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="4bf61-146">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
