---
title: Step 1 Creating a ECMAScript Text File
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f1c2b359-5b0d-467d-a863-6732e23863b9
ms.openlocfilehash: b77d09f9aded3cd5dfca8c76413be8139fce1714
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="step-1-creating-a-ecmascript-text-file"></a>Step 1: Creating a ECMAScript Text File

Für diese exemplarische Vorgehensweise werden Sie eine ECMAScript (JavaScript, JScript)-Textdatei erstellen. Es wird davon ausgegangen, dass Sie mit dem Codieren in JavaScript vertraut sind. 
  
    
    


### <a name="to-create-an-ecmascript-text-file"></a>So erstellen Sie eine ECMAScript-Textdatei


1. Erstellen Sie eine Textdatei und nennen Sie sie JSOM_FeedToContentEditor.txt.
    
  
2. Fügen Sie das folgende Skript zur Datei „JSOM_FeedToContentEditor.txt“ hinzu.
    
    **Beispielcode von:** Vidya Joshi, Microsoft Corporation.
    


```
  
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html>
 <head>Logging results:
 </head>
<body>
<div id='resultdiv'></div>
<script type="text/javascript">         

// Set the page event handlers for onload and unload.
if (window.attachEvent) 
{
    window.attachEvent("onload", Page_Load);
} 
else 
{
// For some browsers window.attachEvent does not exist.
    window.addEventListener("DOMContentLoaded", Page_Load, false);
}

// Load the page. 
function Page_Load() 
{
    Ewa.EwaControl.add_applicationReady(GetEwa);
}

function GetEwa()
{
    om =Ewa.EwaControl.getInstances().getItem(0);
    writelog('DomId:' + om.getDomElement().id,0);

    om.add_activeCellChanged(cellchanged);
    om.add_activeSelectionChanged(selChanged);
    om.add_gridSynchronized(gridSynchronized);
    om.add_workbookChanged(wbchanged);
    om.add_enteredCellEditing(editing);
}

function cellchanged(rangeArgs)
{
    writelog('Address:'+ rangeArgs.getRange().getAddressA1(),1);
    writelog('Value:' + rangeArgs.getFormattedValues(),1);
    writelog('Cell changed event triggered',0);
}

function selChanged(rangeArgs)
{
    writelog('Address:'+ rangeArgs.getRange().getAddressA1(),1);
    writelog('Value:' + rangeArgs.getFormattedValues(),1);
    writelog('Selection changed event triggered',0);
}

function gridSynchronized(res)
{
    writelog('WorkbookPath:' +om.getActiveWorkbook().getWorkbookPath(),1);
    writelog('grid synchronized',0);
}

function wbchanged(r)
{
    writelog('Workbook changed event triggered',0);
}

function editing(rangeArgs)
{
    writelog('Address:'+ rangeArgs.getRange().getAddressA1(),1);
    writelog('Value:' + rangeArgs.getFormattedValues(),1);
    writelog('Entered cell editing event triggered',0);
}

function writelog(output, indentLevel)
{
    output = output + "<br/>";
    document.getElementById('resultdiv').innerHTML = output + document.getElementById('resultdiv').innerHTML ;
}
</script>  
</body>
</html><html> 

```

3. Speichern Sie die Textdatei.
    
  

### <a name="to-save-the-text-file-to-a-trusted-document-library"></a>So speichern Sie die Textdatei in einer vertrauenswürdigen Dokumentbibliothek


1. Laden Sie die im vorherigen Verfahren erstellte Textdatei in eine vertrauenswürdige SharePoint-Dokumentbibliothek hoch. 
    
  
2. Beachten Sie die URL zu der Textdatei. Beispiel:
    
     `http://` _meinserver_ `/Docs/Documents/JSOM_FeedToContentEditor.txt`
    
    Im nächsten Verfahren benötigen Sie diese URL für den Feed zum Inhalts-Editor-Webpart.
    
  

