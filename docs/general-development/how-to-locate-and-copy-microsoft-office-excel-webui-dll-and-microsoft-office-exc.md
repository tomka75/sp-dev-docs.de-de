---
title: How to Locate and Copy Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll
ms.date: 09/25/2017
keywords: how to,howdoi,howto,WebUI DLL
f1_keywords: how to,howdoi,howto,WebUI DLL
ms.prod: sharepoint
ms.assetid: 09ad5d5e-1678-45e4-8159-23ef56f84215
ms.openlocfilehash: 2b2f649329835a9ccdde92a07ab5f443f8fa1716
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-locate-and-copy-microsoftofficeexcelwebuidll-and-microsoftofficeexcelwebuiinternaldll"></a>How to: Locate and Copy Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll

If you want to programmatically add an Excel Web Access Web Part to a SharePoint page and programmatically change the Excel Web Access Web Part, you must add a reference to the required SharePoint DLLs. For example: 
  
    
    


- Microsoft.Office.Excel.WebUI.dll
    
  
- Microsoft.Office.Excel.WebUI.Internal.dll
    
  
- Microsoft.SharePoint.dll
    
  

On the computer running Microsoft SharePoint Server 2010, you can find a copy of Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll in the global assembly cache. Before you can add a reference to Microsoft.Office.Excel.WebUI.dll by using the **Add Reference** dialog box in Microsoft Visual Studio, you must first copy Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll from the global assembly cache to a folder. Then, you can use the **Browse** tab in the **Add Reference** dialog box to browse to the folder that contains the copy of Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll.
  
    
    

The following steps show how to: 
- Locate Microsoft.Office.Excel.WebUI.dll. 
    
  
- Kopieren Sie die Microsoft.Office.Excel.WebUI.dll aus dem globalen Assemblycache in einen beliebigen Ordner.
    
  

> **Hinweis:** Wiederholen Sie die Schritte zum Kopieren der Microsoft.Office.Excel.WebUI.Internal.dll aus dem globalen Assemblycache in einen Ordner. 
  
    
    


### <a name="to-locate-microsoftofficeexcelwebuidll"></a>So suchen Sie nach der Microsoft.Office.Excel.WebUI.dll


1. To start the command-prompt console, click **Start**, and then click **Run**. 
    
  
2. In the **Open** field text box, typecmd. 
    
    The command-prompt console appears.
    
  
3. Verwenden Sie den **cd**-Befehl, um zum Verzeichnis „C:\\Windows\\assembly“ zu navigieren:
    
    > **Hinweis:** Die Verzeichnisstruktur auf Ihrem Computer kann möglicherweise abweichen. In diesem Beispiel wird ein Computer mit Windows Server 2008 verwendet. 

```
  
cd C:\\Windows\\assembly
```

4. Verwenden Sie den **dir**-Befehl zum Anzeigen der Inhalte im Verzeichnis „C:\\Windows\\assembly“:
    
```
  C:\\Windows\\assembly>dir
```


    You will see contents similar to the following:
    


```
  Volume in drive C has no label.
 
 Directory of C:\\Windows\\assembly

02/20/2010  09:22 AM    <DIR>          GAC
02/20/2010  09:39 AM    <DIR>          GAC_32
02/20/2010  09:32 AM    <DIR>          GAC_64
02/22/2010  05:05 PM    <DIR>          GAC_MSIL
02/22/2010  05:35 PM    <DIR>          NativeImages_v2.0.50727_32
02/22/2010  04:33 PM    <DIR>          NativeImages_v2.0.50727_64
02/20/2010  10:34 AM    <DIR>          NativeImages_v4.0.30219_32
02/20/2010  10:35 AM    <DIR>          NativeImages_v4.0.30219_64
02/22/2010  05:04 PM    <DIR>          temp
02/22/2010  05:05 PM    <DIR>          tmp
               0 File(s)              0 bytes
              10 Dir(s)  104,032,665,600 bytes free
```

5. Use the **cd** command again to change the directory and navigate to the gac_msil directory:
    
```
  
C:\\Windows\\assembly>cd gac_msil
```

6. Use the **dir** command to display the content of the "C:\\Windows\\assembly\\GAC_MSIL" directory:
    
```
  C:\\Windows\\assembly\\GAC_MSIL>dir
```


    You will see contents similar to the following:
    


```
  Volume in drive C has no label.
Directory of C:\\Windows\\assembly\\GAC_MSIL
...
02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.Server.Udf
02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.Server.WebServices

02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.WebUI
02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.WebUI.Internal
...
02/20/2010  07:57 AM    <DIR>          Microsoft.SharePoint
...
0 File(s)              0 bytes
             739 Dir(s)  100,594,409,472 bytes free
```

7. Now that you have located Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll, you can copy them to a folder of your choice.
    
  

### <a name="to-copy-microsoftofficeexcelwebuidll"></a>To copy Microsoft.Office.Excel.WebUI.dll


1. Use the **cd** command again to change the directory to "Microsoft.Office.Excel.WebUI":
    
```
  
C:\\Windows\\assembly\\GAC_MSIL>cd Microsoft.Office.Excel.WebUI 
```

2. Use the **dir** command to display the contents:
    
```
  C:\\Windows\\assembly\\GAC_MSIL\\Microsoft.Office.Excel.WebUI>dir
```


    You will see contents similar to the following:
    


```
  Volume in drive C has no label.
Directory of C:\\Windows\\assembly\\GAC_MSIL\Microsoft.Office.Excel.WebUI

02/20/2010  07:57 AM    <DIR>          .
02/20/2010  07:57 AM    <DIR>          ..
02/20/2010  07:57 AM    <DIR>          14.0.0.0__71e9bce111e9429c
               0 File(s)              0 bytes
               3 Dir(s)  104,006,115,328 bytes free
```

3. Use the **cd** command again to change the directory:
    
```
  
C:\\Windows\\assembly\\GAC_MSIL\\Microsoft.Office.Excel.WebUI>cd 14.0.0.0__71e9bce111e9429c
```

4. Use the **copy** command to copy Microsoft.Office.Excel.WebUI.dll to a folder of your choice.
    
    In the following example, Microsoft.Office.Excel.WebUI.dll is copied to "C:\\WebUIAssembly", where "C:\\WebUIAssembly" is a folder that you created previously:
    


```
  C:\\Windows\\assembly\\GAC_MSIL\\Microsoft.Office.Excel.WebUI\\14.0.0.0__71e9bce111e9429c>copy Microsoft.Office.Excel.WebUI.dll c:\\WebUIAssembly
        1 file(s) copied.
```


## <a name="example"></a>Beispiel

The following is an example of the result of using the command prompt to locate and copy Microsoft.Office.Excel.WebUI.dll to a folder.
  
    
    

```

C:\\Windows\\assembly>dir
Volume in drive C has no label.
Directory of C:\\Windows\\assembly

02/20/2010  09:22 AM    <DIR>          GAC
02/20/2010  09:39 AM    <DIR>          GAC_32
02/20/2010  09:32 AM    <DIR>          GAC_64
02/22/2010  05:05 PM    <DIR>          GAC_MSIL
02/22/2010  05:35 PM    <DIR>          NativeImages_v2.0.50727_32
02/22/2010  04:33 PM    <DIR>          NativeImages_v2.0.50727_64
02/20/2010  10:34 AM    <DIR>          NativeImages_v4.0.30219_32
02/20/2010  10:35 AM    <DIR>          NativeImages_v4.0.30219_64
02/22/2010  05:04 PM    <DIR>          temp
02/22/2010  05:05 PM    <DIR>          tmp
               0 File(s)              0 bytes
              10 Dir(s)  104,032,665,600 bytes free
C:\\Windows\\assembly>cd gac_msil

C:\\Windows\\assembly\\GAC_MSIL>dir
 Volume in drive C has no label.
 Directory of C:\\Windows\\assembly\GAC_MSIL
...
02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.Server.Udf
02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.Server.WebServices

02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.WebUI
02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.WebUI.Internal
...

C:\\Windows\\assembly\\GAC_MSIL>cd Microsoft.Office.Excel.WebUI

C:\\Windows\\assembly\\GAC_MSIL\\Microsoft.Office.Excel.WebUI>dir
 Volume in drive C has no label.
Directory of C:\\Windows\\assembly\\GAC_MSIL\Microsoft.Office.Excel.WebUI

02/20/2010  07:57 AM    <DIR>          .
02/20/2010  07:57 AM    <DIR>          ..
02/20/2010  07:57 AM    <DIR>          14.0.0.0__71e9bce111e9429c
               0 File(s)              0 bytes
               3 Dir(s)  104,006,115,328 bytes free

C:\\Windows\\assembly\\GAC_MSIL\\Microsoft.Office.Excel.WebUI>cd 14.0.0.0__71e9bce111e9429c

C:\\Windows\\assembly\\GAC_MSIL\\Microsoft.Office.Excel.WebUI\\14.0.0.0__71e9bce111e9429c>copy Microsoft.Office.Excel.WebUI.dll c:\\WebUIAssembly
        1 file(s) copied.

C:\\Windows\\assembly\\GAC_MSIL\\Microsoft.Office.Excel.WebUI\\14.0.0.0__71e9bce111e9429c>
```


## <a name="see-also"></a>Siehe auch


#### <a name="tasks"></a>Aufgaben


  
    
    
 [How to: Programmatically Add an Excel Web Access Web Part to a Page](how-to-programmatically-add-an-excel-web-access-web-part-to-a-page.md)
  
    
    
 [How to: Trust a Location](how-to-trust-a-location.md)
#### <a name="concepts"></a>Konzepte


  
    
    
 [Excel Services Alerts](excel-services-alerts.md)
  
    
    
 [Excel Services Known Issues and Tips](excel-services-known-issues-and-tips.md)