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
# <a name="step-3-deploying-and-enabling-udfs"></a>Step 3: Deploying and Enabling UDFs

In this step, you will:
  
    
    


1. Deploy SampleUdf.dll, which you created in  [Step 2: Creating a Managed-Code UDF](step-2-creating-a-managed-code-udf.md), to a folder on a computer that has Microsoft SharePoint Server 2010 installed.
    
  
2. Allow user-defined functions (UDFs) to be called from a specific trusted location, for example, trusted Shared Documents location. 
    
  
3. Enable SampleUdf.dll.
    
  

## <a name="deploying-udfs"></a>Deploying UDFs


### <a name="to-deploy-udfs"></a>To deploy UDFs


1. Create a folder named "UDFs" on the local drive of the computer to which you want to deploy UDFs. For example, "C:\\UDFs".
    
  
2. Copy the SampleUdf.dll assembly.
    
  
3. Save SampleUdf.dll in "C:\\UDFs". 
    
  

## <a name="trusting-a-location"></a>Trusting a Location


### <a name="to-trust-a-location"></a>To trust a location


1. On the **Start** menu, click **All Programs**. 
    
  
2. Point to **Microsoft SharePoint 2010 Products** and click **SharePoint Central Administration**. 
    
  
3. Under **Application Management** click **Manage service applications**.
    
  
4. On the Manage Service Applications page, click **Excel Services Application**.
    
  
5. On the **Excel Services Application** page, click **Trusted File Locations**.
    
  
6. On the Trusted File Locations page, click **Add Trusted File Location**. 
    
  
7. On the Add Trusted File Location page, in the **Address** box, type the location where you will save your workbookfor example, _http://MyServer002/Shared%20Documents_. 
    
  
8. Under **Location type**, click the appropriate location type. In this example, select Microsoft SharePoint Foundation.
    
  
9. Under **Trust Children**, select **Children trusted** to trust child libraries or directories.
    
  
10. Under **Allow User-Defined Functions**, select **User-defined functions allowed** to allow UDFs to be called from workbooks stored in this trusted location.
    
  
11. Klicken Sie auf **OK**.
    
  

## <a name="enabling-udfs"></a>Enabling UDFs

To do the following steps, you need a computer that has SharePoint Server 2010 installed.
  
    
    

### <a name="to-enable-udfs"></a>To enable UDFs


1. Follow steps 1 through 3 in the previous procedure ("To trust a location") to display the Shared Services home page for an SSP.
    
  
2. Klicken Sie unter **Excel Services-Einstellungen** auf **Benutzerdefinierte Funktionsassemblys**. 
    
  
3. Klicken Sie auf der Seite „Benutzerdefinierte Funktionen von Excel Services“ auf **Benutzerdefinierte Funktion hinzufügen**, um die Seite „Excel Services: Benutzerdefinierte Funktionsassembly hinzufügen“ aufzurufen.
    
  
4. Geben Sie in das Feld **Assembly** den Pfad zu der Assembly SampleUdf.dll ein. In diesem Beispiel wäre dies _C:\\UDFs\\SampleUdf.dll_.
    
  
5. Under **Assembly Location**, click **File path**.
    
  
6. Under **Enable Assembly**, the **Assembly enabled** check box should be selected by default.
    
  
7. Klicken Sie auf **OK**.
    
  

## <a name="robust-programming"></a>Robuste Programmierung

Ist der **AllowUdfs**-Wert **false**, wenn eine Sitzung in einer Arbeitsmappe mit UDF-Aufrufen gestartet wird, tritt bei den UDF-Aufrufen ein Fehler auf.
  
> [!NOTE]
> Das **AllowUdfs**-Flag wird durch die Option **Benutzerdefinierte Funktionen sind zulässig** angegeben (siehe Schritt 9 im Abschnitt „Festlegen eines vertrauenswürdigen Speicherorts“).
  
    
    

If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session. You can get around this by resetting Microsoft Internet Information Services (IIS). Resetting IIS will reload UDFs.  
    
For more information about resetting IIS, see  [How to: Enable UDFs](how-to-enable-udfs.md).
  
## <a name="see-also"></a>Siehe auch

- [Schritt 1: Erstellen eines Projekts und Hinzufügen einer UDF-Referenz](step-1-creating-a-project-and-adding-a-udf-reference.md)
- [Step 2: Creating a Managed-Code UDF](step-2-creating-a-managed-code-udf.md)
- [Step 4: Testing and Calling UDFs from Cells](step-4-testing-and-calling-udfs-from-cells.md)
- [Gewusst wie: Aktivieren von UDFs](how-to-enable-udfs.md)
- [Exemplarische Vorgehensweise: Entwickeln eines UDF auf Basis von verwaltetem Code](walkthrough-developing-a-managed-code-udf.md)
- [Understanding Excel Services UDFs](understanding-excel-services-udfs.md)
