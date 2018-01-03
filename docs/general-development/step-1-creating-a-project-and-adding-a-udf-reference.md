---
title: Step 1 Creating a Project and Adding a UDF Reference
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4c6f1279-28df-45af-8488-42a6573d526d
ms.openlocfilehash: f4ccef885ce00bdad740154890d81c9495b02c86
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="step-1-creating-a-project-and-adding-a-udf-reference"></a>Step 1: Creating a Project and Adding a UDF Reference

In this step, you will create a project and add a reference to Microsoft.Office.Excel.Server.Udf.dll. 
  
    
    


## <a name="creating-the-project"></a>Erstellen des Projekts

Im folgenden Projekt wird Microsoft Visual Studio 2005 verwendet.
  
> [!NOTE]
> Je nachdem, welche Einstellungen Sie in der der integrierten Entwicklungsumgebung von Visual Studio verwenden, kann das Verfahren zum Erstellen eines Projekts geringfügig von dem hier beschriebenen Verfahren abweichen. 
  
    
    


### <a name="to-create-a-project"></a>So erstellen Sie ein Projekt


1. Starten Sie Visual Studio.
    
  
2. Zeigen Sie im Menü **Datei** auf **Neu**, und klicken Sie dann auf **Projekt**. Das Dialogfeld **Neues Projekt** wird angezeigt.
    
  
3. In the **Project Type** pane, select **Visual C# Projects**.
    
  
4. In the **Templates** pane, click **Class Library**.
    
  
5. In the **Name** box, type **SampleUdf**.
    
  
6. In the **Location** box, type the path where you want to save your project, or click **Browse** to navigate to the folder.
    
  
7. Click **OK**. Your new project appears in **Solution Explorer**. You also will see that a file with the default name of Class1.cs has been added to your project.
    
  
8. You should see the following code in the Class1.cs file:
    
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


## <a name="adding-a-reference"></a>Adding a Reference

The following steps show how to locate Microsoft.Office.Excel.Server.Udf.dll and how to add a reference to it. 
  
    
    

### <a name="to-add-a-reference"></a>To add a reference


1. On the **Project** menu, click **Add Reference**.
    
  
2. Wählen Sie im Dialogfeld **Verweis hinzufügen** der Registerkarte **.NET** **Excel Services UDF Framework**.
    
    > [!NOTE]
    > Sie können das Dialogfeld **Verweis hinzufügen** auch im Bereich **Projektmappen-Explorer** öffnen, indem Sie mit der rechten Maustaste auf **Verweise** klicken und **Verweis hinzufügen** auswählen. 

3. Klicken Sie auf **OK**.
    
    > [!NOTE]
    > Bei den vorherigen Schritten wird vorausgesetzt, dass Sie das Projekt auf einem Computer erstellen, auf dem Microsoft SharePoint Server 2010 installiert ist. Auf dem Computer, auf dem SharePoint Server 2010 installiert ist, finden Sie eine Kopie von Microsoft.Office.Excel.Server.Udf.dll: > [Laufwerk:]\\Program Files\\Common Files\\Microsoft Shared\\web server extensions\\14\\ISAPI 

## <a name="see-also"></a>Siehe auch

- [Schritt 2: Erstellen eines UDF auf Basis von verwaltetem Code](step-2-creating-a-managed-code-udf.md)
- [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md)
- [Step 4: Testing and Calling UDFs from Cells](step-4-testing-and-calling-udfs-from-cells.md)
- [Gewusst wie: Erstellen eines UDF, das einen Webdienst aufruft](how-to-create-a-udf-that-calls-a-web-service.md)
- [Exemplarische Vorgehensweise: Entwickeln eines UDF auf Basis von verwaltetem Code](walkthrough-developing-a-managed-code-udf.md)
- [Understanding Excel Services UDFs](understanding-excel-services-udfs.md)
