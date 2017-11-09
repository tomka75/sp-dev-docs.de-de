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
# <a name="step-1-creating-a-ecmascript-text-file"></a><span data-ttu-id="a9fcc-102">Step 1: Creating a ECMAScript Text File</span><span class="sxs-lookup"><span data-stu-id="a9fcc-102">Step 1: Creating a ECMAScript Text File</span></span>

<span data-ttu-id="a9fcc-p101">Für diese exemplarische Vorgehensweise werden Sie eine ECMAScript (JavaScript, JScript)-Textdatei erstellen. Es wird davon ausgegangen, dass Sie mit dem Codieren in JavaScript vertraut sind.</span><span class="sxs-lookup"><span data-stu-id="a9fcc-p101">For this walkthrough, you will create an ECMAScript (JavaScript, JScript) text file. This walkthrough assumes that you are familiar with coding in JavaScript.</span></span> 
  
    
    


### <a name="to-create-an-ecmascript-text-file"></a><span data-ttu-id="a9fcc-105">So erstellen Sie eine ECMAScript-Textdatei</span><span class="sxs-lookup"><span data-stu-id="a9fcc-105">To create an ECMAScript text file</span></span>


1. <span data-ttu-id="a9fcc-106">Erstellen Sie eine Textdatei und nennen Sie sie JSOM_FeedToContentEditor.txt.</span><span class="sxs-lookup"><span data-stu-id="a9fcc-106">Create a text file and name it JSOM_FeedToContentEditor.txt.</span></span>
    
  
2. <span data-ttu-id="a9fcc-107">Fügen Sie das folgende Skript zur Datei „JSOM_FeedToContentEditor.txt“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="a9fcc-107">Add the following script to the JSOM_FeedToContentEditor.txt file.</span></span>
    
    <span data-ttu-id="a9fcc-108">**Beispielcode von:** Vidya Joshi, Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="a9fcc-108">**Sample code provided by:** Vidya Joshi, Microsoft Corporation.</span></span>
    


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

3. <span data-ttu-id="a9fcc-109">Speichern Sie die Textdatei.</span><span class="sxs-lookup"><span data-stu-id="a9fcc-109">Save the text file.</span></span>
    
  

### <a name="to-save-the-text-file-to-a-trusted-document-library"></a><span data-ttu-id="a9fcc-110">So speichern Sie die Textdatei in einer vertrauenswürdigen Dokumentbibliothek</span><span class="sxs-lookup"><span data-stu-id="a9fcc-110">To save the text file to a trusted document library</span></span>


1. <span data-ttu-id="a9fcc-111">Laden Sie die im vorherigen Verfahren erstellte Textdatei in eine vertrauenswürdige SharePoint-Dokumentbibliothek hoch.</span><span class="sxs-lookup"><span data-stu-id="a9fcc-111">Upload the text file that you created in the previous procedure to a trusted SharePoint document library.</span></span> 
    
  
2. <span data-ttu-id="a9fcc-p102">Beachten Sie die URL zu der Textdatei. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="a9fcc-p102">Note the URL to the text file. For example:</span></span>
    
     <span data-ttu-id="a9fcc-114">`http://` _meinserver_ `/Docs/Documents/JSOM_FeedToContentEditor.txt`</span><span class="sxs-lookup"><span data-stu-id="a9fcc-114">`http://` _myserver_ `/Docs/Documents/JSOM_FeedToContentEditor.txt`</span></span>
    
    <span data-ttu-id="a9fcc-115">Im nächsten Verfahren benötigen Sie diese URL für den Feed zum Inhalts-Editor-Webpart.</span><span class="sxs-lookup"><span data-stu-id="a9fcc-115">In the next procedure, you will need this URL to feed to the Content Editor Web Part.</span></span>
    
  

