---
title: Aktivieren von UDFs
ms.date: 09/25/2017
keywords: how to,howdoi,howto,UDF list
f1_keywords: how to,howdoi,howto,UDF list
ms.prod: sharepoint
ms.assetid: 8c1af2eb-bb22-45e1-82de-a2b4b53d7a26
ms.openlocfilehash: 6eb51af89ab003e507ec9acb2f81a70bf843ee99
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="enable-udfs"></a><span data-ttu-id="5ac04-103">Aktivieren von UDFs</span><span class="sxs-lookup"><span data-stu-id="5ac04-103">How to: Enable UDFs</span></span>

<span data-ttu-id="5ac04-104">Jeder vertrauenswürdiger Excel Services-Speicherort in dem Anbieter für gemeinsame Dienste verfügt ein **AllowUdfs**-Flag.</span><span class="sxs-lookup"><span data-stu-id="5ac04-104">Each Excel Services trusted location in the Shared Services Provider (SSP) has an **AllowUdfs** flag.</span></span>
  
    
    


> <span data-ttu-id="5ac04-105">**Hinweis:** Das **AllowUdfs**-Flag wird durch die Option **Benutzerdefinierte Funktionen sind zugelassen** auf der Seite „Vertrauenswürdige Dateispeicherorte von Excel Services“ bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="5ac04-105">**Note:** The **AllowUdfs** flag is denoted by the **User-defined functions allowed** option on the Excel Services Trusted File Locations page.</span></span>
  
    
    


<span data-ttu-id="5ac04-p101">The default **AllowUdfs** value is **false**. If the **AllowUdfs** value is set to **false** in a particular trusted location, the workbooks in that trusted location are not allowed to call UDFs.</span><span class="sxs-lookup"><span data-stu-id="5ac04-p101">The default **AllowUdfs** value is **false**. If the **AllowUdfs** value is set to **false** in a particular trusted location, the workbooks in that trusted location are not allowed to call UDFs.</span></span>
  
    
    

<span data-ttu-id="5ac04-p102">In order to allow UDFs to be called from a specific trusted location, you set the **AllowUdfs** value to **true**.If the **AllowUdfs** value is **false** when a session is started on a workbook that has UDF calls in this trusted location, the UDF calls will fail. If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session, after the configuration database has been updated.You can get around this by restarting the sessionfor example, by selecting **Reload Workbook** in Excel Web Access.</span><span class="sxs-lookup"><span data-stu-id="5ac04-p102">In order to allow UDFs to be called from a specific trusted location, you set the **AllowUdfs** value to **true**.If the **AllowUdfs** value is **false** when a session is started on a workbook that has UDF calls in this trusted location, the UDF calls will fail. If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session, after the configuration database has been updated.You can get around this by restarting the session—for example, by selecting **Reload Workbook** in Excel Web Access.</span></span>
> <span data-ttu-id="5ac04-111">**Vorsicht** Wenn Sie stattdessen die Microsoft-Internetinformationsdienste (IIS) zurücksetzen, werden alle aktuelle Sitzungen beendet.</span><span class="sxs-lookup"><span data-stu-id="5ac04-111">**Caution:** If you choose to reset Microsoft Internet Information Services (IIS) instead, it will end all current sessions.</span></span> 
  
    
    


## <a name="enabling-udfs"></a><span data-ttu-id="5ac04-112">Aktivieren von UDFs</span><span class="sxs-lookup"><span data-stu-id="5ac04-112">Enabling UDFs</span></span>

<span data-ttu-id="5ac04-113">To do the following steps, you need a computer that has Microsoft SharePoint Server 2010 installed.</span><span class="sxs-lookup"><span data-stu-id="5ac04-113">To do the following steps, you need a computer that has Microsoft SharePoint Server 2010 installed.</span></span>
  
    
    

### <a name="to-enable-udfs"></a><span data-ttu-id="5ac04-114">To enable UDFs</span><span class="sxs-lookup"><span data-stu-id="5ac04-114">To enable UDFs</span></span>


1. <span data-ttu-id="5ac04-115">On the **Start** menu, click **All Programs**.</span><span class="sxs-lookup"><span data-stu-id="5ac04-115">On the **Start** menu, click **All Programs**.</span></span> 
    
  
2. <span data-ttu-id="5ac04-116">Point to **Microsoft Office Server** and click **SharePoint Central Administration**.</span><span class="sxs-lookup"><span data-stu-id="5ac04-116">Point to **Microsoft Office Server** and click **SharePoint Central Administration**.</span></span> 
    
  
3. <span data-ttu-id="5ac04-117">On the Quick Launch, click your Shared Services Provider (SSP) linkfor example, "SharedServices1"to view the Shared Services home page for that particular SSP.</span><span class="sxs-lookup"><span data-stu-id="5ac04-117">On the Quick Launch, click your Shared Services Provider (SSP) link—for example, "SharedServices1"—to view the Shared Services home page for that particular SSP.</span></span>
    
  
4. <span data-ttu-id="5ac04-118">Under **Excel Services Settings**, click **User-defined functions**.</span><span class="sxs-lookup"><span data-stu-id="5ac04-118">Under **Excel Services Settings**, click **User-defined functions**.</span></span> 
    
  
5. <span data-ttu-id="5ac04-119">On the Excel Services User-Defined Functions page, click **Add User-Defined Function** to open the Excel Services Add User-Defined Function Assembly page.</span><span class="sxs-lookup"><span data-stu-id="5ac04-119">On the Excel Services User-Defined Functions page, click **Add User-Defined Function** to open the Excel Services Add User-Defined Function Assembly page.</span></span>
    
  
6. <span data-ttu-id="5ac04-p103">In the **Assembly** box, type the path to the UDF assembly. For example,C:\\MyUdfFolder\\MyUdf.dll.</span><span class="sxs-lookup"><span data-stu-id="5ac04-p103">In the **Assembly** box, type the path to the UDF assembly. For example,C:\\MyUdfFolder\\MyUdf.dll.</span></span>
    
  
7. <span data-ttu-id="5ac04-122">Klicken Sie unter **Assemblyspeicherort** auf **Lokale Datei**.</span><span class="sxs-lookup"><span data-stu-id="5ac04-122">Under **Assembly Location**, click **Local file**.</span></span>
    
    > <span data-ttu-id="5ac04-123">**Hinweis:** Die Option **Lokale Datei** wird in künftigen Versionen von Excel Services durch **Dateipfad** ersetzt. Wählen Sie dann stattdessen „Dateipfad“ aus.</span><span class="sxs-lookup"><span data-stu-id="5ac04-123">**Note:** The **Local file** option will be replaced with **File path** in future releases of Excel Services.</span></span> <span data-ttu-id="5ac04-124">Wenn **Dateipfad** angezeigt wird, wählen Sie dies aus.</span><span class="sxs-lookup"><span data-stu-id="5ac04-124">If you see **File path**, select that instead.</span></span> 
8. <span data-ttu-id="5ac04-125">Standardmäßig sollte unter **Assembly aktivieren** das Kontrollkästchen **Assembly aktiviert** aktiviert sein.</span><span class="sxs-lookup"><span data-stu-id="5ac04-125">Under **Enable Assembly**, the **Assembly enabled** check box should be selected by default.</span></span>
    
  
9. <span data-ttu-id="5ac04-126">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ac04-126">Click **OK**.</span></span>
    
  

## <a name="allowing-udf-calls"></a><span data-ttu-id="5ac04-127">Allowing UDF Calls</span><span class="sxs-lookup"><span data-stu-id="5ac04-127">Allowing UDF Calls</span></span>


### <a name="to-allow-udfs-to-be-called-from-a-workbook"></a><span data-ttu-id="5ac04-128">To allow UDFs to be called from a workbook</span><span class="sxs-lookup"><span data-stu-id="5ac04-128">To allow UDFs to be called from a workbook</span></span>


1. <span data-ttu-id="5ac04-129">Open the Excel Services Add Trusted File Location page (if you are adding a new trusted location) or Excel Services Edit Trusted File Location page (if you are editing an existing trusted location).</span><span class="sxs-lookup"><span data-stu-id="5ac04-129">Open the Excel Services Add Trusted File Location page (if you are adding a new trusted location) or Excel Services Edit Trusted File Location page (if you are editing an existing trusted location).</span></span> 
    
    > <span data-ttu-id="5ac04-130">**Hinweis:** Weitere Informationen zum Festlegen eines vertrauenswürdigen Speicherorts finden Sie unter [Gewusst wie: Festlegen eines vertrauenswürdigen Speicherorts](how-to-trust-a-location.md).</span><span class="sxs-lookup"><span data-stu-id="5ac04-130">**Note:** For more information about trusting a location, see  [How to: Trust a Location](how-to-trust-a-location.md).</span></span> 
2. <span data-ttu-id="5ac04-131">Wählen Sie unter **Benutzerdefinierte Funktionen zulassen** die Option **Benutzerdefinierte Funktionen sind zugelassen**, damit UDFs von einer Arbeitsmappe in diesem vertrauenswürdigen Speicherort aufgerufen werden können.</span><span class="sxs-lookup"><span data-stu-id="5ac04-131">Under **Allow User-Defined Functions**, select **User-defined functions allowed** to allow UDFs to be called from workbooks stored in this trusted location.</span></span>
    
  
3. <span data-ttu-id="5ac04-132">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ac04-132">Click **OK**.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="5ac04-133">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="5ac04-133">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="5ac04-134">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="5ac04-134">Tasks</span></span>


  
    
    
 [<span data-ttu-id="5ac04-135">Step 3: Deploying and Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="5ac04-135">Step 3: Deploying and Enabling UDFs</span></span>](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [<span data-ttu-id="5ac04-136">How to: Create a UDF That Calls a Web Service</span><span class="sxs-lookup"><span data-stu-id="5ac04-136">How to: Create a UDF That Calls a Web Service</span></span>](how-to-create-a-udf-that-calls-a-web-service.md)
  
    
    
 [<span data-ttu-id="5ac04-137">How to: Trust a Location</span><span class="sxs-lookup"><span data-stu-id="5ac04-137">How to: Trust a Location</span></span>](how-to-trust-a-location.md)
#### <a name="concepts"></a><span data-ttu-id="5ac04-138">Konzepte</span><span class="sxs-lookup"><span data-stu-id="5ac04-138">Concepts</span></span>


  
    
    
 [<span data-ttu-id="5ac04-139">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="5ac04-139">Walkthrough: Developing a Managed-Code UDF</span></span>](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [<span data-ttu-id="5ac04-140">Frequently Asked Questions About Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="5ac04-140">Frequently Asked Questions About Excel Services UDFs</span></span>](frequently-asked-questions-about-excel-services-udfs.md)
  
    
    
 [<span data-ttu-id="5ac04-141">Understanding Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="5ac04-141">Understanding Excel Services UDFs</span></span>](understanding-excel-services-udfs.md)
  
    
    
 [<span data-ttu-id="5ac04-142">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="5ac04-142">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="5ac04-143">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="5ac04-143">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
  
    
    
 [<span data-ttu-id="5ac04-144">Excel Services Best Practices</span><span class="sxs-lookup"><span data-stu-id="5ac04-144">Excel Services Best Practices</span></span>](excel-services-best-practices.md)
