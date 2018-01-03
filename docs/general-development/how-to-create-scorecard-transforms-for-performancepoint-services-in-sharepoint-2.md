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
# <a name="create-scorecard-transforms-for-performancepoint-services-in-sharepoint"></a>Erstellen von Scorecardtransformationen für PerformancePoint-Dienste in SharePoint

In diesem Artikel erfahren Sie, wie benutzerdefinierte Scorecardtransformationen für PerformancePoint-Dienste in SharePoint erstellt werden.

## <a name="what-are-scorecard-transforms-in-performancepoint-services"></a>Was sind Scorecardtransformationen für PerformancePoint-Dienste?
<a name="bk_intro"> </a>

Ändern im PerformancePoint-Dienste scorecardtransformationen die Darstellung, Inhalte oder Ansichten vor dem Rendern in einem Dashboard. Weitere Informationen finden Sie unter  [PerformancePoint Services-Scorecardtransformationen (Übersicht)]((http://msdn.microsoft.com/library/d69d171b-827a-48a8-a3e1-7aaf0bfbc7f8%28Office.15%29.aspx)).
  
    
    

## <a name="create-transforms-for-performancepoint-services-scorecards"></a>Erstellen von Transformationen für PerformancePoint-Dienste scorecards
<a name="BKMK_CreateClass"> </a>


1. Installieren Sie PerformancePoint-Dienste oder kopieren Sie die DLLs, die mit PerformancePoint-Dienste auf Ihrem Computer installiert sind. Weitere Informationen finden Sie unter  [PerformancePoint-Dienste-DLLs in Entwicklungsszenarios]((http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx)).
    
  
2. Erstellen Sie in Visual Studio eine C#-Klassenbibliothek. Sollten Sie bereits eine Klassenbibliothek für die Erweiterung erstellt haben, fügen Sie eine neue C#-Klasse hinzu.
    
    Sie müssen die DLL mit einem starken Namen signieren, und stellen Sie sicher, dass alle Assemblys, die durch die DLL mit starkem Namen haben. Erfahren, wie beim Signieren einer Assembly mit einem starken Namen und ein öffentliches/privates Schlüsselpaar erstellen, finden Sie unter  [How to: Create a Public/Private Key Pair]((http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx)).
    
  
3. Fügen Sie Microsoft.PerformancePoint.Scorecards.Client.dll als Assemblyverweis zum Projekt hinzu.
    
  
4. Fügen Sie **using**-Anweisungen für die folgenden Namespaces hinzu:
    
  - **Microsoft.PerformancePoint.Scorecards**
    
  
  - **Microsoft.PerformancePoint.Scorecards.Extensions**
    
  
  - **System.Collections.Generic**
    
  
5. Implementieren Sie die  [IGridViewTransform]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.aspx)) -Schnittstelle.
    
  
6. Überschreiben Sie die  [GetId]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetId.aspx)) -Methode, um die Zeichenfolgebezeichner für Ihre Transformation zurückzugeben. [GetId]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetId.aspx)) muss die gleiche Zeichenfolge wie das Attribut **key** zurückgeben, die für die Transformation in der web.config-Datei PerformancePoint-Dienste registriert ist. Weitere Informationen zum Registrieren von Transformationen finden Sie unter [Gewusst wie: Manuelles Registrieren von PerformancePoint-Dienste-Erweiterungen]((http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx)).
    
  
7. Überschreiben Sie die  [GetTransformType]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetTransformType.aspx)) -Methode, um den Ausführungszeitpunkt für die Transformation anzugeben. Der Ausführungszeitpunkt einer Transformation hängt von deren Typ entsprechend der Definition durch die [GridViewTransformType]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.GridViewTransformType.aspx)) -Aufzählung ab: **PreQuery**, **PostQuery** oder **PreRender**. Weitere Informationen finden Sie unter  [PerformancePoint Services-Scorecardtransformationen (Übersicht)]((http://msdn.microsoft.com/library/d69d171b-827a-48a8-a3e1-7aaf0bfbc7f8%28Office.15%29.aspx)).
    
  
8. Überschreiben Sie die  [Execute]((https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.Execute.aspx)) -Methode zum Definieren der Transformation der Scorecard. Die folgenden Codebeispiele veranschaulichen das Hinzufügen einer Spalte zur Scorecardansicht und das Ändern der Formatierung leerer Scorecardzellen.
    
  
Nachdem Sie die DLL signiert und erstellt haben, installieren Sie die Erweiterung wie unter  [Gewusst wie: Manuelles Registrieren von PerformancePoint-Dienste-Erweiterungen]((http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx)) beschrieben.
## <a name="code-example-1-add-a-column-to-performancepoint-services-scorecards"></a>Codebeispiel 1: Hinzufügen einer Spalte zu PerformancePoint-Dienste Scorecards
<a name="bk_example1"> </a>

Das folgende Codebeispiel erstellt eine Transformation **PreQuery** einer Spalte zu Scorecardansichten gerenderten hinzu, die einen KPI auf spaltenblattebene enthalten. (Wenn die Scorecardansicht Elemente unter der KPIs enthält, wird die Spalte nicht hinzugefügt.)
  
    
    
Bevor Sie dieses Codebeispiel kompilieren können, müssen Sie die Entwicklungsumgebung konfigurieren, wie unter  [Erstellen von Transformationen für PerformancePoint-Dienste scorecards](#BKMK_CreateClass)beschrieben.
  
    
    



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


## <a name="code-example-2-change-the-format-of-empty-cells-in-performancepoint-services-scorecards"></a>Codebeispiel 2: Ändern Sie das Format der leeren Zellen in PerformancePoint-Dienste Scorecards
<a name="bk_example2"> </a>

Im folgenden Codebeispiel wird eine **PreQuery**-Transformation erstellt, die eine graue Hintergrundfarbe auf leere Scorecardzellen anwendet.
  
> [!NOTE]
> Bevor Sie dieses Codebeispiel kompilieren können, müssen Sie die Entwicklungsumgebung konfigurieren, wie unter  [Erstellen von Transformationen für PerformancePoint-Dienste-Scorecards](#BKMK_CreateClass)beschrieben. Darüber hinaus müssen Sie einen Verweis auf die **System.Drawing**-Assembly zu dem Projekt hinzufügen.
  
    
    


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


## <a name="see-also"></a>Siehe auch
<a name="bk_addResources"> </a>


-  [PerformancePoint-Dienste in SharePoint]((https://dev.office.com/sharepoint/docs/general-development/performancepoint-services-in-sharepoint))
    
  
-  [PerformancePoint Services-Scorecards]((http://msdn.microsoft.com/library/e77eccdb-82b3-483a-bb91-dfdc716400dd%28Office.15%29.aspx))
    
  

