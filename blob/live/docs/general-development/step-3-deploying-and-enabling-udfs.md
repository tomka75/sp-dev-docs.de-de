---
title: Step 3 Deploying and Enabling UDFs
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1e5e2a0a-041a-481c-a18b-578562a60e24
ms.openlocfilehash: 7d2abb6cce364a634fcd5f68c139e89931f3c3de
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="step-3-deploying-and-enabling-udfs"></a><span data-ttu-id="adfbe-102">Step 3: Deploying and Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="adfbe-102">Step 3: Deploying and Enabling UDFs</span></span>

<span data-ttu-id="adfbe-103">In this step, you will:</span><span class="sxs-lookup"><span data-stu-id="adfbe-103">In this step, you will:</span></span>
  
    
    


1. <span data-ttu-id="adfbe-104">Deploy SampleUdf.dll, which you created in  [Step 2: Creating a Managed-Code UDF](step-2-creating-a-managed-code-udf.md), to a folder on a computer that has Microsoft SharePoint Server 2010 installed.</span><span class="sxs-lookup"><span data-stu-id="adfbe-104">Deploy SampleUdf.dll, which you created in  [Step 2: Creating a Managed-Code UDF](step-2-creating-a-managed-code-udf.md), to a folder on a computer that has Microsoft SharePoint Server 2010 installed.</span></span>
    
  
2. <span data-ttu-id="adfbe-105">Allow user-defined functions (UDFs) to be called from a specific trusted location, for example, trusted Shared Documents location.</span><span class="sxs-lookup"><span data-stu-id="adfbe-105">Allow user-defined functions (UDFs) to be called from a specific trusted location, for example, trusted Shared Documents location.</span></span> 
    
  
3. <span data-ttu-id="adfbe-106">Enable SampleUdf.dll.</span><span class="sxs-lookup"><span data-stu-id="adfbe-106">Enable SampleUdf.dll.</span></span>
    
  

## <a name="deploying-udfs"></a><span data-ttu-id="adfbe-107">Deploying UDFs</span><span class="sxs-lookup"><span data-stu-id="adfbe-107">Deploying UDFs</span></span>


### <a name="to-deploy-udfs"></a><span data-ttu-id="adfbe-108">To deploy UDFs</span><span class="sxs-lookup"><span data-stu-id="adfbe-108">To deploy UDFs</span></span>


1. <span data-ttu-id="adfbe-p101">Create a folder named "UDFs" on the local drive of the computer to which you want to deploy UDFs. For example, "C:\\UDFs".</span><span class="sxs-lookup"><span data-stu-id="adfbe-p101">Create a folder named "UDFs" on the local drive of the computer to which you want to deploy UDFs. For example, "C:\\UDFs".</span></span>
    
  
2. <span data-ttu-id="adfbe-111">Copy the SampleUdf.dll assembly.</span><span class="sxs-lookup"><span data-stu-id="adfbe-111">Copy the SampleUdf.dll assembly.</span></span>
    
  
3. <span data-ttu-id="adfbe-112">Save SampleUdf.dll in "C:\\UDFs".</span><span class="sxs-lookup"><span data-stu-id="adfbe-112">Save SampleUdf.dll in "C:\\UDFs".</span></span> 
    
  

## <a name="trusting-a-location"></a><span data-ttu-id="adfbe-113">Trusting a Location</span><span class="sxs-lookup"><span data-stu-id="adfbe-113">Trusting a Location</span></span>


### <a name="to-trust-a-location"></a><span data-ttu-id="adfbe-114">To trust a location</span><span class="sxs-lookup"><span data-stu-id="adfbe-114">To trust a location</span></span>


1. <span data-ttu-id="adfbe-115">On the **Start** menu, click **All Programs**.</span><span class="sxs-lookup"><span data-stu-id="adfbe-115">On the **Start** menu, click **All Programs**.</span></span> 
    
  
2. <span data-ttu-id="adfbe-116">Point to **Microsoft SharePoint 2010 Products** and click **SharePoint Central Administration**.</span><span class="sxs-lookup"><span data-stu-id="adfbe-116">Point to **Microsoft SharePoint 2010 Products** and click **SharePoint Central Administration**.</span></span> 
    
  
3. <span data-ttu-id="adfbe-117">Under **Application Management** click **Manage service applications**.</span><span class="sxs-lookup"><span data-stu-id="adfbe-117">Under **Application Management** click **Manage service applications**.</span></span>
    
  
4. <span data-ttu-id="adfbe-118">On the Manage Service Applications page, click **Excel Services Application**.</span><span class="sxs-lookup"><span data-stu-id="adfbe-118">On the Manage Service Applications page, click **Excel Services Application**.</span></span>
    
  
5. <span data-ttu-id="adfbe-119">On the **Excel Services Application** page, click **Trusted File Locations**.</span><span class="sxs-lookup"><span data-stu-id="adfbe-119">On the **Excel Services Application** page, click **Trusted File Locations**.</span></span>
    
  
6. <span data-ttu-id="adfbe-120">On the Trusted File Locations page, click **Add Trusted File Location**.</span><span class="sxs-lookup"><span data-stu-id="adfbe-120">On the Trusted File Locations page, click **Add Trusted File Location**.</span></span> 
    
  
7. <span data-ttu-id="adfbe-121">On the Add Trusted File Location page, in the **Address** box, type the location where you will save your workbookfor example, _http://MyServer002/Shared%20Documents_.</span><span class="sxs-lookup"><span data-stu-id="adfbe-121">On the Add Trusted File Location page, in the **Address** box, type the location where you will save your workbook—for example, _http://MyServer002/Shared%20Documents_.</span></span> 
    
  
8. <span data-ttu-id="adfbe-p102">Under **Location type**, click the appropriate location type. In this example, select Microsoft SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="adfbe-p102">Under **Location type**, click the appropriate location type. In this example, select Microsoft SharePoint Foundation.</span></span>
    
  
9. <span data-ttu-id="adfbe-124">Under **Trust Children**, select **Children trusted** to trust child libraries or directories.</span><span class="sxs-lookup"><span data-stu-id="adfbe-124">Under **Trust Children**, select **Children trusted** to trust child libraries or directories.</span></span>
    
  
10. <span data-ttu-id="adfbe-125">Under **Allow User-Defined Functions**, select **User-defined functions allowed** to allow UDFs to be called from workbooks stored in this trusted location.</span><span class="sxs-lookup"><span data-stu-id="adfbe-125">Under **Allow User-Defined Functions**, select **User-defined functions allowed** to allow UDFs to be called from workbooks stored in this trusted location.</span></span>
    
  
11. <span data-ttu-id="adfbe-126">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="adfbe-126">Click **OK**.</span></span>
    
  

## <a name="enabling-udfs"></a><span data-ttu-id="adfbe-127">Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="adfbe-127">Enabling UDFs</span></span>

<span data-ttu-id="adfbe-128">To do the following steps, you need a computer that has SharePoint Server 2010 installed.</span><span class="sxs-lookup"><span data-stu-id="adfbe-128">To do the following steps, you need a computer that has SharePoint Server 2010 installed.</span></span>
  
    
    

### <a name="to-enable-udfs"></a><span data-ttu-id="adfbe-129">To enable UDFs</span><span class="sxs-lookup"><span data-stu-id="adfbe-129">To enable UDFs</span></span>


1. <span data-ttu-id="adfbe-130">Follow steps 1 through 3 in the previous procedure ("To trust a location") to display the Shared Services home page for an SSP.</span><span class="sxs-lookup"><span data-stu-id="adfbe-130">Follow steps 1 through 3 in the previous procedure ("To trust a location") to display the Shared Services home page for an SSP.</span></span>
    
  
2. <span data-ttu-id="adfbe-131">Klicken Sie unter **Excel Services-Einstellungen** auf **Benutzerdefinierte Funktionsassemblys**.</span><span class="sxs-lookup"><span data-stu-id="adfbe-131">Under **Excel Services Settings**, click **User-defined function assemblies**.</span></span> 
    
  
3. <span data-ttu-id="adfbe-132">Klicken Sie auf der Seite „Benutzerdefinierte Funktionen von Excel Services“ auf **Benutzerdefinierte Funktion hinzufügen**, um die Seite „Excel Services: Benutzerdefinierte Funktionsassembly hinzufügen“ aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="adfbe-132">On the Excel Services User-Defined Functions page, click **Add User-Defined Function** to open the ExcelServices Add User-Defined Function Assembly page.</span></span>
    
  
4. <span data-ttu-id="adfbe-p103">Geben Sie in das Feld **Assembly** den Pfad zu der Assembly SampleUdf.dll ein. In diesem Beispiel wäre dies _C:\\UDFs\\SampleUdf.dll_.</span><span class="sxs-lookup"><span data-stu-id="adfbe-p103">In the **Assembly** box, type the path to the SampleUdf.dll assembly. In this example, it would be _C:\\UDFs\\SampleUdf.dll_.</span></span>
    
  
5. <span data-ttu-id="adfbe-135">Under **Assembly Location**, click **File path**.</span><span class="sxs-lookup"><span data-stu-id="adfbe-135">Under **Assembly Location**, click **File path**.</span></span>
    
  
6. <span data-ttu-id="adfbe-136">Under **Enable Assembly**, the **Assembly enabled** check box should be selected by default.</span><span class="sxs-lookup"><span data-stu-id="adfbe-136">Under **Enable Assembly**, the **Assembly enabled** check box should be selected by default.</span></span>
    
  
7. <span data-ttu-id="adfbe-137">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="adfbe-137">Click **OK**.</span></span>
    
  

## <a name="robust-programming"></a><span data-ttu-id="adfbe-138">Robuste Programmierung</span><span class="sxs-lookup"><span data-stu-id="adfbe-138">Robust programming</span></span>

<span data-ttu-id="adfbe-139">Ist der **AllowUdfs**-Wert **false**, wenn eine Sitzung in einer Arbeitsmappe mit UDF-Aufrufen gestartet wird, tritt bei den UDF-Aufrufen ein Fehler auf.</span><span class="sxs-lookup"><span data-stu-id="adfbe-139">If the **AllowUdfs** value is **false** when a session is started on a workbook that has UDF calls, the UDF calls will fail.</span></span>
  
> [!NOTE]
> <span data-ttu-id="adfbe-140">Das **AllowUdfs**-Flag wird durch die Option **Benutzerdefinierte Funktionen sind zulässig** angegeben (siehe Schritt 9 im Abschnitt „Festlegen eines vertrauenswürdigen Speicherorts“).</span><span class="sxs-lookup"><span data-stu-id="adfbe-140">The **AllowUdfs** flag is denoted by the **User-defined functions allowed** option (see step 9 in the "Trusting a Location" section).</span></span>
  
    
    

<span data-ttu-id="adfbe-p104">If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session. You can get around this by resetting Microsoft Internet Information Services (IIS). Resetting IIS will reload UDFs.</span><span class="sxs-lookup"><span data-stu-id="adfbe-p104">If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session. You can get around this by resetting Microsoft Internet Information Services (IIS). Resetting IIS will reload UDFs.</span></span>  
    
<span data-ttu-id="adfbe-145">For more information about resetting IIS, see  [How to: Enable UDFs](how-to-enable-udfs.md).</span><span class="sxs-lookup"><span data-stu-id="adfbe-145">For more information about resetting IIS, see  [How to: Enable UDFs](how-to-enable-udfs.md).</span></span>
  
## <a name="see-also"></a><span data-ttu-id="adfbe-146">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="adfbe-146">See also</span></span>

- [<span data-ttu-id="adfbe-147">Schritt 1: Erstellen eines Projekts und Hinzufügen einer UDF-Referenz</span><span class="sxs-lookup"><span data-stu-id="adfbe-147">Step 1: Creating a Project and Adding a UDF Reference</span></span>](step-1-creating-a-project-and-adding-a-udf-reference.md)
- [<span data-ttu-id="adfbe-148">Step 2: Creating a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="adfbe-148">Step 2: Creating a Managed-Code UDF</span></span>](step-2-creating-a-managed-code-udf.md)
- [<span data-ttu-id="adfbe-149">Step 4: Testing and Calling UDFs from Cells</span><span class="sxs-lookup"><span data-stu-id="adfbe-149">Step 4: Testing and Calling UDFs from Cells</span></span>](step-4-testing-and-calling-udfs-from-cells.md)
- [<span data-ttu-id="adfbe-150">Gewusst wie: Aktivieren von UDFs</span><span class="sxs-lookup"><span data-stu-id="adfbe-150">How to: Enable UDFs</span></span>](how-to-enable-udfs.md)
- [<span data-ttu-id="adfbe-151">Exemplarische Vorgehensweise: Entwickeln eines UDF auf Basis von verwaltetem Code</span><span class="sxs-lookup"><span data-stu-id="adfbe-151">Walkthrough: Developing a Managed-Code UDF</span></span>](walkthrough-developing-a-managed-code-udf.md)
- [<span data-ttu-id="adfbe-152">Understanding Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="adfbe-152">Understanding Excel Services UDFs</span></span>](understanding-excel-services-udfs.md)
