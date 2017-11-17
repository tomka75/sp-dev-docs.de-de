---
title: Step 1 Creating a Project and Adding a UDF Reference
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4c6f1279-28df-45af-8488-42a6573d526d
ms.openlocfilehash: 530231d09b22be8036a815e6c60945364b5a6ba7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="step-1-creating-a-project-and-adding-a-udf-reference"></a><span data-ttu-id="8af41-102">Step 1: Creating a Project and Adding a UDF Reference</span><span class="sxs-lookup"><span data-stu-id="8af41-102">Step 1: Creating a Project and Adding a UDF Reference</span></span>

<span data-ttu-id="8af41-103">In this step, you will create a project and add a reference to Microsoft.Office.Excel.Server.Udf.dll.</span><span class="sxs-lookup"><span data-stu-id="8af41-103">In this step, you will create a project and add a reference to Microsoft.Office.Excel.Server.Udf.dll.</span></span> 
  
    
    


## <a name="creating-the-project"></a><span data-ttu-id="8af41-104">Erstellen des Projekts</span><span class="sxs-lookup"><span data-stu-id="8af41-104">Creating the Project</span></span>

<span data-ttu-id="8af41-105">Im folgenden Projekt wird Microsoft Visual Studio 2005 verwendet.</span><span class="sxs-lookup"><span data-stu-id="8af41-105">The following project uses Microsoft Visual Studio 2005.</span></span>
  
    
    

> <span data-ttu-id="8af41-106">**Hinweis:** Je nachdem, welche Einstellungen Sie in der integrierten Entwicklungsumgebung von Visual Studio verwenden, kann der Vorgang zum Erstellen eines Projekts leicht unterschiedlich sein kann.</span><span class="sxs-lookup"><span data-stu-id="8af41-106">**Note** Depending on which settings you use in the Visual Studio integrated development environment (IDE), the process to create a project could be slightly different.</span></span> 
  
    
    


### <a name="to-create-a-project"></a><span data-ttu-id="8af41-107">So erstellen Sie ein Projekt</span><span class="sxs-lookup"><span data-stu-id="8af41-107">To create a project</span></span>


1. <span data-ttu-id="8af41-108">Starten Sie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8af41-108">Start Visual Studio.</span></span>
    
  
2. <span data-ttu-id="8af41-p101">Zeigen Sie im Menü **Datei** auf **Neu**, und klicken Sie dann auf **Projekt**. Das Dialogfeld **Neues Projekt** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8af41-p101">On the **File** menu, point to **New**, and then click **Project**. The **New Project** dialog box appears.</span></span>
    
  
3. <span data-ttu-id="8af41-111">In the **Project Type** pane, select **Visual C# Projects**.</span><span class="sxs-lookup"><span data-stu-id="8af41-111">In the **Project Type** pane, select **Visual C# Projects**.</span></span>
    
  
4. <span data-ttu-id="8af41-112">In the **Templates** pane, click **Class Library**.</span><span class="sxs-lookup"><span data-stu-id="8af41-112">In the **Templates** pane, click **Class Library**.</span></span>
    
  
5. <span data-ttu-id="8af41-113">In the **Name** box, type **SampleUdf**.</span><span class="sxs-lookup"><span data-stu-id="8af41-113">In the **Name** box, type **SampleUdf**.</span></span>
    
  
6. <span data-ttu-id="8af41-114">In the **Location** box, type the path where you want to save your project, or click **Browse** to navigate to the folder.</span><span class="sxs-lookup"><span data-stu-id="8af41-114">In the **Location** box, type the path where you want to save your project, or click **Browse** to navigate to the folder.</span></span>
    
  
7. <span data-ttu-id="8af41-p102">Click **OK**. Your new project appears in **Solution Explorer**. You also will see that a file with the default name of Class1.cs has been added to your project.</span><span class="sxs-lookup"><span data-stu-id="8af41-p102">Click **OK**. Your new project appears in **Solution Explorer**. You also will see that a file with the default name of Class1.cs has been added to your project.</span></span>
    
  
8. <span data-ttu-id="8af41-118">You should see the following code in the Class1.cs file:</span><span class="sxs-lookup"><span data-stu-id="8af41-118">You should see the following code in the Class1.cs file:</span></span>
    
```cs
  
using System;
using System.Collections.Generic;
using System.Text;

namespace SampleUdf
{
    public class Class1
    {
    }
}
```


```VB.net
  
Imports System
Imports System.Collections.Generic
Imports System.Text

Namespace SampleUdf
Public Class Class1
End Class
End Namespace
```


## <a name="adding-a-reference"></a><span data-ttu-id="8af41-119">Adding a Reference</span><span class="sxs-lookup"><span data-stu-id="8af41-119">Adding a Reference</span></span>

<span data-ttu-id="8af41-120">The following steps show how to locate Microsoft.Office.Excel.Server.Udf.dll and how to add a reference to it.</span><span class="sxs-lookup"><span data-stu-id="8af41-120">The following steps show how to locate Microsoft.Office.Excel.Server.Udf.dll and how to add a reference to it.</span></span> 
  
    
    

### <a name="to-add-a-reference"></a><span data-ttu-id="8af41-121">To add a reference</span><span class="sxs-lookup"><span data-stu-id="8af41-121">To add a reference</span></span>


1. <span data-ttu-id="8af41-122">On the **Project** menu, click **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="8af41-122">On the **Project** menu, click **Add Reference**.</span></span>
    
  
2. <span data-ttu-id="8af41-123">Wählen Sie im Dialogfeld **Verweis hinzufügen** der Registerkarte **.NET** **Excel Services UDF Framework**.</span><span class="sxs-lookup"><span data-stu-id="8af41-123">In the **Add Reference** dialog box, on the **.NET** tab, select **Excel Services UDF Framework**.</span></span>
    
    > <span data-ttu-id="8af41-124">**Hinweis:** Sie können das Dialogfeld **Verweis hinzufügen** auch im Bereich **Projektmappen-Explorer** öffnen, indem Sie mit der rechten Maustaste auf **Verweise** klicken und **Verweis hinzufügen** auswählen.</span><span class="sxs-lookup"><span data-stu-id="8af41-124">**Note** You can also open the **Add Reference** dialog box in **Solution Explorer** by right-clicking **References** and selecting **Add Reference**.</span></span> 
3. <span data-ttu-id="8af41-125">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="8af41-125">Click **OK**.</span></span>
    
    > <span data-ttu-id="8af41-126">**Hinweis:** Bei den vorherigen Schritten wird vorausgesetzt, dass Sie das Projekt auf einem Computer erstellen, auf dem Microsoft SharePoint Server 2010 installiert ist.</span><span class="sxs-lookup"><span data-stu-id="8af41-126">**Note** The previous steps assume that you are building the project on a computer that has Microsoft SharePoint Server 2010 installed. On the computer where you have installed SharePoint Server 2010, you can find a copy of Microsoft.Office.Excel.Server.Udf.dll at:</span></span> <span data-ttu-id="8af41-127">Auf dem Computer, auf dem SharePoint Server 2010 installiert ist, finden Sie eine Kopie von Microsoft.Office.Excel.Server.Udf.dll: > [Laufwerk:]\\Program Files\\Common Files\\Microsoft Shared\\web server extensions\\14\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="8af41-127">On the computer where you have installed SharePoint Server 2010, you can find a copy of Microsoft.Office.Excel.Server.Udf.dll at:</span></span> 

## <a name="see-also"></a><span data-ttu-id="8af41-128">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="8af41-128">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="8af41-129">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="8af41-129">Tasks</span></span>


  
    
    
 [<span data-ttu-id="8af41-130">Step 2: Creating a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="8af41-130">Step 2: Creating a Managed-Code UDF</span></span>](step-2-creating-a-managed-code-udf.md)
  
    
    
 [<span data-ttu-id="8af41-131">Step 3: Deploying and Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="8af41-131">Step 3: Deploying and Enabling UDFs</span></span>](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [<span data-ttu-id="8af41-132">Step 4: Testing and Calling UDFs from Cells</span><span class="sxs-lookup"><span data-stu-id="8af41-132">Step 4: Testing and Calling UDFs from Cells</span></span>](step-4-testing-and-calling-udfs-from-cells.md)
  
    
    
 [<span data-ttu-id="8af41-133">How to: Create a UDF That Calls a Web Service</span><span class="sxs-lookup"><span data-stu-id="8af41-133">How to: Create a UDF That Calls a Web Service</span></span>](how-to-create-a-udf-that-calls-a-web-service.md)
#### <a name="concepts"></a><span data-ttu-id="8af41-134">Konzepte</span><span class="sxs-lookup"><span data-stu-id="8af41-134">Concepts</span></span>


  
    
    
 [<span data-ttu-id="8af41-135">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="8af41-135">Walkthrough: Developing a Managed-Code UDF</span></span>](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [<span data-ttu-id="8af41-136">Understanding Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="8af41-136">Understanding Excel Services UDFs</span></span>](understanding-excel-services-udfs.md)
