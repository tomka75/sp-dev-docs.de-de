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
  
    
    

- Microsoft SharePoint Server 2010 
    
    > [!NOTE] 
    > Die einfachste Methode, um alles Erforderliche auf dem Server einzurichten, ist die Durchführung einer einfachen eigenständigen Installation. Abgesehen davon benötigen Sie nur noch einen vertrauenswürdigen Speicherort. 

- Excel
    
  
- Visual Studio oder ein vergleichbares mit Microsoft .NET Framework kompatibles Entwicklungstool
    
  
- Aktivieren der Ausführung der UDF-Assembly
    
  
- Eine vertrauenswürdige SharePoint-Dokumentbibliothek, in der eine Arbeitsmappe gespeichert werden soll. Für die Arbeitsmappe muss das Aufrufen von UDFs aktiviert sein, indem der **AllowUdfs**-Wert auf **true** festgelegt ist.
    
  
- Eine Beispielarbeitsmappe, die in einer vertrauenswürdigen SharePoint-Dokumentbibliothek gespeicherte UDFs aufruft
    
  
- Berechtigungen zum Anzeigen und Veröffentlichen einer Arbeitsmappe in einer SharePoint-Dokumentbibliothek
    
    > [!NOTE] 
    > Weitere Informationen zum Festlegen von Berechtigungen finden Sie in der Dokumentation zu Windows SharePoint Services 3.0. 

- Erstellen der Arbeitsmappe mithilfe von Excel
    
  
- Speichern der Arbeitsmappe als xlsx- oder xlsb-Datei
    
    > [!NOTE] 
    > Weitere Informationen dazu, wie Sie einen Speicherort als vertrauenswürdig festlegen, UDFs aktivieren und das **AllowUdfs**-Flag festlegen, finden Sie unter [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md). 

## <a name="see-also"></a>Siehe auch

- [Schritt 1: Erstellen eines Projekts und Hinzufügen einer UDF-Referenz](step-1-creating-a-project-and-adding-a-udf-reference.md)
- [Step 2: Creating a Managed-Code UDF](step-2-creating-a-managed-code-udf.md)
- [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md)
- [Step 4: Testing and Calling UDFs from Cells](step-4-testing-and-calling-udfs-from-cells.md)
- [Gewusst wie: Erstellen eines UDF, das einen Webdienst aufruft](how-to-create-a-udf-that-calls-a-web-service.md)
- [Grundlegendes zu Excel Services-UDFs](understanding-excel-services-udfs.md)
- [Schritt für Schritt: Entwickeln einer benutzerdefinierten Anwendung mit Excel Web Services](walkthrough-developing-a-custom-application-using-excel-web-services.md)
