---
title: Speichern vom Excel-Client auf dem Server
ms.date: 09/25/2017
keywords: how to,howdoi,howto
f1_keywords: how to,howdoi,howto
ms.prod: sharepoint
ms.assetid: 28716ba5-0774-44df-833b-0034d2c63319
ms.openlocfilehash: 18868cec79119123cf8262b9b93e9fd7eca1571f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="save-from-excel-client-to-the-server"></a>Speichern vom Excel-Client auf dem Server

This example shows you how to:

1. Create a workbook with editable ranges.
    
  
2. Speichern Sie die Arbeitsmappe in einer SharePoint-Dokumentbibliothek, die einen vertrauenswürdigen Speicherort darstellt.
    
    > [!NOTE]
    > Es wird vorausgesetzt, dass Sie bereits eine SharePoint-Dokumentbibliothek erstellt und diese als vertrauenswürdigen Speicherort definiert haben. Weitere Informationen finden Sie unter [Gewusst wie: Vertrauen zu einem Standort](how-to-trust-a-location.md).

3. Ändern Sie Werte in einer Arbeitsmappe mithilfe des Parameterbereich in Excel Web Access.
    
  

## <a name="saving-a-workbook-to-excel-services"></a>Saving a Workbook to Excel Services


### <a name="to-create-a-workbook-with-ranges"></a>To create a workbook with ranges


1. Start Excel.
    
  
2. In cell A1, type 8.
    
  
3. In cell A2, type =3*A1.
    
  
4. To make cell A1 editable in Excel Web Access, you must first make cell A1 into a named range: 
    
1. Click the **Formulas** tab, and then click cell **A1** to select it.
    
  
2. On the **Formulas** tab, in the **Defined Names** group, click **Define Name**.
    
  
3. In the **New Name** dialog box, in the **Name** text box, typeMyAOneParam.
    
  

### <a name="to-save-to-excel-services"></a>To save to Excel Services


1. On the **File** menu, click **Save &amp; Send**, and then click **Save to SharePoint**. 
    
  
2. In the **Save to SharePoint** dialog box, click **Publish Options**.
    
  
3. In the **Publish Options** dialog box, on the **Show** tab, ensure that **Entire Workbook** is selected.
    
  
4. On the **Parameters** tab, click **Add**..
    
  
5. In the **Add Parameters** list, select the **MyAOneParam** check box.
    
  
6. Click **OK**. You should now see "MyAOneParam" in the **Parameters** list.
    
  
7. Click **OK** to close the **Publish Options** dialog box.
    
  
8. In the **Save to SharePoint** dialog box, click **Save As**.
    
  
9. In the **Save As** dialog box, ensure that the **Open with Excel in the browser** check box is selected.
    
  
10. In the **File name** text box, type the path to the trusted SharePoint document library where you want to store this workbook. For example,http:// _MyServer002_/Shared%20Documents/TestParam.xlsx.
    
  
11. Click **Save**. You should see TestParam.xlsx in Excel Web Access. 
    
  

### <a name="to-change-values-by-using-parameters"></a>To change values by using parameters


1. In the **Parameters** pane, you should see the named range for cell **A1**that is, **MyAOneParam**. 
    
  
2. You can change the values in cell **A1** and cell **A2** by typing a number in the text box next to **MyAOneParam**. For example, if you type 10 and then click **Apply**, cell **A1** changes to **10** and cell **A2** changes to **30**. 
    
  

## <a name="see-also"></a>Siehe auch


#### <a name="tasks"></a>Aufgaben


  
    
    
 [How to: Save to the Server to Prepare for Programmatic Access](how-to-save-to-the-server-to-prepare-for-programmatic-access.md)
#### <a name="concepts"></a>Konzepte


  
    
    
 [Accessing the SOAP API](accessing-the-soap-api.md)
  
    
    
 [Loop-Back SOAP Calls and Direct Linking](loop-back-soap-calls-and-direct-linking.md)
  
    
    
 [Excel Services Alerts](excel-services-alerts.md)
#### <a name="other-resources"></a>Sonstige Ressourcen


  
    
    
 [Walkthrough: Developing a Custom Application Using Excel Web Services](walkthrough-developing-a-custom-application-using-excel-web-services.md)
