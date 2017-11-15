---
title: How to Deploy UDFs Using SharePoint Foundation Solutions
ms.date: 09/25/2017
keywords: how to,howdoi,howto,udf list,WSS Solutions
f1_keywords: how to,howdoi,howto,udf list,WSS Solutions
ms.prod: sharepoint
ms.assetid: 97751a6c-ef73-4d95-a3c4-98014d84ba48
ms.openlocfilehash: 9b259e58d4a503283098f5b96622e7d968ce99bc
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-deploy-udfs-using-sharepoint-foundation-solutions"></a>How to: Deploy UDFs Using SharePoint Foundation Solutions

This example shows how to deploy a user-defined function (UDF) DLL by using the Microsoft SharePoint Foundation solution framework.
  
    
    

The SharePoint Foundation solution framework lets you bundle all the components to extend SharePoint Foundation in a new file called a solution file (a CAB-based format with a .wsp extension). A solution is a deployable, reusable package that can contain a set of features, site definitions, and assemblies that you can apply to a site, and individually enable or disable. Additionally, you can use the solution file to deploy the contents of a Web Part package, including assemblies, class resources, .dwp files, and other package components. For more information about the SharePoint Foundation solution framework, see the SharePoint Foundation node in the  [Erste Schritte bei der Entwicklung für SharePoint Foundation](http://msdn.microsoft.com/library/ef1187aa-e007-4490-8191-db36a50b3ae4%28Office.15%29.aspx) (http://msdn.microsoft.com/de-DE/library/ee539432(office.14).aspx). The procedure for creating and deploying a UDF assembly by using SharePoint Foundation solution framework is as follows:
  
    
    


1. Create the solution manifest file, Manifest.xml.
    
    The solution manifest (always called Manifest.xml) is stored at the root of a solution file. This file defines the list of features, site definitions, resource files, Web Part files, and assemblies to be processed. It does not define the file structure; if files are included in a solution but not listed in the manifest XML file, they are not processed in any way.
    
    > **Hinweis:** Weitere Informationen zur Struktur der XML-Manifestdatei finden Sie in der Dokumentation zu SharePoint Foundation. 
2. Packen Sie die UDF-Assembly und die Datei „Manifest.xml“ in einer CAB-Datei.
    
  
3. Make sure that the SharePoint Foundation Administration service is running on the server.
    
  
4. Add the solution to the server by using stsadm.exe.
    
  
5. Deploy the solution by using stsadm.exe.
    
  
Jeder vertrauenswürdige Excel Services-Speicherort verfügt über ein **AllowUdfs**-Flag.
> **Hinweis:** Das **AllowUdfs**-Flag wird durch die Option **Benutzerdefinierte Funktionen sind zugelassen** auf der Seite „Vertrauenswürdige Dateispeicherorte von Excel Services“ bezeichnet. Informationen zum Navigieren zur Seite „Vertrauenswürdige Dateispeicherorte“ finden Sie in [Schritt 3: Bereitstellen und Aktivieren von UDFs](step-3-deploying-and-enabling-udfs.md). 
  
    
    

Damit UDFs von einem bestimmten vertrauenswürdigen Speicherort aufgerufen werden können, müssen Sie folgende Schritte ausführen:
- Set the **AllowUdfs** value to **true**. The default value is **false**. 
    
  
- Add the UDF assembly to the trusted UDF list to allow the UDF to be called from a workbook.
    
  
Weitere Informationen zum Aktivieren von UDFs und Hinzufügen von UDFs zur Liste vertrauenswürdiger UDFs finden Sie unter [Vorgehensweise: Aktivieren von UDFs](how-to-enable-udfs.md).
> **Hinweis:** Um Namenskonflikte zu vermeiden, weisen Sie Ihren UDF-Assemblys und deren Abhängigkeiten starke Namen zu, und benennen Sie sie so eindeutig wie möglich. Weitere Informationen finden Sie unter [Bewährte Methoden für Excel Services](excel-services-best-practices.md) und [Bekannte Probleme und Tipps für Excel Services](excel-services-known-issues-and-tips.md). 
  
    
    


## <a name="procedure"></a>Verfahren


### <a name="to-create-the-manifestxml-file"></a>To create the Manifest.xml file


1. Right-click your project in **Solution Explorer**, point to **Add**, and then click **New Item**.
    
  
2. Select **XML File**, and name the file Manifest.xml.
    
  
3. Klicken Sie auf **Hinzufügen**.
    
  
4. Fügen Sie der Datei den folgenden Inhalt hinzu:
    
```XML
  
<?xml version="1.0" encoding="utf-8" ?>
<Solution xmlns="http://schemas.microsoft.com/sharepoint/" SolutionId="{57568687-2CC0-45bf-B66A-2D50D57108CA}" DeploymentServerType="ApplicationServer">
  <Assemblies>
    <Assembly DeploymentTarget="GlobalAssemblyCache" Location="EcsUdfsCommonSet.dll"/>
  </Assemblies>
</Solution>
```


    > **Note:**
      > You should generate a unique GUID for each solution. For more information about **Solution** element, see the SharePoint Foundation [Solutions and Web Part Packages](http://msdn.microsoft.com/library/a145a5eb-fbb6-4328-b5b3-96bf5ce89a19%28Office.15%29.aspx) (http://msdn.microsoft.com/en-us/library/ms413687.aspx).

### <a name="to-create-a-solution-package"></a>So erstellen Sie ein Lösungspaket


- For information about how to create the solution file, see the "Creating a Solution" topic under the "Solutions and Web Part Packages" node in the SharePoint Foundation SDK. 
    
  

### <a name="to-verify-whether-sharepoint-foundation-administration-is-running"></a>To verify whether SharePoint Foundation Administration is running


1. Click **Start**, point to **Administrative Tools**, and then double-click **Services**. 
    
    The **Services** dialog box appears.
    
  
2. Make sure that the status of SharePoint Foundation Administration service shows **Started**. If it does not, right-click SharePoint Foundation Administration, and then select **Start**.
    
  

### <a name="to-add-the-solution"></a>To add the solution


1. Click **Start**, click **Run**, and then typecmd. 
    
    The command prompt console appears.
    
  
2. Run the following script to add the solution to SharePoint server: 
    
    stsadm.exe -o addsolution -filename <pathtoCAB>
    
    > **Hinweis:** Die Datei „Stsadm.exe“ finden Sie unter: > C:\\Programme\\Gemeinsame Dateien\\Microsoft Shared\\web server extensions\\12\\BIN. 

    > 
      >   **Hinweis:** Weitere Informationen zu Optionen des Befehls „Stsadm.exe“ finden Sie unter [Zuordnung von Stsadm-Vorgängen zu Windows PowerShell (SharePoint Foundation 2010)](http://technet.microsoft.com/en-us/library/ff621081.aspx) (http://technet.microsoft.com/de-de/library/ff621081.aspx).

  
    
    

### <a name="to-deploy-the-solution"></a>So stellen Sie die Lösung bereit


1. Click **Start**, click **Run**, and then typecmd. 
    
    The command prompt console appears.
    
  
2. Run the following script to deploy the solution to SharePoint server. 
    
    stsadm.exe -o deploysolution -name <filename of the CAB> -immediate -allowGacDeployment
    
    You should now see your UDF DLL in the global assembly cache.
    
  

## <a name="see-also"></a>Siehe auch


#### <a name="tasks"></a>Aufgaben


  
    
    
 [How to: Create a UDF That Calls a Web Service](how-to-create-a-udf-that-calls-a-web-service.md)
  
    
    
 [How to: Enable UDFs](how-to-enable-udfs.md)
  
    
    
 [How to: Restrict UDF Code Access Security Permissions](how-to-restrict-udf-code-access-security-permissions.md)
#### <a name="concepts"></a>Konzepte


  
    
    
 [Walkthrough: Developing a Managed-Code UDF](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [Frequently Asked Questions About Excel Services UDFs](frequently-asked-questions-about-excel-services-udfs.md)
  
    
    
 [Understanding Excel Services UDFs](understanding-excel-services-udfs.md)
