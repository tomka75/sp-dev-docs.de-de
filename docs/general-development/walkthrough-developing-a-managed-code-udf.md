---
title: Walkthrough Developing a Managed-Code UDF
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e6a00833-0606-4a7d-91c3-b89a6e340348
ms.openlocfilehash: 6b946672852a8aa7b3dcfb17b16997048bb3f521
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="walkthrough-developing-a-managed-code-udf"></a>Walkthrough: Developing a Managed-Code UDF

This walkthrough describes the process for developing Excel Services user-defined functions (UDFs) using Microsoft Visual C#.
  
    
    

During this walkthrough, you will learn how to:
- Create a project using the Microsoft Visual Studio 2005 class library project template.
    
  
- Add a reference to Microsoft.Office.Excel.Server.Udf.dll.
    
  
- Write UDFs for use in Excel Services.
    
  
- Create a workbook to call custom functions from cells.
    
  
- Test and run UDFs in Excel Services.
    
  

## <a name="prerequisites"></a>Voraussetzungen

In order to complete this walkthrough, you will need: 
  
    
    

- Microsoft SharePoint Server 2010. 
    
    > **Hinweis:** Die einfachste Methode, um alles Erforderliche auf dem Server einzurichten, ist die Durchführung einer einfachen eigenständigen Installation. Weitere Anforderungen: Ein vertrauenswürdiger Speicherort. 
- Excel.
    
  
- Visual Studio or a similar Microsoft .NET Framework-compatible development tool.
    
  
- To enable running the UDF assembly.
    
  
- A trusted SharePoint document library in which to store a workbook, and to allow the workbook to call UDFs by setting the **AllowUdfs** value to **true**. 
    
  
- A sample workbook that calls the UDF stored in a trusted SharePoint document library. 
    
  
- Berechtigungen zum Anzeigen und Veröffentlichen einer Arbeitsmappe in einer SharePoint-Dokumentbibliothek. 
    
    > **Hinweis:** Weitere Informationen zum Festlegen von Berechtigungen finden Sie in der Dokumentation zu Windows SharePoint Services 3.0. 
- Erstellen der Arbeitsmappe mithilfe von Excel.
    
  
- Speichern der Arbeitsmappe als xlsx- oder xlsb-Datei.
    
    > **Hinweis:** Weitere Informationen, wie Sie einen vertrauenswürdigen Speicherort erkennen, UDFs aktivieren und die **AllowUdfs**-Kennzeichnung angeben, finden Sie unter [Schritt 3: Bereitstellen und Aktivieren von UDFs](step-3-deploying-and-enabling-udfs.md). 

## <a name="see-also"></a>Siehe auch


#### <a name="tasks"></a>Aufgaben


  
    
    
 [Step 1: Creating a Project and Adding a UDF Reference](step-1-creating-a-project-and-adding-a-udf-reference.md)
  
    
    
 [Step 2: Creating a Managed-Code UDF](step-2-creating-a-managed-code-udf.md)
  
    
    
 [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [Step 4: Testing and Calling UDFs from Cells](step-4-testing-and-calling-udfs-from-cells.md)
  
    
    
 [How to: Create a UDF That Calls a Web Service](how-to-create-a-udf-that-calls-a-web-service.md)
#### <a name="concepts"></a>Konzepte


  
    
    
 [Understanding Excel Services UDFs](understanding-excel-services-udfs.md)
#### <a name="other-resources"></a>Sonstige Ressourcen


  
    
    
 [Walkthrough: Developing a Custom Application Using Excel Web Services](walkthrough-developing-a-custom-application-using-excel-web-services.md)
