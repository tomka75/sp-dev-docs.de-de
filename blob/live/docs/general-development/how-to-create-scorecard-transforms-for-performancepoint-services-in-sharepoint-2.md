---
title: "Erstellen von Scorecardtransformationen für PerformancePoint-Dienste in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: cdcb54a17b5575524acfaa5400234401f150eaa1
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="create-scorecard-transforms-for-performancepoint-services-in-sharepoint"></a><span data-ttu-id="6bb62-102">Erstellen von Scorecardtransformationen für PerformancePoint-Dienste in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6bb62-102">Create scorecard transforms for PerformancePoint Services in SharePoint</span></span>

<span data-ttu-id="6bb62-103">In diesem Artikel erfahren Sie, wie benutzerdefinierte Scorecardtransformationen für PerformancePoint-Dienste in SharePoint erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="6bb62-103">Learn how to create custom scorecard transforms for PerformancePoint Services in SharePoint.</span></span>

## <a name="what-are-scorecard-transforms-in-performancepoint-services"></a><span data-ttu-id="6bb62-104">Was sind Scorecardtransformationen für PerformancePoint-Dienste?</span><span class="sxs-lookup"><span data-stu-id="6bb62-104">What are scorecard transforms in PerformancePoint Services?</span></span>
<span data-ttu-id="6bb62-105"><a name="bk_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="6bb62-105"><a name="bk_intro"> </a></span></span>

<span data-ttu-id="6bb62-p101">Ändern im PerformancePoint-Dienste scorecardtransformationen die Darstellung, Inhalte oder Ansichten vor dem Rendern in einem Dashboard. Weitere Informationen finden Sie unter  [PerformancePoint Services-Scorecardtransformationen (Übersicht)]((http://msdn.microsoft.com/library/d69d171b-827a-48a8-a3e1-7aaf0bfbc7f8%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="6bb62-p101">In PerformancePoint Services, scorecard transforms change the appearance, content, or functionality of scorecard views before they render in a dashboard. For more information, see  [Types of Transforms]((http://msdn.microsoft.com/library/d69d171b-827a-48a8-a3e1-7aaf0bfbc7f8%28Office.15%29.aspx)).</span></span>
  
    
    

## <a name="create-transforms-for-performancepoint-services-scorecards"></a><span data-ttu-id="6bb62-108">Erstellen von Transformationen für PerformancePoint-Dienste scorecards</span><span class="sxs-lookup"><span data-stu-id="6bb62-108">Create transforms for PerformancePoint Services scorecards</span></span>
<span data-ttu-id="6bb62-109"><a name="BKMK_CreateClass"> </a></span><span class="sxs-lookup"><span data-stu-id="6bb62-109"><a name="BKMK_CreateClass"> </a></span></span>


1. <span data-ttu-id="6bb62-p102">Installieren Sie PerformancePoint-Dienste oder kopieren Sie die DLLs, die mit PerformancePoint-Dienste auf Ihrem Computer installiert sind. Weitere Informationen finden Sie unter  [PerformancePoint-Dienste-DLLs in Entwicklungsszenarios]((http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="6bb62-p102">Install PerformancePoint Services, or copy the DLLs that are installed with PerformancePoint Services to your computer. For more information, see  [DLLs with Class Libraries]((http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx)).</span></span>
    
  
2. <span data-ttu-id="6bb62-p103">Erstellen Sie in Visual Studio eine C#-Klassenbibliothek. Sollten Sie bereits eine Klassenbibliothek für die Erweiterung erstellt haben, fügen Sie eine neue C#-Klasse hinzu.</span><span class="sxs-lookup"><span data-stu-id="6bb62-p103">In Visual Studio, create a C# class library. If you have already created a class library for your extension, add a new C# class.</span></span>
    
    <span data-ttu-id="6bb62-p104">Sie müssen die DLL mit einem starken Namen signieren, und stellen Sie sicher, dass alle Assemblys, die durch die DLL mit starkem Namen haben. Erfahren, wie beim Signieren einer Assembly mit einem starken Namen und ein öffentliches/privates Schlüsselpaar erstellen, finden Sie unter  [How to: Create a Public/Private Key Pair]((http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx)).</span><span class="sxs-lookup"><span data-stu-id="6bb62-p104">You must sign your DLL with a strong name, and ensure that all assemblies referenced by your DLL have strong names. To learn how to sign an assembly with a strong name and how to create a public/private key pair, see  [How to: Create a Public/Private Key Pair]((http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx)).</span></span>
    
  
3. <span data-ttu-id="6bb62-116">Fügen Sie Microsoft.PerformancePoint.Scorecards.Client.dll als Assemblyverweis zum Projekt hinzu.</span><span class="sxs-lookup"><span data-stu-id="6bb62-116">Add Microsoft.PerformancePoint.Scorecards.Client.dll as an assembly reference to the project.</span></span>
    
  
4. <span data-ttu-id="6bb62-117">Fügen Sie **using**-Anweisungen für die folgenden Namespaces hinzu:</span><span class="sxs-lookup"><span data-stu-id="6bb62-117">Add **using** directives for the following namespaces:</span></span>
    
  - <span data-ttu-id="6bb62-118">**Microsoft.PerformancePoint.Scorecards**</span><span class="sxs-lookup"><span data-stu-id="6bb62-118">**Microsoft.PerformancePoint.Scorecards**</span></span>
    
  
  - <span data-ttu-id="6bb62-119">**Microsoft.PerformancePoint.Scorecards.Extensions**</span><span class="sxs-lookup"><span data-stu-id="6bb62-119">**Microsoft.PerformancePoint.Scorecards.Extensions**</span></span>
    
  
  - <span data-ttu-id="6bb62-120">**System.Collections.Generic**</span><span class="sxs-lookup"><span data-stu-id="6bb62-120">**System.Collections.Generic**</span></span>
    
  
5. <span data-ttu-id="6bb62-121">Implementieren Sie die  [IGridViewTransform]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.aspx)) -Schnittstelle.</span><span class="sxs-lookup"><span data-stu-id="6bb62-121">Implement the  [IGridViewTransform]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.aspx)) interface.</span></span>
    
  
6. <span data-ttu-id="6bb62-p105">Überschreiben Sie die  [GetId]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetId.aspx)) -Methode, um die Zeichenfolgebezeichner für Ihre Transformation zurückzugeben. [GetId]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetId.aspx)) muss die gleiche Zeichenfolge wie das Attribut **key** zurückgeben, die für die Transformation in der web.config-Datei PerformancePoint-Dienste registriert ist. Weitere Informationen zum Registrieren von Transformationen finden Sie unter [Gewusst wie: Manuelles Registrieren von PerformancePoint-Dienste-Erweiterungen]((http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="6bb62-p105">Override the  [GetId]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetId.aspx)) method to return the string identifier for your transform. [GetId]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetId.aspx)) must return the same string as the **key** attribute that is registered for the transform in the PerformancePoint Services web.config file. For more information about registering scorecard transforms, see [How to: Manually Register PerformancePoint Services Extensions]((http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx)).</span></span>
    
  
7. <span data-ttu-id="6bb62-p106">Überschreiben Sie die  [GetTransformType]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetTransformType.aspx)) -Methode, um den Ausführungszeitpunkt für die Transformation anzugeben. Der Ausführungszeitpunkt einer Transformation hängt von deren Typ entsprechend der Definition durch die [GridViewTransformType]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.GridViewTransformType.aspx)) -Aufzählung ab: **PreQuery**, **PostQuery** oder **PreRender**. Weitere Informationen finden Sie unter  [PerformancePoint Services-Scorecardtransformationen (Übersicht)]((http://msdn.microsoft.com/library/d69d171b-827a-48a8-a3e1-7aaf0bfbc7f8%28Office.15%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="6bb62-p106">Override the  [GetTransformType]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetTransformType.aspx)) method to specify when to run the transform. The point at which a transform runs depends on its type, as defined by the [GridViewTransformType]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.GridViewTransformType.aspx)) enumeration: **PreQuery**, **PostQuery**, or **PreRender**. For more information, see  [Types of Transforms]((http://msdn.microsoft.com/library/d69d171b-827a-48a8-a3e1-7aaf0bfbc7f8%28Office.15%29.aspx)).</span></span>
    
  
8. <span data-ttu-id="6bb62-p107">Überschreiben Sie die  [Execute]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.Execute.aspx)) -Methode zum Definieren der Transformation der Scorecard. Die folgenden Codebeispiele veranschaulichen das Hinzufügen einer Spalte zur Scorecardansicht und das Ändern der Formatierung leerer Scorecardzellen.</span><span class="sxs-lookup"><span data-stu-id="6bb62-p107">Override the  [Execute]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.Execute.aspx)) method to define how to transform the scorecard. The following code examples show how to add a column to a scorecard view and how to change the formatting of empty scorecard cells.</span></span>
    
  
<span data-ttu-id="6bb62-130">Nachdem Sie die DLL signiert und erstellt haben, installieren Sie die Erweiterung wie unter  [Gewusst wie: Manuelles Registrieren von PerformancePoint-Dienste-Erweiterungen]((http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx)) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="6bb62-130">After you sign and build your DLL, install the extension as described in  [How to: Manually Register PerformancePoint Services Extensions]((http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx)).</span></span>
## <a name="code-example-1-add-a-column-to-performancepoint-services-scorecards"></a><span data-ttu-id="6bb62-131">Codebeispiel 1: Hinzufügen einer Spalte zu PerformancePoint-Dienste Scorecards</span><span class="sxs-lookup"><span data-stu-id="6bb62-131">Code example 1: Add a column to PerformancePoint Services scorecards</span></span>
<span data-ttu-id="6bb62-132"><a name="bk_example1"> </a></span><span class="sxs-lookup"><span data-stu-id="6bb62-132"><a name="bk_example1"> </a></span></span>

<span data-ttu-id="6bb62-p108">Das folgende Codebeispiel erstellt eine Transformation **PreQuery** einer Spalte zu Scorecardansichten gerenderten hinzu, die einen KPI auf spaltenblattebene enthalten. (Wenn die Scorecardansicht Elemente unter der KPIs enthält, wird die Spalte nicht hinzugefügt.)</span><span class="sxs-lookup"><span data-stu-id="6bb62-p108">The following code example creates a **PreQuery** transform that adds a column to rendered scorecard views that contain a KPI at the column leaf level. (If the scorecard view includes members below the KPIs, the column is not added.)</span></span>
  
    
    
<span data-ttu-id="6bb62-135">Bevor Sie dieses Codebeispiel kompilieren können, müssen Sie die Entwicklungsumgebung konfigurieren, wie unter  [Erstellen von Transformationen für PerformancePoint-Dienste scorecards](#BKMK_CreateClass)beschrieben.</span><span class="sxs-lookup"><span data-stu-id="6bb62-135">Before you can compile this code example, you must configure your development environment as described in  [Create transforms for PerformancePoint Services scorecards](#BKMK_CreateClass).</span></span>
  
    
    



```cs

using System;
using System.Collections.Generic;
using Microsoft.PerformancePoint.Scorecards;
using Microsoft.PerformancePoint.Scorecards.Extensions;

namespace Microsoft.PerformancePoint.SDK.Samples.ScorecardTransforms.PreQuery
{

    // Represents the class that adds columns of data to a scorecard view. 
    public class AddColumnTransform : IGridViewTransform
    {

        // Set transform type to PreQuery.
        public GridViewTransformType GetTransformType()
        {
            return GridViewTransformType.PreQuery;
        }

        // Return the string identifier of your transform. This value must
        // match the key attribute registered in the web.config file.
        public string GetId()
        {
            return "AddColumn";
        }

        // Run the transform to add a column. 
        public void Execute(GridViewData viewData, PropertyBag parameters, IGlobalCache cache)
        {
            // Verify the scorecard definition.
            if (viewData == null)
            {
                throw new ArgumentException("Parameter cannot be null", "viewData");
            }
                     
            List<GridHeaderItem> leafRowHeaders = viewData.RootRowHeader.GetAllLeafHeadersInTree();

            foreach (GridHeaderItem rowHeader in leafRowHeaders)
            {
                if (rowHeader.HeaderType == ScorecardNodeTypes.Kpi)
                {
                    Kpi kpi = cache.GetKpi(rowHeader.LinkedKpiLocation);
                    if (kpi != null &amp;&amp; viewData.RootColumnHeader != null)
                    {

                        // Create the column header and add it to the root.
                        GridHeaderItem theNewColumn = GridHeaderItem.CreateDetailsHeader(kpi.Owner.DisplayName);

                        // Set the GUIDs for the data headers.
                        // Setting the DefinitionGuid property to the
                        // same value as the root column header enables
                        // Dashboard Designer to display the scorecard. 
                        // Note: Do not try to modify or delete the new
                        // column from within Dashboard Designer.
                        theNewColumn.DefinitionGuid = viewData.RootColumnHeader.DefinitionGuid;
                        theNewColumn.Parent = viewData.RootColumnHeader;
                        theNewColumn.Guid = new Guid();

                        // Insert the column at the end of the collection
                        // of child elements.
                        if (viewData.RootColumnHeader.Children.Count != 0)
                        {
                            viewData.RootColumnHeader.Children.Insert(viewData.RootColumnHeader.Children.Count, theNewColumn);
                        }
                                                                         
                        break;
                    }
                }
            }
            viewData.RootColumnHeader.LinkAndIndexTreeFromRoot();
        }
    }
}
```


## <a name="code-example-2-change-the-format-of-empty-cells-in-performancepoint-services-scorecards"></a><span data-ttu-id="6bb62-136">Codebeispiel 2: Ändern Sie das Format der leeren Zellen in PerformancePoint-Dienste Scorecards</span><span class="sxs-lookup"><span data-stu-id="6bb62-136">Code example 2: Change the format of empty cells in PerformancePoint Services scorecards</span></span>
<span data-ttu-id="6bb62-137"><a name="bk_example2"> </a></span><span class="sxs-lookup"><span data-stu-id="6bb62-137"><a name="bk_example2"> </a></span></span>

<span data-ttu-id="6bb62-138">Im folgenden Codebeispiel wird eine **PreQuery**-Transformation erstellt, die eine graue Hintergrundfarbe auf leere Scorecardzellen anwendet.</span><span class="sxs-lookup"><span data-stu-id="6bb62-138">The following code example creates a **PreQuery** transform that applies a grey background color to empty scorecard cells.</span></span>
  
> [!NOTE]
> <span data-ttu-id="6bb62-139">Bevor Sie dieses Codebeispiel kompilieren können, müssen Sie die Entwicklungsumgebung konfigurieren, wie unter  [Erstellen von Transformationen für PerformancePoint-Dienste-Scorecards](#BKMK_CreateClass)beschrieben.</span><span class="sxs-lookup"><span data-stu-id="6bb62-139">Before you can compile this code example, you must configure your development environment as described in  [Create transforms for PerformancePoint Services scorecards](#BKMK_CreateClass).</span></span> <span data-ttu-id="6bb62-140">Darüber hinaus müssen Sie einen Verweis auf die **System.Drawing**-Assembly zu dem Projekt hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="6bb62-140">In addition, you must add a reference to the **System.Drawing** assembly to your project.</span></span>
  
    
    


```cs

using System;
using System.Collections.Generic;
using Microsoft.PerformancePoint.Scorecards;
using Microsoft.PerformancePoint.Scorecards.Extensions;

namespace Microsoft.PerformancePoint.SDK.Samples
{

    // Represents a transform that applies a grey background color to empty scorecard cells.
    public class GreyEmptiesTransform : IGridViewTransform
    {

        // Set the transform type to "PreRender".
        public GridViewTransformType GetTransformType()
        {
            return GridViewTransformType.PreRender;
        }

        // Return the string identifier of the transform.
        public string GetId()
        {
            return "GreyEmptyCells";
        }

        // Run the transform.
        public void Execute(GridViewData viewData, PropertyBag parameters, IGlobalCache cache)
        {
            // Validate parameters. 
            if (viewData == null)
            {
                throw new ArgumentException("Parameter cannot be null", "viewData");
            }

            // Get the headers under the root row header.
            List<GridHeaderItem> nonLeafRowHeaders = viewData.RootRowHeader.GetAllHeadersInTree();

            // Get the leaf headers under the root column header.
            List<GridHeaderItem> leafColumnHeaders = viewData.RootColumnHeader.GetAllLeafHeadersInTree();

            foreach (GridHeaderItem rowHeader in nonLeafRowHeaders)
            {
                foreach (GridHeaderItem columnHeader in leafColumnHeaders)
                {
                    // Get scorecard cells.
                    GridCell cell = viewData.Cells[rowHeader, columnHeader];

                    if (cell.IsCellEmpty || string.IsNullOrEmpty(cell.ActualValue.ToString()))
                    {
                        GridFormatInfo emptyFormat = new GridFormatInfo(viewData.DefaultCellFormatInfo);
                        emptyFormat.BackColor = new GridColor(System.Drawing.Color.Gray);
                        cell.FormatInfo = emptyFormat;
                    }
                    viewData.Cells[rowHeader, columnHeader] = cell;
                }
            }
        }
    }
}


```


## <a name="see-also"></a><span data-ttu-id="6bb62-141">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="6bb62-141">See also</span></span>
<span data-ttu-id="6bb62-142"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="6bb62-142"><a name="bk_addResources"> </a></span></span>


-  <span data-ttu-id="6bb62-143">[PerformancePoint-Dienste in SharePoint]((https://dev.office.com/sharepoint/docs/general-development/performancepoint-services-in-sharepoint))</span><span class="sxs-lookup"><span data-stu-id="6bb62-143">[PerformancePoint Services in SharePoint]((https://dev.office.com/sharepoint/docs/general-development/performancepoint-services-in-sharepoint))</span></span>
    
  
-  <span data-ttu-id="6bb62-144">[PerformancePoint Services-Scorecards]((http://msdn.microsoft.com/library/e77eccdb-82b3-483a-bb91-dfdc716400dd%28Office.15%29.aspx))</span><span class="sxs-lookup"><span data-stu-id="6bb62-144">[PerformancePoint Services Scorecards]((http://msdn.microsoft.com/library/e77eccdb-82b3-483a-bb91-dfdc716400dd%28Office.15%29.aspx))</span></span>
    
  

