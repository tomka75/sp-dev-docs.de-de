---
title: Aktivieren von UDFs
ms.date: 09/25/2017
keywords: how to,howdoi,howto,UDF list
f1_keywords: how to,howdoi,howto,UDF list
ms.prod: sharepoint
ms.assetid: 8c1af2eb-bb22-45e1-82de-a2b4b53d7a26
ms.openlocfilehash: 6eb51af89ab003e507ec9acb2f81a70bf843ee99
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="enable-udfs"></a>Aktivieren von UDFs

Jeder vertrauenswürdiger Excel Services-Speicherort in dem Anbieter für gemeinsame Dienste verfügt ein **AllowUdfs**-Flag.
  
    
    


> **Hinweis:** Das **AllowUdfs**-Flag wird durch die Option **Benutzerdefinierte Funktionen sind zugelassen** auf der Seite „Vertrauenswürdige Dateispeicherorte von Excel Services“ bezeichnet.
  
    
    


The default **AllowUdfs** value is **false**. If the **AllowUdfs** value is set to **false** in a particular trusted location, the workbooks in that trusted location are not allowed to call UDFs.
  
    
    

In order to allow UDFs to be called from a specific trusted location, you set the **AllowUdfs** value to **true**.If the **AllowUdfs** value is **false** when a session is started on a workbook that has UDF calls in this trusted location, the UDF calls will fail. If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session, after the configuration database has been updated.You can get around this by restarting the sessionfor example, by selecting **Reload Workbook** in Excel Web Access.
> **Vorsicht** Wenn Sie stattdessen die Microsoft-Internetinformationsdienste (IIS) zurücksetzen, werden alle aktuelle Sitzungen beendet. 
  
    
    


## <a name="enabling-udfs"></a>Aktivieren von UDFs

To do the following steps, you need a computer that has Microsoft SharePoint Server 2010 installed.
  
    
    

### <a name="to-enable-udfs"></a>To enable UDFs


1. On the **Start** menu, click **All Programs**. 
    
  
2. Point to **Microsoft Office Server** and click **SharePoint Central Administration**. 
    
  
3. On the Quick Launch, click your Shared Services Provider (SSP) linkfor example, "SharedServices1"to view the Shared Services home page for that particular SSP.
    
  
4. Under **Excel Services Settings**, click **User-defined functions**. 
    
  
5. On the Excel Services User-Defined Functions page, click **Add User-Defined Function** to open the Excel Services Add User-Defined Function Assembly page.
    
  
6. In the **Assembly** box, type the path to the UDF assembly. For example,C:\\MyUdfFolder\\MyUdf.dll.
    
  
7. Klicken Sie unter **Assemblyspeicherort** auf **Lokale Datei**.
    
    > **Hinweis:** Die Option **Lokale Datei** wird in künftigen Versionen von Excel Services durch **Dateipfad** ersetzt. Wählen Sie dann stattdessen „Dateipfad“ aus. Wenn **Dateipfad** angezeigt wird, wählen Sie dies aus. 
8. Standardmäßig sollte unter **Assembly aktivieren** das Kontrollkästchen **Assembly aktiviert** aktiviert sein.
    
  
9. Klicken Sie auf **OK**.
    
  

## <a name="allowing-udf-calls"></a>Allowing UDF Calls


### <a name="to-allow-udfs-to-be-called-from-a-workbook"></a>To allow UDFs to be called from a workbook


1. Open the Excel Services Add Trusted File Location page (if you are adding a new trusted location) or Excel Services Edit Trusted File Location page (if you are editing an existing trusted location). 
    
    > **Hinweis:** Weitere Informationen zum Festlegen eines vertrauenswürdigen Speicherorts finden Sie unter [Gewusst wie: Festlegen eines vertrauenswürdigen Speicherorts](how-to-trust-a-location.md). 
2. Wählen Sie unter **Benutzerdefinierte Funktionen zulassen** die Option **Benutzerdefinierte Funktionen sind zugelassen**, damit UDFs von einer Arbeitsmappe in diesem vertrauenswürdigen Speicherort aufgerufen werden können.
    
  
3. Klicken Sie auf **OK**.
    
  

## <a name="see-also"></a>Siehe auch


#### <a name="tasks"></a>Aufgaben


  
    
    
 [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [How to: Create a UDF That Calls a Web Service](how-to-create-a-udf-that-calls-a-web-service.md)
  
    
    
 [How to: Trust a Location](how-to-trust-a-location.md)
#### <a name="concepts"></a>Konzepte


  
    
    
 [Walkthrough: Developing a Managed-Code UDF](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [Frequently Asked Questions About Excel Services UDFs](frequently-asked-questions-about-excel-services-udfs.md)
  
    
    
 [Understanding Excel Services UDFs](understanding-excel-services-udfs.md)
  
    
    
 [Excel Services Alerts](excel-services-alerts.md)
  
    
    
 [Excel Services Known Issues and Tips](excel-services-known-issues-and-tips.md)
  
    
    
 [Excel Services Best Practices](excel-services-best-practices.md)
