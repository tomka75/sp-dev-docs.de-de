---
title: Walkthrough Developing a Managed-Code UDF
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e6a00833-0606-4a7d-91c3-b89a6e340348
ms.openlocfilehash: 6e7539703fd642349a0b7a4f54f703cad3de7b61
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="walkthrough-developing-a-managed-code-udf"></a><span data-ttu-id="3e564-102">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="3e564-102">Walkthrough: Developing a Managed-Code UDF</span></span>

<span data-ttu-id="3e564-103">This walkthrough describes the process for developing Excel Services user-defined functions (UDFs) using Microsoft Visual C#.</span><span class="sxs-lookup"><span data-stu-id="3e564-103">This walkthrough describes the process for developing Excel Services user-defined functions (UDFs) using Microsoft Visual C#.</span></span>

<span data-ttu-id="3e564-104">During this walkthrough, you will learn how to:</span><span class="sxs-lookup"><span data-stu-id="3e564-104">During this walkthrough, you will learn how to:</span></span>
- <span data-ttu-id="3e564-105">Create a project using the Microsoft Visual Studio 2005 class library project template.</span><span class="sxs-lookup"><span data-stu-id="3e564-105">Create a project using the Microsoft Visual Studio 2005 class library project template.</span></span>
    
  
- <span data-ttu-id="3e564-106">Add a reference to Microsoft.Office.Excel.Server.Udf.dll.</span><span class="sxs-lookup"><span data-stu-id="3e564-106">Add a reference to Microsoft.Office.Excel.Server.Udf.dll.</span></span>
    
  
- <span data-ttu-id="3e564-107">Write UDFs for use in Excel Services.</span><span class="sxs-lookup"><span data-stu-id="3e564-107">Write UDFs for use in Excel Services.</span></span>
    
  
- <span data-ttu-id="3e564-108">Create a workbook to call custom functions from cells.</span><span class="sxs-lookup"><span data-stu-id="3e564-108">Create a workbook to call custom functions from cells.</span></span>
    
  
- <span data-ttu-id="3e564-109">Test and run UDFs in Excel Services.</span><span class="sxs-lookup"><span data-stu-id="3e564-109">Test and run UDFs in Excel Services.</span></span>
    
  

## <a name="prerequisites"></a><span data-ttu-id="3e564-110">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="3e564-110">Prerequisites</span></span>

<span data-ttu-id="3e564-111">In order to complete this walkthrough, you will need:</span><span class="sxs-lookup"><span data-stu-id="3e564-111">In order to complete this walkthrough, you will need:</span></span> 
  
    
    

- <span data-ttu-id="3e564-112">Microsoft SharePoint Server 2010</span><span class="sxs-lookup"><span data-stu-id="3e564-112">Microsoft SharePoint Server 2010</span></span> 
    
    > [!NOTE] 
    > <span data-ttu-id="3e564-p101">Die einfachste Methode, um alles Erforderliche auf dem Server einzurichten, ist die Durchführung einer einfachen eigenständigen Installation. Abgesehen davon benötigen Sie nur noch einen vertrauenswürdigen Speicherort.</span><span class="sxs-lookup"><span data-stu-id="3e564-p101">The easiest way to get all you need on the server is to do a basic, stand-alone install. All you need to add on top of that is a trusted location.</span></span> 

- <span data-ttu-id="3e564-115">Excel</span><span class="sxs-lookup"><span data-stu-id="3e564-115">Excel</span></span>
    
  
- <span data-ttu-id="3e564-116">Visual Studio oder ein vergleichbares mit Microsoft .NET Framework kompatibles Entwicklungstool</span><span class="sxs-lookup"><span data-stu-id="3e564-116">Visual Studio or a similar Microsoft .NET Framework-compatible development tool.</span></span>
    
  
- <span data-ttu-id="3e564-117">Aktivieren der Ausführung der UDF-Assembly</span><span class="sxs-lookup"><span data-stu-id="3e564-117">To enable running the UDF assembly.</span></span>
    
  
- <span data-ttu-id="3e564-118">Eine vertrauenswürdige SharePoint-Dokumentbibliothek, in der eine Arbeitsmappe gespeichert werden soll. Für die Arbeitsmappe muss das Aufrufen von UDFs aktiviert sein, indem der **AllowUdfs**-Wert auf **true** festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="3e564-118">A trusted SharePoint document library in which to store a workbook, and to allow the workbook to call UDFs by setting the **AllowUdfs** value to **true**.</span></span>
    
  
- <span data-ttu-id="3e564-119">Eine Beispielarbeitsmappe, die in einer vertrauenswürdigen SharePoint-Dokumentbibliothek gespeicherte UDFs aufruft</span><span class="sxs-lookup"><span data-stu-id="3e564-119">A sample workbook that calls the UDF stored in a trusted SharePoint document library.</span></span>
    
  
- <span data-ttu-id="3e564-120">Berechtigungen zum Anzeigen und Veröffentlichen einer Arbeitsmappe in einer SharePoint-Dokumentbibliothek</span><span class="sxs-lookup"><span data-stu-id="3e564-120">Permissions to view and publish a workbook to a SharePoint document library.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="3e564-121">Weitere Informationen zum Festlegen von Berechtigungen finden Sie in der Dokumentation zu Windows SharePoint Services 3.0.</span><span class="sxs-lookup"><span data-stu-id="3e564-121">Note: For more information about setting permissions, see the Windows SharePoint Services 3.0 documentation.</span></span> 

- <span data-ttu-id="3e564-122">Erstellen der Arbeitsmappe mithilfe von Excel</span><span class="sxs-lookup"><span data-stu-id="3e564-122">To create the workbook using Excel.</span></span>
    
  
- <span data-ttu-id="3e564-123">Speichern der Arbeitsmappe als xlsx- oder xlsb-Datei</span><span class="sxs-lookup"><span data-stu-id="3e564-123">To save the workbook as an .xlsx or .xlsb file.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="3e564-124">Weitere Informationen dazu, wie Sie einen Speicherort als vertrauenswürdig festlegen, UDFs aktivieren und das **AllowUdfs**-Flag festlegen, finden Sie unter [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md).</span><span class="sxs-lookup"><span data-stu-id="3e564-124">For more information about how to trust a location, how to enable UDFs, and how to set the **AllowUdfs** flag, see [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="3e564-125">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="3e564-125">See also</span></span>

- [<span data-ttu-id="3e564-126">Schritt 1: Erstellen eines Projekts und Hinzufügen einer UDF-Referenz</span><span class="sxs-lookup"><span data-stu-id="3e564-126">Step 1: Creating a Project and Adding a UDF Reference</span></span>](step-1-creating-a-project-and-adding-a-udf-reference.md)
- [<span data-ttu-id="3e564-127">Step 2: Creating a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="3e564-127">Step 2: Creating a Managed-Code UDF</span></span>](step-2-creating-a-managed-code-udf.md)
- [<span data-ttu-id="3e564-128">Step 3: Deploying and Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="3e564-128">Step 3: Deploying and Enabling UDFs</span></span>](step-3-deploying-and-enabling-udfs.md)
- [<span data-ttu-id="3e564-129">Step 4: Testing and Calling UDFs from Cells</span><span class="sxs-lookup"><span data-stu-id="3e564-129">Step 4: Testing and Calling UDFs from Cells</span></span>](step-4-testing-and-calling-udfs-from-cells.md)
- [<span data-ttu-id="3e564-130">Gewusst wie: Erstellen eines UDF, das einen Webdienst aufruft</span><span class="sxs-lookup"><span data-stu-id="3e564-130">How to: Create a UDF That Calls a Web Service</span></span>](how-to-create-a-udf-that-calls-a-web-service.md)
- [<span data-ttu-id="3e564-131">Grundlegendes zu Excel Services-UDFs</span><span class="sxs-lookup"><span data-stu-id="3e564-131">Understanding Excel Services UDFs</span></span>](understanding-excel-services-udfs.md)
- [<span data-ttu-id="3e564-132">Schritt für Schritt: Entwickeln einer benutzerdefinierten Anwendung mit Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="3e564-132">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
