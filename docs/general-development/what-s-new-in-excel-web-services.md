---
title: Neuigkeiten in Excel Web Services
ms.prod: SHAREPOINT
ms.assetid: cb342e94-0308-4608-b027-b73ebe8107b0
ms.openlocfilehash: f5aceebaf28e8caf4ac99beb97de6b87e21d149c
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2017
---
# <a name="whats-new-in-excel-web-services"></a>Neuigkeiten in Excel Web Services

This topic lists the new types and members added to Excel Web Services.
  
    
    


## <a name="excel-web-services-enhancements"></a>Excel Web Services Enhancements

Excel Web Services is expanded and enhanced in Microsoft SharePoint Server 2010. In SharePoint Server 2010, you can edit and save a workbook programmatically. In addition, the Excel Web Services now supports opening workbooks in edit sessions in SharePoint Server 2010. In this scenario, you can use code to edit a workbook at the same time that other users are co-authoring the workbook.
  
    
    
For more information about the Excel Web Services API and more detailed remarks about the new methods, enumerations, and types, see **Microsoft.Office.Excel.Server.WebServices**.
  
    
    

### <a name="new-methods"></a>Neue Methoden

The following are new methods added to Excel Web Services, in alphabetical order: 
  
    
    

- **GetChartImageUrl** Gets a URL value to the chart or PivotChart image file in a workbook.
    
  
- **GetPublishedItemNames** Gets a list of published items in a workbook.
    
  
- **GetSheetNames** Gets a list of all of the sheet names present in a workbook.
    
  
- **OpenWorkbookForEditing** Opens a workbook for editing.
    
  
- **SaveWorkbook** Saves a workbook in the original format (.xlsx, .xlsb, .xlsm).
    
  
- **SaveWorkbookCopy** Saves a workbook by using a different file name and/or saves a workbook to a different SharePoint document library.
    
  
- **SetCalculationOptions** Changes the calculation mode setting for workbooks.
    
  
- **SetParameters** Sets multiple published parameters with a single Web Service call.
    
  
Weitere Schritte:
  
    
    

- You can now set formulas by using the set value methods.
    
  
- Dynamic ranges are supported in Excel Web Services in SharePoint Server 2010.
    
  

### <a name="new-enumerations"></a>New Enumerations

The following are new enumerations added to Excel Web Services, in alphabetical order:
  
    
    

- **ItemType** Indicates the types of the returned items.
    
  
- **SheetType** Indicates the types of the returned sheets.
    
  
- **SheetVisibility** Indicates whether the returned sheets are visible.
    
  
- **SaveOptions** Specifies whether to overwrite an existing, unlocked file.
    
  
- **WorkbookCalculation** Defines the calculation mode setting for a workbook.
    
  

### <a name="new-types"></a>New Types

The following are new types added to Excel Web Services, in alphabetical order:
  
    
    

- **ParameterInfo** Gets or sets the name and values of a parameter.
    
  
- **SheetInfo** Contains information about a sheet in a workbook.
    
  
- **Size** Defines the width and height of the chart image
    
  
- **WorkbookItem** Represents named items in the workbook.
    
  

## <a name="see-also"></a>Siehe auch


#### <a name="other-resources"></a>Sonstige Ressourcen


  
    
    
 [Walkthrough: Developing a Custom Application Using Excel Web Services](walkthrough-developing-a-custom-application-using-excel-web-services)
