---
title: Arbeiten mit dem Excel Services-JavaScript-Objektmodell
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 06219071-a7c1-4f54-b07f-7b7001592330
ms.openlocfilehash: 9bf873dad64b0dedc3d4676646594d70ec3815a7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="working-with-the-excel-services-javascript-object-model"></a>Arbeiten mit dem Excel Services-JavaScript-Objektmodell

Wenn Sie Code mit dem JavaScript-Objektmodell (JSOM) schreiben, gibt es zwei Szenarien, in denen der Code ausgeführt werden kann: Auf einer SharePoint-Seite oder auf einer Host-Webseite mit einer eingebetteten Arbeitsmappe, die auf Microsoft OneDrive gespeichert ist. Dieser Artikel erläutert die Hauptunterschiede zwischen den beiden Szenarien, die sich erheblich auf das Schreiben des Codes auswirken.
  
    
    


## <a name="using-the-excel-services-jsom"></a>Verwenden des Excel Services-JSOM

In Tabelle 1 sind die Unterschiede zwischen den beiden Szenarien aufgeführt, die verfügbar sind, wenn Sie Code mit dem JSOM schreiben.
  
    
    

**Tabelle 1. Szenarien für Excel Services JSOM**


|**Ort**|**Beschreibung**|
|:-----|:-----|
|**OneDrive** <br/> |In diesem Szenario betten Sie eine Arbeitsmappe, die auf OneDrive gespeichert ist, in die Host-Webseite mit einem HTML-Element <div> ein. Dann fügen Sie Code in die Seite ein, die mit der eingebetteten Arbeitsmappe interagiert.  <br/> |
|**SharePoint** <br/> |In diesem Szenario wird eine SharePoint-Seite von SharePoint bereitgestellt. Sie fügen ein Webpart in die SharePoint-Seite ein, das eine an einem vertrauenswürdigen Speicherort gespeicherte Arbeitsmappe enthält. Dann fügen Sie Code in die SharePoint-Seite ein, die mit dem Webpart interagiert.  <br/> |
   
Der Hauptunterschied beim Schreiben von Code für die beiden Szenarien liegt im Abrufen des Verweises zum Objekt [Ewa.EwaControl](http://msdn.microsoft.com/library/6e441406-d67a-0da9-f996-71f4e4b4c144%28Office.15%29.aspx). Da **[Ewa.EwaControl]** der Einstiegspunkt zum JavaScript-Objektmodell ist, müssen Sie einen Verweis für die Zusammenarbeit mit dem JSOM herstellen.
  
    
    

### <a name="getting-a-reference-to-the-ewacontrol-object-sharepoint"></a>Abrufen eines Verweises auf das Objekt EwaControl (SharePoint)

Wenn Sie Code schreiben, der mit einem Webpart auf einer SharePoint-Seite interagiert, erhalten Sie einen Verweis auf das Objekt **[Ewa.EwaControl]**, indem Sie die Methode [Ewa.EwaControlCollection.getItem(index)](http://msdn.microsoft.com/library/11dd3a65-f914-4b34-bbaf-0206c8153d2b%28Office.15%29.aspx) wie im folgenden Codebeispiel gezeigt verwenden.
  
    
    

```

<script type="text/javascript">
var ewa = null;

// Add event handler for onload event.
if (window.attachEvent) 
{ 
    window.attachEvent("onload", ewaOmPageLoad);    
} 
else 
{ 
    window.addEventListener("DOMContentLoaded", ewaOmPageLoad, false); 
}
// Add event handler for applicationReady event.
function ewaOnPageLoad()
{
    if (typeof (Ewa) != "undefined")
    {
Ewa.EwaControl.add_applicationReady(ewaApplicationReady);
    }
    else
    {
alert("Error - the EWA is not loaded.");
    }
    // Add additional page load code here.
}

function ewaApplicationReady()
{
    // Get a reference to the Excel Services Web Part.
    ewa = Ewa.EwaControl.getInstances().getItem(0);

    // Add other initialization logic here.
}

// Add your code here.
    </script>
```


### <a name="getting-a-reference-to-the-ewacontrol-object-onedrive"></a>Abrufen eines Verweises auf das Objekt EwaControl (OneDrive)

Wenn Sie Code schreiben, der mit einer eingebetteten Arbeitsmappe interagiert, die auf OneDrive gespeichert ist, erhalten Sie einen Verweis auf das Objekt **[Ewa.EwaControl]** mithilfe des Objekts [AsyncResult](http://msdn.microsoft.com/library/1da51396-834c-d85b-a9b0-ce21e4329946%28Office.15%29.aspx). Das Objekt **[AsyncResult]** wird in einem einzigen Parameter an die Rückrufmethode übergeben, die Sie in der statischen Methode [Ewa.EwaControl.loadEwaAsync](http://msdn.microsoft.com/library/a7ee4d6d-5472-b942-c78e-b368d30bcb0e%28Office.15%29.aspx) angegeben haben. Wenn der Rückruf aufgerufen wird, ist ein Verweis auf das Objekt **[Ewa.EwaControl]** im Objekt **[AsyncResult]** enthalten. Das folgende Codebeispiel zeigt, wie Sie einen Verweis auf das Objekt **[Ewa.EwaControl]** über das Objekt **[AsyncResult]** erhalten.
  
    
    

```

<div id="myExcelDiv" style="width: 402px; height: 346px"></div>
<script type="text/javascript" src="http://r.office.microsoft.com/r/rlidExcelWLJS?v=1&amp;kip=1"></script>
<script type="text/javascript">
    /*
    * This code uses the Microsoft Office Excel JavaScript object model to programmatically insert the
    * Excel Web App into a div with id=myExcelDiv. The full API is documented at
    * http://msdn.microsoft.com/en-us/library/hh315812.aspx. There you can find out how to programmatically get
    * values from your Excel file and how to use the rest of the object model. 
    */

    // Use this file token to reference Book1.xlsx in the Excel APIs
    // Replace the the placeholder for the  filetoken with your value
    var fileToken = " XXXXXXXXXXXXXXXXXXXXXX/XXXXXXXXXXXXXXXXXXX/";
    var ewa = null;

    // Run the Excel load handler on page load.
    if (window.attachEvent)
    {
        window.attachEvent("onload", loadEwaOnPageLoad);
    } else
    {
        window.addEventListener("DOMContentLoaded", loadEwaOnPageLoad, false);
    }

    function loadEwaOnPageLoad()
    {
        var props = {
            uiOptions: {
                showGridlines: false,
                showRowColumnHeaders: false,
                showParametersTaskPane: false
            },
            interactivityOptions: {
                allowTypingAndFormulaEntry: false,
                allowParameterModification: false,
                allowSorting: false,
                allowFiltering: false,
                allowPivotTableInteractivity: false
            }
        };
        // Embed workbook using loadEwaAsync
        Ewa.EwaControl.loadEwaAsync(fileToken, "myExcelDiv", props, onEwaLoaded);
    }

    function onEwaLoaded(asyncResult)
    { 
        if (asyncResult.getSucceeded())
        {
            // Use the AsyncResult.getEwaControl() method to get a reference to the EwaControl object
            ewa = asyncResult.getEwaControl();
            …
        }
        else
        {
            alert("Async operation failed!");
        }
        // ...
    }    
</script>
```


### <a name="conclusion"></a>Schlussbemerkung

Das Schreiben eines Entwurfs mithilfe des JavaScript-Objektmodells ist für SharePoint und eine Host-Webseite im Wesentlichen identisch. Der Hauptunterschied besteht im Abrufen des Objekts **[Ewa.EwaControl]**. Wenn Sie über einen Verweis zum Objekt **[Ewa.EwaControl]** verfügen, ist der Rest des Codes, den Sie schreiben, für beide Szenarien etwa gleich.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15DevKitchenCon_AnatomyofanappSignupsheets_Additionalresources"> </a>


-  
  [Verwenden der Excel Services-JavaScript-API zum Arbeiten mit eingebetteten Excel-Arbeitsmappen](http://msdn.microsoft.com/en-us/library/hh315812.aspx)
    
  
-  [Ewa.EwaControl.loadEwaAsync](http://msdn.microsoft.com/library/a7ee4d6d-5472-b942-c78e-b368d30bcb0e%28Office.15%29.aspx)
    
  
-  [Ewa.EwaControlCollection.getItem(index)](http://msdn.microsoft.com/library/11dd3a65-f914-4b34-bbaf-0206c8153d2b%28Office.15%29.aspx)
    
  

