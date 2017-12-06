---
title: How to Trust a Location
ms.date: 09/25/2017
keywords: how to,howdoi,howto,trusted location
f1_keywords: how to,howdoi,howto,trusted location
ms.prod: sharepoint
ms.assetid: 0f396c0b-f578-4d1a-9e6b-a75f352265ab
ms.openlocfilehash: 9c769a0d046a112253a61265373355eece0dade9
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-trust-a-location"></a>How to: Trust a Location

Workbooks that you want to access must be placed in a trusted location. If they are not, calls to open the workbooks will fail. This example shows you how to trust a location by using the SharePoint Central Administration page. 
  
    
    

You can also trust a location by using Windows PowerShell. For more information, see the Microsoft SharePoint Server 2010 IT Pro and administration documentation on  [TechNet](http://technet.microsoft.com/en-us/library/ee428287%28office.14%29.aspx). 
> **Tipp:** Weitere Informationen über die Administrationsverbesserung und das Anzeigen von Screenshots der Seite Trusted File Locations finden Sie im Blog-Eintrag [Administrationsverbesserungen für Excel Services in SharePoint 2010](http://blogs.msdn.com/excel/archive/2009/11/16/excel-services-in-sharepoint-2010-administration-improvements.aspx). 
  
    
    


### <a name="to-trust-a-location"></a>Vertrauen zu einem Speicherort


1. On the **Start** menu, click **All Programs**. 
    
  
2. Point to **Microsoft SharePoint 2010 Products**, and then click **SharePoint 2010 Central Administration**. 
    
  
3. On the SharePoint 2010 Central Administration page, under **Application Management**, click **Manage service applications**.
    
  
4. On the Manage Service Application page, click **Excel Services Application**.
    
  
5. On the Manage Excel Services Application page, click **Trusted File Locations**. 
    
  
6. On the Excel Services Application Trusted File Locations page, click **Add Trusted File Location**. 
    
  
7. On the Excel Services Application Add Trusted File Location page, in the **Address** text box, type the location to save your workbookfor example,http:// _MyServer002_/Shared%20Documents. 
    
  
8. Under **Location type**, click the appropriate location type. In this example, select **SharePoint Foundation**.
    
  
9. Under **Trust Children**, select **Children trusted** if you want to trust child libraries or directories.
    
  
10. Klicken Sie auf **OK**.
    
  

## <a name="see-also"></a>Siehe auch


#### <a name="tasks"></a>Aufgaben


  
    
    
 [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [How to: Save from Excel Client to the Server](how-to-save-from-excel-client-to-the-server.md)
#### <a name="concepts"></a>Konzepte


  
    
    
 [Excel Services Alerts](excel-services-alerts.md)
#### <a name="other-resources"></a>Sonstige Ressourcen


  
    
    
 [Walkthrough: Developing a Custom Application Using Excel Web Services](walkthrough-developing-a-custom-application-using-excel-web-services.md)